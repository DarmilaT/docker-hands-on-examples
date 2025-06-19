FROM ubuntu:latest

WORKDIR /app

COPY requirements.txt /app
COPY demo-webapp /app

RUN apt-get update && \
    apt-get install -y python3 python3-pip && \
    pip install --break-system-packages -r requirements.txt

ENTRYPOINT ["python3"]
CMD ["manage.py", "runserver", "0.0.0.0:8000"]
