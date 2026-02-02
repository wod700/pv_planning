FROM python:3.11-slim

WORKDIR /app

ENV MPLBACKEND=Agg \
    PYTHONUNBUFFERED=1 \
    PORT=8080

# Upgrade pip en installeer dependencies
RUN pip install --no-cache-dir --upgrade pip

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy alle code
COPY . .

# Maak output map schrijfbaar (vaak nodig voor matplotlib cache / pandas temp files)
RUN mkdir -p output/archive && chmod -R 777 output

# Expose Cloud Run poort
EXPOSE 8080

# Dynamische poort + bind op alle interfaces
CMD ["sh", "-c", "streamlit run dashboard.py \
    --server.port=${PORT} \
    --server.address=0.0.0.0 \
    --server.headless=true \
    --server.enableCORS=false \
    --server.enableXsrfProtection=false"]
