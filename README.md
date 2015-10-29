# Ansible Role: manage_users

[![Build Status](https://travis-ci.org/smiller171/ansible-user-management.svg?branch=master)](https://travis-ci.org/smiller171/ansible-user-management)

[![Join the chat at https://gitter.im/smiller171/ansible-user-management](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/smiller171/ansible-user-management?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

<a href="https://zenhub.io"><img src="https://raw.githubusercontent.com/ZenHubIO/support/master/zenhub-badge.png"></a>

An Ansible role that sets up users and their ssh keys on unix-based systems  
Users can have multiple keys (add each as a list item)  
any keys not listed will be removed from the authorized_keys file

## Requirements
Set up sudoers file to allow passwordless sudo as passwords will not be set

## Role Variables

Available variables are listed below, along with default values:

The default shell that will be assigned to all users  
    shell: /bin/bash  

List of users that should exist, with authorized keys in a single list item broken by newlines

    manage_users_allowed:
      - name: foo
        authorized:
        - "ssh-rsa AAAAB3NzaC1yc2EAAAABJQAAAQEAlPYybp3CWDzRPo0uF/woyqkfhpZK2T7zn16z+fGYlRQl6gXATIUB4JYfr9pfD+SOW2T4X78P+/h1o4QPCwoesLacaFEFGwUb+SzhVVm6B6q4WMAiJWD6OVXh+SVVvD9rdcz5RMVLqQngrRqBlj4kBIMQ3S8h1cCESbR2P6jszgFj0I6p3tQCpo9yjcVwLqvWFKJgzEm2E2wV/gmrc0PhVRP2guIRN4p6M2ZyIPprdZ6PA8m7Rs4yN3jQ/0alrQ23ECCU4lHoVG9fwvLIq1vh4ikPcUrdA8sSHTE1pkpzvrTv7FtkuUcBrDMedFE7E8dB9pPS+vXIBWVUYJhp9WzVkQ== name@domain.com
        ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAklOUpkDHrfHY17SbrmTIpNLTGK9Tjom/BWDSUGPl+nafzlHDTYW7hdI4yZ5ew18JH4JW9jbhUFrviQzM7xlELEVf4h9lFX5QVkbPppSwg0cda3Pbv7kOdJ/MTyBlWXFCR+HAo3FXRitBqxiX1nKhXpHAZsMciLq8V6RjsNAQwdsdMFvSlVK/7XAt3FaoJoAsncM1Q9x5+3V0Ww68/eIFmb1zuUFljQJKprrX88XypNDvjYNby6vw/Pb0rwert/EnmZ+AW4OZPnTPI89ZPmVMLuayrD2cE86Z/il8b+gw3r3+1nKatmIkjn2so1d01QraTlMqVSsbxNrRFi9wrf+M7Q== smiller@domain.com"

Users that should be removed if they exist

    manage_users_unauthorized:
      - foobar

Groups that users should belong to

    manage_users_groups: "sudo,adm,dialout,cdrom,floppy,audio,video,plugdev"

## Dependencies

None.

## Example Playbook

    ---
    - hosts: all
      sudo: yes
      roles:
      - scott.miller171.manage_users
      vars:
      manage_users_allowed:
      - name: foo
        authorized:
        - "ssh-rsa AAAAB3NzaC1yc2EAAAABJQAAAQEAlPYybp3CWDzRPo0uF/woyqkfhpZK2T7zn16z+fGYlRQl6gXATIUB4JYfr9pfD+SOW2T4X78P+/h1o4QPCwoesLacaFEFGwUb+SzhVVm6B6q4WMAiJWD6OVXh+SVVvD9rdcz5RMVLqQngrRqBlj4kBIMQ3S8h1cCESbR2P6jszgFj0I6p3tQCpo9yjcVwLqvWFKJgzEm2E2wV/gmrc0PhVRP2guIRN4p6M2ZyIPprdZ6PA8m7Rs4yN3jQ/0alrQ23ECCU4lHoVG9fwvLIq1vh4ikPcUrdA8sSHTE1pkpzvrTv7FtkuUcBrDMedFE7E8dB9pPS+vXIBWVUYJhp9WzVkQ== name@domain.com
        ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAklOUpkDHrfHY17SbrmTIpNLTGK9Tjom/BWDSUGPl+nafzlHDTYW7hdI4yZ5ew18JH4JW9jbhUFrviQzM7xlELEVf4h9lFX5QVkbPppSwg0cda3Pbv7kOdJ/MTyBlWXFCR+HAo3FXRitBqxiX1nKhXpHAZsMciLq8V6RjsNAQwdsdMFvSlVK/7XAt3FaoJoAsncM1Q9x5+3V0Ww68/eIFmb1zuUFljQJKprrX88XypNDvjYNby6vw/Pb0rwert/EnmZ+AW4OZPnTPI89ZPmVMLuayrD2cE86Z/il8b+gw3r3+1nKatmIkjn2so1d01QraTlMqVSsbxNrRFi9wrf+M7Q== smiller@domain.com"

      - manage_users_unauthorized:
        - foobar

      - manage_users_groups: "sudo,adm,dialout,cdrom,floppy,audio,video,plugdev"

## License

MIT
