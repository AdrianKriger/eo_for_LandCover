 Land Cover from Satellite Imagery   <img align="right" src="../figs/Prediction_comparison.png">
============================

This is a personal project.
The intention is to create a small scale solution. 
If you are looking for a country or region-wide solution I suggest you investigate [eo-learn](https://github.com/sentinel-hub/eo-learn/tree/master/examples/land-cover-map) and [fastai](https://github.com/sentinel-hub/eo-learn/tree/master/examples/land-cover-fastai); on which these examples are built.

There are possibly easier methods and more efficient workflows to achieve the same result. A very cool example built with Google Cloud Platform can be found [here](http://jpbouchet.com/work/landcover-on-demand/).

This example was created to familiarize myself with creating a land cover map. It first works through the Machine Learing workflow on the [eo-learn](https://eo-learn.readthedocs.io/en/latest/examples.htmlIt) site and then does the same with the [fastai](https://github.com/sentinel-hub/eo-learn/tree/master/examples/land-cover-fastai) Deep Learning example. It does so with an extremely small area. One satellite image. 


### Data

This solution uses [Sentinel-2](https://www.sentinel-hub.com/) imagery and the [South African Land Cover (SANLC) 2018](https://www.environment.gov.za/projectsprogrammes/egis_landcover_datasets) as input:
 
   - A reference land cover is essential. Your local land cover will have all the classes deemed necessary within your area. The SANLC used in this example has 73 classes (which is alot). It is idosyncratic and specific within the context of South Africa's needs. Example: it differentiates formal settlement from informal settlements (slums, favelas, hoovervilles, squater camps). It was created with Sentinel imagery through a semi-automated process entailing an accuracy assessment at 6750 sample points throughout South Africa. It is of a very high standard.
   
    - You'll need an Area-of-Interest (AOI). This example covers an area within the [City of Cape Town](https://www.capetown.gov.za/). It contains a variety of built-environment and agricultural land within a 100km radius. Its a good test.
    
   - Because I did not have the resources to download an entire years worth of satellite imagery but wanted to test and work through both these solutions; I narrowed the search to when wonderful satellite imagery was available. To do so: access [Sentinel Hub](https://www.sentinel-hub.com/), search and note the date a series of suitable images are available. No more than one day should do. 
           
           You'll also need a Sentinel-hub account. You can get a trial version [here](https://www.sentinel-hub.com/). Once you have the account set up, login to Sentinel Hub Configurator. By default you will already have the default confoguration with an instance ID (alpha-numeric code of length 36). Instructions recommended that you create a new configuration (`Add new configuration`) and set the configuration to be based on Python scripts template. Such configuration will already contain all layers used in these examples. Otherwise you will have to define the layers for your configuration yourself.

            After you have decided which configuration to use, you have two options You can either put configuration's instance ID into sentinelhub package's configuration file following the [configuration instructions](https://sentinelhub-py.readthedocs.io/en/latest/configure.html) or you can write it down in the example notebooks.
     

### Process:

There are two solutions: A [LightGBM](https://lightgbm.readthedocs.io/en/latest/) machine learning model and a fastai method that uses [ResNet50]. Each folder contains the respective solution. For simplicity the workflow is broken down into several notebooks. 

    ## eo-learn:

       1) AOI, reference mask and Sentinel-2 imagery (or fill EOPatchs with data);
       2) Train, Test and Validate;
       3) Predict.

    ## fastai:

       1) AOI, reference mask and Sentinel-2 imagery (or fill EOPatchs with data);
       2) Retrieve a previously trained Sentinel-2 Deep Learning model. Train, Test and Validate;
       3) Inference.




    - [City of Cape Town](https://www.capetown.gov.za)
    - [Western Cape Government](https://www.westerncape.gov.za)
    - [Statistics South Africa (StatsSA)](http://www.statssa.gov.za)
    - [South African Police Service](https://www.saps.gov.za)
    - [Council for Scientific and Industrial Research (CSIR)](https://www.csir.co.za)
    
     
 - Although there is a strong possibility of using the:
 
     - [Global Human Settlements Population (GHS-POP)](https://ghsl.jrc.ec.europa.eu/datasets.php) 250m  layer as well.

### The tool will attempt to calculate several indicators about the selected area or areas:
*(this might not be a comparison but an assessment - The City of Cape Town has its own [ECAMP](https://web1.capetown.gov.za/web1/ecamp) evalutation. I don't know how it comes up with its numbers but it will give me a ground truth to gauge my results with)*

- Population distribution and demographics

    - Key statistics with graphs
    
    
- Population growth

    - Compare population from at least two different years
    - Visualize as graphs
    

- Accessibility:

     - Travel Times will focus on accessability to schools, health care and public transport. Also to one or more economic hubs (thus walking and driving).
     - Travel time calculation will be done through ```shortest paths``` on a road and along the local Integrated Bus-Rapid Transit network
     - Dominance areas will cull population numbers from the GHS layer.
     - Visualization through graphs and maps
     

- Green area index

     - Calculate the percentage of green areas.
     - Visualize the results.
     

- Street network metrics

    - Fetch street network data or use CoCT Open Data
    - Calculate street network metrics
    - Visualize the results
    

- Building density and Air Quality

    - Building polygons might be a challenge in South Africa and air quality might not be available for the area of interest. I'll look into it.
