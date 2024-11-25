# Compositional Property Prediction of Perovskites with CrabNet

This example demonstrates how to use [CrabNet](https://github.com/sparks-baird/CrabNet){:target="_blank"} to predict the bandgap of perovskites using data from the [Perovskite Database](https://www.nature.com/articles/s41560-021-00941-3){:target="_blank"}, available in NOMAD for training.

*Authored by José A. Márquez et al.* This example is based on the Jupyter notebook *crabnet-perovskite-bandgap-prediction.ipynb* and can be reproduced using the provided code snippets.

## Installing Needed Libraries

We will start by running a couple of pip installers. Skip this part if you have the libraries installed in your environment.

```python
! pip install torch
! pip install crabnet
! pip install pandas
```

## Retrieve Data using NOMAD API

??? info "Skip the API Call Section if You Have the Data"
    If a `.csv` file in the `data` folder already exists, you can **skip the rest of the steps below** and proceed directly to [next page on data cleaning](M4_x_2_perovskites_crabnet_load_and_clean_data.md). However, make sure that you have installed the necessary libraries and imported them in your notebook before proceeding.


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

bandgaps = []
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
                {"sections:all": ["nomad.datamodel.results.SolarCell"]}
            ]
        },
        'required': {
            'results': {
                'material': {
                    'chemical_formula_reduced': '*',
                    'structural_type': '*'},
                'properties': {
                    'optoelectronic': {
                        'band_gap': '*',
                        'solar_cell': {
                            'open_circuit_voltage': '*',
                            'short_circuit_current_density': '*',
                            'fill_factor': '*',
                            'efficiency': '*'}}},
            },
        },
        'pagination': {'page_size': 1000,
                       'page_after_value': page_after_value}
    }).json()

    if 'next_page_after_value' not in data['pagination'].keys():
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

## Save Data

Finally, we'll convert the data into a Pandas DataFrame and save it to a CSV file for future use.

```python
import pandas as pd
import os

# Convert data into a Pandas DataFrame
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

# Save to a CSV file
if not os.path.exists('data'):
    os.makedirs('data')
df.to_csv('data/perovskite_bandgap_devices.csv', index=False)

# Convert 'bandgap' to numeric and apply unit conversion
df['bandgap'] = pd.to_numeric(df['bandgap'], errors='coerce')
df['bandgap'] = df['bandgap'] * 6.24150974e18

# Display the DataFrame
df.head()
```

We have saved the the data we obtaine from NOMAD API with the name **perovskite_bandgap_devices.csv** into the folder **data** where your notebook is running. Next we will proceed with cleaning this data.
