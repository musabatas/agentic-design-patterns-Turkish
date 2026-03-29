# Ek E - CLI Uzerinde Yapay Zeka Agent'lari

## Giris

Uzun suredir kesin, imperatif komutlarin kalesi olan gelistirici komut satiri, derin bir donusum gecirmektedir. Basit bir kabuktan, yeni bir arac sinifi tarafindan desteklenen akilli, is birlikci bir calisma alanina evrilmektedir: Yapay Zeka Agent Komut Satiri Arayuzleri (CLI). Bu agent'lar sadece komut yurutmenin otesine gecmektedir; dogal dili anlar, tum kod tabaniniz hakkinda baglam korur ve gelistirme yasam dongusunun onemli parcalarini otomatiklestiren karmasik, cok adimli gorevleri yerine getirebilir.

Bu rehber, bu gelisen alandaki dort lider aracin derinlemesine bir incelemesini sunarak, benzersiz guclerini, ideal kullanim alanlarini ve farkli felseefelerini kesfederek is akisiniza en uygun araci belirlemenize yardimci olmaktadir. Belirli bir arac icin saglanan ornek kullanim alanlarinin cogunun diger agent'lar tarafindan da gerceklestirilebilecegini belirtmek onemlidir. Bu araclar arasindaki temel fark, genellikle belirli bir gorev icin elde edebildikleri sonuclarin kalitesi, verimliligi ve inceliigidir. Bu yetenekleri olcmek icin tasarlanmis belirli benchmark'lar vardir ve bunlar asagidaki bolumlerde ele alinacaktir.

## Claude CLI (Claude Code)

Anthropic'in Claude CLI'si, bir projenin mimarisini derin ve butunsel olarak anlayan ust duzey bir kodlama agent'i olarak tasarlanmistir. Temel gucu, karmasik, cok adimli gorevler icin depo hakkinda bir zihinsel model olusturmasina olanak taniyan "agentic" dogasidir. Etkilesim son derece sohbet tabanlidir ve yurutmeden once planlarini aciklayan bir cift programlama oturumuna benzer. Bu, onemli yeniden yapilandirma veya genis mimari etkilere sahip ozelliklerin uygulanmasini iceren buyuk olcekli projeler uzerinde calisan profesyonel gelistiriciler icin idealdir.

**Ornek Kullanim Alanlari:**

1. **Buyuk Olcekli Yeniden Yapilandirma:** Sunun gibi talimat verebilirsiniz: "Mevcut kullanici kimlik dogrulamamiz oturum cerezlerine dayaniyor. Tum kod tabanini durumsuz JWT'leri kullanacak sekilde yeniden yapilandir, giris/cikis endpoint'lerini, middleware'i ve frontend token islemesini guncelle." Claude daha sonra tum ilgili dosyalari okuyup koordineli degisiklikleri gerceklestirir.
2. **API Entegrasyonu:** Yeni bir hava durumu hizmeti icin bir OpenAPI spesifikasyonu saglandiktan sonra, su sekilde diyebilirsiniz: "Bu yeni hava durumu API'sini entegre et. API cagrilarini yonetecek bir hizmet modulu olustur, hava durumunu goruntule'mek icin yeni bir bilesen ekle ve ana panoyu bunu iceerecek sekilde guncelle."
3. **Dokumantasyon Uretimi**: Kotukullanilmis belgelenmis koda sahip karmasik bir modulu gostererek, su sekilde isteyebilirsiniz: "`./src/utils/data_processing.js` dosyasini analiz et. Her fonksiyon icin amacini, parametrelerini ve donus degerini aciklayan kapsamli TSDoc yorumlari olustur."

Claude CLI, dosya okuma, kod yapisi analizi ve duzenleme olusturma dahil olmak uzere temel gelistirme gorevleri icin yerlesik araclara sahip uzmanlasmis bir kodlama asistani olarak isler. Git ile derin entegrasyonu, dogrudan dal ve commit yonetimini kolaylastirir. Agent'in genisletilebilirligi, kullanicilarin ozel araclar tanimlamasini ve entegre etmesini saglayan Multi-tool Control Protocol (MCP) araciliyla saglanir. Bu, ozel API'lerle etkilesim, veritabani sorgulari ve projeye ozel betiklerin yurutulmesine olanak tanir. Bu mimari, gelistiriciyi agent'in islevsel kapsaminin hakemi konumuna yerlestirerek, Claude'u kullanici tarafindan tanimlanmis araclarla guclendirilmis bir akil yurutme motoru olarak nitelendirir.

## Gemini CLI

Google'in Gemini CLI'si, guc ve erisilebilirlik icin tasarlanmis cok yonlu, acik kaynakli bir yapay zeka agent'idir. Gelismis Gemini 2.5 Pro modeli, devasa context window'u ve cok modlu yetenekleri (gorsel ve metin isleme) ile one cikar. Acik kaynakli yapisi, coemert ucretsiz katmani ve "Reason and Act" dongusu, onu seffaf, kontrol edilebilir ve hobi gelisriricilerinden kurumsal gelistiricilere, ozellikle Google Cloud ekosistemindekiilere kadar genis bir kitle icin mukemmel bir genel amacli arac yapar.

**Ornek Kullanim Alanlari:**

1. **Cok Modlu Gelistirme:** Bir tasarim dosyasindan bir web bileseninin ekran goruntusu saglayip (gemini describe component.png) sunun gibi talimat verebilirsiniz: "Bu gorsele tam olarak benzeyen bir React bileseni olusturmak icin HTML ve CSS kodu yaz. Duyarli oldugundan emin ol."
2. **Bulut Kaynak Yonetimi:** Yerlesik Google Cloud entegrasyonunu kullanarak su komutu verebilirsiniz: "Uretim projesinde 1.28'den eski surumleri calisiiran tum GKE kümelerini bul ve bunlari tek tek yukseltmek icin bir gcloud komutu olustur."
3. **Kurumsal Arac Entegrasyonu (MCP araciliigiyla):** Bir gelistirici Gemini'ye sirketin dahili IK API'sine baglanan get-employee-details adinda ozel bir arac saglar. Prompt su sekildedir: "Yeni ise alinan kisi icin bir karsilama belgesi haziirla. Once get-employee-details --id=E90210 aracini kullanarak adini ve ekibini al, ardindan welcome_template.md'yi bu bilgilerle doldur."
4. **Buyuk Olcekli Yeniden Yapilandirma**: Bir gelistiricinin, kullanim disi kalmis bir gunlukleme kutuphanesini yeni, yapilandirilmis bir gunlukleme framework'u ile degistirmek icin buyuk bir Java kod tabanini yeniden yapilandirmasi gerekmektedir. Gemini'yi su prompt ile kullanabilir: 'src/main/java' dizinindeki tum *.java dosyalarini oku. Her dosyada, tum 'org.apache.log4j' import'larini ve 'Logger' sinifini 'org.slf4j.Logger' ve 'LoggerFactory' ile degistir. Logger orneklemesini ve tum .info(), .debug() ve .error() cagrilarini anahtar-deger ciftleriyle yeni yapilandirilmis formati kullanacak sekilde yeniden yaz.

Gemini CLI, cevresiyle etkilesim kurmasina olanak taniyan bir dizi yerlesik araca sahiptir. Bunlar arasinda dosya sistemi islemleri (okuma ve yazma gibi), komut calistirma icin bir kabuk araci ve web getirme ve arama yoluyla internete erisim araclari bulunur. Daha genis baglam icin, birden fazla dosyayi ayni anda okumak icin uzmanlasmis araclar ve sonraki oturumlar icin bilgi kaydetmek icin bir bellek araci kullanir. Bu islevsellik guvenli bir temel uzerine insa edilmistir: korumalı alan (sandbox), riski onlemek icin modelin eylemlerini izole ederken, MCP sunuculari Gemini'nin yerel ortaminiza veya diger API'lere guvenli bir sekilde baglanmasini saglayan bir kopru gorevi gorur.

## Aider

Aider, dosyalariniz uzerinde dogrudan calisan ve degisiklikleri Git'e commit eden gercek bir cift programci olarak hareket eden acik kaynakli bir yapay zeka kodlama asistanidir. Tanimlayici ozelligi dogrudaliigidir; duzzenlemeleri uygular, dogrulamak icin testleri calistirir ve her basarili degisikligi otomatik olarak commit eder. Model-agnostik olmasi, kullanicilara maliyet ve yetenekler uzerinde tam kontrol saglar. Git merkezli is akisi, verimlilik, kontrol ve tum kod degisikliklerinin seffaf, denetlenebilir bir izini degerlendiren gelistiriciler icin mukemmeldir.

**Ornek Kullanim Alanlari:**

1. **Test Odakli Gelistirme (TDD):** Bir gelistirici su sekilde diyebilir: "Bir sayinin faktoriyelini hesaplayan bir fonksiyon icin basarisiz bir test olustur." Aider testi yazip basarisiz olduktan sonra, bir sonraki prompt sunudur: "Simdi testin gecmesini saglayacak kodu yaz." Aider fonksiyonu uygular ve dogrulamak icin testi tekrar calistirir.
2. **Hassas Hata Duzeltme:** Bir hata raporu verildiginde, Aider'a su talimat verilebilir: "billing.py'deki `calculate_total` fonksiyonu artik yillarda basarisiz oluyor. Dosyayi baglama ekle, hatayi duzelt ve duzeltmeni mevcut test paketine karsi dogrula."
3. **Bagimlilik Guncellemeleri:** Sunun gibi talimat verebilirsiniz: "Projemiz 'requests' kutuphanesinin eski bir versiyonunu kullaniyor. Lutfen tum Python dosyalarini gozden gecir, import ifadelerini ve kullanim disi kalmis fonksiyon cagrilarini en son versiyonla uyumlu olacak sekilde guncelle ve ardindan requirements.txt'yi guncelle."

## GitHub Copilot CLI

GitHub Copilot CLI, populer yapay zeka cift programcisini terminale genisleterek birincil avantaji olan GitHub ekosistemiyle yerel, derin entegrasyonu saglar. Bir projenin *GitHub icindeki* baglamini anlar. Agent yetenekleri, bir GitHub sorununa atanmasina, bir duzeltme uzerinde calismasina ve insan incelemesi icin bir pull request gondermesinee olanak tanir.

**Ornek Kullanim Alanlari:**

1. **Otomatik Sorun Cozumleme:** Bir yonetici bir hata biletini (ornegin, "Issue #123: Sayfalamadaki off-by-one hatasini duzelt") Copilot agent'ina atar. Agent daha sonra yeni bir dal olusturur, kodu yazar ve sorunu referans alan bir pull request gonderir -- tumu manuel gelistirici mudahalesi olmadan.
2. **Depo Farkindali Soru-Cevap:** Ekibe yeni katilan bir gelistirici su sekilde sorabilir: "Bu depoda veritabani baglanti mantigi nerede tanimli ve hangi ortam degiskenlerini gerektiriyor?" Copilot CLI, tum depo farkindaliigini kullanarak dosya yollariyla kesin bir cevap saglar.
3. **Kabuk Komutu Yardimcisi:** Karmasik bir kabuk komutu hakkinda emin olmadiginda, bir kullanici su sekilde sorabilir: gh? 50MB'dan buyuk tum dosyalari bul, sikistir ve bir arsiv klasorune yerlestir. Copilot, gorevi gerceklestirmek icin gereken tam kabuk komutunu olusturur.

## Terminal-Bench: Komut Satiri Arayuzlerinde Yapay Zeka Agent'lari Icin Bir Benchmark

Terminal-Bench, yapay zeka agent'larinin komut satiri arayuzunde karmasik gorevleri yurutme yeterliligini degerlendirmek icin tasarlanmis yeni bir degerlendirme cercevesidir. Terminal, metin tabanli ve korumalı alan yapisi nedeniyle yapay zeka agent operasyonu icin optimal bir ortam olarak tanimlanmaktadir. Ilk surum olan Terminal-Bench-Core-v0, bilimsel is akislari ve veri analizi gibi alanlari kapsayan 80 manuel olarak hazirlanmis gorevden olusur. Adil karsilastirmalar saglamak icin, cesitli dil modelleri icin standartlastirilmis bir test ortami olarak hizmet eden minimalist bir agent olan Terminus gelistirilmistir. Cerceve, konteynerizasyon veya dogrudan baglantilar araciliyla cesitli agent'larin entegrasyonuna olanak taniyan genisletilebilirlik icin tasarlanmistir. Gelecek gelistirmeler arasinda buyuk olcekli paralel degerlendirmeler ve yerlesik benchmark'larin dahil edilmesi yer almaktadir. Proje, gorev genislemesi ve is birlikci cerceve gelistirmesi icin acik kaynakli katkilari tesvik etmektedir.

## Sonuc

Bu guclu yapay zeka komut satiri agent'larinin ortaya cikisi, yazilim gelistirmede temel bir degisime isaret etmekte ve terminali dinamik, is birlikci bir ortama donusturmektedir. Gordugumuz gibi, tek bir "en iyi" arac yoktur; bunun yerine, her agent'in uzmanlasmis bir guc sundugu canli bir ekosistem oluskmaktadir. Ideal secim tamamen gelistiricinin ihtiyaclarina baglidir: karmasik mimari gorevler icin Claude, cok yonlu ve cok modlu problem cozme icin Gemini, git merkezli ve dogrudan kod duzenleme icin Aider ve GitHub is akisina sorunsuz entegrasyon icin GitHub Copilot. Bu araclar gelismeye devam ettikce, bunlardan yararlanma becerisi temel bir beceri haline gelecek ve gelistiricilerin yazilimi nasil olusturdugunu, hata ayikladiigini ve yonettiigini temelden degistirecektir.

## Kaynaklar

1. Anthropic. *Claude*. [https://docs.anthropic.com/en/docs/claude-code/cli-reference](https://docs.anthropic.com/en/docs/claude-code/cli-reference)
2. Google Gemini Cli [https://github.com/google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli)
3. Aider. [https://aider.chat/](https://aider.chat/)
4. GitHub *Copilot CLI* [https://docs.github.com/en/copilot/github-copilot-enterprise/copilot-cli](https://docs.github.com/en/copilot/github-copilot-enterprise/copilot-cli)
5. Terminal Bench: [https://www.tbench.ai/](https://www.tbench.ai/)
