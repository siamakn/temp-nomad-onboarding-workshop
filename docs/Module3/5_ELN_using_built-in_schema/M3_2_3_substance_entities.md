# Create Entries for your Substance Using the *Substance ELN* Schema

![Screenshot from the NOMAD UI which shows the Substance ELN schema](../images/built-in_schema/substance/1.png)


In this section you will learn how to create NOMAD entries for entities that will be used as substances in your experiments. You will use NOMAD's built-in schema, called the Substance ELN, and explore the various fields you can populate and the information you can add to NOMAD. 

Based on the example described earlier, we will need to create entries for the following substances:
1. P3HT powder
2. Chloroform
3. Glass substrate
4. Pre-patterned ITO substrates

![Alt text](../images/lab_images/substances.png)

> For general steps on how to create an entry in NOMAD using the built-in ELN schema, see the section [Entries in NOMAD](M3_2_1_creating_entries_built-in_schema.md). When you reach the step 8, select *Substance ELN* from the drop down menu, enter a name for your record, and click Create. 

![Creating an entry in NOMAD for a substance entity and naming it P3HT_powder](../images/built-in_schema/substance/P3H_powder.png)

After clicking the **Create** button, NOMAD will automatically perform the following tasks:

1. NOMAD creates a file for the entry, using the format *.archive.json*.
2. The entry file is stored in the main upload directory. 
3. NOMAD will open the entry, switch to the *data* tab, and open the *data* sub-sections page. 

The *data* sub-sections page allows user to fill in the information about the substance. 

![The defualt entry page that opens once an entry is created. ](../images/built-in_schema/substance/entry_page.png)

The *substance ELN* built-in schema provides several fields that allow input of different quantities:

* Substance name: This is the name of the input file created.
* Datetime: Allows entry for a date/time stamp. 

* Substance ID: A human-readable ID that is unique for the substance within the lab. 
Can be manually entered.

* Detailed Substance Description: A free text field that can be used to enter any additional information about the entry. 

> Remember that this is your ELN and you are using a built-in schema that was created to be as generic as possible to accommodate as many users as possible. You can use the different fields however you like. For example, the Datetime field can be used as a timestamp for opening the polymer container, purchase date, or entry creation date. 

The substance ELN allows you to include additional information for your entity by using sub-sections. 

These can be found at the bottom of the Entry/Data/Data page and include:

* Elemental composition

* Pure substance

* Substance identifier


![Alt text](../images/built-in_schema/substance/substance_sub_sections.png)

### Elemental Composition Sub-section:
Here you can create quantities to define the chemical composition of your substance. You can add the chemical element, its atomic fraction, and its mass fraction. 
Add as many elements as needed to represent your substance. This section is useful for chemical substances.

### Pure Substance Sub-section:
Here you can define your substance as a pure material purchased from an external vendor. This sub-section allows data entry based on three different definition types. 
* PubChem
* CAS
* General

Regardless of the selected definition type, all pure substance subsections contain the following fields: 
1. Substance name
2. IUPAC name
3. Molecular formula
4. Molecular unit
5. Inchi
6. Inchi Key
7. Smile button
8. Canonical Smile
9. CAS Num
