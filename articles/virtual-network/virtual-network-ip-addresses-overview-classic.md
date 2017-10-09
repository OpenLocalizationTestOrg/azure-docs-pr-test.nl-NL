---
title: aaaIP adrestypen in Azure (klassiek) | Microsoft Docs
description: Meer informatie over openbare en particuliere IP-adressen (klassiek) in Azure.
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: 2f8664ab-2daf-43fa-bbeb-be9773efc978
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/11/2016
ms.author: jdial
ms.openlocfilehash: 7e09a5ad5b5f2d55329152b5d843de3c4455d1b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="ip-address-types-and-allocation-methods-classic-in-azure"></a>IP-adrestypen en toewijzingsmethoden Azure (klassiek)
U kunt toewijzen van IP-adressen tooAzure resources toocommunicate met andere Azure-resources, uw on-premises netwerk en Internet Hallo. Er zijn twee soorten IP-adressen kunt u in Azure: openbare en persoonlijke.

Openbare IP-adressen worden gebruikt voor communicatie met de Hallo Internet, met inbegrip van openbare Azure-services.

Privé IP-adressen worden gebruikt voor communicatie binnen een Azure-netwerk (VNet), een cloudservice en uw on-premises netwerk wanneer u een VPN-gateway of ExpressRoute-circuit tooextend de tooAzure van uw netwerk.

> [!IMPORTANT]
> Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../resource-manager-deployment-model.md).  In dit artikel wordt behandeld met het klassieke implementatiemodel Hallo. Microsoft raadt aan dat de meeste nieuwe implementaties Resource Manager gebruiken. Meer informatie over IP-adressen in het Resource Manager door Hallo lezen [IP-adressen](virtual-network-ip-addresses-overview-arm.md) artikel.

## <a name="public-ip-addresses"></a>Openbare IP-adressen
Openbare IP-adressen toestaan toocommunicate met Internet en Azure services voor openbare Azure-resources, zoals [Azure Redis-Cache](https://azure.microsoft.com/services/cache/), [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/), [SQL-databases](../sql-database/sql-database-technical-overview.md), en [Azure storage](../storage/common/storage-introduction.md).

Een openbaar IP-adres is gekoppeld aan de volgende resourcetypen Hallo:

* Cloud services
* IaaS virtuele Machines (VM's)
* PaaS-rolexemplaren
* VPN-gateways
* Toepassingsgateways

### <a name="allocation-method"></a>Toewijzingsmethode
Wanneer een openbaar IP-adres toobe tooan Azure-resource toegewezen moet, is het *dynamisch* toegewezen uit een groep met beschikbare openbare IP-adres binnen Hallo locatie Hallo resource is gemaakt. Dit IP-adres is uitgebracht als Hallo resource is gestopt. Als dit gebeurt wanneer alle Hallo rolinstanties zijn gestopt van een cloudservice, die kunnen worden voorkomen met behulp van een *statische* (gereserveerd) IP-adres (Zie [Cloudservices](#Cloud-services)).

> [!NOTE]
> Hallo-lijst met IP-adresbereiken waarvan openbare IP-adressen tooAzure resources worden toegewezen wordt gepubliceerd op [Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).
> 
> 

### <a name="dns-hostname-resolution"></a>DNS-hostnaamomzetting
Wanneer u een cloudservice of een IaaS VM maakt, moet u tooprovide een cloud service DNS-naam die uniek voor alle resources in Azure is. Hiermee maakt u een toewijzing in hello Azure beheerde DNS-servers voor *dnsname*. cloudapp.net toohello openbaar IP-adres van bron Hallo. Bijvoorbeeld, als u een cloudservice maakt met een cloud service DNS-naam van **contoso**, Hallo volledig gekwalificeerde domeinnaam (FQDN) **contoso.cloudapp.net** tooa openbare IP-adres (VIP) van de oplossing Hallo-cloudservice. Een aangepast domein-CNAME-record verwijst toohello openbaar IP-adres in Azure, kunt u deze toocreate FQDN-naam gebruiken.

### <a name="cloud-services"></a>Cloud services
Een service in de cloud heeft altijd een openbare IP-adres van waarnaar wordt verwezen tooas een virtueel IP-adres (VIP). U kunt de eindpunten in een cloud service tooassociate verschillende poorten in Hallo VIP toointernal poorten op VM's en rolexemplaren binnen Hallo-cloudservice maken. 

Een cloudservice kan meerdere IaaS VM's bevatten of alle weergegeven via PaaS-rolexemplaren Hallo dezelfde VIP voor cloud-service. U kunt ook toewijzen [meerdere VIP's tooa-cloudservice](../load-balancer/load-balancer-multivip.md), waardoor meerdere VIP's scenario's zoals multitenant-omgeving met websites op basis van SSL.

U kunt controleren of openbare IP-adres van een cloudservice Hallo blijft Hallo dezelfde zijn, zelfs wanneer alle rolinstanties Hallo gestopt, met behulp van een *statische* openbare IP-adres, waarnaar wordt verwezen tooas [gereserveerde IP-adres](virtual-networks-reserved-public-ip.md). U kunt een statisch (gereserveerd) IP-resource maken in een specifieke locatie en cloud-service op die locatie tooany toewijzen. U Hallo IP-adres kan niet opgeven voor Hallo gereserveerd IP-adres, het wordt toegewezen van groep met beschikbare IP-adressen op Hallo-locatie die wordt gemaakt. Dit IP-adres wordt niet vrijgegeven totdat u het expliciet verwijdert.

Statisch (gereserveerd) openbare IP-adressen worden vaak gebruikt in Hallo scenario's waarbij een cloudservice:

* firewall-regels toobe setup vereist door eindgebruikers.
* afhankelijk van externe DNS-naamomzetting en een dynamische IP-adres vereist updaten van A-records.
* verbruikt externe webservices die IP-gebaseerd beveiligingsmodel te gebruiken.
* maakt gebruik van SSL-certificaten gekoppelde tooan IP-adres.

> [!NOTE]
> Wanneer u een klassieke virtuele machine, een container maakt *cloudservice* wordt gemaakt door Azure, met een virtueel IP-adres (VIP). Wanneer Hallo is gemaakt via de portal, een standaard RDP of SSH *eindpunt* wordt geconfigureerd via de portal Hallo zodat toohello VM via Hallo cloud service VIP verbinding kunnen maken. Dit VIP cloud-service kan worden gereserveerd, die een gereserveerd IP-adres tooconnect-toohello VM effectief biedt. U kunt extra poorten openen door meer eindpunten configureren.
> 
> 

### <a name="iaas-vms-and-paas-role-instances"></a>IaaS VM's en PaaS-rolexemplaren
U kunt een openbare IP-adres rechtstreeks tooan IaaS [VM](../virtual-machines/virtual-machines-linux-about.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) of PaaS-rolinstantie binnen een cloudservice. Dit is bedoeld tooas een instantieniveau openbare IP-adres ([ILPIP](virtual-networks-instance-level-public-ip.md)). Dit openbare IP-adres kan alleen dynamisch zijn.

> [!NOTE]
> Dit verschilt van Hallo VIP van Hallo-cloudservice, die een container voor IaaS VM's of PaaS-rolexemplaren is, omdat een cloudservice kan bevatten meerdere IaaS VM's of PaaS-rolexemplaren, alle blootgestelde via Hallo dezelfde service VIP cloud.
> 
> 

### <a name="vpn-gateways"></a>VPN-gateways
Een [VPN-gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md) gebruikte tooconnect een Azure VNet tooother Azure VNets of on-premises netwerken kan worden. Een VPN-gateway is een openbaar IP-adres toegewezen *dynamisch*, waardoor communicatie met externe Hallo-netwerk.

### <a name="application-gateways"></a>Toepassingsgateways
Een Azure [toepassingsgateway](../application-gateway/application-gateway-introduction.md) kan worden gebruikt voor Layer7 taakverdeling tooroute netwerkverkeer op basis van HTTP. Toepassingsgateway een openbaar IP-adres is toegewezen *dynamisch*, die fungeert als Hallo VIP taakverdeling.

### <a name="at-a-glance"></a>Een overzicht
Hallo in de volgende tabel ziet u elk resourcetype met mogelijke toewijzingsmethoden hello (dynamische/statisch) en mogelijkheid tooassign meerdere openbare IP-adressen.

| Resource | Dynamisch | Statisch | Meerdere IP-adressen |
| --- | --- | --- | --- |
| Cloudservice |Ja |Ja |Ja |
| IaaS VM of PaaS rolinstantie |Ja |Nee |Nee |
| VPN-gateway |Ja |Nee |Nee |
| Toepassingsgateway |Ja |Nee |Nee |

## <a name="private-ip-addresses"></a>Privé-IP-adressen
Privé IP-adressen toocommunicate Azure-resources met andere bronnen in een cloudservice toestaan of een [virtueel netwerk](virtual-networks-overview.md)(VNet) of tooon-premises netwerk (via een VPN-gateway of ExpressRoute-circuit), zonder gebruik van een Internet-bereikbaar IP-adres.

In Azure klassieke implementatiemodel, kan toohello Azure-resources te volgen op een privé IP-adres worden toegewezen:

* IaaS VM's en PaaS-rolexemplaren
* Interne load balancer
* Toepassingsgateway

### <a name="iaas-vms-and-paas-role-instances"></a>IaaS VM's en PaaS-rolexemplaren
Virtuele machines (VM's) gemaakt met het klassieke implementatiemodel Hallo zijn altijd in een cloudservice, vergelijkbare tooPaaS rolinstanties geplaatst. Hallo-gedrag van privé IP-adressen zijn dus vergelijkbaar voor deze resources.

Het is belangrijk toonote die een cloudservice kan worden geïmplementeerd op twee manieren:

* Als een *zelfstandige* cloudservice waarin het is niet binnen een virtueel netwerk.
* Als onderdeel van een virtueel netwerk.

#### <a name="allocation-method"></a>Toewijzingsmethode
In geval van een *zelfstandige* cloudservice, een particulier IP-adres toegewezen resources-get *dynamisch* van hello Azure-datacenter persoonlijke IP-adresbereik. Het kan worden gebruikt voor communicatie met andere virtuele machines binnen Hallo dezelfde cloudservice. Dit IP-adres kunt wijzigen wanneer Hallo resource wordt gestopt en gestart.

Voor het geval van een cloudservice die is geïmplementeerd in een virtueel netwerk, bronnen persoonlijke ophalen gekoppelde IP-adressen die zijn toegewezen uit het adresbereik Hallo Hallo subnetten (zoals opgegeven in de netwerkconfiguratie). Deze persoonlijke IP-adressen kan worden gebruikt voor communicatie tussen alle virtuele machines binnen Hallo VNet.

Bovendien een particulier IP-adres is toegewezen in geval van een cloud-services binnen een VNet, *dynamisch* (met behulp van DHCP) standaard. Deze kunt wijzigen wanneer Hallo resource wordt gestopt en gestart. tooensure hello IP-adres blijft dezelfde hello, moet u tooset Hallo toewijzingsmethode te*statische*, en geef een geldig IP-adres binnen het bijbehorende adresbereik Hallo.

Statische privé-IP-adressen worden vaak gebruikt voor:

* Virtuele machines die fungeren als domeincontrollers of DNS-servers.
* Virtuele machines waarvoor firewallregels IP-adressen gebruikt.
* Virtuele machines met services die worden gebruikt door andere apps via een IP-adres.

#### <a name="internal-dns-hostname-resolution"></a>Interne DNS-hostnaamomzetting
Alle virtuele Azure-machines en PaaS-rolinstanties zijn geconfigureerd met [Azure beheerde DNS-servers](virtual-networks-name-resolution-for-vms-and-role-instances.md#azure-provided-name-resolution) standaard, tenzij u expliciet aangepaste DNS-servers configureert. Deze DNS-servers bieden interne naamomzetting voor VM's en rolexemplaren die zich bevinden in hetzelfde VNet of cloud service Hallo.

Wanneer u een virtuele machine maakt, wordt een toewijzing voor Hallo hostnaam tooits privé IP-adres toohello Azure beheerde DNS-servers toegevoegd. In geval van een VM meerdere NIC Hallo hostnaam is toegewezen toohello privé IP-adres van Hallo primaire NIC. Deze informatie over de Identiteitstoewijzing is echter beperkt tooresources binnen Hallo dezelfde cloud service of het VNet.

In geval van een *zelfstandige* cloudservice, kunt u zich kunt tooresolve hostnamen van alle VM's / rolexemplaren binnen Hallo dezelfde cloudservice alleen. U zult in geval van een cloudservice binnen een VNet hostnamen kunnen tooresolve van alle Hallo VM's / rolexemplaren binnen Hallo VNet.

### <a name="internal-load-balancers-ilb--application-gateways"></a>Interne load balancers (ILB) en toepassingsgateways
U kunt een particuliere IP-adres toohello **front-end** configuratie van een [Azure interne Load Balancer](../load-balancer/load-balancer-internal-overview.md) (ILB) of een [Azure Application Gateway](../application-gateway/application-gateway-introduction.md). Deze privé IP-adres fungeert als een interne eindpunt, toegankelijk alleen toohello bronnen binnen de virtuele netwerk (VNet) en externe netwerken Hallo verbonden toohello VNet. U kunt ofwel een dynamische of statische privé IP-adres toohello front-end configuratie toewijzen. U kunt ook meerdere persoonlijke IP-adressen tooenable meerdere VIP's scenario's toewijzen.

### <a name="at-a-glance"></a>Een overzicht
Hallo in de volgende tabel ziet u elk resourcetype met mogelijke toewijzingsmethoden hello (dynamische/statisch) en mogelijkheid tooassign meerdere particuliere IP-adressen.

| Resource | Dynamisch | Statisch | Meerdere IP-adressen |
| --- | --- | --- | --- |
| Virtuele machine (in een *zelfstandige* cloudservice) |Ja |Ja |Ja |
| De rolinstantie PaaS (in een *zelfstandige* cloudservice) |Ja |Nee |Ja |
| Virtuele machine of PaaS rolinstantie (in een VNet) |Ja |Ja |Ja |
| Interne load balancer-front-end |Ja |Ja |Ja |
| Application gateway-front-end |Ja |Ja |Ja |

## <a name="limits"></a>Limieten
Hallo in de volgende tabel toont Hallo-limieten opgelegd op IP-adressering in Azure per abonnement. U kunt [contact op met ondersteuning](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooincrease Hallo standaardlimiet van bovengrenzen toohello op basis van de behoeften van uw bedrijf.

|  | Standaardlimiet | Maximumaantal |
| --- | --- | --- |
| Openbare IP-adressen (dynamisch) |5 |contact met ondersteuning |
| Gereserveerde openbare IP-adressen |20 |contact met ondersteuning |
| Openbare VIP per implementatie (cloudservice) |5 |contact met ondersteuning |
| Persoonlijke VIP (ILB) per implementatie (cloudservice) |1 |1 |

Zorg ervoor dat u de volledige set Hallo van lezen [voor netwerken beperkt](../azure-subscription-service-limits.md#networking-limits) in Azure.

## <a name="pricing"></a>Prijzen
In de meeste gevallen zijn openbare IP-adressen beschikbaar. Er is een nominaal kosten toouse aanvullende en/of statische openbare IP-adressen. Zorg dat u begrijpt Hallo [structuur prijzen voor openbare IP-adressen](https://azure.microsoft.com/pricing/details/ip-addresses/).

## <a name="differences-between-resource-manager-and-classic-deployments"></a>Verschillen tussen Resource Manager en klassieke implementaties
Hieronder volgt een vergelijking van IP-adressering functies in het Resource Manager en het klassieke implementatiemodel Hallo.

|  | Resource | Klassiek | Resource Manager |
| --- | --- | --- | --- |
| **Openbare IP-adres** |***VM*** |Waarnaar wordt verwezen tooas een ILPIP (alleen dynamisch) |Bedoelde tooas een openbaar IP-adres (dynamische of statische) |
|  ||Toegewezen tooan IaaS VM of een exemplaar van de rol PaaS |Gekoppelde toohello van de virtuele machine-NIC | |
|  |***Internet gerichte load balancer*** |Tooas VIP (dynamische) of gereserveerd IP-adres (statische) waarnaar wordt verwezen |Bedoelde tooas een openbaar IP-adres (dynamische of statische) | |
|  ||Toegewezen tooa cloudservice |Gekoppelde toohello load balancer front-end configuratie | |
|  | | | |
| **Particulier IP-adres** |***VM*** |Waarnaar wordt verwezen tooas een DIP |Tooas een particulier IP-adres waarnaar wordt verwezen |
|  ||Toegewezen tooan IaaS VM of een exemplaar van de rol PaaS |Toegewezen toohello van de virtuele machine-NIC | |
|  |***Interne load balancer (ILB)*** |Toegewezen toohello ILB (dynamische of statische) |Toegewezen toohello ILB van front-end configuratie (dynamisch of statisch) | |

## <a name="next-steps"></a>Volgende stappen
* [Een virtuele machine met een statisch privé IP-adres implementeren](virtual-networks-static-private-ip-classic-pportal.md) met behulp van hello Azure-portal.

