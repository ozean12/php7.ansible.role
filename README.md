# Ansible Role: PHP7 (PHP-FPM)

[![Build Status](https://travis-ci.org/chusiang/php7.ansible.role.svg?branch=master)](https://travis-ci.org/chusiang/php7.ansible.role) [![Ansible Galaxy](https://img.shields.io/badge/role-php7-blue.svg)](https://galaxy.ansible.com/chusiang/php7/)

An Ansible role of Deploy PHP 7 (php-fpm) for nginx on CentOS, Debian, and Ubuntu. (forked from [itcraftsmanpl.php7](https://galaxy.ansible.com/itcraftsmanpl/php7/))

* Current PHP7 version:

 * Debian & Ubuntu: **7.0.6**
 * CentOS: **7.0.5**

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    # All.
    php_timezone: Asia/Taipei
    php_upload_max_filesize: "20M"
    php_post_max_size: "20M"
    php_memory_limit: "1024M"
    
    # Debian & Ubuntu.
    debian_php7_apt_repo: "http://packages.dotdeb.org"
    debian_php7_apt_key: "https://www.dotdeb.org/dotdeb.gpg"
    ubuntu_php7_ppa_repo: "ppa:ondrej/php"
    
    apt_php_packages:
      - php7.0
      - php7.0-common
      - php7.0-cli
      - php7.0-intl
      - php7.0-curl
      - php7.0-cgi
      - php7.0-fpm
      - php7.0-mysql
      - php7.0-gd
    
    yum_php_packages:
      - php70u-cli
      - php70u-fpm
      - php70u-fpm-nginx
      - php70u-common
      - php70u-mysqlnd
      - php70u-opcache
      - php70u-pdo
      #- php70u-mbstring
    
    # need use 'www-data' on Debian8.
    php_owner: nginx
    php_group: nginx

### Note

1. If you see some error message, maybe you need modify `php_owner` and `php_group` from **nginx** to **www-data**. 

 * Browser:
 
     > `An error occurred.`

 * error.log:

     > `connect() to unix:/var/run/php/php7.0-fpm.sock failed (13: Permission denied) while connecting to upstream ...` 

2. The `/target/path/` of **socket**, configure files is difference on Ubuntu and CentOS. **Be careful your Nginx setting !**

 * Debian & Ubuntu:
      * Configure:
         * `/etc/php/7.0/fpm/php.ini`
         * `/etc/php/7.0/cli/php.ini`
     * Socket: `/var/run/php/php7.0-fpm.sock`

 * CentOS:
     * Configure:
         * `/etc/php-fpm.d/www.conf`
         * `/etc/php.ini`
     * Socket: `/run/php-fpm/www.sock`

## Dependencies

None.

> By the way, if you need to setup nginx, you can use [williamyeh.nginx](https://galaxy.ansible.com/williamyeh/nginx/) role.

## Example Playbook

    - hosts: webservers
      roles:
        - { role: chusiang.php7 }

## License

Copyright (c) chusiang from 2016 under the MIT license.
