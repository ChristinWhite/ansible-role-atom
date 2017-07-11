# ansible-atom

Ansible role to install and configure Atom on macOS with packages and preferences automatically set up.

![License](https://img.shields.io/github/license/mashape/apistatus.svg)

## Requirements

- macOS 10.12 (earlier versions may work)

## Notes

This role was primarily developed for use with [Superlumic](http://superlumic.com/) but may be adapted for other use. Problems, recommendations and pull requests are welcome!

## Defaults

The only default task is installing Atom from Homebrew Cask, no other configuration is executed without being explicitly set.

## Role variables

The [example configuration](example/vars-example.yml) file is more fully documented and a good starting point. My full configuration can be viewed [here](https://github.com/christopherdwhite/superlumic-config/blob/master/roles/apps-atom/vars/main.yml).

# Usage

## Superlumic

Check [Superlumic](https://github.com/superlumic/superlumic) for documentation. A more complete tutorial for this role is in the works.

## Ansible

Non-Superlumic configuration and testing will be completed after basic role is finished.

# License

MIT

# Author

[Chris White](mailto:opensource@chris.christopherdwhite.com) - [@chrisWhite](http://www.twitter.com/chrisWhite)
