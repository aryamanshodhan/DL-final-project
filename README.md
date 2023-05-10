# DL-final-project

Surgical site segmentation is a crucial part of training autonomous robots designed to perform medical procedures. Here we present some supervised methods of performing robot tool image segmentation, and an unsupervised method of generating surgical images using a GAN which could be used for further training.

We used the [CholecSeg8k](https://www.kaggle.com/datasets/newslab/cholecseg8k) dataset consisting of images of cholecystectomy procedures with their corresponding masks. We trained three state of the art models - the UNet, and 2 models with a Resnet backbone: DeepLabV3 and FCN to segment the images  using Cross Entropy Loss and the Adam Optimizer. We chose the Dice Score metric to evaluate our models. 

For each model, we ran multiple experiemnts in this order to evalaute their performance on Segmentation. These experiements were as follows:

- Retraining all parameters of the model: Herein, we either defined the model ourselves(UNet) or imported the model from pytorch without any pre-traiend weight and trained the model to segment the dataset.
- Transfer Learning: Herein, we imported the model from pytorch, froze all but the last layer, and re-trained the paramters of the last layer to segment the dataset. We did so only for DeepLabV3 and FCN since we defined the UNet model ourselves and hence it did not make sense to implement transfer learning using UNet. 
- Recolorization:
    - We performed 3 experiments under recolorization:
    - First, we trained models based on UNet, DeepLabV3 and FCN on recolorization and then evalaued the performance of these models on segmentation.
    - In addition, we also trained a GAN to generate images that we included in our dataset. The first dataset consisted of 50% real images and 50% fake or generated images.
    - The second dataset consisted of 100% fake or generated images.
- Data Augmentation: We performed traditional augmentation on our training datatset such as Randon Horiozntal and Vertical Flipping to test the robustness of our models to such changes.
- Adverarial Augmentation: For DeepLabV3 and FCN, we also added guassian noise to the training dataset to mimic an adversarial attack and tested how well our models generalised to that. 

In addition, we implemeted a Wavelet Transformation to enhance our UNet model to preserve spatial and high frequency information in the image which can be found in a separate file. 

Lastly, we trained  a GAN architecture to generate surgical images using the Adam optimizer, and Binary Cross Entropy Loss. 

This repository consists of the following files:

- DLFinalProject_UNet_Final.ipynb: This notebook contains all experiments related to UNet with the corresponding Training and Validation Loss plots. 
- DLFinalProject_DeepLabV3_Final.ipynb: This notebook contains all experiments related to DeepLabV3 with the corresponding Training and Validation Loss plots.
- DLFinalProject_FCN_Final.ipynb: This notebook contains all experiments related to FCN with the corresponding Training and Validation Loss plots.
- DLFinalProject_WaveletUNet_Final.ipynb: This notebook contains all experiments related to the Wavelet Transformation added to the UNet architechture with the corresponding Training and Validation Loss plots.
- DLFinalProject_Image_Generation_GAN.ipynb: This notebook contains the code to generate surgical images that were further used to enhance the dataset. 
- DLFinalProject_Recolorization.ipynb: This notebook contains the code to train the recolorization models based on UNet, DeepLabV3, and FCN.
- DLFinalProject_Recolorization_with_GAN_images.ipynb: This notebook contains the code to train recolorization models based on the GAN generated images.
- DLFinalProject_Metrics_Final.ipynb: This notebook contains the code to evaluate the segmentation performance of trained models.




