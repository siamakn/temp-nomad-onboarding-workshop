<!-- ## uploading experimental measurement data files to your ELN -->

 # Adding Characterization Data Files to Your NOMAD ELN

In this section, we will explore the process of documenting experiments within the NOMAD ELN, focusing on the essential step of uploading characterization results along with sample and processing information.

Within NOMAD, any file type can be added seamlessly through the ELN upload feature. However, to take full advantage of NOMAD's capabilities, it's critical that data files become Entries. These Entries are processed by NOMAD, transforming them into structured data that allows for easy metadata extraction, visualization, and analysis.

In NOMAD, uploaded files are categorized into two main types: **raw files** and **processed data files**. This distinction is critical to understanding how NOMAD handles and interprets your data.

To facilitate this process, NOMAD is continually expanding its support for various data formats. This support ensures that NOMAD users have access to parsers designed to read specific data formats seamlessly.

??? note  "What exactly is a parser?"

    Think of it as a specialized tool in the NOMAD toolkit. Parsers are small programs designed to take a file as input and produce processed data. They play a crucial role in transforming information from various source formats into NOMAD's structured, schema-based format. Each parser is tailored to a specific file format and is adept at parsing data files of that format. In addition, the parsers are able to navigate through multiple files, such as those referenced in the main file, to ensure comprehensive data processing.

In NOMAD, we support two main categories of data: Theory and Computations data and Measurement (spectroscopy) data.

**Theory and Computations Data:**
For a comprehensive list of codes and related file formats supported in NOMAD, please visit this [page](https://nomad-lab.eu/prod/v1/staging/docs/reference/parsers.html).

**Measurement (Spectroscopy) Data:**
- For generic tabular data in '.csv' and '.xlsx' formats, NOMAD offers a flexible tabular parser that adapts to the structure of the data within the file.
- For Optical Absorption Spectroscopy, NOMAD supports '.asc' files from PerkinElmer Lambda instruments.
- For X-ray Diffraction, NOMAD supports the following file formats:
    - '.xrdml' files from Panalytical instruments.

    - '.rasx' files from Rigaku instruments.

    - 'brml' files from Bruker instruments.

In the following sections, we'll explore how to utilize NOMAD's tabular parser effectively to enhance your data documentation and visualization.

## **NOMAD Support for Data Stored in Tabular File Formats**
It is very common to export measurement data into a tabular format such as .csv or .xlsx.

NOMAD offers a versatile tabular parser that can be configured to process tabular data with different representations, such as data arranged in columns or rows.  
- Columns: each column contains an array of cells that we want to parse into one quantity. Example: current and voltage arrays to be plotted as x and y.
- Rows: each row contains a set of cells that we want to parse into a section, i.e. a set of quantities. Example: an inventory tabular data file (for substrates, precursors, or more) where each column represents a property and each row corresponds to one unit stored in the inventory.

More details on the different representations of tabular data can be found [here](https://nomad-lab.eu/prod/v1/staging/docs/howto/customization/tabular.html).

In this workshop, we will work with measurement data from optical absorption spectroscopy and conductivity measurement stored in a the tabular format .csv, with the columns representations which are shown in the figure below. 

![Alt text](../images/Tabular%20parsers/Example%20data.png)

Our objective is to upload these files into our ELN, make NOMAD parse the data within these files, and then visualize the data in plots that can be viewed in NOMAD. 

To achieve this we will write a schema using the .YAML language and the illustrate how it can be used as ELN in NOMAD. 

### **Step 1: Defining and Saving the Schema File**
Let's start by creating a new schema file with the `.archive.yaml` format, and create a section called Optical_absorption.

```yaml
definitions:
  name: This is a parser for optical absorption data in the .csv format
  sections:
    Optical_absorption:
```
### **Step 2: Adding the Needed Base Sections**
The next step is to inherit the base sections to meet our ELN needs. 

- To create entries from this schema we will use  ``` nomad.datamodel.data.EntryData ```
- To use the tabular parser we will use
``` nomad.parsing.tabular.TableData ```
- To enable the plot function we will use
``` nomad.datamodel.metainfo.plot.PlotSection``` 

### **Step 3: Defining the !uantities of Our Schema**
We will define the quantities in our ELN schema. Three quantities are needed:

1. A quantity to allow the upload of the data file, and apply the tabular parser to transform the data into NOMAD structure. Let's call this ```data_file```

2. A quantity to store the values of our x-axis coming from the tabular parser. Let call this ``` wavelength``` 
3. A quantity to store the values of our x-axis coming from the tabular parser. Let call this ```absorption```

At this stage our schema file will look like this:

```yaml
definitions:
  name: This is a parser for optical absorption data in the .csv format
  sections:
    Optical_absorption:
      base_sections:
        - nomad.datamodel.data.EntryData
        - nomad.parsing.tabular.TableData
        - nomad.datamodel.metainfo.plot.PlotSection
      quantities:
        data_file:
          type: str
          descritpion: Upload your .csv data file
        wavelength:
          type: np.float64
          shape: ['*']
        absorbance:
          type: np.float64
          shape: ['*']

```
### **Step 4: Instructing NOMAD on How to Treat the Different Quantities**
For this, we use the ```m_annotations``` function within each of the quantities to perform the intended task. 
**```data_file``` quantity**
We will need three annotations: 
- The first is to instruct NOMAD to allow for droping and selecting files in this quantity.
Here we will use the following: 
```yaml
eln:
    component: FileEditQuantity
```
- The second is to instruct NOMAD to open the system data browser to select files. 
```yaml 
browser:
    adaptor: RawFileAdaptor
```
- The third one instructs NOMAD to apply the tabular parser to extract the data from the uploaded file.

```yaml
tabular_parser:
    parsing_options:
        comment: '#'
        skiprows: [1]
    mapping_options:
        - mapping_mode: column
            file_mode: current_entry
            sections:
            - '#root' 
```
**``` wavelength```  quantity**
This quantitiy will accept the values from the first column of our tabular data file, that will be extracted by the tabular parser. 
For this purpose we will use the following annotation:
```yaml
tabular:
    name: Wavelength
```
Note that the value for the ```name``` key should be exactly written as the header of the first column in the data file. 

**```absorbance```  quantity**
This quantitiy will accept the values from the second column of our tabular data file, that will be extracted by the tabular parser. 
For this purpose we will use the following annotation:
```yaml
tabular:
    name: Absorbance
```
Note that the value for the ```name``` key should be exactly written as the heared of the first column of in the data file. 

Our schema file at this stage will look as follows:
```yaml
definitions:
  name: This is a parser for optical absorption data in the .csv format
  sections:
    Optical_absorption:
      base_sections:
        - nomad.datamodel.data.EntryData
        - nomad.parsing.tabular.TableData
        - nomad.datamodel.metainfo.plot.PlotSection
      quantities:
        data_file:
          type: str
          descritpion:
            Upload your .csv data file
          m_annotations:
            eln:
              component: FileEditQuantity
            browser:
              adaptor: RawFileAdaptor
            tabular_parser:
              parsing_options:
                comment: '#'
                skiprows: [1]
              mapping_options:
                - mapping_mode: column
                  file_mode: current_entry
                  sections:
                    - '#root'    
        wavelength:
          type: np.float64
          shape: ['*']
          m_annotations:
            tabular:
              name: Wavelength
        absorbance:
          type: np.float64
          shape: ['*']
          m_annotations:
            tabular:
              name: Absorbance
```
### **Step 5: Creating a Plot for Your Data**
To visualize the data from the uploaded and parsed file within your ELN, we will use an annotation for the main section of our schema ```Optical_absorption```

We will use the ```plotly_graph_object``` annotation to instruct NOMAD on which quantities to use for the x-axis and the y-axis, as well as providing a title for the plot.
within ``` plotly_graph_object ``` annotation we use the ```data``` key to define the quantites for each axis. Here the name of the varaiables as will be defined by the scheme should be given.
We will also provide a title to appear on the plot using the ```layout``` key.
```yaml
plotly_graph_object:
    - data:
        x: "#wavelength" 
        y: "#absorbance" 
    layout:
        title: Optical Spectrum
```

At this stage the schema file will be written as follows: 
``` yaml 
definitions:
  name: This is a parser for optical absorption data in the .csv format
  sections:
    Optical_absorption:
      base_sections:
        - nomad.datamodel.data.EntryData
        - nomad.parsing.tabular.TableData
        - nomad.datamodel.metainfo.plot.PlotSection
      quantities:
        data_file:
          type: str
          descritpion:
            Upload your .csv data file
          m_annotations:
            eln:
              component: FileEditQuantity
            browser:
              adaptor: RawFileAdaptor
            tabular_parser:
              parsing_options:
                comment: '#'
                skiprows: [1]
              mapping_options:
                - mapping_mode: column
                  file_mode: current_entry
                  sections:
                    - '#root'                        
        wavelength:
          type: np.float64
          shape: ['*']
          m_annotations:
            tabular:
              name: Wavelength
        absorbance:
          type: np.float64
          shape: ['*']
          m_annotations:
            tabular:
              name: Absorbance
      m_annotations:
              plotly_graph_object:
                data:
                    x: "#wavelength" 
                    y: "#absorbance" 
                layout:
                  title: Optical Spectrum
```
### **Step 6: Uploading Our Schema File to NOMAD and Creating an Entry with Our Data**

Now that we have created the ELN schema file for parsing the optical absorption data file, let's put it into the test in the NOMAD GUI. 

<iframe src="https://scribehow.com/shared/Creating_a_NOMAD_schema_to_parse_tabular_data__hM8UugxXR8CY-U9qIL-dUw?skipIntro=true" width="100%" height="640" allowfullscreen frameborder="0"></iframe>