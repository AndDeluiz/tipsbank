# syntax=docker/dockerfile:1.7

# =============================================================================
# STAGE 1 — builder (Python 3.15-slim)
# =============================================================================
FROM python:3.15-slim-bookworm AS builder

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir --no-compile --target=/packages -r requirements.txt

COPY main.py .

# =============================================================================
# STAGE 2 — runtime (Distroless Python, sem shell, sem package manager)
# Chainguard latest currently uses Python 3.15; keep this aligned with the builder.
# =============================================================================
FROM cgr.dev/chainguard/python:latest

WORKDIR /app

COPY --from=builder /packages /packages
COPY --from=builder /app/main.py /app/main.py

ENV PYTHONUNBUFFERED=1 \
    PYTHONDONTWRITEBYTECODE=1 \
    PYTHONPATH=/packages \
    PATH=/packages/bin:$PATH

EXPOSE 8080

ENTRYPOINT ["python3", "-m", "uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8080"]
