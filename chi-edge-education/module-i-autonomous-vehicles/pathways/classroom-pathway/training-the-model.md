---
description: >-
  Once your data is transferred to your training node, you are now ready to use
  Tensorflow to train a self-driving model.
---

# Training the Model

**Training the Model on the Chameleon Node:**

1. By default, donkeycar uses the tflite\_linear model to train, but we want to use the normal linear model. To change this, go into myconfig.py and change DEFAULT\_MODEL\_TYPE to linear.

```
cd ~/mycar
nano myconfig.py
```

The line with DEFAULT\_MODEL\_TYPE  should look like this:

```
DEFAULT_MODEL_TYPE = 'linear'
```

2. Utilizing all of the gathered data, train a model

```
cd mycar
donkey train --tub ./data/[data subdirectory] --model ./models/<model_name>.h5
```

_Note: be sure to include the .h5 at the end of the model filename_

_**Optional Training Changes**_

1. It is possible to make edits to how the model trains through augmentations and transformations&#x20;

```
nano ~/mycar/myconfig.py
```

2. Some options to play around with include:

<pre><code>OPTIMIZER = 'adam'                #adam, sgd, rmsprop, etc.. None accepts default
<strong>...
</strong><strong>AUGMENTATIONS = ['BLUR']         # changes to image only applied in training to create
</strong>#                            # more variety in the data.
TRANSFORMATIONS = ['CROP']       # changes applied _before_ training augmentations,
#                            # such that augmentations are applied to the transformed image,
</code></pre>

3. You can search for words, like "OPTIMIZER", using ^W.
4. Note: It is very important that the myconfig.py files match between the cars and the Chameleon node, if one thing changes, the other must be changed as well. The following command can be used to sync the files just in case:

```
rsync cc@<training_ip_address>:~/mycar/myconfig.py ~/car/myconfig.py
```

