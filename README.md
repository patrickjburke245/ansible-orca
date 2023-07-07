# Ansible with Orca

Ansible Playbook and Role in for deploying ThreatOptix on a Linux VM.

You'll need to create an API token in the Orca Security UI, and place that in /roles/common/vars/main.yml for this playbook and role to work.

## Variables

| Variable | Description |
| -------  | ----------- |
| api_url  | This represents the API URL that will be used for downloading the ThreatOptix agent. Note that each Orca Region will require a different API location. The US region will look like this api.orcasecurity.io/api/threatoptix/download?agent_type=vm Note the agent_type parameter being passed to the URL |
| api_key | This is the Orca API KEY that will be used to authenticate against the Orca API. All requests to the Orca API must be authenticated. |

## Defaults

A number of the variables have defaults set. Sensible defaults have been used.
It is possible to change the defaults by editing them, or simply overriding them with variables.

| Variable | Default | Description |
| -------- | ------- | ----------- |
| destination_directory | Yes | /opt/ThreatOptix/ |
| install_prerequisites | Yes | Defaults to true - will install unzip if needed |
| agent_name | Yes | ThreatOptix agent |

## ansible.cfg

As this repo contains both a role and an example playbook, it is important to note that not all operating systems are created equally. If you are using public cloud, then depending on the OS that you use, you will need to log in as a different user depending on the OS. Typically, ubuntu uses "**ubuntu**", amazon linux uses "**ec2-user**" and so on. To avoide this, we have provided a sample **ansible.cfg** that allows you to simply change the remote user and the private key file. 

If you are using Ansible Tower, or AWX, then credentials should be passed to the role using within the definition.


# Running the role / playbook

ansible-playbook --extra-vars "api_key=MY_KEY" playbook.yml
