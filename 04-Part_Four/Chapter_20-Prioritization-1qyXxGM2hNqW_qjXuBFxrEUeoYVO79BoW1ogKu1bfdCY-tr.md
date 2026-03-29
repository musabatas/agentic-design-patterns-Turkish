# Bolum 20: Onceliklendirme (Prioritization)

Karmasik, dinamik ortamlarda Agent'lar siklikla cok sayida potansiyel eylem, catisan hedefler ve sinirli kaynaklarla karsilasir. Bir sonraki eylemi belirlemek icin tanimlanmis bir surec olmadan, agent'lar dusuk verimlilik, operasyonel gecikmeler veya temel hedeflere ulasma basarisizligi yasayabilir. Onceliklendirme (Prioritization) kalibi, agent'larin gorevleri, hedefleri veya eylemleri onemine, aciliyetine, bagimlilikarina ve belirlenmis kriterlere dayali olarak degerlendirmesini ve siralamsini saglayarak bu sorunu ele alir. Bu, agent'larin cabalarini en kritik gorevlere yogunlastirmasini saglayarak arttirilmis etkinlik ve hedef uyumlulugu sonucu verir.

## Onceliklendirme Kalibina Genel Bakis

Agent'lar, gorevleri, hedefleri ve alt hedefleri etkili bir sekilde yonetmek ve sonraki eylemlere rehberlik etmek icin onceliklendirme kullanir. Bu surec, birden fazla talebi ele alirken bilinçli karar vermeyi kolaylastirir; hayati veya acil faaliyetleri daha az kritik olanlarin onune koyar. Kaynaklarin kisitli, zamanin sinirli ve hedeflerin catisabilecegi gercek dunya senaryolarinda ozellikle geçerlidir.

Agent onceliklendirmesinin temel yonleri genellikle birkac unsur icerir. Birincisi, kriter tanimlama, gorev degerlendirmesi icin kurallari veya metrikleri belirler. Bunlar arasinda aciliyet (gorevin zamana duyarliligi), onem (birincil hedefe etkisi), bagimliliklar (gorevin digerlerinin on kosulu olup olmadigi), kaynak (Resource) uygunlugu (gerekli arac veya bilgilerin hazir olup olmadigi), maliyet/fayda analizi (caba ile beklenen sonuc karsilastirmasi) ve kisisellestilmis agent'lar icin kullanici tercihleri bulunabilir. Ikincisi, gorev degerlendirmesi, her potansiyel gorevin bu tanimlanmis kriterlere gore degerlendirilmesini icerir; basit kurallardan karmasik puanlama veya LLM'ler tarafindan akil yurutmeye (Reasoning) kadar uzanan yontemler kullanir. Ucuncusu, zamanlama veya secim mantigi, degerlendirmelere dayali olarak optimal sonraki eylemi veya gorev sirasini secen algoritmadir; potansiyel olarak bir kuyruk veya gelismis bir planlama bileseni kullanir. Son olarak, dinamik yeniden onceliklendirme, yeni bir kritik olayin ortaya cikmasi veya bir son tarihin yaklmasi gibi kosullar degistikce agent'in oncelikleri degistirmesine olanak tanir ve agent uyum yetenegini ve yanitlanabilirligini saglar.

Onceliklendirme cesitli düzeylerde gerceklesebilir: kapsayici bir hedef secme (ust duzey hedef onceliklendirmesi), bir plan icindeki adimlari siralama (alt gorev onceliklendirmesi) veya mevcut secenekler arasindandaki bir sonraki ani eylemi secme (eylem secimi). Etkili onceliklendirme, agent'larin ozellikle karmasik, cok hedefli ortamlarda daha akilli, verimli ve saglam davranis sergilemesini saglar. Bu, yoneticilerin tum uyelerin girdilerini dikkate alarak gorevleri onceliklendirdigi insan takım organizasyonunu yansitir.

## Pratik Uygulamalar ve Kullanim Alanlari

Cesitli gercek dunya uygulamalarinda yapay zeka agent'lari, zamaninda ve etkili kararlar almak icin onceliklendirmenin sofistike kullanimini gostermektedir.

* **Otomatik Musteri Destegi:** Agent'lar, sistem kesintisi raporlari gibi acil istekleri, sifre sifirlama gibi rutin konularin onune koyar. Ayrica yuksek degerli musterilere oncelikli muamele yapabilir.
* **Bulut Bilisim:** Yapay zeka, yoğun talep donemlerinde kritik uygulamalara tahsisi onceliklendirerek kaynaklari yonetir ve zamanlar; maliyetleri optimize etmek icin daha az acil toplu isleri yogun olmayan saatlere relegates.
* **Otonom Surus Sistemleri:** Guvenlik ve verimliligi saglamak icin eylemleri surekli olarak onceliklendirir. Ornegin, bir carpismadan kacinmak icin frenleme, serit disiplinini koruma veya yakit verimliligini optimize etmeden once gelir.
* **Finansal Ticaret:** Bot'lar, piyasa kosullari, risk toleransi, kar marjlari ve gercek zamanli haberler gibi faktorleri analiz ederek islemleri onceliklendirir; yuksek oncelikli islemlerin hızla yurutulmesini saglar.
* **Proje Yonetimi:** Yapay zeka agent'lari, son tarihler, bagimliliklar, takim musaitligi ve stratejik oneme dayali olarak bir proje panosundaki gorevleri onceliklendirir.
* **Siber Guvenlik:** Ag trafigini izleyen agent'lar, tehdit ciddiiyetini, potansiyel etkiyi ve varlik kritiligini degerlendirerek uyarilari onceliklendirir ve en tehlikeli tehditlere ani yanitlar saglar.
* **Kisisel Asistan Yapay Zekalari:** Gunluk yasami yonetmek icin onceliklendirme kullanir; takvim olaylarini, hatirlaticiları ve bildirimleri kullanici tarafindan tanimlanan oneme, yaklasan son tarihlere ve mevcut baglama gore duzenler.

Bu ornekler topluca, onceliklendirme yeteneginin genis bir durumlar yelpazesinde yapay zeka agent'larinin gelistirilmis performans ve karar verme yetenekleri icin ne kadar temel oldugunu göstermektedir.

## Uygulamali Kod Ornegi

Asagidaki, LangChain kullanarak bir Proje Yoneticisi yapay zeka agent'inin gelistirilmesini gostermektedir. Bu agent, gorevlerin olusturulmasini, onceliklendirilmesini ve ekip uyelerine atanmasini kolaylastirir ve otomatik proje yonetimi icin buyuk dil modellerinin ozel araclarla uygulamasini gosterir.

```python
import os
import asyncio
from typing import List, Optional, Dict, Type

from dotenv import load_dotenv
from pydantic import BaseModel, Field
from langchain_core.prompts import ChatPromptTemplate
from langchain_core.tools import Tool
from langchain_openai import ChatOpenAI
from langchain.agents import AgentExecutor, create_react_agent
from langchain.memory import ConversationBufferMemory


# --- 0. Configuration and Setup ---
# Loads the OPENAI_API_KEY from the .env file.
load_dotenv()

# The ChatOpenAI client automatically picks up the API key from the environment.
llm = ChatOpenAI(temperature=0.5, model="gpt-4o-mini")


# --- 1. Task Management System ---
class Task(BaseModel):
    """Represents a single task in the system."""
    id: str
    description: str
    priority: Optional[str] = None  # P0, P1, P2
    assigned_to: Optional[str] = None  # Name of the worker


class SuperSimpleTaskManager:
    """An efficient and robust in-memory task manager."""

    def __init__(self):
        # Use a dictionary for O(1) lookups, updates, and deletions.
        self.tasks: Dict[str, Task] = {}
        self.next_task_id = 1

    def create_task(self, description: str) -> Task:
        """Creates and stores a new task."""
        task_id = f"TASK-{self.next_task_id:03d}"
        new_task = Task(id=task_id, description=description)
        self.tasks[task_id] = new_task
        self.next_task_id += 1
        print(f"DEBUG: Task created - {task_id}: {description}")
        return new_task

    def update_task(self, task_id: str, **kwargs) -> Optional[Task]:
        """Safely updates a task using Pydantic's model_copy."""
        task = self.tasks.get(task_id)
        if task:
            # Use model_copy for type-safe updates.
            update_data = {k: v for k, v in kwargs.items() if v is not None}
            updated_task = task.model_copy(update=update_data)
            self.tasks[task_id] = updated_task
            print(f"DEBUG: Task {task_id} updated with {update_data}")
            return updated_task

        print(f"DEBUG: Task {task_id} not found for update.")
        return None

    def list_all_tasks(self) -> str:
        """Lists all tasks currently in the system."""
        if not self.tasks:
            return "No tasks in the system."

        task_strings = []
        for task in self.tasks.values():
            task_strings.append(
                f"ID: {task.id}, Desc: '{task.description}', "
                f"Priority: {task.priority or 'N/A'}, "
                f"Assigned To: {task.assigned_to or 'N/A'}"
            )
        return "Current Tasks:\n" + "\n".join(task_strings)


task_manager = SuperSimpleTaskManager()


# --- 2. Tools for the Project Manager Agent ---
# Use Pydantic models for tool arguments for better validation and clarity.
class CreateTaskArgs(BaseModel):
    description: str = Field(description="A detailed description of the task.")


class PriorityArgs(BaseModel):
    task_id: str = Field(description="The ID of the task to update, e.g., 'TASK-001'.")
    priority: str = Field(description="The priority to set. Must be one of: 'P0', 'P1', 'P2'.")


class AssignWorkerArgs(BaseModel):
    task_id: str = Field(description="The ID of the task to update, e.g., 'TASK-001'.")
    worker_name: str = Field(description="The name of the worker to assign the task to.")


def create_new_task_tool(description: str) -> str:
    """Creates a new project task with the given description."""
    task = task_manager.create_task(description)
    return f"Created task {task.id}: '{task.description}'."


def assign_priority_to_task_tool(task_id: str, priority: str) -> str:
    """Assigns a priority (P0, P1, P2) to a given task ID."""
    if priority not in ["P0", "P1", "P2"]:
        return "Invalid priority. Must be P0, P1, or P2."
    task = task_manager.update_task(task_id, priority=priority)
    return f"Assigned priority {priority} to task {task.id}." if task else f"Task {task_id} not found."


def assign_task_to_worker_tool(task_id: str, worker_name: str) -> str:
    """Assigns a task to a specific worker."""
    task = task_manager.update_task(task_id, assigned_to=worker_name)
    return f"Assigned task {task.id} to {worker_name}." if task else f"Task {task_id} not found."


# All tools the PM agent can use
pm_tools = [
    Tool(
        name="create_new_task",
        func=create_new_task_tool,
        description="Use this first to create a new task and get its ID.",
        args_schema=CreateTaskArgs
    ),
    Tool(
        name="assign_priority_to_task",
        func=assign_priority_to_task_tool,
        description="Use this to assign a priority to a task after it has been created.",
        args_schema=PriorityArgs
    ),
    Tool(
        name="assign_task_to_worker",
        func=assign_task_to_worker_tool,
        description="Use this to assign a task to a specific worker after it has been created.",
        args_schema=AssignWorkerArgs
    ),
    Tool(
        name="list_all_tasks",
        func=task_manager.list_all_tasks,
        description="Use this to list all current tasks and their status."
    ),
]


# --- 3. Project Manager Agent Definition ---
pm_prompt_template = ChatPromptTemplate.from_messages([
    ("system", """You are a focused Project Manager LLM agent. Your goal is to manage project tasks efficiently.
      When you receive a new task request, follow these steps:
    1.  First, create the task with the given description using the `create_new_task` tool. You must do this first to get a `task_id`.
    2.  Next, analyze the user's request to see if a priority or an assignee is mentioned.
        - If a priority is mentioned (e.g., "urgent", "ASAP", "critical"), map it to P0. Use `assign_priority_to_task`.
        - If a worker is mentioned, use `assign_task_to_worker`.
    3.  If any information (priority, assignee) is missing, you must make a reasonable default assignment (e.g., assign P1 priority and assign to 'Worker A').
    4.  Once the task is fully processed, use `list_all_tasks` to show the final state.

    Available workers: 'Worker A', 'Worker B', 'Review Team'
    Priority levels: P0 (highest), P1 (medium), P2 (lowest)
    """),
    ("placeholder", "{chat_history}"),
    ("human", "{input}"),
    ("placeholder", "{agent_scratchpad}")
])

# Create the agent executor
pm_agent = create_react_agent(llm, pm_tools, pm_prompt_template)
pm_agent_executor = AgentExecutor(
    agent=pm_agent,
    tools=pm_tools,
    verbose=True,
    handle_parsing_errors=True,
    memory=ConversationBufferMemory(memory_key="chat_history", return_messages=True)
)


# --- 4. Simple Interaction Flow ---
async def run_simulation():
    print("--- Project Manager Simulation ---")

    # Scenario 1: Handle a new, urgent feature request
    print("\n[User Request] I need a new login system implemented ASAP. It should be assigned to Worker B.")
    await pm_agent_executor.ainvoke({"input": "Create a task to implement a new login system. It's urgent and should be assigned to Worker B."})

    print("\n" + "-" * 60 + "\n")

    # Scenario 2: Handle a less urgent content update with fewer details
    print("[User Request] We need to review the marketing website content.")
    await pm_agent_executor.ainvoke({"input": "Manage a new task: Review marketing website content."})

    print("\n--- Simulation Complete ---")


# Run the simulation
if __name__ == "__main__":
    asyncio.run(run_simulation())
```

Bu kod, buyuk bir dil modeli tarafindan desteklenen bir proje yoneticisi agent'ini simule etmek icin Python ve LangChain kullanarak basit bir gorev yonetim sistemi uygular.

Sistem, gorevleri bellek icerisinde verimli bir sekilde yonetmek icin hizli veri alma amaciyla sozluk yapisi kullanan bir SuperSimpleTaskManager sinifi kullanir. Her gorev, benzersiz bir tanimlayici, aciklayici bir metin, istege bagli bir oncelik seviyesi (P0, P1, P2) ve istege bagli bir atanan kisyi gosterimi gibi ozellikleri kapsayan bir Task Pydantic modeli ile temsil edilir. Bellek kullanimi gorev turune, calisan sayisina ve diger katkida bulunan faktorlere gore degisir. Gorev yoneticisi, gorev olusturma, gorev degistirme ve tum gorevlerin alinmasi icin yontemler saglar.

Agent, gorev yoneticisi ile tanimlanmis bir Araclar seti araciligiyla etkilesim kurar. Bu araclar yeni gorevlerin olusturulmasini, gorevlere oncelik atanmasini, gorevlerin personele tahsisini ve tum gorevlerin listelenmesini kolaylastirir. Her arac, SuperSimpleTaskManager ornegi ile etkilesimi mumkun kilmak icin kapsullenmistir. Pydantic modelleri, veri dogrulamasini saglayarak araclar icin gerekli argumanlari belirlemek amaciyla kullanilir.

Bir AgentExecutor, dil modeli, arac seti ve baglamsal surekliligi korumak icin bir konusma bellek bileseni ile yapilandirilir. Agent'in proje yonetimi rolundeki davranisini yonlendirmek icin belirli bir ChatPromptTemplate tanimlannir. Prompt, agent'a bir gorev olusturarak baslamasini, ardindan belirtildigi sekilde oncelik ve personel atamasini ve kapsamli bir gorev listesiyle bitirmesini talimat verir. P1 onceligi ve 'Worker A' gibi varsayilan atamalar, bilgi eksik oldugu durumlar icin prompt icinde belirlenmistir.

Kod, agent'in operasyonel kapasitesini gostermek icin asenkron yapida bir simulasyon fonksiyonu (`run_simulation`) icerir. Simulasyon iki farkli senaryo yurutur: belirlenmis personelle acil bir gorev yonetimi ve minimum girdiyle daha az acil bir gorev yonetimi. AgentExecutor icinde verbose=True etkinlestirilmesi nedeniyle agent'in eylemleri ve mantiksal surecleri konsola ciktilanir.

# Bir Bakista

**Ne:** Karmasik ortamlarda calisan yapay zeka agent'lari, cok sayida potansiyel eylem, catisan hedefler ve sinirli kaynaklarla karsilasir. Bir sonraki adimi belirlemek icin net bir yontem olmadan, bu agent'lar verimsiz ve etkisiz hale gelme riski tasir. Bu, onemli operasyonel gecikmelere veya birincil hedeflerin tamamen basarisiz olmasina yol acabilir. Temel zorluk, agent'in amacli ve mantikli bir sekilde hareket etmesini saglamak icin bu ezici secenek sayisini yonetmektir.

**Neden:** Onceliklendirme (Prioritization) kalibi, agent'larin gorevleri ve hedefleri siralammasini saglayarak bu sorun icin standartlastirilmis bir cozum sunar. Bu, aciliyet, onem, bagimliliklar ve kaynak maliyeti gibi net kriterlerin olusturulmasiyla basarilir. Agent daha sonra en kritik ve zamaninda eylem yolunu belirlemek icin her potansiyel eylemi bu kriterlere gore degerlendirir. Bu Agentic yetenek, sistemin degisen koullara dinamik olarak uyum saglamasina ve kisitli kaynaklari etkili bir sekilde yonetmesine olanak tanir. En yuksek oncelikli maddelere odaklanarak, agent'in davranisi daha akilli, saglam ve stratejik hedefleriyle uyumlu hale gelir.

**Temel Kural:** Onceliklendirme kalibini, bir Agentic sistemin dinamik bir ortamda etkili bir sekilde calisabilmesi icin kaynak kisitlamalari altinda birden fazla, genellikle catisan gorev veya hedefi ozerk olarak yonetmesi gerektiginde kullanin.

**Gorsel Ozet:**

**![Prioritization Design Pattern](../assets/Prioritization_Design_Pattern.png )

Sekil 1: Onceliklendirme Tasarim Kalibi

# Onemli Cikarimlar

* Onceliklendirme, yapay zeka agent'larinin karmasik, cok yonlu ortamlarda etkili bir sekilde islemesini saglar.
* Agent'lar, gorevleri degerlendirmek ve siralamak icin aciliyet, onem ve bagimliliklar gibi belirlenimis kriterleri kullanir.
* Dinamik yeniden onceliklendirme, agent'larin gercek zamanli degisikliklere yanit olarak operasyonel odaklarini ayarlamalaarina olanak tanir.
* Onceliklendirme, kapsayici stratejik hedefleri ve ani taktiksel kararlari kapsayan cesitli duzeylerde gerceklesir.
* Etkili onceliklendirme, yapay zeka agent'larinin arttirilmis verimliligi ve gelistirilmis operasyonel saglamligi ile sonuçlanir.

# Sonuclar

Sonuc olarak, onceliklendirme kalibi etkili agentic yapay zekanin temel tasidir ve sistemleri dinamik ortamlarin karmasikliklarinda amac ve zeka ile gezinme yetenegine kavusturur. Bir agent'in cok sayida catisan gorev ve hedefi ozerk olarak degerlendirmesine ve sinirli kaynaklarini nereye odaklayacagi konusunda gerekce tabanli kararlar almasina olanak tanir. Bu agentic yetenek, basit gorev yurutmenin otesine gecerek sistemin proaktif, stratejik bir karar verici olarak hareket etmesini saglar. Aciliyet, onem ve bagimliliklar gibi kriterleri tarttarak, agent sofistike, insan benzeri bir akil yurutme sureci sergiler.

Bu agentic davranisinin onemli bir ozelligi, agent'a kosullar degistikce odagini gercek zamanli olarak uyarlama ozerkligini veren dinamik yeniden onceliklendirmedir. Kod orneginde gosterildigi gibi, agent belirsiz istekleri yorumlar, uygun araclari ozerk olarak secer ve kullanir ve hedeflerini yerine getirmek icin eylemlerini mantiksal olarak siralar. Is akisini kendini yonetme yetenegi, gercek bir agentic sistemi basit bir otomatik betikten ayiran seydir. Nihayetinde, onceliklendirmede ustalik, herhangi bir karmasik, gercek dunya senaryosunda etkili ve guvenilir bir sekilde calisabilen saglam ve akilli agent'lar olusturmak icin esastir.

# Referanslar

1. Examining the Security of Artificial Intelligence in Project Management: A Case Study of AI-driven Project Scheduling and Resource Allocation in Information Systems Projects ; [https://www.irejournals.com/paper-details/1706160](https://www.irejournals.com/paper-details/1706160)
2. AI-Driven Decision Support Systems in Agile Software Project Management: Enhancing Risk Mitigation and Resource Allocation; [https://www.mdpi.com/2079-8954/13/3/208](https://www.mdpi.com/2079-8954/13/3/208)
