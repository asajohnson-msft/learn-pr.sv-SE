![PyTorch-logotyp](../media/5-image1.png) 

<span data-ttu-id="52050-102">Vanligtvis brukar djupinlärningsingenjörerna inte implementera matrisalgebraoperationerna helt och hållet för hand.</span><span class="sxs-lookup"><span data-stu-id="52050-102">Typically deep learning engineers don't implement the matrix algebra operations all by hand.</span></span> <span data-ttu-id="52050-103">I stället använder de ramverk som PyTorch eller TensorFlow.</span><span class="sxs-lookup"><span data-stu-id="52050-103">Instead, they use frameworks such as PyTorch or TensorFlow.</span></span>  

<span data-ttu-id="52050-104">PyTorch är ett Python-baserat ramverk som ger flexibilitet som utvecklingsplattform för djupinlärning.</span><span class="sxs-lookup"><span data-stu-id="52050-104">PyTorch is a python-based framework that provides flexibility as a deep learning development platform.</span></span> <span data-ttu-id="52050-105">Det bygger på NumPy, biblioteket för vetenskaplig databehandling i Python.</span><span class="sxs-lookup"><span data-stu-id="52050-105">It's built on the Python scientific computing library, NumPy.</span></span> 

<span data-ttu-id="52050-106">Nu undrar du kanske varför vi ska använda PyTorch för att skapa modeller för djupinlärning?</span><span class="sxs-lookup"><span data-stu-id="52050-106">Now you might ask, why would we use PyTorch to build deep learning models?</span></span>  

- <span data-ttu-id="52050-107">Lättanvänt API – om du kan Python kommer du igång snabbt.</span><span class="sxs-lookup"><span data-stu-id="52050-107">Easy to use API – If you know Python, you can ramp up quickly.</span></span>
- <span data-ttu-id="52050-108">Stöd för Python – PyTorch integreras smidigt med stacken för vetenskaplig databehandling.</span><span class="sxs-lookup"><span data-stu-id="52050-108">Python support – PyTorch smoothly integrates with the scientific computing stack.</span></span>
- <span data-ttu-id="52050-109">Dynamiska beräkningsdiagram – i stället för fördefinierade diagram med specifika funktioner bygger PyTorch databaserade diagram dynamiskt, vilka kan ändras under körning.</span><span class="sxs-lookup"><span data-stu-id="52050-109">Dynamic computation graphs – Instead of predefined graphs with specific functionality, PyTorch builds computational graphs dynamically that can be modified during runtime.</span></span> <span data-ttu-id="52050-110">Dynamiska beräkningsdiagram är värdefulla för kapslad batchbearbetning och när vi inte vet hur mycket minne som krävs för att skapa ett visst nätverk.</span><span class="sxs-lookup"><span data-stu-id="52050-110">Dynamic computation graphs are valuable for nested batching and when we do not know how much memory will be needed for creating a given network.</span></span>

<span data-ttu-id="52050-111">Mer information om PyTorch finns i [den officiella dokumentationen på PyTorch.org](https://pytorch.org/about/).</span><span class="sxs-lookup"><span data-stu-id="52050-111">For more information about PyTorch, see [PyTorch.org official documentation](https://pytorch.org/about/).</span></span>

## <a name="run-your-first-pytorch-model"></a><span data-ttu-id="52050-112">Köra din första PyTorch-modell</span><span class="sxs-lookup"><span data-stu-id="52050-112">Run your first PyTorch model</span></span>

<span data-ttu-id="52050-113">Nu när du har en Docker-container som etablerats från en PyTorch-avbildning är det dags att experimentera.</span><span class="sxs-lookup"><span data-stu-id="52050-113">Now that you have a Docker container provisioned from a PyTorch image, it's time to experiment.</span></span> <span data-ttu-id="52050-114">Som du kanske kommer ihåg laddade vi ned en notebook från [python.org](https://python.org). Denna exempel-notebook vägleder dig genom att träna ett nätverk för att klassificera bilder i olika kategorier.</span><span class="sxs-lookup"><span data-stu-id="52050-114">If you recall, we downloaded a notebook from [python.org](https://python.org). That sample notebook walks you through training a network to classify images  into different categories.</span></span> <span data-ttu-id="52050-115">Det definierar ett djupt CNN (Convolutional Neural Network).</span><span class="sxs-lookup"><span data-stu-id="52050-115">It defines a deep Convolutional Neural Network (CNN).</span></span>

1. <span data-ttu-id="52050-116">Navigera i din lokala webbläsare till den Jupyter Notebook-server som du skapade i föregående övning.</span><span class="sxs-lookup"><span data-stu-id="52050-116">Navigate in your local browser to the Jupyter Notebook server that you set up in the last exercise.</span></span> <span data-ttu-id="52050-117">URL:en ska vara i formatet:</span><span class="sxs-lookup"><span data-stu-id="52050-117">The URL will be of the form:</span></span>

    `<HOSTNAME>.<REGION>.cloudapp.azure.com:8888/?token={sometoken}`

1. <span data-ttu-id="52050-118">Välj notebook `first_pytorch_classifier.ipynb` i instrumentpanelen.</span><span class="sxs-lookup"><span data-stu-id="52050-118">Select the `first_pytorch_classifier.ipynb` notebook in the dashboard.</span></span>

    ![välj the first_pytorch_classifier.ipynb](../media/5-image2.PNG)

    <span data-ttu-id="52050-120">Följ anvisningarna i anteckningsboken för att träna din första PyTorch-klassificerare.</span><span class="sxs-lookup"><span data-stu-id="52050-120">Follow the instructions in the notebook to train your first PyTorch classifier.</span></span>

    ![skärmbild av ”Träna en notebook-klassificerare”](../media/5-image3.PNG)

2. <span data-ttu-id="52050-122">Börja längst upp i notebook och kör varje cell i ordning.</span><span class="sxs-lookup"><span data-stu-id="52050-122">Start from the top of the notebook and run each cell in order.</span></span> <span data-ttu-id="52050-123">Observera följande:</span><span class="sxs-lookup"><span data-stu-id="52050-123">Note the following:</span></span>

    - <span data-ttu-id="52050-124">Vissa av cellerna tar lång tid att köra.</span><span class="sxs-lookup"><span data-stu-id="52050-124">Some of the cells take a long time to run.</span></span> <span data-ttu-id="52050-125">Notera den lilla punkten längst upp till höger i notebook intill orden ”Python 3”.</span><span class="sxs-lookup"><span data-stu-id="52050-125">Observe the small dot in the top right of the notebook beside the words "Python 3".</span></span> <span data-ttu-id="52050-126">När kerneln är upptagen med en åtgärd blir punkten en fylld, mörkare cirkel.</span><span class="sxs-lookup"><span data-stu-id="52050-126">When the kernel is busy with an operation, the dot becomes a filled, darker, circle.</span></span> <span data-ttu-id="52050-127">Den fortsätter se ut så tills åtgärden har slutförts.</span><span class="sxs-lookup"><span data-stu-id="52050-127">It remains that way until the operation is complete.</span></span> 
    - <span data-ttu-id="52050-128">Du tränar en CNN till att klassificera bilder.</span><span class="sxs-lookup"><span data-stu-id="52050-128">You're training a CNN to classify images.</span></span> <span data-ttu-id="52050-129">När nätverket har tränats kommer notebook att testa märkta bilder mot modellen.</span><span class="sxs-lookup"><span data-stu-id="52050-129">Once the network is trained, the notebook will test labeled images against the model.</span></span> <span data-ttu-id="52050-130">Den registrerar den förutsägelse som görs för varje bild och beräknar korrektheten i modellen.</span><span class="sxs-lookup"><span data-stu-id="52050-130">It records the prediction made for each image and calculates the accuracy of the model.</span></span> <span data-ttu-id="52050-131">Du ser resultaten i följande format.</span><span class="sxs-lookup"><span data-stu-id="52050-131">You'll see results in the following format.</span></span>

    ![Träningsresultat som visar korrektheten i modellen](../media/accuracy.png)
    
    - <span data-ttu-id="52050-133">Du kan läsa mer om notebook i [dokumentationen om PyTorch-självstudier](https://pytorch.org/tutorials/beginner/blitz/cifar10_tutorial.html) online.</span><span class="sxs-lookup"><span data-stu-id="52050-133">You can learn more about the notebook in the [PyTorch Tutorials documentation](https://pytorch.org/tutorials/beginner/blitz/cifar10_tutorial.html) online.</span></span>
    
    - <span data-ttu-id="52050-134">Vid slutet av notebook går anteckningarna igenom träning av en GPU.</span><span class="sxs-lookup"><span data-stu-id="52050-134">Towards the end of the notebook, the notes talk about training on a GPU.</span></span> <span data-ttu-id="52050-135">Om du har följt övningarna i den här modulen har du konfigurerat en CPU-baserad virtuell dator.</span><span class="sxs-lookup"><span data-stu-id="52050-135">If you followed the exercises in this module, you have set up a CPU-based VM.</span></span> <span data-ttu-id="52050-136">Detta går bra för en modell av den här storleken, och du ser kanske inte några betydande förbättringar i träningstid med en GPU.</span><span class="sxs-lookup"><span data-stu-id="52050-136">This is fine for a model this size and you may not see any significant improvements in training time with a GPU.</span></span> <span data-ttu-id="52050-137">Om du vill prova modulen med hjälp av en virtuell dator med GPU:er finns det två ändringar som du behöver göra:</span><span class="sxs-lookup"><span data-stu-id="52050-137">If you do want to try the module using a  virtual machine with GPUs, then there are two changes you need to make:</span></span>
    - <span data-ttu-id="52050-138">Etablera DSVM på en GPU-aktiverad VM-storlek i N-serien.</span><span class="sxs-lookup"><span data-stu-id="52050-138">Provision DSVM on a GPU enabled, N-series VM size.</span></span>
    - <span data-ttu-id="52050-139">Skapa en container med `nvidia-docker` i stället för `docker` i den föregående övningen.</span><span class="sxs-lookup"><span data-stu-id="52050-139">Create a container using `nvidia-docker` instead of `docker` in the previous exercise.</span></span>