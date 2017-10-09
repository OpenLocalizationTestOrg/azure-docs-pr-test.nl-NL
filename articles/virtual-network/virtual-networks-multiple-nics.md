---
title: aaaCreate een VM (klassiek) met meerdere NIC's met behulp van PowerShell | Microsoft Docs
description: Meer informatie over hoe toocreate en configureren van virtuele machines met meerdere NIC's met behulp van PowerShell.
services: virtual-network, virtual-machines
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: a1a3952c-2dcc-4977-bd7a-52d623c1fb07
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: 8ef35bd4cfd7e6a527080f1cfc541275ca86f5e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics"></a>Een virtuele machine (klassiek) maken met meerdere NIC 's
U kunt virtuele machines (VM's) in Azure maken en koppelen van meerdere netwerkinterfaces (NIC's) van netwerk-tooeach van uw virtuele machines. Meerdere NIC's zijn vereist voor veel virtuele netwerkapparaten, zoals toepassingen en optimalisatie van WAN-oplossingen. Meerdere NIC's ook bieden isolatie van verkeer tussen NIC's.

![Multi-NIC voor VM](./media/virtual-networks-multiple-nics/IC757773.png)

Hallo afbeelding bevat een virtuele machine met drie NIC's, elk aangesloten tooa ander subnet.

> [!IMPORTANT]
> Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../resource-manager-deployment-model.md). In dit artikel wordt behandeld met het klassieke implementatiemodel Hallo. Microsoft raadt aan dat de meeste nieuwe implementaties Resource Manager gebruiken.

* Internetgerichte VIP (klassieke implementaties) wordt alleen ondersteund op Hallo 'standaard' NIC. Er is slechts één VIP toohello IP-adres van Hallo standaard NIC.
* Instance Level Public IP (LPIP)-adressen (klassieke implementaties) worden op dit moment niet ondersteund voor meerdere NIC virtuele machines.
* volgorde van Hallo NIC's van Hallo binnen Hallo VM wordt willekeurig en kan ook wijzigen via de Azure-infrastructuurupdates. Echter Hallo IP-adressen en bijbehorende ethernet MAC Hallo adressen blijft Hallo dezelfde. Stel **Eth1** heeft 10.1.0.100 van IP-adres en MAC-adres 00-0D-3A-B0-39-0D; na een Azure-infrastructuur bijwerken en opnieuw opstarten, deze kan worden gewijzigd te**Eth2**, maar Hallo IP- en MAC wordt koppelen blijven Hallo dezelfde. Wanneer een opnieuw opstarten de klant geïnitieerde is, Hallo NIC volgorde blijft Hallo dezelfde.
* Hallo-adres voor elke NIC op elke virtuele machine moet zich bevinden in een subnet, meerdere NIC's op één virtuele machine kunt elk worden toegewezen adressen die zich binnen hetzelfde subnet Hallo.
* Hallo VM-grootte bepaalt Hallo aantal NIC's die u voor een virtuele machine kunt maken. Verwijzing Hallo [Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) en [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) VM-groottes artikelen toodetermine hoeveel NIC's die ondersteuning biedt voor elke VM-grootte. 

## <a name="network-security-groups-nsgs"></a>Netwerkbeveiligingsgroepen (nsg's)
In de implementatie van een Resource Manager een NIC op een virtuele machine worden gekoppeld met een Netwerkbeveiligingsgroep (NSG), met inbegrip van een NIC's op een virtuele machine met meerdere NIC's die zijn ingeschakeld. Als een NIC een adres binnen een subnet waar Hallo subnet gekoppeld aan een NSG is is toegewezen, vervolgens toepassen hello regels in het Hallo-subnet NSG ook toothat NIC. In aanvulling tooassociating subnetten met nsg's, kunt u ook een NIC met een NSG koppelen.

Als een subnet is gekoppeld aan een NSG en een NIC in dat subnet afzonderlijk gekoppeld aan een NSG, Hallo gekoppeld NSG-regels worden toegepast in **stromen volgorde** volgens toohello-richting van het Hallo-verkeer wordt doorgegeven in of uit Hallo NIC:

* **Binnenkomend verkeer** eerst waarvan het doel is Hallo NIC in vraag loopt via Hallo subnet, activering Hallo-subnet NSG-regels voordat Hallo NIC passeren, en vervolgens activering Hallo NIC's NSG-regels.
* **Uitgaand verkeer** waarvan de gegevensbron is Hallo NIC betrokken loopt eerste out uit Hallo NIC, activering Hallo NIC's NSG-regels voordat Hallo subnet te doorlopen, en vervolgens activering Hallo-subnet NSG-regels.

Meer informatie over [Netwerkbeveiligingsgroepen](virtual-networks-nsg.md) en hoe ze worden toegepast op basis van koppelingen toosubnets, virtuele machines en NIC's...

## <a name="how-tooconfigure-a-multi-nic-vm-in-a-classic-deployment"></a>Hoe tooConfigure een multi-NIC VM in een klassieke implementatie
Hallo onderstaande instructies helpt u bij het maken van een multi-NIC VM 3 NIC's met: een standaard NIC en twee extra NIC's. Hallo configuratiestappen maakt u een virtuele machine die wordt geconfigureerd op basis van toohello service configuration file fragment hieronder:

    <VirtualNetworkSite name="MultiNIC-VNet" Location="North Europe">
    <AddressSpace>
      <AddressPrefix>10.1.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Frontend">
            <AddressPrefix>10.1.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Midtier">
            <AddressPrefix>10.1.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Backend">
            <AddressPrefix>10.1.2.0/23</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.1.200.0/28</AddressPrefix>
          </Subnet>
        </Subnets>
    … Skip over hello remainder section …
    </VirtualNetworkSite>


U moet Hallo vereisten voordat u probeert toorun Hallo PowerShell-opdrachten in Hallo voorbeeld te volgen.

* Een Azure-abonnement.
* Een geconfigureerde virtueel netwerk. Zie [Virtual Network-overzicht](virtual-networks-overview.md) voor meer informatie over VNets.
* meest recente versie van Azure PowerShell Hallo gedownload en geïnstalleerd. Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).

een virtuele machine met meerdere NIC's, volledige Hallo stappen te volgen met elke opdracht binnen één PowerShell-sessie toocreate:

1. Selecteer een VM-installatiekopie in Azure VM-installatiekopie galerie. Houd er rekening mee dat installatiekopieën regelmatig wordt gewijzigd en beschikbaar per regio zijn. Hallo opgegeven installatiekopie in Hallo in het volgende voorbeeld kan wijzigen of kan niet worden in uw regio, dus u moet de installatiekopie van toospecify Hallo.

    ```powershell
    $image = Get-AzureVMImage `
    -ImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201410.01-en.us-127GB.vhd"
    ```

2. Maak een VM-configuratie.

    ```powershell
    $vm = New-AzureVMConfig -Name "MultiNicVM" -InstanceSize "ExtraLarge" `
    -Image $image.ImageName –AvailabilitySetName "MyAVSet"
    ```

3. Hallo standaard beheerder aanmelding maken.

    ```powershell
    Add-AzureProvisioningConfig –VM $vm -Windows -AdminUserName "<YourAdminUID>" `
    -Password "<YourAdminPassword>"
    ```

4. Toevoegen van extra NIC's toohello VM-configuratie.

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name "Ethernet1" `
    -SubnetName "Midtier" -StaticVNetIPAddress "10.1.1.111" -VM $vm
    Add-AzureNetworkInterfaceConfig -Name "Ethernet2" `
    -SubnetName "Backend" -StaticVNetIPAddress "10.1.2.222" -VM $vm
    ```

5. Hallo-subnet en IP-adres opgeven voor Hallo standaard NIC.

    ```powershell
    Set-AzureSubnet -SubnetNames "Frontend" -VM $vm
    Set-AzureStaticVNetIP -IPAddress "10.1.0.100" -VM $vm
    ```

6. Hallo VM in het virtuele netwerk maken.

    ```powershell
    New-AzureVM -ServiceName "MultiNIC-CS" –VNetName "MultiNIC-VNet" –VMs $vm
    ```

    > [!NOTE]
    > Hallo VNet dat u hier opgeeft, moet al bestaan (zoals vermeld in Hallo vereisten). Hallo in het volgende voorbeeld bevat een virtueel netwerk met de naam **MultiNIC VNet**.
    >

## <a name="limitations"></a>Beperkingen
Hallo volgen beperkingen zijn van toepassing wanneer u meerdere NIC's:

* Virtuele machines met meerdere NIC's moeten worden gemaakt in Azure virtuele netwerken (vnet's). Niet-VNet-virtuele machines kan niet worden geconfigureerd met meerdere NIC's.
* Alle virtuele machines in een beschikbaarheidsset moet toouse ingesteld meerdere NIC's of een enkele netwerkinterfacekaart. Er kan niet een combinatie van meerdere virtuele machines NIC en één NIC-virtuele machines binnen een beschikbaarheidsset. Dezelfde regels gelden voor virtuele machines in een cloudservice. Voor meerdere virtuele machines NIC, ze niet nodig toohave Hallo hetzelfde aantal NIC's, zolang deze hebben elk een ten minste twee.
* Een virtuele machine met één NIC kan niet worden geconfigureerd met meerdere NIC's (en omgekeerd) zodra deze is geïmplementeerd, zonder te verwijderen en opnieuw te maken.

## <a name="secondary-nics-access-tooother-subnets"></a>Secundaire NIC's toegang tooother subnetten
Standaard secundaire NIC's worden niet geconfigureerd met een standaardgateway vanwege toowhich Hallo netwerkverkeer op Hallo secundaire NIC's worden beperkt toobe binnen Hallo hetzelfde subnet. Als gebruikers hello tooenable secundaire NIC's tootalk buiten hun eigen subnet wilt, moet ze tooadd een vermelding in Hallo tabel tooconfigure hello routeringsgateway als die hieronder worden beschreven.

> [!NOTE]
> Virtuele machines voordat juli 2015 mogelijk een standaardgateway geconfigureerd voor alle NIC's hebt gemaakt. Hallo standaardgateway voor secundaire NIC's wordt niet verwijderd totdat deze virtuele machines opnieuw worden gestart. Verbinding met Internet kunt in de besturingssystemen die gebruikmaken van het model, zoals Linux, in de Hallo zwakke host-routering verbreken als hello inkomende en uitgaande verkeer met verschillende NIC's.
> 

### <a name="configure-windows-vms"></a>Windows VM's configureren
Stel dat u een Windows-VM met twee NIC's als volgt:

* Primair NIC IP-adres: 192.168.1.4
* Secundaire NIC IP-adres: 192.168.2.5

Hallo IPv4 routetabel voor deze virtuele machine eruit als volgt:

    IPv4 Route Table
    ===========================================================================
    Active Routes:
    Network Destination        Netmask          Gateway       Interface  Metric
              0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
            127.0.0.0        255.0.0.0         On-link         127.0.0.1    306
            127.0.0.1  255.255.255.255         On-link         127.0.0.1    306
      127.255.255.255  255.255.255.255         On-link         127.0.0.1    306
        168.63.129.16  255.255.255.255      192.168.1.1      192.168.1.4      6
          192.168.1.0    255.255.255.0         On-link       192.168.1.4    261
          192.168.1.4  255.255.255.255         On-link       192.168.1.4    261
        192.168.1.255  255.255.255.255         On-link       192.168.1.4    261
          192.168.2.0    255.255.255.0         On-link       192.168.2.5    261
          192.168.2.5  255.255.255.255         On-link       192.168.2.5    261
        192.168.2.255  255.255.255.255         On-link       192.168.2.5    261
            224.0.0.0        240.0.0.0         On-link         127.0.0.1    306
            224.0.0.0        240.0.0.0         On-link       192.168.1.4    261
            224.0.0.0        240.0.0.0         On-link       192.168.2.5    261
      255.255.255.255  255.255.255.255         On-link         127.0.0.1    306
      255.255.255.255  255.255.255.255         On-link       192.168.1.4    261
      255.255.255.255  255.255.255.255         On-link       192.168.2.5    261
    ===========================================================================

U ziet dat standaardroute hello (0.0.0.0) is alleen beschikbaar toohello primaire NIC. U zich niet kunnen tooaccess bronnen buiten Hallo-subnet voor de secundaire Hallo NIC, zoals hieronder wordt weergegeven:

    C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5

    Pinging 192.168.1.7 from 192.165.2.5 with 32 bytes of data:
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.

tooadd een standaardroute op Hallo secundaire NIC, Hallo stappen hieronder:

1. Uitvoeren vanaf een opdrachtprompt Hallo onderstaande opdracht tooidentify Hallo indexnummer voor Hallo secundaire NIC:
   
        C:\Users\Administrator>route print
        ===========================================================================
        Interface List
         29...00 15 17 d9 b1 6d ......Microsoft Virtual Machine Bus Network Adapter #16
         27...00 15 17 d9 b1 41 ......Microsoft Virtual Machine Bus Network Adapter #14
          1...........................Software Loopback Interface 1
         14...00 00 00 00 00 00 00 e0 Teredo Tunneling Pseudo-Interface
         20...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
        ===========================================================================
2. Let op de tweede invoer Hallo op Hallo tabel, met een index van 27 (in dit voorbeeld).
3. Uitvoeren vanaf de opdrachtprompt Hallo Hallo **route toevoegen** opdracht zoals hieronder wordt weergegeven. In dit voorbeeld u 192.168.2.1 opgeeft als de standaardgateway Hallo voor Hallo secundaire NIC:
   
        route ADD -p 0.0.0.0 MASK 0.0.0.0 192.168.2.1 METRIC 5000 IF 27
4. tootest connectiviteit, toohello opdrachtprompt teruggaan en proberen van tooping een ander subnet van Hallo secundaire NIC als weergegeven int eh voorbeeld hieronder:
   
        C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5
   
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time=2ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
5. U kunt ook controleren dat uw route tabel toocheck Hallo toegevoegde route toe, zoals hieronder wordt weergegeven:
   
        C:\Users\Administrator>route print
   
        ...
   
        IPv4 Route Table
        ===========================================================================
        Active Routes:
        Network Destination        Netmask          Gateway       Interface  Metric
                  0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
                  0.0.0.0          0.0.0.0      192.168.2.1      192.168.2.5   5005
                127.0.0.0        255.0.0.0         On-link         127.0.0.1    306

### <a name="configure-linux-vms"></a>Linux-VM's configureren
Voor virtuele Linux-machines, omdat het standaardgedrag Hallo maakt gebruik van zwakke host routering, wordt geadviseerd om die Hallo secundaire NIC's zijn beperkt tootraffic stromen alleen binnen Hallo hetzelfde subnet. Echter als bepaalde scenario's voor connectiviteit buiten Hallo subnet, gebruikers moeten inschakelen op basis van beleid routering tooensure die Hallo toegangsroutes en uitgaande verkeer gebruikt Hallo dezelfde NIC.

## <a name="next-steps"></a>Volgende stappen
* Implementeer [MultiNIC virtuele machines in een scenario 2-tier-toepassing in een implementatie van Resource Manager](virtual-network-deploy-multinic-arm-template.md).
* Implementeer [MultiNIC virtuele machines in een scenario 2-tier-toepassing in een klassieke implementatie](virtual-network-deploy-multinic-classic-ps.md).

