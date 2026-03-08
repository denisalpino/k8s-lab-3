# Лабораторная работа №1: Развертывание приложения в Kubernetes

**Команда:** Томин Денис

## 1. Описание задачи
Развертывание отказоустойчивого приложения [Название приложения] в локальном кластере Minikube.

## 2. Ход работы
### Шаг 0: Полготовка и скачивание
...
```bash
sudo apt-get update &&
sudo apt-get install -y apt-transport-https ca-certificates curl
```

...
```bash
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.31/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg &&
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.31/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
```

...
```bash
sudo apt-get install -y kubectl &&
curl -LO https://github.com/kubernetes/minikube/releases/latest/download/minikube-installer.exe
```

...
```bash
chmod +x minikube-installer.exe
./minikube-installer.exe
```

### Шаг 1: Запуск кластера
Кластер запущен командой `minikube start`.
![docs/download.jpg](docs/download.jpg)

minikube.exe работает в Windows и успешно создал кластер, но он обновил файл конфигурации (kubeconfig) внутри Windows. В то же время kubectl, установленный в WSL, ищет настройки в своем локальном файле ~/.kube/config, который сейчас пуст.
```bash
rm -rf ~/.kube &&
mkdir -p ~/.kube &&
ln -s /mnt/c/Users/79112/.kube/config ~/.kube/config
```

Был получен следующий статус клавстера:
![docs/status.jpg](docs/status.jpg)

### Шаг 2: Создание манифестов
Мы подготовили Deployment для управления подами и Service для доступа к ним.
(Кратко опиши, что за образ используешь, например nginx).

### Шаг 3: Применение конфигурации
```bash
kubectl apply -f manifests/