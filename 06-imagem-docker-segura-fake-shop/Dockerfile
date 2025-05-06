FROM python:3.11-alpine

RUN apk update && apk upgrade
RUN apk add --no-cache gcc musl-dev libffi-dev postgresql-dev
#RUN pip install --upgrade pip setuptools>=70.0.0 Jinja2>=3.1.6 gunicorn>=23.0.0
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
RUN addgroup -g 1000 python && \
    adduser -u 1000 -G python -D python
RUN apk add --no-cache gcc musl-dev libffi-dev postgresql-dev
USER python
WORKDIR /app
COPY --chown=python:python requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY --chown=python:python . .
EXPOSE 8000
HEALTHCHECK --interval=30s --timeout=5s --start-period=5s --retries=3 \
  CMD wget -q --spider http://localhost:8000/health || exit 1
CMD ["gunicorn", "-b", "0.0.0.0:8000", "app:app"]
