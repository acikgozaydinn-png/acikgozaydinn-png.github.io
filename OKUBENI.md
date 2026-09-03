# Altın & Gümüş Hesaplama — Android PWA/TWA Paketi

Bu paket, Aydın Yatırım Noktası hesaplama aracının mobil uyumlu, kurulabilir bir PWA olarak yayınlanması ve daha sonra Trusted Web Activity (TWA) ile Google Play’e gönderilmesi için hazırlanmıştır.

## Paket içeriği

| Dosya | Görevi |
|---|---|
| `index.html` | Mobil uyumlu hesaplama aracı; altın ve gümüş sekmeleri, sonuçlar ve reklam alanı içerir. |
| `manifest.json` | Uygulama adı, ikonlar, renkler ve kurulum davranışı. |
| `service-worker.js` | İlk ziyaret sonrasında temel çevrimdışı kullanım. |
| `icons/` | 192 ve 512 piksel uygulama ikonları. |
| `gizlilik-politikasi.html` | Web sitesi ve Play Console için gizlilik bildirimi taslağı. |
| `assetlinks.json` | TWA ile web alan adını doğrulamak için şablon. |

## 1. Web yayını

Dosyaları HTTPS destekleyen bir alan adına yükleyin. GitHub Pages kullanılacaksa depo köküne `index.html`, `manifest.json`, `service-worker.js`, `gizlilik-politikasi.html` ve `icons` klasörü konulmalıdır. PWA’nın çalıştığını şu adreslerden kontrol edin:

```text
https://SIZIN-DOMAININIZ/index.html
https://SIZIN-DOMAININIZ/manifest.json
https://SIZIN-DOMAININIZ/service-worker.js
```

Blogger sayfası ayrı kalabilir; ancak TWA’nın açacağı adresin PWA dosyalarını sunan HTTPS alan adı olması gerekir. `assetlinks.json`, mutlaka şu konumda doğrudan erişilebilir olmalıdır:

```text
https://SIZIN-DOMAININIZ/.well-known/assetlinks.json
```

## 2. Reklam geliri

`index.html` içindeki `ad-slot` alanı yerleşim yeridir. Reklam ağı hesabınız ve onayınız varsa, kendi reklam kodunuzu bu alana ekleyin. Reklamları yanıltıcı biçimde hesaplama düğmelerine benzetmeyin, kullanıcı tıklamasını teşvik etmeyin ve gizlilik bildiriminizi reklam sağlayıcısının gerçek çerez/veri uygulamalarına göre güncelleyin. Web reklam geliri ile Android uygulama içi reklam geliri aynı şey değildir; TWA web sayfasını açtığı için öncelikle web reklam hesabı ve site doğrulaması gerekir.

## 3. TWA oluşturma

Node.js ve Java/Android build ortamı olan bir bilgisayarda Bubblewrap kurulabilir:

```bash
npm install -g @bubblewrap/cli
bubblewrap init --manifest https://SIZIN-DOMAININIZ/manifest.json
bubblewrap build
```

İlk kurulumda paket adı olarak aşağıdaki değeri kullanın:

```text
com.aydinyatirimnoktasi.altinhesap
```

Üretim imzalama anahtarını güvenli biçimde yedekleyin. İmzalama anahtarı kaybolursa gelecekteki güncellemelerde sorun yaşayabilirsiniz. Google Play’e yüklemeden önce cihazda veya kapalı test kanalında gerçek URL, geri tuşu, çevrimdışı ekran, reklam alanı ve farklı ekran boyutlarını test edin.

## 4. Digital Asset Links

TWA tam ekran güven ilişkisi için release sertifikasının SHA-256 parmak izini `assetlinks.json` içindeki yer tutucuyla değiştirin. Dosyayı web kökünde `.well-known/assetlinks.json` yoluna koyun. Paket adı ile sertifika parmak izi birebir aynı olmalıdır. Doğrulama başarısız olursa uygulama normal tarayıcı çubuğuyla açılabilir.

## 5. Google Play gönderimi

Google Play Console’da uygulama oluşturup Android App Bundle (`.aab`) yükleyin. Uygulama açıklamasında bunun fiyat/kur hesaplama ve bilgilendirme aracı olduğunu açıkça yazın; “garantili kazanç”, “kesin getiri” veya kişiye özel yatırım tavsiyesi ifadeleri kullanmayın. Gizlilik politikası URL’si, içerik derecelendirmesi, veri güvenliği formu, uygulama ikonu, ekran görüntüleri ve destek e-postası gerekecektir.

3 Eylül 2026 itibarıyla yeni uygulamalar ve güncellemeler için Android 16 / API 36 hedefi gereklidir. Bubblewrap’ın güncel sürümünü ve güncel Android build araçlarını kullanın; Play Console yükleme ekranındaki hedef API uyarısını esas alın.

## Önemli sınırlar

Bu paket hesaplama aracını ve yayın dosyalarını hazırlar; Google Play onayı garanti edilemez. Play politikaları, reklam sağlayıcısının onayı, alan adı sahipliği, gizlilik bildiriminin gerçek uygulamayla uyumu ve mağaza incelemesi ayrıca tamamlanmalıdır. Google Play geliştirici hesabı için kayıt ücreti ve olası vergi/şirket yükümlülükleri bu pakete dahil değildir.

## Kaynaklar

[1] [Android Developers — Trusted Web Activities](https://developer.android.com/develop/ui/views/layout/webapps/trusted-web-activities)

[2] [Android Developers — Google Play target API level requirement](https://developer.android.com/google/play/requirements/target-sdk)

[3] [Google Play Developer Policy Center](https://play.google/developer-content-policy/)

