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
knoxite repository first. You can then use the knoxite URL scheme in order to
interact with the backend.

#### URL Scheme
You can create a repository using the **azurefile** URL scheme:

```bash
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
The storage account name as a prefix of the URL is optional, so you can use
either one of the following formats:

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
**Storage account - blob, file, table, queue**. Then you can use the
`Storage Explorer` to create a new **File Share**.

{{<lbimg src="/images/backends/azure/azure_create_file_storage_focus.png" title="create file storage">}}

After that you can set **Name** and **Quota**. Always keep an eye on your qouta
because knoxite may fail to store files when the maximum is reached.

{{<lbimg src="/images/backends/azure/azure_create_file_storage_2_focus.png" title="set filestore name and quota">}}

The next step is to create the root folder for your knoxite repository.
Use the **New Folder** button to add a new folder in the created file share. You
can use the **Copy URL**-button to get the endpoint needed for the azurefile URL
scheme.

{{<lbimg src="/images/backends/azure/azure_create_folder_copy_url_focus.png" title="create folder and copy url">}}

The last missing parameters to fill into the URL scheme are the
**Storage account name** and one of the **Access keys** which you can easily
copy from Settings > Access keys.

{{<lbimg src="/images/backends/azure/azure_access_keys_focus.png" title="get credentials">}}

---

### Backblaze

In order to to use your B2 Cloud Storage you'll have to setup an application key
first. Then you can use the applications credentials in knoxites URL scheme.

#### URL Scheme

You can use the **backblaze** B2 Cloud Storage in knoxite's URL scheme like
this:

```bash
knoxite repo init -r backblaze://[keyID]:[applicationKey]@/[path]
```

#### Create a new Application

To gather the **KeyID** and **applicationKey** you'll have to login to your
account on [backblaze](https://www.backblaze.com) and go to the **App Keys**
section. There you can click on the **Add a New Application Key** Button.

{{<lbimg src="/images/backends/backblaze/backblaze_add_application_key_focus.png" title="add application key">}}

After that you'll just need to fill in the name for your new application.
Optionally you can only allow access to certain buckets.

{{<lbimg src="/images/backends/backblaze/backblaze_create_new_key_focus.png" title="create new key">}}

The generated **applicationKey** and **keyID** can now be used in knoxite's URL
scheme.

{{<lbimg src="/images/backends/backblaze/backblaze_key_created_focus.png" title="created key">}}

Note that the application key will only appear here once. Make sure to store it
in a secure place.

---

### Dropbox

This is the storage backend for the [Dropbox](https://www.dropbox.com) cloud
storage.

##### Usage

You'll need to provide the OAuth2 access-token without any username in the
knoxite URL scheme in order to interact with this backend:

```bash
knoxite repo init -r dropbox://[generated_access_token]@/[path]
```

##### Receive an access token

Assuming you already have an account on Dropbox you'll have to create an app for
the platform. This can be done [here](https://dropbox.com/developers/apps/). You
can either grant knoxite full access to all folders on Dropbox or access to
a single folder dedicated for it. Note that the name of your app has to be
unique.

{{<lbimg src="/images/backends/dropbox/dropbox_create_new_app_focus.png" title="create app">}}

After creating the app you'll land on its info page. Here you'll need to
generate the OAuth 2 access-token for knoxite. This can be done with a single
click on the corresponding button.

{{<lbimg src="/images/backends/dropbox/dropbox_generate_access_token_focus.png" title="generate token">}}

This generated token can now be used in knoxite's URL scheme. It's better to
save this token in a secure place as Dropbox's interface will not redisplay it
(but you can always generate a new one for the app).

{{<lbimg src="/images/backends/dropbox/dropbox_generated_access_token_focus.png" title="generated token">}}

---

### FTP

---

### Google Cloud Storage
This backend enables knoxite to store data in a Google Cloud Storage bucket.
If you are not familiar with Google Cloud Console, see the detailled guide below
in the **Setting up Google Cloud Storage** section.


#### URL Scheme
You can create a repository using the **googlecloudstorage** URL scheme:

```bash
knoxite repo init -r googlecloudstorage://[path_to_key.json]@/[bucket]/[path]/
```

{{% note %}}
**Note:**

Be aware that the **path to the key** needs to be **url-encoded**.
{{% /note %}}

##### JSON key
As already mentioned, Google Cloud expects credentials in form of a JSON key.
The path to the JSON file, probably stored on your local filesystem, either
needs to be provided via the URL scheme or the `GOOGLE_APPLICATION_CREDENTIALS`
environment variable.

Unlike the parameter in the URL scheme, the path in the environment variable
does **not** need to be url encoded.

When using the environment variable, the path can be left out in the URL scheme
as in the second example below.

##### Examples

```bash
knoxite repo init -r googlecloudstorage://%2Fhome%2Fknoxite%2Fknoxite-demo-733f1cccf67c.json@/knoxite-demo/backups/
knoxite repo init -r googlecloudstorage:///knoxite-demo/backups/
```

#### Setting up Google Cloud Storage
There are multiple steps necessary to set your environment up on Google Cloud
Console.

##### Start a project
In case of being new to Google Cloud Storage, you need to create a project
first. This project will be the container for the Google Cloud Storage you want
to use.

##### Create a bucket
To create a bucket you need to navigate to **Storage > Browser** and create the
bucket. The preferences chosen for this demo are just an example but might be a
fit for backups that you only access occasionally.
{{<lbimg src="/images/backends/googlecloud/focus/gcloud_create_bucket1_focus.png" title="create bucket part 1">}}
{{<lbimg src="/images/backends/googlecloud/focus/gcloud_create_bucket2_focus.png" title="create bucket part 2">}}

##### Create a folder for your repository within the bucket
After creating a bucket you need to add a folder, which will be used to store
the repository in.
{{<lbimg src="/images/backends/googlecloud/focus/gcloud_create_folder_focus.png" title="create folder in bucket">}}

##### Add a service account
In order to access the bucket through the knoxite backend you need a service
account.

Therefore you need to navigate to **IAM & Admin > Service Accounts** and create
a new service account.
{{<lbimg src="/images/backends/googlecloud/focus/gcloud_serviceaccount_create_focus.png" title="create service account">}}

##### Grant access
For the service account to be permitted to access the bucket, you need to grant
access to the project. For testing purposes we choose the Storage Admin role
here. For production use we recommend to set specific roles that fit your needs.
{{<lbimg src="/images/backends/googlecloud/focus/gcloud_serviceaccount_grantaccess_focus.png" title="create service account grant access">}}

##### Create and download the key
In the last step of creating the service account you need to create a key. You
will need this key to use the Knoxite Google Cloud Storage backend.
{{<lbimg src="/images/backends/googlecloud/focus/gcloud_serviceaccount_finish_createkey_focus.png" title="create service account create key">}}

There is only a one-time chance to download this key, so we recommend you to
store it at a safe place in your filesystem. (Of course you are able to create a
new one later)

With the downloaded key you are now ready to use the Google Cloud Storage
backend via the knoxite URL scheme.

{{<lbimg src="/images/backends/googlecloud/focus/gcloud_serviceaccount_createkey_focus.png" title="create service account download key">}}

---

### Google Drive

---

### Mega

To store data on mega you need a mega account and its e-mail address and
password.

#### URL Scheme
You can use the knoxite URL scheme in order to interact with this backend.

{{% note %}}
**Note:**

Be aware that the **e-mail address** needs to be **url-encoded**.
{{% /note %}}

```bash
knoxite repo init -r mega://[mail-address]:[password]@/[path]
```

##### Example

```bash
knoxite repo init -r mega://user%40example.com:password@/knoxite
```

---

### Nextcloud

In order to use knoxite with Nextcloud, you need to use the WebDAV backend.

It is recommended to use a app password with knoxite. To generate a app
password first, go to the settings page of your Nextcloud instance. Navigate to
the Security-Section. In "Devices & sessions" you can generate a app password.

{{<lbimg src="/images/backends/owncloud_nextcloud/nextcloud_apppassword_step1.png">}}

Save the application password to a save location, as it only can be shown once.

{{<lbimg src="/images/backends/owncloud_nextcloud/nextcloud_apppassword_step2.png">}}

If you want to save your knoxite repository to a directory, now is the time to
create the path.

Next, you have to get the WebDAV-URL of your Nextcloud instance and modify the
url a bit. Go to your file overview and click on the settings button in the
bottom left. A menu containing the WebDAV-URL should appear:

{{<lbimg src="/images/backends/owncloud_nextcloud/nextcloud_webdav_path.png">}}

Copy the WebDAV-URL and modify it by the following rules:

- replace the `http` / `https` protocol with `webdav` / `webdavs`
- add your username and your password to the path
- add the subdirectory to the path, if you want

The URL can now be used to initialize a repo:

```bash
knoxite repo init -r webdavs://[user]:[password]@example.com/remote.php/webdav/[path]
```

---

### ownCloud

See [Nextcloud](#nextcloud).

---

### SSH/SFTP

In order to store data on another computer with SSH, you can use the SFTP
backend. You have to authenticate via password, or via private key using
an `ssh-agent` (make sure to check if `$SSH_AUTH_SOCK` is set). Verify that
`~/.ssh/known_hosts` contains a valid host key.

```bash
knoxite repo init -r sftp://[user]:[password]@example.com/[path]
```

---

### WebDAV

Although the WebDAV-backend should be compatible with every WebDAV server, right
now it is only tested with Nextcloud and ownCloud.

You have to replace the `http` / `https` protocol in the URL with `webdav` /
`webdavs`. Authentication works via basic/digest auth. You have to create the
target folder for the repository in Dropbox.

```bash
knoxite repo init -r webdavs://[user]:[password]@example.com/[path]
```

</p>
