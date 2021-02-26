# ubuntu-wsl-setup

Cấu hình ubuntu wsl2, cài đặt các gói cấu hình

## Pre-setup

    sudo apt update
    sudo apt install software-properties-common
    sudo apt-add-repository --yes --update ppa:ansible/ansible
    sudo apt install ansible

    sudo service ssh restart
    sudo dpkg-reconfigure openssh-server
    sudo cp ./ansible.cfg /etc/ansible/ansible.cfg

## Test ping

    ansible -i hosts self -m ping

## Install provision

    ansible-playbook -i hosts -l self provision.yml  --vault-password-file=vault.txt
    ansible-playbook -i hosts -l self provision.yml  --vault-password-file=vault.txt --tags common
    ansible-playbook -i hosts -l self provision.yml  --vault-password-file=vault.txt --tags docker

## Automatically start the docker daemon on wsl2

    sudo visudo
    user ALL=(ALL) NOPASSWD: /usr/bin/dockerd

    echo '# Start Docker daemon automatically when logging in if not running.' >> ~/.bashrc
    echo 'RUNNING=`ps aux | grep dockerd | grep -v grep`' >> ~/.bashrc
    echo 'if [ -z "$RUNNING" ]; then' >> ~/.bashrc
    echo '    sudo dockerd > /dev/null 2>&1 &' >> ~/.bashrc
    echo '    disown' >> ~/.bashrc
    echo 'fi' >> ~/.bashrc
