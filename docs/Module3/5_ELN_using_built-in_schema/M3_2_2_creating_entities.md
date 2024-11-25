# Create Entries for the Entities of Your Experiment

Recording **entities** in NOMAD is done by creating entries for each entity.

Entities are objects that are used throughout your experiments, and can include the following:

* **Substances** or raw materials used to create samples.
* **Samples** to be examined.
* **Instruments** used to create and measure the samples.

For example, consider an experiment where you need to prepare polymer solutions and then deposit them on substrates to create thin film samples. Then, you want to measure the optical absorption spectra and/or the electrical conductivity of your samples.

To do this, you need your solute (polymer powder) and solvent to make the solution at a predefined concentration. Then you will deposit your thin film on a pre-cleaned substrate to create your samples. 
The polymer powder, solvent, and substrate are considered to be the substances used to create your samples, i.e., the solution and the thin film, respectively. 

For example, here are substances that will be used throughout the experiment:

<div style="text-align: center;">
    <img src="../images/lab_images/substances_line.png" alt="Substances" width="800">
</div>

and here are the samples you planned for this experiment: 

<div style="text-align: center;">
    <img src="../images/lab_images/samples_line.png" alt="Samples" width="400">
</div>

In the process of preparing your **samples**, you will use several **instruments**, such as a balance, UV-Ozone cleaner, sonicator, and spin coater. 

Once the samples are ready, you will use another set of **instruments** to measure the optical absorption spectrum and electrical conductivity, i.e., a UV-Vis-NIR spectrometer and an electrical characterization setup, respectively. 

<div style="text-align: center;">
    <img src="../images/lab_images/instruments_line.png" alt="Instruments" width="800">
</div>

NOMAD provides built-in schemas for the three entities mentioned above, with input fields to define them. Creating entries using these built-in schemas allows you to use these entries for other ELN entries and workflows within NOMAD. 

Let's get hands-on and create entries based on built-in schemas for the different **entities** that will be used in this sample experiment. 

1. Substances
2. Samples
3. Instruments

