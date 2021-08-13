## Ansible AWS Playbooks
### Install Prerequisites
`sudo apt-get install python3-pip`
`sudo pip3 install boto boto3`
`sudo pip3 install boto botocore`
### Keys for AWS
- Head over to your .ssh folder and create .pub and .pem keys
- `ssh-keygen -t rsa -b 2048 -v -f eng89_salem_ans`
- `mv eng89_salem_ans eng89_salem_ans.pem` to add the .pem extension
- `chmod 400 eng89_salem_ans.pem`
- `chmod 600 eng89_salem_ans.pub`
### Ansible-Vault
- Create a folder in `/etc/ansible/` called "group_vars" and within another called "all"
- `export EDITOR=nano`
- cd inside and run `sudo -E ansible-vault create pass.yml`
- enter "aws_secret_key:" and "aws_access_key:" and fill in the data
- To ever edit the keys again run this: `sudo -E ansible-vault edit pass.yml`
### Creating EC2 Instances
- Run the command `sudo ansible-playbook {playbook_name}.yml --ask-vault-pass --tags create_ec2 -v` to create an instance
- Add the public instances to the hosts folder under a named group like so: `ubuntu ansible_host=54.154.244.171 ansible_user=ubuntu ansible_ssh_private_key_file=~/.ssh/eng89/eng89_salem_ans.pem`
- Try pinging to the instance: `sudo ansible aws -m ping --ask-vault-pass`
- If that was successful then try SSHing inside: `ssh -i "~/.ssh/eng89/eng89_salem_ans.pem" ubuntu@54.154.244.171`
