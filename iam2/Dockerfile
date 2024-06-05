FROM --platform=$BUILDPLATFORM python:3.12.3-alpine AS builder

# Set Environment Variable
ENV PYTHONUNBUFFERED=1
ENV LANG C.UTF-8
ENV DEBIAN_FRONTEND=noninteractive
ENV TZ="Asia/Ho_Chi_Minh"

# Creating Work Directory
WORKDIR /app


RUN apt-get update -q \
    && apt-get -qy dist-upgrade \
    && apt-get upgrade -y \
    && apt-get -y install build-essential python3-dev default-libmysqlclient-dev pkg-config \
    cron
RUN apt install software-properties-common -y

# Installing requirements.pip from project
COPY requirements.txt ./
RUN python -m pip install --upgrade pip
RUN pip install -r requirements.txt --no-cache-dir

RUN python manage.py collectstatic --no-input

CMD ["gunicorn", "--config=gunicorn.py", "iam2.wsgi:application"]