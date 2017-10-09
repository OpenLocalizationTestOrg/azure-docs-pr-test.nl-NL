## <a name="set-up-azure-powershell-for-azure-dns"></a><span data-ttu-id="ee3ec-101">Azure PowerShell voor Azure DNS instellen</span><span class="sxs-lookup"><span data-stu-id="ee3ec-101">Set up Azure PowerShell for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="ee3ec-102">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="ee3ec-102">Before you begin</span></span>

<span data-ttu-id="ee3ec-103">Controleer of u Hallo volgende items voordat u begint met de configuratie.</span><span class="sxs-lookup"><span data-stu-id="ee3ec-103">Verify that you have hello following items before beginning your configuration.</span></span>

* <span data-ttu-id="ee3ec-104">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="ee3ec-104">An Azure subscription.</span></span> <span data-ttu-id="ee3ec-105">Als u nog geen Azure-abonnement hebt, kunt u [uw voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) of [u aanmelden voor een gratis account](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ee3ec-105">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ee3ec-106">U moet tooinstall Hallo meest recente versie van hello Azure Resource Manager PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="ee3ec-106">You need tooinstall hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="ee3ec-107">Zie voor meer informatie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="ee3ec-107">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

### <a name="sign-in-tooyour-azure-account"></a><span data-ttu-id="ee3ec-108">Meld u aan tooyour Azure-account</span><span class="sxs-lookup"><span data-stu-id="ee3ec-108">Sign in tooyour Azure account</span></span>

<span data-ttu-id="ee3ec-109">Open de PowerShell-console en tooyour-account koppelen.</span><span class="sxs-lookup"><span data-stu-id="ee3ec-109">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="ee3ec-110">Zie voor meer informatie [met behulp van PowerShell met Resource Manager](../articles/azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="ee3ec-110">For more information, see [Using PowerShell with Resource Manager](../articles/azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="select-hello-subscription"></a><span data-ttu-id="ee3ec-111">Hallo-abonnement selecteren</span><span class="sxs-lookup"><span data-stu-id="ee3ec-111">Select hello subscription</span></span>
 
<span data-ttu-id="ee3ec-112">Controleer de abonnementen Hallo voor Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="ee3ec-112">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="ee3ec-113">Kies welke van uw Azure-abonnementen toouse.</span><span class="sxs-lookup"><span data-stu-id="ee3ec-113">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "your_subscription_name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="ee3ec-114">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="ee3ec-114">Create a resource group</span></span>

<span data-ttu-id="ee3ec-115">Azure Resource Manager vereist dat er voor alle resourcegroepen een locatie wordt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="ee3ec-115">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="ee3ec-116">Deze locatie wordt gebruikt als Hallo standaardlocatie voor resources in die resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="ee3ec-116">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="ee3ec-117">Echter, omdat alle DNS-resources globaal en niet regionaal zijn, heeft Hallo keuze van de locatie voor resourcegroep geen invloed op Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="ee3ec-117">However, because all DNS resources are global, not regional, hello choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="ee3ec-118">U kunt deze stap overslaan als u een bestaande resourcegroep gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ee3ec-118">You can skip this step if you are using an existing resource group.</span></span>

```powershell
New-AzureRmResourceGroup -Name MyAzureResourceGroup -location "West US"
```

### <a name="register-resource-provider"></a><span data-ttu-id="ee3ec-119">Resourceprovider registreren</span><span class="sxs-lookup"><span data-stu-id="ee3ec-119">Register resource provider</span></span>

<span data-ttu-id="ee3ec-120">Hello Azure DNS-service wordt beheerd door Hallo Microsoft.Network-resourceprovider.</span><span class="sxs-lookup"><span data-stu-id="ee3ec-120">hello Azure DNS service is managed by hello Microsoft.Network resource provider.</span></span> <span data-ttu-id="ee3ec-121">Uw Azure-abonnement moet geregistreerde toouse deze resourceprovider voordat u Azure DNS kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ee3ec-121">Your Azure subscription must be registered toouse this resource provider before you can use Azure DNS.</span></span> <span data-ttu-id="ee3ec-122">Dit is een eenmalige bewerking voor elk abonnement.</span><span class="sxs-lookup"><span data-stu-id="ee3ec-122">This is a one-time operation for each subscription.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```