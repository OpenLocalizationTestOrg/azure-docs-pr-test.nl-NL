---
title: aaaAzure Site Recovery-ondersteuningsmatrix voor het repliceren van Azure tooAzure | Microsoft Docs
description: "Geeft een overzicht van Hallo ondersteunde besturingssystemen en configuraties voor de Azure Site Recovery-replicatie van de virtuele Azure-machines (VM's) van één regio tooanother voor disaster recovery (Noodherstel) nodig."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/10/2017
ms.author: sujayt
ms.openlocfilehash: 75b2451b4c2069ca4b11deb0efe1329d43879eb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-site-recovery-support-matrix-for-replicating-from-azure-tooazure"></a>Azure Site Recovery-ondersteuningsmatrix voor het repliceren van Azure tooAzure


>[!NOTE]
>
> Site Recovery replicatie voor virtuele machines in Azure is momenteel in preview.

In dit artikel bevat een overzicht van ondersteunde configuraties en -onderdelen voor Azure Site Recovery wanneer repliceren en herstellen van virtuele machines in Azure uit één regio tooanother regio.

## <a name="user-interface-options"></a>Opties voor de gebruikersinterface

**De gebruikersinterface** |  **Ondersteund / niet ondersteund**
--- | ---
**Azure Portal** | Ondersteund
**Klassieke portal** | Niet ondersteund
**PowerShell** | Momenteel niet ondersteund
**REST API** | Momenteel niet ondersteund
**CLI** | Momenteel niet ondersteund


## <a name="resource-move-support"></a>Ondersteuning voor het verplaatsen van resource

**Verplaatsen van brontype** | **Ondersteund / niet ondersteund** | **Opmerkingen**  
--- | --- | ---
**Kluis over brongroepen verplaatsen** | Niet ondersteund |U kunt Hallo Recovery services-kluis niet verplaatsen tussen resourcegroepen.
**Verplaatsen van Compute, Storage en het netwerk naar andere resourcegroepen** | Niet ondersteund |Als u een virtuele machine (of de bijbehorende onderdelen, zoals opslag en netwerk) verplaatst nadat de replicatie is ingeschakeld, u moet toodisable replicatie en replicatie inschakelen voor Hallo virtuele machine opnieuw.


## <a name="support-for-deployment-models"></a>Ondersteuning voor implementatiemodellen

**Implementatiemodel** | **Ondersteund / niet ondersteund** | **Opmerkingen**  
--- | --- | ---
**Klassiek** | Ondersteund | U kunt alleen een klassieke virtuele machine repliceren en deze herstellen als een klassieke virtuele machine. U kunt deze niet herstellen als de virtuele machine van een Resource Manager. Als u een klassieke virtuele machine zonder een virtueel netwerk en rechtstreeks tooan Azure-regio implementeert, wordt het niet ondersteund.
**Resource Manager** | Ondersteund |

## <a name="support-for-replicated-machine-os-versions"></a>Ondersteuning voor gerepliceerde machine OS-versies

Hallo hieronder ondersteuning geldt voor elke werkbelasting die wordt uitgevoerd op Hallo besturingssysteem vermeld.

#### <a name="windows"></a>Windows

- WindowsServer 2016 (Server Core en Server met Bureaubladbelevenis) *
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2 met op minste SP1

>[!NOTE]
>
> \*Windows Server 2016 Nano Server wordt niet ondersteund.

#### <a name="linux"></a>Linux

- Red Hat Enterprise Linux 6.7, 6,8, 7.0, 7.1, 7.2, 7.3
- CentOS 6.5 6.6, 6.7, 6,8, 7.0, 7.1, 7.2, 7.3
- Ubuntu 14.04 TNS Server [ (kernel-versies ondersteund)](#supported-ubuntu-kernel-versions-for-azure-virtual-machines)
- Ubuntu 16.04 TNS Server [ (kernel-versies ondersteund)](#supported-ubuntu-kernel-versions-for-azure-virtual-machines)
- Oracle Enterprise Linux 6.4, 6.5 met Hallo Red Hat compatibel kernel of Unbreakable Enterprise Kernel versie 3 (UEK3)
- SUSE Linux Enterprise Server 11 SP3

>[!NOTE]
>
> Ubuntu-servers met wachtwoord gebaseerde verificatie en aanmelding en Hallo cloud init pakket tooconfigure cloud virtuele machines gebruikt, kan hebben op basis van wachtwoorden aanmelding uitgeschakeld bij failover (afhankelijk van de Hallo cloudinit-configuratie.) Wachtwoord gebaseerde aanmelding kan worden opnieuw worden ingeschakeld op Hallo virtuele machine door opnieuw instellen van wachtwoord Hallo in Hallo instellingen (onder Hallo ondersteuning + gedeelte probleemoplossing) Hallo failover van virtuele machine op Hallo Azure-portal.

### <a name="supported-ubuntu-kernel-versions-for-azure-virtual-machines"></a>Ondersteunde versies van Ubuntu kernel voor Azure virtual machines

**Release** | **De versie van de Mobility-service** | **Kernelversie** |
--- | --- | --- |
14.04 TNS | 9.9 | 3.13.0-24-Generic too3.13.0-117-algemene<br/>3.16.0-25-Generic too3.16.0-77-algemene<br/>3.19.0-18-Generic too3.19.0-80-algemene<br/>4.2.0-18-Generic too4.2.0-42-algemene<br/>4.4.0-21-Generic too4.4.0-75-algemene |
14.04 TNS | 9.10 | 3.13.0-24-Generic too3.13.0-121-algemene<br/>3.16.0-25-Generic too3.16.0-77-algemene<br/>3.19.0-18-Generic too3.19.0-80-algemene<br/>4.2.0-18-Generic too4.2.0-42-algemene<br/>4.4.0-21-Generic too4.4.0-81-algemene |
16.04 TNS | 9.10 | 4.4.0-21-Generic too4.4.0-81-algemene<br/>4.8.0-34-Generic too4.8.0-56-algemene<br/>4.10.0-14-Generic too4.10.0-24-algemene |

## <a name="supported-file-systems-and-guest-storage-configurations-on-azure-virtual-machines-running-linux-os"></a>Ondersteunde bestandssystemen en Gast opslagconfiguraties op Azure virtuele machines met Linux-besturingssysteem

* -Bestandssystemen: ext3, ext4, ReiserFS (Suse Linux Enterprise Server alleen), XFS
* Volumebeheer: LVM2
* Multipath-software: apparaat toewijzen

## <a name="region-support"></a>Regio-ondersteuning

U kunt repliceren en herstellen van virtuele machines tussen twee gedeelten binnen Hallo hetzelfde geografische cluster.

**Geografische cluster** | **Azure-regio's**
-- | --
Amerika | Canada-Oost, Canada centraal, Zuid-centraal VS, West-Centraal VS, VS-Oost, VS-Oost 2, VS-West, VS-West 2, VS-midden, Noord-centraal VS
Europa | VK West, VK Zuid Noord-Europa, West-Europa
Azië | India Zuid, India centraal, Zuidoost-Azië Oost-Azië, Japan-Oost, Japan-West, Korea-midden, Zuid-Korea
Australië   | Australië-Oost, Australië-Zuidoost

>[!NOTE]
>
> Voor de regio Brazilië-Zuid, kunt u alleen repliceren en back-failover tooone Zuid-centraal VS, West-Centraal VS, VS-Oost, VS-Oost 2, VS-West, VS-West 2 Noordelijk Centraal, VS-regio's bevinden en mislukken.


## <a name="support-for-compute-configuration"></a>Ondersteuning voor Compute-configuratie

**Configuratie** | **Ondersteund/niet ondersteund** | **Opmerkingen**
--- | --- | ---
Grootte | Een Azure VM-grootte met ten minste 2 CPU-kernen en 1 GB RAM-geheugen | Raadpleeg te[grootten voor virtuele machine van Azure](../virtual-machines/windows/sizes.md)
Beschikbaarheidssets | Ondersteund | Als u de standaardoptie Hallo tijdens stap 'Replicatie inschakelen' in de portal gebruikt, is de beschikbaarheidsset Hallo automatisch gemaakt op basis van de configuratie van de regio. Kunt u Hallo doel beschikbaarheidsset voor ' gerepliceerde item > Instellingen > berekening en netwerk > beschikbaarheidsset ' elk gewenst moment.
Virtuele machines hybride gebruik voordeel (HUB) | Ondersteund | Als Hallo bron-VM HUB-licentie ingeschakeld heeft, Hallo testfailover of Failover VM gebruikt ook Hallo HUB licentie.
Virtuele-machineschaalsets | Niet ondersteund |
Azure-afbeeldingen - Microsoft gepubliceerd | Ondersteund | Ondersteund, zolang Hallo VM wordt uitgevoerd op een ondersteund besturingssysteem door Site Recovery
Installatiekopieën van galerie van Azure - gepubliceerd van derden | Ondersteund | Ondersteund, zolang Hallo VM wordt uitgevoerd op een ondersteund besturingssysteem door Site Recovery.
Aangepaste installatiekopieën - gepubliceerd van derden | Ondersteund | Ondersteund, zolang Hallo VM wordt uitgevoerd op een ondersteund besturingssysteem door Site Recovery.
Virtuele machines gemigreerd met behulp van Site Recovery | Ondersteund | Als het is een VMware of fysieke machine gemigreerd tooAzure met Site Recovery kunt u toouninstall Hallo oudere versie van de mobility-service nodig en Hallo machine opnieuw opstarten voordat het repliceren van tooanother Azure-regio.

## <a name="support-for-storage-configuration"></a>Ondersteuning voor opslagconfiguratie

**Configuratie** | **Ondersteund/niet ondersteund** | **Opmerkingen**
--- | --- | ---
Maximale grootte van de OS-schijven | 1023 GB | Raadpleeg te[schijven die worden gebruikt door virtuele machines.](../virtual-machines/windows/about-disks-and-vhds.md#disks-used-by-vms)
De grootte van maximaal gegevensschijf | 1023 GB | Raadpleeg te[schijven die worden gebruikt door virtuele machines.](../virtual-machines/windows/about-disks-and-vhds.md#disks-used-by-vms)
Aantal gegevensschijven | Maximaal 64 ondersteund door een specifieke Azure VM-grootte | Raadpleeg te[grootten voor virtuele machine van Azure](../virtual-machines/windows/sizes.md)
Tijdelijke schijf | Altijd uitgesloten van replicatie | Tijdelijke schijf is uitgesloten van replicatie altijd. Plaats geen permanente gegevens niet op de tijdelijke schijf aan de hand van Azure richtlijnen. Raadpleeg te[tijdelijke schijf op Azure Virtual machines](../virtual-machines/windows/about-disks-and-vhds.md#temporary-disk) voor meer informatie.
Gegevens wijzigen snelheid op Hallo schijf | Maximaal 6 MBps per schijf | Als snelheid Hallo gemiddelde gegevens wijzigen op Hallo schijf dan 6 MBps continu, replicatie wordt niet kan verwerken. Echter, als dit een ' burst ' in incidentele gegevens is en Hallo gegevenswijzigingssnelheid is groter dan 6 MBps enige tijd en ontvangt u omlaag, replicatie wordt lopen. In dit geval ziet u mogelijk enigszins vertraagd herstelpunten.
Schijven op standaard storage-accounts | Ondersteund |
Schijven op premium storage-accounts | Ondersteund | Als een virtuele machine schijven die zijn verdeeld over premium en standard storage-accounts bevat, kunt u een ander doelopslagaccount voor elke schijf tooensure hebt u dezelfde configuratie van de opslag in doelregio Hallo
Standaardschijven beheerd | Niet ondersteund |  
Premium-beheerde schijven | Niet ondersteund |
Opslagruimten | Ondersteund |         
Codering in rust (SSE) | Ondersteund | Voor de cache en het doel storage-accounts, kunt u een opslagaccount SSE ingeschakeld.     
Azure Disk Encryption (ADE) | Niet ondersteund |
Schijf hot toevoegen of verwijderen | Niet ondersteund | Als u toevoegen of verwijderen van de gegevensschijf op Hallo VM, u moet toodisable replicatie en replicatie opnieuw voor Hallo VM inschakelen.
Schijf uitsluiten | Niet ondersteund|   Tijdelijke schijf is niet standaard opgenomen.
LRS | Ondersteund |
GRS | Ondersteund |
RA-GRS | Ondersteund |
ZRS | Niet ondersteund |  
Cool en Hot Storage | Niet ondersteund | Schijven voor virtuele machine worden niet ondersteund op cool en hot storage

>[!IMPORTANT]
> Zorg ervoor dat u Hallo volgt [richtlijnen voor opslag](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) voor de bron van Azure virtual machines tooavoid eventuele prestatieproblemen. Als u de standaardinstellingen Hallo volgt, maakt Site Recovery Hallo vereist storage-accounts op basis van Hallo bron configuratie. Als u aanpassen en uw eigen instellingen selecteert, controleert u Hallo volgen (.. / storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) als de bron-VM's.

## <a name="support-for-network-configuration"></a>Ondersteuning voor netwerkconfiguratie
**Configuratie** | **Ondersteund/niet ondersteund** | **Opmerkingen**
--- | --- | ---
Netwerkinterface (NIC) | Een Resourcegroepnaam kunt u het maximum aantal NIC's ondersteund door een specifieke Azure VM-grootte | NIC's worden gemaakt wanneer Hallo VM is gemaakt als onderdeel van de testfailover of failover-bewerking. Hallo aantal NIC's op Hallo failover die VM, is afhankelijk van Hallo aantal NIC's Hallo bron die VM gelijktijdig Hallo heeft met het inschakelen van replicatie. Als u toevoegen/verwijderen NIC nadat de replicatie is ingeschakeld, geen NIC aantal op Hallo failover VM gevolgen.
Internet Load Balancer | Ondersteund | U moet tooassociate Hallo load balancer met een azure automatiseringsscript in een herstelplan vooraf is geconfigureerd.
Interne Load balancer | Ondersteund | U moet tooassociate Hallo load balancer met een azure automatiseringsscript in een herstelplan vooraf is geconfigureerd.
Openbare IP| Ondersteund | U moet een bestaand openbaar IP-toohello NIC tooassociate of maak een en toohello NIC met een azure automatiseringsscript in een plan voor herstel koppelt.
NSG op NIC (Resource Manager)| Ondersteund | U moet tooassociate hello NSG toohello NIC met een azure automatiseringsscript in een plan voor herstel.  
NSG voor subnet (Resource Manager en Classic)| Ondersteund | U moet tooassociate hello NSG toohello NIC met een azure automatiseringsscript in een plan voor herstel.
NSG op virtuele machine (klassiek)| Ondersteund | U moet tooassociate hello NSG toohello NIC met een azure automatiseringsscript in een plan voor herstel.
Gereserveerde IP-adres (statische IP) / behouden van de bron-IP | Ondersteund | Als Hallo NIC op Hallo bron-VM heeft statische IP-configuratie en het doelsubnet Hallo heeft dezelfde IP beschikbaar is, krijgt het toohello failover VM Hallo. Als Hallo Doelsubnet geen Hallo dezelfde IP beschikbaar is, een van de beschikbare IP-adressen in Hallo worden Hallo subnet is gereserveerd voor deze virtuele machine. U kunt opgeven dat een vaste IP-adres van uw keuze in ' gerepliceerde item > Instellingen > berekening en netwerk > netwerkinterfaces. U kunt selecteren Hallo NIC en geef Hallo subnet en IP-adres van uw keuze.
Dynamische IP| Ondersteund | Als Hallo NIC op Hallo bron-VM dynamische IP-configuratie heeft, hello NIC op Hallo failover VM is ook standaard dynamisch. U kunt opgeven dat een vaste IP-adres van uw keuze in ' gerepliceerde item > Instellingen > berekening en netwerk > netwerkinterfaces. U kunt selecteren Hallo NIC en geef Hallo subnet en IP-adres van uw keuze.
Traffic Manager-integratie | Ondersteund | U kunt uw traffic manager zodanig dat verkeer Hallo gerouteerde toohello eindpunt in de regio van de bron op een regelmatige basis en toohello eindpunt in doelregio in geval van een failover is vooraf configureren.
Azure DNS worden beheerd | Ondersteund |
Aangepaste DNS  | Ondersteund |    
Niet-geverifieerde Proxy | Ondersteund | Raadpleeg te[leidraad voor netwerken.](site-recovery-azure-to-azure-networking-guidance.md)    
Geverifieerde proxyserver | Niet ondersteund | Als Hallo VM van een geverifieerde proxyserver voor uitgaande verbinding gebruikmaakt, kan niet worden gerepliceerd met Azure Site Recovery.  
Site tooSite VPN met on-premises (met of zonder ExpressRoute)| Ondersteund | Zorg ervoor dat Hallo udr's en nsg's zijn geconfigureerd op zodanige wijze Hallo Site recovery-verkeer is geen gerouteerde tooon-premises. Raadpleeg te[leidraad voor netwerken.](site-recovery-azure-to-azure-networking-guidance.md)  
TooVNET-VNET-verbinding | Ondersteund | Raadpleeg te[leidraad voor netwerken.](site-recovery-azure-to-azure-networking-guidance.md)  


## <a name="next-steps"></a>Volgende stappen
- Meer informatie over [networking richtlijnen voor het repliceren van virtuele Azure-machines](site-recovery-azure-to-azure-networking-guidance.md)
- Beginnen met het beveiligen van uw werkbelastingen door [virtuele Azure-machines repliceren](site-recovery-azure-to-azure.md)
