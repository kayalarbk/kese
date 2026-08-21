# Elle test kontrol listesi

## Açılış ve karşılama
1. **Animasyon** — Uygulamayı aç. "KE" lacivert, "SE" altın sarısı olarak sırayla
   geliyor mu, altındaki çizgi açılıyor mu? En az ~1.7 sn görünüyor mu?
2. **Karşılama** — İlk açılışta 5 adım sırayla geliyor mu? Geri tuşuyla önceki
   adıma dönünce yazdıkların duruyor mu? "Keseyi aç" sonrası bir daha çıkmıyor mu?
3. **Mod seçimi** — "Sadece gider" seçip bitir. Ekle ekranında Gider/Gelir seçici
   gizli mi? Kaydet butonu "Gideri kaydet" mi diyor? Özet kutuları
   Gider / İşlem / Günlük ort. mu?
4. **Gelirden bütçe** — "Gelir ve gider" seçip %80 ile bitir. Bir gelir kaydet.
   Ayarlar > Bütçe, "hesaplanan bütçe = gelirin %80'i" gösteriyor mu? Yeni gelir
   ekleyince bütçe kendiliğinden büyüyor mu?

## iOS davranışı (gerçek iPhone gerekiyor)
5. **Zoom** — Çift dokun, iki parmakla aç. Sayfa yakınlaşmamalı. Tutar alanına
   dokun; klavye açılırken sayfa kaymamalı/büyümemeli.
6. **Dynamic Island / çentik** — Başlıktaki "Özet" ve dönem etiketi adanın
   altında mı, üstüne binmiyor mu?
7. **Ana ekran çizgisi** — Alt menüdeki dört simge çizginin üstünde mi kalıyor?
   Kaydet butonu ve toast çizgiye değiyor mu?
8. **Yatay mod** — Telefonu yan çevir. İçerik kavisli köşelerin/kameranın altına
   girmiyor mu?
9. **Ana ekrana ekle** — Standalone açıldığında da 5–8 aynı mı?

## Günlük dosyalar ve işlemler
10. **Dosyalar** — Ekle ekranında işlemler gün gün kart olarak mı duruyor?
    Kartta gün numarası, işlem sayısı, kategori renk noktaları ve günün gideri
    doğru mu? Bugünün kartı koyu mu?
11. **Dosya açma** — Karta dokun. Panelde günün gider/gelir/işlem sayısı ve
    işlem listesi çıkıyor mu?
12. **Düzenleme** — Bir işleme dokun. Alanlar dolu geliyor mu? Tutarı değiştir,
    kategori seçiciye gir, kategori seç, geri dön — yazdığın tutar duruyor mu?
    Kaydet dedikten sonra liste ve özet güncelleniyor mu?
13. **Tarih değiştirme** — Düzenlemede tarihi başka bir güne al. Kayıt o günün
    dosyasına taşınıyor ve panel yeni güne dönüyor mu?

## Silme ve geri dönüşüm kutusu
14. **Kısmi kaydırma** — Satırı biraz sola kaydır. Kırmızı zemin ve "Sil"
    etiketi çıkıp satır açık kalıyor mu? Kırmızı alana dokununca siliniyor mu?
15. **Tam kaydırma** — Satırı yarıdan fazla kaydır. Doğrudan siliniyor mu?
16. **Dikey kaydırma** — Satırın üstünde parmağını yukarı/aşağı sürükle. Satır
    kaymadan sayfa normal kayıyor mu?
17. **Kutu** — Ayarlar > Geri dönüşüm kutusu. Silinen kayıt "N saat sonra
    silinir" ile duruyor mu? "Geri" ile listeye dönüyor mu? Kalıcı sil onay
    soruyor mu? Kutuyu boşalt çalışıyor mu?
18. **Hesaplara girmiyor** — Kutuda kayıt varken Özet ve İstatistik
    toplamlarına dahil edilmediğini doğrula.
19. **24 saat** — DevTools'tan `kese-v1` içindeki bir `trash` kaydının
    `deletedAt` değerini 25 saat öncesine al, sayfayı yenile. Kayıt kayboldu mu?

## İstatistik
20. **Dönemler** — Beş sekmeyi sırayla gez. Grafikler yeniden çiziliyor mu,
    üst üste binen eski canvas kalıyor mu? Özel aralıkta iki tarihi değiştir.
21. **Kıyas** — "Geçen döneme göre" bölümündeki "önceki" değerler, geçen ayın
    aynı gün sayısına denk geliyor mu (tam ay değil)?
22. **Projeksiyon** — Aylık bütçe döneminde "Ay sonu projeksiyonu" çıkıyor mu?
    Bütçe dönemini haftalığa alınca kıyas satırı uyarıya dönüyor mu?
23. **Tablo** — Kategori tablosu yatay kaydırılabiliyor mu? Fark sütunundaki
    renkler doğru yönde mi (artış kırmızı, azalış yeşil)?
24. **CSV** — Ayarlar > CSV indir. Dosya Excel'de Türkçe karakterlerle ve
    sütunları ayrılmış şekilde açılıyor mu?

## Veri
25. **Migration** — Eski `kese-v1` verisiyle aç. Emoji kategoriler SVG ikona
    dönüşmüş mü, eski işlemler duruyor mu, hepsi "Kart" olarak mı işaretlenmiş?
26. **Sıfırlama** — Ayarlar > Tüm verileri sil. Karşılama akışı baştan
    başlıyor mu?
27. **Çevrimdışı PWA** — Sayfayı bir kez aç, uçak moduna al, yeniden aç.
    Uygulama açılıyor mu, grafikler önbellekten geliyor mu?
