---
title: aaaGraphical ontwerpen in Azure Automation | Microsoft Docs
description: Grafisch ontwerpen kunt u runbooks toocreate voor Azure Automation zonder het werken met code. Dit artikel bevat een inleiding toographical ontwerpen en alle details van Hallo toostart maken van een grafische runbook nodig.
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 4b6f840c-e941-4293-a728-b33407317943
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/14/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 6ddf18b992d5e5f7f4af95f344007a63ac498549
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="graphical-authoring-in-azure-automation"></a>Grafisch ontwerpen in Azure Automation
## <a name="introduction"></a>Inleiding
Grafisch ontwerpen kunt u runbooks toocreate voor Azure Automation zonder Hallo complexiteit van de onderliggende Windows PowerShell of PowerShell Workflow code Hallo. U voegt activiteiten toohello canvas vanuit een bibliotheek met de cmdlets en runbooks, ze aan elkaar koppelt en tooform een werkstroom configureren.  Als u ooit met System Center Orchestrator of Service Management Automation (SMA) hebt gewerkt, moet dit bekend tooyou eruitzien.   

Dit artikel bevat een inleiding toographical ontwerp en Hallo concepten, moet u tooget gestart bij het maken van een grafisch runbook.

## <a name="graphical-runbooks"></a>Grafische runbooks
Alle runbooks in Azure Automation zijn Windows PowerShell-werkstromen.  Grafisch en grafische PowerShell Workflow-runbooks PowerShell-code die wordt uitgevoerd door Hallo Automation werknemers genereren, maar u bent geen kunnen tooview het of rechtstreeks worden gewijzigd.  Een grafisch runbook kan worden geconverteerd tooa grafische PowerShell Workflow-runbook en vice versa, maar ze niet worden geconverteerd tooa tekstueel runbook. Een bestaande tekstueel runbook kan niet worden geïmporteerd in de grafische editor Hallo.  

## <a name="overview-of-graphical-editor"></a>Overzicht van de grafische editor
U kunt de grafische editor Hallo in hello Azure-portal openen door maken of bewerken van een grafisch runbook.

![Grafische werkruimte](media/automation-graphical-authoring-intro/runbook-graphical-editor.png)

Hallo beschrijven volgende secties Hallo besturingselementen in de grafische editor Hallo.

### <a name="canvas"></a>Canvas
Hallo Canvas is waar u uw runbook te ontwerpen.  U voegt activiteiten uit Hallo-knooppunten in het Hallo-bibliotheek besturingselement toohello runbook en verbind ze met koppelingen toodefine Hallo logica van Hallo runbook.

U kunt in en uit Hallo besturingselementen Hallo Hallo canvas toozoom onderaan in.

![Grafische werkruimte](media/automation-graphical-authoring-intro/runbook-canvas-controls.png)

### <a name="library-control"></a>Besturingselement bibliotheek
Hallo besturingselement bibliotheek is waar u [activiteiten](#activities) tooadd tooyour runbook.  U toevoegen ze toohello canvas waar u ze tooother activiteiten verbindt.  Dit omvat vier secties wordt beschreven in de volgende tabel Hallo.

| Sectie | Beschrijving |
|:--- |:--- |
| Cmdlets |Bevat alle Hallo-cmdlets die kunnen worden gebruikt in uw runbook.  Cmdlets zijn ingedeeld in de module.  Alle Hallo-modules die u hebt geïnstalleerd in uw automation-account zijn beschikbaar. |
| Runbooks |Bevat Hallo runbooks in uw automation-account. Deze runbooks kunnen toohello canvas toobe gebruikt als onderliggende runbooks worden toegevoegd. Alleen runbooks van hetzelfde type core als het runbook wordt bewerkt Hallo Hallo worden weergegeven; Grafische worden runbooks alleen op basis van PowerShell-runbooks weergegeven, terwijl voor grafische PowerShell Workflow-runbooks alleen PowerShell-werkstroom runbooks worden weergegeven. |
| Assets |Hallo omvat [automation activa](http://msdn.microsoft.com/library/dn939988.aspx) in uw automation-account die kan worden gebruikt in uw runbook.  Wanneer u een asset tooa runbook toevoegt, voegt deze toe een workflow-activiteit die de geselecteerde asset Hallo opgehaald.  In geval van variabele assets Hallo kunt u selecteren of een activiteit tooget tooadd Hallo variabele of stel Hallo-variabele. |
| Runbookbesturing |Bevat besturingselement runbookactiviteiten die kunnen worden gebruikt in uw huidige runbook. Een *koppelingspunten* neemt meerdere invoer en wacht totdat alle hebben voltooid voordat de bewerking wordt voortgezet Hallo-werkstroom. Een *Code* activiteit wordt uitgevoerd voor een of meer coderegels PowerShell of PowerShell Workflow, afhankelijk van Hallo grafisch runbooktype.  U kunt deze activiteit kunt gebruiken voor aangepaste code of voor functionaliteit die is moeilijk tooachieve met andere activiteiten. |

### <a name="configuration-control"></a>Configuratiecontrole
Hallo Configuratiebeheer is waarin u details opgeven voor een object dat is geselecteerd op Hallo canvas. Hallo-eigenschappen die beschikbaar zijn in dit besturingselement is afhankelijk van het soort object geselecteerd Hallo.  Wanneer u een optie in Hallo configuratiecontrole selecteert, wordt deze extra blades geopend in de volgorde tooprovide aanvullende informatie.

### <a name="test-control"></a>Besturingselement testen
Hallo Test besturingselement wordt niet weergegeven wanneer de grafische editor Hallo voor het eerst wordt gestart. Dit bestand is geopend wanneer u interactief [grafisch runbook testen](#graphical-runbook-procedures).  

## <a name="graphical-runbook-procedures"></a>Grafisch runbook procedures
### <a name="exporting-and-importing-a-graphical-runbook"></a>Exporteren en importeren van een grafisch runbook
U kunt alleen gepubliceerde versie van een grafische runbook Hallo exporteren.  Als het Hallo-runbook is nog niet gepubliceerd, Hallo **Export gepubliceerd** knop wordt uitgeschakeld.  Wanneer u klikt op Hallo **Export gepubliceerd** knop, hello runbook is gedownloade tooyour lokale computer.  Hallo-naam van Hallo bestand overeenkomt met de naam van de Hallo van Hallo runbook met een *graphrunbook* extensie.

![Gepubliceerde exporteren](media/automation-graphical-authoring-intro/runbook-export.png)

U kunt een grafisch of grafische PowerShell Workflow-runbook-bestand importeren door het selecteren van Hallo **importeren** optie bij het toevoegen van een runbook.   Wanneer u Hallo bestand tooimport selecteert, kunt u dezelfde Hallo **naam** of geef een nieuwe.  Hallo Runbooktype veld worden Hallo type runbook weergegeven nadat het Hallo-bestand geselecteerd en als u een ander type dan is niet juist is probeert, dat wordt een bericht worden gepresenteerd Let er mogelijke conflicten en tijdens de conversie, kan er tooselect evalueert syntaxisfouten.  

![Runbook importeren](media/automation-graphical-authoring-intro/runbook-import-revised20165.png)

### <a name="testing-a-graphical-runbook"></a>Een grafisch runbook testen
Tijdens het Hallo verlaten gepubliceerde versie van Hallo runbook ongewijzigd of kunt u een nieuw runbook testen voordat deze is gepubliceerd, kunt u de Hallo conceptversie van een runbook testen in hello Azure-portal. Hiermee kunt u tooverify die Hallo runbook correct werkt voordat Hallo gepubliceerde versie vervangen. Wanneer u een runbook test, Hallo conceptrunbook wordt uitgevoerd en acties die worden uitgevoerd, zijn voltooid. Er wordt geen Taakgeschiedenis gemaakt, maar uitvoer wordt weergegeven in het deelvenster Testuitvoer Hallo. 

Hallo Test-besturingselement voor een runbook te openen door te openen Hallo runbook om te bewerken en klik vervolgens op Hallo **testvenster** knop.

![Deelvenster-knop testen](media/automation-graphical-authoring-intro/runbook-edit-test-pane.png)

Hallo Test besturingselement wordt gevraagd voor alle parameters voor invoer en u Hallo runbook start door te klikken op Hallo **Start** knop.

![Test knoppen](media/automation-graphical-authoring-intro/runbook-test-start.png)

### <a name="publishing-a-graphical-runbook"></a>Een grafisch runbook publiceren
Elk runbook in Azure Automation heeft een ontwerpversie en een gepubliceerde versie. Alleen Hallo gepubliceerde versie is beschikbaar toobe uitvoeren en alleen de conceptversie Hallo kan worden bewerkt. Hallo gepubliceerde versie wordt niet beïnvloed door de conceptversie van eventuele wijzigingen toohello. Wanneer de conceptversie Hallo gereed toobe beschikbaar is, publiceert u deze die Hallo gepubliceerde versie met de conceptversie Hallo overschrijft.

U kunt een grafisch runbook publiceren door het openen van de runbook om te bewerken en vervolgens te klikken op Hallo Hallo **publiceren** knop.

![De knop Publiceren](media/automation-graphical-authoring-intro/runbook-edit-publish.png)

Wanneer een runbook is nog niet gepubliceerd, heeft een status van **nieuw**.  Wanneer het wordt gepubliceerd, heeft deze een status **gepubliceerde**.  Als u Hallo runbook bewerkt nadat deze is gepubliceerd en Hallo conceptversie en een gepubliceerde versies verschillend zijn, Hallo runbook heeft de status van **In bewerken**.

![Runbook-status](media/automation-graphical-authoring-intro/runbook-statuses-revised20165.png) 

U hebt ook Hallo optie toorevert toohello gepubliceerde versie van een runbook.  Hiermee verwijdert u alle wijzigingen sinds Hallo runbook het laatst is gepubliceerd en de conceptversie Hallo van Hallo runbook door Hallo gepubliceerde versie vervangt.

![Toopublished knop herstellen](media/automation-graphical-authoring-intro/runbook-edit-revert-published.png)

## <a name="activities"></a>Activiteiten
Activiteiten zijn Hallo bouwstenen van een runbook.  Een activiteit kan dit een PowerShell-cmdlet, een onderliggend runbook of een workflow-activiteit.  U een activiteit toohello runbook toevoegen door met de rechtermuisknop te klikken op het in het besturingselement bibliotheek Hallo en **toocanvas toevoegen**.  U kunt Klik en sleep Hallo activiteit tooplace overal op Hallo canvas dat u de configuratie.  Hallo heeft locatie Hallo Hallo-activiteit op Hallo canvas geen invloed op Hallo-bewerking van de runbook Hallo op elke manier.  U kunt lay-out uw runbook echter u het meest geschikte toovisualize vindt werking ervan. 

![Toocanvas toevoegen](media/automation-graphical-authoring-intro/add-to-canvas-revised20165.png)

Selecteer de eigenschappen en parameters Hallo activiteit op Hallo canvas tooconfigure Hallo configuratie blade.  U kunt wijzigen Hallo **Label** van Hallo activiteit toosomething die beschrijvende tooyou.  Hallo oorspronkelijke cmdlet nog steeds wordt uitgevoerd, u gewoon de weergavenaam die wordt gebruikt in de grafische editor Hallo wijzigt.  Hallo-label moet uniek zijn binnen Hallo runbook. 

### <a name="parameter-sets"></a>Parametersets
Een parameterset definieert Hallo verplichte en optionele parameters die waarden voor een bepaalde cmdlet accepteert.  Alle cmdlets hebben ten minste één parameter is ingesteld en sommige meerdere hebben.  Als een cmdlet meerdere parametersets bevat, moet vervolgens u selecteren welke methode u gebruiken wilt voordat u parameters kunt configureren.  Hallo-parameters die u kunt configureren, is afhankelijk van Hallo parameterset die u kiest.  Hallo parameterset gebruikt door een activiteit door te selecteren kunt u **parameterset** en het selecteren van een andere set.  In dit geval de parameterwaarden die u hebt geconfigureerd gaan verloren.

In Hallo voorbeeld te volgen, heeft de cmdlet Get-AzureRmVM Hallo drie parametersets.  U kunt parameterwaarden niet configureren, totdat u een van de parametersets Hallo selecteren.  Hallo parameterset ListVirtualMachineInResourceGroupParamSet is voor het retourneren van alle virtuele machines in een resourcegroep en een enkele optionele parameter.  Hallo GetVirtualMachineInResourceGroupParamSet is voor het opgeven van Hallo virtuele machine gewenste tooreturn en heeft twee verplicht en een optionele parameter.

![Parameterset](media/automation-graphical-authoring-intro/get-azurermvm-parameter-sets.png)

#### <a name="parameter-values"></a>Parameterwaarden
Als u een waarde voor een parameter opgeven, selecteert u een data source toodetermine hoe de Hallo waarde worden opgegeven.  Hallo-gegevensbronnen die beschikbaar voor een bepaalde parameter zijn afhankelijk Hallo geldige waarden voor deze parameter.  Null worden bijvoorbeeld niet een beschikbare optie voor een parameter die null-waarden zijn niet toegestaan.

| Gegevensbron | Beschrijving |
|:--- |:--- |
| Constante waarde |Typ een waarde voor parameter Hallo.  Dit is alleen beschikbaar voor de volgende gegevenstypen Hallo: Int32, Int64, String, Boolean, DateTime, Switch. |
| Uitvoer van activiteit |De uitvoer van een activiteit die voorafgaat aan de huidige activiteit Hallo in Hallo-werkstroom.  Kan alle geldige activiteiten wordt weergegeven.  Selecteer alleen Hallo activiteit toouse de uitvoer voor Hallo parameterwaarde.  Als Hallo activiteit een object met meerdere eigenschappen levert, kunt u opgeven in Hallo-naam van de eigenschap Hallo na het selecteren van Hallo-activiteit. |
| Runbookinvoer |Selecteer een runbookinvoerparameter als invoer toohello activiteitsparameter. |
| Variabelenactivum |Selecteer een Automation-variabele als invoer. |
| Referentie-element |Selecteer een Automation-referentie als invoer. |
| Certificaatasset |Selecteer een Automation-certificaat als invoer. |
| Verbindingstype-Asset |Selecteer een Automation-verbinding als invoer. |
| PowerShell-expressie |Geef een eenvoudige [PowerShell-expressie](#powershell-expressions).  Hallo-expressie wordt geëvalueerd voordat Hallo-activiteit en Hallo resultaat gebruikt voor het Hallo-parameterwaarde.  U kunt variabelen toorefer toohello uitvoer van een activiteit of een runbook-invoerparameter. |
| Niet geconfigureerd |Hiermee wist u elke waarde die eerder was geconfigureerd. |

#### <a name="optional-additional-parameters"></a>Optionele extra parameters
Alle cmdlets hebben Hallo optie tooprovide extra parameters.  Dit zijn algemene PowerShell-parameters of andere aangepaste parameters.  Krijgt u een tekstvak waarin u de parameters in met behulp van PowerShell-syntaxis kunt opgeven.  Bijvoorbeeld: toouse hello **uitgebreid** algemene parameter geeft u **'-Verbose: $True '**.

### <a name="retry-activity"></a>Probeer de activiteit
**Opnieuw proberen** kunt een activiteit toobe meerdere keren uitvoeren totdat een bepaalde voorwaarde wordt voldaan, net als een lus.  U kunt deze functie gebruiken voor activiteiten die foutgevoelig meerdere keren moet uitvoeren, zijn en kan moet meer dan één proberen voor een correcte werking of testen Hallo uitvoergegevens van de activiteit Hallo voor geldige gegevens.    

Wanneer u opnieuw proberen voor een activiteit inschakelt, kunt u een vertraging optreden en een voorwaarde instellen.  Hallo vertraging is het Hallo-tijd (gemeten in seconden of minuten) dat Hallo runbook wacht voordat het Hallo-activiteit opnieuw wordt uitgevoerd.  Als er geen vertraging is opgegeven, klikt u vervolgens Hallo activiteit wordt uitgevoerd opnieuw onmiddellijk nadat deze is voltooid. 

![Activiteit-tijd tussen elke poging](media/automation-graphical-authoring-intro/retry-delay.png)

Hallo opnieuw voorwaarde is een PowerShell-expressie die wordt geëvalueerd nadat elke keer Hallo-activiteit is uitgevoerd.  Als de expressie Hallo tooTrue is opgelost, klikt u vervolgens Hallo activiteit opnieuw uitgevoerd.  Hallo-expressie wordt omgezet tooFalse vervolgens hello activiteit niet opnieuw wordt uitgevoerd als Hallo runbook verplaatst op de volgende activiteit toohello. 

![Activiteit-tijd tussen elke poging](media/automation-graphical-authoring-intro/retry-condition.png)

Hallo opnieuw voorwaarde kunt een variabele met de naam $RetryData waarmee toegang tooinformation over Hallo activiteit pogingen gebruiken.  Deze variabele heeft Hallo eigenschappen in de volgende tabel Hallo.

| Eigenschap | Beschrijving |
|:--- |:--- |
| NumberOfAttempts |Het aantal keren dat Hallo-activiteit is uitgevoerd. |
| Uitvoer |De uitvoer van Hallo laatste uitvoering van Hallo-activiteit. |
| TotalDuration |Time-out verstreken sinds Hallo-activiteit is gestart Hallo eerst. |
| StartedAt |Tijd in UTC-notatie Hallo activiteit voor het eerst is gestart. |

Hieronder vindt u voorbeelden van de activiteit van de nieuwe poging voorwaarden.

    # Run hello activity exactly 10 times.
    $RetryData.NumberOfAttempts -ge 10 

    # Run hello activity repeatedly until it produces any output.
    $RetryData.Output.Count -ge 1 

    # Run hello activity repeatedly until 2 minutes has elapsed. 
    $RetryData.TotalDuration.TotalMinutes -ge 2

Nadat u een nieuwe poging voorwaarde voor een activiteit configureren, Hallo activiteit bevat twee visuele aanwijzingen tooremind u.  Een is opgenomen in het Hallo-activiteit en andere Hallo is wanneer u hello configuratie van Hallo-activiteit bekijkt.

![Activiteit opnieuw Visual indicatoren](media/automation-graphical-authoring-intro/runbook-activity-retry-visual-cue.png)

### <a name="workflow-script-control"></a>Script werkstroombeheer
Een Code-besturingselement is een speciale activiteit accepteert PowerShell of PowerShell Workflow-script, afhankelijk van Hallo type grafisch runbook wordt geschreven in de volgorde tooprovide functionaliteit die anders mogelijk niet beschikbaar.  Er kan geen parameters accepteren, maar het kan variabelen gebruiken voor activiteit uitvoer en runbook-invoerparameters.  Uitvoer van activiteit Hallo wordt toegevoegd aan de gegevensbus toohello tenzij er geen uitgaande koppeling in dat geval deze is toegevoegd toohello uitvoer van Hallo runbook.

Bijvoorbeeld hello volgende code wordt uitgevoerd met behulp van een runbook invoer variabele met de naam $NumberOfDays datumberekeningen.  Vervolgens stuurt een berekende datum-tijd als uitvoer toobe die wordt gebruikt door de volgende activiteiten in Hallo runbook.

    $DateTimeNow = (Get-Date).ToUniversalTime()
    $DateTimeStart = ($DateTimeNow).AddDays(-$NumberOfDays)}
    $DateTimeStart


## <a name="links-and-workflow"></a>Werkstroom en koppelingen
Een **koppeling** verbindt twee activiteiten in een grafisch runbook.  Als een pijl vanuit Hallo activiteit toohello bestemming bronactiviteit wordt deze weergegeven op Hallo canvas.  Hallo activiteiten uitgevoerd in de richting van Hallo pijl Hallo met Hallo doelactiviteit na Hallo bronactiviteit wordt gestart.  

### <a name="create-a-link"></a>Een koppeling maken
Maak een koppeling tussen twee activiteiten door de activiteit van de bron te selecteren Hallo en te klikken op Hallo cirkel onderin Hallo van Hallo vorm.  Sleep Hallo pijl toohello doelactiviteit en release.

![Een koppeling maken](media/automation-graphical-authoring-intro/create-link-revised20165.png)

Selecteer Hallo koppeling tooconfigure eigenschappen Hallo configuratie blade.  Hallo koppelingstype die wordt beschreven horen in de volgende tabel Hallo.

| Koppelingstype | Beschrijving |
|:--- |:--- |
| Pijplijn |Hallo doelactiviteit wordt eenmaal uitvoeren voor elk objectuitvoer vanuit de bronactiviteit Hallo.  Hallo doelactiviteit wordt niet uitgevoerd als de bronactiviteit Hallo in het geen uitvoer resulteert.  De uitvoer van de bronactiviteit Hallo is beschikbaar als een object. |
| Reeks |Hallo doelactiviteit wordt slechts één keer uitgevoerd.  Deze ontvangt matrix met objecten vanuit de bronactiviteit Hallo.  Uitvoer van de bronactiviteit Hallo is beschikbaar als een matrix met objecten. |

### <a name="starting-activity"></a>Starten van de activiteit
Een grafisch runbook start met activiteiten die geen van de koppeling van een binnenkomende.  Dit is vaak slechts één activiteit die moet fungeren als Hallo activiteit voor Hallo runbook wordt gestart.  Als meerdere activiteiten een binnenkomende koppeling niet hebt, start Hallo runbook door ze parallel worden uitgevoerd.  Deze wordt vervolgens volg Hallo koppelingen toorun andere activiteiten elk is voltooid.

### <a name="conditions"></a>Voorwaarden
Wanneer u een voorwaarde op een koppeling opgeeft, wordt de doelactiviteit Hallo alleen uitgevoerd als Hallo voorwaarde tootrue wordt omgezet.  Gewoonlijk gebruikt u een variabele $ActivityOutput in een voorwaarde tooretrieve Hallo uitvoer vanuit de bronactiviteit Hallo.  

U een voorwaarde voor een enkel object opgeven voor een pipeline-koppeling, en Hallo voorwaarde wordt geëvalueerd voor elke objectuitvoer door Hallo bronactiviteit.  Hallo doelactiviteit wordt vervolgens voor elk object dat voldoet aan de voorwaarde hello uitgevoerd.  Bijvoorbeeld met een bronactiviteit van Get-AzureRmVm, Hallo syntaxis kan alleen worden gebruikt voor een pijplijn voorwaardelijke koppeling tooretrieve virtuele machines in de resourcegroep met de naam Hallo *Group1*.  

    $ActivityOutput['Get Azure VMs'].Name -match "Group1"

Voor de koppeling van een reeks wordt Hallo voorwaarde alleen geëvalueerd eenmaal omdat een matrix met alle objecten uitvoer van de bronactiviteit hello wordt geretourneerd.  Als gevolg hiervan is een reeks koppeling kan niet worden gebruikt voor het filteren van zoals een pipeline-koppeling, maar gewoon wordt bepaald of de volgende activiteit hello wordt uitgevoerd. Neem bijvoorbeeld Hallo volgende set van activiteiten in ons runbook VM Start.<br> ![Voorwaardelijke koppeling met reeksen](media/automation-graphical-authoring-intro/runbook-conditional-links-sequence.png)<br>
Er zijn drie verschillende reeks koppelingen die waarden zijn opgegeven tootwo runbook invoerparameters voor VM-naam en de naam van de resourcegroep in volgorde toodetermine die Hallo gepaste actie tootake - beginnen één VM wilt controleren, alle virtuele machines starten in Hallo bron-groep of alle virtuele machines in een abonnement.  Hier volgt Hallo voorwaarde logica voor Hallo sequence koppeling tussen Connect tooAzure en één Get-VM:

    <# 
    Both VMName and ResourceGroupName runbook input parameters have values 
    #>
    (
    (($VMName -ne $null) -and ($VMName.Length -gt 0))
    ) -and (
    (($ResourceGroupName -ne $null) -and ($ResourceGroupName.Length -gt 0))
    )

Wanneer u een voorwaardelijke koppeling gebruikt, worden beschikbaar is via Hallo bron activiteit tooother activiteiten in dat filiaal Hallo-gegevens gefilterd door Hallo voorwaarde.  Als een activiteit Hallo bron toomultiple koppelingen, Hallo vervolgens gegevens beschikbaar tooactivities in elke vertakking hangen af van Hallo voorwaarde in Hallo koppeling toothat vertakking verbinding te maken.

Bijvoorbeeld, Hallo **Start-AzureRmVm** activiteit in onderstaande Hallo-runbook Start alle virtuele machines.  Heeft twee voorwaardelijke koppelingen.  eerste voorwaardelijke koppeling Hallo Hallo-expressie gebruikt *$ActivityOutput ['Start-AzureRmVM']. IsSuccessStatusCode - eq $true* toofilter als Hallo Start-AzureRmVm activiteit is voltooid.  Hallo wordt tweede Hallo expressie *$ActivityOutput ['Start-AzureRmVM']. IsSuccessStatusCode - ne $true* toofilter als Hallo Start-AzureRmVm activiteit toostart Hallo virtuele machine is mislukt.  

![Voorbeeld van een voorwaardelijke koppeling](media/automation-graphical-authoring-intro/runbook-conditional-links.png)

Elke activiteit die volgt op de eerste koppeling Hallo en maakt gebruik van Hallo activiteit uitvoer van Get-AzureVM krijgt alleen Hallo virtuele machines die zijn gestart op Hallo moment die Get-AzureVM is uitgevoerd.  Elke activiteit die volgt op de tweede koppeling Hallo krijgt alleen Hallo Hallo virtuele machines die zijn gestopt tijdens het Hallo die Get-AzureVM is uitgevoerd.  Elke activiteit Hallo derde koppeling krijgen alle virtuele machines ongeacht hun actief is.

### <a name="junctions"></a>Koppelingen
Een verbinding is een speciale activiteit wacht totdat alle binnenkomende takken hebt voltooid.  Hiermee kunt u toorun meerdere activiteiten parallel en zorg ervoor dat alle hebt voltooid voordat u doorgaat.

Hoewel een verbinding een onbeperkt aantal inkomende koppelingen hebben kan, zijn niet meer dan één van deze koppelingen een pijplijn.  het aantal inkomende sequence koppelingen Hallo wordt niet beperkt.  U mag toocreate Hallo verbinding met meerdere inkomende pijplijn koppelingen en Hallo runbook opslaan, maar zal mislukken wanneer deze wordt uitgevoerd.

Hallo in het volgende voorbeeld is onderdeel van een runbook dat wordt gestart van een set van virtuele machines terwijl toothose machines tegelijk downloaden toobe patches worden toegepast.  Is een verbinding gebruikte tooensure dat beide processen zijn voltooid voordat Hallo runbook wordt hervat.

![De verbinding](media/automation-graphical-authoring-intro/runbook-junction.png)

### <a name="cycles"></a>Cycli
Een cyclus is wanneer een doelactiviteit terug koppelingen tooits bron activiteit of tooanother activiteit dat uiteindelijk teruggekoppeld tooits bron.  Cycli worden momenteel niet toegestaan in het grafisch ontwerpen.  Als uw runbook een cyclus is, correct worden opgeslagen, maar wordt er een foutbericht wanneer deze wordt uitgevoerd.

![Cyclus](media/automation-graphical-authoring-intro/runbook-cycle.png)

### <a name="sharing-data-between-activities"></a>Delen van gegevens tussen activiteiten
Alle gegevens die wordt uitgevoerd door een activiteit met de koppeling van een uitgaande geschreven toohello *gegevensbus* voor Hallo runbook.  Elke activiteit in Hallo runbook kunt gebruiken van gegevens op Hallo gegevensbus toopopulate parameterwaarden of opnemen in een script.  Een activiteit hebben toegang tot Hallo-uitvoer van een vorige activiteit in Hallo-werkstroom.     

Hoe Hallo gegevens toohello gegevensbus worden geschreven, is afhankelijk van Hallo type koppeling op Hallo-activiteit.  Voor een **pijplijn**, Hallo gegevens wordt weergegeven als veelvouden objecten.  Voor een **reeks** koppelen, hello gegevens wordt uitgevoerd als een matrix.  Als er slechts één waarde, zal de uitvoer zijn als een matrix met één element.

U kunt toegang tot gegevens op Hallo gegevensbus met een van twee methoden.  Eerst wordt met behulp van een **uitvoer van activiteit** toopopulate van gegevensbron een parameter van een andere activiteit.  Als het Hallo-uitvoer is een object, kunt u één eigenschap opgeven.

![Uitvoer van activiteit](media/automation-graphical-authoring-intro/activity-output-datasource-revised20165.png)

U kunt ook ophalen Hallo-uitvoer van een activiteit in een **PowerShell-expressie** gegevensbron of vanuit een **Werkstroomscript** activiteit met een variabele ActivityOutput.  Als het Hallo-uitvoer is een object, kunt u één eigenschap opgeven.  Variabelen ActivityOutput Hallo syntaxis gebruiken.

    $ActivityOutput['Activity Label']
    $ActivityOutput['Activity Label'].PropertyName 

### <a name="checkpoints"></a>Controlepunten
U kunt instellen [controlepunten](automation-powershell-workflow.md#checkpoints) in een grafische PowerShell Workflow-runbook door te selecteren *controlepunt runbook* op elke activiteit.  Dit zorgt ervoor dat een controlepunt toobe niet instellen nadat het Hallo-activiteit wordt uitgevoerd.

![Controlepunt](media/automation-graphical-authoring-intro/set-checkpoint.png)

Controlepunten is alleen ingeschakeld in de grafische PowerShell Workflow-runbooks, is niet beschikbaar in de grafische runbooks.  Als het runbook hello Azure-cmdlets gebruikt, moet u elke activiteit controlepunt met een Add-AzureRMAccount volgen geval Hallo runbook wordt onderbroken en opnieuw wordt opgestart vanaf dit controlepunt op een andere werknemer. 

## <a name="authenticating-tooazure-resources"></a>Verificatie van tooAzure resources
Runbooks in Azure Automation die Azure-resources te beheren, moet verificatie tooAzure.  Hallo [Run As-account](automation-offering-get-started.md#creating-an-automation-account) (ook waarnaar wordt verwezen tooas van een service-principal) is Hallo standaard methode tooaccess Azure Resource Manager-resources in uw abonnement met Automation-runbooks.  U kunt deze functionaliteit tooa grafisch runbook toevoegen door toe te voegen Hallo **AzureRunAsConnection** verbindingsasset die van Hallo PowerShell gebruikmaakt [Get-AutomationConnection](https://technet.microsoft.com/library/dn919922%28v=sc.16%29.aspx) -cmdlet en [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet toohello canvas. Dit wordt geïllustreerd in Hallo voorbeeld te volgen.<br>![Als verificatie activiteiten uitvoeren](media/automation-graphical-authoring-intro/authenticate-run-as-account.png)<br>
Hallo uitvoeren als-verbinding ophalen activiteit (dat wil zeggen Get-AutomationConnection) is geconfigureerd met een constante waarde gegevensbron met de naam AzureRunAsConnection.<br>![Run As-configuratie-verbinding](media/automation-graphical-authoring-intro/authenticate-runas-parameterset.png)<br>
de volgende activiteit Hello, telt Add-AzureRmAccount Hallo geverifieerde Run As-account voor gebruik in Hallo runbook.<br>
![Parameterset Add-AzureRmAccount](media/automation-graphical-authoring-intro/authenticate-conn-to-azure-parameter-set.png)<br>
Voor Hallo parameters **APPLICATIONID**, **CERTIFICATETHUMBPRINT**, en **TENANTID** moet u toospecify Hallo-naam van Hallo-eigenschap voor het pad naar het veld van Hallo omdat Hallo activiteit levert een object met meerdere eigenschappen.  Wanneer u Hallo runbook uitvoeren, mislukt het anders tijdens tooauthenticate.  Dit is wat u nodig hebt op een minimale tooauthenticate uw runbook Hello Run As-account.

toomaintain achterwaartse compatibiliteit voor abonnees die u hebt gemaakt een Automation-account met een [Azure AD-gebruikersaccount](automation-create-aduser-account.md) toomanage klassieke Azure-implementatie of Hallo methode tooauthenticate voor Azure Resource Manager-resources. de cmdlet Add-AzureAccount Hallo met is een [referentieasset](automation-credentials.md) die staat voor een Active Directory-gebruiker met toegang toohello Azure-account.

U kunt deze functionaliteit tooa grafisch runbook toevoegen door een referentie-asset toohello canvas, gevolgd door een Add-AzureAccount activiteit toe te voegen.  Hallo referentie activiteit-AzureAccount gebruikt voor de invoer.  Dit wordt geïllustreerd in Hallo voorbeeld te volgen.

![Verificatie-activiteiten](media/automation-graphical-authoring-intro/authentication-activities.png)

U hebt tooauthenticate aan begin Hallo van Hallo runbook en na elke controlepunt.  Dit betekent dat met het toevoegen van een activiteit toevoeging Add-AzureAccount na elke activiteit controlepunt-werkstroom. U hoeft niet een referentie voor de toevoeging activiteit sinds kunt u dezelfde Hallo 

![Uitvoer van activiteit](media/automation-graphical-authoring-intro/authentication-activity-output.png)

## <a name="runbook-input-and-output"></a>Runbook invoer en uitvoer
### <a name="runbook-input"></a>Runbookinvoer
Een runbook moet mogelijk invoer van een gebruiker wanneer ze Hallo runbook via hello Azure-portal of vanuit een ander runbook start als Hallo huidige wordt gebruikt als een onderliggend element.
Bijvoorbeeld als u een runbook dat een virtuele machine maakt hebt, moet u mogelijk tooprovide informatie zoals de naam van de Hallo van Hallo virtuele machine en andere eigenschappen telkens wanneer die u Hallo runbook start.  

U accepteert invoer voor een runbook door te definiëren een of meer parameters voor invoer.  U kunt waarden opgeven voor deze parameters die elke keer Hallo runbook wordt gestart.  Wanneer u een runbook met hello Azure-portal start, wordt u tooprovide waarden voor Hallo van invoerparameters van runbook Hallo gevraagd.

U toegang hebt tot invoerparameters voor een runbook door te klikken op Hallo **invoer en uitvoer** op de werkbalk van Hallo runbook.  

![Runbookinvoer uitvoer](media/automation-graphical-authoring-intro/runbook-edit-input-output.png) 

Hiermee opent u Hallo **invoer en uitvoer** besturingselement kunt u een bestaande invoerparameter bewerken of een nieuwe maken door te klikken op **invoer toevoegen**. 

![Invoer toevoegen](media/automation-graphical-authoring-intro/runbook-edit-add-input.png)

Elke invoerparameter wordt gedefinieerd door de eigenschappen in de volgende tabel Hallo Hallo.

| Eigenschap | Beschrijving |
|:--- |:--- |
| Naam |Hallo unieke naam van de Hallo-parameter.  Dit mag alleen alfanumerieke tekens bevatten en mogen geen. |
| Beschrijving |Een optionele beschrijving voor de invoerparameter Hallo. |
| Type |Gegevenstype voor de parameterwaarde Hallo verwacht.  Hello Azure-portal biedt een juiste besturingselement voor Hallo gegevenstype voor elke parameter bij vragen om invoer. |
| Verplicht |Hiermee geeft u op of een waarde voor parameter Hallo moet worden opgegeven.  Hallo-runbook kan niet worden gestart als u een waarde niet opgeeft voor elke verplichte parameter waarmee geen standaardwaarde gedefinieerd heeft. |
| Standaardwaarde |Hiermee geeft u op welke waarde wordt gebruikt voor de parameter Hallo als deze niet is opgegeven.  Dit kan ofwel Null of een specifieke waarde zijn. |

### <a name="runbook-output"></a>Runbook-uitvoer
Gegevens die zijn gemaakt door elke activiteit die geen een uitgaande koppeling wordt toegevoegd toohello [uitvoer van runbook hello](http://msdn.microsoft.com/library/azure/dn879148.aspx).  Hallo uitvoer wordt opgeslagen met de runbooktaak hello en is beschikbaar tooa bovenliggend runbook wanneer Hallo runbook wordt gebruikt als een onderliggend element.  

## <a name="powershell-expressions"></a>PowerShell-expressies
Een van de voordelen van het grafisch ontwerpen Hallo levert u met de Hallo mogelijkheid toobuild een runbook met minimale kennis van PowerShell.  Op dit moment hoeft u een PowerShell-bit tooknow al voor het invullen van bepaalde [parameterwaarden](#activities) en voor de instelling [koppelen voorwaarden](#links-and-workflow).  Deze sectie bevat een korte inleiding tooPowerShell expressies voor gebruikers die mogelijk niet bekend bent met het.  Volledige details van PowerShell zijn beschikbaar op [met Windows PowerShell-scripts](http://technet.microsoft.com/library/bb978526.aspx). 

### <a name="powershell-expression-data-source"></a>Gegevensbron voor PowerShell-expressie
U kunt een PowerShell-expressie gebruiken als bron toopopulate Hallo waarde is ingesteld op een [activiteitsparameter](#activities) met Hallo resultaten van sommige PowerShell-code.  Dit kan bijvoorbeeld één regel code die enkele eenvoudige functie of meerdere regels die bepaalde complexe logica uitvoeren wordt uitgevoerd.  Elke uitvoer van een opdracht die is niet toegewezen tooa variabele parameterwaarde van uitvoer toohello is. 

Bijvoorbeeld, zou Hallo na de opdracht uitvoeren Hallo huidige datum. 

    Get-Date

Hallo volgende opdrachten opbouwen van een tekenreeks van Hallo huidige datum en wijs deze tooa variabele.  Hallo-inhoud van Hallo variabele worden vervolgens toohello uitvoer verzonden. 

    $string = "hello current date is " + (Get-Date)
    $string

Hallo volgende opdrachten evalueren Hallo huidige datum en -tekenreeks geretourneerd die aangeeft of Hallo vandaag een weekend of weekdag. 

    $date = Get-Date
    if (($date.DayOfWeek = "Saturday") -or ($date.DayOfWeek = "Sunday")) { "Weekend" }
    else { "Weekday" }


### <a name="activity-output"></a>Uitvoer van activiteit
toouse hello uitvoer van een vorige activiteit in Hallo runbook, gebruik Hallo $ActivityOutput variabele met de volgende syntaxis Hallo.

    $ActivityOutput['Activity Label'].PropertyName

Bijvoorbeeld wellicht hebt u een activiteit met een eigenschap waarvoor Hallo-naam van een virtuele machine in dat geval kunt u Hallo expressie te volgen.

    $ActivityOutput['Get-AzureVm'].Name

Als het Hallo-eigenschap die Hallo virtuele-machineobject in plaats van alleen een eigenschap, dan hebt u nodig zou retourneren Hallo gehele object met behulp van Hallo syntaxis.

    $ActivityOutput['Get-AzureVm']

U kunt ook Hallo-uitvoer van een activiteit in een complexe expressie zoals Hallo volgende waarmee de naam van de virtuele machine toohello tekst worden aaneengeschakeld.

    "hello computer name is " + $ActivityOutput['Get-AzureVm'].Name


### <a name="conditions"></a>Voorwaarden
Gebruik [vergelijkingsoperators](https://technet.microsoft.com/library/hh847759.aspx) toocompare waarden of kunt vaststellen of een waarde overeenkomt met een opgegeven patroon.  Een vergelijking retourneert een waarde van $true en $false.

Bijvoorbeeld, Hallo na voorwaarde bepaalt of er Hallo virtuele machine van een activiteit met de naam *Get-AzureVM* is momenteel *gestopt*. 

    $ActivityOutput["Get-AzureVM"].PowerState –eq "Stopped"

Hallo volgende voorwaarde controles of hello dezelfde virtuele machine bevindt zich in een staat andere dan *gestopt*.

    $ActivityOutput["Get-AzureVM"].PowerState –ne "Stopped"

U kunt deelnemen aan meerdere voorwaarden met behulp van een [logische operator](https://technet.microsoft.com/library/hh847789.aspx) zoals **- en** of **- of**.  Bijvoorbeeld, Hallo volgende controles voorwaarde of Hallo dezelfde virtuele machine in het vorige voorbeeld Hallo in een status van is *gestopt* of *stoppen*.

    ($ActivityOutput["Get-AzureVM"].PowerState –eq "Stopped") -or ($ActivityOutput["Get-AzureVM"].PowerState –eq "Stopping") 


### <a name="hashtables"></a>Hash-tabellen
[Hash-tabellen](http://technet.microsoft.com/library/hh847780.aspx) zijn naam/waarde-paren die handig zijn voor een set waarden retourneren.  Eigenschappen voor bepaalde activiteiten kunnen een hashtabel in plaats van een eenvoudige waarde verwacht.  U ziet mogelijk ook de hashtabel bedoelde tooas een woordenlijst. 

U maken hash-tabel met de volgende syntaxis Hallo.  Een hashtabel mag een onbeperkt aantal vermeldingen bevatten, maar elk wordt gedefinieerd door een naam en waarde.

    @{ <name> = <value>; [<name> = <value> ] ...}

Hallo wordt volgende expressie bijvoorbeeld een hashtabel toobe in Hallo-gegevensbron wordt gebruikt voor de parameter van een activiteit die een hashtabel met waarden voor een zoekopdracht internet verwacht.

    $query = "Azure Automation"
    $count = 10
    $h = @{'q'=$query; 'lr'='lang_ja';  'count'=$Count}
    $h

Hallo volgende voorbeeld wordt de uitvoer van een activiteit aangeroepen *Twitter-verbinding ophalen* toopopulate een hashtabel.

    @{'ApiKey'=$ActivityOutput['Get Twitter Connection'].ConsumerAPIKey;
      'ApiSecret'=$ActivityOutput['Get Twitter Connection'].ConsumerAPISecret;
      'AccessToken'=$ActivityOutput['Get Twitter Connection'].AccessToken;
      'AccessTokenSecret'=$ActivityOutput['Get Twitter Connection'].AccessTokenSecret}



## <a name="next-steps"></a>Volgende stappen
* tooget gestart met PowerShell workflow-runbooks, Zie [Mijn eerste PowerShell workflow-runbook](automation-first-runbook-textual.md) 
* Zie tooget gestart met grafische runbooks [Mijn eerste grafische runbook](automation-first-runbook-graphical.md)
* tooknow meer informatie over runbooktypen, hun voordelen en beperkingen, Zie [Azure Automation-runbooktypen](automation-runbook-types.md)
* toounderstand hoe Automation Run As-account, met behulp van tooauthenticate Hallo raadpleegt [configureren Azure uitvoeren als-Account](automation-sec-configure-azure-runas-account.md)

