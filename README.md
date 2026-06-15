# CEAM-TP-PROJECT
--
Centre for Autonomous Mobility(CEAM)-Task phase mini project | Shape Classification CNN |  Exploring overfitting, dropout, batch normalization and learning rate effects for CV/AI pipeline understanding.
--
## WHAT I BUILT?
   -I did a simple 3-shape classifier using Conventional neural networks(CNN)
   
   -It had 3 classes:circle,rectangle and triangle
   
   -It had 75 photos taken by me of real day-to day objects

DATASET
--
 -I took photos of real objects like coins, plates, hangers, set square,etc.... and varied angles, lighting, distance
 
 -This way I took each 25 pics for circle, 25 pics for  triangle, 25 pics for rectangle


TRAINING THE CNN
--
-I imported all the libraries needed from 
PyTorch for building the model, 
torchvision for loading images, 
matplotlib for plotting. 

-I also defined transforms to resize every image to 64x64, convert to numbers, and normalize values between -1 and 1.

-I used ImageFolder to automatically load all images and assign labels based on folder names.

-Then I split the dataset 80% for training and 20% for validation.

-I also created DataLoaders to feed images in batches of 16 during training.

-I built a CNN with 2 convolutional layers and 2 fully connected layers. Final layer outputs 3 numbers — one per class.

-I wrote a function that trains the model for a given number of epochs. It uses CrossEntropyLoss to measure how wrong predictions are. Adam optimizer updates weights after each batch. Backpropagation calculates how much each weight contributed to the error. Validation phase checks accuracy on unseen images after every epoch.

-I wrote a function to plot train vs val loss and train vs val accuracy after each experiment. 


EXPERIMENTS
--
-Experiment 1 - Baseline
 -I trained the model with default settings. Learning rate 0.001, batch size 16, no dropout, no batch norm. 
 
 -This was my starting point to compare everything else against. 
 
 -Train accuracy reached 98% but val accuracy stayed around 20-40%. This showed clear overfitting.

-Experiment 2 - Dropout
 -I added Dropout(0.5) after the first fully connected layer. This randomly switches off 50% of neurons during training so the model can't memorize. 
 
 -Train accuracy was slower to increase compared to baseline. 
 
 -But val accuracy was still low because my dataset was too small to fully fix overfitting.

-Experiment 3 - High Learning Rate (Failed)
 -I changed learning rate from 0.001 to 0.1. 
 
 -The loss exploded to 1600 in the very first epoch then crashed down. 
 
 -The model was taking steps too large and kept overshooting the optimal weights. Training never stabilized. 
 
 -This is my failed experiment — too high a learning rate makes training completely unstable.

-Experiment 4 - Small Batch Size
 -I changed batch size from 16 to 4.
 
 -This means the model updated weights after seeing only 4 images at a time instead of 16.
 
 -The val loss curve was much more jagged and noisy compared to baseline.
 
 -Small batches give noisier gradient updates which makes training less stable.

-Experiment 5 - Batch Normalization
 -I added BatchNorm2d after each conv layer. This normalizes the output of each layer so values don't get too big or small.
 
 -Training loss came down faster and more smoothly in the early epochs compared to baseline.
 
 -But still overfit because dataset is too small.


OBSERVATIONS
--
-All experiments showed overfitting

-High LR caused loss to explode to 1600

-Small batch made loss curve more noisy

-Batch norm made training smoother early on


WHAT I LEARNED
--
-*More training accuracy doesn't mean better model as explained in onlineclass....*

-*Dataset size matters a lot*

-*Small changes in hyperparameters change training behavior a lot*
