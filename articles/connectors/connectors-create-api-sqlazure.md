---
title: De Azure SQL Database-connector in uw logische Apps toevoegen | Microsoft Docs
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
ms.openlocfilehash: a3d5cb909dbfcb00f3fbfa0165bb6cd58eb18688
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-azure-sql-database-connector"></a><span data-ttu-id="6315f-103">Aan de slag met de Azure SQL Database-connector</span><span class="sxs-lookup"><span data-stu-id="6315f-103">Get started with the Azure SQL Database connector</span></span>
<span data-ttu-id="6315f-104">Met de Azure SQL Database-connector, werkstromen maken voor uw organisatie die gegevens in de tabellen te beheren.</span><span class="sxs-lookup"><span data-stu-id="6315f-104">Using the Azure SQL Database connector, create workflows for your organization that manage data in your tables.</span></span> 

<span data-ttu-id="6315f-105">Met SQL Database u:</span><span class="sxs-lookup"><span data-stu-id="6315f-105">With SQL Database, you:</span></span>

* <span data-ttu-id="6315f-106">Uw werkstroom door een nieuwe klant toe te voegen aan een database klanten of bijwerken van een order in een orderdatabase is opgebouwd.</span><span class="sxs-lookup"><span data-stu-id="6315f-106">Build your workflow by adding a new customer to a customers database, or updating an order in an orders database.</span></span>
* <span data-ttu-id="6315f-107">Acties voor een rij met gegevens ophalen, een nieuwe rij invoegen en verwijderen van zelfs gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6315f-107">Use actions to get a row of data, insert a new row, and even delete.</span></span> <span data-ttu-id="6315f-108">Bijvoorbeeld, wanneer een record in Dynamics CRM Online (een trigger) wordt gemaakt, klikt u vervolgens een rij invoegen in een Azure SQL Database (een actie).</span><span class="sxs-lookup"><span data-stu-id="6315f-108">For example,  when a record is created in Dynamics CRM Online (a trigger), then insert a row in an Azure SQL Database (an action).</span></span> 

<span data-ttu-id="6315f-109">In dit onderwerp leest u hoe voor het gebruik van de connector van de SQL-Database in een logische app, en vindt u ook de acties.</span><span class="sxs-lookup"><span data-stu-id="6315f-109">This topic shows you how to use the SQL Database connector in a logic app, and also lists the actions.</span></span>

<span data-ttu-id="6315f-110">Zie voor meer informatie over Logic Apps, [wat zijn logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) en [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="6315f-110">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-azure-sql-database"></a><span data-ttu-id="6315f-111">Verbinding maken met Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="6315f-111">Connect to Azure SQL Database</span></span>
<span data-ttu-id="6315f-112">Om uw logische app toegang alle services tot, maakt u eerst een *verbinding* naar de service.</span><span class="sxs-lookup"><span data-stu-id="6315f-112">Before your logic app can access any service, you first create a *connection* to the service.</span></span> <span data-ttu-id="6315f-113">Een verbinding biedt connectiviteit tussen een logische app en een andere service.</span><span class="sxs-lookup"><span data-stu-id="6315f-113">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="6315f-114">Bijvoorbeeld: voor verbinding met SQL-Database, u eerst een SQL-Database maken *verbinding*.</span><span class="sxs-lookup"><span data-stu-id="6315f-114">For example, to connect to SQL Database, you first create a SQL Database *connection*.</span></span> <span data-ttu-id="6315f-115">Een verbinding wilt maken, moet u de referenties die u gebruikt om toegang tot de service die u verbinding met maakt invoeren.</span><span class="sxs-lookup"><span data-stu-id="6315f-115">To create a connection, you enter the credentials you normally use to access the service you are connecting to.</span></span> <span data-ttu-id="6315f-116">Dus in SQL-Database, Voer uw referenties voor SQL-Database om de verbinding te maken.</span><span class="sxs-lookup"><span data-stu-id="6315f-116">So, in SQL Database, enter your SQL Database credentials to create the connection.</span></span> 

#### <a name="create-the-connection"></a><span data-ttu-id="6315f-117">De verbinding maken</span><span class="sxs-lookup"><span data-stu-id="6315f-117">Create the connection</span></span>
> [!INCLUDE [Create the connection to SQL Azure](../../includes/connectors-create-api-sqlazure.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="6315f-118">Een trigger te gebruiken</span><span class="sxs-lookup"><span data-stu-id="6315f-118">Use a trigger</span></span>
<span data-ttu-id="6315f-119">Deze connector heeft geen triggers bestaan niet.</span><span class="sxs-lookup"><span data-stu-id="6315f-119">This connector does not have any triggers.</span></span> <span data-ttu-id="6315f-120">Met andere triggers kunt starten van de logische app, zoals een trigger terugkeerpatroon, een HTTP-Webhook-trigger, triggers beschikbaar met andere connectors en meer.</span><span class="sxs-lookup"><span data-stu-id="6315f-120">Use other triggers to start the logic app, such as a Recurrence trigger, an HTTP Webhook trigger, triggers available with other connectors, and more.</span></span> <span data-ttu-id="6315f-121">[Een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md) bevat een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="6315f-121">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) provides an example.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="6315f-122">Gebruik een actie</span><span class="sxs-lookup"><span data-stu-id="6315f-122">Use an action</span></span>
<span data-ttu-id="6315f-123">Een actie is een bewerking uitgevoerd door de werkstroom die is gedefinieerd in een logische app.</span><span class="sxs-lookup"><span data-stu-id="6315f-123">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="6315f-124">[Meer informatie over acties](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="6315f-124">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="6315f-125">Selecteer het plusteken.</span><span class="sxs-lookup"><span data-stu-id="6315f-125">Select the plus sign.</span></span> <span data-ttu-id="6315f-126">Ziet u verschillende mogelijkheden: **een actie toevoegen**, **een voorwaarde toevoegen**, of een van de **meer** opties.</span><span class="sxs-lookup"><span data-stu-id="6315f-126">You see several choices: **Add an action**, **Add a condition**, or one of the **More** options.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/add-action.png)
2. <span data-ttu-id="6315f-127">Kies **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="6315f-127">Choose **Add an action**.</span></span>
3. <span data-ttu-id="6315f-128">Typ in het tekstvak 'sql' om een lijst met alle beschikbare acties.</span><span class="sxs-lookup"><span data-stu-id="6315f-128">In the text box, type “sql” to get a list of all the available actions.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/sql-1.png) 
4. <span data-ttu-id="6315f-129">Kies in ons voorbeeld **SQL Server - Get-rij**.</span><span class="sxs-lookup"><span data-stu-id="6315f-129">In our example, choose **SQL Server - Get row**.</span></span> <span data-ttu-id="6315f-130">Als er al een verbinding bestaat, selecteert u de **tabelnaam** in de vervolgkeuzelijst, en voert u de **rij-ID** u wilt retourneren.</span><span class="sxs-lookup"><span data-stu-id="6315f-130">If a connection already exists, then select the **Table name** from the drop-down list, and enter the **Row ID** you want to return.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/sample-table.png)
   
    <span data-ttu-id="6315f-131">Als u wordt gevraagd om de verbindingsinformatie, voert u de details om de verbinding te maken.</span><span class="sxs-lookup"><span data-stu-id="6315f-131">If you are prompted for the connection information, then enter the details to create the connection.</span></span> <span data-ttu-id="6315f-132">[De verbinding](connectors-create-api-sqlazure.md#create-the-connection) in dit onderwerp beschrijft deze eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="6315f-132">[Create the connection](connectors-create-api-sqlazure.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="6315f-133">In dit voorbeeld wordt een rij uit een tabel retourneren.</span><span class="sxs-lookup"><span data-stu-id="6315f-133">In this example, we return a row from a table.</span></span> <span data-ttu-id="6315f-134">De gegevens in deze rij, toe te voegen nog een actie die u maakt een bestand met de velden uit de tabel.</span><span class="sxs-lookup"><span data-stu-id="6315f-134">To see the data in this row, add another action that creates a file using the fields from the table.</span></span> <span data-ttu-id="6315f-135">Bijvoorbeeld, een OneDrive-actie die de voornaam en achternaam velden gebruikt voor het maken van een nieuw bestand in de cloud storage-account toevoegen.</span><span class="sxs-lookup"><span data-stu-id="6315f-135">For example, add a OneDrive action that uses the FirstName and LastName fields to create a new file in the cloud storage account.</span></span> 
   > 
   > 
5. <span data-ttu-id="6315f-136">**Sla** uw wijzigingen (linkerbovenhoek van de werkbalk).</span><span class="sxs-lookup"><span data-stu-id="6315f-136">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="6315f-137">Uw logische app wordt opgeslagen en automatisch kan worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="6315f-137">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="6315f-138">Connector-specifieke details</span><span class="sxs-lookup"><span data-stu-id="6315f-138">Connector-specific details</span></span>

<span data-ttu-id="6315f-139">Alle triggers en acties die zijn gedefinieerd in de swagger bekijken en ziet u ook de beperkingen in de [connector details](/connectors/sql/).</span><span class="sxs-lookup"><span data-stu-id="6315f-139">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/sql/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="6315f-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6315f-140">Next steps</span></span>
<span data-ttu-id="6315f-141">[Een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="6315f-141">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="6315f-142">Bekijk de beschikbare connectors in Logic Apps op onze [API's lijst](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="6315f-142">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

