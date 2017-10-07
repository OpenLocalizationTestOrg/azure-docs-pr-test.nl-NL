---
title: aaaAdd voorwaarden en werkstromen - Azure Logic Apps starten | Microsoft Docs
description: Bepalen hoe werkstromen worden uitgevoerd in Azure Logic Apps door voorwaardelijke logica, triggers, acties en parameters toe te voegen.
author: stepsic-microsoft-com
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: e4e24de4-049a-4b3a-a14c-3bf3163287a8
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/28/2017
ms.author: LADocs; stepsic
ms.openlocfilehash: 76d5e44590ffa14cf70d7a93b99a241d286d555b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-logic-apps-features"></a>Functies van logische Apps gebruiken

In een [vorige onderwerp](../logic-apps/logic-apps-create-a-logic-app.md), u hebt uw eerste logische app hebt gemaakt. toocontrol uw logische app werkstroom, kunt u verschillende paden voor uw logische app toorun opgeven en hoe te verwerken gegevens in matrices, verzamelingen en batches. U kunt deze elementen opnemen in uw logische app werkstroom:

* Voorwaarden en [overschakelen instructies](../logic-apps/logic-apps-switch-case.md) kunt u uw logische app uitgevoerd verschillende acties op basis van of bepaalde voorwaarden wordt voldaan.

* [Lussen](../logic-apps/logic-apps-loops-and-scopes.md) kunt u uw logische app herhaaldelijk stappen uitvoeren. Bijvoorbeeld, u kunt acties herhalen via een matrix wanneer u een **For_each** lus. Of u kunt acties herhalen totdat een voorwaarde wordt voldaan, wanneer u een **totdat** lus.

* [Scopes](../logic-apps/logic-apps-loops-and-scopes.md) laat u groeperen reeks acties, bijvoorbeeld tooimplement uitzonderingsverwerking.

* [Debatching](../logic-apps/logic-apps-loops-and-scopes.md) kunt u uw logische app afzonderlijke werkstromen voor items in een matrix met gestart Hallo **SplitOn** opdracht.

Dit onderwerp biedt informatie over andere concepten voor het bouwen van uw logische app:

* Weergave tooedit een bestaande logische app-code
* Opties voor het starten van een werkstroom

## <a name="conditions-run-steps-only-after-meeting-a-condition"></a>Voorwaarden: Stappen uitvoeren na het voldoen aan een voorwaarde

toohave uw logische app stappen alleen uitgevoerd als gegevens aan bepaalde criteria voldoet, kunt u een voorwaarde waarmee gegevens in de werkstroom op basis van specifieke velden of waarden Hallo vergeleken toevoegen.

Stel dat u hebt een logische app die u op een website RSS-feed te veel e-mails voor berichten verzendt. U kunt toevoegen om dat een voorwaarde zodat uw logische app stuurt een e-mailbericht alleen wanneer nieuwe Hallo boekt behoort tooa specifieke categorie.

1. In Hallo [Azure-portal](https://portal.azure.com), zoeken en openen van uw logische app in Logic App-ontwerper.

2. Een voorwaarde toohello werkstroom locatie die u wilt toevoegen. 

   tooadd hello voorwaarde tussen bestaande stappen in Hallo logic app werkstroom aanwijzer Hallo boven Hallo pijl waar u tooadd Hallo voorwaarde. 
   Kies Hallo **plusteken** (**+**), en kies vervolgens **een voorwaarde toevoegen**. Bijvoorbeeld:

   ![Voorwaarde toologic app toevoegen](./media/logic-apps-use-logic-app-features/add-condition.png)

   > [!NOTE]
   > Als u een voorwaarde tooadd aan Hallo einde van uw huidige werkstroom wilt, gaat u toohello onder aan uw logische app en kies **+ een nieuwe stap**.

3. Nu Hallo voorwaarde definiëren. Hallo bronveld dat u tooevaluate, Hallo bewerking tooperform, en de doelwaarde Hallo of veld wilt opgeven. tooyour voorwaarde tooadd bestaande velden kiezen uit Hallo **dynamische inhoud lijst toevoegen**.

   Bijvoorbeeld:

   ![Voorwaarde in de standaardmodus bewerken](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode.png)

   Dit is de volledige voorwaarde Hallo:

   ![Volledige voorwaarde](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode-2.png)

   > [!TIP]
   > Kies toodefine Hallo voorwaarde in code **bewerken in de geavanceerde modus**. Bijvoorbeeld:
   > 
   > ![Voorwaarde in de code bewerken](./media/logic-apps-use-logic-app-features/edit-condition-advanced-mode.png)

4. Onder **als Ja** en **als Nee**, voeg Hallo stappen tooperform op basis van of Hallo voorwaarde wordt voldaan.

   Bijvoorbeeld:

   ![Voorwaarde van Ja en er worden geen paden](./media/logic-apps-use-logic-app-features/condition-yes-no-path.png)

   > [!TIP]
   > U kunt bestaande acties naar Hallo slepen **als Ja** en **als Nee** paden.

5. Wanneer u bent klaar, slaat u uw logische app.

U krijgt nu e-mailberichten alleen wanneer het Hallo-berichten aan de voorwaarde voldoen.

## <a name="repeat-actions-over-a-list-with-foreach"></a>Acties over een lijst met forEach herhalen

Hallo forEach lus bevat een matrix toorepeat een actie via. Als het is niet een matrix, mislukt de Hallo-stroom. Als er action1 die een matrix van berichten en toosend elk bericht gewenste, kunt u deze instructie forEach opnemen in de eigenschappen van uw actie Hallo:`forEach : "@action('action1').outputs.messages"`

## <a name="edit-hello-code-definition-for-a-logic-app"></a>Hallo codedefinitie voor een logische app bewerken

Hoewel u Hallo Logic App-ontwerper hebt, kunt u direct Hallo-code die een logische app definieert bewerken.

1. Kies op de opdrachtbalk Hallo **codeweergave**.

    Een volledige-editor wordt geopend en toont Hallo-definitie die u bewerkt.

    ![Codeweergave](media/logic-apps-use-logic-app-features/codeview.png)

    In de teksteditor hello, kunt u kopiëren en plakken van een willekeurig aantal acties in Hallo dezelfde logische app of tussen logische apps. 
    U kunt ook eenvoudig toevoegen of verwijderen van volledige secties van Hallo definitie en u kunt ook definities met anderen delen.

2. toosave uw bewerkingen kiezen **opslaan**.

## <a name="parameters"></a>Parameters

Enkele mogelijkheden van Logic Apps zijn alleen beschikbaar in de codeweergave, bijvoorbeeld parameters. Parameters kunnen u eenvoudig tooreuse waarden in uw logische app. Als u een e-mailadres die u gebruiken in verschillende acties wilt hebt, moet u dat e-mailadres definiëren als een parameter.

Parameters zijn goed voor het ophalen van waarden waarschijnlijk toochange veel te zijn. Ze zijn vooral nuttig wanneer u parameters in verschillende omgevingen toooverride nodig. hoe toooverride parameters op basis van de omgeving, Zie toolearn [logic app-definities auteur](../logic-apps/logic-apps-author-definitions.md) en [REST API-documentatie](https://docs.microsoft.com/rest/api/logic).

Dit voorbeeld ziet u hoe tooupdate uw bestaande logische app zodat u kunt de parameters voor de zoekterm hello gebruiken.

1. Hallo zoeken in de codeweergave `parameters : {}` object en voeg een `currentFeedUrl` object:

        "currentFeedUrl" : {
            "type" : "string",
            "defaultValue" : "http://rss.cnn.com/rss/cnn_topstories.rss"
        }

2. Ga toohello `When_a_feed-item_is_published` actie, zoeken Hallo `queries` sectie en vervang de waarde van de query Hallo met:`"feedUrl": "#@{parameters('currentFeedUrl')}"` 

    toojoin twee of meer tekenreeksen, u kunt ook Hallo `concat` functie. 
    Bijvoorbeeld: `"@concat('#',parameters('currentFeedUrl'))"` werkt hetzelfde als bovenstaande Hallo Hallo.

3.  Als u bent klaar, kiest u **opslaan**. 

    Nu kunt u Hallo-website RSS-feed door een andere URL via Hallo `currentFeedURL` object.

Meer informatie over [hoe tooauthor logic app-definities](../logic-apps/logic-apps-author-definitions.md).

## <a name="start-logic-app-workflows"></a>Logic app-werkstromen starten

U hebt verschillende opties voor het starten van Hallo werkstroom gedefinieerd in uw logische app. U kunt altijd een werkstroom op verzoek starten in Hallo [Azure-portal].

### <a name="recurrence-triggers"></a>Terugkeerpatroon triggers

Een terugkeerpatroon trigger wordt uitgevoerd met een interval dat u opgeeft. Wanneer Hallo-trigger voorwaardelijke logica heeft, bepaalt Hallo trigger of Hallo werkstroom toorun nodig. Een trigger geeft Hallo werkstroom moet worden uitgevoerd door te retourneren een `200` statuscode. Wanneer Hallo werkstroom niet toorun hoeft, Hallo trigger retourneert een `202` statuscode.

### <a name="callback-using-rest-apis"></a>Callback met REST API 's

een werkstroom toostart, services kunnen een logic app-eindpunt aanroepen. Dit soort logic app op aanvraag, kiest u toostart **nu uitvoeren** op Hallo opdrachtbalk klikken. Zie [werkstromen starten door het aanroepen van logic app eindpunten als triggers](../logic-apps/logic-apps-http-endpoint.md). 

<!-- Shared links -->
[Azure-portal]: https://portal.azure.com

## <a name="next-steps"></a>Volgende stappen

* [Switch-instructies](../logic-apps/logic-apps-switch-case.md) 
* [Lussen, bereiken en debatching](../logic-apps/logic-apps-loops-and-scopes.md)
* [Definities voor logische apps maken](../logic-apps/logic-apps-author-definitions.md)