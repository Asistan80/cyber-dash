# CYBER DASH — Play Store'a Yükleme Rehberi

Bu pakette 2 katman var:
1. **PWA (hazır)** — `index.html`, `manifest.json`, `service-worker.js`, `icons/` → telefonda tarayıcıdan açıp "Ana ekrana ekle" diyerek uygulama gibi kullanabilirsin. Şimdi test edebilirsin.
2. **Native Android (Play Store için)** — Aşağıdaki adımlarla bu PWA'yı gerçek bir `.aab`/`.apk` dosyasına çevirip Play Console'a yükleyebilirsin.

Native build için Android Studio + Node.js gerektiği için bu adımları **kendi bilgisayarında** çalıştırman gerekiyor (burada derleme yapılamıyor).

---

## A) PWA'yı hemen test et

1. Bu klasördeki tüm dosyaları bir web sunucusuna koy (GitHub Pages, Netlify, Vercel — hepsi ücretsiz ve 2 dakikada kurulur). Service worker `file://` ile çalışmaz, bir `https://` adresi gerekir.
2. Android telefonda Chrome ile linki aç → sağ üstteki "⋮" menüsünden **"Ana ekrana ekle"** / **"Uygulamayı yükle"**.
3. Artık telefonda bağımsız bir uygulama ikonu olarak açılıyor, tam ekran, çevrimdışı çalışıyor.

## B) Native Android (.aab) — Play Store için

Bilgisayarında Node.js (18+) ve Android Studio kurulu olmalı.

```bash
# 1. Bu klasörde bir npm projesi başlat
npm init -y
npm install @capacitor/core @capacitor/cli @capacitor/android

# 2. Oyun dosyalarını "www" klasörüne taşı (Capacitor bu klasörü paketler)
mkdir www
cp index.html manifest.json service-worker.js www/
cp -r icons www/

# 3. Capacitor'ı başlat (capacitor.config.json zaten hazır, üzerine yazmasını onayla)
npx cap init "Cyber Dash" "com.seninstudyon.cyberdash" --web-dir www

# 4. Android platformunu ekle
npx cap add android

# 5. Web dosyalarını native projeye senkronize et
npx cap sync android

# 6. Android Studio'da aç
npx cap open android
```

Android Studio açıldıktan sonra:
1. `Build > Generate Signed Bundle / APK` seç.
2. **Android App Bundle (.aab)** seç (Play Store bunu zorunlu kılıyor).
3. Yeni bir **keystore** oluştur (uygulamanın kimliği — bu dosyayı ve şifreyi kaybetme, ileride güncelleme yüklerken tekrar gerekecek).
4. Build alındıktan sonra `.aab` dosyasını Play Console'a yükle.

## C) Play Console'da yapman gerekenler

1. [play.google.com/console](https://play.google.com/console) — bir kerelik 25$ geliştirici kaydı.
2. Yeni uygulama oluştur → `com.seninstudyon.cyberdash` paket adıyla eşleşmeli.
3. Mağaza listesi için gerekenler:
   - Uygulama ikonu (512x512) — `icons/icon-512.png` zaten hazır, sadece arka planını opak yapman gerekebilir (Play Store şeffaf ikon kabul etmiyor).
   - En az 2 ekran görüntüsü (telefonundan oyunu oynarken alabilirsin).
   - Kısa açıklama, gizlilik politikası linki (basit bir tek sayfalık gizlilik metni de yeterli, veri toplamıyorsan "bu uygulama kişisel veri toplamaz" yazan bir sayfa linki).
4. `.aab` dosyasını yükle, içerik derecelendirmesi anketini doldur, yayınla.
5. İlk inceleme genelde 1-3 gün sürüyor.

## Notlar / öneriler

- **Paket adını (`com.seninstudyon.cyberdash`) kendi geliştirici hesabına göre değiştir** — `capacitor.config.json` ve init komutundaki ID'yi güncelle.
- Skor tablosu şu an `localStorage` kullanıyor — bu sadece cihaz bazlı çalışır, oyuncular arasında ortak bir liderlik tablosu istersen bir backend (Firebase gibi) eklememiz gerekir, haber ver.
- Reklam/IAP eklemek istersen (AdMob, Google Play Billing) Capacitor eklentileriyle sonradan entegre edilebilir.
