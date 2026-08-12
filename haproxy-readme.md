# https://github.com/netvirus/ansible-haproxy/blob/main/ansible/inventory/prod/inventory/haproxy/hosts.yml
ip -br a
useradd -m -s /bin/bash -G sudo ansible
passwd ansible  # P@rkan2000

# on controlnode
ssh-keygen -t ed25519 -C "ansible@itbc.corp" -f ~/.ssh/ansible_itbc.corp
mkdir -p /home/ansible/.ssh
chmod 700 /home/ansible/.ssh/
chown ansible:ansible /home/ansible/.ssh/
vi /etc/sudoers # %sudo   ALL=(ALL:ALL) NOPASSWD:ALL
vi /etc/ssh/sshd_config # PasswordAuthentication yes
ssh-copy-id -i ~/.ssh/ansible_itbc.corp.pub ansible@10.44.24.71
ssh-copy-id -i ~/.ssh/ansible_itbc.corp.pub ansible@10.44.24.72
ssh-copy-id -i ~/.ssh/ansible_itbc.corp.pub ansible@10.44.24.73
ssh ansible@10.44.24.72 -i ansible_itbc.corp # to check passwordless connection
python3 -m venv ansible # use virtual environment
source ansible/bin/activate
pip install ansible
ansible --version

# Apply to itbc
ansible-playbook -i ~/git/vldmrhlushko-project/projects/ansible/inventory/prod/inventory/haproxy/hosts-itbc.yml ~/git/vldmrhlushko-project/projects/ansible/playbooks/host-haproxy.yml --tags=haproxy_config

ansible-playbook -i /home/v/itbc_projects/ansible/inventory/prod/inventory/haproxy/hosts-itbc.yml /home/v/itbc_projects/ansible/playbooks/host-haproxy.yml --tags=haproxy_config



# Apply to Delta
ansible-playbook -i ~/git/vldmrhlushko-project/projects/ansible/inventory/prod/inventory/haproxy/hosts-delta.yml ~/git/vldmrhlushko-project/projects/ansible/playbooks/host-haproxy.yml --tags=haproxy_config



