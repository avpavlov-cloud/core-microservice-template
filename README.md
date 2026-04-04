# Core Microservice Helm Chart (Istio & Service Mesh Ready)

Универсальный Helm-чарт для развертывания микросервисов в Kubernetes с продвинутой поддержкой Service Mesh (Istio) и динамическим управлением трафиком.

---

## 🚀 Основные возможности

* **Istio Integration** — автоматическая генерация Gateway, VirtualService и DestinationRule
* **Canary Deployments** — управление весами трафика (v1/v2) через `values.yaml`
* **Subcharts Support** — встроенная зависимость от Redis (Bitnami)
* **Advanced Templating** — использование `_helpers.tpl` для стандартизации
* **Production Ready** — Liveness/Readiness probes, лимиты CPU/RAM и HPA

---

## 🛠 Технологический стек

* Helm v3
* Kubernetes 1.22+
* Istio 1.15+
* Redis (Bitnami OCI Chart)

---

## 📦 Использование репозитория

### 1. Добавление репозитория

```bash
helm repo add avpavlov-repo https://github.io
helm repo update
```

### 2. Установка чарта

```bash
helm install my-app avpavlov-repo/core-microservice-template
```

---

## ⚙️ Конфигурация Canary Release

```yaml
istio:
  enabled: true
  host: "my-app.local"
  canary:
    v1Weight: 80  # 80% трафика на стабильную версию
    v2Weight: 20  # 20% трафика на новую версию
```

### Обновление весов

```bash
helm upgrade my-app avpavlov-repo/core-microservice-template \
  --set istio.canary.v1Weight=50 \
  --set istio.canary.v2Weight=50
```

---

## 📂 Структура проекта

* `templates/istio.yaml` — шлюз и маршруты Istio
* `templates/deployment.yaml` — deployment с поддержкой версий
* `charts/` — зависимости (Redis)
* `values.yaml` — конфигурация
* `index.yaml` — индекс Helm-репозитория

---

## 🧪 Локальная разработка (Minikube)

### Подготовка

```bash
helm dependency build .
helm lint .
helm template my-release .
```

### Установка

```bash
helm install my-app .
```

### Проброс порта

```bash
kubectl port-forward -n istio-system svc/istio-ingressgateway 8080:80
```

---

## ⚙️ Полезные команды Helm

### Установка Helm

```bash
sudo snap install helm --classic
```

### Проверка шаблонов

```bash
helm lint .
```

### Генерация манифестов

```bash
helm template my-test-release .
```

### Сборка зависимостей

```bash
helm dependency build .
```

### Генерация в файл

```bash
helm template my-release ./core-microservice-template | tee final_output.yaml
```

---

## 📦 Работа с пакетами

### Упаковка

```bash
helm package .
```

### Просмотр пакета

```bash
helm show chart ./core-microservice-template-1.0.0.tgz
```

---

## 🌐 Включение Istio в Minikube

```bash
minikube start
```

```bash
minikube addons enable istio-provisioner
minikube addons enable istio
```

```bash
kubectl label namespace default istio-injection=enabled
helm upgrade --install my-app .
kubectl port-forward -n istio-system svc/istio-ingressgateway 8080:80
```

