# ansible-role-kubectl

Ansible role to install `kubectl` and optionally enable Bash autocompletion.

## Role Description

This role downloads the Kubernetes `kubectl` binary for the current host architecture and installs it as a symlink in `/usr/local/bin`. It also supports configuring Bash completion for `kubectl`.

## Requirements

- Ansible 2.1 or newer
- A Linux host (tested on Ubuntu and Debian based systems)
- Network access to `https://dl.k8s.io`

## Role Variables

The following variables are defined in `defaults/main.yaml`:

| Variable                   | Required | Default                                                               | Description                                      |
|----------------------------|----------|-----------------------------------------------------------------------|--------------------------------------------------|
| `kubectl_version`          | no       | `v1.36.3`                                                             | Kubernetes `kubectl` release to install          |
| `kubectl_checksum_url`     | no       | `sha512:https://dl.k8s.io/release/{{ kubectl_version }}/bin/{{ ansible_facts['system'] \| lower }}/{{ _arch }}/kubectl.sha512` | Checksum URL for the `kubectl` binary            |
| `kubectl_download_url`     | no       | `https://dl.k8s.io/release/{{ kubectl_version }}/bin/{{ ansible_facts['system'] \| lower }}/{{ _arch }}/kubectl` | Download URL for the `kubectl` binary            |
| `kubectl_download_dir`     | no       | `/opt/`                                                               | Directory where `kubectl` is downloaded          |
| `kubectl_install_dir`      | no       | `/usr/local/bin/`                                                     | Final install directory for the `kubectl` symlink|
| `kubectl_owner`            | no       | `root`                                                                | Owner for the downloaded `kubectl` binary         |
| `kubectl_group`            | no       | `root`                                                                | Group for the downloaded `kubectl` binary         |
| `kubectl_mode`             | no       | `777`                                                                 | Permissions mode for the downloaded `kubectl`     |
| `kubectl_autocompletion`   | no       | `true`                                                                | Enable Bash autocompletion for `kubectl`         |

## Example Playbook

```yaml
- hosts: all
  become: true
  roles:
    - name: pabichs.kubectl
```

## License

BSD / MIT

## Author

Sebastian Pabich
