# Ek C - Agentic Framework'lere Hizli Bakis

## LangChain

LangChain, LLM'ler tarafindan desteklenen uygulamalar gelistirmek icin bir framework'tur. Temel gucu, bilesenleri bir zincire "borulama" imkani sunan LangChain Expression Language (LCEL) dilinde yatar. Bu, bir adimin ciktisinin bir sonraki adimin girdisi haline geldigi acik, dogrusal bir dizi olusturur. Yonlu Dongusel Olmayan Graflar (DAG) olan is akislari icin insa edilmistir, yani surec dongular olmaksizin tek yonde ilerler.

Kullanim alanlari:

* Basit RAG: Bir belge al, bir prompt olustur, LLM'den bir cevap al.
* Ozetleme: Kullanici metnini al, bir ozetleme prompt'una aktar ve ciktiyi dondur.
* Cikarma: Bir metin blogundan yapilandirilmis veri (JSON gibi) cikar.

Python

```python
# A simple LCEL chain conceptually # (This is not runnable code, just illustrates the flow)
chain = prompt | model | output_parse
```

## LangGraph

LangGraph, daha gelismis agentic sistemleri ele almak icin LangChain uzerine insa edilmis bir kutuphanedir. Is akisinizi dugumler (fonksiyonlar veya LCEL zincirleri) ve kenarlar (kosullu mantik) iceren bir graf olarak tanimlamaniza olanak tanir. Temel avantaji, uygulamanin bir gorev tamamlanana kadar esnek bir sirada dongu yapmasina, yeniden denemesine veya arac cagirmasina olanak taniyan donguler olusturabilmesidir. Uygulama durumunu acikca yonetir; bu durum dugumler arasinda aktarilir ve surec boyunca guncellenir.

Kullanim alanlari:

* Multi-Agent Sistemler: Bir gozetmen agent, gorevleri uzmanlasmis calisaan agent'lara yonlendirir ve hedef (Goal) karsilanana kadar potansiyel olarak dongu yapar.
* Planla-ve-Yurutt Agent'lari: Bir agent bir plan olusturur, bir adim yurutur ve ardindan sonuca dayali olarak plani guncellemek icin geri doner.
* Human-in-the-Loop: Graf, bir sonraki dugume hangi yoldan gidilecegine karar vermeden once insan girdisini bekleyebilir.

| Ozellik | LangChain | LangGraph |
| :---- | :---- | :---- |
| Temel Soyutlama | Zincir (LCEL kullanarak) | Dugum Grafi |
| Is Akisi Turu | Dogrusal (Yonlu Dongusel Olmayan Graf) | Dongusel (Dongulu Graflar) |
| Durum Yonetimi | Genellikle calistirma basina durumsuz | Acik ve kalici durum nesnesi |
| Birincil Kullanim | Basit, ongorerulebilir diziler | Karmasik, dinamik, durumlu agent'lar |

### Hangisini Secmelisiniz?

* Uygulamaniz net, ongorerulebilir ve dogrusal bir adim akisina sahipse **LangChain**'i secin. Sureci A'dan B'ye, C'ye geri donme ihtiyaci olmadan tanimlayabiliyorsaniz, LCEL ile LangChain mukemmel aractir.
* Uygulamanizin akil yurutme, planlama veya bir dongu icinde calismasi gerekiyorsa **LangGraph**'i secin. Agent'inizin araclar kullanmasi, sonuclari yansitmasi ve potansiyel olarak farkli bir yaklasimla yeniden denemesi gerekiyorsa, LangGraph'in dongusel ve durumlu yapisina ihtiyaciniz vardir.

```python
# Graph state
class State(TypedDict):
    topic: str
    joke: str
    story: str
    poem: str
    combined_output: str


# Nodes
def call_llm_1(state: State):
    """First LLM call to generate initial joke"""
    msg = llm.invoke(f"Write a joke about {state['topic']}")
    return {"joke": msg.content}


def call_llm_2(state: State):
    """Second LLM call to generate story"""
    msg = llm.invoke(f"Write a story about {state['topic']}")
    return {"story": msg.content}


def call_llm_3(state: State):
    """Third LLM call to generate poem"""
    msg = llm.invoke(f"Write a poem about {state['topic']}")
    return {"poem": msg.content}


def aggregator(state: State):
    """Combine the joke and story into a single output"""
    combined = f"Here's a story, joke, and poem about {state['topic']}!\n\n"
    combined += f"STORY:\n{state['story']}\n\n"
    combined += f"JOKE:\n{state['joke']}\n\n"
    combined += f"POEM:\n{state['poem']}"
    return {"combined_output": combined}


# Build workflow
parallel_builder = StateGraph(State)

# Add nodes
parallel_builder.add_node("call_llm_1", call_llm_1)
parallel_builder.add_node("call_llm_2", call_llm_2)
parallel_builder.add_node("call_llm_3", call_llm_3)
parallel_builder.add_node("aggregator", aggregator)

# Add edges to connect nodes
parallel_builder.add_edge(START, "call_llm_1")
parallel_builder.add_edge(START, "call_llm_2")
parallel_builder.add_edge(START, "call_llm_3")
parallel_builder.add_edge("call_llm_1", "aggregator")
parallel_builder.add_edge("call_llm_2", "aggregator")
parallel_builder.add_edge("call_llm_3", "aggregator")
parallel_builder.add_edge("aggregator", END)

parallel_workflow = parallel_builder.compile()

# Show workflow
display(Image(parallel_workflow.get_graph().draw_mermaid_png()))

# Invoke
state = parallel_workflow.invoke({"topic": "cats"})
print(state["combined_output"])
```

Bu kod, paralel olarak calisan bir LangGraph is akisi tanimlar ve calistirir. Temel amaci, verilen bir konu hakkinda es zamanli olarak bir espri, bir hikaye ve bir siir uretmek ve ardindan bunlari tek, formatlanmis bir metin ciktisinda birlestirmektir.

## Google ADK

Google'in Agent Development Kit (ADK), birden fazla etkilesen yapay zeka agent'indan olusan uygulamalar olusturmak ve dagitmak icin ust duzey, yapilandirilmis bir framework saglar. Bir agent'in ic mantigi icin temel yapi taslarini saglamak yerine, agent is birligi (Collaboration) orkestrasyonu icin daha keskin goruslu ve uretim odakli bir sistem sunarak LangChain ve LangGraph'tan farklilasinir.

LangChain en temel duzeyde calisir ve bir modeli cagirma ve ciktisini ayristirma gibi operasyon dizileri olusturmak icin bilesenleri ve standartlastirilmis arayuzleri sunar. LangGraph bunu daha esnek ve guclu bir kontrol akisi sunarak genisletir; bir agent'in is akisini durumlu bir graf olarak ele alir. LangGraph kullanarak, bir gelistirici dugumler (fonksiyonlar veya araclar) ve yurutme yolunu belirleyen kenarlari acikca tanimlar. Bu graf yapisi, sistemin dugumler arasinda aktarilan acikca yonetilen bir durum nesnesine dayali olarak dongu yapabilecegi, gorevleri yeniden deneyebilecegi ve kararlar alabilecegi karmasik, dongusel akil yurutmeye olanak tanir. Gelistiriciye tek bir agent'in dusunce sureci uzerinde ince ayarli kontrol veya ilk ilkelerden coklu agent sistemi olusturma yetenegi saglar.

Google'in ADK'si bu dusuk seviyeli graf insasinin buyuk bolumunu soyutlar. Gelistiriciden her dugum ve kenari tanimlamasini istemek yerine, coklu agent etkilesimi icin onceden olusturulmus mimari kaliplar saglar. Ornegin, ADK'da farkli agent'lar arasindaki kontrol akisini otomatik olarak yoneten SequentialAgent veya ParallelAgent gibi yerlesik agent turleri vardir. Genellikle bir birincil agent'in gorevleri uzmanlasmis alt agent'lara devrettigi bir agent "ekibi" kavrami etrafinda mimarilenmistir. Durum ve oturum yonetimi framework tarafindan daha ortuk bir sekilde ele alinir ve LangGraph'in acik durum aktarimindan daha uyumlu ancak daha az detayli bir yaklasim saglar. Dolayisiyla, LangGraph size tek bir robotun veya bir ekibin karmasik kablolamasini tasarlamak icin ayrintili araclar verirken, Google'in ADK'si size birlikte nasil calisacaklarini zaten bilen bir robot filosu olusturmak ve yonetmek icin tasarlanmis bir fabrika montaj hatti verir.

```python
from google.adk.agents import LlmAgent
from google.adk.tools import google_Search

dice_agent = LlmAgent(
    model="gemini-2.0-flash-exp",
    name="question_answer_agent",
    description="A helpful assistant agent that can answer questions.",
    instruction="""Respond to the query using google search""",
    tools=[google_search],
)
```

Bu kod, arama ile guclendiirilmis bir agent olusturur. Bu agent bir soru aldiginda, sadece onceden mevcut bilgisine guuenmeyecektir. Bunun yerine, talimatlarini takip ederek web'den ilgili, gercek zamanli bilgi bulmak icin Google Search aracini kullanacak ve ardından bu bilgiyi cevabini olusturmak icin kullanacaktir.

## Crew.AI

CrewAI, is birlikci roller ve yapilandirilmis surecler uzerine odaklanarak coklu agent sistemleri olusturmak icin bir orkestrasyon framework'u sunar. Temel arac takimlarindan daha yuksek bir soyutlama duzeyinde calisir ve bir insan ekibini yansitan kavramsal bir model saglar. Mantiigin ayrintili akisini bir graf olarak tanimlamak yerine, gelistirici aktoleri ve gorevlendirmelerini tanimlar ve CrewAI etkilesimlerini yonetir.

Bu framework'un temel bilesenleri Agent'lar, Gorevler ve Ekipdir. Bir Agent yalnizca islevi ile degil, belirli bir rol, bir hedef (Goal) ve bir arka hikaye dahil olmak uzere bir kisi ile tanimlanir; bu da davranisini ve iletisim tarzini yonlendirir. Bir Gorev, belirli bir Agent'a atanan, net bir aciklamasi ve beklenen ciktisi olan ayri bir is birimidir. Ekip, Agent'lari ve Gorevler listesini iceren uyumlu birimdir ve onceden tanimlanmis bir Surec yurutur. Bu surec, tipik olarak sirali (bir gorevin ciktisinin sira dahilindeki bir sonrakinin girdisi haline geldigi) veya hiyerarsik (yonetici benzeri bir agent'in gorevleri devrettigi ve diger agent'lar arasinda is akisini koordine ettigi) olan is akisini belirler.

Diger framework'lerle karsilastirildigindan, CrewAI farkli bir konumda yer alir. Bir gelistiricinin her dugum ve kosullu kenari birbirine bagladigi LangGraph'in dusuk seviyeli, acik durum yonetimi ve kontrol akisindan uzaklasinir. Bir durum makinesi insa etmek yerine, gelistirici bir ekip sartnamesi tasarlar. Google'in ADK'si tum agent yasam dongusu icin kapsamli, uretim odakli bir platform sunarken, CrewAI ozellikle agent is birligi mantiiina ve bir uzmanlar ekibinin simule edilmesine odaklanir.

```python
@crew
def crew(self) -> Crew:
   """Creates the research crew"""
   return Crew(
     agents=self.agents,
     tasks=self.tasks,
     process=Process.sequential,
     verbose=True,
   )
```

Bu kod, yapay zeka agent'larindan olusan bir ekip icin sirali bir is akisi olusturur; burada agent'lar ilerleme durumlarini izlemek icin ayrintili gunluk kaydı etkinlestirilmis halde belirli bir sirada gorevler listesiyle ilgilenir.

## Diger Agent Gelistirme Framework'leri

**Microsoft AutoGen**: AutoGen, konusma yoluyla gorevleri cozen birden fazla agent'i orkestre etme uzerine odaklanan bir framework'tur. Mimarisi, farkli yeteneklere sahip agent'larin etkilesim kurmasina olanak taniyarak karmasik problem ayristirma ve is birlikci cozume imkan verir. AutoGen'in temel avantaji, dinamik ve karmasik coklu agent etkilesimlerini destekleyen esnek, konusma odakli yaklasimidir. Ancak bu konusma paradigmasi daha az ongorerulebilir yurutme yollarina yol acabilir ve gorevlerin verimli bir sekilde yakinsamasini saglamak icin sofistike prompt muhendisligi gerektirebilir.

**LlamaIndex**: LlamaIndex, temelde buyuk dil modellerini harici ve ozel veri kaynaklariyla baglamak icin tasarlanmis bir veri framework'udur. RAG gerceklestirebilen bilgili agent'lar olusturmak icin gerekli olan sofistike veri alma ve erisim boru hatlari olusturmada mukemmeldir. Veri indeksleme ve sorgulama yetenekleri, baglam fakindalikli agent'lar olusturmak icin son derece guclu olsa da, karmasik agentic kontrol akisi ve coklu agent orkestrasyonu icin yerel araclari, agent-oncelikli framework'lere kiyasla daha az gelismistir. LlamaIndex, temel teknik zorluk veri erisimi ve sentezi oldugunda en uygunudur.

**Haystack**: Haystack, dil modelleri tarafindan desteklenen olceklenebilir ve uretim-hazir arama sistemleri olusturmak icin tasarlanmis acik kaynakli bir framework'tur. Mimarisi, belge erisimi, soru cevaplama ve ozetleme icin boru hatlari olusturan moduler, birlikte calisabilir dugumlerden olusur. Haystack'in temel gucu, buyuk olcekli bilgi erisim gorevleri icin performans ve olceklenebilirlige odaklanmasidir ve bu onu kurumsal sinif uygulamalar icin uygun kilar. Olasi bir odun verme, arama boru hatlari icin optimize edilmis tasariminin son derece dinamik ve yaratici agentic davranislari uygulamak icin daha katii olabilecegidir.

**MetaGPT**: MetaGPT, onceden tanimlanmis bir Standart Isletme Prosedulleri (SOP) kumesine dayali olarak roller ve gorevler atayarak coklu agent sistemi uygular. Bu framework, agent is birliigini bir yazilim gelistirme sirketini taklit edecek sekilde yapilandirir; agent'lar karmasik gorevleri tamamlamak icin urun yooneticileri veya muhendisler gibi roller ustlenir. Bu SOP odakli yaklasim, ozellikle kod uretimi gibi uzmanlasmis alanlar icin onemli bir avantaj olan son derece yapilandirilmis ve tutarli ciktilar uretir. Framework'un temel sinirlamasi, yuksek derecede uzmanlasmasi olup, temel tasariminin disindaki genel amacli agentic gorevler icin daha az uyarlanabilir olmasini saglar.

**SuperAGI**: SuperAGI, otonom agent'lar icin eksiksiz bir yasam dongusu yonetim sistemi saglamak uzere tasarlanmis acik kaynakli bir framework'tur. Agent saglama, izleme (Monitoring) ve grafik arayuz gibi ozellikler icerir ve agent yurutumunun guvenilirligini artirmayi amaclar. Temel faydasi, donguleme gibi yaygin basarisizlik modlarini ele almak ve agent performansina gozlemlenebilirlik saglamak icin yerlesik mekanizmalara sahip uretim-hazirliigi odagidir. Olasi bir dezavantaj, kapsamli platform yaklasiminin daha hafif, kutuphane tabanli bir framework'e kiyasla daha fazla karmasiklik ve ek yuk getirebilmesidir.

**Semantic Kernel**: Microsoft tarafindan gelistirilen Semantic Kernel, bir "plugin" ve "planner" sistemi araciliyla buyuk dil modellerini geleneksel programlama koduyla entegre eden bir SDK'dir. Bir LLM'nin yerel fonksiyonlari cagirmasina ve is akislarini orkestre etmesine olanak taniyarak, modeli daha buyuk bir yazilim uygulamasi icinde etkili bir sekilde bir akil yurutme motoru olarak ele alir. Temel gucu, ozellikle .NET ve Python ortamlarinda mevcut kurumsal kod tabanlariyla sorunsuz entegrasyonudur. Plugin ve planner mimarisinin kavramsal yuku, daha basit agent framework'lerine kiyasla daha dik bir ogrenme egrisi sunabilir.

**Strands Agents:** Yapay zeka agent'lari olusturmak ve calistirmak icin model odakli bir yaklasim kullanan bir AWS hafif ve esnek SDK'sidir. Basit ve olceklenebilir olacak sekilde tasarlanmis olup, temel konusma asistanlarindan karmasik coklu agent otonom sistemlere kadar her seyi destekler. Framework model-agnostiktir, cesitli LLM saglayicilari icin genis destek sunar ve harici araclara kolay erisim icin MCP ile yerel entegrasyon icerir. Temel avantaji basitligi ve esnekliigidir; baslangiict kolay, ozellestirilebilir bir agent dongusune sahiptir. Olasi bir odun verme, hafif tasariminin, daha kapsamli framework'lerin kutudan cikar cikmaz saglayabilecegi gelismis izleme veya yasam dongusu yonetim sistemleri gibi cevredeki operasyonel altyapinin daha fazlasini gelistiricilerin insa etmesini gerektirebilmesidir.

## Sonuc

Agentic framework'ler ekolojisi, agent mantiiini tanimlamak icin dusuk seviyeli kutuphanelerden coklu agent is birligini orkestre etmek icin ust duzey platformlara kadar cesitli bir arac yelpazesi sunmaktadir. Temel duzeyde, LangChain basit, dogrusal is akislarini etkinlestirirken, LangGraph daha karmasik akil yurutme icin durumlu, dongusel graflar sunar. CrewAI ve Google ADK gibi ust duzey framework'ler odagi onceden tanimlanmis rollere sahip agent ekiplerini orkestre etmeye kaydirirken, LlamaIndex gibi digerleri veri yogun uygulamalarda uzmanlasmistir. Bu cesitlilik, gelistiricilere graf tabanli sistemlerin detayli kontrolu ile daha keskin goruslu platformlarin kolaylastirilmis gelistirmesi arasinda temel bir odun verme sunar. Sonuc olarak, dogru framework'u secmek, uygulamanin basit bir dizi, dinamik bir akil yurutme dongusu veya yonetilen bir uzmanlar ekibi gerektirip gerektirmedigine baglidir. Nihayetinde, bu evrilen ekosistem, gelistiricilerin projelerinin talep ettigi kesin soyutlama duzeyini secerek giderek daha sofistike yapay zeka sistemleri olusturmalarini guclendirir.

Kaynaklar

1. LangChain, [https://www.langchain.com/](https://www.langchain.com/)
2. LangGraph, [https://www.langchain.com/langgraph](https://www.langchain.com/langgraph)
3. Google's ADK, [https://google.github.io/adk-docs/](https://google.github.io/adk-docs/)
4. Crew.AI, [https://docs.crewai.com/en/introduction](https://docs.crewai.com/en/introduction)
