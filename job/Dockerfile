FROM python:3.11-slim

WORKDIR /app

# matplotlib headless
ENV MPLBACKEND=Agg
ENV PYTHONUNBUFFERED=1

COPY requirements.txt /app/
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

ENV PORT=8080
EXPOSE 8080

CMD ["streamlit", "run", "dashboard.py", "--server.port=8080", "--server.address=0.0.0.0"]