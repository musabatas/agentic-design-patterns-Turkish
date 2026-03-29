# Bolum 8: Bellek Yonetimi (Memory Management)

Etkili bellek yonetimi (memory management), akilli agent'larin bilgiyi muhafaza etmesi icin kritik oneme sahiptir. Agent'lar, insanlara benzer sekilde, verimli calisabilmek icin farkli bellek turlerine ihtiyac duyar. Bu bolum, agent'larin anlık (kisa sureli) ve kalici (uzun sureli) bellek gereksinimlerini ele alarak bellek yonetimini derinlemesine incelemektedir.

Agent sistemlerinde bellek, bir agent'in gecmis etkilesimlerden, gozlemlerden ve ogrenme deneyimlerinden elde ettigi bilgileri saklama ve kullanma yetenegini ifade eder. Bu yetenek, agent'larin bilingli kararlar almalarini, konusma baglamini surdurmelerini ve zaman icinde gelismelerini saglar. Agent bellegi genel olarak iki ana kategoriye ayrilir:

* **Kisa Sureli Bellek (Baglamsal Bellek):** Calisma bellegine benzer sekilde, su anda islenmekte olan veya yakın zamanda erisiilen bilgileri tutar. Buyuk dil modelleri (LLM) kullanan agent'lar icin kisa sureli bellek, oncelikle context window icinde bulunur. Bu pencere, mevcut etkilesimdeki son mesajlari, agent yanitlarini, tool use sonuclarini ve agent yansitmalarini icerir; bunlarin tumU LLM'in sonraki yanitlarini ve eylemlerini bilgilendirir. Context window sinirli bir kapasiteye sahiptir ve bu da bir agent'in dogrudan erisebilecegi guncel bilgi miktarini kisitlar. Verimli kisa sureli bellek yonetimi, en ilgili bilgilerin bu sinirli alan icinde tutulmasini icerir; bu, eski konusma bolumlerinin ozetlenmesi veya kilit ayrintilarin vurgulanmasi gibi tekniklerle saglanabilir. "Uzun baglam" pencerelerine sahip modellerin ortaya cikisi, bu kisa sureli bellegin boyutunu genisleterek tek bir etkilesim icinde daha fazla bilginin tutulmasina olanak tanir. Ancak bu baglam hala gecicidir ve oturum sona erdiginde kaybolur; ayrica her seferinde islenmesi maliyetli ve verimsiz olabilir. Sonuc olarak agent'lar, gercek kalicilik elde etmek, gecmis etkilesimlerden bilgi hatirlamak ve kalici bir bilgi tabani olusturmak icin ayri bellek turlerine ihtiyac duyar.
* **Uzun Sureli Bellek (Kalici Bellek):** Agent'larin cesitli etkilesimler, gorevler veya uzun sureler boyunca saklamasi gereken bilgiler icin bir depo gorevi gorur; uzun sureli bilgi tabanlarina benzer. Veriler genellikle agent'in anlik isleme ortaminin disinda, cogu zaman veritabanlarinda, knowledge graph'larda veya vector database'lerde saklanir. Vector database'lerde bilgiler sayisal vektorlere donusturulerek saklanir ve bu sayede agent'lar, tam anahtar kelime eslesmesi yerine anlamsal benzerlige dayali olarak veri alabilir; bu surec semantic search olarak bilinir. Bir agent uzun sureli bellekten bilgiye ihtiyac duydugunda, harici depoyu sorgular, ilgili verileri alir ve anlik kullanim icin kisa sureli baglama entegre eder; boylece onceki bilgiyi mevcut etkilesimle birlestirir.

## Pratik Uygulamalar ve Kullanim Alanlari

Bellek yonetimi, agent'larin bilgiyi takip etmesi ve zaman icinde akilli bir sekilde performans gostermesi icin hayati oneme sahiptir. Bu, agent'larin temel soru-cevap yeteneklerini asmasi icin gereklidir. Uygulama alanlari sunlardir:

* **Chatbot'lar ve Konusma Tabanli Yapay Zeka:** Konusma akisinin surdurlmesi kisa sureli bellege dayanir. Chatbot'lar, tutarli yanitlar verebilmek icin onceki kullanici girislerini hatirlamak zorundadir. Uzun sureli bellek, chatbot'larin kullanici tercihlerini, gecmis sorunlari veya onceki tartismalari hatirlayarak kisisellesirilmis ve surekli etkilesimler sunmasini saglar.
* **Gorev Odakli Agent'lar:** Cok adimli gorevleri yoneten agent'lar, onceki adimlari, mevcut ilerlemeyi ve genel hedefleri takip etmek icin kisa sureli bellege ihtiyac duyar. Bu bilgi, gorevin baglaminda veya gecici depolamada bulunabilir. Uzun sureli bellek, anlik baglamda bulunmayan kullaniciya ozel verilere erismek icin kritiktir.
* **Kisisellesirilmis Deneyimler:** Ozellestirilmis etkilesimler sunan agent'lar, kullanici tercihlerini, gecmis davranislari ve kisisel bilgileri saklamak ve almak icin uzun sureli bellekten yararlanir. Bu, agent'larin yanitlarini ve onerilerini uyarlamasina olanak tanir.
* **Ogrenme (Learning) ve Gelisim:** Agent'lar, gecmis etkilesimlerden ogrenilecek derslerle performanslarini iyilestirebilir. Basarili stratejiler, hatalar ve yeni bilgiler uzun sureli bellekte saklanarak gelecekteki uyum saglamalari kolaylastirilir. Reinforcement learning agent'lari, ogrenilmis strateji veya bilgilerini bu sekilde saklar.
* **Bilgi Erisimi (RAG):** Soru cevaplama icin tasarlanan agent'lar, genellikle Retrieval Augmented Generation (RAG) icinde uygulanan uzun sureli bellekleri olan bir knowledge base'e erisir. Agent, yanitlarini bilgilendirmek icin ilgili belgeleri veya verileri alir.
* **Otonom Sistemler:** Robotlar veya otonom araclar, haritalar, rotalar, nesne konumlari ve ogrenilmis davranislar icin bellege ihtiyac duyar. Bu, anlik cevre icin kisa sureli bellek ve genel cevre bilgisi icin uzun sureli bellegi kapsar.

Bellek, agent'larin gecmisi surdurmesini, ogrenmesini, etkilesimleri kisisellestirmesini ve karmasik, zamana bagli sorunlari yonetmesini saglar.

## Uygulamali Kod: Google Agent Developer Kit (ADK) ile Bellek Yonetimi

Google Agent Developer Kit (ADK), baglam ve bellek yonetimi icin pratik uygulamaya yonelik bilesenler dahil olmak uzere yapilandirilmis bir yontem sunar. Bilgiyi muhafaza etmesi gereken agent'lar olusturmak icin ADK'nin Session, State ve Memory kavramlarini iyi anlamak hayati onem tasir.

Insanlar arasi etkilesimlerde oldugu gibi, agent'lar da tutarli ve dogal konusmalar yurutebilmek icin onceki alismverislerini hatirlayabilme yetenegine ihtiyac duyar. ADK, baglam yonetimini uc temel kavram ve bunlarin iliskili hizmetleri araciligiyla basitletirir.

Bir agent ile her etkilesim, benzersiz bir konusma dizisi olarak dusunulebilir. Agent'lar onceki etkilesimlerden verilere erismek zorunda kalabilir. ADK bunu su sekilde yapilandirir:

* **Session:** Belirli bir etkilesim icin mesajlari ve eylemleri (Event) kaydeden, ayrica o konusmaya ozgu gecici verileri (State) saklayan bireysel bir sohbet dizisi.
* **State (`session.state`):** Bir Session icinde saklanan, yalnizca mevcut aktif sohbet dizisiyle ilgili bilgileri iceren veriler.
* **Memory:** Cesitli gecmis sohbetlerden veya harici kaynaklardan elde edilen bilgilerin aranabilir bir deposu; anlik konusmanin otesinde veri erisimi icin bir kaynak gorevi gorur.

ADK, karmasik, durumlu ve baglam duyarli agent'lar olusturmak icin kritik bilesenlerI yonetmeye yonelik ozel hizmetler sunar. SessionService, sohbet dizilerini (Session nesnelerini) yoneterek baslatma, kayit ve sonlandirma islemlerini yurutur; MemoryService ise uzun sureli bilginin (Memory) saklanmasini ve alinmasini denetler.

Hem SessionService hem de MemoryService, kullanicilarin uygulama ihtiyaclarina gore depolama yontemlerini secmesine olanak taniyan cesitli yapilandirma secenekleri sunar. Test amaciyla bellek ici secenekler mevcuttur, ancak veriler yeniden baslatma islemlerinde kaybolur. Kalici depolama ve olceklenebilirlik icin ADK ayrica veritabani ve bulut tabanli hizmetleri de destekler.

### Session: Her Sohbeti Takip Etme

ADK'deki bir Session nesnesi, bireysel sohbet dizilerini takip etmek ve yonetmek icin tasarlanmistir. Bir agent ile konusma basladiginda, SessionService bir Session nesnesi olusturur ve bu `google.adk.sessions.Session` olarak temsil edilir. Bu nesne, belirli bir konusma dizisine ait tum verileri kapsar: benzersiz tanimlayicilar (`id`, `app_name`, `user_id`), Event nesneleri olarak kronolojik bir olay kaydi, state olarak bilinen oturuma ozgu gecici veriler icin bir depolama alani ve son guncellemeyi gosteren bir zaman damgasi (`last_update_time`). Gelistiriciler genellikle Session nesneleriyle SessionService araciligiyla dolayli olarak etkilesir. SessionService, konusma oturumlarinin yasam dongusunu yonetmekten sorumludur; bu, yeni oturumlar baslatmayi, onceki oturumlari suridurmeyi, oturum aktivitesini (durum guncellemeleri dahil) kaydetmeyi, aktif oturumlari tanimayi ve oturum verilerinin kaldirilmasini yonetmeyi icerir. ADK, oturum gecmisi ve gecici veriler icin cesitli depolama mekanizmalarina sahip birkac SessionService uygulamasi sunar; ornegin, test icin uygun olan ancak uygulama yeniden baslatmalarinda veri kaliciligi saglamayan InMemorySessionService bunlardan biridir.

```python
# Example: Using InMemorySessionService
# This is suitable for local development and testing where data
# persistence across application restarts is not required.
from google.adk.sessions import InMemorySessionService
session_service = InMemorySessionService()
```

Ardindan, yonettiginiz bir veritabanina guvenilir bir sekilde kaydetmek istiyorsaniz DatabaseSessionService vardir.

```python
# Example: Using DatabaseSessionService
# This is suitable for production or development requiring persistent storage.
# You need to configure a database URL (e.g., for SQLite, PostgreSQL, etc.).
# Requires: pip install google-adk[sqlalchemy] and a database driver (e.g., psycopg2 for PostgreSQL)
from google.adk.sessions import DatabaseSessionService
# Example using a local SQLite file:
db_url = "sqlite:///./my_agent_data.db"
session_service = DatabaseSessionService(db_url=db_url)
```

Buna ek olarak, Google Cloud uzerinde olceklenebilir uretim icin Vertex AI altyapisini kullanan VertexAiSessionService bulunmaktadir.

```python
# Example: Using VertexAiSessionService
# This is suitable for scalable production on Google Cloud Platform, leveraging
# Vertex AI infrastructure for session management.
# Requires: pip install google-adk[vertexai] and GCP setup/authentication

from google.adk.sessions import VertexAiSessionService


PROJECT_ID = "your-gcp-project-id"  # Replace with your GCP project ID
LOCATION = "us-central1"  # Replace with your desired GCP location

# The app_name used with this service should correspond to the Reasoning Engine ID or name
REASONING_ENGINE_APP_NAME = (
    "projects/your-gcp-project-id/locations/us-central1/reasoningEngines/your-engine-id"
)  # Replace with your Reasoning Engine resource name

session_service = VertexAiSessionService(project=PROJECT_ID, location=LOCATION)

# When using this service, pass REASONING_ENGINE_APP_NAME to service methods:
# session_service.create_session(app_name=REASONING_ENGINE_APP_NAME, ...)
# session_service.get_session(app_name=REASONING_ENGINE_APP_NAME, ...)
# session_service.append_event(session, event, app_name=REASONING_ENGINE_APP_NAME)
# session_service.delete_session(app_name=REASONING_ENGINE_APP_NAME, ...)
```

Uygun bir SessionService secimi, agent'in etkilesim gecmisinin ve gecici verilerinin nasil saklandigini ve kaliciligini belirledigi icin kritik oneme sahiptir.

Her mesaj alisverisi dongusel bir sureci icerir: Bir mesaj alinir, Runner SessionService kullanarak bir Session alir veya olusturur, agent Session'in baglamini (durum ve gecmis etkilesimler) kullanarak mesaji isler, agent bir yanit uretir ve durumu guncelleyebilir, Runner bunu bir Event olarak kapsullar ve `session_service.append_event` yontemi yeni olayi kaydedip durumu depoda gunceller. Session daha sonra bir sonraki mesaji bekler. Ideal olarak, etkilesim sona erdiginde oturumu sonlandirmak icin `delete_session` yontemi kullanilir. Bu surec, SessionService'in Session'a ozgu gecmisi ve gecici verileri yoneterek surekliligi nasil sagledigini gostermektedir.

### State: Session'in Not Defteri

ADK'de her Session, yani sohbet dizisi, o belirli konusma suresi boyunca agent'in gecici calisma bellegi islevini goren bir state bileseni icerir. session.events tum sohbet gecmisini kaydederken, session.state aktif sohbete iliskin dinamik veri noktalarini saklar ve gunceller.

Temel olarak session.state bir sozluk (dictionary) olarak calisir ve verileri anahtar-deger ciftleri seklinde saklar. Ana islevi, agent'in tutarli diyalog icin gerekli ayrintilari (kullanici tercihleri, gorev ilerlemesi, artimli veri toplama veya sonraki agent eylemlerini etkileyen kosullu isaretler gibi) muhafaza etmesini ve yonetmesini saglamaktir.

State'in yapisi, seriletirebilir Python turleriyle (string, sayi, boolean, liste ve bu temel turleri iceren sozlukler) eslestirilen dize anahtarlarindan olusur. State dinamiktir ve konusma boyunca gelisir. Bu degisikliklerin kaliciligi, yapilandirilan SessionService'e baglidir.

State organizasyonu, veri kapsamini ve kaliciligini tanimlamak icin anahtar on ekleri kullanilarak saglanabilir. On eksiz anahtarlar oturuma ozeldir.

* user: on eki, verileri tum oturumlarda bir kullanici kimligiyle iliskilendirir.
* app: on eki, uygulamanin tum kullanicilari arasinda paylasilan verileri belirtir.
* temp: on eki, yalnizca mevcut isleme turu icin gecerli olan ve kalici olarak saklanmayan verileri gosterir.

Agent, tum state verilerine tek bir session.state sozlugu araciligiyla erisir. SessionService veri alma, birlestirme ve kalicilik islemlerini yurutur. State, `session_service.append_event()` araciligiyla oturum gecmisine bir Event eklendiginde guncellenmelidir. Bu, dogru takibi, kalici hizmetlerde duzgun kaydetmeyi ve durum degisikliklerinin guvenli bir sekilde ele alinmasini saglar.

#### 1. Basit Yol: `output_key` Kullanimi (Agent Metin Yanitlari Icin)

Agent'inizin son metin yanitini dogrudan state'e kaydetmek istiyorsaniz bu en kolay yontemdir. LlmAgent'inizi yapilandirirken, kullanmak istediginiz output\_key'i belirtmeniz yeterlidir. Runner bunu gorur ve olayi eklerken yaniti state'e kaydetmek icin gerekli eylemleri otomatik olarak olusturur. `output_key` araciligiyla durum guncellemesini gosteren bir kod ornegine bakalim.

```python
# Import necessary classes from the Google Agent Developer Kit (ADK)
from google.adk.agents import LlmAgent
from google.adk.sessions import InMemorySessionService, Session
from google.adk.runners import Runner
from google.genai.types import Content, Part


# Define an LlmAgent with an output_key.
greeting_agent = LlmAgent(
 name="Greeter",
 model="gemini-2.0-flash",
 instruction="Generate a short, friendly greeting.",
 output_key="last_greeting",
)


# --- Setup Runner and Session ---
app_name, user_id, session_id = "state_app", "user1", "session1"

session_service = InMemorySessionService()

runner = Runner(
    agent=greeting_agent,
    app_name=app_name,
    session_service=session_service,
)

session = session_service.create_session(
    app_name=app_name,
    user_id=user_id,
    session_id=session_id,
)

print(f"Initial state: {session.state}")


# --- Run the Agent ---
user_message = Content(parts=[Part(text="Hello")])

print("\n--- Running the agent ---")
for event in runner.run(
    user_id=user_id,
    session_id=session_id,
    new_message=user_message,
):
    if event.is_final_response():
        print("Agent responded.")


# --- Check Updated State ---
# Correctly check the state after the runner has finished processing all events.
updated_session = session_service.get_session(app_name, user_id, session_id)
print(f"\nState after agent run: {updated_session.state}")
```

Arka planda Runner, `output_key`'inizi gorur ve `append_event` cagrisinda gerekli eylemleri bir `state_delta` ile otomatik olarak olusturur.

#### 2. Standart Yol: `EventActions.state_delta` Kullanimi (Daha Karmasik Guncellemeler Icin)

Birden fazla anahtari ayni anda guncellemek, yalnizca metin olmayan seyleri kaydetmek, user: veya app: gibi belirli kapsanlari hedeflemek veya agent'in son metin yanitina bagli olmayan guncellemeler yapmak gibi daha karmasik islemler yapmaniz gerektiginde, durum degisikliklerinizin bir sozlugunu (`state_delta`) manuel olarak olusturur ve bunu eklediginiz Event'in EventActions'i icine dahil edersiniz. Bir ornege bakalim:

```python
import time

from google.adk.tools.tool_context import ToolContext
from google.adk.sessions import InMemorySessionService


# --- Define the Recommended Tool-Based Approach ---
def log_user_login(tool_context: ToolContext) -> dict:
    """
    Updates the session state upon a user login event.
    This tool encapsulates all state changes related to a user login.

    Args:
        tool_context: Automatically provided by ADK, gives access to session state.

    Returns:
        A dictionary confirming the action was successful.
    """
    # Access the state directly through the provided context.
    state = tool_context.state

    # Get current values or defaults, then update the state.
    # This is much cleaner and co-locates the logic.
    login_count = state.get("user:login_count", 0) + 1
    state["user:login_count"] = login_count
    state["task_status"] = "active"
    state["user:last_login_ts"] = time.time()
    state["temp:validation_needed"] = True

    print("State updated from within the `log_user_login` tool.")

    return {
        "status": "success",
        "message": f"User login tracked. Total logins: {login_count}.",
    }


# --- Demonstration of Usage ---
# In a real application, an LLM Agent would decide to call this tool.
# Here, we simulate a direct call for demonstration purposes.

# 1. Setup
session_service = InMemorySessionService()
app_name, user_id, session_id = "state_app_tool", "user3", "session3"

session = session_service.create_session(
    app_name=app_name,
    user_id=user_id,
    session_id=session_id,
    state={"user:login_count": 0, "task_status": "idle"},
)

print(f"Initial state: {session.state}")

# 2. Simulate a tool call (in a real app, the ADK Runner does this)
# We create a ToolContext manually just for this standalone example.
from google.adk.tools.tool_context import InvocationContext

mock_context = ToolContext(
    invocation_context=InvocationContext(
        app_name=app_name,
        user_id=user_id,
        session_id=session_id,
        session=session,
        session_service=session_service,
    )
)

# 3. Execute the tool
log_user_login(mock_context)

# 4. Check the updated state
updated_session = session_service.get_session(app_name, user_id, session_id)
print(f"State after tool execution: {updated_session.state}")

# Expected output will show the same state change as the "Before" case,
# but the code organization is significantly cleaner and more robust.
```

Bu kod, bir uygulamada kullanici oturum durumunu yonetmek icin arac tabanli bir yaklasimi gostermektedir. Bir arac olarak islev goren *log_user_login* fonksiyonunu tanimlar. Bu arac, bir kullanici giris yaptiginda oturum durumunu guncellemekten sorumludur.
Fonksiyon, oturumun state sozlugune erismek ve onu degistirmek icin ADK tarafindan saglanan bir ToolContext nesnesi alir. Aracin icinde *user:login_count* degerini arttirir, *task_status*'u "active" olarak ayarlar, *user:last_login_ts (zaman damgasi)* kaydeder ve gecici bir temp:validation\_needed isareti ekler.

Kodun gosterim bolumu, bu aracin nasil kullanilacagini simule eder. Bir bellek ici oturum hizmeti kurar ve onceden tanimlanmis bazi durumlarla bir baslangic oturumu olusturur. Daha sonra ADK Runner'in araci calistirma ortamini taklit etmek icin bir ToolContext manuel olarak olusturulur. `log_user_login` fonksiyonu bu sahte baglamla cagrilir. Son olarak, kod durumun aracin yurutulmesiyle guncellenmis oldugunu gostermek icin oturumu tekrar alir. Amac, durum degisikliklerini araclar icinde kapsullemenin, araclar disinda dogrudan durum manipulasyonuna kiyasla kodu nasil daha temiz ve daha duzenlI hale getirdigini gostermektir.

Bir oturum aldiktan sonra `session.state` sozlugunu dogrudan degistirmenin kesinlikle tavsiye edilmedigini unutmayin; cunku bu, standart olay isleme mekanizmasini atlar. Bu tur dogrudan degisiklikler oturumun olay gecmisinde kaydedilmez, secilen `SessionService` tarafindan kalici olarak saklanmayabilir, es zamanlilik sorunlarina yol acabilir ve zaman damgalari gibi temel meta verileri guncellemez. Oturum durumunu guncellemek icin onerilen yontemler, bir `LlmAgent` uzerinde `output_key` parametresini kullanmak (ozellikle agent'in son metin yanitlari icin) veya `session_service.append_event()` araciligiyla bir olay eklerken `EventActions.state_delta` icinde durum degisikliklerini dahil etmektir. `session.state` oncelikle mevcut verileri okumak icin kullanilmalidir.

Ozetlemek gerekirse, durumunuzu tasarlarken basit tutun, temel veri turlerini kullanin, anahtarlariniza net isimler verin ve on ekleri dogru kullanin, derin ic ice gecmeden kacinin ve durumu her zaman append\_event sureci kullanarak guncelleyin.

## Memory: MemoryService ile Uzun Sureli Bilgi

Agent sistemlerinde Session bileseni, tek bir konusmaya ozgu mevcut sohbet gecmisinin (event'ler) ve gecici verilerin (state) bir kaydini tutar. Ancak agent'larin birden fazla etkilesim boyunca bilgiyi muhafaza etmesi veya harici verilere erismesi icin uzun sureli bilgi yonetimi gereklidir. Bu, MemoryService tarafindan saglanir.

```python
# Example: Using InMemoryMemoryService
# This is suitable for local development and testing where data
# persistence across application restarts is not required.
# Memory content is lost when the app stops.

from google.adk.memory import InMemoryMemoryService

memory_service = InMemoryMemoryService()
```

Session ve State, tek bir sohbet oturumu icin kisa sureli bellek olarak kavramsallastirilabilirken, MemoryService tarafindan yonetilen Uzun Sureli Bilgi kalici ve aranabilir bir depo olarak isler. Bu depo, birden fazla gecmis etkilesimden veya harici kaynaklardan bilgi icerebilir. BaseMemoryService arayuzu tarafindan tanimlanan MemoryService, bu aranabilir, uzun sureli bilgiyi yonetmek icin bir standart olusturur. Temel islevleri sunlardir: bilgi ekleme (bir oturumdan icerik cikararak add\_session\_to\_memory yontemiyle saklama) ve bilgi alma (agent'in depoyu sorgulamasina ve search\_memory yontemiyle ilgili verileri almasina olanak tanima).

ADK, bu uzun sureli bilgi deposunu olusturmak icin birkac uygulama sunar. InMemoryMemoryService, test amacli uygun gecici bir depolama cozumu saglar, ancak veriler uygulama yeniden baslatmalarinda korunmaz. Uretim ortamlari icin genellikle VertexAiRagMemoryService kullanilir. Bu hizmet, Google Cloud'un Retrieval Augmented Generation (RAG) hizmetinden yararlanarak olceklenebilir, kalici ve anlamsal arama yetenekleri saglar (ayrica RAG hakkindaki Bolum 14'e bakiniz).

```python
# Example: Using VertexAiRagMemoryService
# This is suitable for scalable production on GCP, leveraging
# Vertex AI RAG (Retrieval Augmented Generation) for persistent,
# searchable memory.
# Requires: pip install google-adk[vertexai], GCP
# setup/authentication, and a Vertex AI RAG Corpus.

from google.adk.memory import VertexAiRagMemoryService


# The resource name of your Vertex AI RAG Corpus
RAG_CORPUS_RESOURCE_NAME = (
    "projects/your-gcp-project-id/locations/us-central1/ragCorpora/your-corpus-id"
)  # Replace with your Corpus resource name

# Optional configuration for retrieval behavior
SIMILARITY_TOP_K = 5  # Number of top results to retrieve
VECTOR_DISTANCE_THRESHOLD = 0.7  # Threshold for vector similarity

memory_service = VertexAiRagMemoryService(
    rag_corpus=RAG_CORPUS_RESOURCE_NAME,
    similarity_top_k=SIMILARITY_TOP_K,
    vector_distance_threshold=VECTOR_DISTANCE_THRESHOLD,
)

# When using this service, methods like add_session_to_memory
# and search_memory will interact with the specified Vertex AI
# RAG Corpus.
```

## Uygulamali Kod: LangChain ve LangGraph ile Bellek Yonetimi

LangChain ve LangGraph'te Memory, akilli ve dogal hissettiren konusma uygulamalari olusturmak icin kritik bir bilesendir. Bir yapay zeka agent'inin gecmis etkilesimlerden bilgi hatirlamasina, geri bildirimlerden ogrenmesine ve kullanici tercihlerine uyum saglamasina olanak tanir. LangChain'in bellek ozelligi, mevcut prompt'lari zenginlestirmek icin saklanan bir gecmise referans vererek ve ardindan en son alisverisi gelecekte kullanmak uzere kaydederek bunun temelini saglar. Agent'lar daha karmasik gorevleri ustlendikce, bu yetenek hem verimlilik hem de kullanici memnuniyeti icin vazgecilmez hale gelir.

**Kisa Sureli Bellek:** Thread kapsamlidir, yani tek bir oturum veya thread icindeki devam eden konusmayi takip eder. Anlik baglam saglar, ancak tam bir gecmis LLM'in context window'unu zorlayabilir ve bu da hatalara veya dusuk performansa yol acabilir. LangGraph, kisa sureli bellegi agent'in durumunun bir parcasi olarak yonetir ve bu durum bir checkpointer araciligiyla kalici hale getirilir, boylece bir thread herhangi bir zamanda devam ettirilebilir.

**Uzun Sureli Bellek:** Oturumlar arasinda kullaniciya ozel veya uygulama duzeyi verileri saklar ve konusma thread'leri arasinda paylasilir. Ozel "namespace"'lerde kaydedilir ve herhangi bir zamanda herhangi bir thread'de geri cagrilabilir. LangGraph, uzun sureli bellekleri kaydetmek ve geri cagirmak icin store'lar saglayarak agent'larin bilgiyi suresiz olarak muhafaza etmesine olanak tanir.

LangChain, konusma gecmisini yonetmek icin manuel kontrolden zincirler icindeki otomatik entegrasyona kadar cesitli araclar sunar.

**ChatMessageHistory: Manuel Bellek Yonetimi.** Resmi bir zincir disinda bir konusmanin gecmisi uzerinde dogrudan ve basit kontrol icin ChatMessageHistory sinifi idealdir. Diyalog alisverislerinin manuel olarak takip edilmesine olanak tanir.

```python
from langchain.memory import ChatMessageHistory


# Initialize the history object
history = ChatMessageHistory()

# Add user and AI messages
history.add_user_message("I'm heading to New York next week.")
history.add_ai_message("Great! It's a fantastic city.")

# Access the list of messages
print(history.messages)
```

**ConversationBufferMemory: Zincirler Icin Otomatik Bellek.** Bellegi dogrudan zincirlere entegre etmek icin ConversationBufferMemory yaygin bir tercihdir. Konusmanin bir tamponunu tutar ve bunu prompt'unuza sunar. Davranisi iki temel parametreyle ozellestirilebilir:

* `memory_key`: Prompt'unuzda sohbet gecmisini tutacak degisken adini belirleyen bir dize. Varsayilan degeri "history"dir.
* `return_messages`: Gecmisin formatini belirleyen bir boolean.
  * `False` (varsayilan) ise, standart LLM'ler icin ideal olan tek bir formatlanmis dize dondurur.
  * `True` ise, Chat Model'ler icin onerilen format olan bir mesaj nesneleri listesi dondurur.

```python
from langchain.memory import ConversationBufferMemory


# Initialize memory
memory = ConversationBufferMemory()

# Save a conversation turn
memory.save_context(
    {"input": "What's the weather like?"},
    {"output": "It's sunny today."},
)

# Load the memory as a string
print(memory.load_memory_variables({}))
```

Bu bellegi bir LLMChain'e entegre etmek, modelin konusma gecmisine erismesini ve baglamsal olarak uygun yanitlar vermesini saglar.

```python
from langchain_openai import OpenAI
from langchain.chains import LLMChain
from langchain.prompts import PromptTemplate
from langchain.memory import ConversationBufferMemory


# 1. Define LLM and Prompt
llm = OpenAI(temperature=0)

template = """You are a helpful travel agent.
Previous conversation: {history}
New question: {question}
Response:"""
prompt = PromptTemplate.from_template(template)

# 2. Configure Memory
# The memory_key "history" matches the variable in the prompt
memory = ConversationBufferMemory(memory_key="history")

# 3. Build the Chain
conversation = LLMChain(llm=llm, prompt=prompt, memory=memory)

# 4. Run the Conversation
response = conversation.predict(question="I want to book a flight.")
print(response)

response = conversation.predict(question="My name is Sam, by the way.")
print(response)

response = conversation.predict(question="What was my name again?")
print(response)
```

Chat modelleri ile daha etkili sonuclar icin `return_messages=True` ayarlayarak yapilandirilmis bir mesaj nesneleri listesi kullanilmasi onerilir.

```python
from langchain_openai import ChatOpenAI
from langchain.chains import LLMChain
from langchain.memory import ConversationBufferMemory
from langchain_core.prompts import (
    ChatPromptTemplate,
    MessagesPlaceholder,
    SystemMessagePromptTemplate,
    HumanMessagePromptTemplate,
)


# 1. Define Chat Model and Prompt
llm = ChatOpenAI()

prompt = ChatPromptTemplate(
    messages=[
        SystemMessagePromptTemplate.from_template("You are a friendly assistant."),
        MessagesPlaceholder(variable_name="chat_history"),
        HumanMessagePromptTemplate.from_template("{question}"),
    ]
)

# 2. Configure Memory
# return_messages=True is essential for chat models
memory = ConversationBufferMemory(memory_key="chat_history", return_messages=True)

# 3. Build the Chain
conversation = LLMChain(llm=llm, prompt=prompt, memory=memory)

# 4. Run the Conversation
response = conversation.predict(question="Hi, I'm Jane.")
print(response)

response = conversation.predict(question="Do you remember my name?")
print(response)
```

**Uzun Sureli Bellek Turleri**: Uzun sureli bellek, sistemlerin farkli konusmalar arasinda bilgiyi muhafaza etmesine olanak taniyarak daha derin bir baglam ve kisiselleistirme duzeyi saglar. Insan bellegine benzer sekilde uc ture ayrilabilir:

* **Anlamsal Bellek (Semantic Memory): Gercekleri Hatirlamak:** Kullanici tercihleri veya alan bilgisi gibi belirli gercekleri ve kavramlari muhafaza etmeyi icerir. Bir agent'in yanitlarini temellendiirmek icin kullanilir ve daha kisisellesirilmis ve ilgili etkilesimlere yol acar. Bu bilgi, surekli guncellenen bir kullanici "profili" (bir JSON belgesi) veya bireysel olgusal belgelerin bir "koleksiyonu" olarak yonetilebilir.
* **Episodik Bellek (Episodic Memory): Deneyimleri Hatirlamak:** Gecmis olaylari veya eylemleri hatirlmayi icerir. Yapay zeka agent'lari icin episodik bellek, genellikle bir gorevi nasil yerine getireceginI hatirlamak icin kullanilir. Pratikte, genellikle few-shot example prompting araciligiyla uygulanir; burada agent, gorevleri dogru bir sekilde yerine getirmek icin gecmis basarili etkilesim dizilerinden ogrenir.
* **Prosedurel Bellek (Procedural Memory): Kurallari Hatirlamak:** Gorevlerin nasil yapilacagina dair bellek -- agent'in temel talimatlari ve davranislari, genellikle system prompt'unda yer alir. Agent'larin uyum saglamak ve gelismek icin kendi prompt'larini degistirmesi yaygindir. Etkili bir teknik "Yansitma (Reflection)"dir; burada agent mevcut talimatlari ve son etkilesimleriyle yonlendirilir, ardindan kendi talimatlarini iyilestirmesi istenir.

Asagida, bir agent'in LangGraph BaseStore'da saklanan prosedurel bellegini guncellemek icin yansitmayi nasil kullanabilecegini gosteren sozde kod yer almaktadir.

```python
# Node that updates the agent's instructions
def update_instructions(state: State, store: BaseStore):
    namespace = ("instructions",)

    # Get the current instructions from the store
    current_instructions = store.search(namespace)[0]

    # Create a prompt to ask the LLM to reflect on the conversation
    # and generate new, improved instructions
    prompt = prompt_template.format(
        instructions=current_instructions.value["instructions"],
        conversation=state["messages"],
    )

    # Get the new instructions from the LLM
    output = llm.invoke(prompt)
    new_instructions = output["new_instructions"]

    # Save the updated instructions back to the store
    store.put(("agent_instructions",), "agent_a", {"instructions": new_instructions})


# Node that uses the instructions to generate a response
def call_model(state: State, store: BaseStore):
    namespace = ("agent_instructions",)

    # Retrieve the latest instructions from the store
    instructions = store.get(namespace, key="agent_a")[0]

    # Use the retrieved instructions to format the prompt
    prompt = prompt_template.format(
        instructions=instructions.value["instructions"]
    )
    # ... application logic continues
```

LangGraph, uzun sureli bellekleri bir store'da JSON belgeleri olarak saklar. Her bellek, ozel bir namespace (bir klasor gibi) ve ayri bir key (bir dosya adi gibi) altinda duzenlenir. Bu hiyerarsik yapi, bilginin kolay organizasyonunu ve alinmasini saglar. Asagidaki kod, InMemoryStore kullanarak bellekleri put, get ve search islemlerinin nasil yapilacagini gostermektedir.

```python
from langgraph.store.memory import InMemoryStore


# A placeholder for a real embedding function
def embed(texts: list[str]) -> list[list[float]]:
    # In a real application, use a proper embedding model
    return [[1.0, 2.0] for _ in texts]


# Initialize an in-memory store. For production, use a database-backed store.
store = InMemoryStore(index={"embed": embed, "dims": 2})

# Define a namespace for a specific user and application context
user_id = "my-user"
application_context = "chitchat"
namespace = (user_id, application_context)

# 1. Put a memory into the store
store.put(
    namespace,
    "a-memory",  # The key for this memory
    {
        "rules": [
            "User likes short, direct language",
            "User only speaks English & python",
        ],
        "my-key": "my-value",
    },
)

# 2. Get the memory by its namespace and key
item = store.get(namespace, "a-memory")
print("Retrieved Item:", item)

# 3. Search for memories within the namespace, filtering by content
# and sorting by vector similarity to the query.
items = store.search(
    namespace,
    filter={"my-key": "my-value"},
    query="language preferences",
)
print("Search Results:", items)
```

## Vertex Memory Bank

Memory Bank, Vertex AI Agent Engine icerisindeki yonetilen bir hizmettir ve agent'lara kalici, uzun sureli bellek saglar. Bu hizmet, temel gercekleri ve kullanici tercihlerini cikarmak icin konusma gecmislerini asenkron olarak analiz etmek uzere Gemini modellerini kullanir.

Bu bilgiler kalici olarak saklanir, kullanici kimligi gibi tanimli bir kapsama gore duzenlenir ve yeni verileri birlestiirmek ve celiskileri cozmek icin akilli bir sekilde guncellenir. Yeni bir oturum basladiginda agent, embedding'ler kullanarak tam veri cagirma veya benzerlik aramasi yoluyla ilgili bellekleri alir. Bu surec, bir agent'in oturumlar arasinda surekliligi surdurmesine ve hatirlanan bilgilere dayali olarak yanitlari kisisellestirmesine olanak tanir.

Agent'in runner'i, once baslatilan VertexAiMemoryBankService ile etkilesir. Bu hizmet, agent'in konusmalari sirasinda uretilen belleklerin otomatik olarak saklanmasini yonetir. Her bellek, gelecekte dogru bir sekilde alinabilmesi icin benzersiz bir USER\_ID ve APP\_NAME ile etiketlenir.

```python
from google.adk.memory import VertexAiMemoryBankService


agent_engine_id = agent_engine.api_resource.name.split("/")[-1]

memory_service = VertexAiMemoryBankService(
    project="PROJECT_ID",
    location="LOCATION",
    agent_engine_id=agent_engine_id,
)

session = await session_service.get_session(
    app_name=app_name,
    user_id="USER_ID",
    session_id=session.id,
)

await memory_service.add_session_to_memory(session)
```

Memory Bank, Google ADK ile sorunsuz entegrasyon sunarak aninda kullanima hazir bir deneyim saglar. LangGraph ve CrewAI gibi diger agent framework'lerinin kullanicilari icin Memory Bank, dogrudan API cagrilari araciligiyla da destek sunar. Bu entegrasyonlari gosteren cevrimici kod ornekleri ilgilenen okuyucular icin hazir bulunmaktadir.

## Bir Bakista

**Ne**: Agentic sistemler, karmasik gorevleri yerine getirmek ve tutarli deneyimler sunmak icin gecmis etkilesimlerden bilgiyi hatirlama ihtiyaci duyar. Bir bellek mekanizmasi olmadan agent'lar durumsuz (stateless) kalir, konusma baglamini surduremez, deneyimlerden ogrenemez veya kullanicilar icin yanitlari kisisellesitiremez. Bu, onlari temelden basit, tek seferlik etkilesimlerle sinirlar ve cok adimli surecleri veya degisen kullanici ihtiyaclarini karsıilayamazlar. Temel sorun, tek bir konusmanin anlik, gecici bilgisi ile zaman icinde toplanan genis, kalici bilginin nasil etkili bir sekilde yonetilecegdir.

**Neden:** Standartlastirilmis cozum, kisa sureli ve uzun sureli depolamayi birbirinden ayiran ikili bir bellek sistemi uygulamaktir. Kisa sureli, baglamsal bellek, konusma akisini surdurmek icin LLM'in context window'u icindeki son etkilesim verilerini tutar. Kalici olmasi gereken bilgiler icin uzun sureli bellek cozumleri, verimli ve anlamsal erisim icin genellikle vector store'lar olan harici veritabanlarini kullanir. Google ADK gibi agentic framework'ler, bunu yonetmek icin Session (konusma dizisi) ve State (gecici verileri) gibi ozel bilesenler saglar. Uzun sureli bilgi tabanıyla arayuz olusturmak icin ozel bir MemoryService kullanilir ve agent'in ilgili gecmis bilgileri alip mevcut baglamina dahil etmesine olanak tanir.

**Temel kural:** Bu kalıbi, bir agent'in tek bir soruyu yanıtlamaktan daha fazlasini yapmasi gerektiginde kullanin. Bir konusma boyunca baglami surdurmesi, cok adimli gorevlerde ilerlemeyi takip etmesi veya kullanici tercihlerini ve gecmisini hatirlayarak etkilesimleri kisisellestirmesi gereken agent'lar icin vazgecilmezdir. Agent'in gecmis basarilar, basarisizliklar veya yeni edinilen bilgilere dayali olarak ogrenmesi veya uyum saglamasi beklendiginde bellek yonetimini uygulayin.

**Gorsel ozet:**

![Memory Management Design Pattern](../assets/Memory_Management_Design_Pattern.png)

Sekil 1: Bellek yonetimi tasarim kalibi (Memory Management Design Pattern)

## Temel Cikarimlar

Bellek yonetimi hakkindaki ana noktalarin hizli bir ozeti:

* Bellek, agent'larin bilgiyi takip etmesi, ogrenmesi ve etkilesimleri kisisellestirmesi icin son derece onemlidir.
* Konusma tabanli yapay zeka, tek bir sohbet icindeki anlik baglam icin kisa sureli bellege ve birden fazla oturum arasindaki kalici bilgi icin uzun sureli bellege dayanir.
* Kisa sureli bellek (anlik bilgiler) gecicidir ve genellikle LLM'in context window'u veya framework'un baglami nasil aktardigiyla sinirlidir.
* Uzun sureli bellek (kalici bilgiler) farkli sohbetler arasindaki bilgileri vector database'ler gibi harici depolama kullanarak kaydeder ve arama yoluyla erisiilir.
* ADK gibi framework'ler, bellegi yonetmek icin Session (sohbet dizisi), State (gecici sohbet verileri) ve MemoryService (aranabilir uzun sureli bilgi) gibi belirli parcalara sahiptir.
* ADK'nin SessionService'i, gecmisi (event'ler) ve gecici verileri (state) dahil olmak uzere bir sohbet oturumunun tum yasam dongusunu yonetir.
* ADK'nin session.state'i gecici sohbet verileri icin bir sozluktur. On ekler (user:, app:, temp:) verinin nereye ait oldugunu ve kalici olup olmadigini gosterir.
* ADK'de durum, state sozlugunu dogrudan degistirmek yerine event eklerken EventActions.state\_delta veya output\_key kullanilarak guncellenmelidir.
* ADK'nin MemoryService'i bilgileri uzun sureli depoya koymak ve agent'larin genellikle araclar kullanarak aramasini saglamak icindir.
* LangChain, tek bir konusmanin gecmisini otomatik olarak prompt'a enjekte etmek icin ConversationBufferMemory gibi pratik araclar sunarak agent'in anlik baglami hatirlamasini saglar.
* LangGraph, farkli kullanici oturumlari arasinda anlamsal gercekleri, episodik deneyimleri ve hatta guncellenebilir prosedurel kurallari kaydetmek ve almak icin bir store kullanarak gelismis, uzun sureli bellegi mumkun kilar.
* Memory Bank, agent'lara kalici, uzun sureli bellek saglayan yonetilen bir hizmettir; kullaniciya ozel bilgileri otomatik olarak cikarip saklayarak ve geri cagirarak Google ADK, LangGraph ve CrewAI gibi framework'ler arasinda kisisellesitirilmis, surekli konusmalari mumkun kilar.

## Sonuc

Bu bolum, agent sistemleri icin bellek yonetiminin gercekten onemli gorevini ele alarak kisa omurlu baglam ile uzun sure kalici olan bilgi arasindaki farki ortaya koydu. Bu bellek turlerinin nasil yapilandirildigini ve bilgi hatırlayabilen daha akilli agent'lar olusturmada nerelerde kullanildigini konustuk. Google ADK'nin Session, State ve MemoryService gibi belirli parcalariyla bunu nasil yonettiginize ayrintili bir sekilde baktik. Agent'larin hem kisa hem de uzun sureli olarak nasil bilgi hatırlayabilecegini ele aldigimiza gore, simdi nasil ogrenilebileceklerine ve uyum saglayabileceklerine gecebiliriz. Bir sonraki kalip olan "Ogrenme ve Uyum Saglama (Learning and Adaptation)", bir agent'in yeni deneyimlere veya verilere dayali olarak dusunme, hareket etme veya bildiklerini degistirmesi hakkindadir.

## Kaynaklar

1. ADK Memory, [https://google.github.io/adk-docs/sessions/memory/](https://google.github.io/adk-docs/sessions/memory/)
2. LangGraph Memory, [https://langchain-ai.github.io/langgraph/concepts/memory/](https://langchain-ai.github.io/langgraph/concepts/memory/)
3. Vertex AI Agent Engine Memory Bank, [https://cloud.google.com/blog/products/ai-machine-learning/vertex-ai-memory-bank-in-public-preview](https://cloud.google.com/blog/products/ai-machine-learning/vertex-ai-memory-bank-in-public-preview)
