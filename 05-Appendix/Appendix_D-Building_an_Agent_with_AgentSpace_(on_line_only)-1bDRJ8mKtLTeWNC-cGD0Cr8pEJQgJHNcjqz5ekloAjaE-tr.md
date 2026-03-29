# Ek D - AgentSpace ile Agent Olusturma

## Genel Bakis

AgentSpace, yapay zekayi gunluk is akislarina entegre ederek "agent odakli kurumsal" yapiyi kolaylastirmak icin tasarlanmis bir platformdur. Temelinde, belgeler, e-postalar ve veritabanlari dahil olmak uzere bir kurumun tum dijital ayak izi uzerinde birlesik bir arama yetenegi saglar. Bu sistem, bu cesitli kaynaklardan gelen bilgileri kavramak ve sentezlemek icin Google'in Gemini'si gibi gelismis yapay zeka modellerini kullanir.

Platform, karmasik gorevleri yerine getirebilen ve surecleri otomatiklestirebilen uzmanlasmis yapay zeka "agent'larinin" olusturulmasini ve dagitilmasini saglar. Bu agent'lar yalnizca sohbet robotlari degildir; otonom olarak akil yurutebilir, plan yapabilir ve cok adimli eylemler yurutebilir. Ornegin, bir agent bir konuyu arastirabilir, alintili bir rapor derleyebilir ve hatta bir sesli ozet olusturabilir.

Bunu basarmak icin AgentSpace, kisiler, belgeler ve veriler arasindaki iliskileri haritalayan bir kurumsal bilgi grafi olusturur. Bu, yapay zekanin baglami anlamasina ve daha ilgili ve kisisellestirilmis sonuclar sunmasina olanak tanir. Platform ayrica derin teknik uzmanlik gerektirmeden ozel agent'lar olusturmak icin Agent Designer adinda kodsuz bir arayuz icerir.

Dahasi, AgentSpace farkli yapay zeka agent'larinin Agent2Agent (A2A) Protokolu olarak bilinen acik bir protokol araciliyla iletisim (Communication) kurabilecegi ve is birligi (Collaboration) yapabilecegi coklu agent sistemini destekler. Bu birlikte calisabilirlik daha karmasik ve orkestre edilmis is akislarina olanak tanir. Guvenlik (Safety), rol tabanli erisim kontrolleri ve veri sifreleme gibi ozelliklerle temel bir bilesen olarak yer alir ve hassas kurumsal bilgileri korur. Sonuc olarak, AgentSpace akilli, otonom sistemleri dogrudan bir kurumun operasyonel dokusuna goimerek uretkenliigi ve karar vermeyi gelistirmeyi amaclar.

## AgentSpace Kullanici Arayuzu ile Agent Olusturma

Sekil 1, Google Cloud Console'dan AI Applications'i secerek AgentSpace'e nasil erisilecegiini gostermektedir.

![GCP: Access AgentSpace](../assets/GCP_Access_AgentSpace.png)

Sekil 1: AgentSpace'e erismek icin Google Cloud Console'un nasil kullanilacagi

Agent'iniz Calendar, Google Mail, Workaday, Jira, Outlook ve Service Now dahil olmak uzere cesitli hizmetlere baglanabilir (bkz. Sekil 2).

![GCP: Integrate with diverse services](../assets/GCP_Integrate_with_diverse_services.png)

Sekil 2: Google ve ucuncu taraf platformlari dahil olmak uzere cesitli hizmetlerle entegrasyon.

Agent daha sonra Sekil 3'te gosterildigi gibi Google tarafindan saglanan onceden hazirlanmis prompt galersiniden secilen kendi prompt'unu kullanabilir.

![GCP: Googles Gallery of Pre-Assembled Prompts](../assets/GCP_Googles_Gallery_of_Pre_Assembled_Prompts.png)

Sekil 3: Google'in Onceden Hazirlanmis Prompt Galerisi

Alternatif olarak Sekil 4'teki gibi kendi prompt'unuzu olusturabilirsiniz ve bu prompt daha sonra agent'iniz tarafindan kullanilacaktir.

![GCP: Customizing the Agent's Prompt](../assets/GCP_Customizing_the_Agents_Prompt.png)

Sekil 4: Agent Prompt'unu Ozellestirme

AgentSpace, kendi verilerinizi depolamak icin veri depolariyla entegrasyon, Google Knowledge Graph veya ozel Knowledge Graph ile entegrasyon, agent'inizi Web'e acmak icin Web arayuzu ve kullanimi izlemek (Monitoring) icin Analytics ve daha fazlasi gibi bir dizi gelismis ozellik sunar (bkz. Sekil 5).

![GCP: AgentSpace Advanced Capabilities](../assets/GCP_AgentSpace_Advanced_Capabilities.png)

Sekil 5: AgentSpace gelismis yetenekleri

Tamamlandiktan sonra, AgentSpace sohbet arayuzune (Sekil 6) erisilebilir olacaktir.

![GCP: AgentSpace User Interface for initiating a chat with your Agent](../assets/GCP_AgentSpace_User_Interface_for_initiating_a_chat_with_your_Agent.png)

Sekil 6: Agent'inizle sohbet baslatmak icin AgentSpace Kullanici Arayuzu.

## Sonuc

Sonuc olarak, AgentSpace bir kurumun mevcut dijital altyapisi icinde yapay zeka agent'lari gelistirmek ve dagitmak icin islevsel bir cerceve saglar. Sistemin mimarisi, otonom akil yurutme ve kurumsal bilgi grafi haritalama gibi karmasik arka plan sureclerini agent insasi icin bir grafik kullanici arayuzune baglar. Bu arayuz araciliyla kullanicilar, cesitli veri hizmetlerini entegre ederek ve operasyonel parametrelerini prompt'lar araciliyla tanimlayarak agent'lari yapilandirabilir ve sonuc olarak ozellestiirilmis, baglam farkindaliigina sahip otomatik sistemler elde edebilir.

Bu yaklasim, altta yatan teknik karmasikligi soyutlayarak derin programlama uzmanligi gerektirmeden uzmanlasmis coklu agent sistemlerinin olusturulmasini mumkun kilar. Birincil amac, otomatik analitik ve operasyonel yetenekleri dogrudan is akislarina gommeek, boylece surec verimliliigini artirmak ve veri odakli analizi gelistirmektir. Pratik egitim icin, Google Cloud Skills Boost uzerindeki "Build a Gen AI Agent with Agentspace" laboratuvari gibi, beceri edinimi icin yapilandirilmis bir ortam saglayan uygulamali ogrenme modulleri mevcuttur.

## Kaynaklar

1. Create a no-code agent with Agent Designer, [https://cloud.google.com/agentspace/agentspace-enterprise/docs/agent-designer](https://cloud.google.com/agentspace/agentspace-enterprise/docs/agent-designer)
2. Google Cloud Skills Boost, [https://www.cloudskillsboost.google/](https://www.cloudskillsboost.google/)
