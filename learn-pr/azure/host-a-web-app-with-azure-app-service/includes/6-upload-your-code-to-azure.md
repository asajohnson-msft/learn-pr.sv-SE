<span data-ttu-id="0449d-101">Nu ska vi se hur du kan mellanlagra innehållet och distribuera det med kort eller ingen avbrottstid.</span><span class="sxs-lookup"><span data-stu-id="0449d-101">Now, let's see how we can stage our content and deploy with little or no downtime.</span></span>

## <a name="what-is-a-deployment-slot"></a><span data-ttu-id="0449d-102">Vad är ett distributionsfack?</span><span class="sxs-lookup"><span data-stu-id="0449d-102">What is a deployment slot?</span></span>

<span data-ttu-id="0449d-103">Ett distributionsfack är en **fristående** webbapp i App Service som har sitt eget innehåll, sin egen konfiguration och även ett unikt värdnamn.</span><span class="sxs-lookup"><span data-stu-id="0449d-103">A deployment slot is an **independent** app in App Service with its own content, configuration, and even a unique host name.</span></span> <span data-ttu-id="0449d-104">Därför fungerar den precis som andra appar i App Service.</span><span class="sxs-lookup"><span data-stu-id="0449d-104">Therefore, it functions like any other app in App Service.</span></span>

<span data-ttu-id="0449d-105">Du kommer åt varje distributionsfack via dess unika webbadress.</span><span class="sxs-lookup"><span data-stu-id="0449d-105">Each deployment slot is accessible from its unique URL.</span></span> <span data-ttu-id="0449d-106">Låt oss anta att jag har lagt till ett distributionsfack för **mellanlagring** med namnet `BESTBIKE`.</span><span class="sxs-lookup"><span data-stu-id="0449d-106">For instance, let's say I've added a **staging** deployment slot with the name `BESTBIKE`.</span></span> <span data-ttu-id="0449d-107">Programmets och distributionsfackets webbadresser är:</span><span class="sxs-lookup"><span data-stu-id="0449d-107">The URLs for the application and deployment slot are:</span></span>

- https://BESTBIKE.azurewebsites.net/
- https://BESTBIKE-staging.azurewebsites.net/

## <a name="why-are-deployment-slots-useful"></a><span data-ttu-id="0449d-108">Varför är distributionsfack användbara?</span><span class="sxs-lookup"><span data-stu-id="0449d-108">Why are deployment slots useful?</span></span>

<span data-ttu-id="0449d-109">När du distribuerar en webbapp på det traditionella sättet, oavsett om det är via FTP, WebDeploy, Git eller något annat sätt, medför det vissa problem:</span><span class="sxs-lookup"><span data-stu-id="0449d-109">Deploying your web app in the traditional way, whether it be via FTP, Web Deploy, Git, or another way, has some weaknesses:</span></span>

- <span data-ttu-id="0449d-110">När distributionen är färdig startar webbappen kanske om, vilket orsakar en **kallstart** för programmet.</span><span class="sxs-lookup"><span data-stu-id="0449d-110">After the deployment completes, the app might restart, causing a **cold start** for the application.</span></span> <span data-ttu-id="0449d-111">Den första begäran till programmet blir långsammare.</span><span class="sxs-lookup"><span data-stu-id="0449d-111">The first request to the application will be slower.</span></span>

- <span data-ttu-id="0449d-112">Du kan eventuellt distribuera *felaktiga* versioner av appen, så du bör testa dem (i produktion) innan de lanseras till klienterna.</span><span class="sxs-lookup"><span data-stu-id="0449d-112">Potentially, you are deploying a *bad* version of your app, and you should test it (in production) before releasing it to your client.</span></span>

<span data-ttu-id="0449d-113">I de här situationerna kan du använda distributionsfack.</span><span class="sxs-lookup"><span data-stu-id="0449d-113">This is where deployment slots come into play.</span></span> <span data-ttu-id="0449d-114">Du kan skicka ändringar av appen till ett distributionsfack för **mellanlagring** och testa ändringarna utan att de påverkar användare som ansluter till distributionsfacket för **produktion**.</span><span class="sxs-lookup"><span data-stu-id="0449d-114">You can make changes to your app to a **staging** deployment slot and test the changes without impacting users who are accessing the **production** deployment slot.</span></span> <span data-ttu-id="0449d-115">När du är redo att flytta de nya funktionerna till produktion behöver du bara **växla** facken för mellanlagring och produktion **utan avbrottstid**.</span><span class="sxs-lookup"><span data-stu-id="0449d-115">When you are ready to move the new features into production, you can just **swap** the staging and production slots with **no downtime**.</span></span>

<span data-ttu-id="0449d-116">En annan fördel med distributionsfack är att du kan **värma upp** ditt program i en mellanlagringsplats innan du växlar det till produktionsplatsen.</span><span class="sxs-lookup"><span data-stu-id="0449d-116">Another benefit of using deployment slots is that you can **warm up** your application in a staging slot before swapping it into the production slot.</span></span> <span data-ttu-id="0449d-117">Du undviker fördröjningarna från en **kallstart** och den långa initieringskoden.</span><span class="sxs-lookup"><span data-stu-id="0449d-117">You will avoid the delays of a **cold start** and the lengthy initialization code.</span></span>

<span data-ttu-id="0449d-118">Slutligen kan du **växla tillbaka** till föregående distributionsfack om du upptäcker att den nya versionen av programmet inte fungerar som väntat.</span><span class="sxs-lookup"><span data-stu-id="0449d-118">Finally, you can **swap back** to the previous deployment slot if you realize that the new version of your application is not working as you expected.</span></span>

## <a name="what-is-automated-deployment"></a><span data-ttu-id="0449d-119">Vad är automatiserad distribution?</span><span class="sxs-lookup"><span data-stu-id="0449d-119">What is automated deployment?</span></span>

<span data-ttu-id="0449d-120">Automatiserad distribution, eller kontinuerlig integrering, är en process som används för att skicka ut nya funktioner och felkorrigeringar i ett snabbt och upprepat mönster med minimal inverkan på slutanvändarna.</span><span class="sxs-lookup"><span data-stu-id="0449d-120">Automated deployment, or continuous integration, is a process used to push out new features and bug fixes in a fast and repetitive pattern with minimal impact on end users.</span></span>

<span data-ttu-id="0449d-121">Azure har stöd för automatiserad distribution direkt från flera källor.</span><span class="sxs-lookup"><span data-stu-id="0449d-121">Azure supports automated deployment directly from several sources.</span></span> <span data-ttu-id="0449d-122">Följande alternativ är tillgänglig:</span><span class="sxs-lookup"><span data-stu-id="0449d-122">The following options are available:</span></span>

- <span data-ttu-id="0449d-123">**Visual Studio Team Services (VSTS)**: du kan skicka koden till VSTS, bygga koden i molnet, köra testerna, generera en version utifrån koden och slutligen skicka koden till den Azure-webbapp.</span><span class="sxs-lookup"><span data-stu-id="0449d-123">**Visual Studio Team Services (VSTS)**: You can push your code to VSTS, build your code in the cloud, run the tests, generate a release from the code, and finally, push your code to an Azure Web App.</span></span>

- <span data-ttu-id="0449d-124">**GitHub**: Azure har stöd för automatiserad distribution direkt från GitHub.</span><span class="sxs-lookup"><span data-stu-id="0449d-124">**GitHub**: Azure supports automated deployment directly from GitHub.</span></span> <span data-ttu-id="0449d-125">När du ansluter din GitHub-lagringsplats till Azure för automatiserad distribution distribueras eventuella ändringar du push-överför till produktionsgrenen i GitHub automatiskt åt dig.</span><span class="sxs-lookup"><span data-stu-id="0449d-125">When you connect your GitHub repository to Azure for automated deployment, any changes you push to your production branch on GitHub will be automatically deployed for you.</span></span>

- <span data-ttu-id="0449d-126">**Bitbucket**: Tack vare likheterna med GitHub kan du konfigurera en automatiserad distribution med Bitbucket.</span><span class="sxs-lookup"><span data-stu-id="0449d-126">**Bitbucket**: With its similarities to GitHub, you can configure an automated deployment with Bitbucket.</span></span>

- <span data-ttu-id="0449d-127">**OneDrive**: Du kan ansluta ditt OneDrive-konto till App Service så att Azure automatiskt identifierar filer du ändrar på OneDrive-kontot och hämtar de ändrade webbappsfilerna.</span><span class="sxs-lookup"><span data-stu-id="0449d-127">**OneDrive**: You can connect your OneDrive account with App Service so that when you change any file on your OneDrive account, Azure will automatically detect it and pull in any changes on the web app files.</span></span> <span data-ttu-id="0449d-128">Det här är ett utmärkt alternativ för statiska webbplatser.</span><span class="sxs-lookup"><span data-stu-id="0449d-128">This is a great option for static websites.</span></span> <span data-ttu-id="0449d-129">Du kommer att få känslan av att arbeta med ett lokalt filsystem som avspeglar alla eventuella ändringar i Azure smidigt och omedelbart.</span><span class="sxs-lookup"><span data-stu-id="0449d-129">It will give you the feeling that you are dealing with a local file system that reflects any changes on Azure, smoothly and instantly.</span></span>

- <span data-ttu-id="0449d-130">**Dropbox**: På ungefär samma sätt som med OneDrive kan du lagra dina webappsfiler på ett Dropbox-konto och göra så att de automatiskt skickas och distribueras via en webbapp.</span><span class="sxs-lookup"><span data-stu-id="0449d-130">**Dropbox**: Similar to OneDrive, you can host your web app files in a Dropbox account and have them automatically push and be deployed over a web app.</span></span>

- <span data-ttu-id="0449d-131">**Extern lagringsplats**: Du kan konfigurera automatiserad distribution med valfri extern Git-lagringsplats.</span><span class="sxs-lookup"><span data-stu-id="0449d-131">**External repository**: You can configure automated deployment with any external Git repository.</span></span>

### <a name="non-automated-deployment-to-azure"></a><span data-ttu-id="0449d-132">Icke-automatiserad distribution till Azure</span><span class="sxs-lookup"><span data-stu-id="0449d-132">Non-automated deployment to Azure</span></span>

<span data-ttu-id="0449d-133">Det finns några alternativ som du kan använda för att manuellt push-överföra din kod till Azure:</span><span class="sxs-lookup"><span data-stu-id="0449d-133">There are a few options that you can use to manually push your code to Azure:</span></span>

- <span data-ttu-id="0449d-134">**FTP/S**: FTP eller FTPS är ett traditionellt sätt att skicka koden till valfri värdmiljö.</span><span class="sxs-lookup"><span data-stu-id="0449d-134">**FTP/S**: FTP or FTPS is a traditional way of pushing your code to any hosting environment.</span></span> <span data-ttu-id="0449d-135">Även om det inte rekommenderas längre kan du fortfarande använda det.</span><span class="sxs-lookup"><span data-stu-id="0449d-135">Despite the fact that it is not recommended anymore, you can still make use of it.</span></span>

- <span data-ttu-id="0449d-136">**WebDeploy/IDE**: du kan använda IDE:n Visual Studio till att publicera din webbapp i Azure.</span><span class="sxs-lookup"><span data-stu-id="0449d-136">**Web Deploy/IDE**: You can use the Visual Studio IDE to publish your web app to Azure.</span></span> <span data-ttu-id="0449d-137">I publiceringsmekanismen i Visual Studio används WebDeploy-teknik till att skicka din kod till Azure.</span><span class="sxs-lookup"><span data-stu-id="0449d-137">The Visual Studio publishing mechanism can make use of Web Deploy technology to push your code to Azure.</span></span>

- <span data-ttu-id="0449d-138">**Git**: Azure har en **lokal Git-lagringsplats** för ditt program.</span><span class="sxs-lookup"><span data-stu-id="0449d-138">**Git**: Azure maintains a **local Git repository** for your application.</span></span> <span data-ttu-id="0449d-139">Du kan **checka in** din kod till den direkt.</span><span class="sxs-lookup"><span data-stu-id="0449d-139">You can **commit** your code directly to it.</span></span>

> <span data-ttu-id="0449d-140">I den här modulen utför vi en icke-automatiserad distribution med hjälp av Git.</span><span class="sxs-lookup"><span data-stu-id="0449d-140">In this module, we are going to perform a non-automated deployment using Git.</span></span>

## <a name="summary"></a><span data-ttu-id="0449d-141">Sammanfattning</span><span class="sxs-lookup"><span data-stu-id="0449d-141">Summary</span></span>

<span data-ttu-id="0449d-142">I Azure finns flera olika sätt att ladda upp din kod så att det passar i ditt arbetsflöde.</span><span class="sxs-lookup"><span data-stu-id="0449d-142">Azure provides multiple ways to upload your code to help it better fit in with your current workflow.</span></span> <span data-ttu-id="0449d-143">Du kan även använda distributionsfack så att inte användarna upplever några driftstopp.</span><span class="sxs-lookup"><span data-stu-id="0449d-143">You can also use deployment slots to help prevent downtime for your users.</span></span>