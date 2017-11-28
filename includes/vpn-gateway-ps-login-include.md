<span data-ttu-id="e528b-101">Voordat u begint met deze configuratie, moet u zich aanmelden bij uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="e528b-101">Before beginning this configuration, you must log in to your Azure account.</span></span> <span data-ttu-id="e528b-102">De cmdlet vraagt u om de aanmeldingsreferenties voor uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="e528b-102">The cmdlet prompts you for the login credentials for your Azure account.</span></span> <span data-ttu-id="e528b-103">Na het aanmelden, worden de instellingen van uw account gedownload zodat ze beschikbaar zijn voor Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e528b-103">After logging in, it downloads your account settings so they are available to Azure PowerShell.</span></span> <span data-ttu-id="e528b-104">Zie [Using Windows PowerShell with Resource Manager](../articles/powershell-azure-resource-manager.md) (Windows PowerShell gebruiken met Resource Manager) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e528b-104">For more information, see [Using Windows PowerShell with Resource Manager](../articles/powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="e528b-105">Open de PowerShell-console met verhoogde rechten en maak verbinding met uw account om u aan te melden.</span><span class="sxs-lookup"><span data-stu-id="e528b-105">To log in, open your PowerShell console with elevated privileges, and connect to your account.</span></span> <span data-ttu-id="e528b-106">Gebruik het volgende voorbeeld als hulp bij het maken van de verbinding:</span><span class="sxs-lookup"><span data-stu-id="e528b-106">Use the following example to help you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="e528b-107">Als u meerdere Azure-abonnementen hebt, controleert u de abonnementen voor het account.</span><span class="sxs-lookup"><span data-stu-id="e528b-107">If you have multiple Azure subscriptions, check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="e528b-108">Geef het abonnement op dat u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e528b-108">Specify the subscription that you want to use.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
 ```