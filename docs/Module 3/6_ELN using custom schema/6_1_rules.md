<!-- ## Creating an Electronic Lab Notebook using Custom schema -->

# **The six rules of building a custom ELN schema:**

## **1- Schemas can be written in YAML language**

NOMAD schemas can be created using any text editor using the YAML language, and saving the file with our `archive.yaml` format.

YAML, short for "YAML Ain't Markup Language," is a lightweight and human-readable data serialization language. It is a way to represent data in a structured format that's both easy for humans to read and write, and for machines to parse and process. It uses indentation and whitespace to organize data.

NOMAD's archive.yaml files start with the `definitions` keyword and can have a `name` and `description`.


```yaml
definitions:
  name: My NOMAD ELN
  description: This is an electronic lab notebook schema that includes several sections.
```


## **2- Sections must be defined**
The building-blocks of a schema are sections. They are a representation of data and they are the objects that can be instantiated in NOMAD to build your ELN. 
Sections must be defined with a name, set of quantites, and instructions on how they should be dealt with. 

Sections can be defined by using the keyword `sections` and the name of the section with a single indentation.
```yaml
definitions:
  name: My NOMAD ELN
  description: This is an electronic lab notebook schema that includes several sections.

  sections:
    My_first_section:
    My_second_section:
    My_third_section:
```

## **3- Sections can inheret from other sections**
Sections can also borrow the structure of other sections. This is called inherentance. 
This is useful because NOMAD offers several built-in objects called `base-sections`, which can help you to write your schema effeciently.

The built-in base-sections can be inhereted to a user defined section using the `base-section` keyword, and then listing address of the base sections with a single indentation.

```yaml
definitions:
  name: My NOMAD ELN
  description: This is an electronic lab notebook schema that includes several sections.

  sections:
    My_first_section:
        base-sections:
            - nomad.datamodel.data.EntryData
```
## **4- Sections contain quantities and other sections (sub-sections)**
Each section contains a set of quantites that need to be captured by the ELN. The quantities represent the parameters of you measurement or processing conditions.
In additions, sections can also include sub-sections which can be instantiated within the NOMAD dashboard of the relevant section. 
```yaml
definitions:
  name: My NOMAD ELN
  description: This is an electronic lab notebook schema that includes several sections.

  sections:
    My_first_section:
        base-sections:
            - nomad.datamodel.data.EntryData
        quantities:

        sub-sections:
```

## **5- Quantities are defined with properties**

Quantities define possible primitive values. The first line in the quantitiy definition include a user defined name for the quantitiy. The basic properties that go into a quantity definition are `type`, `shape`, and `unit`.

```yaml
definitions:
  name: My NOMAD ELN
  description: This is an electronic lab notebook schema that includes several sections.

  sections:
    My_first_section:
        quantities:
            first_quantity:
                - type: #For example, str or np.float64
                - shape: #For example scalar or list (['*'])
                - unit: #For example, meters, amperes, or seconds
```

## **6- Section and quantities can have annotations**
 Annotations provide additional information that NOMAD can use to alter its behavior around these definitions and how the user can interact with them. Annotations are named blocks of key-value pairs

```yaml
definitions:
  name: My NOMAD ELN
  description: This is an electronic lab notebook schema that includes several sections.

  sections:
    My_first_section:
      m_annotations:
        annotation_name:
          key1: value
          key2: value

        quantities:
            first_quantity:
                type: value
                shape: value
                unit: value
                m_annotations:
                    annotation_name:
                        key1: value
```
## **7- Sections can reference to other sections**



