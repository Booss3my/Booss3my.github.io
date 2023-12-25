---
title: "SOH-estimator"
excerpt: "State of health estimation using charging signals and LSTMs <br/><img src='/images/SOH_estimator/inference.png'>"
collection: portfolio
---

# State of health estimation using charging signals and LSTMs
Real-time Li-Ion state of health estimation using LSTMS (Proof Of Concept)


This notebook presents my implementation of a real-time battery health estimation system developed during my internship at Serma Technologies.

In this system, the model utilizes battery signals, specifically the voltage first derivative recorded during the charging process, to predict battery cell capacity. It is referred to as real-time because the capacity variations between charges are minimal, typically less than 0.001% of the total capacity.

The model architecture consists of two LSTM cells followed by a final linear layer. The training process is as follows:
![model architecture](/images/SOH_estimator/LSTM_model.jpeg)
We define a fixed window size and sample windowed versions of the input signal.
These windowed signals are used to train the model.

![Training data](/images/SOH_estimator/dvdt.jpeg)
To evaluate the model's performance, two test cells are utilized.
Test cell 1             |  Test cell 2
:-------------------------:|:-------------------------:
![test cell 1](/images/SOH_estimator/Ref_88_prediciton.jpg) |  ![test cell 2](/images/SOH_estimator/Ref_90_prediciton.jpg)