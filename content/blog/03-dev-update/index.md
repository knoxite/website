+++
fragment = "content"
weight = 100
#background = ""
#categories = ["knoxite", "blog", "dev update"]

title = "Knoxite Dev Update - 27. August 2020"
title_align = "left"
summary = "It has been a while since the last update from us. Here are some of our development highlights"

display_date = true
date = "2020-08-27"
+++

## Knoxite Development
Quite some things happened over the past months. Here are some of our highlights
in development since our last post. You may want to check them out.

### Core
- We've switched from TravisCI to Github Actions and seperated
  our workflows into *lint*, *built* and *test*. (@muesli
  [#92](https://github.com/knoxite/knoxite/pull/92)
  [#142](https://github.com/knoxite/knoxite/pull/142/)).
- We now provide the knoxite library in our projects root folder and moved
  the commands into a dedicated `cmd/` folder. This is also described in Golangs
  project stucture conventions. (@muesli
  [#96](https://github.com/knoxite/knoxite/pull/96)).

### CLI
- Knoxite now provides a `-v | --version` flag (@craftamap
  [#111](https://github.com/knoxite/knoxite/pull/111)).
- Verify the integrity of your repositories contents at any time with the `verify` command
  (@craftamap [#119](https://github.com/knoxite/knoxite/pull/119)).
  ```
  $ knoxite verify --help
  verify a repo, volume or snapshot

  Usage:
    knoxite verify [<volume> [<snapshot>]] [flags]

  Flags:
    -h, --help             help for verify
    --percentage int   How many archives to be checked between 0 and 100 (default 70)
  ```

- You can change the password of a repository at any time now (@mahartma
  [#114](https://github.com/knoxite/knoxite/pull/114)
  [#128](https://github.com/knoxite/knoxite/pull/128)
  [#116](https://github.com/knoxite/knoxite/pull/116)).
  ```
  $ knoxite repo passwd --help
  The passwd command changes the password of a repository

  Usage:
    knoxite repo passwd [flags]

  Flags:
    -h, --help   help for passwd
   ```

- Knoxite now offers a modular configuration system (@penguwin
  [#120](https://github.com/knoxite/knoxite/pull/120)). You can declare
  shorthands for your repositories and provide default values for settings like
  compression, fault tolerance, encryption and more. Read more about it
  [here]({{< ref "docs/configuration-system">}}).
  ```
  $ knoxite config --help
  The config command manages the knoxite configuration

  Usage:
    knoxite config [command]

  Available Commands:
    alias       Set an alias for the storage backend url to a repository
    cat         display the configuration file on stdout
    convert     convert between several configuration backends
    info        display information about the configuration file on stdout
    init        initialize a new configuration
    set         set configuration values for an alias

  Flags:
    -h, --help   help for config

  Global Flags:
    -C, --configURL string   Path to the configuration file (default "/home/penguwin/.config/knoxite/knoxite.conf")
    -p, --password string    Password to use for data encryption
    -r, --repo string        Repository directory to backup to/restore from (default: current working dir)

  Use "knoxite config [command] --help" for more information about a command.
  ```

### Storage Backends

- Platforms with unlimited storage capabilities will now handle back the
  `ErrAvailableSpaceUnlimited` error (@mahartma
  [#146](https://github.com/knoxite/knoxite/pull/146)).
- We now provie support for [Google Cloud](https://cloud.google.com) (@mahartma
  [#88](https://github.com/knoxite/knoxite/pull/88)
  [#110](https://github.com/knoxite/knoxite/pull/110)).
- Tests for [Mega](https://mega.nz/) are now working again (@mahartma
  [#133](https://github.com/knoxite/knoxite/pull/133)).
- Tests for [Microsoft Azure](https://azure.microsoft.com) are also working
  again (@mahartma [#115](https://github.com/knoxite/knoxite/pull/115)).
- Tests for SFTP backend (@craftamap
  [#87](https://github.com/knoxite/knoxite/pull/87/files)).
- Tests for WebDAV backend  (@craftamap
  [#97](https://github.com/knoxite/knoxite/pull/97)).

For more informations on our storage backends refer to the
[documentation section]({{<ref "docs/storage-backends">}}).

### Misc
A huge amount of improvements, tweaks and minor bugfixes have been submitted by
the knoxite developers since the last time. \
Click
[here](https://github.com/knoxite/knoxite/compare/master@%7B2020-04-14%7D...master@%7B2020-08-27%7D)
for a full commit backlog since our last update.


## Knoxite Hack Retreat

Currently the preparations are in full swing for our **first ever Knoxite Hack
Retreat**. The event will occur between the 31st August and 06th September and
takes place in Zelhelm, Netherlands.
We're optimistic to accomplish all tasks which are left for the first release of
knoxite during this event and are looking forward for a generally good time.

---

Thats it for this update - hope to see you for the next time again.
