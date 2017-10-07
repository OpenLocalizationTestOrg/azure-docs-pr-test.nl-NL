---
title: aaaScenario - Trigger logische apps met Azure Functions en Azure Service Bus | Microsoft Docs
description: Een functie tootrigger een logische app maken met behulp van Azure Functions en Azure Service Bus
services: logic-apps,functions
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 19cbd921-7071-4221-ab86-b44d0fc0ecef
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/23/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: a7b78ebcfe492eee2e08ceeae6b9c5f8ed4717bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scenario-trigger-a-logic-app-with-azure-functions-and-azure-service-bus"></a>Scenario: Een logische app met Azure Functions en Azure Service Bus activeren

Als u toodeploy een langlopende listener of taak nodig hebt, kunt u Azure Functions toocreate een trigger voor een logische app. U kunt bijvoorbeeld een functie die een wachtrij luistert maken en een logische app als een push-signaal wordt direct gestart.

## <a name="build-hello-logic-app"></a>Hallo logische app bouwen
In dit voorbeeld hebt u een functie die wordt uitgevoerd voor elke logische app, die toobe geactiveerd behoeften. Maak eerst een logische app, die een HTTP-verzoek-trigger heeft. Hallo-functie aanroepen dat eindpunt wanneer er een wachtrijbericht is ontvangen.  

1. Een logische app maken.
2. Selecteer Hallo **handmatig - wanneer er een HTTP-aanvraag wordt ontvangen** trigger.
   Desgewenst kunt u een JSON-schema toouse met wachtrij het Hallo-bericht met behulp van een hulpprogramma zoals [jsonschema.net](http://jsonschema.net). Hallo-schema in Hallo trigger te plakken. Schema's helpen bij het Hallo-designer Hallo vorm van gegevens en stroom eigenschappen Hallo gemakkelijker via Hallo workflow begrijpen.
2. Voeg eventuele extra stappen die u wilt toooccur nadat een wachtrijbericht is ontvangen. Bijvoorbeeld, sturen een e-mail via Office 365.  
3. Hallo logic app toogenerate Hallo callback URL voor Hallo trigger toothis logische app opslaan. Hallo-URL wordt weergegeven op Hallo trigger-kaart.

![Hallo-callback URL wordt weergegeven op Hallo trigger-kaart][1]

## <a name="build-hello-function"></a>Hallo-functie maken
Vervolgens moet u een functie die fungeert als Hallo trigger en luistert toohello wachtrij maken.

1. In Hallo [Azure Functions-portal](https://functions.azure.com/signin), selecteer **nieuwe functie**, en selecteer vervolgens Hallo **ServiceBusQueueTrigger - C#** sjabloon.
   
    ![Azure Functions-portal][2]
2. Hallo verbinding toohello Service Bus-wachtrij, die gebruikmaakt hello Azure Service Bus-SDK configureren `OnMessageReceive()` listener.
3. Schrijf een eenvoudige functie toocall Hallo logic app-eindpunt (eerder hebt gemaakt) met behulp van wachtrij het Hallo-bericht als een trigger. Hier volgt een voorbeeld van een volledige van een functie. Hallo-voorbeeld wordt een `application/json` inhoud berichttype, maar u kunt dit type zo nodig wijzigen.
   
   ```
   using System;
   using System.Threading.Tasks;
   using System.Net.Http;
   using System.Text;
   
   private static string logicAppUri = @"https://prod-05.westus.logic.azure.com:443/.........";
   
   public static void Run(string myQueueItem, TraceWriter log)
   {
   
       log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
       using (var client = new HttpClient())
       {
           var response = client.PostAsync(logicAppUri, new StringContent(myQueueItem, Encoding.UTF8, "application/json")).Result;
       }
   }
   ```

tootest, toevoegen van een wachtrijbericht via een hulpprogramma zoals [Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer). Zie Hallo logische app gestart onmiddellijk nadat de functie Hallo Hallo-bericht ontvangt.

<!-- Image References -->
[1]: ./media/logic-apps-scenario-function-sb-trigger/manualtrigger.png
[2]: ./media/logic-apps-scenario-function-sb-trigger/newqueuetriggerfunction.png
