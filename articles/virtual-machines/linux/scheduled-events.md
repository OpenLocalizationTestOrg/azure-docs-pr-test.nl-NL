---
title: aaaScheduled gebeurtenissen voor virtuele Linux-machines in Azure | Microsoft Docs
description: Geplande gebeurtenissen met Hallo metagegevens van de Azure-service voor op uw virtuele Linux-machines.
services: virtual-machines-windows, virtual-machines-linux, cloud-services
documentationcenter: 
author: zivraf
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/14/2017
ms.author: zivr
ms.openlocfilehash: e153c8854725330acefd67d0ef542f6149170a7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-metadata-service-scheduled-events-preview-for-linux-vms"></a><span data-ttu-id="2f290-103">Azure Service metagegevens: Geplande gebeurtenissen (Preview) voor virtuele Linux-machines</span><span class="sxs-lookup"><span data-stu-id="2f290-103">Azure Metadata Service: Scheduled Events (Preview) for Linux VMs</span></span>

> [!NOTE] 
> <span data-ttu-id="2f290-104">Voorbeelden zijn beschikbaar tooyou er op Hallo voorwaarde toohello gebruiksvoorwaarden gaat u akkoord.</span><span class="sxs-lookup"><span data-stu-id="2f290-104">Previews are made available tooyou on hello condition that you agree toohello terms of use.</span></span> <span data-ttu-id="2f290-105">Zie [Microsoft Azure Supplemental Terms of Use for Microsoft Azure Previews (Microsoft Azure Aanvullende gebruiksvoorwaarden voor Microsoft Azure-previews)](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="2f290-105">For more information, see [Microsoft Azure Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span></span>
>

<span data-ttu-id="2f290-106">Geplande gebeurtenissen is een van de Hallo subservices onder hello Azure metagegevens Service.</span><span class="sxs-lookup"><span data-stu-id="2f290-106">Scheduled Events is one of hello subservices under hello Azure Metadata Service.</span></span> <span data-ttu-id="2f290-107">Is verantwoordelijk voor bepaalde informatie over toekomstige gebeurtenissen (bijvoorbeeld opstarten vereist) zodat uw toepassing kunt voor ze voorbereiden en beperkt wordt onderbroken.</span><span class="sxs-lookup"><span data-stu-id="2f290-107">It is responsible for surfacing information regarding upcoming events (for example, reboot) so your application can prepare for them and limit disruption.</span></span> <span data-ttu-id="2f290-108">Het is beschikbaar voor alle virtuele Machine van Azure-typen, met inbegrip van PaaS en IaaS.</span><span class="sxs-lookup"><span data-stu-id="2f290-108">It is available for all Azure Virtual Machine types including PaaS and IaaS.</span></span> <span data-ttu-id="2f290-109">Geplande gebeurtenissen geeft uw virtuele Machine tijd tooperform preventieve taken toominimize Hallo effect van een gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="2f290-109">Scheduled Events gives your Virtual Machine time tooperform preventive tasks toominimize hello effect of an event.</span></span> 

<span data-ttu-id="2f290-110">Geplande gebeurtenissen is beschikbaar voor zowel Windows als een virtuele Linux-machines.</span><span class="sxs-lookup"><span data-stu-id="2f290-110">Scheduled Events is available for both Windows and Linux VMs.</span></span> <span data-ttu-id="2f290-111">Zie voor meer informatie over gebeurtenissen in Windows gepland [gepland gebeurtenissen voor VM's van Windows](../windows/scheduled-events.md).</span><span class="sxs-lookup"><span data-stu-id="2f290-111">For information about Scheduled Events on Windows, see [Scheduled Events for Windows VMs](../windows/scheduled-events.md).</span></span>

## <a name="why-scheduled-events"></a><span data-ttu-id="2f290-112">Waarom gebeurtenissen gepland?</span><span class="sxs-lookup"><span data-stu-id="2f290-112">Why Scheduled Events?</span></span>

<span data-ttu-id="2f290-113">Met gebeurtenissen voor gepland, kunt u stappen ondernemen toolimit Hallo gevolgen van het platform intiated onderhoud of acties gebruiker gestart op uw service.</span><span class="sxs-lookup"><span data-stu-id="2f290-113">With Scheduled Events, you can take steps toolimit hello impact of platform-intiated maintenance or user-initiated actions on your service.</span></span> 

<span data-ttu-id="2f290-114">Meerdere exemplaren werkbelastingen die gebruikmaken van replicatiestatus technieken toomaintain, is mogelijk kwetsbaar toooutages plaatsvinden voor meerdere exemplaren.</span><span class="sxs-lookup"><span data-stu-id="2f290-114">Multi-instance workloads, which use replication techniques toomaintain state, may be vulnerable toooutages happening across multiple instances.</span></span> <span data-ttu-id="2f290-115">Zoals storingen mogelijk dure taken (bijvoorbeeld herbouwen indexen) of zelfs een verlies van de replica.</span><span class="sxs-lookup"><span data-stu-id="2f290-115">Such outages may result in expensive tasks (for example, rebuilding indexes) or even a replica loss.</span></span> 

<span data-ttu-id="2f290-116">In veel andere gevallen hello algemene beschikbaarheid van de service kan worden verbeterd door te voeren, zoals een reeks correct afsluiten voltooit (of annuleren)-onderweg transacties, opnieuw toewijzen van taken tooother virtuele machines in Hallo-cluster (handmatige failover) of hello te verwijderen Virtuele Machine uit een groep met network load balancer.</span><span class="sxs-lookup"><span data-stu-id="2f290-116">In many other cases, hello overall service availability may be improved by performing a graceful shutdown sequence such as completing (or canceling) in-flight transactions, reassigning tasks tooother VMs in hello cluster (manual failover), or removing hello Virtual Machine from a network load balancer pool.</span></span> 

<span data-ttu-id="2f290-117">Er zijn ook gevallen waarbij hulp van een beheerder over een aanstaande gebeurtenis of een dergelijke gebeurtenis logboekregistratie helpen Hallo onderhoudsvriendelijkheid van toepassingen die worden gehost in de cloud Hallo verbeteren.</span><span class="sxs-lookup"><span data-stu-id="2f290-117">There are cases where notifying an administrator about an upcoming event or logging such an event help improving hello serviceability of applications hosted in hello cloud.</span></span>

<span data-ttu-id="2f290-118">Azure Metadata verwerkingsinformatie gepland gebeurtenissen van de Service in de volgende Hallo gebruiksvoorbeelden:</span><span class="sxs-lookup"><span data-stu-id="2f290-118">Azure Metadata Service surfaces Scheduled Events in hello following use cases:</span></span>
-   <span data-ttu-id="2f290-119">Platform geïnitieerd onderhoud (bijvoorbeeld Host-OS-implementatie)</span><span class="sxs-lookup"><span data-stu-id="2f290-119">Platform initiated maintenance (for example, Host OS rollout)</span></span>
-   <span data-ttu-id="2f290-120">Gebruiker gestart aanroepen (bijvoorbeeld gebruiker opnieuw wordt opgestart of redeploys een virtuele machine)</span><span class="sxs-lookup"><span data-stu-id="2f290-120">User-initiated calls (for example, user restarts or redeploys a VM)</span></span>


## <a name="hello-basics"></a><span data-ttu-id="2f290-121">Hallo-basisbeginselen</span><span class="sxs-lookup"><span data-stu-id="2f290-121">hello basics</span></span>  

<span data-ttu-id="2f290-122">Azure service van de metagegevens wordt informatie over het uitvoeren van virtuele Machines met een REST-eindpunt toegankelijk vanuit Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="2f290-122">Azure Metadata service exposes information about running Virtual Machines using a REST Endpoint accessible from within hello VM.</span></span> <span data-ttu-id="2f290-123">Hallo informatie is beschikbaar via een niet-routeerbare IP-adres, zodat deze niet buiten Hallo VM weergegeven wordt.</span><span class="sxs-lookup"><span data-stu-id="2f290-123">hello information is available via a non-routable IP so that it is not exposed outside hello VM.</span></span>

### <a name="scope"></a><span data-ttu-id="2f290-124">Bereik</span><span class="sxs-lookup"><span data-stu-id="2f290-124">Scope</span></span>
<span data-ttu-id="2f290-125">Geplande gebeurtenissen zijn opgehaald tooall virtuele Machines in een cloudservice of tooall virtuele Machines in een Beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="2f290-125">Scheduled events are surfaced tooall Virtual Machines in a cloud service or tooall Virtual Machines in an Availability Set.</span></span> <span data-ttu-id="2f290-126">Als gevolg hiervan moet u controleren Hallo `Resources` veld Hallo gebeurtenis tooidentify die virtuele machines toobe beïnvloed gaat.</span><span class="sxs-lookup"><span data-stu-id="2f290-126">As a result, you should check hello `Resources` field in hello event tooidentify which VMs are going toobe impacted.</span></span> 

### <a name="discovering-hello-endpoint"></a><span data-ttu-id="2f290-127">Hallo-eindpunt detecteren</span><span class="sxs-lookup"><span data-stu-id="2f290-127">Discovering hello endpoint</span></span>
<span data-ttu-id="2f290-128">In geval Hallo waarop een virtuele Machine is gemaakt vanuit een virtueel netwerk (VNet) Hallo metagegevensservice is beschikbaar via een statische niet-routeerbare IP-adres `169.254.169.254`.</span><span class="sxs-lookup"><span data-stu-id="2f290-128">In hello case where a Virtual Machine is created within a Virtual Network (VNet), hello metadata service is available from a static non-routable IP, `169.254.169.254`.</span></span>
<span data-ttu-id="2f290-129">Als Hallo virtuele Machine niet vanuit een virtueel netwerk, Hallo standaard gevallen voor cloudservices en klassieke virtuele machines gemaakt is, is extra logica vereist toodiscover Hallo eindpunt toouse.</span><span class="sxs-lookup"><span data-stu-id="2f290-129">If hello Virtual Machine is not created within a Virtual Network, hello default cases for cloud services and classic VMs, additional logic is required toodiscover hello endpoint toouse.</span></span> <span data-ttu-id="2f290-130">Raadpleeg toothis voorbeeld toolearn hoe te[Hallo host-eindpunt detecteren](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span><span class="sxs-lookup"><span data-stu-id="2f290-130">Refer toothis sample toolearn how too[discover hello host endpoint](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span></span>

### <a name="versioning"></a><span data-ttu-id="2f290-131">Versiebeheer voor onderdelen</span><span class="sxs-lookup"><span data-stu-id="2f290-131">Versioning</span></span> 
<span data-ttu-id="2f290-132">Hallo metagegevens-Service-exemplaar is samengesteld.</span><span class="sxs-lookup"><span data-stu-id="2f290-132">hello Instance Metadata Service is versioned.</span></span> <span data-ttu-id="2f290-133">Versies zijn verplicht en de huidige versie Hallo is `2017-03-01`.</span><span class="sxs-lookup"><span data-stu-id="2f290-133">Versions are mandatory and hello current version is `2017-03-01`.</span></span>

> [!NOTE] 
> <span data-ttu-id="2f290-134">Eerdere versies van de preview van geplande gebeurtenissen {laatste} wordt ondersteund als Hallo api-versie.</span><span class="sxs-lookup"><span data-stu-id="2f290-134">Previous preview releases of scheduled events supported {latest} as hello api-version.</span></span> <span data-ttu-id="2f290-135">Deze indeling wordt niet meer ondersteund en in toekomstige hello wordt afgeschaft.</span><span class="sxs-lookup"><span data-stu-id="2f290-135">This format is no longer supported and will be deprecated in hello future.</span></span>

### <a name="using-headers"></a><span data-ttu-id="2f290-136">Met behulp van headers</span><span class="sxs-lookup"><span data-stu-id="2f290-136">Using headers</span></span>
<span data-ttu-id="2f290-137">Wanneer u query Hallo Metadata Service uitvoert, moet u opgeven Hallo header `Metadata: true` tooensure Hallo verzoek is niet per ongeluk omgeleid.</span><span class="sxs-lookup"><span data-stu-id="2f290-137">When you query hello Metadata Service, you must provide hello header `Metadata: true` tooensure hello request was not unintentionally redirected.</span></span>

### <a name="enabling-scheduled-events"></a><span data-ttu-id="2f290-138">Geplande gebeurtenissen inschakelen</span><span class="sxs-lookup"><span data-stu-id="2f290-138">Enabling Scheduled Events</span></span>
<span data-ttu-id="2f290-139">Hallo schakelt eerste keer dat u een aanvraag voor geplande gebeurtenissen Azure impliciet Hallo functie in op de virtuele Machine.</span><span class="sxs-lookup"><span data-stu-id="2f290-139">hello first time you make a request for scheduled events, Azure implicitly enables hello feature on your Virtual Machine.</span></span> <span data-ttu-id="2f290-140">U moet een vertraagde antwoord als gevolg hiervan verwacht in de eerste aanroep van up tootwo minuten.</span><span class="sxs-lookup"><span data-stu-id="2f290-140">As a result, you should expect a delayed response in your first call of up tootwo minutes.</span></span>

### <a name="user-initiated-maintenance"></a><span data-ttu-id="2f290-141">Onderhoud van de gebruiker gestarte</span><span class="sxs-lookup"><span data-stu-id="2f290-141">User initiated maintenance</span></span>
<span data-ttu-id="2f290-142">Gebruiker gestart onderhoud op virtuele machines via hello Azure-portal API, CLI of PowerShell resulteert in een geplande gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="2f290-142">User initiated virtual machine maintenance via hello Azure portal, API, CLI, or PowerShell results in a scheduled event.</span></span> <span data-ttu-id="2f290-143">Hiermee kunt u tootest Hallo onderhoud voorbereiding logica in uw toepassing te kunnen uw toepassing tooprepare voor onderhoud van de gebruiker gestarte.</span><span class="sxs-lookup"><span data-stu-id="2f290-143">This allows you tootest hello maintenance preparation logic in your application and allows your application tooprepare for user initiated maintenance.</span></span>

<span data-ttu-id="2f290-144">Een virtuele machine opnieuw plant u een gebeurtenis met type `Reboot`.</span><span class="sxs-lookup"><span data-stu-id="2f290-144">Restarting a virtual machine schedules an event with type `Reboot`.</span></span> <span data-ttu-id="2f290-145">Een virtuele machine opnieuw plant u een gebeurtenis met type `Redeploy`.</span><span class="sxs-lookup"><span data-stu-id="2f290-145">Redeploying a virtual machine schedules an event with type `Redeploy`.</span></span>

> [!NOTE] 
> <span data-ttu-id="2f290-146">Op dit moment kan maximaal 10 gebruiker gestarte onderhoudsbewerkingen worden tegelijkertijd gepland.</span><span class="sxs-lookup"><span data-stu-id="2f290-146">Currently a maximum of 10 user initiated maintenance operations can be simultaneously scheduled.</span></span> <span data-ttu-id="2f290-147">Deze limiet wordt minder streng worden gemaakt vóór de algemene beschikbaarheid van gebeurtenissen voor gepland.</span><span class="sxs-lookup"><span data-stu-id="2f290-147">This limit will be relaxed before Scheduled Events general availability.</span></span>

> [!NOTE] 
> <span data-ttu-id="2f290-148">Gebruiker gestarte onderhoud gepland gebeurtenissen ertoe kan momenteel niet worden geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="2f290-148">Currently user initiated maintenance resulting in Scheduled Events is not configurable.</span></span> <span data-ttu-id="2f290-149">Configuratiemogelijkheden is gepland voor een toekomstige release.</span><span class="sxs-lookup"><span data-stu-id="2f290-149">Configurability is planned for a future release.</span></span>

## <a name="using-hello-api"></a><span data-ttu-id="2f290-150">Hallo-API gebruiken</span><span class="sxs-lookup"><span data-stu-id="2f290-150">Using hello API</span></span>

### <a name="query-for-events"></a><span data-ttu-id="2f290-151">Query voor gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="2f290-151">Query for events</span></span>
<span data-ttu-id="2f290-152">U kunt een query voor geplande gebeurtenissen gewoon doordat Hallo volgende aanroepen:</span><span class="sxs-lookup"><span data-stu-id="2f290-152">You can query for Scheduled Events simply by making hello following call:</span></span>

```
curl -H Metadata:true http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

<span data-ttu-id="2f290-153">Een antwoord bevat een matrix van geplande gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="2f290-153">A response contains an array of scheduled events.</span></span> <span data-ttu-id="2f290-154">Een lege matrix betekent zijn momenteel geen gebeurtenissen die zijn gepland.</span><span class="sxs-lookup"><span data-stu-id="2f290-154">An empty array means that there are currently no events scheduled.</span></span>
<span data-ttu-id="2f290-155">In geval van Hallo wanneer er geplande gebeurtenissen, Hallo-antwoord bevat een matrix van gebeurtenissen:</span><span class="sxs-lookup"><span data-stu-id="2f290-155">In hello case where there are scheduled events, hello response contains an array of events:</span></span> 
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

### <a name="event-properties"></a><span data-ttu-id="2f290-156">Eigenschappen van gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="2f290-156">Event properties</span></span>
|<span data-ttu-id="2f290-157">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="2f290-157">Property</span></span>  |  <span data-ttu-id="2f290-158">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="2f290-158">Description</span></span> |
| - | - |
| <span data-ttu-id="2f290-159">Gebeurtenis-id</span><span class="sxs-lookup"><span data-stu-id="2f290-159">EventId</span></span> | <span data-ttu-id="2f290-160">Globaal unieke id voor deze gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="2f290-160">Globally unique identifier for this event.</span></span> <br><br> <span data-ttu-id="2f290-161">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2f290-161">Example:</span></span> <br><ul><li><span data-ttu-id="2f290-162">602d9444-d2cd-49c7-8624-8643e7171297</span><span class="sxs-lookup"><span data-stu-id="2f290-162">602d9444-d2cd-49c7-8624-8643e7171297</span></span>  |
| <span data-ttu-id="2f290-163">EventType</span><span class="sxs-lookup"><span data-stu-id="2f290-163">EventType</span></span> | <span data-ttu-id="2f290-164">Impact die deze gebeurtenis wordt veroorzaakt.</span><span class="sxs-lookup"><span data-stu-id="2f290-164">Impact this event causes.</span></span> <br><br> <span data-ttu-id="2f290-165">Waarden:</span><span class="sxs-lookup"><span data-stu-id="2f290-165">Values:</span></span> <br><ul><li> <span data-ttu-id="2f290-166">`Freeze`: Hallo virtuele Machine is geplande toopause voor enkele seconden.</span><span class="sxs-lookup"><span data-stu-id="2f290-166">`Freeze`: hello Virtual Machine is scheduled toopause for few seconds.</span></span> <span data-ttu-id="2f290-167">Hallo CPU is onderbroken, maar er zijn geen gevolgen voor geheugen, open bestanden of netwerkverbindingen.</span><span class="sxs-lookup"><span data-stu-id="2f290-167">hello CPU is suspended, but there is no impact on memory, open files, or network connections.</span></span> <li><span data-ttu-id="2f290-168">`Reboot`: Hallo virtuele Machine is gepland voor opnieuw opstarten (niet-permanente geheugen is verloren gegaan).</span><span class="sxs-lookup"><span data-stu-id="2f290-168">`Reboot`: hello Virtual Machine is scheduled for reboot (non-persistent memory is lost).</span></span> <li><span data-ttu-id="2f290-169">`Redeploy`: Hallo virtuele Machine is geplande toomove tooanother knooppunt (kortstondige schijven gaan verloren).</span><span class="sxs-lookup"><span data-stu-id="2f290-169">`Redeploy`: hello Virtual Machine is scheduled toomove tooanother node (ephemeral disks are lost).</span></span> |
| <span data-ttu-id="2f290-170">ResourceType</span><span class="sxs-lookup"><span data-stu-id="2f290-170">ResourceType</span></span> | <span data-ttu-id="2f290-171">Type resource dat van invloed is op deze gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="2f290-171">Type of resource this event impacts.</span></span> <br><br> <span data-ttu-id="2f290-172">Waarden:</span><span class="sxs-lookup"><span data-stu-id="2f290-172">Values:</span></span> <ul><li>`VirtualMachine`|
| <span data-ttu-id="2f290-173">Resources</span><span class="sxs-lookup"><span data-stu-id="2f290-173">Resources</span></span>| <span data-ttu-id="2f290-174">Lijst met bronnen die van invloed is op deze gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="2f290-174">List of resources this event impacts.</span></span> <span data-ttu-id="2f290-175">Dit kan toocontain machines gegarandeerd van maximaal één [Updatedomein](manage-availability.md), maar mag niet alle machines in Hallo UD bevatten.</span><span class="sxs-lookup"><span data-stu-id="2f290-175">This is guaranteed toocontain machines from at most one [Update Domain](manage-availability.md), but may not contain all machines in hello UD.</span></span> <br><br> <span data-ttu-id="2f290-176">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2f290-176">Example:</span></span> <br><ul><li> <span data-ttu-id="2f290-177">['FrontEnd_IN_0', 'BackEnd_IN_0']</span><span class="sxs-lookup"><span data-stu-id="2f290-177">["FrontEnd_IN_0", "BackEnd_IN_0"]</span></span> |
| <span data-ttu-id="2f290-178">Gebeurtenisstatus</span><span class="sxs-lookup"><span data-stu-id="2f290-178">Event Status</span></span> | <span data-ttu-id="2f290-179">Status van deze gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="2f290-179">Status of this event.</span></span> <br><br> <span data-ttu-id="2f290-180">Waarden:</span><span class="sxs-lookup"><span data-stu-id="2f290-180">Values:</span></span> <ul><li><span data-ttu-id="2f290-181">`Scheduled`: Deze gebeurtenis is geplande toostart na Hallo tijd die is opgegeven in Hallo `NotBefore` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="2f290-181">`Scheduled`: This event is scheduled toostart after hello time specified in hello `NotBefore` property.</span></span><li><span data-ttu-id="2f290-182">`Started`: Deze gebeurtenis is gestart.</span><span class="sxs-lookup"><span data-stu-id="2f290-182">`Started`: This event has started.</span></span></ul> <span data-ttu-id="2f290-183">Geen `Completed` of soortgelijke status ooit wordt geleverd; Hallo gebeurtenis wordt niet langer worden geretourneerd wanneer het Hallo-gebeurtenis is voltooid.</span><span class="sxs-lookup"><span data-stu-id="2f290-183">No `Completed` or similar status is ever provided; hello event will no longer be returned when hello event is completed.</span></span>
| <span data-ttu-id="2f290-184">NotBefore</span><span class="sxs-lookup"><span data-stu-id="2f290-184">NotBefore</span></span>| <span data-ttu-id="2f290-185">De tijd waarna deze gebeurtenis wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="2f290-185">Time after which this event may start.</span></span> <br><br> <span data-ttu-id="2f290-186">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2f290-186">Example:</span></span> <br><ul><li> <span data-ttu-id="2f290-187">2016-09-19T18:29:47Z</span><span class="sxs-lookup"><span data-stu-id="2f290-187">2016-09-19T18:29:47Z</span></span>  |

### <a name="event-scheduling"></a><span data-ttu-id="2f290-188">Gebeurtenis plannen</span><span class="sxs-lookup"><span data-stu-id="2f290-188">Event scheduling</span></span>
<span data-ttu-id="2f290-189">Elke gebeurtenis is gepland de minimale hoeveelheid tijd in toekomstige Hallo op basis van gebeurtenistype.</span><span class="sxs-lookup"><span data-stu-id="2f290-189">Each event is scheduled a minimum amount of time in hello future based on event type.</span></span> <span data-ttu-id="2f290-190">Deze tijd wordt weergegeven in een gebeurtenis `NotBefore` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="2f290-190">This time is reflected in an event's `NotBefore` property.</span></span> 

|<span data-ttu-id="2f290-191">EventType</span><span class="sxs-lookup"><span data-stu-id="2f290-191">EventType</span></span>  | <span data-ttu-id="2f290-192">Minimale kennisgeving</span><span class="sxs-lookup"><span data-stu-id="2f290-192">Minimum Notice</span></span> |
| - | - |
| <span data-ttu-id="2f290-193">Blokkeren</span><span class="sxs-lookup"><span data-stu-id="2f290-193">Freeze</span></span>| <span data-ttu-id="2f290-194">15 minuten</span><span class="sxs-lookup"><span data-stu-id="2f290-194">15 minutes</span></span> |
| <span data-ttu-id="2f290-195">Opnieuw opstarten</span><span class="sxs-lookup"><span data-stu-id="2f290-195">Reboot</span></span> | <span data-ttu-id="2f290-196">15 minuten</span><span class="sxs-lookup"><span data-stu-id="2f290-196">15 minutes</span></span> |
| <span data-ttu-id="2f290-197">Opnieuw implementeren</span><span class="sxs-lookup"><span data-stu-id="2f290-197">Redeploy</span></span> | <span data-ttu-id="2f290-198">10 minuten</span><span class="sxs-lookup"><span data-stu-id="2f290-198">10 minutes</span></span> |

### <a name="starting-an-event"></a><span data-ttu-id="2f290-199">Een gebeurtenis wordt gestart</span><span class="sxs-lookup"><span data-stu-id="2f290-199">Starting an event</span></span> 

<span data-ttu-id="2f290-200">Zodra u hebt geleerd van een aanstaande gebeurtenis en de logica voor het correct afsluiten voltooid, kunt u Hallo openstaande gebeurtenis goedkeuren door het maken van een `POST` toohello metagegevensservice Hello aanroepen `EventId`.</span><span class="sxs-lookup"><span data-stu-id="2f290-200">Once you have learned of an upcoming event and completed your logic for graceful shutdown, you can approve hello outstanding event by making a `POST` call toohello metadata service with hello `EventId`.</span></span> <span data-ttu-id="2f290-201">Dit geeft aan dat het Hallo minimale melding kunt inkorten tooAzure tijd (indien mogelijk).</span><span class="sxs-lookup"><span data-stu-id="2f290-201">This indicates tooAzure that it can shorten hello minimum notification time (when possible).</span></span> 

```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

> [!NOTE] 
> <span data-ttu-id="2f290-202">Een gebeurtenis zijn bevestigd Hallo gebeurtenis tooproceed staat voor alle `Resources` in Hallo-gebeurtenis niet alleen Hallo virtuele machine die Hallo-gebeurtenis rechthebbenden.</span><span class="sxs-lookup"><span data-stu-id="2f290-202">Acknowledging an event allows hello event tooproceed for all `Resources` in hello event, not just hello virtual machine that acknowledges hello event.</span></span> <span data-ttu-id="2f290-203">U kunt daarom ervoor kiezen tooelect een opvulteken toocoordinate Hallo bevestiging, die mogelijk net zo eenvoudig als eerste machine Hallo in Hallo `Resources` veld.</span><span class="sxs-lookup"><span data-stu-id="2f290-203">You may therefore choose tooelect a leader toocoordinate hello acknowledgement, which may be as simple as hello first machine in hello `Resources` field.</span></span>




## <a name="python-sample"></a><span data-ttu-id="2f290-204">Python-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="2f290-204">Python sample</span></span> 

<span data-ttu-id="2f290-205">Hallo volgende voorbeeldquery's Hallo metagegevensservice voor geplande gebeurtenissen en keurt deze goed elke openstaande gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="2f290-205">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="2f290-206">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2f290-206">Next steps</span></span> 

- <span data-ttu-id="2f290-207">Meer informatie over beschikbare API's in Hallo Hallo [service-exemplaar metagegevens](instance-metadata-service.md).</span><span class="sxs-lookup"><span data-stu-id="2f290-207">Read more about hello APIs available in hello [Instance Metadata service](instance-metadata-service.md).</span></span>
- <span data-ttu-id="2f290-208">Meer informatie over [gepland onderhoud voor Linux virtuele machines in Azure](planned-maintenance.md).</span><span class="sxs-lookup"><span data-stu-id="2f290-208">Learn about [planned maintenance for Linux virtual machines in Azure](planned-maintenance.md).</span></span>
