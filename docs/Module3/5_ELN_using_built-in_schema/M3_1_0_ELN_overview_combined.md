<!-- ## Creating an Electronic Lab Notebook using NOMAD built-in ELN schema -->

<!-- SN: I suggest to combine the whole Overview section with its subsections in a single longer md file. This way reader sees less nested subsections and does not have to go over multiple short pages. They can navigate through subsections by the table of contents at the right side of the deployed page.
I combine it already in a new md file M3_1_0_overview_combined.md, but keep the old files and just comment them out in mkdocs.yaml to decide.
 -->


# Overview

An Electronic Lab Notebook (ELN) is an essential tool for today's scientists, providing a reliable, searchable record of all experimental activities and measurements. Compared to traditional paper-based lab notebooks, ELNs offer significant advantages, including direct access to your research data from any device, seamless integration of measurements and key findings with detailed experimental metadata, and enhanced collaboration capabilities with colleagues and external partners.

## Why Use an ELN?

- **Searchability:** Instantly locate and retrieve samples and experimental details.
- **Organization:** Store all experimental data, from raw measurements to metadata, in one place.
- **Collaboration:** Easily share and manage projects with your team.
- **Security:** Ensure your data is backed up and protected from loss or damage.

For more reasons to implement an ELN today, check out [this external resource](https://www.scinote.net/blog/8-reasons-why-eln-enhance-research-reproducibility/){:target="_blank"} on how ELNs enhance research reproducibility.


## Typical Experimentation Processes

- **Planning:** Plan your experiment by identifying resources and outlining your process.
- **Documenting:** Record each step of your experiment, including materials, procedures, and results.
- **Managing:** Organize your data, notes, and materials for systematic access and review.
- **Sharing:** Collaborate with others by sharing your progress and results within the ELN.


<div style="text-align: center;">
    <img src="../images/overview/1.png" alt="Process of running experiments" width="600">
</div>

## How to Use NOMAD's ELN?

In this module, we'll guide you through the features of the NOMAD ELN to help you manage your research data efficiently. You'll learn how to design your experiments, document your procedures, organize your data, and share your results with colleagues.

# Planning Your Expriments

Planning is the critical first step in effectively conducting your experiments to obtain meaningful results and conclusions. This is the foundation for taking full advantage of NOMAD's ELN functionality and the ELN's built-in schemas.

 This involves several key actions:

1. **Identify Materials and Instruments**: Identify the materials and instruments that will be essential throughout your experiments.

2. **Create a Sample List**: Compile a comprehensive list of samples that will either be used or prepared for your experiments.

3. **Define Processes and Conditions**: Clearly outline the processes, instruments, and conditions required to accurately prepare the samples.

4. **Listing of Measurements**: Develop a detailed list of measurements that will be used to examine the prepared samples.

5. **Define Experimental Workflows**: Establish clear experimental workflows that cover each step from sample preparation to measurements and analysis.

By carefully completing these planning tasks, you will lay a solid foundation for the smooth execution and meaningful results of your scientific endeavors.


<div style="text-align: center;">
    <img src="../images/overview/2.png" alt="." width="600">
</div>

# Documenting Your Experiments

After carefully planning your experiments, the next critical step is to document those plans and their excution by creating a record for each entity and activity involved in your experiment. Using NOMAD as an ELN for documentation ensures a thorough and efficient record of your experimental strategies.

Here's how to document your plans with NOMAD:

1. **Record Materials and Instruments**: Create a record for each substance, tool, and instrument that will be used in your experiment, including detailed descriptions and relevant parameters. 


2. **List Samples and Preparations**: Document the list of samples to be used or prepared, along with their specific characteristics and preparation methods.

3. **Outline Measurement Parameters**: Clearly define the measurements performed to study the samples, specifying the parameters and techniques to be used.

4. **Document Experimental Procedures**: Describe the experimental workflow from sample preparation through measurements and analysis, ensuring that each step is meticulously recorded.

By documenting your experimental plans with NOMAD, you create a comprehensive record that not only helps maintain clarity and organization, but also facilitates reproducibility and collaboration with other researchers.

<div style="text-align: center;">
    <img src="../images/overview/3.png" alt="Aspects of an experiment to be documented" width="600">
</div>

NOMAD offers specifically tailored built-in schemas that can be used to create the records mentioned above: 

| Entity or Activity | NOMAD ELN schema |
|--------------------|------------------|
| Materials | *Substance ELN*| 
| Tools or instruments | *Instrument ELN*|
| Samples | *Generic sample ELN*|
| Sample preparation | *Material processing ELN*|
| Characterization | *Measurement ELN*| 
| Experiment | *Experiment ELN*| 


# Managing Your Experiments

After carefully planning your experiments and thoroughly documenting all entities and activities involved, the next crucial step is to effectively manage them. Efficient experiment management is essential for maintaining organization and ensuring the quality of research outcomes.

In NOMAD, the experiment management process involves integrating multiple (meta)data records into a single experiment, establishing a clear workflow, and creating comprehensive connections to all entries using the built-in schemas. NOMAD also facilitates recording and analyzing data. By using NOMAD's features, you can streamline the experimental process, ensuring accurate documentation, efficient workflow management, and thorough analysis. This leads to robust and reliable research outcomes.

<!-- 
- The word "workflow" in its english meaning has been used in the past 2 sections. Here the NOMAD specific workflow is meant.
- I suggest to use "(meta)data records" instead of "records", so that the reader is seeing less NOMAD specific terms. 
- entries can also be connected through custom schemas, therefore  removed "built-in".
 -->

<div style="text-align: center;">
    <img src="../images/overview/4.png" alt="." width="600">
</div>

This is accomplished by creating references between entries, such as entities or activities. For example, you can link all the measurements performed on a single sample, or reference each prepared sample to its constituents.

# Sharing Your Progress and Outcomes

Finally, it is essential to share your progress and findings with others. This involves keeping your collaborators updated on your latest experiments and enabling them to record their own experiments. By fostering open communication and collaboration, you can benefit from shared insights and collective expertise, accelerating the pace of scientific discovery and innovation.

NOMAD allows you to share your ELNs with your PI, collaborators, and the community. 

<div style="text-align: center;">
    <img src="../images/overview/5.png" alt="." width="600">
</div>