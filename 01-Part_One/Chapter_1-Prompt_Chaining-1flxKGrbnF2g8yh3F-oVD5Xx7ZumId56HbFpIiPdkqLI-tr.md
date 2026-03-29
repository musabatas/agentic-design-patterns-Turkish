# Bolum 1: Prompt Zincirleme

## Prompt Zincirleme Kalibina Genel Bakis

Prompt zincirleme, bazen Pipeline kalıbı olarak da adlandirilan bu yaklasim, buyuk dil modellerinden (LLM) yararlanirken karmasik gorevlerin ele alinmasinda guclu bir paradigmayi temsil eder. Bir LLM'den karmasik bir problemi tek bir monolitik adimda cozmesini beklemek yerine, prompt zincirleme bol-ve-yonet stratejisini savunur. Temel fikir, baslangictaki zorlayici problemi daha kucuk, daha yonetilebilir alt problemlerden olusan bir diziye ayirmaktir. Her alt problem, ozel olarak tasarlanmis bir prompt araciligiyla bireysel olarak ele alinir ve bir prompt'tan uretilen cikti, zincirdeki sonraki prompt'a girdi olarak stratejik bir sekilde beslenir.

Bu sirali isleme teknigi, dogasi geregi LLM'lerle etkilesime modulerlik ve netlik kazandirir. Karmasik bir gorevi parcalara ayirarak, her bir adimi anlamak ve hata ayiklamak kolaylasir, bu da genel sureci daha saglam ve yorumlanabilir kilar. Zincirdeki her adim, daha buyuk problemin belirli bir yonune odaklanmak uzere titizlikle tasarlanabilir ve optimize edilebilir, bu da daha dogru ve odaklanmis ciktilara yol acar.

Bir adimin ciktisinin sonraki adimin girdisi olarak kullanilmasi kritik oneme sahiptir. Bu bilgi aktarimi, onceki islemlerin baglaminin ve sonuclarinin sonraki islemeyi yonlendirdigi bir baglanti zinciri olusturur; bu nedenle bu isim verilmistir. Bu yaklasim, LLM'nin onceki calismasi uzerine insa etmesine, anlayisini rafine etmesine ve istenen cozume dogru kademeli olarak ilerlemesine olanak tanir.

Ayrica, prompt zincirleme sadece problemleri parcalamakla ilgili degildir; ayni zamanda dis bilgi ve araclarin entegrasyonunu da mumkun kilar. Her adimda, LLM'ye harici sistemler, API'ler veya veritabanlariyla etkilesim kurma talimati verilebilir, bu da bilgi ve yeteneklerini dahili egitim verilerinin otesine tasir. Bu yetenek, LLM'lerin potansiyelini onemli olcude genisleterek, onlarin yalnizca izole modeller olarak degil, daha genis ve daha akilli sistemlerin ayrilmaz bilesenleri olarak islevini yerine getirmesine olanak tanir.

Prompt zincirlemenin onemi basit problem cozmekten oteye uzanir. Gelismis yapay zeka agent'lari olusturmak icin temel bir teknik gorevi gorur. Bu agent'lar, dinamik ortamlarda otonom olarak plan yapmak, akil yurutme (Reasoning) gerceklestirmek ve harekete gecmek icin prompt zincirlerini kullanabilir. Prompt'larin siralanmasini stratejik olarak yapilandirarak, bir agent cok adimli akil yurutme, planlama (Planning) ve karar verme gerektiren gorevlerle mesgul olabilir. Bu tur agent workflow'lari, insan dusunce sureclerini daha yakindan taklit ederek, karmasik alanlar ve sistemlerle daha dogal ve etkili etkilesimler saglar.

**Tekli prompt'larin sinirliliklari:** Cok yonlu gorevler icin, bir LLM'ye tek bir karmasik prompt kullanmak verimsiz olabilir; model, kisitlamalar ve talimatlarla bocalar ve potansiyel olarak talimat ihmaline (prompt'un bazi kisimlarinin gozden kacirilmasi), baglamsal sapmaya (modelin baslangic baglamini kaybetmesi), hata yayilimina (erken hatalarin buyumesi), daha uzun context window gerektiren prompt'lara (modelin yanit vermek icin yeterli bilgi alamamasi) ve hallucination'a (bilissel yukun yanlis bilgi uretme olasiligini artirmasi) yol acabilir. Ornegin, bir pazar arastirma raporunu analiz etmeyi, bulgulari ozetlemeyi, veri noktalariyla trendleri belirlemeyi ve bir e-posta taslagi hazirlama istegi, modelin ozetlemeyi iyi yapabilmesine ragmen veri cikarma veya e-posta taslagi hazirlama konusunda basarisiz olma riskini tasir.

**Sirali Ayristirma Yoluyla Gelistirilmis Guvenilirlik:** Prompt zincirleme, karmasik gorevi odaklanmis, sirali bir is akisina ayirarak bu zorluklari giderir ve guvenilirligi ile kontrolu onemli olcude arttirir. Yukaridaki ornek goz onune alindiginda, bir pipeline veya zincirli yaklasim su sekilde tanimlanabilir:

1. Baslangic Prompt'u (Ozetleme): "Asagidaki pazar arastirma raporunun temel bulgularini ozetleyin: \[metin\]." Modelin tek odak noktasi ozetleme olup, bu baslangic adiminin dogrulugunu arttirir.
2. Ikinci Prompt (Trend Belirleme): "Ozeti kullanarak, ortaya cikan ilk uc trendi belirleyin ve her trendi destekleyen belirli veri noktalarini cikartin: \[1. adimin ciktisi\]." Bu prompt artik daha kisitli olup dogrudan dogrulanmis bir cikti uzerine insa edilmektedir.
3. Ucuncu Prompt (E-posta Yazimi): "Pazarlama ekibine, asagidaki trendleri ve destekleyici verilerini ozetleyen kisa bir e-posta taslagi hazirlayin: \[2. adimin ciktisi\]."

Bu ayristirma, surecin daha ayrintili kontrol edilmesine olanak tanir. Her adim daha basit ve daha az belirsizdir, bu da model uzerindeki bilissel yuku azaltir ve daha dogru ve guvenilir bir nihai ciktiya yol acar. Bu modulerlik, her fonksiyonun sonucunu bir sonrakine aktarmadan once belirli bir islem gerceklestirdigi hesaplamali bir pipeline'a benzerdir. Her belirli gorev icin dogru bir yanit saglamak amaciyla, modele her asamada farkli bir rol atanabilir. Ornegin, verilen senaryoda baslangic prompt'u "Pazar Analisti", sonraki prompt "Ticaret Analisti" ve ucuncu prompt "Uzman Dokumantasyon Yazari" olarak atanabilir.

**Yapilandirilmis Ciktinin Rolu:** Bir prompt zincirinin guvenilirligi, adimlar arasinda aktarilan verilerin butunlugune buyuk olcude baglidir. Bir prompt'un ciktisi belirsiz veya kotu bicimlendirilmis ise, sonraki prompt hatali girdi nedeniyle basarisiz olabilir. Bunu onlemek icin, JSON veya XML gibi yapilandirilmis bir cikti formati belirlemek kritik oneme sahiptir.

Ornegin, trend belirleme adiminin ciktisi bir JSON nesnesi olarak bicimlendirillebilir:

```json
{  "trends": [
        {
            "trend_name": "AI-Powered Personalization",
            "supporting_data": "73% of consumers prefer to do business with brands that use personal information to make their shopping experiences more relevant."
        },
        {
            "trend_name": "Sustainable and Ethical Brands",
            "supporting_data": "Sales of products with ESG-related claims grew 28% over the last five years, compared to 20% for products without."
        }
    ]
}
```

Bu yapilandirilmis format, verilerin makine tarafindan okunabilir olmasini ve bir sonraki prompt'a belirsizlik olmadan hassas bir sekilde ayristiriip eklenmesini saglar. Bu uygulama, dogal dilin yorumlanmasindan kaynaklanan hatalari en aza indirir ve saglam, cok adimli LLM tabanli sistemler olusturmanin temel bir bilisenidir.

## Pratik Uygulamalar ve Kullanim Alanlari

Prompt zincirleme, agentic sistemler olustururken genis bir yelpazede uygulanabilen cok yonlu bir kaliptir. Temel faydasi, karmasik problemleri sirali ve yonetilebilir adimlara ayirmaktir. Iste cesitli pratik uygulamalar ve kullanim alanlari:

### 1. Bilgi Isleme Is Akislari

Bircok gorev, ham bilginin birden fazla donusumden gecirilmesini icerir. Ornegin, bir dokumani ozetleme, temel varliklari cikarma ve ardindan bu varliklari bir veritabanini sorgulamak veya bir rapor olusturmak icin kullanma. Bir prompt zinciri su sekilde gorunebilir:

* Prompt 1: Verilen bir URL veya dokumandan metin icerigini cikarma.
* Prompt 2: Temizlenmis metni ozetleme.
* Prompt 3: Ozetten veya orijinal metinden belirli varliklari (ornegin isimler, tarihler, konumlar) cikarma.
* Prompt 4: Varliklari dahili bir bilgi tabaninda aramak icin kullanma.
* Prompt 5: Ozeti, varliklari ve arama sonuclarini birlestiren nihai bir rapor olusturma.

Bu metodoloji, otomatik icerik analizi, yapay zeka destekli arastirma asistanlarinin gelistirilmesi ve karmasik rapor olusturma gibi alanlarda uygulanmaktadir.

### 2. Karmasik Sorgu Yanitlama

Birden fazla akil yurutme veya bilgi erisimi (Knowledge Retrieval) adimi gerektiren karmasik sorulari yanitlamak, temel bir kullanim alanidir. Ornegin, "1929 borsa cokusuunun temel nedenleri neydi ve hukumet politikasi nasil yanit verdi?"

* Prompt 1: Kullanicinin sorgusundaki temel alt sorulari belirleme (cokusun nedenleri, hukumet yaniti).
* Prompt 2: 1929 cokusunun nedenleri hakkinda ozellikle bilgi arastirma veya erisim.
* Prompt 3: Hukumetin 1929 borsa cokusune politika yanitini ozellikle arastirma veya erisim.
* Prompt 4: 2. ve 3. adimlardan elde edilen bilgileri, orijinal sorguya tutarli bir yanit olusturmak icin sentezleme.

Bu sirali isleme metodolojisi, cok adimli cikarim ve bilgi sentezi yapabilen yapay zeka sistemleri gelistirmenin ayrilmaz bir parcasidir. Bu tur sistemler, bir sorgunun tek bir veri noktasindan yanilanamadigi, bunun yerine bir dizi mantiksal adim veya farkli kaynaklardan gelen bilgilerin entegrasyonunu gerektirdigi durumlarda ihtiyac duyulur.

Ornegin, belirli bir konu hakkinda kapsamli bir rapor olusturmak uzere tasarlanmis otomatik bir arastirma agent'i, hibrit bir hesaplama is akisi yurutur. Baslangicta, sistem cok sayida ilgili makaleyi alir. Her makaleden temel bilgilerin cikarilmasi gorevi, her kaynak icin es zamanli olarak gerceklestirilebilir. Bu asama, bagimsiz alt gorevlerin verimlilik en ust duzeye cikarmak icin es zamanli olarak calistirildigi paralel isleme icin cok uygundur.

Ancak, bireysel cikarimlar tamamlandiginda, surec dogasi geregi sirali hale gelir. Sistem once cikarilan verileri harmanlamali, ardindan tutarli bir taslak halinde sentezlemeli ve son olarak bu taslagi nihai bir rapor olusturmak icin gozden gecirip rafine etmelidir. Bu sonraki asamalarin her biri, bir oncekinin basariyla tamamlanmasina mantiksal olarak baglidir. Prompt zincirleme burada uygulanir: harmanlanmis veriler sentez prompt'u icin girdi gorevi gorur ve ortaya cikan sentezlenmis metin, nihai gozden gecirme prompt'u icin girdi olur. Bu nedenle, karmasik islemler genellikle bagimsiz veri toplama icin paralel islemeyi, sentez ve iyilestirmenin bagimli adimlari icin prompt zincirlemeyi birlestirir.

### 3. Veri Cikarma ve Donusturme

Yapilandirilmamis metnin yapilandirilmis bir formata donusturulmesi, genellikle ciktinin dogrulugunu ve tamlilğini iyilestirmek icin sirali degisiklikler gerektiren yinelemeli bir surecle gerceklestirilir.

* Prompt 1: Bir fatura dokumanindan belirli alanlari (ornegin ad, adres, tutar) cikarmayi deneme.
* Isleme: Tum gerekli alanlarin cikarilip cikarilmadigini ve format gereksinimlerini karsilayip karsilamadigini kontrol etme.
* Prompt 2 (Kosullu): Alanlar eksik veya hatali bicimlenmisse, modelden eksik/hatali bilgiyi ozellikle bulmesini isteyen, basarisiz denemeden baglam saglayan yeni bir prompt olusturma.
* Isleme: Sonuclari yeniden dogrulama. Gerekirse tekrarlama.
* Cikti: Cikarilan, dogrulanmis yapilandirilmis verileri saglama.

Bu sirali isleme metodolojisi, ozellikle formlar, faturalar veya e-postalar gibi yapilandirilmamis kaynaklardan veri cikarma ve analize uygulanabilir. Ornegin, bir PDF formu isleme gibi karmasik Optik Karakter Tanima (OCR) problemlerini cozmek, parcalanmis, cok adimli bir yaklasimayla daha etkili bir sekilde ele alinir.

Baslangicta, dokuman goruntusunden birincil metin cikarimini gerceklestirmek icin buyuk bir dil modeli kullanilir. Bunun ardindan model, ham ciktiyi normallestirir; bu adimda ornegin "bin elli" gibi sayisal metni, sayisal karsiligi olan 1050'ye donusturebilir. LLM'ler icin onemli bir zorluk, hassas matematiksel hesaplamalari gerceklestirmektir. Bu nedenle, sonraki bir adimda sistem, gerekli aritmetik islemleri harici bir hesap makinesi aracina devredebilir. LLM gerekli hesaplamayi belirler, normallestirilmis sayilari araca besler ve ardindan hassas sonucu dahil eder. Bu zincirli metin cikarma, veri normallestirme ve harici arac kullanimi dizisi, tek bir LLM sorgusundan guvenilir sekilde elde edilmesi genellikle zor olan nihai, dogru bir sonuca ulasir.

### 4. Icerik Olusturma Is Akislari

Karmasik icerigin yazilmasi, ilk fikirlestirme, yapisal ana hat olusturma, taslak hazirlama ve sonraki revizyon dahil olmak uzere farkli asamalara ayrilan bir prosedur gorevidir.

* Prompt 1: Kullanicinin genel ilgi alanina dayali 5 konu fikri olusturma.
* Isleme: Kullanicinin bir fikir secmesine izin verme veya otomatik olarak en iyisini secme.
* Prompt 2: Secilen konuya dayanarak ayrintili bir ana hat olusturma.
* Prompt 3: Ana hattaki ilk maddeye dayali bir taslak bolum yazma.
* Prompt 4: Ana hattaki ikinci maddeye dayali bir taslak bolum yazma, baglam icin onceki bolumu saglama. Tum ana hat maddeleri icin devam etme.
* Prompt 5: Tam taslagi tutarlilik, ton ve dil bilgisi acisindan gozden gecirme ve iyilestirme.

Bu metodoloji, yaratici anlatilarin, teknik dokumantasyonun ve diger yapilandirilmis metinsel icerik turlerinin otomatik kompozisyonu dahil olmak uzere bir dizi dogal dil uretim gorevi icin kullanilir.

### 5. Durumlu Konusma Agent'lari

Kapsamli durum yonetimi mimarileri sirali baglantidan daha karmasik yontemler kullansa da, prompt zincirleme, konusma surekliligini korumak icin temel bir mekanizma saglar. Bu teknik, diyalog dizisindeki onceki etkilesilmerden gelen bilgileri veya cikarilan varliklari sistematik olarak iceren yeni bir prompt olarak her konusma turunu olusturarak baglami korur.

* Prompt 1: Kullanici Ifadesi 1'i isle, niyet ve temel varliklari belirle.
* Isleme: Konusma durumunu niyet ve varliklarla guncelle.
* Prompt 2: Mevcut duruma dayanarak bir yanit olustur ve/veya gereken sonraki bilgi parcasini belirle.
* Sonraki turlar icin tekrarla; her yeni kullanici ifadesi, biriken konusma gecmisinden (durum) yararlanan bir zinciri baslatir.

Bu ilke, konusma agent'larinin gelistirilmesinde temeldir ve onlarin uzun, cok turlu diyaloglarda baglam ve tutarliligi korumalarini saglar. Konusma gecmisini koruyarak, sistem daha once degisilen bilgilere bagli kullanici girdilerini anlayabilir ve uygun sekilde yanit verebilir.

### 6. Kod Olusturma ve Iyilestirme

Islevsel kodun olusturulmasi, genellikle bir problemin kademeli olarak yurutulen bir dizi ayrik mantiksal isleme ayristrilmasini gerektiren cok asamali bir surecidir.

* Prompt 1: Kullanicinin bir kod fonksiyonu istegini anlama. Sahte kod veya ana hat olusturma.
* Prompt 2: Ana hata dayali ilk kod taslagini yazma.
* Prompt 3: Koddaki potansiyel hatalari veya iyilestirme alanlarini belirleme (belki bir statik analiz araci veya baska bir LLM cagrisi kullanarak).
* Prompt 4: Belirlenen sorunlara dayanarak kodu yeniden yazma veya iyilestirme.
* Prompt 5: Dokumantasyon veya test senaryolari ekleme.

Yapay zeka destekli yazilim gelistirme gibi uygulamalarda, prompt zincirlemenin faydasi karmasik kodlama gorevlerini bir dizi yonetilebilir alt probleme ayirma kapasitesinden kaynaklanir. Bu moduler yapi, her adimda buyuk dil modeli icin operasyonel karmasikligi azaltir. Kritik olarak, bu yaklasim ayni zamanda model cagrılari arasina deterministik mantik eklenebilmesine olanak tanir; is akisi icerisinde ara veri isleme, cikti dogrulama ve kosullu dallanma mumkun kilinir. Bu yontemle, aksi halde guvenilmez veya eksik sonuclara yol acabilecek tek bir cok yonlu istek, bir alt yurutme cercevesi tarafindan yonetilen yapilandirilmis bir islem dizisine donusturulur.

### 7. Cok Modlu ve Cok Adimli Akil Yurutme

Farkli modalitelere sahip veri setlerinin analizi, problemin daha kucuk, prompt tabanli gorevlere ayristrilmasini gerektirir. Ornegin, gomulu metin, belirli metin segmentlerini vurgulayan etiketler ve her etiketi aciklayan tablo verileri iceren bir resmin yorumlanmasi boyle bir yaklasimi gerektirir.

* Prompt 1: Kullanicinin gorsel isteginden metni cikarma ve anlama.
* Prompt 2: Cikarilan gorsel metnini ilgili etiketlerle eslestirme.
* Prompt 3: Gereken ciktiyi belirlemek icin bir tablo kullanarak toplanan bilgileri yorumlama.

# Uygulamali Kod Ornegi

Prompt zincirlemenin uygulanmasi, bir betik icerisindeki dogrudan, sirali fonksiyon cagrilarindan, kontrol akisi, durum ve bilesen entegrasyonunu yonetmek icin tasarlanmis ozelesmis cercevelerin kullanimina kadar uzanir. LangChain, LangGraph, Crew AI ve Google Agent Development Kit (ADK) gibi cerceveler, bu cok adimli surecleri olusturmak ve yurutmek icin yapilandirilmis ortamlar sunar; bu ozellikle karmasik mimariler icin avantajlidir.

Gosterim amacliyla, LangChain ve LangGraph, temel API'leri acikca zincir ve islem grafiklerini olusturmak icin tasarlandigi icin uygun secimlerdir. LangChain, dogrusal diziler icin temel soyutlamalar saglarken, LangGraph bu yetenekleri daha gelismis agentic davranislari uygulamak icin gerekli olan durum bilgisine sahip ve dongusal hesaplamalari destekleyecek sekilde genisletir. Bu ornek temel bir dogrusal diziye odaklanacaktir.

Asagidaki kod, bir veri isleme pipeline'i olarak islev goren iki adimli bir prompt zinciri uygular. Ilk asama, yapilandirilmamis metni ayristirmak ve belirli bilgileri cikarmak icin tasarlanmistir. Sonraki asama bu cikarilan ciktiyi alir ve yapilandirilmis bir veri formatina donusturur.

Bu proseduru tekrarlamak icin, oncelikle gerekli kutuphanelerin kurulmasi gerekmektedir. Bu, asagidaki komut kullanilarak gerceklestirilebilir:

```bash
pip install langchain langchain-community langchain-openai langgraph
```

langchain-openai'nin farkli bir model saglayicisi icin uygun paket ile degistirilebilecegini unutmayin. Ardindan, yurume ortaminin secilen dil modeli saglayicisi (OpenAI, Google Gemini veya Anthropic gibi) icin gerekli API kimlik bilgileriyle yapilandirilmasi gerekmektedir.

```python
import os
from langchain_openai import ChatOpenAI
from langchain_core.prompts import ChatPromptTemplate
from langchain_core.output_parsers import StrOutputParser

# For better security, load environment variables from a .env file
# from dotenv import load_dotenv
# load_dotenv()
# Make sure your OPENAI_API_KEY is set in the .env file

# Initialize the Language Model (using ChatOpenAI is recommended)

llm = ChatOpenAI(temperature=0)

# --- Prompt 1: Extract Information ---

prompt_extract = ChatPromptTemplate.from_template(
    "Extract the technical specifications from the following text:\n\n{text_input}"
)

# --- Prompt 2: Transform to JSON ---

prompt_transform = ChatPromptTemplate.from_template(
    "Transform the following specifications into a JSON object with 'cpu', 'memory', and 'storage' as keys:\n\n{specifications}"
)

# --- Build the Chain using LCEL ---
# The StrOutputParser() converts the LLM's message output to a simple string.
extraction_chain = prompt_extract | llm | StrOutputParser()

# The full chain passes the output of the extraction chain into the 'specifications'
# variable for the transformation prompt.
full_chain = (
    {"specifications": extraction_chain}
        |
    prompt_transform
        |
    llm
        |
    StrOutputParser()
)

# --- Run the Chain ---

input_text = "The new laptop model features a 3.5 GHz octa-core processor, 16GB of RAM, and a 1TB NVMe SSD."

# Execute the chain with the input text dictionary.
final_result = full_chain.invoke({"text_input": input_text})
print("\n--- Final JSON Output ---")
print(final_result)
```

Bu Python kodu, LangChain kutuphanesini kullanarak metni nasil isleyecegini gostermektedir. Iki ayri prompt kullanir: biri bir girdi dizesinden teknik ozellikleri cikarmak, digeri ise bu ozellikleri bir JSON nesnesine bicimlemek icin. Dil modeli etkilesimlerinde ChatOpenAI modeli kullanilir ve StrOutputParser, ciktinin kullanilabilir bir dize formatinda olmasini saglar. LangChain Expression Language (LCEL), bu prompt'lari ve dil modelini zarif bir sekilde zincirlemek icin kullanilir. Ilk zincir olan `extraction_chain`, ozellikleri cikarir. `full_chain` daha sonra cikarma isleminin ciktisini alir ve donusum prompt'u icin girdi olarak kullanir. Bir dizustu bilgisayari tanimlayan ornek bir girdi metni saglanir. `full_chain`, bu metinle cagrilarak her iki adim boyunca islenir. Cikarilan ve bicimlendirilmis ozellikleri iceren nihai sonuc, bir JSON dizesi olarak yazdirilir.

## Baglam Muhendisligi ve Prompt Muhendisligi

Baglam Muhendisligi (bkz. Sekil 1), bir yapay zeka modeline token uretiminden once eksiksiz bir bilgisel ortam tasarlama, olusturma ve sunma disiplinidir. Bu metodoloji, bir modelin cikti kalitesinin modelin mimarisine daha az, saglanan baglamin zenginligine daha fazla bagli oldugunu ileri surer.

![Context Engineering](../assets/context_engineering.png)

Sekil 1: Baglam Muhendisligi, bir yapay zeka icin zengin, kapsamli bir bilgisel ortam olusturma disiplinidir; bu baglamin kalitesi, gelismis Agentic performansi mumkun kilan temel bir faktordur.

Geleneksel prompt muhendisliginden onemli bir evrimi temsil eder; prompt muhendisligi oncelikle kullanicinin ani sorgusunun ifadesini optimize etmeye odaklanir. Baglam Muhendisligi bu kapsami, **sistem prompt'u** gibi cesitli bilgi katmanlarini icermek uzere genisletir. Sistem prompt'u, yapay zekanin operasyonel parametrelerini tanimlayan temel bir talimat setidir -- ornegin, *"Sen bir teknik yazarsin; tonun resmi ve hassas olmalidir."* Baglam ayrica harici verilerle zenginlestirilir. Bu, yapay zekanin yanitini bilgilendirmek icin bir bilgi tabanindan aktif olarak bilgi getirdigi alinan dokumanlari icerir, ornegin bir proje icin teknik ozelliklerin cekilmesi gibi. Ayrica, yapay zekanin gercek zamanli veri elde etmek icin harici bir API kullandigi arac ciktilarini da kapsar, ornegin bir kullanicinin musaitligini belirlemek icin bir takvim sorgulama gibi. Bu acik veriler, kullanici kimligi, etkilesim gecmisi ve cevre durumu gibi kritik ortuk verilerle birlestirilir. Temel ilke, gelismis modellerin bile operasyonel ortamin sinirli veya kotu olusturulmus bir gorunumuyle saglandiginda dusuk performans gosterdikleridir.

Bu uygulama, bu nedenle gorevi sadece bir soruyu yanitmaktan agent icin kapsamli bir operasyonel tablo olusturmaya yeniden cerceveler. Ornegin, baglam muhendisligi uygulanmis bir agent, yalnizca bir sorguya yanit vermekle kalmaz, once kullanicinin takvim musaitligini (bir arac ciktisi), bir e-posta alicisiyla profesyonel iliskiyi (ortuk veri) ve onceki toplantilardaki notlari (alinan dokumanlar) entegre eder. Bu, modelin son derece ilgili, kisisellestilimis ve pragmatik olarak faydali ciktilar uretmesine olanak tanir. "Muhendislik" bileseni, calisma zamaninda bu verileri getirmek ve donusturmek icin saglam pipeline'lar olusturmayi ve baglam kalitesini surekli iyilestirmek icin geri bildirim donguleri kurmmayi icerir.

Bunu uygulamak icin, iyilestirme surecini olcekte otomatiklestirmek amaciyla ozelesmis ayarlama sistemleri kullanilabilir. Ornegin, Google'in Vertex AI prompt optimizer gibi araclar, bir dizi ornek girdi ve onceden tanimlanmis degerlendirme metriklerine karsi yanitlari sistematik olarak degerlendirerek model performansini artirabilir. Bu yaklasim, kapsamli manuel yeniden yazma gerektirmeden prompt'lari ve sistem talimatlarini farkli modeller arasinda uyarlamak icin etkilidir. Boyle bir optimizer'a ornek prompt'lar, sistem talimatlari ve bir sablon saglayarak, baglamsal girdileri programatik olarak rafine edebilir ve gelismis Baglam Muhendisligi icin gereken geri bildirim dongulerini uygulamak icin yapilandirilmis bir yontem sunar.

Bu yapilandirilmis yaklasim, ilkel bir yapay zeka aracini daha gelismis ve baglama duyarli bir sistemden ayiran seydir. Baglamin kendisini birincil bir bilesen olarak ele alir ve agent'in ne bildigi, ne zaman bildigi ve bu bilgiyi nasil kullandigi konusuna kritik onem atfeder. Uygulama, modelin kullanicinin niyeti, gecmisi ve mevcut ortami hakkinda kapsamli bir anlayisa sahip olmasini saglar. Sonuc olarak, Baglam Muhendisligi, durumsuz sohbet robotlarini son derece yetenekli, duruma duyarli sistemlere donusturmek icin kritik bir metodolojidir.

## Bir Bakista

**Ne:** Karmasik gorevler, tek bir prompt icerisinde ele alindiginda genellikle LLM'leri bunaltir ve onemli performans sorunlarina yol acar. Model uzerindeki bilissel yuk, talimatlari gozden kacirma, baglami kaybetme ve yanlis bilgi uretme gibi hatalarin olasiligini artirir. Monolitik bir prompt, birden fazla kisitlamayi ve sirali akil yurutme adimlarini etkili bir sekilde yonetemez. Bu durum, LLM'nin cok yonlu istegin tum yonlerini ele almakta basarisiz olmasi nedeniyle guvenilmez ve yanlis ciktilara yol acar.

**Neden:** Prompt zincirleme, karmasik bir problemi daha kucuk, birbirine bagli alt gorevlerden olusan bir diziye ayirarak standart bir cozum sunar. Zincirdeki her adim, belirli bir islemi gerceklestirmek icin odaklanmis bir prompt kullanir ve guvenilirlik ile kontrolu onemli olcude arttirir. Bir prompt'un ciktisi bir sonraki prompt'a girdi olarak aktarilir, nihai cozume dogru kademeli olarak ilerleyen mantiksal bir is akisi olusturur. Bu moduler, bol-ve-yonet stratejisi, sureci daha yonetilebilir, hata ayiklamasi daha kolay hale getirir ve adimlar arasinda harici araclarin veya yapilandirilmis veri formatlarinin entegrasyonuna olanak tanir. Bu kalip, karmasik is akislarini planlayabilen, akil yurutebilen ve yurutebilen gelismis, cok adimli Agentic sistemler gelistirmek icin temeldir.

**Temel kural:** Bu kalibi, bir gorev tek bir prompt icin cok karmasik oldugunda, birden fazla farkli isleme asamasi icerdiginde, adimlar arasinda harici araclarla etkilesim gerektirdiginde veya cok adimli akil yurutme yapmasi ve durumu korumasi gereken Agentic sistemler olustururken kullanin.

**Gorsel ozet:**

![Prompt Chaining Pattern](../assets/Prompt_Chaining_Pattern.png)

Sekil 2: Prompt Zincirleme Kalibi: Agent'lar kullanicidan bir dizi prompt alir ve her agent'in ciktisi zincirdeki bir sonraki agent icin girdi gorevi gorur.

## Temel Cikarimlar

Iste bazi temel cikarimlar:

* Prompt Zincirleme, karmasik gorevleri daha kucuk, odaklanmis adimlardan olusan bir diziye ayirir. Bu bazen Pipeline kalibi olarak da bilinir.
* Bir zincirdeki her adim, onceki adimin ciktisini girdi olarak kullanarak bir LLM cagrisi veya isleme mantigi icerir.
* Bu kalip, dil modelleriyle karmasik etkilesimlerin guvenilirligini ve yonetilebilirligini arttirir.
* LangChain/LangGraph ve Google ADK gibi cerceveler, bu cok adimli dizileri tanimlamak, yonetmek ve yurutmek icin saglam araclar sunar.

## Sonuc

Karmasik problemleri daha basit, daha yonetilebilir alt gorevlerden olusan bir diziye ayristirarak, prompt zincirleme buyuk dil modellerine rehberlik etmek icin saglam bir cerceve sunar. Bu "bol-ve-yonet" stratejisi, modeli her seferinde tek bir belirli isleme odaklayarak ciktinin guvenilirligini ve kontrolunu onemli olcude arttirir. Temel bir kalip olarak, cok adimli akil yurutme, arac entegrasyonu ve durum yonetimi yapabilen gelismis yapay zeka agent'larinin gelistirilmesini mumkun kilar. Sonuc olarak, prompt zincirlemeyi ustalasmak, tek bir prompt'un yeteneklerinin cok otesinde karmasik is akislarini yurutebilen saglam, baglama duyarli sistemler olusturmak icin kritik oneme sahiptir.

## Kaynaklar

1. LangChain Documentation on LCEL: [https://python.langchain.com/v0.2/docs/core_modules/expression_language/](https://python.langchain.com/v0.2/docs/core_modules/expression_language/)
2. LangGraph Documentation: [https://langchain-ai.github.io/langgraph/](https://langchain-ai.github.io/langgraph/)
3. Prompt Engineering Guide \- Chaining Prompts: [https://www.promptingguide.ai/techniques/chaining](https://www.promptingguide.ai/techniques/chaining)
4. OpenAI API Documentation (General Prompting Concepts): [https://platform.openai.com/docs/guides/gpt/prompting](https://platform.openai.com/docs/guides/gpt/prompting)
5. Crew AI Documentation (Tasks and Processes): [https://docs.crewai.com/](https://docs.crewai.com/)
6. Google AI for Developers (Prompting Guides): [https://cloud.google.com/discover/what-is-prompt-engineering?hl=en](https://cloud.google.com/discover/what-is-prompt-engineering?hl=en)
7. Vertex Prompt Optimizer [https://cloud.google.com/vertex-ai/generative-ai/docs/learn/prompts/prompt-optimizer](https://cloud.google.com/vertex-ai/generative-ai/docs/learn/prompts/prompt-optimizer)
