---
layout: archive
title: "CV"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
---

{% include base_path %}

[French Resume](/Resumes/Cv_fr.pdf)

Education
======
* M.S. in AI, signal and Image processing, ENSEIRB-MATMECA, 2023
* B.S. in Telecommunications, ENSEIRB-MATMECA, 2020
* Mathematics-Physics, Preparatory classes (MPSI/MP*), 2019

Work experience
======
* 2023: Data Science intern @ Cdiscount, Bordeaux, France 
  * Developed and deployed a Machine Leaning model to identify fraudulent delivery disputes:
    * Developed a Streamlit (Python) web app for concurrent data labeling by multiple users.
    * Performed wrangling, exploration, and analysis on large volumes of data from internal company data and external API
  sources with SQL and Python and developed an ETL pipeline storing data in Snowflake and orchestrated with Airflow.
    * Experimented with different modelling approaches and tried multiple features, used Jupyter notebooks for experimentation and W&B for experiment tracking.

      * Used pseudo-labelling to train a gradient boosted tree model with labels from a logistic regression model trained on a small human-labeled training dataset.

    * Deployed the best model pipeline using Argo workflows.

* 2022: Data Science intern @ SERMA Technologies, Bordeaux, France
  * Deep Learning Applications in Li-Ion Battery Cell Aging Modeling proof of concept projects:
    * Developed a Physics-Informed Neural Network model with PyTorch, incorporating the industry-standard ageing equation and aging test data. 

    * Implemented a real-time Li-ion battery cell State of Health estimation system utilizing an LSTM cell based model.