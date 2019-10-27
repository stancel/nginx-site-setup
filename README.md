nginx_site_setup
================

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
		  https: true,
		  nginx_site_setup_site_subfolder_used_to_serve_files: "current/build/html"
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

Whether this role is being run on a shared webserver. If it is run on a shared webserver then it will expect that the web user is not the same as the web group. The default value is false.

```
	nginx_site_setup_used_on_shared_webserver: false
```

Should the site only be viewable on an intranet, certain IP addresses, or block any IP addresses? The default is false.

```
	nginx_site_setup_restrict_site_to_certain_ip_addresses: false
```

The rules are processed in sequence, from top to bottom.  

``` 
	nginx_site_setup_ip_addresses_or_cidr_ranges_to_allow_or_deny: [
	  "allow 1.2.3.4;",
	  "allow 192.168.1.0/24",
	  "deny all;"
	]
```  

Dependencies
------------

None

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```
	- hosts: your_webserver
	  vars_files:
	    - vars/main.yml
	  roles:
	    - stancel.nginx_site_setup 
```

or just pass the variables in the playbook

```
	- hosts: your_webserver 
	  vars:
        nginx_site_setup_sites_to_set_up:
          - {
              url: 'mysite.com',
              name: 'mysite',
              https: true,
              nginx_site_setup_used_on_shared_webserver: true,
              nginx_site_setup_site_subfolder_used_to_serve_files: "current/build/html",
			  nginx_site_setup_restrict_site_to_certain_ip_addresses: true,
			  nginx_site_setup_ip_addresses_or_cidr_ranges_to_allow_or_deny: [
				"allow 1.2.3.4;",
				"allow 192.168.1.0/24",
				"deny all;"
			  ]
		    }
	  roles:
	    - stancel.nginx_site_setup
```

License
-------

GPLv3

Author Information
------------------

[Brad Stance](https://github.com/stancel)
