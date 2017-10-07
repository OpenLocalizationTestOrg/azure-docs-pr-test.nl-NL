---
title: 'Azure Site Recovery: Veelgestelde vragen | Microsoft Docs'
description: Dit artikel wordt populaire vragen over Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5cdc4bcd-b4fe-48c7-8be1-1db39bd9c078
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/22/2017
ms.author: raynew
ms.openlocfilehash: 6d0bd2475466e5745e1f084bd2267d954d624ebd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-site-recovery-frequently-asked-questions-faq"></a>Azure Site Recovery: veelgestelde vragen
Dit artikel bevat veelgestelde vragen over Azure Site Recovery. Als u vragen hebt na het lezen van dit artikel, plaatst u deze op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr).

## <a name="general"></a>Algemeen
### <a name="what-does-site-recovery-do"></a>Wat doet Site Recovery?
Site Recovery draagt bij tooyour zakelijke continuïteit en noodherstelplan (BCDR), door te organiseren en replicatie van Azure VM's tussen regio's, on-premises virtuele machines en fysieke servers tooAzure automatiseren, en on-premises machines tooa secundaire datacenter. [Meer informatie](site-recovery-overview.md).

### <a name="what-can-site-recovery-protect"></a>Wat kan Site Recovery beveiligen?
* **Virtuele machines in Azure**: Site Recovery kan elke workload uitgevoerd op een ondersteunde Azure-virtuele machine gerepliceerd
* **Hyper-V virtuele machines**: Site Recovery kan elke workload uitgevoerd op een virtuele machine van Hyper-V beveiligen.
* **Fysieke servers**: Site Recovery kunt beveiligen fysieke servers met Windows of Linux.
* **Virtuele VMware-machines**: Site Recovery kan elke workload uitgevoerd in een VMware-VM beveiligen.

### <a name="does-site-recovery-support-hello-azure-resource-manager-model"></a>Site Recovery biedt ondersteuning voor hello Azure Resource Manager-model?
Site Recovery is beschikbaar in hello Azure-portal met ondersteuning voor Resource Manager. Site Recovery biedt ondersteuning voor legacy-implementaties in Hallo klassieke Azure-portal. U kunt geen nieuwe kluizen maken in de klassieke portal Hallo en nieuwe functies worden niet ondersteund.

### <a name="can-i-replicate-azure-vms"></a>Kan ik virtuele Azure-machines repliceren?
Ja, kunt u de ondersteunde Azure-machines repliceren tussen Azure-regio's. [Meer informatie](site-recovery-azure-to-azure.md).

### <a name="what-do-i-need-in-hyper-v-tooorchestrate-replication-with-site-recovery"></a>Wat moet ik in Hyper-V tooorchestrate replicatie met Site Recovery?
Voor Hyper-V-hostserver Hallo afhankelijk wat u nodig hebt Hallo implementatiescenario. Bekijk Hallo Hyper-V-vereisten in:

* [TooAzure Hyper-V-machines (zonder VMM) repliceren](site-recovery-hyper-v-site-to-azure.md)
* [TooAzure Hyper-V-machines (met VMM) repliceren](site-recovery-vmm-to-azure.md)
* [Hyper-V-machines tooa secundair datacenter repliceren](site-recovery-vmm-to-vmm.md)
* Als u tooa secundaire repliceert datacenter meer informatie over [ondersteunde gastbesturingssystemen voor Hyper-V-machines](https://technet.microsoft.com/library/mt126277.aspx).
* Als u tooAzure repliceert, alle Hallo gastbesturingssystemen die ondersteuning biedt voor Site Recovery [ondersteund door Azure](https://technet.microsoft.com/library/cc794868%28v=ws.10%29.aspx).

### <a name="can-i-protect-vms-when-hyper-v-is-running-on-a-client-operating-system"></a>Kan ik virtuele machines beveiligen als Hyper-V wordt uitgevoerd op een clientbesturingssysteem?
Nee, virtuele machines moeten zich bevinden op een Hyper-V-hostserver die wordt uitgevoerd op een ondersteunde Windows-servercomputer. Als u tooprotect moet een clientcomputer u kan deze repliceert als een fysieke computer te[Azure](site-recovery-vmware-to-azure.md) of een [secundair datacenter](site-recovery-vmware-to-vmware.md).

### <a name="what-workloads-can-i-protect-with-site-recovery"></a>Welke workloads kan ik met Site Recovery beveiligen?
U kunt Site Recovery tooprotect meeste workloads die worden uitgevoerd op een ondersteunde virtuele machine of fysieke server. Site Recovery biedt ondersteuning voor toepassingsgevoelige replicatie, zodat apps kunnen worden hersteld tooan intelligente status. Het kan worden geïntegreerd met Microsoft-toepassingen zoals SharePoint, Exchange, Dynamics, SQL Server en Active Directory en werkt uitstekend samen met toonaangevende leveranciers, waaronder Oracle, SAP, IBM en Red Hat. Lees [hier](site-recovery-workload.md) meer informatie over workloadbeveiliging.

### <a name="do-hyper-v-hosts-need-toobe-in-vmm-clouds"></a>Moeten Hyper-V-hosts toobe in VMM-clouds?
Als u wilt dat tooreplicate tooa secundair datacenter, moet Hyper-V-machines op host Hyper-V van servers die zich bevinden in een VMM-cloud. Als u tooreplicate tooAzure wilt, kunt u virtuele machines op Hyper-V-hostservers met of zonder VMM-clouds repliceren. [Lees meer](site-recovery-hyper-v-site-to-azure.md).

### <a name="can-i-deploy-site-recovery-with-vmm-if-i-only-have-one-vmm-server"></a>Kan ik Site Recovery met VMM implementeren als ik maar één VMM-server heb?

Ja. Kunt u virtuele machines in Hyper-V-servers in Hallo VMM cloud tooAzure repliceren of u kunt repliceren tussen VMM-clouds op Hallo dezelfde server. Voor lokale tooon-premises replicatie, wordt u aangeraden dat u een VMM-server in beide Hallo primaire en secundaire sites hebben.  

### <a name="what-physical-servers-can-i-protect"></a>Welke fysieke servers kan ik beveiligen?
U kunt fysieke servers met Windows en Linux tooAzure of tooa secundaire site repliceren. [Meer informatie over](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) besturingssysteemvereisten.  Hallo dezelfde vereisten gelden voor het repliceert tooAzure fysieke servers of tooa secundaire site.


Houd er rekening mee dat er fysieke servers als virtuele machines in Azure wordt uitgevoerd als de lokale server uitvalt. Failback tooan een on-premises fysieke server wordt momenteel niet ondersteund. Voor een beveiligd als fysieke machine, kunt u alleen failback tooa VMware virtuele machine.

### <a name="what-vmware-vms-can-i-protect"></a>Welke virtuele VMware-machines kan ik beveiligen?

virtuele VMware-machines tooprotect moet u een vSphere-hypervisor en virtuele machines waarop VMware tools. Ook wordt aangeraden dat u een VMware vCenter server toomanage Hallo hypervisors hebt. [Meer informatie](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) over de juiste vereisten voor het repliceren van VMware-servers en virtuele machines tooAzure of tooa secundaire site.


### <a name="can-i-manage-disaster-recovery-for-my-branch-offices-with-site-recovery"></a>Kan ik met Site Recovery herstel na noodgeval voor mijn filialen beheren?
Ja. Wanneer u Site Recovery tooorchestrate replicatie en failover in uw filialen, krijgt u een uniforme orchestration en de weergave van alle werkbelastingen van uw branch office op een centrale locatie. U kunt eenvoudig failovers uitvoeren en herstel na noodgevallen voor alle filialen van uw hoofdkantoor zonder Hallo vertakkingen beheren.

## <a name="pricing"></a>Prijzen

### <a name="what-charges-do-i-incur-while-using-azure-site-recovery"></a>Welke kosten gebruik ik tijdens het gebruik van Azure Site Recovery?
Wanneer u Site Recovery gebruikt, kosten u die voor de Site Recovery-licentie hello, Azure storage, opslagtransacties en uitgaande gegevensoverdracht. [Meer informatie](https://azure.microsoft.com/pricing/details/site-recovery).

Hallo Site Recovery-licentie is per beveiligde exemplaar, waarbij een exemplaar een virtuele machine of een fysieke server is.

- Als de schijf van een virtuele machine tooa standard-opslagaccount repliceert, is bedoeld voor Hallo opslagverbruik hello Azure storage-kosten. Bijvoorbeeld, als Hallo bron schijfomvang is 1 TB en 400 GB wordt gebruikt, maakt Site Recovery een 1 TB VHD in Azure, maar Hallo opslag in rekening gebracht is 400 GB (plus Hallo en de hoeveelheid opslagruimte die wordt gebruikt voor replicatielogboeken).
- Als de schijf van een virtuele machine tooa premium storage-account repliceert, is hello Azure storage-kosten voor de opslaggrootte Hallo ingericht, afgerond uit voor Hallo dichtstbijzijnde premium-opslag-schijfoptie. Als Hallo bron schijfgrootte 50 GB, maakt u een schijf van 50 GB in Azure Site Recovery en Azure wijst deze toohello dichtstbijzijnde schijf voor premium-opslag (P10).  Kosten berekend op P10 en niet op Hallo 50 GB schijfgrootte.  [Meer informatie](https://aka.ms/premium-storage-pricing).  Als u premium-opslag, een standaard opslagaccount voor de replicatie-logboekregistratie is ook vereist en Hallo hoeveelheid standaard opslagruimte die wordt gebruikt voor deze logboeken wordt ook in rekening gebracht.
- Er zijn geen schijven worden tot een testfailover of een failover gemaakt. Hallo replicatiestatus, kosten opslag onder de categorie 'pagina-blobs en schijf' hello volgens Hallo [opslag prijscategorie Rekenmachine](https://azure.microsoft.com/en-in/pricing/calculator/) zijn gemaakt. Deze kosten zijn gebaseerd op Hallo opslagtype van premium/standaard- en Hallo gegevensredundantie Typ - LRS, GRS, RA-GRS enzovoort.
- Als Hallo optie toouse schijven die worden beheerd op een failover is geselecteerd, [kosten voor beheerde schijven](https://azure.microsoft.com/en-in/pricing/details/managed-disks/) toegepast na de failover van een failover en testen. Kosten zijn niet van toepassing tijdens de replicatie schijven die worden beheerd.
- Als Hallo optie toouse beheerd schijven op een failover niet is ingeschakeld, kosten opslag onder de categorie 'pagina-blobs en schijf' hello volgens Hallo [opslag prijscategorie Rekenmachine](https://azure.microsoft.com/en-in/pricing/calculator/) zijn gemaakt na een failover. Deze kosten zijn gebaseerd op Hallo opslagtype van premium/standaard- en Hallo gegevensredundantie Typ - LRS, GRS, RA-GRS enzovoort.
- Opslagtransacties in rekening worden gebracht tijdens de replicatie van de actieve status en voor standaardbewerkingen VM na een failover-failover testen. Maar deze kosten verwaarloosbaar zijn.

Ook worden kosten tijdens de testfailover, waarbij de kosten van Hallo VM, opslag, uitgaande en opslag transacties worden toegepast.



## <a name="security"></a>Beveiliging
### <a name="is-replication-data-sent-toohello-site-recovery-service"></a>Replicatiegegevens toohello Site Recovery-service verzonden?
Nee, Site Recovery gerepliceerde gegevens niet onderscheppen en heeft geen informatie over wat er op uw virtuele machines of fysieke servers wordt uitgevoerd.
Er worden alleen replicatiegegevens uitgewisseld tussen uw on-premises Hyper-V-hosts, VMware-hypervisors of fysieke servers en de Azure-opslag of uw secundaire site. Site Recovery heeft geen mogelijkheid toointercept die gegevens. Alleen Hallo metagegevens nodig tooorchestrate replicatie en failover toohello Site Recovery-service wordt verzonden.  

Site Recovery is ISO 27001: 2013, 27018, HIPAA, DPA gecertificeerd en is bezig Hallo van SOC2 en FedRAMP JAB-beoordelingen.

### <a name="for-compliance-reasons-even-our-on-premises-metadata-must-remain-within-hello-same-geographic-region-can-site-recovery-help-us"></a>Om wettelijke redenen zelfs de metagegevens van onze lokale moet blijven binnen Hallo dezelfde geografische regio. Site Recovery kan helpen ons?
Ja. Wanneer u een Site Recovery-kluis in een regio maakt, zorgt u ervoor dat alle metagegevens die we nodig tooenable en organisatie van replicatie en failover blijft binnen die regio's geografische grens.

### <a name="does-site-recovery-encrypt-replication"></a>Wordt replicatie met Site Recovery versleuteld?
Voor virtuele machines en fysieke servers wordt repliceren tussen lokale sites van versleuteling in doorvoer ondersteund. Voor virtuele machines en fysieke servers repliceren tooAzure, zowel versleuteling in de doorvoer en [versleuteling in rust (in Azure)](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) worden ondersteund.

## <a name="replication"></a>Replicatie

### <a name="can-i-replicate-over-a-site-to-site-vpn-tooazure"></a>Kan ik repliceren via een site-naar-site VPN-tooAzure?
Azure Site Recovery repliceert gegevens tooan Azure storage-account via een openbaar eindpunt. Replicatie is niet via een VPN site-naar-site. U kunt een VPN site-naar-site maken met een Azure-netwerk. Dit verstoren replicatie van Site Recovery niet.

### <a name="can-i-use-expressroute-tooreplicate-virtual-machines-tooazure"></a>Kan ik ExpressRoute tooreplicate virtuele machines tooAzure gebruiken?
ExpressRoute kan Ja, gebruikte tooreplicate virtuele machines tooAzure zijn. Azure Site Recovery repliceert gegevens tooan Azure Storage-Account via een openbaar eindpunt. U nodig hebt tooset [openbare peering](../expressroute/expressroute-circuit-peerings.md#public-peering) toouse ExpressRoute voor replicatie van Site Recovery. Nadat Hallo virtuele machines zijn is niet via tooan virtuele Azure-netwerk kunt u deze kunt openen met behulp van Hallo [privépeering](../expressroute/expressroute-circuit-peerings.md#private-peering) setup Hello virtuele Azure-netwerk.

### <a name="are-there-any-prerequisites-for-replicating-virtual-machines-tooazure"></a>Zijn er vereisten voor het repliceren van virtuele machines tooAzure?
Virtuele machines die u wilt dat tooreplicate tooAzure moeten voldoen aan [Azure-vereisten](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

Uw Azure gebruikersaccount moet toohave bepaalde [machtigingen](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replicatie van een nieuwe virtuele machine tooAzure.

### <a name="can-i-replicate-hyper-v-generation-2-virtual-machines-tooazure"></a>Kan ik tooAzure van Hyper-V generation 2 virtuele machines repliceren?
Ja. Site Recovery converteert van generatie 2 toogeneration 1 tijdens failover. Bij de failback is Hallo machine geconverteerde back toogeneration 2. [Lees meer](http://azure.microsoft.com/blog/2015/04/28/disaster-recovery-to-azure-enhanced-and-were-listening/).

### <a name="if-i-replicate-tooazure-how-do-i-pay-for-azure-vms"></a>Als ik tooAzure hoe betaal ik voor virtuele Azure-machines repliceren?
Tijdens een normale replicatie gegevens zijn gerepliceerde toogeo-redundante Azure-opslag en hoeft u geen toopay eventuele kosten van de virtuele machine Azure IaaS bieden een groot voordeel. Bij het uitvoeren van een failover-tooAzure Site Recovery automatisch maakt Azure IaaS virtuele machines en daarna moet u gefactureerd voor het Hallo-rekenresources die u in Azure verbruikt.

### <a name="can-i-automate-site-recovery-scenarios-with-an-sdk"></a>Kan ik Site Recovery-scenario's met een SDK automatiseren?
Ja. U kunt met Hallo Rest-API of PowerShell Hallo-SDK van Azure Site Recovery-werkstromen automatiseren. Ondersteunde scenario's voor de implementatie van Site Recovery met behulp van PowerShell:

* [Hyper-V-machines repliceren in VMMs clouds tooAzure PowerShell Resource Manager](site-recovery-vmm-to-azure-powershell-resource-manager.md)
* [Hyper-V-machines repliceren zonder VMM tooAzure PowerShell Resource Manager](site-recovery-deploy-with-powershell-resource-manager.md)

### <a name="if-i-replicate-tooazure-what-kind-of-storage-account-do-i-need"></a>Als ik repliceer tooAzure wat voor soort opslagaccount heb ik nodig?
* **Klassieke Azure-portal**: als u Site Recovery in de klassieke Azure-portal Hallo implementeert, moet u een [standaard geografisch redundante opslagaccount](../storage/common/storage-redundancy.md#geo-redundant-storage). Premium-opslag wordt momenteel niet ondersteund. Hallo-account moet zich in Hallo dezelfde regio bevinden als Hallo Site Recovery-kluis.
* **Azure-portal**: als u Site Recovery in hello Azure-portal implementeert, moet u een LRS of GRS-opslagaccount. GRS wordt aanbevolen, zodat gegevens robuuste als een regionale uitval of als de primaire regio Hallo kan niet worden hersteld. Hallo-account moet zich in Hallo dezelfde regio bevinden als Hallo Recovery Services-kluis. Premium-opslag wordt nu ondersteund voor VMware VM, Hyper-V-machine en replicatie van de fysieke server, wanneer u Site Recovery in hello Azure-portal implementeert.

### <a name="how-often-can-i-replicate-data"></a>Hoe vaak kan ik gegevens repliceren?
* **Hyper-V:** Hyper-V-machines kunnen elke 30 seconden (met uitzondering van premium-opslag), 5 minuten of 15 minuten worden gerepliceerd. Als u de SAN-replicatie hebt ingesteld zijn replicatie is synchroon.
* **VMware en fysieke servers:** hier is de replicatiefrequentie niet relevant. Replicatie is continue.

### <a name="can-i-extend-replication-from-existing-recovery-site-tooanother-tertiary-site"></a>Kan ik Breid replicatie uit bestaande site tooanother tertiaire herstelsite?
Uitgebreide of gekoppelde replicatie wordt niet ondersteund. Deze functie in aanvragen [Feedbackforum](http://feedback.azure.com/forums/256299-site-recovery/suggestions/6097959-support-for-exisiting-extended-replication).

### <a name="can-i-do-an-offline-replication-hello-first-time-i-replicate-tooazure"></a>Kan ik een offline replicatie Hallo eerst die ik tooAzure repliceren?
Nee, dit wordt niet ondersteund. Aanvragen van deze functie in Hallo [Feedbackforum](http://feedback.azure.com/forums/256299-site-recovery/suggestions/6227386-support-for-offline-replication-data-transfer-from).

### <a name="can-i-exclude-specific-disks-from-replication"></a>Kan ik bepaalde schijven uitsluiten van replicatie?
Dit wordt ondersteund wanneer u klaar [repliceren van virtuele VMware-machines en Hyper-V-machines](site-recovery-exclude-disk.md) tooAzure, met behulp van hello Azure-portal.

### <a name="can-i-replicate-virtual-machines-with-dynamic-disks"></a>Kan ik virtuele machines met dynamische schijven repliceren?
Dynamische schijven worden ondersteund bij het repliceren van virtuele Hyper-V-machines. Ze worden ook ondersteund bij het repliceren van virtuele VMware-machines en fysieke machines tooAzure. Hallo-besturingssysteemschijf moet een standaardschijf zijn.

### <a name="can-i-add-a-new-machine-tooan-existing-replication-group"></a>Kan ik een nieuwe machine tooan bestaande replicatiegroep toevoegen?
Het toevoegen van nieuwe machines tooexisting-replicatiegroepen wordt ondersteund. toodo dus replicatiegroep hello (van 'Gerepliceerde items' blade) en klik met de rechtermuisknop/Selecteer contextmenu op Hallo replicatiegroep selecteren en selecteer de relevante optie Hallo.

![Tooreplication groep toevoegen](./media/site-recovery-faq/add-server-replication-group.png)

### <a name="can-i-throttle-bandwidth-allotted-for-hyper-v-replication-traffic"></a>Kan ik de bandbreedte beperken die is toegewezen voor Hyper-V-replicatieverkeer?
Ja. Meer informatie over het beperken van de bandbreedte in Hallo artikelen over implementatie:

* [Capaciteitsplanning voor het repliceren van virtuele VMware-machines en fysieke servers](site-recovery-plan-capacity-vmware.md)
* [Capaciteitsplanning voor het repliceren van Hyper-V-machines in VMM-clouds](site-recovery-vmm-to-azure.md#capacity-planning)
* [Capaciteitsplanning voor het repliceren van Hyper-V-machines zonder VMM](site-recovery-hyper-v-site-to-azure.md)

## <a name="failover"></a>Failover
### <a name="if-im-failing-over-tooazure-how-do-i-access-hello-azure-virtual-machines-after-failover"></a>Als ik ben tooAzure failover, hoe krijg ik toegang tot hello Azure virtuele machines na een failover?
U kunt toegang tot hello Azure VM's via een beveiligde internetverbinding, via een site-naar-site VPN of via Azure ExpressRoute. U moet een aantal zaken in volgorde tooconnect tooprepare. [Meer informatie](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover)


### <a name="if-i-fail-over-tooazure-how-does-azure-make-sure-my-data-is-resilient"></a>Als ik tooAzure hoe Azure ervoor zorgen dat een failover is mijn gegevens tegen?
Azure is ontworpen voor herstelbaarheid. Site Recovery voert automatisch een failover tooa secundaire datacenter Azure, in overeenstemming met hello Azure SLA als Hallo moet zich voordoet. Als dit gebeurt, we ervoor dat uw metagegevens zorgen en kluizen binnen Hallo blijven dezelfde geografische regio die u voor uw kluis hebt gekozen.  

### <a name="if-im-replicating-between-two-datacenters-what-happens-if-my-primary-datacenter-experiences-an-unexpected-outage"></a>Als ik repliceer tussen twee datacentra wat gebeurt er als mijn primaire datacenter een stroomstoring optreedt?
U kunt een niet-geplande failover van de secundaire site Hallo activeren. Site Recovery nodig niet voor connectiviteit van Hallo primaire site tooperform Hallo failover.

### <a name="is-failover-automatic"></a>Vindt failover automatisch plaats?
Failover wordt niet automatisch uitgevoerd. U start een failover met één klik in de portal Hallo of kunt u [Site Recovery PowerShell](/powershell/module/azurerm.siterecovery) tootrigger een failover. Terug mislukt, is een eenvoudige actie in Hallo Site Recovery-portal.

tooautomate die kunt u on-premises Orchestrator of Operations Manager toodetect een storing van de virtuele machine, en vervolgens trigger Hallo failover met behulp van Hallo SDK.

* [Lees meer](site-recovery-create-recovery-plans.md) over plannen voor herstel.
* [Lees meer](site-recovery-failover.md) over failover.
* [Lees meer](site-recovery-failback-azure-to-vmware.md) over mislukte back-VMware-machines en fysieke servers

### <a name="if-my-on-premises-host-is-not-responding-or-crashed-can-i-failover-back-tooa-different-host"></a>Als mijn lokale host niet reageert of vastgelopen, kan ik failover tooa back andere host?
Ja, kunt u Hallo alternatieve locatie toofailback tooa verschillende herstelhost van Azure. Lees meer over opties voor Hallo in Hallo onderstaande koppelingen voor VMware en Hyper-v virtuele machines.

* [Voor virtuele VMware-machines](site-recovery-how-to-failback-azure-to-vmware.md#fail-back-to-the-original-or-alternate-location)
* [Voor Hyper-v virtuele machines](site-recovery-failback-from-azure-to-hyper-v.md#failback-to-an-alternate-location)

## <a name="service-providers"></a>Serviceproviders
### <a name="im-a-service-provider-does-site-recovery-work-for-dedicated-and-shared-infrastructure-models"></a>Ik ben een serviceprovider. Werkt Site Recovery voor toegewezen als gedeelde infrastructuurmodellen?
Ja, Site Recovery werkt voor zowel toegewezen als gedeelde infrastructuurmodellen.

### <a name="for-a-service-provider-is-hello-identity-of-my-tenant-shared-with-hello-site-recovery-service"></a>Is voor een serviceprovider Hallo identiteit van mijn tenants gedeeld met Hallo Site Recovery-service?
Nee. Tenant-identiteit blijft anonieme. Uw tenants hoeft geen toegang tot toohello Site Recovery-portal. Alleen Hallo provider servicebeheerder communiceert met de Hallo-portal.

### <a name="will-tenant-application-data-ever-go-tooazure"></a>Gaat tenant toepassingsgegevens ooit tooAzure?
Bij het repliceren tussen sites van serviceproviders, toepassingsgegevens nooit tooAzure. Gegevens worden in transit en rechtstreeks gerepliceerd tussen sites van serviceproviders Hallo versleuteld.

Als u tooAzure repliceert, worden toepassingsgegevens verzonden tooAzure opslag, maar niet toohello Site Recovery-service. Gegevens in transit is versleuteld en blijven versleuteld in Azure.

### <a name="will-my-tenants-receive-a-bill-for-any-azure-services"></a>Ontvangen mijn tenants een factuur voor Azure-services?
Nee. Azure facturering relatie is rechtstreeks met de Hallo-serviceprovider. Serviceproviders zijn zelf verantwoordelijk voor het genereren van facturen voor hun tenants.

### <a name="if-im-replicating-tooazure-do-we-need-toorun-virtual-machines-in-azure-at-all-times"></a>Als ik repliceer tooAzure, hebben we nodig toorun virtuele machines in Azure te allen tijde?
Nee, gegevens gerepliceerde tooan Azure storage-account in uw abonnement is. Wanneer u een failovertest (details voor DR) of een werkelijke failover uitvoert, maakt Site Recovery automatisch virtuele machines in uw abonnement.

### <a name="do-you-ensure-tenant-level-isolation-when-i-replicate-tooazure"></a>Kunt u isolatie op tenantniveau wanneer ik repliceer tooAzure zorgen?
Ja.

### <a name="what-platforms-do-you-currently-support"></a>Welke platforms worden er momenteel ondersteund?
We bieden ondersteuning voor Azure Pack, Cloud Platform System en System Center gebaseerde (2012 en hoger)-implementaties. [Meer informatie](https://technet.microsoft.com/library/dn850370.aspx) over de integratie van Azure Pack en de Site Recovery.

### <a name="do-you-support-single-azure-pack-and-single-vmm-server-deployments"></a>Worden implementaties van één Azure Pack en één VMM-server ondersteund?
Ja, kunt u Hyper-V virtuele machines tooAzure, repliceren of tussen sites van serviceproviders.  Houd er rekening mee dat als u tussen sites van serviceproviders repliceert, Azure-runbookintegratie niet beschikbaar.

## <a name="next-steps"></a>Volgende stappen
* Lees Hallo [Site Recovery-overzicht](site-recovery-overview.md)
* Informatie over de [Site Recovery-architectuur](site-recovery-components.md)  
