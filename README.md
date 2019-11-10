set_proper_site_permissions
=========

This role is primarily meant to be used with the personal_webserver and documentation_webserver templated playbooks created by Brad Stancel for personal and business uses. The purpose of the role is to make sure that the Linux file permissions are set properly in order to reduce the likelihood of a security related event happening and encourage best practices. The reason I separated it into a role outside of those playbooks is so I can read a list of sites and paths hosted on a shared webserver and run this role independently from those playbooks. This will allow me to run this on a timed basis (cron job) and cover multiple different shared webserver instances.

Requirements
------------

This role is dependent on having websites folders structured in the same way that roles like [stancel.nginx_site_setup](https://galaxy.ansible.com/stancel/nginx_site_setup) setup the folders for the sites that it sets up.

Role Variables
--------------

Sites list used to iterate through and set proper permissions on. Required.

```
set_proper_site_permissions_site_list:
  - {
      name: 'mysite',
      site_subfolder_used_to_serve_files: "current/build/html"
    } 
```

The document root for the webserver. The default is "/var/www"

```
set_proper_site_permissions_web_home: "/var/www"
```

The name of the folder created under each website folder that holds the files the webserver uses as the document root for this site. If this is used with Bedrock WordPress then it should be changed to "web" or "current/web". The default is "www"

```
set_proper_site_permissions_site_subfolder_used_to_serve_files: "www"
```

The name of the folder created under each website folder that holds the files NginX will serve up in its server block. If this is used with Bedrock WordPress then it should be changed to "web". The default is "www"

```
set_proper_site_permissions_site_subfolder_used_to_serve_files: "www"
```

The Linux group used by your webserver. The default value is "www-data"

```
set_proper_site_permissions_webserver_web_group: "www-data"
```

Dependencies
------------

stancel.nginx_site_setup

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```
	- hosts: your_webserver
	  vars_files:
	    - vars/main.yml
	  roles:
	    - stancel.set_proper_site_permissions
```

License
-------

GPLv3

Author Information
------------------

[Brad Stance](https://github.com/stancel)
