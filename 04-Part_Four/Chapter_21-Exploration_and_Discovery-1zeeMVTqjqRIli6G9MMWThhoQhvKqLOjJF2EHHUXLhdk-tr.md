# Bolum 21: Kesif ve Kesfetme (Exploration and Discovery)

Bu bolum, akilli agent'larin operasyonel ortamlarinda aktif olarak yeni bilgi aramalarini, yeni olasiliklari ortaya cikarmalarini ve bilinmeyen bilinmeyenleri belirlemelerini saglayan kaliplari incelemektedir. Kesif (Exploration) ve kesfetme (Discovery), reaktif davranislardan veya onceden tanimlanmis bir cozum uzayindaki optimizasyondan farklidir. Bunun yerine, agent'larin proaktif olarak bilinmeyen bolgelere girmesine, yeni yaklasimlari denemesine ve yeni bilgi veya anlayis olusturmasina odaklanir. Bu kalip, statik bilgi veya onceden programlanmis cozumlerin yetersiz kaldigi acik uclu, karmasik veya hizla gelisen alanlarda calisan agent'lar icin hayati onem tasir. Agent'in anlayisini ve yeteneklerini genisletme kapasitesini vurgular.

## Pratik Uygulamalar ve Kullanim Alanlari

Yapay zeka agent'lari, akilli bir sekilde onceliklendirme ve kesif yapma yetenegine sahiptir; bu da cesitli alanlarda uygulamalara yol acar. Bu agent'lar, potansiyel eylemleri ozerk olarak degerlendirip siralayarak karmasik ortamlarda gezinebilir, gizli iclgoruler ortaya cikarabilir ve yeniligi tesvik edebilir. Bu oncelilklendirilmis kesif kapasitesi, surecleri optimize etmelerini, yeni bilgi kesfetmelerini ve icerik olusturmalarini saglar.

Ornekler:

* **Bilimsel Arastirma Otomasyonu:** Bir agent, yeni malzemeler, ilac adaylari veya bilimsel ilkeleri kesfetmek icin deneyler tasarlar ve yurutur, sonuclari analiz eder ve yeni hipotezler formule eder.
* **Oyun Oynama ve Strateji Olusturma:** Agent'lar, oyun durumlarini kesfeder, ortaya cikan stratejileri kesfeder veya oyun ortamlarindaki zaafiyetleri belirler (ornegin AlphaGo).
* **Pazar Arastirmasi ve Trend Belirleme:** Agent'lar, trendleri, tuketici davranislarini veya pazar firsatlarini belirlemek icin yapilandirilmamis verileri (sosyal medya, haberler, raporlar) tarar.
* **Guvenlik Zaafiyeti Kesfi:** Agent'lar, guvenlik aciklarini veya saldiri vektorlerini bulmak icin sistemleri veya kod tabanlarini inceler.
* **Yaratici Icerik Olusturma:** Agent'lar, sanatsal eserler, muzik kompozisyonlari veya edebi eserler olusturmak icin stil, tema veya veri kombinasyonlarini kesfeder.
* **Kisisellestirilmis Egitim ve Ogretim:** Yapay zeka ogretmenleri, ogrencinin ilerlemesine, ogrenme stiline ve gelistirilmesi gereken alanlara dayali olarak ogrenme yollarini ve icerik sunumunu onceliklendirir.

Google Co-Scientist

Yapay zeka bilim ortagi (AI co-scientist), Google Research tarafindan hesaplama tabanli bir bilimsel is birligi araci olarak tasarlanmis bir yapay zeka sistemidir. Hipotez olusturma, oneri iyilestirme ve deney tasarimi gibi arastirma yonlerinde insan bilim insanlarina yardimci olur. Bu sistem, Gemini LLM uzerinde calisir.

Yapay zeka bilim ortaginin gelistirilmesi, bilimsel arastirmadaki zorluklari ele alir. Bunlar arasinda buyuk hacimlerde bilgi isleme, test edilebilir hipotezler olusturma ve deney planlamasini yonetme bulunur. Yapay zeka bilim ortagi, buyuk olcekli bilgi isleme ve sentez iceren gorevleri yerine getirerek arastirmacilari destekler ve potansiyel olarak veriler icindeki iliskileri ortaya cikarir. Amaci, erken asamadaki arastirmanin hesaplama yogun yonlerini ele alarak insan bilissel sureclerini desteklemektir.

**Sistem Mimarisi ve Metodolojisi:** Yapay zeka bilim ortaginin mimarisi, is birlikci ve yinelemeli surecleri taklit etmek icin yapilandirilmis multi-agent bir cerceve uzerine kuruludur. Bu tasarim, bir arastirma hedefine katkida bulunan, her biri belirli bir role sahip uzmanlasmis yapay zeka agent'larini entegre eder. Bir supervisor agent, hesaplama kaynaklarinin esnek olceklendirmesine olanak taniyan asenkron gorev yurutme cercevesi icinde bu bireysel agent'larin faaliyetlerini yonetir ve koordine eder.

Temel agent'lar ve islevleri sunlardir (bkz. Sekil 1):

* **Olusturma agent'i (Generation agent):** Literatur kesfetme ve simule edilmis bilimsel tartismalar yoluyla ilk hipotezleri ureterek sureci baslatir.
* **Yansitma agent'i (Reflection agent):** Bir akran degerlendirmeni olarak hareket ederek, olusturulan hipotezlerin dogrulugunu, yeniligini ve kalitesini elestirel olarak degerliendirir.
* **Siralama agent'i (Ranking agent):** Simule edilmis bilimsel tartismalar araciligiyla hipotezleri karsilastirmak, siralamak ve onceliklendirmek icin Elo tabanli bir turnuva kullanir.
* **Evrim agent'i (Evolution agent):** Kavramlari basitlestirerek, fikirleri sentezleyerek ve aliksi disi akil yurutmeyi kesfederek en yuksek siralı hipotezleri surekli olarak iyilestirir.
* **Yakinlik agent'i (Proximity agent):** Benzer fikirleri kumeslemek ve hipotez ortamini kesfetmeye yardimci olmak icin bir yakinlik grafi hesaplar.
* **Meta-inceleme agent'i (Meta-review agent):** Tum inceleme ve tartismalardan icgoruler sentezleyerek ortak kaliplari belirler ve geri bildirim saglar; sistemin surekli gelismesini mumkun kilar.

Sistemin operasyonel temeli, dil anlama, akil yurutme ve uretken yetenekler saglayan Gemini'ye dayanir. Sistem, ciktilari yinelemeli olarak akil yurutmek ve gelistirmek icin artan hesaplama kaynaklari tahsis eden bir mekanizma olan "test-time compute scaling" icerir. Sistem, akademik literatur, web tabanli veriler ve veritabanlari dahil cesitli kaynaklardan bilgi isler ve sentezler.

![AI Co-Scientist: Ideation to Validation](../assets/AI_Co_Scientist_Ideation_to_Validation.png)

Sekil 1: (Yazarlarin izniyle) AI Co-Scientist: Fikirden Dogrulamaya

Sistem, bilimsel yontemi yansitan yinelemeli bir "olustur, tartis ve gelistir" yaklasimini takip eder. Bir insan bilim insanindan bilimsel bir problem girdisi aldiktan sonra, sistem kendini iyilestiren bir hipotez olusturma, degerlendirme ve iyilestirme dongusu ile mesgul olur. Hipotezler, agent'lar arasindaki ic degerlendirmeler ve turnuva tabanli bir siralama mekanizmasi dahil olmak uzere sistematik degerlendirmeden gecer.

**Dogrulama ve Sonuclar:** Yapay zeka bilim ortaginin faydası, otomatik benchmark'lar, uzman degerlendirmeleri ve uctan uca islak laboratuvar deneyleri araciligiyla performansini degerlendiren biyotip alanindaki birkac dogrulama calismasinda gosterilmistir.

**Otomatik ve Uzman Degerlendirmesi:** Zorlu GPQA benchmark'inda, sistemin ic Elo degerlendirmesinin sonuclarinin dogrulugu ile uyumlu oldugu gosterilmis ve zor "diamond set"inde %78,4 ust-1 dogruluk elde edilmistir. 200'den fazla arastirma hedefinde yapilan analizler, test zamani hesaplammasinin olceklendirilmesinin hipotezlerin kalitesini (Elo degerlendirmesiyle olculen) tutarli bir sekilde iyilestirdigini gostermistir. 15 zorlu problemden olusan secilmis bir sette, yapay zeka bilim ortagi diger son teknoloji yapay zeka modellerini ve insan uzmanlari tarafindan saglanan "en iyi tahmin" cozumlerini geride birakmistir. Kucuk olcekli bir degerlendirmede, biyomedikal uzmanlar bilim ortaginin ciktiilarini diger temel modellere kiyasla daha yenilikci ve etkili olarak degerlendirmistir. Ilac yeniden amaclandirma icin NIH Specific Aims sayfalari olarak bicimlendirilmis sistem onerileri de alti uzman onkolog paneli tarafindan yuksek kaliteli olarak degerlendirilmistir.

**Uctan Uca Deneysel Dogrulama:**

Ilac Yeniden Amaclandirma: Akut miyeloid losemi (AML) icin sistem yeni ilac adaylari onermiştir. Bunlardan bazilari, KIRA6 gibi, AML'de kullanim icin onceki preklinik kaniti olmayan tamamen yeni onerilerdir. Sonraki in vitro deneyler, KIRA6 ve diger onerilen ilaclarin birden fazla AML hucre hattinda klinik olarak ilgili konsantrasyonlarda tumor hucre canliligini inhibe ettigini dogrulamistir.

Yeni Hedef Kesfi: Sistem, karaciger fibrozu icin yeni epigenetik hedefler belirlemiştir. Insan hepatik organoidleri kullanilarak yapilan laboratuvar deneyleri bu bulguları dogrulayarak, onerilen epigenetik modifiye edicileri hedefleyen ilaclarin onemli anti-fibrotik aktiviteye sahip oldugunu gostermistir. Belirlenen ilaclardan biri zaten baska bir durum icin FDA onayli olup yeniden amaclandirma firsati sunmaktadir.

Antimikrobiyal Direnc: Yapay zeka bilim ortagi, yayinlanmamis deneysel bulguları bagimsiz olarak tekrarlamistir. Belirli mobil genetik elemanlarin (cf-PICI'ler) neden bircok bakteri turunun genelinde bulundugunu aciklamasi istenmistir. Iki gun icinde, sistemin en yuksek siralı hipotezi cf-PICI'lerin konakci araligini genisletmek icin cesitli faj kuyruklariyla etkilestigi olmustur. Bu, bagimsiz bir arastirma grubunun on yildan fazla arastirmadan sonra ulastigi yenilikci, deneysel olarak dogrulanmis kesfini yansitmaktadir.

**Destekleme ve Sinirliliklar:** Yapay zeka bilim ortaginin arkasindaki tasarim felsefesi, insan arastirmasinin tam otomasyonu yerine desteklenmeyi vurgular. Arastirmacilar, dogal dil araciligiyla sistemle etkilesim kurar ve yonlendirir; geri bildirim saglar, kendi fikirlerini katkida bulunur ve yapay zekanin kesfetme sureclerini "scientist-in-the-loop" is birlikci paradigmasinda yonlendirir. Ancak sistemin bazi sinirlilikari vardir. Bilgisi, acik erisimli literature dayanmasıyla kisitlidir ve potansiyel olarak odeme duvarlarinin arkasindaki kritik onceki calismalari kacirabilir. Ayrica, deneyimli bilim insanlari icin onemli olan ancak nadiren yayinlanan olumsuz deney sonuclarina sinirli erisime sahiptir. Dahasi, sistem, olgusal yanlisliklar veya "halusinasyonlar" potansiyeli dahil olmak uzere alttaki LLM'lerin sinirlamaIarini devralir.

**Guvenlik (Safety):** Guvenlik kritik bir husustur ve sistem birden fazla guvenlik onlemi icerir. Tum arastirma hedefleri giriste guvenlik acisindan incelenir ve olusturulan hipotezler de sistemin guvenli olmayan veya etik disi arastirma icin kullanilmasini onlemek amaciyla kontrol edilir. 1.200 celiskili arastirma hedefi kullanan on guvenlik degerlendirmesi, sistemin tehlikeli girdileri saglam bir sekilde redddebildigini gostermistir. Sorumlu gelistirmeyi saglamak icin, gercek dunya geri bildirimi toplamak amaciyla sistem bir Guvenilir Test Edici Programi araciligiyla daha fazla bilim insanina sunulmaktadir.

## Uygulamali Kod Ornegi

Kesif ve Kesfetme alaninda eylemde olan agentic yapay zekanin somut bir ornegine bakalim: MIT Lisansi altinda Samuel Schmidgall tarafindan gelistirilen bir proje olan Agent Laboratory.

"Agent Laboratory", insan bilimsel cabalarini desteklemek icin tasarlanmis otonom bir arastirma is akisi cercevesidir. Bu sistem, bilimsel arastirma surecinin cesitli asamalarini otomatiklestirmek icin uzmanlasmis LLM'lerden yararlanir ve boylece insan arastirmacilarin kavramsallastirma ve elestirel analize daha fazla bilissel kaynak ayirmasini saglar.

Cerceve, otonom arastirma agent'lari icin merkezi olmayan bir depo olan "AgentRxiv"i entegre eder. AgentRxiv, arastirma ciktiilarinin depolanmasini, alinmasini ve gelistirilmesini kolaylastirir.

Agent Laboratory, arastirma surecini farkli asamalar boyunca yonlendirir:

1. **Literatur Taramasi:** Bu ilk asamada, uzmanlasmis LLM gudumlü agent'lar ilgili akademik literaturun otonom olarak toplanmasi ve elestirel analizi ile gorevlendirilir. Bu, ilgili arastirmalari belirlemek, sentezlemek ve kategorize etmek icin arXiv gibi harici veritabanlarindan yararlanmayi icerir ve sonraki asamalar icin kapsamli bir bilgi tabani olustururur.
2. **Deney:** Bu asama, deney tasarimlarinin is birlikci olarak formule edilmesini, veri hazirligi, deneylerin yurutulmesini ve sonuclarin analizini kapsar. Agent'lar, otomatik deney yurutmek icin kod olusturma ve yurutme icin Python ve model erisimi icin Hugging Face gibi entegre araclar kullanir. Sistem, agent'larin gercek zamanli sonuclara dayali olarak deneysel prosedürleri uyarlayip optimize edebilecegi yinelemeli iyilestirme icin tasarlanmistir.
3. **Rapor Yazimi:** Son asamada sistem, kapsamli arastirma raporlarinin olusturulmasini otomatiklestirir. Bu, deney asamasindan elde edilen bulguları literatur taramasindan elde edilen icgorülerle sentezlemeyi, belgeyi akademik konvansiyonlara gore yapilandirmayi ve profesyonel bicimlenirmme ve sekil olusturma icin LaTeX gibi harici araclarin entegre edilmesini icerir.
4. **Bilgi Paylasimi:** AgentRxiv, otonom arastirma agent'larinin bilimsel kesiflerini paylasmarina, erissmesine ve is birlikci olarak ilerletmesine olanak taniyan bir platformdur. Agent'larin onceki bulgular üzerine insa etmesine olanak taniarak kümülatif arastirma ilerlemesini teşvik eder.

Agent Laboratory'nin moduler mimarisi hesaplama esnekligi saglar. Amac, insan arastirmacisini koruyarak gorevleri otomatiklestirerek arastirma verimliligini arttirmaktir.

**Kod Analizi:** Kapsamli bir kod analizi bu kitabin kapsamini assa da, size bazi temel icgorüler sunmak ve kodu kendi basiniza incelemeye tesvik etmek istiyorum.

**Yargilama:** Insan degerlendirme sureclerini taklit etmek icin sistem, ciktilari degerlendirmek uzere uc parcali bir agentic yargilama mekanizmasi kullanir. Bu, her biri uretimi belirli bir perspektiften degerlendirmek uzere yapilandirilmis uc ayri otonom agent'in konuslandirilmasini icerir ve boylece insan yargilamasinin nüansli ve cok yonlu dogasini topluca taklit eder. Bu yaklasim, tekil metriklerin otesine gecen, daha zengin bir niteliksel degerlendirme yakalayan daha saglam ve kapsamli bir degerlendirme saglar.

```python
class ReviewersAgent:
    def __init__(self, model="gpt-4o-mini", notes=None, openai_api_key=None):
        if notes is None:
            self.notes = []
        else:
            self.notes = notes
        self.model = model
        self.openai_api_key = openai_api_key

    def inference(self, plan, report):
        reviewer_1 = "You are a harsh but fair reviewer and expect good experiments that lead to insights for the research topic."
        review_1 = get_score(
            outlined_plan=plan,
            latex=report,
            reward_model_llm=self.model,
            reviewer_type=reviewer_1,
            openai_api_key=self.openai_api_key
        )

        reviewer_2 = "You are a harsh and critical but fair reviewer who is looking for an idea that would be impactful in the field."
        review_2 = get_score(
            outlined_plan=plan,
            latex=report,
            reward_model_llm=self.model,
            reviewer_type=reviewer_2,
            openai_api_key=self.openai_api_key
        )

        reviewer_3 = "You are a harsh but fair open-minded reviewer that is looking for novel ideas that have not been proposed before."
        review_3 = get_score(
            outlined_plan=plan,
            latex=report,
            reward_model_llm=self.model,
            reviewer_type=reviewer_3,
            openai_api_key=self.openai_api_key
        )

        return f"Reviewer #1:\n{review_1}, \nReviewer #2:\n{review_2}, \nReviewer #3:\n{review_3}"
```

Yargilama agent'lari, tipik olarak insan degerlendirmeciler tarafindan kullanilan bilissel cerceve ve degerlendirme kriterlerini yakindan taklit eden belirli bir prompt ile tasarlanmistir. Bu prompt, agent'lari bir insan uzmanin yapacagi sekilde, ilgililik, tutarlilik, olgusal dogruluk ve genel kalite gibi faktorleri dikkate alarak ciktilari analiz etmeye yonlendirir. Bu prompt'lari insan inceleme protokollerini yansitacak sekilde olusturarak, sistem insan benzeri ayirt ediciliğe yaklasan bir degerlendirme sofistikasyonu duzeyine ulasmayı amaclar.

````python
def get_score(outlined_plan, latex, reward_model_llm, reviewer_type=None, attempts=3, openai_api_key=None):
   e = str()
   for _attempt in range(attempts):
       try:

           template_instructions = """
           Respond in the following format:

           THOUGHT:
           <THOUGHT>

           REVIEW JSON:
           ```json
           <JSON>
           ```

           In <THOUGHT>, first briefly discuss your intuitions
           and reasoning for the evaluation.
           Detail your high-level arguments, necessary choices
           and desired outcomes of the review.
           Do not make generic comments here, but be specific
           to your current paper.
           Treat this as the note-taking phase of your review.

           In <JSON>, provide the review in JSON format with
           the following fields in the order:
           - "Summary": A summary of the paper content and
           its contributions.
           - "Strengths": A list of strengths of the paper.
           - "Weaknesses": A list of weaknesses of the paper.
           - "Originality": A rating from 1 to 4
             (low, medium, high, very high).
           - "Quality": A rating from 1 to 4
             (low, medium, high, very high).
           - "Clarity": A rating from 1 to 4
             (low, medium, high, very high).
           - "Significance": A rating from 1 to 4
             (low, medium, high, very high).
           - "Questions": A set of clarifying questions to be
              answered by the paper authors.
           - "Limitations": A set of limitations and potential
              negative societal impacts of the work.
           - "Ethical Concerns": A boolean value indicating
              whether there are ethical concerns.
           - "Soundness": A rating from 1 to 4
              (poor, fair, good, excellent).
           - "Presentation": A rating from 1 to 4
              (poor, fair, good, excellent).
           - "Contribution": A rating from 1 to 4
             (poor, fair, good, excellent).
           - "Overall": A rating from 1 to 10
             (very strong reject to award quality).
           - "Confidence": A rating from 1 to 5
             (low, medium, high, very high, absolute).
           - "Decision": A decision that has to be one of the
             following: Accept, Reject.

           For the "Decision" field, don't use Weak Accept,
           Borderline Accept, Borderline Reject, or Strong Reject.
           Instead, only use Accept or Reject.
           This JSON will be automatically parsed, so ensure
           the format is precise.
           """
````

Bu multi-agent sistemde, arastirma sureci tipik bir akademik hiyerarsiyi yansitan uzmanlasmis roller etrafinda yapilandirilmistir; is akisini duzene sokmak ve ciktiyi optimize etmek icin.

**Professor Agent:** Professor Agent, arastirma gundemini olusturmaktan, arastirma sorularini tanimlamaktan ve gorevleri diger agent'lara devretmekten sorumlu birincil arastirma yoneticisi olarak isler. Bu agent, stratejik yonu belirler ve proje hedefleriyle uyumu saglar.

````python
class ProfessorAgent(BaseAgent):
   def __init__(self, model="gpt4omini", notes=None, max_steps=100, openai_api_key=None):
       super().__init__(model, notes, max_steps, openai_api_key)
       self.phases = ["report writing"]

   def generate_readme(self):
       sys_prompt = f"""You are {self.role_description()} \n Here is the written paper \n{self.report}. Task instructions: Your goal is to integrate all of the knowledge, code, reports, and notes provided to you and generate a readme.md for a github repository."""
       history_str = "\n".join([_[1] for _ in self.history])
       prompt = (
           f"""History: {history_str}\n{'~' * 10}\n"""
           f"Please produce the readme below in markdown:\n")
       model_resp = query_model(model_str=self.model, system_prompt=sys_prompt, prompt=prompt, openai_api_key=self.openai_api_key)
       return model_resp.replace("```markdown", "")
````

**PostDoc Agent:** PostDoc Agent'in rolu arastirmayi yurutmektir. Buna literatur taramalari yapmak, deneyleri tasarlamak ve uygulamak ve makaleler gibi arastirma ciktilari olusturmak dahildir. Onemle, PostDoc Agent, deneysel protokollerin ve veri analizinin pratik uygulamasini mumkun kilan kod yazma ve yurutme yetenegine sahiptir. Bu agent, arastirma eserlerinin birincil ureticisidir.

```python
class PostdocAgent(BaseAgent):
    def __init__(self, model="gpt4omini", notes=None, max_steps=100, openai_api_key=None):
        super().__init__(model, notes, max_steps, openai_api_key)
        self.phases = ["plan formulation", "results interpretation"]

    def context(self, phase):
        sr_str = str()
        if self.second_round:
            sr_str = (
                f"The following are results from the previous experiments\n",
                f"Previous Experiment code: {self.prev_results_code}\n"
                f"Previous Results: {self.prev_exp_results}\n"
                f"Previous Interpretation of results: {self.prev_interpretation}\n"
                f"Previous Report: {self.prev_report}\n"
                f"{self.reviewer_response}\n\n\n"
            )

        if phase == "plan formulation":
            return (
                sr_str,
                f"Current Literature Review: {self.lit_review_sum}",
            )
        elif phase == "results interpretation":
            return (
                sr_str,
                f"Current Literature Review: {self.lit_review_sum}\n"
                f"Current Plan: {self.plan}\n"
                f"Current Dataset code: {self.dataset_code}\n"
                f"Current Experiment code: {self.results_code}\n"
                f"Current Results: {self.exp_results}"
            )

        return ""
```

**Reviewer Agent'lari:** Reviewer agent'lari, PostDoc Agent'in arastirma ciktiilarinin elestirel degerlendirmelerini yaparak makalelerin ve deneysel sonuclarin kalitesini, gecerliligini ve bilimsel titizligini degerlendirir. Bu degerlendirme asamasi, kesinlestirmeden once yuksek bir arastirma ciktisi standardi saglamak icin akademik ortamlardaki akran degerlendirme surecini taklit eder.

**ML Engineering Agent'lari:** Makine Ogrenme Muhendisligi Agent'lari, kod gelistirmek icin bir PhD ogrencisiyle diyalojik is birligi yapan makine ogerenme muhendisleri olarak hizmet eder. Temel islevleri, saglanan literatur taramasi ve deneysel protokolden turetilen icgorüleri entegre ederek veri on isleme icin basit kod uretmektir. Bu, verilerin belirlenen deney icin uygun sekilde bicimlendirilmesini ve hazirlanmasını garanti eder.

```markdown
"You are a machine learning engineer being directed by a PhD student who will help you write the code, and you can interact with them through dialogue.\n"
"Your goal is to produce code that prepares the data for the provided experiment. You should aim for simple code to prepare the data, not complex code. You should integrate the provided literature review and the plan and come up with code to prepare data for this experiment.\n"
```

**SWEngineerAgent'lari:** Yazilim Muhendisligi Agent'lari, Makine Ogerenme Muhendisligi Agent'larini yonlendirir. Temel amaclari, Makine Ogerenme Muhendisligi Agent'ina belirli bir deney icin basit veri hazirlama kodu olusturmasinda yardimci olmaktir. Yazilim Muhendisligi Agent'i, saglanan literatur taramasini ve deneysel plani entegre ederek uretilen kodun karmasik olmayan ve arastirma hedeflerine dogrudan ilgili olmasini saglar.

```markdown
"You are a software engineer directing a machine learning engineer, where the machine learning engineer will be writing the code, and you can interact with them through dialogue.\n"
"Your goal is to help the ML engineer produce code that prepares the data for the provided experiment. You should aim for very simple code to prepare the data, not complex code. You should integrate the provided literature review and the plan and come up with code to prepare data for this experiment.\n"
```

Ozetle, "Agent Laboratory" otonom bilimsel arastirma icin sofistike bir cerceve temsil eder. Temel arastirma asamalarini otomatiklestirerek ve is birlikci yapay zeka gudumlü bilgi olusturmayi kolaylastirarak insan arastirma yeteneklerini desteklemek icin tasarlanmistir. Sistem, insan gozetimini koruyarak rutin gorevleri yoneterek arastirma verimliligini artirmayi amaclar.

## Bir Bakista

**Ne:** Yapay zeka agent'lari genellikle onceden tanimlanmis bilgi ile calisir ve bu durum yeni durumlari veya acik uclu problemleri ele alma yeteneklerini sinirlar. Karmasik ve dinamik ortamlarda, bu statik, onceden programlanmis bilgi gercek yenilik veya kesfetme icin yetersizdir. Temel zorluk, agent'larin basit optimizasyonun otesine gecerek aktif olarak yeni bilgi aramasini ve "bilinmeyen bilinmeyenleri" belirlemesini saglamaktir. Bu, tamamen reaktif davranislardan agent'in kendi anlayisini ve yeteneklerini genisleten proaktif, Agentic kesfetmeye bir paradigma degisikligini gerektirir.

**Neden:** Standartlastirilmis cozum, ozellikle otonom kesif ve kesfetme icin tasarlanmis Agentic yapay zeka sistemleri olusturmaktir. Bu sistemler genellikle bilimsel yontem gibi surecleri taklit etmek icin uzmanlasmis LLM'lerin is birligi yaptigi bir multi-agent cerceve kullanir. Ornegin, farkli agent'lar hipotez olusturma, elestirel inceleme ve en umut verici kavramlari gelistirme gorevleriyle gorevlendirilebilir. Bu yapilandirilmis, is birlikci metodoloji, sistemin genis bilgi ortamlarinda akilli bir sekilde gezinmesine, deney tasarlayip yurutmesine ve gercekten yeni bilgi olusturmasina olanak tanir. Kesfetmenin emek yogun yonlerini otomatiklestirerek bu sistemler insan zekasini destekler ve kesfetme hizini onemli olcude arttirir.

**Temel Kural:** Kesif ve Kesfetme kalibini, cozum uzayinin tamamen tanimlanmadigi acik uclu, karmasik veya hizla gelisen alanlarda calisirken kullanin. Bilimsel arastirma, pazar analizi ve yaratici icerik olusturma gibi yeni hipotezler, stratejiler veya icgorüler olusturmaayi gerektiren gorevler icin idealdir. Bu kalip, bilinen bir sureci optimize etmek yerine "bilinmeyen bilinmeyenleri" ortaya cikarmak hedef oldugunday esastir.

**Gorsel Ozet:**

![Exploration and Discovery Design Pattern](../assets/Exploration_and_Discovery_Design_Pattern.png)

Sekil 2: Kesif ve Kesfetme tasarim kalibi

## Onemli Cikarimlar

* Yapay zekada Kesif ve Kesfetme, agent'larin aktif olarak yeni bilgi ve olasiliklar pesinde kosmasini saglar; bu, karmasik ve gelisen ortamlarda gezinmek icin esastir.
* Google Co-Scientist gibi sistemler, Agent'larin otonom olarak hipotez olusturup deney tasarlayarak insan bilimsel arastirmasini nasil destekleyebildigini gosterir.
* Agent Laboratory'nin uzmanlasmis rolleriyle orneklendirilen multi-agent cerceve, literatur taramasi, deney ve rapor yaziminin otomasyonu yoluyla arastirmayi iyilestirir.
* Nihayetinde bu Agent'lar, hesaplama yogun gorevleri yoneterek insan yaraticiligini ve problem cozme yetenegini gelistirmeyi ve boylece yeniligi ve kesfetmeyi hizlandirmayi amaclar.

## Sonuc

Sonuc olarak, Kesif ve Kesfetme kalibi, gercekten agentic bir sistemin oz varligidir ve pasif talimat takibinin otesine gecerek ortamini proaktif olarak kesfetme yetenegini tanimlar. Bu dogasal agentic durtü, bir yapay zekanin karmasik alanlarda ozerk olarak calismasini guclendirir; yalnizca gorevleri yurutmek degil, yeni bilgiyi ortaya cikarmak icin bagimsiz olarak alt hedefler belirlemek. Bu gelismis agentic davranis, en guclu sekilde, her agent'in daha buyuk bir is birlikci sureçte belirli, proaktif bir role sahip oldugu multi-agent cerceveler araciligiyla gerceklestirilir. Ornegin, Google'in son derece agentic Co-scientist sistemi, bilimsel hipotezleri ozerk olarak olusturan, tartisan ve gelistiren agent'lar icerir.

Agent Laboratory gibi cerceveler, insan arastirma ekiplerini taklit eden agentic bir hiyerarsi olusturarak bunu daha da yapilandirir ve sistemin tum kesfetme yasam dongusunu kendini yonetmesini saglar. Bu kalibin ozü, ortaya cikan agentic davranislari orkestre etmede, sistemin minimum insan mudahalesiyle uzun vadeli, acik uclu hedefleri takip etmesine olanak tanimaktadir. Bu, insan-yapay zeka ortakligini yukselterek yapay zekayi kesfetme gorevlerinin otonom yurutmesini ustlenen gercek bir agentic is birlikci olarak konumlandirir. Bu proaktif kesfetme calismasini agentic bir sisteme devrederek, insan zekasi onemli olcude desteklenir ve yenilik hızlandirilir. Bu kadar guclu agentic yeteneklerin gelistirilmesi, ayni zamanda guvenlik ve etik gozetim konusunda guclu bir taahhut gerektirir. Nihayetinde bu kalip, gercekten agentic yapay zeka olusturmak icin plani saglar ve hesaplama araclarini bilgi pesindeki bagimsiz, hedef odakli ortaklara donusturur.

## Referanslar

1. Exploration-Exploitation Dilemma**:** A fundamental problem in reinforcement learning and decision-making under uncertainty. [https://en.wikipedia.org/wiki/Exploration%E2%80%93exploitation_dilemma](https://en.wikipedia.org/wiki/Exploration%E2%80%93exploitation_dilemma)
2. Google Co-Scientist: [https://research.google/blog/accelerating-scientific-breakthroughs-with-an-ai-co-scientist/](https://research.google/blog/accelerating-scientific-breakthroughs-with-an-ai-co-scientist/)
3. Agent Laboratory: Using LLM Agents as Research Assistants [https://github.com/SamuelSchmidgall/AgentLaboratory](https://github.com/SamuelSchmidgall/AgentLaboratory)
4. AgentRxiv: Towards Collaborative Autonomous Research: [https://agentrxiv.github.io/](https://agentrxiv.github.io/)
