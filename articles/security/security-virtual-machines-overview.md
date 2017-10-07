---
title: beveiligingsfuncties aaaAzure gebruikt met virtuele machines in Azure | Microsoft Docs
description: " Een overzicht van hello Azure-beveiliging kernfuncties die kunnen worden gebruikt met virtuele machines in Azure. Azure VM's geven u Hallo flexibiliteit van virtualisatie zonder toobuy en onderhouden van Hallo fysieke hardware die Hallo VM wordt uitgevoerd. "
services: security
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: TomSh
ms.assetid: 467b2c83-0352-4e9d-9788-c77fb400fe54
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/04/2017
ms.author: terrylan
ms.openlocfilehash: 1a1b9f02bd82a2655f4e2e5d9f9ce7a6671f63fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-security-overview"></a>Overzicht van de beveiliging Azure virtuele Machines
Met Azure Virtual Machines kunt u een brede reeks computeroplossingen op flexibele wijze inzetten. Met ondersteuning voor Microsoft Windows, Linux, Microsoft SQL Server, Oracle, IBM, SAP en Azure BizTalk Services kunt u elke workload en elke taal implementeren op vrijwel elk besturingssysteem.

Een virtuele machine van Azure biedt u flexibiliteit van virtualisatie zonder toobuy Hallo en onderhouden van de fysieke hardware Hallo die Hallo virtuele machine wordt uitgevoerd.  U kunt bouwen en implementeren van uw toepassingen met Hallo zekerheid dat de gegevens beveiligd en veilige de maximaal beveiligde datacenters zijn.

Met Azure, kunt u die verbeterde beveiliging, conform oplossingen bouwen:

* Uw virtuele machines beschermen tegen virussen en malware
* Gevoelige gegevens versleutelen
* Netwerkverkeer beveiligen
* Bedreigingen identificeren en detecteren
* Voldoen aan nalevingsvereisten

Hallo-doel van dit artikel is tooprovide een overzicht van hello Azure-beveiliging kernfuncties die kunnen worden gebruikt met virtuele machines. We bieden ook koppelingen tooarticles waarmee details van elk onderdeel, zodat u meer informatie.  

Hallo core virtuele Machine van Azure security mogelijkheden toobe in dit artikel aan bod:

* Antimalware
* Hardware Security Module
* Virtuele machine schijfversleuteling
* Back-up van virtuele machine
* Azure Site Recovery
* Virtuele netwerken
* Beheer van beveiligingsbeleid en rapportage
* Naleving

## <a name="antimalware"></a>Antimalware
Met Azure, kunt u antimalware-software van beveiliging leveranciers zoals Microsoft, Symantec, Trend Micro en Kaspersky tooprotect uw virtuele machines van schadelijke bestanden, adware en andere dreigingen. Zie Hallo meer meer hieronder toofind artikelen over partneroplossingen.

Microsoft Antimalware voor Azure Cloud Services en virtuele Machines is een functie real-timebeveiliging die helpt bepalen en virussen, spyware en andere schadelijke software verwijderen.  Microsoft Antimalware biedt configureerbare waarschuwingen wanneer bekende schadelijke of ongewenste software probeert tooinstall zelf of uit te op uw Azure-systemen voeren.

Microsoft Antimalware is een single-agent-oplossing voor toepassingen en tenant-omgevingen ontworpen toorun op Hallo achtergrond, zonder menselijke tussenkomst. U kunt beveiliging op basis van Hallo behoeften van uw toepassing werkbelastingen, met een eenvoudige secure--standaard of aangepaste configuratie, met inbegrip van antimalware monitoring Geavanceerd implementeren.

Wanneer u implementeert en Microsoft Antimalware inschakelt, zijn Hallo volgende kernfuncties beschikbaar:

* Real-timebeveiliging - monitors activiteit in de Cloud Services en op virtuele Machines toodetect en blok malware worden uitgevoerd.
* Geplande scan - gerichte scannen toodetect schadelijke software, inclusief actieve programma's regelmatig wordt uitgevoerd.
* Oplossen van malware - neemt actie automatisch op de gedetecteerde malware, zoals het verwijderen of schadelijke bestanden in quarantaine plaatsen en schadelijke registervermeldingen opruimen.
* Updates van de handtekening - automatisch wordt geïnstalleerd Hallo nieuwste beveiliging handtekeningen (virusdefinities) tooensure beveiliging is op de hoogte van een vooraf bepaald frequentie.
* Antimalware-Engine-updates – automatisch updates Hallo Microsoft Antimalware-engine.
* Antimalware-Platform-updates – automatisch updates Hallo Microsoft Antimalware-platform.
* Actieve beveiliging - rapporten tooAzure telemetrie metagegevens over gedetecteerde bedreigingen en verdachte resources tooensure snelle reactie en schakelt realtime synchrone handtekening levering via Hallo Microsoft Active Protection System (MAPS).
* Voorbeelden van de reporting - biedt en rapporten van voorbeelden toohello Microsoft Antimalware-service toohelp verfijnen Hallo-service en enable probleemoplossing.
* Uitsluitingen – toepassing en service beheerders tooconfigure bepaalde bestanden, processen, en stations tooexclude ze uit de beveiliging en scannen voor prestaties en andere redenen.
* Gebeurtenissen verzamelen van Antimalware - Hallo antimalware-servicestatus, verdachte activiteiten en herstelacties genomen in Hallo besturingssysteem gebeurtenislogboek vastgelegd en verzamelt ze in Azure Storage-account van de klant Hallo.

Meer informatie: Zie voor meer informatie over de antimalware-software tooprotect toolearn uw virtuele machines:

* [Microsoft Antimalware voor Azure-Cloudservices en virtuele Machines](azure-security-antimalware.md)
* [Deploying Antimalware Solutions on Azure Virtual Machines](https://azure.microsoft.com/blog/deploying-antimalware-solutions-on-azure-virtual-machines/) (Antimalware-oplossingen implementeren op virtuele machines van Azure)
* [Hoe tooinstall en Trend Micro grondige Security configureren als een Service op een virtuele machine van Windows](../virtual-machines/windows/classic/install-trend.md)
* [Hoe tooinstall en Symantec Endpoint Protection configureren op een virtuele machine van Windows](../virtual-machines/windows/classic/install-symantec.md)
* [Beveiligingsoplossingen in hello Azure Marketplace](https://azure.microsoft.com/marketplace/?term=security)

## <a name="hardware-security-module"></a>Hardware security Module
Versleuteling en authenticatie beveiligingen kunnen worden uitgebreid door sleutelbeveiliging te verbeteren. Door deze te slaan in Azure Sleutelkluis kunt u Hallo-beheer en beveiliging van uw kritieke geheimen en sleutels vereenvoudigen. Sleutelkluis biedt Hallo optie toostore uw sleutels in hardware security modules (HSM's) gecertificeerde tooFIPS 140-2 Level 2-standaarden. De versleutelingssleutels SQL Server voor back-up of [transparante gegevensversleuteling](https://msdn.microsoft.com/library/bb934049.aspx) kunnen alle worden opgeslagen in de Sleutelkluis met alle sleutels of geheimen van uw toepassingen. Machtigingen en toegang toothese beveiligde items worden beheerd via [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).

Meer informatie:

* [Wat is Azure Sleutelkluis?](../key-vault/key-vault-whatis.md)
* [Aan de slag met Azure Sleutelkluis](../key-vault/key-vault-get-started.md)
* [Azure Sleutelkluis-blog](https://blogs.technet.microsoft.com/kv/)

## <a name="virtual-machine-disk-encryption"></a>Virtuele machine schijfversleuteling
Azure Disk Encryption is een nieuwe functie waarmee u de schijven voor Windows en Linux Azure Virtual machines versleutelen. Hallo industrie-initiatief maakt gebruik van Azure Disk Encryption [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) functie van Windows en Hallo [dm-crypt](https://en.wikipedia.org/wiki/Dm-crypt) functie van Linux tooprovide volumeversleuteling voor hello OS- en gegevensschijven Hallo.

Hallo-oplossing is geïntegreerd met Azure Key Vault toohelp u controleren en beheren van Hallo schijf versleutelingssleutels en geheimen in uw abonnement sleutelkluis terwijl u ervoor zorgt dat alle gegevens in de schijven van de virtuele machine Hallo zijn versleuteld in rust in uw Azure-opslag.

Meer informatie:

* [Azure Disk Encryption for Windows and Linux IaaS VM 's](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0)
* [Azure Disk Encryption voor Linux en Windows virtuele Machines](https://blogs.msdn.microsoft.com/azuresecurity/2015/11/16/azure-disk-encryption-for-linux-and-windows-virtual-machines-public-preview-now-available/)
* [Versleutelen van een virtuele machine](../security-center/security-center-disk-encryption.md)

## <a name="virtual-machine-backup"></a>Back-up van virtuele machine
Azure Backup is een schaalbare oplossing die uw toepassingsgegevens beveiligt zonder enige kapitaalinvestering en tegen minimale bedrijfskosten. Toepassingsfouten kunnen uw gegevens beschadigen, en menselijke fouten kunnen fouten introduceren in uw toepassingen. Uw virtuele machines met Windows en Linux zijn beveiligd met Azure Backup.

Meer informatie:

* [Wat is Azure Backup?](../backup/backup-introduction-to-azure-backup.md)
* [Leertraject voor Azure Backup](https://azure.microsoft.com/documentation/learning-paths/backup/)
* [Azure Backup-Service - Veelgestelde vragen](../backup/backup-azure-backup-faq.md)

## <a name="azure-site-recovery"></a>Azure Site Recovery
Er is een belangrijk onderdeel van de BCDR-strategie van uw organisatie uitzoeken hoe tookeep zakelijke workloads en apps up en wordt uitgevoerd als geplande en niet-geplande storingen optreden. Azure Site Recovery kunnen indelen van replicatie, failovers en herstel van workloads en apps, zodat ze beschikbaar vanaf een secundaire locatie zijn als uw primaire locatie uitvalt.

Site Recovery:

* **Uw BCDR-strategie vereenvoudigt** : Site Recovery kunt u eenvoudig toohandle replicatie, failovers en herstel van meerdere zakelijke workloads en apps vanaf één locatie. Site Recovery regelt de replicatie en failovers, maar onderschept uw toepassingsgegevens niet en heeft er ook geen informatie over.
* **Biedt flexibele replicatie** : met behulp van Site Recovery kunt u workloads die worden uitgevoerd op Hyper-V virtuele machines, virtuele VMware-machines en fysieke Windows of Linux-servers repliceren.
* **Biedt ondersteuning voor failover en herstel** : Site Recovery biedt testfailovers toosupport noodhersteloefeningen zonder productieomgevingen. Bovendien kunt u bij verwachte uitval geplande failovers uitvoeren zonder gegevensverlies, en bij onverwachte noodsituaties ongeplande failovers met minimaal gegevensverlies (afhankelijk van de replicatiefrequentie). Na een failover kunt u failback tooyour primaire sites. De herstelplannen van Site Recovery kunnen scripts en Azure Automation-werkmappen bevatten, zodat u failovers en het herstel van toepassingen met meerdere lagen naar behoefte kunt aanpassen.
* **Secundair datacenter elimineert** , kunt u tooa secundaire on-premises site of tooAzure repliceren. Met behulp van Azure als bestemming voor herstel na noodgevallen elimineert Hallo kosten en complexiteit van het onderhouden van een secundaire site. Gerepliceerde gegevens worden opgeslagen in Azure Storage.
* **Kan worden geïntegreerd met bestaande BCDR-technologieën** : Site Recovery werkt samen met andere toepassing BCDR-functies. U kunt bijvoorbeeld de Site Recovery tooprotect Hallo SQL Server back-end van zakelijke workloads. Dit biedt systeemeigen ondersteuning voor SQL Server AlwaysOn toomanage Hallo failovers van beschikbaarheidsgroepen.

Meer informatie:

* [Wat is Azure Site Recovery?](../site-recovery/site-recovery-overview.md)
* [Hoe werkt Azure Site Recovery?](../site-recovery/site-recovery-components.md)
* [Wat werkbelastingen zijn beveiligd door Azure Site Recovery?](../site-recovery/site-recovery-workload.md)

## <a name="virtual-networking"></a>Virtuele netwerken
Verbinding met het netwerk, moeten virtuele machines. toosupport is vereist dat dit vereiste, Azure virtuele machines toobe verbonden tooan Azure Virtual Network. Een Azure-netwerk is een logische constructie die is gebouwd op Hallo fysieke netwerk van Azure-infrastructuur. Elke logische Azure Virtual Network is geïsoleerd van alle andere virtuele netwerken van Azure. Deze isolatie kunt zorgen dat het netwerkverkeer in uw implementaties is niet toegankelijk tooother Microsoft Azure-klanten.

Meer informatie:

* [Overzicht van Azure-netwerk-beveiliging](security-network-overview.md)
* [Overzicht van Virtual Network](../virtual-network/virtual-networks-overview.md)
* [Netwerkfuncties en samenwerking voor zakelijke scenario 's](https://azure.microsoft.com/blog/networking-enterprise/)

## <a name="security-policy-management-and-reporting"></a>Beheer van beveiligingsbeleid en rapportage
Azure Security Center helpt u bij het detecteren, voorkomen van en reageren toothreats en biedt dat u grotere zichtbaarheid van, en controle over, Hallo beveiliging van uw Azure-resources. Het biedt geïntegreerde beveiligingsbewaking en beleidsbeheer voor uw Azure-abonnementen, helpt bedreigingen te detecteren die anders onopgemerkt zouden blijven, en werkt met een uitgebreid ecosysteem van beveiligingsoplossingen.

Azure Security Center helpt u te optimaliseren en beveiliging van de virtuele machine door te controleren:

* Virtuele machine biedt [beveiligingsaanbevelingen](../security-center/security-center-recommendations.md) zoals toepassing systeemupdates, eindpunten ACL's configureren, antimalware inschakelen netwerkbeveiligingsgroepen inschakelen en schijfversleuteling van toepassing.
* Hallo-status van uw virtuele machines controleren

Meer informatie:

* [Inleiding tooAzure Security Center](../security-center/security-center-intro.md)
* [Veelgestelde vragen over Azure Security Center](../security-center/security-center-faq.md)
* [Azure Security Center plannen en bewerkingen](../security-center/security-center-planning-and-operations-guide.md)

## <a name="compliance"></a>Naleving
Virtuele Machines in Azure is gecertificeerd voor FISMA, FedRAMP HIPAA, PCI DSS-niveau 1 en andere belangrijke naleving programma's. Deze certificeringsinstantie gemakkelijker voor de nalevingsvereisten van uw eigen Azure-toepassingen toomeet en voor uw zakelijke tooaddress een breed scala aan nationale en internationale voorschriften.

Meer informatie:

* [Microsoft Trust Center: naleving](https://www.microsoft.com/TrustCenter/Compliance/default.aspx)
* [Vertrouwde Cloud: Microsoft Azure-beveiliging, Privacy en naleving](http://download.microsoft.com/download/1/6/0/160216AA-8445-480B-B60F-5C8EC8067FCA/WindowsAzure-SecurityPrivacyCompliance.pdf)
