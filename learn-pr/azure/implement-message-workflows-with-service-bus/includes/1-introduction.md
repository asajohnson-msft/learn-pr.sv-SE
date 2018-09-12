<span data-ttu-id="fca64-101">Moderna program består ofta av flera delar som körs på separata datorer och enheter som finns på platser över hela världen.</span><span class="sxs-lookup"><span data-stu-id="fca64-101">Modern applications frequently consist of multiple parts running on separate computers and devices, which are in locations around the world.</span></span> <span data-ttu-id="fca64-102">Komplexa nätverk med olika tillförlitlighet och hastighet ligger ofta mellan dessa komponenter.</span><span class="sxs-lookup"><span data-stu-id="fca64-102">Complex networks with varying reliability and speed can be between these components.</span></span> <span data-ttu-id="fca64-103">En grundläggande utmaning med dessa distribuerade program är att kommunicera på ett tillförlitligt sätt mellan komponenterna.</span><span class="sxs-lookup"><span data-stu-id="fca64-103">A fundamental challenge with these distributed applications is how to communicate reliably between the components.</span></span>

<span data-ttu-id="fca64-104">Anta att du är en molnutvecklare för Contoso sektorer, en global pizzakedja.</span><span class="sxs-lookup"><span data-stu-id="fca64-104">Suppose you are a cloud developer for Contoso Slices, a global pizza delivery chain.</span></span> <span data-ttu-id="fca64-105">Din arbetsgivare håller på att uppgradera sin teknik så att användarna kan beställa från webben eller sina mobilappar.</span><span class="sxs-lookup"><span data-stu-id="fca64-105">Your employer is upgrading their technology so that users can place orders from the web or their mobile apps.</span></span> <span data-ttu-id="fca64-106">Beställningarna skickas till användarnas favoritrestaurang där pizzan lagas.</span><span class="sxs-lookup"><span data-stu-id="fca64-106">Those orders will be sent to the user's preferred storefront location, where employees will make the pizza.</span></span> <span data-ttu-id="fca64-107">Efter hand som degen rullas, pizzan läggs in ugnen, förpackas och levereras skickas uppdateringar till användarens mobilapp.</span><span class="sxs-lookup"><span data-stu-id="fca64-107">As the dough is rolled out, pizza put in oven, boxed, and put on a delivery vehicle, updates are sent to the user's mobile app.</span></span> <span data-ttu-id="fca64-108">Användaren får till och med platsuppdateringar när föraren kommer närmare.</span><span class="sxs-lookup"><span data-stu-id="fca64-108">The users even receive location updates as the delivery driver heads toward them.</span></span> 

<span data-ttu-id="fca64-109">Contoso Slice har tidigare skapat ett onlinesystem för att beställa pizza som lagrar beställningsdata i en SQL Server-databas.</span><span class="sxs-lookup"><span data-stu-id="fca64-109">Contoso Slice's previously created an online ordering system that immediately stored order data in a SQL Server database.</span></span> <span data-ttu-id="fca64-110">Varje butik var tvungen att komma ihåg att uppdatera ”webbeställningarna” manuellt för att se om de hade nya beställningar.</span><span class="sxs-lookup"><span data-stu-id="fca64-110">Each store had to remember to manually refresh the "web orders" page to find out if they had new orders.</span></span> <span data-ttu-id="fca64-111">Dessutom, när efterfrågan på pizza var stor, till exempel under sportevenemang, råkade systemet ofta ut för systemavbrott och fel.</span><span class="sxs-lookup"><span data-stu-id="fca64-111">In addition, during peak pizza times like televised sporting events, the system would frequently get deadlock exceptions and timeouts.</span></span> <span data-ttu-id="fca64-112">Slutligen saknade systemet ett centralt betalningssystem och stöd för statusuppdateringar för användaren.</span><span class="sxs-lookup"><span data-stu-id="fca64-112">Finally, the previous system lacked central payment processing or any kind of status updates for the user.</span></span>

<span data-ttu-id="fca64-113">För det här nya, mer ambitiösa projektet anlitade Contoso en molnarkitekt och planerar att använda en fristående arkitektur.</span><span class="sxs-lookup"><span data-stu-id="fca64-113">For this new, more ambitious project, Contoso hired a cloud architect and plans to use a decoupled architecture.</span></span> 

<span data-ttu-id="fca64-114">I den här modulen får vi lära dig hur Azure Service Bus kan hjälpa dig att skapa ett program som är tillförlitligt under belastning.</span><span class="sxs-lookup"><span data-stu-id="fca64-114">In this module we'll learn how Azure Service Bus can help build an application that stays reliable during peak demand.</span></span> <span data-ttu-id="fca64-115">Vi ska också se hur Azure Service Bus gör det enkelt att lägga till funktioner i våra program.</span><span class="sxs-lookup"><span data-stu-id="fca64-115">We'll also see how Azure Service Bus helps make it easy to add functionality to our applications.</span></span> <span data-ttu-id="fca64-116">Under resans gång kommer vi att använda C# för att omsätta lektionerna i praktiken.</span><span class="sxs-lookup"><span data-stu-id="fca64-116">Along the way, we'll be writing the C# code necessary to put these lessons to work.</span></span> <span data-ttu-id="fca64-117">Här får du se hur du kan använda ämnen och köer för Azure Service Bus i en distribuerad arkitektur för att säkerställa tillförlitlig kommunikation vid hög efterfrågan.</span><span class="sxs-lookup"><span data-stu-id="fca64-117">Here, you will see how to use Azure Service Bus topics and queues in a distributed architecture to ensure reliable communications even at times of high demand.</span></span> <span data-ttu-id="fca64-118">Du får också skriva C#-kod som kommunicerar via Service Bus.</span><span class="sxs-lookup"><span data-stu-id="fca64-118">You will also write C# code that communicates through Service Bus.</span></span>

## <a name="learning-objectives"></a><span data-ttu-id="fca64-119">Utbildningsmål</span><span class="sxs-lookup"><span data-stu-id="fca64-119">Learning objectives</span></span>

<span data-ttu-id="fca64-120">I den här modulen får du:</span><span class="sxs-lookup"><span data-stu-id="fca64-120">In is module, you will:</span></span>
- <span data-ttu-id="fca64-121">Välja om du vill använda Service Bus-köer, -ämnen eller -reläer för att kommunicera i ett distribuerat program</span><span class="sxs-lookup"><span data-stu-id="fca64-121">Choose whether to use Service Bus queues, topics, or relays to communicate in a distributed application</span></span>
- <span data-ttu-id="fca64-122">Konfigurera ett Azure Service Bus-namnområde i en Azure-prenumeration</span><span class="sxs-lookup"><span data-stu-id="fca64-122">Configure an Azure Service Bus namespace in an Azure subscription</span></span>
- <span data-ttu-id="fca64-123">Skapa ett Service Bus **-ämne** och använd det för att skicka och ta emot meddelanden</span><span class="sxs-lookup"><span data-stu-id="fca64-123">Create a Service Bus **topic** and use it to send and receive messages</span></span>
- <span data-ttu-id="fca64-124">Skapa en Service Bus **-kö** och använd den för att skicka och ta emot meddelanden</span><span class="sxs-lookup"><span data-stu-id="fca64-124">Create a Service Bus **queue** and use it to send and receive messages</span></span>