<span data-ttu-id="fa4b8-101">Vår server är redo att bearbeta videodata. Det sista vi behöver göra är att öppna de portar som trafikkamerorna ska använda för att ladda upp videofiler till vår server.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-101">Our server is ready to process video data; the last thing we need to do is open the ports that the traffic cameras will use to upload video files to our server.</span></span> 

## <a name="create-a-network-security-group"></a><span data-ttu-id="fa4b8-102">Skapa en nätverkssäkerhetsgrupp</span><span class="sxs-lookup"><span data-stu-id="fa4b8-102">Create a network security group</span></span>

<span data-ttu-id="fa4b8-103">Azure bör ha skapat en säkerhetsgrupp åt oss eftersom vi angav att vi ville ha åtkomst till fjärrskrivbord.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-103">Azure should have created a security group for us because we indicated we wanted Remote Desktop access.</span></span> <span data-ttu-id="fa4b8-104">Men vi ska ändå skapa en ny säkerhetsgrupp så att du ser hur processen ser ut.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-104">But let's create a new security group so you can walk through the entire process.</span></span> <span data-ttu-id="fa4b8-105">Detta är särskilt viktigt om du bestämmer dig för att skapa det virtuella nätverket _innan_ de virtuella datorerna.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-105">This is particularly important if you decide to create your virtual network _before_ your VMs.</span></span> <span data-ttu-id="fa4b8-106">Som vi nämnt tidigare är säkerhetsgrupper _valfria_ och skapas inte nödvändigtvis med nätverket.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-106">As mentioned earlier, security groups are _optional_ and not necessarily created with the network.</span></span>

> [!NOTE]
> <span data-ttu-id="fa4b8-107">Eftersom detta _antas vara_ den andra virtuella datorn, borde vi redan ha en säkerhetsgrupp som vi kan använda för vårt nätverk. Men anta för ett ögonblick att vi inte har någon säkerhetsgrupp eller att reglerna skiljer sig för den här virtuella datorn.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-107">Since this is _supposed_ to be the second VM, we would already have a security group to apply to our network, but let's pretend for a moment that we don't, or that the rules are different for this VM.</span></span>

1. <span data-ttu-id="fa4b8-108">Skapa en ny resurs genom att klicka på knappen **Skapa en resurs** på den vänstra sidopanelen på [Azure Portal](https://portal.azure.com?azure-portal=true).</span><span class="sxs-lookup"><span data-stu-id="fa4b8-108">In the [Azure portal](https://portal.azure.com?azure-portal=true), click the **Create a resource** button in the left corner sidebar to start a new resource creation.</span></span>

1. <span data-ttu-id="fa4b8-109">Skriv ”Nätverkssäkerhetsgrupp” i filterrutan och välj det matchande objektet i listan.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-109">Type "Network security group" into the filter box and select the matching item in the list.</span></span>

1. <span data-ttu-id="fa4b8-110">Kontrollera att distributionsmodellen **Resource Manager** är vald och klicka på **Skapa**.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-110">Make sure the **Resource Manager** deployment model is selected and click **Create**.</span></span>

1. <span data-ttu-id="fa4b8-111">Ange ett **namn** för din säkerhetsgrupp.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-111">Provide a **Name** for your security group.</span></span> <span data-ttu-id="fa4b8-112">Även här är det bra att följa namngivningskonventioner. I vårt exempel använder vi ”test-vp-nsg2” för ”Test Videon Processor Network Security Group #2”.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-112">Again, naming conventions are a good idea here, let's use "test-vp-nsg2" for "Test Video Processor Network Security Group #2".</span></span>

1. <span data-ttu-id="fa4b8-113">Välj rätt **prenumeration** och använd din befintliga **resursgrupp**.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-113">Select the proper **Subscription** and use your existing **Resource group**.</span></span>

1. <span data-ttu-id="fa4b8-114">Placera den sedan på samma **plats** som den virtuella datorn/det virtuella nätverket.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-114">Finally, put it into the same **Location** as the VM / Virtual Network.</span></span> <span data-ttu-id="fa4b8-115">Obs! Du kan inte använda den här resursen om den finns på en annan plats.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-115">This is important - you won't be able to apply this resource if it's in a different location.</span></span>

1. <span data-ttu-id="fa4b8-116">Skapa gruppen genom att klicka på **Skapa**.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-116">Click **Create** to create the group.</span></span>

## <a name="add-a-new-inbound-rule-to-our-network-security-group"></a><span data-ttu-id="fa4b8-117">Lägga till en ny inkommande regel i nätverkssäkerhetsgruppen</span><span class="sxs-lookup"><span data-stu-id="fa4b8-117">Add a new inbound rule to our Network Security Group</span></span>

<span data-ttu-id="fa4b8-118">Distributionen bör slutföras snabbt.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-118">Deployment should complete quickly.</span></span>

1. <span data-ttu-id="fa4b8-119">Leta upp den nya säkerhetsgruppsresursen och välj den på Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-119">Find the new security group resource and select it in the Azure portal.</span></span>

1. <span data-ttu-id="fa4b8-120">På översiktssidan ser du att den har några standardregler för att låsa nätverket.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-120">On the overview page, you'll find that it has some default rules created to lock down the network.</span></span>

    <span data-ttu-id="fa4b8-121">På sidan för inkommande trafik:</span><span class="sxs-lookup"><span data-stu-id="fa4b8-121">On the inbound side:</span></span>

    - <span data-ttu-id="fa4b8-122">All inkommande trafik från ett virtuellt nätverk till ett annat tillåts.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-122">All inbound traffic from one VNet to another is allowed.</span></span> <span data-ttu-id="fa4b8-123">På så sätt kan resurser i det virtuella nätverket prata med varandra.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-123">This lets resources on the VNet talk to each other.</span></span>
    - <span data-ttu-id="fa4b8-124">Azure Load Balancer ”avsöker” begäranden för att säkerställa att den virtuella datorn är aktiv</span><span class="sxs-lookup"><span data-stu-id="fa4b8-124">Azure Load balancer "probe" requests to ensure the VM is alive</span></span>
    - <span data-ttu-id="fa4b8-125">All annan inkommande trafik nekas.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-125">All other inbound traffic is denied.</span></span>
    <span data-ttu-id="fa4b8-126">På sidan för utgående trafik:</span><span class="sxs-lookup"><span data-stu-id="fa4b8-126">On the outbound side:</span></span>
    - <span data-ttu-id="fa4b8-127">All nätverkstrafik i det virtuella nätverket tillåts.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-127">All in-network traffic on the VNet is allowed.</span></span>
    - <span data-ttu-id="fa4b8-128">All utgående trafik till Internet tillåts.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-128">All outbound traffic to the Internet is allowed.</span></span>
    - <span data-ttu-id="fa4b8-129">All annan utgående trafik nekas.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-129">All other outbound traffic is denied.</span></span>

> [!NOTE]
> <span data-ttu-id="fa4b8-130">Dessa standardregler är inställda med höga prioritetsvärden, vilket innebär att de utvärderas _sist_.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-130">These default rules are set with high priority values, which means that they get evaluated _last_.</span></span> <span data-ttu-id="fa4b8-131">De kan inte ändras eller tas bort, men du kan _åsidosätta_ dem genom att skapa mer specifika regler som matchar din trafik med ett lägre prioritetsvärde.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-131">They cannot be changed or deleted, but you can _override_ them by creating more specific rules to match your traffic with a lower priority value.</span></span>

1. <span data-ttu-id="fa4b8-132">Klicka på avsnittet **Inkommande säkerhetsregler** på panelen **Inställningar** för säkerhetsgruppen.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-132">Click the **Inbound security rules** section in the **Settings** panel for the security group.</span></span>

1. <span data-ttu-id="fa4b8-133">Lägg till en ny säkerhetsregel genom att klicka på **+ Lägg till**.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-133">Click **+ Add** to add a new security rule.</span></span>

    ![Lägg till en säkerhetsregel](../media-drafts/8-add-rule.png)

    <span data-ttu-id="fa4b8-135">Du kan ange informationen som behövs för en säkerhetsregel med någon av två metoder: grundläggande och avancerat.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-135">There are two ways to enter the information necessary for a security rule: basic and advanced.</span></span> <span data-ttu-id="fa4b8-136">Du kan växla mellan dem genom att klicka på knappen längst upp på panelen ”Lägg till”.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-136">You can switch between them by clicking the button at the top of the "add" panel.</span></span>

    ![Grundläggande jämfört med avancerad regelinmatning](../media-drafts/8-advanced-create-rule.png)

    <span data-ttu-id="fa4b8-138">I avancerat läge kan du anpassa regeln helt, men om du bara behöver konfigurera ett känt protokoll är det lite enklare att arbeta i grundläggande läge.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-138">The advanced mode provides the ability to completely customize the rule, however, if you just need to configure a known protocol, the basic mode is a bit easier to work with.</span></span>

1. <span data-ttu-id="fa4b8-139">Växla till grundläggande läge.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-139">Switch to the Basic mode.</span></span>

1. <span data-ttu-id="fa4b8-140">Lägg till informationen för vår FTP-regel.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-140">Add the information for our FTP rule.</span></span>

    - <span data-ttu-id="fa4b8-141">Ange FTP för **Tjänst**.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-141">Set the **Service** to be FTP.</span></span> <span data-ttu-id="fa4b8-142">När du gör det anges portintervallet åt dig.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-142">This will set your port range up for you.</span></span>
    - <span data-ttu-id="fa4b8-143">Ange ”1000” för **Prioritet**.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-143">Set the **Priority** to "1000".</span></span> <span data-ttu-id="fa4b8-144">Det måste vara ett lägre värde än för standardregeln **Neka**.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-144">It has to be a lower number than the default **Deny** rule.</span></span> <span data-ttu-id="fa4b8-145">Du kan starta intervallet vid valfritt värde, men vi rekommenderar att du lägger till marginaler om ett undantag måste skapas senare.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-145">You can start the range at any value, but it's recommended you give yourself some space in case an exception needs to be created later.</span></span>
    - <span data-ttu-id="fa4b8-146">Ge regeln ett namn. I vårt exempel använder vi ”traffic-cam-ftp-upload-2”.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-146">Give the rule a name, we'll use "traffic-cam-ftp-upload-2".</span></span>
    - <span data-ttu-id="fa4b8-147">Ge regeln en beskrivning.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-147">Give the rule a description.</span></span>

1. <span data-ttu-id="fa4b8-148">Gå tillbaka till läget **Avancerat**.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-148">Switch back to the **Advanced** mode.</span></span> <span data-ttu-id="fa4b8-149">Observera att inställningarna finns kvar.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-149">Notice that our settings are still present.</span></span> <span data-ttu-id="fa4b8-150">Vi kan använda den här panelen för att skapa mer detaljerade inställningar.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-150">We can use this panel to create more fine-grained settings.</span></span> <span data-ttu-id="fa4b8-151">I synnerhet vill vi sannolikt begränsa **Källa** till en bestämd IP-adress eller ett intervall med IP-adresser som är specifika för kamerorna.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-151">In particular, we would likely restrict the **Source** to be a specific IP address or range of IP addresses specific to the cameras.</span></span> <span data-ttu-id="fa4b8-152">Om du känner till den aktuella IP-adressen för den lokala datorn kan du prova med den.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-152">If you know the current IP address of your local computer, you can try that.</span></span> <span data-ttu-id="fa4b8-153">Annars lämnar du inställningen som ”Alla” så att du kan testa regeln.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-153">Otherwise, leave the setting as "Any" so you can test the rule.</span></span>

1. <span data-ttu-id="fa4b8-154">Klicka på **Lägg till** för att skapa regeln.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-154">Click **Add** to create the rule.</span></span> <span data-ttu-id="fa4b8-155">När du gör det uppdateras listan över regler för inkommande trafik – observera att de visas i prioritetsordning, vilket är den ordning som de kommer att granskas i.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-155">This will update the list of inbound rules - notice they are in priority order, which is how they will be examined.</span></span>
    
## <a name="apply-the-security-group"></a><span data-ttu-id="fa4b8-156">Tillämpa säkerhetsgruppen</span><span class="sxs-lookup"><span data-stu-id="fa4b8-156">Apply the security group</span></span>

<span data-ttu-id="fa4b8-157">Som du kanske minns kan vi tillämpa säkerhetsgruppen på ett nätverksgränssnitt för att skydda en enskild virtuell dator, eller på ett undernät där det i så fall gäller för alla resurser i undernätet.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-157">Recall that we can apply the security group to a network interface to guard a single VM, or to a subnet where it would apply to any resources on that subnet.</span></span> <span data-ttu-id="fa4b8-158">Den senare metoden brukar vara den vanligaste, så vi använder den.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-158">The latter approach tends to be the most common so let's do that.</span></span> <span data-ttu-id="fa4b8-159">Vi kan komma till den här resursen i Azure antingen via den virtuella nätverksresursen eller indirekt via den virtuella datorn som använder det virtuella nätverket.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-159">We could get to this resource in Azure through either the virtual network resource or indirectly through the VM which is using the virtual network.</span></span>

1. <span data-ttu-id="fa4b8-160">Växla till panelen **Översikt** för den virtuella datorn.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-160">Switch to the **Overview** panel for the virtual machine.</span></span> <span data-ttu-id="fa4b8-161">Du kan hitta den virtuella datorn under **Alla resurser**.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-161">You can find the VM under **All Resources**.</span></span>

1. <span data-ttu-id="fa4b8-162">Välj objektet **Nätverk** i avsnittet **Inställningar**.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-162">Select the **Networking** item in the **Settings** section.</span></span>

    ![Nätverksobjekt i inställningarna för virtuella datorer](../media-drafts/8-network-settings.png)

1. <span data-ttu-id="fa4b8-164">I nätverksegenskaperna hittar du information om de nätverksinställningar som tillämpas på den virtuella datorn, inklusive det **virtuella nätverket/undernätet**.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-164">In the networking properties, you will find information about the networking applied to the VM including the **Virtual network/subnet**.</span></span> <span data-ttu-id="fa4b8-165">Det här är en klickbar länk till resursen.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-165">This is a clickable link to get to the resource.</span></span> <span data-ttu-id="fa4b8-166">Klicka på den för att öppna det virtuella nätverket.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-166">Click it to open the virtual network.</span></span> <span data-ttu-id="fa4b8-167">Den här länken är _även_ tillgänglig på panelen **Översikt** för den virtuella datorn.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-167">This link is _also_ available on the **Overview** panel of the VM.</span></span> <span data-ttu-id="fa4b8-168">Någon av dessa öppnar **översikten** för det virtuella nätverket.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-168">Either of these will open the **Overview** of the virtual network.</span></span>

1. <span data-ttu-id="fa4b8-169">Välj objektet **Undernät** i avsnittet **Inställningar**.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-169">In the **Settings** section, select the **Subnets** item.</span></span>

1. <span data-ttu-id="fa4b8-170">Vi bör ha ett enskilt undernät definierat (standard) sedan tidigare då vi skapade den virtuella datorn och nätverket.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-170">We should have a single subnet defined (default) from when we created the VM + network earlier.</span></span> <span data-ttu-id="fa4b8-171">Klicka på objektet i listan för att öppna informationen.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-171">Click the item in the list to open the details.</span></span>

1. <span data-ttu-id="fa4b8-172">Klicka på posten **Nätverkssäkerhetsgrupp**.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-172">Click the **Network security group** entry.</span></span>

1. <span data-ttu-id="fa4b8-173">Välj den nya säkerhetsgruppen: **test-vp-nsg2**.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-173">Select your new security group: **test-vp-nsg2**.</span></span>

1. <span data-ttu-id="fa4b8-174">Spara ändringen genom att klicka på **Spara**.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-174">Click **Save** to save the change.</span></span> <span data-ttu-id="fa4b8-175">Det tar någon minut att tillämpa ändringen i nätverket.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-175">It will take a minute to apply to the network.</span></span>

## <a name="verify-the-rules"></a><span data-ttu-id="fa4b8-176">Verifiera reglerna</span><span class="sxs-lookup"><span data-stu-id="fa4b8-176">Verify the rules</span></span>

<span data-ttu-id="fa4b8-177">Nu ska vi verifiera ändringen.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-177">Let's validate the change.</span></span>

1. <span data-ttu-id="fa4b8-178">Växla tillbaka till panelen **Översikt** för den virtuella datorn.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-178">Switch back to the **Overview** panel for the virtual machine.</span></span> <span data-ttu-id="fa4b8-179">Du kan hitta den virtuella datorn under **Alla resurser**.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-179">You can find the VM under **All Resources**.</span></span>

1. <span data-ttu-id="fa4b8-180">Välj objektet **Nätverk** i avsnittet **Inställningar**.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-180">Select the **Networking** item in the **Settings** section.</span></span>

1. <span data-ttu-id="fa4b8-181">På panelen **Översikt** för nätverket finns en länk för \*\*Gällande säkerhetsregler som snabbt visar hur regler utvärderas.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-181">In the **Overview** panel for the network, there is a link for \*\*Effective security rules that will quickly show you how rules are going to be evaluated.</span></span> <span data-ttu-id="fa4b8-182">Klicka på länken för att öppna analysen och kontrollera att du ser din FTP-regel.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-182">Click the link to open the analysis and make sure you see your FTP rule.</span></span>

    ![Gällande säkerhetsregler för vårt nätverk](../media-drafts/8-effective-rules.png)

1. <span data-ttu-id="fa4b8-184">Om du har installerat FTP-serverrollen bör du kunna ansluta till FTP-slutpunkten nu.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-184">If you installed the FTP server role, you should be able to connect to the FTP endpoint now.</span></span> <span data-ttu-id="fa4b8-185">Prova.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-185">Try it out.</span></span>

## <a name="one-more-thing"></a><span data-ttu-id="fa4b8-186">En till sak</span><span class="sxs-lookup"><span data-stu-id="fa4b8-186">One more thing</span></span>

<span data-ttu-id="fa4b8-187">Det kan vara knepigt att få till säkerhetsreglerna så att de blir rätt.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-187">Security rules are tricky to get right.</span></span> <span data-ttu-id="fa4b8-188">Vi gjorde faktiskt ett misstag när vi tillämpade den här nya säkerhetsgruppen – vi förlorade vår fjärrskrivbordsåtkomst!</span><span class="sxs-lookup"><span data-stu-id="fa4b8-188">We actually made a mistake when we applied this new security group - we lost our Remote Desktop access!</span></span> <span data-ttu-id="fa4b8-189">För att åtgärda det här problemet kan du lägga till en annan regel till säkerhetsgruppen som ger stöd för RDP-åtkomst.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-189">To fix this, you can add another rule to the security group to support RDP access.</span></span> <span data-ttu-id="fa4b8-190">Se till att begränsa de inkommande TCP/IP-adresserna för regeln till de som du äger.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-190">Make sure to restrict the inbound TCP/IP addresses for the rule to be the ones you own.</span></span>

> [!WARNING]
> <span data-ttu-id="fa4b8-191">Se alltid till att låsa portar som används för administrativ åtkomst.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-191">Always make sure to lock down ports used for administrative access.</span></span> <span data-ttu-id="fa4b8-192">En ännu bättre metod är att skapa ett VPN för att länka det virtuella nätverket till ditt privata nätverk och endast tillåta RDP- eller SSH-begäranden från det adressintervallet.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-192">An even better approach is to create a VPN to link the virtual network to your private network and only allow RDP or SSH requests from that address range.</span></span> <span data-ttu-id="fa4b8-193">Du kan också ändra den port som används av RDP till något annat än standardvärdet 3389.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-193">You can also change the port used by RDP to be something other than the default 3389.</span></span> <span data-ttu-id="fa4b8-194">Tänk på att det inte räcker att ändra portarna för att stoppa attacker, det gör det bara lite svårare att upptäcka dem.</span><span class="sxs-lookup"><span data-stu-id="fa4b8-194">Keep in mind that changing ports is not sufficient to stop attacks, it simply makes it a little harder to discover.</span></span>