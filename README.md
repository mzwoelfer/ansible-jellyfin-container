# Jellyfin container install

Installs a containerized Jellyfin instance on a Debian server using docker compose.

[Jellyfin](https://github.com/jellyfin/jellyfin): A free and open-source media server.
Think self-hosted Netflix.

Tested on:
- Debian 12

## Requirements
- Container runtime: `docker` or `nerdctl`.

## Variables
See: [defaults/main.yaml](defaults/main.yaml)

## Installation
Create a `roles/requirements.yaml`:
```YAML
- src: https://github.com/mzwoelfer/ansible_jellyfin_container.git
  name: ansible_jellyfin_container 
  scm: git
  version: main
```

Run a minimal playbook against your Jellyfin server:
```YAML
- hosts: jellyfin_server
  roles:
    - role: ansible_jellyfin_container
      become_user: "{{ ansible_user }}"
```

Access and setup Jellyfin in your browser under `<SERVER-ADDRESS>:8096`

## Example Playbook
Installs latest Jellyfin app via `nerdctl` with the `ansible_user` user
```YAML
- hosts: jellyfin_server
  roles:
    - role: ansible_jellyfin_container
      become: false
      become_user: "{{ ansible_user }}"
      vars:
        container_runtime: "nerdctl"
```

## Usage:
- Access Jellyfin in your browser on `http://localhost:8096`.
- Store movie in `~/jellyfin/media`

## LICENSE
MIT
