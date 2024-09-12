Overview:
=========

NOMAD can be considered as a database for materials-science data.

A database is a structured collection of data designed to capture the relationships between sets of similar data. These specific pieces of data are referred to as data records.

In NOMAD, data records are called **Entries**.

Entries in NOMAD can be searched for, and each entry has its own individual page on the NOMAD GUI.

Every **entry** in NOMAD (data record) includes a set of attributes defining information about the respective record.

In databases, at least one attribute must serve as the unique identifier for the record, and this designated attribute becomes the primary key.

In NOMAD, the primary key for an Entry is the **Entry ID**, and is assigned automatically by NOMAD.

Entries related to the same subject (application, experimental method, computation method, etc.) are organized into groups, each possessing a defined organizational structure. The arrangement of a data group is known as a **schema**, serving as a map that outlines the relationships between each attribute in a data record. Importantly, all records within a data group adhere to the same schema. The precise definition of the schema is crucial for optimizing database searches and constructing FAIR (Findable, Accessible, Interoperable, and Reusable) data.

In this module, we will learn how a user can create entries of structured data in NOMAD.

Upon completion of the module, participants will be able to:

1\. Illustrate various methods for inserting information into NOMAD to create entries.

2\. Identify and utilize built-in schemas within NOMAD.

3\. Develop and implement custom schemas to meet specific data requirements.

4\. Proficiently create and employ a personalized Electronic Laboratory Notebook (ELN) within the NOMAD platform.