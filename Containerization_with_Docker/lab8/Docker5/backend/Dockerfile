FROM python:3.12

WORKDIR /app

COPY . .

RUN pip install --no-cache-dir flask && \
    apt-get update && \
    apt-get install -y iputils-ping wget && \
    rm -rf /var/lib/apt/lists/*

EXPOSE 5000

CMD ["python", "app.py"]
