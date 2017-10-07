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
# <a name="create-dns-zones-and-record-sets-using-hello-net-sdk"></a>Maken van DNS-zones en -recordsets met Hallo .NET SDK

U kunt operations toocreate, delete of update DNS-zones, recordsets en records automatiseren met behulp van DNS-SDK met DNS-beheer van .NET-bibliotheek. Er is een volledig Visual Studio-project beschikbaar [hier.](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True)

## <a name="create-a-service-principal-account"></a>Het account van een service-principal maken

Normaal gesproken krijgt toegang op programmeerniveau tooAzure resources via een speciaal account in plaats van uw eigen gebruikersreferenties. Deze specifieke accounts zijn accounts 'service-principal' genoemd. toouse hello Azure DNS-SDK steekproef project, u eerst een service-principalaccount toocreate nodig hebt en hieraan de juiste machtigingen Hallo.

1. Ga als volgt [deze instructies](../azure-resource-manager/resource-group-authenticate-service-principal.md) toocreate een principal-serviceaccount (hello Azure DNS-SDK-voorbeeldproject wordt ervan uitgegaan dat de verificatie op basis van wachtwoorden.)
2. Een resourcegroep maken ([Hier ziet u hoe](../azure-resource-manager/resource-group-template-deploy-portal.md)).
3. Gebruik Azure RBAC toogrant Hallo service-principalaccount 'DNS-Zone Inzender' machtigingen toohello resourcegroep ([Hier ziet u hoe](../active-directory/role-based-access-control-configure.md).)
4. Als u Azure DNS-SDK-voorbeeldproject hello, als volgt Hallo 'program.cs' bestand bewerken:

   * Voeg de juiste waarden Hallo voor Hallo tenantId, clientId (ook wel bekend als account-ID), geheim (service-principalaccount wachtwoord) en abonnements-id gebruikt in stap 1.
   * Voer Hallo Resourcegroepnaam gekozen in stap 2.
   * Voer een DNS-zone-naam van uw keuze.

## <a name="nuget-packages-and-namespace-declarations"></a>NuGet-pakketten en naamruimtedeclaraties

toouse hello Azure DNS .NET SDK, moet u tooinstall hello **Azure DNS-bibliotheek** NuGet-pakket en andere Azure-pakketten vereist.

1. In **Visual Studio**, opent u een project of een nieuw project.
2. Ga te**extra**  **>**  **NuGet Package Manager**  **>**  **NuGet-pakketten beheren voor Oplossing...** .
3. Klik op **Bladeren**, Hallo inschakelen **Include prerelease** selectievakje, en het type **Microsoft.Azure.Management.Dns** in het zoekvak Hallo.
4. Selecteer Hallo pakket en klikt u op **installeren** tooadd deze tooyour Visual Studio-project.
5. Herhaal de procedure Hallo hierboven tooalso installeren hello-pakketten te volgen: **Microsoft.Rest.ClientRuntime.Azure.Authentication** en **Microsoft.Azure.Management.ResourceManager**.

## <a name="add-namespace-declarations"></a>Naamruimtedeclaraties toevoegen

Hallo volgende naamruimtedeclaraties toevoegen

```cs
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.Dns;
using Microsoft.Azure.Management.Dns.Models;
```

## <a name="initialize-hello-dns-management-client"></a>Hallo DNS-management-client initialiseren

Hallo *DnsManagementClient* Hallo methoden en de vereiste eigenschappen voor het beheren van DNS-zones en -recordsets bevat.  Hallo volgende code wordt geregistreerd in service-principalaccount toohello en maakt een DnsManagementClient-object.

```cs
// Build hello service credentials and DNS management client
var serviceCreds = await ApplicationTokenProvider.LoginSilentAsync(tenantId, clientId, secret);
var dnsClient = new DnsManagementClient(serviceCreds);
dnsClient.SubscriptionId = subscriptionId;
```

## <a name="create-or-update-a-dns-zone"></a>Maken of bijwerken van een DNS-zone

een DNS-zone toocreate, eerst een 'Zone'-object gemaakt toocontain Hallo DNS-zone parameters. Omdat DNS-zones die niet specifiek gebied van de gekoppelde tooa, Hallo locatie too'global ingesteld '. In dit voorbeeld wordt een [Azure Resource Manager 'tag'](https://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/) toohello zone wordt ook worden toegevoegd.

tooactually maken of bijwerken Hallo zone in Azure DNS Hallo zone-object met Hallo zone parameters wordt doorgegeven toohello *DnsManagementClient.Zones.CreateOrUpdateAsyc* methode.

> [!NOTE]
> DnsManagementClient ondersteunt drie bewerkingsmodi: synchrone ('CreateOrUpdate'), asynchrone ('CreateOrUpdateAsync'), of asynchrone met toegang toohello HTTP-antwoord (CreateOrUpdateWithHttpMessagesAsync).  U kunt een van deze modi, afhankelijk van de behoeften van uw toepassing.

Azure DNS ondersteunt optimistische gelijktijdigheid, aangeroepen [Etags](dns-getstarted-create-dnszone.md). In dit voorbeeld geven ' * ' voor header 'If-None-Match' hello Azure DNS toocreate een DNS-zone vertelt als deze niet al bestaat.  Hallo-aanroep mislukt als een zone met de Hallo gegeven naam al in Hallo opgegeven resourcegroep bestaat.

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

## <a name="create-dns-record-sets-and-records"></a>DNS-recordsets en records maken

DNS-records worden beheerd als een recordset. Een recordset is een verzameling van records met Hallo dezelfde naam en noteert u type in een zone.  naam van de recordset Hallo is relatieve toohello zonenaam, Hallo niet volledig gekwalificeerde DNS-naam.

toocreate of update een van de recordset, wordt een object van de parameters 'RecordSet' gemaakt en doorgegeven te*DnsManagementClient.RecordSets.CreateOrUpdateAsync*. Omdat met DNS-zones, er drie bewerkingsmodi zijn: synchrone ('CreateOrUpdate'), asynchrone ('CreateOrUpdateAsync'), of asynchrone met toegang toohello HTTP-antwoord (CreateOrUpdateWithHttpMessagesAsync).

Net als bij de DNS-zones, zijn bewerkingen op recordsets ondersteuning voor de optimistische gelijktijdigheid.  In dit voorbeeld, omdat er geen 'If-Match' en 'If-None-Match' zijn opgegeven, wordt Hallo-Recordset altijd gemaakt.  Deze aanroep overschrijft bestaande recordset Hello dezelfde naam en noteert u typt u deze DNS-zone.

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

## <a name="get-zones-and-record-sets"></a>Get-zones en -recordsets

Hallo *DnsManagementClient.Zones.Get* en *DnsManagementClient.RecordSets.Get* methoden afzonderlijke zones en -recordsets, respectievelijk ophalen. RecordSets worden aangeduid met hun type, de naam en het Hallo-zone en resource groep aanwezig zijn in. Zones worden aangeduid met hun naam en het Hallo resourcegroep aanwezig zijn in.

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);
```

## <a name="update-an-existing-record-set"></a>Een bestaande recordset bijwerken

tooupdate een bestaande DNS-record instellen, eerst ophalen Hallo Recordset en Hallo-record bijwerken inhoud instellen, vervolgens Hallo wijziging verzenden.  In dit voorbeeld opgegeven Hallo 'Etag' van het Hallo-recordset in de parameter 'If-Match' hello opgehaald. Hallo-aanroep mislukt als een gelijktijdige bewerking Hallo-recordset in Hallo tussentijd is gewijzigd.

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);

// Add a new record toohello local object.  Note that records in a record set must be unique/distinct
recordSet.ARecords.Add(new ARecord("5.6.7.8"));

// Update hello record set in Azure DNS
// Note: ETAG check specified, update will be rejected if hello record set has changed in hello meantime
recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSet, recordSet.Etag);
```

## <a name="list-zones-and-record-sets"></a>Lijst met zones en -recordsets

toolist zones, gebruik Hallo *DnsManagementClient.Zones.List...*  methoden die ondersteuning bieden voor alle zones in een opgegeven resourcegroep ofwel alle zones in een bepaald Azure-abonnement (in de verschillende resource groepen.) toolist-recordsets aanbieding, *DnsManagementClient.RecordSets.List...*  methoden die ondersteuning bieden voor een lijst met alle recordsets in een bepaald gebied of deze recordsets van een bepaald type.

Houd er rekening mee wanneer zones en recordsets die het resultaat kunnen worden gepagineerd.  Hallo volgende voorbeeld wordt getoond hoe tooiterate via Hallo pagina's met resultaten. (Een kunstmatig kleine paginagrootte van '2' gebruikte tooforce paginering; in de praktijk deze parameter moet worden weggelaten en Hallo standaard paginagrootte die wordt gebruikt.)

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

## <a name="next-steps"></a>Volgende stappen

Hallo downloaden [Azure DNS-.NET SDK-voorbeeldproject](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True), waaronder meer voorbeelden van hoe toouse hello Azure DNS-.NET SDK, inclusief voorbeelden voor andere typen DNS-records.
