---
title: aaaTroubleshoot-routes - PowerShell | Microsoft Docs
description: Meer informatie over hoe tootroubleshoot routeert hello Azure Resource Manager-implementatiemodel met Azure PowerShell.
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: bf7dc5e7-9399-460e-8e0d-8992dbed98a6
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 7a07806df5c1d0caee921187e6ad29f6755ab535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-routes-using-azure-powershell"></a>Problemen oplossen met Azure PowerShell routes
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

### <a name="view-effective-routes-for-a-network-interface"></a>De effectieve routes weergeven voor een netwerkinterface
toosee hello cumulatieve routes die zijn toegepast tooa netwerkinterface, volledige Hallo stappen te volgen:

1. Start een Azure PowerShell-sessie en meld u aan tooAzure. Als u niet bekend met Azure PowerShell bent, leest u Hallo [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) artikel.
2. Hallo volgende opdracht retourneert alle routes toegepast tooa-netwerkinterface met de naam *VM1 NIC1* in de resourcegroep Hallo *RG1*.
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > Als u de naam van een netwerkinterface Hallo niet weet, typt u Hallo tooretrieve Hallo opdrachtnamen van alle netwerkinterfaces in een resource group.* na
   > 
   > 
   
       Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name
   
   Hallo volgende uitvoer ziet er vergelijkbare toohello uitvoer voor elke route toegepast toohello subnet Hallo die NIC is verbonden met:
   
       Name :
       State : Active
       AddressPrefix : {10.9.0.0/16}
       NextHopType : VNetLocal
       NextHopIpAddress : {}
   
       Name :
       State : Active
       AddressPrefix : {0.0.0.0/16}
       NextHopType : Internet
       NextHopIpAddress : {}
   
   U ziet in Hallo uitvoer Hallo volgende:
   
   * **Naam**: naam van de effectieve route Hallo mag niet leeg zijn, tenzij expliciet is opgegeven voor de gebruiker gedefinieerde routes. 
   * **Status**: geeft de status van de effectieve Hallo-route. Mogelijke waarden zijn 'Active' of 'Ongeldig'
   * **AddressPrefixes**: Hiermee geeft u Hallo-adresvoorvoegsel van Hallo effectieve route in CIDR-notatie. 
   * **nextHopType**: geeft aan Hallo volgende hop voor Hallo opgegeven route. Mogelijke waarden zijn *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering*, of *Null*. Een waarde van *Null* voor **nextHopType** een UDR kan duiden op een ongeldige route. Bijvoorbeeld, als **nextHopType** is *VirtualAppliance* en Hallo virtueel netwerkapparaat VM niet in een status ingericht/uitvoeren is. Als **nextHopType** is *VPNGateway* en er is geen gateway ingericht/uitvoeren in VNet gegeven hello, Hallo route ongeldig geworden.
   * **NextHopIpAddress**: Hallo IP-adres van de volgende hop Hallo van Hallo effectieve route.
   
   Hallo volgende opdracht retourneert Hallo routes in een eenvoudiger tooview tabel:
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1 | Format-Table
   
   Hallo volgende uitvoer is aantal Hallo uitvoer ontvangen voor Hallo scenario eerder beschreven:
   
       Name State AddressPrefix NextHopType NextHopIpAddress
       ---- ----- ------------- ----------- ----------------
       Active {10.9.0.0/16} VnetLocal {}
       Active {0.0.0.0/0} Internet {}
3. Er is geen route vermeld toohello *WestUS VNet3* VNet (10.10.0.0/16)** van het voorvoegsel *WestUS VNet1* (voorvoegsel 10.9.0.0/16) in de uitvoer van de vorige stap Hallo Hallo. Zoals u in de volgende afbeelding hello, Hallo VNet peeringkoppeling Hello *WestUS VNet3* VNet is in Hallo *verbroken* status.
   
    ![](./media/virtual-network-routes-troubleshoot-portal/image4.png)
   
    Hallo bidirectionele koppeling voor Hallo peering verbroken wordt, waarin wordt uitgelegd waarom VM1 kan geen verbinding maken tooVM3 in Hallo *WestUS VNet3* VNet. Instellen van een bidirectionele VNet-peeringkoppeling opnieuw voor *WestUS VNet1* en *WestUS VNet3* VNets. Hier volgt Hallo uitvoer die wordt geretourneerd nadat Hallo VNet peeringkoppeling correct is ingesteld:
   
        Name State AddressPrefix NextHopType NextHopIpAddress
        ---- ----- ------------- ----------- ----------------
        Active {10.9.0.0/16} VnetLocal {}
        Active {10.10.0.0/16} VNetPeering {}
        Active {0.0.0.0/0} Internet {}
   
    Zodra u hebt vastgesteld Hallo probleem, u kunt toevoegen, verwijderen, of wijzig routes en routetabellen. Type Hallo na de opdracht toosee een lijst met opdrachten Hallo gebruikt dus toodo:
   
        Get-Help *-AzureRmRouteConfig

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
  * Netwerkbeveiligingsgroep (NSG) regels mogelijk van invloed op Hallo verkeersstromen. Zie voor meer informatie, Hallo [Netwerkbeveiligingsgroepen oplossen](virtual-network-nsg-troubleshoot-powershell.md) artikel.

