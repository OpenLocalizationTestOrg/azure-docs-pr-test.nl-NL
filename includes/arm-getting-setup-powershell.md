## <a name="setting-up-powershell-for-resource-manager-templates"></a>PowerShell in te stellen voor Resource Manager-sjablonen
Voordat u Azure PowerShell met Resource Manager gebruiken kunt, moet u toohave Hallo rechts Windows PowerShell en Azure PowerShell versies.

### <a name="verify-powershell-versions"></a>Controleer of de PowerShell-versies
Controleer of dat u Windows PowerShell versie 3.0 of 4.0 hebt. toofind hello versie van Windows PowerShell, typ de volgende opdracht achter de opdrachtprompt van Windows PowerShell.

    $PSVersionTable

U ontvangt Hallo type informatie op te volgen:

    Name                           Value
    ----                           -----
    PSVersion                      3.0
    WSManStackVersion              3.0
    SerializationVersion           1.1.0.1
    CLRVersion                     4.0.30319.18444
    BuildVersion                   6.2.9200.16481
    PSCompatibleVersions           {1.0, 2.0, 3.0}
    PSRemotingProtocolVersion      2.2


Verifieer dat Hallo de waarde van **PSVersion** 3.0 of 4.0. Als dit niet het geval is, Zie [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) of [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).

### <a name="set-your-azure-account-and-subscription"></a>Uw Azure-account en -abonnement instellen
Als u nog geen Azure-abonnement hebt, kunt u activeren uw [voordelen als MSDN-abonnee](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) of zich aanmelden voor een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).

Open een Azure PowerShell-opdrachtprompt en meld u aan tooAzure met deze opdracht.

    Login-AzureRmAccount

Als u meerdere Azure-abonnementen hebt, kunt u uw Azure-abonnementen met deze opdracht weergeven.

    Get-AzureRmSubscription

U ontvangt Hallo type informatie op te volgen:

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

Hallo huidige Azure-abonnement kunt u instellen door het uitvoeren van deze opdrachten bij hello Azure PowerShell-opdrachtprompt. Alles binnen de aanhalingstekens hello, inclusief Hallo < en > tekens, met de juiste naam Hallo vervangen.

    $subscr="<SubscriptionName from hello display of Get-AzureRmSubscription>"
    Select-AzureRmSubscription -SubscriptionName $subscr -Current

Zie voor meer informatie over Azure-abonnementen en accounts [hoe: verbinding maken met abonnement tooyour](/powershell/azureps-cmdlets-docs#step-3-connect).

