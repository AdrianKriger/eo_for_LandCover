 Land Cover from Satellite Imagery   
============================

This is a personal project.
The intention is to create a small scale solution. 
If you are looking for a country or region-wide solution I suggest you investigate [eo-learn](https://github.com/sentinel-hub/eo-learn/tree/master/examples/land-cover-map) and [fastai](https://github.com/sentinel-hub/eo-learn/tree/master/examples/land-cover-fastai); on which these examples are built.

There are possibly easier methods and more efficient workflows to achieve the same result. A very cool example built with Google Cloud Platform can be found [here](http://jpbouchet.com/work/landcover-on-demand/).

This example was created to familiarize myself with creating a land cover map. It first works through the Machine Learning workflow on the [eo-learn](https://eo-learn.readthedocs.io/en/latest/examples.htmlIt) site and then does the same with the [fastai](https://github.com/sentinel-hub/eo-learn/tree/master/examples/land-cover-fastai) Deep Learning example. It does so with an extremely small area. One satellite image. 

### Data

This solution uses [Sentinel-2](https://www.sentinel-hub.com/) imagery and the [South African Land Cover (SANLC) 2018](https://www.environment.gov.za/projectsprogrammes/egis_landcover_datasets) as input:
 
   - A reference land cover is essential. Your local land cover will have all the classes deemed necessary within your area. The SANLC used in this example has 73 classes (which is alot). It is idosyncratic and specific within the context of South Africa's needs. Example: it differentiates formal settlement from informal settlements (slums, favelas, hoovervilles, squater camps). It was created with Sentinel imagery through a semi-automated process entailing an accuracy assessment at 6750 sample points throughout South Africa. It is of a very high standard -  - I merged some of these classess to meet my desires.
   
   - You'll need an Area-of-Interest (AOI). This example covers an area within the [City of Cape Town](https://www.capetown.gov.za/). It contains a variety of built-environment and agricultural land within a 100km radius. Its a good test.
    
   - Because I did not have the resources to download an entire years worth of satellite imagery but wanted to test and work through both these solutions; I narrowed the search to when wonderful satellite imagery was available. To do so: access [Sentinel Hub](https://www.sentinel-hub.com/), search and note the date a series of suitable images are available. No more than one day should do. 
           
     You'll also need a Sentinel-hub account. You can get a trial version [here](https://www.sentinel-hub.com/). Once you have the account set up, login to Sentinel Hub Configurator. By default you will already have the default configuration with an instance ID (alpha-numeric code of length 36). Instructions recommended that you create a new configuration (`Add new configuration`) and set the configuration to be based on Python scripts template.

     After you have decided which configuration to use, you can either put the configuration's instance ID into sentinelhub package's configuration file following the [configuration instructions](https://sentinelhub-py.readthedocs.io/en/latest/configure.html) or you can write it down in the example notebooks. 

### Process:

There are two solutions: A [LightGBM](https://lightgbm.readthedocs.io/en/latest/) machine learning model and a fastai method that uses [ResNet50]. Each folder contains the respective solution. For simplicity the workflow is broken down into several notebooks. 

    ## eo-learn:

       1) Select Area and create AOI
       2) Access Sentinel-2 imagery, and along with reference Land Cover, create data for training (or fill EOPatchs);
       3) Train, Test and Validate;
       4) Predict.

    ## fastai:

       1) Select Area and create AOI
       2) Access Sentinel-2 imagery, and along with reference Land Cover, create data for training (or fill EOPatchs);
       3) Retrieve a previously trained Sentinel-2 Deep Learning model. Train, Test and Validate;
       4) Inference.
