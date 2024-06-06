# Creating an Electronic Lab Notebook using NOMAD built-in ELN schema

## **Create Measurement activities using the *measurement ELN* schema**


![Screenshot from the NOMAD UI which shows the measurement ELN schema](images/buit-in%20schema/measurement/1.png)

In this section you will learn how to create NOMAD entries for activities that will be used to describe the measurements in your experiments. You will use the NOMAD built-in schema called *Measurement ELN* and explore the various fields you can fill in and the information you can add to NOMAD.

Based on the example described earlier, we will need to create entries for the following processes:
1. Measuring the optical absorption spectra.

2. Measuring the electrical conductivity.

For general steps on how to create records in NOMAD using the built-in ELN schema, please refer to the [Getting started](5A_1_ELN_built_in_schemas.md) page. When you reach step 8, select *Measurement ELN* from the drop down menu, enter a name for your record, and click Create.

![Creating an entry in NOMAD for measuring the optical absorption spectra and naming it optical absorption](images/buit-in%20schema/measurement/create.png)

After clicking the Create button, the following tasks are automatically performed in NOMAD:
1. NOMAD will create a file for the entry using the *.archive.json* format.
2. The entry file is stored in the main upload directory. 
3. NOMAD will open the entry, switch to the *data* tab, and open the *data* sub-sections page. 

The *data* sub-sections page allows user input to fill in the information about the substance. 

![The default entry page that opens when an entry is created.](images/buit-in%20schema/measurement/Entry%20page.png)

The built-in Measurement ELN schema provides several fields that allow you to enter different quantities: 
* Short Name: This is the name of the input file created.
* Starting Time: Allows you to enter a date/time stamp for the start time of your experiment. 

* ID: A human readable ID that is unique to the measurement within the lab.  Can be manually entered.

* Location: A text field that can be used to specify the location of your measuremement activity.

* Description: A free text field that can be used to enter any additional information about the entry. 

> Remember that this is your ELN and you are using a built-in schema that was created to be as general as possible to accommodate as many users as possible. You can use the different fields however you like. For example, the Description field can be used to provide information about the measurement conditions, modificatoins to the setup, or any relevant observations. 

The Measurement ELN allows you to include additional information for your activities by using sub-sections. 

These can be found at the bottom of the Entry/Data/Data page and include

* Steps

* Samples

* Instrument

* Results

![Alt text](images/buit-in%20schema/measurement/subsections.png)

First, we add the relevant information about our measurement as quantities in the main fields, which will define the main quantities for our activity record.

![Alt text](images/buit-in%20schema/measurement/quantities_filled.png)

The next step is to record the steps performed during the measurement process.

The *steps* subsection can be used to create multiple steps as needed. 
To create steps for your measurement clicking on the + sign, and keeping the section type of *activity step* as show in the following figure.
The *activity step* section allows input for name, time, and comments. 

![Alt text](images/buit-in%20schema/measurement/steps.png)

Lets create the following steps:

1. **samples_in_N2boxes**: Place the samples in the nitrogen-filled boxes. (P3HT on glass and bare glass substrate)
2. **calibration**: Run a baseline calibration with 100% transmission.
3. **load_samples**: load the N2 box with bare glass in the reference beam path, and the N2 box with the P3HT on glass in the measurement beam path. 
3. **measure**: Run the measurement in the range of 300 nm to 1200 nm. 

![Alt text](images/buit-in%20schema/measurement/steps_filled.png)

Continue by adding the samples and the insturment used in the measurement in the relevant subsections.

The results subsection allows text input of any observations on the measurement results. 

Note that the added information in the subsections will be used to automatically fill in the Workflow section as tasks, as well as the References section, which can be viewed in the *Overview* page.

![Alt text](images/buit-in%20schema/measurement/workflow.png)

You can modify the workflow section by adding additional information such as inputs, additional tasks, and outputs. 
To do this, click on the Workflow2 section in the side pane. 

### Advanced: adding measurement results data as an output entry in your ELN

NOMAD offers a tabular parser that can transform data stored in .csv or .xls file formats into a structured JSON file format that can be visualized in GUI.

The tabular parser can be customized to your needs and adapted to your data. Click [here](https://nomad-lab.eu/prod/v1/staging/docs/howto/customization/tabular.html) for more information on NOMAD's tabular parser.

For this example we will assume that the tabular parser has been customized to prase our optical absorption data. You can download the tabular parser, and the example optical absorption data file in .csv format from this link. 

To enable your ELN upload to read the obtained optical absorption data file, so that it can be linked to the respective measurements, follow the following steps:

* Upload the tabular parser schema file to your ELN upload. 
    1. Go to yor ELN overview page and click on **drop files here or click to open dialog** button.
    2. In the open dialog, select the file **polymers_optical_absorption.archive.yaml** file.
 
 ![Alt text](images/buit-in%20schema/measurement/Schema_upload.png)

* Create an entry using the custom schema **polymer optical absorption**. 
    1. Click on the **Create from Schema** button. 
    2. Enter the name of the entry, select the custom schema option, then click on the magnifiying glass. 

    3. In the open dialog, select the only this upload option, then select the My absoprtion ELN schema.

    4. Click create.

![Alt text](images/buit-in%20schema/measurement/Schema_upload_2.png)

After clicking the Create button, the following tasks are automatically performed in NOMAD:
1. NOMAD will create a file for the entry using the *.archive.json* format.
2. The entry file is stored in the main upload directory. 
3. NOMAD will open the entry, switch to the *data* tab, and open the *data* sub-sections page. 

The *data* sub-sections page allows user to upload the results file in the formats of .csv or .xlsx 

Upload the results file P3HT.csv from the example folder, then click save. The P3HT.csv file is now parsed into a strucutre format in NOMAD and can be linked into our ELN. 

![Alt text](images/buit-in%20schema/measurement/UV-VIS.png)

Let us add the results of our measurement as as an output in the workflow in the measurement ELN we have created earlier.

In the workflow section, click on the + icon next to the output subsection, and select the Entry *Optical_spectra_P3HT_on_Glass.archive.json* which we have just created from the raw data file, and provide a name for the entry, then click save. 

![Alt text](images/buit-in%20schema/measurement/workflow_output.png)

The changes will be reflected in the Workflow section and the Reference section of the *Overview* page.

![Alt text](images/buit-in%20schema/measurement/workflow_2.png)


**| [[Previous]](5C_1_Materials_processing_activity.md) |   Create Measurement activities using the *measurement ELN* schema | [[Next] ](5D_0_Managing_experiments.md)|**