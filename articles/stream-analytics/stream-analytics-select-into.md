---
title: aaaDebug Azure Stream Analytics query's met behulp van SELECT INTO | Microsoft Docs
description: Gegevens halverwege voorbeeldquery met behulp van een instructie SELECT INTO in Stream Analytics
keywords: 
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9952e2cf-b335-4a5c-8f45-8d3e1eda2e20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 27e41af1a6ea06b4509d07a3a67087490d0ec1fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="debug-queries-by-using-select-into-statements"></a><span data-ttu-id="aebe9-103">Fouten opsporen in query's met behulp van een instructie SELECT INTO</span><span class="sxs-lookup"><span data-stu-id="aebe9-103">Debug queries by using SELECT INTO statements</span></span>

<span data-ttu-id="aebe9-104">In realtime-gegevensverwerking weten welke gegevens Hallo lijkt erop dat in het midden van Hallo Hallo query handig kan zijn.</span><span class="sxs-lookup"><span data-stu-id="aebe9-104">In real-time data processing, knowing what hello data looks like in hello middle of hello query can be helpful.</span></span> <span data-ttu-id="aebe9-105">Omdat de invoer- of stappen van een Azure Stream Analytics-taak kunnen meerdere keren worden gelezen, kunt u extra SELECT INTO-instructies schrijven.</span><span class="sxs-lookup"><span data-stu-id="aebe9-105">Because inputs or steps of an Azure Stream Analytics job can be read multiple times, you can write extra SELECT INTO statements.</span></span> <span data-ttu-id="aebe9-106">In dat geval voert tussenliggende gegevens naar de opslag en kunt u controleren Hallo juistheid van Hallo gegevens, net zoals *bekijken variabelen* doen wanneer u een programma foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="aebe9-106">Doing so outputs intermediate data into storage and lets you inspect hello correctness of hello data, just as *watch variables* do when you debug a program.</span></span>

## <a name="use-select-into-toocheck-hello-data-stream"></a><span data-ttu-id="aebe9-107">SELECT INTO toocheck Hallo gegevensstroom gebruiken</span><span class="sxs-lookup"><span data-stu-id="aebe9-107">Use SELECT INTO toocheck hello data stream</span></span>

<span data-ttu-id="aebe9-108">Hallo heeft volgende voorbeeldquery in een Azure Stream Analytics-taak een Stroominvoer, twee verwijzing gegevens invoeren en een uitvoer-tooAzure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="aebe9-108">hello following example query in an Azure Stream Analytics job has one stream input, two reference data inputs, and an output tooAzure Table Storage.</span></span> <span data-ttu-id="aebe9-109">Hallo query lid wordt van gegevens van Hallo event hub en twee referentie blobs tooget Hallo naam en categorie-informatie:</span><span class="sxs-lookup"><span data-stu-id="aebe9-109">hello query joins data from hello event hub and two reference blobs tooget hello name and category information:</span></span>

![Voorbeeld van de SELECT INTO-query](./media/stream-analytics-select-into/stream-analytics-select-into-query1.png)

<span data-ttu-id="aebe9-111">Houd er rekening mee dat Hallo-taak wordt uitgevoerd, maar er zijn geen gebeurtenissen zijn in Hallo uitvoer wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="aebe9-111">Note that hello job is running, but no events are being produced in hello output.</span></span> <span data-ttu-id="aebe9-112">Op Hallo **bewaking** tegel, die hier worden weergegeven, kunt u zien dat Hallo-invoer is het opstellen van gegevens, maar u niet welke stap van Hallo weet **JOIN** veroorzaakt alle Hallo gebeurtenissen toobe verwijderd.</span><span class="sxs-lookup"><span data-stu-id="aebe9-112">On hello **Monitoring** tile, shown here, you can see that hello input is producing data, but you don’t know which step of hello **JOIN** caused all hello events toobe dropped.</span></span>

![Hallo bewaking tegel](./media/stream-analytics-select-into/stream-analytics-select-into-monitor.png)
 
<span data-ttu-id="aebe9-114">In dit geval kunt u een paar extra SELECT INTO-instructies te 'melden' hello tussenliggende JOIN-resultaten en Hallo gegevens dat gelezen uit Hallo invoer toevoegen.</span><span class="sxs-lookup"><span data-stu-id="aebe9-114">In this situation, you can add a few extra SELECT INTO statements too“log” hello intermediate JOIN results and hello data that's read from hello input.</span></span>

<span data-ttu-id="aebe9-115">In dit voorbeeld toegevoegd twee nieuwe 'tijdelijke uitvoer."</span><span class="sxs-lookup"><span data-stu-id="aebe9-115">In this example, we've added two new “temporary outputs.”</span></span> <span data-ttu-id="aebe9-116">Ze kunnen worden alle gewenste sink.</span><span class="sxs-lookup"><span data-stu-id="aebe9-116">They can be any sink you like.</span></span> <span data-ttu-id="aebe9-117">We gebruiken hier Azure Storage als een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="aebe9-117">Here we use Azure Storage as an example:</span></span>

![Toevoegen van extra SELECT INTO-instructies](./media/stream-analytics-select-into/stream-analytics-select-into-outputs.png)

<span data-ttu-id="aebe9-119">U kunt vervolgens herschrijven Hallo query als volgt:</span><span class="sxs-lookup"><span data-stu-id="aebe9-119">You can then rewrite hello query like this:</span></span>

![Herschreven SELECT INTO-query](./media/stream-analytics-select-into/stream-analytics-select-into-query2.png)

<span data-ttu-id="aebe9-121">Nu Hallo taak opnieuw starten en laten uitvoeren voor een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="aebe9-121">Now start hello job again, and let it run for a few minutes.</span></span> <span data-ttu-id="aebe9-122">Vervolgens query temp1 en Tijdelijk2 met Visual Studio Cloud Explorer tooproduce Hallo tabellen te volgen:</span><span class="sxs-lookup"><span data-stu-id="aebe9-122">Then query temp1 and temp2 with Visual Studio Cloud Explorer tooproduce hello following tables:</span></span>

<span data-ttu-id="aebe9-123">**tabel temp1**
![SELECT INTO temp1 tabel](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)</span><span class="sxs-lookup"><span data-stu-id="aebe9-123">**temp1 table**
![SELECT INTO temp1 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)</span></span>

<span data-ttu-id="aebe9-124">**tabel Tijdelijk2**
![SELECT INTO Tijdelijk2 tabel](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)</span><span class="sxs-lookup"><span data-stu-id="aebe9-124">**temp2 table**
![SELECT INTO temp2 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)</span></span>

<span data-ttu-id="aebe9-125">Zoals u ziet, temp1 en Tijdelijk2 gegevens hebt en Hallo naamkolom correct in Tijdelijk2 is ingevuld.</span><span class="sxs-lookup"><span data-stu-id="aebe9-125">As you can see, temp1 and temp2 both have data, and hello name column is populated correctly in temp2.</span></span> <span data-ttu-id="aebe9-126">Echter, omdat er nog geen gegevens in de uitvoer, er is iets mis:</span><span class="sxs-lookup"><span data-stu-id="aebe9-126">However, because there is still no data in output, something is wrong:</span></span>

![SELECT INTO output1 tabel zonder gegevens](./media/stream-analytics-select-into/stream-analytics-select-into-out-table-1.png)

<span data-ttu-id="aebe9-128">Door middel van steekproeven Hallo gegevens, kunt u zijn bijna zeker weet dat Hallo probleem met de Hallo is tweede JOIN.</span><span class="sxs-lookup"><span data-stu-id="aebe9-128">By sampling hello data, you can be almost certain that hello issue is with hello second JOIN.</span></span> <span data-ttu-id="aebe9-129">U kunt downloaden van Hallo referentiegegevens van Hallo-blob en te bekijken:</span><span class="sxs-lookup"><span data-stu-id="aebe9-129">You can download hello reference data from hello blob and take a look:</span></span>

![SELECT INTO ref-tabel](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-1.png)

<span data-ttu-id="aebe9-131">Zoals u ziet, wijkt Hallo-indeling van GUID Hallo in deze referentiegegevens af van Hallo-indeling van Hallo [uit]-kolom in Tijdelijk2.</span><span class="sxs-lookup"><span data-stu-id="aebe9-131">As you can see, hello format of hello GUID in this reference data is different from hello format of hello [from] column in temp2.</span></span> <span data-ttu-id="aebe9-132">Daarom is Hallo gegevens niet aangekomen in output1 zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="aebe9-132">That’s why hello data didn’t arrive in output1 as expected.</span></span>

<span data-ttu-id="aebe9-133">U kunt oplossen gegevensindeling hello, tooreference blob te uploaden en probeer het opnieuw:</span><span class="sxs-lookup"><span data-stu-id="aebe9-133">You can fix hello data format, upload it tooreference blob, and try again:</span></span>

![SELECT INTO tijdelijke tabel](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-2.png)

<span data-ttu-id="aebe9-135">Deze tijd wordt Hallo-gegevens in de uitvoer van de Hallo geformatteerd en ingevuld zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="aebe9-135">This time, hello data in hello output is formatted and populated as expected.</span></span>

![Selecteer in de laatste tabel](./media/stream-analytics-select-into/stream-analytics-select-into-final-table.png)


## <a name="get-help"></a><span data-ttu-id="aebe9-137">Help opvragen</span><span class="sxs-lookup"><span data-stu-id="aebe9-137">Get help</span></span>

<span data-ttu-id="aebe9-138">Voor verdere hulp kunt u proberen onze [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="aebe9-138">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="aebe9-139">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="aebe9-139">Next steps</span></span>

* [<span data-ttu-id="aebe9-140">Inleiding tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="aebe9-140">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="aebe9-141">Aan de slag met Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="aebe9-141">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="aebe9-142">Azure Stream Analytics-taken schalen</span><span class="sxs-lookup"><span data-stu-id="aebe9-142">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="aebe9-143">Naslaggids voor Azure Stream Analytics Query</span><span class="sxs-lookup"><span data-stu-id="aebe9-143">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="aebe9-144">REST API-naslaggids voor Azure Stream Analytics Management</span><span class="sxs-lookup"><span data-stu-id="aebe9-144">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

