## <a name="setting-up-powershell-for-resource-manager-templates"></a><span data-ttu-id="3ef43-101">PowerShell in te stellen voor Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="3ef43-101">Setting up PowerShell for Resource Manager templates</span></span>
<span data-ttu-id="3ef43-102">Voordat u Azure PowerShell met Resource Manager gebruiken kunt, moet u toohave Hallo rechts Windows PowerShell en Azure PowerShell versies.</span><span class="sxs-lookup"><span data-stu-id="3ef43-102">Before you can use Azure PowerShell with Resource Manager, you will need toohave hello right Windows PowerShell and Azure PowerShell versions.</span></span>

### <a name="verify-powershell-versions"></a><span data-ttu-id="3ef43-103">Controleer of de PowerShell-versies</span><span class="sxs-lookup"><span data-stu-id="3ef43-103">Verify PowerShell versions</span></span>
<span data-ttu-id="3ef43-104">Controleer of dat u Windows PowerShell versie 3.0 of 4.0 hebt.</span><span class="sxs-lookup"><span data-stu-id="3ef43-104">Verify you have Windows PowerShell version 3.0 or 4.0.</span></span> <span data-ttu-id="3ef43-105">toofind hello versie van Windows PowerShell, typ de volgende opdracht achter de opdrachtprompt van Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3ef43-105">toofind hello version of Windows PowerShell, type this command at a Windows PowerShell command prompt.</span></span>

    $PSVersionTable

<span data-ttu-id="3ef43-106">U ontvangt Hallo type informatie op te volgen:</span><span class="sxs-lookup"><span data-stu-id="3ef43-106">You will receive hello following type of information:</span></span>

    Name                           Value
    ----                           -----
    PSVersion                      3.0
    WSManStackVersion              3.0
    SerializationVersion           1.1.0.1
    CLRVersion                     4.0.30319.18444
    BuildVersion                   6.2.9200.16481
    PSCompatibleVersions           {1.0, 2.0, 3.0}
    PSRemotingProtocolVersion      2.2


<span data-ttu-id="3ef43-107">Verifieer dat Hallo de waarde van **PSVersion** 3.0 of 4.0.</span><span class="sxs-lookup"><span data-stu-id="3ef43-107">Verify that hello value of **PSVersion** is 3.0 or 4.0.</span></span> <span data-ttu-id="3ef43-108">Als dit niet het geval is, Zie [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) of [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span><span class="sxs-lookup"><span data-stu-id="3ef43-108">If not, see [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) or [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span></span>

### <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="3ef43-109">Uw Azure-account en -abonnement instellen</span><span class="sxs-lookup"><span data-stu-id="3ef43-109">Set your Azure account and subscription</span></span>
<span data-ttu-id="3ef43-110">Als u nog geen Azure-abonnement hebt, kunt u activeren uw [voordelen als MSDN-abonnee](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) of zich aanmelden voor een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3ef43-110">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="3ef43-111">Open een Azure PowerShell-opdrachtprompt en meld u aan tooAzure met deze opdracht.</span><span class="sxs-lookup"><span data-stu-id="3ef43-111">Open an Azure PowerShell command prompt and log on tooAzure with this command.</span></span>

    Login-AzureRmAccount

<span data-ttu-id="3ef43-112">Als u meerdere Azure-abonnementen hebt, kunt u uw Azure-abonnementen met deze opdracht weergeven.</span><span class="sxs-lookup"><span data-stu-id="3ef43-112">If you have multiple Azure subscriptions, you can list your Azure subscriptions with this command.</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="3ef43-113">U ontvangt Hallo type informatie op te volgen:</span><span class="sxs-lookup"><span data-stu-id="3ef43-113">You will receive hello following type of information:</span></span>

    SubscriptionId            : fd22919d-eaca-4f2b-841a-e4ac6770g92e
    SubscriptionName          : Visual Studio Ultimate with MSDN
    Environment               : AzureCloud
    SupportedModes            : AzureServiceManagement,AzureResourceManager
    DefaultAccount            : johndoe@contoso.com
    Accounts                  : {johndoe@contoso.com}
    IsDefault                 : True
    IsCurrent                 : True
    CurrentStorageAccountName :
    TenantId                  : 32fa88b4-86f1-419f-93ab-2d7ce016dba7

<span data-ttu-id="3ef43-114">Hallo huidige Azure-abonnement kunt u instellen door het uitvoeren van deze opdrachten bij hello Azure PowerShell-opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="3ef43-114">You can set hello current Azure subscription by running these commands at hello Azure PowerShell command prompt.</span></span> <span data-ttu-id="3ef43-115">Alles binnen de aanhalingstekens hello, inclusief Hallo < en > tekens, met de juiste naam Hallo vervangen.</span><span class="sxs-lookup"><span data-stu-id="3ef43-115">Replace everything within hello quotes, including hello < and > characters, with hello correct name.</span></span>

    $subscr="<SubscriptionName from hello display of Get-AzureRmSubscription>"
    Select-AzureRmSubscription -SubscriptionName $subscr -Current

<span data-ttu-id="3ef43-116">Zie voor meer informatie over Azure-abonnementen en accounts [hoe: verbinding maken met abonnement tooyour](/powershell/azureps-cmdlets-docs#step-3-connect).</span><span class="sxs-lookup"><span data-stu-id="3ef43-116">For more information about Azure subscriptions and accounts, see [How to: Connect tooyour subscription](/powershell/azureps-cmdlets-docs#step-3-connect).</span></span>

