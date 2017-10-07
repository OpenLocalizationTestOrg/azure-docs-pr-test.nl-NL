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
# <a name="manage-batch-accounts-and-quotas-with-hello-batch-management-client-library-for-net"></a><span data-ttu-id="f3a04-103">Batch-accounts en quota's met Hallo Batch Management-clientbibliotheek voor .NET beheren</span><span class="sxs-lookup"><span data-stu-id="f3a04-103">Manage Batch accounts and quotas with hello Batch Management client library for .NET</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f3a04-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f3a04-104">Azure portal</span></span>](batch-account-create-portal.md)
> * [<span data-ttu-id="f3a04-105">Batch Management .NET</span><span class="sxs-lookup"><span data-stu-id="f3a04-105">Batch Management .NET</span></span>](batch-management-dotnet.md)
> 
> 

<span data-ttu-id="f3a04-106">U kunt verlagen onderhoud overhead in uw Azure Batch-toepassingen met behulp van Hallo [Batch Management .NET] [ api_mgmt_net] bibliotheek tooautomate Batch-account maken, verwijderen, sleutelbeheer en quota voor detectie.</span><span class="sxs-lookup"><span data-stu-id="f3a04-106">You can lower maintenance overhead in your Azure Batch applications by using hello [Batch Management .NET][api_mgmt_net] library tooautomate Batch account creation, deletion, key management, and quota discovery.</span></span>

* <span data-ttu-id="f3a04-107">**Batch-accounts maken en verwijderen** binnen elke regio.</span><span class="sxs-lookup"><span data-stu-id="f3a04-107">**Create and delete Batch accounts** within any region.</span></span> <span data-ttu-id="f3a04-108">Als een onafhankelijke softwareleverancier (ISV) bijvoorbeeld, u als een service voor uw clients waarin elk een afzonderlijke Batch-account is toegewezen voor facturatie bieden, kunt u een account maken en verwijderen mogelijkheden tooyour klantportal toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f3a04-108">If, as an independent software vendor (ISV) for example, you provide a service for your clients in which each is assigned a separate Batch account for billing purposes, you can add account creation and deletion capabilities tooyour customer portal.</span></span>
* <span data-ttu-id="f3a04-109">**Ophalen en opnieuw genereren van sleutels** programmatisch voor uw Batch-accounts.</span><span class="sxs-lookup"><span data-stu-id="f3a04-109">**Retrieve and regenerate account keys** programmatically for any of your Batch accounts.</span></span> <span data-ttu-id="f3a04-110">Hierdoor kunt u voldoen aan het beveiligingsbeleid dat periodieke rollover of verstrijken van de sleutels worden afgedwongen.</span><span class="sxs-lookup"><span data-stu-id="f3a04-110">This can help you comply with security policies that enforce periodic rollover or expiry of account keys.</span></span> <span data-ttu-id="f3a04-111">Wanneer u meerdere Batch-accounts in verschillende Azure-regio's hebt, verhoogt de automatisering van dit proces voor de overschakeling van uw oplossing efficiëntie.</span><span class="sxs-lookup"><span data-stu-id="f3a04-111">When you have several Batch accounts in various Azure regions, automation of this rollover process increases your solution's efficiency.</span></span>
* <span data-ttu-id="f3a04-112">**Controleer de accountquota** en Hallo vallen en opstaan verschillende te bepalen welke Batch-accounts hebben welke limieten nemen.</span><span class="sxs-lookup"><span data-stu-id="f3a04-112">**Check account quotas** and take hello trial-and-error guesswork out of determining which Batch accounts have what limits.</span></span> <span data-ttu-id="f3a04-113">Maken van groepen of computerknooppunten toe te voegen, kunt u proactief waar aanpassen door uw account quota's controleren voordat u taken start, of wanneer deze compute resources worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f3a04-113">By checking your account quotas before starting jobs, creating pools, or adding compute nodes, you can proactively adjust where or when these compute resources are created.</span></span> <span data-ttu-id="f3a04-114">U kunt bepalen welke accounts vereisen quotum verhoogt voordat de aanvullende resources in deze accounts toewijzen.</span><span class="sxs-lookup"><span data-stu-id="f3a04-114">You can determine which accounts require quota increases before allocating additional resources in those accounts.</span></span>
* <span data-ttu-id="f3a04-115">**Functies van andere Azure-services combineren** voor een complete beheerervaring--met behulp van Batch Management .NET [Azure Active Directory][aad_about], en Hallo [Azure Resource Manager] [ resman_overview] samen in Hallo dezelfde toepassing.</span><span class="sxs-lookup"><span data-stu-id="f3a04-115">**Combine features of other Azure services** for a full-featured management experience--by using Batch Management .NET, [Azure Active Directory][aad_about], and hello [Azure Resource Manager][resman_overview] together in hello same application.</span></span> <span data-ttu-id="f3a04-116">Met behulp van deze functies en hun API's, kunt u een frictionless verificatie-ervaring bieden, Hallo mogelijkheid toocreate en verwijderen van resourcegroepen en Hallo-mogelijkheden die hierboven zijn beschreven voor een oplossing voor end-to-end.</span><span class="sxs-lookup"><span data-stu-id="f3a04-116">By using these features and their APIs, you can provide a frictionless authentication experience, hello ability toocreate and delete resource groups, and hello capabilities that are described above for an end-to-end management solution.</span></span>

> [!NOTE]
> <span data-ttu-id="f3a04-117">Dit artikel is gericht op Hallo programmatisch beheer van uw Batch-accounts, sleutels en quota's, kunt u veel van deze activiteiten uitvoeren met behulp van Hallo [Azure-portal][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="f3a04-117">While this article focuses on hello programmatic management of your Batch accounts, keys, and quotas, you can perform many of these activities by using hello [Azure portal][azure_portal].</span></span> <span data-ttu-id="f3a04-118">Zie voor meer informatie [een Azure Batch-account maken met Azure-portal Hallo](batch-account-create-portal.md) en [quota en limieten voor hello Azure Batch-service](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="f3a04-118">For more information, see [Create an Azure Batch account using hello Azure portal](batch-account-create-portal.md) and [Quotas and limits for hello Azure Batch service](batch-quota-limit.md).</span></span>
> 
> 

## <a name="create-and-delete-batch-accounts"></a><span data-ttu-id="f3a04-119">Batch-accounts maken en verwijderen</span><span class="sxs-lookup"><span data-stu-id="f3a04-119">Create and delete Batch accounts</span></span>
<span data-ttu-id="f3a04-120">Zoals gezegd, een van de primaire functies Hallo Hallo Batch Management API is toocreate en verwijderen van de Batch-accounts in een Azure-regio.</span><span class="sxs-lookup"><span data-stu-id="f3a04-120">As mentioned, one of hello primary features of hello Batch Management API is toocreate and delete Batch accounts in an Azure region.</span></span> <span data-ttu-id="f3a04-121">toodo dus gebruiken [BatchManagementClient.Account.CreateAsync] [ net_create] en [DeleteAsync][net_delete], of hun synchrone collega's.</span><span class="sxs-lookup"><span data-stu-id="f3a04-121">toodo so, use [BatchManagementClient.Account.CreateAsync][net_create] and [DeleteAsync][net_delete], or their synchronous counterparts.</span></span>

<span data-ttu-id="f3a04-122">Hallo volgende codefragment maakt u een account verkrijgt Hallo account zojuist hebt gemaakt van Hallo Batch-service en wordt deze verwijderd.</span><span class="sxs-lookup"><span data-stu-id="f3a04-122">hello following code snippet creates an account, obtains hello newly created account from hello Batch service, and then deletes it.</span></span> <span data-ttu-id="f3a04-123">In dit fragment en anderen in dit artikel Hallo `batchManagementClient` is een volledig geïnitialiseerd exemplaar van [BatchManagementClient][net_mgmt_client].</span><span class="sxs-lookup"><span data-stu-id="f3a04-123">In this snippet and hello others in this article, `batchManagementClient` is a fully initialized instance of [BatchManagementClient][net_mgmt_client].</span></span>

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
> <span data-ttu-id="f3a04-124">Toepassingen die gebruikmaken van Hallo Batch Management .NET-bibliotheek en de klasse BatchManagementClient vereisen **servicebeheerder** of **CO-beheerder** toegang tot toohello abonnement die eigenaar is van Hallo Batch-account toobe beheerd.</span><span class="sxs-lookup"><span data-stu-id="f3a04-124">Applications that use hello Batch Management .NET library and its BatchManagementClient class require **service administrator** or **coadministrator** access toohello subscription that owns hello Batch account toobe managed.</span></span> <span data-ttu-id="f3a04-125">Zie voor meer informatie, Hallo [Azure Active Directory](#azure-active-directory) sectie en Hallo [AccountManagement] [ acct_mgmt_sample] codevoorbeeld.</span><span class="sxs-lookup"><span data-stu-id="f3a04-125">For more information, see hello [Azure Active Directory](#azure-active-directory) section and hello [AccountManagement][acct_mgmt_sample] code sample.</span></span>
> 
> 

## <a name="retrieve-and-regenerate-account-keys"></a><span data-ttu-id="f3a04-126">Ophalen en opnieuw genereren van sleutels</span><span class="sxs-lookup"><span data-stu-id="f3a04-126">Retrieve and regenerate account keys</span></span>
<span data-ttu-id="f3a04-127">Primaire en secundaire sleutels verkrijgen van een Batch-account in uw abonnement via [ListKeysAsync][net_list_keys].</span><span class="sxs-lookup"><span data-stu-id="f3a04-127">Obtain primary and secondary account keys from any Batch account within your subscription by using [ListKeysAsync][net_list_keys].</span></span> <span data-ttu-id="f3a04-128">U kunt deze sleutels opnieuw genereren met behulp van [RegenerateKeyAsync][net_regenerate_keys].</span><span class="sxs-lookup"><span data-stu-id="f3a04-128">You can regenerate those keys by using [RegenerateKeyAsync][net_regenerate_keys].</span></span>

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
> <span data-ttu-id="f3a04-129">U kunt een werkstroom gestroomlijnde verbinding maken voor uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="f3a04-129">You can create a streamlined connection workflow for your management applications.</span></span> <span data-ttu-id="f3a04-130">Eerst moet u een accountsleutel voor Batch-account Hallo toomanage met gewenst [ListKeysAsync][net_list_keys].</span><span class="sxs-lookup"><span data-stu-id="f3a04-130">First, obtain an account key for hello Batch account you wish toomanage with [ListKeysAsync][net_list_keys].</span></span> <span data-ttu-id="f3a04-131">Vervolgens gebruikt u deze sleutel bij het initialiseren van Hallo Batch .NET-bibliotheek van [BatchSharedKeyCredentials] [ net_sharedkeycred] klasse, die wordt gebruikt bij het initialiseren van [BatchClient] [net_batch_client].</span><span class="sxs-lookup"><span data-stu-id="f3a04-131">Then, use this key when initializing hello Batch .NET library's [BatchSharedKeyCredentials][net_sharedkeycred] class, which is used when initializing [BatchClient][net_batch_client].</span></span>
> 
> 

## <a name="check-azure-subscription-and-batch-account-quotas"></a><span data-ttu-id="f3a04-132">Controleer de Azure-abonnement en quota's Batch-account</span><span class="sxs-lookup"><span data-stu-id="f3a04-132">Check Azure subscription and Batch account quotas</span></span>
<span data-ttu-id="f3a04-133">Azure-abonnementen en Hallo afzonderlijke Azure-services zoals alle Batch-standaardinstelling quota's hebt die Hallo aantal van bepaalde diensten binnen deze beperken.</span><span class="sxs-lookup"><span data-stu-id="f3a04-133">Azure subscriptions and hello individual Azure services like Batch all have default quotas that limit hello number of certain entities within them.</span></span> <span data-ttu-id="f3a04-134">Zie voor Hallo standaardquota voor Azure-abonnementen, [Azure-abonnement en Servicelimieten, quota's en beperkingen](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="f3a04-134">For hello default quotas for Azure subscriptions, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span> <span data-ttu-id="f3a04-135">Zie voor standaardquota Hallo Hallo Batch-service, [quota en limieten voor hello Azure Batch-service](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="f3a04-135">For hello default quotas of hello Batch service, see [Quotas and limits for hello Azure Batch service](batch-quota-limit.md).</span></span> <span data-ttu-id="f3a04-136">U kunt deze quota in uw toepassingen controleren met behulp van Hallo Batch Management .NET-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="f3a04-136">By using hello Batch Management .NET library, you can check these quotas in your applications.</span></span> <span data-ttu-id="f3a04-137">Hiermee kunt u toomake toewijzing beslissingen te nemen voordat u accounts toevoegt of-bronnen zoals pools COMPUTE en rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="f3a04-137">This enables you toomake allocation decisions before you add accounts or compute resources like pools and compute nodes.</span></span>

### <a name="check-an-azure-subscription-for-batch-account-quotas"></a><span data-ttu-id="f3a04-138">Een Azure-abonnement voor Batch-account quota's controleren</span><span class="sxs-lookup"><span data-stu-id="f3a04-138">Check an Azure subscription for Batch account quotas</span></span>
<span data-ttu-id="f3a04-139">Voordat u een Batch-account in een regio maakt, kunt u uw Azure-abonnement toosee controleren of u kunt tooadd een account in deze regio.</span><span class="sxs-lookup"><span data-stu-id="f3a04-139">Before creating a Batch account in a region, you can check your Azure subscription toosee whether you are able tooadd an account in that region.</span></span>

<span data-ttu-id="f3a04-140">In Hallo onderstaande codefragment, gebruiken we eerst [BatchManagementClient.Account.ListAsync] [ net_mgmt_listaccounts] tooget een verzameling van alle Batch-accounts die binnen een abonnement.</span><span class="sxs-lookup"><span data-stu-id="f3a04-140">In hello code snippet below, we first use [BatchManagementClient.Account.ListAsync][net_mgmt_listaccounts] tooget a collection of all Batch accounts that are within a subscription.</span></span> <span data-ttu-id="f3a04-141">Als we deze verzameling hebt verkregen, kunt u het bepalen hoeveel accounts zich in de doelregio Hallo.</span><span class="sxs-lookup"><span data-stu-id="f3a04-141">Once we've obtained this collection, we determine how many accounts are in hello target region.</span></span> <span data-ttu-id="f3a04-142">Vervolgens we gebruiken [BatchManagementClient.Subscriptions] [ net_mgmt_subscriptions] tooobtain Hallo Batch-accountquotum en bepalen hoeveel accounts (indien aanwezig) kunnen worden gemaakt in deze regio.</span><span class="sxs-lookup"><span data-stu-id="f3a04-142">Then we use [BatchManagementClient.Subscriptions][net_mgmt_subscriptions] tooobtain hello Batch account quota and determine how many accounts (if any) can be created in that region.</span></span>

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

<span data-ttu-id="f3a04-143">In bovenstaande Hallo-codefragment `creds` is een exemplaar van [TokenCloudCredentials][azure_tokencreds].</span><span class="sxs-lookup"><span data-stu-id="f3a04-143">In hello snippet above, `creds` is an instance of [TokenCloudCredentials][azure_tokencreds].</span></span> <span data-ttu-id="f3a04-144">een voorbeeld van het maken van dit object toosee Zie Hallo [AccountManagement] [ acct_mgmt_sample] codevoorbeeld op GitHub.</span><span class="sxs-lookup"><span data-stu-id="f3a04-144">toosee an example of creating this object, see hello [AccountManagement][acct_mgmt_sample] code sample on GitHub.</span></span>

### <a name="check-a-batch-account-for-compute-resource-quotas"></a><span data-ttu-id="f3a04-145">Een Batch-account voor compute resource quota's controleren</span><span class="sxs-lookup"><span data-stu-id="f3a04-145">Check a Batch account for compute resource quotas</span></span>
<span data-ttu-id="f3a04-146">Voordat u voor de rekenresources in uw Batch-oplossing, kunt u controleren tooensure Hallo bronnen die u wilt dat tooallocate won't hello accountquota overschrijden.</span><span class="sxs-lookup"><span data-stu-id="f3a04-146">Before increasing compute resources in your Batch solution, you can check tooensure hello resources you want tooallocate won't exceed hello account's quotas.</span></span> <span data-ttu-id="f3a04-147">In Hallo onderstaande codefragment, we Hallo Quotuminformatie voor Batch-account met de naam Hallo afdrukken `mybatchaccount`.</span><span class="sxs-lookup"><span data-stu-id="f3a04-147">In hello code snippet below, we print hello quota information for hello Batch account named `mybatchaccount`.</span></span> <span data-ttu-id="f3a04-148">U kunt in uw eigen toepassing dergelijke informatie toodetermine gebruiken of Hallo account Hallo aanvullende bronnen toobe gemaakt kan verwerken.</span><span class="sxs-lookup"><span data-stu-id="f3a04-148">In your own application, you could use such information toodetermine whether hello account can handle hello additional resources toobe created.</span></span>

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
> <span data-ttu-id="f3a04-149">Hoewel er standaardquota voor Azure-abonnementen en services, veel van deze limieten kunnen worden gegenereerd door het uitgeven van een aanvraag in Hallo [Azure-portal][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="f3a04-149">While there are default quotas for Azure subscriptions and services, many of these limits can be raised by issuing a request in hello [Azure portal][azure_portal].</span></span> <span data-ttu-id="f3a04-150">Zie bijvoorbeeld [quota en limieten voor hello Azure Batch-service](batch-quota-limit.md) voor instructies over het verhogen van de quota van uw Batch-account.</span><span class="sxs-lookup"><span data-stu-id="f3a04-150">For example, see [Quotas and limits for hello Azure Batch service](batch-quota-limit.md) for instructions on increasing your Batch account quotas.</span></span>
> 
> 

## <a name="use-azure-ad-with-batch-management-net"></a><span data-ttu-id="f3a04-151">Azure AD gebruikt met Batch Management .NET</span><span class="sxs-lookup"><span data-stu-id="f3a04-151">Use Azure AD with Batch Management .NET</span></span>

<span data-ttu-id="f3a04-152">Hallo Batch Management .NET-bibliotheek is een Azure-resource provider-client en wordt gebruikt in combinatie met [Azure Resource Manager] [ resman_overview] toomanage account resources via een programma.</span><span class="sxs-lookup"><span data-stu-id="f3a04-152">hello Batch Management .NET library is an Azure resource provider client, and is used together with [Azure Resource Manager][resman_overview] toomanage account resources programmatically.</span></span> <span data-ttu-id="f3a04-153">Azure AD is vereist tooauthenticate aanvragen via een Azure-resource provider client, waaronder Hallo Batch Management .NET-bibliotheek, en via [Azure Resource Manager][resman_overview].</span><span class="sxs-lookup"><span data-stu-id="f3a04-153">Azure AD is required tooauthenticate requests made through any Azure resource provider client, including hello Batch Management .NET library, and through [Azure Resource Manager][resman_overview].</span></span> <span data-ttu-id="f3a04-154">Zie voor meer informatie over het gebruik van Azure AD met Batch Management .NET-bibliotheek Hallo [gebruik Azure Active Directory tooauthenticate Batch-oplossingen](batch-aad-auth.md).</span><span class="sxs-lookup"><span data-stu-id="f3a04-154">For information about using Azure AD with hello Batch Management .NET library, see [Use Azure Active Directory tooauthenticate Batch solutions](batch-aad-auth.md).</span></span> 

## <a name="sample-project-on-github"></a><span data-ttu-id="f3a04-155">Voorbeeld van project op GitHub</span><span class="sxs-lookup"><span data-stu-id="f3a04-155">Sample project on GitHub</span></span>

<span data-ttu-id="f3a04-156">toosee Batch Management .NET in actie, bekijk Hallo [AccountManagment] [ acct_mgmt_sample] voorbeeldproject op GitHub.</span><span class="sxs-lookup"><span data-stu-id="f3a04-156">toosee Batch Management .NET in action, check out hello [AccountManagment][acct_mgmt_sample] sample project on GitHub.</span></span> <span data-ttu-id="f3a04-157">Hallo AccountManagment voorbeeldtoepassing wordt getoond hoe Hallo volgende bewerkingen:</span><span class="sxs-lookup"><span data-stu-id="f3a04-157">hello AccountManagment sample application demonstrates hello following operations:</span></span>

1. <span data-ttu-id="f3a04-158">Verkrijgen van een beveiligingstoken uit Azure AD via [ADAL][aad_adal].</span><span class="sxs-lookup"><span data-stu-id="f3a04-158">Acquire a security token from Azure AD by using [ADAL][aad_adal].</span></span> <span data-ttu-id="f3a04-159">Als Hallo gebruiker is niet al aangemeld, wordt ze gevraagd hun Azure-referenties op te geven.</span><span class="sxs-lookup"><span data-stu-id="f3a04-159">If hello user is not already signed in, they are prompted for their Azure credentials.</span></span>
2. <span data-ttu-id="f3a04-160">Met hello security token dat is verkregen van Azure AD, maken een [SubscriptionClient] [ resman_subclient] tooquery Azure voor een lijst met abonnementen die zijn gekoppeld aan het Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="f3a04-160">With hello security token obtained from Azure AD, create a [SubscriptionClient][resman_subclient] tooquery Azure for a list of subscriptions associated with hello account.</span></span> <span data-ttu-id="f3a04-161">Hallo-gebruiker kunt een abonnement selecteren in de lijst Hallo als deze meer dan één abonnement bevat.</span><span class="sxs-lookup"><span data-stu-id="f3a04-161">hello user can select a subscription from hello list if it contains more than one subscription.</span></span>
3. <span data-ttu-id="f3a04-162">Referenties die zijn gekoppeld aan de geselecteerde Hallo abonnement ophalen.</span><span class="sxs-lookup"><span data-stu-id="f3a04-162">Get credentials associated with hello selected subscription.</span></span>
4. <span data-ttu-id="f3a04-163">Maak een [ResourceManagementClient] [ resman_client] object met behulp van Hallo-referenties.</span><span class="sxs-lookup"><span data-stu-id="f3a04-163">Create a [ResourceManagementClient][resman_client] object by using hello credentials.</span></span>
5. <span data-ttu-id="f3a04-164">Gebruik een [ResourceManagementClient] [ resman_client] object toocreate een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="f3a04-164">Use a [ResourceManagementClient][resman_client] object toocreate a resource group.</span></span>
6. <span data-ttu-id="f3a04-165">Gebruik een [BatchManagementClient] [ net_mgmt_client] object tooperform verschillende bewerkingen van de Batch-account:</span><span class="sxs-lookup"><span data-stu-id="f3a04-165">Use a [BatchManagementClient][net_mgmt_client] object tooperform several Batch account operations:</span></span>
   * <span data-ttu-id="f3a04-166">Maak een Batch-account in de nieuwe resourcegroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="f3a04-166">Create a Batch account in hello new resource group.</span></span>
   * <span data-ttu-id="f3a04-167">Hallo-account zojuist hebt gemaakt van Hallo Batch-service ophalen.</span><span class="sxs-lookup"><span data-stu-id="f3a04-167">Get hello newly created account from hello Batch service.</span></span>
   * <span data-ttu-id="f3a04-168">Hallo-toegangscodes voor het nieuwe account Hallo afdrukken.</span><span class="sxs-lookup"><span data-stu-id="f3a04-168">Print hello account keys for hello new account.</span></span>
   * <span data-ttu-id="f3a04-169">Een nieuwe primaire sleutel voor Hallo account opnieuw genereren.</span><span class="sxs-lookup"><span data-stu-id="f3a04-169">Regenerate a new primary key for hello account.</span></span>
   * <span data-ttu-id="f3a04-170">Hallo Quotuminformatie voor Hallo account afdrukken.</span><span class="sxs-lookup"><span data-stu-id="f3a04-170">Print hello quota information for hello account.</span></span>
   * <span data-ttu-id="f3a04-171">Hallo Quotuminformatie voor Hallo abonnement afdrukken.</span><span class="sxs-lookup"><span data-stu-id="f3a04-171">Print hello quota information for hello subscription.</span></span>
   * <span data-ttu-id="f3a04-172">Alle accounts binnen Hallo abonnement afdrukken.</span><span class="sxs-lookup"><span data-stu-id="f3a04-172">Print all accounts within hello subscription.</span></span>
   * <span data-ttu-id="f3a04-173">Gemaakte account verwijderen.</span><span class="sxs-lookup"><span data-stu-id="f3a04-173">Delete newly created account.</span></span>
7. <span data-ttu-id="f3a04-174">Hallo-resourcegroep verwijderen.</span><span class="sxs-lookup"><span data-stu-id="f3a04-174">Delete hello resource group.</span></span>

<span data-ttu-id="f3a04-175">Voordat u Hallo nieuwe Batch-account en resource groep verwijdert, kunt u deze bekijken in Hallo [Azure-portal][azure_portal]:</span><span class="sxs-lookup"><span data-stu-id="f3a04-175">Before deleting hello newly created Batch account and resource group, you can view them in hello [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="f3a04-176">Hallo-voorbeeldtoepassing toorun is, moet u eerst registreren deze met uw Azure AD-tenant in hello Azure portal en verleen machtigingen-toohello Azure Resource Manager-API.</span><span class="sxs-lookup"><span data-stu-id="f3a04-176">toorun hello sample application successfully, you must first register it with your Azure AD tenant in hello Azure portal and grant permissions toohello Azure Resource Manager API.</span></span> <span data-ttu-id="f3a04-177">Volg de stappen Hallo in [oplossingen voor het beheer van Batch verifiëren met Active Directory](batch-aad-auth-management.md).</span><span class="sxs-lookup"><span data-stu-id="f3a04-177">Follow hello steps provided in [Authenticate Batch Management solutions with Active Directory](batch-aad-auth-management.md).</span></span>


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
