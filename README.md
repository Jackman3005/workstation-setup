# Run the setup

The fastest way to get off the ground and setup your workstation is to copy the below into your terminal:
```bash
# Stage 1: setup-prep
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Jackman3005/workstation-setup/main/bin/setup-prep)" \
# Stage 2: ansible-setup
 && cd "$HOME/workspace/workstation-setup/" && bin/ansible-setup
```
# Stages
There are two stages to this repo:
 1. Setup Preparation
 2. Setup via Ansible Playbook

Both stages are idempotent and can be repeated multiple times.

## Setup Prep
`setup-prep` ensures the environment is ready to run the Ansible Playbook. It performs the following:
1. Ensures XCode Dev tools are correctly setup
2. Ensures Homebrew is installed
3. Ensures Ansible is installed
4. Clones this repository (if not already cloned) to `~/workspace/workstation-setup`

## Ansible Setup
`ansible-setup` installs the Ansible Roles and runs the playbook.

### Skipping tags
If you are repeating the ansible installation and wish to skip portions that have already
completed successfully. Consider skipping tags, for example:
```bash
ansible-playbook main.yml --ask-become-pass --skip-tags homebrew,sdkman
```

Tags for tasks and roles can be found in [main.yml](main.yml). Ansible first runs through
all roles in the order listed and then through all tasks in the order listed.

All tags can be printed by running `ansible-playbook main.yml --list-tags`.
However, some tags are internal to a role, so choose tags carefully.

__Once all issues have been sorted I recommend running the whole playbook without skipping tags to ensure everything is good to go.__



### Credits
This repo is highly inspired from the [Mac Dev Playbook](https://github.com/geerlingguy/mac-dev-playbook) by Jeff Geerling
