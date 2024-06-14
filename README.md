# Домашнее задание к занятию «Управление доступом» - Вдовин Вадим

### Цель задания

В тестовой среде Kubernetes нужно предоставить ограниченный доступ пользователю.

------

### Чеклист готовности к домашнему заданию

1. Установлено k8s-решение, например MicroK8S.
2. Установленный локальный kubectl.
3. Редактор YAML-файлов с подключённым github-репозиторием.

------

### Инструменты / дополнительные материалы, которые пригодятся для выполнения задания

1. [Описание](https://kubernetes.io/docs/reference/access-authn-authz/rbac/) RBAC.
2. [Пользователи и авторизация RBAC в Kubernetes](https://habr.com/ru/company/flant/blog/470503/).
3. [RBAC with Kubernetes in Minikube](https://medium.com/@HoussemDellai/rbac-with-kubernetes-in-minikube-4deed658ea7b).

------

### Задание 1. Создайте конфигурацию для подключения пользователя

1. Создайте и подпишите SSL-сертификат для подключения к кластеру.
```
root@vm1:/home/user# openssl genrsa -out vadim.key 2048
root@vm1:/home/user# openssl req -new -key vadim.key -out vadim.csr -subj "/CN=vadim/O=group1"
root@vm1:/home/user# openssl x509 -req -in vadim.csr -CA /var/snap/microk8s/6070/certs/ca.crt -CAkey /var/snap/microk8s/6070/certs/ca.key -CAcreateserial -out vadim.crt -days 500
Certificate request self-signature ok
subject=CN = vadim, O = group1
```
2. Настройте конфигурационный файл kubectl для подключения.

```
root@vm1:/home/user# kubectl config set-context vadim-context --cluster=microk8s-cluster --user=vadim
Context "vadim-context" created.

root@vm1:/home/user# kubectl config view
apiVersion: v1
clusters:
- cluster:
    certificate-authority-data: DATA+OMITTED
    server: https://10.129.0.6:16443
  name: microk8s-cluster
contexts:
- context:
    cluster: microk8s-cluster
    user: admin
  name: microk8s
- context:
    cluster: microk8s-cluster
    user: vadim
  name: vadim-context
current-context: microk8s
kind: Config
preferences: {}
users:
- name: admin
  user:
    token: REDACTED
- name: vadim
  user:
    client-certificate: /home/user/cert/vadim.crt
    client-key: /home/user/cert/vadim.key
```
3. Создайте роли и все необходимые настройки для пользователя.

```
root@vm1:/home/user# kubectl apply -f role_binding.yaml
rolebinding.rbac.authorization.k8s.io/pod-reader created
root@vm1:/home/user# kubectl apply -f role.yaml
role.rbac.authorization.k8s.io/pod-desc-logs created
```
4. Предусмотрите права пользователя. Пользователь может просматривать логи подов и их конфигурацию (`kubectl logs pod <pod_id>`, `kubectl describe pod <pod_id>`).

```
Добавляем в роль verbs: где ["watch", "list"]

root@vm1:/home/user# kubectl get role pod-desc-logs -o yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"rbac.authorization.k8s.io/v1","kind":"Role","metadata":{"annotations":{},"name":"pod-desc-logs","namespace":"default"},"rules":[{"apiGroups":[""],"resources":["pods","pods/log"],"verbs":["watch","list","get"]}]}
  creationTimestamp: "2024-06-13T15:43:45Z"
  name: pod-desc-logs
  namespace: default
  resourceVersion: "2126"
  uid: 834c7ee6-790d-4059-b028-554274d91f82
rules:
- apiGroups:
  - ""
  resources:
  - pods
  - pods/log
  verbs:
  - watch
  - list
  - get

```
5. Предоставьте манифесты и скриншоты и/или вывод необходимых команд.
