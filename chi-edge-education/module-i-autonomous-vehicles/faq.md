---
description: Fixes for Common Issues and Advice on Where to Find Help
---

# FAQ

### Unable to find SD Card for Flashing

If the student is unable to find the SD card for flashing, it is likely that the partitioning of the SD card is causing the computer to be unable to find it. Use the following UNIX Commands to fix this:

```
diskutil list
sudo diskutil mount <location of resin-boot>
```

_Note: Replace <> with the **Identifier** associated with the resin-boot mount that you found with diskutil list_

### Length of Pushing Container

Although incredibly unlikely, if pushing the container takes too long or some personal computer issues arise, use the leased node to push the image to the car.

### Speed of the Car Decreasing as Battery Drains: Constant Speed Problems

This is an inevitable consequence of utilizing pwm and throttle for forward motion. As the battery drains, the relative throttle will be slower as a consequence of the maximum power being lower. The solution is to utilize an encoder, attach it to a car, and write some code/logic that forces the car to maintain a certain speed regardless of how many pwm pulses are required.

_Note: A flushed out step by step for this has not yet been made, but will be made soon._

### Car Instantly Dying When Driving

It has occurred previously that the car dies the moment that throttle is applied, although every car is different. This is a consequence of a battery that is not fully charged and/or the fact that the pwm is set too high. As such, in the myconfig.py file, by setting the forward throttle pwm to a lower value, this issue can be solved. An additional method is to just set the throttle lower when driving.&#x20;

### Broken Steering:

Likely the motor chassis is faulty and it needs to be replaced

### Wheel not Moving:&#x20;

An axel could have been lost, check the parts and whether new parts need to be ordered.&#x20;

In the meantime, the other axel within the same plane as the wheel that lost its axel can be removed to allow for rear/front wheel drive only. Make sure to increase pwm in the myconfig.py file for forward throttle.

### Cannot SSH to Chameleon

1. No route to host

If after running an ssh command to connect to either the pi or your training node you get an error message that says "no route to host", this is likely because you are trying to ssh to soon before the container has entirely started. To fix this, just wait a few minutes and try the command again.

2. Scary message

If, after trying to ssh to one of your devices, you get a warning message in all caps telling you it is unsafe to connect because the host has changed, you will need to run this command:

```
ssh-keygen -R <ip address>
```

3. Taking forever to connect

If, after running the ssh command to try and connect to one of your devices, the command takes forever to finish executing and eventually times out, this is most likely because you are using the wrong IP address. Make sure you are copying the IP address that is listed in the Network->Floating IPs page on Chameleon. Also, make sure you are using the right command with the right user. For connecting to a normal Chameleon instance, use

```
ssh cc@<ip address>
```

For connecting to the raspberry pi, use

```
ssh root@<ip address>
```

4. invalid key

If you are getting a message saying your key is invalid, it is likely that your public key is not properly stored in the authoried\_keys file in the container. On Chi@Edge you can use the built in console to your container/instance and run

```
nano ~/.ssh/authorized_keys
```

In order to ssh to your device, the public key you generated using ssh-keygen should be listed in this file. If it is not listed, run the following command in the terminal of your own computer

```
cat ~/.ssh/id_ed25519.pub
```

Then, copy the output into the authorized\_keys file you have open on Chameleon. Now, you should be able to ssh into your container from your own computer.

### Donkey Not Found

It is possible that when you log in to your training node again and try to run donkey commands, it will say that donkey is not found. That is because you have to run these commands in your virtual environment, which has likely not been started up again when you re-logged.&#x20;

```
source .venv/bin/activate
```

If all else fails, you can always re-run all of the code from the third step in [Configuring Chameleon Node for Training](pathways/regular-pathway/configuring-chameleon-node-for-training.md). Installing the dependencies should not take as long this time.

### Chameleon Cloud Problems

Contact the [Chameleon Help Desk](https://www.chameleoncloud.org/user/help/ticket/new/guest/) if any issues with utilizing the software arise.

### Donkeycar Problems

If there are issues or extensions beyond what has been included, you can contact the [Donkeycar Discord.](pathways/regular-pathway/syncing-data-from-pi-to-training-node.md)

####

