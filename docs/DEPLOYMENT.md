<!-- Deployment documentation - to be filled in after playbook is complete -->

The target hosts are hardcoded and dependent on the cdtecho project environment specifically for the am4052-deploy host and the am4052-vulnerabledocker host, as the ssh key pairing currently only works for those
2 specific hosts

running:
'''ansible-playbook site.yml'''

in the Assignment2 folder results in the setup of the docker container on the remote host.

This will copy the Dockerfile over to the host, build the image there and spin up a container on the remote host, opening port 2222 and allowing the ssh connections to come in.