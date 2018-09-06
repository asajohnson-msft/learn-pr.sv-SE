<span data-ttu-id="45d37-101">Du har nu lagt till de klientbibliotek som behövs i appen och det har blivit dags att ansluta till ditt Azure Storage-konto.</span><span class="sxs-lookup"><span data-stu-id="45d37-101">You have added the required client libraries to your application and are ready to connect to your Azure Storage account.</span></span> <span data-ttu-id="45d37-102">Men hur kan appen känna av vilket konto den ska ansluta till och i vilken region lagringskontot finns?</span><span class="sxs-lookup"><span data-stu-id="45d37-102">However, how does your app know what account to connect to and what region that storage account exists in?</span></span> <span data-ttu-id="45d37-103">Utan konfiguration kan appen inte ansluta till något Azure Storage-konto.</span><span class="sxs-lookup"><span data-stu-id="45d37-103">Without appropriate configuration, your app will not know how to connect to your Azure Storage account.</span></span> 

<span data-ttu-id="45d37-104">I den här övningen ska du hitta anslutningsinformation om lagringskontot i Azure-portalen och lägga in den i din appkonfiguration så att appen kan ansluta till Azure Storage-kontot.</span><span class="sxs-lookup"><span data-stu-id="45d37-104">Here, you'll locate the storage account connection information in the Azure portal and place it into your application configuration so that your app is ready to connect to your Azure Storage account.</span></span>

## <a name="access-keys"></a><span data-ttu-id="45d37-105">Åtkomstnycklar</span><span class="sxs-lookup"><span data-stu-id="45d37-105">Access keys</span></span>

<span data-ttu-id="45d37-106">Varje lagringskonto har en uppsättning åtkomstnycklar som ger åtkomst till lagringskontot.</span><span class="sxs-lookup"><span data-stu-id="45d37-106">Each storage account has a set of access keys that allow access to the storage account.</span></span> <span data-ttu-id="45d37-107">Om din app behöver ansluta till flera lagringskonton måste appen ha en åtkomstnyckel för varje sådant lagringskonto.</span><span class="sxs-lookup"><span data-stu-id="45d37-107">If your app needs to connect to multiple storage accounts, then your app will require access keys for each storage account.</span></span>

![multiple accounts](..\media-draft\7-multiple-accounts.png)

<span data-ttu-id="45d37-109">Eftersom Azure är en molnleverantör behöver appen komplettera åtkomstnycklarna för autentisering till lagringskonton med information om lagringstjänstens slutpunkter som ger åtkomst till ditt lagringskonto via Internet.</span><span class="sxs-lookup"><span data-stu-id="45d37-109">Since Azure is a cloud provider, in addition to access keys for authentication to storage accounts, your app will need to know the storage service endpoints that provide access over the internet to your storage account.</span></span> <span data-ttu-id="45d37-110">Det enklaste sättet att hantera den här informationen är att använda en anslutningssträng till lagringskontot, där all den anslutningsinformation som behövs finns sparad i en enda textsträng.</span><span class="sxs-lookup"><span data-stu-id="45d37-110">The simplest way to handle this information is to use the storage account connection string, which contains all needed connectivity information in a single string.</span></span>

<span data-ttu-id="45d37-111">Anslutningssträngarna i Azure Storage ser ut ungefär som i exemplet nedan, men med åtkomstnyckeln och kontonamnet för ditt specifika lagringskonto angivet:</span><span class="sxs-lookup"><span data-stu-id="45d37-111">Azure Storage Connection strings look similar to the example below but with the access key and account name of your specific storage account:</span></span>

```csharp
DefaultEndpointsProtocol=https;AccountName={your-storage};AccountKey={your-access-key};EndpointSuffix=core.windows.net
```

## <a name="security"></a><span data-ttu-id="45d37-112">Säkerhet</span><span class="sxs-lookup"><span data-stu-id="45d37-112">Security</span></span>

<span data-ttu-id="45d37-113">Åtkomstnycklar ger åtkomst till ditt lagringskonto och du ska därför undvika att lämna ut dem till något system eller person som du inte vill ska ha tillgång till ditt lagringskonto.</span><span class="sxs-lookup"><span data-stu-id="45d37-113">Access keys are critical to providing access to your storage account and as a result, should not be given to any system or person that you do not wish to have access to your storage account.</span></span> <span data-ttu-id="45d37-114">Åtkomstnycklar har samma funktion som användarnamn och lösenord vid inloggning på en dator.</span><span class="sxs-lookup"><span data-stu-id="45d37-114">Access keys are the equivalent of a username and password to access your computer.</span></span>

![keys in vault](..\media-draft\8-keys-vault.png)

<span data-ttu-id="45d37-116">Anslutningsinformation för lagringskonton lagras vanligtvis i en miljövariabel, databas eller konfiguration.</span><span class="sxs-lookup"><span data-stu-id="45d37-116">Typically, storage account connectivity information is stored within an environment variable, database, or configuration file.</span></span>

<span data-ttu-id="45d37-117">Observera att det kan vara riskabelt att lagra den här informationen i en konfigurationsfil om du tänker inkludera samma fil i källkodskontrollen och lagra den på en offentlig lagringsplats.</span><span class="sxs-lookup"><span data-stu-id="45d37-117">It is important to note that storing this information in a configuration file can also be dangerous if you include that file in source control and store it in a public repository.</span></span> <span data-ttu-id="45d37-118">Det här är tyvärr ett misstag som många användare gör och som kan leda till att vem som helst kan läsa källkoden på den offentliga lagringsplatsen och hitta anslutningsinformationen till ditt lagringskonto.</span><span class="sxs-lookup"><span data-stu-id="45d37-118">This is a common mistake and means that anyone can browse your source code in the public repository and see your storage account connection information.</span></span>

<span data-ttu-id="45d37-119">Lagringskontona har en fristående autentiseringsmekanism med delade åtkomstsignaturer som har stöd för tidsbegränsade och avgränsade behörigheter i de fall där du vill ge andra personer begränsad tillgång.</span><span class="sxs-lookup"><span data-stu-id="45d37-119">Storage Accounts offer a separate authentication mechanism called Shared Access Signatures that support expiration and limited permissions for scenarios where you need to grant limited access.</span></span> <span data-ttu-id="45d37-120">Vi kommer inte att gå närmare in på det här, och det är heller inte något som du måste kunna för att klara av den här modulen, men mer information finns [här](https://docs.microsoft.com/en-us/azure/storage/common/storage-dotnet-shared-access-signature-part-1).</span><span class="sxs-lookup"><span data-stu-id="45d37-120">This topic will not be covered here and is not required knowledge for this module, however more information can be found [here](https://docs.microsoft.com/en-us/azure/storage/common/storage-dotnet-shared-access-signature-part-1).</span></span>

<span data-ttu-id="45d37-121">Varje lagringskonto har två åtkomstnycklar.</span><span class="sxs-lookup"><span data-stu-id="45d37-121">Each storage account has two access keys.</span></span> <span data-ttu-id="45d37-122">Anledningen till detta är att vi vill möjliggöra rotation (och regenerering) av nycklar med jämna mellanrum. Inkludera gärna metoden i ert interna regelverk för att skydda lagringskontona.</span><span class="sxs-lookup"><span data-stu-id="45d37-122">The reason for this is to allow keys to be rotated (regenerated) periodically as part of security best practice in keeping your storage account secure.</span></span> <span data-ttu-id="45d37-123">Den här processen kan köras från Azure-portalen eller kommandoradsgränssnittet (CLI).</span><span class="sxs-lookup"><span data-stu-id="45d37-123">This process can be done from the Azure portal or the CLI.</span></span>

<span data-ttu-id="45d37-124">Om du roterar en nyckel så ogiltigförklaras det ursprungliga nyckelvärdet omedelbart. Detta gör det lätt att återkalla behörigheten om någon obehörig kommit över nyckeln.</span><span class="sxs-lookup"><span data-stu-id="45d37-124">Rotating a key will invalidate the original key value immediately and will revoke access to anyone who obtained the key inappropriately.</span></span> <span data-ttu-id="45d37-125">Då det finns stöd för två nycklar kan du rotera nycklar utan driftstopp i apparna som använder nycklarna i fråga.</span><span class="sxs-lookup"><span data-stu-id="45d37-125">With support for two keys, you can rotate keys without causing downtime in your applications that use them.</span></span> <span data-ttu-id="45d37-126">Appen kan växla över till den alternativa åtkomstnyckeln medan den andra nyckeln regenereras.</span><span class="sxs-lookup"><span data-stu-id="45d37-126">Your app can switch to using the alternate access key, while the other key is regenerated.</span></span> <span data-ttu-id="45d37-127">Om lagringskontot används av flera appar bör samtliga appar använda samma nyckel i samband med att den här tekniken används.</span><span class="sxs-lookup"><span data-stu-id="45d37-127">If you have multiple apps using this storage account, they should all use the same key to support this technique.</span></span> <span data-ttu-id="45d37-128">Klicka [här](https://docs.microsoft.com/en-us/azure/storage/common/storage-create-storage-account#manage-your-storage-access-keys) för mer information.</span><span class="sxs-lookup"><span data-stu-id="45d37-128">See [here](https://docs.microsoft.com/en-us/azure/storage/common/storage-create-storage-account#manage-your-storage-access-keys) for more information.</span></span>

## <a name="advanced-security-options"></a><span data-ttu-id="45d37-129">Avancerade säkerhetsalternativ</span><span class="sxs-lookup"><span data-stu-id="45d37-129">Advanced security options</span></span>

<span data-ttu-id="45d37-130">Azure tillhandahåller lagring med hög säkerhet i form av tjänsten Azure Key Vault som specialutformats för att på ett säkert sätt lagra alla slags hemligheter såsom åtkomstnycklar, lösenord och certifikat.</span><span class="sxs-lookup"><span data-stu-id="45d37-130">Azure offers a high-grade security store called Azure Key Vault designed to securely store any form of secrets like access keys, passwords, or certificates.</span></span> <span data-ttu-id="45d37-131">Med hjälp av den här funktionen kan du på ett säkert sätt lagra dina åtkomstnycklar och få dem automatiskt roterade.</span><span class="sxs-lookup"><span data-stu-id="45d37-131">Using this feature, you can safely store your access keys and have them auto-rotated.</span></span>

<span data-ttu-id="45d37-132">Den här funktionen är överkurs för den här modulen, men om du vill veta mer kan du hitta mer information [här](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-ovw-storage-keys).</span><span class="sxs-lookup"><span data-stu-id="45d37-132">This feature is outside the scope of this module, but more information can be found [here](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-ovw-storage-keys)</span></span>

## <a name="summary"></a><span data-ttu-id="45d37-133">Sammanfattning</span><span class="sxs-lookup"><span data-stu-id="45d37-133">Summary</span></span>

<span data-ttu-id="45d37-134">Om du vill ansluta till ett Azure Storage-konto behöver du två saker.</span><span class="sxs-lookup"><span data-stu-id="45d37-134">To connect to an Azure Storage account, you need two things.</span></span> <span data-ttu-id="45d37-135">En åtkomstnyckel, som kan jämställas med ett användarnamn och ett lösenord och bör behandlas konfidentiellt.</span><span class="sxs-lookup"><span data-stu-id="45d37-135">An access key, which is similar to a username and password and should be kept confidential.</span></span> <span data-ttu-id="45d37-136">Du behöver också en slutpunkt för lagringstjänsten i form av en anslutningssträng.</span><span class="sxs-lookup"><span data-stu-id="45d37-136">You also need a storage service endpoint, which is represented by a connection string.</span></span>
