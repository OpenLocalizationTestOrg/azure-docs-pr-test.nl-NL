---
title: Azure Functions gebruiken voor het uitvoeren van een database opschoontaak | Microsoft Docs
description: Azure Functions gebruiken om een taak die is verbonden met Azure SQL Database periodiek opschonen van rijen.
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
ms.openlocfilehash: 6fd0e32374827b249f5aba1cbfc39117c88c6272
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-functions-to-connect-to-an-azure-sql-database"></a><span data-ttu-id="b4402-103">Azure Functions gebruiken voor verbinding met een Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="b4402-103">Use Azure Functions to connect to an Azure SQL Database</span></span>
<span data-ttu-id="b4402-104">Dit onderwerp leest u het gebruik van Azure Functions voor het maken van een geplande taak opruimen van rijen in een tabel in een Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="b4402-104">This topic shows you how to use Azure Functions to create a scheduled job that cleans up rows in a table in an Azure SQL Database.</span></span> <span data-ttu-id="b4402-105">De nieuwe C#-functie is gemaakt op basis van een vooraf gedefinieerde timer trigger-sjabloon in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="b4402-105">The new C# function is created based on a pre-defined timer trigger template in the Azure portal.</span></span> <span data-ttu-id="b4402-106">Ter ondersteuning van dit scenario, moet u ook een databaseverbindingsreeks instellen als een instelling in de functie-app.</span><span class="sxs-lookup"><span data-stu-id="b4402-106">To support this scenario, you must also set a database connection string as a setting in the function app.</span></span> <span data-ttu-id="b4402-107">Dit scenario maakt gebruik van een bulksgewijze bewerking op de database.</span><span class="sxs-lookup"><span data-stu-id="b4402-107">This scenario uses a bulk operation against the database.</span></span> <span data-ttu-id="b4402-108">Als u wilt laten verwerken afzonderlijke CRUD-bewerkingen in een tabel met Mobile Apps, moet u in plaats daarvan gebruiken [Mobile Apps-bindingen](functions-bindings-mobile-apps.md).</span><span class="sxs-lookup"><span data-stu-id="b4402-108">To have your function process individual CRUD operations in a Mobile Apps table, you should instead use [Mobile Apps bindings](functions-bindings-mobile-apps.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b4402-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b4402-109">Prerequisites</span></span>

+ <span data-ttu-id="b4402-110">In dit onderwerp wordt de timerfunctie van een geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="b4402-110">This topic uses a timer triggered function.</span></span> <span data-ttu-id="b4402-111">Voer de stappen in het onderwerp [maken van een functie in Azure die wordt geactiveerd door een timer](functions-create-scheduled-function.md) om een C#-versie van deze functie te maken.</span><span class="sxs-lookup"><span data-stu-id="b4402-111">Complete the steps in the topic [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md) to create a C# version of this function.</span></span>   

+ <span data-ttu-id="b4402-112">Dit onderwerp wordt beschreven voor een Transact-SQL-opdracht die wordt uitgevoerd een bulkbewerking opschoning in de **SalesOrderHeader** tabel in de voorbeelddatabase van AdventureWorksLT.</span><span class="sxs-lookup"><span data-stu-id="b4402-112">This topic demonstrates a Transact-SQL command that executes a bulk cleanup operation in the **SalesOrderHeader** table in the AdventureWorksLT sample database.</span></span> <span data-ttu-id="b4402-113">Voltooi de stappen in het onderwerp voor het maken van de voorbeelddatabase van AdventureWorksLT [maken van een Azure SQL database in de Azure portal](../sql-database/sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b4402-113">To create the AdventureWorksLT sample database, complete the steps in the topic [Create an Azure SQL database in the Azure portal](../sql-database/sql-database-get-started-portal.md).</span></span> 

## <a name="get-connection-information"></a><span data-ttu-id="b4402-114">Verbindingsgegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="b4402-114">Get connection information</span></span>

<span data-ttu-id="b4402-115">U moet de verbindingsreeks ophalen voor de database die u hebt gemaakt toen u voltooid [maken van een Azure SQL database in de Azure portal](../sql-database/sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b4402-115">You need to get the connection string for the database you created when you completed [Create an Azure SQL database in the Azure portal](../sql-database/sql-database-get-started-portal.md).</span></span>

1. <span data-ttu-id="b4402-116">Meld u aan bij [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b4402-116">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
 
3. <span data-ttu-id="b4402-117">Selecteer **SQL-Databases** uit in het menu links en selecteert u de database op de **SQL-databases** pagina.</span><span class="sxs-lookup"><span data-stu-id="b4402-117">Select **SQL Databases** from the left-hand menu, and select your database on the **SQL databases** page.</span></span>

4. <span data-ttu-id="b4402-118">Selecteer **databaseverbindingsreeksen tonen** en kopieer de volledige **ADO.NET** verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="b4402-118">Select **Show database connection strings** and copy the complete **ADO.NET** connection string.</span></span>

    ![Kopieer de ADO.NET-verbindingsreeks.](./media/functions-scenario-database-table-cleanup/adonet-connection-string.png)

## <a name="set-the-connection-string"></a><span data-ttu-id="b4402-120">De verbindingsreeks instellen</span><span class="sxs-lookup"><span data-stu-id="b4402-120">Set the connection string</span></span> 

<span data-ttu-id="b4402-121">Een functie-app fungeert als host voor de uitvoering van uw functies in Azure.</span><span class="sxs-lookup"><span data-stu-id="b4402-121">A function app hosts the execution of your functions in Azure.</span></span> <span data-ttu-id="b4402-122">Het is een best practice verbindingsreeksen en andere geheime informatie opgeslagen in de functie app-instellingen.</span><span class="sxs-lookup"><span data-stu-id="b4402-122">It is a best practice to store connection strings and other secrets in your function app settings.</span></span> <span data-ttu-id="b4402-123">Met de toepassingsinstellingen wordt voorkomen dat onbedoeld vrijgeven van de verbindingsreeks met uw code.</span><span class="sxs-lookup"><span data-stu-id="b4402-123">Using application settings prevents accidental disclosure of the connection string with your code.</span></span> 

1. <span data-ttu-id="b4402-124">Navigeer naar de functie-app die u hebt gemaakt [maken van een functie in Azure die wordt geactiveerd door een timer](functions-create-scheduled-function.md).</span><span class="sxs-lookup"><span data-stu-id="b4402-124">Navigate to your function app you created [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md).</span></span>

2. <span data-ttu-id="b4402-125">Selecteer **platformfuncties** > **toepassingsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="b4402-125">Select **Platform features** > **Application settings**.</span></span>
   
    ![Toepassingsinstellingen voor de functie-app.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings.png)

2. <span data-ttu-id="b4402-127">Schuif omlaag naar **verbindingsreeksen** en een verbindingsreeks met de instellingen die zijn opgegeven in de tabel toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b4402-127">Scroll down to **Connection strings** and add a connection string using the settings as specified in the table.</span></span>
   
    ![Een verbindingsreeks toevoegen aan de functie app-instellingen.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings-connection-strings.png)

    | <span data-ttu-id="b4402-129">Instelling</span><span class="sxs-lookup"><span data-stu-id="b4402-129">Setting</span></span>       | <span data-ttu-id="b4402-130">Voorgestelde waarde</span><span class="sxs-lookup"><span data-stu-id="b4402-130">Suggested value</span></span> | <span data-ttu-id="b4402-131">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b4402-131">Description</span></span>             | 
    | ------------ | ------------------ | --------------------- | 
    | <span data-ttu-id="b4402-132">**Naam**</span><span class="sxs-lookup"><span data-stu-id="b4402-132">**Name**</span></span>  |  <span data-ttu-id="b4402-133">sqldb_connection</span><span class="sxs-lookup"><span data-stu-id="b4402-133">sqldb_connection</span></span>  | <span data-ttu-id="b4402-134">Gebruikt voor toegang tot de opgeslagen verbindingsreeks in uw functiecode.</span><span class="sxs-lookup"><span data-stu-id="b4402-134">Used to access the stored connection string in your function code.</span></span>    |
    | <span data-ttu-id="b4402-135">**Waarde**</span><span class="sxs-lookup"><span data-stu-id="b4402-135">**Value**</span></span> | <span data-ttu-id="b4402-136">Gekopieerde tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b4402-136">Copied string</span></span>  | <span data-ttu-id="b4402-137">U hebt gekopieerd uit het verleden de verbindingsreeks in de vorige sectie.</span><span class="sxs-lookup"><span data-stu-id="b4402-137">Past the connection string you copied in the previous section.</span></span> |
    | <span data-ttu-id="b4402-138">**Type**</span><span class="sxs-lookup"><span data-stu-id="b4402-138">**Type**</span></span> | <span data-ttu-id="b4402-139">SQL Database</span><span class="sxs-lookup"><span data-stu-id="b4402-139">SQL Database</span></span> | <span data-ttu-id="b4402-140">De standaard SQL Database-verbinding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b4402-140">Use the default SQL Database connection.</span></span> |   

3. <span data-ttu-id="b4402-141">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b4402-141">Click **Save**.</span></span>

<span data-ttu-id="b4402-142">U kunt nu de C# functiecode die verbinding met uw SQL-Database maakt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b4402-142">Now, you can add the C# function code that connects to your SQL Database.</span></span>

## <a name="update-your-function-code"></a><span data-ttu-id="b4402-143">Werk uw functiecode</span><span class="sxs-lookup"><span data-stu-id="b4402-143">Update your function code</span></span>

1. <span data-ttu-id="b4402-144">In de functie-app, selecteert u de functie timer geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="b4402-144">In your function app, select the timer-triggered function.</span></span>
 
3. <span data-ttu-id="b4402-145">De volgende assemblyverwijzingen aan de bovenkant van de bestaande functiecode toevoegen:</span><span class="sxs-lookup"><span data-stu-id="b4402-145">Add the following assembly references at the top of the existing function code:</span></span>

    ```cs
    #r "System.Configuration"
    #r "System.Data"
    ```

3. <span data-ttu-id="b4402-146">Voeg de volgende `using` instructies voor de functie:</span><span class="sxs-lookup"><span data-stu-id="b4402-146">Add the following `using` statements to the function:</span></span>
    ```cs
    using System.Configuration;
    using System.Data.SqlClient;
    using System.Threading.Tasks;
    ```

4. <span data-ttu-id="b4402-147">Vervang de bestaande **uitvoeren** functie met de volgende code:</span><span class="sxs-lookup"><span data-stu-id="b4402-147">Replace the existing **Run** function with the following code:</span></span>
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
                // Execute the command and log the # rows affected.
                var rows = await cmd.ExecuteNonQueryAsync();
                log.Info($"{rows} rows were updated");
            }
        }
    }
    ```

    <span data-ttu-id="b4402-148">Bij deze voorbeeldopdracht updates de **Status** kolom op basis van de verzending.</span><span class="sxs-lookup"><span data-stu-id="b4402-148">This sample command updates the **Status** column based on the ship date.</span></span> <span data-ttu-id="b4402-149">Het moet 32 gegevensrijen bijwerken.</span><span class="sxs-lookup"><span data-stu-id="b4402-149">It should update 32 rows of data.</span></span>

5. <span data-ttu-id="b4402-150">Klik op **opslaan**, bekijk de **logboeken** windows voor de volgende functie uitvoering en noteer het aantal rijen bijgewerkt in de **SalesOrderHeader** tabel.</span><span class="sxs-lookup"><span data-stu-id="b4402-150">Click **Save**, watch the **Logs** windows for the next function execution, then note the number of rows updated in the **SalesOrderHeader** table.</span></span>

    ![Bekijk de logboeken van de functie.](./media/functions-scenario-database-table-cleanup/functions-logs.png)

## <a name="next-steps"></a><span data-ttu-id="b4402-152">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b4402-152">Next steps</span></span>

<span data-ttu-id="b4402-153">Vervolgens informatie over het gebruik van functies met Logic Apps om te integreren met andere services.</span><span class="sxs-lookup"><span data-stu-id="b4402-153">Next, learn how to use Functions with Logic Apps to integrate with other services.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="b4402-154">Maken van een functie die kan worden geïntegreerd met Logic Apps</span><span class="sxs-lookup"><span data-stu-id="b4402-154">Create a function that integrates with Logic Apps</span></span>](functions-twitter-email.md)

<span data-ttu-id="b4402-155">Zie de volgende onderwerpen voor meer informatie over functies:</span><span class="sxs-lookup"><span data-stu-id="b4402-155">For more information about Functions, see the following topics:</span></span>

* [<span data-ttu-id="b4402-156">Naslaginformatie over Azure Functions voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="b4402-156">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="b4402-157">Naslaginformatie voor programmeurs over het coderen van functies en het definiëren van triggers en bindingen.</span><span class="sxs-lookup"><span data-stu-id="b4402-157">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="b4402-158">Azure Functions testen</span><span class="sxs-lookup"><span data-stu-id="b4402-158">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="b4402-159">Beschrijft de verschillende hulpprogramma’s en technieken voor het testen van uw functies.</span><span class="sxs-lookup"><span data-stu-id="b4402-159">Describes various tools and techniques for testing your functions.</span></span>  
