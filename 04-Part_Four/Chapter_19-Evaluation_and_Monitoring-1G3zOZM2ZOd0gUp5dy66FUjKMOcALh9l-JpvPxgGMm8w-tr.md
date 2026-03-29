# Bolum 19: Degerlendirme ve Izleme (Evaluation and Monitoring)

Bu bolum, akilli agent'larin performanslarini sistematik olarak degerlendirmelerine, hedeflere yonelik ilerlemeyi izlemelerine ve operasyonel anomalileri tespit etmelerine olanak taniyan metodolojileri incelemektedir. Bolum 11 hedef belirleme ve izlemeyi ana hatlariyla sunarken ve Bolum 17 Akil Yurutme (Reasoning) mekanizmalarini ele alirken, bu bolum bir agent'in etkinliginin, verimliliginin ve gereksinimlere uyumlulugunun surekli, genellikle harici olcumune odaklanir. Bu, metriklerin tanimlanmasini, geri bildirim dongularinin olusturulmasini ve agent performansinin operasyonel ortamlarda beklentilerle uyumlu olmasini saglayan raporlama sistemlerinin uygulanmasini icerir (bkz. Sekil 1).

![Monitoring and Evaluating Agent Performance](../assets/Monitoring_and_Evaluating_Agent_Performance.png)

Sekil 1: Degerlendirme ve izleme icin en iyi uygulamalar

## Pratik Uygulamalar ve Kullanim Alanlari

En Yaygin Uygulamalar ve Kullanim Alanlari:

* **Canli Sistemlerde Performans Izleme:** Uretim ortaminda konuslandirilmis bir agent'in dogrulugunu, gecikmesini ve kaynak tuketimini surekli olarak izleme (ornegin bir musteri hizmetleri chatbot'unun cozum orani, yanit suresi).
* **Agent Iyilestirmeleri icin A/B Testi:** Optimal yaklasimlari belirlemek icin farkli agent surumlerinin veya stratejilerinin performansini paralel olarak sistematik olarak karsilastirma (ornegin bir lojistik agent'i icin iki farkli planlama algoritmasi deneme).
* **Uyumluluk ve Guvenlik Denetimleri:** Bir agent'in etik yonergelere, duzenleyici gereksinimlere ve guvenlik protokollerine uyumunu zaman icinde izleyen otomatik denetim raporlari olusturma. Bu raporlar, bir human-in-the-loop veya baska bir agent tarafindan dogrulanabilir ve KPI'lar olusturabilir veya sorunlari tespit ettiginde uyarilar tetikleyebilir.
* **Kurumsal Sistemler:** Kurumsal sistemlerde Agentic AI'yi yonetmek icin yeni bir kontrol araci olan yapay zeka "Sozlesmesi" gereklidir. Bu dinamik anlasma, yapay zekaya devredilen gorevlerin hedeflerini, kurallarini ve kontrollerini kodlar.
* **Sapma Tespiti:** Bir agent'in ciktiilarinin zamanla ilgilligini veya dogrulugunu izleme, girdi veri dagilimindaki degisiklikler (kavram sapması) veya cevresel kaymalar nedeniyle performansinin ne zaman dusutugunu tespit etme.
* **Agent Davranisinda Anomali Tespiti:** Bir agent tarafindan alinan, bir hata, kotu niyetli bir saldiri veya ortaya cikan istenmeyen bir davranisi gosterebilecek olagan disi veya beklenmedik eylemleri tespit etme.
* **Ogrenme (Learning) Ilerleme Degerlendirmesi:** Ogrenmek icin tasarlanmis agent'lar icin, ogrenme egrilerini, belirli becerilerdeki gelismelerini veya farkli gorevler veya veri setleri uzerindeki genelleme yeteneklerini izleme.

## Uygulamali Kod Ornegi

Yapay zeka agent'lari icin kapsamli bir degerlendirme cercevesi gelistirmek, karmasikligi acisindan akademik bir disiplin veya kapsamli bir yayin ile karsilastiriliabilecek zorlukta bir girisimdir. Bu zorluk, model performansi, kullanici etkilesimi, etik etkiler ve daha genis toplumsal etki gibi dikkate alinmasi gereken cok sayida faktordan kaynaklanmaktadir. Yine de pratik uygulama icin odak, yapay zeka agent'larinin verimli ve etkili islevi icin gerekli kritik kullanim alanlarina daraltilabilir.

**Agent Yanit Degerlendirmesi:** Bu temel surec, bir agent'in ciktiilarinin kalitesini ve dogrulugunu degerlendirmek icin esastir. Agent'in verilen girdilere yanit olarak ilgili, dogru, mantikli, onyargisiz ve doğru bilgi saglarip saglamadigini belirlemeyi icerir. Degerlendirme metrikleri olgusal dogruluk, akicilik, dilbilgisel hassasiyet ve kullanicinin amacladigi amaca baglilik icerebilir.

```python
def evaluate_response_accuracy(agent_output: str, expected_output: str) -> float:
    """Calculates a simple accuracy score for agent responses."""
    # This is a very basic exact match; real-world would use more sophisticated metrics
    return 1.0 if agent_output.strip().lower() == expected_output.strip().lower() else 0.0


# Example usage
agent_response = "The capital of France is Paris."
ground_truth = "Paris is the capital of France."
score = evaluate_response_accuracy(agent_response, ground_truth)
print(f"Response accuracy: {score}")
```

`evaluate_response_accuracy` Python fonksiyonu, agent'in ciktisi ile beklenen ciktiyi basa ve sona bosluklar cikartilip kucuk harfe donusturdukten sonra birebir, buyuk/kucuk harf duyarsiz karsilastirma yaparak bir yapay zeka agent'inin yaniti icin temel bir dogruluk puani hesaplar. Birebir eslesme icin 1.0, aksi halde 0.0 puani dondurur ve ikili dogru veya yanlis degerlendirmeyi temsil eder. Bu yontem, basit kontroller icin yeterli olsa da, ifade farklilikları veya anlamsal esdegerlik gibi durumlari hesaba katmaz.

Sorun, karsilastirma yonteminde yatmaktadir. Fonksiyon, iki dize arasinda kati, karakter karakter karsilastirma yapar. Saglanan ornekte:

* `agent_response`: "The capital of France is Paris."
* `ground_truth`: "Paris is the capital of France."

Bosluklar cikarilip kucuk harfe donusturdukten sonra bile bu iki dize ayni degildir. Sonuc olarak fonksiyon, her iki cumle de ayni anlami ifade etmesine ragmen yanlis bir sekilde `0.0` dogruluk puani dondurecektir.

Basit bir karsilastirma, anlamsal benzerligi degerlendirmede yetersiz kalir; yalnizca bir agent'in yaniti beklenen ciktiyla tamamen eslestigi durumda basarili olur. Daha etkili bir degerlendirme, cumleler arasindaki anlami ayirt etmek icin gelismis Dogal Dil Isleme (NLP) teknikleri gerektirir. Gercek dunya senaryolarinda kapsamli yapay zeka agent degerlendirmesi icin genellikle daha sofistike metrikler vazgecilmezdir. Bu metrikler; Levenshtein mesafesi ve Jaccard benzerligi gibi Dize Benzerlik Olcumleri, belirli anahtar kelimelerin varligi veya yoklugu icin Anahtar Kelime Analizi, embedding modelleriyle kosinus benzerligi kullanan Anlamsal Benzerlik, LLM-as-a-Judge Degerlendirmeleri (nüansli dogruluk ve yardimciligi degerlendirmek icin daha sonra tartisilan) ve sadakat ile ilgililik gibi RAG'a Ozgu Metrikleri kapsayabilir.

**Gecikme Izleme:** Agent Eylemleri icin Gecikme Izleme, bir yapay zeka agent'inin yanit veya eylem hizinin kritik bir faktor oldugu uygulamalarda hayati onem tasir. Bu surec, bir agent'in istekleri islemek ve ciktilar olusturmak icin gerektirdigu sureyi olcer. Yuksek gecikme, ozellikle gercek zamanli veya etkilesimli ortamlarda kullanici deneyimini ve agent'in genel etkinligini olumsuz etkileyebilir. Pratik uygulamalarda, gecikme verilerini konsola yazdirmak yeterli degildir. Bu bilgilerin kalici bir depolama sistemine kaydedilmesi onerilir. Secenekler arasinda yapilandirilmis gunluk dosyalari (ornegin JSON), zaman serisi veritabanlari (ornegin InfluxDB, Prometheus), veri ambarlari (ornegin Snowflake, BigQuery, PostgreSQL) veya gozlemlenebilirlik platformlari (ornegin Datadog, Splunk, Grafana Cloud) bulunur.

**LLM Etkilesimleri icin Token Kullanim Izleme:** LLM destekli agent'lar icin token kullanimi izleme, maliyetleri yonetmek ve kaynak tahsisini optimize etmek icin hayati onem tasir. LLM etkileşimleri icin faturalandirma genellikle islenen token sayisina (girdi ve cikti) baglidir. Bu nedenle verimli token kullanimi, operasyonel giderleri dogrudan azaltir. Ek olarak, token sayilarini izlemek, prompt muhendisligi veya yanit olusturma sureclerinde potansiyel iyilestirme alanlarini belirlemeye yardimci olur.

```python
# This is conceptual as actual token counting depends on the LLM API
class LLMInteractionMonitor:
    def __init__(self):
        self.total_input_tokens = 0
        self.total_output_tokens = 0

    def record_interaction(self, prompt: str, response: str):
        # In a real scenario, use LLM API's token counter or a tokenizer
        input_tokens = len(prompt.split())  # Placeholder
        output_tokens = len(response.split())  # Placeholder
        self.total_input_tokens += input_tokens
        self.total_output_tokens += output_tokens
        print(f"Recorded interaction: Input tokens={input_tokens}, Output tokens={output_tokens}")

    def get_total_tokens(self):
        return self.total_input_tokens, self.total_output_tokens


# Example usage
monitor = LLMInteractionMonitor()
monitor.record_interaction("What is the capital of France?", "The capital of France is Paris.")
monitor.record_interaction("Tell me a joke.", "Why don't scientists trust atoms? Because they make up everything!")
input_t, output_t = monitor.get_total_tokens()
print(f"Total input tokens: {input_t}, Total output tokens: {output_t}")
```

Bu bolum, buyuk dil modeli etkilesimlerinde token kullanimini izlemek icin tasarlanmis kavramsal bir Python sinifi olan `LLMInteractionMonitor`'u sunar. Sinif, hem girdi hem de cikti token'lari icin sayaclar icerir. `record_interaction` yontemi, prompt ve yanit dizelerini bolerek token sayimini simule eder. Pratik bir uygulamada, hassas token sayimlari icin belirli LLM API tokenizer'lari kullanilacaktir. Etkilesimler gerceklestikce monitor, toplam girdi ve cikti token sayilarini biriktirir. `get_total_tokens` yontemi, maliyet yonetimi ve LLM kullanim optimizasyonu icin onemli olan bu kumülatif toplamlara erisim saglar.

**LLM-as-a-Judge Kullanarak "Yardimcilik" icin Ozel Metrik:** Bir yapay zeka agent'inin "yardimciligi" gibi oznel nitelikleri degerlendirmek, standart nesnel metriklerin otesinde zorluklar sunar. Potansiyel bir cerceve, bir LLM'in degerlendirici olarak kullanimini icerir. Bu LLM-as-a-Judge yaklasimi, baska bir yapay zeka agent'inin ciktisini "yardimcilik" icin onceden tanimlanmis kriterlere dayali olarak degerlendirir. LLM'lerin gelismis dilbilimsel yeteneklerinden yararlanarak bu yontem, basit anahtar kelime eslestirme veya kural tabanli degerlendirmeleri asan nüansli, insan benzeri oznel nitelik degerlendirmeleri sunar. Hala gelistirme asamasinda olsa da, bu teknik niteliksel degerlendirmeleri otomatiklestirme ve olceklendirme acisindan umut vermektedir.

```python
import os
import json
import logging
from typing import Optional

import google.generativeai as genai

# --- Configuration ---
logging.basicConfig(level=logging.INFO, format='%(asctime)s - %(levelname)s - %(message)s')

# Set your API key as an environment variable to run this script
# For example, in your terminal: export GOOGLE_API_KEY='your_key_here'
try:
    genai.configure(api_key=os.environ["GOOGLE_API_KEY"])
except KeyError:
    logging.error("Error: GOOGLE_API_KEY environment variable not set.")
    exit(1)

# --- LLM-as-a-Judge Rubric for Legal Survey Quality ---
LEGAL_SURVEY_RUBRIC = """
 You are an expert legal survey methodologist and a critical legal reviewer. Your task is to evaluate the quality of a given legal survey question. Provide a score from 1 to 5 for overall quality, along with a detailed rationale and specific feedback.

 Focus on the following criteria:

 1.  **Clarity & Precision (Score 1-5):**
    * 1: Extremely vague, highly ambiguous, or confusing.
    * 3: Moderately clear, but could be more precise.
    * 5: Perfectly clear, unambiguous, and precise in its legal terminology (if applicable) and intent.

 2.  **Neutrality & Bias (Score 1-5):**
    * 1: Highly leading or biased, clearly influencing the respondent towards a specific answer.
    * 3: Slightly suggestive or could be interpreted as leading.
    * 5: Completely neutral, objective, and free from any leading language or loaded terms.

 3.  **Relevance & Focus (Score 1-5):**
    * 1: Irrelevant to the stated survey topic or out of scope.
    * 3: Loosely related but could be more focused.
    * 5: Directly relevant to the survey's objectives and well-focused on a single concept.

 4.  **Completeness (Score 1-5):**
    * 1: Omits critical information needed to answer accurately or provides insufficient context.
    * 3: Mostly complete, but minor details are missing.
    * 5: Provides all necessary context and information for the respondent to answer thoroughly.

 5.  **Appropriateness for Audience (Score 1-5):**
    * 1: Uses jargon inaccessible to the target audience or is overly simplistic for experts.
    * 3: Generally appropriate, but some terms might be challenging or oversimplified.
    * 5: Perfectly tailored to the assumed legal knowledge and background of the target survey audience.

 **Output Format:**
 Your response MUST be a JSON object with the following keys:
 * `overall_score`: An integer from 1 to 5 (average of criterion scores, or your holistic judgment).
 * `rationale`: A concise summary of why this score was given, highlighting major strengths and weaknesses.
 * `detailed_feedback`: A bullet-point list detailing feedback for each criterion (Clarity, Neutrality, Relevance, Completeness, Audience Appropriateness). Suggest specific improvements.
 * `concerns`: A list of any specific legal, ethical, or methodological concerns.
 * `recommended_action`: A brief recommendation (e.g., "Revise for neutrality", "Approve as is", "Clarify scope").
"""

class LLMJudgeForLegalSurvey:
    """A class to evaluate legal survey questions using a generative AI model."""

    def __init__(self, model_name: str = 'gemini-1.5-flash-latest', temperature: float = 0.2):
        """
        Initializes the LLM Judge.

        Args:
            model_name (str): The name of the Gemini model to use.
                              'gemini-1.5-flash-latest' is recommended for speed and cost.
                              'gemini-1.5-pro-latest' offers the highest quality.
            temperature (float): The generation temperature. Lower is better for deterministic evaluation.
        """
        self.model = genai.GenerativeModel(model_name)
        self.temperature = temperature

    def _generate_prompt(self, survey_question: str) -> str:
        """Constructs the full prompt for the LLM judge."""
        return f"{LEGAL_SURVEY_RUBRIC}\n\n---\n**LEGAL SURVEY QUESTION TO EVALUATE:**\n{survey_question}\n---"

    def judge_survey_question(self, survey_question: str) -> Optional[dict]:
        """
        Judges the quality of a single legal survey question using the LLM.

        Args:
            survey_question (str): The legal survey question to be evaluated.

        Returns:
            Optional[dict]: A dictionary containing the LLM's judgment, or None if an error occurs.
        """
        full_prompt = self._generate_prompt(survey_question)

        try:
            logging.info(f"Sending request to '{self.model.model_name}' for judgment...")
            response = self.model.generate_content(
                full_prompt,
                generation_config=genai.types.GenerationConfig(
                    temperature=self.temperature,
                    response_mime_type="application/json"
                )
            )

            # Check for content moderation or other reasons for an empty response.
            if not response.parts:
                safety_ratings = response.prompt_feedback.safety_ratings
                logging.error(f"LLM response was empty or blocked. Safety Ratings: {safety_ratings}")
                return None

            return json.loads(response.text)
        except json.JSONDecodeError:
            logging.error(f"Failed to decode LLM response as JSON. Raw response: {response.text}")
            return None
        except Exception as e:
            logging.error(f"An unexpected error occurred during LLM judgment: {e}")
            return None


# --- Example Usage ---
if __name__ == "__main__":
    judge = LLMJudgeForLegalSurvey()

    # --- Good Example ---
    good_legal_survey_question = """
    To what extent do you agree or disagree that current intellectual property laws in Switzerland adequately protect emerging AI-generated content, assuming the content meets the originality criteria established by the Federal Supreme Court?
    (Select one: Strongly Disagree, Disagree, Neutral, Agree, Strongly Agree)
    """
    print("\n--- Evaluating Good Legal Survey Question ---")
    judgment_good = judge.judge_survey_question(good_legal_survey_question)
    if judgment_good:
        print(json.dumps(judgment_good, indent=2))

    # --- Biased/Poor Example ---
    biased_legal_survey_question = """
    Don't you agree that overly restrictive data privacy laws like the FADP are hindering essential technological innovation and economic growth in Switzerland?
    (Select one: Yes, No)
    """
    print("\n--- Evaluating Biased Legal Survey Question ---")
    judgment_biased = judge.judge_survey_question(biased_legal_survey_question)
    if judgment_biased:
        print(json.dumps(judgment_biased, indent=2))

    # --- Ambiguous/Vague Example ---
    vague_legal_survey_question = """
    What are your thoughts on legal tech?
    """
    print("\n--- Evaluating Vague Legal Survey Question ---")
    judgment_vague = judge.judge_survey_question(vague_legal_survey_question)
    if judgment_vague:
        print(json.dumps(judgment_vague, indent=2))
```

Python kodu, uretken bir yapay zeka modeli kullanarak hukuki anket sorularinin kalitesini degerlendirmek icin tasarlanmis bir LLMJudgeForLegalSurvey sinifi tanimlar. Gemini modelleriyle etkilesim kurmak icin google.`generativeai` kutuphanesini kullanir.

Temel islevsellik, bir anket sorusunu degerlendirme icin ayrintili bir rubrikle birlikte modele gondermeyi icerir. Rubrik, anket sorularini degerlendirmek icin bes kriter belirler: Netlik ve Hassasiyet, Tarafsizlik ve Onyargi, Ilgililik ve Odak, Tamlık ve Hedef Kitleye Uygunluk. Her kriter icin 1'den 5'e kadar bir puan atanir ve ciktida ayrintili bir gerekce ve geri bildirim istenir. Kod, rubrigi ve degerlendirilecek anket sorusunu iceren bir prompt olusturur.

`judge_survey_question` yontemi, bu prompt'u yapilandirilmis Gemini modeline gonderir ve tanimlanan yapiya gore biçimlendirilmis bir JSON yaniti talep eder. Beklenen cikti JSON'u, genel bir puan, ozet gerekce, her kriter icin ayrintili geri bildirim, kaygılar listesi ve onerilen bir eylemi icerir. Sinif, yapay zeka modeli etkilesimi sirasindaki potansiyel hatalari, JSON cozme sorunlari veya bos yanitlar gibi durumlari ele alir. Betik, hukuki anket sorularina iliskin ornekleri degerlendirerek isleyisini gosterir ve yapay zekanin onceden tanimlanmis kriterlere dayali olarak kaliteyi nasil degerlendirdigini gosterir.

Sonuca varmadan once, cesitli degerlendirme yontemlerini guclu ve zayif yonleriyle birlikte inceleyelim.

| Degerlendirme Yontemi | Guclu Yanlar | Zayif Yanlar |
| :---- | :---- | :---- |
| Insan Degerlendirmesi | Ince davranislari yakalar | Olceklendirmesi zor, pahali ve zaman alici; cunku oznel insan faktorlerini dikkate alir. |
| LLM-as-a-Judge | Tutarli, verimli ve olceklenebilir. | Ara adimlar gozden kacabilir. LLM yetenekleriyle sinirlidir. |
| Otomatik Metrikler | Olceklenebilir, verimli ve nesnel | Tam yetenekleri yakalamada potansiyel sinirlama. |

## Agent Yollari

Agent'larin yollarini degerlendirmek esastir cunku geleneksel yazilim testleri yetersizdir. Standart kod ongorulebiilir basari/basarisizlik sonuclari verirken, agent'lar olasiliksal olarak calisir ve hem nihai ciktinin hem de agent'in yolunun (bir cozume ulasmak icin atilan adimlar dizisi) niteliksel olarak degerlendirilmesini gerektirir. Multi-agent sistemleri degerlendirmek zorlayicidir cunku surekli degisim halindedirler. Bu, bireysel performansin otesinde iletisim ve ekip calismasinin etkinligini olcen sofistike metriklerin gelistirilmesini gerektirir. Dahasi, ortamlarin kendileri statik degildir ve test senaryolari dahil degerlendirme yontemlerinin zaman icinde uyum saglamasini talep eder.

Bu, kararlarin kalitesini, akil yurutme surecini ve genel sonucu incelemeyi icerir. Otomatik degerlendirmelerin uygulanmasi, ozellikle prototip asamasinin otesindeki gelistirme icin degerlidir. Yol ve arac kullanim analizi, bir agent'in bir hedefe ulasmak icin kullandigi adimlarin degerlendirilmesini icerir; arac secimi, stratejiler ve gorev verimliligi gibi. Ornegin, bir musterinin urun sorgusunu ele alan bir agent, ideal olarak niyet belirleme, veritabani arama araci kullanimi, sonuc inceleme ve rapor olusturma iceren bir yolu izleyebilir. Agent'in gercek eylemleri, hatalari ve verimsizlikleri belirlemek icin bu beklenen veya temel dogru yol ile karsilastirilir. Karsilastirma yontemleri arasinda birebir eslesme (ideal diziye mukemmel eslesme gerektiren), siranli eslesme (sirada dogru eylemler, ekstra adimlara izin veren), herhangi bir sirada eslesme (herhangi bir sirada dogru eylemler, ekstra adimlara izin veren), hassasiyet (tahmin edilen eylemlerin ilgilligini olcen), geri cagirma (ne kadar temel eylemin yakalandigini olcen) ve tek arac kullanimi (belirli bir eylemi kontrol eden) yer alir. Metrik secimi belirli agent gereksinimlerine baglidir; yuksek riskli senaryolar birebir esleme gerektirebilirken, daha esnek durumlar siranli veya herhangi bir sirada eslemeyi kullanabilir.

Yapay zeka agent'larinin degerlendirmesi iki temel yaklasimi icerir: test dosyalari ve evalset dosyalari kullanma. JSON formatindaki test dosyalari, tek, basit agent-model etkilesimlerini veya oturumlari temsil eder ve aktif gelistirme sirasindaki birim testleri icin idealdir; hizli yurutme ve basit oturum karmasikligina odaklanir. Her test dosyasi, bir kullanicinin sorgusu, beklenen arac kullanim yolu, ara agent yanitlari ve nihai yaniti iceren birden fazla tur bulunan tek bir oturum icerir. Ornegin, bir test dosyasi "Yatak Odasindaki `device_2`'yi kapat" kullanici istegini ayrintili olarak icerebilir; agent'in location: Bedroom, `device_id: device_2` ve status: OFF gibi parametrelerle bir `set_device_info` aracini kullanmasini ve "`device_2` durumunu kapali olarak ayarladim." beklenen nihai yaniti belirleyebilir. Test dosyalari klasorlere duzenlenebilir ve degerlendirme kriterlerini tanimlamak icin bir `test_config`.json dosyasi icerebilir. Evalset dosyalari, etkilesimleri degerlendirmek icin "evalset" adli bir veri seti kullanir; karmasik, cok turlu konusmalari ve entegrasyon testlerini simule etmeye uygun birden fazla potansiyel olarak uzun oturum icerir. Bir evalset dosyasi, her biri kullanici sorgulari, beklenen arac kullanimi, ara yanitlar ve referans nihai yanit iceren bir veya daha fazla "tur" ile ayri bir oturumu temsil eden birden fazla "eval" icerir. Ornek bir evalset, kullanicinin once "Ne yapabilirsin?" diye sordugu ve ardindan "10 yuzlu bir zari iki kere at ve sonra 9'un asal olup olmadigini kontrol et" dedigi, beklenen `roll_die` arac cagirilari ve bir `check_prime` arac cagrisini, zar atislari ve asal kontrolunu ozetleyen nihai yanitin yaninda tanimlayan bir oturum icerebilir.

**Multi-agent'lar:** Birden fazla agent iceren karmasik bir yapay zeka sistemini degerlendirmek, bir takim projesini degerlendirmeye cok benzer. Bircok adim ve devir islemi oldugundan, karmasikligi bir avantajdir ve her asamada is kalitesini kontrol etmenize olanak tanir. Her bireysel "agent"in belirli isini ne kadar iyi yaptigini inceleyebilirsiniz, ancak tum sistemin bir butun olarak nasil performans gosterdigini de degerlendirmeniz gerekir.

Bunu yapmak icin, somut orneklerle desteklenen takimin dinamikleri hakkinda onemli sorular sorarsınız:

* Agent'lar etkili bir sekilde is birligi yapiyor mu? Ornegin, bir "Ucus Rezervasyon Agent'i" bir ucus ayarladiktan sonra dogru tarihleri ve varisı noktasini "Otel Rezervasyon Agent'ina" basariyla iletiyor mu? Is birligindeki bir basarisizlik, otelin yanlis hafta icin rezerve edilmesine yol acabilir.
* Iyi bir plan yaptilar mi ve buna sadik kaldilar mi? Planin once ucus, ardindan otel rezervasyonu oldugunu dusunun. "Otel Agent'i" ucus onaylanmadan bir oda rezerve etmeye calisiyorsa, plandan sapmis demektir. Ayrica bir agent'in takilip kalip kalmadigini da kontrol edersiniz; ornegin, surekli "mukemmel" bir kiralik araba ariyip bir sonraki adima hic gecemiyor olmasi gibi.
* Dogru gorev icin dogru agent seciliyor mu? Bir kullanici seyahati icin hava durumunu sorarsa, sistem canli veri saglayan uzmanlasmis bir "Hava Durumu Agent'i" kullanmalidir. Bunun yerine "yazlari genellikle sıcak olur" gibi genel bir yanit veren bir "Genel Bilgi Agent'i" kullaniyorsa, is icin yanlis araci secmis demektir.
* Son olarak, daha fazla agent eklemek performansi iyilestiriyor mu? Takima yeni bir "Restoran Rezervasyon Agent'i" eklerseniz, genel seyahat planlamasini daha iyi ve daha verimli hale getiriyor mu? Yoksa catismalar yaratip sistemi yavaslatarak olceklenebilirlikle ilgili bir sorun mu oldugunu gosteriyor?

## Agent'lardan Gelismis Yuklenicilere

Yakin zamanda, basit yapay zeka agent'larindan gelismis "yuklenicilere" gecis onerilmistir (Agent Companion, gulli ve ark.); olasiliksal, genellikle guvenilmez sistemlerden karmasik, yuksek riskli ortamlar icin tasarlanmis daha deterministik ve hesap verebilir sistemlere gecis (bkz. Sekil 2).

Gunumuzde yaygin yapay zeka agent'lari kisa, yetersiz tanimlara sahip talimatlarla calisir; bu da onlari basit gosterimler icin uygun kilsa da uretimde kirilgan yapar; belirsizlik basarisizliga yol acar. "Yuklenici" modeli, insan dunayasindaki yasal bir hizmet anlasmasina benzer sekilde, acikca tanimlanmis ve karslikli uzerinde mutabik kalinmis sartlar uzerine insa edilmis, kullanici ile yapay zeka arasinda titiz ve resmi bir iliski kurarak bunu ele alir. Bu donusum, daha once otonom sistemlerin kapsamı disinda kalan gorevlerin netligini, guvenilirligini ve saglam bir sekilde yurutulmesini topluca saglayan dort temel sutun tarafindan desteklenir.

Birincisi, bir gorev icin tek dogru kaynak olarak hizmet eden ayrintili bir sartname olan Resmi Sozlesme sutunudur. Basit bir prompt'un cok otesine gecer. Ornegin, bir finansal analiz gorevi icin bir sozlesme yalnizca "gecen ceyregin satislarini analiz et" demez; "Q1 2025 Avrupa pazari satislarini analiz eden, bes belirli veri gorsellestirmesi, Q1 2024 ile karsilastirmali analiz ve dahil edilen tedarik zinciri kesintileri veri setine dayali bir risk degerlendirmesi iceren 20 sayfalik bir PDF rapor" talep eder. Bu sozlesme, gerekli teslim edebilirlikleri, hassas sartnamelerini, kabul edilebilir veri kaynaklarini, is kapsamini ve hatta beklenen hesaplama maliyeti ve tamamlanma suresini acikca tanimlar ve sonucu nesnel olarak dogrulanabilir kilar.

Ikincisi, Dinamik Muzakere ve Geri Bildirim Yasam Dongusu sutunudur. Sozlesme statik bir komut degil, bir diyalogun baslangicidir. Yuklenici agent, ilk sartlari analiz edebilir ve muzakere edebilir. Ornegin, bir sozlesme agent'in erisemedigi belirli bir tescilli veri kaynaginin kullanimini talep ederse, "Belirtilen XYZ veritabani erisiilebilir degil. Lutfen kimlik bilgileri saglayin veya verilerin ayrintilik derecesini hafifce degistirebilecek alternatif bir genel veritabaninin kullanimini onaylayin." diye geri bildirim dondurulur. Ayrica agent'in belirsizlikleri veya potansiyel riskleri isaretlemesine de izin veren bu muzakere asamasi, yurutme baslamadan once yanlis anlamalari cozer, maliyetli basarisizliklari onler ve nihai ciktinin kullanicinin gercek niyetiyle mukemmel bir sekilde uyumlu olmasini saglar.

![Contract Execution Example Among Agents](../assets/Contract_Execution_Example_Among_Agents.png)

Sekil 2: Agent'lar arasi sozlesme yurutme ornegi

Ucuncu sutun, Kalite Odakli Yinelemeli Yurutmedir. Dusuk gecikmeli yanitlar icin tasarlanmis agent'lardan farkli olarak, bir yuklenici dogrulugu ve kaliteyi on planda tutar. Kendini dogrulama ve duzeltme ilkesiyle calisir. Bir kod olusturma sozlesmesi icin, ornegin, agent yalnizca kodu yazmaz; birden fazla algoritmik yaklasim olusturur, bunlari sozlesme icinde tanimlanan birim testlerine karsi derleyip calistirir, her cozumu performans, guvenlik ve okunabilirlik gibi metriklere gore puanlar ve yalnizca tum dogrulama kriterlerini gecen surumu sunar. Sozlesmenin sartnameleri karsilanana kadar kendi calismasini olusturma, inceleme ve iyilestirme ic dongusu, ciktilarina guven olusturmak icin hayati onem tasir.

Son olarak, dorduncu sutun Alt Sozlesmeler Araciligiyla Hiyerarsik Ayristirmadir. Onemli karmasikliktaki gorevler icin, birincil bir yuklenici agent bir proje yoneticisi olarak hareket edebilir ve ana hedafi daha kucuk, daha yonetilebilir alt gorevlere ayirabilir. Bunu, yeni, resmi "alt sozlesmeler" olusturarak basarir. Ornegin, "bir e-ticaret mobil uygulamasi olustur" ana sozlesmesi, birincil agent tarafindan "UI/UX tasarimi", "kullanici kimlik doğrulama modulu gelistirme", "urun veritabani semasi olusturma" ve "odeme gecidi entegrasyonu" icin alt sozlesmelere ayristirılabilir. Bu alt sozlesmelerin her biri, kendi teslimleri ve sartnameleri olan tam, bagimsiz bir sozlesmedir ve diger uzman agent'lara atanabilir. Bu yapilandirilmis ayristirma, sistemin devasa, cok yonlu projeleri son derece organize ve olceklenebilir bir sekilde ele almasina olanak tanir ve yapay zekanin basit bir aractan gercekten otonom ve guvenilir bir problem cozme motoruna gecisini isaret eder.

Nihayetinde, bu yuklenici cercevesi, resmi sartname, muzakere ve dogrulanabilir yurutme ilkelerini dogrudan agent'in temel mantigina gomerek yapay zeka etkilesimini yeniden tasarlar. Bu metodik yaklasim, yapay zekayi umut verici ancak genellikle ongorulemeyen bir asistandan, karmasik projeleri denetlenebilir hassasiyetle ozerk olarak yonetebilen guvenilir bir sisteme yukseltir. Belirsizlik ve guvenilirligin kritik zorluklarini cozerek, bu model guven ve hesap verebilirligin en onemli oldugu gorev-kritik alanlarda yapay zekanin konuslandirilmasinin yolunu acar.

## Google'in ADK'si

Sonuca varmadan once, degerlendirmeyi destekleyen bir cercvenin somut bir ornegine bakalim. Google'in ADK'si ile agent degerlendirmesi (bkz. Sekil 3) uc yontemle yurutullebilir: etkilesimli degerlendirme ve veri seti olusturma icin web tabanli kullanici arayuzu (adk web), test pipeline'larina dahil etmek icin pytest kullanan programatik entegrasyon ve duzenli derleme olusturma ve dogrulama surecleri icin uygun otomatik degerlendirmeler icin dogrudan komut satiri arayuzu (adk eval).

![Evaluation Support for Google ADK](../assets/Evaluation_Support_for_Google_ADK.png)

Sekil 3: Google ADK icin Degerlendirme Destegi

Web tabanli kullanici arayuzu, mevcut veya yeni eval setlerine etkilesimli oturum olusturma ve kaydetmeyi saglar ve degerlendirme durumunu goruntüler. Pytest entegrasyonu, agent modülü ve test dosyasi yolunu belirterek AgentEvaluator.evaluate cagirarak test dosyalarinin entegrasyon testlerinin bir parcasi olarak calistirilmasina olanak tanir.

Komut satiri arayuzu, agent modulu yolu ve eval set dosyasini saglayarak otomatik degerlendirmeyi kolaylastirir; bir yapilandirma dosyasi belirtme veya ayrintili sonuclari yazdirma secenekleri sunar. Daha buyuk bir eval seti icindeki belirli eval'ler, eval set dosya adindan sonra virgullerle ayrılarak yürütme icin secilebilir.

## Bir Bakista

**Ne:** Agentic sistemler ve LLM'ler, performanslarinin zaman icinde dusebilecegi karmasik, dinamik ortamlarda calisir. Olasiliksal ve deterministik olmayan yapilari, guvenilirligin saglanmasi icin geleneksel yazilim testlerinin yetersiz oldugu anlamina gelir. Dinamik multi-agent sistemleri degerlendirmek, surekli degisen yapilari ve ortamlarinin, bireysel performansin otesinde is birlikci basariyi olcebilen uyarlanabilir test yontemleri ve sofistike metriklerin gelistirilmesini talep etmesi nedeniyle onemli bir zorluktur. Veri sapmasi, beklenmedik etkilesimler, arac cagilari ve amacanan hedeflerden sapmalar gibi sorunlar konuslandirmadan sonra ortaya cikabilir. Bu nedenle, bir agent'in etkinligini, verimliligini ve operasyonel ve guvenlik gereksinimlerine bagliliğini olcmek icin surekli degerlendirme gereklidir.

**Neden:** Standartlastirilmis bir degerlendirme ve izleme cercevesi, akilli agent'larin devam eden performansini degerlendirmek ve saglamak icin sistematik bir yol saglar. Bu, dogruluk, gecikme ve LLM'ler icin token kullanimi gibi kaynak tuketimi icin net metrikler tanimlmayi icerir. Ayrica, akil yurutme surecini anlamak icin agentic yollarin analizi ve nüansli, niteliksel degerlendirmeler icin LLM-as-a-Judge kullanimi gibi gelismis teknikleri de kapsar. Geri bildirim donguları ve raporlama sistemleri olusturarak, bu cerceve surekli iyilestirme, A/B testi ve anomali veya performans sapması tespiti saglar ve agent'in hedefleriyle uyumlu kalmasini garanti eder.

**Temel Kural:** Bu kalibi, gercek zamanli performans ve guvenilirligin kritik oldugu canli, uretim ortamlarinda agent'lar konuslandirirken kullanin. Ayrica, iyilestirmeleri yonlendirmek icin bir agent'in veya alttyatan modellerinin farkli surumlerini sistematik olarak karsilastirmak gerektiginde ve uyumluluk, guvenlik ve etik denetimler gerektiren duzenelmis veya yuksek riskli alanlarda calisirken kullanin. Bu kalip, veri veya ortamdaki degisiklikler nedeniyle (sapma) bir agent'in performansi zaman icinde dusulerse veya eylem dizisi (yol) ve yardimcilik gibi oznel ciktilarin kalitesi dahil karmasik agentic davranisi degerlendirilirken de uygundur.

**Gorsel Ozet:**

![Evaluation and Monitoring Design Pattern](../assets/Evaluation_and_Monitoring_Design_Pattern.png)

Sekil 4: Degerlendirme ve Izleme tasarim kalibi

## Onemli Cikarimlar

* Akilli agent'lari degerlendirmek, gercek dunya ortamlarinda etkinliklerini, verimliliklerini ve gereksinimlere uyumluluklarini surekli olarak olcmek icin geleneksel testlerin otesine gecer.
* Agent degerlendirmesinin pratik uygulamalari arasinda canli sistemlerde performans izleme, iyilestirmeler icin A/B testi, uyumluluk denetimleri ve davranistaki sapma veya anomalilerin tespiti bulunur.
* Temel agent degerlendirmesi yanit dogrulugunu degerlendirmeyi icerirken, gercek dunya senaryolari LLM destekli agent'lar icin gecikme izleme ve token kullanim izleme gibi daha sofistike metrikler gerektirir.
* Agent yollari, bir agent'in attigi adimlar dizisi, degerlendirme icin hayati onem tasir; hatalari ve verimsizlikleri belirlemek icin gercek eylemleri ideal, temel dogru yolla karsilastirir.
* ADK, birim testleri icin bireysel test dosyalari ve entegrasyon testleri icin kapsamli evalset dosyalari araciligiyla yapilandirilmis degerlendirme yontemleri saglar; her ikisi de beklenen agent davranisini tanimlar.
* Agent degerlendirmeleri, etkilesimli test icin web tabanli bir kullanici arayuzu, CI/CD entegrasyonu icin pytest ile programatik olarak veya otomatik is akislari icin bir komut satiri arayuzu araciligiyla yurutulebilir.
* Yapay zekayi karmasik, yuksek riskli gorevler icin guvenilir kilmak icin, basit prompt'lardan dogrulanabilir teslimleri ve kapsamı kesin olarak tanimlayan resmi "sozlesmelere" gecmeliyiz. Bu yapilandirilmis anlasma, Agent'larin muzakere etmesine, belirsizlikleri netletirmesine ve kendi calismasını yinelemeli olarak dogrulamasina olanak tanir ve onu ongorulemeyen bir aractan hesap verebilir ve guvenilir bir sisteme donusturur.

## Sonuclar

Sonuc olarak, yapay zeka agent'larini etkili bir sekilde degerlendirmek, dinamik ortamlarda performanslarinin surekli, cok yonlu bir degerlendirmesine gecmeyi gerektirir. Bu, gecikme ve kaynak tuketimi gibi metriklerin pratik izlemesinin yani sira agent'in karar verme surecinin yolu araciligiyla sofistike analizini icerir. Yardimcilik gibi nüansli nitelikler icin, LLM-as-a-Judge gibi yenilikci yontemler vazgecilmez hale gelirken, Google'in ADK'si gibi cerceveler hem birim hem de entegrasyon testi icin yapilandirilmis araclar saglar. Zorluk, odagin bireysel performansin otesinde etkili is birligi ve is birligini degerlendirmeye kaydigi multi-agent sistemlerle yogunlasir.

Kritik uygulamalarda guvenilirligi saglamak icin paradigma, basit, prompt gudumlü agent'lardan resmi anlasmalara bagli gelismis "yuklenicilere" kaymaktadir. Bu yuklenici agent'lar, acik, dogrulanabilir sartlar uzerinde calisarak muzakere etmelerine, gorevleri ayristirmalarina ve titiz kalite standartlarini karsilamak icin calismanlarini kendini dogrulamalarına olanak tanir. Bu yapilandirilmis yaklasim, agent'lari ongorulemeyen araclardan karmasik, yuksek riskli gorevleri ele alabilen hesap verebilir sistemlere donusturur. Nihayetinde bu gelisim, sofistike agentic yapay zekayi gorev-kritik alanlarda konuslandirmak icin gereken guveni olusturmak acisindan hayati onem tasir.

## Referanslar

Ilgili arastirmalar sunlardir:

1. ADK Web: [https://github.com/google/adk-web](https://github.com/google/adk-web)
2. ADK Evaluate: [https://google.github.io/adk-docs/evaluate/](https://google.github.io/adk-docs/evaluate/)
3. Survey on Evaluation of LLM-based Agents, [https://arxiv.org/abs/2503.16416](https://arxiv.org/abs/2503.16416)
4. Agent-as-a-Judge: Evaluate Agents with Agents, [https://arxiv.org/abs/2410.10934](https://arxiv.org/abs/2410.10934)
5. Agent Companion, gulli et al: [https://www.kaggle.com/whitepaper-agent-companion](https://www.kaggle.com/whitepaper-agent-companion)
