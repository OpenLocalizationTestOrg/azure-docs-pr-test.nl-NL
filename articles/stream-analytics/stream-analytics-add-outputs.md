---
title: aaaHow tooconfigure gegevens levert voor Stream Analytics-taken | Microsoft Docs
description: Uitvoer voor Stream Analytics-taken configureren | leren padsegment.
keywords: gegevens uitvoer verplaatsing van gegevens
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 3bbea3da-bfce-4af1-a15e-d4b23874034f
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/26/2017
ms.author: samacha
ms.openlocfilehash: c5d89e9e9f9211d3e778580c071dd53d56aed9fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-data-outputs-for-stream-analytics-jobs"></a><span data-ttu-id="a3d3b-104">Hoe tooconfigure gegevens levert voor Stream Analytics-taken</span><span class="sxs-lookup"><span data-stu-id="a3d3b-104">How tooconfigure data outputs for Stream Analytics jobs</span></span>

<span data-ttu-id="a3d3b-105">Azure Stream Analytics-taken zijn verbonden tooone of meer gegevens uitvoer, die een verbinding tooan bestaande gegevens sink definiëren.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-105">Azure Stream Analytics jobs can be connected tooone or more data outputs, which define a connection tooan existing data sink.</span></span> <span data-ttu-id="a3d3b-106">Als uw Stream Analytics-taak verwerkt en binnenkomende gegevens transformeert, is een stream met gegevens uitvoergebeurtenissen tooyour taakuitvoer geschreven.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-106">As your Stream Analytics job processes and transforms incoming data, a stream of data output events is written tooyour job's output.</span></span>

<span data-ttu-id="a3d3b-107">Stream Analytics gegevens uitvoer kunnen worden gebruikt toosource realtime-dashboards of waarschuwingen, trigger data movement werkstromen of gewoon gegevens archiveren voor batch-verwerking later op.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-107">Stream Analytics data outputs can be used toosource real-time dashboards or alerts, trigger data movement workflows, or simply archive data for batch processing later on.</span></span> <span data-ttu-id="a3d3b-108">Stream Analytics heeft eerste-klas integratie met verschillende Azure-services, die in details hier worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-108">Stream Analytics has first class integration with several Azure services, which are documented in detail here.</span></span>

<span data-ttu-id="a3d3b-109">de Stream Analytics-taak van een uitvoer-tooyour tooadd:</span><span class="sxs-lookup"><span data-stu-id="a3d3b-109">tooadd an output tooyour Stream Analytics job:</span></span>

1. <span data-ttu-id="a3d3b-110">In Hallo [Azure-portal](https://portal.azure.com), opent u de taak en klikt u op **uitvoer** en klik vervolgens op **toevoegen** Hallo uitvoer blade die wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-110">In hello [Azure portal](https://portal.azure.com), open your job and click **Outputs** and then click **Add** in hello Outputs blade that appears.</span></span>
   
    ![Uitvoer toevoegen](./media/stream-analytics-add-outputs/1-stream-analytics-add-outputs.png)  
   
2. <span data-ttu-id="a3d3b-112">Geef een beschrijvende naam voor deze uitvoer in Hallo **Uitvoeraliassen** vak.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-112">Provide a friendly name for this output in hello **Output Alias** box.</span></span> <span data-ttu-id="a3d3b-113">Deze naam kan worden gebruikt in uw job query later op toorefer toohello uitvoer.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-113">This name can be used in your job's query later on toorefer toohello output.</span></span>  
   
    <span data-ttu-id="a3d3b-114">Vul de overige Hallo van Hallo vereist verbinding eigenschappen tooconnect tooyour uitvoer.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-114">Fill in hello rest of hello required connection properties tooconnect tooyour output.</span></span>  <span data-ttu-id="a3d3b-115">Deze velden is afhankelijk van het uitvoertype en hier worden gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-115">These fields vary by output type and are defined in detail here.</span></span>  
   
    ![Gegevenstype verplaatsing kiezen](./media/stream-analytics-add-outputs/2-stream-analytics-add-outputs.png)  
   
3. <span data-ttu-id="a3d3b-117">Afhankelijk van het type uitvoer Hallo moet u mogelijk toospecify hoe Hallo gegevens is geserialiseerd of geformatteerd.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-117">Depending on hello output type, you may need toospecify how hello data is serialized or formatted.</span></span> <span data-ttu-id="a3d3b-118">Hallo serialisatie specifieke instellingen voor elk uitvoertype worden hier beschreven.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-118">hello specific serialization settings for each output type are documented here.</span></span>
   
    <span data-ttu-id="a3d3b-119">Vul de overige Hallo van Hallo vereiste verbinding eigenschappen tooconnect tooyour-gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-119">Fill in hello rest of hello required connection properties tooconnect tooyour data source.</span></span> <span data-ttu-id="a3d3b-120">Deze velden verschillen per type van het type invoer- en bron en worden gedefinieerd in detail in Hallo [taak maken artikel](stream-analytics-create-a-job.md).</span><span class="sxs-lookup"><span data-stu-id="a3d3b-120">These fields vary by type of input and source type and are defined in detail in hello [Create Job article](stream-analytics-create-a-job.md).</span></span>  

> [!Note]
>
> <span data-ttu-id="a3d3b-121">Elke uitvoer element toegevoegde toohello-taak moet bestaan voordat Hallo-taak is gestart en gebeurtenissen start stromende.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-121">Any output element added toohello job, must exist before hello job is started and events start flowing.</span></span> <span data-ttu-id="a3d3b-122">Bijvoorbeeld, als u een Blob-opslag als uitvoer gebruikt, maakt Hallo-taak niet een opslagaccount automatisch.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-122">For example, if you use Blob storage as an output, hello job will not create a storage account automatically.</span></span> <span data-ttu-id="a3d3b-123">Het moet toobe gemaakt door gebruiker Hallo voordat Hallo ASA-taak is gestart.</span><span class="sxs-lookup"><span data-stu-id="a3d3b-123">It needs toobe created by hello user before hello ASA job is started.</span></span>
> 
 

## <a name="get-help"></a><span data-ttu-id="a3d3b-124">Help opvragen</span><span class="sxs-lookup"><span data-stu-id="a3d3b-124">Get help</span></span>
<span data-ttu-id="a3d3b-125">Voor verdere hulp kunt u mogelijk terecht op het [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="a3d3b-125">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3d3b-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a3d3b-126">Next steps</span></span>
* [<span data-ttu-id="a3d3b-127">Inleiding tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="a3d3b-127">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="a3d3b-128">Aan de slag met Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="a3d3b-128">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="a3d3b-129">Azure Stream Analytics-taken schalen</span><span class="sxs-lookup"><span data-stu-id="a3d3b-129">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="a3d3b-130">Naslaggids voor Azure Stream Analytics Query</span><span class="sxs-lookup"><span data-stu-id="a3d3b-130">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="a3d3b-131">REST API-naslaggids voor Azure Stream Analytics Management</span><span class="sxs-lookup"><span data-stu-id="a3d3b-131">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

