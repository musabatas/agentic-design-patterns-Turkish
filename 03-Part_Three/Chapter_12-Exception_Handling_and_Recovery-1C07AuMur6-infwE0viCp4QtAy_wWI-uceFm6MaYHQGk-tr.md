# Bolum 12: Hata Yonetimi ve Kurtarma (Exception Handling and Recovery)

Yapay zeka agent'larinin cesitli gercek dunya ortamlarinda guvenilir bir sekilde calisabilmesi icin, onceden ongoremedikleri durumlari, hatalari ve arizalari yonetebilmeleri gerekir. Insanlarin beklenmedik engellerle karsilastiginda uyum saglamasi gibi, akilli agent'larin da sorunlari tespit etmek, kurtarma prosedurlerini baslatmak veya en azindan kontrollü bir basarisizlik saglamak icin saglam sistemlere ihtiyaci vardir. Bu temel gereksinim, Hata Yonetimi ve Kurtarma (Exception Handling and Recovery) kalibinin temelini olusturur.

Bu kalip, cesitli zorluklar ve anormallikler karsisinda kesintisiz islevsellik ve operasyonel butunluk saglayabilen son derece dayanikli ve direncli agent'lar gelistirmeye odaklanir. Surekli calismayi saglamak icin hem proaktif hazirliklarin hem de reaktif stratejilerin onemini vurgular. Bu uyum yetenegini, agent'larin karmasik ve onceden kestirilemeyen ortamlarda basarili bir sekilde calismasi icin kritik oneme sahiptir ve sonuc olarak genel etkililiklerini ve guvenilirliklerini arttirir.

Beklenmedik olaylari yonetme kapasitesi, bu yapay zeka sistemlerinin yalnizca akilli degil, ayni zamanda kararli ve guvenilir olmasini saglar; bu da dagitim ve performanslarina duyulan guveni arttirir. Kapsamli izleme (Monitoring) ve tani araclarinin entegrasyonu, bir agent'in sorunlari hizla tespit etme ve cozme yetenegini daha da guclendirir, potansiyel aksakliklari onler ve degisen kosullarda daha sorunsuz calismayi saglar. Bu gelismis sistemler, yapay zeka operasyonlarinin butunlugunu ve verimliligi korumak, karmasiklik ve ongorulemeyen durumlari yonetme kapasitelerini pekistirmek icin buyuk onem tasir.

Bu kalip bazen yansitma (Reflection) ile birlikte kullanilabilir. Ornegin, ilk deneme basarisiz olur ve bir hata olusturur ise, yansitici bir surec basarisizligi analiz edebilir ve hatay cozmek icin iyilestirilmis bir prompt gibi rafine edilmis bir yaklasimla gorevi yeniden deneyebilir.

## Hata Yonetimi ve Kurtarma Kalibina Genel Bakis

Hata Yonetimi ve Kurtarma (Exception Handling and Recovery) kalibi, yapay zeka agent'larinin operasyonel basarisizliklari yonetme ihtiyacini ele alir. Bu kalip, arac hatalari veya hizmet kullanilamazligi gibi potansiyel sorunlari onceden tahmin etmeyi ve bunlari azaltmak icin stratejiler gelistirmeyi icerir. Bu stratejiler arasinda hata kaydi tutma (logging), yeniden deneme (retry), alternatif yontemler (fallback), kontrollü performans dusurme (graceful degradation) ve bildirimler yer alabilir. Ek olarak, kalip agent'lari kararli calisma durumuna geri dondurmek icin durum geri alma (state rollback), tani, kendi kendini duzeltme ve yukseltme (escalation) gibi kurtarma mekanizmalarini vurgular. Bu kalibin uygulanmasi, yapay zeka agent'larinin guvenilirligini ve saglamligini artirarak onceden kestirilemeyen ortamlarda calisabilmelerini saglar. Pratik uygulama ornekleri arasinda veritabani hatalariyla basa cikan sohbet botlari, finansal hatalarla ilgilenen ticaret botlari ve cihaz arizalarini yoneten akilli ev agent'lari bulunur. Bu kalip, agent'larin karmasikliklar ve basarisizliklarla karsilasmasina ragmen etkili bir sekilde calismaya devam etmesini saglar.

![Key Components of Exception Handling and Recovery for AI agents](../assets/Key_Components_of_Exception_Handling_and_Recovery_for_AI_agents.png)

Sekil 1: Yapay zeka agent'lari icin hata yonetimi ve kurtarmanin temel bilesenleri

**Hata Tespiti:** Bu, operasyonel sorunlarin ortaya ciktigi anda titizlikle tanimlanmasini icerir. Bu; gecersiz veya bozuk arac ciktilari, 404 (Not Found) veya 500 (Internal Server Error) kodlari gibi belirli API hatalari, hizmetlerden veya API'lerden alisilmadik derecede uzun yanit sureleri ya da beklenen formatlardan sapan tutarsiz ve anlamsiz yanitlar seklinde ortaya cikabilir. Ayrica, daha proaktif anomali tespiti icin diger agent'lar veya ozellestirilmis izleme sistemleri tarafindan izleme uygulanabilir; bu da sistemin potansiyel sorunlari buyumeden once yakalamasini saglar.

**Hata Isleme**: Bir hata tespit edildikten sonra, dikkatle dusunulmus bir mudahale plani gereklidir. Bu, hata ayrintilerinin daha sonra hata ayiklama ve analiz icin kayitlara (log) titizlikle kaydedilmesini icerir. Eylemi veya istegi, bazen hafifce degistirilmis parametrelerle yeniden denemek, ozellikle gecici hatalar icin uygulanabilir bir strateji olabilir (retry). Alternatif stratejiler veya yontemler (fallback) kullanmak, en azindan bir miktar islevselligin korunmasini saglayabilir. Tam kurtarmanin hemen mumkun olmadigi durumlarda, agent en azindan bir miktar deger sunmak icin kismi islevsellik saglayabilir (graceful degradation). Son olarak, insan operatorleri veya diger agent'lari uyarmak, insan mudahalesi veya is birligi gerektiren durumlar icin kritik oneme sahip olabilir (bildirim).

**Kurtarma (Recovery):** Bu asama, bir hatadan sonra agent'i veya sistemi kararli ve calisir bir duruma geri dondurmekle ilgilidir. Bu, hatanin etkilerini geri almak icin son degisikliklerin veya islemlerin tersine cevirilmesini (state rollback) icerebilir. Hatanin nedeninin kapsamli bir sekilde arastirilmasi, tekrarlanmasini onlemek icin hayati onem tasir. Gelecekte ayni hatadan kacinmak icin agent'in planinin, mantigi veya parametrelerinin kendi kendini duzeltme mekanizmasi veya yeniden planlama sureci araciligiyla ayarlanmasi gerekebilir. Karmasik veya ciddi durumlarda, sorunu bir insan operatore veya daha ust duzey bir sisteme yukseltmek (escalation) en iyi hareket tarzi olabilir.

Bu saglam hata yonetimi ve kurtarma kalibinin uygulanmasi, yapay zeka agent'larini kirilgan ve guvenilmez sistemlerden, zorlu ve yuksek derecede onceden kestirilemeyen ortamlarda etkili ve direncli bir sekilde calisabilen saglam, guvenilir bilesenlere donusturebilir. Bu, agent'larin islevselligini surdurmesini, kesinti suresini en aza indirmesini ve beklenmedik sorunlarla karsilastiginda bile sorunsuz ve guvenilir bir deneyim sunmasini saglar.

## Pratik Uygulamalar ve Kullanim Alanlari

Hata Yonetimi ve Kurtarma (Exception Handling and Recovery), kusursuz kosullarin garanti edilemedigi gercek dunya senaryolarinda dagitilan her agent icin kritik oneme sahiptir.

* **Musteri Hizmetleri Sohbet Botlari:** Bir sohbet botu musteri veritabanina erismek istediginde veritabani gecici olarak kapaliysa, cokmemesi gerekir. Bunun yerine, API hatasini tespit etmeli, kullaniciyi gecici sorun hakkinda bilgilendirmeli, belki daha sonra tekrar denemesini onermeli veya sorguyu bir insan agent'a yukseltmelidir.
* **Otomatik Finansal Ticaret:** Bir islem gerceklestirmeye calisan ticaret botu "yetersiz bakiye" veya "piyasa kapali" hatasiyla karsilasabilir. Bu hatalari, hatay kaydederek, ayni gecersiz islemi tekrar tekrar denemeyerek ve potansiyel olarak kullaniciyi bilgilendirerek veya stratejisini ayarlayarak yonetmesi gerekir.
* **Akilli Ev Otomasyonu:** Akilli isiklari kontrol eden bir agent, bir ag sorunu veya cihaz arizasi nedeniyle bir isigi acamayabilir. Bu basarisizligi tespit etmeli, belki yeniden denemeli ve hala basarisiz olursa, kullaniciyi isigin acilamadigini bildirmeli ve manuel mudahale onermelidir.
* **Veri Isleme Agent'lari:** Bir belge yiginini isleme goreviyle gorevlendirilen bir agent, bozuk bir dosyayla karsilasabilir. Bozuk dosyayi atlamali, hatayi kaydetmeli, diger dosyalari islemeye devam etmeli ve tum sureci durdurmak yerine sonunda atlanan dosyalari raporlamalidir.
* **Web Kazima Agent'lari:** Bir web kazima agent'i CAPTCHA, degismis web sitesi yapisi veya sunucu hatasi (ornegin 404 Not Found, 503 Service Unavailable) ile karsilastiginda, bunlari kontrollü bir sekilde yonetmesi gerekir. Bu, duraklamayi, proxy kullanmayi veya basarisiz olan belirli URL'yi raporlamayi icerebilir.
* **Robotik ve Uretim:** Bir montaj gorevi gerceklestiren bir robotik kol, hatali hizalama nedeniyle bir bileseni alamayabilir. Bu basarisizligi tespit etmeli (ornegin sensor geri bildirimi araciligiyla), yeniden ayarlamayi denemeli, alma islemini tekrar denemeli ve sorun devam ederse bir insan operatoru uyarmali veya farkli bir bilesene gecmelidir.

Kisaca, bu kalip yalnizca akilli degil, ayni zamanda gercek dunyanin karmasikliklari karsisinda guvenilir, direncli ve kullanici dostu agent'lar olusturmak icin temel bir unsurdur.

## Uygulamali Kod Ornegi (ADK)

Hata yonetimi ve kurtarma, sistem saglamligi ve guvenilirligi icin hayati onem tasir. Ornegin, bir agent'in basarisiz bir arac cagrisina verdigi yaniti ele alalim. Bu tur basarisizliklar, yanlis arac girdisinden veya aracin bagimli oldugu harici bir hizmetle ilgili sorunlardan kaynaklanabilir.

```python
from google.adk.agents import Agent, SequentialAgent


# Agent 1: Birincil araci dener. Odagi dar ve nettir.
primary_handler = Agent(
    name="primary_handler",
    model="gemini-2.0-flash-exp",
    instruction="""
    Your job is to get precise location information. Use the get_precise_location_info
    tool with the user's provided address.
    """,
    tools=[get_precise_location_info],
)

# Agent 2: Fallback isleyicisi olarak hareket eder, eylemini belirlemek icin durumu kontrol eder.
fallback_handler = Agent(
    name="fallback_handler",
    model="gemini-2.0-flash-exp",
    instruction="""
    Check if the primary location lookup failed by looking at state["primary_location_failed"].
    - If it is True, extract the city from the user's original query and use the get_general_area_info tool.
    - If it is False, do nothing.
    """,
    tools=[get_general_area_info],
)

# Agent 3: Durumdan elde edilen nihai sonucu sunar.
response_agent = Agent(
    name="response_agent",
    model="gemini-2.0-flash-exp",
    instruction="""
    Review the location information stored in state["location_result"]. Present this information
    clearly and concisely to the user. If state["location_result"] does not exist or is empty,
    apologize that you could not retrieve the location.
    """,
    tools=[],  # This agent only reasons over the final state.
)

# SequentialAgent, isleyicilerin garantili bir sirada calismasini saglar.
robust_location_agent = SequentialAgent(
    name="robust_location_agent",
    sub_agents=[primary_handler, fallback_handler, response_agent],
)
```

Bu kod, ADK'nin SequentialAgent yapisini kullanarak uc alt agent'li saglam bir konum bilgisi erisim sistemi tanimlar. `primary_handler`, `get_precise_location_info` aracini kullanarak kesin konum bilgisi elde etmeye calisan ilk agent'tir. `fallback_handler`, birincil aramanin basarisiz olup olmadigini bir durum degiskenini kontrol ederek denetleyen yedek olarak gorev yapar. Birincil arama basarisiz olduysa, fallback agent'i kullanicinin sorgusundan sehri cikarir ve `get_general_area_info` aracini kullanir. `response_agent`, dizideki son agent'tir. Durumda saklanan konum bilgisini inceler. Bu agent, nihai sonucu kullaniciya sunmak icin tasarlanmistir. Konum bilgisi bulunamazsa, ozur diler. SequentialAgent, bu uc agent'in onceden tanimlanmis bir sirada calistirilmasini saglar. Bu yapi, konum bilgisi erisimi icin katmanli bir yaklasim olanagi tanir.

## Bir Bakista

**Ne:** Gercek dunya ortamlarinda calisan yapay zeka agent'lari kacilmaz olarak onceden gorulemeyen durumlar, hatalar ve sistem arizalariyla karsilasir. Bu aksakliklar, arac basarisizliklarindan ve ag sorunlarindan gecersiz verilere kadar uzanabilir ve agent'in gorevlerini tamamlama yetenegini tehdit eder. Bu sorunlari yonetmek icin yapisal bir yol olmadan, agent'lar kirilgan, guvenilmez ve beklenmedik engellerle karsilastiginda tamamen basarisiz olmaya yatkin olabilir. Bu guvenilmezlik, tutarli performansin gerekli oldugu kritik veya karmasik uygulamalarda onlari dagitmayi zorlastirir.

**Neden:** Hata Yonetimi ve Kurtarma (Exception Handling and Recovery) kalibi, saglam ve direncli yapay zeka agent'lari olusturmak icin standartlastirilmis bir cozum sunar. Agent'lari operasyonel basarisizliklari onceden tahmin etme, yonetme ve bunlardan kurtulma konusunda agentic yetenekle donatir. Kalip, arac ciktilarini ve API yanitlarini izleme gibi proaktif hata tespitini ve tani icin kayit tutma, gecici basarisizliklari yeniden deneme veya fallback mekanizmalarini kullanma gibi reaktif isleme stratejilerini icerir. Daha ciddi sorunlar icin, kararli bir duruma geri donme, planini ayarlayarak kendi kendini duzeltme veya sorunu bir insan operatore yukseltme dahil olmak uzere kurtarma protokolleri tanimlar. Bu sistematik yaklasim, agent'larin operasyonel butunlugu korumalarini, basarisizliklardan ders cikarmalarini ve onceden kestirilemeyen ortamlarda guvenilir bir sekilde calismalarini saglar.

**Temel Kural:** Bu kalibi, sistem basarisizliklari, arac hatalari, ag sorunlari veya onceden kestirilemeyen girdilerin mumkun oldugu ve operasyonel guvenilirligin temel bir gereksinim oldugu dinamik, gercek dunya ortamlarinda dagitilan herhangi bir yapay zeka agent'i icin kullanin.

**Gorsel Ozet:**

![Exception Handling Pattern](../assets/Exception_Handling_Pattern.png)

Sekil 2: Hata yonetimi kalibi

## Temel Cikarimlar

Hatirlanmasi gereken temel noktalar:

* Hata Yonetimi ve Kurtarma (Exception Handling and Recovery), saglam ve guvenilir agent'lar olusturmak icin vazgecilmezdir.
* Bu kalip, hatalari tespit etmeyi, bunlari kontrollü bir sekilde yonetmeyi ve kurtarma stratejileri uygulamayi icerir.
* Hata tespiti; arac ciktilarini dogrulama, API hata kodlarini kontrol etme ve timeout'lari kullanma gibi yontemleri icerebilir.
* Isleme stratejileri arasinda kayit tutma (logging), yeniden deneme (retry), alternatif yontemler (fallback), kontrollü performans dusurme (graceful degradation) ve bildirimler yer alir.
* Kurtarma (Recovery), tani, kendi kendini duzeltme veya yukseltme (escalation) yoluyla kararli calismanin yeniden saglanmasina odaklanir.
* Bu kalip, agent'larin onceden kestirilemeyen gercek dunya ortamlarinda bile etkili bir sekilde calismalarini saglar.

## Sonuc

Bu bolum, saglam ve guvenilir yapay zeka agent'lari gelistirmek icin vazgecilmez olan Hata Yonetimi ve Kurtarma (Exception Handling and Recovery) kalibini incelemektedir. Bu kalip, yapay zeka agent'larinin beklenmedik sorunlari nasil tanimlayip yonetebilecegini, uygun yanitlari nasil uygulayabilecegini ve kararli bir calisma durumuna nasil geri donebilecegini ele alir. Bolumde bu kalibin cesitli yonleri tartislir: hatalarin tespiti, kayit tutma (logging), yeniden deneme (retry) ve alternatif yontemler (fallback) gibi mekanizmalar araciligiyla bu hatalarin islenmesi ve agent'i veya sistemi uygun islevine kavusturmak icin kullanilan stratejiler. Hata Yonetimi ve Kurtarma kalibinin pratik uygulamalari, gercek dunya karmasikliklari ve potansiyel basarisizliklarla basa cikmadaki ilgisini gostermek icin cesitli alanlardan orneklendirilmistir. Bu uygulamalar, yapay zeka agent'larini hata yonetimi yetenekleriyle donatmanin, dinamik ortamlarda guvenilirlikleri ve uyum saglamalarina nasil katkida bulundugunu gostermektedir.

## Kaynaklar

1. McConnell, S. (2004). *Code Complete (2nd ed.)*. Microsoft Press.
2. Shi, Y., Pei, H., Feng, L., Zhang, Y., & Yao, D. (2024). *Towards Fault Tolerance in Multi-Agent Reinforcement Learning*. arXiv preprint arXiv:2412.00534.
3. O'Neill, V. (2022). *Improving Fault Tolerance and Reliability of Heterogeneous Multi-Agent IoT Systems Using Intelligence Transfer*. Electronics, 11(17), 2724.
