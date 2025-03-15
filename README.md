**[Çevrimiçi Deneyim](https://design.palxp.cn/)** | **[Çevrimiçi Dokümanlar](https://xp.palxp.cn/)** | [Sık Sorulan Sorular](https://xp.palxp.cn/#/articles/1689323321667) | [Performans Testi](https://juejin.cn/post/7348288810722869300)

---

## Hızlı Tasarım

Güzel, kullanımı kolay ve güçlü özelliklere sahip yaratıcı bir görsel düzenleyici. Gaoding Design, Chuangkit, Canva gibi ticari ürünlerle rekabet eder.

Çeşitli senaryolar için uygundur: poster oluşturma, e-ticaret paylaşım görselleri, makale görselleri, video/sosyal medya kapakları vb. Yazılım indirmeye gerek kalmadan bulut üzerinde düzenleme yapabilir ve hızlıca metin-görsel düzenlemelerini tamamlayabilirsiniz.

[![](https://xp.palxp.cn/images/2023-7-16-1689500112694.gif)](https://design.palxp.cn/)

### Özellikler

- Pürüzsüz sayfa kullanım deneyimi, zengin etkileşim detayları, eksiksiz temel işlevler
- Sunucu tarafında görsel oluşturma, çoklu platformlarda görüntü tutarlılığını sağlar, çeşitli CSS özelliklerini destekler
- Basit AI görsel arka plan kaldırma aracı, görselleri yükleyip tek tıkla arka planı kaldırabilirsiniz
- Teknoloji yığını: Vue3, Vite5, Vuex, ElementPlus, geliştirme deneyimi sorunsuz
- Görsel oluşturma: Puppeteer, Express

### Desteklenen Özellikler

- PSD dosyalarını şablona dönüştürme, çevrimiçi görsel dışa aktarma ve indirme
- Öğeleri sürükleme, gruplama, boyutlandırma, katman ayarlama, hizalama vb. işlemler
- Görsel malzeme ekleme, değiştirme, kırpma, görsel konteyneri vb. özellikler
- SVG malzemelerinin renk ve şeffaflık düzenleme, metin ve süslü yazı kombinasyonları
- Özel tuval boyutu, fare tekerleği ile yakınlaştırma, otomatik tuval uyumu
- Yapışkan hizalama, yardımcı kılavuz çizgileri, cetvel işlevi
- Klavye kısayolları, sağ tıklama menüsü, kopyalama-silme gibi yaygın işlemler
- Stil QR kodu düzenleme, tek renk, degrade, özel logo desteği
- Katman işlemleri, sürükleyerek katman seviyesini değiştirme
- Renk paleti, yerel renk damlalığı (Chrome)

## Hızlı Başlangıç

```
git clone https://github.com/yalcindemir/poster-design.git
cd poster-design
npm run prepared
npm run dev
cd screreenshot
npm run dev
```

![](https://xp.palxp.cn/images/2023-7-16-1689498291322.png)

Web sayfasını görmek için http://127.0.0.1:5173/ adresini ziyaret edin. [Daha fazla doküman](https://xp.palxp.cn/#/articles/1689319644311) için tıklayın.

### Görsel Oluşturma Servisi

Kod, kök dizinde [/screenshot](https://github.com/palxiao/poster-design/tree/main/screenshot) içinde bulunmaktadır. API dokümanını görüntülemek için tıklayın: [API Dokümanı](https://xp.palxp.cn/apidoc/screenshot.html).

### Sunucu Tarafı

Arka uç kısmını kendiniz geliştirmeniz gerekiyor. Şu anda bu projenin demo sürümündeki arka uç API referansı: [API Dokümanı](https://xp.palxp.cn/apidoc/index.html).

## Diğer

Yüksek kaliteli bir içerik topluluğu oluşturmaya, sürdürülebilir bir öğrenme platformu oluşturmaya çalışıyoruz. Aynı zamanda geliştiricilerin projelerinde karşılaştıkları zorlukları çözmeye ve gereksiz yollardan kaçınmalarına yardımcı oluyoruz.

<img style="width: 380px;" src="https://github.com/palxiao/poster-design/assets/21021314/643dcc8b-ef73-4c76-a78c-a7c377b5f268" />

Ayrıca WeChat hesabımızı takip etmekten çekinmeyin: 品味前端 (Pinwei Frontend), "加群" (Gruba Katıl) yazarak iletişime geçebilirsiniz.

<img style="width: 380px;" src="https://xp.palxp.cn/images/2024-3-1-1709306365949.png" />

-----

Bu proje başlangıçta Vue2 ile geliştirildi, şimdi Vue3 ile yeniden yapılandırılıyor. [Bazı yineleme planları](https://xp.palxp.cn/#/articles/1689319986889?id=%e8%bf%ad%e4%bb%a3%e8%ae%a1%e5%88%92).

Şu anda açık kaynak sürümü hala geliştirilmeye devam ediyor ve hala birçok eksiklik var. Karşılaştığınız sorunları Issues bölümünde belirtebilir veya iyileştirmeye yardımcı olmak için Pull Request gönderebilirsiniz.

### Teşekkürler

Proje ayrıca bazı mükemmel açık kaynak projelerden yararlanmış veya referans almıştır, bunlar arasında:

- [moveable](https://github.com/daybrush/moveable): Tuval üzerinde seçme, sürükleme, boyutlandırma vb. yetenekler sağlar
- [html2canvas](https://github.com/niklasvh/html2canvas): Ön yüzde görsel oluşturma için hızlı bir çözüm
- [qr-code-styling](https://qr-code-styling.com/): Stilize edilmiş QR kodları
- [rembg](https://github.com/danielgatis/rembg): Görsel arka plan kaldırma, u2net ön eğitimli modeli kullanır

Açık kaynak kolay değildir, son olarak bu projeye bir **Yıldız** vermeyi unutmayın ~

[![Star History Chart](https://api.star-history.com/svg?repos=palxiao/poster-design&type=Date)](https://star-history.com/#palxiao/poster-design&Date)

### `Yıldız`

Bu projeyi destekleyen tüm arkadaşlara teşekkürler :heart:

[![Stargazers](https://bytecrank.com/nastyox/reporoster/php/stargazersSVG.php?user=palxiao&repo=poster-design)](https://github.com/palxiao/poster-design/stargazers)

### `Çatal`

Bu küçük arkadaşlar Hızlı Tasarım'ı kullanıyor :heart:

[![Forkers](https://bytecrank.com/nastyox/reporoster/php/forkersSVG.php?user=palxiao&repo=poster-design)](https://github.com/palxiao/poster-design/network/members)

### Sponsor Dostlarımız

| Dooring Düşük Kod | DrawOn Masaüstü |
| --- | --- |
| <a href="https://dooring.vip/"> <img style="height: 90px" src="https://github.com/palxiao/poster-design/assets/21021314/2240801f-8484-4fd2-8505-8205daa6d53c" /></a> | <a href="https://www.drawon.cn?useSource=hb1"> <img style="height: 120px" src="https://github.com/palxiao/poster-design/assets/21021314/258bb6ec-4e1e-4c86-b45c-22946213f209" /></a> |

### `Katkıda Bulunanlar`

<a href="https://github.com/palxiao/poster-design/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=palxiao/poster-design" />
</a>

### `LİSANS`

Bu proje tamamen ücretsizdir ve [MIT açık kaynak lisansı](https://github.com/palxiao/poster-design/blob/main/LICENSE) korunduğu sürece kullanılabilir.