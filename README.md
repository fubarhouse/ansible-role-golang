# Ansible Role: Go

[![Build Status](https://travis-ci.org/fubarhouse/ansible-role-golang.svg?branch=master)](https://travis-ci.org/fubarhouse/ansible-role-golang)
[![Ansible Galaxy](https://img.shields.io/badge/galaxy-fubarhouse--golang-5140.svg)](https://galaxy.ansible.com/fubarhouse/golang)
[![MIT licensed](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/fubarhouse/ansible-role-golang/master/LICENSE)

* Install Go to configurable locations.
* Install Go packages
* Support for custom `go get` applications.

**Note**: I am actively seeking packages to include here which are installed using `go get`. They will all feature custom installation tasks and logic.
 
**Note**: You may be required to restart your shell session or to source the configured `shell_profiles` prior to use after installation.

## Requirements

  None.

## Role Variables

Basic configuration
````
go_version: 1.7.4
go_location: /usr/local/go
````

***OS-Specific configuration***

To get this role working on Mac, or any other non-windows system specified at the Go [download page](https://golang.org/dl/), change this variable to the respective code of your system:
````
go_arch: linux-amd64
````
**Note**: Although not officially supported the maintainer does use this role on Mac, and there is no practical reason other platforms (other than Windows) should not work.

To install GoPM, and any other `go get` binaries/projects, add them to `go_get`
````
go_get:
- github.com/gpmgo/gopm
````

To add packages (none installed currently by default), use gopm_packages (depends on gopm). 
````
gopm_packages:
- math
````

To add/change the shell profiles to configure, use the `shell_profiles` array.
````
shell_profiles:
- .bash_profile
````

## Dependencies

None.

## Example Playbook
````
- hosts: localhost
  roles:
    - fubarhouse.python
````

## Installation

* Install using `ansible-galaxy install fubarhouse.python`
* Add the Python role to your playbook.
* Modify above variables as desired.

## License

MIT / BSD

## Author Information

This role was created in 2015 by [Karl Hepworth](https://twitter.com/fubarhouse).
