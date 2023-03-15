# Выполнено ДЗ № 1

 - [x] Основное ДЗ
 - [ ] Задание со *

## В процессе сделано:
 - Установлены docker, kubectl, minikube и аддон для k8s - Dashboard
 - Проверена отказоустойчивость k8s путем удаления всех контейнеров в неймспейсе kube-system.
**Ответ на задание** "Разберитесь почему все pod в namespace kube-system восстановились
после удаления. Укажите причину в описании PR": 
Поды в неймспейсе kube-system самостоятельно восстановились по трем причинам:
1. Под coredns контролируется с помощью Deployment, который использует ReplicaSet. Посмотрев Deployment, видим заданное количество реплик = 1: 
```
$ kubectl edit deployment coredns -n kube-system
...
replicas: 1
```
...
2. Под kube-proxy управляется при помощи DaemonSet. Таким образом, DaemonSet контролирует, что под kube-proxy всегда запущен на каждом узле кластера.
3. Поды etcd, kube-apiserver, kube-controller-manager и kube-scheduler являются static Pods, поэтому kubelet следит, чтобы каждый из этих подов был всегда запущен. Манифесты этих подов описаны по пути /etc/kubernetes/manifests/:
```
$ minikube ssh
Last login: Sun Mar 12 14:57:03 2023 from 192.168.49.1
docker@minikube:~$ ls -lah /etc/kubernetes/manifests/
total 28K
drwxr-xr-x 1 root root 4.0K Mar 11 19:46 .
drwxr-xr-x 1 root root 4.0K Mar 11 19:46 ..
-rw------- 1 root root 2.5K Mar 11 19:46 etcd.yaml
-rw------- 1 root root 4.0K Mar 11 19:46 kube-apiserver.yaml
-rw------- 1 root root 3.4K Mar 11 19:46 kube-controller-manager.yaml
-rw------- 1 root root 1.5K Mar 11 19:46 kube-scheduler.yaml
```
   - Создан веб-сервер на nginx и собран в docker-образ. Docker-образ запушен в Docker Hub
   - Создан манифест web-pod.yaml и применен при помощи команды kubectl apply 
   - Затем дополнила манифест web-pod.yaml описанием init-контейнера. Также описаны volumeMounts для контейнеров web и init и volumes в spec.
   - Удален запущенный под, и применен обновленный манифест web-pod.yaml 
   - Командой kubectl port-forward на локалхост проброшен порт 8000, в результате чего по ссылке http://localhost:8000/index.html открывается веб-страница.

## Как запустить проект:
 - В директории kubernetes-intro запустить команду:
   `kubectl apply -f web-pod.yaml`

## Как проверить работоспособность:
 - Пробросить порт командой
` kubectl port-forward --address 0.0.0.0 pod/web 8000:8000`
 - Перейти на страницу: http://localhost:8000/index.html  

## PR checklist:
 - [x] Выставлен label с темой домашнего задания
