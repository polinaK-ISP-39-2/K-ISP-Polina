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

![image](https://github.com/user-attachments/assets/09c7bad8-cf1a-4677-9fa6-72ecd4794353)

---

## 2. Установка необходимых пакетов

Для работы мне понадобились несколько полезных утилит: `wget`, `curl`, `git` и `tar`. Я установила их одной командой:

```bash
sudo yum install -y wget curl git tar
```

**Почему это важно:**
Эти инструменты нужны для скачивания файлов, работы с Git и распаковки архивов.

![image](https://github.com/user-attachments/assets/9ecbeae8-4496-40ec-b994-70c9c0116c04)

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

![image](https://github.com/user-attachments/assets/be6b23ab-3c4e-4ee6-aa72-fbad8ee38714)

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

![image](https://github.com/user-attachments/assets/d4dd2436-0f4e-4714-9c42-7153e500a7dc)

---

## 5. Скачивание Prometheus

Скачиванию Prometheus версию 3.3.0:

```bash
wget https://github.com/prometheus/prometheus/releases/download/v3.3.0/prometheus-3.3.0.linux-amd64.tar.gz
```

![image](https://github.com/user-attachments/assets/c0f402ec-5a29-4cb4-804d-50cc58628cda)

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

![image](https://github.com/user-attachments/assets/c1220634-5eae-401c-b11c-049249037dd4)

---

## 7. Разархивация скачанного файла

Распаковала архив в текущую директорию:

```bash
tar -zxf prometheus-*.linux-amd64.tar.gz
```

![image](https://github.com/user-attachments/assets/8f009e6c-6dd0-4543-9c10-5437c9c6235f)

---

## 8. Переход в распакованную директорию

Перешла в папку с распакованными файлами:

```bash
cd prometheus-*.linux-amd64
```

![image](https://github.com/user-attachments/assets/f7fe10f7-a257-4346-ba35-f0facb8cd33d)

---

## 9. Проверка текущей директории

Чтобы убедиться, где я нахожусь, выполнила:

```bash
pwd
```

![image](https://github.com/user-attachments/assets/914c1be2-1bea-4481-97bf-76b6142730ca)

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

![image](https://github.com/user-attachments/assets/4969637b-e3c0-4dea-aa68-8a0fe5649282)

---

## 11. Очистка временных файлов

Удалила временные файлы, чтобы не захламлять систему:

```bash
cd .. && rm -rf prometheus-*.linux-amd64/ && rm -f prometheus-*.linux-amd64.tar.gz
```

![image](https://github.com/user-attachments/assets/14fd5630-3389-4467-995f-cdd501d5b20a)

---

## 12. Повторная проверка текущей директории

Убедилась, что вернулась в правильную директорию:

```bash
pwd
```

![image](https://github.com/user-attachments/assets/52eede5a-f0ec-475f-8ea8-d9efc3f9e96a)

---

## 13. Проверка содержимого директории

Проверила, что всё на месте:

```bash
ls -l
```

![image](https://github.com/user-attachments/assets/395c351a-a81d-4171-b09e-d9adb8e9239f)


---
