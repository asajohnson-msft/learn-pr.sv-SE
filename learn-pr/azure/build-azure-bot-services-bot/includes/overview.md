<span data-ttu-id="5235f-101">[Azure Bot Service](https://azure.microsoft.com/en*us/services/bot*service/) kan kombineras med [Microsoft QnA Maker](https://www.qnamaker.ai/) för att ge utvecklarna tillgång till verktyg som kan användas till att skapa och publicera intelligenta robotar som interagerar på ett naturligt sätt med användarna på en rad olika enheter.</span><span class="sxs-lookup"><span data-stu-id="5235f-101">The [Azure Bot Service](https://azure.microsoft.com/en*us/services/bot*service/), combined with [Microsoft QnA Maker](https://www.qnamaker.ai/), provide the tools developers need to build and publish intelligent bots that interact naturally with users using a range of services.</span></span> <span data-ttu-id="5235f-102">I den här labbuppgiften får du lära dig att skapa en robot med Azure Bot Service och ansluta den till en kunskapsbas som sammanställts med QnA Maker.</span><span class="sxs-lookup"><span data-stu-id="5235f-102">In this lab, you will create a bot using the Azure Bot Service and connect it to a knowledge base built with QnA Maker.</span></span> <span data-ttu-id="5235f-103">Därefter kan du interagera med roboten via Skype, en av många populära tjänster som är kompatibla med robotar som skapats med hjälp av Azure Bot Service.</span><span class="sxs-lookup"><span data-stu-id="5235f-103">Then you will interact with the bot using Skype — one of many popular services with which bots built with the Azure Bot Service can integrate.</span></span>

### <a name="whats-covered-in-this-lab"></a><span data-ttu-id="5235f-104">Vad tar vi upp i den här labbuppgiften?</span><span class="sxs-lookup"><span data-stu-id="5235f-104">What's covered in this lab?</span></span>
<span data-ttu-id="5235f-105">I den här labbuppgiften kommer du att göra följande:</span><span class="sxs-lookup"><span data-stu-id="5235f-105">In this lab, you will</span></span>
* <span data-ttu-id="5235f-106">Skapa en Azure Web App-robot som kan vara värd för en robot</span><span class="sxs-lookup"><span data-stu-id="5235f-106">Create an Azure Web App Bot to host a bot</span></span>
* <span data-ttu-id="5235f-107">Skapa en kunskapsbas, fylla den med data och ansluta den till en robot</span><span class="sxs-lookup"><span data-stu-id="5235f-107">Create a knowledge base, populate it with data, and connect it to a bot</span></span>
* <span data-ttu-id="5235f-108">Implementera robotar i koden och felsöka de robotar som du skapar</span><span class="sxs-lookup"><span data-stu-id="5235f-108">Implement bots in code and debug the bots that you build</span></span>
* <span data-ttu-id="5235f-109">Publicera robotar och använda kontinuerlig integrering för att hålla dem uppdaterade</span><span class="sxs-lookup"><span data-stu-id="5235f-109">Publish bots and use continuous integration to keep them up to date</span></span>
* <span data-ttu-id="5235f-110">Felsöka robotar lokalt med hjälp av Visual Studio Code och Microsoft Bot Framework-emulatorn</span><span class="sxs-lookup"><span data-stu-id="5235f-110">Debug bots locally using Visual Studio Code and the Microsoft Bot Framework Emulator</span></span>
* <span data-ttu-id="5235f-111">Ansluta en robot till Skype och interagera med den</span><span class="sxs-lookup"><span data-stu-id="5235f-111">Plug a bot into Skype and interact with it there</span></span>

<span data-ttu-id="5235f-112">För att kunna göra den här labbuppgiften behöver du en aktiv Azure-prenumeration.</span><span class="sxs-lookup"><span data-stu-id="5235f-112">In order to complete this lab you will need an active Microsoft Azure subscription.</span></span> <span data-ttu-id="5235f-113">Om du inte har någon kan du registrera dig för en [kostnadsfri utvärderingsversion](http://aka.ms/WATK-FreeTrial).</span><span class="sxs-lookup"><span data-stu-id="5235f-113">If you don't have one, [sign up for a free trial](http://aka.ms/WATK-FreeTrial).</span></span> <span data-ttu-id="5235f-114">Du behöver även [Visual Studio Code](http://code.visualstudio.com), [Git](https://git-scm.com), [Microsoft Bot Framework-emulatorn](https://emulator.botframework.com/), [Node.js](https://nodejs.org) och [Skype ](https://www.skype.com/en/download-skype/skype-for-computer/).</span><span class="sxs-lookup"><span data-stu-id="5235f-114">You will also need, [Visual Studio Code](http://code.visualstudio.com), [Git](https://git-scm.com), the [Microsoft Bot Framework Emulator](https://emulator.botframework.com/), [Node.js](https://nodejs.org), and [Skype](https://www.skype.com/en/download-skype/skype-for-computer/).</span></span>