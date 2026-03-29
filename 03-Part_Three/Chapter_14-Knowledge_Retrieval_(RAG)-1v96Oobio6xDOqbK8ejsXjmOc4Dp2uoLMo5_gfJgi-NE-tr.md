# Bolum 14: Bilgi Erisimi (Knowledge Retrieval) — RAG

LLM'ler insan benzeri metin uretmede onemli yetenekler sergiler. Ancak bilgi tabanlari genellikle egitildikleri verilerle sinirlidir ve bu durum gercek zamanli bilgilere, belirli sirket verilerine veya son derece uzmanlasmis ayrintilara erisimlerini kisitlar. Bilgi Erisimi (Knowledge Retrieval), yani RAG (Retrieval Augmented Generation), bu sinirlamayi ele alir. RAG, LLM'lerin harici, guncel ve bagllama ozgu bilgilere erismesini ve bunlari entegre etmesini saglayarak ciktilarinin dogrulugunu, ilgilligini ve olgusal temelini guclendirir.

Yapay zeka agent'lari icin bu hayati onem tasir; cunku eylemlerini ve yanitlarini statik egitimlerinin otesinde gercek zamanli, dogrulanabilir veriye dayandirmalarini saglar. Bu yetenek, belirli bir soruyu yanitlamak icin en guncel sirket politikalarina erismek veya siparis vermeden once mevcut envanteri kontrol etmek gibi karmasik gorevleri dogru bir sekilde yerine getirmelerini mumkun kilar. Harici bilgiyi entegre ederek RAG, agent'lari basit sohbet programlarindan etkili, veri odakli ve anlamli isler yapabilen araclara donusturur.

## Bilgi Erisimi (RAG) Kalibina Genel Bakis

Bilgi Erisimi (Knowledge Retrieval) — RAG kalibi, LLM'lere bir yanit uretmeden once harici bilgi tabanlarina erisim vererek yeteneklerini onemli olcude arttirir. RAG, yalnizca dahili, onceden egitilmis bilgiye guevenmek yerine, LLM'lerin bir insanin kitaba basvurmasi veya internette arama yapmasi gibi bilgiyi "aramasina" olanak tanir. Bu surec, LLM'lerin daha dogru, guncel ve dogrulanabilir yanitlar sunmasini saglar.

Bir kullanici RAG kullanan bir yapay zeka sistemine bir soru sordugunda veya bir prompt verdiginde, sorgu dogrudan LLM'ye gonderilmez. Bunun yerine sistem, oncelikle genis bir harici bilgi tabanini — belgeler, veritabanlari veya web sayfalarindan olusan son derece duzenlenmis bir kutuphaneyi — ilgili bilgiler icin tarar. Bu arama basit bir anahtar kelime eslestirmesi degildir; kullanicinin niyetini ve sozcuklerinin arkasindaki anlami kavrayan "semantik bir arama"dir. Bu ilk arama, en uygun parçalari veya bilgi "chunk'larini" cikarir. Cikarilan bu parcalar daha sonra orijinal prompt'a "arttirilarak" (augment) eklenir ve daha zengin, daha bilgilendirilmis bir sorgu olusturur. Son olarak, bu zenginlestirilmis prompt LLM'ye gonderilir. Bu ek baglamla LLM, yalnizca akici ve dogal degil, ayni zamanda alilan verilere olgusal olarak dayanan bir yanit uretebilir.

RAG cercevesi bircok onemli fayda saglar. LLM'lerin guncel bilgilere erismesini saglayarak statik egitim verilerinin kisitlamalarini asmasina olanak tanir. Bu yaklasim ayni zamanda yanltlari dogrulanabilir verilere dayandirarak "hallucination" — yanlis bilgi uretimi — riskini de azaltir. Dahasi, LLM'ler dahili sirket belgeleri veya wikilerde bulunan uzmanlasmis bilgiyi kullanabilir. Bu surecin hayati bir avantaji, bilginin tam kaynagini isaretleyen "alinti" (citation) sunma kapasitesidir ve bu da yapay zekanin yanitlarinin guvenilirligini ve dogrulanabilirligini arttirir.

RAG'in nasil calistigini tam olarak anlamak icin birkac temel kavrami anlamak gereklidir (bkz. Sekil 1):

### Embedding'ler

LLM'ler baglaminda embedding'ler, sozcukler, ifadeler veya tam belgeler gibi metinlerin sayisal temsilleridir. Bu temsiller, bir sayilar listesi olan bir vektor bicimindedir. Temel fikir, farkli metin parcalari arasindaki semantik anlami ve iliskileri matematiksel bir uzayda yakalamaktir. Benzer anlamlara sahip sozcukler veya ifadeler, bu vektor uzayinda birbirine daha yakin embedding'lere sahip olacaktir. Ornegin, basit bir 2B grafik hayal edin. "Kedi" kelimesi (2, 3) koordinatlariyla temsil edilebilirken, "yavru kedi" cok yakin bir sekilde (2.1, 3.1) konumunda olacaktir. Buna karsilik, "araba" kelimesi farkli anlamini yansitan (8, 1) gibi uzak bir koordinata sahip olacaktir. Gercekte, bu embedding'ler yuzlerce hatta binlerce boyutlu cok daha yuksek boyutlu bir uzaydadir ve dilin son derece incelikli bir sekilde anlasilmasini mumkun kilar.

### Metin Benzerligi

Metin benzerligi, iki metin parcasinin birbirine ne kadar benzediginin bir olcusudur. Bu, yuzeysel duzyde sozcuklerin ortakligina bakarak (leksikal benzerlik) veya daha derin, anlam tabanli bir duzeyde olabilir. RAG baglaminda metin benzerligi, bilgi tabaninda kullanicinin sorgusuna karsilik gelen en ilgili bilgiyi bulmak icin kritik onem tasir. Ornegin su cumleleri ele alin: "Fransa'nin baskenti neresidir?" ve "Hangi sehir Fransa'nin baskentidir?". Ifade farklı olsa da ayni soruyu sormaktadirlar. Iyi bir metin benzerlik modeli bunu fark edecek ve yalnizca birkac ortak sozcuk paylasmalalarina ragmen bu iki cumleye yuksek bir benzerlik puani atayacaktir. Bu genellikle metinlerin embedding'leri kullanilarak hesaplanir.

### Semantik Benzerlik ve Mesafe

Semantik benzerlik, yalnizca kullanilan sozcukler yerine tamamen metnin anlami ve baglamina odaklanan daha gelismis bir metin benzerligi bicimidir. Iki metin parcasinin ayni kavrami veya fikri ifade edip etmedigini anlamayi amaclar. Semantik mesafe bunun tersidir; yuksek bir semantik benzerlik dusuk bir semantik mesafe anlamina gelir ve tam tersi. RAG'de semantik arama, kullanicinin sorgusuna en kucuk semantik mesafeye sahip belgeleri bulmaya dayanir. Ornegin, "tuylu bir kedi arkadasai" ve "evcil bir kedi" ifadelerinin "bir" disinda hicbir ortak sozcugu yoktur. Ancak semantik benzerligi anlayan bir model, ayni seye atifta bulunduklarini fark edecek ve bunlari son derece benzer kabul edecektir. Bunun nedeni, embedding'lerinin vektor uzayinda birbirine cok yakin olmasi ve kucuk bir semantik mesafe gostermesidir. Bu, kullanicinin ifadeleri bilgi tabanindaki metinle tam olarak eslesmedigi durumda bile RAG'in ilgili bilgiyi bulmasini saglayan "akilli arama"dir.

![RAG Core Concept: Chunking, Embeddings, and Vector Database](../assets/RAG_Core_Concepts_Chunking_Embeddings_and_Vector_Database.png)

Sekil 1: RAG Temel Kavramlari: Parcalama (Chunking), Embedding'ler ve Vector Database

### Belge Parcalama (Chunking)

Parcalama (Chunking), buyuk belgelerin daha kucuk, daha yonetilebilir parcalara veya "chunk'lara" bolunmesi surecidir. Bir RAG sisteminin verimli calisabilmesi icin, tam buyuk belgeleri LLM'ye besleyemez. Bunun yerine, bu daha kucuk parcalari isler. Belgelerin nasil parcalanacagi, bilginin baglamini ve anlamini korumak icin onemlidir. Ornegin, 50 sayfalik bir kullanim kilavuzunu tek bir metin blogu olarak ele almak yerine, bir parcalama stratejisi onu bolumlere, paragraflara veya hatta cumlelere bolebilir. Ornegin, "Sorun Giderme" bolumu, "Kurulum Kilavuzu"ndan ayri bir chunk olacaktir. Bir kullanici belirli bir sorun hakkinda soru sordugunda, RAG sistemi tum kilavuz yerine en ilgili sorun giderme chunk'ini alabilir. Bu, erisim surecini hizlandirir ve LLM'ye saglanan bilgiyi kullanicinin anlik ihtiyacina daha odakli ve ilgili kilar. Belgeler parcalandiktan sonra, RAG sistemi belirli bir sorgu icin en ilgili parcalari bulmak uzere bir erisim teknigi kullanmalidir. Birincil yontem, kavramsal olarak kullanicinin sorusuna benzer chunk'lari bulmak icin embedding'leri ve semantik mesafeyi kullanan vektor aramasidir. Daha eski ancak hala degerli bir teknik, semantik anlami kavramadan terimlerin sikligi temelinde chunk'lari siralayan anahtar kelime tabanli bir algoritma olan BM25'tir. Her iki dunyanin da en iyisini elde etmek icin, BM25'in anahtar kelime hassasiyetini semantik aramanin baglamsal anlayisiyla birlestiren hibrit arama yaklasimlari siklikla kullanilir. Bu birlestirme, hem tam eslestirmeleri hem de kavramsal ilgiliyi yakalayarak daha saglam ve dogru erisim saglar.

### Vector Database'ler

Vector database, embedding'leri verimli bir sekilde depolamak ve sorgulamak icin tasarlanmis ozellestirilmis bir veritabani turudur. Belgeler parcalandiktan ve embedding'lere donusturuldukten sonra, bu yuksek boyutlu vektorler bir vector database'de depolanir. Anahtar kelime tabanli arama gibi geleneksel erisim teknikleri, bir sorgudaki tam sozcukleri iceren belgeleri bulmakta mukemmeldir ancak derin bir dil anlayisindan yoksundur. "Tuylu kedi arkadasi"nin "kedi" anlamina geldigini fark edemezler. Vector database'ler tam da burada one cikar. Semantik arama icin ozel olarak insa edilmislerdir. Metni sayisal vektorler olarak depolayarak, yalnizca anahtar kelime ortakligiyla degil, kavramsal anlama dayali sonuclar bulabilirler. Kullanicinin sorgusu da bir vektore donusturuldugunde, veritabani milyonlarca vektor arasinda hizla arama yapmak ve anlam olarak "en yakin" olanlari bulmak icin yuksek derecede optimize edilmis algoritmalar (HNSW — Hierarchical Navigable Small World gibi) kullanir. Bu yaklasim, kullanicinin ifadesi kaynak belgelerden tamamen farkli olsa bile ilgili baglami ortaya cikardigi icin RAG icin cok daha ustundur. Ozetle, diger teknikler sozcukleri ararken, vector database'ler anlam arar. Bu teknoloji; Pinecone ve Weaviate gibi yonetilen veritabanlarindan Chroma DB, Milvus ve Qdrant gibi acik kaynakli cozumlere kadar cesitli bicimlerde uygulanmaktadir. Mevcut veritabanlari bile vector arama yetenekleriyle zenginlestirilebilir; Redis, Elasticsearch ve Postgres (pgvector uzantisi kullanilarak) bunun ornekleridir. Temel erisim mekanizmalari genellikle Meta AI'in FAISS'i veya Google Research'un ScaNN'i gibi kutuphaneler tarafindan desteklenir ve bunlar bu sistemlerin verimliliginin temelidir.

### RAG'in Zorluklari

Gucune ragmen, RAG kalibi zorluklardan yoksun degildir. Temel bir sorun, bir sorguyu yanitlamak icin gereken bilginin tek bir chunk'ta bulunmayip bir belgenin veya hatta bircok belgenin birden fazla bolumune yayilmis oldugu durumlarda ortaya cikar. Bu tur durumlarda, erisim mekanizmasi gerekli tum baglami toplayamayabilir ve bu da eksik veya yanliss bir yanita yol acar. Sistemin etkinligi ayni zamanda parcalama ve erisim surecinin kalitesine de buyuk olcude baglidir; ilgisiz chunk'lar aliinirsa, bu gurultu olusturabilir ve LLM'yi karistirabilir. Dahasi, potansiyel olarak celiskili kaynaklardan bilgiyi etkili bir sekilde sentezlemek, bu sistemler icin onemli bir engel olmaya devam etmektedir. Bunun otesinde, bir baska zorluk da RAG'in tum bilgi tabaninin onceden islenmesini ve vector veya graf veritabanlari gibi ozellestirilmis veritabanlarinda depolanmasini gerektirmesidir ki bu onemli bir is yukudur. Dolayisiyla bu bilgi, guncel kalabilmesi icin duzenli mutabakat gerektirir; ozellikle sirket wikileri gibi gelisen kaynaklarla ilgilenirken bu kritik bir gorevdir. Tum bu surec, gecikmeyi, operasyonel maliyetleri ve nihai prompt'ta kullanilan token sayisini artirarak performans uzerinde belirgin bir etkiye sahip olabilir.

Ozetle, Retrieval-Augmented Generation (RAG) kalibi, yapay zekayi daha bilgili ve guvenilir kilma yolunda onemli bir ileri adimindir. Harici bilgi erisim adimini uretim surecine sorunsuz bir sekilde entegre ederek, bagimsiz LLM'lerin temel sinirlamalarindan bazilarnini ele alir. Embedding'ler ve semantik benzerlik gibi temel kavramlar, anahtar kelime ve hibrit arama gibi erisim teknikleriyle birlestiginde, sistemin ilgili bilgiyi akilli bir sekilde bulmasini saglar ve stratejik parcalama bunu yonetilebilir kilar. Tum bu erisim sureci, milyonlarca embedding'i olcekli bir sekilde depolamak ve verimli sorgulamak icin tasarlanmis ozellestirilmis vector database'ler tarafindan desteklenir. Parcalanmis veya celiskili bilgiyi erismenin zorluklari devam etse de, RAG LLM'leri yalnizca baglamsal olarak uygun degil, ayni zamanda dogrulanabilir olgulara dayanan yanitlar uretmeleri icin guclendirir ve yapay zekaya duyulan guveni ve faydayi arttirir.

### Graph RAG

GraphRAG, bilgi erisimi icin basit bir vector database yerine bir bilgi grafi (knowledge graph) kullanan gelismis bir Retrieval-Augmented Generation bicimidir. Karmasik sorgulari, bu yapilandirilmis bilgi tabani icindeki veri varliklari (dugumler — nodes) arasindaki acik iliskileri (kenarlar — edges) takip ederek yanitlar. Temel bir avantaji, geleneksel RAG'in sikca basarisiz oldugu, birden fazla belgeye dagalmis bilgiden yanitlar sentezleme yetenegidir. Bu baglantilari anlayarak, GraphRAG daha baglamsal olarak dogru ve incelikli yanitlar sunar.

Kullanim alanlari arasinda sirketleri piyasa olaylarina baglayan karmasik finansal analiz ve genler ile hastaliklar arasindaki iliskileri kesfetmek icin bilimsel arastirma yer alir. Ancak temel dezavantaji, yuksek kaliteli bir bilgi grafi olusturmak ve surdurmek icin gereken onemli karmasiklik, maliyet ve uzmanlik gereksinimidir. Bu kurulum ayrica daha az esnektir ve daha basit vektor arama sistemlerine kiyasla daha yuksek gecikme sunabilir. Sistemin etkinligi tamamen altta yatan graf yapisinin kalitesine ve eksiksizligine baglidir. Sonuc olarak, GraphRAG karmasik sorular icin ustun baglamsal muhakeme sunar ancak cok daha yuksek uygulama ve bakim maliyetleriyle gelir. Ozetle, derin, birbirine bagli icegorulerin standart RAG'in hizi ve basitligindan daha kritik oldugu yerlerde one cikar.

### Agentic RAG

Bu kalibin bir evrimi olan **Agentic RAG** (bkz. Sekil 2), bilgi cikarimnin guvenilirligini onemli olcude artirmak icin bir akil yurutme (Reasoning) ve karar alma katmani ekler. Yalnizca erisim ve arttirma yapmak yerine, bir "agent" — ozellestirilmis bir yapay zeka bileseni — bilginin kritik bir bekci ve iyilestiricisi olarak gorev yapar. Ilk alinan verileri pasif bir sekilde kabul etmek yerine, bu agent kalitesini, ilgilligini ve eksiksizligini aktif olarak sorgular; asagidaki senaryolarda gosterildigi gibi.

Ilk olarak, bir agent yansitma (Reflection) ve kaynak dogrulamada ustundur. Bir kullanici "Sirketimizin uzaktan calisma politikasi nedir?" diye sorarsa, standart bir RAG, resmi 2025 politika belgesiyle birlikte 2020 tarihli bir blog yazisini cekebilir. Ancak agent, belgelerin meta verilerini analiz eder, 2025 politikasini en guncel ve yetkili kaynak olarak tanir ve kesin bir yanit icin dogru baglami LLM'ye gondermeden once eski blog yazisinii eler.

![Agentic RAG Introduces Reasoning Agent](../assets/Agentic_RAG_Introduces_Reasoning_Agent.png)

Sekil 2: Agentic RAG, daha dogru ve guvenilir bir nihai yanit saglamak icin alinan bilgiyi aktif olarak degerlendiren, uzlastiran ve iyilestiren bir akil yurutme agent'i sunar.

Ikinci olarak, bir agent bilgi celiskilerini uzlastirmada yeteneklidir. Bir finansal analistin "Proje Alpha'nin 1. ceyrek butcesi ne kadardi?" diye sordugunu hayal edin. Sistem iki belge alir: 50.000 € butce belirten bir ilk teklif ve 65.000 € olarak listeleyen kesinlesmis bir mali rapor. Agentic RAG bu celiskiyi belirler, mali raporu daha guvenilir kaynak olarak onceliklendirir ve nihai yanitin en dogru verilere dayanmasini saglayarak LLM'ye dogrulanmis rakammi sunar.

Ucuncu olarak, bir agent karmasik yanitlari sentezlemek icin cok adimli akil yurutme (Reasoning) gerceklestirebilir. Bir kullanici "Urunumuzun ozellikleri ve fiyatlari Rakip X ile nasil karsilastiriliyor?" diye sorarsa, agent bunu ayri alt sorgulara ayirir. Kendi urunun ozellikleri, fiyatlandirmasi, Rakip X'in ozellikleri ve Rakip X'in fiyatlandirmasi icin ayri aramalar baslatir. Bu bireysel bilgi parcalarini topladiktan sonra, agent bunlari LLM'ye beslemeden once yapilandirilmis, karsilastirmali bir baglam halinde sentezler ve basit bir erisimin uretemeyecegi kapsamli bir yanit olanagi tanir.

Dorduncu olarak, bir agent bilgi bosluklerini belirleyebilir ve harici araclar kullanabilir. Bir kullanicinin "Dun piyasaya surduguumuz yeni urunumuze piyasanin anlik tepkisi ne oldu?" diye sordugunu varsayin. Agent, haftalik guncellenen dahili bilgi tabanini arar ve ilgili bir bilgi bulamaz. Bu boslugu fark ettikten sonra, son haber makalelerini ve sosyal medya duygusunu bulmak icin canli web arama API'si gibi bir araci etkinlestirebilir. Agent daha sonra, statik dahili veritabaninin sinirlamalarini asarak guncel bir yanit saglamak icin bu taze toplanan harici bilgiyi kullanir.

### Agentic RAG'in Zorluklari

Guclu olmakla birlikte, agentic katman kendi zorluk setini beraberinde getirir. Temel dezavantaj, karmasiklik ve maliyette onemli bir artistir. Agent'in karar alma mantigi ve arac entegrasyonlarinin tasarimi, uygulanmasi ve bakimi onemli muhendislik cabasi gerektirir ve hesaplama masraflarina ekler. Bu karmasiklik ayni zamanda artan gecikmeye de yol acabilir; cunku agent'in yansitma, arac kullanimi ve cok adimli akil yurutme donguleri, standart dogrudan erisim surecinden daha fazla zaman alir. Dahasi, agent'in kendisi yeni bir hata kaynagi olabilir; hatali bir akil yurutme sureci, ajanin gereksiz donguloerde takilmasina, bir gorevi yanlis yorumlamasina veya ilgili bilgiyi uygunsuz bir sekilde elemesine neden olabilir ve nihayetinde nihai yanitin kalitesini dusurur.

### Ozet

Agentic RAG, standart erisim kalibinin sofistike bir evrimimni temsil eder ve onu pasif bir veri boru hattindan aktif, problem cozen bir cercevye donusturur. Kaynaklari degerlendiren, celiskileri uzlastiran, karmasik sorulari ayristiran ve harici araclar kullanan bir akil yurutme katmani yerlesitirerek, agent'lar uretilen yanitlarin guvenilirligini ve derinligini onemli olcude arttirir. Bu ilerleme yapay zekayi daha guvenilir ve yetenekli kilar; ancak dikkatle yonetilmesi gereken sistem karmasikligi, gecikme ve maliyet acisindan onemli odunlesimlerle birlikte gelir.

## Pratik Uygulamalar ve Kullanim Alanlari

Bilgi Erisimi (Knowledge Retrieval) — RAG, buyuk dil modellerinin (LLM) cesitli sektorlerde kullanimini degistirerek daha dogru ve baglamsal olarak ilgili yanitlar sunma yeteneklerini artirmaktadir.

Uygulamalar sunlardir:

* **Kurumsal Arama ve Soru-Cevap:** Kuruluslar, insan kaynaklari politikalari, teknik kilavuzlar ve urun spesifikasyonlari gibi dahili belgeleri kullanarak calisan sorularini yanitlayan dahili sohbet botlari gelistirebilir. RAG sistemi, LLM'nin yanitini bilgilendirmek icin bu belgelerden ilgili bolumleri cikarir.
* **Musteri Destegi ve Yardim Masalari:** RAG tabanli sistemler, urun kilavuzlari, sik sorulan sorular (FAQ) ve destek taleplerindeki bilgilere eriserek musteri sorularina kesin ve tutarli yanitlar sunabilir. Bu, rutin sorunlar icin dogrudan insan mudahalesine duyulan ihtiyaci azaltabilir.
* **Kisisellestirilmis Icerik Onerisi:** Basit anahtar kelime eslesmesi yerine, RAG bir kullanicinin tercihleri veya onceki etkilesimleriyle semantik olarak iliskili icerigi (makaleler, urunler) belirleyebilir ve erisebilir; bu da daha ilgili onerilere yol acar.
* **Haber ve Guncel Olaylarin Ozetlenmesi:** LLM'ler gercek zamanli haber akislariyla entegre edilebilir. Guncel bir olay hakkinda soruldugunda, RAG sistemi son makaleleri alir ve LLM'nin guncel bir ozet uretmesini saglar.

Harici bilgiyi dahil ederek RAG, LLM'lerin yeteneklerini basit iletisimin otesine, bilgi isleme sistemleri olarak islevgormeye kadar genisletir.

## Uygulamali Kod Ornegi (ADK)

Bilgi Erisimi (RAG) kalibini orneklemek icin uc ornek inceleyelim.

Ilk olarak, RAG yapmak ve LLM'leri arama sonuclarina dayandirmak icin Google Search'un nasil kullaniilacagi gosterilmektedir. RAG harici bilgiye erissmeyi icerdiginden, Google Search araci dogrudan LLM'nin bilgisini artirabilecek yerlesik bir erisim mekanizmasi ornegidir.

```python
from google.adk.tools import google_search
from google.adk.agents import Agent


search_agent = Agent(
    name="research_assistant",
    model="gemini-2.0-flash-exp",
    instruction="You help users research topics. When asked, use the Google Search tool",
    tools=[google_search],
)
```

Ikinci olarak, bu bolum Google ADK icinde Vertex AI RAG yeteneklerinin nasil kullanilacagini aciklar. Saglanan kod, ADK'den VertexAiRagMemoryService'in baslatilmasini gosterir. Bu, bir Google Cloud Vertex AI RAG Corpus'a baglanti kurulmasini saglar. Hizmet, corpus kaynak adi ve `SIMILARITY_TOP_K` ile `VECTOR_DISTANCE_THRESHOLD` gibi istege bagli parametreler belirtilerek yapilandirilir. Bu parametreler erisim surecini etkiler. `SIMILARITY_TOP_K`, alinacak en benzer sonuclarin sayisini tanimlar. `VECTOR_DISTANCE_THRESHOLD`, alinan sonuclar icin semantik mesafe sinirini belirler. Bu kurulum, agent'larin belirlenmis RAG Corpus'tan olceklenebilir ve kalici semantik bilgi erisimi gerceklestirmesini saglar. Surec, olgusal verilere dayanan yanitlarin gelistirilmesini destekleyerek Google Cloud'un RAG islevlerini etkili bir sekilde bir ADK agent'ina entegre eder.

```python
# Import the necessary VertexAiRagMemoryService class from the google.adk.memory module.
from google.adk.memory import VertexAiRagMemoryService


RAG_CORPUS_RESOURCE_NAME = "projects/your-gcp-project-id/locations/us-central1/ragCorpora/your-corpus-id"

# Define an optional parameter for the number of top similar results to retrieve.
# This controls how many relevant document chunks the RAG service will return.
SIMILARITY_TOP_K = 5

# Define an optional parameter for the vector distance threshold.
# This threshold determines the maximum semantic distance allowed for retrieved results;
# results with a distance greater than this value might be filtered out.
VECTOR_DISTANCE_THRESHOLD = 0.7

# Initialize an instance of VertexAiRagMemoryService.
# This sets up the connection to your Vertex AI RAG Corpus.
# - rag_corpus: Specifies the unique identifier for your RAG Corpus.
# - similarity_top_k: Sets the maximum number of similar results to fetch.
# - vector_distance_threshold: Defines the similarity threshold for filtering results.
memory_service = VertexAiRagMemoryService(
    rag_corpus=RAG_CORPUS_RESOURCE_NAME,
    similarity_top_k=SIMILARITY_TOP_K,
    vector_distance_threshold=VECTOR_DISTANCE_THRESHOLD,
)
```

## Uygulamali Kod Ornegi (LangChain)

Ucuncu olarak, LangChain kullanan eksiksiz bir ornegi inceleyelim.

```python
import os
import requests
from typing import List, Dict, Any, TypedDict

from langchain_community.document_loaders import TextLoader
from langchain_core.documents import Document
from langchain_core.prompts import ChatPromptTemplate
from langchain_core.output_parsers import StrOutputParser
from langchain_community.embeddings import OpenAIEmbeddings
from langchain_community.vectorstores import Weaviate
from langchain_openai import ChatOpenAI
from langchain.text_splitter import CharacterTextSplitter
from langchain.schema.runnable import RunnablePassthrough
from langgraph.graph import StateGraph, END

import weaviate
from weaviate.embedded import EmbeddedOptions
import dotenv


# Load environment variables (e.g., OPENAI_API_KEY)
dotenv.load_dotenv()

# Set your OpenAI API key (ensure it's loaded from .env or set here)
# os.environ["OPENAI_API_KEY"] = "YOUR_OPENAI_API_KEY"


# --- 1. Data Preparation (Preprocessing) ---

# Load data
url = "https://github.com/langchain-ai/langchain/blob/master/docs/docs/how_to/state_of_the_union.txt"
res = requests.get(url)
with open("state_of_the_union.txt", "w") as f:
    f.write(res.text)

loader = TextLoader("./state_of_the_union.txt")
documents = loader.load()

# Chunk documents
text_splitter = CharacterTextSplitter(chunk_size=500, chunk_overlap=50)
chunks = text_splitter.split_documents(documents)

# Embed and store chunks in Weaviate
client = weaviate.Client(embedded_options=EmbeddedOptions())

vectorstore = Weaviate.from_documents(
    client=client,
    documents=chunks,
    embedding=OpenAIEmbeddings(),
    by_text=False,
)

# Define the retriever
retriever = vectorstore.as_retriever()

# Initialize LLM
llm = ChatOpenAI(model_name="gpt-3.5-turbo", temperature=0)


# --- 2. Define the State for LangGraph ---
class RAGGraphState(TypedDict):
    question: str
    documents: List[Document]
    generation: str


# --- 3. Define the Nodes (Functions) ---
def retrieve_documents_node(state: RAGGraphState) -> RAGGraphState:
    """Retrieves documents based on the user's question."""
    question = state["question"]
    documents = retriever.invoke(question)
    return {"documents": documents, "question": question, "generation": ""}


def generate_response_node(state: RAGGraphState) -> RAGGraphState:
    """Generates a response using the LLM based on retrieved documents."""
    question = state["question"]
    documents = state["documents"]

    # Prompt template from the PDF
    template = """You are an assistant for question-answering tasks. Use the following pieces of retrieved context to answer the question. If you don't know the answer, just say that you don't know. Use three sentences maximum and keep the answer concise.
Question: {question}
Context: {context}
Answer: """
    prompt = ChatPromptTemplate.from_template(template)

    # Format the context from the documents
    context = "\n\n".join([doc.page_content for doc in documents])

    # Create the RAG chain
    rag_chain = prompt | llm | StrOutputParser()

    # Invoke the chain
    generation = rag_chain.invoke({"context": context, "question": question})

    return {"question": question, "documents": documents, "generation": generation}


# --- 4. Build the LangGraph Graph ---
workflow = StateGraph(RAGGraphState)

# Add nodes
workflow.add_node("retrieve", retrieve_documents_node)
workflow.add_node("generate", generate_response_node)

# Set the entry point
workflow.set_entry_point("retrieve")

# Add edges (transitions)
workflow.add_edge("retrieve", "generate")
workflow.add_edge("generate", END)

# Compile the graph
app = workflow.compile()


# --- 5. Run the RAG Application ---
if __name__ == "__main__":
    print("\n--- Running RAG Query ---")
    query = "What did the president say about Justice Breyer"
    inputs = {"question": query}
    for s in app.stream(inputs):
        print(s)

    print("\n--- Running another RAG Query ---")
    query_2 = "What did the president say about the economy?"
    inputs_2 = {"question": query_2}
    for s in app.stream(inputs_2):
        print(s)
```

Bu Python kodu, LangChain ve LangGraph ile uygulanan bir Retrieval-Augmented Generation (RAG) boru hattini gostermektedir. Surec, bir metin belgesinden turetilen bir bilgi tabaninin olusturulmasiyla baslar; belge chunk'lara bolunerek embedding'lere donusturulur. Bu embedding'ler daha sonra verimli bilgi erisimini kolaylastirmak icin bir Weaviate vector store'da depolanir. LangGraph'te bir StateGraph, iki temel fonksiyon arasindaki is akisini yonetmek icin kullanilir: `retrieve_documents_node` ve `generate_response_node`. `retrieve_documents_node` fonksiyonu, kullanicinin girdisine dayanarak ilgili belge chunk'larini belirlemek icin vector store'u sorgular. Ardindan `generate_response_node` fonksiyonu, alinan bilgileri ve onceden tanimlanmis bir prompt sablonunu kullanarak bir OpenAI LLM araciligiyla bir yanit uretir. `app.stream` yontemi, RAG boru hatti uzerinden sorgularin calistirilmasini mumkun kilar ve sistemin baglamsal olarak ilgili ciktilar uretme kapasitesini gosterir.

## Bir Bakista

**Ne:** LLM'ler etkileyici metin uretme yeteneklerine sahiptir ancak temelde egitim verileriyle sinirlidir. Bu bilgi statiktir; yani gercek zamanli bilgileri veya ozel, alana ozgu verileri icermez. Dolayisiyla yanitlari guncelligini yitirebilir, yanliss olabilir veya uzmanlasmis gorevler icin gereken belirli baglamdan yoksun olabilir. Bu bosluk, guncel ve olgusal yanitlar gerektiren uygulamalar icin guvenilirliklerini kisitlar.

**Neden:** Retrieval-Augmented Generation (RAG) kalibi, LLM'leri harici bilgi kaynaklarina baglayarak standartlastirilmis bir cozum sunar. Bir sorgu alindiginda, sistem oncelikle belirlenen bir bilgi tabanindan ilgili bilgi parcalarini alir. Bu parcalar daha sonra orijinal prompt'a eklenerek zamaninda ve ozel baglamla zenginlestirilir. Bu zenginlestirilmis prompt daha sonra LLM'ye gonderilir ve dogru, dogrulanabilir ve harici verilere dayanan bir yanit uretmesini saglar. Bu surec, LLM'yi etkili bir sekilde kapali kitap bir muhakemeciden acik kitap birine donusturur ve faydaliligini ve guvenilirligini onemli olcude arttirir.

**Temel Kural:** Bu kalibi, bir LLM'nin orijinal egitim verilerinin parcasi olmayan belirli, guncel veya tescilli bilgilere dayanan soruları yanitlamasi veya icerik uretmesi gerektiginde kullanin. Dahili belgeler uzerinde soru-cevap sistemleri, musteri destek botlari ve alintilarla dogrulanabilir, olgu tabanli yanitlar gerektiren uygulamalar olusturmak icin idealdir.

**Gorsel Ozet:**

![Knowledge Retrieval Pattern Database](../assets/Knowledge_Retrieval_Pattern_Database.png)

Bilgi Erisimi kalibi: yapilandirilmis veritabanlarindan bilgi sorgulamak ve erismek icin bir yapay zeka agent'i

![Knowledge Retrieval Pattern Search](../assets/Knowledge_Retrieval_Pattern_Search.png)

Sekil 3: Bilgi Erisimi kalibi: kullanici sorgularina yanit olarak kamusal internetten bilgi bulmak ve sentezlemek icin bir yapay zeka agent'i.

## Temel Cikarimlar

* Bilgi Erisimi (Knowledge Retrieval) — RAG, LLM'lerin harici, guncel ve ozel bilgilere erismesini saglayarak yeteneklerini arttirir.
* Surec, Erisim (bilgi tabaninda ilgili parcalari arama) ve Arttirma (bu parcalari LLM'nin prompt'una ekleme) asamalarini icerir.
* RAG, LLM'lerin guncelligini yitirmis egitim verileri gibi sinirlamalari asmasina yardimci olur, "hallucination"lari azaltir ve alana ozgu bilgi entegrasyonunu mumkun kilar.
* RAG, LLM'nin yanitinin alinan kaynaklara dayandigi icin atfedilebilir yanitlara olanak tanir.
* GraphRAG, farkli bilgi parcalari arasindaki iliskileri anlamak icin bir bilgi grafinden yararlanarak birden fazla kaynaktan veri sentezlemeyi gerektiren karmasik sorulari yanitlar.
* Agentic RAG, basit bilgi erisiminin otesine gecerek harici bilgiyi aktif olarak akil yurutme, dogrulama ve iyilestirme icin akilli bir agent kullanir ve daha dogru ve guvenilir bir yanit saglar.
* Pratik uygulamalar; kurumsal arama, musteri destegi, hukuki arastirma ve kisisellestirilmis onerileri kapsar.

## Sonuc

Sonuc olarak, Retrieval-Augmented Generation (RAG), bir buyuk dil modelinin statik bilgisinin temel sinirlamasini, onu harici, guncel veri kaynaklarina baglayarak ele alir. Surec, oncelikle ilgili bilgi parcalarini alip ardindan kullanicinin prompt'unu zenginlestirerek LLM'nin daha dogru ve baglamsal olarak farkinda yanitlar uretmesini saglar. Bu, embedding'ler, semantik arama ve vector database'ler gibi yalnizca anahtar kelimelere degil anlama dayali bilgi bulan temel teknolojiler sayesinde mumkun olmaktadir. Ciktilari dogrulanabilir verilere dayandirarak, RAG olgusal hatalari onemli olcude azaltir ve tescilli bilgilerin kullanilmasini mumkun kilarak alintiler araciligiyla guveni arttirir.

Gelismis bir evrim olan Agentic RAG, daha da buyuk guvenilirlik icin alinan bilgiyi aktif olarak dogrulayan, uzlastiran ve sentezleyen bir akil yurutme katmani sunar. Benzer sekilde, GraphRAG gibi ozellestirilmis yaklasimlar, acik veri iliskilerinde gezinerek sistemin son derece karmasik, birbiriyle baglantili sorgulara yanitlar sentezlemesini saglayan bilgi graflerinden yararlanir. Bu agent, celiskili bilgileri cozebilir, cok adimli sorgular gerceklestirebilir ve eksik verileri bulmak icin harici araclar kullanabilir. Bu gelismis yontemler karmasiklik ve gecikme eklese de, nihai yanitin derinligini ve guvenilirligini buyuk olcude arttirir. Bu kaliplarin pratik uygulamalari, kurumsal aramadan musteri destegine ve kisisellestirilmis icerik sunumuna kadar sektorleri donusturmektedir. Zorluklara ragmen, RAG yapay zekayi daha bilgili, guvenilir ve faydali kilmak icin kritik bir kaliptir. Nihayetinde, LLM'leri kapali kitap sohbet programlarindan guclu, acik kitap akil yurutme araclarina donusturur.

## Kaynaklar

1. Lewis, P., et al. (2020). *Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks*. [https://arxiv.org/abs/2005.11401](https://arxiv.org/abs/2005.11401)
2. Google AI for Developers Documentation.  *Retrieval Augmented Generation - [https://cloud.google.com/vertex-ai/generative-ai/docs/rag-engine/rag-overview](https://cloud.google.com/vertex-ai/generative-ai/docs/rag-engine/rag-overview)*
3. Retrieval-Augmented Generation with Graphs (GraphRAG), [https://arxiv.org/abs/2501.00309](https://arxiv.org/abs/2501.00309)
4. LangChain and LangGraph: Leonie Monigatti, "Retrieval-Augmented Generation (RAG): From Theory to LangChain Implementation,"  [*https://medium.com/data-science/retrieval-augmented-generation-rag-from-theory-to-langchain-implementation-4e9bd5f6a4f2*](https://medium.com/data-science/retrieval-augmented-generation-rag-from-theory-to-langchain-implementation-4e9bd5f6a4f2)
5. Google Cloud Vertex AI RAG Corpus [*https://cloud.google.com/vertex-ai/generative-ai/docs/rag-engine/manage-your-rag-corpus#corpus-management*](https://cloud.google.com/vertex-ai/generative-ai/docs/rag-engine/manage-your-rag-corpus#corpus-management)
