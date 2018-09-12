<span data-ttu-id="9dc4f-101">Anta att du har ett program för säljteamet i ditt globala företag.</span><span class="sxs-lookup"><span data-stu-id="9dc4f-101">Suppose you have an application for the sales team in your global company.</span></span> <span data-ttu-id="9dc4f-102">Varje teammedlem har en mobiltelefon där din app ska installeras.</span><span class="sxs-lookup"><span data-stu-id="9dc4f-102">Each team member has a mobile phone where your app will be installed.</span></span> <span data-ttu-id="9dc4f-103">En webbtjänst på Azure implementerar affärslogiken för ditt program och lagrar information i Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="9dc4f-103">A web service hosted in Azure implements the business logic for your application and stores information in Azure SQL Database.</span></span> <span data-ttu-id="9dc4f-104">Det finns en instans av webbtjänsten för varje geografisk region.</span><span class="sxs-lookup"><span data-stu-id="9dc4f-104">There is one instance of the web service for each geographical region.</span></span> <span data-ttu-id="9dc4f-105">Du har identifierat följande syften för att skicka meddelanden mellan mobilappen och webbtjänsten:</span><span class="sxs-lookup"><span data-stu-id="9dc4f-105">You have identified the following purposes for sending messages between the mobile app and the web service:</span></span>

- <span data-ttu-id="9dc4f-106">Meddelanden som är relaterade till enskilda försäljningar måste skickas endast till webbtjänstinstansen i användarens region.</span><span class="sxs-lookup"><span data-stu-id="9dc4f-106">Messages that relate to individual sales must be sent only to the web service instance in the user's region.</span></span>
- <span data-ttu-id="9dc4f-107">Meddelanden som är relaterade till försäljningsresultat måste skickas till alla instanser av webbtjänsten.</span><span class="sxs-lookup"><span data-stu-id="9dc4f-107">Messages that relate to sales performance must be sent to all instances of the web service.</span></span>

<span data-ttu-id="9dc4f-108">Du har valt att implementera en Service Bus-kö för det första användningsfallet och Service Bus-ämnet för det andra.</span><span class="sxs-lookup"><span data-stu-id="9dc4f-108">You have decided to implement a Service Bus queue for the first use case and the Service Bus topic for the second use case.</span></span>

<span data-ttu-id="9dc4f-109">I den här övningen skapar du ett Service Bus-namnområde som innehåller både en kö och ett ämne med prenumerationer.</span><span class="sxs-lookup"><span data-stu-id="9dc4f-109">In this exercise, you will create a Service Bus namespace, which will contain both a queue and a topic with subscriptions.</span></span>

## <a name="create-a-service-bus-namespace"></a><span data-ttu-id="9dc4f-110">Skapa ett namnområde för Service Bus</span><span class="sxs-lookup"><span data-stu-id="9dc4f-110">Create a Service Bus namespace</span></span>

<span data-ttu-id="9dc4f-111">I Azure Service Bus är ett namnområde en container med ett unikt fullständigt kvalificerat domännamn för köer, ämnen och reläer.</span><span class="sxs-lookup"><span data-stu-id="9dc4f-111">In Azure Service Bus, a namespace is a container, with a unique fully qualified domain name, for queues, topics, and relays.</span></span> <span data-ttu-id="9dc4f-112">Du börjar med att skapa namnområdet.</span><span class="sxs-lookup"><span data-stu-id="9dc4f-112">You must start by creating the namespace.</span></span>

<span data-ttu-id="9dc4f-113">Varje namnområde har också primära och sekundära krypteringsnycklar för signatur för delad åtkomst (SAS).</span><span class="sxs-lookup"><span data-stu-id="9dc4f-113">Each namespace also has primary and secondary Shared Access Signature (SAS) encryption keys.</span></span> <span data-ttu-id="9dc4f-114">En skickande eller mottagande komponent måste ange dessa nycklar när den ansluter för att få åtkomst till objekten inom namnområdet.</span><span class="sxs-lookup"><span data-stu-id="9dc4f-114">A sending or receiving component must provide these keys when it connects to gain access to the objects within the namespace.</span></span>

<span data-ttu-id="9dc4f-115">Följ de här stegen för att skapa ett Service Bus-namnområde med Azure-portalen:</span><span class="sxs-lookup"><span data-stu-id="9dc4f-115">To create a Service Bus namespace by using the Azure portal, following these steps:</span></span>

1. <span data-ttu-id="9dc4f-116">I en webbläsare går du till [Azure-portalen](https://portal.azure.com/) och loggar in med dina vanliga autentiseringsuppgifter för Azure-kontot.</span><span class="sxs-lookup"><span data-stu-id="9dc4f-116">In a browser, navigate the to [Azure portal](https://portal.azure.com/) and log in with your usual Azure account credentials.</span></span>

1. <span data-ttu-id="9dc4f-117">I det vänstra navigeringsfönstret klickar du på **Alla tjänster**.</span><span class="sxs-lookup"><span data-stu-id="9dc4f-117">In the navigation on the left, click **All services**.</span></span>

1. <span data-ttu-id="9dc4f-118">I bladet **Alla tjänster** bläddrar du ned till avsnittet **Integrering** och klickar sedan på **Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="9dc4f-118">In the **All Services** blade, scroll down to the **INTEGRATION** section and then click **Service Bus**.</span></span>

    ![Skapa ett namnområde för Service Bus](../media-draft/3-create-namespace-1.png)

1. <span data-ttu-id="9dc4f-120">Längst upp till vänster på bladet **Service Bus** klickar du på **Lägg till**.</span><span class="sxs-lookup"><span data-stu-id="9dc4f-120">In the top left of the **Service Bus** blade, click **Add**.</span></span>

1. <span data-ttu-id="9dc4f-121">Ange ett unikt namn för namnområdet i textrutan **Namn**.</span><span class="sxs-lookup"><span data-stu-id="9dc4f-121">In the **Name** textbox, type a unique name for the namespace.</span></span> <span data-ttu-id="9dc4f-122">Till exempel salesteamapp + *dina initialer* + *aktuellt datum*</span><span class="sxs-lookup"><span data-stu-id="9dc4f-122">For example "salesteamapp" + *your initials* + *current date*</span></span>

1. <span data-ttu-id="9dc4f-123">I listrutan **Prisnivå**, väljer du **Standard**.</span><span class="sxs-lookup"><span data-stu-id="9dc4f-123">In the **Pricing tier** drop-down list, select **Standard**.</span></span>

1. <span data-ttu-id="9dc4f-124">I listrutan **Prenumeration** väljer du din prenumeration.</span><span class="sxs-lookup"><span data-stu-id="9dc4f-124">In the **Subscription** drop-down list, select your subscription.</span></span>

1. <span data-ttu-id="9dc4f-125">Under **Resursgrupp** väljer du **Skapa ny** och skriver in **SalesTeamAppRG**.</span><span class="sxs-lookup"><span data-stu-id="9dc4f-125">Under **Resource group** select **Create new**, and then type **SalesTeamAppRG**.</span></span>

1. <span data-ttu-id="9dc4f-126">I listrutan **Plats** väljer du en plats nära dig och klickar sedan på **Skapa**.</span><span class="sxs-lookup"><span data-stu-id="9dc4f-126">In the **Location** drop-down list, select a location near you and then click **Create**.</span></span> <span data-ttu-id="9dc4f-127">Azure skapar det nya Service Bus-namnområdet.</span><span class="sxs-lookup"><span data-stu-id="9dc4f-127">Azure creates the new Service Bus namespace.</span></span>

    ![Skapa ett namnområde för Service Bus](../media-draft/3-create-namespace-2.png)

## <a name="create-a-service-bus-queue"></a><span data-ttu-id="9dc4f-129">Skapa en Service Bus-kö</span><span class="sxs-lookup"><span data-stu-id="9dc4f-129">Create a Service Bus queue</span></span>

<span data-ttu-id="9dc4f-130">Nu när du har ett namnområde, kan du skapa en kö för meddelanden om enskild försäljning.</span><span class="sxs-lookup"><span data-stu-id="9dc4f-130">Now that you have a namespace, you can create a queue for messages about individual sales.</span></span> <span data-ttu-id="9dc4f-131">Det gör du genom att följa dessa steg:</span><span class="sxs-lookup"><span data-stu-id="9dc4f-131">To do this, follow these steps:</span></span>

1. <span data-ttu-id="9dc4f-132">På bladet **Service Bus** klickar du på **Uppdatera**.</span><span class="sxs-lookup"><span data-stu-id="9dc4f-132">In the **Service Bus** blade, click **Refresh**.</span></span> <span data-ttu-id="9dc4f-133">Det namnområde som du nyss skapade visas.</span><span class="sxs-lookup"><span data-stu-id="9dc4f-133">The namespace you just created is displayed.</span></span>

1. <span data-ttu-id="9dc4f-134">Klicka på det namnområde som du nyss skapade.</span><span class="sxs-lookup"><span data-stu-id="9dc4f-134">Click the namespace you just created.</span></span>

1. <span data-ttu-id="9dc4f-135">Längst upp till vänster på namnområdesbladet klickar du på **+ Kö**.</span><span class="sxs-lookup"><span data-stu-id="9dc4f-135">In the top left of the namespace blade, click **+ Queue**.</span></span>

1. <span data-ttu-id="9dc4f-136">I bladet **Skapa kö** i textrutan **Namn** textrutetypen **salesmessages** och klickar sedan på **Skapa**.</span><span class="sxs-lookup"><span data-stu-id="9dc4f-136">In the **Create queue** blade, in the **Name** textbox type **salesmessages**, and then click **Create**.</span></span> <span data-ttu-id="9dc4f-137">Azure skapar kön i ditt namnområde.</span><span class="sxs-lookup"><span data-stu-id="9dc4f-137">Azure creates the queue in your namespace.</span></span>

    ![Skapa en kö](../media-draft/3-create-queue.png)

## <a name="create-a-service-bus-topic-and-subscriptions"></a><span data-ttu-id="9dc4f-139">Skapa ett Service Bus-ämne och prenumerationer</span><span class="sxs-lookup"><span data-stu-id="9dc4f-139">Create a Service Bus topic and subscriptions</span></span>

<span data-ttu-id="9dc4f-140">Du bör också skapa ett ämne som ska användas för meddelanden som är relaterade till försäljningsresultat.</span><span class="sxs-lookup"><span data-stu-id="9dc4f-140">You also want to create a topic that will be used for messages that relate to sales performance.</span></span> <span data-ttu-id="9dc4f-141">Flera instanser av webbtjänsten för affärslogik kommer att prenumerera på det här ämnet från olika länder.</span><span class="sxs-lookup"><span data-stu-id="9dc4f-141">Multiple instances of the business logic web service will subscribe to this topic from different countries.</span></span> <span data-ttu-id="9dc4f-142">Varje meddelande levereras till flera instanser.</span><span class="sxs-lookup"><span data-stu-id="9dc4f-142">Each message will be delivered to multiple instances.</span></span>

<span data-ttu-id="9dc4f-143">Följ de här stegen:</span><span class="sxs-lookup"><span data-stu-id="9dc4f-143">Follow these steps:</span></span>

1. <span data-ttu-id="9dc4f-144">På bladet **Service Bus-namnområde** klickar du på **+ Ämne**.</span><span class="sxs-lookup"><span data-stu-id="9dc4f-144">In the **Service Bus Namespace** blade, click **+ Topic**.</span></span>

1. <span data-ttu-id="9dc4f-145">I bladet **Skapa ämne** i textrutan **Namn** textrutetypen **salesperformancemessages** och klicka sedan på **Skapa**.</span><span class="sxs-lookup"><span data-stu-id="9dc4f-145">In the **Create topic** blade, in the **Name** textbox type **salesperformancemessages**, and then click **Create**.</span></span> <span data-ttu-id="9dc4f-146">Azure skapar ämnet i ditt namnområde.</span><span class="sxs-lookup"><span data-stu-id="9dc4f-146">Azure creates the topic in your namespace.</span></span>

    ![Skapa ett ämne](../media-draft/3-create-topic.png)

1. <span data-ttu-id="9dc4f-148">När ämnet har skapats i bladet **Service Bus-namnområde** under **Entiteter**, klickar du på **Ämnen**.</span><span class="sxs-lookup"><span data-stu-id="9dc4f-148">When the topic has been created, in the **Service Bus Namespace** blade, under **Entities** click **Topics**.</span></span>

1. <span data-ttu-id="9dc4f-149">I listan med ämnen, klickar du på **salesperformancemessages** och klickar sedan på **+ Prenumeration**.</span><span class="sxs-lookup"><span data-stu-id="9dc4f-149">In the list of topics, click **salesperformancemessages** and then click **+ Subscription**.</span></span>

1. <span data-ttu-id="9dc4f-150">I textrutan **Namn**, typen **Americas** och klickar sedan på **Skapa**.</span><span class="sxs-lookup"><span data-stu-id="9dc4f-150">In the **Name** textbox, type **Americas** and then click **Create**.</span></span>

1. <span data-ttu-id="9dc4f-151">Klicka på **+ Prenumeration**.</span><span class="sxs-lookup"><span data-stu-id="9dc4f-151">Click **+ Subscription**.</span></span>

1. <span data-ttu-id="9dc4f-152">I textrutan **Namn**, typen **EuropeAndAfrica** och klickar sedan på **Skapa**.</span><span class="sxs-lookup"><span data-stu-id="9dc4f-152">In the **Name** textbox, type **EuropeAndAfrica** and then click **Create**.</span></span>

<span data-ttu-id="9dc4f-153">Du har skapat den infrastruktur som krävs för att använda Service Bus för att öka flexibiliteten för din säljstyrkas distribuerade program.</span><span class="sxs-lookup"><span data-stu-id="9dc4f-153">You have built the infrastructure required to use Service Bus to increase the resilience of your sales force distributed application.</span></span> <span data-ttu-id="9dc4f-154">Du har skapat en kö för meddelanden om enskild försäljning och ett ämne för meddelanden om försäljningsresultat.</span><span class="sxs-lookup"><span data-stu-id="9dc4f-154">You have created a queue for messages about individual sales and a topic for messages about sales performance.</span></span> <span data-ttu-id="9dc4f-155">Avsnittet innehåller flera prenumerationer eftersom meddelanden som skickas till detta ämne kan levereras till flera mottagande webbtjänster över hela världen.</span><span class="sxs-lookup"><span data-stu-id="9dc4f-155">The topic includes multiple subscriptions because messages sent to that topic can be delivered to multiple recipient web services around the world.</span></span>