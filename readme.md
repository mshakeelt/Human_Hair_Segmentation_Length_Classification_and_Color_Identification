This repository is containg the codes for hair segmentation, classification, and hair color detection based on Tensorflow 2.

I have included environment.yml file which contains all the dependices to run this project. Install anaconda and use the following command to create the enviornment from this yml file 
"conda env create -f environment.yml".

same data is present in the segmentation_dataset and classification_dataset with a slight difference. Segmentation dataset includes all the rgb images along with the catagorical masks. 
Please note that the segmentation masks are in the pixel range [0-2] as they are catagorical. Pixels with values 2 correspondes to hair pixels, 1 to face, and 0 to background. To visualize 
such image I would recommend using ImageJ utility. Open the ImageJ and drag and drop any segmentation mask into this and then from the toolbar->Image->Adjust->Brightness/Contrast->Set set 
the maximum to 2.
In classification datset images are in 3 folders along with some augmentations to balance out the dataset. 

Here is the whole workflow of the whole project.

1- Training a UNET to segment the image into Hair, Face and Background
2- Training an EffecientnetB0 on hair, face, background masks to classify the length of the hair
3- Using colorific to detect the hair color

-------------------------------------------------------------------------------------------------------------------------

Starting Point

main.py includes the code to load the input image from test_images, pretrained segmentation, and classification weights from trained_models, draw inference on the input image and visualize
the results. Comments are present in the file for understanding the flow.

To test the individuale models use their respective inference codes (segmentation_inference.py and classification_inference.py).

To futher train the models on new data. prepare the data in the given format.

Image size would be 224*224*3. masks for segmentation training will be grayscale catagorical masks. Conversion codes are present in the data_preparation.py file. And masks for classification
training will be of 224*224*3 (not grayscale) without any normalization (i.e in the range [0, 255]) as effecientnetb0 expect RGB images for classification.