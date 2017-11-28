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
# <a name="use-azure-functions-tooconnect-tooan-azure-sql-database"></a><span data-ttu-id="7945d-103">Azure Functions tooconnect tooan Azure SQL Database gebruiken</span><span class="sxs-lookup"><span data-stu-id="7945d-103">Use Azure Functions tooconnect tooan Azure SQL Database</span></span>
<span data-ttu-id="7945d-104">Dit onderwerp leest u hoe toouse Azure Functions toocreate een geplande taak ruimt rijen in een tabel in een Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="7945d-104">This topic shows you how toouse Azure Functions toocreate a scheduled job that cleans up rows in a table in an Azure SQL Database.</span></span> <span data-ttu-id="7945d-105">Hallo nieuwe C# functie is gemaakt op basis van een vooraf gedefinieerde timer trigger-sjabloon in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="7945d-105">hello new C# function is created based on a pre-defined timer trigger template in hello Azure portal.</span></span> <span data-ttu-id="7945d-106">toosupport dit scenario moet u ook instellen een databaseverbindingsreeks als een instelling in Hallo functie-app.</span><span class="sxs-lookup"><span data-stu-id="7945d-106">toosupport this scenario, you must also set a database connection string as a setting in hello function app.</span></span> <span data-ttu-id="7945d-107">Dit scenario maakt gebruik van een bulksgewijze bewerking op Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="7945d-107">This scenario uses a bulk operation against hello database.</span></span> <span data-ttu-id="7945d-108">toohave uw functie proces afzonderlijke CRUD-bewerkingen in een tabel met Mobile Apps, moet u in plaats daarvan gebruiken [Mobile Apps-bindingen](functions-bindings-mobile-apps.md).</span><span class="sxs-lookup"><span data-stu-id="7945d-108">toohave your function process individual CRUD operations in a Mobile Apps table, you should instead use [Mobile Apps bindings](functions-bindings-mobile-apps.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7945d-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7945d-109">Prerequisites</span></span>

+ <span data-ttu-id="7945d-110">In dit onderwerp wordt de timerfunctie van een geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="7945d-110">This topic uses a timer triggered function.</span></span> <span data-ttu-id="7945d-111">Volledige Hallo stappen voor het Hallo-onderwerp [maken van een functie in Azure die wordt geactiveerd door een timer](functions-create-scheduled-function.md) toocreate een C#-versie van deze functie.</span><span class="sxs-lookup"><span data-stu-id="7945d-111">Complete hello steps in hello topic [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md) toocreate a C# version of this function.</span></span>   

+ <span data-ttu-id="7945d-112">Dit onderwerp wordt beschreven voor een Transact-SQL-opdracht die wordt uitgevoerd een opschonen bulkbewerking in Hallo **SalesOrderHeader** tabel in de voorbeelddatabase van AdventureWorksLT Hallo.</span><span class="sxs-lookup"><span data-stu-id="7945d-112">This topic demonstrates a Transact-SQL command that executes a bulk cleanup operation in hello **SalesOrderHeader** table in hello AdventureWorksLT sample database.</span></span> <span data-ttu-id="7945d-113">toocreate hello AdventureWorksLT voorbeelddatabase stappen voor voltooid Hallo Hallo onderwerp [maken van een Azure SQL database in Azure-portal Hallo](../sql-database/sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7945d-113">toocreate hello AdventureWorksLT sample database, complete hello steps in hello topic [Create an Azure SQL database in hello Azure portal](../sql-database/sql-database-get-started-portal.md).</span></span> 

## <a name="get-connection-information"></a><span data-ttu-id="7945d-114">Verbindingsgegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="7945d-114">Get connection information</span></span>

<span data-ttu-id="7945d-115">U moet tooget Hallo-verbindingsreeks voor Hallo-database die u hebt gemaakt toen u voltooid [maken van een Azure SQL database in Azure-portal Hallo](../sql-database/sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7945d-115">You need tooget hello connection string for hello database you created when you completed [Create an Azure SQL database in hello Azure portal](../sql-database/sql-database-get-started-portal.md).</span></span>

1. <span data-ttu-id="7945d-116">Meld u bij toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="7945d-116">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
 
3. <span data-ttu-id="7945d-117">Selecteer **SQL-Databases** Hallo links menu en selecteer de database op Hallo **SQL-databases** pagina.</span><span class="sxs-lookup"><span data-stu-id="7945d-117">Select **SQL Databases** from hello left-hand menu, and select your database on hello **SQL databases** page.</span></span>

4. <span data-ttu-id="7945d-118">Selecteer **databaseverbindingsreeksen tonen** en kopiëren Hallo voltooid **ADO.NET** verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="7945d-118">Select **Show database connection strings** and copy hello complete **ADO.NET** connection string.</span></span>

    ![Kopieer Hallo ADO.NET-verbindingsreeks.](./media/functions-scenario-database-table-cleanup/adonet-connection-string.png)

## <a name="set-hello-connection-string"></a><span data-ttu-id="7945d-120">Hallo-verbindingsreeks instellen</span><span class="sxs-lookup"><span data-stu-id="7945d-120">Set hello connection string</span></span> 

<span data-ttu-id="7945d-121">Hallo-uitvoering van uw functies in Azure als host fungeert voor een functie-app.</span><span class="sxs-lookup"><span data-stu-id="7945d-121">A function app hosts hello execution of your functions in Azure.</span></span> <span data-ttu-id="7945d-122">Het is een best practice toostore verbindingsreeksen en andere geheimen in de functie app-instellingen.</span><span class="sxs-lookup"><span data-stu-id="7945d-122">It is a best practice toostore connection strings and other secrets in your function app settings.</span></span> <span data-ttu-id="7945d-123">Met de toepassingsinstellingen wordt voorkomen dat onbedoeld vrijgeven van de verbindingsreeks Hallo met uw code.</span><span class="sxs-lookup"><span data-stu-id="7945d-123">Using application settings prevents accidental disclosure of hello connection string with your code.</span></span> 

1. <span data-ttu-id="7945d-124">Navigeer tooyour functie-app u hebt gemaakt [maken van een functie in Azure die wordt geactiveerd door een timer](functions-create-scheduled-function.md).</span><span class="sxs-lookup"><span data-stu-id="7945d-124">Navigate tooyour function app you created [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md).</span></span>

2. <span data-ttu-id="7945d-125">Selecteer **platformfuncties** > **toepassingsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="7945d-125">Select **Platform features** > **Application settings**.</span></span>
   
    ![Toepassingsinstellingen voor Hallo functie-app.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings.png)

2. <span data-ttu-id="7945d-127">Schuif naar beneden te**verbindingsreeksen** en een verbindingsreeks met Hallo-instellingen zoals opgegeven in de tabel Hallo toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7945d-127">Scroll down too**Connection strings** and add a connection string using hello settings as specified in hello table.</span></span>
   
    ![Voeg een verbinding tekenreeks toohello functie app-instellingen.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings-connection-strings.png)

    | <span data-ttu-id="7945d-129">Instelling</span><span class="sxs-lookup"><span data-stu-id="7945d-129">Setting</span></span>       | <span data-ttu-id="7945d-130">Voorgestelde waarde</span><span class="sxs-lookup"><span data-stu-id="7945d-130">Suggested value</span></span> | <span data-ttu-id="7945d-131">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="7945d-131">Description</span></span>             | 
    | ------------ | ------------------ | --------------------- | 
    | <span data-ttu-id="7945d-132">**Naam**</span><span class="sxs-lookup"><span data-stu-id="7945d-132">**Name**</span></span>  |  <span data-ttu-id="7945d-133">sqldb_connection</span><span class="sxs-lookup"><span data-stu-id="7945d-133">sqldb_connection</span></span>  | <span data-ttu-id="7945d-134">Verbindingsreeks gebruikte tooaccess Hallo opgeslagen in uw functiecode.</span><span class="sxs-lookup"><span data-stu-id="7945d-134">Used tooaccess hello stored connection string in your function code.</span></span>    |
    | <span data-ttu-id="7945d-135">**Waarde**</span><span class="sxs-lookup"><span data-stu-id="7945d-135">**Value**</span></span> | <span data-ttu-id="7945d-136">Gekopieerde tekenreeks</span><span class="sxs-lookup"><span data-stu-id="7945d-136">Copied string</span></span>  | <span data-ttu-id="7945d-137">U hebt gekopieerd in de vorige sectie Hallo Hallo-verbindingsreeks uit het verleden.</span><span class="sxs-lookup"><span data-stu-id="7945d-137">Past hello connection string you copied in hello previous section.</span></span> |
    | <span data-ttu-id="7945d-138">**Type**</span><span class="sxs-lookup"><span data-stu-id="7945d-138">**Type**</span></span> | <span data-ttu-id="7945d-139">SQL Database</span><span class="sxs-lookup"><span data-stu-id="7945d-139">SQL Database</span></span> | <span data-ttu-id="7945d-140">Hallo standaard SQL Database-verbinding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7945d-140">Use hello default SQL Database connection.</span></span> |   

3. <span data-ttu-id="7945d-141">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="7945d-141">Click **Save**.</span></span>

<span data-ttu-id="7945d-142">U kunt nu Hallo C# functiecode die verbinding tooyour SQL-Database maakt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7945d-142">Now, you can add hello C# function code that connects tooyour SQL Database.</span></span>

## <a name="update-your-function-code"></a><span data-ttu-id="7945d-143">Werk uw functiecode</span><span class="sxs-lookup"><span data-stu-id="7945d-143">Update your function code</span></span>

1. <span data-ttu-id="7945d-144">Selecteer in uw app functie Hallo timer geactiveerd functie.</span><span class="sxs-lookup"><span data-stu-id="7945d-144">In your function app, select hello timer-triggered function.</span></span>
 
3. <span data-ttu-id="7945d-145">Hallo assembly-verwijzingen Hallo boven aan de bestaande functiecode Hallo volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="7945d-145">Add hello following assembly references at hello top of hello existing function code:</span></span>

    ```cs
    #r "System.Configuration"
    #r "System.Data"
    ```

3. <span data-ttu-id="7945d-146">Voeg de volgende Hallo `using` instructies toohello functie:</span><span class="sxs-lookup"><span data-stu-id="7945d-146">Add hello following `using` statements toohello function:</span></span>
    ```cs
    using System.Configuration;
    using System.Data.SqlClient;
    using System.Threading.Tasks;
    ```

4. <span data-ttu-id="7945d-147">Hallo bestaande **uitvoeren** functie hello code te volgen:</span><span class="sxs-lookup"><span data-stu-id="7945d-147">Replace hello existing **Run** function with hello following code:</span></span>
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

    <span data-ttu-id="7945d-148">Bij deze voorbeeldopdracht updates Hallo **Status** kolom op basis van Hallo verzenddatum.</span><span class="sxs-lookup"><span data-stu-id="7945d-148">This sample command updates hello **Status** column based on hello ship date.</span></span> <span data-ttu-id="7945d-149">Het moet 32 gegevensrijen bijwerken.</span><span class="sxs-lookup"><span data-stu-id="7945d-149">It should update 32 rows of data.</span></span>

5. <span data-ttu-id="7945d-150">Klik op **opslaan**, bekijk Hallo **logboeken** windows voor Hallo naast functie uitvoeren en vervolgens Let op het aantal rijen bijgewerkt in Hallo Hallo **SalesOrderHeader** tabel.</span><span class="sxs-lookup"><span data-stu-id="7945d-150">Click **Save**, watch hello **Logs** windows for hello next function execution, then note hello number of rows updated in hello **SalesOrderHeader** table.</span></span>

    ![Hallo functie Logboeken bekijken.](./media/functions-scenario-database-table-cleanup/functions-logs.png)

## <a name="next-steps"></a><span data-ttu-id="7945d-152">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7945d-152">Next steps</span></span>

<span data-ttu-id="7945d-153">Vervolgens leert u hoe toouse functioneert met Logic Apps toointegrate met andere services.</span><span class="sxs-lookup"><span data-stu-id="7945d-153">Next, learn how toouse Functions with Logic Apps toointegrate with other services.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="7945d-154">Maken van een functie die kan worden geïntegreerd met Logic Apps</span><span class="sxs-lookup"><span data-stu-id="7945d-154">Create a function that integrates with Logic Apps</span></span>](functions-twitter-email.md)

<span data-ttu-id="7945d-155">Zie voor meer informatie over functies Hallo volgende onderwerpen:</span><span class="sxs-lookup"><span data-stu-id="7945d-155">For more information about Functions, see hello following topics:</span></span>

* [<span data-ttu-id="7945d-156">Naslaginformatie over Azure Functions voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="7945d-156">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="7945d-157">Naslaginformatie voor programmeurs over het coderen van functies en het definiëren van triggers en bindingen.</span><span class="sxs-lookup"><span data-stu-id="7945d-157">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="7945d-158">Azure Functions testen</span><span class="sxs-lookup"><span data-stu-id="7945d-158">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="7945d-159">Beschrijft de verschillende hulpprogramma’s en technieken voor het testen van uw functies.</span><span class="sxs-lookup"><span data-stu-id="7945d-159">Describes various tools and techniques for testing your functions.</span></span>  
