#####################################################################
##                                                                 ##
##                Food classification problem                      ##
##                                                                 ## 
#####################################################################

## Training phase ##
   --------------

We were asked to classify food images into 11 different categories. 
In order to do this, we used a pre-trained network called 'inception',
offered by 'tensorflow' framework. We seperated the data into 11 different
folders, each one containing a specific category of food, we then fed this 
data to the last layer of inception network using the following code inside 
a docker environement :

python tensorflow/examples/image_retraining/retrain.py \
--bottleneck_dir=/tf_files/bottlenecks \
--model_dir=/tf_files/inception \
--output_graph=/tf_files/retrained_graph.pb \
--output_labels=/tf_files/retrained_labels.txt \
--image_dir /tf_files/food_images

This code retrains the inception network (only last layer) using our data
and creates :

bottlenecks : the values of the last layer, just before the output layer.
a retrained graph : graph representing inception network re-trained to predict the category 
                    of new food (it's like the network adapted itself for our specific data).
labels : the labels names used (names of the folders containing each food category).

Our trained model has a train accuracy of 92%, a validation accuracy of 86% and a test accuracy of 87%.

## Prediction (classification) phase ##
   ---------------------------------

Now that we have our trained network in the retrained_graph file (this file has a big size), we can use it
to classify images from the net using the URL of that image.
To do so, we need to have all the previously mentioned files in one folder,
that is : 'retrained_graph.pb', 'retrained_labels.txt', 'label_image.py' and the folder 'Downloaded_images'.
Then we can test the classifier using the command line by giving a URL of an image as an input,
for example like this :

python ./label_image.py https://s-media-cache-ak0.pinimg.com/236x/63/52/49/6352495cb41c2307f96b43acda494079.jpg

When we hit enter, we will see a list of predictions showing probabilities of how likely that image
is a certain type of food. Something like this (for the example given above) :

rice (score = 0.98908)
dairy product (score = 0.00586)
fried food (score = 0.00196)
dessert (score = 0.00177)
vegetables fruit (score = 0.00090)
meat (score = 0.00021)
noodles pasta (score = 0.00007)
seafood (score = 0.00006)
soup (score = 0.00004)
bread (score = 0.00004)
egg (score = 0.00000)






















 


