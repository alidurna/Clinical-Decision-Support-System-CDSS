# CDSS Micro Frontend Uygulamaları

Tüm frontend uygulamaları bu klasör altında toplanmıştır. Proje **pnpm workspace** kullanır.

| Uygulama   | Port | Açıklama                          |
|------------|------|-----------------------------------|
| **shell**  | 5173 | Ana uygulama (host), routing, tema. Remote’ları yükler. |
| **auth**   | 5174 | Giriş sayfası (Login) – remote   |
| **dashboard** | 5175 | Dashboard sayfası – remote     |

## Kurulum (proje kökünden)

```bash
pnpm install
```

## Çalıştırma

**Tek komutla hepsini paralel başlat (önerilen):**

```bash
# Proje kökünden
pnpm dev
```

Tek tek çalıştırmak için:

```bash
pnpm dev:shell      # sadece shell (5173)
pnpm dev:auth       # sadece auth (5174)
pnpm dev:dashboard  # sadece dashboard (5175)
```

Ana giriş: **http://localhost:5173**

Detaylar için `shell/README.md` dosyasına bakın.
