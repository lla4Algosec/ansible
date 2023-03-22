asms-application-new-application
=========

Automatic application deployment into Algosec AppViz module.  

Requirements
------------

At least 2 files are mandatory.

- asms-credential.yml:  
  File hold sensible data used on authentication and few others optional. (It is recommended to vault this file on production)  

  Setup the 3 following variables to join the ASMS.  
  asms_server: 172.16.73.175  
  asms_username: admin  
  asms_password: algosec  

- asms-application-data.yml:  
  File hold application meta data that describe the application content such as : name, critically, flows, ....  

Playbook/roles are executed locally so an https connectivity in between Ansible server and ASMS server is required.   

Role Variables
--------------

The is no settable variables for this role. All is done on playbook.

Dependencies
------------

The uri role is used and part of the default available roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - name: ASMS Create application
      hosts: localhost
      gather_facts: no

    pre_tasks:
    - name: ASMS load credential vars and vault
      include_vars:
        file: asms-credential.yml

    - name: Load ASMS network objets definition
      include_vars:
        file:
      when: asms_application_with_Network_Objects_and_services

    - name: Load ASMS services definition
      include_vars:
        file:
      when: asms_application_with_Network_Objects_and_services

    - name: ASMS load application definition
      include_vars:
        file: asms-application-data.yml

    roles:
    - { role: asms-application-new-network-objects,
        when: asms_application_with_Network_Objects_and_services }

    - { role: asms-application-new-services,
        when: asms_application_with_Network_Objects_and_services }

    - asms-application-new-application  


License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
