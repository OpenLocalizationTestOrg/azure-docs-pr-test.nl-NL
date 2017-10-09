---
title: Service Fabric programmatische schalen aaaAzure | Microsoft Docs
description: Een Azure Service Fabric-cluster in- of schalen Volgens programmatisch toocustom triggers
services: service-fabric
documentationcenter: .net
author: mjrousos
manager: jonjung
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: mikerou
ms.openlocfilehash: a0c6499b1a143a173006248cf8a15380632637e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-service-fabric-cluster-programmatically"></a>Een Service Fabric-cluster via een programma schalen 

De grondbeginselen van Service Fabric-cluster schalen in Azure worden behandeld in de documentatie op [clusterschaling](./service-fabric-cluster-scale-up-down.md). Dit artikel bevat informatie over hoe Service Fabric-clusters zijn gebaseerd op de virtuele-machineschaalsets en kunnen worden geschaald, hetzij handmatig, hetzij met regels voor automatisch schalen. Dit document wordt bekeken programmatische van coördinerende Azure vergroten/verkleinen bewerkingen meer geavanceerde scenario's. 

## <a name="reasons-for-programmatic-scaling"></a>Redenen voor het schalen van programmatische
In veel scenario's vindt u goed oplossingen handmatig of via regels voor automatisch schalen. In andere scenario's, maar ze mogelijk niet Hallo rechts past. Mogelijke nadelen toothese methoden zijn:

- Handmatig schalen, moet u toolog in en expliciet aanvraag operations schalen. Als vergroten/verkleinen bewerkingen vaak vereist of onvoorspelbare tijde zijn, is deze benadering mogelijk geen een goede oplossing.
- Wanneer automatisch schalen regels een exemplaar van een virtuele-machineschaalset verwijdert, verwijdert ze niet automatisch kennis van dat knooppunt uit Hallo gekoppeld Service Fabric-cluster tenzij Hallo knooppunttype een niveau duurzaamheid van zilver of goud heeft. Omdat automatisch schalen regels werken op Hallo schaal instellen (in plaats van op Hallo Service Fabric-niveau), kunnen regels voor automatisch schalen Service Fabric-knooppunten verwijderen zonder afgesloten ze. Het verwijderen van ruwe knooppunt laat 'ghost' status van Service Fabric-knooppunt achter na scale-in-bewerkingen. Een persoon (of een service) nodig tooperiodically opruimen van de status van het verwijderde knooppunt in Hallo Service Fabric-cluster.
  - Let op: een knooppunttype met een serviceniveau duurzaamheid goud of zilver automatisch opschonen van de wordt knooppunten verwijderd.  
- Er is wel [veel metrische gegevens](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md) wordt ondersteund door regels voor automatisch schalen, is nog steeds een beperkte set. Als uw scenario aanroept voor schalen op basis van bepaalde metriek niet behandeld in deze groep, klikt u vervolgens regels voor automatisch schalen niet mogelijk een goede optie.

Op basis van deze beperkingen, kunt u desgewenst tooimplement meer aangepaste automatisch vergroten/verkleinen modellen. 

## <a name="scaling-apis"></a>Schalen van API 's
Azure-API's bestaan waarmee toepassingen tooprogrammatically werken met virtuele-machineschaalsets en Service Fabric-clusters. Als de bestaande opties voor automatisch schalen voor uw scenario niet werken, kunnen u deze API's mogelijk tooimplement aangepaste vergroten/verkleinen logica. 

Een aanpak tooimplementing dit 'home-' Automatische schaling gemaakt functionaliteit tooadd is een nieuwe staatloze service toohello Service Fabric-toepassing toomanage operations schalen. Binnen Hallo-service `RunAsync` methode, een verzameling van triggers kan bepalen of schalen vereist is (inclusief parameters zoals maximale clustergrootte controleren en cooldowns schalen).   

Hallo API die wordt gebruikt voor de virtuele machine scale set interacties (zowel toocheck Hallo Huidig aantal exemplaren van de virtuele machine en toomodify deze) is Hallo [beheersen Azure Management Compute-bibliotheek](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/). Hallo beheersen compute-bibliotheek biedt een API eenvoudig te gebruiken voor interactie met de virtuele-machineschaalsets.

toointeract met Hallo Service Fabric-cluster zelf, gebruik [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).

Hallo schalen code hoeft natuurlijk niet toorun als een service in Hallo cluster toobe geschaald. Beide `IAzure` en `FabricClient` kunt tootheir gekoppeld Azure-resources op afstand verbinding maken, dus Hallo service schalen kan eenvoudig een consoletoepassing of de Windows-service uitvoert vanuit externe Hallo Service Fabric-toepassing. 

## <a name="credential-management"></a>Beheer van referenties
Eén uitdaging van het schrijven van een service toohandle schalen is Hallo-service moet kunnen tooaccess virtuele machine scale set resources zonder een interactieve aanmelding. Toegang tot Service Fabric Hallo cluster is eenvoudig als Hallo service schalen aan in een eigen Service Fabric-toepassing wijzigingen brengt, maar referenties nodig tooaccess zijn Hallo schaalset. toolog in kunt u een [service-principal](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) gemaakt met de Hallo [Azure CLI 2.0](https://github.com/azure/azure-cli).

Een service-principal kan worden gemaakt met de Hallo stappen te volgen:

1. Meld u bij toohello Azure CLI (`az login`) ingesteld als een gebruiker met toegang toohello virtuele-machineschaalset
2. Hallo service principal met de maken`az ad sp create-for-rbac`
    1. Noteer Hallo appId (client-ID elders genoemd), naam, wachtwoord en tenant voor later gebruik.
    2. U moet ook uw abonnements-ID kan worden bekeken met`az account list`

Hallo beheersen compute-bibliotheek kan zich aanmelden met deze referenties als volgt (Houd er rekening mee dat core beheersen Azure typen, zoals `IAzure` zijn in Hallo [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) pakket):

```C#
var credentials = new AzureCredentials(new ServicePrincipalLoginInformation {
                ClientId = AzureClientId,
                ClientSecret = 
                AzureClientKey }, AzureTenantId, AzureEnvironment.AzureGlobalCloud);
IAzure AzureClient = Azure.Authenticate(credentials).WithSubscription(AzureSubscriptionId);

if (AzureClient?.SubscriptionId == AzureSubscriptionId)
{
    ServiceEventSource.Current.ServiceMessage(Context, "Successfully logged into Azure");
}
else
{
    ServiceEventSource.Current.ServiceMessage(Context, "ERROR: Failed toologin tooAzure");
}
```

Nadat u bent aangemeld, scale set-exemplaren kan worden opgevraagd `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.

## <a name="scaling-out"></a>Uitschalen
Hallo beheersen met Azure SDK compute, exemplaren toohello virtuele-machineschaalset ingesteld met een paar aanroepen - kunnen worden toegevoegd

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);
var newCapacity = (int)Math.Min(MaximumNodeCount, scaleSet.Capacity + 1);
scaleSet.Update().WithCapacity(newCapacity).Apply(); 
``` 

U kunt ook kan de grootte van virtuele machine scale set ook worden beheerd met PowerShell-cmdlets. [`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss)Hallo virtuele machine schaalobject set kunnen worden opgehaald. de huidige capaciteit Hallo worden opgeslagen in Hallo `.sku.capacity` eigenschap. Na het wijzigen van Hallo capaciteit toohello waarde gewenst, Hallo virtuele-machineschaalset instellen in Azure kan worden bijgewerkt met de Hallo [ `Update-AzureRmVmss` ](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss) opdracht.

Zoals wanneer een knooppunt handmatig toe te voegen, toe te voegen een schaalset exemplaar moet alle dat benodigde toostart een nieuwe Service Fabric-knooppunt omdat Hallo sjabloon bevat schaalset join extensies tooautomatically nieuwe exemplaren toohello Service Fabric-cluster. 

## <a name="scaling-in"></a>Schalen in

Schalen is vergelijkbaar tooscaling uit. Hallo werkelijke virtuele-machineschaalset wijzigingen zijn vrijwel Hallo dezelfde. Maar zoals eerder is besproken, Service Fabric alleen automatisch opgeruimd verwijderde knooppunten met een duurzaamheid van goud of zilver. Dus in Hallo Brons duurzaamheid schaal in geval, is het nodig toointeract Hello Service Fabric-cluster tooshut omlaag Hallo knooppunt toobe verwijderd en vervolgens tooremove de status.

Hallo knooppunt voorbereiden voor afsluiten omvat het zoeken naar Hallo knooppunt toobe verwijderd (Hallo laatst toegevoegde knooppunt) en het deactiveren. Voor niet-seed-knooppunten nieuwere knooppunten kunnen worden gevonden door te vergelijken `NodeInstanceId`. 

```C#
using (var client = new FabricClient())
{
    var mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync())
        .Where(n => n.NodeType.Equals(NodeTypeToScale, StringComparison.OrdinalIgnoreCase))
        .Where(n => n.NodeStatus == System.Fabric.Query.NodeStatus.Up)
        .OrderByDescending(n => n.NodeInstanceId)
        .FirstOrDefault();
```

Houd er rekening mee dat *seed* knooppunten niet goed lijken tooalways volgen Hallo-conventie groter exemplaar-id's op de eerst worden verwijderd.

Zodra het Hallo knooppunt toobe verwijderd wordt gevonden, kunnen worden gedeactiveerd en dezelfde met behulp van verwijderde Hallo `FabricClient` exemplaar en Hallo `IAzure` exemplaar van eerder.

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);

// Remove hello node from hello Service Fabric cluster
ServiceEventSource.Current.ServiceMessage(Context, $"Disabling node {mostRecentLiveNode.NodeName}");
await client.ClusterManager.DeactivateNodeAsync(mostRecentLiveNode.NodeName, NodeDeactivationIntent.RemoveNode);

// Wait (up tooa timeout) for hello node toogracefully shutdown
var timeout = TimeSpan.FromMinutes(5);
var waitStart = DateTime.Now;
while ((mostRecentLiveNode.NodeStatus == System.Fabric.Query.NodeStatus.Up || mostRecentLiveNode.NodeStatus == System.Fabric.Query.NodeStatus.Disabling) &&
        DateTime.Now - waitStart < timeout)
{
    mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync()).FirstOrDefault(n => n.NodeName == mostRecentLiveNode.NodeName);
    await Task.Delay(10 * 1000);
}

// Decrement VMSS capacity
var newCapacity = (int)Math.Max(MinimumNodeCount, scaleSet.Capacity - 1); // Check min count 

scaleSet.Update().WithCapacity(newCapacity).Apply(); 
```

Als met het uitbreiden van de PowerShell-cmdlets voor het wijzigen van de virtuele-machineschaalset kan set capaciteit ook hier worden gebruikt als een scripting benadering de voorkeur verdient. Zodra de instantie van de virtuele machine hello wordt verwijderd, kan de status van Service Fabric-knooppunt kan worden verwijderd.

```C#
await client.ClusterManager.RemoveNodeStateAsync(mostRecentLiveNode.NodeName);
```

## <a name="potential-drawbacks"></a>Nadelen

Zoals wordt beschreven in voorgaande codefragmenten hello, biedt maken van uw eigen vergroten/verkleinen service grootste mate van controle en aanpassingsmogelijkheden via uw toepassing hello gedrag de schaal. Dit kan handig zijn voor scenario's waarin u nauwkeurige controle over hoe of wanneer een toepassing wordt geschaald in- of nodig zijn. Dit besturingselement is voorzien van een afweging van complexiteit bij de code. Met deze benadering betekent dat u moet tooown code, die niet-triviale is schalen.

Hoe moet u benadert Service Fabric schalen, is afhankelijk van uw scenario. Als schalen is ongewoon, Hallo mogelijkheid tooadd of verwijder knooppunten handmatig is waarschijnlijk voldoende. Voor complexere scenario's, regels voor automatisch schalen en SDK's Hallo mogelijkheid tooscale programmatisch blootstellen bieden krachtige alternatieven.

## <a name="next-steps"></a>Volgende stappen

tooget gestart met het implementeren van uw eigen logica automatisch schalen, Maak uzelf bekend met Hallo concepten en nuttig API's te volgen:

- [Handmatig of automatisch schalen regels schalen](./service-fabric-cluster-scale-up-down.md)
- [Beheersen Azure Management-bibliotheken voor .NET](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (dit is nuttig voor interactie met een Service Fabric-cluster onderliggende virtuele-machineschaalsets)
- [System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (dit is nuttig voor interactie met een Service Fabric-cluster en de knooppunten ervan)
