<span data-ttu-id="f8880-101">Vi började genom att tala om hur du kan kontrollera att du har kontroll över din förbrukning, samt hur du optimerar den.</span><span class="sxs-lookup"><span data-stu-id="f8880-101">We started out by talking about how to ensure you are in control of your consumption as well as optimize it.</span></span> <span data-ttu-id="f8880-102">Här följer några av de viktigaste aspekterna som beskrevs:</span><span class="sxs-lookup"><span data-stu-id="f8880-102">Here are some of the key aspects that were covered:</span></span>

- <span data-ttu-id="f8880-103">Spåra molnutgifter: Vikten av att samla in och granska molnets förbrukningsdata för att förstå molnutgifterna.</span><span class="sxs-lookup"><span data-stu-id="f8880-103">Tracking cloud spend: the importance of gathering and looking at cloud consumption data to understand your cloud spend.</span></span>
- <span data-ttu-id="f8880-104">Ordna för att optimera: Relevansen för en prenumeration och resursgruppens hierarki, samt hur taggar kan ge fler dimensioner.</span><span class="sxs-lookup"><span data-stu-id="f8880-104">Organizing to optimize: the relevance of a subscription and resource group hierarchy and how tags can further help provide various dimensions.</span></span>
- <span data-ttu-id="f8880-105">Det finns flera alternativ för att optimera kostnaderna för IaaS: Rätt storlek, minska antalet körningstimmar och beräkna kostnadsrabatter.</span><span class="sxs-lookup"><span data-stu-id="f8880-105">There are several possibilities to optimize IaaS costs: right-sizing, reducing runtime hours, and compute cost discounts.</span></span>
- <span data-ttu-id="f8880-106">Några exempel visades på hur man optimerar kostnaderna för PaaS: Att använda elastiska pooler i Azure SQL Database för att optimera kostnaderna för lagringsnivåerna i Azure SQL eller Azure Blob Storage och optimera Azure Storage-kostnaderna.</span><span class="sxs-lookup"><span data-stu-id="f8880-106">Some examples were shown to optimize PaaS costs: for example, using Azure SQL Database elastics pools to optimize Azure SQL costs or Azure Blob storage tiering to optimize Azure Storage costs.</span></span>

<span data-ttu-id="f8880-107">Därefter gick vi igenom den åtgärdsinformation som du kan få genom att förstå och implementera övervakning och analys.</span><span class="sxs-lookup"><span data-stu-id="f8880-107">Next, we covered the operational insights you could gain from understanding and implementing monitoring and analytics.</span></span> <span data-ttu-id="f8880-108">Vi såg att det finns olika nivåer där vi kan tillämpa övervakning.</span><span class="sxs-lookup"><span data-stu-id="f8880-108">We determined that there are various levels on which we can apply monitoring.</span></span>

- <span data-ttu-id="f8880-109">Övervakning innebär att samla in och analysera data för att avgöra prestanda, hälsotillstånd och tillgänglighet för de företagsprogram och resurser som man är beroende av.</span><span class="sxs-lookup"><span data-stu-id="f8880-109">Monitoring is the act of collecting and analyzing data to determine the performance, health, and availability of your business application and the resources that it depends on.</span></span>
- <span data-ttu-id="f8880-110">Det finns olika djup för övervakningen.</span><span class="sxs-lookup"><span data-stu-id="f8880-110">There are various depths of monitoring.</span></span> <span data-ttu-id="f8880-111">Kärnövervakningen omfattar aspekter nära Azure-plattformen, till exempel aktivitetsloggning, molntjänsthälsa samt mått och diagnostik.</span><span class="sxs-lookup"><span data-stu-id="f8880-111">Core monitoring covers aspects close to the Azure platform such as activity logging, cloud services health, and metrics and diagnostics.</span></span>
- <span data-ttu-id="f8880-112">Med övervakning av den djupa infrastrukturen kan du samla in information som är utöver vad Azure-infrastrukturen kan ge.</span><span class="sxs-lookup"><span data-stu-id="f8880-112">Deep infrastructure monitoring allows you to gather information besides what the Azure fabric can provide.</span></span> <span data-ttu-id="f8880-113">Vi kan övervaka på nätverks- eller operativsystemnivå för vanliga IaaS-arbetsbelastningar.</span><span class="sxs-lookup"><span data-stu-id="f8880-113">For typical IaaS workloads, we can monitor at the network or operating system level.</span></span>
- <span data-ttu-id="f8880-114">Djupgående programövervakning tar det ännu längre genom att samla in information om mått och diagnostik nära programmet. Detta innebär att du kan identifiera prestandaproblem, användningstrender och information om övergripande tillgänglighet.</span><span class="sxs-lookup"><span data-stu-id="f8880-114">Deep application monitoring takes it even further by gathering metrics and diagnostics information close to the application, allowing you to identity performance issues, usage trends, and overall availability information.</span></span>

<span data-ttu-id="f8880-115">Vi avslutade genom att visa att det finns olika sätt att automatisera uppgifter på när du vill förbättra dina operativa funktioner.</span><span class="sxs-lookup"><span data-stu-id="f8880-115">We wrapped up by discussing that there are various ways to automate tasks to improve your operational capabilities.</span></span> <span data-ttu-id="f8880-116">Här följer några av de viktiga saker som vi har gått igenom:</span><span class="sxs-lookup"><span data-stu-id="f8880-116">Here are some of the key things we covered:</span></span>

- <span data-ttu-id="f8880-117">**Att automatisera distributionen av resurser kan göras på två olika sätt:** imperativt (med skript) eller deklarativt (med mallar).</span><span class="sxs-lookup"><span data-stu-id="f8880-117">**Automating the deployment of resources can take two different approaches:** imperative (scripting) or declarative (templates).</span></span>
- <span data-ttu-id="f8880-118">**När den virtuella datorn har distribuerats ska vi se hur du anpassar den.**</span><span class="sxs-lookup"><span data-stu-id="f8880-118">**After the VM is deployed, we can look at how to customize it.**</span></span> <span data-ttu-id="f8880-119">Antingen använder vi anpassade avbildningar och slipper därmed anpassningen.</span><span class="sxs-lookup"><span data-stu-id="f8880-119">Either by using custom images and thus remove the need for customization in the first place.</span></span> <span data-ttu-id="f8880-120">Eller så kör vi ett skript efter distributionen.</span><span class="sxs-lookup"><span data-stu-id="f8880-120">Or by running a script post deployment.</span></span>
- <span data-ttu-id="f8880-121">**Automatisering av uppgifter i Azure:** Med hjälp av Azure Automation kan du installera uppdateringar eller stänga av virtuella datorer enligt ett schema.</span><span class="sxs-lookup"><span data-stu-id="f8880-121">**Automation of Azure tasks:** Azure Automation can help with installing updates or shutting down virtual machines on a schedule.</span></span>
- <span data-ttu-id="f8880-122">**Labbmiljöer för automatisering:** Azure DevTest Labs tar automatisering ett steg längre genom att tillhandahålla ett lättanvänt gränssnitt där du kan använda olika automatiseringsfunktioner, som t.ex. avbildningar eller avstängning av virtuella datorer, utan att behöva bekymra dig om den faktiska implementeringen av dessa åtgärder.</span><span class="sxs-lookup"><span data-stu-id="f8880-122">**Automation lab environments:** Azure DevTest Labs takes automation one step further by providing an easy-to-use interface that allows you to use various automation capabilities like images or shutting down VMs without having to worry about the actual implementation of those tasks.</span></span>