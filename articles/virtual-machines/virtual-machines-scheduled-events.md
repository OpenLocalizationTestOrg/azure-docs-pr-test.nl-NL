---
title: Gebeurtenissen met de Service Azure metagegevens gepland | Microsoft Docs
description: Reageren op Impactful gebeurtenissen op de virtuele Machine voordat ze optreden.
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
ms.date: 12/10/2016
ms.author: zivr
ms.openlocfilehash: 793803bfc12059a68ec881da9de37116f7a0eb8c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-metadata-service---scheduled-events-preview"></a><span data-ttu-id="d272e-103">Azure Service metagegevens - geplande gebeurtenissen (Preview)</span><span class="sxs-lookup"><span data-stu-id="d272e-103">Azure Metadata Service - Scheduled Events (Preview)</span></span>

> [!NOTE] 
> <span data-ttu-id="d272e-104">Voorbeelden zijn beschikbaar gemaakt voor u op voorwaarde dat u akkoord met de gebruiksvoorwaarden gaat.</span><span class="sxs-lookup"><span data-stu-id="d272e-104">Previews are made available to you on the condition that you agree to the terms of use.</span></span> <span data-ttu-id="d272e-105">Zie [Microsoft Azure Supplemental Terms of Use for Microsoft Azure Previews (Microsoft Azure Aanvullende gebruiksvoorwaarden voor Microsoft Azure-previews)](https://azure.microsoft.com/en-us/support/legal/preview-supplemental-terms/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d272e-105">For more information, see [Microsoft Azure Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/en-us/support/legal/preview-supplemental-terms/).</span></span>
>

<span data-ttu-id="d272e-106">Geplande gebeurtenissen is een van de subservices onder de Azure-Service voor metagegevens.</span><span class="sxs-lookup"><span data-stu-id="d272e-106">Scheduled Events is one of the subservices under the Azure Metadata Service.</span></span> <span data-ttu-id="d272e-107">Is verantwoordelijk voor bepaalde informatie over toekomstige gebeurtenissen (bijvoorbeeld opstarten vereist) zodat uw toepassing kunt voor ze voorbereiden en beperkt wordt onderbroken.</span><span class="sxs-lookup"><span data-stu-id="d272e-107">It is responsible for surfacing information regarding upcoming events (for example, reboot) so your application can prepare for them and limit disruption.</span></span> <span data-ttu-id="d272e-108">Het is beschikbaar voor alle virtuele Machine van Azure-typen, met inbegrip van PaaS en IaaS.</span><span class="sxs-lookup"><span data-stu-id="d272e-108">It is available for all Azure Virtual Machine types including PaaS and IaaS.</span></span> <span data-ttu-id="d272e-109">Geplande gebeurtenissen geeft de tijd van de virtuele Machine preventieve taken uitvoeren om te voorkomen dat dit gevolgen van een gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="d272e-109">Scheduled Events gives your Virtual Machine time to perform preventive tasks to minimize the effect of an event.</span></span> 

## <a name="introduction---why-scheduled-events"></a><span data-ttu-id="d272e-110">Inleiding - waarom gebeurtenissen gepland?</span><span class="sxs-lookup"><span data-stu-id="d272e-110">Introduction - Why Scheduled Events?</span></span>

<span data-ttu-id="d272e-111">U kunt stappen voor het beperken van de gevolgen van het platform intiated onderhoud of acties gebruiker gestart op uw service te nemen met gebeurtenissen voor gepland.</span><span class="sxs-lookup"><span data-stu-id="d272e-111">With Scheduled Events, you can take steps to limit the impact of platform-intiated maintenance or user-initiated actions on your service.</span></span> 

<span data-ttu-id="d272e-112">Meerdere exemplaren werkbelastingen die gebruikmaken van replicatietechnieken om status te behouden, is mogelijk kwetsbaar voor uitval plaatsvinden voor meerdere exemplaren.</span><span class="sxs-lookup"><span data-stu-id="d272e-112">Multi-instance workloads, which use replication techniques to maintain state, may be vulnerable to outages happening across multiple instances.</span></span> <span data-ttu-id="d272e-113">Zoals storingen mogelijk dure taken (bijvoorbeeld herbouwen indexen) of zelfs een verlies van de replica.</span><span class="sxs-lookup"><span data-stu-id="d272e-113">Such outages may result in expensive tasks (for example, rebuilding indexes) or even a replica loss.</span></span> 

<span data-ttu-id="d272e-114">In veel andere gevallen is de algemene beschikbaarheid van de service kan worden verbeterd door te voeren, zoals een reeks correct afsluiten voltooit (of annuleren)-onderweg transacties, opnieuw toewijzen van taken aan andere virtuele machines in het cluster (handmatige failover) of verwijderen van de virtuele Machine in een netwerk load balancer van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="d272e-114">In many other cases, the overall service availability may be improved by performing a graceful shutdown sequence such as completing (or canceling) in-flight transactions, reassigning tasks to other VMs in the cluster (manual failover), or removing the Virtual Machine from a network load balancer pool.</span></span> 

<span data-ttu-id="d272e-115">Er zijn ook gevallen waarbij hulp van een beheerder over een aanstaande gebeurtenis of een dergelijke gebeurtenis logboekregistratie helpen verbeteren de onderhoudsvriendelijkheid van toepassingen die worden gehost in de cloud.</span><span class="sxs-lookup"><span data-stu-id="d272e-115">There are cases where notifying an administrator about an upcoming event or logging such an event help improving the serviceability of applications hosted in the cloud.</span></span>

<span data-ttu-id="d272e-116">Azure Metadata-Service geeft gepland gebeurtenissen weer in de volgende gevallen:</span><span class="sxs-lookup"><span data-stu-id="d272e-116">Azure Metadata Service surfaces Scheduled Events in the following use cases:</span></span>
-   <span data-ttu-id="d272e-117">Platform geïnitieerd onderhoud (bijvoorbeeld Host-OS-implementatie)</span><span class="sxs-lookup"><span data-stu-id="d272e-117">Platform initiated maintenance (for example, Host OS rollout)</span></span>
-   <span data-ttu-id="d272e-118">Gebruiker gestart aanroepen (bijvoorbeeld gebruiker opnieuw wordt opgestart of redeploys een virtuele machine)</span><span class="sxs-lookup"><span data-stu-id="d272e-118">User-initiated calls (for example, user restarts or redeploys a VM)</span></span>


## <a name="scheduled-events---the-basics"></a><span data-ttu-id="d272e-119">Geplande gebeurtenissen - de basisbeginselen</span><span class="sxs-lookup"><span data-stu-id="d272e-119">Scheduled Events - The Basics</span></span>  

<span data-ttu-id="d272e-120">Azure service van de metagegevens wordt informatie over het uitvoeren van virtuele Machines met een REST-eindpunt toegankelijk vanuit de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="d272e-120">Azure Metadata service exposes information about running Virtual Machines using a REST Endpoint accessible from within the VM.</span></span> <span data-ttu-id="d272e-121">De informatie is beschikbaar via een niet-routeerbare IP-adres, zodat deze niet buiten de virtuele machine wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d272e-121">The information is available via a non-routable IP so that it is not exposed outside the VM.</span></span>

### <a name="scope"></a><span data-ttu-id="d272e-122">Bereik</span><span class="sxs-lookup"><span data-stu-id="d272e-122">Scope</span></span>
<span data-ttu-id="d272e-123">Geplande gebeurtenissen worden opgehaald voor alle virtuele Machines in een cloudservice of voor alle virtuele Machines in een Beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="d272e-123">Scheduled events are surfaced to all Virtual Machines in a cloud service or to all Virtual Machines in an Availability Set.</span></span> <span data-ttu-id="d272e-124">Als gevolg hiervan moet u controleren de `Resources` veld in de gebeurtenis geven aan welke VM's gaan worden beïnvloed.</span><span class="sxs-lookup"><span data-stu-id="d272e-124">As a result, you should check the `Resources` field in the event to identify which VMs are going to be impacted.</span></span> 

### <a name="discovering-the-endpoint"></a><span data-ttu-id="d272e-125">Het eindpunt detecteren</span><span class="sxs-lookup"><span data-stu-id="d272e-125">Discovering the Endpoint</span></span>
<span data-ttu-id="d272e-126">In het geval waarbij een virtuele Machine is gemaakt vanuit een virtueel netwerk (VNet), de metagegevensservice is beschikbaar via een statische niet-routeerbare IP-adres `169.254.169.254`.</span><span class="sxs-lookup"><span data-stu-id="d272e-126">In the case where a Virtual Machine is created within a Virtual Network (VNet), the metadata service is available from a static non-routable IP, `169.254.169.254`.</span></span>
<span data-ttu-id="d272e-127">Als de virtuele Machine niet vanuit een virtueel netwerk, de standaard gevallen voor cloudservices en klassieke virtuele machines gemaakt is, worden extra logica is vereist voor het detecteren van het eindpunt te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d272e-127">If the Virtual Machine is not created within a Virtual Network, the default cases for cloud services and classic VMs, additional logic is required to discover the endpoint to use.</span></span> <span data-ttu-id="d272e-128">Raadpleeg dit voorbeeld voor meer informatie over hoe [de host-eindpunt detecteren](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span><span class="sxs-lookup"><span data-stu-id="d272e-128">Refer to this sample to learn how to [discover the host endpoint](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span></span>

### <a name="versioning"></a><span data-ttu-id="d272e-129">Versiebeheer voor onderdelen</span><span class="sxs-lookup"><span data-stu-id="d272e-129">Versioning</span></span> 
<span data-ttu-id="d272e-130">De Service-exemplaar voor metagegevens is samengestelde.</span><span class="sxs-lookup"><span data-stu-id="d272e-130">The Instance Metadata Service is versioned.</span></span> <span data-ttu-id="d272e-131">Versies zijn verplicht en de huidige versie is `2017-03-01`.</span><span class="sxs-lookup"><span data-stu-id="d272e-131">Versions are mandatory and the current version is `2017-03-01`.</span></span>

> [!NOTE] 
> <span data-ttu-id="d272e-132">Eerdere versies van de preview van geplande gebeurtenissen {laatste} wordt ondersteund als de api-versie.</span><span class="sxs-lookup"><span data-stu-id="d272e-132">Previous preview releases of scheduled events supported {latest} as the api-version.</span></span> <span data-ttu-id="d272e-133">Deze indeling wordt niet meer ondersteund en in de toekomst wordt afgeschaft.</span><span class="sxs-lookup"><span data-stu-id="d272e-133">This format is no longer supported and will be deprecated in the future.</span></span>

### <a name="using-headers"></a><span data-ttu-id="d272e-134">Met behulp van Headers</span><span class="sxs-lookup"><span data-stu-id="d272e-134">Using Headers</span></span>
<span data-ttu-id="d272e-135">Wanneer u een query de Metadata-Service, moet u de header geven `Metadata: true` om te controleren of de aanvraag is niet per ongeluk wordt omgeleid.</span><span class="sxs-lookup"><span data-stu-id="d272e-135">When you query the Metadata Service, you must provide the header `Metadata: true` to ensure the request was not unintentionally redirected.</span></span>

### <a name="enabling-scheduled-events"></a><span data-ttu-id="d272e-136">Geplande gebeurtenissen inschakelen</span><span class="sxs-lookup"><span data-stu-id="d272e-136">Enabling Scheduled Events</span></span>
<span data-ttu-id="d272e-137">De eerste keer dat u een aanvraag voor geplande gebeurtenissen schakelt Azure impliciet de functie in op de virtuele Machine.</span><span class="sxs-lookup"><span data-stu-id="d272e-137">The first time you make a request for scheduled events, Azure implicitly enables the feature on your Virtual Machine.</span></span> <span data-ttu-id="d272e-138">U moet een vertraagde antwoord als gevolg hiervan verwacht in de eerste aanroep van twee minuten.</span><span class="sxs-lookup"><span data-stu-id="d272e-138">As a result, you should expect a delayed response in your first call of up to two minutes.</span></span>

### <a name="user-initiated-maintenance"></a><span data-ttu-id="d272e-139">Gebruiker gestart onderhoud</span><span class="sxs-lookup"><span data-stu-id="d272e-139">User Initiated Maintenance</span></span>
<span data-ttu-id="d272e-140">Gebruiker gestart onderhoud op virtuele machines via de Azure-portal API, CLI of PowerShell leidt ertoe dat gebeurtenissen gepland.</span><span class="sxs-lookup"><span data-stu-id="d272e-140">User initiated virtual machine maintenance via the Azure portal, API, CLI, or PowerShell will result in Scheduled Events.</span></span> <span data-ttu-id="d272e-141">Dit kunt u de voorbereiding van onderhoud logica in uw toepassing testen en kan de toepassing om voor te bereiden voor het onderhoud van de gebruiker worden gestart.</span><span class="sxs-lookup"><span data-stu-id="d272e-141">This allows you to test the maintenance preparation logic in your application and allows your application to prepare for user initiated maintenance.</span></span>

<span data-ttu-id="d272e-142">Een virtuele machine opnieuw opstarten wordt gepland als een gebeurtenis met type `Reboot`.</span><span class="sxs-lookup"><span data-stu-id="d272e-142">Restarting a virtual machine will schedule an event with type `Reboot`.</span></span> <span data-ttu-id="d272e-143">Een gebeurtenis met het type dat een virtuele machine wordt gepland `Redeploy`.</span><span class="sxs-lookup"><span data-stu-id="d272e-143">Redeploying a virtual machine will schedule an event with type `Redeploy`.</span></span>

> [!NOTE] 
> <span data-ttu-id="d272e-144">Op dit moment kan maximaal 10 gebruiker gestarte onderhoudsbewerkingen worden tegelijkertijd gepland.</span><span class="sxs-lookup"><span data-stu-id="d272e-144">Currently a maximum of 10 user initiated maintenance operations can be simultaneously scheduled.</span></span> <span data-ttu-id="d272e-145">Deze limiet wordt minder streng worden gemaakt voordat de geplande algemene beschikbaarheid van gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="d272e-145">This limit will be relaxed before Scheduled Events General Availability.</span></span>

> [!NOTE] 
> <span data-ttu-id="d272e-146">Gebruiker gestarte onderhoud gepland gebeurtenissen ertoe kan momenteel niet worden geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="d272e-146">Currently user initiated maintenance resulting in Scheduled Events is not configurable.</span></span> <span data-ttu-id="d272e-147">Configuratiemogelijkheden is gepland voor een toekomstige release.</span><span class="sxs-lookup"><span data-stu-id="d272e-147">Configurability is planned for a future release.</span></span>

## <a name="using-the-api"></a><span data-ttu-id="d272e-148">Met behulp van de API</span><span class="sxs-lookup"><span data-stu-id="d272e-148">Using the API</span></span>

### <a name="query-for-events"></a><span data-ttu-id="d272e-149">Query voor gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="d272e-149">Query for events</span></span>
<span data-ttu-id="d272e-150">U kunt een query voor geplande gebeurtenissen gewoon door de volgende oproep verzenden:</span><span class="sxs-lookup"><span data-stu-id="d272e-150">You can query for Scheduled Events simply by making the following call:</span></span>

```
curl -H Metadata:true http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

<span data-ttu-id="d272e-151">Een antwoord bevat een matrix van geplande gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="d272e-151">A response contains an array of scheduled events.</span></span> <span data-ttu-id="d272e-152">Een lege matrix betekent zijn momenteel geen gebeurtenissen die zijn gepland.</span><span class="sxs-lookup"><span data-stu-id="d272e-152">An empty array means that there are currently no events scheduled.</span></span>
<span data-ttu-id="d272e-153">In het geval wanneer er geplande gebeurtenissen, het antwoord bevat een matrix van gebeurtenissen:</span><span class="sxs-lookup"><span data-stu-id="d272e-153">In the case where there are scheduled events, the response contains an array of events:</span></span> 
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

### <a name="event-properties"></a><span data-ttu-id="d272e-154">Eigenschappen van gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="d272e-154">Event Properties</span></span>
|<span data-ttu-id="d272e-155">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="d272e-155">Property</span></span>  |  <span data-ttu-id="d272e-156">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d272e-156">Description</span></span> |
| - | - |
| <span data-ttu-id="d272e-157">Gebeurtenis-id</span><span class="sxs-lookup"><span data-stu-id="d272e-157">EventId</span></span> | <span data-ttu-id="d272e-158">Globaal unieke id voor deze gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="d272e-158">Globally unique identifier for this event.</span></span> <br><br> <span data-ttu-id="d272e-159">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d272e-159">Example:</span></span> <br><ul><li><span data-ttu-id="d272e-160">602d9444-d2cd-49c7-8624-8643e7171297</span><span class="sxs-lookup"><span data-stu-id="d272e-160">602d9444-d2cd-49c7-8624-8643e7171297</span></span>  |
| <span data-ttu-id="d272e-161">EventType</span><span class="sxs-lookup"><span data-stu-id="d272e-161">EventType</span></span> | <span data-ttu-id="d272e-162">Impact die deze gebeurtenis wordt veroorzaakt.</span><span class="sxs-lookup"><span data-stu-id="d272e-162">Impact this event causes.</span></span> <br><br> <span data-ttu-id="d272e-163">Waarden:</span><span class="sxs-lookup"><span data-stu-id="d272e-163">Values:</span></span> <br><ul><li> <span data-ttu-id="d272e-164">`Freeze`: De virtuele Machine is gepland voor wacht u enkele seconden.</span><span class="sxs-lookup"><span data-stu-id="d272e-164">`Freeze`: The Virtual Machine is scheduled to pause for few seconds.</span></span> <span data-ttu-id="d272e-165">De CPU wordt onderbroken, maar er zijn geen gevolgen voor geheugen, open bestanden of netwerkverbindingen.</span><span class="sxs-lookup"><span data-stu-id="d272e-165">The CPU will be suspended, but there is no impact on memory, open files, or network connections.</span></span> <li><span data-ttu-id="d272e-166">`Reboot`: De virtuele Machine is gepland voor opnieuw opstarten (niet-permanente geheugen is verloren gegaan).</span><span class="sxs-lookup"><span data-stu-id="d272e-166">`Reboot`: The Virtual Machine is scheduled for reboot (non-persistent memory is lost).</span></span> <li><span data-ttu-id="d272e-167">`Redeploy`: Gepland de virtuele Machine naar een ander knooppunt verplaatsen (kortstondige schijven gaan verloren).</span><span class="sxs-lookup"><span data-stu-id="d272e-167">`Redeploy`: The Virtual Machine is scheduled to move to another node (ephemeral disks are lost).</span></span> |
| <span data-ttu-id="d272e-168">ResourceType</span><span class="sxs-lookup"><span data-stu-id="d272e-168">ResourceType</span></span> | <span data-ttu-id="d272e-169">Type resource dat van invloed is op deze gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="d272e-169">Type of resource this event impacts.</span></span> <br><br> <span data-ttu-id="d272e-170">Waarden:</span><span class="sxs-lookup"><span data-stu-id="d272e-170">Values:</span></span> <ul><li>`VirtualMachine`|
| <span data-ttu-id="d272e-171">Resources</span><span class="sxs-lookup"><span data-stu-id="d272e-171">Resources</span></span>| <span data-ttu-id="d272e-172">Lijst met bronnen die van invloed is op deze gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="d272e-172">List of resources this event impacts.</span></span> <span data-ttu-id="d272e-173">Dit kan worden gegarandeerd bevat machines van maximaal één [Updatedomein](windows/manage-availability.md), maar mag niet alle machines in de UD bevatten.</span><span class="sxs-lookup"><span data-stu-id="d272e-173">This is guaranteed to contain machines from at most one [Update Domain](windows/manage-availability.md), but may not contain all machines in the UD.</span></span> <br><br> <span data-ttu-id="d272e-174">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d272e-174">Example:</span></span> <br><ul><li> <span data-ttu-id="d272e-175">['FrontEnd_IN_0', 'BackEnd_IN_0']</span><span class="sxs-lookup"><span data-stu-id="d272e-175">["FrontEnd_IN_0", "BackEnd_IN_0"]</span></span> |
| <span data-ttu-id="d272e-176">Gebeurtenisstatus</span><span class="sxs-lookup"><span data-stu-id="d272e-176">Event Status</span></span> | <span data-ttu-id="d272e-177">Status van deze gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="d272e-177">Status of this event.</span></span> <br><br> <span data-ttu-id="d272e-178">Waarden:</span><span class="sxs-lookup"><span data-stu-id="d272e-178">Values:</span></span> <ul><li><span data-ttu-id="d272e-179">`Scheduled`: Deze gebeurtenis is gepland om te starten na de tijd die is opgegeven in de `NotBefore` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="d272e-179">`Scheduled`: This event is scheduled to start after the time specified in the `NotBefore` property.</span></span><li><span data-ttu-id="d272e-180">`Started`: Deze gebeurtenis is gestart.</span><span class="sxs-lookup"><span data-stu-id="d272e-180">`Started`: This event has started.</span></span></ul> <span data-ttu-id="d272e-181">Geen `Completed` of soortgelijke status ooit wordt geleverd; de gebeurtenis wordt niet meer worden geretourneerd wanneer de gebeurtenis is voltooid.</span><span class="sxs-lookup"><span data-stu-id="d272e-181">No `Completed` or similar status is ever provided; the event will no longer be returned when the event is completed.</span></span>
| <span data-ttu-id="d272e-182">NotBefore</span><span class="sxs-lookup"><span data-stu-id="d272e-182">NotBefore</span></span>| <span data-ttu-id="d272e-183">De tijd waarna deze gebeurtenis wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="d272e-183">Time after which this event may start.</span></span> <br><br> <span data-ttu-id="d272e-184">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d272e-184">Example:</span></span> <br><ul><li> <span data-ttu-id="d272e-185">2016-09-19T18:29:47Z</span><span class="sxs-lookup"><span data-stu-id="d272e-185">2016-09-19T18:29:47Z</span></span>  |

### <a name="event-scheduling"></a><span data-ttu-id="d272e-186">Gebeurtenis plannen</span><span class="sxs-lookup"><span data-stu-id="d272e-186">Event Scheduling</span></span>
<span data-ttu-id="d272e-187">Elke gebeurtenis is gepland op basis van de minimale hoeveelheid tijd in de toekomst op gebeurtenistype.</span><span class="sxs-lookup"><span data-stu-id="d272e-187">Each event is scheduled a minimum amount of time in the future based on event type.</span></span> <span data-ttu-id="d272e-188">Deze tijd wordt weergegeven in een gebeurtenis `NotBefore` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="d272e-188">This time is reflected in an event's `NotBefore` property.</span></span> 

|<span data-ttu-id="d272e-189">EventType</span><span class="sxs-lookup"><span data-stu-id="d272e-189">EventType</span></span>  | <span data-ttu-id="d272e-190">Minimale kennisgeving</span><span class="sxs-lookup"><span data-stu-id="d272e-190">Minimum Notice</span></span> |
| - | - |
| <span data-ttu-id="d272e-191">Blokkeren</span><span class="sxs-lookup"><span data-stu-id="d272e-191">Freeze</span></span>| <span data-ttu-id="d272e-192">15 minuten</span><span class="sxs-lookup"><span data-stu-id="d272e-192">15 minutes</span></span> |
| <span data-ttu-id="d272e-193">Opnieuw opstarten</span><span class="sxs-lookup"><span data-stu-id="d272e-193">Reboot</span></span> | <span data-ttu-id="d272e-194">15 minuten</span><span class="sxs-lookup"><span data-stu-id="d272e-194">15 minutes</span></span> |
| <span data-ttu-id="d272e-195">Opnieuw implementeren</span><span class="sxs-lookup"><span data-stu-id="d272e-195">Redeploy</span></span> | <span data-ttu-id="d272e-196">10 minuten</span><span class="sxs-lookup"><span data-stu-id="d272e-196">10 minutes</span></span> |

### <a name="starting-an-event-expedite"></a><span data-ttu-id="d272e-197">Een gebeurtenis wordt gestart (versnellen)</span><span class="sxs-lookup"><span data-stu-id="d272e-197">Starting an event (expedite)</span></span>

<span data-ttu-id="d272e-198">Zodra u hebt geleerd van een aanstaande gebeurtenis en de logica voor het correct afsluiten voltooid, kunt u de openstaande gebeurtenis goedkeuren door het maken van een `POST` aanroep van de metagegevensservice met de `EventId`.</span><span class="sxs-lookup"><span data-stu-id="d272e-198">Once you have learned of an upcoming event and completed your logic for graceful shutdown, you can approve the outstanding event by making a `POST` call to the metadata service with the `EventId`.</span></span> <span data-ttu-id="d272e-199">Hiermee geeft u aan Azure dat deze de minimale melding kunt inkorten tijd (indien mogelijk).</span><span class="sxs-lookup"><span data-stu-id="d272e-199">This indicates to Azure that it can shorten the minimum notification time (when possible).</span></span> 

```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

> [!NOTE] 
> <span data-ttu-id="d272e-200">Een gebeurtenis zijn bevestigd, hebt u toestaan dat de gebeurtenis om door te gaan voor alle `Resources` in het gebeurtenislogboek, niet alleen de virtuele machine bevestigt dat de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="d272e-200">Acknowledging a event will allow the event to proceed for all `Resources` in the event, not just the virtual machine that acknowledges the event.</span></span> <span data-ttu-id="d272e-201">Daarom kunt u ervoor kiest een opvulteken voor het coördineren van de bevestiging die net zo eenvoudig als het eerste virtuele machine in de `Resources` veld.</span><span class="sxs-lookup"><span data-stu-id="d272e-201">You may therefore choose to elect a leader to coordinate the acknowledgement, which may be as simple as the first machine in the `Resources` field.</span></span>

## <a name="samples"></a><span data-ttu-id="d272e-202">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="d272e-202">Samples</span></span>

### <a name="powershell-sample"></a><span data-ttu-id="d272e-203">PowerShell-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="d272e-203">PowerShell Sample</span></span> 

<span data-ttu-id="d272e-204">Het volgende voorbeeld query op de metagegevensservice voor geplande gebeurtenissen en keurt deze goed elke openstaande gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="d272e-204">The following sample queries the metadata service for scheduled events and approves each outstanding event.</span></span>

```PowerShell
# How to get scheduled events 
function GetScheduledEvents($uri)
{
    $scheduledEvents = Invoke-RestMethod -Headers @{"Metadata"="true"} -URI $uri -Method get
    $json = ConvertTo-Json $scheduledEvents
    Write-Host "Received following events: `n" $json
    return $scheduledEvents
}

# How to approve a scheduled event
function ApproveScheduledEvent($eventId, $docIncarnation, $uri)
{    
    # Create the Scheduled Events Approval Document
    $startRequests = [array]@{"EventId" = $eventId}
    $scheduledEventsApproval = @{"StartRequests" = $startRequests; "DocumentIncarnation" = $docIncarnation} 
    
    # Convert to JSON string
    $approvalString = ConvertTo-Json $scheduledEventsApproval

    Write-Host "Approving with the following: `n" $approvalString

    # Post approval string to scheduled events endpoint
    Invoke-RestMethod -Uri $uri -Headers @{"Metadata"="true"} -Method POST -Body $approvalString
}

function HandleScheduledEvents($scheduledEvents)
{
    # Add logic for handling events here
}

######### Sample Scheduled Events Interaction #########

# Set up the scheduled events URI for a VNET-enabled VM
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


### <a name="c-sample"></a><span data-ttu-id="d272e-205">C\# voorbeeld</span><span class="sxs-lookup"><span data-stu-id="d272e-205">C\# Sample</span></span> 

<span data-ttu-id="d272e-206">Het volgende voorbeeld is van een eenvoudige client die met de metagegevensservice communiceert.</span><span class="sxs-lookup"><span data-stu-id="d272e-206">The following sample is of a simple client that communicates with the metadata service.</span></span>

```csharp
public class ScheduledEventsClient
{
    private readonly string scheduledEventsEndpoint;
    private readonly string defaultIpAddress = "169.254.169.254"; 

    // Set up the scheduled events URI for a VNET-enabled VM
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

<span data-ttu-id="d272e-207">Geplande gebeurtenissen kunnen met behulp van de volgende gegevensstructuren worden voorgesteld:</span><span class="sxs-lookup"><span data-stu-id="d272e-207">Scheduled Events can be represented using the following data structures:</span></span>

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

<span data-ttu-id="d272e-208">Het volgende voorbeeld query op de metagegevensservice voor geplande gebeurtenissen en keurt deze goed elke openstaande gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="d272e-208">The following sample queries the metadata service for scheduled events and approves each outstanding event.</span></span>

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
            Console.WriteLine("Press Enter to approve executing events\n");
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

            Console.WriteLine("Complete. Press enter to repeat\n\n");
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

### <a name="python-sample"></a><span data-ttu-id="d272e-209">Python-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="d272e-209">Python Sample</span></span> 

<span data-ttu-id="d272e-210">Het volgende voorbeeld query op de metagegevensservice voor geplande gebeurtenissen en keurt deze goed elke openstaande gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="d272e-210">The following sample queries the metadata service for scheduled events and approves each outstanding event.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="d272e-211">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d272e-211">Next Steps</span></span> 

- <span data-ttu-id="d272e-212">Meer informatie over de beschikbare API's in de [metagegevensservice-instantie](virtual-machines-instancemetadataservice-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d272e-212">Read more about the APIs available in the [instance metadata service](virtual-machines-instancemetadataservice-overview.md).</span></span>
- <span data-ttu-id="d272e-213">Meer informatie over [gepland onderhoud voor Windows virtuele machines in Azure](windows/planned-maintenance.md).</span><span class="sxs-lookup"><span data-stu-id="d272e-213">Learn about [planned maintenance for Windows virtual machines in Azure](windows/planned-maintenance.md).</span></span>
- <span data-ttu-id="d272e-214">Meer informatie over [gepland onderhoud voor Linux virtuele machines in Azure](linux/planned-maintenance.md).</span><span class="sxs-lookup"><span data-stu-id="d272e-214">Learn about [planned maintenance for Linux virtual machines in Azure](linux/planned-maintenance.md).</span></span>
