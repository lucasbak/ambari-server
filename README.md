java_keystore
=========

A simple role for setting up Keystore and Truststore used in HDP

Requirements
------------

Primarily tested and functional on CentOS 7, but open to others.

Role Variables
--------------

The following variables are used by this role and values are defined in defaults/main.yml:

java_keystore_path: /etc/security/serverKeys        # Path where to store keystores
java_keystore_keystore_password: keystore123        # Keystore password
java_keystore_truststore_password: truststore123    # Truststore password
java_keystore_ca_realm: myRealm                     # Alias that will be used for truststore
java_keystore_cert_folder: /tmp/certs               # Folder that contains all certificates
java_keystore_cacert_name: cacert.pem               # CA certificate file name

Example Playbook
----------------

Here is an example playbook that can readily wrap this role and still be fairly flexible.  You typically don't need to be this flexible on password source.

    - hosts: servers
      vars_files:
        - vars/private.yml
      vars:
        - java_keystore_path: /etc/security/serverKeys 
        
      roles:
         - { role: java_keystore_path }

License
-------

GPLv2

Author Information
------------------

https://github.com/ymadoff/
