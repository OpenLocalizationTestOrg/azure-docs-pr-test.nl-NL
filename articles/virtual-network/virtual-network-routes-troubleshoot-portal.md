---
title: aaaTroubleshoot-routes - Portal | Microsoft Docs
description: Meer informatie over hoe tootroubleshoot routes aan hello Azure Resource Manager deployment model met hello Azure-Portal.
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: bdd8b6dc-02fb-4057-bb23-8289caa9de89
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 579bae91ef3200852032b3953d3cc5d26deada86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-routes-using-hello-azure-portal"></a>Routes met behulp van hello Azure Portal oplossen
> [!div class="op_single_selector"]
> * [Azure Portal](virtual-network-routes-troubleshoot-portal.md)
> * [PowerShell](virtual-network-routes-troubleshoot-powershell.md)
>
>

Als u ondervindt network connectivity problemen tooor van uw Azure-virtuele Machine (VM), routes mogelijk van invloed op uw verkeersstromen VM. Dit artikel bevat een overzicht van diagnostische gegevens mogelijkheden voor routes toohelp probleem verder oplossen.

Routetabellen zijn gekoppeld aan de subnets en effectieve zijn op alle netwerkinterfaces (NIC) in dat subnet. Hallo volgende typen routes kan netwerkinterface toegepaste tooeach zijn:

* **Systeemroutes:** elk subnet dat is gemaakt in een Azure-netwerk (VNet) heeft standaard route systeemtabellen waarmee lokale VNet-verkeer, lokale-verkeer via de VPN-gateways en internetverkeer. Systeemroutes ook aanwezig zijn voor VNets peer is ingesteld.
* **BGP-routes:** doorgegeven toonetwork interfaces via ExpressRoute of site-naar-site VPN-verbindingen. Meer informatie over BGP-routering door te lezen Hallo [BGP met VPN-gateways](../vpn-gateway/vpn-gateway-bgp-overview.md) en [overzicht van ExpressRoute](../expressroute/expressroute-introduction.md) artikelen.
* **Gebruiker gedefinieerde routes (UDR):** als u virtuele netwerkapparaten gebruikt of worden geforceerde tunneling verkeer tooan on-premises netwerk via een site-naar-site VPN, wellicht hebt u gebruiker gedefinieerde routes (udr's) die zijn gekoppeld aan de routetabel voor subnet. Als u niet bekend met udr's bent, leest u Hallo [gebruiker gedefinieerde routes](virtual-networks-udr-overview.md#user-defined-routes) artikel.

Met Hallo verschillende routes die toegepast tooa netwerkinterface worden kunnen, kan het zijn moeilijk toodetermine welke cumulatieve routes geldig zijn. toohelp VM-netwerkverbinding oplossen, kunt u alle Hallo effectieve routes voor een netwerkinterface weergeven in hello Azure Resource Manager-implementatiemodel.

## <a name="using-effective-routes-tootroubleshoot-vm-traffic-flow"></a>Met behulp van effectieve Routes tootroubleshoot VM-netwerkverkeer
In dit artikel maakt gebruik van Hallo scenario als een voorbeeld tooillustrate hoe tootroubleshoot Hallo effectief voor een netwerkinterface routeert te volgen:

Een virtuele machine (*VM1*) verbonden toohello VNet (*VNet1*, voorvoegsel: 10.9.0.0/16) tooconnect tooa VM(VM3) in een nieuw peered VNet is mislukt (*VNet3*, 10.10.0.0/16 voorvoegsel). Er zijn geen udr's of BGP-routes toegepaste tooVM1-NIC1 network interface die is verbonden toohello VM, alleen de systeemroutes van het worden toegepast.

Dit artikel wordt uitgelegd hoe toodetermine Hallo veroorzaken Hallo verbinding mislukt, met behulp van de mogelijkheid effectieve routes in Azure Resource Management-implementatiemodel.
Tijdens het Hallo-voorbeeld wordt alleen de systeemroutes van het, Hallo dezelfde stappen kan worden gebruikte toodetermine binnenkomende en uitgaande verbindingsfouten via een routetype.

> [!NOTE]
> Als uw virtuele machine meer dan één NIC die is gekoppeld heeft, controleert u effectieve routes voor elk Hallo NIC's toodiagnose network connectivity problemen tooand van een virtuele machine.
>
>

### <a name="view-effective-routes-for-a-virtual-machine"></a>De effectieve routes weergeven voor een virtuele machine
toosee hello cumulatieve routes die zijn toegepast tooa VM, volledige Hallo stappen te volgen:

1. Aanmelding toohello Azure-portal op https://portal.azure.com.
2. Klik op **meer services**, klikt u vervolgens op **virtuele machines** in Hallo lijst die wordt weergegeven.
3. Selecteer een VM-tootroubleshoot in Hallo lijst die wordt weergegeven en een VM-blade met opties wordt weergegeven.
4. Klik op **spoor & oplossen van problemen met** en selecteer vervolgens een veelvoorkomend probleem. In dit voorbeeld **ik kan geen verbinding maken toomy Windows VM** is geselecteerd.

    ![](./media/virtual-network-routes-troubleshoot-portal/image1.png)
5. Stappen worden vermeld onder Hallo probleem, zoals wordt weergegeven in de volgende afbeelding Hallo:

    ![](./media/virtual-network-routes-troubleshoot-portal/image2.png)

    Klik op *effectieve routes* in Hallo lijst met aanbevolen stappen.
6. Hallo **effectieve routes** blade wordt weergegeven, zoals wordt weergegeven in de volgende afbeelding Hallo:

    ![](./media/virtual-network-routes-troubleshoot-portal/image3.png)

    Als uw virtuele machine slechts één NIC heeft, is standaard geselecteerd. Als u meer dan één NIC hebt, selecteert u Hallo NIC waarvoor u tooview Hallo effectieve routes wilt.

   > [!NOTE]
   > Als hello VM gekoppeld hello NIC is niet actief is, effectieve routes niet worden weergegeven. Alleen worden hello eerste 200 effectieve routes weergegeven in Hallo-portal. Klik voor de volledige lijst Hallo **downloaden**. Verder kunt u filteren op Hallo van resultaten vanuit Hallo gedownloade CSV-bestand.
   >
   >

    U ziet in Hallo uitvoer Hallo volgende:

   * **Bron**: geeft Hallo-type van de route. Systeemroutes worden weergegeven als *standaard*, udr's worden weergegeven als *gebruiker* en routes gateway (statische of BGP) worden weergegeven als *VPNGateway*.
   * **Status**: geeft de status van de effectieve Hallo-route. Mogelijke waarden zijn *Active* of *ongeldig*.
   * **AddressPrefixes**: Hiermee geeft u Hallo-adresvoorvoegsel van Hallo effectieve route in CIDR-notatie.
   * **nextHopType**: geeft aan Hallo volgende hop voor Hallo opgegeven route. Mogelijke waarden zijn *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering*, of *Null*. Een waarde van *Null* voor **nextHopType** een UDR kan duiden op een ongeldige route. Bijvoorbeeld, als **nextHopType** is *VirtualAppliance* en Hallo virtueel netwerkapparaat VM niet in een status ingericht/uitvoeren is. Als **nextHopType** is *VPNGateway* en er is geen gateway ingericht/uitvoeren in VNet gegeven hello, Hallo route ongeldig geworden.
7. Er is geen route vermeld toohello *WestUS VNET3* VNet (10.10.0.0/16 voorvoegsel) van Hallo *WestUS VNet1* (voorvoegsel 10.9.0.0/16) in de afbeelding in de vorige stap Hallo Hallo. Hallo peeringkoppeling in Hallo volgende afbeelding, wordt Hallo *verbroken* status:

    ![](./media/virtual-network-routes-troubleshoot-portal/image4.png)

    Hallo bidirectionele koppeling voor Hallo peering verbroken wordt, waarin wordt uitgelegd waarom VM1 kan geen verbinding maken tooVM3 in Hallo *WestUS VNet3* VNet.
8. Hallo volgende afbeelding ziet u Hallo routes na het tot stand brengen van Hallo bidirectionele peeringkoppeling:

    ![](./media/virtual-network-routes-troubleshoot-portal/image5.png)

Lees voor meer probleemoplossing scenario's voor evaluatie van geforceerde tunneling en route, Hallo [overwegingen](virtual-network-routes-troubleshoot-portal.md#considerations) sectie van dit artikel.

### <a name="view-effective-routes-for-a-network-interface"></a>De effectieve routes weergeven voor een netwerkinterface
Als het netwerkverkeer is van invloed op voor een bepaalde netwerkinterface (NIC), kunt u een volledige lijst van effectieve routes rechtstreeks op een Netwerkinterfacekaart weergeven. toosee hello cumulatieve routes die zijn toegepast tooa NIC, volledige Hallo stappen te volgen:

1. Aanmelding toohello Azure-portal op https://portal.azure.com.
2. Klik op **meer services**, klikt u vervolgens op **netwerkinterfaces**
3. Zoek in de lijst Hallo Hallo-naam van een NIC of Selecteer deze in Hallo lijst die wordt weergegeven. In dit voorbeeld **VM1 NIC1** is geselecteerd.
4. Selecteer **effectieve routes** in Hallo **netwerkinterface** blade, zoals wordt weergegeven in de volgende afbeelding Hallo:

       ![](./media/virtual-network-routes-troubleshoot-portal/image6.png)

    Hallo **bereik** standaardwaarden toohello-netwerkinterface is geselecteerd.

      ![](./media/virtual-network-routes-troubleshoot-portal/image7.png)

### <a name="view-effective-routes-for-a-route-table"></a>Effectieve routes voor een routetabel weergeven
Als u de gebruiker gedefinieerde routes (udr's) in een routetabel wijzigt, kunt u tooreview Hallo gevolgen van het Hallo-routes wordt toegevoegd aan een bepaalde virtuele machine. Een routetabel kan worden gekoppeld aan een willekeurig aantal subnetten. U kunt nu alle Hallo effectieve routes weergeven voor alle Hallo NIC's die een bepaalde routetabel wordt toegepast zonder tooswitch context uit Hallo route tabel blade gegeven.

Bijvoorbeeld, een UDR (*UDRoute*) is opgegeven in een routetabel (*UDRouteTable*). Deze route verzendt alle internetverkeer van *Subnet1* in Hallo *WestUS VNet1* VNet via een virtueel apparaat voor netwerk (NVA) in *Subnet2* van Hallo hetzelfde VNet. Hallo route wordt weergegeven in de volgende afbeelding Hallo:

![](./media/virtual-network-routes-troubleshoot-portal/image8.png)

toosee hello cumulatieve routes voor een routetabel, volledige Hallo stappen te volgen:

1. Aanmelding toohello Azure-portal op https://portal.azure.com.
2. Klik op **meer services**, klikt u vervolgens op **routetabellen**
3. Hallo zoeklijst voor de routetabel hello wilt toosee cumulatieve routes voor en selecteer deze. In dit voorbeeld **UDRouteTable** is geselecteerd. Een blade voor de routetabel Hallo geselecteerd wordt weergegeven, zoals wordt weergegeven in de volgende afbeelding Hallo:

    ![](./media/virtual-network-routes-troubleshoot-portal/image9.png)
4. Selecteer **effectieve Routes** in Hallo **routetabel** blade. Hallo **bereik** toohello routetabel geselecteerde is ingesteld.
5. Een routetabel kan worden toegepast toomultiple subnetten. Selecteer Hallo **Subnet** gewenste tooreview uit Hallo-lijst. In dit voorbeeld **Subnet1** is geselecteerd.
6. Selecteer een **netwerkinterface**. Alle NIC's aangesloten toohello geselecteerd subnet worden weergegeven. In dit voorbeeld **VM1 NIC1** is geselecteerd.

    ![](./media/virtual-network-routes-troubleshoot-portal/image10.png)

   > [!NOTE]
   > Als Hallo NIC niet gekoppeld aan een actieve virtuele machine is, worden er geen effectieve routes weergegeven.
   >
   >

## <a name="considerations"></a>Overwegingen
Een paar dingen tookeep rekening moet houden bij het controleren van de lijst met routes Hallo geretourneerd:

* Routering is gebaseerd op langste voorvoegsel overeen (LPM) tussen udr's, systeem- en BGP-routes. Als er meer dan één route met Hallo dezelfde LPM overeenkomen, en vervolgens een route geselecteerd op basis van de oorsprong in Hallo volgorde:

  * Gebruiker gedefinieerde route
  * BGP-route
  * Systeemroute (standaard)

    U kunt alleen effectieve routes die overeenkomende LPM op basis van alle routes van Hallo beschikbaar zijn met effectieve routes zien. Door te laten zien hoe Hallo routes daadwerkelijk wordt geëvalueerd voor een bepaalde NIC, maakt dit het veel eenvoudiger tootroubleshoot specifieke routes die mogelijk van invloed op de connectiviteit van uw virtuele machine.
* Als u udr's hebt en van verkeer tooa netwerk virtueel apparaat (NVA) met verzenden *VirtualAppliance* als **nextHopType**, zorg dat doorsturen via IP is ingeschakeld op het Hallo NVA ontvangende Hallo verkeer of pakketten worden verwijderd.
* Als de geforceerde tunneling is ingeschakeld, worden alle uitgaand internetverkeer gerouteerde tooon-premises. RDP/SSH vanaf Internet tooyour die VM niet met deze instelling werkt, afhankelijk van hoe Hallo lokale verwerkt dit verkeer.
  Geforceerde tunneling kan worden ingeschakeld:
  * Als u site-naar-site VPN, door een door de gebruiker opgegeven routes (UDR) met nextHopType als VPN-Gateway
  * Als een standaardroute wordt geadverteerd via BGP
* Voor VNet-verkeer toowork correct peering een systeemroute met **nextHopType** *VNetPeering* voor Hallo van de VNet-voorvoegsel bereik brengen moet bestaan. Als deze route bestaat niet en VNet-peering Hallo opgezocht koppeling OK:
  * Wacht een paar seconden en probeer het opnieuw als het een nieuw opgezette peeringkoppeling. Tijd tot tijd duurt het langer toopropagate routes tooall Hallo netwerkinterfaces in een subnet.
  * Netwerkbeveiligingsgroep (NSG) regels mogelijk van invloed op Hallo verkeersstromen. Zie voor meer informatie, Hallo [Netwerkbeveiligingsgroepen oplossen](virtual-network-nsg-troubleshoot-portal.md) artikel.
