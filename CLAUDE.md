# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is an **Ansible Collection** named `devoping_us.workstation_setup` (version 1.0.0, GPL-2.0-or-later). Its purpose is workstation setup automation — provisioning developer machines with tools, configurations, and dependencies.

## Common Commands

```bash
# Build the collection tarball
ansible-galaxy collection build

# Install the collection locally for testing
ansible-galaxy collection install devoping_us-workstation_setup-*.tar.gz --force

# Install dependencies (if any defined in galaxy.yml)
ansible-galaxy collection install -r requirements.yml

# Lint roles and playbooks
ansible-lint

# Run molecule tests for a role (from within a role directory)
molecule test

# Run a specific molecule scenario
molecule test -s <scenario_name>

# Syntax check a playbook
ansible-playbook --syntax-check playbooks/<playbook>.yml

# Run a playbook against localhost
ansible-playbook playbooks/<playbook>.yml -i localhost, --connection=local
```

## Collection Structure

```
workstation_setup/          # Collection root
├── galaxy.yml              # Collection metadata (namespace, name, version, dependencies)
├── meta/runtime.yml        # Ansible runtime config (plugin routing, redirect rules)
├── roles/                  # Ansible roles go here (each role = subdirectory)
├── plugins/                # Custom modules, filters, callbacks, etc.
├── playbooks/              # Playbooks (not yet created)
└── docs/                   # Additional documentation
```

### Role layout convention (when roles are added)

```
roles/<role_name>/
├── tasks/main.yml
├── defaults/main.yml       # Default variable values
├── vars/main.yml           # Non-overridable variables
├── handlers/main.yml
├── templates/              # Jinja2 templates
├── files/                  # Static files
└── meta/main.yml           # Role metadata and dependencies
```

## Key Files

- **galaxy.yml** — Collection namespace (`devoping_us`), name, version, and build config. Update author/description/URLs before publishing.
- **meta/runtime.yml** — Plugin routing and import redirects; currently has commented-out examples.

## Development Notes

- The collection namespace is `devoping_us` and collection name is `workstation_setup`. When referencing roles from a playbook: `devoping_us.workstation_setup.<role_name>`.
- `ansible-lint` configuration can be added as `.ansible-lint` at the collection root.
- Molecule is the standard testing framework for Ansible roles; add a `molecule/` directory inside each role.
