---
title: aaaIP adrestypen in Azure | Microsoft Docs
description: "Meer informatie over openbare en privé-IP-adressen in Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-resource-manager
ms.assetid: 610b911c-f358-4cfe-ad82-8b61b87c3b7e
ms.service: virtual-network
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.openlocfilehash: 402d3707c00f0b3bf3ef1febd5ade66223da74bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="ip-address-types-and-allocation-methods-in-azure"></a>IP-adrestypen en toewijzingsmethoden in Azure
U kunt toewijzen van IP-adressen tooAzure resources toocommunicate met andere Azure-resources, uw on-premises netwerk en Internet Hallo. Er zijn twee typen IP-adressen die u in Azure kunt gebruiken:

* **Openbare IP-adressen**: gebruikt voor communicatie met de Hallo Internet, met inbegrip van openbare Azure-services
* **Privé IP-adressen**: gebruikt voor communicatie binnen een Azure-netwerk (VNet) en uw on-premises netwerk wanneer u een VPN-gateway of ExpressRoute-circuit tooextend de tooAzure van uw netwerk.

> [!NOTE]
> Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../resource-manager-deployment-model.md).  In dit artikel wordt beschreven hoe u Hallo Resource Manager-implementatiemodel, die Microsoft voor de meeste nieuwe implementaties in plaats van Hallo aanbeveelt [klassieke implementatiemodel](virtual-network-ip-addresses-overview-classic.md).
> 

Als u bekend met het klassieke implementatiemodel hello bent, controleert u Hallo [verschillen in de IP-adressen tussen het klassieke en het Resource Manager](virtual-network-ip-addresses-overview-classic.md#differences-between-resource-manager-and-classic-deployments).

## <a name="public-ip-addresses"></a>Openbare IP-adressen
Openbare IP-adressen toestaan toocommunicate met Internet en Azure services voor openbare Azure-resources, zoals [Azure Redis-Cache](https://azure.microsoft.com/services/cache/), [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/), [SQL-databases](../sql-database/sql-database-technical-overview.md), en [Azure storage](../storage/common/storage-introduction.md).

In Azure Resource Manager is een [openbaar IP](resource-groups-networking.md#public-ip-address)-adres een resource die zijn eigen eigenschappen heeft. U kunt een openbare IP-adres resource koppelen aan een Hallo resources te volgen:

* Virtuele machines (VM's)
* Internetgerichte load balancers
* VPN-gateways
* Toepassingsgateways

### <a name="allocation-method"></a>Toewijzingsmethode
Er zijn twee manieren waarop een IP-adres is toegewezen tooa *openbare* IP-resource - *dynamische* of *statische*. Hallo standaard toewijzingsmethode *dynamische*, waarbij een IP-adres **niet** toegewezen op Hallo-tijd van het maken ervan. Hallo openbaar IP-adres wordt in plaats daarvan toegewezen wanneer u start (of maak) die zijn gekoppeld Hallo resource (zoals een virtuele machine of een load balancer). Hallo IP-adres wordt uitgebracht, wanneer u stoppen (of verwijderen) Hallo resource. Hierdoor Hallo IP-adres toochange wanneer u stoppen en starten van een resource.

tooensure hello IP-adres voor hello gekoppelde bron blijft Hallo dezelfde, kunt u instellen Hallo toewijzingsmethode expliciet te*statische*. In dat geval wordt er onmiddellijk een IP-adres toegewezen. Ze zijn vrijgegeven wanneer u Hallo bron verwijderen of te wijzigen van de toewijzingsmethode*dynamische*.

> [!NOTE]
> Zelfs als u instelt Hallo toewijzingsmethode te*statische*, u kunt geen Hallo werkelijke IP-adres toegewezen toohello opgeven *openbare IP-resource*. In plaats daarvan het toegewezen opgehaald uit een groep met beschikbare IP-adressen in Azure-locatie Hallo Hallo resource is gemaakt in.
>

Statische openbare IP-adressen worden vaak gebruikt in Hallo volgen scenario's:

* Eindgebruikers moeten tooupdate firewall-regels toocommunicate met uw Azure-resources.
* U gebruikt een DNS-naamomzetting waarbij een wijziging in het IP-adres het bijwerken van A-records vereist.
* Uw Azure-resources communiceren met andere apps of services die een op IP-adressen gebaseerd beveiligingsmodel gebruiken.
* U SSL-certificaten gekoppelde tooan IP-adres gebruiken.

> [!NOTE]
> Hallo-lijst met IP-adresbereiken waarvan openbare IP-adressen (dynamische/statisch) tooAzure resources worden toegewezen wordt gepubliceerd op [Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).
>

### <a name="dns-hostname-resolution"></a>DNS-hostnaamomzetting
U kunt opgeven dat een DNS-domeinnaamlabel voor een openbaar IP-resource, maakt u een toewijzing voor *domainnamelabel*. *locatie*. cloudapp.azure.com toohello openbaar IP-adres in hello Azure beheerde DNS-servers. Bijvoorbeeld, als u een openbaar IP-resource met maakt **contoso** als een *domainnamelabel* in Hallo **VS-West** Azure *locatie*, Hallo FQDN-naam (Fully qualified domain name) **contoso.westus.cloudapp.azure.com** toohello openbaar IP-adres van bron hello wordt opgelost. Een aangepast domein-CNAME-record verwijst toohello openbaar IP-adres in Azure, kunt u deze toocreate FQDN-naam gebruiken.

> [!IMPORTANT]
> Elk domeinnaamlabel dat wordt gemaakt, moet uniek zijn binnen de Azure-locatie.  
>

### <a name="virtual-machines"></a>Virtuele machines
U kunt koppelen een openbaar IP-adres met een [Windows](../virtual-machines/windows/overview.md) of [Linux](../virtual-machines/virtual-machines-linux-about.md) VM toewijzen tooits **netwerkinterface**. In geval van een virtuele machine met meerdere netwerkinterfaces Hallo kunt u deze toewijzen toohello *primaire* alleen netwerkinterface. U kunt een dynamisch of een statische openbare IP-adres tooa VM toewijzen.

### <a name="internet-facing-load-balancers"></a>Internetgerichte load balancers
Koppelt u een openbaar IP-adres met een [Azure Load Balancer](../load-balancer/load-balancer-overview.md), door toe te wijzen toohello netwerktaakverdeler **frontend** configuratie. Dit openbare IP-adres doet dienst als een virtueel IP-adres (VIP) met taakverdeling. U kunt een dynamische of statische openbare IP-adres tooa taakverdeler front-toewijzen. U kunt ook meerdere openbare IP-adressen tooa load balancer front-end, waardoor toewijzen [meerdere VIP's](../load-balancer/load-balancer-multivip.md) scenario's, zoals een omgeving met meerdere tenants met websites op basis van SSL.

### <a name="vpn-gateways"></a>VPN-gateways
[Azure VPN-Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md) gebruikte tooconnect is een Azure-netwerk (VNet) tooother Azure VNets of tooan on-premises netwerk. U moet een openbare IP-adres tooits tooassign **IP-configuratie** tooenable het toocommunicate met Hallo extern netwerk. Op dit moment kunt u alleen toewijzen een *dynamische* openbare IP-adres tooa VPN-gateway.

### <a name="application-gateways"></a>Toepassingsgateways
U kunt een openbare IP-adres koppelen aan een Azure [Application Gateway](../application-gateway/application-gateway-introduction.md), door toe te kennen van de gateway toohello **frontend** configuratie. Dit openbare IP-adres doet dienst als een VIP met taakverdeling. Op dit moment kunt u alleen toewijzen een *dynamische* openbare IP-adres tooan toepassingsgateway frontend configuratie.

### <a name="at-a-glance"></a>In een oogopslag
Hallo in de volgende tabel ziet u Hallo specifieke eigenschap waarmee een openbaar IP-adres kan worden gekoppeld tooa op het hoogste niveau resource en Hallo mogelijke toewijzingsmethoden (dynamisch of statisch) die kunnen worden gebruikt.

| Resource op het hoogste niveau | IP-adreskoppeling | Dynamisch | Statisch |
| --- | --- | --- | --- |
| Virtuele machine |Netwerkinterface |Ja |Ja |
| Load balancer |Front-end-configuratie |Ja |Ja |
| VPN-gateway |Gateway-IP-configuratie |Ja |Nee |
| Toepassingsgateway |Front-end-configuratie |Ja |Nee |

## <a name="private-ip-addresses"></a>Privé-IP-adressen
Privé IP-adressen toestaan toocommunicate Azure-resources met andere resources in een [virtueel netwerk](virtual-networks-overview.md) of een on-premises netwerk via een VPN-gateway of ExpressRoute-circuit, zonder gebruik van een Internet-bereikbaar IP-adres.

Hello Azure Resource Manager-implementatiemodel is een particulier IP-adres gekoppeld toohello soorten Azure-resources te volgen:

* VM's
* Interne load balancers (ILB's)
* Toepassingsgateways

### <a name="allocation-method"></a>Toewijzingsmethode
Een persoonlijke IP-adres wordt toegewezen uit Hallo adres bereik van Hallo subnet toowhich Hallo bron is gekoppeld. Hallo-adresbereik van Hallo-subnet zelf is een onderdeel van het Hallo-VNet-adresbereik.

Er zijn twee methoden voor het toewijzen van een privé-IP-adres: *dynamisch* en *statisch*. Hallo standaard toewijzingsmethode *dynamische*, waarbij Hallo IP-adres automatisch wordt toegewezen uit van de bron van het Hallo-subnet (met behulp van DHCP). Dit IP-adres kunt wijzigen wanneer u stoppen en Hallo resource starten.

U kunt de toewijzingsmethode hello te instellen*statische* tooensure Hallo IP-adres blijft Hallo dezelfde. In dit geval moet u ook een geldig IP-adres die deel uitmaakt van het subnet van de bron van de Hallo tooprovide.

Statische privé-IP-adressen worden vaak gebruikt voor:

* Virtuele machines die fungeren als domeincontrollers of DNS-servers.
* Resources die firewallregels gebruiken die zijn gebaseerd op IP-adressen.
* Resources die worden gebruikt door andere apps/resources via een IP-adres.

### <a name="virtual-machines"></a>Virtuele machines
Een persoonlijke IP-adres is toegewezen toohello **netwerkinterface** van een [Windows](../virtual-machines/windows/overview.md) of [Linux](../virtual-machines/virtual-machines-linux-about.md) VM. In geval van een VM met een multi-netwerkinterface, wordt aan elke interface een privé-IP-adres toegewezen. U kunt de toewijzingsmethode Hallo opgeven als dynamische of statische voor een netwerkinterface.

#### <a name="internal-dns-hostname-resolution-for-vms"></a>Interne DNS-hostnaamomzetting (voor VM's)
Alle Azure-VM's zijn standaard geconfigureerd met door [Azure beheerde DNS-servers](virtual-networks-name-resolution-for-vms-and-role-instances.md#azure-provided-name-resolution), tenzij u expliciet aangepaste DNS-servers configureert. Deze DNS-servers bieden interne naamomzetting voor virtuele machines die zich binnen een Hallo hetzelfde VNet.

Wanneer u een virtuele machine maakt, wordt een toewijzing voor Hallo hostnaam tooits privé IP-adres toohello Azure beheerde DNS-servers toegevoegd. In geval van een meerdere netwerkinterface VM Hallo hostnaam is toegewezen toohello privé IP-adres van de primaire netwerkinterface Hallo.

VM's zijn geconfigureerd met Azure beheerde DNS-servers worden kunnen tooresolve Hallo hostnamen van alle virtuele machines binnen hun VNet tootheir privé IP-adressen.

### <a name="internal-load-balancers-ilb--application-gateways"></a>Interne load balancers (ILB) en toepassingsgateways
U kunt een particuliere IP-adres toohello **front-end** configuratie van een [Azure interne Load Balancer](../load-balancer/load-balancer-internal-overview.md) (ILB) of een [Azure Application Gateway](../application-gateway/application-gateway-introduction.md). Deze privé IP-adres fungeert als een interne eindpunt, toegankelijk alleen toohello bronnen binnen de virtuele netwerk (VNet) en externe netwerken Hallo verbonden toohello VNet. U kunt ofwel een dynamische of statische privé IP-adres toohello front-end configuratie toewijzen.

### <a name="at-a-glance"></a>In een oogopslag
Hallo in de volgende tabel ziet u bepaalde Hallo-eigenschap waarmee een persoonlijke IP-adres kan worden gekoppeld tooa op het hoogste niveau resource en Hallo mogelijke toewijzingsmethoden (dynamisch of statisch) die kunnen worden gebruikt.

| Resource op het hoogste niveau | IP-adreskoppeling | Dynamisch | Statisch |
| --- | --- | --- | --- |
| Virtuele machine |Netwerkinterface |Ja |Ja |
| Load balancer |Front-end-configuratie |Ja |Ja |
| Toepassingsgateway |Front-end-configuratie |Ja |Ja |

## <a name="limits"></a>Limieten
Hallo worden limieten opgelegd voor het IP-adressering aangegeven in de volledige set Hallo [voor netwerken beperkt](../azure-subscription-service-limits.md#networking-limits) in Azure. Deze limieten gelden per regio en per abonnement. U kunt [contact op met ondersteuning](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooincrease Hallo standaardlimiet van bovengrenzen toohello op basis van de behoeften van uw bedrijf.

## <a name="pricing"></a>Prijzen
Openbare IP-adressen kunnen een kostprijs hebben. toolearn meer over IP-adres in Azure, bekijk Hallo prijzen [IP-adres prijzen](https://azure.microsoft.com/pricing/details/ip-addresses) pagina.

## <a name="next-steps"></a>Volgende stappen
* [Een virtuele machine met een statische openbare IP-adres met behulp van hello Azure-portal implementeren](virtual-network-deploy-static-pip-arm-portal.md)
* [Een virtuele machine met een statisch openbaar IP-adres implementeren met een sjabloon](virtual-network-deploy-static-pip-arm-template.md)
* [Een virtuele machine implementeren met een statisch privé IP-adres met hello Azure-portal](virtual-networks-static-private-ip-arm-pportal.md)
