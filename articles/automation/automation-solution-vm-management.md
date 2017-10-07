---
title: virtuele machines tijdens rustige uren [Preview] oplossing aaaStart/stoppen | Microsoft Docs
description: Hallo beheeroplossingen voor virtuele machine wordt gestart en uw virtuele Machines van Azure Resource Manager stopt volgens een schema en proactief bewaken van logboekanalyse.
services: automation
documentationCenter: 
authors: mgoedtel
manager: carmonm
editor: 
ms.assetid: 06c27f72-ac4c-4923-90a6-21f46db21883
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: magoedte
ms.openlocfilehash: 6cbe16dfb40bf13f29d9e58ca0bc8c5c7979879d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="startstop-vms-during-off-hours-preview-solution-in-automation"></a>Oplossing voor VM's starten/stoppen buiten kantooruren [Preview] in Automation

Hallo starten/stoppen virtuele machines tijdens rustige uren [Preview] oplossing wordt gestart en uw virtuele machines van Azure Resource Manager op een door de gebruiker gedefinieerde schema gestopt en biedt inzicht in Hallo geslaagd Hallo Automation taken starten en stoppen van uw virtuele machines met OMS Log Analytics.  

## <a name="prerequisites"></a>Vereisten

- Hallo runbooks werken met een [Azure uitvoeren als-account](automation-offering-get-started.md#authentication-methods).  Hallo Run As-account is Hallo voorkeurs-verificatiemethode omdat deze wordt certificaatverificatie gebruikt in plaats van een wachtwoord dat mogelijk verlopen of regelmatig wordt gewijzigd.  

- Deze oplossing kan alleen beheren voor virtuele machines die zich in Hallo hetzelfde abonnement als waarin Hallo Automation-account zich bevindt.  

- Deze oplossing implementeert alleen toohello volgende Azure-regio's - Australië-Zuidoost, VS-Oost, Zuidoost-Azië, en West-Europa.  Hallo-runbooks die Hallo VM planning beheren kan richten op virtuele machines in elke regio.  

- toosend e-mailmeldingen wanneer Hallo runbooks starten en stoppen VM voltooid, zakelijke Office 365-abonnement is vereist.  

## <a name="solution-components"></a>Oplossingsonderdelen

Deze oplossing bestaat uit Hallo na resources die worden geïmporteerd en tooyour Automation-account toegevoegd.

### <a name="runbooks"></a>Runbooks

Runbook | Beschrijving|
--------|------------|
CleanSolution-MS-Mgmt-VM | Dit runbook wordt alle ingesloten bronnen, en schema's verwijderd wanneer u toodelete Hallo oplossing uit uw abonnement gaat.|  
SendMailO365-MS-Mgmt | Met dit runbook wordt een e-mail verzonden via Office 365 Exchange.|
StartByResourceGroup-MS-Mgmt-VM | Dit runbook is bedoeld toostart VMs (zowel klassieke en virtuele machines op basis van ARM) die zich bevindt in een opgegeven lijst met Azure-resource groep(en).
StopByResourceGroup-MS-Mgmt-VM | Dit runbook is bedoeld toostop VMs (zowel klassieke en virtuele machines op basis van ARM) die zich bevindt in een opgegeven lijst met Azure-resource groep(en).|
<br>

### <a name="variables"></a>Variabelen

Variabele | Beschrijving|
---------|------------|
Runbook **SendMailO365-MS-Mgmt** ||
SendMailO365-IsSendEmail-MS-Mgmt | Hiermee wordt opgegeven of met de runbooks StartByResourceGroup-MS-Mgmt-VM en StopByResourceGroup-MS-Mgmt-VM e-mailmeldingen kunnen worden verzonden na voltooiing.  Selecteer **True** tooenable en **False** toodisable e-waarschuwingen. De standaardwaarde is **False**.| 
Runbook **StartByResourceGroup-MS-Mgmt-VM** ||
StartByResourceGroup-ExcludeList-MS-Mgmt-VM | Voer VM namen toobe uitgesloten van de bewerking voor het beheer; namen gescheiden door puntkomma (;) zonder spaties. Waarden zijn hoofdlettergevoelig en het jokerteken (sterretje) wordt ondersteund.|
StartByResourceGroup-SendMailO365-EmailBodyPreFix-MS-Mgmt | Tekst die kan worden toegevoegd toohello begin van de berichttekst Hallo-e-mailbericht.|
StartByResourceGroup-SendMailO365-EmailRunBookAccount-MS-Mgmt | Geeft de naam Hallo Hallo Automation-Account met Hallo e runbook.  **Deze variabele mag niet worden gewijzigd.**|
StartByResourceGroup-SendMailO365-EmailRunbookName-MS-Mgmt | Geeft de naam Hallo van Hallo e runbook.  Dit wordt gebruikt door Hallo StartByResourceGroup-MS-Mgmt-VM en StopByResourceGroup-MS-Mgmt-VM runbooks toosend e-mail.  **Deze variabele mag niet worden gewijzigd.**|
StartByResourceGroup-SendMailO365-EmailRunbookResourceGroup-MS-Mgmt | Hiermee geeft u Hallo-naam van resourcegroep Hallo die Hallo e runbook bevat.  **Deze variabele mag niet worden gewijzigd.**|
StartByResourceGroup-SendMailO365-EmailSubject-MS-Mgmt | Hiermee geeft u Hallo tekst voor de onderwerpregel Hallo Hallo e-mailadres.|  
StartByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt | Hiermee geeft u Hallo geadresseerde(n) Hallo e-mailadres.  Voer de namen van de afzonderlijke puntkomma (;) zonder spaties.|
StartByResourceGroup-TargetResourceGroups-MS-Mgmt-VM | Voer VM namen toobe uitgesloten van de bewerking voor het beheer; namen gescheiden door puntkomma (;) zonder spaties. Waarden zijn hoofdlettergevoelig en het jokerteken (sterretje) wordt ondersteund.  De standaardwaarde (sterretje) neemt alle resourcegroepen in Hallo-abonnement.|
StartByResourceGroup-TargetSubscriptionID-MS-Mgmt-VM | Hiermee geeft u Hallo-abonnement dat virtuele machines toobe beheerd door deze oplossing bevat.  Dit moet Hallo hetzelfde abonnement waarin Hallo Automation-account van deze oplossing zich bevindt.|
Runbook **StopByResourceGroup-MS-Mgmt-VM** ||
StopByResourceGroup-ExcludeList-MS-Mgmt-VM | Voer VM namen toobe uitgesloten van de bewerking voor het beheer; namen gescheiden door puntkomma (;) zonder spaties. Waarden zijn hoofdlettergevoelig en het jokerteken (sterretje) wordt ondersteund.|
StopByResourceGroup-SendMailO365-EmailBodyPreFix-MS-Mgmt | Tekst die kan worden toegevoegd toohello begin van de berichttekst Hallo-e-mailbericht.|
StopByResourceGroup-SendMailO365-EmailRunBookAccount-MS-Mgmt | Geeft de naam Hallo Hallo Automation-Account met Hallo e runbook.  **Deze variabele mag niet worden gewijzigd.**|
StopByResourceGroup-SendMailO365-EmailRunbookResourceGroup-MS-Mgmt | Hiermee geeft u Hallo-naam van resourcegroep Hallo die Hallo e runbook bevat.  **Deze variabele mag niet worden gewijzigd.**|
StopByResourceGroup-SendMailO365-EmailSubject-MS-Mgmt | Hiermee geeft u Hallo tekst voor de onderwerpregel Hallo Hallo e-mailadres.|  
StopByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt | Hiermee geeft u Hallo geadresseerde(n) Hallo e-mailadres.  Voer de namen van de afzonderlijke puntkomma (;) zonder spaties.|
StopByResourceGroup-TargetResourceGroups-MS-Mgmt-VM | Voer VM namen toobe uitgesloten van de bewerking voor het beheer; namen gescheiden door puntkomma (;) zonder spaties. Waarden zijn hoofdlettergevoelig en het jokerteken (sterretje) wordt ondersteund.  De standaardwaarde (sterretje) neemt alle resourcegroepen in Hallo-abonnement.|
StopByResourceGroup-TargetSubscriptionID-MS-Mgmt-VM | Hiermee geeft u Hallo-abonnement dat virtuele machines toobe beheerd door deze oplossing bevat.  Dit moet Hallo hetzelfde abonnement waarin Hallo Automation-account van deze oplossing zich bevindt.|  
<br>

### <a name="schedules"></a>Planningen

Planning | Beschrijving|
---------|------------|
StartByResourceGroup-schema-MS-Mgmt | Planning voor StartByResourceGroup runbook waarmee Hallo opstarten van virtuele machines die worden beheerd door deze oplossing. Wanneer u maakt, wordt standaard tooUTC tijdzone.|
StopByResourceGroup-Schedule-MS-Mgmt | Planning voor StopByResourceGroup runbook waarmee Hallo afsluiten van de virtuele machines die worden beheerd door deze oplossing. Wanneer u maakt, wordt standaard tooUTC tijdzone.|

### <a name="credentials"></a>Referenties

Referentie | Beschrijving|
-----------|------------|
O365Credential | Hiermee geeft u een geldige Office 365-account toosend e-mailadres gebruiker.  Alleen vereist als de variabele SendMailO365-IsSendEmail-MS-Mgmt te is ingesteld**True**.

## <a name="configuration"></a>Configuratie

Hallo stappen tooadd Hallo starten/stoppen virtuele machines tijdens rustige uren [Preview] oplossing tooyour Automation-account na uitvoeren en configureer vervolgens Hallo variabelen toocustomize Hallo oplossing.

1. Hallo-beginscherm in hello Azure-portal, selecteer Hallo **Marketplace** tegel.  Selecteer als Hallo tegel niet langer vastgemaakt tooyour-beginscherm van Hallo navigatiedeelvenster links is **nieuw**.  
2. Hallo Marketplace blade Typ **VM starten** in het zoekvak Hallo en selecteer vervolgens Hallo oplossing **starten/stoppen virtuele machines [Preview] buiten kantooruren** van Hallo zoekresultaten.  
3. In Hallo **starten/stoppen virtuele machines [Preview] buiten kantooruren** blade voor Hallo oplossing geselecteerd, Controleer de overzichtsgegevens Hallo en klik op **maken**.  
4. Hallo **oplossing toevoegen** blade weergegeven waarbij u na vragen aan gebruiker tooconfigure Hallo oplossing voordat u deze in uw Automation-abonnement importeren kunt.<br><br> ![Blade Oplossing toevoegen voor VM-beheer](media/automation-solution-vm-management/vm-management-solution-add-solution-blade.png)<br><br>
5.  Op Hallo **oplossing toevoegen** blade Selecteer **werkruimte** en hier het selecteren van een OMS-werkruimte die gekoppelde toohello dezelfde Azure-abonnement dat Hallo Automation-account is in of maak een nieuwe OMS-werkruimte.  Als u een OMS-werkruimte niet hebt, kunt u **nieuwe werkruimte maken** en op Hallo **OMS-werkruimte** blade Hallo volgende uitvoeren: 
   - Geef een naam voor de nieuwe Hallo **OMS-werkruimte**.
   - Selecteer een **abonnement** toolink tooby selecteren in de vervolgkeuzelijst Hallo als Hallo standaard geselecteerd niet geschikt is.
   - Voor **Resourcegroep** kunt u een nieuwe resourcegroep maken of een bestaande resourcegroep selecteren.  
   - Selecteer een **locatie**.  Hallo enige locaties die worden opgegeven voor selectie zijn momenteel **Australië-Zuidoost**, **VS-Oost**, **Zuidoost-Azië**, en **West-Europa**.
   - Selecteer een **prijscategorie**.  Hallo-oplossing wordt aangeboden in twee lagen: vrij en OMS betaald laag.  Hallo gratis laag heeft een limiet op Hallo hoeveelheid gegevens die worden verzameld per dag, bewaarperiode en runbook-taak runtime minuten.  Hallo OMS betaald laag heeft geen een limiet op Hallo hoeveelheid dagelijks verzamelde gegevens.  

        > [!NOTE]
        > Tijdens het Hallo zelfstandige betaald laag wordt weergegeven als een optie, is het niet van toepassing.  Als u selecteert en verdergaan met het maken van deze oplossing Hallo in uw abonnement, wordt het mislukken.  Dit wordt opgelost bij de officiële release van deze oplossing.<br>Als u deze oplossing gebruikt, worden alleen Automation-taakminuten en logopname gebruikt.  Hallo-oplossing voegt geen extra OMS knooppunten tooyour omgeving.  

6. Na het opgeven van Hallo vereiste informatie op Hallo **OMS-werkruimte** blade, klikt u op **maken**.  Tijdens het Hallo-informatie is geverifieerd en Hallo werkruimte wordt gemaakt, kunt u de voortgang onder bijhouden **meldingen** in Hallo-menu.  Keert u terug toohello **oplossing toevoegen** blade.  
7. Op Hallo **oplossing toevoegen** blade Selecteer **Automation-Account**.  Als u een nieuwe OMS-werkruimte maakt, kunt u zich vereist tooalso maakt een nieuw Automation-account worden gekoppeld aan Hallo nieuwe OMS-werkruimte opgegeven eerder, met inbegrip van uw Azure-abonnement, de resourcegroep en de regio.  U kunt selecteren **een Automation-account maken** en op Hallo **toevoegen Automation-account** blade biedt Hallo volgende: 
  - In Hallo **naam** Hallo naam Hallo Automation-account.

    Alle andere opties worden automatisch ingevuld op basis van Hallo OMS-werkruimte geselecteerd en deze opties kunnen niet worden gewijzigd.  Een Azure uitvoeren als-account is Hallo standaardmethode voor verificatie Hallo runbooks die zijn opgenomen in deze oplossing.  Nadat u op **OK**, Hallo configuratieopties worden gevalideerd en Hallo Automation-account is gemaakt.  U kunt de voortgang onder volgen **meldingen** in Hallo-menu. 

    U kunt ook een bestaand Uitvoeren als-account voor Automation selecteren.  Houd er rekening mee dat Hallo-account die u selecteert al mag geen gekoppelde tooanother OMS-werkruimte, anders een bericht weergegeven in Hallo blade tooinform u.  Als deze al is gekoppeld, wordt u moet tooselect een ander Automation Run As-account of maak een nieuwe.<br><br> ![Automation-Account al gekoppelde tooOMS werkruimte](media/automation-solution-vm-management/vm-management-solution-add-solution-blade-autoacct-warning.png)<br>

8. Ten slotte op Hallo **oplossing toevoegen** blade Selecteer **configuratie** en Hallo **Parameters** blade wordt weergegeven.  Op Hallo **Parameters** blade u wordt gevraagd:  
   - Geef Hallo **ResourceGroup doelnamen**, dit is de naam van een resource-groep die virtuele machines toobe beheerd door deze oplossing bevat.  U kunt meer dan één naam invoeren en de namen scheiden met een puntkomma (de waarden zijn hoofdlettergevoelig).  Met een jokerteken wordt ondersteund als u wilt dat tootarget VM's in alle resourcegroepen in Hallo-abonnement.
   - Selecteer een **planning** dit is een terugkerende datum en tijd voor starten en stoppen Hallo van de virtuele machine in Hallo doel resource groep(en).  Standaard Hallo planning is geconfigureerde toohello UTC-tijdzone en selecteren van een andere regio is niet beschikbaar.  Als u tooconfigure Hallo planning tooyour bepaalde tijdzone wenst na het Hallo-oplossing configureren, Zie [wijzigen Hallo opstarten en afsluiten planning](#modifying-the-startup-and-shutdown-schedule) hieronder.    

10. Zodra u configureren Hallo initiële instellingen die vereist zijn voor Hallo oplossing hebt voltooid, selecteert u **maken**.  Alle instellingen worden gevalideerd en vervolgens probeert toodeploy Hallo oplossing in uw abonnement.  Dit kan duren enkele seconden toocomplete en u kunt de voortgang onder volgen **meldingen** in Hallo-menu. 

## <a name="collection-frequency"></a>Verzamelingsfrequentie

Automation-logboek en taak stroom taakgegevens wordt ingenomen in Hallo OMS-opslagplaats om de vijf minuten.  

## <a name="using-hello-solution"></a>Met behulp van Hallo-oplossing

Wanneer u Hallo VM beheeroplossing toevoegt in de OMS-werkruimte Hallo **StartStopVM weergave** tegel tooyour OMS dashboard worden toegevoegd.  Deze tegel wordt weergegeven voor een aantal en de grafische weergave van Hallo runbooks taken voor het Hallo-oplossing die zijn gestart en zijn met succes voltooid.<br><br> ![Tegel Weergave StartStopVM voor VM-beheer](media/automation-solution-vm-management/vm-management-solution-startstopvm-view-tile.png)  

In uw Automation-account, kunt u toegang tot en beheren van Hallo oplossing door het selecteren van Hallo **oplossingen** tegel en klik vervolgens vanuit Hallo **oplossingen** blade Hallo oplossing selecteren **[begin Stop VM Werkruimte]** uit Hallo-lijst.<br><br> ![Lijst met Automation-oplossingen](media/automation-solution-vm-management/vm-management-solution-autoaccount-solution-list.png)  

Hallo-oplossing wordt weer te geven Hallo **Start Stop VM [werkruimte]** oplossing blade, waarin u belangrijke informatie zoals Hallo kunt bekijken **StartStopVM** tegel, zoals in de OMS-werkruimte die Geeft een aantal en de grafische weergave van Hallo runbooks taken voor het Hallo-oplossing die zijn gestart en zijn met succes voltooid.<br><br> ![Blade VM-oplossing Automation](media/automation-solution-vm-management/vm-management-solution-solution-blade.png)  

Hier kunt u ook de OMS-werkruimte te openen en verdere analyse van Hallo Taakrecords uitvoeren.  Klik op **alle instellingen**, en in Hallo **instellingen** blade, selecteer **Quick Start** en klik vervolgens in Hallo **Quick Start** blade Selecteer  **OMS-Portal**.   Hiermee opent u een nieuw tabblad of een nieuwe browsersessie en stelt u uw OMS-werkruimte voor die aan Automation-account en abonnement is gekoppeld.  


### <a name="configuring-e-mail-notifications"></a>E-mailmeldingen configureren

tooenable e-mailmeldingen wanneer hello runbooks starten en stoppen VM voltooid, moet u toomodify hello **O365Credential** referentie en ten minste Hallo volgende variabelen:

 - SendMailO365-IsSendEmail-MS-Mgmt
 - StartByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt
 - StopByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt

Hallo tooconfigure **O365Credential** referenties, voert u Hallo stappen te volgen:

1. Van uw automation-account, klikt u op **alle instellingen** Hallo boven aan het Hallo-venster. 
2. Op Hallo **instellingen** blade onder sectie Hallo **Automation-Resources**, selecteer **activa**. 
3. Op Hallo **activa** blade, selecteer Hallo **referentie** tegel en van Hallo **referentie** blade, selecteer Hallo **O365Credential**.  
4. Voer een geldige Office 365-gebruikersnaam en wachtwoord en klik vervolgens op **opslaan** toosave uw wijzigingen.  

tooconfigure hello variabelen eerder gemarkeerd uitvoeren Hallo stappen:

1. Van uw automation-account, klikt u op **alle instellingen** Hallo boven aan het Hallo-venster. 
2. Op Hallo **instellingen** blade onder sectie Hallo **Automation-Resources**, selecteer **activa**. 
3. Op Hallo **activa** blade, selecteer Hallo **variabelen** tegel en van Hallo **variabelen** blade Hallo variabele bovenstaande selecteren en te wijzigen met de waarde ervan Hallo na beschrijving voor het opgegeven in Hallo [variabele](##variables) eerder gedeelte.  
4. Klik op **opslaan** toosave Hallo wijzigingen toohello variabele.   

### <a name="modifying-hello-startup-and-shutdown-schedule"></a>Wijzigen Hallo-schema voor opstarten en afsluiten

Het beheren van het Hallo-opstarten en afsluiten schema in deze oplossing volgt Hallo dezelfde stappen zoals wordt beschreven in [plannen van een runbook in Azure Automation](automation-schedules.md).  Denk eraan dat u de configuratie van de planning Hallo niet wijzigen.  U moet toodisable Hallo bestaand schema en een nieuwe maken en koppelen toohello **StartByResourceGroup-MS-Mgmt-VM** of **StopByResourceGroup-MS-Mgmt-VM** runbook dat u wilt dat Hallo tooapply om te plannen.   

## <a name="log-analytics-records"></a>Log Analytics-records

Automation maakt twee soorten records in Hallo OMS-opslagplaats.

### <a name="job-logs"></a>Taaklogboeken

Eigenschap | Beschrijving|
----------|----------|
Caller |  Wie Hallo opnieuw gestart.  Mogelijke waarden zijn een e-mailadres of het systeem voor geplande taken.|
Category | Classificatie van Hallo type gegevens.  Hallo-waarde is voor automatisering kunt JobLogs.|
CorrelationId | De GUID die Hallo correlatie-Id van de runbooktaak Hallo.|
JobId | De GUID die Hallo-Id van de runbooktaak Hallo.|
operationName | Hiermee geeft u Hallo bewerking uitgevoerd in Azure.  Voor automatisering, wordt de taak in Hallo waarde zal worden.|
resourceId | Hiermee geeft u het brontype Hallo in Azure.  Hallo-waarde is voor automatisering kunt Hallo Automation-account gekoppeld Hallo runbook.|
ResourceGroup | Hiermee geeft u Hallo Resourcegroepnaam hello runbooktaak.|
ResourceProvider | Hiermee geeft u hello Azure-service die u levert Hallo resources implementeren en beheren.  Hallo-waarde is voor automatisering kunt Azure Automation.|
ResourceType | Hiermee geeft u het brontype Hallo in Azure.  Hallo-waarde is voor automatisering kunt Hallo Automation-account gekoppeld Hallo runbook.|
resultType | Hallo-status van de runbooktaak Hallo.  Mogelijke waarden zijn:<br>- Gestart<br>- Gestopt<br>- Onderbroken<br>- Mislukt<br>- Geslaagd|
resultDescription | Hierin wordt beschreven Hallo runbook taakstatus resultaat.  Mogelijke waarden zijn:<br>- Taak is gestart<br>- Taak is mislukt<br>- Taak is voltooid|
RunbookName | Geeft de naam Hallo van Hallo runbook.|
SourceSystem | Hiermee geeft u het bronsysteem Hallo voor Hallo gegevens verzonden.  Voor automatisering kunt Hallo waarde zal worden: OpsManager|
StreamType | Hiermee geeft u Hallo type gebeurtenis. Mogelijke waarden zijn:<br>- Uitgebreid<br>- Uitvoer<br>- Fout<br>- Waarschuwing|
SubscriptionId | Hiermee geeft u Hallo abonnements-ID van Hallo-taak.
Time | Datum en tijd wanneer de runbooktaak Hallo uitgevoerd.|


### <a name="job-streams"></a>Taakstromen

Eigenschap | Beschrijving|
----------|----------|
Caller |  Wie Hallo opnieuw gestart.  Mogelijke waarden zijn een e-mailadres of het systeem voor geplande taken.|
Category | Classificatie van Hallo type gegevens.  Hallo-waarde is voor automatisering kunt JobStreams.|
JobId | De GUID die Hallo-Id van de runbooktaak Hallo.|
operationName | Hiermee geeft u Hallo bewerking uitgevoerd in Azure.  Voor automatisering, wordt de taak in Hallo waarde zal worden.|
ResourceGroup | Hiermee geeft u Hallo Resourcegroepnaam hello runbooktaak.|
resourceId | Hiermee geeft u Hallo resource-Id in Azure.  Hallo-waarde is voor automatisering kunt Hallo Automation-account gekoppeld Hallo runbook.|
ResourceProvider | Hiermee geeft u hello Azure-service die u levert Hallo resources implementeren en beheren.  Hallo-waarde is voor automatisering kunt Azure Automation.|
ResourceType | Hiermee geeft u het brontype Hallo in Azure.  Hallo-waarde is voor automatisering kunt Hallo Automation-account gekoppeld Hallo runbook.|
resultType | Hallo-resultaat van de runbooktaak Hallo Hallo tijd Hallo gebeurtenis is gegenereerd.  Mogelijke waarden zijn:<br>- Wordt uitgevoerd|
resultDescription | Bevat de uitvoerstroom Hallo van Hallo runbook.|
RunbookName | Hallo-naam van Hallo runbook.|
SourceSystem | Hiermee geeft u het bronsysteem Hallo voor Hallo gegevens verzonden.  Hallo-waarde is voor automatisering kunt OpsManager|
StreamType | Hallo-type van de taakstroom. Mogelijke waarden zijn:<br>- Voortgang<br>- Uitvoer<br>- Waarschuwing<br>- Fout<br>- Foutopsporing<br>- Uitgebreid|
Time | Datum en tijd wanneer de runbooktaak Hallo uitgevoerd.|

Wanneer u een logboek zoekquery waarmee de records van de categorie van uitvoert **JobLogs** of **JobStreams**, kunt u Hallo **JobLogs** of **JobStreams** weergave waarin een verzameling tegels samenvatten Hallo-updates die zijn geretourneerd door Hallo zoeken.

## <a name="sample-log-searches"></a>Voorbeeldzoekopdrachten in logboeken

Hallo bevat volgende tabel voorbeelden logboek zoekt Taakrecords die door deze oplossing worden verzameld. 

Query’s uitvoeren | Beschrijving|
----------|----------|
Taken zoeken voor runbook StartVM die zijn voltooid | Category=JobLogs RunbookName_s="StartByResourceGroup-MS-Mgmt-VM" ResultType=Succeeded &#124; measure count() by JobId_g|
Taken zoeken voor runbook StopVM die zijn voltooid | Category=JobLogs RunbookName_s="StartByResourceGroup-MS-Mgmt-VM" ResultType=Failed &#124; measure count() by JobId_g
Taakstatus gedurende een periode weergeven voor runbooks StartVM en StopVM | Category=JobLogs RunbookName_s="StartByResourceGroup-MS-Mgmt-VM" OR "StopByResourceGroup-MS-Mgmt-VM" NOT(ResultType="started") | measure Count() by ResultType interval 1day|

## <a name="removing-hello-solution"></a>Hallo-oplossing wordt verwijderd

Als u dat u niet langer toouse Hallo oplossing verdere besluit, kunt u deze verwijderen uit Hallo Automation-account.  Hallo oplossing alleen verwijdert, gebeurt Hallo runbooks, zullen niet worden verwijderd Hallo planningen of variabelen die zijn gemaakt bij het Hallo-oplossing is toegevoegd.  Deze assets, moet u toodelete handmatig als u deze niet met andere runbooks gebruikt.  

toodelete oplossing hello, voert u Hallo stappen te volgen:

1.  Selecteer in uw automation-account Hallo **oplossingen** tegel.  
2.  Op Hallo **oplossingen** blade, selecteer Hallo oplossing **Start Stop VM [werkruimte]**.  Op Hallo **VMManagementSolution [werkruimte]** blade van menu klikt u op Hallo **verwijderen**.<br><br> ![Oplossing voor VM-Mgmt verwijderen](media/automation-solution-vm-management/vm-management-solution-delete.png)
3.  In Hallo **oplossing verwijderen** venster u toodelete Hallo oplossing wilt bevestigen.
4.  Tijdens het Hallo-informatie is geverifieerd en Hallo oplossing wordt verwijderd, u kunt de voortgang onder volgen **meldingen** in Hallo-menu.  Keert u terug toohello **VMManagementSolution [werkruimte]** blade nadat Hallo proces tooremove oplossing is gestart.  

Hallo Automation-account en OMS-werkruimte worden niet verwijderd als onderdeel van dit proces.  Als u niet dat tooretain Hallo OMS-werkruimte wilt, moet u toomanually verwijderen.  Dit kan ook worden bereikt vanaf hello Azure-portal.   Hallo-beginscherm in hello Azure-portal, selecteer **logboekanalyse** en klik vervolgens op Hallo **logboekanalyse** blade, selecteer Hallo werkruimte en klik op **verwijderen** in het menu op Hallo van Hallo werkruimte instellingenblade.  
      
## <a name="next-steps"></a>Volgende stappen

- Zie toolearn meer informatie over hoe tooconstruct verschillende zoekquery's en bekijk Hallo Automation logboeken met Log Analytics taak [zoekopdrachten aanmelden met Log Analytics](../log-analytics/log-analytics-log-searches.md)
- meer over de uitvoering van runbook, hoe toomonitor runbooktaken en andere technische details, Zie toolearn [een runbooktaak bijhouden](automation-runbook-execution.md)
- toolearn meer informatie over OMS Log Analytics en verzameling gegevensbronnen, Zie [verzamelen van Azure storage-gegevens in het overzicht van de Log Analytics](../log-analytics/log-analytics-azure-storage.md)






   

