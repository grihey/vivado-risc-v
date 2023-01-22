
FROM ubuntu:22.10
ARG userid
ARG groupid
ARG username

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y git-core gnupg zip curl device-tree-compiler sudo wget vim gnupg

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 3B4FE6ACC0B21F32
RUN echo 'deb http://security.ubuntu.com/ubuntu bionic-security main universe' >> /etc/apt/sources.list
RUN echo 'deb http://cz.archive.ubuntu.com/ubuntu bionic main' >> /etc/apt/sources.list

RUN apt-get update && apt-get install -y gcc-8-riscv64-linux-gnu #libc6-dev-riscv64-cross
RUN apt-get install -y flex bison build-essential
RUN apt-get install -y binutils-riscv64-linux-gnu
RUN apt-get install -y vim
RUN apt-get install -y libssl-dev
RUN apt-get install -y libdebuginfod-dev
RUN apt-get install -y python3
RUN apt-get install -y locales
RUN apt-get install -y libtinfo5
RUN apt-get install -y bc
RUN apt-get install -y fdisk
RUN apt-get install -y parted
RUN apt-get install -y udev
RUN apt-get install -y dosfstools
RUN apt-get update && apt-get install -y libc6-dev

RUN groupadd -g $groupid $username \
 && useradd -m -u $userid -g $groupid $username \
 && echo $username >/root/username

RUN usermod -aG sudo $username

RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
RUN echo 'PATH="${PATH}:/opt/Xilinx/Vivado/2022.2/bin"' >> /home/grihey/.bashrc
RUN echo 'PATH="${PATH}:/riscv-toolchain/bin"' >> /home/grihey/.bashrc

RUN locale-gen "en_US.UTF-8"

ENV HOME=/home/$username
ENV USER=$username
ENTRYPOINT chroot --userspec=$(cat /root/username):$(cat /root/username) / /bin/bash -i
