---
title: Установка
layout: home
nav_order: 2
---

# Способы установки

## 1. Автоматическая установка (рекомендуется)

**Linux/macOS:**
```
wget https://raw.githubusercontent.com/Anisan/osysHome/master/install.sh  
chmod +x install.sh  
./install.sh
```
**Windows:**
```
curl -L https://raw.githubusercontent.com/Anisan/osysHome/master/install.bat -o install.bat  
install.bat
```
Автоматические скрипты выполняют полную установку, включая загрузку репозитория, создание виртуального окружения, установку зависимостей и основных плагинов.
Автоматические скрипты установки (install.sh и install.bat) выполняют дополнительные задачи, такие как генерация документации с помощью pdoc и проверка зависимостей системы.

## 2. Ручная установка

### Шаг 1: Клонирование репозитория

```
git clone https://github.com/Anisan/osysHome.git  
cd osysHome
```

### Шаг 2: Создание виртуального окружения

**Linux/macOS**
```
python3 -m venv venv  
source venv/bin/activate  
```
**Windows**
```
python -m venv venv  
venv\Scripts\activate
```

### Шаг 3: Установка зависимостей
```
pip install -r requirements.txt  
mkdir plugins
```

### Шаг 4. Установка рекомендуемых модулей
```
git clone https://github.com/Anisan/osysHome-Modules.git plugins/Modules  
git clone https://github.com/Anisan/osysHome-Objects.git plugins/Objects  
git clone https://github.com/Anisan/osysHome-Users.git plugins/Users  
git clone https://github.com/Anisan/osysHome-Scheduler.git plugins/Scheduler  
git clone https://github.com/Anisan/osysHome-wsServer.git plugins/wsServer  
git clone https://github.com/Anisan/osysHome-Dashboard.git plugins/Dashboard  
git clone https://github.com/Anisan/osysHome-Mqtt.git plugins/Mqtt
```


## 3. Docker установка
```
sudo docker build -t osyshome .  
sudo docker run -d --network host -p 5000:5000 osyshome
```
Docker образ автоматически включает все необходимые плагины и зависимости.
 Для Docker установки используется Python 3.13 как базовый образ с предустановленными системными зависимостями включая Git.


# Настройка и запуск

## Создание файла конфигурации:

**Linux/macOS**
```
cp sample_config.yaml config.yaml  
```  
**Windows**
```
copy sample_config.yaml config.yaml
```

## Настройка базы данных в config.yaml
Настройки базы данных находятся в секции database файла config.yaml.
Система поддерживает нескольких СУБД:

**SQLite (по умолчанию)**
```
database:  
  db_name: app.db  
```
**PostgreSQL**
```
database:  
  connection_string: "postgresql://username:password@localhost:5432/osyshome"  
```
**MySQL**
```
database:  
  connection_string: "mysql://username:password@localhost:3306/osyshome"  
```
## Запуск системы:

**Linux/macOS**
```
python3 main.py  
```
**Windows **
```
python main.py
```

После запуска веб-интерфейс будет доступен по адресу http://localhost:5000 .
