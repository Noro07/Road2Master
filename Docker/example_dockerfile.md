# dockerfile example

```dockerfile
FROM python:latest

COPY . /app

WORKDIR /app

RUN pip3 install psycopg2
RUN pip3 install requests
RUN python3 test.py
```
