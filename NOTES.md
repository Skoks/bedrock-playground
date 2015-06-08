# Bedrock Notes

## Roles 

### Vendor roles 



### Bedrock roles 

_Common:_

* Apt update, install new packages
* Handlers for nginx, php-fpm, memcached
* [ADD] Defaults

_Swapfile:_

_Fail2ban:_

_Ferm:_

_Ntp:_

__Network Time Protocol (NTP)__ is a networking protocol for clock synchronization between computer systems over packet-switched, variable-latency data networks. 

More information can be found [ntp.org](http://www.pool.ntp.org/en/)

_Users:_

_Mariadb:_

_Ssmpt:_

_Php:_

_Nginx:_

_Logrotate:_

_Memcached:_

_Composer:_

_WP-CLI:_

## To Do

```
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

* `deploy.sh`
* `deploy.yml`
* role `deploy`