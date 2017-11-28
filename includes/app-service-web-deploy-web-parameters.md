<span data-ttu-id="eaf7d-101">Met Azure Resource Manager kunt u parameters definiëren voor waarden die u wilt opgeven wanneer de sjabloon wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="eaf7d-101">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="eaf7d-102">De sjabloon bevat een sectie met de naam van de Parameters die alle van de parameterwaarden bevat.</span><span class="sxs-lookup"><span data-stu-id="eaf7d-102">The template includes a section called Parameters that contains all of the parameter values.</span></span>
<span data-ttu-id="eaf7d-103">U moet een parameter voor de waarden die variëren op basis van het project dat u wilt implementeren of op basis van de omgeving die u om te implementeert definiëren.</span><span class="sxs-lookup"><span data-stu-id="eaf7d-103">You should define a parameter for those values that will vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="eaf7d-104">Geen parameters op voor waarden die u altijd hetzelfde gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="eaf7d-104">Do not define parameters for values that will always stay the same.</span></span> <span data-ttu-id="eaf7d-105">De waarde van elke parameter wordt gebruikt in de sjabloon voor het definiëren van de resources die worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="eaf7d-105">Each parameter value is used in the template to define the resources that are deployed.</span></span> 

<span data-ttu-id="eaf7d-106">Bij het definiëren van parameters, gebruiken de **allowedValues** aan te geven op welke waarden van een gebruiker kunt opgeven tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="eaf7d-106">When defining parameters, use the **allowedValues** field to specify which values a user can provide during deployment.</span></span> <span data-ttu-id="eaf7d-107">Gebruik de **defaultValue** veld een waarde toewijzen aan de parameter als u geen waarde is opgegeven tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="eaf7d-107">Use the **defaultValue** field to assign a value to the parameter, if no value is provided during deployment.</span></span>

<span data-ttu-id="eaf7d-108">Elke parameter in de sjabloon wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="eaf7d-108">We will describe each parameter in the template.</span></span>

### <a name="sitename"></a><span data-ttu-id="eaf7d-109">Sitenaam</span><span class="sxs-lookup"><span data-stu-id="eaf7d-109">siteName</span></span>
<span data-ttu-id="eaf7d-110">De naam van de web-app die u wilt maken.</span><span class="sxs-lookup"><span data-stu-id="eaf7d-110">The name of the web app that you wish to create.</span></span>

    "siteName":{
      "type":"string"
    }

### <a name="hostingplanname"></a><span data-ttu-id="eaf7d-111">hostingPlanName</span><span class="sxs-lookup"><span data-stu-id="eaf7d-111">hostingPlanName</span></span>
<span data-ttu-id="eaf7d-112">De naam van de App Service-abonnement moet worden gebruikt voor het hosten van de web-app.</span><span class="sxs-lookup"><span data-stu-id="eaf7d-112">The name of the App Service plan to use for hosting the web app.</span></span>

    "hostingPlanName":{
      "type":"string"
    }

### <a name="sku"></a><span data-ttu-id="eaf7d-113">SKU</span><span class="sxs-lookup"><span data-stu-id="eaf7d-113">sku</span></span>
<span data-ttu-id="eaf7d-114">De prijscategorie voor de hosting-plan.</span><span class="sxs-lookup"><span data-stu-id="eaf7d-114">The pricing tier for the hosting plan.</span></span>

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
        "description": "The pricing tier for the hosting plan."
      }
    }

<span data-ttu-id="eaf7d-115">De sjabloon definieert de waarden die zijn toegestaan voor deze parameter en een standaardwaarde (S1) wordt toegewezen als er geen waarde is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="eaf7d-115">The template defines the values that are permitted for this parameter, and assigns a default value (S1) if no value is specified.</span></span>

### <a name="workersize"></a><span data-ttu-id="eaf7d-116">workerSize</span><span class="sxs-lookup"><span data-stu-id="eaf7d-116">workerSize</span></span>
<span data-ttu-id="eaf7d-117">De exemplaargrootte van de hosting-abonnement (klein, Gemiddeld of grote).</span><span class="sxs-lookup"><span data-stu-id="eaf7d-117">The instance size of the hosting plan (small, medium, or large).</span></span>

    "workerSize":{
      "type":"string",
      "allowedValues":[
        "0",
        "1",
        "2"
      ],
      "defaultValue":"0"
    }

<span data-ttu-id="eaf7d-118">De sjabloon definieert de waarden die zijn toegestaan voor deze parameter (0, 1 of 2), en wijst een standaardwaarde (0) als er geen waarde is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="eaf7d-118">The template defines the values that are permitted for this parameter (0, 1, or 2), and assigns a default value (0) if no value is specified.</span></span> <span data-ttu-id="eaf7d-119">De waarden komen overeen met kleine, middelgrote en grote.</span><span class="sxs-lookup"><span data-stu-id="eaf7d-119">The values correspond to small, medium and large.</span></span>

