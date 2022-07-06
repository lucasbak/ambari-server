Ansible Ambari Server
=========

A simple role for setting up Apache Ambari Aserver

Requirements
------------

JAVA
MariaDB / PostgreSQL Database

Role Variables
--------------

The following variables are used by this role and values are defined in defaults/main.yml:

ambari_database: ambari_db                              ## the name of the database used by ambari
ambari_database_user: ambari_db_user                    ## the name of the database' user used by ambari
ambari_database_user_password: ambari_db_password       ## the password of the ambari user database
ambari_ssl: True                                        ## set to True if you want to enable TLS on ambari web console
ambari_ssl_port: 8442                                   ## ambari server ui port
mysql_server_hostname: master01.clemlab.com             ## mysql/MariaDB hostname
mysql_server_port: 3306                                 ## mysql/MariaDB port
ambari_master_key: masterkey                            ## Ambari's Vault Master Key
ssl_cert_folder: /etc/ssl/                              ## Folder containing certificates
ssl_stores_path: /etc/security/serverKeys               ## Folder containing keystores
truststore_password: password                           ## Ambari truststore password keystores
java_home: /usr/java/default                            ## JAVA Home folder

Example Playbook
----------------

Here is an example playbook that can readily wrap this role and still be fairly flexible.  You typically don't need to be this flexible on password source.

- hosts: master01.clemlab.com
  gather_facts: no
  vars_files:
  - vars/external_vars_dev.yml
  - vaults/vault-dev.yml

  roles:
    - role: ambari-server
      tags: ambari_server
      vars:
        ambari_database: "{{ ambari_server_database }}"
        ambari_database_user: "{{ ambari_server_database_user }}"
        ambari_database_user_password: "{{ ambari_server_database_user_password }}"
        ambari_ssl: "{{ ambari_server_ssl }}"
        ambari_ssl_port: "{{ ambari_server_ssl_port }}"
        mysql_server_hostname: "{{ mariadb_server }}"
        mysql_server_port: 3306
        ambari_master_key: "{{ ambari_server_master_key }}"
        ssl_cert_folder: "{{ security_ssl_cert_folder }}"
        ssl_stores_path: "{{ security_server_ssl_stores }}"
        truststore_password: "{{ security_truststore_password }}"
        java_home: /usr/lib/jvm/java

License
-------

GPLv2

Author Information
------------------

https://github.com/lucasbak/
https://github.com/ymadoff/
