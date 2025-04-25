# K-ISP-Polina
# Установка и настройка Prometheus

---

## 1. Проверка и отключение/настройка файервола

Сначала я проверила статус файервола. Для этого выполнила команду:

```bash
sudo firewall-cmd --state
```

Если файервол был включен, то я его остановила и отключила автозапуск:

```bash
sudo systemctl stop firewalld
sudo systemctl disable firewalld
```

**Что сделала:**
- `firewall-cmd --state`: Проверила текущий статус файервола (включен или выключен).
- `systemctl stop firewalld`: Остановила службу файервола.
- `systemctl disable firewalld`: Отключила автозапуск файервола при загрузке системы.

![image](https://github.com/user-attachments/assets/2f1152d4-d5ea-4b70-b699-533f9097adb9)



---

## 2. Установка необходимых пакетов

Для работы мне понадобились несколько полезных утилит: `wget`, `curl`, `git` и `tar`. Я установила их одной командой:

```bash
sudo yum install -y wget curl git tar
```

**Почему это важно:**
Эти инструменты нужны для скачивания файлов, работы с Git и распаковки архивов.

![image](https://github.com/user-attachments/assets/6c76c6f7-1cf8-43fa-a1e3-90ec23155bee)



---

## 3. Установка и настройка Chrony

Установила и настроила Chrony

```bash
sudo yum install -y chrony
sudo systemctl enable chronyd
sudo systemctl start chronyd
```

После запуска проверила статус службы:

```bash
systemctl status chronyd
```

**Что сделала:**
- Установила Chrony — демон для синхронизации времени.
- Добавила службу в автозагрузку и запустила её.
- Проверила, что всё работает корректно.

![image](https://github.com/user-attachments/assets/2dad2889-0037-441c-a85e-d8eb32f429c4)



---

## 4. Проверка и отключение SELinux

Проверила статус SELinux:

```bash
getenforce
```

Если выводилось "Enforcing", то я временно отключила защиту:

```bash
sudo setenforce 0
sudo sed -i 's/^SELINUX=.*/SELINUX=disabled/g' /etc/selinux/config
```

**Что сделала:**
- Проверила режим работы SELinux.
- Переключила его в режим Permissive и изменила конфигурационный файл для полного отключения при следующей загрузке.

![image](https://github.com/user-attachments/assets/8e1cd413-d35a-4d31-8700-9fb79b6fdee7)




---

## 5. Скачивание Prometheus

Скачиванию Prometheus версию 3.3.0:

```bash
wget https://github.com/prometheus/prometheus/releases/download/v3.3.0/prometheus-3.3.0.linux-amd64.tar.gz
```

![image](https://github.com/user-attachments/assets/f9bafefd-b8e8-42d3-8e3b-a606a6a80008)



---

## 6. Создание каталогов для Prometheus

Создала необходимые директории для конфигурации и данных:

```bash
sudo mkdir -p /etc/prometheus /var/lib/prometheus
```

Ипроверила что они существуют:
```bash
ls /etc/prometheus
ls /var/lib/prometheus
```

![image](https://github.com/user-attachments/assets/775fbe74-fc2d-483e-9743-5f8070a8af7c)



---

## 7. Разархивация скачанного файла

Распаковала архив в текущую директорию:

```bash
tar -zxf prometheus-*.linux-amd64.tar.gz
```

![image](https://github.com/user-attachments/assets/65f58797-713e-46dc-a511-054852696b83)



---

## 8. Переход в распакованную директорию

Перешла в папку с распакованными файлами:

```bash
cd prometheus-*.linux-amd64
```

![image](https://github.com/user-attachments/assets/5b2b6deb-4f89-447f-a246-1e03e585f173)



---

## 9. Проверка текущей директории

Чтобы убедиться, где я нахожусь, выполнила:

```bash
pwd
```

![image](https://github.com/user-attachments/assets/d1c9fb04-d455-4b21-80b2-b0e41905483b)



---

## 10. Копирование файлов Prometheus

Скопировала бинарные файлы и конфигурацию в системные директории:

```bash
sudo cp prometheus promtool /usr/local/bin/
sudo cp prometheus.yml /etc/prometheus/
```

**Что сделала:**
- Бинарные файлы (`prometheus`, `promtool`) поместила в `/usr/local/bin/` для глобального доступа.
- Конфигурационный файл (`prometheus.yml`) скопировала в `/etc/prometheus/`.

![image](https://github.com/user-attachments/assets/ed00d099-2bfb-43c0-a051-60679ec58486)



---

## 11. Очистка временных файлов

Удалила временные файлы, чтобы не захламлять систему:

```bash
cd .. && rm -rf prometheus-*.linux-amd64/ && rm -f prometheus-*.linux-amd64.tar.gz
```

![image](https://github.com/user-attachments/assets/6534cbbd-e4f5-4d23-af7d-016cea05df3a)



---

## 12. Повторная проверка текущей директории

Убедилась, что вернулась в правильную директорию:

```bash
pwd
```

![image](https://github.com/user-attachments/assets/6f6098ff-119d-4e3d-888d-91342ee3c468)



---

## 13. Проверка содержимого директории

Проверила, что всё на месте:

```bash
ls -l
```

![image](https://github.com/user-attachments/assets/e95ae4d1-5360-4862-8d07-b4200134d6f3)



---
