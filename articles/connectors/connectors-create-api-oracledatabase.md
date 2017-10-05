---
title: De connector Oracle-Database in Azure Logic Apps toevoegen | Microsoft Docs
description: De connector Oracle-Database in een logische app gebruiken
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
ms.openlocfilehash: cc64441617eb5e7d5e70c1cf5c491a672428bc51
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-the-oracle-database-connector"></a><span data-ttu-id="025e7-103">Aan de slag met de Oracle-Database-connector</span><span class="sxs-lookup"><span data-stu-id="025e7-103">Get started with the Oracle Database connector</span></span>

<span data-ttu-id="025e7-104">De connector Oracle-Database maakt, u organisatie werkstromen die gebruikmaken van gegevens in uw bestaande database.</span><span class="sxs-lookup"><span data-stu-id="025e7-104">Using the Oracle Database connector, you create organizational workflows that use data in your existing database.</span></span> <span data-ttu-id="025e7-105">Deze connector kunt verbinden met een lokale Oracle-Database of Azure een virtuele machine met Oracle-Database is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="025e7-105">This connector can connect to an on-premises Oracle Database, or an Azure virtual machine with Oracle Database installed.</span></span> <span data-ttu-id="025e7-106">Met deze connector kunt u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="025e7-106">With this connector, you can:</span></span>

* <span data-ttu-id="025e7-107">Uw werkstroom door een nieuwe klant toe te voegen aan een database klanten of bijwerken van een order in een orderdatabase is opgebouwd.</span><span class="sxs-lookup"><span data-stu-id="025e7-107">Build your workflow by adding a new customer to a customers database, or updating an order in an orders database.</span></span>
* <span data-ttu-id="025e7-108">Acties voor een rij met gegevens ophalen, een nieuwe rij invoegen en verwijderen van zelfs gebruiken.</span><span class="sxs-lookup"><span data-stu-id="025e7-108">Use actions to get a row of data, insert a new row, and even delete.</span></span> <span data-ttu-id="025e7-109">Bijvoorbeeld, wanneer een record in Dynamics CRM Online (een trigger) wordt gemaakt, klikt u vervolgens een rij invoegen in een Oracle-Database (een actie).</span><span class="sxs-lookup"><span data-stu-id="025e7-109">For example, when a record is created in Dynamics CRM Online (a trigger), then insert a row in an Oracle Database (an action).</span></span> 

<span data-ttu-id="025e7-110">Dit onderwerp leest u hoe u de connector Oracle-Database in een logische app.</span><span class="sxs-lookup"><span data-stu-id="025e7-110">This topic shows you how to use the Oracle Database connector in a logic app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="025e7-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="025e7-111">Prerequisites</span></span>

* <span data-ttu-id="025e7-112">Ondersteunde versies van Oracle:</span><span class="sxs-lookup"><span data-stu-id="025e7-112">Supported Oracle versions:</span></span> 
    * <span data-ttu-id="025e7-113">Oracle 9 en hoger</span><span class="sxs-lookup"><span data-stu-id="025e7-113">Oracle 9 and later</span></span>
    * <span data-ttu-id="025e7-114">Oracle-clientsoftware 8.1.7 of hoger</span><span class="sxs-lookup"><span data-stu-id="025e7-114">Oracle client software 8.1.7 and later</span></span>

* <span data-ttu-id="025e7-115">Installeer de lokale data gateway.</span><span class="sxs-lookup"><span data-stu-id="025e7-115">Install the on-premises data gateway.</span></span> <span data-ttu-id="025e7-116">[Verbinding maken met on-premises gegevens vanuit logic apps](../logic-apps/logic-apps-gateway-connection.md) vermeldt de stappen.</span><span class="sxs-lookup"><span data-stu-id="025e7-116">[Connect to on-premises data from logic apps](../logic-apps/logic-apps-gateway-connection.md) lists the steps.</span></span> <span data-ttu-id="025e7-117">De gateway is vereist voor het verbinding maken met een lokale Oracle-Database of een Azure-virtuele machine met Oracle DB geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="025e7-117">The gateway is required to connect to an on-premises Oracle Database, or an Azure VM with Oracle DB installed.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="025e7-118">De lokale data gateway fungeert als een brug en biedt een veilige gegevensoverdracht tussen on-premises gegevens (gegevens die zich niet in de cloud) en uw logische apps.</span><span class="sxs-lookup"><span data-stu-id="025e7-118">The on-premises data gateway acts as a bridge, and provides a secure data transfer between on-premises data (data that is not in the cloud) and your logic apps.</span></span> <span data-ttu-id="025e7-119">Dezelfde gateway kan worden gebruikt met meerdere services en meerdere gegevensbronnen.</span><span class="sxs-lookup"><span data-stu-id="025e7-119">The same gateway can be used with multiple services, and multiple data sources.</span></span> <span data-ttu-id="025e7-120">U wellicht dus slechts één keer de gateway te installeren.</span><span class="sxs-lookup"><span data-stu-id="025e7-120">So, you may only need to install the gateway once.</span></span>

* <span data-ttu-id="025e7-121">De Oracle-Client installeren op de computer waarop u de lokale data gateway hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="025e7-121">Install the Oracle Client on the machine where you installed the on-premises data gateway.</span></span> <span data-ttu-id="025e7-122">Zorg ervoor dat de 64-bits Oracle-gegevensprovider voor .NET van Oracle installeren:</span><span class="sxs-lookup"><span data-stu-id="025e7-122">Be sure to install the 64-bit Oracle Data Provider for .NET from Oracle:</span></span>  

  [<span data-ttu-id="025e7-123">64-bits ODAC 12c versie 4 (12.1.0.2.4) voor Windows x64</span><span class="sxs-lookup"><span data-stu-id="025e7-123">64-bit ODAC 12c Release 4 (12.1.0.2.4) for Windows x64</span></span>](http://www.oracle.com/technetwork/database/windows/downloads/index-090165.html)

    > [!TIP]
    > <span data-ttu-id="025e7-124">Als de Oracle-client niet is geïnstalleerd, wordt er een fout optreedt wanneer u probeert te maken of de verbinding wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="025e7-124">If the Oracle client is not installed, an error occurs when you try to create or use the connection.</span></span> <span data-ttu-id="025e7-125">Zie de veelvoorkomende fouten in dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="025e7-125">See the common errors in this topic.</span></span>


## <a name="add-the-connector"></a><span data-ttu-id="025e7-126">De connector toevoegen</span><span class="sxs-lookup"><span data-stu-id="025e7-126">Add the connector</span></span>

> [!IMPORTANT]
> <span data-ttu-id="025e7-127">Deze connector heeft geen triggers bestaan niet.</span><span class="sxs-lookup"><span data-stu-id="025e7-127">This connector does not have any triggers.</span></span> <span data-ttu-id="025e7-128">Alleen acties heeft.</span><span class="sxs-lookup"><span data-stu-id="025e7-128">It has only actions.</span></span> <span data-ttu-id="025e7-129">Dus als u uw logische app maakt, een andere trigger voor het starten van uw logische app, zoals toevoegen **schema - terugkeerpatroon**, of **vraag / antwoord - antwoord**.</span><span class="sxs-lookup"><span data-stu-id="025e7-129">So when you create your logic app, add another trigger to start your logic app, such as **Schedule - Recurrence**, or **Request / Response - Response**.</span></span> 

1. <span data-ttu-id="025e7-130">In de [Azure-portal](https://portal.azure.com), een lege logische app maken.</span><span class="sxs-lookup"><span data-stu-id="025e7-130">In the [Azure portal](https://portal.azure.com), create a blank logic app.</span></span>

2. <span data-ttu-id="025e7-131">Aan het begin van uw logische app, selecteer de **vraag / antwoord - aanvraag** trigger:</span><span class="sxs-lookup"><span data-stu-id="025e7-131">At the start of your logic app, select the **Request / Response - Request** trigger:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/request-trigger.png)

3. <span data-ttu-id="025e7-132">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="025e7-132">Select **Save**.</span></span> <span data-ttu-id="025e7-133">Wanneer u opslaat, wordt een aanvraag-URL wordt automatisch gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="025e7-133">When you save, a request URL is automatically generated.</span></span> 

4. <span data-ttu-id="025e7-134">Selecteer **nieuwe stap**, en selecteer **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="025e7-134">Select **New step**, and select **Add an action**.</span></span> <span data-ttu-id="025e7-135">Typ in `oracle` om te zien van de beschikbare acties:</span><span class="sxs-lookup"><span data-stu-id="025e7-135">Type in `oracle` to see the available actions:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/oracledb-actions.png)

    > [!TIP]
    > <span data-ttu-id="025e7-136">Dit is ook de snelste manier om te zien van de triggers en acties die beschikbaar zijn voor elke connector.</span><span class="sxs-lookup"><span data-stu-id="025e7-136">This is also the quickest way to see the triggers and actions available for any connector.</span></span> <span data-ttu-id="025e7-137">Typ in het gedeelte van de connectornaam van de, zoals `oracle`.</span><span class="sxs-lookup"><span data-stu-id="025e7-137">Type in part of the connector name, such as `oracle`.</span></span> <span data-ttu-id="025e7-138">De ontwerpfunctie voor een lijst met alle triggers en acties.</span><span class="sxs-lookup"><span data-stu-id="025e7-138">The designer lists any triggers and any actions.</span></span> 

5. <span data-ttu-id="025e7-139">Selecteer een van de acties zoals **Oracle-Database - Get-rij**.</span><span class="sxs-lookup"><span data-stu-id="025e7-139">Select one of the actions, such as **Oracle Database - Get row**.</span></span> <span data-ttu-id="025e7-140">Selecteer **verbinden via lokale gegevensgateway**.</span><span class="sxs-lookup"><span data-stu-id="025e7-140">Select **Connect via on-premises data gateway**.</span></span> <span data-ttu-id="025e7-141">Voer de naam van de Oracle-server, de verificatiemethode, de gebruikersnaam, wachtwoord en selecteer de gateway:</span><span class="sxs-lookup"><span data-stu-id="025e7-141">Enter the Oracle server name, authentication method, username, password, and select the gateway:</span></span>

    ![](./media/connectors-create-api-oracledatabase/create-oracle-connection.png)

6. <span data-ttu-id="025e7-142">Eenmaal zijn verbonden, selecteer een tabel in de lijst en voer de rij-ID aan de tabel.</span><span class="sxs-lookup"><span data-stu-id="025e7-142">Once connected, select a table from the list, and enter the row ID to your table.</span></span> <span data-ttu-id="025e7-143">U moet weten de in de tabel-id.</span><span class="sxs-lookup"><span data-stu-id="025e7-143">You need to know the identifier to the table.</span></span> <span data-ttu-id="025e7-144">Als u niet weet, contact op met uw beheerder Oracle DB, en de uitvoer van `select * from yourTableName`.</span><span class="sxs-lookup"><span data-stu-id="025e7-144">If you don't know, contact your Oracle DB administrator, and get the output from `select * from yourTableName`.</span></span> <span data-ttu-id="025e7-145">Hiermee krijgt u identificeerbare informatie die u nodig hebt om door te gaan.</span><span class="sxs-lookup"><span data-stu-id="025e7-145">This gives you the identifiable information you need to proceed.</span></span>

    <span data-ttu-id="025e7-146">In het volgende voorbeeld wordt de taakgegevens wordt geretourneerd uit een database Human Resources:</span><span class="sxs-lookup"><span data-stu-id="025e7-146">In the following example, job data is being returned from a Human Resources database:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/table-rowid.png)

7. <span data-ttu-id="025e7-147">In deze stap, kunt u een van de andere connectors gebruiken voor het bouwen van uw werkstroom.</span><span class="sxs-lookup"><span data-stu-id="025e7-147">In this next step, you can use any of the other connectors to build your workflow.</span></span> <span data-ttu-id="025e7-148">Als u ophalen van gegevens uit Oracle testen wilt, klikt u vervolgens verzend een e-mailbericht met de Oracle-gegevens met behulp van een van de verzonden e-connectors, zoals Office 365 of Gmail.</span><span class="sxs-lookup"><span data-stu-id="025e7-148">If you want to test getting data from Oracle, then send yourself an email with the Oracle data using one of the send email connectors, such Office 365 or Gmail.</span></span> <span data-ttu-id="025e7-149">De dynamische tokens van de Oracle-tabel gebruiken om de `Subject` en `Body` van uw e-mailadres:</span><span class="sxs-lookup"><span data-stu-id="025e7-149">Use the dynamic tokens from the Oracle table to build the `Subject` and `Body` of your email:</span></span>

    ![](./media/connectors-create-api-oracledatabase/oracle-send-email.png)

8. <span data-ttu-id="025e7-150">**Sla** uw logische app en selecteer vervolgens **uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="025e7-150">**Save** your logic app, and then select **Run**.</span></span> <span data-ttu-id="025e7-151">Sluit de ontwerpfunctie en bekijk de geschiedenis wordt uitgevoerd voor de status.</span><span class="sxs-lookup"><span data-stu-id="025e7-151">Close the designer, and look at the runs history for the status.</span></span> <span data-ttu-id="025e7-152">Als dit mislukt, selecteer de rij mislukt bericht.</span><span class="sxs-lookup"><span data-stu-id="025e7-152">If it fails, select the failed message row.</span></span> <span data-ttu-id="025e7-153">De ontwerpfunctie wordt geopend en ziet u dat de stap is mislukt en ziet ook de foutgegevens.</span><span class="sxs-lookup"><span data-stu-id="025e7-153">The designer opens, and shows you which step failed, and also shows the error information.</span></span> <span data-ttu-id="025e7-154">Als dat lukt, ontvangt u een e-mailbericht met de informatie die u hebt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="025e7-154">If it succeeds, then you should receive an email with the information you added.</span></span>


### <a name="workflow-ideas"></a><span data-ttu-id="025e7-155">Werkstroom ideeën</span><span class="sxs-lookup"><span data-stu-id="025e7-155">Workflow ideas</span></span>

* <span data-ttu-id="025e7-156">U wilt bewaken van de hashtag #oracle en de tweets in een database te plaatsen, zodat ze kunnen worden opgevraagd, en in andere toepassingen gebruikt.</span><span class="sxs-lookup"><span data-stu-id="025e7-156">You want to monitor the #oracle hashtag, and put the tweets in a database so they can be queried, and used within other applications.</span></span> <span data-ttu-id="025e7-157">In een logische app, voegt u de `Twitter - When a new tweet is posted` activeren en voer de **#oracle** hashtag.</span><span class="sxs-lookup"><span data-stu-id="025e7-157">In a logic app, add the `Twitter - When a new tweet is posted` trigger, and enter the **#oracle** hashtag.</span></span> <span data-ttu-id="025e7-158">Voeg vervolgens de `Oracle Database - Insert row` actie, en selecteer de tabel:</span><span class="sxs-lookup"><span data-stu-id="025e7-158">Then, add the `Oracle Database - Insert row` action, and select your table:</span></span>

    ![](./media/connectors-create-api-oracledatabase/twitter-oracledb.png)

* <span data-ttu-id="025e7-159">Berichten worden verzonden naar een Service Bus-wachtrij.</span><span class="sxs-lookup"><span data-stu-id="025e7-159">Messages are sent to a Service Bus queue.</span></span> <span data-ttu-id="025e7-160">U wilt deze berichten ophalen en plaatsen in een database.</span><span class="sxs-lookup"><span data-stu-id="025e7-160">You want to get these messages, and put them in a database.</span></span> <span data-ttu-id="025e7-161">In een logische app, voegt u de `Service Bus - when a message is received in a queue` activeren en selecteert u de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="025e7-161">In a logic app, add the `Service Bus - when a message is received in a queue` trigger, and select the queue.</span></span> <span data-ttu-id="025e7-162">Voeg vervolgens de `Oracle Database - Insert row` actie, en selecteer de tabel:</span><span class="sxs-lookup"><span data-stu-id="025e7-162">Then, add the `Oracle Database - Insert row` action, and select your table:</span></span>

    ![](./media/connectors-create-api-oracledatabase/sbqueue-oracledb.png)

## <a name="common-errors"></a><span data-ttu-id="025e7-163">Veelvoorkomende fouten</span><span class="sxs-lookup"><span data-stu-id="025e7-163">Common errors</span></span>

#### <a name="error-cannot-reach-the-gateway"></a><span data-ttu-id="025e7-164">**Fout**: de Gateway kan niet worden bereikt.</span><span class="sxs-lookup"><span data-stu-id="025e7-164">**Error**: Cannot reach the Gateway</span></span>

<span data-ttu-id="025e7-165">**Oorzaak**: de lokale data gateway kan geen verbinding maken met de cloud.</span><span class="sxs-lookup"><span data-stu-id="025e7-165">**Cause**: The on-premises data gateway is not able to connect to the cloud.</span></span> 

<span data-ttu-id="025e7-166">**Risicobeperking**: Zorg ervoor dat uw gateway wordt uitgevoerd op de on-premises machine waar u het hebt geïnstalleerd en dat deze verbinding kan maken met internet.</span><span class="sxs-lookup"><span data-stu-id="025e7-166">**Mitigation**: Make sure your gateway is running on the on-premises machine where you installed it, and that it can connect to the internet.</span></span>  <span data-ttu-id="025e7-167">Het is raadzaam om de gateway niet is geïnstalleerd op een computer die kan worden uitgeschakeld of de slaapstand.</span><span class="sxs-lookup"><span data-stu-id="025e7-167">We recommend not installing the gateway on a computer that may be turned off or sleep.</span></span> <span data-ttu-id="025e7-168">U kunt ook de lokale data gateway-service (PBIEgwService) opnieuw.</span><span class="sxs-lookup"><span data-stu-id="025e7-168">You can also restart the on-premises data gateway service (PBIEgwService).</span></span>

#### <a name="error-the-provider-being-used-is-deprecated-systemdataoracleclient-requires-oracle-client-software-version-817-or-greater-please-visit-httpsgomicrosoftcomfwlinkplinkid272376httpsgomicrosoftcomfwlinkplinkid272376-to-install-the-official-provider"></a><span data-ttu-id="025e7-169">**Fout**: de gebruikte provider is verouderd: ' voor System.Data.OracleClient is vereist voor Oracle-clientsoftware version 8.1.7 of hoger.'.</span><span class="sxs-lookup"><span data-stu-id="025e7-169">**Error**: The provider being used is deprecated: 'System.Data.OracleClient requires Oracle client software version 8.1.7 or greater.'.</span></span> <span data-ttu-id="025e7-170">Ga naar [https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) om de officiële provider te installeren.</span><span class="sxs-lookup"><span data-stu-id="025e7-170">Please visit [https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) to install the official provider.</span></span>

<span data-ttu-id="025e7-171">**Oorzaak**: de Oracle-client SDK niet is geïnstalleerd op de computer waarop de lokale data gateway wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="025e7-171">**Cause**: The Oracle client SDK is not installed on the machine where the on-premises data gateway is running.</span></span>  

<span data-ttu-id="025e7-172">**Resolutie**: downloaden en installeren van de Oracle-client-SDK op dezelfde computer als de lokale data gateway.</span><span class="sxs-lookup"><span data-stu-id="025e7-172">**Resolution**: Download and install the Oracle client SDK on the same computer as the on-premises data gateway.</span></span>

#### <a name="error-table-tablename-does-not-define-any-key-columns"></a><span data-ttu-id="025e7-173">**Fout**: tabel [tabelnaam] geen alle sleutelkolommen gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="025e7-173">**Error**: Table '[Tablename]' does not define any key columns</span></span>

<span data-ttu-id="025e7-174">**Oorzaak**: de tabel heeft geen primaire sleutel.</span><span class="sxs-lookup"><span data-stu-id="025e7-174">**Cause**: The table does not have any primary key.</span></span>  

<span data-ttu-id="025e7-175">**Resolutie**: de Oracle-Database connector vereist dat een tabel met een primaire sleutelkolom worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="025e7-175">**Resolution**: The Oracle Database connector requires that a table with a primary key column be used.</span></span>

#### <a name="currently-not-supported"></a><span data-ttu-id="025e7-176">Momenteel ondersteund niet</span><span class="sxs-lookup"><span data-stu-id="025e7-176">Currently not supported</span></span>

* <span data-ttu-id="025e7-177">Weergaven en opgeslagen procedures</span><span class="sxs-lookup"><span data-stu-id="025e7-177">Views and stored procedures</span></span> 
* <span data-ttu-id="025e7-178">Een tabel met samengestelde sleutels</span><span class="sxs-lookup"><span data-stu-id="025e7-178">Any table with composite keys</span></span>
* <span data-ttu-id="025e7-179">Geneste objecttypen in tabellen</span><span class="sxs-lookup"><span data-stu-id="025e7-179">Nested object types in tables</span></span>
 
## <a name="connector-specific-details"></a><span data-ttu-id="025e7-180">Connector-specifieke details</span><span class="sxs-lookup"><span data-stu-id="025e7-180">Connector-specific details</span></span>

<span data-ttu-id="025e7-181">Alle triggers en acties die zijn gedefinieerd in de swagger bekijken en ziet u ook de beperkingen in de [connector details](/connectors/oracle/).</span><span class="sxs-lookup"><span data-stu-id="025e7-181">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/oracle/).</span></span> 

## <a name="get-some-help"></a><span data-ttu-id="025e7-182">Hulp krijgen</span><span class="sxs-lookup"><span data-stu-id="025e7-182">Get some help</span></span>

<span data-ttu-id="025e7-183">De [Azure Logic Apps-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) is een goede plaats om te vragen, beantwoorden van vragen en zien wat anderen Logic Apps doen.</span><span class="sxs-lookup"><span data-stu-id="025e7-183">The [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) is a great place to ask questions, answer questions, and see what other Logic Apps users are doing.</span></span> 

<span data-ttu-id="025e7-184">U kunt logische Apps en connectors verbeteren door uw stem en verzenden van uw ideeën op [http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="025e7-184">You can help improve Logic Apps and connectors by voting and submitting your ideas at [http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish).</span></span> 


## <a name="next-steps"></a><span data-ttu-id="025e7-185">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="025e7-185">Next steps</span></span>
<span data-ttu-id="025e7-186">[Een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md), en bekijk de beschikbare connectors in Logic Apps op onze [API's lijst](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="025e7-186">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md), and explore the available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
