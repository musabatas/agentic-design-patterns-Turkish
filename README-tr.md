# Agentic Tasarim Kaliplari

Bu depo, Antonio Gulli ve Mauro Sauco tarafindan yazilan "Agentic Design Patterns" kitabinin tam metnini icerir. Icerik, topluluk icin kolay erisim ve referans amaciyla Tom Mathews tarafindan derlenmis ve duzenlenmistir.

![Agentic Design Patterns - Kitap Kapagi](assets/Agentic_Design_Patterns_Book_Cover.png)

## Yazarlik ve Kredi

- **Yazarlar:** [Antonio Gulli](https://www.linkedin.com/in/searchguy/) ve [Mauro Sauco](https://www.linkedin.com/in/maurosauco/)
- **Derleyen:** [Tom Mathews](https://www.linkedin.com/in/mathews-tom/)

### Bu kitabi ozel kilan nedir?

Bu 424 sayfalik rehber, akilli, otonom yapay zeka sistemleri insa ederken karsilastigimiz gercek zorluklari ele almaktadir. Teori ile uygulama arasindaki bosluğu kapatır — tam da alanımızın su an ihtiyac duydugu sey. Gercek yapay zeka sistemleri insa etme konusunda ciddi olan herkes icin en iyi kaynaktir. Temel LLM uygulamalarinin otesine gecmeye ve gercekten saglam yapay zeka agent'lari olusturmaya hazir bir muhendis, arastirmaci veya urun yoneticisiyseniz, bu kitap tam size goredir.

Kitap, Prompt Chaining, Yonlendirme (Routing), Planlama (Planning) ve Multi-Agent Sistemler dahil olmak uzere temel agentic kaliplari, hepsi pratik, kod tabanli orneklerle kapsar. Tool Use, Bellek Yonetimi (Memory Management) ve RAG uygulamasinin kapsamli kapsami ile Akil Yurutme Teknikleri (Reasoning Techniques) ve Agent'lar Arasi Iletisim (Inter-Agent Communication) gibi ileri konulari bulacaksiniz.

Icinde bulacaklariniz:

- **Gercek kod ornekleri:** Yalnizca teori degil, calisan uygulamalar.
- **Kanitlanmis kaliplar:** Bellek yonetimi, istisna mantigi, kaynak kontrolu, guvenlik guardrail'leri.
- **Ileri teknikler:** Multi-agent orkestrasyon, agent'lar arasi mesajlasma, human-in-the-loop.
- **MCP (Model Context Protocol) icin tam bir bolum:** Araclari agent'larla entegre etmek icin temel bir framework.

4 bolum boyunca 21 temel kalibi kapsar:

1. Temel kaliplar (prompt chaining, routing, tool use)
2. Ileri sistemler (bellek, ogrenme, izleme)
3. Uretim kaygilari (hata yonetimi, guvenlik, degerlendirme)
4. Multi-agent mimarileri

Cogu yapay zeka icerigi "bir API nasil cagrilir" noktasinda durur. Ancak gercek dunya sistemlerinde su sorulari sormalisiniz:

- Ya agent gorev ortasinda takilirsa?
- Uzun oturumlar boyunca bellegi nasil koruyorsunuz?
- 10'dan fazla agent calistirdiginizda kaosu nasil onluyorsunuz?

Bu kitap, tum bunlari gercekten uygulayabileceginiz kaliplarla cevaplar. Yalnizca 70'ten fazla sayfalik ek bile yatirima deger; Gelismis Prompt teknikleri ve Agentic Framework'lere genel bakis icerir.

## Icindekiler

### Giris

- [Ithaf](00-Introduction/01-Dedication-1cQ61mNpiWn6eSORmWjEjF44vN2Lpba8kyKmNwIC60ig.md)
- [Tesekkur](00-Introduction/02-Acknowledgment-1u2y6tY48bw8nriDUuwWEf9s8g66vyIqBKSKZDOS-n0s.md)
- [Onsoz](00-Introduction/03-Foreword-18Q9kfZuCTL37ztrSjLxwf8Elr5UfAiAavmnj0IqSpbU.md)
- [Bir Dusunce Liderinin Bakis Acisi: Guc ve Sorumluluk](00-Introduction/04-A_Thought_Leaders_Perspective_Power_and_Responsibility-1PWhaXD_UNKgJaxYe3JBxRFRt3_B8Wm67CFxtSBQ4LkU.md)
- [Giris](00-Introduction/05-Introduction-1K5jwqB6jh20uHL0TTWxqWOxFk-dzFxRvHzrRRV79hrg.md)
- [Bir Yapay Zeka Sistemini Agent Yapan Nedir?](00-Introduction/06-What_makes_an_AI_system_an_Agent-1Nw6hRa7ItdLr_Tj5hF2q-OH8B_uPKb--RLn8SXZKA94.md)

### Birinci Bolum: Temel Kaliplar

- [Bolum 1: Prompt Chaining](01-Part_One/Chapter_1-Prompt_Chaining-1flxKGrbnF2g8yh3F-oVD5Xx7ZumId56HbFpIiPdkqLI.md)
- [Bolum 2: Yonlendirme (Routing)](01-Part_One/Chapter_2-Routing-1ux_n8n3T4bYndOjs1DKW5ccpC802KISdy2IWnlvYbas.md)
- [Bolum 3: Paralelizasyon (Parallelization)](01-Part_One/Chapter_3-Parallelization-1XVMp4RcRkoUJTVbrP2foWZX703CUJpWkrhyFU2cfUOA.md)
- [Bolum 4: Yansitma (Reflection)](01-Part_One/Chapter_4-Reflection-1HXXJOQIMWowtLw4WMiSR360caDAlZPtl5dPPgvq9IT4.md)
- [Bolum 5: Tool Use (Function Calling)](01-Part_One/Chapter_5-Tool_Use_(Function_Calling)-1bE4iMljhppqGY1p48gQWtZvk6MfRuJRCiba1yRykGNE.md)
- [Bolum 6: Planlama (Planning)](01-Part_One/Chapter_6-Planning-18vvNESEwHnVUREzIipuaDNCnNAREGqEfy9MQYC9wb4o.md)
- [Bolum 7: Multi-Agent Is Birligi (Collaboration)](01-Part_One/Chapter_7-Multi-Agent_Collaboration-1RZ5-2fykDQKOBx01pwfKkDe0GCs5ydca7xW9Q4wqS_M.md)

### Ikinci Bolum: Ileri Sistemler

- [Bolum 8: Bellek Yonetimi (Memory Management)](02-Part_Two/Chapter_8-Memory_Management-1asVTObtzIye0I9ypAztaeeI_sr_Hx2TORE02uUuqH_c.md)
- [Bolum 9: Ogrenme ve Uyum Saglama (Learning and Adaptation)](02-Part_Two/Chapter_9-Learning_and_Adaptation-1UHTEDCmSM1nwB-iyMoHuYzVcu_B_4KkJ2ITGGUKqo8s.md)
- [Bolum 10: Model Context Protocol (MCP)](02-Part_Two/Chapter_10-Model_Context_Protocol_(MCP)-1e6XimYczKmhX9zpqEyxLFWPQgGuG0brp7Hic2sFl_qw.md)
- [Bolum 11: Hedef Belirleme ve Izleme (Goal Setting and Monitoring)](02-Part_Two/Chapter_11-Goal_Setting_and_Monitoring-10ndlCB39BWjyFRWKpcoKib4vuPD1ojD-x0-ynMaf5uw.md)

### Ucuncu Bolum: Uretim Kaygilari

- [Bolum 12: Hata Yonetimi ve Kurtarma (Exception Handling and Recovery)](03-Part_Three/Chapter_12-Exception_Handling_and_Recovery-1C07AuMur6-infwE0viCp4QtAy_wWI-uceFm6MaYHQGk.md)
- [Bolum 13: Human in the Loop](03-Part_Three/Chapter_13-Human_in_the_Loop-1ImOZcw6yeb7a-uRBMNP1VdovYfyip4IdsAcLu9yue-0.md)
- [Bolum 14: Bilgi Erisimi (Knowledge Retrieval) (RAG)](03-Part_Three/Chapter_14-Knowledge_Retrieval_(RAG)-1v96Oobio6xDOqbK8ejsXjmOc4Dp2uoLMo5_gfJgi-NE.md)

### Dorduncu Bolum: Multi-Agent Mimarileri

- [Bolum 15: Agent'lar Arasi Iletisim (Inter-Agent Communication) (A2A)](04-Part_Four/Chapter_15-Inter_Agent_Communication_(A2A)-1H6HmUYcy5kugt5gt7Kh2Zzb8C62d5pu36RsgMNDCX24.md)
- [Bolum 16: Kaynak Odakli Optimizasyon (Resource-Aware Optimization)](04-Part_Four/Chapter_16-Resource_Aware_Optimization-1nAN58l6JjqEJHk43126uh7xgdEblCpcbsNUHXgtBmJQ.md)
- [Bolum 17: Akil Yurutme Teknikleri (Reasoning Techniques)](04-Part_Four/Chapter_17-Reasoning_Techniques-1Yt1W_hLaC6ZNgJXfT4W6NrCL4TzNVdKOX50kgpHiIq4.md)
- [Bolum 18: Guardrails ve Guvenlik Kaliplari (Safety Patterns)](04-Part_Four/Chapter_18-Guardrails_Safety_Patterns-1Gpc5af_okze1kprRLohP6-81e1KwL6HggjeLvxQyIuk.md)
- [Bolum 19: Degerlendirme ve Izleme (Evaluation and Monitoring)](04-Part_Four/Chapter_19-Evaluation_and_Monitoring-1G3zOZM2ZOd0gUp5dy66FUjKMOcALh9l-JpvPxgGMm8w.md)
- [Bolum 20: Onceliklendirme (Prioritization)](04-Part_Four/Chapter_20-Prioritization-1qyXxGM2hNqW_qjXuBFxrEUeoYVO79BoW1ogKu1bfdCY.md)
- [Bolum 21: Kesif ve Kesfetme (Exploration and Discovery)](04-Part_Four/Chapter_21-Exploration_and_Discovery-1zeeMVTqjqRIli6G9MMWThhoQhvKqLOjJF2EHHUXLhdk.md)

### Ekler

- [Ek A: Gelismis Prompt Teknikleri](05-Appendix/Appendix_A-Advanced_Prompting_Techniques-1V7EKEWibOH6IhHD_PtbFZiml492-2191jDQCcTkhtTI.md)
- [Ek B: Agentic Yapay Zeka Etkilesimleri: GUI'den Gercek Dunya Ortamina](05-Appendix/Appendix_B-AI_Agentic_Interactions_From_GUI_to_Real_World_Environment-11pma_tCoC7uZ2SFKjcR5KyIq0_ooMGSoadI6f9mxG2I.md)
- [Ek C: Agentic Framework'lere Hizli Bir Bakis](05-Appendix/Appendix_C-Quick_Overview_of_Agentic_Frameworks-151rGsiEYOkXUcNDRus_N8TxxuvjoyTDViBhzt9z0Mfw.md)
- [Ek D: AgentSpace ile Agent Olusturma (yalnizca cevrimici)](05-Appendix/Appendix_D-Building_an_Agent_with_AgentSpace_(on_line_only)-1bDRJ8mKtLTeWNC-cGD0Cr8pEJQgJHNcjqz5ekloAjaE.md)
- [Ek E: CLI'da Yapay Zeka Agent'lari](05-Appendix/Appendix_E-AI_Agents_on_the_CLI-1W4znto0a8Ikajw5a4tEyRAaB2nJPJw_iFc4w4qNnjho.md)
- [Ek F: Kaputun Altinda: Agent'larin Akil Yurutme Motorlarina Yakindan Bakis](05-Appendix/Appendix_F-Under_the_Hood_An_Inside_Look_at_the_Agents_Reasoning_Engines-14q3fQ-FZmDgiughno_WLSILMWkURvUgR7mlGiFtvwd4.md)
- [Ek G: Kodlama Agent'lari](05-Appendix/Appendix_G-Coding_Agents-1tVyhgwrD4fu_D_pHUrwhNxoguRG3tLc1KObXFxrxE_s.md)

## Lisans

Bu depo [MIT Lisansi](LICENSE) altinda lisanslanmistir.

![Agentic Design Patterns](assets/Agentic_Design_Patterns.png)
