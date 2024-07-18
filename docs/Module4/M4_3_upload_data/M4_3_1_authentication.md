# Authentication and Checking Uploads

## Authentication

Most of the API operations with NOMAD do not require any authorization and can be freely used without a user or credentials. However, to upload, edit, or view your own data or those shared with you, the API needs to authenticate you.

The NOMAD API uses OAuth and tokens to authenticate users. This guide will walk you through the process of obtaining access tokens, using the NOMAD Python package for authentication, and managing app tokens.

??? note "What is OAuth?"

    OAuth is an open standard for access delegation commonly used as a way to grant websites or applications limited access to user information without exposing passwords. It allows third-party services to exchange information securely and efficiently.

??? note "What are Tokens?"

    Tokens are pieces of data that are used to authorize access to an API. In the NOMAD API, tokens are used to authenticate users. There are two main types of tokens:
        1. **Access Tokens**: Short-lived tokens used for API requests.
        2. **App Tokens**: Tokens with a user-defined expiration time, used for longer sessions.

Users might need to authenticate themselves using their username and password in the following use cases:

    - When using the API dashboard
    - When interacting with NOMAD API using python.
    - When working with the NOMAD python package.

1. To use authentication in the [API dashboard](https://nomad-lab.eu/prod/v1/api/v1/extensions/docs), simply use the "Authorize" button
![Authenticate in the API Dashboard](../images/API_dashboard_auth.gif)

2. When interacting with NOMAD using python you need access tokens. You can obtain access tokens by sending a GET request to the NOMAD authentication endpoint (/auth/token', see the [API dashboard](https://nomad-lab.eu/prod/v1/api/v1/extensions/docs)). In the following example, we first obtain our access token from the `/auth/token` endpoint, and use it later as a `header` parameter when sending other requests. Simply replace 'myname' and 'mypassword' with your actual username and password and run it. 

```python
import requests
import json

response = requests.get(
    'https://nomad-lab.eu/prod/v1/api/v1/auth/token', 
    params=dict(username='myname', password='mypassword')
)

token = response.json()['access_token']
```

??? tip "App tokens"
    If the short-term expiration of the default access token (obtained from the `/auth/token` endpoint) does not suit your needs, you can request an app token with a user-defined expiration from the `/auth/app_token` endpoint:

    ```python
    response = requests.get(
    'https://nomad-lab.eu/prod/v1/api/v1/auth/app_token?expires_in=86400',
    headers={'Authorization': f'Bearer {token}'})
    app_token = response.json()['access_token']
    ```

3. If you have the [NOMAD Python package](https://nomad-lab.eu/prod/v1/docs/howto/programmatic/pythonlib.html) installed, you can use its `Auth` implementation to directly authenticate yourself in the requests you send. Here is an example on how the username and password is given, when using the `Auth` e.g., to to see the user uploads:


```python
import requests
from nomad.client import Auth

response = requests.get(
    'https://nomad-lab.eu/prod/v1/api/v1/uploads',
    auth=Auth(user='myname or email', password='mypassword')
)
uploads = response.json()['data']


```

## Checking Uploads 

Following example shows how you can check your uploads in NOMAD.

1.  send a GET request to the `/auth/token` endpoint and save your access token (repeated step).
2. send a GET request to the `/uploads` endpoint contains your 'uploads' information. Let's print them!

```python
import requests
import json

response = requests.get(
    'https://nomad-lab.eu/prod/v1/api/v1/auth/token', params=dict(username='my_username', password='my_password'))

token = response.json()['access_token']

response = requests.get(
    'https://nomad-lab.eu/prod/v1/api/v1/uploads',
    headers={'Authorization': f'Bearer {token}'}
)
uploads = response.json()['data']
print(json.dumps(uploads, indent = 4))


```

The output of the above snippet should look like the following. It is a python list with several elements (in this example only 1). Each element is a JSON (or python dict) containing information about each of your uploads.

```JSON
[
    {
        "process_running": false,
        "current_process": "process_upload",
        "process_status": "SUCCESS",
        "last_status_message": "Process process_upload completed successfully",
        "errors": [],
        "warnings": [],
        "complete_time": "2024-07-16T13:57:53.459000",
        "upload_id": "VWGLXmy4S2-cdeteN2Xxaw",
        "upload_name": "FAIRmat_logo.png",
        "upload_create_time": "2024-07-16T13:57:53.308000",
        "main_author": "ebb26223-0cec-4d81-98f5-3b25db945b54",
        "coauthors": [],
        "coauthor_groups": [],
        "reviewers": [],
        "reviewer_groups": [],
        "writers": [
            "ebb26223-0cec-4d81-98f5-3b25db945b54"
        ],
        "writer_groups": [],
        "viewers": [
            "ebb26223-0cec-4d81-98f5-3b25db945b54"
        ],
        "viewer_groups": [],
        "published": false,
        "published_to": [],
        "with_embargo": false,
        "embargo_length": 0,
        "license": "CC BY 4.0",
        "entries": 0,
        "upload_files_server_path": "/nomad/prod/fs/staging/V/VWGLXmy4S2-cdeteN2Xxaw"
    }
]

```

Next we will explore how we can use other API endpoints to create datasets and upload files.