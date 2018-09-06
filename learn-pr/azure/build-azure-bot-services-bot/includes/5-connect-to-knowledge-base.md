### <a name="exercise-5-connect-the-bot-to-the-knowledge-base"></a><span data-ttu-id="a09ab-101">Övning 5: Ansluta chattroboten till kunskapsbasen</span><span class="sxs-lookup"><span data-stu-id="a09ab-101">Exercise 5: Connect the bot to the knowledge base</span></span>

<span data-ttu-id="a09ab-102">I den här övningen ansluter du din chattrobot till QnA Maker-kunskapsbasen du skapade tidigare, så att chattroboten kan föra en intelligent konversation.</span><span class="sxs-lookup"><span data-stu-id="a09ab-102">In this exercise, you will connect your bot to the QnA Maker knowledge base you built earlier so the bot can carry on an intelligent conversation.</span></span> <span data-ttu-id="a09ab-103">När du ansluter till kunskapsbasen hämtas en del information från QnA Maker-portalen. Den kopieras till Azure-portalen, chattrobotens kod uppdateras och sedan distribueras chattroboten till Azure igen.</span><span class="sxs-lookup"><span data-stu-id="a09ab-103">Connecting to the knowledge base involves retrieving some information from the QnA Maker portal, copying it into the Azure portal, updating the bot code, and then redeploying the bot to Azure.</span></span>

1. <span data-ttu-id="a09ab-104">Gå tillbaka till den [QnA Maker-portalen](https://www.qnamaker.ai/) och klicka på ditt namn i det övre högra hörnet.</span><span class="sxs-lookup"><span data-stu-id="a09ab-104">Return to the [QnA Maker portal](https://www.qnamaker.ai/) and click your name in the upper-right corner.</span></span> <span data-ttu-id="a09ab-105">Välj **Hantera slutpunktsnycklar** från listrutan.</span><span class="sxs-lookup"><span data-stu-id="a09ab-105">Select **Manage endpoint keys** from the menu that drops down.</span></span> <span data-ttu-id="a09ab-106">Klicka på **Visa** för att visa den primära slutpunktsnyckeln och på **Kopiera** för att kopiera den till Urklipp.</span><span class="sxs-lookup"><span data-stu-id="a09ab-106">Click **Show** to show the primary endpoint key, and **Copy** to copy it to the clipboard.</span></span> <span data-ttu-id="a09ab-107">Klistra sedan in den i en textfil så att du enkelt kan få tag på den om en stund.</span><span class="sxs-lookup"><span data-stu-id="a09ab-107">Then paste it into a text file so you can easily retrieve it in a moment.</span></span>

    ![Kopiera slutpunktsnyckeln](../images/copy-primary-key.png)
    
    <span data-ttu-id="a09ab-109">_Kopiera slutpunktsnyckeln_</span><span class="sxs-lookup"><span data-stu-id="a09ab-109">_Copying the endpoint key_</span></span> 

1. <span data-ttu-id="a09ab-110">Klicka på **Mina kunskapsbaser** i menyn längst upp på sidan.</span><span class="sxs-lookup"><span data-stu-id="a09ab-110">Click **My knowledge bases** in the menu at the top of the page.</span></span> <span data-ttu-id="a09ab-111">Klicka sedan på **Visa kod** för kunskapsbasen du skapade tidigare.</span><span class="sxs-lookup"><span data-stu-id="a09ab-111">Then click **View Code** for the knowledge base that you created earlier.</span></span>

    ![Öppna kunskapsbasen](../images/open-knowledge-base.png)

    <span data-ttu-id="a09ab-113">_Öppna kunskapsbasen_</span><span class="sxs-lookup"><span data-stu-id="a09ab-113">_Opening the knowledge base_</span></span>

1. <span data-ttu-id="a09ab-114">Kopiera kunskapsbasens ID från den första raden och värdnamnet från den andra raden. Klistra in dem i en textfil.</span><span class="sxs-lookup"><span data-stu-id="a09ab-114">Copy the knowledge base ID from the first line and the host name from the second line and paste them into a text file as well.</span></span> <span data-ttu-id="a09ab-115">Stäng sedan dialogrutan.</span><span class="sxs-lookup"><span data-stu-id="a09ab-115">Then close the dialog.</span></span> <span data-ttu-id="a09ab-116">Ta **inte** med prefixet ”https://” i värdnamnet du kopierar.</span><span class="sxs-lookup"><span data-stu-id="a09ab-116">**Do not** include the "https://" prefix in the host name that you copy.</span></span>

    ![Kopiera kunskapsbasens ID och värdnamn](../images/copy-endpoint-info.png)
    
    <span data-ttu-id="a09ab-118">_Kopiera kunskapsbasens ID och värdnamn_</span><span class="sxs-lookup"><span data-stu-id="a09ab-118">_Copying the knowledge base ID and host name_</span></span>  

1. <span data-ttu-id="a09ab-119">Återgå till din Web App Bot i Azure-portalen.</span><span class="sxs-lookup"><span data-stu-id="a09ab-119">Return to the Web App Bot in the Azure portal.</span></span> <span data-ttu-id="a09ab-120">Klicka på **Programinställningar** i menyn till vänster och rulla nedåt tills du hittar programinställningarna QnAKnowledgebaseId, QnAAuthKey och QnAEndpointHostName.</span><span class="sxs-lookup"><span data-stu-id="a09ab-120">Click **Application settings** in the menu on the left and scroll down until you find application settings named "QnAKnowledgebaseId," "QnAAuthKey,", and "QnAEndpointHostName."</span></span> <span data-ttu-id="a09ab-121">Klistra in kunskapsbasens ID och värdnamn från steg 3 och slutpunktsnyckeln från steg 1 i de här fälten.</span><span class="sxs-lookup"><span data-stu-id="a09ab-121">Paste the knowledge base ID and host name obtained in Step 3 and the endpoint key obtained in Step 1 into these fields.</span></span> <span data-ttu-id="a09ab-122">Klicka sedan på **Spara**.</span><span class="sxs-lookup"><span data-stu-id="a09ab-122">Then click **Save**.</span></span>

    ![Redigera programinställningar](../images/enter-app-settings.png)

    <span data-ttu-id="a09ab-124">_Redigera programinställningar_</span><span class="sxs-lookup"><span data-stu-id="a09ab-124">_Editing application settings_</span></span> 
 
1. <span data-ttu-id="a09ab-125">Gå tillbaka till Visual Studio Code och ersätt innehållet i **app.js** med koden nedan.</span><span class="sxs-lookup"><span data-stu-id="a09ab-125">Return to Visual Studio Code and replace the contents of **app.js** with the code below.</span></span> <span data-ttu-id="a09ab-126">Spara sedan filen.</span><span class="sxs-lookup"><span data-stu-id="a09ab-126">Then save the file.</span></span>

    ```JavaScript
    var restify = require('restify');
    var builder = require('botbuilder');
    var botbuilder_azure = require("botbuilder-azure");
    var builder_cognitiveservices = require("botbuilder-cognitiveservices");
    
    // Setup Restify Server
    var server = restify.createServer();
    server.listen(process.env.port || process.env.PORT || 3978, function () {
       console.log('%s listening to %s', server.name, server.url); 
    });
      
    // Create chat connector for communicating with the Bot Framework Service
    var connector = new builder.ChatConnector({
        appId: process.env.MicrosoftAppId,
        appPassword: process.env.MicrosoftAppPassword     
    });
    
    // Listen for messages from users 
    server.post('/api/messages', connector.listen());
     
    // Create your bot with a function to receive messages from the user
    var bot = new builder.UniversalBot(connector);
    
    var recognizer = new builder_cognitiveservices.QnAMakerRecognizer({
        knowledgeBaseId: process.env.QnAKnowledgebaseId, 
        authKey: process.env.QnAAuthKey,
        endpointHostName: process.env.QnAEndpointHostName
    });
    
    var basicQnAMakerDialog = new builder_cognitiveservices.QnAMakerDialog({
        recognizers: [recognizer],
        defaultMessage: "I'm not quite sure what you're asking. Please ask your question again.",
        qnaThreshold: 0.3
    });
    
    bot.dialog('basicQnAMakerDialog', basicQnAMakerDialog);
    
    bot.dialog('/',
    [
        function (session) {
            session.replaceDialog('basicQnAMakerDialog');
        }
    ]);
    ```

    <span data-ttu-id="a09ab-127">Notera anropet om att skapa en ```QnAMakerDialog```-instans på rad 30.</span><span class="sxs-lookup"><span data-stu-id="a09ab-127">Note the call to create a ```QnAMakerDialog``` instance on line 30.</span></span> <span data-ttu-id="a09ab-128">Det här skapar en dialogruta som integrerar en chattrobot som skapats med Azure Bot Service med en kunskapsbas som skapats med Microsoft QnA Maker.</span><span class="sxs-lookup"><span data-stu-id="a09ab-128">This creates a dialog that integrates a bot built with the Azure Bot Service with a knowledge base built Microsoft QnA Maker.</span></span>
 
1. <span data-ttu-id="a09ab-129">Klicka på knappen **Källkodskontroll** i aktivitetsfältet i Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="a09ab-129">Click the **Source Control** button in the activity bar in Visual Studio Code.</span></span> <span data-ttu-id="a09ab-130">Skriv ”Connected to knowledge base” i meddelanderutan och klicka på bockmarkeringen för att bekräfta ändringarna.</span><span class="sxs-lookup"><span data-stu-id="a09ab-130">Type "Connected to knowledge base" into the message box, and click the check mark to commit your changes.</span></span> <span data-ttu-id="a09ab-131">Klicka på ellipsen och använd kommandot **Publicera gren** till att skicka ändringarna till fjärrdatabasen (och därmed till Azure Web App).</span><span class="sxs-lookup"><span data-stu-id="a09ab-131">Then click the ellipsis and use the **Publish Branch** command to push these changes to the remote repository (and therefore to the Azure Web App).</span></span>

1. <span data-ttu-id="a09ab-132">Gå tillbaka till din Web App Bot i Azure-portalen och klicka på **Testa i webbchatt** till vänster för att öppna testkonsolen.</span><span class="sxs-lookup"><span data-stu-id="a09ab-132">Return to the Web App Bot in the Azure portal and click **Test in Web Chat** on the left to open the test console.</span></span> <span data-ttu-id="a09ab-133">Skriv ”What's the most popular software programming language in the world?”</span><span class="sxs-lookup"><span data-stu-id="a09ab-133">Type "What's the most popular software programming language in the world?"</span></span> <span data-ttu-id="a09ab-134">i fältet längst ned i chattfönstret och tryck på **Enter**.</span><span class="sxs-lookup"><span data-stu-id="a09ab-134">into the box at the bottom of the chat window and press **Enter**.</span></span> <span data-ttu-id="a09ab-135">Bekräfta att chattroboten svarar så här:</span><span class="sxs-lookup"><span data-stu-id="a09ab-135">Confirm that the bot responds as follows:</span></span>

    ![Testa chattroboten](../images/portal-testing-chat.png)

    <span data-ttu-id="a09ab-137">_Testa chattroboten_</span><span class="sxs-lookup"><span data-stu-id="a09ab-137">_Testing the bot_</span></span>

<span data-ttu-id="a09ab-138">Nu när roboten är ansluten till kunskapsbasen är det sista steget att testa den i verkligheten.</span><span class="sxs-lookup"><span data-stu-id="a09ab-138">Now that the bot is connected to the knowledge base, the final step is to test it in the wild.</span></span> <span data-ttu-id="a09ab-139">Och vad kan vara mer verkligt än att testa den med Skype?</span><span class="sxs-lookup"><span data-stu-id="a09ab-139">And what could be wilder than testing it with Skype?</span></span>