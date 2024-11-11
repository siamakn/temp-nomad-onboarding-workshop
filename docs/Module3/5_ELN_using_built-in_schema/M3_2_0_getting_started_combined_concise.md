# Entries in NOMAD

NOMAD is a free, open-source data management platform for materials science, aimed at making scientific research data FAIR. Similar to general-use databases, NOMAD manages a structured collection of data and is designed to capture relationships between them. In general database terminology, these pieces of data are referred to as data records. In NOMAD, they are called **Entries**. Entries in NOMAD can be visualized in the NOMAD graphical user interface (GUI) as well as accessed programmatically via its API.

In general databases, every data record includes a set of attributes describing it. One attribute, always present, serves as a unique identifier for that data record, which is called the primary key of that data record. In NOMAD, each **Entry** (data record) has an **entry_id** as its primary key, which is automatically assigned by NOMAD.

Entries related to the same topic, such as application, experimental method, computation method, are organized into groups with a *defined structure*. This structured organization in NOMAD is referred to as **schema**. A schema outlines relationships between attributes within each entry, which can be used to make a *template* with input fields for various entry parameters. This schema-based organization is essential for optimizing database searches needed for FAIR data.

NOMAD offers a wide range of **built-in schemas** for general use, while also allowing users to create and upload **custom schemas** for their specific needs. This flexibility allow users to define new data structures for their particular types of research data, while all entries within the same data group follow the same schema, ensuring consistency, interoperability and reusability across records.

## **NOMAD ELN Entries**

Using the NOMAD ELN functionality, you can capture comprehensive information about substances, samples, instruments, and experimental workflows. Each ELN record in NOMAD is created based on a schema that defines the structure and necessary parameters. For instance, the *Measurement ELN* schema is designed for documenting characterization measurements. This schema allows you to record specific measurement details, such as instrument settings, calibration data, and the actual measured physical properties (like absorption or diffraction patterns). 


## **Learning Objectives**

In this module, we will learn how to create entries of structured data in NOMAD.

Upon completion of the module, participants will be able to:

1. Illustrate various methods for inserting information into NOMAD to create entries.

2. Identify and utilize built-in schemas within NOMAD.

3. Develop and implement custom schemas to meet specific data requirements.

4. Proficiently create and employ a personalized Electronic LaboratoryNotebook (ELN) within the NOMAD platform.


