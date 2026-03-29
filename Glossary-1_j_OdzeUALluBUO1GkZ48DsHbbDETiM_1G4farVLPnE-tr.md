# Sozluk

## Temel Kavramlar

**Prompt:** Prompt, bir kullanicinin bir yapay zeka modeline yanit almak icin sundugu, genellikle soru, talimat veya ifade seklindeki girdidir. Prompt'un kalitesi ve yapisi, modelin ciktisini buyuk olcude etkiler ve prompt muhendisligini yapay zekayi etkili bir sekilde kullanmak icin onemli bir beceri haline getirir.

**Context Window:** Context window, bir yapay zeka modelinin hem girdiyi hem de urettigi ciktiyi dahil ederek bir seferde isleyebildigi maksimum token sayisidir. Bu sabit boyut kritik bir sinirlamadir; pencere disindaki bilgi goz ardi edilirken, daha buyuk pencereler daha karmasik konusmalara ve belge analizine olanak tanir.

**In-Context Learning:** In-context learning, bir yapay zekanin herhangi bir yeniden egitim gerektirmeden dogrudan prompt icinde verilen orneklerden yeni bir gorevi ogrenme yetenegidir. Bu guclu ozellik, tek bir genel amacli modelin aninda sayisiz belirli goreve uyarlanmasini saglar.

**Zero-Shot, One-Shot ve Few-Shot Prompting:** Bunlar, bir modele bir gorevi yonlendirmek icin sifir, bir veya birkaç ornek verilen prompt tekniklerindir. Daha fazla ornek saglamak, genellikle modelin kullanicinin niyetini daha iyi anlamasina yardimci olur ve belirli gorev icin dogrulugunu arttirir.

**Multimodality:** Multimodality, bir yapay zekanin metin, goruntu ve ses gibi birden fazla veri turundeki bilgiyi anlama ve isleme yetenegidir. Bu, bir goruntuyu tanimlama veya sozlu bir soruyu cevaplama gibi daha cok yonlu ve insana benzer etkilesimlere olanak tanir.

**Grounding:** Grounding, bir modelin ciktilarini olgusal dogrulugu saglamak ve hallucination'lari azaltmak icin dogrulanabilir, gercek dunya bilgi kaynaklarina baglama surrecidir. Bu genellikle yapay zeka sistemlerini daha guvenilir kilmak icin RAG gibi tekniklerle gerceklestirilir.

## Temel Yapay Zeka Model Mimarileri

**Transformers:** Transformer, cogu modern LLM'nin temelini olusturan sinir agi mimarisidir. Temel yeniligi, uzun metin dizilerini verimli bir sekilde isleyen ve kelimeler arasindaki karmasik iliskileri yakalayan self-attention mekanizmasidir.

**Recurrent Neural Network (RNN):** Recurrent Neural Network, Transformer'dan once gelen temel bir mimaridir. RNN'ler bilgiyi sirasiyla isler ve onceki girdilerin bir "bellegini" korumak icin donguler kullanir; bu da onlari metin ve konusma isleme gibi gorevler icin uygun hale getirmistir.

**Mixture of Experts (MoE):** Mixture of Experts, bir "router" agin herhangi bir girdiyi islemek icin dinamik olarak kucuk bir "uzman" ag alt kumesi sectigi verimli bir model mimarisidir. Bu, modellerin hesaplama maliyetlerini yonetilebilir tutarken cok sayida parametreye sahip olmasina olanak tanir.

**Diffusion Models:** Diffusion modelleri, yuksek kaliteli goruntular olusturmada ustun olan uretici modellerdir. Verilere rastgele gurultu ekleyerek ve ardindan bir modeli bu sureci titizlikle tersine cevirmek icin egiterek calisir, boylece rastgele bir baslangic noktasindan yeni veriler uretebilirler.

**Mamba:** Mamba, ozellikle cok uzun baglamlar icin yuksek verimlilikle dizileri islemek amaciyla Selective State Space Model (SSM) kullanan yeni bir yapay zeka mimarisidir. Secici mekanizmasi, gurultuyu filtrelerken ilgili bilgiye odaklanmasina olanak tanir ve onu Transformer'a potansiyel bir alternatif yapar.

## LLM Gelistirme Yasam Dongusu

Guclu bir dil modelinin gelistirilmesi belirli bir diziyi takip eder. Genel internet metinlerinden olusan genis bir veri kumesi uzerinde egitilerek dil, akil yurutme ve dunya bilgisi ogrenmesini saglayan buyuk bir temel modelin insa edildigi Pre-training ile baslar. Ardindan, genel modelin yeteneklerini belirli bir amac icin uyarlamak amaciyla daha kucuk, goreve ozel veri kumeleri uzerinde daha fazla egitildigi uzmanlaasma asamasi olan Fine-tuning gelir. Son asama, ozellestirilmis modelin davranisinin, ciktilarinin yardimci, zararsiz ve insan degerleriyle uyumlu olmasini saglamak icin ayarlandigi Alignment'tir.

**Pre-training Teknikleri:** Pre-training, bir modelin buyuk miktarda veriden genel bilgi ogrendigi ilk asamadir. Bunun icin en onemli teknikler, modelin ogrenecegi farkli hedefler icerir. En yaygin olani, modelin bir cumledeki sonraki kelimeyi tahmin ettigi Causal Language Modeling (CLM)'dir. Bir digeri, modelin bir metindeki kasitli olarak gizlenmis kelimeleri doldurdugu Masked Language Modeling (MLM)'dir. Diger onemli yontemler arasinda modelin bozulmus bir girdiyi orijinal durumuna geri yuklemesini ogrendigi Denoising Objectives, benzer ve benzer olmayan veri parcalari arasinda ayrım yapmayi ogrendigi Contrastive Learning ve iki cumlenin mantiksal olarak birbirini takip edip etmedigini belirlediği Next Sentence Prediction (NSP) yer alir.

**Fine-tuning Teknikleri:** Fine-tuning, genel bir on-egitimli modeli daha kucuk, ozellestirilmis bir veri kumesi kullanarak belirli bir goreve uyarlama suresidir. En yaygin yaklasim, modelin dogru girdi-cikti ciftlerinin etiketli ornekleri uzerinde egitildigi Supervised Fine-Tuning (SFT)'dir. Populer bir varyant, modeli kullanici komutlarini daha iyi takip etmeye odaklanan Instruction Tuning'dir. Bu sureci daha verimli hale getirmek icin, yalnizca az sayida parametreyi guncelleyen LoRA (Low-Rank Adaptation) ve bellek optimize edilmis surumu QLoRA gibi en onemli teknikleri iceren Parameter-Efficient Fine-Tuning (PEFT) yontemleri kullanilir. Bir baska teknik olan Retrieval-Augmented Generation (RAG), fine-tuning veya cikarim asamasinda modeli harici bir bilgi kaynagina baglayarak gelistirir.

**Alignment ve Guvenlik Teknikleri:** Alignment, bir yapay zeka modelinin davranisinin insan degerleri ve beklentileriyle uyumlu olmasini saglama, onu yardimci ve zararsiz kilma suresidir. En one cikan teknik, insan tercihlerine gore egitilmis bir "odul modeli"nin yapay zekanin ogrenme surecini yonlendirdigi, genellikle kararlilik icin Proximal Policy Optimization (PPO) gibi bir algoritma kullanan Reinforcement Learning from Human Feedback (RLHF)'dir. Ayri bir odul modeline olan ihtiyaci ortadan kaldiran Direct Preference Optimization (DPO) ve veri toplama isini daha da basitlestiren Kahneman-Tversky Optimization (KTO) gibi daha basit alternatifler ortaya cikmistir. Guvenli dagitimi saglamak icin, ciktiları filtrelemek ve zararli eylemleri gercek zamanli olarak engellemek amaciyla son bir guvenlik katmani olarak Guardrails uygulanir.

## Yapay Zeka Agent Yeteneklerinin Gelistirilmesi

Yapay zeka agent'lari, cevrelereini algilayabilen ve hedeflere ulasmak icin otonom eylemler gerceklestirebilen sistemlerdir. Etkililikleri, saglam akil yurutme (reasoning) cerceveleriyle arttirilir.

**Chain of Thought (CoT):** Bu prompt teknigi, bir modeli son bir cevap vermeden once adim adim akil yurutmesini aciklamaya tesvik eder. Bu "yuksek sesle dusunme" sureci, genellikle karmasik akil yurutme gorevlerinde daha dogru sonuclara yol acar.

**Tree of Thoughts (ToT):** Tree of Thoughts, bir agent'in bir agacin dallari gibi birden fazla akil yurutme yolunu es zamanli olarak kesfettigi gelismis bir akil yurutme cercevesidir. Agent'in farkli dusunce hatlarini kendi kendine degerlendirmesine ve takip edilecek en umut verici olani secmesine olanak tanir ve karmasik problem cozmede daha etkili hale getirir.

**ReAct (Reason and Act):** ReAct, akil yurutme ve eylemi bir dongu icinde birlestiren bir agent framework'udur. Agent once ne yapacagini "dusunur", ardindan bir arac kullanarak bir "eylem" gerceklestirir ve sonuc olarak elde edilen gozlemi bir sonraki dusuncesini bilgilendirmek icin kullanir; bu da onu karmasik gorevleri cozmede son derece etkili kilar.

**Planlama (Planning):** Bu, bir agent'in ust duzey bir hedefi daha kucuk, yonetilebilir alt gorevler dizisine bolme yetenegidir. Agent daha sonra bu adimlari sirasiyla yurutmek icin bir plan olusturur ve karmasik, cok adimli gorevleri yerine getirmesine olanak tanir.

**Deep Research:** Deep research, bir agent'in bilgiyi yinelemeli olarak arayarak, bulgulari sentezleyerek ve yeni sorular belirleyerek bir konuyu derinlemesine otonom olarak kesfetme kapasitesini ifade eder. Bu, agent'in tek bir arama sorgusunun cok otesinde bir konu hakkinda kapsamli bir anlayis olusturmasina olanak tanir.

**Critique Model:** Critique model, baska bir yapay zeka modelinin ciktisini incelemek, degerlendirmek ve geri bildirim saglamak icin egitilmis ozellestirilmis bir yapay zeka modelidir. Otomatik bir elestirmen olarak gorev yapar ve hatalari belirlemeye, akil yurutmeyi iyilestirmeye ve nihai ciktinin istenen kalite standardini karsilamasini saglamaya yardimci olur.
