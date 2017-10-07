---
title: aaaCustom code voor Azure Logic Apps met Azure Functions | Microsoft Docs
description: Maken en uitvoeren van aangepaste code voor Azure Logic Apps met Azure Functions
services: logic-apps,functions
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 9fab1050-cfbc-4a8b-b1b3-5531bee92856
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 18b3821ed7e434feb568b9b96e9a5a2189dba3bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-and-run-custom-code-for-logic-apps-through-azure-functions"></a>Toevoegen en het uitvoeren van aangepaste code voor logic apps via Azure Functions

aangepaste codefragmenten toorun van C# of node.js in logic apps, kunt u aangepaste functies via Azure Functions. 
[Azure Functions](../azure-functions/functions-overview.md) biedt server gratis computergebruik in Microsoft Azure en zijn handig voor het uitvoeren van deze taken:

* Geavanceerde opmaak of compute van velden in logic apps
* Berekeningen in een werkstroom.
* Hallo logic app-functionaliteit met functies die worden ondersteund in C# of node.js uitbreiden

## <a name="create-custom-functions-for-your-logic-apps"></a>Aangepaste functies voor uw logische apps maken

Het is raadzaam dat u een functie in hello Azure Functions-portal, Hallo **Generic Webhook - knooppunt** of **Generic Webhook - C#** sjablonen. Hallo resultaat maakt een sjabloon die accepteert een door het automatisch ingevuld `application/json` van een logische app. Functies die u van deze sjablonen maakt worden automatisch gedetecteerd en worden weergegeven in Hallo Logic App-ontwerper onder **Azure Functions in mijn regio.**

In de Azure-portal op Hallo Hallo **integreren** deelvenster voor de functie, de sjabloon moet worden weergegeven die **modus** instellen te**Webhook** en **Webhook type** te is ingesteld,**algemene JSON**. 

Webhook functies een aanvraag accepteren en doorgegeven aan de methode Hallo via een `data` variabele. U kunt toegang tot Hallo eigenschappen van uw payload met puntnotatie zoals `data.function-name`. Voor een eenvoudige JavaScript-functie die een DateTime-waarde naar een datumtekenreeks converteert, ziet er bijvoorbeeld Hallo voorbeeld te volgen:

```
function start(req, res){
    var data = req.body;
    res = {
        body: data.date.ToDateString();
    }
}
```

## <a name="call-azure-functions-from-logic-apps"></a>Azure-functies aanroepen vanuit logic apps

toolist hello containers in uw abonnement en selecteer Hallo-functie die u wilt dat toocall in Logic App-ontwerper, klikt u op Hallo **acties** menu en selecteer een van de **Azure Functions in mijn regio**.

Nadat u de functie Hallo selecteert, bent u toospecify gevraagd een object van de nettolading van de invoer. Dit object is Hallo-bericht dat logic app verzendt toohello functie Hallo en moet een JSON-object. Bijvoorbeeld, als u wilt dat toopass in Hallo **laatst gewijzigd** datum na een trigger Salesforce Hallo functie nettolading kan eruitzien als in dit voorbeeld:

![Datum van laatste wijziging][1]

## <a name="trigger-logic-apps-from-a-function"></a>Trigger logische apps van een functie

U kunt een logische app van binnen een functie activeren. Zie [Logic apps als aanroepbare eindpunten](logic-apps-http-endpoint.md). Een logische app met een handmatige trigger maken en vervolgens genereren binnen de functie van een HTTP POST toohello handmatige trigger-URL met Hallo nettolading die u wilt toohello logische app verzonden.

### <a name="create-a-function-from-logic-app-designer"></a>Een functie maken vanuit Logic App-ontwerper

U kunt ook een node.js-webhook-functie maken vanuit Hallo designer. Selecteer eerst **Azure Functions in mijn regio** en kies vervolgens een container voor uw functie. Als u nog een container hebt, moet u toocreate van Hallo [Azure Functions-portal](https://functions.azure.com/signin). Selecteer vervolgens **nieuw**.  

een sjabloon op basis van Hallo gegevens die u toocompute wilt, toogenerate Geef Hallo context-object dat u van plan bent toopass in een functie. Dit object moet een JSON-object. Bijvoorbeeld, als u in Hallo bestandsinhoud van een FTP-actie doorgeeft, Hallo context nettolading ziet eruit als in dit voorbeeld:

![De nettolading van de context][2]

> [!NOTE]
> Omdat dit object is niet geconverteerd als een tekenreeks, wordt inhoud Hallo toegevoegd rechtstreeks toohello JSON-nettolading. Echter, treedt een fout als Hallo-object geen JSON-token is (dat wil zeggen, een tekenreeks of een JSON-object/array). toocast Hallo-object als een tekenreeks toevoegen aanhalingstekens in de eerste illustratie Hallo in dit artikel.
> 

Hallo designer genereert vervolgens een functie-sjabloon dat u inline kunt maken. Variabelen zijn vooraf gemaakt op basis van dat u van plan toopass in de functie Hallo bent Hallo-context.

<!--Image references-->
[1]: ./media/logic-apps-azure-functions/callfunction.png
[2]: ./media/logic-apps-azure-functions/createfunction.png
