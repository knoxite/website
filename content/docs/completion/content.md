+++
fragment = "content"
weight = 100
title = "Completion"
subtitle = "Generate command-line completion for a variety of shells"

[sidebar]
  sticky = true
+++

## Bash

This script depends on the `bash-completion` package. If it is not installed
  already, you can install it via your OS's package manager.

To load completions in your current shell session:
```
$ source <(knoxite completion bash)
```

To load completions for every new session, execute once:
Linux:
```
$ knoxite completion bash > /etc/bash_completion.d/knoxite
```
MacOS:
```
$ knoxite completion bash > /usr/local/etc/bash_completion.d/knoxite
```

You will need to start a new shell for this setup to take effect.

## Fish

To load completions in your current shell session:
```
$ knoxite completion fish | source
```

To load completions for every new session, execute once:
```
$ knoxite completion fish > ~/.config/fish/completions/knoxite.fish
```

You will need to start a new shell for this setup to take effect.

## Powershell

To load completions in your current shell session:
```
PS C:\> knoxite completion powershell | Out-String | Invoke-Expression
```

To load completions for every new session, add the output of the above command
to your powershell profile.

## Zsh
If shell completion is not already enabled in your environment you will need to
enable it. You can execute the following once:

```
$ echo "autoload -U compinit; compinit" >> ~/.zshrc
```

To load completions for every new session, execute once:

Linux:
```
$ knoxite completion zsh > "${fpath[1]}/_knoxite"
```

MacOS:
```
$ knoxite completion zsh > /usr/local/share/zsh/site-functions/_knoxite
```

You will need to start a new shell for this setup to take effect.

## Other

Is your shell not listed? We got you covered!

You can use the hidden `_carapace` command to generate the completion for
following shells:
- Elvish
- Ion
- Nushell
- Oil
- Tcsh
- Xonsh

Note that support for these shells is currently *experimental*, refer to the
corresponding help text for install instructions.
