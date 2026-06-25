FROM mcr.microsoft.com/devcontainers/python:3.12

ENV DEBIAN_FRONTEND=noninteractive
ENV ANSIBLE_COLLECTIONS_PATHS=/usr/share/ansible/collections

# Install minimal system deps and Ansible + collections so the image is ready-to-use
RUN apt-get update \
  && apt-get install -y --no-install-recommends git curl unzip \
  && rm -rf /var/lib/apt/lists/* \
  && python3 -m pip install --upgrade pip \
  && pip install --no-cache-dir ansible-core boto3 botocore passlib \
  && curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o /tmp/awscliv2.zip \
  && unzip /tmp/awscliv2.zip -d /tmp \
  && /tmp/aws/install --update \
  && rm -rf /tmp/aws /tmp/awscliv2.zip \
  && mkdir -p /usr/share/ansible/collections \
  && ansible-galaxy collection install -p /usr/share/ansible/collections community.general community.aws amazon.aws ansible.posix

CMD ["sleep", "infinity"]
