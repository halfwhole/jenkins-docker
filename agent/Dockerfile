FROM jenkins/jnlp-slave:3.35-5

ARG TINI_VERSION=v0.18.0
ARG ANSIBLE_VERSION=2.9.9-1ppa~trusty

USER root

## Install tini
RUN curl -L https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini -o /tini && \
    chmod +x /tini && \
## Install ansible
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367 && \
    echo "deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main" >> /etc/apt/sources.list && \
    apt update -y && \
    apt install --no-install-recommends -y ansible=${ANSIBLE_VERSION} && \
## Remove cache
    rm -rf /var/lib/apt/lists/* /root/.cache

ENTRYPOINT ["/tini", "--", "jenkins-agent"]

USER jenkins
