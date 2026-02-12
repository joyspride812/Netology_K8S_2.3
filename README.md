# Netology_K8S_2.3 (Моисеенко А.Н.)
## Задание 1: Работа с ConfigMaps
### Задача
Развернуть приложение (nginx + multitool), решить проблему конфигурации через ConfigMap и подключить веб-страницу.

### Шаги выполнения
- Создать Deployment с двумя контейнерами: nginx и multitool
- Подключить веб-страницу через ConfigMap
- Проверить доступность
<img width="753" height="243" alt="image" src="https://github.com/user-attachments/assets/c698b0af-76a5-4917-9e10-674335518f9c" />

### Манифесты:
- [deployment.yaml](https://github.com/joyspride812/Netology_K8S_2.3/edit/main/deployment.yaml)
- [configmap-web.yaml](https://github.com/joyspride812/Netology_K8S_2.3/edit/main/configmap-web.yaml)
## Задание 2: Настройка HTTPS с Secrets
## Задача
Развернуть приложение с доступом по HTTPS, используя самоподписанный сертификат.

### Шаги выполнения
- Сгенерировать SSL-сертификат openssl req -x509 -nodes -days 365 -newkey rsa:2048
-keyout tls.key -out tls.crt -subj "/CN=myapp.example.com"
- Создать Secret
- Настроить Ingress
- Проверить HTTPS-доступ
<img width="747" height="195" alt="image" src="https://github.com/user-attachments/assets/c796dc1f-af29-469f-93ca-7348cedbeba1" />

### Манифесты:
- [secret-tls.yaml](https://github.com/joyspride812/Netology_K8S_2.3/edit/main/secret-tls.yaml)
- [ingress-tls.yaml](https://github.com/joyspride812/Netology_K8S_2.3/edit/main/ingress-tls.yaml)
## Задание 3: Настройка RBAC
### Задача
Создать пользователя с ограниченными правами (только просмотр логов и описания подов).

### Шаги выполнения
- Включите RBAC в microk8s microk8s enable rbac
- Создать SSL-сертификат для пользователя openssl genrsa -out developer.key 2048
<img width="630" height="25" alt="image" src="https://github.com/user-attachments/assets/1a38b0c1-06cd-40d4-a607-bd1a6cd17999" />

openssl req -new -key developer.key -out developer.csr -subj "/CN={ИМЯ ПОЛЬЗОВАТЕЛЯ}" image
<img width="958" height="21" alt="image" src="https://github.com/user-attachments/assets/c435de65-4e55-4d84-9b57-3277634ad358" />

openssl x509 -req -in developer.csr -CA {CA серт вашего кластера} -CAkey {CA ключ вашего кластера} -CAcreateserial -out developer.crt -days 365 image
<img width="643" height="158" alt="image" src="https://github.com/user-attachments/assets/6a947a34-c88a-49c4-910c-2f865472e793" />

- Создать Role (только просмотр логов и описания подов) и RoleBinding
- Проверить доступ
<img width="602" height="55" alt="image" src="https://github.com/user-attachments/assets/a50dd27d-fb2e-43a0-bff0-6a4301228152" />

### Манифесты:
- [role-pod-reader.yaml](https://github.com/joyspride812/Netology_K8S_2.3/edit/main/role-pod-reader.yaml)
- [rolebinding-developer.yaml](https://github.com/joyspride812/Netology_K8S_2.3/edit/main/rolebinding-developer.yaml)
