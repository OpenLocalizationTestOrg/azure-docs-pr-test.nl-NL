---
title: Logboeken met diagnostische gegevens voor Azure Data Lake Store weergeven | Microsoft Docs
description: 'Begrijpen hoe instellen en toegang tot diagnoselogboeken voor Azure Data Lake Store '
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: f6e75eb1-d0ae-47cf-bdb8-06684b7c0a94
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: b7a38ec445ef0ce13f3f1931e8ee246dce6412a5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-store"></a><span data-ttu-id="c0616-103">Toegang tot diagnoselogboeken voor Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="c0616-103">Accessing diagnostic logs for Azure Data Lake Store</span></span>
<span data-ttu-id="c0616-104">Meer informatie over het vastleggen van diagnostische gegevens voor uw Data Lake Store-account inschakelen en weergeven van de logboeken die worden verzameld voor uw account.</span><span class="sxs-lookup"><span data-stu-id="c0616-104">Learn about how to enable diagnostic logging for your Data Lake Store account and how to view the logs collected for your account.</span></span>

<span data-ttu-id="c0616-105">Organisaties kunnen diagnostische logboekregistratie inschakelen voor hun Azure Data Lake Store-account voor het verzamelen van gegevens audittrails voor bestandstoegang, waarmee informatie, zoals de lijst van gebruikers die toegang tot de gegevens, hoe vaak de gegevens worden gebruikt, hoeveel gegevens worden opgeslagen in het account enz.</span><span class="sxs-lookup"><span data-stu-id="c0616-105">Organizations can enable diagnostic logging for their Azure Data Lake Store account to collect data access audit trails that provides information such as list of users accessing the data, how frequently the data is accessed, how much data is stored in the account, etc.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c0616-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c0616-106">Prerequisites</span></span>
* <span data-ttu-id="c0616-107">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="c0616-107">**An Azure subscription**.</span></span> <span data-ttu-id="c0616-108">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c0616-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="c0616-109">**Azure Data Lake Store-account**.</span><span class="sxs-lookup"><span data-stu-id="c0616-109">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="c0616-110">Volg de instructies in [Aan de slag met Azure Data Lake Store met Azure Portal](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c0616-110">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](data-lake-store-get-started-portal.md).</span></span>

## <a name="enable-diagnostic-logging-for-your-data-lake-store-account"></a><span data-ttu-id="c0616-111">Diagnostische logboekregistratie inschakelen voor uw Data Lake Store-account</span><span class="sxs-lookup"><span data-stu-id="c0616-111">Enable diagnostic logging for your Data Lake Store account</span></span>
1. <span data-ttu-id="c0616-112">Meld u aan bij de nieuwe [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c0616-112">Sign on to the new [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c0616-113">Open uw Data Lake Store-account en klik op de blade van het Data Lake Store-account **instellingen**, en klik vervolgens op **diagnostische logboeken**.</span><span class="sxs-lookup"><span data-stu-id="c0616-113">Open your Data Lake Store account, and from your Data Lake Store account blade, click **Settings**, and then click **Diagnostic logs**.</span></span>
3. <span data-ttu-id="c0616-114">In de **diagnostische logboeken** blade, klikt u op **diagnostische gegevens inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="c0616-114">In the **Diagnostics logs** blade, click **Turn on diagnostics**.</span></span>

    <span data-ttu-id="c0616-115">![Diagnostische logboekregistratie inschakelen](./media/data-lake-store-diagnostic-logs/turn-on-diagnostics.png "logboeken met diagnostische gegevens inschakelen")</span><span class="sxs-lookup"><span data-stu-id="c0616-115">![Enable diagnostic logging](./media/data-lake-store-diagnostic-logs/turn-on-diagnostics.png "Enable diagnostic logs")</span></span>

3. <span data-ttu-id="c0616-116">In de **diagnostische** blade Breng de volgende wijzigingen Diagnostische logboekregistratie configureren.</span><span class="sxs-lookup"><span data-stu-id="c0616-116">In the **Diagnostic** blade, make the following changes to configure diagnostic logging.</span></span>
   
    <span data-ttu-id="c0616-117">![Diagnostische logboekregistratie inschakelen](./media/data-lake-store-diagnostic-logs/enable-diagnostic-logs.png "logboeken met diagnostische gegevens inschakelen")</span><span class="sxs-lookup"><span data-stu-id="c0616-117">![Enable diagnostic logging](./media/data-lake-store-diagnostic-logs/enable-diagnostic-logs.png "Enable diagnostic logs")</span></span>
   
   * <span data-ttu-id="c0616-118">Stel **Status** naar **op** Diagnostische logboekregistratie in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="c0616-118">Set **Status** to **On** to enable diagnostic logging.</span></span>
   * <span data-ttu-id="c0616-119">U kunt kiezen om te verwerken/store de gegevens op verschillende manieren.</span><span class="sxs-lookup"><span data-stu-id="c0616-119">You can choose to store/process the data in different ways.</span></span>
     
        * <span data-ttu-id="c0616-120">Selecteer de optie voor **archiveren naar een opslagaccount** voor het opslaan van Logboeken voor een Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="c0616-120">Select the option to **Archive to a storage account** to store logs to an Azure Storage account.</span></span> <span data-ttu-id="c0616-121">U gebruikt deze optie als u wilt archiveren van de gegevens die batch verwerkt op een later tijdstip worden.</span><span class="sxs-lookup"><span data-stu-id="c0616-121">You use this option if you want to archive the data that will be batch-processed at a later date.</span></span> <span data-ttu-id="c0616-122">Als u deze optie selecteert, moet u een Azure Storage-account voor het opslaan van de logboeken naar opgeven.</span><span class="sxs-lookup"><span data-stu-id="c0616-122">If you select this option you must provide an Azure Storage account to save the logs to.</span></span>
        
        * <span data-ttu-id="c0616-123">Selecteer de optie voor **Stream naar een event hub** stroom logboek gegevens naar een Azure Event Hub.</span><span class="sxs-lookup"><span data-stu-id="c0616-123">Select the option to **Stream to an event hub** to stream log data to an Azure Event Hub.</span></span> <span data-ttu-id="c0616-124">Zeer waarschijnlijk zal gebruik deze optie als u een pijplijn downstreamverwerking binnenkomende Logboeken in realtime analyseren.</span><span class="sxs-lookup"><span data-stu-id="c0616-124">Most likely you will use this option if you have a downstream processing pipeline to analyze incoming logs at real time.</span></span> <span data-ttu-id="c0616-125">Als u deze optie selecteert, moet u de details opgeven voor de Azure Event Hub die u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c0616-125">If you select this option, you must provide the details for the Azure Event Hub you want to use.</span></span>

        * <span data-ttu-id="c0616-126">Selecteer de optie voor **verzenden met logboekanalyse** om de Azure Log Analytics-service gebruiken voor het analyseren van de gegenereerde logboekgegevens.</span><span class="sxs-lookup"><span data-stu-id="c0616-126">Select the option to **Send to Log Analytics** to use the Azure Log Analytics service to analyze the generated log data.</span></span> <span data-ttu-id="c0616-127">Als u deze optie selecteert, moet u de details opgeven voor de Operations Management Suite-werkruimte dat zou u de logboekanalyse uitvoeren is.</span><span class="sxs-lookup"><span data-stu-id="c0616-127">If you select this option, you must provide the details for the Operations Management Suite workspace that you would use the perform log analysis.</span></span>
     
   * <span data-ttu-id="c0616-128">Geef op of u wilt ophalen controlelogboeken of Logboeken aanvragen of beide.</span><span class="sxs-lookup"><span data-stu-id="c0616-128">Specify whether you want to get audit logs or request logs or both.</span></span>
   * <span data-ttu-id="c0616-129">Geef het aantal dagen waarvoor de gegevens moeten worden bewaard.</span><span class="sxs-lookup"><span data-stu-id="c0616-129">Specify the number of days for which the data must be retained.</span></span> <span data-ttu-id="c0616-130">Bewaartermijn is alleen van toepassing als u Azure storage-account gebruikt voor het archiveren van gegevens aan het logboek.</span><span class="sxs-lookup"><span data-stu-id="c0616-130">Retention is only applicable if you are using Azure storage account to archive log data.</span></span>
   * <span data-ttu-id="c0616-131">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c0616-131">Click **Save**.</span></span>

<span data-ttu-id="c0616-132">Wanneer u de diagnostische instellingen hebt ingeschakeld, kunt u bekijken in de logboekbestanden in de **diagnostische logboeken** tabblad.</span><span class="sxs-lookup"><span data-stu-id="c0616-132">Once you have enabled diagnostic settings, you can watch the logs in the **Diagnostic Logs** tab.</span></span>

## <a name="view-diagnostic-logs-for-your-data-lake-store-account"></a><span data-ttu-id="c0616-133">Diagnostische logboeken bekijken voor uw Data Lake Store-account</span><span class="sxs-lookup"><span data-stu-id="c0616-133">View diagnostic logs for your Data Lake Store account</span></span>
<span data-ttu-id="c0616-134">Er zijn twee manieren om de logboekgegevens voor uw Data Lake Store-account weer te geven.</span><span class="sxs-lookup"><span data-stu-id="c0616-134">There are two ways to view the log data for your Data Lake Store account.</span></span>

* <span data-ttu-id="c0616-135">Vanuit de weergave-instellingen van Data Lake Store-account</span><span class="sxs-lookup"><span data-stu-id="c0616-135">From the Data Lake Store account settings view</span></span>
* <span data-ttu-id="c0616-136">Vanuit het Azure-opslagaccount waar de gegevens worden opgeslagen</span><span class="sxs-lookup"><span data-stu-id="c0616-136">From the Azure Storage account where the data is stored</span></span>

### <a name="using-the-data-lake-store-settings-view"></a><span data-ttu-id="c0616-137">De weergave van Data Lake Store-instellingen</span><span class="sxs-lookup"><span data-stu-id="c0616-137">Using the Data Lake Store Settings view</span></span>
1. <span data-ttu-id="c0616-138">Van uw Data Lake Store-account **instellingen** blade, klikt u op **diagnostische logboeken**.</span><span class="sxs-lookup"><span data-stu-id="c0616-138">From your Data Lake Store account **Settings** blade, click **Diagnostic Logs**.</span></span>
   
    <span data-ttu-id="c0616-139">![Diagnostische logboekregistratie weergave](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs.png "diagnostische logboeken bekijken")</span><span class="sxs-lookup"><span data-stu-id="c0616-139">![View diagnostic logging](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs.png "View diagnostic logs")</span></span> 
2. <span data-ttu-id="c0616-140">In de **diagnostische logboeken** blade ziet u de logboeken door gecategoriseerd **controlelogboeken** en **aanvragen logboeken**.</span><span class="sxs-lookup"><span data-stu-id="c0616-140">In the **Diagnostic Logs** blade, you should see the logs categorized by **Audit Logs** and **Request Logs**.</span></span>
   
   * <span data-ttu-id="c0616-141">Logboeken aanvragen vastleggen elk verzoek API op het Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="c0616-141">Request logs capture every API request made on the Data Lake Store account.</span></span>
   * <span data-ttu-id="c0616-142">Controlelogboeken zijn vergelijkbaar met Logboeken aanvragen, maar bieden een veel gedetailleerder verdeling van de bewerkingen die worden uitgevoerd op het Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="c0616-142">Audit Logs are similar to request Logs but provide a much more detailed breakdown of the operations being performed on the Data Lake Store account.</span></span> <span data-ttu-id="c0616-143">Bijvoorbeeld, kan een API-aanroep voor één upload in Logboeken van de aanvraag leiden tot meerdere "Toevoegen" bewerkingen in de controlelogboeken.</span><span class="sxs-lookup"><span data-stu-id="c0616-143">For example, a single upload API call in request logs might result in multiple "Append" operations in the audit logs.</span></span>
3. <span data-ttu-id="c0616-144">Klik op de **downloaden** link tegen elke logboekvermelding om de logboeken te downloaden.</span><span class="sxs-lookup"><span data-stu-id="c0616-144">Click the **Download** link against each log entry to download the logs.</span></span>

### <a name="from-the-azure-storage-account-that-contains-log-data"></a><span data-ttu-id="c0616-145">Vanuit het Azure-opslagaccount waarin de logboekgegevens</span><span class="sxs-lookup"><span data-stu-id="c0616-145">From the Azure Storage account that contains log data</span></span>
1. <span data-ttu-id="c0616-146">Open de blade van Azure Storage-account die zijn gekoppeld met Data Lake Store voor logboekregistratie en klik op Blobs.</span><span class="sxs-lookup"><span data-stu-id="c0616-146">Open the Azure Storage account blade associated with Data Lake Store for logging, and then click Blobs.</span></span> <span data-ttu-id="c0616-147">De **Blob-service** blade bevat twee containers.</span><span class="sxs-lookup"><span data-stu-id="c0616-147">The **Blob service** blade lists two containers.</span></span>
   
    <span data-ttu-id="c0616-148">![Diagnostische logboekregistratie weergave](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account.png "diagnostische logboeken bekijken")</span><span class="sxs-lookup"><span data-stu-id="c0616-148">![View diagnostic logging](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account.png "View diagnostic logs")</span></span>
   
   * <span data-ttu-id="c0616-149">De container **insights-logboeken-controlegebeurtenissen** bevat de controlelogboeken.</span><span class="sxs-lookup"><span data-stu-id="c0616-149">The container **insights-logs-audit** contains the audit logs.</span></span>
   * <span data-ttu-id="c0616-150">De container **insights-logboeken-aanvragen** bevat de logboeken van de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="c0616-150">The container **insights-logs-requests** contains the request logs.</span></span>
2. <span data-ttu-id="c0616-151">De logboeken worden binnen deze containers in de volgende structuur opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="c0616-151">Within these containers, the logs are stored under the following structure.</span></span>
   
    <span data-ttu-id="c0616-152">![Diagnostische logboekregistratie weergave](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account-structure.png "diagnostische logboeken bekijken")</span><span class="sxs-lookup"><span data-stu-id="c0616-152">![View diagnostic logging](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account-structure.png "View diagnostic logs")</span></span>
   
    <span data-ttu-id="c0616-153">Als u bijvoorbeeld kan het volledige pad naar een controlelogboek worden`https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=04/m=00/PT1H.json`</span><span class="sxs-lookup"><span data-stu-id="c0616-153">As an example, the complete path to an audit log could be `https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=04/m=00/PT1H.json`</span></span>
   
    <span data-ttu-id="c0616-154">Similary, het volledige pad naar een logboek met aanvragen kan worden`https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=14/m=00/PT1H.json`</span><span class="sxs-lookup"><span data-stu-id="c0616-154">Similary, the complete path to a request log could be `https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=14/m=00/PT1H.json`</span></span>

## <a name="understand-the-structure-of-the-log-data"></a><span data-ttu-id="c0616-155">De structuur van de logboekgegevens begrijpen</span><span class="sxs-lookup"><span data-stu-id="c0616-155">Understand the structure of the log data</span></span>
<span data-ttu-id="c0616-156">Logboeken van de audit en aanvraag zijn in een JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="c0616-156">The audit and request logs are in a JSON format.</span></span> <span data-ttu-id="c0616-157">In deze sectie we kijken naar de JSON-structuur voor aanvraag en controlelogboeken.</span><span class="sxs-lookup"><span data-stu-id="c0616-157">In this section, we look at the structure of JSON for request and audit logs.</span></span>

### <a name="request-logs"></a><span data-ttu-id="c0616-158">Logboeken aanvragen</span><span class="sxs-lookup"><span data-stu-id="c0616-158">Request logs</span></span>
<span data-ttu-id="c0616-159">Hier volgt een voorbeeldvermelding voor het in het logboek voor aanvraag JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="c0616-159">Here's a sample entry in the JSON-formatted request log.</span></span> <span data-ttu-id="c0616-160">Elke blob heeft een basis-object aangeroepen **records** die een matrix van logboek-objecten bevat.</span><span class="sxs-lookup"><span data-stu-id="c0616-160">Each blob has one root object called **records** that contains an array of log objects.</span></span>

    {
    "records": 
      [        
        . . . .
        ,
        {
             "time": "2016-07-07T21:02:53.456Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Requests",
             "operationName": "GETCustomerIngressEgress",
             "resultType": "200",
             "callerIpAddress": "::ffff:1.1.1.1",
             "correlationId": "4a11c709-05f5-417c-a98d-6e81b3e29c58",
             "identity": "1808bd5f-62af-45f4-89d8-03c5e81bac30",
             "properties": {"HttpMethod":"GET","Path":"/webhdfs/v1/Samples/Outputs/Drivers.csv","RequestContentLength":0,"ClientRequestId":"3b7adbd9-3519-4f28-a61c-bd89506163b8","StartTime":"2016-07-07T21:02:52.472Z","EndTime":"2016-07-07T21:02:53.456Z"}
        }
        ,
        . . . .
      ]
    }

#### <a name="request-log-schema"></a><span data-ttu-id="c0616-161">Schema voor aanvraag-logboek</span><span class="sxs-lookup"><span data-stu-id="c0616-161">Request log schema</span></span>
| <span data-ttu-id="c0616-162">Naam</span><span class="sxs-lookup"><span data-stu-id="c0616-162">Name</span></span> | <span data-ttu-id="c0616-163">Type</span><span class="sxs-lookup"><span data-stu-id="c0616-163">Type</span></span> | <span data-ttu-id="c0616-164">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c0616-164">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c0616-165">tijd</span><span class="sxs-lookup"><span data-stu-id="c0616-165">time</span></span> |<span data-ttu-id="c0616-166">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c0616-166">String</span></span> |<span data-ttu-id="c0616-167">De tijdstempel (in UTC) van het logboek</span><span class="sxs-lookup"><span data-stu-id="c0616-167">The timestamp (in UTC) of the log</span></span> |
| <span data-ttu-id="c0616-168">resourceId</span><span class="sxs-lookup"><span data-stu-id="c0616-168">resourceId</span></span> |<span data-ttu-id="c0616-169">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c0616-169">String</span></span> |<span data-ttu-id="c0616-170">De ID van de resource die bewerking vond plaats op</span><span class="sxs-lookup"><span data-stu-id="c0616-170">The ID of the resource that operation took place on</span></span> |
| <span data-ttu-id="c0616-171">category</span><span class="sxs-lookup"><span data-stu-id="c0616-171">category</span></span> |<span data-ttu-id="c0616-172">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c0616-172">String</span></span> |<span data-ttu-id="c0616-173">De logboek-categorie.</span><span class="sxs-lookup"><span data-stu-id="c0616-173">The log category.</span></span> <span data-ttu-id="c0616-174">Bijvoorbeeld: **aanvragen**.</span><span class="sxs-lookup"><span data-stu-id="c0616-174">For example, **Requests**.</span></span> |
| <span data-ttu-id="c0616-175">operationName</span><span class="sxs-lookup"><span data-stu-id="c0616-175">operationName</span></span> |<span data-ttu-id="c0616-176">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c0616-176">String</span></span> |<span data-ttu-id="c0616-177">De naam van de bewerking die wordt vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="c0616-177">Name of the operation that is logged.</span></span> <span data-ttu-id="c0616-178">Bijvoorbeeld: getfilestatus.</span><span class="sxs-lookup"><span data-stu-id="c0616-178">For example, getfilestatus.</span></span> |
| <span data-ttu-id="c0616-179">resultType</span><span class="sxs-lookup"><span data-stu-id="c0616-179">resultType</span></span> |<span data-ttu-id="c0616-180">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c0616-180">String</span></span> |<span data-ttu-id="c0616-181">De status van de bewerking, bijvoorbeeld 200.</span><span class="sxs-lookup"><span data-stu-id="c0616-181">The status of the operation, For example, 200.</span></span> |
| <span data-ttu-id="c0616-182">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="c0616-182">callerIpAddress</span></span> |<span data-ttu-id="c0616-183">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c0616-183">String</span></span> |<span data-ttu-id="c0616-184">Het IP-adres van de client die de aanvraag</span><span class="sxs-lookup"><span data-stu-id="c0616-184">The IP address of the client making the request</span></span> |
| <span data-ttu-id="c0616-185">correlationId</span><span class="sxs-lookup"><span data-stu-id="c0616-185">correlationId</span></span> |<span data-ttu-id="c0616-186">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c0616-186">String</span></span> |<span data-ttu-id="c0616-187">De id van het logboek dat kan worden gebruikt om een set van gerelateerde logboekvermeldingen groepen</span><span class="sxs-lookup"><span data-stu-id="c0616-187">The id of the log that can used to group together a set of related log entries</span></span> |
| <span data-ttu-id="c0616-188">identity</span><span class="sxs-lookup"><span data-stu-id="c0616-188">identity</span></span> |<span data-ttu-id="c0616-189">Object</span><span class="sxs-lookup"><span data-stu-id="c0616-189">Object</span></span> |<span data-ttu-id="c0616-190">De identiteit die door het logboek is gegenereerd</span><span class="sxs-lookup"><span data-stu-id="c0616-190">The identity that generated the log</span></span> |
| <span data-ttu-id="c0616-191">properties</span><span class="sxs-lookup"><span data-stu-id="c0616-191">properties</span></span> |<span data-ttu-id="c0616-192">JSON</span><span class="sxs-lookup"><span data-stu-id="c0616-192">JSON</span></span> |<span data-ttu-id="c0616-193">Zie hieronder voor meer informatie</span><span class="sxs-lookup"><span data-stu-id="c0616-193">See below for details</span></span> |

#### <a name="request-log-properties-schema"></a><span data-ttu-id="c0616-194">Aanvraag logboek eigenschappen schema</span><span class="sxs-lookup"><span data-stu-id="c0616-194">Request log properties schema</span></span>
| <span data-ttu-id="c0616-195">Naam</span><span class="sxs-lookup"><span data-stu-id="c0616-195">Name</span></span> | <span data-ttu-id="c0616-196">Type</span><span class="sxs-lookup"><span data-stu-id="c0616-196">Type</span></span> | <span data-ttu-id="c0616-197">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c0616-197">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c0616-198">HttpMethod</span><span class="sxs-lookup"><span data-stu-id="c0616-198">HttpMethod</span></span> |<span data-ttu-id="c0616-199">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c0616-199">String</span></span> |<span data-ttu-id="c0616-200">De HTTP-methode gebruikt voor het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="c0616-200">The HTTP Method used for the operation.</span></span> <span data-ttu-id="c0616-201">Bijvoorbeeld, ophalen.</span><span class="sxs-lookup"><span data-stu-id="c0616-201">For example, GET.</span></span> |
| <span data-ttu-id="c0616-202">Pad</span><span class="sxs-lookup"><span data-stu-id="c0616-202">Path</span></span> |<span data-ttu-id="c0616-203">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c0616-203">String</span></span> |<span data-ttu-id="c0616-204">Het pad van de bewerking is uitgevoerd op</span><span class="sxs-lookup"><span data-stu-id="c0616-204">The path the operation was performed on</span></span> |
| <span data-ttu-id="c0616-205">RequestContentLength</span><span class="sxs-lookup"><span data-stu-id="c0616-205">RequestContentLength</span></span> |<span data-ttu-id="c0616-206">int</span><span class="sxs-lookup"><span data-stu-id="c0616-206">int</span></span> |<span data-ttu-id="c0616-207">De lengte van de inhoud van de HTTP-aanvraag</span><span class="sxs-lookup"><span data-stu-id="c0616-207">The content length of the HTTP request</span></span> |
| <span data-ttu-id="c0616-208">clientRequestId</span><span class="sxs-lookup"><span data-stu-id="c0616-208">ClientRequestId</span></span> |<span data-ttu-id="c0616-209">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c0616-209">String</span></span> |<span data-ttu-id="c0616-210">De Id die is uniek voor deze aanvraag</span><span class="sxs-lookup"><span data-stu-id="c0616-210">The Id that uniquely identifies this request</span></span> |
| <span data-ttu-id="c0616-211">StartTime</span><span class="sxs-lookup"><span data-stu-id="c0616-211">StartTime</span></span> |<span data-ttu-id="c0616-212">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c0616-212">String</span></span> |<span data-ttu-id="c0616-213">Het tijdstip waarop de server de aanvraag ontvangen</span><span class="sxs-lookup"><span data-stu-id="c0616-213">The time at which the server received the request</span></span> |
| <span data-ttu-id="c0616-214">Eindtijd</span><span class="sxs-lookup"><span data-stu-id="c0616-214">EndTime</span></span> |<span data-ttu-id="c0616-215">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c0616-215">String</span></span> |<span data-ttu-id="c0616-216">Het tijdstip waarop de server een antwoord verzonden</span><span class="sxs-lookup"><span data-stu-id="c0616-216">The time at which the server sent a response</span></span> |

### <a name="audit-logs"></a><span data-ttu-id="c0616-217">Controlelogboeken</span><span class="sxs-lookup"><span data-stu-id="c0616-217">Audit logs</span></span>
<span data-ttu-id="c0616-218">Hier wordt een voorbeeldvermelding voor het controlelogboek met JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="c0616-218">Here's a sample entry in the JSON-formatted audit log.</span></span> <span data-ttu-id="c0616-219">Elke blob heeft een basis-object aangeroepen **records** die een matrix van logboek-objecten bevat</span><span class="sxs-lookup"><span data-stu-id="c0616-219">Each blob has one root object called **records** that contains an array of log objects</span></span>

    {
    "records": 
      [        
        . . . .
        ,
        {
             "time": "2016-07-08T19:08:59.359Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Audit",
             "operationName": "SeOpenStream",
             "resultType": "0",
             "correlationId": "381110fc03534e1cb99ec52376ceebdf;Append_BrEKAmg;25.66.9.145",
             "identity": "A9DAFFAF-FFEE-4BB5-A4A0-1B6CBBF24355",
             "properties": {"StreamName":"adl://<data_lake_store_account_name>.azuredatalakestore.net/logs.csv"}
        }
        ,
        . . . .
      ]
    }

#### <a name="audit-log-schema"></a><span data-ttu-id="c0616-220">Audit log schema</span><span class="sxs-lookup"><span data-stu-id="c0616-220">Audit log schema</span></span>
| <span data-ttu-id="c0616-221">Naam</span><span class="sxs-lookup"><span data-stu-id="c0616-221">Name</span></span> | <span data-ttu-id="c0616-222">Type</span><span class="sxs-lookup"><span data-stu-id="c0616-222">Type</span></span> | <span data-ttu-id="c0616-223">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c0616-223">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c0616-224">tijd</span><span class="sxs-lookup"><span data-stu-id="c0616-224">time</span></span> |<span data-ttu-id="c0616-225">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c0616-225">String</span></span> |<span data-ttu-id="c0616-226">De tijdstempel (in UTC) van het logboek</span><span class="sxs-lookup"><span data-stu-id="c0616-226">The timestamp (in UTC) of the log</span></span> |
| <span data-ttu-id="c0616-227">resourceId</span><span class="sxs-lookup"><span data-stu-id="c0616-227">resourceId</span></span> |<span data-ttu-id="c0616-228">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c0616-228">String</span></span> |<span data-ttu-id="c0616-229">De ID van de resource die bewerking vond plaats op</span><span class="sxs-lookup"><span data-stu-id="c0616-229">The ID of the resource that operation took place on</span></span> |
| <span data-ttu-id="c0616-230">category</span><span class="sxs-lookup"><span data-stu-id="c0616-230">category</span></span> |<span data-ttu-id="c0616-231">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c0616-231">String</span></span> |<span data-ttu-id="c0616-232">De logboek-categorie.</span><span class="sxs-lookup"><span data-stu-id="c0616-232">The log category.</span></span> <span data-ttu-id="c0616-233">Bijvoorbeeld: **Audit**.</span><span class="sxs-lookup"><span data-stu-id="c0616-233">For example, **Audit**.</span></span> |
| <span data-ttu-id="c0616-234">operationName</span><span class="sxs-lookup"><span data-stu-id="c0616-234">operationName</span></span> |<span data-ttu-id="c0616-235">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c0616-235">String</span></span> |<span data-ttu-id="c0616-236">De naam van de bewerking die wordt vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="c0616-236">Name of the operation that is logged.</span></span> <span data-ttu-id="c0616-237">Bijvoorbeeld: getfilestatus.</span><span class="sxs-lookup"><span data-stu-id="c0616-237">For example, getfilestatus.</span></span> |
| <span data-ttu-id="c0616-238">resultType</span><span class="sxs-lookup"><span data-stu-id="c0616-238">resultType</span></span> |<span data-ttu-id="c0616-239">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c0616-239">String</span></span> |<span data-ttu-id="c0616-240">De status van de bewerking, bijvoorbeeld 200.</span><span class="sxs-lookup"><span data-stu-id="c0616-240">The status of the operation, For example, 200.</span></span> |
| <span data-ttu-id="c0616-241">correlationId</span><span class="sxs-lookup"><span data-stu-id="c0616-241">correlationId</span></span> |<span data-ttu-id="c0616-242">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c0616-242">String</span></span> |<span data-ttu-id="c0616-243">De id van het logboek dat kan worden gebruikt om een set van gerelateerde logboekvermeldingen groepen</span><span class="sxs-lookup"><span data-stu-id="c0616-243">The id of the log that can used to group together a set of related log entries</span></span> |
| <span data-ttu-id="c0616-244">identity</span><span class="sxs-lookup"><span data-stu-id="c0616-244">identity</span></span> |<span data-ttu-id="c0616-245">Object</span><span class="sxs-lookup"><span data-stu-id="c0616-245">Object</span></span> |<span data-ttu-id="c0616-246">De identiteit die door het logboek is gegenereerd</span><span class="sxs-lookup"><span data-stu-id="c0616-246">The identity that generated the log</span></span> |
| <span data-ttu-id="c0616-247">properties</span><span class="sxs-lookup"><span data-stu-id="c0616-247">properties</span></span> |<span data-ttu-id="c0616-248">JSON</span><span class="sxs-lookup"><span data-stu-id="c0616-248">JSON</span></span> |<span data-ttu-id="c0616-249">Zie hieronder voor meer informatie</span><span class="sxs-lookup"><span data-stu-id="c0616-249">See below for details</span></span> |

#### <a name="audit-log-properties-schema"></a><span data-ttu-id="c0616-250">Audit log eigenschappen schema</span><span class="sxs-lookup"><span data-stu-id="c0616-250">Audit log properties schema</span></span>
| <span data-ttu-id="c0616-251">Naam</span><span class="sxs-lookup"><span data-stu-id="c0616-251">Name</span></span> | <span data-ttu-id="c0616-252">Type</span><span class="sxs-lookup"><span data-stu-id="c0616-252">Type</span></span> | <span data-ttu-id="c0616-253">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c0616-253">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c0616-254">StreamName</span><span class="sxs-lookup"><span data-stu-id="c0616-254">StreamName</span></span> |<span data-ttu-id="c0616-255">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c0616-255">String</span></span> |<span data-ttu-id="c0616-256">Het pad van de bewerking is uitgevoerd op</span><span class="sxs-lookup"><span data-stu-id="c0616-256">The path the operation was performed on</span></span> |

## <a name="samples-to-process-the-log-data"></a><span data-ttu-id="c0616-257">Voorbeelden voor het verwerken van de logboekgegevens</span><span class="sxs-lookup"><span data-stu-id="c0616-257">Samples to process the log data</span></span>
<span data-ttu-id="c0616-258">Een voorbeeld van een biedt Azure Data Lake Store voor het verwerken en analyseren van de logboekgegevens.</span><span class="sxs-lookup"><span data-stu-id="c0616-258">Azure Data Lake Store provides a sample on how to process and analyze the log data.</span></span> <span data-ttu-id="c0616-259">U vindt het voorbeeld op [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span><span class="sxs-lookup"><span data-stu-id="c0616-259">You can find the sample at [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span></span> 

## <a name="see-also"></a><span data-ttu-id="c0616-260">Zie ook</span><span class="sxs-lookup"><span data-stu-id="c0616-260">See also</span></span>
* [<span data-ttu-id="c0616-261">Overzicht van Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="c0616-261">Overview of Azure Data Lake Store</span></span>](data-lake-store-overview.md)
* [<span data-ttu-id="c0616-262">Gegevens in Data Lake Store beveiligen</span><span class="sxs-lookup"><span data-stu-id="c0616-262">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)

