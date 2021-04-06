---
#esowc
#deep_learning
---

# Challenge #21 - Machine Learning to improve the CAMS global air quality forecasts

CAMS runs a global climate model (GCM) to predict global air pollution at resolution of 40km x 40km. Due to the scale of the GCM and uncertainties in inputs, there are errors when trying to accurately predict air quality on regional scales. Hence, bias correction methods must be used as a post-processing step to minimize bias.

Traditional bias-correcting methods assume that the bias is constant across time. Additionally, due to the spatially sparse air quality observations, it is hard to leverage spatial structure when deploying bias correction methods.

Hence, we propose a Recurrent U-Net Deep Learning model which will be able to capture the time-varying behavior of the bias, and individually correct at each location by considering the meteorogical factors

- (*how are we leveraging spatial structure if at all*?)
- **consider the openAQ fragmentation process**

**Problem**: Developing an ML algorithm to predict and correct the time-varying bias of the global CAMS forecast for surface PM2.5, O3 and NO2 at the locations of the air-quality monitoring stations.

**Solution**: Use a Recurrent U-Net model to capture the variability at the station locations.

The Recurrent U-Net model has already proved viable in predicting summertime MDA8 surface ozone concentrations in the US [cite Tailong's preprint on arxiv], using meteorogical fields from the ERA-interim reanalysis and monthly mean NOx emissions from the Community Emissions Data System (CEDS) inventory as predictors. The model is able to capture daily, seasonal and interannual variability in MDA8 ozone across US with $r^2$ = 0.83.

We would develop an modified version of this model which would be able to work well with the openAQ dataset

How many station locations? (from openAQ)
NO2 1476 
O3 2661
PM2.5 20406

Different amounts of training data and thus 3 different models for (same architecture) each species.

April: Proposal + Research + brushing up on Python stack (Xarray + possibly Dask?) + TensorFlow2. (unsure about integrating Dask with tf2), Pangeo stack
May - June: Gather and preprocessing data, reducing data size. Probably the longest of the tasks. The goal is to create a single 4D tensor containing relevant data (or figure out how to efficiently read in data during training from local CAMS + openAQ dataset)
June-July: Modifying existing TensorFlow model architecture to read data and improve model performance.
July-August: Analysis over different regions.




