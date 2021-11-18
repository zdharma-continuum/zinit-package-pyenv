# Deprecated

❗ All zinit-packages have been migrated to https://github.com/zdharma-continuum/zinit-packages
You'll find the source for this here package in https://github.com/zdharma-continuum/zinit-packages/tree/HEAD/pyenv
# pyenv/pyenv as a Zsh package

##### Homepage link: [pyenv/pyenv](https://github.com/pyenv/pyenv)

| **Package source:** | Source Tarball | Binary | Git | Node | Gem |
|:-------------------:|:--------------:|:------:|:---:|:----:|:---:|
| **Status:**         |    + <br> (default) |  -  | + | – |  –  |

[Zplugin](https://github.com/zdharma-continuum/zinit) can use the NPM package registry
to automatically:

- get the plugin's Git repository OR release-package URL,
- get the list of the recommended ices for the plugin,
    - there can be multiple lists of ices,
    - the ice lists are stored in *profiles*; there's at least one profile, *default*,
    - the ices can be selectively overriden.

Example invocations that'll install
[pyenv/pyenv](https://github.com/pyenv/pyenv) either from the release archive
or from Git repository:

```zsh
# Download the tarball with the default ice list
zplugin pack for pyenv

# Download the tarball with the bin-gem-node annex-utilizing ice list
zplugin pack"bgn" for pyenv

# Download with the bin-gem-node annex-utilizing ice list FROM GIT REPOSITORY
zplugin pack"bgn" git for pyenv
```

## Default Profile

Provides the `pyenv` version manager by extending `$PATH` to make it point into
the `bin` subdirectory of the plugin.

The Zplugin command executed will be equivalent to:

```zsh
zplugin lucid as'command' pick'bin/pyenv' atinit'export PYENV_ROOT="$PWD"' \
    atclone'PYENV_ROOT="$PWD" ./libexec/pyenv init - > zpyenv.zsh' \
    atpull"%atclone" src"zpyenv.zsh" nocompile'!' for \
        pyenv/pyenv
```

## Bin-Gem-Node Profile

Provides the version manager via *shims*, i.e.: automatic forwarder scripts created
under `$ZPFX/bin` (which is added to the `$PATH` by default by Zplugin). It needs the
[bin-gem-node](https://github.com/zplugin/z-a-bin-gem-node) annex (it has the
shim-creation feature).

The Zplugin command executed will be equivalent to:

```zsh
zplugin as'null' lucid  atinit'export PYENV_ROOT="$PWD"' \
    atclone'PYENV_ROOT="$PWD" ./libexec/pyenv init - > zpyenv.zsh' \
    atpull"%atclone" src"zpyenv.zsh" nocompile'!' sbin"bin/pyenv" for \
        pyenv/pyenv
```

<!-- vim:set ft=markdown tw=80 fo+=an1 autoindent: -->
