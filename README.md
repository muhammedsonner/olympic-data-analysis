# Olympic Games Data Analysis (EDA) 🏅

Bu depo, Olimpiyat Oyunları'nın tarihsel verileri üzerine gerçekleştirilen bir Keşifsel Veri Analizi (EDA) projesini içermektedir. Proje **devam etmekte** olup kapsamı genişletilmektedir.

---

## 📁 Proje Yapısı

```
olympic-data-analysis/
│
├── bios.csv                  # Ham sporcu biyografi verisi
├── bios_clean.csv            # Temizlenmiş sporcu biyografi verisi
├── results.csv               # Ham yarışma sonuçları verisi
├── results_clean.csv         # Temizlenmiş yarışma sonuçları verisi
│
├── bios_cleaning.ipynb       # Biyografi verisi temizleme pipeline'ı
├── results_cleaning.ipynb    # Sonuçlar verisi temizleme pipeline'ı
└── eda.ipynb                 # Keşifsel veri analizi
```

---

## 📓 Notebook Açıklamaları

### 1. `bios_cleaning.ipynb` — Sporcu Biyografi Temizleme
Ham `bios.csv` dosyasını okur, dönüşümleri uygular ve `bios_clean.csv` olarak kaydeder:

- **İsim temizleme:** `•` karakteri ve fazladan boşlukların giderilmesi (`Used name`, `Full name`)
- **Ölçüm ayrıştırma:** `Measurements` sütunundan `height_cm`, `weight_min_kg`, `weight_max_kg` sütunlarının regex ile elde edilmesi; tekil değerler, ondalıklılar ve aralıklar (`80–90 kg`) desteklenmektedir
- **Doğum/ölüm bilgisi:** `Born` ve `Died` sütunlarından tarih, yıl, doğum yeri ve ülkenin çıkarılması
- **Cinsiyet kodlaması:** `Male → M`, `Female → F`
- **Sütun normalleştirme:** Tüm sütun adları küçük harfe ve alt çizgi formatına dönüştürülür

**Kullanılan kütüphaneler:** `pandas`, `numpy`, `re`

---

### 2. `results_cleaning.ipynb` — Yarışma Sonuçları Temizleme
Ham `results.csv` dosyasını okur, dönüşümleri uygular ve `results_clean.csv` olarak kaydeder:

- **Gereksiz sütunların kaldırılması:** `Unnamed: 7`, `Nationality`
- **Yıl & sezon çıkarımı:** `Games` sütunundan `Year` ve `Season` (`Summer`/`Winter`) elde edilir
- **Sıra temizleme:** `pos` sütunundan sayısal sıra (`pos_rank`) ve metin durum (`pos_status`) ayrıştırılır
- **Veri düzeltmesi:** Eksik/hatalı NOC kodunun manuel olarak düzeltilmesi (Charlotta Säfvenberg → SWE)
- **Sütun normalleştirme:** Tüm sütun adları standart formata getirilir

**Kullanılan kütüphaneler:** `pandas`, `re`

---

### 3. `eda.ipynb` — Keşifsel Veri Analizi
`bios_clean.csv` ve `results_clean.csv` dosyaları üzerinde kapsamlı analiz ve görselleştirmeler gerçekleştirilir.

| Analiz | İçerik |
|---|---|
| 🌍 NOC Katılım Analizi | En çok sporcu yetiştiren 20 NOC |
| 📏 Boy Dağılımı | Histogram, boxplot ve IQR tabanlı aykırı değer analizi |
| ⚖️ Kilo Dağılımı | `weight_min/max/mid_kg` üzerinden histogram ve boxplot |
| 🔗 Boy-Kilo Korelasyonu | Scatter plot; Pearson korelasyonu ~0.77 |
| 📅 Yaş Trendleri | Yaz ve Kış Olimpiyatları'nda 1896'dan günümüze ortalama yaş değişimi |
| 🥇 Madalya Analizi | NOC bazında altın/gümüş/bronz madalya dağılımı (Top 20) |
| 📈 Madalya Tarihsel Trendi | Olimpiyat yılına ve sezone göre toplam madalya sayısı değişimi |
| 🏆 Olimpiyat Başarı Verimliliği | Katılım başına madalya oranı; hem genel hem Yaz Olimpiyatları özelinde |

**Kullanılan kütüphaneler:** `pandas`, `numpy`, `math`, `matplotlib`

---

## 🚀 Gelecek Çalışmalar (To-Do)

- [ ] Ülkelerin farklı spor dallarındaki madalya dağılımının analizi
- [ ] Yaz ve Kış Olimpiyatları'ndaki madalya dağılımının karşılaştırması
- [ ] Spor dalı bazında performans trendleri

> *Not: Analizlerde ülkeler, veri setindeki **NOC kodları** temel alınarak değerlendirilmektedir. Farklı dönemlerde aynı coğrafi bölgeyi ya da ülkeyi temsil etmiş farklı NOC kodları birleştirilmemiştir.*

---

## 🗄️ Veri Kaynağı

Kullanılan veri setleri (`bios.csv`, `results.csv`), [Olympedia.org](https://www.olympedia.org/) sitesinden sporcu profilleri ve yarışma sonuçlarının scraping yöntemiyle toplanmasıyla oluşturulmuştur. Scraping algoritması ve veri seti yapısı orijinal olarak **Keith Galli** tarafından oluşturulmuş olup burada **MIT Lisansı** kapsamında kullanılmaktadır.

---

## 🛠️ Kullanılan Teknolojiler

| Kütüphane | Amaç |
|---|---|
| `pandas` | Veri okuma, temizleme, dönüştürme ve gruplama |
| `numpy` | Sayısal hesaplamalar, `NaN` yönetimi |
| `matplotlib` | Görselleştirme (histogram, boxplot, scatter, bar, line) |
| `re` | Regex tabanlı metin ayrıştırma (standart kütüphane) |
| `math` | Temel matematiksel yardımcı fonksiyonlar (standart kütüphane) |
| Jupyter Notebook | İnteraktif geliştirme ortamı |

---

## 💻 Nasıl Çalıştırılır

1. Bu repoyu yerel makinenize klonlayın:
   ```bash
   git clone https://github.com/muhammedsonner/olympic-data-analysis.git
   cd olympic-data-analysis
   ```

2. Gerekli kütüphaneleri yükleyin:
   ```bash
   pip install pandas numpy matplotlib jupyter
   ```

3. Notebook'ları sırasıyla çalıştırın:
   - `bios_cleaning.ipynb` → `bios_clean.csv` üretir
   - `results_cleaning.ipynb` → `results_clean.csv` üretir
   - `eda.ipynb` → Temizlenmiş dosyaları kullanarak analiz yapar

4. Jupyter Notebook'u başlatın:
   ```bash
   jupyter notebook
   ```

> **Not:** Ham veri dosyaları (`bios.csv` ~27 MB, `results.csv` ~34 MB) büyük boyutludur. Temizlenmiş dosyalar (`bios_clean.csv`, `results_clean.csv`) repoda mevcutsa temizleme adımlarını atlayabilirsiniz.