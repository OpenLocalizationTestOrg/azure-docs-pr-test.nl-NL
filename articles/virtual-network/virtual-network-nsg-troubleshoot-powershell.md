---
title: aaaTroubleshoot Netwerkbeveiligingsgroepen - PowerShell | Microsoft Docs
description: Meer informatie over hoe tootroubleshoot Netwerkbeveiligingsgroepen in hello Azure Resource Manager deployment model met Azure PowerShell.
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 4c732bb7-5cb1-40af-9e6d-a2a307c2a9c4
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 95fd60fa72cf6d17fa990e3c3eb7d980878f7c15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-network-security-groups-using-azure-powershell"></a>Problemen met Netwerkbeveiligingsgroepen met Azure PowerShell
> [!div class="op_single_selector"]
> * [Azure Portal](virtual-network-nsg-troubleshoot-portal.md)
> * [PowerShell](virtual-network-nsg-troubleshoot-powershell.md)
> 
> 

Als u Netwerkbeveiligingsgroepen (nsg's) geconfigureerd op de virtuele machine (VM) en problemen met de netwerkverbinding van de VM ondervinden, biedt dit artikel een overzicht van diagnostische gegevens mogelijkheden voor het nsg's toohelp probleem verder oplossen.

Nsg's kunnen u toocontrol Hallo typen verkeer stromen en naar uw virtuele machines (VM's). Nsg's kunnen worden toegepast toosubnets in een Azure-netwerk (VNet), netwerkinterfaces (NIC) of beide. Hallo effectieve regels toegepast tooa NIC zijn een aggregatie van Hallo-regels die zijn opgenomen in Hallo nsg's toegepast tooa NIC en het Hallo-subnet is verbonden met. Regels in deze nsg's kunnen soms met elkaar conflicteren en invloed van een virtuele machine netwerkverbinding.  

U kunt alle Hallo effectieve beveiligingsregels voor verbindingen weergeven van uw nsg's, zoals toegepast op de NIC's van de VM. Dit artikel laat zien hoe tootroubleshoot VM-verbindingsproblemen met deze regels in hello Azure Resource Manager-implementatiemodel. Als u niet bekend met concepten VNet en NSG bent, leest u Hallo [virtueel netwerk](virtual-networks-overview.md) en [Netwerkbeveiligingsgroepen](virtual-networks-nsg.md) overzicht artikelen.

## <a name="using-effective-security-rules-tootroubleshoot-vm-traffic-flow"></a>Met behulp van effectieve beveiligingsregels tootroubleshoot VM-netwerkverkeer
Hallo-scenario dat volgt is een voorbeeld van een veelvoorkomend verbindingsprobleem:

Een virtuele machine met de naam *VM1* maakt deel uit van een subnet met de naam *Subnet1* binnen een VNet met de naam *WestUS VNet1*. Een poging tooconnect toohello met RDP via TCP-poort 3389 VM is mislukt. Nsg's worden toegepast op beide Hallo NIC *VM1 NIC1* en subnet Hallo *Subnet1*. Verkeer tooTCP poort 3389 is toegestaan in Hallo NSG die is gekoppeld aan de netwerkinterface Hallo *VM1 NIC1*, maar TCP pingen tooVM1 van poort 3389 mislukt.

Hoewel dit voorbeeld wordt de TCP-poort 3389 gebruikt, Hallo volgende stappen kan worden gebruikte toodetermine binnenkomende en uitgaande verbindingsfouten via een willekeurige poort.

## <a name="detailed-troubleshooting-steps"></a>Gedetailleerde stappen voor probleemoplossing
De volgende volledige Hallo stappen tootroubleshoot nsg's voor een virtuele machine:

1. Start een Azure PowerShell-sessie en meld u aan tooAzure. Als u niet bekend bent met behulp van Azure PowerShell, leest u Hallo [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) artikel.
2. Voer Hallo na de opdracht tooreturn alle NSG-regels toegepast tooa NIC met de naam *VM1 NIC1* in de resourcegroep Hallo *RG1*:
   
        Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > Als u niet Hallo-naam van een NIC weet, voert u Hallo tooretrieve Hallo opdrachtnamen van alle NIC's in een resourcegroep te volgen: 
   > 
   > `Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name`
   > 
   > 
   
    Hallo volgende tekst is een voorbeeld van Hallo effectieve regels uitvoer die wordt geretourneerd voor Hallo *VM1 NIC1* NIC:
   
        NetworkSecurityGroup   : {
                                   "Id": "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkSecurityGroups/VM1-NIC1-NSG"
                                 }
        Association            : {
                                   "NetworkInterface": {
                                     "Id": "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkInterfaces/VM1-NIC1"
                                   }
                                 }
        EffectiveSecurityRules : [
                                 {
                                 "Name": "securityRules/allowRDP",
                                 "Protocol": "Tcp",
                                 "SourcePortRange": "0-65535",
                                 "DestinationPortRange": "3389-3389",
                                 "SourceAddressPrefix": "Internet",
                                 "DestinationAddressPrefix": "0.0.0.0/0",
                                 "ExpandedSourceAddressPrefix": [… ],
                                 "ExpandedDestinationAddressPrefix": [],
                                 "Access": "Allow",
                                 "Priority": 1000,
                                 "Direction": "Inbound"
                                 },
                                 {
                                 "Name": "defaultSecurityRules/AllowVnetInBound",
                                 "Protocol": "All",
                                 "SourcePortRange": "0-65535",
                                 "DestinationPortRange": "0-65535",
                                 "SourceAddressPrefix": "VirtualNetwork",
                                 "DestinationAddressPrefix": "VirtualNetwork",
                                 "ExpandedSourceAddressPrefix": [
                                  "10.9.0.0/16",
                                  "168.63.129.16/32",
                                  "10.0.0.0/16",
                                  "10.1.0.0/16"
                                  ],
                                 "ExpandedDestinationAddressPrefix": [
                                  "10.9.0.0/16",
                                  "168.63.129.16/32",
                                  "10.0.0.0/16",
                                  "10.1.0.0/16"
                                  ],
                                  "Access": "Allow",
                                  "Priority": 65000,
                                  "Direction": "Inbound"
                                  },…
                         ]
   
        NetworkSecurityGroup   : {
                                   "Id": 
                                 "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkSecurityGroups/Subnet1-NSG"
                                 }
        Association            : {
                                   "Subnet": {
                                     "Id": 
                                 "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/virtualNetworks/WestUS-VNet1/subnets/Subnet1"
                                 }
                                 }
        EffectiveSecurityRules : [
                                 {
                                "Name": "securityRules/denyRDP",
                                "Protocol": "Tcp",
                                "SourcePortRange": "0-65535",
                                "DestinationPortRange": "3389-3389",
                                "SourceAddressPrefix": "Internet",
                                "DestinationAddressPrefix": "0.0.0.0/0",
                                "ExpandedSourceAddressPrefix": [
                                   ... ],
                                "ExpandedDestinationAddressPrefix": [],
                                "Access": "Deny",
                                "Priority": 1000,
                                "Direction": "Inbound"
                                },
                                {
                                "Name": "defaultSecurityRules/AllowVnetInBound",
                                "Protocol": "All",
                                "SourcePortRange": "0-65535",
                                "DestinationPortRange": "0-65535",
                                "SourceAddressPrefix": "VirtualNetwork",
                                "DestinationAddressPrefix": "VirtualNetwork",
                                "ExpandedSourceAddressPrefix": [
                                "10.9.0.0/16",
                                "168.63.129.16/32",
                                "10.0.0.0/16",
                                "10.1.0.0/16"
                                ],
                                "ExpandedDestinationAddressPrefix": [
                                "10.9.0.0/16",
                                "168.63.129.16/32",
                                "10.0.0.0/16",
                                "10.1.0.0/16"
                                ],
                                "Access": "Allow",
                                "Priority": 65000,
                                "Direction": "Inbound"
                                },...
                                ]
   
    Let op de volgende informatie in de uitvoer van de Hallo Hallo:
   
   * Er zijn twee **NetworkSecurityGroup** secties: een is gekoppeld aan een subnet (*Subnet1*) en een is gekoppeld aan een NIC (*VM1 NIC1*). In dit voorbeeld is een NSG toegepaste tooeach.
   * **Koppeling** Hallo resource (subnet of NIC) ziet u een bepaalde NSG is gekoppeld. Als Hallo NSG-resource verplaatst/ontkoppeld is onmiddellijk voordat u deze opdracht uitvoert, moet u mogelijk toowait een paar seconden voor Hallo wijziging tooreflect in de opdrachtuitvoer Hallo. 
   * de namen van de regel die worden voorafgegaan door Hallo *defaultSecurityRules*: wanneer een NSG is gemaakt, verschillende standaard beveiligingsregels worden gemaakt binnen deze. Standaardregels kunnen niet worden verwijderd, maar kunnen ze met hogere prioriteitregels worden overschreven.
     Lees Hallo [NSG overzicht](virtual-networks-nsg.md#default-rules) toolearn artikel meer informatie over het NSG standaard beveiligingsregels voor verbindingen.
   * **ExpandedAddressPrefix** Hallo adresvoorvoegsels voor standaardtags NSG wordt uitgebreid. Labels vertegenwoordigen meerdere adresvoorvoegsels. Uitbreiding van Hallo labels kan nuttig zijn bij het oplossen van VM-connectiviteit van specifieke adresvoorvoegsels. Bijvoorbeeld, met een VNET-peering, VIRTUAL_NETWORK tag wordt uitgebreid tooshow VNet-voorvoegsels in de vorige uitvoer Hallo brengen.
     
     > [!NOTE]
     > Hallo alleen toont effectieve opdrachtregels als een NSG gekoppeld aan een subnet, een NIC of beide is. Een virtuele machine mogelijk meerdere NIC's met verschillende nsg's die zijn toegepast. Bij het oplossen van problemen Hallo-opdracht uitvoeren voor elke NIC.
     > 
     > 
3. tooease filteren via een groter aantal NSG-regels, Voer Hallo opdrachten tootroubleshoot verder te volgen: 
   
        $NSGs = Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
        $NSGs.EffectiveSecurityRules | Sort-Object Direction, Access, Priority | Out-GridView
   
    Een filter voor RDP-verkeer (TCP-poort 3389), is toegepast toohello rasterweergave, zoals wordt weergegeven in de volgende afbeelding Hallo:
   
    ![Lijst met regels](./media/virtual-network-nsg-troubleshoot-powershell/rules.png)
4. Zoals u in de rasterweergave hello ziet, er zijn beide toestaan en weigeren voor regels voor RDP. Hallo uitvoer uit stap 2 toont die Hallo *DenyRDP* regel in Hallo NSG toegepast toohello subnet is. Voor binnenkomende regels worden eerst toegepast nsg's toohello subnet verwerkt. Als een overeenkomst wordt gevonden, wordt Hallo NSG toegepast toohello-netwerkinterface niet verwerkt. In dit geval Hallo *DenyRDP* regel van Hallo subnet RDP toohello VM blokkeert (**VM1**).
   
   > [!NOTE]
   > Een virtuele machine kan meerdere NIC's aangesloten tooit hebben. Elk ander subnet verbonden tooa mogelijk. Aangezien het Hallo-opdrachten in de vorige stappen Hallo worden uitgevoerd op basis van een NIC, is het belangrijk tooensure die u opgeeft Hallo NIC die je hebt Hallo connectiviteit is mislukt. Als u niet zeker weet, kunt u kunt altijd Hallo opdrachten uitvoeren op elke NIC die is gekoppeld toohello VM.
   > 
   > 
5. tooRDP in VM1, wijziging Hallo *weigeren RDP (3389)* regel te*toestaan RDP(3389)* in Hallo **Subnet1 NSG** NSG. Controleer of de TCP-poort 3389 openen door het openen van een RDP-verbinding toohello VM of Hallo psping om het hulpprogramma is. U meer informatie over psping om door te lezen Hallo [psping om downloadpagina.](https://technet.microsoft.com/sysinternals/psping.aspx)
   
    U kunt regels of verwijderen uit een NSG met behulp van Hallo informatie in de uitvoer van de volgende opdracht Hallo Hallo:
   
        Get-Help *-AzureRmNetworkSecurityRuleConfig

## <a name="considerations"></a>Overwegingen
Overweeg de volgende punten bij het oplossen van problemen met de netwerkconnectiviteit Hallo:

* Standaard NSG-regels blokkeert binnenkomende toegang vanaf Hallo internet en alleen toestaan VNet binnenkomend verkeer. Regels moeten expliciet worden toegevoegd tooallow binnenkomende toegang via Internet, zoals vereist.
* Als er geen NSG beveiligingsregels voor verbindingen van een virtuele machine network connectivity toofail veroorzaakt, kan Hallo probleem worden veroorzaakt:
  * Firewall-software die binnen het besturingssysteem Hallo van de virtuele machine worden uitgevoerd
  * Routes die zijn geconfigureerd voor virtuele apparaten of lokale verkeer. Internet-verkeer kan worden omgeleid tooon-premises via geforceerde tunneling. Een RDP/SSH-verbinding van Hallo Internet tooyour VM werkt mogelijk niet met deze instelling kan, afhankelijk van hoe Hallo lokale netwerkhardware dit verkeer verwerkt. Lees Hallo [probleemoplossing Routes](virtual-network-routes-troubleshoot-powershell.md) artikel toolearn hoe toodiagnose route problemen die kunnen worden belemmeren Hallo verkeersstroom in en uit van Hallo VM. 
* Als u de VNets, standaard brengen hebt, vouw Hallo VIRTUAL_NETWORK tag automatisch tooinclude voorvoegsels voor VNets peer is ingesteld. U kunt deze voorvoegsels weergeven in Hallo **ExpandedAddressPrefix** lijst tootroubleshoot eventuele problemen gerelateerde tooVNet peering connectiviteit. 
* Effectieve beveiligingsregels worden alleen weergegeven als er is een NSG die is gekoppeld aan Hallo van de virtuele machine NIC en of subnet. 
* Als er geen nsg's die zijn gekoppeld aan Hallo NIC of subnet en u een openbaar IP-adres toegewezen tooyour VM hebt, is alle poorten zijn geopend voor inkomend en uitgaand verkeer. Als Hallo VM een openbaar IP-adres heeft, wordt het toepassen van nsg's toohello NIC of subnet sterk aanbevolen.  

