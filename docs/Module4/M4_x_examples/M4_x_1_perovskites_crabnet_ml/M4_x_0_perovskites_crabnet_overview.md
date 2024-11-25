# Overview

In this section, we will work through a real scientific example to predict the bandgap of perovskite materials from their composition. Perovskites are a class of materials that have gained significant attention in recent years, particularly in the field of solar cells, due to their promising optoelectronic properties. Predicting the bandgap from composition allows researchers to efficiently screen and design new materials with desired properties.


## The Scientific Question

The key question we aim to address is:

**How can we predict the bandgap of perovskite materials based on their chemical composition using machine learning (ML) and data on NOMAD?**

## Steps to Address the Question:

To answer this question, we will break down the process into three main steps:

1. **Retrieve Data from NOMAD via API**: 
    - We will begin by querying the NOMAD database to retrieve data on perovskite materials. This data include information about the materials' chemical compositions and their corresponding bandgap values.
    - We will save the data as a CSV file for further processing.

2. **Clean and Prepare Data for ML**:
    - We will clean the data by removing duplicates, handling missing values, and grouping data by unique chemical formulas.
    - We will also explore the distribution of elements in the dataset to understand its diversity and potential biases, i.e., ensure our dataset quality.

3. **Build, Train, and Evaluate an ML Model**:
    - We will use CrabNet, a deep learning model designed for predicting material properties based on chemical composition, to predict the bandgap of perovskite materials. The model will be trained on the cleaned dataset and its performance evaluated using validation and test datasets.
    - Finally, we will use the trained model to predict the bandgap for new materials.

This workflow serves as a real-world example of using NOMAD data and ML for materials science research. By following this module, you’ll learn how to integrate NOMAD's API with ML tools to tackle scientific challenges.

This example can be considered a real scientific case study. The approach and methods we use here are applicable to actual research problems in materials science. By following through this module, you will not only gain practical experience with using NOMAD's API but also gain some idea of how large data which is retrieved from NOMAD can be used for machine learning and understand how these tools can be used to address significant scientific questions in the field.


