<span data-ttu-id="be97a-101">Minne är den viktigaste resursen för Redis eftersom det är en minnesintern databas.</span><span class="sxs-lookup"><span data-stu-id="be97a-101">Memory is the most critical resource for Azure Redis Cache, because it's an in-memory database.</span></span> <span data-ttu-id="be97a-102">Du kan stöta på problem när du börjar lägga till data som överskrider mängden tillgängligt minne.</span><span class="sxs-lookup"><span data-stu-id="be97a-102">You can run into problems when you begin adding data that exceeds the amount of memory available.</span></span> <span data-ttu-id="be97a-103">Azure Redis Cache stöder borttagningsprinciper, som anger hur data ska hanteras när du får slut på minne.</span><span class="sxs-lookup"><span data-stu-id="be97a-103">Azure Redis Cache supports eviction policies, which indicate how data should be handled when you run out of memory.</span></span>

<span data-ttu-id="be97a-104">Här anger du en borttagningsprincip för att fastställa vad dina data ska vara när du överskrider den maximala mängden minne.</span><span class="sxs-lookup"><span data-stu-id="be97a-104">Here, you'll set an eviction policy to determine what your data should do when you exceed the maximum amount of memory.</span></span>

## <a name="what-is-an-eviction-policy"></a><span data-ttu-id="be97a-105">Vad är en borttagningsprincip?</span><span class="sxs-lookup"><span data-stu-id="be97a-105">What is an eviction policy?</span></span>

<span data-ttu-id="be97a-106">En borttagningsprincip är en plan som bestämmer hur dina data ska hanteras när du överskrider den maximala mängden tillgängligt minne.</span><span class="sxs-lookup"><span data-stu-id="be97a-106">An eviction policy is a plan that determines how your data should be managed when you exceed the maximum amount of memory available.</span></span> <span data-ttu-id="be97a-107">Genom att använda en borttagningsprincip kan du till exempel säga till Azure Redis Cache att ta bort en slumpmässig nyckel för att göra plats för nya data som infogas.</span><span class="sxs-lookup"><span data-stu-id="be97a-107">For example, using an eviction policy, you could tell Azure Redis Cache to delete a random key to make room for the new data being inserted.</span></span>

### <a name="types-of-eviction-policies"></a><span data-ttu-id="be97a-108">Typer av borttagningsprinciper</span><span class="sxs-lookup"><span data-stu-id="be97a-108">Types of eviction policies</span></span>

<span data-ttu-id="be97a-109">Det finns sex olika borttagningsprinciper som tillhandahålls av Azure Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="be97a-109">There are six different eviction policies provided by Azure Redis Cache.</span></span> <span data-ttu-id="be97a-110">Alla dessa värden utför en åtgärd när du försöker infoga data när minnesutrymmet är slut.</span><span class="sxs-lookup"><span data-stu-id="be97a-110">All of these values perform an action when you attempt to insert data when you're out of memory.</span></span>

* <span data-ttu-id="be97a-111">**noeviction:** ingen borttagningsprincip.</span><span class="sxs-lookup"><span data-stu-id="be97a-111">**noeviction:** No eviction policy.</span></span> <span data-ttu-id="be97a-112">Returnerar ett meddelanden om du försöker infoga data.</span><span class="sxs-lookup"><span data-stu-id="be97a-112">Returns an error message if you attempt to insert data.</span></span>

* <span data-ttu-id="be97a-113">**allkeys-lru:** tar bort den tidigast använda nyckeln.</span><span class="sxs-lookup"><span data-stu-id="be97a-113">**allkeys-lru:** Removes the least recently used key.</span></span>

* <span data-ttu-id="be97a-114">**allkeys-random:** tar bort en slumpmässig nyckel.</span><span class="sxs-lookup"><span data-stu-id="be97a-114">**allkeys-random:** Removes a random key.</span></span>

* <span data-ttu-id="be97a-115">**volatile-lru:** tar bort den tidigast använda nyckeln av alla nycklar med angiven förfallotid.</span><span class="sxs-lookup"><span data-stu-id="be97a-115">**volatile-lru:** Removes the least recently used key out of all the keys with an expiration set.</span></span>

* <span data-ttu-id="be97a-116">**volatile-ttl:** tar bort nyckeln med kortaste livslängd baserat på den angivna förfallotiden.</span><span class="sxs-lookup"><span data-stu-id="be97a-116">**volatile-ttl:** Removes the key with the shortest time to live based on the expiration set for it.</span></span>

* <span data-ttu-id="be97a-117">**volatile-random:** tar bort en slumpmässig nyckel som har en angiven förfallotid.</span><span class="sxs-lookup"><span data-stu-id="be97a-117">**volatile-random:** Removes a random key that has an expiration set.</span></span>

## <a name="how-to-set-an-eviction-policy"></a><span data-ttu-id="be97a-118">Så här anger du en borttagningsprincip</span><span class="sxs-lookup"><span data-stu-id="be97a-118">How to set an eviction policy</span></span>

<span data-ttu-id="be97a-119">Azure har en enkel nedrullningsbar meny för att ange borttagningsprincip för Azure Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="be97a-119">Azure provides a simple drop-down menu to set the eviction policy for Azure Redis Cache.</span></span> <span data-ttu-id="be97a-120">Välj **Avancerade inställningar** och använd listmenyn **maxmemory-policy**.</span><span class="sxs-lookup"><span data-stu-id="be97a-120">Select **Advanced Settings**, and use the **maxmemory-policy** drop-down menu.</span></span>

<span data-ttu-id="be97a-121">Eftersom minne är kritiskt för Azure Redis Cache så finns det stöd för borttagningsprinciper.</span><span class="sxs-lookup"><span data-stu-id="be97a-121">Since memory is critical to Azure Redis Cache, there is support for eviction policies.</span></span> <span data-ttu-id="be97a-122">En borttagningsprincip bestämmer vad som ska göras med befintliga data när minnesutrymmet är slut och du försöker infoga nya data.</span><span class="sxs-lookup"><span data-stu-id="be97a-122">An eviction policy determines what should be done with existing data when you're out of memory and attempt to insert new data.</span></span>