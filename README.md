# Data-Pipelines-with-TensorFlow-Data-Services
# Starting with basics of TFServing

# STEP 1: GET IMPORTS AND CREATE A MODEL
It can use any dataset either custom made or from keras.datasets.NAME_OF_DATASET.

# STEP 2: TRAIN THE MODEL AND EVALUATE IT
define the optimizer, loss function, epochs etc and train the model.

# STEP 3: SAVE THE MODEL AND DEFINE THE EXPORT PATH
Here, we save the model with model.save and some 'os' operation. Finally define an EXPORT directory where saved model will be loacted to load it to TFServing using apt key.

# STEP 4: STARTING TFSERVING
Using the following piece of code

!echo "deb http://storage.googleapis.com/tensorflow-serving-apt stable tensorflow-model-server tensorflow-model-server-universal" | tee /etc/apt/sources.list.d/tensorflow-serving.list && \

curl https://storage.googleapis.com/tensorflow-serving-apt/tensorflow-serving.release.pub.gpg | apt-key add -

!apt update


# STEP 5: LOAD TRAINED MODEL TO TFSERVING 
After it loads we can start making inference requests using REST. There are some important parameters:

rest_api_port: The port that you'll use for REST requests.
model_name: You'll use this in the URL of REST requests. It can be anything.
model_base_path: This is the path to the directory where you've saved your model. 

# STEP 6: MAKE REQUEST TO MODEL IN TFSERVING
Create the JSON object for a batch of three inference requests, and see how well our model recognizes things using following code.

import json

data = json.dumps({"signature_name": "serving_default", "instances": test_images[0:3].tolist()})

# STEP 7: REST REQUEST FOR INFERENCE
Get inference using http request that loads json response.










