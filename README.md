# Лабораторная работа № 1

Двухкомпонентное приложение: Nginx и Python. Развертывание - Ansible и Docker Compose.

## Требования

- Управляющая Linux-машина с Ansible и Git.
- Управляемая Ubuntu с Python 3, SSH и правами sudo.
- Доступ к интернету.

## Развертывание

1. Клонировать репозиторий на управляющую машину и перейти в каталог проекта.
2. В `ansible/inventory.ini` указать IP и пользователя управляемой машины.
3. Настроить подключение по SSH-ключу.
4. В `ansible/deploy.yml` указать адрес доступного репозитория в `repo_url`.
5. Установить зависимости и запустить плейбук:

   ```bash
   ansible-galaxy collection install -r ansible/requirements.yml
   ansible -i ansible/inventory.ini app_servers -m ping
   ansible-playbook -i ansible/inventory.ini ansible/deploy.yml --ask-become-pass
   ```
## Проверка

Открыть `http://IP_СЕРВЕРА:8080` и нажать «Проверить бэкенд».

Проверить API:

```bash
curl http://IP_СЕРВЕРА:8080/api/message
```

Ожидаемый результат - JSON с сообщением и именем контейнера.

Проверить контейнеры на управляемой машине:

```bash
cd /opt/iac-lab1
sudo docker compose ps
```

Оба сервиса - `frontend` и `backend` - должны быть запущены.

## Остановка

На управляемой машине выполнить:

```bash
cd /opt/iac-lab1
sudo docker compose down
```
