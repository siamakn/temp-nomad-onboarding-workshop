<!-- ## Creating an Electronic Lab Notebook using Custom schema -->

# Your First NOMAD Custom ELN

In this section, we will take you through writing your first custom ELN schema, which we will use to create a basic ELN to capture an experiment of solution processing of polymer films.

We will create an ELN for documenting polymer thin films samples prepared by spincoating.

We would like our ELN to accept input for the following quantities:
- Sample ID
- Creation time
- Substrate 
- Substrate cleaning procedure
- Solute
- Solvent
- Solution concentration (mg/ml)
- Spin coating speed (in rpm)
- Spin coating acceleration (in rpm/s)
- Film thickness (in nm)
- Comments

## **Let's Build Our Custom Schema**
The first step of writing a schema is to create a new file using any text editor and save it in the  `.archive.yaml` format.
Lets name our file `My_spincoating_ELN.archive.yaml`.

The next step is to start filling in the schema file with the name, description, and sections. 

We will use the keyword `definitions`, and will only define one section in this schema. The sections should inherit the base section `nomad.datamodel.data.EntryData`.
<!-- add a note on why this is needed -->
```yaml
definitions:
  name: My spincoating ELN
  description: This is an electronic lab notebook for documenting polymer thin films samples prepared by spincoating
  sections:
    polymer_thin_films:
      base_sections:
          - nomad.datamodel.data.EntryData
```
Now we define the quantities which will capture the information of our experiment.

```yaml
definitions:
  name: My spincoating ELN
  description: This is an electronic lab notebook for documenting polymer thin films samples prepared by spincoating
  sections:
    polymer_thin_films:
      base_sections:
          - nomad.datamodel.data.EntryData
      quantities:
        Sample ID:
        Creation time:
        Substrate: 
        Substrate cleaning procedure:
        Solute:
        Solvent:
        Solution concentration:
        Spin coating speed:
        Spin coating acceleration:
        Film thickness:
        Comments:
```
At this stage, we have created the skeleton for our custom schema. Lets add a type for each of the quantities in the schema using the keyword `type`, which will define the kind of values that can be used for each quantity.
A comprehensive list of all the values that `type` accepts can be found [here](https://nomad-lab.eu/prod/v1/staging/docs/howto/customization/basics.html#type).
We will also add `units` to the numerical quantities to define their physical meaning. 

In our example, we will use the following types for our data:
- text (str)
- numbers (np.float64)
- date and time (Datetime)
- list of choices (Enum)

```yaml
definitions:
  name: My spincoating ELN
  description: This is an electronic lab notebook for documenting polymer thin films samples prepared by spincoating
  sections:
    polymer_thin_films:
      base_sections:
          - nomad.datamodel.data.EntryData
      quantities:
        Sample ID:
            type: str
        Creation time:
            type: Datetime
        Substrate: 
            type:
                type_kind: Enum
                type_data:
                    - 'glass'
                    - 'ITO'
        Substrate cleaning procedure:
            type: str
        Solute:
            type:
                type_kind: Enum
                type_data:
                    - 'Regioregular P3HT'
                    - 'Regiorandom P3HT'
        Solvent:
            type:
                type_kind: Enum
                type_data:
                    - 'Chloroform'
                    - 'Dichlorobenzene'
        Solution concentration:
            type: np.float64
            unit: mg/ml
        Spin coating speed:
            type: np.float64
            unit: rpm
        Spin coating acceleration:
            type: np.float64
            unit: rpm / second
        Film thickness:
            type: np.float64
            unit: nm
        Comments:
            type: str
```
Let's save the schema and instantiate an entry to see how it will look like in the NOMAD GUI. 

The entry created contains all the quantities that we have created; however, it offers no means for user interactivity, i.e., input for the ELN. 

In order to allow user input in your ELN, we need to instruct NOMAD how to deal with the different quantities using annotations. Annotations in NOMAD are created using the `m_annotations`. 

Annotations are named blocks of key-value pairs.
```yaml
      m_annotations:
        annotation_name:
          key1: value
          key2: value
```
A complete list of annotations available in NOMAD can be found [here](https://nomad-lab.eu/prod/v1/staging/docs/reference/annotations.html).

We will primarily use the ELN annotations in the schema to allow data entry to quantities we have created. 

```yaml
definitions:
  name: My spincoating ELN
  description: This is an electronic lab notebook for documenting polymer thin films samples prepared by spincoating
  sections:
    polymer_thin_films:
      base_sections:
          - nomad.datamodel.data.EntryData
      quantities:
        Sample ID:
            type: str
            m_annotations:
                eln:
                    component: StringEditQuantity
        Creation time:
            type: Datetime
            m_annotations:
                eln:
                    component: DateTimeEditQuantity
        Substrate: 
            type:
                type_kind: Enum
                type_data:
                    - 'glass'
                    - 'ITO'
            m_annotations:
                eln:
                    component: RadioEnumEditQuantity
        Substrate cleaning procedure:
            type: str
            m_annotations:
                eln:
                    component: RichTextEditQuantity
        Solute:
            type:
                type_kind: Enum
                type_data:
                    - 'Regioregular P3HT'
                    - 'Regiorandom P3HT'
            m_annotations:
                eln:
                    component: RadioEnumEditQuantity
        Solvent:
            type:
                type_kind: Enum
                type_data:
                    - 'Chloroform'
                    - 'Dichlorobenzene'
            m_annotations:
                eln:
                    component: RadioEnumEditQuantity
        Solution concentration:
            type: np.float64
            unit: mg/ml
            m_annotations:
                eln:
                    component: NumberEditQuantity
                    defaultDisplayUnit: "mg/ml"
        Spin coating speed:
            type: np.float64
            unit: rpm
            m_annotations:
                eln:
                    component: NumberEditQuantity
                    defaultDisplayUnit: "rpm"
        Spin coating acceleration:
            type: np.float64
            unit: rpm / second
            m_annotations:
                eln:
                    component: NumberEditQuantity
                    defaultDisplayUnit: "rpm/s"
        Film thickness:
            type: np.float64
            unit: nm
            m_annotations:
                eln:
                component: NumberEditQuantity
                defaultDisplayUnit: "nm"
        Comments:
            type: str
            m_annotations:
                eln:
                    component: RichTextEditQuantity

```

Let's save the schema and re-upload the file to NOMAD. Entries associated with this schema will be automatically updated. 
You can see now that the ELN allows for interactivity, and accepts input of user for the various quantities. 

This is now a functional ELN in which you can document the samples and the fabrication conditions. 
Let's create a few entries with your first ELN. 