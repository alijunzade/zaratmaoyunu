# 🎯 Silgi Fırlatma Savaşları

## ✅ Tamamlanan Değişiklikler

### 1. 🎲 → 🎯 Silgi Mekaniği
- Zar yerine dikdörtgen silgi (5×10×40 cuboid)
- Ağırlıklı sonuç sistemi:
  - ➕ (35%) - Tam kazan
  - ➖ (35%) - Tam kaybet  
  - ✖️ (12%) - 2 kat kazan
  - ➗ (12%) - Yarım kazan
  - 💎 (3%) - JACKPOT! 2 kat kazan
  - 💀 (3%) - FELAKET! 2 kat kaybet

### 2. 🔊 Ses Sistemi (AudioManager)
- Lazy loading (ilk tıklamada yüklenir)
- LocalStorage ile mute tercihi kaydedilir
- Sağ alt köşede mute toggle butonu
- Throttled ses efektleri (performans için)

### 3. 🎬 Video Entegrasyonu
- 3 saniyelik silgi animasyonu
- Ekranın ortasında gösterilir
- Animasyon sonunda otomatik kapanır

### 4. 🎮 Oyun Kuralları (Korundu)
- 2 oyuncu, sıra bazlı
- Çeyrek daire başlangıç alanları
- Serbest şekil çizimi
- Alan limiti kontrolü
- Overlay temizleme

## 📁 Dosya Yapısı

```
zar atma oyunu 1/
├── index.html (ANA OYUN DOSYASI)
├── assets/
│   ├── audio/
│   │   ├── ES_Lighting, Spell, Cast, Positive, Big, Glimmer 03 - Epidemic Sound - 0000-2185.wav
│   │   ├── ES_Cartoon Comic Expressions, Jump - Epidemic Sound - 0000-0754.wav
│   │   ├── ES_Bright, Chimes 03 - Epidemic Sound - 0000-2259.wav
│   │   ├── ES_Toy Tambourine, Single Hit - Epidemic Sound - 0000-0196.wav
│   │   ├── ES_Buttons, Switches, Mixed, Antique, Special, Clicks - Epidemic Sound - 0000-1250.wav
│   │   └── ES_Hands, Dry Hands Rubbing Bare Arms - Epidemic Sound - 0000-1852.wav
│   └── video/
│       └── eraser_roll.webm
└── README.md
```

## 🎯 YAPILACAKLAR (Dosyaları Ekleyin)

### Ses Dosyaları
Aşağıdaki WAV dosyalarını `assets/audio/` klasörüne kopyalayın:

1. **ES_Lighting, Spell, Cast, Positive, Big, Glimmer 03 - Epidemic Sound - 0000-2185.wav**
   - Kullanım: Jackpot sesi

2. **ES_Cartoon Comic Expressions, Jump - Epidemic Sound - 0000-0754.wav**
   - Kullanım: Alan seçimi başlangıcı

3. **ES_Bright, Chimes 03 - Epidemic Sound - 0000-2259.wav**
   - Kullanım: Kazanç sesleri

4. **ES_Toy Tambourine, Single Hit - Epidemic Sound - 0000-0196.wav**
   - Kullanım: Kayıp sesleri

5. **ES_Buttons, Switches, Mixed, Antique, Special, Clicks - Epidemic Sound - 0000-1250.wav**
   - Kullanım: Buton tıklama

6. **ES_Hands, Dry Hands Rubbing Bare Arms - Epidemic Sound - 0000-1852.wav**
   - Kullanım: Alan çizimi (throttled)

### Video Dosyası
`assets/video/` klasörüne şu dosyayı ekleyin:

- **eraser_roll.webm**
  - 3 saniye silgi yuvarlanma animasyonu
  - Hafif toz efekti ile

## ⚙️ Özellikler

### Audio Manager
- **Lazy Loading**: İlk kullanıcı etkileşimine kadar bekler (tarayıcı politikası)
- **Mute Toggle**: Sağ alt köşede 🔊/🔇 butonu
- **LocalStorage**: Mute tercihi kaydedilir
- **Throttling**: Aynı sesin çok sık çalmasını engeller (150ms)
- **Volume Control**: Her ses için ayrı seviye ayarı

### Video Manager
- **URL Encoding**: Dosya isimlerindeki boşluk ve virgüller otomatik encode edilir
- **Auto Hide**: Animasyon bitince otomatik kapanır
- **No Blocking**: Oyun akışını engellemez

### Ses Mapping
- **buttonClick** (#5): Roll butonu tıklama
- **selectionStart** (#2): Alan çizimi başlangıcı (çok düşük ses)
- **selectionDrag** (#6): Alan çizimi süresi (throttled, 150ms, çok düşük)
- **win** (#3): Kazanç sonuçları
- **jackpot** (#1): Jackpot özel sesi
- **loss** (#4): Kayıp sonuçları (düşük ses)

## 🚀 Nasıl Çalıştırılır?

1. Ses dosyalarını `assets/audio/` klasörüne kopyalayın
2. Video dosyasını `assets/video/` klasörüne kopyalayın
3. `index.html` dosyasını tarayıcıda açın
4. Sağ alt köşedeki 🔊 butonu ile sesi açıp kapatabilirsiniz

## 🎨 Kod Yapısı

### AudioManager
```javascript
AudioManager.init()        // İlk yükleme
AudioManager.play(key)     // Ses çal
AudioManager.toggleMute()  // Mute toggle
```

### VideoManager  
```javascript
VideoManager.show()  // Video göster
VideoManager.hide()  // Video gizle
```

## 🔧 Ayarlamalar

### Ses Seviyeleri (index.html içinde)
```javascript
volumes: {
    buttonClick: 0.25,
    selectionStart: 0.12,
    selectionDrag: 0.10,
    win: 0.30,
    jackpot: 0.30,
    loss: 0.20
}
```

### Silgi Ağırlıkları
```javascript
const ERASER_OUTCOMES = [
    { weight: 35, gain: 1 },   // +
    { weight: 35, gain: -1 },  // -
    { weight: 12, gain: 2 },   // ×
    { weight: 12, gain: 0.5 }, // ÷
    { weight: 3, gain: 2 },    // 💎
    { weight: 3, gain: -2 }    // 💀
];
```

## 📝 Notlar

- Dosya isimleri TAM olarak korunmalı (boşluklar ve virgüller dahil)
- URL encoding otomatik yapılır
- Mute tercihi tarayıcıda saklanır
- Video 3 saniye boyunca gösterilir
- Tüm sesler throttled (overlay kaos yok)

## ✨ Yeni Özellikler

1. **Disaster Outcome**: Shield yerine -2× kayıp (💀)
2. **Mute Toggle**: Sağ alt köşede buton
3. **Video Overlay**: Silgi animasyonu
4. **Professional SFX**: Epidemic Sound dosyaları
5. **Smart Throttling**: Performanslı ses sistemi

---

**Geliştirici Notu**: Tüm değişiklikler mevcut oyun yapısını koruyarak yapıldı. Hiçbir temel mekanik bozulmadı.
