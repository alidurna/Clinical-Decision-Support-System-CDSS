# CDSS Frontend (Micro Frontend)

React tabanlı shell (host) uygulaması. Login ve Dashboard micro frontend olarak ayrı uygulamalardan yüklenir. Proje **pnpm workspace** ile yönetilir.

## Mimari

- **Shell (apps/shell)** – Port 5173. Ana uygulama, routing, tema. Remote’ları yükler.
- **Auth (apps/auth)** – Port 5174. Giriş sayfası (Login).
- **Dashboard (apps/dashboard)** – Port 5175. Dashboard sayfası.

## Kurulum (pnpm)

Proje **kökinden** tek komutla tüm bağımlılıkları yükle:

```bash
pnpm install
```

## Geliştirme

**Tüm micro frontend’leri paralel çalıştır (proje kökünden):**

```bash
pnpm dev
```

Tek tek çalıştırmak için (kökten):

```bash
pnpm dev:shell
pnpm dev:auth
pnpm dev:dashboard
```

Veya bu klasörden: `pnpm run dev`

Ana uygulama: **http://localhost:5173**

## Build

Proje kökünden tüm uygulamaları build et:

```bash
pnpm build
```

Sadece micro frontend’ler: `pnpm build:apps`

