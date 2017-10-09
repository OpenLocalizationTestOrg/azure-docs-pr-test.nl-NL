## <a name="set-up-azure-cli-for-azure-dns"></a><span data-ttu-id="7477a-101">Set up Azure CLI for Azure DNS (Azure CLI instellen voor Azure DNS)</span><span class="sxs-lookup"><span data-stu-id="7477a-101">Set up Azure CLI for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="7477a-102">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="7477a-102">Before you begin</span></span>

<span data-ttu-id="7477a-103">Controleer of u Hallo volgende items voordat u begint met de configuratie.</span><span class="sxs-lookup"><span data-stu-id="7477a-103">Verify that you have hello following items before beginning your configuration.</span></span>

* <span data-ttu-id="7477a-104">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="7477a-104">An Azure subscription.</span></span> <span data-ttu-id="7477a-105">Als u nog geen Azure-abonnement hebt, kunt u [uw voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) of [u aanmelden voor een gratis account](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7477a-105">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="7477a-106">Installeer de nieuwste versie Hallo van hello Azure CLI, beschikbaar voor Windows, Linux of MAC.</span><span class="sxs-lookup"><span data-stu-id="7477a-106">Install hello latest version of hello Azure CLI, available for Windows, Linux, or MAC.</span></span> <span data-ttu-id="7477a-107">Meer informatie vindt u op [installeren hello Azure CLI](../articles/cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="7477a-107">More information is available at [Install hello Azure CLI](../articles/cli-install-nodejs.md).</span></span>

### <a name="sign-in-tooyour-azure-account"></a><span data-ttu-id="7477a-108">Meld u aan tooyour Azure-account</span><span class="sxs-lookup"><span data-stu-id="7477a-108">Sign in tooyour Azure account</span></span>

<span data-ttu-id="7477a-109">Open een consolevenster en doorloop de verificatie met uw referenties.</span><span class="sxs-lookup"><span data-stu-id="7477a-109">Open a console window and authenticate with your credentials.</span></span> <span data-ttu-id="7477a-110">Zie voor meer informatie [aanmelden tooAzure van hello Azure CLI](../articles/xplat-cli-connect.md)</span><span class="sxs-lookup"><span data-stu-id="7477a-110">For more information, see [Log in tooAzure from hello Azure CLI](../articles/xplat-cli-connect.md)</span></span>

```azurecli
azure login
```

### <a name="switch-cli-mode"></a><span data-ttu-id="7477a-111">Naar de CLI-modus schakelen</span><span class="sxs-lookup"><span data-stu-id="7477a-111">Switch CLI mode</span></span>

<span data-ttu-id="7477a-112">Azure DNS maakt gebruik van Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7477a-112">Azure DNS uses Azure Resource Manager.</span></span> <span data-ttu-id="7477a-113">Zorg ervoor dat u overschakelt van CLI-modus toouse Azure Resource Manager-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="7477a-113">Make sure you switch CLI mode toouse Azure Resource Manager commands.</span></span>

```azurecli
azure config mode arm
```

### <a name="select-hello-subscription"></a><span data-ttu-id="7477a-114">Hallo-abonnement selecteren</span><span class="sxs-lookup"><span data-stu-id="7477a-114">Select hello subscription</span></span>

<span data-ttu-id="7477a-115">Controleer de abonnementen Hallo voor Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="7477a-115">Check hello subscriptions for hello account.</span></span>

```azurecli
azure account list
```

<span data-ttu-id="7477a-116">Kies welke van uw Azure-abonnementen toouse.</span><span class="sxs-lookup"><span data-stu-id="7477a-116">Choose which of your Azure subscriptions toouse.</span></span>

```azurecli
azure account set "subscription name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="7477a-117">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="7477a-117">Create a resource group</span></span>

<span data-ttu-id="7477a-118">Azure Resource Manager vereist dat er voor alle resourcegroepen een locatie wordt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="7477a-118">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="7477a-119">Dit wordt gebruikt als Hallo standaardlocatie voor resources in die resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="7477a-119">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="7477a-120">Echter, omdat alle DNS-resources globaal en niet regionaal zijn, heeft Hallo keuze van de locatie voor resourcegroep geen invloed op Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="7477a-120">However, because all DNS resources are global, not regional, hello choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="7477a-121">U kunt deze stap overslaan als u een bestaande resourcegroep gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7477a-121">You can skip this step if you are using an existing resource group.</span></span>

```azurecli
azure group create -n myresourcegroup --location "West US"
```

### <a name="register-resource-provider"></a><span data-ttu-id="7477a-122">Resourceprovider registreren</span><span class="sxs-lookup"><span data-stu-id="7477a-122">Register resource provider</span></span>

<span data-ttu-id="7477a-123">Hello Azure DNS-service wordt beheerd door Hallo Microsoft.Network-resourceprovider.</span><span class="sxs-lookup"><span data-stu-id="7477a-123">hello Azure DNS service is managed by hello Microsoft.Network resource provider.</span></span> <span data-ttu-id="7477a-124">Uw Azure-abonnement moet geregistreerde toouse deze resourceprovider voordat u Azure DNS kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7477a-124">Your Azure subscription must be registered toouse this resource provider before you can use Azure DNS.</span></span> <span data-ttu-id="7477a-125">Dit is een eenmalige bewerking voor elk abonnement.</span><span class="sxs-lookup"><span data-stu-id="7477a-125">This is a one-time operation for each subscription.</span></span>

```azurecli
azure provider register --namespace Microsoft.Network
```

