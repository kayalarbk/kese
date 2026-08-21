# Kese — Harcama Defteri

Günlük gelir ve gider takibi için tek dosyalık, kurulum gerektirmeyen bir PWA.
Vanilla HTML/CSS/JS ile yazıldı; derleme adımı, bağımlılık yönetimi ve sunucu
tarafı yok. Tüm veri tarayıcıda `localStorage` içinde (`kese-v1` anahtarı)
tutulur — hiçbir kayıt dışarı gönderilmez.

**Canlı:** https://kayalarbk.github.io/kese/

## Özellikler

### Kayıt
- Gün gün **dosyalanan** işlem listesi. Bir güne dokununca o günün özeti ve
  işlemleri açılır.
- **Sola kaydırarak silme.** Satır kaydırıldığında kırmızı "Sil" alanı çıkar;
  yarıdan fazla kaydırma doğrudan siler.
- **Düzenleme.** İşleme dokunmak tutar, tür, kategori, ödeme türü, kart, tarih,
  saat ve açıklamayı değiştirebileceğin paneli açar.
- **Geri dönüşüm kutusu.** Silinen kayıt 24 saat kutuda bekler, sonra kalıcı
  silinir. Bu süre boyunca hiçbir toplama veya grafiğe dahil edilmez; tek tek
  geri yüklenebilir.
- Kategoriler açılan bir panelden seçilir; kart / nakit ayrımı yapılır.

### Kullanım modu
İlk açılıştaki karşılama akışında ne kaydedeceğini seçersin:

| Mod | Etkisi |
| --- | --- |
| Sadece gider | Ekleme ekranında gelir alanı hiç görünmez, bütçeyi kendin belirlersin |
| Gelir ve gider | Bütçe elle girilmez, dönem gelirinin seçtiğin yüzdesi olur |
| Sadece gelir | Bütçe ve harcama halkası kurulmaz, özet gelir toplamını gösterir |

Gelir de kaydediliyorsa bütçe sabit bir rakam değildir: gelir kaydettikçe bütçe
kendiliğinden güncellenir, geri kalan kısım tasarruf hedefi olarak gösterilir.

### İstatistik
- KPI şeridi: gider, gelir, net, tasarruf oranı, günlük ortalama, işlem sayısı
- Geçen dönemle **takvimsel** karşılaştırma (yarım ay, geçen ayın aynı
  uzunluktaki dilimiyle kıyaslanır — tamamlanmış ayla değil)
- Ay sonu projeksiyonu: tahmini gider, bütçe aşımı/payı, kalan günler için
  günlük harcama sınırı
- Günlük harcama çubukları + 7 günlük hareketli ortalama
- İşlem büyüklüğü: ortalama, medyan, standart sapma, en küçük–en büyük
- Kategori tablosu: tutar, pay, işlem sayısı, ortalama işlem, önceki döneme fark
- Haftanın günü ve günün saati profilleri
- Aylık gelir/gider çubukları + net çizgisi, kümülatif seyir, kart/nakit kırılımı
- CSV dışa aktarma

### Arayüz
- Açılışta "KE" lacivert / "SE" altın sarısı animasyonlu giriş
- Lacivert + açık tema, tamamı CSS değişkeni üzerinden
- 41 parçalık inline SVG ikon seti
- **iPhone için ayarlı:** zoom kapalı (çift dokunuş, pinch ve girdi odağı dahil),
  Dynamic Island ve ana ekran çizgisi güvenli alanları hesaba katılıyor,
  yatay modda kavisli köşeler korunuyor
- 44px dokunma hedefleri, `:focus-visible`, `prefers-reduced-motion`
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
| `sw.js` | Service worker (`kese-v3` önbelleği) |
| `PROGRESS.md` | Sürüm notları, bilinen sorunlar, sonraki adımlar |
| `TEST.md` | Elle test kontrol listesi |

## Bilinen eksikler

- Uygulama ikonları (`icon-192.png`, `icon-512.png`, `icon-512-maskable.png`)
  henüz üretilmedi; "ana ekrana ekle" jenerik ikon gösterir.
- Tekrar eden işlem alanı kaydediliyor ama otomatik kayıt üretmiyor.
- Kaydırarak silme yalnızca dokunmatik cihazlarda; masaüstünde düzenleme
  panelindeki silme butonu kullanılır.
- Chart.js CDN'den geliyor; ilk açılış çevrimdışıysa istatistik boş görünür.
- Zoom kapatıldığı için sayfa büyütülemez — bilinçli bir tercih.

Ayrıntılar için `PROGRESS.md`.
