---
description: >-
  This page shows our results for evaluating the different Keras model types
  built into Donkeycar.
---

# Evaluation of Different Model Types

**Overview:**

In this extension, we evaluated the performance of each Keras model available to be used with our sample data. The Keras model types tested were Linear, Categorical, RNN, 3D, Memory, and Inferred. The time to train each model was recorded. After each model was trained, we synced the models to the pi and ran each of them using the drive command. We evaluated the results by recording the maximum distance each car could go along the track without leaving the road. Since some models worked well enough to where the car could stay on the road indefinitely, we also recorded the max speed the each model could run at without ever leaving the road.&#x20;

**Procedure:**

Here are the steps to follow to reproduce this experiment. This assumes you have already collected a large enough dataset to run a model proficiently.

1. Train each model type

Use the following command to train a model of a certain type on your training node. The time command at the front will keep track of the time it takes for training. Be sure to chance \<type> to the model type you want to train (i.e. linear, categorical, RNN, etc.) and also give the model an appropriate name in place of \<name>.

```
time donkey train --tub ./data --model ./models/<name>.h5 --type <type>
```

2. Sync the model back to the car

Just like in the procedure for the first part of this project, you will have to run the rsync command to move the model from the training node to the car. Run the following command on the car.

```
rsync cc@<ip address>:~/mycar/models/<name>.h5 ~/car/model
```

3. Run the model

Running the model using the drive command is similar to how it is used in the first part of this project. The only difference is that the model type should be specified. Run the following command on the car. Replace \<model\_type> with the type of model that you trained (i.e. linear, categorical, RNN, etc.).

```
python3 manage.py drive --model ~/car/models/<model_name> --type <model_type>
```

4. Switch to Full Auto in web browser

Just like in the first part of this project, you paste your car's ip address into a web browser to bring up the ui so you can drive your car. Ensure your car is in the correct position on your track, then select Full Auto from the dropdown menu or press "A" on your keyboard.

5. Evaluate Results

Observe the behavior of the car as it is running the model. Does it stay inside the lines? If not, how far does it get before going off of the track? The speed of the car is based off of the PWM value for forward throttle in myconfig.py. If you want to change this speed refer back to the last step in [Car Calibration](../../classroom-pathway/car-calibration.md) to find the value for FORWARD\_THROTTLE in myconfig.py. Choosing how to classify model effectiveness is up to you, but the metrics we chose were distance along track before leaving the road and max accurate speed. We discuss our results below.

**Results:**

Our first attempt at evaluating model effectiveness was to record how far the car made it along the track before failing. We defined "failing" as leaving the track entirely, which allows the car some breathing room for touching the edges of the track. The following table shows the best performance for each model using it's ideal speed. If a model was able to run 100% accurately at a slow enough speed, then "Doesn't Fail" was recorded.

| Model Type  | Distance Before Failure |
| ----------- | ----------------------- |
| Linear      | Doesn't Fail            |
| Categorical | Doesn't Fail            |
| RNN         | 2.5 Laps                |
| 3D          | Doesn't Fail            |
| Memory      | Doesn't Fail            |
| Inferred    | Doesn't Fail            |

As it can be seen, 5 out of 6 model types were able to run successfully at a low enough speed. The RNN model, even on the lowest possible speed, was only able to make it around the track 2.5 times before failing. The 5 successful models were able to drive accurately for the entire time they were run, but some could handle higher speeds than others. This led us to evaluate model performance in a different way.

_Note on the 5 "successful" models: the claim that each model "Doesn't Fail" only applies to the 4-5 minutes that they were run. During that span, the model drove completely accurately. It is possible that, if more time were given, the model could fail at some point, but since there is a limited battery supply anyway, we determined 4-5 minutes to be enough time to test._

Next, we found the maximum speed that each model could run at without leaving the track. We did this by changing the FORWARD\_THROTTLE PWM value in myconfig.py back and forth until the highest speed that could sustain accurate driving was found. Then, lap times were recorded at this speed. The average lap times for each model operating at maximum accurate speed are show in the graph below.

<figure><img src="../../../../../.gitbook/assets/Average Lap Times for each Model.png" alt=""><figcaption></figcaption></figure>

These lap times show which model was able to sustain accurate driving at the highest speed. Our results show that the Inferred model type is able to run at the fastest speed, followed by Linear, 3D, Categorical, and Memory. From these results, we can conclude that the Inferred model type is the better performing model since it was able to operate accurately at a higher speed than all other model types. When the car is driving at a higher speed, it has less reaction time to decide which was to turn. Since Inferred was able to accurately drive with a lower reaction time than all other models, it can be concluded that it is able to make the best decisions.

**Possible Improvements:**

1. Increase speed when evaluating Distance-Before-Failure

When testing models for how far they could make it along the track, the speed was likely set too low. This metric is only helpful if all models fail at some point so that the distance before failure can be compared. Since most models were able to drive the car along the track indefinitely, we were not able to make this comparison. In the future, we would run each model at a constant, higher speed.

2. Make speed not dependent on battery percentage

The speed of the car can be changed by altering the PWM value for FORWARD\_THROTTLE in myconfig.py. However, speed can still change based on how much battery the car has left. When the car is running on lower battery, it will drive slowing than if it had a full battery, even if the PWM value is held constant. This issue was encountered when evaluating the max accurate speed of the models. While lap times were being recorded, the battery was draining and, as a result, the car would move slower. Below are lap times recorded for the Memory model type.

| Trail Number | Lap Time (secs) |
| ------------ | --------------- |
| 1            | 17.76           |
| 2            | 16.3            |
| 3            | 16.58           |
| 4            | 17.05           |
| 5            | 16.7            |
| 6            | 17.46           |
| 7            | 18.1            |
| 8            | 18.8            |
| 9            | 18.31           |
| 10           | 18.78           |
| 11           | 18.87           |

The data above shows how the recorded lap times increase as trails increase. This is because the battery is draining and, since the PWM value was held constance, the car decreases in speed. A possible way of fixing this would be to add an odometer to the car which could keep track of real distance it is moving and use that instead of PWM.
