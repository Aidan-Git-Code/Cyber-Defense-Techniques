# Cyber-Defense-Techniques
Assignment Repository for CDT

## Assignment 2 – Privileged Docker container (SSH access)

The playbook deploys a **privileged** Docker container. By default **SSH is enabled** so Blue/Red team can SSH into the container, then perform the host filesystem mount escape from inside.

- **SSH:** port `2222` on the deployment host (maps to container port 22).
- **Credentials:** `blueteam` / `blueteam` (set in `roles/vulnerable_docker/defaults/main.yml`: `vuln_docker_ssh_user`, `vuln_docker_ssh_password`).

Example:
```bash
ssh -p 2222 blueteam@<deployment-host-ip>
# Then from inside the container: mount host root and escape (see docs/EXPLOITATION.md).
```

To disable SSH and use only `docker exec` from the host, set in `group_vars/all.yml` or extra vars: `vuln_docker_enable_ssh: false`.
