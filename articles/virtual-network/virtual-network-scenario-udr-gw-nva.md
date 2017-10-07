---
title: aaaHybrid verbinding met 2-tier-toepassing | Microsoft Docs
description: Meer informatie over hoe toodeploy virtuele apparaten en UDR toocreate de omgeving van een toepassing met meerdere lagen in Azure
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 1f509bec-bdd1-470d-8aa4-3cf2bb7f6134
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/05/2016
ms.author: jdial
ms.openlocfilehash: 53599862289dbf9c6ab3289b0cb8dda6430f20f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-appliance-scenario"></a>Virtueel apparaat scenario
Een veelvoorkomend scenario tussen groter Azure klant is Hallo nodig tooprovide een toepassing met twee lagen die toegankelijk is toohello Internet, en tegelijkertijd toegang toohello back-laag van een on-premises datacenter. Dit document begeleidt u stapsgewijs door een scenario waarbij de gebruiker gedefinieerde Routes (UDR), een VPN-Gateway en netwerk virtuele apparaten toodeploy een omgeving met twee lagen die voldoet aan Hallo volgens de vereisten:

* Webtoepassing toegankelijk moet zijn vanop Hallo alleen het openbare Internet.
* Hosting Hallo webtoepassing-server moet kunnen tooaccess een back-end-toepassingsserver.
* Al het verkeer van Hallo Internet toohello webtoepassing moet via een virtueel firewallapparaat gaan. Deze virtueel apparaat wordt gebruikt voor Internet-verkeer.
* Alle verkeer dat hierheen gaat toohello toepassingsserver moet gaan via een firewall virtueel apparaat. Deze virtueel apparaat wordt gebruikt voor toegang tot toohello back-endserver en toegang afkomstig van Hallo on-premises netwerk via een VPN-Gateway.
* Beheerders moeten kunnen toomanage Hallo firewall virtuele apparaten van hun lokale computers, met behulp van een derde firewall virtueel apparaat gebruikt uitsluitend voor beheerdoeleinden.

Dit is een standaard DMZ scenario met een Perimeternetwerk en een beveiligd netwerk. Dergelijke scenario kan worden gemaakt in Azure met nsg's, firewall virtuele apparaten of een combinatie van beide. Hallo in de volgende tabel bevat enkele van Hallo-voor- en nadelen tussen nsg's en virtuele firewallapparaten.

|  | Professionals | Nadelen |
| --- | --- | --- |
| NSG |Er zijn geen kosten. <br/>Geïntegreerd in Azure RBAC. <br/>Regels kunnen worden gemaakt in ARM-sjablonen. |Complexiteit kan variëren in grotere omgevingen. |
| Firewall |Volledige controle over vlak van gegevens. <br/>Centraal beheer via de firewall-console. |Kosten van de firewall-apparaat. <br/>Niet geïntegreerd met Azure RBAC. |

Hallo oplossing onderstaande gebruikt firewall virtuele apparaten tooimplement een DMZ/beveiligd netwerk scenario.

## <a name="considerations"></a>Overwegingen
U kunt Hallo-omgeving die hierboven worden uitgelegd in Azure met behulp van verschillende functies die beschikbaar zijn vandaag, als volgt implementeren.

* **Virtueel netwerk (VNet)**. Een Azure VNet fungeert in vergelijkbare wijze tooan on-premises netwerk en kunnen worden gesegmenteerd in een of meer subnetten tooprovide verkeersisolatie en scheiding van problemen.
* **Virtueel apparaat**. Diverse partners bieden virtuele apparaten in hello Azure Marketplace die kunnen worden gebruikt voor de drie firewalls Hallo die hierboven worden beschreven. 
* **De gebruiker gedefinieerde Routes (UDR)**. Routetabellen kunnen udr's die worden gebruikt door Azure netwerken toocontrol Hallo stroom van pakketten binnen een VNet bevatten. Deze routetabellen kunnen worden toegepast toosubnets. Een van de nieuwste functies Hallo in Azure is Hallo mogelijkheid tooapply een route tabel toohello GatewaySubnet, bieden Hallo mogelijkheid tooforward al het verkeer afkomstig is van een virtueel apparaat voor hybride verbinding tooa in hello Azure VNet.
* **Doorsturen via IP**. Standaard hello Azure VPN-engine doorsturen van pakketten toovirtual netwerkinterfacekaarten (NIC's) alleen als Hallo pakket doel-IP-adres overeenkomt met de Hallo NIC IP-adres. Als een UDR definieert een pakket tooa gegeven virtueel apparaat moet worden verzonden, zou hello Azure VPN-engine daarom dat pakket verwijderen. tooensure hello pakket tooa VM (in dit geval een virtueel apparaat), die niet de werkelijke bestemming Hallo Hallo pakket wordt geleverd, moet u doorsturen via IP tooenable voor Hallo virtueel apparaat.
* **Netwerkbeveiligingsgroepen (nsg's)**. Hallo in het volgende voorbeeld maakt geen gebruik van het nsg's, maar u kunt nsg's toegepast toohello subnetten en/of NIC's in deze oplossing toofurther filter Hallo binnenkomend en uitgaand verkeer die subnetten en NIC's.

![IPv6-connectiviteit](./media/virtual-network-scenario-udr-gw-nva/figure01.png)

In dit voorbeeld is er een abonnement dat Hallo volgende bevat:

* 2 resourcegroepen, niet weergegeven in Hallo-diagram. 
  * **ONPREMRG**. Bevat alle resources nodig toosimulate een on-premises netwerk.
  * **AZURERG**. Bevat alle resources die nodig zijn voor Hallo virtueel netwerk van Azure-omgeving. 
* Een VNet met de naam **onpremvnet** toomimic een on-premises datacenter gesegmenteerde hieronder vermelde gebruikt.
  * **onpremsn1**. Subnet met een virtuele machine (VM) die met Ubuntu toomimic een on-premises server.
  * **onpremsn2**. Subnet met een virtuele machine Ubuntu toomimic met een on-premises-computer die wordt gebruikt door een beheerder.
* Er is een firewall virtueel apparaat met de naam **OPFW** op **onpremvnet** toomaintain een tunnel te gebruikt**azurevnet**.
* Een VNet met de naam **azurevnet** gesegmenteerde zoals hieronder weergegeven.
  * **azsn1**. Externe firewall subnet uitsluitend voor Hallo externe firewall gebruikt. Al het internetverkeer wordt geleverd in via dit subnet. Dit subnet bevat alleen een gekoppelde NIC toohello externe firewall.
  * **azsn2**. Front-end-subnet die als host fungeert voor een virtuele machine wordt uitgevoerd als een webserver die kan worden bereikt vanaf Hallo Internet.
  * **azsn3**. Back-end subnet die als host fungeert voor een virtuele machine een back-end-toepassingsserver die wordt geopend door Hallo front-end-webserver uitgevoerd.
  * **azsn4**. Management subnet gebruikt uitsluitend tooprovide management toegang tooall firewall virtuele apparaten. Dit subnet bevat alleen een NIC voor elke firewall virtueel apparaat gebruikt voor Hallo-oplossing.
  * **GatewaySubnet**. Azure hybride verbinding subnet vereist voor de ExpressRoute- en VPN-Gateway tooprovide-connectiviteit tussen Azure VNets en andere netwerken. 
* Er zijn 3 firewall virtuele apparaten in Hallo **azurevnet** netwerk. 
  * **AZF1**. Externe firewall blootgesteld toohello openbare Internet met behulp van een openbare IP-adres resource in Azure. U moet tooensure die u hebt een sjabloon van Hallo Marketplace, of rechtstreeks van de leverancier van uw apparaat, dat voorziet in een virtueel apparaat 3-NIC.
  * **AZF2**. Interne firewall gebruikt toocontrol verkeer tussen **azsn2** en **azsn3**. Dit is ook een 3-NIC virtueel apparaat.
  * **AZF3**. Beheer van firewall toegankelijk tooadministrators van Hallo on-premises datacenter, en verbonden tooa management subnet gebruikt toomanage alle firewallapparaten. U kunt 2-NIC sjablonen voor virtueel apparaat vinden in Hallo Marketplace of aanvragen rechtstreeks bij de leverancier van uw apparaat.

## <a name="user-defined-routing-udr"></a>Door de gebruiker gedefinieerde Routering
Elk subnet in Azure mag gekoppelde tooa UDR tabel die wordt gebruikt toodefine hoe in dat subnet gestart verkeer wordt gerouteerd. Als er geen udr's zijn gedefinieerd, wordt standaard routes tooallow verkeer tooflow uit één subnet tooanother gebruikt in Azure. toobetter udr's begrijpen, gaat u naar [wat de gebruiker gedefinieerde Routes en doorsturen via IP zijn](virtual-networks-udr-overview.md#ip-forwarding).

tooensure communicatie vindt plaats via Hallo rechts firewallapparaat, op basis van de laatste vereiste Hallo hierboven, moet u toocreate Hallo volgende met udr's in de routetabel **azurevnet**.

### <a name="azgwudr"></a>azgwudr
Hallo alleen verkeer van de lokale tooAzure gebruikte toomanage Hallo firewalls door verbinding te maken in dit scenario**AZF3**, en dat verkeer Hallo interne firewall, moet via **AZF2**. Slechts één route is daarom nodig in Hallo **GatewaySubnet** zoals hieronder wordt weergegeven.

| Doel | Volgende hop | Uitleg |
| --- | --- | --- |
| 10.0.4.0/24 |10.0.3.11 |Lokale verkeer tooreach management firewall kunt **AZF3** |

### <a name="azsn2udr"></a>azsn2udr
| Doel | Volgende hop | Uitleg |
| --- | --- | --- |
| 10.0.3.0/24 |10.0.2.11 |Kan subnet voor back-end van verkeer toohello die als host fungeert voor de toepassingsserver Hallo via **AZF2** |
| 0.0.0.0/0 |10.0.2.10 |Hiermee kunt u alle andere verkeer toobe doorgestuurd via **AZF1** |

### <a name="azsn3udr"></a>azsn3udr
| Doel | Volgende hop | Uitleg |
| --- | --- | --- |
| 10.0.2.0/24 |10.0.3.10 |Gegevensverkeer te**azsn2** tooflow van app-server toohello webserver via **AZF2** |

U moet ook routetabellen toocreate voor Hallo subnetten in **onpremvnet** toomimic Hallo lokale datacenter.

### <a name="onpremsn1udr"></a>onpremsn1udr
| Doel | Volgende hop | Uitleg |
| --- | --- | --- |
| 192.168.2.0/24 |192.168.1.4 |Gegevensverkeer te**onpremsn2** via **OPFW** |

### <a name="onpremsn2udr"></a>onpremsn2udr
| Doel | Volgende hop | Uitleg |
| --- | --- | --- |
| 10.0.3.0/24 |192.168.2.4 |Kan verkeerssubnet toohello back in Azure maakt via **OPFW** |
| 192.168.1.0/24 |192.168.2.4 |Gegevensverkeer te**onpremsn1** via **OPFW** |

## <a name="ip-forwarding"></a>Doorsturen via IP
Zijn de functies die u in combinatie tooallow virtuele apparaten toobe gebruikt toocontrol netwerkverkeer in een Azure-VNet gebruiken kunt UDR en doorsturen via IP.  Een virtueel apparaat is niets meer dan een virtuele machine die een toepassing die wordt gebruikt toohandle-netwerkverkeer in een bepaalde manier, zoals een firewall of een NAT-apparaat wordt uitgevoerd.

Deze virtueel apparaat die VM kunnen tooreceive inkomend verkeer die moet worden verholpen niet tooitself. een VM-verkeer tooreceive tooallow geadresseerd tooother bestemmingen, u moet voor Hallo VM doorsturen via IP inschakelen. Dit is een Azure-instelling, niet een instelling in het gastbesturingssysteem Hallo. Uw nog steeds behoeften-toorun van virtueel apparaat, enkele toepassing toohandle type Hallo binnenkomend verkeer en op de juiste wijze omgeleid.

toolearn meer informatie over het doorsturen via IP, gaat u naar [wat de gebruiker gedefinieerde Routes en doorsturen via IP zijn](virtual-networks-udr-overview.md#ip-forwarding).

Stel, dat u hebt Hallo na de installatie in een Azure vnet bijvoorbeeld:

* Subnet **onpremsn1** bevat een virtuele machine met de naam **onpremvm1**.
* Subnet **onpremsn2** bevat een virtuele machine met de naam **onpremvm2**.
* Een virtueel apparaat met de naam **OPFW** te is verbonden**onpremsn1** en **onpremsn2**.
* Een door de gebruiker gedefinieerde route gekoppeld te**onpremsn1** geeft aan dat alle te verkeer**onpremsn2** te moeten worden verzonden**OPFW**.

Op dit punt, als **onpremvm1** tooestablish probeert een verbinding met **onpremvm2**, hello UDR wordt gebruikt en verkeer te worden verzonden**OPFW** als Hallo volgende hop. Houd er rekening mee dat het doel van de daadwerkelijke pakket Hallo wordt niet gewijzigd, wordt nog steeds aangegeven **onpremvm2** Hallo doel. 

Zonder de IP-doorsturen is ingeschakeld voor **OPFW**, hello Azure virtuele netwerken logica wordt hello-pakketten verwijderen, omdat alleen pakketten toobe verzonden tooa VM als hello van de virtuele machine IP-adres Hallo bestemming voor hello-pakket.

Met het doorsturen van IP-stuurt Hallo logica van de virtuele Azure-netwerk hello-pakketten tooOPFW, zonder dat u de oorspronkelijke doeladres wijzigt. **OPFW** moet verwerken hello-pakketten en bepalen welke toodo mee.

Voor de bovenstaande toowork Hallo scenario, moet u inschakelen op Hallo NIC's voor doorsturen via IP **OPFW**, **AZF1**, **AZF2**, en **AZF3** die worden gebruikt voor routering (alle NIC's, behalve Hallo die zijn gekoppeld toohello management subnet). 

## <a name="firewall-rules"></a>Firewallregels
Zoals hierboven wordt beschreven, doorsturen via IP alleen zorgt ervoor dat pakketten toohello virtuele apparaten worden verzonden. Uw apparaat moet nog steeds toodecide welke toodo met deze pakketten. Hallo bovenstaande scenario moet u toocreate Hallo regels in uw apparaten te volgen:

### <a name="opfw"></a>OPFW
OPFW vertegenwoordigt een on-premises-apparaat met Hallo volgens de regels voor:

* **Route**: alle verkeer too10.0.0.0/16 (**azurevnet**) moet worden verzonden via de tunnel **ONPREMAZURE**.
* **Beleid**: alle bidirectionele verkeer tussen **port2** en **ONPREMAZURE**.

### <a name="azf1"></a>AZF1
AZF1 vertegenwoordigt een Azure virtueel apparaat Hallo volgens de regels met:

* **Beleid**: alle bidirectionele verkeer tussen **port1** en **port2**.

### <a name="azf2"></a>AZF2
AZF2 vertegenwoordigt een Azure virtueel apparaat Hallo volgens de regels met:

* **Route**: alle verkeer too10.0.0.0/16 (**onpremvnet**) toohello Azure-gateway IP-adres (dat wil zeggen 10.0.0.1) moet worden verzonden via **port1**.
* **Beleid**: alle bidirectionele verkeer tussen **port1** en **port2**.

## <a name="network-security-groups-nsgs"></a>Netwerkbeveiligingsgroepen (nsg's)
Nsg's worden in dit scenario wordt niet gebruikt. U kunt echter nsg's tooeach subnet toorestrict binnenkomend en uitgaand verkeer toepassen. U kunt bijvoorbeeld Hallo volgende NSG-regels toohello externe FW subnet toepassen.

**Binnenkomende**

* Alle TCP-verkeer van Hallo Internet tooport 80 op elke virtuele machine in Hallo subnet toestaan.
* Al het andere verkeer vanaf Hallo Internet weigeren.

**Uitgaande**

* Alle verkeer toohello Internet weigeren.

## <a name="high-level-steps"></a>Hoog niveau stappen
toodeploy in dit scenario Hallo hoog niveau stappen hieronder.

1. Aanmelding tooyour Azure-abonnement.
2. Als u een VNet toomimic hello toodeploy lokale netwerk wilt, Hallo-resources die deel van uitmaken inrichten **ONPREMRG**.
3. Hallo-resources die deel van uitmaken inrichten **AZURERG**.
4. Hallo-tunnel inrichten van **onpremvnet** te**azurevnet**.
5. Zodra alle resources zijn ingericht, meld u aan te**onpremvm2** en ping 10.0.3.101 tootest connectiviteit tussen **onpremsn2** en **azsn3**.

