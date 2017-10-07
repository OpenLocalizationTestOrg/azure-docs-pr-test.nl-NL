---
title: aaaHow toostart streaming-taken in de Stream Analytics | Microsoft Docs
description: Hoe een streaming-taak uitgevoerd in Azure Stream Analytics | leren padsegment.
keywords: Streaming-taken
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9d46950f-2b69-49ce-a567-df558c5dd820
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 67aa14860c38cbd0535d0ec4f23729445d0185c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-streaming-job-in-azure-stream-analytics"></a><span data-ttu-id="3769c-104">Hoe toorun een streaming-taak in Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3769c-104">How toorun a streaming job in Azure Stream Analytics</span></span>
<span data-ttu-id="3769c-105">Wanneer een taak invoer, query's en uitvoer, zijn alle opgegeven dat kunt u Hallo Stream Analytics-taak starten.</span><span class="sxs-lookup"><span data-stu-id="3769c-105">When a job input, query and output have all been specified you can start hello Stream Analytics job.</span></span>

<span data-ttu-id="3769c-106">toostart uw taak:</span><span class="sxs-lookup"><span data-stu-id="3769c-106">toostart your job:</span></span>

1. <span data-ttu-id="3769c-107">Klik in de klassieke Azure-portal Hallo van Hallo taak dashboard op **Start** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="3769c-107">In hello Azure Classic portal, from hello job dashboard, click **Start** at hello bottom of hello page.</span></span>
   
   ![Taak knop starten](./media/stream-analytics-run-a-job/1-stream-analytics-run-a-job.png)  
   
   <span data-ttu-id="3769c-109">Klik in hello Azure-portal, op **Start** Hallo boven aan de pagina van de taak.</span><span class="sxs-lookup"><span data-stu-id="3769c-109">In hello Azure portal, click **Start** at hello top of your job page.</span></span>
   
   ![Azure portal starttaak knop](./media/stream-analytics-run-a-job/4-stream-analytics-run-a-job.png)  
2. <span data-ttu-id="3769c-111">Geef een **Start uitvoer** waarde toodetermine wanneer deze taak zal starten uitvoer te produceren.</span><span class="sxs-lookup"><span data-stu-id="3769c-111">Specify a **Start Output** value toodetermine when this job will start producing output.</span></span> <span data-ttu-id="3769c-112">Hallo standaardinstelling voor taken die eerder niet is gestart is **begintijd taak**, wat betekent dat deze taak Hallo begint onmiddellijk verwerken van gegevens.</span><span class="sxs-lookup"><span data-stu-id="3769c-112">hello default setting for jobs that have not previously been started is **Job Start Time**, which means that hello job will immediately start processing data.</span></span> <span data-ttu-id="3769c-113">U kunt ook opgeven een **aangepaste** tijd in Hallo in het verleden (voor het gebruiken van historische gegevens) of Hallo toekomstige (toodelay verwerken tot een toekomstig tijdstip).</span><span class="sxs-lookup"><span data-stu-id="3769c-113">You can also specify a **Custom** time in hello past (for consuming historical data) or hello future (toodelay processing until a future time).</span></span> <span data-ttu-id="3769c-114">Voor gevallen wanneer een taak is eerder gestart en gestopt, optie Hallo **laatste tijd geëindigd** is beschikbaar in de volgorde tooresume Hallo taak in de tijd van laatste uitvoer Hallo en voorkomen dat gegevens verloren gaan.</span><span class="sxs-lookup"><span data-stu-id="3769c-114">For cases when a job has been previously started and stopped, hello option **Last Stopped Time** is available in order tooresume hello job from hello last output time and avoid data loss.</span></span>  
   
   ![Streaming-taak tijd starten](./media/stream-analytics-run-a-job/2-stream-analytics-run-a-job.png)  
   
   ![Azure portal Start streaming-taak tijd](./media/stream-analytics-run-a-job/5-stream-analytics-run-a-job.png)  
3. <span data-ttu-id="3769c-117">Bevestig uw selectie.</span><span class="sxs-lookup"><span data-stu-id="3769c-117">Confirm your selection.</span></span> <span data-ttu-id="3769c-118">Hallo taakstatus verandert te*starten* en zal spoedig te verplaatsen*met* eenmaal Hallo-taak is gestart.</span><span class="sxs-lookup"><span data-stu-id="3769c-118">hello job status will change too*Starting* and will shortly move too*Running* once hello job has started.</span></span> <span data-ttu-id="3769c-119">U kunt Hallo voortgang Hallo **Start** Hallo-bewerking **Notification Hub**:</span><span class="sxs-lookup"><span data-stu-id="3769c-119">You can monitor hello progress of hello **Start** operation in hello **Notification Hub**:</span></span>
   
   ![Streaming-taak uitgevoerd](./media/stream-analytics-run-a-job/3-stream-analytics-run-a-job.png)  
   
   ![Azure-portal streaming-taak uitgevoerd](./media/stream-analytics-run-a-job/6-stream-analytics-run-a-job.png)  

## <a name="get-help"></a><span data-ttu-id="3769c-122">Help opvragen</span><span class="sxs-lookup"><span data-stu-id="3769c-122">Get help</span></span>
<span data-ttu-id="3769c-123">Voor verdere hulp kunt u mogelijk terecht op het [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="3769c-123">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="3769c-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3769c-124">Next steps</span></span>
* [<span data-ttu-id="3769c-125">Inleiding tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3769c-125">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="3769c-126">Aan de slag met Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3769c-126">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="3769c-127">Azure Stream Analytics-taken schalen</span><span class="sxs-lookup"><span data-stu-id="3769c-127">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="3769c-128">Naslaggids voor Azure Stream Analytics Query</span><span class="sxs-lookup"><span data-stu-id="3769c-128">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="3769c-129">REST API-naslaggids voor Azure Stream Analytics Management</span><span class="sxs-lookup"><span data-stu-id="3769c-129">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

