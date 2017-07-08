# ansible-atom

Ansible role to install and configure Atom on macOS with packages and preferences automatically set up.

## Requirements

- macOS 10.12 (earlier versions may work)

## Notes

This role was primarily developed for use with [Superlumic](http://superlumic.com/) but may be adapted for other use. Problems, recommendations and pull requests are welcome!

## Defaults

The only default task is installing Atom from Homebrew Cask, no other configuration is executed without being explicitly set.

## Role variables

The [example configuration](example/vars-example.yml) file is more fully documented and a good starting point. My full configuration can be viewed [here](https://github.com/christopherdwhite/superlumic-config/blob/master/roles/apps-atom/vars/main.yml).

### Atom Installation

Install the beta version of Atom from Homebrew Cask:

```yaml
### Install Beta
#
# Required: no
# Type: boolean
# Default: false
#
# Description:
#   Installs the beta version of Atom from Homebrew Cask
#
beta: true
```

### Packages

#### Install packages

The packages variable runs `apm install {{ packages }}` and supports all options except for `--packages-file` which is addressed in the next variable.

```yaml
### Install Packages
#
# Required: no
# Type: list
# Default: false
#
# Description:
#   Installs listed packages
#
# Command:
#   apm install {{ packages }}
#
packages:
  - aligner
  - aligner-css --check -- verbose --production --compatible
  - aligner-javascript --silent
  - aligner-php --quiet
  - aligner-scss@1.3.0
  - adrianlee44/atom-aligner-ruby
  - 'https://github.com/adrianlee44/atom-aligner-stylus'
```

#### Install packages from file

Instead of specifying your packages as a list of variables you can instead provide a plaintext file.

To use a packages file add a `files` folder to your role and include the file within it, then set the filename to the package_files variable

```yaml
### Install Packages from File
#
# Required: no
# Type: list (filenames)
# Default: false
#
# Command:
#   apm install --package-file {{ package_files }}
#
# Description:
#   This task uses the same install command as the install packages but allows you to pass a plaintext file listing packages delineated by new lines.
#
# Requirement:
#   Plaintext files should be placed within the files folder in the role and should only include the filename. The path is provided by the role.
#
package_files:
  - packages.txt
```

#### Uninstall packages

If you need to ensure that a package is not installed anywhere you can specify a list of packages to be uninstalled.

```yaml
### Uninstall Packages
#
# Required: no
# Type: list
# Default: false
#
# Command:
#   apm uninstall {{ packages }}
#   
# Description:
#   Uninstall packages
#
uninstall:
- alginer-luo
```

#### Other commands

##### Clean

```yaml
### clean
#
# Required: no
# Type: boolean
# Default: false
#
# Command:
#   apm clean
#
# Command --help:
#   Deletes all packages in the node_modules folder that are not referenced as a dependency in the package.json file.
#
clean: true
```

##### Config

```yaml
### config
#
# Required: no
# Type: array
# Default: false
#
# Command:
#   apm config {{ config.command }} {{ config.key }} {{ config.value }}
#
# Command --help:
#   Usage: apm config set <key> <value>
#          apm config get <key>
#          apm config delete <key>
#          apm config list
#          apm config edit
#
# Note:
#   All options are supported except for edit but not all of them make sense in the context of Ansible unless your doing some kind of output logging. Set and delete are the only options you would commonly use. Trying to use edit will be skipped altogether to prevent the text editor from hijacking the shell
#
config:
  - { command: 'set', key: 'some key', value: 'some value' }
  - { command: 'delete', key: 'some key'}
```

##### Dedupe

```yaml
### dedupe
#
# Required: no
# Type: list
# Default: false
#
# Command:
#   apm dedupe {{ dedupe.packages }}
#
# Command --help:
#   Usage: apm dedupe [<package_name>...]
#
#   Reduce duplication in the node_modules folder in the current directory.
#
#   This command is experimental.
#
# Note:
#   It appears that you can run this without specifying a package to presumably dedupe all but this has not been tested.
#
dedupe:
  -
  - 'some package'
```

## Dependencies

- [roderik.superlumic-homebrew](https://github.com/superlumic/ansible-role-homebrew)

# Usage

## Superlumic

Check [Superlumic](https://github.com/superlumic/superlumic) for documentation. A more complete tutorial for this role is in the works.

## Ansible

Non-Superlumic configuration and testing will be completed after basic role is complete.

# License

MIT

# Author

[Chris White](mailto:opensource@chris.christopherdwhite.com) - [@chrisWhite](http://www.twitter.com/chrisWhite)
