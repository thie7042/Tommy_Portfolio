# Project portfolio
This is a brief catalogue outlining my previous and ongoing research projects. For more information, feel free to reach out to me directly at thie7042@uni.sydney.edu.au, or message me on [Linkedin](https://www.linkedin.com/in/tommy-hielscher-4a40771b6/).


# Machine Learning Digital Twin for Structural Health Monitoring

![](/Images/Video_Demo.gif)


## Project brief
The novel digital twin solution that has been designed and prototyped within this research project aims to demonstrate a holistic, end-to-end fibre optic structural health monitoring strategy that integrates embedded Fibre Bragg Grating sensors, open-source software and fundamental machine learning modelling techniques. Through a collaborative partnership between Laing O’Rourke and The University of Sydney, a series of 64 fibre optic sensors and 8 temperature sensors have been embedded internally within a footbridge located in the Engineering and Technology Precinct (ETP) to continuously measure and collect structural data. These datasets have been leveraged to train a series of machine learning models and develop an integrated digital twin prototype as a collective monitoring solution.

![](/Images/ETP_Bridge.PNG)

<div align="center"> The ETP footbridge, Sydney University
</div>

## Problem statement 
Public and private authorities that manage large infrastructure projects have a responsibility and vested interest in maintaining the longevity of their assets. The structural health monitoring (SHM) methodologies which are applied to these projects conventionally prioritise minimal service disruption, efficient resource allocation and a reduction in the degree of operational risk. The value provided by effective structural health monitoring systems cannot be overstated. In the United States, there are 625,000 bridges listed by the Department of Transportation, 30 percent of which have been officially classified as structurally deficient or functionally obsolete. Furthermore, a 2001 BRIME report concluded that across three different European countries (France, Germany and the UK), deficiencies within highway bridges were present at rates of 39%, 30% and 37% respectively. 

![](/Images/Global_SHM_Stats.PNG)

Traditional techniques of non-destructive evaluation (NDE) for the monitoring of these assets have also been severely limited to routine visual examinations which are unable to provide continuous information into the long-term behaviour of these structures. A technical report published by the U.S Federal Highway administration concluded that 58% of sample average condition ratings for tested structural elements were assigned incorrectly.  These inaccurate evaluation techniques result in economically impractical maintenance schedules and uninformed resource allocation for asset management at an industry scale. The accumulative effects of stagnant industry practices and mass structural deterioration pose a significant risk to the built environment, with the potential to produce a marked decline in serviceability over time.

## Data collection
During the construction of the footbridge, six FBG strain arrays containing 16 sensors at 1.0 m spacing were installed with a spatial resolution of 6.2 mm and a strain resolution of 2 µε. These arrays were fixed to the longitudinal rebar at the bottom and top portions of the concrete slab. Additional arrays were attached along the top surface of the post-tensioning duct as an intermediary reference to evaluate the accuracy of the recorded data. Temperature sensor arrays containing 4 sensors at 5.0 m spacing were also embedded within the footbridge along the top and bottom longitudinal rebar to account for the effects of thermal variation. The installed sensors were linked to a secure interrogator system located on site, with transmitted signals periodically set at 10 second increments to simplify the data architecture and workflow used in this prototype. This signal rate was modified to 1 second increments during the loading experiment to increase the resolution of the structural analysis, before being returned to a 10 second acquisition rate for sustainable long-term data collection & monitoring. 

![](/Images/Sensor_Installation.png)

<div align="center"> Sensor installation at ETP during construction
</div>
## Tested Models
Within the scope of this research project, four machine learning models were analysed: linear regression, ridge regression, lasso regression and an artificial neural network (ANN). These techniques provided a broad spectrum of complexity and hyperparameter diversity, allowing for the identification of a suitable machine learning model that best describes the temperature-strain relationship. For the selection of suitable hyperparameters, 10-fold CV & exhaustive grid-search were used. Hyperparameters which yielded the smallest model error were retained, allowing for the performance of optimised machine learning models to be directly compared against one another.

![](/Images/Hypertune.png)

## Neural Network
Across all of the tested statistical metrics (Gaussian distribution of errors, mean absolute error (MAE), mean squared error (MSE), root mean squared error (RMSE) and the coefficient of determination), the artificial neural network generated the most robust and consistent baseline strain datasets, allowing the digital twin to accurately visualise the footbridges structural response to loading. This analysis includes the derived strain, bending moment and deflection induced within the footbridge when subject to mechanical loading events. The implementation of an artificial neural network has been modelled to forecast baseline strain behaviour as influenced by temperature variance, captured from embedded strain and temperature sensors.

![](/Images/ANN.png)

<div align="center"> ANN strain prediction
</div>

![](/Images/Norm.png)

<div align="center"> Gaussian error distribution
</div>

![](/Images/Stats.png)
<div align="center"> Statistical model comparison
</div>

## Digital Twin UI
In order to mobilise the adoption of FOS sensor technology within the structural health monitoring industry, this framework was designed as an intuitive, user friendly and insightful tool that can be integrated within the workflow of site engineers, asset inspectors and project managers. The Unity Digital twin prototype was programmed with the objective of communicating significant quantities of Big data to provide actionable insights into the structural response of an asset under load, including the induced strain, bending moment and deflection. 

![](/Images/Unity_UI.png)


# Bayesian Optimization with Gaussian Process 

## Context: Locating the maxima

![](/Images/Target_Function.png)


## Context: Building the covariance matrix

![](/Images/Covariance.png)

## Context: Sampling the Prior

![](/Images/Prior_sampling.png)

## Context: Creating the surrogate model

![](/Images/Proxy_model.png)

## Context: Optimizing the acquisition function

![](/Images/Steps.png)

* Current research: Applying Bayesian Optimization with GP to create a proxy model of computationally expensive Finite Element simulations.
* See "Master" branch for development works. This project is currently in progress, with updates to come in the following months.

