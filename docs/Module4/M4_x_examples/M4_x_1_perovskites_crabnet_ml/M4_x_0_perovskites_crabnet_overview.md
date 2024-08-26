# Overview: Predicting Bandgap of Perovskites Using Machine Learning with CrabNet

In this module, we will work through a real scientific example using machine learning (ML) to predict the bandgap of perovskite materials. Perovskites are a class of materials that have gained significant attention in recent years, particularly in the field of solar cells, due to their promising optoelectronic properties.

## The Scientific Question

The key question we aim to address is:

**How can we predict the bandgap of perovskite materials based on their chemical composition using machine learning?**

Bandgap is a crucial property for materials used in optoelectronic devices, such as solar cells, as it determines the range of light the material can absorb and convert into electricity. Accurately predicting the bandgap from composition allows researchers to efficiently screen and design new materials with desired properties.

## What We Will Do

To answer this question, we will break down the process into three main steps:

1. **Retrieve Data from NOMAD and Save It to a CSV File**: 
    - We will begin by querying the NOMAD database to retrieve data on perovskite materials. This data includes information about the materials' chemical compositions and their corresponding bandgap values.
    - The retrieved data will be saved to a CSV file for further processing.

2. **Clean the Data and Prepare It for Machine Learning**:
    - In this step, we will clean the retrieved data by removing duplicates, handling missing values, and grouping the data based on unique chemical formulas.
    - We will also explore the distribution of elements in the dataset to understand its diversity and potential biases.

3. **Build, Train, and Evaluate a Machine Learning Model**:
    - We will use the CrabNet model to predict the bandgap of the perovskite materials. CrabNet is a deep learning model specifically designed for materials property prediction based on chemical composition.
    - The model will be trained on the cleaned dataset, and we will evaluate its performance using validation and test datasets.
    - Finally, we will use the trained model to predict the bandgap for new materials.


This example can be considered a real scientific case study. The approach and methods we use here are applicable to actual research problems in materials science. By following through this module, you will not only gain practical experience with using NOMAD's API but also gain some idea of how large data which is retrieved from NOMAD can be used for machine learning and understand how these tools can be used to address significant scientific questions in the field.


