# ServiceMain/Dockerfile

FROM python:3.10-slim

# Устанавливаем необходимые пакеты
RUN apt-get update && apt-get install -y git curl cron awscli && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Устанавливаем рабочую директорию
WORKDIR /app

# Клонируем репозиторий с GitHub (замените URL на ваш)
RUN git clone https://github.com/danikodev/rtdm_ServiceMain_update.git .

# Копируем файл с зависимостями
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Копируем скрипт резервного копирования в контейнер
COPY db-backup.sh /usr/local/bin/db-backup.sh

# Установка прав на исполняемость для скрипта резервного копирования
RUN chmod +x /usr/local/bin/db-backup.sh

# Настройка cron для автоматического выполнения бэкапов
RUN echo '0 2 * * * /usr/local/bin/db-backup.sh' >> /etc/crontab

# Установка переменной окружения
ENV YANDEX_TOKEN="y0__wgBEMn84L0GGJrSNCDstPmLEj3mibU9UTJQhVvzwdQpi-g7DeLm"

# Запускаем cron и приложение одновременно
CMD ["sh", "-c", "cron && python ServiceMain/main.py"]
