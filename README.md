# Clinical Decision Support System (CDSS)
# Design architect: Captain Ali Durna of the Atılgan ship.

Clinical Decision Support System (CDSS), hem doktorlar hem de hastalar için tasarlanmış kapsamlı bir klinik karar destek sistemidir. Doktorlar için, hasta verilerini hızlıca analiz ederek tanı, tedavi ve ilaç önerileri sunan akıllı bir asistan görevi görür. Sistem, hasta geçmişi, laboratuvar sonuçları, ilaç bilgileri ve diğer klinik verileri bir araya getirerek, kanıta dayalı tıp prensiplerine uygun öneriler üretir ve doktorların daha doğru kararlar vermesine yardımcı olur.

Hastalar ve kullanıcılar için ise, kendi sağlık verilerini görüntüleyebilecekleri, ilaç etkileşimlerini kontrol edebilecekleri ve tedavi süreçlerini takip edebilecekleri kullanıcı dostu bir platform sunar. Sistem, kullanıcıların sağlık durumlarını daha iyi anlamalarına ve doktorlarıyla daha etkili iletişim kurmalarına olanak tanır.

CDSS, gerçek zamanlı veri analizi yaparak kritik durumlarda hem doktorlara hem de kullanıcılara anında uyarılar sağlar. Bu sayede tıbbi hataların azaltılması, hasta güvenliğinin artırılması ve tedavi süreçlerinin optimize edilmesi hedeflenmektedir. Sistem, modern sağlık teknolojileri ve yapay zeka algoritmaları kullanarak, hem sağlık profesyonellerinin hem de hastaların ihtiyaçlarına göre özelleştirilebilir bir yapıda tasarlanmıştır.

## 🏗️ Mimari

Proje mikro servis mimarisi ile geliştirilmiştir:

- **Frontend**: React.js
- **Backend**: Java Spring Boot (Mikro Servisler)
- **AI Service**: Python (Flask/FastAPI)
- **Database**: PostgreSQL
- **Orchestration**: Docker & Docker Compose

## 📁 Proje Yapısı

```
Clinical-Decision-Support-System-CDSS/
├── frontend/                 # React frontend uygulaması
├── backend/
│   ├── api-gateway/         # API Gateway servisi
│   ├── auth-service/        # Kimlik doğrulama servisi
│   ├── patient-service/     # Hasta yönetim servisi
│   ├── doctor-service/      # Doktor yönetim servisi
│   └── notification-service/# Bildirim servisi
├── ai-service/              # Python AI/ML servisi
├── docker/                  # Docker yapılandırmaları
└── docker-compose.yml       # Servis orchestration
```

## 🚀 Hızlı Başlangıç

### Gereksinimler

- Docker & Docker Compose
- Node.js 18+ (Frontend geliştirme için)
- Java 17+ (Backend geliştirme için)
- Python 3.9+ (AI servis geliştirme için)

### Tüm Servisleri Çalıştırma

```bash
docker-compose up -d
```

Frontend: http://localhost:3000
API Gateway: http://localhost:8080
AI Service: http://localhost:5000

### Geliştirme Modu
PROJE YAPIM AŞAMASINDA
Her servis ayrı ayrı çalıştırılabilir. Detaylar için ilgili servis klasöründeki README dosyalarına bakın.

## 🔧 Teknolojiler

- **Frontend**: React, TypeScript, Material-UI
- **Backend**: Spring Boot, Spring Cloud, JPA
- **AI/ML**: Python, TensorFlow/PyTorch, scikit-learn
- **Database**: PostgreSQL
- **Containerization**: Docker, Docker Compose
