# Result
## Usefull Material to be Tried 
* **[CheXNet: Radiologist-Level Pneumonia Detection on Chest X-Rays with Deep Learning](https://stanfordmlgroup.github.io/projects/chexnet/)**<br />
* **[MSFCN-multiple supervised fully convolutional networks for the osteosarcoma segmentation of CT images
Author links open overlay panel](http://www.sciencedirect.com/science/article/pii/S0169260716310926)**
* **[Densely Connected Convolutional Networks](https://arxiv.org/abs/1608.06993)**
## Add Batch Normalization to Unet Layers
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
Repeated:<br />
The training dice accuracy is around [0.9913 0.9910] <br />
The testing dice accuracy is around [0.836 0.8071] <br />
<img src="results/train1image_repeated.png" width=1024 />
**Conlucsion: result could varies a bit from training**
Test Images:
<img src="results/Train1Image_valid1.png" width=1024 />
### Context Methods
* **structure**<br /> Connect Ways, Inputs, layer numbers, dropouts, loss should be adjust 
<img src="results/unet_methods.png" width=1024 />

* **Context Generator** (**MiaLab**)<br /> 
Generating context influence the outcome a lot. Changing parameters(*model weight*  &nbsp;*CurvatureWeighting*  &nbsp;*MaxIteration* &nbsp; *MaxInitialIteration*) correctly to get around this.

* **Training Ways**<br /> 
  * pure context
  * zero cross context
  * random cross context

### Pure Context 
**Context Parameter**:<br />
*model weight*:0.3  &nbsp;*CurvatureWeighting*:0.2  &nbsp;*MaxIteration*:30 &nbsp; *MaxInitialIteration*:30<br />
First is train image<br />
<img src="results/shapecontex_train.png" width=210 />
<img src="results/shapecontext_valid.png" width=210 />
<img src="results/shapecontext_valid_2.png" width=210 />
<img src="results/shapecontext_valid_3.png" width=210 />
<img src="results/shapecontext_valid_4.png" width=210 />
<img src="results/shapecontex_valid_5.png" width=210 />
<img src="results/shapecontext_valid_6.png" width=210 />
<img src="results/shapecontext_valid_7.png" width=210 />

**Network Structure**
<img src="results/unet1.png" width=1024 />
The training dice accuracy is around [0.991 0.990] <br />
The testing dice accuracy is around [0.7735 0.7686] <br />
Summary:
<img src="results/Train1image_summary.png" width=1024 />
Test Images:
<img src="results/Train1img_puretrain_test.png" width=1024 />

### Random Cross Context 1
**Context Parameter**:<br />
*model weight*:0.3  &nbsp;*CurvatureWeighting*:0.2  &nbsp;*MaxIteration*:30 &nbsp; *MaxInitialIteration*:30<br />
<img src="results/shapecontex_train.png" width=210 />
<img src="results/shapecontext_valid.png" width=210 />
<img src="results/shapecontext_valid_2.png" width=210 />
<img src="results/shapecontext_valid_3.png" width=210 />
<img src="results/shapecontext_valid_4.png" width=210 />
<img src="results/shapecontex_valid_5.png" width=210 />
<img src="results/shapecontext_valid_6.png" width=210 />
<img src="results/shapecontext_valid_7.png" width=210 />
**Network Structure**:same with above
*Training*:<br />

||Random        | CROSS         |CONTEXT   | PureContext
|------------ |------------ | ------------- | -------------| -------------
**1**|0.988 | 0.991|0.9914|**->0.991**
**2**|0.9874 | 0.9902|0.9910|**->0.991**

*The testing*:<br />

||Random        | CROSS         |CONTEXT  |PureContext
|------------ |------------ | ------------- | -------------| -------------
**1**|0.5825 | 0.8077|0.8046|**->0.802**
**2**|0.010 | 0.7961|0.7916|**->0.831**

Summary:<br />
(from folds 2, it indicats test acc could converge to **0** some times when training with zeros)
<img src="results/Train1image_zerocross_summary.png" width=1024 />

Random Images-fold1&fold2:<br />
<img src="results/train1image_zeros.png" width=430 />
<img src="results/train1image_zeros_2.png" width=430 />

Random Cross Images-fold1&fold2:<br />
<img src="results/train1image_all.png" width=430 />
<img src="results/train1image_all_1.png" width=430 />

Context Images-fold1&fold2:<br />
<img src="results/train1image_zerocross.png" width=430 />
<img src="results/train1image_zerocross_2.png" width=430 />
### zeros Cross Context 1
**Context Parameter**:<br />
*model weight*:0.3  &nbsp;*CurvatureWeighting*:0.2  &nbsp;*MaxIteration*:30 &nbsp; *MaxInitialIteration*:30<br />
<img src="results/shapecontex_train.png" width=210 />
<img src="results/shapecontext_valid.png" width=210 />
<img src="results/shapecontext_valid_2.png" width=210 />
<img src="results/shapecontext_valid_3.png" width=210 />
<img src="results/shapecontext_valid_4.png" width=210 />
<img src="results/shapecontex_valid_5.png" width=210 />
<img src="results/shapecontext_valid_6.png" width=210 />
<img src="results/shapecontext_valid_7.png" width=210 />
**Network Structure**:same with above
*Training*:<br />

||Zeros        | CROSS         |CONTEXT | PureContext
|------------ |------------ | ------------- | ------------- | -------------
**1**|0.9868 | 0.9910|0.9915|**->0.991**
**2**|0.9867 | 0.9906|0.9910  |**->0.991**

*The testing*:<br />

||Zeros       | CROSS         |CONTEXT  | PureContext
|------------ |------------ | ------------- | ------------- | -------------
**1**|0.0110 | 0.8364|0.8822|**->0.802**
**2**|0.0015 | 0.9048| 0.8983|**->0.831**

Summary:<br />
(from folds 2, it indicats test acc could converge to **0** some times when training with zeros)
<img src="results/realzerocontext1_summary.png" width=1024 />

Zeros Images-fold1&fold2:<br />
<img src="results/realzeroscontext1_zeros1.png" width=430 />
<img src="results/realzeroscontext1_zeros2.png" width=430 />

Zeros Cross Images-fold1&fold2:<br />
<img src="results/realzeroscontext1_all1.png" width=430 />
<img src="results/realzeroscontex1_all2.png" width=430 />

Context Images-fold1&fold2:<br />
<img src="results/realzeroscontext1_valid1.png" width=430 />
<img src="results/realzeroscontext1_valid2.png" width=430 />

### zeros Cross Context 1 iteration 2 (without training)

**Context Parameter**:<br />
*model weight*:0.3  &nbsp;*CurvatureWeighting*:0.2  &nbsp;*MaxIteration*:30 &nbsp; *MaxInitialIteration*:30<br />
same with above<br />
**Network Structure**:same with above
*The testing*:<br />
[0.8799 0.9217]<br />

| |iteration 2        |zerocrossContext
|------------ | -------------| -------------
**1**|0.8799  |**->0.8822**
**2**|0.9217  |**->0.8983**


Summary:<br />
<img src="results/Train1image_zerocrossiteration_summary.png" width=1024 />

Context Images-fold1&fold2:<br />
<img src="results/Train1imageiteration1_zeroscross1_valid1.png" width=430 />
<img src="results/train1imageiteration_zeroscross1_valid2.png" width=430 />
### zeros Cross Context 1 iteration 3 (without training)

**Context Parameter**:<br />
*model weight*:0.3  &nbsp;*CurvatureWeighting*:0.2  &nbsp;*MaxIteration*:30 &nbsp; *MaxInitialIteration*:30<br />
same with above<br />
**Network Structure**:same with above
*The testing*:<br />
[0.8874 0.9248]<br />

| |iteration 3      |iteration 2    |zerocrossContext
|------------ | -------------|-------------| -------------
**1**|0.8874  |0.8799 |**->0.8822**
**2**|0.9248  |0.9217 |**->0.8983**

Summary:<br />
<img src="results/train1image_zeroscrossiteration2_summary.png" width=1024 />

Context Images-fold1&fold2:<br />
<img src="results/train1image_zeroscrossiteration2_valid1.png" width=430 />
<img src="results/train1image_zeroscrossiteration2_valid2.png" width=430 />

### zeros Cross Context 1 iteration 4 (without training)

**Context Parameter**:<br />
*model weight*:0.3  &nbsp;*CurvatureWeighting*:0.2  &nbsp;*MaxIteration*:30 &nbsp; *MaxInitialIteration*:30<br />
same with above<br />
**Network Structure**:same with above
*The testing*:<br />
[0.8902 0.9259]<br />

| |iteration 4      |iteration 3    |iteration 2    |zerocrossContext
|------------ | -------------|-------------|-------------| -------------
**1**|0.8902  |0.8874 |0.8799 |**->0.8822**
**2**|0.9259  |0.9248 |0.9217 |**->0.8983**

Summary:<br />
<img src="results/train1image_zerosacross1iteration3_summary.png" width=1024 />

Context Images-fold1&fold2:<br />
<img src="results/train1image_zeroscrossiteration3_valid1.png" width=430 />
<img src="results/train1image_zeroscrossiteration3_valid2.png" width=430 />

### zeros Cross Context 1 iteration 5 (without training)

**Context Parameter**:<br />
*model weight*:0.3  &nbsp;*CurvatureWeighting*:0.2  &nbsp;*MaxIteration*:30 &nbsp; *MaxInitialIteration*:30<br />
same with above<br />
**Network Structure**:same with above
*The testing*:<br />
[0.8900 0.9267]<br />

||iteration 5  |iteration 4      |iteration 3    |iteration 2    |zerocrossContext
|------------ | -------------| -------------|-------------|-------------| -------------
**1**|0.8900 |0.8902  |0.8874 |0.8799 |**->0.8822**
**2**|0.9267 |0.9259  |0.9248 |0.9217 |**->0.8983**

### zeros Cross Context 1 iteration 6 (without training)

**Context Parameter**:<br />
*model weight*:0.3  &nbsp;*CurvatureWeighting*:0.2  &nbsp;*MaxIteration*:30 &nbsp; *MaxInitialIteration*:30<br />
same with above<br />
**Network Structure**:same with above
*The testing*:<br />
[0.8912 0.9273]<br />

||iteration 6 |iteration 5  |iteration 4      |iteration 3    |iteration 2    |zerocrossContext
|------------ |------------ | -------------| -------------|-------------|-------------| -------------
**1**|0.8912 |0.8900 |0.8902  |0.8874 |0.8799 |**->0.8822**
**2**|0.9273 |0.9267 |0.9259  |0.9248 |0.9217 |**->0.8983**

Context Images-fold1&fold2:<br />
<img src="results/train1image_zerocrossiteration6_valid1.png" width=430 />
<img src="results/train1image_zeroscrossiteration6_valid2.png" width=430 />

### zeros Cross Context 1 iteration 7 (without training)

**Context Parameter**:<br />
*model weight*:0.3  &nbsp;*CurvatureWeighting*:0.2  &nbsp;*MaxIteration*:30 &nbsp; *MaxInitialIteration*:30<br />
same with above<br />
**Network Structure**:same with above
*The testing*:<br />
[0.8921 0.9273]<br />

||iteration 7|iteration 6 |iteration 5  |iteration 4      |iteration 3    |iteration 2    |zerocrossContext
|------------ |------------ |------------ | -------------| -------------|-------------|-------------| -------------
**1**|0.8921 |0.8912 |0.8900 |0.8902  |0.8874 |0.8799 |**->0.8822**
**2**|0.9274 |0.9273 |0.9267 |0.9259  |0.9248 |0.9217 |**->0.8983**

Context Images-fold1&fold2:<br />
<img src="results/train1image_zerocrossiteration7_valid1.png" width=430 />
<img src="results/train1image_zeroscrossiteration7_valid2.png" width=430 />

### zeros Cross Context 1 iteration 8 (without training)

**Context Parameter**:<br />
*model weight*:0.3  &nbsp;*CurvatureWeighting*:0.2  &nbsp;*MaxIteration*:30 &nbsp; *MaxInitialIteration*:30<br />
same with above<br />
**Network Structure**:same with above
*The testing*:<br />
[0.8930 0.9275]<br />

||iteration 8|iteration 7|iteration 6 |iteration 5  |iteration 4  |iteration 3   |iteration 2    |zerocrossContext
|------------ |------------ |------------ |------------ | -------------| -------------|-------------|-------------| -------------
**1**|0.8930 |0.8921 |0.8912 |0.8900 |0.8902  |0.8874 |0.8799 |**->0.8822**
**2**|0.9275 |0.9274 |0.9273 |0.9267 |0.9259  |0.9248 |0.9217 |**->0.8983**

Context Images-fold1&fold2:<br />
<img src="results/train1image_zeroscrossiteration8_valid1.png" width=430 />
<img src="results/train1image_zeroscrossiteration8_valid2.png" width=430 />


### Random Cross Context 2
**Context Parameter**:<br />
*model weight*:0.28  &nbsp;*CurvatureWeighting*:0.1  &nbsp;*MaxIteration*:32 &nbsp; *MaxInitialIteration*:20<br />
First is train image<br />
<img src="results/shapecontext_valid2_train.png" width=280 />
<img src="results/shapecontext_valid2_1.png" width=280 />
<img src="results/shapecontex_valid2_2.png" width=280 />
<img src="results/shapecontext_valid2_3.png" width=280 />
<img src="results/shapecontext_valid2_4.png" width=280 />
<img src="results/shapecontext_valid2_5.png" width=280 />

*Training*:<br />

||Random       | CROSS         |CONTEXT | PureContext
|------------ |------------ | ------------- | -------------| -------------
**1**|0.9878 | 0.9909|0.9914|**->0.991**
**2**|0.9881 | 0.9907|0.9910|**->0.991**

*The testing*:<br />

||Random        | CROSS         |CONTEXT | PureContext
|------------ |------------ | ------------- | -------------| -------------
**1**|0.4432 | 0.7747|0.7662|**->0.802**
**2**|0.5603 | 0.7777|0.7775|**->0.831**

Summary:
<img src="results/zeroscross2_summary.png" width=1024 />
Random Images-fold1&fold2:<br />
<img src="results/contextimg2_zeros1.png" width=430 />
<img src="results/contextimg2_zeros2.png" width=430 />

Random Cross Images-fold1&fold2:<br />
<img src="results/contextimg2_all1.png" width=430 />
<img src="results/contextimgs2_all2.png" width=430 />

Context Images-fold1&fold2:<br />
<img src="results/contextimg2_valid1.png" width=430 />
<img src="results/contextimg2_valid2.png" width=430 />
#### Diff (Random cross context & pure)
* Pure unet outcome (without context )with groud truth(Pred - Ground Truth)<br />
"black" means outside part of ground truth 
<img src="results/diff_purewithgroundtruth.png" width=1024 />


* Random context outcome (final Random cross outcome)with ground truth(Pred - Ground Truth)
<img src="results/diff_zeroscontextandgroundtruth.png" width=1024 />

* Pure unet outcome with Random context(Pure - Context)
<img src="results/diff_zerosandpure.png" width=1024 />


### Random Cross Context 3
**Context Parameter**:<br />
*model weight*:0.29  &nbsp;*CurvatureWeighting*:0.15  &nbsp;*MaxIteration*:30 &nbsp; *MaxInitialIteration*:28<br />
First is train image<br />
<img src="results/shapecontext3_train.png" width=210 />
<img src="results/shapecontext3_valid1.png" width=210 />
<img src="results/shapecontext3_valid2.png" width=210 />
<img src="results/shapecontext3_valid3.png" width=210 />
<img src="results/shapecontext3_valid4.png" width=210 />
<img src="results/shapecontext3_valid5.png" width=210 />
<img src="results/shapecontext3_valid6.png" width=210 />
<img src="results/context3_valid7.png" width=210 />

*Training*:<br />

||Random        | CROSS         |CONTEXT | PureContext
|------------ |------------ | ------------- | -------------| -------------
**1**|0.9899 | 0.9914| -|**0.991**
**2**|0.9896 | 0.9910| -|**0.991**

*The testing*:<br />

||Random        | CROSS         |CONTEXT  | PureContext
|------------ |------------ | ------------- | -------------| -------------
**1**|0.2639 | 0.8008| -|**0.802**
**2**|0.0063 | 0.8005| -|**0.831**

Summary:
<img src="results/Train1image_zerocross3_summary.png" width=1024 />

Random Images-fold1&fold2:<br />
<img src="results/contextimage3_zeros1.png" width=430 />
<img src="results/contextimage3_zeros2.png" width=430 />

Random Cross Images-fold1&fold2:<br />
<img src="results/contextimage3_all1.png" width=430 />
<img src="results/contextimage3_all2.png" width=430 />

### Zeros Cross Context 3
**Context Parameter**:<br />
*model weight*:0.29  &nbsp;*CurvatureWeighting*:0.15  &nbsp;*MaxIteration*:30 &nbsp; *MaxInitialIteration*:28<br />
First is train image<br />
same with Random Cross Context<br />
<img src="results/shapecontext3_train.png" width=210 />
<img src="results/shapecontext3_valid1.png" width=210 />
<img src="results/shapecontext3_valid2.png" width=210 />
<img src="results/shapecontext3_valid3.png" width=210 />
<img src="results/shapecontext3_valid4.png" width=210 />
<img src="results/shapecontext3_valid5.png" width=210 />
<img src="results/shapecontext3_valid6.png" width=210 />
<img src="results/context3_valid7.png" width=210 />
*Training*:<br />

||Zeros        | CROSS         |CONTEXT  | PureContext
|------------ |------------ | ------------- | -------------| -------------
**1**|0.9900 | 0.9916| -|**0.991**
**2**|0.9889 | 0.9912| -|**0.991**

*The testing*:<br />

||Zeros        | CROSS         |CONTEXT  | PureContext
|------------ |------------ | ------------- | -------------| -------------
**1**|0.0003 | 0.8529| -|**0.802**
**2**|0.0008 | 0.8788| -|**0.831**

Summary:
<img src="results/realzerocross3_summary.png" width=1024 />

Zeros Images-fold1&fold2:<br />
<img src="results/realzeroscross3_zeros1.png" width=430 />
<img src="results/realzeroscross3_zeros2.png" width=430 />

Zeros Cross Images-fold1&fold2:<br />
<img src="results/realzeroscross3_all1.png" width=430 />
<img src="results/realzeroscross3_all2.png" width=430 />

#### Diff (zeros cross context & pure)
* Pure unet outcome (without context )with groud truth(Pred - Ground Truth)<br />
"black" means outside part of ground truth 
<img src="results/diff_pure_TG.png" width=1024 />


* Random context outcome (final Random cross outcome)with ground truth(Pred - Ground Truth)
<img src="results/diff_zeroscontext_GT.png" width=1024 />

* Pure unet outcome with Random context(Pure - Context)
<img src="results/contextandpure.png" width=1024 />

##  Training 20-folds

### Pure training
The training dice accuracy is around [0.9902 0.9916 0.9913] <br />
The testing dice accuracy is around [0.9543 0.9443 0.9067] <br />
Summary:<br />
<img src="results/20folds_puretrain_summary.png" width=1024 />
**Conlucsion: result could varies a bit from training**<br />
Test Images:<br />
<img src="results/20folds_valid1.png" width=1024 />

### zeros Cross Context 
**Context Parameter**:<br />
*model weight*:0.28  &nbsp;*CurvatureWeighting*:0.2  &nbsp;*MaxIteration*:35 &nbsp; *MaxInitialIteration*:30<br />

**Network Structure**:didn't capture
*Training*:<br />

||Zeros        | CROSS         |CONTEXT | PureContext
|------------ |------------ | ------------- | ------------- | -------------
**1**|0.9909 | 0.9908|0.9918|**->0.9902**
**2**|0.9905| 0.9915|-  |**->0.9916**
**3**|- | -|- |**->0.9916**

*The testing*:<br />

||Zeros        | CROSS         |CONTEXT  | PureContext
|------------ |------------ | ------------- | ------------- | -------------
**1**|1e^-8 | 0.9619|0.9620|**->0.9543**
**2**|0.1691| 0.9612|-  |**->0.9443**
**3**|- | -|- |**->0.9067**

Summary:<br />
<img src="results/20folds_zerocross1_summary.png" width=1024 />

Zeros Images-fold1:<br />
<img src="results/20folds_zeroscross1_zeros1.png" width=1024 />

Zeros Cross Images-fold1:<br />
<img src="results/20folds_zeroscross1_all1.png" width=1024 />

Context Images-fold1:<br />
<img src="results/20folds_zerocross_valid1.png" width=1024 />

##  Training 5-folds

### Pure training(without data augmentation)
The training dice accuracy is around [0.9915 0.9911 0.9924] <br />
The testing dice accuracy is around [0.9667 0.9702 0.9703] <br />
Summary:<br />
<img src="results/5folds_pureunet_summary.png.png" width=1024 />
Test Images:<br />
folds 1:<br />
<img src="results/5folds_pureunet_valid.png" width=1024 />
folds 2:<br />
<img src="results/5folds_pureunet_valid2.png" width=1024 />
folds 3:<br />
<img src="results/5folds_pureunet_valid3.png" width=1024 />

### Pure training(data augmentation)
The training dice accuracy is around [0.9918 0.9920 0.9920] <br />
The testing dice accuracy is around [0.9722 0.9724 0.9718] <br />
Summary:<br />
<img src="results/5folds_pureunetaugmentation_summary.png" width=1024 />
Test Images:<br />
folds 1:<br />
<img src="results/5folds_pureunetaugmentation_valid1.png" width=1024 />
folds 2:<br />
<img src="results/5folds_pureunetaugmenation_valid2.png" width=1024 />
folds 3:<br />
<img src="results/unet_pureunetaugmentation_valid3.png" width=1024 />

### zeros Cross Context 
**Context Parameter**:<br />
*model weight*:0.28  &nbsp;*CurvatureWeighting*:0.2  &nbsp;*MaxIteration*:37 &nbsp; *MaxInitialIteration*:30<br />

**Network Structure**:didn't capture
*Training*:<br />

||Zeros        | CROSS         |CONTEXT | PureContext
|------------ |------------ | ------------- | ------------- | -------------
**1**|0.9895 | 0.9903|0.9916|**->0.9915**
**2**|0.9905| 0.9923|0.9707 |**->0.9911**
**3**|- | -|- |**->0.9924**

*The testing*:<br />

||Zeros        | CROSS         |CONTEXT  | PureContext
|------------ |------------ | ------------- | ------------- | -------------
**1**|9e^-5 | 0.9720|0.9732|**->0.9667**
**2**|1e^-6| 0.9718|0.9717|**->0.9702**
**3**|- | -|- |**->0.9703**

Summary:<br />
<img src="results/5folds_zeroscross1_summary.png" width=1024 />

Zeros Images-fold1:<br />
<img src="results/5fold_zeroscross1_zeros1.png" width=1024 />

Zeros Cross Images-fold1:<br />
<img src="results/5folds_zerocross1_all1.png" width=1024 />

Context Images-fold1:<br />
<img src="results/5folds_zeroscross1_valid1.png" width=1024 />



## EXTENSION

Unet-iner:
<img src="results/runet_iner.png" width=1024 />

Self-cycle three times:<br />
20 folds Training acc :0.97-0.99<br />
20 folds Testing acc : 0.01-0.70<br />
**Unstable**<br />
<img src="results/RUNET.png" width=1024 />


Self-cycle three times:<br />
20 flods Training acc :0.97-0.99<br />
20 folds Testing acc : 0.40-0.90<br />
**Unstable(better than 0)**<br />
<img src="results/RUNET_1.png" width=1024 />

20 folds Training 0.97-0.99<br />
20 folds Testing  ----0.85 (min 0.69 max 0.9)<br />
<img src="results/runet_2.png" width=1024 />


### To be tried 
* **Do recurrent among context unet**

<img src="results/MSfcn.png" width=1024 />

**combined loss from different layers(used in MSFCN)**
<img src="results/combined_loss.png" width=512 /><br />
Ref: [Object Skeleton Extraction in Natural Images by Fusing Scale-associated Deep
Side Outputs
Supplementary Material](http://openaccess.thecvf.com/content_cvpr_2016/supplemental/Shen_Object_Skeleton_Extraction_2016_CVPR_supplemental.pdf)
**chenging context model structure**<br />
* structure1
<img src="results/unet_cat.png" width=1024 />

* structure2
<img src="results/unet_catloss.png" width=1024 />

* structure3
<img src="results/model_catloss_2.png" width=1024 />

* structure4
  *  *iner*<img src="results/runet_iner_improve.png" width=1024 />
  *  *Rnet_improve*<img src="results/Runet_improve.png" width=1024 />
  
* strucute5
 * **improve MSFCN to be NET-MSFCN**
 

 









































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


