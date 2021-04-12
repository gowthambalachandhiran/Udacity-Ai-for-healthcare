Name : Gowtham Balachandhiran

Name of the modality : Hippocampus volume quantification to gauge Alzheimer's Disease(HiVAD)

***Objective of the modality***:
The objective of the modality is to capture the risk of population by quantifying the volume of Hippocampus tissue. We are leveraging an AI model which can predict mask which is indicative of hippocampus tissue in the brain. This will help us understand if there are any evidence of tissue atrophy causing dementia due to Alzheimer's Disease.

***What data was used in training the model***
We are using the "Hippocampus" dataset from the Medical Decathlon competition. This dataset is stored as a collection of NIFTI files, with one file per volume, and one file per corresponding segmentation mask. The original images here are T2 MRI scans of the full brain. As noted, in this dataset we are using cropped volumes where only the region around the hippocampus has been cut out. But segmentation is still hard. 

***How did you label your training data?***
All data has been labeled and verified by an expert human rater, and with the best effort to mimic the accuracy required for clinical use. This refers to the silver standard.

***Evaluation Metric***
We have used dice score and jaccard score for metric calculation.

Dice score formula = 2 * |X intersction Y | / |x| + |Y|
Jaccard score = 1 - |X intersection Y|/|X union Y|

###Algorithm and training and performance

We can see from the graph that training and validation error has reduced

<img src="../../section2/out/TrainVsValLoss.png" alt="Flowchart" height="400"/>

***Please find the performance metrics***
"overall": {
    "mean_dice": 0.8870042299687226,
    "mean_jaccard": 0.4435021149843613
  }
  
We are nearing 90% of mean dice however we could have done better in Jaccard score.
  
### What will the model predict
We have the radiologist annotate the mask from the original image. This is going to be the interesting areas or part Hippocampus tissue. Since this is cropped image this will have greater focus on interesting tissue.
  
  
  ***Integration of the AI module with a front end***
  We can send image from PACS in DICOMM and NIFI file format. The image will be sent to the AI module. The module will be predicting the mask and probability mask heatmap.
  
You can see the mask annotated by radiologist
  
<img src="../../section2/out/Mask1.png" alt="Mask1" height="400"/>
 
Predicted mask by our model corresponding to the annotated mask

<img src="../../section2/out/Prediction1.png" alt="Prediction1" height="400"/>  

Corresponding probability map could be found below.

<img src="../../section2/out/Probabilitymap1.png" alt="Probabilitymap1" height="400"/>

### In case of incorrect coverage of predicted mask compared with original mask 

***In case predicted mask is bigger than original area of interesting tissue***

This will give a wrong perception that the tissue has no degeneration. For example if the actual volume in mm3 is 3500 and if the coverage by the model is bigger it would have impact on volume which would mean false inflation of tissue which would interpret that this is normal and may not indicate Alzheimer's Disease (False Negative). This will have impact on sensitivity on the model.

***In case predicted mask is smaller than original area of interesting tissue***

This will falsely interpret that there is evidence for the degeneration of the tissue. This will create false positives from the sample. This will have impact on the precision of the model.

### How can we improve our model

 We could afford more silver standards leveraging more radiologist but it is a costlier method.

We could get more synthesize more data from augumentation technique but since this is a 3d image and each slice is part of the data it becomes difficult to augment at a slice level.

Other alternative is collect more series and associated study(More data) sample. 

We could also increase the complaxity of the model which add more non-linearities in the model to learn more 








  


  
  