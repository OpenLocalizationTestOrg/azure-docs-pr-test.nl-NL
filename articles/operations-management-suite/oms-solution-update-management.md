---
title: aaaUpdate beheeroplossing in OMS | Microsoft Docs
description: Dit artikel is bedoeld toohelp u begrijpt hoe toouse deze oplossing toomanage updates voor uw Windows- en Linux-computers.
services: operations-management-suite
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: e33ce6f9-d9b0-4a03-b94e-8ddedcc595d2
ms.service: operations-management-suite
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/27/2017
ms.author: magoedte
ms.openlocfilehash: 2dd321913bf049ab1996fd60a2f74b8417084dcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="update-management-solution-in-oms"></a>De oplossing voor updatebeheer in OMS

![Symbool voor updatebeheer](./media/oms-solution-update-management/update-management-symbol.png)

Hallo Update beheeroplossing in OMS kunt u beveiligingsupdates toomanage-besturingssysteem voor uw Windows- en Linux-computers die zijn geïmplementeerd in Azure, lokale omgevingen of andere cloudproviders.  U kunt snel Hallo status van de beschikbare updates op alle agentcomputers te beoordelen en Hallo-proces voor het installeren van vereiste updates voor servers beheren.


## <a name="solution-overview"></a>Oplossingenoverzicht
Computers die worden beheerd door OMS gebruikt Hallo volgende voor het uitvoeren van implementaties beoordelen en bij te werken:

* OMS-agent voor Windows of Linux
* PowerShell Desired State Configuration (DSC) voor Linux
* Automation Hybrid Runbook Worker
* Microsoft Update of Windows Server Update Services voor Windows-computers

Hallo volgende diagrammen ziet u een conceptueel overzicht van Hallo gedrag en gegevensstroom van hoe Hallo-oplossing evalueert en beveiliging updates tooall geldt verbonden Windows Server- en Linux-computers in een werkruimte.    

#### <a name="windows-server"></a>Windows Server
![Processtroom voor het beheren van Windows Server-updates](media/oms-solution-update-management/update-mgmt-windows-updateworkflow.png)

#### <a name="linux"></a>Linux
![Processtroom voor het beheren van Linux-updates](media/oms-solution-update-management/update-mgmt-linux-updateworkflow.png)

Nadat de computer Hallo voert een scan voor compatibiliteit van updates, stuurt Hallo OMS-agent Hallo-gegevens in bulk tooOMS. Op een computer venster Hallo compatibiliteitsscan standaard elke 12 uur uitgevoerd.  Schema voor scan van toohello, Hallo scannen voor Updatevereisten wordt bovendien binnen 15 minuten als Hallo Microsoft Monitoring Agent (MMA) installatie is opnieuw gestart, voorafgaande tooupdate en na installatie van update gestart.  Compatibiliteitsscan hello wordt elke drie uur standaard uitgevoerd met een Linux-computer en een scan voor naleving binnen 15 minuten wordt gestart als Hallo MMA agent opnieuw wordt opgestart.  

Hallo compatibiliteitsinformatie wordt vervolgens verwerkt en samengevat in Hallo dashboards die zijn opgenomen in Hallo oplossing of doorzoekbare met behulp van gebruiker gedefinieerde of pre-door de gedefinieerde query's.  Hallo oplossing rapporten hoe up-to-date hello computer is gebaseerd op welke gegevensbron u geconfigureerde toosynchronize met zijn.  Als Windows-computer Hallo geconfigureerde tooreport tooWSUS, afhankelijk van wanneer WSUS het laatst is gesynchroniseerd met Microsoft Update worden Hallo resultaten kunnen afwijken van wat Microsoft-Updates wordt weergegeven.  Hallo dezelfde voor Linux-computers die zijn geconfigureerd tooreport tooa lokale opslagplaats ten opzichte van een openbare opslagplaats.   

U kunt implementeren en software-updates installeren op computers die door het maken van een geplande implementatie Hallo-updates zijn vereist.  Updates die zijn geclassificeerd als *optioneel* niet zijn opgenomen in de reikwijdte van de implementatie voor Windows-computers Hallo alleen updates vereist.  Hallo geplande implementatie wordt gedefinieerd welke doelcomputers ontvangt Hallo toepasselijke updates, door het expliciet opgeven van computers of selecteren van een [computergroep](../log-analytics/log-analytics-computer-groups.md) die is gebaseerd op het logboek van zoekopdrachten van een specifieke verzameling computers.  U ook een planning tooapprove opgeven en toewijzen van een bepaalde periode wanneer updates geïnstalleerd binnen toobe zijn toegestaan.  Updates worden geïnstalleerd door runbooks in Azure Automation.  U kunt deze runbooks niet weergeven en ze vereisen geen configuratie.  Wanneer een Update-implementatie wordt gemaakt, maakt u een planning die wordt gestart een runbook master bijwerken op Hallo tijd voor computers Hallo opgenomen opgegeven.  Dit master-runbook start een onderliggend runbook op elke agent die installatie van de vereiste updates uitvoert.       

Op Hallo datum en tijd die is opgegeven in de update-implementatie hello, voert doelcomputers Hallo Hallo implementatie parallel.  Een scan wordt eerste uitgevoerd tooverify Hallo updates nog steeds vereist zijn en worden ze geïnstalleerd.  Het is belangrijk toonote voor WSUS-clientcomputers, als Hallo updates niet worden goedgekeurd in WSUS, Hallo-update-implementatie mislukt.  Hallo-resultaten van Hallo toegepast updates worden doorgestuurd tooOMS toobe verwerkt en worden samengevat in Hallo dashboards of door Hallo Hallo gebeurtenissen zoeken.     

## <a name="prerequisites"></a>Vereisten
* Hallo oplossing presterende update beoordelingen op basis van Windows Server 2008 en hoger ondersteunt en update-implementaties op basis van Windows Server 2008 R2 SP1 en hoger.  Server Core- en nanoserverinstallatieopties worden niet ondersteund.

    > [!NOTE]
    > Ondersteuning voor het implementeren van updates tooWindows Server 2008 R2 SP1 is vereist voor .NET Framework 4.5 en WMF 5.0 of hoger.
    >  
* Windows-clientbesturingssystemen worden niet ondersteund.  
* Windows-agents moeten geconfigureerde toocommunicate met een Windows Server Update Services (WSUS)-server of hebt toegang tooMicrosoft Update.  

    > [!NOTE]
    > Hallo Windows-agent kan niet door System Center Configuration Manager gelijktijdig worden beheerd.  
    >
* CentOS 6 (x86/x64) en 7 (x64)  
* Red Hat Enterprise 6 (x86/x64) en 7 (x64)  
* SUSE Linux Enterprise Server 11 (x86/x64) en 12 (x64)  
* Ubuntu 12.04 LTS en nieuwer x86/x64   
    > [!NOTE]  
    > tooavoid updates worden toegepast buiten een onderhoudsvenster op Ubuntu, opnieuw Unattended-Upgrade pakket toodisable automatische updates configureren. Voor meer informatie over tooconfigure deze, Zie [Automatische Updates-onderwerp in Hallo Ubuntu Server Guide](https://help.ubuntu.com/lts/serverguide/automatic-updates.html).

* Linux-agents moeten toegang tooan-update opslagplaats hebben.  

    > [!NOTE]
    > Een OMS-Agent wordt voor Linux geconfigureerd tooreport toomultiple OMS werkruimten niet ondersteund met deze oplossing.  
    >

Voor meer informatie over hoe tooinstall hello OMS-Agent voor Linux en download de nieuwste versie Hallo verwijzen te[Operations Management Suite-Agent voor Linux](https://github.com/microsoft/oms-agent-for-linux).  Lees voor informatie over hoe tooinstall OMS-Agent voor Windows hello, [Operations Management Suite-Agent voor Windows](../log-analytics/log-analytics-windows-agents.md).  

### <a name="permissions"></a>Machtigingen
In de volgorde toocreate update-implementaties, moet u toobe rol van Inzender Hallo in uw Automation-account en de werkruimte voor logboekanalyse verleend.  

## <a name="solution-components"></a>Oplossingsonderdelen
Deze oplossing bestaat uit Hallo resources die zijn toegevoegd tooyour Automation-account en rechtstreeks verbonden zijn met agents of verbonden beheergroep van Operations Manager te volgen.

### <a name="management-packs"></a>Management packs
Als uw System Center Operations Manager-beheergroep verbonden tooan OMS-werkruimte is, worden volgende management packs Hallo in Operations Manager geïnstalleerd.  Deze management packs worden na het toevoegen van deze oplossing ook op rechtstreeks verbonden Windows-computers geïnstalleerd. Er is niets tooconfigure of beheren met deze management packs.

* Microsoft System Center Advisor Update Assessment Intelligence Pack (Microsoft.IntelligencePacks.UpdateAssessment)
* Microsoft.IntelligencePack.UpdateAssessment.Configuration (Microsoft.IntelligencePack.UpdateAssessment.Configuration)
* Implementatie MP bijwerken

Zie voor meer informatie over hoe de oplossing management packs worden bijgewerkt, [verbinding maken met Operations Manager tooLog Analytics](../log-analytics/log-analytics-om-agents.md).

### <a name="hybrid-worker-groups"></a>Hybrid Worker-groepen
Nadat u deze oplossing hebt ingeschakeld, geeft elke Windows-computer rechtstreeks verbonden tooyour OMS-werkruimte wordt automatisch geconfigureerd als een hybride Runbook Worker toosupport hello runbooks zijn opgenomen in deze oplossing.  Voor elke Windows-computer worden beheerd door Hallo-oplossing, wordt het weergegeven onder Hallo Hybrid Runbook Worker-groepen blade van Automation-account Hallo Hallo naamconventie volgen *Hostname FQDN_GUID*.  U kunt deze groepen niet targeten met runbooks uit uw account. De bewerking mislukt dan. Deze groepen zijn alleen bedoeld toosupport Hallo beheeroplossing.   

U kunt wel toevoegen Hallo Windows-computers tooa Hybrid Runbook Worker-groep in uw Automation-account toosupport Automation-runbooks, zolang u dezelfde voor zowel Hallo oplossing als hybride Runbook Worker-groepslidmaatschap account Hallo gebruikt.  Deze functionaliteit is tooversion 7.2.12024.0 Hallo Hybrid Runbook Worker toegevoegd.  

## <a name="configuration"></a>Configuratie
Hallo stappen tooadd hello tooyour OMS-werkruimte updatebeheer oplossing te volgen uitvoeren en Bevestig het melden van agents. Windows-agents al verbonden tooyour werkruimte worden automatisch toegevoegd zonder aanvullende configuratie.

U kunt met behulp van de volgende methoden Hallo Hallo-oplossing implementeren:

* Uit Azure Marketplace in hello Azure-portal door Hallo Automation en Control aanbieding of oplossing voor het beheer van de Update te selecteren
* Van Hallo galerie met OMS oplossingen in de OMS-werkruimte

Als er al een Automation-account en de OMS-werkruimte gekoppeld samen in Hallo dezelfde resourcegroep en regio, Automation & besturingselement selecteren zal Controleer de configuratie en alleen Hallo oplossing installeren en configureren in beide services.  Hallo updatebeheer oplossing selecteren uit Azure Marketplace Hallo levert hetzelfde gedrag.  Als u niet de services die zijn geïmplementeerd in uw abonnement hebt, stappen Hallo in Hallo **nieuwe oplossing maken** blade en bevestigt u wilt dat andere tooinstall Hallo aanbevolen oplossingen vooraf zijn geselecteerd.  U kunt desgewenst Hallo updatebeheer oplossing tooyour OMS-werkruimte met behulp van Hallo stappen wordt beschreven in toevoegen [toevoegen OMS oplossingen](../log-analytics/log-analytics-add-solutions.md) van Hallo galerie met oplossingen.  

### <a name="confirm-oms-agents-and-operations-manager-management-group-connected-toooms"></a>OMS-agents en Operations Manager management groep verbonden tooOMS bevestigen

tooconfirm rechtstreeks verbonden zijn OMS-Agent voor Linux en Windows OMS, communiceert na een paar minuten kunt u uitvoeren Hallo logboek zoeken te volgen:

* Linux - `Type=Heartbeat OSType=Linux | top 500000 | dedup SourceComputerId | Sort Computer | display Table`.  

* Windows - `Type=Heartbeat OSType=Windows | top 500000 | dedup SourceComputerId | Sort Computer | display Table`

U kunt op een computer met Windows hello na tooverify agent-connectiviteit met OMS bekijken:

1.  Open Microsoft Monitoring Agent in het Configuratiescherm en op Hallo **Azure logboekanalyse (OMS)** tabblad, hello agent wordt een bericht weergegeven: **Hallo Microsoft Monitoring Agent verbonden is toohello Microsoft Operations Management Suite-service**.   
2.  Open Windows-gebeurtenislogboek hello, te navigeren**toepassingen en Services Logs\Operations Manager** en zoek naar gebeurtenis-ID 3000 en 5002 van bron-Service-Connector.  Deze gebeurtenissen geven Hallo-computer is geregistreerd bij de OMS-werkruimte Hallo en configuratie ontvangt.  

Als het Hallo-agent niet kunnen toocommunicate Hello OMS-service en het geconfigureerde toocommunicate Hello internet via een firewall of proxyserver, bevestig Hallo firewall of proxyserver correct is geconfigureerd aan de hand van [netwerk configuratie voor Windows-agent](../log-analytics/log-analytics-windows-agents.md#network) of [netwerkconfiguratie voor Linux-agent](../log-analytics/log-analytics-agent-linux.md#network).

> [!NOTE]
> Als uw Linux-systemen geconfigureerde toocommunicate met een proxy of Gateway OMS worden en u voorbereiden op deze oplossing werk Hallo *proxy.conf* toogrant hello omiuser machtigingsgroep leesmachtiging op Hallo-bestand door Hallo volgende opdrachten uitvoeren:  
> `sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/proxy.conf`  
> `sudo chmod 644 /etc/opt/microsoft/omsagent/proxy.conf`


Bij pas toegevoegde Linux-agents staat de status **Bijgewerkt** na het uitvoeren van een beoordeling.  Dit proces kan too6 uren duren.

tooconfirm een Operations Manager-beheergroep communiceert met OMS, Zie [Operations Manager-integratie valideren met OMS](../log-analytics/log-analytics-om-agents.md#validate-operations-manager-integration-with-oms).

## <a name="data-collection"></a>Gegevensverzameling
### <a name="supported-agents"></a>Ondersteunde agents
Hallo volgende tabel beschrijft Hallo verbonden gegevensbronnen die worden ondersteund door deze oplossing.

| Verbonden bron | Ondersteund | Beschrijving |
| --- | --- | --- |
| Windows-agents |Ja |Hallo oplossing verzamelt informatie over systeemupdates van Windows-agents en start de installatie van vereiste updates. |
| Linux-agents |Ja |Hallo oplossing verzamelt informatie over systeemupdates van Linux-agents en installatie van vereiste updates op ondersteunde distributies initieert. |
| Beheergroep Operations Manager |Ja |Hallo oplossing verzamelt informatie over systeemupdates van agents in een verbonden beheergroep.<br>Een rechtstreekse verbinding tussen Hallo Operations Manager-agent tooLog Analytics is niet vereist. Gegevens doorgestuurd vanuit Hallo management groep toohello OMS-opslagplaats. |
| Azure Storage-account |Nee |Azure Storage bevat geen informatie over systeemupdates. |

### <a name="collection-frequency"></a>Verzamelingsfrequentie
Voor elke beheerde Windows-computer wordt twee keer per dag een scan uitgevoerd. Elke 15 minuten Hallo Windows-API wordt aangeroepen tooquery voor Hallo laatste update tijd toodetermine als de status is gewijzigd en als dat het geval er een scan voor naleving wordt gestart.  Voor elke beheerde Linux-computer wordt elke drie uur een scan uitgevoerd.

Het kan duren van 30 minuten too6 uur voor Hallo dashboard toodisplay bijgewerkt gegevens van beheerde computers.   

## <a name="using-hello-solution"></a>Met behulp van Hallo-oplossing
Wanneer u Hallo updatebeheer oplossing tooyour OMS-werkruimte toevoegt, Hallo **updatebeheer** tegel tooyour OMS dashboard worden toegevoegd. Deze tegel wordt een aantal en de grafische weergave van Hallo aantal computers in uw omgeving en de updatenaleving ervan weergegeven.<br><br>
![Tegel overzicht updatebeheer](media/oms-solution-update-management/update-management-summary-tile.png)  


## <a name="viewing-update-assessments"></a>Update-evaluaties weergeven
Klik op Hallo **updatebeheer** tegel tooopen hello **updatebeheer** dashboard.<br><br> ![Dashboard overzicht updatebeheer](./media/oms-solution-update-management/update-management-dashboard.png)<br>

Dit dashboard biedt een gedetailleerd overzicht van de updatestatus, ingesteld op type besturingssysteem en updateclassificatie (kritiek, beveiligingsgerelateerd of anders, zoals bij een definitie-update). Hallo resultaten in elke tegel in dit dashboard geven alleen updates die zijn goedgekeurd voor implementatie, die is gebaseerd op basis van synchronisatiebron Hallo-computers.   Hallo **Update-implementaties** tegel wanneer geselecteerd, wordt doorgestuurd toohello Update-implementaties pagina kunt u schema's wordt uitgevoerd, voltooide implementaties, implementaties weergeven of een nieuwe implementatie plannen.  

U kunt uitvoeren van een logboek-zoekquery waarmee alle records door te klikken op de specifieke tegel Hallo of toorun een query voor een bepaalde categorie en vooraf gedefinieerde criteria, selecteer één van Hallo lijst onder Hallo **algemene query's voor Update** kolom.    

## <a name="installing-updates"></a>Updates installeren
Nadat updates zijn beoordeeld voor alle Hallo Linux en Windows-computers in uw werkruimte, kan de vereiste updates zijn geïnstalleerd door het maken van een *Update-implementatie*.  Een update-implementatie is een geplande installatie van de vereiste updates voor een of meer computers.  U Geef Hallo-datum en tijd voor de implementatie van Hallo bovendien tooa computer of groep computers die moeten worden opgenomen in het Hallo-bereik van een implementatie.  toolearn meer informatie over computergroepen, Zie [computergroepen in logboekanalyse](../log-analytics/log-analytics-computer-groups.md).  Wanneer u computergroepen in de installatie van updates opneemt, wordt slechts één keer groep memnbership geëvalueerd op Hallo moment schema gemaakt.  Wijzigingen tooa groep worden niet weergegeven.  toowork dit, Hallo geplande update-implementatie en maak deze opnieuw.

> [!NOTE]
> Windows geïmplementeerde virtuele machines van hello Azure Marketplace standaard tooreceive automatische updates van Windows Update-Service zijn ingesteld.  Dit gedrag wordt niet gewijzigd na het toevoegen van deze oplossing of VM's van Windows tooyour werkruimte.  Als u niet actief beheerde updates met deze oplossing dit, Hallo standaardgedrag (automatisch updates van toepassing) wordt toegepast.  

Voor virtuele machines gemaakt op basis van Hallo op aanvraag Red Hat Enterprise Linux (RHEL) installatiekopieën beschikbaar in Azure Marketplace, zijn ze geregistreerde tooaccess hello [Red Hat Update-infrastructuur (RHUI)](../virtual-machines/virtual-machines-linux-update-infrastructure-redhat.md) geïmplementeerd in Azure.  Alle Linux-distributie moet worden bijgewerkt vanuit Hallo distributies online bestandsopslagplaats volgende hun ondersteunde methoden.  

### <a name="viewing-update-deployments"></a>Update-implementaties weergeven
Klik op Hallo **Update-implementatie** tegel tooview Hallo lijst met bestaande Update-implementaties.  Ze zijn gegroepeerd op status – **Gepland**, **Wordt uitgevoerd** en **voltooid**.<br><br> ![Pagina Planning update-implementaties](./media/oms-solution-update-management/update-updatedeployment-schedule-page.png)<br>  

Hallo eigenschappen worden weergegeven voor elke Update-implementatie worden beschreven in de volgende tabel Hallo.

| Eigenschap | Beschrijving |
| --- | --- |
| Naam |Naam van het Hallo-Update-implementatie. |
| Planning |Type planning.  Beschikbare opties zijn *één keer*, *elke week* en *elke maand*. |
| Begintijd |Datum en tijd waarop het Hallo-Update-implementatie is gepland toostart. |
| Duur |Het aantal minuten Hallo-Update-implementatie toorun is toegestaan.  Als alle updates niet binnen deze duur zijn geïnstalleerd en vervolgens de resterende updates Hallo moet wachten tot Hallo volgende Update-implementatie. |
| Servers |Het aantal computers dat is beïnvloed door het Hallo-Update-implementatie.  |
| Status |Huidige status van het Hallo-Update-implementatie.<br><br>Mogelijke waarden zijn:<br>- Niet gestart<br>- Wordt uitgevoerd<br>- Voltooid |

Selecteer een voltooide Update-implementatie tooview detail welkomstscherm waaronder Hallo kolommen in de volgende tabel Hallo.  Deze kolommen zal worden ingevuld indien Hallo-Update-implementatie niet nog niet gestart.<br><br> ![Overzicht van de resultaten van de update-implementatie](./media/oms-solution-update-management/update-management-deploymentresults-dashboard.png)

| Kolom | Beschrijving |
| --- | --- |
| **Weergave voor computers** | |
| Windows-computers |Hallo-nummer van de Windows-computers in het Hallo-Update-implementatie per status bevat.  Klik op een toorun status een logboek zoekopdracht retourneren van dat alle records bijwerken met de status voor Hallo implementatie-Update. |
| Linux-computers |Hallo aantal Linux-computers in het Hallo-Update-implementatie per status bevat.  Klik op een toorun status een logboek zoekopdracht retourneren van dat alle records bijwerken met de status voor Hallo implementatie-Update. |
| Installatiestatus computer |Geeft een lijst Hallo computers die zijn betrokken bij Hallo-Update-implementatie en Hallo percentage van de updates die is geïnstalleerd. Klik op een van de Hallo vermeldingen toorun een logboek zoekopdracht retourneren van alle ontbrekende en essentiële updates. |
| **Weergave voor updates** | |
| Windows-updates |Geeft een lijst van Windows-updates die zijn opgenomen in Hallo implementatie-Update en de bijbehorende installatiestatus per elke update.  Selecteer een update toorun een logboek zoekopdracht alle records voor die specifieke update bij te werken of klik op Hallo status toorun een logboek zoekopdracht retourneren van dat alle records voor de implementatie van Hallo bijwerken retourneren. |
| Linux-updates |Geeft een lijst van Linux-updates die zijn opgenomen in Hallo implementatie-Update en de bijbehorende installatiestatus per elke update.  Selecteer een update toorun een logboek zoekopdracht alle records voor die specifieke update bij te werken of klik op Hallo status toorun een logboek zoekopdracht retourneren van dat alle records voor de implementatie van Hallo bijwerken retourneren. |

### <a name="creating-an-update-deployment"></a>Een update-implementatie maken
Maak een nieuwe Update-implementatie door te klikken op Hallo **toevoegen** knop bovenaan Hallo Hallo scherm tooopen hello **nieuwe Update-implementatie** pagina.  U moet waarden opgeven voor Hallo eigenschappen in de volgende tabel Hallo.

| Eigenschap | Beschrijving |
| --- | --- |
| Naam |Unieke naam tooidentify Hallo-update-implementatie. |
| Tijdzone |Tijdzone toouse voor Hallo begintijd. |
| Planningstype | Type planning.  Beschikbare opties zijn *één keer*, *elke week* en *elke maand*.  
| Begintijd |Datum en tijd toostart Hallo-update-implementatie. **Opmerking:** Hallo eerste aflopen kan worden uitgevoerd in een implementatie is 30 minuten van huidige tijd als u onmiddellijk toodeploy nodig. |
| Duur |Het aantal minuten Hallo-Update-implementatie toorun is toegestaan.  Als alle updates niet binnen deze duur zijn geïnstalleerd en vervolgens de resterende updates Hallo moet wachten tot Hallo volgende Update-implementatie. |
| Computers |Namen van computers of groepen tooinclude van computer- en doel in Hallo-Update-implementatie.  Selecteer een of meer vermeldingen in de vervolgkeuzelijst Hallo. |

<br><br> ![Pagina Nieuwe update-implementatie](./media/oms-solution-update-management/update-newupdaterun-page.png)

### <a name="time-range"></a>Tijdsbereik
Hallo-bereik van Hallo-gegevens geanalyseerd in Hallo oplossing voor het beheer van de Update is standaard van alle verbonden beheergroepen gegenereerd binnen Hallo afgelopen dag.

toochange hello tijdsbereik Hallo gegevens, selecteer **gegevens op basis van** Hallo boven aan het Hallo-dashboard. U kunt selecteren records gemaakt of bijgewerkt binnen Hallo afgelopen 7 dagen, 1 dag of 6 uur. U kunt ook **Aangepast** selecteren en een aangepast datumbereik opgeven.

## <a name="log-analytics-records"></a>Log Analytics-records
Hallo updatebeheer oplossing maakt twee soorten records in Hallo OMS-opslagplaats.

### <a name="update-records"></a>Records bijwerken
Een record met het type **Bijwerken** wordt gemaakt voor elke update die is geïnstalleerd of vereist is op elke computer. Update-records hebben Hallo eigenschappen in de volgende tabel Hallo.

| Eigenschap | Beschrijving |
| --- | --- |
| Type |*Update* |
| SourceSystem |Hallo-bron die installatie van Hallo-update is goedgekeurd.<br>Mogelijke waarden zijn:<br>- Microsoft Update<br>- Windows Update<br>- SCCM<br>- Linux-servers (opgehaald van pakketbeheer) |
| Goedgekeurd |Hiermee geeft u op of Hallo-update is goedgekeurd voor installatie.<br> Voor Linux-servers is dit momenteel optioneel omdat patchen niet wordt beheerd door OMS. |
| Classificatie voor Windows |Classificatie van Hallo-update.<br>Mogelijke waarden zijn:<br>-    Toepassingen<br>- Essentiële updates<br>- Definitie-updates<br>- Functiepakketten<br>- Beveiligingsupdates<br>- Servicepacks<br>- Updatepakketten<br>- Updates |
| Classificatie voor Linux |Cassification van Hallo-update.<br>Mogelijke waarden zijn:<br>- Essentiële updates<br>- Beveiligingsupdates<br>- Andere Updates |
| Computer |Naam van het Hallo-computer. |
| InstallTimeAvailable |Hiermee geeft u op of Hallo installatietijd beschikbaar is van andere geïnstalleerde agents dezelfde Hallo bijwerken. |
| InstallTimePredictionSeconds |Geschatte installatietijd (in seconden) op basis van andere geïnstalleerde agents Hallo dezelfde update. |
| KBID |ID van Hallo KB-artikel waarin wordt beschreven Hallo-update. |
| ManagementGroupName |De naam van de beheergroep Hallo voor SCOM-agents.  Voor andere agents is dit AOI -<workspace ID>. |
| MSRCBulletinID |ID van Hallo Microsoft-beveiligingsbulletin Hallo update beschrijven. |
| MSRCSeverity |Ernst van de Microsoft-beveiligingsbulletin Hallo.<br>Mogelijke waarden zijn:<br>- Kritiek<br>- Belangrijk<br>- Gemiddeld |
| Optioneel |Hiermee geeft u op of Hallo-update optioneel is. |
| Product |Naam van de productupdate Hallo Hallo is voor.  Klik op **weergave** tooopen Hallo artikel in een browser. |
| PackageSeverity |Hallo ernst van Hallo-probleem opgelost in deze update, zoals gemeld door Hallo Linux distro leveranciers. |
| PublishDate |Datum en tijd waarop Hallo update is geïnstalleerd. |
| RebootBehavior |Hiermee wordt aangegeven als update Hallo opnieuw opstarten afgedwongen.<br>Mogelijke waarden zijn:<br>- canrequestreboot<br>- neverreboots |
| RevisionNumber |Het revisienummer van Hallo-update. |
| SourceComputerId |GUID toouniquely Hallo computer identificeren. |
| TimeGenerated |Datum en tijd waarop Hallo record voor het laatst is bijgewerkt. |
| Titel |De titel van het Hallo-update. |
| UpdateID |GUID toouniquely identificeren Hallo-update. |
| UpdateState |Hiermee geeft u op of Hallo-update is geïnstalleerd op deze computer.<br>Mogelijke waarden zijn:<br>-Geïnstalleerd - is Hallo-update geïnstalleerd op deze computer.<br>-Nodig - Hallo-update is niet geïnstalleerd en is vereist op deze computer. |

Wanneer u een logboek zoekquery waarmee records met een type uitvoert **Update** kunt u Hallo **Updates** weergave waarin een verzameling tegels samenvatten Hallo-updates die zijn geretourneerd door Hallo zoeken. U kunt klikken op Hallo vermeldingen in Hallo **ontbreekt en toegepaste updates** en **vereiste en optionele updates** tegels tooscope Hallo weergeven toothat instellen van updates. Selecteer Hallo **lijst** of **tabel** tooreturn Hallo afzonderlijke records weergeven.<br>

![Weergave update logboekzoekactie met Recordtype update](./media/oms-solution-update-management/update-la-view-updates.png)  

In Hallo **tabel** weergeven, kunt u klikken op Hallo **KBID** voor elke record tooopen een browser met Hallo KB-artikel. Hiermee kunt u tooquickly lezen over de details op Hallo van bepaalde Hallo-update.<br>

![Weergave tabel logboekzoekactie met tegels recordtype updates](./media/oms-solution-update-management/update-la-view-table.png)

In Hallo **lijst** weergave u klikt op Hallo **weergave** koppeling volgende toohello KBID tooopen Hallo KB-artikel.<br>

![Weergave lijst logboekzoekactie met tegels recordtype updates](./media/oms-solution-update-management/update-la-view-list.png)

### <a name="updatesummary-records"></a>UpdateSummary records
Een record van het type **UpdateSummary** wordt gemaakt voor elke Windows-agentcomputer. Deze record wordt telkens bijgewerkt wanneer Hallo computer wordt gescand op updates. **UpdateSummary** records Hallo eigenschappen in de volgende tabel Hallo hebben.

| Eigenschap | Beschrijving |
| --- | --- |
| Type |UpdateSummary |
| SourceSystem |OpsManager |
| Computer |Naam van het Hallo-computer. |
| CriticalUpdatesMissing |Het aantal essentiële updates ontbreken op Hallo-computer. |
| ManagementGroupName |De naam van de beheergroep Hallo voor SCOM-agents. Voor andere agents is dit AOI -<workspace ID>. |
| NETRuntimeVersion |De versie van Hallo .NET runtime op Hallo computer geïnstalleerd. |
| OldestMissingSecurityUpdateBucket |Bucket toocategorize Hallo tijd sinds Hallo oudste ontbrekende beveiligingsupdate op deze computer is gepubliceerd.<br>Mogelijke waarden zijn:<br>- Ouder<br>-    180 dagen geleden<br>- 150 dagen geleden<br>-    120 dagen geleden<br>- 90 dagen geleden<br>- 60dagen geleden<br>-    30 dagen geleden<br>-    Recent |
| OldestMissingSecurityUpdateInDays |Aantal dagen sinds Hallo oudste ontbrekende beveiligingsupdate op deze computer is gepubliceerd. |
| OsVersion |Versie van besturingssysteem Hallo op Hallo computer geïnstalleerd. |
| OtherUpdatesMissing |Het aantal andere updates ontbreken op Hallo-computer. |
| SecurityUpdatesMissing |Het aantal beveiligingsupdates ontbreken op Hallo-computer. |
| SourceComputerId |GUID toouniquely Hallo computer identificeren. |
| TimeGenerated |Datum en tijd waarop Hallo record voor het laatst is bijgewerkt. |
| TotalUpdatesMissing |Totaal aantal updates ontbreken op Hallo-computer. |
| WindowsUpdateAgentVersion |Versienummer van Windows Update-agent op de computer Hallo Hallo. |
| WindowsUpdateSetting |Instelling voor hoe Hallo computer belangrijke updates worden geïnstalleerd.<br>Mogelijke waarden zijn:<br>- Uitgeschakeld<br>- Waarschuwen vóór installatie<br>- Geplande installatie |
| WSUSServer |URL van de WSUS-server als Hallo computer geconfigureerd toouse een. |

## <a name="sample-log-searches"></a>Voorbeeldzoekopdrachten in logboeken
Hallo volgende tabel biedt een voorbeeld-logboek zoekt bijwerkrecords die door deze oplossing worden verzameld.

| Query’s uitvoeren | Beschrijving |
| --- | --- |
| Type:Update OSType!=Linux UpdateState=Needed Optional=false Approved!=false &#124; measure count() by Computer |Servercomputers met Windows die moeten worden bijgewerkt |
| Type:Update OSType=Linux UpdateState!="Not needed" &#124; measure count() by Computer |Linux-servers die moeten worden bijgewerkt | 
| Type=Update UpdateState=Needed Optional=false &#124; select Computer,Title,KBID,Classification,UpdateSeverity,PublishedDate |Alle computers met ontbrekende updates |
| Type=Update UpdateState=Needed Optional=false Computer="COMPUTER01.contoso.com" &#124; select Computer,Title,KBID,Product,UpdateSeverity,PublishedDate |Ontbrekende updates voor een specifieke computer (vervang de waarde door de naam van uw eigen computer)|
| Type=Update UpdateState=Needed Optional=false (Classification="Security Updates" OR Classification="Critical Updates") |Alle computers met ontbrekende essentiële of beveiligingsupdates | 
| Type=Update UpdateState=Needed Optional=false (Classification="Security Updates" OR Classification="Critical Updates") Computer IN {Type=UpdateSummary WindowsUpdateSetting=Manual &#124; Distinct Computer} &#124; Distinct KBID |Essentiële of beveiligingsupdates die benodigd zijn door machines wanneer updates handmatig worden toegepast |
| Type=Event EventLevelName=error Computer IN {Type=Update (Classification="Security Updates" OR Classification="Critical Updates") UpdateState=Needed Optional=false &#124; Distinct Computer} |Foutgebeurtenissen voor machines met ontbrekende essentiële of beveiligingsupdates |
| Type=Update Optional=false Classification="Update Rollups" UpdateState=Needed &#124; select Computer,Title,KBID,Classification,UpdateSeverity,PublishedDate |Alle computers met ontbrekende updatepakketten | 
| Type=Update UpdateState=Needed Optional=false &#124; Distinct Title |Afzonderlijke ontbrekende updates op alle computers | 
| Type:UpdateRunProgress InstallationStatus=failed &#124; measure count() by Computer, Title, UpdateRunName |Windows-servercomputer met updates die zijn mislukt tijdens het uitvoeren van updates | 
| Type:UpdateRunProgress InstallationStatus=failed &#124; measure count() by Computer, Product, UpdateRunName |Linux-server met updates die zijn mislukt tijdens het uitvoeren van updates | 
| Type=UpdateSummary &#124; measure count() by WSUSServer |WSUS-computerlidmaatschap | 
| Type=UpdateSummary &#124; measure count() by WindowsUpdateSetting |Configuratie automatische updates | 
| Type=UpdateSummary WindowsUpdateSetting=Manual |Computers met automatische update uitgeschakeld | 
| Type=Update and OSType=Linux and UpdateState!="Not needed" &#124; measure count() by Computer |Lijst met alle Hallo Linux-machines waarvoor een pakketupdate beschikbaar | 
| Type=Update and OSType=Linux and UpdateState!="Not needed" and (Classification="Critical Updates" OR Classification="Security Updates") &#124; measure count() by Computer |Lijst van alle Hallo Linux-machines waarvoor een pakketupdate beschikbaar die hierin beveiligingslek essentiële of beveiligingsupdates | 
| Type=Update and OSType=Linux and UpdateState!="Not needed" |Lijst met alle pakketten waarvoor een update beschikbaar is | 
| Type=Update  and OSType=Linux and UpdateState!="Not needed" and (Classification="Critical Updates" OR Classification="Security Updates") |Lijst met alle pakketten waarvoor een update beschikbaar die essentiële of beveiligingskwetsbaarheid oplost | 
| Type:UpdateRunProgress &#124; measure Count() by UpdateRunName |Weergeven met welke update-implementaties computers zijn gewijzigd | 
| Type:UpdateRunProgress UpdateRunName="DeploymentName" &#124; measure Count() by Computer |Computers die zijn bijgewerkt tijdens het uitvoeren van updates (vervang de waarde met de naam van uw update-implementatie) | 
| Type=Update and OSType=Linux and OSName = Ubuntu &#124; measure count() by Computer |Lijst met alle Hallo 'Ubuntu' machines met een update beschikbaar | 

## <a name="troubleshooting"></a>Problemen oplossen

Deze sectie bevat informatie toohelp problemen oplossen met Hallo oplossing voor het beheer van de Update.  

### <a name="how-do-i-troubleshoot-onboarding-issues"></a>Hoe kan ik problemen met onboarding oplossen?
Als u problemen ondervindt tijdens een poging tooonboard Hallo oplossing of een virtuele machine, Controleer Hallo **toepassingen en Services Logs\Operations Manager** gebeurtenislogboek voor gebeurtenissen met de ID 4502 en gebeurtenis gebeurtenisbericht met **Microsoft.EnterpriseManagement.HealthService.AzureAutomation.HybridAgent**.  Hallo volgende tabel licht de specifieke foutberichten en een mogelijke oplossing voor elk.  

| Bericht | Reden | Oplossing |   
|----------|----------|----------|  
| Kan geen tooRegister Machine voor het beheer van de Patch<br>Registratie is mislukt met uitzondering<br>System.InvalidOperationException: {"Message":"Machine is al<br>geregistreerd tooa ander account. "} | Computer is al vrijgegeven tooanother werkruimte voor updatebeheer | Voer het opruimen van de oude artefacten door [Hallo hybrid runbook-groep verwijderen](../automation/automation-hybrid-runbook-worker.md#remove-hybrid-worker-groups)|  
| Kan geen te registreren Machine voor het beheer van de Patch<br>Registratie is mislukt met uitzondering<br>System.Net.Http.HttpRequestException: Er is een fout opgetreden tijdens het Hallo-aanvraag verzenden. ---><br>System.Net.WebException: Hallo onderliggende verbinding<br>is gesloten: Er is een onverwachte fout<br>opgetreden tijdens het ontvangen. ---> System.ComponentModel.Win32Exception:<br>Hallo-client en server niet kunnen communiceren,<br>omdat ze geen gemeenschappelijk algoritme hebben | Communicatie wordt geblokkeerd door proxy/gateway/firewall | [Netwerkvereisten bekijken](../automation/automation-offering-get-started.md#network-planning)|  
| Kan geen tooRegister Machine voor het beheer van de Patch<br>Registratie is mislukt met uitzondering<br>Newtonsoft.Json.JsonReaderException: Fout tijdens het parseren van oneindig positieve waarde. | Communicatie wordt geblokkeerd door proxy/gateway/firewall | [Netwerkvereisten bekijken](../automation/automation-offering-get-started.md#network-planning)| 
| Hallo certificaat doorgegeven door de service Hallo <wsid>. oms.opinsights.azure.com<br>is niet uitgegeven door een certificeringsinstantie<br>die wordt gebruikt voor Microsoft-services. Neem contact op met<br>uw netwerk beheerder toosee als er een proxy die onderschept worden uitgevoerd<br>TLS/SSL-communicatie wordt onderschept. |Communicatie wordt geblokkeerd door proxy/gateway/firewall | [Netwerkvereisten bekijken](../automation/automation-offering-get-started.md#network-planning)|  
| Kan geen tooRegister Machine voor het beheer van de Patch<br>Registratie is mislukt met uitzondering<br>AgentService.HybridRegistration.<br>PowerShell.Certificates.CertificateCreationException:<br>Kan geen toocreate een zelfondertekend certificaat. ---><br>System.UnauthorizedAccessException: Toegang is geweigerd. | Genereren van zelfondertekend certificaat is mislukt | Controleer of het systeemaccount<br>leestoegang toofolder:<br>**C:\ProgramData\Microsoft\**<br>**Crypto\RSA**|  

### <a name="how-do-i-troubleshoot-update-deployments"></a>Hoe kan ik problemen met update-implementaties oplossen?
U kunt Hallo resultaten van Hallo runbook die verantwoordelijk is voor het implementeren van Hallo-updates die zijn opgenomen in Hallo geplande update-implementatie van Hallo taken blade van uw Automation-account is gekoppeld aan Hallo OMS-werkruimte ondersteuning van deze oplossing weergeven.  Hallo runbook **Patch MicrosoftOMSComputer** is een onderliggend runbook die gericht is op een specifieke beheerde computer en controleren van de uitgebreide stroom hello wordt gedetailleerde informatie voor deze implementatie.  Hallo-uitvoer wordt weergegeven die updates van toepassing zijn vereist, status, status van de installatie en aanvullende details downloaden.<br><br> ![De taakstatus van de update-implementatie](media/oms-solution-update-management/update-la-patchrunbook-outputstream.png)<br>

Zie [Automation-runbookuitvoer en -berichten](../automation/automation-runbook-output-and-messages.md) voor meer informatie.   

## <a name="next-steps"></a>Volgende stappen
* Logboek van zoekopdrachten in gebruiken [logboekanalyse](../log-analytics/log-analytics-log-searches.md) tooview gedetailleerde gegevens bijwerken.
* [Maak uw eigen dashboards](../log-analytics/log-analytics-dashboards.md) die de updatecompatibiliteit voor uw beheerde computers weergeven.
* [Maak waarschuwingen](../log-analytics/log-analytics-alerts.md) wanneer wordt vastgesteld dat er essentiële updates ontbreken op de computers of als automatische updates is uitgeschakeld voor een computer.  
