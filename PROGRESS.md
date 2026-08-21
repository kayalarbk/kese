# Kese — PROGRESS

Kişisel harcama takip PWA'sı. Vanilla HTML/CSS/JS, tek dosya (`index.html`),
tek storage anahtarı (`kese-v1`).

---

## Sürüm 2.0 — Lacivert tema revizyonu

### Analiz bulguları (v1.x)
- ~14 hard-coded renk CSS ve JS içine dağılmıştı (`#222A44`, `${color}22`, `rgba(...)`).
- Beş ayrı buton dili: `.btn`, `.qbtn`, `.opt`, `.chip`, `.sg`.
- `.del` (~24px) ve `.sw` (30px) dokunma hedefleri 44px altındaydı.
- 11 farklı font boyutu, 3 font ailesi, 8 farklı boşluk değeri.
- Emoji ikonlar platformlar arası tutarsız render oluyordu.
- Grafikler el yapımıydı: tooltip, eksen, dokunma etkileşimi yoktu.
- Veri modelinde ödeme türü, gelir kaydı ve kart bilgisi yoktu.

### Yapıldı
- [x] **Token katmanı.** Tüm renk/boşluk/yarıçap/tipografi `:root` altında. Kod
      içinde hard-coded hex kalmadı; tek istisna kategori renkleri (`COLORS`
      dizisi, kullanıcı verisinin parçası).
- [x] **Lacivert + açık tema.** Zemin `--bg`, kartlar `--surface`, header ve alt
      menü `--navy-900`. Tek gradient: Ekle ekranının tutar kartı
      (`--navy-900 → --navy-600`). Gölgeler nötr, `0 2px 8px rgba(11,27,58,.06)`.
- [x] **Emoji temizliği.** 41 ikonluk inline SVG seti (1.5px stroke, 24px,
      `currentColor`). Kategori ikonu = SVG + kategori rengi. Başlık, buton ve
      bildirimlerde emoji yok.
- [x] **Ekleme ekranı yeniden tasarım.** Tutar en üstte (36px, tabular-nums,
      numeric klavye), Gelir/Gider segmented, kategori 4 sütunlu ikon grid,
      Ödeme türü segmented (varsayılan Kart) + koşullu kart dropdown'ı,
      Tarih/Saat ikili satır, açıklama, tekrar eden işlem. Kaydet sticky ve form
      geçersizken disabled. Kayıt sonrası haptic + toast + form sıfırlama.
- [x] **Veri modeli.** `paymentMethod: "card" | "cash"`, `type`, `cardId`,
      `repeat` alanları eklendi. `migrate()` eski kayıtlara `paymentMethod:"card"`
      ve `type:"expense"` atıyor; hiçbir kayıt silinmiyor. Emoji ikonlar
      `EMOJI_MAP` ile isim tabanlı ikona çevriliyor (`catSeed: 3`).
- [x] **Özet sadeleştirildi.** Bütçe halkası, gelir/gider/net, kümülatif ay
      seyri, kategori kırılımı, son 5 işlem. Ödeme türü kırılımı özette yok.
- [x] **İstatistik.** Chart.js 4.4.1. Dönem seçici (Hafta/Ay/3 Ay/Yıl/Özel,
      sticky), KPI şeridi (toplam, % değişim, günlük ortalama, en yüksek gün),
      donut + yüzde listesi, aylık gelir-gider bar, kümülatif line (geçen dönem
      kesikli), kart/nakit stacked bar, en çok harcanan 5 kategori, en büyük 5
      işlem. Her blokta boş durum.
- [x] **Bileşenler.** `.card`, `.btn`, `.seg`, `.tile`, `.kpi`, `.li`, `.chartbox`,
      `emptyState()`, `confirmDlg()`, `toast()`, `openSheet()`.
- [x] Silmede onay diyaloğu + geri al toast'ı (işlem, kategori, kart, sıfırlama).
- [x] 44px dokunma hedefleri, `:focus-visible`, `prefers-reduced-motion`,
      iOS `safe-area`, loading skeleton.
- [x] PWA: `manifest.json` yeni tema rengiyle, `sw.js` cache sürümü `kese-v2`,
      Chart.js ve font CDN'i önbelleğe alınıyor.

### Yapılmadı / bilinen sorunlar
- **İkon dosyaları yok.** `icon-192.png`, `icon-512.png`,
  `icon-512-maskable.png` üretilmedi. Manifest bunlara işaret ediyor; dosyalar
  eklenene kadar "ana ekrana ekle" ikonu jenerik görünür.
- **Tekrar eden işlem** alanı kaydediliyor ama henüz otomatik kayıt üretmiyor.
  Zamanlayıcı mantığı yazılmadı.
- **İşlem düzenleme yok.** Sadece silme + geri al var.
- **Chart.js CDN'den geliyor.** İlk açılış çevrimdışıysa istatistik ekranı boş
  durum gösterir. İkinci açılıştan itibaren SW önbelleğinden gelir.
- **Kategori sıralaması sabit.** Sürükle-bırak sıralama yok.
- Kur/çoklu para birimi yok, tek para birimi ₺.
- Gelir kategorileri bütçe halkasına dahil değil (tasarım kararı).

### Sonraki adımlar
1. Uygulama ikonlarını üret, manifest'i doğrula.
2. Tekrar eden işlemler için açılışta "vadesi gelenleri oluştur" kontrolü.
3. İşlem düzenleme (uzun basma → düzenle sayfası).
4. Kategori bazlı alt limitler ve limit aşımı uyarısı.
