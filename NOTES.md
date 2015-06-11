# Bedrock Notes

## Roles 

### Vendor roles 

_NTP:_

This role installs and NTP.

__Network Time Protocol (NTP)__ is a networking protocol for clock synchronization between computer systems over packet-switched, variable-latency data networks. 

More information can be found [ntp.org](http://www.pool.ntp.org/en/)


### Bedrock roles 

_Common:_

* Apt update, install new packages
* Handlers for nginx, php-fpm, memcached
* [ADD] Defaults

_Swapfile:_

_Fail2ban:_

Installs and configures `Fail2ban`. Fail2Ban monitors log files of specific services and bans ip addresses with `iptables` firewall. 

_Ferm:_



_Users:_

* Ensures that `web_user` exists
* Adds `web_user` to `www-data`
* Create `/etc/sudoers.d` file

After running this role every sudoer has access to all commands within a variable set of users, and global setting determines whether NOPASSWD is set or not.

_Mariadb:_

_Ssmpt:_

_Php:_

_Nginx:_

_Logrotate:_

_Memcached:_

_Composer:_

_WP-CLI:_

## To Do

### Development roles

```
# Dev.yml

  roles:
    - { role: common, tags: [common] }
    - { role: fail2ban, tags: [fail2ban] }
    - { role: ferm, tags: [ferm] }
    - { role: ntp }
    - { role: mariadb, tags: [mariadb] }
    - { role: ssmtp, tags: [ssmtp mail] }
    - { role: php, when: not hhvm, tags: [php] }
    - { role: hhvm, when: hhvm, tags: [hhvm] }
    - { role: php5-xdebug, tags: [xdebug], when: xdebug_install | default(False) }
    - { role: nginx, tags: [nginx] }
    - { role: logrotate, tags: [logrotate] }
    - { role: memcached, tags: [memcached] }
    - { role: composer, tags: [composer] }
    - { role: wp-cli, tags: [wp-cli] }
    - { role: wordpress-setup, tags: [wordpress, wordpress-setup] }
    - { role: wordpress-install, tags: [wordpress, wordpress-install] }
```

### Production roles

```
# Server.yml

  roles:
    - { role: common, tags: [common] }
    - { role: swapfile, swapfile_size: 1GB, tags: [swapfile] }
    - { role: fail2ban, tags: [fail2ban] }
    - { role: ferm, tags: [ferm] }
    - { role: ntp }
    - { role: users, tags: [users] }
    - { role: mariadb, tags: [mariadb] }
    - { role: ssmtp, tags: [ssmtp mail] }
    - { role: php, when: not hhvm, tags: [php] }
    - { role: hhvm, when: hhvm, tags: [hhvm] }
    - { role: nginx, tags: [nginx] }
    - { role: logrotate, tags: [logrotate] }
    - { role: memcached, tags: [memcached] }
    - { role: composer, tags: [composer] }
    - { role: wp-cli, tags: [wp-cli] }
    - { role: github-ssh-keys, tags: [github-ssh-keys], when: github_ssh_keys is defined }
    - { role: wordpress-setup, tags: [wordpress, wordpress-setup] }
```

### Deployment 

* `deploy.sh`
* `deploy.yml`
* role `deploy`

### Import/dump mysql DB

http://docs.ansible.com/mysql_db_module.html
