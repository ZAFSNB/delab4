# Задание 1. Подготовка окружения для локального кластера

## Требования

- Docker Desktop (или Docker Engine) — kind запускает узлы кластера как контейнеры;
- kubectl — клиент Kubernetes;
- kind — утилита создания кластера.

## Установка (Windows)

```powershell
winget install --id Kubernetes.kind -e --accept-source-agreements --accept-package-agreements
winget install --id Kubernetes.kubectl -e
```

## Создание кластера

```bash
kind create cluster --config kind-config.yaml
```

Конфигурация `kind-config.yaml` создаёт три узла: один control-plane и два worker.

## Проверка

```bash
kubectl cluster-info
kubectl get nodes -o wide
```

Все узлы должны быть в состоянии `Ready`.

## Удаление кластера

```bash
kind delete cluster --name lab4
```
