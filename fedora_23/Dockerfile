
FROM fedora:23
MAINTAINER "Andrew Rothstein" andrew.rothstein@gmail.com

# install ansible
RUN dnf update -y && dnf install -y python2 python2-dnf libselinux-python python-pip && pip install --upgrade pip && pip install ansible==1.9.1
RUN ansible --version

# configure ansible to target the localhost -- inside the container
ADD ansible.cfg /etc/ansible/ansible.cfg
ADD localhost /etc/ansible/hosts
RUN ansible '*' -m ping

# embed roles
ONBUILD ADD requirements.yml requirements.yml
ONBUILD RUN ansible-galaxy install -r requirements.yml

# execute playbook to configure container to suit
ONBUILD ADD playbook.yml playbook.yml
ONBUILD RUN ansible-playbook playbook.yml