# Bolum 7: Coklu Agent Is Birligi (Multi-Agent Collaboration)

Monolitik bir agent mimarisi, iyi tanimlanmis problemler icin etkili olabilse de, karmasik, cok alanli gorevlerle karsilastiginda yetenekleri genellikle kisitlidir. Coklu Agent Is Birligi kalibi, bir sistemi farkli, ozelesmis agent'larin isbirlikci bir toplulugu olarak yapilandirarak bu sinirliliklari giderir. Bu yaklasim, ust duzey bir hedefin ayrik alt problemlere ayristirildigi gorev dekompozisyonu ilkesine dayanir. Her alt problem daha sonra, o gorev icin en uygun belirli araclara, veri erisimiune veya akil yurutme yeteneklerine sahip bir agent'a atanir.

Ornegin, karmasik bir arastirma sorgusu ayristilabilir ve bilgi erisimi icin bir Arastirma Agent'ina, istatistiksel isleme icin bir Veri Analiz Agent'ina ve nihai raporu olusturmak icin bir Sentez Agent'ina atanabilir. Boyle bir sistemin etkinligi yalnizca is bolumunden degil, agent'lar arasi iletisim (Communication) mekanizmalarindan kritik olarak baglidir. Bu, agent'larin veri alisverisi yapmasina, alt gorevler devretmesine ve nihai ciktinin tutarli olmasini saglamak icin eylemlerini koordine etmesine olanak taniyan standartlasilmis bir iletisim protokolu ve paylasilan bir ontoloji gerektirir.

Bu dagitik mimari, gelistirilmis modulerlik, olceklenebilirlik ve saglamlik dahil olmak uzere cesitli avantajlar sunar; cunku tek bir agent'in basarisizligi mutlaka toplam sistem arizasina yol acmaz. Is birligi, coklu agent sisteminin kolektif performansinin topluluk icerisindeki herhangi bir bireysel agent'in potansiyel yeteneklerini asan sinerjik bir sonuc olusturmasina olanak tanir.

## Coklu Agent Is Birligi Kalibina Genel Bakis

Coklu Agent Is Birligi kalibi, birden fazla bagimsiz veya yari bagimsiz agent'in ortak bir hedefe ulasmak icin birlikte calistigi sistemler tasarlamayi icerir. Her agent tipik olarak tanimlanmis bir role, genel hedefle uyumlu belirli hedeflere ve potansiyel olarak farkli araclara veya bilgi tabanlarina erisime sahiptir. Bu kalibin gucu, bu agent'lar arasindaki etkilesim ve sinerjide yatar.

Is birligi cesitli bicimler alabilir:

* **Sirali Devir:** Bir agent bir gorevi tamamlar ve ciktisini bir pipeline'daki sonraki adim icin baska bir agent'a aktarir (Planlama kalibina benzer, ancak acikca farkli agent'lari icerir).
* **Paralel Isleme:** Birden fazla agent, bir problemin farkli bolumlerinde es zamanli olarak calisir ve sonuclari daha sonra birlestirilir.
* **Tartisma ve Uzlasma:** Cesitli bakis aciilarina ve bilgi kaynaklarina sahip Agent'larin secenekleri degerlendirmek icin tartismalara girdigi, sonuc olarak bir uzllasmaya veya daha bilgilendirilmis bir karara vardigi Coklu Agent Is Birligi.
* **Hiyerarsik Yapilar:** Bir yonetici agent, gorevleri arac erisimlerine veya eklenti yeteneklerine dayanarak calisan agent'lara dinamik olarak devredebilir ve sonuclarini sentezleyebilir. Her agent ayrica tek bir agent'in tum araclari ele almasi yerine ilgili arac gruplarini ele alabilir.
* **Uzman Takimlar:** Farkli alanlarda (ornegin bir arastirmaci, bir yazar, bir editor) ozelesmis bilgiye sahip Agent'lar, karmasik bir cikti uretmek icin is birligi yapar.
* **Elestirmen-Gozden Geciren:** Agent'lar planlar, taslaklar veya yanitlar gibi ilk ciktilar olusturur. Ikinci bir agent grubu daha sonra bu ciktiyi politikalara uyum, guvenlik, uyumluluk, dogruluk, kalite ve organizasyonel hedeflerle uyum acisindan elesttirel olarak degerlendirir. Orijinal olusturucu veya nihai bir agent, bu geri bildirime dayanarak ciktiyi revize eder. Bu kalip ozellikle kod olusturma, arastirma yazimi, mantik kontrolu ve etik uyumun saglanmasi icin etkilidir. Bu yaklasmiin avantajlari arasinda artan saglamlik, gelistirilmis kalite ve hallucination veya hata olasiliginin azalmasi bulunur.

Bir multi-agent sistemi (bkz. Sekil 1) temel olarak agent rollerinin ve sorumluluklarinin belirlenmesini, agent'larin bilgi alisverisi yaptigi iletisim kanallarinin olusturulmasini ve isbirlikci cabalarini yonlendiren bir gorev akisi veya etkilesim protokolunun formule edilmesini kapsar.

![Multi-Agent System](../assets/Multi_Agent_System.png)

Sekil 1: Multi-agent sistemi ornegi

Crew AI ve Google ADK gibi cerceveler, agent'larin, gorevlerin ve etkilesim prosedurlerinin belirtilmesi icin yapilar saglayarak bu paradigmayi kolaylastirmak uzere tasarlanmistir. Bu yaklasim, cesitli ozelesmis bilgi gerektiren, birden fazla ayrik asama iceren veya es zamanli isleme ve agent'lar arasi bilgi dogrulamasindn yararlanan zorluiklar icin ozellikle etkilidir.

## Pratik Uygulamalar ve Kullanim Alanlari

Coklu Agent Is Birligi, cok sayida alanda uygulanabilir guclu bir kaliptir:

* **Karmasik Arastirma ve Analiz:** Bir agent takimi bir arastirma projesinde is birligi yapabilir. Bir agent akademik veritabanlarinda aramada, digeri bulgulari ozetlemede, ucuncusu trendleri belirlemede ve dorduncusu bilgileri bir raporda sentezlemede uzmanlasiabilir. Bu, bir insan arastirma takiminin nasil calisabilecegini yansitir.
* **Yazilim Gelistirme:** Agent'larin yazilim olusturmada is birligi yaptigini hayal edin. Bir agent gereksinim analisti, digeri kod ureticisi, ucuncusu testci ve dorduncusu dokumantasyon yazari olabilir. Bilesenleri olusturmak ve dogrulamak icin ciktilari birbirlerine aktarabilirler.
* **Yaratici Icerik Olusturma:** Pazarlama kampanyasi olusturmak bir pazar arastirma agent'i, metin yazari agent'i, grafik tasarim agent'i (gorsel olusturma araclari kullanan) ve sosyal medya planlama agent'ini icerebilir ve hepsi birlikte calisir.
* **Finansal Analiz:** Bir multi-agent sistemi finansal piyasalari analiz edebilir. Agent'lar borsa verilerini getirme, haber duyarlilik analizi, teknik analiz yapma ve yatirim onerileri olusturma konularinda uzmanlaabilir.
* **Musteri Destek Eskalasyonu:** On saf destek agent'i ilk sorglari ele alabilir, gerektiginde karmasik sorunlari bir uzman agent'a (ornegin teknik uzman veya faturalama uzmani) eskalasyoon yapabilir; problem karmasikligina dayali sirali devri gosterir.
* **Tedarik Zinciri Optimizasyonu:** Agent'lar bir tedarik zincirindeki farkli dugumleri (tedarikcciler, ureticiler, dagitimcilar) temsil edebilir ve degisen talep veya aksakliklara yanit olarak envanter seviyeleri, lojistik ve zamanlamayi optimize etmek icin is birligi yapabilir.
* **Ag Analizi ve Onarimi:** Otonom operasyonlar, ozellikle ariza tespitinde agentic bir mimariden buyuk olcude faydalanir. Birden fazla agent, sorunlari triajlamak ve gidermek, optimal eylemleri onermek icin is birligi yapabilir. Bu agent'lar ayrica geleneksel makine ogrenmesi modelleri ve araclariyla entegre olabilir, mevcut sistemlerden yararlanirken ayni zamanda Generative AI'nin avantajlarini sunabilir.

Ozelesmis agent'lari belirleme ve karsilikli iliskilerini titizlikle orkestre etme kapasitesi, gelistiricilerin gelistirilmis modulerlik, olceklenebilirlik ve tekil, entegre bir agent icin asilmaz olacak karmasikliklari ele alma yetenegii sergileyen sistemler olusturmasini guclendirir.

## Coklu Agent Is Birligi: Karsilikli Iliskileri ve Iletisim Yapilarini Kesfetme

Agent'larin etkilesim ve iletisim yollarini anlamak, etkili multi-agent sistemleri tasarlamak icin temeldir. Sekil 2'de gosterildigi gibi, en basit tek agent senaryosundan karmasik, ozel tasarlanmis isbirlikci cercevelere uzanan bir karsilikli iliski ve iletisim modeli yelpazesi mevcuttur. Her model, benzersiz avantajlar ve zorluklar sunar ve multi-agent sisteminin genel verimlilligini, saglamligini ve uyarlanabilirligini etkiler.

### 1. Tek Agent

En temel duzeyde, bir "Tek Agent" diger varliklarla dogrudan etkilesim veya iletisim olmadan otonom olarak calisir. Bu model uygulamasi ve yonetimi basit olsa da, yetenekleri dogasi geregi bireysel agent'in kapsami ve kaynaklariyla sinirlidir. Her biri tek, kendine yeterli bir agent tarafindan cozulebilen bagimsiz alt problemlere ayristrilabilir gorevler icin uygundur.

### 2. Ag

"Ag" modeli, birden fazla agent'in merkeziyetsiz bir sekilde dogrudan birbirleriyle etkilesime girdigi, is birligine dogru onemli bir adimi temsil eder. Iletisim tipik olarak esler arasi (peer-to-peer) gerceklesir ve bilgi, kaynak ve hatta gorev paylasiimina olanak tanir. Bu model direnci tesvik eder, cunku bir agent'in basarisizligi mutlaka tum sistemi sakatlamaz. Ancak, buyuk, yapilandirilmamis bir agda iletisim yuukunu yonetmek ve tutarli karar vermeyi saglamak zorlayici olabilir.

### 3. Supervizor

"Supervizor" modelinde, ozel bir agent olan "supervizor", bir grup alt agent'in faaliyetlerini denetler ve koordine eder. Supervizor, iletisim, gorev tahsisi ve catisma cozumu icin merkezi bir duyum gorevi gorur. Bu hiyerarsik yapi, net yetki hatlari sunar ve yonetim ile kontrolu basitlestirebilir. Ancak, tek bir ariza noktasi (supervizor) getirir ve supervizor cok sayida ast veya karmasik gorevlerle bunaldığında bir darboğaz haline gelebilir.

### 4. Arac Olarak Supervizor

Bu model, "Supervizor" kavraminin nüansli bir uzantisidir; burada supervizorün rolu dogrudan komuta ve kontrolden cok diger agent'lara kaynaklar, rehberlik veya analitik destek saglamaktir. Supervizor, diger agent'larin gorevlerini daha etkili bir sekilde yerine getirmelerini saglayan araclar, veriler veya hesaplama hizmetleri sunabilir, ancak her eylemlerini mutlaka dikte etmez. Bu yaklasim, kati yukaaridan asagiya kontrol dayatmadan supervizorün yeteneklerinden yararlanmayi amaclar.

### 5. Hiyerarsik

"Hiyerarsik" model, cok katmanli bir organizasyonel yapi olusturmak icin supervizor kavramini genisletir. Bu, ust duzey supervisorlerin alt duzey olanlari denetledigi ve nihayetinde en alt katmanda operasyonel agent'lar toplulugunu iceren birden fazla supervizor duzeyi icerir. Bu yapi, her biri hiyerarsinin belirli bir katmani tarafindan yonetilen alt problemlere ayristrilabilir karmasik problemler icin uygundur. Olceklenebilirlik ve karmasiiklik yonetimine yapilandirilmis bir yaklasim saglar ve tanimlanmis sinirlar icerisinde dagitik karar vermeye olanak tanir.

![Agents Communicate and Interact in Various Ways](../assests/Agents_Communicate_and_Interact_in_Various_Ways.png)

Sekil 2: Agent'lar cesitli sekillerde iletisim kurar ve etkilesime girer.

### 6. Ozel

"Ozel" model, multi-agent sistem tasariminda nihai esnekligi temsil eder. Belirli bir problem veya uygulamanin gereksinimlerine tam olarak uyarlanmis benzersiz karsilikli iliski ve iletisim yapilarinin olusturulmasina olanak tanir. Bu, onceden bahsedilen modellerden unsurlari birlestiren hibrit yaklasimlari veya ortamin benzersiz kisitlamalari ve firsatlarindan ortaya cikan tamamen ozgun tasarimlari icerebilir. Ozel modeller genellikle belirli performans metrikleri icin optimizasyon yapma, son derece dinamik ortamlari ele alma veya alan spesifik bilgiyi sistemin mimarisine dahil etme ihtiyacindan doggar. Ozel modellerin tasarimi ve uygulanmasi tipik olarak multi-agent sistemleri ilkelerinin derin bir anlayisini ve iletisim protokolleri, koordinasyon mekanizmalari ve ortaya cikan davranislarin dikkatli bir sekilde degerlendirilmesini gerektirir.

Ozetle, bir multi-agent sistemi icin karsilikli iliski ve iletisim modelinin secimi kritik bir tasarim kararidir. Her model, farkli avantajlar ve dezavantajlar sunar ve optimal secim, gorevin karmasikligi, agent sayisi, istenen otonomi duzeyi, saglamlik ihtiyaci ve kabul edilebilir iletisim yuku gibi faktorlere baglidir. Multi-agent sistemlerindeki gelecekteki gelismeler, muhtemelen bu modelleri kesfetmeye ve iyilestirmeye devam edecek ve isbirlikci zeka icin yeni paradigmalar gelistirecektir.

## Uygulamali Kod (Crew AI)

Bu Python kodu, yapay zeka trendleri hakkinda bir blog yazisi olusturmak icin CrewAI cercevesini kullanan yapay zeka destekli bir crew tanimlar. Ortami kurarak, .env dosyasindan API anahtarlarini yukleyerek baslar. Uygulamanin cekirdegi iki agent tanimlmayi icerir: yapay zeka trendlerini bulmak ve ozetlemek icin bir arastirmaci ve arastirmaya dayanarak bir blog yazisi olusturmak icin bir yazar.

Buna gore iki gorev tanimlanir: biri trendleri arastirmak, digeri ise arastirma gorevinin ciktisina bagli olarak blog yazsini yazmak. Bu agent'lar ve gorevler daha sonra, gorevlerin sirayla yurutuldugu sirali bir surec belirterek bir Crew'da bir araya getirilir. Crew, agent'lar, gorevler ve bir dil modeli ("gemini-2.0-flash" modeli) ile baslatilir. Ana fonksiyon, istenen ciktiyi uretmek icin agent'lar arasindaki is birligini orkestre eden kickoff() yontemiyle bu crew'u yurutur. Son olarak, kod crew'un yurutumunun nihai sonucunu, yani olusturulan blog yazsini yazdirir.

```python
import os
from dotenv import load_dotenv
from crewai import Agent, Task, Crew, Process
from langchain_google_genai import ChatGoogleGenerativeAI


def setup_environment():
    """Loads environment variables and checks for the required API key."""
    load_dotenv()
    if not os.getenv("GOOGLE_API_KEY"):
        raise ValueError("GOOGLE_API_KEY not found. Please set it in your .env file.")


def main():
    """
    Initializes and runs the AI crew for content creation using the latest Gemini model.
    """
    setup_environment()

    # Define the language model to use.
    # Updated to a model from the Gemini 2.0 series for better performance and features.
    # For cutting-edge (preview) capabilities, you could use "gemini-2.5-flash".
    llm = ChatGoogleGenerativeAI(model="gemini-2.0-flash")

    # Define Agents with specific roles and goals
    researcher = Agent(
        role='Senior Research Analyst',
        goal='Find and summarize the latest trends in AI.',
        backstory="You are an experienced research analyst with a knack for identifying key trends and synthesizing information.",
        verbose=True,
        allow_delegation=False,
    )

    writer = Agent(
        role='Technical Content Writer',
        goal='Write a clear and engaging blog post based on research findings.',
        backstory="You are a skilled writer who can translate complex technical topics into accessible content.",
        verbose=True,
        allow_delegation=False,
    )

    # Define Tasks for the agents
    research_task = Task(
        description="Research the top 3 emerging trends in Artificial Intelligence in 2024-2025. Focus on practical applications and potential impact.",
        expected_output="A detailed summary of the top 3 AI trends, including key points and sources.",
        agent=researcher,
    )

    writing_task = Task(
        description="Write a 500-word blog post based on the research findings. The post should be engaging and easy for a general audience to understand.",
        expected_output="A complete 500-word blog post about the latest AI trends.",
        agent=writer,
        context=[research_task],
    )

    # Create the Crew
    blog_creation_crew = Crew(
        agents=[researcher, writer],
        tasks=[research_task, writing_task],
        process=Process.sequential,
        llm=llm,
        verbose=2,  # Set verbosity for detailed crew execution logs
    )

    # Execute the Crew
    print("## Running the blog creation crew with Gemini 2.0 Flash... ##")
    try:
        result = blog_creation_crew.kickoff()
        print("\n------------------\n")
        print("## Crew Final Output ##")
        print(result)
    except Exception as e:
        print(f"\nAn unexpected error occurred: {e}")


if __name__ == "__main__":
    main()
```

Simdi Google ADK cercevesi icerisindeki diger orneklere dalacagiz; ozellikle hiyerarsik, paralel ve sirali koordinasyon paradigmalarina ve bir agent'in operasyonel arac olarak uygulanmasina odaklanacagiz.

## Uygulamali Kod (Google ADK)

Asagidaki kod ornegi, bir ebeveyn-cocuk iliskisi olusturarak Google ADK icerisinde hiyerarsik bir agent yapisinin kurulmasini gosterir. Kod iki tur agent tanimlar: LlmAgent ve BaseAgent'tan turetilmis ozel bir TaskExecutor agent'i. TaskExecutor, LLM disii belirli gorevler icin tasarlanmistir ve bu ornekte yalnizca "Task finished successfully" olayi uretir. `greeter` adli bir LlmAgent, belirtilmis bir model ve dostane bir karsilayici olarak hareket etme talimatiyla baslatilir. Ozel TaskExecutor, `task_doer` olarak orneklenir. `coordinator` adli bir ebeveyn LlmAgent, ayrica bir model ve talimatlarla olusturulur. Koordinatorun talimatlari, selamlamalari greeter'a ve gorev yurutmeyi `task_doer`'a devretmesini yonlendirir. Greeter ve `task_doer`, koordinatore alt agent'lar olarak eklenerek bir ebeveyn-cocuk iliskisi kurulur. Kod daha sonra bu iliskinin dogru bir sekilde kuruldugunnu dogrular. Son olarak, agent hiyerarsisinin basariyla olusturulduguna dair bir mesaj yazdirir.

```python
from typing import AsyncGenerator

from google.adk.agents import LlmAgent, BaseAgent
from google.adk.agents.invocation_context import InvocationContext
from google.adk.events import Event


# Correctly implement a custom agent by extending BaseAgent
class TaskExecutor(BaseAgent):
    """A specialized agent with custom, non-LLM behavior."""
    name: str = "TaskExecutor"
    description: str = "Executes a predefined task."

    async def _run_async_impl(self, context: InvocationContext) -> AsyncGenerator[Event, None]:
        """Custom implementation logic for the task."""
        # This is where your custom logic would go.
        # For this example, we'll just yield a simple event.
        yield Event(author=self.name, content="Task finished successfully.")


# Define individual agents with proper initialization
# LlmAgent requires a model to be specified.
greeter = LlmAgent(
    name="Greeter",
    model="gemini-2.0-flash-exp",
    instruction="You are a friendly greeter.",
)

# Instantiate our concrete custom agent
task_doer = TaskExecutor()

# Create a parent agent and assign its sub-agents
# The parent agent's description and instructions should guide its delegation logic.
coordinator = LlmAgent(
    name="Coordinator",
    model="gemini-2.0-flash-exp",
    description="A coordinator that can greet users and execute tasks.",
    instruction="When asked to greet, delegate to the Greeter. When asked to perform a task, delegate to the TaskExecutor.",
    sub_agents=[
        greeter,
        task_doer,
    ],
)

# The ADK framework automatically establishes the parent-child relationships.
# These assertions will pass if checked after initialization.
assert greeter.parent_agent == coordinator
assert task_doer.parent_agent == coordinator

print("Agent hierarchy created successfully.")
```

Bu kod parcasi, yinelemeli is akislari olusturmak icin Google ADK cercevesi icerisinde LoopAgent'in kullanimini gostermektedir. Kod iki agent tanimlar: ConditionChecker ve ProcessingStep. ConditionChecker, oturum durumundaki bir "status" degerini kontrol eden ozel bir agent'tir. "status" "completed" ise, ConditionChecker donguyu durdurmak icin bir olay yukselttir. Aksi takdirde, donguye devam etmek icin bir olay uretir. `ProcessingStep`, "gemini-2.0-flash-exp" modelini kullanan bir LlmAgent'tir. Talimati, bir gorevi yerine getirmek ve son adimsa oturum `status`'unu "completed" olarak ayarlamaktir. StatusPoller adli bir LoopAgent olusturulur. StatusPoller, `max_iterations=10` ile yapilandirilmistir. StatusPoller, hem ProcessingStep hem de bir ConditionChecker ornegini alt agent'lar olarak icerir. LoopAgent, alt agent'lari 10 yinelemeye kadar sirali olarak yurutecek ve ConditionChecker statusun "completed" oldugunu buldugunda duracaktir.

```python
import asyncio
from typing import AsyncGenerator

from google.adk.agents import LoopAgent, LlmAgent, BaseAgent
from google.adk.events import Event, EventActions
from google.adk.agents.invocation_context import InvocationContext


# Best Practice: Define custom agents as complete, self-describing classes.
class ConditionChecker(BaseAgent):
    """A custom agent that checks for a 'completed' status in the session state."""
    name: str = "ConditionChecker"
    description: str = "Checks if a process is complete and signals the loop to stop."

    async def _run_async_impl(
        self, context: InvocationContext
    ) -> AsyncGenerator[Event, None]:
        """Checks state and yields an event to either continue or stop the loop."""
        status = context.session.state.get("status", "pending")
        is_done = status == "completed"

        if is_done:
            # Escalate to terminate the loop when the condition is met.
            yield Event(author=self.name, actions=EventActions(escalate=True))
        else:
            # Yield a simple event to continue the loop.
            yield Event(author=self.name, content="Condition not met, continuing loop.")


# Correction: The LlmAgent must have a model and clear instructions.
process_step = LlmAgent(
    name="ProcessingStep",
    model="gemini-2.0-flash-exp",
    instruction=(
        "You are a step in a longer process. Perform your task. "
        "If you are the final step, update session state by setting 'status' to 'completed'."
    ),
)


# The LoopAgent orchestrates the workflow.
poller = LoopAgent(
    name="StatusPoller",
    max_iterations=10,
    sub_agents=[
        process_step,
        ConditionChecker(),  # Instantiating the well-defined custom agent.
    ],
)

# This poller will now execute 'process_step'
# and then 'ConditionChecker' repeatedly until the status is 'completed'
# or 10 iterations have passed.
```

Bu kod parcasi, dogrusal is akislarinin olusturulması icin tasarlanmis Google ADK'daki SequentialAgent kalibini aciklar. Bu kod, google.adk.agents kutuphanesini kullanarak sirali bir agent pipeline'i tanimlar. Pipeline, step1 ve step2 olmak uzere iki agent'tan olusur. step1, `Step1_Fetch` olarak adlandirilir ve ciktisi oturum durumunda `data` anahtari altinda saklanir. step2, `Step2_Process` olarak adlandirilir ve `session.state["data"]` icerisinde saklanan bilgileri analiz edip bir ozet saglamasi talimati verilir. "MyPipeline" adli SequentialAgent, bu alt agent'larin yurutme sirasini orkestre eder. Pipeline baslangic girdisiyle calistirildiginda, oncelikle step1 yurutulur. step1'in yaniti "data" anahtari altinda oturum durumuna kaydedilir. Ardindan, step2, step1'in talimati uyarinca duruma yerlestiriligi bilgiyi kullanarak yurutulur. Bu yapi, bir agent'in ciktisinin bir sonraki icin girdi haline geldigi is akislari olusturmayi saglar. Bu, cok adimli yapay zeka veya veri isleme pipeline'lari olusturmada yaygin bir kaliptir.

```python
from google.adk.agents import SequentialAgent, Agent


# This agent's output will be saved to session.state["data"]
step1 = Agent(
    name="Step1_Fetch",
    output_key="data",
)

# This agent will use the data from the previous step.
# We instruct it on how to find and use this data.
step2 = Agent(
    name="Step2_Process",
    instruction="Analyze the information found in state['data'] and provide a summary.",
)

pipeline = SequentialAgent(
    name="MyPipeline",
    sub_agents=[step1, step2],
)

# When the pipeline is run with an initial input, Step1 will execute,
# its response will be stored in session.state["data"], and then
# Step2 will execute, using the information from the state as instructed.
```

Asagidaki kod ornegi, birden fazla agent gorevinin es zamanli yurutulmesini kolaylastiran Google ADK'daki ParallelAgent kalibini gostermektedir. `data_gatherer`, iki alt agent'i es zamanli olarak calistirmak icin tasarlanmistir: `weather_fetcher` ve `news_fetcher`. `weather_fetcher` agent'ina belirli bir konum icin hava durumunu almasi ve sonucu `session.state["weather_data"]` icerisinde depolamasi talimati verilir. Benzer sekilde, `news_fetcher` agent'ina belirli bir konu icin en onemli haberi almasi ve `session.state["news_data"]` icerisinde depolamasi talimati verilir. Her alt agent, "gemini-2.0-flash-exp" modelini kullanmak icin yapilandirilmistir. ParallelAgent, bu alt agent'larin yurutumunu orkestre eder ve paralel olarak calismaalarina olanak tanir. Hem `weather_fetcher` hem de `news_fetcher`'dan gelen sonuclar toplanir ve oturum durumunda saklanir. Son olarak, ornek agent'in yurutumu tamamlandiktan sonra `final_state`'ten toplanan hava durumu ve haber verilerine nasil erisilebilecegini gosterir.

```python
from google.adk.agents import Agent, ParallelAgent


# It's better to define the fetching logic as tools for the agents.
# For simplicity in this example, we'll embed the logic in the agent's instruction.
# In a real-world scenario, you would use tools.

# Define the individual agents that will run in parallel
weather_fetcher = Agent(
    name="weather_fetcher",
    model="gemini-2.0-flash-exp",
    instruction="Fetch the weather for the given location and return only the weather report.",
    output_key="weather_data",  # The result will be stored in session.state["weather_data"]
)

news_fetcher = Agent(
    name="news_fetcher",
    model="gemini-2.0-flash-exp",
    instruction="Fetch the top news story for the given topic and return only that story.",
    output_key="news_data",  # The result will be stored in session.state["news_data"]
)

# Create the ParallelAgent to orchestrate the sub-agents
data_gatherer = ParallelAgent(
    name="data_gatherer",
    sub_agents=[
        weather_fetcher,
        news_fetcher,
    ],
)
```

Saglanan kod segmenti, Google ADK icerisindeki "Arac Olarak Agent" paradigmasini ornekler; bir agent'in baska bir agent'in yeteneklerini fonksiyon cagirmasina benzer bir sekilde kullanmasina olanak tanir. Ozellikle, kod Google'in LlmAgent ve AgentTool siniflarini kullanan bir gorsel olusturma sistemi tanimlar. Iki agent'tan olusur: bir ebeveyn `artist_agent` ve bir alt agent `image_generator_agent`. `generate_image` fonksiyonu, gorsel olusturmayi simule eden basit bir aractir ve sahte gorsel verileri dondurur. `image_generator_agent`, aldigi bir metin prompt'una dayanarak bu araci kullanmaktan sorumludur. `artist_agent`'in rolu, oncelikle yaratici bir gorsel prompt'u icat etmektir. Ardindan, `image_generator_agent`'i bir AgentTool sarmalayicisi araciligiyla cagirir. AgentTool, bir agent'in baska bir agent'i arac olarak kullanmasina olanak taniyan bir kopru gorevi gorur. `artist_agent` `image_tool`'u cagirdiginda, AgentTool, `image_generator_agent`'i sanatcinin icat ettigi prompt ile cagirir. `image_generator_agent` daha sonra bu prompt ile `generate_image` fonksiyonunu kullanir. Son olarak, olusturulan gorsel (veya sahte veriler) agent'lar araciiligiyla yukari dogru geri dondurulur. Bu mimari, ust duzey bir agent'in bir gorevi gerceklestirmek icin alt duzey, ozelesmis bir agent'i orkestre ettigi katmanli bir agent sistemini gosterir.

```python
from google.adk.agents import LlmAgent
from google.adk.tools import agent_tool
from google.genai import types


# 1. A simple function tool for the core capability.
# This follows the best practice of separating actions from reasoning.
def generate_image(prompt: str) -> dict:
    """
    Generates an image based on a textual prompt.

    Args:
        prompt: A detailed description of the image to generate.

    Returns:
        A dictionary with the status and the generated image bytes.
    """
    print(f"TOOL: Generating image for prompt: '{prompt}'")
    # In a real implementation, this would call an image generation API.
    # For this example, we return mock image data.
    mock_image_bytes = b"mock_image_data_for_a_cat_wearing_a_hat"
    return {
        "status": "success",
        # The tool returns the raw bytes, the agent will handle the Part creation.
        "image_bytes": mock_image_bytes,
        "mime_type": "image/png",
    }


# 2. Refactor the ImageGeneratorAgent into an LlmAgent.
# It now correctly uses the input passed to it.
image_generator_agent = LlmAgent(
    name="ImageGen",
    model="gemini-2.0-flash",
    description="Generates an image based on a detailed text prompt.",
    instruction=(
        "You are an image generation specialist. Your task is to take the user's request "
        "and use the `generate_image` tool to create the image. "
        "The user's entire request should be used as the 'prompt' argument for the tool. "
        "After the tool returns the image bytes, you MUST output the image."
    ),
    tools=[generate_image],
)


# 3. Wrap the corrected agent in an AgentTool.
# The description here is what the parent agent sees.
image_tool = agent_tool.AgentTool(
    agent=image_generator_agent,
    description="Use this tool to generate an image. The input should be a descriptive prompt of the desired image.",
)


# 4. The parent agent remains unchanged. Its logic was correct.
artist_agent = LlmAgent(
    name="Artist",
    model="gemini-2.0-flash",
    instruction=(
        "You are a creative artist. First, invent a creative and descriptive prompt for an image. "
        "Then, use the `ImageGen` tool to generate the image using your prompt."
    ),
    tools=[image_tool],
)
```

## Bir Bakista

**Ne:** Karmasik problemler genellikle tek bir monolitik LLM tabanli agent'in yeteneklerini asar. Yalniz bir agent, cok yonlu bir gorevin tum bolumlerini ele almak icin gereken cesitli, ozelesmis becerilere veya belirli araclara erisimden yoksun olabilir. Bu sinirlilik bir darbogazz yaratir, sistemin genel etkinligini ve olceklenebilirligini azaltir. Sonuc olarak, gelismis, cok alanli hedeflerin ele alinmasi verimsiz hale gelir ve eksik veya optimal altinda sonuclara yol acabilir.

**Neden:** Coklu Agent Is Birligi kalibi, birden fazla, isbirligi yapan agent'tan olusan bir sistem olusturarak standart bir cozum sunar. Karmasik bir problem daha kucuk, daha yonetilebilir alt problemlere ayristirilir. Her alt problem, onu cozmek icin gereken hassas araclara ve yeteneklere sahip ozelesmis bir agent'a atanir. Bu agent'lar, sirali devirler, paralel is akislari veya hiyerarsik yetkilendirme gibi tanimlanmis iletisim protokolleri ve etkilesim modelleri araciligiyla birlikte calisir. Bu agentic, dagitik yaklasim, herhangi bir tek agent icin mumkun olmayacak sonuclar elde edilmesine olanak taniyan sinerjik bir etki yaratir.

**Temel kural:** Bu kalibi, bir gorev tek bir agent icin cok karmasik oldugunda ve ozelesmis beceriler veya araclar gerektiren farkli alt gorevlere ayristiriiabileceginde kullanin. Cesitli uzmanliktan, paralel islemden veya birden fazla asamali yapilandirilmis bir is akisindan yararlanan problemler icin, ornegin karmasik arastirma ve analiz, yazilim gelistirme veya yaratici icerik olusturma gibi idealdir.

**Gorsel ozet:**

![Multi-Agent Design Pattern](../assets/Multi_Agent_Design_Pattern.png)

Sekil 3: Multi-Agent tasarim kalibi

## Temel Cikarimlar

* Coklu agent is birligi, birden fazla agent'in ortak bir hedefe ulasmak icin birlikte calismasini icerir.
* Bu kalip, ozelesmis roller, dagitilmis gorevler ve agent'lar arasi iletisimden yararlanir.
* Is birligi, sirali devirler, paralel isleme, tartisma veya hiyerarsik yapilar gibi bicimler alabilir.
* Bu kalip, cesitli uzmanlik veya birden fazla farkli asama gerektiren karmasik problemler icin idealdir.

## Sonuc

Bu bolum, sistemler icerisinde birden fazla ozelesmis agent'i orkestre etmenin faydalarini gostererek Coklu Agent Is Birligi kalibini inceledi. Cesitli is birligi modellerini inceledik ve kalibin cesitli alanlardaki karmasik, cok yonlu problemlerin ele alinmasindaki temel rolunu vurguladik. Agent is birligini anlamak, dogal olarak onlarin dis ortamla etkilesimlerine dair bir sorusturmaya yol acar.

## Kaynaklar

1. Multi-Agent Collaboration Mechanisms: A Survey of LLMs, [https://arxiv.org/abs/2501.06322](https://arxiv.org/abs/2501.06322)
2. Multi-Agent System -- The Power of Collaboration, [https://aravindakumar.medium.com/introducing-multi-agent-frameworks-the-power-of-collaboration-e9db31bba1b6](https://aravindakumar.medium.com/introducing-multi-agent-frameworks-the-power-of-collaboration-e9db31bba1b6)
