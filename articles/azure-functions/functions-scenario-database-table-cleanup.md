---
title: Azure Functions-tooperform aaaUse een database opschonen taak | Microsoft Docs
description: Gebruik Azure Functions tooschedule een taak die is verbonden tooAzure SQL-Database tooperiodically opschonen van rijen.
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 076f5f95-f8d2-42c7-b7fd-6798856ba0bb
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/22/2017
ms.author: glenga
ms.openlocfilehash: 063a25fe8d14a75d54e9b72cec9fc1e25fa3ff44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-functions-tooconnect-tooan-azure-sql-database"></a>Azure Functions tooconnect tooan Azure SQL Database gebruiken
Dit onderwerp leest u hoe toouse Azure Functions toocreate een geplande taak ruimt rijen in een tabel in een Azure SQL Database. Hallo nieuwe C# functie is gemaakt op basis van een vooraf gedefinieerde timer trigger-sjabloon in hello Azure-portal. toosupport dit scenario moet u ook instellen een databaseverbindingsreeks als een instelling in Hallo functie-app. Dit scenario maakt gebruik van een bulksgewijze bewerking op Hallo-database. toohave uw functie proces afzonderlijke CRUD-bewerkingen in een tabel met Mobile Apps, moet u in plaats daarvan gebruiken [Mobile Apps-bindingen](functions-bindings-mobile-apps.md).

## <a name="prerequisites"></a>Vereisten

+ In dit onderwerp wordt de timerfunctie van een geactiveerd. Volledige Hallo stappen voor het Hallo-onderwerp [maken van een functie in Azure die wordt geactiveerd door een timer](functions-create-scheduled-function.md) toocreate een C#-versie van deze functie.   

+ Dit onderwerp wordt beschreven voor een Transact-SQL-opdracht die wordt uitgevoerd een opschonen bulkbewerking in Hallo **SalesOrderHeader** tabel in de voorbeelddatabase van AdventureWorksLT Hallo. toocreate hello AdventureWorksLT voorbeelddatabase stappen voor voltooid Hallo Hallo onderwerp [maken van een Azure SQL database in Azure-portal Hallo](../sql-database/sql-database-get-started-portal.md). 

## <a name="get-connection-information"></a>Verbindingsgegevens ophalen

U moet tooget Hallo-verbindingsreeks voor Hallo-database die u hebt gemaakt toen u voltooid [maken van een Azure SQL database in Azure-portal Hallo](../sql-database/sql-database-get-started-portal.md).

1. Meld u bij toohello [Azure-portal](https://portal.azure.com/).
 
3. Selecteer **SQL-Databases** Hallo links menu en selecteer de database op Hallo **SQL-databases** pagina.

4. Selecteer **databaseverbindingsreeksen tonen** en kopiëren Hallo voltooid **ADO.NET** verbindingsreeks.

    ![Kopieer Hallo ADO.NET-verbindingsreeks.](./media/functions-scenario-database-table-cleanup/adonet-connection-string.png)

## <a name="set-hello-connection-string"></a>Hallo-verbindingsreeks instellen 

Hallo-uitvoering van uw functies in Azure als host fungeert voor een functie-app. Het is een best practice toostore verbindingsreeksen en andere geheimen in de functie app-instellingen. Met de toepassingsinstellingen wordt voorkomen dat onbedoeld vrijgeven van de verbindingsreeks Hallo met uw code. 

1. Navigeer tooyour functie-app u hebt gemaakt [maken van een functie in Azure die wordt geactiveerd door een timer](functions-create-scheduled-function.md).

2. Selecteer **platformfuncties** > **toepassingsinstellingen**.
   
    ![Toepassingsinstellingen voor Hallo functie-app.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings.png)

2. Schuif naar beneden te**verbindingsreeksen** en een verbindingsreeks met Hallo-instellingen zoals opgegeven in de tabel Hallo toevoegen.
   
    ![Voeg een verbinding tekenreeks toohello functie app-instellingen.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings-connection-strings.png)

    | Instelling       | Voorgestelde waarde | Beschrijving             | 
    | ------------ | ------------------ | --------------------- | 
    | **Naam**  |  sqldb_connection  | Verbindingsreeks gebruikte tooaccess Hallo opgeslagen in uw functiecode.    |
    | **Waarde** | Gekopieerde tekenreeks  | U hebt gekopieerd in de vorige sectie Hallo Hallo-verbindingsreeks uit het verleden. |
    | **Type** | SQL Database | Hallo standaard SQL Database-verbinding gebruiken. |   

3. Klik op **Opslaan**.

U kunt nu Hallo C# functiecode die verbinding tooyour SQL-Database maakt toevoegen.

## <a name="update-your-function-code"></a>Werk uw functiecode

1. Selecteer in uw app functie Hallo timer geactiveerd functie.
 
3. Hallo assembly-verwijzingen Hallo boven aan de bestaande functiecode Hallo volgende toevoegen:

    ```cs
    #r "System.Configuration"
    #r "System.Data"
    ```

3. Voeg de volgende Hallo `using` instructies toohello functie:
    ```cs
    using System.Configuration;
    using System.Data.SqlClient;
    using System.Threading.Tasks;
    ```

4. Hallo bestaande **uitvoeren** functie hello code te volgen:
    ```cs
    public static async Task Run(TimerInfo myTimer, TraceWriter log)
    {
        var str = ConfigurationManager.ConnectionStrings["sqldb_connection"].ConnectionString;
        using (SqlConnection conn = new SqlConnection(str))
        {
            conn.Open();
            var text = "UPDATE SalesLT.SalesOrderHeader " + 
                    "SET [Status] = 5  WHERE ShipDate < GetDate();";

            using (SqlCommand cmd = new SqlCommand(text, conn))
            {
                // Execute hello command and log hello # rows affected.
                var rows = await cmd.ExecuteNonQueryAsync();
                log.Info($"{rows} rows were updated");
            }
        }
    }
    ```

    Bij deze voorbeeldopdracht updates Hallo **Status** kolom op basis van Hallo verzenddatum. Het moet 32 gegevensrijen bijwerken.

5. Klik op **opslaan**, bekijk Hallo **logboeken** windows voor Hallo naast functie uitvoeren en vervolgens Let op het aantal rijen bijgewerkt in Hallo Hallo **SalesOrderHeader** tabel.

    ![Hallo functie Logboeken bekijken.](./media/functions-scenario-database-table-cleanup/functions-logs.png)

## <a name="next-steps"></a>Volgende stappen

Vervolgens leert u hoe toouse functioneert met Logic Apps toointegrate met andere services.

> [!div class="nextstepaction"] 
> [Maken van een functie die kan worden geïntegreerd met Logic Apps](functions-twitter-email.md)

Zie voor meer informatie over functies Hallo volgende onderwerpen:

* [Naslaginformatie over Azure Functions voor ontwikkelaars](functions-reference.md)  
  Naslaginformatie voor programmeurs over het coderen van functies en het definiëren van triggers en bindingen.
* [Azure Functions testen](functions-test-a-function.md)  
  Beschrijft de verschillende hulpprogramma’s en technieken voor het testen van uw functies.  
