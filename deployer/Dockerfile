FROM pad92/ansible-alpine:latest

RUN ansible-galaxy install kwoodson.yedit
RUN ansible-galaxy collection install community.general ansible.posix

ADD download-os-image /usr/bin