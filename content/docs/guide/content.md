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
A repository contains volumes which store your data organized in
[snapshots](#snapshots).

#### Initializing a volume
To initialize a volume use the `init` command and provide a name for it:
```
$ knoxite volume init "Backups" -d "My system backups"
Volume 66e03034 (Name: Backups, Description: My system backups) create
```

Optionally you can provide a further description on the volumes purpose with the
`-d, --description` flag.

#### List volumes
You can also `list` all your volumes inside of a repository:
```
$ knoxite volume list
ID        Name                              Description
--------------------------------------------------------------------------------------------
da0327e0  Project                           My projects data stored in knoxite
908b4279  Music                             My music collection stored in knoxite
990726a7  Pictures                          My pictures stored in knoxite
```

---

### Snapshots
Snapshots are best used to incremental store your data in a volume. Knoxite
takes care to chunk your data, encrypt it and to de-duplicate redundant data
chunks.
You can choose between several encryption and compression algorithms in the
process.
When your repository contains several storage backends you're also able to set
a fault-tolerance level for your snapshots.

#### Store data in a snapshot
In order to create a new snapshot choose your the desired volume and hit the
`store` command:
```
$ knoxite store [volume ID] data -d "Backup of my data"
data/document.txt                   5.17 MiB  236.51 MiB/s [#############################] 100.00%
data/other.txt                      3.55 MiB  257.24 MiB/s [#############################] 100.00%
...
Snapshot 13190897 created: 17 files, 2 dirs, 0 symlinks, 0 errors, 1.71 GiB Original Size, 1.42 GiB Storage Size
```

The `store` command offers a variety of useful flags:
- `-c, --compression` lets you choose the compression algorithm used to store
  your data.
- `-d, --description` can be used to describe changes made from snapshot to
  snapshot.
- `-e, --encryption` lets you choose the encryption algorithm.
- `-t, --tolerance` can be used to set a fault tolerance level against *n*
  backend failures.
- `-x, --excludes` lets you choose to exclude files and folders from the
  snapshot.

Run `snapshot store --help` for further information or see the guide
sections: [Compression](#compression), [Encryption](#encryption) and
[Fault-Tolerance](#fault-tolerance)

#### List Snapshots
You can get an overview of snapshots stored within a volume using the `list`
command:
```
$ knoxite snapshot list [volume ID]
ID        Date                 Original Size  Storage Size  Description
-----------------------------------------------------------------------------------------------
13190897  2020-04-20 04:20:20       1.71 GiB      1.42 GiB  Backup of my data
a44c9844  2020-04-20 04:23:42       8.72 MiB      1.00 MiB  Added some more data
-----------------------------------------------------------------------------------------------
                                    1.71 MiB      1.42 GiB
```

#### Viewing a snapshot's content
Running the following command lists the entire content of a snapshot:

```
$ knoxite ls [snapshot ID]
Perms       User   Group          Size  ModTime              Name
----------------------------------------------------------------------------------------------
-rw-r--r--  user   group      5.69 MiB  2016-07-29 02:06:04  document.txt
-rw-r--r--  user   group      4.17 MiB  2016-07-29 02:05:22  other.txt
...
```

#### Displaying a file's contents
With the following command you can also print out a file's content to stdout:
```
$ knoxite cat [snapshot ID] document.txt
This is the sample text stored in document.txt
```

#### Cloning a snapshot
It's easy to clone an existing snapshot, adding files to or updating existing
files in it:

```
$ knoxite -r /tmp/knoxite clone [snapshot ID] $HOME
document.txt          5.89 MiB / 5.89 MiB [#########################################] 100.00%
other.txt             5.10 MiB / 5.10 MiB [#########################################] 100.00%
...
Snapshot aefc4591 created: 9 files, 8 dirs, 0 symlinks, 0 errors, 1.34 GiB Original Size, 1.34 GiB Storage Size
```

The `clone` and `store` commands share the same set of optional command line
flags. So while cloning you snapshots you can still choose between several
encryption and compression algorithms, set a fault-tolerance level or exclude
files and folders.

#### Mounting a snapshot
You can even mount a snapshot (currently read-only, read-write is
work-in-progress):

```
$ knoxite -r /tmp/knoxite mount [snapshot ID] /mnt
```

---

### Encryption
Choose between several encryption algorithms with the `-e, --encryption` flag
while storing your data.

```
$ knoxite store -e aes latest data/ -d "AES encrypted snapshot"
```

### Fault-Tolerance
Assuming you've already configured several backends in your repository you can
consider to set a fault tolerance level agains *n* backend failures with the
`-t, --tolerance` flag like this:
```
$ knoxite store [volume ID] data/ -t 2
data/document.txt                      5.17 MiB  123.42 MiB/s [#############################] 100.00%
data/other.txt                         3.55 MiB  420.49 MiB/s [#############################] 100.00%
8.72 MiB / 8.72 MiB (3 of 3) 126.73 MiB/s [#################################################] 100.00%
Snapshot c82d256e created: 2 files, 1 dirs, 0 symlinks, 0 errors, 8.72 MiB Original Size, 4.36 MiB Storage Size
```

In this example two storage backends can be offline and you're still able to
access all of your data stored in this snapshot. Knoxite verifies that the
chosen fault tolerance level is **below** the number of configured storage
backends for the repository. See the [repository](#repositories) section for
more information on adding storage backends to your repository.

### Compression
While storing data into snapshots you can choose to compress your data with
several algorithms.

To do so use the the `-c --compression` option:

```
$ knoxite store -c gzip latest data/ -d "Compressed snapshot"
```

For a full list of available compression algorithms refer to the `--help` option:
```
$ knoxite store --help
...
Flags:
  -c, --compression string     compression algo to use: none (default), flate, gzip, lzma, zlib, zstd
```

### Automatic backups

### Restoring a backup
You can `restore` your data from a snapshot to a desired location as simply as this:
```
$ knoxite restore [snapshot ID] /desired/location
data/other.txt       3.55 MiB / 3.55 MiB  69.78 MiB/s [#############################] 100.00%
data/document.txt    5.17 MiB / 5.17 MiB  91.11 MiB/s [#############################] 100.00%
Restore done: 2 files, 1 dirs, 0 symlinks, 0 errors, 8.72 MiB Original Size, 4.27 MiB Storage Size
```

You can prevent restoring unwanted files or directories with the `x, --excludes`
flag.

</p>
