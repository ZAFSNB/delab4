# Overview

Report on LabRabota4. Методы и средства оркестрации в многоконтейнерных системах (Kubernetes, kind).



- Задание 1 (группа 13) — каталог `task1/`: конфигурация локального кластера kind.
- Задание 2 (группа 13) — каталог `task2/`: манифесты Pod, PVC, ReplicaSet.
- Отчет — `docs/report.md`.

Быстрый запуск:

```bash
cd task1
kind create cluster --config kind-config.yaml
kubectl get nodes -o wide
```

# Author

Чжао Аофэй, группа 13.

