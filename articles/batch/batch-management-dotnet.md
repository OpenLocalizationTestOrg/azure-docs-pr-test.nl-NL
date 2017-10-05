---
title: Batch-account-resources beheren met de clientbibliotheek voor .NET - Azure | Microsoft Docs
description: Maken, verwijderen en wijzigen van resources van Azure Batch-account met de Batch Management .NET-bibliotheek.
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
ms.openlocfilehash: eafde9258222a2ab09ade2e366f9cc595a303dec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-batch-accounts-and-quotas-with-the-batch-management-client-library-for-net"></a><span data-ttu-id="71f2b-103">Batch-accounts en quota's met de clientbibliotheek Batch Management beheren voor .NET</span><span class="sxs-lookup"><span data-stu-id="71f2b-103">Manage Batch accounts and quotas with the Batch Management client library for .NET</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="71f2b-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="71f2b-104">Azure portal</span></span>](batch-account-create-portal.md)
> * [<span data-ttu-id="71f2b-105">Batch Management .NET</span><span class="sxs-lookup"><span data-stu-id="71f2b-105">Batch Management .NET</span></span>](batch-management-dotnet.md)
> 
> 

<span data-ttu-id="71f2b-106">U kunt verlagen onderhoud overhead in uw Azure Batch-toepassingen met behulp van de [Batch Management .NET] [ api_mgmt_net] bibliotheek voor het automatiseren van Batch-account maken, verwijderen, sleutelbeheer en quota voor detectie.</span><span class="sxs-lookup"><span data-stu-id="71f2b-106">You can lower maintenance overhead in your Azure Batch applications by using the [Batch Management .NET][api_mgmt_net] library to automate Batch account creation, deletion, key management, and quota discovery.</span></span>

* <span data-ttu-id="71f2b-107">**Batch-accounts maken en verwijderen** binnen elke regio.</span><span class="sxs-lookup"><span data-stu-id="71f2b-107">**Create and delete Batch accounts** within any region.</span></span> <span data-ttu-id="71f2b-108">Als een onafhankelijke softwareleverancier (ISV) bijvoorbeeld, u als een service voor uw clients waarin elk een afzonderlijke Batch-account is toegewezen voor facturatie bieden, kunt u de mogelijkheden voor het maken en verwijderen van het account naar de portal voor uw klant kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="71f2b-108">If, as an independent software vendor (ISV) for example, you provide a service for your clients in which each is assigned a separate Batch account for billing purposes, you can add account creation and deletion capabilities to your customer portal.</span></span>
* <span data-ttu-id="71f2b-109">**Ophalen en opnieuw genereren van sleutels** programmatisch voor uw Batch-accounts.</span><span class="sxs-lookup"><span data-stu-id="71f2b-109">**Retrieve and regenerate account keys** programmatically for any of your Batch accounts.</span></span> <span data-ttu-id="71f2b-110">Hierdoor kunt u voldoen aan het beveiligingsbeleid dat periodieke rollover of verstrijken van de sleutels worden afgedwongen.</span><span class="sxs-lookup"><span data-stu-id="71f2b-110">This can help you comply with security policies that enforce periodic rollover or expiry of account keys.</span></span> <span data-ttu-id="71f2b-111">Wanneer u meerdere Batch-accounts in verschillende Azure-regio's hebt, verhoogt de automatisering van dit proces voor de overschakeling van uw oplossing efficiëntie.</span><span class="sxs-lookup"><span data-stu-id="71f2b-111">When you have several Batch accounts in various Azure regions, automation of this rollover process increases your solution's efficiency.</span></span>
* <span data-ttu-id="71f2b-112">**Controleer de accountquota** en vindt meteen vallen en opstaan buiten te bepalen welke Batch-accounts hebt welke grenzen.</span><span class="sxs-lookup"><span data-stu-id="71f2b-112">**Check account quotas** and take the trial-and-error guesswork out of determining which Batch accounts have what limits.</span></span> <span data-ttu-id="71f2b-113">Maken van groepen of computerknooppunten toe te voegen, kunt u proactief waar aanpassen door uw account quota's controleren voordat u taken start, of wanneer deze compute resources worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="71f2b-113">By checking your account quotas before starting jobs, creating pools, or adding compute nodes, you can proactively adjust where or when these compute resources are created.</span></span> <span data-ttu-id="71f2b-114">U kunt bepalen welke accounts vereisen quotum verhoogt voordat de aanvullende resources in deze accounts toewijzen.</span><span class="sxs-lookup"><span data-stu-id="71f2b-114">You can determine which accounts require quota increases before allocating additional resources in those accounts.</span></span>
* <span data-ttu-id="71f2b-115">**Functies van andere Azure-services combineren** voor een complete beheerervaring--met behulp van Batch Management .NET [Azure Active Directory][aad_about], en de [Azure Resource Manager] [ resman_overview] samen in dezelfde toepassing.</span><span class="sxs-lookup"><span data-stu-id="71f2b-115">**Combine features of other Azure services** for a full-featured management experience--by using Batch Management .NET, [Azure Active Directory][aad_about], and the [Azure Resource Manager][resman_overview] together in the same application.</span></span> <span data-ttu-id="71f2b-116">U kunt een frictionless verificatie-ervaring, de mogelijkheid om te maken en verwijderen van resourcegroepen en de mogelijkheden die worden hier niet beschreven voor een oplossing voor end-to-end opgeven met behulp van deze functies en hun API's.</span><span class="sxs-lookup"><span data-stu-id="71f2b-116">By using these features and their APIs, you can provide a frictionless authentication experience, the ability to create and delete resource groups, and the capabilities that are described above for an end-to-end management solution.</span></span>

> [!NOTE]
> <span data-ttu-id="71f2b-117">Dit artikel is gericht op het programmatisch beheer van uw Batch-accounts, sleutels en quota's, kunt u veel van deze activiteiten uitvoeren met behulp van de [Azure-portal][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="71f2b-117">While this article focuses on the programmatic management of your Batch accounts, keys, and quotas, you can perform many of these activities by using the [Azure portal][azure_portal].</span></span> <span data-ttu-id="71f2b-118">Zie voor meer informatie [een Azure Batch-account maken met de Azure-portal](batch-account-create-portal.md) en [quota en limieten voor de Azure Batch-service](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="71f2b-118">For more information, see [Create an Azure Batch account using the Azure portal](batch-account-create-portal.md) and [Quotas and limits for the Azure Batch service](batch-quota-limit.md).</span></span>
> 
> 

## <a name="create-and-delete-batch-accounts"></a><span data-ttu-id="71f2b-119">Batch-accounts maken en verwijderen</span><span class="sxs-lookup"><span data-stu-id="71f2b-119">Create and delete Batch accounts</span></span>
<span data-ttu-id="71f2b-120">Zoals vermeld, is een van de belangrijkste functies van de Batch-API Management maken en verwijderen van de Batch-accounts in een Azure-regio.</span><span class="sxs-lookup"><span data-stu-id="71f2b-120">As mentioned, one of the primary features of the Batch Management API is to create and delete Batch accounts in an Azure region.</span></span> <span data-ttu-id="71f2b-121">Gebruiken om dit te doen [BatchManagementClient.Account.CreateAsync] [ net_create] en [DeleteAsync][net_delete], of hun synchrone collega's.</span><span class="sxs-lookup"><span data-stu-id="71f2b-121">To do so, use [BatchManagementClient.Account.CreateAsync][net_create] and [DeleteAsync][net_delete], or their synchronous counterparts.</span></span>

<span data-ttu-id="71f2b-122">Het volgende codefragment maakt u een account, verkrijgt de nieuwe account van de Batch-service en wordt deze verwijderd.</span><span class="sxs-lookup"><span data-stu-id="71f2b-122">The following code snippet creates an account, obtains the newly created account from the Batch service, and then deletes it.</span></span> <span data-ttu-id="71f2b-123">In dit fragment en anderen in dit artikel `batchManagementClient` is een volledig geïnitialiseerd exemplaar van [BatchManagementClient][net_mgmt_client].</span><span class="sxs-lookup"><span data-stu-id="71f2b-123">In this snippet and the others in this article, `batchManagementClient` is a fully initialized instance of [BatchManagementClient][net_mgmt_client].</span></span>

```csharp
// Create a new Batch account
await batchManagementClient.Account.CreateAsync("MyResourceGroup",
    "mynewaccount",
    new BatchAccountCreateParameters() { Location = "West US" });

// Get the new account from the Batch service
AccountResource account = await batchManagementClient.Account.GetAsync(
    "MyResourceGroup",
    "mynewaccount");

// Delete the account
await batchManagementClient.Account.DeleteAsync("MyResourceGroup", account.Name);
```

> [!NOTE]
> <span data-ttu-id="71f2b-124">Toepassingen die gebruikmaken van de Batch Management .NET-bibliotheek en de klasse BatchManagementClient vereisen **servicebeheerder** of **CO-beheerder** toegang tot het abonnement dat eigenaar is van het Batch-account om te worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="71f2b-124">Applications that use the Batch Management .NET library and its BatchManagementClient class require **service administrator** or **coadministrator** access to the subscription that owns the Batch account to be managed.</span></span> <span data-ttu-id="71f2b-125">Zie voor meer informatie de [Azure Active Directory](#azure-active-directory) sectie en de [AccountManagement] [ acct_mgmt_sample] codevoorbeeld.</span><span class="sxs-lookup"><span data-stu-id="71f2b-125">For more information, see the [Azure Active Directory](#azure-active-directory) section and the [AccountManagement][acct_mgmt_sample] code sample.</span></span>
> 
> 

## <a name="retrieve-and-regenerate-account-keys"></a><span data-ttu-id="71f2b-126">Ophalen en opnieuw genereren van sleutels</span><span class="sxs-lookup"><span data-stu-id="71f2b-126">Retrieve and regenerate account keys</span></span>
<span data-ttu-id="71f2b-127">Primaire en secundaire sleutels verkrijgen van een Batch-account in uw abonnement via [ListKeysAsync][net_list_keys].</span><span class="sxs-lookup"><span data-stu-id="71f2b-127">Obtain primary and secondary account keys from any Batch account within your subscription by using [ListKeysAsync][net_list_keys].</span></span> <span data-ttu-id="71f2b-128">U kunt deze sleutels opnieuw genereren met behulp van [RegenerateKeyAsync][net_regenerate_keys].</span><span class="sxs-lookup"><span data-stu-id="71f2b-128">You can regenerate those keys by using [RegenerateKeyAsync][net_regenerate_keys].</span></span>

```csharp
// Get and print the primary and secondary keys
BatchAccountListKeyResult accountKeys =
    await batchManagementClient.Account.ListKeysAsync(
        "MyResourceGroup",
        "mybatchaccount");
Console.WriteLine("Primary key:   {0}", accountKeys.Primary);
Console.WriteLine("Secondary key: {0}", accountKeys.Secondary);

// Regenerate the primary key
BatchAccountRegenerateKeyResponse newKeys =
    await batchManagementClient.Account.RegenerateKeyAsync(
        "MyResourceGroup",
        "mybatchaccount",
        new BatchAccountRegenerateKeyParameters() {
            KeyName = AccountKeyType.Primary
            });
```

> [!TIP]
> <span data-ttu-id="71f2b-129">U kunt een werkstroom gestroomlijnde verbinding maken voor uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="71f2b-129">You can create a streamlined connection workflow for your management applications.</span></span> <span data-ttu-id="71f2b-130">Eerst moet u een toegangssleutel voor het Batch-account dat u beheren wilt met [ListKeysAsync][net_list_keys].</span><span class="sxs-lookup"><span data-stu-id="71f2b-130">First, obtain an account key for the Batch account you wish to manage with [ListKeysAsync][net_list_keys].</span></span> <span data-ttu-id="71f2b-131">Vervolgens gebruikt u deze sleutel bij het initialiseren van de Batch .NET-bibliotheek [BatchSharedKeyCredentials] [ net_sharedkeycred] klasse, die wordt gebruikt bij het initialiseren van [BatchClient][net_batch_client].</span><span class="sxs-lookup"><span data-stu-id="71f2b-131">Then, use this key when initializing the Batch .NET library's [BatchSharedKeyCredentials][net_sharedkeycred] class, which is used when initializing [BatchClient][net_batch_client].</span></span>
> 
> 

## <a name="check-azure-subscription-and-batch-account-quotas"></a><span data-ttu-id="71f2b-132">Controleer de Azure-abonnement en quota's Batch-account</span><span class="sxs-lookup"><span data-stu-id="71f2b-132">Check Azure subscription and Batch account quotas</span></span>
<span data-ttu-id="71f2b-133">Azure-abonnementen en de afzonderlijke Azure-services zoals alle Batch-standaardinstelling quota's hebt die het aantal van bepaalde diensten binnen deze beperken.</span><span class="sxs-lookup"><span data-stu-id="71f2b-133">Azure subscriptions and the individual Azure services like Batch all have default quotas that limit the number of certain entities within them.</span></span> <span data-ttu-id="71f2b-134">Zie voor de standaardquota voor Azure-abonnementen, [Azure-abonnement en Servicelimieten, quota's en beperkingen](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="71f2b-134">For the default quotas for Azure subscriptions, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span> <span data-ttu-id="71f2b-135">Zie voor de standaardquota van de Batch-service [quota en limieten voor de Azure Batch-service](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="71f2b-135">For the default quotas of the Batch service, see [Quotas and limits for the Azure Batch service](batch-quota-limit.md).</span></span> <span data-ttu-id="71f2b-136">U kunt deze quota in uw toepassingen controleren met behulp van de Batch Management .NET-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="71f2b-136">By using the Batch Management .NET library, you can check these quotas in your applications.</span></span> <span data-ttu-id="71f2b-137">Hiermee kunt u om toewijzing beslissingen te nemen voordat u accounts toevoegt of-bronnen zoals pools COMPUTE en rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="71f2b-137">This enables you to make allocation decisions before you add accounts or compute resources like pools and compute nodes.</span></span>

### <a name="check-an-azure-subscription-for-batch-account-quotas"></a><span data-ttu-id="71f2b-138">Een Azure-abonnement voor Batch-account quota's controleren</span><span class="sxs-lookup"><span data-stu-id="71f2b-138">Check an Azure subscription for Batch account quotas</span></span>
<span data-ttu-id="71f2b-139">Voordat u een Batch-account in een regio maakt, kunt u uw Azure-abonnement om te zien of u kunt een account toevoegen in deze regio zijn controleren.</span><span class="sxs-lookup"><span data-stu-id="71f2b-139">Before creating a Batch account in a region, you can check your Azure subscription to see whether you are able to add an account in that region.</span></span>

<span data-ttu-id="71f2b-140">In het onderstaande codefragment gebruiken we eerst [BatchManagementClient.Account.ListAsync] [ net_mgmt_listaccounts] ophalen van een verzameling van alle Batch-accounts die binnen een abonnement.</span><span class="sxs-lookup"><span data-stu-id="71f2b-140">In the code snippet below, we first use [BatchManagementClient.Account.ListAsync][net_mgmt_listaccounts] to get a collection of all Batch accounts that are within a subscription.</span></span> <span data-ttu-id="71f2b-141">Als we deze verzameling hebt verkregen, kunt u het bepalen hoeveel accounts zich in de doelregio.</span><span class="sxs-lookup"><span data-stu-id="71f2b-141">Once we've obtained this collection, we determine how many accounts are in the target region.</span></span> <span data-ttu-id="71f2b-142">Vervolgens we gebruiken [BatchManagementClient.Subscriptions] [ net_mgmt_subscriptions] verkrijgen van de Batch-accountquotum en bepalen hoeveel accounts (indien aanwezig) kunnen worden gemaakt in deze regio.</span><span class="sxs-lookup"><span data-stu-id="71f2b-142">Then we use [BatchManagementClient.Subscriptions][net_mgmt_subscriptions] to obtain the Batch account quota and determine how many accounts (if any) can be created in that region.</span></span>

```csharp
// Get a collection of all Batch accounts within the subscription
BatchAccountListResponse listResponse =
        await batchManagementClient.Account.ListAsync(new AccountListParameters());
IList<AccountResource> accounts = listResponse.Accounts;
Console.WriteLine("Total number of Batch accounts under subscription id {0}:  {1}",
    creds.SubscriptionId,
    accounts.Count);

// Get a count of all accounts within the target region
string region = "westus";
int accountsInRegion = accounts.Count(o => o.Location == region);

// Get the account quota for the specified region
SubscriptionQuotasGetResponse quotaResponse = await batchManagementClient.Subscriptions.GetSubscriptionQuotasAsync(region);
Console.WriteLine("Account quota for {0} region: {1}", region, quotaResponse.AccountQuota);

// Determine how many accounts can be created in the target region
Console.WriteLine("Accounts in {0}: {1}", region, accountsInRegion);
Console.WriteLine("You can create {0} accounts in the {1} region.", quotaResponse.AccountQuota - accountsInRegion, region);
```

<span data-ttu-id="71f2b-143">In het bovenstaande codefragment `creds` is een exemplaar van [TokenCloudCredentials][azure_tokencreds].</span><span class="sxs-lookup"><span data-stu-id="71f2b-143">In the snippet above, `creds` is an instance of [TokenCloudCredentials][azure_tokencreds].</span></span> <span data-ttu-id="71f2b-144">Zie voor een voorbeeld van het maken van dit object, de [AccountManagement] [ acct_mgmt_sample] codevoorbeeld op GitHub.</span><span class="sxs-lookup"><span data-stu-id="71f2b-144">To see an example of creating this object, see the [AccountManagement][acct_mgmt_sample] code sample on GitHub.</span></span>

### <a name="check-a-batch-account-for-compute-resource-quotas"></a><span data-ttu-id="71f2b-145">Een Batch-account voor compute resource quota's controleren</span><span class="sxs-lookup"><span data-stu-id="71f2b-145">Check a Batch account for compute resource quotas</span></span>
<span data-ttu-id="71f2b-146">Voordat u voor de rekenresources in uw Batch-oplossing, kunt u controleren om te controleren of de bronnen die u wilt toewijzen van het account quota won't overschrijden.</span><span class="sxs-lookup"><span data-stu-id="71f2b-146">Before increasing compute resources in your Batch solution, you can check to ensure the resources you want to allocate won't exceed the account's quotas.</span></span> <span data-ttu-id="71f2b-147">In het onderstaande codefragment we de quota-informatie voor het Batch-account met de naam afdrukken `mybatchaccount`.</span><span class="sxs-lookup"><span data-stu-id="71f2b-147">In the code snippet below, we print the quota information for the Batch account named `mybatchaccount`.</span></span> <span data-ttu-id="71f2b-148">In uw eigen toepassing kunt u deze informatie gebruiken om te bepalen of het account kan worden gebruikt voor het verwerken van de aanvullende bronnen worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="71f2b-148">In your own application, you could use such information to determine whether the account can handle the additional resources to be created.</span></span>

```csharp
// First obtain the Batch account
BatchAccountGetResponse getResponse =
    await batchManagementClient.Account.GetAsync("MyResourceGroup", "mybatchaccount");
AccountResource account = getResponse.Resource;

// Now print the compute resource quotas for the account
Console.WriteLine("Core quota: {0}", account.Properties.CoreQuota);
Console.WriteLine("Pool quota: {0}", account.Properties.PoolQuota);
Console.WriteLine("Active job and job schedule quota: {0}", account.Properties.ActiveJobAndJobScheduleQuota);
```

> [!IMPORTANT]
> <span data-ttu-id="71f2b-149">Hoewel er standaardquota voor Azure-abonnementen en services, veel van deze limieten kunnen worden gegenereerd door het uitgeven van een aanvraag in de [Azure-portal][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="71f2b-149">While there are default quotas for Azure subscriptions and services, many of these limits can be raised by issuing a request in the [Azure portal][azure_portal].</span></span> <span data-ttu-id="71f2b-150">Zie bijvoorbeeld [quota en limieten voor de Azure Batch-service](batch-quota-limit.md) voor instructies over het verhogen van de quota van uw Batch-account.</span><span class="sxs-lookup"><span data-stu-id="71f2b-150">For example, see [Quotas and limits for the Azure Batch service](batch-quota-limit.md) for instructions on increasing your Batch account quotas.</span></span>
> 
> 

## <a name="use-azure-ad-with-batch-management-net"></a><span data-ttu-id="71f2b-151">Azure AD gebruikt met Batch Management .NET</span><span class="sxs-lookup"><span data-stu-id="71f2b-151">Use Azure AD with Batch Management .NET</span></span>

<span data-ttu-id="71f2b-152">De Batch Management .NET-bibliotheek is een Azure-resource provider-client en wordt gebruikt in combinatie met [Azure Resource Manager] [ resman_overview] account om resources te beheren via een programma.</span><span class="sxs-lookup"><span data-stu-id="71f2b-152">The Batch Management .NET library is an Azure resource provider client, and is used together with [Azure Resource Manager][resman_overview] to manage account resources programmatically.</span></span> <span data-ttu-id="71f2b-153">Azure AD is vereist voor de verificatie via een Azure-resource provider-client, met inbegrip van de Batch Management .NET-bibliotheek en aanvragen [Azure Resource Manager][resman_overview].</span><span class="sxs-lookup"><span data-stu-id="71f2b-153">Azure AD is required to authenticate requests made through any Azure resource provider client, including the Batch Management .NET library, and through [Azure Resource Manager][resman_overview].</span></span> <span data-ttu-id="71f2b-154">Zie voor meer informatie over het gebruik van Azure AD met de Batch Management .NET-bibliotheek [gebruik Azure Active Directory voor het verifiëren van Batch-oplossingen](batch-aad-auth.md).</span><span class="sxs-lookup"><span data-stu-id="71f2b-154">For information about using Azure AD with the Batch Management .NET library, see [Use Azure Active Directory to authenticate Batch solutions](batch-aad-auth.md).</span></span> 

## <a name="sample-project-on-github"></a><span data-ttu-id="71f2b-155">Voorbeeld van project op GitHub</span><span class="sxs-lookup"><span data-stu-id="71f2b-155">Sample project on GitHub</span></span>

<span data-ttu-id="71f2b-156">Bekijk Batch Management .NET in actie vindt de [AccountManagment] [ acct_mgmt_sample] voorbeeldproject op GitHub.</span><span class="sxs-lookup"><span data-stu-id="71f2b-156">To see Batch Management .NET in action, check out the [AccountManagment][acct_mgmt_sample] sample project on GitHub.</span></span> <span data-ttu-id="71f2b-157">De voorbeeldtoepassing AccountManagment ziet u de volgende bewerkingen:</span><span class="sxs-lookup"><span data-stu-id="71f2b-157">The AccountManagment sample application demonstrates the following operations:</span></span>

1. <span data-ttu-id="71f2b-158">Verkrijgen van een beveiligingstoken uit Azure AD via [ADAL][aad_adal].</span><span class="sxs-lookup"><span data-stu-id="71f2b-158">Acquire a security token from Azure AD by using [ADAL][aad_adal].</span></span> <span data-ttu-id="71f2b-159">Als de gebruiker niet is al aangemeld, wordt ze gevraagd om hun Azure referenties.</span><span class="sxs-lookup"><span data-stu-id="71f2b-159">If the user is not already signed in, they are prompted for their Azure credentials.</span></span>
2. <span data-ttu-id="71f2b-160">Met het beveiligingstoken dat is verkregen van Azure AD, maken een [SubscriptionClient] [ resman_subclient] op Azure-query voor een lijst met abonnementen die zijn gekoppeld aan het account.</span><span class="sxs-lookup"><span data-stu-id="71f2b-160">With the security token obtained from Azure AD, create a [SubscriptionClient][resman_subclient] to query Azure for a list of subscriptions associated with the account.</span></span> <span data-ttu-id="71f2b-161">De gebruiker kan een abonnement uit de lijst selecteren als het bevat meer dan één abonnement.</span><span class="sxs-lookup"><span data-stu-id="71f2b-161">The user can select a subscription from the list if it contains more than one subscription.</span></span>
3. <span data-ttu-id="71f2b-162">Referenties die zijn gekoppeld aan het geselecteerde abonnement ophalen.</span><span class="sxs-lookup"><span data-stu-id="71f2b-162">Get credentials associated with the selected subscription.</span></span>
4. <span data-ttu-id="71f2b-163">Maak een [ResourceManagementClient] [ resman_client] object met de referenties.</span><span class="sxs-lookup"><span data-stu-id="71f2b-163">Create a [ResourceManagementClient][resman_client] object by using the credentials.</span></span>
5. <span data-ttu-id="71f2b-164">Gebruik een [ResourceManagementClient] [ resman_client] object om een resourcegroep te maken.</span><span class="sxs-lookup"><span data-stu-id="71f2b-164">Use a [ResourceManagementClient][resman_client] object to create a resource group.</span></span>
6. <span data-ttu-id="71f2b-165">Gebruik een [BatchManagementClient] [ net_mgmt_client] object meerdere Batch-account bewerkingen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="71f2b-165">Use a [BatchManagementClient][net_mgmt_client] object to perform several Batch account operations:</span></span>
   * <span data-ttu-id="71f2b-166">Maak een Batch-account in de nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="71f2b-166">Create a Batch account in the new resource group.</span></span>
   * <span data-ttu-id="71f2b-167">De nieuwe account ophalen van de Batch-service.</span><span class="sxs-lookup"><span data-stu-id="71f2b-167">Get the newly created account from the Batch service.</span></span>
   * <span data-ttu-id="71f2b-168">De account-sleutels voor het nieuwe account afdrukken.</span><span class="sxs-lookup"><span data-stu-id="71f2b-168">Print the account keys for the new account.</span></span>
   * <span data-ttu-id="71f2b-169">Een nieuwe primaire sleutel voor het account opnieuw genereren.</span><span class="sxs-lookup"><span data-stu-id="71f2b-169">Regenerate a new primary key for the account.</span></span>
   * <span data-ttu-id="71f2b-170">De quota-informatie voor het account afdrukken.</span><span class="sxs-lookup"><span data-stu-id="71f2b-170">Print the quota information for the account.</span></span>
   * <span data-ttu-id="71f2b-171">De quota-informatie voor het abonnement afdrukken.</span><span class="sxs-lookup"><span data-stu-id="71f2b-171">Print the quota information for the subscription.</span></span>
   * <span data-ttu-id="71f2b-172">Alle accounts binnen het abonnement afdrukken.</span><span class="sxs-lookup"><span data-stu-id="71f2b-172">Print all accounts within the subscription.</span></span>
   * <span data-ttu-id="71f2b-173">Gemaakte account verwijderen.</span><span class="sxs-lookup"><span data-stu-id="71f2b-173">Delete newly created account.</span></span>
7. <span data-ttu-id="71f2b-174">De resourcegroep verwijderen.</span><span class="sxs-lookup"><span data-stu-id="71f2b-174">Delete the resource group.</span></span>

<span data-ttu-id="71f2b-175">Voordat u de nieuwe Batch-account en resource groep verwijdert, u kunt ze weergeven in de [Azure-portal][azure_portal]:</span><span class="sxs-lookup"><span data-stu-id="71f2b-175">Before deleting the newly created Batch account and resource group, you can view them in the [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="71f2b-176">Als u wilt de voorbeeldtoepassing is uitgevoerd, moet u eerst registreren met uw Azure AD-tenant in de Azure portal en machtigingen verlenen voor de Azure Resource Manager-API.</span><span class="sxs-lookup"><span data-stu-id="71f2b-176">To run the sample application successfully, you must first register it with your Azure AD tenant in the Azure portal and grant permissions to the Azure Resource Manager API.</span></span> <span data-ttu-id="71f2b-177">Volg de stappen in [oplossingen voor het beheer van Batch verifiëren met Active Directory](batch-aad-auth-management.md).</span><span class="sxs-lookup"><span data-stu-id="71f2b-177">Follow the steps provided in [Authenticate Batch Management solutions with Active Directory](batch-aad-auth-management.md).</span></span>


<span data-ttu-id="71f2b-178">[aad_about]: ../active-directory/active-directory-whatis.md "Wat is Azure Active Directory?"</span><span class="sxs-lookup"><span data-stu-id="71f2b-178">[aad_about]: ../active-directory/active-directory-whatis.md "What is Azure Active Directory?"</span></span>
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
<span data-ttu-id="71f2b-179">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Verificatie-scenario's voor Azure AD"</span><span class="sxs-lookup"><span data-stu-id="71f2b-179">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Authentication Scenarios for Azure AD"</span></span>
<span data-ttu-id="71f2b-180">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Toepassingen integreren met Azure Active Directory"</span><span class="sxs-lookup"><span data-stu-id="71f2b-180">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrating Applications with Azure Active Directory"</span></span>
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
