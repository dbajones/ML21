Challenge #21 - Machine Learning to improve the CAMS global air quality forecasts

Problem: Developing an ML algorithm to predict and correct the time-varying bias of the global CAMS forecast for surface PM2.5, O3 and NO2 at the locations of the air-quality monitoring stations.

Solution: Use a Recurrent U-Net model to capture the variability at the station locations

How many station locations? (from openAQ)
NO2 1476 
O3 2661
PM2.5 20406

Different amounts of training data and thus 3 different models for (same architecture) each species.

April: Proposal + Research + brushing up on Python stack (Xarray + possibly Dask?) + TensorFlow2. (unsure about integrating Dask with tf2)
May - June: Gather and preprocessing data, reducing data size. Probably the longest of the tasks. The goal is to create a single 4D tensor containing relevant data (or figure out how to efficiently read in data during training from local CAMS + openAQ dataset)
June-July: Modifying existing TensorFlow model architecture to read data and improve model performance. Modify the loss function to 
July-August: Analysis over different regions.

Problem: the openAQ dataset is spatially sparse




