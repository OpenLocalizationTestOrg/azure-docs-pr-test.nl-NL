---
title: een toepassing met meerdere lagen SharePoint met Azure Site Recovery aaaReplicate | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooreplicate een toepassing met meerdere lagen SharePoint met behulp van Azure Site Recovery-mogelijkheden.
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: sutalasi
ms.openlocfilehash: d856034ac2a3c95b0c1f0cf85e62c4e7a5a3210f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-sharepoint-application-for-disaster-recovery-using-azure-site-recovery"></a>Een toepassing met meerdere lagen SharePoint voor herstel na noodgevallen met Azure Site Recovery repliceren

Dit artikel wordt beschreven in detail hoe een SharePoint-toepassing met tooprotect [Azure Site Recovery](site-recovery-overview.md).


## <a name="overview"></a>Overzicht

Microsoft SharePoint is een krachtige toepassing waarmee u een groep kunt of afdeling organiseren, samenwerken en informatie delen. SharePoint kan bieden intranet-portals, document en bestandsbeheer, samenwerking, sociale netwerken, extranetten, websites, zoeken enterprise en business intelligence. Heeft ook integratie, integratie en werkstroom automatiseringsmogelijkheden worden uitgebreid. Normaal gesproken beschouwen organisaties als een laag 1 toepassing gevoelige toodowntime en verlies van gegevens.

Microsoft SharePoint biedt vandaag de dag geen eventuele herstelfuncties out-of-the-box-noodherstel. Ongeacht het Hallo-type en de schaal van een noodgeval wordt herstel Hallo gebruikgemaakt van een stand-by-datacenter dat u Hallo-farm kunt herstellen. Stand-by-datacenters zijn vereist voor scenario's waarbij lokaal redundante systemen en back-ups Hallo onderbreking in de primaire Datacenter Hallo kunnen herstellen.

Een goede noodhersteloplossing moet modellering van herstelplannen toestaan om complexe toepassingsarchitecturen Hallo zoals SharePoint. Deze moet ook Hallo mogelijkheid tooadd aangepast stappen toohandle Toepassingstoewijzingen tussen verschillende lagen en daarom een failover met één klik voorzien van een lagere RTO in geval van een noodgeval Hallo hebben.

Dit artikel wordt beschreven in detail hoe een SharePoint-toepassing met tooprotect [Azure Site Recovery](site-recovery-overview.md). Dit artikel wordt uitgelegd aanbevolen procedures voor het repliceren van een drielaagse SharePoint toepassing tooAzure, hoe u een herstel na noodgevallen detailanalyse kunt doen en hoe kunt u failover Hallo toepassing tooAzure.

U kunt Hallo onderstaande video over het herstellen van een multi-laag toepassing tooAzure bekijken.

> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/Disaster-Recovery-of-load-balanced-multi-tier-applications-using-Azure-Site-Recovery/player]


## <a name="prerequisites"></a>Vereisten

Voordat u begint, zorg er dan voor dat u begrijpt Hallo volgende:

1. [Een virtuele machine tooAzure repliceren](site-recovery-vmware-to-azure.md)
2. Hoe te[ontwerpen van een netwerk herstel](site-recovery-network-design.md)
3. [Tijdens het doorzoeken van een failover-test tooAzure](site-recovery-test-failover-to-azure.md)
4. [Tijdens het doorzoeken van een failover-tooAzure](site-recovery-failover.md)
5. Hoe te[repliceren van een domeincontroller](site-recovery-active-directory.md)
6. Hoe te[SQL-Server repliceren](site-recovery-sql.md)

## <a name="sharepoint-architecture"></a>SharePoint-architectuur

SharePoint kan worden geïmplementeerd op een of meer servers met gelaagde topologieën en server rollen tooimplement een farm ontwerp dat voldoet aan specifieke doelen en doelstellingen. Een typische grote, hoogwaardige aanvraag SharePoint-serverfarm die ondersteuning biedt voor een groot aantal gelijktijdige gebruikers en een groot aantal inhoudsitems gebruik service groeperen als onderdeel van hun strategie schaalbaarheid. Deze methode omvat de services uitgevoerd op speciale servers, deze services te groeperen en vervolgens Hallo servers uitbreiden als een groep. Hallo illustreert volgende topologie Hallo-service en server groepering voor een drielaagse SharePoint-serverfarm. Raadpleeg de documentatie tooSharePoint en product line architecturen voor gedetailleerde richtlijnen voor verschillende SharePoint-topologieën. U vindt meer informatie over de implementatie van SharePoint 2013 in [dit document](https://technet.microsoft.com/en-us/library/cc303422.aspx).



![Implementatie-patroon 1](./media/site-recovery-sharepoint/sharepointarch.png)


## <a name="site-recovery-support"></a>Site Recovery-ondersteuning

Virtuele VMware-machines met Windows Server 2012 R2 Enterprise zijn voor het maken van dit artikel gebruikt. SharePoint 2013 Enterprise edition en Enterprise-editie van SQL server 2014 werden gebruikt. Als de replicatie van Site Recovery is toepassing networkdirect, Hallo aanbevelingen voor zover hier verwachte toohold op voor de volgende scenario's ook.

### <a name="source-and-target"></a>Bron en doel

**Scenario** | **de secundaire site tooa** | **tooAzure**
--- | --- | ---
**Hyper-V** | Ja | Ja
**VMware** | Ja | Ja
**Fysieke server** | Ja | Ja

### <a name="sharepoint-versions"></a>SharePoint-versies
Hallo volgende SharePoint server-versies worden ondersteund.

* SharePoint server 2013 standaard
* SharePoint server 2013 Enterprise
* SharePoint server 2016 standaard
* SharePoint server 2016 Enterprise

### <a name="things-tookeep-in-mind"></a>Dingen tookeep rekening

Als u een gedeelde cluster op basis van schijven als een laag in uw toepassing is u niet gaat worden kunnen toouse Site Recovery replicatie tooreplicate die virtuele machines. U kunt systeemeigen replicatie geleverd door de toepassing hello gebruiken en gebruik vervolgens een [herstelplan](site-recovery-create-recovery-plans.md) toofailover alle lagen.

## <a name="replicating-virtual-machines"></a>Repliceren van virtuele machines

Ga als volgt [in deze richtlijnen](site-recovery-vmware-to-azure.md) toostart Hallo virtuele machine tooAzure repliceren.

* Zodra het Hallo-replicatie is voltooid, zorg dat u gaat tooeach virtuele machine van elke laag en selecteert u dezelfde beschikbaarheidsset voor ' gerepliceerde item > Instellingen > Eigenschappen > berekening en netwerk '. Bijvoorbeeld, als uw weblaag 3 VM's heeft, zorg er alle Hallo 3 VM's zijn geconfigureerd toobe deel uitmaken van dezelfde beschikbaarheidsset in Azure.

    ![Set Beschikbaarheidsset](./media/site-recovery-sharepoint/select-av-set.png)

* Voor instructies over het beveiligen van Active Directory en DNS te verwijzen[beveiligen van Active Directory en DNS](site-recovery-active-directory.md) document.

* Voor instructies over het beveiligen van databaselaag uitgevoerd op de SQL server te verwijzen[SQL Server beveiligen](site-recovery-active-directory.md) document.

## <a name="networking-configuration"></a>Netwerkconfiguratie

### <a name="network-properties"></a>Eigenschappen van het netwerk

* Voor Hallo App en weblaag VMs netwerkinstellingen configureren in Azure-portal zodat Hallo VMs beschikken over gekoppelde toohello rechts DR netwerk na een failover.

    ![Netwerk selecteren](./media/site-recovery-sharepoint/select-network.png)


* Als u een statisch IP-adres gebruikt, geeft u Hallo IP die u wilt dat virtuele machine tootake in Hallo Hallo **IP-adres doel** veld

    ![Vaste IP-adres instellen](./media/site-recovery-sharepoint/set-static-ip.png)

### <a name="dns-and-traffic-routing"></a>DNS- en verkeersroutering

Voor sites, internetgericht [maken van een Traffic Manager-profiel van het type 'Prioriteit'](../traffic-manager/traffic-manager-create-profile.md) in hello Azure-abonnement. En configureer vervolgens uw DNS- en Traffic Manager-profiel in Hallo manier te volgen.


| **Waar** | **Bron** | **Doel**|
| --- | --- | --- |
| Openbare DNS-server | Openbare DNS-server voor SharePoint-sites <br/><br/> Voorbeeld: sharepoint.contoso.com | Traffic Manager <br/><br/> contososharepoint.trafficmanager.NET |
| On-premises DNS | sharepointonprem.contoso.com | Openbare IP-adres op Hallo lokale farm |


In Hallo Traffic Manager-profiel [Hallo primaire en herstelsites eindpunten maken](../traffic-manager/traffic-manager-configure-priority-routing-method.md). Het externe eindpunt hello gebruiken voor lokaal eindpunt en openbare IP-adres voor de Azure-eindpunt. Zorg ervoor dat Hallo prioriteit hoger tooon lokaal eindpunt is ingesteld.

Host een testpagina op een specifieke poort (bijvoorbeeld 800) in Hallo SharePoint web-laag voor Traffic Manager tooautomatically detecteren beschikbaarheid na failover. Dit is een tijdelijke oplossing als u anonieme verificatie niet voor een van uw SharePoint-sites inschakelen.

[Hallo Traffic Manager-profiel configureren](../traffic-manager/traffic-manager-configure-priority-routing-method.md) Hello onder instellingen.

* Routeringsmethode - 'Prioriteit'
* DNS time toolive (TTL) - 30 seconden
* Instellingen voor eindpunt monitor - als u anonieme verificatie kunt inschakelen, kunt u een specifieke website-eindpunt kunt geven. Of u kunt een testpagina gebruiken op een specifieke poort (bijvoorbeeld 800).

## <a name="creating-a-recovery-plan"></a>Een herstelplan maken

Een herstelplan kunt Hallo failover van de verschillende lagen in een toepassing met meerdere lagen, daarom toepassing consistentie van de sequentiëren. Ga als volgt Hallo onderstaande stappen te volgen bij het maken van een herstelplan voor een webtoepassing met meerdere lagen. [Meer informatie over het maken van een herstelplan](site-recovery-runbook-automation.md#customize-the-recovery-plan).

### <a name="adding-virtual-machines-toofailover-groups"></a>Toevoegen van virtuele machines toofailover groepen

1. Een herstelplan door toe te voegen Hallo App en weblaag virtuele machines maken.
2. Klik op 'Aanpassen' toogroup Hallo virtuele machines. Standaard uitmaken alle virtuele machines deel van 'Groep 1'.

    ![RP aanpassen](./media/site-recovery-sharepoint/rp-groups.png)

3. Maak een andere groep (groep 2) en Hallo weblaag VM's verplaatsen naar de nieuwe groep Hallo. Uw virtuele machines van de App-laag moeten deel uitmaken van 'Groep 1' en weblaag virtuele machines moeten deel uitmaken van 'Groep 2'. Dit is tooensure die Hallo App laag virtuele machines opstarten eerst gevolgd door Web laag virtuele machines.


### <a name="adding-scripts-toohello-recovery-plan"></a>Het herstelplan toohello toe te voegen scripts

U kunt meest gebruikte hello Azure Site Recovery scripts implementeren in uw Automation-account te klikken op Hallo 'TooAzure implementeren' hieronder. Wanneer u een script voor gepubliceerde gebruikt, zorg ervoor dat u Hallo richtlijnen in Hallo script volgen.

[![TooAzure implementeren](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)

1. Toevoegen van een vooraf actiescript too'Group 1 toofailover SQL-beschikbaarheidsgroep. Hallo 'ASR SQL FailoverAG' script gepubliceerd in de voorbeeldscripts hello gebruiken. Zorg ervoor dat u Volg de instructies Hallo in Hallo script en Hallo vereist wijzigingen in Hallo-script op de juiste wijze.

    ![Toevoegen-AG-Script-stap-1](./media/site-recovery-sharepoint/add-ag-script-step1.png)

    ![Toevoegen-AG-Script-stap-2](./media/site-recovery-sharepoint/add-ag-script-step2.png)

2. Voeg een post actie script tooattach een load balancer op Hallo failover van virtuele machines van de weblaag (groep 2). Hallo 'ASR AddSingleLoadBalancer' script gepubliceerd in de voorbeeldscripts hello gebruiken. Zorg ervoor dat u Volg de instructies Hallo in Hallo script en Hallo vereist wijzigingen in Hallo-script op de juiste wijze.

    ![Toevoegen-LB-Script-stap-1](./media/site-recovery-sharepoint/add-lb-script-step1.png)

    ![Toevoegen-LB-Script-stap-2](./media/site-recovery-sharepoint/add-lb-script-step2.png)

3. Voeg een handmatige stap tooupdate Hallo DNS-records toopoint toohello nieuwe farm in Azure.

    * Er is geen DNS-updates zijn voor internetgericht sites vereist na failover. Hallo stappen wordt beschreven in Hallo 'Netwerken richtlijnen' sectie tooconfigure Traffic Manager. Als Hallo Traffic Manager-profiel is ingesteld zoals beschreven in de vorige sectie Hallo, voegt u een script tooopen dummy-poort (800 in Hallo voorbeeld) toe op Hallo Azure VM.

    * Voor interne gerichte sites, voegt u een handmatige stap tooupdate Hallo DNS-record toopoint toohello nieuwe Web-laag van de virtuele machine load balancer IP.

4. Een handmatige stap toorestore-zoektoepassing toevoegen van een back-up of een nieuwe search-service starten.

5. Voor de Search-servicetoepassing is teruggezet vanaf een back-up, volgt u onderstaande stappen te volgen.

    * Deze methode wordt ervan uitgegaan dat een back-up van de servicetoepassing Hallo voordat Hallo onherstelbare gebeurtenis is uitgevoerd en die Hallo back-up beschikbaar op Hallo DR-site is.
    * Dit kan eenvoudig worden bereikt door Hallo back-up plannen (bijvoorbeeld, eenmaal per dag) en het gebruik van een back-upkopie procedure tooplace Hallo op Hallo DR-site. Procedures kopie kunnen programma's systeemscript zoals AzCopy (Azure Copy)- of DFSR (Distributed File Services Replication) instellen.
    * Nu dat Hallo SharePoint-farm wordt uitgevoerd, gaat van Centraalbeheersite Hallo 'Back-up en herstellen' en selecteert u terugzetten. Hallo terugzetten interrogates Hallo back-uplocatie opgegeven (mogelijk moet u tooupdate Hallo waarde). Hallo servicetoepassing back-up u toorestore wilt selecteren.
    * Zoeken wordt teruggezet. Houd er rekening mee dat herstellen Hallo verwacht toofind Hallo dezelfde topologie (hetzelfde aantal servers) en dezelfde harde schijf letters toothose servers wordt toegewezen. Zie voor meer informatie ['Herstellen Search-service-toepassing in SharePoint 2013'](https://technet.microsoft.com/library/ee748654.aspx) document.


6. Voor het beginnen met een nieuwe toepassing van de Search-service, volgt u onderstaande stappen te volgen.

    * Deze methode wordt ervan uitgegaan dat er een back-up van Hallo "zoeken" Beheerdatabase beschikbaar op Hallo DR-site is.
    * Aangezien hello andere databases Search-servicetoepassing niet worden gerepliceerd, moeten ze toobe opnieuw gemaakt. toodo dus tooCentral beheer navigeren en Hallo Search-servicetoepassing te verwijderen. Op welke host Hallo Search-Index verwijderen Hallo indexbestanden servers.
    * Maak opnieuw Hallo Search-servicetoepassing en deze databases hello wordt opnieuw gemaakt. Het verdient aanbeveling toohave een voorbereide script dat wordt opnieuw gemaakt deze servicetoepassing omdat het niet mogelijk tooperform alle acties via Hallo GUI. Bijvoorbeeld, zijn Hallo index stationslocatie en configureren van Hallo zoektopologie alleen mogelijk met SharePoint PowerShell-cmdlets. Gebruik Hallo Windows PowerShell-cmdlet terugzetten SPEnterpriseSearchServiceApplication en geef Hallo logboek verzonden en zoeken Beheerdatabase, Search_Service__DB gerepliceerd. Deze cmdlet geeft zoekconfiguratie hello, schema, beheerde eigenschappen, regels en bronnen en andere onderdelen van een reeks Hallo gemaakt.
    * Zodra het Hallo die Search-servicetoepassing is niet opnieuw worden gemaakt, moet u een volledige verkenning voor elke inhoudsbron toorestore Hallo Search-Service starten. Er verloren gegevens gaan analytics uit Hallo lokale farm, zoals zoeken aanbevelingen.

7. Nadat alle Hallo stappen zijn voltooid, sla het herstelplan Hallo en de uiteindelijke herstelplan hello, ziet er als de volgende.

    ![Opgeslagen RP](./media/site-recovery-sharepoint/saved-rp.png)

## <a name="doing-a-test-failover"></a>Een testfailover uitvoeren
Ga als volgt [in deze richtlijnen](site-recovery-test-failover-to-azure.md) toodo een testfailover.

1.  Ga tooAzure portal en selecteer de Recovery Services-kluis.
2.  Klik op Hallo herstelplan is gemaakt voor de SharePoint-toepassing.
3.  Klik op 'Testfailover'.
4.  Selecteer herstelpunt en het virtuele netwerk van Azure toostart Hallo test failover-proces.
5.  Wanneer secundaire Hallo-omgeving is, kunt u uw validaties kunt uitvoeren.
6.  Zodra Hallo validaties voltooid zijn, klikt u op 'Opschonen testfailover' op Hallo herstelplan en Hallo testfailoveromgeving is opgeschoond.

Voor hulp bij de testfailover uitvoeren voor AD en DNS, te verwijzen[Testfailover-overwegingen voor AD- en DNS-](site-recovery-active-directory.md#test-failover-considerations) document.

Voor hulp bij de testfailover doet voor SQL altijd op beschikbaarheidsgroepen, Raadpleeg te[doen testfailover voor SQL Server Always On](site-recovery-sql.md#steps-to-do-a-test-failover) document.

## <a name="doing-a-failover"></a>U een failover uitvoert
Ga als volgt [in deze richtlijnen](site-recovery-failover.md) om een failover uit te voeren.

1.  Ga tooAzure portal en selecteer de Recovery Services-kluis.
2.  Klik op Hallo herstelplan is gemaakt voor de SharePoint-toepassing.
3.  Klik op 'Failover'.
4.  Selecteer herstelproces punt toostart Hallo failover.

## <a name="next-steps"></a>Volgende stappen
U kunt meer lezen over [andere toepassingen repliceren](site-recovery-workload.md) met Site Recovery.
