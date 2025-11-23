# How To

## Fix for libvirt permissions
$ echo 'security_driver = "none"' | sudo tee -a /etc/libvirt/qemu.conf
$ sudo systemctl restart libvirtd

## Cloud Init commands
$ openssl passwd -6 -salt $RANDOM 'foo'

## Terraform commands
$ terraform init
$ terraform plan -out=main.plan
$ terraform apply main.plan -auto-approve
--
$ terraform destroy -auto-approve

## Ansible Setup
$ cd ansible
$ ansible-playbook ansible-playbook_apt-update-upgrade.yaml
$ 

