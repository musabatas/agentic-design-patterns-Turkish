# Sozluk

## Temel Kavramlar

- **Prompt**: Prompt, bir kullanicinin bir yapay zeka modeline yanit almak icin sundugu, genellikle soru, talimat veya ifade seklindeki girdidir. Prompt'un kalitesi ve yapisi, modelin ciktisini buyuk olcude etkiler ve prompt muhendisligini yapay zekayi etkili bir sekilde kullanmak icin onemli bir beceri haline getirir.

- **Context Window**: Context window, bir yapay zeka modelinin hem girdiyi hem de urettigi ciktiyi dahil ederek bir seferde isleyebildigi maksimum token sayisidir. Bu sabit boyut kritik bir sinirlamadir; pencere disindaki bilgi goz ardi edilirken, daha buyuk pencereler daha karmasik konusmalara ve belge analizine olanak tanir.

- **In-Context Learning**: In-context learning, bir yapay zekanin herhangi bir yeniden egitim gerektirmeden dogrudan prompt icinde verilen orneklerden yeni bir gorevi ogrenme yetenegidir. Bu guclu ozellik, tek bir genel amacli modelin aninda sayisiz belirli goreve uyarlanmasini saglar.

- **Zero-Shot, One-Shot ve Few-Shot Prompting**: Bunlar, bir modele bir gorevi yonlendirmek icin sifir, bir veya birkac ornek verilen prompt tekniklerindir. Daha fazla ornek saglamak, genellikle modelin kullanicinin niyetini daha iyi anlamasina yardimci olur ve belirli gorev icin dogrulugunu arttirir.

- **Multimodality**: Multimodality, bir yapay zekanin metin, goruntu ve ses gibi birden fazla veri turundeki bilgiyi anlama ve isleme yetenegidir. Bu, bir goruntuyu tanimlama veya sozlu bir soruyu cevaplama gibi daha cok yonlu ve insana benzer etkilesimlere olanak tanir.

**Grounding**: Grounding, bir modelin ciktilarini olgusal dogrulugu saglamak ve hallucination'lari azaltmak icin dogrulanabilir, gercek dunya bilgi kaynaklarina baglama suresidir. Bu genellikle yapay zeka sistemlerini daha guvenilir kilmak icin RAG gibi tekniklerle gerceklestirilir.

## Temel Yapay Zeka Model Mimarileri

- **Transformers**: Transformer, cogu modern LLM'nin temelini olusturan sinir agi mimarisidir. Temel yeniligi, uzun metin dizilerini verimli bir sekilde isleyen ve kelimeler arasindaki karmasik iliskileri yakalayan self-attention mekanizmasidir.

- **Recurrent Neural Network (RNN)**: Recurrent Neural Network, Transformer'dan once gelen temel bir mimaridir. RNN'ler bilgiyi sirasiyla isler ve onceki girdilerin bir "bellegini" korumak icin donguler kullanir; bu da onlari metin ve konusma isleme gibi gorevler icin uygun hale getirmistir.

- **Mixture of Experts (MoE)**: Mixture of Experts, bir "router" agin herhangi bir girdiyi islemek icin dinamik olarak kucuk bir "uzman" ag alt kumesi sectigi verimli bir model mimarisidir. Bu, modellerin hesaplama maliyetlerini yonetilebilir tutarken cok sayida parametreye sahip olmasina olanak tanir.

- **Diffusion Models**: Diffusion modelleri, yuksek kaliteli goruntular olusturmada ustun olan uretici modellerdir. Verilere rastgele gurultu ekleyerek ve ardindan bir modeli bu sureci titizlikle tersine cevirmek icin egiterek calisir, boylece rastgele bir baslangic noktasindan yeni veriler uretebilirler.

- **Mamba**: Mamba, ozellikle cok uzun baglamlar icin yuksek verimlilikle dizileri islemek amaciyla Selective State Space Model (SSM) kullanan yeni bir yapay zeka mimarisidir. Secici mekanizmasi, gurultuyu filtrelerken ilgili bilgiye odaklanmasina olanak tanir ve onu Transformer'a potansiyel bir alternatif yapar.

## LLM Gelistirme Yasam Dongusu

- Guclu bir dil modelinin gelistirilmesi belirli bir diziyi takip eder. Genel internet metinlerinden olusan genis bir veri kumesi uzerinde egitilerek dil, akil yurutme ve dunya bilgisi ogrenmesini saglayan buyuk bir temel modelin insa edildigi Pre-training ile baslar. Ardindan, genel modelin yeteneklerini belirli bir amac icin uyarlamak amaciyla daha kucuk, goreve ozel veri kumeleri uzerinde daha fazla egitildigi uzmanlaasma asamasi olan Fine-tuning gelir. Son asama, ozellestirilmis modelin davranisinin, ciktilarinin yardimci, zararsiz ve insan degerleriyle uyumlu olmasini saglamak icin ayarlandigi Alignment'tir.

- Pre-training Teknikleri: Pre-training, bir modelin buyuk miktarda veriden genel bilgi ogrendigi ilk asamadir. Bunun icin en onemli teknikler, modelin ogrenecegi farkli hedefler icerir. En yaygin olani, modelin bir cumledeki sonraki kelimeyi tahmin ettigi Causal Language Modeling (CLM)'dir. Bir digeri, modelin bir metindeki kasitli olarak gizlenmis kelimeleri doldurdugu Masked Language Modeling (MLM)'dir. Diger onemli yontemler arasinda modelin bozulmus bir girdiyi orijinal durumuna geri yuklemesini ogrendigi Denoising Objectives, benzer ve benzer olmayan veri parcalari arasinda ayrim yapmayi ogrendigi Contrastive Learning ve iki cumlenin mantiksal olarak birbirini takip edip etmedigini belirlediği Next Sentence Prediction (NSP) yer alir.

- Fine-tuning Teknikleri: Fine-tuning, genel bir on-egitimli modeli daha kucuk, ozellestirilmis bir veri kumesi kullanarak belirli bir goreve uyarlama suresidir. En yaygin yaklasim, modelin dogru girdi-cikti ciftlerinin etiketli ornekleri uzerinde egitildigi Supervised Fine-Tuning (SFT)'dir. Populer bir varyant, modeli kullanici komutlarini daha iyi takip etmeye odaklanan Instruction Tuning'dir. Bu sureci daha verimli hale getirmek icin, yalnizca az sayida parametreyi guncelleyen LoRA (Low-Rank Adaptation) ve bellek optimize edilmis surumu QLoRA gibi en onemli teknikleri iceren Parameter-Efficient Fine-Tuning (PEFT) yontemleri kullanilir. Bir baska teknik olan Retrieval-Augmented Generation (RAG), fine-tuning veya cikarim asamasinda modeli harici bir bilgi kaynagina baglayarak gelistirir.

- Alignment ve Guvenlik Teknikleri: Alignment, bir yapay zeka modelinin davranisinin insan degerleri ve beklentileriyle uyumlu olmasini saglama, onu yardimci ve zararsiz kilma suresidir. En one cikan teknik, insan tercihlerine gore egitilmis bir "odul modeli"nin yapay zekanin ogrenme surecini yonlendirdigi, genellikle kararlilik icin Proximal Policy Optimization (PPO) gibi bir algoritma kullanan Reinforcement Learning from Human Feedback (RLHF)'dir. Ayri bir odul modeline olan ihtiyaci ortadan kaldiran Direct Preference Optimization (DPO) ve veri toplama isini daha da basitlestiren Kahneman-Tversky Optimization (KTO) gibi daha basit alternatifler ortaya cikmistir. Guvenli dagitimi saglamak icin, ciktilari filtrelemek ve zararli eylemleri gercek zamanli olarak engellemek amaciyla son bir guvenlik katmani olarak Guardrails uygulanir.

## Yapay Zeka Agent Yeteneklerinin Gelistirilmesi

- Yapay zeka agent'lari, cevrelerini algilayabilen ve hedeflere ulasmak icin otonom eylemler gerceklestirebilen sistemlerdir. Etkililikleri, saglam akil yurutme (reasoning) cerceveleriyle arttirilir.

- **Chain of Thought (CoT)**: Bu prompt teknigi, bir modeli son bir cevap vermeden once adim adim akil yurutmesini aciklamaya tesvik eder. Bu "yuksek sesle dusunme" sureci, genellikle karmasik akil yurutme gorevlerinde daha dogru sonuclara yol acar.

- **Tree of Thoughts (ToT)**: Tree of Thoughts, bir agent'in bir agacin dallari gibi birden fazla akil yurutme yolunu es zamanli olarak kesfettigi gelismis bir akil yurutme cercevesidir. Agent'in farkli dusunce hatlarini kendi kendine degerlendirmesine ve takip edilecek en umut verici olani secmesine olanak tanir ve karmasik problem cozmede daha etkili hale getirir.

**ReAct (Reason and Act)**: ReAct, akil yurutme ve eylemi bir dongu icinde birlestiren bir agent framework'udur. Agent once ne yapacagini "dusunur", ardindan bir arac kullanarak bir "eylem" gerceklestirir ve sonuc olarak elde edilen gozlemi bir sonraki dusuncesini bilgilendirmek icin kullanir; bu da onu karmasik gorevleri cozmede son derece etkili kilar.

- **Planlama (Planning)**: Bu, bir agent'in ust duzey bir hedefi daha kucuk, yonetilebilir alt gorevler dizisine bolme yetenegidir. Agent daha sonra bu adimlari sirasiyla yurutmek icin bir plan olusturur ve karmasik, cok adimli gorevleri yerine getirmesine olanak tanir.

- **Deep Research**: Deep research, bir agent'in bilgiyi yinelemeli olarak arayarak, bulgulari sentezleyerek ve yeni sorular belirleyerek bir konuyu derinlemesine otonom olarak kesfetme kapasitesini ifade eder. Bu, agent'in tek bir arama sorgusunun cok otesinde bir konu hakkinda kapsamli bir anlayis olusturmasina olanak tanir.

- **Critique Model**: Critique model, baska bir yapay zeka modelinin ciktisini incelemek, degerlendirmek ve geri bildirim saglamak icin egitilmis ozellestirilmis bir yapay zeka modelidir. Otomatik bir elestirmen olarak gorev yapar ve hatalari belirlemeye, akil yurutmeyi iyilestirmeye ve nihai ciktinin istenen kalite standardini karsilamasini saglamaya yardimci olur.

## Terimler Dizini

Bu terimler dizini Gemini Pro 2.5 kullanilarak olusturulmustur. Prompt ve akil yurutme adimlari, zaman tasarrufu faydalarini gostermek ve egitim amaciyla sonunda yer almaktadir.

### A

- A/B Testing - Bolum 3: Paralelizasyon (Parallelization)
- Action Selection - Bolum 20: Onceliklendirme (Prioritization)
- Adaptation - Bolum 9: Ogrenme ve Uyum Saglama (Learning and Adaptation)
- Adaptive Task Allocation - Bolum 16: Kaynak Odakli Optimizasyon (Resource-Aware Optimization)
- Adaptive Tool Use & Selection - Bolum 16: Kaynak Odakli Optimizasyon (Resource-Aware Optimization)
- Agent - Bir Yapay Zeka Sistemini Agent Yapan Nedir?
- Agent-Computer Interfaces (ACIs) - Ek B
- Agent-Driven Economy - Bir Yapay Zeka Sistemini Agent Yapan Nedir?
- Agent as a Tool - Bolum 7: Multi-Agent Is Birligi (Collaboration)
- Agent Cards - Bolum 15: Agent'lar Arasi Iletisim (A2A)
- Agent Development Kit (ADK) - Bolum 2: Yonlendirme (Routing), Bolum 3: Paralelizasyon (Parallelization), Bolum 4: Yansitma (Reflection), Bolum 5: Tool Use, Bolum 7: Multi-Agent Is Birligi (Collaboration), Bolum 8: Bellek Yonetimi (Memory Management), Bolum 12: Hata Yonetimi ve Kurtarma (Exception Handling and Recovery), Bolum 13: Human-in-the-Loop, Bolum 15: Agent'lar Arasi Iletisim (A2A), Bolum 16: Kaynak Odakli Optimizasyon (Resource-Aware Optimization), Bolum 19: Degerlendirme ve Izleme (Evaluation and Monitoring), Ek C
- Agent Discovery - Bolum 15: Agent'lar Arasi Iletisim (A2A)
- Agent Trajectories - Bolum 19: Degerlendirme ve Izleme (Evaluation and Monitoring)
- Agentic Tasarim Kaliplari (Design Patterns) - Giris
- Agentic RAG - Bolum 14: Bilgi Erisimi (Knowledge Retrieval) (RAG)
- Agentic Sistemler - Giris
- AI Co-scientist - Bolum 21: Kesif ve Kesfetme (Exploration and Discovery)
- Alignment - Sozluk
- AlphaEvolve - Bolum 9: Ogrenme ve Uyum Saglama (Learning and Adaptation)
- Analogies - Ek A
- Anomaly Detection - Bolum 19: Degerlendirme ve Izleme (Evaluation and Monitoring)
- Anthropic's Claude 4 Series - Ek B
- Anthropic's Computer Use - Ek B
- API Interaction - Bolum 10: Model Context Protocol (MCP)
- Artifacts - Bolum 15: Agent'lar Arasi Iletisim (A2A)
- Asynchronous Polling - Bolum 15: Agent'lar Arasi Iletisim (A2A)
- Audit Logs - Bolum 15: Agent'lar Arasi Iletisim (A2A)
- Automated Metrics - Bolum 19: Degerlendirme ve Izleme (Evaluation and Monitoring)
- Automatic Prompt Engineering (APE) - Ek A
- Autonomy - Giris
- A2A (Agent-to-Agent) - Bolum 15: Agent'lar Arasi Iletisim (A2A)

### B

- Behavioral Constraints - Bolum 18: Guardrails/Guvenlik Kaliplari (Safety Patterns)
- Browser Use - Ek B

### C

- Callbacks - Bolum 18: Guardrails/Guvenlik Kaliplari (Safety Patterns)
- Causal Language Modeling (CLM) - Sozluk
- Chain of Debates (CoD) - Bolum 17: Akil Yurutme Teknikleri (Reasoning Techniques)
- Chain-of-Thought (CoT) - Bolum 17: Akil Yurutme Teknikleri (Reasoning Techniques), Ek A
- Chatbots - Bolum 8: Bellek Yonetimi (Memory Management)
- ChatMessageHistory - Bolum 8: Bellek Yonetimi (Memory Management)
- Checkpoint and Rollback - Bolum 18: Guardrails/Guvenlik Kaliplari (Safety Patterns)
- Chunking - Bolum 14: Bilgi Erisimi (Knowledge Retrieval) (RAG)
- Clarity and Specificity - Ek A
- Client Agent - Bolum 15: Agent'lar Arasi Iletisim (A2A)
- Code Generation - Bolum 1: Prompt Chaining, Bolum 4: Yansitma (Reflection)
- Code Prompting - Ek A
- CoD (Chain of Debates) - Bolum 17: Akil Yurutme Teknikleri (Reasoning Techniques)
- CoT (Chain of Thought) - Bolum 17: Akil Yurutme Teknikleri (Reasoning Techniques), Ek A
- Collaboration - Bolum 7: Multi-Agent Is Birligi (Collaboration)
- Compliance - Bolum 19: Degerlendirme ve Izleme (Evaluation and Monitoring)
- Conciseness - Ek A
- Content Generation - Bolum 1: Prompt Chaining, Bolum 4: Yansitma (Reflection)
- Context Engineering - Bolum 1: Prompt Chaining
- Context Window - Sozluk
- Contextual Pruning & Summarization - Bolum 16: Kaynak Odakli Optimizasyon (Resource-Aware Optimization)
- Contextual Prompting - Ek A
- Contractor Model - Bolum 19: Degerlendirme ve Izleme (Evaluation and Monitoring)
- ConversationBufferMemory - Bolum 8: Bellek Yonetimi (Memory Management)
- Conversational Agents - Bolum 1: Prompt Chaining, Bolum 4: Yansitma (Reflection)
- Cost-Sensitive Exploration - Bolum 16: Kaynak Odakli Optimizasyon (Resource-Aware Optimization)
- CrewAI - Bolum 3: Paralelizasyon (Parallelization), Bolum 5: Tool Use, Bolum 6: Planlama (Planning), Bolum 7: Multi-Agent Is Birligi (Collaboration), Bolum 18: Guardrails/Guvenlik Kaliplari (Safety Patterns), Ek C
- Critique Agent - Bolum 16: Kaynak Odakli Optimizasyon (Resource-Aware Optimization)
- Critique Model - Sozluk
- Customer Support - Bolum 13: Human-in-the-Loop

### D

- Data Extraction - Bolum 1: Prompt Chaining
- Data Labeling - Bolum 13: Human-in-the-Loop
- Database Integration - Bolum 10: Model Context Protocol (MCP)
- DatabaseSessionService - Bolum 8: Bellek Yonetimi (Memory Management)
- Debate and Consensus - Bolum 7: Multi-Agent Is Birligi (Collaboration)
- Decision Augmentation - Bolum 13: Human-in-the-Loop
- Decomposition - Ek A
- Deep Research - Bolum 6: Planlama (Planning), Bolum 17: Akil Yurutme Teknikleri (Reasoning Techniques), Sozluk
- Delimiters - Ek A
- Denoising Objectives - Sozluk
- Dependencies - Bolum 20: Onceliklendirme (Prioritization)
- Diffusion Models - Sozluk
- Direct Preference Optimization (DPO) - Bolum 9: Ogrenme ve Uyum Saglama (Learning and Adaptation)
- Discoverability - Bolum 10: Model Context Protocol (MCP)
- Drift Detection - Bolum 19: Degerlendirme ve Izleme (Evaluation and Monitoring)
- Dynamic Model Switching - Bolum 16: Kaynak Odakli Optimizasyon (Resource-Aware Optimization)
- Dynamic Re-prioritization - Bolum 20: Onceliklendirme (Prioritization)

### E

- Embeddings - Bolum 14: Bilgi Erisimi (Knowledge Retrieval) (RAG)
- Embodiment - Bir Yapay Zeka Sistemini Agent Yapan Nedir?
- Energy-Efficient Deployment - Bolum 16: Kaynak Odakli Optimizasyon (Resource-Aware Optimization)
- Episodic Memory - Bolum 8: Bellek Yonetimi (Memory Management)
- Error Detection - Bolum 12: Hata Yonetimi ve Kurtarma (Exception Handling and Recovery)
- Error Handling - Bolum 12: Hata Yonetimi ve Kurtarma (Exception Handling and Recovery)
- Escalation Policies - Bolum 13: Human-in-the-Loop
- Evaluation - Bolum 19: Degerlendirme ve Izleme (Evaluation and Monitoring)
- Exception Handling - Bolum 12: Hata Yonetimi ve Kurtarma (Exception Handling and Recovery)
- Expert Teams - Bolum 7: Multi-Agent Is Birligi (Collaboration)
- Exploration and Discovery - Bolum 21: Kesif ve Kesfetme (Exploration and Discovery)
- External Moderation APIs - Bolum 18: Guardrails/Guvenlik Kaliplari (Safety Patterns)

### F

- Factored Cognition - Ek A
- FastMCP - Bolum 10: Model Context Protocol (MCP)
- Fault Tolerance - Bolum 18: Guardrails/Guvenlik Kaliplari (Safety Patterns)
- Few-Shot Learning - Bolum 9: Ogrenme ve Uyum Saglama (Learning and Adaptation)
- Few-Shot Prompting - Ek A
- Fine-tuning - Sozluk
- Formalized Contract - Bolum 19: Degerlendirme ve Izleme (Evaluation and Monitoring)
- Function Calling - Bolum 5: Tool Use, Ek A

### G

- Gemini Live - Ek B
- Gems - Ek A
- Generative Media Orchestration - Bolum 10: Model Context Protocol (MCP)
- Goal Setting - Bolum 11: Hedef Belirleme ve Izleme (Goal Setting and Monitoring)
- GoD (Graph of Debates) - Bolum 17: Akil Yurutme Teknikleri (Reasoning Techniques)
- Google Agent Development Kit (ADK) - Bolum 2: Yonlendirme (Routing), Bolum 3: Paralelizasyon (Parallelization), Bolum 4: Yansitma (Reflection), Bolum 5: Tool Use, Bolum 7: Multi-Agent Is Birligi (Collaboration), Bolum 8: Bellek Yonetimi (Memory Management), Bolum 12: Hata Yonetimi ve Kurtarma (Exception Handling and Recovery), Bolum 13: Human-in-the-Loop, Bolum 15: Agent'lar Arasi Iletisim (A2A), Bolum 16: Kaynak Odakli Optimizasyon (Resource-Aware Optimization), Bolum 19: Degerlendirme ve Izleme (Evaluation and Monitoring), Ek C
- Google Co-Scientist - Bolum 21: Kesif ve Kesfetme (Exploration and Discovery)
- Google DeepResearch - Bolum 6: Planlama (Planning)
- Google Project Mariner - Ek B
- Graceful Degradation - Bolum 12: Hata Yonetimi ve Kurtarma (Exception Handling and Recovery), Bolum 16: Kaynak Odakli Optimizasyon (Resource-Aware Optimization)
- Graph of Debates (GoD) - Bolum 17: Akil Yurutme Teknikleri (Reasoning Techniques)
- Grounding - Sozluk
- Guardrails - Bolum 18: Guardrails/Guvenlik Kaliplari (Safety Patterns)

### H

- Haystack - Ek C
- Hierarchical Decomposition - Bolum 19: Degerlendirme ve Izleme (Evaluation and Monitoring)
- Hierarchical Structures - Bolum 7: Multi-Agent Is Birligi (Collaboration)
- HITL (Human-in-the-Loop) - Bolum 13: Human-in-the-Loop
- Human-in-the-Loop (HITL) - Bolum 13: Human-in-the-Loop
- Human-on-the-loop - Bolum 13: Human-in-the-Loop
- Human Oversight - Bolum 13: Human-in-the-Loop, Bolum 18: Guardrails/Guvenlik Kaliplari (Safety Patterns)

### I

- In-Context Learning - Sozluk
- InMemoryMemoryService - Bolum 8: Bellek Yonetimi (Memory Management)
- InMemorySessionService - Bolum 8: Bellek Yonetimi (Memory Management)
- Input Validation/Sanitization - Bolum 18: Guardrails/Guvenlik Kaliplari (Safety Patterns)
- Instructions Over Constraints - Ek A
- Inter-Agent Communication (A2A) - Bolum 15: Agent'lar Arasi Iletisim (A2A)
- Intervention and Correction - Bolum 13: Human-in-the-Loop
- IoT Device Control - Bolum 10: Model Context Protocol (MCP)
- Iterative Prompting / Refinement - Ek A

### J

- Jailbreaking - Bolum 18: Guardrails/Guvenlik Kaliplari (Safety Patterns)

### K

- Kahneman-Tversky Optimization (KTO) - Sozluk
- Knowledge Retrieval (RAG) - Bolum 14: Bilgi Erisimi (Knowledge Retrieval) (RAG)

### L

- LangChain - Bolum 1: Prompt Chaining, Bolum 2: Yonlendirme (Routing), Bolum 3: Paralelizasyon (Parallelization), Bolum 4: Yansitma (Reflection), Bolum 5: Tool Use, Bolum 8: Bellek Yonetimi (Memory Management), Bolum 20: Onceliklendirme (Prioritization), Ek C
- LangGraph - Bolum 1: Prompt Chaining, Bolum 2: Yonlendirme (Routing), Bolum 3: Paralelizasyon (Parallelization), Bolum 4: Yansitma (Reflection), Bolum 5: Tool Use, Bolum 8: Bellek Yonetimi (Memory Management), Ek C
- Latency Monitoring - Bolum 19: Degerlendirme ve Izleme (Evaluation and Monitoring)
- Learned Resource Allocation Policies - Bolum 16: Kaynak Odakli Optimizasyon (Resource-Aware Optimization)
- Learning and Adaptation - Bolum 9: Ogrenme ve Uyum Saglama (Learning and Adaptation)
- LLM-as-a-Judge - Bolum 19: Degerlendirme ve Izleme (Evaluation and Monitoring)
- LlamaIndex - Ek C
- LoRA (Low-Rank Adaptation) - Sozluk
- Low-Rank Adaptation (LoRA) - Sozluk

### M

- Mamba - Sozluk
- Masked Language Modeling (MLM) - Sozluk
- MASS (Multi-Agent System Search) - Bolum 17: Akil Yurutme Teknikleri (Reasoning Techniques)
- MCP (Model Context Protocol) - Bolum 10: Model Context Protocol (MCP)
- Memory Management - Bolum 8: Bellek Yonetimi (Memory Management)
- Memory-Based Learning - Bolum 9: Ogrenme ve Uyum Saglama (Learning and Adaptation)
- MetaGPT - Ek C
- Microsoft AutoGen - Ek C
- Mixture of Experts (MoE) - Sozluk
- Model Context Protocol (MCP) - Bolum 10: Model Context Protocol (MCP)
- Modularity - Bolum 18: Guardrails/Guvenlik Kaliplari (Safety Patterns)
- Monitoring - Bolum 11: Hedef Belirleme ve Izleme (Goal Setting and Monitoring), Bolum 19: Degerlendirme ve Izleme (Evaluation and Monitoring)
- Multi-Agent Collaboration - Bolum 7: Multi-Agent Is Birligi (Collaboration)
- Multi-Agent System Search (MASS) - Bolum 17: Akil Yurutme Teknikleri (Reasoning Techniques)
- Multimodality - Sozluk
- Multimodal Prompting - Ek A

### N

- Negative Examples - Ek A
- Next Sentence Prediction (NSP) - Sozluk

### O

- Observability - Bolum 18: Guardrails/Guvenlik Kaliplari (Safety Patterns)
- One-Shot Prompting - Ek A
- Online Learning - Bolum 9: Ogrenme ve Uyum Saglama (Learning and Adaptation)
- OpenAI Deep Research API - Bolum 6: Planlama (Planning)
- OpenEvolve - Bolum 9: Ogrenme ve Uyum Saglama (Learning and Adaptation)
- OpenRouter - Bolum 16: Kaynak Odakli Optimizasyon (Resource-Aware Optimization)
- Output Filtering/Post-processing - Bolum 18: Guardrails/Guvenlik Kaliplari (Safety Patterns)

### P

- PAL (Program-Aided Language Models) - Bolum 17: Akil Yurutme Teknikleri (Reasoning Techniques)
- Parallelization - Bolum 3: Paralelizasyon (Parallelization)
- Parallelization & Distributed Computing Awareness - Bolum 16: Kaynak Odakli Optimizasyon (Resource-Aware Optimization)
- Parameter-Efficient Fine-Tuning (PEFT) - Sozluk
- PEFT (Parameter-Efficient Fine-Tuning) - Sozluk
- Performance Tracking - Bolum 19: Degerlendirme ve Izleme (Evaluation and Monitoring)
- Persona Pattern - Ek A
- Personalization - Bir Yapay Zeka Sistemini Agent Yapan Nedir?
- Planning - Bolum 6: Planlama (Planning), Sozluk
- Prioritization - Bolum 20: Onceliklendirme (Prioritization)
- Principle of Least Privilege - Bolum 18: Guardrails/Guvenlik Kaliplari (Safety Patterns)
- Proactive Resource Prediction - Bolum 16: Kaynak Odakli Optimizasyon (Resource-Aware Optimization)
- Procedural Memory - Bolum 8: Bellek Yonetimi (Memory Management)
- Program-Aided Language Models (PAL) - Bolum 17: Akil Yurutme Teknikleri (Reasoning Techniques)
- Project Astra - Ek B
- Prompt - Sozluk
- Prompt Chaining - Bolum 1: Prompt Chaining
- Prompt Engineering - Ek A
- Proximal Policy Optimization (PPO) - Bolum 9: Ogrenme ve Uyum Saglama (Learning and Adaptation)
- Push Notifications - Bolum 15: Agent'lar Arasi Iletisim (A2A)

### Q

- QLoRA - Sozluk
- Quality-Focused Iterative Execution - Bolum 19: Degerlendirme ve Izleme (Evaluation and Monitoring)

### R

- RAG (Retrieval-Augmented Generation) - Bolum 8: Bellek Yonetimi (Memory Management), Bolum 14: Bilgi Erisimi (Knowledge Retrieval) (RAG), Ek A
- ReAct (Reason and Act) - Bolum 17: Akil Yurutme Teknikleri (Reasoning Techniques), Ek A, Sozluk
- Reasoning - Bolum 17: Akil Yurutme Teknikleri (Reasoning Techniques)
- Reasoning-Based Information Extraction - Bolum 10: Model Context Protocol (MCP)
- Recovery - Bolum 12: Hata Yonetimi ve Kurtarma (Exception Handling and Recovery)
- Recurrent Neural Network (RNN) - Sozluk
- Reflection - Bolum 4: Yansitma (Reflection)
- Reinforcement Learning - Bolum 9: Ogrenme ve Uyum Saglama (Learning and Adaptation)
- Reinforcement Learning from Human Feedback (RLHF) - Sozluk
- Reinforcement Learning with Verifiable Rewards (RLVR) - Bolum 17: Akil Yurutme Teknikleri (Reasoning Techniques)
- Remote Agent - Bolum 15: Agent'lar Arasi Iletisim (A2A)
- Request/Response (Polling) - Bolum 15: Agent'lar Arasi Iletisim (A2A)
- Resource-Aware Optimization - Bolum 16: Kaynak Odakli Optimizasyon (Resource-Aware Optimization)
- Retrieval-Augmented Generation (RAG) - Bolum 8: Bellek Yonetimi (Memory Management), Bolum 14: Bilgi Erisimi (Knowledge Retrieval) (RAG), Ek A
- RLHF (Reinforcement Learning from Human Feedback) - Sozluk
- RLVR (Reinforcement Learning with Verifiable Rewards) - Bolum 17: Akil Yurutme Teknikleri (Reasoning Techniques)
- RNN (Recurrent Neural Network) - Sozluk
- Role Prompting - Ek A
- Router Agent - Bolum 16: Kaynak Odakli Optimizasyon (Resource-Aware Optimization)
- Routing - Bolum 2: Yonlendirme (Routing)

### S

- Safety - Bolum 18: Guardrails/Guvenlik Kaliplari (Safety Patterns)
- Scaling Inference Law - Bolum 17: Akil Yurutme Teknikleri (Reasoning Techniques)
- Scheduling - Bolum 20: Onceliklendirme (Prioritization)
- Self-Consistency - Ek A
- Self-Correction - Bolum 4: Yansitma (Reflection), Bolum 17: Akil Yurutme Teknikleri (Reasoning Techniques)
- Self-Improving Coding Agent (SICA) - Bolum 9: Ogrenme ve Uyum Saglama (Learning and Adaptation)
- Self-Refinement - Bolum 17: Akil Yurutme Teknikleri (Reasoning Techniques)
- Semantic Kernel - Ek C
- Semantic Memory - Bolum 8: Bellek Yonetimi (Memory Management)
- Semantic Similarity - Bolum 14: Bilgi Erisimi (Knowledge Retrieval) (RAG)
- Separation of Concerns - Bolum 18: Guardrails/Guvenlik Kaliplari (Safety Patterns)
- Sequential Handoffs - Bolum 7: Multi-Agent Is Birligi (Collaboration)
- Server-Sent Events (SSE) - Bolum 15: Agent'lar Arasi Iletisim (A2A)
- Session - Bolum 8: Bellek Yonetimi (Memory Management)
- SICA (Self-Improving Coding Agent) - Bolum 9: Ogrenme ve Uyum Saglama (Learning and Adaptation)
- SMART Goals - Bolum 11: Hedef Belirleme ve Izleme (Goal Setting and Monitoring)
- State - Bolum 8: Bellek Yonetimi (Memory Management)
- State Rollback - Bolum 12: Hata Yonetimi ve Kurtarma (Exception Handling and Recovery)
- Step-Back Prompting - Ek A
- Streaming Updates - Bolum 15: Agent'lar Arasi Iletisim (A2A)
- Structured Logging - Bolum 18: Guardrails/Guvenlik Kaliplari (Safety Patterns)
- Structured Output - Bolum 1: Prompt Chaining, Ek A
- SuperAGI - Ek C
- Supervised Fine-Tuning (SFT) - Sozluk
- Supervised Learning - Bolum 9: Ogrenme ve Uyum Saglama (Learning and Adaptation)
- System Prompting - Ek A

### T

- Task Evaluation - Bolum 20: Onceliklendirme (Prioritization)
- Text Similarity - Bolum 14: Bilgi Erisimi (Knowledge Retrieval) (RAG)
- Token Usage - Bolum 19: Degerlendirme ve Izleme (Evaluation and Monitoring)
- Tool Use - Bolum 5: Tool Use, Ek A
- Tool Use Restrictions - Bolum 18: Guardrails/Guvenlik Kaliplari (Safety Patterns)
- ToT (Tree of Thoughts) - Bolum 17: Akil Yurutme Teknikleri (Reasoning Techniques), Ek A, Sozluk
- Transformers - Sozluk
- Tree of Thoughts (ToT) - Bolum 17: Akil Yurutme Teknikleri (Reasoning Techniques), Ek A, Sozluk

### U

- Unsupervised Learning - Bolum 9: Ogrenme ve Uyum Saglama (Learning and Adaptation)
- User Persona - Ek A

### V

- Validation - Bolum 3: Paralelizasyon (Parallelization)
- Vector Search - Bolum 14: Bilgi Erisimi (Knowledge Retrieval) (RAG)
- VertexAiRagMemoryService - Bolum 8: Bellek Yonetimi (Memory Management)
- VertexAiSessionService - Bolum 8: Bellek Yonetimi (Memory Management)
- Vibe Coding - Ek B
- Visual Perception - Ek B

### W

- Webhooks - Bolum 15: Agent'lar Arasi Iletisim (A2A)

### Z

- Zero-Shot Learning - Bolum 9: Ogrenme ve Uyum Saglama (Learning and Adaptation)
- Zero-Shot Prompting - Ek A

## Prompt

Asagida bu terimler dizinini olusturmak icin kullanilan prompt yer almaktadir.

> *Do you read <https://docs.google.com/document/d/1rsaK53T3Lg5KoGwvf8ukOUvbELRtH-V0LnOIFDxBryE/edit?tab=t.0> and all the related documents in the first page Please extract all the titles for each chapter. and print them. Then process the content of all the individual chapters, and create a detailed index used for publishing, a list of words or phrases ('headings') and associated pointers ('locators') to where useful material relating to that heading can be found in a document or collection of documents. I don't want a sample index. I want the full index, with 100 index terms*

## Gemini 2.5: Akil Yurutme Adimlari

### Dizin Olusturmaya Baslangiç

Google Doc'u okuyarak sureci baslattim. Suanda kullanicinin istegini anlamaya odaklaniyorum: kapsamli bir dizin olusturmak icin bolum basliklarini cikarmak. Belgeyi dikkatlice inceliyorum, bolum aralarini belirtecek net yapisal unsurlari ariyorum. Dizin olusturma surecini yonlendirecek tutarli bicimlendirme veya anahtar kelimeleri belirlemeyi umuyorum.

### Dizin Cikarma Surecinin Tanimlanmasi

Simdi goreve tamamen odaklandim. Kullanicinin istegini uygulanabilir adimlara ayirdim. Ilk odagim ana Google Doc'a erismek icin Workspaces'i kullanmak. Bunu takiben, ilgili belgeleri bulmak ve almak icin belgeyi ayristirip ayni araci kullanacagim. Son olarak, tum belgelerden tum bolum basliklarini cikaracak ve kapsamli bir dizin olusturacagim. Detayli sureci planladim.

### Cikarma Stratejisinin Iyilestirilmesi

Kullanicinin talimatlari acik: bir Google Doc, ilgili belgeler okunacak ve kapsamli bir dizin olusturulacak. Cok adimli bir plan gelistirdim. Ilk olarak, Workspaces ana Google Doc'a erisecek. Ardindan, ilgili belgeleri bulmak ve okumak icin belgeyi ayristirip yine Workspaces'i kullanacagim. Simdi basliklari cikarmaya ve gerekli terimlerle kapsamli dizini olusturmaya odaklaniyorum. Kullanicinin kapsamli bir dizin icin ozel taleplerine dogruluk onceligi veriyorum.

#### 1. Kullanici niyetinin belirlenmesi:

Kullanicinin Google Doc ve ilgili belgelerden bir bolum basligi listesi ve kapsamli dizin istedigini belirledim. Simdi bu cikarma ve dizinleme sureci icin en etkili yontemi bulmam gerekiyor. Gorevi kolaylastirmak icin potansiyel API islevselliklerini arastiriyorum ve farkli belge yaplarini yonetmek icin en iyi stratejiyi degerlendirmem gerekecek.

#### 2. Arac Kullaniminin Degerlendirilmesi

Duzeli ifade kullanarak ana belgeden bolum URL'lerini cikarttim. Simdi her bolumun gercek icerigini almak icin Workspaces'i kullanmaya hazirim. Her bolumun metnine sahip oldugumda, dizinleme islemine gecerim.

### Bolum icerigine erisim:

Her bolumun URL'lerini ana belgeden basariyla belirledim ve artik Workspaces ile kullanabilirim. Bir sonraki adimim bu URL'lerden icerigi almak olacak, bu da dizin olusturmami saglayacaktir. Verimlilíge odaklaniyorum, bu bilgiyi hizla islemeyi hedefliyorum.

### Bolum Iceriginin Alinmasi

Her bolumun URL'lerini ana belgeden basariyla belirledim ve Workspaces'i kullanmaya hazirim. Planim bu URL'leri cikartmak, verimlilik icin cagrilari toplu yapmak ve ardindan istenen dizini olusturmak icin alinan icerigi islemektir. Bu, istendigi gibi en az 100 terimli kapsamli ve dogru bir sonuca zemin hazirlayarak tum ilgili bilgilerin yakalanmasini saglar.

### URL Alimini Baslatma

Simdi ana belgeden bolum URL'lerini basariyla cikardim. Suanda her bolumun icerigini almak icin Workspaces aracina cagrilar ayarliyorum. Amac, dizinleme icin gerekli metni elde etmektir. Bu bilgi daha sonra istendigi gibi en az 100 terimli dizinin olusturulmasini kolaylastiracaktir.

### Bolum Cikarma Isleminin Baslatilmasi

Ana belgeden bolum URL'lerini basariyla belirledim ve cikardim, yukarda dahil edilmistir. Simdi her URL icin bolum icerigini elde etmek uzere Workspaces'i kullanmaya devam ediyorum. Amac, dizinleme icin gerekli metni elde etmektir. Bu bilgi daha sonra istendigi gibi en az 100 terimli dizinin olusturulmasini kolaylastiracaktir. Bu bilgiyi almaya basladim.

### Bolum Aliminin Koordinasyonu

Bolum URL'lerini cikardim ve Workspaces'e cagri baslattim. Suanda her bolumun icerigini aliyorum. Sorunsuz bir surec saglamak icin hiz sinirlandirma sorunlarini onlemek amaciyla cagrilari toplulastiriyorum. Bu, dizin icin gereken metni verimli bir sekilde derlemememi saglayacaktir.

### Kullanici Isteginin Cozumlenmesi

Kullanicinin ihtiyacini belirledim. Iki temel cikti gerektiriyorlar: birincisi, Google Docs'tan cikartilmis kapsamli bir bolum basliklari listesi ve ikincisi, en az yuz temel terimi iceren ayrintili bir dizin. Basliklari cikarma sureci basit gorunurken, dizinin derlenmesi daha nüansli bir analiz icerecektir.

### Baslik Cikarma ve Dizinleme

Kullanicinin ihtiyacini basariyla belirledim: saglanan belgelerden bolum basliklarini cikarmak ve kapsamli bir dizin derlemek. Ana belge ve bolumleri dahil 31 Google Docs'un icerigini aldim. Ek arac gerekmedigi dogrulandim. Planim iki adim iceriyor: birincisi, belge dosya adlarindan bolum basliklarini cikarmak ve ikincisi, anahtar terimler ve bolum isaretcileri ile dizini olusturmak icin metni titizlikle islemek.

### Cikarma Planinin Olusturulmasi

Kullanicinin istegini ele almak icin yaklasisinmi iyilestirdim. Simdi kesin bir plan formule ettim. Birinci olarak, 31 alinan belgenin dosya adlarindan bolum basliklarini derleyecegim. Ikinci olarak ve daha karmasik olarak, 100 girdiyi asan kapsamli, alfabetik sirada duzenli bir dizin olusturmak icin icerigi titizlikle analiz edecegim. Cikarma ve dizinleme stratejimi sonuclandirdim ve simdi uygulamaya baslayabilirim.

### Cikarma Stratejisinin Sekillenmesi

Yaklasinimim iyi tanimlanmis durumda. 31 alinan belgenin dosya adlarindan bolum basliklarini derleyecegim. Ardindan, 100 girdiyi asan alfabetik olarak duzenlenmis bir dizin olusturmak icin icerigi titizlikle analiz edecegim. Cikarma ve dizinleme stratejisini sonuclandirdim ve simdi uygulamaya baslayabilirim. Kullanicinin, Agentic Design Patterns serisindeki cesitli bolum ve eklerdeki icerigi kapsayan ayrintili bir dizin hedefi artik ulasılabilir durumda. Yalnizca ornek bir dizin degil, kapsamli bir yanit sunmaya odaklanacagim.

### Yaklasimin Tanimlanmasi

Kullanicinin ihtiyacini netlestirdim. Belge dosya adlarindan bolum basliklarini cikartacagim. Bunu takiben, 100 girdiyi asan girisleri alfabetik siralayla olusturup bolum konumlarini not alarak dikkatli bir dizin olusturacagim. Dizinleme ve cikarma surecine baslamaya hazirim.
