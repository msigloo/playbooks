# Ubuntu health check playbook

This repository contains an Ansible playbook to perform a routine health check on Ubuntu systems. It reports CPU load, memory usage, and disk usage (root filesystem), and emits simple warnings when thresholds are exceeded.

Files
- `ubuntu_health_check.yml` - Ansible playbook that gathers facts and prints CPU, memory, and storage checks.

Usage

Run the playbook against your target hosts (for example, `localhost`):

```powershell
ansible-playbook -i localhost, -c local ubuntu_health_check.yml
```

Adjust thresholds inside the playbook under the `vars` section:
- `small_disk_threshold_gb` - warn when root available is below this (default: 10 GB)
- `high_load_threshold` - warn when 1-minute load average is above this (default: 1.0)

Notes
- The playbook asserts the host distribution contains "Ubuntu" and will fail otherwise.
- It uses `df` and `/proc/loadavg` for sampling; it's safe and non-invasive (tasks are run with `changed_when: false`).
