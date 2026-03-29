# Bolum 3: Paralelizasyon (Parallelization)

## Paralelizasyon Kalibina Genel Bakis

Onceki bolumlerde, sirali is akislari icin Prompt Zincirleme'yi ve dinamik karar verme ile farkli yollar arasindaki gecisler icin Yonlendirme'yi (Routing) inceledik. Bu kalipler gerekli olsa da, bircok karmasik agentic gorev, birbiri ardina degil *es zamanli* olarak yurutulebilen birden fazla alt gorev icerir. **Paralelizasyon** kalibinin kritik hale geldigi nokta burasdir.

Paralelizasyon, LLM cagirilari, arac kullanimlari veya hatta tamamen alt agent'lar gibi birden fazla bileseni es zamanli olarak yurutmeyi icerir (bkz. Sekil 1). Bir adimin tamamlanmasini beklemeden sonrakini baslatmak yerine, paralel yurutme bagimsiz gorevlerin ayni anda calismasina olanak tanir ve bagimsiz parcalara ayrilabilen gorevler icin genel yurutme suresini onemli olcude azaltir.

Bir konuyu arastirmak ve bulgularini ozetlemek icin tasarlanmis bir agent dusunun. Sirali bir yaklasim su sekilde olabilir:

1. Kaynak A'yi ara.
2. Kaynak A'yi ozetle.
3. Kaynak B'yi ara.
4. Kaynak B'yi ozetle.
5. A ve B ozetlerinden nihai bir yanit sentezle.

Paralel bir yaklasim ise su sekilde olabilir:

1. Kaynak A'yi ara *ve* Kaynak B'yi es zamanli olarak ara.
2. Her iki arama tamamlandiginda, Kaynak A'yi ozetle *ve* Kaynak B'yi es zamanli olarak ozetle.
3. A ve B ozetlerinden nihai bir yanit sentezle (bu adim tipik olarak siralidir ve paralel adimlarin bitmesini bekler).

Temel fikir, is akisinin diger parcalarin ciktisina bagli olmayan bolulerini belirlemek ve bunlari paralel olarak yurutmektir. Bu, ozellikle gecikmeye sahip harici hizmetlerle (API'ler veya veritabanlari gibi) calisirken etkilidir, cunku birden fazla istegi es zamanli olarak gonderebilirsiniz.

Paralelizasyonun uygulanmasi genellikle asenkron yurutme veya coklu is parcacigi/coklu islemi destekleyen cerceveler gerektirir. Modern agentic cerceveler, asenkron islemler goz onunde bulundurularak tasarlanmistir ve paralel calisabilecek adimlari kolayca tanimlamaniza olanak tanir.

![Parallelization with Sub-Agents](../assets/Parallelization_with_Sub_Agents.png)

Sekil 1. Alt agent'larla paralelizasyon ornegi

LangChain, LangGraph ve Google ADK gibi cerceveler, paralel yurutme icin mekanizmalar saglar. LangChain Expression Language (LCEL) icerisinde, calistirilabilir nesneleri | (sirali icin) gibi operatorler kullanarak birlestirerek ve zincirlerinizi veya grafiklerinizi es zamanli olarak yurutulen dallara sahip olacak sekilde yapilandirarak paralel yurutme elde edebilirsiniz. Grafik yapisiyla LangGraph, tek bir durum gecisinden yurutulebilecek birden fazla dugum tanimlameniza olanak tanir ve is akisinda paralel dallari etkili bir sekilde mumkun kilar. Google ADK, agent'larin paralel yurutumunu kolaylastirmak ve yonetmek icin saglam, yerel mekanizmalar sunar ve karmasik, multi-agent sistemlerin verimliligini ve olceklenebilirligini onemli olcude arttirir. ADK cercevesindeki bu dogal yetenek, gelistiricilerin birden fazla agent'in sirali degil es zamanli olarak calısabilecegi cozumler tasarlamasina ve uygulamasina olanak tanir.

Paralelizasyon kalibi, ozellikle birden fazla bagimsiz arama, hesaplama veya harici hizmetlerle etkilesim iceren gorevlerle karsilastiginda, agentic sistemlerin verimliligini ve yanit verebilirligini iyilestirmek icin hayati onem tasir. Karmasik agent is akislarinin performansini optimize etmek icin temel bir tekniktir.

## Pratik Uygulamalar ve Kullanim Alanlari

Paralelizasyon, cesitli uygulamalarda agent performansini optimize etmek icin guclu bir kaliptir:

### 1. Bilgi Toplama ve Arastirma

Birden fazla kaynaktan es zamanli olarak bilgi toplamak klasik bir kullanim alanidir.

* **Kullanim Alani:** Bir sirketi arastiran bir agent.
  * **Paralel Gorevler:** Haber makalelerini arama, borsa verilerini cekme, sosyal medya bahislerini kontrol etme ve sirket veritabanini sorgulama -- hepsi ayni anda.
  * **Fayda:** Sirali aramalara gore cok daha hizli kapsamli bir gorunum elde eder.

### 2. Veri Isleme ve Analiz

Farkli analiz tekniklerini uygulama veya farkli veri segmentlerini es zamanli olarak isleme.

* **Kullanim Alani:** Musteri geri bildirimlerini analiz eden bir agent.
  * **Paralel Gorevler:** Duygu analizi yapma, anahtar kelimeleri cikarma, geri bildirimleri kategorize etme ve acil sorunlari belirleme -- hepsi bir geri bildirim yigininda es zamanli olarak.
  * **Fayda:** Hizli bir sekilde cok yonlu bir analiz saglar.

### 3. Coklu API veya Arac Etkilesimi

Farkli bilgi turleri toplamak veya farkli eylemler gerceklestirmek icin birden fazla bagimsiz API veya araci cagirma.

* **Kullanim Alani:** Seyahat planlama agent'i.
  * **Paralel Gorevler:** Ucus fiyatlarini kontrol etme, otel musaitligini arama, yerel etkinlikleri arastirma ve restoran onerilerini bulma -- hepsi es zamanli olarak.
  * **Fayda:** Tam bir seyahat planini daha hizli sunar.

### 4. Birden Fazla Bilesene Sahip Icerik Olusturma

Karmasik bir icerigin farkli bolulerini paralel olarak olusturma.

* **Kullanim Alani:** Pazarlama e-postasi olusturan bir agent.
  * **Paralel Gorevler:** Konu satiri olusturma, e-posta govdesini taslak hazirlama, ilgili bir gorsel bulma ve harekete gecirici mesaj metni olusturma -- hepsi es zamanli olarak.
  * **Fayda:** Nihai e-postayi daha verimli bir sekilde birlestirir.

### 5. Dogrulama ve Gecerlilik Kontrolu

Birden fazla bagimsiz kontrol veya dogrulamayi es zamanli olarak gerceklestirme.

* **Kullanim Alani:** Kullanici girdisini dogrulayan bir agent.
  * **Paralel Gorevler:** E-posta formatini kontrol etme, telefon numarasini dogrulama, adresi bir veritabanina karsi dogrulama ve kufur kontrolu yapma -- hepsi es zamanli olarak.
  * **Fayda:** Girdi gecerliligi hakkinda daha hizli geri bildirim saglar.

### 6. Cok Modlu Isleme

Ayni girdinin farkli modalitelerini (metin, gorsel, ses) es zamanli olarak isleme.

* **Kullanim Alani:** Metin ve gorsel iceren bir sosyal medya gondersini analiz eden bir agent.
  * **Paralel Gorevler:** Duygu ve anahtar kelimeler icin metni analiz etme *ve* nesneler ve sahne tanimi icin gorseli analiz etme -- hepsi es zamanli olarak.
  * **Fayda:** Farkli modalitelerden gelen icegoruleri daha hizli birlestirir.

### 7. A/B Testi veya Coklu Secenek Olusturma

En iyisini secmek icin bir yanit veya ciktinin birden fazla varyasyonunu paralel olarak olusturma.

* **Kullanim Alani:** Farkli yaratici metin secenekleri olusturan bir agent.
  * **Paralel Gorevler:** Biraz farkli prompt'lar veya modeller kullanarak bir makale icin uc farkli baslik olusturma -- hepsi es zamanli olarak.
  * **Fayda:** En iyi secenegin hizli bir sekilde karsilastirilmasina ve secilmesine olanak tanir.

Paralelizasyon, agentic tasarimda temel bir optimizasyon teknigi olup, gelistiricilerin bagimsiz gorevler icin es zamanli yurutmeden yararlanarak daha performansli ve duyarli uygulamalar olusturmasina olanak tanir.

## Uygulamali Kod Ornegi (LangChain)

LangChain cercevesinde paralel yurutme, LangChain Expression Language (LCEL) tarafindan kolaylastirilir. Temel yontem, birden fazla calistirilabilir bileseni bir sozluk veya liste yapisi icerisinde yapilandirmayi icerir. Bu koleksiyon, zincirdeki sonraki bir bilesene girdi olarak aktarildiginda, LCEL calisma zamani icerdigi calistirilabilirleri es zamanli olarak yurutur.

LangGraph baglaminda, bu ilke grafigin topolojisine uygulanir. Paralel is akislari, dogrudan sirali bagimliliklari olmayan birden fazla dugumun tek bir ortak dugumden baslatilabilecegi sekilde grafik mimarisi olusturularak tanimlanir. Bu paralel yollar, sonuclari grafikte sonraki bir yakinlasma noktasinda toplanmadan once bagimsiz olarak yurutulur.

Asagidaki uygulama, LangChain cercevesiyle olusturulmus bir paralel isleme is akisini gostermektedir. Bu is akisi, tek bir kullanici sorgusuna yanit olarak iki bagimsiz islemi es zamanli olarak yurutmek icin tasarlanmistir. Bu paralel surecler, ayri zincirler veya fonksiyonlar olarak baslatilir ve ilgili ciktilari daha sonra birlesik bir sonucta toplanir.

Bu uygulamanin on kosullari, langchain, langchain-community ve langchain-openai gibi bir model saglayici kutuphanesi gibi gerekli Python paketlerinin kurulmasini icermektedir. Ayrica, secilen dil modeli icin gecerli bir API anahtari, kimlik dogrulama icin yerel ortamda yapilandirilmis olmalidir.

```python
import os
import asyncio
from typing import Optional

from langchain_openai import ChatOpenAI
from langchain_core.prompts import ChatPromptTemplate
from langchain_core.output_parsers import StrOutputParser
from langchain_core.runnables import Runnable, RunnableParallel, RunnablePassthrough


# --- Configuration ---
# Ensure your API key environment variable is set (e.g., OPENAI_API_KEY)
try:
    llm: Optional[ChatOpenAI] = ChatOpenAI(model="gpt-4o-mini", temperature=0.7)
except Exception as e:
    print(f"Error initializing language model: {e}")
    llm = None


# --- Define Independent Chains ---
# These three chains represent distinct tasks that can be executed in parallel.
summarize_chain: Runnable = (
    ChatPromptTemplate.from_messages([
        ("system", "Summarize the following topic concisely:"),
        ("user", "{topic}"),
    ])
    | llm
    | StrOutputParser()
)

questions_chain: Runnable = (
    ChatPromptTemplate.from_messages([
        ("system", "Generate three interesting questions about the following topic:"),
        ("user", "{topic}"),
    ])
    | llm
    | StrOutputParser()
)

terms_chain: Runnable = (
    ChatPromptTemplate.from_messages([
        ("system", "Identify 5-10 key terms from the following topic, separated by commas:"),
        ("user", "{topic}"),
    ])
    | llm
    | StrOutputParser()
)


# --- Build the Parallel + Synthesis Chain ---
# 1. Define the block of tasks to run in parallel. The results of these,
#    along with the original topic, will be fed into the next step.
map_chain = RunnableParallel(
    {
        "summary": summarize_chain,
        "questions": questions_chain,
        "key_terms": terms_chain,
        "topic": RunnablePassthrough(),  # Pass the original topic through
    }
)

# 2. Define the final synthesis prompt which will combine the parallel results.
synthesis_prompt = ChatPromptTemplate.from_messages([
    (
        "system",
        """Based on the following information:
        Summary: {summary}
        Related Questions: {questions}
        Key Terms: {key_terms}
        Synthesize a comprehensive answer."""
    ),
    ("user", "Original topic: {topic}"),
])

# 3. Construct the full chain by piping the parallel results directly
#    into the synthesis prompt, followed by the LLM and output parser.
full_parallel_chain = map_chain | synthesis_prompt | llm | StrOutputParser()


# --- Run the Chain ---
async def run_parallel_example(topic: str) -> None:
    """
    Asynchronously invokes the parallel processing chain with a specific topic
    and prints the synthesized result.

    Args:
        topic: The input topic to be processed by the LangChain chains.
    """
    if not llm:
        print("LLM not initialized. Cannot run example.")
        return

    print(f"\n--- Running Parallel LangChain Example for Topic: '{topic}' ---")
    try:
        # The input to `ainvoke` is the single 'topic' string,
        # then passed to each runnable in the `map_chain`.
        response = await full_parallel_chain.ainvoke(topic)
        print("\n--- Final Response ---")
        print(response)
    except Exception as e:
        print(f"\nAn error occurred during chain execution: {e}")


if __name__ == "__main__":
    test_topic = "The history of space exploration"
    # In Python 3.7+, asyncio.run is the standard way to run an async function.
    asyncio.run(run_parallel_example(test_topic))
```

Saglanan Python kodu, paralel yurutmeden yararlanarak belirli bir konuyu verimli bir sekilde islemek icin tasarlanmis bir LangChain uygulamasi uygular. asyncio'nun paralelizm degil, es zamanlilik (concurrency) sagladigini unutmayin. Bunu, bir gorev bosta oldugundan (ornegin bir ag istegi beklediginde) gorevler arasinda akilli bir sekilde gecis yapan bir olay dongusu kullanarak tek bir is parcacigi uzerinde basarir. Bu, birden fazla gorevin ayni anda ilerlediginin etkisini yaratir, ancak kodun kendisi hala tek bir is parcacigi tarafindan yurutulmekte olup Python'un Global Interpreter Lock (GIL) tarafindan sinirlandirilmistir.

Kod, `langchain_openai` ve `langchain_core`'dan dil modelleri, prompt'lar, cikti ayristirma ve calistirilabilir yapilar icin temel modulleri iceri aktararak baslar. Kod, ozellikle "gpt-4o-mini" modelini kullanan bir ChatOpenAI ornegi baslatmayi dener ve yaraticilik kontrolu icin belirtilmis bir sicaklik degerine sahiptir. Dil modeli baslatma sirasinda saglamlik icin try-except blogu kullanilir. Daha sonra, her biri girdi konusunda ayri bir gorev gerceklestirmek uzere tasarlanmis uc bagimsiz LangChain "zinciri" tanilanir. Ilk zincir, konuyu kisa ve oz bir sekilde ozetlemek icindir ve bir sistem mesaji ile konu yer tutucusunu iceren bir kullanici mesaji kullanir. Ikinci zincir, konuyla ilgili uc ilginc soru olusturmak uzere yapilandirilmistir. Ucuncu zincir, girdi konusundan 5 ila 10 anahtar terim belirlemek icin kurulmustur ve bunlarin virgule ayrilmis olarak istenmesi saglanir. Bu bagimsiz zincirlerin her biri, belirli gorevine uyarlanmis bir ChatPromptTemplate, ardindan baslatilan dil modeli ve ciktiyi bir dize olarak bicimlemek icin bir StrOutputParser'dan olusur.

Ardindan, bu uc zinciri bir araya getirmek icin bir RunnableParallel blogu olusturulur ve bunlarin es zamanli olarak yurutulmesine olanak tanir. Bu paralel calistirilabilir, orijinal girdi konusunun sonraki adimlar icin de erisilebilir olmasini saglamak icin bir RunnablePassthrough da icerir. Nihai sentez adimi icin, ozeti, sorulari, anahtar terimleri ve orijinal konuyu girdi olarak alarak kapsamli bir yanit olusturan ayri bir ChatPromptTemplate tanimlanir. `full_parallel_chain` adli tam uctan uca isleme zinciri, `map_chain`'i (paralel blok) sentez prompt'una, ardindan dil modeline ve cikti ayristiricisina siralandirarak olusturulur. Bu `full_parallel_chain`'in nasil cagrilacagini gostermek icin `run_parallel_example` adli asenkron bir fonksiyon saglanmistir. Bu fonksiyon, konuyu girdi olarak alir ve asenkron zinciri calistirmak icin invoke kullanir. Son olarak, standart Python `if __name__ == "__main__":` blogu, `run_parallel_example`'in bu durumda "The history of space exploration" ornk konusuyla nasil yurutulecegini, asenkron yurutmeyi yonetmek icin asyncio.run kullanarak gosterir.

Ozunde, bu kod belirli bir konu icin birden fazla LLM cagrisinin (ozetleme, sorular ve terimler icin) ayni anda gerceklestigi ve sonuclarinin nihai bir LLM cagrisiyla birlestirildigi bir is akisi olusturur. Bu, LangChain kullanarak bir agentic is akisinda paralelizasyonun temel fikrini sergiler.

## Uygulamali Kod Ornegi (Google ADK)

Simdi dikkatimizi Google ADK cercevesi icerisinde bu kavramlari gosteren somut bir ornege cevirelim. ADK temel bilesenlerinin, ornegin ParallelAgent ve SequentialAgent'in, es zamanli yurutmeden yararlanarak gelistirilmis verimlilik icin bir agent akisi olusturmak icin nasil uygulanabilecegini inceleyecegiz.

```python
from google.adk.agents import LlmAgent, ParallelAgent, SequentialAgent
from google.adk.tools import google_search

GEMINI_MODEL = "gemini-2.0-flash"


# --- 1. Define Researcher Sub-Agents (to run in parallel) ---

# Researcher 1: Renewable Energy
researcher_agent_1 = LlmAgent(
    name="RenewableEnergyResearcher",
    model=GEMINI_MODEL,
    instruction="""You are an AI Research Assistant specializing in energy. Research the latest advancements in 'renewable energy sources'. Use the Google Search tool provided. Summarize your key findings concisely (1-2 sentences). Output *only* the summary. """,
    description="Researches renewable energy sources.",
    tools=[google_search],
    # Store result in state for the merger agent
    output_key="renewable_energy_result",
)

# Researcher 2: Electric Vehicles
researcher_agent_2 = LlmAgent(
    name="EVResearcher",
    model=GEMINI_MODEL,
    instruction="""You are an AI Research Assistant specializing in transportation. Research the latest developments in 'electric vehicle technology'. Use the Google Search tool provided. Summarize your key findings concisely (1-2 sentences). Output *only* the summary. """,
    description="Researches electric vehicle technology.",
    tools=[google_search],
    # Store result in state for the merger agent
    output_key="ev_technology_result",
)

# Researcher 3: Carbon Capture
researcher_agent_3 = LlmAgent(
    name="CarbonCaptureResearcher",
    model=GEMINI_MODEL,
    instruction="""You are an AI Research Assistant specializing in climate solutions. Research the current state of 'carbon capture methods'. Use the Google Search tool provided. Summarize your key findings concisely (1-2 sentences). Output *only* the summary. """,
    description="Researches carbon capture methods.",
    tools=[google_search],
    # Store result in state for the merger agent
    output_key="carbon_capture_result",
)


# --- 2. Create the ParallelAgent (Runs researchers concurrently) ---
# This agent orchestrates the concurrent execution of the researchers.
# It finishes once all researchers have completed and stored their results in state.
parallel_research_agent = ParallelAgent(
    name="ParallelWebResearchAgent",
    sub_agents=[researcher_agent_1, researcher_agent_2, researcher_agent_3],
    description="Runs multiple research agents in parallel to gather information.",
)


# --- 3. Define the Merger Agent (Runs after the parallel agents) ---
# This agent takes the results stored in the session state by the parallel agents
# and synthesizes them into a single, structured response with attributions.
merger_agent = LlmAgent(
    name="SynthesisAgent",
    model=GEMINI_MODEL,  # Or potentially a more powerful model if needed for synthesis
    instruction="""You are an AI Assistant responsible for combining research findings into a structured report. Your primary task is to synthesize the following research summaries, clearly attributing findings to their source areas. Structure your response using headings for each topic. Ensure the report is coherent and integrates the key points smoothly.

**Crucially:** Your entire response MUST be grounded *exclusively* on the information provided in the 'Input Summaries' below. Do NOT add any external knowledge, facts, or details not present in these specific summaries.

**Input Summaries:**
*   **Renewable Energy:**
    {renewable_energy_result}
*   **Electric Vehicles:**
    {ev_technology_result}
*   **Carbon Capture:**
    {carbon_capture_result}

**Output Format:**
## Summary of Recent Sustainable Technology Advancements

### Renewable Energy Findings (Based on RenewableEnergyResearcher's findings)
[Synthesize and elaborate *only* on the renewable energy input summary provided above.]

### Electric Vehicle Findings (Based on EVResearcher's findings)
[Synthesize and elaborate *only* on the EV input summary provided above.]

### Carbon Capture Findings (Based on CarbonCaptureResearcher's findings)
[Synthesize and elaborate *only* on the carbon capture input summary provided above.]

### Overall Conclusion
[Provide a brief (1-2 sentence) concluding statement that connects *only* the findings presented above.]

Output *only* the structured report following this format. Do not include introductory or concluding phrases outside this structure, and strictly adhere to using only the provided input summary content.
""",
    description="Combines research findings from parallel agents into a structured, cited report, strictly grounded on provided inputs.",
    # No tools needed for merging
    # No output_key needed here, as its direct response is the final output of the sequence
)


# --- 4. Create the SequentialAgent (Orchestrates the overall flow) ---
# This is the main agent that will be run. It first executes the ParallelAgent
# to populate the state, and then executes the MergerAgent to produce the final output.
sequential_pipeline_agent = SequentialAgent(
    name="ResearchAndSynthesisPipeline",
    # Run parallel research first, then merge
    sub_agents=[parallel_research_agent, merger_agent],
    description="Coordinates parallel research and synthesizes the results.",
)

root_agent = sequential_pipeline_agent
```

Bu kod, surdurulebilir teknoloji gelismeleri hakkinda bilgi arastirmak ve sentezlemek icin kullanilan bir multi-agent sistemi tanimlar. Ozelesmis arastirmacilar olarak gorev yapmak uzere uc LlmAgent ornegi kurar. `ResearcherAgent_1` yenilenebilir enerji kaynaklarina, `ResearcherAgent_2` elektrikli arac teknolojisine ve `ResearcherAgent_3` karbon yakalama yontemlerine odaklanir. Her arastirmaci agent'i, `GEMINI_MODEL` ve `google_search` aracini kullanmak uzere yapilandirilmistir. Bulgularini kisa ve oz bir sekilde (1-2 cumle) ozetlemek ve bu ozetleri `output_key` kullanarak oturum durumunda depolamak uzere talimatlandirilmislardir.

Daha sonra, bu uc arastirmaci agent'i es zamanli olarak calistirmak icin ParallelWebResearchAgent adli bir ParallelAgent olusturulur. Bu, arastirmanin paralel olarak yurutulmesini saglar ve potansiyel olarak zaman tasarrufu saglar. ParallelAgent, tum alt agent'lari (arastirmacilar) islerini tamamlayip durumu doldurdugunda yurutumunu tamamlar.

Ardindan, arastirma sonuclarini sentezlemek icin bir MergerAgent (ayni zamanda bir LlmAgent) tanimlanir. Bu agent, paralel arastirmacilar tarafindan oturum durumunda depolanan ozetleri girdi olarak alir. Talimati, ciktinin yalnizca saglanan girdi ozetlerine dayali olmasi gerektigini vurgular ve harici bilgi eklemeyi yasaklar. MergerAgent, birlestirilen bulgulari her konu icin basliklar ve kisa bir genel sonuc iceren bir rapora yapilandirmak icin tasarlanmistir.

Son olarak, tum is akisini yonetmek icin ResearchAndSynthesisPipeline adli bir SequentialAgent olusturulur. Birincil kontrolor olarak bu ana agent, once arastirmayi gerceklestirmek icin ParallelAgent'i yurutur. ParallelAgent tamamlandiginda, SequentialAgent toplanan bilgileri sentezlemek icin MergerAgent'i yurutur. `sequential_pipeline_agent`, bu multi-agent sistemini calistirmak icin giris noktasini temsil eden `root_agent` olarak ayarlanir. Genel surec, birden fazla kaynaktan paralel olarak verimli bir sekilde bilgi toplamak ve ardindan bunu tek, yapilandirilmis bir raporda birlestirmek icin tasarlanmistir.

## Bir Bakista

**Ne:** Bircok agentic is akisi, nihai bir hedefe ulasmak icin tamamlanmasi gereken birden fazla alt gorev icerir. Her gorevin bir oncekinin bitmesini bekledigi tamamen sirali bir yurutme genellikle verimsiz ve yavasir. Bu gecikme, farkli API'leri cagirmak veya birden fazla veritabanini sorgulamak gibi harici G/C islemlerine bagli gorevlerde onemli bir darbogazz haline gelir. Es zamanli yurutme icin bir mekanizma olmadan, toplam isleme suresi tum bireysel gorev surelerinin toplamidir ve sistemin genel performansini ve yanit verebilirligini engeller.

**Neden:** Paralelizasyon kalibi, bagimsiz gorevlerin es zamanli yurutulmesini saglayarak standart bir cozum sunar. Bir is akisinin, arac kullanimlari veya LLM cagirilari gibi birbirlerinin anlik ciktilarina bagli olmayan bilesenlerini belirleyerek calisir. LangChain ve Google ADK gibi agentic cerceveler, bu es zamanli islemleri tanimlamak ve yonetmek icin yerlesik yapilar saglar. Ornegin, bir ana surec paralel olarak calisan birden fazla alt gorevi cagirabilir ve tumu tamamlanana kadar bekleyebilir, ardindan sonraki adima gecebilir. Bu bagimsiz gorevleri birbiri ardina degil ayni anda calistirarak, bu kalip toplam yurutme suresini onemli olcude azaltir.

**Temel kural:** Bu kalibi, bir is akisi birden fazla API'den veri getirme, farkli veri parcalarini isleme veya sonraki sentez icin birden fazla icerik parcasi olusturma gibi es zamanli olarak calistirilabilecek birden fazla bagimsiz islem icerdiginde kullanin.

**Gorsel ozet:**

![Parallelization Design Pattern](../assets/Parallelization_Design_Pattern.png)

Sekil 2: Paralelizasyon tasarim kalibi

## Temel Cikarimlar

Iste temel cikarimlar:

* Paralelizasyon, verimliligini artirmak icin bagimsiz gorevleri es zamanli olarak yurutmeye yonelik bir kaliptir.
* Ozellikle gorevlerin API cagirilari gibi harici kaynaklari beklemeyi icerdigi durumlarda faydalidir.
* Es zamanli veya paralel bir mimarinin benimsenmesi, tasarim, hata ayiklama ve sistem gunluguleme gibi temel gelistirme asamalarini etkileyen onemli karmasiklik ve maliyet getirir.
* LangChain ve Google ADK gibi cerceveler, paralel yurutmeyi tanimlamak ve yonetmek icin yerlesik destek saglar.
* LangChain Expression Language (LCEL) icerisinde RunnableParallel, birden fazla calistirilabiliri yan yana calistirmak icin temel bir yapidir.
* Google ADK, bir Coordinator agent'inin LLM'sinin bagimsiz alt gorevleri belirledigi ve bunlarin ozelesmis alt agent'lar tarafindan es zamanli olarak islenmesini tetikledigi LLM Tabanli Yetkilendirme araciligiyla paralel yurutmeyi kolaylastirabilir.
* Paralelizasyon, genel gecikmeyi azaltmaya yardimci olur ve agentic sistemleri karmasik gorevler icin daha duyarli hale getirir.

## Sonuc

Paralelizasyon kalibi, bagimsiz alt gorevleri es zamanli olarak yuruterek hesaplama is akislarini optimize etme yontemidir. Bu yaklasim, ozellikle birden fazla model cikarimi veya harici hizmetlere cagri iceren karmasik islemlerde genel gecikmeyi azaltir.

Cerceveler, bu kalibi uygulamak icin farkli mekanizmalar saglar. LangChain'de, birden fazla isleme zincirini es zamanli olarak acikca tanimlamak ve yurutmek icin RunnableParallel gibi yapilar kullanilir. Buna karsilik, Google Agent Developer Kit (ADK) gibi cerceveler, birincil bir koordinator modelin farkli alt gorevleri es zamanli olarak calısabilecek ozelesmis agent'lara atadigi multi-agent yetkilendirme yoluyla paralelizasyon elde edebilir.

Paralel islemeyi sirali (zincirleme) ve kosullu (yonlendirme) kontrol akislariyla entegre ederek, cesitli ve karmasik gorevleri verimli bir sekilde yonetebilen gelismis, yuksek performansli hesaplama sistemleri olusturmak mumkun hale gelir.

## Kaynaklar

Paralelizasyon kalibi ve ilgili kavramlar hakkinda daha fazla okuma icin bazi kaynaklar:

1. LangChain Expression Language (LCEL) Documentation (Parallelism): [https://python.langchain.com/docs/concepts/lcel/](https://python.langchain.com/docs/concepts/lcel/)
2. Google Agent Developer Kit (ADK) Documentation (Multi-Agent Systems): [https://google.github.io/adk-docs/agents/multi-agents/](https://google.github.io/adk-docs/agents/multi-agents/)
3. Python `asyncio` Documentation: [https://docs.python.org/3/library/asyncio.html](https://docs.python.org/3/library/asyncio.html)
