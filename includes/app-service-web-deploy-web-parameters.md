<span data-ttu-id="ec60d-101">Met Azure Resource Manager u parameters definiëren voor waarden gewenste toospecify wanneer Hallo sjabloon wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="ec60d-101">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="ec60d-102">Hallo-sjabloon bevat een sectie met de naam van de Parameters die alle Hallo parameterwaarden bevat.</span><span class="sxs-lookup"><span data-stu-id="ec60d-102">hello template includes a section called Parameters that contains all of hello parameter values.</span></span>
<span data-ttu-id="ec60d-103">U moet een parameter voor de waarden die variëren op basis van Hallo-project die u implementeert of op basis van Hallo-omgeving die u om te implementeert definiëren.</span><span class="sxs-lookup"><span data-stu-id="ec60d-103">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="ec60d-104">Definieer parameters niet voor waarden die altijd blijft dezelfde Hallo.</span><span class="sxs-lookup"><span data-stu-id="ec60d-104">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="ec60d-105">De waarde van elke parameter wordt gebruikt in Hallo sjabloon toodefine Hallo resources die zijn geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="ec60d-105">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span> 

<span data-ttu-id="ec60d-106">Bij het definiëren van parameters gebruiken Hallo **allowedValues** veld toospecify die de waarden van een gebruiker kunt opgeven tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="ec60d-106">When defining parameters, use hello **allowedValues** field toospecify which values a user can provide during deployment.</span></span> <span data-ttu-id="ec60d-107">Gebruik Hallo **defaultValue** tooassign veld een waarde toohello parameter, als geen waarde is opgegeven tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="ec60d-107">Use hello **defaultValue** field tooassign a value toohello parameter, if no value is provided during deployment.</span></span>

<span data-ttu-id="ec60d-108">Er wordt elke parameter in de sjabloon Hallo beschreven.</span><span class="sxs-lookup"><span data-stu-id="ec60d-108">We will describe each parameter in hello template.</span></span>

### <a name="sitename"></a><span data-ttu-id="ec60d-109">Sitenaam</span><span class="sxs-lookup"><span data-stu-id="ec60d-109">siteName</span></span>
<span data-ttu-id="ec60d-110">Hallo-naam van Hallo web-app die u wenst dat toocreate.</span><span class="sxs-lookup"><span data-stu-id="ec60d-110">hello name of hello web app that you wish toocreate.</span></span>

    "siteName":{
      "type":"string"
    }

### <a name="hostingplanname"></a><span data-ttu-id="ec60d-111">hostingPlanName</span><span class="sxs-lookup"><span data-stu-id="ec60d-111">hostingPlanName</span></span>
<span data-ttu-id="ec60d-112">Hallo-naam van het Hallo-App Service plan toouse voor het hosten van Hallo web-app.</span><span class="sxs-lookup"><span data-stu-id="ec60d-112">hello name of hello App Service plan toouse for hosting hello web app.</span></span>

    "hostingPlanName":{
      "type":"string"
    }

### <a name="sku"></a><span data-ttu-id="ec60d-113">SKU</span><span class="sxs-lookup"><span data-stu-id="ec60d-113">sku</span></span>
<span data-ttu-id="ec60d-114">Hallo prijscategorie voor Hallo hosting-plan.</span><span class="sxs-lookup"><span data-stu-id="ec60d-114">hello pricing tier for hello hosting plan.</span></span>

    "sku": {
      "type": "string",
      "allowedValues": [
        "F1",
        "D1",
        "B1",
        "B2",
        "B3",
        "S1",
        "S2",
        "S3",
        "P1",
        "P2",
        "P3",
        "P4"
      ],
      "defaultValue": "S1",
      "metadata": {
        "description": "hello pricing tier for hello hosting plan."
      }
    }

<span data-ttu-id="ec60d-115">Hallo sjabloon definieert Hallo-waarden die zijn toegestaan voor deze parameter en een standaardwaarde (S1) wordt toegewezen als er geen waarde is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="ec60d-115">hello template defines hello values that are permitted for this parameter, and assigns a default value (S1) if no value is specified.</span></span>

### <a name="workersize"></a><span data-ttu-id="ec60d-116">workerSize</span><span class="sxs-lookup"><span data-stu-id="ec60d-116">workerSize</span></span>
<span data-ttu-id="ec60d-117">Hallo exemplaargrootte van Hallo die als host fungeert voor plan (klein, Gemiddeld of grote).</span><span class="sxs-lookup"><span data-stu-id="ec60d-117">hello instance size of hello hosting plan (small, medium, or large).</span></span>

    "workerSize":{
      "type":"string",
      "allowedValues":[
        "0",
        "1",
        "2"
      ],
      "defaultValue":"0"
    }

<span data-ttu-id="ec60d-118">Hallo sjabloon definieert Hallo-waarden die zijn toegestaan voor deze parameter (0, 1 of 2), en wijst een standaardwaarde (0) als er geen waarde is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="ec60d-118">hello template defines hello values that are permitted for this parameter (0, 1, or 2), and assigns a default value (0) if no value is specified.</span></span> <span data-ttu-id="ec60d-119">Hallo-waarden komen overeen toosmall, middelgrote en grote.</span><span class="sxs-lookup"><span data-stu-id="ec60d-119">hello values correspond toosmall, medium and large.</span></span>

