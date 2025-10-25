FROM python:3.12-slim

WORKDIR /app

COPY . .

RUN pip install flask

EXPOSE 5000

ENTRYPOINT ["python", "app.py" ]
