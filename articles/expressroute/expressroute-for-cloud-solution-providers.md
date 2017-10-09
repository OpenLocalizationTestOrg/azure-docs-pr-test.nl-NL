---
title: aaaAzure ExpressRoute voor Cloud Solution Providers | Microsoft Docs
description: Dit artikel bevat informatie voor Cloudserviceproviders die wilt tooincorporate Azure-services en ExpressRoute in hun aanbod.
documentationcenter: na
services: expressroute
author: richcar
manager: carmonm
editor: 
ms.assetid: f6c5f8ee-40ba-41a1-ae31-67669ca419a6
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: richcar
ms.openlocfilehash: 062ecbb5e461e4384b01c4ac478cab696b7ed398
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-for-cloud-solution-providers-csp"></a>ExpressRoute voor Cloud Solution Providers (CSP)
Microsoft biedt grootschalige services waarmee traditionele leveranciers en distributeurs (CSP) toobe kunnen toorapidly inrichten van nieuwe services en oplossingen voor uw klanten zonder Hallo moeten tooinvest bij de ontwikkeling van deze nieuwe services. tooallow hello Cloud Solution Provider (CSP) Hallo mogelijkheid toodirectly beheer van deze nieuwe services, Microsoft biedt programma's en API's waarmee Hallo CSP toomanage Microsoft Azure-resources namens uw klanten. Een van deze resources is ExpressRoute. ExpressRoute kan Hallo CSP tooconnect bestaande klant resources tooAzure services. ExpressRoute is een zeer snelle persoonlijke communicatie koppeling tooservices in Azure. 

ExpresRoute bestaat uit twee circuits voor hoge beschikbaarheid die zijn aangesloten tooa één klant abonnementen en kan niet worden gedeeld door meerdere klanten. Elk circuit moet worden beëindigd in een andere router toomaintain Hallo hoge beschikbaarheid.

> [!NOTE]
> Er zijn limieten voor de bandbreedte en verbinding in ExpressRoute, wat betekent dat er bij grote/complexe implementaties meerdere ExpressRoute-circuits per klant zijn vereist.
> 
> 

Microsoft Azure biedt een toenemend aantal services dat u tooyour klanten kunt aanbieden.  toobest profiteren van deze services vereist het gebruik van Hallo ExpressRoute-verbindingen tooprovide hoge snelheid lage latentie toegang toohello Microsoft Azure-omgeving.

## <a name="microsoft-azure-management"></a>Microsoft Azure-beheer
Microsoft biedt CSP's met API's toomanage hello Azure-klantabonnementen doordat programmatische integratie met uw eigen servicebeheersystemen. U vindt de ondersteunde beheermogelijkheden [hier](https://msdn.microsoft.com/library/partnercenter/dn974944.aspx).

## <a name="microsoft-azure-resource-management"></a>Beheer van Microsoft Azure-resources
Afhankelijk van Hallo bepalen contract met uw klant hoe Hallo abonnement wordt beheerd. Hallo CSP Hallo maken direct kunt beheren en onderhouden van resources of Hallo klant kunt controle houden over Hallo Microsoft Azure-abonnement en hello Azure resources maken als ze nodig hebben. Als uw klant Hallo maken van resources in de Microsoft Azure-abonnement beheert gebruiken ze een van twee modellen: model 'Doorverbinden' of 'Leiden naar' model. Deze modellen worden beschreven in Hallo uit te voeren.  

### <a name="connect-through-model"></a>Het model 'Doorverbinden'
![alternatieve tekst](./media/expressroute-for-cloud-solution-providers/connect-through.png)  

In het model ' hello doorverbinden ' maakt Hallo CSP een rechtstreekse verbinding tussen uw datacenter en van uw klant Azure-abonnement. Hallo rechtstreekse verbinding wordt gemaakt met behulp van ExpressRoute en verbindt uw netwerk met Azure. Uw klant maakt vervolgens verbinding tooyour netwerk. Dit scenario vereist dat die klant Hallo Hallo CSP-netwerk tooaccess Azure-services passeert. 

Als uw klant andere Azure-abonnementen niet worden beheerd door Hallo u, gebruiken deze Hallo openbare Internet of een eigen privéverbinding tooconnect toothose services onder Hallo niet CSP-abonnement ingericht. 

Voor CSP Azure-services beheren, wordt ervan uitgegaan dat Hallo CSP heeft de identiteit van een eerder gemaakt opslaan die zouden worden gerepliceerd naar Azure Active Directory voor het beheer van het CSP-abonnement via aobo (Administrate). Situaties waarvoor dit scenario bevatten waarbij een partner of serviceprovider al een bestaande relatie met de klant hello, Hallo klant al gebruikmaakt van services provider momenteel of Hallo partner heeft een tooprovide desire een combinatie van de provider gehoste en Azure gehoste oplossingen tooprovide flexibiliteit en het adres van de klant uitdagingen die kunnen alleen door de CSP kunnen niet worden verwerkt. Dit model wordt weergegeven in onderstaande **afbeelding**.

![alternatieve tekst](./media/expressroute-for-cloud-solution-providers/connect-through-model.png)

### <a name="connect-toomodel"></a>Verbinding maken met toomodel
![alternatieve tekst](./media/expressroute-for-cloud-solution-providers/connect-to.png)

In Hallo Connect toomodel, Hallo serviceprovider een rechtstreekse verbinding tussen hun klant datacenter maakt en hello CSP ingerichte Azure-abonnement via ExpressRoute over Hallo klant (klant) netwerk.

> [!NOTE]
> Hallo klant zou voor ExpressRoute moet toocreate en onderhouden van Hallo ExpressRoute-circuit.  
> 
> 

In dit scenario moet dat die Hallo klant rechtstreeks verbinding maken via een klant netwerk tooaccess CSP beheerde Azure-abonnement met een rechtstreekse netwerkverbinding die is gemaakt, die eigendom zijn van en geheel of gedeeltelijk beheerd door de klant Hallo. Bij deze klanten wordt ervan uitgegaan dat Hallo-provider heeft momenteel geen archief tot stand gebracht en Hallo provider Hallo klant helpt zou bij het repliceren van het huidige identiteitsarchief in Azure Active Directory voor het beheren van hun abonnement via AOBO. Situaties waarvoor dit scenario zijn waarbij een partner of serviceprovider al een bestaande relatie met de klant hello, Hallo klant al gebruikmaakt van services provider momenteel of Hallo partner heeft een desire tooprovide-services die zijn gebaseerd uitsluitend op Azure gehoste oplossingen, zonder Hallo nodig voor de infrastructuur of een bestaand provider datacenter.

![alternatieve tekst](./media/expressroute-for-cloud-solution-providers/connect-to-model.png)

Hallo keuze tussen deze twee opties zijn op basis van de behoeften van uw klant en uw huidige moet tooprovide Azure services. details van deze modellen en Hallo Hallo op rollen gebaseerde toegangsbeheer, netwerken, die is gekoppeld en identiteit ontwerppatronen worden behandeld in de details in Hallo koppelingen te volgen:

* **RBAC (op rollen gebaseerd toegangsbeheer)**: RBAC is gebaseerd op Azure Active Directory.  Klik [hier](../active-directory/role-based-access-control-configure.md) voor meer informatie over Azure RBAC. 
* **Networking** – dekt Hallo verschillende onderwerpen van netwerken in Microsoft Azure.
* **Azure Active Directory (AAD)** : AAD biedt Hallo Identiteitsbeheer voor Microsoft Azure en 3e SaaS-toepassingen van derden. Klik [hier](https://azure.microsoft.com/documentation/services/active-directory/) voor meer informatie over Azure AD.  

## <a name="network-speeds"></a>Netwerksnelheden
ExpressRoute ondersteunt netwerksnelheden van 50 Mb/s too10Gb/s. Hierdoor kunnen klanten toopurchase Hallo hoeveelheid netwerkbandbreedte die nodig zijn voor hun specifieke omgeving.

> [!NOTE]
> Netwerkbandbreedte kan worden verhoogd naar behoefte zonder communicatie verstoren, maar tooreduce Hallo netwerksnelheid omlaag Hallo circuit wordt verbroken en opnieuw worden gemaakt met de lagere netwerksnelheid Hallo vereist.  
> 
> 

ExpressRoute ondersteunt Hallo verbindingen van meerdere vNets tooa één ExpressRoute-circuit voor beter gebruik van verbindingen met hogere snelheid Hallo. Een enkel ExpressRoute-circuit kan worden gedeeld met meerdere Azure-abonnementen die eigendom zijn van Hallo dezelfde klant.

## <a name="configuring-expressroute"></a>ExpressRoute configureren
ExpressRoute kan worden geconfigureerd toosupport drie typen verkeer ([Routeringsdomeinen](#ExpressRoute-routing-domains)) via een enkel ExpressRoute-circuit. Dit verkeer is onderverdeeld in Microsoft-peering, openbare Azure-peering en privépeering. U kunt ervoor kiezen een of alle soorten verkeer toobe verzonden via een enkel ExpressRoute-circuit of meerdere ExpressRoute-circuits, afhankelijk van de grootte Hallo Hallo ExpressRoute-circuit en isolatie door uw klant vereiste gebruiken. Hallo beveiligingsstatus van uw klant mogelijk niet is toegestaan openbaar verkeer en particuliere verkeer tootraverse via hetzelfde circuit Hallo.

### <a name="connect-through-model"></a>Het model 'Doorverbinden'
In een Hallo doorverbinden configuratie kunt u zich verantwoordelijk voor alle Hallo networking fundering tooconnect uw klanten datacenter resources toohello abonnementen worden gehost in Azure. Elk van de klant gewenste toouse mogelijkheden van Azure wordt hun eigen ExpressRoute-verbinding, die worden beheerd door moet Hallo u. Hallo gebruikt u Hallo dezelfde methoden Hallo klant zou gebruiken tooprocure hello ExpressRoute-circuit. Hallo u volgt dezelfde stappen die worden beschreven in artikel Hallo Hallo [ExpressRoute-werkstromen](expressroute-workflows.md) voor circuitinrichting en circuitstatussen. Hallo die vervolgens configureert u Hallo Border Gateway Protocol (BGP) routes toocontrol Hallo verkeer tussen Hallo on-premises netwerk en Azure vNet.

### <a name="connect-toomodel"></a>Verbinding maken met toomodel
Connect-tooconfiguration uw klant al heeft een bestaande verbinding tooAzure of initieert een verbinding toohello internetprovider ExpressRoute koppelen vanuit uw datacenter van de klant rechtstreeks tooAzure, in plaats van uw datacenter. toobegin hello inrichtingsproces, uw klant wordt stappen Hallo zoals hierboven wordt beschreven in Hallo doorverbinden model. Zodra het Hallo-circuit tot stand is gebracht, moet uw klant tooconfigure Hallo lokale routers toobe kunnen tooaccess uw netwerk- en Azure vNets.

U kunt helpen bij het Hallo-verbinding instellen en configureren Hallo tooallow Hallo resources van routes in uw toocommunicate clientresources Hallo client bronnen in uw datacenter of met Hallo-middelen gehost in Azure.

## <a name="expressroute-routing-domains"></a>ExpressRoute-routeringsdomeinen
ExpressRoute biedt drie routeringsdomeinen: openbare peering, privépeering en Microsoft-peering. Elk van de Routeringsdomeinen Hallo zijn geconfigureerd met identieke routers in actief / actief-configuratie voor hoge beschikbaarheid. Klik [hier](expressroute-circuit-peerings.md) voor meer informatie over de ExpressRoute-routeringsdomeinen.

U kunt aangepaste routes filters tooallow alleen Hallo route (s) of wilt u tooallow moet definiëren. Voor meer informatie of toosee hoe toomake deze wijzigingen zien artikel: [maken en wijzigen van routering voor een ExpressRoute-circuit met PowerShell](expressroute-howto-routing-classic.md) voor meer informatie over routeringsfilters.

> [!NOTE]
> Voor Microsoft- en openbare Peering connectiviteit moet echter een openbare IP-adres is het eigendom van Hallo klant of CSP en tooall gedefinieerd regels moet voldoen. Zie voor meer informatie, Hallo [vereisten voor ExpressRoute](expressroute-prerequisites.md) pagina.  
> 
> 

## <a name="routing"></a>Routering
ExpressRoute maakt verbinding toohello Azure netwerken via hello Azure virtuele netwerkgateway. Netwerkgateways bieden routering voor virtuele netwerken in Azure.

Maken van Azure Virtual Networks, maakt ook een standaardrouteringstabel voor Hallo vNet toodirect verkeer van Hallo subnetten van Hallo vNet. Als Hallo standaardroutetabel onvoldoende voor Hallo oplossing aangepaste is routes tooroute uitgaande verkeer toocustom apparaten kunnen worden gemaakt of tooblock routeert toospecific subnetten of externe netwerken.

### <a name="default-routing"></a>Standaardroutering
Hallo-standaardroutetabel bevat Hallo routes te volgen:

* Routering binnen een subnet
* Subnet-naar-subnet binnen het virtuele netwerk Hallo
* toohello Internet
* Virtueel netwerk-naar-virtueel netwerk via VPN-gateway
* Virtueel netwerk-naar-on-premises netwerk via een VPN- of ExpressRoute-gateway

![alternatieve tekst](./media/expressroute-for-cloud-solution-providers/default-routing.png)  

### <a name="user-defined-routing-udr"></a>Door de gebruiker gedefinieerde routering
Gebruiker gedefinieerde routes geven Hallo-besturingselement van het verkeer uitgaand van Hallo toegewezen subnet tooother subnetten in het virtuele netwerk Hallo of via een van de andere vooraf gedefinieerde gateways (ExpressRoute; internet of VPN) Hallo. Hallo standaardrouteringstabel kan worden vervangen door een door de gebruiker gedefinieerde routeringstabel die Hallo standaardrouteringstabel vervangen door aangepaste routes. Met de gebruiker gedefinieerde routering kunnen klanten specifieke routes tooappliances zoals firewalls of inbraakdetectieapparaten maken of blokkeren toegang toospecific subnetten van die als host fungeert voor de gebruiker gedefinieerde route Hallo Hallo-subnet. Klik [hier](../virtual-network/virtual-networks-udr-overview.md) voor een overzicht van door de gebruiker gedefinieerde routes. 

## <a name="security"></a>Beveiliging
Afhankelijk van welk model in gebruik en doorverbinden Connect tooor is uw klant Hallo beveiligingsbeleid definieert in het vNet of biedt Hallo beleid beveiligingsvereisten toohello CSP toodefine tootheir vNets. Hallo volgende beveiligingscriteria kan worden gedefinieerd:

1. **Klantisolatie** : hello Azure-platform biedt klantisolatie door de klant-ID en vNet-gegevens opslaan in een beveiligde database, gebruikte tooencapsulate verkeer van elke klant in een GRE-tunnel.
2. **Netwerkbeveiligingsgroep (NSG) netwerk** regels zijn voor het definiëren van verkeer toegestaan naar en van Hallo subnetten binnen vNets in Azure. Standaard bevatten Hallo NSG blok regels tooblock verkeer van Hallo Internet toohello vNet en regels voor toestaan voor verkeer binnen een vNet. Klik [hier](https://azure.microsoft.com/blog/network-security-groups/) voor meer informatie over netwerkbeveiligingsgroepen.
3. **Geforceerde tunneling** : dit is een optie tooredirect internet gebonden verkeer vanuit Azure toobe via Hallo ExpressRoute-verbinding toohello premises datacentrum. Klik [hier](expressroute-routing.md#advertising-default-routes) voor meer informatie over geforceerde tunneling.  
4. **Versleuteling** : hoewel Hallo ExpressRoute-circuits toegewezen tooa specifieke klant zijn, is er Hallo mogelijkheid dat Hallo netwerkprovider wordt geschonden, waardoor een indringer het pakketverkeer tooexamine. dit potentieel, een klant of CSP-verkeer via kunt versleutelen tooaddress Hallo verbinding met het beleid voor IPSec-tunnelmodus voor al het verkeer tussen Hallo op lokale bronnen en Azure-resources (Raadpleeg toohello optionele tunnelmodus IPSec voor klant 1 definiëren in afbeelding 5: ExpressRoute-beveiliging hierboven). de tweede optie Hallo zijn toouse een firewallapparaat op elk eindpunt Hallo Hallo ExpressRoute-circuit. Hiervoor moet extra 3e partij firewall VM's / toestellen toobe geïnstalleerd op beide uiteinden tooencrypt Hallo-verkeer via Hallo ExpressRoute-circuit.

![alternatieve tekst](./media/expressroute-for-cloud-solution-providers/expressroute-security.png)  

## <a name="next-steps"></a>Volgende stappen
Hallo Cloud Solution Provider-service biedt een manier tooincrease uw klanten waarde tooyour zonder Hallo voor dure infrastructuur en capaciteit aankopen, daarbij uw positie als Hallo primaire uitbesteding provider nodig. Naadloze integratie met Microsoft Azure kunt u doen via Hallo CSP-API, zodat u toointegrate beheer van Microsoft Azure binnen uw bestaande beheerframeworks.  

Als u meer informatie vindt u op Hallo koppelingen te volgen:

[Microsoft Cloud Solution Provider-programma](https://partner.microsoft.com/en-US/Solutions/cloud-reseller-overview).  
[Ophalen van gereed tootransact als een Cloud Solution Provider](https://partner.microsoft.com/en-us/solutions/cloud-reseller-pre-launch).  
[Microsoft Cloud Solution Provider-resources](https://partner.microsoft.com/en-us/solutions/cloud-reseller-resources).

