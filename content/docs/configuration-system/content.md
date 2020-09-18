+++
fragment = "content"
weight = 100
title = "Configuration System"
subtitle = "knoxite's configuration system"

[sidebar]
  sticky = true
+++

<p>

Knoxite provides a configuration system for your repositories. You can declare
shorthands for your repositories and provide default values for settings like
encryption, compression or excludes.
The `config` command offers a variety of subcommands in order to help you
managing your configuration.

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
```

A configuration is structured in [toml](https://github.com/toml-lang/toml) format and looks like
this:
```toml
[repositories]
  [repositories.fort]
    url = "/tmp/knox"
    compression = "gzip"
    tolerance = 0
    encryption = ""
    store_excludes = ["dont/store/this/folder*", "and/this/file"]
    restore_excludes = ["dont/restore/this/folder*"]
```

### Initializing the configuration

Before we can start composing our configuration we need to initialize the empty
file first. You can do that using the `init` command:
```
$ knoxite config init
2020/08/26 13:33:33 Writing configuration file to: /home/user/.config/knoxite/knoxite.conf
```

This will leave us with an empty configuration file:
```toml
[repositories]
```

By default knoxite will use the OS dependant standard paths for this file:
- On Unix based systems this is `~/.config/knoxite/knoxite.conf            `
- On macOS it's                 `~/Library/Preferences/knoxite/knoxite.conf`
- and on Windows it's           `%LOCALAPPDATA%/knoxite/Config/knoxite.conf`

You can also specify the desired location and configuration backend with the `-C
| --configURL` flag like this:
```
$ knoxite config init -C crypto://password@/home/user/config/knoxite/encrypted.conf
2020/08/17 10:49:51 Writing configuration file to: /home/user/.config/knoxite/encrypted.conf
```

Here we initialize the configuration file to be encrypted with the password
`password` and store it with the name `encrypted.conf`. You can also omit the
password part and knoxite will prompt you for it - this is also considered more
secure.
Another cool thing is that knoxite will recognize encrypted configuration files
while trying to read them out. Therefore you can reference them just like a
normal configuration file - without the `crypto://` protocol prefix - in further
usage.

### Creating an alias
The `alias` command creates a shorthand for a repository's configuration. In
this example we're assigning the alias `fort` to the repo located at
`/tmp/knox`:
```
$ knoxite config alias fort -r /tmp/knox
```

Looking at our configuration again we can see that we've created the shorthand
`fort` with a configuration profile:
```toml
[repositories]
  [repositories.fort]
    url = "/tmp/knox"
    compression = ""
    tolerance = 0
    encryption = ""
```

This shorthand can now further be used in the `-R | --alias` flag when executing
other commands:
```
$ knoxite -R fort store latest .
...
```

### Setting values
The `set` command lets you specify configuration values for an alias stored in
the knoxite configuration. This is especially useful while working with
encrypted configuration files.

```
Usage:
  knoxite config set <option> <value> [flags]
```

The option value consists of the repos alias and the configuration value to set
separated by a dot.

This is how this command can look like in action:
```
$ knoxite config set fort.compression gzip
```
Here we set `gzip` as the default compression algorithm for the `fort`
repository which looks like this in the config:

```toml
[repositories]
  [repositories.fort]
    url = "/tmp/knox"
    compression = "gzip"
    tolerance = 0
    encryption = ""
```

The `store_excludes` and `restore_excludes` are defined as an array of strings
and will work with the pattern syntax specified in Golangs
`filepath.Match`-Method. You can find it [here](https://golang.org/pkg/path/filepath/#Match).

Here's an example:
```
$ knoxite config set fort.store_excludes dont/store/this/folder\* and/this/file
```

```toml
[repositories]
  [repositories.fort]
    url = "/tmp/knox"
    compression = "gzip"
    tolerance = 0
    encryption = ""
    store_excludes = ["dont/store/this/folder*", "and/this/file"]
```

### Converting between backends
The `convert` command helps you to translate between different configuration
backends. There are currently three types of configuration backends supported
by knoxite:
- `file://`:   normal unencrypted toml file (default)
- `crypto://`: AES-GCM encrypted file
- `mem://`:    no file - everything in memory

Converting an unencrypted configuration file into an encrypted one does work
like this:
```
$ knoxite config convert ~/.config/knoxite/knoxite.conf crypto://password@~/.config/encrypted-knoxite.conf
```
As always you can also omit the password part as knoxite will prompt for a
password when none is supplied.


### Displaying the configs contents
The `info` and `cat` command can both be used to display the configurations
contents.

The `info` command outputs a quick summary of the stored configurations:
```
$ knoxite config info
Alias            Storage URL                          Compression      Tolerance             Encryption
-------------------------------------------------------------------------------------------------------
fort             /tmp/knox                            gzip             0
```

To display the full configuration in the original toml format use `cat`:
```
$ knoxite config cat
[repositories]
  [repositories.fort]
    url = "/tmp/knox"
    compression = "gzip"
    tolerance = 0
    encryption = ""
    store_excludes = ["dont/store/this/folder*", "and/this/file"]
```

Note that the `cat` command also displays the exclude options for store and
restore operations whereas `info` does not provide any information on these at
the moment.

</p>
