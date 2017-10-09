---
title: aaaTesting SAP NetWeaver op Microsoft Azure SUSE Linux Virtual machines | Microsoft Docs
description: SAP NetWeaver testen op Microsoft Azure SUSE Linux VM's
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 645e358b-3ca1-4d3d-bf70-b0f287498d7a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: hermannd
ms.openlocfilehash: 0e3faab05417a1a15541e2b79aa7eddacda44611
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="running-sap-netweaver-on-microsoft-azure-suse-linux-vms"></a>SAP NetWeaver uitvoeren op Microsoft Azure SUSE Linux VM's
Dit artikel bevat verschillende dingen tooconsider wanneer u SAP NetWeaver op virtuele Microsoft Azure SUSE Linux-machines (VM's) uitvoert. SAP NetWeaver wordt vanaf mei 19 2016 officieel ondersteund in SUSE Linux virtuele machines in Azure. Alle gegevens met betrekking tot Linux-versies en versies van de kernel SAP vindt u in SAP-notitie 1928533 ' SAP-toepassingen in Azure: ondersteunde producten en Azure VM typen '.
Aanvullende documentatie over SAP op Linux VM's vindt u hier: [SAP op Linux virtuele machines (VM's) met behulp van](get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Hallo volgende informatie kunt u een aantal mogelijke valkuilen voorkomen.

## <a name="suse-images-on-azure-for-running-sap"></a>Installatiekopieën van SUSE op Azure voor het uitvoeren van SAP
Alleen SUSE Linux Enterprise Server SLES 12 (SPx) gebruiken voor het uitvoeren van SAP NetWeaver op Azure, - Zie ook SAP-notitie 1928533. De installatiekopie van een speciale SUSE in hello Azure Marketplace ('SLES 11 SP3 voor SAP CAL'), maar dit is niet bedoeld voor algemeen gebruik. Gebruik geen deze installatiekopie omdat deze bestemd voor Hallo [SAP-Cloudbibliotheek toestel](https://cal.sap.com/) oplossing.  

U moet Azure Resource Manager gebruiken voor alle nieuwe tests en installaties op Azure. toolook voor installatiekopieën van SUSE SLES en versies met Azure PowerShell of hello Azure-opdrachtregelinterface (CLI) gebruik Hallo opdrachten te volgen. Vervolgens kunt u Hallo uitvoer, bijvoorbeeld toodefine Hallo installatiekopie van het besturingssysteem in een JSON-sjabloon voor het implementeren van een nieuwe SUSE Linux VM.
Deze PowerShell-opdrachten zijn geldig voor Azure PowerShell-versie 1.0.1 of hoger.

Wanneer deze nog steeds mogelijk toouse Hallo standaard SLES installatiekopieën voor SAP-installaties is het beste toomake gebruik van nieuwe SLES Hallo voor SAP-installatiekopieën die beschikbaar zijn nu op Hallo Azure installatiekopie galerie. Meer informatie over deze installatiekopieën vindt u op het Hallo overeenkomt [Azure Marketplace pagina]( https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SUSE.SLES-SAP ) of Hallo [webpagina SUSE Veelgestelde vragen over SLES voor SAP]( https://www.suse.com/products/sles-for-sap/frequently-asked-questions/ ).


* Zoek naar de bestaande uitgevers, met inbegrip van SUSE:
  
   ```
   PS  : Get-AzureRmVMImagePublisher -Location "West Europe"  | where-object { $_.publishername -like "*US*"  }
   CLI : azure vm image list-publishers westeurope | grep "US"
   ```
* Zoeken naar bestaande aanbiedingen van SUSE:
  
   ```
   PS  : Get-AzureRmVMImageOffer -Location "West Europe" -Publisher "SUSE"
   CLI : azure vm image list-offers westeurope SUSE
   ```
* Zoek naar de offerings SUSE SLES:
  
   ```
   PS  : Get-AzureRmVMImageSku -Location "West Europe" -Publisher "SUSE" -Offer "SLES"
   PS  : Get-AzureRmVMImageSku -Location "West Europe" -Publisher "SUSE" -Offer "SLES-SAP"
   CLI : azure vm image list-skus westeurope SUSE SLES
   CLI : azure vm image list-skus westeurope SUSE SLES-SAP
   ```
* Zoek naar een specifieke versie van een SKU SLES:
  
   ```
   PS  : Get-AzureRmVMImage -Location "West Europe" -Publisher "SUSE" -Offer "SLES" -skus "12-SP2"
   PS  : Get-AzureRmVMImage -Location "West Europe" -Publisher "SUSE" -Offer "SLES-SAP" -skus "12-SP2"
   CLI : azure vm image list westeurope SUSE SLES 12-SP2
   CLI : azure vm image list westeurope SUSE SLES-SAP 12-SP2
   ```

## <a name="installing-walinuxagent-in-a-suse-vm"></a>WALinuxAgent installeren in een VM SUSE
Hallo agent WALinuxAgent aangeroepen maakt deel uit van Hallo SLES afbeeldingen in hello Azure Marketplace. Zie voor informatie over het installeren van deze handmatig (bijvoorbeeld tijdens het uploaden van een besturingssysteem SLES virtuele harde schijf (VHD) on-premises):

* [OpenSUSE](http://software.opensuse.org/package/WALinuxAgent)
* [Azure](../../linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [SUSE](https://www.suse.com/communities/blog/suse-linux-enterprise-server-configuration-for-windows-azure/)

## <a name="sap-enhanced-monitoring"></a>SAP 'uitgebreide bewaking'
SAP 'Verbeterde aan bewaking' is een verplichte vereisten toorun SAP op Azure. Controleer de details in SAP Houd er rekening mee 2191498 'SAP op Linux met Azure: verbeterde Monitoring'.

## <a name="attaching-azure-data-disks-tooan-azure-linux-vm"></a>Azure data schijven tooan Azure Linux VM koppelen
U moet nooit Azure gegevens schijven tooan Azure Linux VM koppelen met behulp van Hallo apparaat-ID. Gebruik in plaats daarvan (UUID) Hallo universally unique identifier. Wees voorzichtig wanneer u grafische hulpprogramma's toomount Azure gegevensschijven, bijvoorbeeld gebruiken. Controleer de vermeldingen in /etc/fstab Hallo.

probleem met de apparaat-ID Hallo Hallo is dat kan worden gewijzigd en vervolgens hello Azure VM in het opstartproces Hallo kan vastlopen. toomitigate hello probleem, kunt u Hallo nofail parameter toevoegen in /etc/fstab. Maar wees voorzichtig met nofail omdat toepassingen Hallo koppelpunt als voordat u kunnen gebruiken, en naar de Hallo root-bestandssysteem schrijven kunnen als een externe Azure-gegevensschijf tijdens het Hallo opstarten niet is gekoppeld.

Hallo enige uitzondering hierop toomounting via UUID is een besturingssysteemschijf voor het oplossen van problemen, zoals beschreven in de volgende sectie Hallo koppelen.

## <a name="troubleshooting-a-suse-vm-that-isnt-accessible-anymore"></a>Het oplossen van een SUSE VM die niet meer worden geopend
Mogelijk zijn er situaties waarin een SUSE VM op Azure reageert niet meer in het opstartproces hello (bijvoorbeeld met een fout met betrekking tot het koppelen van de schijven). U kunt dit probleem controleren via Hallo boot diagnostics functie voor Azure Virtual Machines v2 in hello Azure-portal. Zie voor meer informatie [opstarten diagnostics](https://azure.microsoft.com/blog/boot-diagnostics-for-virtual-machines-v2/).

Eenzijdige toosolve Hallo probleem is tooattach hello besturingssysteemschijf van Hallo beschadigd VM tooanother SUSE VM op Azure. Breng juiste wijzigingen zoals /etc/fstab bewerken of verwijderen van netwerk udev regels, zoals beschreven in de volgende sectie Hallo.

Er is een belangrijkste tooconsider. Implementeren van verschillende SUSE-virtuele machines van dezelfde Azure Marketplace-installatiekopie (bijvoorbeeld SLES 11 SP4) zorgt ervoor dat Hallo Hallo OS schijf tooalways worden gekoppeld door Hallo dezelfde UUID. Daarom kan het Hallo UUID tooattach een besturingssysteemschijf van een andere virtuele machine die is geïmplementeerd met behulp van dezelfde Azure Marketplace-installatiekopie in twee identieke UUID's resulteert Hallo gebruik. Deze problemen veroorzaakt en kan betekenen dat Hallo VM zijn alleen bedoeld voor het oplossen van problemen in feite vanaf Hallo gekoppeld opstarten wordt en beschadigde OS-schijf in plaats van de oorspronkelijke Hallo.

Er zijn twee manieren tooavoid dit:

* Gebruik een andere Azure Marketplace-installatiekopie voor Hallo probleemoplossing van de virtuele machine (bijvoorbeeld SLES 11 SPx in plaats van SLES 12).
* Hallo beschadigd OS-schijf niet koppelen vanuit een andere virtuele machine via UUID--gebruik iets anders.

## <a name="uploading-a-suse-vm-from-on-premises-tooazure"></a>Uploaden van een VM SUSE van lokale tooAzure
Zie voor een beschrijving van Hallo stappen tooupload een SUSE VM van lokale tooAzure [een SLES of openSUSE virtuele machine voorbereiden voor Azure](../../linux/suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Als u wilt dat een virtuele machine zonder Hallo deprovision stap aan Hallo einde (bijvoorbeeld tookeep een bestaande installatie van de SAP, evenals de hostnaam Hallo) tooupload, controleert u Hallo volgende items:

* Zorg ervoor dat Hallo OS-schijf is gekoppeld met behulp van UUID en niet Hallo apparaat-ID. Wijzigen van tooUUID alleen bij /etc/fstab is niet genoeg voor de besturingssysteemschijf Hallo. Bovendien Vergeet niet tooadapt Hallo opstartlaadprogramma via YaST of door /boot/grub/menu.lst te bewerken.
* Als u Hallo VHDX-indeling voor Hallo SUSE besturingssysteemschijf gebruiken en tooVHD converteren voor het uploaden van tooAzure, is het zeer waarschijnlijk dat Hallo-netwerkapparaat wordt gewijzigd van eth0 tooeth1. tooavoid problemen wanneer u later op Azure bent opgestart back tooeth0 wijzigen, zoals beschreven in [eth0 in hersteld gekloond SLES 11 VMware](https://dartron.wordpress.com/2013/09/27/fixing-eth1-in-cloned-sles-11-vmware/).

Bovendien van toowhat beschreven in artikel hello, is het raadzaam dat u dit verwijderen:

   /lib/udev/Rules.d/75-persistent-NET-generator.Rules

U kunt ook hello Azure Linux Agent (waagent) toohelp u potentiële problemen voorkomen installeren, zolang er meerdere NIC's zijn.

## <a name="deploying-a-suse-vm-on-azure"></a>Implementeren van een VM SUSE op Azure
U moet nieuwe SUSE virtuele machines maken met behulp van JSON-sjabloonbestanden in Hallo nieuwe Azure Resource Manager-model. Nadat Hallo JSON-sjabloonbestand is gemaakt, kunt u Hallo VM implementeren met behulp van Hallo CLI-opdracht als een alternatieve tooPowerShell te volgen:

   ```
   azure group deployment create "<deployment name>" -g "<resource group name>" --template-file "<../../filename.json>"

   ```
Zie voor meer informatie over de JSON-sjabloonbestanden [Azure Resource Manager-sjablonen samenstellen](../../../resource-group-authoring-templates.md) en [Azure-snelstartsjablonen](https://azure.microsoft.com/documentation/templates/).

Zie voor meer informatie over de CLI en Azure Resource Manager [gebruik hello Azure CLI voor Mac, Linux en Windows Azure Resource Manager](../../../xplat-cli-azure-resource-manager.md).

## <a name="sap-license-and-hardware-key"></a>SAP-licentie en hardware-sleutel
Hallo officiële SAP-Azure-certificering was een nieuw mechanisme geïntroduceerd toocalculate Hallo SAP hardwaresleutel die wordt gebruikt voor Hallo SAP-licentie. Hallo SAP kernel had toobe aangepast toomake gebruik hiervan. Eerdere versies van de SAP kernel voor Linux bevat geen deze code wijzigen. Daarom in bepaalde situaties (bijvoorbeeld Azure VM vergroten/verkleinen), Hallo SAP hardwaresleutel gewijzigd en Hallo SAP-licentie is niet langer geldig. Dit is opgelost in het meest recente SAP Linux kernels Hallo. Controleer de SAP-notitie 1928533 voor meer informatie.

## <a name="suse-sapconf-package--tuned-adm"></a>SUSE sapconf pakket / afgestemd adm
SUSE biedt een pakket genaamd 'sapconf', waarmee een reeks SAP-specifieke instellingen worden beheerd. Voor meer informatie over wat dit pakket komt en hoe tooinstall en deze gebruiken, Zie [sapconf tooprepare een SUSE Linux Enterprise Server toorun SAP-systemen met](https://www.suse.com/communities/blog/using-sapconf-to-prepare-suse-linux-enterprise-server-to-run-sap-systems/) en [wat is er sapconf of hoe tooprepare een SUSE Linux Enterprise Server voor het uitvoeren van SAP-systemen? ](http://scn.sap.com/community/linux/blog/2014/03/31/what-is-sapconf-or-how-to-prepare-a-suse-linux-enterprise-server-for-running-sap-systems).

In Hallo tussentijd is er een nieuw hulpprogramma die sapconf - afgestemd adm. vervangt Een vindt meer informatie over dit hulpprogramma Hallo twee koppelingen onderstaande te volgen.

SLES afgestemd adm profiel sap-hana kunt raadplegen voor informatie over [hier](https://www.suse.com/documentation/sles-for-sap-12/book_s4s/data/sec_s4s_configure_sapconf.html) 

Prestatieafstemming systemen voor SAP-werkbelastingen met afgestemd adm - vindt [hier](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/book_s4s/book_s4s.pdf) in hoofdstuk 6.2

## <a name="nfs-share-in-distributed-sap-installations"></a>NFS-sharemachtigingen in gedistribueerde SAP-installaties
Als er een gedistribueerde installatie--kunt bijvoorbeeld waar tooinstall Hallo database en SAP-toepassingsservers in afzonderlijke virtuele machines--Hallo u delen Hallo /sapmnt directory via Network File System (NFS). Als u problemen met de installatiestappen Hallo hebt nadat u de NFS-share voor /sapmnt Hallo hebt gemaakt, controleert u toosee als 'no_root_squash' hello share is ingesteld.

## <a name="logical-volumes"></a>Logische volumes
In de afgelopen Hallo desgewenst een een groot volume logische over meerdere Azure data-schijven (bijvoorbeeld voor Hallo SAP-database), is het raadzaam toouse mdadm lvm volledig nog niet is gevalideerd op Azure. hoe tooset up Linux RAID op Azure met behulp van mdadm, Zie toolearn [configureren van software-RAID op Linux](../../linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). In Hallo tussentijd vanaf het begin van mei 2016 ook lvm wordt volledig ondersteund in Azure en kan worden gebruikt als een alternatieve toomdadm. Zie voor aanvullende informatie met betrekking tot lvm op Azure [LVM configureren op een Linux VM in Azure](../../linux/configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="azure-suse-repository"></a>Azure SUSE opslagplaats
Als er een probleem met toegang toohello standaard Azure SUSE opslagplaats, kunt u een eenvoudige opdracht tooreset deze. Dit kan gebeuren als u een persoonlijke installatiekopie van het besturingssysteem in een Azure-regio en kopiëren Hallo installatiekopie tooa andere regio waar u toodeploy maakt nieuwe virtuele machines die zijn gebaseerd op deze persoonlijke installatiekopie van het besturingssysteem. Voert Hallo opdracht binnen Hallo VM te volgen:

   ```
   service guestregister restart
   ```

## <a name="gnome-desktop"></a>Gnome bureaublad
Als u wilt dat toouse hello Gnome bureaublad tooinstall een compleet SAP-demo systeem binnen een enkele VM--met inbegrip van een GUI SAP browser en SAP-beheerconsole--deze hint tooinstall gebruiken op Hallo Azure SLES installatiekopieën:

   Voor SLES 11:

   ```
   zypper in -t pattern gnome
   ```

   Voor SLES 12:

   ```
   zypper in -t pattern gnome-basic
   ```

## <a name="sap-support-for-oracle-on-linux-in-hello-cloud"></a>SAP-ondersteuning voor Oracle op Linux in Hallo cloud
Er is een beperking van de ondersteuning van Oracle op Linux in gevirtualiseerde omgevingen. Hoewel dit niet het onderwerp van een Azure-specifieke, is het belangrijk toounderstand. SAP biedt geen ondersteuning voor Oracle op SUSE of Red Hat in een openbare cloud zoals Azure. toodiscuss in dit onderwerp rechtstreeks contact opnemen met Oracle.

