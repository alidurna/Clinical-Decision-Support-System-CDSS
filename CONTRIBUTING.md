# Branch'ler ve Görev Dağılımı

Proje iş bölümü için **3 branch** kullanılıyor. Her branch’i çekip kendi alanında geliştirme yap, bitince `main`’e merge edin.

## Branch'ler

| Branch | İçerik | Çalışma alanı |
|--------|--------|----------------|
| **main** | Ana branch. Tamamlanan özellikler buraya merge edilir. | — |
| **feature/intro** | **Giriş / tanıtım sayfası** — Projeyi tanıtan, karşılama sayfası. | `apps/shell/src/pages/Home.tsx` |
| **feature/login** | **Giriş yap** — Login sayfası. | `apps/auth/` (Login bileşeni) |
| **feature/register** | **Kayıt ol** — Kayıt (register) sayfası. | `apps/auth/` (Register bileşeni eklenmeli) |

## Çalışma akışı

1. **Branch’i çek:**
   ```bash
   git fetch origin
   git checkout feature/intro    # veya feature/login  veya  feature/register
   ```

2. **Geliştirme yap**, commit’le:
   ```bash
   git add .
   git commit -m "feat: ..."
   ```

3. **GitHub’a gönder:**
   ```bash
   git push origin feature/intro
   # veya  git push origin feature/login
   # veya  git push origin feature/register
   ```

4. **Bitince:** GitHub’da Pull Request aç → `main`’e merge.

## Not

- **feature/intro** → Tanıtım sayfası (shell’deki Home).
- **feature/login** → Sadece “Giriş yap” (apps/auth içindeki mevcut Login).
- **feature/register** → “Kayıt ol” sayfası; `apps/auth` içine yeni Register bileşeni/sayfası eklenir.
