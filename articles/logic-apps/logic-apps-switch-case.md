---
title: de instructie aaaSwitch voor verschillende acties in Azure Logic Apps | Microsoft Docs
description: Kies verschillende acties tooperform in logic apps op basis van Expressiewaarden met behulp van een switch-instructie
services: logic-apps
keywords: Switch-instructie
author: derek1ee
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: LADocs; deli
ms.openlocfilehash: 09ed7e4a752003aba157e9156bf4dc89ef86f5ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="perform-different-actions-in-logic-apps-with-a-switch-statement"></a>Verschillende acties worden uitgevoerd in logic apps met een switch-instructie

Wanneer het ontwerpen van een werkstroom, hebt u vaak tootake verschillende acties die zijn gebaseerd op Hallo-waarde van een object of een expressie. Bijvoorbeeld, wilt u mogelijk uw logische app toobehave anders op basis van de statuscode Hallo van een HTTP-aanvraag, of een optie in een e-mailbericht hebt geselecteerd.

U kunt een instructie switch tooimplement deze scenario's gebruiken. Uw logische app kunt beoordelen een token of een expressie, en kies Hallo geval Hello dezelfde waarde tooexecute Hallo opgegeven acties. Slechts één case moet overeenkomen met de Hallo switch-instructie.

> [!TIP]
> Net als alle programmeertalen ondersteuning switch instructies alleen gelijkheid operators. Als u andere relationele operators, zoals 'groter dan', gebruikt u een voorwaardeninstructie.
> tooensure deterministische uitvoeringsgedrag, gevallen moeten een uniek en statische waarde in plaats van de dynamische-tokens of expressie bevatten.

## <a name="prerequisites"></a>Vereisten

- Een actief Azure-abonnement. Als u een actief Azure-abonnement geen [een gratis account maken](https://azure.microsoft.com/free/), of probeer [Logic Apps voor gratis](https://tryappservice.azure.com/).
- [Elementaire kennis over logic apps](logic-apps-what-are-logic-apps.md)

## <a name="add-a-switch-statement-tooyour-workflow"></a>Een switch-instructie tooyour-werkstroom toevoegen

tooshow de werking van een switch-instructie, in dit voorbeeld wordt een logische app dat monitors bestanden tooDropbox geüpload. Wanneer nieuwe Hallo-bestanden zijn geüpload, Hallo logische app verzendt e-mail tooan goedkeurder die u kiest of tootransfer die tooSharePoint bestanden. Hallo app gebruikmaakt van een switchinstructie die verschillende acties uitvoert op basis van de Hallo die Hallo goedkeurder worden geselecteerd.

1. Een logische app maken en selecteer deze trigger: **Dropbox - wanneer een bestand wordt gemaakt**.

   ![Dropbox - gebruiken wanneer een bestand trigger wordt gemaakt](./media/logic-apps-switch-case/dropbox-trigger.jpg)

2. Deze actie onder Hallo-trigger toevoegen: **Outlook.com - e-mailbericht verzenden-goedkeuring**

   > [!TIP]
   > Logische apps ondersteunen ook verzenden goedkeuring e-scenario's uit een Outlook van Office 365-account.

   - Als u een bestaande verbinding geen hebt, wordt u gevraagd toocreate een.
   - Vul de velden Hallo vereist. Bijvoorbeeld onder **naar**, Hallo e-mailadres voor het verzenden van Hallo goedkeurder e-mailadres opgeven.
   - Onder **gebruikersopties**, voer `Approve, Reject`.

   ![Configureer de verbinding](./media/logic-apps-switch-case/send-approval-email-action.jpg)

3. Toevoegen van een switchinstructie.

   - Selecteer **+ een nieuwe stap** > **... Meer** > **toevoegen van een case**. 
   - Nu we tooselect Hallo actie tooperform op basis van Hallo willen `SelectedOptions` de uitvoer van Hallo *goedkeuring per E-mail* in te grijpen. 
   U vindt dit veld in Hallo **dynamische inhoud toevoegen** selector.
   - Gebruik *geval 1* toohandle wanneer Hallo goedkeurder selecteert `Approve`.
     - Als goedgekeurd, kopieert u Hallo oorspronkelijke bestand tooSharePoint Online Hello [ **SharePoint Online - bestand maken** actie](../connectors/connectors-create-api-sharepointonline.md).
     - Voeg een andere actie Hallo case toonotify gebruikers een nieuw bestand is beschikbaar in SharePoint.
   - Toevoegen van een andere aanvraag toohandle wanneer gebruiker selecteert `Reject`.
     - Als afgewezen, verzendt u een e-mailmelding andere goedkeurders wordt geïnformeerd dat Hallo-bestand wordt geweigerd en geen verdere actie vereist is.
   - `SelectedOptions`biedt slechts twee opties, zodat we Hallo kunt laten **standaard** geval leeg.

   ![Switch-instructie](./media/logic-apps-switch-case/switch.jpg)

   > [!NOTE]
   > Switch-instructie moet minimaal één letter in geval van toevoeging toohello standaard.

4. Na het Hallo-switch-instructie het oorspronkelijke bestand geüpload tooDropbox Hallo worden verwijderd door deze actie toe te voegen: **Dropbox - bestand verwijderen**

5. Sla uw logische app. Uw app testen door een tooDropbox bestand uploaden. U ontvangt binnenkort een e-mailbericht goedkeuring. Selecteer een optie en Hallo gedrag observeren.

   > [!TIP]
   > Te zoeken over[uw logische apps bewaken](logic-apps-monitor-your-logic-apps.md).

## <a name="understand-hello-code-behind-switch-statements"></a>Hallo code achter switch instructies begrijpen

Nu dat u een logische app met een switchinstructie is gemaakt, bekijken we de definitie van Hallo achter Hallo switch-instructie.

```json
"Switch": {
    "type": "Switch",
    "expression": "@body('Send_approval_email')?['SelectedOption']",
    "cases": {
        "Case 1" : {
            "case" : "Approved",
            "actions" : {}
        },
        "Case 2" : {
            "case" : "Rejected",
            "actions" : {}
        }
    },
    "default": {
        "actions": {}
    },
    "runAfter": {
        "Send_approval_email": [
            "Succeeded"
        ]
    }
}
```

* `"Switch"`Hallo naam is van de switch-instructie hello, die u kunt de naam voor de leesbaarheid. 
* `"type": "Switch"`Geeft aan dat de actie Hallo een switch-instructie. 
* `"expression"`Hallo goedkeurder van geselecteerde optie in dit voorbeeld is en geëvalueerd op basis van elk geval later in Hallo definitie is gedeclareerd. 
* `"cases"`kan een onbeperkt aantal gevallen bevatten. Voor elk geval `"Case *"` is de standaardnaam hello van geval Hallo die u kunt de naam voor de leesbaarheid. 
`"case"`Hiermee geeft u Hallo case-label, waarvoor de switch-expressie gebruikt voor vergelijking Hallo en moet een constante en unieke waarde. Als geen van de gevallen Hallo overeenkomt met de Hallo schakelexpressie, acties onder `"default"` worden uitgevoerd.

## <a name="get-help"></a>Help opvragen

tooask vragen, antwoorden op vragen, en zien welke andere Azure Logic Apps-gebruikers doen, gaat u naar Hallo [Azure Logic Apps-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp Azure Logic Apps en connectors verbeteren, stem of ideeën op Hallo indienen [Azure Logic Apps gebruiker feedback site](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Volgende stappen

- Meer informatie over hoe te[voorwaarden toevoegen](logic-apps-use-logic-app-features.md)
- Meer informatie over [fout en uitzonderingsverwerking](logic-apps-exception-handling.md)
- Ontdek meer [werkstroom taal mogelijkheden](logic-apps-author-definitions.md)