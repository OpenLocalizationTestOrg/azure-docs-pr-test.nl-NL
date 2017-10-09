
## <a name="start-your-powershell-session"></a>Een PowerShell-sessie starten
U moet eerst toohave Hallo nieuwste [Azure PowerShell](http://msdn.microsoft.com/library/mt619274.aspx) geïnstalleerd en wordt uitgevoerd. Zie voor gedetailleerde informatie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azureps-cmdlets-docs).

> [!NOTE]
> Hallo voorbeelden in dit onderwerp gebruiken [Azure Resource Manager-implementatiemodel](../articles/azure-resource-manager/resource-group-overview.md), zodat de voorbeelden gebruiken Hallo [Azure Resource Manager-cmdlets](http://msdn.microsoft.com/library/azure/mt125356.aspx). 
> 
> 

Voer Hallo [ **Add-AzureRmAccount** ](http://msdn.microsoft.com/library/mt619267.aspx) cmdlet en u krijgt een teken in het scherm tooenter uw referenties. Gebruik Hallo dezelfde referenties toosign in toohello Azure-portal te gebruiken.

    Add-AzureRmAccount

Als u meerdere abonnementen hello gebruiken [ **Set-AzureRmContext** ](http://msdn.microsoft.com/library/mt619263.aspx) cmdlet tooselect welk abonnement uw PowerShell-sessie moet worden gebruikt. toosee welk abonnement Hallo huidige PowerShell sessie wordt gebruikt, voer [ **Get-AzureRmContext**](http://msdn.microsoft.com/library/mt619265.aspx). toosee uitvoeren van uw abonnementen [ **Get-AzureRmSubscription**](http://msdn.microsoft.com/library/mt619284.aspx).

    Set-AzureRmContext -SubscriptionId '4cac86b0-1e56-bbbb-aaaa-000000000000'

