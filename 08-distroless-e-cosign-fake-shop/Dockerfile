FROM cgr.dev/chainguard/python:latest-dev AS builder
WORKDIR /app
RUN python -m venv /app/venv
ENV PATH="/app/venv/bin:$PATH"
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
FROM cgr.dev/chainguard/python:latest
WORKDIR /app
COPY . .
COPY --from=builder /app/venv /app/venv
ENV PATH="/app/venv/bin:$PATH"
EXPOSE 8000
CMD ["python", "app.py"]
