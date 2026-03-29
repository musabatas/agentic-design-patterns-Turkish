# Bolum 11: Hedef Belirleme ve Izleme (Goal Setting and Monitoring)

Yapay zeka agent'larinin gercekten etkili ve amacli olmasi icin yalnizca bilgi isleme veya arac kullanma yeteneginden fazlasina ihtiyac duyarlar; net bir yonelime ve gercekten basarili olup olmadiklarini bilmenin bir yoluna ihtiyaclari vardir. Hedef Belirleme ve Izleme (Goal Setting and Monitoring) kalibi tam da burada devreye girer. Bu kalip, agent'lara calisacaklari belirli hedefler vermek ve bu hedeflerin karsilanip karsilanmadigini izleyip belirleyebilecekleri araclarla donatmak hakkindadir.

## Hedef Belirleme ve Izleme Kalibina Genel Bakis

Bir yolculuk planlamayi dusunun. Hedefinizde kendiliginizden belirmezsiniz. Nereye gitmek istediginize karar verirsiniz (hedef durum), nereden basladiginizi belirlersiniz (baslangic durumu), mevcut secenekleri degerlendirirsiniz (ulasim, rotalar, butce) ve ardindan bir dizi adim belirlersiniz: bilet al, bavul hazirla, havaalani/istasyona git, araca bin, var, konaklama bul, vb. Bu adim adim surec -- genellikle bagimliliklari ve kisitlamalari goz onunde bulunduran -- temelde agentic sistemlerde planlama (planning) ile kastettigimiz seydir.

Yapay zeka agent'lari baglaminda planlama (planning), tipik olarak bir agent'in ust duzey bir hedef alip otonom veya yari otonom bir sekilde bir dizi ara adim veya alt hedef uretmesini icerir. Bu adimlar daha sonra sirali olarak veya tool use, routing veya coklu agent is birligi (multi-agent collaboration) gibi diger kaliplari potansiyel olarak iceren daha karmasik bir akista yurutulebilir. Planlama mekanizmasi, gelismis arama algoritmalari, mantiksal akil yurutme (reasoning) veya giderek artan bir sekilde, egitim verileri ve gorev anlayisina dayali olarak makul ve etkili planlar uretmek icin buyuk dil modellerinin (LLM) yeteneklerinden yararlanmayi icerebilir.

Iyi bir planlama yetenegI, agent'larin basit, tek adimli sorgular olmayan sorunlarin ustesinden gelmesini saglar. Cok yonlu istekleri ele almalarini, yeniden planlama yaparak degisen kosullara uyum saglamalarini ve karmasik is akislarini duzenlemelerini mumkun kilar. Basit bir reaktif sistemi, tanimlanmis bir hedefe dogru proaktif olarak calisabilecek bir sisteme donustuuren, bircok gelismis agentic davranisi destekleyen temel bir kaliptir.

## Pratik Uygulamalar ve Kullanim Alanlari

Hedef Belirleme ve Izleme kalibi, karmasik, gercek dunya senaryolarinda otonom ve guvenilir bir sekilde calisabilen agent'lar olusturmak icin vazgecilmezdir. Iste bazi pratik uygulamalar:

* **Musteri Destek Otomasyonu:** Bir agent'in hedefi "musterinin fatura sorusunu cozmek" olabilir. Konusmayi izler, veritabani kayitlarini kontrol eder ve faturayi ayarlamak icin araclar kullanir. Basari, fatura degisikliginin onaylanmasi ve olumlu musteri geri bildirimi alinmasi ile izlenir. Sorun cozulmezse, eskale eder.
* **Kisisellestirilmis Ogrenme Sistemleri:** Bir ogrenme agent'inin hedefi "ogrencinin cebir anlayisini gelistirmek" olabilir. Ogrencinin alisstirmalardaki ilerlemesini izler, ogretim materyallerini uyarlar ve dogruluk ile tamamlama suresi gibi performans metriklerini takip ederek ogrenci zorluk yasarsa yaklasiminii ayarlar.
* **Proje Yonetimi Asistanlari:** Bir agent, "proje kilometre tasi X'in Y tarihine kadar tamamlanmasini saglamak" goreviyle yetkilendiirlebilir. Gorev durumlarini, ekip iletisimlerini ve kaynak kullanilabirlligini izleyerek gecikmeleri isaret eder ve hedef risk altindaysa duzeltici eylemler onerir.
* **Otomatik Ticaret Botlari:** Bir ticaret agent'inin hedefi "risk toleransi icinde kalarak portfoy kazanclarini maksimize etmek" olabilir. Piyasa verilerini, mevcut portfoy degerini ve risk gostergelerini surekli izler, kosullar hedefleriyle uyustigunda islem gerceklestirir ve risk esikleri asilirsa strateji ayarlar.
* **Robotik ve Otonom Araclar:** Otonom bir aracin birincil hedefi "yolculari A'dan B'ye guvenli bir sekilde tasiimak"tir. Ceevresini (diger araclar, yayalar, trafik isiklari), kendi durumunu (hiz, yakit) ve planlanan rota boyunca ilerlemesini surekli izleyerek hedefe guvenli ve verimli bir sekilde ulasmak icin surus davranisini uyarlar.
* **Icerik Moderasyonu:** Bir agent'in hedefi "X platformundan zararli icerigi tespit etmek ve kaldirmak" olabilir. Gelen icerigi izler, siniflandirma modelleri uygular ve yanlis pozitif/negatif gibi metrikleri takip ederek filtreleme kriterlerini ayarlar veya belirsiz vakalari insan denetcilere eskalasyon yapar.

Bu kalip, guvenilir bir sekilde calismasi, belirli sonuclar elde etmesi ve dinamik kosullara uyum saglamasi gereken agent'lar icin temeldir ve akilli oz yonetim icin gerekli framework'u saglar.

## Uygulamali Kod Ornegi

Hedef Belirleme ve Izleme kalibini gostermek icin LangChain ve OpenAI API'lerini kullanan bir ornek sunuyoruz. Bu Python betigi, Python kodu uretmek ve iyilestirmek icin tasarlanmis otonom bir yapay zeka agent'ini ana hatilariyla cizer. Temel islevi, belirtilen problemler icin cozumler uretmek ve kullanici tarafindan tanimlanan kalite olcutlerine uyumu saglamaktir.

Bir "hedef belirleme ve izleme" kalibi kullanir; burada kodu yalnizca bir kez uretmez, bunun yerine olusturma, oz degerlendirme ve iyilestirmenin yinelemeli bir donguusune girer. Agent'in basarisi, uretilen kodun baslangic hedeflerini basariyla karsilayip karsilamadigina dair kendi yapay zeka tabanli yargilamasiyla olculur. Nihai cikti, bu iyilestirme surecinin doruk noktasini temsil eden parlak, aciklamali ve kullanima hazir bir Python dosyasidir.

**Bagimliliklar**:

```python
pip install langchain_openai openai python-dotenv .env file with key in OPENAI_API_KEY
```

Bu betigi en iyi sekilde, bir projeye atanmis otonom bir yapay zeka programcisi olarak hayal ederek anlayabilirsiniz (bkz. Sekil 1). Surec, yapay zekaya ayrinti bir proje brifi -- cozmesi gereken belirli kodlama problemi -- verdiginizde baslar.

```python
# MIT License
# Copyright (c) 2025 Mahtab Syed
# https://www.linkedin.com/in/mahtabsyed/

"""
Hands-On Code Example - Iteration 2
-  To illustrate the Goal Setting and Monitoring pattern, we have an example using LangChain and OpenAI APIs:

Objective: Build an AI Agent which can write code for a specified use case based on specified goals:
-  Accepts a coding problem (use case) in code or can be as input.
-  Accepts a list of goals (e.g., "simple", "tested", "handles edge cases")  in code or can be input.
-  Uses an LLM (like GPT-4o) to generate and refine Python code until the goals are met. (I am using max 5 iterations, this could be based on a set goal as well)
-  To check if we have met our goals I am asking the LLM to judge this and answer just True or False which makes it easier to stop the iterations.
-  Saves the final code in a .py file with a clean filename and a header comment.
"""

import os
import random
import re
from pathlib import Path

from langchain_openai import ChatOpenAI
from dotenv import load_dotenv, find_dotenv


# 🔐 Load environment variables
_ = load_dotenv(find_dotenv())
OPENAI_API_KEY = os.getenv("OPENAI_API_KEY")
if not OPENAI_API_KEY:
    raise EnvironmentError("❌ Please set the OPENAI_API_KEY environment variable.")

# ✅ Initialize OpenAI model
print("📡 Initializing OpenAI LLM (gpt-4o)...")
llm = ChatOpenAI(
    model="gpt-4o",  # If you dont have access to got-4o use other OpenAI LLMs
    temperature=0.3,
    openai_api_key=OPENAI_API_KEY,
)


# --- Utility Functions ---
def generate_prompt(
    use_case: str, goals: list[str], previous_code: str = "", feedback: str = ""
) -> str:
    print("📝 Constructing prompt for code generation...")
    base_prompt = f"""
You are an AI coding agent. Your job is to write Python code based on the following use case:

Use Case: {use_case}

Your goals are:
{chr(10).join(f"- {g.strip()}" for g in goals)}
"""
    if previous_code:
        print("🔄 Adding previous code to the prompt for refinement.")
        base_prompt += f"\nPreviously generated code:\n{previous_code}"
    if feedback:
        print("📋 Including feedback for revision.")
        base_prompt += f"\nFeedback on previous version:\n{feedback}\n"

    base_prompt += "\nPlease return only the revised Python code. Do not include comments or explanations outside the code."
    return base_prompt


def get_code_feedback(code: str, goals: list[str]) -> str:
    print("🔍 Evaluating code against the goals...")
    feedback_prompt = f"""
You are a Python code reviewer. A code snippet is shown below. Based on the following goals:

{chr(10).join(f"- {g.strip()}" for g in goals)}

Please critique this code and identify if the goals are met. Mention if improvements are needed for clarity, simplicity, correctness, edge case handling, or test coverage.

Code:
{code}
"""
    return llm.invoke(feedback_prompt)


def goals_met(feedback_text: str, goals: list[str]) -> bool:
    """
    Uses the LLM to evaluate whether the goals have been met based on the feedback text.
    Returns True or False (parsed from LLM output).
    """
    review_prompt = f"""
You are an AI reviewer.

Here are the goals:
{chr(10).join(f"- {g.strip()}" for g in goals)}

Here is the feedback on the code:
\"\"\"
{feedback_text}
\"\"\"

Based on the feedback above, have the goals been met?

Respond with only one word: True or False.
"""
    response = llm.invoke(review_prompt).content.strip().lower()
    return response == "true"


def clean_code_block(code: str) -> str:
    lines = code.strip().splitlines()
    if lines and lines[0].strip().startswith("```"):
        lines = lines[1:]
    if lines and lines[-1].strip() == "```":
        lines = lines[:-1]
    return "\n".join(lines).strip()


def add_comment_header(code: str, use_case: str) -> str:
    comment = f"# This Python program implements the following use case:\n# {use_case.strip()}\n"
    return comment + "\n" + code


def to_snake_case(text: str) -> str:
    text = re.sub(r"[^a-zA-Z0-9 ]", "", text)
    return re.sub(r"\s+", "_", text.strip().lower())


def save_code_to_file(code: str, use_case: str) -> str:
    print("💾 Saving final code to file...")

    summary_prompt = (
        f"Summarize the following use case into a single lowercase word or phrase, "
        f"no more than 10 characters, suitable for a Python filename:\n\n{use_case}"
    )
    raw_summary = llm.invoke(summary_prompt).content.strip()
    short_name = re.sub(r"[^a-zA-Z0-9_]", "", raw_summary.replace(" ", "_").lower())[:10]

    random_suffix = str(random.randint(1000, 9999))
    filename = f"{short_name}_{random_suffix}.py"
    filepath = Path.cwd() / filename

    with open(filepath, "w") as f:
        f.write(code)

    print(f"✅ Code saved to: {filepath}")
    return str(filepath)


# --- Main Agent Function ---
def run_code_agent(use_case: str, goals_input: str, max_iterations: int = 5) -> str:
    goals = [g.strip() for g in goals_input.split(",")]

    print(f"\n🎯 Use Case: {use_case}")
    print("🎯 Goals:")
    for g in goals:
        print(f"  - {g}")

    previous_code = ""
    feedback = ""

    for i in range(max_iterations):
        print(f"\n=== 🔁 Iteration {i + 1} of {max_iterations} ===")
        prompt = generate_prompt(
            use_case,
            goals,
            previous_code,
            feedback if isinstance(feedback, str) else feedback.content,
        )

        print("🚧 Generating code...")
        code_response = llm.invoke(prompt)
        raw_code = code_response.content.strip()
        code = clean_code_block(raw_code)
        print("\n🧾 Generated Code:\n" + "-" * 50 + f"\n{code}\n" + "-" * 50)

        print("\n📤 Submitting code for feedback review...")
        feedback = get_code_feedback(code, goals)
        feedback_text = feedback.content.strip()
        print("\n📥 Feedback Received:\n" + "-" * 50 + f"\n{feedback_text}\n" + "-" * 50)

        if goals_met(feedback_text, goals):
            print("✅ LLM confirms goals are met. Stopping iteration.")
            break

        print("🛠️ Goals not fully met. Preparing for next iteration...")
        previous_code = code

    final_code = add_comment_header(code, use_case)
    return save_code_to_file(final_code, use_case)


# --- CLI Test Run ---
if __name__ == "__main__":
    print("\n🧠 Welcome to the AI Code Generation Agent")

    # Example 1
    use_case_input = "Write code to find BinaryGap of a given positive integer"
    goals_input = "Code simple to understand, Functionally correct, Handles comprehensive edge cases, Takes positive integer input only, prints the results with few examples"
    run_code_agent(use_case_input, goals_input)

    # Example 2
    # use_case_input = "Write code to count the number of files in current directory and all its nested sub directories, and print the total count"
    # goals_input = (
    #     "Code simple to understand, Functionally correct, Handles comprehensive edge cases, Ignore recommendations for performance, Ignore recommendations for test suite use like unittest or pytest"
    # )
    # run_code_agent(use_case_input, goals_input)

    # Example 3
    # use_case_input = "Write code which takes a command line input of a word doc or docx file and opens it and counts the number of words, and characters in it and prints all"
    # goals_input = "Code simple to understand, Functionally correct, Handles edge cases"
    # run_code_agent(use_case_input, goals_input)
```

Bu brifle birlikte, nihai kodun karsilamasi gereken hedefleri temsil eden kati bir kalite kontrol listesi sunarssiniz -- "cozum basit olmali", "fonksiyonel olarak dogru olmali" veya "beklenmedik uc vakalari ele almali" gibi kriterler.

![Goal Setting and Monitor example](../assets/Goal_Setting_and_Monitoring.png)

Sekil 1: Hedef Belirleme ve Izleme ornegi

Bu gorevi alan yapay zeka programcisi calissmaya baslar ve kodun ilk taslagini uretir. Ancak bu baslangic surumunu hemen gondermek yerine, kritik bir adim gerceklestirmek icin durur: titiz bir oz inceleme. Sunduggunuz kalite kontrol listesindeki her maddeyi kendi yarattigiyla dikkatle karsilastirir ve kendi kalite guvencc muftettisi gibi hareket eder. Bu incelemeden sonra, kendi ilerlemesi hakkinda basit, tarafsiz bir karar verir: tum standartlari karsiliyorsa "True" veya yetersiz kaliyorsa "False".

Karar "False" ise yapay zeka pes etmez. Oz elesttirisinden elde ettigi icgoruleri kullanarak zayifliklari tespit eden ve kodu akillica yeniden yazan dusunceli bir revizyon asamasina girer. Bu taslak hazirlama, oz inceleme ve iyilestirme dongusu, her yineleme hedeflere daha fazla yaklasmayi hedefleyerek devam eder. Bu surec, yapay zeka her gerekssinimini karsilayarak sonunda "True" durumuna ulasana kadar veya bir gelistiricinin son teslim tarihine karsi calismasi gibi onceden tanimlanmis bir deneme sinirna ulasana kadar tekrarlanir. Kod bu son incelemeden gectiginde, betik parlak cozumu paketler, yardimci aciklamalar ekler ve kullanima hazir, temiz yeni bir Python dosyasina kaydeder.

**Uyarilar ve Degerlendirmeler:** Bunun ornekleyici bir gosterim oldugunu ve uretime hazir kod olmadigini belirtmek onemlidir. Gercek dunya uygulamalari icin birkac faktor dikkate alinmalidir. Bir LLM, bir hedefin amaclanan anlamini tam olarak kavrayamayabilir ve performansini yanlis olarak basarili degeerlendirebilir. Hedef iyi anlasilsa bile model hallucination yapabilir. Ayni LLM'in hem kodu yazmaktan hem de kalitesini yargilamaktan sorumlu oldugunda, yanlis yonde gidip gitmedigini kesfetmekte daha fazla zorluk cekebilir.

Sonuc olarak LLM'ler sihirli bir sekilde kusursuz kod uretmez; uretilen kodu calistirip test etmeniz gerekir. Dahasi, basit ornekteki "izleme" temeldir ve surecin sonsuza kadar calisma riski olusturur.

```text
Act as an expert code reviewer with a deep commitment to producing clean, correct, and simple code. Your core mission is to eliminate code "hallucinations" by ensuring every suggestion is grounded in reality and best practices. When I provide you with a code snippet, I want you to: -- Identify and Correct Errors: Point out any logical flaws, bugs, or potential runtime errors. -- Simplify and Refactor: Suggest changes that make the code more readable, efficient, and maintainable without sacrificing correctness. -- Provide Clear Explanations: For every suggested change, explain why it is an improvement, referencing principles of clean code, performance, or security. -- Offer Corrected Code: Show the "before" and "after" of your suggested changes so the improvement is clear. Your feedback should be direct, constructive, and always aimed at improving the quality of the code.
```

Daha saglam bir yaklasim, belirli roller vererek bu endiiseleri ayirmaktan gecer. Ornegin, her birinin belirli bir rolu oldugu Gemini kullanan kisisel bir yapay zeka agent ekibi olusturdum:

* Esli Programci (Peer Programmer): Kod yazmaaya ve beyin firtinasina yardimci olur.
* Kod Gozden Gecirici (Code Reviewer): Hatalari yakalar ve iyilestirmeler onerir.
* Dokumantasyon Uzmani (Documenter): Net ve ozlu dokumantasyon uretir.
* Test Yazici (Test Writer): Kapsamli birim testleri olusturur.
* Prompt Iyilestirici (Prompt Refiner): Yapay zeka ile etkilesimleri optimize eder.

Bu coklu agent sisteminde, programci agent'indan ayri bir varlik olarak hareket eden Kod Gozden Gecirici, ornekteki hakime benzer bir prompt'a sahiptir ve bu, nesnel degerlendirmeyi onemli olcude iyilestirir. Bu yapi dogal olarak daha iyi pratiklere yol acar; cunku Test Yazici agent'i, Esli Programci tarafindan uretilen kod icin birim testleri yazma ihtiyacini karsilayabilir.

Ilgilenen okuyucuya, daha gelismis kontroller ekleme ve kodu uretime daha yakin hale getirme gorevini biirakiyorum.

## Bir Bakista

**Ne**: Yapay zeka agent'lari genellikle net bir yonelimden yoksundur ve bu, basit, reaktif gorevlerin otesinde amacli hareket etmelerini engeller. Tanimlanmis hedefler olmadan, karmasik, cok adimli problemlerin ustesinden bagimsiz olarak gelemez veya sofistike is akislarini duzenleyemezler. Dahasi, eylemlerinin basarili bir sonuca yol acip acmadigini beliirlemek icin dogal bir mekanizmalari yoktur. Bu, ozerklikleerini sinirlar ve yalnizca gorev yurutmenin yeterli olmadigi dinamik, gercek dunya senaryolarinda gercekten etkili olmaliarini engeller.

**Neden**: Hedef Belirleme ve Izleme kalibi, agentic sistemlere bir amac duygusu ve oz degerlendirme yetenegii yerleistirerek standartlastirilmis bir cozum sunar. Agent'in ulasacagi acik, olculebilir hedeflerin acikca tanimlanmasini icerir. Bununla es zamanli olarak, agent'in ilerlemesini ve cevresinin durumunu bu hedeflere karsi surekli izleyen bir izleme mekanizmasi olusturur. Bu, agent'in performansini degerlendirmesini, rotasini duzeltmesini ve basari yolundan saparsa planini uyarlamasini saglayan kritik bir geri bildirim dongusu olusturur. Bu kalibi uygulayarak gelistiriciler, basit reaktif agent'lari proaktif, hedefe yonelik, otonom ve guvenilir islem yapabilecek sistemlere donusturebilir.

**Temel kural**: Bu kalibi, bir yapay zeka agent'inin cok adimli bir gorevi otonom olarak yurutmesi, dinamik kosullara uyum saglamasi ve surekli insan mudahalesi olmadan belirli, ust duzey bir hedefi guvenilir bir sekilde gercceklestirmesi gerektiginde kullanin.

**Gorsel ozet**:

![Goal Design Pattern](../assets/Goal_Design_Pattern.png)

Sekil 2: Hedef tasarim kaliplari (Goal Design Patterns)

## Temel Cikarimlar

Temel cikarimlar sunlardir:

* Hedef Belirleme ve Izleme (Goal Setting and Monitoring), agent'lari amac ve ilerlemeyi takip etme mekanizmalariyla donatir.
* Hedefler belirli, olculebilir, ulasiiabilir, ilgili ve zaman sinirli (SMART) olmalidir.
* Etkili izleme icin metrikleri ve basari kriterlerini net bir sekilde tanimlamak esastir.
* Izleme, agent eylemlerini, cevre durumlarini ve arac ciktilarini gozlemeyi icerir.
* Izlemeden gelen geri bildirim donguleri, agent'larin uyum saglamasina, planlari gozden gecirmesine veya sorunlari eskale etmesine olanak tanir.
* Google'in ADK'sinda hedefler genellikle agent talimatlari araciligiyla iletilir ve izleme, durum yonetimi ile arac etkilesimleri araciligiyla gerceklestirilir.

## Sonuc

Bu bolum, Hedef Belirleme ve Izleme (Goal Setting and Monitoring) paradigmasina odaklanmistir. Bu kavraimin yapay zeka agent'larini yalnizca reaktif sistemlerden proaktif, hedefe yonelik varliklara nasil donusturdugunu vurguladim. Metin, acik, olculebilir hedefler tanimllamanin ve ilerlemeyi takip etmek icin titiz izleme prosedutleri olusturmanin onemini vurguladi. Pratik uygulamalar, bu paradigmanin musteri hizmetinden robotige kadar cesitli alanlarda guvenilir otonom isletimi nasil destekledigini gosterdi. Kavramsal bir kodlama ornegi, agent yonergeleri ve durum yonetimini kullanarak bir agent'in belirlenmis hedeflerine ulasmasini yonlendirmek ve degerlendirmek icin bu ilkelerin yapilandirilmis bir framework icindeki uygulamasini gostermektedir. Sonuc olarak, agent'lari hedef formule etme ve denetleme yetenegiyle donatmak, gercekten akilli ve hesap verebilir yapay zeka sistemleri olusturma yolunda temel bir adimdir.

## Kaynaklar

1. SMART Goals Framework. [https://en.wikipedia.org/wiki/SMART\_criteria](https://en.wikipedia.org/wiki/SMART_criteria)
