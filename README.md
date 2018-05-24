# Transfer-Learning-using-VGG16-in-Keras
Using VGG16 network trained on ImageNet for transfer learning and accuracy comparison

The same task has been undertaken using three different approaches in order to compare them.

**Task:** Image classification  
**Dataset:** Dogs vs Cats dataset from Kaggle.  
**Dataset size:** 1000 x 2 training images. 400 x 2 validation images.

### Data augmentation:
Keras provides *ImageDataGenerator* class for performing data augmentation. We will use this to augment the data via random transformations. Rotation, scaling, shearing, flipping, zooming are some possible ways.
![cat data augmentation](https://user-images.githubusercontent.com/20294710/40472806-7e39c4e6-5f08-11e8-857c-3952c2986718.jpg)


## First approach:
Training a small convnet from scratch.  
**Architecture:** A very small convnet with few layers and few filters per layer, alongside data augmentation and dropout. Dropout and augmentation help avoid overfitting.  
### Accuracy: ~80%

## Second approach:
Using the bottleneck features of a pre-trained network.  
I have used the VGG16 architecture which was pretrained on the ImageNet dataset.  
The strategy is to only instantiate the convolutional part of the model, everything up to the fully-connected layers. Then run the model on training and validation data, record the output (bottleneck features), then train a small FC model on top of those features.  
### Accuracy: ~90%

## Third Approach:
Fine-tuning the top layers of a a pre-trained network  
Fine-tuning is when you start with a trained network, then retrain it on a new dataset with very minor weight updates. This can be done in three steps:
- instantiate the convolutional base of VGG16 and load its weights
- add our previously defined fully-connected model on top, and load its weights
- freeze the layers of the VGG16 model up to the last convolutional block
### Accuracy: 93%+

## Notes:
The first and second approaches were run for 50 epochs each. The third was much more computationally intensive and hence was run only for one epoch and yet displayed a very high accuracy.
