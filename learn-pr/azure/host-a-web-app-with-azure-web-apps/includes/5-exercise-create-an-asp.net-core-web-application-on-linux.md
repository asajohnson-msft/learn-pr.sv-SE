<span data-ttu-id="b9bf4-101">I den här övningen skapar du en ASP.NET Core-webbapp med hjälp av .NET CLI på en Ubuntu-dator.</span><span class="sxs-lookup"><span data-stu-id="b9bf4-101">In this unit, you will create an ASP.NET Core web app using the .NET CLI on an Ubuntu machine.</span></span>

## <a name="aspnet-core-installation-on-linux-environment"></a><span data-ttu-id="b9bf4-102">ASP.NET Core-installation i Linux-miljö</span><span class="sxs-lookup"><span data-stu-id="b9bf4-102">ASP.NET Core installation on Linux environment</span></span>

<span data-ttu-id="b9bf4-103">Gå till Microsofts [nedladdningssida för .NET](https://www.microsoft.com/net/download) och följ samma steg som på .NET Core SDK-sidan.</span><span class="sxs-lookup"><span data-stu-id="b9bf4-103">Visit the Microsoft [.NET Downloads page](https://www.microsoft.com/net/download) and follow the same steps mentioned on the .NET Core SDK page.</span></span> <span data-ttu-id="b9bf4-104">De finns nedan.</span><span class="sxs-lookup"><span data-stu-id="b9bf4-104">They are below.</span></span> <span data-ttu-id="b9bf4-105">För att köra kommandona måste du öppna en ny **terminalinstans**.</span><span class="sxs-lookup"><span data-stu-id="b9bf4-105">In order to execute the commands, you need to open a new **Terminal** command-line instance.</span></span>

### <a name="register-microsoft-key-and-feed"></a><span data-ttu-id="b9bf4-106">Registrera Microsoft-nyckel och feed</span><span class="sxs-lookup"><span data-stu-id="b9bf4-106">Register Microsoft key and feed</span></span>

<span data-ttu-id="b9bf4-107">Innan du installerar .NET måste du registrera Microsoft-nyckeln, registrera produktlagringsplatsen och installera nödvändiga beroenden.</span><span class="sxs-lookup"><span data-stu-id="b9bf4-107">Before installing .NET, you'll need to register the Microsoft key, register the product repository, and install the required dependencies.</span></span> <span data-ttu-id="b9bf4-108">Detta behöver bara göras en gång per dator.</span><span class="sxs-lookup"><span data-stu-id="b9bf4-108">This only needs to be done once per machine.</span></span>

```console
~$ wget -q https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb
~$ sudo dpkg -i packages-microsoft-prod.deb
```

## <a name="install-the-net-sdk"></a><span data-ttu-id="b9bf4-109">Installera .NET SDK</span><span class="sxs-lookup"><span data-stu-id="b9bf4-109">Install the .NET SDK</span></span>

<span data-ttu-id="b9bf4-110">Uppdatera de produkter som är tillgängliga för installation och sedan installera .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="b9bf4-110">Update the products available for installation, then install the .NET SDK.</span></span>

<span data-ttu-id="b9bf4-111">Kör följande kommandon i kommandotolken:</span><span class="sxs-lookup"><span data-stu-id="b9bf4-111">At your command prompt, run the following commands:</span></span>

```console
sudo apt-get install apt-transport-https
sudo apt-get update
sudo apt-get install dotnet-sdk-2.1
```

<span data-ttu-id="b9bf4-112">Under installationen kan du bli ombedd att ange lösenordet för kontot.</span><span class="sxs-lookup"><span data-stu-id="b9bf4-112">During the installation process, you might be asked to enter your account password.</span></span> <span data-ttu-id="b9bf4-113">Ange lösenordet och tryck på Retur för att fortsätta.</span><span class="sxs-lookup"><span data-stu-id="b9bf4-113">Provide your password and hit Enter to continue.</span></span>

<span data-ttu-id="b9bf4-114">För att verifiera installationen skriver du följande:</span><span class="sxs-lookup"><span data-stu-id="b9bf4-114">To verify the installation, type the following:</span></span>

```console
dotnet --version
```

<span data-ttu-id="b9bf4-115">Och de utdata som visas är:</span><span class="sxs-lookup"><span data-stu-id="b9bf4-115">And the output displayed is:</span></span>

```console
2.1.302
```

<span data-ttu-id="b9bf4-116">Nu när du har installerat .NET Core SDK har du även ASP.NET Core installerat.</span><span class="sxs-lookup"><span data-stu-id="b9bf4-116">Now that you have the .NET Core SDK installed, you also have the ASP.NET Core installed.</span></span> <span data-ttu-id="b9bf4-117">Nu går vi igenom hur du kan använda .NET CLI för att skapa ett nytt ASP.NET Core-projekt med hjälp av de kommandon vi just har lärt oss.</span><span class="sxs-lookup"><span data-stu-id="b9bf4-117">Let's see together how you can make use of the .NET CLI to create a new ASP.NET Core project using the commands we just learned.</span></span>

## <a name="open-a-terminal-window"></a><span data-ttu-id="b9bf4-118">Öppna ett terminalfönster</span><span class="sxs-lookup"><span data-stu-id="b9bf4-118">Open a Terminal window</span></span>

<span data-ttu-id="b9bf4-119">Först behöver du öppna terminalfönstret.</span><span class="sxs-lookup"><span data-stu-id="b9bf4-119">First, you need to open the Terminal window.</span></span> <span data-ttu-id="b9bf4-120">I terminalfönstret kan du köra kommandon, det fungerar ungefär som kommandotolken i Windows.</span><span class="sxs-lookup"><span data-stu-id="b9bf4-120">The Terminal window allows you to execute commands, and has a similar role to the Windows Command Prompt window.</span></span>

## <a name="create-a-new-web-project"></a><span data-ttu-id="b9bf4-121">Skapa ett nytt webbprojekt</span><span class="sxs-lookup"><span data-stu-id="b9bf4-121">Create a new web project</span></span>

<span data-ttu-id="b9bf4-122">Navet bland .NET CLI-verktygen är drivrutinsverktyget *dotnet*.</span><span class="sxs-lookup"><span data-stu-id="b9bf4-122">The heart of the .NET CLI tools is the *dotnet* driver tool.</span></span> <span data-ttu-id="b9bf4-123">Med det här kommandot skapar du ett nytt ASP.NET Core-webbprojekt.</span><span class="sxs-lookup"><span data-stu-id="b9bf4-123">Using this command, you will create a new ASP.NET Core web project.</span></span>

<span data-ttu-id="b9bf4-124">För att skapa ett nytt ASP.NET Core MVC-program behöver du bara ange följande kommandon:</span><span class="sxs-lookup"><span data-stu-id="b9bf4-124">To create a new ASP.NET Core MVC application, you only need to type the following commands:</span></span>

```console
cd ~/Documents
mkdir BestBikeApp   # Hit Enter
cd BestBikeApp      # Hit Enter
dotnet new mvc      # Hit Enter
```

<span data-ttu-id="b9bf4-125">Med kommandona ovan navigerar du till rotmappen *Documents* och skapar sedan en ny mapp.</span><span class="sxs-lookup"><span data-stu-id="b9bf4-125">The above commands navigate to the *Documents* root folder, and then create a new folder.</span></span> <span data-ttu-id="b9bf4-126">Sedan kan du öppna den mappen.</span><span class="sxs-lookup"><span data-stu-id="b9bf4-126">Then, you go inside that folder.</span></span> <span data-ttu-id="b9bf4-127">Kör .NET CLI-kommandot för att generera ett nytt ASP.NET MVC-program med alla de paket återställda:</span><span class="sxs-lookup"><span data-stu-id="b9bf4-127">Finally, you issue the .NET CLI command to generate a new ASP.NET MVC application with all the packages restored:</span></span>

```console
The template "ASP.NET Core Web App (Model-View-Controller)" was created successfully.
This template contains technologies from parties other than Microsoft, see https://aka.ms/aspnetcore-template-3pn-210 for details.

Processing post-creation actions...
Running 'dotnet restore' on /home/your-user/Documents/BestBikeApp/BestBikeApp.csproj...
...
```

<span data-ttu-id="b9bf4-128">Allt du behöver göra nu är att köra appen genom att ange det här kommandot:</span><span class="sxs-lookup"><span data-stu-id="b9bf4-128">All you have to do now is run the application by issuing this command:</span></span>

```console
dotnet run
```

<span data-ttu-id="b9bf4-129">I *terminalen* visar *dotnet*-kommandot användbar information för den app som körs:</span><span class="sxs-lookup"><span data-stu-id="b9bf4-129">In the *terminal*, the *dotnet* command displays some useful information for the running app:</span></span>

```console
Using launch settings from /home/your-user/Documents/BestBikeApp/Properties/launchSettings.json...
...
Hosting environment: Development
Content root path: /home/your-user/Documents/BestBikeApp
Now listening on: https://localhost:5001
Now listening on: http://localhost:5000
Application started. Press Ctrl+C to shut down.
```

<span data-ttu-id="b9bf4-130">Utdata beskriver situationen efter att du har startat appen: programmet körs och lyssnar på port 5001 och 5002 (via HTTPS).</span><span class="sxs-lookup"><span data-stu-id="b9bf4-130">The output describes the situation after starting your app: the application is running and listening at port 5001 and 5002 (via HTTPS).</span></span>

<span data-ttu-id="b9bf4-131">För att kunna köra HTTPS lokalt på datorn i utvecklingsläge behöver du skapa och lita på ett **självsignerat certifikat**.</span><span class="sxs-lookup"><span data-stu-id="b9bf4-131">In order to run HTTPS locally on the machine in development mode, you need to create and trust a **self-signed certificate**.</span></span>

## <a name="create-a-self-signed-certificate"></a><span data-ttu-id="b9bf4-132">Skapa ett självsignerat certifikat</span><span class="sxs-lookup"><span data-stu-id="b9bf4-132">Create a self-signed certificate</span></span>

<span data-ttu-id="b9bf4-133">Kör kommandot nedan för att generera ett självsignerat certifikat för utveckling:</span><span class="sxs-lookup"><span data-stu-id="b9bf4-133">Run the command below to generate a development self-signed certificate:</span></span>

```console
dotnet dev-certs https -v
```

<span data-ttu-id="b9bf4-134">När kommandot körs returneras följande:</span><span class="sxs-lookup"><span data-stu-id="b9bf4-134">Running the command returns the following:</span></span>

```console
The HTTPS developer certificate was generated successfully.
```

## <a name="run-the-application"></a><span data-ttu-id="b9bf4-135">Köra programmet</span><span class="sxs-lookup"><span data-stu-id="b9bf4-135">Run the application</span></span>

<span data-ttu-id="b9bf4-136">I den här demonstrationen använder vi webbläsaren Firefox.</span><span class="sxs-lookup"><span data-stu-id="b9bf4-136">For this demonstration, we are using the Firefox browser.</span></span>

<span data-ttu-id="b9bf4-137">Öppna webbläsaren och ange adressen: `http://localhost:5001` för att kontrollera att programmet körs korrekt.</span><span class="sxs-lookup"><span data-stu-id="b9bf4-137">Open the browser and type in the address `http://localhost:5001` to verify the application is running successfully.</span></span>

![Skärmbild som visar en webbläsare med ASP.NET Core MVC-mallen för standardwebbsidan.](../media/5-asp-core-mvc-default-template.PNG)

> [!NOTE]
> <span data-ttu-id="b9bf4-139">Du måste **lägga till ett undantag** för programmets URL eftersom Firefox inte kunde verifiera det självsignerade certifikatet för utveckling.</span><span class="sxs-lookup"><span data-stu-id="b9bf4-139">You need to **add an exception** for the application's URL because the development self-signed certificate couldn't be verified by Firefox.</span></span>
