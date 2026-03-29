# Bolum 16: Kaynak Odakli Optimizasyon (Resource-Aware Optimization)

Kaynak Odakli Optimizasyon (Resource-Aware Optimization), akilli agent'larin calisma sirasinda hesaplama, zaman ve finansal kaynaklari dinamik olarak izlemesini ve yonetmesini saglar. Bu, oncelikli olarak eylem siralamaya odaklanan basit planlamadan (Planning) farklidir. Kaynak Odakli Optimizasyon, agent'larin belirli kaynak butceleri dahilinde hedeflere ulasmak veya verimliligi optimize etmek icin eylem yurutme konusunda kararlar almasini gerektirir. Bu, daha doğru ancak pahali modeller ile daha hizli, dusuk maliyetli modeller arasinda secim yapmayi ya da daha rafine bir yanit icin ek hesaplama gücü ayirip ayirmama veya daha hizli ancak daha az ayrintili bir yanit dondurme kararini icerir.

Ornegin, bir finans analisti icin buyuk bir veri setini analiz etmekle gorevlendirilmis bir agent'i ele alalim. Analist hemen bir on rapor istiyorsa, agent temel eğilimleri hizla ozetlemek icin daha hizli ve uygun maliyetli bir model kullanabilir. Ancak analist kritik bir yatirim karari icin yuksek dogrulukta bir tahmin gerektiriyorsa ve daha buyuk bir butcesi ve daha fazla zamani varsa, agent guclu, yavas ama daha hassas bir tahminci model kullanmak icin daha fazla kaynak ayirir. Bu kategorideki onemli bir strateji, tercih edilen modelin asiri yuklenme veya kisitlama nedeniyle kullanilamaz oldugunda bir guvenlik agi gorevi goren fallback mekanizmasidir. Zarif bir bozulma saglamak icin sistem otomatik olarak varsayilan veya daha uygun maliyetli bir modele gecer ve tamamen basarisiz olmak yerine hizmet surekliligi saglar.

## Pratik Uygulamalar ve Kullanim Alanlari

Pratik kullanim alanlari sunlardir:

* **Maliyet Optimize Edilmis LLM Kullanimi:** Bir agent'in butce kisitlamasina dayanarak karmasik gorevler icin buyuk, pahali bir LLM mi yoksa daha basit sorgular icin daha kucuk, uygun maliyetli bir LLM mi kullanacagina karar vermesi.
* **Gecikmeye Duyarli Islemler:** Gercek zamanli sistemlerde, bir agent'in zamaninda yanit saglamak icin daha hizli ancak potansiyel olarak daha az kapsamli bir akil yurutme (Reasoning) yolu secmesi.
* **Enerji Verimliligi:** Uc cihazlarda veya sinirli gucle konuslandirilan agent'lar icin, pil omrunu korumak amaciyla islemelerini optimize etme.
* **Hizmet Guvenirligi icin Fallback:** Birincil secim kullanilamaz oldugunda bir agent'in otomatik olarak yedek modele gecmesi, hizmet surekliligi ve zarif bozulma saglamasi.
* **Veri Kullanim Yonetimi:** Bant genisligi veya depolama tasarrufu icin tam veri seti indirmeleri yerine ozetlenmis veri erisimine yonelen bir agent.
* **Uyarlanabilir Gorev Tahsisi:** Multi-agent sistemlerde, agent'larin mevcut hesaplama yukune veya kullanilabilir zamana gore kendilerine gorev atamalari.

## Uygulamali Kod Ornegi

Kullanici sorularini yanitmak icin akilli bir sistem, her sorunun zorlugunu degerlendirebilir. Basit sorgular icin Gemini Flash gibi uygun maliyetli bir dil modeli kullanir. Karmasik sorular icin daha guclu ancak pahali bir dil modeli (Gemini Pro gibi) degerlendirilir. Daha guclu modeli kullanma karari ayni zamanda kaynak uygunluguna, ozellikle butce ve zaman kisitlarina baglidir. Bu sistem uygun modelleri dinamik olarak secer.

Ornegin, hiyerarsik bir agent ile olusturulmus bir seyahat planlayicisini ele alalim. Kullanicinin karmasik istegini anlama, cok adimli bir guzergaha ayristirma ve mantiksal kararlar verme gibi ust duzey planlama, Gemini Pro gibi sofistike ve daha guclu bir LLM tarafindan yonetilecektir. Bu, baglam derinligine sahip ve akil yurutme yetenegine sahip olmasi gereken "planlayici" agent'tir.

Ancak plan olusturulduktan sonra, ucus fiyatlarini arama, otel musaitligi kontrol etme veya restoran degerlendirmelerini bulma gibi plan icindeki bireysel gorevler temelde basit, tekrarlanabilir web sorgularidir. Bu "tool function call'lari" Gemini Flash gibi daha hizli ve uygun maliyetli bir modelle yurutulebilir. Uygun maliyetli modelin bu basit web aramalari icin neden kullanilabildigi daha kolay gorsellestirilirken, karmasik planlama asamasi tutarli ve mantikli bir seyahat plani saglamak icin daha gelismis modelin ustun zekasini gerektirir.

Google'in ADK'si, farkli agent'larin uzmanlasmis gorevleri ele almasina olanak taniyan multi-agent mimarisi araciligiyla bu yaklasimi destekler. Model esnekligi, hem Gemini Pro hem de Gemini Flash dahil olmak uzere cesitli Gemini modellerinin dogrudan kullanilmasini veya LiteLLM araciligiyla diger modellerin entegrasyonunu saglar. ADK'nin orkestrasyon yetenekleri, uyarlanabilir davranis icin dinamik, LLM gudumlü yonlendirmeyi (Routing) destekler. Yerlesik degerlendirme ozellikleri, sistem iyilestirmesi icin kullanilabilecek agent performansinin sistematik degerlendirilmesine olanak tanir (Degerlendirme ve Izleme bolumune bakiniz).

Simdi, ayni kuruluma sahip ancak farkli modeller ve maliyetler kullanan iki agent tanimlanacaktir.

```python
# Conceptual Python-like structure, not runnable code
from google.adk.agents import Agent
# from google.adk.models.lite_llm import LiteLlm  # If using models not directly supported by ADK's default Agent

# Agent using the more expensive Gemini Pro 2.5
gemini_pro_agent = Agent(
    name="GeminiProAgent",
    model="gemini-2.5-pro",  # Placeholder for actual model name if different
    description="A highly capable agent for complex queries.",
    instruction="You are an expert assistant for complex problem-solving.",
)

# Agent using the less expensive Gemini Flash 2.5
gemini_flash_agent = Agent(
    name="GeminiFlashAgent",
    model="gemini-2.5-flash",  # Placeholder for actual model name if different
    description="A fast and efficient agent for simple queries.",
    instruction="You are a quick assistant for straightforward questions.",
)
```

Bir Router Agent, kisa sorgulari daha ucuz modellere ve uzun sorgulari daha yetenekli modellere yonlendiren sorgu uzunlugu gibi basit metriklere dayali olarak sorgulari yonlendirebilir. Ancak daha sofistike bir Router Agent, sorgu nüanslarini ve karmasikligini analiz etmek icin LLM veya ML modellerini kullanabilir. Bu LLM router'i, hangi alt dil modelinin en uygun oldugunu belirleyebilir. Ornegin, gerceksel bilgi geri cagirma isteyen bir sorgu flash modeline yonlendirilirken, derin analiz gerektiren karmasik bir sorgu pro modeline yonlendirilir.

Optimizasyon teknikleri, LLM router'inin etkinligini daha da artirabilir. Prompt tuning, daha iyi yonlendirme kararlari icin router LLM'i yonlendirmek amaciyla prompt'lar hazirlmayi icerir. LLM router'inin sorgular ve optimal model secimleri veri seti uzerinde fine-tuning yapilmasi, dogrulugunu ve verimliligini arttirir. Bu dinamik yonlendirme yetenegi, yanit kalitesi ile maliyet etkinligi arasindaki dengeyi saglar.

```python
# Conceptual Python-like structure, not runnable code
import asyncio
from typing import AsyncGenerator

from google.adk.agents import Agent, BaseAgent
from google.adk.events import Event
from google.adk.agents.invocation_context import InvocationContext


class QueryRouterAgent(BaseAgent):
    name: str = "QueryRouter"
    description: str = "Routes user queries to the appropriate LLM agent based on complexity."

    async def _run_async_impl(self, context: InvocationContext) -> AsyncGenerator[Event, None]:
        user_query = context.current_message.text  # Assuming text input
        query_length = len(user_query.split())  # Simple metric: number of words

        if query_length < 20:  # Example threshold for simplicity vs. complexity
            print(f"Routing to Gemini Flash Agent for short query (length: {query_length})")
            # In a real ADK setup, you would 'transfer_to_agent' or directly invoke
            # For demonstration, we'll simulate a call and yield its response
            response = await gemini_flash_agent.run_async(context.current_message)
            yield Event(author=self.name, content=f"Flash Agent processed: {response}")
        else:
            print(f"Routing to Gemini Pro Agent for long query (length: {query_length})")
            response = await gemini_pro_agent.run_async(context.current_message)
            yield Event(author=self.name, content=f"Pro Agent processed: {response}")
```

Elestiri Agent'i (Critique Agent), dil modellerinden gelen yanitlari degerlendirerek birkac isleve hizmet eden geri bildirim saglar. Kendini duzeltme icin hatalari veya tutarsizliklari belirleyerek yanitlayan agent'i ciktisini iyilestirmeye yonlendirir ve kaliteyi arttirir. Ayrica dogruluk ve ilgililik gibi metrikleri izleyerek performans izleme (Monitoring) icin yanitlari sistematik olarak degerlendirir; bunlar optimizasyon icin kullanilir.

Ek olarak, geri bildirimi pekistirmeli ogrenme veya fine-tuning isareti verebilir; ornegin Flash modelinin yetersiz yanitlarinin tutarli olarak belirlenmesi, router agent'inin mantigini iyilestirebilir. Butceyi dogrudan yonetmese de, Elestiri Agent'i, basit sorgulari Pro modeline veya karmasik sorgulari Flash modeline yonlendirmek gibi optimal olmayan yonlendirme secimlerini belirleyerek dolayli butce yonetimine katkida bulunur; bu da kotu sonuclara yol acar. Bu, kaynak tahsisini ve maliyet tasarruflarini iyilestiren ayarlamalari bilgilendirir.

Elestiri Agent'i, yalnizca yanitlayan agent'tan uretilen metni veya hem orijinal sorguyu hem de uretilen metni incelemek uzere yapilandirilabilir; bu, yanitin ilk soruyla uyumunun kapsamli bir degerlendirmesini mumkun kilar.

```python
CRITIC_SYSTEM_PROMPT = """
You are the **Critic Agent**, serving as the quality assurance arm of our collaborative research assistant system. Your primary function is to **meticulously review and challenge** information from the Researcher Agent, guaranteeing **accuracy, completeness, and unbiased presentation**. Your duties encompass: * **Assessing research findings** for factual correctness, thoroughness, and potential leanings. * **Identifying any missing data** or inconsistencies in reasoning. * **Raising critical questions** that could refine or expand the current understanding. * **Offering constructive suggestions** for enhancement or exploring different angles. * **Validating that the final output is comprehensive** and balanced. All criticism must be constructive. Your goal is to fortify the research, not invalidate it. Structure your feedback clearly, drawing attention to specific points for revision. Your overarching aim is to ensure the final research product meets the highest possible quality standards.
"""
```

Elestiri Agent'i, rolunu, sorumluluklarini ve geri bildirim yaklasimini ozetleyen onceden tanimlanmis bir sistem prompt'una dayali olarak calisir. Bu agent icin iyi tasarlanmis bir prompt, islevini bir degerlendirici olarak acikca belirlemelidir. Elestirel odak alanlarini belirtmeli ve salt reddetme yerine yapici geri bildirim saglamayi vurgulamalıdir. Prompt ayrica hem guclü yanlarin hem de zayifliklarin belirlenmesini tesvik etmeli ve agent'i geri bildirimini nasil yapilandiracagi ve sunacagi konusunda yonlendirmelidir.

## OpenAI ile Uygulamali Kod

Bu sistem, kullanici sorgularini verimli bir sekilde islemek icin kaynak odakli bir optimizasyon stratejisi kullanir. Once her sorguyu en uygun ve maliyet etkin isleme yolunu belirlemek icin uc kategoriden birine siniflandirir. Bu yaklasim, basit isteklerde hesaplama kaynaklarinin israf edilmesini onlerken, karmasik sorgularin gerekli ilgiyi almasini saglar. Uc kategori sunlardir:

* simple: Karmasik akil yurutme veya harici veri gerektirmeden dogrudan yanıtlanabilecek basit sorular icin.
* reasoning: Daha guclu modellere yonlendirilen, mantiksal cikarim veya cok adimli dusunme surecleri gerektiren sorgular icin.
* `internetsearch`: Guncel bilgi gerektiren sorular icin, guncel bir yanit saglamak amaciyla otomatik olarak Google Arama tetikler.

Kod MIT lisansi altindadir ve Github'da mevcuttur: ([https://github.com/mahtabsyed/21-Agentic-Patterns/blob/main/16ResourceAwareOptLLMReflectionv2.ipynb](https://github.com/mahtabsyed/21-Agentic-Patterns/blob/main/16_Resource_Aware_Opt_LLM_Reflection_v2.ipynb))

```python
# MIT License
# Copyright (c) 2025 Mahtab Syed
# https://www.linkedin.com/in/mahtabsyed/

import os
import json
import requests
from dotenv import load_dotenv
from openai import OpenAI


# Load environment variables
load_dotenv()

OPENAI_API_KEY = os.getenv("OPENAI_API_KEY")
GOOGLE_CUSTOM_SEARCH_API_KEY = os.getenv("GOOGLE_CUSTOM_SEARCH_API_KEY")
GOOGLE_CSE_ID = os.getenv("GOOGLE_CSE_ID")

if not OPENAI_API_KEY or not GOOGLE_CUSTOM_SEARCH_API_KEY or not GOOGLE_CSE_ID:
    raise ValueError(
        "Please set OPENAI_API_KEY, GOOGLE_CUSTOM_SEARCH_API_KEY, and GOOGLE_CSE_ID in your .env file."
    )

client = OpenAI(api_key=OPENAI_API_KEY)


# --- Step 1: Classify the Prompt ---
def classify_prompt(prompt: str) -> dict:
    system_message = {
        "role": "system",
        "content": (
            "You are a classifier that analyzes user prompts and returns one of three categories ONLY:\n\n"
            "- simple\n"
            "- reasoning\n"
            "- internet_search\n\n"
            "Rules:\n"
            "- Use 'simple' for direct factual questions that need no reasoning or current events.\n"
            "- Use 'reasoning' for logic, math, or multi-step inference questions.\n"
            "- Use 'internet_search' if the prompt refers to current events, recent data, or things not in your training data.\n\n"
            "Respond ONLY with JSON like:\n"
            '{ "classification": "simple" }'
        ),
    }
    user_message = {"role": "user", "content": prompt}

    response = client.chat.completions.create(
        model="gpt-4o",
        messages=[system_message, user_message],
        temperature=1,
    )
    reply = response.choices[0].message.content
    return json.loads(reply)


# --- Step 2: Google Search ---
def google_search(query: str, num_results: int = 1) -> list:
    url = "https://www.googleapis.com/customsearch/v1"
    params = {
        "key": GOOGLE_CUSTOM_SEARCH_API_KEY,
        "cx": GOOGLE_CSE_ID,
        "q": query,
        "num": num_results,
    }
    try:
        response = requests.get(url, params=params)
        response.raise_for_status()
        results = response.json()
        if "items" in results and results["items"]:
            return [
                {
                    "title": item.get("title"),
                    "snippet": item.get("snippet"),
                    "link": item.get("link"),
                }
                for item in results["items"]
            ]
        else:
            return []
    except requests.exceptions.RequestException as e:
        return {"error": str(e)}


# --- Step 3: Generate Response ---
def generate_response(prompt: str, classification: str, search_results=None) -> tuple[str, str]:
    if classification == "simple":
        model = "gpt-4o-mini"
        full_prompt = prompt

    elif classification == "reasoning":
        model = "o4-mini"
        full_prompt = prompt

    elif classification == "internet_search":
        model = "gpt-4o"
        # Convert each search result dict to a readable string
        if search_results:
            search_context = "\n".join(
                [
                    f"Title: {item.get('title')}\nSnippet: {item.get('snippet')}\nLink: {item.get('link')}"
                    for item in search_results
                ]
            )
        else:
            search_context = "No search results found."
        full_prompt = (
            "Use the following web results to answer the user query: "
            f"{search_context}\nQuery: {prompt}"
        )
    else:
        # Fallback
        model = "gpt-4o"
        full_prompt = prompt

    response = client.chat.completions.create(
        model=model,
        messages=[{"role": "user", "content": full_prompt}],
        temperature=1,
    )
    return response.choices[0].message.content, model


# --- Step 4: Combined Router ---
def handle_prompt(prompt: str) -> dict:
    classification_result = classify_prompt(prompt)
    classification = classification_result["classification"]

    search_results = None
    if classification == "internet_search":
        search_results = google_search(prompt)

    answer, model = generate_response(prompt, classification, search_results)
    return {"classification": classification, "response": answer, "model": model}


if __name__ == "__main__":
    test_prompt = "What is the capital of Australia?"
    # test_prompt = "Explain the impact of quantum computing on cryptography."
    # test_prompt = "When does the Australian Open 2026 start, give me full date?"

    result = handle_prompt(test_prompt)

    print("🔍 Classification:", result["classification"])
    print("🧠 Model Used:", result["model"])
    print("🧠 Response:\n", result["response"])
```

Bu Python kodu, kullanici sorularini yanitlamak icin bir prompt yonlendirme sistemi uygular. OpenAI ve Google Custom Search icin gerekli API anahtarlarini bir .env dosyasindan yukleyerek baslar. Temel islevsellik, kullanicinin prompt'unu uc kategoriye siniflandirmaktadir: simple, reasoning veya internet search. Bu siniflandirma adimi icin ozel bir fonksiyon bir OpenAI modeli kullanir. Prompt guncel bilgi gerektiriyorsa, Google Custom Search API kullanilarak bir Google aramasi yapilir. Baska bir fonksiyon daha sonra siniflandirmaya dayali olarak uygun bir OpenAI modelini secerek nihai yaniti olusturur. Internet arama sorgulari icin, arama sonuclari modele baglam olarak saglanir. Ana `handleprompt` fonksiyonu bu is akisini yoneterek, yanit olusturmadan once siniflandirma ve arama (gerekiyorsa) fonksiyonlarini cagirir. Siniflandirmayi, kullanilan modeli ve olusturulan yaniti dondurur. Bu sistem, farkli sorgu turlerini daha iyi bir yanit icin optimize edilmis yontemlere verimli bir sekilde yonlendirir.

# OpenRouter ile Uygulamali Kod Ornegi

OpenRouter, tek bir API uc noktasi araciligiyla yuzlerce yapay zeka modeline birlesik bir arayuz sunar. Otomatik failover ve maliyet optimizasyonu saglar; tercih ettiginiz SDK veya framework ile kolay entegrasyon imkani sunar.

```python
import json
import requests

response = requests.post(
    url="https://openrouter.ai/api/v1/chat/completions",
    headers={
        "Authorization": "Bearer <OPENROUTER_API_KEY>",
        "HTTP-Referer": "<YOUR_SITE_URL>",  # Optional. Site URL for rankings on openrouter.ai.
        "X-Title": "<YOUR_SITE_NAME>",      # Optional. Site title for rankings on openrouter.ai.
    },
    data=json.dumps({
        "model": "openai/gpt-4o",  # Optional
        "messages": [
            {
                "role": "user",
                "content": "What is the meaning of life?"
            }
        ]
    }),
)
```

Bu kod parcasi, OpenRouter API ile etkilesim kurmak icin requests kutuphanesini kullanir. Bir kullanici mesajiyla chat completion uc noktasina bir POST istegi gonderir. Istek, bir API anahtari ve istege bagli site bilgileri iceren yetkilendirme basliklarini icerir. Amac, belirtilen bir dil modelinden (bu durumda "openai/gpt-4o") bir yanit almaktir.

OpenRouter, belirli bir istegi islemek icin kullanilan hesaplama modelini yonlendirme ve belirleme icin iki farkli metodoloji sunar.

* **Otomatik Model Secimi:** Bu fonksiyon, mevcut modellerin kuratoryel bir setinden secilen optimize edilmis bir modele istek yonlendirir. Secim, kullanicinin prompt'unun belirli icerigine dayanir. Istegi nihayetinde isleyen modelin tanımlayicisi, yanitin meta verilerinde dondurulur.

```json
{
    "model": "openrouter/auto",
    ... // Other params
}
```

* **Sirali Model Fallback:** Bu mekanizma, kullanicilarin hiyerarsik bir model listesi belirtmesine olanak taniyan operasyonel yedeklilik saglar. Sistem once istegi siradaki birincil model ile islemeye calisir. Bu birincil model, hizmet kullanilamazligi, hiz sinirlamasi veya icerik filtreleme gibi herhangi bir hata durumu nedeniyle yanit veremezse, sistem istegi otomatik olarak siradaki belirtilen modele yeniden yonlendirir. Bu islem, listedeki bir model istegi basariyla yurutene veya liste tukenene kadar devam eder. Operasyonun nihai maliyeti ve yanita dondurulen model tanımlayicisi, hesaplamayi basariyla tamamlayan modele karsilik gelecektir.

```json
{
    "models": ["anthropic/claude-3.5-sonnet", "gryphe/mythomax-l2-13b"],
    ... // Other params }
```

OpenRouter, mevcut yapay zeka modellerini toplam token uretimine gore siralayan ayrintili bir liderlik tablosu ([https://openrouter.ai/rankings](https://openrouter.ai/rankings)) sunar. Ayrica farkli saglayicilardan (ChatGPT, Gemini, Claude) en son modelleri de sunar (bkz. Sekil 1).

![OpenRouter Web site](../assets/OpenRouter_Web_Site.png)

Sekil 1: OpenRouter Web sitesi ([https://openrouter.ai/](https://openrouter.ai/))

## Dinamik Model Degistirmenin Otesinde: Agent Kaynak Optimizasyonlarinin Genis Yelpazesi

Kaynak odakli optimizasyon, gercek dunya kisitlamalari dahilinde verimli ve etkili bir sekilde calisan akilli agent sistemleri gelistirmede buyuk onem tasir. Bir dizi ek tekniğe goz atalim:

**Dinamik Model Degistirme**, gorev karmasikligina ve mevcut hesaplama kaynaklarina dayali olarak buyuk dil modellerinin stratejik secimini iceren kritik bir tekniktir. Basit sorgularla karsilasildiginda hafif, maliyet etkin bir LLM konuslandirilabilirken, karmasik, cok yonlu problemler daha sofistike ve kaynak yogun modellerin kullanimini gerektirir.

**Uyarlanabilir Arac Kullanimi ve Secimi**, agent'larin bir arac paketinden akilli bir sekilde secim yapmasini saglayarak, her bir alt gorev icin en uygun ve verimli olani, API kullanim maliyetleri, gecikme ve yurutme suresi gibi faktorleri dikkatli bir sekilde dikkate alarak secmesini garanti eder. Bu dinamik arac secimi, harici API'lerin ve hizmetlerin kullanimini optimize ederek genel sistem verimliligini arttirir.

**Baglamsal Budama ve Ozetleme**, agent'lar tarafindan islenen bilgi miktarini yonetmede hayati bir rol oynar; prompt token sayisini stratejik olarak minimize eder ve etkileşim gecmisinden yalnizca en ilgili bilgileri akilli bir sekilde ozetleyip secici bir sekilde tutarak cikarim maliyetlerini azaltir ve gereksiz hesaplama yukunu onler.

**Proaktif Kaynak Tahmini**, gelecek is yuklerini ve sistem gereksinimlerini tahmin ederek kaynak taleplerini onceden bilmeyi icerir; bu da kaynaklarin proaktif tahsisi ve yonetimini mumkun kilerek sistem yanitlanabilirligini saglar ve darbogazlari onler.

**Maliyet Duyarli Kesif**, multi-agent sistemlerde optimizasyon hususlarini geleneksel hesaplama maliyetlerinin yanı sira iletisim maliyetlerini de kapsayacak sekilde genisletir; agent'larin is birligi yapma ve bilgi paylasma stratejilerini etkiler ve genel kaynak harcamasini minimize etmeyi amaclar.

**Enerji Verimli Konuslandirma**, ozellikle siki kaynak kisitlamalari olan ortamlar icin uyarlanmis olup akilli agent sistemlerinin enerji ayak izini minimize etmeyi, calisma suresini uzatmayi ve genel isletme maliyetlerini azaltmayi amaclar.

**Paralelizasyon (Parallelization) ve Dagitik Hesaplama Farkindaligi**, agent'larin isleme gucunu ve verimini artirmak icin dagitik kaynaklardan yararlanir; hesaplama is yuklerini daha yuksek verimlilik ve daha hizli gorev tamamlama icin birden fazla makine veya islemciye dagitir.

**Ogrenilmis Kaynak Tahsis Politikalari**, geri bildirim ve performans metriklerine dayali olarak agent'larin kaynak tahsis stratejilerini zaman icinde uyarlamasini ve optimize etmesini saglayan bir ogrenme mekanizmasi sunar ve surekli iyilestirme yoluyla verimliligi arttirir.

**Zarif Bozulma ve Fallback Mekanizmalari**, kaynak kisitlamalari ciddi olsa bile akilli agent sistemlerinin, belki de azaltilmis bir kapasitede, calismasya devam etmesini saglar; performansi zarif bir sekilde dusurup temel islevsellik saglamak ve isletimi surdurmek icin alternatif stratejilere yonelir.

## Bir Bakista

**Ne:** Kaynak Odakli Optimizasyon, akilli sistemlerde hesaplama, zaman ve finansal kaynaklarin tuketimini yonetme sorununu ele alir. LLM tabanli uygulamalar pahali ve yavas olabilir ve her gorev icin en iyi modeli veya araci secmek genellikle verimsizdir. Bu, bir sistemin ciktisinin kalitesi ile onu uretmek icin gereken kaynaklar arasinda temel bir odunlesim yaratir. Dinamik bir yonetim stratejisi olmadan sistemler, degisen gorev karmasikliklarina uyum saglayamaz veya butce ve performans kisitlamalari dahilinde calisamaz.

**Neden:** Standartlastirilmis cozum, mevcut goreve dayali olarak kaynaklari akilli bir sekilde izleyen ve tahsis eden bir agentic sistem olusturmaktir. Bu kalip, genellikle gelen bir istegin karmasikligini ilk olarak siniflandirmak icin bir "Router Agent" kullanir. Istek daha sonra en uygun LLM'e veya araca yonlendirilir; basit sorgular icin hizli, ucuz bir model, karmasik akil yurutme icin ise daha guclu bir model kullanilir. Bir "Elestiri Agent'i" (Critique Agent), yanitin kalitesini degerlendirerek ve zaman icinde yonlendirme mantigini iyilestirmek icin geri bildirim saglayarak sureci daha da iyilestirebilir. Bu dinamik, multi-agent yaklasim, sistemin verimli calismasini saglayarak yanit kalitesi ile maliyet etkinligi arasinda denge kurar.

**Temel Kural:** Bu kalibi, API cagrilari veya hesaplama gucu icin siki mali butceler altinda calisirken, hizli yanit surelerinin kritik oldugu gecikmeye duyarli uygulamalar olustururken, sinirli pil omru gibi kaynak kisitli donanim uzerinde agent'lar konuslandirirken, yanit kalitesi ile operasyonel maliyet arasindaki odunlesimi programatik olarak dengelemekte ve farkli gorevlerin degisen kaynak gereksinimlerine sahip oldugu karmasik, cok adimli is akislarini yonetirken kullanin.

**Gorsel Ozet:**

![Resource-Aware Optimization Design Pattern](../assets/Resource_Aware_Optimization_Design_Pattern.png)

Sekil 2: Kaynak Odakli Optimizasyon Tasarim Kalibi

## Onemli Cikarimlar

* Kaynak Odakli Optimizasyon Esastir: Akilli agent'lar hesaplama, zaman ve finansal kaynaklari dinamik olarak yonetebilir. Model kullanimi ve yurutme yollarina iliskin kararlar, gercek zamanli kisitlara ve hedeflere dayali olarak alinir.
* Olceklenebilirlik icin Multi-Agent Mimari: Google'in ADK'si, moduler tasarimi mumkun kilan bir multi-agent cercevesi saglar. Farkli agent'lar (yanitlama, yonlendirme, elestiri) belirli gorevleri ele alir.
* Dinamik, LLM Gudumlü Yonlendirme: Bir Router Agent, sorgu karmasikligina ve butceye dayali olarak sorgulari dil modellerine (basit icin Gemini Flash, karmasik icin Gemini Pro) yonlendirir. Bu, maliyet ve performansi optimize eder.
* Elestiri Agent'i Islevselliği: Ozel bir Elestiri Agent'i, kendini duzeltme, performans izleme ve yonlendirme mantigini iyilestirme icin geri bildirim saglar, sistem etkinligini arttirir.
* Geri Bildirim ve Esneklik ile Optimizasyon: Elestiri icin degerlendirme yetenekleri ve model entegrasyon esnekligi, uyarlanabilir ve kendini iyilestiren sistem davranisina katkida bulunur.
* Ek Kaynak Odakli Optimizasyonlar: Diger yontemler arasinda Uyarlanabilir Arac Kullanimi ve Secimi, Baglamsal Budama ve Ozetleme, Proaktif Kaynak Tahmini, Multi-Agent Sistemlerde Maliyet Duyarli Kesif, Enerji Verimli Konuslandirma, Paralelizasyon ve Dagitik Hesaplama Farkindaligi, Ogrenilmis Kaynak Tahsis Politikalari, Zarif Bozulma ve Fallback Mekanizmalari ve Kritik Gorevlerin Onceliklendirilmesi bulunur.

## Sonuclar

Kaynak odakli optimizasyon, akilli agent'larin gelistirilmesinde esastir ve gercek dunya kisitlamalari dahilinde verimli calismayi mumkun kilar. Hesaplama, zaman ve finansal kaynaklarin yonetilmesi sayesinde agent'lar optimal performans ve maliyet etkinligi elde edebilir. Dinamik model degistirme, uyarlanabilir arac kullanimi ve baglamsal budama gibi teknikler, bu verimlilige ulasmak icin hayati onem tasir. Ogrenilmis kaynak tahsis politikalari ve zarif bozulma gibi gelismis stratejiler, degisen kosullar altinda agent'in uyarlanabilirligini ve direncini arttirir. Bu optimizasyon ilkelerinin agent tasarimina entegre edilmesi, olceklenebilir, sagalm ve surdurulebilir yapay zeka sistemleri olusturmak icin esastir.

## Referanslar

1. Google's Agent Development Kit (ADK): [https://google.github.io/adk-docs/](https://google.github.io/adk-docs/)
2. Gemini Flash 2.5 & Gemini 2.5 Pro:  [https://aistudio.google.com/](https://aistudio.google.com/)
3. OpenRouter: [https://openrouter.ai/docs/quickstart](https://openrouter.ai/docs/quickstart)
