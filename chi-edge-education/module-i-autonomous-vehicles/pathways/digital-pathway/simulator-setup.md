---
description: >-
  Donkeycar also has a simulated environment available if real-world resources
  are unavailable to you.
---

# Simulator Setup

This page is for those who wish to complete this project, but do not have access to a physical car and raspberry pi. Below, you will find the steps to set up the Donkeycar simulator on your own computer. After the simulator is set up and you are able to drive around the virtual environment and collect data, you can skip to [Collecting Data](../regular-pathway/collecting-data.md) to complete the rest of the project. From this point on, treat your own computer where you run the simulation as if it is the raspberry pi in the rest of the instructions. This means that if the instructions say to run a command on the Pi, run it on your own computer. You should still have access to a regular Chameleon instance if you want to train your model in a reasonable time. To reserve your Chameleon instance, go to [Reserving your Pi on Chi@Edge](../regular-pathway/adding-pi-and-leasing-chameleon-node/reserving-your-pi-on-chi-edge.md), click the link to the Trovi artifact, and only run the reserve\_baremetal script, not the one to reserve the Pi. Setting up the simulator is also needed for an extension of this project: reinforcement learning.

**Simulator Set-up and Configuration**

1. Create a directory in the root called projects

```
mkdir ~/projects
```

_Note: make sure you have python installed_

2. Inside of this directory, clone the donkeycar repository

```
cd ~/projects
git clone https://github.com/autorope/donkeycar.git
```

_Note: this should create a donkeycar directory inside of the projects directory_

3. Change to donkeycar directory and set it up

```
cd donkeycar
git checkout main
```

Installation for Linux and Windows

```
pip install -e [pc]
```

Installation for Mac

```
pip install -e .\[pc\]
```

4. Download and unzip the simulator for the host pc
   1. [https://github.com/tawnkramer/gym-donkeycar/releases](https://github.com/tawnkramer/gym-donkeycar/releases)
   2. Go to the latest release and click the zip file for your operating system
   3. Unzip the contents
   4. Remember the location and find the absolute file path of the executable file&#x20;

_Note: on Mac, it will download a zip, unzip it and inside of the file is a .app file, two-finger click it and click “Show Package Contents”_

5. Set aside the path which should look akin to: “/Users/kylezheng/Downloads/DonkeySimMac/donkey\_sim.app/Contents/MacOS/donkey\_sim”
6. Clone the donkeycar gym repo in projects and set it up

```
cd ~/projects
git clone https://github.com/tawnkramer/gym-donkeycar.git
cd gym-donkeycar
```

_Note: creates gym-donkeycar directory inside of the projects directory_

Installation for Windows and Linux:

```
pip install -e .[gym-donkeycar]
```

Installation for Mac:

```
pip install -e .\[gym-donkeycar\]
```

7. Creating donkey application

```
cd ~/projects
donkey createcar --path mycar
cd mycar
```

8. File configuration for Donkeycar gym and Simulator

```
nano myconfig.py
```

Use this keyboard shortcut: control + w. Type “gym” and press enter.

Find the area that reads:

```
DONKEY_GYM = False
DONKEY_SIM_PATH = “path to sim”
DONKEY_GYM_ENV_NAME = “donkey-generated-track-v0”
```

Uncomment all three lines by deleting the # at the beginning of the lines

Change the lines to read:

```
DONKEY_GYM = False
DONKEY_SIM_PATH = <path_to_executeable>
DONKEY_GYM_ENV_NAME = “donkey-generated-track-v0”
```

Inside of the <> is the absolute file path for the executable set aside in Step 5

\