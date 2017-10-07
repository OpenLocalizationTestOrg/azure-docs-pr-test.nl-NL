---
title: aaaMonitor en gegevenspijplijnen - Azure beheren | Microsoft Docs
description: Ontdek hoe toouse Hallo toomonitor voor bewaking en beheer-app en beheren van Azure data factory's en pijplijnen.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: f3f07bc4-6dc3-4d4d-ac22-0be62189d578
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: spelluru
ms.openlocfilehash: 5e4ef6ec5fb8ebc9bda0be7899a39a51d58403d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-hello-monitoring-and-management-app"></a>Bewaken en beheren van Azure Data Factory-pijplijnen met Hallo-app voor bewaking en beheer
> [!div class="op_single_selector"]
> * [Met behulp van Azure portal/Azure PowerShell](data-factory-monitor-manage-pipelines.md)
> * [Met bewaking en beheer-app](data-factory-monitor-manage-app.md)
>
>

Dit artikel wordt beschreven hoe toouse Hallo app toomonitor voor bewaking en beheer, beheren en fouten opsporen in uw Data Factory-pijplijnen. Het biedt ook informatie over hoe toocreate tooget melding op fouten waarschuwingen. U kunt aan de slag met het gebruik van de toepassing hello door te kijken Hallo volgende video:

> [!NOTE]
> Hallo-gebruikersinterface wordt weergegeven in Hallo video mogelijk niet precies overeenkomt met wat u ziet in Hallo-portal. Het iets oudere is, maar concepten Hallo blijven hetzelfde. 

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-Data-Factory-Monitoring-and-Managing-Big-Data-Piplines/player]
>

## <a name="launch-hello-monitoring-and-management-app"></a>Hallo bewaking en beheer-app starten
toolaunch hello Monitor en app Management, klikt u op Hallo **Monitor & beheren** tegel op Hallo **Data Factory** blade van uw gegevensfactory.

![Bewaking van de tegel op Hallo Data Factory-startpagina](./media/data-factory-monitor-manage-app/MonitoringAppTile.png)

U ziet Hallo bewaking en beheer app in een apart venster geopend.  

![App voor controle en beheer](./media/data-factory-monitor-manage-app/AppLaunched.png)

> [!NOTE]
> Als u ziet dat Hallo webbrowser is vastgelopen bij 'Autoriseren...', schakelt u Hallo **blokkeren van cookies van derden en sitegegevens** selectievakje-- of houd deze is geselecteerd, maakt u een uitzondering voor **login.microsoftonline.com** , en probeer het vervolgens opnieuw tooopen Hallo app.


In Hallo Activiteitsvensters lijst in het middelste deelvenster hello ziet u een venster van de activiteit voor elke uitvoering van een activiteit. Als u Hallo activiteit gepland toorun elk uur gedurende vijf uur hebt, ziet u bijvoorbeeld vijf activiteit windows die zijn gekoppeld aan vijf gegevenssegmenten. Als er geen activiteit windows in de lijst Hallo Hallo onderin, Hallo te volgen:
 
- Update Hallo **begintijd** en **eindtijd** filters op Hallo bovenste toomatch Hallo start en eindtijd van de pijplijn en klik op Hallo **toepassen** knop.  
- lijst van de activiteit Windows Hello wordt niet automatisch vernieuwd. Klik op Hallo **vernieuwen** op de werkbalk in Hallo Hallo **Activiteitsvensters** lijst.  

Als u geen deze stappen met een tootest Data Factory-toepassing, zelfstudie Hallo: [gegevens kopiëren van Blob Storage tooSQL-Database met de Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

## <a name="understand-hello-monitoring-and-management-app"></a>Hallo-app voor bewaking en beheer begrijpen
Er zijn drie tabbladen aan de linkerkant Hallo: **Resource Explorer**, **weergaven**, en **waarschuwingen**. het eerste tabblad hello (**Resource Explorer**) is standaard geselecteerd.

### <a name="resource-explorer"></a>Resource Explorer
U ziet Hallo volgende:

* Hallo Resource Explorer **structuurweergave** in het linkerdeelvenster Hallo.
* Hallo **diagramweergave** Hallo boven in het middelste deelvenster Hallo.
* Hallo **Activiteitsvensters** lijst Hallo onderaan in het middelste deelvenster Hallo.
* Hallo **eigenschappen**, **activiteit venster Explorer**, en **Script** tabbladen in het rechterdeelvenster Hallo.

In Resource Explorer ziet u alle resources (pijplijnen, gegevenssets, gekoppelde services) in de gegevensfactory Hallo in een boomstructuur. Wanneer u een object selecteren in Resource Explorer:

* Hallo gekoppelde Data Factory-entiteit op Hallo diagramweergave is gemarkeerd.
* [Activiteit windows gekoppeld](data-factory-scheduling-and-execution.md) zijn gemarkeerd in de lijst met Hallo activiteit Windows hello onderaan.  
* Hallo-eigenschappen van het geselecteerde object Hallo worden weergegeven in het venster Eigenschappen Hallo in het rechterdeelvenster Hallo.
* Hallo JSON-definitie van het geselecteerde object hello wordt weergegeven, indien van toepassing. Bijvoorbeeld: een gekoppelde service, een dataset of een pijplijn.

![Resource Explorer](./media/data-factory-monitor-manage-app/ResourceExplorer.png)

Zie Hallo [planning en uitvoering](data-factory-scheduling-and-execution.md) artikel voor meer conceptuele informatie over windows activiteit.

### <a name="diagram-view"></a>Diagramweergave
Hallo diagramweergave van een data factory biedt één van glas toomonitor en beheren van een gegevensfactory en de activa. Wanneer u een Data Factory-entiteit (gegevensset/pipeline) in de diagramweergave Hallo selecteert:

* Hallo data factory-entiteit wordt geselecteerd in de structuurweergave Hallo.
* Hallo gekoppelde windows zijn gemarkeerd in de lijst van de activiteit Windows hello activiteit.
* Hallo-eigenschappen van het geselecteerde object Hallo worden weergegeven in het venster Eigenschappen Hallo.

Wanneer Hallo pijplijn (niet in een onderbroken status) is ingeschakeld, wordt deze met een groene lijn weergegeven:

![Pijplijn uitgevoerd](./media/data-factory-monitor-manage-app/PipelineRunning.png)

U kunt onderbreken, hervatten of een pipeline is beëindigd door te selecteren in de diagramweergave Hallo en Hallo knoppen op de opdrachtbalk Hallo.

![Onderbreken/hervatten op de opdrachtbalk Hallo](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)
 
Er zijn drie opdrachtbalkknoppen voor Hallo pijplijn in Hallo diagramweergave. U kunt Hallo tweede knop toopause Hallo pijplijn gebruiken. Onderbreken Hallo activiteiten momenteel wordt uitgevoerd niet beëindigen en kan ze doorgaan toocompletion. Hallo derde knop pauzeert Hallo pijplijn en beëindigt de bestaande activiteiten in uitvoering. de eerste knop Hallo hervatten Hallo pijplijn. Wanneer uw pijplijn wordt onderbroken, verandert de kleur van de Hallo van Hallo pijplijn. Bijvoorbeeld ziet een onderbroken pijplijn er in Hallo installatiekopie te volgen: 

![Pijplijn onderbroken](./media/data-factory-monitor-manage-app/PipelinePaused.png)

Meervoudige selectie twee of meer pijplijnen kunt u met behulp van Hallo Ctrl-toets. U kunt Hallo opdracht balk knoppen toopause/hervatten meerdere pijplijnen tegelijk.

U kunt ook met de rechtermuisknop op een pijplijn en selecteer opties toosuspend, hervatten of een pipeline is beëindigd. 

![Contextmenu voor de pijplijn](./media/data-factory-monitor-manage-app/right-click-menu-for-pipeline.png)

Klik op Hallo **pijplijn openen** toosee alle Hallo activiteiten in de pijplijn Hallo optie. 

![Menu Pijplijn openen](./media/data-factory-monitor-manage-app/OpenPipelineMenu.png)

In de weergave van de pijplijn Hallo geopend ziet u alle activiteiten in Hallo pijplijn. In dit voorbeeld is er slechts één activiteit: Kopieeractiviteit. 

![Geopende pijplijn](./media/data-factory-monitor-manage-app/OpenedPipeline.png)

back-toogo toohello vorige weergave, klikt u op Hallo data factory-naam in Hallo breadcrumb menu Hallo boven.

Pijplijnweergave hello, wanneer u een uitvoergegevensset of wanneer u de muisaanwijzer over uitvoergegevensset hello, selecteert ziet u in Hallo Windows van de activiteit pop-upvenster voor deze gegevensset.

![Activiteit Windows pop-upvenster](./media/data-factory-monitor-manage-app/ActivityWindowsPopup.png)

U kunt een activiteit venster toosee details klikken voor het in Hallo **eigenschappen** venster in het rechterdeelvenster Hallo.

![Eigenschappen van het venster activiteit](./media/data-factory-monitor-manage-app/ActivityWindowProperties.png)

In het rechterdeelvenster Hallo overschakelen toohello **activiteit venster Explorer** toosee tabblad meer informatie.

![Activiteit venster Explorer](./media/data-factory-monitor-manage-app/ActivityWindowExplorer.png)

U ziet ook **opgelost variabelen** voor elke poging uitvoeren voor een activiteit in Hallo **pogingen** sectie.

![Opgelost variabelen](./media/data-factory-monitor-manage-app/ResolvedVariables.PNG)

Overschakelen van toohello **Script** toosee Hallo JSON-script-definitie voor het geselecteerde object Hallo tabblad.   

![Tabblad script](./media/data-factory-monitor-manage-app/ScriptTab.png)

Hier ziet u activiteitsvensters op drie locaties:

* Hallo activiteit Windows pop-upvenster in Hallo diagramweergave (middelste deelvenster).
* Hallo activiteit venster Explorer in het rechterdeelvenster Hallo.
* lijst met Hallo activiteit Windows in Hallo onderste deelvenster.

U kunt bladeren toohello vorige week in Hallo Windows van de activiteit pop-upvenster en activiteit venster Explorer en Hallo volgende week met behulp van Hallo pijlen naar rechts en.

![Activiteit Explorer-venster horizontaal pijlen](./media/data-factory-monitor-manage-app/ActivityWindowExplorerLeftRightArrows.png)

Aan de onderkant van de Hallo Hallo diagramweergave, ziet u deze knoppen: inzoomen, uitzoomen, zoomen tooFit, zoomen 100%, indeling vergrendelen. Hallo **indeling vergrendelen** knop voorkomt u dat u per ongeluk tabellen en pijplijnen verplaatsen in Hallo diagramweergave. Deze is standaard ingeschakeld. U kunt deze uitschakelen en entiteiten navigeren in Hallo-diagram. Wanneer u deze uitschakelen, gebruikt u Hallo laatste knop tooautomatically positie tabellen en pijplijnen. U kunt ook in- of uitzoomen met Hallo muiswiel.

![Diagram van weergave zoomopdrachten](./media/data-factory-monitor-manage-app/DiagramViewZoomCommands.png)

### <a name="activity-windows-list"></a>Lijst met Windows
Hallo Activiteitsvensters lijst onderaan Hallo Hallo middelste deelvenster geeft alle activiteitsvensters voor Hallo gegevensset die u hebt geselecteerd in Hallo Resource Explorer of Hallo diagramweergave. Hallo-lijst is standaard in aflopende volgorde, wat betekent dat u de meest recente activiteitvenster boven Hallo Hallo ziet.

![Lijst met Windows](./media/data-factory-monitor-manage-app/ActivityWindowsList.png)

Deze lijst vernieuwd niet automatisch zodat dit gebruik de knop Hallo vernieuwen op Hallo werkbalk toomanually vernieuwen.  

Activiteit windows kunnen worden gebruikt in een Hallo volgende statussen:

<table>
<tr>
    <th align="left">Status</th><th align="left">Substatus</th><th align="left">Beschrijving</th>
</tr>
<tr>
    <td rowspan="8">Wachten</td><td>ScheduleTime</td><td>Hallo-tijd is niet geleverd voor Hallo activiteit venster toorun.</td>
</tr>
<tr>
<td>DatasetDependencies</td><td>Hallo upstream-afhankelijkheden zijn niet gereed.</td>
</tr>
<tr>
<td>ComputeResources</td><td>Hallo rekenresources zijn niet beschikbaar.</td>
</tr>
<tr>
<td>ConcurrencyLimit</td> <td>Alle Hallo-activiteitsinstanties zijn bezig met andere windows activiteit.</td>
</tr>
<tr>
<td>ActivityResume</td><td>Hallo-activiteit is onderbroken en Hallo activiteit windows kan niet worden uitgevoerd totdat deze hervat.</td>
</tr>
<tr>
<td>Probeer het opnieuw</td><td>Er wordt opnieuw geprobeerd Hallo activiteit is uitgevoerd.</td>
</tr>
<tr>
<td>Validatie</td><td>Validatie is nog niet gestart.</td>
</tr>
<tr>
<td>ValidationRetry</td><td>Validatie is wachten toobe opnieuw geprobeerd.</td>
</tr>
<tr>
<tr>
<td rowspan="2">InProgress</td><td>Valideren</td><td>Validatie wordt uitgevoerd.</td>
</tr>
<td>-</td>
<td>venster van de activiteit Hello wordt verwerkt.</td>
</tr>
<tr>
<td rowspan="4">Is mislukt</td><td>Time-out</td><td>Hallo activiteit uitvoeren duurde langer dan is toegestaan door Hallo-activiteit.</td>
</tr>
<tr>
<td>Geannuleerd</td><td>venster van de activiteit Hallo is geannuleerd door in te grijpen.</td>
</tr>
<tr>
<td>Validatie</td><td>Validatie is mislukt.</td>
</tr>
<tr>
<td>-</td><td>venster van de activiteit Hallo mislukt toobe gegenereerd of gevalideerd.</td>
</tr>
<td>Gereed</td><td>-</td><td>venster van de activiteit Hallo is gereed voor gebruik.</td>
</tr>
<tr>
<td>Overgeslagen</td><td>-</td><td>venster Hallo-activiteit is niet verwerkt.</td>
</tr>
<tr>
<td>Geen</td><td>-</td><td>Het venster van een activiteit tooexist gebruikt met een andere status, maar is opnieuw ingesteld.</td>
</tr>
</table>


Wanneer u klikt op een venster van de activiteit in de lijst hello, ziet u meer informatie over het in Hallo **activiteit Windows Verkenner** of Hallo **eigenschappen** -venster op de juiste Hallo.

![Activiteit venster Explorer](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-2.png)

### <a name="refresh-activity-windows"></a>Activiteit windows vernieuwen
Hallo details worden niet automatisch vernieuwd, dus Hallo de knop Vernieuwen (Hallo tweede knop) op de opdrachtbalk lijst met toomanually vernieuwen Hallo activiteit windows hello gebruiken.  

### <a name="properties-window"></a>Eigenschappenvenster
het venster Eigenschappen Hello wordt Hallo meest rechtse deelvenster van Hallo-app voor bewaking en beheer.

![Eigenschappenvenster](./media/data-factory-monitor-manage-app/PropertiesWindow.png)

Eigenschappen voor Hallo-item dat u hebt geselecteerd in Hallo Resource Explorer (structuurweergave), wordt de diagramweergave of activiteit Windows-lijst.

### <a name="activity-window-explorer"></a>Activiteit venster Explorer
Hallo **activiteit venster Explorer** venster is in Hallo meest rechtse deelvenster van Hallo-app voor bewaking en beheer. Meer informatie over het venster van de Hallo-activiteit die u hebt geselecteerd in Hallo Windows van de activiteit pop-upvenster of lijst van de activiteit Windows hello wordt weergegeven.

![Activiteit venster Explorer](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-3.png)

U kunt venster van de activiteit tooanother schakelen door erop te klikken in de weergave van de kalender Hallo Hallo boven. U kunt ook gebruik Hallo pijl-links/rechts pijltjesknoppen op Hallo bovenste toosee activiteit windows hello vorige week of Hallo volgende week.

U kunt werkbalkknoppen hello gebruiken in Hallo onderste deelvenster toorerun Hallo activiteitvenster of Hallo details in het deelvenster Hallo vernieuwen.

### <a name="script"></a>Script
U kunt Hallo **Script** tabblad tooview Hallo JSON-definitie Hallo Data Factory-entiteit (gekoppelde service, gegevensset of pijplijn) geselecteerd.

![Tabblad script](./media/data-factory-monitor-manage-app/ScriptTab.png)

## <a name="use-system-views"></a>Systeemweergaven gebruiken
Hallo bewaking en beheer-app bevat vooraf samengestelde systeemweergaven (**recente activiteit windows**, **activiteitsvensters is mislukt**, **windows activiteit In uitvoering**) die kunt u tooview recente/mislukt/in uitvoering activiteitsvensters van uw gegevensfactory.

Overschakelen van toohello **weergaven** tabblad aan de linkerkant Hallo door erop te klikken.

![Weergaven tabblad bewaking](./media/data-factory-monitor-manage-app/MonitoringViewsTab.png)

Er zijn momenteel drie systeemweergaven die worden ondersteund. Selecteer een optie toosee recente activiteit windows, windows mislukte activiteit of activiteit in uitvoering windows in de lijst met activiteit Windows hello (onderaan Hallo Hallo middelste deelvenster).

Wanneer u selecteert Hallo **recente activiteit windows** optie, ziet u alle recente activiteit windows in aflopende volgorde Hallo **tijd laatste poging**.

U kunt Hallo **activiteitsvensters is mislukt** activiteitsvensters toosee is mislukt in Hallo lijst bekijken. Selecteer een mislukte activiteit-venster in Hallo toosee details weergeven over het in Hallo **eigenschappen** venster of Hallo **activiteit venster Explorer**. U kunt ook alle logboeken voor een mislukte activiteitvenster downloaden.

## <a name="sort-and-filter-activity-windows"></a>Activiteitsvensters sorteren en filteren
Wijziging Hallo **begintijd** en **eindtijd** instellingen in de opdrachtbalk toofilter activiteit windows hello. Nadat u Hallo begintijd en eindtijd wijzigt, klikt u op Hallo knop volgende toohello end toorefresh hello Activiteitsvensters lijst time.

![Begin- en eindtijden](./media/data-factory-monitor-manage-app/StartAndEndTimes.png)

> [!NOTE]
> Alle tijden zijn momenteel in UTC-notatie in Hallo-app voor bewaking en beheer.
>
>

In Hallo **Activiteitsvensters lijst**, klikt u op Hallo-naam van een kolom (bijvoorbeeld: Status).

![Menu kolom activiteit Windows-lijst](./media/data-factory-monitor-manage-app/ActivityWindowsListColumnMenu.png)

U kunt doen Hallo volgende:

* Sorteren in oplopende volgorde.
* Sorteren in aflopende volgorde.
* Filteren op een of meer waarden (Ready, Waiting, enzovoort).

Wanneer u een filter voor een kolom opgeven, ziet u de knop filteren Hallo voor die kolom, waarmee wordt aangegeven dat de Hallo-waarden in kolom Hallo gefilterde waarden zijn ingeschakeld.

![Filteren op een kolom van een lijst van de activiteit Windows hello](./media/data-factory-monitor-manage-app/ActivityWindowsListFilterInColumn.png)

U kunt dezelfde pop-upvenster tooclear filters Hallo. tooclear alle filters voor lijst van de activiteit Windows hello, klik op Hallo filter wissen op de opdrachtbalk Hallo.

![Alle filters voor een lijst van de activiteit Windows hello wissen](./media/data-factory-monitor-manage-app/ClearAllFiltersActivityWindowsList.png)

## <a name="perform-batch-actions"></a>Batch-acties uitvoeren
### <a name="rerun-selected-activity-windows"></a>Geselecteerde activiteit windows opnieuw uitvoeren
Selecteer een activiteitvenster, klikt u op Hallo pijl-omlaag voor Hallo eerste knop en selecteer **opnieuw uitvoeren** / **opnieuw uitvoeren met upstream in pijplijn**. Wanneer u Hallo selecteert **opnieuw uitvoeren met upstream in pijplijn** optie, evenals alle upstream-activiteit-vensters opnieuw worden uitgevoerd.
    ![Voer een venster van de activiteit](./media/data-factory-monitor-manage-app/ReRunSlice.png)

Kunt u ook meerdere activiteitsvensters selecteren in lijst Hallo en ze opnieuw uitvoeren op Hallo hetzelfde moment. Kunt u toofilter activiteitsvensters op basis van status hello (bijvoorbeeld: **mislukt**)-- en voert u na het corrigeren van Hallo probleem waardoor Hallo activiteit windows toofail activiteitsvensters Hallo is mislukt. Zie de volgende sectie voor meer informatie over het filteren van activiteit windows in de lijst Hallo Hallo.  

### <a name="pauseresume-multiple-pipelines"></a>Meerdere pijplijnen onderbreken/hervatten
U kunt multiselect twee of meer pijplijnen met Hallo Ctrl-toets. U kunt Hallo opdrachtbalkknoppen (die zijn gemarkeerd in rood Hallo rechthoek op Hallo volgende afbeelding) toopause/hervatten ze.

![Onderbreken/hervatten op de opdrachtbalk Hallo](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)

## <a name="create-alerts"></a>Waarschuwingen maken
Hallo **waarschuwingen** pagina kunt u bij het maken van een waarschuwing en de bestaande waarschuwingen weergeven/bewerken/verwijderen. U kunt ook inschakelen/uitschakelen een waarschuwing. toosee Hallo pagina waarschuwingen, klikt u op Hallo **waarschuwingen** tabblad.

![Tabblad waarschuwingen](./media/data-factory-monitor-manage-app/AlertsTab.png)

### <a name="toocreate-an-alert"></a>toocreate een waarschuwing
1. Klik op **waarschuwing toevoegen** tooadd een waarschuwing. U ziet Hallo **Details** pagina.

    ![Waarschuwingen - pagina met Details maken](./media/data-factory-monitor-manage-app/CreateAlertDetailsPage.png)
2. Geef Hallo **naam** en **beschrijving** voor Hallo waarschuwing en klik op **volgende**. U ziet Hallo **Filters** pagina.

    ![Waarschuwingen - pagina Filters maken](./media/data-factory-monitor-manage-app/CreateAlertFiltersPage.png)
3. Selecteer Hallo **gebeurtenis**, **status**, en **substatus** (optioneel) dat u wilt dat toocreate Data Factory-service voor een waarschuwing en klik op **volgende**. U ziet Hallo **ontvangers** pagina.

    ![Waarschuwingen - ontvangers pagina maken](./media/data-factory-monitor-manage-app/CreateAlertRecipientsPage.png)
4. Selecteer Hallo **e-abonnementsbeheerders** optie en/of geef een **extra beheerders-e**, en klik op **voltooien**. U ziet de waarschuwing in de lijst Hallo Hallo.

    ![Lijst met waarschuwingen](./media/data-factory-monitor-manage-app/AlertsList.png)

Gebruik de knoppen met de Hallo die gekoppeld aan Hallo waarschuwing tooedit/delete/inschakelen/uitschakelen een waarschuwing zijn in de lijst met Hallo-meldingen.

### <a name="eventstatussubstatus"></a>Status-gebeurtenis/substatus
Hallo bevat volgende tabel Hallo lijst met beschikbare gebeurtenissen en status (en substatus).

| De naam van gebeurtenis | Status | Substatus |
| --- | --- | --- |
| Activiteit die wordt uitgevoerd gestart |Gestart |Starting |
| Activiteit die wordt uitgevoerd is voltooid |Geslaagd |Geslaagd |
| Activiteit die wordt uitgevoerd is voltooid |Is mislukt |Fout in de Resource-toewijzing<br/><br/>Mislukte uitvoering<br/><br/>Time-out<br/><br/>De validatie is mislukt<br/><br/>Afgebroken |
| On-Demand HDI-Cluster maken gestart |Gestart |-|
| On-Demand HDI-Cluster is gemaakt |Geslaagd |-|
| On-Demand-HDI-Cluster is verwijderd |Geslaagd |-|

### <a name="tooedit-delete-or-disable-an-alert"></a>tooedit, verwijderen of uitschakelen van een waarschuwing

Gebruik hello tooedit knoppen (rood gemarkeerd), verwijderen of uitschakelen van een waarschuwing te volgen.

![Waarschuwingen knoppen](./media/data-factory-monitor-manage-app/AlertButtons.png)
