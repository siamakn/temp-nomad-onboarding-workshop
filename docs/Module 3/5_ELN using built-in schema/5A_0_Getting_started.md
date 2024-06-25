# Getting started

## **Introduction to NOMAD entries**

NOMAD is a free, and open-source data management platform for materials science, whose goal is to make scientific research data FAIR (findable, accessible, interoperable and reusable).

NOMAD provides tools for data management, sharing, and publishing. The platform lets you structure, explore, and analyze your data and the data of others.

Similar to general use databases, NOMAD manages a structured collection of data and is designed to capture the relationships between sets of similar data. These specific pieces of data are referred to as data records.

In NOMAD data records are called **Entries**, which have individual pages that can be explored using the NOMAD graphical user interface (GUI) or programatically via API.

Every **entry** in NOMAD (datarecord) includes a set of attributes defining information about the respective record.

In databases, at least one attribute must serve as the unique identifier for the record, and this designated attribute becomes the primary key.

In NOMAD, the primary key for an Entry is the **Entry ID**, and is assigned automatically by NOMAD.

Entries related to the same subject (application, experimental method,computation method, etc.) are organized into groups, each possessing a defined organizational structure. The arrangement of a data group is known as a **schema**, serving as a map that outlinesthe relationships between each attribute in a data record. Importantly, allrecords within a data group adhere to the same schema. The precise definitionof the schema is crucial for optimizing database searches and constructing FAIR(Findable, Accessible, Interoperable, and Reusable) data.

In this module, we will learn how a user can create entries of structured data in NOMAD.

Upon completion of the module, participants will be able to:

1\. Illustrate various methods for inserting information into NOMAD to create entries.

2\. Identify and utilize built-in schemas within NOMAD.

3\. Develop and implement custom schemas to meet specific data requirements.

4\. Proficiently create and employ a personalized Electronic LaboratoryNotebook (ELN) within the NOMAD platform.

| [[Previous]](5_04_Overview_share.md) |   Introduction to NOMAD entries| [[Next]](5A_1_ELN_built_in_schemas.md)
|------------|-----------|-------|

