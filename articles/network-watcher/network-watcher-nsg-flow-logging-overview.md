---
title: Inleiding tot registratie van de stroom voor Netwerkbeveiligingsgroepen met Azure-netwerk-Watcher | Microsoft Docs
description: Deze pagina wordt uitgelegd hoe u NSG stroom Logboeken gebruiken een functie van Azure-netwerk-Watcher
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 47d91341-16f1-45ac-85a5-e5a640f5d59e
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b7a9162d6c6219b6b1c51a49cd34b9616e9d3e8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-flow-logging-for-network-security-groups"></a><span data-ttu-id="edca7-103">Inleiding tot registratie van de stroom voor Netwerkbeveiligingsgroepen</span><span class="sxs-lookup"><span data-stu-id="edca7-103">Introduction to flow logging for Network Security Groups</span></span>

<span data-ttu-id="edca7-104">Netwerkbeveiligingsgroep stroom logboeken zijn een functie van netwerk-Watcher waarmee u informatie bekijken over inkomende en uitgaande IP-verkeer via een Netwerkbeveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="edca7-104">Network Security Group flow logs are a feature of Network Watcher that allows you to view information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="edca7-105">Deze stroom logboeken zijn geschreven in json-indeling en binnenkomende en uitgaande stromen weergeven op basis van een per regel, de NIC die de stroom van toepassing, 5-tuple informatie over de stroom (bron/het doel-IP, bron/het doel-poort, het Protocol) en als het verkeer is toegestaan of geweigerd.</span><span class="sxs-lookup"><span data-stu-id="edca7-105">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

![Overzicht van de stroom-Logboeken][1]

<span data-ttu-id="edca7-107">Stroom registreert Netwerkbeveiligingsgroepen doel, zijn ze niet dezelfde als de andere logboeken worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="edca7-107">While flow logs target Network Security Groups, they are not displayed the same as the other logs.</span></span> <span data-ttu-id="edca7-108">Stroom logboeken worden alleen binnen een opslagaccount en het pad van de logboekregistratie opgeslagen, zoals wordt weergegeven in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="edca7-108">Flow logs are stored only within a storage account and following the logging path as shown in the following example:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="edca7-109">Het bewaarbeleid dezelfde Denk op andere logboeken van toepassing op de logboeken van de stroom.</span><span class="sxs-lookup"><span data-stu-id="edca7-109">The same retention policies as seen on other logs apply to flow logs.</span></span> <span data-ttu-id="edca7-110">Logboeken hebben een bewaarbeleid die kan worden ingesteld van 1 dag en 365 dagen.</span><span class="sxs-lookup"><span data-stu-id="edca7-110">Logs have a retention policy that can be set from 1 day to 365 days.</span></span> <span data-ttu-id="edca7-111">Als geen bewaarbeleid is ingesteld, worden de logboeken voor altijd bewaard.</span><span class="sxs-lookup"><span data-stu-id="edca7-111">If a retention policy is not set, the logs are maintained forever.</span></span>

## <a name="log-file"></a><span data-ttu-id="edca7-112">Logboekbestand</span><span class="sxs-lookup"><span data-stu-id="edca7-112">Log file</span></span>

<span data-ttu-id="edca7-113">Stroom logboeken hebben meerdere eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="edca7-113">Flow logs have multiple properties.</span></span> <span data-ttu-id="edca7-114">De volgende lijst bevat een overzicht van de eigenschappen die worden geretourneerd binnen het NSG stroom logboek:</span><span class="sxs-lookup"><span data-stu-id="edca7-114">The following list is a listing of the properties that are returned within the NSG flow log:</span></span>

* <span data-ttu-id="edca7-115">**tijd** - tijd wanneer de gebeurtenis is vastgelegd</span><span class="sxs-lookup"><span data-stu-id="edca7-115">**time** - Time when the event was logged</span></span>
* <span data-ttu-id="edca7-116">**systeem-id** -Netwerkbeveiligingsgroep resource-id.</span><span class="sxs-lookup"><span data-stu-id="edca7-116">**systemId** - Network Security Group resource Id.</span></span>
* <span data-ttu-id="edca7-117">**categorie** -de categorie van de gebeurtenis is dit altijd NetworkSecurityGroupFlowEvent zijn</span><span class="sxs-lookup"><span data-stu-id="edca7-117">**category** - The category of the event, this is always be NetworkSecurityGroupFlowEvent</span></span>
* <span data-ttu-id="edca7-118">**ResourceID** -de resource-Id van de NSG</span><span class="sxs-lookup"><span data-stu-id="edca7-118">**resourceid** - The resource Id of the NSG</span></span>
* <span data-ttu-id="edca7-119">**operationName** -altijd NetworkSecurityGroupFlowEvents</span><span class="sxs-lookup"><span data-stu-id="edca7-119">**operationName** - Always NetworkSecurityGroupFlowEvents</span></span>
* <span data-ttu-id="edca7-120">**eigenschappen** -een verzameling eigenschappen van de stroom</span><span class="sxs-lookup"><span data-stu-id="edca7-120">**properties** - A collection of properties of the flow</span></span>
    * <span data-ttu-id="edca7-121">**Versie** -versienummer van het schema van de event Log stromen</span><span class="sxs-lookup"><span data-stu-id="edca7-121">**Version** - Version number of the Flow Log event schema</span></span>
    * <span data-ttu-id="edca7-122">**stromen** -een verzameling van stromen.</span><span class="sxs-lookup"><span data-stu-id="edca7-122">**flows** - A collection of flows.</span></span> <span data-ttu-id="edca7-123">Deze eigenschap heeft meerdere vermeldingen voor verschillende regels</span><span class="sxs-lookup"><span data-stu-id="edca7-123">This property has multiple entries for different rules</span></span>
        * <span data-ttu-id="edca7-124">**regel** -regel voor de stromen worden weergegeven</span><span class="sxs-lookup"><span data-stu-id="edca7-124">**rule** - Rule for which the flows are listed</span></span>
            * <span data-ttu-id="edca7-125">**stromen** -een verzameling van stromen</span><span class="sxs-lookup"><span data-stu-id="edca7-125">**flows** - a collection of flows</span></span>
                * <span data-ttu-id="edca7-126">**Mac** -het MAC-adres van de NIC voor de virtuele machine waar de stroom is verzameld</span><span class="sxs-lookup"><span data-stu-id="edca7-126">**mac** - The MAC address of the NIC for the VM where the flow was collected</span></span>
                * <span data-ttu-id="edca7-127">**flowTuples** -een tekenreeks waarin meerdere eigenschappen voor de stroom-tuple in CSV-indeling</span><span class="sxs-lookup"><span data-stu-id="edca7-127">**flowTuples** - A string that contains multiple properties for the flow tuple in comma-separated format</span></span>
                    * <span data-ttu-id="edca7-128">**Tijdstempel** -deze waarde is de tijdstempel van wanneer de stroom is opgetreden in de indeling van de UNIX-EPOCHE</span><span class="sxs-lookup"><span data-stu-id="edca7-128">**Time Stamp** - This value is the time stamp of when the flow occurred in UNIX EPOCH format</span></span>
                    * <span data-ttu-id="edca7-129">**Bron-IP** -de bron-IP</span><span class="sxs-lookup"><span data-stu-id="edca7-129">**Source IP** - The source IP</span></span>
                    * <span data-ttu-id="edca7-130">**Bestemming IP** -de doel-IP</span><span class="sxs-lookup"><span data-stu-id="edca7-130">**Destination IP** - The destination IP</span></span>
                    * <span data-ttu-id="edca7-131">**Bronpoort** -de bronpoort</span><span class="sxs-lookup"><span data-stu-id="edca7-131">**Source Port** - The source port</span></span>
                    * <span data-ttu-id="edca7-132">**Doelpoort** -poort van de bestemming</span><span class="sxs-lookup"><span data-stu-id="edca7-132">**Destination Port** - The destination Port</span></span>
                    * <span data-ttu-id="edca7-133">**Protocol** -het protocol van de stroom.</span><span class="sxs-lookup"><span data-stu-id="edca7-133">**Protocol** - The protocol of the flow.</span></span> <span data-ttu-id="edca7-134">Geldige waarden zijn **T** voor TCP- en **U** voor UDP</span><span class="sxs-lookup"><span data-stu-id="edca7-134">Valid values are **T** for TCP and **U** for UDP</span></span>
                    * <span data-ttu-id="edca7-135">**Verkeer van de stroom** -de richting van het netwerkverkeer.</span><span class="sxs-lookup"><span data-stu-id="edca7-135">**Traffic Flow** - The direction of the traffic flow.</span></span> <span data-ttu-id="edca7-136">Geldige waarden zijn **ik** voor binnenkomend en **O** voor uitgaand.</span><span class="sxs-lookup"><span data-stu-id="edca7-136">Valid values are **I** for inbound and **O** for outbound.</span></span>
                    * <span data-ttu-id="edca7-137">**Verkeer** - of verkeer is toegestaan of geweigerd.</span><span class="sxs-lookup"><span data-stu-id="edca7-137">**Traffic** - Whether traffic was allowed or denied.</span></span> <span data-ttu-id="edca7-138">Geldige waarden zijn **A** voor toegestaan en **D** voor geweigerd.</span><span class="sxs-lookup"><span data-stu-id="edca7-138">Valid values are **A** for allowed and **D** for denied.</span></span>


<span data-ttu-id="edca7-139">Hier volgt een voorbeeld van een stroom voor logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="edca7-139">The following is an example of a Flow log.</span></span> <span data-ttu-id="edca7-140">Zoals u er zijn meerdere records die de lijst met eigenschappen die worden beschreven in de vorige sectie volgen ziet.</span><span class="sxs-lookup"><span data-stu-id="edca7-140">As you can see there are multiple records that follow the property list described in the preceding section.</span></span> 

> [!NOTE]
> <span data-ttu-id="edca7-141">Waarden in de eigenschap flowTuples zijn een door komma's gescheiden lijst.</span><span class="sxs-lookup"><span data-stu-id="edca7-141">Values in the flowTuples property are a comma-separated list.</span></span>
 
```json
{
    "records": 
    [
        
        {
             "time": "2017-02-16T22:00:32.8950000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282421,42.119.146.95,10.1.0.4,51529,5358,T,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282370,163.28.66.17,10.1.0.4,61771,3389,T,I,A","1487282393,5.39.218.34,10.1.0.4,58596,3389,T,I,A","1487282393,91.224.160.154,10.1.0.4,61540,3389,T,I,A","1487282423,13.76.89.229,10.1.0.4,53163,3389,T,I,A"]}]}]}
        }
        ,
        {
             "time": "2017-02-16T22:01:32.8960000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282481,195.78.210.194,10.1.0.4,53,1732,U,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282435,61.129.251.68,10.1.0.4,57776,3389,T,I,A","1487282454,84.25.174.170,10.1.0.4,59085,3389,T,I,A","1487282477,77.68.9.50,10.1.0.4,65078,3389,T,I,A"]}]}]}
        }
        ,
        {
             "time": "2017-02-16T22:02:32.9040000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282492,175.182.69.29,10.1.0.4,28918,5358,T,I,D","1487282505,71.6.216.55,10.1.0.4,8080,8080,T,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282512,91.224.160.154,10.1.0.4,59046,3389,T,I,A"]}]}]}
        }
        ,
        ...
```

## <a name="next-steps"></a><span data-ttu-id="edca7-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="edca7-142">Next steps</span></span>

<span data-ttu-id="edca7-143">Informatie over het inschakelen van stroom Logboeken in via [logboekregistratie inschakelen stromen](network-watcher-nsg-flow-logging-portal.md).</span><span class="sxs-lookup"><span data-stu-id="edca7-143">Learn how to enable Flow logs by visiting [Enabling Flow logging](network-watcher-nsg-flow-logging-portal.md).</span></span>

<span data-ttu-id="edca7-144">Meer informatie over NSG logboekregistratie in via [Meld analytics voor netwerkbeveiligingsgroepen (nsg's)](../virtual-network/virtual-network-nsg-manage-log.md).</span><span class="sxs-lookup"><span data-stu-id="edca7-144">Learn about NSG logging by visiting [Log analytics for network security groups (NSGs)](../virtual-network/virtual-network-nsg-manage-log.md).</span></span>

<span data-ttu-id="edca7-145">Ontdek als verkeer wordt toegestaan of geweigerd op een virtuele machine in via [controleren verkeer met IP-stroom controleren](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="edca7-145">Find out if traffic is allowed or denied on a VM by visiting [Verify traffic with IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-overview/figure1.png

