## An example NOMAD API call 

Let's consider the following example. Imagine we would like to send a POST request to NOMAD's API and make a *search query* for entries that contain both Ti and O in their chemical formula. The NOMAD database most probably contains a large number of entries that satisfy our search query. To narrow it down, we restrict it to 1 entry and only ask for the entry_id of that entry. You can simply run the following code in your terminal:

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
- You send the request to `"http://nomad-lab.eu/prod/v1/api/v1/entries/query"`. The API endpoint is `"/entries/query"`.
-  The HTTP method used is `POST`, implying that the request is sending (or posting) data to create or update resources (in this case, we are *posting* data to initiate a search query, which did not exist previously, i.e., we are creating this search query). The `-X` flag in curl specifies the request method to use when communicating with the HTTP server.
-  The headers are flagged with `-H`. The header `Content-Type: application/json`  tells that the type of the content (request body) that we are sending is in JSON format. The `Accept: application/json` tells we would like to receive the response as JSON format as well. If an authentication were required, it would be included here as well.
-  The body (data we are sending) is flagged with `-d`. The JSON object within the single quotes is ahe actual JSON data being sent with the request, which defines the search parameters and what information to include in the response:
  
```bash
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
It defines the search criteria (materials containing the elements "Ti" and "O"), how many results to return (in our case, 1), and what details to include in the response (entry_id).

The response you receive from the server will look *similar* to the following:

```bash
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
    "total": 41531,
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

If you look at the response  closely, you will notice that the response contains information that is *partly* repeating our request (not neccessarily word-for-word, but in a normalized way), *partly* default values for optional parameters that we even did not include in our request, and finally the actual *data* that we requested.

Let’s consider the following simplified layout of the server response, which includes placeholders to represent details that we discuss later

```bash
{
  "owner": "public",
  "query": {...},
  "pagination": {...},
  "required": {...},
  "data": [{"entry_id": "---5IlI80yY5VWEpBMT_H-TBHOiH"}]
}

```
 In this simplified response:

*   **Owner**: Indicates which data are being queried. `public` meaning anyone can access the data.
*   **Query**: This section reiterates the search parameters we sent, but in a normalized structure.
*   **Pagination**: Manages how the data is returned or displayed.  
*   **Required**: Elements or parameters that we specifically requested to be included or excluded in the response.
*   **Data**: The actual information we received.

Now, let's break it down and explore more:

**`owner`**: The `owner` parameter in the NOMAD API allows you to filter entries based on their visibility and ownership. You can specify your search to include various levels of access such as `admin`, `all`, `public`, `shared`, `staging`, `user`, and `visible`. 
Each option tailors the search to different visibility levels, from entries accessible by all users to those restricted to private use. For detailed explanations of each option, refer to the [NOMAD Documentation](https://nomad-lab.eu/prod/v1/docs/howto/programmatic/api.html).

**`query`**: the reformated version of our initial query (see the "name" and "value" lables):

```bash
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
Please note, it is just a simple query. However, more complex queries can be written using logical operators such as **and**, **or** and, **not**. Also shortcuts can be alternatively used to change the logical combination of values in a list, e.g., a suffix to the quantity `any:` (the default), `none:`. Furthermore, comparison operators such as `lt` (less than), or `gt` (greater than)
 can be used to add more filter in the query, both in the form of shortcuts (`lt:`, and `gt:`) and given as an extra filter parameter. The [NOMAD Documentation](https://nomad-lab.eu/prod/v1/docs/howto/programmatic/api.html) provides more details and examples on this topic.


* **`pagination`**: The `pagination` section in the API response organizes how results are delivered:


    - `page_size`: Number of results per page, that we set to 1 in our query.
    - `order_by`: Indicates the criteria used to order the entries. Here the matching 41531 eintries were sorted by `entry_id` (the default in this case) and the first one (`"page_size": 1`) is returend in the response.
    - `order`:  The sorting direction to sort the 41531 matching entries. can be ascending `asc`)  or descending `des`. The default is `asc`.
    - `total`: Total number of entries matching the query, here 41531.
    - `next_page_after_value`: Provides a cursor for pagination. This value is used to fetch the next set of results in subsequent queries. It helps in managing large datasets by allowing the user to continue retrieving data right where the previous query left off. The [NOMAD Documentation](https://nomad-lab.eu/prod/v1/docs/howto/programmatic/api.html) provides a an example on how to use the `next_page_after_value` in order to fetch larger datasets. 


```{bash}
"pagination": {
  "page_size": 1,
  "order_by": "entry_id",
  "order": "asc",
  "total": 41531,
  "next_page_after_value": "---5IlI80yY5VWEpBMT_H-TBHOiH"
}
```

The above example was just to showcase different components of a simple API call.
However, our focus in this tutorial will be on using the Python `requests` library. This approach combines simplicity with powerful capabilities, making it ideal for both beginners and experienced users. In particular its built-in JSON decoding capabilities,  simplify working with JSON data.

The same POST request can be written using the Python `requests` library. For this, open a programming environment of your choice (e.g., VSCode, Jupyter notebook, NOMAD NORTH, etc.) and paste the following piece of code and run:


```python
import requests
import json

url = "http://nomad-lab.eu/prod/v1/api/v1/entries/query"

headers = {
    "Content-Type": "application/json",
    "Accept": "application/json"
}

data = {
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

response = requests.post(url, headers=headers, data=json.dumps(data))

formatted_response = json.dumps(response.json(), indent=2)
print(formatted_response)
```
The response you receive looks similar to what you have received when you sent the API call using `curl` from your terminal:

```python
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
    "total": 41531,
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