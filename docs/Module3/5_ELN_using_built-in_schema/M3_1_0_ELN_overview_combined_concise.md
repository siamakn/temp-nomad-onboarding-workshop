<!-- ## Creating an Electronic Lab Notebook using NOMAD built-in ELN schema -->

# Overview

An Electronic Lab Notebook (ELN) is a digital platform for recording, organizing, and sharing experimental activities, data and metadata. It provides scientists with searchable records, accessible from any device, allowing for more efficient data integration, enhanced collaboration, and robust research documentation.


??? info "Benefits of Using an ELN"
    - **Searchability:** Instantly locate and retrieve samples data and experimental details.
    - **Organization:** Store all experimental data, from raw measurements to metadata, in one place.
    - **Collaboration:** Easily share and manage projects with your team.
    - **Security:** Keep your data backed up and protected from loss or damage.

    For more reasons to implement an ELN, check out [this external resource](https://www.scinote.net/blog/8-reasons-why-eln-enhance-research-reproducibility/){:target="_blank"} on how ELNs enhance research reproducibility.

In this module, you will be guided through NOMAD ELN functionality to efficiently manage your research data. You will learn to design experiments, document procedures, organize data, and share results with colleagues.

In a typical experiment, you will work through these main processes:

- **Planning:** Outline your resources and steps.
- **Documenting:** Record materials, procedures, and results.
- **Managing:** Organize data and notes for easy access.
- **Sharing:** Share your progress and results with your team members or collaborators.

<div style="text-align: center;">
    <img src="../images/overview/1.png" alt="Process of running experiments" width="600">
</div>

Next, we will explore each of these processes in more detail.


# Planning Your Experiments

Planning is the starting point to effectively conduct your experiments and obtain meaningful results and insights. This is the foundation for taking full advantage of NOMAD's ELN functionality.

 Here are a few foundational steps to consider:

1. **Identify Materials and Instruments**: List the materials and instruments needed for your experiments.

2. **Create a Sample List**: Prepare a list of samples that will be used or prepared, obviously, as far as you can plan.

3. **Define Processes and Conditions**: Outline the processes, instruments, and conditions required for sample preparation.

4. **Listing of Measurements**: Develop a detailed list of measurements for examining samples.

5. **Define Experimental Procedures**: Establish procedures that cover each experimental step from sample preparation to measurements and analysis.


<div style="text-align: center;">
    <img src="../images/overview/2.png" alt="." width="600">
</div>



# Documenting Your Experiments

After planning, the next step is to document those plans by creating a record for each **entity** and **activity** involved in your experiment. Using NOMAD's ELN for documentation creates a thorough and organized record of your experimental work.

Here's how to document your plans with NOMAD:

1. **Record Materials and Instruments**: Create a record for each substance, tool, and instrument, including detailed descriptions and parameters. 

2. **List Samples and Preparations**: Document the list of samples to be used or prepared, along with their specific characteristics and preparation methods.

3. **Outline Measurement Parameters**: Clearly define the measurements for studying the samples, specifying techniques and parameters to be used.

4. **Document Experimental Procedures**: Describe the steps from sample preparation to measurement and analysis. Make sure that each step is meticulously recorded.


<div style="text-align: center;">
    <img src="../images/overview/3.png" alt="Aspects of an experiment to be documented" width="600">
</div>


NOMAD offers built-in schemas designed to document key aspects of experiments. While these cover essential and general needs, advanced users can create custom schemas for more specific requirements. Here is a list of built-in schemas to start with:

| Entity or Activity     | NOMAD's built-in schema name      |
|------------------------|------------------------|
| Materials              | *Substance ELN*        |
| Tools or instruments   | *Instrument ELN*       |
| Samples                | *Generic sample ELN*   |
| Sample preparation     | *Material processing ELN* |
| Characterization       | *Measurement ELN*      |
| Experiment             | *Experiment ELN*       |



# Managing Your Experiments

After planning and documenting all entities and activities involved in your experiment, the next important step is to effectively manage them.

In NOMAD, managing experiments means integrating various (meta)data records, which are referred to as **Entities** or **Activities** in NOMAD’s data model, into a single **experiment** record. This process sets up a clearly defined workflow and connects all entries using schemas.


<div style="text-align: center;">
    <img src="../images/overview/4.png" alt="." width="600">
</div>

This is accomplished by creating references between entries, such as **Entities** or **Activities**. For example, you can link all the measurements performed on a single sample, or reference each prepared sample to its elemental constituents, etc.

# Sharing Your Progress and Outcomes

Finally, it is essential to share your scientific progress and findings with others. Sharing your research progress and findings with team members or collaborators not only keeps everyone aligned but also allows for real-time input and feedback.

NOMAD allows for sharing ELNs with selected individuals—whether the project's PIs, team members, collaborators, or the entire research community—with just a few clicks.

<div style="text-align: center;">
    <img src="../images/overview/5.png" alt="." width="600">
</div>





## **Learning Objectives**

In this module, we will learn how to create entries of structured data in NOMAD.

Upon completion of the module, participants will be able to:

1. Illustrate various methods for inserting information into NOMAD to create entries.

2. Identify and utilize built-in schemas within NOMAD.

3. Develop and implement custom schemas to meet specific data requirements.

4. Proficiently create and employ a personalized Electronic LaboratoryNotebook (ELN) within the NOMAD platform.
