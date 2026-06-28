# 🟢 CYBER DASH

Neon siberpunk temalı, tek parmakla oynanan hyper-casual arcade kaçış oyunu. Kayarak engellerden kaç, ne kadar yakın geçersen o kadar çok kombo kazan!

**🎮 Oyna:** [asistan80.github.io/cyber-dash](https://asistan80.github.io/cyber-dash/)

![Durum](https://img.shields.io/badge/durum-oynanabilir-39ff8f) ![Platform](https://img.shields.io/badge/platform-web%20%7C%20PWA-2fd8ff) ![Lisans](https://img.shields.io/badge/lisans-kişisel%20proje-ff8a2b)

---

## 🕹️ Oynanış

- **Tek parmakla kontrol:** Ekranı sola/sağa kaydır, parmağını kaldırınca karakter otomatik orta şeride döner.
- **Risk & Ödül:** Kırmızı/turuncu engellere ne kadar **yakın** (teğet) geçersen, o kadar yüksek **combo çarpanı** kazanırsın.
- **Mavi enerji küpleri** topla, skor ve "Data" (oyun içi para birimi) kazan.
- Çarpışınca oyun **anında** yeniden başlıyor — bekleme yok, "bir kez daha" dürtüsü tam burada.

## ✨ Özellikler

| Özellik | Açıklama |
|---|---|
| 🌟 Near-Miss Combo Sistemi | Engele yakın geçtikçe x2, x3... combo çarpanı ve ekran flaşı |
| 📈 Artan Zorluk Seviyeleri | Skor arttıkça hız artıyor, yeni mekanikler (kayan engeller, glitch efekti, rastgele spawn) açılıyor |
| 🏆 İsimli Skor Tablosu | En iyi 10 skor, isimle kaydediliyor (cihaz bazlı, `localStorage`) |
| 🎨 Kozmetik Mağaza | 10 farklı neon kostüm + 8 farklı kuyruk efekti, oyun içi "Data" ile satın alınıyor |
| 🔊 Ses Açma/Kapama | Sağ üstteki buton ile senkron sesleri aç/kapat |
| 📱 PWA Desteği | Telefonda "Ana ekrana ekle" ile tam ekran, çevrimdışı çalışan bir uygulama gibi kullanılabilir |

## 🎨 Görsel Tarz

Koyu arka planlar üzerine parlayan neon yeşil ve elektrik mavisi — siberpunk/synthwave estetiği. Tüm efektler (parçacıklar, ekran titremesi, glitch) `<canvas>` üzerinde gerçek zamanlı çiziliyor.

## 🛠️ Teknik Detaylar

- **Tek dosyalık HTML/CSS/JS** — harici kütüphane yok, derleme adımı yok.
- Oyun mantığı ve render `index.html` içinde, `<canvas>` 2D context kullanılarak yazıldı.
- Ses efektleri Web Audio API ile gerçek zamanlı sentezleniyor (ses dosyası yok).
- İlerleme (skor tablosu, açılan kozmetikler, ses tercihi) `localStorage` ile cihazda saklanıyor.

### Dosya yapısı

```
cyber-dash/
├── index.html              # Oyunun tamamı (HTML + CSS + JS)
├── manifest.json            # PWA manifest (ikon, isim, tam ekran ayarı)
├── service-worker.js        # Çevrimdışı çalışma için cache mantığı
├── icons/                    # Uygulama ikonları (192px, 512px, maskable)
├── capacitor.config.json     # Native Android paketleme için hazır config
└── PLAY_STORE_REHBERI.md     # Play Store'a yükleme adımları (Capacitor → APK/AAB)
```

## 📲 Mobilde Kullanma

1. Linki Chrome'da aç: `https://asistan80.github.io/cyber-dash/`
2. Sağ üstteki **⋮** menüsünden **"Ana ekrana ekle"** / **"Uygulamayı yükle"** seç.
3. Artık tam ekran, ikonlu, çevrimdışı çalışan bir uygulama gibi kullanabilirsin.

Play Store'a gerçek bir uygulama olarak yüklemek istersen `PLAY_STORE_REHBERI.md` dosyasındaki adımları takip edebilirsin (Capacitor ile native Android paketine çevirme rehberi).

## 🚀 Yerelde Çalıştırma

Bu proje herhangi bir build aracı gerektirmiyor. Sadece:

```bash
git clone https://github.com/asistan80/cyber-dash.git
cd cyber-dash
```

`index.html`'i bir tarayıcıda aç (veya `python3 -m http.server` ile basit bir sunucu başlat — service worker'ın çalışması için `https://` veya `localhost` üzerinden açman gerekir, `file://` ile çalışmaz).

## 📝 Yol Haritası / Fikirler

- [ ] Ortak (global) skor tablosu için backend entegrasyonu
- [ ] Daha fazla kozmetik / sezonsal temalar
- [ ] Reklam veya satın alma entegrasyonu (Play Store sürümü için)

## 📄 Lisans

Bu proje kişisel/deneme amaçlı geliştirilmiştir.

---

*Claude (Anthropic) ile birlikte geliştirildi 🤖*
