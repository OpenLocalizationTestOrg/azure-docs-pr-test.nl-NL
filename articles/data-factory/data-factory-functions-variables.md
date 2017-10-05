---
title: Data Factory-functies en systeemvariabelen | Microsoft Docs
description: Geeft een lijst van Azure Data Factory-functies en systeemvariabelen
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
services: data-factory
ms.assetid: b6b3c2ae-b0e8-4e28-90d8-daf20421660d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 72a966bdc271f86b9568d3310d2e22d83b447594
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-data-factory---functions-and-system-variables"></a><span data-ttu-id="1a5af-103">Azure Data Factory - functies en systeemvariabelen</span><span class="sxs-lookup"><span data-stu-id="1a5af-103">Azure Data Factory - Functions and System Variables</span></span>
<span data-ttu-id="1a5af-104">Dit artikel bevat informatie over functies en variabelen die worden ondersteund door Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1a5af-104">This article provides information about functions and variables supported by Azure Data Factory.</span></span>

## <a name="data-factory-system-variables"></a><span data-ttu-id="1a5af-105">Data Factory-systeemvariabelen</span><span class="sxs-lookup"><span data-stu-id="1a5af-105">Data Factory system variables</span></span>
| <span data-ttu-id="1a5af-106">Naam variabele</span><span class="sxs-lookup"><span data-stu-id="1a5af-106">Variable Name</span></span> | <span data-ttu-id="1a5af-107">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="1a5af-107">Description</span></span> | <span data-ttu-id="1a5af-108">Bereik van het object</span><span class="sxs-lookup"><span data-stu-id="1a5af-108">Object Scope</span></span> | <span data-ttu-id="1a5af-109">JSON-bereik en gebruiksvoorbeelden</span><span class="sxs-lookup"><span data-stu-id="1a5af-109">JSON Scope and Use Cases</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a5af-110">WindowStart</span><span class="sxs-lookup"><span data-stu-id="1a5af-110">WindowStart</span></span> |<span data-ttu-id="1a5af-111">Begin van het tijdsinterval voor de huidige activiteit venster uitvoeren</span><span class="sxs-lookup"><span data-stu-id="1a5af-111">Start of time interval for current activity run window</span></span> |<span data-ttu-id="1a5af-112">Activiteit</span><span class="sxs-lookup"><span data-stu-id="1a5af-112">activity</span></span> |<ol><li><span data-ttu-id="1a5af-113">Geef op query's voor selectie.</span><span class="sxs-lookup"><span data-stu-id="1a5af-113">Specify data selection queries.</span></span> <span data-ttu-id="1a5af-114">Zie connector artikelen waarnaar wordt verwezen in de [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="1a5af-114">See connector articles referenced in the [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span></li> |
| <span data-ttu-id="1a5af-115">WindowEnd</span><span class="sxs-lookup"><span data-stu-id="1a5af-115">WindowEnd</span></span> |<span data-ttu-id="1a5af-116">Einde van het tijdsinterval voor de huidige activiteit venster uitvoeren</span><span class="sxs-lookup"><span data-stu-id="1a5af-116">End of time interval for current activity run window</span></span> |<span data-ttu-id="1a5af-117">Activiteit</span><span class="sxs-lookup"><span data-stu-id="1a5af-117">activity</span></span> |<span data-ttu-id="1a5af-118">hetzelfde als WindowStart.</span><span class="sxs-lookup"><span data-stu-id="1a5af-118">same as WindowStart.</span></span> |
| <span data-ttu-id="1a5af-119">SliceStart</span><span class="sxs-lookup"><span data-stu-id="1a5af-119">SliceStart</span></span> |<span data-ttu-id="1a5af-120">Begin van het tijdsinterval voor het segment wordt geproduceerd</span><span class="sxs-lookup"><span data-stu-id="1a5af-120">Start of time interval for data  slice being produced</span></span> |<span data-ttu-id="1a5af-121">Activiteit</span><span class="sxs-lookup"><span data-stu-id="1a5af-121">activity</span></span><br/><span data-ttu-id="1a5af-122">Gegevensset</span><span class="sxs-lookup"><span data-stu-id="1a5af-122">dataset</span></span> |<ol><li><span data-ttu-id="1a5af-123">Geef dynamische paden en bestandsnamen tijdens het werken met [Azure Blob](data-factory-azure-blob-connector.md) en [bestandssysteem gegevenssets](data-factory-onprem-file-system-connector.md).</span><span class="sxs-lookup"><span data-stu-id="1a5af-123">Specify dynamic folder paths and file names while working with [Azure Blob](data-factory-azure-blob-connector.md) and [File System datasets](data-factory-onprem-file-system-connector.md).</span></span></li><li><span data-ttu-id="1a5af-124">Invoer afhankelijkheden data factory-functies in activiteit invoer verzameling opgeven.</span><span class="sxs-lookup"><span data-stu-id="1a5af-124">Specify input dependencies with data factory functions in activity inputs collection.</span></span></li></ol> |
| <span data-ttu-id="1a5af-125">SliceEnd</span><span class="sxs-lookup"><span data-stu-id="1a5af-125">SliceEnd</span></span> |<span data-ttu-id="1a5af-126">Einde van de tijdsinterval voor het huidige segment.</span><span class="sxs-lookup"><span data-stu-id="1a5af-126">End of time interval for current data slice.</span></span> |<span data-ttu-id="1a5af-127">Activiteit</span><span class="sxs-lookup"><span data-stu-id="1a5af-127">activity</span></span><br/><span data-ttu-id="1a5af-128">Gegevensset</span><span class="sxs-lookup"><span data-stu-id="1a5af-128">dataset</span></span> |<span data-ttu-id="1a5af-129">hetzelfde als SliceStart.</span><span class="sxs-lookup"><span data-stu-id="1a5af-129">same as SliceStart.</span></span> |

> [!NOTE]
> <span data-ttu-id="1a5af-130">Op dit moment vereist gegevensfactory dat de planning die is opgegeven in de activiteit exact overeenkomt met het schema dat is opgegeven in de beschikbaarheid van de uitvoergegevensset.</span><span class="sxs-lookup"><span data-stu-id="1a5af-130">Currently data factory requires that the schedule specified in the activity exactly matches the schedule specified in availability of the output dataset.</span></span> <span data-ttu-id="1a5af-131">Daarom WindowStart, WindowEnd, en SliceStart en SliceEnd altijd toegewezen aan dezelfde periode en een segment één uitvoer.</span><span class="sxs-lookup"><span data-stu-id="1a5af-131">Therefore, WindowStart, WindowEnd, and SliceStart and SliceEnd always map to the same time period and a single output slice.</span></span>
> 

### <a name="example-for-using-a-system-variable"></a><span data-ttu-id="1a5af-132">Voorbeeld voor het gebruik van een systeemvariabele</span><span class="sxs-lookup"><span data-stu-id="1a5af-132">Example for using a system variable</span></span>
<span data-ttu-id="1a5af-133">In het volgende voorbeeld, jaar, maand, dag en tijd van **SliceStart** worden uitgepakt in verschillende variabelen die worden gebruikt door **folderPath** en **fileName** eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="1a5af-133">In the following example, year, month, day, and time of **SliceStart** are extracted into separate variables that are used by **folderPath** and **fileName** properties.</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```

## <a name="data-factory-functions"></a><span data-ttu-id="1a5af-134">Data Factory-functies</span><span class="sxs-lookup"><span data-stu-id="1a5af-134">Data Factory functions</span></span>
<span data-ttu-id="1a5af-135">U kunt functies gebruiken in gegevensfactory samen met de variabelen voor de volgende doeleinden:</span><span class="sxs-lookup"><span data-stu-id="1a5af-135">You can use functions in data factory along with system variables for the following purposes:</span></span>

1. <span data-ttu-id="1a5af-136">Query's voor selectie opgeven (Zie connector artikelen waarnaar wordt verwezen door de [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="1a5af-136">Specifying data selection queries (see connector articles referenced by the [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span>
   
   <span data-ttu-id="1a5af-137">De syntaxis voor het aanroepen van een data factory-functie is:  **$$ <function>**  voor selectie van query's en andere eigenschappen in de activiteit en gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="1a5af-137">The syntax to invoke a data factory function is: **$$<function>** for data selection queries and other properties in the activity and datasets.</span></span>  
2. <span data-ttu-id="1a5af-138">Invoer afhankelijkheden opgeven data factory-functies in activiteit invoer verzameling.</span><span class="sxs-lookup"><span data-stu-id="1a5af-138">Specifying input dependencies with data factory functions in activity inputs collection.</span></span>
   
    <span data-ttu-id="1a5af-139">$$ is niet nodig voor het opgeven van invoer afhankelijkheid expressies.</span><span class="sxs-lookup"><span data-stu-id="1a5af-139">$$ is not needed for specifying input dependency expressions.</span></span>     

<span data-ttu-id="1a5af-140">In het volgende voorbeeld, **sqlReaderQuery** eigenschap in een JSON-bestand is toegewezen aan een waarde die is geretourneerd door de `Text.Format` functie.</span><span class="sxs-lookup"><span data-stu-id="1a5af-140">In the following sample, **sqlReaderQuery** property in a JSON file is assigned to a value returned by the `Text.Format` function.</span></span> <span data-ttu-id="1a5af-141">Dit voorbeeld gebruikt ook een systeemvariabele met de naam **WindowStart**, die staat voor de begintijd van het venster van de activiteit die wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1a5af-141">This sample also uses a system variable named **WindowStart**, which represents the start time of the activity run window.</span></span>

```json
{
    "Type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('SELECT * FROM MyTable WHERE StartTime = \\'{0:yyyyMMdd-HH}\\'', WindowStart)"
}
```

<span data-ttu-id="1a5af-142">Zie [aangepaste datum en tijd-indeling tekenreeksen](https://msdn.microsoft.com/library/8kb3ddd4.aspx) onderwerp dat beschrijft de verschillende opmaakopties die u kunt gebruiken (bijvoorbeeld: ay versus jjjj).</span><span class="sxs-lookup"><span data-stu-id="1a5af-142">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: ay vs. yyyy).</span></span> 

### <a name="functions"></a><span data-ttu-id="1a5af-143">Functies</span><span class="sxs-lookup"><span data-stu-id="1a5af-143">Functions</span></span>
<span data-ttu-id="1a5af-144">De volgende tabellen worden de functies in Azure Data Factory:</span><span class="sxs-lookup"><span data-stu-id="1a5af-144">The following tables list all the functions in Azure Data Factory:</span></span>

| <span data-ttu-id="1a5af-145">Category</span><span class="sxs-lookup"><span data-stu-id="1a5af-145">Category</span></span> | <span data-ttu-id="1a5af-146">Functie</span><span class="sxs-lookup"><span data-stu-id="1a5af-146">Function</span></span> | <span data-ttu-id="1a5af-147">Parameters</span><span class="sxs-lookup"><span data-stu-id="1a5af-147">Parameters</span></span> | <span data-ttu-id="1a5af-148">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="1a5af-148">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a5af-149">Time</span><span class="sxs-lookup"><span data-stu-id="1a5af-149">Time</span></span> |<span data-ttu-id="1a5af-150">AddHours(X,Y)</span><span class="sxs-lookup"><span data-stu-id="1a5af-150">AddHours(X,Y)</span></span> |<span data-ttu-id="1a5af-151">X: datum/tijd</span><span class="sxs-lookup"><span data-stu-id="1a5af-151">X: DateTime</span></span> <br/><br/><span data-ttu-id="1a5af-152">Y: int</span><span class="sxs-lookup"><span data-stu-id="1a5af-152">Y: int</span></span> |<span data-ttu-id="1a5af-153">Y uren toevoegt aan de opgegeven tijd X.</span><span class="sxs-lookup"><span data-stu-id="1a5af-153">Adds Y hours to the given time X.</span></span> <br/><br/><span data-ttu-id="1a5af-154">Voorbeeld:`9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="1a5af-154">Example: `9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM`</span></span> |
| <span data-ttu-id="1a5af-155">Time</span><span class="sxs-lookup"><span data-stu-id="1a5af-155">Time</span></span> |<span data-ttu-id="1a5af-156">AddMinutes(X,Y)</span><span class="sxs-lookup"><span data-stu-id="1a5af-156">AddMinutes(X,Y)</span></span> |<span data-ttu-id="1a5af-157">X: datum/tijd</span><span class="sxs-lookup"><span data-stu-id="1a5af-157">X: DateTime</span></span> <br/><br/><span data-ttu-id="1a5af-158">Y: int</span><span class="sxs-lookup"><span data-stu-id="1a5af-158">Y: int</span></span> |<span data-ttu-id="1a5af-159">Voegt Y minuten tot en met X.</span><span class="sxs-lookup"><span data-stu-id="1a5af-159">Adds Y minutes to X.</span></span><br/><br/><span data-ttu-id="1a5af-160">Voorbeeld:`9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM`</span><span class="sxs-lookup"><span data-stu-id="1a5af-160">Example: `9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM`</span></span> |
| <span data-ttu-id="1a5af-161">Time</span><span class="sxs-lookup"><span data-stu-id="1a5af-161">Time</span></span> |<span data-ttu-id="1a5af-162">StartOfHour(X)</span><span class="sxs-lookup"><span data-stu-id="1a5af-162">StartOfHour(X)</span></span> |<span data-ttu-id="1a5af-163">X: datum/tijd</span><span class="sxs-lookup"><span data-stu-id="1a5af-163">X: Datetime</span></span> |<span data-ttu-id="1a5af-164">Hiermee haalt u de begintijd voor het uur dat wordt vertegenwoordigd door het uurgedeelte van X.</span><span class="sxs-lookup"><span data-stu-id="1a5af-164">Gets the starting time for the hour represented by the hour component of X.</span></span> <br/><br/><span data-ttu-id="1a5af-165">Voorbeeld:`StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="1a5af-165">Example: `StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM`</span></span> |
| <span data-ttu-id="1a5af-166">Date</span><span class="sxs-lookup"><span data-stu-id="1a5af-166">Date</span></span> |<span data-ttu-id="1a5af-167">AddDays(X,Y)</span><span class="sxs-lookup"><span data-stu-id="1a5af-167">AddDays(X,Y)</span></span> |<span data-ttu-id="1a5af-168">X: datum/tijd</span><span class="sxs-lookup"><span data-stu-id="1a5af-168">X: DateTime</span></span><br/><br/><span data-ttu-id="1a5af-169">Y: int</span><span class="sxs-lookup"><span data-stu-id="1a5af-169">Y: int</span></span> |<span data-ttu-id="1a5af-170">Voegt Y dagen tot en met X.</span><span class="sxs-lookup"><span data-stu-id="1a5af-170">Adds Y days to X.</span></span> <br/><br/><span data-ttu-id="1a5af-171">Voorbeeld: 9, 15/2013 12:00:00 PM + 2 dagen = 9/17/2013 12:00:00 PM.</span><span class="sxs-lookup"><span data-stu-id="1a5af-171">Example: 9/15/2013 12:00:00 PM + 2 days = 9/17/2013 12:00:00 PM.</span></span><br/><br/><span data-ttu-id="1a5af-172">U kunt dagen te aftrekken door te geven Y als een negatief getal.</span><span class="sxs-lookup"><span data-stu-id="1a5af-172">You can subtract days too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="1a5af-173">Voorbeeld: `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="1a5af-173">Example: `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`.</span></span> |
| <span data-ttu-id="1a5af-174">Date</span><span class="sxs-lookup"><span data-stu-id="1a5af-174">Date</span></span> |<span data-ttu-id="1a5af-175">AddMonths(X,Y)</span><span class="sxs-lookup"><span data-stu-id="1a5af-175">AddMonths(X,Y)</span></span> |<span data-ttu-id="1a5af-176">X: datum/tijd</span><span class="sxs-lookup"><span data-stu-id="1a5af-176">X: DateTime</span></span><br/><br/><span data-ttu-id="1a5af-177">Y: int</span><span class="sxs-lookup"><span data-stu-id="1a5af-177">Y: int</span></span> |<span data-ttu-id="1a5af-178">Voegt Y maanden tot en met X.</span><span class="sxs-lookup"><span data-stu-id="1a5af-178">Adds Y months to X.</span></span><br/><br/><span data-ttu-id="1a5af-179">`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="1a5af-179">`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.</span></span><br/><br/><span data-ttu-id="1a5af-180">U kunt maanden te aftrekken door te geven Y als een negatief getal.</span><span class="sxs-lookup"><span data-stu-id="1a5af-180">You can subtract months too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="1a5af-181">Voorbeeld: `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="1a5af-181">Example: `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.</span></span>|
| <span data-ttu-id="1a5af-182">Date</span><span class="sxs-lookup"><span data-stu-id="1a5af-182">Date</span></span> |<span data-ttu-id="1a5af-183">AddQuarters(X,Y)</span><span class="sxs-lookup"><span data-stu-id="1a5af-183">AddQuarters(X,Y)</span></span> |<span data-ttu-id="1a5af-184">X: datum/tijd</span><span class="sxs-lookup"><span data-stu-id="1a5af-184">X: DateTime</span></span> <br/><br/><span data-ttu-id="1a5af-185">Y: int</span><span class="sxs-lookup"><span data-stu-id="1a5af-185">Y: int</span></span> |<span data-ttu-id="1a5af-186">Voegt Y * X 3 maanden.</span><span class="sxs-lookup"><span data-stu-id="1a5af-186">Adds Y * 3 months to X.</span></span><br/><br/><span data-ttu-id="1a5af-187">Voorbeeld:`9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="1a5af-187">Example: `9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM`</span></span> |
| <span data-ttu-id="1a5af-188">Date</span><span class="sxs-lookup"><span data-stu-id="1a5af-188">Date</span></span> |<span data-ttu-id="1a5af-189">AddWeeks(X,Y)</span><span class="sxs-lookup"><span data-stu-id="1a5af-189">AddWeeks(X,Y)</span></span> |<span data-ttu-id="1a5af-190">X: datum/tijd</span><span class="sxs-lookup"><span data-stu-id="1a5af-190">X: DateTime</span></span><br/><br/><span data-ttu-id="1a5af-191">Y: int</span><span class="sxs-lookup"><span data-stu-id="1a5af-191">Y: int</span></span> |<span data-ttu-id="1a5af-192">Voegt Y * X 7 dagen</span><span class="sxs-lookup"><span data-stu-id="1a5af-192">Adds Y * 7 days to X</span></span><br/><br/><span data-ttu-id="1a5af-193">Voorbeeld: 9, 15/2013 12:00:00 PM + 1 week = 9/22/2013 12:00:00 uur</span><span class="sxs-lookup"><span data-stu-id="1a5af-193">Example: 9/15/2013 12:00:00 PM + 1 week = 9/22/2013 12:00:00 PM</span></span><br/><br/><span data-ttu-id="1a5af-194">U kunt de weken te aftrekken door te geven Y als een negatief getal.</span><span class="sxs-lookup"><span data-stu-id="1a5af-194">You can subtract weeks too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="1a5af-195">Voorbeeld: `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="1a5af-195">Example: `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`.</span></span> |
| <span data-ttu-id="1a5af-196">Date</span><span class="sxs-lookup"><span data-stu-id="1a5af-196">Date</span></span> |<span data-ttu-id="1a5af-197">AddYears(X,Y)</span><span class="sxs-lookup"><span data-stu-id="1a5af-197">AddYears(X,Y)</span></span> |<span data-ttu-id="1a5af-198">X: datum/tijd</span><span class="sxs-lookup"><span data-stu-id="1a5af-198">X: DateTime</span></span><br/><br/><span data-ttu-id="1a5af-199">Y: int</span><span class="sxs-lookup"><span data-stu-id="1a5af-199">Y: int</span></span> |<span data-ttu-id="1a5af-200">Voegt Y jaar tot en met X.</span><span class="sxs-lookup"><span data-stu-id="1a5af-200">Adds Y years to X.</span></span><br/><br/>`Example: 9/15/2013 12:00:00 PM + 1 year = 9/15/2014 12:00:00 PM`<br/><br/><span data-ttu-id="1a5af-201">U kunt jaar te aftrekken door te geven Y als een negatief getal.</span><span class="sxs-lookup"><span data-stu-id="1a5af-201">You can subtract years too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="1a5af-202">Voorbeeld: `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="1a5af-202">Example: `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`.</span></span> |
| <span data-ttu-id="1a5af-203">Date</span><span class="sxs-lookup"><span data-stu-id="1a5af-203">Date</span></span> |<span data-ttu-id="1a5af-204">Day(X)</span><span class="sxs-lookup"><span data-stu-id="1a5af-204">Day(X)</span></span> |<span data-ttu-id="1a5af-205">X: datum/tijd</span><span class="sxs-lookup"><span data-stu-id="1a5af-205">X: DateTime</span></span> |<span data-ttu-id="1a5af-206">Hiermee haalt u het daggedeelte van X.</span><span class="sxs-lookup"><span data-stu-id="1a5af-206">Gets the day component of X.</span></span><br/><br/><span data-ttu-id="1a5af-207">Voorbeeld: `Day of 9/15/2013 12:00:00 PM is 9`.</span><span class="sxs-lookup"><span data-stu-id="1a5af-207">Example: `Day of 9/15/2013 12:00:00 PM is 9`.</span></span> |
| <span data-ttu-id="1a5af-208">Date</span><span class="sxs-lookup"><span data-stu-id="1a5af-208">Date</span></span> |<span data-ttu-id="1a5af-209">DayOfWeek(X)</span><span class="sxs-lookup"><span data-stu-id="1a5af-209">DayOfWeek(X)</span></span> |<span data-ttu-id="1a5af-210">X: datum/tijd</span><span class="sxs-lookup"><span data-stu-id="1a5af-210">X: DateTime</span></span> |<span data-ttu-id="1a5af-211">Hiermee haalt u de dag van het onderdeel van de week van X.</span><span class="sxs-lookup"><span data-stu-id="1a5af-211">Gets the day of week component of X.</span></span><br/><br/><span data-ttu-id="1a5af-212">Voorbeeld: `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`.</span><span class="sxs-lookup"><span data-stu-id="1a5af-212">Example: `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`.</span></span> |
| <span data-ttu-id="1a5af-213">Date</span><span class="sxs-lookup"><span data-stu-id="1a5af-213">Date</span></span> |<span data-ttu-id="1a5af-214">DayOfYear(X)</span><span class="sxs-lookup"><span data-stu-id="1a5af-214">DayOfYear(X)</span></span> |<span data-ttu-id="1a5af-215">X: datum/tijd</span><span class="sxs-lookup"><span data-stu-id="1a5af-215">X: DateTime</span></span> |<span data-ttu-id="1a5af-216">Hiermee haalt u de dag van het jaar, uitgedrukt in het jaargedeelte van X.</span><span class="sxs-lookup"><span data-stu-id="1a5af-216">Gets the day in the year represented by the year component of X.</span></span><br/><br/><span data-ttu-id="1a5af-217">Voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="1a5af-217">Examples:</span></span><br/>`12/1/2015: day 335 of 2015`<br/>`12/31/2015: day 365 of 2015`<br/>`12/31/2016: day 366 of 2016 (Leap Year)` |
| <span data-ttu-id="1a5af-218">Date</span><span class="sxs-lookup"><span data-stu-id="1a5af-218">Date</span></span> |<span data-ttu-id="1a5af-219">DaysInMonth(X)</span><span class="sxs-lookup"><span data-stu-id="1a5af-219">DaysInMonth(X)</span></span> |<span data-ttu-id="1a5af-220">X: datum/tijd</span><span class="sxs-lookup"><span data-stu-id="1a5af-220">X: DateTime</span></span> |<span data-ttu-id="1a5af-221">Hiermee haalt u de dagen van de maand dat wordt vertegenwoordigd door het maandgedeelte van de parameter X.</span><span class="sxs-lookup"><span data-stu-id="1a5af-221">Gets the days in the month represented by the month component of parameter X.</span></span><br/><br/><span data-ttu-id="1a5af-222">Voorbeeld: `DaysInMonth of 9/15/2013 are 30 since there are 30 days in the September month`.</span><span class="sxs-lookup"><span data-stu-id="1a5af-222">Example: `DaysInMonth of 9/15/2013 are 30 since there are 30 days in the September month`.</span></span> |
| <span data-ttu-id="1a5af-223">Date</span><span class="sxs-lookup"><span data-stu-id="1a5af-223">Date</span></span> |<span data-ttu-id="1a5af-224">EndOfDay(X)</span><span class="sxs-lookup"><span data-stu-id="1a5af-224">EndOfDay(X)</span></span> |<span data-ttu-id="1a5af-225">X: datum/tijd</span><span class="sxs-lookup"><span data-stu-id="1a5af-225">X: DateTime</span></span> |<span data-ttu-id="1a5af-226">Hiermee haalt u de datum-tijd die het einde van de dag (daggedeelte) van X.</span><span class="sxs-lookup"><span data-stu-id="1a5af-226">Gets the date-time that represents the end of the day (day component) of X.</span></span><br/><br/><span data-ttu-id="1a5af-227">Voorbeeld: `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`.</span><span class="sxs-lookup"><span data-stu-id="1a5af-227">Example: `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`.</span></span> |
| <span data-ttu-id="1a5af-228">Date</span><span class="sxs-lookup"><span data-stu-id="1a5af-228">Date</span></span> |<span data-ttu-id="1a5af-229">EndOfMonth(X)</span><span class="sxs-lookup"><span data-stu-id="1a5af-229">EndOfMonth(X)</span></span> |<span data-ttu-id="1a5af-230">X: datum/tijd</span><span class="sxs-lookup"><span data-stu-id="1a5af-230">X: DateTime</span></span> |<span data-ttu-id="1a5af-231">Het einde van de maand dat wordt vertegenwoordigd door maandgedeelte van de parameter X opgehaald.</span><span class="sxs-lookup"><span data-stu-id="1a5af-231">Gets the end of the month represented by month component of parameter X.</span></span> <br/><br/><span data-ttu-id="1a5af-232">Voorbeeld: `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (datum / tijd die het einde van de maand September vertegenwoordigt)</span><span class="sxs-lookup"><span data-stu-id="1a5af-232">Example: `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (date time that represents the end of September month)</span></span> |
| <span data-ttu-id="1a5af-233">Date</span><span class="sxs-lookup"><span data-stu-id="1a5af-233">Date</span></span> |<span data-ttu-id="1a5af-234">StartOfDay(X)</span><span class="sxs-lookup"><span data-stu-id="1a5af-234">StartOfDay(X)</span></span> |<span data-ttu-id="1a5af-235">X: datum/tijd</span><span class="sxs-lookup"><span data-stu-id="1a5af-235">X: DateTime</span></span> |<span data-ttu-id="1a5af-236">Hiermee haalt u het begin van de dag dat wordt vertegenwoordigd door het daggedeelte van de parameter X.</span><span class="sxs-lookup"><span data-stu-id="1a5af-236">Gets the start of the day represented by the day component of parameter X.</span></span><br/><br/><span data-ttu-id="1a5af-237">Voorbeeld: `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`.</span><span class="sxs-lookup"><span data-stu-id="1a5af-237">Example: `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`.</span></span> |
| <span data-ttu-id="1a5af-238">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="1a5af-238">DateTime</span></span> |<span data-ttu-id="1a5af-239">FROM(X)</span><span class="sxs-lookup"><span data-stu-id="1a5af-239">From(X)</span></span> |<span data-ttu-id="1a5af-240">X: de tekenreeks</span><span class="sxs-lookup"><span data-stu-id="1a5af-240">X: String</span></span> |<span data-ttu-id="1a5af-241">Parseren van tekenreeks X naar een datum-tijd.</span><span class="sxs-lookup"><span data-stu-id="1a5af-241">Parse string X to a date time.</span></span> |
| <span data-ttu-id="1a5af-242">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="1a5af-242">DateTime</span></span> |<span data-ttu-id="1a5af-243">Ticks(X)</span><span class="sxs-lookup"><span data-stu-id="1a5af-243">Ticks(X)</span></span> |<span data-ttu-id="1a5af-244">X: datum/tijd</span><span class="sxs-lookup"><span data-stu-id="1a5af-244">X: DateTime</span></span> |<span data-ttu-id="1a5af-245">Hiermee haalt u de maatstreepjes eigenschap van de parameter X. Eén tik is gelijk aan 100 nanoseconden.</span><span class="sxs-lookup"><span data-stu-id="1a5af-245">Gets the ticks property of the parameter X. One tick equals 100 nanoseconds.</span></span> <span data-ttu-id="1a5af-246">De waarde van deze eigenschap geeft het aantal maatstreepjes dat is verstreken sinds 12:00:00 middernacht, 1 januari 0001.</span><span class="sxs-lookup"><span data-stu-id="1a5af-246">The value of this property represents the number of ticks that have elapsed since 12:00:00 midnight, January 1, 0001.</span></span> |
| <span data-ttu-id="1a5af-247">Tekst</span><span class="sxs-lookup"><span data-stu-id="1a5af-247">Text</span></span> |<span data-ttu-id="1a5af-248">Format(X)</span><span class="sxs-lookup"><span data-stu-id="1a5af-248">Format(X)</span></span> |<span data-ttu-id="1a5af-249">X: tekenreeksvariabele</span><span class="sxs-lookup"><span data-stu-id="1a5af-249">X: String variable</span></span> |<span data-ttu-id="1a5af-250">Hiermee maakt u de tekst (Gebruik `\\'` combinatie escape `'` teken).</span><span class="sxs-lookup"><span data-stu-id="1a5af-250">Formats the text (use `\\'` combination to escape `'` character).</span></span>|

> [!IMPORTANT]
> <span data-ttu-id="1a5af-251">Wanneer u een functie binnen een andere functie, hoeft u niet te gebruiken  **$$**  voorvoegsel voor de interne functie.</span><span class="sxs-lookup"><span data-stu-id="1a5af-251">When using a function within another function, you do not need to use **$$** prefix for the inner function.</span></span> <span data-ttu-id="1a5af-252">Bijvoorbeeld: $$Text.Format ('PartitionKey eq \\' my_pkey_filter_value\\' en RowKey ge \\' {0: jjjj-MM-dd: mm: SS}\\'', Time.AddHours (SliceStart -6)).</span><span class="sxs-lookup"><span data-stu-id="1a5af-252">For example: $$Text.Format('PartitionKey eq \\'my_pkey_filter_value\\' and RowKey ge \\'{0: yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(SliceStart, -6)).</span></span> <span data-ttu-id="1a5af-253">U ziet dat in dit voorbeeld  **$$**  voorvoegsel wordt niet gebruikt voor de **Time.AddHours** functie.</span><span class="sxs-lookup"><span data-stu-id="1a5af-253">In this example, notice that **$$** prefix is not used for the **Time.AddHours** function.</span></span> 

#### <a name="example"></a><span data-ttu-id="1a5af-254">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="1a5af-254">Example</span></span>
<span data-ttu-id="1a5af-255">In het volgende voorbeeld invoer- en parameters voor de Hive-activiteit worden bepaald met behulp van de `Text.Format` functie en SliceStart systeemvariabele.</span><span class="sxs-lookup"><span data-stu-id="1a5af-255">In the following example, input and output parameters for the Hive activity are determined by using the `Text.Format` function and SliceStart system variable.</span></span> 

```json  
{
    "name": "HiveActivitySamplePipeline",
        "properties": {
    "activities": [
            {
            "name": "HiveActivitySample",
            "type": "HDInsightHive",
            "inputs": [
                    {
                    "name": "HiveSampleIn"
                    }
            ],
            "outputs": [
                    {
                    "name": "HiveSampleOut"
                }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "typeproperties": {
                    "scriptPath": "adfwalkthrough\\scripts\\samplehive.hql",
                    "scriptLinkedService": "StorageLinkedService",
                    "defines": {
                        "Input": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
                    },
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                }
            }
            }
    ]
    }
}
```

### <a name="example-2"></a><span data-ttu-id="1a5af-256">Voorbeeld 2</span><span class="sxs-lookup"><span data-stu-id="1a5af-256">Example 2</span></span>

<span data-ttu-id="1a5af-257">In het volgende voorbeeld wordt de datum/tijd-parameter voor de activiteit opgeslagen Procedure met behulp van de tekst bepaald.</span><span class="sxs-lookup"><span data-stu-id="1a5af-257">In the following example, the DateTime parameter for the Stored Procedure Activity is determined by using the Text.</span></span> <span data-ttu-id="1a5af-258">Functie en de variabele SliceStart-indeling.</span><span class="sxs-lookup"><span data-stu-id="1a5af-258">Format function and the SliceStart variable.</span></span> 

```json
{
    "name": "SprocActivitySamplePipeline",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                    }
                },
                "outputs": [
                    {
                        "name": "sprocsampleout"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SprocActivitySample"
            }
        ],
            "start": "2016-08-02T00:00:00Z",
            "end": "2016-08-02T05:00:00Z",
        "isPaused": false
    }
}
```

### <a name="example-3"></a><span data-ttu-id="1a5af-259">Voorbeeld 3</span><span class="sxs-lookup"><span data-stu-id="1a5af-259">Example 3</span></span>
<span data-ttu-id="1a5af-260">Als u wilt gegevens lezen uit de vorige dag in plaats van de dag dat wordt vertegenwoordigd door de SliceStart, gebruikt u de functie AddDays zoals weergegeven in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="1a5af-260">To read data from previous day instead of day represented by the SliceStart, use the AddDays function as shown in the following example:</span></span> 

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-01-01T08:00:00",
        "end": "2017-01-01T11:00:00",
        "description": "hive activity",
        "activities": [
            {
                "name": "SampleHiveActivity",
                "inputs": [
                    {
                        "name": "MyAzureBlobInput",
                        "startTime": "Date.AddDays(SliceStart, -1)",
                        "endTime": "Date.AddDays(SliceEnd, -1)"
                    }
                ],
                "outputs": [
                    {
                        "name": "MyAzureBlobOutput"
                    }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adftutorial\\hivequery.hql",
                    "scriptLinkedService": "StorageLinkedService",
                    "defines": {
                        "Year": "$$Text.Format('{0:yyyy}',WindowsStart)",
                        "Month": "$$Text.Format('{0:MM}',WindowStart)",
                        "Day": "$$Text.Format('{0:dd}',WindowStart)"
                    }
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "OldestFirst",
                    "retry": 2,
                    "timeout": "01:00:00"
                }
            }
        ]
    }
}
```

<span data-ttu-id="1a5af-261">Zie [aangepaste datum en tijd-indeling tekenreeksen](https://msdn.microsoft.com/library/8kb3ddd4.aspx) onderwerp dat beschrijft de verschillende opmaakopties die u kunt gebruiken (bijvoorbeeld: jj versus jjjj).</span><span class="sxs-lookup"><span data-stu-id="1a5af-261">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: yy vs. yyyy).</span></span> 

