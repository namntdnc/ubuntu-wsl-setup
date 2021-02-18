# ubuntu-wsl-setup

Cấu hình ubuntu wsl2, cài đặt các gói cấu hình

## Pre-setup

    sudo service sshd restart

    sudo dpkg-reconfigure openssh-server

    sudo cp ./ansible.cfg /etc/ansible/ansible.cfg

## Test ping

    ansible -i host self -m ping

## Install provision

    ansible-playbook -i host -l self provision.yml  --vault-password-file=vault.txt
