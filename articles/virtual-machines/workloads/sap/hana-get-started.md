---
title: 'Snelstartgids: Handmatige installatie van de single instance SAP HANA op Azure Virtual Machines | Microsoft Docs'
description: Snelstartgids voor handmatige installatie van de single instance SAP HANA op Azure Virtual Machines
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: c51a2a06-6e97-429b-a346-b433a785c9f0
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 09/15/2016
ms.author: hermannd
ms.openlocfilehash: 57b58b8e07379eed5641f5f89d55b38f52c69e44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-manual-installation-of-single-instance-sap-hana-on-azure-vms"></a>Snelstartgids: Handmatige installatie van de single instance SAP HANA op Azure Virtual machines
## <a name="introduction"></a>Inleiding
Deze handleiding helpt u Hiermee stelt u een single instance SAP HANA op Azure virtuele machines (VM's) wanneer u SAP NetWeaver 7.5 en SAP HANA 1.0 SP12 handmatig installeren. Deze handleiding Hallo richt zich op het implementeren van SAP HANA op Azure. Er is geen vervanging voor SAP-documentatie. 

>[!Note]
>Deze handleiding beschrijft de implementaties van SAP HANA in Azure Virtual machines. Zie voor meer informatie over het implementeren van SAP HANA in grote exemplaren HANA [SAP op Azure virtuele machines (VM's) met behulp van](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/get-started).
 
## <a name="prerequisites"></a>Vereisten
Deze handleiding wordt ervan uitgegaan dat u bekend met dergelijke infrastructuur als een dienst (IaaS) basisbeginselen als bent:
 * Hoe toodeploy virtuele machines of virtuele netwerken via hello Azure-portal of PowerShell.
 * Hello Azure platformoverschrijdende opdrachtregelinterface (CLI), waaronder Hallo optie toouse notatie JSON (JavaScript Object)-sjablonen.

Deze handleiding wordt ervan uitgegaan dat u bekend met bent:
* SAP HANA en SAP NetWeaver en hoe tooinstall ze lokaal.
* Installeren en besturingssysteem SAP HANA en SAP exemplaren van een toepassing in Azure.
* Hallo volgende concepten en procedures:
   * Planning voor SAP-implementatie op Azure, met inbegrip van Azure Virtual Network planning en gebruik van Azure Storage. Zie [SAP NetWeaver op Azure Virtual Machines (VM's) - handleiding voor Planning en implementatie](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/planning-guide).
   * Implementatie van de principes en manieren toodeploy virtuele machines in Azure. Zie [virtuele Machines van Azure-implementatie voor SAP](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/deployment-guide).
   * Hoge beschikbaarheid voor SAP NetWeaver ASC's (ABAP SAP centrale Services), SCS (SAP centrale Services) en Ebruikers (geëvalueerd ontvangst regeling) in Azure. Zie [hoge beschikbaarheid voor SAP NetWeaver op Azure Virtual machines](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide).
   * Meer informatie over het tooimprove efficiëntie bij gebruik van een multi-SID-installatie van ASC's / SCS op Azure. Zie [maken van een configuratie van de multi-SID SAP NetWeaver](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-multi-sid). 
   * Principes van actieve SAP NetWeaver gebaseerd op Linux gebaseerde virtuele machines in Azure. Zie [SAP NetWeaver uitgevoerd op Microsoft Azure SUSE Linux VM's](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/suse-quickstart). Deze handleiding bevat de specifieke instellingen voor Linux in Azure VM's en de details op hoe tooproperly koppelen aan Azure storage schijven tooLinux virtuele machines.

Op dit moment worden Azure Virtual machines gecertificeerd door SAP voor SAP HANA scale-up alleen configuraties. Scale-out configuraties met SAP HANA-werkbelastingen zijn nog niet ondersteund. Zie voor SAP HANA hoge beschikbaarheid in geval van een scale-up-configuraties, [hoge beschikbaarheid van SAP HANA op Azure virtuele machines (VM's)](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-high-availability).

Als u tooget zoekt een SAP HANA-exemplaar of S/4HANA of BW/4HANA system zeer snel tijdig worden geïmplementeerd, kunt u overwegen gebruik Hallo van [SAP-Cloudbibliotheek toestel](http://cal.sap.com). Vindt u documentatie over het implementeren, bijvoorbeeld een systeem S/4HANA via SAP CAL op Azure in [in deze handleiding](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/cal-s4h). U hoeft alleen toohave is een Azure-abonnement en een SAP-gebruiker die kan worden geregistreerd met SAP-Cloudbibliotheek toestel.

## <a name="additional-resources"></a>Aanvullende bronnen
### <a name="sap-hana-backup"></a>SAP HANA back-up
Zie voor informatie over back-ups SAP HANA-databases op Azure Virtual machines:
* [Back-handleiding voor SAP HANA op Azure Virtual Machines](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-backup-guide)
* [SAP HANA Azure back-up op bestandsniveau](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-backup-file-level)
* [SAP HANA-back-up op basis van opslag-momentopnamen](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-backup-storage-snapshots)

### <a name="sap-cloud-appliance-library"></a>SAP-Cloudbibliotheek toestel
Zie voor meer informatie over het gebruik van SAP-Cloudbibliotheek toestel toodeploy S/4HANA of BW/4HANA [implementeren SAP S/4HANA of BW/4HANA in Microsoft Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/cal-s4h).

### <a name="sap-hana-supported-operating-systems"></a>SAP HANA-ondersteunde besturingssystemen.
Zie voor informatie over SAP HANA-ondersteunde besturingssystemen, [SAP ondersteuning Opmerking #2235581 - SAP HANA: ondersteunde besturingssystemen](https://launchpad.support.sap.com/#/notes/2235581/E). Virtuele machines in Azure ondersteunen slechts een subset van deze besturingssystemen. Hallo volgende besturingssystemen worden ondersteund toodeploy SAP HANA op Azure: 

* SUSE Linux Enterprise Server 12.x
* Red Hat Enterprise Linux 7.2

Zie voor aanvullende SAP-documentatie over SAP HANA en verschillende Linux-besturingssystemen:

* [SAP ondersteuning Opmerking #171356 - SAP-Software op Linux: algemene informatie](https://launchpad.support.sap.com/#/notes/1984787)
* [SAP-notitie ondersteuning #1944799 - richtlijnen voor SAP HANA SLES voor installatie van besturingssysteem](http://go.sap.com/documents/2016/05/e8705aae-717c-0010-82c7-eda71af511fa.html)
* [SAP ondersteuning Opmerking #2205917 - SAP HANA DB aanbevolen OS-instellingen voor SLES 12 voor SAP-toepassingen](https://launchpad.support.sap.com/#/notes/2205917/E)
* [SAP ondersteuning Opmerking #1984787 - SUSE Linux Enterprise Server 12: Opmerkingen bij de installatie van de](https://launchpad.support.sap.com/#/notes/1984787)
* [SAP ondersteuning Opmerking #1391070 - oplossingen voor Linux-UUID](https://launchpad.support.sap.com/#/notes/1391070)
* [SAP-notitie ondersteuning #2009879 - SAP HANA richtlijnen voor het Red Hat Enterprise Linux (RHEL)-besturingssysteem](https://launchpad.support.sap.com/#/notes/2009879)
* [2292690 - SAP HANA-database: OS aanbevolen instellingen voor RHEL 7](https://launchpad.support.sap.com/#/notes/2292690/E)

### <a name="sap-monitoring-in-azure"></a>SAP bewaken in Azure
Zie voor informatie over SAP bewaken in Azure:

* [SAP-notitie 2191498](https://launchpad.support.sap.com/#/notes/2191498/E). Deze opmerking wordt besproken SAP 'uitgebreide bewaking' met een virtuele Linux-machines in Azure. 
* [SAP-notitie 1102124](https://launchpad.support.sap.com/#/notes/1102124/E). Deze opmerking vindt u informatie over SAPOSCOL op Linux. 
* [SAP-notitie 2178632](https://launchpad.support.sap.com/#/notes/2178632/E). Deze opmerking wordt belangrijkste bewaking metrische gegevens voor SAP beschreven in Microsoft Azure.

### <a name="azure-vm-types"></a>Azure VM-typen
Azure VM-typen en werkbelasting SAP-ondersteunde scenario's gebruikt met SAP HANA worden beschreven in [SAP gecertificeerd IaaS Platforms](https://www.sap.com/dmc/exp/2014-09-02-hana-hardware/enEN/iaas.html). 

Azure VM-typen die zijn gecertificeerd door SAP voor SAP NetWeaver of S/4HANA toepassingslaag Hallo zijn gedocumenteerd in [SAP-notitie 1928533 - SAP-toepassingen in Azure: typen ondersteunde producten en de virtuele machine van Azure](https://launchpad.support.sap.com/#/notes/1928533/E).

>[!Note]
>SAP-Linux-Azure-integratie wordt alleen ondersteund op Azure Resource Manager en niet Hallo-klassieke implementatiemodel. 

## <a name="manual-installation-of-sap-hana"></a>Handmatige installatie van het SAP HANA
Deze handleiding wordt beschreven hoe toomanually SAP HANA op Azure VM's op twee verschillende manieren installeren:

* Met behulp van SAP Software inrichting Manager (SWPM) als onderdeel van een gedistribueerde installatie NetWeaver in Hallo 'database-exemplaar installeren' stap
* Met behulp van Hallo SAP HANA-database lifecycle manager hulpprogramma HDBLCM en vervolgens NetWeaver te installeren

U kunt ook gebruiken SWPM tooinstall alle onderdelen (SAP HANA Hallo SAP-toepassingsserver en Hallo ASC's exemplaar) in één enkele virtuele machine, zoals beschreven in dit [SAP HANA-blog aankondiging](https://blogs.saphana.com/2013/12/31/announcement-sap-hana-and-sap-netweaver-as-abap-deployed-on-one-server-is-generally-available/). Deze optie wordt niet beschreven in deze snelstartgids, maar de problemen die u in aanmerking moet nemen zijn Hallo Hallo dezelfde.

Voordat u een installatie start, raden we aan dat u Hallo leest ' voorbereiden Azure VM's voor handmatige installatie van het SAP HANA ' verderop in deze handleiding. In dat geval kan u helpen voorkomen van verschillende algemene fouten die optreden mogelijk wanneer u alleen een standaard Azure VM-configuratie gebruiken.

## <a name="key-steps-for-sap-hana-installation-when-you-use-sap-swpm"></a>Belangrijke stappen voor SAP HANA-installatie wanneer u SAP SWPM
Deze sectie vindt belangrijke stappen voor de installatie van een handmatige, single instance SAP HANA Hallo wanneer u SAP SWPM tooperform een gedistribueerde SAP NetWeaver 7.5 installatie gebruiken. Hallo afzonderlijke stappen worden in meer detail in schermopnamen verderop in deze handleiding beschreven.

1. Maak een Azure-netwerk met twee test-virtuele machines.
2. Hallo twee virtuele Azure-machines met besturingssystemen (in ons voorbeeld SUSE Linux Enterprise Server (SLES) en SLES voor SAP-toepassingen 12 SP1), implementeren op basis van toohello Azure Resource Manager-model.
3. Twee Azure standard of premium-schijven (bijvoorbeeld 75 GB of 500 GB schijven) toohello toepassing opslagserver VM koppelen.
4. Premium-opslag schijven toohello HANA DB server VM koppelen. Zie sectie van de Hallo 'Disk setup' verderop in deze handleiding voor meer informatie.
5. Afhankelijk van de vereisten voor de grootte of doorvoer, meerdere schijven koppelen en vervolgens striped volumes maken met behulp van logische volumebeheer of een beheerprogramma voor meerdere apparaten (MDADM) op Hallo OS niveau binnen Hallo VM.
6. XFS bestandssystemen op Hallo gekoppelde schijven of logische volumes maken.
7. Koppel Hallo nieuwe XFS bestandssystemen op Hallo OS-niveau. Een bestandssysteem wordt gebruikt voor alle Hallo SAP-software. Gebruik bijvoorbeeld Hallo van andere bestandssysteem voor Hallo /sapmnt directory en back-ups. Koppel Hallo XFS bestandssystemen op Hallo premium-opslag-schijven als /hana en /usr/sap op Hallo SAP HANA-database-server. Dit proces is de benodigde tooprevent Hallo hoofdmap bestandssysteem, die geen grote op Linux Azure Virtual machines, wordt gevuld.
8. Voer Hallo lokale IP-adressen van Hallo test VM's in Hallo/etc/hosts-bestand.
9. Voer Hallo **nofail** parameter in Hallo/etc/fstab-bestand.
10. Stel Linux kernel parameters volgens toohello Linux-besturingssysteem versie die u gebruikt. Zie het juiste SAP opmerkingen hello, die HANA en Hallo 'Kernel parameters'-sectie in deze handleiding bespreken voor meer informatie.
11. Voeg wisselruimte toe.
12. Installeer eventueel een grafische bureaublad op Hallo test VM's. Anders gebruikt u een installatie op afstand SAPinst.
13. Hallo SAP-software downloaden van Hallo SAP Service Marketplace.
14. Hallo ASC's SAP-exemplaar installeren op Hallo appserver VM.
15. Share Hallo /sapmnt directory tussen Hallo testen virtuele machines met behulp van NFS. Hallo-toepassingsserver VM is Hallo NFS-server.
16. Hallo database-exemplaar, met inbegrip van HANA, met behulp van SWPM op Hallo databaseserver VM installeren.
17. Server van de primaire toepassing hello (Pa's) op Hallo-toepassingsserver VM installeren.
18. Start SAP Management Console (SAP MV). Verbinding met SAP-GUI of HANA Studio, bijvoorbeeld.

## <a name="key-steps-for-sap-hana-installation-when-you-use-hdblcm"></a>Belangrijke stappen voor SAP HANA-installatie, wanneer u HDBLCM
Deze sectie vindt belangrijke stappen voor de installatie van een handmatige, single instance SAP HANA Hallo wanneer u SAP HDBLCM tooperform een gedistribueerde SAP NetWeaver 7.5 installatie gebruiken. Hallo afzonderlijke stappen worden in meer detail in schermopnamen in deze handleiding beschreven.

1. Maak een Azure-netwerk met twee test-virtuele machines.
2. Twee Azure VM's met besturingssystemen (in ons voorbeeld SLES en SLES voor SAP-toepassingen 12 SP1) implementeren volgens toohello Azure Resource Manager-model.
3. Twee Azure standard of premium-schijven (bijvoorbeeld 75 GB of 500 GB schijven) toohello app opslagserver VM koppelen.
4. Premium-opslag schijven toohello HANA DB server VM koppelen. Zie sectie van de Hallo 'Disk setup' verderop in deze handleiding voor meer informatie.
5. Afhankelijk van de vereisten voor de grootte of doorvoer, koppel meerdere schijven en striped volumes maken met behulp van logische volumebeheer of een beheerprogramma voor meerdere apparaten (MDADM) op Hallo OS niveau binnen Hallo VM.
6. XFS bestandssystemen op Hallo gekoppelde schijven of logische volumes maken.
7. Koppel Hallo nieuwe XFS bestandssystemen op Hallo OS-niveau. Gebruik een bestandssysteem voor alle Hallo SAP-software en gebruik Hallo andere één voor Hallo /sapmnt directory en back-ups, bijvoorbeeld. Koppel Hallo XFS bestandssystemen op Hallo premium-opslag-schijven als /hana en /usr/sap op Hallo SAP HANA-database-server. U hoeft dit proces toohelp te voorkomen dat Hallo hoofdmap bestandssysteem dat niet groot op Linux Azure Virtual machines, wordt gevuld.
8. Voer Hallo lokale IP-adressen van Hallo test VM's in Hallo/etc/hosts-bestand.
9. Voer Hallo **nofail** parameter in Hallo/etc/fstab-bestand.
10. Stel kernel parameters volgens toohello Linux-besturingssysteem versie die u gebruikt. Zie het juiste SAP opmerkingen hello, die HANA en Hallo 'Kernel parameters'-sectie in deze handleiding bespreken voor meer informatie.
11. Voeg wisselruimte toe.
12. Installeer eventueel een grafische bureaublad op Hallo test VM's. Anders gebruikt u een installatie op afstand SAPinst.
13. Hallo SAP-software downloaden van Hallo SAP Service Marketplace.
14. Maak een groep, sapsys, met groep-ID 1001 op Hallo HANA DB server VM.
15. SAP HANA op Hallo DB server VM installeren met behulp van HANA Database Lifecycle Manager (HDBLCM).
16. Hallo ASC's SAP-exemplaar installeren op Hallo appserver VM.
17. Share Hallo /sapmnt directory tussen Hallo testen virtuele machines met behulp van NFS. Hallo-toepassingsserver VM is Hallo NFS-server.
18. Hallo-database-exemplaar, met inbegrip van HANA, met behulp van SWPM op Hallo HANA databaseserver VM installeren.
19. Server van de primaire toepassing hello (Pa's) op Hallo-toepassingsserver VM installeren.
20. SAP MV starten. Verbinding maken via SAP-GUI of HANA Studio.

## <a name="preparing-azure-vms-for-a-manual-installation-of-sap-hana"></a>Azure Virtual machines voorbereiden voor een handmatige installatie van de SAP HANA
Deze sectie bevat de volgende onderwerpen Hallo:

* Updates voor het besturingssysteem
* Installatie van de schijf
* Kernel-parameters
* Bestandssystemen
* Hallo/etc/hosts-bestand
* Hallo bestand/etc/fstab-fouten

### <a name="os-updates"></a>Updates voor het besturingssysteem
Controle voor Linux OS-updates en oplossingen voordat u extra software installeert. Door het installeren van een patch mogelijk kunnen tooavoid een aanroep van toohello de helpdesk.

Zorg ervoor dat u gebruikt:
* SUSE Linux Enterprise Server voor SAP-toepassingen.
* Red Hat Enterprise Linux voor SAP-toepassingen of Red Hat Enterprise Linux voor SAP HANA. 

Als u nog niet gedaan hebt, registreren Hallo implementatie van een besturingssysteem met uw abonnement Linux van Hallo Linux leverancier. Houd er rekening mee dat SUSE heeft installatiekopieën van het besturingssysteem voor SAP-toepassingen die al services bevatten en die automatisch worden geregistreerd.

Hier volgt een voorbeeld van het controleren op beschikbare patches voor SUSE Linux via Hallo **zypper** opdracht:

 `sudo zypper list-patches`

Patches zijn afhankelijk van Hallo soort probleem geclassificeerd op categorie en ernst. Veelgebruikte waarden voor de categorie zijn: **beveiliging**, **aanbevolen**, **optionele**, **functie**, **document**, of **yast**.
Veelgebruikte waarden voor ernst zijn: **kritieke**, **belangrijke**, **gemiddeld**, **lage**, of **niet nader omschreven**.

Hallo **zypper** opdracht ziet er slechts voor Hallo-updates die uw geïnstalleerde pakketten moeten. U kunt bijvoorbeeld deze opdracht gebruiken:

`sudo zypper patch  --category=security,recommended --severity=critical,important`

U kunt de parameter Hallo toevoegen `--dry-run` tootest Hallo update zonder Hallo system daadwerkelijk worden bijgewerkt.


### <a name="disk-setup"></a>Installatie van de schijf
Hallo hoofdmap bestandssysteem in een Linux-VM in Azure is een maximale grootte. Daarom is het nodig tooattach extra schijfruimte tooan Azure VM voor het uitvoeren van SAP. Hallo gebruik van Azure standard-opslag-schijven mogelijk niet voldoende voor SAP toepassingsserver virtuele Azure-machines. Voor SAP HANA DBMS Azure VM's is Hallo gebruik van Azure Premium-opslag-schijven voor productie- en niet voor productie-implementaties echter verplicht.

Op basis van Hallo [opslagvereisten voor SAP HANA TDI](https://www.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html), Hallo na de configuratie van Azure Premium-opslag wordt voorgesteld: 

| VM-SKU | RAM |  hana/gegevens en hana/logboekbestanden <br /> striped met LVM of MDADM | / hana/gedeeld | / Root-volume | / usr/sap |
| --- | --- | --- | --- | --- | --- |
| GS5 | 448 GB | 2 x P30 | 1 x P20 | 1 x P10 | 1 x P10 | 

Hallo HANA gegevensvolume en logboekvolume in Hallo voorgestelde schijfconfiguratie, worden op Hallo dezelfde set Azure premium-schijven voor opslag met LVM of MDADM striped geplaatst. Het is niet nodig toodefine alle RAID-redundantie niveau omdat Azure Premium-opslag houdt drie afbeeldingen van Hallo schijven voor redundantie. toomake zeker dat u voldoende opslagruimte configureert Raadpleeg Hallo [opslagvereisten voor SAP HANA TDI](https://www.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html) en [Update handleiding en SAP HANA-serverinstallatie](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4c/24d332a37b4a3caad3e634f9900a45/frameset.htm). Denk ook na over Hallo verschillende virtuele harde schijf (VHD) doorvoer volumes Hallo verschillende Azure premium-opslag-schijven zoals beschreven in [beheerde schijven voor virtuele machines en hoge prestaties Premium-opslag](https://docs.microsoft.com/azure/storage/storage-premium-storage). 

U kunt toevoegen om dat meer premium-opslag schijven toohello HANA DBMS VM's voor het opslaan van de database of het transactielogboek logboekback-ups.

Zie voor meer informatie over Hallo twee belangrijkste hulpprogramma's tooconfigure striping Hallo artikelen te volgen:

* [Configureren van software-RAID op Linux](../../linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [LVM configureren op een virtuele Linux-machine in Azure](../../linux/configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Zie voor meer informatie over het koppelen van tooAzure virtuele machines met Linux als een gastbesturingssysteem schijven, [toevoegen van een schijf tooa Linux VM](../../linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Azure Premium-opslag kunt u de modi van de schijfcache toodefine. Voor Hallo striped set /hana/data en /hana/log, moet schijfcache worden uitgeschakeld. Voor hello andere volumes (schijven) Hallo caching modus te moet worden ingesteld**ReadOnly**.

Zie voor meer informatie [Premium-opslag: krachtige opslag voor Azure Virtual Machine-werkbelasting](../../../storage/common/storage-premium-storage.md).

toofind voorbeeld JSON-sjablonen voor het maken van virtuele machines, gaat u te[Azure-Snelstartsjablonen](https://github.com/Azure/azure-quickstart-templates).
Hallo vm-eenvoudige-sles sjabloon is een eenvoudige sjabloon. Bevat een opslagsectie, met een schijf extra 100 GB aan gegevens. Deze sjabloon kan worden gebruikt als basis. U kunt specifieke configuratie van Hallo sjabloon tooyour aanpassen.

>[!Note]
>Het is belangrijk tooattach hello Azure storage-schijf met behulp van een UUID zoals beschreven in [SAP NetWeaver uitgevoerd op Microsoft Azure SUSE Linux VM's](suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

In de testomgeving Hallo zijn twee schijven van Azure standard-opslag gekoppelde toohello SAP appserver VM, zoals wordt weergegeven in de volgende schermafbeelding Hallo. Alle Hallo SAP-software (inclusief NetWeaver 7.5, SAP-GUI en SAP HANA) één schijf opgeslagen voor de installatie. de tweede schijf Hallo gezorgd dat voldoende vrije ruimte beschikbaar voor aanvullende vereisten (bijvoorbeeld een back-up en test gegevens) en voor Hallo /sapmnt directory (dat wil zeggen, SAP-profielen) toobe gedeeld door alle virtuele machines die deel uitmaken van toohello dezelfde SAP Liggend.

![SAP HANA app server schijven venster om van twee gegevensschijven en de grootte weer te geven](./media/hana-get-started/image003.jpg)


### <a name="kernel-parameters"></a>Kernel-parameters
SAP HANA vereist specifieke Linux kernel instellingen, die geen deel uitmaken van Hallo standaard Azure-galerie installatiekopieën en moeten handmatig worden ingesteld. Afhankelijk van of u SUSE of Red Hat gebruikt, kunnen de Hallo parameters anders zijn. Hallo SAP opmerkingen bij de eerder vermelde geven informatie over deze parameters. In Hallo schermafbeeldingen weergegeven werd SUSE Linux 12 SP1 gebruikt. 

SLES voor SAP-toepassingen 12 GA en SLES voor SAP-toepassingen 12 SP1 hebt u een nieuw hulpprogramma **afgestemd adm**, dat vervangt oude Hallo **sapconf** hulpprogramma. Er is een speciaal SAP HANA-profiel beschikbaar voor **afgestemd adm**. Hallo volgende tootune Hallo system voor SAP HANA invoeren als een hoofdgebruiker:

   `tuned-adm profile sap-hana`

Voor meer informatie over **afgestemd adm**, Zie Hallo [SUSE documentatie over afgestemd adm](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip).

In Hallo schermafbeelding te volgen, kunt u zien hoe **afgestemd adm** gewijzigde Hallo `transparent_hugepage` en `numa_balancing` waarden, op basis van toohello vereiste SAP HANA-instellingen.

![Hallo afgestemd adm hulpprogramma waarden volgens toorequired SAP HANA-instellingen gewijzigd](./media/hana-get-started/image005.jpg)

Gebruik toomake Hallo SAP HANA kernel instellingen permanent, **grub2** op SLES 12. Voor meer informatie over **grub2**, gaat u toohello [structuur van configuratiebestand](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip) sectie Hallo SUSE documentatie.

Hallo volgende schermafbeelding ziet u hoe Hallo kernel-instellingen zijn gewijzigd in het configuratiebestand Hallo en vervolgens gecompileerd met behulp van **grub2 mkconfig**:

![Kernel-instellingen gewijzigd in het configuratiebestand Hallo en gecompileerd met behulp van grub2 mkconfig](./media/hana-get-started/image006.jpg)

Een andere optie is toochange Hallo instellingen met behulp van YaST en Hallo **opstartlaadprogramma** > **Kernel Parameters** instellingen:

![Hallo Kernel Parameters tabblad instellingen van YaST opstartlaadprogramma](./media/hana-get-started/image007.jpg)

### <a name="file-systems"></a>Bestandssystemen
Hallo volgende schermafbeelding ziet u twee bestandssystemen die zijn gemaakt op Hallo SAP appserver VM boven op Hallo twee gekoppelde Azure standard-opslag-schijven. Beide bestandssystemen zijn van het type XFS en gekoppelde te/sapdata en /sapsoftware zijn.

Het is niet verplicht toostructure uw bestandssystemen op deze manier. Hebt u andere opties voor het structureren Hallo schijfruimte. Hallo meest belangrijk aandachtspunt is tooprevent Hallo hoofdmap bestandssysteem onvoldoende vrije ruimte.

![Twee bestandssystemen die zijn gemaakt op Hallo SAP appserver VM](./media/hana-get-started/image008.jpg)

Met betrekking tot Hallo VM voor SAP HANA-database, tijdens de installatie van een database, wanneer u SAPinst (SWPM) en Hallo **typische** installatieoptie, alles onder /hana en /usr/sap is geïnstalleerd. de standaardlocatie Hallo voor Hallo SAP HANA logboekback-up is onder /usr/sap. Opnieuw, omdat het is belangrijk tooprevent Hallo hoofdmap bestandssysteem onvoldoende opslagruimte, zorg ervoor dat er voldoende ruimte beschikbaar is onder /hana en /usr/sap voordat u SAP HANA installeren met behulp van SWPM.

Zie voor een beschrijving van Hallo standaard bestandssysteem lay-out van SAP HANA Hallo [Update handleiding en SAP HANA-serverinstallatie](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4c/24d332a37b4a3caad3e634f9900a45/frameset.htm).

![Aanvullende bestandssystemen die zijn gemaakt op Hallo SAP appserver VM](./media/hana-get-started/image009.jpg)

Wanneer u SAP NetWeaver op een standaard SLES/SLES voor SAP-toepassingen 12 Azure-galerie installatiekopie installeert, wordt een bericht weergegeven dat er geen wisselruimte, zoals wordt weergegeven in de volgende schermafbeelding Hallo. toodismiss die dit bericht, kunt u handmatig een wisselbestand toevoegen met behulp van **dd**, **mkswap**, en **swapon**. toolearn hoe, zoekt u "handmatig toevoegen van een wisselbestand' in hello [Using Hallo YaST Partitioner](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip) sectie Hallo SUSE documentatie.

Een andere optie is tooconfigure wisselruimte via Hallo Linux VM-agent. Zie voor meer informatie, Hallo [gebruikershandleiding voor Azure Linux Agent](../../linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

![Pop-bericht verschijnt dat er onvoldoende wisselruimte is](./media/hana-get-started/image010.jpg)


### <a name="hello-etchosts-file"></a>Hallo/etc/hosts-bestand
Voordat u tooinstall SAP, zorg er dan voor dat u Hallo hostnamen en IP-adressen van Hallo SAP virtuele machines in Hallo/etc/hosts-bestand opnemen. Alle Hallo SAP-VM's binnen een virtuele Azure-netwerk te implementeren en gebruik vervolgens Hallo interne IP-adressen, zoals hier wordt weergegeven:

![Hostnamen en IP-adressen van Hallo SAP-virtuele machines die zijn vermeld in Hallo/etc/hosts-bestand](./media/hana-get-started/image011.jpg)

### <a name="hello-etcfstab-file"></a>Hallo bestand/etc/fstab-fouten

Het is nuttig tooadd hello **nofail** parameter toohello fstab-bestand. Op deze manier als er iets mis met Hallo schijven gaat, Hallo VM komt niet vastlopen in Hallo-opstartproces. Maar houd er rekening mee dat extra schijfruimte mogelijk niet beschikbaar en processen Hallo root-bestandssysteem opvullen mogelijk. Als /hana ontbreekt, start SAP HANA niet.

![Hallo nofail parameter toohello fstab-bestand toevoegen](./media/hana-get-started/image000c.jpg)

## <a name="graphical-gnome-desktop-on-sles-12sles-for-sap-applications-12"></a>Grafische GNOME bureaublad op SLES 12/SLES voor SAP-toepassingen 12
Deze sectie bevat de volgende onderwerpen Hallo:

* Hallo GNOME bureaublad en xrdp installeert op SLES 12/SLES voor SAP-toepassingen 12
* Java gebaseerde SAP MV uitgevoerd met behulp van Firefox op SLES 12/SLES voor SAP-toepassingen 12

U kunt ook alternatieven zoals Xterminal of VNC (wordt niet beschreven in deze handleiding) gebruiken.

### <a name="installing-hello-gnome-desktop-and-xrdp-on-sles-12sles-for-sap-applications-12"></a>Hallo GNOME bureaublad en xrdp installeert op SLES 12/SLES voor SAP-toepassingen 12
Als u een Windows-achtergrond hebt, kunt u eenvoudig een grafische bureaublad rechtstreeks in Hallo SAP virtuele Linux-machines toorun Firefox, SAPinst, GUI SAP, SAP MV of HANA Studio gebruiken en toohello VM via Hallo Remote Desktop Protocol (RDP) van een Windows-computer verbinding te maken. Afhankelijk van uw bedrijfsbeleid over het toevoegen van grafische gebruikersinterfaces tooproduction en niet-productieve op basis van Linux-systemen, wilt u mogelijk tooinstall GNOME op uw server. tooinstall hello GNOME desktop op een Azure-SLES 12/SLES voor SAP-toepassingen 12 VM:

1. Hallo GNOME bureaublad door in te voeren na de opdracht (bijvoorbeeld in een venster PuTTY) Hallo installeren:

   `zypper in -t pattern gnome-basic`

2. Xrdp tooallow een verbinding toohello VM via RDP installeren:

   `zypper in xrdp`

3. /Etc/sysconfig/windowmanager bewerken en stel Hallo standaard venster manager tooGNOME:

   `DEFAULT_WM="gnome"`

4. Voer **chkconfig** toomake ervoor gezorgd dat xrdp automatisch wordt gestart na opnieuw opstarten:

   `chkconfig -level 3 xrdp on`

5. Als er een probleem met de Hallo RDP-verbinding, probeert u toorestart (uit een PuTTY venster bijvoorbeeld):

   `/etc/xrdp/xrdp.sh restart`

6. Als een herstart xrdp vermeld in de vorige Hallo stap niet werkt, controleert u voor een bestand .pid:

   `check /var/run` 

   Zoek naar `xrdp.pid`. Als u wordt gevonden, verwijderen en probeer het opnieuw toorestart.

### <a name="starting-sap-mc"></a>SAP MV starten
Na de installatie van Hallo GNOME bureaublad Hallo grafische vanaf Java gebaseerde SAP MV van Mozilla Firefox tijdens het uitvoeren van een Azure-SLES 12/SLES voor SAP-toepassingen 12 VM mogelijk een foutbericht weergegeven vanwege Hallo Java browser-invoegtoepassing ontbreekt.

Hallo URL toostart Hallo SAP MV is `<server>:5<instance_number>13`.

Zie voor meer informatie [starten Hallo SAP Management webconsole](https://help.sap.com/saphelp_nwce10/helpdata/en/48/6b7c6178dc4f93e10000000a42189d/frameset.htm).

Hallo ziet volgende schermafbeelding Hallo foutbericht dat wordt weergegeven wanneer Hallo Java browser-invoegtoepassing ontbreekt:

![Foutbericht dat aangeeft dat de ontbrekende Java browser-invoegtoepassing](./media/hana-get-started/image013.jpg)

Eenzijdige toosolve Hallo probleem is tooinstall Hallo ontbreekt invoegtoepassing met behulp van YaST, zoals wordt weergegeven in de volgende schermafbeelding Hallo:

![Met behulp van YaST tooinstall invoegtoepassing ontbreekt](./media/hana-get-started/image014.jpg)

Wanneer u opnieuw Hallo SAP Management Console-URL invoeren, verschijnt een bericht gevraagd u tooactivate Hallo invoegtoepassing:

![In het dialoogvenster invoegtoepassing activering aanvraagt](./media/hana-get-started/image015.jpg)

U kunt ook een foutbericht over een ontbrekend bestand, ontvangen javafx.properties. Dit is vereiste gerelateerde toohello van Oracle Java 1.8 voor SAP GUI 7.4. (Zie [SAP-notitie 2059429](https://launchpad.support.sap.com/#/notes/2059424).) Hallo IBM Java-versie noch Hallo openjdk pakket geleverd met SLES/SLES voor SAP-toepassingen 12 bevat Hallo benodigde javafx.properties bestand. Hallo-oplossing is toodownload en Java SE 8 installeren uit Oracle.

Zie voor informatie over een soortgelijk probleem met openjdk op openSUSE Hallo bespreking van de thread [SAPGui 7.4 Java voor openSUSE 42,1 Leap](https://scn.sap.com/thread/3908306).

## <a name="manual-installation-of-sap-hana-swpm"></a>Handmatige installatie van het SAP HANA: SWPM
Hallo reeks schermafbeeldingen in deze sectie toont Hallo belangrijke stappen voor het installeren van SAP NetWeaver 7.5 en SAP HANA SP12 wanneer u SWPM (SAPinst) gebruikt. Als onderdeel van een installatie van de NetWeaver 7.5 kunt SWPM Hallo HANA-database ook installeren als één exemplaar.

In een testomgeving voorbeeld er slechts één geavanceerde Business Application Programming (ABAP) appserver geïnstalleerd. Zoals u in de volgende schermafbeelding Hallo, hebben we Hallo gebruikt **Distributed System** optie tooinstall hello ASC's- en serverinstanties van de primaire toepassing in een virtuele machine van Azure en SAP HANA als Hallo databasesysteem in een andere virtuele machine in Azure.

![ASC's en exemplaren van de primaire toepassing-server is geïnstalleerd met behulp van Hallo Distributed System optie](./media/hana-get-started/image012.jpg)

Nadat Hallo ASC's exemplaar op Hallo appserver VM is geïnstalleerd en is moet ingesteld te 'groen' hello SAP Management Console (weergegeven in de volgende schermafbeelding Hallo) Hallo /sapmnt directory (inclusief Hallo SAP profiel directory) worden gedeeld met Hallo SAP HANA databaseserver VM. Hallo DB installatiestap moet toegang tot toothis informatie. Hallo beste manier tooprovide toegang is toouse NFS, die kan worden geconfigureerd met behulp van YaST.

![SAP-beheerconsole weergeven Hallo ASC's exemplaar geïnstalleerd op de server van de app Hallo VM en te 'groen' instellen](./media/hana-get-started/image016.jpg)

Hallo op Hallo appserver VM/sapmnt directory via NFS mag worden gedeeld met behulp van Hallo **rw** en **no_root_squash** opties. Hallo zijn standaard **ro** en **root_squash**, wat mogelijk tooproblems leiden bij het installeren van Hallo database-exemplaar.

![Hallo /sapmnt directory via NFS delen met behulp van Hallo rw en no_root_squash opties](./media/hana-get-started/image017b.jpg)

Zoals Hallo volgende Schermafbeelding toont, Hallo /sapmnt share van de server van de app Hallo VM moet worden geconfigureerd op Hallo SAP HANA-database server VM met behulp van **NFS-Client** (en YaST).

![Hallo /sapmnt share zijn geconfigureerd met behulp van de NFS-Client](./media/hana-get-started/image018b.jpg)

installatie van een gedistribueerde NetWeaver 7.5 tooperform (**Database-exemplaar**), als weergegeven in Hallo schermafbeelding te volgen, toohello SAP HANA databaseserver VM aanmelden en SWPM starten.

![Een database-exemplaar installeren toohello SAP HANA databaseserver VM aanmelden en SWPM gestart](./media/hana-get-started/image019.jpg)

Nadat u hebt geselecteerd **typische** installatie en Hallo pad toohello-installatiemedia, voert een DB SID, Hallo hostnaam, exemplaarnummer hello, en wachtwoord systeembeheerder Hallo DB.

![Hallo SAP HANA-database systeembeheerder aanmelden pagina](./media/hana-get-started/image035b.jpg)

Hallo wachtwoord invoeren voor Hallo DBACOCKPIT schema:

![Hallo wachtwoordinvoer vak voor Hallo DBACOCKPIT schema](./media/hana-get-started/image036b.jpg)

Geef een vraag voor Hallo SAPABAP1 schema wachtwoord:

![Geef een vraag voor Hallo SAPABAP1 schema wachtwoord](./media/hana-get-started/image037b.jpg)

Nadat elke taak is voltooid, wordt een groen vinkje volgende tooeach fase Hallo DB installatieproces weergegeven. Hallo-bericht 'uitvoering van... Database exemplaar is voltooid' wordt weergegeven.

![Taak is voltooid-venster met bevestigingsbericht](./media/hana-get-started/image023.jpg)

Hallo SAP-beheerconsole moet ook na de installatie is voltooid, DB-exemplaar als 'groen' hello weergeven en Hallo volledige lijst weergeven met SAP HANA processen (hdbindexserver, hdbcompileserver, enzovoort).

![SAP Management Console-venster met de lijst met SAP HANA-processen](./media/hana-get-started/image024.jpg)

Hallo toont volgende schermafbeelding Hallo onderdelen van Hallo bestandsstructuur onder Hallo /hana/shared directory die SWPM tijdens het Hallo HANA-installatie gemaakt. Omdat er geen optie toospecify een ander pad, is het belangrijk toomount extra schijfruimte onder Hallo /hana directory voordat Hallo SAP HANA-installatie met behulp van SWPM. Dit voorkomt u dat Hallo root-bestandssysteem geen beschikbare ruimte die wordt uitgevoerd.

![Hallo /hana/shared bestand mapstructuur gemaakt tijdens de installatie van de HANA](./media/hana-get-started/image025.jpg)

Deze schermafbeelding ziet u de bestandsstructuur Hallo van Hallo /usr/sap map:

![Hallo /usr/sap directory bestandsstructuur](./media/hana-get-started/image026.jpg)

de laatste stap Hallo van Hallo gedistribueerd ABAP installatie is tooinstall Hallo primaire application server-exemplaar:

![ABAP installatie tonen primaire application server-exemplaar als laatste stap Hallo](./media/hana-get-started/image027b.jpg)

Nadat het Hallo primaire application server-exemplaar en SAP-GUI zijn geïnstalleerd, gebruikt u Hallo **DBA Cockpit** transactie tooconfirm die Hallo SAP HANA-installatie correct is voltooid:

![DBA Cockpit venster geslaagde installatie bevestigen](./media/hana-get-started/image028b.jpg)

Als een laatste stap mogelijk u wilt toofirst installatie HANA Studio Hallo SAP appserver-machine en vervolgens verbinding toohello SAP HANA-exemplaar dat wordt uitgevoerd op Hallo DB server VM:

![SAP HANA Studio installeren in Hallo SAP appserver VM](./media/hana-get-started/image038b.jpg)

## <a name="manual-installation-of-sap-hana-hdblcm"></a>Handmatige installatie van het SAP HANA: HDBLCM
In aanvulling tooinstalling SAP HANA als onderdeel van een gedistribueerde installatie met behulp van SWPM, kunt u Hallo HANA zelfstandige eerst installeren met behulp van HDBLCM. U kunt bijvoorbeeld SAP NetWeaver 7.5, installeren. Hallo schermafbeeldingen in deze sectie laten zien hoe dit proces werkt.

Zie voor meer informatie over Hallo HANA HDBLCM hulpprogramma's:

* [Kiezen Hallo Corrigeer SAP HANA HDBLCM voor uw taak](https://help.sap.com/saphelp_hanaplatform/helpdata/en/68/5cff570bb745d48c0ab6d50123ca60/content.htm)
* [SAP HANA Lifecycle beheerhulpprogramma 's](http://saphanatutorial.com/sap-hana-lifecycle-management-tools/)
* [Update-handleiding en SAP HANA-serverinstallatie](http://help.sap.com/hana/SAP_HANA_Server_Installation_Guide_en.pdf)

problemen met een standaard tooavoid ID groepsinstelling voor Hallo `\<HANA SID\>adm user` (gemaakt door Hallo HDBLCM hulpprogramma), definieert u een nieuwe groep is aangeroepen `sapsys` met behulp van de groeps-ID `1001` voordat u een SAP HANA via HDBLCM installeert:

![Nieuwe groep 'sapsys' gedefinieerd met behulp van groep-ID 1001](./media/hana-get-started/image030.jpg)

Wanneer u HDBLCM Hallo eerst wordt gestart, wordt een eenvoudige startmenu weergegeven. SELECT-item 1, **nieuw systeem installeren**, zoals weergegeven in de volgende schermafbeelding Hallo:

![Optie "Nieuw systeem installeren" in hello HDBLCM startvenster](./media/hana-get-started/image031.jpg)

Hallo volgende schermafbeelding alle Hallo sleutel opties weergegeven die u eerder hebt geselecteerd.

> [!IMPORTANT]
> Mappen die zijn met de naam van het logboek HANA en gegevensvolumes, evenals Hallo installatiepad (hana/gedeeld in dit voorbeeld) en /usr/sap, moeten niet deel uitmaken van Hallo root-bestandssysteem. Deze mappen behoren toohello Azure gegevensschijven die zijn aangesloten toohello VM (beschreven in de sectie Hallo 'Disk setup'). Deze aanpak helpt voorkomen dat Hallo root-bestandssysteem geen ruimte meer is die wordt uitgevoerd. In Hallo schermafbeelding te volgen, kunt u zien dat Hallo HANA-systeembeheerder heeft gebruikers-ID `1005` en maakt deel uit van Hallo `sapsys` groep (ID `1001`) die is gedefinieerd vóór het Hallo-installatie.

![Lijst van alle belangrijke SAP HANA-onderdelen eerder hebt geselecteerd](./media/hana-get-started/image032.jpg)

U kunt controleren Hallo `\<HANA SID\>adm user` (`azdadm` in de volgende schermafbeelding Hallo) details in Hallo/etc/passwd map:

![HANA \<HANA SID\>adm Gebruikersdetails vermeld in Hallo/etc/passwd directory](./media/hana-get-started/image033.jpg)

Nadat u een SAP HANA installeren met behulp van HDBLCM, ziet u Hallo bestandsstructuur in SAP HANA-Studio, zoals wordt weergegeven in de volgende schermafbeelding Hallo. Hallo SAPABAP1 schema, die alle Hallo SAP NetWeaver tabellen bevat, is nog niet beschikbaar.

![Bestandsstructuur voor SAP HANA in SAP HANA-Studio](./media/hana-get-started/image034.jpg)

Nadat u SAP HANA installeert, kunt u SAP NetWeaver installeren toe. Hallo-installatie is als weergegeven in Hallo schermafbeelding te volgen, als een gedistribueerde installatie uitgevoerd met behulp van SWPM (zoals beschreven in de vorige sectie Hallo). Wanneer u de database-instantie Hallo installeren met behulp van SWPM, voert u Hallo dezelfde gegevens met behulp van HDBLCM (bijvoorbeeld: hostnaam, HANA SID en exemplaarnummer). SWPM hello bestaande HANA installatie gebruikt vervolgens en voegt meer schema's.

![Een gedistribueerde installatie uitgevoerd met behulp van SWPM](./media/hana-get-started/image035b.jpg)

Hallo volgende schermafbeelding ziet Hallo SWPM installatiestap waarin u gegevens over Hallo DBACOCKPIT schema invoeren:

![Hallo SWPM installatiestap waar DBACOCKPIT schemagegevens zijn ingevoerd](./media/hana-get-started/image036b.jpg)

Voer de gegevens over Hallo SAPABAP1 schema:

![Gegevens over Hallo SAPABAP1 schema invoeren](./media/hana-get-started/image037b.jpg)

Nadat Hallo SWPM database-exemplaar installatie is voltooid, ziet u Hallo SAPABAP1 schema in SAP HANA Studio:

![Hallo SAPABAP1 schema in SAP HANA-Studio](./media/hana-get-started/image038b.jpg)

Ten slotte nadat Hallo SAP-app-server en SAP-GUI-installaties zijn voltooid, kunt u controleren Hallo HANA-database-exemplaar met behulp van Hallo **DBA Cockpit** transactie:

![Hallo HANA-database-exemplaar is gecontroleerd met Hallo DBA Cockpit transactie](./media/hana-get-started/image039b.jpg)


## <a name="sap-software-downloads"></a>SAP softwaredownloads
U kunt software downloaden van Hallo SAP Service Marketplace, zoals wordt weergegeven in de volgende schermafbeeldingen Hallo.

Download NetWeaver 7.5 voor Linux/HANA:

 ![SAP-Service-installatie en Upgrade-venster voor het downloaden van de NetWeaver 7.5](./media/hana-get-started/image001.jpg)

Download HANA SP12 Platform editie:

 ![SAP-Service-installatie en Upgrade-venster voor het downloaden van HANA SP12 Platform Edition](./media/hana-get-started/image002.jpg)

