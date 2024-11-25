## Build and Train the Model

We randomize the dataset and split it into training, validation, and test sets in a ratio of 80%, 10%, and 10%, respectively.

```python
import numpy as np

train_df, val_df, test_df = np.split(
    df_grouped_formula.sample(frac=1, random_state=42), 
    [
        int(0.8 * len(df_grouped_formula)), 
        int(0.9 * len(df_grouped_formula))
    ]
)
```


We then fit the model using the CrabNet implementation.

```python
from crabnet.crabnet_ import CrabNet

crabnet_bandgap = CrabNet(mat_prop="bandgap", model_name='perovskite_bg_prediction', elem_prop='mat2vec', learningcurve=True)
crabnet_bandgap.fit(train_df, val_df)
```

## Evaluate the Model

After training, we evaluate the model using the validation data.

```python
from crabnet.utils.figures import act_pred
from sklearn.metrics import r2_score
from sklearn.metrics import mean_squared_error
from sklearn.metrics import mean_absolute_error

# Train data
train_df_zeros = pd.DataFrame(({"formula": train_df['formula'], "target": [0.0]*len(train_df['formula'])}))
train_df_predicted, train_df_predicted_sigma = crabnet_bandgap.predict(train_df_zeros, return_uncertainty=True)

act_pred(train_df['target'], train_df_predicted)
r2 = r2_score(train_df['target'], train_df_predicted)
print(f'R2 score: {r2}')
mse = mean_squared_error(train_df['target'], train_df_predicted)
print(f'MSE: {mse}')
mae = mean_absolute_error(train_df['target'], train_df_predicted)
print(f'MAE: {mae} eV')
```

for validation data we have:

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

and finally for test data:

```python
# Test data

test_df_zeros = pd.DataFrame(({"formula": test_df['formula'], "target": [0.0]*len(test_df['formula'])}))
test_df_predicted, test_df_predicted_sigma = crabnet_bandgap.predict(test_df_zeros, return_uncertainty=True)

act_pred(test_df['target'], test_df_predicted)

r2 = r2_score(test_df['target'], test_df_predicted)
print(f'R2 score: {r2}')
mse = mean_squared_error(test_df['target'], test_df_predicted)
print(f'MSE: {mse}')
mae = mean_absolute_error(test_df['target'], test_df_predicted)
print(f'MAE: {mae} eV')
```


### Use the Model for Prediction from Individual Formulas

Now we are going to run some predictions. We will start loading the model just in case you want to start direcly here in a new session. 

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
file_path = r'perovskite_bg_prediction.pth'
crabnet_model.load_network(file_path)
```
Then define a function and run it for predicting the bandgap from individual formulas:

```python

# Function to predict the bandgap of a given formula
def predict_bandgap(formula):
    input_df = pd.DataFrame({"formula": [formula], "target": [0.0]})
    prediction, prediction_sigma = crabnet_bandgap.predict(input_df, return_uncertainty=True)
    return prediction, prediction_sigma

# Main script to take user input and display predictions
while True:
    formula = input("Enter a formula (e.g., CsPbBr3, CH3NH3PbI3) or type 'exit' to quit: ")
    if formula.lower() == 'exit':
        print("Exiting prediction tool. Goodbye!")
        break
    try:
        prediction, prediction_sigma = predict_bandgap(formula)
        print(f"Predicted bandgap: {np.round(prediction[0], 3)} +/- {np.round(prediction_sigma[0], 3)} eV")
    except Exception as e:
        print(f"Error during prediction: {e}")
```

??? tip "Bonus: Interactive Bandgap Predictor with Dataset Check"
    This interactive widget allows you to input a chemical formula, predict its bandgap using the trained model, and check if the formula exists in the dataset. If it does, the widget displays the average bandgap value used during training.

    ```python
    import pandas as pd
    import numpy as np
    from ipywidgets import Text, Button, VBox, HBox, Output
    from IPython.display import display

    # Function to predict the bandgap of a given formula
    def predict_bandgap(formula):
        val_df = pd.DataFrame({"formula": [formula], "target": [0.0]})
        prediction, prediction_sigma = crabnet_bandgap.predict(val_df, return_uncertainty=True)
        return prediction, prediction_sigma

    # Function to check if the formula exists in the dataset
    def check_formula_in_dataset(formula):
        if formula in df_grouped_formula['formula'].values:
            avg_bandgap = df_grouped_formula.loc[
                df_grouped_formula['formula'] == formula, 'target'
            ].values[0]
            return avg_bandgap
        else:
            return None

    # Setting up the widget interface
    formula_input = Text(
        value='',
        placeholder='Enter formula (e.g., CsPbBr3)',
        description='Formula:',
    )
    predict_button = Button(description='Predict Bandgap', button_style='success')
    output = Output()

    def on_click(b):
        with output:
            output.clear_output()
            try:
                formula = formula_input.value.strip()
                if not formula:
                    print("Please enter a valid chemical formula.")
                    return

                # Prediction
                prediction, sigma = predict_bandgap(formula)
                print(f"Predicted Bandgap: {np.round(prediction[0], 3)} ± {np.round(sigma[0], 3)} eV")

                # Dataset check
                avg_bandgap = check_formula_in_dataset(formula)
                if avg_bandgap is not None:
                    print(f"The averaged literature bandgap for {formula} is {avg_bandgap:.3f} eV (from dataset).")
                else:
                    print(f"The formula '{formula}' is not contained in the dataset.")
            except Exception as e:
                print(f"Error: {e}")

    predict_button.on_click(on_click)

    display(VBox([HBox([formula_input, predict_button]), output]))
    ```
