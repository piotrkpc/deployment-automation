# Redpanda-provision

Utilities to easily provision a [Redpanda](https://vectorized.io) cluster on AWS.

Terraform & Ansible are used to create and manage the nodes and deploy the application.

## Installation Requirements

* Install terraform in your preferred way https://www.terraform.io/downloads.html
* Install Ansible https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html
* `ansible-galaxy install -r ansible/requirements.yml` to gather ansible requirements

## Usage

### Optional Steps: Deploying the VMs

Steps 1-3 are only needed to create new EC2 instances to deploy the redpanda cluster on.
If already created infrastructure is going to be used, they can safely be skipped but you will need to update the `hosts.ini` file with your specific information.

Please refer to each cloud's readme for more information: [AWS](aws/readme.md), [GCP](gcp/readme.md)

### Required Steps: Deploying Redpanda

Before running these steps, verify that the `hosts.ini` file contains the correct information for your infrastructure. This will be automatically populated if using the terraform steps above.
        
1. `ansible-playbook --private-key <your_private_key> -i hosts.ini -v ansible/playbooks/provision-node.yml -e redpanda_packagecloud_token=<your_token_here>

2. Use rpk & standard kafka tool to produce/consume from the redpanda cluster & access the grafana installation on the monitor host.
