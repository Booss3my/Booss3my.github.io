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


Introduction:
I implemented a real-time Li-Ion state of health (SOH) estimation system during my internship at Serma Technologies. The project's focus was on predicting battery cell capacity using signals from the charging process, with particular attention to the voltage first derivative. This choice was based on a comprehensive analysis that considered both the correlation with the target variable and the ease of capturing relevant information.

Method Used:
In designing the model architecture, the decision to emphasize the voltage first derivative was informed by its identified strengths in correlation with the target variable. Additionally, the ease of capturing relevant features from this signal played a crucial role in its selection. The chosen architecture utilizes two Long Short-Term Memory (LSTM) cells followed by a final linear layer. The LSTM cells were preferred due to their ability to effectively capture and remember long-term dependencies in sequential data, aligning with the temporal nature of the charging signals.

The training process involves defining a fixed window size and sampling windowed versions of the input signal, specifically the voltage first derivative. This tailored approach allows the model to learn and leverage the most informative aspects of the signal for accurate SOH estimation. PyTorch was employed for its flexibility in implementing deep learning architectures, and the utilization of Kaggle P100 GPUs expedited the training process.

Languages/Libraries and Frameworks Used:
The project was implemented using Python as the primary programming language. PyTorch, with its LSTM implementation, was chosen as the deep learning framework, offering the necessary tools for sequence modeling. The computational power of Kaggle P100 GPUs was harnessed to optimize the training phase.


### Results
The implemented model demonstrated highly satisfactory performance across multiple key metrics:

#### Inference Latency:

For a chosen window size of 20 minutes (sampled at 1Hz) on a single Kaggle P100 GPU notebook, the latency of the inference pipeline was found to be less than 30ms. This remarkable efficiency ensures that the capacity prediction process doesn't impede the charging-discharging cycle, eliminating any waiting time after a full charge. The real-time nature of the system is crucial for maintaining the continuous operation of the battery without unnecessary delays.

#### Mean Absolute Error (MAE):

On the test cells, the MAE was measured at 1.3%. Importantly, after the 100th cycle, the MAE further improved to 0.39%. It's noteworthy that the model faces challenges in accurately predicting the value 0 due to the sigmoid activation function in the last layer. However, this specific challenge is deemed less critical, as the primary focus is on the model's performance as the battery undergoes aging. The model's ability to deliver accurate predictions during the aging phase is paramount, and the achieved MAE values reflect its robust performance in this context.


Test cell 1             |  Test cell 2
:-------------------------:|:-------------------------:
![test cell 1](/images/SOH_estimator/Ref_88_prediciton.jpg) |  ![test cell 2](/images/SOH_estimator/Ref_90_prediciton.jpg)