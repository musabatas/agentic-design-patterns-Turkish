# Bir AI Sistemini Agent Yapan Nedir?

Basit bir ifadeyle, bir **AI agent**, cevresini algilamak ve belirli bir hedefe ulasmak icin eylemler gerceklestirmek uzere tasarlanmis bir sistemdir. Standart bir Buyuk Dil Modelinin (LLM) evrimidir ve planlama, arac kullanma ve cevresiylen etkilesim kurma yetenekleriyle guclendirilmistir. Agentic AI'yi is basinda ogrenen akilli bir asistan olarak dusunun. Isleri halletmek icin basit, bes adimli bir dongu izler (bkz. Sekil 1):

1. **Gorevi Al:** Ona "takvimimi duzenle" gibi bir hedef verirsiniz.
2. **Ortami Tara:** E-postalari okuyarak, takvimleri kontrol ederek ve kisilere eriserek neler oldugunu anlamak icin gerekli tum bilgileri toplar.
3. **Dusun:** Hedefe ulasmak icin en uygun yaklasimi degerlendirerek bir eylem plani olusturur.
4. **Harekete Gec:** Davetiye gondererek, toplantilar planlayarak ve takviminizi guncelleyerek plani yurutur.
5. **Ogren ve Gelis:** Basarili sonuclari gozlemler ve buna gore uyum saglar. Ornegin, bir toplanti yeniden planlanirsa, sistem gelecekteki performansini artirmak icin bu olaydan ogrenme (Learning) yapar.

![Agentic AI Problem-Solving Process](../assets/Agentic_AI_Problem_Solving_Process.png)

Sekil 1: Agentic AI, deneyimlerden surekli ogrenen akilli bir asistan olarak isler. Gorevleri yerine getirmek icin basit bir bes adimli dongu uzerinden calisir.

Agent'lar sasirtici bir hizla giderek daha populer hale gelmektedir. Son calismalara gore, buyuk BT sirketlerinin buyuk cogunlugu bu agent'lari aktif olarak kullanmakta ve bestte biri gecen yil icinde kullanmaya baslamistir. Finans piyasalari da bunu fark etmektedir. 2024 sonuna kadar, AI agent startup'lari 2 milyar dolardan fazla yatirim toplamis ve pazarin degeri 5,2 milyar dolar olarak belirlenmistir. 2034'e kadar yaklasik 200 milyar dolara ulasmasi beklenmektedir. Kisacasi, tum isaretler AI agent'larinin gelecek ekonomimizde buyuk bir rol oynayacagina isaret etmektedir.

Sadece iki yil icinde, AI paradigmasi dramatik bir sekilde degisti; basit otomasyondan sofistike, otonom sistemlere gecis yapildi (bkz. Sekil 2). Baslangicta, is akislari verileri LLM'lerle islemek icin temel prompt'lara ve tetikleyicilere dayaniyordu. Bu, modelleri olgusal bilgilerle temelleyerek guvenilirligi artiran Retrieval-Augmented Generation (RAG) ile evrimlesti. Ardindan cesitli araclari kullanabilen bireysel AI Agent'larinin gelismesini gorduk. Bugun, uzmanlasmis agent'lardan olusan bir ekibin karmasik hedeflere ulasmak icin uyum icinde calistigi Agentic AI cagina giriyoruz; bu, AI'nin is birlikci gucunde onemli bir sicramayi isaret ediyor.

![Transitioning from LLMs to RAG, then to Agentic RAG, and finally to Agentic AI](../assets/Transitioning_from_LLMs_to_RAG_to_Agentic_RAG_to_Agentic_AI.png)

Sekil 2: LLM'lerden RAG'e, ardindan Agentic RAG'e ve son olarak Agentic AI'ya gecis.

Bu kitabin amaci, uzmanlasmis agent'larin nasil uyum icinde calisip karmasik hedeflere ulasmak icin is birligi (Collaboration) yapabileceginin tasarim kaliplarini (Design Patterns) tartismaktir ve her bolumde bir is birligi ve etkilesim paradigmasi goreceksiniz.

Bunu yapmadan once, agent karmasikligi yelpazesini kapsayan ornekleri inceleyelim (bkz. Sekil 3).

## Seviye 0: Temel Akil Yurutme Motoru

Bir LLM kendi basina bir agent olmasa da, temel bir agentic sistemin akil yurutme (Reasoning) cekirdegi olarak hizmet edebilir. Bir 'Seviye 0' yapilandirmasinda, LLM araclar, bellek veya cevre etkilesimi olmadan calisir ve yalnizca on-egitimli bilgisine dayali olarak yanit verir. Gucu, yerlesik kavramlari aciklamak icin kapsamli egitim verilerinden yararlanmasinda yatar. Bu guclu dahili akil yurutmenin bedeliyse, guncel olaylara dair tam bir farkindelik eksikligidir. Ornegin, bu bilgi on-egitimli bilgisinin disindaysa, 2025 Oscar "En Iyi Film" odul sahibini soyleyemez.

## Seviye 1: Bagli Problem Cozucu

Bu seviyede, LLM harici araclara baglanan ve bunlari kullanan islevsel bir agent haline gelir. Problem cozme kapasitesi artik on-egitimli bilgisiyle sinirli degildir. Bunun yerine, internet (arama yoluyla) veya veritabanlari (Retrieval Augmented Generation veya RAG yoluyla) gibi kaynaklardan bilgi toplamak ve islemek icin bir dizi eylem yurutebilir. Ayrintili bilgi icin Bolum 14'e bakiniz.

Ornegin, yeni TV programlarini bulmak icin agent guncel bilgiye ihtiyac duyuldugunu fark eder, bulmak icin bir arama araci kullanir ve ardindan sonuclari sentezler. Onemli olarak, daha yuksek dogruluk icin uzmanlasmis araclar da kullanabilir; ornegin AAPL'nin canli hisse senedi fiyatini almak icin bir finans API'si cagirabilir. Birden fazla adimda dis dunyayla etkilesim kurma yetenegi, Seviye 1 agent'inin temel kabiliyetidir.

## Seviye 2: Stratejik Problem Cozucu

Bu seviyede, bir agent'in yetenekleri onemli olcude genisler; stratejik planlama (Planning), proaktif yardim ve kendini gelistirmeyi kapsar; prompt engineering ve context engineering temel yetkinliklerdir.

Ilk olarak, agent tek arac kullaniminin otesine gecip stratejik problem cozme yoluyla karmasik, cok parcali sorunlarla basa cikar. Bir dizi eylem yurutturken, her adim icin en ilgili bilgiyi secme, paketleme ve yonetme stratejik sureci olan context engineering'i aktif olarak gerceklestirir. Ornegin, iki konum arasinda bir kahveci bulmak icin once bir harita araci kullanir. Ardindan bu ciktiyi muhendislik eder; bilissel asiri yuklemeyi onlemek ve ikinci adimin verimli ve dogru olmasini saglamak icin belki sadece bir sokak isimleri listesi olan kisa, odaklanmis bir baglam hazirlar ve yerel bir arama aracina besler. Bir AI'dan maksimum dogruluk elde etmek icin ona kisa, odaklanmis ve guclu bir baglam verilmelidir. Context engineering, mevcut tum kaynaklardan en kritik bilgiyi stratejik olarak secerek, paketleyerek ve yoneterek bunu basaran disiplindir. Modelin sinirli dikkatini etkili bir sekilde yoneterek asiri yuklemeyi onler ve herhangi bir gorevde yuksek kaliteli, verimli performans saglar. Ayrintili bilgi icin Ek A'ya bakiniz.

Bu seviye proaktif ve surekli calismaya yol acar. E-postaniza bagli bir seyahat asistani bunu gosterir; uzun bir ucus onay e-postasindan baglami muhendislik eder; takviminize ve bir hava durumu API'sine yapilacak sonraki arac cagrilari icin yalnizca anahtar detayleri (ucus numaralari, tarihler, konumlar) secer.

Yazilim muhendisligi gibi uzmanlasmis alanlarda, agent bu disiplini uygulayarak tum is akisini yonetir. Bir hata raporu atandiginda, raporu okur ve kod tabanina erisir, ardindan bu buyuk bilgi kaynaklarini stratejik olarak muhendislik ederek dogru kod yamasini verimli bir sekilde yazmak, test etmek ve gondermek icin guclu, odaklanmis bir baglama donusturur.

Son olarak, agent kendi context engineering sureclerini rafine ederek kendini gelistirme basarir. Bir prompt'un nasil iyilestirilebilecegi konusunda geri bildirim istediginde, baslangic girdilerini daha iyi nasil duzenleyecegini ogrenmektedir. Bu, gelecekteki gorevler icin bilgiyi nasil paketledigini otomatik olarak iyilestirmesine olanak tanir ve zaman icinde dogrulugunu ve verimliligi artiran guclu, otomatik bir geri bildirim dongusu olusturur. Ayrintili bilgi icin Bolum 17'ye bakiniz.

![Various Instances Demonstrating the Spectrum of Agent Complexity](../assets/Various_Instances_Demonstrating_the_Spectrum_of_Agent_Complexity.png)

Sekil 3: Agent karmasikligi yelpazesini gosteren cesitli ornekler.

## Seviye 3: Is Birlikci Multi-Agent Sistemlerin Yukselisi

Seviye 3'te, AI gelistirmede onemli bir paradigma degisimi goruyoruz; tek, her seye kadir bir super agent arayisindan sofistike, is birlikci multi-agent sistemlerin yukselisine dogru bir gecis. Ozunde bu yaklasim, karmasik zorluklarin genellikle tek bir genelci tarafindan degil, uyum icinde calisan bir uzmanlar ekibi tarafindan en iyi sekilde cozuldugunu kabul eder. Bu model, farkli departmanlara belirli roller atanan ve cok yonlu hedefleri ele almak icin is birligi yapan bir insan organizasyonunun yapisini dogrudan yansitir. Boyle bir sistemin kolektif gucu, bu is bolumu ve koordineli caba yoluyla yaratilan sinerjide yatar. Ayrintili bilgi icin Bolum 7'ye bakiniz.

Bu kavrami somutlastirmak icin, yeni bir urun lansman surecinin karmasik is akisini dusunun. Tek bir agent'in her yonu ele almaya calismasi yerine, bir "Proje Yoneticisi" agent'i merkezi koordinator olarak hizmet edebilir. Bu yonetici, gorevleri diger uzmanlasmis agent'lara devrederek tum sureci orkestre eder: tuketici verilerini toplamak icin bir "Pazar Arastirmasi" agent'i, kavramlar gelistirmek icin bir "Urun Tasarimi" agent'i ve tanitim materyalleri hazirlamak icin bir "Pazarlama" agent'i. Basarilarinin anahtari, aralarindaki kesintisiz iletisim ve bilgi paylasimidir; tum bireysel cabalarin kolektif hedefe ulasmak icin uyumlu olmasini saglar.

Otonom, ekip tabanli otomasyonun bu vizyonu halihazirda gelistirilmekte olsa da, mevcut engelleri kabul etmek onemlidir. Bu tur multi-agent sistemlerin etkinligi, su anda kullandiklari LLM'lerin akil yurutme sinirlamalari tarafindan kisitlanmaktadir. Ayrica, birbirlerinden gercekten ogrenme ve tutarli bir birim olarak gelisme yetenekleri hala erken asamalarindadir. Bu teknolojik darbogazlarin asılmasi kritik bir sonraki adimdir ve bunu basarmak, bu seviyenin derin vaadini ortaya cikaracaktir: tum is sureclerini bastan sona otomatiklestirme yetenegi.

## Agent'larin Gelecegi: En Onemli 5 Hipotez

AI agent gelistirme, yazilim otomasyonu, bilimsel arastirma ve musteri hizmetleri gibi alanlarda benzeri gorulmemis bir hizla ilerlemektedir. Mevcut sistemler etkileyici olsa da, henuz baslangiç asamasindadir. Bir sonraki yenilik dalgasi muhtemelen agent'lari daha guvenilir, is birlikci ve hayatlarimiza daha derinden entegre hale getirmeye odaklanacaktir. Gelecek icin bes oncu hipotez sunuyoruz (bkz. Sekil 4).

### Hipotez 1: Genelci Agent'in Ortaya Cikisi

Ilk hipotez, AI agent'larinin dar uzmanlardan, karmasik, belirsiz ve uzun vadeli hedefleri yuksek guvenilirlikle yonetebilen gercek genelcilere evrilecegi yonundedir. Ornegin, bir agent'a "Gelecek ceyrekte Lizbon'da 30 kisilik sirket ofis disitoplantimi planla" gibi basit bir prompt verebilirsiniz. Agent daha sonra haftalarca tum projeyi yonetir; butce onaylarindan ucus muzakerelerine, mekan seciminden calisanlarin geri bildirimlerinden ayrintili bir program olusturmaya kadar her seyi halleder ve duzenli guncellemeler saglar. Bu otonomi seviyesine ulasmak, AI akil yurutme, bellek ve neredeyse mukemmel guvenilirlikte temel atilimlar gerektirecektir. Alternatif ama birbirini dislamayan bir yaklasim, Kucuk Dil Modellerinin (SLM) yukselisidir. Bu "Lego benzeri" kavram, tek bir monolitik modeli olceklendirmek yerine kucuk, uzmanlasmis uzman agent'lardan sistemler olusturmayi icerir. Bu yontem, daha ucuz, hata ayiklamasi daha kolay ve dagitimi daha basit sistemler vaat eder. Nihayetinde, buyuk genelci modellerin gelistirilmesi ve daha kucuk uzmanlasmis modellerin kompozisyonu, her ikisi de makul yollardir ve birbirini tamamlayabilir.

### Hipotez 2: Derin Kisisellesirme ve Proaktif Hedef Kesfi

Ikinci hipotez, agent'larin derinden kissellestirilmis ve proaktif ortaklar haline gelecegini one surmektedir. Yeni bir agent sinifinin ortaya cikisina tanik oluyoruz: proaktif ortak. Benzersiz kaliplarınızdan ve hedeflerinizden ogrenen bu sistemler, sadece emirleri yerine getirmekten ihtiyaclarinizi onceden tahmin etmeye dogru gecmeye baslamaktadir. AI sistemleri, sohbetlere veya talimatlara sadece yanit vermenin otesine gecip kullanici adina gorevleri baslatip yuruttukleri ve surecte aktif olarak is birligi yaptiklari zaman agent olarak isler. Bu, basit gorev yurütmenin otesine gecerek proaktif hedef kesfi (Discovery) alanina girer.

Ornegin, surdurulebilir enerjiyi arastiriyorsaniz, agent gizli hedefinizi belirleyebilir ve kurslar onererek veya arastirmalari ozetleyerek proaktif olarak destekleyebilir. Bu sistemler hala gelisirken, izledikleri yol aciktir. Giderek daha proaktif hale gelecek ve eylemin yardimci olacagindan yuksek duzeyde emin olduklarinda sizin adınıza insiyatif almayi ogreneceklerdir. Nihayetinde agent, henuz tam olarak dile getirmediginiz tutkularinizi kesfetmenize ve gerceklestirmenize yardimci olan vazgecilmez bir muttefik haline gelir.

![Five Hypotheses about the Future of Agents](../assets/Five_Hypotheses_about_the_Future_of_Agents.png)

Sekil 4: Agent'larin gelecegine dair bes hipotez

### Hipotez 3: Cisimlesme ve Fiziksel Dunyayla Etkilesim

Bu hipotez, agent'larin tamamen dijital sinirlarindan kurtularak fiziksel dunyada faaliyet gosterecegini ongormektedir. Agentic AI'yi robotikle butunlestirerek, "cisimlestirilmis agent'larin" yukselisini gorecegiz. Bir tamirci cagirmak yerine, ev agent'inizdan sizinti yapan bir musluyu tamir etmesini isteyebilirsiniz. Agent, sorunu algilamak icin goruntu sensorlerini kullanir, bir plan olusturmak icin bir tesisatcilik bilgi kutuphanesine erisir ve ardindan tamiri gerceklestirmek icin robotik manipulatorlerini hassasiyetle kontrol eder. Bu, dijital zeka ile fiziksel eylem arasindaki ucurumu kapatarak, imalattan lojistige, yasli bakimindan ev bakimina kadar her seyi donusturecek cok buyuk bir adim olacaktir.

### Hipotez 4: Agent Gucuyle Calisn Ekonomi

Dorduncu hipotez, yuksek duzeyde otonom agent'larin ekonomide aktif katilimcilar haline gelecegi ve yeni pazarlar ve is modelleri yaratacagi yonundedir. Agent'larin, kar gibi belirli bir sonucu maksimize etmekle gorevlendirilmis bagimsiz ekonomik varliklar olarak hareket ettigini gorebiliriz. Bir girisimci, tum bir e-ticaret isini yurutmek icin bir agent baslabilir. Agent, sosyal medyayi analiz ederek trend urunleri belirler, pazarlama metni ve gorselleri uretir, diger otomatik sistemlerle etkilesime girerek tedarik zinciri lojistigini yonetir ve gercek zamanli talebe gore fiyatlandirmayi dinamik olarak ayarlar. Bu degisim, insanlarin dogrudan yonetmesinin imkansiz oldugu bir hiz ve olcekte calisan yeni, hiper verimli bir "agent ekonomisi" yaratacaktir.

### Hipotez 5: Hedefe Yonelik, Metamorfik Multi-Agent Sistemi

Bu hipotez, acik programlamadan degil, beyan edilmis bir hedeften hareket eden akilli sistemlerin ortaya cikisini one surmektedir. Kullanici yalnizca istenen sonucu belirtir ve sistem buna nasil ulasacagini otonom olarak belirler. Bu, hem bireysel hem de kolektif duzeyde gercek kendini gelistirme kapasitesine sahip metamorfik multi-agent sistemlerine dogru temel bir geçisi isaret eder.

Bu sistem dinamik bir varlik olacaktir, tek bir agent degil. Kendi performansini analiz etme ve multi-agent is gucunun topolojisini degistirme; eldeki gorev icin en etkili ekibi olusturmak amaciyla gerektiginde agent'lar yaratma, coglama veya kaldirma yetenegine sahip olacaktir. Bu evrim birden fazla duzeyde gerceklesir:

* Mimari Degisiklik: En derin duzeyde, bireysel agent'lar kendi kaynak kodlarini yeniden yazabilir ve daha yuksek verimlilik icin ic yapilarini yeniden mimarlandirbilir; orijinal hipotezdeki gibi.
* Talimat Degisikligi: Daha ust duzeyde, sistem surekli olarak otomatik prompt engineering ve context engineering gerceklestirir. Herhangi bir insan mudahalesi olmadan, her agent'a verilen talimatlari ve bilgileri rafine ederek optimal rehberlikle calismalirini saglar.

Ornegin, bir girisimci sadece niyetini beyan eder: "El yapimi kahve satan basarili bir e-ticaret isletmesi kur." Sistem, baska bir programlama olmadan harekete gecer. Baslangicta bir "Pazar Arastirmasi" agent'i ve bir "Markalasmira" agent'i olusturabilir. Ilk bulgulara dayanarak, markalasmira agent'ini kaldirip uc yeni uzmanlasmis agent olusturmaya karar verebilir: bir "Logo Tasarimi" agent'i, bir "Web Magaza Platformu" agent'i ve bir "Tedarik Zinciri" agent'i. Dahili prompt'larini daha iyi performans icin surekli olarak ayarlar. Web magaza agent'i bir darbogazhaline gelirse, sistem sitenin farkli bolumlerinde calismak uzere onu uc paralel agent'a coglayabilir ve beyan edilen hedefe en iyi sekilde ulasmak icin kendi yapisini aninda yeniden mimarlandirir.

## Sonuc

Ozunde, bir AI agent'i geleneksel modellerden onemli bir sicramayi temsil eder; belirli hedeflere ulasmak icin algılayan, planlayan ve harekete gecen otonom bir sistem olarak isler. Bu teknolojinin evrimi, tek, arac kullanan agent'lardan cok yonlu hedefleri ele alan karmasik, is birlikci multi-agent sistemlerine dogru ilerlemektedir. Gelecek hipotezleri; genelci, kisisellestirilmis ve hatta fiziksel olarak cisimlestirilmis agent'larin ekonomide aktif katilimcilar haline gelecegini ongormektedir. Bu surregelen gelişme, tum is akislarini otomatiklestirmeye ve teknolojyle olan iliskimizi temelden yeniden tanimlamaya hadir, kendini gelistiren, hedefe yonelik sistemlere dogru buyuk bir paradigma degisiminin sinyalini vermektedir.

## Referanslar

1. Cloudera, Inc. (April 2025), 96% of enterprises are increasing their use of AI agents.[https://www.cloudera.com/about/news-and-blogs/press-releases/2025-04-16-96-percent-of-enterprises-are-expanding-use-of-ai-agents-according-to-latest-data-from-cloudera.html](https://www.cloudera.com/about/news-and-blogs/press-releases/2025-04-16-96-percent-of-enterprises-are-expanding-use-of-ai-agents-according-to-latest-data-from-cloudera.html)
2. Autonomous generative AI agents: [https://www.deloitte.com/us/en/insights/industry/technology/technology-media-and-telecom-predictions/2025/autonomous-generative-ai-agents-still-under-development.html](https://www.deloitte.com/us/en/insights/industry/technology/technology-media-and-telecom-predictions/2025/autonomous-generative-ai-agents-still-under-development.html)
3. Market.us. Global Agentic AI Market Size, Trends and Forecast 2025–2034. [https://market.us/report/agentic-ai-market/](https://market.us/report/agentic-ai-market/)
