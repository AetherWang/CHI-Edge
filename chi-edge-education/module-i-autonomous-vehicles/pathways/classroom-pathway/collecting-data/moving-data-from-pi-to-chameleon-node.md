---
description: >-
  The steps for the student in order to sync the data from the pi to the remote
  cloud instance.
---

# Moving Data from Pi to Chameleon Node

**Note:** If the teacher does not want the students to touch anything related to edge-cloud computing, then this step can be done by the TA.&#x20;

1. If you have a lot of data, it may be time-efficient to compress the data into a zip file before syncing it.

<pre><code><strong>cd ~/car/data
</strong><strong>zip -r data.zip ~/car/data
</strong></code></pre>

2. Then sync them from the pi to the Chameleon Node:

```
rsync -r ~/car/data/data.zip cc@<Chameleon_Node_Floating_IP_Address>:~/mycar/data
```

_Note: may need to add key before syncing_

```
ssh-add <file path/name of private key>
```

3. Wait for the rsync command to finish (could take a few minutes), then, on the Chameleon node, unzip the data:

```
unzip data.zip -d ~/mycar/data
```

_Note: if the files are not found, it could be due to a wrong saving location and this requires the individual to find their zip file by browsing with UNIX Commands._
