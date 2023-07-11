---
description: >-
  The final step in the process where the results of all your data collection
  and training can be evaluated.
---

# Running the Model in Simulator

**Running the model in the Simulator**

1. In your local \~/mycar directory, run the following command to load the model:

```
python manage.py drive --model <filepath_to_model>
```

_Note: like when you originally ran the simulator, a Unity interface application should also pop up._

2. Open the Web UI in a web browser by navigating to:

```
<ip_address_of_edge_device>:8887
```

3. Split screen the Web UI and simulator
4. Above the camera display of the Web UI, to the left, there is a drop-down that says User, click on it and pick either Full Auto or Auto Steer
   1. Full Auto: gives full control to the AI&#x20;
   2. Auto Steer: human controls the throttle but the AI controls the steering

**Tips for Running the Model**

1. Make sure you are running the model in the same environment you collected data in.
   1. This means more than just running it on the same track. The model will work best if it is also in the same lighting and its surroundings are the same.
