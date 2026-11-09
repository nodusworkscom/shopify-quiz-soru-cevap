# Shopify Quiz Soru Cevap Eklentisi

Shopify temasına **tek Liquid dosyasıyla** eklenen soru-cevap quiz popup'ı. Ziyaretçi soldaki QUIZ sekmesinden ya da sayfa açıldıktan sonra kendiliğinden çıkan pencerede soruları yanıtlar. Hepsi doğruysa e-posta adresini bırakır ve indirim kodunu görür. Kodu kopyalayabilir ya da sepete işleyen bağlantıyla devam eder.

Kod, [Shopify quiz soru cevap eklentisi](https://nodusworks.com/blog/shopify-quiz-soru-cevap-eklentisi) yazısının uygulanabilir halidir. Sunucu, uygulama ve ek varlık gerekmez. Sorular, doğru cevap, indirim kodu, renk ve açılış ayarları tema düzenleyiciden yönetilir.

Geliştiren: [Nodus Works](https://nodusworks.com) — Shopify partner ajansı.

## Ne işe yarar?

- Popup quiz, masaüstünde kart, telefonda alttan açılan panel
- Solda sabit QUIZ sekmesi (sağa alınabilir)
- İsteğe bağlı kendiliğinden açılma, varsayılan 5 saniye
- Soru başına 4 seçeneğe kadar; boş bırakılan seçenek gizlenir
- Tüm sorular doğruysa kod. Yanlış cevapta quiz başa döner, doğru şık söylenmez
- İsteğe bağlı e-posta adımı. Adres Shopify müşteri listesine, belirlediğiniz etiketle kaydolur
- Kod ekranına varsayılan 7 gün erişim. Süre bitince quiz yeniden çözülür
- Her açılışta cevapları karıştırma
- Türkçe, İngilizce ve Almanca arayüz. Soru metinleri dil bazında ayrı bloklarla yönetilir
- Tema yazı tipini kullanır, renkler ayardan gelir

## Kurulum

Online Store 2.0 temalarında ve `sections` klasörü olan eski temalarda çalışır. Dosyayı bir kez ekleyin.

### 1. Dosyayı temaya koyun

`sections/nw-quiz-popup.liquid` dosyasını temanızda aynı yola kopyalayın.

Shopify yönetiminde **Online Store → Themes → … → Edit code** yolunu da kullanabilirsiniz. Dosyayı `sections` altına yeni bir section olarak yapıştırın.

### 2. Her sayfada çalışsın

`layout/theme.liquid` dosyasında `</body>` etiketinden hemen önce:

```liquid
{% section 'nw-quiz-popup' %}
```

Bölümü bir JSON şablonuna ayrıca eklemeyin. İki kez basılırsa ikincisi kendini kapatır; yine de tek yerde durması yeter.

### 3. İndirim kodunu Shopify'da açın

**İndirimler → İndirim oluştur → İndirim kodu.**

Tema ayarındaki kod ile buradaki kod aynı olmalıdır. Varsayılan örnek `HOSGELDIN`. Yüzdeyi, alt limiti, tarihini ve kullanım sayısını indirim kaydından siz belirlersiniz. Bu dosya indirim kaydı oluşturmaz.

### 4. Tema düzenleyiciden yönetin

**Online Store → Themes → Customize.** Bölüm adı **Quiz popup**.

Soru bloğu yokken ziyaretçinin diline göre 3 örnek soru çalışır. **Soru ekle** dediğiniz anda örnekler kalkar; kendi sorularınızın tamamını ekleyin. Her soruda doğru seçeneğin numarasını işaretleyin. Seçenek 4 boş kalabilir.

| Ayar | Ne işe yarar |
| --- | --- |
| İndirim kodu | Pencerede görünen ve `/discount/KOD` ile sepete işlenen kod |
| Koddan önce e-posta iste | Açıksa kod, e-posta Shopify'a yazıldıktan sonra görünür |
| Müşteri etiketi | Müşteri kaydına eklenen etiket. Varsayılan `quiz` |
| Kod ekranına erişim | Kazanan ziyaretçi kodu QUIZ sekmesinden kaç gün yeniden açabilir |
| Kendiliğinden aç / gecikme | Sayfa yüklenince popup açılır mı, kaç saniye sonra |
| Kapatınca yeniden açılma | Bir daha açılmasın, bu oturumda bir kez, ya da kod alınana kadar her sayfa |
| Cevapları karıştır | Şıkların sırası her denemede değişir. Doğru şık numarası karışmaz |
| QUIZ sekmesi | Sol ya da sağ kenarda sabit sekme |
| Başlık, e-posta metni, kod metni | Boşsa TR / EN / DE otomatik dolar |

### 5. Çok dil

Arayüz metinleri `request.locale` değerine göre gelir:

- `tr` Türkçe
- `en` İngilizce
- `de` Almanca
- Bunların dışındaki diller İngilizce arayüz görür

Sorular ayrıdır. Bloğun dili **Tüm diller** ise herkes aynı soruyu görür. İngilizce soru için yeni blok açıp dili English seçin. O dilde blok yoksa ve başka dillerde blok varsa, o dil örnek sorulara düşmez; yalnızca eşleşen bloklar gösterilir. Hiç blok yoksa üç örnek soru, ziyaretçinin dilinde gelir.

Başlık alanını doldurursanız otomatik çeviri kapanır ve yazdığınız metin bütün dillerde kullanılır. O metni Shopify Translate ile dil dil çevirin.

### 6. Kontrol

Tema önizlemesinde QUIZ sekmesine basın.

1. Bilerek yanlış cevap verin. Pencere kodu açmamalı, **Baştan başla** demeli.
2. Örnek sorularda doğru sıra: sepetteki kod alanı, Shopify'da oluşturulmuş indirim, aynı pencerede.
3. E-posta adımında mağazada kayıtlı olmayan bir adres yazın.
4. **Müşteriler** listesinde adres `quiz` etiketiyle duruyor mu bakın.
5. Kodu kopyalayın. **İndirimi uygula** sizi `/discount/KOD` adresine götürmeli.
6. Sekmeyi yeniden açın. Süre dolmadan kod ekranı gelmeli, quiz yeniden sorulmamalı.
7. Temayı İngilizce ve Almanca önizleyin. Sekme metnini değiştirmediyseniz QUIZ aynı kalır, pencere o dile geçer.

## E-posta nereye gider?

İstek, temanızın kullandığı Shopify müşteri formunun gittiği adrese gider: `/contact`. Gövdede `form_type=customer`, e-posta, etiket ve `contact[accepts_marketing]=true` vardır. Kendi sunucunuz, webhook'unuz ya da uygulama proxy'niz yoktur.

Adres **Müşteriler** altına pazarlama izniyle düşer. Klaviyo, Omnisend ya da benzeri bir araç Shopify müşteri kaydını dinliyorsa oradan da görebilir. Bu dosya o araçlara doğrudan bağlanmaz.

E-posta adımını kapatırsanız doğru cevapların ardından kod hemen görünür. Blogdaki sade akış budur.

## Sınırlar

İndirim kodu Liquid ayarında durur. Ziyaretçi sayfa kaynağına bakarsa kodu görebilir. Gizli, kişiye özel ya da tek kullanımlık kod istiyorsanız Shopify Functions veya bir uygulama gerekir. Bu bölüm, kaynak kodu görülebilen bir kampanya kodu içindir.

Yanlış cevap da tarayıcıda kontrol edilir. Doğru şık numarası HTML içindedir. Amaç sınav güvenliği değil, kampanyadır.

Bot koruması veya mağaza şifresi `/contact` isteğini keserse kod açılmaz; ziyaretçi yeniden dener. Kod, e-posta kaydı başarılı olmadan gösterilmez. "Bu adres zaten kayıtlı" Shopify'dan dönerse kod yine açılır.

Çerez bandı, sepet çekmecesi veya başka bir popup aynı anda açılırsa üst üste binebilirler. QUIZ sekmesi varsayılan olarak soldadır; sepet balonu genelde sağda kalır.

## Sık sorulan sorular

### Shopify quiz eklentisi için uygulama şart mı?

Hayır. Tema bölümüdür. App Store kurulumu, API anahtarı ve aylık ücret yoktur.

### Kaç soru eklenir?

Tema düzenleyicide 50 soru bloğuna kadar. Shopify bölüm sınırı budur. Örnek kurulum 3 sorudur. Kod, hepsi doğruysa açılır.

### İndirim her sepette çalışır mı?

Kodun Shopify indiriminde tanımlı olması, tarihinin ve sepet koşullarının uyması gerekir. Bölüm yalnızca kodu gösterir ve `/discount/KOD` bağlantısını kurar.

### Tema güncellemesi dosyayı siler mi?

Dosyayı doğrudan temaya yapıştırdıysanız, temayı mağazadan güncellemek veya temayı baştan yüklemek bu dosyayı ve `theme.liquid` satırını silebilir. Güncellemeden önce ikisini de yedekleyin. Daha kalıcı yol, aynı dosyayı bir tema kopyasında tutmaktır.

### Şifre sayfasında çıkar mı?

Hayır. Mağaza şifre sayfası ve hediye kartı sayfasına basılmaz.

## English

Single-file Shopify theme section: a quiz popup, a sticky QUIZ tab, and a discount code after every answer is correct. Optional email step posts to Shopify's own customer endpoint (`/contact`). No app server.

1. Add `sections/nw-quiz-popup.liquid` to the theme.
2. Before `</body>` in `layout/theme.liquid`: `{% section 'nw-quiz-popup' %}`.
3. Create the same code under Discounts.
4. Edit questions under **Customize → Quiz popup**.

The UI is Turkish, English, or German from the store locale. Other locales get English chrome. Question blocks can target `all`, `tr`, `en`, or `de`. The code sits in the theme setting, so it is visible in the page source.

## Lisans

MIT. Ayrıntı için [LICENSE](LICENSE).
