---
description: >-
  Before you can train a self-driving model, you must drive it to collect
  training data.
---

# Collecting Data

**Collecting Data with the Simulator:**

1. Run the Simulator from the mycar directory

```
python manage.py drive
```

In a moment, this will open a window with a car in simulated surroundings

_Note: You can not control the car from this window_

Open Google Chrome and type this url in:

```
http://localhost:8887
```

With Joystick mode on, our through a physical game controller, you can control the car, which should propagate from through both the WebUI and the Simulator Opened

_Note: Throttle can be changed from 100% to a lower number, preferably 10%_

2. Configuration&#x20;
   1. Go to the envs directory:
   2. Example file path:&#x20;

```
cd /Users/kylezheng/projects/gym-donkeycar/gym_donkeycar/envs
```

Inside of donkey\_env.py change steer\_limit to 0.5

Reinforcement learning can be found in donkey\_sim.py&#x20;

Other lower priority configurations can be changed from the same files

_Note: Do not attempt to use the simulator trained model in the real world! Remember the Simulator to Real Gap. Although there is a technique utilizing auto-encoders and Soft Actor Critic that allow for robust performance, documentation has not been included (yet)._

3. Split screen the Unity Game application and the WebUI&#x20;
4. To drive with the physical game controller, you will need to click on gamepad in the WebUI. The USB that came along with the controller in the Waveshare PiRacer Pro kit needs to be plugged into your computer that has the WebUI open. Depending on the pwm value you set for forward throttle, you may need to set the maximum throttle percentage to less than 100% in order to control the car.

**Data Collection Tips**

1. Trash folder to store practice data

When you begin driving, you may make some mistakes like going off of the track. We want to make sure that the data we use to train the model is good data without mistakes. The next page will explain how to clean up bad data. However, if you want to just drive around and not worry about filling up the data directory with bad data, you can create a new subdirectory within data.

```
cd ~/car/data
mkdir trash
```

Then you can edit the myconfig.py file to store newly collected data in this subdirectory.

```
cd ~/car
nano myconfig.py
```

Uncomment these top three lines and change the directory of DATA\_PATH

```
import os
# 
# #PATHS
CAR_PATH = PACKAGE_PATH = os.path.dirname(os.path.realpath(__file__))
DATA_PATH = os.path.join(CAR_PATH, 'data/trash')
```

2. Amount of data needed

When the data is collected and stored as records in the data directory or whatever path you are telling it to save the data. These records consist of .catalog files, images directory, and manifest files. Catalog files are where your steering and throttle values are recorded while driving. Each of these corresponds to an image in the images directory based on their id number. Catalog\_manifest files store information about each catalog file and the manifest.json file is where certain records are marked for deletion. The number of records you have can be discerned from the number of catalog files since each catalog file can only contain up to 1,000 records. In order to see any kind of behavior from your model, it is recommended that you collect 10,000 records. We found that in order to train a working model, almost 30,000 records are needed.
