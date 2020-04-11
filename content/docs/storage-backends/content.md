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

### WebDAV

</p>
