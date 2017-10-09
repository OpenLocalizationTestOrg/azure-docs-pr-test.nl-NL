---
title: aaaOptimize VM netwerkdoorvoer | Microsoft Docs
description: Meer informatie over hoe toooptimize virtuele machine van Azure-netwerk doorvoer.
services: virtual-network
documentationcenter: na
author: steveesp
manager: Gerald DeGrace
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: steveesp
ms.openlocfilehash: a5cff2d0ab6e3553c3f90d99629521a431477de0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-network-throughput-for-azure-virtual-machines"></a>Netwerkdoorvoer voor Azure virtual machines optimaliseren

Azure virtuele machines (VM) hebben netwerk standaardinstellingen die verder kunnen worden geoptimaliseerd voor netwerkdoorvoer. Dit artikel wordt beschreven hoe toooptimize doorvoer netwerk voor Microsoft Azure Windows en Linux-virtuele machines, inclusief belangrijke distributies zoals Ubuntu en CentOS van Red Hat.

## <a name="windows-vm"></a>Windows VM

Als uw virtuele machine van Windows wordt ondersteund met [versnelde netwerken](virtual-network-create-vm-accelerated-networking.md), het inschakelen van deze functie zijn Hallo optimale configuratie voor de doorvoer. Met behulp van ontvangen Side Scaling (RSS) bereiken hogere maximale doorvoer dan een virtuele machine zonder RSS voor alle andere Windows-VM. RSS mogelijk in een virtuele machine van Windows standaard uitgeschakeld. Hallo toodetermine stappen te volgen of RSS is ingeschakeld en tooenable voltooien als deze uitgeschakeld.

1. Voer Hallo `Get-NetAdapterRss` PowerShell-opdracht toosee als de RSS is ingeschakeld voor een netwerkadapter. In Hallo volgende voorbeelduitvoer geretourneerd van Hallo `Get-NetAdapterRss`, RSS is niet ingeschakeld.

    ```powershell
    Name                    : Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : False
    ```
2. Voer Hallo opdracht tooenable RSS te volgen:

    ```powershell
    Get-NetAdapter | % {Enable-NetAdapterRss -Name $_.Name}
    ```
    vorige opdracht Hallo heeft geen uitvoer. Hallo opdracht NIC-instellingen, waardoor tijdelijke verbinding wordt verbroken voor ongeveer een minuut gewijzigd. Er verschijnt een dialoogvenster Reconnecting tijdens Hallo verbinding wordt verbroken. Verbinding is doorgaans hersteld na Hallo derde poging.
3. Controleer of RSS is ingeschakeld in Hallo VM hiertoe Hallo `Get-NetAdapterRss` opdracht opnieuw. Als dit lukt, wordt Hallo volgende voorbeelduitvoer geretourneerd:

    ```powershell
    Name                    :Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : True
    ```

## <a name="linux-vm"></a>Virtuele Linux-machine

RSS is altijd ingeschakeld in een Azure Linux VM standaard. Linux-kernels die zijn uitgebracht sinds januari 2017 nieuwe netwerk Optimalisatieopties opnemen waarmee u een Linux-VM tooachieve hogere netwerkdoorvoer.

### <a name="ubuntu"></a>Ubuntu

In de optimalisatie van bindingsvolgorde tooget Hallo, moet u eerst toohello ondersteund meest recente versie, vanaf juni 2017 die bijwerken:
```json
"Publisher": "Canonical",
"Offer": "UbuntuServer",
"Sku": "16.04-LTS",
"Version": "latest"
```
Nadat het Hallo-update is voltooid, voert u Hallo opdrachten tooget Hallo nieuwste kernel te volgen:

```bash
apt-get -f install
apt-get --fix-missing install
apt-get clean
apt-get -y update
apt-get -y upgrade
```

Optionele opdracht:

`apt-get -y dist-upgrade`
#### <a name="ubuntu-azure-preview-kernel"></a>Ubuntu Azure Preview-kernel
> [!WARNING]
> Deze Azure Linux Preview kernel heeft mogelijk geen Hallo hetzelfde niveau van beschikbaarheid en betrouwbaarheid als Marketplace-installatiekopieën en kernels die in het algemeen beschikbaarheid release. Hallo-functie wordt niet ondersteund, kan hebben beperkte mogelijkheden en zijn mogelijk niet zo betrouwbaar is als Hallo standaard kernel. Gebruik deze kernel niet voor productieworkloads.

De prestaties aanzienlijk doorvoer kan worden bereikt door hello Azure Linux kernel voorgestelde installeren. tootry deze kernel deze too/etc/apt/sources.list regel toevoegen

```bash
#add this toohello end of /etc/apt/sources.list (requires elevation)
deb http://archive.ubuntu.com/ubuntu/ xenial-proposed restricted main multiverse universe
```

Voer deze opdrachten als hoofdmap.
```bash
apt-get update
apt-get install "linux-azure"
reboot
```

### <a name="centos"></a>CentOS

In de optimalisatie van bindingsvolgorde tooget Hallo, moet u eerst toohello ondersteund meest recente versie, vanaf juli 2017 die bijwerken:
```json
"Publisher": "OpenLogic",
"Offer": "CentOS",
"Sku": "7.3",
"Version": "latest"
```
Nadat het Hallo-update is voltooid, Hallo installeren de nieuwste Linux Integration Services (LIS).
Hallo doorvoeroptimalistatietaak wordt LIS, vanaf 4.2.2-2. Voer Hallo opdrachten tooinstall LIS te volgen:

```bash
sudo yum update
sudo reboot
sudo yum install microsoft-hyper-v
```

### <a name="red-hat"></a>Red Hat

In de optimalisatie van bindingsvolgorde tooget Hallo, moet u eerst toohello ondersteund meest recente versie, vanaf juli 2017 die bijwerken:
```json
"Publisher": "RedHat"
"Offer": "RHEL"
"Sku": "7.3"
"Version": "7.3.2017071923"
```
Nadat het Hallo-update is voltooid, Hallo installeren de nieuwste Linux Integration Services (LIS).
Hallo doorvoeroptimalistatietaak wordt LIS, vanaf 4.2. Voer Hallo opdrachten toodownload te volgen en installeren van LIS:

```bash
mkdir lis4.2.2-2
cd lis4.2.2-2
wget https://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
tar xvzf lis-rpms-4.2.2-2.tar.gz
cd LISISO
install.sh #or upgrade.sh if prior LIS was previously installed
```

Meer informatie over Linux Integration Services versie 4.2 voor Hyper-V door het bekijken van Hallo [downloadpagina](https://www.microsoft.com/download/details.aspx?id=55106).

## <a name="next-steps"></a>Volgende stappen
* Nu hello VM geoptimaliseerd, gaat u naar Hallo resultaat [bandbreedte/doorvoer testen van de virtuele machine van Azure](virtual-network-bandwidth-testing.md) voor uw scenario.
* Klik hier als u meer wilt weten met [Azure Virtual Network Veelgestelde vragen (FAQ)](virtual-networks-faq.md)
