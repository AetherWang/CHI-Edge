---
description: Utilizing the cloud for training instead of the local computer.
---

# Syncing Data from Local Computer to Training Node (Digital Version)

_Note: you will notice that this digital version is much simpler than when a physical car is involved._&#x20;

_All of the following steps are done on your local computer._&#x20;

**Syncing the Data:**

1. If you have a lot of data, it may be time-efficient to compress the data into a zip file before syncing it.&#x20;

<pre><code><strong>cd ~/mycar/data
</strong><strong>zip -r data.zip ~/mycar/data
</strong></code></pre>

_Note: \~/mycar/data is an example of where the di_

2. Then sync them from the pi to the Chameleon Node:

```
rsync -r ~/mycar/data/data.zip cc@<Chameleon_Node_Floating_IP_Address>:~/mycar/data
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
