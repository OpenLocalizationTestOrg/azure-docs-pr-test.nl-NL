Voordat u deze configuratie, moet u zich aanmeldt tooyour Azure-account. Hallo-cmdlet wordt u gevraagd om de aanmeldingsreferenties Hallo voor uw Azure-account. Na het aanmelden, downloadt het instellingen van uw account, zodat ze beschikbaar tooAzure PowerShell. Zie [Using Windows PowerShell with Resource Manager](../articles/powershell-azure-resource-manager.md) (Windows PowerShell gebruiken met Resource Manager) voor meer informatie.

toolog, open de PowerShell-console met verhoogde bevoegdheden en tooyour-account koppelen. Gebruik Hallo voorbeeld toohelp die u verbinding maakt te volgen:

```powershell
Login-AzureRmAccount
```

Als u meerdere Azure-abonnementen hebt, controleert u Hallo abonnementen voor Hallo-account.

```powershell
Get-AzureRmSubscription
```

Hallo-abonnement dat u wilt dat toouse opgeven.

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
 ```