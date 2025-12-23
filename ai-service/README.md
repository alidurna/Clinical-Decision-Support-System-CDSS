# CDSS AI Service

Python tabanlı yapay zeka servisi. Makine öğrenimi modelleri ve veri analizi için kullanılır.

## Kurulum

```bash
python -m venv venv
source venv/bin/activate  # Linux/Mac
# veya
venv\Scripts\activate  # Windows

pip install -r requirements.txt
```

## Çalıştırma

```bash
python app.py
```

Servis http://localhost:5000 adresinde çalışacaktır.

## Endpoints

- `GET /health` - Health check
- `POST /predict` - AI tahmin endpoint'i
- `POST /analyze` - Hasta verisi analizi

