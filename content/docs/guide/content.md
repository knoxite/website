+++
fragment = "content"
weight = 100
title = "Guide"
subtitle = "knoxite's User Manual"

[sidebar]
  sticky = true
+++

<p>

### Repositories

### Volumes

### Snapshots

### Encryption
Choose between several encryption algorithms with the `-e, --encryption` flag
while storing your data.

```
$ knoxite store -e aes latest data/ -d "AES encrypted snapshot"
```

### Fault-Tolerance

### Compression
While storing data into snapshots you can choose to compress your data with
several algorithms.

To do so use the the `-c --compression` option:

```
$ knoxite store -c gzip latest data/ -d "Compressed snapshot"
```

### Automatic backups

### Restoring a backup

</p>
