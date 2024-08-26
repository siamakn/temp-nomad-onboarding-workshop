## Build and Fit the Model

We will begin by splitting the dataframe into `train_df`, `val_df`, and `test_df` in the ratio of 0.8, 0.1, 0.1.

```python
# Randomize the dataframe and split into train_df, val_df and test_df in the ratio of 0.8, 0.1, 0.1
train_df, val_df, test_df = \
              np.split(df_grouped_formula.sample(frac=1, random_state=42),
                       [int(.8*len(df_grouped_formula)), int(.9*len(df_grouped_formula))])
# train_df.head(), val_df.head(), test_df.head()
```

We then fit the model using the CrabNet implementation.

```python
crabnet_bandgap = CrabNet(mat_prop="bandgap", model_name='perovskite_eg_prediction', elem_prop='mat2vec', learningcurve=True)
crabnet_bandgap.fit(train_df, val_df)
```

### Model Evaluation
After training, we evaluate the model using the validation data.

```python
# Validation data
val_df_zeros = pd.DataFrame(({"formula": val_df['formula'], "target": [0.0]*len(val_df['formula'])}))
val_df_predicted, val_df_predicted_sigma = crabnet_bandgap.predict(val_df_zeros, return_uncertainty=True)

act_pred(val_df['target'], val_df_predicted)
r2 = r2_score(val_df['target'], val_df_predicted)
print(f'R2 score: {r2}')
mse = mean_squared_error(val_df['target'], val_df_predicted)
print(f'MSE: {mse}')
mae = mean_absolute_error(val_df['target'], val_df_predicted)
print(f'MAE: {mae} eV')
```

Next, we test the model using the test data.

```python
# Test data
test_df_zeros = pd.DataFrame(({"formula": test_df['formula'], "target": [0.0]*len(test_df['formula'])}))
test_df_predicted, test_df_predicted_sigma = crabnet_bandgap.predict(test_df_zeros, return_uncertainty=True)
```

### Predict

Now we are going to run some predictions. We will start by loading the model, just in case you want to start directly here in a new session.

#### Load the Model

```python
from crabnet.kingcrab import SubCrab
from crabnet.crabnet_ import CrabNet
import pandas as pd # only if you jump to this cell directly
import numpy as np

# Instantiate SubCrab
sub_crab_model = SubCrab()

# Instantiate CrabNet and set its model to SubCrab
crabnet_model = CrabNet()
crabnet_model.model = sub_crab_model

# Load the pre-trained network
file_path = r'perovskite_eg_prediction.pth'
crabnet_model.load_network(file_path)
```

#### Prediction from Individual Formula

```python
import ipywidgets as widgets
from IPython.display import display

# Write a function to calculate the bandgap of a perovskite given the composition
def predict_bandgap(formula):
    val_df = pd.DataFrame(({"formula": formula, "target": [0.0]*len(formula)}))
    prediction, prediction_sigma = crabnet_model.predict(val_df, return_uncertainty=True)
    return prediction, prediction_sigma

output = widgets.Output()

def predict_and_display(formula):
    with output:
        output.clear_output()
        # Your prediction code here
        prediction, prediction_sigma = predict_bandgap(formula)
        print(f'Predicted bandgap: {np.round(prediction[0], 3)} +/- {np.round(prediction_sigma[0],3)} eV')

# Create input widget
formula_widget = widgets.Text(
    value='',
    placeholder='CsPbBr3, CH3NH3PbI3, CH6I3NPb ...',
    description='Formula:',
    disabled=False
)

# Create button widget
button_widget = widgets.Button(
    description='Predict bandgap',
    disabled=False,
    button_style='',
    tooltip='Click me',
    icon='check'
)

# Define function to handle button click
def on_button_click(b):
    predict_and_display(formula_widget.value)

# Attach button click function to button widget
button_widget.on_click(on_button_click)

# Display the widgets and output
display(widgets.VBox([widgets.HBox([formula_widget, button_widget]), output]))
```
Finally, we can check if the formula exists in the dataset and retrieve its averaged bandgap value.

```python
# Check if the above formula exists in the dataset:
if (df_grouped_formula.eq(formula_widget.value).any().formula):
    Egap = df_grouped_formula.target[df_grouped_formula["formula"] == formula_widget.value].tolist()[0]
    print(f"The averaged literature bandgap for {formula_widget.value} is {Egap:.3f} eV")
else:
    print(f"The formula {formula_widget.value} is not contained in the dataset")
```
