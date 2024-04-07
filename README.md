# Репозиторий для выполнения домашних заданий курса "Инфраструктурная платформа на основе Kubernetes-2024-02"

# ДЗ № 5

Применяем все yaml-файлы.

```bash
cd kubernetes-security
kubectl apply -f namespace.yaml -f clusterrole-metrics.yaml -f sa-monitoring.yaml -f rb-monitoring.yaml -f sa-cd.yaml -f rb-cd.yaml -f -f service.yaml -f deployment.yaml
```

Создание токена для сервисного аккаунта cd с временем действия 1 день:

```bash
kubectl create token cd --namespace homework --duration 24h
```

Запуск kubectl со своим конфигурационным файлом:

```bash
export KUBECONFIG=(pwd)/kubeconfig
kubectl auth whoami
```

Проверка:

- эндпоинта /metrics запустить в поде

```bash
curl -vk -H "Authorization: Bearer $(cat /var/run/secrets/kubernetes.io/serviceaccount/token)" https://${KUBERNETES_SERVICE_HOST}:${KUBERNETES_SERVICE_PORT_HTTPS}/metrics
```

- сервиса

```bash
kubectl --namespace homework port-forward svc/httpd-service 8080:80
curl -v 127.0.0.1:8080/metrics.html
```