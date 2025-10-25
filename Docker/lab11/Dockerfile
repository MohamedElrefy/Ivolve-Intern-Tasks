FROM python:3.11-slim

WORKDIR /app

COPY . .

RUN pip install --no-cache-dir flask

ENV APP_MODE=production

ENV APP_REGION=canda-west

EXPOSE 8080

ENTRYPOINT [ "python", "app.py" ]