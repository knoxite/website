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

This is the storage backend for the [dropbox](https://www.dropbox.com) cloud
storage.

##### Usage

You'll just need to provide the OAuth2 access token without any username in
the knoxite URL scheme in order to interact with this backend:

```
knoxite repo init -r dropbox://generated_access_token@/desired/path
```

##### Receive an access token

Assuming you already have an account on dropbox you'll have to create an app for
the platform. This can be done [here](https://dropbox.com/developers/apps/). You
can either grant knoxite full access to all folders on dropbox or just access to
a single folder dedicated for it. Note that the name of your app has to be
unique.

![create app](/images/backends/dropbox_create_app.png)

After creating the app you'll land on its info page. Here you'll need to
generate the OAuth 2 access token for knoxite. This can be done with a single
click on the corresponding button.

![generate token](/images/backends/dropbox_generate_token.png)

This generated token can now be used in knoxites URL scheme. It's better to save
this token in a secure place as dropboxs interface will not redisplay it (but
you can always generate a new one for the app).

![generated token](/images/backends/dropbox_generated_token.png)

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

In order to store data to another computer with ssh, you can use the sftp 
backend. You have to authenticate via password, or via private key using
an `ssh-agent` (Make sure to check if `$SSH_AUTH_SOCK` is set). 
Also make sure that `~/.ssh/known_hosts` contains a valid host key.

```
knoxite repo init -r sftp://user:password@knoxitessh.com:/path/to/repo
```

### WebDAV (Next-/OwnCloud)

Although the WebDAV-Backend should be compatible with every WebDAV-Backend,
right now it is only tested with Next-/OwnCloud.

You have to replace the `http`/`https` in the baseurl with `webdav`/`webdavs`.
Authentication works via basic/digest auth.
Please also check out if the path you set already exists.

**Basic Example:**

```
knoxite repo init -r webdavs://user@password@webdavhost.com/path/to/repo
```

**Next-/OwnCloud-Example:**

```
knoxite repo init -r webdavs://user@password@knoxitecloud.com/remote.php/webdav/path/to/repo
```



</p>
