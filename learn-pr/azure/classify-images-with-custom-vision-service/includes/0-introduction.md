<span data-ttu-id="c667f-101">[Microsoft Cognitive Services](https://azure.microsoft.com/services/cognitive-services/ "Microsoft Cognitive Services") är en uppsättning tjänster och API:er som drivs med maskininlärning, och gör att utvecklare kan lägga till intelligenta funktioner som ansiktsigenkänning i foton och videor, analysera tonen i en text och bygga in språkförståelse i sina appar.</span><span class="sxs-lookup"><span data-stu-id="c667f-101">[Microsoft Cognitive Services](https://azure.microsoft.com/services/cognitive-services/ "Microsoft Cognitive Services") is a suite of services and APIs backed by machine learning that enables developers to incorporate intelligent features such as facial recognition in photos and videos, sentiment analysis in text, and language understanding into their applications.</span></span> <span data-ttu-id="c667f-102">Microsofts [Custom Vision Service](https://azure.microsoft.com/services/cognitive-services/custom-vision-service/) är en av de senaste medlemmarna i Cognitive Services-familjen.</span><span class="sxs-lookup"><span data-stu-id="c667f-102">The Microsoft [Custom Vision Service](https://azure.microsoft.com/services/cognitive-services/custom-vision-service/) is among the newest members of the Cognitive Services suite.</span></span> <span data-ttu-id="c667f-103">Det används till att skapa modeller för bildklassificering som ”lär sig” från taggade bilder som du tillhandahåller.</span><span class="sxs-lookup"><span data-stu-id="c667f-103">Its purpose is to create image classification models that "learn" from labeled images you provide.</span></span> <span data-ttu-id="c667f-104">Vill du veta om ett foto innehåller en bild av en blomma?</span><span class="sxs-lookup"><span data-stu-id="c667f-104">Want to know if a photo contains a picture of a flower?</span></span> <span data-ttu-id="c667f-105">Träna upp Custom Vision Service med en samling bilder av blommor. Sedan kan tjänsten avgörs om nästa bild du skickar innehåller en blomma, eller till om med vilken sorts blomma det är.</span><span class="sxs-lookup"><span data-stu-id="c667f-105">Train the Custom Vision Service with a collection of flower images, and it can tell you whether the next image includes a flower — or even what type of flower it is.</span></span>

### <a name="learning-objectives"></a><span data-ttu-id="c667f-106">Utbildningsmål</span><span class="sxs-lookup"><span data-stu-id="c667f-106">Learning objectives</span></span>

<span data-ttu-id="c667f-107">I den här modulen kommer du att göra följande:</span><span class="sxs-lookup"><span data-stu-id="c667f-107">In this module, you will:</span></span>

- <span data-ttu-id="c667f-108">Skapa ett Custom Vision Service-projekt.</span><span class="sxs-lookup"><span data-stu-id="c667f-108">Create a Custom Vision Service project.</span></span>
- <span data-ttu-id="c667f-109">Träna upp en Custom Vision Service-modell med taggade bilder.</span><span class="sxs-lookup"><span data-stu-id="c667f-109">Train a Custom Vision Service model with tagged images.</span></span>
- <span data-ttu-id="c667f-110">Testa en Custom Vision Service-modell.</span><span class="sxs-lookup"><span data-stu-id="c667f-110">Test a Custom Vision Service model.</span></span>
- <span data-ttu-id="c667f-111">Skapa appar där Custom Vision Service-modeller används genom anrop till REST-API:er.</span><span class="sxs-lookup"><span data-stu-id="c667f-111">Create apps that leverage Custom Vision Service models by calling REST APIs.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="c667f-112">Krav</span><span class="sxs-lookup"><span data-stu-id="c667f-112">Prerequisites</span></span>  

<!---TODO: Need links here and better verbiage--->
- <span data-ttu-id="c667f-113">Ett [Microsoft-konto](https://account.microsoft.com/account).</span><span class="sxs-lookup"><span data-stu-id="c667f-113">A [Microsoft account](https://account.microsoft.com/account).</span></span>
- <span data-ttu-id="c667f-114">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="c667f-114">Visual Studio Code</span></span>
- <span data-ttu-id="c667f-115">Node.js.</span><span class="sxs-lookup"><span data-stu-id="c667f-115">Node.js.</span></span>