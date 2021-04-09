---
#esowc
#deep_learning
---

# Challenge #21 - Machine Learning to improve the CAMS global air quality forecasts

CAMS runs a global climate model (GCM) to predict global air pollution at resolution of 40km x 40km. Due to the scale of the GCM and uncertainties in inputs, there are errors when trying to accurately predict air quality on regional scales. Hence, bias-correction methods are used as a post-processing step to minimize bias.

Simple bias-correcting methods assume that the bias is constant across time. Additionally, due to the spatially sparse air quality observations, it is hard to leverage spatial structure when deploying bias-correction methods. This problem is further complicated when considering a global model.

In order to improve bias-correction, we propose a 2 stage transfer learning approach using a Recurrent U-Net Deep Learning model, which will be able to capture the time-varying behavior of the model and then the bias.

We would conduct the study initially on a specific region (USA) which would serve as a proof of concept, due to the availability of stationary reference-grade data on openAQ (all PM2.5, O3 and NO2). We would be able to leverage past knowledge with previous studies conducted on this region[1]. This model would then be able to be trained on different regions including Europe and China. The lower-quality data would require more rigorous treatment and a deeper study before inclusion.

[Previous work of colleague on Github by Tailong He at University of Toronto](https://github.com/tailonghe/DLO3)

Note current DL model is similar but not yet adapted to the task. We would develop a modified version of this model which would be able to work  with the CAMS + openAQ dataset. We would include as inputs all three species, and output predictions of those species for the year, including met fields from CAMS. I

The Recurrent U-Net model has already proved viable in predicting summertime MDA8 surface ozone concentrations in the US, using meteorological fields from the ERA-interim reanalysis and monthly mean NOx emissions from the Community Emissions Data System (CEDS) inventory as predictors.

![map](map.png)
*Figure above shows a map of station locations on openAQ*

*A (conceptually simpler) one-dimensional approach would be to train the model to perform better at the station location, by penalizing it's error at the locations. However, this approach is limited due to the sparsity of station locations, and would fail to use the global nature of the CAMS model.*

A two-stage approach allows us to work with the sparse observations and the global  model. The first stage model would be a black-box version of CAMS. Then we can use a second stage to train the model at the station locations. The bias-correction would then be the difference between these two stages. This would provide better insight of CAMS's performance in specific regions. 

# Rough timeline

May: Gather and preprocess openAQ + CAMs data, reducing data size. Probably the longest of the tasks. The goal is to create a single 4D tensor containing relevant data (or figure out how to efficiently read in data during training from local CAMS + openAQ dataset during training.  Use Xarray (and possibly Dask) to handle large amounts of data.

Deliverable: a cohesive dataset which is able to be easily fed into a Tensorflow deep learning model

June: Modifying existing TensorFlow model architecture for stage one and second stage transfer learning. Train model on CAMS first, followed by training on openAQ. The first task should be simple, with the later being a bit more challenging. 

Deliverable: Trained TensorFlow model which is able to correct bias over USA

July: Regional analysis. Further improve model performance

Deliverable: Analysis + Results. Why is the model working well/not so well

August: Make reproducible, open source friendly, documentation and extendable to other regions

Deliverable : Well documented Github repository
