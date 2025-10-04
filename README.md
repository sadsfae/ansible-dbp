# ansible-dbp
Gather all the `/dev/disk/by-path` across all your hosts and generate a YAML report

[![GHA](https://github.com/sadsfae/ansible-dbp/actions/workflows/ansible-lint.yml/badge.svg)](https://github.com/sadsfae/ansible-dbp/actions)

## Requirements
* Python 2.7 or above on your remote hosts

## Usage

* Add your hosts
```bash
vim hosts
```
* Run it to generate `disk_paths_report.yml`
```bash
ansible-playbook -i hosts disk_by_path.yml
```
>[!NOTE]
> If you do not have [root ssh keys copied](https://github.com/sadsfae/ansible-sshkeys) you can pass root password via `-e`
>

```bash
ansible-playbook -i hosts disk_report_playbook.yml -e "root_password='your_password'"
```
## Example Report

```yaml
e43-h11-000-r650.example.com:
    nvme0n1: /dev/disk/by-path/pci-0000:65:00.0-nvme-1
    sda: /dev/disk/by-path/pci-0000:67:00.0-scsi-0:2:0:0
    sdb: /dev/disk/by-path/pci-0000:67:00.0-scsi-0:2:1:0
    sdc: /dev/disk/by-path/pci-0000:67:00.0-scsi-0:2:2:0
e43-h13-000-r650.example.com:
    nvme0n1: /dev/disk/by-path/pci-0000:65:00.0-nvme-1
    sda: /dev/disk/by-path/pci-0000:67:00.0-scsi-0:2:0:0
    sdb: /dev/disk/by-path/pci-0000:67:00.0-scsi-0:2:2:0
    sdc: /dev/disk/by-path/pci-0000:67:00.0-scsi-0:2:1:0
```
