# Ansible Runner Execution Environment

This repository contains a GitHub Actions workflow to build and publish a custom Ansible execution environment based on the official Ansible Runner container image.

## Overview

The Ansible Runner container is being deprecated in favor of Ansible Builder and execution environments. This repository provides a simple way to create and maintain your own execution environment with custom dependencies and system packages.

## What's Included

- GitHub Actions workflow to automatically build and push the container image
- Configuration for a custom Ansible execution environment
- System package dependencies via bindep.txt
- Python and Ansible Galaxy dependencies

## How to Use This Image

Pull the image from GitHub Container Registry:

```bash
docker pull ghcr.io/OWNER/ansible-runner:latest
```

Run a playbook with the execution environment:

```bash
docker run --rm -v $(pwd):/runner ghcr.io/OWNER/ansible-runner:latest ansible-playbook playbook.yml
```

## Using in Your Own Repository

To build this image in your own GitHub repository:

1. Fork this repository or copy the workflow file to your project
2. Ensure your repository has permission to create packages
3. The workflow will automatically run on pushes to the master branch
4. You can also manually trigger the workflow from the Actions tab

Your image will be available at `ghcr.io/YOUR-USERNAME/ansible-runner:latest`

## Customization

### System Packages

Edit `bindep.txt` to add or remove system packages:

```
# System packages required
iproute
git
curl
openssh-clients
rsync
# Add your packages here
```

### Python Dependencies

Edit `requirements.txt` to add Python packages:

```
# Example
requests>=2.25.0
boto3>=1.18.0
```

### Ansible Collections

Edit `requirements.yml` to add Ansible collections:

```yaml
---
collections:
  - name: ansible.posix
  - name: community.general
  # Add your collections here
```

## Building Locally

You can build the execution environment locally:

1. Install Ansible Builder:
   ```bash
   pip install ansible-builder
   ```

2. Build the execution environment:
   ```bash
   ansible-builder build -t ansible-runner:latest
   ```

## Why Use This?

- **Reproducible environments**: Ensure consistent Ansible execution across different systems
- **Dependency management**: Package all dependencies in a single container
- **CI/CD integration**: Easy to integrate with your existing CI/CD pipelines
- **Simplified transition**: Move from Ansible Runner to the newer execution environment model

## Contributing

Contributions are welcome! Feel free to fork this repository and submit pull requests.

## License

MIT

---

*Note: This repository provides a starting point for creating custom Ansible execution environments. Fork it and customize it to fit your specific needs.*