+++
fragment = "content"
weight = 100
title = "Storage Backends"
#subtitle = ""

[sidebar]
  sticky = true
+++

<p>

### Local filesystem

### Amazon S3

### Backblaze

### Dropbox

### FTP

### Google Drive

### Mega

To store data on mega you need a mega account and its e-mail address and password.
You can use the knoxite URL scheme in order to interact with this backend.
Currently the e-mail address needs to be url encoded.


```
knoxite repo init -r mega://example%40knoxite.com:password@/desired/path
```

### SSH/SFTP

### WebDAV

</p>
