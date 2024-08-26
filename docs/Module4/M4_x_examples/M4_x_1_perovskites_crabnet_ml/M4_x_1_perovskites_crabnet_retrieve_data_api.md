# Compositional Based Property Prediction of Perovskites with CrabNet

This tutorial demonstrates how to use [CrabNet](https://github.com/sparks-baird/CrabNet) to predict the bandgap of perovskites using data from the [Perovskite Database](https://www.nature.com/articles/s41560-021-00941-3) available in NOMAD for training.

*Authored by José A. Márquez, et al.*

The presented example here is based on the Jupyter notebook ``crabnet-perovskite-bandgap-prediction.ipynb``  by *José A. Márquez, et al.* and can be found in NOMAD using the entry_id ``Should Ask Pepe for Permission and ID``. To follow along, you might either download the notebook and run the cells, or copy and paste the code snippets given here onto a jupyter notebook and run them. 


## Imports

We will start by running a couple of pip installers and importing the necessary libraries.

```python
! pip install torch
! pip install crabnet
! pip install pandas
```
Then import necessary libraries:
```python
from crabnet.crabnet_ import CrabNet
import numpy as np
from crabnet.utils.data import groupby_formula
import nest_asyncio
import pandas as pd
nest_asyncio.apply()

```

## Fetch Data using NOMAD API

In this section, we will fetch some perovskite solar cell data from the NOMAD API. This can be skipped if you already have the data available.

You can use your password if you need to access unpublished data from your uploads. If your screen is being shared or recorded, you probably want to hide your password when typing it. For this you might use the ``getpass`` library among other options:

```python
import getpass
password = getpass.getpass()
```
Then, use the password to get data in which you have visibility. In the following code snippet, you authenticate yourself with ``yourusername`` and the password you gave above and get an access tocken:

```python
response = requests.get(
    'https://nomad-lab.eu/prod/v1/staging/api/v1/auth/token', 
    params=dict(username='yourusername', password=password))
token = response.json()['access_token']
```
In your API query, pass this token in the request:

```python
while True:
  data = requests.post(f'{base_url}/entries/archive/query', 
                       headers={'Authorization': f'Bearer {token}'}, 
                       json={...})
```

Now, let’s retrieve some data from the NOMAD API and save it to a file. This is a one-time operation. If you already have the data (e.g., you have already gone through this section and saved the data file), you can skip this step.

```python
import requests

base_url = 'https://nomad-lab.eu/prod/v1/api/v1'

def extract_values(entry):
  try:
    bandgaps.append(entry['results']['properties']['electronic']['band_structure_electronic'][0]['band_gap'][0]['value'])
  except:
    bandgaps.append('None')
  try:
    reduced_formulas.append(entry['results']['material']['chemical_formula_reduced'])
    iupac_formulas.append(entry['results']['material']['chemical_formula_iupac'])
    descriptive_formulas.append(entry['results']['material']['chemical_formula_descriptive'])
  except:
    reduced_formulas.append('None')
    iupac_formulas.append('None')
    descriptive_formulas.append('None')
  try:
    vocs.append(entry['results']['properties']['optoelectronic']['solar_cell']['open_circuit_voltage'])
  except:
    vocs.append('None')
  try:
    jscs.append(entry['results']['properties']['optoelectronic']['solar_cell']['short_circuit_current_density'])
  except:
    jscs.append('None')
  try:
    ffs.append(entry['results']['properties']['optoelectronic']['solar_cell']['fill_factor'])
  except:
    ffs.append('None')
  try:
    pces.append(entry['results']['properties']['optoelectronic']['solar_cell']['efficiency'])
  except:
    pces.append('None')
  try:
    device_stack.append(entry['results']['properties']['optoelectronic']['solar_cell']['device_stack'])
  except:
    device_stack.append('None')
  try:
    htl.append(entry['results']['properties']['optoelectronic']['solar_cell']['hole_transport_layer'])
  except:
    htl.append('None')
  try:
    etl.append(entry['results']['properties']['optoelectronic']['solar_cell']['electron_transport_layer'])
  except:
    etl.append('None')
  try:
    structural_dimensionality.append(entry['results']['material']['structural_type'])
  except:
    structural_dimensionality.append('None')
  return bandgaps, reduced_formulas, iupac_formulas, descriptive_formulas, vocs, jscs, ffs, pces, device_stack, htl, etl, structural_dimensionality

bandgaps =[]
vocs = []
jscs = []
ffs = []
pces = []
reduced_formulas = []
iupac_formulas = []
descriptive_formulas = []
htl = []
etl = []
device_stack = []
structural_dimensionality = []
page_after_value = None

while True:
  data = requests.post(f'{base_url}/entries/query', json={
    "owner": "visible",
    "aggregations": {},
    "query": {
      "and": [
        {"results.material.elements:all": ["Sn"]},
        {"sections:all": ["nomad.datamodel.results.SolarCell"]},
        # {"quantities:all": [
        #   "results.properties.electronic.band_structure_electronic.band_gap.value"
        # ]}
        ]},

    'required': {
    #   'data':{
    # },
      'results':{
          'material': {
              'chemical_formula_reduced':'*',
              'structural_type':'*' },
          'properties': {
              'optoelectronic':{
                  'band_gap':'*',
                  'solar_cell':{
                      'open_circuit_voltage':'*',
                      'short_circuit_current_density':'*',
                      'fill_factor':'*',
                      'efficiency':'*',
                      }}},},
      },
    'pagination': {'page_size': 1000,
                   'page_after_value': page_after_value}
  }).json()

  if 'next_page_after_value' not in data['pagination'].keys():
    # make sure to grasp the entries of the last page before breaking
    for entry in data['data']:
      if 'results' not in entry.keys():
        continue
      elif 'chemical_formula_reduced' not in entry['results']['material'].keys():
        continue
      else:
        extract_values(entry)
    break
  page_after_value = data['pagination']['next_page_after_value']

  for entry in data['data']:
    if 'results' not in entry.keys():
      continue
    elif 'chemical_formula_reduced' not in entry['results']['material'].keys():
      continue
    else:
      extract_values(entry)
```

You can verify that the data was fetched correctly by printing some of the values:

```python
print(bandgaps[0])
print(len(bandgaps))
```

## Put Data into a Pandas Dataframe and Save It

Finally, we'll convert the data into a Pandas DataFrame and save it to a CSV file for future use.

```python
df = pd.DataFrame({
    'reduced_formulas': reduced_formulas,
    'iupac_formulas': iupac_formulas,
    'descriptive_formulas': descriptive_formulas,
    'bandgap': bandgaps,
    'voc': vocs,
    'jsc': jscs,
    'ff': ffs,
    'pce': pces,
    'device_stack': device_stack,
    'htl': htl,
    'etl': etl,
    'structural_dimensionality': structural_dimensionality
    })

# create data directory if it doesn't exist
import os
if not os.path.exists('data'):
    os.makedirs('data')
df.to_csv('data/perovskite_bandgap_devices.csv', index=False)
df.head()
df['bandgap'] = pd.to_numeric(df['bandgap'], errors='coerce')
df['bandgap'] = df['bandgap']*6.24150974e18
df
```

We have saved the the data we obtaine from NOMAD API with the name ``perovskite_bandgap_devices.csv`` into the folder ```data`` where your notebook is running. Next we will proceed with cleaning this data.
