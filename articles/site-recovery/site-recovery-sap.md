---
title: een meerlaagse SAP NetWeaver toepassingsimplementatie met Azure Site Recovery aaaProtect | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooprotect SAP NetWeaver toepassingsimplementaties met behulp van Azure Site Recovery
services: site-recovery
documentationcenter: 
author: mayanknayar
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: manayar
ms.openlocfilehash: 34651c7b14d23a44005372f4f923c401e0224231
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="protect-a-multi-tier-sap-netweaver-application-deployment-using-azure-site-recovery"></a>Een meerlaagse SAP NetWeaver toepassingsimplementatie met Azure Site Recovery beveiligen

De meeste implementaties van grote en middelgrote SAP hebben enige vorm van oplossing voor herstel na noodgevallen.  Hallo belang van oplossingen voor robuuste en testable herstel na noodgevallen is toegenomen als u meer kernactiviteiten processen zijn verplaatst tooapplications zoals SAP.  Azure Site Recovery is getest en geïntegreerd met SAP-toepassingen en Hallo-mogelijkheden van de meeste oplossingen on-premises herstel na noodgevallen, op een lagere totale eigendomskosten (TCO) dan concurrerende oplossingen overschrijdt.
Met Azure Site Recovery kunt u het volgende doen:
* Schakel de beveiliging van toepassingen voor SAP NetWeaver en NetWeaver productie uitvoeren van de on-premises onderdelen tooAzure repliceren.
* Schakel de beveiliging van toepassingen voor SAP NetWeaver en NetWeaver productie met Azure, met het repliceren van onderdelen tooanother Azure-datacenter.
* Vereenvoudig de cloudmigratie, met behulp van Site Recovery toomigrate uw tooAzure SAP-implementatie.
* Vereenvoudig SAP-projectupgrades, tests en het maken van prototypen door een on-demand een productiekloon te maken voor het testen van SAP-toepassingen.

Dit artikel wordt beschreven hoe tooprotect SAP NetWeaver toepassingsimplementaties met behulp van [Azure Site Recovery](site-recovery-overview.md). In dit artikel bevat informatie over aanbevolen procedures voor het beveiligen van een implementatie van de drie lagen SAP NetWeaver in Azure door te repliceren tooanother Azure-datacenter met Azure Site Recovery Hallo ondersteund scenario's en configuraties, Hallo en hoe tooperform failovers, die beide testen failovers (noodhersteloefeningen) en de werkelijke failovers.


## <a name="prerequisites"></a>Vereisten
Voordat u begint, zorg er dan voor dat u begrijpt Hallo volgende:

1. [Een virtuele machine tooAzure repliceren](azure-to-azure-walkthrough-enable-replication.md)
2. Hoe te[ontwerpen van een netwerk herstel](site-recovery-azure-to-azure-networking-guidance.md)
3. [Tijdens het doorzoeken van een failover-test tooAzure](azure-to-azure-walkthrough-test-failover.md)
4. [Tijdens het doorzoeken van een failover-tooAzure](site-recovery-failover.md)
5. Hoe te[repliceren van een domeincontroller](site-recovery-active-directory.md)
6. Hoe te[SQL-Server repliceren](site-recovery-sql.md)

## <a name="supported-scenarios"></a>Ondersteunde scenario 's
Met Azure Site Recovery kunt u een oplossing van het herstel na noodgevallen voor Hallo volgen scenario's implementeren:
* SAP-systemen die zijn uitgevoerd in een Azure-datacenter repliceren tooanother Azure-datacenter (Azure naar Azure DR), zoals ontworpen [hier](https://aka.ms/asr-a2a-architecture).
* SAP-systemen die zijn uitgevoerd op servers met VMWare (of fysiek) lokale replicerende tooa DR-site in een Azure-datacenter (VMware naar Azure DR), waarvoor een aantal extra onderdelen zoals ontworpen [hier](https://aka.ms/asr-v2a-architecture).
* SAP-systemen waarop Hyper-V lokale replicerende tooa DR-site in een Azure-datacenter (Hyper-V-Azure DR), waarvoor een aantal extra onderdelen zoals ontworpen [hier](https://aka.ms/asr-h2a-architecture).

Dit document maakt gebruik van Hallo eerste case - Azure naar Azure DR - toodemonstrate van Azure Site Recovery SAP disaster recovery mogelijkheden. Zoals Azure Site Recovery-replicatie networkdirect toepassing is, is het Hallo-proces dat wordt beschreven verwachte toohold voor andere scenario's ook.

### <a name="required-foundation-services"></a>Vereiste foundation-services
Dit scenario documentatie alle is geïmplementeerd met Hallo foundation-services geïmplementeerd te volgen:
* ExpressRoute of Site-naar-Site virtueel particulier netwerk (VPN)
* Ten minste één Active Directory-domeincontroller en DNS-server worden uitgevoerd in Azure

Het is raadzaam dat die hierboven Hallo-infrastructuur is tot stand gebrachte voorafgaande toodeploying Azure Site Recovery.


## <a name="typical-sap-application-deployment"></a>Typische toepassing SAP-implementatie
Grote SAP-klanten wordt meestal tussen 6 too20 afzonderlijke SAP-toepassingen implementeren.  De meeste van deze toepassingen zijn gebaseerd op Hallo SAP NetWeaver ABAP of Java-engines.  Ondersteuning van deze toepassingen van de NetWeaver core zijn veel kleiner specifieke niet - NetWeaver SAP zelfstandige motoren en doorgaans een aantal niet-SAP-toepassingen.  

Kritieke tooinventory alle Hallo SAP toepassingen worden uitgevoerd in een liggend en toodetermine Hallo implementatiemodus (laag 2 of 3-laagse), versies, patches, grootte en verloop tarieven en vereisten voor de persistentie schijf is.

![Patroon van de implementatie](./media/site-recovery-sap/sap-typical-deployment.png)

Hallo SAP databaselaag persistentie moet worden beveiligd via Hallo systeemeigen DBMS's zoals SQL Server AlwaysOn, Oracle DataGuard of HANA System Replication. Hallo clientlaag ook niet wordt beveiligd door Azure Site Recovery, maar het is belangrijk tooconsider onderwerpen die invloed zijn op deze laag zoals DNS-servers vertraging, beveiliging en externe toegang toohello DR datacenter.

Azure Site Recovery is Hallo aanbevolen oplossing voor de toepassingslaag hello, met inbegrip van (A) SCS. Andere toepassingen zoals NetWeaver SAP-toepassingen en toepassingen niet SAP deel uitmaken van Hallo algemene SAP implementatieomgeving en moet ook worden beveiligd met Azure Site Recovery.

## <a name="replicate-virtual-machines"></a>Virtuele machines repliceren
Ga als volgt [in deze richtlijnen](azure-to-azure-walkthrough-enable-replication.md) toostart repliceren van alle Hallo SAP toepassing virtuele machines toohello Azure DR-datacenter.

Als u een statisch IP-adres gebruikt, kunt u Hallo IP die u wilt dat virtuele machine tootake in Hallo Network interface-kaarten sectie in de berekenings-en netwerkinstellingen Hallo opgeven.

![Doel-IP](./media/site-recovery-sap/sap-static-ip.png)


## <a name="creating-a-recovery-plan"></a>Een herstelplan maken
Een herstelplan kunt Hallo failover van de verschillende lagen in een toepassing met meerdere lagen, daarom toepassing consistentie van de sequentiëren. Volg stappen Hallo [hier](site-recovery-create-recovery-plans.md) tijdens het maken van een herstelplan voor een webtoepassing met meerdere lagen.

### <a name="adding-scripts-toohello-recovery-plan"></a>Het herstelplan toohello toe te voegen scripts
Mogelijk moet u toodo bepaalde bewerkingen op Hallo failover voor virtuele Azure-machines na failover en testen voor uw toepassingen toofunction correct. U kunt automatiseren Hallo post failoverbewerking zoals het bijwerken van DNS-vermelding en bindingen en verbindingen, wijzigen door de bijbehorende scripts toevoegen in het herstelplan Hallo zoals beschreven in [in dit artikel](site-recovery-create-recovery-plans.md#add-scripts).

### <a name="dns-update"></a>DNS-updates
Als Hallo DNS is geconfigureerd voor dynamische DNS-updates vervolgens Hallo DNS virtuele machines meestal met de nieuwe IP-adres Hallo werkt zodra ze starten. Als u wilt dat een expliciete stap tooupdate DNS-Hello tooadd nieuwe IP-adressen van virtuele machines van Hallo voegt u dit [tooupdate IP-adres in DNS-script](https://aka.ms/asr-dns-update) als een post-actie op herstel planningsgroepen.  

## <a name="example-azure-to-azure-deployment"></a>Voorbeeld van een Azure-Azure-implementatie
In het diagram hieronder hello Azure Site Recovery Azure naar Azure herstel na noodgevallen hello wordt beschreven:
* Hallo primaire Datacenter Singapore (Azure Zuidoost-Azië wordt) en Hallo DR datacenter is Hongkong (Azure Oost-Azië).  In dit scenario wordt lokale beschikbaarheid verstrekt wanneer er twee virtuele machines waarop SQL Server AlwaysOn wordt uitgevoerd in synchrone modus in Singapore.
* Hallo File Share ASC's kan gebruikte tooprovide HA voor Hallo SAP individuele storingspunten zijn. File Share ASC's vereist een gedeelde clusterschijf geen en toepassingen zoals SIOS zijn niet vereist.
* DR-beveiliging voor Hallo DBMS laag wordt bereikt met behulp van asynchrone replicatie.
* Dit scenario bevat 'symmetrisch DR' – een term gebruikt toodescribe een DR-oplossing die een exacte replica van de productie, daarom Hallo DR SQL Server-oplossing heeft voor lokale beschikbaarheid. Hallo gebruik van symmetrische Noodherstel is niet verplicht voor Hallo databaselaag en veel klanten gebruikmaken van Hallo flexibiliteit van cloud-implementaties toobuild een lokaal hoge Beschikbaarheidsknooppunt snel na een DR-gebeurtenis.
* Hallo diagram ziet u Hallo SAP NetWeaver ASC's en server toepassingslaag gerepliceerd door Azure Site Recovery.

![Replicatiescenario](./media/site-recovery-sap/sap-replication-scenario.png)

## <a name="doing-a-test-failover"></a>Een testfailover uitvoeren
Ga als volgt [in deze richtlijnen](azure-to-azure-walkthrough-test-failover.md) toodo een testfailover.

1.  Ga tooAzure portal en selecteer de Recovery Services-kluis.
2.  Klik op Hallo herstelplan is gemaakt voor SAP-toepassingen (s).
3.  Klik op 'Testfailover'.
4.  Selecteer herstelpunt en het virtuele netwerk van Azure toostart Hallo test failover-proces.
5.  Wanneer secundaire Hallo-omgeving is, kunt u uw validaties kunt uitvoeren.
6.  Als Hallo validaties voltooid zijn, klik op 'Opschonen testfailover' en tooclean Hallo failover-omgeving.

## <a name="doing-a-failover"></a>U een failover uitvoert
Ga als volgt [in deze richtlijnen](site-recovery-failover.md) bij het uitvoeren van een failover.

1.  Ga tooAzure portal en selecteer de Recovery Services-kluis.
2.  Klik op Hallo herstelplan is gemaakt voor SAP-toepassingen.
3.  Klik op 'Failover'.
4.  Selecteer herstelproces punt toostart Hallo failover.

## <a name="next-steps"></a>Volgende stappen
Meer informatie over het bouwen van een noodherstel voor SAP NetWeaver implementaties met Azure Site Recovery in [dit technisch document](http://aka.ms/asr-sap). Hallo technisch document ook aanbevelingen voor verschillende SAP-architecturen wordt beschreven, een lijst van ondersteunde toepassingen en VM-typen voor SAP op Azure en beschrijft mogelijke Testplannen voor uw noodherstel.

Meer informatie over [repliceren van andere werkbelastingen](site-recovery-workload.md) met Site Recovery.
