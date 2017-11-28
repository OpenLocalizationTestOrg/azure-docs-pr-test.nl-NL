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
# <a name="get-started-with-hello-oracle-database-connector"></a><span data-ttu-id="7522d-103">Aan de slag met Hallo Oracle-Database-connector</span><span class="sxs-lookup"><span data-stu-id="7522d-103">Get started with hello Oracle Database connector</span></span>

<span data-ttu-id="7522d-104">Hallo-connector voor Oracle-Database maakt, u organisatie werkstromen die gebruikmaken van gegevens in uw bestaande database.</span><span class="sxs-lookup"><span data-stu-id="7522d-104">Using hello Oracle Database connector, you create organizational workflows that use data in your existing database.</span></span> <span data-ttu-id="7522d-105">Deze connector kunt verbinden tooan lokale Oracle-Database of een Azure virtuele machine met Oracle-Database is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="7522d-105">This connector can connect tooan on-premises Oracle Database, or an Azure virtual machine with Oracle Database installed.</span></span> <span data-ttu-id="7522d-106">Met deze connector kunt u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="7522d-106">With this connector, you can:</span></span>

* <span data-ttu-id="7522d-107">Uw werkstroom door het toevoegen van een nieuwe database van de klant tooa klanten of bijwerken van een order in een orderdatabase bouwen.</span><span class="sxs-lookup"><span data-stu-id="7522d-107">Build your workflow by adding a new customer tooa customers database, or updating an order in an orders database.</span></span>
* <span data-ttu-id="7522d-108">Acties tooget een rij met gegevens gebruiken, een nieuwe rij invoegen en zelfs verwijderen.</span><span class="sxs-lookup"><span data-stu-id="7522d-108">Use actions tooget a row of data, insert a new row, and even delete.</span></span> <span data-ttu-id="7522d-109">Bijvoorbeeld, wanneer een record in Dynamics CRM Online (een trigger) wordt gemaakt, klikt u vervolgens een rij invoegen in een Oracle-Database (een actie).</span><span class="sxs-lookup"><span data-stu-id="7522d-109">For example, when a record is created in Dynamics CRM Online (a trigger), then insert a row in an Oracle Database (an action).</span></span> 

<span data-ttu-id="7522d-110">Dit onderwerp leest u hoe toouse Hallo Oracle-Database-connector in een logische app.</span><span class="sxs-lookup"><span data-stu-id="7522d-110">This topic shows you how toouse hello Oracle Database connector in a logic app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7522d-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7522d-111">Prerequisites</span></span>

* <span data-ttu-id="7522d-112">Ondersteunde versies van Oracle:</span><span class="sxs-lookup"><span data-stu-id="7522d-112">Supported Oracle versions:</span></span> 
    * <span data-ttu-id="7522d-113">Oracle 9 en hoger</span><span class="sxs-lookup"><span data-stu-id="7522d-113">Oracle 9 and later</span></span>
    * <span data-ttu-id="7522d-114">Oracle-clientsoftware 8.1.7 of hoger</span><span class="sxs-lookup"><span data-stu-id="7522d-114">Oracle client software 8.1.7 and later</span></span>

* <span data-ttu-id="7522d-115">Hallo lokale gegevensgateway installeren.</span><span class="sxs-lookup"><span data-stu-id="7522d-115">Install hello on-premises data gateway.</span></span> <span data-ttu-id="7522d-116">[Verbinding maken met tooon-premises gegevens vanuit logic apps](../logic-apps/logic-apps-gateway-connection.md) lijsten Hallo stappen.</span><span class="sxs-lookup"><span data-stu-id="7522d-116">[Connect tooon-premises data from logic apps](../logic-apps/logic-apps-gateway-connection.md) lists hello steps.</span></span> <span data-ttu-id="7522d-117">Hallo-gateway is vereist tooconnect tooan lokale Oracle-Database of een Azure-virtuele machine met Oracle DB geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="7522d-117">hello gateway is required tooconnect tooan on-premises Oracle Database, or an Azure VM with Oracle DB installed.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="7522d-118">Hallo lokale gegevensgateway fungeert als een brug en biedt een veilige gegevensoverdracht tussen on-premises gegevens (gegevens die zich niet in de cloud Hallo) en uw logische apps.</span><span class="sxs-lookup"><span data-stu-id="7522d-118">hello on-premises data gateway acts as a bridge, and provides a secure data transfer between on-premises data (data that is not in hello cloud) and your logic apps.</span></span> <span data-ttu-id="7522d-119">Hallo dezelfde gateway kan worden gebruikt met meerdere services en meerdere gegevensbronnen.</span><span class="sxs-lookup"><span data-stu-id="7522d-119">hello same gateway can be used with multiple services, and multiple data sources.</span></span> <span data-ttu-id="7522d-120">Daarom moet u mogelijk alleen tooinstall Hallo gateway eenmaal.</span><span class="sxs-lookup"><span data-stu-id="7522d-120">So, you may only need tooinstall hello gateway once.</span></span>

* <span data-ttu-id="7522d-121">Hallo Oracle-Client installeren op Hallo-computer waarop u Hallo lokale gegevensgateway hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="7522d-121">Install hello Oracle Client on hello machine where you installed hello on-premises data gateway.</span></span> <span data-ttu-id="7522d-122">Zorg ervoor dat tooinstall hello 64-bits Oracle-gegevensprovider voor .NET van Oracle:</span><span class="sxs-lookup"><span data-stu-id="7522d-122">Be sure tooinstall hello 64-bit Oracle Data Provider for .NET from Oracle:</span></span>  

  [<span data-ttu-id="7522d-123">64-bits ODAC 12c versie 4 (12.1.0.2.4) voor Windows x64</span><span class="sxs-lookup"><span data-stu-id="7522d-123">64-bit ODAC 12c Release 4 (12.1.0.2.4) for Windows x64</span></span>](http://www.oracle.com/technetwork/database/windows/downloads/index-090165.html)

    > [!TIP]
    > <span data-ttu-id="7522d-124">Als Hallo Oracle-client niet is geïnstalleerd, wordt er een fout optreedt wanneer u toocreate probeert of Hallo verbinding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7522d-124">If hello Oracle client is not installed, an error occurs when you try toocreate or use hello connection.</span></span> <span data-ttu-id="7522d-125">Zie Hallo veelvoorkomende fouten in dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="7522d-125">See hello common errors in this topic.</span></span>


## <a name="add-hello-connector"></a><span data-ttu-id="7522d-126">Hallo connector toevoegen</span><span class="sxs-lookup"><span data-stu-id="7522d-126">Add hello connector</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7522d-127">Deze connector heeft geen triggers bestaan niet.</span><span class="sxs-lookup"><span data-stu-id="7522d-127">This connector does not have any triggers.</span></span> <span data-ttu-id="7522d-128">Alleen acties heeft.</span><span class="sxs-lookup"><span data-stu-id="7522d-128">It has only actions.</span></span> <span data-ttu-id="7522d-129">Dus bij het maken van uw logische app toevoegen een andere trigger toostart uw logische app, zoals **schema - terugkeerpatroon**, of **vraag / antwoord - antwoord**.</span><span class="sxs-lookup"><span data-stu-id="7522d-129">So when you create your logic app, add another trigger toostart your logic app, such as **Schedule - Recurrence**, or **Request / Response - Response**.</span></span> 

1. <span data-ttu-id="7522d-130">In Hallo [Azure-portal](https://portal.azure.com), een lege logische app maken.</span><span class="sxs-lookup"><span data-stu-id="7522d-130">In hello [Azure portal](https://portal.azure.com), create a blank logic app.</span></span>

2. <span data-ttu-id="7522d-131">Bij Hallo begin van uw logische app, selecteer Hallo **vraag / antwoord - aanvraag** trigger:</span><span class="sxs-lookup"><span data-stu-id="7522d-131">At hello start of your logic app, select hello **Request / Response - Request** trigger:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/request-trigger.png)

3. <span data-ttu-id="7522d-132">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="7522d-132">Select **Save**.</span></span> <span data-ttu-id="7522d-133">Wanneer u opslaat, wordt een aanvraag-URL wordt automatisch gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="7522d-133">When you save, a request URL is automatically generated.</span></span> 

4. <span data-ttu-id="7522d-134">Selecteer **nieuwe stap**, en selecteer **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="7522d-134">Select **New step**, and select **Add an action**.</span></span> <span data-ttu-id="7522d-135">Typ in `oracle` toosee Hallo beschikbare acties:</span><span class="sxs-lookup"><span data-stu-id="7522d-135">Type in `oracle` toosee hello available actions:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/oracledb-actions.png)

    > [!TIP]
    > <span data-ttu-id="7522d-136">Dit is de snelste manier toosee Hallo Hallo triggers en acties die beschikbaar zijn voor elke connector.</span><span class="sxs-lookup"><span data-stu-id="7522d-136">This is also hello quickest way toosee hello triggers and actions available for any connector.</span></span> <span data-ttu-id="7522d-137">Typ in het deel van naam van de connector hello, zoals `oracle`.</span><span class="sxs-lookup"><span data-stu-id="7522d-137">Type in part of hello connector name, such as `oracle`.</span></span> <span data-ttu-id="7522d-138">Hallo designer geeft een lijst van alle triggers en acties.</span><span class="sxs-lookup"><span data-stu-id="7522d-138">hello designer lists any triggers and any actions.</span></span> 

5. <span data-ttu-id="7522d-139">Selecteer een van de Hallo acties, zoals **Oracle-Database - Get-rij**.</span><span class="sxs-lookup"><span data-stu-id="7522d-139">Select one of hello actions, such as **Oracle Database - Get row**.</span></span> <span data-ttu-id="7522d-140">Selecteer **verbinden via lokale gegevensgateway**.</span><span class="sxs-lookup"><span data-stu-id="7522d-140">Select **Connect via on-premises data gateway**.</span></span> <span data-ttu-id="7522d-141">Voer Hallo Oracle-servernaam, verificatiemethode, gebruikersnaam, wachtwoord en selecteer Hallo gateway:</span><span class="sxs-lookup"><span data-stu-id="7522d-141">Enter hello Oracle server name, authentication method, username, password, and select hello gateway:</span></span>

    ![](./media/connectors-create-api-oracledatabase/create-oracle-connection.png)

6. <span data-ttu-id="7522d-142">Eenmaal zijn verbonden, selecteer een tabel in de lijst Hallo en Voer Hallo rij-id-tooyour tabel.</span><span class="sxs-lookup"><span data-stu-id="7522d-142">Once connected, select a table from hello list, and enter hello row ID tooyour table.</span></span> <span data-ttu-id="7522d-143">U moet tooknow Hallo id toohello tabel.</span><span class="sxs-lookup"><span data-stu-id="7522d-143">You need tooknow hello identifier toohello table.</span></span> <span data-ttu-id="7522d-144">Als u niet weet, contact op met uw beheerder Oracle DB en ophalen van de uitvoer van Hallo `select * from yourTableName`.</span><span class="sxs-lookup"><span data-stu-id="7522d-144">If you don't know, contact your Oracle DB administrator, and get hello output from `select * from yourTableName`.</span></span> <span data-ttu-id="7522d-145">Dit biedt u identificeerbare informatie die u nodig hebt tooproceed Hallo.</span><span class="sxs-lookup"><span data-stu-id="7522d-145">This gives you hello identifiable information you need tooproceed.</span></span>

    <span data-ttu-id="7522d-146">In Hallo voorbeeld te volgen, taakgegevens uit een database Human Resources geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="7522d-146">In hello following example, job data is being returned from a Human Resources database:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/table-rowid.png)

7. <span data-ttu-id="7522d-147">In deze stap, kunt u een van de Hallo andere toobuild connectors uw werkstroom.</span><span class="sxs-lookup"><span data-stu-id="7522d-147">In this next step, you can use any of hello other connectors toobuild your workflow.</span></span> <span data-ttu-id="7522d-148">Als u wilt dat tootest ophalen van gegevens uit Oracle, verzend een e-mailbericht met Hallo Oracle-gegevens met een van de Hallo verzenden van e-connectors, zoals Office 365 of Gmail.</span><span class="sxs-lookup"><span data-stu-id="7522d-148">If you want tootest getting data from Oracle, then send yourself an email with hello Oracle data using one of hello send email connectors, such Office 365 or Gmail.</span></span> <span data-ttu-id="7522d-149">Gebruik dynamische tokens van Hallo Oracle tabel toobuild Hallo Hallo `Subject` en `Body` van uw e-mailadres:</span><span class="sxs-lookup"><span data-stu-id="7522d-149">Use hello dynamic tokens from hello Oracle table toobuild hello `Subject` and `Body` of your email:</span></span>

    ![](./media/connectors-create-api-oracledatabase/oracle-send-email.png)

8. <span data-ttu-id="7522d-150">**Sla** uw logische app en selecteer vervolgens **uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="7522d-150">**Save** your logic app, and then select **Run**.</span></span> <span data-ttu-id="7522d-151">Hallo ontwerpen sluiten en bekijkt hello wordt uitgevoerd geschiedenis voor Hallo status.</span><span class="sxs-lookup"><span data-stu-id="7522d-151">Close hello designer, and look at hello runs history for hello status.</span></span> <span data-ttu-id="7522d-152">Als het mislukt, selecteert u Hallo mislukt bericht rij.</span><span class="sxs-lookup"><span data-stu-id="7522d-152">If it fails, select hello failed message row.</span></span> <span data-ttu-id="7522d-153">Hallo designer wordt geopend en ziet u dat de stap is mislukt, en bevat informatie over de fout Hallo.</span><span class="sxs-lookup"><span data-stu-id="7522d-153">hello designer opens, and shows you which step failed, and also shows hello error information.</span></span> <span data-ttu-id="7522d-154">Als dat lukt, ontvangt u een e-mail met Hallo-informatie die u hebt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="7522d-154">If it succeeds, then you should receive an email with hello information you added.</span></span>


### <a name="workflow-ideas"></a><span data-ttu-id="7522d-155">Werkstroom ideeën</span><span class="sxs-lookup"><span data-stu-id="7522d-155">Workflow ideas</span></span>

* <span data-ttu-id="7522d-156">U wilt toomonitor hello #oracle hashtag en Hallo tweets in een database te plaatsen, zodat ze kunnen worden opgevraagd, en in andere toepassingen gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7522d-156">You want toomonitor hello #oracle hashtag, and put hello tweets in a database so they can be queried, and used within other applications.</span></span> <span data-ttu-id="7522d-157">Voeg in een logische app, Hallo `Twitter - When a new tweet is posted` activeren en Voer Hallo **#oracle** hashtag.</span><span class="sxs-lookup"><span data-stu-id="7522d-157">In a logic app, add hello `Twitter - When a new tweet is posted` trigger, and enter hello **#oracle** hashtag.</span></span> <span data-ttu-id="7522d-158">Vervolgens voegt u Hallo `Oracle Database - Insert row` actie, en selecteer de tabel:</span><span class="sxs-lookup"><span data-stu-id="7522d-158">Then, add hello `Oracle Database - Insert row` action, and select your table:</span></span>

    ![](./media/connectors-create-api-oracledatabase/twitter-oracledb.png)

* <span data-ttu-id="7522d-159">Berichten worden tooa Service Bus-wachtrij.</span><span class="sxs-lookup"><span data-stu-id="7522d-159">Messages are sent tooa Service Bus queue.</span></span> <span data-ttu-id="7522d-160">U wilt dat deze berichten tooget en plaatsen in een database.</span><span class="sxs-lookup"><span data-stu-id="7522d-160">You want tooget these messages, and put them in a database.</span></span> <span data-ttu-id="7522d-161">Voeg in een logische app, Hallo `Service Bus - when a message is received in a queue` trigger en selecteer Hallo wachtrij.</span><span class="sxs-lookup"><span data-stu-id="7522d-161">In a logic app, add hello `Service Bus - when a message is received in a queue` trigger, and select hello queue.</span></span> <span data-ttu-id="7522d-162">Vervolgens voegt u Hallo `Oracle Database - Insert row` actie, en selecteer de tabel:</span><span class="sxs-lookup"><span data-stu-id="7522d-162">Then, add hello `Oracle Database - Insert row` action, and select your table:</span></span>

    ![](./media/connectors-create-api-oracledatabase/sbqueue-oracledb.png)

## <a name="common-errors"></a><span data-ttu-id="7522d-163">Veelvoorkomende fouten</span><span class="sxs-lookup"><span data-stu-id="7522d-163">Common errors</span></span>

#### <a name="error-cannot-reach-hello-gateway"></a><span data-ttu-id="7522d-164">**Fout**: Hallo Gateway niet bereikbaar</span><span class="sxs-lookup"><span data-stu-id="7522d-164">**Error**: Cannot reach hello Gateway</span></span>

<span data-ttu-id="7522d-165">**Oorzaak**: Hallo lokale gegevensgateway is niet kunnen tooconnect toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="7522d-165">**Cause**: hello on-premises data gateway is not able tooconnect toohello cloud.</span></span> 

<span data-ttu-id="7522d-166">**Risicobeperking**: Zorg ervoor dat uw gateway wordt uitgevoerd op Hallo on-premises machine waar u het hebt geïnstalleerd en dat deze verbinding kan maken van toohello internet.</span><span class="sxs-lookup"><span data-stu-id="7522d-166">**Mitigation**: Make sure your gateway is running on hello on-premises machine where you installed it, and that it can connect toohello internet.</span></span>  <span data-ttu-id="7522d-167">U wordt aangeraden geen Hallo gateway installeren op een computer die kan worden uitgeschakeld of de slaapstand.</span><span class="sxs-lookup"><span data-stu-id="7522d-167">We recommend not installing hello gateway on a computer that may be turned off or sleep.</span></span> <span data-ttu-id="7522d-168">U kunt ook Hallo lokale data gateway-service (PBIEgwService) opnieuw.</span><span class="sxs-lookup"><span data-stu-id="7522d-168">You can also restart hello on-premises data gateway service (PBIEgwService).</span></span>

#### <a name="error-hello-provider-being-used-is-deprecated-systemdataoracleclient-requires-oracle-client-software-version-817-or-greater-please-visit-httpsgomicrosoftcomfwlinkplinkid272376httpsgomicrosoftcomfwlinkplinkid272376-tooinstall-hello-official-provider"></a><span data-ttu-id="7522d-169">**Fout**: Hallo provider die wordt gebruikt is afgeschaft: ' voor System.Data.OracleClient is vereist voor Oracle-clientsoftware version 8.1.7 of hoger.'.</span><span class="sxs-lookup"><span data-stu-id="7522d-169">**Error**: hello provider being used is deprecated: 'System.Data.OracleClient requires Oracle client software version 8.1.7 or greater.'.</span></span> <span data-ttu-id="7522d-170">Ga naar [https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) tooinstall Hallo officiële provider.</span><span class="sxs-lookup"><span data-stu-id="7522d-170">Please visit [https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) tooinstall hello official provider.</span></span>

<span data-ttu-id="7522d-171">**Oorzaak**: Hallo Oracle-client SDK niet is geïnstalleerd op machine Hallo waar hello lokale gegevensgateway wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7522d-171">**Cause**: hello Oracle client SDK is not installed on hello machine where hello on-premises data gateway is running.</span></span>  

<span data-ttu-id="7522d-172">**Resolutie**: downloaden en installeren van Hallo Oracle-client SDK op Hallo dezelfde computer als Hallo lokale gegevensgateway.</span><span class="sxs-lookup"><span data-stu-id="7522d-172">**Resolution**: Download and install hello Oracle client SDK on hello same computer as hello on-premises data gateway.</span></span>

#### <a name="error-table-tablename-does-not-define-any-key-columns"></a><span data-ttu-id="7522d-173">**Fout**: tabel [tabelnaam] geen alle sleutelkolommen gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="7522d-173">**Error**: Table '[Tablename]' does not define any key columns</span></span>

<span data-ttu-id="7522d-174">**Oorzaak**: Hallo tabel heeft geen primaire sleutel.</span><span class="sxs-lookup"><span data-stu-id="7522d-174">**Cause**: hello table does not have any primary key.</span></span>  

<span data-ttu-id="7522d-175">**Resolutie**: Hallo Oracle-Database connector vereist dat een tabel met een primaire sleutelkolom worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7522d-175">**Resolution**: hello Oracle Database connector requires that a table with a primary key column be used.</span></span>

#### <a name="currently-not-supported"></a><span data-ttu-id="7522d-176">Momenteel ondersteund niet</span><span class="sxs-lookup"><span data-stu-id="7522d-176">Currently not supported</span></span>

* <span data-ttu-id="7522d-177">Weergaven en opgeslagen procedures</span><span class="sxs-lookup"><span data-stu-id="7522d-177">Views and stored procedures</span></span> 
* <span data-ttu-id="7522d-178">Een tabel met samengestelde sleutels</span><span class="sxs-lookup"><span data-stu-id="7522d-178">Any table with composite keys</span></span>
* <span data-ttu-id="7522d-179">Geneste objecttypen in tabellen</span><span class="sxs-lookup"><span data-stu-id="7522d-179">Nested object types in tables</span></span>
 
## <a name="connector-specific-details"></a><span data-ttu-id="7522d-180">Connector-specifieke details</span><span class="sxs-lookup"><span data-stu-id="7522d-180">Connector-specific details</span></span>

<span data-ttu-id="7522d-181">Alle triggers en acties die zijn gedefinieerd in swagger Hallo bekijken en ook bekijken in Hallo beperkingen [connector details](/connectors/oracle/).</span><span class="sxs-lookup"><span data-stu-id="7522d-181">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/oracle/).</span></span> 

## <a name="get-some-help"></a><span data-ttu-id="7522d-182">Hulp krijgen</span><span class="sxs-lookup"><span data-stu-id="7522d-182">Get some help</span></span>

<span data-ttu-id="7522d-183">Hallo [Azure Logic Apps-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) is uitermate plaatsen tooask vragen beantwoorden van vragen en zien wat anderen Logic Apps doen.</span><span class="sxs-lookup"><span data-stu-id="7522d-183">hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) is a great place tooask questions, answer questions, and see what other Logic Apps users are doing.</span></span> 

<span data-ttu-id="7522d-184">U kunt logische Apps en connectors verbeteren door uw stem en verzenden van uw ideeën op [http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="7522d-184">You can help improve Logic Apps and connectors by voting and submitting your ideas at [http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish).</span></span> 


## <a name="next-steps"></a><span data-ttu-id="7522d-185">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7522d-185">Next steps</span></span>
<span data-ttu-id="7522d-186">[Een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md), en bekijk de beschikbare connectors Hallo in Logic Apps op onze [API's lijst](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="7522d-186">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md), and explore hello available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
