# **Creating Entries for the Instrument Using the *Instrument ELN* Schema**

<div style="text-align: center;">
    <img src="../images/built-in_schema/instrument/1_line.png" alt="Screenshot of the NOMAD user interface showing the instrument ELN schema" width="400">
</div>

In this section, you will learn how to create NOMAD entries for entities that are instruments used to prepare and characterize your samples. You will use NOMAD's built-in schema, called *Instrument ELN*, and explore the various fields you can populate and the information you can add to NOMAD. 

Based on the example described earlier, we will need to create entries for the following instruments:

1. UV Ozone cleaner
2. Ultrasonic bath
3. Scale
4. Optical spectrometer
5. Conductivity board
6. Spin coater

> For general steps on how to create an entry in NOMAD using the built-in ELN schema, see the section [Entries in NOMAD](M3_2_1_creating_entries_built-in_schema.md). When you reach the step 8, select **Instrument ELN** from the drop-down menu, enter a name for your entry, and click **CREATE**. 
>

Let's start by creating an entry for the UV Ozone Purifier. 

<div style="text-align: center;">
    <img src="../images/built-in_schema/instrument/create_line.png" alt="Creating an entry in NOMAD for an instrument" width="400">
</div>


After clicking the **CREATE** button, the following tasks are automatically performed within NOMAD:

   1. NOMAD will create a file for the entry using the *.archive.json* format.
   2. The entry file is stored in the main upload directory. 
   3. NOMAD will open the entry, switch to the *DATA* tab, and open the *data* subsections page. 

The *data* subsections page allows users to input information about the instrument. 


<div style="text-align: center;">
    <img src="../images/built-in_schema/instrument/quantities_line.png" alt="The defualt entry page that opens when an entry is created." width="400">
</div>

In the Instrument ELN built-in schema, several fields are available to accept entry of different quantities: 

* Short name: This is the name of the input file created.
* Datetime: Allows the entry of a date/time stamp. 

* ID: A human readable ID that is unique to the instrument within the laboratory. 

* Description: A free text field that can be used to enter any additional information about the entry. 

> Remember that this is your ELN and you are using a built-in schema that was created to be as general as possible to accommodate a wide range of users. You are free to use the various fields as you see fit. 
