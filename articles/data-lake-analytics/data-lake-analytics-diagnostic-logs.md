---
title: Diagnostische logboeken aaaViewing voor Azure Data Lake Analytics | Microsoft Docs
description: 'Begrijpen hoe toosetup en toegang diagnostische logboeken voor Azure Data Lake analytics '
services: data-lake-analytics
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf5633d4-bc43-444e-90fc-f90fbd0b7935
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 4cd1eb6f585c1ef96c358340232ef85721a972b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-analytics"></a><span data-ttu-id="0b029-103">Toegang tot diagnoselogboeken voor Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="0b029-103">Accessing diagnostic logs for Azure Data Lake Analytics</span></span>

<span data-ttu-id="0b029-104">Diagnostische logboekregistratie kunt u toocollect gegevens audittrails voor bestandstoegang.</span><span class="sxs-lookup"><span data-stu-id="0b029-104">Diagnostic logging allows you toocollect data access audit trails.</span></span> <span data-ttu-id="0b029-105">Deze logboeken vindt u informatie, zoals:</span><span class="sxs-lookup"><span data-stu-id="0b029-105">These logs provide information such as:</span></span>

* <span data-ttu-id="0b029-106">Een lijst met gebruikers die Hallo-gegevens gebruikte.</span><span class="sxs-lookup"><span data-stu-id="0b029-106">A list of users that accessed hello data.</span></span>
* <span data-ttu-id="0b029-107">Hoe vaak gegevens hello worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="0b029-107">How frequently hello data is accessed.</span></span>
* <span data-ttu-id="0b029-108">Hoeveel gegevens worden opgeslagen in Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="0b029-108">How much data is stored in hello account.</span></span>

## <a name="enable-logging"></a><span data-ttu-id="0b029-109">Logboekregistratie inschakelen</span><span class="sxs-lookup"><span data-stu-id="0b029-109">Enable logging</span></span>

1. <span data-ttu-id="0b029-110">Meld u aan bij toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0b029-110">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="0b029-111">Uw Data Lake Analytics-account openen en selecteer **diagnostische logboeken** van Hallo __Monitor__ sectie.</span><span class="sxs-lookup"><span data-stu-id="0b029-111">Open your Data Lake Analytics account and select **Diagnostic logs** from hello __Monitor__ section.</span></span> <span data-ttu-id="0b029-112">Selecteer vervolgens __diagnostische gegevens inschakelen__.</span><span class="sxs-lookup"><span data-stu-id="0b029-112">Next, select __Turn on diagnostics__.</span></span>

    ![Schakel diagnostische gegevens toocollect audit en logboeken aanvragen](./media/data-lake-analytics-diagnostic-logs/turn-on-logging.png)

3. <span data-ttu-id="0b029-114">Van __diagnostische instellingen__, Hallo status too__On__ instellen en selecteert u opties voor logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="0b029-114">From __Diagnostics settings__, set hello status too__On__ and select logging options.</span></span>

    <span data-ttu-id="0b029-115">![Schakel diagnostische gegevens toocollect audit en logboeken aanvragen](./media/data-lake-analytics-diagnostic-logs/enable-diagnostic-logs.png "logboeken met diagnostische gegevens inschakelen")</span><span class="sxs-lookup"><span data-stu-id="0b029-115">![Turn on diagnostics toocollect audit and request logs](./media/data-lake-analytics-diagnostic-logs/enable-diagnostic-logs.png "Enable diagnostic logs")</span></span>

   * <span data-ttu-id="0b029-116">Stel **Status** te**op** tooenable Diagnostische logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="0b029-116">Set **Status** too**On** tooenable diagnostic logging.</span></span>

   * <span data-ttu-id="0b029-117">U kunt toostore/proces Hallo gegevens op drie verschillende manieren.</span><span class="sxs-lookup"><span data-stu-id="0b029-117">You can choose toostore/process hello data in three different ways.</span></span>

     * <span data-ttu-id="0b029-118">Selecteer __archiveren tooa opslagaccount__ toostore wordt geregistreerd in Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="0b029-118">Select __Archive tooa storage account__ toostore logs in an Azure storage account.</span></span> <span data-ttu-id="0b029-119">Gebruik deze optie als u tooarchive Hallo gegevens.</span><span class="sxs-lookup"><span data-stu-id="0b029-119">Use this option if you want tooarchive hello data.</span></span> <span data-ttu-id="0b029-120">Als u deze optie selecteert, moet u een Azure storage-account toosave Hallo logboeken naar opgeven.</span><span class="sxs-lookup"><span data-stu-id="0b029-120">If you select this option, you must provide an Azure storage account toosave hello logs to.</span></span>

     * <span data-ttu-id="0b029-121">Selecteer **tooan Event Hub Stream** toostream logboek gegevens tooan Azure Event Hub.</span><span class="sxs-lookup"><span data-stu-id="0b029-121">Select **Stream tooan Event Hub** toostream log data tooan Azure Event Hub.</span></span> <span data-ttu-id="0b029-122">Gebruik deze optie als u hebt een downstreamverwerking pijplijn die is binnenkomende Logboeken in realtime analyseren.</span><span class="sxs-lookup"><span data-stu-id="0b029-122">Use this option if you have a downstream processing pipeline that is analyzing incoming logs in real time.</span></span> <span data-ttu-id="0b029-123">Als u deze optie selecteert, moet u Hallo details opgeven voor hello Azure Event Hub die u wilt dat toouse.</span><span class="sxs-lookup"><span data-stu-id="0b029-123">If you select this option, you must provide hello details for hello Azure Event Hub you want toouse.</span></span>

     * <span data-ttu-id="0b029-124">Selecteer __tooLog Analytics verzenden__ toosend Hallo gegevens toohello Log Analytics-service.</span><span class="sxs-lookup"><span data-stu-id="0b029-124">Select __Send tooLog Analytics__ toosend hello data toohello Log Analytics service.</span></span> <span data-ttu-id="0b029-125">Gebruik deze optie als u wilt dat toouse logboekanalyse toogather en analyseren van Logboeken.</span><span class="sxs-lookup"><span data-stu-id="0b029-125">Use this option if you want toouse Log Analytics toogather and analyze logs.</span></span>
   * <span data-ttu-id="0b029-126">Geef op of u wilt dat de controlelogboeken tooget of Logboeken aanvragen of beide.</span><span class="sxs-lookup"><span data-stu-id="0b029-126">Specify whether you want tooget audit logs or request logs or both.</span></span>  <span data-ttu-id="0b029-127">Een aanvraag logboek worden vastgelegd elke API-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="0b029-127">A request log captures every API request.</span></span> <span data-ttu-id="0b029-128">Een controlelogboek registreert alle bewerkingen die worden geactiveerd door deze API-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="0b029-128">An audit log records all operations that are triggered by that API request.</span></span>

   * <span data-ttu-id="0b029-129">Voor __tooa opslagaccount archiveren__, geef het aantal dagen tooretain Hallo gegevens Hallo.</span><span class="sxs-lookup"><span data-stu-id="0b029-129">For __Archive tooa storage account__, specify hello number of days tooretain hello data.</span></span>

   * <span data-ttu-id="0b029-130">Klik op __Opslaan__.</span><span class="sxs-lookup"><span data-stu-id="0b029-130">Click __Save__.</span></span>

        > [!NOTE]
        > <span data-ttu-id="0b029-131">U moet een selecteren __archiveren tooa opslagaccount__, __Stream tooan Event Hub__ of __tooLog Analytics verzenden__ voordat u op Hallo __Opslaan__knop.</span><span class="sxs-lookup"><span data-stu-id="0b029-131">You must select either __Archive tooa storage account__, __Stream tooan Event Hub__ or __Send tooLog Analytics__ before clicking hello __Save__ button.</span></span>

<span data-ttu-id="0b029-132">Wanneer u de diagnostische instellingen hebt ingeschakeld, kunt u terugkeren toohello __diagnostische logboeken__ blade tooview Hallo Logboeken.</span><span class="sxs-lookup"><span data-stu-id="0b029-132">Once you have enabled diagnostic settings, you can return toohello __Diagnostics logs__ blade tooview hello logs.</span></span>

## <a name="view-logs"></a><span data-ttu-id="0b029-133">Logboeken bekijken</span><span class="sxs-lookup"><span data-stu-id="0b029-133">View logs</span></span>

### <a name="use-hello-data-lake-analytics-view"></a><span data-ttu-id="0b029-134">Hallo Data Lake Analytics-weergave gebruiken</span><span class="sxs-lookup"><span data-stu-id="0b029-134">Use hello Data Lake Analytics view</span></span>

1. <span data-ttu-id="0b029-135">Account van uw Data Lake Analytics blade onder **bewaking**, selecteer **diagnostische logboeken** en selecteer vervolgens een vermelding toodisplay logboeken voor.</span><span class="sxs-lookup"><span data-stu-id="0b029-135">From your Data Lake Analytics account blade, under **Monitoring**, select **Diagnostic Logs** and then select an entry toodisplay logs for.</span></span>

    <span data-ttu-id="0b029-136">![Diagnostische logboekregistratie weergave](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs.png "diagnostische logboeken bekijken")</span><span class="sxs-lookup"><span data-stu-id="0b029-136">![View diagnostic logging](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs.png "View diagnostic logs")</span></span>

2. <span data-ttu-id="0b029-137">Hallo logboeken worden ingedeeld in verschillende **controlelogboeken** en **aanvragen logboeken**.</span><span class="sxs-lookup"><span data-stu-id="0b029-137">hello logs are categorized by **Audit Logs** and **Request Logs**.</span></span>

    ![logboekvermeldingen](./media/data-lake-analytics-diagnostic-logs/diagnostic-log-entries.png)

   * <span data-ttu-id="0b029-139">Logboeken aanvragen vastleggen elk verzoek API op Hallo Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="0b029-139">Request logs capture every API request made on hello Data Lake Analytics account.</span></span>
   * <span data-ttu-id="0b029-140">Controlelogboeken zijn vergelijkbaar toorequest logboeken maar bieden een veel gedetailleerder verdeling van Hallo-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="0b029-140">Audit Logs are similar toorequest Logs but provide a much more detailed breakdown of hello operations.</span></span> <span data-ttu-id="0b029-141">Bijvoorbeeld, kan een API-aanroep voor het uploaden van één in een logboek met aanvragen resulteren in meerdere "Toevoegen" bewerkingen in het controlelogboek.</span><span class="sxs-lookup"><span data-stu-id="0b029-141">For example, a single upload API call in a request log can result in multiple "Append" operations in its audit log.</span></span>

3. <span data-ttu-id="0b029-142">Klik op Hallo **downloaden** koppeling voor een logboek vermelding toodownload die zich aanmelden.</span><span class="sxs-lookup"><span data-stu-id="0b029-142">Click hello **Download** link for a log entry toodownload that log.</span></span>

### <a name="use-hello-azure-storage-account-that-contains-log-data"></a><span data-ttu-id="0b029-143">Hello Azure Storage-account met logboekgegevens gebruiken</span><span class="sxs-lookup"><span data-stu-id="0b029-143">Use hello Azure Storage account that contains log data</span></span>

1. <span data-ttu-id="0b029-144">Open hello Azure Storage-accountblade die is gekoppeld met Data Lake Analytics voor logboekregistratie en klik vervolgens op __Blobs__.</span><span class="sxs-lookup"><span data-stu-id="0b029-144">Open hello Azure Storage account blade associated with Data Lake Analytics for logging, and then click __Blobs__.</span></span> <span data-ttu-id="0b029-145">Hallo **Blob-service** blade bevat twee containers.</span><span class="sxs-lookup"><span data-stu-id="0b029-145">hello **Blob service** blade lists two containers.</span></span>

    <span data-ttu-id="0b029-146">![Diagnostische logboekregistratie weergave](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs-storage-account.png "diagnostische logboeken bekijken")</span><span class="sxs-lookup"><span data-stu-id="0b029-146">![View diagnostic logging](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs-storage-account.png "View diagnostic logs")</span></span>

   * <span data-ttu-id="0b029-147">Hallo-container **insights-logboeken-controlegebeurtenissen** Hallo controlelogboeken bevat.</span><span class="sxs-lookup"><span data-stu-id="0b029-147">hello container **insights-logs-audit** contains hello audit logs.</span></span>
   * <span data-ttu-id="0b029-148">Hallo-container **insights-logboeken-aanvragen** Hallo aanvraag Logboeken bevat.</span><span class="sxs-lookup"><span data-stu-id="0b029-148">hello container **insights-logs-requests** contains hello request logs.</span></span>
2. <span data-ttu-id="0b029-149">In deze containers worden Hallo logboeken opgeslagen onder Hallo structuur te volgen:</span><span class="sxs-lookup"><span data-stu-id="0b029-149">Within these containers, hello logs are stored under hello following structure:</span></span>

        resourceId=/
          SUBSCRIPTIONS/
            <<SUBSCRIPTION_ID>>/
              RESOURCEGROUPS/
                <<RESOURCE_GRP_NAME>>/
                  PROVIDERS/
                    MICROSOFT.DATALAKEANALYTICS/
                      ACCOUNTS/
                        <DATA_LAKE_ANALYTICS_NAME>>/
                          y=####/
                            m=##/
                              d=##/
                                h=##/
                                  m=00/
                                    PT1H.json

   > [!NOTE]
   > <span data-ttu-id="0b029-150">Hallo `##` vermeldingen in Hallo pad bevatten Hallo jaar, maand, dag en uur in welke Hallo logboek is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0b029-150">hello `##` entries in hello path contain hello year, month, day, and hour in which hello log was created.</span></span> <span data-ttu-id="0b029-151">Data Lake Analytics maakt een bestand om het uur, dus `m=` bevat altijd een waarde van `00`.</span><span class="sxs-lookup"><span data-stu-id="0b029-151">Data Lake Analytics creates one file every hour, so `m=` always contains a value of `00`.</span></span>

    <span data-ttu-id="0b029-152">Hallo volledige pad tooan controlelogboek kan bijvoorbeeld worden:</span><span class="sxs-lookup"><span data-stu-id="0b029-152">As an example, hello complete path tooan audit log could be:</span></span>

        https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=04/m=00/PT1H.json

    <span data-ttu-id="0b029-153">Op deze manier kan logboek Hallo volledige pad tooa-aanvragen worden:</span><span class="sxs-lookup"><span data-stu-id="0b029-153">Similarly, hello complete path tooa request log could be:</span></span>

        https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=14/m=00/PT1H.json

## <a name="log-structure"></a><span data-ttu-id="0b029-154">Logboek-structuur</span><span class="sxs-lookup"><span data-stu-id="0b029-154">Log structure</span></span>

<span data-ttu-id="0b029-155">Hallo controle en aanvraag logboeken zijn in een gestructureerde JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="0b029-155">hello audit and request logs are in a structured JSON format.</span></span>

### <a name="request-logs"></a><span data-ttu-id="0b029-156">Logboeken aanvragen</span><span class="sxs-lookup"><span data-stu-id="0b029-156">Request logs</span></span>

<span data-ttu-id="0b029-157">Hier wordt een voorbeeldvermelding voor het registreren van de JSON-indeling verzoeken Hallo.</span><span class="sxs-lookup"><span data-stu-id="0b029-157">Here's a sample entry in hello JSON-formatted request log.</span></span> <span data-ttu-id="0b029-158">Elke blob heeft een basis-object aangeroepen **records** die een matrix van logboek-objecten bevat.</span><span class="sxs-lookup"><span data-stu-id="0b029-158">Each blob has one root object called **records** that contains an array of log objects.</span></span>

    {
    "records":
      [        
        . . . .
        ,
        {
             "time": "2016-07-07T21:02:53.456Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/<data_lake_analytics_account_name>",
             "category": "Requests",
             "operationName": "GetAggregatedJobHistory",
             "resultType": "200",
             "callerIpAddress": "::ffff:1.1.1.1",
             "correlationId": "4a11c709-05f5-417c-a98d-6e81b3e29c58",
             "identity": "1808bd5f-62af-45f4-89d8-03c5e81bac30",
             "properties": {
                 "HttpMethod":"POST",
                 "Path":"/JobAggregatedHistory",
                 "RequestContentLength":122,
                 "ClientRequestId":"3b7adbd9-3519-4f28-a61c-bd89506163b8",
                 "StartTime":"2016-07-07T21:02:52.472Z",
                 "EndTime":"2016-07-07T21:02:53.456Z"
                 }
        }
        ,
        . . . .
      ]
    }

#### <a name="request-log-schema"></a><span data-ttu-id="0b029-159">Schema voor aanvraag-logboek</span><span class="sxs-lookup"><span data-stu-id="0b029-159">Request log schema</span></span>

| <span data-ttu-id="0b029-160">Naam</span><span class="sxs-lookup"><span data-stu-id="0b029-160">Name</span></span> | <span data-ttu-id="0b029-161">Type</span><span class="sxs-lookup"><span data-stu-id="0b029-161">Type</span></span> | <span data-ttu-id="0b029-162">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0b029-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0b029-163">tijd</span><span class="sxs-lookup"><span data-stu-id="0b029-163">time</span></span> |<span data-ttu-id="0b029-164">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0b029-164">String</span></span> |<span data-ttu-id="0b029-165">Hallo tijdstempel (in UTC) van het Hallo-logboek</span><span class="sxs-lookup"><span data-stu-id="0b029-165">hello timestamp (in UTC) of hello log</span></span> |
| <span data-ttu-id="0b029-166">resourceId</span><span class="sxs-lookup"><span data-stu-id="0b029-166">resourceId</span></span> |<span data-ttu-id="0b029-167">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0b029-167">String</span></span> |<span data-ttu-id="0b029-168">Hallo-id van het Hallo-resource die werd plaats op</span><span class="sxs-lookup"><span data-stu-id="0b029-168">hello identifier of hello resource that operation took place on</span></span> |
| <span data-ttu-id="0b029-169">category</span><span class="sxs-lookup"><span data-stu-id="0b029-169">category</span></span> |<span data-ttu-id="0b029-170">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0b029-170">String</span></span> |<span data-ttu-id="0b029-171">Hallo logboek categorie.</span><span class="sxs-lookup"><span data-stu-id="0b029-171">hello log category.</span></span> <span data-ttu-id="0b029-172">Bijvoorbeeld: **aanvragen**.</span><span class="sxs-lookup"><span data-stu-id="0b029-172">For example, **Requests**.</span></span> |
| <span data-ttu-id="0b029-173">operationName</span><span class="sxs-lookup"><span data-stu-id="0b029-173">operationName</span></span> |<span data-ttu-id="0b029-174">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0b029-174">String</span></span> |<span data-ttu-id="0b029-175">Naam van Hallo-bewerking die wordt vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="0b029-175">Name of hello operation that is logged.</span></span> <span data-ttu-id="0b029-176">Bijvoorbeeld: GetAggregatedJobHistory.</span><span class="sxs-lookup"><span data-stu-id="0b029-176">For example, GetAggregatedJobHistory.</span></span> |
| <span data-ttu-id="0b029-177">resultType</span><span class="sxs-lookup"><span data-stu-id="0b029-177">resultType</span></span> |<span data-ttu-id="0b029-178">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0b029-178">String</span></span> |<span data-ttu-id="0b029-179">Hallo-status van Hallo bewerking, bijvoorbeeld 200.</span><span class="sxs-lookup"><span data-stu-id="0b029-179">hello status of hello operation, For example, 200.</span></span> |
| <span data-ttu-id="0b029-180">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="0b029-180">callerIpAddress</span></span> |<span data-ttu-id="0b029-181">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0b029-181">String</span></span> |<span data-ttu-id="0b029-182">Hallo IP-adres van de aanvraag Hallo Hallo-client</span><span class="sxs-lookup"><span data-stu-id="0b029-182">hello IP address of hello client making hello request</span></span> |
| <span data-ttu-id="0b029-183">correlationId</span><span class="sxs-lookup"><span data-stu-id="0b029-183">correlationId</span></span> |<span data-ttu-id="0b029-184">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0b029-184">String</span></span> |<span data-ttu-id="0b029-185">Hallo-id van Hallo logboek.</span><span class="sxs-lookup"><span data-stu-id="0b029-185">hello identifier of hello log.</span></span> <span data-ttu-id="0b029-186">Deze waarde kan worden gebruikt toogroup een set van gerelateerde logboekvermeldingen.</span><span class="sxs-lookup"><span data-stu-id="0b029-186">This value can be used toogroup a set of related log entries.</span></span> |
| <span data-ttu-id="0b029-187">identity</span><span class="sxs-lookup"><span data-stu-id="0b029-187">identity</span></span> |<span data-ttu-id="0b029-188">Object</span><span class="sxs-lookup"><span data-stu-id="0b029-188">Object</span></span> |<span data-ttu-id="0b029-189">Hallo-identiteit die Hallo-logboek is gegenereerd</span><span class="sxs-lookup"><span data-stu-id="0b029-189">hello identity that generated hello log</span></span> |
| <span data-ttu-id="0b029-190">properties</span><span class="sxs-lookup"><span data-stu-id="0b029-190">properties</span></span> |<span data-ttu-id="0b029-191">JSON</span><span class="sxs-lookup"><span data-stu-id="0b029-191">JSON</span></span> |<span data-ttu-id="0b029-192">Zie de volgende Hallo-sectie (aanvraag logboek eigenschappen schema) voor meer informatie</span><span class="sxs-lookup"><span data-stu-id="0b029-192">See hello next section (Request log properties schema) for details</span></span> |

#### <a name="request-log-properties-schema"></a><span data-ttu-id="0b029-193">Aanvraag logboek eigenschappen schema</span><span class="sxs-lookup"><span data-stu-id="0b029-193">Request log properties schema</span></span>

| <span data-ttu-id="0b029-194">Naam</span><span class="sxs-lookup"><span data-stu-id="0b029-194">Name</span></span> | <span data-ttu-id="0b029-195">Type</span><span class="sxs-lookup"><span data-stu-id="0b029-195">Type</span></span> | <span data-ttu-id="0b029-196">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0b029-196">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0b029-197">HttpMethod</span><span class="sxs-lookup"><span data-stu-id="0b029-197">HttpMethod</span></span> |<span data-ttu-id="0b029-198">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0b029-198">String</span></span> |<span data-ttu-id="0b029-199">Hallo HTTP-methode gebruikt voor Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="0b029-199">hello HTTP Method used for hello operation.</span></span> <span data-ttu-id="0b029-200">Bijvoorbeeld, ophalen.</span><span class="sxs-lookup"><span data-stu-id="0b029-200">For example, GET.</span></span> |
| <span data-ttu-id="0b029-201">Pad</span><span class="sxs-lookup"><span data-stu-id="0b029-201">Path</span></span> |<span data-ttu-id="0b029-202">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0b029-202">String</span></span> |<span data-ttu-id="0b029-203">Hallo pad Hallo-bewerking is uitgevoerd op</span><span class="sxs-lookup"><span data-stu-id="0b029-203">hello path hello operation was performed on</span></span> |
| <span data-ttu-id="0b029-204">RequestContentLength</span><span class="sxs-lookup"><span data-stu-id="0b029-204">RequestContentLength</span></span> |<span data-ttu-id="0b029-205">int</span><span class="sxs-lookup"><span data-stu-id="0b029-205">int</span></span> |<span data-ttu-id="0b029-206">Hallo inhoudslengte van Hallo HTTP-aanvraag</span><span class="sxs-lookup"><span data-stu-id="0b029-206">hello content length of hello HTTP request</span></span> |
| <span data-ttu-id="0b029-207">clientRequestId</span><span class="sxs-lookup"><span data-stu-id="0b029-207">ClientRequestId</span></span> |<span data-ttu-id="0b029-208">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0b029-208">String</span></span> |<span data-ttu-id="0b029-209">Hallo-id die is uniek voor deze aanvraag</span><span class="sxs-lookup"><span data-stu-id="0b029-209">hello identifier that uniquely identifies this request</span></span> |
| <span data-ttu-id="0b029-210">StartTime</span><span class="sxs-lookup"><span data-stu-id="0b029-210">StartTime</span></span> |<span data-ttu-id="0b029-211">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0b029-211">String</span></span> |<span data-ttu-id="0b029-212">Hallo tijdstip welke Hallo ontvangen Hallo serveraanvraag</span><span class="sxs-lookup"><span data-stu-id="0b029-212">hello time at which hello server received hello request</span></span> |
| <span data-ttu-id="0b029-213">Eindtijd</span><span class="sxs-lookup"><span data-stu-id="0b029-213">EndTime</span></span> |<span data-ttu-id="0b029-214">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0b029-214">String</span></span> |<span data-ttu-id="0b029-215">Hallo tijd welke Hallo-server een antwoord verzonden</span><span class="sxs-lookup"><span data-stu-id="0b029-215">hello time at which hello server sent a response</span></span> |

### <a name="audit-logs"></a><span data-ttu-id="0b029-216">Controlelogboeken</span><span class="sxs-lookup"><span data-stu-id="0b029-216">Audit logs</span></span>

<span data-ttu-id="0b029-217">Hier wordt een voorbeeldvermelding voor het controlelogboek van Hallo JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="0b029-217">Here's a sample entry in hello JSON-formatted audit log.</span></span> <span data-ttu-id="0b029-218">Elke blob heeft een basis-object aangeroepen **records** die een matrix van logboek-objecten bevat.</span><span class="sxs-lookup"><span data-stu-id="0b029-218">Each blob has one root object called **records** that contains an array of log objects.</span></span>

    {
    "records":
      [        
        . . . .
        ,
        {
             "time": "2016-07-28T19:15:16.245Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/<data_lake_ANALYTICS_account_name>",
             "category": "Audit",
             "operationName": "JobSubmitted",
             "identity": "user@somewhere.com",
             "properties": {
                 "JobId":"D74B928F-5194-4E6C-971F-C27026C290E6",
                 "JobName": "New Job",
                 "JobRuntimeName": "default",
                 "SubmitTime": "7/28/2016 7:14:57 PM"
                 }
        }
        ,
        . . . .
      ]
    }

#### <a name="audit-log-schema"></a><span data-ttu-id="0b029-219">Audit log schema</span><span class="sxs-lookup"><span data-stu-id="0b029-219">Audit log schema</span></span>

| <span data-ttu-id="0b029-220">Naam</span><span class="sxs-lookup"><span data-stu-id="0b029-220">Name</span></span> | <span data-ttu-id="0b029-221">Type</span><span class="sxs-lookup"><span data-stu-id="0b029-221">Type</span></span> | <span data-ttu-id="0b029-222">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0b029-222">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0b029-223">tijd</span><span class="sxs-lookup"><span data-stu-id="0b029-223">time</span></span> |<span data-ttu-id="0b029-224">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0b029-224">String</span></span> |<span data-ttu-id="0b029-225">Hallo tijdstempel (in UTC) van het Hallo-logboek</span><span class="sxs-lookup"><span data-stu-id="0b029-225">hello timestamp (in UTC) of hello log</span></span> |
| <span data-ttu-id="0b029-226">resourceId</span><span class="sxs-lookup"><span data-stu-id="0b029-226">resourceId</span></span> |<span data-ttu-id="0b029-227">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0b029-227">String</span></span> |<span data-ttu-id="0b029-228">Hallo-id van het Hallo-resource die werd plaats op</span><span class="sxs-lookup"><span data-stu-id="0b029-228">hello identifier of hello resource that operation took place on</span></span> |
| <span data-ttu-id="0b029-229">category</span><span class="sxs-lookup"><span data-stu-id="0b029-229">category</span></span> |<span data-ttu-id="0b029-230">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0b029-230">String</span></span> |<span data-ttu-id="0b029-231">Hallo logboek categorie.</span><span class="sxs-lookup"><span data-stu-id="0b029-231">hello log category.</span></span> <span data-ttu-id="0b029-232">Bijvoorbeeld: **Audit**.</span><span class="sxs-lookup"><span data-stu-id="0b029-232">For example, **Audit**.</span></span> |
| <span data-ttu-id="0b029-233">operationName</span><span class="sxs-lookup"><span data-stu-id="0b029-233">operationName</span></span> |<span data-ttu-id="0b029-234">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0b029-234">String</span></span> |<span data-ttu-id="0b029-235">Naam van Hallo-bewerking die wordt vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="0b029-235">Name of hello operation that is logged.</span></span> <span data-ttu-id="0b029-236">Bijvoorbeeld: JobSubmitted.</span><span class="sxs-lookup"><span data-stu-id="0b029-236">For example, JobSubmitted.</span></span> |
| <span data-ttu-id="0b029-237">resultType</span><span class="sxs-lookup"><span data-stu-id="0b029-237">resultType</span></span> |<span data-ttu-id="0b029-238">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0b029-238">String</span></span> |<span data-ttu-id="0b029-239">Een substatus voor taakstatus hello (operationName).</span><span class="sxs-lookup"><span data-stu-id="0b029-239">A substatus for hello job status (operationName).</span></span> |
| <span data-ttu-id="0b029-240">resultSignature</span><span class="sxs-lookup"><span data-stu-id="0b029-240">resultSignature</span></span> |<span data-ttu-id="0b029-241">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0b029-241">String</span></span> |<span data-ttu-id="0b029-242">Meer informatie over de status van de taak hello (operationName).</span><span class="sxs-lookup"><span data-stu-id="0b029-242">Additional details on hello job status (operationName).</span></span> |
| <span data-ttu-id="0b029-243">identity</span><span class="sxs-lookup"><span data-stu-id="0b029-243">identity</span></span> |<span data-ttu-id="0b029-244">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0b029-244">String</span></span> |<span data-ttu-id="0b029-245">Hallo-gebruiker die Hallo bewerking aangevraagd.</span><span class="sxs-lookup"><span data-stu-id="0b029-245">hello user that requested hello operation.</span></span> <span data-ttu-id="0b029-246">Bijvoorbeeld susan@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="0b029-246">For example, susan@contoso.com.</span></span> |
| <span data-ttu-id="0b029-247">properties</span><span class="sxs-lookup"><span data-stu-id="0b029-247">properties</span></span> |<span data-ttu-id="0b029-248">JSON</span><span class="sxs-lookup"><span data-stu-id="0b029-248">JSON</span></span> |<span data-ttu-id="0b029-249">Zie de volgende Hallo-sectie (schema Audit log-eigenschappen) voor meer informatie</span><span class="sxs-lookup"><span data-stu-id="0b029-249">See hello next section (Audit log properties schema) for details</span></span> |

> [!NOTE]
> <span data-ttu-id="0b029-250">**resultType** en **resultSignature** bieden informatie over het resultaat van een bewerking Hallo en alleen een waarde bevatten als een bewerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="0b029-250">**resultType** and **resultSignature** provide information on hello result of an operation, and only contain a value if an operation has completed.</span></span> <span data-ttu-id="0b029-251">Bijvoorbeeld, ze alleen bevatten een waarde wanneer **operationName** bevat een waarde van **JobStarted** of **JobEnded**.</span><span class="sxs-lookup"><span data-stu-id="0b029-251">For example, they only contain a value when **operationName** contains a value of **JobStarted** or **JobEnded**.</span></span>
>
>

#### <a name="audit-log-properties-schema"></a><span data-ttu-id="0b029-252">Audit log eigenschappen schema</span><span class="sxs-lookup"><span data-stu-id="0b029-252">Audit log properties schema</span></span>

| <span data-ttu-id="0b029-253">Naam</span><span class="sxs-lookup"><span data-stu-id="0b029-253">Name</span></span> | <span data-ttu-id="0b029-254">Type</span><span class="sxs-lookup"><span data-stu-id="0b029-254">Type</span></span> | <span data-ttu-id="0b029-255">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0b029-255">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0b029-256">JobId</span><span class="sxs-lookup"><span data-stu-id="0b029-256">JobId</span></span> |<span data-ttu-id="0b029-257">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0b029-257">String</span></span> |<span data-ttu-id="0b029-258">Hallo-ID toegewezen toohello taak</span><span class="sxs-lookup"><span data-stu-id="0b029-258">hello ID assigned toohello job</span></span> |
| <span data-ttu-id="0b029-259">Taaknaam</span><span class="sxs-lookup"><span data-stu-id="0b029-259">JobName</span></span> |<span data-ttu-id="0b029-260">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0b029-260">String</span></span> |<span data-ttu-id="0b029-261">Hallo-naam die is opgegeven voor het Hallo-taak</span><span class="sxs-lookup"><span data-stu-id="0b029-261">hello name that was provided for hello job</span></span> |
| <span data-ttu-id="0b029-262">JobRunTime</span><span class="sxs-lookup"><span data-stu-id="0b029-262">JobRunTime</span></span> |<span data-ttu-id="0b029-263">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0b029-263">String</span></span> |<span data-ttu-id="0b029-264">Hallo runtime tooprocess Hallo taak gebruikt</span><span class="sxs-lookup"><span data-stu-id="0b029-264">hello runtime used tooprocess hello job</span></span> |
| <span data-ttu-id="0b029-265">SubmitTime</span><span class="sxs-lookup"><span data-stu-id="0b029-265">SubmitTime</span></span> |<span data-ttu-id="0b029-266">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0b029-266">String</span></span> |<span data-ttu-id="0b029-267">Hallo-tijd (in UTC) die Hallo-taak is verzonden</span><span class="sxs-lookup"><span data-stu-id="0b029-267">hello time (in UTC) that hello job was submitted</span></span> |
| <span data-ttu-id="0b029-268">StartTime</span><span class="sxs-lookup"><span data-stu-id="0b029-268">StartTime</span></span> |<span data-ttu-id="0b029-269">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0b029-269">String</span></span> |<span data-ttu-id="0b029-270">Hallo tijd Hallo taak is gestart na het indienen (in UTC)</span><span class="sxs-lookup"><span data-stu-id="0b029-270">hello time hello job started running after submission (in UTC)</span></span> |
| <span data-ttu-id="0b029-271">Eindtijd</span><span class="sxs-lookup"><span data-stu-id="0b029-271">EndTime</span></span> |<span data-ttu-id="0b029-272">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0b029-272">String</span></span> |<span data-ttu-id="0b029-273">Hallo tijd Hallo taak is beëindigd</span><span class="sxs-lookup"><span data-stu-id="0b029-273">hello time hello job ended</span></span> |
| <span data-ttu-id="0b029-274">Parallelle uitvoering</span><span class="sxs-lookup"><span data-stu-id="0b029-274">Parallelism</span></span> |<span data-ttu-id="0b029-275">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0b029-275">String</span></span> |<span data-ttu-id="0b029-276">Hallo aantal aangevraagd voor deze taak tijdens het indienen van Data Lake Analytics-eenheden</span><span class="sxs-lookup"><span data-stu-id="0b029-276">hello number of Data Lake Analytics units requested for this job during submission</span></span> |

> [!NOTE]
> <span data-ttu-id="0b029-277">**SubmitTime**, **StartTime**, **EndTime**, en **parallelle uitvoering** bieden informatie over een bewerking.</span><span class="sxs-lookup"><span data-stu-id="0b029-277">**SubmitTime**, **StartTime**, **EndTime**, and **Parallelism** provide information on an operation.</span></span> <span data-ttu-id="0b029-278">Deze vermeldingen alleen een waarde bevatten als die opnieuw is gestart of voltooid.</span><span class="sxs-lookup"><span data-stu-id="0b029-278">These entries only contain a value if that operation has started or completed.</span></span> <span data-ttu-id="0b029-279">Bijvoorbeeld: **SubmitTime** bevat alleen een waarde na **operationName** heeft Hallo waarde **JobSubmitted**.</span><span class="sxs-lookup"><span data-stu-id="0b029-279">For example, **SubmitTime** only contains a value after **operationName** has hello value **JobSubmitted**.</span></span>

## <a name="process-hello-log-data"></a><span data-ttu-id="0b029-280">Processen Hallo logboekgegevens</span><span class="sxs-lookup"><span data-stu-id="0b029-280">Process hello log data</span></span>

<span data-ttu-id="0b029-281">Azure Data Lake Analytics bevat een voorbeeld over het tooprocess Hallo logboekgegevens en analyseren.</span><span class="sxs-lookup"><span data-stu-id="0b029-281">Azure Data Lake Analytics provides a sample on how tooprocess and analyze hello log data.</span></span> <span data-ttu-id="0b029-282">U vindt Hallo voorbeeld op [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span><span class="sxs-lookup"><span data-stu-id="0b029-282">You can find hello sample at [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0b029-283">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0b029-283">Next steps</span></span>
* [<span data-ttu-id="0b029-284">Overzicht van Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="0b029-284">Overview of Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
