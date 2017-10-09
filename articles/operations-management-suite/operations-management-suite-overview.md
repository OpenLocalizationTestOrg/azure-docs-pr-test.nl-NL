---
title: aaaOperations overzicht Management Suite (OMS) | Microsoft Docs
description: Microsoft Operations Management Suite (OMS) is een cloudoplossing voor IT-beheer van Microsoft waarmee u uw on-premises en cloudinfrastructuur kunt beheren en beveiligen.  In dit artikel beschrijft Hallo-waarde van OMS Hallo verschillende services en aanbiedingen die zijn opgenomen in OMS identificeert en vindt u koppelingen tootheir gedetailleerde inhoud.
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 9dc437b9-e83c-45da-917c-cb4f4d8d6333
ms.service: operations-management-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: bwren
ms.openlocfilehash: ec3fe6d82aec46d1f715a4338f126e79e04a9147
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-operations-management-suite-oms"></a>Wat is Operations Management Suite (OMS)?
Dit artikel bevat een inleiding tooOperations Management Suite (OMS) met inbegrip van een kort overzicht van Hallo bedrijfswaarde biedt, Hallo-services en management oplossingen bevat en Hallo aanbiedingen dat samen verschillende services pakket en oplossingen.  Koppelingen zijn opgenomen toohello gedetailleerde documentatie over het implementeren en gebruiken van elke service en de oplossing.

## <a name="from-on-premises-toohello-cloud"></a>Uit lokale toohello cloud
Microsoft biedt al langere tijd producten voor het beheren van bedrijfsoplossingen.  Meerdere producten zijn samengevoegd tot Hallo System Center-productreeks management in 2007.  Deze Configuration Manager waarmee u functies zoals softwaredistributie en voorraad, Operations Manager die voorziet in proactieve controle van systemen en toepassingen, Orchestrator waaronder runbooks tooautomate handmatige processen opgenomen , en Data Protection Manager back-up en herstel van essentiële informatie.

System Center-producten ervaring met meer bronnen toohello cloud te verplaatsen, meer cloudfuncties, zoals Operations Manager en het beheren van resources in Azure Orchestrator.  Ze waren echter nog steeds primair bedoeld als on-premises oplossingen, en vereisten daarom een aanzienlijke investering in implementatie en onderhoud van een on-premises beheeromgeving.  toocompletely gebruikmaken van Hallo cloud en ondersteuning voor toekomstige toepassingen, een nieuwe benadering toomanagement is vereist.

## <a name="introducing-operations-management-suite"></a>Kennismaking met Operations Management Suite
Operations Management Suite (ook wel bekend als OMS) is een verzameling van management-services die zijn ontworpen in de cloud Hallo van Hallo starten.  In plaats van on-premises resources te implementeren en beheren, worden OMS-onderdelen volledig in Azure gehost.  De benodigde configuratie is minimaal en u kunt alles letterlijk binnen een paar minuten in werking zetten.  

- **Implementatie met minimale kosten en complexiteit.**  Omdat alle Hallo-onderdelen en -gegevens voor de OMS worden opgeslagen in Azure, kun je wel en uitgevoerd in een korte periode zonder Hallo complexiteit en de investeringen in on-premises onderdelen.
- **Schaal toocloud niveaus.**  U hebt geen tooworry over het betalen van rekenresources die u niet nodig hebt of over het uitvoeren van de opslagruimte sinds Hallo cloud kunt u toopay alleen voor wat u daadwerkelijk gebruik en tooany load die u nodig hebt kunnen gemakkelijk worden geschaald.  U kunt starten door het beheer van enkele bronnen tooget gestart en vervolgens van tooyour gehele omgeving te schalen.
- **Profiteren van de nieuwste functies Hallo.**  Er worden continu functies aan OMS toegevoegd en bestaande functies worden bijgewerkt.  U hebt voortdurend toegang toohello nieuwste functies zonder de vereiste toodeploy updates.
- **Geïntegreerde services.**  Terwijl elke Hallo OMS-services bieden aanzienlijke waarde op hun eigen, kunnen ze samenwerken toosolve complexe beheerscenario's.  Een runbook in Azure Automation kan bijvoorbeeld station van een failoverproces met Azure Site Recovery en meld u vervolgens informatie tooLog Analytics toogenerate een waarschuwing.
- **Wereldwijde kennis.**  Oplossingen voor het beheer in OMS hebben continu toegang toohello meest recente informatie.  Hallo beveiligings- en Audit oplossing kunt bijvoorbeeld een bedreiging-analyse met behulp van de nieuwste dreigingen Hallo wereld Hallo wordt gedetecteerd uitvoeren.
- **Toegang waar u ook bent.**  U hebt toegang tot uw beheeromgeving vanaf elke locatie, mits u de beschikking hebt over een browser.  Hallo OMS-app installeren op uw smartphone voor toegang tot tooyour bewakingsgegevens.

### <a name="is-it-just-for-hello-cloud"></a>Is het slechts voor Hallo cloud?
Omdat OMS-services worden uitgevoerd Hallo cloud betekent niet dat dat ze uw on-premises omgeving effectief niet beheren.  Het plaatsen van een agent op elke Windows of Linux-computer in uw datacenter en deze stuurt gegevens tooLog Analytics waarin deze kan worden geanalyseerd samen met alle andere gegevens verzameld van de cloud of on-premises services.  Azure Backup en Azure Site Recovery tooleverage Hallo cloud voor back-up en hoge beschikbaarheid voor lokale bronnen gebruiken.  
Runbooks in de cloud Hallo geen gewoonlijk toegang tot uw lokale bronnen, maar u kunt een agent installeren op een of meer computers te die fungeert als host voor runbooks in uw datacenter.  Wanneer u een runbook start, geeft u gewoon of u wilt dat deze toorun in Hallo cloud of op een lokale worker.

## <a name="hybrid-management-with-system-center"></a>Hybride beheer met System Center
Als u een bestaande installatie van System Center hebt, kunt u deze onderdelen integreren met OMS services tooprovide een hybride oplossing voor zowel uw on-premises en cloud-omgevingen gebruik te maken van de relatieve specialisaties Hallo van elk product.  Verbinding maken met uw bestaande Operations Manager management groep tooLog Analytics tooanalyze beheerde agenten in Hallo cloud.  Gebruik uw bestaande back-upproces met Data Protection Manager toobackup uw gegevens toohello cloud.  


## <a name="oms-services"></a>OMS-services
Hallo kernfunctionaliteit van OMS wordt verstrekt door een set services die worden uitgevoerd in Azure.  Elke service biedt een specifieke beheerfunctie en u kunt verschillende scenario's voor services tooachieve combineren.

|| Service | Beschrijving |
|:--|:--|:--|
| ![Log Analytics](media/operations-management-suite-overview/icon-log-analytics.png) | Log Analytics | Bewaak en analyseer Hallo beschikbaarheid en prestaties van andere bronnen, met inbegrip van fysieke en virtuele machines. |
| ![Azure Automation](media/operations-management-suite-overview/icon-automation.png) | Automatisering | Automatiseer handmatige processen en dwing configuraties af voor fysieke en virtuele machines. |
| ![Azure Backup](media/operations-management-suite-overview/icon-backup.png) | Back-up | Maak back-ups van en herstel kritieke gegevens. |
| ![Azure Site Recovery](media/operations-management-suite-overview/icon-site-recovery.png) | Site Recovery | Bied hoge beschikbaarheid voor kritieke toepassingen. |

### <a name="log-analytics"></a>Log Analytics
[Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics) biedt bewakingsservices voor OMS door in een centrale opslagplaats gegevens te verzamelen van beheerde resources.  Deze gegevens kan bevatten gebeurtenissen, prestatiegegevens of aangepaste worden geleverd via Hallo API. Zodra verzameld, zijn Hallo gegevens beschikbaar voor waarschuwingen, analyse en exporteren.  Deze methode kunt u tooconsolidate gegevens uit diverse bronnen, zodat u gegevens van uw Azure-services met uw bestaande on-premises omgeving combineren kunt.  Ook duidelijk scheidt u Hallo verzamelen van gegevens van de Hallo van Hallo actie op die van die gegevens, zodat alle acties beschikbaar tooall soorten gegevens zijn.  

![Overzicht van Log Analytics](media/operations-management-suite-overview/overview-log-analytics.png)

#### <a name="collecting-data"></a>Verzamelen van gegevens
Er zijn tal van manieren waarop u gegevens tot Hallo-opslagplaats voor logboekanalyse tooanalyze krijgen kunt.

- **Windows- of Linux-computers en -VM's.**  U Hallo Microsoft Monitoring Agent installeren op [Windows](../log-analytics/log-analytics-windows-agents.md) en [Linux](../log-analytics/log-analytics-linux-agents.md) computers of virtuele machines die u wilt dat toocollect gegevens uit.  Hallo-agent wordt automatisch downloaden van logboekanalyse configuratie waarmee gebeurtenissen en prestaties gegevens toocollect worden gedefinieerd.  U kunt eenvoudig hello agent installeren op virtuele machines worden uitgevoerd in Azure met behulp van hello Azure-portal.  Als u een bestaande Operations Manager-omgeving hebt, kunt Hallo management groep tooLog Analytics u verbinding en verzamelen van gegevens van alle bestaande agents automatisch wordt gestart.
- **Azure-services.**  Log Analytics verzamelt telemetrie van [Azure Diagnostics- en Azure-bewaking](../log-analytics/log-analytics-azure-storage.md) in Hallo opslagplaats zodat u Azure-resources kunt bewaken.
- **Gegevensverzamelaar-API.**  Log Analytics heeft een [REST-API voor het invullen van gegevens vanuit elke client](../log-analytics/log-analytics-data-collector-api.md).  Hiermee kunt u toocollect gegevens uit toepassingen van derden of aangepaste management scenario's implementeren.  Een veelgebruikte methode toouse is een runbook in Azure Automation toocollect gegevens en gebruik vervolgens Hallo Data Collector API toowrite het toohello opslagplaats.

#### <a name="reporting-and-analyzing-data"></a>Rapporteren en analyseren van gegevens
Log Analytics bevat een krachtige query language tooextract gegevens die zijn opgeslagen in de opslagplaats Hallo.  Omdat de gegevens van alle bronnen worden opgeslagen als records, kunt u gegevens uit meerdere bronnen in één query analyseren.
  
Bovendien tooad hoc analyse, Log Analytics biedt meerdere manieren tooreport en analyseren van gegevens uit een query.

- **Weergaven en dashboards.**  [Weergaven](../log-analytics/log-analytics-view-designer.md) en [dashboards](../log-analytics/log-analytics-dashboards.md) visualiseren Hallo resultaten van een query in Hallo-portal.  Beheeroplossingen bevatten meestal weergaven die Hallo gegevens van Hallo-oplossing analyseren.  U kunt ook tooanalyze gegevens van uw eigen aangepaste weergaven maken en gemakkelijk beschikbaar zijn in uw aangepaste portal maken.
- **Exporteren.**  U hebt Hallo optie tooexport Hallo resultaten van een query zodat u deze buiten Log Analytics kunt analyseren.  U kunt zelfs een reguliere export te plannen[Power BI](../log-analytics/log-analytics-powerbi.md) waarmee u belangrijke mogelijkheden voor visualisatie en -analyse.
- **API voor zoeken in logboeken.**  Log Analytics heeft een [REST-API voor het verzamelen van gegevens vanuit elke client](../log-analytics/log-analytics-log-search-api.md).  Dit kunt u tooprogrammatically werken met gegevens die worden verzameld in Hallo opslagplaats of vanuit een ander controleprogramma.

#### <a name="alerting"></a>Waarschuwingen
Log Analytics kan u [proactief waarschuwen](../log-analytics/log-analytics-alerts.md) of corrigerende actie ondernemen wanneer er een probleem wordt gedetecteerd.  Net als andere analyses in Log Analytics wordt dit gedaan met zoeken in logboeken.  Deze zoekopdracht wordt uitgevoerd op een regelmatige en een waarschuwing wordt gemaakt als Hallo resultaten aan bepaalde criteria voldoen.

![Waarschuwingen in Log Analytics](media/operations-management-suite-overview/overview-alerts.png)

Bovendien toocreating een waarschuwing record in Hallo Log Analytics-opslagplaats, waarschuwingen kunnen duren Hallo van de volgende activiteiten.

- **E-mail.**  E-mailbericht verzenden tooproactively waarschuwt u over een probleem dat is gevonden.
- **Runbook.**  Een waarschuwing in Log Analytics kan een runbook starten in Azure Automation.  Dit gebeurt meestal tooattempt toocorrect Hallo gedetecteerd probleem.  Hallo runbook kan worden gestart in de cloud in Hallo Hallo geval van een probleem in Azure of een andere cloud, of het kan worden gestart op een lokale agent voor een probleem op een fysieke of virtuele machine.
- **Webhook.**  Een waarschuwing kunt starten van een webhook en gegevens uit de resultaten Hallo van Hallo logboek zoekopdracht doorgeven.  Hierdoor integratie met externe services, zoals een alternatieve waarschuwingsmethoden systeem of probeert tootake corrigerende maatregelen voor een externe website.

### <a name="azure-automation"></a>Azure Automation
[Azure Automation](http://azure.microsoft.com/documentation/services/automation) proces tooOMS voor automatisering en configuratie biedt.  Deze handmatige processen worden geautomatiseerd en helpt tooenforce configuraties voor fysieke en virtuele computers.  

#### <a name="process-automation"></a>Procesautomatisering
Azure Automation automatiseert handmatige processen met behulp van [runbooks](../automation/automation-runbook-types.md) die zijn gebaseerd op een PowerShell-script of PowerShell-werkstroom.  Dit omvat ook activa ondersteunende runbooks zoals variabelen die kunnen worden gedeeld tussen meerdere runbooks en referenties en verbindingen waarmee u toostore versleutelde gegevens die mogelijk vereist zijn voor een runbook voor verificatie.
Runbooks bieden procesautomatisering voor Hallo andere Hallo suite-services.  Aangezien elk Hallo andere services kunnen worden geopend met PowerShell of via een REST-API, kunt u runbooks tooperform functies zoals het verzamelen van gegevens in Log Analytics management of het initiëren van een back-up met Azure Backup.

##### <a name="accessing-resources"></a>Toegang tot resources
Omdat runbooks zijn gebaseerd op PowerShell, kunnen ze alle resources beheren die toegankelijk zijn met de PowerShell-cmdlets.  Wanneer u [laden van een module](../automation/automation-integration-modules.md) in uw Automation-account, wordt deze beschikbaar tooall runbooks in het account. 
 
Wanneer runbooks worden uitgevoerd in de cloud hello, toegang te krijgen tot alle resources die toegankelijk is vanuit de cloud Hallo.  Dit kunnen resources zijn in uw Azure-abonnement, in een andere cloud zoals Amazon Web Services (AWS), of een service die toegankelijk is via een REST-API.  Runbooks in de cloud Hallo onder alle referenties niet uitgevoerd, maar ze kunnen gebruikmaken van Automation activa zoals referenties, verbindingen en certificaten tooauthenticate tooresources die ze toegang krijgen tot.

Resources in uw datacentrum kunnen niet waarschijnlijk worden geopend vanuit een runbook uitgevoerd in de cloud Hallo.  U kunt een of meer installeren [Hybrid Runbook Workers](../automation/automation-hybrid-runbook-worker.md) in uw gegevens center echter toorun runbooks waarvoor toegang tot toolocal bronnen.  Wanneer u een runbook start, kunt u opgeven of deze moet worden uitgevoerd in Hallo cloud of op een specifieke werknemer.

![Azure Automation-runbooks](media/operations-management-suite-overview/overview-runbooks.png)

##### <a name="starting-a-runbook"></a>Een runbook starten
Runbooks kunnen worden [gestart via een aantal methoden](../automation/automation-starting-a-runbook.md) zodat ze kunnen worden opgenomen in verschillende beheerscenario's.  

- **Azure Portal.**  Net als andere Azure-services kunnen Azure Automation worden beheerd vanaf hello Azure-Portal.  Bovendien toostarting runbooks, u kunt ze importeren of maak uw eigen.
- **Gepland.**  U kunt runbooks toostart plannen met regelmatige tussenpozen.  Hiermee kunt u tooautomatically herhalen een reguliere beheerproces of gegevens verzamelen tooLog Analytics.
- **PowerShell en API.**  U kunt starten van runbooks en geeft deze vereiste parameterinformatie van een PowerShell-cmdlet of REST-API van Azure Automation Hallo.  
- **Webhook.**  Een webhook kan worden gemaakt voor elk runbook die toestaat dat deze toobe gestart vanaf externe toepassingen of websites.
- **Waarschuwing in Log Analytics.**  Een waarschuwing in Log Analytics kan een runbook tooattempt toocorrect Hallo probleem geïdentificeerd door Hallo waarschuwing automatisch starten.

#### <a name="configuration-management"></a>Configuration Management
[PowerShell Desired State Configuration (DSC)](../automation/automation-dsc-overview.md) is een beheerplatform in Windows PowerShell die kunt u toodeploy en af te dwingen Hallo configuratie van fysieke en virtuele machines.  Azure Automation DSC-configuraties beheert en biedt een pull-server in de cloud Hallo of agents toegang hebt tot tooretrieve vereiste configuraties.

![Azure Automation DSC](media/operations-management-suite-overview/overview-dsc.png)

### <a name="azure-backup-and-azure-site-recovery"></a>Azure Backup en Azure Site Recovery
Azure Backup en Azure Site Recovery bijdragen toobusiness bedrijfscontinuïteit en herstel na noodgevallen.  Deze hebben elk een functies waarmee u tooensure dat toepassingen beschikbaar blijven wanneer er storingen optreden en toonormal operations retourneren wanneer-systemen worden geleverd weer online is.  Beide services bijdragen toohello herstelpuntdoelen (RPO's) en hersteltijddoelen (RTO's) voor uw organisatie gedefinieerd. De RPO bepaalt Hallo acceptabele limiet waarin gegevens zijn niet beschikbaar tijdens een storing en Hallo RTO beperkt Hallo acceptabele hoeveelheid tijd in die een service of de app is niet beschikbaar tijdens een storing.

#### <a name="azure-backup"></a>Azure Backup
[Azure Backup](http://azure.microsoft.com/documentation/services/backup) biedt services voor het maken van back-ups en herstellen van gegevens voor OMS.  Het beschermt uw toepassingsgegevens en bewaart deze jarenlang, zonder dat u grote investeringen hoeft te doen en met een minimum aan operationele kosten.  Deze kan back-upgegevens van fysieke en virtuele Windows-servers in toevoeging tooapplication werkbelastingen zoals SQL Server en SharePoint.  Het kan ook worden gebruikt door System Center Data Protection Manager (DPM) tooreplicate beveiligde gegevens tooAzure voor redundantie en langetermijnopslag.

Beveiligde gegevens in Azure Backup worden opgeslagen in een back-upkluis in een bepaalde geografische regio. Hallo-gegevens worden gerepliceerd binnen dezelfde regio Hallo en, afhankelijk van Hallo type kluis, kan ook worden gerepliceerde tooanother regio voor verdere tolerantie.

Azure Backup heeft drie fundamentele scenario's.

- **Windows-computer met Azure Backup-agent.** Back-up van bestanden en mappen van elke WindowsServer of client rechtstreeks tooyour Azure Backup-kluis.<br><br>![Windows-computer met Azure Backup-agent](media/operations-management-suite-overview/overview-backup-01.png)
- **System Center Data Protection Manager (DPM) of Microsoft Azure Backup Server.** Gebruik de DPM- of Microsoft Azure Backup-Server toobackup bestanden en mappen in toevoeging tooapplication werkbelastingen zoals SQL en SharePoint toolocal opslag en vervolgens gerepliceerd tooyour Azure Backup-kluis. Ondersteunt Windows- en Linux-VM's op Hyper-V of VMware.<br><br>![System Center Data Protection Manager (DPM) of Microsoft Azure Backup Server](media/operations-management-suite-overview/overview-backup-02.png)
- **Extensies van virtuele Azure-machines.** Back-up van Windows of Linux virtuele machines in Azure tooyour Azure Backup-kluis.<br><br>![Extensies voor virtuele Azure-machines](media/operations-management-suite-overview/overview-backup-03.png)



#### <a name="azure-site-recovery"></a>Azure Site Recovery
[Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery) biedt bedrijfscontinuïteit door te organiseren replicatie van de lokale virtuele en fysieke machines tooAzure of tooa secundaire site. Als uw primaire site niet beschikbaar is, schakelt u over de secundaire locatie toohello zodat gebruikers kunnen werken blijven en mislukken wanneer systemen tooworking order retourneren. 

Azure Site Recovery biedt hoge beschikbaarheid voor servers en toepassingen.  Dit draagt bij tooyour zakelijke continuïteit en noodherstelplan (BCDR) door te organiseren replicatie, failovers en herstel van on-premises Hyper-V virtuele machines, virtuele VMware-machines en fysieke Windows of Linux-servers. U kunt replicatie van machines tooa secundaire Datacenter of uw datacenter uitbreiden door het repliceren van tooAzure. Site Recovery biedt ook eenvoudige functionaliteit voor failover en herstel voor werkbelastingen. Site Recovery is geïntegreerd met mechanismen voor herstel na noodgevallen, zoals SQL Server AlwaysOn, en biedt plannen voor herstel voor een eenvoudige failover van werkbelastingen die zich gelaagd op meerdere computers bevinden.

Azure Site Recovery heeft drie fundamentele replicatiescenario's.

- **Virtuele Hyper-V-machines repliceren.**  Als Hyper-V virtuele machines in VMM-clouds worden beheerd, kunt u tooa secundaire center of tooAzure gegevensopslag repliceren. Replicatie tooAzure is via een beveiligde internetverbinding. Replicatie tooa secundair datacenter is via Hallo LAN.  Als Hyper-V virtuele machines worden niet beheerd door VMM, kunt u alleen tooAzure opslag repliceren. Replicatie tooAzure is via een beveiligde internetverbinding.<br><br>![Virtuele Hyper-V-machines repliceren](media/operations-management-suite-overview/overview-siterecovery-hyperv.png)
- **Virtuele VMware-machines repliceren.**  U kunt repliceren VMware virtuele machines tooa secundair datacenter waarop VMware of tooAzure opslag wordt uitgevoerd. Replicatie tooAzure kan plaatsvinden via een site-naar-site VPN of Azure ExpressRoute of via een beveiligde internetverbinding. Replicatie tooa secundair datacenter vindt plaats via Hallo InMage Scout gegevenskanaal.<br><br>![Virtuele VMware-machines repliceren](media/operations-management-suite-overview/overview-siterecovery-vmware.png)
- **Fysieke Windows- en Linux-servers repliceren**  U kunt fysieke servers tooa secundaire datacenter of tooAzure opslag repliceren. Replicatie tooAzure kan plaatsvinden via een site-naar-site VPN of Azure ExpressRoute of via een beveiligde internetverbinding. Replicatie tooa secundair datacenter vindt plaats via Hallo InMage Scout gegevenskanaal. Azure Site Recovery heeft een OMS-oplossing die een aantal statistieken worden weergegeven, maar moet u hello Azure-portal gebruiken voor alle bewerkingen.<br><br>![Fysieke Windows- en Linux-servers repliceren](media/operations-management-suite-overview/overview-siterecovery-physical.png)


Met Site Recovery worden metagegevens opgeslagen in kluizen in een bepaalde geografische Azure-regio. Er is geen gerepliceerde gegevens worden opgeslagen door Hallo Site Recovery-service.

## <a name="management-solutions"></a>Beheeroplossingen
[Beheeroplossingen](operations-management-suite-solutions.md) zijn voorverpakte sets met logica die een bepaald beheerscenario implementeren door van een of meer OMS-services gebruik te maken.  Er zijn verschillende oplossingen beschikbaar van Microsoft en partners kunt u eenvoudig toevoegen tooyour Azure-abonnement tooincrease Hallo waarde van uw investering in OMS.  Als partner kunt u uw eigen oplossingen toosupport uw toepassingen en services maken en ze toousers via Hallo Quick Start-sjablonen of Azure Marketplace.

Een goed voorbeeld van een oplossing die gebruikmaakt van meerdere services tooprovide aanvullende functionaliteit is Hallo [Update beheeroplossing](oms-solution-update-management.md).  Deze oplossing gebruikt Hallo Log Analytics-agent voor Windows en Linux toocollect informatie over vereiste updates op elke agent.  Deze gegevens toohello logboekanalyse opslagplaats, waar u het met een opgenomen dashboard analyseren kunt geschreven.  Wanneer u een implementatie maakt, zijn runbooks in Azure Automation gebruikte tooinstall vereiste updates.  U hoeft tooworry Hallo onderliggende details over of deze het volledige proces in Hallo portal beheren.

![Oplossing](media/operations-management-suite-overview/overview-solution.png)

De meeste oplossingen kunnen een of meer Hallo na functies uitvoeren.

- Verzamelen van aanvullende gegevens.  Log Analytics verzamelt een verscheidenheid aan gegevens van clients en services inclusief gebeurtenissen en prestatiegegevens.  Een beheeroplossing kan aanvullende informatie verzamelen die niet beschikbaar is vanuit andere gegevensbronnen, vaak met behulp van Azure Automation-runbooks.
- Bieden van aanvullende analyse van verzamelde gegevens.  Beheeroplossingen omvatten dashboards en weergaven die analyse en visualisatie van gegevens bieden.  Deze koppeling back toopredefined logboek zoekopdrachten waarmee u toodrill in Hallo gedetailleerde gegevens.  Ze kunnen ook analyse uitvoeren op gegevens die al is verzameld in Hallo-opslagplaats, bijvoorbeeld over beveiligingsgebeurtenissen voor patronen die wijzen op een bedreiging zoeken.
- Toevoegen van functionaliteit.  Sommige Microsoft-oplossingen kunnen bouwen voort op Hallo-mogelijkheden van Hallo core services tooprovide aanvullende functionaliteit.  Serviceoverzicht biedt een eigen console toodiscover bijvoorbeeld en -server en Procesafhankelijkheden in realtime worden toegewezen.
Oplossingen worden regelmatig toegevoegd tooOMS door Microsoft en partners zodat u toocontinuously verhogen Hallo-waarde van uw investering.  U kunt bladeren en Microsoft-oplossingen via Hallo oplossingen catalogus in Hallo OMS-portal installeren of bladeren en oplossingen voor zowel Microsoft en haar partners via hello Azure Marketplace in hello Azure-Portal installeren.  

![Galerie van oplossingen](media/operations-management-suite-overview/solution-gallery.png)


## <a name="next-steps"></a>Volgende stappen
* Meer informatie over [Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics).
* Meer informatie over [Azure Automation](../automation/automation-intro.md).
* Meer informatie over [Azure Backup](http://azure.microsoft.com/documentation/services/backup).
* Meer informatie over [Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery).
* Hallo detecteren [oplossingen die beschikbaar zijn](../log-analytics/log-analytics-add-solutions.md) in Hallo verschillende OMS aanbiedingen. 

