## Load Data

We will now import `perovskite_bandgap_devices.csv` from the **data** folder as a pandas DataFrame. This DataFrame contains the results of the API query above, which typically takes several minutes to process.

The distribution of the chemical diversity of the dataset can be visualized using the dynamic periodic table of the NOMAD entries explorer. The bottom-right corner of each element shows the number of entries (solar cells) that contain the element in the absorber. It's clear that the dataset is imbalanced, with the majority of the entries being *Pb* based, containing *C*, *N*, and *H* (hybrid perovskites), and mostly halide compounds, with most of the entries having *I* and/or *Br*.

```python
df = pd.read_csv('data/sia_perovskite_bandgap_devices.csv')
# Change the values of bandgap from units of Joule to electronvolt
df['bandgap'] = pd.to_numeric(df['bandgap'], errors='coerce')
df['bandgap'] = df['bandgap']*6.24150974e18
df.describe()
df.head()
```

Let's see how our ``df`` look like:

```python
df.describe()
```

### Group Repeated Formulas

There are many repeated formulas and bandgap values in the DataFrame. We will use the `group_by_formula` function from CrabNet utilities to end up with unique formula-bandgap pairs. To do so, we will average the values for a given formula:

```python
df.dropna(inplace=True)
df
```

Let's rename columns and use the ``gourpby_formula`` function from CrabNet:

```python
# Rename the column 'bandgap' to 'target'
df.rename(columns={'bandgap': 'target'}, inplace=True)
df.rename(columns={'reduced_formulas': 'formula'}, inplace=True)
# Group repeated formulas and take the mean of the target
df_grouped_formula = groupby_formula(df, how='mean')
df_grouped_formula.head()
```

Let's now check the shape of the datafram:

```python
df_grouped_formula.shape
```
#### Element Prevalence 
We will use `pymatviz` ([link to docs](https://pymatviz.janosh.dev/)) for visualizing the element prevalence.

Run the following snippet if the package is not installed in the environment yet, otherwise skip it.

```python
!pip install git+https://github.com/janosh/pymatviz
```
Once installed, we import and use it:

```python
from pymatviz import ptable_heatmap_plotly

ptable_heatmap_plotly(df_grouped_formula['formula'], log=True, colorscale='BuPu', font_colors='black', fmt='.3g', color_bar=dict(orientation="v", title= 'Element prevalence'))
```

As you can see the current data is heavily based on hybrid halide perovskites, so we expect the model to perform better when predicting these materials. Let's continue and build the model in the next section!