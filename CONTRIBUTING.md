# Branch'ler ve Görev Dağılımı

Proje iş bölümü için 3 branch kullanılıyor. Her branch’i çekip kendi alanında geliştirme yap, bitince `main`’e merge edin.

## Branch'ler

| Branch | İçerik | Kim çalışır |
|--------|--------|-------------|
| **main** | Ana branch. Tamamlanan özellikler buraya merge edilir. | — |
| **feature/intro** | **Giriş / tanıtım sayfası** — Projeyi tanıtan, karşılama sayfası (şu an `apps/shell` içindeki Home sayfası). | Tanıtım sayfasından sorumlu kişi |
| **feature/auth** | **Auth (giriş / kayıt)** — Giriş yap, Kayıt ol sayfaları. `apps/auth` micro frontend. | Auth’tan sorumlu kişi |

## Çalışma akışı

1. **Branch’i çek:**  
   `git fetch origin`  
   `git checkout feature/intro`  veya  `git checkout feature/auth`

2. **Geliştirme yap**, commit’le:  
   `git add .`  
   `git commit -m "feat: ..."`

3. **GitHub’a gönder:**  
   `git push origin feature/intro`  veya  `git push origin feature/auth`

4. **Bitince:** GitHub’da Pull Request aç → `main`’e merge.

## Not

- `feature/intro` → çalışma alanı: `apps/shell/src/pages/Home.tsx` (ve gerekirse shell’deki routing/tema).
- `feature/auth` → çalışma alanı: `apps/auth/` (Login, ileride Kayıt ol bileşeni).
