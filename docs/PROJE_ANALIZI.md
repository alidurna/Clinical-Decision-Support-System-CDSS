# CDSS Proje Analizi

**Tarih:** 10 Şubat 2025  
**Proje:** Clinical Decision Support System (CDSS)

---

## 1. Genel Bakış

CDSS, doktor ve hasta odaklı bir klinik karar destek sistemidir. Mikro servis mimarisi ile tasarlanmış; frontend React, backend Java Spring Boot, yapay zeka katmanı Python ile geliştirilecektir.

| Katman        | Teknoloji              | Durum        |
|---------------|------------------------|-------------|
| Frontend      | React 18, TypeScript, Vite, MUI | ✅ Çalışır iskelet |
| Backend       | Java 17, Spring Boot   | ⚠️ Sadece uygulama sınıfları |
| AI Service    | Python, Flask          | ⚠️ Placeholder endpoint'ler |
| Veritabanı    | PostgreSQL             | ✅ docker-compose'da tanımlı |
| Orchestration | Docker Compose         | ✅ Tanımlı |

---

## 2. Proje Yapısı

```
Clinical-Decision-Support-System-CDSS/
├── .github/workflows/     # CI: python-package-conda.yml (conda/env eksik)
├── .gitignore
├── README.md
├── docker-compose.yml     # 8 servis: gateway, auth, patient, doctor, notification, ai, postgres, frontend
├── apps/                  # Micro frontend'ler
│   ├── shell/            # React host (SPA), routing, tema, port 5173
│   ├── auth/             # Login micro frontend, port 5174
│   └── dashboard/        # Dashboard micro frontend, port 5175
├── backend/
│   ├── api-gateway/      # Spring Cloud Gateway, port 8080
│   ├── auth-service/     # Spring Boot, JWT, JPA, PostgreSQL, port 8081
│   ├── patient-service/  # Spring Boot, JPA, port 8082
│   ├── doctor-service/   # Spring Boot, JPA, port 8083
│   └── notification-service/  # Spring Boot, port 8084
└── ai-service/
    ├── app.py            # Flask: /health, /predict, /analyze (placeholder)
    ├── requirements.txt  # flask, numpy, pandas, scikit-learn, tensorflow, gunicorn
    └── Dockerfile
```

---

## 3. Detaylı Analiz

### 3.1 Frontend (React)

- **Paketler:** react, react-dom, react-router-dom, axios, @mui/material, @mui/icons-material, @emotion/react, @emotion/styled, vite, typescript, @vitejs/plugin-react.
- **Sayfalar:** `/` (Home), `/login` (Login), `/dashboard` (Dashboard). Gerçek API çağrısı yok; Login sadece `/dashboard`’a yönlendiriyor.
- **API proxy:** Vite ile `/api` → `http://localhost:8080` tanımlı.
- **Eksikler:**
  - `frontend/nginx.conf` yok; production Docker build’de `COPY nginx.conf` hata verir.
  - `docker-compose` frontend portu 3000; Dockerfile ise nginx ile 80 expose ediyor (port eşlemesi 3000:3000 olunca container içi 3000’de nginx çalışmıyor; 3000:80 olmalı veya Dockerfile’da EXPOSE 3000 + nginx 3000 dinlemeli).
  - Auth state (context/store), API client (axios instance), hata yönetimi ve ortam değişkenleri (.env) yok.

### 3.2 Backend (Java Spring Boot)

- **api-gateway:** Spring Cloud Gateway. Route’lar: `/api/auth/**`, `/api/patients/**`, `/api/doctors/**`, `/api/notifications/**`, `/api/ai/**`. Sadece `ApiGatewayApplication.java` var; yapılandırma application.yml’de.
- **auth-service:** Web, JPA, Security, PostgreSQL, JWT (jjwt) bağımlılıkları var. Sadece `AuthServiceApplication.java` mevcut; controller, entity, repository, security config yok.
- **patient-service / doctor-service:** Web, JPA, PostgreSQL, actuator. Sadece main application sınıfları var; controller/entity/repository yok.
- **notification-service:** Web, actuator. Controller yok.

**Özet:** Backend tamamen iskelet; hiçbir REST endpoint veya veritabanı modeli yok.

### 3.3 AI Service (Python)

- **Flask uygulaması:** `/health` (200 + status), `/predict` (POST, sabit örnek cevap), `/analyze` (POST, sabit örnek cevap).
- **Bağımlılıklar:** flask, flask-cors, numpy, pandas, scikit-learn, tensorflow, requests, python-dotenv, gunicorn.
- **Eksikler:** Gerçek model yükleme/tahmin yok; `request.json` kullanılıyor ama sonuç sabit. TensorFlow kullanılmıyor.

### 3.4 Docker & Orchestration

- **docker-compose.yml:** api-gateway, auth-service, patient-service, doctor-service, notification-service, ai-service, postgres, frontend. Hepsi `cdss-network`’te.
- **PostgreSQL:** Tek instance; `POSTGRES_DB=cdss` ile tek veritabanı. Servisler ayrı DB bekliyor (örn. cdss_auth, cdss_patient, cdss_doctor); compose’da sadece tek DB var, bu yüzden başlangıçta auth/patient/doctor aynı DB’ye bağlanır veya hata alır. Ayrı DB’ler için init script veya ayrı volume/container düşünülmeli.
- **Frontend:** `REACT_APP_API_URL=http://localhost:8080`; container içinden `localhost` backend’e erişemez. `http://api-gateway:8080` veya gateway’in dış host’u kullanılmalı (client tarayıcıda çalıştığı için aslında tarayıcıda `localhost:8080` doğru; sadece container’da build anında kullanılıyorsa sorun olabilir).

### 3.5 CI/CD

- **.github/workflows/python-package-conda.yml:** Push’ta tetikleniyor. Python 3.10, conda, `conda env update --file environment.yml --name base` ve flake8, pytest çalıştırıyor.
- **Eksik:** Proje kökünde `environment.yml` yok; workflow fail eder. Ayrıca proje çoklu dil (Java, Node, Python); sadece Python için tek workflow var.

---

## 4. Tespit Edilen Sorunlar ve Eksikler

| # | Sorun / Eksik | Öncelik |
|---|----------------|--------|
| 1 | `frontend/nginx.conf` dosyası yok; frontend Docker build hata verir. | Yüksek |
| 2 | Frontend Docker: port 3000 vs 80 uyumsuzluğu. | Yüksek |
| 3 | Backend’de hiç REST controller/entity/repository yok. | Yüksek |
| 4 | PostgreSQL: tek DB; servisler ayrı DB bekliyor (cdss_auth, cdss_patient, cdss_doctor). | Orta |
| 5 | GitHub Actions: `environment.yml` yok; conda workflow fail eder. | Orta |
| 6 | AI servisi: gerçek model ve tahmin/analiz mantığı yok. | Orta |
| 7 | Frontend: auth state, API client, .env örnek dosyası yok. | Orta |
| 8 | Login sayfası backend’e istek atmıyor; sadece client-side yönlendirme. | Düşük (backend hazır olunca) |

---

## 5. Önerilen Sonraki Adımlar

1. **Frontend Docker:** `frontend/nginx.conf` ekle; SPA fallback (try_files) ile `index.html` dönsün. Port 80 veya 3000 tutarlı olacak şekilde compose ve Dockerfile’ı güncelle.
2. **Backend:** Her serviste en az bir health/readiness endpoint (ve gerekirse actuator) + birer örnek controller (auth: login/register, patient: CRUD, doctor: CRUD, notification: send) ve JPA entity/repository ekle.
3. **Veritabanı:** docker-compose’da PostgreSQL init script ile `cdss_auth`, `cdss_patient`, `cdss_doctor` veritabanlarını oluştur; servis connection string’lerini buna göre ayarla.
4. **CI/CD:** `environment.yml` ekle (veya workflow’u ai-service’e özel pip/venv ile değiştir); isteğe bağlı Java/Node build ve test adımları ekle.
5. **AI Service:** Basit bir sklearn veya TensorFlow modeli (örn. demo risk skoru) yükleyip `/predict` ve `/analyze`’da kullan; input validasyonu ekle.
6. **Frontend:** Axios instance (baseURL, interceptors), basit auth context (token saklama), `.env.example` ve login’in gerçekten auth-service’e istek atması.

---

## 6. Özet

Proje, mimari ve teknoloji seçimi açısından tutarlı bir CDSS iskeletine sahip. Frontend çalışır durumda; backend ve AI servisi sadece uygulama giriş noktaları ve yapılandırma seviyesinde. Production’a yaklaşmak için Docker (nginx + port), veritabanı, REST API’ler, AI mantığı ve CI/CD eksiklerinin giderilmesi gerekiyor. Bu dokümandaki “Tespit Edilen Sorunlar” ve “Önerilen Sonraki Adımlar” sırasıyla uygulanabilir.
