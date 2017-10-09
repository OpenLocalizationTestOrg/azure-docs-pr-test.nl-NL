---
title: aaaNetwork beveiligingsgroepen in Azure | Microsoft Docs
description: Meer informatie over hoe tooisolate verkeer binnen uw virtuele netwerken die gebruikmaken van Hallo gedistribueerde firewall in Azure met behulp van Netwerkbeveiligingsgroepen stromen.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 20e850fc-6456-4b5f-9a3f-a8379b052bc9
ms.service: virtual-network
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/11/2016
ms.author: jdial
ms.openlocfilehash: 3528ce833dab17977327c3c9ae0e78316e5e6a05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="filter-network-traffic-with-network-security-groups"></a>Netwerkverkeer filteren met netwerkbeveiligingsgroepen

Een netwerkbeveiligingsgroep (NSG) bevat een lijst met regels voor toestaan of weigeren netwerkverkeer tooresources verbonden tooAzure virtuele netwerken (VNet). Nsg's kunnen worden gekoppeld toosubnets, afzonderlijke virtuele machines (klassiek) of afzonderlijke netwerkinterfaces (NIC) tooVMs (Resource Manager) zijn gekoppeld. Wanneer een NSG gekoppeld tooa subnet is, Hallo regels van toepassing tooall bronnen verbonden toohello subnet. Verkeer kan verder worden beperkt door het ook een NSG tooa VM of NIC koppelen

> [!NOTE]
> Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../resource-manager-deployment-model.md). In dit artikel komen beide modellen, maar Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.

## <a name="nsg-resource"></a>NSG-resource
Nsg's bevatten Hallo volgende eigenschappen:

| Eigenschap | Beschrijving | Beperkingen | Overwegingen |
| --- | --- | --- | --- |
| Naam |Naam voor Hallo NSG |Moet uniek zijn binnen Hallo regio.<br/>Kan letters, cijfers, onderstrepingstekens, punten en afbreekstreepjes bevatten.<br/>Moet beginnen met een letter of cijfer.<br/>Moet eindigen op een letter, cijfer of onderstrepingsteken.<br/>Mag niet meer dan 80 tekens bevatten. |Omdat u toocreate verschillende nsg's moeten mogelijk, zorg er dan voor dat u beschikt over een naamgevingsconventie die het gemakkelijk tooidentify Hallo-functie van uw nsg's maakt. |
| Regio |Azure [regio](https://azure.microsoft.com/regions) waar hello NSG wordt gemaakt. |Nsg's kunnen alleen worden gekoppeld tooresources binnen Hallo dezelfde regio bevinden als Hallo NSG. |Hallo toolearn over hoeveel nsg's die u kunt opnemen per regio, lezen [Azure beperkt](../azure-subscription-service-limits.md#virtual-networking-limits-classic) artikel.|
| Resourcegroep |Hallo [resourcegroep](../azure-resource-manager/resource-group-overview.md#resource-groups) hello NSG bestaat in. |Hoewel een NSG in een resourcegroep bestaat, gekoppelde tooresources in elke willekeurige resourcegroep kan zijn, zolang het Hallo-resource maakt deel uit van Hallo dezelfde Azure-regio als Hallo NSG. |Resourcegroepen zijn gebruikte toomanage meerdere resources samen als een implementatie-eenheid.<br/>U kunt overwegen voor groepering Hallo NSG met resources die deze is gekoppeld. |
| Regels |Regels voor binnenkomend of uitgaand verkeer die bepalen welk verkeer wordt toegestaan of geweigerd. | |Zie Hallo [NSG-regels](#Nsg-rules) sectie van dit artikel. |

> [!NOTE]
> ACL's voor eindpunten en netwerkbeveiliging groepen worden niet ondersteund op Hallo hetzelfde VM-exemplaar. Als u wilt dat een NSG toouse en beschikken over een ACL voor eindpunten al, moet u eerst Hallo ACL voor eindpunten verwijderen. hoe een ACL tooremove Lees toolearn hello [beheren toegangsbeheerlijsten (ACL's) voor eindpunten met behulp van PowerShell](virtual-networks-acl-powershell.md) artikel.
> 

### <a name="nsg-rules"></a>NSG-regels
NSG-regels bevatten Hallo volgende eigenschappen:

| Eigenschap | Beschrijving | Beperkingen | Overwegingen |
| --- | --- | --- | --- |
| **Naam** |Naam voor het Hallo-regel. |Moet uniek zijn binnen Hallo regio.<br/>Kan letters, cijfers, onderstrepingstekens, punten en afbreekstreepjes bevatten.<br/>Moet beginnen met een letter of cijfer.<br/>Moet eindigen op een letter, cijfer of onderstrepingsteken.<br/>Mag niet meer dan 80 tekens bevatten. |U kunt meerdere regels binnen een NSG hebben, dus zorg ervoor dat u de volgende naamgevingsregels waarmee u tooidentify Hallo-functie van de regel. |
| **Protocol** |Protocol toomatch voor Hallo regel. |TCP, UDP of * |Gebruik * als een protocol omvat dit zowel ICMP (alleen Oost-West-verkeer), als goed als UDP en TCP en kan het aantal regels u moet Hallo kleiner.<br/>AT Hallo dezelfde gebruik * mogelijk specifiek genoeg, dus het wordt aanbevolen dat u * alleen indien nodig. |
| **Bronpoortbereik** |Bron poort bereik toomatch voor Hallo regel. |Poortnummer tussen 1 too65535, poortbereik (voorbeeld: 1-65535), of * (voor alle poorten). |Bronpoorten kunnen kortstondig zijn. Tenzij in uw clientprogramma een specifieke poort wordt gebruikt, gebruikt u in de meeste gevallen *.<br/>Probeer toouse poortbereiken zoveel mogelijk tooavoid Hallo voor meerdere regels nodig.<br/>Meerdere poorten of poortbereiken kunnen niet worden gegroepeerd met komma's. |
| **Doelpoortbereik** |Bestemming poort bereik toomatch voor Hallo regel. |Poortnummer tussen 1 too65535, poortbereik (voorbeeld: 1-65535), of \* (voor alle poorten). |Probeer toouse poortbereiken zoveel mogelijk tooavoid Hallo voor meerdere regels nodig.<br/>Meerdere poorten of poortbereiken kunnen niet worden gegroepeerd met komma's. |
| **Bronadresvoorvoegsel** |Bron adres voorvoegsel of tag toomatch voor Hallo regel. |Eén IP-adres (bijvoorbeeld 10.10.10.10), een IP-subnet (bijvoorbeeld 192.168.1.0/24), een [standaardtag](#default-tags) of * (voor alle adressen). |Overweeg het gebruik van bereiken, standaardtags en * tooreduce Hallo aantal regels. |
| **Doeladresvoorvoegsel** |Bestemming adres voorvoegsel of tag toomatch voor Hallo regel. | Eén IP-adres (bijvoorbeeld 10.10.10.10), een IP-subnet (bijvoorbeeld 192.168.1.0/24), een [standaardtag](#default-tags) of * (voor alle adressen). |Overweeg het gebruik van bereiken, standaardtags en * tooreduce Hallo aantal regels. |
| **Richting** |Richting van verkeer toomatch voor Hallo regel. |Binnenkomend of uitgaand. |Regels voor binnenkomend en uitgaand verkeer worden afzonderlijk verwerkt op basis van de richting. |
| **Prioriteit** |Regels worden gecontroleerd in volgorde van prioriteit Hallo. Zodra een regel van toepassing is, worden geen andere regels meer getest. | Getal tussen 100 en 4096. | Houd rekening met het maken van regels verspringen met 100 voor elke regel tooleave ruimte voor nieuwe regels die u in Hallo toekomstige mogelijk maken. |
| **Toegang** |Type toegang tooapply of Hallo regel van toepassing is. | Toestaan of weigeren. | Houd er rekening mee dat als een regel voor toestaan, niet voor een pakket gevonden is, Hallo pakket genegeerd. |

NSG's bevatten twee sets met regels: een voor binnenkomend verkeer en een voor uitgaand verkeer. Hallo-prioriteit voor een regel moet uniek zijn binnen elke set. 

![Verwerking van NSG-regels](./media/virtual-network-nsg-overview/figure3.png) 

Hallo vorige afbeelding ziet u hoe NSG-regels worden verwerkt.

### <a name="default-tags"></a>Standaardtags
Standaardtags zijn systeem-id's tooaddress een categorie IP-adressen. U kunt standaardtags gebruiken in Hallo **bronadresvoorvoegsel** en **doeladresvoorvoegsel** eigenschappen van een regel. Er zijn drie standaardtags die u kunt gebruiken:

* **VirtualNetwork** (Resource Manager) (**VIRTUAL_NETWORK** voor klassieke): dit label bevat adresruimte Hallo virtuele netwerk (CIDR-bereiken gedefinieerd in Azure), alle verbonden lokale adresruimten en verbonden Azure VNets (lokale netwerken).
* **AzureLoadBalancer** (Resource Manager) (**AZURE_LOADBALANCER** voor klassiek): met deze tag wordt de load balancer voor de infrastructuur van Azure aangeduid. Hallo-tag vertaalt tooan Azure datacenter IP waar Azure statuscontroles afkomstig zijn.
* **Internet** (Resource Manager) (**INTERNET** voor klassieke): deze tag geeft Hallo IP-adresruimte die buiten het virtuele netwerk Hallo en bereikbaar is via het openbare Internet. Hallo bereik bevat Hallo [Azure openbare IP-adresruimten](https://www.microsoft.com/download/details.aspx?id=41653).

### <a name="default-rules"></a>Standaardregels
Alle NSG's bevatten een set met standaardregels. Hallo-standaardregels kunnen niet worden verwijderd, maar omdat ze de laagste prioriteit Hallo zijn toegewezen, kunnen ze worden overschreven door het Hallo-regels die u maakt. 

Hallo-standaardregels toestaan en weigeren verkeer als volgt:
- **Virtueel netwerk:** Verkeer dat afkomstig is van en eindigt in een virtueel netwerk wordt toegestaan in zowel binnenkomende als uitgaande richting.
- **Internet:** Uitgaand verkeer is toegestaan, maar binnenkomend verkeer wordt geblokkeerd.
- **De load balancer:** toestaan Azure load balancer tooprobe Hallo status van uw VM's en rolinstanties. Als u geen set met taakverdeling gebruikt, kunt u deze regel onderdrukken.

**Standaardregels voor binnenkomend verkeer**

| Name | Prioriteit | Bron-IP | Bronpoort | Doel-IP | Doelpoort | Protocol | Access |
| --- | --- | --- | --- | --- | --- | --- | --- |
| AllowVNetInBound |65000 | VirtualNetwork | * | VirtualNetwork | * | * | Toestaan |
| AllowAzureLoadBalancerInBound | 65001 | AzureLoadBalancer | * | * | * | * | Toestaan |
| DenyAllInBound |65500 | * | * | * | * | * | Weigeren |

**Standaardregels voor uitgaand verkeer**

| Naam | Prioriteit | Bron-IP | Bronpoort | Doel-IP | Doelpoort | Protocol | Access |
| --- | --- | --- | --- | --- | --- | --- | --- |
| AllowVnetOutBound | 65000 | VirtualNetwork | * | VirtualNetwork | * | * | Toestaan |
| AllowInternetOutBound | 65001 | * | * | Internet | * | * | Toestaan |
| DenyAllOutBound | 65500 | * | * | * | * | * | Weigeren |

## <a name="associating-nsgs"></a>NSG's koppelen
U kunt een NSG tooVMs NIC's en subnetten, afhankelijk van het Hallo-implementatiemodel die u, als volgt gebruikt koppelen:

* **Virtuele machine (alleen klassiek):** beveiligingsregels worden toegepast tooall verkeer naar/van Hallo VM. 
* **NIC (alleen voor Resource Manager):** beveiligingsregels worden toegepast tooall verkeer naar/van Hallo NIC Hallo NSG is gekoppeld. In een VM meerdere NIC's kunt u verschillende toepassen (of dezelfde Hallo) NSG tooeach NIC afzonderlijk. 
* **Subnet (Resource Manager en classic):** beveiligingsregels worden toegepast tooany verkeer naar/van alle resources verbonden toohello VNet.

U kunt verschillende nsg's tooa VM (of NIC, afhankelijk van het implementatiemodel Hallo) koppelen en die een NIC of VM is verbonden met subnet Hallo. Beveiligingsregels voor verkeer van de toegepaste toohello, door de prioriteit in elke NSG, in Hallo volgt volgorde:

- **Binnenkomend verkeer**

  1. **NSG die is toegepast toosubnet:** als een subnet NSG een overeenkomende regel toodeny verkeer heeft, Hallo pakket genegeerd.

  2. **NSG toegepast tooNIC** (Resource Manager) of VM (klassiek): als VM\NIC NSG heeft een vergelijkingsregel die verkeer weigert, pakketten wegvallen op Hallo VM\NIC, zelfs als een subnet NSG heeft een vergelijkingsregel waarmee verkeer.

- **Uitgaand verkeer**

  1. **NSG toegepast tooNIC** (Resource Manager) of VM (klassiek): als een NSG VM\NIC een vergelijkingsregel die verkeer weigert heeft, pakketten verloren gaan.

  2. **NSG die is toegepast toosubnet:** als een subnet NSG een vergelijkingsregel die verkeer weigert heeft, pakketten wegvallen, zelfs als een NSG VM\NIC heeft een vergelijkingsregel waarmee verkeer.

> [!NOTE]
> Hoewel u kunt alleen een enkele tooa subnet, VM of NIC; in NSG koppelen u kunt koppelen dezelfde NSG tooas Hallo veel resources als u wilt.
>

## <a name="implementation"></a>Implementatie
U kunt nsg's implementeren in Hallo Resource Manager of de klassieke implementatiemodellen Hallo volgende hulpprogramma's gebruiken:

| Implementatieprogramma | Klassiek | Resource Manager |
| --- | --- | --- |
| Azure Portal   | Ja | [Ja](virtual-networks-create-nsg-arm-pportal.md) |
| PowerShell     | [Ja](virtual-networks-create-nsg-classic-ps.md) | [Ja](virtual-networks-create-nsg-arm-ps.md) |
| Azure CLI **V1**   | [Ja](virtual-networks-create-nsg-classic-cli.md) | [Ja](virtual-networks-create-nsg-cli-nodejs.md) |
| Azure CLI **V2**   | Nee | [Ja](virtual-networks-create-nsg-arm-cli.md) |
| Azure Resource Manager-sjabloon   | Nee  | [Ja](virtual-networks-create-nsg-arm-template.md) |

## <a name="planning"></a>Planning
Voordat u nsg's implementeert, moet u tooanswer Hallo vragen te volgen:

1. Welke typen resources wilt u toofilter verkeer tooor uit? U kunt resources zoals NIC's (Resource Manager), VM’s (klassiek), Cloud Services, omgevingen met toepassingsservices en VM- schaalsets verbinden. 
2. Hallo-bronnen die u wilt dat toofilter verkeer van verbonden toosubnets in bestaande vnet's zijn?

Lees voor meer informatie over het plannen van netwerkbeveiliging in Azure Hallo [Cloudservices en netwerkbeveiliging](../best-practices-network-security.md) artikel. 

## <a name="design-considerations"></a>Overwegingen bij het ontwerpen
Zodra u Hallo-antwoorden toohello vragen in Hallo weet [Planning](#Planning) sectie, bekijkt hello uit te voeren voordat u uw nsg's definieert:

### <a name="limits"></a>Limieten
Er zijn limieten toohello aantal nsg's die u kunt een abonnement hebben en het aantal regels per NSG. meer informatie over het Hallo-limieten, Hallo lezen toolearn [Azure beperkt](../azure-subscription-service-limits.md#networking-limits) artikel.

### <a name="vnet-and-subnet-design"></a>VNET's en subnetten ontwerpen
Omdat nsg's kunnen toegepaste toosubnets, kunt u Hallo aantal nsg's minimaliseren door uw resources groeperen per subnet, en het nsg's toosubnets toepassen.  Als u tooapply nsg's toosubnets besluit, merkt u dat bestaande vnet's en subnetten zijn niet gedefinieerd met nsg's in gedachten. U kunt moet de nieuwe vnet's en subnetten toosupport toodefine uw NSG-ontwerp en de nieuwe subnetten van nieuwe resources tooyour implementeren. U kunt vervolgens een migratie strategie toomove bestaande resources toohello nieuwe subnetten definiëren. 

### <a name="special-rules"></a>Speciale regels
Als u verkeer toegestaan door Hallo volgens de regels voor blokkeert, moet uw infrastructuur kan niet communiceren met essentiële Azure-services:

* **Virtuele IP-adres van het hostknooppunt Hallo:** basisinfrastructuur services, zoals DHCP, DNS en statuscontrole worden geleverd via het gevirtualiseerde host Hallo IP-adres 168.63.129.16. Dit openbare IP-adres behoort tooMicrosoft en Hallo enige gevirtualiseerde IP-adres is in alle regio's gebruikt voor dit doel. Dit IP-adres toegewezen toohello fysieke IP-adres van Hallo servermachine (hostknooppunt) die als host fungeert voor Hallo VM. Hallo hostknooppunt fungeert als Hallo DHCP relay, recursieve van Hallo-DNS-omzetter en bron voor Hallo Hallo en voor de load balancer-test voor health Hallo machine health test. Communicatie toothis IP-adres is niet een aanval.
* **Licentieverlening (Key Management Service):** voor alle Windows installatiekopieën die op de VM’s machines worden uitgevoerd, is een licentie vereist. tooensure-licentieverlening, een aanvraag verzonden toohello Key Management Service-hostservers dat dergelijke query's te verwerken. Hallo-aanvraag wordt gedaan uitgaande via poort 1688.

### <a name="icmp-traffic"></a>ICMP-verkeer
de huidige NSG-regels Hallo kunnen alleen voor protocollen *TCP* of *UDP*. Er is geen specifieke tag voor *ICMP*. Evenwel is ICMP-verkeer toegestaan binnen een VNet door Hallo AllowVNetInBound standaardregel, waarmee verkeer tooand van elke poort en protocol binnen Hallo VNet.

### <a name="subnets"></a>Subnetten
* Overweeg het Hallo-aantal lagen die uw workload. Elke laag kan worden geïsoleerd met behulp van een subnet, en een subnet van de toohello NSG toegepast. 
* Als u een subnet tooimplement voor een VPN-gateway of ExpressRoute-circuit nodig hebt, **niet** een NSG toothat subnet toepassen. Als u dit wel doet, mislukken verbindingen tussen VNets of tussen lokale netwerkonderdelen onderling. 
* Als u een virtueel netwerkapparaat (NVA) tooimplement moet, verbinding Hallo NVA tooits eigen subnet en tooand van de gebruiker gedefinieerde routes (UDR) van Hallo NVA maken. U kunt een subnetniveau NSG toofilter verkeer in dit subnet implementeren. meer informatie over udr's, Hallo lezen toolearn [gebruiker gedefinieerde routes](virtual-networks-udr-overview.md) artikel.

### <a name="load-balancers"></a>Load balancers
* Houd rekening met Hallo load balancing en netwerk adres regels voor elke load balancer die wordt gebruikt door elk van de werkbelastingen NAT (Netwerkadresomzetting). NAT-regels zijn gebonden tooa back-end-pool met NIC's (Resource Manager) of VM's / Cloud Services-rolexemplaren (klassiek). Overweeg te maken van een NSG voor elke groep back-end, zodat alleen verkeer toegewezen via Hallo regels die zijn geïmplementeerd in Hallo netwerktaakverdelers. Een NSG voor elke back-end-adresgroep maken wordt gegarandeerd dat verkeer dat afkomstig is toohello back-end-pool rechtstreeks (plaats via Hallo load balancer), ook gefilterd.
* In klassieke implementaties maakt u eindpunten waarop poorten van een load balancer tooports op uw virtuele machines of rolinstanties. U kunt ook uw eigen individuele openbare load balancer maken via Resource Manager. Hallo doelpoort voor binnenkomend verkeer is Hallo werkelijke poort van Hallo virtuele machine of rolinstantie, niet Hallo poort door een load balancer beschikbaar gesteld. Hallo Hallo bronpoort en het adres voor Hallo verbinding toohello die VM is een poort en adres op externe computer in Hallo Internet, niet Hallo-poort en beschikbaar gesteld door Hallo load balancer-adres op.
* Wanneer u nsg's toofilter verkeer afkomstig is van een interne load balancer (ILB) maakt, zijn Hallo bron poort en adres bereik toegepast van Hallo niet Hallo load balancer-computer die afkomstig zijn. Hallo-poort en adres doelbereik zijn die van de doelcomputer hello, niet Hallo load balancer.

### <a name="other"></a>Overige
* Op basis van het eindpunt toegangsbeheerlijsten (ACL) en nsg's worden niet ondersteund op Hallo hetzelfde VM-exemplaar. Als u wilt dat een NSG toouse en beschikken over een ACL voor eindpunten al, moet u eerst Hallo ACL voor eindpunten verwijderen. Voor informatie over het tooremove een eindpunt-ACL, Zie Hallo [eindpunt-ACL's beheren](virtual-networks-acl-powershell.md) artikel.
* Resource Manager kunt u een NSG die is gekoppeld tooa NIC voor VM's met meerdere NIC's tooenable management (RAS) op basis van de NIC per. Unieke nsg's tooeach NIC koppelen, kunnen scheiding van verkeerstypen via NIC's.
* Vergelijkbare toohello gebruik van load balancers, bij het filteren van verkeer van andere vnet's, moet u bronadresbereik Hallo van Hallo externe computer niet Hallo gateway Hallo VNets verbinden.
* Veel Azure-services kunnen niet worden verbonden tooVNets. Als een Azure-resource niet verbonden tooa VNet is, kunt u een NSG toofilter verkeer toohello resource niet gebruiken.  Hallo-documentatie voor Hallo-services te lezen u toodetermine of Hallo-service verbonden tooa VNet worden kan.

## <a name="sample-deployment"></a>Voorbeeldimplementatie
een veelvoorkomend scenario van een toepassing met twee lagen weergegeven in de volgende afbeelding Hallo Houd rekening met tooillustrate Hallo toepassing hello informatie in dit artikel:

![NSG's](./media/virtual-network-nsg-overview/figure1.png)

Zoals u in het diagram hello, Hallo *Web1* en *Web2* VM's zijn verbonden toohello *FrontEnd* subnet en Hallo *DB1* en *DB2* VM's zijn verbonden toohello *back-end* subnet.  Beide subnetten behoren tot Hallo *TestVNet* VNet. Hallo toepassingsonderdelen elke uitgevoerd binnen een virtuele machine van Azure verbonden tooa VNet. Hallo scenario heeft Hallo volgens de vereisten:

1. Scheiding van verkeer tussen hello WEB- en database-servers.
2. Regels forward verkeer van Hallo load balancer tooall-webservers op poort 80 voor taakverdeling.
3. Load balancer NAT-regels forward verkeer dat afkomstig is in Hallo load balancer op poort 50001 tooport 3389 op Hallo WEB1 VM.
4. Er is geen toohello toegang front-end of back-end virtuele machines van Hallo Internet, met uitzondering van vereisten 2 en 3.
5. Er is geen uitgaande toegang tot Internet op Hallo WEB of DB-servers.
6. Toegang van Hallo FrontEnd-subnet is toegestaan tooport 3389 van elke willekeurige webserver.
7. Toegang van Hallo FrontEnd-subnet is toegestaan tooport 3389 van een databaseserver.
8. Toegang van Hallo FrontEnd-subnet is toegestaan tooport 1433 van alle DB-servers.
9. Scheiding van beheerverkeer (poort 3389) en databaseverkeer (poort 1433) op verschillende NIC's in DB-servers.

Vereisten 1-6 (met uitzondering van vereisten 3 en 4) zijn alle beperkt toosubnet spaties. Hallo volgende nsg's Hallo vorige aan vereisten voldoen, terwijl het minimaliseert Hallo aantal nsg's vereist:

### <a name="frontend"></a>FrontEnd
**Regels voor binnenkomend verkeer**

| Regel | Toegang | Prioriteit | Bronadresbereik | Bronpoort | Doeladresbereik | Doelpoort | Protocol |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Allow-Inbound-HTTP-Internet | Toestaan | 100 | Internet | * | * | 80 | TCP |
| Allow-Inbound-RDP-Internet | Toestaan | 200 | Internet | * | * | 3389 | TCP |
| Deny-Inbound-All | Weigeren | 300 | Internet | * | * | * | TCP |

**Regels voor uitgaand verkeer**

| Regel | Toegang | Prioriteit | Bronadresbereik | Bronpoort | Doeladresbereik | Doelpoort | Protocol |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Deny-Internet-All |Weigeren |100 | * | * | Internet | * | * |

### <a name="backend"></a>BackEnd
**Regels voor binnenkomend verkeer**

| Regel | Toegang | Prioriteit | Bronadresbereik | Bronpoort | Doeladresbereik | Doelpoort | Protocol |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Deny-Internet-All | Weigeren | 100 | Internet | * | * | * | * |

**Regels voor uitgaand verkeer**

| Regel | Toegang | Prioriteit | Bronadresbereik | Bronpoort | Doeladresbereik | Doelpoort | Protocol |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Deny-Internet-All | Weigeren | 100 | * | * | Internet | * | * |

Hallo volgende nsg's worden gemaakt en gekoppeld tooNICs in Hallo VM's te volgen:

### <a name="web1"></a>WEB1
**Regels voor binnenkomend verkeer**

| Regel | Toegang | Prioriteit | Bronadresbereik | Bronpoort | Doeladresbereik | Doelpoort | Protocol |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Allow-Inbound-RDP-Internet | Toestaan | 100 | Internet | * | * | 3389 | TCP |
| Allow-Inbound-HTTP-Internet | Toestaan | 200 | Internet | * | * | 80 | TCP |

> [!NOTE]
> Hallo bronadresbereik voor Hallo vorige regels wordt **Internet**, niet Hallo virtuele IP-adres van voor Hallo load balancer. Hallo-bronpoort *, niet 500001. NAT-regels voor load balancers zijn niet hetzelfde als het NSG-beveiligingsregels Hallo. NSG-regels voor beveiliging zijn altijd gerelateerde toohello oorspronkelijke bron en bestemming van het verkeer, **niet** Hallo load balancer tussen twee Hallo. 
> 
> 

### <a name="web2"></a>WEB2
**Regels voor binnenkomend verkeer**

| Regel | Toegang | Prioriteit | Bronadresbereik | Bronpoort | Doeladresbereik | Doelpoort | Protocol |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Deny-Inbound-RDP-Internet | Weigeren | 100 | Internet | * | * | 3389 | TCP |
| Allow-Inbound-HTTP-Internet | Toestaan | 200 | Internet | * | * | 80 | TCP |

### <a name="db-servers-management-nic"></a>DB-servers (beheer-NIC)
**Regels voor binnenkomend verkeer**

| Regel | Toegang | Prioriteit | Bronadresbereik | Bronpoort | Doeladresbereik | Doelpoort | Protocol |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Allow-Inbound-RDP-Front-end | Toestaan | 100 | 192.168.1.0/24 | * | * | 3389 | TCP |

### <a name="db-servers-database-traffic-nic"></a>DB-servers (NIC voor databaseverkeer)
**Regels voor binnenkomend verkeer**

| Regel | Toegang | Prioriteit | Bronadresbereik | Bronpoort | Doeladresbereik | Doelpoort | Protocol |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Allow-Inbound-SQL-Front-end | Toestaan | 100 | 192.168.1.0/24 | * | * | 1433 | TCP |

Omdat sommige Hallo nsg's gekoppeld tooindividual NIC's zijn, zijn regels Hallo voor resources die zijn geïmplementeerd via Resource Manager. Regels worden gecombineerd voor subnet en NIC, afhankelijk van hoe ze zijn gekoppeld. 

## <a name="next-steps"></a>Volgende stappen
* [NSG's implementeren (Resource Manager)](virtual-networks-create-nsg-arm-pportal.md).
* [NSG's implementeren (klassiek)](virtual-networks-create-nsg-classic-ps.md).
* [NSG-logboeken beheren](virtual-network-nsg-manage-log.md).
* [Problemen met NSG’s oplossen] (virtual-network-nsg-troubleshoot-portal.md)
