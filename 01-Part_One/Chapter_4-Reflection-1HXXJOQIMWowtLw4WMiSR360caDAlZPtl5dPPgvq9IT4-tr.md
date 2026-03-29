# Bolum 4: Yansitma (Reflection)

## Yansitma Kalibina Genel Bakis

Onceki bolumlerde temel agentic kaliplari inceledik: sirali yurutme icin Zincirleme, dinamik yol secimi icin Yonlendirme (Routing) ve es zamanli gorev yurutme icin Paralelizasyon (Parallelization). Bu kalipler, agent'larin karmasik gorevleri daha verimli ve esnek bir sekilde gerceklestirmesini saglar. Ancak, gelismis is akislariyla bile, bir agent'in ilk ciktisi veya plani optimal, dogru veya eksiksiz olmayabilir. **Yansitma** kalibinin devreye girdigi nokta burasdir.

Yansitma kalibi, bir agent'in kendi calismasini, ciktisini veya dahili durumunu degerlendirmesini ve bu degerlendirmeyi performansini iyilestirmek veya yanitini rafine etmek icin kullanmasini icerir. Bu, agent'in geri bildirime, dahili elestiriye veya istenen kriterlere karsi karsilastirmaya dayanarak ciktisini yinelemeli olarak iyilestirmesine veya yaklasimini ayarlamasina olanak taniyan bir oz-duzeltme veya oz-iyilestirme bicimidir. Yansitma, zaman zaman gorevi ozellikle baslangic agent'inin ciktisini analiz etmek olan ayri bir agent tarafindan kolaylastiriabilir.

Ciktinin dogrudan sonraki adima aktarildigi basit bir sirali zincirden veya bir yol secen yonlendirmeden farkli olarak, yansitma bir geri bildirim dongusu getirir. Agent yalnizca bir cikti uretmekle kalmaz; ardindan bu ciktiyi (veya onu olusturan sureci) inceler, potansiyel sorunlari veya iyilestirme alanlarini belirler ve daha iyi bir surum olusturmak veya gelecekteki eylemlerini degistirmek icin bu icgoruleri kullanir.

Surec tipik olarak su adimlari icerir:

1. **Yurutme:** Agent bir gorev gerceklestirir veya ilk ciktiyi uretir.
2. **Degerlendirme/Elestiri:** Agent (genellikle baska bir LLM cagrisi veya kurallar kumesi kullanarak) onceki adimin sonucunu analiz eder. Bu degerlendirme, olgusal dogruluk, tutarlilik, stil, tamlilk, talimatlara uyum veya diger ilgili kriterleri kontrol edebilir.
3. **Yansitma/Iyilestirme:** Elestiriye dayanarak, agent nasil iyilestirme yapacagini belirler. Bu, rafine edilmis bir cikti olusturmayi, sonraki bir adim icin parametreleri ayarlamayi veya hatta genel plani degistirmeyi icerebilir.
4. **Yineleme (Istege bagli ancak yaygin):** Rafine edilmis cikti veya ayarlanmis yaklasim daha sonra yurutulur ve yansitma sureci, tatmin edici bir sonuc elde edilene veya bir durdurma kosulu karsilanana kadar tekrarlanabilir.

Yansitma kalibinin onemli ve oldukca etkili bir uygulamasi, sureci iki ayri mantiksal role ayirir: bir Uretici ve bir Elestirmen. Buna genellikle "Ureticii-Elestirmen" veya "Uretici-Gozden Geciren" modeli denir. Tek bir agent kendi kendine yansitma yapabilse de, iki ozelesmis agent (veya farkli sistem prompt'larina sahip iki ayri LLM cagrisi) kullanmak genellikle daha saglam ve tarafsiz sonuclar verir.

1. Uretici Agent: Bu agent'in birincil sorumlulugu, gorevin ilk yurutumunu gerceklestirmektir. Tamamen icerik olusturmaya odaklanir; ister kod yazmak, ister blog yazmak taslagi, ister bir plan olusturmak olsun. Baslangic prompt'unu alir ve ciktinin ilk surumunu uretir.

2. Elestirmen Agent: Bu agent'in tek amaci, Uretici tarafindan olusturulan ciktiyi degerlendirmektir. Farkli bir talimat seti, genellikle farkli bir persona verilir (ornegin "Sen kiddemli bir yazilim muhendisisin", "Sen titiz bir olgu kontrolcususun"). Elestirmen'in talimatlari, Uretici'nin calismasini olgusal dogruluk, kod kalitesi, stilistik gereksinimler veya tamlilk gibi belirli kriterlere karsi analiz etmesini yonlendirir. Kusurlari bulmak, iyilestirmeler onermek ve yapilandirilmis geri bildirim saglamak icin tasarlanmistir.

Bu gorevlerin ayriilmasi gucludur cunku bir agent'in kendi calismasini gozden gecirmesinin "bilissel yanliligini" onler. Elestirmen agent, ciktiya taze bir perspektiften yaklasr ve tamamen hatalari bulmaya ve iyilestirme alanlari belirlemeye adanmistir. Elestirmen'den gelen geri bildirim daha sonra Uretici agent'a geri aktarilir ve Uretici, ciktinin yeni, rafine edilmis bir surumunu olusturmak icin bunu kilavuz olarak kullanir. Saglanan LangChain ve ADK kod ornekleri, her ikisi de bu iki-agent modelini uygular: LangChain ornegi bir elestirmen personasi olusturmak icin belirli bir `reflector_prompt` kullanirken, ADK ornegi acikca bir uretici ve bir gozden geciren agent tanimlar.

Yansitmanin uygulanmasi, genellikle agent'in is akisini bu geri bildirim dongulerini icermek uzere yapilandirmayi gerektirir. Bu, koddaki yinelemeli donguler araciligiyla veya degerlendirme sonuclarina dayali durum yonetimi ve kosullu gecisleri destekleyen cerceveler kullanilarak gerceklestirilebilir. Bir LangChain/LangGraph veya ADK veya Crew.AI zinciri icerisinde tek bir degerlendirme ve iyilestirme adimi uygulanabilirken, gercek yinelemeli yansitma tipik olarak daha karmasik orkestrasyon gerektirir.

Yansitma kalibi, yuksek kaliteli ciktilar uretebilen, nüansli gorevleri ele alabilen ve bir dereceye kadar oz-farkindalik ve uyarlanabilirlik sergileyen agent'lar olusturmak icin kritik oneme sahiptir. Agent'lari talimatbari basitce yerine getirmekten daha gelismis bir problem cozme ve icerik uretme bicimine dogru ilerletir.

Yansitmanin hedef belirleme ve izleme (Monitoring) ile kesisimini (bkz. Bolum 11) not etmeye deger. Bir hedef (Goal), agent'in oz-degerlendirmesi icin nihai olcut saglar, izleme ise ilerlemeyi takip eder. Bircok pratik durumda, Yansitma daha sonra sapmalari analiz etmek ve stratejisini ayarlamak icin izlenen geri bildirimini kullanan duzeltici motor gorevi gorebilir. Bu sinerji, agent'i pasif bir yurutuculden hedeflerine uyarlanabilir sekilde calisan amacli bir sisteme donusturur.

Ayrica, Yansitma kalibinin etkinligi, LLM'nin konusmanin bir hafizasini (Memory) tutmasi durumunda onemli olcude artar (bkz. Bolum 8). Bu konusma gecmisi, degerlendirme asamasi icin kritik baglam saglar ve agent'in ciktisini yalnizca tek basina degil, onceki etkilesimlerin, kullanici geri bildiriminin ve gelisen hedeflerin arka planinda degerlendirmesine olanak tanir. Agent'in gecmis elestirilerden ders cikarmasini ve hatalari tekrarlamamasini saglar. Hafiza olmadan, her yansitma kendine yeten bir olaydir; hafizayla birlikte yansitma, her dongunun bir oncekinin uzerine insa ettigi kumlatif bir surec haline gelir ve daha akilli, baglama duyarli iyilestirmeye yol acar.

## Pratik Uygulamalar ve Kullanim Alanlari

Yansitma kalibi, cikti kalitesinin, dogrulugulun veya karmasik kisitlamalara uyumun kritik oldugu senaryolarda degerlidir:

### 1. Yaratici Yazim ve Icerik Olusturma

Olusturulan metni, hikayeleri, siirleri veya pazarlama metinlerini iyilestirme.

* **Kullanim Alani:** Blog yazisi yazan bir agent.
  * **Yansitma:** Taslak olustur, akis, ton ve netlik acisindan elestir, ardindan elestiriye dayanarak yeniden yaz. Yazi kalite standartlarini karsilayina kadar tekrarla.
  * **Fayda:** Daha cilali ve etkili icerik uretir.

### 2. Kod Olusturma ve Hata Ayiklama

Kod yazma, hatalari belirleme ve duzeltme.

* **Kullanim Alani:** Python fonksiyonu yazan bir agent.
  * **Yansitma:** Ilk kodu yaz, testleri veya statik analizi calistir, hatalari veya verimsizlikleri belirle, ardindan bulgulara dayanarak kodu degistir.
  * **Fayda:** Daha saglam ve islevsel kod uretir.

### 3. Karmasik Problem Cozme

Cok adimli akil yurutme gorevlerinde ara adimlari veya onerilen cozumleri degerlendirme.

* **Kullanim Alani:** Mantik bulmacasi cozen bir agent.
  * **Yansitma:** Bir adim oner, cozume daha yakin gotUrup goturmedigini veya celiskiler getirip getirmedigini degerlendir, gerekirse geri don veya farkli bir adim sec.
  * **Fayda:** Agent'in karmasik problem alanlarinda gezinme yetenegini gelistirir.

### 4. Ozetleme ve Bilgi Sentezi

Ozetleri dogruluk, tamlilk ve ozluluk acisindan iyilestirme.

* **Kullanim Alani:** Uzun bir dokumani ozetleyen bir agent.
  * **Yansitma:** Ilk ozeti olustur, orijinal dokumandaki temel noktalarla karsilastir, eksik bilgileri dahil etmek veya dogruluguil iyilestirmek icin ozeti rafine et.
  * **Fayda:** Daha dogru ve kapsamli ozetler olusturur.

### 5. Planlama ve Strateji

Onerilen bir plani degerlendirme ve potansiyel kusurlari veya iyilestirmeleri belirleme.

* **Kullanim Alani:** Bir hedefe ulasmak icin bir dizi eylem planlayan bir agent.
  * **Yansitma:** Plan olustur, yurutumunu simule et veya kisitlamalara karsi uygulanabilirligini degerlendir, degerlendirmeye dayanarak plani gozden gecir.
  * **Fayda:** Daha etkili ve gercekci planlar gelistirir.

### 6. Konusma Agent'lari

Baglami korumak, yanlisanlamalari duzeltmek veya yanit kalitesini artirmak icin konusmadaki onceki turlari gozden gecirme.

* **Kullanim Alani:** Musteri destek sohbet robotu.
  * **Yansitma:** Kullanici yanitindan sonra, tutarliligi saglamak ve kullanicinin en son girdisini dogru bir sekilde ele almak icin konusma gecmisini ve son olusturulan mesaji gozden gecir.
  * **Fayda:** Daha dogal ve etkili konusmalara yol acar.

Yansitma, agentic sistemlere bir ust-bilis katmani ekleyerek, kendi ciktilari ve sureclerinden ogrenmellerini ve daha akilli, guvenilir ve yuksek kaliteli sonuclara ulasmalarini saglar.

## Uygulamali Kod Ornegi (LangChain)

Eksiksiz, yinelemeli bir yansitma surecinin uygulanmasi, durum yonetimi ve dongusal yurutme mekanizmalari gerektirir. Bunlar, LangGraph gibi grafik tabanli cercevelerde veya ozel prosedural kod araciligiyla yerel olarak ele alinirken, tek bir yansitma dongusuunun temel ilkesi, LCEL'in (LangChain Expression Language) bilesimsel sozdizimi kullanilarak etkili bir sekilde gosterilebilir.

Bu ornek, bir sayinin faktoriyelini hesaplayan bir Python fonksiyonunu yinelemeli olarak olusturmak ve iyilestirmek icin Langchain kutuphanesi ve OpenAI'nin GPT-4o modelini kullanan bir yansitma dongusü uygular. Surec bir gorev prompt'uyla baslar, ilk kodu olusturur ve ardindan simule edilmis bir kiddemli yazilim muhendisi rolunden gelen elestirilere dayanarak kodu tekrar tekrar yansitir, her yinelemede kodu rafine eder; ta ki elestiri asamasi kodun mukemmel olduguna karar verene veya maksimum yineleme sayisina ulasilana kadar. Son olarak, ortaya cikan rafine edilmis kodu yazdirir.

Oncelikle, gerekli kutuphanelerin kurulu oldugundan emin olun:

```bash
pip install langchain langchain-community langchain-openai
```

Ayrica, sectiginiz dil modeli icin API anahtarinizla ortaminizi yapilandirmaniz gerekecektir (ornegin OpenAI, Google Gemini, Anthropic).

```python
import os
from dotenv import load_dotenv
from langchain_openai import ChatOpenAI
from langchain_core.prompts import ChatPromptTemplate
from langchain_core.messages import SystemMessage, HumanMessage


# --- Configuration ---
# Load environment variables from .env file (for OPENAI_API_KEY)
load_dotenv()

# Check if the API key is set
if not os.getenv("OPENAI_API_KEY"):
    raise ValueError("OPENAI_API_KEY not found in .env file. Please add it.")

# Initialize the Chat LLM. We use gpt-4o for better reasoning.
# A lower temperature is used for more deterministic outputs.
llm = ChatOpenAI(model="gpt-4o", temperature=0.1)


def run_reflection_loop():
    """
    Demonstrates a multi-step AI reflection loop to progressively improve a Python function.
    """
    # --- The Core Task ---
    task_prompt = """
    Your task is to create a Python function named `calculate_factorial`.
    This function should do the following:
    1.  Accept a single integer `n` as input.
    2.  Calculate its factorial (n!).
    3.  Include a clear docstring explaining what the function does.
    4.  Handle edge cases: The factorial of 0 is 1.
    5.  Handle invalid input: Raise a ValueError if the input is a negative number.
    """

    # --- The Reflection Loop ---
    max_iterations = 3
    current_code = ""

    # We will build a conversation history to provide context in each step.
    message_history = [HumanMessage(content=task_prompt)]

    for i in range(max_iterations):
        print("\n" + "=" * 25 + f" REFLECTION LOOP: ITERATION {i + 1} " + "=" * 25)

        # --- 1. GENERATE / REFINE STAGE ---
        # In the first iteration, it generates. In subsequent iterations, it refines.
        if i == 0:
            print("\n>>> STAGE 1: GENERATING initial code...")
            # The first message is just the task prompt.
            response = llm.invoke(message_history)
            current_code = response.content
        else:
            print("\n>>> STAGE 1: REFINING code based on previous critique...")
            # The message history now contains the task,
            # the last code, and the last critique.
            # We instruct the model to apply the critiques.
            message_history.append(HumanMessage(content="Please refine the code using the critiques provided."))
            response = llm.invoke(message_history)
            current_code = response.content

        print("\n--- Generated Code (v" + str(i + 1) + ") ---\n" + current_code)
        message_history.append(response)  # Add the generated code to history

        # --- 2. REFLECT STAGE ---
        print("\n>>> STAGE 2: REFLECTING on the generated code...")
        # Create a specific prompt for the reflector agent.
        # This asks the model to act as a senior code reviewer.
        reflector_prompt = [
            SystemMessage(content="""
                You are a senior software engineer and an expert
                in Python.
                Your role is to perform a meticulous code review.
                Critically evaluate the provided Python code based
                on the original task requirements.
                Look for bugs, style issues, missing edge cases,
                and areas for improvement.
                If the code is perfect and meets all requirements,
                respond with the single phrase 'CODE_IS_PERFECT'.
                Otherwise, provide a bulleted list of your critiques.
            """),
            HumanMessage(content=f"Original Task:\n{task_prompt}\n\nCode to Review:\n{current_code}"),
        ]

        critique_response = llm.invoke(reflector_prompt)
        critique = critique_response.content

        # --- 3. STOPPING CONDITION ---
        if "CODE_IS_PERFECT" in critique:
            print("\n--- Critique ---\nNo further critiques found. The code is satisfactory.")
            break

        print("\n--- Critique ---\n" + critique)
        # Add the critique to the history for the next refinement loop.
        message_history.append(HumanMessage(content=f"Critique of the previous code:\n{critique}"))

    print("\n" + "=" * 30 + " FINAL RESULT " + "=" * 30)
    print("\nFinal refined code after the reflection process:\n")
    print(current_code)


if __name__ == "__main__":
    run_reflection_loop()
```

Kod, ortami ayarlayarak, API anahtarlarini yukleyerek ve odaklanmis ciktilar icin dusuk sicaklikta GPT-4o gibi guclu bir dil modeli baslatarak baslar. Temel gorev, bir sayinin faktoriyelini hesaplayan bir Python fonksiyonu isteyen bir prompt ile tanimlanir ve docstring'ler, uc durumlar (0'in faktoriyeli) ve negatif girdiler icin hata yonetimi (Exception Handling) gibi belirli gereksinimler icerir. `run_reflection_loop` fonksiyonu yinelemeli iyilestirme surecini yonetir. Dongu icerisinde, ilk yinelemede dil modeli gorev prompt'una dayanarak ilk kodu olusturur. Sonraki yinelemelerde, onceki adimdan gelen elestirilere dayanarak kodu rafine eder. Dil modeli tarafindan oynanan ancak farkli bir sistem prompt'una sahip ayri bir "yansitici" rol, olusturulan kodu orijinal gorev gereksinimlerine karsi elestirmek icin kiddemli bir yazilim muhendisi gorevi gorur. Bu elestiri, bulunan sorunlarin madde imsli bir listesi veya sorun bulunmadiysa `CODE_IS_PERFECT` ifadesi olarak saglanir. Dongu, elestiri kodun mukemmel oldugunu belirtene veya maksimum yineleme sayisina ulasilana kadar devam eder. Konusma gecmisi, hem olusturma/iyilestirme hem de yansitma asamalari icin baglam saglamak uzere her adimda dil modeline korunur ve aktarilir. Son olarak, betik dongu sona erdikten sonra son olusturulan kod surumunu yazdirir.

## Uygulamali Kod Ornegi (ADK)

Simdi Google ADK kullanilarak uygulanan kavramsal bir kod ornegine bakalim. Ozellikle, kod bunu bir Uretici-Elestirmen yapisi kullanarak sergiler; burada bir bilesen (Uretici) ilk sonucu veya plani olusturur ve baska bir bilesen (Elestirmen) kritik geri bildirim saglar ve Uretici'yi daha rafine veya dogru bir nihai ciktiya dogru yonlendirir.

```python
from google.adk.agents import SequentialAgent, LlmAgent


# The first agent generates the initial draft.
generator = LlmAgent(
    name="DraftWriter",
    description="Generates initial draft content on a given subject.",
    instruction="Write a short, informative paragraph about the user's subject.",
    output_key="draft_text",  # The output is saved to this state key.
)

# The second agent critiques the draft from the first agent.
reviewer = LlmAgent(
    name="FactChecker",
    description="Reviews a given text for factual accuracy and provides a structured critique.",
    instruction="""
    You are a meticulous fact-checker.
    1. Read the text provided in the state key 'draft_text'.
    2. Carefully verify the factual accuracy of all claims.
    3. Your final output must be a dictionary containing two keys:
       - "status": A string, either "ACCURATE" or "INACCURATE".
       - "reasoning": A string providing a clear explanation for your status, citing specific issues if any are found.
    """,
    output_key="review_output",  # The structured dictionary is saved here.
)

# The SequentialAgent ensures the generator runs before the reviewer.
review_pipeline = SequentialAgent(
    name="WriteAndReview_Pipeline",
    sub_agents=[generator, reviewer],
)

# Execution Flow:
# 1. generator runs -> saves its paragraph to state['draft_text'].
# 2. reviewer runs -> reads state['draft_text'] and saves its dictionary output to state['review_output'].
```

Bu kod, metin olusturmak ve gozden gecirmek icin Google ADK'da sirali bir agent pipeline'i kullanimini gostermektedir. Iki LlmAgent ornegi tanimlar: generator ve reviewer. Generator agent'i, belirli bir konuda ilk taslak paragraf olusturmak icin tasarlanmistir. Kisa ve bilgilendirici bir parcca yazmasi talimati verilmistir ve ciktisini `draft_text` durum anahtarina kaydeder. Reviewer agent'i, generator tarafindan uretilen metin icin olgu kontrolcusu gorevi gorur. `draft_text`'ten metni okumasi ve olgusal dogrulugunu dogrulamasi talimati verilmistir. Reviewer'in ciktisi, iki anahtar iceren yapilandirilmis bir sozluktur: status ve reasoning. status, metnin "ACCURATE" veya "INACCURATE" oldugunu belirtir, reasoning ise durum icin bir aciklama saglar. Bu sozluk, `review_output` durum anahtarina kaydedilir. Iki agent'in yurutme sirasini yonetmek icin `review_pipeline` adli bir SequentialAgent olusturulur. Generator'un once, ardindan reviewer'in calismasini saglar. Genel yurutme akisi, generator'un metin uretmesi ve duruma kaydetmesidir. Ardindan, reviewer bu metni durumdan okur, olgu kontrolunu gerceklestirir ve bulgularini (durum ve gerekcceyi) duruma geri kaydeder. Bu pipeline, ayri agent'lar kullanarak yapilandirilmis bir icerik olusturma ve gozden gecirme surecine olanak tanir.

**Not:** ADK'nin LoopAgent'ini kullanan alternatif bir uygulama da ilgilenenler icin mevcuttur.

Sonuca varmadan once, Yansitma kalibinin cikti kalitesini onemli olcude artirmasina ragmen, onemli odunlerle birlikte geldigini dusunmek onemlidir. Yinelemeli surec, guclu olmakla birlikte, daha yuksek maliyetlere ve gecikmeye yol acabilir, cunku her iyilestirme dongusü yeni bir LLM cagrisi gerektirebilir ve bu da onu zamana duyarli uygulamalar icin optimal olmaktan cikarir. Ayrica, kalip bellek yogundur; her yinelemeyle konusma gecmisi, ilk cikti, elestiri ve sonraki iyilestirmeler dahil olmak uzere genisler.

## Bir Bakista

**Ne:** Bir agent'in ilk ciktisi genellikle optimalin altindadir; yanilsamalar, eksiklikler veya karmasik gereksinimleri karsilayamama sorunlarindan muzdariptir. Temel agentic is akislarinda, agent'in kendi hatalarini taniyip duzeltmesi icin yerlesik bir surec yoktur. Bu sorun, agent'in kendi calismasini degerlendirmesi veya daha saglam bir sekilde, kaliteden bagimsiz olarak ilk yanitin nihai yanit olmasini onleyen bir elestirmen gorevi gorecek ayri bir mantiksal agent'in tanitilmasiyla cozulur.

**Neden:** Yansitma kalibi, oz-duzeltme ve iyilestirme icin bir mekanizma sunarak bir cozum saglar. Bir "uretici" agent'in bir cikti olusturdugu ve ardindan bir "elestirmen" agent'in (veya ureticinin kendisinin) bunu onceden tanimlanmis kriterlere karsi degerlendirdigi bir geri bildirim dongusu olusturur. Bu elestiri daha sonra iyilestirilmis bir surum olusturmak icin kullanilir. Bu yinelemeli uretme, degerlendirme ve iyilestirme sureci, nihai sonucun kalitesini kademeli olarak artirir ve daha dogru, tutarli ve guvenilir sonuclara yol acar.

**Temel kural:** Yansitma kalibini, nihai ciktinin kalitesi, dogrulugu ve ayrintisi hiz ve maliyetten daha onemli oldugunda kullanin. Ozellikle cilali uzun metinler olusturma, kod yazma ve hata ayiklama ve ayrintili planlar olusturma gibi gorevler icin etkilidir. Gorevler, genel bir uretici agent'in kacirabilecegi yuksek tarafsizlik veya ozelesmis degerlendirme gerektirdiginde ayri bir elestirmen agent kulllanin.

**Gorsel ozet:**

![Reflection Design Pattern, Self-Reflection](../assets/Reflection_Design_Pattern_Self_Reflection.png)

Sekil 1: Yansitma tasarim kalibi, oz-yansitma

![Reflection Design Pattern, Producer and Critique Agent](../assets/Reflection_Design_Pattern_Producer_and_Critique_Agent.png)

Sekil 2: Yansitma tasarim kalibi, uretici ve elestirmen agent

## Temel Cikarimlar

* Yansitma kalibinin birincil avantaji, ciktilari yinelemeli olarak oz-duzeltme ve iyilestirme yetenegidir; bu da onemli olcude daha yuksek kalite, dogruluk ve karmasik talimatlara uyum saglar.
* Yurutme, degerlendirme/elestiri ve iyilestirme geri bildirim dongusunu icerir. Yansitma, yuksek kaliteli, dogru veya nüansli ciktilar gerektiren gorevler icin gereklidir.
* Guclu bir uygulama, ayri bir agent'in (veya prompt'lanmis rolun) ilk ciktiyi degerlendirdigi Uretici-Elestirmen modelidir. Bu gorev ayirimi tarafsiizligi artirir ve daha ozelesmis, yapilandirilmis geri bildirim saglar.
* Ancak, bu faydalar artan gecikme ve hesaplama maliyeti, ayrica modelin context window'unu asma veya API hizmetleri tarafindan kisitlanma riski ile birlikte gelir.
* Tam yinelemeli yansitma genellikle durumlu is akislari (LangGraph gibi) gerektirirken, tek bir yansitma adimi LangChain'de LCEL kullanilarak ciktiyi elestiri ve sonraki iyilestirme icin aktararak uygulanabilir.
* Google ADK, bir agent'in ciktisinin baska bir agent tarafindan elestirildigi ve sonraki iyilestirme adimlarina olanak taniyan sirali is akislari araciligiyla yansitmayi kolaylastirabilir.
* Bu kalip, agent'larin oz-duzeltme yapmasini ve zaman icerisinde performanslarini artirmasini saglar.

## Sonuc

Yansitma kalibi, bir agent'in is akisi icerisinde oz-duzeltme icin kritik bir mekanizma saglar ve tek gecisli bir yurutmenin otesinde yinelemeli iyilestirme mumkun kilar. Bu, sistemin bir cikti urettigi, belirli kriterlere karsi degerlendirdigi ve ardindan bu degerlendirmeyi rafine edilmis bir sonuc olusturmak icin kullandigi bir dongu olusturularak gerceklestirilir. Bu degerlendirme, agent'in kendisi (oz-yansitma) veya genellikle daha etkili bir sekilde farkli bir elestirmen agent tarafindan gerceklestirilebilir; bu, kalip icerisinde onemli bir mimari secimidir.

Tam otonom, cok adimli bir yansitma sureci durum yonetimi icin saglam bir mimari gerektirirken, temel ilkesi tek bir olusturma-elestirme-iyilestirme dongusuunee etkili bir sekilde gosterilir. Bir kontrol yapisi olarak yansitma, daha saglam ve islevsel olarak karmasik agentic sistemler olusturmak icin diger temel kaliplarla entegre edilebilir.

## Kaynaklar

Yansitma kalibi ve ilgili kavramlar hakkinda daha fazla okuma icin bazi kaynaklar:

1. Training Language Models to Self-Correct via Reinforcement Learning, [https://arxiv.org/abs/2409.12917](https://arxiv.org/abs/2409.12917)
2. LangChain Expression Language (LCEL) Documentation: [https://python.langchain.com/docs/introduction/](https://python.langchain.com/docs/introduction/)
3. LangGraph Documentation:[https://www.langchain.com/langgraph](https://www.langchain.com/langgraph)
4. Google Agent Developer Kit (ADK) Documentation (Multi-Agent Systems): [https://google.github.io/adk-docs/agents/multi-agents/](https://google.github.io/adk-docs/agents/multi-agents/)
