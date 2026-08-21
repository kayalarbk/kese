# Kese — Harcama Defteri

Günlük gelir ve gider takibi için tek dosyalık, kurulum gerektirmeyen bir PWA.
Vanilla HTML/CSS/JS ile yazıldı; derleme adımı, bağımlılık yönetimi ve sunucu
tarafı yok. Tüm veri tarayıcıda `localStorage` içinde (`kese-v1` anahtarı)
tutulur — hiçbir kayıt dışarı gönderilmez.

## Özellikler

- Gelir ve gider kaydı; kart / nakit ödeme türü ayrımı
- Kategori yönetimi, kategori renkleri ve 41 parçalık inline SVG ikon seti
- Bütçe halkası, aylık net özet ve son işlemler
- İstatistik ekranı: dönem seçici (Hafta / Ay / 3 Ay / Yıl / Özel), KPI şeridi,
  donut, gelir-gider bar, kümülatif seyir, kart-nakit kırılımı — Chart.js 4.4.1
- Lacivert + açık tema, tamamı CSS değişkeni üzerinden
- Silmede onay diyaloğu ve geri al desteği
- 44px dokunma hedefleri, `:focus-visible`, `prefers-reduced-motion`,
  iOS `safe-area` desteği
- Çevrimdışı çalışma: service worker uygulama kabuğunu ve CDN varlıklarını
  önbelleğe alır

## Çalıştırma

Statik dosyalar olduğu için herhangi bir HTTP sunucusu yeterli. Service worker
`file://` üzerinden çalışmaz, bu yüzden sunucu üzerinden açılmalı:

```bash
python -m http.server 8000
# http://localhost:8000
```

## Dosyalar

| Dosya | İçerik |
| --- | --- |
| `index.html` | Uygulamanın tamamı — işaretleme, stil, mantık |
| `manifest.json` | PWA manifesti |
| `sw.js` | Service worker (`kese-v2` önbelleği) |
| `PROGRESS.md` | Sürüm notları, bilinen sorunlar, sonraki adımlar |
| `TEST.md` | Elle test kontrol listesi |

## Bilinen eksikler

- Uygulama ikonları (`icon-192.png`, `icon-512.png`, `icon-512-maskable.png`)
  henüz üretilmedi; "ana ekrana ekle" jenerik ikon gösterir.
- Tekrar eden işlem alanı kaydediliyor ama otomatik kayıt üretmiyor.
- İşlem düzenleme yok, yalnızca silme + geri al var.

Ayrıntılar için `PROGRESS.md`.
