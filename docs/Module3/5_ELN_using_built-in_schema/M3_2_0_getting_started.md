# Getting Started

NOMAD is a free, and open-source data management platform for materials science, whose goal is to make scientific research data FAIR (findable, accessible, interoperable and reusable).

NOMAD provides tools for data management, sharing, and publishing. The platform lets you structure, explore, and analyze your data and the data of others.

Similar to general use databases, NOMAD manages a structured collection of data and is designed to capture the relationships between sets of similar data. These specific pieces of data are referred to as data records.

## **Introduction to NOMAD Entries**

In NOMAD, data records are called **Entries**, which have individual pages that can be explored using the NOMAD graphical user interface (GUI) or programmatically via the API.

Every **entry** in NOMAD (data record) includes a set of attributes defining information about the respective record. In databases generally, at least one attribute serves as the unique identifier for the record, known as the primary key. In NOMAD, the primary key for an entry is the **entry_id**, and is assigned automatically by NOMAD.

Entries related to the same subject (application, experimental method, computation method, etc.) are organized into groups, each with a defined organizational structure. The arrangement of a data group is known as a **schema**, serving as a map that outlines the relationships between each attribute in a data record. Importantly, all records within a data group adhere to the same schema. The precise definition of the schema is crucial for optimizing database searches and constructing FAIR(Findable, Accessible, Interoperable, and Reusable) data.

## **Entries in NOMAD ELN**

Using the NOMAD ELN functionality, you will want to capture all the information related to the substances, samples, and instruments that will be used in your experiment. Furthermore, documenting the measurements performed and the analysis of the acquired data will also be needed. 

For each record, an entry in NOMAD is created based on a data schema that defines the structure. A schema serves as a template with input fields for various parameters of each entry. NOMAD offers a wide range of built-in schemas for general use, as well as, the ability to create your own schema and uploading it to NOMAD. 

## **Learning Objectives**

In this module, we will learn how a user can create entries of structured data in NOMAD.

Upon completion of the module, participants will be able to:

1. Illustrate various methods for inserting information into NOMAD to create entries.

2. Identify and utilize built-in schemas within NOMAD.

3. Develop and implement custom schemas to meet specific data requirements.

4. Proficiently create and employ a personalized Electronic LaboratoryNotebook (ELN) within the NOMAD platform.


