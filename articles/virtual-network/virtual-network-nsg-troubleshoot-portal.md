---
title: aaaTroubleshoot Netwerkbeveiligingsgroepen - Portal | Microsoft Docs
description: Meer informatie over hoe tootroubleshoot Netwerkbeveiligingsgroepen in hello Azure Resource Manager deployment model hello Azure Portal gebruiken.
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: a54feccf-0123-4e49-a743-eb8d0bdd1ebc
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 0d3d2110fe1507f36e3b933de924a0876db2747a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-network-security-groups-using-hello-azure-portal"></a>Problemen met Netwerkbeveiligingsgroepen hello Azure Portal gebruiken
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

### <a name="vm"></a>Regels voor een effectieve beveiligingsmethode voor een virtuele machine weergeven
De volgende volledige Hallo stappen tootroubleshoot nsg's voor een virtuele machine:

U kunt de volledige lijst met Hallo effectieve beveiligingsregels voor verbindingen op een Netwerkinterfacekaart, van de virtuele machine zelf Hallo weergeven. U kunt ook toevoegen, wijzigen en verwijderen van zowel NIC en het subnetmasker NSG-regels Hallo effectieve regels blade als u deze bewerkingen tooperform machtigingen hebt.

1. Aanmelding toohello Azure-portal op https://portal.azure.com.
2. Klik op **meer services**, klikt u vervolgens op **virtuele machines** in Hallo lijst die wordt weergegeven.
3. Selecteer een VM-tootroubleshoot in Hallo lijst die wordt weergegeven en een VM-blade met opties wordt weergegeven.
4. Klik op **spoor & oplossen van problemen met** en selecteer vervolgens een veelvoorkomend probleem. In dit voorbeeld **ik kan geen verbinding maken toomy Windows VM** is geselecteerd. 
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image1.png)
5. Stappen worden vermeld onder Hallo probleem, zoals wordt weergegeven in de volgende afbeelding Hallo: 
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image2.png)
   
    Klik op *een effectieve beveiligingsmethode groep regels* in Hallo lijst met aanbevolen stappen.
6. Hallo **een effectieve beveiligingsmethode regels ophalen** blade wordt weergegeven, zoals wordt weergegeven in de volgende afbeelding Hallo:
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image3.png)
   
    U ziet Hallo uit te voeren van Hallo afbeelding:
   
   * **Bereik:** instellen te*VM1*, Hallo VM in stap 3 hebt geselecteerd.
   * **Netwerkinterface:** *VM1 NIC1* is geselecteerd. Een virtuele machine kan meerdere netwerkinterfaces (NIC) hebben. Elke NIC kan unieke effectieve Beveiligingsregels hebben. Wanneer het oplossen van problemen, moet u wellicht tooview Hallo effectieve beveiligingsregels voor elke NIC.
   * **Gekoppelde nsg's:** nsg's kunnen worden toegepast tooboth Hallo NIC en Hallo subnet Hallo NIC is verbonden met. Een NSG is in de afbeelding hello, toegepaste tooboth Hallo NIC en Hallo subnet die is verbonden met. U kunt klikken op Hallo NSG namen wijzigen toodirectly regels in Hallo nsg's.
   * **Tabblad VM1 nsg:** Hallo lijst met regels die worden weergegeven in afbeelding Hallo is voor Hallo NSG toohello NIC. toegepast Verschillende standaardregels worden gemaakt door Azure wanneer er een NSG wordt gemaakt. U kunt de standaardregels Hallo niet verwijderen, maar kunt u deze overschrijven met regels met een hogere prioriteit. meer informatie over standaardregels lezen Hallo toolearn [NSG overzicht](virtual-networks-nsg.md#default-rules) artikel.
   * **Doelkolom:** sommige Hallo regels tekst hebben in de kolom hello, terwijl anderen adresvoorvoegsels hebben. Hallo-tekst is Hallo-naam van de standaardregel labels toegepast toohello beveiliging wanneer deze is gemaakt. Hallo-tags zijn systeem-id's die meerdere voorvoegsels vertegenwoordigen. Selecteren van een regel met een label, zoals *AllowInternetOutBound*, een lijst met voorvoegsels in Hallo Hallo **adres voorvoegsels** blade.
   * **Download:** Hallo lijst met regels lang kan zijn. U kunt een CSV-bestand van Hallo regels voor offline-analyse downloaden door te klikken op **downloaden** en het Hallo-bestand op te slaan.
   * **AllowRDP** binnenkomende regel: met deze regel kunnen RDP-verbindingen toohello VM.
7. Klik op Hallo **Subnet1 NSG** tabblad tooview Hallo effectieve regels uit Hallo NSG toegepast toohello subnet, zoals wordt weergegeven in de volgende afbeelding Hallo: 
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image4.png)
   
    Kennisgeving Hallo *denyRDP* **inkomend** regel. Regels voor binnenkomende verbindingen op Hallo subnet toegepast worden geëvalueerd vóór regels toegepast op Hallo-netwerkinterface. Aangezien Hallo weigeren regel wordt toegepast op Hallo subnet, mislukt Hallo aanvraag tooconnect tooTCP 3389 omdat Hallo regel voor toestaan op Hallo NIC nooit wordt geëvalueerd. 
   
    Hallo *denyRDP* regel is Hallo reden waarom de Hallo RDP-verbinding is mislukt. Verwijdert, moet de Hallo probleem oplossen.
   
   > [!NOTE]
   > Als Hallo VM die is gekoppeld met Hallo NIC is niet actief is, of nsg's zijn niet toegepast toohello NIC of subnet, geen regels worden weergegeven.
   > 
   > 
8. tooedit NSG-regels, klik op *Subnet1 NSG* in Hallo **nsg's die zijn gekoppeld** sectie.
   Hiermee opent u Hallo **Subnet1 NSG** blade. U kunt rechtstreeks Hallo regels bewerken door te klikken op **inkomende beveiligingsregels**.
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image7.png)
9. Na het verwijderen van Hallo *denyRDP* inkomende hello-regel **Subnet1 NSG** en het toevoegen van een *allowRDP* regel, Hallo effectieve regels lijst ziet eruit als Hallo volgende afbeelding:
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image8.png)
   
    Controleer of de TCP-poort 3389 openen door het openen van een RDP-verbinding toohello VM of Hallo psping om het hulpprogramma is. U meer informatie over psping om door te lezen Hallo [psping om downloadpagina](https://technet.microsoft.com/sysinternals/psping.aspx).

### <a name="nic"></a>Regels voor een effectieve beveiligingsmethode voor een netwerkinterface weergeven
Als uw VM-netwerkverkeer wordt gebracht voor een specifieke NIC, kunt u een volledige lijst met Hallo effectieve regels voor Hallo NIC uit Hallo network interfaces context weergeven door Hallo volgende stappen uit te voeren:

1. Aanmelding toohello Azure-portal op https://portal.azure.com.
2. Klik op **meer services**, klikt u vervolgens op **netwerkinterfaces** in Hallo lijst die wordt weergegeven.
3. Selecteer een netwerkinterface. In de Hallo volgende afbeelding, een NIC met de naam *VM1 NIC1* is geselecteerd.
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image5.png)
   
    U ziet dat Hallo **bereik** toohello netwerkinterface geselecteerd is ingesteld. stap 6 van Hallo toolearn informatie over aanvullende informatie wordt weergegeven, Hallo lezen **nsg's oplossen voor een VM** sectie van dit artikel.
   
   > [!NOTE]
   > Als een NSG wordt verwijderd uit een netwerkinterface, Hallo subnet NSG is nog steeds een effectieve op Hallo gegeven NIC. In dit geval zou Hallo uitvoer alleen regels uit Hallo subnet NSG weergeven. Regels worden alleen weergegeven als Hallo NIC gekoppelde tooa VM.
   > 
   > 
4. U kunt rechtstreeks bewerken van regels voor het nsg's die zijn gekoppeld aan een NIC en een subnet. toolearn lezen hoe stap 8 van Hallo **effectieve beveiligingsregels voor een virtuele machine weergeven** sectie van dit artikel.

## <a name="nsg"></a>Een effectieve beveiligingsmethode regels weergeven voor een netwerkbeveiligingsgroep (NSG)
Bij het NSG-regels wijzigen, kunt u tooreview Hallo gevolgen van het Hallo-regels wordt toegevoegd aan een bepaalde virtuele machine. U kunt een volledige lijst met Hallo effectieve beveiligingsregels voor verbindingen weergeven voor alle Hallo NIC's die een bepaalde NSG wordt toegepast zonder tooswitch context uit Hallo NSG blade gegeven. tootroubleshoot effectieve regels binnen een NSG, volledige Hallo stappen te volgen:

1. Aanmelding toohello Azure-portal op https://portal.azure.com.
2. Klik op **meer services**, klikt u vervolgens op **Netwerkbeveiligingsgroepen** in Hallo lijst die wordt weergegeven.
3. Selecteer een NSG. In de Hallo volgende afbeelding, is een NSG VM1 nsg met de naam geselecteerd.
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image6.png)
   
    U ziet de volgende secties van de vorige afbeelding Hallo Hallo:
   
   * **Bereik:** toohello NSG geselecteerd ingesteld.
   * **Virtuele machine:** wanneer een NSG is toegepaste tooa subnet, toegepaste tooall interfaces gekoppelde tooall virtuele machines verbonden toohello netwerksubnet is. Deze lijst bevat alle virtuele machines die deze NSG wordt toegepast op. In de lijst Hallo kunt u een VM.
     
     > [!NOTE]
     > Als een NSG toegepaste tooonly een subnet leeg is, wordt de virtuele machines worden niet weergegeven. Als een NSG wordt toegepast tooa NIC die niet gekoppeld aan een virtuele machine is wordt die NIC's ook niet weergegeven. 
     > 
     > 
   * **Netwerkinterface:** een virtuele machine kan meerdere netwerkinterfaces hebben. Kunt u een netwerkinterface gekoppelde toohello VM geselecteerd.
   * **AssociatedNSGs:** op elk gewenst moment een NIC kan hebben up tootwo effectieve NSGs, één toohello NIC toegepast en andere subnet toohello Hallo. Hoewel het Hallo-bereik is geselecteerd als VM1-nsg als Hallo NIC een effectieve subnet NSG heeft, ziet Hallo uitvoer beide nsg's.
4. U kunt rechtstreeks bewerken van regels voor het nsg's die zijn gekoppeld aan een NIC of een subnet. toolearn lezen hoe stap 8 van Hallo **effectieve beveiligingsregels voor een virtuele machine weergeven** sectie van dit artikel.

stap 6 van Hallo toolearn informatie over aanvullende informatie wordt weergegeven, Hallo lezen **effectieve beveiligingsregels voor een virtuele machine weergeven** sectie van dit artikel.

> [!NOTE]
> Als een subnet en NIC elk slechts één NSG toegepast toothem hebben, wordt een NSG kan worden gekoppeld toomultiple NIC's en meerdere subnetten.
> 
> 

## <a name="considerations"></a>Overwegingen
Overweeg de volgende punten bij het oplossen van problemen met de netwerkconnectiviteit Hallo:

* Standaard NSG-regels blokkeert binnenkomende toegang vanaf Hallo internet en alleen toestaan VNet binnenkomend verkeer. Regels moeten expliciet worden toegevoegd tooallow binnenkomende toegang via Internet, zoals vereist.
* Als er geen NSG beveiligingsregels voor verbindingen van een virtuele machine network connectivity toofail veroorzaakt, kan Hallo probleem worden veroorzaakt:
  * Firewall-software die binnen het besturingssysteem Hallo van de virtuele machine worden uitgevoerd
  * Routes die zijn geconfigureerd voor virtuele apparaten of lokale verkeer. Internet-verkeer kan worden omgeleid tooon-premises via geforceerde tunneling. Een RDP/SSH-verbinding van Hallo Internet tooyour VM werkt mogelijk niet met deze instelling kan, afhankelijk van hoe Hallo lokale netwerkhardware dit verkeer verwerkt. Lees Hallo [probleemoplossing Routes](virtual-network-routes-troubleshoot-powershell.md) artikel toolearn hoe toodiagnose route problemen die kunnen worden belemmeren Hallo verkeersstroom in en uit van Hallo VM. 
* Als u de VNets, standaard brengen hebt, vouw Hallo VIRTUAL_NETWORK tag automatisch tooinclude voorvoegsels voor VNets peer is ingesteld. U kunt deze voorvoegsels weergeven in Hallo **ExpandedAddressPrefix** lijst tootroubleshoot eventuele problemen gerelateerde tooVNet peering connectiviteit. 
* Effectieve beveiligingsregels worden alleen weergegeven als er is een NSG die is gekoppeld aan Hallo van de virtuele machine NIC en of subnet. 
* Als er geen nsg's die zijn gekoppeld aan Hallo NIC of subnet en u een openbaar IP-adres toegewezen tooyour VM hebt, is alle poorten zijn geopend voor inkomend en uitgaand verkeer. Als Hallo VM een openbaar IP-adres heeft, wordt het toepassen van nsg's toohello NIC of subnet sterk aanbevolen.

