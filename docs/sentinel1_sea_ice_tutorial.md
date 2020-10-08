# Sea ice mapping from Sentinel-1 SAR images using the SIP software

## Background

The information of sea ice in polar regions is crucial for various applications including climate change study and marine navigation. As an integral part of the Earth’s climate system, sea ice interacts with both the ocean and the atmosphere and modulates the heat and moisture fluxes.
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

Our projects therefore aims to design innovative deep neural network models and systems
tailored to the Sentinel-1 SAR sea ice characteristics for fast and accurate production of sea ice
maps over large Arctic area using big Sentinel-1 SAR data in support of the climate change
study and Arctic ship navigation. We have been making significant progress on designing novel
convolutional neural network (CNN) models and algorithms that are capable of not only
efficiently capturing the subtle textual signature of sea ice from Sentinel-1 imagery but also
accurately preserving the edges and boundaries between semantic classes. Nevertheless, the
value and impact of our research are critically bottlenecked by the limitations of our
desktop-based computational power, which does not allow us to leverage complex fully
convolutional CNN architectures that proved to achieve much higher accuracy than our current
approaches, and also prohibits us from processing a large number of Sentinel-1 images for
achieving a meaningful spatial-temporal scale. We therefore strongly hope that we can receive
the support from Microsoft Azure cloud computing platform, which will help us overcome our
limitations and enable us to achieve an online cloud-based operational sea ice mapping system
that generate high-precision pixel-level sea ice maps and ice charts that benefits various climate
change researchers and end-users.

## Steps

**Step 1: Run app and open data.** 
- Run SIP;
- Open the '.json' file in ***'SIP/data/sentinel1_preprocessed_imgs'***;
- Also open the associated '.tiff' image.

**Step 2: Draw region of interst (ROI).**  
- ***Double click a class*** in the 'Label List' panel on the right to choose a class; 
- Draw point, or line or polygon to add more ROI for this class;
- ***To finish drawing line and polygon, type 'c' from keyboard***;
- Save drawing using default name;

**Step 3: Edit config file.** 
- Copy the ***config_os.yaml.bak*** in the config folder and change its name to ***config_os.yaml***;
- Find ***sentinel1_params***, ***raw_data_dir***, ***dirs***; ***For all directories in these three parameters, make sure you have changed them to your own directories***.

**Step 4: Prepare label mask.** 
- Click on ***"Get masks"*** under ***Classification*** menu;
- First select the config file you just edited, and then select the csv file you just saved;
- This step transfer ROIs from vectors to mask images;
- Take a look at the png images generated in the ***raw_img_dir*** directory in the config file;

**Step 5: Prepare all dirs and data.** 
- Click on ***"Prepare data"*** under ***Classification*** menu to prepare all training, test and prediction data. 
- You need to choose the .yaml 'config' file you just edited. 
- Once finished, go to ***dirs->data->train/val/test/predict*** folders in the config file, to open and take a look at the ***data_file.yaml*** files. Think about why ***dirs->data/predict*** has different image with train, val and test.   

**Step 6: Train classifier.** 
- Click on ***'Train classifier'*** under ***Classification*** menu and then choose the .yaml config file you just edited. 
- Once training is finished, go to ***raw_data_dir*** in the config file to take a look at the generated label maps of the training images. 
- Go to ***dirs->save->model*** folder in the config file, check ***the training and validation accuracies*** in the ***train.log*** file.

**Step 7: Test classifier.** 
- You can optionally run ***"Test classifier"*** under the ***Classification***, but it will run on the same image using the trained model in Step 6. 
- You also need to select the same .yaml config file. 
- Check the ***test accuracies*** in the "test.log" file under the ***dirs->save->model*** folder in the config file.  

**Step 8: Predict label map on a new image.** 
- Click on ***"Predict image"*** under the ***Classification*** menu to run the trained model on the other scene in the ***raw_img_dir*** folder. You also need to select the same config file. 
- Once it is done, you can check the label map of the test image in the ***raw_img_dir*** folder.
- Check the "predict.log" file under the ***dirs->save->model*** folder in the config file. 


