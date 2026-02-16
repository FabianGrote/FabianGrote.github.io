---
title: 'Blog Post AirPhyNet'
date: 2026-02-16
permalink: /posts/2026/02/blog-post-airphynet/
tags:
  - neural_networks
  - science
  - air_quality
---

AI meets science: How AirPhyNet makes air quality forecasting more accurate and understandable
======

Introduction
------
Imagine if we could combine the precision of physical laws with the incredible speed of Artificial Intelligence. That is exactly what AirPhyNet does. First presented at the ICLR 2024 by Kethmi Hettige, Jiahao Ji, Shili Xiang, Cheng Long, Gao Cong, and Jingyuan Wang, this framework addresses a critical challenge.
In a world where air quality increasingly impacts our health, relying solely on historical data is no longer enough. AirPhyNet goes a step further: it integrates fundamental principles like diffusion and advection directly into a deep neural network. In this post, discover how this 'Physics-Guided Neural Network' is revolutionizing air pollutant forecasting and why it outperforms previous models and approaches.


Why do we need to predict air quality?
------
Predicting air quality is a vital necessity for both public health and urban management. Accurate forecasts act as an early warning system, allowing the authorities to carry out improvement measures in advance. This can be reduction of traffic or even sending out warnings for vulnerable groups like children and the elderly to avoid exposure during high-pollution events.

What is air pollution exactly?
------
In their paper Kethmi et al. define air pollution as refering to the disruption of natural traits of the atmosphere through contamination of the environment by chemical, physical, or biological substance.

What makes air quality prediction so hard?
------
Several challenges exist that make this task of predicting air quality hard.
First of all the air quality dynamics are complex. Air pollutants don't just sit still. Multiple factors influence how many are in the air and how they move. These can be factors such as wind, traffic intensity, buildings, industiral emissions created by a company close by or reactions in the atmosphere.

Furthermore there is the challenge of data sparsity. For example in Stuttgart the city measures air quality only at 9 stations distributed throughout the city.

![Image of air quality measurement station locations in Stuttgart.](/images/karte-luft-st-neu.jpg)

Third it is an both interesting and also demanding challenge to predict sudden changes, that can occur for instance when a bad weather front suddenly appears.

Last it is important for scientists as well as government employees to be able to understand how the prediction was created.
Neural networks have the habit of beeing a black box.  Without knowing why a change is happening, these models can't provide the reliable, interpretable insights needed for critical public health decisions.


From Physics to Data: Previous Approaches to Air Quality Prediction
------
In the literature up to AirPhyNet, forecasting air quality methods have used one of two approaches:

**Physics-Based Models**\
Inspired by atmospheric science, these traditional approaches portray the dynamics of air pollution as a set of complex differential equations (e.g., Vardoulakis et al., 2003; Liu et al., 2005). While they are grounded in the actual laws of nature, they require immense computational power to solve these equations numerically. Therefor they are often employed only on larger spatial scales, which restricts their ability to provide real-time and fine-grained prediction.

**Data-Driven Models**\
Deep learning allowed researches in the past years to utilize historical pollution data to learn complex relationships without needing prior knowledge of physical processes. Various types of neural networks have been explored, including GNNs (Ji et al., 2023), RNNs, and Attention-based models (Wang et al., 2022; Liang et al., 2023). However, these models have also clear limitations.
Most require extensive training data to achieve accurate long-term predictions, making them less effective in sparse data scenarios.\
The absence of physics constraints limits their generalizability to new environments.\
And as mentioned in the introduction their "black-box" nature raises significant challenges regarding interpretability and transparency for researchers and authorities that want to take decisions based on the results.

Bridging the gap: How AirPhyNet solves these limitations by combining the data and physics approach
------
The power of AirPhyNet lies in its three-stage hybrid design, where the combination of the three stages allows it to overcome the limitations of the models so far that where based either on a physics-based or data-driven approach.\
![Combination of data and physic approaches](/images/CombinationDataAndPhysics.png)

**1. block: Capturing time with a RNN-based encoder**\
The process starts by feeding historical air pollution data into an RNN-based encoder. The historical air pollution data is thereby of type "PM 2.5 concentration".\
This RNN-based encoder extracts temporal information and encodes it into an initial state. Therefor it uses the historical data to determine this state. This enables the model to output good results even in 24,48 or 72 hours in the future, as we can see later. 

![Architecture of AirPhyNet](/images/AirPhyNet_Framework.png)

**2. block: Modeling physics with a GNN-based differential equation network**\
This is where the core innovation of this paper happens. Using a Graph Neural Network (GNN), the model solves a differential equations network that represent diffusion and advection. \
Diffusion describes the random motion of particles from an area of high density to an area of low density.\
Advection describes the principle of transport of particles due to a flow field. In the case of air pollution that mostly means wind.\
This allows the model to understand how air pollutants physically spread between locations (represented in the GNN as nodes).\
This is important for overcoming the limitation of data sparsity, that the previous solely data-driven approaches in the literature faced. In geographical regions with not so many sensors and therefor no or not so much historical pollution data, the physics-guided layer can calculate how the air pollution is likely to behave and move. It furthermore allows the network to be more interpretable then models relying solely on data and are therefor often only black boxes to the user.

**3. block:  Generating results with a decoder**\
In the last block, a decoder translates the in the 2. block learned physical dynamics back into concrete values of PM 2.5 air pollution concentration.

Why AirPhyNet is a game changer
------
Through extensive testing on real-world datasets from the cities of Beijing and Shenzhen, Kethmi et al. demonstrated that combining physics with deep learning on historical data offers measurable advantages over existing state-of-the-art models.

AirPhyNet reduces prediction errors (MAE/RMSE) by up to 10% compared to traditional deep learning models. Its accuracy remains remarkably stable even for long-term forecasts of up to 72 hours.

The evaluation by Kethmi et al. further demonstrates that combining historical observations with physical constraints leads to improved performance in regions with sparse monitoring data, compared to old approaches.

This hybrid design also enhances robustness. The evaluations show that AirPhyNet responds more effectively to abrupt fluctuations in air quality than previous methods, maintaining stable and reliable predictions even under rapidly changing air quality conditions.

By integrating physics via the differential equations in the second block, the framework offers a level of interpretability for researchers and authorities, as can be seen below.

![Visualisierung der Ergebnisse](/images/case_2.png)

Conclusion
------
AirPhyNet marks a turning point in air quality prediction. It proves that we no longer have to choose between the reliability of physics and the speed of deep learning. The future of air quality prediction and similar use cases lies in hybridization.