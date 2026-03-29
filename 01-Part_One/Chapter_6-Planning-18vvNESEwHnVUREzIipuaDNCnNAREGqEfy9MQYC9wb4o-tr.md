# Bolum 6: Planlama (Planning)

Akilli davranis genellikle sadece anlik girdiye tepki vermekten daha fazlasini gerektirir. Ongoru, karmasik gorevleri daha kucuk, yonetilebilir adimlara bolme ve istenen bir sonuca nasil ulasiacagi konusunda strateji belirleme kapasitesini gerektirir. Planlama (Planning) kalibinin devreye girdigi nokta burasdir. Ozunde planlama, bir agent'in veya agent sisteminin baslangic durumundan bir hedef (Goal) durumuna dogru ilerlemek icin bir eylem dizisi formule etme yetenegidir.

## Planlama Kalibina Genel Bakis

Yapay zeka baglaminda, bir planlama agent'ini karmasik bir hedef devrettiginiz bir uzman olarak dusunmek yararlidir. "Bir takim etkinligi organize et" diye sordugunuzda, *ne*'yi -- hedefi ve kisitlamalarini -- tanimlamis olursunuz, ancak *nasil*'i degil. Agent'in temel gorevi, bu hedefe otonom olarak bir rota cizmektir. Oncelikle baslangic durumunu (ornegin butce, katilimci sayisi, istenen tarihler) ve hedef durumu (basariyla rezerve edilmis bir etkinlik) anlamali ve ardindan bunlari birbirine baglayan optimal eylem dizisini kesfetmelidir. Plan onceden bilinmez; istege yanit olarak olusturulur.

Bu surecin ayirt edici ozelligi uyarlanabilirliktir. Baslangic plani yalnizca bir baslangic noktasidir, kati bir senaryo degil. Agent'in gercek gucu, yeni bilgileri dahil etme ve projeyi engellerin etrafinda yonlendirme yetenegidir. Ornegin, tercih edilen mekan musait degilse veya secilen bir yemek hizmeti tamamen doluysa, yetenekli bir agent basitce basarisiz olmaz. Uyum saglar. Yeni kisitlamayi kaydeder, seceneklerini yeniden degerlendirir ve alternatif mekanlar veya tarihler onererek yeni bir plan formule eder.

Ancak, esneklik ve ongorebiilirlik arasindaki odurlestirmeyi tanimak onemlidir. Dinamik planlama belirli bir aractir, evrensel bir cozum degil. Bir problemin cozumu zaten iyi anlasilmis ve tekrarlanabilir oldugunda, agent'i onceden belirlenmmis, sabit bir is akisiyla sinirlandirmak daha etkilidir. Bu yaklasim, belirsizligi ve onceden kestirilemeyen davranis riskini azaltmak icin agent'in otonopisini sinirlar ve guvenilir ve tutarli bir sonuc garanti eder. Bu nedenle, bir planlama agent'i mi yoksa basit bir gorev yurutme agent'i mi kullanilacagi karari tek bir soruya baglidir: "nasil"in kesfedilmesi mi gerekiyor, yoksa zaten biliniyor mu?

## Pratik Uygulamalar ve Kullanim Alanlari

Planlama kalibi, otonom sistemlerde temel bir hesaplama surecidir ve bir agent'in belirli bir hedefe ulasmak icin bir eylem dizisi sentezlemesini saglar; ozellikle dinamik veya karmasik ortamlarda. Bu surec, ust duzey bir hedefi ayrik, yurutulebilir adimlardan olusan yapilandirilmis bir plana donusturur.

Prosedural gorev otomasyonu gibi alanlarda, planlama karmasik is akislarini orkestre etmek icin kullanilir. Ornegin, yeni bir calisanin ise alim sureci gibi bir is sureci, sistem hesaplari olusturma, egitim modulleri atama ve farkli departmanlarla koordinasyon gibi yonlendirilmis bir alt gorevler dizisine ayriitirilabilir. Agent, bu adimlari mantiksal bir sirada yurutmek icin bir plan olusturur ve bagimliliklari yonetmek icin gerekli araclari cagirir veya cesitli sistemlerle etkilesime girer.

Robotik ve otonom navigasyon alaninda, planlama durum-uzayi gecisi icin temeldir. Fiziksel bir robot veya sanal bir varlik olsun, bir sistem baslangic durumundan hedef durumuna gecis icin bir yol veya eylem dizisi olusturmak zorundadir. Bu, engel kacinma veya trafik kurallarina uyma gibi cevre kisitlamalarina uyarak zaman veya enerji tuketimi gibi metrikler icin optimizasyon yapmayi icerir.

Bu kalip, yapilandirilmis bilgi sentezi icin de kritiktir. Arastirma raporu gibi karmasik bir cikti olusturmakla gorevlendirildiginde, bir agent bilgi toplama, veri ozetleme, icerik yapilandirma ve yinelemeli iyilestirme icin farkli asamalar iceren bir plan formule edebilir. Benzer sekilde, cok adimli problem cozumu iceren musteri destek senaryolarinda, bir agent teshis, cozum uygulama ve eskalasyon icin sistematik bir plan olusturabilir ve izleyebilir.

Ozunde, Planlama kalibi bir agent'in basit, reaktif eylemlerin otesine gecerek hedefe yonelik davranisa gecmesine olanak tanir. Birbirine bagli operasyonlarin tutarli bir dizisini gerektiren problemleri cozmek icin gerekli mantiksal cercveyi saglar.

## Uygulamali Kod (Crew AI)

Asagidaki bolum, Crew AI cercevesi kullanilarak Planlama kalibinin bir uygulamasini gosterecektir. Bu kalip, oncelikle karmasik bir sorguyu ele almak icin cok adimli bir plan formule eden ve ardindan bu plani sirali olarak yurutulen bir agent'i icerir.

```python
import os
from dotenv import load_dotenv
from crewai import Agent, Task, Crew, Process
from langchain_openai import ChatOpenAI


# Load environment variables from .env file for security
load_dotenv()


# 1. Explicitly define the language model for clarity
llm = ChatOpenAI(model="gpt-4-turbo")


# 2. Define a clear and focused agent
planner_writer_agent = Agent(
    role='Article Planner and Writer',
    goal='Plan and then write a concise, engaging summary on a specified topic.',
    backstory=(
        'You are an expert technical writer and content strategist. '
        'Your strength lies in creating a clear, actionable plan before writing, '
        'ensuring the final summary is both informative and easy to digest.'
    ),
    verbose=True,
    allow_delegation=False,
    llm=llm,  # Assign the specific LLM to the agent
)


# 3. Define a task with a more structured and specific expected output
topic = "The importance of Reinforcement Learning in AI"

high_level_task = Task(
    description=(
        f"1. Create a bullet-point plan for a summary on the topic: '{topic}'.\n"
        f"2. Write the summary based on your plan, keeping it around 200 words."
    ),
    expected_output=(
        "A final report containing two distinct sections:\n\n"
        "### Plan\n"
        "- A bulleted list outlining the main points of the summary.\n\n"
        "### Summary\n"
        "- A concise and well-structured summary of the topic."
    ),
    agent=planner_writer_agent,
)


# Create the crew with a clear process
crew = Crew(
    agents=[planner_writer_agent],
    tasks=[high_level_task],
    process=Process.sequential,
)


# Execute the task
print("## Running the planning and writing task ##")
result = crew.kickoff()

print("\n\n---\n## Task Result ##\n---")
print(result)
```

Bu kod, belirli bir konuda bir ozet planlamak ve yazmak icin bir yapay zeka agent'i olusturmak icin CrewAI kutuphanesini kullanir. Gerekli kutuphaneleri, Crew.ai ve `langchain_openai` dahil olmak uzere iceri aktararak ve .env dosyasindan ortam degiskenlerini yukleyerek baslar. Agent ile kullanim icin bir ChatOpenAI dil modeli acikca tanimlanir. Belirli bir rol ve hedefe sahip `planner_writer_agent` adli bir Agent olusturulur: kisa ve ozlu bir ozet planlamak ve ardindan yazmak. Agent'in arka plani, planlama ve teknik yazma konusundaki uzmanligini vurgular. Beklenen cikti icin belirli bir formatla, once bir plan olusturmak, ardindan "The importance of Reinforcement Learning in AI" konusunda bir ozet yazmak icin net bir aciklamaya sahip bir Gorev tanimlanir. Bir Crew, agent ve gorevle birlikte, bunlari sirali olarak islemek uzere olusturulur. Son olarak, crew.kickoff() yontemi tanimli gorevi yurutmek icin cagrilir ve sonuc yazdirilir.

## Google DeepResearch

Google Gemini DeepResearch (bkz. Sekil 1), otonom bilgi erisimi ve sentezi icin tasarlanmis agent tabanli bir sistemdir. Karmasik konulari sistematik olarak kesfetmek icin Google Search'u dinamik ve yinelemeli olarak sorgulayan cok adimli bir agentic pipeline araciligiyla isler. Sistem, genis bir web tabanli kaynak kumelini islemek, toplanan verileri alaka duzeyii ve bilgi boslluklari acisindan degerlendirmek ve bunlari gidermek icin sonraki aramalari gerceklestirmek uzere tasarlanmistir. Nihai cikti, dogrulanmis bilgileri, orijinal kaynaklara atiflarla yapilandirilmis, cok sayfali bir ozette birlestirir.

Bunu genisleterek, sistemin islemi tek bir sorgu-yanit olayi degil, yonetilen, uzun sureli bir surecdir. Kullanicinin prompt'unu cok noktali bir arastirma planina ayristirarak baslar (bkz. Sekil 1) ve bu plan, inceleme ve degistirme icin kullaniciya sunulur. Bu, yurutmeden once arastirma yoneliminin isbirlikci bir sekilde sekillendirilmesine olanak tanir. Plan onaylandiginda, agentic pipeline yinelemeli arama-ve-analiz donguusunu baslatir. Bu, yalnizca onceden tanimlanmis bir dizi aramayi yurutmekten ibaret degildir; agent, topladigi bilgilere dayanarak sorgularini dinamik olarak formule eder ve rafine eder, aktif olarak bilgi bosluklarini belirler, veri noktalarini dogrular ve tutarsizliklari giderir.

![Google Deep Research agent generating an execution plan for using Google Search as a tool](../assets/Google_Deep_Research_Agent_Generating_an_execution_plan_for_using_Google_Search_as_a_Tool.png)

Sekil 1: Google Deep Research agent'i, Google Search'u arac olarak kullanmak icin bir yurutme plani olusturuyor.

Temel bir mimari bilesen, sistemin bu sureci asenkron olarak yonetme yetenegidir. Bu tasarim, yuuzlerce kaynagin analizini icerebilen sorusturmanin tek noktali arizalara karsi direncli olmasini ve kullanicinin sureci terk edip tamamlandiginda bildirim almasini saglar. Sistem ayrica kullanici tarafindan saglanan dokumanlari entegre ederek, ozel kaynaklardan gelen bilgileri web tabanli arastirmasiyla birlestirebilir. Nihai cikti, yalnizca bulgularin birlesmis bir listesi degil, yapilandirilmis, cok sayfali bir rapordur. Sentez asamasinda, model toplanan bilgilerin kritik bir degerlendirmesini yapar, ana temalari belirler ve icerigi mantiksal bolumlere sahip tutarli bir anlatiya doner. Rapor, genellikle bir ses ozeti, grafikler ve alintilanan orijinal kaynaklara baglantilar gibi ozellikler icererek etkilesimli olacak sekilde tasarlanmistir ve kullanici tarafindan dogrulama ve daha fazla kesetme saglar. Sentezlenmis sonuclara ek olarak, model arastirdigi ve danistigi kaynaklarin tam listesini acikca dondurur (bkz. Sekil 2). Bunlar atiflar olarak sunulur ve birincil bilgiye tam seffaflik ve dogrudan erisim saglar. Bu tum surec, basit bir sorguyu kapsamli, sentezlenmis bir bilgi kumeesine donusturur.

![An example of Deep Research plan being executed, resulting in Google Search being used as a tool to search various web sources](../assets/Example_of_Deep_Research_Plan_Being_Executed_Resulting_in_Google_Search_being_used_as_a_Tool_to_Search_Various_Web_Sources.png)

Sekil 2: Deep Research planinin yurutulen bir ornegi, sonucunda Google Search cesitli web kaynaklarini aramak icin arac olarak kullanilir.

Manuel veri toplama ve sentez icin gereken onemli zaman ve kaynak yatirimini azaltarak, Gemini DeepResearch bilgi kesfii icin daha yapilandirilmis ve kapsamli bir yontem sunar. Sistemin degeri ozellikle cesitli alanlardaki karmasik, cok yonlu arastirma gorevlerinde belirgindir.

Ornegin, rekabet analizinde agent, pazar trendleri, rakip urun ozellikleri, cesitli cevrimici kaynaklardan kamuoyu duyarliligi ve pazarlama stratejileri hakkinda verileri sistematik olarak toplamak ve harmanlamak icin yonlendirilebilir. Bu otomatik surec, birden fazla rakibi manuel olarak takip etmenin zahmetli gorevinin yerini alir ve analistlerin veri toplamak yerine ust duzey stratejik yorumlamaya odaklanmasina olanak tanir (bkz. Sekil 3).

![Final output generated by the Google Deep Research agent, analyzing on our behalf sources obtained using Google Search as a tool](../assets/Final_Output_Generated_by_Google_Deep_Research_Agent_Analyzing_on_our_Behalf_Sources_Obtained_using_Google_Search_as_a_Tool.png)

Sekil 3: Google Deep Research agent'i tarafindan olusturulan nihai cikti, Google Search'u arac olarak kullanarak bizim adimiza elde edilen kaynaklari analiz eder.

Benzer sekilde, akademik kesftte sistem kapsamli literatur taramalari yapmak icin guclu bir arac gorevi gorur. Temel makalleri belirleyip ozetleyebilir, belirli bir alan icerisindeki kavramlarin gelisimini cok sayida yayinda izleyebilir ve ortaya cikan arastirma cephelerini haritalaayabilir, boylece akademik arastirmanin baslangic ve en zaman alici asamasini hizlandirir.

Bu yaklasminin verimliligi, manuel arastirmadaki temel bir darbogazz olan yinelemeli arama-ve-filtreleme donguusunun otomasyonundan kaynaklanmaktadir. Kapsamlilik, sistemin karsilastiriailabilir bir zaman diliminde bir insan arasstirmacisi icin tipik olarak uygulanabilir olandan daha buyuk bir hacim ve cesitlilikte bilgi kaynaklarini isleme kapasitesiyle saglanir. Bu daha genis analiz kapsami, secim yanlililigini potansiyelini azaltmaya yardimci olur ve daha az belirgin ancak potansiyel olarak kritik bilgilerin ortaya cikma olasiligini artirir, bu da konunun daha saglam ve iyi desteklenmmis bir anlassimasina yol acar.

## OpenAI Deep Research API

OpenAI Deep Research API, karmasik arastirma gorevlerini otomatiklestirmek icin tasarlanmis ozel bir aractir. Gercek dunya kaynaklarindan bagimsiz olarak akil yurutebilen, plan yapabilen ve bilgi sentezleyebbilen gelismis, agentic bir model kullanir. Basit bir soru-cevap modelinden farkli olarak, ust duzey bir sorgu alir ve bunu otonom olarak alt sorulara ayirir, yerlesik aracllarini kullanarak web aramalari yapar ve yapilandirilmis, atif acsindan zengin bir nihai rapor sunar. API, yazim sirasinda yuksek kaliteli sentez icin o3-deep-research-2025-06-26 ve gecikmeye duyarli uygulamalar icin daha hizli o4-mini-deep-research-2025-06-26 gibi modelleri kulllanarak bu tum surece dogrudan programatik erisim saglar.

Deep Research API, aksi takdirde saatlerce surecek manuel arastirmayi otomatiklestirdigi icin faydalidir ve is stratejisi, yatirim kararlari veya politika onerileri bilgilendirmek icin uygun profesyonel duzeyde, veri odakli raporlar sunar. Temel faydalari sunlardir:

* **Yapilandirilmis, Atifli Cikti:** Kaynak meta verilerine bagli satirici atiflarla iyi organize edilmis raporlar uretir, iddialarin dogrulanabilir ve veri destekli olmasini saglar.
* **Seffaflik:** ChatGPT'deki soyutlanmis surecin aksine, API agent'in akil yurutmesi, yuruttugu belirli web arama sorgulari ve calistirdigi herhangi bir kod dahil olmak uzere tum ara adimlari acigar eder. Bu, ayrintili hata ayiklama, analiz ve nihai yanitin nasil olusturuldugunu daha derin anlama olanak tanir.
* **Genisletilebilirlik:** Model Context Protocol'u (MCP) destekler ve gelistiricilerin agent'i ozel bilgi tabanlarina ve dahili veri kaynaklarina baglamasina olanak tanir, kamu web arastirmasini tescilli bilgilerle harmanlar.

API'yi kullanmak icin, client.responses.create ucu noktasina bir model, bir girdi prompt'u ve agent'in kulllanabilecegi araclari belirten bir istek gonderirsiniz. Girdi, tipik olarak agent'in personasini ve istenen cikti formatini tanimlayan bir `system_message` ile `user_query`'yi icerir. `web_search_preview` aracini dahil etmeniz gerekir ve istege bagli olarak dahili veriler icin `code_interpreter` veya ozel MCP araclari (bkz. Bolum 10) ekleyebilirsiniz.

```python
from openai import OpenAI


# Initialize the client with your API key
client = OpenAI(api_key="YOUR_OPENAI_API_KEY")


# Define the agent's role and the user's research question
system_message = """
You are a professional researcher preparing a structured, data-driven report.
Focus on data-rich insights, use reliable sources, and include inline citations.
"""

user_query = "Research the economic impact of semaglutide on global healthcare systems."


# Create the Deep Research API call
response = client.responses.create(
    model="o3-deep-research-2025-06-26",
    input=[
        {
            "role": "developer",
            "content": [{"type": "input_text", "text": system_message}],
        },
        {
            "role": "user",
            "content": [{"type": "input_text", "text": user_query}],
        },
    ],
    reasoning={"summary": "auto"},
    tools=[{"type": "web_search_preview"}],
)


# Access and print the final report from the response
final_report = response.output[-1].content[0].text
print(final_report)


# --- ACCESS INLINE CITATIONS AND METADATA ---
print("--- CITATIONS ---")
annotations = response.output[-1].content[0].annotations

if not annotations:
    print("No annotations found in the report.")
else:
    for i, citation in enumerate(annotations):
        # The text span the citation refers to
        cited_text = final_report[citation.start_index : citation.end_index]
        print(f"Citation {i + 1}:")
        print(f"  Cited Text: {cited_text}")
        print(f"  Title: {citation.title}")
        print(f"  URL: {citation.url}")
        print(f"  Location: chars {citation.start_index}–{citation.end_index}")

print("\n" + "=" * 50 + "\n")


# --- INSPECT INTERMEDIATE STEPS ---
print("--- INTERMEDIATE STEPS ---")

# 1. Reasoning Steps: Internal plans and summaries generated by the model.
try:
    reasoning_step = next(item for item in response.output if item.type == "reasoning")
    print("\n[Found a Reasoning Step]")
    for summary_part in reasoning_step.summary:
        print(f"  - {summary_part.text}")
except StopIteration:
    print("\nNo reasoning steps found.")

# 2. Web Search Calls: The exact search queries the agent executed.
try:
    search_step = next(item for item in response.output if item.type == "web_search_call")
    print("\n[Found a Web Search Call]")
    print(f"  Query Executed: '{search_step.action['query']}'")
    print(f"  Status: {search_step.status}")
except StopIteration:
    print("\nNo web search steps found.")

# 3. Code Execution: Any code run by the agent using the code interpreter.
try:
    code_step = next(item for item in response.output if item.type == "code_interpreter_call")
    print("\n[Found a Code Execution Step]")
    print("  Code Input:")
    print(f"  ```python\n{code_step.input}\n  ```")
    print("  Code Output:")
    print(f"  {code_step.output}")
except StopIteration:
    print("\nNo code execution steps found.")
```

Bu kod parcasi, "Deep Research" gorevi gerceklestirmek icin OpenAI API'sini kullanir. Kimlik dogrulama icin kritik olan API anahtarinizla OpenAI istemcisini baslatarak baslar. Ardindan, yapay zeka agent'inin rolunu profesyonel bir arastirmaci olarak tanimlar ve semaglutid'in ekonomik etkisi hakkinda kullanicinin arastirma sorusunu belirler. Kod, tanimlanan sistem mesajini ve kullanici sorgusunu girdi olarak saglayarak o3-deep-research-2025-06-26 modeline bir API cagrisi olusturur. Ayrica akil yurutmenin otomatik bir ozetini ister ve web arama yeteneklerini etkinlestirir. API cagrisini yaptiktan sonra, nihai olusturulan raporu cikarir ve yazdirir.

Ardindan, alinttilanan metin, baslik, URL ve rapor icindeki konum dahil olmak uzere raporun anotasyonlarindan satirici atiflara ve meta verilere erismmeyi ve goruntulemeyi dener. Son olarak, modelin attigi ara adimlari, akil yurutme adimlari, web arama cagirilari (yurutulen sorgu dahil) ve bir kod yorumlayicisi kullaniildiysa herhangi bir kod yurutme adimi gibi ayrintilari inceler ve yazdirir.

## Bir Bakista

**Ne:** Karmasik problemler genellikle tek bir eylemle cozulemez ve istenen bir sonuca ulasmak icin ongoru gerektirir. Yapilandirilmis bir yaklasim olmadan, bir agentic sistem birden fazla adim ve bagimliliik iceren cok yonlu istekleri ele almakta zorlanir. Bu, ust duzey hedefleri yonetilebilir bir dizi daha kucuk, yurutulebilir goreve ayirmayi zorlastirir. Sonuc olarak, sistem etkili bir sekilde strateji belirleyemez ve karmasik hedeflerle karsilastiginda eksik veya yanlis sonuclara yol acar.

**Neden:** Planlama kalibi, bir agentic sistemin once bir hedefe yonelik tutarli bir plan olusturmasini saglayarak standart bir cozum sunar. Ust duzey bir hedefin daha kucuk, eyleme donusturullebilir adimlar veya alt hedefler dizisine ayristirilmasini icerir. Bu, sistemin karmasik is akislarini yonetmesine, cesitli araclari orkestre etmesine ve bagimlilikklari mantiksal bir sirada ele almasina olanak tanir. LLM'ler, genis egitim verilerine dayanarak makul ve etkili planlar olusturabailecekleri icin buna ozellikle uygundur. Bu yapilandirilmis yaklasim, basit bir reaktif agent'i karmasik bir hedefe dogru proaktif olarak calisabilen ve gerekirse planini uyarlayabilen stratejik bir yurutucuye donusturur.

**Temel kural:** Bu kalibi, bir kullanicinin istegi tek bir eylem veya aracla ele alinamayacak kadar karmasik oldugunda kullanin. Ayrintili bir arastirma raporu olusturma, yeni bir calisani ise alma veya rekabet analizi yapma gibi cok adimli surecleri otomatiklestirmek icin idealdir. Planlama kalibini, bir gorevin nihai, sentezlenmis bir sonuca ulasmak icin birbirine bagli operasyonlar dizisi gerektirdigi her durumda uygulayin.

**Gorsel ozet**

![Planning Design Pattern](../assets/Planning_Design_Pattern.png)

Sekil 4: Planlama tasarim kalibi

## Temel Cikarimlar

* Planlama, agent'larin karmasik hedefleri eyleme donusturullebilir, sirali adimlara ayirmasini saglar.
* Cok adimli gorevleri ele almak, is akisi otomasyonu ve karmasik ortamlarda gezinmek icin gereklidir.
* LLM'ler, gorev aciklamalarina dayanarak adim adim yaklasimlar olusturarak planlama yapabilir.
* Acikca planlama adimlari gerektiren prompt'lama veya gorevler tasarlama, agent cercevelerinde bu davranisi tesvik eder.
* Google Deep Research, Google Search'u arac olarak kullanarak bizim adimiza kaynaklari analiz eden bir agent'tir. Yansitir, planlar ve yurutur.

## Sonuc

Sonuc olarak, Planlama kalibi agentic sistemleri basit reaktif yanitlayicilardan stratejik, hedefe yonelik yurutculere yUkselten temel bir billesendir. Modern buyuk dil modelleri, ust duzey hedefleri tutarli, eyleme donusturulebilir adimlara otonom olarak ayristirarak bunun icin temel yetenegi saglar. Bu kalip, CrewAI agent'inin bir yazma plani olusturup izlemesinde gosterildigi gibi basit, sirali gorev yurutmeden daha karmasik ve dinamik sistemlere olceklenir. Google DeepResearch agent'i, surekli bilgi toplamaaya dayanarak uyarlanan ve gelisen yinelemeli arastirma planlari olusturarak bu gelismis uygulamayi ornekler. Sonuc olarak planlama, karmasik problemler icin insan niyeti ile otomatik yurutme arasinda temel kopruyu saglar. Bir problem cozme yaklasimini yapilandirarak, bu kalip agent'larin karmasik is akislarini yonetmesini ve kapsamli, sentezlenmis sonuclar sunmasini mumkun kilar.

## Kaynaklar

1. Google DeepResearch (Gemini Feature): [gemini.google.com](http://gemini.google.com)
2. OpenAI, Introducing deep research  [https://openai.com/index/introducing-deep-research/](https://openai.com/index/introducing-deep-research/)
3. Perplexity, Introducing Perplexity Deep Research, [https://www.perplexity.ai/hub/blog/introducing-perplexity-deep-research](https://www.perplexity.ai/hub/blog/introducing-perplexity-deep-research)
