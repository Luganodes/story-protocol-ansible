# Story Protocol Ansible Automation

## Overview

This Ansible collection provides comprehensive automation for deploying, managing, and maintaining Story protocol network nodes. The playbooks support seamless network participation, configuration, and maintenance across multiple systems.

## Features

- 🌐 Network Joining
  - Automated Cosmovisor setup
  - Simplified network integration

- 🔒 Security Configuration
  - Firewall rule management
  - Secure node deployment

- 📦 Snapshot Synchronization
  - Efficient network state download
  - Parallel snapshot retrieval
  - Easy node synchronization

- 🔄 Node Management
  - Binary upgrades
  - Service maintenance
  - Flexible configuration

## Prerequisites

### System Requirements
- Operating System: Debian-based Linux distributions (recommended)
- Python 3.x
- Ansible 2.10+

### Recommended Hardware
- CPU: 4+ cores
- RAM: 16GB+
- Storage: 500GB SSD
- Network: Stable internet connection (25 MBit/s or more)


## Quick Start Guide

### 1. Repository Setup
```bash
git clone https://github.com/your-repo/story-protocol-ansible.git
cd story-protocol-ansible
```

### 2. Configuration
Edit the inventory file in `inventory/story.yaml` with your specific node details:
- Node moniker
- Network configuration
- Binary URLs
- Snapshot sources

### 3. Network Joining
```bash
ansible-playbook playbook/join_network.yaml -i inventory/story.yaml
```

### 4. Verify Synchronization
```bash
# Check Geth service logs
journalctl -afu geth 

# Check Cosmovisor logs
journalctl -afu cosmovisor
```

## Advanced Operations

### Snapshot Synchronization

#### Download Snapshots
```bash
ansible-playbook playbook/snapshot_download.yaml -i inventory/story.yaml
```

#### Check Snapshot download status
```bash
ansible-playbook playbook/snapshot_check.yaml -i inventory/story.yaml
```

#### Extract Snapshots
```bash
ansible-playbook playbook/snapshot_extract.yaml -i inventory/story.yaml
```

> **Note**: During a fresh installation using snapshots, you may encounter a critical initialization error where Cosmovisor fails to locate the latest upgrade binary. This typically occurs when the node's upgrade directory structure is not properly established before snapshot restoration:
> ```bash
> ansible-playbook playbook/fix_snapshot_first.yaml -i inventory/story.yaml
> ```

### Binary Upgrades

#### Upgrade Geth
1. Update `story_geth_binary_url` and `story_geth_binary_version`
```bash
ansible-playbook playbook/upgrade_geth.yaml -i inventory/story.yaml
```

#### Upgrade Story Node
1. Update `story_node_binary_url`, `story_node_binary_version`, and `story_node_upgrade_height`
```bash
ansible-playbook playbook/upgrade_node.yaml -i inventory/story.yaml
```

## Configuration Example

```yaml
story:
  vars:
    moniker: story-protocol-node
    network_name: odyssey
    # ... (other configuration parameters)
  
  hosts:
    story-protocol-testnet-node-1: 
      ansible_host: story-protocol-testnet-node-1
      ansible_user: debian
```

## Best Practices

- Always backup your node configuration before major upgrades
- Monitor system resources during synchronization
- Use stable and reliable snapshot sources
- Keep Ansible and dependencies updated

## Troubleshooting

- Verify network connectivity
- Check Ansible version compatibility
- Ensure proper permissions for service management
- Review logs for specific error messages

## Contributing

Contributions are welcome! Please submit pull requests or open issues for improvements and bug fixes.

## License

[MIT License](LICENSE)

## Support

For additional support, please open an issue in the GitHub repository or contact the maintainers.