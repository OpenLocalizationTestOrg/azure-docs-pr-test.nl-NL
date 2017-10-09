<span data-ttu-id="4cadf-101">Voordat u deze configuratie, moet u zich aanmeldt tooyour Azure-account.</span><span class="sxs-lookup"><span data-stu-id="4cadf-101">Before beginning this configuration, you must log in tooyour Azure account.</span></span> <span data-ttu-id="4cadf-102">Hallo-cmdlet wordt u gevraagd om de aanmeldingsreferenties Hallo voor uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="4cadf-102">hello cmdlet prompts you for hello login credentials for your Azure account.</span></span> <span data-ttu-id="4cadf-103">Na het aanmelden, downloadt het instellingen van uw account, zodat ze beschikbaar tooAzure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4cadf-103">After logging in, it downloads your account settings so they are available tooAzure PowerShell.</span></span> <span data-ttu-id="4cadf-104">Zie [Using Windows PowerShell with Resource Manager](../articles/powershell-azure-resource-manager.md) (Windows PowerShell gebruiken met Resource Manager) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="4cadf-104">For more information, see [Using Windows PowerShell with Resource Manager](../articles/powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="4cadf-105">toolog, open de PowerShell-console met verhoogde bevoegdheden en tooyour-account koppelen.</span><span class="sxs-lookup"><span data-stu-id="4cadf-105">toolog in, open your PowerShell console with elevated privileges, and connect tooyour account.</span></span> <span data-ttu-id="4cadf-106">Gebruik Hallo voorbeeld toohelp die u verbinding maakt te volgen:</span><span class="sxs-lookup"><span data-stu-id="4cadf-106">Use hello following example toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="4cadf-107">Als u meerdere Azure-abonnementen hebt, controleert u Hallo abonnementen voor Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="4cadf-107">If you have multiple Azure subscriptions, check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="4cadf-108">Hallo-abonnement dat u wilt dat toouse opgeven.</span><span class="sxs-lookup"><span data-stu-id="4cadf-108">Specify hello subscription that you want toouse.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
 ```