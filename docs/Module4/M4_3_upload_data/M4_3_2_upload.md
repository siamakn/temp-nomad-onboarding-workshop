
# Creating Datasets and Uploading Files

## Creating Datasets

Following example shows how you can create a dataset using NOMAD's API. 
1. Send a GET request to the `/auth/token` endpoint to obtain your access token (replace 'my_username' and 'my_password' with your actual username and password). This step is one to one repeated from the [last page](M4_3_1_authentication.md).

```python
import requests
import json

response = requests.get(
    'https://nomad-lab.eu/prod/v1/api/v1/auth/token', params=dict(username='my_username', password='my_password'))

token = response.json()['access_token']
```
2. Once you have your `access_token`, send a POST request to the `/datasets/` endpoint, include your token in the header. Also include the dataset name (replace 'replace\_the\_dataset\_name\_here' with a desired name.)

```python
base_url ='https://nomad-lab.eu/prod/v1/api/v1'
endpoint = '/datasets/'
my_dataset ='replace_the_dataset_name_here'
response = requests.post( base_url + endpoint, headers={'Authorization': f'Bearer {token}', 'Accept': 'application/json'},
            json={"dataset_name": my_dataset}
            )
```

3. The dataset is now created. Let's print the response we received which contains information about the dataset we just created in a readable manner.

```python
print(json.dumps(response.json(), indent = 4))
```

The print should look something like the following:

```json
{
    "dataset_id": "3uMiCF_4TEqhaoA_I3X1Yw",
    "data": {
        "dataset_id": "3uMiCF_4TEqhaoA_I3X1Yw",
        "dataset_name": "my_dataset",
        "user_id": "ebb26223-0cec-4d81-98f5-3b25db945b54",
        "dataset_create_time": "2024-07-16T15:16:30.783936+00:00",
        "dataset_modified_time": "2024-07-16T15:16:30.783936+00:00",
        "dataset_type": "owned"
    }
}
```

## Uploading Files

Following example shows how you can upload a file (here the FAIRmat_logo.png) using NOMAD's API.

1. Get your access token from the `/auth/token` endpoint and save it in `token` (If you did already, you don't have to repeat it!).
2. Once you have your `token`, you need to send a POST request to the `/uploads` endpoint and provide a file name. To simplyfiy the process, place the file you plan to upload in the directory that you are running the code. Here, opening the file in **binary read mode** ('rb') is essential when you need to upload or process binary files such as images, zip files, or any other non-text files.
 
```python
base_url ='https://nomad-lab.eu/prod/v1/api/v1'
endpoint = '/uploads'
file_name = 'FAIRmat_logo.png'

with open(file_name, 'rb') as f:
    response = requests.post(
    base_url + endpoint,
    headers={'Authorization': f'Bearer {token}', 'Accept': 'application/json'},
    files={'file': (file_name, f)}
    )
```
You can now check the response, e.g., print it to see if the file has been uploaded successfully:

```python
print(json.dumps(response.json(), indent=4))
```

Congratulations! You have learned the principles of working with the NOMAD API and can now leverage your programming skills to explore the NOMAD API in more details. [NOMAD Documentation](https://nomad-lab.eu/prod/v1/docs/howto/programmatic/publish_python.html){:target="_blank"} also provides further information and examples.