# Using the API helper on Entry Pages

In this example, we will learn how to query data that are referenced in an expected location with a relatively complex address.

Here is the question: Suppose our task is to access the density of states for an entry that contains both Ti and O and includes calculations for dos and electronic band structure via the API.

## Step 1: Using the GUI to apply filters

We had this previously, for the sake of completeness, the steps to follow are:

1. Open the NOMAD GUI and navigate to the 'Explore' tab.
2. On the left sidebar under 'Filters', select 'Ti' and 'O' from the periodic table under 'Elements / Formula'.
3. Go to 'Properties' -> 'Electronic' and check 'Density of States'.
4. The GUI will now display materials that contain both Ti and O, and have the selected electronic properties, namely dos and electronic band structure. Currently, there are 46 results matching these filters.

## Step 2: Find the relevant endpoing from API helper.

1. Let's choose the first entry that appears in the filtered results. The principle is similar for all the entries, but if you would prefer to look at the same entry of this example, you can access the entry with the `entry_id` "kAarJxUt4bGajfLZFyqEPnxRK59_" (you can use the search bar in the GUI to access it)
2. On the entry page, locate and click the API button (`API`) at the bottom-left of the page.
3. Scroll down to see the POST request.
5. Find the POST request, have look ok the URL: "https://nomad-lab.eu/prod/v1/api/v1//entries/kAarJxUt4bGajfLZFyqEPnxRK59_/archive/query". You can see that there is a key which looks like an `entry_id`. Also, you can distinguish the API endpoint `entries/{entry_id}/archive/query` implying that this endpoint allows you to query the 'archive' data, i.e., (processed) data, given you have its `entry_id`
6. Copy the `entry_id` from the POST request.

## Step 3: Using the API Dashboard

1. Open the [API dashboard](https://nomad-lab.eu/prod/v1/api/v1/extensions/docs) in a new tab.
2. Navigate to the endpoint `entries/{entry_id}/archive/query` and expand it. The description says "Returns a partial archive for the given entry_id based on the required specified in the body." It seems like what we are interested in. It just needs an `entry_id` and `required` part. There is no need for a `pagination`, `owner` etc.
3. Click on 'Try it out'.
4. The `entry_id` can be copied from entry page or the URL of the POST request. In our example it is "kAarJxUt4bGajfLZFyqEPnxRK59_". In order to write the `required` part, we should first locate the desired data.

## Step 4: Locating the desired data

Since we are only interested in the density of states (dos), we need to specify this in the `required` field. Intuitively, we look for the dos data in the `data` section of the response:

1. Go back to the API Helper on the entry page.
2. Scroll down to see the RESPONSE under the POST request.
3. Expand the 'data' section.
4. Expand the 'archive' section.
5. Expand the 'results' section.
6. Expand the 'properties' section.
7. Expand the 'electronic' section.
8. Expand the 'dos_electronic' section.
9. Expand the '0' section.
10. Here you will find "energies", "total", "spin_polarized", "energy_fermi", and "band_gap". If you are looking at a different entry, you might see other sections. However, it does not matter. The key point is that we are able to locate the desired data that we would like to access via API.
11. Note the path to "energies", which is `/run/0/calculation/0/dos_electronic/0/energies`. The data of interest are **not** here, but are actually **referenced** here with their **path**. 

Now let's quickly verify if the dos data are in `/run/0/calculation/0/dos_electronic/0/energies`. 

1. Go back to the `Response` under the POST request in the API Helper of the entry page.
2. Expand the 'data' section.
3. Expand the 'archive' section.
4. Expand the 'run' section.
5. Expand the first element (`0`) of the 'run' section.
6. Expand the 'calculation' section.
7. Expand the first element (`0`) of the 'calculation' section.
8. Expand the 'dos_electronic' section.
9. Expand the first element (`0`) of the 'dos_electronic' section.
10. Expand the 'energies' section to verify that the actual data is present.

## Step 5: Constructing the `required` and executing the query 

Switch to the API dashboard and under the endpoint `entries/{entry_id}/archive/query` click on 'Try it out'. Paste the `entry_id` to its place, if you havn't done it yet.

Remember, the path to the data is `/run/0/calculation/0/dos_electronic/0/energies`. We need to construct the `required` field to reflect this path to be able to retrieve dos data. This is how it is done:

```json
{
  "required": {
    "run[0]": {
      "calculation[0]": {
        "dos_electronic[0]": {
          "energies": "*"
        }
      }
    }
  }
}
```

This structure tells the NOMAD backend to 

* go to the first element of the `run` section (consider `run` as a python list, then its first element will be `"run[0]"`).
  
* From there, go to the first element of the `calculation` section (`"calculation[0]"`). 

* Then go to the first element of the `dos_electronic` section (`"dos_electronic[0]"`).

* Finally, retrieve everything in the `energies` section (`"energies": "*"`).

After clicking on "Execute", the response is back via code 200 and can be downloaded as a JSON file.

Well done! You could retrieve data from data containers (sections) deep in NOMAD data architecture.

??? note "formatting JSON"
    When writing in JSON format (the `required`), indentation is not essential. One could write the same `required` as following:
    ```json
    {"required": {"run[0]": {"calculation[0]": {"dos_electronic[0]": {"energies": "*"}}}}} 
    ```
    Indentation just helps to easily identify the structure and hierarchy of the JSON data. A common practice is to use two or four spaces for each level of indentation you can write it. You could write everything in 1 line, or alternatively get your JSON formatted using one of several available online tools, e.g., [this one](https://jsonformatter.org/). These tools often allow checking the correctness of JSON format, e.g., missing curled brackets etc.


![Example to use the API Dashboard](../../images/TiO_dos_complete.gif)

??? question "How do you retrieve dos data for 10 entries?"
    What would you do if you want to do the same procedure for 10 entries?

??? note "Hint"

    - The API dashboard also shows the CURL request that can be sent to retrieve this data.
    - You already learned how to use API via CURL [here](../M4_2_1_example_api_explained.md) 
    - You have also learned how to extract the `entry_id` of the entries which match your search criteria in a [former example](../M4_2_2_leveraging_pagination.md) 






