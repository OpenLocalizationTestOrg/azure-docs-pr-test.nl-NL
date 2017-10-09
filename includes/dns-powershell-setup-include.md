## <a name="set-up-azure-powershell-for-azure-dns"></a>Azure PowerShell voor Azure DNS instellen

### <a name="before-you-begin"></a>Voordat u begint

Controleer of u Hallo volgende items voordat u begint met de configuratie.

* Een Azure-abonnement. Als u nog geen Azure-abonnement hebt, kunt u [uw voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) of [u aanmelden voor een gratis account](https://azure.microsoft.com/pricing/free-trial/).
* U moet tooinstall Hallo meest recente versie van hello Azure Resource Manager PowerShell-cmdlets. Zie voor meer informatie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azureps-cmdlets-docs).

### <a name="sign-in-tooyour-azure-account"></a>Meld u aan tooyour Azure-account

Open de PowerShell-console en tooyour-account koppelen. Zie voor meer informatie [met behulp van PowerShell met Resource Manager](../articles/azure-resource-manager/powershell-azure-resource-manager.md).

```powershell
Login-AzureRmAccount
```

### <a name="select-hello-subscription"></a>Hallo-abonnement selecteren
 
Controleer de abonnementen Hallo voor Hallo-account.

```powershell
Get-AzureRmSubscription
```

Kies welke van uw Azure-abonnementen toouse.

```powershell
Select-AzureRmSubscription -SubscriptionName "your_subscription_name"
```

### <a name="create-a-resource-group"></a>Een resourcegroep maken

Azure Resource Manager vereist dat er voor alle resourcegroepen een locatie wordt opgegeven. Deze locatie wordt gebruikt als Hallo standaardlocatie voor resources in die resourcegroep. Echter, omdat alle DNS-resources globaal en niet regionaal zijn, heeft Hallo keuze van de locatie voor resourcegroep geen invloed op Azure DNS.

U kunt deze stap overslaan als u een bestaande resourcegroep gebruikt.

```powershell
New-AzureRmResourceGroup -Name MyAzureResourceGroup -location "West US"
```

### <a name="register-resource-provider"></a>Resourceprovider registreren

Hello Azure DNS-service wordt beheerd door Hallo Microsoft.Network-resourceprovider. Uw Azure-abonnement moet geregistreerde toouse deze resourceprovider voordat u Azure DNS kunt gebruiken. Dit is een eenmalige bewerking voor elk abonnement.

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```