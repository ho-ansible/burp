# Ansible role: burp
Graham Keeling's backup software.
This role is for a client that will send its backups to a
remote [server](https://github.com/ho-ansible/burp-server).

## Compiling binaries
For now, this role assumes you have precompiled binaries for the appropriate
version and platforms, stored under `files/bin`.
It would probably be better to create versioned packages for the OS.

To compile, setup a Debian build box as follows:
```
sudo apt-get install autoconf automake libtool g++ pkg-config
sudo apt-get install librsync-dev libz-dev libssl-dev uthash-dev libyajl-dev libncurses-dev
git clone https://github.com/grke/burp && cd burp/
git checkout {{ burp_version }}
autoreconf -fis
./configure --prefix=/usr --sysconfdir=/etc/burp --localstatedir=/var
make
```

## Requirements
Only tested on Debian stable, for now.

## Role Variables
+ `burp_server`: address of remote burp server
+ `burp_port` (default: 4971): TCP port of remote server
+ `burp_status_port (default: 4972): TCP port of remote status server
+ `burp_conf_dir` (default: /etc/burp): where to put all config files
+ `burp_server_CN` (default: burp): Common Name on SSL cert presented by server
+ `burp_pw` (default: none): simple pre-shared password authenticating client-server communication

## Dependencies
None.

## Example Playbook

```
- hosts: all
  roles:
    - { role: ho-ansible.burp }
```

## License
+ burp is licensed [AGPLv3](https://burp.grke.org/licence.html).
+ This ansible role is licensed [MIT](LICENSE).

## Author Information
+ burp is by [Graham Keeling](http://burp.grke.org/)
+ This ansible role is by [Sean Ho](https://github.com/ho-ansible/)
