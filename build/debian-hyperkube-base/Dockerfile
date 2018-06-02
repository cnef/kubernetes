# Copyright 2017 The Kubernetes Authors.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

FROM BASEIMAGE

RUN echo deb http://mirrors.aliyun.com/debian/ stretch main non-free contrib > /etc/apt/sources.list && \
    echo deb http://mirrors.aliyun.com/debian/ stretch-updates main non-free contrib >> /etc/apt/sources.list && \
    echo deb http://mirrors.aliyun.com/debian-security/ stretch/updates main non-free contrib >> /etc/apt/sources.list

RUN echo CACHEBUST>/dev/null && clean-install \
    bash

# The samba-common, cifs-utils, and nfs-common packages depend on
# ucf, which itself depends on /bin/bash.
RUN echo "dash dash/sh boolean false" | debconf-set-selections
RUN DEBIAN_FRONTEND=noninteractive dpkg-reconfigure dash

RUN echo CACHEBUST>/dev/null && clean-install \
    apt-transport-https \
    ca-certificates \
    ceph-common \
    cifs-utils \
    conntrack \
    e2fsprogs \
    ebtables \
    ethtool \
    git \
    gnupg \
    iptables \
    jq \
    kmod \
    openssh-client \
    nfs-common \
    socat \
    util-linux \
    wget

RUN wget -O /tmp/rsa.pub https://download.gluster.org/pub/gluster/glusterfs/4.0/rsa.pub && \
    apt-key add /tmp/rsa.pub && \
    rm /tmp/rsa.pub -rf && \
    echo deb [arch=amd64] https://download.gluster.org/pub/gluster/glusterfs/4.0/LATEST/Debian/stretch/amd64/apt stretch main > \
    /etc/apt/sources.list.d/gluster.list && \
    echo CACHEBUST>/dev/null && clean-install glusterfs-client=4.0.2-2

COPY cni-bin/bin /opt/cni/bin
