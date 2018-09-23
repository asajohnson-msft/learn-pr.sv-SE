<span data-ttu-id="254ec-101">Anta att ditt företag använder sig av containeravbildningar för att hantera beräkningsbelastningar.</span><span class="sxs-lookup"><span data-stu-id="254ec-101">Suppose your company makes use of container images to manage compute workloads.</span></span> <span data-ttu-id="254ec-102">Du kan använda de lokala Docker-verktygen till att bygga dina containeravbildningar.</span><span class="sxs-lookup"><span data-stu-id="254ec-102">You use the local Docker tooling to build your container images.</span></span>

<span data-ttu-id="254ec-103">Nu kan du skapa dina containrar med Azure Container Registry Build.</span><span class="sxs-lookup"><span data-stu-id="254ec-103">You can now use Azure Container Registry Build to build these containers.</span></span> <span data-ttu-id="254ec-104">I Container Registry Build kan du även integrera DevOps-processer med automatiserad kompilering när källkod checkas in.</span><span class="sxs-lookup"><span data-stu-id="254ec-104">Container Registry Build also allows for DevOps process integration with automated build on source code commit.</span></span>

<span data-ttu-id="254ec-105">Låt oss automatisera skapandet av en containeravbildning med Azure Container Registry Build.</span><span class="sxs-lookup"><span data-stu-id="254ec-105">Let's automate the creation of a container image using Azure Container Registry Build.</span></span>

## <a name="create-a-container-image-with-azure-container-registry-build"></a><span data-ttu-id="254ec-106">Skapa en containeravbildning med Azure Container Registry Build</span><span class="sxs-lookup"><span data-stu-id="254ec-106">Create a container image with Azure Container Registry Build</span></span>

<span data-ttu-id="254ec-107">En Docker-standardfil ger kompileringsinstruktioner.</span><span class="sxs-lookup"><span data-stu-id="254ec-107">A standard Dockerfile to provides build instructions.</span></span> <span data-ttu-id="254ec-108">I Azure Container Registry Build kan du återanvända valfri Docker-fil som finns i din miljö, inklusive kompileringar i flera steg.</span><span class="sxs-lookup"><span data-stu-id="254ec-108">Azure Container Registry Build allows you to reuse any Dockerfile currently in your environment, including multi-staged builds.</span></span>

<span data-ttu-id="254ec-109">Vi använder en ny Docker-fil i vårt exempel.</span><span class="sxs-lookup"><span data-stu-id="254ec-109">We'll use a new Dockerfile for our example.</span></span> 

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

<span data-ttu-id="254ec-110">Det första steget är att skapa en ny fil med namnet `Dockerfile`.</span><span class="sxs-lookup"><span data-stu-id="254ec-110">The first step is to create a new file named `Dockerfile`.</span></span> <span data-ttu-id="254ec-111">Du kan redigera filen i valfri textredigerare.</span><span class="sxs-lookup"><span data-stu-id="254ec-111">You can use any text editor to edit the file.</span></span> <span data-ttu-id="254ec-112">Vi använder Cloud Shell Editor i det här exemplet.</span><span class="sxs-lookup"><span data-stu-id="254ec-112">We'll use Cloud Shell Editor for this example.</span></span> <span data-ttu-id="254ec-113">Öppna redigeringsprogrammet genom att ange följande kommando i Cloud Shell-fönstret.</span><span class="sxs-lookup"><span data-stu-id="254ec-113">Enter the following command into the Cloud Shell window to open the editor.</span></span>

```bash
code
```

<span data-ttu-id="254ec-114">Kopiera följande innehåll till din nya Docker-fil.</span><span class="sxs-lookup"><span data-stu-id="254ec-114">Copy the following contents to your new Dockerfile.</span></span> <span data-ttu-id="254ec-115">Var noga med att spara filen.</span><span class="sxs-lookup"><span data-stu-id="254ec-115">Make sure to save the file.</span></span> 

```bash
FROM    node:9-alpine
ADD     https://raw.githubusercontent.com/Azure-Samples/acr-build-helloworld-node/master/package.json /
ADD     https://raw.githubusercontent.com/Azure-Samples/acr-build-helloworld-node/master/server.js /
RUN     npm install
EXPOSE  80
CMD     ["node", "server.js"]
```

<span data-ttu-id="254ec-116">Spara genom att använda tangentkombinationen <kbd>Ctrl+S</kbd>.</span><span class="sxs-lookup"><span data-stu-id="254ec-116">Use the key combination <kbd>Ctrl+S</kbd> to save.</span></span> <span data-ttu-id="254ec-117">Ge filen namnet `Dockerfile` när du tillfrågas.</span><span class="sxs-lookup"><span data-stu-id="254ec-117">Name the file `Dockerfile` when prompted.</span></span>

<span data-ttu-id="254ec-118">Den här konfigurationen lägger till ett Node.js-program i `node:9-alpine`-avbildningen.</span><span class="sxs-lookup"><span data-stu-id="254ec-118">This configuration adds a Node.js application to the `node:9-alpine` image.</span></span> <span data-ttu-id="254ec-119">Därefter konfigureras containern för att leverera programmet via port 80 med instruktionen *EXPOSE*.</span><span class="sxs-lookup"><span data-stu-id="254ec-119">After that, it configures the container to serve the application on port 80 via the *EXPOSE* instruction.</span></span>

<span data-ttu-id="254ec-120">Skapa nu containeravbildningen från Docker-filen genom att köra Azure CLI-kommandot `az acr build`.</span><span class="sxs-lookup"><span data-stu-id="254ec-120">Now run the Azure CLI command `az acr build` to build the container image from the Dockerfile.</span></span>

```azurecli
az acr build --registry <acrName> --image helloacrbuild:v1 .
```

<span data-ttu-id="254ec-121">När det här kommandot körs ser du att avbildningen skapas och push-överförs till ditt containerregister.</span><span class="sxs-lookup"><span data-stu-id="254ec-121">You'll see the image being built and pushed to your Container Registry as you run the command.</span></span>

## <a name="verify-the-image"></a><span data-ttu-id="254ec-122">Verifiera avbildningen</span><span class="sxs-lookup"><span data-stu-id="254ec-122">Verify the image</span></span>

<span data-ttu-id="254ec-123">Kör följande kommando för att verifiera att avbildningen har skapats och lagrats i registret.</span><span class="sxs-lookup"><span data-stu-id="254ec-123">Run the following command to verify that the image has been created and stored in the registry.</span></span>

```azurecli
az acr repository list --name <acrName> --output table
```

<span data-ttu-id="254ec-124">Utdata bör se ut ungefär så här:</span><span class="sxs-lookup"><span data-stu-id="254ec-124">The output should look similar to the following:</span></span>

```console
Result
-------------
helloacrbuild
```

<span data-ttu-id="254ec-125">Avbildningen `helloacrbuild` är nu redo att användas.</span><span class="sxs-lookup"><span data-stu-id="254ec-125">The `helloacrbuild` image is now ready to be used.</span></span>