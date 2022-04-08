# libvirt_cloudimg



sudo apt install virt-manager \

wget http://cloud-images.ubuntu.com/focal/current/focal-server-cloudimg-amd64.img \

qemu-img create -b focal-server-cloudimg-amd64.img -f qcow2 -F qcow2 ubuntu-1.img 50G \

qemu-img info ubuntu-1.img \

genisoimage -output ubuntu-cidata.iso -volid cidata -joliet -rock user-data meta-data \

qemu-img resize ubuntu-1.img +5G \

vim user-data \

#cloud-config \

users:
- name: ubuntu
  plain_text_passwd: 'ubuntu'
  sudo: ALL=(ALL) NOPASSWD:ALL
  groups: sudo
  shell: /bin/bash
  lock_passwd: false
ssh_pwauth: True

vim meta-data \

local-hostname: ubuntu \


