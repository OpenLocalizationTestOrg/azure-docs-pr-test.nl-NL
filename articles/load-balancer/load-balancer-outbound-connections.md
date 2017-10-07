---
title: uitgaande verbindingen aaaUnderstanding in Azure | Microsoft Docs
description: Dit artikel wordt uitgelegd hoe de Azure VM's toocommunicate met openbare internetservices kunt.
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
ms.assetid: 5f666f2a-3a63-405a-abcd-b2e34d40e001
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 5/31/2017
ms.author: kumud
ms.openlocfilehash: ffe59971b934a16c9f6f78e3b15869a0072320d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-outbound-connections-in-azure"></a>Uitleg over uitgaande verbindingen in Azure

Een virtuele Machine (VM) in Azure kunnen communiceren met de eindpunten buiten Azure in openbare IP-adresruimte. Wanneer een virtuele machine een uitgaande stroom tooa doel in openbare IP-adresruimte initieert, wordt Azure Hallo van de virtuele machine privé IP-adres tooa openbare IP-adres wordt toegewezen en kunt terugkerend verkeer tooreach Hallo VM.

Azure biedt drie verschillende methoden tooachieve uitgaande verbindingen. Elke methode heeft een eigen mogelijkheden en beperkingen. Elke methode zorgvuldig te controleren toochoose die aan uw behoeften voldoet.

| Scenario | Methode | Opmerking |
| --- | --- | --- |
| Standalone VM (Er is geen load balancer, geen Instance Level Public IP-adres) |Standaard snat omzetten |Azure koppelt een openbare IP-adres voor snat omzetten |
| Taakverdeling VM (geen Instance Level Public IP-adres op virtuele machine) |Snat omzetten met Hallo load balancer |Azure maakt gebruik van een openbaar IP-adres van de Load Balancer Hallo voor snat omzetten |
| Virtuele machine met Instance Level Public IP-adres (met of zonder load balancer) |Snat omzetten wordt niet gebruikt. |Hallo openbare IP-adres toegewezen toohello VM maakt gebruik van Azure |

Als u niet dat een VM-toocommunicate met eindpunten buiten Azure in openbare IP-adresruimte wilt, kunt u Netwerkbeveiligingsgroep groepen (NSG) tooblock toegang gebruiken. Met behulp van de nsg's wordt besproken in nader [openbare connectiviteit voorkomen](#preventing-public-connectivity).

## <a name="standalone-vm-with-no-instance-level-public-ip-address"></a>Standalone VM zonder Instance Level Public IP-adres

In dit scenario Hallo VM maakt geen deel uit van een pool Load Balancer van Azure en heeft een exemplaar niveau openbare IP (ILPIP)-adres toegewezen tooit geen. Wanneer Hallo VM een uitgaande stroom maakt, vertaalt Azure Hallo persoonlijke IP-bronadres van Hallo uitgaande stroom tooa openbare IP-bronadres. Hallo openbare IP-adres voor deze uitgaande stroom kan niet worden geconfigureerd en komt niet in mindering gebracht op Hallo van openbare IP-resource limiet voor het abonnement. Azure bron Network Address Translation (snat omzetten) tooperform deze functie gebruikt. Kortstondige poorten Hallo openbare IP-adres zijn gebruikte toodistinguish afzonderlijke stromen afkomstig van Hallo VM. Kortstondige poorten snat omzetten dynamisch toegewezen wanneer stromen worden gemaakt. In deze context worden Hallo kortstondige poorten gebruikt voor snat omzetten waarnaar wordt verwezen tooas snat omzetten poorten.

Snat omzetten poorten zijn een eindige resource die kan worden verbruikt. Het is belangrijk toounderstand hoe ze worden verbruikt. Één snat omzetten poort wordt per stroom tooa enkel IP-adres gebruikt. Voor meerdere stromen toohello hetzelfde doel-IP-adres, elke stroom verbruikt één poort snat omzetten. Dit zorgt ervoor dat Hallo stromen unieke wanneer afkomstig is van Hallo dezelfde openbare IP-adres toohello hetzelfde IP-doeladres. Meerdere stromen elke tooa verschillende IP-doeladres gebruiken één poort per bestemming snat omzetten. de IP-doeladres Hallo maakt Hallo stromen uniek.

U kunt [Log Analytics voor Load Balancer](load-balancer-monitor-log.md) en [waarschuwing gebeurtenislogboeken toomonitor voor snat omzetten poort uitputting berichten](load-balancer-monitor-log.md#alert-event-log). Wanneer snat omzetten poort resources zijn uitgeput, mislukken uitgaande stromen tot snat omzetten poorten zijn vrijgegeven door bestaande stromen. Load Balancer gebruikmaakt van een niet-actieve time-out van 4 minuten voor het vrijmaken van poorten snat omzetten.

## <a name="load-balanced-vm-with-no-instance-level-public-ip-address"></a>Taakverdeling met virtuele machine geen Instance Level Public IP-adres

In dit scenario uitmaakt Hallo VM deel van een Load Balancer van Azure-toepassingen.  Hallo VM heeft geen een openbaar IP-adres toegewezen tooit. Hallo Load Balancer resource moet worden geconfigureerd met een regel toolink Hallo openbare IP-frontend met Hallo back-endpool.  Als u deze configuratie niet uitvoert, is Hallo gedrag zoals beschreven in de sectie Hallo hierboven voor [Standalone VM met geen Instance Level Public IP](load-balancer-outbound-connections.md#standalone-vm-with-no-instance-level-public-ip-address).

Wanneer hello taakverdeling VM een uitgaande stroom maakt, vertaalt Azure Hallo persoonlijke IP-bronadres van Hallo uitgaande stroom toohello openbaar IP-adres van de openbare Load Balancer-frontend Hallo. Azure bron Network Address Translation (snat omzetten) tooperform deze functie gebruikt. Kortstondige poorten Hallo Load Balancer openbare IP-adres zijn gebruikte toodistinguish afzonderlijke stromen afkomstig van Hallo VM. Kortstondige poorten snat omzetten dynamisch toegewezen wanneer uitgaande stromen worden gemaakt. In deze context worden Hallo kortstondige poorten gebruikt voor snat omzetten waarnaar wordt verwezen tooas snat omzetten poorten.

Snat omzetten poorten zijn een eindige resource die kan worden verbruikt. Het is belangrijk toounderstand hoe ze worden verbruikt. Één snat omzetten poort wordt per stroom tooa enkel IP-adres gebruikt. Voor meerdere stromen toohello hetzelfde doel-IP-adres, elke stroom verbruikt één poort snat omzetten. Dit zorgt ervoor dat Hallo stromen unieke wanneer afkomstig is van Hallo dezelfde openbare IP-adres toohello hetzelfde IP-doeladres. Meerdere stromen elke tooa verschillende IP-doeladres gebruiken één poort per bestemming snat omzetten. de IP-doeladres Hallo maakt Hallo stromen uniek.

U kunt [Log Analytics voor Load Balancer](load-balancer-monitor-log.md) en [waarschuwing gebeurtenislogboeken toomonitor voor snat omzetten poort uitputting berichten](load-balancer-monitor-log.md#alert-event-log). Wanneer snat omzetten poort resources zijn uitgeput, mislukken uitgaande stromen tot snat omzetten poorten zijn vrijgegeven door bestaande stromen. Load Balancer gebruikmaakt van een niet-actieve time-out van 4 minuten voor het vrijmaken van poorten snat omzetten.

## <a name="vm-with-an-instance-level-public-ip-address-with-or-without-load-balancer"></a>Virtuele machine met een Instance Level Public IP-adres (met of zonder Load Balancer)

In dit scenario heeft Hallo VM een exemplaar niveau openbare IP (ILPIP) tooit toegewezen. Het maakt niet uit of Hallo VM gelijkmatig verdeeld wordt, of niet. Wanneer een ILPIP wordt gebruikt, wordt de bron Network Address Translation (snat omzetten) niet gebruikt. Hallo ILPIP Hallo VM gebruikt voor alle uitgaande stromen. Als uw toepassing veel uitgaande stromen initieert en u snat omzetten uitputting ondervindt, kunt u overwegen een tooavoid ILPIP snat omzetten beperkingen toewijzen.

## <a name="discovering-hello-public-ip-used-by-a-given-vm"></a>Hallo openbare IP-adres gebruikt door een bepaalde virtuele machine detecteren

Er zijn veel manieren toodetermine Hallo openbare IP-bronadres van een uitgaande verbinding. OpenDNS biedt een service die u kunt weergeven Hallo openbare IP-adres van uw virtuele machine. Hallo nslookup-opdracht kunt u een DNS-query verzenden voor Hallo naam myip.opendns.com toohello OpenDNS conflictoplosser. Hallo-service retourneert Hallo bron IP-adres dat gebruikt toosend Hallo query is. Als u de volgende query uit uw VM Hallo uitvoert, is antwoord Hallo Hallo die openbare IP-adres wordt gebruikt voor die VM.

    nslookup myip.opendns.com resolver1.opendns.com

## <a name="preventing-public-connectivity"></a>Zo wordt voorkomen dat openbare-connectiviteit

Soms is het ongewenste voor een VM-toobe toegestaan toocreate een uitgaande stroom of er is een vereiste toomanage welke doelen kunnen worden bereikt met uitgaande stromen. In dit geval gebruikt u [Netwerkbeveiligingsgroep groepen (NSG)](../virtual-network/virtual-networks-nsg.md) toomanage Hallo bestemmingen die Hallo VM kan bereiken. Wanneer u een NSG toepast tooa taakverdeling VM, moet u toopay aandacht toohello [standaard labels](../virtual-network/virtual-networks-nsg.md#default-tags) en [regels standaard](../virtual-network/virtual-networks-nsg.md#default-rules).

U moet ervoor zorgen dat Hallo VM health test aanvragen kan ontvangen van Azure Load Balancer. Als een NSG blokken health test aanvragen van Hallo AZURE_LOADBALANCER standaardlabel, uw VM health test mislukt en Hallo VM is gemarkeerd als niet actief. Load Balancer stopt het verzenden van nieuwe stromen toothat VM.

## <a name="limitations"></a>Beperkingen

Als [meerdere (openbare) IP-adressen zijn gekoppeld aan een load balancer](load-balancer-multivip-overview.md), een van deze openbare IP-adressen zijn geschikt is voor uitgaande stromen.

Azure maakt gebruik van een algoritme toodetermine Hallo aantal snat omzetten beschikbare poorten op basis van de grootte Hallo van Hallo van toepassingen.  Dit kan op dit moment niet worden geconfigureerd.

Het is belangrijk toorememember die het aantal beschikbare poorten voor snat omzetten Hallo niet rechtstreeks omgezet toonumber van verbindingen. Raadpleeg hierboven voor specifieke informatie over wanneer en hoe snat omzetten poorten zijn toegewezen en hoe toomanage deze onuitputtelijk bron.
