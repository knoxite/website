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
A repository contains all the data for knoxite to work with. You can create
repositories at different locations and combine them into one. Click
[here](/docs/storage-backends/) for information about accessing different
storage backends within the knoxite repo URL.
The data you store in these repositories will be encrypted with a password which
you'll have to provide at the repositories initialisation process.
**Be warned:** if you lose this password, you wont be able to access any of your
data.

#### Initializing a repository
To initialize a repository use the `init` command:
```
$ knoxite repo -r /tmp/knoxite init
Enter password:
Created new repository at /tmp/knoxite
```

The `-r, --repo` flag specifies the repositories location.
Knoxite will ask you for a password and proceeds to initialize a repository at
the given location (in this case */tmp/knoxite*).

You can provide default settings for the repositories location and password
with environment variables:
```
$ export KNOXITE_REPOSITORY=path/to/repo
$ export KNOXITE_PASSWORD=password
```

**IMPORTANT NOTE:** Providing your password with the `-p, --password` flag or
via the environment variable is considered **UNSAFE** and should not be done
unless you know what you're doing.

#### Adding backends to a repository
You can insert an already exisiting repository into another one with the `add`
command:
```
$ knoxite repo -r /main/repo add /second/repo
Added /second/repo to repository
```

#### Display repository information
Let knoxite show you information about the configured storage backends of a repository with
the `info` command:
```
$ knoxite repo -r /main/repo info
Storage URL                                       Available Space
-----------------------------------------------------------------
/main/repo                                             142.23 GiB
/second/repo                                           420.20 GiB
```

The `cat` command provides the information in *json* format:
```
$ knoxite repo cat -r /main/repo
{
    "version": 3,
    "volumes": null,
    "storage": [
        "/main/repo",
        "/second/repo"
    ]
}
```

#### Release redundant data
After some actions (e.g. removing snapshots) you can free up space by releasing
redundant data which is no longer referenced within your repository. Use the
`pack` command to do so:
```
$ knoxite repo pack
Chunk a1623dda9c02deac6da040e84e6af3e228af97fbbd42198529ba0c4836d83603 is no longer referenced by any snapshot. Deleting!
Chunk 5b1e1c3ca2de4a6951b61ff7aa41a272411c18e2e8954b12d6c5d4abd71c79e0 is no longer referenced by any snapshot. Deleting!
...
Freed storage space: 23.42 MiB
```

---

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
