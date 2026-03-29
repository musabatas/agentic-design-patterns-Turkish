# Bolum 17: Akil Yurutme Teknikleri (Reasoning Techniques)

Bu bolum, akilli agent'lar icin gelismis akil yurutme (Reasoning) metodolojilerini inceleyerek cok adimli mantiksal cikarimlar ve problem cozmeye odaklanir. Bu teknikler, basit sirali islemlerin otesine gecerek agent'in ic akil yurutme surecini acik hale getirir. Bu, agent'larin problemleri parcalamasina, ara adimlari degerlendirmesine ve daha saglam ve doğru sonuclara ulasmasina olanak tanir. Bu gelismis yontemler arasindaki temel bir ilke, cikarim sirasinda artan hesaplama kaynaklarinin tahsisidir. Bu, agent'a veya alttaki LLM'e bir sorguyu islemek ve yanit olusturmak icin daha fazla islem suresi veya adim saglamak anlamina gelir. Hizli, tek gecislik bir islem yerine, agent yinelemeli iyilestirme yapabilir, birden fazla cozum yolunu kesfedebilir veya harici araclar kullanabilir. Cikarim sirasindaki bu uzatilmis isleme suresi, ozellikle daha derin analiz ve musavere gerektiren karmasik problemler icin genellikle dogrulugu, tutarliligi ve saglanligi onemli olcude arttirir.

## Pratik Uygulamalar ve Kullanim Alanlari

Pratik uygulamalar sunlardir:

* **Karmasik Soru Yanitlama:** Farkli kaynaklardan veri entegrasyonunu ve mantiksal cikarim yurutmeyi gerektiren cok atlamali sorgularin cozulenmesini kolaylastirma; birden fazla akil yurutme yolunun incelenmesini icerebilir ve bilgi sentezlemek icin uzatilmis cikarim suresinden faydalanir.
* **Matematiksel Problem Cozme:** Matematiksel problemlerin daha kucuk, cozulebilir bileşenlere bolunmesini, adim adim sureci gostermeyi ve hassas hesaplamalar icin kod yurutmesini saglamak; burada uzatilmis cikarim, daha karmasik kod olusturma ve dogrulama yapmayi mumkun kilar.
* **Kod Hata Ayiklama ve Olusturma:** Bir agent'in kod olusturma veya duzeltme gerekcessini aciklamasini, potansiyel sorunlari sirali olarak tespit etmesini ve test sonuclarina dayali olarak kodu yinelemeli olarak iyilestirmesini (Kendini Duzeltme) destekleme; kapsamli hata ayiklama dongusleri icin uzatilmis cikarim suresinden yararlanir.
* **Stratejik Planlama (Planning):** Cesitli secenekler, sonuclar ve on kosullar uzerinden akil yurutme yoluyla kapsamli planlarin gelistirilmesine yardimci olma ve gercek zamanli geri bildirime dayali olarak planlari ayarlama (ReAct); burada uzatilmis musavere daha etkili ve guvenilir planlara yol acabilir.
* **Tibbi Teshis:** Bir agent'in belirtileri, test sonuclarini ve hasta gecmislerini sistematik olarak degerlendirerek bir teşhise ulasmasina, her asamadaki akil yurutmesini ifade etmesine ve potansiyel olarak veri alma icin harici araclar kullanmasina (ReAct) yardimci olma. Artan cikarim suresi, daha kapsamli bir ayirici tani koymayi mumkun kilar.
* **Hukuki Analiz:** Arguman formule etmek veya rehberlik saglamak icin hukuki belgelerin ve emsallerin analizini destekleme, atilan mantiksal adimlarin ayrintilandirilmasi ve kendini duzeltme yoluyla mantiksal tutarlilik saglanmasi. Artan cikarim suresi, daha derinlemesine hukuki arastirma ve arguman olusturmaya olanak tanir.

## Akil Yurutme Teknikleri

Baslangic olarak, yapay zeka modellerinin problem cozme yeteneklerini gelistirmek icin kullanilan temel akil yurutme tekniklerine dalalim.

**Chain-of-Thought (CoT)** prompting, adim adim bir dusunme surecini taklit ederek LLM'lerin karmasik akil yurutme yeteneklerini onemli olcude gelistirir (bkz. Sekil 1). Dogrudan bir yanit saglamak yerine, CoT prompt'lari modeli bir dizi ara akil yurutme adimi olusturmaya yonlendirir. Bu acik ayristi, LLM'lerin karmasik problemleri daha kucuk, daha yonetilebilir alt problemlere ayristirarak ele almasina olanak tanir. Bu teknik, aritmetik, sagduyu akil yurutmesi ve sembolik manipulasyon gibi cok adimli akil yurutme gerektiren gorevlerde modelin performansini belirgin sekilde arttirir. CoT'nin temel bir avantaji, zor bir tek adimlik problemi bir dizi daha basit adima donusturme yetenegidir; boylece LLM'in akil yurutme surecinin seffafligini arttirir. Bu yaklasim yalnizca dogrulugu artirmakla kalmaz, ayni zamanda modelin karar verme surecine iliskin degerli bilgiler sunarak hata ayiklama ve anlama konusunda yardimci olur. CoT, adim adim akil yurutmeyi gosteren few-shot ornekler sunma veya modele sadece "adim adim dusun" talimatini verme gibi cesitli stratejiler kullanilarak uygulanabilir. Etkinligi, modelin ic islemesini daha kasitli ve mantiksal bir ilerleyise yonlendirme yeteneginden kaynaklanir. Sonuc olarak, Chain-of-Thought, cagdas LLM'lerde gelismis akil yurutme yeteneklerini etkinlestirmek icin temel bir teknik haline gelmistir. Karmasik problemlerin yonetilebilir alt problemlere ayristirilmasi ve bu gelistirilmis seffaflik, otonom agent'lar icin ozellikle onemlidir; cunku karmasik ortamlarda daha guvenilir ve denetlenebilir eylemler gerceklestirmelerini saglar.

![COT: Chain of Thought](../assets/COT_Chain_of_Thought.png)

Sekil 1: Agent tarafindan olusturulan ayrintili, adim adim yanitla birlikte CoT prompt'u.

Bir ornek gorelim. Yapay zekaya nasil dusunecegini anlatan bir dizi talimatla baslar; kişiligini ve izlenecek net bir bes adimli sureci tanimlar. Bu, yapilandirilmis dusunmeyi baslatan prompt'tur.

Bunu takiben, ornek CoT surecini eylemde gosterir. "Agent'in Dusunme Sureci" etiketli bolum, modelin talimat verilen adimlari uyguladigi ic monologdur. Bu, kelimenin tam anlamiyla "dusunce zinciri"dir. Son olarak, "Agent'in Nihai Yaniti", bu dikkatli, adim adim akil yurutme surecinin sonucu olarak olusturulan cilali, kapsamli ciktidir.

```markdown
You are an Information Retrieval Agent. Your goal is to answer the user's question comprehensively and accurately by thinking step-by-step.

Here's the process you must follow:
1.  **Analyze the Query:** Understand the core subject and specific requirements of the user's question. Identify key entities, keywords, and the type of information being sought.
2.  **Formulate Search Queries (for Knowledge Base):** Based on your analysis, generate a list of precise search queries that you would use to retrieve relevant information from a knowledge base or external tools.
3.  **Simulate Information Retrieval (Self-Correction/Reasoning):** For each search query, mentally consider what kind of information you expect to find. If you were to retrieve the content, what would be the most relevant snippets? Think about potential ambiguities or missing pieces.
4.  **Synthesize Information:** Based on the simulated retrieval and your understanding of the user's original query, synthesize the gathered information into a coherent and complete answer. Ensure all aspects of the query are addressed.
5.  **Review and Refine:** Before finalizing, critically evaluate your answer. Is it accurate? Is it comprehensive? Is it easy to understand? Is it concise? If not, identify what needs to be improved and how.

**User Query:** "Explain the main differences between classical computers and quantum computers, and briefly describe a potential application of quantum computing."

**Agent's Thought Process (Internal CoT Output - encouraged by the prompt):**

**Thought 1 (Analyze Query):**
The user wants two things:
    1.  Main differences between classical and quantum computers.
    2.  One potential application of quantum computing. Keywords: classical computers, quantum computers, differences, potential application.

**Thought 2 (Formulate Search Queries):**
    - "differences classical vs quantum computers"
    - "how quantum computers work"
    - "how classical computers work"
    - "applications of quantum computing"

**Thought 3 (Simulate Information Retrieval & Identify Key Concepts):**
    - From "differences": Expect concepts like bits vs. qubits, superposition, entanglement, probabilistic nature, computational power for specific problems.
    - From "how they work": Classical uses transistors/binary. Quantum uses quantum mechanics.
    - From "applications": Expect drug discovery, material science, cryptography, optimization.

**Thought 4 (Synthesize Information):**
Classical computers use bits (0 or 1), processing information sequentially. Quantum computers use qubits, which can be 0, 1, or both simultaneously (superposition), and can be entangled, allowing for vastly different computational approaches. This enables them to solve certain problems (like factoring large numbers or simulating complex molecules) far more efficiently than classical computers. A potential application is in drug discovery, where quantum computers could simulate molecular interactions with unprecedented accuracy, accelerating the development of new medicines.

**Thought 5 (Review and Refine):**
    - Differences are covered (bits vs qubits, superposition, entanglement, processing).
    - Application is given (drug discovery). - Is it brief? Yes. - Is it clear? Yes. - Looks good.

**Agent's Final Answer (Output to User):**
Classical computers process information using bits, which can be either a 0 or a 1 at any given time, performing operations sequentially. In contrast, quantum computers utilize qubits, which can exist in multiple states simultaneously through superposition and can be linked through entanglement, allowing for exponentially more complex computations. This fundamental difference enables quantum machines to tackle certain problems, such as simulating molecular structures or breaking complex encryption, that are intractable for even the most powerful classical supercomputers. A significant potential application of quantum computing lies in drug discovery, where its ability to precisely model molecular behavior could revolutionize the development of new pharmaceuticals.
```

**Tree-of-Thought (ToT)**, Chain-of-Thought (CoT) uzerine insa edilen bir akil yurutme teknigidir. Buyuk dil modellerinin farkli ara adimlara dallanarak birden fazla akil yurutme yolunu kesfetmesine olanak tanir ve bir agac yapisi olusturur (bkz. Sekil 2). Bu yaklasim, geri izleme, kendini duzeltme ve alternatif cozumlerin kesfini mumkun kilarak karmasik problem cozmeyi destekler. Olasiliklar agacini koruyarak, model bir yaniti kesinlestirmeden once cesitli akil yurutme yollarini degerlendirebilir. Bu yinelemeli surec, modelin stratejik planlama ve karar verme gerektiren zorlu gorevleri ele alma yetenegini geliştirir.

![TOT: Tree of Thought](../assets/TOT_Tree_of_Thought.png)

Sekil 2: Tree of Thoughts Ornegi

**Kendini duzeltme (Self-correction)**, kendini iyilestirme olarak da bilinen, ozellikle Chain-of-Thought prompting icerisinde bir agent'in akil yurutme surecinin onemli bir yonudur. Agent'in olusturulan icerigini ve ara dusunce sureclerini ic degerlendirmesini icerir. Bu elestirel inceleme, agent'in anlayisi veya cozumlerindeki belirsizlikleri, bilgi bosluklerini veya yanlisliklari tespit etmesini saglar. Bu gozden gecirme ve iyilestirme dongusu, agent'in yaklasimini ayarlamasina, yanit kalitesini artirmasina ve nihai bir cikti sunmadan once dogruluk ve kapsamliligi saglamasina olanak tanir. Bu ic elestiri, Bolum 4'teki orneklerde gosterildigi gibi, agent'in guvenilir ve yuksek kaliteli sonuclar uretme kapasitesini geliştirir.

Bu ornek, yapay zeka tarafindan olusturulan icerigin iyilestirilmesi icin kritik olan sistematik bir kendini duzeltme surecini gostermektedir. Taslak olusturma, orijinal gereksinimlere gore gozden gecirme ve belirli iyilestirmelerin uygulanmasindan olusan yinelemeli bir donguyu icerir. Gosterim, yapay zekanin islevini bes adimli analitik ve revizyon is akisiyla tanimlanan bir "Kendini Duzeltme Agent'i" olarak tanimlayarak baslar. Bunu takiben, sosyal medya gonderisinin standart alti bir "Ilk Taslagi" sunulur. "Kendini Duzeltme Agent'inin Dusunme Sureci" gosterimin temelini olusturur. Burada Agent, taslagi talimatlarına gore elestirel bir sekilde degerlendirir; dusuk etkilesim ve belirsiz eylem cagrisi gibi zayifliklari tespit eder. Ardindan daha etkili fiiller ve emoji kullanimi gibi somut iyilestirmeler onerir. Surec, kendini tanimlamis ayarlamalari entegre eden cilali ve belirgin sekilde gelistirilmis bir surum olan "Nihai Gozden Gecirilmis Icerik" ile sona erer.

```markdown
You are a highly critical and detail-oriented Self-Correction Agent. Your task is to review a previously generated piece of content against its original requirements and identify areas for improvement. Your goal is to refine the content to be more accurate, comprehensive, engaging, and aligned with the prompt.

Here's the process you must follow for self-correction:

1.  **Understand Original Requirements:** Review the initial prompt/requirements that led to the content's creation. What was the *original intent*? What were the key constraints or goals?
2.  **Analyze Current Content:** Read the provided content carefully.
3.  **Identify Discrepancies/Weaknesses:** Compare the current content against the original requirements. Look for:
    * **Accuracy Issues:** Are there any factual errors or misleading statements?
    * **Completeness Gaps:** Does it fully address all aspects of the original prompt? Is anything missing?
    * **Clarity & Coherence:** Is the language clear, concise, and easy to understand? Does it flow logically?
    * **Tone & Style:** Does it match the desired tone and style (e.g., professional, engaging, concise)?
    * **Engagement:** Is it captivating? Does it hold the reader's attention?
    * **Redundancy/Verbosity:** Can any parts be condensed or removed without losing meaning?
4.  **Propose Specific Improvements:** For each identified weakness, suggest concrete and actionable changes. Do not just state the problem; propose a solution.
5.  **Generate Revised Content:** Based on your proposed improvements, rewrite the original content to incorporate all the necessary changes. Ensure the revised content is polished and ready for final use.

**Original Prompt/Requirements:** "Write a short, engaging social media post (max 150 characters) announcing a new eco-friendly product line: 'GreenTech Gadgets'."

**Initial Draft (Content to be corrected):** "We have new products. They are green and techy. Buy GreenTech Gadgets now!"

**Self-Correction Agent's Thought Process (Internal CoT Output - encouraged by the prompt):**

**Thought 1 (Understand Original Requirements):**
    - Short, engaging social media post.
    - Max 150 characters.
    - Announce "GreenTech Gadgets" - a new eco-friendly product line.

**Thought 2 (Analyze Current Content):**
"We have new products. They are green and techy. Buy GreenTech Gadgets now!" (64 characters)

**Thought 3 (Identify Discrepancies/Weaknesses):** - **Engaging:** Not very engaging. Sounds generic. - **Eco-friendly:** Implied by "green," but not explicitly highlighted as a benefit. - **Call to Action:** "Buy now!" is okay, but could be more compelling. - **Conciseness:** It's short, but could use stronger verbs/phrasing. - **Impact:** Lacks excitement for a new product launch.

**Thought 4 (Propose Specific Improvements):** - Make it more dynamic and exciting. - Emphasize "eco-friendly" and "innovation." - Use stronger verbs and more active voice. - Add a clear, engaging call to action. - Ensure it stays under 150 characters. **Thought 5 (Generate Revised Content):** Original: "We have new products. They are green and techy. Buy GreenTech Gadgets now!" Revised idea 1: "🌱 Discover GreenTech Gadgets! Our new eco-friendly line blends innovation with sustainability. Go green, go smart! Shop now! #EcoFriendly #GreenTech" (148 characters) This revision directly addresses eco-friendliness, uses emojis for engagement, adds a stronger call to action, and includes relevant hashtags while staying within the character limit. **Self-Correction Agent's Final Revised Content (Output to User):** 🌱 Discover GreenTech Gadgets! Our new eco-friendly line blends innovation with sustainability. Go green, go smart! Shop now! #EcoFriendly #GreenTech
```

Temel olarak bu teknik, Agent'in icerik olusturmasina dogrudan bir kalite kontrol olcusu entegre ederek, karmasik kullanici taleplerini daha etkili bir sekilde karsilayan daha rafine, hassas ve ustun sonuclar uretir.

**Program-Aided Language Models (PALMs)**, LLM'leri sembolik akil yurutme yetenekleriyle butunlestirir. Bu entegrasyon, LLM'in problem cozme surecinin bir parcasi olarak Python gibi kod olusturmasina ve yurutmesine olanak tanir. PALMs, karmasik hesaplamalari, mantiksal islemleri ve veri manipulasyonunu deterministik bir programlama ortamina aktarir. Bu yaklasim, LLM'lerin dogruluk veya tutarlilik acisindan sinirlamalar gosterebildigi gorevler icin geleneksel programlamanin guclerinden yararlanir. Sembolik zorluklarla karsilastiginda, model kod uretebilir, yurutebilir ve sonuclari dogal dile donusturebilir. Bu hibrit metodoloji, LLM'in anlama ve olusturma yeteneklerini hassas hesaplamayla birlestirerek modelin potansiyel olarak artmis guvenilirlik ve dogrulukla daha genis bir karmasik problem yelpazesini ele almasini saglar. Agent'lar icin bu onemlidir cunku anlama ve olusturma yeteneklerinin yaninda hassas hesaplamadan yararlanarak daha doğru ve guvenilir eylemler gerceklestirmelerine olanak tanir. Ornek olarak, kod olusturmak icin Google'in ADK'sindaki harici araclarin kullanimi verilebilir.

```python
from google.adk.tools import agent_tool
from google.adk.agents import Agent
from google.adk.tools import google_search
from google.adk.code_executors import BuiltInCodeExecutor


search_agent = Agent(
    model="gemini-2.0-flash",
    name="SearchAgent",
    instruction="""
    You're a specialist in Google Search
    """,
    tools=[google_search],
)

coding_agent = Agent(
    model="gemini-2.0-flash",
    name="CodeAgent",
    instruction="""
    You're a specialist in Code Execution
    """,
    code_executor=BuiltInCodeExecutor(),
)

root_agent = Agent(
    name="RootAgent",
    model="gemini-2.0-flash",
    description="Root Agent",
    tools=[
        agent_tool.AgentTool(agent=search_agent),
        agent_tool.AgentTool(agent=coding_agent),
    ],
)
```

**Reinforcement Learning with Verifiable Rewards (RLVR):** Etkili olsa da, bircok LLM tarafindan kullanilan standart Chain-of-Thought (CoT) prompting, akil yurutmeye yonelik nispeten temel bir yaklasimdir. Problemin karmasikligina uyum saglamadan tek, onceden belirlendirilmis bir dusunce hatti olusturur. Bu sinirlamalari asmak icin, uzmanlasmis "akil yurutme modelleri" olarak adlandirilan yeni bir sinif gelistirilmistir. Bu modeller, bir yanit vermeden once degisken miktarda "dusunme" suresi ayirarak farkli bir sekilde calisir. Bu "dusunme" sureci, binlerce token uzunlugunda daha kapsamli ve dinamik bir Chain-of-Thought uretir. Bu genisletilmis akil yurutme, kendini duzeltme ve geri izleme gibi daha karmasik davranislara olanak tanir; model, daha zor problemlere daha fazla caba harcar. Bu modelleri mumkun kilan temel yenilik, Reinforcement Learning from Verifiable Rewards (RLVR) adli bir egitim stratejisidir. Modeli bilinen dogru yanitlari olan problemler (matematik veya kod gibi) uzerinde egiterek, deneme yanilma yoluyla etkili, uzun formlu akil yurutme olusturmayi ogrenir. Bu, modelin dogrudan insan denetimi olmadan problem cozme yeteneklerini gelistirmesine olanak tanir. Nihayetinde bu akil yurutme modelleri yalnizca bir yanit uretmez; planlama, izleme ve degerlendirme gibi gelismis becerileri gosteren bir "akil yurutme yolu" olustururlar. Bu gelistirilmis akil yurutme ve strateji olusturma yetenegei, karmasik gorevleri minimum insan mudahalesiyle parcalayip cozebilen otonom yapay zeka agent'larinin gelistirilmesi icin temeldir.

**ReAct** (Reasoning and Acting, bkz. Sekil 3; burada KB, Knowledge Base anlamina gelir), Chain-of-Thought (CoT) prompting'i bir agent'in araclar araciligiyla harici ortamlarla etkilesim kurma yetenegiyle butunlestiren bir paradigmadir. Nihai bir yanit ureten uretken modellerden farkli olarak, bir ReAct agent'i hangi eylemlerin alinacagi konusunda akil yurütur. Bu akil yurutme asamasi, CoT'ye benzer bir ic planlama surecini icerir; burada agent sonraki adimlarini belirler, mevcut araclari dikkate alir ve sonuclari onceden tahmin eder. Bunu takiben agent, bir veritabani sorgulama, hesaplama yapma veya bir API ile etkilesim kurma gibi bir arac veya fonksiyon cagrisi yuruterek harekete gecer.

![REACT: Reasoning and Act](../assets/REACT_Reasoning_and_Act.png)

Sekil 3: Reasoning and Act

ReAct, aralikli bir sekilde calisir: agent bir eylem yurutur, sonucu gozlemler ve bu gozlemi sonraki akil yurutmeye dahil eder. Bu "Dusunce, Eylem, Gozlem, Dusunce..." yinelemeli dongusu, agent'in planini dinamik olarak uyarlamasina, hatalari duzeltmesine ve cevreyle birden fazla etkilesim gerektiren hedeflere ulasmasina olanak tanir. Agent gercek zamanli geri bildirime yanit verdigi icin, bu, dogrusal CoT'ye kiyasla daha saglam ve esnek bir problem cozme yaklasimi saglar. Dil modeli anlama ve olusturmayi arac kullanma yetenegi ile birlestirerek, ReAct, agent'larin hem akil yurutme hem de pratik uygulama gerektiren karmasik gorevleri gerceklestirmesini saglar. Bu yaklasim, agent'larin yalnizca akil yurutmelerini degil, ayni zamanda pratik olarak adimlar yurutmelerini ve dinamik ortamlarla etkilesim kurmalarini saglayan agent'lar icin hayati onem tasir.

**CoD** (Chain of Debates), Microsoft tarafindan onerilen, birden fazla, cesitli modelin bir problemi cozmek icin is birligi yapip tartistigi resmi bir yapay zeka framework'udur; tek bir yapay zekanin "dusunce zinciri"nin otesine gecer. Bu sistem, farkli modellerin ilk fikirleri sunduğu, birbirlerinin akil yurutmesini elestirdigi ve karsı argumanlar sunduğu bir yapay zeka konsey toplantisi gibi isler. Temel amac, kolektif zekayi kullanarak dogrulugu artirmak, onyargiyi azaltmak ve nihai yanitin genel kalitesini iyilestirmektir. Bir yapay zeka akran degerlendirmesi olarak isleyen bu yontem, akil yurutme surecinin seffaf ve guvenilir bir kaydini olusturur. Nihayetinde, tek bir Agent'in yanit vermesinden, daha saglam ve doğrulanmis bir cozum bulmak icin birlikte calisan is birlikci bir Agent ekibine gecisi temsil eder.

**GoD** (Graph of Debates), tartismayi basit bir zincir yerine dinamik, dogrusal olmayan bir ag olarak yeniden tasarlayan gelismis bir Agentic framework'tur. Bu modelde, argumanlar "destekler" veya "curuter" gibi iliskileri ifade eden kenarlarla birbirine bagli tek tek dugumlerdir ve gercek tartismanin cok iş parcacikli dogasini yansitir. Bu yapi, yeni sorgulama hatlarinin dinamik olarak dallanmasina, bagimsiz olarak gelismesine ve hatta zaman icinde birlesemesine olanak tanir. Bir sonuca, bir dizinin sonunda degil, tum grafik icerisinde en saglam ve iyi desteklenen arguman kumesini belirleyerek ulasilir. Bu baglamda "iyi desteklenmis", saglam bir sekilde olusturulmus ve dogrulanabilir bilgiyi ifade eder. Bu, dogasi geregi dogru olan ve genis capta gerçek olarak kabul edilen ground truth olarak kabul edilen bilgiyi icerebilir. Ek olarak, bilginin harici kaynaklara ve gercek dunya verilerine karsi doğrulandiği search grounding araciligiyla elde edilen olgusal kanitlari kapsar. Son olarak, bir tartisma sirasinda birden fazla modelin ulastigi uzlasmayla da ilgilidir; bu, sunulan bilgiye yuksek derecede mutabakat ve guven oldugunu gosterir. Bu kapsamli yaklasim, tartisilan bilgi icin daha saglam ve guvenilir bir temel saglar. Bu yaklasim, karmasik, is birlikci yapay zeka akil yurutmesi icin daha butunsel ve gercekci bir model sunar.

**MASS (istege bagli gelismis konu):** Multi-agent sistemlerin tasariminin derinlemesine analizi, etkinliklerinin hem bireysel agent'lari programlamak icin kullanilan prompt'larin kalitesine hem de etkilesimlerini belirleyen topolojiye kritik olarak bagimli oldugunu ortaya koyar. Bu sistemlerin tasarlanmasinin karmasikligi onemlidir cunku genis ve karmasik bir arama uzayini icerir. Bu zorlugun ustesinden gelmek icin, MAS tasarimini otomatiklestirmek ve optimize etmek amaciyla Multi-Agent System Search (MASS) adli yeni bir cerceve gelistirilmistir.

MASS, prompt ve topoloji optimizasyonunu aralikli olarak yaparak karmasik tasarim uzayinda sistematik olarak ilerleyen cok asamali bir optimizasyon stratejisi kullanir (bkz. Sekil 4).

**1. Blok Duzeyinde Prompt Optimizasyonu:** Surec, bireysel agent turleri veya "bloklar" icin prompt'larin yerel optimizasyonuyla baslar; her bilesenin daha buyuk bir sisteme entegre edilmeden once rolunu etkili bir sekilde yerine getirmesini saglar. Bu ilk adim, sonraki topoloji optimizasyonunun, kotu yapilandirilmis olanlarin birikimli etkisinden zarar gormek yerine, iyi performans gosteren agent'lar uzerine insa etmesini saglayan önemli bir adimdir. Ornegin, HotpotQA veri seti icin optimize ederken, bir "Debator" agent'inin prompt'u yaratici bir sekilde "buyuk bir yayinin uzman dogruluk denetcisi" olarak hareket etmesi icin cercevelenir. Optimize edilmis gorevi, diger agent'lardan gelen onerilen yanitlari titizlikle incelemek, saglanan baglam parcalariyla carpraz referans yapmak ve tutarsizliklari veya desteklenmeyen iddialari belirlemektir. Blok duzeyinde optimizasyon sirasinda kesfedilen bu uzmanlasmis rol oynama prompt'u, debator agent'ini daha buyuk bir is akisina yerlestirmeden once bilgi sentezlemede son derece etkili hale getirmeyi amaclar.

**2. Workflow Topoloji Optimizasyonu:** Yerel optimizasyonun ardindan MASS, ozellestirilebilir bir tasarim uzayindan farkli agent etkilesimlerini secerek ve duzenleyerek is akisi topolojisini optimize eder. Bu aramayi verimli hale getirmek icin MASS, etki agirlikli bir yontem kullanir. Bu yontem, her topolojinin bir temel agent'a gore performans kazancini olcerek "artimli etkisini" hesaplar ve bu puanlari aramayi daha umut verici kombinasyonlara yonlendirmek icin kullanir. Ornegin, MBPP kodlama gorevi icin optimize ederken, topoloji aramasi belirli bir hibrit is akisinin en etkili oldugunu kesfeder. Bulunan en iyi topoloji basit bir yapi degil, yinelemeli bir iyilestirme surecinin harici arac kullanimiyla kombinasyonudur. Spesifik olarak, kodu test senaryolarina karsi calıstiran bir executor agent tarafindan doğrulanan birkac yansitma (Reflection) turundan gecen bir predictor agent'tan olusur. Bu kesfedilen is akisi, kodlama icin yinelemeli kendini duzeltmeyi harici dogrulama ile birlestiren bir yapinin daha basit MAS tasarimlarindan ustun oldugunu gosterir.

![MASS: Multi-Agent System Search](../assets/MASS_Multi_Agent_System_Search.png)

Sekil 4: (Yazarlarin izniyle): Multi-Agent System Search (MASS) Framework'u, optimize edilebilir prompt'lari (talimatlar ve gosterimler) ve yapilandirabilir agent yapi taslarini (Aggregate, Reflect, Debate, Summarize ve Tool-use) kapsayan bir arama uzayinda ilerleyen uc asamali bir optimizasyon surecidir. Ilk asama, Blok Duzeyinde Prompt Optimizasyonu, her agent modulu icin prompt'lari bagimsiz olarak optimize eder. Ikinci asama, Workflow Topoloji Optimizasyonu, etki agirlikli bir tasarim uzayindan gecerli sistem yapilandirmalari ornekler ve optimize edilmis prompt'lari entegre eder. Son asama, Workflow Duzeyinde Prompt Optimizasyonu, Ikinci asamadan optimal is akisi belirlendikten sonra tum multi-agent sistemi icin ikinci bir tur prompt optimizasyonu icerir.

**3. Workflow Duzeyinde Prompt Optimizasyonu:** Son asama, tum sistemin prompt'larinin global optimizasyonunu icerir. En iyi performans gosteren topoloji belirlendikten sonra, prompt'lar orkestrasyon icin uyarlanmis olduklarindan ve agent karsilikli bagimliliklarinin optimize edildiginden emin olmak icin tek, butunlesik bir varlik olarak ince ayarlanir. Ornek olarak, DROP veri seti icin en iyi topolojiyi bulduktan sonra, son optimizasyon asamasi "Predictor" agent'inin prompt'unu iyilestirir. Nihai, optimize edilmis prompt son derece ayrintilidir; agent'a veri setinin bir ozetiyle baslar, "cikarimci soru yanitlama" ve "sayisal bilgi" odagina dikkat ceker. Ardindan dogru soru yanitlama davranisinin few-shot orneklerini icerir ve temel talimati yuksek riskli bir senaryo olarak cerceveler: "Acil bir haber raporu icin kritik sayisal bilgileri cikarmakla gorevlendirilmis son derece uzmanlasmis bir yapay zekasiniz. Canli bir yayin dogrulugunuza ve hiziniza guveniyordur". Meta bilgi, ornekler ve rol oynamayi birlestiren bu cok yonlu prompt, dogrulugu maksimize etmek icin nihai is akisina ozel olarak ayarlanmistir.

Temel Bulgular ve Ilkeler: Deneyler, MASS tarafindan optimize edilen MAS'in, bir dizi gorevde mevcut elle tasarlanmis sistemleri ve diger otomatik tasarim yontemlerini onemli olcude geride biraktigini gostermektedir. Bu arastirmadan turetilen etkili MAS icin temel tasarim ilkeleri uc yonludur:

* Bireysel agent'lari olusturmadan once yuksek kaliteli prompt'larla optimize edin.
* Kisitlanmamis bir arama uzayini kesfetmek yerine etkili topolojileri bir araya getirerek MAS olusturun.
* Agent'lar arasindaki karsilikli bagimliliklari nihai, is akisi duzeyinde bir ortak optimizasyon araciligiyla modelleyin ve optimize edin.

Temel akil yurutme tekniklerine iliskin tartismamiz uzerine insa ederek, once temel bir performans ilkesini inceleyelim: LLM'ler icin Olceklendirme Cikarim Yasasi. Bu yasa, bir modelin performansinin, kendisine tahsis edilen hesaplama kaynaklari arttikca ongorulebiilir bir sekilde iyilestigini belirtir. Bu ilkeyi, bir yapay zeka agent'inin bir konuyu alt sorulara ayirarak, Web arama aracini kullanarak ve bulgularini sentezleyerek ozerk olarak arastirdigi Deep Research gibi karmasik sistemlerde eylemde gorebiliriz.

**Deep Research.** "Deep Research" terimi, yorulmak bilmeyen, metodik arastirma asistanlari olarak hareket etmek uzere tasarlanmis bir kategori yapay zeka Agentic aracini tanimlar. Bu alandaki basslica platformlar arasinda Perplexity AI, Google'in Gemini arastirma yetenekleri ve OpenAI'in ChatGPT icindeki gelismis islevleri bulunur (bkz. Sekil 5).

![Google Deep Research for Information Gathering](../assets/Google_Deep_Research_for_Information_Gathering.png)

Sekil 5: Bilgi Toplama icin Google Deep Research

Bu araclarin tanittigi temel bir degisiklik, arama surecinin kendisindeki degisikliktir. Standart bir arama aninda baglantilar saglayarak sentez isini size birakir. Deep Research farkli bir modelle calisir. Burada bir yapay zekaya karmasik bir sorgu verirsiniz ve genellikle birkac dakikalik bir "zaman butcesi" tanirsiniz. Bu sabirliliginiz karsiliginda ayrintili bir rapor alirsiniz.

Bu sure zarfinda yapay zeka, sizin adıniza agentic bir sekilde calisir. Bir kisi icin inanilmaz derecede zaman alici olacak bir dizi sofistike adimi ozerk olarak gerceklestirir:

1. Ilk Kesfetme: Ilk prompt'unuza dayali olarak birden fazla, hedefli arama yurutur.
2. Akil Yurutme ve Iyilestirme: Sonuclarin ilk dalgasini okur ve analiz eder, bulguları sentezler ve boslukları, celiskileri veya daha fazla ayrinti gerektiren alanlari elestirel olarak belirler.
3. Takip Sorusturmasi: Ic akil yurutmesine dayali olarak bu boslukları doldurmak ve anlayisini derinlestirmek icin yeni, daha nüansli aramalar yapar.
4. Nihai Sentez: Birkac tur yinelemeli arama ve akil yurutmeden sonra, doğrulanmis tum bilgileri tek, tutarli ve yapilandirilmis bir ozete derler.

Bu sistematik yaklasim, kapsamli ve iyi dusunulmus bir yanit saglayarak bilgi toplamanin verimliligini ve derinligini onemli olcude arttirir ve boylece daha agentic karar vermeyi kolaylastirir.

## Olceklendirme Cikarim Yasasi

Bu kritik ilke, bir LLM'in performansi ile cikarim olarak bilinen operasyonel asamasinda tahsis edilen hesaplama kaynaklari arasindaki iliskiyi belirler. Cikarim Olceklendirme Yasasi, model kalitesinin bir modelin olusturulmasi sirasinda artan veri hacmi ve hesaplama gucu ile nasil iyilestilgi uzerine odaklanan daha bilinen egitim olceklendirme yasalarindan farklidir. Bunun yerine, bu yasa ozellikle bir LLM'in aktif olarak bir cikti veya yanit olustururken meydana gelen dinamik odunlesimleri inceler.

Bu yasanin temel tasi, ustun sonuclarin nispeten daha kucuk bir LLM'den cikarim zamaninda hesaplama yatirimini arttirarak siklikla elde edilebilecegi bulgusudur. Bu, daha guclu bir GPU kullanmak anlamina gelmez; aksine daha sofistike veya kaynak yogun cikarim stratejileri kullanmak anlamina gelir. Boyle bir stratejinin onemli bir ornegi, modele birden fazla potansiyel yanit olusturmasini, belki de cesitli beam search veya self-consistency yontemleri gibi tekniklerle, ve ardindan en optimal ciktiyi belirlemek icin bir secim mekanizmasi kullanmasini talimat vermektir. Bu yinelemeli iyilestirme veya coklu aday olusturma sureci daha fazla hesaplama dongusu gerektirir ancak nihai yanitin kalitesini onemli olcude yukseltebilir.

Bu ilke, Agent sistemlerinin konuslandirilmasinda bilingli ve ekonomik olarak saglam karar verme icin onemli bir cerceve sunar. Daha buyuk bir modelin her zaman daha iyi performans saglayacagi sezgisel kavramina meydan okur. Yasa, daha kucuk bir modelin cikarim sirasinda daha buyuk bir "dusunme butcesi" verildiginde, daha basit, daha az hesaplama yogun bir olusturma surecine dayanan cok daha buyuk bir modelin performansini zaman zaman asabilecegini one surer. Buradaki "dusunme butcesi", cikarim sirasinda uygulanan ek hesaplama adimlarini veya karmasik algoritmalari ifade eder ve daha kucuk modelin bir yanita karar vermeden once daha genis bir olasilik yelpazesini kesfetmesini veya daha titiz ic kontroller uygulamasini saglar.

Sonuc olarak, Olceklendirme Cikarim Yasasi verimli ve maliyet etkin Agentic sistemler olusturmak icin temel hale gelir. Birkac birbirine bagli faktoru titizlikle dengelemek icin bir metodoloji saglar:

* **Model Boyutu:** Daha kucuk modeller, bellek ve depolama acisindan dogal olarak daha az talepkardır.
* **Yanit Gecikmesi:** Artan cikarim zamani hesaplamasi gecikmeye ekleyebilirken, yasa, performans kazanclarinin bu artisi aştigi noktayi veya asiri gecikmeleri onlemek icin hesaplamanin nasil stratejik olarak uygulanacagini belirlemeye yardimci olur.
* **Operasyonel Maliyet:** Daha buyuk modellerin konuslandirilmasi ve calistirilmasi, artan enerji tuketimi ve altyapi gereksinimleri nedeniyle genellikle daha yuksek devam eden operasyonel maliyetlere yol acar. Yasa, bu maliyetleri gereksiz yere artirmadan performansin nasil optimize edilecegini gosterir.

Olceklendirme Cikarim Yasasini anlayarak ve uygulayarak, gelistiriciler ve kuruluslar belirli agentic uygulamalar icin optimal performansa yonelik stratejik secimler yapabilir ve hesaplama kaynaklarinin LLM'in ciktisinin kalitesi ve faydasi uzerinde en onemli etkiye sahip olacaklari yerlere tahsis edilmesini saglar. Bu, basit bir "buyuk olan daha iyidir" paradigmasinin otesine gecerek yapay zeka konuslandirmasina daha nüansli ve ekonomik olarak uygulanabilir yaklasimlar saglar.

## Uygulamali Kod Ornegi

Google tarafindan acik kaynakli olarak paylasilan DeepSearch kodu, gemini-fullstack-langgraph-quickstart deposu araciligiyla kullanilabilir (Sekil 6). Bu depo, gelisiticilerin Gemini 2.5 ve LangGraph orkestrasyon framework'u kullanarak tam yigin yapay zeka agent'lari olusturmasi icin bir sablon saglar. Bu acik kaynak yigini, agent tabanli mimarilerle deneyler yapmayi kolaylastirir ve Gemma gibi yerel LLM'lerle entegre edilebilir. Docker ve moduler proje iskeletlemesi kullanarak hizli prototipleme saglar. Bu surumun iyi yapilandirilmis bir gosterim niteliginde oldugu ve uretim icin hazir bir backend olarak tasarlanmadigi belirtilmelidir.

![Example of DeepSearch with multiple Reflection Steps](../assets/Example_of_DeepSearch_with_multiple_Reflection_Steps.png)

Sekil 6: (Yazarlarin izniyle) Birden Fazla Yansitma (Reflection) Adimi ile DeepSearch Ornegi

Bu proje, gelismis arastirma ve konusmali yapay zeka icin tasarlanmis bir React frontend ve bir LangGraph backend iceren tam yigin bir uygulama sunar. Bir LangGraph agent'i, Google Gemini modelleri kullanarak dinamik olarak arama sorgulari olusturur ve Google Search API araciligiyla web arastirmasini entegre eder. Sistem, bilgi bosluklerini belirlemek, aramalari yinelemeli olarak iyilestirmek ve alintilarla yanitlari sentezlemek icin yansitmali akil yurutme kullanir. Frontend ve backend hot-reloading destekler. Projenin yapisi ayri frontend/ ve backend/ dizinleri icerir. Kurulum gereksinimleri Node.js, npm, Python 3.8+ ve bir Google Gemini API anahtarini icerir. API anahtarini backend'in .env dosyasinda yapilandirdiktan sonra, hem backend (pip install . kullanarak) hem de frontend (npm install) icin bagimliliklar kurulabilir. Gelistirme sunuculari make dev ile esanli veya ayri ayri calistrilabilir. backend/src/agent/graph.py dosyasinda tanimlanan backend agent'i, ilk arama sorgulari olusturur, web arastirmasi yapar, bilgi acigi analizi gerceklestirir, sorgulari yinelemeli olarak iyilestirir ve bir Gemini modeli kullanarak alintili bir yanit sentezler. Uretim konuslandirmasi, backend sunucusunun statik bir frontend derlemesi sunmasini gerektirir ve gercek zamanli ciktiyi streaming icin Redis ve verileri yonetmek icin bir Postgres veritabanı gerektirir. Bir Docker imaji docker-compose up kullanilarak olusturulup calistiriilabilir; bu ayrica docker-compose.yml ornegi icin bir LangSmith API anahtari gerektirir. Uygulama, React ile Vite, Tailwind CSS, Shadcn UI, LangGraph ve Google Gemini kullanir. Proje Apache License 2.0 altinda lisanslidir.

| ``# Create our Agent Graph builder = StateGraph(OverallState, config_schema=Configuration) # Define the nodes we will cycle between builder.add_node("generate_query", generate_query) builder.add_node("web_research", web_research) builder.add_node("reflection", reflection) builder.add_node("finalize_answer", finalize_answer) # Set the entrypoint as `generate_query` # This means that this node is the first one called builder.add_edge(START, "generate_query") # Add conditional edge to continue with search queries in a parallel branch builder.add_conditional_edges(    "generate_query", continue_to_web_research, ["web_research"] ) # Reflect on the web research builder.add_edge("web_research", "reflection") # Evaluate the research builder.add_conditional_edges(    "reflection", evaluate_research, ["web_research", "finalize_answer"] ) # Finalize the answer builder.add_edge("finalize_answer", END) graph = builder.compile(name="pro-search-agent")`` |
| :---- |

Sekil 4: LangGraph ile DeepSearch Ornegi (backend/src/agent/graph.py dosyasindan kod)

## Peki, Agent'lar Ne Dusunur?

Ozetle, bir agent'in dusunme sureci, problemleri cozmek icin akil yurutme ve eylemi birlestiren yapilandirilmis bir yaklasimdir. Bu yontem, bir agent'in adimlarini acikca planlamasina, ilerlemesini izlemesine ve bilgi toplamak icin harici araclarla etkilesim kurmasina olanak tanir.

Ozunde, agent'in "dusunmesi" guclu bir LLM tarafindan kolaylastirilir. Bu LLM, agent'in sonraki eylemlerine rehberlik eden bir dizi dusunce olusturur. Surec genellikle bir dusunce-eylem-gozlem dongusunu takip eder:

1. **Dusunce:** Agent, ilk olarak problemi parcalayan, bir plan formule eden veya mevcut durumu analiz eden metinsel bir dusunce olusturur. Bu ic monolog, agent'in akil yurutme surecini seffaf ve yonlendirilebilir kilar.
2. **Eylem:** Dusunceye dayali olarak, agent onceden tanimlanmis, ayrik bir secenekler kumesinden bir eylem secer. Ornegin, bir soru yanitlama senaryosunda, eylem uzayi cevrimici arama yapmayi, belirli bir web sayfasindan bilgi almayi veya nihai bir yanit saglamayi icerebilir.
3. **Gozlem:** Agent daha sonra alinan eyleme dayali olarak cevresinden geri bildirim alir. Bu, bir web arama sonuclari veya bir web sayfasinin icerigi olabilir.

Bu dongu, agent nihai bir cozume ulastigini belirleyip bir "bitir" eylemi gerceklestirinceye kadar tekrarlanır; her gozlem bir sonraki dusunceyi bilgilendirir.

Bu yaklasimin etkililigi, alttaki LLM'in gelismis akil yurutme ve planlama yeteneklerine dayanir. Agent'i yonlendirmek icin, ReAct framework'u genellikle LLM'e insan benzeri problem cozme yollarinin orneklerinin saglandigi few-shot learning kullanir. Bu ornekler, benzer gorevleri cozmek icin dusuncelerin ve eylemlerin nasil etkili bir sekilde birlestirileceğini gosterir.

Bir agent'in dusunce sikligi, goreve bagli olarak ayarlanabilir. Gercek kontrolu gibi bilgi yogun akil yurutme gorevleri icin, mantikli bir bilgi toplama ve akil yurutme akisi saglamak icin dusunceler genellikle her eylemle aralikli olarak yerlestirilir. Buna karsilik, simulasyonlu bir ortamda gezinme gibi cok sayida eylem gerektiren karar verme gorevleri icin, dusunceler daha az siklikta kullanilabilir; agent'in dusunmenin ne zaman gerekli olduguna karar vermesine olanak tanır.

## Bir Bakista

**Ne:** Karmasik problem cozme, genellikle tek bir dogrudan yanitin otesini gerektirir ve yapay zeka icin onemli bir zorluk olusturur. Temel problem, yapay zeka agent'larinin mantiksal cikarim, ayristirma ve stratejik planlama gerektiren cok adimli gorevleri ele almasini saglamaktir. Yapilandirilmis bir yaklasim olmadan, agent'lar karmasikliklari ele almakta basarisiz olabilir ve yanlis veya eksik sonuclara yol acabilir. Bu gelismis akil yurutme metodolojileri, bir agent'in ic "dusunce" surecini acik hale getirmeyi amaclayarak, zorluklari sistematik olarak islemesine olanak tanir.

**Neden:** Standartlastirilmis cozum, bir agent'in problem cozme sureci icin yapilandirilmis bir cerceve saglayan bir akil yurutme teknikleri paketidir. Chain-of-Thought (CoT) ve Tree-of-Thought (ToT) gibi metodolojiler, LLM'leri problemleri parcalamaya ve birden fazla cozum yolunu kesfetmeye yonlendirir. Kendini Duzeltme (Self-Correction), yanitlarin yinelemeli olarak iyilestirilmesine olanak taniarak daha yuksek dogruluk saglar. ReAct gibi agentic framework'ler, akil yurutmeyi eylemle butunlestirerek agent'larin harici araclar ve ortamlarla etkilesim kurarak bilgi toplamasina ve planlarini uyarlamasina olanak tanir. Acik akil yurutme, kesfetme, iyilestirme ve arac kullaniminin bu kombinasyonu, daha saglam, seffaf ve yetenekli yapay zeka sistemleri olusturur.

**Temel Kural:** Bu akil yurutme tekniklerini, bir problemin tek gecislik bir yanit icin cok karmasik oldugunda ve ayristirma, cok adimli mantik, harici veri kaynaklari veya araclarla etkilesim ya da stratejik planlama ve uyum gerektirdiginde kullanin. "Calismayı" veya dusunce surecini gostermenin nihai yanit kadar onemli oldugu gorevler icin idealdir.

**Gorsel Ozet:**

![Reasoning Design Pattern](../assets/Reasoning_Design_Pattern.png)

Sekil 7: Akil yurutme tasarim kalibi

## Onemli Cikarimlar

* Akil yurutmelerini acik hale getirerek, agent'lar seffaf, cok adimli planlar formule edebilir; bu, otonom eylem ve kullanici guveni icin temel yetenektir.
* ReAct framework'u, agent'lara temel operasyonel dongusunu saglayarak, salt akil yurutmenin otesine gecip bir ortamda dinamik olarak hareket etmelerini ve uyum saglamalarini icin harici araclarla etkilesim kurmalarini guclendirir.
* Olceklendirme Cikarim Yasasi, bir agent'in performansinin yalnizca alttaki model boyutuyla degil, tahsis edilen "dusunme suresiyle" ilgili oldugunu ima eder; daha kasitli ve daha yuksek kaliteli otonom eylemlere olanak tanir.
* Chain-of-Thought (CoT), bir agent'in ic monologu olarak hizmet ederek karmasik bir hedefa yonelik bir dizi yonetilebilir eyleme ayristirarak bir plan formule etmenin yapilandirilmis bir yolunu saglar.
* Tree-of-Thought ve Kendini Duzeltme, agent'lara musavere etme yetenegi kazandirarak birden fazla stratejiyi degerlendirmelerine, hatalardan geri donmelerine ve yurutmeden once kendi planlarini iyilestirmelerine olanak tanir.
* Chain of Debates (CoD) gibi is birlikci framework'ler, tekil agent'lardan, daha karmasik problemlerin ustesinden gelmek ve bireysel onyargilari azaltmak icin birlikte akil yurutebilen multi-agent sistemlerine gecisi isaret eder.
* Deep Research gibi uygulamalar, bu tekniklerin, bir kullanici adina derinlemesine arastirma gibi karmasik, uzun sureli gorevleri tamamen ozerk olarak yurutebilen agent'larda nasil sonuclanadigini gosterir.
* Etkili agent ekipleri olusturmak icin MASS gibi framework'ler, bireysel agent'larin nasil talimatlandirildigi ve nasil etkilestiklerinin optimizasyonunu otomatiklestirerek tum multi-agent sisteminin optimal performans gostermesini saglar.
* Bu akil yurutme tekniklerini entegre ederek, yalnizca otomatik degil gercekten otonom, planlamak, hareket etmek ve karmasik problemleri dogrudan denetim olmadan cozmek icin guvenilir agent'lar insaa ederiz.

## Sonuclar

Modern yapay zeka, pasif araclardan, yapilandirilmis akil yurutme yoluyla karmasik hedefleri ele alabilen otonom agent'lara evrilmektedir. Bu agentic davranis, agent'in harekete gecmeden once tutarli bir plan formule etmesini saglayan Chain-of-Thought (CoT) gibi tekniklerle guclendirilmis bir ic monologla baslar. Gercek otonomi, agent'larin Kendini Duzeltme ve Tree-of-Thought (ToT) araciligiyla elde ettigi musavereyi gerektirir; birden fazla stratejiyi degerlendirmelerine ve kendi calismilarini bagimsiz olarak iyilestirmelerine olanak tanir. Tamamen agentic sistemlere gecisteki pivotal sicrma, bir agent'in dusunmenin otesine gecip harici araclari kullanarak harekete gecmesini guclerndiren ReAct framework'undan gelir. Bu, dusunce, eylem ve gozlemden olusan temel agentic donguyu olusturarak agent'in cevresel geri bildirime dayali olarak stratejisini dinamik olarak uyarlamasina olanak tanir.

Bir agent'in derin musavere kapasitesi, daha fazla hesaplama "dusunme suresi"nin dogrudan daha saglam otonom eylemlere dönüstugu Olceklendirme Cikarim Yasasi tarafindan beslenir. Sonraki sinir, Chain of Debates (CoD) gibi framework'lerin ortak bir hedefe ulasmak icin birlikte akil yuruten is birlikci agent toplulukları olusturdugu multi-agent sistemidir. Bu teorik degildir; Deep Research gibi agentic uygulamalar, otonom agent'larin bir kullanici adina karmasik, cok adimli sorusturmalari nasil yurutebildigini zaten gostermektedir. Kapsayici hedef, karmasik problemleri bagimsiz olarak yonetmek ve cozmek icin guvenilir guvenilir ve seffaf otonom agent'lar muhendislik etmektir. Nihayetinde, acik akil yurutmeyi eylem gucuyle birlestirerek, bu metodolojiler yapay zekanin gercekten agentic problem cozuculere donusumunu tamamlamaktadir.

## Referanslar

Ilgili arastirmalar sunlardir:

1. "Chain-of-Thought Prompting Elicits Reasoning in Large Language Models" by Wei et al. (2022)
2. "Tree of Thoughts: Deliberate Problem Solving with Large Language Models" by Yao et al. (2023)
3. "Program-Aided Language Models" by Gao et al. (2023)
4. "ReAct: Synergizing Reasoning and Acting in Language Models" by Yao et al. (2023)
5. Inference Scaling Laws: An Empirical Analysis of Compute-Optimal Inference for LLM Problem-Solving, 2024
6. Multi-Agent Design: Optimizing Agents with Better Prompts and Topologies, [https://arxiv.org/abs/2502.02533](https://arxiv.org/abs/2502.02533)
