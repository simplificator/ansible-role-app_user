FROM debian:9

RUN apt-get update && apt-get install -y python-pip
RUN pip install ansible

ADD . /etc/ansible/roles/app_user

ADD test/ .

RUN ansible-playbook --connection=local provision-test.yml