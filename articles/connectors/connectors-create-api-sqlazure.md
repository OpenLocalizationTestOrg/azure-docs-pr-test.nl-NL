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
# <a name="get-started-with-hello-azure-sql-database-connector"></a><span data-ttu-id="8434a-103">Aan de slag met hello Azure SQL Database-connector</span><span class="sxs-lookup"><span data-stu-id="8434a-103">Get started with hello Azure SQL Database connector</span></span>
<span data-ttu-id="8434a-104">Maak met hello Azure SQL Database connector werkstromen voor uw organisatie die gegevens in de tabellen te beheren.</span><span class="sxs-lookup"><span data-stu-id="8434a-104">Using hello Azure SQL Database connector, create workflows for your organization that manage data in your tables.</span></span> 

<span data-ttu-id="8434a-105">Met SQL Database u:</span><span class="sxs-lookup"><span data-stu-id="8434a-105">With SQL Database, you:</span></span>

* <span data-ttu-id="8434a-106">Uw werkstroom door het toevoegen van een nieuwe database van de klant tooa klanten of bijwerken van een order in een orderdatabase bouwen.</span><span class="sxs-lookup"><span data-stu-id="8434a-106">Build your workflow by adding a new customer tooa customers database, or updating an order in an orders database.</span></span>
* <span data-ttu-id="8434a-107">Acties tooget een rij met gegevens gebruiken, een nieuwe rij invoegen en zelfs verwijderen.</span><span class="sxs-lookup"><span data-stu-id="8434a-107">Use actions tooget a row of data, insert a new row, and even delete.</span></span> <span data-ttu-id="8434a-108">Bijvoorbeeld, wanneer een record in Dynamics CRM Online (een trigger) wordt gemaakt, klikt u vervolgens een rij invoegen in een Azure SQL Database (een actie).</span><span class="sxs-lookup"><span data-stu-id="8434a-108">For example,  when a record is created in Dynamics CRM Online (a trigger), then insert a row in an Azure SQL Database (an action).</span></span> 

<span data-ttu-id="8434a-109">Dit onderwerp leest u hoe toouse SQL Database-connector in een logische app Hallo en ook een lijst met acties Hallo.</span><span class="sxs-lookup"><span data-stu-id="8434a-109">This topic shows you how toouse hello SQL Database connector in a logic app, and also lists hello actions.</span></span>

<span data-ttu-id="8434a-110">toolearn meer informatie over Logic Apps, Zie [wat zijn logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) en [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="8434a-110">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooazure-sql-database"></a><span data-ttu-id="8434a-111">Verbinding maken met tooAzure SQL-Database</span><span class="sxs-lookup"><span data-stu-id="8434a-111">Connect tooAzure SQL Database</span></span>
<span data-ttu-id="8434a-112">Om uw logische app toegang alle services tot, maakt u eerst een *verbinding* toohello service.</span><span class="sxs-lookup"><span data-stu-id="8434a-112">Before your logic app can access any service, you first create a *connection* toohello service.</span></span> <span data-ttu-id="8434a-113">Een verbinding biedt connectiviteit tussen een logische app en een andere service.</span><span class="sxs-lookup"><span data-stu-id="8434a-113">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="8434a-114">Bijvoorbeeld: tooconnect tooSQL Database, u eerst een SQL-Database maken *verbinding*.</span><span class="sxs-lookup"><span data-stu-id="8434a-114">For example, tooconnect tooSQL Database, you first create a SQL Database *connection*.</span></span> <span data-ttu-id="8434a-115">toocreate een verbinding, u Hallo referenties die u normaal gesproken tooaccess Hallo service die u verbinding maakt.</span><span class="sxs-lookup"><span data-stu-id="8434a-115">toocreate a connection, you enter hello credentials you normally use tooaccess hello service you are connecting to.</span></span> <span data-ttu-id="8434a-116">Dus in SQL-Database, voert u de verbinding met uw SQL Database referenties toocreate Hallo.</span><span class="sxs-lookup"><span data-stu-id="8434a-116">So, in SQL Database, enter your SQL Database credentials toocreate hello connection.</span></span> 

#### <a name="create-hello-connection"></a><span data-ttu-id="8434a-117">Hallo verbinding maken</span><span class="sxs-lookup"><span data-stu-id="8434a-117">Create hello connection</span></span>
> [!INCLUDE [Create hello connection tooSQL Azure](../../includes/connectors-create-api-sqlazure.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="8434a-118">Een trigger te gebruiken</span><span class="sxs-lookup"><span data-stu-id="8434a-118">Use a trigger</span></span>
<span data-ttu-id="8434a-119">Deze connector heeft geen triggers bestaan niet.</span><span class="sxs-lookup"><span data-stu-id="8434a-119">This connector does not have any triggers.</span></span> <span data-ttu-id="8434a-120">Gebruik andere triggers toostart Hallo logische app, zoals een trigger terugkeerpatroon, een HTTP-Webhook-trigger, triggers beschikbaar met andere connectors en meer.</span><span class="sxs-lookup"><span data-stu-id="8434a-120">Use other triggers toostart hello logic app, such as a Recurrence trigger, an HTTP Webhook trigger, triggers available with other connectors, and more.</span></span> <span data-ttu-id="8434a-121">[Een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md) bevat een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="8434a-121">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) provides an example.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="8434a-122">Gebruik een actie</span><span class="sxs-lookup"><span data-stu-id="8434a-122">Use an action</span></span>
<span data-ttu-id="8434a-123">Een actie is een bewerking uitgevoerd door Hallo werkstroom gedefinieerd in een logische app.</span><span class="sxs-lookup"><span data-stu-id="8434a-123">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="8434a-124">[Meer informatie over acties](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="8434a-124">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="8434a-125">Selecteer Hallo plus -teken.</span><span class="sxs-lookup"><span data-stu-id="8434a-125">Select hello plus sign.</span></span> <span data-ttu-id="8434a-126">Ziet u verschillende mogelijkheden: **een actie toevoegen**, **een voorwaarde toevoegen**, of een van de Hallo **meer** opties.</span><span class="sxs-lookup"><span data-stu-id="8434a-126">You see several choices: **Add an action**, **Add a condition**, or one of hello **More** options.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/add-action.png)
2. <span data-ttu-id="8434a-127">Kies **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="8434a-127">Choose **Add an action**.</span></span>
3. <span data-ttu-id="8434a-128">Typ in het tekstvak hello, 'sql' tooget een lijst met alle beschikbare Hallo-acties.</span><span class="sxs-lookup"><span data-stu-id="8434a-128">In hello text box, type “sql” tooget a list of all hello available actions.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/sql-1.png) 
4. <span data-ttu-id="8434a-129">Kies in ons voorbeeld **SQL Server - Get-rij**.</span><span class="sxs-lookup"><span data-stu-id="8434a-129">In our example, choose **SQL Server - Get row**.</span></span> <span data-ttu-id="8434a-130">Als er al een verbinding bestaat, selecteert u Hallo **tabelnaam** in de vervolgkeuzelijst hello, en voert u Hallo **rij-ID** gewenste tooreturn.</span><span class="sxs-lookup"><span data-stu-id="8434a-130">If a connection already exists, then select hello **Table name** from hello drop-down list, and enter hello **Row ID** you want tooreturn.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/sample-table.png)
   
    <span data-ttu-id="8434a-131">Als u wordt gevraagd om de verbindingsgegevens hello, voert u Hallo details toocreate Hallo verbinding.</span><span class="sxs-lookup"><span data-stu-id="8434a-131">If you are prompted for hello connection information, then enter hello details toocreate hello connection.</span></span> <span data-ttu-id="8434a-132">[Hallo verbinding maken](connectors-create-api-sqlazure.md#create-the-connection) in dit onderwerp beschrijft deze eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="8434a-132">[Create hello connection](connectors-create-api-sqlazure.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="8434a-133">In dit voorbeeld wordt een rij uit een tabel retourneren.</span><span class="sxs-lookup"><span data-stu-id="8434a-133">In this example, we return a row from a table.</span></span> <span data-ttu-id="8434a-134">toosee hello gegevens in deze rij toevoegen een andere actie die u maakt een bestand met behulp van velden uit de tabel Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="8434a-134">toosee hello data in this row, add another action that creates a file using hello fields from hello table.</span></span> <span data-ttu-id="8434a-135">Bijvoorbeeld, een OneDrive-actie die gebruikmaakt van Hallo FirstName en LastName velden toocreate een nieuw bestand in Hallo cloud storage-account toevoegen.</span><span class="sxs-lookup"><span data-stu-id="8434a-135">For example, add a OneDrive action that uses hello FirstName and LastName fields toocreate a new file in hello cloud storage account.</span></span> 
   > 
   > 
5. <span data-ttu-id="8434a-136">**Sla** uw wijzigingen (linksboven Hallo werkbalk).</span><span class="sxs-lookup"><span data-stu-id="8434a-136">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="8434a-137">Uw logische app wordt opgeslagen en automatisch kan worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="8434a-137">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="8434a-138">Connector-specifieke details</span><span class="sxs-lookup"><span data-stu-id="8434a-138">Connector-specific details</span></span>

<span data-ttu-id="8434a-139">Alle triggers en acties die zijn gedefinieerd in swagger Hallo bekijken en ook bekijken in Hallo beperkingen [connector details](/connectors/sql/).</span><span class="sxs-lookup"><span data-stu-id="8434a-139">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/sql/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8434a-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8434a-140">Next steps</span></span>
<span data-ttu-id="8434a-141">[Een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="8434a-141">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="8434a-142">Verken Hallo van andere beschikbare connectors in Logic Apps op onze [API's lijst](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="8434a-142">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

