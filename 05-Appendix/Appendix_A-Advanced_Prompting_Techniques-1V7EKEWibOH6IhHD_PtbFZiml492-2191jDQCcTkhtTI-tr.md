# Ek A: Gelismis Prompt Teknikleri

## Prompt'a Giris

Prompt, dil modelleriyle etkilesimin temel arayuzu olup modeli istenen ciktiyi uretmeye yonlendirmek icin girdilerin olusturulma surecidir. Bu surecte isteklerin yapilandirilmasi, ilgili baglamın salanmasi, cikti formatinin belirlenmesi ve beklenen yanit turlerinin gosterilmesi yer alir. Iyi tasarlanmis prompt'lar, dil modellerinin potansiyelini en ust duzeye cikartarak dogru, ilgili ve yaratici yanitlar alinmasini saglar. Buna karsilik, kotukullanmis tasarlanmis prompt'lar belirsiz, ilgisiz veya hatali ciktilara yol acabilir.

Prompt muhendisliginin amaci, dil modellerinden tutarli sekilde yuksek kaliteli yanitlar elde etmektir. Bu, modellerin yeteneklerini ve sinirliliklerini anlamayi ve hedeflenen amaclari etkili bir sekilde iletmeyi gerektirir. Yapay zeka ile iletisim uzmanligi gelistirmeyi, yani ona en iyi sekilde nasil talimat verilecegini ogrenmeyi icerir.

Bu ek, temel etkilesim yontemlerinin otesine gecen cesitli prompt tekniklerini ayrintili olarak ele almaktadir. Karmasik isteklerin yapilandirilmasi, modelin akil yurutme (Reasoning) yeteneklerinin gelistirilmesi, cikti formatlarinin kontrol edilmesi ve harici bilgilerin entegrasyonu icin metodolojileri incelemektedir. Bu teknikler, basit sohbet robotlarindan karmasik multi-agent sistemlere kadar genis bir uygulama yelpazesinde kullanilabilir ve agentic uygulamalarin performansini ve guvenilirligini artirabilir.

Agentic kaliplar, yani akilli sistemler olusturmak icin kullanilan mimari yapilar, ana bollumlerde ayrintili olarak ele alinmaktadir. Bu kaliplar, agent'larin nasil plan yaptigini, arac kullandigini, bellegi yonettigini ve is birligi (Collaboration) yaptigini tanimlar. Bu agentic sistemlerin etkinligi, dil modelleriyle anlamli bir sekilde etkilesim kurabilme yeteneklerine baglidir.

## Temel Prompt Ilkeleri

Dil Modellerinde Etkili Prompt Icin Temel Ilkeler:

Etkili prompt, dil modelleriyle iletisimi yonlendiren temel ilkelere dayanir; bu ilkeler cesitli modeller ve gorev karmasikliklari genelinde uygulanabilir. Bu ilkelere hakim olmak, tutarli bir sekilde faydali ve dogru yanitlar uretmek icin gereklidir.

**Netlik ve Ozgulluk**: Talimatlar net ve kesin olmalidir. Dil modelleri oruntuleri yorumlar; birden fazla yorum yanlis yanitlara yol acabilir. Gorevi, istenen cikti formatini ve tum sinirlamalari veya gereksinimleri tanimlayin. Belirsiz dil veya varsayimlardan kacinin. Yetersiz prompt'lar belirsiz ve yanlis yanitlara yol acar ve anlamli cikti elde etmeyi zorlastirir.

**Kisa ve Oz**: Ozgulluk cok onemli olsa da, kisa ve oz olmaktan odun verilmemelidir. Talimatlar dogrudan olmalidir. Gereksiz ifadeler veya karmasik cumle yapilari modeli sasirtabilir veya ana talimati gizleyebilir. Prompt'lar basit olmalidir; kullanici icin kafa karistirici olan sey buyuk olasilikla model icin de kafa karistiricidir. Karmasik dil ve gereksiz bilgilerden kacinin. Istenen eylemi acikca belirlemek icin dogrudan ifadeler ve etken fiiller kullanin. Etkili fiiller sunlardir: Act, Analyze, Categorize, Classify, Contrast, Compare, Create, Describe, Define, Evaluate, Extract, Find, Generate, Identify, List, Measure, Organize, Parse, Pick, Predict, Provide, Rank, Recommend, Return, Retrieve, Rewrite, Select, Show, Sort, Summarize, Translate, Write.

**Fiil Kullanimi:** Fiil secimi onemli bir prompt aracidir. Eylem fiilleri beklenen islemi belirtir. "Bu metni ozetlemeyi dusun" yerine, "Asagidaki metni ozetle" gibi dogrudan bir talimat daha etkilidir. Kesin fiiller, modeli o belirli gorev icin ilgili egitim verilerini ve sureclerini etkinlestirmeye yonlendirir.

**Kisitlamalar Yerine Talimatlar:** Pozitif talimatlar genellikle negatif kisitlamalardan daha etkilidir. Istenen eylemi belirtmek, yapilmamasi gerekeni belirtmekten tercih edilir. Kisitlamalarin guvenlik veya siki bicimlendirme icin yeri olsa da, asiri bagimlililk modelin hedeften ziyade kacinmaya odaklanmasina neden olabilir. Prompt'lari modeli dogrudan yonlendirecek sekilde cerceveleyin. Pozitif talimatlar insan rehberligi tercihlerine uyar ve kafa karisikligini azaltir.

**Deney ve Yineleme:** Prompt muhendisligi yinelemeli bir surecdir. En etkili prompt'u belirlemek birden fazla deneme gerektirir. Bir taslakla baslain, test edin, ciktiyi analiz edin, eksiklikleri belirleyin ve prompt'u iyilestirin. Model varyasyonlari, yapilandirmalar (sicaklik veya top-p gibi) ve kucuk ifade degisiklikleri farkli sonuclar verebilir. Denemelerin belgelenmesi, ogrenme ve gelistirme icin hayati oneme sahiptir. Istenen performansa ulasmak icin deney ve yineleme gereklidir.

Bu ilkeler, dil modelleriyle etkili iletisimin temelini olusturur. Netlik, kisalik, eylem fiilleri, pozitif talimatlar ve yinelemeyi on plana koyarak, daha gelismis prompt tekniklerini uygulamak icin saglam bir cerceve olusturulur.

## Temel Prompt Teknikleri

Temel ilkelere dayanarak, temel teknikler dil modellerine yanitlarini yonlendirmek icin degisen duzeylerde bilgi veya ornek saglar. Bu yontemler, prompt muhendisliginde bir baslangic asamasi olarak hizmet eder ve genis bir uygulama yelpazesi icin etkilidir.

### Zero-Shot Prompt

Zero-shot prompt, dil modeline istenen girdi-cikti cifti ornegi verilmeden bir talimat ve girdi verilerinin saglandigi en temel prompt bicimidir. Gorevi anlamak ve ilgili bir yanit uretmek tamamen modelin on egitimindeki bilgiye dayanir. Temelde, bir zero-shot prompt bir gorev aciklamasi ve sureci baslatmak icin baslangic metninden olusur.

* **Ne zaman kullanilmali:** Zero-shot prompt, modelin egitimi sirasinda buyuk olasilikla yogun bir sekilde karsilastigi gorevler icin genellikle yeterlidir; ornegin basit soru cevaplama, metin tamamlama veya basit metin ozetleme gibi. Ilk denemede kullanilacak en hizli yaklasimdir.
* **Ornek:**
  Translate the following English sentence to French: 'Hello, how are you?'

### One-Shot Prompt

One-shot prompt, gercek gorevi sunmadan once dil modeline girdinin ve karsilik gelen istenen ciktinin tek bir orneginin saglanmasini icerir. Bu yontem, modelin tekrarlamasi beklenen oruntularin gosterilmesi icin bir baslangic gosterimi islevi gorur. Amac, modeli verilen gorevi etkili bir sekilde yerine getirmek icin sablon olarak kullanabilecegi somut bir ornekle donatmaktir.

* **Ne zaman kullanilmali:** One-shot prompt, istenen cikti formati veya tarz belirli veya daha az yaygin oldugunda kullanislidir. Modele ogrenebilecegi somut bir ornek verir. Belirli bir yapi veya ton gerektiren gorevlerde zero-shot'a kiyasla performansi artirabilir.
* **Ornek:**
  Translate the following English sentences to Spanish:
  English: 'Thank you.'
  Spanish: 'Gracias.'

  English: 'Please.'
  Spanish:

### Few-Shot Prompt

Few-shot prompt, genellikle uc ila bes adet girdi-cikti cifti ornegi saglayarak one-shot prompt'u gelistirir. Bu, beklenen yanitlarin daha net bir oruntusunu gostermeyi ve modelin bu oruntuleri yeni girdiler icin tekrarlama olasiligini artirmayi amaclar. Bu yontem, modeli belirli bir cikti oruntusunu takip etmeye yonlendirmek icin birden fazla ornek saglar.

* **Ne zaman kullanilmali:** Few-shot prompt, istenen ciktinin belirli bir format, tarz veya nueansli varyasyonlara uymasini gerektiren gorevler icin ozellikle etkilidir. Siniflandirma, belirli semalara sahip veri cikarma veya belirli bir tarzda metin uretme gibi gorevler icin mukemmeldir; ozellikle zero-shot veya one-shot tutarli sonuclar vermediginde. En az uc ila bes ornek kullanmak genel bir kural olup gorev karmasikligi ve model token siniirlarina gore ayarlanmalidir.
* **Ornek Kalitesi ve Cesitliligi Onemi:** Few-shot prompt'un etkinligi buyuk olcude saglanan orneklerin kalitesine ve cesitliligine baglidir. Ornekler dogru, gorevi temsil edici ve modelin karsilasabilecegi potansiyel varyasyonlari veya uc durumlari kapsar nitelikte olmalidir. Yuksek kaliteli, iyi yazilmis ornekler cok onemlidir; kucuk bir hata bile modeli sasirtabilir ve istenmeyen ciktilara neden olabilir. Cesitli orneklerin dahil edilmesi, modelin gorulmemis girdilere daha iyi genelleme yapmasina yardimci olur.
* **Siniflandirma Orneklerinde Siniflarin Karistirilmasi:** Siniflandirma gorevleri icin (modelin girdiyi onceden tanimlanmis siniflara kategorize etmesi gerektiginde) few-shot prompt kullanirken, farkli siniflardan orneklerin sirasini karistirmak en iyi uygulamadir. Bu, modelin belirli ornek siralamasina asiri uyum saglamasini onler ve her sinifin temel ozelliklerini bagimsiz olarak tanimayi ogrenmesini saglar; bu da gorulmemis veriler uzerinde daha saglam ve genellenebilir bir performansa yol acar.
* **"Many-Shot" Ogrenmeye Evrilme:** Gemini gibi modern LLM'ler uzun baglam modellemesiyle guclenirken, "many-shot" ogrenimi kullanmada son derece etkili hale gelmektedir. Bu, karmasik gorevler icin optimal performansin artik dogrudan prompt icine cok daha fazla ornek -- hatta bazen yuzlerce -- dahil edilerek elde edilebilecegi anlamina gelir ve modelin daha karmasik oruntuleri ogrenmesine olanak tanir.
* **Ornek:**
  Classify the sentiment of the following movie reviews as POSITIVE, NEUTRAL, or NEGATIVE:

  Review: "The acting was superb and the story was engaging."
  Sentiment: POSITIVE

  Review: "It was okay, nothing special."
  Sentiment: NEUTRAL

  Review: "I found the plot confusing and the characters unlikable."
  Sentiment: NEGATIVE

  Review: "The visuals were stunning, but the dialogue was weak."
  Sentiment:

Zero-shot, one-shot ve few-shot prompt tekniklerinin ne zaman uygulanacagini anlamak ve ornekleri dusunceli bir sekilde hazirlayip duzenlemek, agentic sistemlerin etkinligini artirmak icin esasdir. Bu temel yontemler, cesitli prompt stratejileri icin temel olusturur.

## Prompt'larin Yapilandirilmasi

Ornek saglama gibi temel tekniklerin otesinde, prompt'unuzu yapilandirma sekiliniz dil modelini yonlendirmede kritik bir rol oynar. Yapilandirma, prompt icinde talimatlar, baglam veya ornekler gibi farkli bilgi turlerini acik ve duzenli bir sekilde saglamak icin farkli bolumlerin veya ogelerin kullanilmasini icerir. Bu, modelin prompt'u dogru bir sekilde ayristirmasina ve her metin parcasinin belirli rolunu anlamasina yardimci olur.

### Sistem Prompt

Sistem prompt, bir dil modeli icin genel baglami ve amaci belirleyerek, bir etkilesim veya oturum icin hedeflenen davranisini tanimlar. Bu, kurallari, bir kisiyi veya genel davranisi olusturan talimatlarin veya arka plan bilgilerinin saglanmasini icerir. Belirli kullanici sorgularindan farkli olarak, bir sistem prompt modelin yanitlari icin temel yonergeler saglar. Etkilesim boyunca modelin tonunu, tarzini ve genel yaklasimini etkiler. Ornegin, bir sistem prompt modele tutarli bir sekilde kisa ve yardimci olmasi veya yanitlarin genel bir kitle icin uygun olmasi talimati verebilir. Sistem prompt'lari ayrica saygi dilini koruma gibi yonergeler icerebilen guvenlik ve toksiklik kontrolu icin de kullanilir.

Ayrica, etkinliklerini en ust duzeye cikarmak icin sistem prompt'lari, LLM tabanli yinelemeli iyilestirme yoluyla otomatik prompt optimizasyonundan gecirilir. Vertex AI Prompt Optimizer gibi hizmetler, kullanici tarafindan tanimlanan metrikler ve hedef verilere dayali olarak prompt'lari sistematik bir sekilde iyilestirerek belirli bir gorev icin mumkun olan en yuksek performansi saglar.

* **Ornek:**
  You are a helpful and harmless AI assistant. Respond to all queries in a polite and informative manner. Do not generate content that is harmful, biased, or inappropriate

### Rol Prompt

Rol prompt, dil modeline belirli bir karakter, kisi veya kimlik atar ve genellikle sistem veya baglamsal prompt ile birlikte kullanilir. Bu, modele o rolle iliskili bilgi, ton ve iletisim tarzini benimsetmeyi icerir. Ornegin, "Bir seyahat rehberi gibi davran" veya "Uzman bir veri analistisin" gibi prompt'lar modeli o atanan rolun bakis acisi ve uzmanligini yansitmaya yonlendirir. Bir rol tanimlamak, ton, tarz ve odakli uzmanlik icin bir cerceve saglar ve ciktinin kalitesini ve ilgiligini artirmayi amaclar. Rol icinde istenen tarz da belirtilebilir; ornegin, "espirili ve ilham verici bir tarz."

* **Ornek:**
  Act as a seasoned travel blogger. Write a short, engaging paragraph about the best hidden gem in Rome.

### Ayiricilarin Kullanimi

Etkili prompt, dil modelleri icin talimatlarin, baglaminin, orneklerin ve girdinin net bir sekilde ayirt edilmesini icerir. Uclu ters tirnak (```), XML etiketleri (<instruction>, <context>) veya isaretleyiciler (---) gibi ayiricilar, bu bolumleri gorsel ve programatik olarak ayirmak icin kullanilabilir. Prompt muhendisliginde yaygin olarak kullanilan bu uygulama, modelin prompt'un her parcasinin rolunu acikca anlamasini saglayarak yanlis yorumlamayi en aza indirir.

* **Ornek:**
  <instruction>Summarize the following article, focusing on the main arguments presented by the author.</instruction>
  <article>
  [Insert the full text of the article here]
  </article>

## Baglam Muhendisligi (Contextual Engineering)

Baglam muhendisligi, statik sistem prompt'larindan farkli olarak, gorevler ve konusmalar icin kritik arka plan bilgilerini dinamik olarak saglar. Bu surekli degisen bilgi, modellerin nueanslarini kavramasina, gecmis etkilesimleri hatilamasina ve ilgili ayrintilari entegre etmesine yardimci olarak temellendirilmis yanitlara ve daha akici diyaloglara yol acar. Ornekler arasinda onceki diyalog, ilgili belgeler (Retrieval Augmented Generation'da oldugu gibi) veya belirli operasyonel parametreler yer alir. Ornegin, Japonya'ya bir seyahati tartisirken, mevcut konusma baglamini kullanarak Tokyo'da uc aile dostu etkinlik istenebilir. Agentic sistemlerde, baglam muhendisligi bellek kaliciligi, karar verme ve alt gorevler arasinda koordinasyon gibi temel agent davranislarinin temelidir. Dinamik baglamsal boru hatlarina sahip agent'lar, hedefleri zaman icinde surdurebilir, stratejileri uyarlayabilir ve diger agent'lar veya araclarla sorunsuz bir sekilde is birligi yapabilir -- bu nitelikler uzun vadeli otonomi icin gereklidir. Bu metodoloji, bir modelin ciktisinin kalitesinin modelin mimarisinden cok, saglanan baglamin zenginligine baglioldugunu ileri surer. Bu, geleneksel prompt muhendisliginden onemli bir evrime isaret eder; geleneksel yaklasim oncelikle anlik kullanici sorgularinin ifadesini optimize etmeye odaklaniyordu. Baglam muhendisligi kapsamini birden fazla bilgi katmanini iceeecek sekilde genisletir.

Bu katmanlar sunlari icerir:

* **Sistem prompt'lari:** Yapay zekanin operasyonel parametrelerini tanimlayan temel talimatlar (ornegin, "Sen bir teknik yazarsin; tonun resmi ve kesin olmalidir").
* **Harici veri:**
  * **Alinan belgeler:** Yanitlari bilgilendirmek icin bir bilgi tabanindan aktif olarak alinan bilgiler (ornegin, teknik spesifikasyonlarin cekilmesi).
  * **Arac ciktilari:** Yapay zekanin gercek zamanli veriler icin harici bir API kullanmasindan elde edilen sonuclar (ornegin, musaitlik icin takvim sorgulama).
* **Ortuk veri:** Kullanici kimligi, etkilesim gecmisi ve cevre durumu gibi kritik bilgiler. Ortuk baglamin dahil edilmesi gizlilik ve etik veri yonetimi ile ilgili zorluklar olusturur. Bu nedenle, ozellikle kurumsal, saglik ve finans sektorlerinde baglam muhendisligi icin saglam yonetisim esastir.

Temel ilke, gelismis modellerin bile sinirli veya kotukullanilmis olusturulmus bir operasyonel cevre gorunumuyle dusuk performans gosterdigir. Bu uygulama, gorevi sadece bir soruyu cevaplamaktan, agent icin kapsamli bir operasyonel tablo olusturmaya donusturur. Ornegin, baglam muhendisligi uygulanmis bir agent, bir sorguya yanit vermeden once kullanicinin takvim musaitligini (arac ciktisi), bir e-posta alicisiyla profesyonel iliskiyi (ortuk veri) ve onceki toplanti notlarini (alinan belgeler) entegre eder. Bu, modelin son derece ilgili, kisisellestirilmis ve pragmatik olarak faydali ciktilar uretmesini saglar. "Muhendislik" yonu, bu verileri calisma zamaninda almak ve donusturmek icin saglam boru hatlari olusturmayi ve baglam kalitesini surekli iyilestirmek icin geri bildirim dongulerini kurmayı icerir.

Bunu uygulamak icin, Google'in Vertex AI prompt optimizer gibi uzmanlasmis ayarlama sistemleri, iyilestirme surecini buyuk olcekte otomatiklestirebilir. Yanitlari ornek girdilere ve onceden tanimlanmis metriklere gore sistematik olarak degerlendirerek, bu araclar model performansini artirabilir ve kapsamli manuel yeniden yazma gerektirmeden prompt'lari ve sistem talimatlarini farkli modeller arasinda uyarlayabilir. Bir optimize ediciye ornek prompt'lar, sistem talimatlari ve bir sablon saglamak, baglamsal girdileri programatik olarak iyilestirmesine olanak tanir ve sofistike Baglam Muhendisligi icin gerekli geri bildirim dongulrini uygulamak icin yapilandirilmis bir yontem sunar.
Bu yapilandirilmis yaklasim, basit bir yapay zeka aracini daha sofistike, baglamsal farkindaliiga sahip bir sistemden ayirir. Baglami birincil bir bilesen olarak ele alir ve agent'in ne bildigi, ne zaman bildigi ve bu bilgiyi nasil kullandigi uzerinde durur. Bu uygulama, modelin kullanicinin niyetini, gecmisini ve mevcut ortamini kapsamli bir sekilde anlamasini saglar. Sonuc olarak, Baglam Muhendisligi, durumsuz sohbet robotlarini son derece yetenekli, durumsal farkindaliiga sahip sistemlere donusturmek icin kritik bir metodolojidir.

## Yapilandirilmis Cikti (Structured Output)

Cogu zaman prompt'un amaci sadece serbest bicimli bir metin yaniti almak degil, belirli, makine tarafindan okunabilir bir formatta bilgi ciikarmak veya uretmektir. JSON, XML, CSV veya Markdown tablolari gibi yapilandirilmis cikti istemek kritik bir yapilandirma tekniigidir. Ciktiyi belirli bir formatta acikca isteyerek ve potansiyel olarak istenen yapinin bir semasini veya ornegini saglayarak, modeli yanitini agentic sisteminizin veya uygulamanizin diger parcalari tarafindan kolayca ayristiirilabilecek ve kullanilabilecek sekilde duzenlemeye yonlendirirsiniz. Veri cikarma icin JSON nesneleri dondurmek, modeli bir yapi olusturmaya zorladigi ve hallucination'lari sinirlandirabildigi icin faydalidir. Ozellikle veri cikarma veya kategorize etme gibi yaratici olmayan gorevler icin cikti formatlariyla deney yapmak onerilir.

* **Ornek:**
  Extract the following information from the text below and return it as a JSON object with keys `name`, `address`, and `phone.number`.

  Text: "Contact John Smith at 123 Main St, Anytown, CA or call (555) 123-4567."

Sistem prompt'larinin, rol atamalarinin, baglamsal bilgilerin, ayiricilarin ve yapilandirilmis ciktinin etkili kullanimi, dil modelleriyle etkilesimlerin netligini, kontrolunu ve faydasini onemli olcude artirarak guvenilir agentic sistemler gelistirmek icin saglam bir temel olusturur. Yapilandirilmis cikti istemek, dil modelinin ciktisinin sonraki sistem veya isleme adimlari icin girdi olarak hizmet ettigi boru hatlari olusturmak icin kritik oneme sahiptir.

**Pydantic ile Nesne Yonelimli Bir Cephe Olusturma:** Yapilandirilmis ciktiyi zorlamak ve birlikte calisabiliriiigi artirmak icin guclu bir teknik, LLM'nin urettigi verileri Pydantic nesnelerinin orneklerine doldurmaktir. Pydantic, Python tip anotasyonlarini kullanan veri dogrulama ve ayar yonetimi icin bir Python kutuphanesidir. Bir Pydantic modeli tanimlayarak, istenen veri yapiniz icin acik ve uygulanabilir bir sema olusturursunuz. Bu yaklasim, prompt'un ciktisina etkili bir sekilde nesne yonelimli bir cephe saglayarak ham metni veya yari yapilandirilmis verileri dogrulanmis, tip ipuclu Python nesnelerine donusturur.

`model.validate.json` yontemini kullanarak bir LLM'den gelen JSON dizesini dogrudan bir Pydantic nesnesine ayristirabilirsiniz. Bu, ayristirma ve dogrulamayi tek bir adimda birlestirdigi icin ozellikle kullanislidir.

```python
from pydantic import BaseModel, EmailStr, Field, ValidationError
from typing import List, Optional
from datetime import date


# --- Pydantic Model Definition (from above) ---
class User(BaseModel):
    name: str = Field(..., description="The full name of the user.")
    email: EmailStr = Field(..., description="The user's email address.")
    date_of_birth: Optional[date] = Field(None, description="The user's date of birth.")
    interests: List[str] = Field(default_factory=list, description="A list of the user's interests.")


# --- Hypothetical LLM Output ---
llm_output_json = """
{
    "name": "Alice Wonderland",
    "email": "alice.w@example.com",
    "date_of_birth": "1995-07-21",
    "interests": [
        "Natural Language Processing",
        "Python Programming",
        "Gardening"
    ]
}
"""


# --- Parsing and Validation ---
try:
    # Use the model_validate_json class method to parse the JSON string.
    # This single step parses the JSON and validates the data against the User model.
    user_object = User.model_validate_json(llm_output_json)

    # Now you can work with a clean, type-safe Python object.
    print("Successfully created User object!")
    print(f"Name: {user_object.name}")
    print(f"Email: {user_object.email}")
    print(f"Date of Birth: {user_object.date_of_birth}")
    print(f"First Interest: {user_object.interests[0]}")

    # You can access the data like any other Python object attribute.
    # Pydantic has already converted the 'date_of_birth' string to a datetime.date object.
    print(f"Type of date_of_birth: {type(user_object.date_of_birth)}")
except ValidationError as e:
    # If the JSON is malformed or the data doesn't match the model's types,
    # Pydantic will raise a ValidationError.
    print("Failed to validate JSON from LLM.")
    print(e)
```

Bu Python kodu, Pydantic kutuphanesinin bir veri modeli tanimlamak ve JSON verilerini dogrulamak icin nasil kullanildigini gostermektedir. Isim, e-posta, dogum tarihi ve ilgi alanlari icin tip ipuclari ve aciklamalar iceren bir User modeli tanimlar. Kod daha sonra User modelinin `model.validate.json` yontemini kullanarak bir Buyuk Dil Modelinden (LLM) gelen varsayimsal bir JSON ciktisini ayristirir. Bu yontem, hem JSON ayristirmasini hem de veri dogrulamasini modelin yapisi ve turlerine gore yonetir. Son olarak, kod dogrulanmis verilere ortaya cikan Python nesnesinden erisir ve JSON'un gecersiz olmasi durumunda ValidationError icin hata islemesi icerir.

XML verileri icin xmltodict kutuphanesi, XML'i bir sozluge donusturmek icin kullanilabilir ve bu sozluk daha sonra ayristirma icin bir Pydantic modeline aktarilabilir. Pydantic modelinizde Field alias'lari kullanarak, XML'in genellikle ayrintili veya ozellik agirlikli yapisini nesnenizin alanlarina sorunsuz bir sekilde eslestirbiilirsiniz.

Bu metodoloji, LLM tabanli bilesenlerin daha buyuk bir sistemin diger parcalariyla birlikte calisabilirligini saglamak icin paha bicilmezdir. Bir LLM'nin ciktisi bir Pydantic nesnesi icinde kapsullendiginde, verilerin beklenen yapi ve turlere uygun oldugu guencesiyle diger fonksiyonlara, API'lere veya veri isleme boru hatlarina guvenilir bir sekilde aktarilabilir. Sistem bilesenlerinizin sinirlarinda "dogrulama degil, ayristirma" uygulamasi daha saglam ve bakimi kolay uygulamalara yol acar.

Sistem prompt'larinin, rol atamalarinin, baglamsal bilgilerin, ayiricilarin ve yapilandirilmis ciktinin etkili kullanimi, dil modelleriyle etkilesimlerin netligini, kontrolunu ve faydasini onemli olcude artirarak guvenilir agentic sistemler gelistirmek icin saglam bir temel olusturur. Yapilandirilmis cikti istemek, dil modelinin ciktisinin sonraki sistem veya isleme adimlari icin girdi olarak hizmet ettigi boru hatlari olusturmak icin kritik oneme sahiptir.

Prompt'larin Yapilandirilmasi: Ornek saglama gibi temel tekniklerin otesinde, prompt'unuzu yapilandirma sekiliniz dil modelini yonlendirmede kritik bir rol oynar. Yapilandirma, prompt icinde talimatlar, baglam veya ornekler gibi farkli bilgi turlerini acik ve duzenli bir sekilde saglamak icin farkli bolumlerin veya ogelerin kullanilmasini icerir. Bu, modelin prompt'u dogru bir sekilde ayristirmasina ve her metin parcasinin belirli rolunu anlamasina yardimci olur.

# Akil Yurutme ve Dusunce Sureci Teknikleri

Buyuk dil modelleri oruntu tanima ve metin uretmede mukemmeldir ancak genellikle karmasik, cok adimli akil yurutme (Reasoning) gerektiren gorevlerde zorluklarla karsilasir. Bu ek, modellerin ic dusunce sureclerini ortaya cikarmaya tesvik ederek bu akil yurutme yeteneklerini gelistirmek icin tasarlanmis tekniklere odaklanir. Ozellikle, mantiksal cikarim, matematiksel hesaplama ve planlama (Planning) yeteneklerini gelistirme yontemlerini ele alir.

## Chain of Thought (CoT)

Chain of Thought (CoT) prompt teknigi, modeli nihai bir cevaba ulasmadan once ara akil yurutme adimlari uretmeye acikca tesvik ederek dil modellerinin akil yurutme yeteneklerini gelistirmek icin guclu bir yontemdir. Sadece sonucu sormak yerine, modele "adim adim dusun" talimati verilir. Bu surec, bir insanin bir problemi daha kucuk, daha yonetilebilir parcalara ayirip bunlari sirasiyla islemesine benzer.

CoT, LLM'nin ozellikle bir tur hesaplama veya mantiksal cikarim gerektiren gorevlerde daha dogru cevaplar uretmesine yardimci olur; bu gorevlerde modeller aksi takdirde zorlanabilir ve yanlis sonuclar uretebilir. Bu ara adimlari ureterek, modelin dogru yolda kalmasi ve gerekli islemleri dogru bir sekilde gerceklestirmesi daha olasi hale gelir.

CoT'nin iki temel varyasyonu vardir:

* **Zero-Shot CoT:** Bu, akil yurutme surecinin herhangi bir ornegi saglanmadan prompt'unuza basitce "Adim adim dusunelim" (veya benzer bir ifade) eklenmesini icerir. Sasirtici bir sekilde, bircok gorev icin bu basit ekleme, modelin ic akil yurutme izini ortaya cikarma yetenegini tetikleyerek performansini onemli olcude artirabilir.
  * **Ornek (Zero-Shot CoT):**
    If a train travels at 60 miles per hour and covers a distance of 240 miles, how long did the journey take? Let's think step by step.

* **Few-Shot CoT:** Bu, CoT'yi few-shot prompt ile birlestirrir. Modele hem girdinin, hem adim adim akil yurutme surecinin hem de nihai ciktinin gosterildigi birkac ornek saglanir. Bu, modele akil yurutmeyi nasil gerceklestirecegi ve yanitini nasil yapilandiracagi konusunda daha net bir sablon verir ve genellikle zero-shot CoT'ye kiyasla daha karmasik gorevlerde daha iyi sonuclar verir.
  * **Ornek (Few-Shot CoT):**
    Q: The sum of three consecutive integers is 36. What are the integers?
    A: Let the first integer be x. The next consecutive integer is x+1, and the third is x+2. The sum is x + (x+1) + (x+2) = 3x + 3. We know the sum is 36, so 3x + 3 = 36. Subtract 3 from both sides: 3x = 33. Divide by 3: x = 11. The integers are 11, 11+1=12, and 11+2=13. The integers are 11, 12, and 13.

    Q: Sarah has 5 apples, and she buys 8 more. She eats 3 apples. How many apples does she have left? Let's think step by step.
    A: Let's think step by step. Sarah starts with 5 apples. She buys 8 more, so she adds 8 to her initial amount: 5 + 8 = 13 apples. Then, she eats 3 apples, so we subtract 3 from the total: 13 - 3 = 10. Sarah has 10 apples left. The answer is 10.

CoT bircok avantaj sunar. Uygulamasi nispeten dusuk eforludur ve fine-tuning gerektirmeden hazir LLM'lerle son derece etkili olabilir. Onemli bir fayda, modelin ciktisinin artan yorumlanabilirliigidir; takip ettigi akil yurutme adimlarini gorebilirsiniz, bu da belirli bir cevaba neden ulastigini anlamaya ve bir seyler ters gittiginde hata ayiklamaya yardimci olur. Ayrica, CoT prompt'larin farkli dil model versiyonlari arasinda saglamliligini artirmaktadir, yani model guncellendiginde performansin dusme olasiligi daha azdir. Ana dezavantaj, akil yurutme adimlarinin olusturulmasinin cikti uzunlugunu artirmasi, daha yuksek token kullanimina yol acmasi ve bu durumun maliyeti ve yanit suresini artirabilmesidir.

CoT icin en iyi uygulamalar arasinda nihai cevabin akil yurutme adimlarindan *sonra* sunulmasi yer alir, cunku akil yurutmenin olusturulmasi cevap icin sonraki token tahminlerini etkiler. Ayrica, tek bir dogru cevabi olan gorevler icin (matematiksel problemler gibi), her adimda en olasi sonraki token'in deterministik secimini saglamak amaciyla CoT kullanirken modelin sicakliginin 0'a (greedy decoding) ayarlanmasi onerilir.

## Oz-Tutarlilik (Self-Consistency)

Chain of Thought fikri uzerine insa edilen Oz-Tutarlilik teknigi, dil modellerinin olasiliksal dogasini kullanarak akil yurutmenin guvenilirligini artirmayi amaclar. Tek bir greedy akil yurutme yoluna guuenmek yerine (temel CoT'de oldugu gibi), Oz-Tutarlilik ayni problem icin birden fazla farkli akil yurutme yolu uretir ve ardindan bunlar arasindaki en tutarli cevabi secer.

Oz-Tutarlilik uc ana adim icerir:

1. **Cesitli Akil Yurutme Yollari Olusturma:** Ayni prompt (genellikle bir CoT prompt'u) LLM'ye birden fazla kez gonderilir. Daha yuksek bir sicaklik ayari kullanilarak, model farkli akil yurutme yaklasimlari kesfetmeye ve cesitli adim adim aciklamalar uretmeye tesvik edilir.
2. **Cevabi Cikarma:** Nihai cevap, olusturulan her akil yurutme yolundan cikarilir.
3. **En Yaygin Cevabi Secme:** Cikarilan cevaplar uzerinde cogunluk oyu gerceklestirilir. Cesitli akil yurutme yollarinda en sik gorulen cevap, nihai, en tutarli cevap olarak secilir.

Bu yaklasim, birden fazla gecerli akil yurutme yolunun bulunabilecegi veya modelin tek bir denemede hataya yatkin olabilecegi gorevlerde yanitlarin dogrulugunu ve tutarliligini arttirir. Faydasi, cevabin dogru olma olasiliginin sahte bir olasilik tahmini sunmasi ve genel dogrulugu artirmasidir. Ancak onemli maliyet, ayni sorgu icin modelin birden fazla kez calistirilmasi gereksinimidir ve bu durum cok daha yuksek hesaplama ve gidere yol acar.

* **Ornek (Kavramsal):**
  * *Prompt:* "Is the statement 'All birds can fly' true or false? Explain your reasoning."
  * *Model Calistirma 1 (Yuksek Sicaklik):* Cogu kusu ucmayi ele alir, Dogru sonucuna varir.
  * *Model Calistirma 2 (Yuksek Sicaklik):* Penguenler ve devekuslarini ele alir, Yanlis sonucuna varir.
  * *Model Calistirma 3 (Yuksek Sicaklik):* *Genel olarak* kuslari ele alir, istisnalardan kscaca bahseder, Dogru sonucuna varir.
  * *Oz-Tutarlilik Sonucu:* Cogunluk oyuna dayali olarak (Dogru iki kez gorulur), nihai cevap "Dogru"dur. (Not: Daha sofistike bir yaklasim akil yurutme kalitesini de tartardir).

## Geri Adim Atma Prompt'u (Step-Back Prompting)

Geri adim atma prompt'u, oncelikle dil modelinden belirli ayrintilari ele almadan once gorevle ilgili genel bir ilke veya kavrami dusunmesini isteyerek akil yurutmeyi gelistirir. Bu daha genis soruya verilen yanit, daha sonra orijinal problemi cozmek icin baglam olarak kullanilir.

Bu surec, dil modelinin ilgili arka plan bilgisini ve daha genis akil yurutme stratejilerini etkinlestirmesine olanak tanir. Altta yatan ilkelere veya daha yuksek duzey soyutlamalara odaklanarak, model yuzeysel unsurlardan daha az etkilenen, daha dogru ve anlayisli cevaplar uretebilir. Baslangicta genel faktorleri dikkate almak, belirli yaratici ciktilar uretmek icin daha guclu bir temel saglayabilir. Geri adim atma prompt'u, elestirel dusunmeyi ve bilgi uygulamasini tesvik eder ve genel ilkeleri vurgulayarak onyargilari potansiyel olarak azaltir.

* **Ornek:**
  * *Prompt 1 (Geri Adim):* "What are the key factors that make a good detective story?"
  * *Model Yaniti 1:* (Kirmizi ringa, cekici motif, kusurlu bakarakter, mantiksal ipuclari, tatmin edici cozum gibi unsurları listeler).
  * *Prompt 2 (Orijinal Gorev + Geri Adim Baglami):* "Using the key factors of a good detective story [insert Model Response 1 here], write a short plot summary for a new mystery novel set in a small town."

## Tree of Thoughts (ToT)

Tree of Thoughts (ToT), Chain of Thought yontemini genisleten gelismis bir akil yurutme tekniigidir. Tek bir dogrusal ilerleme izlemek yerine, bir dil modelinin birden fazla akil yurutme yolunu es zamanli olarak kesfetmesini saglar. Bu teknik, her dugumun bir "dusunce" -- ara adim olarak islev goren tutarli bir dil dizisi -- temsil ettigi bir agac yapisi kullanir. Her dugumden, model dallanarak alternatif akil yurutme yollarini kesifedebilir.

ToT, cozume ulasmadan once kesif (Exploration), geri izleme veya birden fazla olasiiliigin degerlendirilmesini gerektiren karmasik problemler icin ozellikle uygundur. Dogrusal Chain of Thought yonteminden hesaplama acisindan daha talepkar ve uygulanmasi daha karmasik olsa da, ToT kasitli ve kesfedici problem cozmeyi gerektiren gorevlerde ustun sonuclar elde edebilir. Bir agent'in cesitli bakis acilarini dikkate almasina ve "dusunce agaci" icindeki alternatif dallari inceleyerek baslangic hatalarindan potansiyel olarak kurtulmasina olanak tanir.

* **Ornek (Kavramsal):** "Bu olay orgusu noktalarina dayanarak bir hikaye icin uc farkli olasi son gelistirin" gibi karmasik bir yaratici yazma gorevi icin, ToT modelin tek bir dogrusal devam uretmek yerine onemli bir donge noktasindan farkli anlatim dallarini kesfetmesine olanak tanir.

Bu akil yurutme ve dusunce sureci teknikleri, basit bilgi alma veya metin uretmenin otesindeki gorevleri yerine getirebilen agent'lar olusturmak icin kritik oneme sahiptir. Modelleri akil yurutmelerini ortaya koymaya, birden fazla bakis acisini dikkate almaya veya genel ilkelere geri donmeye tesvik ederek, agentic sistemler icindeki karmasik bilissel gorevleri gerceklestirme yeteneklerini onemli olcude artirabilriiz.

# Eylem ve Etkilesim Teknikleri

Akilli agent'lar, metin uretmenin otesinde cevreleriyle aktif olarak etkilesim kurma yetenegine sahiptir. Bu, arac kullanmayi, harici fonksiyonlari yurutmeyi ve gozlem, akil yurutme ve eylem dongulerine katilmayi icerir. Bu bolum, bu aktif davranislari mumkun kilan prompt tekniklerini incelemektedir.

## Tool Use / Function Calling

Bir agent icin kritik bir yetenek, ic yeteneklerinin otesinde eylemler gerceklestirmek icin harici araclar kullanmak veya fonksiyon cagirmaktir. Bu eylemler web aramalari, veritabani erisimi, e-posta gonderme, hesaplama yapma veya harici API'lerle etkilesim kurmayi icerebilir. Tool use icin etkili prompt, modele arac kullaniminin uygun zamanlamasi ve metodolojisi hakkinda talimat veren prompt'lar tasarlamayi icerir.

Modern dil modelleri genellikle "function calling" veya "tool use" icin fine-tuning'den gecer. Bu, mevcut araclarin aciklamalarini, amaclarini ve parametrelerini yorumlamalarini saglar. Bir kullanici istegi alindiiinda, model arac kullaniminin gerekliligini belirleyebilir, uygun araci tanimlayabilir ve cagrimi icin gerekli argumanlari biimlendirebilir. Model araci dogrudan yurutmez. Bunun yerine, araci ve parametrelerini belirten yapilandirilmis bir cikti, tipik olarak JSON formatinda, uretir. Bir agentic sistem daha sonra bu ciktiyi isler, araci yurutur ve araCin sonucunu modele geri saglayarak devam eden etkilesime entegre eder.

* **Ornek:**
  You have access to a weather tool that can get the current weather for a specified city. The tool is called '`get.current.weather`' and takes a '`city`' parameter (string).

  User: What's the weather like in London right now?

  * *Beklenen Model Ciktisi (Function Call):*
    {
      "tool.code": "get.current.weather",
      "tool.name": "get.current.weather",
      "parameters": {
        "city": "London"
      }
    }

## ReAct (Reason & Act)

ReAct, yani Akil Yurut ve Eyleme Gec, Chain of Thought tarzinda akil yurutmeyi araclar kullanarak eylem gerceklestirme yetenegiyle birbirine gecmis bir sekilde birlestiren bir prompt paradigmasidir. ReAct, insanlarin nasil calistigini taklit eder -- sozlu olarak akil yurutuur ve daha fazla bilgi toplamak veya bir hedefe dogru ilerleme kaydetmek icin eylemler gerceklestiririz.

ReAct kaliibi bir dongu icerir:

1. **Dusunce:** Model, mevcut anilayisini ve planini aciklayan bir dusunce sureci olusturur.
2. **Eylem:** Dusunceye dayanarak, model genellikle bir arac kullanarak (ornegin, Arama, Hesap Makinesi, API cagirisi) bir eylem gerceklestirmeye karar verir. Aracin adini ve gerekli girdiyi cikti olarak verir.
3. **Gozlem:** Agentic sistem araci calistirir ve sonucu (Gozlem) modele geri saglar.
4. Dongu, modelin en son "Gozlem"e dayali yeni bir "Dusunce" uretmesiyle devam eder ve gorev tamamlanana ve model bir "Nihai Cevap" ciktisi verene kadar daha fazla "Eylem" ve "Gozlem"e yol acar.

Bu birbirine gecmis dusunme ve eyleme gecme sureci, agent'in dinamik olarak bilgi toplamasina, arac ciktilarina tepki vermesine ve yaklasimini iyilestirmesine olanak tanir ve bu da ozellikle dinamik ortamlar veya harici bilgi kaynaklariyla etkilesim gerektiren gorevler icin etkili olmasini saglar.

* **Ornek (Gosterimsel ReAct Izi):**
  User: What is the capital of France and its current population?

  Thought: The user is asking for two pieces of information: the capital of France and its population. I can use a search tool to find this information. I will start by confirming the capital, although I am likely to know it.
  Action: Search({"query": "capital of France"})
  Observation: Paris

  Thought: Okay, the capital is Paris. Now I need to find the population of Paris.
  Action: Search({"query": "current population of Paris"})
  Observation: The population of Paris was estimated to be around 2.1 million people in 2023.

  Thought: I have found both pieces of information. I can now provide the final answer to the user.
  Final Answer: The capital of France is Paris, and its estimated population in 2023 was around 2.1 million people.

Bu teknikler, dunyayla aktif olarak etkilesim kurabilen, gercek zamanli bilgi alabilen ve harici sistemlerle etkilesim gerektiren gorevleri yerine getirebilen agent'lar olusturmak icin hayati oneme sahiptir.

## Gelismis Teknikler

Temel, yapisal ve akil yurutme kaliplarinin otesinde, agentic sistemlerin yeteneklerini ve verimliliigini daha da artirabilen birkac prompt teknigi daha vardir. Bunlar, prompt'lari optimize etmek icin yapay zekayi kullanmaktan harici bilgileri dahil etmeye ve kullanici ozelliklerine gore yanitlari uyarlamaya kadar uzanir.

### Otomatik Prompt Muhendisligi (APE)

Etkili prompt'lar olusturmanin karmasik ve yinelemeli bir surec olabilecegini kabul eden Otomatik Prompt Muhendisligi (APE), prompt'lari olusturmak, degerlendirmek ve iyilestirmek icin dil modellerinin kendilerini kullanmayi arastiirir. Bu yontem, prompt tasariminda kapsamli insan cabasi gerektirmeden model performansini potansiyel olarak artirarak prompt yazma surecini otomatiklestirmeyi amaclar.

Genel fikir, bir "meta-model"in veya bir surecin gorev aciklamasi alip birden fazla aday prompt uretmesidir. Bu prompt'lar daha sonra belirli bir girdi seti uzerinde urrettikleri ciktinin kalitesine gore degerlendirilir (belki BLEU veya ROUGE gibi metrikler veya insan degerlendirmesi kullanilarak). En iyi performans gosteren prompt'lar secilebilir, potansiyel olarak daha da iyilestirilebilir ve hedef gorev icin kullanilabilir. Bir sohbet robotunu egitmek icin kullanici sorgusunun varyasyonlarini uretmek icin LLM kullanmak bunun bir ornegidir.

* **Ornek (Kavramsal):** Bir gelistirici su aciklamayi saglar: "Bir e-postadan tarih ve gondereni cikarabilen bir prompt'a ihtiyacim var." Bir APE sistemi birkac aday prompt uretir. Bunlar ornek e-postalarda test edilir ve tutarli bir sekilde dogru bilgiyi cikaran prompt secilir.

Programatik prompt optimizasyonunun yeniden ifade edilmis ve biraz genisletilmis bir aciklamasi, ozellikle DSPy gibi cerceveler kullanilarak:

Bir diger guclu prompt optimizasyon teknigi, ozellikle DSPy cercevesi tarafindan onerilir ve prompt'lari statik metin olarak degil, otomatik olarak optimize edilebilen programatik moduller olarak ele almayi icerir. Bu yaklasim, manuel deneme-yanilmanin otesine geceerek daha sistematik, veri odakli bir metodolojiye dogru ilerler.

Bu teknigin temeli iki anahtar bilesene dayanir:

1. **Altin Kume (veya Yuksek Kaliteli Veri Kumesi):** Bu, yuksek kaliteli girdi-cikti ciftlerinden olusan temsili bir kumedir. Belirli bir gorev icin basarili bir yanitin neye benzedigini tanimlayan "zemin gercegi" olarak hizmet eder.
2. **Amac Fonksiyonu (veya Puanlama Metrigi):** Bu, LLM'nin ciktisini veri kumesindeki karsilik gelen "altin" ciktiyla otomatik olarak degerlendiren bir fonksiyondur. Yanitin kalitesini, dogrulugunu veya isabetrliligini gosteren bir puan dondurur.

Bu bilesenleri kullanan bir optimize edici, ornegin bir Bayes optimize edici, prompt'u sistematik olarak iyiilestirir. Bu surec genellikle bagimsiz olarak veya birlikte kullanilabilen iki ana strateji icerir:

* **Few-Shot Ornek Optimizasyonu:** Bir gelistiricinin few-shot prompt icin ornekleri manuel olarak secmesi yerine, optimize edici altin kumeden farkli ornek kombinasyonlarini programatik olarak ornekler. Daha sonra, modeli istenen ciktilari uretmeye en etkili sekilde yonlendiren belirli ornek kumesini belirlemek icin bu kombinasyonlari test eder.

* **Talimatsal Prompt Optimizasyonu:** Bu yaklasimda, optimize edici prompt'un temel talimatlarini otomatik olarak iyilestirir. Bir LLM'yi "meta-model" olarak kullanarak prompt'un metnini yinelemeli olarak mutasyona ugraatir ve yeniden ifade eder -- ifadeyi, tonu veya yapiyi ayarlayarak -- amac fonksiyonundan en yuksek puanlari veren ifadeyi kesfeder.

Her iki strateji icin de nihai amac, amac fonksiyonundan alinan puanlari maksimize etmek, boylece prompt'u yuksek kaliteli altin kumeye tutarli bir sekilde daha yakin sonuclar uretecek sekilde etkili bir bicimde "egitmek"tir. Bu iki yaklasimi birlestirerek, sistem modele *hangi talimatlarin* verilecegini ve *hangi orneklerin* gosterilecegini es zamanli olarak optimize edebilir ve bu da belirli gorev icin makine tarafindan optimize edilmis, son derece etkili ve saglam bir prompt'a yol acar.

### Yinelemeli Prompt / Iyilestirme

Bu teknik, basit, temel bir prompt ile baslamayi ve ardindan modelin ilk yanitlarina dayanarak yinelemeli olarak iyilestirmeyi icerir. Modelin ciktisi tam olarak dogru degilse, eksiklikleri analiz edip bunlari gidermek icin prompt'u degistirirsiniz. Bu, otomatik bir surecten (APE gibi) cok, insan odakli yinelemeli bir tasarim dongusu hakkindadir.

* **Ornek:**
  * *Deneme 1:* "Write a product description for a new type of coffee maker." (Sonuc cok genel).
  * *Deneme 2:* "Write a product description for a new type of coffee maker. Highlight its speed and ease of cleaning." (Sonuc daha iyi, ancak ayrintisiz).
  * *Deneme 3:* "Write a product description for the 'SpeedClean Coffee Pro'. Emphasize its ability to brew a pot in under 2 minutes and its self-cleaning cycle. Target busy professionals." (Sonuc istenen ciktiya cok daha yakin).

### Negatif Ornekler Saglama

"Kisitlamalar Yerine Talimatlar" ilkesi genel olarak gecerli olsa da, dikkatli kullanilmak kaydiyla negatif ornekler saglamanin yardimci olabilecegi durumlar vardir. Negatif ornek, modele bir girdi ve *istenmeyen* bir cikti veya bir girdi ve *uretilmemesi gereken* bir cikti gosterir. Bu, sinirlari netlestirmeye veya belirli turde yanlis yanitlari onlemeye yardimci olabilir.

* **Ornek:**
  Generate a list of popular tourist attractions in Paris. Do NOT include the Eiffel Tower.

  Example of what NOT to do:
  Input: List popular landmarks in Paris.
  Output: The Eiffel Tower, The Louvre, Notre Dame Cathedral.

### Analoji Kullanimi

Bir gorevi bir analoji kullanarak cercevelemek, bazen modelin istenen ciktiyi veya sureci taniidik bir seye iliskilendirerek anlamasina yardimci olabilir. Bu, ozellikle yaratici gorevler veya karmasik rolleri aciklamak icin faydali olabilir.

* **Ornek:**
  Act as a "data chef". Take the raw ingredients (data points) and prepare a "summary dish" (report) that highlights the key flavors (trends) for a business audience.

### Faktorlu Bilis / Ayristirma (Factored Cognition / Decomposition)

Cok karmasik gorevler icin, genel hedefi daha kucuk, daha yonetilebilir alt gorevlere ayirmak ve modeli her alt gorev uzerinde ayri ayri sorgulamak etkili olabilir. Alt gorevlerden elde edilen sonuclar daha sonra nihai sonuca ulasmak icin birlestirilir. Bu, prompt zincirleme ve planlama ile iliskilidir ancak problemin kasitli olarak ayristirilmasini vurgular.

* **Ornek:** Bir arastirma makalesi yazmak icin:
  * Prompt 1: "Generate a detailed outline for a paper on the impact of AI on the job market."
  * Prompt 2: "Write the introduction section based on this outline: [insert outline intro]."
  * Prompt 3: "Write the section on 'Impact on White-Collar Jobs' based on this outline: [insert outline section]." (Diger bolumler icin tekrarlaniir).
  * Prompt N: "Combine these sections and write a conclusion."

### Retrieval Augmented Generation (RAG)

RAG, dil modellerini prompt sureci sirasinda harici, guncel veya alana ozgu bilgilere erisim saglayarak gelistiren guclu bir tekniktir. Bir kullanici soru sordugunda, sistem once bir bilgi tabanindan (ornegin bir veritabani, belge kumesi, web) ilgili belgeleri veya verileri alir. Alinan bu bilgi daha sonra prompt'a baglam olarak dahil edilir ve dil modelinin bu harici bilgiye dayali bir yanit uretmesine olanak tanir. Bu, hallucination gibi sorunlari azaltir ve modelin egitilmedigi veya cok yeni olan bilgilere erisim saglar. Bu, dinamik veya ozel bilgilerle calismasi gereken agentic sistemler icin onemli bir kaliptir.

* **Ornek:**
  * *Kullanici Sorgusu:* "What are the new features in the latest version of the Python library 'X'?"
  * *Sistem Eylemi:* "Python library X latest features" icin bir dokumantasyon veritabaninda arama yapilir.
  * *LLM'ye Prompt:* "Based on the following documentation snippets: [insert retrieved text], explain the new features in the latest version of Python library 'X'."

### Kisi Kaliibi (Kullanici Kisisi)

Rol prompt modele bir kisi atarken, Kisi Kalibi kullaniciyi veya modelin ciktisinin hedef kitlesini tanimlamayi icerir. Bu, modelin yanitini dil, karmasiklik, ton ve saglanan bilgi turu acisindan uyarlamasina yardimci olur.

* **Ornek:**
  You are explaining quantum physics. The target audience is a high school student with no prior knowledge of the subject. Explain it simply and use analogies they might understand.

  Explain quantum physics: [Insert basic explanation request]

Bu gelismis ve tamamlayici teknikler, prompt muhendislerine model davranisini optimize etmek, harici bilgileri entegre etmek ve agentic is akislari icinde belirli kullanicilar ve gorevler icin etkilesimleri uyarlamak icin ek araclar saglar.

## Google Gems Kullanimi

Google'in yapay zeka "Gems"leri (bkz. Sekil 1), buyuk dil model mimarisi icinde kullanici tarafindan yapilandirilabilir bir ozelliigi temsil eder. Her "Gem", belirli, tekrarlanabilir gorevler icin ozellestirilmis temel Gemini yapay zekasinin uzmanlasmis bir ornegi olarak isler. Kullanicilar, operasyonel parametrelerini olusturan acik talimatlar seti saglayarak bir Gem olusturur. Bu baslangic talimat seti, Gem'in belirlenmis amacini, yanit tarzini ve bilgi alanini tanimlar. Altta yatan model, konusma boyunca bu onceden tanimlanmis yoneergelere tutarli bir sekilde uymak icin tasarlanmistir.

Bu, odakli uygulamalar icin son derece uzmanlasmis yapay zeka agent'larinin olusturulmasina olanak tanir. Ornegin, bir Gem yalnizca belirli programlama kutuphanelerine basvuran bir kod yorumlayicisi olarak yapilandiirilabilir. Bir digeri, spekulatif yorum olmaksizin ozetler ureterek veri kumelerini analiz etmek icin talimatlandirilabilir. Farkli bir Gem, belirli bir resmi stil kilavuzuna bagli bir cevirmen olarak hizmet edebilir. Bu surec, yapay zeka icin kalici, goreve ozgu bir baglam olusturur.

Sonuc olarak, kullanici her yeni sorguda ayni baglamsal bilgiyi yeniden kurmak zorunda kalmaz. Bu metodoloji, konusma tekrarini azaltir ve gorev yurutmenin verimliliigini artirir. Ortaya cikan etkilesimler daha odakli olup, kullanicinin baslangic gereksinimleriyle tutarli bir sekilde uyumlu ciktilar verir. Bu cerceve, genel amacli bir yapay zeka modeline ince ayarli, kalici kullanici yonlendirmesi uygulamaya olanak tanir. Sonuc olarak, Gems genel amacli etkilesimden uzmanlasmis, onceden tanimlanmis yapay zeka islevselliklerine gecisi mumkun kilar.

![Example of Google Gem Usage](../assets/Example_of_Google_Gem_Usage.png)

Sekil 1: Google Gem kullanim ornegi.

## Prompt'lari Iyilestirmek Icin LLM Kullanimi (Meta Yaklasim)

Etkili prompt'lar olusturmak icin netlik, yapi, baglam veya ornekler saglama uzerine cok sayida teknik inceledik. Ancak bu surec yinelemeli olabilir ve bazen zorlu olabilir. Ya buyuk dil modellerinin, ornegin Gemini'nin gucunden yararlanarak prompt'larimizi *iyilestirebilseydik*? Prompt iyilestirme icin LLM'lerin kullanilmasinin ozu budur -- yapay zekayi yapay zekaya verilen talimatlari optimize etmek icin kullanan bir "meta" uygulama.

Bu yetenek ozellikle heyecan vericidir cunku bir tur yapay zeka kendini iyilestirmesini veya en azindan yapay zeka ile etkilesimde yapay zeka destekli insan gelisimini temsil eder. Yalnizca insan sezgisine ve deneme-yanilmaya guuenmek yerine, prompt'larimizi daha iyi hale getirmek icin oneriler almak uzere LLM'nin dil, oruntuler ve hatta yaygin prompt tuzaklari konusundaki anilayisindan faydalanabiliriz. LLM'yi prompt muhendisligi surecinde is birlikci bir ortaga donustuurur.

Bu pratikte nasil calisir? Bir dil modeline iyilestirmeye calistiginiz mevcut bir prompt'u, gerceklestirmesini istediginiz gorevi ve belki de su anda aldiiginiz ciktinin orneklerini (ve neden beklentilerinizi karsilamadigini) saglayabilirsiniz. Ardindan LLM'den prompt'u analiz edip iyilestirmeler onermesini istersiniz.

Guclu akil yurutme ve dil uretme yeteneklerine sahip Gemini gibi bir model, mevcut prompt'unuzu potansiyel belirsizlik alanlari, ozgulluk eksikligi veya verimsiz ifadeler acisindan analiz edebilir. Tartistigimiz tekniklerin dahil edilmesini onerebilir; ornegin ayiricilar ekleme, istenen cikti formatini netlestirme, daha etkili bir kisi onerme veya few-shot orneklerin dahil edilmesini tavsiye etme gibi.

Bu meta-prompt yaklasiminin faydalari sunlardir:

* **Hizlandirilmis Yineleme:** Salt manuel deneme ve yanilmadan cok daha hizli iyilestirme onerileri alin.
* **Kor Noktalarin Tespiti:** Bir LLM, prompt'unuzdaki gozden kacirdiginiz belirsizlikleri veya potansiyel yanlis yorumlamalari fark edebilir.
* **Ogrenme Firsati:** LLM'nin yaptigi onerri turlerini gorerek, prompt'lari etkili kilan unsurlar hakkinda daha fazla bilgi edinebilir ve kendi prompt muhendisligi becerilerinizi gelistirebilirsiniz.
* **Olceklenebilirlik:** Ozellikle cok sayida prompt ile ugrasildiginda, prompt optimizasyon surecinin bazi kisimlarin potansiyel olarak otomatiklestirin.

LLM'nin onerilerinin her zaman mukemmel olmadigini ve herhangi bir manuel olarak olusturulmus prompt gibi degerlendirilip test edilmesi gerektigini belirtmek onemlidir. Ancak, guclu bir baslangic noktasi saglar ve iyilestirme surecini onemli olcude kolaylastirabilir.

* **Iyilestirme Icin Ornek Prompt:**
  Analyze the following prompt for a language model and suggest ways to improve it to consistently extract the main topic and key entities (people, organizations, locations) from news articles. The current prompt sometimes misses entities or gets the main topic wrong.

  Existing Prompt:
  "Summarize the main points and list important names and places from this article: [insert article text]"

  Suggestions for Improvement:

Bu ornekte, baska bir prompt'u elestirmek ve gelistirmek icin LLM'yi kullaniyoruz. Bu meta-duzey etkilesim, bu modellerin esnekligini ve gucunu gostererek, once aldiklari temel talimatlari optimize ederek daha etkili agentic sistemler olusturmamiza olanak tanir. Yapay zekanin yapay zeka ile daha iyi iletisim kurmamiza yardimci oldugu buyu leyici bir dongudur.

## Belirli Gorevler Icin Prompt

Simdiye kadar tartisilan teknikler genis capli uygulanabilir olsa da, bazi gorevler belirli prompt hususlarindan fayda gorur. Bunlar ozellikle kod ve cok modlu girdiler alaninda gecerlidir.

### Kod Prompt

Buyuk kod veri kumeleri uzerinde egitilmis dil modelleri, gelistiriciler icin guclu yardimcilar olabilir. Kod icin prompt, LLM'lerin kod uretme, aciklama, cevrime veya hata ayiklama amaciyla kullanilmasini icerir. Cesitli kullanim alanlari mevcuttur:

* **Kod yazmak icin prompt'lar:** Modelden istenen islevselligin aciklamasina dayali olarak kod parcalari veya fonksiyonlar uretmesini istemek.
  * **Ornek:** "Write a Python function that takes a list of numbers and returns the average."
* **Kod aciklamak icin prompt'lar:** Bir kod parcasi saglayip modelden ne yaptigini satir satir veya ozet olarak aciklamasini istemek.
  * **Ornek:** "Explain the following JavaScript code snippet: [insert code]."
* **Kod cevirmek icin prompt'lar:** Modelden kodu bir programlama dilinden digerine cevirmesini istemek.
  * **Ornek:** "Translate the following Java code to C++: [insert code]."
* **Kod hata ayiklama ve inceleme icin prompt'lar:** Hatasi olan veya iyilestirilebilecek kodu saglayip modelden sorunlari belirlemesini, duzeltme onerilerini sunmasini veya yeniden duzenleme onerileri vermesini istemek.
  * **Ornek:** "The following Python code is giving a 'NameError'. What is wrong and how can I fix it? [insert code and traceback]."

Etkili kod prompt'u genellikle yeterli baglam saglanmasini, istenen dil ve versiyonun beliritilmesini ve islevsellik veya sorun hakkinda net olunmasini gerektirir.

### Cok Modlu Prompt (Multimodal Prompting)

Bu ekin ve mevcut LLM etkilesimlerinin buyuk bolumunun odagi metin tabanli olsa da, alan farkli modaliteler (metin, gorsel, ses, video vb.) arasinda bilgi isleyebilen ve uretebilen cok modlu modellere dogru hizla ilerlemektedir. Cok modlu prompt, modeli yonlendirmek icin bir girdi kombinasyonunun kullanilmasini icerir. Bu, sadece metin yerine birden fazla girdi formatinin kullanilmasini ifade eder.

* **Ornek:** Bir diyagram gorseli saglayip modelden diyagramda gosterilen sureci aciklamasini istemek (Gorsel Girdi + Metin Prompt). Veya bir gorsel saglayip modelden aciklayici bir baslik uretmesini istemek (Gorsel Girdi + Metin Prompt -> Metin Ciktisi).

Cok modlu yetenekler daha sofistike hale geldikce, prompt teknikleri bu birlesik girdileri ve ciktilari etkili bir sekilde kullanmak icin evrim gecirecektir.

## En Iyi Uygulamalar ve Deneyler

Yetenekli bir prompt muhendisi olmak, surekli ogrenme ve deney iceren yinelemeli bir surecdir. Vurgulanmaya ve yinelennmeye deger birkac degerli en iyi uygulama sunlardir:

* **Ornekler Saglayin:** Bir veya birden fazla ornek saglamak (one veya few-shot), modeli yonlendirmenin en etkili yollarindan biridir.
* **Basitlikle Tasarlayin:** Prompt'larinizi kisa, net ve anlasilir tutun. Gereksiz jargon veya asiri karmasik ifadelerden kacinin.
* **Cikti Hakkinda Spesifik Olun:** Modelin yanitinin istenen formatini, uzunlugunu, tarzini ve icerigini acikca tanimlayin.
* **Kisitlamalar Yerine Talimatlar Kullanin:** Modele ne yapmamasini degil, ne yapmasini istediginizi soylemeye odaklanin.
* **Maksimum Token Uzunlugunu Kontrol Edin:** Uretilen ciktinin uzunlugunu yonetmek icin model yapilandirmalarini veya acik prompt talimatlarini kullanin.
* **Prompt'larda Degiskenler Kullanin:** Uygulamalarda kullanilan prompt'lar icin, belirli degerleri sert kodlamaktan kacinarak dinamik ve yeniden kullanilabilir yapmak icin degiskenler kullanin.
* **Girdi Formatlari ve Yazim Tarzlariyla Deney Yapin:** Prompt'unuzu farkli sekillerde ifade etmeyi (soru, ifade, talimat) deneyin ve en iyi sonuclari elde etmek icin farkli tonlar veya tarzlarla deney yapin.
* **Siniflandirma Gorevlerinde Few-Shot Prompt Icin Siniflari Karistirin:** Asiri uyumu onlemek icin farkli kategorilerden orneklerin sirasini rastgele hale getirin.
* **Model Guncellemelerine Uyum Saglayin:** Dil modelleri surekli guncellenntedir. Mevcut prompt'larinizi yeni model versiyonlarinda test etmeye ve yeni yeteneklerden yararlanmak veya performansi korumak icin ayarlamaya hazir olun.
* **Cikti Formatlariyla Deney Yapin:** Ozellikle yaratici olmayan gorevler icin, JSON veya XML gibi yapilandirilmis cikti istemeyi deneyin.
* **Diger Prompt Muhendisleriyle Birlikte Deney Yapin:** Baskalariyla is birligi yapmak farkli bakis acilari saglayabilir ve daha etkili prompt'lar kesfetmeye yol acabilir.
* **CoT En Iyi Uygulamalari:** Chain of Thought icin belirli uygulamalari unutmayin; ornegin cevabi akil yurutmeden sonra yerlestirmek ve tek bir dogru cevabi olan gorevler icin sicakligi 0'a ayarlamak gibi.
* **Cesitli Prompt Denemelerini Belgeleyin:** Bu, neyin ise yaradigini, neyin yaramadigini ve nedenini izlemek icin kritik oneme sahiptir. Prompt'larinizin, yapilandirmalarinizin ve sonuclarinizin yapilandirilmis bir kaydini tutun.
* **Prompt'lari Kod Tabanlarinda Kaydedin:** Prompt'lari uygulamalara entegre ederken, daha kolay bakim ve versiyon kontrolu icin bunlari ayri, iyi duzenlenmis dosyalarda saklayin.
* **Otomatik Testlere ve Degerlendirmeye Guvenin:** Uretim sistemleri icin, prompt performansini izlemek ve yeni verilere genellemeyi saglamak icin otomatik testler ve degerlendirme prosedurleri uygulayin.

Prompt muhendisligi pratikle gelisen bir beceridir. Bu ilkeleri ve teknikleri uygulayarak ve deney ile belgelemeye sistematik bir yaklasim surdurereek, etkili agentic sistemler olusturma becerinizi onemli olcude gelistirebilirsiniz.

## Sonuc

Bu ek, prompt'u basit bir soru sorma eylemi yerine disiplinli bir muhendislik pratiigi olarak yeniden cerceveleyerek kapsamli bir genel bakis sunmaktadir. Temel amaci, genel amacli dil modellerini belirli gorevler icin uzmanlasmis, guvenilir ve son derece yetenekli araclara nasil donusturulebileceeeini gostermektir. Yolculuk, etkili yapay zeka iletisiminin temeli olan netlik, kisalik ve yinelemeli deney gibi vazgecilmez temel ilkelerle baslar. Bu ilkeler kritik oneme sahiptir cunku dogal dildeki yapisal belirsizligi azaltarak modelin olasiliksal ciktilarini tek, dogru niyete yonlendirmeye yardimci olur. Bu temel uzerine insa edilen zero-shot, one-shot ve few-shot prompt gibi temel teknikler, ornekler araciliyla beklenen davranisi gostermek icin temel yontemler olarak hizmet eder. Bu yontemler, degisen duzeylerde baglamsal rehberlik saglayarak modelin yanit tarzini, tonunu ve formatini guclu bir sekilde sekillendiirir. Sadece orneklerin otesinde, acik roller, sistem duzeyinde talimatlar ve net ayiricilarla prompt'larin yapilandirilmasi, model uzerinde ince ayarli kontrol icin onemli bir mimari katman saglar.

Bu tekniklerin onemi, karmasik, cok adimli operasyonlar icin gerekli kontrol ve guvenilirligi saglayan otonom agent'lar olusturma baglaminda en ust duzeye cikar. Bir agent'in etkili bir sekilde plan olusturup yurutebilmesi icin Chain of Thought ve Tree of Thoughts gibi gelismis akil yurutme kaliplarini kullanmasi gerekir. Bu sofistike yontemler, modeli mantiksal adimlarini dissal hale getirmeye, karmasik hedefleri sistematik olarak yonetilebilir alt gorevler dizisine ayirmaya zorlae. Tum agentic sistemin operasyonel guvenilirliigi, her bilesenin ciktisinin ongoreulelebilirligine dayanir. JSON gibi yapilandirilmis veri istemenin ve bunu Pydantic gibi araclarla programatik olarak dogrulamanin salt bir kolaylik degil, saglam otomasyon icin mutlak bir gereklilik olmasinin nedeni tam olarak budur. Bu disiplin olmadan, agent'in ic bilissel bilesenleri guvenilir bir sekilde iletisim kuramaz ve otomatik bir is akisi icinde felaketle sonuclanan basarisizliklara yol acar. Sonuc olarak, bu yapilandirma ve akil yurutme teknikleri, bir modelin olasiliksal metin uretimini bir agent icin deterministik ve guvenilir bir bilissel motora basariyla donusturenlerdir.

Dahasi, bu prompt'lar bir agent'a cevresnii algilama ve ona gore hareket etme konusundaki kritik yetenegi verenlerdir; dijital dusunce ile gercek dunya etkilesimi arasindaki kosulleri kapatir. ReAct ve yerel function calling gibi eylem odakli cerceveler, agent'in elleri olarak hizmet eden hayati mekanizmalardir ve ona araclari kullanma, API'leri sorgulama ve verileri manipule etme imkani tanir. Paralel olarak, Retrieval Augmented Generation (RAG) ve daha genis Baglam Muhendisligi disiplini gibi teknikler agent'in duyulari olarak islerv gorur. Harici bilgi tabanlarindan ilgili, gercek zamanli bilgileri aktif olarak alarak agent'in kararlarinin guncel, olgusal gerceklige dayali olmasini saglar. Bu kritik yetenek, agent'in statik ve potansiyel olarak guncelligini yitirmis egitim verileriyle sinirli kalacagi bir boslukta calirmasini onler. Bu tam prompt yelpazesine hakim olmak, genel amacli bir dil modelini basit bir metin uretecinden otonomi, farkindalik ve zeka ile karmasik gorevleri yerine getirebilen gercek anlamda sofistike bir agent'a yukselten kesin beceridir.

## Kaynaklar

Prompt muhendisligi tekniklerinin daha fazla okunmasi ve derinlemesine arastirilmasi icin kaynak listesi:

1. Prompt Engineering, [https://www.kaggle.com/whitepaper-prompt-engineering](https://www.kaggle.com/whitepaper-prompt-engineering)
2. Chain-of-Thought Prompting Elicits Reasoning in Large Language Models, [https://arxiv.org/abs/2201.11903](https://arxiv.org/abs/2201.11903)
3. Self-Consistency Improves Chain of Thought Reasoning in Language Models,  [https://arxiv.org/pdf/2203.11171](https://arxiv.org/pdf/2203.11171)
4. ReAct: Synergizing Reasoning and Acting in Language Models, [https://arxiv.org/abs/2210.03629](https://arxiv.org/abs/2210.03629)
5. Tree of Thoughts: Deliberate Problem Solving with Large Language Models,  [https://arxiv.org/pdf/2305.10601](https://arxiv.org/pdf/2305.10601)
6. Take a Step Back: Evoking Reasoning via Abstraction in Large Language Models, [https://arxiv.org/abs/2310.06117](https://arxiv.org/abs/2310.06117)
7. DSPy: Programming—not prompting—Foundation Models [https://github.com/stanfordnlp/dspy](https://github.com/stanfordnlp/dspy)
