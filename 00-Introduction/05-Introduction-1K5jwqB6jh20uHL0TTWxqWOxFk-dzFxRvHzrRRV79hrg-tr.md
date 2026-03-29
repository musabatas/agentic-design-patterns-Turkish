# Onsoz

"Agentic Design Patterns: A Hands-On Guide to Building Intelligent Systems" kitabina hos geldiniz. Modern yapay zeka manzarasina baktigimizda, basit, tepkisel programlardan baglami anlayabilen, kararlar alabilen ve cevreleriyle ve diger sistemlerle dinamik olarak etkilesime girebilen sofistike, otonom varliklara dogru acik bir evrim goruyoruz. Bunlar akilli agent'lar ve bunlarin olusturdugu agentic sistemlerdir.

Guclu buyuk dil modellerinin (LLM) ortaya cikisi, bu agent'larin bircogi icin bilissel motor gorevi gorerek, insan benzeri metin ve medya gibi icerikleri anlama ve uretme konusunda benzeri gorulmemis yetenekler saglamistir. Ancak bu yetenekleri karmasik hedefleri guvenilir bir sekilde gerceklestirebilen sistemlere donusturmek, guclu bir modelden daha fazlasini gerektirir. Agent'in nasil algilayacagina, planlayacagina, harekete gececegine ve etkilesime girecegine dair yapi, tasarim ve dusunceli bir yaklasim gerektirir.

Akilli sistemler insa etmeyi, bir tuval uzerinde karmasik bir sanat eseri veya muhendislik projesi olusturmak olarak dusunun. Bu tuval bos bir gorsel alan degil, agent'larinizin var olmasi ve calismasi icin ortam ve araclari saglayan altyapi ve framework'lerdir. Akilli uygulamanizi uzerine insa edeceginiz temeldir; durum, iletisim (Communication), arac erisimi ve mantik akisini yonetir.

Bu agentic tuval uzerinde etkili bir sekilde insa etmek, bilesenleri rastgele bir araya getirmekten daha fazlasini gerektirir. Agent davranisini tasarlama ve uygulamadaki ortak zorluklari ele alan kanitlanmis teknikleri --**kaliplari**-- anlamayi gerektirir. Nasil ki mimari kaliplar bir binanin insasina rehberlik ediyorsa veya tasarim kaliplari (Design Patterns) yazilimi yapilandiriyorsa, agentic tasarim kaliplari da sectiginiz tuval uzerinde akilli agent'lari hayata gecirirken karsilasacaginiz tekrarlayan sorunlara yeniden kullanilabilir cozumler sunar.

## Agentic Sistemler Nedir?

Ozunde bir agentic sistem, cevresini (hem dijital hem de potansiyel olarak fiziksel) algilamak, bu algilara ve onceden tanimlanmis veya ogrenilmis hedeflere dayali bilinçli kararlar almak ve bu hedeflere otonom olarak ulasmak icin eylemler yuruten bir hesaplama varligi olarak tasarlanmistir. Kati, adim adim talimatlari izleyen geleneksel yazilimin aksine, agent'lar belirli bir esneklik ve insiyatif sergiler.

Musteri sorgularini yonetecek bir sisteme ihtiyaciniz oldugunu hayal edin. Geleneksel bir sistem sabit bir senaryo izleyebilir. Oysa bir agentic sistem, bir musterinin sorgusunun nüanslarini algilayabilir, bilgi tabanilarina erisebilir, diger dahili sistemlerle (siparis yonetimi gibi) etkilesime girebilir, gerektiginde aciklayici sorular sorabilir ve sorunu proaktif olarak cozebilir, hatta gelecekteki ihtiyaclari bile onceden tahmin edebilir. Bu agent'lar, uygulamanizin altyapisindan olusan tuval uzerinde calisarak kendilerine sunulan hizmet ve verilerden yararlanir.

Agentic sistemler genellikle su ozelliklerle karakterize edilir: surekli insan gozetimi olmadan hareket etmeye olanak taniyan **otonomi**; hedeflerine yonelik eylemleri baslatma olan **proaktiflik**; cevresindeki degisikliklere etkili bir sekilde yanit veren **reaktiflik**. Temelde **hedefe yonelik**dirler ve surekli olarak amaclarini gerceklestirmeye calisirlar. Kritik bir yetenek olan **tool use**, harici API'ler, veritabanlari veya hizmetlerle etkilesim kurmalarini --fiilen kendi tuvallerinin otesine uzanmalarini-- saglar. **Bellek** (Memory) sayesinde etkilesimler boyunca bilgiyi korurlar ve kullanicilar, diger sistemler veya ayni ya da bagli tuvallerde calisan diger agent'larla **iletisim** (Communication) kurabilirler.

Bu ozellikleri etkili bir sekilde gerceklestirmek onemli bir karmasiklik getirir. Agent, tuvalinde birden fazla adim boyunca durumu nasil korur? Bir araci *ne zaman* ve *nasil* kullanacagina nasil karar verir? Farkli agent'lar arasindaki iletisim nasil yonetilir? Beklenmedik sonuclari veya hatalari ele almak icin sisteme nasil dayaniklilik insa edersiniz?

## Agent Gelistirmede Kaliplar Neden Onemlidir

Bu karmasiklik, agentic tasarim kaliplarinin (Design Patterns) neden vazgecilmez oldugunu tam olarak aciklar. Bunlar kati kurallar degil, agentic alanda standart tasarim ve uygulama zorluklarina kanitlanmis yaklasimlar sunan, savas alaninda test edilmis sablonlar veya planlardir. Bu tasarim kaliplarini taniyor ve uyguluyor olarak, tuvaliniz uzerinde insa ettiginiz agent'larin yapisini, bakim kolayligini, guvenilirligini ve verimliligi artiran cozumlere erisim kazanirsiniz.

Tasarim kaliplari kullanmak, konusma akisi yonetimi, harici yeteneklerin entegrasyonu veya birden fazla agent eyleminin koordinasyonu gibi gorevler icin temel cozumleri yeniden icat etmenizi onler. Agent'inizin mantigini daha net ve baskalarinin (ve gelecekte kendinizin) anlamasini ve bakimini kolaylastiran ortak bir dil ve yapi saglarlar. Hata yonetimi (Exception Handling) veya durum yonetimi icin tasarlanmis kaliplarin uygulanmasi, daha saglam ve guvenilir sistemler insa etmeye dogrudan katkida bulunur. Bu yerlesik yaklasimlari kullanmak gelistirme surecinizi hizlandirir ve agent davranisinin temel mekaniklerine degil, uygulamanizin benzersiz yonlerine odaklanmanizi saglar.

Bu kitap, cesitli teknik tuvaller uzerinde sofistike agent'lar insa etmek icin temel yapi taslari ve teknikleri temsil eden 21 temel tasarim kalibini ortaya koymaktadir. Bu kaliplari anlamak ve uygulamak, akilli sistemleri etkili bir sekilde tasarlama ve uygulama becerinizi onemli olcude yukseltecektir.

## Kitaba Genel Bakis ve Nasil Kullanilir

Bu kitap, "Agentic Design Patterns: A Hands-On Guide to Building Intelligent Systems", pratik ve erisilebilir bir kaynak olarak tasarlanmistir. Birincil odagi, her bir agentic kalibi acikca aciklamak ve uygulamasini gostermek icin somut, calistirilabilir kod ornekleri sunmaktir. 21 ozel bolumd boyunca, ardisik islemleri yapilandirma (Prompt Chaining) ve harici etkilesim (Tool Use) gibi temel kavramlardan is birligi (Multi-Agent Collaboration) ve ozduzeltme (Self-Correction) gibi daha ileri konulara kadar genis bir tasarim kaliplari yelpazesini kesfedecegiz.

Kitap bolum bolum organize edilmistir ve her bolum tek bir agentic kaliba derinlemesine dalmaktadir. Her bolumde su bilesenleri bulacaksiniz:

* Kalibin ve agentic tasarimdaki rolunun acik bir aciklamasini sunan ayrintili bir **Kalip Genel Bakisi**.
* Kalibin vazgecilmez oldugu gercek dunya senaryolarini ve sagladigi faydalari gosteren **Pratik Uygulamalar ve Kullanim Alanlari** bolumu.
* Kalibin uygulamasini onemli agent gelistirme framework'leri kullanarak gosteren pratik, calistirilabilir kod sunan bir **Uygulamali Kod Ornegi**. Kalibin teknik bir tuval baglaminda nasil uygulandigini burada goreceksiniz.
* Hizli gozden gecirme icin en kritik noktalari ozetleyen **Temel Cikarimlar**.
* Kalip ve ilgili kavramlar uzerine daha derin ogrenme icin kaynaklar sunan **Referanslar**.

Bolumler kavramlari kademeli olarak olusturacak sekilde siralanmis olsa da, kitabi bir referans olarak kullanip kendi agent gelistirme projelerinizde karsilastiginiz belirli zorluklari ele alan bolumlere atlamaktan cekinmeyin. Ekler, ileri prompt teknikleri, AI agent'larini gercek dunya ortamlarinda uygulama ilkeleri ve temel agentic framework'lere genel bir bakis sunmaktadir. Buna ek olarak, AgentSpace gibi belirli platformlarla ve komut satiri arabirimi icin agent insa etme konusunda adim adim rehberlik sunan pratik, yalnizca cevrimici egitimler dahil edilmistir. Vurgu boyunca pratik uygulama uzerindedir; kod orneklerini calistirmanizi, bunlarla deney yapmanizi ve sectiginiz tuval uzerinde kendi akilli sistemlerinizi insa etmek icin uyarlamanizi siddetle tesvik ediyoruz.

Sik duydugum harika bir soru su: 'AI bu kadar hizli degisirken, cabuk eskiyebilecek bir kitap neden yazilir?' Motivasyonum aslinda tam tersiydi. Her seyin bu kadar hizli hareket etmesi, tam da bu nedenle bir adim geri atip saglasmalasan temel ilkeleri belirlememiz gerektigini gosteriyor. RAG, Reflection, Routing, Memory ve tartistigim diger kaliplar temel yapi taslari haline geliyor. Bu kitap, uzerine insa etmemiz gereken temeli saglayan bu cekirdek fikirleri uzerine dusunmeye bir davettir. Insanlarin temel kaliplar uzerinde bu dusunme anlarina ihtiyaci vardir.

## Kullanilan Framework'lere Giris

Kod orneklerimiz icin somut bir "tuval" saglamak uzere (ayrica bkz. Ek), oncelikli olarak uc onemli agent gelistirme framework'u kullanacagiz. **LangChain**, durum yonetimi uzantisi **LangGraph** ile birlikte, dil modellerini ve diger bilesenleri zincirlemek icin esnek bir yol sunarak karmasik islem dizileri ve grafikleri olusturmak icin saglam bir tuval saglar. **Crew AI**, birden fazla AI agent'ini, rolunu ve gorevini orkestre etmek icin ozellikle tasarlanmis yapilandirilmis bir framework sunarak ozellikle is birlikci agent sistemleri icin uygun bir tuval gorevi gorur. **Google Agent Developer Kit (Google ADK)**, agent'lar insa etmek, degerlendirmek ve dagitmak icin araclar ve bilesenler sunarak genellikle Google'in AI altyapisiyla entegre, bir baska degerli tuval saglar.

Bu framework'ler, agent gelistirme tuvalinin farkli yonlerini temsil eder ve her birinin guclü yanlari vardir. Bu araclar uzerinde ornekler gostererek, agentic sistemleriniz icin sectiginiz belirli teknik ortamdan bagimsiz olarak kaliplarin nasil uygulanabilecegine dair daha genis bir anlayis kazanacaksiniz. Ornekler, kalibin temel mantigini ve framework'un tuvali uzerindeki uygulamasini aciklik ve pratiklige odaklanarak net bir sekilde gosterecek sekilde tasarlanmistir.

Bu kitabin sonunda, 21 temel agentic kalibin arkasindaki temel kavramlari anlamakla kalmayacak, ayni zamanda bunlari etkili bir sekilde uygulamak icin pratik bilgi ve kod orneklerine sahip olacak ve sectiginiz gelistirme tuvali uzerinde daha akilli, yetenekli ve otonom sistemler insa etmenizi saglayacaksiniz. Haydi bu uygulamali yolculuga baslayalim!
