---
title: Aanroepen van REST-eindpunten met HTTP- en Swagger-connector voor Azure Logic Apps | Microsoft Docs
description: Verbinding maken met de REST-eindpunten vanuit logic apps via Swagger met de HTTP- + Swagger connector
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: eccfd87c-c5fe-4cf7-b564-9752775fd667
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: 3e9229d94e96aad7b769d0e55d208d856e3b80bc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-the-http--swagger-action"></a><span data-ttu-id="8b6dc-103">Aan de slag met de HTTP- + Swagger actie</span><span class="sxs-lookup"><span data-stu-id="8b6dc-103">Get started with the HTTP + Swagger action</span></span>

<span data-ttu-id="8b6dc-104">U kunt geen klas connector maken voor een willekeurig eindpunt REST via een [Swagger-document](https://swagger.io) bij het gebruik van de HTTP- + Swagger actie in de werkstroom van uw logische app.</span><span class="sxs-lookup"><span data-stu-id="8b6dc-104">You can create a first-class connector to any REST endpoint through a [Swagger document](https://swagger.io) when you use the HTTP + Swagger action in your logic app workflow.</span></span> <span data-ttu-id="8b6dc-105">U kunt logische apps voor het aanroepen van een REST-eindpunt met een uitstekende Logic App-ontwerper ervaring ook uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="8b6dc-105">You can also extend logic apps to call any REST endpoint with a first-class Logic App Designer experience.</span></span>

<span data-ttu-id="8b6dc-106">Zie voor meer informatie over het maken van logische apps met connectors, [maken van een nieuwe logische app](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="8b6dc-106">To learn how to create logic apps with connectors, see [Create a new logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-http--swagger-as-a-trigger-or-an-action"></a><span data-ttu-id="8b6dc-107">Gebruik HTTP + Swagger als een trigger of een actie</span><span class="sxs-lookup"><span data-stu-id="8b6dc-107">Use HTTP + Swagger as a trigger or an action</span></span>

<span data-ttu-id="8b6dc-108">De HTTP- + de Swagger activeren en de actie werken op dezelfde manier als de [HTTP-actie](connectors-native-http.md) maar bieden een betere ervaring in Logic App-ontwerper bij het blootstellen van de structuur van de API en de uitvoer van de [Swagger-metagegevens](https://swagger.io).</span><span class="sxs-lookup"><span data-stu-id="8b6dc-108">The HTTP + Swagger trigger and action work the same as the [HTTP action](connectors-native-http.md) but provide a better experience in Logic App Designer by exposing the API structure and outputs from the [Swagger metadata](https://swagger.io).</span></span> <span data-ttu-id="8b6dc-109">U kunt ook HTTP gebruiken + Swagger connector als een trigger.</span><span class="sxs-lookup"><span data-stu-id="8b6dc-109">You can also use the HTTP + Swagger connector as a trigger.</span></span> <span data-ttu-id="8b6dc-110">Als u implementeren, een polling-trigger wilt, volgt u het polling-patroon dat wordt beschreven in [maken van aangepaste API's om aan te roepen andere API's, services en systemen van logic apps](../logic-apps/logic-apps-create-api-app.md#polling-triggers).</span><span class="sxs-lookup"><span data-stu-id="8b6dc-110">If you want to implement a polling trigger, follow the polling pattern that's described in [Create custom APIs to call other APIs, services, and systems from logic apps](../logic-apps/logic-apps-create-api-app.md#polling-triggers).</span></span>

<span data-ttu-id="8b6dc-111">Meer informatie over [logic app triggers en acties](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8b6dc-111">Learn more about [logic app triggers and actions](connectors-overview.md).</span></span>

<span data-ttu-id="8b6dc-112">Hier volgt een voorbeeld van het gebruik van de HTTP-+ Swagger-bewerkings-als een actie in een werkstroom in een logische app.</span><span class="sxs-lookup"><span data-stu-id="8b6dc-112">Here's an example of how to use the HTTP + Swagger operation as an action in a workflow in a logic app.</span></span>

1. <span data-ttu-id="8b6dc-113">Selecteer de **nieuwe stap** knop.</span><span class="sxs-lookup"><span data-stu-id="8b6dc-113">Select the **New Step** button.</span></span>
2. <span data-ttu-id="8b6dc-114">Selecteer **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="8b6dc-114">Select **Add an action**.</span></span>
3. <span data-ttu-id="8b6dc-115">Typ in het zoekvak actie **swagger** aan de lijst het HTTP-Swagger-actie.</span><span class="sxs-lookup"><span data-stu-id="8b6dc-115">In the action search box, type **swagger** to list the HTTP + Swagger action.</span></span>
   
    ![Selecteer HTTP + Swagger actie](./media/connectors-native-http-swagger/using-action-1.png)
4. <span data-ttu-id="8b6dc-117">Typ de URL voor een Swagger-document:</span><span class="sxs-lookup"><span data-stu-id="8b6dc-117">Type the URL for a Swagger document:</span></span>
   
   * <span data-ttu-id="8b6dc-118">Om te werken vanuit Logic App Designer, moet de URL een HTTPS-eindpunt en CORS is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="8b6dc-118">To work from the Logic App Designer, the URL must be an HTTPS endpoint and have CORS enabled.</span></span>
   * <span data-ttu-id="8b6dc-119">Als de Swagger-document niet aan deze vereiste voldoen, kunt u [Azure Storage met CORS ingeschakeld](#hosting-swagger-from-storage) voor het opslaan van het document.</span><span class="sxs-lookup"><span data-stu-id="8b6dc-119">If the Swagger document doesn't meet this requirement, you can use [Azure Storage with CORS enabled](#hosting-swagger-from-storage) to store the document.</span></span>
5. <span data-ttu-id="8b6dc-120">Klik op **volgende** om te lezen en weergeven van de Swagger-document.</span><span class="sxs-lookup"><span data-stu-id="8b6dc-120">Click **Next** to read and render from the Swagger document.</span></span>
6. <span data-ttu-id="8b6dc-121">Voeg in de parameters die vereist voor de HTTP-aanroep zijn.</span><span class="sxs-lookup"><span data-stu-id="8b6dc-121">Add in any parameters that are required for the HTTP call.</span></span>
   
    ![HTTP-bewerking voltooien](./media/connectors-native-http-swagger/using-action-2.png)
7. <span data-ttu-id="8b6dc-123">Als u wilt opslaan en publiceren van uw logische app, klikt u op **opslaan** op designer werkbalk.</span><span class="sxs-lookup"><span data-stu-id="8b6dc-123">To save and publish your logic app, click **Save** on designer toolbar.</span></span>

### <a name="host-swagger-from-azure-storage"></a><span data-ttu-id="8b6dc-124">Host Swagger uit Azure Storage</span><span class="sxs-lookup"><span data-stu-id="8b6dc-124">Host Swagger from Azure Storage</span></span>
<span data-ttu-id="8b6dc-125">Het is raadzaam om te verwijzen naar een Swagger-document dat niet wordt gehost of die niet voldoen aan de beveiliging en cross-origin-vereisten voor de designer.</span><span class="sxs-lookup"><span data-stu-id="8b6dc-125">You might want to reference a Swagger document that's not hosted, or that doesn't meet the security and cross-origin requirements for the designer.</span></span> <span data-ttu-id="8b6dc-126">U lost dit probleem, kunt u de Swagger-document opslaan in Azure Storage en inschakelen van CORS om te verwijzen naar het document.</span><span class="sxs-lookup"><span data-stu-id="8b6dc-126">To resolve this issue, you can store the Swagger document in Azure Storage and enable CORS to reference the document.</span></span>  

<span data-ttu-id="8b6dc-127">Hier volgen de stappen voor het maken, configureren en opslaan van documenten Swagger in Azure Storage:</span><span class="sxs-lookup"><span data-stu-id="8b6dc-127">Here are the steps to create, configure, and store Swagger documents in Azure Storage:</span></span>

1. <span data-ttu-id="8b6dc-128">[Een Azure storage-account maken met Azure Blob storage](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="8b6dc-128">[Create an Azure storage account with Azure Blob storage](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="8b6dc-129">Als u deze stap, stel de machtigingen op **openbare toegang**.</span><span class="sxs-lookup"><span data-stu-id="8b6dc-129">To perform this step, set permissions to **Public Access**.</span></span>

2. <span data-ttu-id="8b6dc-130">CORS inschakelen in de blob.</span><span class="sxs-lookup"><span data-stu-id="8b6dc-130">Enable CORS on the blob.</span></span> 

   <span data-ttu-id="8b6dc-131">U kunt gebruiken om automatisch te configureren met deze instelling, [dit PowerShell-script](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1).</span><span class="sxs-lookup"><span data-stu-id="8b6dc-131">To automatically configure this setting, you can use [this PowerShell script](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1).</span></span>

3. <span data-ttu-id="8b6dc-132">Het Swagger-bestand uploaden naar de blob.</span><span class="sxs-lookup"><span data-stu-id="8b6dc-132">Upload the Swagger file to the blob.</span></span> 

   <span data-ttu-id="8b6dc-133">U kunt uitvoeren in deze stap van de [Azure-portal](https://portal.azure.com) of vanuit een hulpprogramma zoals [Azure Opslagverkenner](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="8b6dc-133">You can perform this step from the [Azure portal](https://portal.azure.com) or from a tool like [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

4. <span data-ttu-id="8b6dc-134">Verwijzen naar een HTTPS-koppeling in het document in Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="8b6dc-134">Reference an HTTPS link to the document in Azure Blob storage.</span></span> 

   <span data-ttu-id="8b6dc-135">De koppeling maakt gebruik van deze indeling:</span><span class="sxs-lookup"><span data-stu-id="8b6dc-135">The link uses this format:</span></span>

   `https://*storageAccountName*.blob.core.windows.net/*container*/*filename*`

## <a name="technical-details"></a><span data-ttu-id="8b6dc-136">Technische details</span><span class="sxs-lookup"><span data-stu-id="8b6dc-136">Technical details</span></span>
<span data-ttu-id="8b6dc-137">Hieronder vindt u de details voor de triggers en acties die in het volgende HTTP- + Swagger connector ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="8b6dc-137">Following are the details for the triggers and actions that this HTTP + Swagger connector supports.</span></span>

## <a name="http--swagger-triggers"></a><span data-ttu-id="8b6dc-138">HTTP- + Swagger-triggers</span><span class="sxs-lookup"><span data-stu-id="8b6dc-138">HTTP + Swagger triggers</span></span>
<span data-ttu-id="8b6dc-139">Een trigger is een gebeurtenis die kan worden gebruikt om de werkstroom die gedefinieerd in een logische app te starten.</span><span class="sxs-lookup"><span data-stu-id="8b6dc-139">A trigger is an event that can be used to start the workflow that's defined in a logic app.</span></span> [<span data-ttu-id="8b6dc-140">Meer informatie over triggers.</span><span class="sxs-lookup"><span data-stu-id="8b6dc-140">Learn more about triggers.</span></span>](connectors-overview.md) <span data-ttu-id="8b6dc-141">De HTTP- + Swagger connector heeft een trigger.</span><span class="sxs-lookup"><span data-stu-id="8b6dc-141">The HTTP + Swagger connector has one trigger.</span></span>

| <span data-ttu-id="8b6dc-142">Trigger</span><span class="sxs-lookup"><span data-stu-id="8b6dc-142">Trigger</span></span> | <span data-ttu-id="8b6dc-143">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="8b6dc-143">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8b6dc-144">HTTP- + Swagger</span><span class="sxs-lookup"><span data-stu-id="8b6dc-144">HTTP + Swagger</span></span> |<span data-ttu-id="8b6dc-145">Maken van een HTTP-aanroep en de antwoordinhoud wordt geretourneerd</span><span class="sxs-lookup"><span data-stu-id="8b6dc-145">Make an HTTP call and return the response content</span></span> |

## <a name="http--swagger-actions"></a><span data-ttu-id="8b6dc-146">HTTP- + Swagger-acties</span><span class="sxs-lookup"><span data-stu-id="8b6dc-146">HTTP + Swagger actions</span></span>
<span data-ttu-id="8b6dc-147">Een actie is een bewerking die wordt uitgevoerd door de werkstroom die gedefinieerd in een logische app.</span><span class="sxs-lookup"><span data-stu-id="8b6dc-147">An action is an operation that's carried out by the workflow that's defined in a logic app.</span></span> [<span data-ttu-id="8b6dc-148">Meer informatie over acties.</span><span class="sxs-lookup"><span data-stu-id="8b6dc-148">Learn more about actions.</span></span>](connectors-overview.md) <span data-ttu-id="8b6dc-149">De HTTP- + Swagger connector heeft een mogelijke actie.</span><span class="sxs-lookup"><span data-stu-id="8b6dc-149">The HTTP + Swagger connector has one possible action.</span></span>

| <span data-ttu-id="8b6dc-150">Actie</span><span class="sxs-lookup"><span data-stu-id="8b6dc-150">Action</span></span> | <span data-ttu-id="8b6dc-151">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="8b6dc-151">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8b6dc-152">HTTP- + Swagger</span><span class="sxs-lookup"><span data-stu-id="8b6dc-152">HTTP + Swagger</span></span> |<span data-ttu-id="8b6dc-153">Maken van een HTTP-aanroep en de antwoordinhoud wordt geretourneerd</span><span class="sxs-lookup"><span data-stu-id="8b6dc-153">Make an HTTP call and return the response content</span></span> |

### <a name="action-details"></a><span data-ttu-id="8b6dc-154">Actiedetails</span><span class="sxs-lookup"><span data-stu-id="8b6dc-154">Action details</span></span>
<span data-ttu-id="8b6dc-155">De HTTP- + Swagger connector wordt geleverd met een mogelijke actie.</span><span class="sxs-lookup"><span data-stu-id="8b6dc-155">The HTTP + Swagger connector comes with one possible action.</span></span> <span data-ttu-id="8b6dc-156">Hieronder vindt u informatie over elk van de acties, hun vereiste en optionele invoervelden en de bijbehorende uitvoerdetails die gekoppeld aan hun gebruik zijn.</span><span class="sxs-lookup"><span data-stu-id="8b6dc-156">Following is information about each of the actions, their required and optional input fields, and the corresponding output details that are associated with their usage.</span></span>

#### <a name="http--swagger"></a><span data-ttu-id="8b6dc-157">HTTP- + Swagger</span><span class="sxs-lookup"><span data-stu-id="8b6dc-157">HTTP + Swagger</span></span>
<span data-ttu-id="8b6dc-158">Controleer een uitgaande HTTP-aanvraag met hulp van Swagger-metagegevens.</span><span class="sxs-lookup"><span data-stu-id="8b6dc-158">Make an HTTP outbound request with assistance of Swagger metadata.</span></span>
<span data-ttu-id="8b6dc-159">Een sterretje (*) betekent een verplicht veld.</span><span class="sxs-lookup"><span data-stu-id="8b6dc-159">An asterisk (*) means a required field.</span></span>

| <span data-ttu-id="8b6dc-160">Weergavenaam</span><span class="sxs-lookup"><span data-stu-id="8b6dc-160">Display name</span></span> | <span data-ttu-id="8b6dc-161">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="8b6dc-161">Property name</span></span> | <span data-ttu-id="8b6dc-162">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="8b6dc-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b6dc-163">Methode *</span><span class="sxs-lookup"><span data-stu-id="8b6dc-163">Method*</span></span> |<span data-ttu-id="8b6dc-164">Methode</span><span class="sxs-lookup"><span data-stu-id="8b6dc-164">method</span></span> |<span data-ttu-id="8b6dc-165">HTTP-term moet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8b6dc-165">HTTP verb to use.</span></span> |
| <span data-ttu-id="8b6dc-166">URI *</span><span class="sxs-lookup"><span data-stu-id="8b6dc-166">URI*</span></span> |<span data-ttu-id="8b6dc-167">URI</span><span class="sxs-lookup"><span data-stu-id="8b6dc-167">uri</span></span> |<span data-ttu-id="8b6dc-168">De URI voor de HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="8b6dc-168">URI for the HTTP request.</span></span> |
| <span data-ttu-id="8b6dc-169">Headers</span><span class="sxs-lookup"><span data-stu-id="8b6dc-169">Headers</span></span> |<span data-ttu-id="8b6dc-170">Headers</span><span class="sxs-lookup"><span data-stu-id="8b6dc-170">headers</span></span> |<span data-ttu-id="8b6dc-171">Een JSON-object van het HTTP-headers te nemen.</span><span class="sxs-lookup"><span data-stu-id="8b6dc-171">A JSON object of HTTP headers to include.</span></span> |
| <span data-ttu-id="8b6dc-172">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="8b6dc-172">Body</span></span> |<span data-ttu-id="8b6dc-173">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="8b6dc-173">body</span></span> |<span data-ttu-id="8b6dc-174">De hoofdtekst van de HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="8b6dc-174">The HTTP request body.</span></span> |
| <span data-ttu-id="8b6dc-175">Authentication</span><span class="sxs-lookup"><span data-stu-id="8b6dc-175">Authentication</span></span> |<span data-ttu-id="8b6dc-176">Verificatie</span><span class="sxs-lookup"><span data-stu-id="8b6dc-176">authentication</span></span> |<span data-ttu-id="8b6dc-177">De verificatie moet worden gebruikt voor de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="8b6dc-177">Authentication to use for request.</span></span> <span data-ttu-id="8b6dc-178">Zie voor meer informatie de [HTTP connector](connectors-native-http.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="8b6dc-178">For more information, see the [HTTP connector](connectors-native-http.md#authentication).</span></span> |

<span data-ttu-id="8b6dc-179">**Uitvoerdetails**</span><span class="sxs-lookup"><span data-stu-id="8b6dc-179">**Output details**</span></span>

<span data-ttu-id="8b6dc-180">HTTP-antwoord</span><span class="sxs-lookup"><span data-stu-id="8b6dc-180">HTTP response</span></span>

| <span data-ttu-id="8b6dc-181">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="8b6dc-181">Property Name</span></span> | <span data-ttu-id="8b6dc-182">Gegevenstype</span><span class="sxs-lookup"><span data-stu-id="8b6dc-182">Data type</span></span> | <span data-ttu-id="8b6dc-183">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="8b6dc-183">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b6dc-184">Headers</span><span class="sxs-lookup"><span data-stu-id="8b6dc-184">Headers</span></span> |<span data-ttu-id="8b6dc-185">object</span><span class="sxs-lookup"><span data-stu-id="8b6dc-185">object</span></span> |<span data-ttu-id="8b6dc-186">Antwoordheaders</span><span class="sxs-lookup"><span data-stu-id="8b6dc-186">Response headers</span></span> |
| <span data-ttu-id="8b6dc-187">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="8b6dc-187">Body</span></span> |<span data-ttu-id="8b6dc-188">object</span><span class="sxs-lookup"><span data-stu-id="8b6dc-188">object</span></span> |<span data-ttu-id="8b6dc-189">Response-object</span><span class="sxs-lookup"><span data-stu-id="8b6dc-189">Response object</span></span> |
| <span data-ttu-id="8b6dc-190">Statuscode</span><span class="sxs-lookup"><span data-stu-id="8b6dc-190">Status Code</span></span> |<span data-ttu-id="8b6dc-191">int</span><span class="sxs-lookup"><span data-stu-id="8b6dc-191">int</span></span> |<span data-ttu-id="8b6dc-192">HTTP-statuscode</span><span class="sxs-lookup"><span data-stu-id="8b6dc-192">HTTP status code</span></span> |

### <a name="http-responses"></a><span data-ttu-id="8b6dc-193">HTTP-antwoorden</span><span class="sxs-lookup"><span data-stu-id="8b6dc-193">HTTP responses</span></span>
<span data-ttu-id="8b6dc-194">Bij het aanroepen op diverse acties, krijgt u mogelijk bepaalde antwoorden.</span><span class="sxs-lookup"><span data-stu-id="8b6dc-194">When making calls to various actions, you might get certain responses.</span></span> <span data-ttu-id="8b6dc-195">Hier volgt een tabel staat aangegeven van de bijbehorende antwoorden en beschrijvingen.</span><span class="sxs-lookup"><span data-stu-id="8b6dc-195">Following is a table that outlines corresponding responses and descriptions.</span></span>

| <span data-ttu-id="8b6dc-196">Naam</span><span class="sxs-lookup"><span data-stu-id="8b6dc-196">Name</span></span> | <span data-ttu-id="8b6dc-197">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="8b6dc-197">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8b6dc-198">200</span><span class="sxs-lookup"><span data-stu-id="8b6dc-198">200</span></span> |<span data-ttu-id="8b6dc-199">OK</span><span class="sxs-lookup"><span data-stu-id="8b6dc-199">OK</span></span> |
| <span data-ttu-id="8b6dc-200">202</span><span class="sxs-lookup"><span data-stu-id="8b6dc-200">202</span></span> |<span data-ttu-id="8b6dc-201">Geaccepteerd</span><span class="sxs-lookup"><span data-stu-id="8b6dc-201">Accepted</span></span> |
| <span data-ttu-id="8b6dc-202">400</span><span class="sxs-lookup"><span data-stu-id="8b6dc-202">400</span></span> |<span data-ttu-id="8b6dc-203">Onjuiste aanvraag</span><span class="sxs-lookup"><span data-stu-id="8b6dc-203">Bad request</span></span> |
| <span data-ttu-id="8b6dc-204">401</span><span class="sxs-lookup"><span data-stu-id="8b6dc-204">401</span></span> |<span data-ttu-id="8b6dc-205">Niet geautoriseerd</span><span class="sxs-lookup"><span data-stu-id="8b6dc-205">Unauthorized</span></span> |
| <span data-ttu-id="8b6dc-206">403</span><span class="sxs-lookup"><span data-stu-id="8b6dc-206">403</span></span> |<span data-ttu-id="8b6dc-207">Is niet toegestaan</span><span class="sxs-lookup"><span data-stu-id="8b6dc-207">Forbidden</span></span> |
| <span data-ttu-id="8b6dc-208">404</span><span class="sxs-lookup"><span data-stu-id="8b6dc-208">404</span></span> |<span data-ttu-id="8b6dc-209">Niet gevonden</span><span class="sxs-lookup"><span data-stu-id="8b6dc-209">Not Found</span></span> |
| <span data-ttu-id="8b6dc-210">500</span><span class="sxs-lookup"><span data-stu-id="8b6dc-210">500</span></span> |<span data-ttu-id="8b6dc-211">Interne serverfout.</span><span class="sxs-lookup"><span data-stu-id="8b6dc-211">Internal server error.</span></span> <span data-ttu-id="8b6dc-212">Er is een onbekende fout opgetreden.</span><span class="sxs-lookup"><span data-stu-id="8b6dc-212">Unknown error occurred.</span></span> |

- - -
## <a name="next-steps"></a><span data-ttu-id="8b6dc-213">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8b6dc-213">Next steps</span></span>

* [<span data-ttu-id="8b6dc-214">Een logische app maken</span><span class="sxs-lookup"><span data-stu-id="8b6dc-214">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="8b6dc-215">Andere connectors zoeken</span><span class="sxs-lookup"><span data-stu-id="8b6dc-215">Find other connectors</span></span>](apis-list.md)