# Proje Açıklaması
Hat simülasyonu tek sayfalık bir web uygulaması olarak üretim hattındaki istasyonları, görevleri ve iş akışını görselleştirir. Kullanıcılar istasyon ekleyip düzenleyerek toplam süreleri tanımlar, paralel sunucu sayısını ayarlar ve ayrık olay tabanlı motor ile hat performansını gerçek zamanlı izler.

# Dosya Yapısı
```
Hat_Dengeleme/
├── index.html   # HTML, CSS ve JavaScript tek dosyada birleşir
└── README.md    # Bu kılavuz
```

# Kurulum (Local Çalıştırma)
Projeyi indirmek için aşağıdaki yöntemlerden birini kullanabilirsiniz:

```bash
git clone <repo-adresi>
cd Hat_Dengeleme
```

Alternatif olarak GitHub arayüzünden **Code → Download ZIP** seçeneği ile indirip arşivi açabilirsiniz.

Bu uygulama tek dosyalı olduğu için harici bağımlılık gerektirmez; ek kurulum adımı yoktur.

# Çalıştırma Talimatı
Projeyi açmanın iki basit yolu vardır:

1. Dosya yöneticinizde `index.html` dosyasına çift tıklayın. Varsayılan tarayıcınızda simülasyon açılır.
2. Tercihe göre basit bir HTTP sunucusu ile çalıştırmak için terminalde:

   ```bash
   cd Hat_Dengeleme
   python -m http.server 8000
   ```

   Ardından tarayıcıda `http://localhost:8000/index.html` adresine gidin.

# Kullanım
- **+ İstasyon Ekle** ile yeni bir istasyon oluşturun; istasyon adı, paralel sunucu (1–4) ve görev listesi alanlarını doldurun.
- Görev eklemek için `Görev Adı`, `Operatör` (≥1) ve `Süre(sn)` (>0) değerlerini yazın; satırdaki artı simgesiyle yeni görev eklenir.
- Üst çubuktaki **Başlat**, **Durdur** ve **Sıfırla** butonları simülasyon akışını kontrol eder. Klavye kısayolları: `B`, `D`, `R`.
- Hız kaydırgacını 0.25×–4× aralığında ayarlayarak animasyon hızını değiştirin; metrik hesapları mantıksal zamanda kalır.
- Hedef adet alanına sayı girerseniz o kadar ürün tamamlandığında simülasyon otomatik olarak durur.
- Rapor modali Cycle Time, Throughput, Ortalama WIP, istasyon bazlı kuyruk uzunluğu ve darboğaz analizlerini gösterir; CSV olarak indirebilirsiniz.

# Görselleştirme
- İstasyonlar yatay kartlar halinde sıralanır; aralarındaki oklar ürünlerin akış yönünü belirtir.
- Baloncuk animasyonları (job'lar) oklar boyunca ilerler; istasyonda boş sunucu yoksa kartın üzerinde FIFO kuyruğu görünür.
- Darboğaz oluştuğunda istasyon çerçevesi kırmızı tonuna geçer ve canlı `qLen` ile `util%` etiketleri uyarı niteliği taşır.

# Sistem Gereksinimleri
- Güncel bir masaüstü tarayıcı (Chrome, Edge veya Firefox) yeterlidir.
- Uygulama internet bağlantısı olmadan çalışır.
- En az 1366×768 çözünürlük önerilir; daha geniş ekranlar görselleştirmeyi kolaylaştırır.

# Lisans
Bu prototip **kişisel ve eğitim amaçlı kullanım içindir**. Başka bir lisans belirtilmemiştir.
