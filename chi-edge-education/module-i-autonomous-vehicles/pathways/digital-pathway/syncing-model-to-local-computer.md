---
description: >-
  After you have trained your model, you will need to use rsync again to get it
  onto the local computer.
---

# Syncing Model to Local Computer

**Syncing the Model to your Local Computer**

1. To move the model file from the Chameleon Node to the local computer, run the following command from your computer:

<pre><code><strong>rsync cc@&#x3C;Chameleon_Floating_Ip_Address>:~/mycar/models/&#x3C;model_name> ~/mycar/models
</strong></code></pre>

2. Be sure to also sync the myconfig.py file since this could affect how the pi interprets the model

```
rsync cc@<Chameleon_Floating_Ip_Address>:~/mycar/my_config.py ~/mycar/my_config.py
```



_**Note: \~/mycar/models/\<model\_name>: is a file path and if the naming of the directories are not within convention, it could lead to errors.**_&#x20;
