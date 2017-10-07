---
title: Virtueel netwerk (VNet) aaaAzure Planning and Design Guide | Microsoft Docs
description: Meer informatie over hoe tooplan en ontwerp van virtuele netwerken in Azure op basis van uw vereisten isolatie, connectiviteit en locatie.
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 3a4a9aea-7608-4d2e-bb3c-40de2e537200
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/08/2016
ms.author: jdial
ms.openlocfilehash: f3ffadf8cf254f64b1f86b44f90315d2bc679f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="plan-and-design-azure-virtual-networks"></a>Plannen en ontwerpen van virtuele netwerken van Azure
Het maken van een VNet tooexperiment met is eenvoudig genoeg, maar de kans op zijn, implementeert u meerdere VNets via tijd toosupport Hallo productie behoeften van uw organisatie. Met een bepaalde planning en ontwerp, wordt u kunnen toodeploy VNets en Hallo resources u effectiever moet verbinden. Als u niet bekend bent met Vnetten, verdient het aanbeveling die u [meer informatie over VNets](virtual-networks-overview.md) en [hoe toodeploy](virtual-networks-create-vnet-arm-pportal.md) een voordat u doorgaat.

## <a name="plan"></a>Plannen
Een goed begrip van de Azure-abonnementen, regio's en resources van netwerk is essentieel voor succes. U kunt Hallo lijst met overwegingen hieronder als uitgangspunt gebruiken. Zodra u deze overwegingen begrijpt, kunt u Hallo vereisten voor uw netwerkontwerp definiëren.

### <a name="considerations"></a>Overwegingen
Voordat het Hallo planning van de onderstaande vragen beantwoorden, moet u de volgende Hallo:

* Alles wat die u in Azure maakt bestaat uit een of meer resources. Een virtuele machine (VM) is een resource, Hallo adapter netwerkinterface (NIC) die wordt gebruikt door een virtuele machine is een resource, Hallo openbaar IP-adres gebruikt door een NIC is een resource, Hallo VNet Hallo NIC is verbonden toois een resource.
* Maken van resources in een [Azure-regio](https://azure.microsoft.com/regions/#services) en -abonnement. Resources kunnen alleen worden verbonden tooa virtueel netwerk dat bestaat in Hallo dezelfde regio en abonnement Hallo-bron is in.
* U kunt andere virtuele netwerken tooeach verbinding maken met behulp van:
    * **[Virtueel netwerk peering](virtual-network-peering-overview.md)**: Hallo virtuele netwerken moeten aanwezig zijn in Hallo dezelfde Azure-regio. Bandbreedte tussen resources in virtuele netwerken brengen is Hallo dezelfde alsof Hallo resources verbonden toohello hetzelfde virtuele netwerk.
    * **Een Azure [VPN-Gateway](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)**: Hallo virtuele netwerken kunnen bestaan in Hallo dezelfde zijn, of andere Azure-regio's. Bandbreedte tussen resources in virtuele netwerken die zijn verbonden via een VPN-Gateway wordt beperkt door de bandbreedte Hallo Hallo VPN-Gateway.
* VNets tooyour on-premises netwerk verbinding kunnen maken met behulp van een Hallo [connectiviteitsopties](../vpn-gateway/vpn-gateway-about-vpngateways.md#s2smulti) beschikbaar in Azure.
* Verschillende bronnen kunnen worden gegroepeerd [resourcegroepen](../azure-resource-manager/resource-group-overview.md#resource-groups), waardoor het gemakkelijker toomanage Hallo resource als eenheid. Een resourcegroep kan resources uit meerdere regio's, bevatten, zolang Hallo resources toohello behoren hetzelfde abonnement.

### <a name="define-requirements"></a>Vereisten definiëren
Hallo vragen hieronder als uitgangspunt gebruiken voor het ontwerp van uw Azure-netwerk.    

1. Wat Azure locaties wordt u toohost VNets gebruiken?
2. Moet u tooprovide communicatie tussen deze Azure locaties?
3. Moet u tooprovide communicatie tussen uw Azure-VNet(s) en uw lokale clientresources?
4. Hoeveel infrastructuur als een Service (IaaS) virtuele machines, cloud services-rollen en web-apps wilt die u voor uw oplossing nodig?
5. Moet u tooisolate-verkeer op basis van groepen met VM's (dat wil zeggen front-end-webservers en back-end-databaseservers)?
6. Moet u toocontrol netwerkverkeer met behulp van virtuele apparaten?
7. Gebruikers moeten verschillende sets machtigingen toodifferent Azure-resources doen?

### <a name="understand-vnet-and-subnet-properties"></a>VNet en de subneteigenschappen begrijpen
VNet en subnetten resources helpen definiëren een beveiligingsgrens voor werkbelastingen in Azure. Een VNet wordt gekenmerkt door een verzameling van adresruimten, gedefinieerd als CIDR-blokken.

> [!NOTE]
> Netwerkbeheerders bent bekend met CIDR-notatie. Als u niet bekend met CIDR bent, [meer informatie over het](http://whatismyipaddress.com/cidr).
>
>

VNets bevatten hello volgende eigenschappen.

| Eigenschap | Beschrijving | Beperkingen |
| --- | --- | --- |
| **naam** |VNet-naam |Tekenreeks van too80 tekens. Kan bevatten letters, cijfers, onderstrepingstekens, punten of afbreekstreepjes. Moet beginnen met een letter of cijfer. Moet eindigen op een letter, cijfer of onderstrepingsteken. Kan bevat hoofdletter of kleine letters bestaan. |
| **location** |Azure-locatie (ook waarnaar wordt verwezen tooas regio). |Moet een Hallo geldige Azure-locaties. |
| **de addressSpace** |Verzameling van adresvoorvoegsels die gezamenlijk Hallo VNet in CIDR-notatie. |Moet een matrix van geldig CIDR-adresblokken, met inbegrip van openbare IP-adresbereiken. |
| **subnetten** |Verzameling van subnetten die gezamenlijk Hallo VNet |Zie de onderstaande Hallo subnet eigenschappen-tabel. |
| **dhcpOptions** |Object met een enkele vereiste eigenschap met de naam **dnsServers**. | |
| **dnsServers** |Matrix van DNS-servers die worden gebruikt door Hallo VNet. Als er geen server is opgegeven, wordt Azure interne naamomzetting gebruikt. |Moet een matrix van u too10 DNS-servers IP-adres. |

Een subnet is een onderliggende resource van een VNet en helpt bij het segmenten van adresruimten binnen een CIDR-blok met behulp van IP-adresvoorvoegsels definiëren. NIC's kunnen worden toegevoegd, toosubnets en verbonden tooVMs, tegelijk connectiviteit biedt voor verschillende werkbelastingen.

Subnetten bevatten Hallo volgende eigenschappen.

| Eigenschap | Beschrijving | Beperkingen |
| --- | --- | --- |
| **naam** |Subnetnaam |Tekenreeks van too80 tekens. Kan bevatten letters, cijfers, onderstrepingstekens, punten of afbreekstreepjes. Moet beginnen met een letter of cijfer. Moet eindigen op een letter, cijfer of onderstrepingsteken. Kan bevat hoofdletter of kleine letters bestaan. |
| **location** |Azure-locatie (ook waarnaar wordt verwezen tooas regio). |Moet een Hallo geldige Azure-locaties. |
| **addressPrefix** |Één adresvoorvoegsel die Hallo subnet in CIDR-notatie |Moet een enkel CIDR-blok die deel uitmaakt van een van de adresruimten van Hallo VNet. |
| **networkSecurityGroup** |NSG die is toegepast toohello subnet | |
| **Migratiestatus** |Routetabel toegepast toohello subnet | |
| **ipConfigurations** |Verzameling van IP-configuratie-objecten die worden gebruikt door de NIC's aangesloten toohello subnet | |

### <a name="name-resolution"></a>Naamomzetting
Uw VNet gebruikt standaard [Azure verschafte naamomzetting](virtual-networks-name-resolution-for-vms-and-role-instances.md) tooresolve namen binnen Hallo VNet en op Hallo openbare Internet. Als u uw datacenters VNets tooyour lokale verbinding, moet u echter tooprovide [uw eigen DNS-server](virtual-networks-name-resolution-for-vms-and-role-instances.md) tooresolve namen tussen uw netwerken.  

### <a name="limits"></a>Limieten
Bekijk Hallo netwerken limieten in Hallo [Azure beperkt](../azure-subscription-service-limits.md#networking-limits) artikel tooensure die uw ontwerp niet met een van de Hallo limieten conflicteert. Sommige limieten kunnen worden verhoogd door een ondersteuningsticket te openen.

### <a name="role-based-access-control-rbac"></a>RBAC (op rollen gebaseerd toegangsbeheer)
U kunt [Azure RBAC](../active-directory/role-based-access-built-in-roles.md) toocontrol Hallo niveau van de verschillende gebruikers toegang hebben toodifferent resources in Azure. Op die manier scheiden Hallo-werk dat door uw team op basis van hun behoeften.

Wat virtuele netwerken zijn betrokken gebruikers in Hallo **Network Contributor** rol hebben volledige controle over virtuele Azure Resource Manager-netwerkbronnen. Op deze manier voor gebruikers in Hallo **klassieke Network Contributor** rol hebben volledig beheer over de resources van klassieke virtuele netwerk.

> [!NOTE]
> U kunt ook [uw eigen rollen maken](../active-directory/role-based-access-control-configure.md) tooseparate de behoeften van uw administratieve.
>
>

## <a name="design"></a>Ontwerpen
Zodra u Hallo-antwoorden toohello vragen in Hallo weet [plannen](#Plan) sectie, lees de volgende Hallo voordat u uw vnet's definieert.

### <a name="number-of-subscriptions-and-vnets"></a>Het aantal abonnementen en VNets
U moet rekening houden met het maken van meerdere VNets in Hallo volgen scenario's:

* **Virtuele machines die in verschillende Azure locaties geplaatst toobe moeten**. VNets in Azure zijn regionaal. Ze niet meerdere locaties kunnen omvatten. Daarom moet u ten minste één VNet voor elke gewenste toohost virtuele machines in Azure-locatie.
* **Werklasten die volledig zijn geïsoleerd van elkaar toobe moeten**. U kunt afzonderlijke VNets, die Hallo zelfs gebruik hetzelfde IP-adresruimtes, tooisolate verschillende werkbelastingen van elkaar maken.

Houd er rekening mee dat Hallo limieten bovenstaande per regio per abonnement zijn. Dit betekent dat kunt u meerdere abonnementen tooincrease Hallo limiet van resources die u in Azure kunt onderhouden. U kunt een site-naar-site-VPN en een ExpressRoute-circuit tooconnect VNets uit verschillende abonnementen.

### <a name="subscription-and-vnet-design-patterns"></a>Abonnement en de ontwerppatronen VNet
Hallo in de volgende tabel bevat enkele veelvoorkomende ontwerppatronen voor abonnementen en VNets.

| Scenario | Diagram | Professionals | Nadelen |
| --- | --- | --- | --- |
| Abonnement van één, twee VNets per app |![Één abonnement](./media/virtual-network-vnet-plan-design-arm/figure1.png) |Slechts één abonnement toomanage. |Maximum aantal VNets per Azure-regio. Daarna moet u meer abonnementen. Bekijk Hallo [Azure beperkt](../azure-subscription-service-limits.md#networking-limits) artikel voor meer informatie. |
| Met één abonnement per app, twee VNets per app |![Één abonnement](./media/virtual-network-vnet-plan-design-arm/figure2.png) |Maakt gebruik van slechts twee VNets per abonnement. |Moeilijker toomanage wanneer er te veel apps. |
| Met één abonnement per bedrijfseenheid, twee VNets per app. |![Één abonnement](./media/virtual-network-vnet-plan-design-arm/figure3.png) |Verhouding tussen aantal abonnementen en VNets. |Maximum aantal VNets per bedrijfseenheid (abonnement). Bekijk Hallo [Azure beperkt](../azure-subscription-service-limits.md#networking-limits) artikel voor meer informatie. |
| Met één abonnement per bedrijfseenheid, twee VNets per groep van toepassingen. |![Één abonnement](./media/virtual-network-vnet-plan-design-arm/figure4.png) |Verhouding tussen aantal abonnementen en VNets. |Apps moeten worden geïsoleerd met behulp van subnetten en nsg's. |

### <a name="number-of-subnets"></a>Aantal subnetten
U moet rekening houden met meerdere subnetten in een VNet in Hallo volgen scenario's:

* **Er is onvoldoende privé IP-adressen voor alle NIC's in een subnet**. Als uw subnetadresruimte niet voldoende IP-adressen voor Hallo aantal NIC's in Hallo subnet bevat, moet u toocreate meerdere subnetten. Houd er rekening mee dat Azure reserveert 5 privé IP-adressen van elk subnet dat kan niet worden gebruikt: Hallo het eerste en laatste adressen van de adresruimte hello (voor Hallo subnetadres en multicast) en 3 adressen toobe intern (voor DHCP en DNS-doeleinden) gebruikt.
* **Beveiliging**. U kunt subnetten tooseparate groepen met VM's van elkaar gebruiken voor werkbelastingen met een gelaagde structuur, en van toepassing op andere [netwerkbeveiligingsgroepen (nsg's)](virtual-networks-nsg.md#subnets) voor deze subnetten.
* **Hybride verbindingen**. U kunt VPN-gateways en een ExpressRoute-circuits te gebruiken[verbinding](../vpn-gateway/vpn-gateway-about-vpngateways.md#s2smulti) uw tooone VNets een andere, en tooyour on-premises gegevens center(s). VPN-gateways en een ExpressRoute-circuits vereist een subnet van hun eigen toobe gemaakt.
* **Virtuele apparaten**. U kunt een virtueel apparaat, zoals een firewall, WAN-accelerator of VPN-gateway gebruiken in een Azure VNet. Wanneer u doet dit, moet u deze te[verkeer routeren](virtual-networks-udr-overview.md) toothose toestellen en ze te isoleren in hun eigen subnet.

### <a name="subnet-and-nsg-design-patterns"></a>Subnet en ontwerppatronen voor NSG
Hallo in de volgende tabel bevat enkele veelvoorkomende ontwerppatronen voor het gebruik van subnetten.

| Scenario | Diagram | Professionals | Nadelen |
| --- | --- | --- | --- |
| Nsg's per toepassingslaag per app met één subnet |![Één subnet](./media/virtual-network-vnet-plan-design-arm/figure5.png) |Slechts één subnet toomanage. |Meerdere nsg's nodig tooisolate elke toepassing. |
| Eén subnet per nsg's per toepassingslaag-app |![Subnet per app](./media/virtual-network-vnet-plan-design-arm/figure6.png) |Minder toomanage nsg's. |Meerdere subnetten toomanage. |
| Eén subnet per toepassingslaag, nsg's per app. |![Subnet per laag](./media/virtual-network-vnet-plan-design-arm/figure7.png) |Verhouding tussen aantal subnetten en nsg's. |Maximum aantal nsg's per abonnement. Bekijk Hallo [Azure beperkt](../azure-subscription-service-limits.md#networking-limits) artikel voor meer informatie. |
| Eén subnet per toepassingslaag per app, nsg's per subnet |![Subnet per laag per app](./media/virtual-network-vnet-plan-design-arm/figure8.png) |Mogelijk kleiner aantal nsg's. |Meerdere subnetten toomanage. |

## <a name="sample-design"></a>Voorbeeld-ontwerp
tooillustrate hello toepassing hello informatie in dit artikel Overweeg Hallo scenario te volgen.

U werkt voor een bedrijf met 2 datacenters in Noord-Amerika en twee datacenters Europa. U hebt vastgesteld 6 verschillende toepassingen klantgerichte onderhouden door 2 verschillende bedrijfseenheden die u wilt dat toomigrate tooAzure als een test. Hallo-basisarchitectuur voor Hallo toepassingen zijn als volgt:

* App1, App2 App3 en App4 zijn op Linux-servers Ubuntu gehoste webtoepassingen. Elke toepassing verbindt tooa afzonderlijke toepassingsserver die als host fungeert van de RESTful-services op Linux-servers. Hallo RESTful-services verbinding tooa back-end MySQL-database.
* App5 en App6 zijn webtoepassingen die worden gehost op Windows-servers met Windows Server 2012 R2. Elke toepassing verbinding tooa back-end van SQL Server-database.
* Alle apps worden momenteel gehost op een van het bedrijf Hallo datacenters in Noord-Amerika.
* Hallo lokale datacenters gebruik Hallo 10.0.0.0/8-adresruimte.

U moet toodesign een virtueel netwerk-oplossing die voldoet aan Hallo volgens de vereisten:

* Elk bedrijfsonderdeel moet niet worden beïnvloed door het brongebruik van andere bedrijfseenheden.
* Hallo hoeveelheid vnet's en subnetten toomake van eenvoudiger beheer te beperken.
* Elk bedrijfsonderdeel moet een enkel test-/ ontwikkelingsfase gebruikt voor alle toepassingen VNet hebben.
* Elke toepassing wordt gehost in 2 verschillende Azure-datacenters per continent (Noord-Amerika en Europa).
* Elke toepassing is volledig geïsoleerd van elkaar.
* Elke toepassing kan worden geopend door klanten via Hallo Internet met behulp van HTTP.
* Elke toepassing toegankelijk zijn voor gebruikers verbonden toohello lokale datacenters met behulp van een versleutelde-tunnel.
* Verbinding tooon-premises datacenters moeten bestaande VPN-apparaten gebruiken.
* Hallo van bedrijf netwerken groep moet hebben volledig beheer over Hallo VNet-configuratie.
* Ontwikkelaars in elk bedrijfsonderdeel moet alleen kunnen toodeploy VMs tooexisting subnetten.
* Alle toepassingen worden gemigreerd omdat deze tooAzure (lift-en-shift).
* Hallo-databases in elke vestiging moeten tooother Azure repliceren locaties eenmaal per dag.
* Elke toepassing gebruik 5 front-end-webservers, 2 toepassingsservers (indien nodig) en 2-databaseservers.

### <a name="plan"></a>Plannen
U moet beginnen met uw ontwerp plannen door het beantwoorden van vraag in Hallo Hallo [vereisten definiëren](#Define-requirements) sectie zoals hieronder wordt weergegeven.

1. Wat Azure locaties wordt u toohost VNets gebruiken?

    2 locaties in Noord-Amerika en Europa 2 locaties. U moet kiezen die zijn gebaseerd op Hallo fysieke locatie van uw bestaande lokale datacenters. Op die manier heeft de verbinding van uw fysieke locaties tooAzure een betere latentie.
2. Moet u tooprovide communicatie tussen deze Azure locaties?

    Ja. Aangezien het Hallo-databases moet gerepliceerde tooall locaties.
3. Moet u tooprovide communicatie tussen uw Azure-VNet(s) en uw lokale gegevens center(s)?

    Ja. Omdat gebruikers verbonden moet toohello lokale datacenters kunnen tooaccess Hallo toepassingen via een versleutelde-tunnel.
4. Hoeveel IaaS VM's moet u voor uw oplossing?

    200 IaaS VM's. App1, App2 App3 en App4 vereisen 5 webservers elke 2 toepassingsservers elke en 2-databaseservers elke. Dit is een totaal van 9 IaaS VM's per toepassing of 36 IaaS VM's. App5 en App6 moet 5 webservers en 2-databaseservers. Dit is een totaal van 7 IaaS VM's per toepassing of 14 IaaS VM's. Daarom moet u 50 IaaS VM's voor alle toepassingen in elke Azure-regio. Omdat we toouse 4 regio's moeten, zijn er 200 IaaS VM's.

    U moet ook tooprovide DNS-servers in elke VNet of in de naam van uw lokale gegevens centers tooresolve tussen uw Azure IaaS VM's en uw on-premises netwerk.
5. Moet u tooisolate-verkeer op basis van groepen met VM's (dat wil zeggen front-end-webservers en back-end-databaseservers)?

    Ja. Elke toepassing moet volledig geïsoleerd van elkaar en elke toepassingslaag moet ook worden geïsoleerd.
6. Moet u toocontrol netwerkverkeer met behulp van virtuele apparaten?

    Nee. Virtuele apparaten kunnen worden gebruikt tooprovide meer controle over het netwerkverkeer, met inbegrip van meer gedetailleerde logboekregistratie voor het vlak van gegevens.
7. Gebruikers moeten verschillende sets machtigingen toodifferent Azure-resources doen?

    Ja. Hallo netwerken team moet volledig beheer over Hallo virtuele netwerkinstellingen, terwijl ontwikkelaars kunnen toodeploy alleen moet hun virtuele machines toopre bestaande subnetten.

### <a name="design"></a>Ontwerpen
U moet volgen Hallo ontwerp abonnementen, VNets, subnetten en nsg's opgeven. Nsg's hier worden besproken, maar u moet weten over [nsg's](virtual-networks-nsg.md) voordat u uw ontwerp voltooit.

**Het aantal abonnementen en VNets**

Hallo volgens de vereisten zijn gerelateerde toosubscriptions en VNets:

* Elk bedrijfsonderdeel moet niet worden beïnvloed door het brongebruik van andere bedrijfseenheden.
* Hallo hoeveelheid vnet's en subnetten te beperken.
* Elk bedrijfsonderdeel moet een enkel test-/ ontwikkelingsfase gebruikt voor alle toepassingen VNet hebben.
* Elke toepassing wordt gehost in 2 verschillende Azure-datacenters per continent (Noord-Amerika en Europa).

Op basis van deze vereisten, moet u een abonnement voor elk bedrijfsonderdeel. Op die manier verbruik van bronnen van een zakelijke eenheid niet meetelt limieten voor andere bedrijfseenheden. En omdat u wilt dat toominimize Hallo aantal vnet's, moet u overwegen Hallo **met één abonnement per bedrijfseenheid, twee VNets per groep van toepassingen** patroon zoals hieronder wordt weergegeven.

![Één abonnement](./media/virtual-network-vnet-plan-design-arm/figure9.png)

U moet ook toospecify Hallo-adresruimte voor elk VNet. Omdat u moet connectiviteit tussen Hallo on-premises datacenters en hello Azure-regio's, Hallo-adresruimte die is gebruikt voor Azure VNets kan niet conflicteren met Hallo on-premises netwerk, en Hallo-adresruimte die wordt gebruikt door elk VNet moet niet conflicteren met andere bestaande vnet's. U kunt deze vereisten Hallo-adresruimten in onderstaande toosatisfy Hallo-tabel.  

| **Abonnement** | **VNet** | **Azure-regio** | **Adresruimte** |
| --- | --- | --- | --- |
| BU1 |ProdBU1US1 |VS - west |172.16.0.0/16 |
| BU1 |ProdBU1US2 |VS - oost |172.17.0.0/16 |
| BU1 |ProdBU1EU1 |Noord-Europa |172.18.0.0/16 |
| BU1 |ProdBU1EU2 |West-Europa |172.19.0.0/16 |
| BU1 |TestDevBU1 |VS - west |172.20.0.0/16 |
| BU2 |TestDevBU2 |VS - west |172.21.0.0/16 |
| BU2 |ProdBU2US1 |VS - west |172.22.0.0/16 |
| BU2 |ProdBU2US2 |VS - oost |172.23.0.0/16 |
| BU2 |ProdBU2EU1 |Noord-Europa |172.24.0.0/16 |
| BU2 |ProdBU2EU2 |West-Europa |172.25.0.0/16 |

**Aantal subnetten en nsg 's**

Hallo volgens de vereisten zijn gerelateerde toosubnets en nsg's:

* Hallo hoeveelheid vnet's en subnetten te beperken.
* Elke toepassing is volledig geïsoleerd van elkaar.
* Elke toepassing kan worden geopend door klanten via Hallo Internet met behulp van HTTP.
* Elke toepassing toegankelijk zijn voor gebruikers verbonden toohello lokale datacenters met behulp van een versleutelde-tunnel.
* Verbinding tooon-premises datacenters moeten bestaande VPN-apparaten gebruiken.
* Hallo-databases in elke vestiging moeten tooother Azure repliceren locaties eenmaal per dag.

Op basis van deze vereisten, kan u één subnet per toepassingslaag gebruiken, en nsg's toofilter verkeer per toepassing. Op die manier hoeft u slechts 3 subnetten in elke VNet (front-end, toepassingslaag en gegevenslaag) en één NSG per toepassing per subnet. In dit geval moet u overwegen Hallo **één subnet per toepassingslaag, nsg's per app** ontwerppatroon. Hallo afbeelding hieronder ziet u Hallo gebruik van Hallo ontwerppatroon dat vertegenwoordigt Hallo **ProdBU1US1** VNet.

![Eén subnet per laag, één NSG per toepassing per laag](./media/virtual-network-vnet-plan-design-arm/figure11.png)

Echter, moet u ook een extra subnet toocreate voor Hallo VPN-verbinding tussen VNets hello en uw lokale datacenters. En u toospecify Hallo-adresruimte moet voor elk subnet. Hallo afbeelding hieronder ziet u een Voorbeeldoplossing voor **ProdBU1US1** VNet. U kunt dit scenario wilt repliceren voor elk VNet. Elke kleur vertegenwoordigt een andere toepassing.

![Voorbeeld VNet](./media/virtual-network-vnet-plan-design-arm/figure10.png)

**Toegangsbeheer**

Hallo volgende vereisten zijn verwante tooaccess besturingselement:

* Hallo van bedrijf netwerken groep moet hebben volledig beheer over Hallo VNet-configuratie.
* Ontwikkelaars in elk bedrijfsonderdeel moet alleen kunnen toodeploy VMs tooexisting subnetten.

Op basis van deze vereisten, kunt u gebruikers kunnen toevoegen van Hallo networking-team toohello ingebouwde **Network Contributor** rol in elk abonnement; en maak een aangepaste beveiligingsrol voor Hallo toepassingsontwikkelaars in elk abonnement geeft Deze rechten tooadd VMs tooexisting subnetten.

## <a name="next-steps"></a>Volgende stappen
* [Implementeren van een virtueel netwerk](virtual-networks-create-vnet-arm-template-click.md) op basis van een scenario.
* Begrijpen hoe te[verdelen](../load-balancer/load-balancer-overview.md) IaaS VM's en [beheren van routering via meerdere Azure-regio's](../traffic-manager/traffic-manager-overview.md).
* Meer informatie over [nsg's en hoe tooplan en ontwerp](virtual-networks-nsg.md) een NSG-oplossing.
* Meer informatie over uw [cross-premises en VNet-connectiviteitsopties](../vpn-gateway/vpn-gateway-about-vpngateways.md#s2smulti).
