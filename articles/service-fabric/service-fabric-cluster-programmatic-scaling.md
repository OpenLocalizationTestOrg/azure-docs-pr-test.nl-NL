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
# <a name="scale-a-service-fabric-cluster-programmatically"></a><span data-ttu-id="6244d-103">Een Service Fabric-cluster via een programma schalen</span><span class="sxs-lookup"><span data-stu-id="6244d-103">Scale a Service Fabric cluster programmatically</span></span> 

<span data-ttu-id="6244d-104">De grondbeginselen van Service Fabric-cluster schalen in Azure worden behandeld in de documentatie op [clusterschaling](./service-fabric-cluster-scale-up-down.md).</span><span class="sxs-lookup"><span data-stu-id="6244d-104">Fundamentals of scaling a Service Fabric cluster in Azure are covered in documentation on [cluster scaling](./service-fabric-cluster-scale-up-down.md).</span></span> <span data-ttu-id="6244d-105">Dit artikel bevat informatie over hoe Service Fabric-clusters zijn gebaseerd op de virtuele-machineschaalsets en kunnen worden geschaald, hetzij handmatig, hetzij met regels voor automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="6244d-105">That article covers how Service Fabric clusters are built on top of virtual machine scale sets and can be scaled either manually or with auto-scale rules.</span></span> <span data-ttu-id="6244d-106">Dit document wordt bekeken programmatische van coördinerende Azure vergroten/verkleinen bewerkingen meer geavanceerde scenario's.</span><span class="sxs-lookup"><span data-stu-id="6244d-106">This document looks at programmatic methods of coordinating Azure scaling operations for more advanced scenarios.</span></span> 

## <a name="reasons-for-programmatic-scaling"></a><span data-ttu-id="6244d-107">Redenen voor het schalen van programmatische</span><span class="sxs-lookup"><span data-stu-id="6244d-107">Reasons for programmatic scaling</span></span>
<span data-ttu-id="6244d-108">In veel scenario's vindt u goed oplossingen handmatig of via regels voor automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="6244d-108">In many scenarios, scaling manually or via auto-scale rules are good solutions.</span></span> <span data-ttu-id="6244d-109">In andere scenario's, maar ze mogelijk niet Hallo rechts past.</span><span class="sxs-lookup"><span data-stu-id="6244d-109">In other scenarios, though, they may not be hello right fit.</span></span> <span data-ttu-id="6244d-110">Mogelijke nadelen toothese methoden zijn:</span><span class="sxs-lookup"><span data-stu-id="6244d-110">Potential drawbacks toothese approaches include:</span></span>

- <span data-ttu-id="6244d-111">Handmatig schalen, moet u toolog in en expliciet aanvraag operations schalen.</span><span class="sxs-lookup"><span data-stu-id="6244d-111">Manually scaling requires you toolog in and explicitly request scaling operations.</span></span> <span data-ttu-id="6244d-112">Als vergroten/verkleinen bewerkingen vaak vereist of onvoorspelbare tijde zijn, is deze benadering mogelijk geen een goede oplossing.</span><span class="sxs-lookup"><span data-stu-id="6244d-112">If scaling operations are required frequently or at unpredictable times, this approach may not be a good solution.</span></span>
- <span data-ttu-id="6244d-113">Wanneer automatisch schalen regels een exemplaar van een virtuele-machineschaalset verwijdert, verwijdert ze niet automatisch kennis van dat knooppunt uit Hallo gekoppeld Service Fabric-cluster tenzij Hallo knooppunttype een niveau duurzaamheid van zilver of goud heeft.</span><span class="sxs-lookup"><span data-stu-id="6244d-113">When auto-scale rules remove an instance from a virtual machine scale set, they do not automatically remove knowledge of that node from hello associated Service Fabric cluster unless hello node type has a durability level of Silver or Gold.</span></span> <span data-ttu-id="6244d-114">Omdat automatisch schalen regels werken op Hallo schaal instellen (in plaats van op Hallo Service Fabric-niveau), kunnen regels voor automatisch schalen Service Fabric-knooppunten verwijderen zonder afgesloten ze.</span><span class="sxs-lookup"><span data-stu-id="6244d-114">Because auto-scale rules work at hello scale set level (rather than at hello Service Fabric level), auto-scale rules can remove Service Fabric nodes without shutting them down gracefully.</span></span> <span data-ttu-id="6244d-115">Het verwijderen van ruwe knooppunt laat 'ghost' status van Service Fabric-knooppunt achter na scale-in-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="6244d-115">This rude node removal will leave 'ghost' Service Fabric node state behind after scale-in operations.</span></span> <span data-ttu-id="6244d-116">Een persoon (of een service) nodig tooperiodically opruimen van de status van het verwijderde knooppunt in Hallo Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="6244d-116">An individual (or a service) would need tooperiodically clean up removed node state in hello Service Fabric cluster.</span></span>
  - <span data-ttu-id="6244d-117">Let op: een knooppunttype met een serviceniveau duurzaamheid goud of zilver automatisch opschonen van de wordt knooppunten verwijderd.</span><span class="sxs-lookup"><span data-stu-id="6244d-117">Note that a node type with a durability level of Gold or Silver will automatically clean up removed nodes.</span></span>  
- <span data-ttu-id="6244d-118">Er is wel [veel metrische gegevens](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md) wordt ondersteund door regels voor automatisch schalen, is nog steeds een beperkte set.</span><span class="sxs-lookup"><span data-stu-id="6244d-118">Although there are [many metrics](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md) supported by auto-scale rules, it is still a limited set.</span></span> <span data-ttu-id="6244d-119">Als uw scenario aanroept voor schalen op basis van bepaalde metriek niet behandeld in deze groep, klikt u vervolgens regels voor automatisch schalen niet mogelijk een goede optie.</span><span class="sxs-lookup"><span data-stu-id="6244d-119">If your scenario calls for scaling based on some metric not covered in that set, then auto-scale rules may not be a good option.</span></span>

<span data-ttu-id="6244d-120">Op basis van deze beperkingen, kunt u desgewenst tooimplement meer aangepaste automatisch vergroten/verkleinen modellen.</span><span class="sxs-lookup"><span data-stu-id="6244d-120">Based on these limitations, you may wish tooimplement more customized automatic scaling models.</span></span> 

## <a name="scaling-apis"></a><span data-ttu-id="6244d-121">Schalen van API 's</span><span class="sxs-lookup"><span data-stu-id="6244d-121">Scaling APIs</span></span>
<span data-ttu-id="6244d-122">Azure-API's bestaan waarmee toepassingen tooprogrammatically werken met virtuele-machineschaalsets en Service Fabric-clusters.</span><span class="sxs-lookup"><span data-stu-id="6244d-122">Azure APIs exist which allow applications tooprogrammatically work with virtual machine scale sets and Service Fabric clusters.</span></span> <span data-ttu-id="6244d-123">Als de bestaande opties voor automatisch schalen voor uw scenario niet werken, kunnen u deze API's mogelijk tooimplement aangepaste vergroten/verkleinen logica.</span><span class="sxs-lookup"><span data-stu-id="6244d-123">If existing auto-scale options don't work for your scenario, these APIs make it possible tooimplement custom scaling logic.</span></span> 

<span data-ttu-id="6244d-124">Een aanpak tooimplementing dit 'home-' Automatische schaling gemaakt functionaliteit tooadd is een nieuwe staatloze service toohello Service Fabric-toepassing toomanage operations schalen.</span><span class="sxs-lookup"><span data-stu-id="6244d-124">One approach tooimplementing this 'home-made' auto-scaling functionality is tooadd a new stateless service toohello Service Fabric application toomanage scaling operations.</span></span> <span data-ttu-id="6244d-125">Binnen Hallo-service `RunAsync` methode, een verzameling van triggers kan bepalen of schalen vereist is (inclusief parameters zoals maximale clustergrootte controleren en cooldowns schalen).</span><span class="sxs-lookup"><span data-stu-id="6244d-125">Within hello service's `RunAsync` method, a set of triggers can determine if scaling is required (including checking parameters such as maximum cluster size and scaling cooldowns).</span></span>   

<span data-ttu-id="6244d-126">Hallo API die wordt gebruikt voor de virtuele machine scale set interacties (zowel toocheck Hallo Huidig aantal exemplaren van de virtuele machine en toomodify deze) is Hallo [beheersen Azure Management Compute-bibliotheek](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/).</span><span class="sxs-lookup"><span data-stu-id="6244d-126">hello API used for virtual machine scale set interactions (both toocheck hello current number of virtual machine instances and toomodify it) is hello [fluent Azure Management Compute library](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/).</span></span> <span data-ttu-id="6244d-127">Hallo beheersen compute-bibliotheek biedt een API eenvoudig te gebruiken voor interactie met de virtuele-machineschaalsets.</span><span class="sxs-lookup"><span data-stu-id="6244d-127">hello fluent compute library provides an easy-to-use API for interacting with virtual machine scale sets.</span></span>

<span data-ttu-id="6244d-128">toointeract met Hallo Service Fabric-cluster zelf, gebruik [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).</span><span class="sxs-lookup"><span data-stu-id="6244d-128">toointeract with hello Service Fabric cluster itself, use [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).</span></span>

<span data-ttu-id="6244d-129">Hallo schalen code hoeft natuurlijk niet toorun als een service in Hallo cluster toobe geschaald.</span><span class="sxs-lookup"><span data-stu-id="6244d-129">Of course, hello scaling code doesn't need toorun as a service in hello cluster toobe scaled.</span></span> <span data-ttu-id="6244d-130">Beide `IAzure` en `FabricClient` kunt tootheir gekoppeld Azure-resources op afstand verbinding maken, dus Hallo service schalen kan eenvoudig een consoletoepassing of de Windows-service uitvoert vanuit externe Hallo Service Fabric-toepassing.</span><span class="sxs-lookup"><span data-stu-id="6244d-130">Both `IAzure` and `FabricClient` can connect tootheir associated Azure resources remotely, so hello scaling service could easily be a console application or Windows service running from outside hello Service Fabric application.</span></span> 

## <a name="credential-management"></a><span data-ttu-id="6244d-131">Beheer van referenties</span><span class="sxs-lookup"><span data-stu-id="6244d-131">Credential management</span></span>
<span data-ttu-id="6244d-132">Eén uitdaging van het schrijven van een service toohandle schalen is Hallo-service moet kunnen tooaccess virtuele machine scale set resources zonder een interactieve aanmelding.</span><span class="sxs-lookup"><span data-stu-id="6244d-132">One challenge of writing a service toohandle scaling is that hello service must be able tooaccess virtual machine scale set resources without an interactive login.</span></span> <span data-ttu-id="6244d-133">Toegang tot Service Fabric Hallo cluster is eenvoudig als Hallo service schalen aan in een eigen Service Fabric-toepassing wijzigingen brengt, maar referenties nodig tooaccess zijn Hallo schaalset.</span><span class="sxs-lookup"><span data-stu-id="6244d-133">Accessing hello Service Fabric cluster is easy if hello scaling service is modifying its own Service Fabric application, but credentials are needed tooaccess hello scale set.</span></span> <span data-ttu-id="6244d-134">toolog in kunt u een [service-principal](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) gemaakt met de Hallo [Azure CLI 2.0](https://github.com/azure/azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6244d-134">toolog in, you can use a [service principal](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) created with hello [Azure CLI 2.0](https://github.com/azure/azure-cli).</span></span>

<span data-ttu-id="6244d-135">Een service-principal kan worden gemaakt met de Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6244d-135">A service principal can be created with hello following steps:</span></span>

1. <span data-ttu-id="6244d-136">Meld u bij toohello Azure CLI (`az login`) ingesteld als een gebruiker met toegang toohello virtuele-machineschaalset</span><span class="sxs-lookup"><span data-stu-id="6244d-136">Log in toohello Azure CLI (`az login`) as a user with access toohello virtual machine scale set</span></span>
2. <span data-ttu-id="6244d-137">Hallo service principal met de maken`az ad sp create-for-rbac`</span><span class="sxs-lookup"><span data-stu-id="6244d-137">Create hello service principal with `az ad sp create-for-rbac`</span></span>
    1. <span data-ttu-id="6244d-138">Noteer Hallo appId (client-ID elders genoemd), naam, wachtwoord en tenant voor later gebruik.</span><span class="sxs-lookup"><span data-stu-id="6244d-138">Make note of hello appId (called 'client ID' elsewhere), name, password, and tenant for later use.</span></span>
    2. <span data-ttu-id="6244d-139">U moet ook uw abonnements-ID kan worden bekeken met`az account list`</span><span class="sxs-lookup"><span data-stu-id="6244d-139">You will also need your subscription ID, which can be viewed with `az account list`</span></span>

<span data-ttu-id="6244d-140">Hallo beheersen compute-bibliotheek kan zich aanmelden met deze referenties als volgt (Houd er rekening mee dat core beheersen Azure typen, zoals `IAzure` zijn in Hallo [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) pakket):</span><span class="sxs-lookup"><span data-stu-id="6244d-140">hello fluent compute library can log in using these credentials as follows (note that core fluent Azure types like `IAzure` are in hello [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) package):</span></span>

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

<span data-ttu-id="6244d-141">Nadat u bent aangemeld, scale set-exemplaren kan worden opgevraagd `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.</span><span class="sxs-lookup"><span data-stu-id="6244d-141">Once logged in, scale set instance count can be queried via `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.</span></span>

## <a name="scaling-out"></a><span data-ttu-id="6244d-142">Uitschalen</span><span class="sxs-lookup"><span data-stu-id="6244d-142">Scaling out</span></span>
<span data-ttu-id="6244d-143">Hallo beheersen met Azure SDK compute, exemplaren toohello virtuele-machineschaalset ingesteld met een paar aanroepen - kunnen worden toegevoegd</span><span class="sxs-lookup"><span data-stu-id="6244d-143">Using hello fluent Azure compute SDK, instances can be added toohello virtual machine scale set with just a few calls -</span></span>

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);
var newCapacity = (int)Math.Min(MaximumNodeCount, scaleSet.Capacity + 1);
scaleSet.Update().WithCapacity(newCapacity).Apply(); 
``` 

<span data-ttu-id="6244d-144">U kunt ook kan de grootte van virtuele machine scale set ook worden beheerd met PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="6244d-144">Alternatively, virtual machine scale set size can also be managed with PowerShell cmdlets.</span></span> <span data-ttu-id="6244d-145">[`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss)Hallo virtuele machine schaalobject set kunnen worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="6244d-145">[`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss) can retrieve hello virtual machine scale set object.</span></span> <span data-ttu-id="6244d-146">de huidige capaciteit Hallo worden opgeslagen in Hallo `.sku.capacity` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="6244d-146">hello current capacity will be stored in hello `.sku.capacity` property.</span></span> <span data-ttu-id="6244d-147">Na het wijzigen van Hallo capaciteit toohello waarde gewenst, Hallo virtuele-machineschaalset instellen in Azure kan worden bijgewerkt met de Hallo [ `Update-AzureRmVmss` ](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss) opdracht.</span><span class="sxs-lookup"><span data-stu-id="6244d-147">After changing hello capacity toohello desired value, hello virtual machine scale set in Azure can be updated with hello [`Update-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss) command.</span></span>

<span data-ttu-id="6244d-148">Zoals wanneer een knooppunt handmatig toe te voegen, toe te voegen een schaalset exemplaar moet alle dat benodigde toostart een nieuwe Service Fabric-knooppunt omdat Hallo sjabloon bevat schaalset join extensies tooautomatically nieuwe exemplaren toohello Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="6244d-148">As when adding a node manually, adding a scale set instance should be all that's needed toostart a new Service Fabric node since hello scale set template includes extensions tooautomatically join new instances toohello Service Fabric cluster.</span></span> 

## <a name="scaling-in"></a><span data-ttu-id="6244d-149">Schalen in</span><span class="sxs-lookup"><span data-stu-id="6244d-149">Scaling in</span></span>

<span data-ttu-id="6244d-150">Schalen is vergelijkbaar tooscaling uit. Hallo werkelijke virtuele-machineschaalset wijzigingen zijn vrijwel Hallo dezelfde.</span><span class="sxs-lookup"><span data-stu-id="6244d-150">Scaling in is similar tooscaling out. hello actual virtual machine scale set changes are practically hello same.</span></span> <span data-ttu-id="6244d-151">Maar zoals eerder is besproken, Service Fabric alleen automatisch opgeruimd verwijderde knooppunten met een duurzaamheid van goud of zilver.</span><span class="sxs-lookup"><span data-stu-id="6244d-151">But, as was discussed previously, Service Fabric only automatically cleans up removed nodes with a durability of Gold or Silver.</span></span> <span data-ttu-id="6244d-152">Dus in Hallo Brons duurzaamheid schaal in geval, is het nodig toointeract Hello Service Fabric-cluster tooshut omlaag Hallo knooppunt toobe verwijderd en vervolgens tooremove de status.</span><span class="sxs-lookup"><span data-stu-id="6244d-152">So, in hello Bronze-durability scale-in case, it's necessary toointeract with hello Service Fabric cluster tooshut down hello node toobe removed and then tooremove its state.</span></span>

<span data-ttu-id="6244d-153">Hallo knooppunt voorbereiden voor afsluiten omvat het zoeken naar Hallo knooppunt toobe verwijderd (Hallo laatst toegevoegde knooppunt) en het deactiveren.</span><span class="sxs-lookup"><span data-stu-id="6244d-153">Preparing hello node for shutdown involves finding hello node toobe removed (hello most recently added node) and deactivating it.</span></span> <span data-ttu-id="6244d-154">Voor niet-seed-knooppunten nieuwere knooppunten kunnen worden gevonden door te vergelijken `NodeInstanceId`.</span><span class="sxs-lookup"><span data-stu-id="6244d-154">For non-seed nodes, newer nodes can be found by comparing `NodeInstanceId`.</span></span> 

```C#
using (var client = new FabricClient())
{
    var mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync())
        .Where(n => n.NodeType.Equals(NodeTypeToScale, StringComparison.OrdinalIgnoreCase))
        .Where(n => n.NodeStatus == System.Fabric.Query.NodeStatus.Up)
        .OrderByDescending(n => n.NodeInstanceId)
        .FirstOrDefault();
```

<span data-ttu-id="6244d-155">Houd er rekening mee dat *seed* knooppunten niet goed lijken tooalways volgen Hallo-conventie groter exemplaar-id's op de eerst worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="6244d-155">Be aware that *seed* nodes don't seem tooalways follow hello convention that greater instance IDs are removed first.</span></span>

<span data-ttu-id="6244d-156">Zodra het Hallo knooppunt toobe verwijderd wordt gevonden, kunnen worden gedeactiveerd en dezelfde met behulp van verwijderde Hallo `FabricClient` exemplaar en Hallo `IAzure` exemplaar van eerder.</span><span class="sxs-lookup"><span data-stu-id="6244d-156">Once hello node toobe removed is found, it can be deactivated and removed using hello same `FabricClient` instance and hello `IAzure` instance from earlier.</span></span>

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

<span data-ttu-id="6244d-157">Als met het uitbreiden van de PowerShell-cmdlets voor het wijzigen van de virtuele-machineschaalset kan set capaciteit ook hier worden gebruikt als een scripting benadering de voorkeur verdient.</span><span class="sxs-lookup"><span data-stu-id="6244d-157">As with scaling out, PowerShell cmdlets for modifying virtual machine scale set capacity can also be used here if a scripting approach is preferable.</span></span> <span data-ttu-id="6244d-158">Zodra de instantie van de virtuele machine hello wordt verwijderd, kan de status van Service Fabric-knooppunt kan worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="6244d-158">Once hello virtual machine instance is removed, Service Fabric node state can be removed.</span></span>

```C#
await client.ClusterManager.RemoveNodeStateAsync(mostRecentLiveNode.NodeName);
```

## <a name="potential-drawbacks"></a><span data-ttu-id="6244d-159">Nadelen</span><span class="sxs-lookup"><span data-stu-id="6244d-159">Potential drawbacks</span></span>

<span data-ttu-id="6244d-160">Zoals wordt beschreven in voorgaande codefragmenten hello, biedt maken van uw eigen vergroten/verkleinen service grootste mate van controle en aanpassingsmogelijkheden via uw toepassing hello gedrag de schaal.</span><span class="sxs-lookup"><span data-stu-id="6244d-160">As demonstrated in hello preceding code snippets, creating your own scaling service provides hello highest degree of control and customizability over your application's scaling behavior.</span></span> <span data-ttu-id="6244d-161">Dit kan handig zijn voor scenario's waarin u nauwkeurige controle over hoe of wanneer een toepassing wordt geschaald in- of nodig zijn. Dit besturingselement is voorzien van een afweging van complexiteit bij de code.</span><span class="sxs-lookup"><span data-stu-id="6244d-161">This can be useful for scenarios requiring precise control over when or how an application scales in or out. However, this control comes with a tradeoff of code complexity.</span></span> <span data-ttu-id="6244d-162">Met deze benadering betekent dat u moet tooown code, die niet-triviale is schalen.</span><span class="sxs-lookup"><span data-stu-id="6244d-162">Using this approach means that you need tooown scaling code, which is non-trivial.</span></span>

<span data-ttu-id="6244d-163">Hoe moet u benadert Service Fabric schalen, is afhankelijk van uw scenario.</span><span class="sxs-lookup"><span data-stu-id="6244d-163">How you should approach Service Fabric scaling depends on your scenario.</span></span> <span data-ttu-id="6244d-164">Als schalen is ongewoon, Hallo mogelijkheid tooadd of verwijder knooppunten handmatig is waarschijnlijk voldoende.</span><span class="sxs-lookup"><span data-stu-id="6244d-164">If scaling is uncommon, hello ability tooadd or remove nodes manually is probably sufficient.</span></span> <span data-ttu-id="6244d-165">Voor complexere scenario's, regels voor automatisch schalen en SDK's Hallo mogelijkheid tooscale programmatisch blootstellen bieden krachtige alternatieven.</span><span class="sxs-lookup"><span data-stu-id="6244d-165">For more complex scenarios, auto-scale rules and SDKs exposing hello ability tooscale programmatically offer powerful alternatives.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6244d-166">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6244d-166">Next steps</span></span>

<span data-ttu-id="6244d-167">tooget gestart met het implementeren van uw eigen logica automatisch schalen, Maak uzelf bekend met Hallo concepten en nuttig API's te volgen:</span><span class="sxs-lookup"><span data-stu-id="6244d-167">tooget started implementing your own auto-scaling logic, familiarize yourself with hello following concepts and useful APIs:</span></span>

- [<span data-ttu-id="6244d-168">Handmatig of automatisch schalen regels schalen</span><span class="sxs-lookup"><span data-stu-id="6244d-168">Scaling manually or with auto-scale rules</span></span>](./service-fabric-cluster-scale-up-down.md)
- <span data-ttu-id="6244d-169">[Beheersen Azure Management-bibliotheken voor .NET](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (dit is nuttig voor interactie met een Service Fabric-cluster onderliggende virtuele-machineschaalsets)</span><span class="sxs-lookup"><span data-stu-id="6244d-169">[Fluent Azure Management Libraries for .NET](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (useful for interacting with a Service Fabric cluster's underlying virtual machine scale sets)</span></span>
- <span data-ttu-id="6244d-170">[System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (dit is nuttig voor interactie met een Service Fabric-cluster en de knooppunten ervan)</span><span class="sxs-lookup"><span data-stu-id="6244d-170">[System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (useful for interacting with a Service Fabric cluster and its nodes)</span></span>
