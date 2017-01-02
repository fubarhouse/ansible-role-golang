# Ansible Role: Go

[![Build Status](https://travis-ci.org/fubarhouse/ansible-role-golang.svg?branch=master)](https://travis-ci.org/fubarhouse/ansible-role-golang)
[![Ansible Galaxy](https://img.shields.io/badge/galaxy-fubarhouse--golang-5140.svg)](https://galaxy.ansible.com/fubarhouse/golang)
[![MIT licensed](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/fubarhouse/ansible-role-golang/master/LICENSE)

* Clean install optional - recommended if changing between static and gvm installations.
* Install a static binary of Go; or
* Install multiple versions of Go using GVM; or
* Install from Go Source (currently does not compile Go source).
* Installs using the Ansible way, the GVM installation script has been converted into Ansible tasks.
* Install allows additional flags to be passed in (ie --binary --prefer-binary --source)
* Install from mirror URL
* Install to any location
* Example playbooks have been provided for the four installation types.

## Requirements

  None.

## Role Variables

Installation configuration
````
go_install_type: gvm # or static
go_install_flag: "--binary"
go_custom_mirror: https://storage.googleapis.com/golang
````

Basic configuration
````
go_version: 1.7.4
go_location: /usr/local/go

````

Multiple version configuration
````
go_versions:
- 1.4
- 1.7.1
- 1.7.3
````

***OS-Specific configuration***

To get `static` installations working on Mac, or any other non-windows system specified at the Go [download page](https://golang.org/dl/), change this variable to the respective code of your system:
````
go_arch: linux-amd64
````
**Note**: Although not officially supported the maintainer does use this role on Mac, and there is no practical reason other platforms (other than Windows) should not work.

To install GoPM, and any other `go get` binaries/projects, add them to `go_get`
````
go_get:
- name: gopm
  url: github.com/gpmgo/gopm
- name: golint
  url: github.com/golang/lint/golint
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

### Example #1 - default installation
````
- hosts: localhost
  roles:
    - fubarhouse.golang
````

### Example #2 - static installation
````
- hosts: localhost
  vars:
    go_install_type: static
    go_version: go1.7.4
  roles:
    - fubarhouse.golang
````

### Example #3 - standard gvm installation
````
- hosts: localhost
  vars:
    go_install_type: gvm
    go_version: go1.7.4
    go_versions:
    - 1
    - 1.7.0
    - 1.7.1
    - 1.7.3
  roles:
    - fubarhouse.golang
````

### Example #4 - gvm installation via source method
****Note****: The `source` method does not build/compile versions, but still runs off binary installations by default. This is planned to change in the future.
````
- hosts: localhost
  vars:
    go_install_type: source
    go_version: go1.7.4
    go_versions:
    - go1
    - go1.7.1
  roles:
    - fubarhouse.golang
````

## Installation

* Install using `ansible-galaxy install fubarhouse.golang`
* Add this role to your playbook.
* Modify above variables as desired.
* Whenever changes/upgrades are required, it's ****recommended**** to either:
  * set `go_install_clean` to `true` (boolean) in order to perform a clean installation; or
  * simply rerun with the changed variables in order to relink the symlinks to the default go version - otherwise the symlinks to `go_get` packages will always point to their original destination.

## License

MIT / BSD

## Author Information

This role was created in 2016 by [Karl Hepworth](https://twitter.com/fubarhouse).
