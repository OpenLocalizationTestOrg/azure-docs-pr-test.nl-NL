---
title: aaaAdd Hallo-connector voor Oracle-Database in Azure Logic Apps | Microsoft Docs
description: Hallo-connector voor Oracle-Database in een logische app gebruiken
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: mandia; ladocs
ms.openlocfilehash: 8a802a6c4782e210ff71848614152cb46ba5d651
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-oracle-database-connector"></a>Aan de slag met Hallo Oracle-Database-connector

Hallo-connector voor Oracle-Database maakt, u organisatie werkstromen die gebruikmaken van gegevens in uw bestaande database. Deze connector kunt verbinden tooan lokale Oracle-Database of een Azure virtuele machine met Oracle-Database is geïnstalleerd. Met deze connector kunt u het volgende doen:

* Uw werkstroom door het toevoegen van een nieuwe database van de klant tooa klanten of bijwerken van een order in een orderdatabase bouwen.
* Acties tooget een rij met gegevens gebruiken, een nieuwe rij invoegen en zelfs verwijderen. Bijvoorbeeld, wanneer een record in Dynamics CRM Online (een trigger) wordt gemaakt, klikt u vervolgens een rij invoegen in een Oracle-Database (een actie). 

Dit onderwerp leest u hoe toouse Hallo Oracle-Database-connector in een logische app.

## <a name="prerequisites"></a>Vereisten

* Ondersteunde versies van Oracle: 
    * Oracle 9 en hoger
    * Oracle-clientsoftware 8.1.7 of hoger

* Hallo lokale gegevensgateway installeren. [Verbinding maken met tooon-premises gegevens vanuit logic apps](../logic-apps/logic-apps-gateway-connection.md) lijsten Hallo stappen. Hallo-gateway is vereist tooconnect tooan lokale Oracle-Database of een Azure-virtuele machine met Oracle DB geïnstalleerd. 

    > [!NOTE]
    > Hallo lokale gegevensgateway fungeert als een brug en biedt een veilige gegevensoverdracht tussen on-premises gegevens (gegevens die zich niet in de cloud Hallo) en uw logische apps. Hallo dezelfde gateway kan worden gebruikt met meerdere services en meerdere gegevensbronnen. Daarom moet u mogelijk alleen tooinstall Hallo gateway eenmaal.

* Hallo Oracle-Client installeren op Hallo-computer waarop u Hallo lokale gegevensgateway hebt geïnstalleerd. Zorg ervoor dat tooinstall hello 64-bits Oracle-gegevensprovider voor .NET van Oracle:  

  [64-bits ODAC 12c versie 4 (12.1.0.2.4) voor Windows x64](http://www.oracle.com/technetwork/database/windows/downloads/index-090165.html)

    > [!TIP]
    > Als Hallo Oracle-client niet is geïnstalleerd, wordt er een fout optreedt wanneer u toocreate probeert of Hallo verbinding gebruiken. Zie Hallo veelvoorkomende fouten in dit onderwerp.


## <a name="add-hello-connector"></a>Hallo connector toevoegen

> [!IMPORTANT]
> Deze connector heeft geen triggers bestaan niet. Alleen acties heeft. Dus bij het maken van uw logische app toevoegen een andere trigger toostart uw logische app, zoals **schema - terugkeerpatroon**, of **vraag / antwoord - antwoord**. 

1. In Hallo [Azure-portal](https://portal.azure.com), een lege logische app maken.

2. Bij Hallo begin van uw logische app, selecteer Hallo **vraag / antwoord - aanvraag** trigger: 

    ![](./media/connectors-create-api-oracledatabase/request-trigger.png)

3. Selecteer **Opslaan**. Wanneer u opslaat, wordt een aanvraag-URL wordt automatisch gegenereerd. 

4. Selecteer **nieuwe stap**, en selecteer **een actie toevoegen**. Typ in `oracle` toosee Hallo beschikbare acties: 

    ![](./media/connectors-create-api-oracledatabase/oracledb-actions.png)

    > [!TIP]
    > Dit is de snelste manier toosee Hallo Hallo triggers en acties die beschikbaar zijn voor elke connector. Typ in het deel van naam van de connector hello, zoals `oracle`. Hallo designer geeft een lijst van alle triggers en acties. 

5. Selecteer een van de Hallo acties, zoals **Oracle-Database - Get-rij**. Selecteer **verbinden via lokale gegevensgateway**. Voer Hallo Oracle-servernaam, verificatiemethode, gebruikersnaam, wachtwoord en selecteer Hallo gateway:

    ![](./media/connectors-create-api-oracledatabase/create-oracle-connection.png)

6. Eenmaal zijn verbonden, selecteer een tabel in de lijst Hallo en Voer Hallo rij-id-tooyour tabel. U moet tooknow Hallo id toohello tabel. Als u niet weet, contact op met uw beheerder Oracle DB en ophalen van de uitvoer van Hallo `select * from yourTableName`. Dit biedt u identificeerbare informatie die u nodig hebt tooproceed Hallo.

    In Hallo voorbeeld te volgen, taakgegevens uit een database Human Resources geretourneerd: 

    ![](./media/connectors-create-api-oracledatabase/table-rowid.png)

7. In deze stap, kunt u een van de Hallo andere toobuild connectors uw werkstroom. Als u wilt dat tootest ophalen van gegevens uit Oracle, verzend een e-mailbericht met Hallo Oracle-gegevens met een van de Hallo verzenden van e-connectors, zoals Office 365 of Gmail. Gebruik dynamische tokens van Hallo Oracle tabel toobuild Hallo Hallo `Subject` en `Body` van uw e-mailadres:

    ![](./media/connectors-create-api-oracledatabase/oracle-send-email.png)

8. **Sla** uw logische app en selecteer vervolgens **uitvoeren**. Hallo ontwerpen sluiten en bekijkt hello wordt uitgevoerd geschiedenis voor Hallo status. Als het mislukt, selecteert u Hallo mislukt bericht rij. Hallo designer wordt geopend en ziet u dat de stap is mislukt, en bevat informatie over de fout Hallo. Als dat lukt, ontvangt u een e-mail met Hallo-informatie die u hebt toegevoegd.


### <a name="workflow-ideas"></a>Werkstroom ideeën

* U wilt toomonitor hello #oracle hashtag en Hallo tweets in een database te plaatsen, zodat ze kunnen worden opgevraagd, en in andere toepassingen gebruikt. Voeg in een logische app, Hallo `Twitter - When a new tweet is posted` activeren en Voer Hallo **#oracle** hashtag. Vervolgens voegt u Hallo `Oracle Database - Insert row` actie, en selecteer de tabel:

    ![](./media/connectors-create-api-oracledatabase/twitter-oracledb.png)

* Berichten worden tooa Service Bus-wachtrij. U wilt dat deze berichten tooget en plaatsen in een database. Voeg in een logische app, Hallo `Service Bus - when a message is received in a queue` trigger en selecteer Hallo wachtrij. Vervolgens voegt u Hallo `Oracle Database - Insert row` actie, en selecteer de tabel:

    ![](./media/connectors-create-api-oracledatabase/sbqueue-oracledb.png)

## <a name="common-errors"></a>Veelvoorkomende fouten

#### <a name="error-cannot-reach-hello-gateway"></a>**Fout**: Hallo Gateway niet bereikbaar

**Oorzaak**: Hallo lokale gegevensgateway is niet kunnen tooconnect toohello cloud. 

**Risicobeperking**: Zorg ervoor dat uw gateway wordt uitgevoerd op Hallo on-premises machine waar u het hebt geïnstalleerd en dat deze verbinding kan maken van toohello internet.  U wordt aangeraden geen Hallo gateway installeren op een computer die kan worden uitgeschakeld of de slaapstand. U kunt ook Hallo lokale data gateway-service (PBIEgwService) opnieuw.

#### <a name="error-hello-provider-being-used-is-deprecated-systemdataoracleclient-requires-oracle-client-software-version-817-or-greater-please-visit-httpsgomicrosoftcomfwlinkplinkid272376httpsgomicrosoftcomfwlinkplinkid272376-tooinstall-hello-official-provider"></a>**Fout**: Hallo provider die wordt gebruikt is afgeschaft: ' voor System.Data.OracleClient is vereist voor Oracle-clientsoftware version 8.1.7 of hoger.'. Ga naar [https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) tooinstall Hallo officiële provider.

**Oorzaak**: Hallo Oracle-client SDK niet is geïnstalleerd op machine Hallo waar hello lokale gegevensgateway wordt uitgevoerd.  

**Resolutie**: downloaden en installeren van Hallo Oracle-client SDK op Hallo dezelfde computer als Hallo lokale gegevensgateway.

#### <a name="error-table-tablename-does-not-define-any-key-columns"></a>**Fout**: tabel [tabelnaam] geen alle sleutelkolommen gedefinieerd

**Oorzaak**: Hallo tabel heeft geen primaire sleutel.  

**Resolutie**: Hallo Oracle-Database connector vereist dat een tabel met een primaire sleutelkolom worden gebruikt.

#### <a name="currently-not-supported"></a>Momenteel ondersteund niet

* Weergaven en opgeslagen procedures 
* Een tabel met samengestelde sleutels
* Geneste objecttypen in tabellen
 
## <a name="connector-specific-details"></a>Connector-specifieke details

Alle triggers en acties die zijn gedefinieerd in swagger Hallo bekijken en ook bekijken in Hallo beperkingen [connector details](/connectors/oracle/). 

## <a name="get-some-help"></a>Hulp krijgen

Hallo [Azure Logic Apps-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) is uitermate plaatsen tooask vragen beantwoorden van vragen en zien wat anderen Logic Apps doen. 

U kunt logische Apps en connectors verbeteren door uw stem en verzenden van uw ideeën op [http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish). 


## <a name="next-steps"></a>Volgende stappen
[Een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md), en bekijk de beschikbare connectors Hallo in Logic Apps op onze [API's lijst](apis-list.md).
