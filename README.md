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
- **+ İstasyon Ekle** ile yeni bir istasyon oluşturun; istasyon adı, operatör/paralel sunucu sayısını (1–16 arası) ve görev listesini düzenleyin.
- Görev eklemek için `Görev Adı`, `Operatör` (≥1) ve `Süre(sn)` (>0) alanlarını doldurun; satırdaki artı simgesiyle yeni görev eklersiniz.
- Operatör sayısı istasyon kapasitesini paralel sunucu olarak artırır; tek bir ürünün servis süresi görev sürelerinin toplamı olarak sabit kalır.
- Üst çubuktaki **Başlat**, **Durdur** ve **Sıfırla** butonları simülasyonu yönetir. Klavye kısayolları: `B`, `D`, `R`.
- Hız kaydırgacını 0.25×–16× aralığında ayarlayarak yalnızca animasyon hızını değiştirin; mantıksal zaman ve metrikler sabit kalır.
- **Analiz/Öneri** butonuna tıklayıp açılan modalde takt time (sn/ürün) girin; darboğaz istasyonu, teorik throughput, +1/+2 operatör what-if senaryoları ve kuyruk etkisi raporlanır.
- Üst çubuktaki **Sonuçları Gör** butonu simülasyon bitmeden de dashboardu açar; cycle time, toplam tamamlanan, throughput ve ortalama WIP kartlarını, istasyon bazlı performans tablosunu ve “Analiz / Öneriler” metnini canlı izleyebilirsiniz.
- Dashboard altındaki CSV ve PDF (yazdır → PDF olarak kaydet) butonlarıyla raporu dışa aktarın; PDF düğmesi tarayıcının yazdırma penceresini açar ve “PDF olarak kaydet” seçeneğinin kullanılabilirliği tarayıcıya bağlıdır.
- Üst çubuktaki “Tamamlanan: N” rozeti hat genelinde tamamlanan ürün sayısını canlı olarak gösterir.
- Hedef adet alanına sayı girerseniz o kadar ürün tamamlandığında simülasyon otomatik durur ve dashboard açılır; tam ekran modundaysanız sonuçları manuel olarak görüntüleyebilirsiniz.
- Görsel paneldeki **🔳 Tam Ekran** butonu yalnızca animasyon alanını büyütür; tekrar tıklayarak veya `Esc` ile normal görünüme dönebilirsiniz.

# “İstasyon Ekle” Butonu İpucu
Simülasyona yeni istasyon eklenemiyorsa aşağıdaki kontrol listesini izleyin:

- `index.html` dosyasını tarayıcıda açmanız yeterlidir; gerekirse `python -m http.server` ile basit sunucu kullanabilirsiniz.
- HTML içinde `id="addStationBtn"` olan **tek** bir buton bulunduğunu ve `type="button"` kullanıldığını doğrulayın; bu sayede form submit tetiklenmez.
- Sayfa yüklendikten sonra (DOMContentLoaded) `onAddStationClick` dinleyicisinin yalnızca bir kez bağlandığını ve konsolda `Station added:` logunun göründüğünü kontrol edin.
- CSS tarafında butonun üzerinde `pointer-events:none` veren veya üstünü örten bir eleman olmadığından emin olun; gerektiğinde geliştirici araçlarıyla katmanları inceleyin.
- Tarayıcı konsolunda hata görürseniz ekran görüntüsü alın; `addStation`, `renderStations`, `renderGraph`, `saveState` ve `loadPersistedState` fonksiyonlarının tanımlı olduğundan ve script etiketinin yalnızca bir kez yüklendiğinden emin olun.

# Hızlı Hata Kontrolü (Invalid or unexpected token)
`Uncaught SyntaxError: Invalid or unexpected token` mesajı alırsanız şu adımları uygulayın:

```bash
# Kod dosyalarının UTF-8 olduğundan emin olun (VS Code → File → Save with Encoding → UTF-8)
# Kopyalanan metinlerdeki akıllı tırnakları düz tırnaklarla değiştirin
# Şüpheli karakterleri silip yeniden yazın (özellikle yorum satırları ve template literal'ler)
```

- Görünmez karakterleri temizlemek için sorunu yaşayan satırı silip yeniden yazın; gerekirse `View → Toggle Render Whitespace` özelliğini açın.
- `<script>` etiketinin doğru kapandığını, betiğin yalnızca bir kez çağrıldığını ve dosya yolunda yazım hatası olmadığını doğrulayın.
- Son değişikliklerinizde yarım kalan template literal, kapatılmamış parantez veya çok satırlı yorum olmadığını tekrar kontrol edin.
- Değişikliklerden sonra tarayıcıyı yenileyip konsolun temiz kaldığını doğrulayın.

# Görselleştirme
- İstasyonlar yatay kartlar halinde sıralanır; aralarındaki oklar ürünlerin akış yönünü belirtir.
- Baloncuk animasyonları (job'lar) oklar boyunca ilerler; istasyonda boş sunucu yoksa kartın üzerinde FIFO kuyruğu görünür.
- Darboğaz oluştuğunda istasyon çerçevesi kırmızı tonuna geçer ve canlı `qLen` ile `util%` etiketleri uyarı niteliği taşır.
- Her istasyon kartında anlık kuyruk, aktif paralel servis sayısı, kalan süre ve yüzde ilerleme rozetleri görüntülenir.
- Görsel paneldeki “− / % / +” zoom denetimi, sahneyi 0.5×–2.5× aralığında büyütüp küçültür; animasyon akışı bozulmaz.
- Dashboard açıldığında cycle time, toplam tamamlanan, throughput ve WIP kartları ile istasyon tablosu; ayrıca kuyruk/utilizasyon çubuk grafiği ve tamamlanma eğrisi çizgi grafiği otomatik olarak güncellenir.
- Ekranın sağ alt köşesindeki yarı saydam **E.DEMIR** imzası her modda görünür ve tasarımın imzası olarak konumunu korur.

# Sistem Gereksinimleri
- Güncel bir masaüstü tarayıcı (Chrome, Edge veya Firefox) yeterlidir.
- Uygulama internet bağlantısı olmadan çalışır.
- En az 1366×768 çözünürlük önerilir; daha geniş ekranlar görselleştirmeyi kolaylaştırır.

# Lisans
Bu prototip **kişisel ve eğitim amaçlı kullanım içindir**. Başka bir lisans belirtilmemiştir.
