## Your first NOMAD API call

Let's consider the following example. Imagine we would like search NOMAD for materials that contain both Ti and O in their chemical formula. Since NOMAD ,ost likely contains a large number of matching entries, we narrow the search to just one result and request only its `entry_id`. 


## The **Request**

For this you will need to prepare a proper search query, send it to the NOMAD's API using a client. NOMAD servers process your request and prepare a response and sends back to you via the client.

You can run the following command in your terminal to execute this query: 

```bash
curl -X POST "http://nomad-lab.eu/prod/v1/api/v1/entries/query" \
     -H "Content-Type: application/json" \
     -H "Accept: application/json" \
     -d '{
           "query": {
               "results.material.elements": {
                   "all": ["Ti", "O"]
               }
           },
           "pagination": {
               "page_size": 1
           },
           "required": {
               "include": ["entry_id"]
           }
         }'
```
In this example:

- You use `cURL` as your API client in the terminal to send your HTTP request.
- The HTTP method used is `POST`, implying that you are sending (i.e., posting) data to create or update resources (in this case, you are *creating* a search query in NOMAD servers, which did not exist previously, therefore you used `POST`). The `-X` flag in curl specifies the request method (`POST`) to use when communicating with the HTTP server.

- You send the request to the **API endpoint** which is `"http://nomad-lab.eu/prod/v1/api/v1/entries/query"`. Since the initiall part of the URL stays the same in different endpoints, sometimes only the changing part (`"/entries/query"`) is referred to as endpoint.

??? details "What are NOMAD's API endpoints?"
    In general, rach API has documentation explaining its endpoints. A list of API endpoints and their documentation can be found in [NOMAD's API dashboard](https://nomad-lab.eu/prod/v1/api/v1/extensions/docs){:target="_blank"}. The endpoints in NOMAD often imply their functionality. For instance, a `POST` request to the endpoint `/datasets/{dataset_id}/action/doi` implies assigning a DOI to a dataset by providing its `dataset_id`.

-  **Headers** are flagged with `-H`. The header `Content-Type: application/json`  tells that the the data that you are sending (the request body) is in JSON format. The `Accept: application/json` tells you would like to receive the response as JSON format as well. If an authentication were required, it would be included here as well.
-  The **Body** (data we are sending) is flagged with `-d`. The JSON object after the flag `-d` within the single quotes is the actual JSON data being sent with the request, which defines the search parameters and what information to include in the response:
  
```json
{
  "query": {
    "results.material.elements": {
      "all": ["Ti", "O"]
    }
  },
  "pagination": {
    "page_size": 1
  },
  "required": {
    "include": ["entry_id"]
  }
}

```
Let's have a closer look to the data (request body) you included after the `-d` flag. It defines the search criteria (materials containing the elements "Ti" and "O"), how many results to return (in our case, 1), and what details to include in the response (entry_id) in a structured format.

## The **Response**

The **response** you receive from the server will look *similar* to the following:

```json
{
  "owner": "public",
  "query": {
    "name": "results.material.elements",
    "value": {
      "all": [
        "Ti",
        "O"
      ]
    }
  },
  "pagination": {
    "page_size": 1,
    "order_by": "entry_id",
    "order": "asc",
    "total": 41544,
    "next_page_after_value": "---5IlI80yY5VWEpBMT_H-TBHOiH"
  },
  "required": {
    "include": [
      "entry_id"
    ]
  },
  "data": [
    {
      "entry_id": "---5IlI80yY5VWEpBMT_H-TBHOiH"
    }
  ]
}

```

If you look at the response closely, you will notice that the response contains information that is *partly repeating your request* (not necessarily word-for-word, but in a normalized way), and *partly default values for optional parameters that you even did not include in our request*, and finally the *actual data that you requested*.

Let’s consider the following simplified layout of the server response that you received from the `/entries/query` endpoint of the NOMAD API. It includes placeholders ("...") to represent details that we discuss later:

```json
{
  "owner": "public",
  "query": {...},
  "pagination": {...},
  "required": {...},
  "data": [{"entry_id": "---5IlI80yY5VWEpBMT_H-TBHOiH"}]
}

```
 In this simplified response:

*   **`owner`**: Indicates which data are being queried. `public` means publicly available data. You will see more details soon.
*   **`query`**: This section reiterates the search parameters you sent, but in a normalized structure.
*   **`pagination`**: Manages how the data is returned or displayed.
*   **`required`**: Elements or parameters that you specifically requested to be included or excluded in the response data.
*   **`data`**: The actual data you received as response.

Now, let's break it down and explore more:

**`owner`**: The `owner` parameter in the NOMAD API allows you to filter entries based on their visibility and ownership. You can specify your search to include various levels of access such as `admin`, `all`, `public`, `shared`, `staging`, `user`, and `visible`. 
Each option tailors the search to different visibility levels, from entries accessible by all users to those restricted to private use. For detailed explanations of each option, refer to the [NOMAD Documentation](https://nomad-lab.eu/prod/v1/docs/howto/programmatic/api.html){:target="_blank"}.

**`query`**: The reformatted version of our initial query (see the "name" and "value" lables):

```json
"query": {
  "name": "results.material.elements",
  "value": {
    "all": [
      "Ti",
      "O"
    ]
  }
}
```

??? details "Advanced query options in NOMAD"
    The example we are inspecting here is actually a basic query example. NOMAD supports more complex queries that can be written using logical operators such as **and**, **or**, and **not**. Also, you can use shortcuts to modify the logical combination of values in a list, such as `any:` (default) or `none:`. Furthermore, comparison operators like `lt:` (less than) or `gt:` (greater than) can also be used to refine your query further, either as shortcuts or extra filter parameters.  

    For detailed explanations and examples of advanced query options, refer to the [NOMAD Documentation](https://nomad-lab.eu/prod/v1/docs/howto/programmatic/api.html){:target="_blank"}.



* **`pagination`**: The `pagination` section in the API **response** organizes how results are delivered:


    - `page_size`: Number of results per page, that you set to 1 in your query.
    - `order_by`: Indicates the criteria used to order the entries. Here the matching 41544 entries were sorted by `entry_id` (the default in this case) and the first one (`"page_size": 1`) is returned in the response.
    - `order`:  The sorting direction to sort the 41544 matching entries. can be ascending `asc`)  or descending `desc`. The default is `asc`.
    - `total`: Total number of entries matching the query, here 41544.
    - `next_page_after_value`: Provides a cursor for pagination. This value is used to fetch the next set of results in subsequent queries. It helps in managing large datasets by allowing the user to continue retrieving data right where the previous query left off. The [NOMAD Documentation](https://nomad-lab.eu/prod/v1/docs/howto/programmatic/api.html){:target="_blank"} provides a an example on how to use the `next_page_after_value` in order to fetch larger datasets. 


```json
"pagination": {
  "page_size": 1,
  "order_by": "entry_id",
  "order": "asc",
  "total": 41544,
  "next_page_after_value": "---5IlI80yY5VWEpBMT_H-TBHOiH"
}
```
Please note that the `pagination` section in the response also includes default values for parameters not explicitly set in our POST request, such as `order_by`, `order`, and `next_page_after_value`. In our [next example](M4_2_2_leveraging_pagination.md), we will explore how these parameters can be used to enhance control over API calls.

## How do they look in Python?

The above example was just to showcase different components of a basic API call. We used the `curl` client, because it was easier to explain different components of an API request. However, our focus in this tutorial will be on using the Python's `requests` library as the API client. This approach combines simplicity with powerful capabilities, making it ideal for both beginners and experienced users. In particular its built-in JSON decoding capabilities,  simplify working with JSON data.

The same POST request can be written using the Python `requests` library. For this, open a programming environment of your choice (e.g., VSCode, Jupyter Notebook, NORTH, etc.) and paste the following piece of code and run:


```python
import requests
import json

url = "http://nomad-lab.eu/prod/v1/api/v1/entries/query"

headers = {
    "Content-Type": "application/json",
    "Accept": "application/json"
}

request_data = {
    "query": {
        "results.material.elements": {
            "all": ["Ti", "O"]
        }
    },
    "pagination": {
        "page_size": 1
    },
    "required": {
        "include": ["entry_id"]
    }
}

response = requests.post(url, headers=headers, data=json.dumps(request_data))

formatted_response = json.dumps(response.json(), indent=2)
print(formatted_response)
```
The response you receive should look similar to what you have received when you sent the API call using `curl` from your terminal:

```json
{
  "owner": "public",
  "query": {
    "name": "results.material.elements",
    "value": {
      "all": [
        "Ti",
        "O"
      ]
    }
  },
  "pagination": {
    "page_size": 1,
    "order_by": "entry_id",
    "order": "asc",
    "total": 41544,
    "next_page_after_value": "---5IlI80yY5VWEpBMT_H-TBHOiH"
  },
  "required": {
    "include": [
      "entry_id"
    ]
  },
  "data": [
    {
      "entry_id": "---5IlI80yY5VWEpBMT_H-TBHOiH"
    }
  ]
}
```