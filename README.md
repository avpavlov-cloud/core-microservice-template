Установка HELM
```bash
sudo snap install helm --classic
```
Проверка шаблонов HELM в директории проекта
```bash
helm lint .
```

Генерация итоговых манифестов
```bash
helm template my-test-release .
```

Устновка зависимости связанной с Redis
```bash
helm dependency build .
```

Генерация в файл
```bash
helm template my-release ./core-microservice-template | tee final_output.yaml
```

## Упаковка в метаданные проекта
Упаковка
```bash
helm package .
```

Распаковка
```bash
helm show chart ./core-microservice-template-1.0.0.tgz
```

## Включить Istio
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
```


