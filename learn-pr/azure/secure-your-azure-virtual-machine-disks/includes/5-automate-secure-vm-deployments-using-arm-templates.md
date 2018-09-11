<span data-ttu-id="8cfb4-101">Tänk dig att ditt företag distribuerar flera servrar som en del av övergången till molnet.</span><span class="sxs-lookup"><span data-stu-id="8cfb4-101">Suppose your company is deploying several servers as part of their cloud transition.</span></span> <span data-ttu-id="8cfb4-102">Virtuella datordiskar måste krypteras under distributionen så att de inte är sårbara under något skede.</span><span class="sxs-lookup"><span data-stu-id="8cfb4-102">VM disks must be encrypted during the deployment, so there's no time when the disks are vulnerable.</span></span> <span data-ttu-id="8cfb4-103">Du vill automatisera den här processen och måste ändra Azure Resource Manager (ARM)-mallarna, så kryptering automatiskt aktiveras.</span><span class="sxs-lookup"><span data-stu-id="8cfb4-103">You want to automate this process and have to modify the Azure Resource Manager (ARM) templates to automatically enable encryption.</span></span>

<span data-ttu-id="8cfb4-104">Här tar vi en titt på hur du använder en ARM-mall för att automatiskt aktivera kryptering för nya virtuella Windows-datorer.</span><span class="sxs-lookup"><span data-stu-id="8cfb4-104">Here, we'll look at how to use an ARM template to automatically enable encryption for new Windows VMs.</span></span>

## <a name="what-are-arm-templates"></a><span data-ttu-id="8cfb4-105">Vad är ARM-mallar?</span><span class="sxs-lookup"><span data-stu-id="8cfb4-105">What are ARM templates?</span></span>

<span data-ttu-id="8cfb4-106">ARM-mallar är JSON-filer som används för att definiera en resurs att distribuera till Azure, till exempel en virtuell dator.</span><span class="sxs-lookup"><span data-stu-id="8cfb4-106">ARM templates are JSON files used to define a resource to deploy to Azure, such as a virtual machine.</span></span> <span data-ttu-id="8cfb4-107">Du kan skriva dem från början, och för vissa Azure-resurser som virtuella datorer kan du generera dem genom att använda Azure-portalen.</span><span class="sxs-lookup"><span data-stu-id="8cfb4-107">You can write them from scratch, and for some Azure resources, including VMs, you can use the Azure portal to generate them.</span></span> <span data-ttu-id="8cfb4-108">Du måste fylla i all nödvändig information för en manuell distribution av virtuella datorer, men i stället för att distribuera den virtuella datorn till Azure sparar du mallen.</span><span class="sxs-lookup"><span data-stu-id="8cfb4-108">You'll need to complete the required information for a manual VM deployment, but instead of deploying the VM to Azure, you save the template.</span></span>

<span data-ttu-id="8cfb4-109">Det finns exempelmallar i GitHub.</span><span class="sxs-lookup"><span data-stu-id="8cfb4-109">There are example templates available in GitHub.</span></span>

## <a name="using-github-templates"></a><span data-ttu-id="8cfb4-110">Använda GitHub-mallar</span><span class="sxs-lookup"><span data-stu-id="8cfb4-110">Using GitHub templates</span></span>

<span data-ttu-id="8cfb4-111">GitHub har en mall för att aktivera kryptering med namnet **Enable encryption on a running Windows VM ARM** (Aktivera kryptering på en Windows VM ARM som körs).</span><span class="sxs-lookup"><span data-stu-id="8cfb4-111">GitHub has template for enabling encryption called the **Enable encryption on a running Windows VM ARM**.</span></span> <span data-ttu-id="8cfb4-112">Du hittar den i lagringsplatsen för [Azure-snabbstartsmallar](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="8cfb4-112">You can find it in the [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates) repository.</span></span> <span data-ttu-id="8cfb4-113">På sidan readme (viktigt) för mallen finns knappen Deploy to Azure (Distribuera till Azure) som öppnar mallen i Azure-portalen.</span><span class="sxs-lookup"><span data-stu-id="8cfb4-113">The readme page for the template provides a Deploy to Azure button that then opens the template in the Azure portal.</span></span>

<span data-ttu-id="8cfb4-114">Med hjälp av mallen kan du distribuera en virtuell Windows Server-dator som har kryptering färdigt aktiverat.</span><span class="sxs-lookup"><span data-stu-id="8cfb4-114">The template enables you to deploy a Windows Server VM, with encryption pre-enabled.</span></span> <span data-ttu-id="8cfb4-115">Innan du använder mallen måste du se till att alla förhandskrav för kryptering är uppfyllda.</span><span class="sxs-lookup"><span data-stu-id="8cfb4-115">Before using the template, you must make sure that all of the encryption pre-requisites are in place.</span></span> <span data-ttu-id="8cfb4-116">Du behöver även konfigurationsinformationen från skriptet om förhandskrav, till exempel AAD-klient-ID och AAD-klienthemlighet.</span><span class="sxs-lookup"><span data-stu-id="8cfb4-116">You'll also need the configuration information that is provided by the pre-requisites script, such as AAD Client ID and AAD Client Secret.</span></span>

<span data-ttu-id="8cfb4-117">Du skapar en ny virtuell dator genom att ange den nödvändiga informationen i mallen.</span><span class="sxs-lookup"><span data-stu-id="8cfb4-117">You create a new VM by entering the required information on the template.</span></span> <span data-ttu-id="8cfb4-118">Du startar sedan distributionen genom att klicka på **Köp** (kostnaden är vanligtvis den normala beräkningsavgiften för Azure).</span><span class="sxs-lookup"><span data-stu-id="8cfb4-118">You then initiate deployment by clicking **Purchase** (the cost is typically the normal Azure compute charge).</span></span>

## <a name="deploy-an-encrypted-vm-by-using-a-template"></a><span data-ttu-id="8cfb4-119">Distribuera en krypterad virtuell dator med hjälp av en mall</span><span class="sxs-lookup"><span data-stu-id="8cfb4-119">Deploy an encrypted VM by using a template</span></span>

<span data-ttu-id="8cfb4-120">De huvudsakliga stegen för att distribuera en krypterad virtuell dator med hjälp av en mall är:</span><span class="sxs-lookup"><span data-stu-id="8cfb4-120">The main steps involved in deploying an encrypted VM using a template are:</span></span>

1. <span data-ttu-id="8cfb4-121">Få tillgång till och kör mallen **Enable encryption on a running Windows VM ARM** (Aktivera kryptering på en Windows VM ARM som körs) från GitHub.</span><span class="sxs-lookup"><span data-stu-id="8cfb4-121">Access and run the **Enable encryption on a running Windows VM ARM** template from GitHub.</span></span>

1. <span data-ttu-id="8cfb4-122">Lägg till den nödvändiga informationen på skriptets konfigurationssida.</span><span class="sxs-lookup"><span data-stu-id="8cfb4-122">Add the required details in the script configuration page.</span></span>

1. <span data-ttu-id="8cfb4-123">Distribuera en ny virtuell dator med hjälp av skriptet genom att klicka på **Köp**.</span><span class="sxs-lookup"><span data-stu-id="8cfb4-123">Deploy a new VM using the script by clicking **Purchase**.</span></span>

1. <span data-ttu-id="8cfb4-124">Verifiera diskens krypteringsstatus genom att använda Azure-portalen.</span><span class="sxs-lookup"><span data-stu-id="8cfb4-124">Use the Azure portal to verify disk encryption status.</span></span>