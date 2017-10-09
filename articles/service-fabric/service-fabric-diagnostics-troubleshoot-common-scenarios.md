---
title: aaaTroubleshooting met gebeurtenistracering | Microsoft Docs
description: Hallo meest voorkomende problemen aangetroffen tijdens het implementeren van services op Microsoft Azure Service Fabric.
services: service-fabric
documentationcenter: .net
author: mattrowmsft
manager: timlt
editor: 
ms.assetid: 5eb8ef21-da04-4ac8-8b9a-5f7ff1e0a180
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/31/2016
ms.author: mattrow
redirect_url: /azure/service-fabric/service-fabric-diagnostics-overview
ms.openlocfilehash: f5adb7e15fa1e2c964bbbc5726246630c95e13f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-common-issues-when-you-deploy-services-on-azure-service-fabric"></a><span data-ttu-id="731bd-103">Algemene problemen bij het implementeren van services op Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="731bd-103">Troubleshoot common issues when you deploy services on Azure Service Fabric</span></span>
<span data-ttu-id="731bd-104">Wanneer u services op uw computer developer uitvoert, is het eenvoudig toouse [de hulpprogramma's voor foutopsporing van Visual Studio](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="731bd-104">When you're running services on your developer computer, it is easy toouse [Visual Studio's debugging tools](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span> <span data-ttu-id="731bd-105">Voor externe clusters [statusrapporten](service-fabric-view-entities-aggregated-health.md) zijn altijd een goede plaats toostart.</span><span class="sxs-lookup"><span data-stu-id="731bd-105">For remote clusters, [health reports](service-fabric-view-entities-aggregated-health.md) are always a good place toostart.</span></span> <span data-ttu-id="731bd-106">Hallo eenvoudigste manieren tooaccess deze rapporten via PowerShell zijn of [SFX](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="731bd-106">hello easiest ways tooaccess these reports are through PowerShell or [SFX](service-fabric-visualizing-your-cluster.md).</span></span> <span data-ttu-id="731bd-107">In dit artikel wordt ervan uitgegaan dat u een extern Clusterbeheer zijn foutopsporing en basiskennis van hoe u een van deze hulpprogramma's voor toouse.</span><span class="sxs-lookup"><span data-stu-id="731bd-107">This article assumes that you are debugging a remote cluster and have a basic understanding of how toouse either of these tools.</span></span>

## <a name="application-crash"></a><span data-ttu-id="731bd-108">De toepassing is vastgelopen</span><span class="sxs-lookup"><span data-stu-id="731bd-108">Application crash</span></span>
<span data-ttu-id="731bd-109">Hallo ' partitie is lager dan aantal replica of het exemplaar als doel ' rapport is een goede indicatie die uw service is gecrasht.</span><span class="sxs-lookup"><span data-stu-id="731bd-109">hello "Partition is below target replica or instance count" report is a good indication that your service is crashing.</span></span> <span data-ttu-id="731bd-110">toofind uit waar de service is gecrasht duurt nog iets meer onderzoek.</span><span class="sxs-lookup"><span data-stu-id="731bd-110">toofind out where your service is crashing takes a little more investigation.</span></span> <span data-ttu-id="731bd-111">Als uw service wordt uitgevoerd op grote schaal, is de beste vriend een reeks goed doordacht traceringen.</span><span class="sxs-lookup"><span data-stu-id="731bd-111">When your service is running at scale, your best friend will be a set of well-thought-out traces.</span></span>  <span data-ttu-id="731bd-112">We raden aan dat u probeert [Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) voor het verzamelen van deze traceringen en gebruik van een oplossing zoals [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) voor het weergeven en zoeken Hallo traceringen.</span><span class="sxs-lookup"><span data-stu-id="731bd-112">We suggest that you try [Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) for collecting those traces and using a solution such as [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) for viewing and searching hello traces.</span></span>

![SFX partitie Health](./media/service-fabric-diagnostics-troubleshoot-common-scenarios/crashNewApp.png)

### <a name="during-service-or-actor-initialization"></a><span data-ttu-id="731bd-114">Tijdens de initialisatie van de service of actor</span><span class="sxs-lookup"><span data-stu-id="731bd-114">During service or actor initialization</span></span>
<span data-ttu-id="731bd-115">Eventuele uitzonderingen voordat Hallo servicetype is geïnitialiseerd, wordt Hallo proces toocrash.</span><span class="sxs-lookup"><span data-stu-id="731bd-115">Any exceptions before hello service type is initialized will cause hello process toocrash.</span></span> <span data-ttu-id="731bd-116">Voor deze typen crashes weergegeven logboek voor toepassingsgebeurtenissen Hallo Hallo-fout opgetreden in de service.</span><span class="sxs-lookup"><span data-stu-id="731bd-116">For these types of crashes, hello application event log will show hello error from your service.</span></span>
<span data-ttu-id="731bd-117">Dit zijn de meest voorkomende uitzonderingen toosee Hallo voordat het Hallo-service is geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="731bd-117">These are hello most common exceptions toosee before hello service is initialized.</span></span>

<span data-ttu-id="731bd-118">***System.IO.FileNotFoundException***</span><span class="sxs-lookup"><span data-stu-id="731bd-118">***System.IO.FileNotFoundException***</span></span>

<span data-ttu-id="731bd-119">Deze fout wordt vaak vanwege toomissing assembly-afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="731bd-119">This error is often due toomissing assembly dependencies.</span></span> <span data-ttu-id="731bd-120">Controleer Hallo CopyLocal eigenschap in Visual Studio of Hallo globale assembly-cache voor het Hallo-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="731bd-120">Check hello CopyLocal property in Visual Studio or hello global assembly cache for hello node.</span></span>

<span data-ttu-id="731bd-121">***System.Runtime.InteropServices.COMException*** *op System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory (IntPtr, IFabricStatefulServiceFactory)*</span><span class="sxs-lookup"><span data-stu-id="731bd-121">***System.Runtime.InteropServices.COMException*** *at System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory(IntPtr, IFabricStatefulServiceFactory)*</span></span>

 <span data-ttu-id="731bd-122">Hiermee wordt aangegeven met die naam Hallo geregistreerde service type komt niet overeen met de Hallo servicemanifest.</span><span class="sxs-lookup"><span data-stu-id="731bd-122">This indicates that hello registered service type name does not match hello service manifest.</span></span>

<span data-ttu-id="731bd-123">[Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) geconfigureerde tooupload Hallo logboek voor toepassingsgebeurtenissen voor alle knooppunten in uw automatisch kan worden.</span><span class="sxs-lookup"><span data-stu-id="731bd-123">[Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) can be configured tooupload hello application event log for all your nodes automatically.</span></span>

### <a name="runasync-or-onactivateasync"></a><span data-ttu-id="731bd-124">RunAsync() of OnActivateAsync()</span><span class="sxs-lookup"><span data-stu-id="731bd-124">RunAsync() or OnActivateAsync()</span></span>
<span data-ttu-id="731bd-125">Als Hallo crash tijdens de initialisatie van de Hallo gebeurt of van uw geregistreerde servicetype of actor wordt uitgevoerd, Hallo uitzondering wordt onderschept door Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="731bd-125">If hello crash happens during hello initialization or running of your registered service type or actor, hello exception will be caught by Azure Service Fabric.</span></span> <span data-ttu-id="731bd-126">U kunt deze van Hallo EventSource providers uiteengezet in de sectie 'Volgende stappen' hello weergeven.</span><span class="sxs-lookup"><span data-stu-id="731bd-126">You can view these from hello EventSource providers detailed in hello "Next steps" section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="731bd-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="731bd-127">Next steps</span></span>
<span data-ttu-id="731bd-128">Meer informatie over bestaande diagnostische gegevens die worden geleverd door de Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="731bd-128">Learn more about existing diagnostics provided by Service Fabric:</span></span>

* [<span data-ttu-id="731bd-129">Betrouwbare actoren diagnostische gegevens</span><span class="sxs-lookup"><span data-stu-id="731bd-129">Reliable Actors diagnostics</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="731bd-130">Betrouwbare diagnostische gegevens voor Services</span><span class="sxs-lookup"><span data-stu-id="731bd-130">Reliable Services diagnostics</span></span>](service-fabric-reliable-services-diagnostics.md)

