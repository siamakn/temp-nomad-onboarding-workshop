# Getting started with creating materials for the NOMAD Onboarding Workshop Materials

 This guide will help us get started with contributing content using MkDocs, which utilizes the Markdown format.

**NOTE: This guide assumes you are not working on a tracked git repository.**

## Creating Markdown Files

Among many alternatives for creating Markdown files, Visual Studio Code (VSCode) is a popular option that offers real-time Markdown preview. To use VSCode for Markdown:

1. Open VSCode and create a new file.
2. Add the `.md` extension to your filename.
3. To see a live preview, click on the "Open Preview to the Side" icon located at the top right of the editor.

## To create a new documentation page:

**NOTE: This guide assumes you are not working on a tracked git repository.**

1. Create a `.md` file or copy an existing one into a directory inside the `docs` directory of your project.
3. Add the filename with its extention and its path to the navigation by updating the `mkdocs.yml` configuration file under the `nav` section.

Here is a generic example entry in `mkdocs.yml`:

```yaml
nav:
  - Home: index.md
  - Your New Page: path/to/your-new-page.md
```
 
 Make sure your the newly made file is placed in correct Section or SubSection. For instance, after copying a newly made `Section3_mdfile.md` into a directory named `Section3` inside the `docs` directory, the `mkdocs.yml` file should be modified as follows:

```yaml
nav:
  - Home: index.md
  - Section1: Section1/Section1_mdfile.md
  - Section2:
    - Section2/Section2_mdfile.md
    - Section2_SubSection1: Section2/Section2_SubSection1/Section2_SubSection1_mdfile.md
    - Section2_SubSection2: Section2/Section2_SubSection2/Section2_SubSection2_mdfile.md
  - Section3: Section3/Section3_mdfile.md
```



## Referencing Webpages

You can create links to other webpages using the following Markdown syntax:
```
[FAIRmat website](https://www.fairmat-nfdi.eu/fairmat/)
```
which gives:

[FAIRmat website](https://www.fairmat-nfdi.eu/fairmat/)

## Adding Images

To add images to your  `.md`' file:

 Save your image in the docs/assets folder.
 Reference the image in your Markdown file using the syntax:



```str
![A sample text for the image](relative_path_to_your_image/image-filename.png)
```


Be sure to replace `image-filename.png` with the actual file name and correct relative path to your image, and provide suitable alternative text.

###### For writing relative paths in markdown:
* Same directory: `![Image](image.png)`
* Subdirectory: `![Image](subdirectory/image.png)` 
* Parent directory: `![Image](../image.png)` 

###### Best practices for file naming
* Avoid spaces: Use hyphens (-) or underscores (\_) instead.
* Use lowercase: Prevents issues with case sensitivity.

## Formatting Text

Here's how you can format text in Markdown:

- **Bold**: `**Bold Text**`
- *Italic*: `*Italic Text*`
- `Inline Code`: `` `Inline Code` ``
- [FAIRmat website](https://www.fairmat-nfdi.eu/fairmat/): `[FAIRmat website](https://www.fairmat-nfdi.eu/fairmat/)`



## Adding Tables

Create tables using pipes and dashes:

```
| Header One | Header Two | Header Three |
|------------|------------|--------------|
| Row One    | Data       | Data         |
| Row Two    | Data       | Data         |
```
gives

| Header One | Header Two | Header Three |
|------------|------------|--------------|
| Row One    | Data       | Data         |
| Row Two    | Data       | Data         |

## Code Blocks

Include code blocks with syntax highlighting by specifying the language:

    ```python
    def example_function():
        print("Let's be FAIR")

    example_function()
    ```
gives:
 
```python
def example_function():
    print("Let's be FAIR")

example_function()
```

## Further Resources

- For complete MkDocs documentation, visit [MkDocs Official Documentation](https://www.mkdocs.org).
- For more on Markdown syntax, visit [Markdown Guide](https://www.markdownguide.org).

Thank you for contributing to our documentation project!