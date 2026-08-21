# Kese — PROGRESS

Kişisel harcama takip PWA'sı. Vanilla HTML/CSS/JS, tek dosya (`index.html`),
tek storage anahtarı (`kese-v1`).

---

## Sürüm 3.0 — Mobil davranış, günlük dosyalar, karşılama akışı

### Yapıldı

**iOS / PWA davranışı**
- [x] Zoom kapatıldı. Dört katman: viewport'ta `user-scalable=no, maximum-scale=1`,
      `html,body{touch-action:manipulation}` (çift dokunuş), `gesturestart`/
      `gesturechange`/`gestureend` + çok parmaklı `touchmove` engelleme (pinch),
      tüm girdilerde `font-size:16px` (odaklanınca oluşan otomatik zoom).
- [x] `-webkit-text-size-adjust:100%` — Safari'nin otomatik yazı büyütmesi kapalı.
- [x] `overscroll-behavior:none` html ve body'de — lastik gibi çekilme yok.
- [x] Dynamic Island / çentik: `--safe-t` başlık dolgusuna ekleniyor,
      appbar `min-height: safe-t + 56px`.
- [x] Ana ekran çizgisi (home indicator): alt menü yüksekliği `60px + safe-b`,
      `padding-bottom:safe-b`, buton yüksekliği sabit 60px. Hiçbir dokunma
      hedefi çizginin üstüne gelmiyor.
- [x] Yatay güvenli alan: `--safe-l` / `--safe-r` tokenları; appbar, main, nav,
      sheet, dialog ve toast bunları kullanıyor (yatay mod ve kavisli köşeler).
- [x] `-webkit-user-select:none` + `-webkit-touch-callout:none` arayüzde;
      girdi alanlarında seçim açık.
- [x] Alt panel yüksekliği `svh` tabanlı, `overscroll-behavior:contain`.

**Günlük dosyalar**
- [x] İşlemler tek tek listelenmiyor; her gün bir "dosya" kartı. Kartta gün
      numarası, gün adı, işlem sayısı, kategori renk noktaları, günün gideri ve
      varsa geliri var.
- [x] Dosyaya dokununca alt panel açılıyor: günün gider/gelir/işlem sayısı
      özeti, en çok harcanan kategori ve işlem listesi.
- [x] Özet ekranı "Son işlemler" yerine "Son günler" (4 dosya) gösteriyor.

**Kaydırarak silme**
- [x] Çarpı butonu kaldırıldı. Satır sola kaydırılıyor; altından kırmızı zemin
      ve "Sil" etiketi çıkıyor.
- [x] Eksen kilidi: ilk 6px'te yatay/dikey karar veriliyor. Dikeyse sayfa normal
      kayıyor, yataysa `preventDefault` ile sayfa kaydırması durduruluyor.
- [x] Genişliğin %45'ini geçen kaydırma doğrudan siliyor; %55×96px eşiğini geçen
      kaydırma satırı açık bırakıyor, kırmızı alana dokunmak siliyor.

**İşlem düzenleme**
- [x] Satıra dokunmak düzenleme panelini açıyor: tutar, tür, kategori, ödeme
      türü, kart, tarih, saat, açıklama, tekrar.
- [x] Panel taslak nesne üzerinde çalışıyor. Kategori seçiciye gidip geri
      dönünce yazılanlar kaybolmuyor.
- [x] Tarih değişirse kayıt yeni günün dosyasına taşınıyor ve panel o güne
      dönüyor.

**Kategori seçici**
- [x] Ekleme formundaki satır içi 4 sütunlu grid kaldırıldı; yerine seçili
      kategoriyi gösteren bir buton ve dokununca açılan panel geldi.
- [x] Aynı seçici düzenleme panelinden de çağrılıyor (geri dönüşlü).

**Geri dönüşüm kutusu**
- [x] Silinen işlem `S.trash`'e `deletedAt` damgasıyla taşınıyor, 24 saat
      (`TRASH_TTL`) sonra kalıcı siliniyor.
- [x] Temizlik açılışta ve dakikada bir çalışıyor.
- [x] Ayarlar > Geri dönüşüm kutusu: kalan süre, tek tek geri yükleme, tek tek
      kalıcı silme, kutuyu boşaltma.
- [x] Kutudaki kayıtlar hiçbir hesaba, grafiğe veya toplama girmiyor.
- [x] Silme anında "Geri al" toast'ı da duruyor.

**Karşılama akışı ve giriş animasyonu**
- [x] Açılış animasyonu: "KE" lacivert, "SE" altın sarısı; harfler sırayla
      geliyor, altındaki çizgi iki rengi birleştirerek açılıyor. En az 1.75 sn.
- [x] İlk açılışta 5 adımlı karşılama: isim → ne kaydedeceği → kullanım amacı
      (çoklu seçim) → bütçe → özet.
- [x] Kullanım modu: `sadece gider` / `gelir ve gider` / `sadece gelir`.
      Tek türlü kullanımda ekleme ekranında tür seçici hiç görünmüyor,
      öneriler ve kategori seçici o türe kilitleniyor.
- [x] Özet kutuları moda göre değişiyor. Sadece gelir modunda halka gideri
      değil geliri gösteriyor.
- [x] Gelir de kaydediliyorsa bütçe elle girilmiyor: `budgetMode:'income'`,
      bütçe = dönem geliri × `spendRatio` (%60/70/80/90). Gelir değiştikçe bütçe
      kendiliğinden güncelleniyor, kalan kısım tasarruf hedefi olarak gösteriliyor.
- [x] Ayarlar > Kullanım: mod ve profil (isim, amaçlar) sonradan değiştirilebiliyor.

**İstatistik — yeniden yazıldı**
- [x] 6 KPI: toplam gider, toplam gelir, net, tasarruf oranı, günlük ortalama,
      işlem sayısı.
- [x] Geçen dönemle karşılaştırma artık takvimsel: yarım ay, geçen ayın aynı
      uzunluktaki dilimiyle kıyaslanıyor (`prevRange`), tamamlanmış ayla değil.
- [x] Ay sonu projeksiyonu: mevcut tempoyla tahmini ay sonu gideri, bütçe aşımı
      /payı, kalan günler için günlük sınır. Yalnızca aylık bütçe döneminde.
- [x] Günlük harcama çubukları + 7 günlük hareketli ortalama çizgisi.
- [x] İşlem büyüklüğü: ortalama, medyan, standart sapma, en küçük–en büyük,
      ortalama-medyan farkının ne anlama geldiğini açıklayan not.
- [x] Kategori tablosu: tutar, pay, işlem sayısı, ortalama işlem ve önceki
      döneme göre fark. Yatay kaydırmalı.
- [x] Haftanın günü profili (gün başına ortalama) ve günün saati profili
      (gece/sabah/öğleden sonra/akşam), tepe değer vurgulu.
- [x] Aylık gelir/gider çubukları üzerine net çizgisi.
- [x] Kümülatif seyir, kart/nakit, en büyük 5 işlem, bu hafta/geçen hafta korundu.
- [x] CSV dışa aktarma (`sep=;` + BOM, Excel'de Türkçe sorunsuz).

### Yapılmadı / bilinen sorunlar
- **İkon dosyaları yok.** `icon-192.png`, `icon-512.png`,
  `icon-512-maskable.png` üretilmedi. Manifest bunlara işaret ediyor.
- **Tekrar eden işlem** alanı kaydediliyor ama hâlâ otomatik kayıt üretmiyor.
- **Chart.js CDN'den geliyor.** İlk açılış çevrimdışıysa istatistik boş durum
  gösterir.
- **Kategori sıralaması sabit.** Sürükle-bırak yok.
- **Kaydırarak silme yalnızca dokunmatikte.** Masaüstünde fare ile kaydırma yok;
  silmek için satıra tıklayıp düzenleme panelindeki "Geri dönüşüm kutusuna taşı"
  kullanılıyor.
- Kur/çoklu para birimi yok, tek para birimi ₺.
- Gelir kategorileri bütçe halkasına dahil değil (tasarım kararı).
- Zoom kapatıldığı için görme güçlüğü olan kullanıcılar sayfayı büyütemez;
  bu bilinçli bir tercih (istek üzerine).

### Sonraki adımlar
1. Uygulama ikonlarını üret, manifest'i doğrula.
2. Tekrar eden işlemler için açılışta "vadesi gelenleri oluştur" kontrolü.
3. Kategori bazlı alt limitler ve limit aşımı uyarısı.
4. Chart.js'i yerelleştir (CDN bağımlılığını kaldır).
