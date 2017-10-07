---
title: aaaCall REST-eindpunten met HTTP- en Swagger-connector voor Azure Logic Apps | Microsoft Docs
description: Verbinding maken met tooREST eindpunten vanuit logic apps via Swagger met Hallo HTTP + Swagger-connector
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
ms.openlocfilehash: baaa57689ff41fcd052f9d86086e36619ddec46e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-http--swagger-action"></a><span data-ttu-id="945eb-103">Aan de slag met Hallo HTTP + Swagger-actie</span><span class="sxs-lookup"><span data-stu-id="945eb-103">Get started with hello HTTP + Swagger action</span></span>

<span data-ttu-id="945eb-104">Kunt u een uitstekende connector tooany REST-eindpunt via een [Swagger-document](https://swagger.io) wanneer u Hallo HTTP + Swagger actie gebruikt in uw logische app-werkstroom.</span><span class="sxs-lookup"><span data-stu-id="945eb-104">You can create a first-class connector tooany REST endpoint through a [Swagger document](https://swagger.io) when you use hello HTTP + Swagger action in your logic app workflow.</span></span> <span data-ttu-id="945eb-105">U kunt logische apps toocall ook een REST-eindpunt met een uitstekende Logic App-ontwerper ervaring uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="945eb-105">You can also extend logic apps toocall any REST endpoint with a first-class Logic App Designer experience.</span></span>

<span data-ttu-id="945eb-106">hoe toocreate logic apps met connectors, Zie toolearn [maken van een nieuwe logische app](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="945eb-106">toolearn how toocreate logic apps with connectors, see [Create a new logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-http--swagger-as-a-trigger-or-an-action"></a><span data-ttu-id="945eb-107">Gebruik HTTP + Swagger als een trigger of een actie</span><span class="sxs-lookup"><span data-stu-id="945eb-107">Use HTTP + Swagger as a trigger or an action</span></span>

<span data-ttu-id="945eb-108">Hallo HTTP + Swagger-trigger en action werk dezelfde als Hallo Hallo [HTTP-actie](connectors-native-http.md) maar bieden een betere ervaring in Logic App-ontwerper bij het blootstellen van Hallo API structuur en uitvoer van Hallo [Swagger-metagegevens](https://swagger.io) .</span><span class="sxs-lookup"><span data-stu-id="945eb-108">hello HTTP + Swagger trigger and action work hello same as hello [HTTP action](connectors-native-http.md) but provide a better experience in Logic App Designer by exposing hello API structure and outputs from hello [Swagger metadata](https://swagger.io).</span></span> <span data-ttu-id="945eb-109">U kunt ook Hallo HTTP + Swagger-connector gebruiken als een trigger.</span><span class="sxs-lookup"><span data-stu-id="945eb-109">You can also use hello HTTP + Swagger connector as a trigger.</span></span> <span data-ttu-id="945eb-110">Als u een polling-trigger tooimplement wilt, volgen Hallo polling-patroon dat wordt beschreven in [maken van aangepaste API's toocall andere API's, services en systemen van logische apps](../logic-apps/logic-apps-create-api-app.md#polling-triggers).</span><span class="sxs-lookup"><span data-stu-id="945eb-110">If you want tooimplement a polling trigger, follow hello polling pattern that's described in [Create custom APIs toocall other APIs, services, and systems from logic apps](../logic-apps/logic-apps-create-api-app.md#polling-triggers).</span></span>

<span data-ttu-id="945eb-111">Meer informatie over [logic app triggers en acties](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="945eb-111">Learn more about [logic app triggers and actions](connectors-overview.md).</span></span>

<span data-ttu-id="945eb-112">Hier volgt een voorbeeld van hoe toouse Hallo HTTP + Swagger bewerking als een actie in een werkstroom in een logische app.</span><span class="sxs-lookup"><span data-stu-id="945eb-112">Here's an example of how toouse hello HTTP + Swagger operation as an action in a workflow in a logic app.</span></span>

1. <span data-ttu-id="945eb-113">Selecteer Hallo **nieuwe stap** knop.</span><span class="sxs-lookup"><span data-stu-id="945eb-113">Select hello **New Step** button.</span></span>
2. <span data-ttu-id="945eb-114">Selecteer **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="945eb-114">Select **Add an action**.</span></span>
3. <span data-ttu-id="945eb-115">Typ in het zoekvak Hallo actie, **swagger** toolist Hallo HTTP + Swagger in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="945eb-115">In hello action search box, type **swagger** toolist hello HTTP + Swagger action.</span></span>
   
    ![Selecteer HTTP + Swagger actie](./media/connectors-native-http-swagger/using-action-1.png)
4. <span data-ttu-id="945eb-117">Type Hallo-URL voor een Swagger-document:</span><span class="sxs-lookup"><span data-stu-id="945eb-117">Type hello URL for a Swagger document:</span></span>
   
   * <span data-ttu-id="945eb-118">toowork van Hallo Logic App-ontwerper, Hallo-URL moet een HTTPS-eindpunt en CORS is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="945eb-118">toowork from hello Logic App Designer, hello URL must be an HTTPS endpoint and have CORS enabled.</span></span>
   * <span data-ttu-id="945eb-119">Als Hallo Swagger-document niet aan deze vereiste voldoen, kunt u [Azure Storage met CORS ingeschakeld](#hosting-swagger-from-storage) toostore Hallo-document.</span><span class="sxs-lookup"><span data-stu-id="945eb-119">If hello Swagger document doesn't meet this requirement, you can use [Azure Storage with CORS enabled](#hosting-swagger-from-storage) toostore hello document.</span></span>
5. <span data-ttu-id="945eb-120">Klik op **volgende** tooread en render van Hallo Swagger-document.</span><span class="sxs-lookup"><span data-stu-id="945eb-120">Click **Next** tooread and render from hello Swagger document.</span></span>
6. <span data-ttu-id="945eb-121">In de parameters die vereist voor Hallo HTTP-aanroep zijn toevoegen.</span><span class="sxs-lookup"><span data-stu-id="945eb-121">Add in any parameters that are required for hello HTTP call.</span></span>
   
    ![HTTP-bewerking voltooien](./media/connectors-native-http-swagger/using-action-2.png)
7. <span data-ttu-id="945eb-123">toosave en uw logische app publiceren, klikt u op **opslaan** op designer werkbalk.</span><span class="sxs-lookup"><span data-stu-id="945eb-123">toosave and publish your logic app, click **Save** on designer toolbar.</span></span>

### <a name="host-swagger-from-azure-storage"></a><span data-ttu-id="945eb-124">Host Swagger uit Azure Storage</span><span class="sxs-lookup"><span data-stu-id="945eb-124">Host Swagger from Azure Storage</span></span>
<span data-ttu-id="945eb-125">U kunt een Swagger-document dat niet wordt gehost of die niet voldoen aan de Hallo beveiligings- en cross-origin-vereisten voor Hallo designer tooreference.</span><span class="sxs-lookup"><span data-stu-id="945eb-125">You might want tooreference a Swagger document that's not hosted, or that doesn't meet hello security and cross-origin requirements for hello designer.</span></span> <span data-ttu-id="945eb-126">tooresolve dit probleem kunt u Hallo Swagger-document opslaan in Azure Storage en inschakelen van CORS tooreference Hallo-document.</span><span class="sxs-lookup"><span data-stu-id="945eb-126">tooresolve this issue, you can store hello Swagger document in Azure Storage and enable CORS tooreference hello document.</span></span>  

<span data-ttu-id="945eb-127">Hier volgen Hallo stappen toocreate, configureren en Swagger documenten opslaan in Azure Storage:</span><span class="sxs-lookup"><span data-stu-id="945eb-127">Here are hello steps toocreate, configure, and store Swagger documents in Azure Storage:</span></span>

1. <span data-ttu-id="945eb-128">[Een Azure storage-account maken met Azure Blob storage](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="945eb-128">[Create an Azure storage account with Azure Blob storage](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="945eb-129">tooperform deze stap, machtigingen instellen te**openbare toegang**.</span><span class="sxs-lookup"><span data-stu-id="945eb-129">tooperform this step, set permissions too**Public Access**.</span></span>

2. <span data-ttu-id="945eb-130">CORS inschakelen op Hallo blob.</span><span class="sxs-lookup"><span data-stu-id="945eb-130">Enable CORS on hello blob.</span></span> 

   <span data-ttu-id="945eb-131">tooautomatically deze instelling configureert, kunt u [dit PowerShell-script](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1).</span><span class="sxs-lookup"><span data-stu-id="945eb-131">tooautomatically configure this setting, you can use [this PowerShell script](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1).</span></span>

3. <span data-ttu-id="945eb-132">Hallo Swagger-bestand toohello blob uploaden.</span><span class="sxs-lookup"><span data-stu-id="945eb-132">Upload hello Swagger file toohello blob.</span></span> 

   <span data-ttu-id="945eb-133">U kunt deze stap uitvoeren via Hallo [Azure-portal](https://portal.azure.com) of vanuit een hulpprogramma zoals [Azure Opslagverkenner](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="945eb-133">You can perform this step from hello [Azure portal](https://portal.azure.com) or from a tool like [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

4. <span data-ttu-id="945eb-134">Verwijzen naar een document HTTPS koppeling toohello in Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="945eb-134">Reference an HTTPS link toohello document in Azure Blob storage.</span></span> 

   <span data-ttu-id="945eb-135">Hallo-koppeling gebruikt deze indeling:</span><span class="sxs-lookup"><span data-stu-id="945eb-135">hello link uses this format:</span></span>

   `https://*storageAccountName*.blob.core.windows.net/*container*/*filename*`

## <a name="technical-details"></a><span data-ttu-id="945eb-136">Technische details</span><span class="sxs-lookup"><span data-stu-id="945eb-136">Technical details</span></span>
<span data-ttu-id="945eb-137">Hieronder vindt u details Hallo voor Hallo triggers en acties die dit HTTP + Swagger connector ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="945eb-137">Following are hello details for hello triggers and actions that this HTTP + Swagger connector supports.</span></span>

## <a name="http--swagger-triggers"></a><span data-ttu-id="945eb-138">HTTP- + Swagger-triggers</span><span class="sxs-lookup"><span data-stu-id="945eb-138">HTTP + Swagger triggers</span></span>
<span data-ttu-id="945eb-139">Een trigger is een gebeurtenis die kan worden gebruikt toostart Hallo werkstroom die gedefinieerd in een logische app.</span><span class="sxs-lookup"><span data-stu-id="945eb-139">A trigger is an event that can be used toostart hello workflow that's defined in a logic app.</span></span> [<span data-ttu-id="945eb-140">Meer informatie over triggers.</span><span class="sxs-lookup"><span data-stu-id="945eb-140">Learn more about triggers.</span></span>](connectors-overview.md) <span data-ttu-id="945eb-141">Hallo HTTP + Swagger connector heeft een trigger.</span><span class="sxs-lookup"><span data-stu-id="945eb-141">hello HTTP + Swagger connector has one trigger.</span></span>

| <span data-ttu-id="945eb-142">Trigger</span><span class="sxs-lookup"><span data-stu-id="945eb-142">Trigger</span></span> | <span data-ttu-id="945eb-143">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="945eb-143">Description</span></span> |
| --- | --- |
| <span data-ttu-id="945eb-144">HTTP- + Swagger</span><span class="sxs-lookup"><span data-stu-id="945eb-144">HTTP + Swagger</span></span> |<span data-ttu-id="945eb-145">De aanroep van een HTTP- en antwoordinhoud Hallo retourneren</span><span class="sxs-lookup"><span data-stu-id="945eb-145">Make an HTTP call and return hello response content</span></span> |

## <a name="http--swagger-actions"></a><span data-ttu-id="945eb-146">HTTP- + Swagger-acties</span><span class="sxs-lookup"><span data-stu-id="945eb-146">HTTP + Swagger actions</span></span>
<span data-ttu-id="945eb-147">Een actie is een bewerking die wordt uitgevoerd door Hallo werkstroom die gedefinieerd in een logische app.</span><span class="sxs-lookup"><span data-stu-id="945eb-147">An action is an operation that's carried out by hello workflow that's defined in a logic app.</span></span> [<span data-ttu-id="945eb-148">Meer informatie over acties.</span><span class="sxs-lookup"><span data-stu-id="945eb-148">Learn more about actions.</span></span>](connectors-overview.md) <span data-ttu-id="945eb-149">Hallo HTTP + Swagger connector heeft een mogelijke actie.</span><span class="sxs-lookup"><span data-stu-id="945eb-149">hello HTTP + Swagger connector has one possible action.</span></span>

| <span data-ttu-id="945eb-150">Actie</span><span class="sxs-lookup"><span data-stu-id="945eb-150">Action</span></span> | <span data-ttu-id="945eb-151">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="945eb-151">Description</span></span> |
| --- | --- |
| <span data-ttu-id="945eb-152">HTTP- + Swagger</span><span class="sxs-lookup"><span data-stu-id="945eb-152">HTTP + Swagger</span></span> |<span data-ttu-id="945eb-153">De aanroep van een HTTP- en antwoordinhoud Hallo retourneren</span><span class="sxs-lookup"><span data-stu-id="945eb-153">Make an HTTP call and return hello response content</span></span> |

### <a name="action-details"></a><span data-ttu-id="945eb-154">Actiedetails</span><span class="sxs-lookup"><span data-stu-id="945eb-154">Action details</span></span>
<span data-ttu-id="945eb-155">Hallo HTTP + Swagger connector wordt geleverd met een mogelijke actie.</span><span class="sxs-lookup"><span data-stu-id="945eb-155">hello HTTP + Swagger connector comes with one possible action.</span></span> <span data-ttu-id="945eb-156">Hieronder vindt u informatie over elk van de Hallo acties, de vereiste en optionele invoervelden en Hallo uitvoerdetails die gekoppeld aan hun gebruik zijn overeenkomt.</span><span class="sxs-lookup"><span data-stu-id="945eb-156">Following is information about each of hello actions, their required and optional input fields, and hello corresponding output details that are associated with their usage.</span></span>

#### <a name="http--swagger"></a><span data-ttu-id="945eb-157">HTTP- + Swagger</span><span class="sxs-lookup"><span data-stu-id="945eb-157">HTTP + Swagger</span></span>
<span data-ttu-id="945eb-158">Controleer een uitgaande HTTP-aanvraag met hulp van Swagger-metagegevens.</span><span class="sxs-lookup"><span data-stu-id="945eb-158">Make an HTTP outbound request with assistance of Swagger metadata.</span></span>
<span data-ttu-id="945eb-159">Een sterretje (*) betekent een verplicht veld.</span><span class="sxs-lookup"><span data-stu-id="945eb-159">An asterisk (*) means a required field.</span></span>

| <span data-ttu-id="945eb-160">Weergavenaam</span><span class="sxs-lookup"><span data-stu-id="945eb-160">Display name</span></span> | <span data-ttu-id="945eb-161">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="945eb-161">Property name</span></span> | <span data-ttu-id="945eb-162">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="945eb-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="945eb-163">Methode *</span><span class="sxs-lookup"><span data-stu-id="945eb-163">Method*</span></span> |<span data-ttu-id="945eb-164">Methode</span><span class="sxs-lookup"><span data-stu-id="945eb-164">method</span></span> |<span data-ttu-id="945eb-165">HTTP-term toouse.</span><span class="sxs-lookup"><span data-stu-id="945eb-165">HTTP verb toouse.</span></span> |
| <span data-ttu-id="945eb-166">URI *</span><span class="sxs-lookup"><span data-stu-id="945eb-166">URI*</span></span> |<span data-ttu-id="945eb-167">URI</span><span class="sxs-lookup"><span data-stu-id="945eb-167">uri</span></span> |<span data-ttu-id="945eb-168">De URI voor Hallo HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="945eb-168">URI for hello HTTP request.</span></span> |
| <span data-ttu-id="945eb-169">Headers</span><span class="sxs-lookup"><span data-stu-id="945eb-169">Headers</span></span> |<span data-ttu-id="945eb-170">Headers</span><span class="sxs-lookup"><span data-stu-id="945eb-170">headers</span></span> |<span data-ttu-id="945eb-171">Een JSON-object van het HTTP-headers tooinclude.</span><span class="sxs-lookup"><span data-stu-id="945eb-171">A JSON object of HTTP headers tooinclude.</span></span> |
| <span data-ttu-id="945eb-172">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="945eb-172">Body</span></span> |<span data-ttu-id="945eb-173">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="945eb-173">body</span></span> |<span data-ttu-id="945eb-174">Hallo hoofdtekst van de HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="945eb-174">hello HTTP request body.</span></span> |
| <span data-ttu-id="945eb-175">Authentication</span><span class="sxs-lookup"><span data-stu-id="945eb-175">Authentication</span></span> |<span data-ttu-id="945eb-176">Verificatie</span><span class="sxs-lookup"><span data-stu-id="945eb-176">authentication</span></span> |<span data-ttu-id="945eb-177">Verificatie toouse voor aanvraag.</span><span class="sxs-lookup"><span data-stu-id="945eb-177">Authentication toouse for request.</span></span> <span data-ttu-id="945eb-178">Zie voor meer informatie, Hallo [HTTP connector](connectors-native-http.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="945eb-178">For more information, see hello [HTTP connector](connectors-native-http.md#authentication).</span></span> |

<span data-ttu-id="945eb-179">**Uitvoerdetails**</span><span class="sxs-lookup"><span data-stu-id="945eb-179">**Output details**</span></span>

<span data-ttu-id="945eb-180">HTTP-antwoord</span><span class="sxs-lookup"><span data-stu-id="945eb-180">HTTP response</span></span>

| <span data-ttu-id="945eb-181">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="945eb-181">Property Name</span></span> | <span data-ttu-id="945eb-182">Gegevenstype</span><span class="sxs-lookup"><span data-stu-id="945eb-182">Data type</span></span> | <span data-ttu-id="945eb-183">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="945eb-183">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="945eb-184">Headers</span><span class="sxs-lookup"><span data-stu-id="945eb-184">Headers</span></span> |<span data-ttu-id="945eb-185">object</span><span class="sxs-lookup"><span data-stu-id="945eb-185">object</span></span> |<span data-ttu-id="945eb-186">Antwoordheaders</span><span class="sxs-lookup"><span data-stu-id="945eb-186">Response headers</span></span> |
| <span data-ttu-id="945eb-187">Hoofdtekst</span><span class="sxs-lookup"><span data-stu-id="945eb-187">Body</span></span> |<span data-ttu-id="945eb-188">object</span><span class="sxs-lookup"><span data-stu-id="945eb-188">object</span></span> |<span data-ttu-id="945eb-189">Response-object</span><span class="sxs-lookup"><span data-stu-id="945eb-189">Response object</span></span> |
| <span data-ttu-id="945eb-190">Statuscode</span><span class="sxs-lookup"><span data-stu-id="945eb-190">Status Code</span></span> |<span data-ttu-id="945eb-191">int</span><span class="sxs-lookup"><span data-stu-id="945eb-191">int</span></span> |<span data-ttu-id="945eb-192">HTTP-statuscode</span><span class="sxs-lookup"><span data-stu-id="945eb-192">HTTP status code</span></span> |

### <a name="http-responses"></a><span data-ttu-id="945eb-193">HTTP-antwoorden</span><span class="sxs-lookup"><span data-stu-id="945eb-193">HTTP responses</span></span>
<span data-ttu-id="945eb-194">Bij het maken van aanroepen toovarious acties, krijgt u mogelijk bepaalde antwoorden.</span><span class="sxs-lookup"><span data-stu-id="945eb-194">When making calls toovarious actions, you might get certain responses.</span></span> <span data-ttu-id="945eb-195">Hier volgt een tabel staat aangegeven van de bijbehorende antwoorden en beschrijvingen.</span><span class="sxs-lookup"><span data-stu-id="945eb-195">Following is a table that outlines corresponding responses and descriptions.</span></span>

| <span data-ttu-id="945eb-196">Naam</span><span class="sxs-lookup"><span data-stu-id="945eb-196">Name</span></span> | <span data-ttu-id="945eb-197">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="945eb-197">Description</span></span> |
| --- | --- |
| <span data-ttu-id="945eb-198">200</span><span class="sxs-lookup"><span data-stu-id="945eb-198">200</span></span> |<span data-ttu-id="945eb-199">OK</span><span class="sxs-lookup"><span data-stu-id="945eb-199">OK</span></span> |
| <span data-ttu-id="945eb-200">202</span><span class="sxs-lookup"><span data-stu-id="945eb-200">202</span></span> |<span data-ttu-id="945eb-201">Geaccepteerd</span><span class="sxs-lookup"><span data-stu-id="945eb-201">Accepted</span></span> |
| <span data-ttu-id="945eb-202">400</span><span class="sxs-lookup"><span data-stu-id="945eb-202">400</span></span> |<span data-ttu-id="945eb-203">Onjuiste aanvraag</span><span class="sxs-lookup"><span data-stu-id="945eb-203">Bad request</span></span> |
| <span data-ttu-id="945eb-204">401</span><span class="sxs-lookup"><span data-stu-id="945eb-204">401</span></span> |<span data-ttu-id="945eb-205">Niet geautoriseerd</span><span class="sxs-lookup"><span data-stu-id="945eb-205">Unauthorized</span></span> |
| <span data-ttu-id="945eb-206">403</span><span class="sxs-lookup"><span data-stu-id="945eb-206">403</span></span> |<span data-ttu-id="945eb-207">Is niet toegestaan</span><span class="sxs-lookup"><span data-stu-id="945eb-207">Forbidden</span></span> |
| <span data-ttu-id="945eb-208">404</span><span class="sxs-lookup"><span data-stu-id="945eb-208">404</span></span> |<span data-ttu-id="945eb-209">Niet gevonden</span><span class="sxs-lookup"><span data-stu-id="945eb-209">Not Found</span></span> |
| <span data-ttu-id="945eb-210">500</span><span class="sxs-lookup"><span data-stu-id="945eb-210">500</span></span> |<span data-ttu-id="945eb-211">Interne serverfout.</span><span class="sxs-lookup"><span data-stu-id="945eb-211">Internal server error.</span></span> <span data-ttu-id="945eb-212">Er is een onbekende fout opgetreden.</span><span class="sxs-lookup"><span data-stu-id="945eb-212">Unknown error occurred.</span></span> |

- - -
## <a name="next-steps"></a><span data-ttu-id="945eb-213">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="945eb-213">Next steps</span></span>

* [<span data-ttu-id="945eb-214">Een logische app maken</span><span class="sxs-lookup"><span data-stu-id="945eb-214">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="945eb-215">Andere connectors zoeken</span><span class="sxs-lookup"><span data-stu-id="945eb-215">Find other connectors</span></span>](apis-list.md)