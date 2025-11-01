# Kubernetes Cluster with Vagrant and Ansible

This project allows you to create a **multi-node Kubernetes cluster** (1 master + N workers) using **Vagrant** and **Ansible** on your local machine. It automates the installation of Docker, containerd, Kubernetes components, and a network plugin (Flannel) for inter-pod communication.

---

## Prerequisites

Make sure you have the following installed:

- [Vagrant](https://www.vagrantup.com/)  
- [VirtualBox](https://www.virtualbox.org/)  
- [Ansible](https://www.ansible.com/)  

---

## Start the cluster with Vagrant:

```sh
vagrant up
```
```
1. Vagrant will create the master and worker VMs.
2. Ansible will automatically provision all nodes, install dependencies, initialize Kubernetes master, deploy Flannel, and join workers.
```

---

## Check the cluster status:

```sh
vagrant ssh master
kubectl get nodes

```