# Ansible Role: PHP7 (PHP-FPM)

[![Build Status](https://travis-ci.org/chusiang/php7.ansible.role.svg?branch=master)](https://travis-ci.org/chusiang/php7.ansible.role) [![Ansible Galaxy](https://img.shields.io/badge/role-php7-blue.svg)](https://galaxy.ansible.com/chusiang/php7/) [![Docker Hub](https://img.shields.io/badge/docker-php7-blue.svg)](https://hub.docker.com/r/chusiang/php7/) [![](https://images.microbadger.com/badges/image/chusiang/php7.svg)](https://microbadger.com/images/chusiang/php7 "Get your own image badge on microbadger.com")

An Ansible role of Deploy PHP 7 (php-fpm) for nginx on CentOS, Debian, and Ubuntu. (forked from [itcraftsmanpl.php7](https://galaxy.ansible.com/itcraftsmanpl/php7/))

* Current PHP7 version:

 * Debian & Ubuntu: **7.0.6**
 * CentOS: **7.0.5**

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    # All.
    php_version: "7.0"
    php_timezone: Asia/Taipei
    php_upload_max_filesize: "20M"
    php_post_max_size: "20M"
    php_memory_limit: "1024M"
    
    # Debian & Ubuntu.
    debian_php7_apt_repo: "http://packages.dotdeb.org"
    debian_php7_apt_key: "https://www.dotdeb.org/dotdeb.gpg"
    ubuntu_php7_ppa_repo: "ppa:ondrej/php"
    
    apt_php_packages:
      - php{{ php_version }}
      - php{{ php_version }}-cgi
      - php{{ php_version }}-cli
      - php{{ php_version }}-common
      - php{{ php_version }}-curl
      - php{{ php_version }}-fpm
      - php{{ php_version }}-gd
      - php{{ php_version }}-intl
      - php{{ php_version }}-json
      - php{{ php_version }}-mysql
      #- php{{ php_version }}-pear
    
    yum_php_packages:
      - php{{ php_version_yum }}-cli
      - php{{ php_version_yum }}-common
      - php{{ php_version_yum }}-fpm
      - php{{ php_version_yum }}-fpm-nginx
      - php{{ php_version_yum }}-json
      - php{{ php_version_yum }}-mysqlnd
      - php{{ php_version_yum }}-opcache
      - php{{ php_version_yum }}-pdo
      #- php{{ php_version_yum }}-mbstring
      #- php{{ php_version_yum }}-pear
    
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

## Docker Container

This repository contains Dockerized [Ansible](https://github.com/ansible/ansible), published to the public [Docker Hub](https://hub.docker.com/) via **automated build** mechanism.

> Docker Hub: [chusiang/php7](https://hub.docker.com/r/chusiang/php7/)

### Images

* chusiang/php7:ubuntu14.04 (lastest)
* chusiang/php7:centos6

### Usage

    $ docker run -it -v /src:/data chusiang/php7:ubuntu14.04 bash
    [root@a68e807eec8f tmp]# php -v
    PHP 7.0.7 (cli) (built: May 31 2016 11:36:12) ( NTS )
    Copyright (c) 1997-2016 The PHP Group
    Zend Engine v3.0.0, Copyright (c) 1998-2016 Zend Technologies
        with Zend OPcache v7.0.6-dev, Copyright (c) 1999-2016, by Zend Technologies
    

## License

Copyright (c) chusiang from 2016 under the MIT license.
