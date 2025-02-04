# ServiceYandex/Dockerfile

FROM python:3.10-slim

# Устанавливаем необходимые пакеты
RUN apt-get update && apt-get install -y git curl awscli && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Устанавливаем рабочую директорию
WORKDIR /app

# Клонируем репозиторий с GitHub (замените URL на ваш)
RUN git clone https://github.com/danikodev/rtdm_ServiceYandex_update.git .

# Копируем файл с зависимостями
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Копируем SSL-сертификаты в контейнер (замените на ваши файлы)
COPY /etc/letsencrypt/live/daniko.ddns.net/fullchain.pem /app/cert.pem
COPY /etc/letsencrypt/live/daniko.ddns.net/privkey.pem /app/key.pem

# Установка переменной окружения (если необходимо)
ENV YANDEX_TOKEN="y0__wgBEMn84L0GGJrSNCDstPmLEj3mibU9UTJQhVvzwdQpi-g7DeLm"

# Запускаем приложение с указанием пути к сертификатам
CMD ["python", "ServiceYandex/main.py"]
