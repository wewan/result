# Result
## Usefull Material to be Tried (Important)
* **[CheXNet: Radiologist-Level Pneumonia Detection on Chest X-Rays with Deep Learning](https://stanfordmlgroup.github.io/projects/chexnet/)**<br />
* **[MSFCN-multiple supervised fully convolutional networks for the osteosarcoma segmentation of CT images
Author links open overlay panel](http://www.sciencedirect.com/science/article/pii/S0169260716310926)**
* **[Densely Connected Convolutional Networks](https://arxiv.org/abs/1608.06993)**
## Add Batch Normalization to Unet
According
[Batch Normalization: Accelerating Deep Network Training by Reducing Internal Covariate Shift](https://arxiv.org/abs/1502.03167) <br />
(Training) &nbsp;**Grey**: BN after Relu &nbsp;&nbsp;  **Pink**: BN before Relu &nbsp;&nbsp;   **Red**: without BN 
<img src="results/BNdiff.png" width=1024 />
(Testing)&nbsp; **Orange**: BN after Relu  &nbsp;&nbsp;  **Green**: BN before Relu &nbsp;&nbsp;  **Blue**: without BN
<img src="results/BNdifftest.png" width=1024 />

##  Training 1 Image
### Pure training
The training dice accuracy is around [0.991 0.991] <br />
The testing dice accuracy is around [0.802 0.831] <br />
Summary:
<img src="results/train1image.png" width=1024 />
Repeated:
<img src="results/train1image_repeated.png" width=1024 />
**Conlucsion: result could varies a bit from training**

Test Images:
<img src="results/Train1Image_valid1.png" width=1024 />
### Pure Context
**Context Parameter**:<br />
*model weight*:0.3  &nbsp;*CurvatureWeighting*:0.2  &nbsp;*MaxIteration*:30 &nbsp; *MaxInitialIteration*:30<br />
**Network Structure**
<img src="results/unet1.png" width=1024 />


The training dice accuracy is around [0.991 0.990] <br />
The testing dice accuracy is around [0.7735 0.7686] <br />
Summary:
<img src="results/Train1image_summary.png" width=1024 />
Test Images:
<img src="results/Train1img_puretrain_test.png" width=1024 />

### Zero Cross Context
**Context Parameter**:<br />
*model weight*:0.3  &nbsp;*CurvatureWeighting*:0.2  &nbsp;*MaxIteration*:30 &nbsp; *MaxInitialIteration*:30<br />
**Network Structure**:same with above
*Training*:<br />

||ZEROS        | CROSS         |CONTEXT
|------------ |------------ | ------------- | -------------
**1**|0.988 | 0.991|0.9914
**2**|0.9874 | 0.9902|0.9910

*The testing*:<br />

||ZEROS        | CROSS         |CONTEXT
|------------ |------------ | ------------- | -------------
**1**|0.5825 | 0.8077|0.8046
**2**|0.010 | 0.7961|0.7916

Summary:
<img src="results/Train1image_zerocross_summary.png" width=1024 />

### To be tried 

<img src="results/MSfcn.png" width=1024 />

**combined loss from different layers(used in MSFCN)**
<img src="results/combined_loss.png" width=512 /><br />
Ref: [Object Skeleton Extraction in Natural Images by Fusing Scale-associated Deep
Side Outputs
Supplementary Material](http://openaccess.thecvf.com/content_cvpr_2016/supplemental/Shen_Object_Skeleton_Extraction_2016_CVPR_supplemental.pdf)



## EXTERNTION

Self-cycle three times:
<img src="results/RUNET.png" width=1024 />
20folds Training acc :0.97-0.99<br />
20folds Testing acc : 0.01-0.70<br />
**Unstable**<br />

Self-cycle three times:
<img src="results/RUNET_1.png" width=1024 />
20flods Training acc :0.97-0.99<br />
20folds Testing acc : 0.40-0.90<br />
**Unstable(better than 0)**<br />

<img src="results/runet_2.png" width=1024 />
20folds Training 0.97-0.99<br />
20folds Testing  ----0.85 (min 0.69 max 0.9)<br />

To try:
MSFCN






































## IOU of 5-Folds-CV,10-Folds-CV 
##### 5-Folds-CV:<br />
The dice accuracy of training is around 0.98 <br />
The dice accuracy of testing  is around 0.95 <br />
<img src="results/IOU_5folds.png" width=1024 />
From pictures above we could see the testing accuracy increase a lot after 70 steps <br />
##### 10-Folds-CV:<br />
The dice accuracy of training is around 0.97<br />
The dice accuracy of testing  is around 0.94<br />
<img src="results/IOU_10folds.png" width=1024 />
From pictures above we could see the testing accuracy increase a lot after 120 steps<br />
##### Average reuslts of 10-Folds-CV after 250 epochs:
<img src="results/average_results7.png" width=1024 />
<img src="results/average_result8.png" width=1024 />
<img src="results/average_result9.png" width=1024 />
<img src="results/average_result10.png" width=1024 />


## Histogram of 5-Folds-CV,10-Folds-CV 
##### 5-Folds-CV:<br />
<img src="results/Histogram_5folds_train.png" width=430  /><img src="results/Histogram_5folds_test.png" width=430  />
##### 10-Folds-CV:<br />
<img src="results/Histogram_train_10folds.png" width=430  /><img src="results/Histogram_test_10folds.png" width=430 />

## Images of outputs 
##### 5-Folds-CV, 200epochs<br />
<img src="results/5folds_preds.png" width=1024 />

##### 10-Folds-CV, 250epochs<br />
<img src="results/saveimgs_10folds.png" width=1024 />

##### 5-Folds-CV, preds screenshots<br />
<img src="results/Preds_5folds_200epochs.png" width=1024 />

##### 10-Folds-CV, preds screenshots<br />
<img src="results/preds_10folds.png" width=1024 />

##  Test while traing 5-Folds-CV
<img src="results/49images_train.png" width=1024 />
extract testing preds after 60 epochs<br />
<img src="results/60epochs.png" width=1024 />
extract testing preds after 60 epochs<br />
<img src="results/80epochs.png" width=1024 />


