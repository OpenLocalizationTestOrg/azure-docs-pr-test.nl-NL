---
title: Een data invoer toevoegen aan Stream Analytics-taken | Microsoft Docs
description: Informatie over het aansluiten van een gegevensbron om uw Stream Analytics-taak als streaming gegevensinvoer uit Event Hubs of verwijzing gegevens uit Blog van storage.
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
ms.openlocfilehash: 8bdbcf78f2892cbd1e1cc09cef220dff08dd9490
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="add-a-streaming-data-input-or-reference-data-to-a-stream-analytics-job"></a><span data-ttu-id="19015-104">Een streaming gegevens invoer- of gegevens toevoegen aan Stream Analytics-taak</span><span class="sxs-lookup"><span data-stu-id="19015-104">Add a streaming data input or reference data to a Stream Analytics job</span></span>
<span data-ttu-id="19015-105">Informatie over het aansluiten van een gegevensbron om uw Stream Analytics-taak als streaming gegevensinvoer uit Event Hubs of verwijzing gegevens uit Blob storage.</span><span class="sxs-lookup"><span data-stu-id="19015-105">Learn how to hook up a data source to your Stream Analytics job as streaming data input from Event Hubs or reference data from Blob storage.</span></span>

<span data-ttu-id="19015-106">Azure Stream Analytics-taken kunnen worden verbonden met een invoer of meer, die elk een verbinding met een bestaande gegevensbron definieert.</span><span class="sxs-lookup"><span data-stu-id="19015-106">Azure Stream Analytics jobs can be connected to one data input or more, each of which define a connection to an existing data source.</span></span> <span data-ttu-id="19015-107">Wanneer gegevens worden verzonden aan die gegevensbron, wordt gebruikt door de Stream Analytics-taak en verwerkt in realtime als het streamen van gegevens.</span><span class="sxs-lookup"><span data-stu-id="19015-107">As data is sent to that data source, it is consumed by the Stream Analytics job and processed in real time as streaming data.</span></span> <span data-ttu-id="19015-108">Stream Analytics heeft eerste-klas integratie met [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) en [Azure Blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md) zowel binnen als buiten het abonnement van de taak.</span><span class="sxs-lookup"><span data-stu-id="19015-108">Stream Analytics has first class integration with [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) and [Azure Blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md) both within and outside of the job's subscription.</span></span>

<span data-ttu-id="19015-109">In dit artikel is een stap in de [leertraject voor Stream Analytics](/documentation/learning-paths/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="19015-109">This article is a step in the [Stream Analytics learning path](/documentation/learning-paths/stream-analytics/).</span></span>

## <a name="data-input-streaming-data-and-reference-data"></a><span data-ttu-id="19015-110">Invoer: Streaming en verwijzingsgegevens</span><span class="sxs-lookup"><span data-stu-id="19015-110">Data input: Streaming data and reference data</span></span>
<span data-ttu-id="19015-111">Er zijn twee verschillende soorten invoer in Stream Analytics: gegevensstromen en referentiegegevens.</span><span class="sxs-lookup"><span data-stu-id="19015-111">There are two distinct types of inputs in Stream Analytics: data streams and reference data.</span></span>

* <span data-ttu-id="19015-112">**Gegevensstromen**: Stream Analytics-taken moeten ten minste één gegevensstroominvoer worden verbruikt en wordt omgezet door de taak bevatten.</span><span class="sxs-lookup"><span data-stu-id="19015-112">**Data Streams**: Stream Analytics jobs must include at least one data stream input to be consumed and transformed by the job.</span></span> <span data-ttu-id="19015-113">Azure Blob storage en Azure Event Hubs worden ondersteund als invoer gegevensbronnen stroom.</span><span class="sxs-lookup"><span data-stu-id="19015-113">Azure Blob storage and Azure Event Hubs are supported as data stream input sources.</span></span> <span data-ttu-id="19015-114">Azure Event Hubs worden gebruikt voor het verzamelen van verbonden apparaten, services en toepassingen.</span><span class="sxs-lookup"><span data-stu-id="19015-114">Azure Event Hubs are used to collect event streams from connected devices, services and applications.</span></span> <span data-ttu-id="19015-115">Azure Blob-opslag kan worden gebruikt als een invoerbron voor het opnemen van grote hoeveelheden gegevens als een stroom.</span><span class="sxs-lookup"><span data-stu-id="19015-115">Azure Blob storage can be used as an input source for ingesting bulk data as a stream.</span></span>  
* <span data-ttu-id="19015-116">**Referentiegegevens**: Stream Analytics ondersteunt een tweede gegevenstype reserve invoerverwijzing genoemd.</span><span class="sxs-lookup"><span data-stu-id="19015-116">**Reference data**: Stream Analytics supports a second type of auxiliary input called reference data.</span></span>  <span data-ttu-id="19015-117">In plaats van de gegevens in beweging, worden deze gegevens zijn statisch of vertraging wijzigen.</span><span class="sxs-lookup"><span data-stu-id="19015-117">As opposed to data in motion, this data is static or slowing changing.</span></span>  <span data-ttu-id="19015-118">Dit wordt meestal gebruikt voor het uitvoeren van de op te zoeken en correlatie met gegevensstromen voor het maken van een uitgebreidere set van gegevens.</span><span class="sxs-lookup"><span data-stu-id="19015-118">It is typically used for performing look-ups and correlations with data streams to create a richer data set.</span></span>  <span data-ttu-id="19015-119">Azure Blob-opslag is momenteel de enige ondersteunde invoerbron voor referentiegegevens.</span><span class="sxs-lookup"><span data-stu-id="19015-119">Azure Blob storage is currently the only supported input source for reference data.</span></span>  

<span data-ttu-id="19015-120">Een invoer toevoegen aan Stream Analytics-taak:</span><span class="sxs-lookup"><span data-stu-id="19015-120">To add an input to your Stream Analytics job:</span></span>

1. <span data-ttu-id="19015-121">Klik in de Azure portal op **invoer** en klik vervolgens op **invoer toevoegen** in uw Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="19015-121">In the Azure portal click **Inputs** and then click **Add an Input** in your Stream Analytics job.</span></span>
   
    ![Klassieke Azure-portal - invoer toevoegen.](./media/stream-analytics-add-inputs/1-stream-analytics-add-inputs.png)  
   
    <span data-ttu-id="19015-123">Klik in de Azure portal op de **invoer** -tegel in de Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="19015-123">In the Azure portal click the **Inputs** tile in your Stream Analytics job.</span></span>  
   
    ![Azure-portal - invoer toevoegen.](./media/stream-analytics-add-inputs/7-stream-analytics-add-inputs.png)  
2. <span data-ttu-id="19015-125">Geef het type van de invoer: beide **gegevensstroom** of **referentiegegevens**.</span><span class="sxs-lookup"><span data-stu-id="19015-125">Specify the type of the input: either **Data stream** or **Reference data**.</span></span>
   
    ![Voer, gestreamd of verwijst naar de juiste gegevens toevoegen](./media/stream-analytics-add-inputs/2-stream-analytics-add-inputs.png)  
   
    ![Voer, gestreamd of verwijst naar de juiste gegevens toevoegen](./media/stream-analytics-add-inputs/8-stream-analytics-add-inputs.png)  
3. <span data-ttu-id="19015-128">Als een gegevensstroom invoer maakt, geeft u het brontype voor de invoer.</span><span class="sxs-lookup"><span data-stu-id="19015-128">If creating a Data Stream input, specify the source type for the input.</span></span>  <span data-ttu-id="19015-129">Deze stap worden overgeslagen tijdens het maken van referentiegegevens als alleen-Blob-opslag op dit moment wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="19015-129">This step can be skipped during Reference Data creation as only Blob storage is supported at this time.</span></span>
   
    ![Gegevens gegevensstroominvoer toevoegen](./media/stream-analytics-add-inputs/3-stream-analytics-add-inputs.png)  
   
    ![Gegevens gegevensstroominvoer toevoegen](./media/stream-analytics-add-inputs/9-stream-analytics-add-inputs.png)  
4. <span data-ttu-id="19015-132">Geef een beschrijvende naam voor deze invoer in het vak Invoeralias.</span><span class="sxs-lookup"><span data-stu-id="19015-132">Provide a friendly name for this input in the Input Alias box.</span></span>  <span data-ttu-id="19015-133">Deze naam wordt gebruikt in uw job query later op om te verwijzen naar de invoer.</span><span class="sxs-lookup"><span data-stu-id="19015-133">This name will be used in your job's query later on to refer to the input.</span></span>
   
    <span data-ttu-id="19015-134">Vul in de rest van de vereiste verbindingseigenschappen verbinding maken met de gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="19015-134">Fill in the rest of the required connection properties to connect to your data source.</span></span> <span data-ttu-id="19015-135">Deze velden verschillen per type van het type invoer- en bron en worden gedefinieerd in detail [hier](stream-analytics-create-a-job.md).</span><span class="sxs-lookup"><span data-stu-id="19015-135">These fields vary by type of input and source type and are defined in detail [here](stream-analytics-create-a-job.md).</span></span>  
   
    ![Event hub gegevensinvoer toevoegen](./media/stream-analytics-add-inputs/4-stream-analytics-add-inputs.png)  
5. <span data-ttu-id="19015-137">Geef de serialisatie-instellingen voor de ingevoerde gegevens:</span><span class="sxs-lookup"><span data-stu-id="19015-137">Specify the serialization settings for the input data:</span></span>
   
   * <span data-ttu-id="19015-138">Om er zeker van te zijn uw query's werken zoals verwacht, geef de **gebeurtenis serialisatie-indeling** van binnenkomende gegevens.</span><span class="sxs-lookup"><span data-stu-id="19015-138">To make sure your queries work the way you expect, specify the **Event Serialization Format** of incoming data.</span></span>  <span data-ttu-id="19015-139">Ondersteunde serialisatie-indelingen zijn JSON, CSV en Avro.</span><span class="sxs-lookup"><span data-stu-id="19015-139">Supported serialization formats are JSON, CSV, and Avro.</span></span>
   * <span data-ttu-id="19015-140">Controleer of de **codering** voor de gegevens.</span><span class="sxs-lookup"><span data-stu-id="19015-140">Verify the **Encoding** for the data.</span></span>  <span data-ttu-id="19015-141">Alleen de coderingsindeling UTF-8 wordt momenteel ondersteund.</span><span class="sxs-lookup"><span data-stu-id="19015-141">UTF-8 is the only supported encoding format at this time.</span></span>
     
     ![Instellingen voor serialisatie van gegevens voor de gegevens invoeren](./media/stream-analytics-add-inputs/5-stream-analytics-add-inputs.png)  
     
     ![Instellingen voor serialisatie van gegevens voor de gegevens invoeren](./media/stream-analytics-add-inputs/10-stream-analytics-add-inputs.png)  
6. <span data-ttu-id="19015-144">Na het voltooien van het maken van de invoer, Stream Analytics controleert of dat deze verbinding met de invoerbron maken kan.</span><span class="sxs-lookup"><span data-stu-id="19015-144">After completing the input creation, Stream Analytics will verify that it can connect to the input source.</span></span>  <span data-ttu-id="19015-145">U kunt de status van de bewerking verbinding testen bekijken in de Notification hub.</span><span class="sxs-lookup"><span data-stu-id="19015-145">You can view the status of the Test Connection operation in the Notification hub.</span></span>
   
    ![Verbinding van de invoer streaminggegevens testen](./media/stream-analytics-add-inputs/6-stream-analytics-add-inputs.png)  
   
    ![Verbinding van de invoer streaminggegevens testen](./media/stream-analytics-add-inputs/11-stream-analytics-add-inputs.png)  

## <a name="get-help-with-streaming-data-inputs"></a><span data-ttu-id="19015-148">Hulp bij het streaming-gegevens invoeren</span><span class="sxs-lookup"><span data-stu-id="19015-148">Get help with streaming data inputs</span></span>
<span data-ttu-id="19015-149">Voor verdere hulp kunt u mogelijk terecht op het [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="19015-149">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="19015-150">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="19015-150">Next steps</span></span>
* [<span data-ttu-id="19015-151">Inleiding tot Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="19015-151">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="19015-152">Aan de slag met Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="19015-152">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="19015-153">Azure Stream Analytics-taken schalen</span><span class="sxs-lookup"><span data-stu-id="19015-153">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="19015-154">Naslaggids voor Azure Stream Analytics Query</span><span class="sxs-lookup"><span data-stu-id="19015-154">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="19015-155">REST API-naslaggids voor Azure Stream Analytics Management</span><span class="sxs-lookup"><span data-stu-id="19015-155">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

