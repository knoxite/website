+++
fragment = "content"
weight = 100
title = "Storage Backends"
#subtitle = ""

[sidebar]
  sticky = true
+++

<p>

### Filesystem

---

### Amazon S3

---

### Azure File Storage

In order to store data on Azure you need to set up a file storage for your
knoxite repository first. Then we use the knoxite URL scheme in order to
interact with the backend.

#### URL Scheme
You can create a repository using the **azurefile** URL scheme:

```
knoxite repo init -r azurefile://[storage_account_name]:[access_key]@[endpoint]
```

On Azure you can find the storage account name and the access key at
`Storage Account` > `Access keys`.

{{% note %}}
**Note:** Be aware that the access key needs to be **url-encoded**. So the
slashes **(/)** and the equals signs **(=)** need to be replaced:

| CHARACTER&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | URL-ENCODING |
| --------------------------------------------------------------- | ------------ |
| /                                                               | %2F          |
| =                                                               | %3D          |
{{% /note %}}

##### Endpoint
The endpoint is the URL of the folder you want your repository stored in.
The storage account name as a prefix of the URL is optional, so you can use one
of the following formats:

`
storageaccountname.file.core.windows.net/file_share_name/root_folder
`
or
`
file.core.windows.net/file_share_name/root_folder
`

##### Example
```
azurefile://knoxitetest:DbxvVZMMzXWqEykTupObp9aD%2Fz7UH1TyO2NAeZpU1klkUut4SEtOCCEOfp42%2FQLXYKRgmDUUwjzi4XJTe1nB6w%3D%3D@knoxitetest.file.core.windows.net/knoxite/home-backups
```

#### Setting up your Azure File Storage
In order to use Azure File Storage you need to add a resource of the type
**Storage account - blob, file, table, queue**. Then we can use the
`Storage Explorer` to create a new **File Share**.

![create file storage](/images/backends/azure_create_file_storage_focus.png)

After that we can set **Name** and **Quota**. Always keep an eye on your qouta
because knoxite may fail to store files when the maximum is reached.

![set filestore name and quota](/images/backends/azure_create_file_storage_2_focus.png)

The next step is to create the root folder for your knoxite repository.
Use the **New Folder** button to add a new folder in the created file share. You
can use the **Copy URL**-button to get the endpoint needed for the azurefile URL
scheme.

![create folder and copy url](/images/backends/azure_create_folder_copy_url_focus.png)

The last missing parameters to fill into the URL scheme are the
**Storage account name** and one of the **Access keys** which you can easily
copy from Settings > Access keys.

![get credentials](/images/backends/azure_access_keys_focus.png)

---

### Backblaze

In order to to use your B2 Cloud Storage you'll have to setup an application key
first. Then you can use the applications credentials in knoxites URL scheme.

#### URL Scheme

You can use the **backblaze** B2 Cloud Storage in knoxite's URL scheme like
this:
```
knoxite repo init -r backblaze://[keyID]:[applicationKey]@/desired/path
```

#### Create a new Application

To gather the **KeyID** and **applicationKey** you'll have to login to your
account on [backblaze](https://www.backblaze.com) and go to the **App Keys**
section. There you can click on the **Add a New Application Key** Button.

![add application key](/images/backends/backblaze_add_application_key_focus.png)

After that you'll just need to fill in the name for your new application.
Optionally you can only allow access to certain buckets.

![create new key](/images/backends/backblaze_create_new_key_focus.png)

The generated **applicationKey** and **keyID** can now be used in knoxite's URL
scheme.

![created key](/images/backends/backblaze_key_created_focus.png)

Note that the application key will only appear here once. Make sure to store it in a
secure place.

---

### Dropbox

This is the storage backend for the [Dropbox](https://www.dropbox.com) cloud
storage.

##### Usage

You'll need to provide the OAuth2 access-token without any username in the
knoxite URL scheme in order to interact with this backend:

```
knoxite repo init -r dropbox://generated_access_token@/desired/path
```

##### Receive an access token

Assuming you already have an account on Dropbox you'll have to create an app for
the platform. This can be done [here](https://dropbox.com/developers/apps/). You
can either grant knoxite full access to all folders on Dropbox or access to
a single folder dedicated for it. Note that the name of your app has to be
unique.

![create app](/images/backends/dropbox_create_new_app_focus.png)

After creating the app you'll land on its info page. Here you'll need to
generate the OAuth 2 access-token for knoxite. This can be done with a single
click on the corresponding button.

![generate token](/images/backends/dropbox_generate_access_token_focus.png)

This generated token can now be used in knoxite's URL scheme. It's better to
save this token in a secure place as Dropbox's interface will not redisplay it
(but you can always generate a new one for the app).

![generated token](/images/backends/dropbox_generated_access_token_focus.png)

---

### FTP

---

### Google Drive

---

### Mega

To store data on mega you need a mega account and its e-mail address and
password. You can use the knoxite URL scheme in order to interact with this
backend. Currently the e-mail address needs to be url-encoded.


```
knoxite repo init -r mega://example%40knoxite.com:password@/desired/path
```

---

### SSH/SFTP

In order to store data on another computer with SSH, you can use the SFTP
backend. You have to authenticate via password, or via private key using
an `ssh-agent` (make sure to check if `$SSH_AUTH_SOCK` is set). Verify that
`~/.ssh/known_hosts` contains a valid host key.

```
knoxite repo init -r sftp://user:password@knoxitessh.com:/path/to/repo
```

---

### WebDAV (Nextcloud, ownCloud, ...)

Although the WebDAV-backend should be compatible with every WebDAV server, right
now it is only tested with Nextcloud and ownCloud.

You have to replace the `http` / `https` protocol in the URL with `webdav` /
`webdavs`. Authentication works via basic/digest auth. You have to create the
target folder for the repository in Dropbox.

##### Basic Example

```
knoxite repo init -r webdavs://user:password@webdavhost.com/path/to/repo
```

##### Nextcloud and ownCloud Example

```
knoxite repo init -r webdavs://user:password@knoxitecloud.com/remote.php/webdav/path/to/repo
```
</p>
