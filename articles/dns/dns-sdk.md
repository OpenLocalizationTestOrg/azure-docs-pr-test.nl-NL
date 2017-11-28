---
title: aaaCreate DNS-zones en -recordsets in met behulp van Azure DNS Hallo .NET SDK | Microsoft Docs
description: Hoe toocreate DNS-zones en record Hiermee stelt u in Azure DNS met behulp van Hallo .NET SDK.
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: eed99b87-f4d4-4fbf-a926-263f7e30b884
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/19/2016
ms.author: jonatul
ms.openlocfilehash: e3bab98b13b787427219acb7ec55e53490512fe7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-dns-zones-and-record-sets-using-hello-net-sdk"></a><span data-ttu-id="f1ce8-103">Maken van DNS-zones en -recordsets met Hallo .NET SDK</span><span class="sxs-lookup"><span data-stu-id="f1ce8-103">Create DNS zones and record sets using hello .NET SDK</span></span>

<span data-ttu-id="f1ce8-104">U kunt operations toocreate, delete of update DNS-zones, recordsets en records automatiseren met behulp van DNS-SDK met DNS-beheer van .NET-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-104">You can automate operations toocreate, delete, or update DNS zones, record sets, and records by using DNS SDK with .NET DNS Management library.</span></span> <span data-ttu-id="f1ce8-105">Er is een volledig Visual Studio-project beschikbaar [hier.](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True)</span><span class="sxs-lookup"><span data-stu-id="f1ce8-105">A full Visual Studio project is available [here.](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True)</span></span>

## <a name="create-a-service-principal-account"></a><span data-ttu-id="f1ce8-106">Het account van een service-principal maken</span><span class="sxs-lookup"><span data-stu-id="f1ce8-106">Create a service principal account</span></span>

<span data-ttu-id="f1ce8-107">Normaal gesproken krijgt toegang op programmeerniveau tooAzure resources via een speciaal account in plaats van uw eigen gebruikersreferenties.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-107">Typically, programmatic access tooAzure resources is granted via a dedicated account rather than your own user credentials.</span></span> <span data-ttu-id="f1ce8-108">Deze specifieke accounts zijn accounts 'service-principal' genoemd.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-108">These dedicated accounts are called 'service principal' accounts.</span></span> <span data-ttu-id="f1ce8-109">toouse hello Azure DNS-SDK steekproef project, u eerst een service-principalaccount toocreate nodig hebt en hieraan de juiste machtigingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-109">toouse hello Azure DNS SDK sample project, you first need toocreate a service principal account and assign it hello correct permissions.</span></span>

1. <span data-ttu-id="f1ce8-110">Ga als volgt [deze instructies](../azure-resource-manager/resource-group-authenticate-service-principal.md) toocreate een principal-serviceaccount (hello Azure DNS-SDK-voorbeeldproject wordt ervan uitgegaan dat de verificatie op basis van wachtwoorden.)</span><span class="sxs-lookup"><span data-stu-id="f1ce8-110">Follow [these instructions](../azure-resource-manager/resource-group-authenticate-service-principal.md) toocreate a service principal account (hello Azure DNS SDK sample project assumes password-based authentication.)</span></span>
2. <span data-ttu-id="f1ce8-111">Een resourcegroep maken ([Hier ziet u hoe](../azure-resource-manager/resource-group-template-deploy-portal.md)).</span><span class="sxs-lookup"><span data-stu-id="f1ce8-111">Create a resource group ([here's how](../azure-resource-manager/resource-group-template-deploy-portal.md)).</span></span>
3. <span data-ttu-id="f1ce8-112">Gebruik Azure RBAC toogrant Hallo service-principalaccount 'DNS-Zone Inzender' machtigingen toohello resourcegroep ([Hier ziet u hoe](../active-directory/role-based-access-control-configure.md).)</span><span class="sxs-lookup"><span data-stu-id="f1ce8-112">Use Azure RBAC toogrant hello service principal account 'DNS Zone Contributor' permissions toohello resource group ([here's how](../active-directory/role-based-access-control-configure.md).)</span></span>
4. <span data-ttu-id="f1ce8-113">Als u Azure DNS-SDK-voorbeeldproject hello, als volgt Hallo 'program.cs' bestand bewerken:</span><span class="sxs-lookup"><span data-stu-id="f1ce8-113">If using hello Azure DNS SDK sample project, edit hello 'program.cs' file as follows:</span></span>

   * <span data-ttu-id="f1ce8-114">Voeg de juiste waarden Hallo voor Hallo tenantId, clientId (ook wel bekend als account-ID), geheim (service-principalaccount wachtwoord) en abonnements-id gebruikt in stap 1.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-114">Insert hello correct values for hello tenantId, clientId (also known as account ID), secret (service principal account password) and subscriptionId as used in step 1.</span></span>
   * <span data-ttu-id="f1ce8-115">Voer Hallo Resourcegroepnaam gekozen in stap 2.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-115">Enter hello resource group name chosen in step 2.</span></span>
   * <span data-ttu-id="f1ce8-116">Voer een DNS-zone-naam van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-116">Enter a DNS zone name of your choice.</span></span>

## <a name="nuget-packages-and-namespace-declarations"></a><span data-ttu-id="f1ce8-117">NuGet-pakketten en naamruimtedeclaraties</span><span class="sxs-lookup"><span data-stu-id="f1ce8-117">NuGet packages and namespace declarations</span></span>

<span data-ttu-id="f1ce8-118">toouse hello Azure DNS .NET SDK, moet u tooinstall hello **Azure DNS-bibliotheek** NuGet-pakket en andere Azure-pakketten vereist.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-118">toouse hello Azure DNS .NET SDK, you need tooinstall hello **Azure DNS Management Library** NuGet package and other required Azure packages.</span></span>

1. <span data-ttu-id="f1ce8-119">In **Visual Studio**, opent u een project of een nieuw project.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-119">In **Visual Studio**, open a project or new project.</span></span>
2. <span data-ttu-id="f1ce8-120">Ga te**extra**  **>**  **NuGet Package Manager**  **>**  **NuGet-pakketten beheren voor Oplossing...** .</span><span class="sxs-lookup"><span data-stu-id="f1ce8-120">Go too**Tools** **>** **NuGet Package Manager** **>** **Manage NuGet Packages for Solution...**.</span></span>
3. <span data-ttu-id="f1ce8-121">Klik op **Bladeren**, Hallo inschakelen **Include prerelease** selectievakje, en het type **Microsoft.Azure.Management.Dns** in het zoekvak Hallo.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-121">Click **Browse**, enable hello **Include prerelease** checkbox, and type **Microsoft.Azure.Management.Dns** in hello search box.</span></span>
4. <span data-ttu-id="f1ce8-122">Selecteer Hallo pakket en klikt u op **installeren** tooadd deze tooyour Visual Studio-project.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-122">Select hello package and click **Install** tooadd it tooyour Visual Studio project.</span></span>
5. <span data-ttu-id="f1ce8-123">Herhaal de procedure Hallo hierboven tooalso installeren hello-pakketten te volgen: **Microsoft.Rest.ClientRuntime.Azure.Authentication** en **Microsoft.Azure.Management.ResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-123">Repeat hello process above tooalso install hello following packages: **Microsoft.Rest.ClientRuntime.Azure.Authentication** and **Microsoft.Azure.Management.ResourceManager**.</span></span>

## <a name="add-namespace-declarations"></a><span data-ttu-id="f1ce8-124">Naamruimtedeclaraties toevoegen</span><span class="sxs-lookup"><span data-stu-id="f1ce8-124">Add namespace declarations</span></span>

<span data-ttu-id="f1ce8-125">Hallo volgende naamruimtedeclaraties toevoegen</span><span class="sxs-lookup"><span data-stu-id="f1ce8-125">Add hello following namespace declarations</span></span>

```cs
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.Dns;
using Microsoft.Azure.Management.Dns.Models;
```

## <a name="initialize-hello-dns-management-client"></a><span data-ttu-id="f1ce8-126">Hallo DNS-management-client initialiseren</span><span class="sxs-lookup"><span data-stu-id="f1ce8-126">Initialize hello DNS management client</span></span>

<span data-ttu-id="f1ce8-127">Hallo *DnsManagementClient* Hallo methoden en de vereiste eigenschappen voor het beheren van DNS-zones en -recordsets bevat.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-127">hello *DnsManagementClient* contains hello methods and properties necessary for managing DNS zones and recordsets.</span></span>  <span data-ttu-id="f1ce8-128">Hallo volgende code wordt geregistreerd in service-principalaccount toohello en maakt een DnsManagementClient-object.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-128">hello following code logs in toohello service principal account and creates a DnsManagementClient object.</span></span>

```cs
// Build hello service credentials and DNS management client
var serviceCreds = await ApplicationTokenProvider.LoginSilentAsync(tenantId, clientId, secret);
var dnsClient = new DnsManagementClient(serviceCreds);
dnsClient.SubscriptionId = subscriptionId;
```

## <a name="create-or-update-a-dns-zone"></a><span data-ttu-id="f1ce8-129">Maken of bijwerken van een DNS-zone</span><span class="sxs-lookup"><span data-stu-id="f1ce8-129">Create or update a DNS zone</span></span>

<span data-ttu-id="f1ce8-130">een DNS-zone toocreate, eerst een 'Zone'-object gemaakt toocontain Hallo DNS-zone parameters.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-130">toocreate a DNS zone, first a "Zone" object is created toocontain hello DNS zone parameters.</span></span> <span data-ttu-id="f1ce8-131">Omdat DNS-zones die niet specifiek gebied van de gekoppelde tooa, Hallo locatie too'global ingesteld '.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-131">Because DNS zones are not linked tooa specific region, hello location is set too'global'.</span></span> <span data-ttu-id="f1ce8-132">In dit voorbeeld wordt een [Azure Resource Manager 'tag'](https://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/) toohello zone wordt ook worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-132">In this example, an [Azure Resource Manager 'tag'](https://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/) is also added toohello zone.</span></span>

<span data-ttu-id="f1ce8-133">tooactually maken of bijwerken Hallo zone in Azure DNS Hallo zone-object met Hallo zone parameters wordt doorgegeven toohello *DnsManagementClient.Zones.CreateOrUpdateAsyc* methode.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-133">tooactually create or update hello zone in Azure DNS, hello zone object containing hello zone parameters is passed toohello *DnsManagementClient.Zones.CreateOrUpdateAsyc* method.</span></span>

> [!NOTE]
> <span data-ttu-id="f1ce8-134">DnsManagementClient ondersteunt drie bewerkingsmodi: synchrone ('CreateOrUpdate'), asynchrone ('CreateOrUpdateAsync'), of asynchrone met toegang toohello HTTP-antwoord (CreateOrUpdateWithHttpMessagesAsync).</span><span class="sxs-lookup"><span data-stu-id="f1ce8-134">DnsManagementClient supports three modes of operation: synchronous ('CreateOrUpdate'), asynchronous ('CreateOrUpdateAsync'), or asynchronous with access toohello HTTP response ('CreateOrUpdateWithHttpMessagesAsync').</span></span>  <span data-ttu-id="f1ce8-135">U kunt een van deze modi, afhankelijk van de behoeften van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-135">You can choose any of these modes, depending on your application needs.</span></span>

<span data-ttu-id="f1ce8-136">Azure DNS ondersteunt optimistische gelijktijdigheid, aangeroepen [Etags](dns-getstarted-create-dnszone.md).</span><span class="sxs-lookup"><span data-stu-id="f1ce8-136">Azure DNS supports optimistic concurrency, called [Etags](dns-getstarted-create-dnszone.md).</span></span> <span data-ttu-id="f1ce8-137">In dit voorbeeld geven ' * ' voor header 'If-None-Match' hello Azure DNS toocreate een DNS-zone vertelt als deze niet al bestaat.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-137">In this example, specifying "*" for hello 'If-None-Match' header tells Azure DNS toocreate a DNS zone if one does not already exist.</span></span>  <span data-ttu-id="f1ce8-138">Hallo-aanroep mislukt als een zone met de Hallo gegeven naam al in Hallo opgegeven resourcegroep bestaat.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-138">hello call fails if a zone with hello given name already exists in hello given resource group.</span></span>

```cs
// Create zone parameters
var dnsZoneParams = new Zone("global"); // All DNS zones must have location = "global"

// Create a Azure Resource Manager 'tag'.  This is optional.  You can add multiple tags
dnsZoneParams.Tags = new Dictionary<string, string>();
dnsZoneParams.Tags.Add("dept", "finance");

// Create hello actual zone.
// Note: Uses 'If-None-Match *' ETAG check, so will fail if hello zone exists already.
// Note: For non-async usage, call dnsClient.Zones.CreateOrUpdate(resourceGroupName, zoneName, dnsZoneParams, null, "*")
// Note: For getting hello http response, call dnsClient.Zones.CreateOrUpdateWithHttpMessagesAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*")
var dnsZone = await dnsClient.Zones.CreateOrUpdateAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*");
```

## <a name="create-dns-record-sets-and-records"></a><span data-ttu-id="f1ce8-139">DNS-recordsets en records maken</span><span class="sxs-lookup"><span data-stu-id="f1ce8-139">Create DNS record sets and records</span></span>

<span data-ttu-id="f1ce8-140">DNS-records worden beheerd als een recordset.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-140">DNS records are managed as a record set.</span></span> <span data-ttu-id="f1ce8-141">Een recordset is een verzameling van records met Hallo dezelfde naam en noteert u type in een zone.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-141">A record set is a set of records with hello same name and record type within a zone.</span></span>  <span data-ttu-id="f1ce8-142">naam van de recordset Hallo is relatieve toohello zonenaam, Hallo niet volledig gekwalificeerde DNS-naam.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-142">hello record set name is relative toohello zone name, not hello fully qualified DNS name.</span></span>

<span data-ttu-id="f1ce8-143">toocreate of update een van de recordset, wordt een object van de parameters 'RecordSet' gemaakt en doorgegeven te*DnsManagementClient.RecordSets.CreateOrUpdateAsync*.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-143">toocreate or update a record set, a "RecordSet" parameters object is created and passed too*DnsManagementClient.RecordSets.CreateOrUpdateAsync*.</span></span> <span data-ttu-id="f1ce8-144">Omdat met DNS-zones, er drie bewerkingsmodi zijn: synchrone ('CreateOrUpdate'), asynchrone ('CreateOrUpdateAsync'), of asynchrone met toegang toohello HTTP-antwoord (CreateOrUpdateWithHttpMessagesAsync).</span><span class="sxs-lookup"><span data-stu-id="f1ce8-144">As with DNS zones, there are three modes of operation: synchronous ('CreateOrUpdate'), asynchronous ('CreateOrUpdateAsync'), or asynchronous with access toohello HTTP response ('CreateOrUpdateWithHttpMessagesAsync').</span></span>

<span data-ttu-id="f1ce8-145">Net als bij de DNS-zones, zijn bewerkingen op recordsets ondersteuning voor de optimistische gelijktijdigheid.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-145">As with DNS zones, operations on record sets include support for optimistic concurrency.</span></span>  <span data-ttu-id="f1ce8-146">In dit voorbeeld, omdat er geen 'If-Match' en 'If-None-Match' zijn opgegeven, wordt Hallo-Recordset altijd gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-146">In this example, since neither 'If-Match' nor 'If-None-Match' are specified, hello record set is always created.</span></span>  <span data-ttu-id="f1ce8-147">Deze aanroep overschrijft bestaande recordset Hello dezelfde naam en noteert u typt u deze DNS-zone.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-147">This call overwrites any existing record set with hello same name and record type in this DNS zone.</span></span>

```cs
// Create record set parameters
var recordSetParams = new RecordSet();
recordSetParams.TTL = 3600;

// Add records toohello record set parameter object.  In this case, we'll add a record of type 'A'
recordSetParams.ARecords = new List<ARecord>();
recordSetParams.ARecords.Add(new ARecord("1.2.3.4"));

// Add metadata toohello record set.  Similar tooAzure Resource Manager tags, this is optional and you can add multiple metadata name/value pairs
recordSetParams.Metadata = new Dictionary<string, string>();
recordSetParams.Metadata.Add("user", "Mary");

// Create hello actual record set in Azure DNS
// Note: no ETAG checks specified, will overwrite existing record set if one exists
var recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSetParams);
```

## <a name="get-zones-and-record-sets"></a><span data-ttu-id="f1ce8-148">Get-zones en -recordsets</span><span class="sxs-lookup"><span data-stu-id="f1ce8-148">Get zones and record sets</span></span>

<span data-ttu-id="f1ce8-149">Hallo *DnsManagementClient.Zones.Get* en *DnsManagementClient.RecordSets.Get* methoden afzonderlijke zones en -recordsets, respectievelijk ophalen.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-149">hello *DnsManagementClient.Zones.Get* and *DnsManagementClient.RecordSets.Get* methods retrieve individual zones and record sets, respectively.</span></span> <span data-ttu-id="f1ce8-150">RecordSets worden aangeduid met hun type, de naam en het Hallo-zone en resource groep aanwezig zijn in.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-150">RecordSets are identified by their type, name, and hello zone and resource group they exist in.</span></span> <span data-ttu-id="f1ce8-151">Zones worden aangeduid met hun naam en het Hallo resourcegroep aanwezig zijn in.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-151">Zones are identified by their name and hello resource group they exist in.</span></span>

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);
```

## <a name="update-an-existing-record-set"></a><span data-ttu-id="f1ce8-152">Een bestaande recordset bijwerken</span><span class="sxs-lookup"><span data-stu-id="f1ce8-152">Update an existing record set</span></span>

<span data-ttu-id="f1ce8-153">tooupdate een bestaande DNS-record instellen, eerst ophalen Hallo Recordset en Hallo-record bijwerken inhoud instellen, vervolgens Hallo wijziging verzenden.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-153">tooupdate an existing DNS record set, first retrieve hello record set, then update hello record set contents, then submit hello change.</span></span>  <span data-ttu-id="f1ce8-154">In dit voorbeeld opgegeven Hallo 'Etag' van het Hallo-recordset in de parameter 'If-Match' hello opgehaald.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-154">In this example, we specify hello 'Etag' from hello retrieved record set in hello 'If-Match' parameter.</span></span> <span data-ttu-id="f1ce8-155">Hallo-aanroep mislukt als een gelijktijdige bewerking Hallo-recordset in Hallo tussentijd is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-155">hello call fails if a concurrent operation has modified hello record set in hello meantime.</span></span>

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);

// Add a new record toohello local object.  Note that records in a record set must be unique/distinct
recordSet.ARecords.Add(new ARecord("5.6.7.8"));

// Update hello record set in Azure DNS
// Note: ETAG check specified, update will be rejected if hello record set has changed in hello meantime
recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSet, recordSet.Etag);
```

## <a name="list-zones-and-record-sets"></a><span data-ttu-id="f1ce8-156">Lijst met zones en -recordsets</span><span class="sxs-lookup"><span data-stu-id="f1ce8-156">List zones and record sets</span></span>

<span data-ttu-id="f1ce8-157">toolist zones, gebruik Hallo *DnsManagementClient.Zones.List...*  methoden die ondersteuning bieden voor alle zones in een opgegeven resourcegroep ofwel alle zones in een bepaald Azure-abonnement (in de verschillende resource groepen.) toolist-recordsets aanbieding, *DnsManagementClient.RecordSets.List...*  methoden die ondersteuning bieden voor een lijst met alle recordsets in een bepaald gebied of deze recordsets van een bepaald type.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-157">toolist zones, use hello *DnsManagementClient.Zones.List...* methods, which support listing either all zones in a given resource group or all zones in a given Azure subscription (across resource groups.) toolist record sets, use *DnsManagementClient.RecordSets.List...* methods, which support either listing all record sets in a given zone or only those record sets of a specific type.</span></span>

<span data-ttu-id="f1ce8-158">Houd er rekening mee wanneer zones en recordsets die het resultaat kunnen worden gepagineerd.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-158">Note when listing zones and record sets that results may be paginated.</span></span>  <span data-ttu-id="f1ce8-159">Hallo volgende voorbeeld wordt getoond hoe tooiterate via Hallo pagina's met resultaten.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-159">hello following example shows how tooiterate through hello pages of results.</span></span> <span data-ttu-id="f1ce8-160">(Een kunstmatig kleine paginagrootte van '2' gebruikte tooforce paginering; in de praktijk deze parameter moet worden weggelaten en Hallo standaard paginagrootte die wordt gebruikt.)</span><span class="sxs-lookup"><span data-stu-id="f1ce8-160">(An artificially small page size of '2' is used tooforce paging; in practice this parameter should be omitted and hello default page size used.)</span></span>

```cs
// Note: in this demo, we'll use a very small page size (2 record sets) toodemonstrate paging
// In practice, tooimprove performance you would use a large page size or just use hello system default
int recordSets = 0;
var page = await dnsClient.RecordSets.ListAllInResourceGroupAsync(resourceGroupName, zoneName, "2");
recordSets += page.Count();

while (page.NextPageLink != null)
{
    page = await dnsClient.RecordSets.ListAllInResourceGroupNextAsync(page.NextPageLink);
    recordSets += page.Count();
}
```

## <a name="next-steps"></a><span data-ttu-id="f1ce8-161">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f1ce8-161">Next steps</span></span>

<span data-ttu-id="f1ce8-162">Hallo downloaden [Azure DNS-.NET SDK-voorbeeldproject](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True), waaronder meer voorbeelden van hoe toouse hello Azure DNS-.NET SDK, inclusief voorbeelden voor andere typen DNS-records.</span><span class="sxs-lookup"><span data-stu-id="f1ce8-162">Download hello [Azure DNS .NET SDK sample project](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True), which includes further examples of how toouse hello Azure DNS .NET SDK, including examples for other DNS record types.</span></span>
