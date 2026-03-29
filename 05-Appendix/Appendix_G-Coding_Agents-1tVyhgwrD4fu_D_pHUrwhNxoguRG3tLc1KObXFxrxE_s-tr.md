# Ek G - Kodlama Agent'lari

## Vibe Coding: Bir Baslangic Noktasi

"Vibe coding", hizli yenilik ve yaratici kesif (Exploration) icin guclu bir teknik haline gelmistir. Bu uygulama, ilk taslaklar olusturmak, karmasik mantigi ana hatlariyla belirlemek veya hizli prototipler insa etmek icin LLM'lerin kullanilmasini icerir ve baslangic surtunmesini onemli olcude azaltir. "Bos sayfa" problemini asmak icin paha bicilmezdir ve gelistiricilerin belirsiz bir kavramdan somut, calistirilabilir koda hizla gecis yapmasini saglar. Vibe coding, ozellikle taniidik olunmayan API'leri kesifederken veya yeni mimari oruntuleri test ederken etkilidir; cunku mukemmel uygulama icin anlik ihtiyaci ortadan kaldirir. Olusturulan kod genellikle yaratici bir katalizor gorevi gorur ve gelistiricilerin elestirmesi, yeniden yapilandirmasi ve genisletmesi icin bir temel saglar. Birincil gucu, yazilim yasam dongusunun baslangic kesif ve fikirlesme asamalarini hizlandirma yetenegiindedir. Ancak, vibe coding beyin firtinasinda mukemmel olsa da, saglam, olceklenebilir ve bakimi kolay yazilim gelistirmek daha yapilandirilmis bir yaklasim gerektirir; salt uretimden uzmanlasmis kodlama agent'lariyla is birlikci bir ortakliga gecis yapilmalidir.

## Ekip Uyeleri Olarak Agent'lar

Baslangic dalgasi ham kod uretimine -- fikirlesme icin mukemmel "vibe code" -- odaklanmis olsa da, sektorde artik uretim calismasi icin daha entegre ve guclu bir paradigmaya dogru bir kayis yasiianmaktadir. En etkili gelistirme ekipleri, gorevleri yalnizca Agent'a devretmekle kalmaz; sofistike kodlama agent'larindan olusan bir paket ile kendilerini guclendirmektedir. Bu agent'lar, yorulmak bilmeyen, uzmanlasmis ekip uyeleri olarak hareket eder, insan yaraticiligini artirirmak ve bir ekibin olceklenebilirligini ve hizini dramatik bir sekilde yukseltir.

Bu evrim, sektorde onderlerin aciiklamalarinda yansimaktadir. 2025 baslarinda Alphabet CEO'su Sundar Pichai, Google'da **"***yeni kodun %30'undan fazlasinin artik Gemini modellerimiz tarafindan destekleniyor veya olusturuluyor olduugunu ve bunun gelistirme hizimizi temelden degistirdigini* belirtmistir.  Microsoft da benzer bir iddiada bulunmustur. Bu sektorde capinda degisim, gercek siniirin gelistiricilerin yerini almak degil, onlari gucllendirmek oldugunu isaretlemektedir. Hedef (Goal), insanlarin mimari vizyonu ve yaratici problem cozmeyi yonlendirdigi, agent'larin ise test, dokumantasyon ve inceleme gibi uzmanlasmis, olceklenebilir gorevleri ele aldigi guclendirilmis bir iliskidir.

Bu bolum, insan gelistiricilerin yaratici liderler ve mimarlar olarak hareket ederken yapay zeka agent'larinin guc carpani olarak islerv gordugu temel felsefeye dayanan bir insan-agent ekibi duzenleme cercevesi sunmaktadir. Bu cerceve uc temel ilke uzerine kuruludur:

1. **Insan Liderliginde Orkestrasyon:** Gelistirici ekip lideri ve proje mimaridir. Her zaman dongunun icindedir, is akisini orkestre eder, ust duzey hedefleri belirler ve nihai kararlari alir. Agent'lar gucludur, ancak destekleyici is birlikcilerdir. Gelistirici hangi agent'in gorevlendirileceegini yonlendirir, gerekli baglami saglar ve en onemlisi, Agent tarafindan olusturulan herhangi bir cikti uzerinde nihai yargiyi uygulayarak projenin kalite standartlari ve uzun vadeli vizyonuyla uyumlu olmasini saglar.
2. **Baglamin Onceligi:** Bir agent'in performansi tamamen baglaminin kalitesine ve eksiksizligine baglidir. Kotukullanilmis baglamla guclu bir LLM isesiizdir. Bu nedenle, cercevemiz titiz, insan liderliginde baglam kurasylonuna oncelik verir. Otomatik, kara kutu baglam erisiminden kacinilir. Gelistirici, Agent ekip uyesi icin mukemmel "brifing"i bir araya getirmekten sorumludur. Bu sunlari icerir:
   * **Eksiksiz Kod Tabani:** Agent'in mevcut oruntuleri ve mantigi anlamasi icin ilgili tum kaynak kodunun saglanmasi.
   * **Harici Bilgi:** Belirli dokumantasyon, API tanimlari veya tasarim belgelerinin saglanmasi.
   * **Insan Brifinggi:** Acik hedefler, gereksinimler, pull request aciklamalari ve stil kilavuzlarinin ifade edilmesi.
3. **Dogrudan Model Erisimi:** En ileri sonuclari elde etmek icin agent'larin sinir modellere (ornegin Gemini 2.5 PRO, Claude Opus 4, OpenAI, DeepSeek vb.) dogrudan erisimle desteklenmesi gerekmektedir. Daha az guclu modeller kullanmak veya istekleri baglami gizleyen veya kisaltan araci platformlar uzerinden yonlendirmek performansi dusurucektir. Cerceve, her agent'in en yuksek potansiyeline ulasmasini saglayarak insan lideri ile altta yatan modelin ham yetenekleri arasinda mumkun olan en saf diyalogu olusturmak uzerine insa edilmistir.

Cerceve, gelistirme yasam dongusundeki temel islevler icin tasarlanmis uzmanlasmis agent'lardan olusan bir ekip olarak yapilandirilmistir. Insan gelistirici, gorevleri devreden ve sonuclari entegre eden merkezi orkestrator olarak hareket eder.

## Temel Bilesenler

Bir sinir Buyuk Dil Modelini etkili bir sekilde kullanmak icin, bu cerceve uzmanlasmis agent'lardan olusan bir ekibe farkli gelistirme rolleri atar. Bu agent'lar ayri uygulamalar degildir; dikkatle hazirlanmis, role ozgu prompt'lar ve baglamlar araciliyla LLM icinde cagirilan kavramsal kisilerdir. Bu yaklasim, modelin genis yeteneklerinin eldeki goreve kesin olarak odaklanmasini saglar; ilk kodu yazmaktan nueansli, elestirel bir inceleme gerceklestirmeye kadar.

**Orkestrator: Insan Gelistirici:** Bu is birlikci cercevede, insan gelistirici Orkestrator olarak hareket eder ve yapay zeka agent'lari uzerinde merkezi zeka ve nihai otorite gorevini ustlenir.

* **Rol:** Ekip Lideri, Mimar ve nihai karar verici. Orkestrator gorevleri tanimlar, baglami hazirlar ve agent'lar tarafindan yapilan tum calismaalari dogrular.
  * **Arayuz:** Gelistiricinin kendi terminali, editoru ve secilen Agent'larin yerel web arayuzu.

**Baglam Hazirlama Alani:** Herhangi bir basarili agent etkilesiminin temeli olarak, Baglam Hazirlama Alani insan gelistiricinin eksiksiz ve goreve ozgu bir brifing titizliikle hazirladigi yerdir.

* **Rol:** Her gorev icin ozel bir calisma alani; agent'larin eksiksiz ve dogru bir brifing almasini saglar.
  * **Uygulama:** Hedefler, kod dosyalari ve ilgili dokumantasyon icin markdown dosyalari iceren gecici bir dizin (task-context/)

**Uzman Agent'lar:** Hedefli prompt'lar kullanarak, her biri belirli bir gelistirme gorevi icin uyarlanmis bir uzman agent ekibi olusturabiliriz.

* **Iskelet Agent: Uygulayici**
  * **Amac:** Ayrintili spesifikasyonlara dayali olarak yeni kod yazar, ozellikler uygular veya sablonlar olusturur.
    * **Cagri Prompt'u:** "*Sen kdemli bir yazilim muhendisisin. 01_BRIEF.md'deki gereksinimlere ve 02_CODE/ icindeki mevcut oruntulere dayanarak ozelliigi uygula...*"
  * **Test Muhendisi Agent: Kalite Muhafizi**
    * **Amac:** Yeni veya mevcut kod icin kapsamli birim testleri, entegrasyon testleri ve uctan uca testler yazar.
    * **Cagri Prompt'u:** "Sen bir kalite guvence muhendisisin. 02_CODE/ icinde saglanan kod icin [Test Framework'u, ornegin pytest] kullanarak eksiksiz bir birim test paketi yaz. Tum uc durumlarini kapsa ve projenin test felsefesine uy."
  * **Belgelendirici Agent: Katip**
    * **Amac:** Fonksiyonlar, siniflar, API'ler veya tum kod tabanlari icin acik, kisa dokumantasyon olusturur.
    * **Cagri Prompt'u:** "Sen bir teknik yazarsin. Saglanan kodda tanimlanan API endpoint'leri icin markdown dokumantasyonu olustur. Istek/yanit orneklerini dahil et ve her parametreyi acikla."
  * **Optimize Edici Agent: Yeniden Yapilandirma Ortagi**
    * **Amac:** Okunabilirliigi, bakimi ve verimliligi iyilestirmek icin performans optimizasyonlari (Optimization) ve kod yeniden yapilandirma onerileri sunar.
    * **Cagri Prompt'u:** "Saglanan kodu performans darbogazlari veya netlik icin yeniden yapilandirilabilecek alanlar acisindan analiz et. Neden bir iyilestirme olduklarini aciklamalarla birlikte belirli degisiklikler oner."
  * **Surec Agent: Kod Denetcisi**
    * **Elestiri:** Agent, potansiyel hatalari, stil ihlallerini ve mantiksal kusurlari belirleyerek ilk gecisi yapar; bir statik analiz araci gibi.
    * **Yansitma (Reflection):** Agent daha sonra kendi elestirisini analiz eder. Bulguları sentezler, en kritik sorunlari onceliklendiirir, bilgic veya dusuk etkili onerileri eler ve insan gelistirici icin ust duzey, eyleme gecirilebilir bir ozet saglar.
    * **Cagri Prompt'u:** "Sen kod incelemesi yapan bir bas muhendissin. Once degisikliklerin ayrintili bir elestirisini yap. Ikinci olarak, en onemli geri bildirimin kisa, onceliklendirilmis bir ozetini saglamak icin elestirinihususun uzerinde yansit."

Sonuc olarak, bu insan liderliginde model, gelistiricinin stratejik yonu ile agent'larin taktiksel yurutmesi arasinda guclu bir sinerji yaratir. Buna bagli olarak, gelistiriciler rutin gorevlerin otesine gecerek uzmanliklarini en fazla deger ureten yaratici ve mimari zorluklara odaklayabilir.

## Pratik Uygulama

### Kurulum Kontrol Listesi

Insan-agent ekip cercevesini etkili bir sekilde uygulamak icin, verimliligi artirirken kontrolu korumaya odaklanan asagidaki kurulum onerilir.

1. **Sinir Modellere Erisim Saglayin** En az iki lider buyuk dil modeli, ornegin Gemini 2.5 Pro ve Claude 4 Opus icin API anahtarlari edinin. Bu cift-saglayici yaklasim karsilastirmali analiz yapmaniza olanak tanir ve tek platform sinirliliklaarina veya kesintilerine karsi koruma saglar. Bu kimlik bilgileri, herhangi bir uretim sirrini yonetir gibi guvenli bir sekilde yonetilmelidir.
2. **Yerel Baglam Orkestratoruunu Uygulayin** Rastgele betikler yerine, baglami yonetmek icin hafif bir CLI araci veya yerel bir agent calistirici kullanin. Bu araclar, proje kokunuzde LLM prompt'u icin hangi dosyalarin, dizinlerin veya hatta URL'lerin tek bir yukte derleneceegini belirten basit bir yapilandirma dosyasi (ornegin context.toml) tanimlaamaniza izin vermelidir. Bu, her istekte modelin ne gordugugu uzerinde tam, seffaf kontrol saglaamanizi garanti eder.
3. **Surum Kontrolluu Prompt Kutuphanesi Olusturun** Projenizin Git deposu icinde ozel bir /prompts dizini olusturun. Icinde, her uzman agent icin cagri prompt'larini (ornegin reviewer.md, documenter.md, tester.md) markdown dosyalari olarak saklayin. Prompt'larinizi kod olarak ele almak, tum ekibin yapay zeka agent'larainiza verilen talimatlari zaman icinde is birligi yaparak islemesine, iyilestirmesine ve surumlendirmesine olanak tanir.
4. **Agent Is Akislarini Git Hook'lariyla Entegre Edin** Yerel Git hook'larini kullanarak inceleme ritminizi otomatiklestirin. Ornegin, bir pre-commit hook, hazirlanmis degisiklikleriniz uzerinde Inceleyici Agent'i otomatik olarak tetikleyecek sekilde yapiilandiirilabilir. Agent'in elestiri ve yansitma ozeti dogrudan terminalinizde sunularak, commit'i sonlandirmadan once aninda geri bildirim saglar ve kalite guvence adimini dogrudan gelistirme sureciinize entegre eder.

![Coding Specialist Examples](../assets/Coding_Specialist_Examples.png)

Sekil 1: Kodlama Uzmani Ornekleri

### Guclendirilmis Ekibi Yonetme Ilkeleri

Bu cercveyi basariyla yonetmek, tek basina katkida bulunandan insan-yapay zeka ekibinin liderine evrilerek asagidaki ilkeler rehberliginde ilerlemeyi gerektirir:

* **Mimari Sahipligi Koruyun** Rolunuz stratejik yonu belirlemek ve ust duzey mimariyi sahiplenmektir. "Ne" ve "neden"i siz tanimlar, agent ekibini "nasil"i hizlandirmak icin kullanirsiniz. Tasarimin nihai **hakemi** siz olarak, her bilesenin projenin uzun vadeli vizyonu ve kalite standartlariyla uyumlu olmasini saglarsiniiz.
* **Brifing Sanatini Ustun** Bir agent'in ciktisinin kalitesi, girdisinin kalitesinin dogrudan bir yansiimasidir. Her gorev icin acik, belirsizlik icermeyen ve kapsamli baglam saglayarak brifing sanatinda ustalasin. Prompt'unuzu basit bir komut olarak degil, yeni, son derece yetenekli bir ekip uyesi icin eksiksiz bir brifing paketi olarak dusunun.
* **Nihai Kalite Kapisi Olarak Hareket Edin** Bir agent'in ciktisi her zaman bir oneri, asla bir emirdir. Inceleyici Agent'in geri bildirimini guclu bir sinyal olarak degerlendirin, ancak nihai kalite kapisi sizsiniz. Tum degisiklikleri dogrulamak, sorgulamak ve onaylamak icin alan uzmanliginizi ve projeye ozgu bilginizi uygulayarak kod tabaninin butunlugunun son muhafizi olarak hareket edin.
* **Yinelemeli Diyalog Yur** En iyi sonuclar monologdan degil, konusmadan cikar. Bir agent'in ilk ciktisi kusurlu ise, onu atmayin -- iyilestirin. Duzeltici geri bildirim saglayin, aciklayici baglam ekleyin ve baska bir deneme icin yonlendirin. Bu yinelemeli diyalog, ozellikle "Yansitma" ciktisi nihai bir rapor degil, is birlikci bir tartismanin baslangici olarak tasarlanmis Inceleyici Agent ile kritik oneme sahiptir.

## Sonuc

Kod gelistirmenin gelecegi gelmistir ve guclendirilmistir. Yalniz kodlayici donemi, gelistiricilerin uzmanlasmis yapay zeka agent'larindan olusan ekipleri yonettigi yeni bir paradigmaya yerini birakmiistir. Bu model, insan rolunu azaltmaz; rutin gorevleri otomatiklestirerek, bireysel etkiyi olcekleendirerek ve daha once hayal edilemeyen bir gelistirme hizina ulasarak onu yuceltir.

Taktik yurutmeyi Agent'lara devederek, gelistiriciler artik bilissel enerjilerini gercekten onemli olana adayabilir: stratejik yenilik, dayanikli mimari tasarim ve kullanicilari memnun eden urunler insa etmek icin gereken yaratici problem cozme. Temel iliski yeniden tanimlanmistir; artik insan-makine yarismasi degil, tek, sorunsuz entegre bir ekip olarak calisan insan yaraticiligi ve yapay zeka arasinda bir ortakliktir.

## Kaynaklar

1. AI is responsible for generating more than 30% of the code at Google [https://www.reddit.com/r/singularity/comments/1k7rxo0/ai_is_now_writing_well_over_30_of_the_code_at/](https://www.reddit.com/r/singularity/comments/1k7rxo0/ai_is_now_writing_well_over_30_of_the_code_at/)
2. AI is responsible for generating more than 30% of the code at Microsoft [https://www.businesstoday.in/tech-today/news/story/30-of-microsofts-code-is-now-ai-generated-says-ceo-satya-nadella-474167-2025-04-30](https://www.businesstoday.in/tech-today/news/story/30-of-microsofts-code-is-now-ai-generated-says-ceo-satya-nadella-474167-2025-04-30)
