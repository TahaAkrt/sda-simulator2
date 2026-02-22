[README_SDA_SIMULATOR2 (2).md](https://github.com/user-attachments/files/25462951/README_SDA_SIMULATOR2.2.md)
# 🛰️ Space Domain Awareness Simulator v2

**Advanced Interactive Simulation of Parallax-Based RSO Tracking**

## 🔗 Hızlı Erişim

**🌐 Canlı Demo:** https://tahaakrt.github.io/sda-simulator2

**📄 IEEE Makalesi:** https://doi.org/10.1109/TAES.2025.3528922

**💾 GitHub Repo:** https://github.com/TahaAkrt/sda-simulator2

---

## 📡 Proje Hakkında

Bu simülatör, **uydu formasyonlarında star tracker kullanarak uzay alan farkındalığını (SDA) artırmaya** yönelik yenilikçi bir yaklaşımı interaktif olarak görselleştirir. 

IEEE Transactions on Aerospace and Electronic Systems'de yayınlanan bilimsel makaleye dayanır ve **gerçek zamanlı parallaks hesaplamaları, Monte Carlo analizi ve Gibbs yörünge belirleme** içerir.

### 🎯 Ana Konsept

İki uydu, **star tracker** kameralarını kullanarak aynı **Resident Space Object (RSO)** uzay çöpünü farklı açılardan gözlemler. **Parallaks etkisi** sayesinde:

- RSO'nun gerçek zamanlı 3D konumu hesaplanır
- Yörünge parametreleri belirlenir  
- **~0.69 metre hassasiyet** elde edilir (7000 km yörüngede!)

```
        RSO (Uzay Çöpü)
           ★
          /│\
         / │ \
        /  │  \
    ST-1   │   ST-2
  (Uydu1) DÜNYA (Uydu2)
  
  Parallaks = farklı açılardan bakış
```

---

## 📄 Kaynak Makale

**"Enhancing Space Domain Awareness Using Star Trackers in Satellite Formations"**

| | |
|---|---|
| **Yazarlar** | Kathiravan Thangavel, Tomás Burroni, Pablo Servidia, Dario Spiller, Roberto Sabatini |
| **Dergi** | IEEE Transactions on Aerospace and Electronic Systems |
| **Cilt/Sayı** | Vol. 61, No. 3, s. 8028-8033 |
| **Tarih** | Haziran 2025 |
| **DOI** | [10.1109/TAES.2025.3528922](https://doi.org/10.1109/TAES.2025.3528922) |

---

## ✨ Simülatör Özellikleri

### 🎮 5 İnteraktif Sekme

#### 1️⃣ **Simülasyon Sekmesi**
- Gerçek zamanlı 3D yörünge görselleştirmesi
- ST-1 (yeşil) ve ST-2 (turuncu) uydu formasyonu
- RSO (mavi) takibi ve tahmin edilen konum (sarı)
- Star tracker FOV görüntüleri (20° × 20°)
- Anlık metrikler: α₁, α₂, konum hatası, paralaks açısı

#### 2️⃣ **Parallaks Hesap Sekmesi**
- Denklem 9-11'in canlı implementasyonu
- Özelleştirilebilir uydu ve RSO konumları
- Monte Carlo analizi (200 iterasyon)
- Hata dağılımı histogramı

#### 3️⃣ **Yörünge Analizi Sekmesi**
- **Algoritma 1** adım adım görselleştirme
- 160 gözlem → 6. dereceden polinom fit
- Gibbs yöntemi ile yörünge belirleme
- Tablo II karşılaştırması (gerçek vs. tahmin)

#### 4️⃣ **Hassasiyet Analizi Sekmesi**
- Taban uzaklığı vs. konum hatası
- Centroid hatası vs. RSO pozisyon hatası
- Hata kaynakları pasta grafiği (%87 centroid, %8 GNSS)

#### 5️⃣ **Makale Özeti Sekmesi**
- Tüm denklemler ve parametreler
- Simülasyon koşulları
- Uygulama alanları
- Yazarlar ve atıf bilgileri

---

## 🧮 Matematiksel Temeller

### Temel Denklemler

**Birim Vektör (Eq. 1)**
```
u*ˢ = [x*, y*, f]ᵀ / √(x*² + y*² + f²)
```

**RSO Konumu (Eq. 3)**
```
p₁ + α₁·u₁ = p₂ + α₂·u₂
```

**Kapalı Form Çözümü (Eq. 9)**
```
[α₁]         1        [ 1    u₁ᵀu₂ ] [-dᵀu₁]
[α₂] = ────────────── [            ] [     ]
       1-(u₁ᵀu₂)²    [ u₁ᵀu₂   1  ] [ dᵀu₂]

d = p₁ - p₂  (taban vektörü)
```

**Tahmin Edilen Konum (Eq. 11)**
```
p̂ₜ = (p₁ + α₁u₁ + p₂ + α₂u₂) / 2
```

**RSO Görsel Büyüklük (Eq. 2)**
```
mₒ = -26.8 - 2.5·log₁₀(μAF(Φ)) + 5·log₁₀(‖ρ‖)

F(Φ) = 2/(3π²)·((π-Φ)cos(Φ) + sin(Φ))
```

---

## 🔬 Simülasyon Parametreleri

### Yörünge Konfigürasyonu
| Parametre | Değer | Açıklama |
|-----------|-------|----------|
| **Uydu İrtifası (Hₛ)** | 600 km | ST-1 ve ST-2 yörünge yüksekliği |
| **RSO İrtifası (Hₒ)** | 700 km | Hedef nesne yüksekliği |
| **Taban b₁** | 9 km | ST-1 Y ekseni offset |
| **Taban b₂** | -11 km | ST-2 Y ekseni offset |
| **Taban b₃** | 0.5 km | Z ekseni offset |
| **Yörünge Tipi** | SSO Frozen | Sun-synchronous orbit |

### Star Tracker Özellikleri
| Parametre | Değer |
|-----------|-------|
| **FOV (Görüş Alanı)** | 20° × 20° |
| **Çözünürlük** | 1024 × 1024 piksel |
| **Piksel Açısı** | ~0.02°/piksel |
| **Centroid Hatası** | 0.015 px (1 arc sec) |

### GNSS Doğruluğu
| Sistem | Doğruluk |
|--------|----------|
| **PPP (Absolute)** | ±100 mm |
| **RTK (Relative)** | ±10 mm |

### Gözlem Parametreleri
| Parametre | Değer |
|-----------|-------|
| **Eş Zamanlı Gözlem** | 160 örnek |
| **Gözlem Süresi** | 160 saniye |
| **Polinom Derecesi** | 6 |
| **Gibbs Noktaları** | 3 (başlangıç, orta, son) |

---

## 📊 Performans Sonuçları (Tablo II)

| Orbital Parametre | Gerçek Değer | Tahmin Hatası |
|-------------------|--------------|---------------|
| **a (Yarı-büyük eksen)** | 7085.1 km | **0.69 m** ✅ |
| **e (Eksantrisite)** | 0.00106 | 3.8×10⁻⁷ |
| **i (Eğim)** | 97.8161° | 2.6×10⁻⁶ ° |
| **Ω (RAAN)** | 0.573° | 2.1×10⁻⁵ ° |
| **ω (Perigee arg.)** | 90° | 0.1348° |
| **λ(t₀) (Enlem arg.)** | 77.4810° | **4.6×10⁻⁶ °** ✅ |

> 🎯 **7000+ km yörüngede sadece 0.69 metre hata!**

---

## 🛠️ Teknoloji & Mimari

### Frontend Stack
```
┌─────────────────────────────────────┐
│  Pure HTML5 + CSS3 + Vanilla JS     │
│  • Hiçbir framework kullanılmadı    │
│  • Tek dosya, bağımsız çalışır      │
│  • CDN bağımlılığı yok              │
└─────────────────────────────────────┘
```

### Kullanılan Teknolojiler
- **Canvas API** → 2D grafik rendering
- **Galois Field Aritmetiği** → Reed-Solomon hata düzeltme
- **Polinom Fit** → Gürültü azaltma (6. derece)
- **Gibbs Orbital Mekanik** → 3 noktalı yörünge belirleme
- **QRCode.js (embedded)** → Mobil erişim

### Hata Kaynakları Analizi
```
Toplam Hata Dağılımı:
┌──────────────────────────────┐
│ Centroid Hatası      87%  ████████▓│
│ GNSS Absolute (PPP)   8%  █        │
│ GNSS Relative (RTK)   3%  ▓        │
│ Diğer                 2%  ▒        │
└──────────────────────────────┘
```

---

## 🚀 Kullanım

### Seçenek 1: Canlı Demo
```
https://tahaakrt.github.io/sda-simulator2
```

### Seçenek 2: Yerel Çalıştırma
```bash
# Depoyu klonlayın
git clone https://github.com/TahaAkrt/sda-simulator2.git

# Tarayıcıda açın
open index.html
# veya
firefox index.html
# veya dosyayı çift tıklayın
```

### Seçenek 3: QR Kod ile Mobil
1. Bilgisayarda siteyi açın
2. Alt kısımda **"QR KOD İLE AÇ"** butonuna tıklayın
3. Telefonunuzun kamerasıyla QR kodu tarayın
4. Mobil cihazda simülatör açılır 📱

---

## 🎓 Eğitim Amaçlı Kullanım

Bu simülatör şu konuları öğretmek için idealdir:

### Uzay Mühendisliği
- ✅ Uzay alan farkındalığı (Space Domain Awareness)
- ✅ Resident Space Object (RSO) takibi
- ✅ Uydu formasyonu uçuşu
- ✅ Yörünge mekaniği ve Gibbs yöntemi

### Optik Sistemler
- ✅ Star tracker kamera teknolojisi
- ✅ Centroid belirleme algoritmaları
- ✅ Görüntü işleme ve pattern recognition

### Navigasyon
- ✅ GNSS PPP (Precise Point Positioning)
- ✅ GNSS RTK (Real-Time Kinematic)
- ✅ Yörünge belirleme ve filtreleme

### Matematik & Algoritmalar
- ✅ Parallaks geometrisi
- ✅ Galois Field aritmetiği
- ✅ Reed-Solomon hata düzeltme
- ✅ Monte Carlo simülasyonu
- ✅ Polinom fit ve regresyon

---

## 📱 Mobil Uyumluluk

Simülatör responsive tasarıma sahiptir:

| Cihaz | Uyumluluk |
|-------|-----------|
| 💻 Desktop | ✅ Tam özellikli |
| 📱 Mobil (Dikey) | ✅ Optimize edilmiş |
| 📱 Mobil (Yatay) | ✅ Geliştirilmiş görünüm |
| 📊 Tablet | ✅ Tam uyumlu |

---

## 🌟 Öne Çıkan Özellikler

### 🚀 Teknik Avantajlar
- **Sıfır Bağımlılık** → Hiçbir npm, pip, kurulum yok
- **Tek Dosya** → index.html her şeyi içerir
- **Çevrimdışı Çalışır** → İnternet gerektirmez
- **Cross-Platform** → Windows, macOS, Linux, mobil

### 🎯 Bilimsel Doğruluk
- **IEEE Peer-Reviewed** → Hakemli dergi makalesi
- **Gerçek Denklemler** → Eq. 1-11 direkt implementasyon
- **Doğrulanmış Sonuçlar** → Tablo II ile karşılaştırılabilir

### 🎨 Kullanıcı Deneyimi
- **Koyu Uzay Teması** → Göz yormayan tasarım
- **Animasyonlu Yıldız Alanı** → Gerçekçi atmosfer
- **İnteraktif Kontroller** → Canlı parametre değişimi
- **QR Kod Entegrasyonu** → Anında mobil erişim

---

## 👨‍💻 Geliştirici

**Taha Akkurt**

IEEE TAES 2025 makalesinin interaktif web implementasyonu. Uzay mühendisliği ve eğitim teknolojileri odaklı proje.

---

## 📜 Atıf (Citation)

Bu simülatörü akademik çalışmalarınızda kullanırsanız lütfen orijinal makaleyi referans gösterin:

### BibTeX
```bibtex
@article{thangavel2025enhancing,
  title={Enhancing Space Domain Awareness Using Star Trackers in Satellite Formations},
  author={Thangavel, Kathiravan and Burroni, Tom{\'a}s and Servidia, Pablo and Spiller, Dario and Sabatini, Roberto},
  journal={IEEE Transactions on Aerospace and Electronic Systems},
  volume={61},
  number={3},
  pages={8028--8033},
  year={2025},
  publisher={IEEE},
  doi={10.1109/TAES.2025.3528922}
}
```

### APA
```
Thangavel, K., Burroni, T., Servidia, P., Spiller, D., & Sabatini, R. (2025). 
Enhancing Space Domain Awareness Using Star Trackers in Satellite Formations. 
IEEE Transactions on Aerospace and Electronic Systems, 61(3), 8028-8033. 
https://doi.org/10.1109/TAES.2025.3528922
```

---

## 🔗 Bağlantılar

**🌐 Canlı Demo:**  
https://tahaakrt.github.io/sda-simulator2

**📄 IEEE Makalesi:**  
https://doi.org/10.1109/TAES.2025.3528922

**💾 GitHub Deposu:**  
https://github.com/TahaAkrt/sda-simulator2

**📱 QR Kod Erişimi:**  
Siteyi açın → Alt kısımda "QR KOD İLE AÇ" butonuna tıklayın

---

## 🤝 Katkıda Bulunma

Bu bir eğitim projesidir. Öneriler ve geri bildirimler için:

1. **Issues** → Hata bildirimi veya özellik isteği
2. **Pull Request** → Kod katkısı
3. **Discussions** → Genel sorular

---

## 📞 İletişim

- **GitHub:** [@TahaAkrt](https://github.com/TahaAkrt)
- **Proje Soruları:** GitHub Issues
- **Makale Hakkında:** Orijinal yazarlarla iletişime geçin

---

## 🎯 Kullanım Senaryoları

### Eğitim
- Üniversite uzay mühendisliği dersleri
- Yüksek lisans/doktora araştırmaları
- Online eğitim platformları

### Araştırma
- Yeni algoritmaların test edilmesi
- Hata analizi çalışmaları
- Simülasyon doğrulama

### Sunum & Demo
- Konferans sunumları
- Proje savunmaları
- Halkla ilişkiler etkinlikleri

---

## 📈 Gelecek Geliştirmeler

Potansiyel iyileştirmeler:

- [ ] WebGL ile 3D dünya modeli
- [ ] Çoklu RSO takibi
- [ ] Gerçek TLE verisi entegrasyonu
- [ ] PDF rapor dışa aktarma
- [ ] İngilizce dil desteği
- [ ] Karanlık/Aydınlık tema geçişi

---

## ⚖️ Lisans

Bu proje **eğitim amaçlı** bir açık kaynak simülasyondur. 

Orijinal bilimsel araştırma IEEE'ye aittir ve standart akademik atıf kurallarına tabidir.

---

<div align="center">

### 🌌 Uzay Alan Farkındalığı — Geleceğin Uzay Trafiği Yönetimi

**Star Tracker + GNSS + Parallax = 0.69m Hassasiyet**

**🚀 Canlı Demo:** https://tahaakrt.github.io/sda-simulator2

**📖 IEEE Makalesi:** https://doi.org/10.1109/TAES.2025.3528922

---

**v2.0** | Taha Akkurt | 2025

</div>
