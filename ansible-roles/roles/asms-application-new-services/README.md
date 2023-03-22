asms-application-new-services
=========

Automatic services deployment into Algosec AppViz module.  

Requirements
------------

At least 2 files are mandatory.

- asms-credential.yml:  
  File hold sensible data used on authentication and few others optional. (It is recommended to vault this file on production)  

  Setup the 3 following variables to join the ASMS.  
  asms_server: 172.16.73.175  
  asms_username: admin  
  asms_password: algosec  

- asms-application-services-data.yml:  
  File hold services meta data that describe the application content such as : name, port, protocol, ....  

Playbook/roles are executed locally so an https connectivity in between Ansible server and ASMS server is required.   

Role Variables
--------------

The is no settable variables for this role. All is done on playbook.

Dependencies
------------

The uri role is used and part of the default available roles.

Example Playbook
----------------

    - name: Create application services
      hosts: localhost
      gather_facts: no

      pre_tasks:
        - name: Load ASMS credential vars (vault capable)
          include_vars:
            file: asms-credential.yml

        - name: Load ASMS services definition
          include_vars:
            file: asms-application-services-data.yml

      roles:
        - asms-application-new-services


License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
