---
title: aaaMultiple VIP's voor Azure Load Balancer | Microsoft Docs
description: Overzicht van meerdere VIP's op Azure Load Balancer
services: load-balancer
documentationcenter: na
author: chkuhtz
manager: narayan
editor: 
ms.assetid: 748e50cd-3087-4c2e-a9e1-ac0ecce4f869
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/11/2016
ms.author: chkuhtz
ms.openlocfilehash: e186e1248e7d187e7efd0668dc3244465ce3e156
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="multiple-vips-for-azure-load-balancer"></a>Meerdere VIP's voor Azure Load Balancer

Azure Load Balancer kunt u tooload saldo services op meerdere poorten of meerdere IP-adressen. Over een set van virtuele machines kunt u openbare en interne load balancer definities tooload saldo stromen.

Dit artikel wordt beschreven Hallo grondbeginselen van deze mogelijkheid, belangrijke concepten en beperkingen. Als u alleen tooexpose services op één IP-adres wilt, kunt u vinden vereenvoudigde instructies voor het [openbare](load-balancer-get-started-internet-portal.md) of [interne](load-balancer-get-started-ilb-arm-portal.md) load balancer-configuraties. Meerdere VIP's toe te voegen, is incrementele tooa configuratie voor één VIP. Hallo-concepten in dit artikel gebruikt, kunt u een vereenvoudigde configuratie op elk gewenst moment uitbreiden.

Wanneer u een Azure Load Balancer definieert, worden een front-end- en een back-endconfiguratie zijn verbonden met regels. Hallo health test waarnaar wordt verwezen door het Hallo-regel is gebruikte toodetermine hoe nieuwe stromen tooa knooppunt in de back-endpool Hallo worden verzonden. Hallo-frontend is gedefinieerd door een virtuele IP-adres (VIP), dit een 3-tuple bestaat uit een IP-adres (openbare of interne), een transportprotocol (UDP of TCP) en een poortnummer is. Een DIP is dat een IP-adres op een Azure virtuele NIC tooa VM in de back-endpool Hallo gekoppeld.

Hallo volgende tabel bevat enkele voorbeeld-frontend-configuraties:

| VIP | IP-adres | Protocol | poort |
| --- | --- | --- | --- |
| 1 |65.52.0.1 |TCP |80 |
| 2 |65.52.0.1 |TCP |*8080* |
| 3 |65.52.0.1 |*UDP* |80 |
| 4 |*65.52.0.2* |TCP |80 |

Hallo tabel ziet u vier verschillende frontends. Frontends #1, #2 en &#3; zijn een enkele VIP met meerdere regels. Hallo hetzelfde IP-adres wordt gebruikt, maar Hallo-poort of -protocol is verschillend voor elke frontend. Frontends #1 en #4 zijn een voorbeeld van meerdere VIP's waar hello dezelfde frontend-protocol en poort opnieuw worden gebruikt tussen meerdere VIP's.

Azure Load Balancer biedt flexibiliteit voor het definiëren van regels voor taakverdeling Hallo. Een regel verklaart hoe een adres en poort op Hallo frontend toegewezen toohello doeladres en poort op Hallo back-end. Of back-end-poorten zijn opnieuw gebruikt verschillende regels, is afhankelijk van Hallo type Hallo regel. Elk type regel heeft bepaalde vereisten die invloed kunnen zijn op de host-configuratie en test ontwerp. Er zijn twee typen regels:

1. de standaardregel Hallo met geen back endpoort opnieuw gebruiken
2. Hallo zwevend IP regel waar back-end-poorten worden hergebruikt

Azure Load Balancer kunt u toomix beide typen-regel op Hallo van dezelfde load balancer-configuratie. Hallo load balancer kunt gebruiken ze tegelijkertijd voor een bepaalde virtuele machine of een combinatie hiervan, zolang u Hallo beperkingen van de regel Hallo naleeft. Welke regeltype dat u kiest, is afhankelijk van Hallo vereisten van uw toepassing en Hallo complexiteit ondersteunen dat de configuratie. U moet evalueren welke regeltypen zijn het meest geschikt is voor uw scenario.

We verkennen deze scenario's verder door te beginnen met het standaardgedrag Hallo.

## <a name="rule-type-1-no-backend-port-reuse"></a>Regeltype #1: Er is geen back-end-poort opnieuw gebruiken

![MultiVIP-afbeelding](./media/load-balancer-multivip-overview/load-balancer-multivip.png)

In dit scenario worden Hallo frontend VIP's als volgt geconfigureerd:

| VIP | IP-adres | Protocol | poort |
| --- | --- | --- | --- |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |*65.52.0.2* |TCP |80 |

Hallo DIP is de bestemming Hallo Hallo binnenkomende stroom. In de back-endpool hello wordt elke VM Hallo desired-service op een unieke poort op een DIP. Deze service is gekoppeld aan Hallo frontend via de regeldefinitie van een.

We definiëren twee regels:

| Regel | Frontend toewijzen | toobackend van toepassingen |
| --- | --- | --- |
| 1 |![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) VIP1:80 |![back-end](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) DIP1:80, ![back-end](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) DIP2:80 |
| 2 |![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) VIP2:80 |![back-end](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) DIP1:81, ![back-end](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) DIP2:81 |

Hallo voltooid toewijzen in Azure Load Balancer is nu als volgt:

| Regel | VIP-IP-adres | Protocol | poort | Doel | poort |
| --- | --- | --- | --- | --- | --- |
| ![Regel](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |DIP IP-adres |80 |
| ![Regel](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |65.52.0.2 |TCP |80 |DIP IP-adres |81 |

Elke regel moet een stroom met een unieke combinatie van IP-adres en de doelpoort opleveren. Door verschillende Hallo doelpoort van Hallo stroom kunnen meerdere regels leveren stromen toohello dezelfde DIP op verschillende poorten.

Statuscontroles zijn altijd gerichte toohello DIP van een virtuele machine. U moet u zorgen dat uw test Hallo health Hallo VM weergeeft.

## <a name="rule-type-2-backend-port-reuse-by-using-floating-ip"></a>Regeltype #2: back-end-poort opnieuw gebruiken met behulp van zwevend IP

Azure Load Balancer flexibel Hallo tooreuse Hallo front-endpoort over meerdere VIP's ongeacht Hallo regeltype dat u gebruikt. Bovendien sommige toepassingsscenario's liever of Hallo dezelfde die wordt gebruikt door meerdere exemplaren van een toepassing op een enkele virtuele machine in de back-endpool hello toobe poort vereisen. Algemene voorbeelden poort hergebruik van omvatten clustering voor hoge beschikbaarheid, virtuele apparaten en het blootstellen van meerdere TLS eindpunten zonder opnieuw versleutelen.

Als u tooreuse hello backendpoort over meerdere regels wilt, moet u zwevend IP inschakelen in de regeldefinitie Hallo.

Zwevend IP is een deel van wat staat bekend als Direct Server retourneren (DSR). DSR bestaat uit twee delen: een stroom-topologie en een IP-schema. Op een niveau platform werkt Azure Load Balancer altijd in een topologie van de stroom DSR ongeacht of zwevend IP is ingeschakeld of niet. Dit betekent dat Hallo uitgaande deel uitmaakt van een stroom is altijd goed herschreven tooflow rechtstreeks back toohello oorsprong.

Met regeltype Hallo standaard wordt Azure een traditionele load balancing-toewijzingsschema voor IP-adres voor eenvoudig te gebruiken. Inschakelen zwevend IP wijzigingen Hallo IP-adrestoewijzing schema tooallow voor extra flexibiliteit uitgelegd hieronder.

Hallo volgende diagram ziet u deze configuratie:

![MultiVIP-afbeelding](./media/load-balancer-multivip-overview/load-balancer-multivip-dsr.png)

In dit scenario heeft elke virtuele machine in de back-endpool Hallo drie netwerkinterfaces:

* DIP: een virtuele NIC die is gekoppeld aan Hallo VM (IP-configuratie van Azure NIC resource)
* VIP1: een loopback-interface in het gastbesturingssysteem dat is geconfigureerd met IP-adres van VIP1
* VIP2: een loopback-interface in het gastbesturingssysteem dat is geconfigureerd met IP-adres van VIP2

> [!IMPORTANT]
> Hallo-configuratie van de logische interfaces hello wordt uitgevoerd binnen Hallo gastbesturingssysteem. Deze configuratie is niet uitgevoerd of worden beheerd door Azure. Zonder deze configuratie werken Hallo regels niet. Health test definities Hallo DIP Hallo VM gebruiken in plaats van Hallo logische VIP. Daarom moet uw service test antwoorden opgeven op een DIP-poort die Hallo-status van Hallo-service wordt aangeboden op Hallo logische VIP te weerspiegelen.

Stel Hallo dezelfde frontend-configuratie zoals in het voorgaande scenario Hallo:

| VIP | IP-adres | Protocol | poort |
| --- | --- | --- | --- |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |*65.52.0.2* |TCP |80 |

We definiëren twee regels:

| Regel | Frontend toewijzen | toobackend van toepassingen |
| --- | --- | --- |
| 1 |![Regel](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) VIP1:80 |![back-end](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) VIP1:80 (in VM1 en VM2) |
| 2 |![Regel](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) VIP2:80 |![back-end](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) VIP2:80 (in VM1 en VM2) |

Hallo volgende tabel ziet u Hallo volledige toewijzing in Hallo load balancer:

| Regel | VIP-IP-adres | Protocol | poort | Doel | poort |
| --- | --- | --- | --- | --- | --- |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |hetzelfde als het VIP (65.52.0.1) |hetzelfde als het VIP (80) |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |65.52.0.2 |TCP |80 |hetzelfde als het VIP (65.52.0.2) |hetzelfde als het VIP (80) |

Hallo bestemming Hallo stroom voor inkomende hello VIP-adres op Hallo loopback-interface in Hallo VM is. Elke regel moet een stroom met een unieke combinatie van IP-adres en de doelpoort opleveren. Door verschillende Hallo IP-adres van de stroom hello, hergebruik van de poort is mogelijk op Hallo van dezelfde virtuele machine. Uw service is blootgestelde toohello load balancer door deze binding toohello VIP van IP-adres en poort van Hallo respectieve loopback-interface.

Merk op dat in dit voorbeeld Hallo doelpoort niet wijzigt. Hoewel dit een zwevend IP-scenario is, Azure Load Balancer biedt ook ondersteuning voor het definiëren van een back-end doelpoort voor regel toorewrite hello en toomake anders dan de Hallo frontend doelpoort.

Hallo regeltype zwevend IP is Hallo basis van verschillende patronen van load balancer-configuratie. Een voorbeeld dat beschikbaar is Hallo [SQL AlwaysOn met meerdere Listeners](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md) configuratie. Na verloop van tijd documenteren we meer van deze scenario's.

## <a name="limitations"></a>Beperkingen

* Configuraties met meerdere VIP worden alleen ondersteund met IaaS VM's.
* Met Hallo zwevend IP regel, moet uw toepassing hello DIP gebruiken voor uitgaande stromen. Uw toepassing wordt gebonden toohello VIP-adres op Hallo loopback-interface in Hallo Gast OS geconfigureerd, klikt u vervolgens snat omzetten is niet beschikbaar toorewrite Hallo uitgaande stroom als Hallo-stroom is mislukt.
* Openbare IP-adressen hebben een invloed op de facturering. Zie voor meer informatie [prijzen van IP-adres](https://azure.microsoft.com/pricing/details/ip-addresses/)
* Abonnement-beperkingen gelden. Zie voor meer informatie [Servicelimieten](../azure-subscription-service-limits.md#networking-limits) voor meer informatie.
