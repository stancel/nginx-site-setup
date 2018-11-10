nginx_site_setup
=========

Ansible role that sets up one or more new virtual hosts on an NginX webserver.

Requirements
------------

You'll need to have NginX already setup and working on the server you are running this role on.

Role Variables
--------------

Sites to setup and host on the webserver
```
	nginx_site_setup_sites_to_set_up:
	  - {
		  url: 'mysite.com',
		  name: 'mysite',
		  nginx_server_name: 'mysite.comm www.mysite.com',
		  https: true
		}
```

The NginX client max body size. The default is 10m.
```
	nginx_site_setup_nginx_server_client_max_body_size: 10m
```

The document root for the webserver. The default value is "/var/www"
```
	nginx_site_setup_web_home: "/var/www"
```

The name of the folder created under each website folder that holds the files NginX will serve up in its server block. The default is "www". If this is used with Bedrock WordPress then it should be changed to "web".
```
	nginx_site_setup_site_subfolder_used_to_serve_files: "www"
```

The linux username used by your webserver. The default value is "www-data"
```
	nginx_site_setup_web_user: "www-data"
```

The linux group used by your webserver. The default value is "www-data"
```
	nginx_site_setup_web_group: "www-data"
```


Dependencies
------------

None

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

	- hosts: your_webserver
	  vars_files:
	    - vars/main.yml
	  roles:
	    - stancel.nginx_site_setup 

or just pass the variables in the playbook

	- hosts: your_webserver 
	  vars:
        nginx_site_setup_sites_to_set_up:
          - {
              url: 'mysite.com',
              name: 'mysite',
              nginx_server_name: 'mysite.comm www.mysite.com',
              https: true
		    }
	  roles:
	    - stancel.nginx_site_setup

License
-------

GPLv3

Author Information
------------------

[Brad Stance](https://github.com/stancel)


