### <a name="exercise-3-train-a-tensorflow-model"></a><span data-ttu-id="dd25c-101">Övning 3: Träna en TensorFlow-modell</span><span class="sxs-lookup"><span data-stu-id="dd25c-101">Exercise 3: Train a TensorFlow model</span></span>

<span data-ttu-id="dd25c-102">I den här övningen kommer du att träna en bildklassificeringsmodell som byggts med [TensorFlow](https://www.tensorflow.org/) för att identifiera bilder som innehåller varmkorvar.</span><span class="sxs-lookup"><span data-stu-id="dd25c-102">In this exercise, you will train an image-classification model built with [TensorFlow](https://www.tensorflow.org/) to recognize images that contain hot dogs.</span></span> <span data-ttu-id="dd25c-103">I stället för att skapa modellen från grunden, vilket skulle kräva enorma mängder datorkraft och tiotusentals eller hundratusentals bilder kommer du att anpassa en befintlig modell. Det är en metod som kallas för [transfer learning](https://en.wikipedia.org/wiki/Transfer_learning), överförd inlärning.</span><span class="sxs-lookup"><span data-stu-id="dd25c-103">Rather than create the model from scratch, which would require vast amounts of computing power and tens or hundreds of thousands of images, you will customize a preexisting model, a practice known as [transfer learning](https://en.wikipedia.org/wiki/Transfer_learning).</span></span> <span data-ttu-id="dd25c-104">Med överförd inlärning kan du få hög precision efter bara ett par minuters träningstid på en vanlig bärbar eller stationär dator och med så lite som några dussin bilder.</span><span class="sxs-lookup"><span data-stu-id="dd25c-104">Transfer learning allows you to achieve high levels of accuracy with as little as a few minutes of training time on a typical laptop or PC and as few as several dozen images.</span></span>

<span data-ttu-id="dd25c-105">När det handlar om djupinlärning utgår överförd inlärning från ett djupt neuralt nätverk som har tränats för att utföra bildklassificering. Ett lager som anpassar nätverket efter din problemdomän läggs till; till exempel att dela upp bilder i två grupper: de som innehåller varmkorvar och de som inte gör det.</span><span class="sxs-lookup"><span data-stu-id="dd25c-105">In the context of deep learning, transfer learning involves starting with a deep neural network that is pretrained to perform image classification and adding a layer that customizes the network for your problem domain — for example, to classify images into two groups: those that contain hot dogs, and those that do not.</span></span> <span data-ttu-id="dd25c-106">Fler än 20 redan tränade TensorFlow-modeller för bildklassificering är tillgängliga i modellerna<https://github.com/tensorflow/models/tree/master/research/slim#pre-trained-models.> The [Inception](https://arxiv.org/abs/1512.00567) och [ResNet](https://towardsdatascience.com/an-overview-of-resnet-and-its-variants-5281e2f56035). Dessa kännetecknas av högre precision och följaktligen även större resursbehov. MobileNet-modellerna å andra sidan kompromissar när det gäller precision, men väger upp i format och energieffektivitet, och dessa har utvecklats med mobila enheter i åtanke.</span><span class="sxs-lookup"><span data-stu-id="dd25c-106">More than 20 pretrained TensorFlow image-classification models are available at <https://github.com/tensorflow/models/tree/master/research/slim#pre-trained-models.> The [Inception](https://arxiv.org/abs/1512.00567) and [ResNet](https://towardsdatascience.com/an-overview-of-resnet-and-its-variants-5281e2f56035) models are characterized by higher accuracy and commensurately higher resource requirements, while the MobileNet models trade accuracy for compactness and power efficiency and were developed with mobile devices in mind.</span></span> <span data-ttu-id="dd25c-107">Alla dessa modeller är välkända bland djupinlärningsexperter och de har använts vid ett antal tävlingar samt i verkliga program.</span><span class="sxs-lookup"><span data-stu-id="dd25c-107">All of these models are well known in the deep-learning community and have been used in a number of competitions as well as in real-world applications.</span></span> <span data-ttu-id="dd25c-108">Du kommer att använda en av MobileNet-modellerna som grund för ditt neurala nätverk för att uppnå en rimlig balans mellan precision och träningstid.</span><span class="sxs-lookup"><span data-stu-id="dd25c-108">You will use one of the MobileNet models as the basis for your neural network in order to strike a reasonable balance between accuracy and training time.</span></span>

<span data-ttu-id="dd25c-109">Att träna modellen kräver lite mer än att bara köra ett Python-skript som laddar ned basmodellen och lägger till ett lager som tränats med domänspecifika bilder och etiketter.</span><span class="sxs-lookup"><span data-stu-id="dd25c-109">Training the model involves little more than running a Python script that downloads the base model and adds a layer trained with domain-specific images and labels.</span></span> <span data-ttu-id="dd25c-110">Skriptet du behöver finns på GitHub och bilderna du kommer att använda sätts samman från tusentals matbilder från den offentliga domänen som finns på [Kaggle](https://www.kaggle.com).</span><span class="sxs-lookup"><span data-stu-id="dd25c-110">The script you need is available on GitHub, and the images you will use were assembled from thousands of public-domain food images available from [Kaggle](https://www.kaggle.com).</span></span>

1. <span data-ttu-id="dd25c-111">I Data Science VM klickar du på terminalikonen längst ned på skärmen för att öppna ett terminalfönster.</span><span class="sxs-lookup"><span data-stu-id="dd25c-111">In the Data Science VM, click the Terminal icon at the bottom of the screen to open a terminal window.</span></span>

    ![Öppna ett terminalfönster](../images/launch-terminal.png)

    <span data-ttu-id="dd25c-113">_Öppna ett terminalfönster_</span><span class="sxs-lookup"><span data-stu-id="dd25c-113">_Launching a terminal window_</span></span>

1. <span data-ttu-id="dd25c-114">Kör följande kommando i terminalfönstret för att navigera till mappen ”notebooks”:</span><span class="sxs-lookup"><span data-stu-id="dd25c-114">Execute the following command in the terminal window to navigate to the "notebooks" folder:</span></span>

    ```bash
    cd notebooks
    ```
    <span data-ttu-id="dd25c-115">Den här mappen innehåller redan exempel på Jupyter-anteckningsböcker som samlats ihop för DSVM.</span><span class="sxs-lookup"><span data-stu-id="dd25c-115">This folder is prepopulated with sample Jupyter notebooks curated for the DSVM.</span></span>

1. <span data-ttu-id="dd25c-116">Använd nu följande kommando för att klona lagringsplatsen för ”TensorFlow för Poets” från GitHub:</span><span class="sxs-lookup"><span data-stu-id="dd25c-116">Now use the following command to clone the "TensorFlow for Poets" repository from GitHub:</span></span>

    ```bash
    git clone https://github.com/googlecodelabs/tensorflow-for-poets-2
    ```
    > <span data-ttu-id="dd25c-117">**Tips**: Du kan kopiera den här raden till Urklipp och sedan använda **Skift + Ins** för att klistra in den i terminalfönstret.</span><span class="sxs-lookup"><span data-stu-id="dd25c-117">**Tip**: You can copy this line to the clipboard, and then use **Shift+Ins** to paste it into the terminal window.</span></span>

    <span data-ttu-id="dd25c-118">Den här lagringsplatsen innehåller skript för att skapa modeller för överförd inlärning, anropa en tränad modell för att kunna klassificera en bild och mycket mer.</span><span class="sxs-lookup"><span data-stu-id="dd25c-118">This repo contains scripts for creating transfer-learning models, invoking a trained model in order to classify an image, and more.</span></span> <span data-ttu-id="dd25c-119">Det är en del av [Google Codelabs](https://codelabs.developers.google.com/), som innehåller en mängd olika resurser och praktiska övningar för programutvecklare som vill lära sig mer om TensorFlow och andra Google-verktyg och API:er.</span><span class="sxs-lookup"><span data-stu-id="dd25c-119">It is part of [Google Codelabs](https://codelabs.developers.google.com/), which contains a variety of resources and hands-on labs for software developers interested in learning about TensorFlow and other Google tools and APIs.</span></span>

1. <span data-ttu-id="dd25c-120">När kloningen är avslutad navigerar du till mappen som innehåller den klonade modellen:</span><span class="sxs-lookup"><span data-stu-id="dd25c-120">Once cloning is complete, navigate to the folder containing the cloned model:</span></span>

    ```bash
    cd tensorflow-for-poets-2
    ```

1. <span data-ttu-id="dd25c-121">Du kan använda följande kommando för att ladda ned de bilder som du ska använda för att träna modellen:</span><span class="sxs-lookup"><span data-stu-id="dd25c-121">Use the following command to download the images that will be used to train the model:</span></span>

    ```bash
    wget https://topcs.blob.core.windows.net/public/tensorflow-resources.zip -O temp.zip; unzip temp.zip -d tf_files; rm temp.zip
    ```

    <span data-ttu-id="dd25c-122">Det här kommandot laddar ned en zip-fil som innehåller hundratals matbilder – hälften innehåller varmkorvar och den andra hälften gör det inte – och kopierar dem till undermappen som heter ”tf_files”.</span><span class="sxs-lookup"><span data-stu-id="dd25c-122">This command downloads a zip file containing hundreds of food images — half containing hot dogs, and half that do not — and copies them into the subdirectory named "tf_files."</span></span>

1. <span data-ttu-id="dd25c-123">Klicka på filhanteringsikonen längst ned på skärmen för att öppna ett fönster med filhanteraren.</span><span class="sxs-lookup"><span data-stu-id="dd25c-123">Click the File Manager icon at the bottom of the screen to open a File Manager window.</span></span>

    ![Starta filhanteraren](../images/launch-file-manager.png)

    <span data-ttu-id="dd25c-125">_Starta filhanteraren_</span><span class="sxs-lookup"><span data-stu-id="dd25c-125">_Launching File Manager_</span></span>

1. <span data-ttu-id="dd25c-126">I filhanteraren navigerar du till mappen ”notebooks/tensorflow-for-poets-2/tf_files”.</span><span class="sxs-lookup"><span data-stu-id="dd25c-126">In File Manager, navigate to the "notebooks/tensorflow-for-poets-2/tf_files" folder.</span></span> <span data-ttu-id="dd25c-127">Bekräfta att mappen innehåller underkatalogerna ”hot_dog” och ”not_hot_dog”.</span><span class="sxs-lookup"><span data-stu-id="dd25c-127">Confirm that the folder contains a pair of subdirectories named "hot_dog" and "not_hot_dog."</span></span> <span data-ttu-id="dd25c-128">Den förra innehåller flera hundra bilder som innehåller varmkorvar, medan den senare innehåller samma antal bilder som **inte** innehåller varmkorvar.</span><span class="sxs-lookup"><span data-stu-id="dd25c-128">The former contains several hundred images containing hot dogs, while the latter contains an equal number of images that do **not** contain hot dogs.</span></span> <span data-ttu-id="dd25c-129">Bläddra bland bilderna i mappen ”hot_dog” för att få en känsla för hur de ser ut.</span><span class="sxs-lookup"><span data-stu-id="dd25c-129">Browse the images in the "hot_dog" folder to get a feel for what they look like.</span></span> <span data-ttu-id="dd25c-130">Titta också på bilderna i mappen ”not_hot_dog”.</span><span class="sxs-lookup"><span data-stu-id="dd25c-130">Check out the images in the "not_hot_dog" folder as well.</span></span>

    > <span data-ttu-id="dd25c-131">För att träna ett neuralt nätverk så att det kan avgöra om en bild innehåller en varmkorv kommer du att träna det med bilder med och utan varmkorvar.</span><span class="sxs-lookup"><span data-stu-id="dd25c-131">In order to train a neural network to determine whether an image contains a hot dog, you will train it with images that contain hot dogs as well as images that do not contain hot dogs.</span></span>

    ![Bilder i mappen ”hot_dog”](../images/hot-dog-images.png)

    <span data-ttu-id="dd25c-133">*Bilder i mappen ”hot_dog”*</span><span class="sxs-lookup"><span data-stu-id="dd25c-133">*Images in the "hot_dog" folder*</span></span>

    <span data-ttu-id="dd25c-134">Bekräfta också att mappen innehåller en textfil med namnet **retrained_labels_hotdog.txt**.</span><span class="sxs-lookup"><span data-stu-id="dd25c-134">Also confirm that the folder contains a text file named **retrained_labels_hotdog.txt**.</span></span> <span data-ttu-id="dd25c-135">Den här filen identifierar underkatalogerna som innehåller träningsbilderna.</span><span class="sxs-lookup"><span data-stu-id="dd25c-135">This file identifies the subdirectories containing the training images.</span></span> <span data-ttu-id="dd25c-136">Den används av Python-skriptet som tränar modellen.</span><span class="sxs-lookup"><span data-stu-id="dd25c-136">It is used by the Python script that trains the model.</span></span> <span data-ttu-id="dd25c-137">Skriptet räknar filerna i varje underkatalog som identifierats i textfilen (textfilens namn är en parameter som skickas till skriptet) och använder de filerna för att träna nätverket.</span><span class="sxs-lookup"><span data-stu-id="dd25c-137">The script enumerates the files in each subdirectory identifed in the text file (the text file's name is a parameter passed to the script) and uses those files to train the network.</span></span>

1. <span data-ttu-id="dd25c-138">Öppna ett andra terminalfönster och navigera till mappen ”notebooks/tensorflow-for-poets-2” – samma mapp som är öppen i det första terminalfönstret.</span><span class="sxs-lookup"><span data-stu-id="dd25c-138">Open a second terminal window and navigate to the "notebooks/tensorflow-for-poets-2" folder — the same one that is open in the first terminal window.</span></span> <span data-ttu-id="dd25c-139">Använd sedan följande kommando för att starta [TensorBoard](https://www.tensorflow.org/programmers_guide/summaries_and_tensorboard), vilket är en uppsättning verktyg som används för att visualisera TensorFlow-modeller och få insyn i processen för överförd inlärning:</span><span class="sxs-lookup"><span data-stu-id="dd25c-139">Then use the following command to launch [TensorBoard](https://www.tensorflow.org/programmers_guide/summaries_and_tensorboard), which is a set of tools used to visualize TensorFlow models and gain insight into the transfer-learning process:</span></span>

     ```bash
     tensorboard --logdir tf_files/training_summaries
     ```

     > <span data-ttu-id="dd25c-140">Det här kommandot misslyckas om en instans av TensorBoard redan körs.</span><span class="sxs-lookup"><span data-stu-id="dd25c-140">This command will fail if there is already an instance of TensorBoard running.</span></span> <span data-ttu-id="dd25c-141">Om du får ett meddelande om att port 6006 redan används använder du ett ```pkill -f "tensorboard"```-kommando för att avsluta den befintliga processen.</span><span class="sxs-lookup"><span data-stu-id="dd25c-141">If you are notified that port 6006 is already in use, use a ```pkill -f "tensorboard"``` command to kill the existing process.</span></span> <span data-ttu-id="dd25c-142">Kör sedan kommandot ```tensorboard``` igen.</span><span class="sxs-lookup"><span data-stu-id="dd25c-142">Then execute the ```tensorboard``` command again.</span></span>

1. <span data-ttu-id="dd25c-143">Växla tillbaka till det ursprungliga terminalfönstret och kör följande kommandon:</span><span class="sxs-lookup"><span data-stu-id="dd25c-143">Switch back to the original terminal window and execute the following commands:</span></span>

    ```bash
    IMAGE_SIZE=224;
    ARCHITECTURE="mobilenet_0.50_${IMAGE_SIZE}";
    ```

    <span data-ttu-id="dd25c-144">Dessa kommandon initierar miljövariabler som anger upplösningen för träningsbilderna och basmodellen som det neurala nätverket byggs på.</span><span class="sxs-lookup"><span data-stu-id="dd25c-144">These commands initialize environment variables specifying the resolution of the training images and the base model that your neural network will build upon.</span></span> <span data-ttu-id="dd25c-145">Giltiga värden för IMAGE_SIZE är 128, 160, 192 och 224.</span><span class="sxs-lookup"><span data-stu-id="dd25c-145">Valid values for IMAGE_SIZE are 128, 160, 192, and 224.</span></span> <span data-ttu-id="dd25c-146">Högre värden ökar träningstiden, men ökar också precisionen för klassificeraren.</span><span class="sxs-lookup"><span data-stu-id="dd25c-146">Higher values increase the training time, but also increase the accuracy of the classifier.</span></span>

1. <span data-ttu-id="dd25c-147">Kör nu följande kommando för att starta processen för överförd inlärning – det vill säga för att träna modellen med bilderna du laddat ned:</span><span class="sxs-lookup"><span data-stu-id="dd25c-147">Now execute the following command to start the transfer-learning process — that is, to train the model with the images you downloaded:</span></span>

    ```bash
    python scripts/retrain.py \
    --bottleneck_dir=tf_files/bottlenecks \
    --how_many_training_steps=500 \
    --model_dir=tf_files/models/ \
    --summaries_dir=tf_files/training_summaries/"${ARCHITECTURE}" \
    --output_graph=tf_files/retrained_graph_hotdog.pb \
    --output_labels=tf_files/retrained_labels_hotdog.txt \
    --architecture="${ARCHITECTURE}" \
    --image_dir=tf_files \
    --testing_percentage=15 \
    --validation_percentage=15
    ```

    <span data-ttu-id="dd25c-148">**retrain.py** är ett av skripten på lagringsplatsen som du laddade ned.</span><span class="sxs-lookup"><span data-stu-id="dd25c-148">**retrain.py** is one of the scripts in the repo that you downloaded.</span></span> <span data-ttu-id="dd25c-149">Det är komplext och består av fler än 1 000 rader med kod och kommentarer.</span><span class="sxs-lookup"><span data-stu-id="dd25c-149">It is complex, comprising more than 1,000 lines of code and comments.</span></span> <span data-ttu-id="dd25c-150">Dess uppgift är att ladda ned den angivna modellen med ```--architecture```-växeln och lägga till ett nytt lager som tränats med bilderna i underkatalogerna för den katalog som angetts med ```--image_dir```-växeln.</span><span class="sxs-lookup"><span data-stu-id="dd25c-150">Its job is to download the model specified with the ```--architecture``` switch and add to it a new layer trained with the images found in subdirectories of the directory specified with the ```--image_dir``` switch.</span></span> <span data-ttu-id="dd25c-151">Varje bild är märkt med namnet på underkatalogen där den finns – i det här fallet ”hot_dog” eller ”not_hot_dog” – vilket gör det möjligt för det modifierade neurala nätverket att klassificera bilder som läggs till som bilder av varmkorvar (”hot_dog”) eller bilder som inte innehåller varmkorvar (”not_hot_dog”).</span><span class="sxs-lookup"><span data-stu-id="dd25c-151">Each image is labeled with the name of the subdirectory in which it is located — in this case, either "hot_dog" or "not_hot_dog" — enabling the modified neural network to classify images input to it as hot-dog images ("hot_dog") or not-hot-dog images ("not_hot_dog").</span></span> <span data-ttu-id="dd25c-152">Utdata från träningssessionen är en TensorFlow-modellfil med namnet **retrained_graph_hotdog.pb**.</span><span class="sxs-lookup"><span data-stu-id="dd25c-152">The output from the training session is a TensorFlow model file named **retrained_graph_hotdog.pb**.</span></span> <span data-ttu-id="dd25c-153">Namn och plats anges i ```--output_graph```-växeln.</span><span class="sxs-lookup"><span data-stu-id="dd25c-153">The name and location are specified in the ```--output_graph``` switch.</span></span>

1. <span data-ttu-id="dd25c-154">Vänta tills träningen har slutförts. Det bör ta mindre än fem minuter.</span><span class="sxs-lookup"><span data-stu-id="dd25c-154">Wait for training to complete; it should take less than 5 minutes.</span></span> <span data-ttu-id="dd25c-155">Kontrollera sedan resultatet för att fastställa hur exakt modellen är.</span><span class="sxs-lookup"><span data-stu-id="dd25c-155">Then check the output to determine the accuracy of the model.</span></span> <span data-ttu-id="dd25c-156">Resultaten kan variera något från det som visas nedan, eftersom träningsprocessen omfattar en liten mängd slumpmässiga uppskattningar.</span><span class="sxs-lookup"><span data-stu-id="dd25c-156">Your result may vary slightly from the one below because the training process involves a small amount of random estimation.</span></span>

      ![Mäta modellens precision](../images/running-transfer-learning.png)

      <span data-ttu-id="dd25c-158">_Mäta modellens precision_</span><span class="sxs-lookup"><span data-stu-id="dd25c-158">_Gauging the model's accuracy_</span></span>

1. <span data-ttu-id="dd25c-159">Klicka på webbläsarikonen längst ned på skrivbordet för att öppna webbläsaren som installerats på Data Science VM.</span><span class="sxs-lookup"><span data-stu-id="dd25c-159">Click the browser icon at the bottom of the desktop to open the browser installed in the Data Science VM.</span></span> <span data-ttu-id="dd25c-160">Navigera sedan till <http://0.0.0.0:6006> för att ansluta till Tensorboard.</span><span class="sxs-lookup"><span data-stu-id="dd25c-160">Then navigate to <http://0.0.0.0:6006> to connect to Tensorboard.</span></span>

    ![Starta Firefox](../images/launch-firefox.png)

    <span data-ttu-id="dd25c-162">_Starta Firefox_</span><span class="sxs-lookup"><span data-stu-id="dd25c-162">_Launching Firefox_</span></span>

1. <span data-ttu-id="dd25c-163">Granska diagrammet ”accuracy_1”.</span><span class="sxs-lookup"><span data-stu-id="dd25c-163">Inspect the graph labeled "accuracy_1."</span></span> <span data-ttu-id="dd25c-164">Den blå linjen visar precisionen som uppnåtts över tid efter det att de 500 träningsstegen som angetts med ```how_many_training_steps```-växeln utförts.</span><span class="sxs-lookup"><span data-stu-id="dd25c-164">The blue line depicts the accuracy achieved over time as the 500 training steps specified with the ```how_many_training_steps``` switch are executed.</span></span> <span data-ttu-id="dd25c-165">Det här mätvärdet är viktigt eftersom det visar hur modellens precision utvecklas i takt med att träningen fortskrider.</span><span class="sxs-lookup"><span data-stu-id="dd25c-165">This metric is important, because it shows how the accuracy of the model evolves as training progresses.</span></span> <span data-ttu-id="dd25c-166">Lika viktigt är avståndet mellan de blå och orangefärgade linjerna. De beräknar mängden överanpassning som sker och bör alltid minimeras.</span><span class="sxs-lookup"><span data-stu-id="dd25c-166">Equally important is the distance between the blue and orange lines, which quantifies the amount of overfitting that occurred and should always be minimized.</span></span> <span data-ttu-id="dd25c-167">[Överanpassning](https://en.wikipedia.org/wiki/Overfitting) innebär att modellen är bra på att klassificera bilderna den tränats med, men inte lika bra på att klassificera andra bilder som visas för den.</span><span class="sxs-lookup"><span data-stu-id="dd25c-167">[Overfitting](https://en.wikipedia.org/wiki/Overfitting) means the model is adept at classifying the images it was trained with, but not as adept at classifying other images presented to it.</span></span> <span data-ttu-id="dd25c-168">Resultaten här är godtagbara eftersom skillnaden är mindre än 10 % mellan den orangefärgade linjen (”träningsprecisionen” som uppnåtts med träningsbilderna) och den blå linjen (”valideringsprecisionen” som uppnåtts när modellen testats med bilder utanför träningsuppsättningen).</span><span class="sxs-lookup"><span data-stu-id="dd25c-168">The results here are acceptable, because there is a difference of less than 10% between the orange line (the "training" accuracy achieved with the training images) and the blue line (the "validation" accuracy achieved when tested with images outside the training set).</span></span>

    ![TensorBoard Scalars-vyn](../images/tensorboard-scalars.png)

    <span data-ttu-id="dd25c-170">_TensorBoard Scalars-vyn_</span><span class="sxs-lookup"><span data-stu-id="dd25c-170">_The TensorBoard Scalars display_</span></span>

1. <span data-ttu-id="dd25c-171">Klicka på **DIAGRAM** på TensorBoard-menyn och inspektera diagrammet som visas där.</span><span class="sxs-lookup"><span data-stu-id="dd25c-171">Click **GRAPHS** in the TensorBoard menu and inspect the graph shown there.</span></span> <span data-ttu-id="dd25c-172">Det primära syftet med det här diagrammet är att skildra det neurala nätverket och lagren som det består av.</span><span class="sxs-lookup"><span data-stu-id="dd25c-172">The primary purpose of this graph is to depict the neural network and the layers that comprise it.</span></span> <span data-ttu-id="dd25c-173">I det här exemplet är ”input_1” lagret som har tränats med matbilder och lagts till i nätverket.</span><span class="sxs-lookup"><span data-stu-id="dd25c-173">In this example, "input_1" is the layer that was trained with food images and added to the network.</span></span> <span data-ttu-id="dd25c-174">”MobilenetV1” är det neurala basnätverk som du utgick från.</span><span class="sxs-lookup"><span data-stu-id="dd25c-174">"MobilenetV1" is the base neural network that you started with.</span></span> <span data-ttu-id="dd25c-175">Det innehåller många lager som inte visas.</span><span class="sxs-lookup"><span data-stu-id="dd25c-175">It contains many layers which aren't shown.</span></span> <span data-ttu-id="dd25c-176">Om du hade skapat ett djupt neuralt nätverk från grunden skulle alla lager ingått i diagrammet här.</span><span class="sxs-lookup"><span data-stu-id="dd25c-176">Had you built a deep neural network from scratch, all of the layers would have been diagrammed here.</span></span> <span data-ttu-id="dd25c-177">(Om du vill se de lager som utgör MobileNet dubbelklickar du på blocket MobilenetV1 i diagrammet). Du hittar mer information om diagramvyn och den informationen som visas där i [TensorBoard: diagramvisualisering](https://www.tensorflow.org/programmers_guide/graph_viz).</span><span class="sxs-lookup"><span data-stu-id="dd25c-177">(If you would like to see the layers that comprise the MobileNet, double-click the "MobilenetV1" block in the diagram.) For more information on the Graphs display and the information surfaced there, refer to [TensorBoard: Graph Visualization](https://www.tensorflow.org/programmers_guide/graph_viz).</span></span>

    ![TensorBoard-diagramvyn](../images/tensorboard-graphs.png)

    <span data-ttu-id="dd25c-179">_TensorBoard-diagramvyn_</span><span class="sxs-lookup"><span data-stu-id="dd25c-179">_The TensorBoard Graphs display_</span></span>

1. <span data-ttu-id="dd25c-180">Återgå till filhanteraren och navigera till mappen ”notebooks/tensorflow-for-poets-2/tf_files”.</span><span class="sxs-lookup"><span data-stu-id="dd25c-180">Switch back to File Manager and navigate to the "notebooks/tensorflow-for-poets-2/tf_files" folder.</span></span> <span data-ttu-id="dd25c-181">Bekräfta att den innehåller en fil med namnet **retrained_graph_hotdog.pb**.</span><span class="sxs-lookup"><span data-stu-id="dd25c-181">Confirm that it contains a file named **retrained_graph_hotdog.pb**.</span></span> <span data-ttu-id="dd25c-182">*Den här filen skapades under träningsprocessen och innehåller den tränade TensorFlow-modellen*.</span><span class="sxs-lookup"><span data-stu-id="dd25c-182">*This file was created during the training process and contains the trained TensorFlow model*.</span></span> <span data-ttu-id="dd25c-183">Du använder den i nästa övning för att anropa modellen från appen NotHotDog.</span><span class="sxs-lookup"><span data-stu-id="dd25c-183">You will use it in the next exercise to invoke the model from the NotHotDog app.</span></span>

<span data-ttu-id="dd25c-184">Skriptet som du körde i steg 10 angav 500 träningssteg, vilket skapar en balans mellan precision och den tid som krävs för träningen.</span><span class="sxs-lookup"><span data-stu-id="dd25c-184">The script that you executed in Step 10 specified 500 training steps, which strikes a balance between accuracy and the time required for training.</span></span> <span data-ttu-id="dd25c-185">Om du vill kan du prova att träna modellen igen med ett högre ```how_many_training_steps```-värde, till exempel 1 000 eller 2 000.</span><span class="sxs-lookup"><span data-stu-id="dd25c-185">If you would like, try training the model again with a higher ```how_many_training_steps``` value such as 1000 or 2000.</span></span> <span data-ttu-id="dd25c-186">Ett högre antal steg resulterar vanligtvis i högre precision, men på bekostnad av ökad träningstid.</span><span class="sxs-lookup"><span data-stu-id="dd25c-186">A higher step count generally results in higher accuracy, but at the expense of increased training time.</span></span> <span data-ttu-id="dd25c-187">Se upp för överanpassning, vilket, som vi redan nämnt, framgår av skillnaden mellan den orangefärgade och den blå linjen i Tensorboard-vyn med skalaxlar.</span><span class="sxs-lookup"><span data-stu-id="dd25c-187">Watch out for overfitting, which, as a reminder, is represented by the difference between the orange and blue lines in TensorBoard's Scalars display.</span></span>