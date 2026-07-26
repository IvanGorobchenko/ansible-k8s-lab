# Ansible K8s Lab

Набор Ansible-плейбуков для автоматической подготовки инфраструктуры
под Kubernetes-кластер: базовая настройка машин, установка Docker
и полная подготовка узлов под kubeadm.

## Состав

- `playbook-base.yml` — обновление системы и установка базовых утилит
- `playbook-docker.yml` — установка Docker Engine + плагины по официальному репозиторию
- `playbook-k8s-prep.yml` — подготовка узлов под Kubernetes: модули ядра, sysctl, containerd (SystemdCgroup), установка и фиксация kubelet/kubeadm/kubectl, отключение swap
- `playbook-ctrl-kubectl.yml` — установка kubectl на управляющем узле и раскладка kubeconfig с мастера

## Топология (inventory.ini)

- `control` — управляющий узел
- `masters` — master-узлы кластера
- `workers` — рабочие узлы
- группа `k8s` объединяет masters + workers

## Как запустить

​```bash
ansible-playbook -i inventory.ini playbook-base.yml
ansible-playbook -i inventory.ini playbook-docker.yml
ansible-playbook -i inventory.ini playbook-k8s-prep.yml
ansible-playbook -i inventory.ini playbook-ctrl-kubectl.yml
​```

## Требования

- Ansible на управляющей машине (с коллекцией `community.general`)
- Ubuntu на целевых узлах
- Доступ по SSH к узлам
- Kubernetes v1.31

## Примечания

- `inventory.ini` содержит примерные адреса — подставьте свои
- Проект разворачивался и отлаживался на локальных виртуальных машинах
