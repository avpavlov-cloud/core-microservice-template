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