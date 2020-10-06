# First example: Process Sentinel-1 SAR image for sea ice classification

![](./pics/classify.gif)

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
- Once training is finished, you can see the generated label map by clicking on this file in the 'Image List' panel on the left. 
- Check ***the training and validation accuracies*** in the "train_log" file under the "save_model" folder specified in the .yaml config file you edited. 
- Change the ***number of epoches*** in the .yaml config file and see what happens. 

**Step 7: Test classifier.** 
- You can optionally run ***"Test classifier"*** under ***classification***, but it will run on the same image using the trained model in Step 6. 
- You also need to select the same .yaml config file. 
- Check the ***test accuracies*** in the "test_log" file under the "save_model" folder specified in the .yaml config file.  

**Step 8: Predict label map on a new image.** 
- Click on ***"Predict image"*** to run the trained model on the other scene in the folder.
- Once it is done, you can also check the label map in the "Image List" panel. You also need to select the same .yaml config file.
- Check the "predict_log" file under the "save_model" folder specified in the .yaml config file. 


