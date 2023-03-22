asms-application-new-network-objects
=========

Automatic Network objects deployment into Algosec AppViz module.  

Requirements
------------

At least 2 files are mandatory.  

- asms-credential.yml    
  File holds sensitive data used for authentication. It is strongly recommended to use vault for this file on production environnements.  

  Setup the 3 following variables allow making changes to the AlgoSec server:    
  asms_server: 172.16.73.175  
  asms_username: admin  
  asms_password: algosec  

- asms-application-network-objects-data.yml  
  File holds network objects meta data that describes the network objects content such as : name, IP, type, ....  

Playbook/roles are executed locally so an https connectivity in between Ansible server and ASMS server is required.   

Role Variables
--------------

The is no settable variables for this role. All is done on playbook.

Dependencies
------------

The uri role is used and part of the default available roles.

Example Playbook
----------------

    - name: Create application network objects
      hosts: localhost
      gather_facts: no

      pre_tasks:
        - name: Load ASMS credential vars (vault capable)
          include_vars:
            file: asms-credential.yml

        - name: Load ASMS network objets definition
          include_vars:
            file: asms-application-network-objects-data.yml

      roles:
        - asms-application-new-network-objects



License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
