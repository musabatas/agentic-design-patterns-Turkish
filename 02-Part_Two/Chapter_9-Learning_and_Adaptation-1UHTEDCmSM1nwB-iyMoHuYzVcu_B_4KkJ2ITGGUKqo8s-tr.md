# Bolum 9: Ogrenme ve Uyum Saglama (Learning and Adaptation)

Ogrenme (learning) ve uyum saglama (adaptation), yapay zeka agent'larinin yeteneklerini gelistirmek icin kritik oneme sahiptir. Bu surecler, agent'larin onceden tanimlanmis parametrelerin otesine gecmesini saglayarak deneyim ve cevre etkilesimi yoluyla otonom bir sekilde gelismelerine olanak tanir. Ogrenme ve uyum saglama sayesinde agent'lar, yeni durumlarla etkili bir sekilde basa cikabilir ve surekli manuel mudahale olmadan performanslarini optimize edebilir. Bu bolum, agent ogrenme ve uyum saglamanin altinda yatan ilkeleri ve mekanizmalari ayrintili olarak incelemektedir.

## Buyuk Resim

Agent'lar, yeni deneyimlere ve verilere dayali olarak dusunce, eylem veya bilgilerini degistirerek ogrenir ve uyum saglar. Bu, agent'larin basitce talimatlari takip etmekten zaman icinde daha akilli hale gelmeye evrilmesini saglar.

* **Reinforcement Learning:** Agent'lar eylemleri dener, olumlu sonuclar icin oduller ve olumsuz sonuclar icin cezalar alarak degisen durumlarda optimal davranislari ogrenir. Robotlari kontrol eden veya oyun oynayan agent'lar icin faydalidir.
* **Supervised Learning:** Agent'lar etiketli orneklerden ogrenerek girisleri istenen ciktilara baglar ve karar verme ile oruntu tanima gibi gorevleri mumkun kilar. E-postalari siniflaylan veya trendleri tahmin eden agent'lar icin idealdir.
* **Unsupervised Learning:** Agent'lar etiketlenmemis verilerdeki gizli baglantilari ve oruntuleri kesfederek icgorulere, organizasyona ve cevrelerinin zihinsel bir haritasinin olusturulmasina yardimci olur. Belirli bir yonlendirme olmadan veri kesfeden agent'lar icin faydalidir.
* **LLM Tabanli Agent'larla Few-Shot/Zero-Shot Learning:** LLM'lerden yararlanan agent'lar, minimum sayida ornekle veya net talimatlarla yeni gorevlere hizla uyum saglayabilir ve yeni komutlara veya durumlara hizli yanitlar verebilir.
* **Online Learning:** Agent'lar yeni verilerle bilgilerini surekli gunceller; bu, dinamik ortamlarda gercek zamanli tepkiler ve surekli uyum saglama icin esastir. Surekli veri akislarini isleyen agent'lar icin kritiktir.
* **Bellek Tabanli Ogrenme (Memory-Based Learning):** Agent'lar, benzer durumlarda mevcut eylemlerini ayarlamak icin gecmis deneyimlerini hatirlar, baglam farkindagiini ve karar verme yetenegini gelisitrir. Bellek geri cagirma yeteneklerine sahip agent'lar icin etkilidir.

Agent'lar, ogrenmeye dayali olarak strateji, anlayis veya hedeflerini degistirerek uyum saglar. Bu, onceden tahmin edilemeyen, degisen veya yeni ortamlardaki agent'lar icin hayati onem tasir.

**Proximal Policy Optimization (PPO)**, surekli bir eylem araligi olan ortamlarda (bir robotun eklemlerini kontrol etme veya bir oyundaki karakter gibi) agent'lari egitmek icin kullanilan bir reinforcement learning algoritmasidir. Ana hedefi, bir agent'in politikasi (policy) olarak bilinen karar verme stratejisini guvenilir ve kararli bir sekilde gelistirmektir.

PPO'nun temel fikri, agent'in politikasinda kucuk ve dikkatli guncellemeler yapmaktir. Performansin cOkmesine neden olabilecek drastik degisikliklerden kacinir. Nasil calistigina bakalim:

1. Veri Toplama: Agent, mevcut politikasini kullanarak cevresiyle etkilesir (ornegin bir oyun oynar) ve bir grup deneyim (durum, eylem, odul) toplar.
2. Bir "Vekil" Hedefin Degerlendirilmesi: PPO, potansiyel bir politika guncellemesinin beklenen odulu nasil degistirecegini hesaplar. Ancak bu odulu sadece maksimize etmek yerine, ozel bir "kirpilmis" (clipped) amac fonksiyonu kullanir.
3. "Kirpma" Mekanizmasi: PPO'nun kararliliginin anahtari budur. Mevcut politika etrafinda bir "guven bolgesi" veya guvenli alan olusturur. Algoritmanin, mevcut stratejiden cok farkli bir guncelleme yapmasi engellenir. Bu kirpma, bir guvenlik freni gibi davranarak agent'in ogrenmesini bozan buyuk, riskli bir adim atmamasini saglar.

Kisacasi PPO, performansi iyilestirme ile bilinen, calisan bir stratejiye yakin kalma arasinda denge kurarak egitim sirasinda felaket niteiginde basarisizliklari onler ve daha kararli ogrenmeye yol acar.

**Direct Preference Optimization (DPO)**, buyuk dil modellerini (LLM) insan tercihlerine hizalamak icin ozellikle tasarlanmis daha yeni bir yontemdir. Bu gorev icin PPO kullanmaya daha basit ve daha dogrudan bir alternatif sunar.

DPO'yu anlamak icin, once geleneksel PPO tabanli hizalama yontemini anlamak yardimci olur:

* PPO Yaklasimi (Iki Adimli Surec):
  1. Bir Reward Model Egitme: Ilk olarak, insanlarin farkli LLM yanitlarini derecelendirdigi veya karsilastirdigi insan geri bildirim verileri toplanir (ornegin "Yanit A, Yanit B'den daha iyi"). Bu veriler, herhangi bir yeni yanita bir insanin verecegi puani tahmin etmek gorevi olan reward model adli ayri bir yapay zeka modeli egitmek icin kullanilir.
  2. PPO ile Fine-Tuning: Ardindan LLM, PPO kullanilarak fine-tune edilir. LLM'in hedefi, reward model'dan mumkun olan en yuksek puani alacak yanitlar uretmektir. Reward model, egitim oyunundaki "hakem" gorevi gorur.

Bu iki adimli surec karmasik ve dengesiz olabilir. Ornegin LLM, bir bosluk bulup kotu yanitlar icin yuksek puanlar almak uzere reward model'i "hack'lemeyi" ogrenebilir.

* DPO Yaklasimi (Dogrudan Surec): DPO, reward model'i tamamen atlar. Insan tercihlerini bir odul puanina donusturup sonra bu puan icin optimize etmek yerine, DPO tercih verilerini dogrudan LLM'in politikasini guncellemek icin kullanir.
* Tercih verilerini dogrudan optimal politikayla iliskilendiren matematiksel bir iliski kullanarak calisir. Esasen modele su ders verilir: "*Tercih edilen* yanita benzer yanitlar uretme olasiligini artir ve *tercih edilmeyen* yanita benzer yanitlar uretme olasiligini azalt."

Ozunde DPO, dil modelini dogrudan insan tercih verileri uzerinde optimize ederek hizalamayi basitlesitirir. Bu, ayri bir reward model egitmenin ve kullanmanin karmasikligini ve potansiyel dengesizligini onleyerek hizalama surecini daha verimli ve dayanikli hale getirir.

## Pratik Uygulamalar ve Kullanim Alanlari

Uyum saglayan agent'lar, deneyimsel verilere dayali yinelemeli guncellemeler araciligiyla degisken ortamlarda gelismis performans sergiler.

* **Kisisellestirilmis asistan agent'lari**, bireysel kullanici davranislarinin boylamsal analiziyle etkilesim protokollerini iyilestirerek son derece optimize edilmis yanit uretimi saglar.
* **Ticaret botu agent'lari**, yuksek cozunurluklu gercek zamanli piyasa verilerine dayali olarak model parametrelerini dinamik bir sekilde ayarlayarak karar verme algoritmalarini optimize eder ve boylece finansal getirileri maksimize edip risk faktorlerini azaltir.
* **Uygulama agent'lari**, gozlemlenen kullanici davranisina dayali dinamik degisiklik yoluyla kullanici arayuzunu ve islevselligini optimize eder ve kullanici katilimini ve sistem sezgiselligini artirir.
* **Robotik ve otonom arac agent'lari**, sensor verilerini ve gecmis eylem analizini entegre ederek navigasyon ve tepki yeteneklerini gelistirir ve cesitli cevre kosullarinda guvenli ve verimli calismayi mumkun kilar.
* **Dolandiricilik tespit agent'lari**, yeni tanimlanan dolandiricilik kaliplariyla tahmin modellerini iyilestirerek anomali tespitini gelistirir, sistem guvenligini artirir ve finansal kayiplari en aza indirir.
* **Oneri agent'lari**, kullanici tercih ogrenme algoritmalarini kullanarak icerik secim hassasiyetini gelistirir ve son derece bireysellestirilmis ve baglamsal olarak uygun oneriler sunar.
* **Oyun yapay zeka agent'lari**, stratejik algoritmalari dinamik olarak uyarlayarak oyuncu katilimini artirir ve boylece oyun karmasikligini ve zorlugunu yukseltir.
* **Bilgi Tabani Ogrenen Agent'lar**: Agent'lar, sorun tanimlamlari ve kanitlanmis cozumlerden olusan dinamik bir bilgi tabanini surdurmek icin Retrieval Augmented Generation (RAG) kullanabilir (bkz. Bolum 14). Basarili stratejileri ve karsilasilan zorlklari saklayarak agent, karar verme sirasinda bu verilere basvurabilir ve daha once basarili olan kaliplari uygulayarak veya bilinen tuzaklardan kacinarak yeni durumlara daha etkili bir sekilde uyum saglayabilir.

## Vaka Calismasi: Kendini Gelistiren Kodlama Agent'i (SICA)

Kendini Gelistiren Kodlama Agent'i (Self-Improving Coding Agent - SICA), Maxime Robeyns, Laurence Aitchison ve Martin Szummer tarafindan gelistirilmis olup agent tabanli ogrenmedeki bir ilerlemeyi temsil eder ve bir agent'in kendi kaynak kodunu degistirme kapasitesini gostermektedir. Bu, bir agent'in digerini egittigi geleneksel yaklasimlarin aksine; SICA, hem degistirici hem de degistirilen varlik olarak hareket ederek kod tabanini cesitli kodlama zorluklarindaki performansi iyilestirmek icin yinelemeli olarak iyilestirir.

SICA'nin kendini gelistirmesi yinelemeli bir dongu araciligiyla calisiir (bkz. Sekil 1). Baslangicta SICA, gecmis surumlerinin ve bunlarin benchmark testlerindeki performanslarinin bir arsivini inceler. Basari, zaman ve hesaplama maliyetini dikkate alan agirlikli bir formule dayali olarak hesaplanan en yuksek performans puanina sahip surumu secer. Ardindan bu secilen surum, bir sonraki kendini degistirme turunu ustlenir. Potansiyel iyilestirmeleri belirlemek icin arsivi analiz eder ve daha sonra kod tabanini dogrudan degistirir. Degistirilmis agent daha sonra benchmark'lara karsi test edilir ve sonuclar arsive kaydedilir. Bu surec tekrarlanarak dogrudan gecmis performanstan ogrenmeyi kolaylastirir. Bu kendini gelistirme mekanizmasi, SICA'nin geleneksel egitim paradigmalari gerektirmeden yeteneklerini evrimlestirmesine olanak tanir.

![SICA's self-improvement, learning and adapting based on its past versions](../assets/SICAs_self_improvement_learning_and_adapting_based_on_its_past_versions.png)

Sekil 1: SICA'nin kendini gelistirmesi, gecmis surumlerine dayali ogrenme ve uyum saglama

SICA onemli olcude kendini gelistirme sureci gecirdi ve bu, kod duzenleme ve gezinme alaninda ilerlemelere yol acti. Baslangicta SICA, kod degisiklikleri icin temel bir dosya uzerine yazma yaklasimi kullaniyordu. Ardindan daha akilli ve baglamsal duzenlemeler yapabilen bir "Smart Editor" gelistirdi. Bu, hedefli degisiklikler ve oruntu tabanli duzenleme icin diff'leri iceren bir "Diff-Enhanced Smart Editor"a ve isleme taleplerini azaltmak icin bir "Quick Overwrite Tool"a donustu.

SICA ayrica verimlilik icin Abstract Syntax Tree (AST) ayristirmasini kullanan "Minimal Diff Output Optimization" ve "Context-Sensitive Diff Minimization" uygulamalari gerceklestirdi. Ek olarak bir "SmartEditor Input Normalizer" eklendi. Gezinme acisindan SICA, kod tabanindaki tanimlari belirlemek icin kodun yapisal haritasini (AST) kullanan bir "AST Symbol Locator"u bagimsiz olarak olusturu. Daha sonra hizli arama ile AST kontrolunu birlestiren bir "Hybrid Symbol Locator" gelistirildi. Bu, ilgili kod bolumlierine odaklanarak arama hizini artiran "Optimized AST Parsing in Hybrid Symbol Locator" araciligiyla daha da optimize edildi (bkz. Sekil 2).

![Performance across Iterations](../assets/Performance_across_Iterations.png)

Sekil 2: Yinelemeler boyunca performans. Onemli iyilestirmeler, ilgili arac veya agent degisiklikleriyle aciklanmistir. (Maxime Robeyns, Martin Szummer, Laurence Aitchison'in izniyle)

SICA'nin mimarisi, temel dosya islemleri, komut yurutme ve aritmetik hesaplamalar icin temel bir arac takimi icerir. Sonuc gonderme ve ozellestirilmis alt agent'larin (kodlama, problem cozme ve akil yurutme) cagirilmasi icin mekanizmalar icerir. Bu alt agent'lar, karmasik gorevleri ayrıstirir ve ozellikle uzun iyilestirme donguleri sirasinda LLM'in baglam uzunlugunu yonetir.

Bir baska LLM olan asenkron bir gozetmen (overseer), SICA'nin davranisini izleyerek donguler veya durgunluk gibi potansiyel sorunlari belirler. SICA ile iletisim kurar ve gerektiginde yurutmeyi durdurmak icin mudahale edebilir. Gozetmen, oruntuleri ve verimsizlikleri belirlemek icin bir callgraph ve mesaj ile arac eylemlerinin bir logu dahil olmak uzere SICA'nin eylemlerinin ayrintili bir raporunu alir.

SICA'nin LLM'i, bilgileri context window'u, yani kisa sureli bellegi icinde, calisma icin kritik olan yapilandirilmis bir sekilde organize eder. Bu yapi, agent hedeflerini, arac ve alt agent dokumantasyonunu ve sistem talimatlarini tanimlayan bir System Prompt icerir. Bir Core Prompt, problem ifadesini veya talimati, acik dosyalarin icerigini ve bir dizin haritasini icerir. Assistant Messages, agent'in adim adim akil yurutmesini, arac ve alt agent cagri kayitlari ve sonuclarini ve gozetmen iletisimlerini kaydeder. Bu organizasyon, verimli bilgi akisini kolaylastirarak LLM islemini gelisitrir ve isleme suresini ve maliyetlerini azaltir. Baslangicta, dosya degisiklikleri yalnizca degisiklikleri gosteren ve periyodik olarak birlestirilen diff'ler olarak kaydedildi.

**SICA: Koda Bir Bakis:** SICA'nin uygulamasina daha derinden bakmak, yeteneklerini destekleyen birkac onemli tasarim secimini ortaya koyar. Tartisildiigi gibi sistem, kodlama agent'i, problem cozucu agent ve akil yurutme agent'i gibi birkac alt agent icereen moduler bir mimariyle insa edilmistir. Bu alt agent'lar, arac cagrilarina benzer sekilde ana agent tarafindan cagrilir ve karmasik gorevleri ayrisitirma ile ozellikle uzun meta-iyilestirme yinelemeleri sirasinda baglam uzunlugunu verimli bir sekilde yonetme gorevi gorur.

Proje aktif olarak gelistirilmekte olup, egitim sonrasi LLM'lerin tool use ve diger agentic gorevler uzerinde kullanilmasina ilgi duyanlara saglam bir framework sunmayi amaclamaktadir. Tam kod, daha fazla kesfetme ve katki icin [https://github.com/MaximeRobeyns/self_improving_coding_agent/](https://github.com/MaximeRobeyns/self_improving_coding_agent/) GitHub deposunda mevcuttur.

Guvenlik acisindan proje, Docker konteynerizasyonunu kuvvetle vurgular; bu, agent'in ozel bir Docker konteyneri icinde calistiigi anlamina gelir. Bu, agent'in kabuk komutlari yurutme yetenegini goz onune aldiginda ana makineden izolasyon saglayarak istenmeyen dosya sistemi manipulasyonu gibi riskleri azaltan kritik bir onlemdir.

Seffaflik ve kontrolu saglamak icin sistem, event bus'taki olaylari ve agent'in callgraph'ini goruntulestiiren etkiileisimli bir web sayfasi araciligiyla saglam gozlemlenebilirlik sunar. Bu, agent'in eylemlerine kapsamli icgoriler sunarak kullanicilarin bireysel olaylari incelemesine, gozetmen mesajlarini okumasina ve daha net bir anlayis icin alt agent izlerini daraltmasina olanak tanir.

Temel zekasi acisindan, agent framework'u cesitli saglayicilardan LLM entegrasyonunu destekleyerek belirli gorevler icin en uygun modeli bulmak uzere farkli modellerle deneme yapilmasini mumkun kilar. Son olarak, kritik bir bilesen, ana agent ile es zamanli olarak calisan asenkron gozetmendir. Bu gozetmen, agent'in davranisini periyodik olarak patolojik sapmalar veya durgunluk acisindan degerlendrir ve gerektiginde bildirim gonderek veya hatta agent'in yurutulmesini iptal ederek mudahale edebilir. Sistemin durumunun ayrintili bir metin temsilini alir; buna bir callgraph ve LLM mesajlari, arac cagrilari ve yanitlarin bir olay akisi dahildir; bu, verimsiz oruntuleri veya tekrarlanan calismayı tespit etmesine olanak tanir.

Ilk SICA uygulamasindaki dikkat cekici bir zorluk, LLM tabanli agent'in her meta-iyilestirme yinelemesinde bagimsiz olarak yeni, yenilikci, uygulanabilir ve ilgi cekici degisiklikler onermesini saglamakti. Bu sinirlilik, ozellikle LLM agent'larinda acik uclu ogrenmeyi ve otantik yaraticiligi tesvik etme konusunda, mevcut arastirmalarda temel bir inceleme alani olmaya devam etmektedir.

## AlphaEvolve ve OpenEvolve

**AlphaEvolve**, Google tarafindan algoritmalari kesfetmek ve optimize etmek icin gelistirilmis bir yapay zeka agent'idir. LLM'lerin, ozellikle Gemini modellerinin (Flash ve Pro), otomatik degerlendirme sistemlerinin ve evrimsel bir algoritma framework'unun bir kombinasyonunu kullanir. Bu sistem, hem teorik matematik hem de pratik bilisim uygulamalarini ilerlemeyi amaclar.

AlphaEvolve, bir Gemini model toplulugu kullanir. Flash, genis bir yelpazede baslangic algoritma onerileri uretmek icin kullanilirken, Pro daha derinlemesine analiz ve iyilestirme saglar. Onerilen algoritmalar daha sonra onceden tanimlanmis kriterlere gore otomatik olarak degerlendirilir ve puanlanir. Bu degerlendirme, cozumleri yinelemeli olarak iyilestirmek icin kullanilan geri bildirim saglayarak optimize edilmis ve yeni algoritmalara yol acar.

Pratik bilisim alaninda AlphaEvolve, Google'in altyapisi icinde konuslandirilmistir. Veri merkezi zamanlamasinda iyilestirmeler gostermis ve kuresel hesaplama kaynak kullaniminda %0,7'lik bir azalma saglamistir. Ayrica, yaklasan Tensor Processing Unit'ler (TPU'lar) icin Verilog kodunda optimizasyonlar onererek donanim tasarimina katki saglamistir. Dahasi AlphaEvolve, Gemini mimarisinin temel bir kernel'inda %23'luk bir hiz artisi ve FlashAttention icin dusuk duzeyli GPU talimatlarinda %32,5'e kadar optimizasyon dahil olmak uzere yapay zeka performansini hizlandirmistir.

Temel arastirma alaninda AlphaEvolve, 4x4 karmasik degerli matrisler icin 48 skaler carpma kullanan bir yontem dahil olmak uzere matris carpimi icin yeni algoritmalarin kesfine katki saglamis ve onceden bilinen cozumleri asmistir. Daha genis matematiksel arastirmalarda, 50'den fazla acik problemin %75'inde mevcut son teknoloji cozumleri yeniden kesfetmis ve %20'sinde mevcut cozumleri iyilestirmistir; ornekler arasinda opusme sayisi (kissing number) problemindeki ilerlemeler yer almaktadir.

**OpenEvolve**, kodu yinelemeli olarak optimize etmek icin LLM'lerden yararlanan evrimsel bir kodlama agent'idir (bkz. Sekil 3). LLM destekli kod uretimi, degerlendirme ve secim pipeline'ini duzenleyerek cesitli gorevler icin programlari surekli olarak gelistirir. OpenEvolve'un onemli bir yonu, tek fonksiyonlarla sinirli kalmak yerine tam kod dosyalarini evrimlestirme kapasitesidir. Agent, cok yonluluk icin tasarlanmistir; birden fazla programlama dili destegi ve herhangi bir LLM icin OpenAI uyumlu API'lerle uyumluluk sunar. Dahasi, cok amacli optimizasyon icerir, esnek prompt muhendisligi sunar ve karmasik kodlama zorluklarini verimli bir sekilde ele almak icin dagitik degerlendirme yapabilir.

![OpenEvolve Architecture](../assets/OpenEvolve_Architecture.png)

Sekil 3: OpenEvolve ic mimarisi bir controller tarafindan yonetilir. Bu controller birkac temel bileseni duzenleer: program sampler, Program Database, Evaluator Pool ve LLM Ensembles. Temel islevi, kod kalitesini artirmak icin bunlarin ogrenme ve uyum saglama (learning and adaptation) sureclerini kolaylastirmaktir.

Bu kod parcasi, bir program uzerinde evrimsel optimizasyon gerceklestirmek icin OpenEvolve kutuphanesini kullanir. Sistemi bir baslangic programi, bir degerlendirme dosyasi ve bir yapilandirma dosyasi yollariyla baslatir. `evolve.run(iterations=1000)` satiri, programin gelistirilmis bir surumunu bulmak icin 1000 yineleme boyunca evrimsel sureci baslatir. Son olarak, evrim sirasinda bulunan en iyi programin metriklerini dort ondalik basamaga kadar formatlanmis olarak yazdirir.

```python
from openevolve import OpenEvolve


# Initialize the system
evolve = OpenEvolve(
    initial_program_path="path/to/initial_program.py",
    evaluation_file="path/to/evaluator.py",
    config_path="path/to/config.yaml",
)

# Run the evolution
best_program = await evolve.run(iterations=1000)

print("Best program metrics:")
for name, value in best_program.metrics.items():
    print(f"  {name}: {value:.4f}")
```

## Bir Bakista

**Ne:** Yapay zeka agent'lari genellikle onceden programlanmis mantigin yetersiz kaldigi dinamik ve onceden tahmin edilemeyen ortamlarda calisir. Performanslari, ilk tasarimlari sirasinda ongoruiilmeyen yeni durumlarla karsilastiklarinda dusebilir. Deneyimden ogrenme yetenegine sahip olmadan agent'lar stratejilerini optimize edemez veya etkilesimlerini zaman icinde kisisellestiremez. Bu katiilik, etkililiklerini sinirlar ve karmasik, gercek dunya senaryolarinda gercek ozerklige ulasmaairini engeller.

**Neden:** Standartlastirilmis cozum, statik agent'lari dinamik, evrilen sistemlere donusturmek icin ogrenme ve uyum saglama mekanizmalaarini entegre etmektir. Bu, bir agent'in yeni verilere ve etkilesimlere dayali olarak bilgi ve davranislarini otonom bir sekilde iyilestirmesine olanak tanir. Agentic sistemler, reinforcement learning'den Kendini Gelistiren Kodlama Agent'i (SICA) ornegindeki gibi kendini degistirme gibi daha gelismis tekniklere kadar cesitli yontemler kullanabilir. Google'in AlphaEvolve'u gibi gelismis sistemler, karmasik problemlere tamamen yeni ve daha verimli cozumler kesfetmek icin LLM'ler ve evrimsel algoritmalardan yararlanir. Surekli ogrenme sayesinde agent'lar yeni gorevlerde ustalaasabilir, performanslarini gelistirebilir ve surekli manuel yeniden programlama gerektirmeden degisen kosullara uyum saglayabilir.

**Temel kural:** Bu kalibi, dinamik, belirsiz veya evrilen ortamlarda calismasi gereken agent'lar olustururken kullanin. Kisisellesitirme, surekli performans iyilestirmesi ve yeni durumlari otonom olarak ele alma yetenegine ihtiyac duyan uygulamalar icin vazgecilmezdir.

**Gorsel ozet:**

![Learning and Adapting Pattern](../assets/Learning_and_Adapting_Pattern.png)

Sekil 4: Ogrenme ve uyum saglama kalibi (Learning and Adapting Pattern)

## Temel Cikarimlar

* Ogrenme ve Uyum Saglama (Learning and Adaptation), agent'larin deneyimlerini kullanarak yaptiklari islerde daha iyi olmalari ve yeni durumlarla basa cikmalari hakkindadir.
* "Uyum saglama", bir agent'in davranisinda veya bilgisinde ogrenmeden kaynaklanan gorunur degisikliktir.
* SICA (Kendini Gelistiren Kodlama Agent'i), gecmis performansina dayali olarak kodunu degistirerek kendini gelistirir. Bu, Smart Editor ve AST Symbol Locator gibi araclara yol acmistir.
* Ozellestirilmis "alt agent'lar" ve bir "gozetmen"e sahip olmak, bu kendini gelistiren sistemlerin buyuk gorevleri yonetmesine ve yolda kalmasina yardimci olur.
* Bir LLM'in "context window"unun nasil yapilandirildigI (system prompt'lar, core prompt'lar ve assistant mesajlariyla) agent'larin ne kadar verimli calistigii icin son derece onemlidir.
* Bu kalip, her zaman degisen, belirsiz veya kisisel bir dokunusu gerektiren ortamlarda calismasi gereken agent'lar icin hayati onem tasir.
* Ogrenen agent'lar olusturmak genellikle onlari makine ogrenimi araclarina baglamayi ve veri akisini yonetmeyi gerektirir.
* Temel kodlama araclariyla donatilmis bir agent sistemi, kendini otonom olarak duzenleyebilir ve boylece benchmark gorevlerindeki performansini artirabilir.
* AlphaEvolve, Google'in LLM'ler ve evrimsel bir framework kullanarak algoritmalari otonom olarak kesfeden ve optimize eden yapay zeka agent'idir ve hem temel arastirmayI hem de pratik bilisim uygulamalarini onemli olcude gelistirir.

## Sonuc

Bu bolum, Yapay Zeka'da ogrenme ve uyum saglamanin kritik rollerini incellemektedir. Yapay zeka agent'lari, surekli veri edinimi ve deneyim yoluyla performanslarini gelistirir. Kendini Gelistiren Kodlama Agent'i (SICA), kod degisiklikleri araciligiyla yeteneklerini otonom olarak gelistirerek bunu orneklemektedir.

Mimari, uygulamalar, planlama (planning), coklu agent is birligi (multi-agent collaboration), bellek yonetimi (memory management) ile ogrenme ve uyum saglama dahil olmak uzere agentic yapay zekanin temel bilesenlerini inceledik. Ogrenme ilkeleri, ozellikle coklu agent sistemlerinde koordineli iyilestirme icin hayati onem tasir. Bunu basarmak icin ayar verilerinin, katilimci her agent'in bireysel giris ve ciktilarini yakalayarak tam etkilesim yolunu dogru bir sekilde yansitmasi gerekir.

Bu ogeler, Google'in AlphaEvolve'u gibi onemli ilerlemelere katki saglar. Bu yapay zeka sistemi, LLM'ler, otomatik degerlendirme ve evrimsel bir yaklasim kullanarak algoritmalari bagimsiz olarak kesfeder ve iyilestirir ve bilimsel arastirma ile hesaplama tekniklerinde ilerleme saglar. Bu tur kaliplar, sofistike yapay zeka sistemleri insa etmek icin birlestirilebilir. AlphaEvolve gibi gelismeler, yapay zeka agent'lari tarafindan otonom algoritmik kesif ve optimizasyonun ulascilabilir oldugunu gostermektedir.

## Kaynaklar

1. Sutton, R. S., & Barto, A. G. (2018). *Reinforcement Learning: An Introduction*. MIT Press.
2. Goodfellow, I., Bengio, Y., & Courville, A. (2016). *Deep Learning*. MIT Press.
3. Mitchell, T. M. (1997). *Machine Learning*. McGraw-Hill.
4. **Proximal Policy Optimization Algorithms** by John Schulman, Filip Wolski, Prafulla Dhariwal, Alec Radford, and Oleg Klimov. You can find it on arXiv: [https://arxiv.org/abs/1707.06347](https://arxiv.org/abs/1707.06347)
5. Robeyns, M., Aitchison, L., & Szummer, M. (2025). *A Self-Improving Coding Agent*. arXiv:2504.15228v2. [https://arxiv.org/pdf/2504.15228](https://arxiv.org/pdf/2504.15228)  [https://github.com/MaximeRobeyns/self_improving_coding_agent](https://github.com/MaximeRobeyns/self_improving_coding_agent)
6. AlphaEvolve blog, [https://deepmind.google/discover/blog/alphaevolve-a-gemini-powered-coding-agent-for-designing-advanced-algorithms/](https://deepmind.google/discover/blog/alphaevolve-a-gemini-powered-coding-agent-for-designing-advanced-algorithms/)
7. OpenEvolve, [https://github.com/codelion/openevolve](https://github.com/codelion/openevolve)
