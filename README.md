# Задача 1: Работа с сервис-аккаунтами через утилиту kubectl в установленном minikube

Создадим новый сервис аккаунт и посмотрим на него:

```shell
desema@control1:~$ kubectl create serviceaccount netology
serviceaccount/netology created

desema@control1:~$ kubectl get serviceaccounts
NAME                                SECRETS   AGE
default                             1         59d
netology                            1         6s
nfs-server-nfs-server-provisioner   1         46d

desema@control1:~$ kubectl get serviceaccount
NAME                                SECRETS   AGE
default                             1         59d
netology                            1         10s
nfs-server-nfs-server-provisioner   1         46d
desema@control1:~$
```

Поиграемся с выводом в разные форматы:
```shell
desema@control1:~$ kubectl get serviceaccount netology -o yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  creationTimestamp: "2021-12-16T17:32:00Z"
  name: netology
  namespace: default
  resourceVersion: "487095"
  uid: a3344aae-20ac-4c3b-bcfe-f93cb703e925
secrets:
- name: netology-token-txcwf

desema@control1:~$ kubectl get serviceaccount default -o json
{
    "apiVersion": "v1",
    "kind": "ServiceAccount",
    "metadata": {
        "creationTimestamp": "2021-10-17T20:18:38Z",
        "name": "default",
        "namespace": "default",
        "resourceVersion": "432",
        "uid": "3452ae23-44e0-42ea-befa-3ff5a1904d77"
    },
    "secrets": [
        {
            "name": "default-token-mnhwx"
        }
    ]
}
```

После этого выгрузим сервис-аккаунты в файл, удалим наш тестовый и вернём его обратно импортом из файла:

```shell
desema@control1:~$ kubectl get serviceaccounts -o json > serviceaccounts.json
desema@control1:~$ kubectl get serviceaccount netology -o yaml > netology.yml
desema@control1:~$ kubectl delete serviceaccount netology
serviceaccount "netology" deleted
desema@control1:~$ kubectl apply -f netology.yml
serviceaccount/netology created
```