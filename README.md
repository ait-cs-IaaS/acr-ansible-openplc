# Ansible-Role: acr-ansible-openplc

AIT-CyberRange: Installs and configures openplc. 


## Requirements

- Debian or Ubuntu 

## Role Variables

```yaml
openplc_branch: master
# defaults file for openplc
openplc_restart_sleep_seconds: 60 # amount of time to sleep before starting the service when restarting
openplc_install_force: false
openplc_deploy_dir: /opt/OpenPLC_v3
openplc_st_files: [] # List of files
openplc_config_files: [] # List of dicts: src, dest
openplc_config_templates: [] # List of dicts: src, dest
openplc_users: [] # list of user dicts
openplc_user: openplc

openplc_users_csv_template: users.csv.j2
openplc_users_csv_template_dest: /tmp/openplc_users.csv

openplc_hardware_layer: psm_linux
openplc_hardware_layer_md5:
  "{{ (openplc_hardware_layer + '\n') | hash('md5') }}"
```

## Example Playbook

```yaml
- hosts: localhost
  roles:
    - acr-ansible-openplc
      vars:
        openplc_active_program: 124677.st
        openplc_st_files:
          - src: 'files/openplc/ladder_logic.st'
            dest: '{{ openplc_active_program }}'
        openplc_config_files:
          - src: files/openplc/mbconfig.cfg
            dest: webserver/mbconfig.cfg
          - src: files/openplc/openplc.db
            dest: webserver/openplc.db
          - src: files/openplc/psm_app.py
            dest: webserver/core/psm/main.py
```

## License

GPL-3.0

## Author
- David Mark Allison
- Lenhard Reuter