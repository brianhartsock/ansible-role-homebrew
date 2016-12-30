Ansible Role Homebrew
=========

[![Build Status](https://travis-ci.org/brianhartsock/ansible-role-homebrew.svg?branch=master)](https://travis-ci.org/brianhartsock/ansible-role-homebrew)

Simple role to install [homebrew](http://brew.sh), homebrew packages, and [homebrew cask](https://caskroom.github.io) packages. It will also update homebrew and upgrade packages.

Requirements
------------

- OSX
- [Homebrew](http://brew.sh)

Role Variables
--------------

Customize the defaults to fit your own needs. These are very specific to my personal insall.

|Name|Description|Default|
|----|-----------|-------|
|homebrew_update|Wheether or note to update homebrew and upgrade all packages each run|true|
|homebrew_packages|List of homebrew packages to install.|See [defaults](defaults/main.yml)|
|homebrew_cask_packages|List of homebrew cask packages to install.|See [defaults](defaults/main.yml)|

Dependencies
------------

_None_

Example Playbook
----------------

    - hosts: localhost
      roles:
         - brianhartsock.homebrew

License
-------

MIT

Author Information
------------------

Created with love by [Brian Hartsock](http://blog.brianhartsock.com).
