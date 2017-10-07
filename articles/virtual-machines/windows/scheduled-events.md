---
title: aaaScheduled gebeurtenissen voor Windows-machines in Azure | Microsoft Docs
description: Geplande gebeurtenissen met Hallo metagegevens van de Azure-service voor op uw Windows virtuele machines.
services: virtual-machines-windows, virtual-machines-linux, cloud-services
documentationcenter: 
author: zivraf
manager: timlt
editor: 
tags: 
ms.assetid: 28d8e1f2-8e61-4fbe-bfe8-80a68443baba
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/14/2017
ms.author: zivr
ms.openlocfilehash: c9f5f332a5d77e8d54d1ae8bdaadafc1a14f3b77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-metadata-service-scheduled-events-preview-for-windows-vms"></a><span data-ttu-id="8a283-103">Azure Service metagegevens: Geplande gebeurtenissen (Preview) voor Windows-VM 's</span><span class="sxs-lookup"><span data-stu-id="8a283-103">Azure Metadata Service: Scheduled Events (Preview) for Windows VMs</span></span>

> [!NOTE] 
> <span data-ttu-id="8a283-104">Voorbeelden zijn beschikbaar tooyou er op Hallo voorwaarde toohello gebruiksvoorwaarden gaat u akkoord.</span><span class="sxs-lookup"><span data-stu-id="8a283-104">Previews are made available tooyou on hello condition that you agree toohello terms of use.</span></span> <span data-ttu-id="8a283-105">Zie [Microsoft Azure Supplemental Terms of Use for Microsoft Azure Previews (Microsoft Azure Aanvullende gebruiksvoorwaarden voor Microsoft Azure-previews)](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="8a283-105">For more information, see [Microsoft Azure Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span></span>
>

<span data-ttu-id="8a283-106">Geplande gebeurtenissen is een van de Hallo subservices onder hello Azure metagegevens Service.</span><span class="sxs-lookup"><span data-stu-id="8a283-106">Scheduled Events is one of hello subservices under hello Azure Metadata Service.</span></span> <span data-ttu-id="8a283-107">Is verantwoordelijk voor bepaalde informatie over toekomstige gebeurtenissen (bijvoorbeeld opstarten vereist) zodat uw toepassing kunt voor ze voorbereiden en beperkt wordt onderbroken.</span><span class="sxs-lookup"><span data-stu-id="8a283-107">It is responsible for surfacing information regarding upcoming events (for example, reboot) so your application can prepare for them and limit disruption.</span></span> <span data-ttu-id="8a283-108">Het is beschikbaar voor alle virtuele Machine van Azure-typen, met inbegrip van PaaS en IaaS.</span><span class="sxs-lookup"><span data-stu-id="8a283-108">It is available for all Azure Virtual Machine types including PaaS and IaaS.</span></span> <span data-ttu-id="8a283-109">Geplande gebeurtenissen geeft uw virtuele Machine tijd tooperform preventieve taken toominimize Hallo effect van een gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="8a283-109">Scheduled Events gives your Virtual Machine time tooperform preventive tasks toominimize hello effect of an event.</span></span> 

<span data-ttu-id="8a283-110">Geplande gebeurtenissen is beschikbaar voor Linux- en VM's van Windows.</span><span class="sxs-lookup"><span data-stu-id="8a283-110">Scheduled Events is available for both Linux and Windows VMs.</span></span> <span data-ttu-id="8a283-111">Zie voor meer informatie over gebeurtenissen voor gepland op Linux [gepland gebeurtenissen voor virtuele Linux-machines](../windows/scheduled-events.md).</span><span class="sxs-lookup"><span data-stu-id="8a283-111">For information about Scheduled Events on Linux, see [Scheduled Events for Linux VMs](../windows/scheduled-events.md).</span></span>

## <a name="why-scheduled-events"></a><span data-ttu-id="8a283-112">Waarom gebeurtenissen gepland?</span><span class="sxs-lookup"><span data-stu-id="8a283-112">Why Scheduled Events?</span></span>

<span data-ttu-id="8a283-113">Met gebeurtenissen voor gepland, kunt u stappen ondernemen toolimit Hallo gevolgen van het platform intiated onderhoud of acties gebruiker gestart op uw service.</span><span class="sxs-lookup"><span data-stu-id="8a283-113">With Scheduled Events, you can take steps toolimit hello impact of platform-intiated maintenance or user-initiated actions on your service.</span></span> 

<span data-ttu-id="8a283-114">Meerdere exemplaren werkbelastingen die gebruikmaken van replicatiestatus technieken toomaintain, is mogelijk kwetsbaar toooutages plaatsvinden voor meerdere exemplaren.</span><span class="sxs-lookup"><span data-stu-id="8a283-114">Multi-instance workloads, which use replication techniques toomaintain state, may be vulnerable toooutages happening across multiple instances.</span></span> <span data-ttu-id="8a283-115">Zoals storingen mogelijk dure taken (bijvoorbeeld herbouwen indexen) of zelfs een verlies van de replica.</span><span class="sxs-lookup"><span data-stu-id="8a283-115">Such outages may result in expensive tasks (for example, rebuilding indexes) or even a replica loss.</span></span> 

<span data-ttu-id="8a283-116">In veel andere gevallen hello algemene beschikbaarheid van de service kan worden verbeterd door te voeren, zoals een reeks correct afsluiten voltooit (of annuleren)-onderweg transacties, opnieuw toewijzen van taken tooother virtuele machines in Hallo-cluster (handmatige failover) of hello te verwijderen Virtuele Machine uit een groep met network load balancer.</span><span class="sxs-lookup"><span data-stu-id="8a283-116">In many other cases, hello overall service availability may be improved by performing a graceful shutdown sequence such as completing (or canceling) in-flight transactions, reassigning tasks tooother VMs in hello cluster (manual failover), or removing hello Virtual Machine from a network load balancer pool.</span></span> 

<span data-ttu-id="8a283-117">Er zijn ook gevallen waarbij hulp van een beheerder over een aanstaande gebeurtenis of een dergelijke gebeurtenis logboekregistratie helpen Hallo onderhoudsvriendelijkheid van toepassingen die worden gehost in de cloud Hallo verbeteren.</span><span class="sxs-lookup"><span data-stu-id="8a283-117">There are cases where notifying an administrator about an upcoming event or logging such an event help improving hello serviceability of applications hosted in hello cloud.</span></span>

<span data-ttu-id="8a283-118">Azure Metadata verwerkingsinformatie gepland gebeurtenissen van de Service in de volgende Hallo gebruiksvoorbeelden:</span><span class="sxs-lookup"><span data-stu-id="8a283-118">Azure Metadata Service surfaces Scheduled Events in hello following use cases:</span></span>
-   <span data-ttu-id="8a283-119">Platform geïnitieerd onderhoud (bijvoorbeeld Host-OS-implementatie)</span><span class="sxs-lookup"><span data-stu-id="8a283-119">Platform initiated maintenance (for example, Host OS rollout)</span></span>
-   <span data-ttu-id="8a283-120">Gebruiker gestart aanroepen (bijvoorbeeld gebruiker opnieuw wordt opgestart of redeploys een virtuele machine)</span><span class="sxs-lookup"><span data-stu-id="8a283-120">User-initiated calls (for example, user restarts or redeploys a VM)</span></span>


## <a name="hello-basics"></a><span data-ttu-id="8a283-121">Hallo-basisbeginselen</span><span class="sxs-lookup"><span data-stu-id="8a283-121">hello basics</span></span>  

<span data-ttu-id="8a283-122">Azure service van de metagegevens wordt informatie over het uitvoeren van virtuele Machines met een REST-eindpunt toegankelijk vanuit Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="8a283-122">Azure Metadata service exposes information about running Virtual Machines using a REST Endpoint accessible from within hello VM.</span></span> <span data-ttu-id="8a283-123">Hallo informatie is beschikbaar via een niet-routeerbare IP-adres, zodat deze niet buiten Hallo VM weergegeven wordt.</span><span class="sxs-lookup"><span data-stu-id="8a283-123">hello information is available via a non-routable IP so that it is not exposed outside hello VM.</span></span>

### <a name="scope"></a><span data-ttu-id="8a283-124">Bereik</span><span class="sxs-lookup"><span data-stu-id="8a283-124">Scope</span></span>
<span data-ttu-id="8a283-125">Geplande gebeurtenissen zijn opgehaald tooall virtuele Machines in een cloudservice of tooall virtuele Machines in een Beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="8a283-125">Scheduled events are surfaced tooall Virtual Machines in a cloud service or tooall Virtual Machines in an Availability Set.</span></span> <span data-ttu-id="8a283-126">Als gevolg hiervan moet u controleren Hallo `Resources` veld Hallo gebeurtenis tooidentify die virtuele machines toobe beïnvloed gaat.</span><span class="sxs-lookup"><span data-stu-id="8a283-126">As a result, you should check hello `Resources` field in hello event tooidentify which VMs are going toobe impacted.</span></span> 

### <a name="discovering-hello-endpoint"></a><span data-ttu-id="8a283-127">Hallo-eindpunt detecteren</span><span class="sxs-lookup"><span data-stu-id="8a283-127">Discovering hello endpoint</span></span>
<span data-ttu-id="8a283-128">In geval Hallo waarop een virtuele Machine is gemaakt vanuit een virtueel netwerk (VNet) Hallo metagegevensservice is beschikbaar via een statische niet-routeerbare IP-adres `169.254.169.254`.</span><span class="sxs-lookup"><span data-stu-id="8a283-128">In hello case where a Virtual Machine is created within a Virtual Network (VNet), hello metadata service is available from a static non-routable IP, `169.254.169.254`.</span></span>
<span data-ttu-id="8a283-129">Als Hallo virtuele Machine niet vanuit een virtueel netwerk, Hallo standaard gevallen voor cloudservices en klassieke virtuele machines gemaakt is, is extra logica vereist toodiscover Hallo eindpunt toouse.</span><span class="sxs-lookup"><span data-stu-id="8a283-129">If hello Virtual Machine is not created within a Virtual Network, hello default cases for cloud services and classic VMs, additional logic is required toodiscover hello endpoint toouse.</span></span> <span data-ttu-id="8a283-130">Raadpleeg toothis voorbeeld toolearn hoe te[Hallo host-eindpunt detecteren](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span><span class="sxs-lookup"><span data-stu-id="8a283-130">Refer toothis sample toolearn how too[discover hello host endpoint](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span></span>

### <a name="versioning"></a><span data-ttu-id="8a283-131">Versiebeheer voor onderdelen</span><span class="sxs-lookup"><span data-stu-id="8a283-131">Versioning</span></span> 
<span data-ttu-id="8a283-132">Hallo metagegevens-Service-exemplaar is samengesteld.</span><span class="sxs-lookup"><span data-stu-id="8a283-132">hello Instance Metadata Service is versioned.</span></span> <span data-ttu-id="8a283-133">Versies zijn verplicht en de huidige versie Hallo is `2017-03-01`.</span><span class="sxs-lookup"><span data-stu-id="8a283-133">Versions are mandatory and hello current version is `2017-03-01`.</span></span>

> [!NOTE] 
> <span data-ttu-id="8a283-134">Eerdere versies van de preview van geplande gebeurtenissen {laatste} wordt ondersteund als Hallo api-versie.</span><span class="sxs-lookup"><span data-stu-id="8a283-134">Previous preview releases of scheduled events supported {latest} as hello api-version.</span></span> <span data-ttu-id="8a283-135">Deze indeling wordt niet meer ondersteund en in toekomstige hello wordt afgeschaft.</span><span class="sxs-lookup"><span data-stu-id="8a283-135">This format is no longer supported and will be deprecated in hello future.</span></span>

### <a name="using-headers"></a><span data-ttu-id="8a283-136">Met behulp van headers</span><span class="sxs-lookup"><span data-stu-id="8a283-136">Using headers</span></span>
<span data-ttu-id="8a283-137">Wanneer u query Hallo Metadata Service uitvoert, moet u opgeven Hallo header `Metadata: true` tooensure Hallo verzoek is niet per ongeluk omgeleid.</span><span class="sxs-lookup"><span data-stu-id="8a283-137">When you query hello Metadata Service, you must provide hello header `Metadata: true` tooensure hello request was not unintentionally redirected.</span></span>

### <a name="enabling-scheduled-events"></a><span data-ttu-id="8a283-138">Geplande gebeurtenissen inschakelen</span><span class="sxs-lookup"><span data-stu-id="8a283-138">Enabling Scheduled Events</span></span>
<span data-ttu-id="8a283-139">Hallo schakelt eerste keer dat u een aanvraag voor geplande gebeurtenissen Azure impliciet Hallo functie in op de virtuele Machine.</span><span class="sxs-lookup"><span data-stu-id="8a283-139">hello first time you make a request for scheduled events, Azure implicitly enables hello feature on your Virtual Machine.</span></span> <span data-ttu-id="8a283-140">U moet een vertraagde antwoord als gevolg hiervan verwacht in de eerste aanroep van up tootwo minuten.</span><span class="sxs-lookup"><span data-stu-id="8a283-140">As a result, you should expect a delayed response in your first call of up tootwo minutes.</span></span>

### <a name="user-initiated-maintenance"></a><span data-ttu-id="8a283-141">Onderhoud van de gebruiker gestarte</span><span class="sxs-lookup"><span data-stu-id="8a283-141">User initiated maintenance</span></span>
<span data-ttu-id="8a283-142">Gebruiker gestart onderhoud op virtuele machines via hello Azure-portal API, CLI of PowerShell resulteert in een geplande gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="8a283-142">User initiated virtual machine maintenance via hello Azure portal, API, CLI, or PowerShell results in a scheduled event.</span></span> <span data-ttu-id="8a283-143">Hiermee kunt u tootest Hallo onderhoud voorbereiding logica in uw toepassing te kunnen uw toepassing tooprepare voor onderhoud van de gebruiker gestarte.</span><span class="sxs-lookup"><span data-stu-id="8a283-143">This allows you tootest hello maintenance preparation logic in your application and allows your application tooprepare for user initiated maintenance.</span></span>

<span data-ttu-id="8a283-144">Een virtuele machine opnieuw plant u een gebeurtenis met type `Reboot`.</span><span class="sxs-lookup"><span data-stu-id="8a283-144">Restarting a virtual machine schedules an event with type `Reboot`.</span></span> <span data-ttu-id="8a283-145">Een virtuele machine opnieuw plant u een gebeurtenis met type `Redeploy`.</span><span class="sxs-lookup"><span data-stu-id="8a283-145">Redeploying a virtual machine schedules an event with type `Redeploy`.</span></span>

> [!NOTE] 
> <span data-ttu-id="8a283-146">Op dit moment kan maximaal 10 gebruiker gestarte onderhoudsbewerkingen worden tegelijkertijd gepland.</span><span class="sxs-lookup"><span data-stu-id="8a283-146">Currently a maximum of 10 user initiated maintenance operations can be simultaneously scheduled.</span></span> <span data-ttu-id="8a283-147">Deze limiet wordt minder streng worden gemaakt vóór de algemene beschikbaarheid van gebeurtenissen voor gepland.</span><span class="sxs-lookup"><span data-stu-id="8a283-147">This limit will be relaxed before Scheduled Events general availability.</span></span>

> [!NOTE] 
> <span data-ttu-id="8a283-148">Gebruiker gestarte onderhoud gepland gebeurtenissen ertoe kan momenteel niet worden geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="8a283-148">Currently user initiated maintenance resulting in Scheduled Events is not configurable.</span></span> <span data-ttu-id="8a283-149">Configuratiemogelijkheden is gepland voor een toekomstige release.</span><span class="sxs-lookup"><span data-stu-id="8a283-149">Configurability is planned for a future release.</span></span>

## <a name="using-hello-api"></a><span data-ttu-id="8a283-150">Hallo-API gebruiken</span><span class="sxs-lookup"><span data-stu-id="8a283-150">Using hello API</span></span>

### <a name="query-for-events"></a><span data-ttu-id="8a283-151">Query voor gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="8a283-151">Query for events</span></span>
<span data-ttu-id="8a283-152">U kunt een query voor geplande gebeurtenissen gewoon doordat Hallo volgende aanroepen:</span><span class="sxs-lookup"><span data-stu-id="8a283-152">You can query for Scheduled Events simply by making hello following call:</span></span>

```
curl -H Metadata:true http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

<span data-ttu-id="8a283-153">Een antwoord bevat een matrix van geplande gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="8a283-153">A response contains an array of scheduled events.</span></span> <span data-ttu-id="8a283-154">Een lege matrix betekent zijn momenteel geen gebeurtenissen die zijn gepland.</span><span class="sxs-lookup"><span data-stu-id="8a283-154">An empty array means that there are currently no events scheduled.</span></span>
<span data-ttu-id="8a283-155">In geval van Hallo wanneer er geplande gebeurtenissen, Hallo-antwoord bevat een matrix van gebeurtenissen:</span><span class="sxs-lookup"><span data-stu-id="8a283-155">In hello case where there are scheduled events, hello response contains an array of events:</span></span> 
```
{
    "DocumentIncarnation": {IncarnationID},
    "Events": [
        {
            "EventId": {eventID},
            "EventType": "Reboot" | "Redeploy" | "Freeze",
            "ResourceType": "VirtualMachine",
            "Resources": [{resourceName}],
            "EventStatus": "Scheduled" | "Started",
            "NotBefore": {timeInUTC},              
        }
    ]
}
```

### <a name="event-properties"></a><span data-ttu-id="8a283-156">Eigenschappen van gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="8a283-156">Event properties</span></span>
|<span data-ttu-id="8a283-157">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="8a283-157">Property</span></span>  |  <span data-ttu-id="8a283-158">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="8a283-158">Description</span></span> |
| - | - |
| <span data-ttu-id="8a283-159">Gebeurtenis-id</span><span class="sxs-lookup"><span data-stu-id="8a283-159">EventId</span></span> | <span data-ttu-id="8a283-160">Globaal unieke id voor deze gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="8a283-160">Globally unique identifier for this event.</span></span> <br><br> <span data-ttu-id="8a283-161">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8a283-161">Example:</span></span> <br><ul><li><span data-ttu-id="8a283-162">602d9444-d2cd-49c7-8624-8643e7171297</span><span class="sxs-lookup"><span data-stu-id="8a283-162">602d9444-d2cd-49c7-8624-8643e7171297</span></span>  |
| <span data-ttu-id="8a283-163">EventType</span><span class="sxs-lookup"><span data-stu-id="8a283-163">EventType</span></span> | <span data-ttu-id="8a283-164">Impact die deze gebeurtenis wordt veroorzaakt.</span><span class="sxs-lookup"><span data-stu-id="8a283-164">Impact this event causes.</span></span> <br><br> <span data-ttu-id="8a283-165">Waarden:</span><span class="sxs-lookup"><span data-stu-id="8a283-165">Values:</span></span> <br><ul><li> <span data-ttu-id="8a283-166">`Freeze`: Hallo virtuele Machine is geplande toopause voor enkele seconden.</span><span class="sxs-lookup"><span data-stu-id="8a283-166">`Freeze`: hello Virtual Machine is scheduled toopause for few seconds.</span></span> <span data-ttu-id="8a283-167">Hallo CPU is onderbroken, maar er zijn geen gevolgen voor geheugen, open bestanden of netwerkverbindingen.</span><span class="sxs-lookup"><span data-stu-id="8a283-167">hello CPU is suspended, but there is no impact on memory, open files, or network connections.</span></span> <li><span data-ttu-id="8a283-168">`Reboot`: Hallo virtuele Machine is gepland voor opnieuw opstarten (niet-permanente geheugen is verloren gegaan).</span><span class="sxs-lookup"><span data-stu-id="8a283-168">`Reboot`: hello Virtual Machine is scheduled for reboot (non-persistent memory is lost).</span></span> <li><span data-ttu-id="8a283-169">`Redeploy`: Hallo virtuele Machine is geplande toomove tooanother knooppunt (kortstondige schijven gaan verloren).</span><span class="sxs-lookup"><span data-stu-id="8a283-169">`Redeploy`: hello Virtual Machine is scheduled toomove tooanother node (ephemeral disks are lost).</span></span> |
| <span data-ttu-id="8a283-170">ResourceType</span><span class="sxs-lookup"><span data-stu-id="8a283-170">ResourceType</span></span> | <span data-ttu-id="8a283-171">Type resource dat van invloed is op deze gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="8a283-171">Type of resource this event impacts.</span></span> <br><br> <span data-ttu-id="8a283-172">Waarden:</span><span class="sxs-lookup"><span data-stu-id="8a283-172">Values:</span></span> <ul><li>`VirtualMachine`|
| <span data-ttu-id="8a283-173">Resources</span><span class="sxs-lookup"><span data-stu-id="8a283-173">Resources</span></span>| <span data-ttu-id="8a283-174">Lijst met bronnen die van invloed is op deze gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="8a283-174">List of resources this event impacts.</span></span> <span data-ttu-id="8a283-175">Dit kan toocontain machines gegarandeerd van maximaal één [Updatedomein](manage-availability.md), maar mag niet alle machines in Hallo UD bevatten.</span><span class="sxs-lookup"><span data-stu-id="8a283-175">This is guaranteed toocontain machines from at most one [Update Domain](manage-availability.md), but may not contain all machines in hello UD.</span></span> <br><br> <span data-ttu-id="8a283-176">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8a283-176">Example:</span></span> <br><ul><li> <span data-ttu-id="8a283-177">['FrontEnd_IN_0', 'BackEnd_IN_0']</span><span class="sxs-lookup"><span data-stu-id="8a283-177">["FrontEnd_IN_0", "BackEnd_IN_0"]</span></span> |
| <span data-ttu-id="8a283-178">Gebeurtenisstatus</span><span class="sxs-lookup"><span data-stu-id="8a283-178">Event Status</span></span> | <span data-ttu-id="8a283-179">Status van deze gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="8a283-179">Status of this event.</span></span> <br><br> <span data-ttu-id="8a283-180">Waarden:</span><span class="sxs-lookup"><span data-stu-id="8a283-180">Values:</span></span> <ul><li><span data-ttu-id="8a283-181">`Scheduled`: Deze gebeurtenis is geplande toostart na Hallo tijd die is opgegeven in Hallo `NotBefore` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="8a283-181">`Scheduled`: This event is scheduled toostart after hello time specified in hello `NotBefore` property.</span></span><li><span data-ttu-id="8a283-182">`Started`: Deze gebeurtenis is gestart.</span><span class="sxs-lookup"><span data-stu-id="8a283-182">`Started`: This event has started.</span></span></ul> <span data-ttu-id="8a283-183">Geen `Completed` of soortgelijke status ooit wordt geleverd; Hallo gebeurtenis wordt niet langer worden geretourneerd wanneer het Hallo-gebeurtenis is voltooid.</span><span class="sxs-lookup"><span data-stu-id="8a283-183">No `Completed` or similar status is ever provided; hello event will no longer be returned when hello event is completed.</span></span>
| <span data-ttu-id="8a283-184">NotBefore</span><span class="sxs-lookup"><span data-stu-id="8a283-184">NotBefore</span></span>| <span data-ttu-id="8a283-185">De tijd waarna deze gebeurtenis wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="8a283-185">Time after which this event may start.</span></span> <br><br> <span data-ttu-id="8a283-186">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8a283-186">Example:</span></span> <br><ul><li> <span data-ttu-id="8a283-187">2016-09-19T18:29:47Z</span><span class="sxs-lookup"><span data-stu-id="8a283-187">2016-09-19T18:29:47Z</span></span>  |

### <a name="event-scheduling"></a><span data-ttu-id="8a283-188">Gebeurtenis plannen</span><span class="sxs-lookup"><span data-stu-id="8a283-188">Event scheduling</span></span>
<span data-ttu-id="8a283-189">Elke gebeurtenis is gepland de minimale hoeveelheid tijd in toekomstige Hallo op basis van gebeurtenistype.</span><span class="sxs-lookup"><span data-stu-id="8a283-189">Each event is scheduled a minimum amount of time in hello future based on event type.</span></span> <span data-ttu-id="8a283-190">Deze tijd wordt weergegeven in een gebeurtenis `NotBefore` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="8a283-190">This time is reflected in an event's `NotBefore` property.</span></span> 

|<span data-ttu-id="8a283-191">EventType</span><span class="sxs-lookup"><span data-stu-id="8a283-191">EventType</span></span>  | <span data-ttu-id="8a283-192">Minimale kennisgeving</span><span class="sxs-lookup"><span data-stu-id="8a283-192">Minimum Notice</span></span> |
| - | - |
| <span data-ttu-id="8a283-193">Blokkeren</span><span class="sxs-lookup"><span data-stu-id="8a283-193">Freeze</span></span>| <span data-ttu-id="8a283-194">15 minuten</span><span class="sxs-lookup"><span data-stu-id="8a283-194">15 minutes</span></span> |
| <span data-ttu-id="8a283-195">Opnieuw opstarten</span><span class="sxs-lookup"><span data-stu-id="8a283-195">Reboot</span></span> | <span data-ttu-id="8a283-196">15 minuten</span><span class="sxs-lookup"><span data-stu-id="8a283-196">15 minutes</span></span> |
| <span data-ttu-id="8a283-197">Opnieuw implementeren</span><span class="sxs-lookup"><span data-stu-id="8a283-197">Redeploy</span></span> | <span data-ttu-id="8a283-198">10 minuten</span><span class="sxs-lookup"><span data-stu-id="8a283-198">10 minutes</span></span> |

### <a name="starting-an-event"></a><span data-ttu-id="8a283-199">Een gebeurtenis wordt gestart</span><span class="sxs-lookup"><span data-stu-id="8a283-199">Starting an event</span></span> 

<span data-ttu-id="8a283-200">Zodra u hebt geleerd van een aanstaande gebeurtenis en de logica voor het correct afsluiten voltooid, kunt u Hallo openstaande gebeurtenis goedkeuren door het maken van een `POST` toohello metagegevensservice Hello aanroepen `EventId`.</span><span class="sxs-lookup"><span data-stu-id="8a283-200">Once you have learned of an upcoming event and completed your logic for graceful shutdown, you can approve hello outstanding event by making a `POST` call toohello metadata service with hello `EventId`.</span></span> <span data-ttu-id="8a283-201">Dit geeft aan dat het Hallo minimale melding kunt inkorten tooAzure tijd (indien mogelijk).</span><span class="sxs-lookup"><span data-stu-id="8a283-201">This indicates tooAzure that it can shorten hello minimum notification time (when possible).</span></span> 

```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

> [!NOTE] 
> <span data-ttu-id="8a283-202">Een gebeurtenis zijn bevestigd Hallo gebeurtenis tooproceed staat voor alle `Resources` in Hallo-gebeurtenis niet alleen Hallo virtuele machine die Hallo-gebeurtenis rechthebbenden.</span><span class="sxs-lookup"><span data-stu-id="8a283-202">Acknowledging an event allows hello event tooproceed for all `Resources` in hello event, not just hello virtual machine that acknowledges hello event.</span></span> <span data-ttu-id="8a283-203">U kunt daarom ervoor kiezen tooelect een opvulteken toocoordinate Hallo bevestiging, die mogelijk net zo eenvoudig als eerste machine Hallo in Hallo `Resources` veld.</span><span class="sxs-lookup"><span data-stu-id="8a283-203">You may therefore choose tooelect a leader toocoordinate hello acknowledgement, which may be as simple as hello first machine in hello `Resources` field.</span></span>


## <a name="powershell-sample"></a><span data-ttu-id="8a283-204">PowerShell-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="8a283-204">PowerShell sample</span></span> 

<span data-ttu-id="8a283-205">Hallo volgende voorbeeldquery's Hallo metagegevensservice voor geplande gebeurtenissen en keurt deze goed elke openstaande gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="8a283-205">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

```PowerShell
# How tooget scheduled events 
function GetScheduledEvents($uri)
{
    $scheduledEvents = Invoke-RestMethod -Headers @{"Metadata"="true"} -URI $uri -Method get
    $json = ConvertTo-Json $scheduledEvents
    Write-Host "Received following events: `n" $json
    return $scheduledEvents
}

# How tooapprove a scheduled event
function ApproveScheduledEvent($eventId, $docIncarnation, $uri)
{    
    # Create hello Scheduled Events Approval Document
    $startRequests = [array]@{"EventId" = $eventId}
    $scheduledEventsApproval = @{"StartRequests" = $startRequests; "DocumentIncarnation" = $docIncarnation} 
    
    # Convert tooJSON string
    $approvalString = ConvertTo-Json $scheduledEventsApproval

    Write-Host "Approving with hello following: `n" $approvalString

    # Post approval string tooscheduled events endpoint
    Invoke-RestMethod -Uri $uri -Headers @{"Metadata"="true"} -Method POST -Body $approvalString
}

function HandleScheduledEvents($scheduledEvents)
{
    # Add logic for handling events here
}

######### Sample Scheduled Events Interaction #########

# Set up hello scheduled events URI for a VNET-enabled VM
$localHostIP = "169.254.169.254"
$scheduledEventURI = 'http://{0}/metadata/scheduledevents?api-version=2017-03-01' -f $localHostIP 

# Get events
$scheduledEvents = GetScheduledEvents $scheduledEventURI

# Handle events however is best for your service
HandleScheduledEvents $scheduledEvents

# Approve events when ready (optional)
foreach($event in $scheduledEvents.Events)
{
    Write-Host "Current Event: `n" $event
    $entry = Read-Host "`nApprove event? Y/N"
    if($entry -eq "Y" -or $entry -eq "y")
    {
        ApproveScheduledEvent $event.EventId $scheduledEvents.DocumentIncarnation $scheduledEventURI 
    }
}
``` 


## <a name="c-sample"></a><span data-ttu-id="8a283-206">C\# voorbeeld</span><span class="sxs-lookup"><span data-stu-id="8a283-206">C\# sample</span></span> 

<span data-ttu-id="8a283-207">Hallo is volgende een voorbeeld van een eenvoudige client die met de service Hallo-metagegevens communiceert.</span><span class="sxs-lookup"><span data-stu-id="8a283-207">hello following sample is of a simple client that communicates with hello metadata service.</span></span>

```csharp
public class ScheduledEventsClient
{
    private readonly string scheduledEventsEndpoint;
    private readonly string defaultIpAddress = "169.254.169.254"; 

    // Set up hello scheduled events URI for a VNET-enabled VM
    public ScheduledEventsClient()
    {
        scheduledEventsEndpoint = string.Format("http://{0}/metadata/scheduledevents?api-version=2017-03-01", defaultIpAddress);
    }

    // Get events
    public string GetScheduledEvents()
    {
        Uri cloudControlUri = new Uri(scheduledEventsEndpoint);
        using (var webClient = new WebClient())
        {
            webClient.Headers.Add("Metadata", "true");
            return webClient.DownloadString(cloudControlUri);
        }   
    }

    // Approve events
    public void ApproveScheduledEvents(string jsonPost)
    {
        using (var webClient = new WebClient())
        {
            webClient.Headers.Add("Content-Type", "application/json");
            webClient.UploadString(scheduledEventsEndpoint, jsonPost);
        }
    }
}
```

<span data-ttu-id="8a283-208">Geplande gebeurtenissen kunnen worden voorgesteld met Hallo gegevensstructuren te volgen:</span><span class="sxs-lookup"><span data-stu-id="8a283-208">Scheduled Events can be represented using hello following data structures:</span></span>

```csharp
public class ScheduledEventsDocument
{
    public string DocumentIncarnation;
    public List<CloudControlEvent> Events { get; set; }
}

public class CloudControlEvent
{
    public string EventId { get; set; }
    public string EventStatus { get; set; }
    public string EventType { get; set; }
    public string ResourceType { get; set; }
    public List<string> Resources { get; set; }
    public DateTime? NotBefore { get; set; }
}

public class ScheduledEventsApproval
{
    public string DocumentIncarnation;
    public List<StartRequest> StartRequests = new List<StartRequest>();
}

public class StartRequest
{
    [JsonProperty("EventId")]
    private string eventId;

    public StartRequest(string eventId)
    {
        this.eventId = eventId;
    }
}
```

<span data-ttu-id="8a283-209">Hallo volgende voorbeeldquery's Hallo metagegevensservice voor geplande gebeurtenissen en keurt deze goed elke openstaande gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="8a283-209">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

```csharp
public class Program
{
    static ScheduledEventsClient client;

    static void Main(string[] args)
    {
        client = new ScheduledEventsClient();

        while (true)
        {
            string json = client.GetDocument();
            ScheduledEventsDocument scheduledEventsDocument = JsonConvert.DeserializeObject<ScheduledEventsDocument>(json);

            HandleEvents(scheduledEventsDocument.Events);

            // Wait for user response
            Console.WriteLine("Press Enter tooapprove executing events\n");
            Console.ReadLine();

            // Approve events
            ScheduledEventsApproval scheduledEventsApprovalDocument = new ScheduledEventsApproval()
            {
                DocumentIncarnation = scheduledEventsDocument.DocumentIncarnation
            };
        
            foreach (CloudControlEvent event in scheduledEventsDocument.Events)
            {
                scheduledEventsApprovalDocument.StartRequests.Add(new StartRequest(event.EventId));
            }

            if (scheduledEventsApprovalDocument.StartRequests.Count > 0)
            {
                // Serialize using Newtonsoft.Json
                string approveEventsJsonDocument =
                    JsonConvert.SerializeObject(scheduledEventsApprovalDocument);

                Console.WriteLine($"Approving events with json: {approveEventsJsonDocument}\n");
                client.ApproveScheduledEvents(approveEventsJsonDocument);
            }

            Console.WriteLine("Complete. Press enter toorepeat\n\n");
            Console.ReadLine();
            Console.Clear();
        }
    }

    private static void HandleEvents(List<CloudControlEvent> events)
    {
        // Add logic for handling events here
    }
}
```

## <a name="python-sample"></a><span data-ttu-id="8a283-210">Python-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="8a283-210">Python sample</span></span> 

<span data-ttu-id="8a283-211">Hallo volgende voorbeeldquery's Hallo metagegevensservice voor geplande gebeurtenissen en keurt deze goed elke openstaande gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="8a283-211">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

```python
#!/usr/bin/python

import json
import urllib2
import socket
import sys

metadata_url = "http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01"
headers = "{Metadata:true}"
this_host = socket.gethostname()

def get_scheduled_events():
   req = urllib2.Request(metadata_url)
   req.add_header('Metadata', 'true')
   resp = urllib2.urlopen(req)
   data = json.loads(resp.read())
   return data

def handle_scheduled_events(data):
    for evt in data['Events']:
        eventid = evt['EventId']
        status = evt['EventStatus']
        resources = evt['Resources']
        eventtype = evt['EventType']
        resourcetype = evt['ResourceType']
        notbefore = evt['NotBefore'].replace(" ","_")
        if this_host in resources:
            print "+ Scheduled Event. This host is scheduled for " + eventype + " not before " + notbefore
            # Add logic for handling events here

def main():
   data = get_scheduled_events()
   handle_scheduled_events(data)
   
if __name__ == '__main__':
  main()
  sys.exit(0)
```

## <a name="next-steps"></a><span data-ttu-id="8a283-212">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8a283-212">Next steps</span></span> 

- <span data-ttu-id="8a283-213">Meer informatie over beschikbare API's in Hallo Hallo [service-exemplaar metagegevens](instance-metadata-service.md).</span><span class="sxs-lookup"><span data-stu-id="8a283-213">Read more about hello APIs available in hello [Instance Metadata service](instance-metadata-service.md).</span></span>
- <span data-ttu-id="8a283-214">Meer informatie over [gepland onderhoud voor Windows virtuele machines in Azure](planned-maintenance.md).</span><span class="sxs-lookup"><span data-stu-id="8a283-214">Learn about [planned maintenance for Windows virtual machines in Azure](planned-maintenance.md).</span></span>

