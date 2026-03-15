# Kişisel Website Yeniden Tasarımı - Design Spec

**Tarih:** 2026-03-15
**Versiyon:** 1.0
**Status:** Draft

---

## 1. Genel Bakış

Bu spec, mevcut kişisel website'nin (ilkerhalil.github.io) kapsamlı yeniden tasarımını tanımlar. Amaç, modern canlı renkler, yeni içerik bölümleri ve gelişmiş işlevsellik ile daha dikkat çekici ve işlevsel bir site oluşturmaktır.

## 2. Kapsam

### 2.1 Görsel Tasarım
- **Renk Paleti:** Canlı renkler (Akvamarin #06b6d4, Mercan #f97316, Fuşya #ec4899)
- **Tipografi:** Mevcut fontlar korunacak (Lora, DM Sans, DM Mono)
- **Layout:** Tek sayfa (single-page), mevcut yapı korunacak
- **Animasyonlar:** Scroll-triggered, hover efektleri, smooth geçişler

### 2.2 Yeni İçerik Bölümleri
- Projects/Portfolio - Önemli projelerin listesi
- Blog - Teknoloji yazıları ve makaleler
- Testimonials - İş arkadaşlarından/müşterilerden referanslar
- Speaking - Konferans ve sunum geçmişi
- GitHub Özet - Aktif repolar ve contribution grafığı

### 2.3 İşlevsellik Özellikleri
- Theme Toggle - Açık/Koyu mod geçişi
- Sosyal Medya İkonları - Header ve footer'da
- Performans Optimizasyonu - Lazy loading, kod optimizasyonları

---

## 3. Tasarım Kararları

### 3.1 Renk Sistemi

```css
:root {
  /* Light Theme */
  --primary: #06b6d4;    /* Akvamarin */
  --secondary: #f97316;  /* Mercan */
  --accent: #ec4899;     /* Fuşya */
  --bg: #f8fafc;
  --bg-alt: #f1f5f9;
  --text: #0f172a;
  --text-muted: #64748b;
}

[data-theme="dark"] {
  --bg: #0f172a;
  --bg-alt: #1e293b;
  --text: #f8fafc;
  --text-muted: #94a3b8;
}
```

### 3.2 Teknoloji Stack
- Vanilla HTML5, CSS3, JavaScript (ES6+)
- CSS Custom Properties ile theme desteği
- IntersectionObserver API ile scroll animasyonları
- Native lazy loading için loading="lazy" attribute

### 3.3 Bölüm Sırası

```
1. Hero (güncellenecek)
2. Skills (mevcut - renkler güncellenecek)
3. Projects (yeni)
4. Blog (yeni)
5. Testimonials (yeni)
6. Speaking (yeni)
7. GitHub (yeni)
8. Experience (mevcut - renkler güncellenecek)
9. Contact (güncellenecek)
```

---

## 4. Bölüm Detayları

### 4.1 Hero Section
- Mevcut greeting devam edecek
- Renk vurguları canlı tonlarla güncellenecek
- CTA butonları canlı renk gradient'leri alacak

### 4.2 Projects Section
- Grid layout (3 kolon desktop, 1 kolon mobile)
- Her proje kartı: başlık, açıklama, tech stack tags, link
- Hover efekti: kart elevation + border glow

### 4.3 Blog Section
- Son yazıların listesi (max 6)
- Her yazı: başlık, özet, tarih, okuma süresi
- Tags ile kategori gösterimi

### 4.4 Testimonials
- Horizontal scroll veya grid
- Her testimonial: alıntı, isim, pozisyon, şirket
- Profil fotoğrafı placeholder (gravatar veya initial)

### 4.5 Speaking Section
- Timeline formatında geçmiş konuşmalar
- Etkinlik adı, tarih, konu başlığı, konum

### 4.6 GitHub Section
- En aktif 6 repo kartı
- Yıllık contribution grafığı (SVG veya static image)
- Toplam stars, forks sayacı

### 4.7 Contact Section
- Mevcut bilgiler korunacak
- Sosyal medya ikonları eklenecek
- Email, LinkedIn, GitHub linkleri

---

## 5. İşlevsellik

### 5.1 Theme Toggle
- Navbar'da icon buton (güneş/ay ikonu)
- localStorage ile tercih kaydedilecek
- CSS variables üzerinden anlık theme değişimi

### 5.2 Animasyonlar
- `.reveal` class ile scroll-triggered fade-in
- Hoverefektleri: transform scale, box-shadow
- Buton hover: background gradient geçişi

### 5.3 Performans
- Images: loading="lazy"
- CSS: minify, kritik CSS inline
- JS: defer loading
- Font: font-display: swap

---

## 6. Mobil Uyumluluk

- Responsive breakpoints: 480px, 768px, 1024px
- Hamburger menu mobile nav için
- Grid: 1 kolon mobile, 2 tablet, 3+ desktop

---

## 7. Dış Bağımlılıklar

- Google Fonts: Lora, DM Sans, DM Mono
- Font Awesome veya SVG ikonlar (sosyal medya)
- GitHub API (public data, rate limit içinde)

---

## 8. Sonraki Adımlar

1. HTML/CSS/JS implementasyonu
2. Manuel test (tüm bölümler, responsive, theme toggle)
3. Deploy ve production test