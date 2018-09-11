<span data-ttu-id="9f591-101">I den här kursdelen utvärderar du en befintlig databas med hjälp av Data Migration Assistant och granskar funktioner som används i den lokala SQL Server-instansen som för närvarande inte stöds av Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="9f591-101">In this unit, you'll assess an existing database using the Data Migration Assistant and review any features used in the local SQL Server instance that aren't currently supported by Azure SQL Database.</span></span>

## <a name="setup"></a><span data-ttu-id="9f591-102">Konfiguration</span><span class="sxs-lookup"><span data-stu-id="9f591-102">Setup</span></span>

1. <span data-ttu-id="9f591-103">[Installera **Data Migration Assistant**](https://www.microsoft.com/download/details.aspx?id=53595) om du inte redan har gjort det.</span><span class="sxs-lookup"><span data-stu-id="9f591-103">[Install the **Data Migration Assistant**](https://www.microsoft.com/download/details.aspx?id=53595) if you haven't done so already.</span></span>

1. <span data-ttu-id="9f591-104">Du behöver en SQL Server-instans som körs. Kontrollera att du har anslutningsinformationen tillgänglig.</span><span class="sxs-lookup"><span data-stu-id="9f591-104">You'll need a SQL Server instance running, ensure you have connection details available.</span></span>

<!-- 1. [**** likely replace with an LOD VM *****] TODO: -->

1. <span data-ttu-id="9f591-105">Öppna en webbläsare och navigera till https://docs.microsoft.com/sql/samples/adventureworks-install-configure?view=sql-server-2017.</span><span class="sxs-lookup"><span data-stu-id="9f591-105">Start an Internet browser and navigate to https://docs.microsoft.com/sql/samples/adventureworks-install-configure?view=sql-server-2017.</span></span>

1. <span data-ttu-id="9f591-106">I **OLTP downloads** (OLTP-nedladdningar) klickar du på **AdventureWorks2008R2.bak** och sparar den till den lokala datorn.</span><span class="sxs-lookup"><span data-stu-id="9f591-106">In **OLTP downloads**, click **AdventureWorks2008R2.bak** and save it to your local machine.</span></span>

1. <span data-ttu-id="9f591-107">I Management Studio återställer du *AdventureWorks 2008R2* till din standardinstans.</span><span class="sxs-lookup"><span data-stu-id="9f591-107">In Management Studio, restore *AdventureWorks 2008R2* to your default instance.</span></span>

## <a name="create-an-assessment"></a><span data-ttu-id="9f591-108">Skapa en utvärdering</span><span class="sxs-lookup"><span data-stu-id="9f591-108">Create an assessment</span></span>

1. <span data-ttu-id="9f591-109">Starta **Microsoft Data Migration Assistant**.</span><span class="sxs-lookup"><span data-stu-id="9f591-109">Start the **Microsoft Data Migration Assistant**.</span></span>

1. <span data-ttu-id="9f591-110">I appens vänstra navigeringsfönstret klickar du på __+__ för att skapa ett nytt Data Migration Assistant-projekt.</span><span class="sxs-lookup"><span data-stu-id="9f591-110">In the app's left-hand navigation, click __+__ to create a new Data Migration Assistant project.</span></span>

1. <span data-ttu-id="9f591-111">Ange följande alternativ:</span><span class="sxs-lookup"><span data-stu-id="9f591-111">Specify the following options:</span></span>

    - <span data-ttu-id="9f591-112">**Projekttyp** – välj *Utvärdering*</span><span class="sxs-lookup"><span data-stu-id="9f591-112">**Project type** - Select *Assessment*</span></span>
    - <span data-ttu-id="9f591-113">**Projektnamn** – ange ett namn för ditt projekt, till exempel ”Bicycle DB Assessment”</span><span class="sxs-lookup"><span data-stu-id="9f591-113">**Project name** - Enter a name for your project - for example, "Bicycle DB Assessment"</span></span>
    - <span data-ttu-id="9f591-114">**Typ av källserver** – välj *SQL Server*</span><span class="sxs-lookup"><span data-stu-id="9f591-114">**Source server type** - Select *SQL Server*</span></span>
    - <span data-ttu-id="9f591-115">**Typ av målserver** – välj *Azure SQL Database*</span><span class="sxs-lookup"><span data-stu-id="9f591-115">**Target server type** - Select *Azure SQL Database*</span></span>

1. <span data-ttu-id="9f591-116">Klicka på **Skapa**.</span><span class="sxs-lookup"><span data-stu-id="9f591-116">Click **Create**.</span></span>
    <span data-ttu-id="9f591-117">![Skärmbild som visar den konfiguration som beskrivs i Data Migration Assistant för dina AdventureWorks SQL Server-data.](../media-draft/3-create-assessment.png)</span><span class="sxs-lookup"><span data-stu-id="9f591-117">![Screenshot showing the described configuration in the Data Migration Assistant for your AdventureWorks SQL Server data.](../media-draft/3-create-assessment.png)</span></span>

1. <span data-ttu-id="9f591-118">Välj typ av utvärderingsrapport – markera båda:</span><span class="sxs-lookup"><span data-stu-id="9f591-118">Select the assessment report type - check both:</span></span>
    - <span data-ttu-id="9f591-119">Kontrollera databaskompatibilitet</span><span class="sxs-lookup"><span data-stu-id="9f591-119">Check database compatibility</span></span>
    - <span data-ttu-id="9f591-120">Kontrollera funktionsparitet</span><span class="sxs-lookup"><span data-stu-id="9f591-120">Check feature parity</span></span>

1. <span data-ttu-id="9f591-121">Klicka på **Nästa**.</span><span class="sxs-lookup"><span data-stu-id="9f591-121">Click **Next**.</span></span>

## <a name="add-databases-to-assess"></a><span data-ttu-id="9f591-122">Lägg till databaser att utvärdera</span><span class="sxs-lookup"><span data-stu-id="9f591-122">Add databases to assess</span></span>

1. <span data-ttu-id="9f591-123">Klicka på **Lägg till källor** för att öppna anslutningsmenyn.</span><span class="sxs-lookup"><span data-stu-id="9f591-123">Click **Add Sources** to open the connection menu.</span></span>

1. <span data-ttu-id="9f591-124">Gör följande:</span><span class="sxs-lookup"><span data-stu-id="9f591-124">Do the following:</span></span>

    - <span data-ttu-id="9f591-125">Ange ditt befintliga SQL-serverinstansnamn</span><span class="sxs-lookup"><span data-stu-id="9f591-125">Enter your existing SQL server instance name</span></span>
    - <span data-ttu-id="9f591-126">Välj **Autentiseringstyp**</span><span class="sxs-lookup"><span data-stu-id="9f591-126">Select the **Authentication** type</span></span>
    - <span data-ttu-id="9f591-127">Ange anslutningsegenskaper för servern</span><span class="sxs-lookup"><span data-stu-id="9f591-127">Specify the connection properties for your server</span></span>

1. <span data-ttu-id="9f591-128">Klicka på **Anslut**.</span><span class="sxs-lookup"><span data-stu-id="9f591-128">CLick **Connect**.</span></span>

1. <span data-ttu-id="9f591-129">I **Lägg till källor** väljer du de databaser som ska utvärderas.</span><span class="sxs-lookup"><span data-stu-id="9f591-129">In **Add sources**, select the databases to assess.</span></span> <span data-ttu-id="9f591-130">För den här övningen väljer du **AdventureWorks2008R2**.</span><span class="sxs-lookup"><span data-stu-id="9f591-130">For this exercise, select **AdventureWorks2008R2**.</span></span>

1. <span data-ttu-id="9f591-131">Klicka på **Lägg till**.</span><span class="sxs-lookup"><span data-stu-id="9f591-131">Click **Add**.</span></span>
    > [!NOTE]
    > <span data-ttu-id="9f591-132">Om du vill lägga till databaser från flera SQL Server-instanser använder du knappen **Lägg till källor**.</span><span class="sxs-lookup"><span data-stu-id="9f591-132">To add databases from multiple SQL Server instances, use the **Add Sources** button.</span></span> <span data-ttu-id="9f591-133">Du kan ta bort flera databaser genom att hålla ned tangenterna SKIFT + CTRL, markera de databaser som ska tas bort och sedan klicka på **Ta bort källor**.</span><span class="sxs-lookup"><span data-stu-id="9f591-133">To remove multiple databases, hold the SHIFT+CTRL keys to select the databases you want to remove, then click **Remove Sources**.</span></span>

1. <span data-ttu-id="9f591-134">Klicka på **Starta utvärderingen**.</span><span class="sxs-lookup"><span data-stu-id="9f591-134">Click **Start Assessment**.</span></span>

## <a name="view-results"></a><span data-ttu-id="9f591-135">Visa resultat</span><span class="sxs-lookup"><span data-stu-id="9f591-135">View results</span></span>

<span data-ttu-id="9f591-136">Om det finns flera databaser visas resultaten för varje databas när de blir tillgängliga.</span><span class="sxs-lookup"><span data-stu-id="9f591-136">If there are multiple databases, the results for each database appears as soon as it is available.</span></span> <span data-ttu-id="9f591-137">Du behöver inte vänta tills alla databasutvärderingar är klara.</span><span class="sxs-lookup"><span data-stu-id="9f591-137">You don't need to wait for all database assessments to complete.</span></span>

1. <span data-ttu-id="9f591-138">När utvärderingen för **AdventureWorks** är klar klickar du på **Kompatibilitetsproblem** och **Funktionsrekommendationer** för att visa resultatet.</span><span class="sxs-lookup"><span data-stu-id="9f591-138">Once the assessment for **AdventureWorks** is complete, click **Compatibility issues** and **Feature recommendations** to view the results.</span></span>

    - <span data-ttu-id="9f591-139">Kategorin för SQL Server-funktionsparitet visar en lista över funktioner som kanske inte stöds fullständigt samt åtgärder för att lösa dessa problem.</span><span class="sxs-lookup"><span data-stu-id="9f591-139">The SQL Server feature parity category lists features that might not be fully supported and steps to remedy these issues.</span></span> <span data-ttu-id="9f591-140">Problem med funktionsparitet stoppar inte en migrering.</span><span class="sxs-lookup"><span data-stu-id="9f591-140">Feature parity issues will not stop a migration.</span></span>
    - <span data-ttu-id="9f591-141">Kategorin för kompatibilitetsproblem visar en lista över funktioner som skulle blockera en migrering samt åtgärder för att lösa dessa problem.</span><span class="sxs-lookup"><span data-stu-id="9f591-141">The Compatibility issues category lists features that would block a migration and steps to remedy these issues.</span></span>

## <a name="summary"></a><span data-ttu-id="9f591-142">Sammanfattning</span><span class="sxs-lookup"><span data-stu-id="9f591-142">Summary</span></span>

<span data-ttu-id="9f591-143">I den här kursdelen utvärderade en lokalt installerad SQL Server-databas för att kontrollera om några funktioner skulle bli tillgängliga när du migrerar databasen till Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="9f591-143">In this unit, you assessed a locally installed SQL Server database to verify if any features would be unavailable when you migrate the database to Azure SQL Database.</span></span>