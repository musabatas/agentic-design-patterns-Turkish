# Bolum 5: Arac Kullanimi (Function Calling)

## Arac Kullanimi Kalibina Genel Bakis

Simdiye kadar, oncelikle dil modelleri arasindaki etkilesimleri orkestre etmeyi ve agent'in dahili is akisi icerisindeki bilgi akisini yonetmeyi iceren agentic kaliplari tartistik (Zincirleme, Yonlendirme, Paralelizasyon, Yansitma). Ancak, agent'larin gercekten faydali olabilmesi ve gercek dunya veya harici sistemlerle etkilesime girebilmesi icin Arac kullanma yetenegine ihtiyaclari vardir.

Arac Kullanimi kalibi, genellikle function calling olarak adlandirilan bir mekanizma araciligiyla uygulanir ve bir agent'in harici API'ler, veritabanlari, hizmetler veya hatta kod yurutme ile etkilesime girmesini saglar. Agent'in cekirdegindeki LLM'nin, kullanicinin istegine veya gorevin mevcut durumuna dayanarak belirli bir harici fonksiyonu ne zaman ve nasil kullanacagina karar vermesine olanak tanir.

Surec tipik olarak su adimlari icerir:

1. **Arac Tanimi:** Harici fonksiyonlar veya yetenekler LLM'ye tanimlanir ve aciklanir. Bu aciklama, fonksiyonun amacini, adini ve kabul ettigi parametreleri, turleri ve aciklamalariyla birlikte icerir.
2. **LLM Karari:** LLM, kullanicinin istegini ve mevcut arac tanimlarini alir. Istegi ve araclari anlamasina dayanarak, LLM istegi yerine getirmek icin bir veya daha fazla aracin cagrilmasinin gerekli olup olmadigina karar verir.
3. **Fonksiyon Cagrisi Olusturma:** LLM bir arac kullanmaya karar verirse, cagrilacak aracin adini ve kullanicinin isteginden cikarilan argumanlari (parametreleri) belirten yapilandirilmis bir cikti (genellikle bir JSON nesnesi) olusturur.
4. **Arac Yurutme:** Agentic cerceve veya orkestrasyon katmani bu yapilandirilmis ciktiyi yakalar. Istenen araci tanir ve saglanan argumanlarlaa gercek harici fonksiyonu yurutur.
5. **Gozlem/Sonuc:** Arac yurutumunden elde edilen cikti veya sonuc agent'a geri dondurulur.
6. **LLM Isleme (Istege bagli ancak yaygin):** LLM, aracin ciktisini baglam olarak alir ve bunu kullaniciya nihai bir yanit formule etmek veya is akisindaki sonraki adima karar vermek icin kullanir (bu, baska bir araci cagirmayi, yansitmayi veya nihai bir yanit saglamayi icerebilir).

Bu kalip temeldir cunku LLM'nin egitim verilrinin sinirliligini kirar ve guncel bilgilere erismesine, dahili olarak yapamayacagi hesaplamalari gerceklestirmesine, kullaniciya ozgu verilerle etkilesime girmesine veya gercek dunyada eylemleri tetiklemesine olanak tanir. Function calling, LLM'nin akil yurutme yetenekleri ile mevcut genis harici islevsellik yelpazesi arasindaki bosluyu kapatan teknik mekanizmadir.

"Function calling" belirli, onceden tanimlanmis kod fonksiyonlarini cagirmayi uygun bir sekilde tanimlarken, daha genis "tool calling" kavramini dusunmek faydalidir. Bu daha genis terim, bir agent'in yeteneklerinin basit fonksiyon yurutmenin cok otesine uzanabilecegini kabul eder. Bir "arac" geleneksel bir fonksiyon olabilir, ancak ayni zamanda karmasik bir API ucu noktasi, bir veritabani istegi veya hatta baska bir ozelesmis agent'a yonlendirilmis bir talimat da olabilir. Bu bakis acisi, ornegin birincil bir agent'in karmasik bir veri analizi gorevini ozel bir "analist agent'ina" devredebilecegi veya harici bir bilgi tabanini API'si araciligiyla sorgulayabilecegi daha gelismis sistemler tasavvur etmemize olanak tanir. "Tool calling" acisindan dusunmek, agent'larin cesitli bir dijital kaynaklar ve diger akilli varliklar ekosistemi genelinde orkestrator olarak hareket etme potansiyelini daha iyi yakalar.

LangChain, LangGraph ve Google Agent Developer Kit (ADK) gibi cerceveler, araclari tanimlamak ve agent is akislarina entegre etmek icin saglam destek saglar; genellikle Gemini veya OpenAI serisi gibi modern LLM'lerin yerel function calling yeteneklerinden yararlanir. Bu cercevelerin "tuvalinde", araclari tanimlar ve ardindan agent'lari (tipik olarak LLM Agent'lar) bu araclarin farkinda olacak ve kullanabilecek sekilde yapilandirirsiniz.

Arac Kullanimi, guclu, etkilesimli ve harici olarak bilinli agent'lar olusturmak icin temel tas niteliginde bir kaliptir.

## Pratik Uygulamalar ve Kullanim Alanlari

Arac Kullanimi kalibi, bir agent'in metin olusturmanin otesine gecerek bir eylem gerceklestirmesi veya belirli, dinamik bilgileri almmasi gereken hemen her senaryoda uygulanabilir:

### 1. Harici Kaynaklardan Bilgi Erisimi

LLM'nin egitim verilerinde bulunmayan gercek zamanli verilere veya bilgilere erisim.

* **Kullanim Alani:** Hava durumu agent'i.
  * **Arac:** Bir konum alan ve mevcut hava kosullarini donduren bir hava durumu API'si.
  * **Agent Akisi:** Kullanici "Londra'da hava nasil?" diye sorar, LLM hava durumu aracina ihtiyac duyuldugunu belirler, araci "Londra" ile cagiriir, arac veri dondurur, LLM veriyi kullanici dostu bir yanita bicimlendirir.

### 2. Veritabanlari ve API'lerle Etkilesim

Yapilandirilmis veriler uzerinde sorgulama, guncelleme veya diger islemleri gerceklestirme.

* **Kullanim Alani:** E-ticaret agent'i.
  * **Araclar:** Urun envantterini kontrol etmek, siparis durumunu almak veya odemeleri islemek icin API cagirilari.
  * **Agent Akisi:** Kullanici "X urunu stokta var mi?" diye sorar, LLM envanter API'sini cagirir, arac stok sayisini dondurur, LLM kullaniciya stok durumunu bildirir.

### 3. Hesaplama ve Veri Analizi Yapma

Harici hesap makineleri, veri analiz kutuphaneleri veya istatistik araclari kullanma.

* **Kullanim Alani:** Finans agent'i.
  * **Araclar:** Hesap makinesi fonksiyonu, borsa veri API'si, elektronik tablo araci.
  * **Agent Akisi:** Kullanici "AAPL'in mevcut fiyati nedir ve 150$'dan 100 hisse alsam potansiyel karimi hesapla?" der, LLM borsa API'sini cagirir, mevcut fiyati alir, ardindan hesap makinesi aracini cagirir, sonucu alir, yaniti bicimlendirir.

### 4. Iletisim Gonderme

E-postalar, mesajlar gonderme veya harici iletisim hizmetlerine API cagirilari yapma.

* **Kullanim Alani:** Kisisel asistan agent'i.
  * **Arac:** E-posta gonderme API'si.
  * **Agent Akisi:** Kullanici "John'a yarin ki toplanti hakkinda bir e-posta gonder" der, LLM istekten cikarilan alici, konu ve govdeyle e-posta aracini cagirirr.

### 5. Kod Yurutme

Belirli gorevleri gerceklestirmek icin guvenli bir ortamda kod parcalari calistirma.

* **Kullanim Alani:** Kodlama asistani agent'i.
  * **Arac:** Kod yorumlayicisi.
  * **Agent Akisi:** Kullanici bir Python parcasi saglar ve "Bu kod ne yapar?" diye sorar, LLM kodu calistirmak ve ciktisini analiz etmek icin yorumlayici aracini kullanir.

### 6. Diger Sistemleri veya Cihazlari Kontrol Etme

Akilli ev cihazlari, IoT platformlari veya diger bagli sistemlerle etkilesim.

* **Kullanim Alani:** Akilli ev agent'i.
  * **Arac:** Akilli isiklari kontrol etmek icin bir API.
  * **Agent Akisi:** Kullanici "Oturma odasinin isikkarini kapat" der. LLM, komut ve hedef cihaz ile akilli ev aracini cagirir.

Arac Kullanimi, bir dil modelini metin ureteciden dijital veya fiziksel dunyada algilayabilen, akil yurutebilen ve harekete gecebilen bir agent'a donusturen seydir (bkz. Sekil 1).

![Some Examples of an Agent Using Tool](Some_Examples_of_an_Agent_Using_Tool.png)

Sekil 1: Bir Agent'in Arac Kullanmasinin Bazi Ornekleri

## Uygulamali Kod Ornegi (LangChain)

LangChain cercevesi icerisinde arac kullaniminin uygulanmasi iki asamali bir surecdir. Ilk olarak, bir veya daha fazla arac tanimlanir, tipik olarak mevcut Python fonksiyonlari veya diger calistirilabilir bilesenler kapsullenerek. Ardindan, bu araclar bir dil modeline baglanir ve boylece modele, bir kullanicinin sorgusunu yerine getirmek icin harici bir fonksiyon cagrisiniin gerekli oldugunu belirlediginde yapilandirilmis bir arac kullanim istegi olusturma yetenegi verilir.

Asagidaki uygulama, oncelikle bir bilgi erisim aracini simule etmek icin basit bir fonksiyon tanimlayarak bu ilkeyi gosterecektir. Ardindan, kullanici girdisine yanit olarak bu aractan yararlanmak icin bir agent olusturulacak ve yapilandirilacaktir. Bu ornegin yurutulmesi, temel LangChain kutuphanelerinin ve modele ozgu bir saglayici paketinin kurulmasini gerektirir. Ayrica, secilen dil modeli hizmetiyle uygun kimlik dogrulama, tipik olarak yerel ortamda yapilandirilan bir API anahtari araciligiyla, gerekli bir on kosuldur.

```python
import os
import getpass
import asyncio
import nest_asyncio
from typing import List
from dotenv import load_dotenv
import logging

from langchain_google_genai import ChatGoogleGenerativeAI
from langchain_core.prompts import ChatPromptTemplate
from langchain_core.tools import tool as langchain_tool
from langchain.agents import create_tool_calling_agent, AgentExecutor


# UNCOMMENT
# Prompt the user securely and set API keys as environment variables
os.environ["GOOGLE_API_KEY"] = getpass.getpass("Enter your Google API key: ")
os.environ["OPENAI_API_KEY"] = getpass.getpass("Enter your OpenAI API key: ")

try:
    # A model with function/tool calling capabilities is required.
    llm = ChatGoogleGenerativeAI(model="gemini-2.0-flash", temperature=0)
    print(f"✅ Language model initialized: {llm.model}")
except Exception as e:
    print(f"🛑 Error initializing language model: {e}")
    llm = None


# --- Define a Tool ---
@langchain_tool
def search_information(query: str) -> str:
    """
    Provides factual information on a given topic. Use this tool to find answers to phrases
    like 'capital of France' or 'weather in London?'.
    """
    print(f"\n--- 🛠️ Tool Called: search_information with query: '{query}' ---")

    # Simulate a search tool with a dictionary of predefined results.
    simulated_results = {
        "weather in london": "The weather in London is currently cloudy with a temperature of 15°C.",
        "capital of france": "The capital of France is Paris.",
        "population of earth": "The estimated population of Earth is around 8 billion people.",
        "tallest mountain": "Mount Everest is the tallest mountain above sea level.",
        "default": f"Simulated search result for '{query}': No specific information found, but the topic seems interesting.",
    }
    result = simulated_results.get(query.lower(), simulated_results["default"])
    print(f"--- TOOL RESULT: {result} ---")
    return result


tools = [search_information]


# --- Create a Tool-Calling Agent ---
if llm:
    # This prompt template requires an `agent_scratchpad` placeholder for the agent's internal steps.
    agent_prompt = ChatPromptTemplate.from_messages([
        ("system", "You are a helpful assistant."),
        ("human", "{input}"),
        ("placeholder", "{agent_scratchpad}"),
    ])

    # Create the agent, binding the LLM, tools, and prompt together.
    agent = create_tool_calling_agent(llm, tools, agent_prompt)

    # AgentExecutor is the runtime that invokes the agent and executes the chosen tools.
    # The 'tools' argument is not needed here as they are already bound to the agent.
    agent_executor = AgentExecutor(agent=agent, verbose=True, tools=tools)


async def run_agent_with_tool(query: str):
    """Invokes the agent executor with a query and prints the final response."""
    print(f"\n--- 🏃 Running Agent with Query: '{query}' ---")
    try:
        response = await agent_executor.ainvoke({"input": query})
        print("\n--- ✅ Final Agent Response ---")
        print(response["output"])
    except Exception as e:
        print(f"\n🛑 An error occurred during agent execution: {e}")


async def main():
    """Runs all agent queries concurrently."""
    tasks = [
        run_agent_with_tool("What is the capital of France?"),
        run_agent_with_tool("What's the weather like in London?"),
        run_agent_with_tool("Tell me something about dogs."),  # Should trigger the default tool response
    ]
    await asyncio.gather(*tasks)


nest_asyncio.apply()
asyncio.run(main())

```

Kod, LangChain kutuphanesini ve Google Gemini modelini kullanan arac cagiran bir agent kurar. Belirli sorgulara olgusal yanitlar saglmayi simule eden bir `search_information` araci tanimlar. Aracin "weather in london", "capital of france" ve "population of earth" icin onceden tanimlanmis yanitlari ve diger sorgular icin varsayilan bir yaniti vardir. Arac cagirma yeteneklerine sahip bir ChatGoogleGenerativeAI modeli baslatilir. Agent'in etkilesimini yonlendirmek icin bir ChatPromptTemplate olusturulur. `create_tool_calling_agent` fonksiyonu, dil modelini, araclari ve prompt'u bir agent'ta birlestirir. Daha sonra agent'in yurutumunu ve arac cagirmayi yonetmek icin bir AgentExecutor kurulur. Verilen bir sorguyla agent'i cagirmak ve sonucu yazdirmak icin `run_agent_with_tool` asenkron fonksiyonu tanimlanir. Ana asenkron fonksiyon, es zamanli olarak calistirilmak uzere birden fazla sorgu hazirlar. Bu sorgular, `search_information` aracinin hem belirli hem de varsayilan yanitlarini test etmek icin tasarlanmistir. Son olarak, asyncio.run(main()) cagrisi tum agent gorevlerini yurutur. Kod, agent kurulumu ve yurutme ile devam etmeden once basarili LLM baslatma kontrolleri icerir.

# Uygulamali Kod Ornegi (CrewAI)

Bu kod, CrewAI cercevesi icerisinde function calling (Araclar) uygulamasinin pratik bir ornegini saglar. Bir agent'in bilgi aramak icin bir aracla donatildigi basit bir senaryo kurar. Ornek, ozellikle bu agent ve arac kullanilarak simule edilmis bir hisse senedi fiyatinin getirilmesini gostermektedir.

```python
# pip install crewai langchain-openai

import os
from crewai import Agent, Task, Crew
from crewai.tools import tool
import logging


# --- Best Practice: Configure Logging ---
# A basic logging setup helps in debugging and tracking the crew's execution.
logging.basicConfig(level=logging.INFO, format='%(asctime)s - %(levelname)s - %(message)s')


# --- Set up your API Key ---
# For production, it's recommended to use a more secure method for key management
# like environment variables loaded at runtime or a secret manager.
#
# Set the environment variable for your chosen LLM provider (e.g., OPENAI_API_KEY)
# os.environ["OPENAI_API_KEY"] = "YOUR_API_KEY"
# os.environ["OPENAI_MODEL_NAME"] = "gpt-4o"


# --- 1. Refactored Tool: Returns Clean Data ---
# The tool now returns raw data (a float) or raises a standard Python error.
# This makes it more reusable and forces the agent to handle outcomes properly.
@tool("Stock Price Lookup Tool")
def get_stock_price(ticker: str) -> float:
    """
    Fetches the latest simulated stock price for a given stock ticker symbol.
    Returns the price as a float. Raises a ValueError if the ticker is not found.
    """
    logging.info(f"Tool Call: get_stock_price for ticker '{ticker}'")
    simulated_prices = {
        "AAPL": 178.15,
        "GOOGL": 1750.30,
        "MSFT": 425.50,
    }
    price = simulated_prices.get(ticker.upper())
    if price is not None:
        return price
    else:
        # Raising a specific error is better than returning a string.
        # The agent is equipped to handle exceptions and can decide on the next action.
        raise ValueError(f"Simulated price for ticker '{ticker.upper()}' not found.")


# --- 2. Define the Agent ---
# The agent definition remains the same, but it will now leverage the improved tool.
financial_analyst_agent = Agent(
    role='Senior Financial Analyst',
    goal='Analyze stock data using provided tools and report key prices.',
    backstory="You are an experienced financial analyst adept at using data sources to find stock information. You provide clear, direct answers.",
    verbose=True,
    tools=[get_stock_price],
    # Allowing delegation can be useful, but is not necessary for this simple task.
    allow_delegation=False,
)


# --- 3. Refined Task: Clearer Instructions and Error Handling ---
# The task description is more specific and guides the agent on how to react
# to both successful data retrieval and potential errors.
analyze_aapl_task = Task(
    description=(
        "What is the current simulated stock price for Apple (ticker: AAPL)? "
        "Use the 'Stock Price Lookup Tool' to find it. "
        "If the ticker is not found, you must report that you were unable to retrieve the price."
    ),
    expected_output=(
        "A single, clear sentence stating the simulated stock price for AAPL. "
        "For example: 'The simulated stock price for AAPL is $178.15.' "
        "If the price cannot be found, state that clearly."
    ),
    agent=financial_analyst_agent,
)


# --- 4. Formulate the Crew ---
# The crew orchestrates how the agent and task work together.
financial_crew = Crew(
    agents=[financial_analyst_agent],
    tasks=[analyze_aapl_task],
    verbose=True  # Set to False for less detailed logs in production
)


# --- 5. Run the Crew within a Main Execution Block ---
# Using a __name__ == "__main__": block is a standard Python best practice.
def main():
    """Main function to run the crew."""
    # Check for API key before starting to avoid runtime errors.
    if not os.environ.get("OPENAI_API_KEY"):
        print("ERROR: The OPENAI_API_KEY environment variable is not set.")
        print("Please set it before running the script.")
        return

    print("\n## Starting the Financial Crew...")
    print("---------------------------------")

    # The kickoff method starts the execution.
    result = financial_crew.kickoff()

    print("\n---------------------------------")
    print("## Crew execution finished.")
    print("\nFinal Result:\n", result)


if __name__ == "__main__":
    main()
```

Bu kod, finansal analiz gorevini simule etmek icin Crew.ai kutuphanesini kullanan basit bir uygulamayi gostermektedir. Onceden tanimlanmis ticker'lar icin hisse senedi fiyatlari aramayni simule eden ozel bir arac olan `get_stock_price` tanimlar. Arac, gecerli ticker'lar icin kayan noktali sayi dondurmek veya gecersiz olanlar icin ValueError yukseltmek uzere tasarlanmistir. Senior Financial Analyst rolune sahip `financial_analyst_agent` adli bir Crew.ai Agent'i olusturulur. Bu agent'a etkilesim kurmasi icin `get_stock_price` araci verilir. Agent'a ozellikle araci kullanarak AAPL icin simule edilmis hisse senedi fiyatini bulmasi talimati verilen `analyze_aapl_task` adli bir Gorev tanimlanir. Gorev tanimi, araci kullanirken hem basari hem de basarisizlik durumlarinin nasil ele alinacagina dair net talimatlar icerir. `financial_analyst_agent` ve `analyze_aapl_task`'tan olusan bir Crew olusturulur. Hem agent hem de crew icin verbose ayari, yurutme sirasinda ayrintili gunlukleme saglamak icin etkinlestirilmistir. Betigin ana bolumu, standart `if __name__ == "__main__":` blogu icerisinde kickoff() yontemiyle crew'un gorevini calistirir. Crew'u baslatmadan once, agent'in islemesi icin gerekli olan `OPENAI_API_KEY` ortam degiskeninin ayarlanip ayarlanmadigini kontrol eder. Crew'un yurutumunun sonucu, yani gorevin ciktisi, daha sonra konsola yazdirilir. Kod ayrica crew'un eylemlerini ve arac cagrilarini daha iyi takip etmek icin temel gunlukleme yapilandirmasini icerir. API anahtar yonetimi icin ortam degiskenleri kullanir, ancak uretim ortamlari icin daha guvenli yontemlerin onerildigini belirtir. Kisacasi, temel mantik Crew.ai'de isbirlikci bir is akisi olusturmak icin araclarin, agent'larin ve gorevlerin nasil tanimlanacagini sergiler.

## Uygulamali Kod (Google ADK)

Google Agent Developer Kit (ADK), dogrudan bir agent'in yeteneklerine dahil edilebilecek yerel olarak entegre araclarin bir kutuphanesini icerir.

**Google search:** Bu tur bir bilesenin birincil ornegi Google Search aracidir. Bu arac, Google Search motoruna dogrudan bir arayuz gorevi gorerek, agent'i web aramalari yapma ve harici bilgi alma islevselligiyle donatir.

```python
from google.adk.agents import Agent as ADKAgent
from google.adk.runners import Runner
from google.adk.sessions import InMemorySessionService
from google.adk.tools import google_search
from google.genai import types
import nest_asyncio
import asyncio


# Define variables required for Session setup and Agent execution
APP_NAME = "Google Search Agent"
USER_ID = "user1234"
SESSION_ID = "1234"


# Define Agent with access to search tool
root_agent = ADKAgent(
    name="basic_search_agent",
    model="gemini-2.0-flash-exp",
    description="Agent to answer questions using Google Search.",
    instruction="I can answer your questions by searching the internet. Just ask me anything!",
    tools=[google_search],  # Google Search is a pre-built tool to perform Google searches.
)


# Agent Interaction
async def call_agent(query: str):
    """
    Helper function to call the agent with a query.
    """
    # Session and Runner
    session_service = InMemorySessionService()
    await session_service.create_session(
        app_name=APP_NAME,
        user_id=USER_ID,
        session_id=SESSION_ID,
    )

    runner = Runner(agent=root_agent, app_name=APP_NAME, session_service=session_service)

    content = types.Content(role='user', parts=[types.Part(text=query)])
    events = runner.run(user_id=USER_ID, session_id=SESSION_ID, new_message=content)

    for event in events:
        if event.is_final_response() and event.content:
            # Safely extract text from the final response
            if hasattr(event.content, "text") and event.content.text:
                final_response = event.content.text
            elif event.content.parts:
                final_response = "".join(
                    part.text for part in event.content.parts if getattr(part, "text", None)
                )
            else:
                final_response = ""
            print("Agent Response:", final_response)


nest_asyncio.apply()
asyncio.run(call_agent("what's the latest ai news?"))
```

Bu kod, Python icin Google ADK kullanilarak desteklenen temel bir agent'in nasil olusturulacagini ve kullanilacagini gostermektedir. Agent, bir arac olarak Google Search'u kullanarak sorulari yanitlamak icin tasarlanmistir. Oncelikle, IPython, google.adk ve google.genai'den gerekli kutuphaneler iceri aktarilir. Uygulama adi, kullanici kimligi ve oturum kimligi icin sabitler tanimlanir. Amacini ve talimatlarini belirten bir aciklama ile `basic_search_agent` adli bir Agent ornegi olusturulur. ADK tarafindan saglanan onceden olusturulmus bir arac olan Google Search aracini kullanmak uzere yapilandirilmistir. Agent icin oturumlari yonetmek uzere bir InMemorySessionService (bkz. Bolum 8) baslatilir. Belirtilen uygulama, kullanici ve oturum kimlikleri icin yeni bir oturum olusturulur. Olusturulan agent'i oturum hizmetiyle baglayan bir Runner ornegi olusturulur. Bu runner, bir oturum icerisinde agent'in etkilesimlerini yurutmekten sorumludur. Agent'a sorgu gonderme ve yaniti isleme surecini basitlestirmek icin `call_agent` yardimci fonksiyonu tanimlanir. `call_agent` icerisinde, kullanicinin sorgusu 'user' rolune sahip bir types.Content nesnesi olarak bicimlendirilir. runner.run yontemi, kullanici kimligi, oturum kimligi ve yeni mesaj icerigi ile cagrilir. runner.run yontemi, agent'in eylemlerini ve yanitlarini temsil eden olaylarin bir listesini dondurur. Kod, nihai yaniti bulmak icin bu olaylari yineler. Bir olay nihai yanit olarak tanimlanirsa, o yanitin metin icerigi cikarilir. Cikarilan agent yaniti daha sonra konsola yazdirilir. Son olarak, `call_agent` fonksiyonu agent'i calisma halinde gostermek icin "what's the latest ai news?" sorgusuyla cagrilir.

**Kod yurutme:** Google ADK, dinamik kod yurutme icin bir ortam dahil olmak uzere ozelesmis gorevler icin entegre bilesenler icerir. `built_in_code_execution` araci, bir agent'a sandbox'lu bir Python yorumlayicisi saglar. Bu, modelin hesaplama gorevleri gerceklestirmek, veri yaplarini manipule etmek ve prosedural betikler yurutmek icin kod yazip calistirmasina olanak tanir. Bu islevsellik, deterministik mantik ve hassas hesaplamalar gerektiren ve olasiliksal dil uretiminin kapsaminin disinda kalan problemleri ele almak icin kritiktir.

```python
import os
import getpass
import asyncio
import nest_asyncio
from typing import List
from dotenv import load_dotenv
import logging

from google.adk.agents import Agent as ADKAgent, LlmAgent
from google.adk.runners import Runner
from google.adk.sessions import InMemorySessionService
from google.adk.tools import google_search
from google.adk.code_executors import BuiltInCodeExecutor
from google.genai import types


# Define variables required for Session setup and Agent execution
APP_NAME = "calculator"
USER_ID = "user1234"
SESSION_ID = "session_code_exec_async"


# Agent Definition
code_agent = LlmAgent(
    name="calculator_agent",
    model="gemini-2.0-flash",
    code_executor=BuiltInCodeExecutor(),
    instruction="""You are a calculator agent.
    When given a mathematical expression, write and execute Python code to calculate the result.
    Return only the final numerical result as plain text, without markdown or code blocks.
    """,
    description="Executes Python code to perform calculations.",
)


# Agent Interaction (Async)
async def call_agent_async(query: str):
    # Session and Runner
    session_service = InMemorySessionService()
    await session_service.create_session(app_name=APP_NAME, user_id=USER_ID, session_id=SESSION_ID)

    runner = Runner(agent=code_agent, app_name=APP_NAME, session_service=session_service)

    content = types.Content(role='user', parts=[types.Part(text=query)])
    print(f"\n--- Running Query: {query} ---")

    try:
        # Use run_async
        async for event in runner.run_async(user_id=USER_ID, session_id=SESSION_ID, new_message=content):
            print(f"Event ID: {event.id}, Author: {event.author}")

            if event.content and event.content.parts and event.is_final_response():
                for part in event.content.parts:  # Iterate through all parts
                    if getattr(part, "executable_code", None):
                        # Access the actual code string via .code
                        print(f"  Debug: Agent generated code:\n```python\n{part.executable_code.code}\n```")
                    elif getattr(part, "code_execution_result", None):
                        # Access outcome and output correctly
                        print(
                            "  Debug: Code Execution Result: "
                            f"{part.code_execution_result.outcome} - Output:\n{part.code_execution_result.output}"
                        )
                    elif getattr(part, "text", None) and not part.text.isspace():
                        # Also print any text parts found in any event for debugging
                        print(f"  Text: '{part.text.strip()}'")

                # --- Check for final response AFTER specific parts ---
                text_parts = [part.text for part in event.content.parts if getattr(part, "text", None)]
                final_result = "".join(text_parts)
                print(f"==> Final Agent Response: {final_result}")

    except Exception as e:
        print(f"ERROR during agent run: {e}")

    print("-" * 30)


# Main async function to run the examples
async def main():
    await call_agent_async("Calculate the value of (5 + 7) * 3")
    await call_agent_async("What is 10 factorial?")


# Execute the main async function
try:
    nest_asyncio.apply()
    asyncio.run(main())
except RuntimeError as e:
    # Handle specific error when running asyncio.run in an already running loop (like Jupyter/Colab)
    if "cannot be called from a running event loop" in str(e):
        print("\nRunning in an existing event loop (like Colab/Jupyter).")
        print("Please run `await main()` in a notebook cell instead.")
        # If in an interactive environment like a notebook, you might need to run:
        # await main()
    else:
        raise e  # Re-raise other runtime errors
```

Bu betik, matematiksel problemleri Python kodu yazarak ve yuruterek cozen bir agent olusturmak icin Google'in Agent Development Kit (ADK) kullanir. Ozellikle hesap makinesi olarak hareket etmesi talimat verilen bir LlmAgent tanimlar ve `built_in_code_execution` araci ile donatir. Birincil mantik, kullanicinin sorgusunu agent'in runner'ina gonderen ve ortaya cikan olaylari isleyen `call_agent_async` fonksiyonunda bulunur. Bu fonksiyon icerisinde, asenkron bir dongu olaylar boyunca yineleyerek, hata ayiklama icin olusturulan Python kodunu ve yurutme sonucunu yazdirir. Kod, bu ara adimlari sayisal yaniti iceren nihai olaydan dikkatlice ayirt eder. Son olarak, bir ana fonksiyon hesaplama yetenegini gostermek icin agent'i iki farkli matematiksel ifadeyle calistirir.

**Kurumsal arama:** Bu kod, Python'da google.adk kutuphanesini kullanan bir Google ADK uygulamasi tanimlar. Ozellikle, belirli bir Vertex AI Search veri deposunu arayarak sorulari yanitlamak icin tasarlanmis bir VSearchAgent kullanir. Kod, `q2_strategy_vsearch_agent` adli bir VSearchAgent baslatir ve bir aciklama, kullanilacak model ("gemini-2.0-flash-exp") ve Vertex AI Search veri deposunun kimligini saglar. `DATASTORE_ID`'nin bir ortam degiskeni olarak ayarlanmasi beklenir. Ardindan agent icin bir Runner kurar ve konusma gecmisini yonetmek icin InMemorySessionService kullanir. Agent ile etkilesim icin `call_vsearch_agent_async` asenkron fonksiyonu tanimlanir. Bu fonksiyon bir sorgu alir, bir mesaj icerik nesnesi olusturur ve sorguyu agent'a gondermek icin runner'in `run_async` yontemini cagirirr. Fonksiyon daha sonra agent'in yanitini geldiginde konsola geri akisir. Ayrica, veri deposundan kaynak atifllari dahil olmak uzere nihai yanit hakkinda bilgi yazdirir. Yanlis veri deposu kimligi veya eksik izinler gibi potansiyel sorunlar hakkinda bilgilendirici mesajlar saglayan hata yonetimi dahil edilmistir. Ornek sorgularla agent'in nasil cagirilacagini gostermek icin `run_vsearch_example` adli baska bir asenkron fonksiyon saglanmistir. Ana yurutme blogu `DATASTORE_ID`'nin ayarlanip ayarlanmadigini kontrol eder ve ardindan ornegi asyncio.run kullanarak calistirir. Jupyter not defteri gibi halihazirda calisan bir olay dongusu olan bir ortamda kodun calistirilmasi durumunu ele almak icin bir kontrol icerir.

```python
import asyncio
import os

from google.genai import types
from google.adk import agents
from google.adk.runners import Runner
from google.adk.sessions import InMemorySessionService


# --- Configuration ---
# Ensure you have set your GOOGLE_API_KEY and DATASTORE_ID environment variables
# For example:
# os.environ["GOOGLE_API_KEY"] = "YOUR_API_KEY"
# os.environ["DATASTORE_ID"] = "YOUR_DATASTORE_ID"
DATASTORE_ID = os.environ.get("DATASTORE_ID")


# --- Application Constants ---
APP_NAME = "vsearch_app"
USER_ID = "user_123"  # Example User ID
SESSION_ID = "session_456"  # Example Session ID


# --- Agent Definition (Updated with the newer model from the guide) ---
vsearch_agent = agents.VSearchAgent(
    name="q2_strategy_vsearch_agent",
    description="Answers questions about Q2 strategy documents using Vertex AI Search.",
    model="gemini-2.0-flash-exp",  # Updated model based on the guide's examples
    datastore_id=DATASTORE_ID,
    model_parameters={"temperature": 0.0},
)


# --- Runner and Session Initialization ---
runner = Runner(
    agent=vsearch_agent,
    app_name=APP_NAME,
    session_service=InMemorySessionService(),
)


# --- Agent Invocation Logic ---
async def call_vsearch_agent_async(query: str):
    """Initializes a session and streams the agent's response."""
    print(f"User: {query}")
    print("Agent: ", end="", flush=True)
    try:
        # Construct the message content correctly
        content = types.Content(role='user', parts=[types.Part(text=query)])

        # Process events as they arrive from the asynchronous runner
        async for event in runner.run_async(
            user_id=USER_ID,
            session_id=SESSION_ID,
            new_message=content,
        ):
            # For token-by-token streaming of the response text
            if hasattr(event, "content_part_delta") and event.content_part_delta:
                print(event.content_part_delta.text, end="", flush=True)

            # Process the final response and its associated metadata
            if event.is_final_response():
                print()  # Newline after the streaming response
                if getattr(event, "grounding_metadata", None):
                    print(
                        f"  (Source Attributions: "
                        f"{len(event.grounding_metadata.grounding_attributions)} sources found)"
                    )
                else:
                    print("  (No grounding metadata found)")
                print("-" * 30)
    except Exception as e:
        print(f"\nAn error occurred: {e}")
        print("Please ensure your datastore ID is correct and that the service account has the necessary permissions.")
        print("-" * 30)


# --- Run Example ---
async def run_vsearch_example():
    # Replace with a question relevant to YOUR datastore content
    await call_vsearch_agent_async("Summarize the main points about the Q2 strategy document.")
    await call_vsearch_agent_async("What safety procedures are mentioned for lab X?")


# --- Execution ---
if __name__ == "__main__":
    if not DATASTORE_ID:
        print("Error: DATASTORE_ID environment variable is not set.")
    else:
        try:
            asyncio.run(run_vsearch_example())
        except RuntimeError as e:
            # This handles cases where asyncio.run is called in an environment
            # that already has a running event loop (like a Jupyter notebook).
            if "cannot be called from a running event loop" in str(e):
                print("Skipping execution in a running event loop. Please run this script directly.")
            else:
                raise e
```

Genel olarak, bu kod bir veri deposunda depolanan bilgilere dayali olarak sorulari yanitlamak icin Vertex AI Search'ten yararlanan bir konusmasal yapay zeka uygulamasi olusturmak icin temel bir cerceve sunar. Bir agent tanimlamayi, bir runner kurmayi ve asenkron olarak agent ile etkilesime girerken yaniti akisla nasil gosterecegini gosterir. Odak noktasi, kullanici sorgularini yanitlamak icin belirli bir veri deposundan bilgi erisimi ve sentezlemektir.

**Vertex Extensions:** Vertex AI extension'i, bir modelin gercek zamanli veri isleme ve eylem yurutme icin harici API'lere baglanmasini saglayan yapilandirilmis bir API sarmalayicisidir. Extension'lar kurumsal duzeyde guvenlik, veri gizliligi ve performans garantileri sunar. Kod olusturup calistirma, web sitelerini sorgulama ve ozel veri depolarindan bilgi analiz etme gibi gorevler icin kullanilabilirler. Google, Code Interpreter ve Vertex AI Search gibi yaygin kullanim alanlari icin onceden olusturulmus extension'lar sunar ve ozel olanlar olusturma secenegi de vardir. Extension'larin birincil faydasi, guclu kurumsal kontroller ve diger Google urunleriyle sorunsuz entegrasyondur. Extension'lar ile function calling arasindaki temel fark, yurutulme seklindedir: Vertex AI extension'lari otomatik olarak yurutur, function call'lar ise kullanici veya istemci tarafindan manuel yurutme gerektirir.

## Bir Bakista

**Ne:** LLM'ler guclu metin uretecleridir, ancak dis dunyadan temel olarak kopukturlar. Bilgileri statiktir, egitildikleri verilerle sinirlidir ve eylem gercceklestirme veya gercek zamanli bilgi alma yeteneginden yoksundurlar. Bu dogal sinirlilik, harici API'ler, veritabanlari veya hizmetlerle etkilesim gerektiren gorevleri tamamlamalarini engeller. Bu harici sistemlere bir kopru olmadan, gercek dunya problemlerini cozmedeki faydalari ciddi sekilde kisitlanir.

**Neden:** Arac Kullanimi kalibi, genellikle function calling araciligiyla uygulanir ve bu soruna standart bir cozum sunar. Mevcut harici fonksiyonlari veya "araclari", LLM'nin anlayabilecegi sekilde tanimlayarak calisir. Kullanicinin istegine dayanarak, agentic LLM bir aracin gerekli olup olmadigina karar verebilir ve hangi fonksiyonun hangi argumanlarda cagrilacagini belirten yapilandirilmis bir veri nesnesi (JSON gibi) olusturabilir. Bir orkestrasyon katmani bu fonksiyon cagrisini yurutur, sonucu alir ve LLM'ye geri besler. Bu, LLM'nin guncel, harici bilgileri veya bir eylemin sonucunu nihai yanitina dahil etmesine olanak tanir ve etkili bir sekilde ona eylem yapma yetenegi verir.

**Temel kural:** Arac Kullanimi kalibini, bir agent'in LLM'nin dahili bilgisinin disina cikarak dis dunya ile etkilesime gecmesi gerektiginde kullanin. Bu, gercek zamanli veri gerektiren gorevler (ornegin hava durumu, hisse senedi fiyatlari kontrol etme), ozel veya tescilli bilgilere erisim (ornegin bir sirketin veritabanini sorgulama), hassas hesaplamalar yapma, kod yurutme veya diger sistemlerde eylem tetikleme (ornegin e-posta gonderme, akilli cihazlari kontrol etme) icin gereklidir.

**Gorsel ozet:**

![Tool Use Design Pattern](../assets/Tool_Use_Design_Pattern.png)

Sekil 2: Arac kullanimi tasarim kalibi

## Temel Cikarimlar

* Arac Kullanimi (Function Calling), agent'larin harici sistemlerle etkilesime girmesine ve dinamik bilgilere erismesine olanak tanir.
* LLM'nin anlayabilecegi net aciklamalar ve parametrelerle araclarin tanimlanmasini icerir.
* LLM, bir araci ne zaman kullanacagina karar verir ve yapilandirilmis fonksiyon cagirilari olusturur.
* Agentic cerceveler, gercek arac cagrilarini yurutur ve sonuclari LLM'ye geri dondurur.
* Arac Kullanimi, gercek dunya eylemleri gerceklestirebilen ve guncel bilgi saglayabilen agent'lar olusturmak icin gereklidir.
* LangChain, @tool decorator'u kullanarak arac tanimini basitlestirr ve arac kullanan agent'lar olusturmak icin `create_tool_calling_agent` ve AgentExecutor saglar.
* Google ADK, Google Search, Code Execution ve Vertex AI Search Tool gibi cok faydali onceden olusturulmus araclara sahiptir.

## Sonuc

Arac Kullanimi kalibi, buyuk dil modellerinin islevsel kapsamini dogas geregi metin uretme yeteneklerinin otesine genisletmek icin kritik bir mimari ilkedir. Bir modeli harici yazilim ve veri kaynaklariyla arayuz olusturma yetenegiyle donatarak, bu paradigma bir agent'in eylemler gerceklestirmesine, hesaplamalar yapmasina ve diger sistemlerden bilgi almasina olanak tanir. Bu surec, modelin bir kullanicinin sorgusunu yerine getirmek icin bunu yapmanin gerekli oldugunu belirlediginde harici bir araci cagirmak icin yapilandirilmis bir istek olusturmasini icerir. LangChain, Google ADK ve Crew AI gibi cerceveler, bu harici araclarin entegrasyonunu kolaylastiran yapilandirilmis soyutlamalar ve bilesenler sunar. Bu cerceveler, arac ozelliklerini modele sunma ve modelin sonraki arac kullanim isteklerini ayristirma surecini yonetir. Bu, harici dijital ortamlarla etkilesime girebilen ve eylem yapabilen gelismis agentic sistemlerin gelistirilmesini basitlestirirr.

## Kaynaklar

1. LangChain Documentation (Tools): [https://python.langchain.com/docs/integrations/tools/](https://python.langchain.com/docs/integrations/tools/)
2. Google Agent Developer Kit (ADK) Documentation (Tools): [https://google.github.io/adk-docs/tools/](https://google.github.io/adk-docs/tools/)
3. OpenAI Function Calling Documentation: [https://platform.openai.com/docs/guides/function-calling](https://platform.openai.com/docs/guides/function-calling)
4. CrewAI Documentation (Tools): [https://docs.crewai.com/concepts/tools](https://docs.crewai.com/concepts/tools)
