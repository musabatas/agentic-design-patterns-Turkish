# Bolum 15: Araclar Arasi Iletisim (A2A)

Bireysel yapay zeka agent'lari, gelismis yeteneklere sahip olsalar bile, karmasik ve cok boyutlu problemlerle basa cikarken siklikla sinirlamalarla karsilasir. Bu sorunu asmak icin, Araclar Arasi Iletisim (Inter-Agent Communication - A2A), farkli framework'lerle gelistirilmis olabilecek cesitli yapay zeka agent'larinin etkili bir sekilde is birligi (Collaboration) yapmasini saglar. Bu is birligi, kesintisiz koordinasyon, gorev devri ve bilgi alisverisini icerir.

Google'in A2A protokolu, bu evrensel iletisimi (Communication) kolaylastirmak icin tasarlanmis acik bir standartdir. Bu bolum, A2A'yi, pratik uygulamalarini ve Google ADK icerisindeki uygulanisini inceleyecektir.

## Araclar Arasi Iletisim Kalibina Genel Bakis

Agent2Agent (A2A) protokolu, farkli yapay zeka agent framework'leri arasinda iletisim ve is birligini saglamak icin tasarlanmis acik bir standartdir. Birlikte calisabilirlik saglayarak, LangGraph, CrewAI veya Google ADK gibi teknolojilerle gelistirilen yapay zeka agent'larinin koken veya framework farkliliklarindan bagimsiz olarak birlikte calismasina olanak tanir.

A2A; Atlassian, Box, LangChain, MongoDB, Salesforce, SAP ve ServiceNow dahil olmak uzere bir dizi teknoloji sirketi ve hizmet saglayicisi tarafindan desteklenmektedir. Microsoft, acik protokollere olan bagliligini gostererek A2A'yi Azure AI Foundry ve Copilot Studio'ya entegre etmeyi planlamaktadir. Ayrica Auth0 ve SAP, platformlarina ve agent'larina A2A destegi eklemektedir.

Acik kaynakli bir protokol olarak A2A, gelisimini ve yaygin benimsenmesini kolaylastirmak icin topluluk katkilarini memnuniyetle karsilar.

## A2A'nin Temel Kavramlari

A2A protokolu, agent etkilesimleri icin birkac temel kavram uzerine insa edilmis yapilandirilmis bir yaklasim sunar. Bu kavramlarin kapsamli bir sekilde anlasilmasi, A2A uyumlu sistemler gelistiren veya entegre eden herkes icin cok onemlidir. A2A'nin temel yapitaslari arasinda Temel Aktorler, Agent Card, Agent Kesfi, Iletisim ve Gorevler, Etkilesim Mekanizmalari ve Guvenlik yer alir; bunlarin tumunu ayrintili olarak inceleyecegiz.

**Temel Aktorler:** A2A uc ana varlik icerir:

* Kullanici: Agent yardimi icin istekleri baslatir.
* A2A Istemcisi (Client Agent): Kullanici adina eylem veya bilgi talep etmek icin hareket eden bir uygulama veya yapay zeka agent'i.
* A2A Sunucusu (Remote Agent): Istemci isteklerini islemek ve sonuclari dondurmek icin bir HTTP uc noktasi saglayan bir yapay zeka agent'i veya sistem. Uzak agent "opak" bir sistem olarak calisir; yani istemcinin onun dahili operasyonel ayrintilarina hakim olmasi gerekmez.

**Agent Card:** Bir agent'in dijital kimligi, genellikle bir JSON dosyasi olan Agent Card'i ile tanimlanir. Bu dosya, istemci etkilesimi ve otomatik kesif icin temel bilgileri icerir; bunlar arasinda agent'in kimligi, uç nokta URL'si ve surum bilgisi yer alir. Ayrica streaming veya push notification gibi desteklenen yetenekleri, belirli becerileri, varsayilan girdi/cikti modlarini ve kimlik dogrulama gereksinimlerini de ayrintilandirir. Asagida bir WeatherBot icin ornek bir Agent Card yer almaktadir.

```json
{
    "name": "WeatherBot",
    "description": "Provides accurate weather forecasts and historical data.",
    "url": "http://weather-service.example.com/a2a",
    "version": "1.0.0",
    "capabilities": {
        "streaming": true,
        "pushNotifications": false,
        "stateTransitionHistory": true
    },
    "authentication": {
        "schemes": [
            "apiKey"
        ]
    },
    "defaultInputModes": [
        "text"
    ],
    "defaultOutputModes": [
        "text"
    ],
    "skills": [
        {
            "id": "get_current_weather",
            "name": "Get Current Weather",
            "description": "Retrieve real-time weather for any location.",
            "inputModes": [
                "text"
            ],
            "outputModes": [
                "text"
            ],
            "examples": [
                "What's the weather in Paris?",
                "Current conditions in Tokyo"
            ],
            "tags": [
                "weather",
                "current",
                "real-time"
            ]
        },
        {
            "id": "get_forecast",
            "name": "Get Forecast",
            "description": "Get 5-day weather predictions.",
            "inputModes": [
                "text"
            ],
            "outputModes": [
                "text"
            ],
            "examples": [
                "5-day forecast for New York",
                "Will it rain in London this weekend?"
            ],
            "tags": [
                "weather",
                "forecast",
                "prediction"
            ]
        }
    ]
}
```

**Agent Kesfi:** Istemcilerin, mevcut A2A Sunucularinin yeteneklerini tanimlayan Agent Card'lari bulmasini saglar. Bu islem icin birkac strateji mevcuttur:

* Well-Known URI: Agent'lar, Agent Card'larini standartlastirilmis bir yolda (ornegin, /.well-known/agent.json) barindirir. Bu yaklasim, genel veya alana ozgu kullanim icin genis, genellikle otomatik erisilebilirlik sunar.
* Kuratoryel Kayitlar: Agent Card'larinin yayinlandigi ve belirli kriterlere gore sorgulanabilecegi merkezi bir katalog saglar. Bu, merkezi yonetim ve erisim kontrolu gerektiren kurumsal ortamlar icin uygundur.
* Dogrudan Yapilandirma: Agent Card bilgileri gomulu olarak veya ozel olarak paylasilir. Bu yontem, dinamik kesfin onemli olmadigi yakin bagli veya ozel sistemler icin uygundur.

Secilen yontemden bagimsiz olarak, Agent Card uc noktalarinin guvenliginin saglanmasi onemlidir. Bu, ozellikle kart hassas (ancak gizli olmayan) bilgiler iceriyorsa, erisim kontrolu, karsilikli TLS (mTLS) veya ag kisitlamalari yoluyla gerceklestirilebilir.

**Iletisim ve Gorevler:** A2A cati altinda iletisim, uzun sureli islemler icin temel calisma birimlerini temsil eden asenkron gorevler etrafinda yapilandirilmistir. Her goreve benzersiz bir tanimlayici atanir ve gonderildi, calisiyor veya tamamlandi gibi bir dizi durumdan gecer; bu tasarim, karmasik operasyonlarda paralel islemeyi destekler. Agent'lar arasi iletisim bir Mesaj araciligiyla gerceklesir.

Bu iletisim, mesaji tanimlayan anahtar-deger meta verileri olan ozellikler (ornegini onceligi veya olusturulma zamani gibi) ve iletilen gercek icerigi tasiyan bir veya daha fazla parca icerir; bu parcalar duz metin, dosyalar veya yapilandirilmis JSON verileri olabilir. Bir agent'in gorev sirasinda urettigi somut ciktilar artifact olarak adlandirilir. Mesajlar gibi, artifact'lar da bir veya daha fazla parcadan olusur ve sonuclar elde edildikce artimli olarak aktarilabilir. A2A cati altindaki tum iletisim, yukler icin JSON-RPC 2.0 protokolu kullanilarak HTTP(S) uzerinden gerceklestirilir. Birden fazla etkilesim boyunca surekliligi korumak icin, ilgili gorevleri gruplamak ve baglami korumak amaciyla sunucu tarafindan olusturulan bir contextId kullanilir.

**Etkilesim Mekanizmalari:** Istek/Yanit (Polling) ve Server-Sent Events (SSE). A2A, cesitli yapay zeka uygulama ihtiyaclarina uygun, her biri farkli bir mekanizmaya sahip birden fazla etkilesim yontemi sunar:

* Senkron Istek/Yanit: Hizli, anlik islemler icindir. Bu modelde istemci bir istek gonderir ve sunucunun bunu isleyip tek bir senkron alisveriste eksiksiz bir yanit dondurmesini aktif olarak bekler.
* Asenkron Polling: Islenmesi daha uzun suren gorevler icin uygundur. Istemci bir istek gonderir ve sunucu bunu hemen "calisiyor" durumu ve bir gorev kimligiyle onaylar. Istemci daha sonra diger islemleri gerceklestirmekte serbesttir ve gorev "tamamlandi" veya "basarisiz" olarak isaretlenene kadar sunucuya periyodik olarak yeni istekler gondererek gorev durumunu kontrol edebilir.
* Streaming Guncellemeleri (Server-Sent Events - SSE): Gercek zamanli, artimli sonuclar almak icin idealdir. Bu yontem, sunucudan istemciye kalici, tek yonlu bir baglanti kurar. Uzak agent'in, istemcinin birden fazla istek yapmasi gerekmeden durum degisiklikleri veya kismi sonuclar gibi guncellemeleri surekli olarak gondermesine olanak tanir.
* Push Notification'lar (Webhook'lar): Surekli bir baglanti veya sik polling'in verimsiz oldugu, cok uzun sureli veya kaynak yogun gorevler icin tasarlanmistir. Istemci bir webhook URL'si kaydedebilir ve sunucu, gorev durumu onemli olcude degistiginde (ornegin tamamlandiginda) bu URL'ye asenkron bir bildirim ("push") gonderir.

Agent Card, bir agent'in streaming veya push notification yeteneklerini destekleyip desteklemedigini belirtir. Dahasi, A2A modalite bagimsizdir; yani bu etkilesim kaliplarini yalnizca metin icin degil, ayni zamanda ses ve video gibi diger veri turleri icin de kolaylastirarak zengin, cok modlu yapay zeka uygulamalarini mumkun kilar. Hem streaming hem de push notification yetenekleri Agent Card icerisinde belirtilir.

```json
# Synchronous Request Example
{
    "jsonrpc": "2.0",
    "id": "1",
    "method": "sendTask",
    "params": {
        "id": "task-001",
        "sessionId": "session-001",
        "message": {
            "role": "user",
            "parts": [
                {
                    "type": "text",
                    "text": "What is the exchange rate from USD to EUR?"
                }
            ]
        },
        "acceptedOutputModes": [
            "text/plain"
        ],
        "historyLength": 5
    }
}
```

Senkron istek, sendTask yontemini kullanir; burada istemci sorgusuna tek ve eksiksiz bir yanit ister ve bekler. Buna karsilik, streaming istegi sendTaskSubscribe yontemini kullanarak kalici bir baglanti kurar ve agent'in zaman icinde birden fazla artimli guncelleme veya kismi sonuc gondermesine olanak tanir.

```json
# Streaming Request Example
{
    "jsonrpc": "2.0",
    "id": "2",
    "method": "sendTaskSubscribe",
    "params": {
        "id": "task-002",
        "sessionId": "session-001",
        "message": {
            "role": "user",
            "parts": [
                {
                    "type": "text",
                    "text": "What's the exchange rate for JPY to GBP today?"
                }
            ]
        },
        "acceptedOutputModes": [
            "text/plain"
        ],
        "historyLength": 5
    }
}
```

**Guvenlik (Safety):** Araclar Arasi Iletisim (A2A), sistem mimarisinin hayati bir bilesenini olusturarak agent'lar arasinda guvenli ve kesintisiz veri alisverisini saglar. Birkac yerlesik mekanizma araciligiyla saglam ve butunluk yuksek iletisim garanti eder.

Karsilikli Tasima Katmani Guvenligi (Mutual TLS): Yetkisiz erisimi ve veri dinlemeyi onlemek, guvenli iletisimi saglamak icin sifreli ve kimlik dogrulamali baglantilar kurulur.

Kapsamli Denetim Gunlukleri: Tum araclar arasi iletisimler titizlikle kaydedilir; bilgi akisi, ilgili agent'lar ve eylemler ayrintilandirilir. Bu denetim izi, hesap verebilirlik, sorun giderme ve guvenlik analizi icin buyuk onem tasir.

Agent Card Beyani: Kimlik dogrulama gereksinimleri, agent'in kimligini, yeteneklerini ve guvenlik politikalarini ozetleyen bir yapilandirma ogesi olan Agent Card'da acikca beyan edilir. Bu, kimlik dogrulama yonetimini merkezilestirip basitlestirir.

Kimlik Bilgisi Yonetimi: Agent'lar genellikle HTTP basliklarindan gecirilen OAuth 2.0 token'lari veya API anahtarlari gibi guvenli kimlik bilgileri kullanarak kimlik dogrulamasi yapar. Bu yontem, kimlik bilgilerinin URL'lerde veya mesaj govdelerinde aciga cikmasini onleyerek genel guvenligi arttirir.

## A2A ve MCP Karsilastirmasi

A2A, Anthropic'in Model Context Protocol'unu (MCP) tamamlayan bir protokoldur (bkz. Sekil 1). MCP, agent'lar icin baglam yapilandirmasi ve harici veri ile araclarla etkilesimlere odaklanirken, A2A agent'lar arasi koordinasyon ve iletisimi kolaylastirarak gorev devri ve is birligini mumkun kilar.

![Comparison A2A and MCP Protocols](../assets/Comparison_A2A_and_MCP_Protocols.png)

Sekil 1: A2A ve MCP Protokollerinin Karsilastirmasi

A2A'nin amaci, karmasik multi-agent yapay zeka sistemlerinin gelistirilmesinde verimliligi artirmak, entegrasyon maliyetlerini azaltmak ve yenilik ile birlikte calisabilirlik ilkelerini tesvik etmektir. Bu nedenle, A2A'nin temel bilesenlerinin ve operasyonel yontemlerinin kapsamli bir sekilde anlasilmasi, is birligine dayali ve birlikte calisabilir yapay zeka agent sistemlerinin etkili tasarimi, uygulanmasi ve kullanimi icin hayati onem tasir.

## Pratik Uygulamalar ve Kullanim Alanlari

Araclar Arasi Iletisim, cesitli alanlarda sofistike yapay zeka cozumleri olusturmak icin vazgecilmezdir; modulerlik, olceklenebilirlik ve gelistirilmis zeka saglar.

* **Coklu Framework Is Birligi:** A2A'nin temel kullanim alani, altinda yatan framework'lerden (ornegin ADK, LangChain, CrewAI) bagimsiz olarak bagimsiz yapay zeka agent'larinin iletisim kurmasini ve is birligi yapmasini saglamaktir. Bu, farkli agent'larin bir problemin farkli yonlerinde uzmanlasmis oldugu karmasik multi-agent sistemleri olusturmak icin esastir.
* **Otomatik Workflow Orkestrasyon:** Kurumsal ortamlarda A2A, agent'larin gorevleri devretmesini ve koordine etmesini saglayarak karmasik is akislarini kolaylastirabilir. Ornegin, bir agent ilk veri toplamayı yapabilir, ardindan analiz icin baska bir agent'a devredebilir ve son olarak rapor olusturma icin ucuncu bir agent'a yonlendirebilir; tumu A2A protokolu araciligiyla iletisim kurar.
* **Dinamik Bilgi Erisimi:** Agent'lar, gercek zamanli bilgi almak ve paylasma icin iletisim kurabilir. Bir birincil agent, uzmanlasmis bir "veri cekme agent'indan" canli piyasa verilerini isteyebilir; bu agent daha sonra bilgiyi toplamak icin harici API'leri kullanir ve geri gonderir.

## Uygulamali Kod Ornegi

A2A protokolunun pratik uygulamalarini inceleyelim. [https://github.com/google-a2a/a2a-samples/tree/main/samples](https://github.com/google-a2a/a2a-samples/tree/main/samples) adresindeki depo; LangGraph, CrewAI, Azure AI Foundry ve AG2 gibi cesitli agent framework'lerinin A2A kullanarak nasil iletisim kurabilecegini gosteren Java, Go ve Python ornekleri saglar. Bu depodaki tum kod Apache 2.0 lisansi altinda yayimlanmistir. A2A'nin temel kavramlarini daha iyi gostermek icin, Google ile kimlik dogrulamali araclar kullanan ADK tabanli bir agent ile A2A Sunucusu kurmaya odaklanan kod parcalarini inceleyecegiz. [https://github.com/google-a2a/a2a-samples/blob/main/samples/python/agents/birthday_planner_adk/calendar_agent/adk_agent.py](https://github.com/google-a2a/a2a-samples/blob/main/samples/python/agents/birthday_planner_adk/calendar_agent/adk_agent.py) adresine bakalim.

```python
import datetime

from google.adk.agents import LlmAgent  # type: ignore[import-untyped]
from google.adk.tools.google_api_tool import CalendarToolset  # type: ignore[import-untyped]


async def create_agent(client_id: str, client_secret: str) -> LlmAgent:
    """Constructs the ADK agent."""
    toolset = CalendarToolset(client_id=client_id, client_secret=client_secret)
    return LlmAgent(
        model="gemini-2.0-flash-001",
        name="calendar_agent",
        description="An agent that can help manage a user's calendar",
        instruction=(
            f""" You are an agent that can help manage a user's calendar. Users will request information about the state of their calendar """
            f""" or to make changes to their calendar. Use the provided tools for interacting with the calendar API. """
            f""" If not specified, assume the calendar the user wants is the 'primary' calendar. """
            f""" When using the Calendar API tools, use well-formed RFC3339 timestamps. Today is {datetime.datetime.now()}. """
        ),
        tools=await toolset.get_tools(),
    )
```

Bu Python kodu, bir ADK LlmAgent olusturan asenkron bir `create_agent` fonksiyonu tanimlar. Google Calendar API'sine erismek icin saglanan istemci kimlik bilgilerini kullanarak bir `CalendarToolset` baslatir. Ardindan, belirli bir Gemini modeli, aciklayici bir ad ve kullanicinin takvimini yonetmek icin talimatlarla yapilandirilmis bir `LlmAgent` ornegi olusturulur. Agent, Calendar API ile etkilesime girmesini ve kullanici sorgularina takvim durumlari veya degisiklikleri hakkinda yanit vermesini saglayan `CalendarToolset`'ten takvim araclariyla donatilir. Agent'in talimatlari, zamansal baglam icin mevcut tarihi dinamik olarak dahil eder. Bir agent'in nasil olusturuldugunu gostermek icin, GitHub'daki A2A orneklerinde bulunan `calendar_agent`'in onemli bir bolumunu inceleyelim.

Asagidaki kod, agent'in belirli talimatlari ve araclariyla nasil tanimlandigini gosterir. Lutfen bu islevi aciklamak icin gereken kodun yalnizca bir bolumunun gosterildigini unutmayin; dosyanin tamamina buradan erisebilirsiniz: [https://github.com/a2aproject/a2a-samples/blob/main/samples/python/agents/birthday_planner_adk/calendar_agent/__main__.py](https://github.com/a2aproject/a2a-samples/blob/main/samples/python/agents/birthday_planner_adk/calendar_agent/__main__.py)

```python
def main(host: str = "0.0.0.0", port: int = 8000):
    # Verify an API key is set.
    # Not required if using Vertex AI APIs.
    if os.getenv("GOOGLE_GENAI_USE_VERTEXAI") != "TRUE" and not os.getenv("GOOGLE_API_KEY"):
        raise ValueError(
            "GOOGLE_API_KEY environment variable not set and "
            "GOOGLE_GENAI_USE_VERTEXAI is not TRUE."
        )

    skill = AgentSkill(
        id="check_availability",
        name="Check Availability",
        description="Checks a user's availability for a time using their Google Calendar",
        tags=["calendar"],
        examples=["Am I free from 10am to 11am tomorrow?"],
    )

    agent_card = AgentCard(
        name="Calendar Agent",
        description="An agent that can manage a user's calendar",
        url=f"http://{host}:{port}/",
        version="1.0.0",
        defaultInputModes=["text"],
        defaultOutputModes=["text"],
        capabilities=AgentCapabilities(streaming=True),
        skills=[skill],
    )

    adk_agent = asyncio.run(
        create_agent(
            client_id=os.getenv("GOOGLE_CLIENT_ID"),
            client_secret=os.getenv("GOOGLE_CLIENT_SECRET"),
        )
    )

    runner = Runner(
        app_name=agent_card.name,
        agent=adk_agent,
        artifact_service=InMemoryArtifactService(),
        session_service=InMemorySessionService(),
        memory_service=InMemoryMemoryService(),
    )
    agent_executor = ADKAgentExecutor(runner, agent_card)

    async def handle_auth(request: Request) -> PlainTextResponse:
        await agent_executor.on_auth_callback(
            str(request.query_params.get("state")),
            str(request.url),
        )
        return PlainTextResponse("Authentication successful.")

    request_handler = DefaultRequestHandler(
        agent_executor=agent_executor,
        task_store=InMemoryTaskStore(),
    )

    a2a_app = A2AStarletteApplication(
        agent_card=agent_card,
        http_handler=request_handler,
    )
    routes = a2a_app.routes()
    routes.append(
        Route(
            path="/authenticate",
            methods=["GET"],
            endpoint=handle_auth,
        )
    )
    app = Starlette(routes=routes)

    uvicorn.run(app, host=host, port=port)


if __name__ == "__main__":
    main()
```

Bu Python kodu, Google Calendar kullanarak kullanici musaitligini kontrol etmek icin A2A uyumlu bir "Calendar Agent" kurulumunu gosterir. Kimlik dogrulama amaciyla API anahtarlarinin veya Vertex AI yapilandirmalarinin dogrulanmasini icerir. Agent'in "check_availability" becerisi dahil olmak uzere yetenekleri, agent'in ag adresini de belirten bir AgentCard icerisinde tanimlanir. Ardindan, artifact'lar, oturumlar ve bellek yonetimi icin bellek ici hizmetlerle yapilandirilmis bir ADK agent'i olusturulur. Kod daha sonra bir Starlette web uygulamasini baslatir, bir kimlik dogrulama geri aramasi ve A2A protokol isleyicisini dahil eder ve agent'i HTTP uzerinden sunmak icin Uvicorn ile calistirir.

Bu ornekler, yeteneklerini tanimlamaktan bir web hizmeti olarak calistirmaya kadar A2A uyumlu bir agent olusturma surecini gostermektedir. Agent Card'lar ve ADK kullanilarak, gelistiriciler Google Calendar gibi araclarla entegre olabilen birlikte calisabilir yapay zeka agent'lari olusturabilir. Bu pratik yaklasim, A2A'nin multi-agent bir ekosistem olusturmadaki uygulamasini gostermektedir.

A2A'nin daha fazla kesfedilmesi icin [https://www.trickle.so/blog/how-to-build-google-a2a-project](https://www.trickle.so/blog/how-to-build-google-a2a-project) adresindeki kod gosterimi onerilir. Bu baglantiyla ulasilan kaynaklar arasinda Python ve JavaScript'te ornek A2A istemcileri ve sunuculari, multi-agent web uygulamalari, komut satiri arayuzleri ve cesitli agent framework'leri icin ornek uygulamalar bulunmaktadir.

## Bir Bakista

**Ne:** Bireysel yapay zeka agent'lari, ozellikle farkli framework'ler uzerine insa edilmis olanlar, genellikle karmasik, cok yonlu problemlerde tek basina zorlanir. Temel zorluk, bunlarin etkili bir sekilde iletisim kurmasini ve is birligi yapmasini saglayan ortak bir dil veya protokolun bulunmamasidir. Bu izolasyon, birden fazla uzman agent'in benzersiz becerilerini birlestirerek daha buyuk gorevleri cozebilecegi sofistike sistemlerin olusturulmasini engeller. Standartlastirilmis bir yaklasim olmadan, bu farkli agent'lari entegre etmek maliyetli, zaman alici olup daha guclu ve tutarli yapay zeka cozumlerinin gelistirilmesini engeller.

**Neden:** Araclar Arasi Iletisim (A2A) protokolu, bu sorun icin acik ve standartlastirilmis bir cozum sunar. Birlikte calisabilirlik saglayan HTTP tabanli bir protokol olup, farkli yapay zeka agent'larinin altta yatan teknolojiden bagimsiz olarak koordine olmasini, gorev devretmesini ve bilgi paylasmasini mumkun kilar. Temel bir bilesen olan Agent Card, bir agent'in yeteneklerini, becerilerini ve iletisim uc noktalarini tanimlayan, kesif ve etkilesimi kolaylastiran dijital bir kimlik dosyasidir. A2A, cesitli kullanim alanlarini desteklemek icin senkron ve asenkron iletisim dahil cesitli etkilesim mekanizmalari tanimlar. Agent is birligi icin evrensel bir standart olusturarak A2A, karmasik multi-agent sistemleri icin moduler ve olceklenebilir bir ekosistem olusturur.

**Temel Kural:** Bu kalibi, iki veya daha fazla yapay zeka agent'i arasinda is birligini orkestre etmeniz gerektiginde kullanin; ozellikle farkli framework'lerle (ornegin Google ADK, LangGraph, CrewAI) insa edilmislerse. Uzman agent'larin bir is akisinin belirli bolumlerini ele aldigi karmasik, moduler uygulamalar olusturmak icin idealdir; ornegin veri analizini bir agent'a, rapor olusturmayi baska bir agent'a devretmek gibi. Bu kalip, bir agent'in bir gorevi tamamlamak icin diger agent'larin yeteneklerini dinamik olarak kesfetmesi ve tuketmesi gerektiginde de onemlidir.

**Gorsel Ozet:**

![A2A Inter-Agent Communication Pattern](../assets/A2A_Inter-Agent_Communication_Pattern.png)

Sekil 2: A2A araclar arasi iletisim kalibi

## Onemli Cikarimlar

Onemli Cikarimlar:

* Google A2A protokolu, farkli framework'lerle olusturulmus yapay zeka agent'lari arasinda iletisim ve is birligini kolaylastiran acik, HTTP tabanli bir standartdir.
* AgentCard, bir agent icin dijital bir tanimlayici gorevi gorerek diger agent'lar tarafindan yeteneklerinin otomatik olarak kesfedilmesini ve anlasilmasini saglar.
* A2A, degisen iletisim ihtiyaclarini karsilamak icin hem senkron istek-yanit etkilesimleri (`tasks/send` kullanarak) hem de streaming guncellemeleri (`tasks/sendSubscribe` kullanarak) sunar.
* Protokol, agent'larin ek bilgi talep etmesine ve etkilesimler sirasinda baglami korumasina olanak taniyan `input-required` durumu dahil cok turlu konusmalari destekler.
* A2A, uzman agent'larin farkli portlarda bagimsiz olarak calisabilecegi moduler bir mimariyi tesvik eder ve sistem olceklenebilirligini ve dagitimini mumkun kilar.
* Trickle AI gibi araclar, A2A iletisimlerini gorselllestirmeye ve izlemeye yardimci olarak gelisiticilerin multi-agent sistemlerini izlemesini, hata ayiklamasini ve optimize etmesini saglar.
* A2A, farkli agent'lar arasindaki gorevleri ve is akislarini yonetmek icin ust duzey bir protokol iken, Model Context Protocol (MCP), LLM'lerin harici kaynaklarla arayuz olusturmasi icin standartlastirilmis bir arayuz saglar.

## Sonuclar

Araclar Arasi Iletisim (A2A) protokolu, bireysel yapay zeka agent'larinin dogasindan kaynaklanan izolasyonu asmak icin hayati bir acik standart olusturur. Ortak bir HTTP tabanli cati saglayarak, Google ADK, LangGraph veya CrewAI gibi farkli platformlarda insa edilmis agent'lar arasinda kesintisiz is birligi ve birlikte calisabilirlik saglar. Temel bir bilesen olan Agent Card, bir agent'in yeteneklerini acikca tanimlayan ve diger agent'lar tarafindan dinamik kesfini mumkun kilan dijital bir kimlik gorevi gorur. Protokolun esnekligi, genis bir uygulama yelpazesine hitap eden senkron istekler, asenkron polling ve gercek zamanli streaming gibi cesitli etkilesim kaliplarini destekler.

Bu, uzman agent'larin karmasik otomatik is akislarini orkestre etmek icin birlestirilecegi moduler ve olceklenebilir mimarilerin olusturulmasini saglar. Guvenlik, iletisimleri korumak icin mTLS ve acik kimlik dogrulama gereksinimleri gibi yerlesik mekanizmalarla temel bir unsurdur. MCP gibi diger standartlari tamamlarken, A2A'nin benzersiz odagi agent'lar arasindaki ust duzey koordinasyon ve gorev devridir. Buyuk teknoloji sirketlerinin guclu destegi ve pratik uygulamalarin mevcudiyeti, artan onemini vurgulamaktadir. Bu protokol, gelisiticilerin daha sofistike, dagitik ve akilli multi-agent sistemleri olusturmasinin yolunu acar. Nihayetinde A2A, is birligine dayali yapay zekanin yenilikci ve birlikte calisabilir bir ekosistemini tesvik etmek icin temel bir yapitasidir.

## Referanslar

1. Chen, B. (2025, April 22). *How to Build Your First Google A2A Project: A Step-by-Step Tutorial*. Trickle.so Blog. [https://www.trickle.so/blog/how-to-build-google-a2a-project](https://www.trickle.so/blog/how-to-build-google-a2a-project)
2. Google A2A GitHub Repository. [https://github.com/google-a2a/A2A](https://github.com/google-a2a/A2A)
3. Google Agent Development Kit (ADK) [https://google.github.io/adk-docs/](https://google.github.io/adk-docs/)
4. Getting Started with Agent-to-Agent (A2A) Protocol: [https://codelabs.developers.google.com/intro-a2a-purchasing-concierge\#0](https://codelabs.developers.google.com/intro-a2a-purchasing-concierge#0)
5. Google AgentDiscovery \- [https://a2a-protocol.org/latest/](https://a2a-protocol.org/latest/)
6. Communication between different AI frameworks such as LangGraph, CrewAI, and Google ADK [https://www.trickle.so/blog/how-to-build-google-a2a-project](https://www.trickle.so/blog/how-to-build-google-a2a-project#setting-up-your-a2a-development-environment)
7. Designing Collaborative Multi-Agent Systems with the A2A Protocol [https://www.oreilly.com/radar/designing-collaborative-multi-agent-systems-with-the-a2a-protocol/](https://www.oreilly.com/radar/designing-collaborative-multi-agent-systems-with-the-a2a-protocol/)
