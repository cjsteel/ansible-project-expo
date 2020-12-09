# bash_magic

Usage of bash_magic makes it easy to manage and automate the addition and removal of bash startup file scripts using a traditional *.d directory structure without cluttering up your systems bash startup file(s). It is designed so that a single (vetted) repository of bash scripts can be used as it's source and allows the "activation" of only those scripts required for a particualr system or user via symlinks to `~/.*.d` directories used to organize them into basic categories.

* [Installing bash_magic](https://github.com/devonjones/bash_magic)

## Overview and Layout

Symlinks to a repository of scripts organized by types located in a users `~/bin/bash_magic` allow you to automatically load (import) the scripts when you start a terminal session.

```shell
~/.bashrc  # automatically loads all scripts pointed to by symlinks in the following directories:
~/.bash_aliases.d/
~/.bash_completion.d/
~/.bash_functions.d/
```
