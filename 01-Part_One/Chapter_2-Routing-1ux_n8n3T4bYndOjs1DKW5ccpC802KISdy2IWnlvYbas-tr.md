# Bolum 2: Yonlendirme (Routing)

## Yonlendirme Kalibina Genel Bakis

Prompt zincirleme yoluyla sirali isleme, dil modelleriyle deterministik, dogrusal is akislarini yurutmek icin temel bir teknik olsa da, uyarlanabilir yanitlar gerektiren senaryolarda uygulanabilirligi sinirlidir. Gercek dunyada agentic sistemler, genellikle ortamin durumu, kullanici girdisi veya onceki bir islemin sonucu gibi kosullu faktorlere dayanarak birden fazla potansiyel eylem arasinda karar vermek zorundadir. Farkli ozelesmis fonksiyonlara, araclara veya alt sureclere kontrol akisini yoneten bu dinamik karar verme kapasitesi, yonlendirme (Routing) olarak bilinen bir mekanizma araciligiyla saglanir.

Yonlendirme, bir agent'in operasyonel cercevesine kosullu mantik kazandirarak, sabit bir yurutme yolundan agent'in belirli kriterleri dinamik olarak degerlendirerek olasi sonraki eylemler kumesinden secim yaptigi bir modele gecisi mumkun kilar. Bu, daha esnek ve baglama duyarli sistem davranisina olanak tanir.

Ornegin, musteri sorgulari icin tasarlanmis bir agent, bir yonlendirme fonksiyonuyla donatildiginda, oncelikle gelen bir sorguyu siniflandirarak kullanicinin niyetini belirleyebilir. Bu siniflandirmaya dayanarak, sorguyu onceden belirlenmmis tek bir yanit yoluna varsayilan olarak yonlendirmek yerine, dogrudan soru yanitlama icin ozelesmis bir agent'a, hesap bilgileri icin bir veritabani erisim aracina veya karmasik sorunlar icin bir eskalasyon prosedurune yonlendirebilir. Bu nedenle, yonlendirme kullanan daha gelismis bir agent sunlari yapabilir:

1. Kullanicinin sorgusunu analiz etme.
2. Sorguyu *niyetine* gore **yonlendirme**:
   * Niyet "siparis durumu kontrol" ise, siparis veritabaniyla etkilesime giren bir alt agent'a veya arac zincirine yonlendirme.
   * Niyet "urun bilgisi" ise, urun katalogunu arayan bir alt agent'a veya zincire yonlendirme.
   * Niyet "teknik destek" ise, sorun giderme kilavuzlarina erisen veya bir insana eskalasyon yapan farkli bir zincire yonlendirme.
   * Niyet belirsiz ise, bir aciklama alt agent'ina veya prompt zincirine yonlendirme.

Yonlendirme kalibinin temel bileseni, degerlendirmeyi gerceklestiren ve akisi yonlendiren bir mekanizmadir. Bu mekanizma cesitli yollarla uygulanabilir:

* **LLM Tabanli Yonlendirme:** Dil modelinin kendisi, girdiyi analiz etmesi ve sonraki adimi veya hedefi gosteren belirli bir tanimlayici veya talimat cikti olarak uretmesi icin prompt'lanabilir. Ornegin, bir prompt LLM'den "Asagidaki kullanici sorgusunu analiz edin ve yalnizca kategoriyi cikti olarak verin: 'Siparis Durumu', 'Urun Bilgisi', 'Teknik Destek' veya 'Diger'" seklinde isteyebilir. Agentic sistem daha sonra bu ciktiyi okur ve is akisini buna gore yonlendirir.
* **Embedding Tabanli Yonlendirme:** Girdi sorgusu bir vektor embedding'e donusturulur (bkz. RAG, Bolum 14). Bu embedding daha sonra farkli rotalari veya yetenekleri temsil eden embedding'lerle karsilastirilir. Sorgu, embedding'i en benzer olan rotaya yonlendirilir. Bu, kararin yalnizca anahtar kelimelere degil, girdinin anlamina dayandigi semantik yonlendirme icin faydalidir.
* **Kural Tabanli Yonlendirme:** Bu, girdiden cikarilan anahtar kelimelere, kaliplara veya yapilandirilmis verilere dayali onceden tanimlanmis kurallarin veya mantigin (ornegin if-else ifadeleri, switch case'leri) kullanilmasini icerir. Bu, LLM tabanli yonlendirmeden daha hizli ve daha deterministik olabilir, ancak nüansli veya yeni girdileri ele almak icin daha az esnektir.
* **Makine Ogrenmesi Model Tabanli Yonlendirme:** Bir yonlendirme gorevi gerceklestirmek icin kucuk bir etiketli veri kumeleri uzerinde ozellikle egitilmis bir ayristirici model, ornegin bir siniflandirici kullanir. Embedding tabanli yontemlerle kavramsal benzerlikler paylasmakla birlikte, temel ozelligi ozelesmis bir yonlendirme fonksiyonu olusturmak icin modelin parametrelerini ayarlayan denetimli ince ayar (fine-tuning) surecidir. Bu teknik, LLM tabanli yonlendirmeden farklidir cunku karar verme bileseni, cikarim zamaninda bir prompt yurutulen uretken bir model degildir. Bunun yerine, yonlendirme mantigi ince ayarli modelin ogrenilmis agirliklarinda kodlanmistir. LLM'ler, egitim setini zenginlestirmek icin sentetik veri olusturmak amaciyla bir on isleme adiminda kullanilabilir, ancak gercek zamanli yonlendirme kararinin kendisinde yer almazlar.

Yonlendirme mekanizmalari, bir agent'in operasyonel dongusu icerisinde birden fazla noktada uygulanabilir. Birincil bir gorevi siniflandirmak icin baslangicta, sonraki bir eylemi belirlemek icin bir isleme zinciri icerisindeki ara noktalarda veya verilen bir kumeden en uygun araci secmek icin bir alt rutin sirasinda uygulanabilirler.

LangChain, LangGraph ve Google'in Agent Developer Kit (ADK) gibi hesaplama cerceveleri, bu tur kosullu mantigi tanimlamak ve yonetmek icin acik yapilar saglar. Durum tabanli grafik mimarisiyle LangGraph, kararlarin tum sistemin biriken durumuna bagli oldugu karmasik yonlendirme senaryolari icin ozellikle uygundur. Benzer sekilde, Google'in ADK'si, yonlendirme mantiginin uygulanmasi icin temel olusturan bir agent'in yeteneklerini ve etkilesim modellerini yapilandirmak icin temel bilesenler saglar. Bu cerceveler tarafindan saglanan yurutme ortamlarinda, gelistiriciler olasi operasyonel yollari ve hesaplama grafigindeki dugumler arasindaki gecisleri belirleyen fonksiyonlari veya model tabanli degerlendirmeleri tanimlar.

Yonlendirmenin uygulanmasi, bir sistemin deterministik sirali islemenin otesine gecmesini saglar. Genis bir girdi ve durum degisikligi yelpazesine dinamik ve uygun sekilde yanit verebilen daha uyarlanabilir yurutme akislarinin gelistirilmesini kolaylastirir.

## Pratik Uygulamalar ve Kullanim Alanlari

Yonlendirme kalibi, uyarlanabilir agentic sistemlerin tasariminda kritik bir kontrol mekanizmasidir ve degisken girdilere ve dahili durumlara yanit olarak yurutme yolunu dinamik olarak degistirmelerini saglar. Faydasi, gerekli bir kosullu mantik katmani saglayarak birden fazla alana yayilir.

Sanal asistanlar veya yapay zeka destekli ogretmenler gibi insan-bilgisayar etkilesiminde, yonlendirme kullanici niyetini yorumlamak icin kullanilir. Dogal dil sorgusunun ilk analizi, belirli bir bilgi erisim aracini cagirma, bir insan operatore eskalasyon yapma veya kullanici performansina dayali bir mufredata sonraki modulu secme gibi en uygun sonraki eylemi belirler. Bu, sistemin dogrusal diyalog akislarinin otesine gecmesini ve baglamsal olarak yanit vermesini saglar.

Otomatik veri ve dokuman isleme pipeline'larinda, yonlendirme bir siniflandirma ve dagitim fonksiyonu gorevi gorur. Gelen veriler, e-postalar, destek talepleri veya API yükleri gibi, icerik, meta veri veya formata gore analiz edilir. Sistem daha sonra her bir ogeyi, bir satis potansiyeli alma sureci, JSON veya CSV formatlari icin belirli bir veri donusum fonksiyonu veya acil sorun eskalasyon yolu gibi ilgili bir is akisina yonlendirir.

Birden fazla ozelesmis arac veya agent iceren karmasik sistemlerde, yonlendirme ust duzey bir dagitici gorevi gorur. Arama, ozetleme ve analiz icin farkli agent'lardan olusan bir arastirma sistemi, mevcut hedefe gore gorevleri en uygun agent'a atamak icin bir yonlendirici kullanir. Benzer sekilde, yapay zeka kodlama asistani, bir kod parcasini dogru ozelesmis araca gecirmeden once programlama dilini ve kullanicinin niyetini -- hata ayiklama, aciklama veya ceviri -- belirlemek icin yonlendirme kullanir.

Sonuc olarak, yonlendirme islevsel olarak cesitli ve baglama duyarli sistemler olusturmak icin gerekli olan mantiksal karar verme kapasitesini saglar. Bir agent'i onceden tanimlanmis dizilerin statik bir yurutucusunden, degisen kosullar altinda bir gorevi gerceklestirmek icin en etkili yontem hakkinda kararlar verebilen dinamik bir sisteme donusturur.

## Uygulamali Kod Ornegi (LangChain)

Kodda yonlendirme uygulamak, olasi yollari ve hangi yolun secilecegine karar veren mantigi tanimlamayi icerir. LangChain ve LangGraph gibi cerceveler, bunun icin belirli bilesenler ve yapilar saglar. LangGraph'in durum tabanli grafik yapisi, yonlendirme mantigini goruntulemek ve uygulamak icin ozellikle sezgiseldir.

Bu kod, LangChain ve Google'in Generative AI'sini kullanan basit bir agent benzeri sistemi gostermektedir. Istegin niyetine (rezervasyon, bilgi veya belirsiz) gore kullanici isteklerini farkli simule edilmis "alt agent" isleyicilerine yonlendiren bir "koordinator" kurar. Sistem, istegi siniflandirmak icin bir dil modeli kullanir ve ardindan uygun isleyici fonksiyona devreder; bu, multi-agent mimarilerde sikca gorulen temel bir yetkilendirme kalibini simule eder.

Oncelikle, gerekli kutuphanelerin kurulu oldugundan emin olun:

```bash
pip install langchain langgraph google-cloud-aiplatform langchain-google-genai google-adk deprecated pydantic
```

Ayrica, sectiginiz dil modeli icin API anahtarinizla ortaminizi yapilandirmaniz gerekecektir (ornegin OpenAI, Google Gemini, Anthropic).

```python
# Copyright (c) 2025 Marco Fago
# https://www.linkedin.com/in/marco-fago/
#
# This code is licensed under the MIT License.
# See the LICENSE file in the repository for the full license text.

from langchain_google_genai import ChatGoogleGenerativeAI
from langchain_core.prompts import ChatPromptTemplate
from langchain_core.output_parsers import StrOutputParser
from langchain_core.runnables import RunnablePassthrough, RunnableBranch


# --- Configuration ---
# Ensure your API key environment variable is set (e.g., GOOGLE_API_KEY)
try:
    llm = ChatGoogleGenerativeAI(model="gemini-2.5-flash", temperature=0)
    print(f"Language model initialized: {llm.model}")
except Exception as e:
    print(f"Error initializing language model: {e}")
    llm = None


# --- Define Simulated Sub-Agent Handlers (equivalent to ADK sub_agents) ---
def booking_handler(request: str) -> str:
    """Simulates the Booking Agent handling a request."""
    print("\n--- DELEGATING TO BOOKING HANDLER ---")
    return f"Booking Handler processed request: '{request}'. Result: Simulated booking action."


def info_handler(request: str) -> str:
    """Simulates the Info Agent handling a request."""
    print("\n--- DELEGATING TO INFO HANDLER ---")
    return f"Info Handler processed request: '{request}'. Result: Simulated information retrieval."


def unclear_handler(request: str) -> str:
    """Handles requests that couldn't be delegated."""
    print("\n--- HANDLING UNCLEAR REQUEST ---")
    return f"Coordinator could not delegate request: '{request}'. Please clarify."


# --- Define Coordinator Router Chain (equivalent to ADK coordinator's instruction) ---
# This chain decides which handler to delegate to.
coordinator_router_prompt = ChatPromptTemplate.from_messages([
    (
        "system",
        """Analyze the user's request and determine which specialist handler should process it.
        - If the request is related to booking flights or hotels,
           output 'booker'.
        - For all other general information questions, output 'info'.
        - If the request is unclear or doesn't fit either category,
           output 'unclear'.
        ONLY output one word: 'booker', 'info', or 'unclear'."""
    ),
    ("user", "{request}")
])

if llm:
    coordinator_router_chain = coordinator_router_prompt | llm | StrOutputParser()


# --- Define the Delegation Logic (equivalent to ADK's Auto-Flow based on sub_agents) ---
# Use RunnableBranch to route based on the router chain's output.

# Define the branches for the RunnableBranch
branches = {
    "booker": RunnablePassthrough.assign(
        output=lambda x: booking_handler(x['request']['request'])
    ),
    "info": RunnablePassthrough.assign(
        output=lambda x: info_handler(x['request']['request'])
    ),
    "unclear": RunnablePassthrough.assign(
        output=lambda x: unclear_handler(x['request']['request'])
    ),
}

# Create the RunnableBranch. It takes the output of the router chain
# and routes the original input ('request') to the corresponding handler.
delegation_branch = RunnableBranch(
    (lambda x: x['decision'].strip() == 'booker', branches["booker"]),  # Added .strip()
    (lambda x: x['decision'].strip() == 'info', branches["info"]),      # Added .strip()
    branches["unclear"]  # Default branch for 'unclear' or any other output
)

# Combine the router chain and the delegation branch into a single runnable
# The router chain's output ('decision') is passed along with the original input ('request')
# to the delegation_branch.
coordinator_agent = {
    "decision": coordinator_router_chain,
    "request": RunnablePassthrough()
} | delegation_branch | (lambda x: x['output'])  # Extract the final output


# --- Example Usage ---
def main():
    if not llm:
        print("\nSkipping execution due to LLM initialization failure.")
        return

    print("--- Running with a booking request ---")
    request_a = "Book me a flight to London."
    result_a = coordinator_agent.invoke({"request": request_a})
    print(f"Final Result A: {result_a}")

    print("\n--- Running with an info request ---")
    request_b = "What is the capital of Italy?"
    result_b = coordinator_agent.invoke({"request": request_b})
    print(f"Final Result B: {result_b}")

    print("\n--- Running with an unclear request ---")
    request_c = "Tell me about quantum physics."
    result_c = coordinator_agent.invoke({"request": request_c})
    print(f"Final Result C: {result_c}")


if __name__ == "__main__":
    main()
```

Belirtildigi gibi, bu Python kodu LangChain kutuphanesini ve Google'in Generative AI modelini, ozellikle gemini-2.5-flash'i kullanarak basit bir agent benzeri sistem olusturur. Ayrintili olarak, uc simule edilmis alt agent isleyicisi tanimlar: `booking_handler`, `info_handler` ve `unclear_handler`; her biri belirli istek turlerini islemek icin tasarlanmistir.

Temel bir bilesen, gelen kullanici isteklerini uc kategoriden birine siniflandirmasi icin dil modeline talimat vermek icin bir ChatPromptTemplate kullanan `coordinator_router_chain`'dir: `booker`, `info` veya `unclear`. Bu yonlendirici zincirin ciktisi daha sonra orijinal istegi ilgili isleyici fonksiyona devretmek icin bir RunnableBranch tarafindan kullanilir. RunnableBranch, dil modelinden gelen karari kontrol eder ve istek verilerini `booking_handler`, `info_handler` veya `unclear_handler`'a yonlendirir. `coordinator_agent` bu bilesenleri birlestirir; oncelikle istegi bir karar icin yonlendirir ve ardindan istegi secilen isleyiciye aktarir. Nihai cikti, isleyicinin yanitindan cikarilir.

Ana fonksiyon, uc ornek istekle sistemin kullanimini gostererek, farkli girdilerin simule edilmis agent'lar tarafindan nasil yonlendirildigini ve islendigini sergiler. Saglamlik icin dil modeli baslatma icin hata yonetimi dahil edilmistir. Kod yapisi, merkezi bir koordinatorun gorevleri niyete dayali olarak ozelesmis agent'lara devrettigi temel bir multi-agent cercevesini taklit eder.

## Uygulamali Kod Ornegi (Google ADK)

Agent Development Kit (ADK), agentic sistemler muhendisligi icin bir cercevedir ve bir agent'in yeteneklerini ve davranislarini tanimlamak icin yapilandirilmis bir ortam saglar. Acik hesaplama grafikleri uzerine kurulu mimarilerin aksine, ADK paradigmasinda yonlendirme genellikle agent'in fonksiyonlarini temsil eden ayrik bir "araclar" kumesi tanimlayarak uygulanir. Bir kullanici sorgusuna yanit olarak uygun aracin secimi, kullanici niyetini dogru fonksiyon isleyicisiyle eslestirmek icin temel bir modeli kullanan cercevnin dahili mantigi tarafindan yonetilir.

Bu Python kodu, Google'in ADK kutuphanesini kullanan bir Agent Development Kit (ADK) uygulamasinin bir ornegini gostermektedir. Tanimlanmis talimatlara dayanarak kullanici isteklerini ozelesmis alt agent'lara (rezervasyonlar icin "Booker" ve genel bilgi icin "Info") yonlendiren bir "Coordinator" agent'i kurar. Alt agent'lar daha sonra isteklerin islendigini simule etmek icin belirli araclar kullanarak, bir agent sistemi icerisindeki temel bir yetkilendirme kalibini sergiler.

```python
# Copyright (c) 2025 Marco Fago
#
# This code is licensed under the MIT License.
# See the LICENSE file in the repository for the full license text.

import uuid
from typing import Dict, Any, Optional

from google.adk.agents import Agent
from google.adk.runners import InMemoryRunner
from google.adk.tools import FunctionTool
from google.genai import types
from google.adk.events import Event


# --- Define Tool Functions ---
# These functions simulate the actions of the specialist agents.
def booking_handler(request: str) -> str:
    """
    Handles booking requests for flights and hotels.

    Args:
        request: The user's request for a booking.

    Returns:
        A confirmation message that the booking was handled.
    """
    print("-------------------------- Booking Handler Called ----------------------------")
    return f"Booking action for '{request}' has been simulated."


def info_handler(request: str) -> str:
    """
    Handles general information requests.

    Args:
        request: The user's question.

    Returns:
        A message indicating the information request was handled.
    """
    print("-------------------------- Info Handler Called ----------------------------")
    return f"Information request for '{request}'. Result: Simulated information retrieval."


def unclear_handler(request: str) -> str:
    """Handles requests that couldn't be delegated."""
    return f"Coordinator could not delegate request: '{request}'. Please clarify."


# --- Create Tools from Functions ---
booking_tool = FunctionTool(booking_handler)
info_tool = FunctionTool(info_handler)

# Define specialized sub-agents equipped with their respective tools
booking_agent = Agent(
    name="Booker",
    model="gemini-2.0-flash",
    description="A specialized agent that handles all flight "
                "and hotel booking requests by calling the booking tool.",
    tools=[booking_tool],
)

info_agent = Agent(
    name="Info",
    model="gemini-2.0-flash",
    description="A specialized agent that provides general information "
                "and answers user questions by calling the info tool.",
    tools=[info_tool],
)

# Define the parent agent with explicit delegation instructions
coordinator = Agent(
    name="Coordinator",
    model="gemini-2.0-flash",
    instruction=(
        "You are the main coordinator. Your only task is to analyze "
        "incoming user requests "
        "and delegate them to the appropriate specialist agent. Do not try to answer the user directly.\n"
        "- For any requests related to booking flights or hotels, delegate to the 'Booker' agent.\n"
        "- For all other general information questions, delegate to the 'Info' agent."
    ),
    description="A coordinator that routes user requests to the correct specialist agent.",
    # The presence of sub_agents enables LLM-driven delegation (Auto-Flow) by default.
    sub_agents=[booking_agent, info_agent],
)


# --- Execution Logic ---
async def run_coordinator(runner: InMemoryRunner, request: str):
    """Runs the coordinator agent with a given request and delegates."""
    print(f"\n--- Running Coordinator with request: '{request}' ---")
    final_result = ""
    try:
        user_id = "user_123"
        session_id = str(uuid.uuid4())

        await runner.session_service.create_session(
            app_name=runner.app_name,
            user_id=user_id,
            session_id=session_id,
        )

        for event in runner.run(
            user_id=user_id,
            session_id=session_id,
            new_message=types.Content(
                role='user',
                parts=[types.Part(text=request)],
            ),
        ):
            if event.is_final_response() and event.content:
                # Try to get text directly from event.content to avoid iterating parts
                if hasattr(event.content, 'text') and event.content.text:
                    final_result = event.content.text
                elif event.content.parts:
                    # Fallback: Iterate through parts and extract text (might trigger warning)
                    text_parts = [part.text for part in event.content.parts if getattr(part, "text", None)]
                    final_result = "".join(text_parts)
                # Assuming the loop should break after the final response
                break

        print(f"Coordinator Final Response: {final_result}")
        return final_result

    except Exception as e:
        print(f"An error occurred while processing your request: {e}")
        return f"An error occurred while processing your request: {e}"


async def main():
    """Main function to run the ADK example."""
    print("--- Google ADK Routing Example (ADK Auto-Flow Style) ---")
    print("Note: This requires Google ADK installed and authenticated.")

    runner = InMemoryRunner(coordinator)

    # Example Usage
    result_a = await run_coordinator(runner, "Book me a hotel in Paris.")
    print(f"Final Output A: {result_a}")

    result_b = await run_coordinator(runner, "What is the highest mountain in the world?")
    print(f"Final Output B: {result_b}")

    result_c = await run_coordinator(runner, "Tell me a random fact.")  # Should go to Info
    print(f"Final Output C: {result_c}")

    result_d = await run_coordinator(runner, "Find flights to Tokyo next month.")  # Should go to Booker
    print(f"Final Output D: {result_d}")


if __name__ == "__main__":
    import nest_asyncio

    nest_asyncio.apply()
    await main()
```

Bu betik, ana bir Coordinator agent'i ve iki ozelesmis `sub_agents`'tan olusur: Booker ve Info. Her ozelesmis agent, bir eylemi simule eden bir Python fonksiyonunu saran bir FunctionTool ile donatilmistir. `booking_handler` fonksiyonu ucus ve otel rezervasyonlarini islemeyi simule ederken, `info_handler` fonksiyonu genel bilgi eriisimini simule eder. `unclear_handler`, koordinatorun devredemedigi istekler icin bir geri donus mekanizmasi olarak dahil edilmistir; ancak mevcut koordinator mantigi, ana `run_coordinator` fonksiyonunda yetkilendirme basarisizligi icin bunu acikca kullanmamaktadir.

Coordinator agent'inin temel rolu, talimatinda tanimlandigi gibi, gelen kullanici mesajlarini analiz etmek ve bunlari Booker veya Info agent'ina devretmektir. Bu yetkilendirme, Coordinator'un tanimli `sub_agents`'i oldugu icin ADK'nin Auto-Flow mekanizmasi tarafindan otomatik olarak yonetilir. `run_coordinator` fonksiyonu bir InMemoryRunner kurar, bir kullanici ve oturum kimligi olusturur ve ardindan kullanicinin istegini koordinator agent'i uzerinden islemek icin runner'i kullanir. runner.run yontemi istegi isler ve olay uretir; kod nihai yanit metnini event.content'ten cikarir.

Ana fonksiyon, farkli isteklerle koordinatoru calistirarak sistemin kullanimini gosterir ve rezervasyon isteklerini Booker'a, bilgi isteklerini ise Info agent'ina nasil devrettigini sergiler.

## Bir Bakista

**Ne:** Agentic sistemler genellikle tek bir dogrusal surecle ele alinamayan cok cesitli girdi ve durumlara yanit vermek zorundadir. Basit bir sirali is akisi, baglama dayali kararlar verme yeteneginden yoksundur. Belirli bir gorev icin dogru araci veya alt sureci secmek icin bir mekanizma olmadan, sistem katı ve uyarlanamaz kalir. Bu sinirlilik, gercek dunyadaki kullanici isteklerinin karmasikligini ve degiskenligini yonetebilen gelismis uygulamalar olusturmayi zorlastirir.

**Neden:** Yonlendirme kalibi, bir agent'in operasyonel cercevesine kosullu mantik kazandirarak standart bir cozum sunar. Sistemin oncelikle gelen bir sorguyu analiz ederek niyetini veya niteligini belirlemesini saglar. Bu analize dayanarak, agent kontrol akisini en uygun ozelesmis araca, fonksiyona veya alt agent'a dinamik olarak yonlendirir. Bu karar, LLM'leri prompt'lama, onceden tanimlanmis kurallar uygulama veya embedding tabanli semantik benzerlik kullanma dahil cesitli yontemlerle yonlendirilebilir. Sonuc olarak, yonlendirme statik, onceden belirlenmmis bir yurutme yolunu en iyi olasi eylemi secebilen esnek ve baglama duyarli bir is akisina donusturur.

**Temel Kural:** Yonlendirme kalibini, bir agent'in kullanicinin girdisine veya mevcut duruma dayanarak birden fazla farkli is akisi, arac veya alt agent arasinda karar vermesi gerektiginde kullanin. Farkli gorev turlerini ele almak icin gelen istekleri triajlamasi veya siniflandirmasi gereken uygulamalar icin, ornegin satis sorgulamalarini, teknik destegi ve hesap yonetimi sorularini ayirt eden bir musteri destek botu gibi, gereklidir.

**Gorsel Ozet:**

![Router Pattern, using LLM as a Router](../assets/Router_Pattern_Using_LLM_as_a_Router.png)

Sekil 1: Yonlendirici kalibi, LLM'yi Yonlendirici olarak kullanma

## Temel Cikarimlar

* Yonlendirme, agent'larin koullara dayali olarak bir is akisindaki sonraki adim hakkinda dinamik kararlar vermesini saglar.
* Agent'larin cesitli girdileri ele almasina ve davranislarini uyarlamasina olanak taniyarak dogrusal yurutmenin otesine gecmeyi mumkun kilar.
* Yonlendirme mantigi, LLM'ler, kural tabanli sistemler veya embedding benzerligi kullanilarak uygulanabilir.
* LangGraph ve Google ADK gibi cerceveler, agent is akislari icerisinde yonlendirmeyi tanimlamak ve yonetmek icin yapilandirilmis yollar sunar, ancak farkli mimari yaklasimlariyla.

## Sonuc

Yonlendirme kalibi, gercek anlamda dinamik ve duyarli agentic sistemler olusturmada kritik bir adimdir. Yonlendirmeyi uygulayarak, basit, dogrusal yurutme akislarinin otesine gecer ve agent'larimizi bilgileri nasil isleyecekleri, kullanici girdisine nasil yanit verecekleri ve mevcut araclari veya alt agent'lari nasil kullanacaklari konusunda akilli kararlar almaya yetkilendiririz.

Yonlendirmenin musteri hizmetleri sohbet robotlarindan karmasik veri isleme pipeline'larina kadar cesitli alanlarda nasil uygulanabilecegini gorduk. Girdiyi analiz etme ve is akisini kosullu olarak yonlendirme yetisi, gercek dunya gorevlerinin dogasinda bulunan degiskenligi ele alabilen agent'lar olusturmak icin temeldir.

LangChain ve Google ADK kullanan kod ornekleri, yonlendirmeyi uygulamanin iki farkli ama etkili yaklasiimini gostermektedir. LangGraph'in grafik tabanli yapisi, durumlari ve gecisleri tanimlamanin gorsel ve acik bir yolunu sunarak karmasik, cok adimli, karmasik yonlendirme mantigina sahip is akislari icin idealdir. Ote yandan Google ADK, genellikle ayrik yetenekler (Araclar) tanimlama ve kullanici isteklerini uygun arac isleyicisine yonlendirmek icin cercevnin yetenegine dayanma uzerine odaklanir; bu, iyi tanimlanmis bir dizi ayrik eyleme sahip agent'lar icin daha basit olabilir.

Yonlendirme kalibini ustalasmak, farkli senaryolarda akillica gezinebilen ve baglama dayali uyarlanmis yanitlar veya eylemler saglayabilen agent'lar olusturmak icin gereklidir. Cok yonlu ve saglam agentic uygulamalar olusturmanin temel bir bilisenidir.

## Kaynaklar

1. LangGraph Documentation: [https://www.langchain.com/](https://www.langchain.com/)
2. Google Agent Developer Kit Documentation: [https://google.github.io/adk-docs/](https://google.github.io/adk-docs/)
