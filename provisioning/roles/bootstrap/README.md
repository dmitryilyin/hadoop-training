Role BOOTSTRAP
==============
OS-family independent
Install commonly used software

Example of a playbook:

````yml
    ---
    # Bootstrap
    - hosts: localhost
      connection: local
      gather_facts: true
      roles:
        - { role: bootstrap,
            tags: bootstrap,
            become: yes,
            become_method: sudo
          }
````

