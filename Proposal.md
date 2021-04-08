---
#esowc
#deep_learning
---

# Challenge #21 - Machine Learning to improve the CAMS global air quality forecasts

CAMS runs a global climate model (GCM) to predict global air pollution at resolution of 40km x 40km. Due to the scale of the GCM and uncertainties in inputs, there are errors when trying to accurately predict air quality on regional scales. Hence, bias-correction methods are used as a post-processing step to minimize bias.

Simple bias-correcting methods assume that the bias is constant across time. Additionally, due to the spatially sparse air quality observations, it is hard to leverage spatial structure when deploying bias-correction methods. This problem is further complicated when considering a global model.

In order to improve bias-correction, we propose a 2 stage transfer learning approach using a Recurrent U-Net Deep Learning model, which will be able to capture the time-varying behavior of the model and then the bias.

 We would conduct the study initially on a specific region (e.g. Europe) which would serve as a proof of concept. This model would then be trained on different regions. We have a more observations over Europe and USA. *This model could then be used on sparser regions, East Asia, Austraia*

![map](map.png)

*A (conceptually simpler) one-dimensional approach would be to train the model to perform better at the station location, by penalizing it's error at the locations. However, this approach is limited due to the sparsity of station locations, and would fail to use the global nature of the CAMS model.*

A two-stage approach allows us to work with the sparse observations and the global  model. The first stage model would be a black-box version of CAMS. Then we can use a second stage to train the model at the station locations. The bias-correction would then be the difference between these two stages. This would provide better insight of CAMS's performance in specific regions. 

- **Consider the openAQ fragmentation process, especially in regard to the error, source type**
  i.e. the source-type and  mobility, distinguish between reference-grade and low-cost sensor data

The Recurrent U-Net model has already proved viable in predicting summertime MDA8 surface ozone concentrations in the US [cite Tailong's preprint on arxiv], using meteorogical fields from the ERA-interim reanalysis and monthly mean NOx emissions from the Community Emissions Data System (CEDS) inventory as predictors. *more information about Tailong's model.*

We would develop an modified version of this model which would be able to work well with the openAQ dataset

How many station locations? (from openAQ)
- NO2 1476 
- O3 2661
- PM2.5 20406

Different amounts of training data and thus 3 different models for (same architecture) each species. Inclusion of all 3 gases could potentially increase/decrease  model performance. 

# Timeline

May: Gather and preprocess openAQ data, reducing data size. Probably the longest of the tasks. The goal is to create a single 4D tensor containing relevant data (or figure out how to efficiently read in data during training from local CAMS + openAQ dataset). Use Xarray (and possibly Dask) to handle big data.

Deliverable: cohesive dataset

Mid- June: Modifying existing TensorFlow model architecture for 2nd stage transfer learning

Deliverable: Trained TensorFlow model

July: Regional analysis. Extend to other regions.

August: Make opensource freindly, documentation and presentation

## More specifics