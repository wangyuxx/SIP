# Sea ice mapping from Sentinel-1 SAR images using the SIP software

## Background

The information of sea ice in polar regions is crucial for various applications including 
climate change study and marine navigation. As an integral part of the Earth’s climate system, 
sea ice interacts with both the ocean and the atmosphere and modulates the heat and moisture fluxes.
In particular, the extent and distribution of sea ice relative to open sea water are important
indicators of the contraction of Arctic ice caps, and has been recognized as essential climate
variables by both world meteorological organization (WMO) and the United Nations framework
convention on climate change (UNFCCC). Moreover, sea ice and open water distribution
information is also important for ship navigation along Arctic sea routes that greatly shorten the
marine transportation distance between northwestern Europe and northeastern Asia.

Satellite synthetic aperture radar (SAR), due to its capability to penetrate the cloud and work
day and night, provides a powerful tool for sea ice monitoring. The Sentinel-1 satellite generates
immense free SAR images over the Arctic area, allowing operational monitoring of sea ice
extend and dynamics. Nevertheless, fast and accurate discrimination of sea ice and open water
from Sentinel-1 SAR imagery using traditional machine learning techniques is difficult due to the
huge data volume, sensor limitations, and the complex ocean state. To address these problems
for large-scale sea ice mapping, it is important to investigate the GPU-boosted deep neural
network approach that is very efficient at handling the big complex data.

## Overall Objective

* We have initiaed a project that aims to use the SIP software system with innovative deep neural network models
tailored to the Sentinel-1 SAR sea ice characteristics for fast and accurate production of sea ice
maps over large Arctic area using big Sentinel-1 SAR data in support of the climate change
study and Arctic ship navigation, with the following sub-objectives:

  * Design novel convolutional neural network (CNN) models and algorithms that are capable of not only
efficiently capturing the subtle textual signature of sea ice from Sentinel-1 imagery but also
accurately preserving the edges and boundaries between semantic classes. 

  * Optimize SIP to allow the use of desktop-based computational power for processing a large number of Sentinel-1 images
in a meaningful spatial-temporal scale. Also, based on SIP, build an online cloud-based operational sea ice mapping system
that generate high-precision pixel-level sea ice maps and ice charts that benefits various climate
change researchers and end-users.

## Tutorial Objectives

As the first step, this tutorial has the following objectives:

* ***Compare the performance of two typical CNN architectures***, i.e., (1) pixel/patch-based CNN architecture that outputs
the label of a single pixel, and (2) image-based fully convolutional CNN architecture that outputs a label map of 
all pixels on the image. 

    * Both approaches are residual neural network;
    * Approach (1) tends to have a smaller field of view than approach (2) that 
has many convolutional and pooling layers, and therefore may be less efficient at texture feature extraction;
    * If the input image patch is big, approach (1) is less efficient at preserving small objects and class boundaries,
whereas approach (2) can do a better job using some detail-perservation tricks, e.g., skip connnections;
    * Due to patch-overlapping, approach (1) requires more GPU memories during training;
    * Approach (1) is trained on pixel samples which are relatively easier to obtain with a large quantity, 
whereas approach 2 is trained on much less image samples whose full label maps are difficult to obtain;

* ***Combine approach (1) and (2) to develop a semi-supervised classification approach*** (3).

## Experiments

1. ***Experiment with approach 1***

   1. Train approach (1) using pixels sampels collected from the training images;
   1. Use the trained (1) to generate full label maps for training and test images;
   1. Calculate training, validation and test accuracies for approach (1)

1. ***Experiment with approach 2***

    1. Train approach (2) using image samples whose label maps are sparse in the sense that only 
some pixels on these maps have labels, and most pixels do not have labels;
    1. Use the trained (2) to generate full label maps for training and test images;
    1. Calculate training, validation and test accuracies for approach (2)

1. ***Experiment with approach 3***

    1. Train approach (2) using generated full label maps of the training images generated in experiment 1 step ii;
    1. Use the trained (2) to predict full label maps of training images, validation images and test images; 
    1. Calculate the training, validation and test accuracies of this approach, which is approach 3;
    1. Compare the accuracies of approach 1, 2, and 3 to see whether approach 3 has the highest accurcies;

## Procedures of Experiment 1

1. **Download data**
  1. Go to https://search.asf.alaska.edu/#/. Please copy *POLYGON((-169.5982 69.4421,-157.2591 71.9421,-141.6889 70.0305,-135.3576 69.9672,-127.5021 71.384,-139.323 78.3118,-164.763 80.1023,-169.5982 69.4421))* and paste it to **Area of Interet** in the webpage. Click ***Filters*** and set ***starting date*** and ***end date*** to be 2019.09.01, ***File type*** to be L1 GRD MD, and ***Beam Mode*** to be EW. Click on ***Search***, and you should find 10 scenes. Download them. 
  
1. **Run app and open data.** 
  1. Run SIP;
  1. Open the '.json' file in ***'SIP/data/sentinel1_preprocessed_imgs'***;
  1. Also open the associated '.tiff' image.

1. **Step 2: Draw region of interst (ROI).**  
  1. ***Double click a class*** in the 'Label List' panel on the right to choose a class; 
  1. Draw point, or line or polygon to add more ROI for this class;
  1. ***To finish drawing line and polygon, type 'c' from keyboard***;
  1. Save drawing using default name;

1. **Step 3: Edit config file.** 
  1. Copy the ***config_os.yaml.bak*** in the config folder and change its name to ***config_os.yaml***;
  1. Find ***sentinel1_params***, ***raw_data_dir***, ***dirs***; ***For all directories in these three parameters, make sure you have changed them to your own directories***.

1. **Step 4: Prepare label mask.** 
  1. Click on ***"Get masks"*** under ***Classification*** menu;
  1. First select the config file you just edited, and then select the csv file you just saved;
  1. This step transfer ROIs from vectors to mask images;
  1. Take a look at the png images generated in the ***raw_img_dir*** directory in the config file;

1. **Step 5: Prepare all dirs and data.** 
  1. Click on ***"Prepare data"*** under ***Classification*** menu to prepare all training, test and prediction data. 
  1. You need to choose the .yaml 'config' file you just edited. 
  1. Once finished, go to ***dirs->data->train/val/test/predict*** folders in the config file, to open and take a look at the ***data_file.yaml*** files. Think about why ***dirs->data/predict*** has different image with train, val and test.   

1. **Step 6: Train classifier.** 
  1. Click on ***'Train classifier'*** under ***Classification*** menu and then choose the .yaml config file you just edited. 
  1. Once training is finished, go to ***raw_data_dir*** in the config file to take a look at the generated label maps of the training images. 
  1. Go to ***dirs->save->model*** folder in the config file, check ***the training and validation accuracies*** in the ***train.log*** file.

1. **Step 7: Test classifier.** 
  1. You can optionally run ***"Test classifier"*** under the ***Classification***, but it will run on the same image using the trained model in Step 6. 
  1. You also need to select the same .yaml config file. 
  1. Check the ***test accuracies*** in the "test.log" file under the ***dirs->save->model*** folder in the config file.  

1. **Step 8: Predict label map on a new image.** 
  1. Click on ***"Predict image"*** under the ***Classification*** menu to run the trained model on the other scene in the ***raw_img_dir*** folder. You also need to select the same config file. 
  1. Once it is done, you can check the label map of the test image in the ***raw_img_dir*** folder.
  1. Check the "predict.log" file under the ***dirs->save->model*** folder in the config file. 


