# Eye Gender Predicctor
Predict Gender from Eye Morphology Using CNN

## Introduction
Here, we have created a custom CNN architecture loosely based off of ResNet that is used in order to predict gender of an image subject using eye morphology. The architecture used consists of a Deep CNN architecture that is bolstered by the use of Data Augmentation and Skip Connections.

## Data
The data, present in `eye_gender_data.zip` consists of a Training set with labelled images and a test set with unlabelled images. The images are photos of eyes with an associated male or female label.

Here's some sample data:

![image](https://user-images.githubusercontent.com/87599801/177036607-cfe135e9-a0aa-4e4b-929a-cbce75e7b7e5.png)


## Architecture

Our architecture consists of the following :
1. **Data Augmentation Layer -** We start with a augmenting the data with random flips, rotations, zooms and crops. You can see our data augmentation layer in action in our ipynb file.
2. **Convolution -** We then have a basic CNN and ReLU layer
3. **Residual Blocks -** We then have 14 successive residual block layers that consist of BatchNorm, Dropout and CNN layers with the input being added back to the output. This is the key feature of Residual Blocks or Skip Connections and improves accuracy and prevents vanishing gradients in Deep NNs. Some residual bloakcs also consist of a downsampling layer to reduce dimensionality.
4. **Avg Pooling -** We pass it through an Average Pooling Layer to reduce dimensionality.
5. **Feed Forward Network -** After convolution and pooling, We finally pass our downsampled output through a Dense layer i.e a Normal Neural Net to finally output a prediction

We compile our model using binary cross-entropy as our loss function and Adam as our optimizer.

For a visual representation of our architecture, scroll to the bottom of this ReadMe.

## Implementing Our Code

First, open your Terminal and clone this repository
```
git clone https://github.com/ramsundaram101/Eye-Gender-Predicctor
```

#### Training

If you want to train your own model, run the `train.py` script. You can also go through our `.ipynb` file to comb through the code yourself and visualize the data
```
python train.py --zip_file eye_gender_data.zip --no_epochs 50 --image_size 100
```
Feel free to change the no of epochs and image size (although 100 is what gave us the best results). The zip_file parameter is the location of the file containing the dataset

#### Predictions
Now, to run our model on some fresh data
```
python predict.py --zip_file eye_gender_data.zip --model_path eye_cnn_model --image_size 100
```
Again, the zip file parameter leads to our testing data. The `model_path` parameter leads to our saved model. To use our pre-trained model use `eye_cnn_model` here. To use your trained model, use `my_trained_model` here. The `image_size` parameter should be the same as that which you trained the model with. To avoid any issues, we recommend sticking to 100.

## Full Architecture
As promised, here is our full architecture. Please be warned, it's quite a long image.

![model](https://user-images.githubusercontent.com/87599801/177036490-15847235-d837-41fe-87d5-2e2ca658cee8.png)

Than you for so much for reading. I'm quite surprised you scrolled all the way down here


