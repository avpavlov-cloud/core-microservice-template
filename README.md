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

