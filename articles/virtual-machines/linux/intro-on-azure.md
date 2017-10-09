---
title: aaaIntroduction tooLinux in Azure | Microsoft Docs
description: Meer informatie over het gebruik van Linux virtuele machines in Azure.
services: virtual-machines-linux
documentationcenter: python
author: szarkos
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: b13bf305-87bf-4df3-815e-e8f6337aa6ea
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: szark
ms.openlocfilehash: 3a931447ee23ce7000174ca314c3e10abc6b8e74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toolinux-on-azure"></a>TooLinux inleiding op Azure
Dit onderwerp bevat een overzicht van bepaalde aspecten van het gebruik van virtuele Linux-machines in hello Azure-cloud. Implementatie van een virtuele Linux-machine is een eenvoudig proces met behulp van een afbeelding uit Hallo-galerie.

## <a name="authentication-usernames-passwords-and-ssh-keys"></a>Verificatie: Gebruikersnamen, wachtwoorden en SSH-sleutels
Bij het maken van een virtuele Linux-machine met behulp van Azure-portal Hallo tooprovide wordt u gevraagd ofwel een gebruikersnaam en wachtwoord of een openbare SSH-sleutel. Hallo keuze van een gebruikersnaam voor het implementeren van een virtuele Linux-machine in Azure is onderwerp toohello volgende beperking: namen van systeemaccounts (UID < 100) al aanwezig in Hallo virtuele machine zijn niet toegestaan, 'root' bijvoorbeeld.

* Zie [een virtuele Machine met Linux maken](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Zie [hoe tooUse SSH met Linux op Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="obtaining-superuser-privileges-using-sudo"></a>Het verkrijgen van supergebruiker bevoegdheden gebruiken`sudo`
Hallo-gebruikersaccount dat is opgegeven tijdens de implementatie van de virtuele machine-exemplaar in Azure is een bevoegd account. Dit account is geconfigureerd door hello Azure Linux Agent toobe kunnen tooelevate bevoegdheden tooroot (supergebruiker account) met behulp van Hallo `sudo` hulpprogramma. Nadat u bent aangemeld met dit gebruikersaccount, kunt u zich kunt toorun opdrachten als hoofdmap Hallo opdrachtsyntaxis:

    # sudo <COMMAND>

U kunt eventueel verkrijgen voor een basis-shell met **sudo -s**.

* Zie [hoofdmap bevoegdheden met op Linux virtuele machines in Azure](use-root-privileges.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="firewall-configuration"></a>Firewall-configuratie
Azure biedt een binnenkomend pakketfilter waarmee de connectiviteit tooports opgegeven in hello Azure-portal wordt beperkt. Hallo is alleen toegestane poort standaard SSH. U kunt de up tooadditional toegangspoorten op uw virtuele Linux-machine openen door eindpunten configureren in hello Azure-portal:

* Zie: [hoe tooSet Up eindpunten tooa virtuele Machine](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

Hallo Linux afbeeldingen in de galerie van Azure Hallo Hallo niet inschakelt *iptables* firewall standaard. Indien gewenst, Hallo firewall mogelijk worden geconfigureerd tooprovide extra filteren.

## <a name="hostname-changes"></a>Hostname wijzigingen
Wanneer u een exemplaar van een installatiekopie van Linux in eerste instantie implementeert, zijn vereiste tooprovide een hostnaam voor Hallo virtuele machine. Zodra Hallo virtuele machine wordt uitgevoerd, is deze hostnaam gepubliceerde toohello platform DNS-servers, zodat meerdere virtuele machines verbonden tooeach andere IP-adres zoekacties met behulp van hostnamen kunt uitvoeren.

Als de hostnaam wijzigingen aanbrengen wilt na de implementatie van een virtuele machine, gebruik de opdracht Hallo

    # sudo hostname <newname>

Hello Azure Linux Agent bevat functionaliteit tooautomatically deze naamswijziging detecteren en op de juiste wijze configureren Hallo virtuele machine toopersist deze wijziging en publiceren van deze wijziging toohello platform DNS-servers.

* [Gebruikershandleiding voor Azure Linux-Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="cloud-init"></a>Cloud-Init
**Ubuntu** en **virtuele CoreOS** installatiekopieën gebruikmaken van cloud-init op Azure meer mogelijkheden biedt voor het uitvoeren van een virtuele machine de bootstrap.

* [Hoe tooInject aangepaste gegevens](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Aangepaste gegevens en Cloud-Init op Microsoft Azure](https://azure.microsoft.com/blog/2014/04/21/custom-data-and-cloud-init-on-windows-azure/)
* [Azure Swap-partities met behulp van Cloud-Init maken](https://wiki.ubuntu.com/AzureSwapPartitions)
* [Hoe tooUse virtuele CoreOS op Azure](https://coreos.com/os/docs/latest/booting-on-azure.html)

## <a name="virtual-machine-image-capture"></a>Virtuele Machine installatiekopie vast te leggen
Azure biedt Hallo mogelijkheid toocapture Hallo status van een bestaande virtuele machine in een installatiekopie die u kunt vervolgens gebruikte toodeploy aanvullende VM-instanties worden. Hello Azure Linux Agent mogelijk gebruikte toorollback aantal Hallo aanpassing die tijdens het inrichtingsproces Hallo is uitgevoerd. U kunt stappen Hallo hieronder toocapture een virtuele machine als afbeelding:

1. Voer **waagent-deprovision** tooundo aanpassing inrichten. Of **waagent-deprovision + user** toooptionally Hallo-gebruikersaccount dat is opgegeven tijdens het inrichtingsproces en alle gekoppelde gegevens verwijderen.
2. Sluit omlaag/Hallo virtuele machine uitschakelen.
3. Klik op **vastleggen** in hello Azure portal of gebruik Hallo PowerShell of CLI hulpprogramma's voor toocapture Hallo virtuele machine als afbeelding.
   
   * Zie: [hoe tooCapture een virtuele Linux-Machine tooUse als sjabloon](classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

## <a name="attaching-disks"></a>Schijven toevoegen
Elke virtuele machine is tijdelijk en lokale *resource schijf* gekoppeld. Omdat de gegevens op de schijf van een resource zijn mogelijk niet over herstarts duurzame, vaak wordt gebruikt door toepassingen en processen die worden uitgevoerd in de virtuele machine Hallo voor tijdelijke en **tijdelijke** opslag van gegevens. Het is ook gebruikte toostore Hallo pagina of het swap-bestanden voor Hallo-besturingssysteem.

Op Linux, Hallo resource schijf is gewoonlijk beheerd door hello Azure Linux Agent en automatisch te worden gekoppeld**mnt/resourcegroep** (of **mnt** Ubuntu afbeeldingen).

> [!NOTE]
> Houd er rekening mee dat Hallo resource-schijf is een **tijdelijke** schijf, en die mogelijk worden verwijderd en opnieuw geformatteerd als hello VM opnieuw wordt opgestart.
> 
> 

Op Linux Hallo gegevensschijf kan worden genoemd door de kernel Hallo als `/dev/sdc`, en gebruikers moeten toopartition, indeling en koppel deze resource. Deze procedure wordt besproken in de zelfstudie Hallo stapsgewijze: [hoe tooAttach een gegevensschijf tooa virtuele Machine](../windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

* **Zie ook:** [configureren van Software-RAID op Linux](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) & [LVM configureren op een virtuele Linux-machine in Azure](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

