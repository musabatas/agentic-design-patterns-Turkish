# **Sikca Sorulan Sorular: Agentic Tasarim Kaliplari (Design Patterns)**

## 1. "Agentic tasarim kalibi" nedir?

Agentic tasarim kalibi (design pattern), akilli, otonom sistemler (agent'lar) insa ederken karsilasilan yaygin bir soruna yeniden kullanilabilir, ust duzey bir cozumdur. Bu kaliplar, geleneksel programlamada yazilim tasarim kaliplarinin yaptigi gibi, agent davranislarini tasarlamak icin yapilandirilmis bir cerceve saglar. Gelistiricilerin daha saglam, ongorelulebilir ve etkili yapay zeka agent'lari olusturmalarina yardimci olur.

## 2. Bu rehberin ana amaci nedir?

Rehber, agentic sistemlerin tasarimi ve insasi icin pratik, uygulamali bir giris saglamayi amaclar. Teorik tartismalarin otesine gecerek, gelistiricilerin karmasik, hedef odakli davranisi guvenilir bir sekilde sergileyebilen agent'lar olusturmak icin kullanabilecegi somut mimari planlari sunar.

## 3. Bu rehberin hedef kitlesi kimdir?

Bu rehber, buyuk dil modelleri (LLM'ler) ve diger yapay zeka bilesenleriyle uygulamalar gelistiren yapay zeka gelistiricileri, yazilim muhendisleri ve sistem mimarlar icin yazilmistir. Basit prompt-yanit etkilesimlerinden sofistike, otonom agent'lar olusturmaya gecmek isteyenler icindir.

## 4. Tartisilan bazi temel agentic kaliplar nelerdir?

Icindekiler tablosuna gore rehber, su temel kaliplari kapsar:

- **Yansitma (Reflection):** Bir agent'in performansini iyilestirmek icin kendi eylem ve ciktilarini elestirme yetenegiu.
- **Planlama (Planning):** Karmasik bir hedefi daha kucuk, yonetilebilir adim veya gorevlere bolme sureci.
- **Tool Use:** Bir agent'in kendi basina yapamadigi bilgileri edinmek veya eylemleri gerceklestirmek icin harici araclari (kod yorumlayicilari, arama motorlari veya diger API'ler gibi) kullanma kalibi.
- **Multi-Agent Is Birligi (Collaboration):** Birden fazla uzman agent'in bir sorunu cozmek icin birlikte calistigi, genellikle bir "lider" veya "orkestrator" agent iceren mimari.
- **Human-in-the-Loop:** Bir agent'in eylemleri icin geri bildirim, duzeltme ve onay saglayarak insan gozetimi ve mudahalesinin entegrasyonu.

## 5. "Planlama" neden onemli bir kaliptir?

Planlama (Planning), bir agent'in tek bir eylemle cozulemeyen karmasik, cok adimli gorevleri ustlenmesine olanak tanidigi icin hayati onem tasir. Bir plan olusturarak agent, tutarli bir strateji surdürebilir, ilerlemesini takip edebilir ve hatalari veya beklenmedik engelleri yapilandirilmis bir sekilde yonetebilir. Bu, agent'in "takilmasini" veya kullanicinin nihai hedefinden sapmasini onler.

## 6. Bir agent icin "arac" ile "beceri" arasindaki fark nedir?

Terimler genellikle birbirinin yerine kullanilsa da, bir "arac" genellikle agent'in basvurabildigi harici bir kaynagi ifade eder (ornegin bir hava durumu API'si, bir hesap makinesi). Bir "beceri" ise agent'in ogrendigi, genellikle belirli bir islevi yerine getirmek icin tool use'u dahili akil yurutmeyle birlestiren daha entegre bir yetenektir (ornegin "ucak bileti alma" becerisi, takvim ve havayolu API'lerini kullanmayi icerebilir).

## 7. "Yansitma" (Reflection) kalibi bir agent'in performansini nasil iyilestirir?

Yansitma (Reflection), bir tür kendini duzeltme mekanizmasi olarak calisir. Bir yanit olusturduktdan veya bir gorevi tamamladiktan sonra, agent calismassini gozden gecirmesi, hatalari kontrol etmesi, belirli kriterlere gore kalitesini degerlendirmesi veya alternatif yaklasimlari degerlendirmesi icin yonlendirilebilir. Bu yinelemeli iyilestirme sureci, agent'in daha dogru, ilgili ve yuksek kaliteli sonuclar uretmesine yardimci olur.

## 8. Yansitma (Reflection) kalibinin temel fikri nedir?

Yansitma (Reflection) kalibi, bir agent'a geri adim atarak kendi calismassini elestirme yetenegini verir. Tek seferde nihai bir cikti uretmek yerine, agent bir taslak olusturur ve ardindan kusurlar, eksik bilgiler veya iyilestirme alanlari belirleyerek uzerinde "yansima" yapar. Bu kendini duzeltme sureci, yanitlarinin kalitesini ve dogrulugunu artirmanin anahtaridir.

## 9. Yuksek kaliteli cikti icin basit "prompt chaining" neden yeterli degildir?

Basit prompt chaining (bir prompt'un ciktisinin bir sonrakinin girdisi haline geldigi) genellikle cok temeldir. Model, gercekten iyilestirmeden onceki ciktisini sadece yeniden ifade edebilir. Gercek bir Yansitma (Reflection) kalibi, agent'in calismassini belirli standartlara gore analiz etmesini, mantik hatalarini kontrol etmesini veya olgulari dogrulamasini gerektiren daha yapilandirilmis bir elestiri gerektirir.

## 10. Bu bolumde bahsedilen iki ana yansitma turu nedir?

Bolum, iki temel yansitma bicimine deginir:

- **"Isini kontrol et" Yansitmasi:** Agent'in yalnizca onceki ciktisini gozden gecirmesi ve duzeltmesi istenen temel bir bicimldir. Basit hatalari yakalamak icin iyi bir baslangic noktasidir.
- **"Ic Elestirmen" Yansitmasi:** "Calisan" agent'in ciktisini degerlendirmek icin ayri bir "elestirmen" agent'in (veya ozel bir prompt'un) kullanildigi daha gelismis bir bicimldir. Bu elestiremne, aradigl belirli kriterler verilebilir ve bu da daha titiz ve hedefli iyilestirmelere yol acar.

## 11. Yansitma (Reflection) hallucination'lari azaltmada nasil yardimci olur?

Bir agent'i calismassini gozden gecirmeye, ozellikle ifadelerini bilinen bir kaynakla karsilastirarak veya kendi akil yurutme adimlarini kontrol ederek yonlendirmek, Yansitma (Reflection) kalibi hallucination (uydurma olgu uretme) olasililigini onemli olcude azaltabilir. Agent, saglanan baglamda daha fazla temellenmeye ve desteklenmemis bilgi uretme olasiliiginin azalmasina zorlanir.

## 12. Yansitma (Reflection) kalibi birden fazla kez uygulanabilir mi?

Evet, yansitma yinelemeli bir surec olabilir. Bir agent, her dongude ciktisini daha da iyilestirerek calismassini birden fazla kez yansitmaya tabi tutulabilir. Bu, ilk veya ikinci denemenin hala ince hatalar icerebilecegi veya onemli olcude iyilestirilebilecegi karmasik gorevler icin ozellikle yararlidir.

## 13. Yapay zeka agent'lari baglaminda Planlama (Planning) kalibi nedir?

Planlama (Planning) kalibi, bir agent'in karmasik, ust duzey bir hedefi daha kucuk, eyleme donusturulebilir adimlar dizisine bolmesini icerircr. Buyuk bir problemi tek seferde cozmeye calismak yerine, agent once bir "plan" olusturur ve ardindan plandaki her adimi uygular; bu cok daha guvenilir bir yaklasimdir.

## 14. Karmasik gorevler icin planlama neden gereklidir?

LLM'ler birden fazla adim veya bagimlilik gerektiren gorevlerde zorlanabilir. Bir plan olmadan, bir agent genel hedefi gozden kacirrabilir, onemli adimlari atlayabilir veya bir adimin ciktisini sonraki icin girdi olarak isleyemeyebilir. Bir plan, orijinal istegin tum gereksinimlerinin mantiksal bir sirada karsilanmasini saglayan net bir yol haritasi saglar.

## 15. Planlama (Planning) kalibini uygulamanin yaygin bir yolu nedir?

Yaygin bir uygulama, agent'in once yapilandirilmis bir formatta (JSON dizisi veya numarali liste gibi) bir adim listesi uretmesidir. Sistem daha sonra bu listeyi yineleyerek her adimi tek tek yurutur ve sonucu bir sonraki eylemi bilgilendirmek icin agent'a geri besler.

## 16. Agent, yurutme sirasinda hatalari veya degisiklikleri nasil yonetir?

Saglam bir planlama kalibi, dinamik ayarlamalara olanak tanir. Bir adim basarisiz olursa veya durum degisirse, agent mevcut durumdan "yeniden planlamaya" yonlendirilebilir. Hatayi analiz edebilir, kalan adimlari degistirebilir veya engeli asmak icin yeni adimlar bile ekleyebilir.

## 17. Kullanici plani gorur mu?

Bu bir tasarim tercidhidir. Bircok durumda, onay icin plani once kullaniciya gostermek iyi bir uygulamadir. Bu, "Human-in-the-Loop" kalibiyla uyumludur ve kullaniciya, agent'in onerilen eylemleri yurutulmeden once seffaflik ve kontrol saglar.

## 18. "Tool Use" kalibi neyi icerir?

Tool Use kalibi, bir agent'in harici yazilim veya API'lerle etkilesime girerek yeteneklerini genisletmesine olanak tanir. Bir LLM'nin bilgisi statik oldugundan ve kendi basina gercek dunya eylemleri gerceklestiremeyeceginden, araclar canli bilgiye (ornegin Google Search), ozel verilere (ornegin bir sirketin veritabani) veya eylem gerceklestirme kapasitesine (ornegin e-posta gonderme, toplanti planlama) erisim saglar.

## 19. Bir agent hangi araci kullanacagina nasil karar verir?

Agent'a genellikle mevcut araclarin bir listesi ve her aracin ne yaptigina ve hangi parametreleri gerektirdigine dair aciklamalar verilir. Dahili bilgisiyle basedeyemeyecegi bir istekle karsilastiginda, agent'in akil yurutme yeteneği gorevi tamamlamak icin listeden en uygun araci secmesine olanak tanir.

## 20. Bu baglamda bahsedilen "ReAct" (Reason and Act) framework'u nedir?

ReAct, akil yurutme ve eylemi birlestiren populer bir framework'tur. Agent, **Thought** (ne yapmassi gerektigini dusunme), **Action** (hangi araci hangi girdilerle kullanacagina karar verme) ve **Observation** (aractan gelen sonucu gorme) dongusunu takip eder. Bu dongu, kullanicinin istegini yerine getirmek icin yeterli bilgi toplayana kadar devam eder.

## 21. Tool use uygulamasinda bazi zorluklar nelerdir?

Temel zorluklar sunlardir:

- **Hata Yonetimi (Exception Handling):** Araclar basarisiz olabilir, beklenmedik veriler dondurebilir veya zaman asimina ugrabilir. Agent'in bu hatalari taniyabilmesi ve tekrar denemeye, farkli bir arac kullanmaya veya kullanicidan yardim istemeye karar verebilmesi gerekir.
- **Guvenlik (Safety):** Bir agent'a araclara, ozellikle eylem gerceklestiren araclara erisim vermek, guvenlik etkileri tasir. Hassas islemler icin guvenlik onlemleri, izinler ve genellikle insan onayi olmassi hayati onem tasir.
- **Prompt Olusturma:** Agent'in dogru bicimlendirilmis arac cagrilari (ornegin dogru fonksiyon adi ve parametreler) uretmesi icin etkili bir sekilde yonlendirilmesi gerekir.

## 22. Human-in-the-Loop (HITL) kalibi nedir?

HITL, agent'in is akisina insan gozetimi ve etkilesimini entegre eden bir kaliptir. Tamamen otonom olmak yerine, agent kritik noktalarda insan geri bildirimi, onayi, aciklama veya yonlendirme istemek icin durakslar.

## 23. HITL agentic sistemler icin neden onemlidir?

Birkac nedenden dolayi hayati onem tasir:

- **Guvenlik ve Kontrol (Safety):** Yuksek riskli gorevler (ornegin finansal islemler, resmi yazismalar gonderme) icin HITL, agent'in onerilen eylemlerinin yurutulmeden once bir insan tarafindan dogrulanmasini saglar.
- **Kalitenin Iyilestirilmesi:** Insanlar, agent'in performansini iyilestirmek icin kullanabilecegi duzeltmeler veya nüansli geri bildirim saglayabilir, ozellikle oznel veya belirsiz gorevlerde.
- **Guven Olusturma:** Kullanicilarin yonlendirebilecekleri ve denetleyebilecekleri bir yapay zeka sistemine guvenme ve benimseme olasiliigi daha yuksektir.

## 24. Bir is akisinin hangi noktalarinda insan dahil edilmelidir?

Insan mudahalesi icin yaygin noktalar sunlardir:

- **Plan Onayi:** Cok adimli bir plani yurutmeden once.
- **Tool Use Onayi:** Gercek dunya sonuclari olan veya maliyeti olan bir araci kullanmadan once.
- **Belirsizlik Cozumu:** Agent nasil devam edeceginden emin olmadiginda veya kullanicidan daha fazla bilgiye ihtiyac duyduğunda.
- **Nihai Cikti Incelemesi:** Nihai sonucu son kullaniciya veya sisteme teslim etmeden once.

## 25. Surekli insan mudahalesi verimsiz degil mi?

Olabilir, bu yuzden anahtar, dogru dengeyi bulmaktir. HITL, her bir eylem icin degil, kritik kontrol noktalarinda uygulanmalıdir. Amac, insan ve agent arasinda, agent'in isin buyuk bolumunu ustlendigi ve insanin stratejik yonlendirme sagladigi is birlikci bir ortaklik kurmaktir.

## 26. Multi-Agent Is Birligi (Collaboration) kalibi nedir?

Bu kalip, ortak bir hedefe ulasmak icin birlikte calisan birden fazla uzman agent'dan olusan bir sistem olusturmayi icerir. Her seyi yapmaya calisan tek bir "genel" agent yerine, her biri belirli bir role veya uzmanlık alanina sahip bir "uzman" agent ekibi olusturulur.

## 27. Multi-agent sistemlerin faydalari nelerdir?

- **Modulerlik ve Uzmanlasma:** Her agent, belirli gorevi icin ince ayar yapilabilir ve yonlendirilebilir (ornegin bir "arastirmaci" agent, bir "yazar" agent, bir "kod" agent), bu da daha yuksek kaliteli sonuclara yol acar.
- **Azaltilmis Karmasiklik:** Karmasik bir is akisini uzman rollere bölmek, genel sistemi tasarlamayi, hata ayiklamayi ve bakimini kolaylastirir.
- **Benzetimli Beyin Firtinasi:** Farkli agent'lar bir probleml hakkinda farkli bakis acilari sunabilir ve bir insan ekibinin calismasina benzer sekilde daha yaratici ve saglam cozumlere yol acabilir.

## 28. Multi-agent sistemler icin yaygin bir mimari nedir?

Yaygin bir mimari, bir **Orkestrator Agent** (bazen "yonetici" veya "sef" olarak adlandirilir) icerir. Orkestrator genel hedefi anlar, onu parcalar ve alt gorevleri uygun uzman agent'lara devreder. Ardindan uzmanlarin sonuclarini toplayarak nihai bir ciktiya sentezler.

## Agent'lar birbirleriyle nasil iletisim kurar?

Iletisim genellikle orkestrator tarafindan yonetilir. Ornegin, orkestrator "arastirmaci" agent'in ciktisini "yazar" agent'a baglam olarak aktarabilir. Agent'larin bulgularini paylasabilecegi paylasimli bir "karalama tahtasi" veya mesaj veri yolu, baska bir yaygin iletisim yontemidir.

## Bir agent'i degerlendirmek neden geleneksel bir yazilim programini degerlendirmekten daha zordur?

Geleneksel yazilimin deterministik ciktilari vardir (ayni girdi her zaman ayni ciktiyi uretir). Agent'lar, ozellikle LLM kullananlar, deterministik degildir ve performanslari oznel olabilir. Onlari degerlendirmek, yalnizca teknik olarak "dogru" olup olmadiğini degil, ciktillarinin *kalitesini* ve *ilgililigini* degerlendirmeyi gerektirir.

## Agent performansini degerlendirmek icin bazi yaygin yontemler nelerdir?

Rehber birkac yontem oner:

- **Sonuc Tabanli Degerlendirme:** Agent nihai hedefe basariyla ulasti mi? Orneğin, gorev "bir ucak bileti al" idiyse, bir bilet gercekten dogru bir sekilde alindi mi? Bu en onemli olcuttur.
- **Surec Tabanli Degerlendirme:** Agent'in *sureci* verimli ve mantikli miydi? Dogru araclari kullandı mi? Makul bir plan izledi mi? Bu, bir agent'in neden basarisiz olabileceğini hata ayiklamaya yardimci olur.
- **Insan Degerlendirmesi:** Insanların agent'in performansini yardimcilik, dogruluk ve tutarlilik gibi kriterlere gore bir olcekte (ornegin 1-5) puanlamasi. Bu, kullaniciya yonelik uygulamalar icin hayati onem tasir.

## "Agent trajectory" nedir?

Agent trajectory, bir agent'in bir gorevi yerine getirirken attigi adimlarin tam kaydiidir. Tum dusunceleri, eylemleri (arac cagrilari) ve gozlemlerini icerir. Bu trajectory'lerin analizi, agent davranisini hata ayiklama ve anlamanin onemli bir parcasidir.

## Deterministik olmayan bir sistem icin guvenilir testler nasil olusturulur?

Bir agent'in ciktisinin tam ifadesini garanti edemezsiniz, ancak temel unsurlari kontrol eden testler olusturabilirsiniz. Ornegin, agent'in nihai yanitinin belirli bilgileri *icerip icermedigini* veya belirli bir araci dogru parametrelerle basariyla çağırıp çağırmadığını dogrulayan bir test yazabilirsiniz. Bu genellikle ozel bir test ortaminda sahte araclar kullanilarak yapilir.

## Bir agent'a prompt vermek basit bir ChatGPT prompt'undan nasil farklidir?

Bir agent'a prompt vermek, isletim talimatlari olarak islev goren ayrintili bir "system prompt" veya anayasa olusturmayi icerir. Bu, tek bir kullanici sorgusunun otesine gecer; agent'in rolunu, mevcut araclarini, izlemesi gereken kaliplari (ReAct veya Planlama gibi), kisitlamalarini ve kisiligini tanimlar.

## Bir agent icin iyi bir system prompt'un temel bilesenleri nelerdir?

Guclu bir system prompt tipik olarak sunlari icerir:

- **Rol ve Hedef:** Agent'in kim oldugunu ve birincil amacinin ne oldugunu acikca tanimlayin.
- **Arac Tanimlari:** Mevcut araclarin, aciklamalarinin ve nasil kullanilacaginin bir listesi (ornegin belirli bir function calling formatinda).
- **Kisitlamalar ve Kurallar:** Agent'in ne *yapmamasi* gerektigine dair acik talimatlar (ornegin "Onay almadan arac kullanmayin," "Finansal tavsiye vermeyin").
- **Surec Talimatlari:** Hangi kaliplarin kullanilacagina dair rehberlik. Ornegin, "Once bir plan olusturun. Ardindan, plani adim adim yurutun."
- **Ornek Trajectory'ler:** Basarili "dusunce-eylem-gozlem" dongulericin birkac ornek saglamak, agent'in guvenilirligini onemli olcude iyilestirebilir.

## "Prompt leakage" nedir?

Prompt leakage, system prompt'un parcalarinin (arac tanimlari veya dahili talimatlar gibi) agent'in kullaniciya verdigi nihai yanitte yanlislikla aciga cikmasi durumudur. Bu, kullanici icin kafa karistirici olabilir ve altta yatan uygulama ayrintolarini ifsa edebilir. Akil yurutme ve nihai yanit olusturma icin ayri prompt'lar kullanma gibi teknikler bunu onlemeye yardimci olabilir.

## Agentic sistemlerde bazi gelecek egilimleri nelerdir?

Rehber, su gelecege isaret eder:

- **Daha Otonom Agent'lar:** Daha az insan mudahalesi gerektiren ve kendi baslarina ogrenip uyum saglayabilen agent'lar.
- **Yuksek Derecede Uzmanlasmis Agent'lar:** Belirli gorevler icin kiralanabilir veya abone olunabilir bir agent ekosistemi (ornegin bir seyahat agent'i, bir arastirma agent'i).
- **Daha Iyi Araclar ve Platformlar:** Saglam multi-agent sistemleri olusturmayi, test etmeyi ve dagitmayi kolaylastiran daha sofistike framework'ler ve platformlarin gelistirilmesi.
