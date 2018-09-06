### <a name="exercise-6-use-the-app-to-classify-images"></a><span data-ttu-id="82bdd-101">Övning 6: Använda appen för att klassificera bilder</span><span class="sxs-lookup"><span data-stu-id="82bdd-101">Exercise 6: Use the app to classify images</span></span>

<span data-ttu-id="82bdd-102">I den här övningen ska du använda appen Artworks för att skicka in bilder till Custom Vision Service och få dem klassificerade.</span><span class="sxs-lookup"><span data-stu-id="82bdd-102">In this exercise, you will use the Artworks app to submit images to the Custom Vision Service for classification.</span></span> <span data-ttu-id="82bdd-103">Appen använder JSON-information som returneras från metoden [PredictImage](https://southcentralus.dev.cognitive.microsoft.com/docs/services/eb68250e4e954d9bae0c2650db79c653/operations/58acd3c1ef062f0344a42814) i Custom Visions Prediction-API för att avgöra om en bild föreställer en tavla målad av Picasso, Rembrandt, Pollock – eller ingen av dessa.</span><span class="sxs-lookup"><span data-stu-id="82bdd-103">The app uses the JSON information returned from calls to the Custom Vision Prediction API's [PredictImage](https://southcentralus.dev.cognitive.microsoft.com/docs/services/eb68250e4e954d9bae0c2650db79c653/operations/58acd3c1ef062f0344a42814) method to tell you whether an image represents a painting by Picasso, Rembrandt, Pollock, or none of the above.</span></span> <span data-ttu-id="82bdd-104">Den visar också sannolikheten för att klassificeringen är korrekt.</span><span class="sxs-lookup"><span data-stu-id="82bdd-104">It also shows the probability that the classification assigned to the image is correct.</span></span>

1. <span data-ttu-id="82bdd-105">Klicka på knappen **Browse (...)** (Bläddra (...)) i appen Artworks.</span><span class="sxs-lookup"><span data-stu-id="82bdd-105">Click the **Browse (...)** button in the Artworks app.</span></span> 

    ![Bläddra efter lokala bilder i appen Artworks](../images/app-click-browse.png)

    <span data-ttu-id="82bdd-107">_Bläddra efter lokala bilder i appen Artworks_</span><span class="sxs-lookup"><span data-stu-id="82bdd-107">_Browsing for local images in the Artworks app_</span></span> 

1. <span data-ttu-id="82bdd-108">Bläddra till mappen Quick Tests (Snabbtest) bland labbresurserna.</span><span class="sxs-lookup"><span data-stu-id="82bdd-108">Browse to the "Quick Tests" folder in the lab resources.</span></span> <span data-ttu-id="82bdd-109">Välj en fil som heter **PicassoTest_02.jpg** och klicka sedan på **Öppna**.</span><span class="sxs-lookup"><span data-stu-id="82bdd-109">Select the file named **PicassoTest_02.jpg**, and then click **Open**.</span></span>

1. <span data-ttu-id="82bdd-110">Klicka på knappen **Predict** (Förutsäg) för att skicka bilden till Custom Vision Service.</span><span class="sxs-lookup"><span data-stu-id="82bdd-110">Click the **Predict** button to submit the image to the Custom Vision Service.</span></span>

    ![Skicka bilden till Custom Vision Service](../images/app-click-predict.png)

    <span data-ttu-id="82bdd-112">_Skicka bilden till Custom Vision Service_</span><span class="sxs-lookup"><span data-stu-id="82bdd-112">_Submitting the image to the Custom Vision Service_</span></span> 

1. <span data-ttu-id="82bdd-113">Kontrollera att appen identifierar tavlan som en målning av Picasso.</span><span class="sxs-lookup"><span data-stu-id="82bdd-113">Confirm that the app identifies the painting as a Picasso.</span></span>

    ![Klassificera en bild som en Picasso](../images/app-prediction-01.png)

    <span data-ttu-id="82bdd-115">_Klassificera en bild som en Picasso_</span><span class="sxs-lookup"><span data-stu-id="82bdd-115">_Classifying an image as a Picasso_</span></span> 

1. <span data-ttu-id="82bdd-116">Upprepa steg 1 till 3 för **RembrandtTest_01.jpg** och **PollockTest_01.jpg** och kontrollera att appen identifierar dessa som konstverk målade av Rembrandt och Pollock.</span><span class="sxs-lookup"><span data-stu-id="82bdd-116">Repeat steps 1 through 3 for **RembrandtTest_01.jpg** and **PollockTest_01.jpg** and confirm that the app can identify paintings by Rembrandt and Pollock.</span></span>

    ![Klassificera en bild som en Rembrandt](../images/app-prediction-02.png)

    <span data-ttu-id="82bdd-118">_Klassificera en bild som en Rembrandt_</span><span class="sxs-lookup"><span data-stu-id="82bdd-118">_Classifying an image as a Rembrandt_</span></span> 

1. <span data-ttu-id="82bdd-119">Upprepa steg 1 till 3 för **VanGoghTest_01.png** och **VanGoghTest_02.png** och kontrollera att appen inte identifierar dessa som konstverk målade av Picasso, Rembrandt eller Pollock.</span><span class="sxs-lookup"><span data-stu-id="82bdd-119">Repeat steps 1 through 3 for **VanGoghTest_01.png** and **VanGoghTest_02.png** and confirm that the app does not identify these Van Gogh masterworks as paintings by Picasso, Rembrandt, or Pollock.</span></span>

    ![Inte Picasso, Rembrandt eller Pollock](../images/app-prediction-03.png)

    <span data-ttu-id="82bdd-121">_Inte Picasso, Rembrandt eller Pollock_</span><span class="sxs-lookup"><span data-stu-id="82bdd-121">_Not a Picasso, Rembrandt, or Pollock_</span></span> 

1. <span data-ttu-id="82bdd-122">Som du ser är tillförlitligheten lika stor när du använder Prediction-API:t i appen som när du går via Custom Vision Service-portalen. Men det är roligare att använda appen!</span><span class="sxs-lookup"><span data-stu-id="82bdd-122">As you can see, using the Prediction API from an app is as reliable as through the Custom Vision Service portal — and way more fun!</span></span> <span data-ttu-id="82bdd-123">Om du går till sidan Predictions (Förutsägelser) i portalen hittar du alla bilder som laddades upp i appen där med.</span><span class="sxs-lookup"><span data-stu-id="82bdd-123">What's more, if you go to the Predictions page in the portal, you'll find each of the images uploaded via the app shown there as well.</span></span>
 
    ![Bild som skickats till Custom Vision Service](../images/portal-all-predictions.png)

    <span data-ttu-id="82bdd-125">_Bild som skickats till Custom Vision Service_</span><span class="sxs-lookup"><span data-stu-id="82bdd-125">_image submitted to the Custom Vision Service_</span></span> 

<span data-ttu-id="82bdd-126">Passa på att experimentera med egna bilder och testa modellens förmåga att identifiera olika konstnärer eller bara att avgöra att en bild inte målats av Picasso, Rembrandt eller Pollock.</span><span class="sxs-lookup"><span data-stu-id="82bdd-126">Feel free to test with images of your own and gauge the model's adeptness at identifying artists or determining that an image is not a Picasso, Rembrandt, or Pollock.</span></span> <span data-ttu-id="82bdd-127">Om du vill att modellen även ska kunna känna igen målningar av Van Gogh laddar du upp några Van Gogh-bilder, taggar dem som ”Van Gogh” och tränar om modellen.</span><span class="sxs-lookup"><span data-stu-id="82bdd-127">If you'd like to train it to recognize Van Goghs, too, upload some Van Gogh paintings, tag them with "Van Gogh," and retrain the model.</span></span> <span data-ttu-id="82bdd-128">Det finns ingen gräns för hur mycket intelligens du kan tillföra – bara du är villig och har tid till att utföra träningen.</span><span class="sxs-lookup"><span data-stu-id="82bdd-128">There is no limit to the intelligence you can add if you're willing to do the training.</span></span> <span data-ttu-id="82bdd-129">Kom ihåg att ju fler bilder du tränar modellen med, desto smartare blir den.</span><span class="sxs-lookup"><span data-stu-id="82bdd-129">And remember that in general, the more images you train with, the smarter the model will be.</span></span>