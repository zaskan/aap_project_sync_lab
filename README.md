## Ansible Controller Control nodes testing

The code within this repository is experimental and has been developed solely for testing purposes. It is intended to serve as a basis for experimentation and exploration and may contain unfinished features, unstable implementations, or components that are subject to change. Users are advised to proceed with caution when using or modifying the code, as it is not optimized for production environments and may lack thorough testing or full documentation.

### Lab 1 - Upgrade project on every nodes

This lab objective is to test a workaround to synchronize the project code on every control nodes. In order to do that, the playbook disables every nodes, and activates the nodes one by one in a loop and updates the project there. Finally, it enables every node. Theoretically, the jobs running shouldn't be affected, and the project code should be present on every node.
In order to perform the first test, I have executed multiple jobs:

```
for i in {1..50}; do curl -k -X POST https://MY_CONTROLLER_USER:MY_CONTROLLER_PASSWORD@MY_CONTROLLER_HOSTNAME/api/v2/job_templates/MY_JOB_TEMPLATE_ID/launch/; done
```

After that, I launched the main.yml playbook to launch the project sync.
It disable control nodes and only enable the specific ones in which the project is updated. Once it finish every node should have the code and should be enabled.

```
ansible-playbook main.yml -e '{"project_name": "MY_PROJECT_NAME"}'
```

The job templates running, still running and I can't see failures there. Anyways, I need further testing with different scenarios. 

