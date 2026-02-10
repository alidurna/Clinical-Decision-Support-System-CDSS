# Clinical Decision Support System (CDSS)
# Design architect: Captain Ali Durna of the Atılgan ship.

Clinical Decision Support System (CDSS), hem doktorlar hem de hastalar için tasarlanmış kapsamlı bir klinik karar destek sistemidir. Doktorlar için, hasta verilerini hızlıca analiz ederek tanı, tedavi ve ilaç önerileri sunan akıllı bir asistan görevi görür. Sistem, hasta geçmişi, laboratuvar sonuçları, ilaç bilgileri ve diğer klinik verileri bir araya getirerek, kanıta dayalı tıp prensiplerine uygun öneriler üretir ve doktorların daha doğru kararlar vermesine yardımcı olur.

Hastalar ve kullanıcılar için ise, kendi sağlık verilerini görüntüleyebilecekleri, ilaç etkileşimlerini kontrol edebilecekleri ve tedavi süreçlerini takip edebilecekleri kullanıcı dostu bir platform sunar. Sistem, kullanıcıların sağlık durumlarını daha iyi anlamalarına ve doktorlarıyla daha etkili iletişim kurmalarına olanak tanır.

CDSS, gerçek zamanlı veri analizi yaparak kritik durumlarda hem doktorlara hem de kullanıcılara anında uyarılar sağlar. Bu sayede tıbbi hataların azaltılması, hasta güvenliğinin artırılması ve tedavi süreçlerinin optimize edilmesi hedeflenmektedir. Sistem, modern sağlık teknolojileri ve yapay zeka algoritmaları kullanarak, hem sağlık profesyonellerinin hem de hastaların ihtiyaçlarına göre özelleştirilebilir bir yapıda tasarlanmıştır.

## 🏗️ Mimari

Proje **mikro servis** (backend) ve **micro frontend** (frontend) mimarisi ile geliştirilmiştir:

- **Frontend**: React, TypeScript, Vite — **Micro Frontend** (Module Federation), pnpm workspace
- **Backend**: Java Spring Boot (Mikro Servisler)
- **AI Service**: Python (Flask/FastAPI)
- **Database**: PostgreSQL
- **Orchestration**: Docker & Docker Compose

## 📱 Micro Frontend (Frontend Mimarisi)

Frontend, **Module Federation** (Vite plugin) ile parçalara ayrılmıştır; her uygulama bağımsız geliştirilebilir ve tek shell içinde birleştirilir.

| Uygulama   | Klasör        | Port | Açıklama |
|------------|---------------|------|----------|
| **Shell**  | `apps/shell`  | 5173 | Ana uygulama (host): routing, tema, remote’ları yükler |
| **Auth**   | `apps/auth`   | 5174 | Giriş sayfası (Login) — remote |
| **Dashboard** | `apps/dashboard` | 5175 | Dashboard sayfası — remote |

- **pnpm workspace**: Tüm frontend uygulamaları `apps/` altında, tek `pnpm install` ile kurulur.
- Detaylı anlatım: [apps/README.md](apps/README.md)

## 📁 Proje Yapısı

```
Clinical-Decision-Support-System-CDSS/
├── apps/                        # Micro frontend (pnpm workspace)
│   ├── shell/                   # Host uygulama — port 5173
│   ├── auth/                    # Login remote — port 5174
│   └── dashboard/               # Dashboard remote — port 5175
├── backend/
│   ├── api-gateway/             # API Gateway — port 8080
│   ├── auth-service/            # Kimlik doğrulama
│   ├── patient-service/         # Hasta yönetimi
│   ├── doctor-service/          # Doktor yönetimi
│   └── notification-service/   # Bildirim servisi
├── ai-service/                  # Python AI/ML servisi — port 5000
├── docker/                      # Docker yapılandırmaları
├── package.json                 # Kök script'ler (pnpm dev, pnpm build)
├── pnpm-workspace.yaml          # Workspace tanımı (apps/*)
└── docker-compose.yml           # Tüm servisler
```

## 🚀 Hızlı Başlangıç

### Gereksinimler

- **pnpm** (frontend için önerilen) veya Node.js 18+
- Docker & Docker Compose (tüm stack için)
- Java 17+ (backend geliştirme)
- Python 3.9+ (AI servisi geliştirme)

### Frontend çalıştırma (Micro Frontend)

```bash
# Bağımlılıkları kur (proje kökünden)
pnpm install

# Shell + Auth + Dashboard'u paralel başlat
pnpm dev
```

- **Ana uygulama:** http://localhost:5173  
- Login ve Dashboard bu adres üzerinden remote olarak yüklenir.

Tek tek çalıştırmak: `pnpm dev:shell` | `pnpm dev:auth` | `pnpm dev:dashboard`

### Tüm servisleri Docker ile çalıştırma

```bash
docker-compose up -d
```

| Servis      | Adres |
|-------------|--------|
| Frontend    | http://localhost:3000 |
| API Gateway | http://localhost:8080 |
| AI Service  | http://localhost:5000 |

### Geliştirme modu

Her servis ayrı ayrı çalıştırılabilir. Detaylar için ilgili klasördeki README dosyalarına bakın (örn. `apps/README.md`, `apps/shell/README.md`).

## 🔧 Teknolojiler

- **Frontend**: React, TypeScript, Vite, Material-UI, Module Federation (micro frontend), pnpm workspace
- **Backend**: Spring Boot, Spring Cloud, JPA
- **AI/ML**: Python, TensorFlow/PyTorch, scikit-learn
- **Database**: PostgreSQL
- **Containerization**: Docker, Docker Compose
