<img style="float:left" alight="left" height="128px" width="100px" src="https://github.com/fubarhouse/ansible-role-golang/raw/master/gopher.png">

# Ansible Role: Go

[![Build Status](https://travis-ci.org/fubarhouse/ansible-role-golang.svg?branch=master)](https://travis-ci.org/fubarhouse/ansible-role-golang)
[![Ansible Galaxy](https://img.shields.io/badge/galaxy-fubarhouse--golang-5140.svg)](https://galaxy.ansible.com/fubarhouse/golang)
[![MIT licensed](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/fubarhouse/ansible-role-golang/master/LICENSE)

* Clean installs optional
* Installs a Go workspace
* Installs from mirror URL
* Installs to any location

## Requirements

  None.

## Role Variables

Installation configuration
````
go_custom_mirror: https://storage.googleapis.com/golang
````

Basic configuration
````
go_version: 1.8.1
GOROOT: /home/vagrant/go
````

Optional configuration
````
GOOS: darwin
GOARCH: amd64
````

To install `go get` binaries/projects, add them to `go_get`
````
go_get:
- name: gopm
  url: github.com/gpmgo/gopm
- name: golint
  url: github.com/golang/lint/golint
````

To ensure all packages are removed before running the play, you can use the go_reget variable:
````
go_reget: true
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

Image of Go's mascot was created by [Takuya Ueda](https://twitter.com/tenntenn). Licenced under the Creative Commons 3.0 Attributions license. This image has been resized for purpose, but is otherwise unchanged.