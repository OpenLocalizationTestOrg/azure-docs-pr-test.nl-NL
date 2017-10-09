## <a name="prepare-tooauthenticate-azure-resource-manager-requests"></a><span data-ttu-id="3f546-101">Azure Resource Manager-aanvragen tooauthenticate voorbereiden</span><span class="sxs-lookup"><span data-stu-id="3f546-101">Prepare tooauthenticate Azure Resource Manager requests</span></span>
<span data-ttu-id="3f546-102">U moet alle Hallo-bewerkingen die u uitvoert op resources met behulp van Hallo verifiëren [Azure Resource Manager] [ lnk-authenticate-arm] met Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="3f546-102">You must authenticate all hello operations that you perform on resources using hello [Azure Resource Manager][lnk-authenticate-arm] with Azure Active Directory (AD).</span></span> <span data-ttu-id="3f546-103">Hallo gemakkelijkste manier tooconfigure toouse PowerShell of Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="3f546-103">hello easiest way tooconfigure this is toouse PowerShell or Azure CLI.</span></span>

<span data-ttu-id="3f546-104">Hallo installeren [Azure PowerShell-cmdlets] [ lnk-powershell-install] voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="3f546-104">Install hello [Azure PowerShell cmdlets][lnk-powershell-install] before you continue.</span></span>

<span data-ttu-id="3f546-105">Hallo van de volgende stappen tonen hoe tooset up wachtwoordverificatie voor een AD-toepassing met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3f546-105">hello following steps show how tooset up password authentication for an AD application using PowerShell.</span></span> <span data-ttu-id="3f546-106">U kunt deze opdrachten uitvoeren in een standaard PowerShell-sessie.</span><span class="sxs-lookup"><span data-stu-id="3f546-106">You can run these commands in a standard PowerShell session.</span></span>

1. <span data-ttu-id="3f546-107">Meld u bij tooyour Azure-abonnement met Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="3f546-107">Log in tooyour Azure subscription using hello following command:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="3f546-108">Aanmelden tooAzure verleent u tooall toegang tot Azure-abonnementen die zijn gekoppeld aan uw referenties in Media Player Hallo als u meerdere Azure-abonnementen hebt.</span><span class="sxs-lookup"><span data-stu-id="3f546-108">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="3f546-109">Hallo opdracht toolist hello Azure-abonnementen beschikbaar voor u toouse volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="3f546-109">Use hello following command toolist hello Azure subscriptions available for you toouse:</span></span>

    ```powershell
    Get-AzureRMSubscription
    ```

    <span data-ttu-id="3f546-110">Gebruik Hallo opdracht tooselect abonnement dat u wilt dat uw IoT-hub-opdrachten toomanage toouse toorun hello te volgen.</span><span class="sxs-lookup"><span data-stu-id="3f546-110">Use hello following command tooselect subscription that you want toouse toorun hello commands toomanage your IoT hub.</span></span> <span data-ttu-id="3f546-111">U kunt Hallo abonnementsnaam of ID van uitvoer van de vorige opdracht Hallo Hallo gebruiken:</span><span class="sxs-lookup"><span data-stu-id="3f546-111">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

2. <span data-ttu-id="3f546-112">Maak een notitie van uw **TenantId** en **SubscriptionId**.</span><span class="sxs-lookup"><span data-stu-id="3f546-112">Make a note of your **TenantId** and **SubscriptionId**.</span></span> <span data-ttu-id="3f546-113">U nodig ze later.</span><span class="sxs-lookup"><span data-stu-id="3f546-113">You need them later.</span></span>
3. <span data-ttu-id="3f546-114">Maak een nieuwe Azure Active Directory-toepassing hello de volgende opdracht en vervangt Hallo plaats houders met:</span><span class="sxs-lookup"><span data-stu-id="3f546-114">Create a new Azure Active Directory application using hello following command, replacing hello place holders:</span></span>
   
   * <span data-ttu-id="3f546-115">**{Weergavenaam}:** een weergavenaam voor uw toepassing, zoals **MySampleApp**</span><span class="sxs-lookup"><span data-stu-id="3f546-115">**{Display name}:** a display name for your application such as **MySampleApp**</span></span>
   * <span data-ttu-id="3f546-116">**{URL startpagina}:** URL van de startpagina Hallo van uw app, zoals Hallo **http://mysampleapp/home**.</span><span class="sxs-lookup"><span data-stu-id="3f546-116">**{Home page URL}:** hello URL of hello home page of your app such as **http://mysampleapp/home**.</span></span> <span data-ttu-id="3f546-117">Deze URL heeft geen toopoint tooa echte toepassing nodig.</span><span class="sxs-lookup"><span data-stu-id="3f546-117">This URL does not need toopoint tooa real application.</span></span>
   * <span data-ttu-id="3f546-118">**{Toepassings-id}:** een unieke id zoals **http://mysampleapp**.</span><span class="sxs-lookup"><span data-stu-id="3f546-118">**{Application identifier}:** A unique identifier such as **http://mysampleapp**.</span></span> <span data-ttu-id="3f546-119">Deze URL heeft geen toopoint tooa echte toepassing nodig.</span><span class="sxs-lookup"><span data-stu-id="3f546-119">This URL does not need toopoint tooa real application.</span></span>
   * <span data-ttu-id="3f546-120">**{Wachtwoord}:** een wachtwoord dat u tooauthenticate met uw app.</span><span class="sxs-lookup"><span data-stu-id="3f546-120">**{Password}:** A password that you use tooauthenticate with your app.</span></span>
     
     ```powershell
     New-AzureRmADApplication -DisplayName {Display name} -HomePage {Home page URL} -IdentifierUris {Application identifier} -Password {Password}
     ```
4. <span data-ttu-id="3f546-121">Maak een notitie van Hallo **ApplicationId** van Hallo-toepassing die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3f546-121">Make a note of hello **ApplicationId** of hello application you created.</span></span> <span data-ttu-id="3f546-122">U nodig dit later.</span><span class="sxs-lookup"><span data-stu-id="3f546-122">You need this later.</span></span>
5. <span data-ttu-id="3f546-123">Maak een nieuwe service-principal maken met Hallo de volgende opdracht en vervangt **{MyApplicationId}** Hello **ApplicationId** uit de vorige stap Hallo:</span><span class="sxs-lookup"><span data-stu-id="3f546-123">Create a new service principal using hello following command, replacing **{MyApplicationId}** with hello **ApplicationId** from hello previous step:</span></span>
   
    ```powershell
    New-AzureRmADServicePrincipal -ApplicationId {MyApplicationId}
    ```
6. <span data-ttu-id="3f546-124">Instellen van een roltoewijzing met Hallo de volgende opdracht en vervangt **{MyApplicationId}** met uw **ApplicationId**.</span><span class="sxs-lookup"><span data-stu-id="3f546-124">Set up a role assignment using hello following command, replacing **{MyApplicationId}** with your **ApplicationId**.</span></span>
   
    ```powershell
    New-AzureRmRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName {MyApplicationId}
    ```

<span data-ttu-id="3f546-125">U bent nu klaar hello Azure AD-toepassing waarmee u tooauthenticate maken van uw aangepaste C#-toepassing.</span><span class="sxs-lookup"><span data-stu-id="3f546-125">You have now finished creating hello Azure AD application that enables you tooauthenticate from your custom C# application.</span></span> <span data-ttu-id="3f546-126">U moet Hallo waarden verderop in deze zelfstudie te volgen:</span><span class="sxs-lookup"><span data-stu-id="3f546-126">You need hello following values later in this tutorial:</span></span>

* <span data-ttu-id="3f546-127">TenantId</span><span class="sxs-lookup"><span data-stu-id="3f546-127">TenantId</span></span>
* <span data-ttu-id="3f546-128">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="3f546-128">SubscriptionId</span></span>
* <span data-ttu-id="3f546-129">ApplicationId</span><span class="sxs-lookup"><span data-stu-id="3f546-129">ApplicationId</span></span>
* <span data-ttu-id="3f546-130">Wachtwoord</span><span class="sxs-lookup"><span data-stu-id="3f546-130">Password</span></span>

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
