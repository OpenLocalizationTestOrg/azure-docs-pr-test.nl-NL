---
title: aaaDebug met bewerking en service-Logboeken in Stream Analytics | Microsoft Docs
description: Hoe toouse Stream Analytics-bewerkingslogboeken
keywords: Service-Logboeken
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: a2ed9676-f0bd-4398-87c8-a592779ac728
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: d3dd27706ccc879a724e1894b33d47021d972f31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="debug-stream-analytics-jobs-using-service-and-operation-logs"></a><span data-ttu-id="64f38-104">Fouten opsporen-service en bewerking logboeken met Stream Analytics-taken</span><span class="sxs-lookup"><span data-stu-id="64f38-104">Debug Stream Analytics jobs using service and operation logs</span></span>
<span data-ttu-id="64f38-105">Alle Azure-services levering operationele berichten toousers toorecord logboekdetails toomanagement bewerkingen gerelateerd.</span><span class="sxs-lookup"><span data-stu-id="64f38-105">All Azure services supply operational logging messages toousers toorecord details related toomanagement operations.</span></span> <span data-ttu-id="64f38-106">Deze informatie kan worden gebruikt voor foutopsporing zoals taakstatus, de voortgang van de taak en fout berichten tootrack Hallo voortgang van een taak gedurende een periode van start tooprocessing toooutput weergeven in Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="64f38-106">In Azure Stream Analytics, this information can be used for debugging purposes such as viewing job status, job progress, and failure messages tootrack hello progress of a job over time, from start tooprocessing toooutput.</span></span>

## <a name="find-operation-logs-in-hello-azure-management-portal"></a><span data-ttu-id="64f38-107">Bewerkingslogboeken op Hallo Azure Management portal zoeken</span><span class="sxs-lookup"><span data-stu-id="64f38-107">Find operation logs in hello Azure Management portal</span></span>
<span data-ttu-id="64f38-108">Bewerkingslogboeken toegankelijk zijn op twee manieren:</span><span class="sxs-lookup"><span data-stu-id="64f38-108">Operation Logs can be accessed in two ways:</span></span>  

* <span data-ttu-id="64f38-109">Dashboard van Hallo Stream Analytics-taak</span><span class="sxs-lookup"><span data-stu-id="64f38-109">Dashboard of hello Stream Analytics job</span></span>  
* <span data-ttu-id="64f38-110">Management-Services in de klassieke Azure-portal Hallo</span><span class="sxs-lookup"><span data-stu-id="64f38-110">Management Services in hello Azure Classic portal</span></span>  

## <a name="dashboard-of-hello-stream-analytics-job"></a><span data-ttu-id="64f38-111">Dashboard van Hallo Stream Analytics-taak</span><span class="sxs-lookup"><span data-stu-id="64f38-111">Dashboard of hello Stream Analytics job</span></span>
<span data-ttu-id="64f38-112">Een koppeling toohello overeenkomt logboeken van een Stream Analytics-taak wordt weergegeven op het tabblad van de taak van het Hallo-Dashboard. Als u op de koppeling klikt, wordt ingesteld Hallo filters zodanig dat het meest recente logboeken voor die specifieke taak bevat.</span><span class="sxs-lookup"><span data-stu-id="64f38-112">A link toohello corresponding logs of a Stream Analytics job is displayed on hello job’s Dashboard tab. If you click on that link, it will set hello filters in a way that it shows latest logs for that specific job.</span></span>

  ![Selecteer beheerservices Logboeken](./media/stream-analytics-operation-logs/01-stream-analytics-operation-logs.png)  

## <a name="management-services"></a><span data-ttu-id="64f38-114">Management-Services</span><span class="sxs-lookup"><span data-stu-id="64f38-114">Management Services</span></span>
<span data-ttu-id="64f38-115">toomanually Navigeer toohello Bewerkingslogboeken voor Stream Analytics en andere services in de klassieke Azure-portal Hallo:</span><span class="sxs-lookup"><span data-stu-id="64f38-115">toomanually navigate toohello Operation Logs for Stream Analytics and other services in hello Azure Classic portal:</span></span>

1. <span data-ttu-id="64f38-116">Klik op **beheerservices** in Hallo [klassieke Azure-portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="64f38-116">Click on **Management Services** in hello [Azure Classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="64f38-117">Selecteer **Stream Analytics** voor **Type** en Hallo-naam van de taak Hallo voor **servicenaam**.</span><span class="sxs-lookup"><span data-stu-id="64f38-117">Select **Stream Analytics** for **Type** and hello name of hello job for **Service Name**.</span></span>  
   
   ![Selecteer de Stream Analytics](./media/stream-analytics-operation-logs/02-stream-analytics-operation-logs.png)  

## <a name="find-audit-logs-in-hello-azure-portal"></a><span data-ttu-id="64f38-119">Controlelogboeken niet vinden in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="64f38-119">Find audit logs in hello Azure portal</span></span>
<span data-ttu-id="64f38-120">toofind operationele logboeken voor de Stream Analytics-taak in hello Azure-portal, klikt u op **Bladeren** en selecteer vervolgens **controlelogboeken**.</span><span class="sxs-lookup"><span data-stu-id="64f38-120">toofind operational logs for your Stream Analytics job in hello Azure portal, Click **Browse** and then select **Audit logs**.</span></span>

  ![Azure-portal Stream Analytics selecteren](./media/stream-analytics-operation-logs/06-stream-analytics-operation-logs.png)  

<span data-ttu-id="64f38-122">Hiermee opent u een blade met gebeurtenissen van Hallo afgelopen 7 dagen voor alle resources in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="64f38-122">This will open a blade showing events from hello last 7 days for all resources in your subscription.</span></span>  <span data-ttu-id="64f38-123">U kunt toosee gebeurtenissen van een type opgeven of het tijdsbestek filteren door te klikken op Hallo **Filter** opdracht.</span><span class="sxs-lookup"><span data-stu-id="64f38-123">You can filter toosee events of a specify type or time frame by clicking hello **Filter** command.</span></span>

  ![Azure-portal Stream Analytics selecteren](./media/stream-analytics-operation-logs/07-stream-analytics-operation-logs.png)  

## <a name="get-log-details"></a><span data-ttu-id="64f38-125">Logboekdetails van het ophalen</span><span class="sxs-lookup"><span data-stu-id="64f38-125">Get log details</span></span>
<span data-ttu-id="64f38-126">U kunt filteren op Status tooview Hallo logboeken en tijdsbereik voor uw project.</span><span class="sxs-lookup"><span data-stu-id="64f38-126">You can filter by Time Range and Status tooview hello logs for your job.</span></span>

<span data-ttu-id="64f38-127">Hello Azure-beheerportal, klik op Hallo **Details** knop onderaan Hallo Hallo venster tooview meer informatie over een geselecteerde gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="64f38-127">In hello Azure Management portal, click on hello **Details** button at hello bottom of hello window tooview more details about a selected event.</span></span> 

  ![Details van selecteren](./media/stream-analytics-operation-logs/03-stream-analytics-operation-logs.png)  

<span data-ttu-id="64f38-129">Azure-portal, klik op een vermelding logboek toosee Hallo in Hallo gedetailleerde gebeurtenissen in het.</span><span class="sxs-lookup"><span data-stu-id="64f38-129">In hello Azure portal, click on a log entry toosee hello detailed events inside it.</span></span>

  ![Azure-portal Details selecteren](./media/stream-analytics-operation-logs/08-stream-analytics-operation-logs.png)  

<span data-ttu-id="64f38-131">Daar kunt u Hallo openen **Detail** blade door te klikken op Hallo-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="64f38-131">From there, you can open hello **Detail** blade by clicking on hello event.</span></span>

  ![Azure-portal Details selecteren](./media/stream-analytics-operation-logs/09-stream-analytics-operation-logs.png)  

## <a name="debug-a-failed-job"></a><span data-ttu-id="64f38-133">Fouten opsporen in een mislukte taak</span><span class="sxs-lookup"><span data-stu-id="64f38-133">Debug a failed job</span></span>
<span data-ttu-id="64f38-134">Klik op het zoekpictogram Hallo in hello Azure-beheerportal, en typ 'mislukt'.</span><span class="sxs-lookup"><span data-stu-id="64f38-134">In hello Azure Management portal, click on hello Search icon and type ‘failed’.</span></span> <span data-ttu-id="64f38-135">Hiermee geeft u een resultaat van alle logboeken met fouten.</span><span class="sxs-lookup"><span data-stu-id="64f38-135">This gives a result of all logs with failures.</span></span> 

  ![Foutopsporing van een taak die is mislukt](./media/stream-analytics-operation-logs/04-stream-analytics-operation-logs.png)  

<span data-ttu-id="64f38-137">In hello Azure-portal, kunt u filteren op niveau van het bericht tooview **Kritiek** gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="64f38-137">In hello Azure portal, you can filter by level of message tooview **Critical** events.</span></span>

  ![Azure portal foutopsporing](./media/stream-analytics-operation-logs/10-stream-analytics-operation-logs.png)  

<span data-ttu-id="64f38-139">Selecteer een van de Hallo fouten en klik op Hallo **Details** voor meer informatie over Hallo-fout.</span><span class="sxs-lookup"><span data-stu-id="64f38-139">You can select any one of hello failures, and click on hello **Details** for more information on hello error.</span></span>  <span data-ttu-id="64f38-140">Bepaalde foutberichten bevatten ook informatie over hoe toomitigate Hallo probleem.</span><span class="sxs-lookup"><span data-stu-id="64f38-140">Some error messages also provide information about how toomitigate hello issue.</span></span> 

  ![Details van bewerking](./media/stream-analytics-operation-logs/05-stream-analytics-operation-logs.png)  

<span data-ttu-id="64f38-142">Geval u toocontact moet [ondersteuning](https://azure.microsoft.com/support/options/) of geef informatie toohello team via Hallo [MSDN-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics), houd er rekening mee Hallo operationele Details, speciaal Hallo **correlatie-ID**.</span><span class="sxs-lookup"><span data-stu-id="64f38-142">In case you need toocontact [Support](https://azure.microsoft.com/support/options/) or provide information toohello team via hello [MSDN forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics), please note hello Operation Details, specifically hello **Correlation ID**.</span></span> 

## <a name="get-help"></a><span data-ttu-id="64f38-143">Help opvragen</span><span class="sxs-lookup"><span data-stu-id="64f38-143">Get help</span></span>
<span data-ttu-id="64f38-144">Voor verdere hulp kunt u mogelijk terecht op het [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="64f38-144">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="64f38-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="64f38-145">Next steps</span></span>
* [<span data-ttu-id="64f38-146">Inleiding tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="64f38-146">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="64f38-147">Aan de slag met Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="64f38-147">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="64f38-148">Azure Stream Analytics-taken schalen</span><span class="sxs-lookup"><span data-stu-id="64f38-148">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="64f38-149">Naslaggids voor Azure Stream Analytics Query</span><span class="sxs-lookup"><span data-stu-id="64f38-149">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="64f38-150">REST API-naslaggids voor Azure Stream Analytics Management</span><span class="sxs-lookup"><span data-stu-id="64f38-150">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

