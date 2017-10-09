---
title: een virtueel netwerk voor een Premium Azure Redis-Cache aaaConfigure | Microsoft Docs
description: Meer informatie over hoe toocreate en Virtual Network-ondersteuning voor uw exemplaren Premium-laag Azure Redis-Cache beheren
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 8b1e43a0-a70e-41e6-8994-0ac246d8bf7f
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: sdanie
ms.openlocfilehash: fab715f4d9365ee4c2f8b89d2e2e58768c25b671
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-virtual-network-support-for-a-premium-azure-redis-cache"></a>Hoe tooconfigure Virtual Network-ondersteuning voor een Premium Azure Redis-Cache
Azure Redis-Cache heeft verschillende cache aanbiedingen die flexibiliteit bij het Hallo-keuze van de cachegrootte en -onderdelen bieden, met inbegrip van Premium-laag functies zoals clustering, persistentie en virtual network-ondersteuning. Een VNet is een particulier netwerk in Hallo cloud. Wanneer een Azure Redis-Cache-exemplaar is geconfigureerd met een VNet, is niet openbaar toegankelijk en kunnen alleen worden geopend vanuit virtuele machines en toepassingen binnen Hallo VNet. Dit artikel wordt beschreven hoe het virtuele netwerk tooconfigure ondersteuning bieden voor een premium Azure Redis-Cache-exemplaar.

> [!NOTE]
> Azure Redis-Cache ondersteunt zowel klassieke en Resource Manager VNets.
> 
> 

Zie voor informatie over andere functies van premium-cache, [inleiding toohello Azure Redis-Cache Premium-laag](cache-premium-tier-intro.md).

## <a name="why-vnet"></a>Waarom VNet?
[Azure-netwerk (VNet)](https://azure.microsoft.com/services/virtual-network/) implementatie biedt verbeterde beveiliging en isolatie voor uw Azure Redis-Cache, evenals de subnetten, toegangscontrolebeleid, en andere functies toofurther toegang beperken.

## <a name="virtual-network-support"></a>Virtual network-ondersteuning
Ondersteuning voor Virtual Network (VNet) is geconfigureerd op Hallo **nieuwe Redis-Cache** blade tijdens het maken van de cache. 

[!INCLUDE [redis-cache-create](../../includes/redis-cache-premium-create.md)]

Nadat u een premium-prijscategorie hebt geselecteerd, kunt u VNet Redis-integratie configureren met behulp van een VNet dat in Hallo hetzelfde abonnement en dezelfde locatie als uw cache. toouse een nieuw VNet maken het eerst door de volgende stappen in Hallo [een virtueel netwerk maken met Azure-portal Hallo](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) of [een virtueel netwerk (klassiek) maken met behulp van Azure-portal Hallo](../virtual-network/virtual-networks-create-vnet-classic-pportal.md) en ga daarna terug toohello **Nieuwe Redis-Cache** blade toocreate en configureren van uw premium-cache.

tooconfigure hello VNet voor de nieuwe cache, klikt u op **virtueel netwerk** op Hallo **nieuwe Redis-Cache** blade en selecteer Hallo gewenst VNet uit de vervolgkeuzelijst Hallo.

![Virtueel netwerk][redis-cache-vnet]

Selecteer de gewenste subnet uit Hallo Hallo **Subnet** vervolgkeuzelijst lijst en geef de gewenste Hallo **statisch IP-adres**. Als u van een klassiek VNet hello gebruikmaakt **statisch IP-adres** veld is optioneel en als niets wordt opgegeven, wordt een gekozen van subnet Hallo geselecteerd.

> [!IMPORTANT]
> Bij het implementeren van een Azure Redis-Cache tooa Resource Manager VNet moet Hallo cache een toegewezen subnet dat geen andere resources, met uitzondering van Azure Redis-Cache-exemplaren bevat. Als wordt geprobeerd toodeploy wordt een Azure Redis-Cache tooa Resource Manager VNet tooa subnet met andere resources, het Hallo-implementatie mislukt.
> 
> 

![Virtueel netwerk][redis-cache-vnet-ip]

> [!IMPORTANT]
> Azure bepaalde IP-adressen binnen elk subnet gereserveerd en deze adressen kunnen niet worden gebruikt. Hallo zijn eerste en laatste IP-adressen van Hallo subnetten gereserveerd voor protocol overeenstemming, samen met drie meer adressen voor Azure-services gebruikt. Zie voor meer informatie [zijn er beperkingen voor het gebruik van IP-adressen binnen deze subnetten?](../virtual-network/virtual-networks-faq.md#are-there-any-restrictions-on-using-ip-addresses-within-these-subnets)
> 
> Bij toevoeging toohello IP-adressen die worden gebruikt door hello Azure VNET infrastructuur, elke Redis-exemplaar in Hallo subnet gebruikt twee IP-adressen per shard en één extra IP-adres voor Hallo load balancer. Een niet-geclusterde cache wordt beschouwd als een shard toohave.
> 
> 

Nadat het Hallo-cache wordt gemaakt, kunt u Hallo-configuratie voor Hallo VNet weergeven door te klikken op **virtueel netwerk** van Hallo **Resource menu**.

![Virtueel netwerk][redis-cache-vnet-info]

tooconnect tooyour Azure Redis-cache-exemplaar bij gebruik van een VNet Geef Hallo-hostnaam van uw cache in de verbindingsreeks Hallo zoals weergegeven in het volgende voorbeeld Hallo:

    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        return ConnectionMultiplexer.Connect("contoso5premium.redis.cache.windows.net,abortConnect=false,ssl=true,password=password");
    });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

## <a name="azure-redis-cache-vnet-faq"></a>Azure Redis-Cache VNet Veelgestelde vragen
Hallo volgende lijst bevat toocommonly van antwoorden op veelgestelde vragen over het schalen van hello Azure Redis-Cache.

* [Wat zijn enkele veelvoorkomende configuratiefouten bij Azure Redis-Cache en VNets?](#what-are-some-common-misconfiguration-issues-with-azure-redis-cache-and-vnets)
* [Hoe kan ik mijn cache werkt in een VNET controleren?](#how-can-i-verify-that-my-cache-is-working-in-a-vnet)
* [Kan ik VNets met een standaard of basic-cache gebruiken?](#can-i-use-vnets-with-a-standard-or-basic-cache)
* [Waarom een Redis-cache niet in sommige subnetten maar geen andere?](#why-does-creating-a-redis-cache-fail-in-some-subnets-but-not-others)
* [Wat zijn Hallo subnet adresvereisten?](#what-are-the-subnet-address-space-requirements)
* [Werk alle functies van de cache bij het hosten van een cache in een VNET?](#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)

## <a name="what-are-some-common-misconfiguration-issues-with-azure-redis-cache-and-vnets"></a>Wat zijn enkele veelvoorkomende configuratiefouten bij Azure Redis-Cache en VNets?
Wanneer Azure Redis-Cache wordt gehost in een VNet, worden Hallo-poorten in Hallo volgende tabellen gebruikt. 

>[!IMPORTANT]
>Als het Hallo-poorten in Hallo volgende tabellen worden geblokkeerd, is het mogelijk dat Hallo cache niet goed werkt. Met een of meer van deze poorten geblokkeerd is Hallo meest voorkomende onjuiste configuratie probleem wanneer u Azure Redis-Cache in een VNet.
> 
> 

- [Vereisten voor de uitgaande poort](#outbound-port-requirements)
- [Vereisten voor de binnenkomende poort](#inbound-port-requirements)

### <a name="outbound-port-requirements"></a>Vereisten voor de uitgaande poort

Er zijn zeven vereisten van de uitgaande poort.

- Indien gewenst, alle uitgaande verbindingen toohello internet via een client kan worden gemaakt op lokale controlemogelijkheden apparaten.
- Drie Hallo poorten verkeer tooAzure eindpunten onderhoud Azure Storage en Azure DNS worden gerouteerd.
- Hallo resterende poortbereiken en voor interne communicatie voor Redis-subnet. Er is geen subnet NSG-regels zijn vereist voor interne communicatie voor Redis-subnet.

| Poort(en) | Richting | Protocol-Transport | Doel | Lokaal IP | Externe IP |
| --- | --- | --- | --- | --- | --- |
| 80, 443 |Uitgaand |TCP |Redis-afhankelijkheden op Azure Storage/PKI (Internet) | (Redis subnet) |* |
| 53 |Uitgaand |TCP/UDP |Afhankelijkheden van DNS (Internet/VNet) redis | (Redis subnet) |* |
| 8443 |Uitgaand |TCP |Interne communicatie voor Redis | (Redis subnet) | (Redis subnet) |
| 10221-10231 |Uitgaand |TCP |Interne communicatie voor Redis | (Redis subnet) | (Redis subnet) |
| 20226 |Uitgaand |TCP |Interne communicatie voor Redis | (Redis subnet) |(Redis subnet) |
| 13000-13999 |Uitgaand |TCP |Interne communicatie voor Redis | (Redis subnet) |(Redis subnet) |
| 15000-15999 |Uitgaand |TCP |Interne communicatie voor Redis | (Redis subnet) |(Redis subnet) |


### <a name="inbound-port-requirements"></a>Vereisten voor de binnenkomende poort

Er zijn acht vereisten voor het bereik van binnenkomende poort. Inkomende aanvragen in deze bereiken zijn inkomende verkeer van andere services die worden gehost in Hallo hetzelfde VNET of interne toohello Redis subnet communicatie.

| Poort(en) | Richting | Protocol-Transport | Doel | Lokaal IP | Externe IP |
| --- | --- | --- | --- | --- | --- |
| 6379, 6380 |Inkomend |TCP |Client communicatie tooRedis, Azure taakverdeling | (Redis subnet) |Virtueel netwerk, Azure Load Balancer |
| 8443 |Inkomend |TCP |Interne communicatie voor Redis | (Redis subnet) |(Redis subnet) |
| 8500 |Inkomend |TCP/UDP |Azure load balancing | (Redis subnet) |Azure Load Balancer |
| 10221-10231 |Inkomend |TCP |Interne communicatie voor Redis | (Redis subnet) |(Redis subnet), Load Balancer van Azure |
| 13000-13999 |Inkomend |TCP |Client communicatie tooRedis Clusters, Azure load balancing | (Redis subnet) |Virtueel netwerk, Azure Load Balancer |
| 15000-15999 |Inkomend |TCP |Client communicatie tooRedis Clusters, Azure load Balancing | (Redis subnet) |Virtueel netwerk, Azure Load Balancer |
| 16001 |Inkomend |TCP/UDP |Azure load balancing | (Redis subnet) |Azure Load Balancer |
| 20226 |Inkomend |TCP |Interne communicatie voor Redis | (Redis subnet) |(Redis subnet) |

### <a name="additional-vnet-network-connectivity-requirements"></a>Aanvullende VNET-connectiviteit netwerkvereisten

Er zijn verbindingsproblemen netwerkvereisten voor Azure Redis-Cache kan niet in eerste instantie in een virtueel netwerk worden voldaan. Azure Redis-Cache is vereist op dat alle Hallo items toofunction correct bij gebruik binnen een virtueel netwerk te volgen.

* Uitgaande connectiviteit tooAzure opslag netwerkeindpunten overal ter wereld. Dit omvat eindpunten zich in Hallo dezelfde regio bevinden als hello Azure Redis-Cache-exemplaar, evenals de storage-eindpunten zich in **andere** Azure-regio's. Azure Storage-eindpunten omgezet onder de volgende DNS-domeinen Hallo: *table.core.windows.net*, *blob.core.windows.net*, *queue.core.windows.net*, en *file.core.windows.net*. 
* Uitgaande netwerkverbinding te*ocsp.msocsp.com*, *mscrl.microsoft.com*, en *crl.microsoft.com*. Deze connectiviteit is benodigde toosupport SSL-functionaliteit.
* Hallo DNS-configuratie voor het virtuele netwerk Hallo moet geschikt is voor het oplossen van alle Hallo eindpunten en domeinen die zijn vermeld in Hallo eerdere punten. Deze DNS-vereisten kunnen worden voldaan door te zorgen voor een geldig DNS-infrastructuur is geconfigureerd en onderhouden voor Hallo virtuele netwerk.
* Uitgaande network connectivity toohello Azure Monitoring-eindpunten die onder de volgende DNS-domeinen Hallo oplossen na: shoebox2 black.shoebox2.metrics.nsatc.net, Noord-prod2.prod2.metrics.nsatc.net azglobal-black.azglobal.metrics.nsatc.net, shoebox2-red.shoebox2.metrics.nsatc.net, Oost-prod2.prod2.metrics.nsatc.net azglobal-red.azglobal.metrics.nsatc.net.

### <a name="how-can-i-verify-that-my-cache-is-working-in-a-vnet"></a>Hoe kan ik mijn cache werkt in een VNET controleren?

>[!IMPORTANT]
>Wanneer u verbinding maakt tooan Azure Redis-Cache-exemplaar dat wordt gehost in een VNET, Hallo uw cache moeten clients zich in hetzelfde VNET, met inbegrip van de testtoepassingen of diagnostische hulpprogramma's voor pingen.
>
>

Nadat port requirements for Windows hello zijn geconfigureerd zoals beschreven in de vorige sectie hello, kunt u controleren of uw cache werkt door Hallo volgende stappen uit te voeren.

- [Opnieuw opstarten](cache-administration.md#reboot) Hallo alle knooppunten in de cache. Als alle Hallo vereiste cacheafhankelijkheden kunnen niet worden bereikt (zoals beschreven in [Poortvereisten voor binnenkomende](cache-how-to-premium-vnet.md#inbound-port-requirements) en [uitgaande Poortvereisten](cache-how-to-premium-vnet.md#outbound-port-requirements)), Hallo cache niet kunnen toorestart is.
- Nadat de cache-knooppunten Hallo opnieuw hebt opgestart (zoals gerapporteerd door de status van de cache in Azure-portal Hallo Hallo), kunt u Hallo volgende tests uitvoeren:
  - Hallo cache-eindpunt (met behulp van poort 6380) vanaf een machine die zich binnen Hallo pingen hetzelfde VNET als Hallo cache, met behulp van [tcping](https://www.elifulkerson.com/projects/tcping.php). Bijvoorbeeld:
    
    `tcping.exe contosocache.redis.cache.windows.net 6380`
    
    Als hello `tcping` tool meldt dat Hallo-poort is geopend, Hallo-cache is beschikbaar voor de verbinding van clients in Hallo VNET.

  - Tootest van een andere manier is een test-cacheclient toocreate (die mogelijk een eenvoudige consoletoepassing met StackExchange.Redis) die verbinding maakt toohello cache en toegevoegd enkele items uit de cache Hallo opgehaald. Installeer Hallo voorbeeld clienttoepassing op een virtuele machine die zich in hetzelfde VNET als Hallo cache Hallo en voer dit tooverify connectiviteit toohello cache.


### <a name="can-i-use-vnets-with-a-standard-or-basic-cache"></a>Kan ik VNets met een standaard of basic-cache gebruiken?
VNets kan alleen worden gebruikt met premium-caches.

### <a name="why-does-creating-a-redis-cache-fail-in-some-subnets-but-not-others"></a>Waarom een Redis-cache niet in sommige subnetten maar geen andere?
Als u een Azure Redis-Cache tooa Resource Manager VNet implementeert, moet Hallo cache zich in een speciale subnet op dat er is geen resourcetype bevat. Als wordt geprobeerd toodeploy wordt een Azure Redis-Cache tooa Resource Manager VNet subnet met andere resources, het Hallo-implementatie mislukt. Voordat u een nieuwe Redis-cache kunt maken, moet u bestaande resources binnen het subnet Hallo Hallo verwijderen.

U kunt meerdere typen implementeren van resources tooa klassieke VNet, zolang er voldoende IP-adressen beschikbaar.

### <a name="what-are-hello-subnet-address-space-requirements"></a>Wat zijn Hallo subnet adresvereisten?
Azure bepaalde IP-adressen binnen elk subnet gereserveerd en deze adressen kunnen niet worden gebruikt. Hallo zijn eerste en laatste IP-adressen van Hallo subnetten gereserveerd voor protocol overeenstemming, samen met drie meer adressen voor Azure-services gebruikt. Zie voor meer informatie [zijn er beperkingen voor het gebruik van IP-adressen binnen deze subnetten?](../virtual-network/virtual-networks-faq.md#are-there-any-restrictions-on-using-ip-addresses-within-these-subnets)

Bij toevoeging toohello IP-adressen die worden gebruikt door hello Azure VNET infrastructuur, elke Redis-exemplaar in Hallo subnet gebruikt twee IP-adressen per shard en één extra IP-adres voor Hallo load balancer. Een niet-geclusterde cache wordt beschouwd als een shard toohave.

### <a name="do-all-cache-features-work-when-hosting-a-cache-in-a-vnet"></a>Werk alle functies van de cache bij het hosten van een cache in een VNET?
Als uw cache deel van een VNET uitmaakt, toegang alleen clients in VNET Hallo Hallo-cache. Als gevolg hiervan werken hello volgende cache functies niet op dit moment.

* Console redis - omdat Redis-Console wordt uitgevoerd in uw lokale browser, die zich buiten de Hallo VNET, het tooyour cache kan geen verbinding kunt maken.

## <a name="use-expressroute-with-azure-redis-cache"></a>ExpressRoute gebruiken met Azure Redis-Cache
Klanten kunnen verbinding maken met een [Azure ExpressRoute](https://azure.microsoft.com/services/expressroute/) circuit tootheir virtuele netwerkinfrastructuur, waardoor hun lokale netwerk tooAzure uitbreiden. 

Standaard een nieuwe ExpressRoute-circuit voert geen geforceerde tunneling (aankondiging van een standaardroute 0.0.0.0/0) op een VNET. Als gevolg hiervan uitgaande internetverbinding is toegestaan rechtstreeks vanuit Hallo VNET en clienttoepassingen kunnen tooconnect tooother Azure zijn eindpunten, met inbegrip van Azure Redis-Cache.

Een algemene configuratie van de klant is echter toouse geforceerde tunneling (adverteren een standaardroute) waardoor uitgaande Internet verkeer tooinstead stroom lokale. Dit netwerkverkeer wordt verbroken verbinding met Azure Redis-Cache als uitgaand verkeer Hallo vervolgens lokale geblokkeerd zodat hello Azure Redis-Cache-exemplaar niet kunnen toocommunicate met de bijbehorende afhankelijkheden is.

Hallo-oplossing is toodefine een (of meer) gebruiker gedefinieerde routes (udr's) op Hallo subnet met hello Azure Redis-Cache. Een UDR definieert subnet-specifieke routes die in plaats van de standaardroute Hallo gehonoreerd.

Indien mogelijk, wordt aangeraden toouse Hallo volgende configuratie:

* Hallo ExpressRoute configuratie kondigt 0.0.0.0/0 en standaard force alle uitgaande verkeer lokale tunnels.
* Hallo UDR toegepast toohello subnet hello Azure Redis-Cache met definieert 0.0.0.0/0 met een werkende route voor TCP/IP-verkeer toohello openbare internet. bijvoorbeeld door het instellen van Hallo van volgende hop type too'Internet'.

Hallo is gecombineerde effect van deze stappen dat Hallo subnetniveau UDR voorrang hebben op Hallo ExpressRoute geforceerde tunneling, zodat uitgaande toegang tot Internet vanaf hello Azure Redis-Cache.

Maken van verbinding tooan Azure Redis-Cache-exemplaar van een on-premises toepassing met behulp van ExpressRoute is niet een typische gebruiksscenario vanwege redenen tooperformance (clients moeten voor de beste prestaties Azure Redis-Cache in Hallo dezelfde regio bevinden als hello Azure Redis-Cache).

>[!IMPORTANT] 
>Hallo routes die zijn gedefinieerd in een UDR **moet** worden specifiek genoeg tootake voorrang boven alle routes die worden geadverteerd door Hallo ExpressRoute configuratie. Hallo volgende voorbeeld wordt Hallo brede 0.0.0.0/0-adresbereik, en als zodanig kan mogelijk worden per ongeluk genegeerd door route-advertisements met behulp van specifieke adresbereiken.

>[!WARNING]  
>Azure Redis-Cache wordt niet ondersteund met ExpressRoute-configuraties die **onjuist cross-adverteert routes van Hallo pad toohello persoonlijke peering pad voor openbare peering**. ExpressRoute-configuraties waarvoor openbare peering is geconfigureerd, ontvangt de route-advertisements van Microsoft voor een groot aantal Microsoft Azure-IP-adresbereiken. Als deze adresbereiken onjuist cross aangekondigd op Hallo-pad voor persoonlijke peering, is Hallo resultaat dat alle uitgaande pakketten van subnet hello Azure Redis-Cache van het exemplaar van de klant ten onrechte force via een tunnel tooa on-premises netwerk infrastructuur. Deze stroom van het netwerk verbreekt Azure Redis-Cache. Hallo oplossing toothis probleem is toostop cross-adverteert routes van Hallo pad toohello persoonlijke peering pad voor openbare peering.


Achtergrondinformatie over de gebruiker gedefinieerde routes zijn beschikbaar in deze [overzicht](../virtual-network/virtual-networks-udr-overview.md).

Zie voor meer informatie over ExpressRoute [technisch overzicht van ExpressRoute](../expressroute/expressroute-introduction.md).

## <a name="next-steps"></a>Volgende stappen
Meer informatie over hoe meer premium toouse functies in de cache.

* [Inleiding toohello Azure Redis-Cache Premium-laag](cache-premium-tier-intro.md)

<!-- IMAGES -->

[redis-cache-vnet]: ./media/cache-how-to-premium-vnet/redis-cache-vnet.png

[redis-cache-vnet-ip]: ./media/cache-how-to-premium-vnet/redis-cache-vnet-ip.png

[redis-cache-vnet-info]: ./media/cache-how-to-premium-vnet/redis-cache-vnet-info.png

