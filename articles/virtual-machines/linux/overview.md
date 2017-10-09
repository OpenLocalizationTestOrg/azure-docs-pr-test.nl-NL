---
title: aaaOverview van Linux virtuele machines in Azure | Microsoft Docs
description: Beschrijving van Azure Compute, opslag en netwerken services met Linux virtuele machines.
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: rickstercdn
manager: timlt
editor: 
ms.assetid: 7965a80f-ea24-4cc2-bc43-60b574101902
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 09/14/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 958e219d53026d787a7a41f2fd13c29c739a9238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-and-linux"></a>Azure en Linux
Microsoft Azure is een groeiende verzameling geïntegreerde openbare cloud services analytics, virtuele Machines, databases, mobiel, netwerken, opslag, waaronder en web&mdash;ideaal voor het hosten van uw oplossingen.  Microsoft Azure biedt een schaalbare computerplatform waarmee u tooonly betalen voor wat u gebruikt, als u wilt dat deze - zonder tooinvest in lokale hardware.  Azure is gereed wanneer u uw oplossingen up tooscale zijn en uit toowhatever scale u tooservice Hallo behoeften van uw clients nodig hebt.

Als u bekend met bent verschillende functies van Amazon Hallo AWS, u kunt controleren hello Azure vs AWS [definitie toewijzing document](https://azure.microsoft.com/campaigns/azure-vs-aws/mapping/).

## <a name="regions"></a>Regio's
Microsoft Azure-resources worden gedistribueerd over meerdere geografische regio's Hallo wereld.  Een 'regio' geeft meerdere datacenters in één geografisch gebied.  We hebben 34 regio's, algemeen beschikbaar Hallo wereld met een extra 4 gebieden aangekondigd. Omdat we tooexpand onze wereldwijde dekking blijven - onderhouden we dat een bijgewerkte lijst met bestaande en nieuwe aangekondigd regio's.

* [Azure-regio's](https://azure.microsoft.com/regions/)

## <a name="availability"></a>Beschikbaarheid
We een bedrijfstak toonaangevende één exemplaar virtuele machine van de serviceovereenkomst van 99,9% opgegeven implementeren van Hallo VM voor premium-opslag voor alle schijven aangekondigd.  Om uw implementatie tooqualify voor onze standaard 99,95% VM Service Level Agreement, u moet nog steeds toodeploy twee of meer virtuele machines die de werkbelasting binnen een beschikbaarheidsset. Dit zorgt ervoor uw virtuele machines zijn verdeeld over meerdere domeinen met fouten in onze datacenters, evenals geïmplementeerd op hosts met verschillende onderhoudsvensters. Hallo volledige [Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_0/) wordt uitgelegd Hallo gegarandeerde beschikbaarheid van Azure als geheel.

## <a name="managed-disks"></a>Beheerde schijven

Schijven ingangen Azure Storage-account maken en beheren op de achtergrond Hallo voor u en zorgt ervoor dat u hebt geen tooworry over schaalbaarheidsbeperkingen Hallo Hallo opslagaccount die worden beheerd. U gewoon opgeven Hallo schijfgrootte en Hallo prestatielaag (Standard of Premium) en Azure maakt en beheert Hallo schijf voor u. Zelfs als u schijven toevoegen of Hallo VM omhoog en omlaag schalen, hebt u geen tooworry over Hallo opslag wordt gebruikt. Als u nieuwe virtuele machines, maakt [hello Azure CLI 2.0 gebruiken](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) of hello Azure portal toocreate virtuele machines met beheerde-besturingssysteem en gegevensschijven. Als u virtuele machines met niet-beheerde schijven hebt, kunt u [converteren van uw virtuele machines toobe back met schijven beheerd](convert-unmanaged-to-managed-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

U kunt ook aangepaste installatiekopieën in een opslagaccount per Azure-regio beheren en ze toocreate honderden van virtuele machines in hello gebruiken hetzelfde abonnement. Zie voor meer informatie over beheerde schijven Hallo [schijven overzicht beheerde](../windows/managed-disks-overview.md).

## <a name="azure-virtual-machines--instances"></a>Virtuele Machines in Azure & exemplaren
Microsoft Azure ondersteunt de uitvoering van een aantal populaire Linux-distributies geleverd en wordt onderhouden door een aantal partners.  U vindt distributies zoals Red Hat Enterprise, CentOS, Debian, Ubuntu, virtuele CoreOS, RancherOS, FreeBSD en nog veel meer in hello Azure Marketplace. We actief werken met verschillende Linux-community's tooadd nog meer versies toohello [door Azure goedgekeurde Linux Distros](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) lijst.

Als uw voorkeur Linux distro keuze niet momenteel aanwezig is in de galerie hello, u kunt 'Bring your own Linux' VM door [maakt en uploadt u een Linux-VHD in Azure](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Virtuele machines van Azure kunt u een breed scala aan oplossingen computergebruik in een flexibele manier toodeploy. U kunt vrijwel elke werkbelasting en een andere taal op bijna elk besturingssysteem - Windows, Linux, implementeren of een aangepaste gemaakt bij een van onze groeiende lijst met partners. Nog niet wordt weergegeven wat u zoekt?  U hoeft niet - u kunt ook uw eigen installatiekopieën zetten van on-premises.

## <a name="vm-sizes"></a>VM-grootten
Wanneer u een virtuele machine in Azure implementeert, gaat u een VM-grootte binnen één van de reeks grootten die is geschikt tooyour werkbelasting tooselect. Hallo grootte zijn ook van invloed op Hallo verwerkingskracht, geheugen, en de opslagcapaciteit van Hallo virtuele machine. U wordt gefactureerd op basis van Hallo hoeveelheid tijd Hallo VM wordt uitgevoerd en de toegewezen bronnen verbruiken. Een volledige lijst met [grootten van virtuele Machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Hier volgen enkele algemene richtlijnen voor het selecteren van een VM-grootte van een van onze reeks (A, D, DS, G en GS).
* A-serie VM's zijn onze waarde prijs instapmodellen VMs voor lichte werkbelastingen en scenario's voor ontwikkelen en testen. Ze kunnen algemeen beschikbaar zijn in alle regio's en verbinding maken en alle standaard resources beschikbaar toovirtual machines gebruiken.
* A-serie grootten (A8 - A11) zijn speciale berekenings-intensieve configuraties geschikt is voor high-performance computing clustertoepassingen.
* D-reeks VM's zijn ontworpen toorun toepassingen die hoger rekencapaciteit en prestaties van de tijdelijke schijf. D-reeks virtuele machines bieden snellere processors, een hogere ratio van geheugen-core- en een SSD-station (SSD) voor de tijdelijke schijf Hallo.
* Dv2-serie Hallo meest recente versie van onze D-reeks is, biedt een krachtige CPU. Hallo CPU Dv2-serie is ongeveer 35% sneller dan Hallo D-reeks CPU. Is gebaseerd op Hallo nieuwste 2,4 GHz Intel Xeon® E5-2673 v3-processor (Haskell), en met Hallo Intel Turbo versterking Technology 2.0, up too3.2 GHz kunt gaan. Hallo Dv2-serie heeft dezelfde configuraties voor geheugen en schijfruimte Hallo zoals Hallo D-reeks.
* G-serie VMs Hallo bieden de meeste geheugen en uitgevoerd op hosts met Intel Xeon E5 V3-familie processor een.

Opmerking: DS-serie en GS-serie virtuele machines hebben toegang tooPremium opslag - onze SSD back opslag voor hoge prestaties, lage latentie voor i/o-intensieve werkbelastingen. Premium Storage is beschikbaar in bepaalde regio's. Zie deze artikelen voor meer informatie:

* [Premium-opslag: Krachtige opslag voor workloads van de virtuele machine van Azure](../../storage/common/storage-premium-storage.md)

## <a name="automation"></a>Automatisering
tooachieve een juiste DevOps cultuur, alle infrastructuur moet de code.  Wanneer alle infrastructuur Hallo leven in code deze gemakkelijk kan worden opnieuw gemaakt (Phoenix Servers).  Azure werkt met alle Hallo belangrijke automation tooling zoals Ansible, Chef, SaltStack en Puppet.  Azure heeft ook een eigen tooling voor automation:

* [Azure-sjablonen](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Azure VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Azure-ondersteuning voor rolt [cloud init](http://cloud-init.io/) in de meeste Linux Distros die dit ondersteunen.  Op dit moment zijn van Canonical Ubuntu virtuele machines geïmplementeerd met cloud-init zijn standaard ingeschakeld.  Rood hoeden RHEL, CentOS en Fedora cloud init ondersteunen, maar hello Azure installatiekopieën onderhouden met RedHat hebben geen cloud-init zijn geïnstalleerd.  toouse cloud-init op een serie RedHat OS, moet u een aangepaste installatiekopie maken met cloud-init zijn geïnstalleerd.

* [Met behulp van cloud-init op Azure Linux VM 's](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quotas"></a>Quota
Elke Azure-abonnement heeft standaard de quotalimieten dat kan invloed hebben op Hallo-implementatie van een groot aantal virtuele machines voor uw project. de huidige limiet Hallo op basis van per abonnement is 20 VM's per regio.  De quotalimieten snel kunnen worden verhoogd en gemakkelijk door het indienen van een ondersteuningsticket aanvragen van een limiet verhogen.  Voor meer informatie over de quotalimieten voor:

* [Servicelimieten voor Azure-abonnement](../../azure-subscription-service-limits.md)

## <a name="partners"></a>Partners
Microsoft werkt samen met onze partners tooensure Hallo installatiekopieën beschikbaar zijn bijgewerkt en geoptimaliseerd voor een Azure-runtime.  Controleer de marketplace pagina's hieronder voor meer informatie over onze partners.

* Linux op Azure - [goedgekeurde distributies](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* SUSE - [Azure Marketplace - SUSE Linux Enterprise Server](https://azuremarketplace.microsoft.com/en-us/marketplace/apps?search=%27SUSE%27)
* RedHat - [Azure Marketplace - Red Hat Enterprise Linux 7.2](https://azure.microsoft.com/marketplace/partners/redhat/redhatenterpriselinux72/)
* Canonieke - [Azure Marketplace - Ubuntu Server 16.04 TNS](https://azure.microsoft.com/marketplace/partners/canonical/ubuntuserver1604lts/)
* Debian - [Azure Marketplace - Debian 8 'Jessie'](https://azure.microsoft.com/marketplace/partners/credativ/debian8/)
* FreeBSD - [Azure Marketplace - FreeBSD 10.3](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd103/)
* Virtuele CoreOS - [Azure Marketplace - virtuele CoreOS (stabiel)](https://azure.microsoft.com/marketplace/partners/coreos/coreosstable/)
* RancherOS - [Azure Marketplace - RancherOS](https://azure.microsoft.com/marketplace/partners/rancher/rancheros/)
* Bitnami - [Bitnami-bibliotheek voor Azure](https://azure.bitnami.com/)
* Mesosphere - [Azure Marketplace - Mesosphere DC/OS op Azure](https://azure.microsoft.com/marketplace/partners/mesosphere/dcosdcos/)
* Docker - [Azure Marketplace - Azure Containerservice met Docker Swarm](https://azure.microsoft.com/marketplace/partners/microsoft/acsswarms/)
* Jenkins - [Azure Marketplace - CloudBees Jenkins Platform](https://azure.microsoft.com/marketplace/partners/cloudbees/jenkins-platformjenkins-platform/)

## <a name="getting-started-with-linux-on-azure"></a>Aan de slag met Linux op Azure
toobegin met Azure u moet een Azure-account, hello Azure CLI is geïnstalleerd en een paar SSH openbare en persoonlijke sleutels.

### <a name="sign-up-for-an-account"></a>Registreren voor een account
Hallo eerste stap bij het gebruik van hello Azure-Cloud is toosign voor een Azure-account.  Ga toohello [Azure accountaanmelding](https://azure.microsoft.com/pricing/free-trial/) pagina tooget gestart.

### <a name="install-hello-cli"></a>Hallo CLI installeren
Met uw nieuwe Azure-account, u kunt aan de slag onmiddellijk met hello Azure portal een webgebaseerde admin-venster is.  toomanage hello Azure-Cloud via het opdrachtregelprogramma hello, installeert u Hallo `azure-cli`.  Hallo installeren [Azure CLI 2.0](/cli/azure/install-azure-cli) op uw Mac of Linux-werkstation.

### <a name="create-an-ssh-key-pair"></a>Een SSH-sleutelpaar maken
U hebt nu een Azure-account, hello Azure-web-portal en hello Azure CLI.  de volgende stap Hallo is toocreate een SSH-sleutelpaar dat wordt gebruikt tooSSH in Linux zonder een wachtwoord te gebruiken.  [SSH-sleutels maken in Linux en Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooenable wachtwoordloze aanmelding en betere beveiliging.

### <a name="create-a-vm-using-hello-cli"></a>Een virtuele machine maken met CLI Hallo
Maken van een Linux-VM, is het gebruik van Hallo CLI is een snelle manier toodeploy een virtuele machine zonder verlaten Hallo terminal die u werkt.  Alles wat die u op het webportaal Hallo opgeven kunt is beschikbaar via een opdrachtregel vlag of de switch.  

* [Maak een Linux-VM met Hallo CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="create-a-vm-in-hello-portal"></a>Een virtuele machine maken in Hallo-portal
Maken van een Linux-VM in hello Azure-web-portal is een manier tooeasily punt en klik door de verschillende opties tooget tooa implementatie Hallo.  In plaats van opdrachtregelprogramma vlaggen of switches, bent u kunnen tooview een nice web-indeling van de verschillende opties en instellingen.  Alles beschikbaar via de opdrachtregelinterface Hallo is ook beschikbaar in het Hallo-portal.

* [Maak een Linux-VM met Hallo Portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="login-using-ssh-without-a-password"></a>Aanmelding via SSH zonder wachtwoord
Hallo VM wordt nu uitgevoerd in Azure en u bent klaar toolog in.  Gebruik van wachtwoorden toolog in via SSH is onveilig en tijdrovend.  Met behulp van SSH-sleutels is Hallo meest veilige manier en ook de snelste manier toologin Hallo.  Wanneer u u Linux VM via Hallo portal of Hallo CLI maakt, hebt u twee opties voor verificatie.  Als u een wachtwoord voor SSH kiest, configureert Azure Hallo VM tooallow aanmeldingen via wachtwoorden.  Als u hebt gekozen toouse openbare SSH-sleutel, Azure Hallo VM configureert tooonly toestaan aanmeldingen via SSH-sleutels en wachtwoord aanmeldingen uitgeschakeld. toosecure uw Linux-VM met alleen belangrijke SSH-aanmeldingen, zodat gebruik Hallo SSH openbare sleutel optie tijdens het maken van VM's in Hallo portal of CLI Hallo.

## <a name="related-azure-components"></a>Gerelateerde Azure-onderdelen
## <a name="storage"></a>Storage
* [Inleiding tooMicrosoft Azure Storage](../../storage/common/storage-introduction.md)
* [Voeg een schijf tooa Linux-VM met hello azure-cli](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Hoe tooattach data schijf tooa Linux VM in hello Azure-portal](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="networking"></a>Netwerken
* [Overzicht van Virtual Network](../../virtual-network/virtual-networks-overview.md)
* [IP-adressen in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)
* [Openen van poorten tooa Linux VM in Azure](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Maken van een volledig gekwalificeerde domeinnaam in hello Azure-portal](portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="containers"></a>Containers
* [Virtuele Machines en Containers in Azure](containers.md)
* [Azure Container Service Inleiding](../../container-service/container-service-intro.md)
* [Een Azure Container Service-cluster implementeren](../../container-service/dcos-swarm/container-service-deployment.md)

## <a name="next-steps"></a>Volgende stappen
U hebt nu een overzicht van Linux in Azure.  de volgende stap Hallo toodive in en maakt een paar virtuele machines!

* [Bekijk onze groeiende lijst met voorbeelden van Scripts voor algemene taken via AzureCLI](cli-samples.md)
