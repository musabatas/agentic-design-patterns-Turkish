# Bolum 10: Model Context Protocol

LLM'lerin agent olarak etkili bir sekilde calisabilmesi icin yeteneklerinin multimodal icerik uretiminin otesine gecmesi gerekir. Guncel verilere erisim, harici yazilimlarin kullanimi ve belirli operasyonel gorevlerin yurutulmesi dahil olmak uzere dis cevre ile etkilesim gereklidir. Model Context Protocol (MCP), LLM'lerin harici kaynaklarla arayuz olusturmasi icin standartlastirilmis bir arayuz saglayarak bu ihtiyaci karsilar. Bu protokol, tutarli ve onceden tahmin edilebilir entegrasyonu kolaylastirmak icin temel bir mekanizma gorevi gorur.

## MCP Kalibina Genel Bakis

Herhangi bir LLM'in, her biri icin ozel bir entegrasyon gerektirmeden herhangi bir harici sisteme, veritabanina veya araca baglanmasini saglayan evrensel bir adaptor hayal edin. Model Context Protocol (MCP) temelde budur. Gemini, OpenAI'nin GPT modelleri, Mixtral ve Claude gibi LLM'lerin harici uygulamalar, veri kaynaklari ve araclarla nasil iletisim kurdugunu standartlastirmak icin tasarlanmis acik bir standdarttir. LLM'lerin baglam elde etme, eylem yurutme ve cesitli sistemlerle etkilesim kurma seklini basitlestiren evrensel bir baglanti mekanizmasi olarak dusunulebilir.

MCP, bir istemci-sunucu (client-server) mimarisi uzerinde calisir. Farkli ogelerin -- veri (resource olarak adlandirilir), etkilesimli sablonlar (esasen prompt'lar) ve eyleme donusturulebilir fonksiyonlar (tool olarak bilinir) -- bir MCP sunucusu tarafindan nasil sunuldugunu tanimlar. Bunlar daha sonra bir LLM ana uygulamasi veya bir yapay zeka agent'inin kendisi olabilen bir MCP istemcisi tarafindan tuketilir. Bu standartlastirilmis yaklasim, LLM'lerin cesitli operasyonel ortamlara entegrasyonunun karmasikligini onemli olcude azaltir.

Ancak MCP, bir "agentic arayuz" icin bir sozlesmedir ve etkinligi buyuk olcude sundugu temel API'lerin tasarimina baglidir. Gelistiricilerin mevcut eski API'leri degisiklik yapmadan basitce sarmalamalari riski vardir ki bu, bir agent icin optimal olmayabilir. Ornegin, bir bilet sisteminiin API'si yalnizca tam bilet ayrintilairini birer birer almaya izin veriyorsa, yuksek oncelikli biletleri ozetlemesi istenen bir agent yuksek hacimlerde yavas ve yanlis olacaktir. Gercekten etkili olmasi icin, temel API, deterministik olmayan agent'in verimli calismasina yardimci olmak icin filtreleme ve siralama gibi deterministik ozelliklerle iyilestirilmelidir. Bu, agent'larin deterministik is akislarini sihirli bir sekilde degistirmedigini; genellikle basarili olmak icin daha guclu deterministik destege ihtiyac duydugunu vurgular.

Dahasi, MCP, giris veya ciktisi agent tarafindan dogal olarak anlasilamayan bir API'yi sarmalayabilir. Bir API yalnizca veri formati agent dostu ise faydalidir ve MCP'nin kendisi bu garantiyi vermez. Ornegin, dosyalari PDF olarak donduren bir belge deposu icin bir MCP sunucusu olusturmak, tuketici agent PDF icerigini ayristiramazsa buyuk olcude isesizdir. Daha iyi yaklasim, oncelikle agent'in gercekten okuyup isleyebilecegi Markdown gibi bir metin surumu donduren bir API olusturmak olacaktir. Bu, gelistiricilerin gercek uyumlulugu saglamak icin yalnizca baglantiya degil, alisverisi yapilan verinin dogasina da dikkat etmesi gerektigini gostermektedir.

## MCP ile Tool Function Calling Karsilastirmasi

Model Context Protocol (MCP) ve tool function calling, LLM'lerin harici yeteneklerle (araclar dahil) etkilesim kurmasini ve eylemler yurutmesini saglayan farkli mekanizmalardir. Her ikisi de LLM yeteneklerini metin uretiminin otesine genisletmeye hizmet etse de, yaklasimlari ve soyutlama duzeyleri bakimindan farklilasir.

Tool function calling, bir LLM'den belirli, onceden tanimlanmis bir araca veya fonksiyona yapilan dogrudan bir istek olarak dusunulebilir. Bu baglamda "arac" ve "fonksiyon" kelimelerini birbirinin yerine kullandigimizi belirtelim. Bu etkilesim, LLM'in harici eylem gerektiren bir kullanicinin niyetini anlayisina dayali olarak bir istegi bicimlendirdigi bire bir iletisim modeliyle karakterize edilir. Uygulama kodu daha sonra bu istegi yurutur ve sonucu LLM'e dondurur. Bu surec genellikle tescilli (proprietary) olup farkli LLM saglayicilari arasinda degisiklik gosterir.

Buna karsilik, Model Context Protocol (MCP), LLM'lerin harici yetenekleri kesfetmesi, bunlarla iletisim kurmasi ve kullanmasi icin standartlastirilmis bir arayuz olarak calisiir. Genis bir yelpazedeki araclar ve sistemlerle etkilesimi kolaylastiran acik bir protokol olarak isler ve uyumlu herhangi bir aracin uyumlu herhangi bir LLM tarafindan erisilebilecegi bir ekosistem olusturmayi amaclar. Bu, farkli sistemler ve uygulamalar arasinda birlikte calisabilirlik (interoperability), birlestirilebilirlik (composability) ve yeniden kullanilabilirlik (reusability) saglar. Federatif bir model benimseyerek, birlikte calisabilirligi onemli olcude iyilestirir ve mevcut varliklarin degerini aciga cikariz. Bu strateji, daginik ve eski hizmetleri basitce MCP uyumlu bir arayuzle sarmalayarak modern bir ekosisteme dahil etmemize olanak tanir. Bu hizmetler bagimsiz olarak calismaaya devam eder, ancak artik yeni uygulamalar ve is akislarina dahil edilebilir ve is birliklerinin LLM'ler tarafindan duzenlenebilmesiyle ceviklik ve yeniden kullanilabilirlik saglanir; temel sistemlerin maliyetli yeniden yazilmalari gerekmez.

MCP ile tool function calling arasindaki temel farklarin bir dokumu asagida verilmistir:

| Ozellik | Tool Function Calling | Model Context Protocol (MCP) |
| ----- | ----- | ----- |
| **Standartlasma** | Tescilli ve satici bazinda ozeldir. Format ve uygulama LLM saglayicilari arasinda farklilik gosterir. | Acik, standartlastirilmis bir protokol; farkli LLM'ler ve araclar arasinda birlikte calisabilirliigi tesvik eder. |
| **Kapsam** | Bir LLM'in belirli, onceden tanimlanmis bir fonksiyonun yurutulmesini istemesi icin dogrudan bir mekanizma. | LLM'ler ve harici araclarin birbirini kesfetmesi ve iletisim kurmasi icin daha genis bir framework. |
| **Mimari** | LLM ile uygulamanin arac islem mantigi arasinda bire bir etkilesim. | LLM destekli uygulamalarin (istemciler) cesitli MCP sunucularina (araclar) baglanabilecegi ve kullanabilecegi bir istemci-sunucu mimarisi. |
| **Kesfedilebilirlik** | LLM'e belirli bir konusma baglaminda hangi araclarin mevcut oldugu acikca bildirilir. | Mevcut araclarin dinamik kesfini mumkun kilar. Bir MCP istemcisi, hangi yetenekleri sundugunu gormek icin bir sunucuyu sorgulayabilir. |
| **Yeniden Kullanilabilirlik** | Arac entegrasyonlari genellikle kullanilan belirli uygulama ve LLM ile sikica baglantilidirr. | Uyumlu herhangi bir uygulama tarafindan erisilebilen yeniden kullanilabilir, bagimsiz "MCP sunuculari"nin gelistirilmesini tesvik eder. |

Tool function calling'i bir yapay zekaya belirli bir takim ozel yapim arac -- belirli bir anahtar ve tornavida gibi -- vermek olarak dusunun. Bu, sabit bir gorev setine sahip bir atolye icin verimlidir. MCP (Model Context Protocol) ise evrensel, standartlastirilmis bir priz sistemi olusturmak gibidir. Araclarin kendisini saglamaz, ancak herhangi bir ureticiden uyumlu herhangi bir aracin takiilip calissmasina olanak taniyarak dinamik ve surekli genisleyen bir atolye mumkun kilar.

Kisacasi, function calling birkac belirli fonksiyona dogrudan erisim saglarken, MCP LLM'lerin genis bir harici kaynak yelpazesini kesfetmesine ve kullanmasina olanak taniyan standartlastirilmis iletisim framework'udur. Basit uygulamalar icin belirli araclar yeterlidir; uyum saglamasi gereken karmasik, birbirine bagli yapay zeka sistemleri icin MCP gibi evrensel bir standart vazgecilmezdir.

## MCP Icin Ek Degerlendirmeler

MCP guclu bir framework sunsa da, kapsamli bir degerlendirme, belirli bir kullanim alani icin uygunlugunu etkileyen birkac kritik yonu dikkate almayi gerektirir. Bazi yonleri daha ayrintili inceleyelim:

* **Tool, Resource ve Prompt Ayrimi**: Bu bilesenlerin belirli rollerini anlamak onemlidir. Bir resource statik veridir (ornegin bir PDF dosyasi, bir veritabani kaydi). Bir tool, bir eylem gerceklestiren yurtulebilir bir fonksiyondur (ornegin e-posta gonderme, bir API'yi sorgulama). Bir prompt, LLM'i bir resource veya tool ile nasil etkilesime gecegiii konusunda yonlendiren, etikelesimin yapilandirilmis ve etkili olmasini saglayan bir sablondur.
* **Kesfedilebilirlik (Discoverability)**: MCP'nin temel bir avantaji, bir MCP istemcisinin hangi araclari ve kaynaklari sundugunu ogrenmek icin bir sunucuyu dinamik olarak sorgulayabilmesidir. Bu "tam zamaninda" kesfetme mekanizmasi, yeniden dagitilmadan yeni yeteneklere uyum saglamasi gereken agent'lar icin gucludur.
* **Guvenlik (Security)**: Herhangi bir protokol araciligiyla araclari ve verileri aciga cikarmak saglam guvenlik onlemleri gerektirir. Bir MCP uygulamasi, hangi istemcilerin hangi sunuculara erisebilecegini ve hangi belirli eylemleri gerceklesitirmelerine izin verildigini kontrol etmek icin kimlik dogrulama ve yetkilendirme icermelidir.
* **Uygulama (Implementation)**: MCP acik bir standart olmasina ragmen uygulanmasi karmasik olabilir. Ancak saglayicilar bu sureci basitlestirmeye baslamistir. Ornegin Anthropic veya FastMCP gibi bazi model saglayicilari, gelistiricilerin MCP istemcileri ve sunuculari olusturmasini ve baglamasini kolaylastiran, standart kodun buyuk bolumunu soyutlayan SDK'lar sunar.
* **Hata Yonetimi (Error Handling)**: Kapsamli bir hata yonetimi stratejisi kritiktir. Protokol, hatalarin (ornegin arac yurutme basarisizligi, kullanilamayan sunucu, gecersiz istek) LLM'e nasil iletilecegini tanimlayarak onun basarisizligi anlamasini ve potansiyel olarak alternatif bir yaklasim denemesini saglamalidir.
* **Yerel ve Uzak Sunucu**: MCP sunuculari, agent ile ayni makinede yerel olarak veya farkli bir sunucuda uzaktan konusllandirilabilir. Hiz ve hassas verilerle guvenlik icin yerel bir sunucu tercih edilebilirken, uzak bir sunucu mimarisi bir organizasyon genelinde ortak araclara paylasiilan, olceklenebilir erisim saglar.
* **Talep Uzerine ve Toplu Isleme (On-demand vs. Batch)**: MCP, hem talep uzerine, etkilesimli oturumlari hem de daha buyuk olcekli toplu islemeyi destekleyebilir. Secim uygulamaya baglidir; anlik arac erisimi gerektiren gercek zamanli bir konusma agent'indan kayitlari toplu olarak isleyen bir veri analizi pipeline'ina kadar degisir.
* **Tasiima Mekanizmasi (Transportation Mechanism)**: Protokol ayrica iletisim icin temel aktarim katmanlarini da tanimlar. Yerel etkilesimler icin verimli sureclerer arasi iletisim saglamak uzere STDIO (standart giris/cikis) uzerinden JSON-RPC kullanir. Uzak baglantilar icin kalici ve verimli istemci-sunucu iletisimini mumkun kilmak icin Streamable HTTP ve Server-Sent Events (SSE) gibi web dostu protokollerden yararlanir.

Model Context Protocol, bilgi akisini standartlastirmak icin bir istemci-sunucu modeli kullanir. MCP'nin gelismis agentic davranislarini anlamak icin bilesen etkilesimini kavramak onemlidir:

1. **Buyuk Dil Modeli (LLM)**: Temel zeka. Kullanici isteklerini isler, planlar olusturur ve harici bilgiye erismesi veya bir eylem gerceklestirmesi gerekip gerekmedggine karar verir.
2. **MCP Istemcisi (MCP Client)**: LLM etrafindaki bir uygulama veya sarmalayicidir. LLM'in niyetini MCP standardina uygun resmi bir istege donusturen araci gorevi gorur. MCP Sunucularin kesfedilmesinden, baglanilmasindan ve iletisim kurulmasindan sorumludur.
3. **MCP Sunucusu (MCP Server)**: Dis dunyaya acilan kapdir. Yetkili herhangi bir MCP Istemcisine bir dizi tool, resource ve prompt sunar. Her sunucu tipik olarak belirli bir alandan sorumludur; ornegin bir sirketin dahili veritabanina baglanti, bir e-posta hizmeti veya genel bir API.
4. **Opsiyonel Ucuncu Taraf (3P) Hizmeti:** MCP Sunucusunun yonettigi ve sundugu gercek harici araci, uygulamayi veya veri kaynagini temsil eder. Istenen eylemi gerceklestiren nihai uc noktadir; ornegin tescilli bir veritabanini sorgulamak, bir SaaS platformuyla etkilesim kurmak veya genel bir hava durumu API'sini cagirmak.

Etkilesim akisi su sekildedir:

1. **Kesfetme (Discovery)**: MCP Istemcisi, LLM adina bir MCP Sunucusunu hangi yetenekleri sundugunu sormak icin sorgular. Sunucu, mevcut tool'larini (ornegin send_email), resource'larini (ornegin customer_database) ve prompt'larini listeleyen bir manifest ile yanit verir.
2. **Istek Formullasyonu (Request Formulation)**: LLM, kesfedilen tool'lardan birini kullanmasi gerektigine karar verir. Ornegin bir e-posta gondermeye karar verir. Kullanilacak araci (send_email) ve gerekli parametreleri (alici, konu, govde) belirterek bir istek formule eder.
3. **Istemci Iletisimi (Client Communication)**: MCP Istemcisi, LLM'in formule ettigi istegi alir ve uygun MCP Sunucusuna standartlastirilmis bir cagri olarak gonderir.
4. **Sunucu Yurutmesi (Server Execution)**: MCP Sunucusu istegi alir. Istemciyi dogrular, istegi gecerlilik kontrolune tabi tutar ve ardindan temeldeki yazilimla arayuz olusturarak (ornegin bir e-posta API'sinin send() fonksiyonunu cagirarak) belirtilen eylemi yurutur.
5. **Yanit ve Baglam Guncellemesi (Response and Context Update)**: Yurutmeden sonra MCP Sunucusu, MCP Istemcisine standartlastirilmis bir yanit gonderir. Bu yanit, eylemin basarili olup olmadigini gosterir ve ilgili ciktiyi (ornegin gonderilen e-posta icin bir onay kimligi) icerir. Istemci daha sonra bu sonucu LLM'e ileterek baglamini gunceller ve gorevinin bir sonraki adimina gecmesini saglar.

## Pratik Uygulamalar ve Kullanim Alanlari

MCP, yapay zeka/LLM yeteneklerini onemli olcude genisleterek onlari daha cok yonlu ve guclu hale getirir. Iste dokuz temel kullanim alani:

* **Veritabani Entegrasyonu:** MCP, LLM'lerin ve agent'larin veritabanlarindaki yapilandirilmis verilerle sorunsuz bir sekilde etkeilsim kurmasini saglar. Ornegin, MCP Toolbox for Databases kullanarak bir agent, gercek zamanli bilgi almak, raporlar olusturmak veya kayitlari guncellemek icin Google BigQuery veri kumelerini sorgulayabilir; tumU dogal dil komutlariyla.
* **Uretici Medya Orkestrasyonu:** MCP, agent'larin gelismis uretici medya hizmetleriyle entegre olmasini saglar. MCP Tools for Genmedia Services araciligiyla bir agent, yapay zeka uygulamalari icerisinde dinamik icerik olusturmak icin goruntu uretimi icin Google Imagen, video olusturma icin Google Veo, gercekci sesler icin Google Chirp 3 HD veya muzik bestesi icin Google Lyria icereen is akislari duzenleyebilir.
* **Harici API Etkilesimi:** MCP, LLM'lerin herhangi bir harici API'yi cagirmasi ve yanitlar almasi icin standartlastirilmis bir yol saglar. Bu, bir agent'in canli hava durumu verisi alabilecegi, hisse senedi fiyatlarini cekebilecegi, e-posta gonderebilecegi veya CRM sistemleriyle etkilesime girebilecegi anlamina gelir; yeteneklerini temel dil modelinin cok otesine genisletir.
* **Akil Yurutme Tabanli Bilgi Cikarimi:** Bir LLM'in guclu akil yurutme (reasoning) becerilerinden yararlanan MCP, geleneksel arama ve erisim sistemlerini asan etkili, sorguya bagimli bilgi cikarimini kolaylastirir. Geleneksel bir arama aracinin tum belgeyi dondurmmesi yerine, agent metni analiz edebilir ve bir kullanicinin karmasik sorusunu dogrudan yanitlayan kesin maddeyi, sekli veya ifadeyi cikarabilir.
* **Ozel Arac Gelistirme:** Gelistiriciler ozel araclar olusturabilir ve bunlari bir MCP sunucusu araciligiyla (ornegin FastMCP kullanarak) sunabilir. Bu, ozellestirilmis dahili fonksiyonlarin veya tescilli sistemlerin, LLM'i dogrudan degistirmeye gerek kalmadan standartlastirilmis, kolay tuketilebilir bir formatta LLM'lere ve diger agent'lara sunulmasini saglar.
* **LLM-Uygulama Arasi Standartlastirilmis Iletisim:** MCP, LLM'ler ile etkilesimde bulunduklari uygulamalar arasinda tutarli bir iletisim katmani saglar. Bu, entegrasyon yukunu azaltir, farkli LLM saglayicilari ve ana uygulamalar arasinda birlikte calisabilirliigi tesvik eder ve karmasik agentic sistemlerin gelistirilmesini basitlesitirir.
* **Karmasik Is Akisi Orkestrasyonu:** Cesitli MCP ile sunulan araclar ve veri kaynaklarini birleistirerek agent'lar son derece karmasik, cok adimli is akislari duzenleyebilir. Bir agent, ornegin bir veritabanindan musteri verilerini alabilir, kisisellesitirilmis bir pazarlama gorseli olusturabilir, ozellestirilmis bir e-posta taslagi hazirrlayabilir ve ardindan bunu gonderebilir; tumU farkli MCP hizmetleriyle etkilesim kurarak.
* **IoT Cihaz Kontrolu:** MCP, LLM'in Nesnelerin Interneti (IoT) cihazlariyla etkilesimini kolaylastirabilir. Bir agent, akilli ev cihazlarina, endustriyel sensorlere veya robotlara komutlar gondermek icin MCP kullanabilir ve fiziksel sistemlerin dogal dil kontrolunu ve otomasyonunu mumkun kilar.
* **Finansal Hizmetler Otomasyonu:** Finansal hizmetlerde MCP, LLM'lerin cesitli finansal veri kaynaklari, ticaret platformlari veya uyumluluk sistemleriyle etkilesim kurmasini saglayabilir. Bir agent, piyasa verilerini analiz edebilir, islem gerceklestirebilir, kisisellesitirilmis finansal tavsiyeler uretebilir veya duzenleyici raporlamayi otomatiklestirebilir; tumU guvenli ve standartlastirilmis iletisimi surduurerek.

Kisacasi, Model Context Protocol (MCP), agent'larin veritabanlari, API'lar ve web kaynaklarindan gercek zamanli bilgiye erismesini saglar. Ayrica agent'larin e-posta gonderme, kayitlari guncelleme, cihazlari kontrol etme ve cesitli kaynaklardan verileri entegre edip isleyerek karmasik gorevleri yurutmesine olanak tanir. Ek olarak MCP, yapay zeka uygulamalari icin medya uretim araclarini destekler.

## ADK ile Uygulamali Kod Ornegi

Bu bolum, dosya sistemi islemleri saglayan yerel bir MCP sunucusuna nasil baglanilacagini ve bir ADK agent'inin yerel dosya sistemiyle etkilesim kurmasinin nasil saglanacagini aciklamaktadir.

### MCPToolset ile Agent Kurulumu

Dosya sistemi etkilesimi icin bir agent yapilandirmak uzere bir `agent.py` dosyasi olusturulmelidir (ornegin `./adk_agent_samples/mcp_agent/agent.py` konumunda). `MCPToolset`, `LlmAgent` nesnesinin `tools` listesi icinde olusturulur. `args` listesindeki `"/path/to/your/folder"` ifadesinin, MCP sunucusunun erisebilecegi yerel sistemdeki bir dizinin mutlak yolu ile degistirilmesi kritik oneme sahiptir. Bu dizin, agent tarafindan gerceklestirilen dosya sistemi islemleri icin kok olacaktir.

```python
import os

from google.adk.agents import LlmAgent
from google.adk.tools.mcp_tool.mcp_toolset import MCPToolset, StdioServerParameters


# Create a reliable absolute path to a folder named 'mcp_managed_files'
# within the same directory as this agent script.
# This ensures the agent works out-of-the-box for demonstration.
# For production, you would point this to a more persistent and secure location.
TARGET_FOLDER_PATH = os.path.join(
    os.path.dirname(os.path.abspath(__file__)),
    "mcp_managed_files",
)

# Ensure the target directory exists before the agent needs it.
os.makedirs(TARGET_FOLDER_PATH, exist_ok=True)

root_agent = LlmAgent(
    model="gemini-2.0-flash",
    name="filesystem_assistant_agent",
    instruction=(
        "Help the user manage their files. You can list files, read files, and write files. "
        f"You are operating in the following directory: {TARGET_FOLDER_PATH}"
    ),
    tools=[
        MCPToolset(
            connection_params=StdioServerParameters(
                command="npx",
                args=[
                    "-y",  # Argument for npx to auto-confirm install
                    "@modelcontextprotocol/server-filesystem",
                    # This MUST be an absolute path to a folder.
                    TARGET_FOLDER_PATH,
                ],
            ),
            # Optional: You can filter which tools from the MCP server are exposed.
            # For example, to only allow reading:
            # tool_filter=['list_directory', 'read_file']
        )
    ],
)
```

npm (Node Package Manager) 5.2.0 ve sonraki surumlerle birlikte gelen `npx` (Node Package Execute), npm kayit defterinden Node.js paketlerinin dogrudan calistirilmasini saglayan bir yardimci programdir. Bu, global kurulum ihtiyacini ortadan kaldirir. Esasen `npx` bir npm paket calistiricidir ve Node.js paketleri olarak dagitilan bircok topluluk MCP sunucusunu calistirmak icin yaygin olarak kullanilir.

Agent Development Kit (ADK) icin agent.py dosyasinin kesfedilebilir bir Python paketi olarak taninmasini saglamak icin bir `__init__.py` dosyasi olusturmak gereklidir. Bu dosya, [agent.py](http://agent.py) ile ayni dizinde bulunmalidir.

```python
# ./adk_agent_samples/mcp_agent/__init__.py
from . import agent
```

Elbette, kullanim icin desteklenen baska komutlar da mevcuttur. Ornegin python3'e baglanmak su sekilde saglanabilir:

```python
connection_params = StdioConnectionParams(
    server_params={
        "command": "python3",
        "args": ["./agent/mcp_server.py"],
        "env": {
            "SERVICE_ACCOUNT_PATH": SERVICE_ACCOUNT_PATH,
            "DRIVE_FOLDER_ID": DRIVE_FOLDER_ID,
        },
    }
)
```

Python baglaminda UVX, gecici, izole bir Python ortaminda komutlari yurutmek icin uv kullanan bir komut satiri aracidir. Esasen Python araclarini ve paketlerini global olarak veya projenizin ortamina kurmadan calistirmaniza olanak tanir. MCP sunucusu araciligiyla calistirabilirsiniz.

```python
connection_params = StdioConnectionParams(
    server_params={
        "command": "uvx",
        "args": ["mcp-google-sheets@latest"],
        "env": {
            "SERVICE_ACCOUNT_PATH": SERVICE_ACCOUNT_PATH,
            "DRIVE_FOLDER_ID": DRIVE_FOLDER_ID,
        },
    }
)
```

MCP Sunucusu olusturulduktan sonra, bir sonraki adim ona baglanmaktir.

## MCP Sunucusunu ADK Web ile Baglama

Baslangic icin 'adk web' komutunu calistirin. Terminalinizde mcp_agent'in ust dizinine (ornegin adk_agent_samples) gidin ve calistirin:

```python
cd ./adk_agent_samples # Or your equivalent parent directory
adk web
```

ADK Web kullanici arayuzu tarayiciniza yuklendiginde, agent menusunden `filesystem_assistant_agent`'i secin. Ardindan su gibi prompt'larla deneyler yapin:

* "Bu klasorun icerigini goster."
* "`sample.txt` dosyasini oku." (Bu, `sample.txt`'nin `TARGET_FOLDER_PATH` konumunda bulundugunu varsayar.)
* "`another_file.md` icinde ne var?"

## FastMCP ile MCP Sunucusu Olusturma

FastMCP, MCP sunucularinin gelistirilmesini kolaylastirmak icin tasarlanmis yuksek duzeyli bir Python framework'udur. Protokol karmasikliklarini soyutlayan bir katman saglayarak gelistiricilerin temel mantiga odaklanmasina olanak tanir.

Kutuphane, basit Python dekoratarleri kullanarak tool'larin, resource'larin ve prompt'larin hizli bir sekilde tanimlanmasini saglar. Onemli bir avantaji, Python fonksiyon imzalarini, tip ipuclarini ve dokumantasyon dizelerini akilli bir sekilde yorumlayarak gerekli yapay zeka modeli arayuz spesifikasyonlarini olusturan otomatik sema uretimidir. Bu otomasyon, manuel yapilandirmayi en aza indirir ve insan hatasini azaltir.

Temel arac olusturmanin otesinde FastMCP, sunucu birlestirme ve proxy gibi gelismis mimari kaliplari kolaylastirir. Bu, karmasik, cok bilesenli sistemlerin moduler gelistirilmesini ve mevcut hizmetlerin yapay zeka tarafindan erisilebilir bir framework'e sorunsuz entegrasyonunu mumkun kilar. Ek olarak FastMCP, verimli, dagitik ve olceklenebilir yapay zeka destekli uygulamalar icin optimizasyonlar icerir.

## FastMCP ile Sunucu Kurulumu

## Gostermek icin, sunucu tarafindan saglanan basit bir "greet" aracini ele alalim. ADK agent'lari ve diger MCP istemcileri, aktif olduugunda HTTP kullanarak bu aracla etkilesim kurabilir

```python
# fastmcp_server.py
# This script demonstrates how to create a simple MCP server using FastMCP.
# It exposes a single tool that generates a greeting.
# 1. Make sure you have FastMCP installed:
# pip install fastmcp

from fastmcp import FastMCP, Client


# Initialize the FastMCP server.
mcp_server = FastMCP()


# Define a simple tool function.
# The `@mcp_server.tool` decorator registers this Python function as an MCP tool.
# The docstring becomes the tool's description for the LLM.
@mcp_server.tool
def greet(name: str) -> str:
    """
    Generates a personalized greeting.

    Args:
        name: The name of the person to greet.

    Returns:
        A greeting string.
    """
    return f"Hello, {name}! Nice to meet you."


# Or if you want to run it from the script:
if __name__ == "__main__":
    mcp_server.run(
        transport="http",
        host="127.0.0.1",
        port=8000,
    )
```

Bu Python betigi, bir kisinin adini alip kisisellesitirilmis bir selamlama donduren greet adinda tek bir fonksiyon tanimlar. Bu fonksiyonun uzerindeki @tool() dekoratoru, onu bir yapay zeka veya baska bir programin kullanabilecegi bir arac olarak otomatik olarak kaydeder. Fonksiyonun dokumantasyon dizesi ve tip ipuclari, FastMCP tarafindan Agent'a aracin nasil calistigini, hangi girislere ihtiyac duydugunu ve ne dondurecegini bildirmek icin kullanilir.

Betik calistirildiginda, localhost:8000 uzerinde istek dinleyen FastMCP sunucusunu baslatir. Bu, greet fonksiyonunu bir ag hizmeti olarak kullanilabilir hale getirir. Bir agent daha sonra bu sunucuya baglanacak sekilde yapilandiirilabilir ve daha buyuk bir gorevin parcasi olarak selamlama uretmek icin greet aracini kullanabilir. Sunucu, manuel olarak durdurulana kadar surekli calisir.

## FastMCP Sunucusunu ADK Agent'i ile Tuketme

Bir ADK agent'i, calisan bir FastMCP sunucusunu kullanmak icin bir MCP istemcisi olarak yapilandiirilabilir. Bu, FastMCP sunucusunun ag adresi (genellikle <http://localhost:8000>) ile HttpServerParameters'in yapilandirilmasini gerektirir.

Sunucu tarafindan sunulan belirli araclara (ornegin 'greet') agent'in arac kullanimini kisitlamak icin bir `tool_filter` parametresi dahil edilebilir. "John Doe'yu selamla" gibi bir istekle yonlendirildiginde, agent'in gomulu LLM'i MCP araciligiyla mevcut olan 'greet' aracini tanir, "John Doe" argumaniyla cagirur ve sunucunun yanitini dondurur. Bu surec, MCP araciligiyla sunulan kullanici tanimli araclarin bir ADK agent'i ile entegrasyonunu gostermektedir.

Bu yapilandirmayi olusturmak icin bir agent dosyasi (ornegin ./adk_agent_samples/fastmcp_client_agent/ konumundaki agent.py) gereklidir. Bu dosya, bir ADK agent'i olusturacak ve calisan FastMCP sunucusuyla baglanti kurmak icin HttpServerParameters kullanacaktir.

```python
# ./adk_agent_samples/fastmcp_client_agent/agent.py
import os

from google.adk.agents import LlmAgent
from google.adk.tools.mcp_tool.mcp_toolset import MCPToolset, HttpServerParameters


# Define the FastMCP server's address.
# Make sure your fastmcp_server.py (defined previously) is running on this port.
FASTMCP_SERVER_URL = "http://localhost:8000"

root_agent = LlmAgent(
    model="gemini-2.0-flash",  # Or your preferred model
    name="fastmcp_greeter_agent",
    instruction='You are a friendly assistant that can greet people by their name. Use the "greet" tool.',
    tools=[
        MCPToolset(
            connection_params=HttpServerParameters(
                url=FASTMCP_SERVER_URL,
            ),
            # Optional: Filter which tools from the MCP server are exposed
            # For this example, we're expecting only 'greet'
            tool_filter=["greet"],
        )
    ],
)
```

Betik, Gemini dil modelini kullanan `fastmcp_greeter_agent` adinda bir Agent tanimlar. Amaci insanlari selamlamak olan dost canilsi bir asistan olarak davranmasi talimati verilir. Kritik olarak, kod bu agent'i gorevini yerine getirmek icin bir aracla donatir. localhost:8000 uzerinde calisan ayri bir sunucuya (onceki ornekteki FastMCP sunucusu olmasi beklenir) baglanmak icin bir MCPToolset yapilandirir. Agent'a ozellikle o sunucuda barindirilan greet aracina erisim verilir. Ozunde bu kod, sistemin istemci tarafini kurar; hedefinin insanlari selamlamak oldugunu anlayan ve bunu basarmak icin tam olarak hangi harici araci kullanacagini bilen akilli bir agent olusturur.

`fastmcp_client_agent` dizini icinde bir `__init__.py` dosyasi olusturmak gereklidir. Bu, agent'in ADK icin kesfedilebilir bir Python paketi olarak taninmasini saglar.

Baslamak icin yeni bir terminal acin ve FastMCP sunucusunu baslatmak icin `python fastmcp_server.py` calistirin. Ardindan, terminalinizde `fastmcp_client_agent`'in ust dizinine (ornegin `adk_agent_samples`) gidin ve `adk web` calistirin. ADK Web kullanici arayuzu tarayicinizda yuklendiginde, agent menusunden `fastmcp_greeter_agent`'i secin. Ardindan "John Doe'yu selamla" gibi bir prompt girerek test edebilirsiniz. Agent, bir yanit olusturmak icin FastMCP sunucunuzdaki `greet` aracini kullanacaktir.

## Bir Bakista

**Ne:** Agent olarak etkili bir sekilde calisabilmek icin LLM'lerin basit metin uretiminin otesine gecmesi gerekir. Guncel verilere erismek ve harici yazilimlari kullanmak icin dis cevre ile etkilesim yetenegine ihtiyac duyarlar. Standartlastirilmis bir iletisim yontemi olmadan, bir LLM ile harici bir arac veya veri kaynagi arasindaki her entegrasyon ozel, karmasik ve yeniden kullanilamaz bir caba haline gelir. Bu rastgele yaklasim, olceklenebilirligi engeller ve karmasik, birbirine bagli yapay zeka sistemleri olusturmayi zor ve verimsiz kilar.

**Neden:** Model Context Protocol (MCP), LLM'ler ve harici sistemler arasinda evrensel bir arayuz gorevi gorerek standartlastirilmis bir cozum sunar. Harici yeteneklerin nasil kesfedilecegini ve kullanilacagini tanimlayan acik, standartlastirilmis bir protokol olusturur. Bir istemci-sunucu modelinde calisan MCP, sunucularin tool'lari, veri resource'larini ve etkileisimli prompt'lari uyumlu herhangi bir istemciye sunmasina olanak tanir. LLM destekli uygulamalar bu istemciler olarak hareket eder, mevcut kaynaklari dinamik olarak kesfeder ve onceden tahmin edilebilir bir sekilde onlarla etkilesime girer. Bu standartlastirilmis yaklasim, birlikte calisan ve yeniden kullanilabilir bir bilesen ekosistemi yaratarak karmasik agentic is akislarinin gelistirilmesini onemli olcude basitlesitirir.

**Temel kural:** Model Context Protocol'u (MCP), cesitli ve gelisen bir harici araclar, veri kaynaklari ve API'lar setiyle etkilesim kurmasi gereken karmasik, olceklenebilir veya kurumsal duzeyde agentic sistemler olustururken kullanin. Farkli LLM'ler ve araclar arasinda birlikte calisabilirlik bir oncelik oldugunda ve agent'larin yeniden dagitilmadan yeni yetenekleri dinamik olarak kesfetme yetenegine ihtiyac duydugunda idealdir. Sabit ve sinirli sayida onceden tanimlanmis fonksiyona sahip daha basit uygulamalar icin dogrudan tool function calling yeterli olabilir.

**Gorsel ozet:**

![Model Context Protocol](../assets/Model_Context_Protocol.png)

Sekil 1: Model Context Protocol

## Temel Cikarimlar

Temel cikarimlar sunlardir:

* Model Context Protocol (MCP), LLM'ler ile harici uygulamalar, veri kaynaklari ve araclar arasinda standartlastirilmis iletisimi kolaylastiran acik bir standarttir.
* Resource'larin, prompt'larin ve tool'larin sunulmasi ve tuketilmesi icin yontemleri tanimlayan bir istemci-sunucu mimarisi kullanir.
* Agent Development Kit (ADK), hem mevcut MCP sunucularinin kullanilmasini hem de ADK araclarinin bir MCP sunucusu araciligiyla sunulmasini destekler.
* FastMCP, ozellikle Python'da uygulanan araclari sunmak icin MCP sunucularinin gelistirilmesini ve yonetimini basitlesitirir.
* MCP Tools for Genmedia Services, agent'larin Google Cloud'un uretici medya yetenekleriyle (Imagen, Veo, Chirp 3 HD, Lyria) entegre olmasini saglar.
* MCP, LLM'lerin ve agent'larin gercek dunya sistemleriyle etkilesim kurmasini, dinamik bilgilere erismesini ve metin uretiminin otesinde eylemler gerceklestirmesini mumkun kilar.

## Sonuc

Model Context Protocol (MCP), Buyuk Dil Modelleri (LLM'ler) ile harici sistemler arasinda iletisimi kolaylastiran acik bir standarttir. LLM'lerin kaynaklara erismesini, prompt'lari kullanmasini ve standartlastirilmis araclar araciligiyla eylemler yurutmesini saglayan bir istemci-sunucu mimarisi kullanir. MCP, LLM'lerin veritabanlariyla etkilesim kurmasini, uretici medya is akislarini yonetmesini, IoT cihazlarini kontrol etmesini ve finansal hizmetleri otomatiklestirmesini saglar. Pratik ornekler, dosya sistemi sunuculari ve FastMCP ile olusturulan sunucular dahil olmak uzere MCP sunuculariyla iletisim kurmak icin agent'larin nasil yapilandirilacagini gostererek Agent Development Kit (ADK) ile entegrasyonunu aciklar. MCP, temel dil yeteneklerinin otesine gecen etkilesimli yapay zeka agent'lari gelistirmek icin temel bir bilesendir.

## Kaynaklar

1. Model Context Protocol (MCP) Documentation. (Latest). *Model Context Protocol (MCP)*. [https://google.github.io/adk-docs/mcp/](https://google.github.io/adk-docs/mcp/)
2. FastMCP Documentation. FastMCP. [https://github.com/jlowin/fastmcp](https://github.com/jlowin/fastmcp)
3. MCP Tools for Genmedia Services. *MCP Tools for Genmedia Services*. [https://google.github.io/adk-docs/mcp/\#mcp-servers-for-google-cloud-genmedia](https://google.github.io/adk-docs/mcp/#mcp-servers-for-google-cloud-genmedia)
4. MCP Toolbox for Databases Documentation. (Latest). *MCP Toolbox for Databases*. [https://google.github.io/adk-docs/mcp/databases/](https://google.github.io/adk-docs/mcp/databases/)
