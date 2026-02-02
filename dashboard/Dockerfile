FROM python:3.11-slim

WORKDIR /app

ENV MPLBACKEND=Agg
ENV PYTHONUNBUFFERED=1

# (optioneel maar handig) pip up-to-date
RUN pip install --no-cache-dir --upgrade pip

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

# Maak output map schrijfbaar (handig voor archives / matplotlib cache)
RUN mkdir -p output/archive && chmod -R 777 output

EXPOSE 8080

# Cloud Run: luister op $PORT en bind op 0.0.0.0
CMD ["sh","-c","streamlit run dashboard.py --server.port=${PORT:-8080} --server.address=0.0.0.0 --server.headless=true --browser.gatherUsageStats=false"]
