# Задание 2. Знакомство с ресурсами Kubernetes

## Состав каталога

| Файл | Ресурс | Назначение |
|---|---|---|
| `pod.yaml` | Pod | простой под с одним контейнером nginx |
| `pvc.yaml` | PersistentVolumeClaim | заявка на том 1 Gi (динамическое создание PV) |
| `pod-with-volume.yaml` | Pod + PVC + emptyDir | под с постоянным (`/data`) и временным (`/cache`) томами |
| `replicaset.yaml` | ReplicaSet | 3 реплики nginx, самовосстановление подов |

## Применение

```bash
kubectl apply -f pod.yaml
kubectl apply -f pvc.yaml
kubectl apply -f pod-with-volume.yaml
kubectl apply -f replicaset.yaml
```

## Проверка

```bash
kubectl get pods -o wide                 # поды и узлы, на которых они запущены
kubectl get pvc,pv                       # том связан (Bound)
kubectl logs lab4-volume-demo            # вывод записи в /data и /cache
kubectl exec lab4-volume-demo -- sh -c "df -h /data; cat /data/log.txt"
kubectl get rs,pods -l app=lab4-rs -o wide
```

## Демонстрация

1. **Монтирование тома.** `pod-with-volume.yaml` пишет строку в `/data/log.txt` (PVC) и в `/cache/tmp.txt` (emptyDir).
2. **Сохранность данных.** После `kubectl delete pod lab4-volume-demo` и повторного `apply` файл `/data/log.txt` содержит обе записи — том пережил пересоздание пода.
3. **Самовосстановление.** После удаления любого пода ReplicaSet создаёт новый, число подов возвращается к трём.

## Удаление ресурсов

```bash
kubectl delete -f replicaset.yaml -f pod-with-volume.yaml -f pod.yaml -f pvc.yaml
```
