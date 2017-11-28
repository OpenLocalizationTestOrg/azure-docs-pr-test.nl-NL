---
title: aaaData Factory functies en systeemvariabelen | Microsoft Docs
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
ms.openlocfilehash: d2936c2821797947bb37d9775226a6c19c4b8ab9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---functions-and-system-variables"></a><span data-ttu-id="1cbf7-103">Azure Data Factory - functies en systeemvariabelen</span><span class="sxs-lookup"><span data-stu-id="1cbf7-103">Azure Data Factory - Functions and System Variables</span></span>
<span data-ttu-id="1cbf7-104">Dit artikel bevat informatie over functies en variabelen die worden ondersteund door Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-104">This article provides information about functions and variables supported by Azure Data Factory.</span></span>

## <a name="data-factory-system-variables"></a><span data-ttu-id="1cbf7-105">Data Factory-systeemvariabelen</span><span class="sxs-lookup"><span data-stu-id="1cbf7-105">Data Factory system variables</span></span>
| <span data-ttu-id="1cbf7-106">Naam variabele</span><span class="sxs-lookup"><span data-stu-id="1cbf7-106">Variable Name</span></span> | <span data-ttu-id="1cbf7-107">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="1cbf7-107">Description</span></span> | <span data-ttu-id="1cbf7-108">Bereik van het object</span><span class="sxs-lookup"><span data-stu-id="1cbf7-108">Object Scope</span></span> | <span data-ttu-id="1cbf7-109">JSON-bereik en gebruiksvoorbeelden</span><span class="sxs-lookup"><span data-stu-id="1cbf7-109">JSON Scope and Use Cases</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1cbf7-110">WindowStart</span><span class="sxs-lookup"><span data-stu-id="1cbf7-110">WindowStart</span></span> |<span data-ttu-id="1cbf7-111">Begin van het tijdsinterval voor de huidige activiteit venster uitvoeren</span><span class="sxs-lookup"><span data-stu-id="1cbf7-111">Start of time interval for current activity run window</span></span> |<span data-ttu-id="1cbf7-112">Activiteit</span><span class="sxs-lookup"><span data-stu-id="1cbf7-112">activity</span></span> |<ol><li><span data-ttu-id="1cbf7-113">Geef op query's voor selectie.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-113">Specify data selection queries.</span></span> <span data-ttu-id="1cbf7-114">Zie connector artikelen waarnaar wordt verwezen in Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-114">See connector articles referenced in hello [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span></li> |
| <span data-ttu-id="1cbf7-115">WindowEnd</span><span class="sxs-lookup"><span data-stu-id="1cbf7-115">WindowEnd</span></span> |<span data-ttu-id="1cbf7-116">Einde van het tijdsinterval voor de huidige activiteit venster uitvoeren</span><span class="sxs-lookup"><span data-stu-id="1cbf7-116">End of time interval for current activity run window</span></span> |<span data-ttu-id="1cbf7-117">Activiteit</span><span class="sxs-lookup"><span data-stu-id="1cbf7-117">activity</span></span> |<span data-ttu-id="1cbf7-118">hetzelfde als WindowStart.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-118">same as WindowStart.</span></span> |
| <span data-ttu-id="1cbf7-119">SliceStart</span><span class="sxs-lookup"><span data-stu-id="1cbf7-119">SliceStart</span></span> |<span data-ttu-id="1cbf7-120">Begin van het tijdsinterval voor het segment wordt geproduceerd</span><span class="sxs-lookup"><span data-stu-id="1cbf7-120">Start of time interval for data  slice being produced</span></span> |<span data-ttu-id="1cbf7-121">Activiteit</span><span class="sxs-lookup"><span data-stu-id="1cbf7-121">activity</span></span><br/><span data-ttu-id="1cbf7-122">Gegevensset</span><span class="sxs-lookup"><span data-stu-id="1cbf7-122">dataset</span></span> |<ol><li><span data-ttu-id="1cbf7-123">Geef dynamische paden en bestandsnamen tijdens het werken met [Azure Blob](data-factory-azure-blob-connector.md) en [bestandssysteem gegevenssets](data-factory-onprem-file-system-connector.md).</span><span class="sxs-lookup"><span data-stu-id="1cbf7-123">Specify dynamic folder paths and file names while working with [Azure Blob](data-factory-azure-blob-connector.md) and [File System datasets](data-factory-onprem-file-system-connector.md).</span></span></li><li><span data-ttu-id="1cbf7-124">Invoer afhankelijkheden data factory-functies in activiteit invoer verzameling opgeven.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-124">Specify input dependencies with data factory functions in activity inputs collection.</span></span></li></ol> |
| <span data-ttu-id="1cbf7-125">SliceEnd</span><span class="sxs-lookup"><span data-stu-id="1cbf7-125">SliceEnd</span></span> |<span data-ttu-id="1cbf7-126">Einde van de tijdsinterval voor het huidige segment.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-126">End of time interval for current data slice.</span></span> |<span data-ttu-id="1cbf7-127">Activiteit</span><span class="sxs-lookup"><span data-stu-id="1cbf7-127">activity</span></span><br/><span data-ttu-id="1cbf7-128">Gegevensset</span><span class="sxs-lookup"><span data-stu-id="1cbf7-128">dataset</span></span> |<span data-ttu-id="1cbf7-129">hetzelfde als SliceStart.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-129">same as SliceStart.</span></span> |

> [!NOTE]
> <span data-ttu-id="1cbf7-130">Op dit moment gegevensfactory vereist dat Hallo plannen opgegeven in de Hallo Hallo schema is opgegeven in de beschikbaarheid van de uitvoergegevensset Hallo exact overeenkomt met de activiteit.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-130">Currently data factory requires that hello schedule specified in hello activity exactly matches hello schedule specified in availability of hello output dataset.</span></span> <span data-ttu-id="1cbf7-131">Daarom WindowStart, WindowEnd, en SliceStart en SliceEnd worden altijd toegewezen toohello dezelfde periode en een segment één uitvoer time.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-131">Therefore, WindowStart, WindowEnd, and SliceStart and SliceEnd always map toohello same time period and a single output slice.</span></span>
> 

### <a name="example-for-using-a-system-variable"></a><span data-ttu-id="1cbf7-132">Voorbeeld voor het gebruik van een systeemvariabele</span><span class="sxs-lookup"><span data-stu-id="1cbf7-132">Example for using a system variable</span></span>
<span data-ttu-id="1cbf7-133">In het volgende voorbeeld, jaar, maand, dag en tijd van Hallo **SliceStart** worden uitgepakt in verschillende variabelen die worden gebruikt door **folderPath** en **fileName** eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-133">In hello following example, year, month, day, and time of **SliceStart** are extracted into separate variables that are used by **folderPath** and **fileName** properties.</span></span>

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

## <a name="data-factory-functions"></a><span data-ttu-id="1cbf7-134">Data Factory-functies</span><span class="sxs-lookup"><span data-stu-id="1cbf7-134">Data Factory functions</span></span>
<span data-ttu-id="1cbf7-135">U kunt functies gebruiken in gegevensfactory samen met systeemvariabelen voor Hallo volgende doeleinden:</span><span class="sxs-lookup"><span data-stu-id="1cbf7-135">You can use functions in data factory along with system variables for hello following purposes:</span></span>

1. <span data-ttu-id="1cbf7-136">Query's voor selectie opgeven (Zie connector artikelen waarnaar wordt verwezen door Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-136">Specifying data selection queries (see connector articles referenced by hello [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span>
   
   <span data-ttu-id="1cbf7-137">Hallo syntaxis tooinvoke een data factory-functie is:  **$$ <function>**  voor selectie van query's en andere eigenschappen in het Hallo-activiteit en gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-137">hello syntax tooinvoke a data factory function is: **$$<function>** for data selection queries and other properties in hello activity and datasets.</span></span>  
2. <span data-ttu-id="1cbf7-138">Invoer afhankelijkheden opgeven data factory-functies in activiteit invoer verzameling.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-138">Specifying input dependencies with data factory functions in activity inputs collection.</span></span>
   
    <span data-ttu-id="1cbf7-139">$$ is niet nodig voor het opgeven van invoer afhankelijkheid expressies.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-139">$$ is not needed for specifying input dependency expressions.</span></span>     

<span data-ttu-id="1cbf7-140">In het volgende voorbeeld Hallo **sqlReaderQuery** eigenschap in een JSON-bestand is toegewezen tooa-waarde geretourneerd door Hallo `Text.Format` functie.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-140">In hello following sample, **sqlReaderQuery** property in a JSON file is assigned tooa value returned by hello `Text.Format` function.</span></span> <span data-ttu-id="1cbf7-141">Dit voorbeeld gebruikt ook een systeemvariabele met de naam **WindowStart**, die staat voor Hallo-begintijd van Hallo-activiteit venster uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-141">This sample also uses a system variable named **WindowStart**, which represents hello start time of hello activity run window.</span></span>

```json
{
    "Type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('SELECT * FROM MyTable WHERE StartTime = \\'{0:yyyyMMdd-HH}\\'', WindowStart)"
}
```

<span data-ttu-id="1cbf7-142">Zie [aangepaste datum en tijd-indeling tekenreeksen](https://msdn.microsoft.com/library/8kb3ddd4.aspx) onderwerp dat beschrijft de verschillende opmaakopties die u kunt gebruiken (bijvoorbeeld: ay versus jjjj).</span><span class="sxs-lookup"><span data-stu-id="1cbf7-142">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: ay vs. yyyy).</span></span> 

### <a name="functions"></a><span data-ttu-id="1cbf7-143">Functies</span><span class="sxs-lookup"><span data-stu-id="1cbf7-143">Functions</span></span>
<span data-ttu-id="1cbf7-144">Hallo tabellen na een overzicht van alle Hallo-functies in Azure Data Factory:</span><span class="sxs-lookup"><span data-stu-id="1cbf7-144">hello following tables list all hello functions in Azure Data Factory:</span></span>

| <span data-ttu-id="1cbf7-145">Category</span><span class="sxs-lookup"><span data-stu-id="1cbf7-145">Category</span></span> | <span data-ttu-id="1cbf7-146">Functie</span><span class="sxs-lookup"><span data-stu-id="1cbf7-146">Function</span></span> | <span data-ttu-id="1cbf7-147">Parameters</span><span class="sxs-lookup"><span data-stu-id="1cbf7-147">Parameters</span></span> | <span data-ttu-id="1cbf7-148">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="1cbf7-148">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1cbf7-149">Time</span><span class="sxs-lookup"><span data-stu-id="1cbf7-149">Time</span></span> |<span data-ttu-id="1cbf7-150">AddHours(X,Y)</span><span class="sxs-lookup"><span data-stu-id="1cbf7-150">AddHours(X,Y)</span></span> |<span data-ttu-id="1cbf7-151">X: datum/tijd</span><span class="sxs-lookup"><span data-stu-id="1cbf7-151">X: DateTime</span></span> <br/><br/><span data-ttu-id="1cbf7-152">Y: int</span><span class="sxs-lookup"><span data-stu-id="1cbf7-152">Y: int</span></span> |<span data-ttu-id="1cbf7-153">Voegt Y uren toohello gelegenheid X.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-153">Adds Y hours toohello given time X.</span></span> <br/><br/><span data-ttu-id="1cbf7-154">Voorbeeld:`9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="1cbf7-154">Example: `9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM`</span></span> |
| <span data-ttu-id="1cbf7-155">Time</span><span class="sxs-lookup"><span data-stu-id="1cbf7-155">Time</span></span> |<span data-ttu-id="1cbf7-156">AddMinutes(X,Y)</span><span class="sxs-lookup"><span data-stu-id="1cbf7-156">AddMinutes(X,Y)</span></span> |<span data-ttu-id="1cbf7-157">X: datum/tijd</span><span class="sxs-lookup"><span data-stu-id="1cbf7-157">X: DateTime</span></span> <br/><br/><span data-ttu-id="1cbf7-158">Y: int</span><span class="sxs-lookup"><span data-stu-id="1cbf7-158">Y: int</span></span> |<span data-ttu-id="1cbf7-159">Y minuten tooX toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-159">Adds Y minutes tooX.</span></span><br/><br/><span data-ttu-id="1cbf7-160">Voorbeeld:`9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM`</span><span class="sxs-lookup"><span data-stu-id="1cbf7-160">Example: `9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM`</span></span> |
| <span data-ttu-id="1cbf7-161">Time</span><span class="sxs-lookup"><span data-stu-id="1cbf7-161">Time</span></span> |<span data-ttu-id="1cbf7-162">StartOfHour(X)</span><span class="sxs-lookup"><span data-stu-id="1cbf7-162">StartOfHour(X)</span></span> |<span data-ttu-id="1cbf7-163">X: datum/tijd</span><span class="sxs-lookup"><span data-stu-id="1cbf7-163">X: Datetime</span></span> |<span data-ttu-id="1cbf7-164">Opgehaald Hallo begintijd voor Hallo uur dat wordt vertegenwoordigd door Hallo uurgedeelte van X.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-164">Gets hello starting time for hello hour represented by hello hour component of X.</span></span> <br/><br/><span data-ttu-id="1cbf7-165">Voorbeeld:`StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="1cbf7-165">Example: `StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM`</span></span> |
| <span data-ttu-id="1cbf7-166">Date</span><span class="sxs-lookup"><span data-stu-id="1cbf7-166">Date</span></span> |<span data-ttu-id="1cbf7-167">AddDays(X,Y)</span><span class="sxs-lookup"><span data-stu-id="1cbf7-167">AddDays(X,Y)</span></span> |<span data-ttu-id="1cbf7-168">X: datum/tijd</span><span class="sxs-lookup"><span data-stu-id="1cbf7-168">X: DateTime</span></span><br/><br/><span data-ttu-id="1cbf7-169">Y: int</span><span class="sxs-lookup"><span data-stu-id="1cbf7-169">Y: int</span></span> |<span data-ttu-id="1cbf7-170">Y dagen tooX toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-170">Adds Y days tooX.</span></span> <br/><br/><span data-ttu-id="1cbf7-171">Voorbeeld: 9, 15/2013 12:00:00 PM + 2 dagen = 9/17/2013 12:00:00 PM.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-171">Example: 9/15/2013 12:00:00 PM + 2 days = 9/17/2013 12:00:00 PM.</span></span><br/><br/><span data-ttu-id="1cbf7-172">U kunt dagen te aftrekken door te geven Y als een negatief getal.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-172">You can subtract days too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="1cbf7-173">Voorbeeld: `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-173">Example: `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`.</span></span> |
| <span data-ttu-id="1cbf7-174">Date</span><span class="sxs-lookup"><span data-stu-id="1cbf7-174">Date</span></span> |<span data-ttu-id="1cbf7-175">AddMonths(X,Y)</span><span class="sxs-lookup"><span data-stu-id="1cbf7-175">AddMonths(X,Y)</span></span> |<span data-ttu-id="1cbf7-176">X: datum/tijd</span><span class="sxs-lookup"><span data-stu-id="1cbf7-176">X: DateTime</span></span><br/><br/><span data-ttu-id="1cbf7-177">Y: int</span><span class="sxs-lookup"><span data-stu-id="1cbf7-177">Y: int</span></span> |<span data-ttu-id="1cbf7-178">Y maanden tooX toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-178">Adds Y months tooX.</span></span><br/><br/><span data-ttu-id="1cbf7-179">`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-179">`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.</span></span><br/><br/><span data-ttu-id="1cbf7-180">U kunt maanden te aftrekken door te geven Y als een negatief getal.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-180">You can subtract months too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="1cbf7-181">Voorbeeld: `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-181">Example: `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.</span></span>|
| <span data-ttu-id="1cbf7-182">Date</span><span class="sxs-lookup"><span data-stu-id="1cbf7-182">Date</span></span> |<span data-ttu-id="1cbf7-183">AddQuarters(X,Y)</span><span class="sxs-lookup"><span data-stu-id="1cbf7-183">AddQuarters(X,Y)</span></span> |<span data-ttu-id="1cbf7-184">X: datum/tijd</span><span class="sxs-lookup"><span data-stu-id="1cbf7-184">X: DateTime</span></span> <br/><br/><span data-ttu-id="1cbf7-185">Y: int</span><span class="sxs-lookup"><span data-stu-id="1cbf7-185">Y: int</span></span> |<span data-ttu-id="1cbf7-186">Voegt Y * tooX 3 maanden.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-186">Adds Y * 3 months tooX.</span></span><br/><br/><span data-ttu-id="1cbf7-187">Voorbeeld:`9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="1cbf7-187">Example: `9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM`</span></span> |
| <span data-ttu-id="1cbf7-188">Date</span><span class="sxs-lookup"><span data-stu-id="1cbf7-188">Date</span></span> |<span data-ttu-id="1cbf7-189">AddWeeks(X,Y)</span><span class="sxs-lookup"><span data-stu-id="1cbf7-189">AddWeeks(X,Y)</span></span> |<span data-ttu-id="1cbf7-190">X: datum/tijd</span><span class="sxs-lookup"><span data-stu-id="1cbf7-190">X: DateTime</span></span><br/><br/><span data-ttu-id="1cbf7-191">Y: int</span><span class="sxs-lookup"><span data-stu-id="1cbf7-191">Y: int</span></span> |<span data-ttu-id="1cbf7-192">Voegt Y * tooX 7 dagen</span><span class="sxs-lookup"><span data-stu-id="1cbf7-192">Adds Y * 7 days tooX</span></span><br/><br/><span data-ttu-id="1cbf7-193">Voorbeeld: 9, 15/2013 12:00:00 PM + 1 week = 9/22/2013 12:00:00 uur</span><span class="sxs-lookup"><span data-stu-id="1cbf7-193">Example: 9/15/2013 12:00:00 PM + 1 week = 9/22/2013 12:00:00 PM</span></span><br/><br/><span data-ttu-id="1cbf7-194">U kunt de weken te aftrekken door te geven Y als een negatief getal.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-194">You can subtract weeks too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="1cbf7-195">Voorbeeld: `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-195">Example: `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`.</span></span> |
| <span data-ttu-id="1cbf7-196">Date</span><span class="sxs-lookup"><span data-stu-id="1cbf7-196">Date</span></span> |<span data-ttu-id="1cbf7-197">AddYears(X,Y)</span><span class="sxs-lookup"><span data-stu-id="1cbf7-197">AddYears(X,Y)</span></span> |<span data-ttu-id="1cbf7-198">X: datum/tijd</span><span class="sxs-lookup"><span data-stu-id="1cbf7-198">X: DateTime</span></span><br/><br/><span data-ttu-id="1cbf7-199">Y: int</span><span class="sxs-lookup"><span data-stu-id="1cbf7-199">Y: int</span></span> |<span data-ttu-id="1cbf7-200">Y jaar tooX toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-200">Adds Y years tooX.</span></span><br/><br/>`Example: 9/15/2013 12:00:00 PM + 1 year = 9/15/2014 12:00:00 PM`<br/><br/><span data-ttu-id="1cbf7-201">U kunt jaar te aftrekken door te geven Y als een negatief getal.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-201">You can subtract years too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="1cbf7-202">Voorbeeld: `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-202">Example: `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`.</span></span> |
| <span data-ttu-id="1cbf7-203">Date</span><span class="sxs-lookup"><span data-stu-id="1cbf7-203">Date</span></span> |<span data-ttu-id="1cbf7-204">Day(X)</span><span class="sxs-lookup"><span data-stu-id="1cbf7-204">Day(X)</span></span> |<span data-ttu-id="1cbf7-205">X: datum/tijd</span><span class="sxs-lookup"><span data-stu-id="1cbf7-205">X: DateTime</span></span> |<span data-ttu-id="1cbf7-206">Hiermee haalt u Hallo daggedeelte van X.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-206">Gets hello day component of X.</span></span><br/><br/><span data-ttu-id="1cbf7-207">Voorbeeld: `Day of 9/15/2013 12:00:00 PM is 9`.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-207">Example: `Day of 9/15/2013 12:00:00 PM is 9`.</span></span> |
| <span data-ttu-id="1cbf7-208">Date</span><span class="sxs-lookup"><span data-stu-id="1cbf7-208">Date</span></span> |<span data-ttu-id="1cbf7-209">DayOfWeek(X)</span><span class="sxs-lookup"><span data-stu-id="1cbf7-209">DayOfWeek(X)</span></span> |<span data-ttu-id="1cbf7-210">X: datum/tijd</span><span class="sxs-lookup"><span data-stu-id="1cbf7-210">X: DateTime</span></span> |<span data-ttu-id="1cbf7-211">Hiermee haalt u Hallo dag van het onderdeel van de week van X.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-211">Gets hello day of week component of X.</span></span><br/><br/><span data-ttu-id="1cbf7-212">Voorbeeld: `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-212">Example: `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`.</span></span> |
| <span data-ttu-id="1cbf7-213">Date</span><span class="sxs-lookup"><span data-stu-id="1cbf7-213">Date</span></span> |<span data-ttu-id="1cbf7-214">DayOfYear(X)</span><span class="sxs-lookup"><span data-stu-id="1cbf7-214">DayOfYear(X)</span></span> |<span data-ttu-id="1cbf7-215">X: datum/tijd</span><span class="sxs-lookup"><span data-stu-id="1cbf7-215">X: DateTime</span></span> |<span data-ttu-id="1cbf7-216">Hiermee haalt u Hallo dag in Hallo jaar, uitgedrukt in Hallo jaargedeelte van X.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-216">Gets hello day in hello year represented by hello year component of X.</span></span><br/><br/><span data-ttu-id="1cbf7-217">Voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="1cbf7-217">Examples:</span></span><br/>`12/1/2015: day 335 of 2015`<br/>`12/31/2015: day 365 of 2015`<br/>`12/31/2016: day 366 of 2016 (Leap Year)` |
| <span data-ttu-id="1cbf7-218">Date</span><span class="sxs-lookup"><span data-stu-id="1cbf7-218">Date</span></span> |<span data-ttu-id="1cbf7-219">DaysInMonth(X)</span><span class="sxs-lookup"><span data-stu-id="1cbf7-219">DaysInMonth(X)</span></span> |<span data-ttu-id="1cbf7-220">X: datum/tijd</span><span class="sxs-lookup"><span data-stu-id="1cbf7-220">X: DateTime</span></span> |<span data-ttu-id="1cbf7-221">Hallo dagen in Hallo maand dat wordt vertegenwoordigd door Hallo maandgedeelte van de parameter X opgehaald.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-221">Gets hello days in hello month represented by hello month component of parameter X.</span></span><br/><br/><span data-ttu-id="1cbf7-222">Voorbeeld: `DaysInMonth of 9/15/2013 are 30 since there are 30 days in hello September month`.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-222">Example: `DaysInMonth of 9/15/2013 are 30 since there are 30 days in hello September month`.</span></span> |
| <span data-ttu-id="1cbf7-223">Date</span><span class="sxs-lookup"><span data-stu-id="1cbf7-223">Date</span></span> |<span data-ttu-id="1cbf7-224">EndOfDay(X)</span><span class="sxs-lookup"><span data-stu-id="1cbf7-224">EndOfDay(X)</span></span> |<span data-ttu-id="1cbf7-225">X: datum/tijd</span><span class="sxs-lookup"><span data-stu-id="1cbf7-225">X: DateTime</span></span> |<span data-ttu-id="1cbf7-226">Hiermee haalt u Hallo datum-tijd die Hallo-einde van Hallo dag (daggedeelte) van X aangeeft.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-226">Gets hello date-time that represents hello end of hello day (day component) of X.</span></span><br/><br/><span data-ttu-id="1cbf7-227">Voorbeeld: `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-227">Example: `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`.</span></span> |
| <span data-ttu-id="1cbf7-228">Date</span><span class="sxs-lookup"><span data-stu-id="1cbf7-228">Date</span></span> |<span data-ttu-id="1cbf7-229">EndOfMonth(X)</span><span class="sxs-lookup"><span data-stu-id="1cbf7-229">EndOfMonth(X)</span></span> |<span data-ttu-id="1cbf7-230">X: datum/tijd</span><span class="sxs-lookup"><span data-stu-id="1cbf7-230">X: DateTime</span></span> |<span data-ttu-id="1cbf7-231">Hallo-einde van Hallo maand dat wordt vertegenwoordigd door maandgedeelte van de parameter X opgehaald.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-231">Gets hello end of hello month represented by month component of parameter X.</span></span> <br/><br/><span data-ttu-id="1cbf7-232">Voorbeeld: `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (datum / tijd die Hallo einde van September maand vertegenwoordigt)</span><span class="sxs-lookup"><span data-stu-id="1cbf7-232">Example: `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (date time that represents hello end of September month)</span></span> |
| <span data-ttu-id="1cbf7-233">Date</span><span class="sxs-lookup"><span data-stu-id="1cbf7-233">Date</span></span> |<span data-ttu-id="1cbf7-234">StartOfDay(X)</span><span class="sxs-lookup"><span data-stu-id="1cbf7-234">StartOfDay(X)</span></span> |<span data-ttu-id="1cbf7-235">X: datum/tijd</span><span class="sxs-lookup"><span data-stu-id="1cbf7-235">X: DateTime</span></span> |<span data-ttu-id="1cbf7-236">Hiermee haalt u Hallo Hallo dag dat wordt vertegenwoordigd door Hallo daggedeelte van de parameter X is gestart.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-236">Gets hello start of hello day represented by hello day component of parameter X.</span></span><br/><br/><span data-ttu-id="1cbf7-237">Voorbeeld: `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-237">Example: `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`.</span></span> |
| <span data-ttu-id="1cbf7-238">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="1cbf7-238">DateTime</span></span> |<span data-ttu-id="1cbf7-239">FROM(X)</span><span class="sxs-lookup"><span data-stu-id="1cbf7-239">From(X)</span></span> |<span data-ttu-id="1cbf7-240">X: de tekenreeks</span><span class="sxs-lookup"><span data-stu-id="1cbf7-240">X: String</span></span> |<span data-ttu-id="1cbf7-241">Parseren van tekenreeks X tooa datum / tijd.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-241">Parse string X tooa date time.</span></span> |
| <span data-ttu-id="1cbf7-242">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="1cbf7-242">DateTime</span></span> |<span data-ttu-id="1cbf7-243">Ticks(X)</span><span class="sxs-lookup"><span data-stu-id="1cbf7-243">Ticks(X)</span></span> |<span data-ttu-id="1cbf7-244">X: datum/tijd</span><span class="sxs-lookup"><span data-stu-id="1cbf7-244">X: DateTime</span></span> |<span data-ttu-id="1cbf7-245">Hallo ticks eigenschap van de parameter Hallo X opgehaald. Eén tik is gelijk aan 100 nanoseconden.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-245">Gets hello ticks property of hello parameter X. One tick equals 100 nanoseconds.</span></span> <span data-ttu-id="1cbf7-246">Hallo-waarde van deze eigenschap vertegenwoordigt Hallo aantal maatstreepjes dat is verstreken sinds 12:00:00 middernacht, 1 januari 0001.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-246">hello value of this property represents hello number of ticks that have elapsed since 12:00:00 midnight, January 1, 0001.</span></span> |
| <span data-ttu-id="1cbf7-247">Tekst</span><span class="sxs-lookup"><span data-stu-id="1cbf7-247">Text</span></span> |<span data-ttu-id="1cbf7-248">Format(X)</span><span class="sxs-lookup"><span data-stu-id="1cbf7-248">Format(X)</span></span> |<span data-ttu-id="1cbf7-249">X: tekenreeksvariabele</span><span class="sxs-lookup"><span data-stu-id="1cbf7-249">X: String variable</span></span> |<span data-ttu-id="1cbf7-250">Indelingen tekst hello (Gebruik `\\'` combinatie tooescape `'` teken).</span><span class="sxs-lookup"><span data-stu-id="1cbf7-250">Formats hello text (use `\\'` combination tooescape `'` character).</span></span>|

> [!IMPORTANT]
> <span data-ttu-id="1cbf7-251">Wanneer u een functie binnen een andere functie, hoeft u niet toouse  **$$**  voorvoegsel voor de interne Hallo-functie.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-251">When using a function within another function, you do not need toouse **$$** prefix for hello inner function.</span></span> <span data-ttu-id="1cbf7-252">Bijvoorbeeld: $$Text.Format ('PartitionKey eq \\' my_pkey_filter_value\\' en RowKey ge \\' {0: jjjj-MM-dd: mm: SS}\\'', Time.AddHours (SliceStart -6)).</span><span class="sxs-lookup"><span data-stu-id="1cbf7-252">For example: $$Text.Format('PartitionKey eq \\'my_pkey_filter_value\\' and RowKey ge \\'{0: yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(SliceStart, -6)).</span></span> <span data-ttu-id="1cbf7-253">U ziet dat in dit voorbeeld  **$$**  voorvoegsel wordt niet gebruikt voor Hallo **Time.AddHours** functie.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-253">In this example, notice that **$$** prefix is not used for hello **Time.AddHours** function.</span></span> 

#### <a name="example"></a><span data-ttu-id="1cbf7-254">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="1cbf7-254">Example</span></span>
<span data-ttu-id="1cbf7-255">In Hallo volgende bijvoorbeeld invoer en uitvoer parameters voor Hallo Hive-activiteit worden bepaald met behulp van Hallo `Text.Format` functie en SliceStart systeemvariabele.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-255">In hello following example, input and output parameters for hello Hive activity are determined by using hello `Text.Format` function and SliceStart system variable.</span></span> 

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

### <a name="example-2"></a><span data-ttu-id="1cbf7-256">Voorbeeld 2</span><span class="sxs-lookup"><span data-stu-id="1cbf7-256">Example 2</span></span>

<span data-ttu-id="1cbf7-257">Hallo in Hallo voorbeeld te volgen, DateTime-parameter voor de activiteit opgeslagen Procedure is bepaald met behulp van de tekst hello Hallo.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-257">In hello following example, hello DateTime parameter for hello Stored Procedure Activity is determined by using hello Text.</span></span> <span data-ttu-id="1cbf7-258">Functie formatteren en Hallo SliceStart-variabele.</span><span class="sxs-lookup"><span data-stu-id="1cbf7-258">Format function and hello SliceStart variable.</span></span> 

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

### <a name="example-3"></a><span data-ttu-id="1cbf7-259">Voorbeeld 3</span><span class="sxs-lookup"><span data-stu-id="1cbf7-259">Example 3</span></span>
<span data-ttu-id="1cbf7-260">tooread gegevens uit de vorige dag in plaats van de dag dat wordt vertegenwoordigd door Hallo SliceStart, gebruik de functie AddDays Hallo zoals getoond in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="1cbf7-260">tooread data from previous day instead of day represented by hello SliceStart, use hello AddDays function as shown in hello following example:</span></span> 

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

<span data-ttu-id="1cbf7-261">Zie [aangepaste datum en tijd-indeling tekenreeksen](https://msdn.microsoft.com/library/8kb3ddd4.aspx) onderwerp dat beschrijft de verschillende opmaakopties die u kunt gebruiken (bijvoorbeeld: jj versus jjjj).</span><span class="sxs-lookup"><span data-stu-id="1cbf7-261">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: yy vs. yyyy).</span></span> 

