# Privileged container with SSH for competition (Blue/Red team access).
# Build args set from Ansible variables - do not hardcode credentials in image.
FROM ubuntu:22.04

ARG SSH_USER=blueteam
ARG SSH_PASSWORD=blueteam

USER root

RUN apt update && DEBIAN_FRONTEND=noninteractive apt install -y --no-install-recommends \
    openssh-server \
    && apt install -y sudo \
    && mkdir -p /run/sshd \
    && useradd -m -s /bin/bash "$SSH_USER" \
    && echo "$SSH_USER:$SSH_PASSWORD" | chpasswd \
    && sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin no/' /etc/ssh/sshd_config \
    && sed -i 's/#PasswordAuthentication yes/PasswordAuthentication yes/' /etc/ssh/sshd_config \
    && sed -i 's/#PermitEmptyPasswords no/PermitEmptyPasswords no/' /etc/ssh/sshd_config \
    && rm -rf /var/lib/apt/lists/* \
    && echo "blueteam ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/blueteam \
    && chmod 0440 /etc/sudoers.d/blueteam
EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
