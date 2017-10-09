
## <a name="start-your-powershell-session"></a>Een PowerShell-sessie starten
Eerst, u moet hebben Hallo nieuwste Azure PowerShell geïnstalleerd en uitgevoerd. Zie voor gedetailleerde informatie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azureps-cmdlets-docs).

> [!NOTE]
> Veel nieuwe functies van SQL-Database worden alleen ondersteund wanneer u Hallo [Azure Resource Manager-implementatiemodel](../articles/azure-resource-manager/resource-group-overview.md), zodat de voorbeelden gebruiken Hallo [Azure SQL Database PowerShell-cmdlets](https://msdn.microsoft.com/library/azure/mt574084\(v=azure.300\).aspx) voor Resource Manager . Hallo service management (klassiek) implementatiemodel [cmdlets van Azure SQL Database-servicebeheer](https://msdn.microsoft.com/library/azure/dn546723\(v=azure.300\).aspx) worden ondersteund voor compatibiliteit met eerdere versies, maar we raden u Hallo Resource Manager-cmdlets gebruiken.
> 
> 

Voer Hallo [ **Add-AzureRmAccount** ](https://msdn.microsoft.com/library/azure/mt619267\(v=azure.300\).aspx) cmdlet, en u krijgt een aanmeldingsscherm tooenter uw referenties. Gebruik Hallo dezelfde referenties toosign in toohello Azure-portal te gebruiken.

```PowerShell
Add-AzureRmAccount
```

Als u meerdere abonnementen hebt, gebruikt u Hallo [ **Set-AzureRmContext** ](https://msdn.microsoft.com/library/azure/mt619263\(v=azure.300\).aspx) cmdlet tooselect welk abonnement uw PowerShell-sessie moet worden gebruikt. toosee welk abonnement Hallo huidige PowerShell sessie wordt gebruikt, voer [ **Get-AzureRmContext**](https://msdn.microsoft.com/library/azure/mt619265\(v=azure.300\).aspx). toosee uitvoeren van uw abonnementen [ **Get-AzureRmSubscription**](https://msdn.microsoft.com/library/azure/mt619284\(v=azure.300\).aspx).

```PowerShell
Set-AzureRmContext -SubscriptionId '4cac86b0-1e56-bbbb-aaaa-000000000000'
```
