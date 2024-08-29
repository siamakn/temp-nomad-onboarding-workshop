# NOMAD Structures Your Research Data

Structured data is a key compoenent in the journey towards achieving FAIR data. NOMAD streamlines this process by providing predefinde structure for collected reasearch data as well as converting raw files into structured and FAIR-compliant data. This transformation is done through the use of schemas, parsers, and Electronic Lab Notebooks (ELNs).

??? note "what are structured data?"
    Structured data refers to information that is organized and formatted in a way that makes it easily searchable, understandable, and usable by both humans and machines. It typically adheres to a predefined model or schema, which dictates how the data is arranged—such as in tables, rows, and columns in a database, or within specific fields in a file format like XML or JSON.


<div style="text-align: center;">
    <img src="images/NOMAD_structuring_workflow.png" alt="NOMAD Structuring Workflow" width="400">
</div>


At the core of the structuring process in NOMAD is the schema. Schemas define possible structures for processed data and metadata, organizing this data hierarchically in sections and subsections. They also define the interconnection between different pieces of data as well as their relevant metadata. For example, in a schema, the units of a measured quantity are defined—such as ensuring that a mass measurement cannot be assigned a unit of length. In essence, schemas are based on ontologies, as they define possible relationships between data and metadata organized within them.

To simplify, a schema is a design that defines how the structure and relationship of the data should be. An analogy would be a schema as the blueprint of a toolbox, where the design specifies the places for the tools, once a template based on this schema is created. Some placeholders in template must be filled with information (data), while others are optional. For instance, when uploading data to NOMAD, it is mandatory to specify when and which user is uploading the data. However, certain fields, such as whether the data includes a DOI, are optional. In simpler terms, some fields in the schema are required while others are optional.

<div style="text-align: center;">
    <img src="images/schema_template_toolbox_analogy.png" alt="Schema Template Toolbox Analogy" width="800">
</div>

??? note "Structured data and Metainfo"
    All data in NOMAD follows a schema that defines how the data is hierarchically structured and cross-referenced. This schema is called the NOMAD Metainfo. It defines a general domain-independent super structure, as well as highly detailed, specialized data from specific methods, tools, and programs.

Based on the chosen or newly created schema, NOMAD structures data into sections and subsections, where each section can contain data and additional sections. Without selecting a schema when uploading files onto NOMAD, the system treats the files as a block of binary information, functioning merely as a storage service without the organizational benefits; similar to how a service like Dropbox would work.

Creating a schema enables the development of Electronic Lab Notebooks (ELNs) that exploit this schema to organize data in a FAIR-compliant manner. Returning to the analogy, the schema defines the placeholders in the ELN user interface, guiding users on which fields should be filled with data or metadata and what kind. For example, imagine an experiment measuring both the heating rate and evaporation rate of water in a beaker placed in a heat bath at a fixed temperature of 120°C. When using a predefined schema or preparing a schema for such an experiment, the ELN would require the user to provide temperature units for the temperature field placeholder and mass units for the water mass placeholder. When the ELN is created based on this schema, the user can easily see the placeholders and fill in the information (or have it filled automatically by the instrument), ensuring that the temperature field only accepts temperature units and the mass field only accepts mass units.

The same principle applies when uploading a file onto NOMAD with an available parser. The parser is a computer script that goes through your file and collects the information to fill the placeholders defined by the schema. Therefore, the primary effort lies in preparing a proper schema for your experiment. Once the schema is prepared, the data can be placed in the correct placeholders either manually via an ELN or by using a computer script (parser). The result is consistent: the data will be stored in a FAIR manner.


In summary, the transition from raw files to FAIR data in NOMAD is achieved by careful design and implementation of schemas, which structure and organize data to ensure its findability, accessibility, interoperability, and reusability.
