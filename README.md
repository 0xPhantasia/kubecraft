# kubecraft
Automated and simple on-premise Kubernetes cluster deployment with Ansible and Helm.

## Prerequisites

You need to have:

- 2 or more running Rocky Linux >=8 hosts, with SSH access to a local sudoer account on each one
- An Ansible ready machine or environment
- Hosts need to be reachable from the Ansible host and between each other on port tcp/22
- No devices or network configuration must prevent the communication between master and worker nodes on the list of ports to be opened, see "k8s_quickstart.yml" for port list
- A DNS server configured to work with the hosts, you can also make it work with /etc/hosts

## Usage

To use that template you can adapt the hosts.yml file to your needs by filling the necessary IP, hostnames and connection informations.

Once the hosts.yml file is populated, you can start the deployment with ```ansible-playbook --verbose k8s_quickstart.yml -i hosts.yaml -e ansible_become_pass=<REMOTE_ACCOUNT_PASS>```

For k8s administration purposes please use the newly created account "kube", **any other account will not work.**

**Note:** The password REMOTE_ACCOUNT_PASS provided must be the one used by the local sudoer account of every VM to be added to the cluster. It will be reused for the "kube" user. That is set to be improved in the future.

## Improvements TODO

- Helm chart support for additional services configuration
- Deployment of ingress controller service
- Automation of Windows DNS round-robin configuration (other DNS solutions to be considered later...)
- Make the playbook 100% idempotent
- Allow for multiple OS compability (Debian, RHEL, Ubuntu ...)
- Support of env variables for credentials usage
- Autoscaling configuration

