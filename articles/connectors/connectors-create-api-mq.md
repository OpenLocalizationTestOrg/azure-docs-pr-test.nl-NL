---
title: aaaLearn hoe toouse Hallo MQ-connector in Azure Logic Apps | Microsoft Docs
description: Verbinding maken met tooan on-premises of Azure MQ server van uw logische app werkstroom toobrowse, ontvangen en verzenden van berichten tooWebSphere MQ
services: logic-apps
author: valthom
manager: anneta
documentationcenter: 
editor: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 06/01/2017
ms.author: valthom; ladocs
ms.openlocfilehash: 8b36d53b457ced1a7461c229aecfcf8e4ae668a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-ibm-mq-server-from-logic-apps-using-hello-mq-connector"></a>Verbinding maken met IBM MQ server tooan vanuit logic apps met behulp van Hallo MQ-connector 

Microsoft-Connector voor MQ verzendt en berichten die zijn opgeslagen in een MQ Server on-premises of in Azure ophaalt. Deze connector omvat een Microsoft-MQ-client die met een externe IBM MQ-server via een TCP/IP-netwerk communiceert. Dit document is een connector starter handleiding toouse Hallo MQ. Raden wij u beginnen door te bladeren door een enkel bericht in een wachtrij en probeert u het Hallo andere acties.    

Hallo MQ connector bevat Hallo van de volgende activiteiten. Er zijn geen triggers.

-   Een enkel bericht zonder te verwijderen van het Hallo-bericht van Hallo IBM MQ Server bladeren
-   Berichten batchgewijs zoeken zonder het Hallo-berichten verwijderen uit IBM MQ Server Hallo
-   Een enkel bericht ontvangen en het Hallo-bericht verwijderen uit IBM MQ Server Hallo
-   Ontvangen berichten batchgewijs en Hallo-berichten uit Hallo IBM MQ Server verwijderen
-   Een enkel bericht toohello IBM MQ Server verzenden 

## <a name="prerequisites"></a>Vereisten

* Als u een on-premises MQ server, [Hallo lokale gegevensgateway installeren](../logic-apps/logic-apps-gateway-install.md) op een server in uw netwerk. Als Hallo MQ Server openbaar beschikbaar is of beschikbaar is in Azure, vervolgens Hallo data gateway is niet gebruikt of nodig.

    > [!NOTE]
    > Hallo-server waar Hallo On-Premises Data Gateway is geïnstalleerd moet ook beschikken over .net Framework 4.6 voor Hallo MQ Connector toofunction geïnstalleerd.

* Maken van hello Azure-resource voor Hallo lokale gegevensgateway - [Hallo data gateway-verbinding instellen](../logic-apps/logic-apps-gateway-connection.md).

* IBM WebSphere MQ versies officieel ondersteund:
   * MQ 7.5
   * MQ 8.0

## <a name="create-a-logic-app"></a>Een logische app maken

1. In Hallo **Azure start board**, selecteer  **+**  (plusteken) **Web en mobiel**, en vervolgens **logische App**. 
2. Voer Hallo **naam**, zoals MQTestApp, **abonnement**, **resourcegroep**, en **locatie** (gebruik Hallo locatie waar hello lokale Data Gateway verbinding is geconfigureerd). Selecteer **pincode toodashboard**, en selecteer **maken**.  
![Logische App maken](media/connectors-create-api-mq/Create_Logic_App.png)

## <a name="add-a-trigger"></a>Een trigger toevoegen

> [!NOTE]
> Hallo MQ-Connector heeft geen geen triggers bestaan. Dus uw logische app, zoals hello gebruiken een ander trigger toostart **terugkeerpatroon** trigger. 

1. Hallo **Logic Apps Designer** wordt geopend, selecteer **terugkeerpatroon** in Hallo lijst met algemene triggers.
2. Selecteer **bewerken** binnen Hallo terugkeerpatroon Trigger. 
3. Set Hallo **frequentie** te**dag**, en set Hallo **Interval** te**7**. 

## <a name="browse-a-single-message"></a>Een enkel bericht bladeren
1. Selecteer **+ een nieuwe stap**, en selecteer **een actie toevoegen**.
2. Typ in het zoekvak Hallo `mq`, en selecteer vervolgens **MQ - bladeren bericht**.  
![Bericht bladeren](media/connectors-create-api-mq/Browse_message.png)

3. Als er geen een bestaande MQ-verbinding, klikt u vervolgens Hallo verbinding te maken:  

    1. Selecteer **verbinden via lokale gegevensgateway**, en Voer Hallo eigenschappen van uw server MQ.  
    Voor **Server**, Voer Hallo MQ-servernaam of Voer Hallo IP-adres, gevolgd door een dubbele punt en Hallo-poortnummer. 
    2. Hallo **gateway** dropdown geeft een lijst van de bestaande gatewayverbindingen die zijn geconfigureerd. Selecteer uw gateway.
    3. Selecteer **maken** na voltooiing. Uw verbinding lijkt vergelijkbare toohello volgende:   
    ![Verbindingseigenschappen](media/connectors-create-api-mq/Connection_Properties.png)

4. U kunt in de eigenschappen van Hallo actie:  

    * Gebruik Hallo **wachtrij** eigenschap tooaccess een andere wachtrijnaam heeft dan de waarde die is gedefinieerd in Hallo verbinding
    * Gebruik Hallo **MessageId**, **CorrelationId**, **GroupId**, en andere toobrowse eigenschappen voor een bericht op basis van verschillende MQ Hallo-berichteigenschappen
    * Stel **IncludeInfo** te**True** tooinclude extra berichtinformatie in Hallo uitvoer. Of stel deze in te**False** toonot aanvullend berichtinformatie opnemen in Hallo uitvoer.
    * Voer een **time-out** waarde toodetermine hoe lang toowait voor een tooarrive bericht in een lege wachtrij. Als er niets wordt opgegeven, eerste bericht in de wachtrij Hallo Hallo is opgehaald er is geen tijd besteed aan het wachten op een bericht tooappear.  
    ![Berichteigenschappen bladeren](media/connectors-create-api-mq/Browse_message_Props.png)

5. **Sla** uw wijzigingen en vervolgens **uitvoeren** uw logische app:  
![Opslaan en uitvoeren](media/connectors-create-api-mq/Save_Run.png)

6. Na enkele seconden Hallo stappen Hallo uitgevoerd worden weergegeven en kunt u Hallo uitvoer bekijkt. Selecteer Hallo groen vinkje toosee details van elke stap. Selecteer **Zie ruwe uitvoer** toosee meer informatie over het Hallo uitvoergegevens.  
![Bericht uitvoer bladeren](media/connectors-create-api-mq/Browse_message_output.png)  

    Onbewerkte uitvoer:  
    ![Bericht onbewerkte uitvoer bladeren](media/connectors-create-api-mq/Browse_message_raw_output.png)

7. Wanneer Hallo **IncludeInfo** optie tootrue is ingesteld, Hallo volgende uitvoer weergegeven:  
![Bladeren bericht bevatten info](media/connectors-create-api-mq/Browse_message_Include_Info.png)

## <a name="browse-multiple-messages"></a>Meerdere berichten bladeren
Hallo **berichten Bladeren** actie bevat een **BatchSize** optie tooindicate hoeveel berichten moeten worden geretourneerd uit de wachtrij Hallo.  Als **BatchSize** heeft geen vermelding alle berichten worden geretourneerd. Hallo geretourneerd uitvoer is een matrix van berichten.

1. Bij het toevoegen van Hallo **berichten Bladeren** actie eerste Hallo-verbinding die is geconfigureerd, is standaard geselecteerd. Selecteer **verbinding wijzigen** toocreate een nieuwe verbinding, of Selecteer een andere verbinding.

2. Hallo-uitvoer van bladeren berichten wordt weergegeven:  
![Berichten uitvoer bladeren](media/connectors-create-api-mq/Browse_messages_output.png)

## <a name="receive-a-single-message"></a>Een enkel bericht ontvangen
Hallo **ontvangen van berichten** actie heeft dezelfde in- en uitgangen als Hallo Hallo **bladeren bericht** in te grijpen. Wanneer u **ontvangen van berichten**, het Hallo-bericht is verwijderd uit de wachtrij Hallo.

## <a name="receive-multiple-messages"></a>Meerdere berichten ontvangen
Hallo **berichten ontvangen** actie heeft dezelfde in- en uitgangen als Hallo Hallo **berichten Bladeren** in te grijpen. Wanneer u **berichten ontvangen**, Hallo-berichten worden verwijderd uit de wachtrij Hallo.

Als er geen berichten in wachtrij Hallo zijn bij het uitvoeren van een bladeren of een ontvangen, wordt Hallo stap mislukt met de Hallo volgende uitvoer:  
![MQ Nee bericht fout](media/connectors-create-api-mq/MQ_No_Msg_Error.png)

## <a name="send-a-message"></a>Een bericht verzenden
1. Bij het toevoegen van Hallo **bericht verzenden** actie eerste Hallo-verbinding die is geconfigureerd, is standaard geselecteerd. Selecteer **verbinding wijzigen** toocreate een nieuwe verbinding, of Selecteer een andere verbinding. Hallo geldig **berichttypen** zijn **Datagram**, **antwoord**, of **aanvragen**.  
![Eigenschappen van bericht verzenden](media/connectors-create-api-mq/Send_Msg_Props.png)

2. Hallo uitvoer van een bericht verzenden ziet eruit als Hallo volgende:  
![De uitvoer bericht verzenden](media/connectors-create-api-mq/Send_Msg_Output.png)

## <a name="connector-specific-details"></a>Connector-specifieke details

Alle triggers en acties die zijn gedefinieerd in swagger Hallo bekijken en ook bekijken in Hallo beperkingen [connector details](/connectors/mq/).

## <a name="next-steps"></a>Volgende stappen
[Een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md). Verken Hallo van andere beschikbare connectors in Logic Apps op onze [API's lijst](apis-list.md).
