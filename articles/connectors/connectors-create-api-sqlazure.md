---
title: aaaAdd hello Azure SQL Database-connector in uw logische Apps | Microsoft Docs
description: Overzicht van Azure SQL Database-connector met de parameters van de REST-API
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d8a319d0-e4df-40cf-88f0-29a6158c898c
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: a9ca0f446d05dc00f310a908eee8d50e41fcd82b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-azure-sql-database-connector"></a>Aan de slag met hello Azure SQL Database-connector
Maak met hello Azure SQL Database connector werkstromen voor uw organisatie die gegevens in de tabellen te beheren. 

Met SQL Database u:

* Uw werkstroom door het toevoegen van een nieuwe database van de klant tooa klanten of bijwerken van een order in een orderdatabase bouwen.
* Acties tooget een rij met gegevens gebruiken, een nieuwe rij invoegen en zelfs verwijderen. Bijvoorbeeld, wanneer een record in Dynamics CRM Online (een trigger) wordt gemaakt, klikt u vervolgens een rij invoegen in een Azure SQL Database (een actie). 

Dit onderwerp leest u hoe toouse SQL Database-connector in een logische app Hallo en ook een lijst met acties Hallo.

toolearn meer informatie over Logic Apps, Zie [wat zijn logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) en [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-tooazure-sql-database"></a>Verbinding maken met tooAzure SQL-Database
Om uw logische app toegang alle services tot, maakt u eerst een *verbinding* toohello service. Een verbinding biedt connectiviteit tussen een logische app en een andere service. Bijvoorbeeld: tooconnect tooSQL Database, u eerst een SQL-Database maken *verbinding*. toocreate een verbinding, u Hallo referenties die u normaal gesproken tooaccess Hallo service die u verbinding maakt. Dus in SQL-Database, voert u de verbinding met uw SQL Database referenties toocreate Hallo. 

#### <a name="create-hello-connection"></a>Hallo verbinding maken
> [!INCLUDE [Create hello connection tooSQL Azure](../../includes/connectors-create-api-sqlazure.md)]
> 
> 

## <a name="use-a-trigger"></a>Een trigger te gebruiken
Deze connector heeft geen triggers bestaan niet. Gebruik andere triggers toostart Hallo logische app, zoals een trigger terugkeerpatroon, een HTTP-Webhook-trigger, triggers beschikbaar met andere connectors en meer. [Een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md) bevat een voorbeeld.

## <a name="use-an-action"></a>Gebruik een actie
Een actie is een bewerking uitgevoerd door Hallo werkstroom gedefinieerd in een logische app. [Meer informatie over acties](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

1. Selecteer Hallo plus -teken. Ziet u verschillende mogelijkheden: **een actie toevoegen**, **een voorwaarde toevoegen**, of een van de Hallo **meer** opties.
   
    ![](./media/connectors-create-api-sqlazure/add-action.png)
2. Kies **een actie toevoegen**.
3. Typ in het tekstvak hello, 'sql' tooget een lijst met alle beschikbare Hallo-acties.
   
    ![](./media/connectors-create-api-sqlazure/sql-1.png) 
4. Kies in ons voorbeeld **SQL Server - Get-rij**. Als er al een verbinding bestaat, selecteert u Hallo **tabelnaam** in de vervolgkeuzelijst hello, en voert u Hallo **rij-ID** gewenste tooreturn.
   
    ![](./media/connectors-create-api-sqlazure/sample-table.png)
   
    Als u wordt gevraagd om de verbindingsgegevens hello, voert u Hallo details toocreate Hallo verbinding. [Hallo verbinding maken](connectors-create-api-sqlazure.md#create-the-connection) in dit onderwerp beschrijft deze eigenschappen. 
   
   > [!NOTE]
   > In dit voorbeeld wordt een rij uit een tabel retourneren. toosee hello gegevens in deze rij toevoegen een andere actie die u maakt een bestand met behulp van velden uit de tabel Hallo Hallo. Bijvoorbeeld, een OneDrive-actie die gebruikmaakt van Hallo FirstName en LastName velden toocreate een nieuw bestand in Hallo cloud storage-account toevoegen. 
   > 
   > 
5. **Sla** uw wijzigingen (linksboven Hallo werkbalk). Uw logische app wordt opgeslagen en automatisch kan worden ingeschakeld.

## <a name="connector-specific-details"></a>Connector-specifieke details

Alle triggers en acties die zijn gedefinieerd in swagger Hallo bekijken en ook bekijken in Hallo beperkingen [connector details](/connectors/sql/). 

## <a name="next-steps"></a>Volgende stappen
[Een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md). Verken Hallo van andere beschikbare connectors in Logic Apps op onze [API's lijst](apis-list.md).

