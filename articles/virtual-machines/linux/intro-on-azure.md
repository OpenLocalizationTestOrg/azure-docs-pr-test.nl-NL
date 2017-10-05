---
title: Inleiding tot Linux in Azure | Microsoft Docs
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
ms.openlocfilehash: 7bd0c5549a2e1f592681760d5ef464b9570ca4ab
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-linux-on-azure"></a>Inleiding tot Linux op Azure
Dit onderwerp bevat een overzicht van bepaalde aspecten van het gebruik van virtuele Linux-machines in de Azure-cloud. Implementatie van een virtuele Linux-machine is een eenvoudig proces met behulp van een afbeelding uit de galerie.

## <a name="authentication-usernames-passwords-and-ssh-keys"></a>Verificatie: Gebruikersnamen, wachtwoorden en SSH-sleutels
Wanneer u een virtuele Linux-machine met de Azure portal maakt, u wordt gevraagd te bieden beide een gebruikersnaam en wachtwoord of een openbare SSH-sleutel. De keuze van een gebruikersnaam voor het implementeren van een virtuele Linux-machine in Azure is onderworpen aan de volgende beperking: namen van systeemaccounts (UID < 100) die al aanwezig zijn in de virtuele machine zijn niet toegestaan, 'root' bijvoorbeeld.

* Zie [een virtuele Machine met Linux maken](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Zie [SSH gebruiken met Linux op Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="obtaining-superuser-privileges-using-sudo"></a>Het verkrijgen van supergebruiker bevoegdheden gebruiken`sudo`
Het gebruikersaccount dat is opgegeven tijdens de implementatie van de virtuele machine-exemplaar in Azure is een bevoegd account. Dit account is geconfigureerd door de Azure Linux Agent kunnen voor uitbreiding van bevoegdheden naar de hoofdmap (supergebruiker account) met behulp van de `sudo` hulpprogramma. Nadat u bent aangemeld met dit gebruikersaccount, kunt u zich kunnen opdrachten uit te voeren als de opdrachtsyntaxis hoofdmap:

    # sudo <COMMAND>

U kunt eventueel verkrijgen voor een basis-shell met **sudo -s**.

* Zie [hoofdmap bevoegdheden met op Linux virtuele machines in Azure](use-root-privileges.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="firewall-configuration"></a>Firewall-configuratie
Azure biedt een binnenkomend pakketfilter dat de verbinding wordt beperkt tot de poorten die zijn opgegeven in de Azure-portal. Standaard is de enige toegestane poort SSH. U kunt van toegang tot extra poorten openen op uw virtuele Linux-machine door het configureren van eindpunten in de Azure portal:

* Zie: [eindpunten aan een virtuele Machine instellen](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

De Linux-afbeeldingen in de galerie van Azure niet inschakelt de *iptables* firewall standaard. Indien gewenst, kan de firewall worden geconfigureerd om te bieden aanvullende filteren.

## <a name="hostname-changes"></a>Hostname wijzigingen
Wanneer u een exemplaar van een installatiekopie van Linux in eerste instantie implementeert, hoeft u de hostnaam van een voor de virtuele machine op te geven. Zodra de virtuele machine wordt uitgevoerd, wordt deze hostnaam is gepubliceerd op de DNS-servers van platform zodat meerdere virtuele machines met elkaar verbonden IP-adres zoekacties met behulp van hostnamen kunt uitvoeren.

Als de hostnaam wijzigingen aanbrengen wilt na de implementatie van een virtuele machine, gebruik de opdracht

    # sudo hostname <newname>

De Azure Linux Agent bevat een functie voor automatisch detecteren van deze wijziging en de virtuele machine voor deze wijziging behouden en deze wijziging publiceren naar de platform-DNS-servers op de juiste wijze configureren.

* [Gebruikershandleiding voor Azure Linux-Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="cloud-init"></a>Cloud-Init
**Ubuntu** en **virtuele CoreOS** installatiekopieën gebruikmaken van cloud-init op Azure meer mogelijkheden biedt voor het uitvoeren van een virtuele machine de bootstrap.

* [Het invoeren van aangepaste gegevens](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Aangepaste gegevens en Cloud-Init op Microsoft Azure](https://azure.microsoft.com/blog/2014/04/21/custom-data-and-cloud-init-on-windows-azure/)
* [Azure Swap-partities met behulp van Cloud-Init maken](https://wiki.ubuntu.com/AzureSwapPartitions)
* [Het gebruik van virtuele CoreOS op Azure](https://coreos.com/os/docs/latest/booting-on-azure.html)

## <a name="virtual-machine-image-capture"></a>Virtuele Machine installatiekopie vast te leggen
Azure biedt de mogelijkheid om vast te leggen van de status van een bestaande virtuele machine in een installatiekopie die kan vervolgens worden gebruikt voor het implementeren van extra virtuele machine-exemplaren. De Azure Linux Agent kan worden gebruikt voor het terugdraaien van een aantal van de aanpassingen die tijdens het inrichtingsproces is uitgevoerd. U mag de volgende stappen voor het vastleggen van een virtuele machine als een installatiekopie:

1. Voer **waagent-deprovision** aanpassing van de inrichting ongedaan te maken. Of **waagent-deprovision + user** eventueel het gebruikersaccount opgegeven tijdens de inrichting en alle gekoppelde gegevens verwijderen.
2. Omlaag/uitschakelen van de virtuele machine afgesloten.
3. Klik op **vastleggen** in de Azure-portal of gebruik PowerShell of CLI hulpprogramma's voor de virtuele machine als afbeelding vastleggen.
   
   * Zie: [het vastleggen van een virtuele Linux-Machine voor gebruik als een sjabloon](classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

## <a name="attaching-disks"></a>Schijven toevoegen
Elke virtuele machine is tijdelijk en lokale *resource schijf* gekoppeld. Omdat de gegevens op de schijf van een resource zijn mogelijk niet over herstarts duurzame, vaak wordt gebruikt door toepassingen en processen die worden uitgevoerd in de virtuele machine voor tijdelijke en **tijdelijke** opslag van gegevens. Dit wordt ook gebruikt voor het opslaan van de pagina of het wisselen van bestanden voor het besturingssysteem.

Op Linux, de resource-schijf is gewoonlijk beheerd door de Azure Linux Agent en automatisch gekoppeld aan **mnt/resourcegroep** (of **mnt** Ubuntu afbeeldingen).

> [!NOTE]
> Denk eraan dat de resource-schijf is een **tijdelijke** schijf, en die mogelijk worden verwijderd en opnieuw geformatteerd als de virtuele machine opnieuw is opgestart.
> 
> 

Op Linux de gegevensschijf kan worden met de naam van de kernel als `/dev/sdc`, en gebruikers moeten partitie formatteren en koppelen van die bron. Deze procedure wordt besproken in de zelfstudie stapsgewijze: [hoe een gegevensschijf koppelen aan een virtuele Machine](../windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

* **Zie ook:** [configureren van Software-RAID op Linux](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) & [LVM configureren op een virtuele Linux-machine in Azure](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

