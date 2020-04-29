# THIS REPOSITORY CONTAINS EXAMPLES FOR WORKING WITH TFSERVING, TFHUB, TENSORBOARD & FEDRATED LEARNING.
**For basics of FEDRATED LEARNING**
https://github.com/lmoroney/dlaicourse/blob/master/TensorFlow%20Deployment/Course%204%20-%20TensorFlow%20Serving/Week%204/Examples/Custom_Federated_Algorithms%2C_Part_1_Introduction_to_the_Federated_Core.ipynb

# Basics of TFServing

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

# Basics of TFHub

# STEP 1: IMPORT TENSORFLOW HUB AS HUB

# STEP 2: GET DATASET
Either custom or using tfds i.e tensorflow datasets

# STEP 3: TRAIN , VALIDATION AND TEST SPLIT
* Load dataset using tfds.load() then split.
* Best way using split = tfds.SPLIT.TEST

# STEP 4: BATCH THE TEST DATA
dataset_tr = self.train_dataset.shuffle(self._buffer_size).batch(self._batch_size)

# STEP 5: SAVE AND TRAIN MODEL
tf.saved_model.save(self._model, self._export_path) and model.compile() + model.fit()

# STEP 6: CREATE A TARBALL
The export_model method saved our model in the TensorFlow SavedModel format in the ./saved_model directory. The SavedModel format saves our model and its weights in various files and directories. This makes it difficult to distribute our model. Therefore, it is convenient to create a single compressed file that contains all the files and folders of our model. To do this, we will use the tar archiving program to create a tarball (similar to a Zip file) that contains our SavedModel.

!tar -cz -f module.tar.gz -C ./saved_model .

# STEP 7: MODULE HANDLE
1. For TEXT EMBEDDINGS : "https://tfhub.dev/google/tf2-preview/gnews-swivel-20dim/1"

2. For Images: MODULE_HANDLE ="https://tfhub.dev/google/tf2-preview/{}/feature_vector/4".format(handle_base)

# STEP 8: FEATURE EXTRACTOR
feature_extractor = hub.KerasLayer(MODULE_HANDLE)   OR put this in tf.keras.Sequential().

# STEP 9: EVALUATE ON TEST DATA

**important link**

https://tfhub.dev/

https://www.tensorflow.org/tfx/guide/serving

https://tensorboard.dev/   for tensorboard















