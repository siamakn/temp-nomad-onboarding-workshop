
 When working with large datasets in NOMAD's API, efficient retrieval of data is important. Pagination allows us to manage large responses by splitting them into manageable pages. In this section, we will demonstrate how to use `pagination` to retrieve a specific number of entries.

 Let's recall [[our first basic example]](M4_2_1_example_api_explained.md) where we sent a POST request to NOMAD's API to obtain the `entry_id` of entries containing both Ti and O in their chemical formula. The response looked like this:
 

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

### Retrieving Multiple Entries
Suppose we want to obtain the `entry_id` of the 120 **most recently** uploaded entries while maintaining the same query criteria. In our previous example, the `pagination` had `"page_size": 1`, which retrieved only one entry. NOMAD's API allows setting the `page_size` up to 10000. We can also specify parameters such as `order_by` and `order`.

To achieve this, we can modify the `pagination` in our POST request: set the `page_size` to 120, and change `order_by` and `order` to "upload_create_time" and "desc", respectively.

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
        "page_size": 120,
        "order_by": "upload_create_time",
        "order": "desc"
    },
    "required": {
        "include": ["entry_id"]
    }
}

response = requests.post(url, headers=headers, data=json.dumps(request_data))
response_json = response.json()

for entry in response_json['data']:
    print(entry['entry_id'])

```

In this specific example, we are only querying the `entry_id`, which is a string of a few dozen bytes. Setting `"page_size": 10000` will give a response with a size of a few hundred megabytes. But what if we want to query larger data (e.g., raw files) or inspect a larger number of entries?

### Handling Large Data Sets

If we need to query larger data sets or inspect a larger number of entries (e.g., 12000 entries), it is practical to retrieve data iteratively to avoid crashes. The `next_page_after_value` in the `pagination` of response can be used as a cursor to iteratively paginate through the results. How?

 The `page_after_value`is an attribute that defines the position after which the page begins, and is used to navigate through the total list of results.

When requesting the first page, no value should be provided for `page_after_value`, therefore, we will set it to `None`. Each **response** will contain a value `next_page_after_value` (see the response on top of the page), which can be used to obtain the next page (by setting the `page_after_value` in our next request to this value).


```python
import requests
import json

url = "http://nomad-lab.eu/prod/v1/api/v1/entries/query"

page_after_value = None
entries_retrieved = 0
desired_number_of_entries = 120

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
        "page_size": 1,
        "order_by": "upload_create_time",
        "order": "desc",
        "page_after_value": page_after_value
    },
    "required": {
        "include": ["entry_id"]
    }
}

while entries_retrieved < desired_number_of_entries:
    response = requests.post(url, headers=headers, data=json.dumps(request_data))
    response_json = response.json()
    
    request_data['pagination']['page_after_value'] = response_json['pagination']['next_page_after_value']
    
    for entry in response_json['data']:
        print(entry['entry_id'])
        entries_retrieved += 1
        
        if entries_retrieved >= desired_number_of_entries:
            break

```







