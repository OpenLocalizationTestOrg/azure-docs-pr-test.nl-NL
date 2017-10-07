---
title: aaaManage Batch-account-resources met Hallo-clientbibliotheek voor .NET - Azure | Microsoft Docs
description: Maken, verwijderen en wijzigen van Azure Batch-account resources met Hallo Batch Management .NET-bibliotheek.
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 16279b23-60ff-4b16-b308-5de000e4c028
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/24/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 638d8129f3841ffcfb2e10f5d531a319bcbb7701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-accounts-and-quotas-with-hello-batch-management-client-library-for-net"></a>Batch-accounts en quota's met Hallo Batch Management-clientbibliotheek voor .NET beheren

> [!div class="op_single_selector"]
> * [Azure Portal](batch-account-create-portal.md)
> * [Batch Management .NET](batch-management-dotnet.md)
> 
> 

U kunt verlagen onderhoud overhead in uw Azure Batch-toepassingen met behulp van Hallo [Batch Management .NET] [ api_mgmt_net] bibliotheek tooautomate Batch-account maken, verwijderen, sleutelbeheer en quota voor detectie.

* **Batch-accounts maken en verwijderen** binnen elke regio. Als een onafhankelijke softwareleverancier (ISV) bijvoorbeeld, u als een service voor uw clients waarin elk een afzonderlijke Batch-account is toegewezen voor facturatie bieden, kunt u een account maken en verwijderen mogelijkheden tooyour klantportal toevoegen.
* **Ophalen en opnieuw genereren van sleutels** programmatisch voor uw Batch-accounts. Hierdoor kunt u voldoen aan het beveiligingsbeleid dat periodieke rollover of verstrijken van de sleutels worden afgedwongen. Wanneer u meerdere Batch-accounts in verschillende Azure-regio's hebt, verhoogt de automatisering van dit proces voor de overschakeling van uw oplossing efficiëntie.
* **Controleer de accountquota** en Hallo vallen en opstaan verschillende te bepalen welke Batch-accounts hebben welke limieten nemen. Maken van groepen of computerknooppunten toe te voegen, kunt u proactief waar aanpassen door uw account quota's controleren voordat u taken start, of wanneer deze compute resources worden gemaakt. U kunt bepalen welke accounts vereisen quotum verhoogt voordat de aanvullende resources in deze accounts toewijzen.
* **Functies van andere Azure-services combineren** voor een complete beheerervaring--met behulp van Batch Management .NET [Azure Active Directory][aad_about], en Hallo [Azure Resource Manager] [ resman_overview] samen in Hallo dezelfde toepassing. Met behulp van deze functies en hun API's, kunt u een frictionless verificatie-ervaring bieden, Hallo mogelijkheid toocreate en verwijderen van resourcegroepen en Hallo-mogelijkheden die hierboven zijn beschreven voor een oplossing voor end-to-end.

> [!NOTE]
> Dit artikel is gericht op Hallo programmatisch beheer van uw Batch-accounts, sleutels en quota's, kunt u veel van deze activiteiten uitvoeren met behulp van Hallo [Azure-portal][azure_portal]. Zie voor meer informatie [een Azure Batch-account maken met Azure-portal Hallo](batch-account-create-portal.md) en [quota en limieten voor hello Azure Batch-service](batch-quota-limit.md).
> 
> 

## <a name="create-and-delete-batch-accounts"></a>Batch-accounts maken en verwijderen
Zoals gezegd, een van de primaire functies Hallo Hallo Batch Management API is toocreate en verwijderen van de Batch-accounts in een Azure-regio. toodo dus gebruiken [BatchManagementClient.Account.CreateAsync] [ net_create] en [DeleteAsync][net_delete], of hun synchrone collega's.

Hallo volgende codefragment maakt u een account verkrijgt Hallo account zojuist hebt gemaakt van Hallo Batch-service en wordt deze verwijderd. In dit fragment en anderen in dit artikel Hallo `batchManagementClient` is een volledig geïnitialiseerd exemplaar van [BatchManagementClient][net_mgmt_client].

```csharp
// Create a new Batch account
await batchManagementClient.Account.CreateAsync("MyResourceGroup",
    "mynewaccount",
    new BatchAccountCreateParameters() { Location = "West US" });

// Get hello new account from hello Batch service
AccountResource account = await batchManagementClient.Account.GetAsync(
    "MyResourceGroup",
    "mynewaccount");

// Delete hello account
await batchManagementClient.Account.DeleteAsync("MyResourceGroup", account.Name);
```

> [!NOTE]
> Toepassingen die gebruikmaken van Hallo Batch Management .NET-bibliotheek en de klasse BatchManagementClient vereisen **servicebeheerder** of **CO-beheerder** toegang tot toohello abonnement die eigenaar is van Hallo Batch-account toobe beheerd. Zie voor meer informatie, Hallo [Azure Active Directory](#azure-active-directory) sectie en Hallo [AccountManagement] [ acct_mgmt_sample] codevoorbeeld.
> 
> 

## <a name="retrieve-and-regenerate-account-keys"></a>Ophalen en opnieuw genereren van sleutels
Primaire en secundaire sleutels verkrijgen van een Batch-account in uw abonnement via [ListKeysAsync][net_list_keys]. U kunt deze sleutels opnieuw genereren met behulp van [RegenerateKeyAsync][net_regenerate_keys].

```csharp
// Get and print hello primary and secondary keys
BatchAccountListKeyResult accountKeys =
    await batchManagementClient.Account.ListKeysAsync(
        "MyResourceGroup",
        "mybatchaccount");
Console.WriteLine("Primary key:   {0}", accountKeys.Primary);
Console.WriteLine("Secondary key: {0}", accountKeys.Secondary);

// Regenerate hello primary key
BatchAccountRegenerateKeyResponse newKeys =
    await batchManagementClient.Account.RegenerateKeyAsync(
        "MyResourceGroup",
        "mybatchaccount",
        new BatchAccountRegenerateKeyParameters() {
            KeyName = AccountKeyType.Primary
            });
```

> [!TIP]
> U kunt een werkstroom gestroomlijnde verbinding maken voor uw toepassingen. Eerst moet u een accountsleutel voor Batch-account Hallo toomanage met gewenst [ListKeysAsync][net_list_keys]. Vervolgens gebruikt u deze sleutel bij het initialiseren van Hallo Batch .NET-bibliotheek van [BatchSharedKeyCredentials] [ net_sharedkeycred] klasse, die wordt gebruikt bij het initialiseren van [BatchClient] [net_batch_client].
> 
> 

## <a name="check-azure-subscription-and-batch-account-quotas"></a>Controleer de Azure-abonnement en quota's Batch-account
Azure-abonnementen en Hallo afzonderlijke Azure-services zoals alle Batch-standaardinstelling quota's hebt die Hallo aantal van bepaalde diensten binnen deze beperken. Zie voor Hallo standaardquota voor Azure-abonnementen, [Azure-abonnement en Servicelimieten, quota's en beperkingen](../azure-subscription-service-limits.md). Zie voor standaardquota Hallo Hallo Batch-service, [quota en limieten voor hello Azure Batch-service](batch-quota-limit.md). U kunt deze quota in uw toepassingen controleren met behulp van Hallo Batch Management .NET-bibliotheek. Hiermee kunt u toomake toewijzing beslissingen te nemen voordat u accounts toevoegt of-bronnen zoals pools COMPUTE en rekenknooppunten.

### <a name="check-an-azure-subscription-for-batch-account-quotas"></a>Een Azure-abonnement voor Batch-account quota's controleren
Voordat u een Batch-account in een regio maakt, kunt u uw Azure-abonnement toosee controleren of u kunt tooadd een account in deze regio.

In Hallo onderstaande codefragment, gebruiken we eerst [BatchManagementClient.Account.ListAsync] [ net_mgmt_listaccounts] tooget een verzameling van alle Batch-accounts die binnen een abonnement. Als we deze verzameling hebt verkregen, kunt u het bepalen hoeveel accounts zich in de doelregio Hallo. Vervolgens we gebruiken [BatchManagementClient.Subscriptions] [ net_mgmt_subscriptions] tooobtain Hallo Batch-accountquotum en bepalen hoeveel accounts (indien aanwezig) kunnen worden gemaakt in deze regio.

```csharp
// Get a collection of all Batch accounts within hello subscription
BatchAccountListResponse listResponse =
        await batchManagementClient.Account.ListAsync(new AccountListParameters());
IList<AccountResource> accounts = listResponse.Accounts;
Console.WriteLine("Total number of Batch accounts under subscription id {0}:  {1}",
    creds.SubscriptionId,
    accounts.Count);

// Get a count of all accounts within hello target region
string region = "westus";
int accountsInRegion = accounts.Count(o => o.Location == region);

// Get hello account quota for hello specified region
SubscriptionQuotasGetResponse quotaResponse = await batchManagementClient.Subscriptions.GetSubscriptionQuotasAsync(region);
Console.WriteLine("Account quota for {0} region: {1}", region, quotaResponse.AccountQuota);

// Determine how many accounts can be created in hello target region
Console.WriteLine("Accounts in {0}: {1}", region, accountsInRegion);
Console.WriteLine("You can create {0} accounts in hello {1} region.", quotaResponse.AccountQuota - accountsInRegion, region);
```

In bovenstaande Hallo-codefragment `creds` is een exemplaar van [TokenCloudCredentials][azure_tokencreds]. een voorbeeld van het maken van dit object toosee Zie Hallo [AccountManagement] [ acct_mgmt_sample] codevoorbeeld op GitHub.

### <a name="check-a-batch-account-for-compute-resource-quotas"></a>Een Batch-account voor compute resource quota's controleren
Voordat u voor de rekenresources in uw Batch-oplossing, kunt u controleren tooensure Hallo bronnen die u wilt dat tooallocate won't hello accountquota overschrijden. In Hallo onderstaande codefragment, we Hallo Quotuminformatie voor Batch-account met de naam Hallo afdrukken `mybatchaccount`. U kunt in uw eigen toepassing dergelijke informatie toodetermine gebruiken of Hallo account Hallo aanvullende bronnen toobe gemaakt kan verwerken.

```csharp
// First obtain hello Batch account
BatchAccountGetResponse getResponse =
    await batchManagementClient.Account.GetAsync("MyResourceGroup", "mybatchaccount");
AccountResource account = getResponse.Resource;

// Now print hello compute resource quotas for hello account
Console.WriteLine("Core quota: {0}", account.Properties.CoreQuota);
Console.WriteLine("Pool quota: {0}", account.Properties.PoolQuota);
Console.WriteLine("Active job and job schedule quota: {0}", account.Properties.ActiveJobAndJobScheduleQuota);
```

> [!IMPORTANT]
> Hoewel er standaardquota voor Azure-abonnementen en services, veel van deze limieten kunnen worden gegenereerd door het uitgeven van een aanvraag in Hallo [Azure-portal][azure_portal]. Zie bijvoorbeeld [quota en limieten voor hello Azure Batch-service](batch-quota-limit.md) voor instructies over het verhogen van de quota van uw Batch-account.
> 
> 

## <a name="use-azure-ad-with-batch-management-net"></a>Azure AD gebruikt met Batch Management .NET

Hallo Batch Management .NET-bibliotheek is een Azure-resource provider-client en wordt gebruikt in combinatie met [Azure Resource Manager] [ resman_overview] toomanage account resources via een programma. Azure AD is vereist tooauthenticate aanvragen via een Azure-resource provider client, waaronder Hallo Batch Management .NET-bibliotheek, en via [Azure Resource Manager][resman_overview]. Zie voor meer informatie over het gebruik van Azure AD met Batch Management .NET-bibliotheek Hallo [gebruik Azure Active Directory tooauthenticate Batch-oplossingen](batch-aad-auth.md). 

## <a name="sample-project-on-github"></a>Voorbeeld van project op GitHub

toosee Batch Management .NET in actie, bekijk Hallo [AccountManagment] [ acct_mgmt_sample] voorbeeldproject op GitHub. Hallo AccountManagment voorbeeldtoepassing wordt getoond hoe Hallo volgende bewerkingen:

1. Verkrijgen van een beveiligingstoken uit Azure AD via [ADAL][aad_adal]. Als Hallo gebruiker is niet al aangemeld, wordt ze gevraagd hun Azure-referenties op te geven.
2. Met hello security token dat is verkregen van Azure AD, maken een [SubscriptionClient] [ resman_subclient] tooquery Azure voor een lijst met abonnementen die zijn gekoppeld aan het Hallo-account. Hallo-gebruiker kunt een abonnement selecteren in de lijst Hallo als deze meer dan één abonnement bevat.
3. Referenties die zijn gekoppeld aan de geselecteerde Hallo abonnement ophalen.
4. Maak een [ResourceManagementClient] [ resman_client] object met behulp van Hallo-referenties.
5. Gebruik een [ResourceManagementClient] [ resman_client] object toocreate een resourcegroep.
6. Gebruik een [BatchManagementClient] [ net_mgmt_client] object tooperform verschillende bewerkingen van de Batch-account:
   * Maak een Batch-account in de nieuwe resourcegroep Hallo.
   * Hallo-account zojuist hebt gemaakt van Hallo Batch-service ophalen.
   * Hallo-toegangscodes voor het nieuwe account Hallo afdrukken.
   * Een nieuwe primaire sleutel voor Hallo account opnieuw genereren.
   * Hallo Quotuminformatie voor Hallo account afdrukken.
   * Hallo Quotuminformatie voor Hallo abonnement afdrukken.
   * Alle accounts binnen Hallo abonnement afdrukken.
   * Gemaakte account verwijderen.
7. Hallo-resourcegroep verwijderen.

Voordat u Hallo nieuwe Batch-account en resource groep verwijdert, kunt u deze bekijken in Hallo [Azure-portal][azure_portal]:

Hallo-voorbeeldtoepassing toorun is, moet u eerst registreren deze met uw Azure AD-tenant in hello Azure portal en verleen machtigingen-toohello Azure Resource Manager-API. Volg de stappen Hallo in [oplossingen voor het beheer van Batch verifiëren met Active Directory](batch-aad-auth-management.md).


[aad_about]: ../active-directory/active-directory-whatis.md "Wat is Azure Active Directory?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Verificatie-scenario's voor Azure AD"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Toepassingen integreren met Azure Active Directory"
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_mgmt_net]: https://msdn.microsoft.com/library/azure/mt463120.aspx
[azure_portal]: http://portal.azure.com
[azure_storage]: https://azure.microsoft.com/services/storage/
[azure_tokencreds]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.tokencloudcredentials.aspx
[batch_explorer_project]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[net_batch_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_list_keys]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.listkeysasync.aspx
[net_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.createasync.aspx
[net_delete]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.deleteasync.aspx
[net_regenerate_keys]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.regeneratekeyasync.aspx
[net_sharedkeycred]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.auth.batchsharedkeycredentials.aspx
[net_mgmt_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.batchmanagementclient.aspx
[net_mgmt_subscriptions]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.batchmanagementclient.subscriptions.aspx
[net_mgmt_listaccounts]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.iaccountoperations.listasync.aspx
[resman_api]: https://msdn.microsoft.com/library/azure/mt418626.aspx
[resman_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.resources.resourcemanagementclient.aspx
[resman_subclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.subscriptions.subscriptionclient.aspx
[resman_overview]: ../azure-resource-manager/resource-group-overview.md

[1]: ./media/batch-management-dotnet/portal-01.png
[2]: ./media/batch-management-dotnet/portal-02.png
[3]: ./media/batch-management-dotnet/portal-03.png
