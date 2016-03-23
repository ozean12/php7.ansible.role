# Ansible Role: PHP7

An Ansible role that installs and configure PHP 7 on Debian/Ubuntu servers.

Current PHP7 version: **7.0.4**

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    php_ppa: "ppa:ondrej/php"    
    php_packages:
      - php7.0-common
      - php7.0-cli
      - php7.0-intl
      - php7.0-curl
      - php7.0-cgi
      - php7.0-fpm
      - php7.0-mysql
      - php7.0-gd
    php_timezone: Asia/Taipei
    php_upload_max_filesize: "20M"
    php_post_max_size: "20M"
    php_memory_limit: "1024M"
    php_owner: www-data
    php_group: www-data

### Note

If you see some error message, maybe you need modify `php_owner` and `php_group` from **www-data** to **nginx**. 

* Browser:
 
 > `An error occurred.`

* error.log:

 > `connect() to unix:/var/run/php/php7.0-fpm.sock failed (13: Permission denied) while connecting to upstream ...` 


## Dependencies

None.

## Example Playbook

    - hosts: webservers
      roles:
        - { role: chusiang.php7 }

## License

MIT