FROM python:3.11-slim

WORKDIR /app

ENV MPLBACKEND=Agg
ENV PYTHONUNBUFFERED=1
ENV PORT=8080

COPY requirements.txt /app/
RUN pip install --no-cache-dir -r requirements.txt

COPY . /app/

EXPOSE 8080


RUN mkdir -p /app/output/archive && chmod -R 777 /app/output

# Headless matplotlib (vaak crash oorzaak in containers)
ENV MPLBACKEND=Agg

# Expose de poort die Cloud Run verwacht
EXPOSE 8080

# Dynamische poort: gebruik $PORT (Cloud Run zet dit op 8080), fallback naar 8501 lokaal
CMD streamlit run dashboard.py \
    --server.port=${PORT:-8501} \
    --server.address=0.0.0.0 \
    --server.headless=true \
    --server.enableCORS=false \
    --server.enableXsrfProtection=false
