# ansible-dbp
Gather all the `/dev/disk/by-path` across all your hosts and generate a YAML report

[![GHA](https://github.com/sadsfae/ansible-dbp/actions/workflows/ansible-lint.yml/badge.svg)](https://github.com/sadsfae/ansible-dbp/actions)

## Host Requirements
* Only an accessible SSH service is required on remote hosts.
* This should even work on systems without Python installed like appliances.

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
* A file is generated every run called `disk_paths_report.yml`

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

## Performance
* Because this does not collect Ansible facts it's pretty fast.
* In testing it takes about _34 seconds_ for 100+ hosts.
* Adjusting Ansible [forks](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_strategies.html#setting-the-number-of-forks) may significantly speed up the process further.
