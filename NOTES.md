# Bedrock Notes

## Roles 

### Vendor roles 

_NTP_:

This role installs and NTP.

__Network Time Protocol (NTP)__ is a networking protocol for clock synchronization between computer systems over packet-switched, variable-latency data networks. 

More information can be found [ntp.org](http://www.pool.ntp.org/en/)


### Bedrock roles 

__Common__:

* Apt update, install new packages
* Handlers for nginx, php-fpm, memcached
* [ADD] Defaults

__Swapfile__:

__Fail2ban__:

Installs and configures `Fail2ban`. Fail2Ban monitors log files of specific services and bans ip addresses with `iptables` firewall. 

__Ferm__:

Working with `iptables` directly can be really painful and the [ufw module](http://docs.ansible.com/ufw_module.html) is decent for basic needs but sometimes you need a bit more control. I also like the approach of writing templates rather than executing `allow`/`deny` commands with `ufw`.

__Network Time Protocol__:

This role enables users to install and configure ntp on their hosts.

__Mariadb__:

This role installs `Mariadb` and remove default DB.

__Users__:

* Ensures that `web_user` exists
* Adds `web_user` to `www-data`
* Create `/etc/sudoers.d` file

After running this role every sudoer has access to all commands within a variable set of users, and global setting determines whether NOPASSWD is set or not.


__SSMTP__:

Install and configure SSMTP - email delivery program.

__PHP__:

Install php 5.6 and other common php packages. Set up php.ini and php-fpm.conf configuration files.

__Nginx__:

Install and setup nginx configuration, wordpress nginx configuration, SSL if enabled

__Logrotate__:

Installs logrotate and provides an easy way to setup additional logrotate scripts by specifying a list of directives.

__Memcached__:

Install and setup Memcached with PHP support.

__Composer__:

Install and update composer.

__WP-CLI__:

Install command line interface for WordPress

__wordpress-setup__:



__wordpress-install__:




## To Do

- How to setup SSL? Name of `.cert` file ? 
- Logrotate details, add log rotates configurations for each service? 
- Add Memcached notes
- 

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
