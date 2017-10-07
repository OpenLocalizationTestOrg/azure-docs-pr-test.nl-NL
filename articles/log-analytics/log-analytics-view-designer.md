---
title: aaaCreate tooanalyze gegevens bekijkt in OMS Log Analytics | Microsoft Docs
description: Weergave Designer in Log Analytics kunt u toocreate aangepaste weergaven die worden weergegeven in Hallo OMS en Azure-portal en verschillende visualisaties van gegevens in de OMS-opslagplaats Hallo bevatten. Dit artikel bevat een overzicht van Designer bekijken en procedures voor het maken en bewerken van aangepaste weergaven.
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: ce41dc30-e568-43c1-97fa-81e5997c946a
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: bwren
ms.openlocfilehash: 40b4bfef50d70e4479b6cae16abfa8ec33d1a2f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-view-designer-toocreate-custom-views-in-log-analytics"></a>Ontwerper toocreate aangepaste weergaven gebruiken in Log Analytics
Hallo-ontwerper in [logboekanalyse](log-analytics-overview.md) kunt u toocreate aangepaste weergaven in de OMS-console Hallo die verschillende visualisaties van gegevens in de OMS-opslagplaats Hallo bevatten. Dit artikel bevat een overzicht van Designer bekijken en procedures voor het maken en bewerken van aangepaste weergaven.

Er zijn andere artikelen die beschikbaar zijn voor weergave Designer:

* [Tegel verwijzing](log-analytics-view-designer-tiles.md) -verwijzing van instellingen voor elk Hallo Hallo tegels beschikbaar toouse in aangepaste weergaven.
* [Visualisatie onderdeelverwijzing](log-analytics-view-designer-parts.md) -verwijzing van instellingen voor elk Hallo Hallo tegels beschikbaar toouse in aangepaste weergaven.

>[!NOTE]
> Als uw werkruimte bijgewerkte toohello is [querytaal van nieuwe logboekanalyse](log-analytics-log-search-upgrade.md), en vervolgens de query's in alle weergaven moeten worden geschreven in Hallo [nieuwe querytaal](https://go.microsoft.com/fwlink/?linkid=856078).  De weergaven die zijn gemaakt voordat het Hallo-werkruimte is bijgewerkt worden doorloopt geconverteerd.

## <a name="concepts"></a>Concepten
Weergaven maken met de Hallo-ontwerper bevatten Hallo-elementen in de volgende tabel Hallo.

| Onderdeel | Beschrijving |
|:--- |:--- |
| Tegel |Op Hallo hoofddashboard Log Analytics overzicht weergegeven.  Bevat een visual samenvatten van gegevens in Hallo Hallo aangepaste weergave.  Verschillende typen van de tegel bieden verschillende visualisaties van records in Hallo OMS-opslagplaats.  Klik op Hallo tegel tooopen Hallo aangepaste weergave. |
| Aangepaste weergave |Wanneer gebruiker Hallo op Hallo tegel weergegeven.  Bevat een of meer visualisatie delen. |
| Visualisatie delen |Visualisatie van gegevens in de OMS-opslagplaats Hallo op basis van een of meer [Meld zoekopdrachten](log-analytics-log-searches.md).  De meeste onderdelen bevat een Header die een hoog niveau visualisatie bevat en een lijst met Hallo bovenste resultaten.  Verschillende typen bieden verschillende visualisaties van records in Hallo OMS-opslagplaats.  Klik op elementen in Hallo onderdeel tooperform een logboek zoekopdracht bieden gedetailleerde records. |

![Overzicht van de Designer](media/log-analytics-view-designer/overview.png)

## <a name="add-view-designer-tooyour-workspace"></a>Ontwerper tooyour werkruimte toevoegen
Hoewel weergave Designer Preview-versie, moet u deze toevoegen tooyour werkruimte door te selecteren **Voorbeeldfuncties** in Hallo **instellingen** sectie van Hallo OMS-portal.

![Voorbeeld inschakelen](media/log-analytics-view-designer/preview.png)

## <a name="creating-and-editing-views"></a>Maken en bewerken van weergaven
### <a name="create-a-new-view"></a>Een nieuwe weergave maken
Een nieuwe weergave openen in Hallo **ontwerper** door te klikken op Hallo-ontwerper-tegel in Hallo hoofddashboard OMS.

![Designer-venster weergeven](media/log-analytics-view-designer/view-designer-tile.png)

### <a name="edit-an-existing-view"></a>Een bestaande weergave bewerken
tooedit een bestaande weergave in hello, open Hallo weergeven door te klikken op de tegel in Hallo hoofddashboard OMS-ontwerper.  Klik vervolgens op Hallo **bewerken** knop tooopen Hallo weergave in Hallo-ontwerper.

![Een weergave bewerken](media/log-analytics-view-designer/menu-edit.png)

### <a name="clone-an-existing-view"></a>Klonen van een bestaande weergave
Wanneer u een weergave klonen, wordt een nieuwe weergave gemaakt en geopend in de Hallo-ontwerper.  nieuwe weergave Hallo heeft dezelfde naam als de oorspronkelijke met 'Kopie' toegevoegde toohello einde van het Hallo Hallo.  een weergave, open tooclone Hallo bestaande weergave door te klikken op de tegel in Hallo hoofddashboard OMS.  Klik vervolgens op Hallo **kloon** knop tooopen Hallo weergave in Hallo-ontwerper.

![Klonen van een weergave](media/log-analytics-view-designer/edit-menu-clone.png)

### <a name="delete-an-existing-view"></a>Een bestaande weergave verwijderen
toodelete een bestaande weergave open Hallo weergeven door te klikken op de tegel in Hallo hoofddashboard OMS.  Klik vervolgens op Hallo **bewerken** tooopen Hallo weergave in Hallo Designer bekijken en klik op **weergave verwijderen**.

![Een weergave verwijderen](media/log-analytics-view-designer/edit-menu-delete.png)

### <a name="export-an-existing-view"></a>Exporteren van een bestaande weergave
U kunt een weergave tooa JSON-bestand dat u kunt importeren in een andere werkruimte of gebruik in exporteren een [Azure Resource Manager-sjabloon](../azure-resource-manager/resource-group-authoring-templates.md).  tooexport een bestaande weergave open Hallo weergeven door te klikken op de tegel in Hallo hoofddashboard OMS.  Klik vervolgens op Hallo **exporteren** knop toocreate een bestand in de downloadmap Hallo van de browser.  Hallo-naam van Hallo-bestand worden Hallo-naam van weergave met de extensie Hallo Hallo *omsview*.

![Een weergave exporteren](media/log-analytics-view-designer/edit-menu-export.png)

### <a name="import-an-existing-view"></a>Importeren van een bestaande weergave
U kunt importeren een *omsview* -bestand dat u hebt geëxporteerd uit een andere beheergroep.  een bestaande weergave tooimport eerst een nieuwe weergave maken.  Klik vervolgens op Hallo **importeren** knop en selecteer Hallo *omsview* bestand.  in de bestaande weergave Hallo worden Hallo configuratie uit Hallo-bestand gekopieerd.

![Een weergave exporteren](media/log-analytics-view-designer/edit-menu-import.png)

## <a name="working-with-view-designer"></a>Werken met de Designer bekijken
Hallo-ontwerper bestaat uit drie deelvensters.  Hallo **ontwerp** deelvenster Hallo aangepaste weergave vertegenwoordigt.  Wanneer u tegels en onderdelen toevoegen van Hallo **besturingselement** deelvenster toohello **ontwerp** deelvenster ze zijn toegevoegd toohello weergeven.  Hallo **eigenschappen** deelvenster Hallo-eigenschappen voor Hallo tegel of geselecteerde onderdeel weergegeven.

![Designer weergeven](media/log-analytics-view-designer/view-designer-screenshot.png)

### <a name="configure-view-tile"></a>Tegel configureren
Een aangepaste weergave kan slechts één tegel hebben.  Selecteer Hallo **tegel** tabblad in Hallo **besturingselement** deelvenster tooview Hallo huidige tegel of Selecteer een alternatieve.  Hallo **eigenschappen** deelvenster Hallo-eigenschappen voor de huidige tegel hello wordt weergegeven.  Hallo tegel eigenschappen configureren op basis van toohello gedetailleerde informatie in Hallo [tegel verwijzing](log-analytics-view-designer-tiles.md) en klik op **toepassen** toosave wijzigingen.

### <a name="configure-visualization-parts"></a>Visualisatie onderdelen configureren
Een weergave kan een onbeperkt aantal visualisatie onderdelen bevatten.  Selecteer Hallo **weergave** tabblad en vervolgens een visualisatie deel tooadd toohello weergeven.  Hallo **eigenschappen** deelvenster Hallo-eigenschappen voor Hallo geselecteerd onderdeel weergegeven.  Hallo weergave configureren volgens toohello eigenschappen gedetailleerde informatie in Hallo [visualisatie onderdeelverwijzing](log-analytics-view-designer-parts.md) en klik op **toepassen** toosave wijzigingen.

### <a name="delete-a-visualization-part"></a>U kunt een visualisatie deel verwijderen
U kunt een visualisatie-onderdeel verwijderen van Hallo weergeven door te klikken op Hallo **X** knop in Hallo rechtsboven Hallo-onderdeel.

### <a name="rearrange-visualization-parts"></a>Visualisatie onderdelen rangschikken
Weergaven hebben slechts één rij met visualisatie delen.  Bestaande onderdelen in een weergave rangschikken door te klikken en slepen tooa nieuwe locatie.

## <a name="next-steps"></a>Volgende stappen
* Voeg [tegels](log-analytics-view-designer-tiles.md) tooyour aangepaste weergave.
* Voeg [visualisatie delen](log-analytics-view-designer-parts.md) tooyour aangepaste weergave.
