---
title: aaaIntroduction tooflow logboekregistratie voor Netwerkbeveiligingsgroepen met Azure-netwerk-Watcher | Microsoft Docs
description: Deze pagina wordt uitgelegd hoe toouse NSG stroom registreert voor een functie van Azure-netwerk-Watcher
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
ms.openlocfilehash: da85e946147b14717144cb47d1c742057c6dfa24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooflow-logging-for-network-security-groups"></a><span data-ttu-id="4456a-103">Inleiding tooflow logboekregistratie voor Netwerkbeveiligingsgroepen</span><span class="sxs-lookup"><span data-stu-id="4456a-103">Introduction tooflow logging for Network Security Groups</span></span>

<span data-ttu-id="4456a-104">Netwerkbeveiligingsgroep stroom logboeken zijn een functie van netwerk-Watcher waarmee u tooview informatie over inkomende en uitgaande IP-verkeer via een Netwerkbeveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="4456a-104">Network Security Group flow logs are a feature of Network Watcher that allows you tooview information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="4456a-105">Deze stroom logboeken zijn geschreven in json-indeling en weergeven van uitgaande en inkomende stromen per regel op basis van een Hallo NIC Hallo stroom is van toepassing op 5-tuple informatie over het Hallo-stroom (bron/het doel-IP, bron/het doel-poort, het Protocol) en als hello verkeer is toegestaan of geweigerd.</span><span class="sxs-lookup"><span data-stu-id="4456a-105">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

![Overzicht van de stroom-Logboeken][1]

<span data-ttu-id="4456a-107">Terwijl de stroom registreert Netwerkbeveiligingsgroepen doel, worden ze niet weergegeven Hallo dezelfde als Hallo andere logboeken.</span><span class="sxs-lookup"><span data-stu-id="4456a-107">While flow logs target Network Security Groups, they are not displayed hello same as hello other logs.</span></span> <span data-ttu-id="4456a-108">Stroom logboeken worden opgeslagen alleen binnen een opslagaccount en een pad naar de volgende Hallo logboekregistratie, zoals wordt weergegeven in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="4456a-108">Flow logs are stored only within a storage account and following hello logging path as shown in hello following example:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="4456a-109">Hallo dezelfde bewaarbeleidsregels weergegeven op andere logboeken tooflow logboeken toegepast.</span><span class="sxs-lookup"><span data-stu-id="4456a-109">hello same retention policies as seen on other logs apply tooflow logs.</span></span> <span data-ttu-id="4456a-110">Logboeken hebben een bewaarbeleid van 1 dag too365 dagen kan worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="4456a-110">Logs have a retention policy that can be set from 1 day too365 days.</span></span> <span data-ttu-id="4456a-111">Als een bewaarbeleid niet is ingesteld, worden altijd Hallo logboeken gehandhaafd.</span><span class="sxs-lookup"><span data-stu-id="4456a-111">If a retention policy is not set, hello logs are maintained forever.</span></span>

## <a name="log-file"></a><span data-ttu-id="4456a-112">Logboekbestand</span><span class="sxs-lookup"><span data-stu-id="4456a-112">Log file</span></span>

<span data-ttu-id="4456a-113">Stroom logboeken hebben meerdere eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="4456a-113">Flow logs have multiple properties.</span></span> <span data-ttu-id="4456a-114">Hallo bevat volgende lijst een overzicht van Hallo-eigenschappen die worden geretourneerd in Hallo NSG stroom logboek in:</span><span class="sxs-lookup"><span data-stu-id="4456a-114">hello following list is a listing of hello properties that are returned within hello NSG flow log:</span></span>

* <span data-ttu-id="4456a-115">**tijd** - bij het Hallo-gebeurtenis is vastgelegd</span><span class="sxs-lookup"><span data-stu-id="4456a-115">**time** - Time when hello event was logged</span></span>
* <span data-ttu-id="4456a-116">**systeem-id** -Netwerkbeveiligingsgroep resource-id.</span><span class="sxs-lookup"><span data-stu-id="4456a-116">**systemId** - Network Security Group resource Id.</span></span>
* <span data-ttu-id="4456a-117">**categorie** -Hallo categorie van de gebeurtenis hello, is dit altijd NetworkSecurityGroupFlowEvent zijn</span><span class="sxs-lookup"><span data-stu-id="4456a-117">**category** - hello category of hello event, this is always be NetworkSecurityGroupFlowEvent</span></span>
* <span data-ttu-id="4456a-118">**ResourceID** -resource-Id van het NSG Hallo Hallo</span><span class="sxs-lookup"><span data-stu-id="4456a-118">**resourceid** - hello resource Id of hello NSG</span></span>
* <span data-ttu-id="4456a-119">**operationName** -altijd NetworkSecurityGroupFlowEvents</span><span class="sxs-lookup"><span data-stu-id="4456a-119">**operationName** - Always NetworkSecurityGroupFlowEvents</span></span>
* <span data-ttu-id="4456a-120">**eigenschappen** -een verzameling eigenschappen van Hallo stroom</span><span class="sxs-lookup"><span data-stu-id="4456a-120">**properties** - A collection of properties of hello flow</span></span>
    * <span data-ttu-id="4456a-121">**Versie** -versienummer van Hallo stromen logboek gebeurtenis schema</span><span class="sxs-lookup"><span data-stu-id="4456a-121">**Version** - Version number of hello Flow Log event schema</span></span>
    * <span data-ttu-id="4456a-122">**stromen** -een verzameling van stromen.</span><span class="sxs-lookup"><span data-stu-id="4456a-122">**flows** - A collection of flows.</span></span> <span data-ttu-id="4456a-123">Deze eigenschap heeft meerdere vermeldingen voor verschillende regels</span><span class="sxs-lookup"><span data-stu-id="4456a-123">This property has multiple entries for different rules</span></span>
        * <span data-ttu-id="4456a-124">**regel** -regel voor welke Hallo stromen worden weergegeven</span><span class="sxs-lookup"><span data-stu-id="4456a-124">**rule** - Rule for which hello flows are listed</span></span>
            * <span data-ttu-id="4456a-125">**stromen** -een verzameling van stromen</span><span class="sxs-lookup"><span data-stu-id="4456a-125">**flows** - a collection of flows</span></span>
                * <span data-ttu-id="4456a-126">**Mac** -MAC-adres van Hallo NIC voor VM waar Hallo-stroom werd verzameld Hallo Hallo</span><span class="sxs-lookup"><span data-stu-id="4456a-126">**mac** - hello MAC address of hello NIC for hello VM where hello flow was collected</span></span>
                * <span data-ttu-id="4456a-127">**flowTuples** -een tekenreeks waarin meerdere eigenschappen voor Hallo stroom tuple in CSV-indeling</span><span class="sxs-lookup"><span data-stu-id="4456a-127">**flowTuples** - A string that contains multiple properties for hello flow tuple in comma-separated format</span></span>
                    * <span data-ttu-id="4456a-128">**Tijdstempel** -deze waarde is Hallo tijdstempel wanneer het Hallo-stroom is opgetreden in de indeling van de UNIX-EPOCHE</span><span class="sxs-lookup"><span data-stu-id="4456a-128">**Time Stamp** - This value is hello time stamp of when hello flow occurred in UNIX EPOCH format</span></span>
                    * <span data-ttu-id="4456a-129">**Bron-IP** - hello bron-IP</span><span class="sxs-lookup"><span data-stu-id="4456a-129">**Source IP** - hello source IP</span></span>
                    * <span data-ttu-id="4456a-130">**Bestemming IP** -Hallo doel-IP</span><span class="sxs-lookup"><span data-stu-id="4456a-130">**Destination IP** - hello destination IP</span></span>
                    * <span data-ttu-id="4456a-131">**Bronpoort** - hello bronpoort</span><span class="sxs-lookup"><span data-stu-id="4456a-131">**Source Port** - hello source port</span></span>
                    * <span data-ttu-id="4456a-132">**Doelpoort** -Hallo doelpoort</span><span class="sxs-lookup"><span data-stu-id="4456a-132">**Destination Port** - hello destination Port</span></span>
                    * <span data-ttu-id="4456a-133">**Protocol** -protocol van de stroom Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="4456a-133">**Protocol** - hello protocol of hello flow.</span></span> <span data-ttu-id="4456a-134">Geldige waarden zijn **T** voor TCP- en **U** voor UDP</span><span class="sxs-lookup"><span data-stu-id="4456a-134">Valid values are **T** for TCP and **U** for UDP</span></span>
                    * <span data-ttu-id="4456a-135">**Verkeer van de stroom** -Hallo richting van het Hallo-netwerkverkeer.</span><span class="sxs-lookup"><span data-stu-id="4456a-135">**Traffic Flow** - hello direction of hello traffic flow.</span></span> <span data-ttu-id="4456a-136">Geldige waarden zijn **ik** voor binnenkomend en **O** voor uitgaand.</span><span class="sxs-lookup"><span data-stu-id="4456a-136">Valid values are **I** for inbound and **O** for outbound.</span></span>
                    * <span data-ttu-id="4456a-137">**Verkeer** - of verkeer is toegestaan of geweigerd.</span><span class="sxs-lookup"><span data-stu-id="4456a-137">**Traffic** - Whether traffic was allowed or denied.</span></span> <span data-ttu-id="4456a-138">Geldige waarden zijn **A** voor toegestaan en **D** voor geweigerd.</span><span class="sxs-lookup"><span data-stu-id="4456a-138">Valid values are **A** for allowed and **D** for denied.</span></span>


<span data-ttu-id="4456a-139">Hallo Hieronder volgt een voorbeeld van een stroom-logboek.</span><span class="sxs-lookup"><span data-stu-id="4456a-139">hello following is an example of a Flow log.</span></span> <span data-ttu-id="4456a-140">Zoals u er zijn meerdere records die Hallo eigenschappenlijst beschreven in voorgaande sectie Hallo volgen ziet.</span><span class="sxs-lookup"><span data-stu-id="4456a-140">As you can see there are multiple records that follow hello property list described in hello preceding section.</span></span> 

> [!NOTE]
> <span data-ttu-id="4456a-141">Waarden in de eigenschap flowTuples Hallo zijn een door komma's gescheiden lijst.</span><span class="sxs-lookup"><span data-stu-id="4456a-141">Values in hello flowTuples property are a comma-separated list.</span></span>
 
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

## <a name="next-steps"></a><span data-ttu-id="4456a-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4456a-142">Next steps</span></span>

<span data-ttu-id="4456a-143">Meer informatie over hoe tooenable stroom registreert in via [logboekregistratie inschakelen stromen](network-watcher-nsg-flow-logging-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4456a-143">Learn how tooenable Flow logs by visiting [Enabling Flow logging](network-watcher-nsg-flow-logging-portal.md).</span></span>

<span data-ttu-id="4456a-144">Meer informatie over NSG logboekregistratie in via [Meld analytics voor netwerkbeveiligingsgroepen (nsg's)](../virtual-network/virtual-network-nsg-manage-log.md).</span><span class="sxs-lookup"><span data-stu-id="4456a-144">Learn about NSG logging by visiting [Log analytics for network security groups (NSGs)](../virtual-network/virtual-network-nsg-manage-log.md).</span></span>

<span data-ttu-id="4456a-145">Ontdek als verkeer wordt toegestaan of geweigerd op een virtuele machine in via [controleren verkeer met IP-stroom controleren](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="4456a-145">Find out if traffic is allowed or denied on a VM by visiting [Verify traffic with IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-overview/figure1.png

