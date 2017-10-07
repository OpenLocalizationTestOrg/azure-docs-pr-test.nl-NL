---
title: een data aaaAdd invoer tooyour Stream Analytics-taken | Microsoft Docs
description: Meer informatie over hoe toohook van een data source tooyour Stream Analytics als streaming gegevensinvoer uit Event Hubs of verwijzing gegevens uit Blog van storage taak.
keywords: gegevens invoeren, streamen van gegevens
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: 
ms.assetid: 9e59bd24-2a80-4ecb-b6b2-309a07c70bcd
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 674000268fcdf9bc000af3e2f166cb66f1366922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-streaming-data-input-or-reference-data-tooa-stream-analytics-job"></a><span data-ttu-id="2368a-104">Een streaming invoer- of gegevens tooa Stream Analytics-taak toevoegen</span><span class="sxs-lookup"><span data-stu-id="2368a-104">Add a streaming data input or reference data tooa Stream Analytics job</span></span>
<span data-ttu-id="2368a-105">Meer informatie over hoe toohook van een data source tooyour Stream Analytics taak als streaming gegevensinvoer uit Event Hubs of verwijzing gegevens uit Blob storage.</span><span class="sxs-lookup"><span data-stu-id="2368a-105">Learn how toohook up a data source tooyour Stream Analytics job as streaming data input from Event Hubs or reference data from Blob storage.</span></span>

<span data-ttu-id="2368a-106">Azure Stream Analytics-taken kunnen worden verbonden tooone gegevensinvoer of meer, die elk een verbinding tooan bestaande gegevensbron definiëren.</span><span class="sxs-lookup"><span data-stu-id="2368a-106">Azure Stream Analytics jobs can be connected tooone data input or more, each of which define a connection tooan existing data source.</span></span> <span data-ttu-id="2368a-107">Wanneer gegevens worden verzonden toothat gegevensbron, wordt gebruikt door de Stream Analytics-taak Hallo en verwerkt in realtime als het streamen van gegevens.</span><span class="sxs-lookup"><span data-stu-id="2368a-107">As data is sent toothat data source, it is consumed by hello Stream Analytics job and processed in real time as streaming data.</span></span> <span data-ttu-id="2368a-108">Stream Analytics heeft eerste-klas integratie met [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) en [Azure Blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md) zowel binnen als buiten van de taak van het Hallo-abonnement.</span><span class="sxs-lookup"><span data-stu-id="2368a-108">Stream Analytics has first class integration with [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) and [Azure Blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md) both within and outside of hello job's subscription.</span></span>

<span data-ttu-id="2368a-109">In dit artikel is een stap in Hallo [leertraject voor Stream Analytics](/documentation/learning-paths/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="2368a-109">This article is a step in hello [Stream Analytics learning path](/documentation/learning-paths/stream-analytics/).</span></span>

## <a name="data-input-streaming-data-and-reference-data"></a><span data-ttu-id="2368a-110">Invoer: Streaming en verwijzingsgegevens</span><span class="sxs-lookup"><span data-stu-id="2368a-110">Data input: Streaming data and reference data</span></span>
<span data-ttu-id="2368a-111">Er zijn twee verschillende soorten invoer in Stream Analytics: gegevensstromen en referentiegegevens.</span><span class="sxs-lookup"><span data-stu-id="2368a-111">There are two distinct types of inputs in Stream Analytics: data streams and reference data.</span></span>

* <span data-ttu-id="2368a-112">**Gegevensstromen**: Stream Analytics-taken moeten ten minste één gegevensstroom invoer toobe verbruikt en getransformeerd door Hallo taak bevatten.</span><span class="sxs-lookup"><span data-stu-id="2368a-112">**Data Streams**: Stream Analytics jobs must include at least one data stream input toobe consumed and transformed by hello job.</span></span> <span data-ttu-id="2368a-113">Azure Blob storage en Azure Event Hubs worden ondersteund als invoer gegevensbronnen stroom.</span><span class="sxs-lookup"><span data-stu-id="2368a-113">Azure Blob storage and Azure Event Hubs are supported as data stream input sources.</span></span> <span data-ttu-id="2368a-114">Azure Event Hubs zijn gebruikte toocollect gebeurtenisstromen van verbonden apparaten, services en toepassingen.</span><span class="sxs-lookup"><span data-stu-id="2368a-114">Azure Event Hubs are used toocollect event streams from connected devices, services and applications.</span></span> <span data-ttu-id="2368a-115">Azure Blob-opslag kan worden gebruikt als een invoerbron voor het opnemen van grote hoeveelheden gegevens als een stroom.</span><span class="sxs-lookup"><span data-stu-id="2368a-115">Azure Blob storage can be used as an input source for ingesting bulk data as a stream.</span></span>  
* <span data-ttu-id="2368a-116">**Referentiegegevens**: Stream Analytics ondersteunt een tweede gegevenstype reserve invoerverwijzing genoemd.</span><span class="sxs-lookup"><span data-stu-id="2368a-116">**Reference data**: Stream Analytics supports a second type of auxiliary input called reference data.</span></span>  <span data-ttu-id="2368a-117">Als de tegengestelde toodata in beweging zijn deze gegevens statisch of vertraging wijzigen.</span><span class="sxs-lookup"><span data-stu-id="2368a-117">As opposed toodata in motion, this data is static or slowing changing.</span></span>  <span data-ttu-id="2368a-118">Dit wordt meestal gebruikt voor het uitvoeren van de op te zoeken en correlatie met gegevensstromen toocreate een uitgebreidere set van gegevens.</span><span class="sxs-lookup"><span data-stu-id="2368a-118">It is typically used for performing look-ups and correlations with data streams toocreate a richer data set.</span></span>  <span data-ttu-id="2368a-119">Azure Blob-opslag bevindt zich momenteel in de invoerbron Hallo alleen ondersteund voor referentiegegevens.</span><span class="sxs-lookup"><span data-stu-id="2368a-119">Azure Blob storage is currently hello only supported input source for reference data.</span></span>  

<span data-ttu-id="2368a-120">tooadd een invoer tooyour Stream Analytics-taak:</span><span class="sxs-lookup"><span data-stu-id="2368a-120">tooadd an input tooyour Stream Analytics job:</span></span>

1. <span data-ttu-id="2368a-121">Klik in hello Azure-portal op **invoer** en klik vervolgens op **invoer toevoegen** in uw Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="2368a-121">In hello Azure portal click **Inputs** and then click **Add an Input** in your Stream Analytics job.</span></span>
   
    ![Klassieke Azure-portal - invoer toevoegen.](./media/stream-analytics-add-inputs/1-stream-analytics-add-inputs.png)  
   
    <span data-ttu-id="2368a-123">Klik in hello Azure-portal op Hallo **invoer** -tegel in de Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="2368a-123">In hello Azure portal click hello **Inputs** tile in your Stream Analytics job.</span></span>  
   
    ![Azure-portal - invoer toevoegen.](./media/stream-analytics-add-inputs/7-stream-analytics-add-inputs.png)  
2. <span data-ttu-id="2368a-125">Geef Hallo Hallo invoer: beide **gegevensstroom** of **referentiegegevens**.</span><span class="sxs-lookup"><span data-stu-id="2368a-125">Specify hello type of hello input: either **Data stream** or **Reference data**.</span></span>
   
    ![Invoer, gestreamd of verwijst naar de juiste gegevens Hallo toevoegen](./media/stream-analytics-add-inputs/2-stream-analytics-add-inputs.png)  
   
    ![Invoer, gestreamd of verwijst naar de juiste gegevens Hallo toevoegen](./media/stream-analytics-add-inputs/8-stream-analytics-add-inputs.png)  
3. <span data-ttu-id="2368a-128">Als het maken van een gegevensstroom invoer opgeven Hallo brontype voor Hallo-invoer.</span><span class="sxs-lookup"><span data-stu-id="2368a-128">If creating a Data Stream input, specify hello source type for hello input.</span></span>  <span data-ttu-id="2368a-129">Deze stap worden overgeslagen tijdens het maken van referentiegegevens als alleen-Blob-opslag op dit moment wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="2368a-129">This step can be skipped during Reference Data creation as only Blob storage is supported at this time.</span></span>
   
    ![Gegevens gegevensstroominvoer toevoegen](./media/stream-analytics-add-inputs/3-stream-analytics-add-inputs.png)  
   
    ![Gegevens gegevensstroominvoer toevoegen](./media/stream-analytics-add-inputs/9-stream-analytics-add-inputs.png)  
4. <span data-ttu-id="2368a-132">Geef een beschrijvende naam voor deze invoer in Hallo Invoeralias vak.</span><span class="sxs-lookup"><span data-stu-id="2368a-132">Provide a friendly name for this input in hello Input Alias box.</span></span>  <span data-ttu-id="2368a-133">Deze naam wordt gebruikt in uw job query later op toorefer toohello invoer.</span><span class="sxs-lookup"><span data-stu-id="2368a-133">This name will be used in your job's query later on toorefer toohello input.</span></span>
   
    <span data-ttu-id="2368a-134">Vul de overige Hallo van Hallo vereiste verbinding eigenschappen tooconnect tooyour-gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="2368a-134">Fill in hello rest of hello required connection properties tooconnect tooyour data source.</span></span> <span data-ttu-id="2368a-135">Deze velden verschillen per type van het type invoer- en bron en worden gedefinieerd in detail [hier](stream-analytics-create-a-job.md).</span><span class="sxs-lookup"><span data-stu-id="2368a-135">These fields vary by type of input and source type and are defined in detail [here](stream-analytics-create-a-job.md).</span></span>  
   
    ![Event hub gegevensinvoer toevoegen](./media/stream-analytics-add-inputs/4-stream-analytics-add-inputs.png)  
5. <span data-ttu-id="2368a-137">Hallo serialisatie instellingen opgeven voor de invoergegevens Hallo:</span><span class="sxs-lookup"><span data-stu-id="2368a-137">Specify hello serialization settings for hello input data:</span></span>
   
   * <span data-ttu-id="2368a-138">controleren of uw query's werken Hallo zoals verwacht toomake Hallo opgeven **gebeurtenis serialisatie-indeling** van binnenkomende gegevens.</span><span class="sxs-lookup"><span data-stu-id="2368a-138">toomake sure your queries work hello way you expect, specify hello **Event Serialization Format** of incoming data.</span></span>  <span data-ttu-id="2368a-139">Ondersteunde serialisatie-indelingen zijn JSON, CSV en Avro.</span><span class="sxs-lookup"><span data-stu-id="2368a-139">Supported serialization formats are JSON, CSV, and Avro.</span></span>
   * <span data-ttu-id="2368a-140">Controleer of Hallo **codering** voor Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="2368a-140">Verify hello **Encoding** for hello data.</span></span>  <span data-ttu-id="2368a-141">UTF-8 wordt de coderingsindeling Hallo alleen ondersteund op dit moment.</span><span class="sxs-lookup"><span data-stu-id="2368a-141">UTF-8 is hello only supported encoding format at this time.</span></span>
     
     ![Instellingen voor serialisatie van gegevens voor gegevensinvoer Hallo](./media/stream-analytics-add-inputs/5-stream-analytics-add-inputs.png)  
     
     ![Instellingen voor serialisatie van gegevens voor gegevensinvoer Hallo](./media/stream-analytics-add-inputs/10-stream-analytics-add-inputs.png)  
6. <span data-ttu-id="2368a-144">Na het voltooien van de invoer maken Hallo Stream Analytics controleert of dat deze de invoerbron toohello verbinding kan maken.</span><span class="sxs-lookup"><span data-stu-id="2368a-144">After completing hello input creation, Stream Analytics will verify that it can connect toohello input source.</span></span>  <span data-ttu-id="2368a-145">U kunt Hallo status Hallo testverbinding bewerking bekijken in Hallo Notification hub.</span><span class="sxs-lookup"><span data-stu-id="2368a-145">You can view hello status of hello Test Connection operation in hello Notification hub.</span></span>
   
    ![De testverbinding Hallo gegevensstromen invoer](./media/stream-analytics-add-inputs/6-stream-analytics-add-inputs.png)  
   
    ![De testverbinding Hallo gegevensstromen invoer](./media/stream-analytics-add-inputs/11-stream-analytics-add-inputs.png)  

## <a name="get-help-with-streaming-data-inputs"></a><span data-ttu-id="2368a-148">Hulp bij het streaming-gegevens invoeren</span><span class="sxs-lookup"><span data-stu-id="2368a-148">Get help with streaming data inputs</span></span>
<span data-ttu-id="2368a-149">Voor verdere hulp kunt u mogelijk terecht op het [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="2368a-149">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="2368a-150">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2368a-150">Next steps</span></span>
* [<span data-ttu-id="2368a-151">Inleiding tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2368a-151">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="2368a-152">Aan de slag met Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2368a-152">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="2368a-153">Azure Stream Analytics-taken schalen</span><span class="sxs-lookup"><span data-stu-id="2368a-153">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="2368a-154">Naslaggids voor Azure Stream Analytics Query</span><span class="sxs-lookup"><span data-stu-id="2368a-154">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="2368a-155">REST API-naslaggids voor Azure Stream Analytics Management</span><span class="sxs-lookup"><span data-stu-id="2368a-155">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

