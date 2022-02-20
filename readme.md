# GUN DETECTOR USING SSD

### Description
 Detecting guns present in the image 
_Input_: Normal image containing Gun.
_Output_: Valid classes: 'Gun'

## Tensorflow Object detection API:
  1. Followed Tensorflow Official object detection API DOC to setup the tensorflow object detection API [TFOD2](https://tensorflow-object-detection-api-tutorial.readthedocs.io/en/latest/)

  2. Followed this to setup the TFOD2 API and custom object detection folder structure.

## Data Preparation   
  1. Converted text annotations into xml annotations then these xml annotations are used to generate tf records.
  2. used [DATA PREPROCESSING](data_preprocessing.ipynb) to generate the xml files.

## Training data 

In current dataset contains 330 training images and trained with 320*320 dimensions 

 Train Dataset | Test | 
| --- | --- |
| 312| 20|

Trained the model with batch size 2 and total steps of 5000 steps which means our epochs are roughly 32


## Training instructions: 
we will start training from /train directory.

1. To train the model first we need to generate the train and test.records file as our model will expect this as input. we will generate that using [GENERATE TF RECORDS](/train/generate_tfrecord.py)
2. Download the SSD pretrained model file from [Model Zoo](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/tf2_detection_zoo.md) and move it into pretrained folder and extract it using tar -xvf file_name
3. create a models folder in train and move the pipeline.config there as this is our main model folder where all checkpoints will be stores.
4. edit this config files with suitable parameters as in out case class was changed to 1 and other pretrained model paths and eval paths, batch size, total steps were defined here.
5. start the training using [START TRAINING](/train/model_main_tf2.py)
6. Evaluate the model using the same train file but pass the checkpint dir path in argsparser.
7. Export the model for Inferencing using [Export model](/train/exporter_main_v2.py) and Exported model is saved in exported directory.

For detailed training process we can follow instructions provided in [TFOD2 API](https://tensorflow-object-detection-api-tutorial.readthedocs.io/en/latest/)


### Current performance metrics 

 
Following is the screenshot for model evaluation on 20 test images.

For our model Average Presion for IOU 0.5 is .22, as we can see our AP is very less, as the quality of the images provided is very low and few objects have multiple class and very cluttered data, we can improve the map by colleting more good quality data. and overall training data is also very less so gathering mode data can help boosting the mAP.

Detailed Evaluation matrix screenshot can be found below:

 <img src = "files/modeal_eval.png" height="720" width="1080"/> 


## Inference:
Model Inference is written in [INFERENCE NOTEBOOK](inference.ipynb)


### Testing instructions 

1.Copy Utils folder in from model/objectdetection/utils or install the TFOD2 API as mentioned above

2.Install dependencies using requirements.txt file

3.Use [INFERENCE NOTEBOOK](inference.ipynb) to test the model on different images.
