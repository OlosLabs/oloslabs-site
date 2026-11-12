# Olos Labs — Landing Page (Paket Deploy)

Landing page statis untuk https://oloslabs.com — 100% client-side, tanpa backend, tanpa build step.

## Isi paket

```
oloslabs-site/
├── index.html                                  # Landing page lengkap (satu file: HTML + CSS + JS)
└── assets/
    └── oloslabs-logo-square-v1-2026-10-27.png  # Logo asli (dipakai WebGL particle + fallback)
```

Total: ~92 KB. Sumber eksternal via CDN (tidak perlu di-host):
- three.js r128 — `https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js`
- Google Fonts — Outfit (300/400/500) + Noto Sans SC (300/400/500)

## Fitur yang sudah termasuk

1. Particle WebGL logo Olos Labs — sampling langsung dari PNG asli, morph scatter saat scroll, parallax kursor, warna mengikuti tema
2. Dua bahasa: default **中文 (zh-Hans)**, toggle ke EN di topbar, pilihan tersimpan di localStorage (`olos-lang`), `<html lang>` dinamis
3. Dark/light theme: mengikuti `prefers-color-scheme`, toggle tersimpan di localStorage (`olos-theme`), tombol sun/moon
4. Kontak: `contact@oloslabs.com` bisa diklik (mailto:) di section Contact DAN di bagian Report a vulnerability
5. Section: Hero, Divisions (4 divisi x 3 invariant), Standards, Quality Gate, Origin, House of Brands, Contact, Security, Footer
6. Responsif penuh (desktop + mobile), scrollbar disembunyikan, menghormati `prefers-reduced-motion`
7. Bebas pola tulisan AI-slop: tanpa em dash, tanpa klise, sentence case, klaim terukur

## Cara deploy

### Opsi A — GitHub Pages (rekomendasi, org sudah ada di github.com/OlosLabs)

1. Buat repo baru `OlosLabs/oloslabs.github.io` (nama ini = domain utama org), atau repo lain untuk preview
2. Push seluruh isi folder ini ke branch `main`:
   ```bash
   git init && git add . && git commit -m "Olos Labs landing page"
   git remote add origin https://github.com/OlosLabs/oloslabs.github.io.git
   git push -u origin main
   ```
3. Settings → Pages → Source: `main` branch → Save
4. Custom domain: Settings → Pages → Custom domain: `oloslabs.com` → aktifkan Enforce HTTPS
5. DNS di registrar domain:
   ```
   A     @     185.199.108.153
   A     @     185.199.109.153
   A     @     185.199.110.153
   A     @     185.199.111.153
   CNAME www     <username>.github.io
   ```
6. Tunggu DNS propagate (5 menit - 24 jam), cek https://oloslabs.com

### Opsi B — Cloudflare Pages (lebih cepat, SSL otomatis)

1. Dashboard → Pages → Create project → Upload assets (drag & drop folder ini)
   atau connect Git repo
2. Build settings: kosongkan (output = root)
3. Custom domain: tambahkan `oloslabs.com` + `www.oloslabs.com` → ikuti instruksi DNS
4. Selesai — SSL otomatis

### Opsi C — Vercel / Netlify

Sama: drag & drop folder ini, arahkan domain. Tidak ada build command, tidak ada output directory khusus.

## Verifikasi setelah deploy

- [ ] Hero: partikel logo muncul (tunggu 1-2 detik, sampling berjalan setelah PNG termuat)
- [ ] Toggle 中文/EN mengganti seluruh teks tanpa reload
- [ ] Toggle tema sun/moon mengganti terang/gelap, partikel ikut warna tema
- [ ] `contact@oloslabs.com` bisa diklik di Contact & Security
- [ ] Scroll halaman penuh, partikel menyebar lalu berkumpul kembali
- [ ] Mobile: mark dekat headline (bukan terpisah jauh), nav ringkas (GitHub + tombol)

## Catatan teknis untuk agent

- **Jangan menambahkan framework** (React/Next) — situs ini sengaja statis murni; kebutuhan 100% fungsi sudah terpenuhi client-side
- Jika membutuhkan halaman tambahan di masa depan (House of Brands, per-produk), migrasikan ke **Astro** — struktur konten di index.html sudah bersih dan mudah dipindah
- Semua teks terjemahan berada dalam kamus `D` (EN→ZH) di bagian bawah index.html — edit di sana untuk mengubah copy, ikuti kaidah: tanpa em dash, tanpa kutip keriting, tanpa klise (delve/seamless/unleash/dll), sentence case, klaim selalu terukur
- Partikel mengambil bentuk dari `assets/oloslabs-logo-square-v1-2026-10-27.png`; jika logo di GitHub (`OlosLabs/.github/assets`) diperbarui, ganti file PNG ini dengan versi baru — partikel otomatis mengikuti bentuk barunya
- Parameter partikel di bagian bawah index.html: `fit` (ukuran), `idle` (amplitudo goyang), `size` (ukuran titik), `look` (parallax kursor)

## Kontak

- Domain: https://oloslabs.com
- GitHub: https://github.com/OlosLabs
- Email: contact@oloslabs.com

Copyright (c) 2026 Olos Labs
