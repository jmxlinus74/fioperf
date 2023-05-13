FROM amazonlinux:2023

# Options for setup script
ARG INSTALL_ZSH="false"
ARG UPGRADE_PACKAGES="true"
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# Install requirements.
RUN yum -y install rpm dnf-plugins-core \
 && yum -y update \
 && yum -y install \
      python3.9 \
      python3-pip \
      python3-pyyaml \
      python3-devel \
      python3-virtualenv \
      tar \
      gcc \
      zlib-devel \
      libjpeg-devel \
      make \
      fio \
 && yum clean all

# Install needed packages and setup non-root user. Use a separate RUN statement to add your own dependencies.
COPY library-scripts/*.sh library-scripts/*.env /tmp/library-scripts/
RUN bash /tmp/library-scripts/common-redhat.sh "${INSTALL_ZSH}" "${USERNAME}" "${USER_UID}" "${USER_GID}" "${UPGRADE_PACKAGES}" "true" "true" \
    && yum clean all -y && rm -rf /var/lib/apt/lists/* /tmp/library-scripts

RUN virtualenv -p /usr/bin/python3 --system-site-packages /vpy3 \
    && /vpy3/bin/pip install --no-cache-dir --upgrade pip
  
