---
title: aaaAzure Data Factory - naslaginformatie voor JSON-scriptverwerking | Microsoft Docs
description: JSON-schema's biedt voor Data Factory-entiteiten.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 813fd752bb0ecb1b513d022b9f302325105dac31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---json-scripting-reference"></a><span data-ttu-id="34b16-103">Azure Data Factory - JSON-scriptverwerking verwijzing</span><span class="sxs-lookup"><span data-stu-id="34b16-103">Azure Data Factory - JSON Scripting Reference</span></span>
<span data-ttu-id="34b16-104">Dit artikel bevat JSON-schema's en voorbeelden voor het definiëren van Azure Data Factory-entiteiten (pipeline, activiteit, gegevensset en gekoppelde service).</span><span class="sxs-lookup"><span data-stu-id="34b16-104">This article provides JSON schemas and examples for defining Azure Data Factory entities (pipeline, activity, dataset, and linked service).</span></span>  

## <a name="pipeline"></a><span data-ttu-id="34b16-105">Pijplijn</span><span class="sxs-lookup"><span data-stu-id="34b16-105">Pipeline</span></span> 
<span data-ttu-id="34b16-106">Hallo op hoog niveau structuur voor de definitie van een pijplijn is als volgt:</span><span class="sxs-lookup"><span data-stu-id="34b16-106">hello high-level structure for a pipeline definition is as follows:</span></span> 

```json
{
  "name": "SamplePipeline",
  "properties": {
    "description": "Describe what pipeline does",
    "activities": [
    ],
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

<span data-ttu-id="34b16-107">Volgende tabel beschrijft de eigenschappen Hallo binnen Hallo pijplijn JSON-definitie:</span><span class="sxs-lookup"><span data-stu-id="34b16-107">Following table describes hello properties within hello pipeline JSON definition:</span></span>

| <span data-ttu-id="34b16-108">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-108">Property</span></span> | <span data-ttu-id="34b16-109">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-109">Description</span></span> | <span data-ttu-id="34b16-110">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-110">Required</span></span>
-------- | ----------- | --------
| <span data-ttu-id="34b16-111">naam</span><span class="sxs-lookup"><span data-stu-id="34b16-111">name</span></span> | <span data-ttu-id="34b16-112">Naam van het Hallo-pijplijn.</span><span class="sxs-lookup"><span data-stu-id="34b16-112">Name of hello pipeline.</span></span> <span data-ttu-id="34b16-113">Geef een naam die Hallo-actie die Hallo activiteit vertegenwoordigt of pijplijn geconfigureerde toodo is</span><span class="sxs-lookup"><span data-stu-id="34b16-113">Specify a name that represents hello action that hello activity or pipeline is configured toodo</span></span><br/><ul><li><span data-ttu-id="34b16-114">Maximum aantal tekens: 260</span><span class="sxs-lookup"><span data-stu-id="34b16-114">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="34b16-115">Moet beginnen met een letter, cijfer of onderstrepingsteken (_)</span><span class="sxs-lookup"><span data-stu-id="34b16-115">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="34b16-116">Volgende tekens zijn niet toegestaan: '. ', '+ ','?', '/', '< ',' >', ' * ', "%", "&", ":","\\'</span><span class="sxs-lookup"><span data-stu-id="34b16-116">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="34b16-117">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-117">Yes</span></span> |
| <span data-ttu-id="34b16-118">description</span><span class="sxs-lookup"><span data-stu-id="34b16-118">description</span></span> |<span data-ttu-id="34b16-119">Beschrijving van wat Hallo activiteit of pijplijn wordt gebruikt voor</span><span class="sxs-lookup"><span data-stu-id="34b16-119">Text describing what hello activity or pipeline is used for</span></span> | <span data-ttu-id="34b16-120">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-120">No</span></span> |
| <span data-ttu-id="34b16-121">activities</span><span class="sxs-lookup"><span data-stu-id="34b16-121">activities</span></span> | <span data-ttu-id="34b16-122">Bevat een lijst van activiteiten.</span><span class="sxs-lookup"><span data-stu-id="34b16-122">Contains a list of activities.</span></span> | <span data-ttu-id="34b16-123">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-123">Yes</span></span> |
| <span data-ttu-id="34b16-124">start</span><span class="sxs-lookup"><span data-stu-id="34b16-124">start</span></span> |<span data-ttu-id="34b16-125">Datum-begintijd voor de Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="34b16-125">Start date-time for hello pipeline.</span></span> <span data-ttu-id="34b16-126">Moet in [ISO-indeling](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="34b16-126">Must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="34b16-127">Bijvoorbeeld: 2014-10-14T16:32:41.</span><span class="sxs-lookup"><span data-stu-id="34b16-127">For example: 2014-10-14T16:32:41.</span></span> <br/><br/><span data-ttu-id="34b16-128">Het is mogelijk toospecify een plaatselijke tijd, bijvoorbeeld een geschatte tijd.</span><span class="sxs-lookup"><span data-stu-id="34b16-128">It is possible toospecify a local time, for example an EST time.</span></span> <span data-ttu-id="34b16-129">Hier volgt een voorbeeld: `2016-02-27T06:00:00**-05:00`, namelijk 6 AM EST.</span><span class="sxs-lookup"><span data-stu-id="34b16-129">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="34b16-130">Hallo begin- en eigenschappen samen actieve periode opgeven voor Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="34b16-130">hello start and end properties together specify active period for hello pipeline.</span></span> <span data-ttu-id="34b16-131">Uitvoer segmenten worden alleen gemaakt met deze actieve periode.</span><span class="sxs-lookup"><span data-stu-id="34b16-131">Output slices are only produced with in this active period.</span></span> |<span data-ttu-id="34b16-132">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-132">No</span></span><br/><br/><span data-ttu-id="34b16-133">Als u een waarde voor Hallo end-eigenschap opgeeft, moet u de waarde voor Hallo begineigenschap opgeven.</span><span class="sxs-lookup"><span data-stu-id="34b16-133">If you specify a value for hello end property, you must specify value for hello start property.</span></span><br/><br/><span data-ttu-id="34b16-134">Hallo kunnen begin- en eindtijden niet leeg toocreate een pijplijn.</span><span class="sxs-lookup"><span data-stu-id="34b16-134">hello start and end times can both be empty toocreate a pipeline.</span></span> <span data-ttu-id="34b16-135">U moet beide waarden opgeven tooset een actieve periode voor Hallo pijplijn toorun.</span><span class="sxs-lookup"><span data-stu-id="34b16-135">You must specify both values tooset an active period for hello pipeline toorun.</span></span> <span data-ttu-id="34b16-136">Als u geen begin- en eindtijden opgeeft wanneer u een pijplijn maakt, kunt u deze instellen met behulp van de cmdlet Set-AzureRmDataFactoryPipelineActivePeriod hello later.</span><span class="sxs-lookup"><span data-stu-id="34b16-136">If you do not specify start and end times when creating a pipeline, you can set them using hello Set-AzureRmDataFactoryPipelineActivePeriod cmdlet later.</span></span> |
| <span data-ttu-id="34b16-137">Einde</span><span class="sxs-lookup"><span data-stu-id="34b16-137">end</span></span> |<span data-ttu-id="34b16-138">Einddatum en-tijd voor de Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="34b16-138">End date-time for hello pipeline.</span></span> <span data-ttu-id="34b16-139">Als in de ISO-indeling moet worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="34b16-139">If specified must be in ISO format.</span></span> <span data-ttu-id="34b16-140">Bijvoorbeeld: 2014-10-14T17:32:41</span><span class="sxs-lookup"><span data-stu-id="34b16-140">For example: 2014-10-14T17:32:41</span></span> <br/><br/><span data-ttu-id="34b16-141">Het is mogelijk toospecify een plaatselijke tijd, bijvoorbeeld een geschatte tijd.</span><span class="sxs-lookup"><span data-stu-id="34b16-141">It is possible toospecify a local time, for example an EST time.</span></span> <span data-ttu-id="34b16-142">Hier volgt een voorbeeld: `2016-02-27T06:00:00**-05:00`, namelijk 6 AM EST.</span><span class="sxs-lookup"><span data-stu-id="34b16-142">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="34b16-143">9999-09-09 toorun Hallo pijplijn voor onbepaalde tijd opgeven als waarde voor end-eigenschap Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="34b16-143">toorun hello pipeline indefinitely, specify 9999-09-09 as hello value for hello end property.</span></span> |<span data-ttu-id="34b16-144">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-144">No</span></span> <br/><br/><span data-ttu-id="34b16-145">Als u een waarde voor Hallo start eigenschap opgeeft, moet u de waarde voor end-eigenschap Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="34b16-145">If you specify a value for hello start property, you must specify value for hello end property.</span></span><br/><br/><span data-ttu-id="34b16-146">Zie de opmerkingen voor Hallo **start** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="34b16-146">See notes for hello **start** property.</span></span> |
| <span data-ttu-id="34b16-147">isPaused</span><span class="sxs-lookup"><span data-stu-id="34b16-147">isPaused</span></span> |<span data-ttu-id="34b16-148">Als de set tootrue Hallo pijplijn kan niet worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="34b16-148">If set tootrue hello pipeline does not run.</span></span> <span data-ttu-id="34b16-149">Standaardwaarde = false.</span><span class="sxs-lookup"><span data-stu-id="34b16-149">Default value = false.</span></span> <span data-ttu-id="34b16-150">U kunt deze eigenschap tooenable gebruiken of uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="34b16-150">You can use this property tooenable or disable.</span></span> |<span data-ttu-id="34b16-151">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-151">No</span></span> |
| <span data-ttu-id="34b16-152">pipelineMode</span><span class="sxs-lookup"><span data-stu-id="34b16-152">pipelineMode</span></span> |<span data-ttu-id="34b16-153">Hallo-methode voor het plannen wordt uitgevoerd voor de Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="34b16-153">hello method for scheduling runs for hello pipeline.</span></span> <span data-ttu-id="34b16-154">Toegestane waarden zijn: (standaard), gepland eenmalige.</span><span class="sxs-lookup"><span data-stu-id="34b16-154">Allowed values are: scheduled (default), onetime.</span></span><br/><br/><span data-ttu-id="34b16-155">De geplande' geeft aan dat Hallo-pijplijn wordt uitgevoerd op een opgegeven tijdsinterval volgens tooits actieve periode (begin- en -tijd).</span><span class="sxs-lookup"><span data-stu-id="34b16-155">‘Scheduled’ indicates that hello pipeline runs at a specified time interval according tooits active period (start and end time).</span></span> <span data-ttu-id="34b16-156">'Eenmalige' geeft aan dat Hallo-pijplijn wordt slechts één keer uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="34b16-156">‘Onetime’ indicates that hello pipeline runs only once.</span></span> <span data-ttu-id="34b16-157">Eenmalige pijplijnen eenmaal gemaakt kunnen niet worden gewijzigd/bijgewerkt op dit moment.</span><span class="sxs-lookup"><span data-stu-id="34b16-157">Onetime pipelines once created cannot be modified/updated currently.</span></span> <span data-ttu-id="34b16-158">Zie [Onetime pijplijn](data-factory-create-pipelines.md#onetime-pipeline) voor meer informatie over het instellen van eenmalige.</span><span class="sxs-lookup"><span data-stu-id="34b16-158">See [Onetime pipeline](data-factory-create-pipelines.md#onetime-pipeline) for details about onetime setting.</span></span> |<span data-ttu-id="34b16-159">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-159">No</span></span> |
| <span data-ttu-id="34b16-160">expirationTime</span><span class="sxs-lookup"><span data-stu-id="34b16-160">expirationTime</span></span> |<span data-ttu-id="34b16-161">Tijdsduur na het maken voor welke Hallo pijplijn is geldig en moet worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="34b16-161">Duration of time after creation for which hello pipeline is valid and should remain provisioned.</span></span> <span data-ttu-id="34b16-162">Als er geen elk actief is, is mislukt, of in behandeling wordt uitgevoerd, Hallo pijplijn wordt automatisch verwijderd wanneer het Hallo-verlooptijd is bereikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-162">If it does not have any active, failed, or pending runs, hello pipeline is deleted automatically once it reaches hello expiration time.</span></span> |<span data-ttu-id="34b16-163">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-163">No</span></span> |


## <a name="activity"></a><span data-ttu-id="34b16-164">Activiteit</span><span class="sxs-lookup"><span data-stu-id="34b16-164">Activity</span></span> 
<span data-ttu-id="34b16-165">Hallo op hoog niveau structuur voor een activiteit in de definitie van een pijplijn (activiteiten element) is als volgt:</span><span class="sxs-lookup"><span data-stu-id="34b16-165">hello high-level structure for an activity within a pipeline definition (activities element) is as follows:</span></span>

```json
{
    "name": "ActivityName",
    "description": "description", 
    "type": "<ActivityType>",
    "inputs":  "[]",
    "outputs":  "[]",
    "linkedServiceName": "MyLinkedService",
    "typeProperties":
    {

    },
    "policy":
    {
    }
    "scheduler":
    {
    }
}
```

<span data-ttu-id="34b16-166">Na de tabel wordt beschreven Hallo eigenschappen binnen Hallo activiteit JSON-definitie:</span><span class="sxs-lookup"><span data-stu-id="34b16-166">Following table describe hello properties within hello activity JSON definition:</span></span>

| <span data-ttu-id="34b16-167">Label</span><span class="sxs-lookup"><span data-stu-id="34b16-167">Tag</span></span> | <span data-ttu-id="34b16-168">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-168">Description</span></span> | <span data-ttu-id="34b16-169">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-169">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-170">naam</span><span class="sxs-lookup"><span data-stu-id="34b16-170">name</span></span> |<span data-ttu-id="34b16-171">Naam van Hallo-activiteit.</span><span class="sxs-lookup"><span data-stu-id="34b16-171">Name of hello activity.</span></span> <span data-ttu-id="34b16-172">Geef een naam die Hallo-actie die Hallo activiteit vertegenwoordigt toodo geconfigureerd</span><span class="sxs-lookup"><span data-stu-id="34b16-172">Specify a name that represents hello action that hello activity is configured toodo</span></span><br/><ul><li><span data-ttu-id="34b16-173">Maximum aantal tekens: 260</span><span class="sxs-lookup"><span data-stu-id="34b16-173">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="34b16-174">Moet beginnen met een letter, cijfer of onderstrepingsteken (_)</span><span class="sxs-lookup"><span data-stu-id="34b16-174">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="34b16-175">Volgende tekens zijn niet toegestaan: '. ', '+ ','?', '/', '< ',' >', ' * ', "%", "&", ":","\\'</span><span class="sxs-lookup"><span data-stu-id="34b16-175">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="34b16-176">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-176">Yes</span></span> |
| <span data-ttu-id="34b16-177">description</span><span class="sxs-lookup"><span data-stu-id="34b16-177">description</span></span> |<span data-ttu-id="34b16-178">Tekst die beschrijft wat Hallo-activiteit wordt gebruikt voor.</span><span class="sxs-lookup"><span data-stu-id="34b16-178">Text describing what hello activity is used for.</span></span> |<span data-ttu-id="34b16-179">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-179">Yes</span></span> |
| <span data-ttu-id="34b16-180">type</span><span class="sxs-lookup"><span data-stu-id="34b16-180">type</span></span> |<span data-ttu-id="34b16-181">Hiermee geeft u Hallo Hallo-activiteit.</span><span class="sxs-lookup"><span data-stu-id="34b16-181">Specifies hello type of hello activity.</span></span> <span data-ttu-id="34b16-182">Zie Hallo [GEGEVENSARCHIEVEN](#data-stores) en [activiteiten voor GEGEVENSTRANSFORMATIE](#data-transformation-activities) secties voor verschillende soorten activiteiten.</span><span class="sxs-lookup"><span data-stu-id="34b16-182">See hello [DATA STORES](#data-stores) and [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) sections for different types of activities.</span></span> |<span data-ttu-id="34b16-183">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-183">Yes</span></span> |
| <span data-ttu-id="34b16-184">Invoer</span><span class="sxs-lookup"><span data-stu-id="34b16-184">inputs</span></span> |<span data-ttu-id="34b16-185">Invoertabellen die worden gebruikt door Hallo-activiteit</span><span class="sxs-lookup"><span data-stu-id="34b16-185">Input tables used by hello activity</span></span><br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |<span data-ttu-id="34b16-186">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-186">Yes</span></span> |
| <span data-ttu-id="34b16-187">uitvoer</span><span class="sxs-lookup"><span data-stu-id="34b16-187">outputs</span></span> |<span data-ttu-id="34b16-188">Uitvoergegevens tabellen gebruikt door Hallo-activiteit.</span><span class="sxs-lookup"><span data-stu-id="34b16-188">Output tables used by hello activity.</span></span><br/><br/>`// one output table`<br/>`"outputs":  [ { "name": “outputtable1” } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": “outputtable1” }, { "name": “outputtable2” }  ],` |<span data-ttu-id="34b16-189">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-189">Yes</span></span> |
| <span data-ttu-id="34b16-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="34b16-190">linkedServiceName</span></span> |<span data-ttu-id="34b16-191">Naam van Hallo gekoppelde service die wordt gebruikt door het Hallo-activiteit.</span><span class="sxs-lookup"><span data-stu-id="34b16-191">Name of hello linked service used by hello activity.</span></span> <br/><br/><span data-ttu-id="34b16-192">Een activiteit kan vereisen dat u opgeeft Hallo gekoppelde service die is gekoppeld aan toohello vereist compute-omgeving.</span><span class="sxs-lookup"><span data-stu-id="34b16-192">An activity may require that you specify hello linked service that links toohello required compute environment.</span></span> |<span data-ttu-id="34b16-193">Ja voor HDInsight-activiteiten, Azure Machine Learning-activiteiten en activiteit opgeslagen Procedure.</span><span class="sxs-lookup"><span data-stu-id="34b16-193">Yes for HDInsight activities, Azure Machine Learning activities, and Stored Procedure Activity.</span></span> <br/><br/><span data-ttu-id="34b16-194">Nee voor alle andere</span><span class="sxs-lookup"><span data-stu-id="34b16-194">No for all others</span></span> |
| <span data-ttu-id="34b16-195">typeProperties</span><span class="sxs-lookup"><span data-stu-id="34b16-195">typeProperties</span></span> |<span data-ttu-id="34b16-196">Eigenschappen in Hallo typeProperties sectie, is afhankelijk van type Hallo-activiteit.</span><span class="sxs-lookup"><span data-stu-id="34b16-196">Properties in hello typeProperties section depend on type of hello activity.</span></span> |<span data-ttu-id="34b16-197">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-197">No</span></span> |
| <span data-ttu-id="34b16-198">policy</span><span class="sxs-lookup"><span data-stu-id="34b16-198">policy</span></span> |<span data-ttu-id="34b16-199">Beleidsregels die invloed hebben op Hallo run-time gedrag van Hallo-activiteit.</span><span class="sxs-lookup"><span data-stu-id="34b16-199">Policies that affect hello run-time behavior of hello activity.</span></span> <span data-ttu-id="34b16-200">Als deze niet is opgegeven, worden de standaardbeleidsregels gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-200">If it is not specified, default policies are used.</span></span> |<span data-ttu-id="34b16-201">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-201">No</span></span> |
| <span data-ttu-id="34b16-202">Scheduler</span><span class="sxs-lookup"><span data-stu-id="34b16-202">scheduler</span></span> |<span data-ttu-id="34b16-203">'scheduler'-eigenschap is gebruikte toodefine gewenst schema voor het Hallo-activiteit.</span><span class="sxs-lookup"><span data-stu-id="34b16-203">“scheduler” property is used toodefine desired scheduling for hello activity.</span></span> <span data-ttu-id="34b16-204">Bijbehorende subeigenschappen zijn hetzelfde als de waarden in Hallo HALLO hallo [eigenschap beschikbaarheid in een dataset](data-factory-create-datasets.md#dataset-availability).</span><span class="sxs-lookup"><span data-stu-id="34b16-204">Its subproperties are hello same as hello ones in hello [availability property in a dataset](data-factory-create-datasets.md#dataset-availability).</span></span> |<span data-ttu-id="34b16-205">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-205">No</span></span> |

### <a name="policies"></a><span data-ttu-id="34b16-206">Beleidsregels</span><span class="sxs-lookup"><span data-stu-id="34b16-206">Policies</span></span>
<span data-ttu-id="34b16-207">Beleid geldt voor Hallo run-time gedrag van een activiteit specifiek wanneer Hallo segment van een tabel wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="34b16-207">Policies affect hello run-time behavior of an activity, specifically when hello slice of a table is processed.</span></span> <span data-ttu-id="34b16-208">Hallo volgende tabel biedt details Hallo.</span><span class="sxs-lookup"><span data-stu-id="34b16-208">hello following table provides hello details.</span></span>

| <span data-ttu-id="34b16-209">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-209">Property</span></span> | <span data-ttu-id="34b16-210">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="34b16-210">Permitted values</span></span> | <span data-ttu-id="34b16-211">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="34b16-211">Default Value</span></span> | <span data-ttu-id="34b16-212">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-212">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-213">Gelijktijdigheid van taken</span><span class="sxs-lookup"><span data-stu-id="34b16-213">concurrency</span></span> |<span data-ttu-id="34b16-214">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="34b16-214">Integer</span></span> <br/><br/><span data-ttu-id="34b16-215">De maximale waarde: 10</span><span class="sxs-lookup"><span data-stu-id="34b16-215">Max value: 10</span></span> |<span data-ttu-id="34b16-216">1</span><span class="sxs-lookup"><span data-stu-id="34b16-216">1</span></span> |<span data-ttu-id="34b16-217">Het aantal gelijktijdige uitvoeringen van Hallo-activiteit.</span><span class="sxs-lookup"><span data-stu-id="34b16-217">Number of concurrent executions of hello activity.</span></span><br/><br/><span data-ttu-id="34b16-218">Bepaalt de Hallo aantal parallelle activiteit uitvoeringen die kunnen ontstaan op verschillende segmenten.</span><span class="sxs-lookup"><span data-stu-id="34b16-218">It determines hello number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="34b16-219">Bijvoorbeeld, als een activiteit toogo via moet sneller een groot aantal beschikbare gegevens, een grotere waarde voor gelijktijdigheid Hallo gegevensverwerking.</span><span class="sxs-lookup"><span data-stu-id="34b16-219">For example, if an activity needs toogo through a large set of available data, having a larger concurrency value speeds up hello data processing.</span></span> |
| <span data-ttu-id="34b16-220">executionPriorityOrder</span><span class="sxs-lookup"><span data-stu-id="34b16-220">executionPriorityOrder</span></span> |<span data-ttu-id="34b16-221">NewestFirst</span><span class="sxs-lookup"><span data-stu-id="34b16-221">NewestFirst</span></span><br/><br/><span data-ttu-id="34b16-222">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="34b16-222">OldestFirst</span></span> |<span data-ttu-id="34b16-223">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="34b16-223">OldestFirst</span></span> |<span data-ttu-id="34b16-224">Hiermee wordt bepaald Hallo ordening van gegevenssegmenten dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="34b16-224">Determines hello ordering of data slices that are being processed.</span></span><br/><br/><span data-ttu-id="34b16-225">Als er 2 segmenten (één gebeurt om 4 uur en 17: 00 uur een andere één voor één) en beide zijn in behandeling kan worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="34b16-225">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span></span> <span data-ttu-id="34b16-226">Als u Hallo executionPriorityOrder toobe NewestFirst instelt, wordt eerst segment hello om 17.00 verwerkt.</span><span class="sxs-lookup"><span data-stu-id="34b16-226">If you set hello executionPriorityOrder toobe NewestFirst, hello slice at 5 PM is processed first.</span></span> <span data-ttu-id="34b16-227">Op dezelfde manier als u Hallo executionPriorityORder toobe OldestFIrst hebt ingesteld, klikt u vervolgens Hallo segment om 4 uur is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="34b16-227">Similarly if you set hello executionPriorityORder toobe OldestFIrst, then hello slice at 4 PM is processed.</span></span> |
| <span data-ttu-id="34b16-228">retry</span><span class="sxs-lookup"><span data-stu-id="34b16-228">retry</span></span> |<span data-ttu-id="34b16-229">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="34b16-229">Integer</span></span><br/><br/><span data-ttu-id="34b16-230">De maximale waarde is 10</span><span class="sxs-lookup"><span data-stu-id="34b16-230">Max value can be 10</span></span> |<span data-ttu-id="34b16-231">0</span><span class="sxs-lookup"><span data-stu-id="34b16-231">0</span></span> |<span data-ttu-id="34b16-232">Aantal nieuwe pogingen voordat de gegevensverwerking Hallo voor Hallo segment wordt als mislukt gemarkeerd.</span><span class="sxs-lookup"><span data-stu-id="34b16-232">Number of retries before hello data processing for hello slice is marked as Failure.</span></span> <span data-ttu-id="34b16-233">Activiteit is uitgevoerd voor een gegevenssegment wordt opnieuw geprobeerd up toohello opgegeven aantal nieuwe pogingen.</span><span class="sxs-lookup"><span data-stu-id="34b16-233">Activity execution for a data slice is retried up toohello specified retry count.</span></span> <span data-ttu-id="34b16-234">Hallo nieuwe poging wordt gedaan zo snel mogelijk na een storing Hallo.</span><span class="sxs-lookup"><span data-stu-id="34b16-234">hello retry is done as soon as possible after hello failure.</span></span> |
| <span data-ttu-id="34b16-235">timeout</span><span class="sxs-lookup"><span data-stu-id="34b16-235">timeout</span></span> |<span data-ttu-id="34b16-236">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="34b16-236">TimeSpan</span></span> |<span data-ttu-id="34b16-237">00:00:00</span><span class="sxs-lookup"><span data-stu-id="34b16-237">00:00:00</span></span> |<span data-ttu-id="34b16-238">Time-out voor Hallo-activiteit.</span><span class="sxs-lookup"><span data-stu-id="34b16-238">Timeout for hello activity.</span></span> <span data-ttu-id="34b16-239">Voorbeeld: 00:10:00 (impliceert time-out 10 minuten)</span><span class="sxs-lookup"><span data-stu-id="34b16-239">Example: 00:10:00 (implies timeout 10 mins)</span></span><br/><br/><span data-ttu-id="34b16-240">Als een waarde niet opgegeven is of 0 is, is Hallo time-out oneindig.</span><span class="sxs-lookup"><span data-stu-id="34b16-240">If a value is not specified or is 0, hello timeout is infinite.</span></span><br/><br/><span data-ttu-id="34b16-241">Hallo gegevensverwerking tijd op een segment overschrijdt de time-outwaarde Hallo, deze wordt geannuleerd als Hallo-systeem probeert tooretry Hallo verwerking.</span><span class="sxs-lookup"><span data-stu-id="34b16-241">If hello data processing time on a slice exceeds hello timeout value, it is canceled, and hello system attempts tooretry hello processing.</span></span> <span data-ttu-id="34b16-242">Hallo aantal nieuwe pogingen, is afhankelijk van de eigenschap retry Hallo.</span><span class="sxs-lookup"><span data-stu-id="34b16-242">hello number of retries depends on hello retry property.</span></span> <span data-ttu-id="34b16-243">Wanneer een time-out optreedt, Hallo status tooTimedOut ingesteld.</span><span class="sxs-lookup"><span data-stu-id="34b16-243">When timeout occurs, hello status is set tooTimedOut.</span></span> |
| <span data-ttu-id="34b16-244">Vertraging</span><span class="sxs-lookup"><span data-stu-id="34b16-244">delay</span></span> |<span data-ttu-id="34b16-245">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="34b16-245">TimeSpan</span></span> |<span data-ttu-id="34b16-246">00:00:00</span><span class="sxs-lookup"><span data-stu-id="34b16-246">00:00:00</span></span> |<span data-ttu-id="34b16-247">Geef Hallo vertraging optreden voordat de verwerking van Hallo segment wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="34b16-247">Specify hello delay before data processing of hello slice starts.</span></span><br/><br/><span data-ttu-id="34b16-248">Hallo-uitvoering van de activiteit voor een gegevenssegment wordt gestart nadat Hallo vertraging is verstreken Hallo uitvoeringstijd verwacht.</span><span class="sxs-lookup"><span data-stu-id="34b16-248">hello execution of activity for a data slice is started after hello Delay is past hello expected execution time.</span></span><br/><br/><span data-ttu-id="34b16-249">Voorbeeld: 00:10:00 (betekent vertraging van 10 minuten)</span><span class="sxs-lookup"><span data-stu-id="34b16-249">Example: 00:10:00 (implies delay of 10 mins)</span></span> |
| <span data-ttu-id="34b16-250">longRetry</span><span class="sxs-lookup"><span data-stu-id="34b16-250">longRetry</span></span> |<span data-ttu-id="34b16-251">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="34b16-251">Integer</span></span><br/><br/><span data-ttu-id="34b16-252">De maximale waarde: 10</span><span class="sxs-lookup"><span data-stu-id="34b16-252">Max value: 10</span></span> |<span data-ttu-id="34b16-253">1</span><span class="sxs-lookup"><span data-stu-id="34b16-253">1</span></span> |<span data-ttu-id="34b16-254">Hallo aantal lang pogingen proberen voordat Hallo segment uitvoering is mislukt.</span><span class="sxs-lookup"><span data-stu-id="34b16-254">hello number of long retry attempts before hello slice execution is failed.</span></span><br/><br/><span data-ttu-id="34b16-255">longRetry pogingen door longRetryInterval gelijkmatig verdeeld.</span><span class="sxs-lookup"><span data-stu-id="34b16-255">longRetry attempts are spaced by longRetryInterval.</span></span> <span data-ttu-id="34b16-256">Als u een tijd tussen pogingen toospecify moet, dus longRetry gebruiken.</span><span class="sxs-lookup"><span data-stu-id="34b16-256">So if you need toospecify a time between retry attempts, use longRetry.</span></span> <span data-ttu-id="34b16-257">Als zowel de nieuwe pogingen en de longRetry worden opgegeven, elke poging longRetry bevat nieuwe pogingen en Hallo kunt u het maximale aantal pogingen is opnieuw * longRetry.</span><span class="sxs-lookup"><span data-stu-id="34b16-257">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and hello max number of attempts is Retry * longRetry.</span></span><br/><br/><span data-ttu-id="34b16-258">Bijvoorbeeld, als er Hallo instellingen in Hallo activiteit-beleid te volgen:</span><span class="sxs-lookup"><span data-stu-id="34b16-258">For example, if we have hello following settings in hello activity policy:</span></span><br/><span data-ttu-id="34b16-259">Probeer: 3</span><span class="sxs-lookup"><span data-stu-id="34b16-259">Retry: 3</span></span><br/><span data-ttu-id="34b16-260">longRetry: 2</span><span class="sxs-lookup"><span data-stu-id="34b16-260">longRetry: 2</span></span><br/><span data-ttu-id="34b16-261">longRetryInterval: 01:00:00 uur</span><span class="sxs-lookup"><span data-stu-id="34b16-261">longRetryInterval: 01:00:00</span></span><br/><br/><span data-ttu-id="34b16-262">Wordt ervan uitgegaan dat er is slechts één segment tooexecute (status Waiting) en Hallo activiteit is uitgevoerd elke keer mislukt.</span><span class="sxs-lookup"><span data-stu-id="34b16-262">Assume there is only one slice tooexecute (status is Waiting) and hello activity execution fails every time.</span></span> <span data-ttu-id="34b16-263">Er zou worden in eerste instantie 3 opeenvolgende uitvoering pogingen.</span><span class="sxs-lookup"><span data-stu-id="34b16-263">Initially there would be 3 consecutive execution attempts.</span></span> <span data-ttu-id="34b16-264">Na elke poging zijn Hallo segment status probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="34b16-264">After each attempt, hello slice status would be Retry.</span></span> <span data-ttu-id="34b16-265">Nadat de eerste 3 pogingen hebben bekeken, zou Hallo segment status LongRetry zijn.</span><span class="sxs-lookup"><span data-stu-id="34b16-265">After first 3 attempts are over, hello slice status would be LongRetry.</span></span><br/><br/><span data-ttu-id="34b16-266">Na een uur (dat wil zeggen, de longRetryInteval waarde), zou er een andere set 3 opeenvolgende uitvoering pogingen.</span><span class="sxs-lookup"><span data-stu-id="34b16-266">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span></span> <span data-ttu-id="34b16-267">Hallo segment status zou niet hierna is en geen pogingen meer zou worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="34b16-267">After that, hello slice status would be Failed and no more retries would be attempted.</span></span> <span data-ttu-id="34b16-268">Daarom is algemene 6 geprobeerd.</span><span class="sxs-lookup"><span data-stu-id="34b16-268">Hence overall 6 attempts were made.</span></span><br/><br/><span data-ttu-id="34b16-269">Als een uitvoering is geslaagd, Hallo segment de status gereed zijn en er worden geen pogingen meer geprobeerd.</span><span class="sxs-lookup"><span data-stu-id="34b16-269">If any execution succeeds, hello slice status would be Ready and no more retries are attempted.</span></span><br/><br/><span data-ttu-id="34b16-270">longRetry kan worden gebruikt in situaties waarbij afhankelijke gegevens aankomen op niet-deterministische tijdstippen of hello algehele omgeving flaky onder welke gegevensverwerking plaatsvindt.</span><span class="sxs-lookup"><span data-stu-id="34b16-270">longRetry may be used in situations where dependent data arrives at non-deterministic times or hello overall environment is flaky under which data processing occurs.</span></span> <span data-ttu-id="34b16-271">In dergelijke gevallen niet pogingen doen achter elkaar kunt en uitvoer doet na een tijd resulteert in het Hallo-interval gewenst.</span><span class="sxs-lookup"><span data-stu-id="34b16-271">In such cases, doing retries one after another may not help and doing so after an interval of time results in hello desired output.</span></span><br/><br/><span data-ttu-id="34b16-272">Waarschuwing: geen hoge waarden voor de longRetry of longRetryInterval instelt.</span><span class="sxs-lookup"><span data-stu-id="34b16-272">Word of caution: do not set high values for longRetry or longRetryInterval.</span></span> <span data-ttu-id="34b16-273">Hogere waarden dat normaal gesproken andere al problemen.</span><span class="sxs-lookup"><span data-stu-id="34b16-273">Typically, higher values imply other systemic issues.</span></span> |
| <span data-ttu-id="34b16-274">longRetryInterval</span><span class="sxs-lookup"><span data-stu-id="34b16-274">longRetryInterval</span></span> |<span data-ttu-id="34b16-275">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="34b16-275">TimeSpan</span></span> |<span data-ttu-id="34b16-276">00:00:00</span><span class="sxs-lookup"><span data-stu-id="34b16-276">00:00:00</span></span> |<span data-ttu-id="34b16-277">Hallo vertraging tussen pogingen lang</span><span class="sxs-lookup"><span data-stu-id="34b16-277">hello delay between long retry attempts</span></span> |

### <a name="typeproperties-section"></a><span data-ttu-id="34b16-278">typeProperties sectie</span><span class="sxs-lookup"><span data-stu-id="34b16-278">typeProperties section</span></span>
<span data-ttu-id="34b16-279">Hallo typeProperties sectie verschilt voor elke activiteit.</span><span class="sxs-lookup"><span data-stu-id="34b16-279">hello typeProperties section is different for each activity.</span></span> <span data-ttu-id="34b16-280">Activiteiten voor gegevenstransformatie hebben zojuist Hallo-type-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="34b16-280">Transformation activities have just hello type properties.</span></span> <span data-ttu-id="34b16-281">Zie [activiteiten voor GEGEVENSTRANSFORMATIE](#data-transformation-activities) sectie in dit artikel voor JSON-voorbeelden die activiteiten voor gegevenstransformatie in een pijplijn definiëren.</span><span class="sxs-lookup"><span data-stu-id="34b16-281">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span></span> 

<span data-ttu-id="34b16-282">**Kopieeractiviteit** heeft twee subsecties in Hallo typeProperties sectie: **bron** en **sink**.</span><span class="sxs-lookup"><span data-stu-id="34b16-282">**Copy activity** has two subsections in hello typeProperties section: **source** and **sink**.</span></span> <span data-ttu-id="34b16-283">Zie [GEGEVENSARCHIEVEN](#data-stores) sectie in dit artikel voor JSON-voorbeelden die tonen hoe een data toouse opslaan als een bron-en/of sink.</span><span class="sxs-lookup"><span data-stu-id="34b16-283">See [DATA STORES](#data-stores) section in this article for JSON samples that show how toouse a data store as a source and/or sink.</span></span> 

### <a name="sample-copy-pipeline"></a><span data-ttu-id="34b16-284">Voorbeeld van kopieerpijplijn</span><span class="sxs-lookup"><span data-stu-id="34b16-284">Sample copy pipeline</span></span>
<span data-ttu-id="34b16-285">In het Hallo-voorbeeldpijplijn te volgen, wordt een activiteit van het type **kopie** in Hallo **activiteiten** sectie.</span><span class="sxs-lookup"><span data-stu-id="34b16-285">In hello following sample pipeline, there is one activity of type **Copy** in hello **activities** section.</span></span> <span data-ttu-id="34b16-286">In dit voorbeeld Hallo [Kopieeractiviteit](data-factory-data-movement-activities.md) gegevens worden gekopieerd van een Azure Blob storage tooan Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="34b16-286">In this sample, hello [Copy activity](data-factory-data-movement-activities.md) copies data from an Azure Blob storage tooan Azure SQL database.</span></span> 

```json
{
  "name": "CopyPipeline",
  "properties": {
    "description": "Copy data from a blob tooAzure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "type": "Copy",
        "inputs": [
          {
            "name": "InputDataset"
          }
        ],
        "outputs": [
          {
            "name": "OutputDataset"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink",
            "writeBatchSize": 10000,
            "writeBatchTimeout": "60:00:00"
          }
        },
        "Policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
    ],
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

<span data-ttu-id="34b16-287">Houd er rekening mee Hallo volgende punten:</span><span class="sxs-lookup"><span data-stu-id="34b16-287">Note hello following points:</span></span>

* <span data-ttu-id="34b16-288">In Hallo gedeelte activiteiten is er slechts één activiteit waarvan **type** te is ingesteld,**kopie**.</span><span class="sxs-lookup"><span data-stu-id="34b16-288">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span>
* <span data-ttu-id="34b16-289">Invoer voor Hallo-activiteit is ingesteld, te**InputDataset** en de uitvoer voor Hallo activiteit te is ingesteld**OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="34b16-289">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span>
* <span data-ttu-id="34b16-290">In Hallo **typeProperties** sectie **BlobSource** is opgegeven als Hallo brontype en **SqlSink** is opgegeven als Hallo sink-type.</span><span class="sxs-lookup"><span data-stu-id="34b16-290">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span>

<span data-ttu-id="34b16-291">Zie [GEGEVENSARCHIEVEN](#data-stores) sectie in dit artikel voor JSON-voorbeelden die tonen hoe een data toouse opslaan als een bron-en/of sink.</span><span class="sxs-lookup"><span data-stu-id="34b16-291">See [DATA STORES](#data-stores) section in this article for JSON samples that show how toouse a data store as a source and/or sink.</span></span>    

<span data-ttu-id="34b16-292">Zie voor een volledige procedure voor het maken van deze pipeline [zelfstudie: gegevens kopiëren van Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="34b16-292">For a complete walkthrough of creating this pipeline, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

### <a name="sample-transformation-pipeline"></a><span data-ttu-id="34b16-293">Voorbeeld van pijplijn voor transformatie</span><span class="sxs-lookup"><span data-stu-id="34b16-293">Sample transformation pipeline</span></span>
<span data-ttu-id="34b16-294">In het Hallo-voorbeeldpijplijn te volgen, wordt een activiteit van het type **HDInsightHive** in Hallo **activiteiten** sectie.</span><span class="sxs-lookup"><span data-stu-id="34b16-294">In hello following sample pipeline, there is one activity of type **HDInsightHive** in hello **activities** section.</span></span> <span data-ttu-id="34b16-295">In dit voorbeeld Hallo [HDInsight Hive-activiteit](data-factory-hive-activity.md) transformeert u gegevens uit een Azure Blob-opslag door het uitvoeren van een Hive-scriptbestand op een Azure HDInsight Hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="34b16-295">In this sample, hello [HDInsight Hive activity](data-factory-hive-activity.md) transforms data from an Azure Blob storage by running a Hive script file on an Azure HDInsight Hadoop cluster.</span></span> 

```json
{
    "name": "TransformPipeline",
    "properties": {
        "description": "My first Azure Data Factory pipeline",
        "activities": [
            {
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                    "scriptLinkedService": "AzureStorageLinkedService",
                    "defines": {
                        "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                        "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "policy": {
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Month",
                    "interval": 1
                },
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ],
        "start": "2016-04-01T00:00:00",
        "end": "2016-04-02T00:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="34b16-296">Houd er rekening mee Hallo volgende punten:</span><span class="sxs-lookup"><span data-stu-id="34b16-296">Note hello following points:</span></span> 

* <span data-ttu-id="34b16-297">In Hallo gedeelte activiteiten is er slechts één activiteit waarvan **type** te is ingesteld,**HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="34b16-297">In hello activities section, there is only one activity whose **type** is set too**HDInsightHive**.</span></span>
* <span data-ttu-id="34b16-298">Hallo Hive-scriptbestand **partitionweblogs.hql**, wordt opgeslagen in hello Azure storage-account (Hallo door scriptLinkedService met de opgegeven **AzureStorageLinkedService**), en in  **script** map in container Hallo **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="34b16-298">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>
* <span data-ttu-id="34b16-299">Hallo **definieert** sectie is gebruikte toospecify Hallo runtime-instellingen die toohello hive-script worden doorgegeven als Hive-configuratiewaarden (bijvoorbeeld `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).</span><span class="sxs-lookup"><span data-stu-id="34b16-299">hello **defines** section is used toospecify hello runtime settings that are passed toohello hive script as Hive configuration values (e.g `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).</span></span>

<span data-ttu-id="34b16-300">Zie [activiteiten voor GEGEVENSTRANSFORMATIE](#data-transformation-activities) sectie in dit artikel voor JSON-voorbeelden die activiteiten voor gegevenstransformatie in een pijplijn definiëren.</span><span class="sxs-lookup"><span data-stu-id="34b16-300">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span></span>

<span data-ttu-id="34b16-301">Zie voor een volledige procedure voor het maken van deze pipeline [zelfstudie: bouwen van uw eerste pijplijn tooprocess gegevens met Hadoop-cluster](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="34b16-301">For a complete walkthrough of creating this pipeline, see [Tutorial: Build your first pipeline tooprocess data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span> 

## <a name="linked-service"></a><span data-ttu-id="34b16-302">Gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="34b16-302">Linked service</span></span>
<span data-ttu-id="34b16-303">Hallo op hoog niveau structuur voor de definitie van een gekoppelde service is als volgt:</span><span class="sxs-lookup"><span data-stu-id="34b16-303">hello high-level structure for a linked service definition is as follows:</span></span>

```json
{
    "name": "<name of hello linked service>",
    "properties": {
        "type": "<type of hello linked service>",
        "typeProperties": {
        }
    }
}
```

<span data-ttu-id="34b16-304">Na de tabel wordt beschreven Hallo eigenschappen binnen Hallo activiteit JSON-definitie:</span><span class="sxs-lookup"><span data-stu-id="34b16-304">Following table describe hello properties within hello activity JSON definition:</span></span>

| <span data-ttu-id="34b16-305">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-305">Property</span></span> | <span data-ttu-id="34b16-306">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-306">Description</span></span> | <span data-ttu-id="34b16-307">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-307">Required</span></span> |
| -------- | ----------- | -------- | 
| <span data-ttu-id="34b16-308">naam</span><span class="sxs-lookup"><span data-stu-id="34b16-308">name</span></span> | <span data-ttu-id="34b16-309">Naam van Hallo gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="34b16-309">Name of hello linked service.</span></span> | <span data-ttu-id="34b16-310">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-310">Yes</span></span> | 
| <span data-ttu-id="34b16-311">Eigenschappen - type</span><span class="sxs-lookup"><span data-stu-id="34b16-311">properties - type</span></span> | <span data-ttu-id="34b16-312">Hallo type gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="34b16-312">Type of hello linked service.</span></span> <span data-ttu-id="34b16-313">Bijvoorbeeld: Azure Storage, Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="34b16-313">For example: Azure Storage, Azure SQL Database.</span></span> |
| <span data-ttu-id="34b16-314">typeProperties</span><span class="sxs-lookup"><span data-stu-id="34b16-314">typeProperties</span></span> | <span data-ttu-id="34b16-315">Hallo typeProperties sectie bevat de elementen die zijn verschillend voor elke gegevensopslag of compute-omgeving.</span><span class="sxs-lookup"><span data-stu-id="34b16-315">hello typeProperties section has elements that are different for each data store or compute environment.</span></span> <span data-ttu-id="34b16-316">Zie [gegevensarchieven](#datastores) sectie voor alle Hallo gegevensarchief gekoppelde services en [omgevingen compute](#compute-environments) voor alle Hallo compute gekoppelde services</span><span class="sxs-lookup"><span data-stu-id="34b16-316">See [data stores](#datastores) section for all hello data store linked services and [compute environments](#compute-environments) for all hello compute linked services</span></span> |   

## <a name="dataset"></a><span data-ttu-id="34b16-317">Gegevensset</span><span class="sxs-lookup"><span data-stu-id="34b16-317">Dataset</span></span> 
<span data-ttu-id="34b16-318">Een gegevensset in Azure Data Factory is als volgt gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="34b16-318">A dataset in Azure Data Factory is defined as follows:</span></span>

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "external": <boolean flag tooindicate external data. only for input datasets>,
        "linkedServiceName": "<Name of hello linked service that refers tooa data store.>",
        "structure": [
            {
                "name": "<Name of hello column>",
                "type": "<Name of hello type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        },
        "availability": {
            "frequency": "<Specifies hello time unit for data slice production. Supported frequency: Minute, Hour, Day, Week, Month>",
            "interval": "<Specifies hello interval within hello defined frequency. For example, frequency set too'Hour' and interval set too1 indicates that new data slices should be produced hourly>"
        },
       "policy":
        {      
        }
    }
}
```

<span data-ttu-id="34b16-319">Hallo volgende tabel beschrijft de eigenschappen in Hallo hierboven JSON:</span><span class="sxs-lookup"><span data-stu-id="34b16-319">hello following table describes properties in hello above JSON:</span></span>   

| <span data-ttu-id="34b16-320">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-320">Property</span></span> | <span data-ttu-id="34b16-321">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-321">Description</span></span> | <span data-ttu-id="34b16-322">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-322">Required</span></span> | <span data-ttu-id="34b16-323">Standaard</span><span class="sxs-lookup"><span data-stu-id="34b16-323">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-324">naam</span><span class="sxs-lookup"><span data-stu-id="34b16-324">name</span></span> | <span data-ttu-id="34b16-325">Naam van het Hallo-gegevensset.</span><span class="sxs-lookup"><span data-stu-id="34b16-325">Name of hello dataset.</span></span> <span data-ttu-id="34b16-326">Zie [Azure Data Factory - naamgevingsregels](data-factory-naming-rules.md) voor naamgevingsregels.</span><span class="sxs-lookup"><span data-stu-id="34b16-326">See [Azure Data Factory - Naming rules](data-factory-naming-rules.md) for naming rules.</span></span> |<span data-ttu-id="34b16-327">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-327">Yes</span></span> |<span data-ttu-id="34b16-328">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="34b16-328">NA</span></span> |
| <span data-ttu-id="34b16-329">type</span><span class="sxs-lookup"><span data-stu-id="34b16-329">type</span></span> | <span data-ttu-id="34b16-330">Type Hallo gegevensset.</span><span class="sxs-lookup"><span data-stu-id="34b16-330">Type of hello dataset.</span></span> <span data-ttu-id="34b16-331">Geef een Hallo die worden ondersteund door Azure Data Factory (bijvoorbeeld: AzureBlob, AzureSqlTable).</span><span class="sxs-lookup"><span data-stu-id="34b16-331">Specify one of hello types supported by Azure Data Factory (for example: AzureBlob, AzureSqlTable).</span></span> <span data-ttu-id="34b16-332">Zie [GEGEVENSARCHIEVEN](#data-stores) voor alle opgeslagen gegevens en de gegevensset die worden ondersteund door de Data Factory Hallo sectie.</span><span class="sxs-lookup"><span data-stu-id="34b16-332">See [DATA STORES](#data-stores) section for all hello data stores and dataset types supported by Data Factory.</span></span> | 
| <span data-ttu-id="34b16-333">structuur</span><span class="sxs-lookup"><span data-stu-id="34b16-333">structure</span></span> | <span data-ttu-id="34b16-334">Schema van Hallo dataset.</span><span class="sxs-lookup"><span data-stu-id="34b16-334">Schema of hello dataset.</span></span> <span data-ttu-id="34b16-335">Het bevat kolommen, de typen, enz.</span><span class="sxs-lookup"><span data-stu-id="34b16-335">It contains columns, their types, etc.</span></span> | <span data-ttu-id="34b16-336">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-336">No</span></span> |<span data-ttu-id="34b16-337">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="34b16-337">NA</span></span> |
| <span data-ttu-id="34b16-338">typeProperties</span><span class="sxs-lookup"><span data-stu-id="34b16-338">typeProperties</span></span> | <span data-ttu-id="34b16-339">Eigenschappen die overeenkomen toohello type geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="34b16-339">Properties corresponding toohello selected type.</span></span> <span data-ttu-id="34b16-340">Zie [GEGEVENSARCHIEVEN](#data-stores) sectie voor de ondersteunde typen en hun eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="34b16-340">See [DATA STORES](#data-stores) section for supported types and their properties.</span></span> |<span data-ttu-id="34b16-341">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-341">Yes</span></span> |<span data-ttu-id="34b16-342">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="34b16-342">NA</span></span> |
| <span data-ttu-id="34b16-343">external</span><span class="sxs-lookup"><span data-stu-id="34b16-343">external</span></span> | <span data-ttu-id="34b16-344">Booleaanse waarde vlag toospecify of een gegevensset wordt expliciet geproduceerd door een data factory-pijplijn of niet.</span><span class="sxs-lookup"><span data-stu-id="34b16-344">Boolean flag toospecify whether a dataset is explicitly produced by a data factory pipeline or not.</span></span> |<span data-ttu-id="34b16-345">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-345">No</span></span> |<span data-ttu-id="34b16-346">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="34b16-346">false</span></span> |
| <span data-ttu-id="34b16-347">availability</span><span class="sxs-lookup"><span data-stu-id="34b16-347">availability</span></span> | <span data-ttu-id="34b16-348">Hiermee definieert u Hallo venster of Hallo segmentering model voor Hallo gegevensset productie te verwerken.</span><span class="sxs-lookup"><span data-stu-id="34b16-348">Defines hello processing window or hello slicing model for hello dataset production.</span></span> <span data-ttu-id="34b16-349">Zie voor meer informatie op Hallo gegevensset segmentering model [planning en uitvoering](data-factory-scheduling-and-execution.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-349">For details on hello dataset slicing model, see [Scheduling and Execution](data-factory-scheduling-and-execution.md) article.</span></span> |<span data-ttu-id="34b16-350">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-350">Yes</span></span> |<span data-ttu-id="34b16-351">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="34b16-351">NA</span></span> |
| <span data-ttu-id="34b16-352">policy</span><span class="sxs-lookup"><span data-stu-id="34b16-352">policy</span></span> |<span data-ttu-id="34b16-353">Definieert Hallo criteria of Hallo voorwaarde waaraan Hallo gegevensset segmenten moeten voldoen.</span><span class="sxs-lookup"><span data-stu-id="34b16-353">Defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span> <br/><br/><span data-ttu-id="34b16-354">Zie voor meer informatie [gegevensset beleid](#Policy) sectie.</span><span class="sxs-lookup"><span data-stu-id="34b16-354">For details, see [Dataset Policy](#Policy) section.</span></span> |<span data-ttu-id="34b16-355">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-355">No</span></span> |<span data-ttu-id="34b16-356">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="34b16-356">NA</span></span> |

<span data-ttu-id="34b16-357">Elke kolom in Hallo **structuur** sectie bevat Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="34b16-357">Each column in hello **structure** section contains hello following properties:</span></span>

| <span data-ttu-id="34b16-358">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-358">Property</span></span> | <span data-ttu-id="34b16-359">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-359">Description</span></span> | <span data-ttu-id="34b16-360">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-360">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-361">naam</span><span class="sxs-lookup"><span data-stu-id="34b16-361">name</span></span> |<span data-ttu-id="34b16-362">Naam van het Hallo-kolom.</span><span class="sxs-lookup"><span data-stu-id="34b16-362">Name of hello column.</span></span> |<span data-ttu-id="34b16-363">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-363">Yes</span></span> |
| <span data-ttu-id="34b16-364">type</span><span class="sxs-lookup"><span data-stu-id="34b16-364">type</span></span> |<span data-ttu-id="34b16-365">Het gegevenstype van kolom Hallo.</span><span class="sxs-lookup"><span data-stu-id="34b16-365">Data type of hello column.</span></span>  |<span data-ttu-id="34b16-366">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-366">No</span></span> |
| <span data-ttu-id="34b16-367">Cultuur</span><span class="sxs-lookup"><span data-stu-id="34b16-367">culture</span></span> |<span data-ttu-id="34b16-368">.NET-gebaseerde cultuur toobe gebruikt bij het type is opgegeven en .NET-type `Datetime` of `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="34b16-368">.NET based culture toobe used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span></span> <span data-ttu-id="34b16-369">Standaard is `en-us`.</span><span class="sxs-lookup"><span data-stu-id="34b16-369">Default is `en-us`.</span></span> |<span data-ttu-id="34b16-370">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-370">No</span></span> |
| <span data-ttu-id="34b16-371">Indeling</span><span class="sxs-lookup"><span data-stu-id="34b16-371">format</span></span> |<span data-ttu-id="34b16-372">Indeling van tekenreeks toobe gebruikt bij het type is opgegeven en .NET-type `Datetime` of `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="34b16-372">Format string toobe used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span></span> |<span data-ttu-id="34b16-373">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-373">No</span></span> |

<span data-ttu-id="34b16-374">Hallo voorbeeld te volgen, Hallo gegevensset heeft drie kolommen `slicetimestamp`, `projectname`, en `pageviews` en ze zijn van het type: String, String en Decimal respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="34b16-374">In hello following example, hello dataset has three columns `slicetimestamp`, `projectname`, and `pageviews` and they are of type: String, String, and Decimal respectively.</span></span>

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

<span data-ttu-id="34b16-375">Hallo volgende tabel beschrijft eigenschappen die u in Hallo gebruiken kunt **beschikbaarheid** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-375">hello following table describes properties you can use in hello **availability** section:</span></span>

| <span data-ttu-id="34b16-376">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-376">Property</span></span> | <span data-ttu-id="34b16-377">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-377">Description</span></span> | <span data-ttu-id="34b16-378">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-378">Required</span></span> | <span data-ttu-id="34b16-379">Standaard</span><span class="sxs-lookup"><span data-stu-id="34b16-379">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-380">frequency</span><span class="sxs-lookup"><span data-stu-id="34b16-380">frequency</span></span> |<span data-ttu-id="34b16-381">Hiermee geeft u tijdseenheid Hallo voor gegevensset segment productie.</span><span class="sxs-lookup"><span data-stu-id="34b16-381">Specifies hello time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="34b16-382"><b>Ondersteunde frequentie</b>: minuut, uur, dag, Week, maand</span><span class="sxs-lookup"><span data-stu-id="34b16-382"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="34b16-383">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-383">Yes</span></span> |<span data-ttu-id="34b16-384">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="34b16-384">NA</span></span> |
| <span data-ttu-id="34b16-385">interval</span><span class="sxs-lookup"><span data-stu-id="34b16-385">interval</span></span> |<span data-ttu-id="34b16-386">Hiermee geeft u een vermenigvuldiger voor de frequentie</span><span class="sxs-lookup"><span data-stu-id="34b16-386">Specifies a multiplier for frequency</span></span><br/><br/><span data-ttu-id="34b16-387">"Frequentie x-interval" bepaalt hoe vaak hello segment wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="34b16-387">”Frequency x interval” determines how often hello slice is produced.</span></span><br/><br/><span data-ttu-id="34b16-388">Als u de gegevensset toobe gesegmenteerd op uurbasis moet hello, stelt u <b>frequentie</b> te<b>uur</b>, en <b>interval</b> te<b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="34b16-388">If you need hello dataset toobe sliced on an hourly basis, you set <b>Frequency</b> too<b>Hour</b>, and <b>interval</b> too<b>1</b>.</span></span><br/><br/><span data-ttu-id="34b16-389"><b>Opmerking</b>: als u de frequentie als minuut opgeeft, raden wij aan dat u Hallo interval toono kleiner is dan 15</span><span class="sxs-lookup"><span data-stu-id="34b16-389"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set hello interval toono less than 15</span></span> |<span data-ttu-id="34b16-390">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-390">Yes</span></span> |<span data-ttu-id="34b16-391">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="34b16-391">NA</span></span> |
| <span data-ttu-id="34b16-392">stijl</span><span class="sxs-lookup"><span data-stu-id="34b16-392">style</span></span> |<span data-ttu-id="34b16-393">Hiermee geeft u op of Hallo segment Hallo beginnen of eindigen van hello-interval moet worden geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="34b16-393">Specifies whether hello slice should be produced at hello start/end of hello interval.</span></span><ul><li><span data-ttu-id="34b16-394">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="34b16-394">StartOfInterval</span></span></li><li><span data-ttu-id="34b16-395">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="34b16-395">EndOfInterval</span></span></li></ul><br/><br/><span data-ttu-id="34b16-396">Als de frequentie tooMonth is ingesteld en stijl tooEndOfInterval is ingesteld, wordt Hallo segment op Hallo laatste dag van de maand geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="34b16-396">If Frequency is set tooMonth and style is set tooEndOfInterval, hello slice is produced on hello last day of month.</span></span> <span data-ttu-id="34b16-397">Als Hallo stijl is ingesteld tooStartOfInterval, wordt Hallo segment geproduceerd op Hallo eerste dag van de maand.</span><span class="sxs-lookup"><span data-stu-id="34b16-397">If hello style is set tooStartOfInterval, hello slice is produced on hello first day of month.</span></span><br/><br/><span data-ttu-id="34b16-398">Als frequentie tooDay is ingesteld en stijl tooEndOfInterval is ingesteld, wordt in het afgelopen uur van de dag Hallo HALLO hallo segment geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="34b16-398">If Frequency is set tooDay and style is set tooEndOfInterval, hello slice is produced in hello last hour of hello day.</span></span><br/><br/><span data-ttu-id="34b16-399">Als frequentie tooHour is ingesteld en stijl tooEndOfInterval is ingesteld, worden Hallo segment wordt geproduceerd achter Hallo Hallo uur.</span><span class="sxs-lookup"><span data-stu-id="34b16-399">If Frequency is set tooHour and style is set tooEndOfInterval, hello slice is produced at hello end of hello hour.</span></span> <span data-ttu-id="34b16-400">Voor een segment 1-2 uur gedurende Hallo segment geproduceerd om 2 uur.</span><span class="sxs-lookup"><span data-stu-id="34b16-400">For example, for a slice for 1 PM – 2 PM period, hello slice is produced at 2 PM.</span></span> |<span data-ttu-id="34b16-401">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-401">No</span></span> |<span data-ttu-id="34b16-402">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="34b16-402">EndOfInterval</span></span> |
| <span data-ttu-id="34b16-403">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="34b16-403">anchorDateTime</span></span> |<span data-ttu-id="34b16-404">Hiermee definieert u Hallo absolute positie in de tijd die wordt gebruikt door de grenzen van scheduler toocompute gegevensset segment.</span><span class="sxs-lookup"><span data-stu-id="34b16-404">Defines hello absolute position in time used by scheduler toocompute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="34b16-405"><b>Opmerking</b>: als Hallo AnchorDateTime bevat de datumonderdelen die meer gedetailleerd dan Hallo frequentie zijn dan hello gedetailleerdere onderdelen worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="34b16-405"><b>Note</b>: If hello AnchorDateTime has date parts that are more granular than hello frequency then hello more granular parts are ignored.</span></span> <br/><br/><span data-ttu-id="34b16-406">Bijvoorbeeld, als hello <b>interval</b> is <b>per uur</b> (frequentie: uur en interval: 1) en Hallo <b>AnchorDateTime</b> bevat <b>minuten en seconden</b>vervolgens Hallo <b>minuten en seconden</b> delen van Hallo AnchorDateTime worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="34b16-406">For example, if hello <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and hello <b>AnchorDateTime</b> contains <b>minutes and seconds</b> then hello <b>minutes and seconds</b> parts of hello AnchorDateTime are ignored.</span></span> |<span data-ttu-id="34b16-407">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-407">No</span></span> |<span data-ttu-id="34b16-408">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="34b16-408">01/01/0001</span></span> |
| <span data-ttu-id="34b16-409">offset</span><span class="sxs-lookup"><span data-stu-id="34b16-409">offset</span></span> |<span data-ttu-id="34b16-410">TimeSpan door welke Hallo begin en einde van alle segmenten van de gegevensset zijn verplaatst.</span><span class="sxs-lookup"><span data-stu-id="34b16-410">Timespan by which hello start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="34b16-411"><b>Opmerking</b>: als zowel anchorDateTime als offset worden opgegeven, Hallo resultaat Hallo gecombineerd shift is.</span><span class="sxs-lookup"><span data-stu-id="34b16-411"><b>Note</b>: If both anchorDateTime and offset are specified, hello result is hello combined shift.</span></span> |<span data-ttu-id="34b16-412">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-412">No</span></span> |<span data-ttu-id="34b16-413">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="34b16-413">NA</span></span> |

<span data-ttu-id="34b16-414">Hallo beschikbaarheidssectie na geeft aan dat uitvoergegevensset Hallo is geproduceerd per uur (of) invoer gegevensset per uur beschikbaar is:</span><span class="sxs-lookup"><span data-stu-id="34b16-414">hello following availability section specifies that hello output dataset is either produced hourly (or) input dataset is available hourly:</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

<span data-ttu-id="34b16-415">Hallo **beleid** sectie in de definitie van gegevensset definieert Hallo criteria of Hallo-voorwaarde die Hallo segmenten van de gegevensset moet voldoen.</span><span class="sxs-lookup"><span data-stu-id="34b16-415">hello **policy** section in dataset definition defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span>

| <span data-ttu-id="34b16-416">De naam van beleid</span><span class="sxs-lookup"><span data-stu-id="34b16-416">Policy Name</span></span> | <span data-ttu-id="34b16-417">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-417">Description</span></span> | <span data-ttu-id="34b16-418">Te worden toegepast</span><span class="sxs-lookup"><span data-stu-id="34b16-418">Applied too</span></span>| <span data-ttu-id="34b16-419">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-419">Required</span></span> | <span data-ttu-id="34b16-420">Standaard</span><span class="sxs-lookup"><span data-stu-id="34b16-420">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="34b16-421">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="34b16-421">minimumSizeMB</span></span> |<span data-ttu-id="34b16-422">Valideert dat Hallo-gegevens in een **Azure blob** voldoet aan de vereisten van de minimale grootte (in megabytes) Hallo.</span><span class="sxs-lookup"><span data-stu-id="34b16-422">Validates that hello data in an **Azure blob** meets hello minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="34b16-423">Azure Blob</span><span class="sxs-lookup"><span data-stu-id="34b16-423">Azure Blob</span></span> |<span data-ttu-id="34b16-424">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-424">No</span></span> |<span data-ttu-id="34b16-425">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="34b16-425">NA</span></span> |
| <span data-ttu-id="34b16-426">minimumRows</span><span class="sxs-lookup"><span data-stu-id="34b16-426">minimumRows</span></span> |<span data-ttu-id="34b16-427">Valideert dat Hallo-gegevens in een **Azure SQL-database** of een **Azure-tabel** Hallo minimum aantal rijen bevat.</span><span class="sxs-lookup"><span data-stu-id="34b16-427">Validates that hello data in an **Azure SQL database** or an **Azure table** contains hello minimum number of rows.</span></span> |<ul><li><span data-ttu-id="34b16-428">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="34b16-428">Azure SQL Database</span></span></li><li><span data-ttu-id="34b16-429">Azure-tabel</span><span class="sxs-lookup"><span data-stu-id="34b16-429">Azure Table</span></span></li></ul> |<span data-ttu-id="34b16-430">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-430">No</span></span> |<span data-ttu-id="34b16-431">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="34b16-431">NA</span></span> |

<span data-ttu-id="34b16-432">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="34b16-432">**Example:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="34b16-433">Tenzij een gegevensset wordt geproduceerd door Azure Data Factory, moet dit worden gemarkeerd als **externe**.</span><span class="sxs-lookup"><span data-stu-id="34b16-433">Unless a dataset is being produced by Azure Data Factory, it should be marked as **external**.</span></span> <span data-ttu-id="34b16-434">Deze instelling geldt doorgaans toohello input van de eerste activiteit in een pijplijn tenzij activiteit of koppeling van de pijplijn wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-434">This setting generally applies toohello inputs of first activity in a pipeline unless activity or pipeline chaining is being used.</span></span>

| <span data-ttu-id="34b16-435">Naam</span><span class="sxs-lookup"><span data-stu-id="34b16-435">Name</span></span> | <span data-ttu-id="34b16-436">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-436">Description</span></span> | <span data-ttu-id="34b16-437">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-437">Required</span></span> | <span data-ttu-id="34b16-438">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="34b16-438">Default Value</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-439">dataDelay</span><span class="sxs-lookup"><span data-stu-id="34b16-439">dataDelay</span></span> |<span data-ttu-id="34b16-440">Controle van de tijd toodelay Hallo Hallo beschikbaarheid van externe gegevens voor het opgegeven segment Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="34b16-440">Time toodelay hello check on hello availability of hello external data for hello given slice.</span></span> <span data-ttu-id="34b16-441">Bijvoorbeeld, als Hallo gegevens elk uur beschikbaar is, Hallo selectievakje toosee Hallo externe gegevens beschikbaar is en het bijbehorende Hallo segment kan gereed oplopen met behulp van dataDelay.</span><span class="sxs-lookup"><span data-stu-id="34b16-441">For example, if hello data is available hourly, hello check toosee hello external data is available and hello corresponding slice is Ready can be delayed by using dataDelay.</span></span><br/><br/><span data-ttu-id="34b16-442">Is alleen van toepassing toohello huidige tijd.</span><span class="sxs-lookup"><span data-stu-id="34b16-442">Only applies toohello present time.</span></span>  <span data-ttu-id="34b16-443">Bijvoorbeeld, als het is nu om 13:00 uur en deze waarde 10 minuten is, Hallo validatie wordt gestart om 1:10 uur.</span><span class="sxs-lookup"><span data-stu-id="34b16-443">For example, if it is 1:00 PM right now and this value is 10 minutes, hello validation starts at 1:10 PM.</span></span><br/><br/><span data-ttu-id="34b16-444">Deze instelling heeft geen invloed op de segmenten in de afgelopen hello (segmenten met segment eindtijd + dataDelay < nu) zonder enige vertraging worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="34b16-444">This setting does not affect slices in hello past (slices with Slice End Time + dataDelay < Now) are processed without any delay.</span></span><br/><br/><span data-ttu-id="34b16-445">Tijd groter is dan 23:59 uur moeten toospecified met Hallo `day.hours:minutes:seconds` indeling.</span><span class="sxs-lookup"><span data-stu-id="34b16-445">Time greater than 23:59 hours need toospecified using hello `day.hours:minutes:seconds` format.</span></span> <span data-ttu-id="34b16-446">Bijvoorbeeld: toospecify 24 uur niet gebruiken 24:00:00; Gebruik in plaats daarvan 1.00:00:00.</span><span class="sxs-lookup"><span data-stu-id="34b16-446">For example, toospecify 24 hours, don't use 24:00:00; instead, use 1.00:00:00.</span></span> <span data-ttu-id="34b16-447">Als u 24:00:00, wordt dit beschouwd als 24 dagen (24.00:00:00).</span><span class="sxs-lookup"><span data-stu-id="34b16-447">If you use 24:00:00, it is treated as 24 days (24.00:00:00).</span></span> <span data-ttu-id="34b16-448">Geef 1:04:00:00 voor 1 dag en 4 uur.</span><span class="sxs-lookup"><span data-stu-id="34b16-448">For 1 day and 4 hours, specify 1:04:00:00.</span></span> |<span data-ttu-id="34b16-449">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-449">No</span></span> |<span data-ttu-id="34b16-450">0</span><span class="sxs-lookup"><span data-stu-id="34b16-450">0</span></span> |
| <span data-ttu-id="34b16-451">retryInterval</span><span class="sxs-lookup"><span data-stu-id="34b16-451">retryInterval</span></span> |<span data-ttu-id="34b16-452">Hallo wachttijd tussen een fout en Hallo volgende nieuwe poging.</span><span class="sxs-lookup"><span data-stu-id="34b16-452">hello wait time between a failure and hello next retry attempt.</span></span> <span data-ttu-id="34b16-453">Als een try mislukt, is het volgende proberen Hallo na retryInterval.</span><span class="sxs-lookup"><span data-stu-id="34b16-453">If a try fails, hello next try is after retryInterval.</span></span> <br/><br/><span data-ttu-id="34b16-454">Als het nu om 13:00 uur, beginnen we de eerste poging Hallo.</span><span class="sxs-lookup"><span data-stu-id="34b16-454">If it is 1:00 PM right now, we begin hello first try.</span></span> <span data-ttu-id="34b16-455">Als Hallo duur toocomplete Hallo eerste validatiecontrole 1 minuut Hallo-bewerking is mislukt is, een nieuwe poging gedaan Hallo is 1:00 + 1 min (duur) + 1 min. (interval voor opnieuw proberen) = 1:02 PM.</span><span class="sxs-lookup"><span data-stu-id="34b16-455">If hello duration toocomplete hello first validation check is 1 minute and hello operation failed, hello next retry is at 1:00 + 1 min (duration) + 1 min (retry interval) = 1:02 PM.</span></span> <br/><br/><span data-ttu-id="34b16-456">Er is geen vertraging segmenten in de afgelopen Hallo.</span><span class="sxs-lookup"><span data-stu-id="34b16-456">For slices in hello past, there is no delay.</span></span> <span data-ttu-id="34b16-457">Hallo opnieuw gebeurt onmiddellijk.</span><span class="sxs-lookup"><span data-stu-id="34b16-457">hello retry happens immediately.</span></span> |<span data-ttu-id="34b16-458">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-458">No</span></span> |<span data-ttu-id="34b16-459">00:01:00 (1 minuut)</span><span class="sxs-lookup"><span data-stu-id="34b16-459">00:01:00 (1 minute)</span></span> |
| <span data-ttu-id="34b16-460">retryTimeout</span><span class="sxs-lookup"><span data-stu-id="34b16-460">retryTimeout</span></span> |<span data-ttu-id="34b16-461">Hallo-out voor nieuwe pogingen.</span><span class="sxs-lookup"><span data-stu-id="34b16-461">hello timeout for each retry attempt.</span></span><br/><br/><span data-ttu-id="34b16-462">Als deze eigenschap is ingesteld too10 minuten, Hallo validatie behoeften toobe voltooid binnen 10 minuten.</span><span class="sxs-lookup"><span data-stu-id="34b16-462">If this property is set too10 minutes, hello validation needs toobe completed within 10 minutes.</span></span> <span data-ttu-id="34b16-463">Als het duurt langer dan 10 minuten tooperform Hallo validatie, probeer Hallo time-out.</span><span class="sxs-lookup"><span data-stu-id="34b16-463">If it takes longer than 10 minutes tooperform hello validation, hello retry times out.</span></span><br/><br/><span data-ttu-id="34b16-464">Als alle pogingen voor Hallo validatie een time-out optreedt, wordt als een time-out opgetreden bij Hallo segment gemarkeerd.</span><span class="sxs-lookup"><span data-stu-id="34b16-464">If all attempts for hello validation times out, hello slice is marked as TimedOut.</span></span> |<span data-ttu-id="34b16-465">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-465">No</span></span> |<span data-ttu-id="34b16-466">00:10:00 (10 minuten)</span><span class="sxs-lookup"><span data-stu-id="34b16-466">00:10:00 (10 minutes)</span></span> |
| <span data-ttu-id="34b16-467">maximumRetry</span><span class="sxs-lookup"><span data-stu-id="34b16-467">maximumRetry</span></span> |<span data-ttu-id="34b16-468">Aantal keren dat toocheck voor beschikbaarheid Hallo Hallo externe gegevens.</span><span class="sxs-lookup"><span data-stu-id="34b16-468">Number of times toocheck for hello availability of hello external data.</span></span> <span data-ttu-id="34b16-469">Hallo toegestane maximale waarde is 10.</span><span class="sxs-lookup"><span data-stu-id="34b16-469">hello allowed maximum value is 10.</span></span> |<span data-ttu-id="34b16-470">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-470">No</span></span> |<span data-ttu-id="34b16-471">3</span><span class="sxs-lookup"><span data-stu-id="34b16-471">3</span></span> |


## <a name="data-stores"></a><span data-ttu-id="34b16-472">GEGEVENSOPSLAG</span><span class="sxs-lookup"><span data-stu-id="34b16-472">DATA STORES</span></span>
<span data-ttu-id="34b16-473">Hallo [gekoppelde service](#linked-service) beschrijvingen van de opgegeven sectie voor de JSON-elementen die algemene tooall typen gekoppelde services zijn.</span><span class="sxs-lookup"><span data-stu-id="34b16-473">hello [Linked service](#linked-service) section provided descriptions for JSON elements that are common tooall types of linked services.</span></span> <span data-ttu-id="34b16-474">Deze sectie bevat informatie over de JSON-elementen die specifiek tooeach gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="34b16-474">This section provides details about JSON elements that are specific tooeach data store.</span></span>

<span data-ttu-id="34b16-475">Hallo [gegevensset](#dataset) beschrijvingen van de opgegeven sectie voor de JSON-elementen die algemene tooall typen gegevenssets zijn.</span><span class="sxs-lookup"><span data-stu-id="34b16-475">hello [Dataset](#dataset) section provided descriptions for JSON elements that are common tooall types of datasets.</span></span> <span data-ttu-id="34b16-476">Deze sectie bevat informatie over de JSON-elementen die specifiek tooeach gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="34b16-476">This section provides details about JSON elements that are specific tooeach data store.</span></span>

<span data-ttu-id="34b16-477">Hallo [activiteit](#activity) beschrijvingen van de opgegeven sectie voor de JSON-elementen die algemene tooall soorten activiteiten zijn.</span><span class="sxs-lookup"><span data-stu-id="34b16-477">hello [Activity](#activity) section provided descriptions for JSON elements that are common tooall types of activities.</span></span> <span data-ttu-id="34b16-478">Deze sectie bevat informatie over de JSON-elementen die specifiek tooeach gegevensarchief wanneer deze wordt gebruikt als een bron/sink in een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="34b16-478">This section provides details about JSON elements that are specific tooeach data store when it is used as a source/sink in a copy activity.</span></span>  

<span data-ttu-id="34b16-479">Klik op de koppeling Hallo voor Hallo store u geïnteresseerd bent in toosee Hallo JSON-schema voor de gekoppelde service, gegevensset en bron/sink voor de kopieeractiviteit Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="34b16-479">Click hello link for hello store you are interested in toosee hello JSON schemas for linked service, dataset, and hello source/sink for hello copy activity.</span></span>

| <span data-ttu-id="34b16-480">Category</span><span class="sxs-lookup"><span data-stu-id="34b16-480">Category</span></span> | <span data-ttu-id="34b16-481">Gegevensarchief</span><span class="sxs-lookup"><span data-stu-id="34b16-481">Data store</span></span> 
|:--- |:--- |
| <span data-ttu-id="34b16-482">**Azure**</span><span class="sxs-lookup"><span data-stu-id="34b16-482">**Azure**</span></span> |[<span data-ttu-id="34b16-483">Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="34b16-483">Azure Blob storage</span></span>](#azure-blob-storage) |
| &nbsp; |[<span data-ttu-id="34b16-484">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="34b16-484">Azure Data Lake Store</span></span>](#azure-datalake-store) |
| &nbsp; |[<span data-ttu-id="34b16-485">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="34b16-485">Azure Cosmos DB</span></span>](#azure-cosmos-db) |
| &nbsp; |[<span data-ttu-id="34b16-486">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="34b16-486">Azure SQL Database</span></span>](#azure-sql-database) |
| &nbsp; |[<span data-ttu-id="34b16-487">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="34b16-487">Azure SQL Data Warehouse</span></span>](#azure-sql-data-warehouse) |
| &nbsp; |[<span data-ttu-id="34b16-488">Azure Search</span><span class="sxs-lookup"><span data-stu-id="34b16-488">Azure Search</span></span>](#azure-search) |
| &nbsp; |[<span data-ttu-id="34b16-489">Azure Table storage</span><span class="sxs-lookup"><span data-stu-id="34b16-489">Azure Table storage</span></span>](#azure-table-storage) |
| <span data-ttu-id="34b16-490">**Databases**</span><span class="sxs-lookup"><span data-stu-id="34b16-490">**Databases**</span></span> |[<span data-ttu-id="34b16-491">Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="34b16-491">Amazon Redshift</span></span>](#amazon-redshift) |
| &nbsp; |[<span data-ttu-id="34b16-492">IBM DB2</span><span class="sxs-lookup"><span data-stu-id="34b16-492">IBM DB2</span></span>](#ibm-db2) |
| &nbsp; |[<span data-ttu-id="34b16-493">MySQL</span><span class="sxs-lookup"><span data-stu-id="34b16-493">MySQL</span></span>](#mysql) |
| &nbsp; |[<span data-ttu-id="34b16-494">Oracle</span><span class="sxs-lookup"><span data-stu-id="34b16-494">Oracle</span></span>](#oracle) |
| &nbsp; |[<span data-ttu-id="34b16-495">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="34b16-495">PostgreSQL</span></span>](#postgresql) |
| &nbsp; |[<span data-ttu-id="34b16-496">SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="34b16-496">SAP Business Warehouse</span></span>](#sap-business-warehouse) |
| &nbsp; |[<span data-ttu-id="34b16-497">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="34b16-497">SAP HANA</span></span>](#sap-hana) |
| &nbsp; |[<span data-ttu-id="34b16-498">SQL Server</span><span class="sxs-lookup"><span data-stu-id="34b16-498">SQL Server</span></span>](#sql-server) |
| &nbsp; |[<span data-ttu-id="34b16-499">Sybase</span><span class="sxs-lookup"><span data-stu-id="34b16-499">Sybase</span></span>](#sybase) |
| &nbsp; |[<span data-ttu-id="34b16-500">Teradata</span><span class="sxs-lookup"><span data-stu-id="34b16-500">Teradata</span></span>](#teradata) |
| <span data-ttu-id="34b16-501">**NoSQL**</span><span class="sxs-lookup"><span data-stu-id="34b16-501">**NoSQL**</span></span> |[<span data-ttu-id="34b16-502">Cassandra</span><span class="sxs-lookup"><span data-stu-id="34b16-502">Cassandra</span></span>](#cassandra) |
| &nbsp; |[<span data-ttu-id="34b16-503">MongoDB</span><span class="sxs-lookup"><span data-stu-id="34b16-503">MongoDB</span></span>](#mongodb) |
| <span data-ttu-id="34b16-504">**File**</span><span class="sxs-lookup"><span data-stu-id="34b16-504">**File**</span></span> |[<span data-ttu-id="34b16-505">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="34b16-505">Amazon S3</span></span>](#amazon-s3) |
| &nbsp; |[<span data-ttu-id="34b16-506">Bestandssysteem</span><span class="sxs-lookup"><span data-stu-id="34b16-506">File System</span></span>](#file-system) |
| &nbsp; |[<span data-ttu-id="34b16-507">FTP</span><span class="sxs-lookup"><span data-stu-id="34b16-507">FTP</span></span>](#ftp) |
| &nbsp; |[<span data-ttu-id="34b16-508">HDFS</span><span class="sxs-lookup"><span data-stu-id="34b16-508">HDFS</span></span>](#hdfs) |
| &nbsp; |[<span data-ttu-id="34b16-509">SFTP</span><span class="sxs-lookup"><span data-stu-id="34b16-509">SFTP</span></span>](#sftp) |
| <span data-ttu-id="34b16-510">**Andere**</span><span class="sxs-lookup"><span data-stu-id="34b16-510">**Others**</span></span> |[<span data-ttu-id="34b16-511">HTTP</span><span class="sxs-lookup"><span data-stu-id="34b16-511">HTTP</span></span>](#http) |
| &nbsp; |[<span data-ttu-id="34b16-512">OData</span><span class="sxs-lookup"><span data-stu-id="34b16-512">OData</span></span>](#odata) |
| &nbsp; |[<span data-ttu-id="34b16-513">ODBC</span><span class="sxs-lookup"><span data-stu-id="34b16-513">ODBC</span></span>](#odbc) |
| &nbsp; |[<span data-ttu-id="34b16-514">Salesforce</span><span class="sxs-lookup"><span data-stu-id="34b16-514">Salesforce</span></span>](#salesforce) |
| &nbsp; |[<span data-ttu-id="34b16-515">Web-tabel</span><span class="sxs-lookup"><span data-stu-id="34b16-515">Web Table</span></span>](#web-table) |

## <a name="azure-blob-storage"></a><span data-ttu-id="34b16-516">Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="34b16-516">Azure Blob Storage</span></span>

### <a name="linked-service"></a><span data-ttu-id="34b16-517">Gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="34b16-517">Linked service</span></span>
<span data-ttu-id="34b16-518">Er zijn twee soorten gekoppelde services: gekoppelde Azure Storage-service en de gekoppelde Azure Storage SAS-service.</span><span class="sxs-lookup"><span data-stu-id="34b16-518">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span></span>

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="34b16-519">Een gekoppelde Azure Storage-service</span><span class="sxs-lookup"><span data-stu-id="34b16-519">Azure Storage Linked Service</span></span>
<span data-ttu-id="34b16-520">toolink uw Azure storage-account tooa data factory met behulp van Hallo **accountsleutel**, maak een gekoppelde Azure Storage-service.</span><span class="sxs-lookup"><span data-stu-id="34b16-520">toolink your Azure storage account tooa data factory by using hello **account key**, create an Azure Storage linked service.</span></span> <span data-ttu-id="34b16-521">toodefine een Azure Storage gekoppelde service, set Hallo **type** Hallo gekoppelde service te**AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="34b16-521">toodefine an Azure Storage linked service, set hello **type** of hello linked service too**AzureStorage**.</span></span> <span data-ttu-id="34b16-522">U kunt vervolgens opgeven na eigenschappen in Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-522">Then, you can specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="34b16-523">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-523">Property</span></span> | <span data-ttu-id="34b16-524">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-524">Description</span></span> | <span data-ttu-id="34b16-525">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-525">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="34b16-526">connectionString</span><span class="sxs-lookup"><span data-stu-id="34b16-526">connectionString</span></span> |<span data-ttu-id="34b16-527">Geef informatie tooconnect tooAzure opslag voor de eigenschap connectionString Hallo nodig.</span><span class="sxs-lookup"><span data-stu-id="34b16-527">Specify information needed tooconnect tooAzure storage for hello connectionString property.</span></span> |<span data-ttu-id="34b16-528">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-528">Yes</span></span> |

##### <a name="example"></a><span data-ttu-id="34b16-529">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-529">Example</span></span>  

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

#### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="34b16-530">Gekoppelde Azure Storage SAS-Service</span><span class="sxs-lookup"><span data-stu-id="34b16-530">Azure Storage SAS Linked Service</span></span>
<span data-ttu-id="34b16-531">Hallo SAS van Azure Storage gekoppelde service, kunt u een Azure Storage-Account tooan Azure data factory toolink met behulp van een Shared Access Signature (SAS).</span><span class="sxs-lookup"><span data-stu-id="34b16-531">hello Azure Storage SAS linked service allows you toolink an Azure Storage Account tooan Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="34b16-532">Het biedt Hallo data factory toegang beperkt/tijdsgebonden tooall/specifieke bronnen (blobcontainer) / in Hallo-opslag.</span><span class="sxs-lookup"><span data-stu-id="34b16-532">It provides hello data factory with restricted/time-bound access tooall/specific resources (blob/container) in hello storage.</span></span> <span data-ttu-id="34b16-533">toolink uw Azure storage-account tooa data factory met behulp van Shared Access Signature maken van een SAS van Azure Storage gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="34b16-533">toolink your Azure storage account tooa data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span></span> <span data-ttu-id="34b16-534">een Azure Storage-SAS toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="34b16-534">toodefine an Azure Storage SAS linked service, set hello **type** of hello linked service too**AzureStorageSas**.</span></span> <span data-ttu-id="34b16-535">U kunt vervolgens opgeven na eigenschappen in Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-535">Then, you can specify following properties in hello **typeProperties** section:</span></span>   

| <span data-ttu-id="34b16-536">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-536">Property</span></span> | <span data-ttu-id="34b16-537">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-537">Description</span></span> | <span data-ttu-id="34b16-538">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-538">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="34b16-539">sasUri</span><span class="sxs-lookup"><span data-stu-id="34b16-539">sasUri</span></span> |<span data-ttu-id="34b16-540">Geef de Shared Access Signature URI toohello Azure Storage-resources zoals blob-container of tabel.</span><span class="sxs-lookup"><span data-stu-id="34b16-540">Specify Shared Access Signature URI toohello Azure Storage resources such as blob, container, or table.</span></span> |<span data-ttu-id="34b16-541">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-541">Yes</span></span> |

##### <a name="example"></a><span data-ttu-id="34b16-542">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-542">Example</span></span>

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<storageUri>?<sasToken>"   
        }  
    }  
}  
```

<span data-ttu-id="34b16-543">Zie voor meer informatie over deze gekoppelde services, [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-543">For more information about these linked services, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="34b16-544">Gegevensset</span><span class="sxs-lookup"><span data-stu-id="34b16-544">Dataset</span></span>
<span data-ttu-id="34b16-545">toodefine een Azure Blob-gegevensset set Hallo **type** van Hallo gegevensset te**AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="34b16-545">toodefine an Azure Blob dataset, set hello **type** of hello dataset too**AzureBlob**.</span></span> <span data-ttu-id="34b16-546">Geef vervolgens de volgende specifieke eigenschappen van de Azure-Blob in Hallo Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-546">Then, specify hello following Azure Blob specific properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="34b16-547">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-547">Property</span></span> | <span data-ttu-id="34b16-548">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-548">Description</span></span> | <span data-ttu-id="34b16-549">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-549">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-550">folderPath</span><span class="sxs-lookup"><span data-stu-id="34b16-550">folderPath</span></span> |<span data-ttu-id="34b16-551">Pad toohello container en map in Hallo blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="34b16-551">Path toohello container and folder in hello blob storage.</span></span> <span data-ttu-id="34b16-552">Voorbeeld: myblobcontainer\myblobfolder\\</span><span class="sxs-lookup"><span data-stu-id="34b16-552">Example: myblobcontainer\myblobfolder\\</span></span> |<span data-ttu-id="34b16-553">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-553">Yes</span></span> |
| <span data-ttu-id="34b16-554">fileName</span><span class="sxs-lookup"><span data-stu-id="34b16-554">fileName</span></span> |<span data-ttu-id="34b16-555">De naam van Hallo blob.</span><span class="sxs-lookup"><span data-stu-id="34b16-555">Name of hello blob.</span></span> <span data-ttu-id="34b16-556">Bestandsnaam is optioneel en is hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="34b16-556">fileName is optional and case-sensitive.</span></span><br/><br/><span data-ttu-id="34b16-557">Als u een bestandsnaam, Hallo activiteit (inclusief kopiëren) werkt opgeeft op Hallo specifieke Blob.</span><span class="sxs-lookup"><span data-stu-id="34b16-557">If you specify a filename, hello activity (including Copy) works on hello specific Blob.</span></span><br/><br/><span data-ttu-id="34b16-558">Bestandsnaam is opgegeven, bevat kopiëren alle Blobs Hallo folderPath voor invoergegevensset.</span><span class="sxs-lookup"><span data-stu-id="34b16-558">When fileName is not specified, Copy includes all Blobs in hello folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="34b16-559">Wanneer fileName niet voor een uitvoergegevensset opgegeven is, Hallo-naam van Hallo gegenereerd bestand in Hallo volgt deze indeling zou worden: gegevens. <Guid>.txt (voorbeeld:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="34b16-559">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="34b16-560">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-560">No</span></span> |
| <span data-ttu-id="34b16-561">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="34b16-561">partitionedBy</span></span> |<span data-ttu-id="34b16-562">partitionedBy is een optionele eigenschap.</span><span class="sxs-lookup"><span data-stu-id="34b16-562">partitionedBy is an optional property.</span></span> <span data-ttu-id="34b16-563">Kunt u deze toospecify een dynamische folderPath en de bestandsnaam voor de reeksgegevens.</span><span class="sxs-lookup"><span data-stu-id="34b16-563">You can use it toospecify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="34b16-564">FolderPath kan bijvoorbeeld parameters worden gebruikt voor elk uur van gegevens.</span><span class="sxs-lookup"><span data-stu-id="34b16-564">For example, folderPath can be parameterized for every hour of data.</span></span> |<span data-ttu-id="34b16-565">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-565">No</span></span> |
| <span data-ttu-id="34b16-566">Indeling</span><span class="sxs-lookup"><span data-stu-id="34b16-566">format</span></span> | <span data-ttu-id="34b16-567">Hallo na indelingstypen worden ondersteund: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="34b16-567">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="34b16-568">Set Hallo **type** eigenschap onder indeling tooone van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="34b16-568">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="34b16-569">Zie voor meer informatie [tekstindeling](data-factory-supported-file-and-compression-formats.md#text-format), [Json-indeling](data-factory-supported-file-and-compression-formats.md#json-format), [Avro-indeling](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc indeling](data-factory-supported-file-and-compression-formats.md#orc-format), en [parketvloeren indeling](data-factory-supported-file-and-compression-formats.md#parquet-format) secties.</span><span class="sxs-lookup"><span data-stu-id="34b16-569">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="34b16-570">Als u wilt dat te**kopiëren van bestanden als-is** tussen bestandsgebaseerde winkels (binaire kopiëren) Hallo indeling sectie in beide definities invoer en uitvoer gegevensset overslaan.</span><span class="sxs-lookup"><span data-stu-id="34b16-570">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="34b16-571">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-571">No</span></span> |
| <span data-ttu-id="34b16-572">Compressie</span><span class="sxs-lookup"><span data-stu-id="34b16-572">compression</span></span> | <span data-ttu-id="34b16-573">Hallo-type en compressieniveau voor Hallo gegevens opgeven.</span><span class="sxs-lookup"><span data-stu-id="34b16-573">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="34b16-574">Ondersteunde typen zijn: **GZip**, **Deflate**, **BZip2**, en **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="34b16-574">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="34b16-575">Ondersteunde niveaus: **optimale** en **snelst**.</span><span class="sxs-lookup"><span data-stu-id="34b16-575">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="34b16-576">Zie voor meer informatie [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="34b16-576">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="34b16-577">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-577">No</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-578">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-578">Example</span></span>

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
 ```


<span data-ttu-id="34b16-579">Zie voor meer informatie [Azure Blob-connector](data-factory-azure-blob-connector.md#dataset-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-579">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#dataset-properties) article.</span></span>

### <a name="blobsource-in-copy-activity"></a><span data-ttu-id="34b16-580">BlobSource in de kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="34b16-580">BlobSource in Copy Activity</span></span>
<span data-ttu-id="34b16-581">Als u gegevens uit een Azure Blob Storage kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**BlobSource**, en opgeven na eigenschappen in Hallo ** bron ** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-581">If you are copying data from an Azure Blob Storage, set hello **source type** of hello copy activity too**BlobSource**, and specify following properties in hello **source **section:</span></span>

| <span data-ttu-id="34b16-582">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-582">Property</span></span> | <span data-ttu-id="34b16-583">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-583">Description</span></span> | <span data-ttu-id="34b16-584">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="34b16-584">Allowed values</span></span> | <span data-ttu-id="34b16-585">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-585">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-586">Recursieve</span><span class="sxs-lookup"><span data-stu-id="34b16-586">recursive</span></span> |<span data-ttu-id="34b16-587">Hiermee wordt aangegeven of Hallo gegevens recursief is gelezen vanuit Hallo submappen of alleen vanuit de opgegeven map Hallo.</span><span class="sxs-lookup"><span data-stu-id="34b16-587">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="34b16-588">True (standaardwaarde), False</span><span class="sxs-lookup"><span data-stu-id="34b16-588">True (default value), False</span></span> |<span data-ttu-id="34b16-589">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-589">No</span></span> |

#### <a name="example-blobsource"></a><span data-ttu-id="34b16-590">Voorbeeld: BlobSource **</span><span class="sxs-lookup"><span data-stu-id="34b16-590">Example: BlobSource**</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
### <a name="blobsink-in-copy-activity"></a><span data-ttu-id="34b16-591">BlobSink in de kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="34b16-591">BlobSink in Copy Activity</span></span>
<span data-ttu-id="34b16-592">Als u gegevens tooan Azure Blob-opslag kopiëren wilt, stelt u Hallo **type sink** Hallo kopieeractiviteit te**BlobSink**, en opgeven na eigenschappen in Hallo **sink** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-592">If you are copying data tooan Azure Blob Storage, set hello **sink type** of hello copy activity too**BlobSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="34b16-593">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-593">Property</span></span> | <span data-ttu-id="34b16-594">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-594">Description</span></span> | <span data-ttu-id="34b16-595">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="34b16-595">Allowed values</span></span> | <span data-ttu-id="34b16-596">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-596">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-597">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="34b16-597">copyBehavior</span></span> |<span data-ttu-id="34b16-598">Hallo kopie gedrag definieert wanneer Hallo bron BlobSource of bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="34b16-598">Defines hello copy behavior when hello source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="34b16-599"><b>PreserveHierarchy</b>: gehandhaafd Hallo bestandshiërarchie in de doelmap Hallo.</span><span class="sxs-lookup"><span data-stu-id="34b16-599"><b>PreserveHierarchy</b>: preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="34b16-600">Hallo relatieve pad van de bestandsmap toosource bron is identiek toohello relatieve pad van de bestandsmap tootarget doel.</span><span class="sxs-lookup"><span data-stu-id="34b16-600">hello relative path of source file toosource folder is identical toohello relative path of target file tootarget folder.</span></span><br/><br/><span data-ttu-id="34b16-601"><b>FlattenHierarchy</b>: alle bestanden uit de bronmap Hallo zijn in Hallo eerst niveau van de doelmap.</span><span class="sxs-lookup"><span data-stu-id="34b16-601"><b>FlattenHierarchy</b>: all files from hello source folder are in hello first level of target folder.</span></span> <span data-ttu-id="34b16-602">Hallo doelbestanden hebben automatisch gegenereerde naam.</span><span class="sxs-lookup"><span data-stu-id="34b16-602">hello target files have auto generated name.</span></span> <br/><br/><span data-ttu-id="34b16-603"><b>MergeFiles (standaard):</b> alle bestanden uit map Hallo-tooone bronbestand worden samengevoegd.</span><span class="sxs-lookup"><span data-stu-id="34b16-603"><b>MergeFiles (default):</b> merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="34b16-604">Als Hallo bestand/Blob-naam wordt opgegeven, zou Hallo Samengevoegde bestandsnaam Hallo opgegeven name; zijn anders zou worden automatisch gegenereerde naam.</span><span class="sxs-lookup"><span data-stu-id="34b16-604">If hello File/Blob Name is specified, hello merged file name would be hello specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="34b16-605">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-605">No</span></span> |

#### <a name="example-blobsink"></a><span data-ttu-id="34b16-606">Voorbeeld: BlobSink</span><span class="sxs-lookup"><span data-stu-id="34b16-606">Example: BlobSink</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="34b16-607">Zie voor meer informatie [Azure Blob-connector](data-factory-azure-blob-connector.md#copy-activity-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-607">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-data-lake-store"></a><span data-ttu-id="34b16-608">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="34b16-608">Azure Data Lake Store</span></span>

### <a name="linked-service"></a><span data-ttu-id="34b16-609">Gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="34b16-609">Linked service</span></span>
<span data-ttu-id="34b16-610">een Azure Data Lake Store gekoppelde service toodefine, Hallo set Hallo type gekoppelde service te**AzureDataLakeStore**, en opgeven na eigenschappen in Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-610">toodefine an Azure Data Lake Store linked service, set hello type of hello linked service too**AzureDataLakeStore**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="34b16-611">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-611">Property</span></span> | <span data-ttu-id="34b16-612">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-612">Description</span></span> | <span data-ttu-id="34b16-613">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-613">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="34b16-614">type</span><span class="sxs-lookup"><span data-stu-id="34b16-614">type</span></span> | <span data-ttu-id="34b16-615">Hallo type eigenschap moet worden ingesteld op: **AzureDataLakeStore**</span><span class="sxs-lookup"><span data-stu-id="34b16-615">hello type property must be set to: **AzureDataLakeStore**</span></span> | <span data-ttu-id="34b16-616">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-616">Yes</span></span> |
| <span data-ttu-id="34b16-617">dataLakeStoreUri</span><span class="sxs-lookup"><span data-stu-id="34b16-617">dataLakeStoreUri</span></span> | <span data-ttu-id="34b16-618">Geef informatie op over hello Azure Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="34b16-618">Specify information about hello Azure Data Lake Store account.</span></span> <span data-ttu-id="34b16-619">Het is in de volgende indeling Hallo: `https://[accountname].azuredatalakestore.net/webhdfs/v1` of `adl://[accountname].azuredatalakestore.net/`.</span><span class="sxs-lookup"><span data-stu-id="34b16-619">It is in hello following format: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span></span> | <span data-ttu-id="34b16-620">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-620">Yes</span></span> |
| <span data-ttu-id="34b16-621">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="34b16-621">subscriptionId</span></span> | <span data-ttu-id="34b16-622">Azure-abonnement Id toowhich Data Lake Store hoort.</span><span class="sxs-lookup"><span data-stu-id="34b16-622">Azure subscription Id toowhich Data Lake Store belongs.</span></span> | <span data-ttu-id="34b16-623">Vereist voor sink</span><span class="sxs-lookup"><span data-stu-id="34b16-623">Required for sink</span></span> |
| <span data-ttu-id="34b16-624">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="34b16-624">resourceGroupName</span></span> | <span data-ttu-id="34b16-625">Azure resource group name toowhich Data Lake Store hoort.</span><span class="sxs-lookup"><span data-stu-id="34b16-625">Azure resource group name toowhich Data Lake Store belongs.</span></span> | <span data-ttu-id="34b16-626">Vereist voor sink</span><span class="sxs-lookup"><span data-stu-id="34b16-626">Required for sink</span></span> |
| <span data-ttu-id="34b16-627">servicePrincipalId</span><span class="sxs-lookup"><span data-stu-id="34b16-627">servicePrincipalId</span></span> | <span data-ttu-id="34b16-628">Geef Hallo van client-id op.</span><span class="sxs-lookup"><span data-stu-id="34b16-628">Specify hello application's client ID.</span></span> | <span data-ttu-id="34b16-629">Ja (voor verificatie voor service-principal)</span><span class="sxs-lookup"><span data-stu-id="34b16-629">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="34b16-630">servicePrincipalKey</span><span class="sxs-lookup"><span data-stu-id="34b16-630">servicePrincipalKey</span></span> | <span data-ttu-id="34b16-631">De sleutel van de toepassing hello opgeven.</span><span class="sxs-lookup"><span data-stu-id="34b16-631">Specify hello application's key.</span></span> | <span data-ttu-id="34b16-632">Ja (voor verificatie voor service-principal)</span><span class="sxs-lookup"><span data-stu-id="34b16-632">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="34b16-633">Tenant</span><span class="sxs-lookup"><span data-stu-id="34b16-633">tenant</span></span> | <span data-ttu-id="34b16-634">Geef informatie op Hallo tenant (domain name of tenant-ID) in uw toepassing zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="34b16-634">Specify hello tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="34b16-635">U kunt deze ophalen door zwevende Hallo muis in Hallo rechterbovenhoek Hallo Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="34b16-635">You can retrieve it by hovering hello mouse in hello top-right corner of hello Azure portal.</span></span> | <span data-ttu-id="34b16-636">Ja (voor verificatie voor service-principal)</span><span class="sxs-lookup"><span data-stu-id="34b16-636">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="34b16-637">Autorisatie</span><span class="sxs-lookup"><span data-stu-id="34b16-637">authorization</span></span> | <span data-ttu-id="34b16-638">Klik op **autoriseren** knop in Hallo **Data Factory-Editor** en voer uw referenties waarmee eigenschap toothis Hallo automatisch gegenereerde autorisatie-URL worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="34b16-638">Click **Authorize** button in hello **Data Factory Editor** and enter your credential that assigns hello auto-generated authorization URL toothis property.</span></span> | <span data-ttu-id="34b16-639">Ja (voor verificatie van gebruikersreferenties)</span><span class="sxs-lookup"><span data-stu-id="34b16-639">Yes (for user credential authentication)</span></span>|
| <span data-ttu-id="34b16-640">sessie-id</span><span class="sxs-lookup"><span data-stu-id="34b16-640">sessionId</span></span> | <span data-ttu-id="34b16-641">OAuth-sessie-id van Hallo OAuth-autorisatie-sessie.</span><span class="sxs-lookup"><span data-stu-id="34b16-641">OAuth session id from hello OAuth authorization session.</span></span> <span data-ttu-id="34b16-642">Elke sessie-id is uniek en kan slechts eenmaal worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-642">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="34b16-643">Deze instelling wordt automatisch gegenereerd wanneer u Data Factory-Editor.</span><span class="sxs-lookup"><span data-stu-id="34b16-643">This setting is automatically generated when you use Data Factory Editor.</span></span> | <span data-ttu-id="34b16-644">Ja (voor verificatie van gebruikersreferenties)</span><span class="sxs-lookup"><span data-stu-id="34b16-644">Yes (for user credential authentication)</span></span> |

#### <a name="example-using-service-principal-authentication"></a><span data-ttu-id="34b16-645">Voorbeeld: met behulp van verificatie van de service-principal</span><span class="sxs-lookup"><span data-stu-id="34b16-645">Example: using service principal authentication</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info. Example: microsoft.onmicrosoft.com>"
        }
    }
}
```

#### <a name="example-using-user-credential-authentication"></a><span data-ttu-id="34b16-646">Voorbeeld: met behulp van verificatie van gebruikersreferenties</span><span class="sxs-lookup"><span data-stu-id="34b16-646">Example: using user credential authentication</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

<span data-ttu-id="34b16-647">Zie voor meer informatie [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#linked-service-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-647">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="34b16-648">Gegevensset</span><span class="sxs-lookup"><span data-stu-id="34b16-648">Dataset</span></span>
<span data-ttu-id="34b16-649">toodefine een gegevensset Azure Data Lake Store set Hallo **type** van Hallo gegevensset te**AzureDataLakeStore**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties**sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-649">toodefine an Azure Data Lake Store dataset, set hello **type** of hello dataset too**AzureDataLakeStore**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="34b16-650">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-650">Property</span></span> | <span data-ttu-id="34b16-651">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-651">Description</span></span> | <span data-ttu-id="34b16-652">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-652">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="34b16-653">folderPath</span><span class="sxs-lookup"><span data-stu-id="34b16-653">folderPath</span></span> |<span data-ttu-id="34b16-654">Pad toohello container en map in hello Azure Data Lake opslaan.</span><span class="sxs-lookup"><span data-stu-id="34b16-654">Path toohello container and folder in hello Azure Data Lake store.</span></span> |<span data-ttu-id="34b16-655">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-655">Yes</span></span> |
| <span data-ttu-id="34b16-656">fileName</span><span class="sxs-lookup"><span data-stu-id="34b16-656">fileName</span></span> |<span data-ttu-id="34b16-657">Naam van bestand Hallo in hello Azure Data Lake store.</span><span class="sxs-lookup"><span data-stu-id="34b16-657">Name of hello file in hello Azure Data Lake store.</span></span> <span data-ttu-id="34b16-658">Bestandsnaam is optioneel en is hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="34b16-658">fileName is optional and case-sensitive.</span></span> <br/><br/><span data-ttu-id="34b16-659">Als u een filename opgeeft, werkt Hallo activiteit (inclusief kopiëren) op Hallo specifiek bestand.</span><span class="sxs-lookup"><span data-stu-id="34b16-659">If you specify a filename, hello activity (including Copy) works on hello specific file.</span></span><br/><br/><span data-ttu-id="34b16-660">Bestandsnaam is opgegeven, bevat kopiëren alle bestanden in Hallo folderPath voor invoergegevensset.</span><span class="sxs-lookup"><span data-stu-id="34b16-660">When fileName is not specified, Copy includes all files in hello folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="34b16-661">Wanneer fileName niet voor een uitvoergegevensset opgegeven is, Hallo-naam van Hallo gegenereerd bestand in Hallo volgt deze indeling zou worden: gegevens. <Guid>.txt (voorbeeld:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="34b16-661">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="34b16-662">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-662">No</span></span> |
| <span data-ttu-id="34b16-663">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="34b16-663">partitionedBy</span></span> |<span data-ttu-id="34b16-664">partitionedBy is een optionele eigenschap.</span><span class="sxs-lookup"><span data-stu-id="34b16-664">partitionedBy is an optional property.</span></span> <span data-ttu-id="34b16-665">Kunt u deze toospecify een dynamische folderPath en de bestandsnaam voor de reeksgegevens.</span><span class="sxs-lookup"><span data-stu-id="34b16-665">You can use it toospecify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="34b16-666">FolderPath kan bijvoorbeeld parameters worden gebruikt voor elk uur van gegevens.</span><span class="sxs-lookup"><span data-stu-id="34b16-666">For example, folderPath can be parameterized for every hour of data.</span></span> |<span data-ttu-id="34b16-667">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-667">No</span></span> |
| <span data-ttu-id="34b16-668">Indeling</span><span class="sxs-lookup"><span data-stu-id="34b16-668">format</span></span> | <span data-ttu-id="34b16-669">Hallo na indelingstypen worden ondersteund: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="34b16-669">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="34b16-670">Set Hallo **type** eigenschap onder indeling tooone van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="34b16-670">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="34b16-671">Zie voor meer informatie [tekstindeling](data-factory-supported-file-and-compression-formats.md#text-format), [Json-indeling](data-factory-supported-file-and-compression-formats.md#json-format), [Avro-indeling](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc indeling](data-factory-supported-file-and-compression-formats.md#orc-format), en [parketvloeren indeling](data-factory-supported-file-and-compression-formats.md#parquet-format) secties.</span><span class="sxs-lookup"><span data-stu-id="34b16-671">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="34b16-672">Als u wilt dat te**kopiëren van bestanden als-is** tussen bestandsgebaseerde winkels (binaire kopiëren) Hallo indeling sectie in beide definities invoer en uitvoer gegevensset overslaan.</span><span class="sxs-lookup"><span data-stu-id="34b16-672">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="34b16-673">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-673">No</span></span> |
| <span data-ttu-id="34b16-674">Compressie</span><span class="sxs-lookup"><span data-stu-id="34b16-674">compression</span></span> | <span data-ttu-id="34b16-675">Hallo-type en compressieniveau voor Hallo gegevens opgeven.</span><span class="sxs-lookup"><span data-stu-id="34b16-675">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="34b16-676">Ondersteunde typen zijn: **GZip**, **Deflate**, **BZip2**, en **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="34b16-676">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="34b16-677">Ondersteunde niveaus: **optimale** en **snelst**.</span><span class="sxs-lookup"><span data-stu-id="34b16-677">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="34b16-678">Zie voor meer informatie [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="34b16-678">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="34b16-679">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-679">No</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-680">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-680">Example</span></span>
```json
{
    "name": "AzureDataLakeStoreInput",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="34b16-681">Zie voor meer informatie [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#dataset-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-681">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#dataset-properties) article.</span></span> 

### <a name="azure-data-lake-store-source-in-copy-activity"></a><span data-ttu-id="34b16-682">Azure Data Lake Store-bron in de kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="34b16-682">Azure Data Lake Store Source in Copy Activity</span></span>
<span data-ttu-id="34b16-683">Als u gegevens uit een Azure Data Lake Store kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**AzureDataLakeStoreSource**, en opgeven na eigenschappen in Hallo **bron**  sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-683">If you are copying data from an Azure Data Lake Store, set hello **source type** of hello copy activity too**AzureDataLakeStoreSource**, and specify following properties in hello **source** section:</span></span>

<span data-ttu-id="34b16-684">**AzureDataLakeStoreSource** ondersteunt de volgende eigenschappen Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-684">**AzureDataLakeStoreSource** supports hello following properties **typeProperties** section:</span></span>

| <span data-ttu-id="34b16-685">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-685">Property</span></span> | <span data-ttu-id="34b16-686">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-686">Description</span></span> | <span data-ttu-id="34b16-687">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="34b16-687">Allowed values</span></span> | <span data-ttu-id="34b16-688">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-688">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-689">Recursieve</span><span class="sxs-lookup"><span data-stu-id="34b16-689">recursive</span></span> |<span data-ttu-id="34b16-690">Hiermee wordt aangegeven of Hallo gegevens recursief is gelezen vanuit Hallo submappen of alleen vanuit de opgegeven map Hallo.</span><span class="sxs-lookup"><span data-stu-id="34b16-690">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="34b16-691">True (standaardwaarde), False</span><span class="sxs-lookup"><span data-stu-id="34b16-691">True (default value), False</span></span> |<span data-ttu-id="34b16-692">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-692">No</span></span> |

#### <a name="example-azuredatalakestoresource"></a><span data-ttu-id="34b16-693">Voorbeeld: AzureDataLakeStoreSource</span><span class="sxs-lookup"><span data-stu-id="34b16-693">Example: AzureDataLakeStoreSource</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureDakeLaketoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureDataLakeStoreInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "AzureDataLakeStoreSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="34b16-694">Zie voor meer informatie [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-694">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span></span>

### <a name="azure-data-lake-store-sink-in-copy-activity"></a><span data-ttu-id="34b16-695">Azure Data Lake Store Sink in de kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="34b16-695">Azure Data Lake Store Sink in Copy Activity</span></span>
<span data-ttu-id="34b16-696">Als u gegevens tooan Azure Data Lake Store kopieert, stelt u Hallo **type sink** Hallo kopieeractiviteit te**AzureDataLakeStoreSink**, en opgeven na eigenschappen in Hallo **sink**sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-696">If you are copying data tooan Azure Data Lake Store, set hello **sink type** of hello copy activity too**AzureDataLakeStoreSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="34b16-697">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-697">Property</span></span> | <span data-ttu-id="34b16-698">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-698">Description</span></span> | <span data-ttu-id="34b16-699">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="34b16-699">Allowed values</span></span> | <span data-ttu-id="34b16-700">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-700">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-701">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="34b16-701">copyBehavior</span></span> |<span data-ttu-id="34b16-702">Hiermee geeft u Hallo kopie gedrag.</span><span class="sxs-lookup"><span data-stu-id="34b16-702">Specifies hello copy behavior.</span></span> |<span data-ttu-id="34b16-703"><b>PreserveHierarchy</b>: gehandhaafd Hallo bestandshiërarchie in de doelmap Hallo.</span><span class="sxs-lookup"><span data-stu-id="34b16-703"><b>PreserveHierarchy</b>: preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="34b16-704">Hallo relatieve pad van de bestandsmap toosource bron is identiek toohello relatieve pad van de bestandsmap tootarget doel.</span><span class="sxs-lookup"><span data-stu-id="34b16-704">hello relative path of source file toosource folder is identical toohello relative path of target file tootarget folder.</span></span><br/><br/><span data-ttu-id="34b16-705"><b>FlattenHierarchy</b>: alle bestanden uit de bronmap Hallo worden gemaakt in Hallo eerste niveau van de doelmap.</span><span class="sxs-lookup"><span data-stu-id="34b16-705"><b>FlattenHierarchy</b>: all files from hello source folder are created in hello first level of target folder.</span></span> <span data-ttu-id="34b16-706">Hallo doelbestanden worden gemaakt met de automatisch gegenereerde naam.</span><span class="sxs-lookup"><span data-stu-id="34b16-706">hello target files are created with auto generated name.</span></span><br/><br/><span data-ttu-id="34b16-707"><b>MergeFiles</b>: alle bestanden uit map Hallo-tooone bronbestand worden samengevoegd.</span><span class="sxs-lookup"><span data-stu-id="34b16-707"><b>MergeFiles</b>: merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="34b16-708">Als Hallo bestand/Blob-naam wordt opgegeven, zou Hallo Samengevoegde bestandsnaam Hallo opgegeven name; zijn anders zou worden automatisch gegenereerde naam.</span><span class="sxs-lookup"><span data-stu-id="34b16-708">If hello File/Blob Name is specified, hello merged file name would be hello specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="34b16-709">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-709">No</span></span> |

#### <a name="example-azuredatalakestoresink"></a><span data-ttu-id="34b16-710">Voorbeeld: AzureDataLakeStoreSink</span><span class="sxs-lookup"><span data-stu-id="34b16-710">Example: AzureDataLakeStoreSink</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoDataLake",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureDataLakeStoreOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "AzureDataLakeStoreSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="34b16-711">Zie voor meer informatie [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-711">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-cosmos-db"></a><span data-ttu-id="34b16-712">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="34b16-712">Azure Cosmos DB</span></span>  

### <a name="linked-service"></a><span data-ttu-id="34b16-713">Gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="34b16-713">Linked service</span></span>
<span data-ttu-id="34b16-714">een Cosmos Azure DB toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**DocumentDb**, en opgeven na eigenschappen in Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-714">toodefine an Azure Cosmos DB linked service, set hello **type** of hello linked service too**DocumentDb**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="34b16-715">**Eigenschap**</span><span class="sxs-lookup"><span data-stu-id="34b16-715">**Property**</span></span> | <span data-ttu-id="34b16-716">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="34b16-716">**Description**</span></span> | <span data-ttu-id="34b16-717">**Vereist**</span><span class="sxs-lookup"><span data-stu-id="34b16-717">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-718">connectionString</span><span class="sxs-lookup"><span data-stu-id="34b16-718">connectionString</span></span> |<span data-ttu-id="34b16-719">Geef informatie nodig tooconnect tooAzure Cosmos-DB-database.</span><span class="sxs-lookup"><span data-stu-id="34b16-719">Specify information needed tooconnect tooAzure Cosmos DB database.</span></span> |<span data-ttu-id="34b16-720">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-720">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-721">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-721">Example</span></span>

```json
{
    "name": "CosmosDBLinkedService",
    "properties": {
        "type": "DocumentDb",
        "typeProperties": {
            "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
        }
    }
}
```
<span data-ttu-id="34b16-722">Zie voor meer informatie [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#linked-service-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-722">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="34b16-723">Gegevensset</span><span class="sxs-lookup"><span data-stu-id="34b16-723">Dataset</span></span>
<span data-ttu-id="34b16-724">toodefine een gegevensset Azure Cosmos DB set Hallo **type** van Hallo gegevensset te**DocumentDbCollection**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-724">toodefine an Azure Cosmos DB dataset, set hello **type** of hello dataset too**DocumentDbCollection**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="34b16-725">**Eigenschap**</span><span class="sxs-lookup"><span data-stu-id="34b16-725">**Property**</span></span> | <span data-ttu-id="34b16-726">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="34b16-726">**Description**</span></span> | <span data-ttu-id="34b16-727">**Vereist**</span><span class="sxs-lookup"><span data-stu-id="34b16-727">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-728">CollectionName</span><span class="sxs-lookup"><span data-stu-id="34b16-728">collectionName</span></span> |<span data-ttu-id="34b16-729">Naam van hello Azure DB die Cosmos-verzameling.</span><span class="sxs-lookup"><span data-stu-id="34b16-729">Name of hello Azure Cosmos DB collection.</span></span> |<span data-ttu-id="34b16-730">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-730">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-731">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-731">Example</span></span>

```json
{
    "name": "PersonCosmosDBTable",
    "properties": {
        "type": "DocumentDbCollection",
        "linkedServiceName": "CosmosDBLinkedService",
        "typeProperties": {
            "collectionName": "Person"
        },
        "external": true,
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```
<span data-ttu-id="34b16-732">Zie voor meer informatie [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#dataset-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-732">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#dataset-properties) article.</span></span>

### <a name="azure-cosmos-db-collection-source-in-copy-activity"></a><span data-ttu-id="34b16-733">Azure Cosmos DB verzameling bron in de kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="34b16-733">Azure Cosmos DB Collection Source in Copy Activity</span></span>
<span data-ttu-id="34b16-734">Als u gegevens uit een Cosmos Azure DB kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**DocumentDbCollectionSource**, en opgeven na eigenschappen in Hallo **bron** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-734">If you are copying data from an Azure Cosmos DB, set hello **source type** of hello copy activity too**DocumentDbCollectionSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="34b16-735">**Eigenschap**</span><span class="sxs-lookup"><span data-stu-id="34b16-735">**Property**</span></span> | <span data-ttu-id="34b16-736">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="34b16-736">**Description**</span></span> | <span data-ttu-id="34b16-737">**Toegestane waarden**</span><span class="sxs-lookup"><span data-stu-id="34b16-737">**Allowed values**</span></span> | <span data-ttu-id="34b16-738">**Vereist**</span><span class="sxs-lookup"><span data-stu-id="34b16-738">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-739">query</span><span class="sxs-lookup"><span data-stu-id="34b16-739">query</span></span> |<span data-ttu-id="34b16-740">Geef gegevens op Hallo query tooread.</span><span class="sxs-lookup"><span data-stu-id="34b16-740">Specify hello query tooread data.</span></span> |<span data-ttu-id="34b16-741">Queryreeks wordt ondersteund door Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="34b16-741">Query string supported by Azure Cosmos DB.</span></span> <br/><br/><span data-ttu-id="34b16-742">Voorbeeld:`SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span><span class="sxs-lookup"><span data-stu-id="34b16-742">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span></span> |<span data-ttu-id="34b16-743">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-743">No</span></span> <br/><br/><span data-ttu-id="34b16-744">Als niet wordt opgegeven, Hallo SQL-instructie die is uitgevoerd:`select <columns defined in structure> from mycollection`</span><span class="sxs-lookup"><span data-stu-id="34b16-744">If not specified, hello SQL statement that is executed: `select <columns defined in structure> from mycollection`</span></span> |
| <span data-ttu-id="34b16-745">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="34b16-745">nestingSeparator</span></span> |<span data-ttu-id="34b16-746">Speciaal teken tooindicate dat document Hallo is genest</span><span class="sxs-lookup"><span data-stu-id="34b16-746">Special character tooindicate that hello document is nested</span></span> |<span data-ttu-id="34b16-747">Willekeurig teken.</span><span class="sxs-lookup"><span data-stu-id="34b16-747">Any character.</span></span> <br/><br/><span data-ttu-id="34b16-748">Azure Cosmos-database is een NoSQL-opslagplaats voor JSON-documenten, waarbij geneste structuren zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="34b16-748">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="34b16-749">Azure Data Factory kunt toodenote gebruikershiërarchie via nestingSeparator die "."</span><span class="sxs-lookup"><span data-stu-id="34b16-749">Azure Data Factory enables user toodenote hierarchy via nestingSeparator, which is “.”</span></span> <span data-ttu-id="34b16-750">in hello bovenstaande voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="34b16-750">in hello above examples.</span></span> <span data-ttu-id="34b16-751">Met Hallo scheidingsteken, genereert kopieeractiviteit Hallo Hallo "Name" object met drie onderliggende elementen eerste, middelste en laatste, volgens too"Name.First ', 'Name.Middle' en 'Name.Last' in hello tabeldefinitie.</span><span class="sxs-lookup"><span data-stu-id="34b16-751">With hello separator, hello copy activity will generate hello “Name” object with three children elements First, Middle and Last, according too“Name.First”, “Name.Middle” and “Name.Last” in hello table definition.</span></span> |<span data-ttu-id="34b16-752">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-752">No</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-753">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-753">Example</span></span>

```json
{
    "name": "DocDbToBlobPipeline",
    "properties": {
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "DocumentDbCollectionSource",
                    "query": "SELECT Person.Id, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person",
                    "nestingSeparator": "."
                },
                "sink": {
                    "type": "BlobSink",
                    "blobWriterAddHeader": true,
                    "writeBatchSize": 1000,
                    "writeBatchTimeout": "00:00:59"
                }
            },
            "inputs": [{
                "name": "PersonCosmosDBTable"
            }],
            "outputs": [{
                "name": "PersonBlobTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromCosmosDbToBlob"
        }],
        "start": "2016-04-01T00:00:00",
        "end": "2016-04-02T00:00:00"
    }
}
```

### <a name="azure-cosmos-db-collection-sink-in-copy-activity"></a><span data-ttu-id="34b16-754">Azure Cosmos DB verzameling Sink in de kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="34b16-754">Azure Cosmos DB Collection Sink in Copy Activity</span></span>
<span data-ttu-id="34b16-755">Als u gegevens tooAzure Cosmos DB kopieert, stelt u Hallo **type sink** Hallo kopieeractiviteit te**DocumentDbCollectionSink**, en opgeven na eigenschappen in Hallo **sink**sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-755">If you are copying data tooAzure Cosmos DB, set hello **sink type** of hello copy activity too**DocumentDbCollectionSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="34b16-756">**Eigenschap**</span><span class="sxs-lookup"><span data-stu-id="34b16-756">**Property**</span></span> | <span data-ttu-id="34b16-757">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="34b16-757">**Description**</span></span> | <span data-ttu-id="34b16-758">**Toegestane waarden**</span><span class="sxs-lookup"><span data-stu-id="34b16-758">**Allowed values**</span></span> | <span data-ttu-id="34b16-759">**Vereist**</span><span class="sxs-lookup"><span data-stu-id="34b16-759">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-760">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="34b16-760">nestingSeparator</span></span> |<span data-ttu-id="34b16-761">Er is een speciaal teken in Hallo bron kolom naam tooindicate dat document genest nodig.</span><span class="sxs-lookup"><span data-stu-id="34b16-761">A special character in hello source column name tooindicate that nested document is needed.</span></span> <br/><br/><span data-ttu-id="34b16-762">Zoals hierboven: `Name.First` in Hallo-uitvoer produceert tabel Hallo JSON-structuur in Hallo Cosmos DB document te volgen:</span><span class="sxs-lookup"><span data-stu-id="34b16-762">For example above: `Name.First` in hello output table produces hello following JSON structure in hello Cosmos DB document:</span></span><br/><br/><span data-ttu-id="34b16-763">"Name": {</span><span class="sxs-lookup"><span data-stu-id="34b16-763">"Name": {</span></span><br/>    <span data-ttu-id="34b16-764">' First ': 'John'</span><span class="sxs-lookup"><span data-stu-id="34b16-764">"First": "John"</span></span><br/><span data-ttu-id="34b16-765">},</span><span class="sxs-lookup"><span data-stu-id="34b16-765">},</span></span> |<span data-ttu-id="34b16-766">Teken gebruikte tooseparate aantal geneste niveaus.</span><span class="sxs-lookup"><span data-stu-id="34b16-766">Character that is used tooseparate nesting levels.</span></span><br/><br/><span data-ttu-id="34b16-767">Standaardwaarde is `.` (punt).</span><span class="sxs-lookup"><span data-stu-id="34b16-767">Default value is `.` (dot).</span></span> |<span data-ttu-id="34b16-768">Teken gebruikte tooseparate aantal geneste niveaus.</span><span class="sxs-lookup"><span data-stu-id="34b16-768">Character that is used tooseparate nesting levels.</span></span> <br/><br/><span data-ttu-id="34b16-769">Standaardwaarde is `.` (punt).</span><span class="sxs-lookup"><span data-stu-id="34b16-769">Default value is `.` (dot).</span></span> |
| <span data-ttu-id="34b16-770">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="34b16-770">writeBatchSize</span></span> |<span data-ttu-id="34b16-771">Aantal parallelle aanvragen tooAzure Cosmos DB service toocreate documenten.</span><span class="sxs-lookup"><span data-stu-id="34b16-771">Number of parallel requests tooAzure Cosmos DB service toocreate documents.</span></span><br/><br/><span data-ttu-id="34b16-772">Bij het kopiëren van gegevens van Azure DB die Cosmos met behulp van deze eigenschap kunt u de prestaties van Hallo verfijnen.</span><span class="sxs-lookup"><span data-stu-id="34b16-772">You can fine-tune hello performance when copying data to/from Azure Cosmos DB by using this property.</span></span> <span data-ttu-id="34b16-773">U kunt een betere prestaties verwachten wanneer u writeBatchSize verhogen omdat meer parallelle aanvragen tooAzure Cosmos DB worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="34b16-773">You can expect a better performance when you increase writeBatchSize because more parallel requests tooAzure Cosmos DB are sent.</span></span> <span data-ttu-id="34b16-774">Maar u moet tooavoid beperking die kunnen genereert fout het Hallo-bericht: 'Vragen snelheid is groot'.</span><span class="sxs-lookup"><span data-stu-id="34b16-774">However you’ll need tooavoid throttling that can throw hello error message: "Request rate is large".</span></span><br/><br/><span data-ttu-id="34b16-775">Beperking wordt bepaald door een aantal factoren, onder andere de grootte van documenten, aantal termen in documenten, indexeren beleid van de doelverzameling, enzovoort. Voor het kopiëren van, kunt u een betere verzameling (bijvoorbeeld S3) toohave Hallo meeste doorvoer beschikbaar (2500 aanvragen eenheden/seconde).</span><span class="sxs-lookup"><span data-stu-id="34b16-775">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (for example, S3) toohave hello most throughput available (2,500 request units/second).</span></span> |<span data-ttu-id="34b16-776">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="34b16-776">Integer</span></span> |<span data-ttu-id="34b16-777">Nee (standaard: 5)</span><span class="sxs-lookup"><span data-stu-id="34b16-777">No (default: 5)</span></span> |
| <span data-ttu-id="34b16-778">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="34b16-778">writeBatchTimeout</span></span> |<span data-ttu-id="34b16-779">Wachttijd voor Hallo bewerking toocomplete voordat een time-out optreedt.</span><span class="sxs-lookup"><span data-stu-id="34b16-779">Wait time for hello operation toocomplete before it times out.</span></span> |<span data-ttu-id="34b16-780">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="34b16-780">timespan</span></span><br/><br/> <span data-ttu-id="34b16-781">Voorbeeld: "00: 30:00 ' (30 minuten).</span><span class="sxs-lookup"><span data-stu-id="34b16-781">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="34b16-782">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-782">No</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-783">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-783">Example</span></span>

```json
{
    "name": "BlobToDocDbPipeline",
    "properties": {
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "DocumentDbCollectionSink",
                    "nestingSeparator": ".",
                    "writeBatchSize": 2,
                    "writeBatchTimeout": "00:00:00"
                },
                "translator": {
                    "type": "TabularTranslator",
                    "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, title: aaaTitle, Suffix: Suffix"
                }
            },
            "inputs": [{
                "name": "PersonBlobTableIn"
            }],
            "outputs": [{
                "name": "PersonCosmosDbTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromBlobToCosmosDb"
        }],
        "start": "2016-04-14T00:00:00",
        "end": "2016-04-15T00:00:00"
    }
}
```

<span data-ttu-id="34b16-784">Zie voor meer informatie [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#copy-activity-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-784">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#copy-activity-properties) article.</span></span>

## <a name="azure-sql-database"></a><span data-ttu-id="34b16-785">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="34b16-785">Azure SQL Database</span></span>

### <a name="linked-service"></a><span data-ttu-id="34b16-786">Gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="34b16-786">Linked service</span></span>
<span data-ttu-id="34b16-787">een Azure SQL Database toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**AzureSqlDatabase**, en opgeven na eigenschappen in Hallo **typeProperties**sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-787">toodefine an Azure SQL Database linked service, set hello **type** of hello linked service too**AzureSqlDatabase**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="34b16-788">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-788">Property</span></span> | <span data-ttu-id="34b16-789">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-789">Description</span></span> | <span data-ttu-id="34b16-790">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-790">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-791">connectionString</span><span class="sxs-lookup"><span data-stu-id="34b16-791">connectionString</span></span> |<span data-ttu-id="34b16-792">Geef informatie tooconnect toohello Azure SQL Database-exemplaar voor de eigenschap connectionString Hallo nodig.</span><span class="sxs-lookup"><span data-stu-id="34b16-792">Specify information needed tooconnect toohello Azure SQL Database instance for hello connectionString property.</span></span> |<span data-ttu-id="34b16-793">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-793">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-794">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-794">Example</span></span>
```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="34b16-795">Zie voor meer informatie [Azure SQL-connector](data-factory-azure-sql-connector.md#linked-service-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-795">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="34b16-796">Gegevensset</span><span class="sxs-lookup"><span data-stu-id="34b16-796">Dataset</span></span>
<span data-ttu-id="34b16-797">toodefine een gegevensset Azure SQL Database set Hallo **type** van Hallo gegevensset te**AzureSqlTable**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-797">toodefine an Azure SQL Database dataset, set hello **type** of hello dataset too**AzureSqlTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="34b16-798">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-798">Property</span></span> | <span data-ttu-id="34b16-799">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-799">Description</span></span> | <span data-ttu-id="34b16-800">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-800">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-801">tableName</span><span class="sxs-lookup"><span data-stu-id="34b16-801">tableName</span></span> |<span data-ttu-id="34b16-802">De naam van het Hallo-tabel of weergave in hello Azure SQL Database-exemplaar waarnaar de gekoppelde service verwijst.</span><span class="sxs-lookup"><span data-stu-id="34b16-802">Name of hello table or view in hello Azure SQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="34b16-803">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-803">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-804">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-804">Example</span></span>

```json
{
    "name": "AzureSqlInput",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="34b16-805">Zie voor meer informatie [Azure SQL-connector](data-factory-azure-sql-connector.md#dataset-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-805">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-source-in-copy-activity"></a><span data-ttu-id="34b16-806">SQL-bron in de kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="34b16-806">SQL Source in Copy Activity</span></span>
<span data-ttu-id="34b16-807">Als u gegevens uit een Azure SQL Database kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**SqlSource**, en opgeven na eigenschappen in Hallo **bron** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-807">If you are copying data from an Azure SQL Database, set hello **source type** of hello copy activity too**SqlSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="34b16-808">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-808">Property</span></span> | <span data-ttu-id="34b16-809">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-809">Description</span></span> | <span data-ttu-id="34b16-810">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="34b16-810">Allowed values</span></span> | <span data-ttu-id="34b16-811">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-811">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-812">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="34b16-812">sqlReaderQuery</span></span> |<span data-ttu-id="34b16-813">Hallo aangepaste query tooread gegevens worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-813">Use hello custom query tooread data.</span></span> |<span data-ttu-id="34b16-814">SQL-query-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="34b16-814">SQL query string.</span></span> <span data-ttu-id="34b16-815">Voorbeeld: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="34b16-815">Example: `select * from MyTable`.</span></span> |<span data-ttu-id="34b16-816">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-816">No</span></span> |
| <span data-ttu-id="34b16-817">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="34b16-817">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="34b16-818">Naam van Hallo opgeslagen procedure die gegevens uit Hallo brontabel leest.</span><span class="sxs-lookup"><span data-stu-id="34b16-818">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="34b16-819">Naam van Hallo opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="34b16-819">Name of hello stored procedure.</span></span> |<span data-ttu-id="34b16-820">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-820">No</span></span> |
| <span data-ttu-id="34b16-821">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="34b16-821">storedProcedureParameters</span></span> |<span data-ttu-id="34b16-822">Parameters voor Hallo opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="34b16-822">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="34b16-823">Naam/waarde-paren.</span><span class="sxs-lookup"><span data-stu-id="34b16-823">Name/value pairs.</span></span> <span data-ttu-id="34b16-824">Namen en hoofdlettergebruik van parameters moeten overeenkomen met Hallo namen en hoofdlettergebruik van Hallo opgeslagen procedureparameters.</span><span class="sxs-lookup"><span data-stu-id="34b16-824">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="34b16-825">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-825">No</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-826">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-826">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="34b16-827">Zie voor meer informatie [Azure SQL-connector](data-factory-azure-sql-connector.md#copy-activity-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-827">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-sink-in-copy-activity"></a><span data-ttu-id="34b16-828">SQL-Sink in de kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="34b16-828">SQL Sink in Copy Activity</span></span>
<span data-ttu-id="34b16-829">Als u gegevens tooAzure SQL-Database kopiëren wilt, stelt u Hallo **type sink** Hallo kopieeractiviteit te**SqlSink**, en opgeven na eigenschappen in Hallo **sink** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-829">If you are copying data tooAzure SQL Database, set hello **sink type** of hello copy activity too**SqlSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="34b16-830">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-830">Property</span></span> | <span data-ttu-id="34b16-831">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-831">Description</span></span> | <span data-ttu-id="34b16-832">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="34b16-832">Allowed values</span></span> | <span data-ttu-id="34b16-833">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-833">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-834">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="34b16-834">writeBatchTimeout</span></span> |<span data-ttu-id="34b16-835">Wachttijd voor Hallo batch insert-bewerking toocomplete voordat een time-out optreedt.</span><span class="sxs-lookup"><span data-stu-id="34b16-835">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="34b16-836">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="34b16-836">timespan</span></span><br/><br/> <span data-ttu-id="34b16-837">Voorbeeld: "00: 30:00 ' (30 minuten).</span><span class="sxs-lookup"><span data-stu-id="34b16-837">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="34b16-838">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-838">No</span></span> |
| <span data-ttu-id="34b16-839">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="34b16-839">writeBatchSize</span></span> |<span data-ttu-id="34b16-840">Voegt de gegevens in SQL-tabel Hallo wanneer Hallo buffergrootte writeBatchSize bereikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-840">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="34b16-841">Geheel getal (aantal rijen)</span><span class="sxs-lookup"><span data-stu-id="34b16-841">Integer (number of rows)</span></span> |<span data-ttu-id="34b16-842">Nee (standaard: 10000)</span><span class="sxs-lookup"><span data-stu-id="34b16-842">No (default: 10000)</span></span> |
| <span data-ttu-id="34b16-843">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="34b16-843">sqlWriterCleanupScript</span></span> |<span data-ttu-id="34b16-844">Geef een query voor de Kopieeractiviteit tooexecute zodat de gegevens van een bepaald segment wordt opgeschoond.</span><span class="sxs-lookup"><span data-stu-id="34b16-844">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="34b16-845">Een query-instructie.</span><span class="sxs-lookup"><span data-stu-id="34b16-845">A query statement.</span></span> |<span data-ttu-id="34b16-846">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-846">No</span></span> |
| <span data-ttu-id="34b16-847">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="34b16-847">sliceIdentifierColumnName</span></span> |<span data-ttu-id="34b16-848">Geef de naam van een kolom voor de Kopieeractiviteit toofill met segment-ID automatisch gegenereerd en die is gebruikt tooclean van gegevens van een bepaald segment wanneer opnieuw uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="34b16-848">Specify a column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="34b16-849">De naam van de kolom van een kolom met gegevenstype binary(32).</span><span class="sxs-lookup"><span data-stu-id="34b16-849">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="34b16-850">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-850">No</span></span> |
| <span data-ttu-id="34b16-851">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="34b16-851">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="34b16-852">Naam van Hallo opgeslagen procedure die upserts (updates/INSERT) gegevens in de doeltabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="34b16-852">Name of hello stored procedure that upserts (updates/inserts) data into hello target table.</span></span> |<span data-ttu-id="34b16-853">Naam van Hallo opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="34b16-853">Name of hello stored procedure.</span></span> |<span data-ttu-id="34b16-854">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-854">No</span></span> |
| <span data-ttu-id="34b16-855">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="34b16-855">storedProcedureParameters</span></span> |<span data-ttu-id="34b16-856">Parameters voor Hallo opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="34b16-856">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="34b16-857">Naam/waarde-paren.</span><span class="sxs-lookup"><span data-stu-id="34b16-857">Name/value pairs.</span></span> <span data-ttu-id="34b16-858">Namen en hoofdlettergebruik van parameters moeten overeenkomen met Hallo namen en hoofdlettergebruik van Hallo opgeslagen procedureparameters.</span><span class="sxs-lookup"><span data-stu-id="34b16-858">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="34b16-859">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-859">No</span></span> |
| <span data-ttu-id="34b16-860">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="34b16-860">sqlWriterTableType</span></span> |<span data-ttu-id="34b16-861">Geef een tabel type naam toobe in Hallo opgeslagen procedure gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-861">Specify a table type name toobe used in hello stored procedure.</span></span> <span data-ttu-id="34b16-862">Kopieeractiviteit beschikbaar Hallo-gegevens worden verplaatst in een tijdelijke tabel met dit tabeltype.</span><span class="sxs-lookup"><span data-stu-id="34b16-862">Copy activity makes hello data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="34b16-863">Opgeslagen procedurecode kunt Hallo gegevens wordt gekopieerd met de bestaande gegevens vervolgens samenvoegen.</span><span class="sxs-lookup"><span data-stu-id="34b16-863">Stored procedure code can then merge hello data being copied with existing data.</span></span> |<span data-ttu-id="34b16-864">Een typenaam van de tabel.</span><span class="sxs-lookup"><span data-stu-id="34b16-864">A table type name.</span></span> |<span data-ttu-id="34b16-865">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-865">No</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-866">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-866">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="34b16-867">Zie voor meer informatie [Azure SQL-connector](data-factory-azure-sql-connector.md#copy-activity-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-867">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-sql-data-warehouse"></a><span data-ttu-id="34b16-868">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="34b16-868">Azure SQL Data Warehouse</span></span>

### <a name="linked-service"></a><span data-ttu-id="34b16-869">Gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="34b16-869">Linked service</span></span>
<span data-ttu-id="34b16-870">een Azure SQL Data Warehouse toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**AzureSqlDW**, en opgeven na eigenschappen in Hallo **typeProperties**sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-870">toodefine an Azure SQL Data Warehouse linked service, set hello **type** of hello linked service too**AzureSqlDW**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="34b16-871">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-871">Property</span></span> | <span data-ttu-id="34b16-872">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-872">Description</span></span> | <span data-ttu-id="34b16-873">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-873">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-874">connectionString</span><span class="sxs-lookup"><span data-stu-id="34b16-874">connectionString</span></span> |<span data-ttu-id="34b16-875">Geef informatie tooconnect toohello Azure SQL Data Warehouse-exemplaar voor de eigenschap connectionString Hallo nodig.</span><span class="sxs-lookup"><span data-stu-id="34b16-875">Specify information needed tooconnect toohello Azure SQL Data Warehouse instance for hello connectionString property.</span></span> |<span data-ttu-id="34b16-876">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-876">Yes</span></span> |



#### <a name="example"></a><span data-ttu-id="34b16-877">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-877">Example</span></span>

```json
{
    "name": "AzureSqlDWLinkedService",
    "properties": {
        "type": "AzureSqlDW",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="34b16-878">Zie voor meer informatie [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-878">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="34b16-879">Gegevensset</span><span class="sxs-lookup"><span data-stu-id="34b16-879">Dataset</span></span>
<span data-ttu-id="34b16-880">toodefine een gegevensset Azure SQL Data Warehouse set Hallo **type** van Hallo gegevensset te**AzureSqlDWTable**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties**sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-880">toodefine an Azure SQL Data Warehouse dataset, set hello **type** of hello dataset too**AzureSqlDWTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="34b16-881">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-881">Property</span></span> | <span data-ttu-id="34b16-882">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-882">Description</span></span> | <span data-ttu-id="34b16-883">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-883">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-884">tableName</span><span class="sxs-lookup"><span data-stu-id="34b16-884">tableName</span></span> |<span data-ttu-id="34b16-885">De naam van het Hallo-tabel of weergave in hello Azure SQL Data Warehouse-database die Hallo gekoppelde service verwijst.</span><span class="sxs-lookup"><span data-stu-id="34b16-885">Name of hello table or view in hello Azure SQL Data Warehouse database that hello linked service refers to.</span></span> |<span data-ttu-id="34b16-886">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-886">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-887">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-887">Example</span></span>

```json
{
    "name": "AzureSqlDWInput",
    "properties": {
    "type": "AzureSqlDWTable",
        "linkedServiceName": "AzureSqlDWLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="34b16-888">Zie voor meer informatie [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-888">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-dw-source-in-copy-activity"></a><span data-ttu-id="34b16-889">SQL DW-bron in de kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="34b16-889">SQL DW Source in Copy Activity</span></span>
<span data-ttu-id="34b16-890">Als u gegevens uit Azure SQL Data Warehouse kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**SqlDWSource**, en opgeven na eigenschappen in Hallo **bron**sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-890">If you are copying data from Azure SQL Data Warehouse, set hello **source type** of hello copy activity too**SqlDWSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="34b16-891">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-891">Property</span></span> | <span data-ttu-id="34b16-892">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-892">Description</span></span> | <span data-ttu-id="34b16-893">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="34b16-893">Allowed values</span></span> | <span data-ttu-id="34b16-894">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-894">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-895">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="34b16-895">sqlReaderQuery</span></span> |<span data-ttu-id="34b16-896">Hallo aangepaste query tooread gegevens worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-896">Use hello custom query tooread data.</span></span> |<span data-ttu-id="34b16-897">SQL-query-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="34b16-897">SQL query string.</span></span> <span data-ttu-id="34b16-898">Bijvoorbeeld: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="34b16-898">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="34b16-899">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-899">No</span></span> |
| <span data-ttu-id="34b16-900">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="34b16-900">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="34b16-901">Naam van Hallo opgeslagen procedure die gegevens uit Hallo brontabel leest.</span><span class="sxs-lookup"><span data-stu-id="34b16-901">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="34b16-902">Naam van Hallo opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="34b16-902">Name of hello stored procedure.</span></span> |<span data-ttu-id="34b16-903">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-903">No</span></span> |
| <span data-ttu-id="34b16-904">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="34b16-904">storedProcedureParameters</span></span> |<span data-ttu-id="34b16-905">Parameters voor Hallo opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="34b16-905">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="34b16-906">Naam/waarde-paren.</span><span class="sxs-lookup"><span data-stu-id="34b16-906">Name/value pairs.</span></span> <span data-ttu-id="34b16-907">Namen en hoofdlettergebruik van parameters moeten overeenkomen met Hallo namen en hoofdlettergebruik van Hallo opgeslagen procedureparameters.</span><span class="sxs-lookup"><span data-stu-id="34b16-907">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="34b16-908">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-908">No</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-909">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-909">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLDWtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSqlDWInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlDWSource",
                    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="34b16-910">Zie voor meer informatie [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-910">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-dw-sink-in-copy-activity"></a><span data-ttu-id="34b16-911">SQL DW Sink in de kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="34b16-911">SQL DW Sink in Copy Activity</span></span>
<span data-ttu-id="34b16-912">Als u gegevens tooAzure SQL Data Warehouse kopiëren wilt, stelt u Hallo **type sink** Hallo kopieeractiviteit te**SqlDWSink**, en opgeven na eigenschappen in Hallo **sink** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-912">If you are copying data tooAzure SQL Data Warehouse, set hello **sink type** of hello copy activity too**SqlDWSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="34b16-913">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-913">Property</span></span> | <span data-ttu-id="34b16-914">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-914">Description</span></span> | <span data-ttu-id="34b16-915">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="34b16-915">Allowed values</span></span> | <span data-ttu-id="34b16-916">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-916">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-917">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="34b16-917">sqlWriterCleanupScript</span></span> |<span data-ttu-id="34b16-918">Geef een query voor de Kopieeractiviteit tooexecute zodat de gegevens van een bepaald segment wordt opgeschoond.</span><span class="sxs-lookup"><span data-stu-id="34b16-918">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="34b16-919">Een query-instructie.</span><span class="sxs-lookup"><span data-stu-id="34b16-919">A query statement.</span></span> |<span data-ttu-id="34b16-920">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-920">No</span></span> |
| <span data-ttu-id="34b16-921">allowPolyBase</span><span class="sxs-lookup"><span data-stu-id="34b16-921">allowPolyBase</span></span> |<span data-ttu-id="34b16-922">Hiermee wordt aangegeven of toouse PolyBase (indien van toepassing) in plaats van BULKINSERT mechanisme.</span><span class="sxs-lookup"><span data-stu-id="34b16-922">Indicates whether toouse PolyBase (when applicable) instead of BULKINSERT mechanism.</span></span> <br/><br/> <span data-ttu-id="34b16-923">**Met PolyBase is Hallo aanbevolen manier tooload gegevens in SQL Data Warehouse.**</span><span class="sxs-lookup"><span data-stu-id="34b16-923">**Using PolyBase is hello recommended way tooload data into SQL Data Warehouse.**</span></span> |<span data-ttu-id="34b16-924">True</span><span class="sxs-lookup"><span data-stu-id="34b16-924">True</span></span> <br/><span data-ttu-id="34b16-925">False (standaard)</span><span class="sxs-lookup"><span data-stu-id="34b16-925">False (default)</span></span> |<span data-ttu-id="34b16-926">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-926">No</span></span> |
| <span data-ttu-id="34b16-927">polyBaseSettings</span><span class="sxs-lookup"><span data-stu-id="34b16-927">polyBaseSettings</span></span> |<span data-ttu-id="34b16-928">Een groep met eigenschappen die kunnen worden opgegeven wanneer hello **allowPolybase** eigenschap is ingesteld, te**true**.</span><span class="sxs-lookup"><span data-stu-id="34b16-928">A group of properties that can be specified when hello **allowPolybase** property is set too**true**.</span></span> |&nbsp; |<span data-ttu-id="34b16-929">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-929">No</span></span> |
| <span data-ttu-id="34b16-930">rejectValue</span><span class="sxs-lookup"><span data-stu-id="34b16-930">rejectValue</span></span> |<span data-ttu-id="34b16-931">Hiermee geeft u op Hallo getal of het percentage van de rijen die kunnen worden afgewezen voordat het Hallo-query is mislukt.</span><span class="sxs-lookup"><span data-stu-id="34b16-931">Specifies hello number or percentage of rows that can be rejected before hello query fails.</span></span> <br/><br/><span data-ttu-id="34b16-932">Meer informatie over Hallo PolyBase van opties in Hallo afwijzen **argumenten** sectie van [maken EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="34b16-932">Learn more about hello PolyBase’s reject options in hello **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span></span> |<span data-ttu-id="34b16-933">0 (standaard), 1, 2...</span><span class="sxs-lookup"><span data-stu-id="34b16-933">0 (default), 1, 2, …</span></span> |<span data-ttu-id="34b16-934">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-934">No</span></span> |
| <span data-ttu-id="34b16-935">rejectType</span><span class="sxs-lookup"><span data-stu-id="34b16-935">rejectType</span></span> |<span data-ttu-id="34b16-936">Hiermee geeft u op of Hallo rejectValue optie is opgegeven als een letterlijke waarde of een percentage.</span><span class="sxs-lookup"><span data-stu-id="34b16-936">Specifies whether hello rejectValue option is specified as a literal value or a percentage.</span></span> |<span data-ttu-id="34b16-937">In waarde (standaard), Percentage</span><span class="sxs-lookup"><span data-stu-id="34b16-937">Value (default), Percentage</span></span> |<span data-ttu-id="34b16-938">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-938">No</span></span> |
| <span data-ttu-id="34b16-939">rejectSampleValue</span><span class="sxs-lookup"><span data-stu-id="34b16-939">rejectSampleValue</span></span> |<span data-ttu-id="34b16-940">Bepaalt het aantal rijen tooretrieve Hallo voordat Hallo PolyBase Hallo percentage geweigerde rijen opnieuw berekend.</span><span class="sxs-lookup"><span data-stu-id="34b16-940">Determines hello number of rows tooretrieve before hello PolyBase recalculates hello percentage of rejected rows.</span></span> |<span data-ttu-id="34b16-941">1, 2, …</span><span class="sxs-lookup"><span data-stu-id="34b16-941">1, 2, …</span></span> |<span data-ttu-id="34b16-942">Ja, als **rejectType** is **percentage**</span><span class="sxs-lookup"><span data-stu-id="34b16-942">Yes, if **rejectType** is **percentage**</span></span> |
| <span data-ttu-id="34b16-943">useTypeDefault</span><span class="sxs-lookup"><span data-stu-id="34b16-943">useTypeDefault</span></span> |<span data-ttu-id="34b16-944">Hiermee geeft u op hoe toohandle ontbreken waarden in tekstbestanden gescheiden wanneer PolyBase gegevens uit Hallo tekstbestand ophaalt.</span><span class="sxs-lookup"><span data-stu-id="34b16-944">Specifies how toohandle missing values in delimited text files when PolyBase retrieves data from hello text file.</span></span><br/><br/><span data-ttu-id="34b16-945">Meer informatie over deze eigenschap in Hallo argumenten sectie [maken EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span><span class="sxs-lookup"><span data-stu-id="34b16-945">Learn more about this property from hello Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span></span> |<span data-ttu-id="34b16-946">True, False (standaard)</span><span class="sxs-lookup"><span data-stu-id="34b16-946">True, False (default)</span></span> |<span data-ttu-id="34b16-947">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-947">No</span></span> |
| <span data-ttu-id="34b16-948">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="34b16-948">writeBatchSize</span></span> |<span data-ttu-id="34b16-949">Voegt de gegevens in SQL-tabel Hallo wanneer Hallo buffergrootte writeBatchSize bereikt</span><span class="sxs-lookup"><span data-stu-id="34b16-949">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize</span></span> |<span data-ttu-id="34b16-950">Geheel getal (aantal rijen)</span><span class="sxs-lookup"><span data-stu-id="34b16-950">Integer (number of rows)</span></span> |<span data-ttu-id="34b16-951">Nee (standaard: 10000)</span><span class="sxs-lookup"><span data-stu-id="34b16-951">No (default: 10000)</span></span> |
| <span data-ttu-id="34b16-952">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="34b16-952">writeBatchTimeout</span></span> |<span data-ttu-id="34b16-953">Wachttijd voor Hallo batch insert-bewerking toocomplete voordat een time-out optreedt.</span><span class="sxs-lookup"><span data-stu-id="34b16-953">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="34b16-954">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="34b16-954">timespan</span></span><br/><br/> <span data-ttu-id="34b16-955">Voorbeeld: "00: 30:00 ' (30 minuten).</span><span class="sxs-lookup"><span data-stu-id="34b16-955">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="34b16-956">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-956">No</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-957">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-957">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQLDW",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlDWOutput"
            }],
            "typeProperties": {
                "source": {
                "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlDWSink",
                    "allowPolyBase": true
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="34b16-958">Zie voor meer informatie [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-958">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-search"></a><span data-ttu-id="34b16-959">Azure Search</span><span class="sxs-lookup"><span data-stu-id="34b16-959">Azure Search</span></span>

### <a name="linked-service"></a><span data-ttu-id="34b16-960">Gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="34b16-960">Linked service</span></span>
<span data-ttu-id="34b16-961">een Azure Search toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**AzureSearch**, en opgeven na eigenschappen in Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-961">toodefine an Azure Search linked service, set hello **type** of hello linked service too**AzureSearch**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="34b16-962">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-962">Property</span></span> | <span data-ttu-id="34b16-963">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-963">Description</span></span> | <span data-ttu-id="34b16-964">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-964">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="34b16-965">URL</span><span class="sxs-lookup"><span data-stu-id="34b16-965">url</span></span> | <span data-ttu-id="34b16-966">De URL voor hello Azure Search-service.</span><span class="sxs-lookup"><span data-stu-id="34b16-966">URL for hello Azure Search service.</span></span> | <span data-ttu-id="34b16-967">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-967">Yes</span></span> |
| <span data-ttu-id="34b16-968">sleutel</span><span class="sxs-lookup"><span data-stu-id="34b16-968">key</span></span> | <span data-ttu-id="34b16-969">Administratorsleutel voor hello Azure Search-service.</span><span class="sxs-lookup"><span data-stu-id="34b16-969">Admin key for hello Azure Search service.</span></span> | <span data-ttu-id="34b16-970">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-970">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-971">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-971">Example</span></span>

```json
{
    "name": "AzureSearchLinkedService",
    "properties": {
        "type": "AzureSearch",
        "typeProperties": {
            "url": "https://<service>.search.windows.net",
            "key": "<AdminKey>"
        }
    }
}
```

<span data-ttu-id="34b16-972">Zie voor meer informatie [Azure Search-connector](data-factory-azure-search-connector.md#linked-service-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-972">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="34b16-973">Gegevensset</span><span class="sxs-lookup"><span data-stu-id="34b16-973">Dataset</span></span>
<span data-ttu-id="34b16-974">toodefine een gegevensset Azure Search set Hallo **type** van Hallo gegevensset te**AzureSearchIndex**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie :</span><span class="sxs-lookup"><span data-stu-id="34b16-974">toodefine an Azure Search dataset, set hello **type** of hello dataset too**AzureSearchIndex**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="34b16-975">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-975">Property</span></span> | <span data-ttu-id="34b16-976">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-976">Description</span></span> | <span data-ttu-id="34b16-977">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-977">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="34b16-978">type</span><span class="sxs-lookup"><span data-stu-id="34b16-978">type</span></span> | <span data-ttu-id="34b16-979">de eigenschap type Hello te moet worden ingesteld**AzureSearchIndex**.</span><span class="sxs-lookup"><span data-stu-id="34b16-979">hello type property must be set too**AzureSearchIndex**.</span></span>| <span data-ttu-id="34b16-980">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-980">Yes</span></span> |
| <span data-ttu-id="34b16-981">NaamCommunity</span><span class="sxs-lookup"><span data-stu-id="34b16-981">indexName</span></span> | <span data-ttu-id="34b16-982">Naam van hello Azure Search-index.</span><span class="sxs-lookup"><span data-stu-id="34b16-982">Name of hello Azure Search index.</span></span> <span data-ttu-id="34b16-983">Data Factory maakt geen Hallo index.</span><span class="sxs-lookup"><span data-stu-id="34b16-983">Data Factory does not create hello index.</span></span> <span data-ttu-id="34b16-984">Hallo-index moet bestaan in Azure Search.</span><span class="sxs-lookup"><span data-stu-id="34b16-984">hello index must exist in Azure Search.</span></span> | <span data-ttu-id="34b16-985">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-985">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-986">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-986">Example</span></span>

```json
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties": {
            "indexName": "products"
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
    }
}
```

<span data-ttu-id="34b16-987">Zie voor meer informatie [Azure Search-connector](data-factory-azure-search-connector.md#dataset-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-987">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#dataset-properties) article.</span></span>

### <a name="azure-search-index-sink-in-copy-activity"></a><span data-ttu-id="34b16-988">Sink voor Azure Search-Index in de kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="34b16-988">Azure Search Index Sink in Copy Activity</span></span>
<span data-ttu-id="34b16-989">Als u gegevens tooan Azure Search-index kopieert, stelt u Hallo **type sink** Hallo kopieeractiviteit te**AzureSearchIndexSink**, en opgeven na eigenschappen in Hallo **sink**sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-989">If you are copying data tooan Azure Search index, set hello **sink type** of hello copy activity too**AzureSearchIndexSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="34b16-990">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-990">Property</span></span> | <span data-ttu-id="34b16-991">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-991">Description</span></span> | <span data-ttu-id="34b16-992">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="34b16-992">Allowed values</span></span> | <span data-ttu-id="34b16-993">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-993">Required</span></span> |
| -------- | ----------- | -------------- | -------- |
| <span data-ttu-id="34b16-994">WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="34b16-994">WriteBehavior</span></span> | <span data-ttu-id="34b16-995">Hiermee geeft u op of toomerge of vervangen, wanneer een document al in Hallo index bestaat.</span><span class="sxs-lookup"><span data-stu-id="34b16-995">Specifies whether toomerge or replace when a document already exists in hello index.</span></span> | <span data-ttu-id="34b16-996">samenvoegen (standaard)</span><span class="sxs-lookup"><span data-stu-id="34b16-996">Merge (default)</span></span><br/><span data-ttu-id="34b16-997">Uploaden</span><span class="sxs-lookup"><span data-stu-id="34b16-997">Upload</span></span>| <span data-ttu-id="34b16-998">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-998">No</span></span> |
| <span data-ttu-id="34b16-999">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="34b16-999">WriteBatchSize</span></span> | <span data-ttu-id="34b16-1000">Gegevens geüpload in hello Azure Search-index wanneer Hallo buffergrootte writeBatchSize bereikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-1000">Uploads data into hello Azure Search index when hello buffer size reaches writeBatchSize.</span></span> | <span data-ttu-id="34b16-1001">1 too1 000.</span><span class="sxs-lookup"><span data-stu-id="34b16-1001">1 too1,000.</span></span> <span data-ttu-id="34b16-1002">Standaardwaarde is 1000.</span><span class="sxs-lookup"><span data-stu-id="34b16-1002">Default value is 1000.</span></span> | <span data-ttu-id="34b16-1003">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1003">No</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-1004">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1004">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "SqlServertoAzureSearchIndex",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " SqlServerInput"
            }],
            "outputs": [{
                "name": "AzureSearchIndexDataset"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "AzureSearchIndexSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="34b16-1005">Zie voor meer informatie [Azure Search-connector](data-factory-azure-search-connector.md#copy-activity-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1005">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#copy-activity-properties) article.</span></span>

## <a name="azure-table-storage"></a><span data-ttu-id="34b16-1006">Azure-tabelopslag</span><span class="sxs-lookup"><span data-stu-id="34b16-1006">Azure Table Storage</span></span>

### <a name="linked-service"></a><span data-ttu-id="34b16-1007">Gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="34b16-1007">Linked service</span></span>
<span data-ttu-id="34b16-1008">Er zijn twee soorten gekoppelde services: gekoppelde Azure Storage-service en de gekoppelde Azure Storage SAS-service.</span><span class="sxs-lookup"><span data-stu-id="34b16-1008">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span></span>

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="34b16-1009">Een gekoppelde Azure Storage-service</span><span class="sxs-lookup"><span data-stu-id="34b16-1009">Azure Storage Linked Service</span></span>
<span data-ttu-id="34b16-1010">toolink uw Azure storage-account tooa data factory met behulp van Hallo **accountsleutel**, maak een gekoppelde Azure Storage-service.</span><span class="sxs-lookup"><span data-stu-id="34b16-1010">toolink your Azure storage account tooa data factory by using hello **account key**, create an Azure Storage linked service.</span></span> <span data-ttu-id="34b16-1011">toodefine een Azure Storage gekoppelde service, set Hallo **type** Hallo gekoppelde service te**AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="34b16-1011">toodefine an Azure Storage linked service, set hello **type** of hello linked service too**AzureStorage**.</span></span> <span data-ttu-id="34b16-1012">U kunt vervolgens opgeven na eigenschappen in Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-1012">Then, you can specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="34b16-1013">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1013">Property</span></span> | <span data-ttu-id="34b16-1014">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1014">Description</span></span> | <span data-ttu-id="34b16-1015">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1015">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="34b16-1016">type</span><span class="sxs-lookup"><span data-stu-id="34b16-1016">type</span></span> |<span data-ttu-id="34b16-1017">Hallo type eigenschap moet worden ingesteld op: **AzureStorage**</span><span class="sxs-lookup"><span data-stu-id="34b16-1017">hello type property must be set to: **AzureStorage**</span></span> |<span data-ttu-id="34b16-1018">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1018">Yes</span></span> |
| <span data-ttu-id="34b16-1019">connectionString</span><span class="sxs-lookup"><span data-stu-id="34b16-1019">connectionString</span></span> |<span data-ttu-id="34b16-1020">Geef informatie tooconnect tooAzure opslag voor de eigenschap connectionString Hallo nodig.</span><span class="sxs-lookup"><span data-stu-id="34b16-1020">Specify information needed tooconnect tooAzure storage for hello connectionString property.</span></span> |<span data-ttu-id="34b16-1021">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1021">Yes</span></span> |

<span data-ttu-id="34b16-1022">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="34b16-1022">**Example:**</span></span>  

```json
{  
    "name": "StorageLinkedService",  
    "properties": {  
        "type": "AzureStorage",  
        "typeProperties": {  
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"  
        }  
    }  
}  
```

#### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="34b16-1023">Gekoppelde Azure Storage SAS-Service</span><span class="sxs-lookup"><span data-stu-id="34b16-1023">Azure Storage SAS Linked Service</span></span>
<span data-ttu-id="34b16-1024">Hallo SAS van Azure Storage gekoppelde service, kunt u een Azure Storage-Account tooan Azure data factory toolink met behulp van een Shared Access Signature (SAS).</span><span class="sxs-lookup"><span data-stu-id="34b16-1024">hello Azure Storage SAS linked service allows you toolink an Azure Storage Account tooan Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="34b16-1025">Het biedt Hallo data factory toegang beperkt/tijdsgebonden tooall/specifieke bronnen (blobcontainer) / in Hallo-opslag.</span><span class="sxs-lookup"><span data-stu-id="34b16-1025">It provides hello data factory with restricted/time-bound access tooall/specific resources (blob/container) in hello storage.</span></span> <span data-ttu-id="34b16-1026">toolink uw Azure storage-account tooa data factory met behulp van Shared Access Signature maken van een SAS van Azure Storage gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="34b16-1026">toolink your Azure storage account tooa data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span></span> <span data-ttu-id="34b16-1027">een Azure Storage-SAS toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="34b16-1027">toodefine an Azure Storage SAS linked service, set hello **type** of hello linked service too**AzureStorageSas**.</span></span> <span data-ttu-id="34b16-1028">U kunt vervolgens opgeven na eigenschappen in Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-1028">Then, you can specify following properties in hello **typeProperties** section:</span></span>   

| <span data-ttu-id="34b16-1029">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1029">Property</span></span> | <span data-ttu-id="34b16-1030">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1030">Description</span></span> | <span data-ttu-id="34b16-1031">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1031">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="34b16-1032">type</span><span class="sxs-lookup"><span data-stu-id="34b16-1032">type</span></span> |<span data-ttu-id="34b16-1033">Hallo type eigenschap moet worden ingesteld op: **AzureStorageSas**</span><span class="sxs-lookup"><span data-stu-id="34b16-1033">hello type property must be set to: **AzureStorageSas**</span></span> |<span data-ttu-id="34b16-1034">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1034">Yes</span></span> |
| <span data-ttu-id="34b16-1035">sasUri</span><span class="sxs-lookup"><span data-stu-id="34b16-1035">sasUri</span></span> |<span data-ttu-id="34b16-1036">Geef de Shared Access Signature URI toohello Azure Storage-resources zoals blob-container of tabel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1036">Specify Shared Access Signature URI toohello Azure Storage resources such as blob, container, or table.</span></span> |<span data-ttu-id="34b16-1037">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1037">Yes</span></span> |

<span data-ttu-id="34b16-1038">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="34b16-1038">**Example:**</span></span>

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<storageUri>?<sasToken>"   
        }  
    }  
}  
```

<span data-ttu-id="34b16-1039">Zie voor meer informatie over deze gekoppelde services, [Azure Table Storage connector](data-factory-azure-table-connector.md#linked-service-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1039">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="34b16-1040">Gegevensset</span><span class="sxs-lookup"><span data-stu-id="34b16-1040">Dataset</span></span>
<span data-ttu-id="34b16-1041">toodefine een gegevensset Azure Table set Hallo **type** van Hallo gegevensset te**AzureTable**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-1041">toodefine an Azure Table dataset, set hello **type** of hello dataset too**AzureTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="34b16-1042">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1042">Property</span></span> | <span data-ttu-id="34b16-1043">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1043">Description</span></span> | <span data-ttu-id="34b16-1044">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1044">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-1045">tableName</span><span class="sxs-lookup"><span data-stu-id="34b16-1045">tableName</span></span> |<span data-ttu-id="34b16-1046">De naam van de tabel Hallo in hello Azure Table-Database-instantie waarnaar de gekoppelde service verwijst.</span><span class="sxs-lookup"><span data-stu-id="34b16-1046">Name of hello table in hello Azure Table Database instance that linked service refers to.</span></span> |<span data-ttu-id="34b16-1047">Ja.</span><span class="sxs-lookup"><span data-stu-id="34b16-1047">Yes.</span></span> <span data-ttu-id="34b16-1048">Wanneer een tabelnaam is opgegeven zonder een azureTableSourceQuery, worden alle records uit de tabel Hallo gekopieerde toohello bestemming.</span><span class="sxs-lookup"><span data-stu-id="34b16-1048">When a tableName is specified without an azureTableSourceQuery, all records from hello table are copied toohello destination.</span></span> <span data-ttu-id="34b16-1049">Als een azureTableSourceQuery ook is opgegeven, worden records uit de tabel Hallo die voldoet aan de query Hallo gekopieerde toohello bestemming.</span><span class="sxs-lookup"><span data-stu-id="34b16-1049">If an azureTableSourceQuery is also specified, records from hello table that satisfies hello query are copied toohello destination.</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-1050">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1050">Example</span></span>

```json
{
    "name": "AzureTableInput",
    "properties": {
        "type": "AzureTable",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="34b16-1051">Zie voor meer informatie over deze gekoppelde services, [Azure Table Storage connector](data-factory-azure-table-connector.md#dataset-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1051">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#dataset-properties) article.</span></span> 

### <a name="azure-table-source-in-copy-activity"></a><span data-ttu-id="34b16-1052">Bron van de Azure-tabel in de kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="34b16-1052">Azure Table Source in Copy Activity</span></span>
<span data-ttu-id="34b16-1053">Als u gegevens uit Azure Table Storage kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**AzureTableSource**, en opgeven na eigenschappen in Hallo **bron**sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-1053">If you are copying data from Azure Table Storage, set hello **source type** of hello copy activity too**AzureTableSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="34b16-1054">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1054">Property</span></span> | <span data-ttu-id="34b16-1055">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1055">Description</span></span> | <span data-ttu-id="34b16-1056">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="34b16-1056">Allowed values</span></span> | <span data-ttu-id="34b16-1057">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1057">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-1058">azureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="34b16-1058">azureTableSourceQuery</span></span> |<span data-ttu-id="34b16-1059">Hallo aangepaste query tooread gegevens worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-1059">Use hello custom query tooread data.</span></span> |<span data-ttu-id="34b16-1060">Azure-tabel queryreeks.</span><span class="sxs-lookup"><span data-stu-id="34b16-1060">Azure table query string.</span></span> <span data-ttu-id="34b16-1061">Zie de voorbeelden in de volgende sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="34b16-1061">See examples in hello next section.</span></span> |<span data-ttu-id="34b16-1062">Nee.</span><span class="sxs-lookup"><span data-stu-id="34b16-1062">No.</span></span> <span data-ttu-id="34b16-1063">Wanneer een tabelnaam is opgegeven zonder een azureTableSourceQuery, worden alle records uit de tabel Hallo gekopieerde toohello bestemming.</span><span class="sxs-lookup"><span data-stu-id="34b16-1063">When a tableName is specified without an azureTableSourceQuery, all records from hello table are copied toohello destination.</span></span> <span data-ttu-id="34b16-1064">Als een azureTableSourceQuery ook is opgegeven, worden records uit de tabel Hallo die voldoet aan de query Hallo gekopieerde toohello bestemming.</span><span class="sxs-lookup"><span data-stu-id="34b16-1064">If an azureTableSourceQuery is also specified, records from hello table that satisfies hello query are copied toohello destination.</span></span> |
| <span data-ttu-id="34b16-1065">azureTableSourceIgnoreTableNotFound</span><span class="sxs-lookup"><span data-stu-id="34b16-1065">azureTableSourceIgnoreTableNotFound</span></span> |<span data-ttu-id="34b16-1066">Geef aan of slikken Hallo uitzondering van de tabel niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="34b16-1066">Indicate whether swallow hello exception of table not exist.</span></span> |<span data-ttu-id="34b16-1067">DE WAARDE TRUE</span><span class="sxs-lookup"><span data-stu-id="34b16-1067">TRUE</span></span><br/><span data-ttu-id="34b16-1068">DE WAARDE FALSE</span><span class="sxs-lookup"><span data-stu-id="34b16-1068">FALSE</span></span> |<span data-ttu-id="34b16-1069">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1069">No</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-1070">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1070">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureTabletoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureTableInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "AzureTableSource",
                    "AzureTableSourceQuery": "PartitionKey eq 'DefaultPartitionKey'"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="34b16-1071">Zie voor meer informatie over deze gekoppelde services, [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1071">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span></span> 

### <a name="azure-table-sink-in-copy-activity"></a><span data-ttu-id="34b16-1072">Azure-tabel Sink in de kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="34b16-1072">Azure Table Sink in Copy Activity</span></span>
<span data-ttu-id="34b16-1073">Als u gegevens tooAzure Table Storage kopieert, stelt u Hallo **type sink** Hallo kopieeractiviteit te**AzureTableSink**, en opgeven na eigenschappen in Hallo **sink** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-1073">If you are copying data tooAzure Table Storage, set hello **sink type** of hello copy activity too**AzureTableSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="34b16-1074">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1074">Property</span></span> | <span data-ttu-id="34b16-1075">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1075">Description</span></span> | <span data-ttu-id="34b16-1076">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="34b16-1076">Allowed values</span></span> | <span data-ttu-id="34b16-1077">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1077">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-1078">azureTableDefaultPartitionKeyValue</span><span class="sxs-lookup"><span data-stu-id="34b16-1078">azureTableDefaultPartitionKeyValue</span></span> |<span data-ttu-id="34b16-1079">Standaardwaarde voor de partitiesleutel die kan worden gebruikt door Hallo sink.</span><span class="sxs-lookup"><span data-stu-id="34b16-1079">Default partition key value that can be used by hello sink.</span></span> |<span data-ttu-id="34b16-1080">Een string-waarde.</span><span class="sxs-lookup"><span data-stu-id="34b16-1080">A string value.</span></span> |<span data-ttu-id="34b16-1081">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1081">No</span></span> |
| <span data-ttu-id="34b16-1082">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="34b16-1082">azureTablePartitionKeyName</span></span> |<span data-ttu-id="34b16-1083">Naam van het Hallo-kolom waarvan de waarden worden gebruikt als partitiesleutels opgeven.</span><span class="sxs-lookup"><span data-stu-id="34b16-1083">Specify name of hello column whose values are used as partition keys.</span></span> <span data-ttu-id="34b16-1084">Als niet wordt opgegeven, wordt AzureTableDefaultPartitionKeyValue gebruikt als partitiesleutel Hallo.</span><span class="sxs-lookup"><span data-stu-id="34b16-1084">If not specified, AzureTableDefaultPartitionKeyValue is used as hello partition key.</span></span> |<span data-ttu-id="34b16-1085">De naam van een kolom.</span><span class="sxs-lookup"><span data-stu-id="34b16-1085">A column name.</span></span> |<span data-ttu-id="34b16-1086">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1086">No</span></span> |
| <span data-ttu-id="34b16-1087">azureTableRowKeyName</span><span class="sxs-lookup"><span data-stu-id="34b16-1087">azureTableRowKeyName</span></span> |<span data-ttu-id="34b16-1088">Naam van het Hallo-kolom waarvan de kolomwaarden worden gebruikt als de rijsleutel opgeven.</span><span class="sxs-lookup"><span data-stu-id="34b16-1088">Specify name of hello column whose column values are used as row key.</span></span> <span data-ttu-id="34b16-1089">Als niet wordt opgegeven, gebruikt u een GUID voor elke rij.</span><span class="sxs-lookup"><span data-stu-id="34b16-1089">If not specified, use a GUID for each row.</span></span> |<span data-ttu-id="34b16-1090">De naam van een kolom.</span><span class="sxs-lookup"><span data-stu-id="34b16-1090">A column name.</span></span> |<span data-ttu-id="34b16-1091">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1091">No</span></span> |
| <span data-ttu-id="34b16-1092">azureTableInsertType</span><span class="sxs-lookup"><span data-stu-id="34b16-1092">azureTableInsertType</span></span> |<span data-ttu-id="34b16-1093">Hallo modus tooinsert gegevens in Azure-tabel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1093">hello mode tooinsert data into Azure table.</span></span><br/><br/><span data-ttu-id="34b16-1094">Deze eigenschap bepaalt of bestaande rijen in de uitvoertabel Hallo met partitie-als rijsleutels die overeenkomt met de waarden vervangen of samenvoegen van hebben.</span><span class="sxs-lookup"><span data-stu-id="34b16-1094">This property controls whether existing rows in hello output table with matching partition and row keys have their values replaced or merged.</span></span> <br/><br/><span data-ttu-id="34b16-1095">toolearn over hoe deze instellingen (merge en vervangen) werken, Zie [invoegen of Merge entiteit](https://msdn.microsoft.com/library/azure/hh452241.aspx) en [invoegen of vervangen entiteit](https://msdn.microsoft.com/library/azure/hh452242.aspx) onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="34b16-1095">toolearn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span></span> <br/><br> <span data-ttu-id="34b16-1096">Deze instelling is van toepassing op Hallo rijniveau niet Hallo-tabelniveau, en geen van beide optie worden de rijen in de uitvoertabel Hallo die niet bestaan in de invoer Hallo verwijderd.</span><span class="sxs-lookup"><span data-stu-id="34b16-1096">This setting applies at hello row level, not hello table level, and neither option deletes rows in hello output table that do not exist in hello input.</span></span> |<span data-ttu-id="34b16-1097">samenvoegen (standaard)</span><span class="sxs-lookup"><span data-stu-id="34b16-1097">merge (default)</span></span><br/><span data-ttu-id="34b16-1098">vervangen</span><span class="sxs-lookup"><span data-stu-id="34b16-1098">replace</span></span> |<span data-ttu-id="34b16-1099">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1099">No</span></span> |
| <span data-ttu-id="34b16-1100">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="34b16-1100">writeBatchSize</span></span> |<span data-ttu-id="34b16-1101">Voegt de gegevens in hello Azure-tabel wanneer Hallo writeBatchSize of writeBatchTimeout is bereikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-1101">Inserts data into hello Azure table when hello writeBatchSize or writeBatchTimeout is hit.</span></span> |<span data-ttu-id="34b16-1102">Geheel getal (aantal rijen)</span><span class="sxs-lookup"><span data-stu-id="34b16-1102">Integer (number of rows)</span></span> |<span data-ttu-id="34b16-1103">Nee (standaard: 10000)</span><span class="sxs-lookup"><span data-stu-id="34b16-1103">No (default: 10000)</span></span> |
| <span data-ttu-id="34b16-1104">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="34b16-1104">writeBatchTimeout</span></span> |<span data-ttu-id="34b16-1105">Voegt de gegevens in hello Azure-tabel wanneer Hallo writeBatchSize of writeBatchTimeout is bereikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-1105">Inserts data into hello Azure table when hello writeBatchSize or writeBatchTimeout is hit</span></span> |<span data-ttu-id="34b16-1106">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="34b16-1106">timespan</span></span><br/><br/><span data-ttu-id="34b16-1107">Voorbeeld: "00: 20:00 ' (20 minuten)</span><span class="sxs-lookup"><span data-stu-id="34b16-1107">Example: “00:20:00” (20 minutes)</span></span> |<span data-ttu-id="34b16-1108">Nee (standaard toostorage client standaardtime-out waarde 90 sec)</span><span class="sxs-lookup"><span data-stu-id="34b16-1108">No (Default toostorage client default timeout value 90 sec)</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-1109">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1109">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoTable",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureTableOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "AzureTableSink",
                    "writeBatchSize": 100,
                    "writeBatchTimeout": "01:00:00"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="34b16-1110">Zie voor meer informatie over deze gekoppelde services, [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1110">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span></span> 

## <a name="amazon-redshift"></a><span data-ttu-id="34b16-1111">Amazon RedShift</span><span class="sxs-lookup"><span data-stu-id="34b16-1111">Amazon RedShift</span></span>

### <a name="linked-service"></a><span data-ttu-id="34b16-1112">Gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="34b16-1112">Linked service</span></span>
<span data-ttu-id="34b16-1113">een Redshift Amazon toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**AmazonRedshift**, en opgeven na eigenschappen in Hallo **typeProperties**sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-1113">toodefine an Amazon Redshift linked service, set hello **type** of hello linked service too**AmazonRedshift**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="34b16-1114">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1114">Property</span></span> | <span data-ttu-id="34b16-1115">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1115">Description</span></span> | <span data-ttu-id="34b16-1116">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1116">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-1117">server</span><span class="sxs-lookup"><span data-stu-id="34b16-1117">server</span></span> |<span data-ttu-id="34b16-1118">IP-naam adres of de hostnaam van Hallo Amazon Redshift server.</span><span class="sxs-lookup"><span data-stu-id="34b16-1118">IP address or host name of hello Amazon Redshift server.</span></span> |<span data-ttu-id="34b16-1119">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1119">Yes</span></span> |
| <span data-ttu-id="34b16-1120">poort</span><span class="sxs-lookup"><span data-stu-id="34b16-1120">port</span></span> |<span data-ttu-id="34b16-1121">toolisten Hello aantal Hallo TCP-poort die Hallo Amazon Redshift server gebruikt voor clientverbindingen.</span><span class="sxs-lookup"><span data-stu-id="34b16-1121">hello number of hello TCP port that hello Amazon Redshift server uses toolisten for client connections.</span></span> |<span data-ttu-id="34b16-1122">Nee, de standaardwaarde: 5439</span><span class="sxs-lookup"><span data-stu-id="34b16-1122">No, default value: 5439</span></span> |
| <span data-ttu-id="34b16-1123">database</span><span class="sxs-lookup"><span data-stu-id="34b16-1123">database</span></span> |<span data-ttu-id="34b16-1124">Naam van Hallo Amazon Redshift database.</span><span class="sxs-lookup"><span data-stu-id="34b16-1124">Name of hello Amazon Redshift database.</span></span> |<span data-ttu-id="34b16-1125">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1125">Yes</span></span> |
| <span data-ttu-id="34b16-1126">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="34b16-1126">username</span></span> |<span data-ttu-id="34b16-1127">Naam van de gebruiker die toegang toohello database heeft.</span><span class="sxs-lookup"><span data-stu-id="34b16-1127">Name of user who has access toohello database.</span></span> |<span data-ttu-id="34b16-1128">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1128">Yes</span></span> |
| <span data-ttu-id="34b16-1129">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="34b16-1129">password</span></span> |<span data-ttu-id="34b16-1130">Wachtwoord voor gebruikersaccount Hallo.</span><span class="sxs-lookup"><span data-stu-id="34b16-1130">Password for hello user account.</span></span> |<span data-ttu-id="34b16-1131">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1131">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-1132">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1132">Example</span></span>

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties": {
        "type": "AmazonRedshift",
        "typeProperties": {
            "server": "<Amazon Redshift host name or IP address>",
            "port": 5439,
            "database": "<database name>",
            "username": "user",
            "password": "password"
        }
    }
}
```

<span data-ttu-id="34b16-1133">Zie voor meer informatie [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#linked-service-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1133">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="34b16-1134">Gegevensset</span><span class="sxs-lookup"><span data-stu-id="34b16-1134">Dataset</span></span>
<span data-ttu-id="34b16-1135">toodefine een gegevensset Amazon Redshift set Hallo **type** van Hallo gegevensset te**RelationalTable**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-1135">toodefine an Amazon Redshift dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="34b16-1136">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1136">Property</span></span> | <span data-ttu-id="34b16-1137">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1137">Description</span></span> | <span data-ttu-id="34b16-1138">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1138">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-1139">tableName</span><span class="sxs-lookup"><span data-stu-id="34b16-1139">tableName</span></span> |<span data-ttu-id="34b16-1140">De naam van de tabel Hallo in Hallo Amazon Redshift database waarnaar de gekoppelde service verwijst.</span><span class="sxs-lookup"><span data-stu-id="34b16-1140">Name of hello table in hello Amazon Redshift database that linked service refers to.</span></span> |<span data-ttu-id="34b16-1141">Nee (als **query** van **RelationalSource** is opgegeven)</span><span class="sxs-lookup"><span data-stu-id="34b16-1141">No (if **query** of **RelationalSource** is specified)</span></span> |


#### <a name="example"></a><span data-ttu-id="34b16-1142">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1142">Example</span></span>

```json
{
    "name": "AmazonRedshiftInputDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "AmazonRedshiftLinkedService",
        "typeProperties": {
            "tableName": "<Table name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
<span data-ttu-id="34b16-1143">Zie voor meer informatie [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#dataset-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1143">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="34b16-1144">Relationele gegevensbron in de kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="34b16-1144">Relational Source in Copy Activity</span></span> 
<span data-ttu-id="34b16-1145">Als u gegevens vanaf Amazon Redshift kopieert, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**RelationalSource**, en opgeven na eigenschappen in Hallo **bron** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-1145">If you are copying data from Amazon Redshift, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="34b16-1146">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1146">Property</span></span> | <span data-ttu-id="34b16-1147">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1147">Description</span></span> | <span data-ttu-id="34b16-1148">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="34b16-1148">Allowed values</span></span> | <span data-ttu-id="34b16-1149">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1149">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-1150">query</span><span class="sxs-lookup"><span data-stu-id="34b16-1150">query</span></span> |<span data-ttu-id="34b16-1151">Hallo aangepaste query tooread gegevens worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-1151">Use hello custom query tooread data.</span></span> |<span data-ttu-id="34b16-1152">SQL-query-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="34b16-1152">SQL query string.</span></span> <span data-ttu-id="34b16-1153">Bijvoorbeeld: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="34b16-1153">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="34b16-1154">Nee (als **tableName** van **gegevensset** is opgegeven)</span><span class="sxs-lookup"><span data-stu-id="34b16-1154">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-1155">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1155">Example</span></span>

```json
{
    "name": "CopyAmazonRedshiftToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "AmazonRedshiftInputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "AmazonRedshiftToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```
<span data-ttu-id="34b16-1156">Zie voor meer informatie [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#copy-activity-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1156">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#copy-activity-properties) article.</span></span>

## <a name="ibm-db2"></a><span data-ttu-id="34b16-1157">IBM DB2</span><span class="sxs-lookup"><span data-stu-id="34b16-1157">IBM DB2</span></span>

### <a name="linked-service"></a><span data-ttu-id="34b16-1158">Gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="34b16-1158">Linked service</span></span>
<span data-ttu-id="34b16-1159">een IBM DB2 toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**OnPremisesDB2**, en opgeven na eigenschappen in Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-1159">toodefine an IBM DB2 linked service, set hello **type** of hello linked service too**OnPremisesDB2**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="34b16-1160">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1160">Property</span></span> | <span data-ttu-id="34b16-1161">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1161">Description</span></span> | <span data-ttu-id="34b16-1162">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1162">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-1163">server</span><span class="sxs-lookup"><span data-stu-id="34b16-1163">server</span></span> |<span data-ttu-id="34b16-1164">Naam van Hallo DB2-server.</span><span class="sxs-lookup"><span data-stu-id="34b16-1164">Name of hello DB2 server.</span></span> |<span data-ttu-id="34b16-1165">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1165">Yes</span></span> |
| <span data-ttu-id="34b16-1166">database</span><span class="sxs-lookup"><span data-stu-id="34b16-1166">database</span></span> |<span data-ttu-id="34b16-1167">Naam van Hallo DB2-database.</span><span class="sxs-lookup"><span data-stu-id="34b16-1167">Name of hello DB2 database.</span></span> |<span data-ttu-id="34b16-1168">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1168">Yes</span></span> |
| <span data-ttu-id="34b16-1169">Schema</span><span class="sxs-lookup"><span data-stu-id="34b16-1169">schema</span></span> |<span data-ttu-id="34b16-1170">Naam van Hallo schema in Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="34b16-1170">Name of hello schema in hello database.</span></span> <span data-ttu-id="34b16-1171">Hallo-schemanaam is hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="34b16-1171">hello schema name is case-sensitive.</span></span> |<span data-ttu-id="34b16-1172">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1172">No</span></span> |
| <span data-ttu-id="34b16-1173">authenticationType</span><span class="sxs-lookup"><span data-stu-id="34b16-1173">authenticationType</span></span> |<span data-ttu-id="34b16-1174">Type verificatie gebruikt tooconnect toohello DB2-database.</span><span class="sxs-lookup"><span data-stu-id="34b16-1174">Type of authentication used tooconnect toohello DB2 database.</span></span> <span data-ttu-id="34b16-1175">Mogelijke waarden zijn: anoniem, basis en Windows.</span><span class="sxs-lookup"><span data-stu-id="34b16-1175">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="34b16-1176">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1176">Yes</span></span> |
| <span data-ttu-id="34b16-1177">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="34b16-1177">username</span></span> |<span data-ttu-id="34b16-1178">Geef de gebruikersnaam als u basisverificatie of Windows-verificatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-1178">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="34b16-1179">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1179">No</span></span> |
| <span data-ttu-id="34b16-1180">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="34b16-1180">password</span></span> |<span data-ttu-id="34b16-1181">Wachtwoord voor gebruikersaccount Hallo die u hebt opgegeven voor Hallo gebruikersnaam opgeven.</span><span class="sxs-lookup"><span data-stu-id="34b16-1181">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="34b16-1182">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1182">No</span></span> |
| <span data-ttu-id="34b16-1183">gatewayName</span><span class="sxs-lookup"><span data-stu-id="34b16-1183">gatewayName</span></span> |<span data-ttu-id="34b16-1184">Naam van Hallo-gateway die Hallo Data Factory-service moet tooconnect toohello lokale DB2-database gebruiken.</span><span class="sxs-lookup"><span data-stu-id="34b16-1184">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises DB2 database.</span></span> |<span data-ttu-id="34b16-1185">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1185">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-1186">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1186">Example</span></span>
```json
{
    "name": "OnPremDb2LinkedService",
    "properties": {
        "type": "OnPremisesDb2",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
<span data-ttu-id="34b16-1187">Zie voor meer informatie [IBM DB2-connector](#data-factory-onprem-db2-connector.md#linked-service-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1187">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="34b16-1188">Gegevensset</span><span class="sxs-lookup"><span data-stu-id="34b16-1188">Dataset</span></span>
<span data-ttu-id="34b16-1189">toodefine een DB2-gegevensset, set Hallo **type** van Hallo gegevensset te**RelationalTable**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-1189">toodefine a DB2 dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span>

| <span data-ttu-id="34b16-1190">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1190">Property</span></span> | <span data-ttu-id="34b16-1191">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1191">Description</span></span> | <span data-ttu-id="34b16-1192">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1192">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-1193">tableName</span><span class="sxs-lookup"><span data-stu-id="34b16-1193">tableName</span></span> |<span data-ttu-id="34b16-1194">De naam van het Hallo-tabel in Hallo DB2-Database-instantie waarnaar de gekoppelde service verwijst.</span><span class="sxs-lookup"><span data-stu-id="34b16-1194">Name of hello table in hello DB2 Database instance that linked service refers to.</span></span> <span data-ttu-id="34b16-1195">Hallo tableName is hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="34b16-1195">hello tableName is case-sensitive.</span></span> |<span data-ttu-id="34b16-1196">Nee (als **query** van **RelationalSource** is opgegeven)</span><span class="sxs-lookup"><span data-stu-id="34b16-1196">No (if **query** of **RelationalSource** is specified)</span></span> 

#### <a name="example"></a><span data-ttu-id="34b16-1197">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1197">Example</span></span>
```json
{
    "name": "Db2DataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremDb2LinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="34b16-1198">Zie voor meer informatie [IBM DB2-connector](#data-factory-onprem-db2-connector.md#dataset-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1198">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="34b16-1199">Relationele gegevensbron in de kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="34b16-1199">Relational Source in Copy Activity</span></span>
<span data-ttu-id="34b16-1200">Als u gegevens uit IBM DB2 kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**RelationalSource**, en opgeven na eigenschappen in Hallo **bron** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-1200">If you are copying data from IBM DB2, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="34b16-1201">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1201">Property</span></span> | <span data-ttu-id="34b16-1202">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1202">Description</span></span> | <span data-ttu-id="34b16-1203">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="34b16-1203">Allowed values</span></span> | <span data-ttu-id="34b16-1204">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1204">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-1205">query</span><span class="sxs-lookup"><span data-stu-id="34b16-1205">query</span></span> |<span data-ttu-id="34b16-1206">Hallo aangepaste query tooread gegevens worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-1206">Use hello custom query tooread data.</span></span> |<span data-ttu-id="34b16-1207">SQL-query-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="34b16-1207">SQL query string.</span></span> <span data-ttu-id="34b16-1208">Bijvoorbeeld: `"query": "select * from "MySchema"."MyTable""`.</span><span class="sxs-lookup"><span data-stu-id="34b16-1208">For example: `"query": "select * from "MySchema"."MyTable""`.</span></span> |<span data-ttu-id="34b16-1209">Nee (als **tableName** van **gegevensset** is opgegeven)</span><span class="sxs-lookup"><span data-stu-id="34b16-1209">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-1210">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1210">Example</span></span>
```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from \"Orders\""
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "Db2DataSet"
            }],
            "outputs": [{
                "name": "AzureBlobDb2DataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "Db2ToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```
<span data-ttu-id="34b16-1211">Zie voor meer informatie [IBM DB2-connector](#data-factory-onprem-db2-connector.md#copy-activity-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1211">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#copy-activity-properties) article.</span></span>

## <a name="mysql"></a><span data-ttu-id="34b16-1212">MySQL</span><span class="sxs-lookup"><span data-stu-id="34b16-1212">MySQL</span></span>

### <a name="linked-service"></a><span data-ttu-id="34b16-1213">Gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="34b16-1213">Linked service</span></span>
<span data-ttu-id="34b16-1214">een MySQL toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**OnPremisesMySql**, en opgeven na eigenschappen in Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-1214">toodefine a MySQL linked service, set hello **type** of hello linked service too**OnPremisesMySql**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="34b16-1215">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1215">Property</span></span> | <span data-ttu-id="34b16-1216">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1216">Description</span></span> | <span data-ttu-id="34b16-1217">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1217">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-1218">server</span><span class="sxs-lookup"><span data-stu-id="34b16-1218">server</span></span> |<span data-ttu-id="34b16-1219">Naam van Hallo MySQL-server.</span><span class="sxs-lookup"><span data-stu-id="34b16-1219">Name of hello MySQL server.</span></span> |<span data-ttu-id="34b16-1220">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1220">Yes</span></span> |
| <span data-ttu-id="34b16-1221">database</span><span class="sxs-lookup"><span data-stu-id="34b16-1221">database</span></span> |<span data-ttu-id="34b16-1222">Naam van Hallo MySQL-database.</span><span class="sxs-lookup"><span data-stu-id="34b16-1222">Name of hello MySQL database.</span></span> |<span data-ttu-id="34b16-1223">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1223">Yes</span></span> |
| <span data-ttu-id="34b16-1224">Schema</span><span class="sxs-lookup"><span data-stu-id="34b16-1224">schema</span></span> |<span data-ttu-id="34b16-1225">Naam van Hallo schema in Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="34b16-1225">Name of hello schema in hello database.</span></span> |<span data-ttu-id="34b16-1226">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1226">No</span></span> |
| <span data-ttu-id="34b16-1227">authenticationType</span><span class="sxs-lookup"><span data-stu-id="34b16-1227">authenticationType</span></span> |<span data-ttu-id="34b16-1228">Type verificatie gebruikt tooconnect toohello MySQL-database.</span><span class="sxs-lookup"><span data-stu-id="34b16-1228">Type of authentication used tooconnect toohello MySQL database.</span></span> <span data-ttu-id="34b16-1229">Mogelijke waarden zijn: `Basic`.</span><span class="sxs-lookup"><span data-stu-id="34b16-1229">Possible values are: `Basic`.</span></span> |<span data-ttu-id="34b16-1230">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1230">Yes</span></span> |
| <span data-ttu-id="34b16-1231">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="34b16-1231">username</span></span> |<span data-ttu-id="34b16-1232">Geef de gebruiker de naam van tooconnect toohello MySQL-database.</span><span class="sxs-lookup"><span data-stu-id="34b16-1232">Specify user name tooconnect toohello MySQL database.</span></span> |<span data-ttu-id="34b16-1233">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1233">Yes</span></span> |
| <span data-ttu-id="34b16-1234">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="34b16-1234">password</span></span> |<span data-ttu-id="34b16-1235">Geef het wachtwoord voor Hallo-gebruikersaccount die u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="34b16-1235">Specify password for hello user account you specified.</span></span> |<span data-ttu-id="34b16-1236">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1236">Yes</span></span> |
| <span data-ttu-id="34b16-1237">gatewayName</span><span class="sxs-lookup"><span data-stu-id="34b16-1237">gatewayName</span></span> |<span data-ttu-id="34b16-1238">Naam van Hallo-gateway die Hallo Data Factory-service moet tooconnect toohello lokale MySQL-database gebruiken.</span><span class="sxs-lookup"><span data-stu-id="34b16-1238">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises MySQL database.</span></span> |<span data-ttu-id="34b16-1239">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1239">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-1240">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1240">Example</span></span>

```json
{
    "name": "OnPremMySqlLinkedService",
    "properties": {
        "type": "OnPremisesMySql",
        "typeProperties": {
            "server": "<server name>",
            "database": "<database name>",
            "schema": "<schema name>",
            "authenticationType": "<authentication type>",
            "userName": "<user name>",
            "password": "<password>",
            "gatewayName": "<gateway>"
        }
    }
}
```

<span data-ttu-id="34b16-1241">Zie voor meer informatie [MySQL connector](data-factory-onprem-mysql-connector.md#linked-service-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1241">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="34b16-1242">Gegevensset</span><span class="sxs-lookup"><span data-stu-id="34b16-1242">Dataset</span></span>
<span data-ttu-id="34b16-1243">toodefine een gegevensset MySQL set Hallo **type** van Hallo gegevensset te**RelationalTable**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-1243">toodefine a MySQL dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="34b16-1244">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1244">Property</span></span> | <span data-ttu-id="34b16-1245">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1245">Description</span></span> | <span data-ttu-id="34b16-1246">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1246">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-1247">tableName</span><span class="sxs-lookup"><span data-stu-id="34b16-1247">tableName</span></span> |<span data-ttu-id="34b16-1248">De naam van de tabel Hallo in Hallo MySQL-Database-instantie waarnaar de gekoppelde service verwijst.</span><span class="sxs-lookup"><span data-stu-id="34b16-1248">Name of hello table in hello MySQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="34b16-1249">Nee (als **query** van **RelationalSource** is opgegeven)</span><span class="sxs-lookup"><span data-stu-id="34b16-1249">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-1250">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1250">Example</span></span>

```json
{
    "name": "MySqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremMySqlLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="34b16-1251">Zie voor meer informatie [MySQL connector](data-factory-onprem-mysql-connector.md#dataset-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1251">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="34b16-1252">Relationele gegevensbron in de kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="34b16-1252">Relational Source in Copy Activity</span></span>
<span data-ttu-id="34b16-1253">Als u gegevens uit een MySQL-database kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**RelationalSource**, en opgeven na eigenschappen in Hallo **bron** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-1253">If you are copying data from a MySQL database, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="34b16-1254">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1254">Property</span></span> | <span data-ttu-id="34b16-1255">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1255">Description</span></span> | <span data-ttu-id="34b16-1256">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="34b16-1256">Allowed values</span></span> | <span data-ttu-id="34b16-1257">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1257">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-1258">query</span><span class="sxs-lookup"><span data-stu-id="34b16-1258">query</span></span> |<span data-ttu-id="34b16-1259">Hallo aangepaste query tooread gegevens worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-1259">Use hello custom query tooread data.</span></span> |<span data-ttu-id="34b16-1260">SQL-query-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="34b16-1260">SQL query string.</span></span> <span data-ttu-id="34b16-1261">Bijvoorbeeld: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="34b16-1261">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="34b16-1262">Nee (als **tableName** van **gegevensset** is opgegeven)</span><span class="sxs-lookup"><span data-stu-id="34b16-1262">No (if **tableName** of **dataset** is specified)</span></span> |


#### <a name="example"></a><span data-ttu-id="34b16-1263">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1263">Example</span></span>
```json
{
    "name": "CopyMySqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "MySqlDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobMySqlDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "MySqlToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="34b16-1264">Zie voor meer informatie [MySQL connector](data-factory-onprem-mysql-connector.md#copy-activity-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1264">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#copy-activity-properties) article.</span></span> 

## <a name="oracle"></a><span data-ttu-id="34b16-1265">Oracle</span><span class="sxs-lookup"><span data-stu-id="34b16-1265">Oracle</span></span> 

### <a name="linked-service"></a><span data-ttu-id="34b16-1266">Gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="34b16-1266">Linked service</span></span>
<span data-ttu-id="34b16-1267">een Oracle toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**OnPremisesOracle**, en opgeven na eigenschappen in Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-1267">toodefine an Oracle linked service, set hello **type** of hello linked service too**OnPremisesOracle**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="34b16-1268">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1268">Property</span></span> | <span data-ttu-id="34b16-1269">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1269">Description</span></span> | <span data-ttu-id="34b16-1270">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1270">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-1271">driverType</span><span class="sxs-lookup"><span data-stu-id="34b16-1271">driverType</span></span> | <span data-ttu-id="34b16-1272">Geef op welke stuurprogramma toouse toocopy gegevens uit / tooOracle Database.</span><span class="sxs-lookup"><span data-stu-id="34b16-1272">Specify which driver toouse toocopy data from/tooOracle Database.</span></span> <span data-ttu-id="34b16-1273">Toegestane waarden zijn **Microsoft** of **ODP** (standaard).</span><span class="sxs-lookup"><span data-stu-id="34b16-1273">Allowed values are **Microsoft** or **ODP** (default).</span></span> <span data-ttu-id="34b16-1274">Zie [ondersteunde versie en installatieopties](#supported-versions-and-installation) gedeelte stuurprogrammagegevens.</span><span class="sxs-lookup"><span data-stu-id="34b16-1274">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span></span> | <span data-ttu-id="34b16-1275">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1275">No</span></span> |
| <span data-ttu-id="34b16-1276">connectionString</span><span class="sxs-lookup"><span data-stu-id="34b16-1276">connectionString</span></span> | <span data-ttu-id="34b16-1277">Geef informatie tooconnect toohello Oracle-Database-exemplaar voor de eigenschap connectionString Hallo nodig.</span><span class="sxs-lookup"><span data-stu-id="34b16-1277">Specify information needed tooconnect toohello Oracle Database instance for hello connectionString property.</span></span> | <span data-ttu-id="34b16-1278">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1278">Yes</span></span> |
| <span data-ttu-id="34b16-1279">gatewayName</span><span class="sxs-lookup"><span data-stu-id="34b16-1279">gatewayName</span></span> | <span data-ttu-id="34b16-1280">Naam van Hallo gateway die die gebruikte tooconnect toohello lokale Oracle-server</span><span class="sxs-lookup"><span data-stu-id="34b16-1280">Name of hello gateway that that is used tooconnect toohello on-premises Oracle server</span></span> |<span data-ttu-id="34b16-1281">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1281">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-1282">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1282">Example</span></span>
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString": "Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="34b16-1283">Zie voor meer informatie [Oracle connector](data-factory-onprem-oracle-connector.md#linked-service-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1283">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="34b16-1284">Gegevensset</span><span class="sxs-lookup"><span data-stu-id="34b16-1284">Dataset</span></span>
<span data-ttu-id="34b16-1285">toodefine een gegevensset Oracle set Hallo **type** van Hallo gegevensset te**OracleTable**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-1285">toodefine an Oracle dataset, set hello **type** of hello dataset too**OracleTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="34b16-1286">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1286">Property</span></span> | <span data-ttu-id="34b16-1287">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1287">Description</span></span> | <span data-ttu-id="34b16-1288">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1288">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-1289">tableName</span><span class="sxs-lookup"><span data-stu-id="34b16-1289">tableName</span></span> |<span data-ttu-id="34b16-1290">De naam van de tabel Hallo in Hallo Oracle-Database die Hallo gekoppelde service verwijst.</span><span class="sxs-lookup"><span data-stu-id="34b16-1290">Name of hello table in hello Oracle Database that hello linked service refers to.</span></span> |<span data-ttu-id="34b16-1291">Nee (als **oracleReaderQuery** van **OracleSource** is opgegeven)</span><span class="sxs-lookup"><span data-stu-id="34b16-1291">No (if **oracleReaderQuery** of **OracleSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-1292">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1292">Example</span></span>

```json
{
    "name": "OracleInput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "offset": "01:00:00",
            "interval": "1",
            "anchorDateTime": "2016-02-27T12:00:00",
            "frequency": "Hour"
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="34b16-1293">Zie voor meer informatie [Oracle connector](data-factory-onprem-oracle-connector.md#dataset-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1293">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#dataset-properties) article.</span></span>

### <a name="oracle-source-in-copy-activity"></a><span data-ttu-id="34b16-1294">Oracle-bron in de kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="34b16-1294">Oracle Source in Copy Activity</span></span>
<span data-ttu-id="34b16-1295">Als u gegevens uit een Oracle-database kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**OracleSource**, en opgeven na eigenschappen in Hallo **bron** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-1295">If you are copying data from an Oracle database, set hello **source type** of hello copy activity too**OracleSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="34b16-1296">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1296">Property</span></span> | <span data-ttu-id="34b16-1297">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1297">Description</span></span> | <span data-ttu-id="34b16-1298">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="34b16-1298">Allowed values</span></span> | <span data-ttu-id="34b16-1299">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1299">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-1300">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="34b16-1300">oracleReaderQuery</span></span> |<span data-ttu-id="34b16-1301">Hallo aangepaste query tooread gegevens worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-1301">Use hello custom query tooread data.</span></span> |<span data-ttu-id="34b16-1302">SQL-query-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="34b16-1302">SQL query string.</span></span> <span data-ttu-id="34b16-1303">Bijvoorbeeld: `select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="34b16-1303">For example: `select * from MyTable`</span></span> <br/><br/><span data-ttu-id="34b16-1304">Als niet wordt opgegeven, Hallo SQL-instructie die is uitgevoerd:`select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="34b16-1304">If not specified, hello SQL statement that is executed: `select * from MyTable`</span></span> |<span data-ttu-id="34b16-1305">Nee (als **tableName** van **gegevensset** is opgegeven)</span><span class="sxs-lookup"><span data-stu-id="34b16-1305">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-1306">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1306">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "OracletoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " OracleInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "OracleSource",
                    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
            "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="34b16-1307">Zie voor meer informatie [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1307">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span></span>

### <a name="oracle-sink-in-copy-activity"></a><span data-ttu-id="34b16-1308">Oracle-Sink in de kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="34b16-1308">Oracle Sink in Copy Activity</span></span>
<span data-ttu-id="34b16-1309">Als u gegevens tooam Oracle-database kopiëren wilt, stelt u Hallo **type sink** Hallo kopieeractiviteit te**OracleSink**, en opgeven na eigenschappen in Hallo **sink** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-1309">If you are copying data tooam Oracle database, set hello **sink type** of hello copy activity too**OracleSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="34b16-1310">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1310">Property</span></span> | <span data-ttu-id="34b16-1311">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1311">Description</span></span> | <span data-ttu-id="34b16-1312">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="34b16-1312">Allowed values</span></span> | <span data-ttu-id="34b16-1313">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1313">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-1314">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="34b16-1314">writeBatchTimeout</span></span> |<span data-ttu-id="34b16-1315">Wachttijd voor Hallo batch insert-bewerking toocomplete voordat een time-out optreedt.</span><span class="sxs-lookup"><span data-stu-id="34b16-1315">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="34b16-1316">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="34b16-1316">timespan</span></span><br/><br/> <span data-ttu-id="34b16-1317">Voorbeeld: 00:30:00 (30 minuten).</span><span class="sxs-lookup"><span data-stu-id="34b16-1317">Example: 00:30:00 (30 minutes).</span></span> |<span data-ttu-id="34b16-1318">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1318">No</span></span> |
| <span data-ttu-id="34b16-1319">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="34b16-1319">writeBatchSize</span></span> |<span data-ttu-id="34b16-1320">Voegt de gegevens in SQL-tabel Hallo wanneer Hallo buffergrootte writeBatchSize bereikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-1320">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="34b16-1321">Geheel getal (aantal rijen)</span><span class="sxs-lookup"><span data-stu-id="34b16-1321">Integer (number of rows)</span></span> |<span data-ttu-id="34b16-1322">Nee (standaard: 100)</span><span class="sxs-lookup"><span data-stu-id="34b16-1322">No (default: 100)</span></span> |
| <span data-ttu-id="34b16-1323">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="34b16-1323">sqlWriterCleanupScript</span></span> |<span data-ttu-id="34b16-1324">Geef een query voor de Kopieeractiviteit tooexecute zodat de gegevens van een bepaald segment wordt opgeschoond.</span><span class="sxs-lookup"><span data-stu-id="34b16-1324">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="34b16-1325">Een query-instructie.</span><span class="sxs-lookup"><span data-stu-id="34b16-1325">A query statement.</span></span> |<span data-ttu-id="34b16-1326">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1326">No</span></span> |
| <span data-ttu-id="34b16-1327">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="34b16-1327">sliceIdentifierColumnName</span></span> |<span data-ttu-id="34b16-1328">Geef kolomnaam voor Kopieeractiviteit toofill met segment-ID automatisch gegenereerd en die is gebruikt tooclean van gegevens van een bepaald segment wanneer opnieuw uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="34b16-1328">Specify column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="34b16-1329">De naam van de kolom van een kolom met gegevenstype binary(32).</span><span class="sxs-lookup"><span data-stu-id="34b16-1329">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="34b16-1330">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1330">No</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-1331">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1331">Example</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-05T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoOracle",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "OracleOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "OracleSink"
                }
            },
            "scheduler": {
                "frequency": "Day",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="34b16-1332">Zie voor meer informatie [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1332">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span></span>

## <a name="postgresql"></a><span data-ttu-id="34b16-1333">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="34b16-1333">PostgreSQL</span></span>

### <a name="linked-service"></a><span data-ttu-id="34b16-1334">Gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="34b16-1334">Linked service</span></span>
<span data-ttu-id="34b16-1335">een PostgreSQL toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**OnPremisesPostgreSql**, en opgeven na eigenschappen in Hallo **typeProperties**sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-1335">toodefine a PostgreSQL linked service, set hello **type** of hello linked service too**OnPremisesPostgreSql**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="34b16-1336">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1336">Property</span></span> | <span data-ttu-id="34b16-1337">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1337">Description</span></span> | <span data-ttu-id="34b16-1338">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1338">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-1339">server</span><span class="sxs-lookup"><span data-stu-id="34b16-1339">server</span></span> |<span data-ttu-id="34b16-1340">Naam van Hallo PostgreSQL-server.</span><span class="sxs-lookup"><span data-stu-id="34b16-1340">Name of hello PostgreSQL server.</span></span> |<span data-ttu-id="34b16-1341">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1341">Yes</span></span> |
| <span data-ttu-id="34b16-1342">database</span><span class="sxs-lookup"><span data-stu-id="34b16-1342">database</span></span> |<span data-ttu-id="34b16-1343">Naam van Hallo PostgreSQL-database.</span><span class="sxs-lookup"><span data-stu-id="34b16-1343">Name of hello PostgreSQL database.</span></span> |<span data-ttu-id="34b16-1344">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1344">Yes</span></span> |
| <span data-ttu-id="34b16-1345">Schema</span><span class="sxs-lookup"><span data-stu-id="34b16-1345">schema</span></span> |<span data-ttu-id="34b16-1346">Naam van Hallo schema in Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="34b16-1346">Name of hello schema in hello database.</span></span> <span data-ttu-id="34b16-1347">Hallo-schemanaam is hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="34b16-1347">hello schema name is case-sensitive.</span></span> |<span data-ttu-id="34b16-1348">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1348">No</span></span> |
| <span data-ttu-id="34b16-1349">authenticationType</span><span class="sxs-lookup"><span data-stu-id="34b16-1349">authenticationType</span></span> |<span data-ttu-id="34b16-1350">Type verificatie gebruikt tooconnect toohello PostgreSQL-database.</span><span class="sxs-lookup"><span data-stu-id="34b16-1350">Type of authentication used tooconnect toohello PostgreSQL database.</span></span> <span data-ttu-id="34b16-1351">Mogelijke waarden zijn: anoniem, basis en Windows.</span><span class="sxs-lookup"><span data-stu-id="34b16-1351">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="34b16-1352">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1352">Yes</span></span> |
| <span data-ttu-id="34b16-1353">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="34b16-1353">username</span></span> |<span data-ttu-id="34b16-1354">Geef de gebruikersnaam als u basisverificatie of Windows-verificatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-1354">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="34b16-1355">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1355">No</span></span> |
| <span data-ttu-id="34b16-1356">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="34b16-1356">password</span></span> |<span data-ttu-id="34b16-1357">Wachtwoord voor gebruikersaccount Hallo die u hebt opgegeven voor Hallo gebruikersnaam opgeven.</span><span class="sxs-lookup"><span data-stu-id="34b16-1357">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="34b16-1358">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1358">No</span></span> |
| <span data-ttu-id="34b16-1359">gatewayName</span><span class="sxs-lookup"><span data-stu-id="34b16-1359">gatewayName</span></span> |<span data-ttu-id="34b16-1360">Naam van Hallo-gateway die Hallo Data Factory-service moet tooconnect toohello lokale PostgreSQL-database gebruiken.</span><span class="sxs-lookup"><span data-stu-id="34b16-1360">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises PostgreSQL database.</span></span> |<span data-ttu-id="34b16-1361">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1361">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-1362">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1362">Example</span></span>

```json
{
    "name": "OnPremPostgreSqlLinkedService",
    "properties": {
        "type": "OnPremisesPostgreSql",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
<span data-ttu-id="34b16-1363">Zie voor meer informatie [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#linked-service-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1363">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="34b16-1364">Gegevensset</span><span class="sxs-lookup"><span data-stu-id="34b16-1364">Dataset</span></span>
<span data-ttu-id="34b16-1365">toodefine een gegevensset PostgreSQL set Hallo **type** van Hallo gegevensset te**RelationalTable**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-1365">toodefine a PostgreSQL dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="34b16-1366">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1366">Property</span></span> | <span data-ttu-id="34b16-1367">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1367">Description</span></span> | <span data-ttu-id="34b16-1368">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1368">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-1369">tableName</span><span class="sxs-lookup"><span data-stu-id="34b16-1369">tableName</span></span> |<span data-ttu-id="34b16-1370">De naam van de tabel Hallo in Hallo PostgreSQL-Database-instantie waarnaar de gekoppelde service verwijst.</span><span class="sxs-lookup"><span data-stu-id="34b16-1370">Name of hello table in hello PostgreSQL Database instance that linked service refers to.</span></span> <span data-ttu-id="34b16-1371">Hallo tableName is hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="34b16-1371">hello tableName is case-sensitive.</span></span> |<span data-ttu-id="34b16-1372">Nee (als **query** van **RelationalSource** is opgegeven)</span><span class="sxs-lookup"><span data-stu-id="34b16-1372">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-1373">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1373">Example</span></span>
```json
{
    "name": "PostgreSqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremPostgreSqlLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="34b16-1374">Zie voor meer informatie [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#dataset-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1374">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="34b16-1375">Relationele gegevensbron in de kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="34b16-1375">Relational Source in Copy Activity</span></span>
<span data-ttu-id="34b16-1376">Als u gegevens uit een PostgreSQL-database kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**RelationalSource**, en opgeven na eigenschappen in Hallo **bron**sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-1376">If you are copying data from a PostgreSQL database, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="34b16-1377">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1377">Property</span></span> | <span data-ttu-id="34b16-1378">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1378">Description</span></span> | <span data-ttu-id="34b16-1379">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="34b16-1379">Allowed values</span></span> | <span data-ttu-id="34b16-1380">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1380">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-1381">query</span><span class="sxs-lookup"><span data-stu-id="34b16-1381">query</span></span> |<span data-ttu-id="34b16-1382">Hallo aangepaste query tooread gegevens worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-1382">Use hello custom query tooread data.</span></span> |<span data-ttu-id="34b16-1383">SQL-query-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="34b16-1383">SQL query string.</span></span> <span data-ttu-id="34b16-1384">Bijvoorbeeld: "query": "Selecteer * uit \"MySchema\".\" MyTable\"'.</span><span class="sxs-lookup"><span data-stu-id="34b16-1384">For example: "query": "select * from \"MySchema\".\"MyTable\"".</span></span> |<span data-ttu-id="34b16-1385">Nee (als **tableName** van **gegevensset** is opgegeven)</span><span class="sxs-lookup"><span data-stu-id="34b16-1385">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-1386">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1386">Example</span></span>

```json
{
    "name": "CopyPostgreSqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from \"public\".\"usstates\""
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "PostgreSqlDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobPostgreSqlDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "PostgreSqlToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="34b16-1387">Zie voor meer informatie [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#copy-activity-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1387">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#copy-activity-properties) article.</span></span>

## <a name="sap-business-warehouse"></a><span data-ttu-id="34b16-1388">SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="34b16-1388">SAP Business Warehouse</span></span>


### <a name="linked-service"></a><span data-ttu-id="34b16-1389">Gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="34b16-1389">Linked service</span></span>
<span data-ttu-id="34b16-1390">een SAP Business Warehouse (BW) toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**SapBw**, en opgeven na eigenschappen in Hallo **typeProperties**sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-1390">toodefine a SAP Business Warehouse (BW) linked service, set hello **type** of hello linked service too**SapBw**, and specify following properties in hello **typeProperties** section:</span></span>  

<span data-ttu-id="34b16-1391">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1391">Property</span></span> | <span data-ttu-id="34b16-1392">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1392">Description</span></span> | <span data-ttu-id="34b16-1393">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="34b16-1393">Allowed values</span></span> | <span data-ttu-id="34b16-1394">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1394">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="34b16-1395">server</span><span class="sxs-lookup"><span data-stu-id="34b16-1395">server</span></span> | <span data-ttu-id="34b16-1396">Naam van het Hallo-server op welke Hallo SAP BW exemplaar zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="34b16-1396">Name of hello server on which hello SAP BW instance resides.</span></span> | <span data-ttu-id="34b16-1397">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="34b16-1397">string</span></span> | <span data-ttu-id="34b16-1398">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1398">Yes</span></span>
<span data-ttu-id="34b16-1399">systemNumber</span><span class="sxs-lookup"><span data-stu-id="34b16-1399">systemNumber</span></span> | <span data-ttu-id="34b16-1400">Systeem aantal Hallo SAP BW-systeem.</span><span class="sxs-lookup"><span data-stu-id="34b16-1400">System number of hello SAP BW system.</span></span> | <span data-ttu-id="34b16-1401">Twee cijfers decimaal getal weergegeven als een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="34b16-1401">Two-digit decimal number represented as a string.</span></span> | <span data-ttu-id="34b16-1402">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1402">Yes</span></span>
<span data-ttu-id="34b16-1403">clientId</span><span class="sxs-lookup"><span data-stu-id="34b16-1403">clientId</span></span> | <span data-ttu-id="34b16-1404">Client-ID van de client Hallo in Hallo SAP W system.</span><span class="sxs-lookup"><span data-stu-id="34b16-1404">Client ID of hello client in hello SAP W system.</span></span> | <span data-ttu-id="34b16-1405">Drie cijfers decimaal getal weergegeven als een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="34b16-1405">Three-digit decimal number represented as a string.</span></span> | <span data-ttu-id="34b16-1406">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1406">Yes</span></span>
<span data-ttu-id="34b16-1407">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="34b16-1407">username</span></span> | <span data-ttu-id="34b16-1408">Naam van het Hallo-gebruiker met toegang toohello SAP-server</span><span class="sxs-lookup"><span data-stu-id="34b16-1408">Name of hello user who has access toohello SAP server</span></span> | <span data-ttu-id="34b16-1409">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="34b16-1409">string</span></span> | <span data-ttu-id="34b16-1410">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1410">Yes</span></span>
<span data-ttu-id="34b16-1411">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="34b16-1411">password</span></span> | <span data-ttu-id="34b16-1412">Wachtwoord voor gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="34b16-1412">Password for hello user.</span></span> | <span data-ttu-id="34b16-1413">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="34b16-1413">string</span></span> | <span data-ttu-id="34b16-1414">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1414">Yes</span></span>
<span data-ttu-id="34b16-1415">gatewayName</span><span class="sxs-lookup"><span data-stu-id="34b16-1415">gatewayName</span></span> | <span data-ttu-id="34b16-1416">Naam van Hallo-gateway die Hallo Data Factory-service moet tooconnect toohello lokale SAP BW exemplaar gebruiken.</span><span class="sxs-lookup"><span data-stu-id="34b16-1416">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SAP BW instance.</span></span> | <span data-ttu-id="34b16-1417">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="34b16-1417">string</span></span> | <span data-ttu-id="34b16-1418">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1418">Yes</span></span>
<span data-ttu-id="34b16-1419">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="34b16-1419">encryptedCredential</span></span> | <span data-ttu-id="34b16-1420">Hallo versleutelde referentie-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="34b16-1420">hello encrypted credential string.</span></span> | <span data-ttu-id="34b16-1421">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="34b16-1421">string</span></span> | <span data-ttu-id="34b16-1422">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1422">No</span></span>

#### <a name="example"></a><span data-ttu-id="34b16-1423">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1423">Example</span></span>

```json
{
    "name": "SapBwLinkedService",
    "properties": {
        "type": "SapBw",
        "typeProperties": {
            "server": "<server name>",
            "systemNumber": "<system number>",
            "clientId": "<client id>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="34b16-1424">Zie voor meer informatie [SAP Business Warehouse-connector](data-factory-sap-business-warehouse-connector.md#linked-service-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1424">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="34b16-1425">Gegevensset</span><span class="sxs-lookup"><span data-stu-id="34b16-1425">Dataset</span></span>
<span data-ttu-id="34b16-1426">toodefine een gegevensset SAP BW set Hallo **type** van Hallo gegevensset te**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="34b16-1426">toodefine a SAP BW dataset, set hello **type** of hello dataset too**RelationalTable**.</span></span> <span data-ttu-id="34b16-1427">Er zijn geen type-specifieke eigenschappen ondersteund voor SAP BW-gegevensset Hallo van het type **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="34b16-1427">There are no type-specific properties supported for hello SAP BW dataset of type **RelationalTable**.</span></span>  

#### <a name="example"></a><span data-ttu-id="34b16-1428">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1428">Example</span></span>

```json
{
    "name": "SapBwDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapBwLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
<span data-ttu-id="34b16-1429">Zie voor meer informatie [SAP Business Warehouse-connector](data-factory-sap-business-warehouse-connector.md#dataset-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1429">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="34b16-1430">Relationele gegevensbron in de kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="34b16-1430">Relational Source in Copy Activity</span></span>
<span data-ttu-id="34b16-1431">Als u gegevens uit een SAP Business Warehouse kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**RelationalSource**, en opgeven na eigenschappen in Hallo **bron**sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-1431">If you are copying data from SAP Business Warehouse, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="34b16-1432">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1432">Property</span></span> | <span data-ttu-id="34b16-1433">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1433">Description</span></span> | <span data-ttu-id="34b16-1434">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="34b16-1434">Allowed values</span></span> | <span data-ttu-id="34b16-1435">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1435">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-1436">query</span><span class="sxs-lookup"><span data-stu-id="34b16-1436">query</span></span> | <span data-ttu-id="34b16-1437">Hiermee geeft u Hallo MDX-query tooread gegevens van Hallo SAP BW-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="34b16-1437">Specifies hello MDX query tooread data from hello SAP BW instance.</span></span> | <span data-ttu-id="34b16-1438">MDX-query.</span><span class="sxs-lookup"><span data-stu-id="34b16-1438">MDX query.</span></span> | <span data-ttu-id="34b16-1439">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1439">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-1440">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1440">Example</span></span>

```json
{
    "name": "CopySapBwToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "<MDX query for SAP BW>"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "SapBwDataset"
            }],
            "outputs": [{
                "name": "AzureBlobDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SapBwToBlob"
        }],
        "start": "2017-03-01T18:00:00",
        "end": "2017-03-01T19:00:00"
    }
}
```

<span data-ttu-id="34b16-1441">Zie voor meer informatie [SAP Business Warehouse-connector](data-factory-sap-business-warehouse-connector.md#copy-activity-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1441">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#copy-activity-properties) article.</span></span> 

## <a name="sap-hana"></a><span data-ttu-id="34b16-1442">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="34b16-1442">SAP HANA</span></span>

### <a name="linked-service"></a><span data-ttu-id="34b16-1443">Gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="34b16-1443">Linked service</span></span>
<span data-ttu-id="34b16-1444">een SAP HANA toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**SapHana**, en opgeven na eigenschappen in Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-1444">toodefine a SAP HANA linked service, set hello **type** of hello linked service too**SapHana**, and specify following properties in hello **typeProperties** section:</span></span>  

<span data-ttu-id="34b16-1445">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1445">Property</span></span> | <span data-ttu-id="34b16-1446">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1446">Description</span></span> | <span data-ttu-id="34b16-1447">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="34b16-1447">Allowed values</span></span> | <span data-ttu-id="34b16-1448">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1448">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="34b16-1449">server</span><span class="sxs-lookup"><span data-stu-id="34b16-1449">server</span></span> | <span data-ttu-id="34b16-1450">Naam van het Hallo-server op welke Hallo SAP HANA exemplaar zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="34b16-1450">Name of hello server on which hello SAP HANA instance resides.</span></span> <span data-ttu-id="34b16-1451">Als de server een aangepaste poort gebruikt is, geeft u `server:port`.</span><span class="sxs-lookup"><span data-stu-id="34b16-1451">If your server is using a customized port, specify `server:port`.</span></span> | <span data-ttu-id="34b16-1452">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="34b16-1452">string</span></span> | <span data-ttu-id="34b16-1453">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1453">Yes</span></span>
<span data-ttu-id="34b16-1454">authenticationType</span><span class="sxs-lookup"><span data-stu-id="34b16-1454">authenticationType</span></span> | <span data-ttu-id="34b16-1455">Het type verificatie.</span><span class="sxs-lookup"><span data-stu-id="34b16-1455">Type of authentication.</span></span> | <span data-ttu-id="34b16-1456">De tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="34b16-1456">string.</span></span> <span data-ttu-id="34b16-1457">'Basic' of 'Windows'</span><span class="sxs-lookup"><span data-stu-id="34b16-1457">"Basic" or "Windows"</span></span> | <span data-ttu-id="34b16-1458">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1458">Yes</span></span> 
<span data-ttu-id="34b16-1459">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="34b16-1459">username</span></span> | <span data-ttu-id="34b16-1460">Naam van het Hallo-gebruiker met toegang toohello SAP-server</span><span class="sxs-lookup"><span data-stu-id="34b16-1460">Name of hello user who has access toohello SAP server</span></span> | <span data-ttu-id="34b16-1461">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="34b16-1461">string</span></span> | <span data-ttu-id="34b16-1462">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1462">Yes</span></span>
<span data-ttu-id="34b16-1463">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="34b16-1463">password</span></span> | <span data-ttu-id="34b16-1464">Wachtwoord voor gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="34b16-1464">Password for hello user.</span></span> | <span data-ttu-id="34b16-1465">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="34b16-1465">string</span></span> | <span data-ttu-id="34b16-1466">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1466">Yes</span></span>
<span data-ttu-id="34b16-1467">gatewayName</span><span class="sxs-lookup"><span data-stu-id="34b16-1467">gatewayName</span></span> | <span data-ttu-id="34b16-1468">Naam van Hallo-gateway die Hallo Data Factory-service moet tooconnect toohello lokale SAP HANA-exemplaar gebruiken.</span><span class="sxs-lookup"><span data-stu-id="34b16-1468">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SAP HANA instance.</span></span> | <span data-ttu-id="34b16-1469">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="34b16-1469">string</span></span> | <span data-ttu-id="34b16-1470">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1470">Yes</span></span>
<span data-ttu-id="34b16-1471">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="34b16-1471">encryptedCredential</span></span> | <span data-ttu-id="34b16-1472">Hallo versleutelde referentie-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="34b16-1472">hello encrypted credential string.</span></span> | <span data-ttu-id="34b16-1473">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="34b16-1473">string</span></span> | <span data-ttu-id="34b16-1474">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1474">No</span></span>

#### <a name="example"></a><span data-ttu-id="34b16-1475">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1475">Example</span></span>

```json
{
    "name": "SapHanaLinkedService",
    "properties": {
        "type": "SapHana",
        "typeProperties": {
            "server": "<server name>",
            "authenticationType": "<Basic, or Windows>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}

```
<span data-ttu-id="34b16-1476">Zie voor meer informatie [SAP HANA-connector](data-factory-sap-hana-connector.md#linked-service-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1476">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#linked-service-properties) article.</span></span>
 
### <a name="dataset"></a><span data-ttu-id="34b16-1477">Gegevensset</span><span class="sxs-lookup"><span data-stu-id="34b16-1477">Dataset</span></span>
<span data-ttu-id="34b16-1478">toodefine een SAP HANA-gegevensset set Hallo **type** van Hallo gegevensset te**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="34b16-1478">toodefine a SAP HANA dataset, set hello **type** of hello dataset too**RelationalTable**.</span></span> <span data-ttu-id="34b16-1479">Er zijn geen type-specifieke eigenschappen ondersteund voor SAP HANA-gegevensset Hallo van het type **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="34b16-1479">There are no type-specific properties supported for hello SAP HANA dataset of type **RelationalTable**.</span></span> 

#### <a name="example"></a><span data-ttu-id="34b16-1480">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1480">Example</span></span>

```json
{
    "name": "SapHanaDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapHanaLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
<span data-ttu-id="34b16-1481">Zie voor meer informatie [SAP HANA-connector](data-factory-sap-hana-connector.md#dataset-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1481">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="34b16-1482">Relationele gegevensbron in de kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="34b16-1482">Relational Source in Copy Activity</span></span>
<span data-ttu-id="34b16-1483">Als u gegevens uit een SAP HANA-gegevensarchief kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**RelationalSource**, en opgeven na eigenschappen in Hallo **bron**sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-1483">If you are copying data from a SAP HANA data store, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="34b16-1484">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1484">Property</span></span> | <span data-ttu-id="34b16-1485">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1485">Description</span></span> | <span data-ttu-id="34b16-1486">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="34b16-1486">Allowed values</span></span> | <span data-ttu-id="34b16-1487">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1487">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-1488">query</span><span class="sxs-lookup"><span data-stu-id="34b16-1488">query</span></span> | <span data-ttu-id="34b16-1489">Hiermee geeft u Hallo SQL query tooread gegevens van Hallo SAP HANA-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="34b16-1489">Specifies hello SQL query tooread data from hello SAP HANA instance.</span></span> | <span data-ttu-id="34b16-1490">SQL-query.</span><span class="sxs-lookup"><span data-stu-id="34b16-1490">SQL query.</span></span> | <span data-ttu-id="34b16-1491">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1491">Yes</span></span> |


#### <a name="example"></a><span data-ttu-id="34b16-1492">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1492">Example</span></span>


```json
{
    "name": "CopySapHanaToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "<SQL Query for HANA>"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "SapHanaDataset"
            }],
            "outputs": [{
                "name": "AzureBlobDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SapHanaToBlob"
        }],
        "start": "2017-03-01T18:00:00",
        "end": "2017-03-01T19:00:00"
    }
}
```

<span data-ttu-id="34b16-1493">Zie voor meer informatie [SAP HANA-connector](data-factory-sap-hana-connector.md#copy-activity-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1493">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#copy-activity-properties) article.</span></span>


## <a name="sql-server"></a><span data-ttu-id="34b16-1494">SQL Server</span><span class="sxs-lookup"><span data-stu-id="34b16-1494">SQL Server</span></span>

### <a name="linked-service"></a><span data-ttu-id="34b16-1495">Gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="34b16-1495">Linked service</span></span>
<span data-ttu-id="34b16-1496">Maken van een gekoppelde service van het type **OnPremisesSqlServer** toolink een lokale SQL Server-database tooa data factory.</span><span class="sxs-lookup"><span data-stu-id="34b16-1496">You create a linked service of type **OnPremisesSqlServer** toolink an on-premises SQL Server database tooa data factory.</span></span> <span data-ttu-id="34b16-1497">Hallo volgende tabel biedt een beschrijving voor de service voor JSON-elementen specifieke tooon-premises SQL Server gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="34b16-1497">hello following table provides description for JSON elements specific tooon-premises SQL Server linked service.</span></span>

<span data-ttu-id="34b16-1498">Hallo volgende tabel bevat een beschrijving voor JSON-elementen specifieke tooSQL gekoppelde Server-service.</span><span class="sxs-lookup"><span data-stu-id="34b16-1498">hello following table provides description for JSON elements specific tooSQL Server linked service.</span></span>

| <span data-ttu-id="34b16-1499">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1499">Property</span></span> | <span data-ttu-id="34b16-1500">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1500">Description</span></span> | <span data-ttu-id="34b16-1501">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1501">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-1502">type</span><span class="sxs-lookup"><span data-stu-id="34b16-1502">type</span></span> |<span data-ttu-id="34b16-1503">Hallo type eigenschap moet worden ingesteld op: **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="34b16-1503">hello type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="34b16-1504">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1504">Yes</span></span> |
| <span data-ttu-id="34b16-1505">connectionString</span><span class="sxs-lookup"><span data-stu-id="34b16-1505">connectionString</span></span> |<span data-ttu-id="34b16-1506">Geef connectionString informatie nodig tooconnect toohello lokale SQL Server-database met behulp van de SQL-verificatie of de Windows-verificatie.</span><span class="sxs-lookup"><span data-stu-id="34b16-1506">Specify connectionString information needed tooconnect toohello on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="34b16-1507">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1507">Yes</span></span> |
| <span data-ttu-id="34b16-1508">gatewayName</span><span class="sxs-lookup"><span data-stu-id="34b16-1508">gatewayName</span></span> |<span data-ttu-id="34b16-1509">Naam van Hallo-gateway die Hallo Data Factory-service moet tooconnect toohello lokale SQL Server-database gebruiken.</span><span class="sxs-lookup"><span data-stu-id="34b16-1509">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SQL Server database.</span></span> |<span data-ttu-id="34b16-1510">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1510">Yes</span></span> |
| <span data-ttu-id="34b16-1511">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="34b16-1511">username</span></span> |<span data-ttu-id="34b16-1512">Geef de gebruikersnaam als u Windows-verificatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-1512">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="34b16-1513">Voorbeeld: **domainname\\gebruikersnaam**.</span><span class="sxs-lookup"><span data-stu-id="34b16-1513">Example: **domainname\\username**.</span></span> |<span data-ttu-id="34b16-1514">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1514">No</span></span> |
| <span data-ttu-id="34b16-1515">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="34b16-1515">password</span></span> |<span data-ttu-id="34b16-1516">Wachtwoord voor gebruikersaccount Hallo die u hebt opgegeven voor Hallo gebruikersnaam opgeven.</span><span class="sxs-lookup"><span data-stu-id="34b16-1516">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="34b16-1517">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1517">No</span></span> |

<span data-ttu-id="34b16-1518">U kunt referenties met een Hallo versleutelen **nieuw AzureRmDataFactoryEncryptValue** cmdlet en in de verbindingsreeks hello gebruiken, zoals wordt weergegeven in het volgende voorbeeld Hallo (**EncryptedCredential** eigenschap):</span><span class="sxs-lookup"><span data-stu-id="34b16-1518">You can encrypt credentials using hello **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in hello connection string as shown in hello following example (**EncryptedCredential** property):</span></span>  

```json
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a><span data-ttu-id="34b16-1519">Voorbeeld: JSON voor het gebruik van SQL-verificatie</span><span class="sxs-lookup"><span data-stu-id="34b16-1519">Example: JSON for using SQL Authentication</span></span>

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
#### <a name="example-json-for-using-windows-authentication"></a><span data-ttu-id="34b16-1520">Voorbeeld: JSON voor het gebruik van Windows-verificatie</span><span class="sxs-lookup"><span data-stu-id="34b16-1520">Example: JSON for using Windows Authentication</span></span>

<span data-ttu-id="34b16-1521">Als de gebruikersnaam en wachtwoord zijn opgegeven, gateway maakt gebruik van deze tooimpersonate Hallo opgegeven gebruiker account tooconnect toohello lokale SQL Server-database.</span><span class="sxs-lookup"><span data-stu-id="34b16-1521">If username and password are specified, gateway uses them tooimpersonate hello specified user account tooconnect toohello on-premises SQL Server database.</span></span> <span data-ttu-id="34b16-1522">Gatewayserver verbindt anders toohello SQL-Server rechtstreeks met de beveiligingscontext Hallo van Gateway (het starten van de account).</span><span class="sxs-lookup"><span data-stu-id="34b16-1522">Otherwise, gateway connects toohello SQL Server directly with hello security context of Gateway (its startup account).</span></span>

```json
{
    "Name": " MyOnPremisesSQLDB",
    "Properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
            "username": "<domain\\username>",
            "password": "<password>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="34b16-1523">Zie voor meer informatie [SQL Server-connector](data-factory-sqlserver-connector.md#linked-service-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1523">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="34b16-1524">Gegevensset</span><span class="sxs-lookup"><span data-stu-id="34b16-1524">Dataset</span></span>
<span data-ttu-id="34b16-1525">toodefine een SQL Server-gegevensset set Hallo **type** van Hallo gegevensset te**SqlServerTable**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-1525">toodefine a SQL Server dataset, set hello **type** of hello dataset too**SqlServerTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="34b16-1526">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1526">Property</span></span> | <span data-ttu-id="34b16-1527">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1527">Description</span></span> | <span data-ttu-id="34b16-1528">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1528">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-1529">tableName</span><span class="sxs-lookup"><span data-stu-id="34b16-1529">tableName</span></span> |<span data-ttu-id="34b16-1530">De naam van het Hallo-tabel of weergave in Hallo SQL Server Database-instantie waarnaar de gekoppelde service verwijst.</span><span class="sxs-lookup"><span data-stu-id="34b16-1530">Name of hello table or view in hello SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="34b16-1531">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1531">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-1532">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1532">Example</span></span>
```json
{
    "name": "SqlServerInput",
    "properties": {
        "type": "SqlServerTable",
        "linkedServiceName": "SqlServerLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="34b16-1533">Zie voor meer informatie [SQL Server-connector](data-factory-sqlserver-connector.md#dataset-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1533">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-source-in-copy-activity"></a><span data-ttu-id="34b16-1534">SQL-bron in de kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="34b16-1534">Sql Source in Copy Activity</span></span>
<span data-ttu-id="34b16-1535">Als u gegevens uit een SQL Server-database kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**SqlSource**, en opgeven na eigenschappen in Hallo **bron** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-1535">If you are copying data from a SQL Server database, set hello **source type** of hello copy activity too**SqlSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="34b16-1536">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1536">Property</span></span> | <span data-ttu-id="34b16-1537">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1537">Description</span></span> | <span data-ttu-id="34b16-1538">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="34b16-1538">Allowed values</span></span> | <span data-ttu-id="34b16-1539">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1539">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-1540">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="34b16-1540">sqlReaderQuery</span></span> |<span data-ttu-id="34b16-1541">Hallo aangepaste query tooread gegevens worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-1541">Use hello custom query tooread data.</span></span> |<span data-ttu-id="34b16-1542">SQL-query-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="34b16-1542">SQL query string.</span></span> <span data-ttu-id="34b16-1543">Bijvoorbeeld: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="34b16-1543">For example: `select * from MyTable`.</span></span> <span data-ttu-id="34b16-1544">Kan naar meerdere tabellen uit Hallo database waarnaar wordt verwezen door de invoergegevensset Hallo verwijzen.</span><span class="sxs-lookup"><span data-stu-id="34b16-1544">May reference multiple tables from hello database referenced by hello input dataset.</span></span> <span data-ttu-id="34b16-1545">Als niet wordt opgegeven, Hallo SQL-instructie die is uitgevoerd: Selecteer een van de MyTable.</span><span class="sxs-lookup"><span data-stu-id="34b16-1545">If not specified, hello SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="34b16-1546">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1546">No</span></span> |
| <span data-ttu-id="34b16-1547">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="34b16-1547">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="34b16-1548">Naam van Hallo opgeslagen procedure die gegevens uit Hallo brontabel leest.</span><span class="sxs-lookup"><span data-stu-id="34b16-1548">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="34b16-1549">Naam van Hallo opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="34b16-1549">Name of hello stored procedure.</span></span> |<span data-ttu-id="34b16-1550">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1550">No</span></span> |
| <span data-ttu-id="34b16-1551">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="34b16-1551">storedProcedureParameters</span></span> |<span data-ttu-id="34b16-1552">Parameters voor Hallo opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="34b16-1552">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="34b16-1553">Naam/waarde-paren.</span><span class="sxs-lookup"><span data-stu-id="34b16-1553">Name/value pairs.</span></span> <span data-ttu-id="34b16-1554">Namen en hoofdlettergebruik van parameters moeten overeenkomen met Hallo namen en hoofdlettergebruik van Hallo opgeslagen procedureparameters.</span><span class="sxs-lookup"><span data-stu-id="34b16-1554">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="34b16-1555">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1555">No</span></span> |

<span data-ttu-id="34b16-1556">Als hello **sqlReaderQuery** is opgegeven voor Hallo SqlSource, hello Kopieeractiviteit deze query wordt uitgevoerd tegen Hallo SQL Server-Database tooget Hallo brongegevens.</span><span class="sxs-lookup"><span data-stu-id="34b16-1556">If hello **sqlReaderQuery** is specified for hello SqlSource, hello Copy Activity runs this query against hello SQL Server Database source tooget hello data.</span></span>

<span data-ttu-id="34b16-1557">U kunt ook een opgeslagen procedure opgeven door te geven Hallo **sqlReaderStoredProcedureName** en **storedProcedureParameters** (als hello opgeslagen procedure parameters zijn vereist).</span><span class="sxs-lookup"><span data-stu-id="34b16-1557">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="34b16-1558">Als u geen sqlReaderQuery of sqlReaderStoredProcedureName opgeeft, zijn gedefinieerd in de sectie structuur Hallo Hallo-kolommen gebruikte toobuild een toorun selectiequery tegen Hallo SQL Server-Database.</span><span class="sxs-lookup"><span data-stu-id="34b16-1558">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section are used toobuild a select query toorun against hello SQL Server Database.</span></span> <span data-ttu-id="34b16-1559">Als de definitie van de gegevensset Hallo geen Hallo structuur, worden alle kolommen uit Hallo tabel geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="34b16-1559">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

> [!NOTE]
> <span data-ttu-id="34b16-1560">Als u werkt met **sqlReaderStoredProcedureName**, moet u nog steeds toospecify een waarde voor Hallo **tableName** eigenschap in de gegevensset Hallo JSON.</span><span class="sxs-lookup"><span data-stu-id="34b16-1560">When you use **sqlReaderStoredProcedureName**, you still need toospecify a value for hello **tableName** property in hello dataset JSON.</span></span> <span data-ttu-id="34b16-1561">Er zijn geen controles uitgevoerd voor deze tabel al.</span><span class="sxs-lookup"><span data-stu-id="34b16-1561">There are no validations performed against this table though.</span></span>


#### <a name="example"></a><span data-ttu-id="34b16-1562">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1562">Example</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "SqlServertoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " SqlServerInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="34b16-1563">In dit voorbeeld **sqlReaderQuery** voor Hallo SqlSource is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="34b16-1563">In this example, **sqlReaderQuery** is specified for hello SqlSource.</span></span> <span data-ttu-id="34b16-1564">Deze query Hallo Kopieeractiviteit uitgevoerd tegen Hallo tooget SQL Server-Database-Hallo brongegevens.</span><span class="sxs-lookup"><span data-stu-id="34b16-1564">hello Copy Activity runs this query against hello SQL Server Database source tooget hello data.</span></span> <span data-ttu-id="34b16-1565">U kunt ook een opgeslagen procedure opgeven door te geven Hallo **sqlReaderStoredProcedureName** en **storedProcedureParameters** (als hello opgeslagen procedure parameters zijn vereist).</span><span class="sxs-lookup"><span data-stu-id="34b16-1565">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span> <span data-ttu-id="34b16-1566">Hallo sqlReaderQuery kunt verwijzen naar meerdere tabellen in Hallo database waarnaar wordt verwezen door Hallo invoergegevensset.</span><span class="sxs-lookup"><span data-stu-id="34b16-1566">hello sqlReaderQuery can reference multiple tables within hello database referenced by hello input dataset.</span></span> <span data-ttu-id="34b16-1567">Het is niet beperkt tooonly Hallo tabel van deze dataset tableName typeProperty Hallo ingesteld.</span><span class="sxs-lookup"><span data-stu-id="34b16-1567">It is not limited tooonly hello table set as hello dataset's tableName typeProperty.</span></span>

<span data-ttu-id="34b16-1568">Als u geen sqlReaderQuery of sqlReaderStoredProcedureName opgeeft, zijn gedefinieerd in de sectie structuur Hallo Hallo-kolommen gebruikte toobuild een toorun selectiequery tegen Hallo SQL Server-Database.</span><span class="sxs-lookup"><span data-stu-id="34b16-1568">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section are used toobuild a select query toorun against hello SQL Server Database.</span></span> <span data-ttu-id="34b16-1569">Als de definitie van de gegevensset Hallo geen Hallo structuur, worden alle kolommen uit Hallo tabel geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="34b16-1569">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

<span data-ttu-id="34b16-1570">Zie voor meer informatie [SQL Server-connector](data-factory-sqlserver-connector.md#copy-activity-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1570">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-sink-in-copy-activity"></a><span data-ttu-id="34b16-1571">SQL-Sink in de kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="34b16-1571">Sql Sink in Copy Activity</span></span>
<span data-ttu-id="34b16-1572">Als u gegevens tooa SQL Server-database kopiëren wilt, stelt u Hallo **type sink** Hallo kopieeractiviteit te**SqlSink**, en opgeven na eigenschappen in Hallo **sink** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-1572">If you are copying data tooa SQL Server database, set hello **sink type** of hello copy activity too**SqlSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="34b16-1573">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1573">Property</span></span> | <span data-ttu-id="34b16-1574">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1574">Description</span></span> | <span data-ttu-id="34b16-1575">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="34b16-1575">Allowed values</span></span> | <span data-ttu-id="34b16-1576">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1576">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-1577">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="34b16-1577">writeBatchTimeout</span></span> |<span data-ttu-id="34b16-1578">Wachttijd voor Hallo batch insert-bewerking toocomplete voordat een time-out optreedt.</span><span class="sxs-lookup"><span data-stu-id="34b16-1578">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="34b16-1579">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="34b16-1579">timespan</span></span><br/><br/> <span data-ttu-id="34b16-1580">Voorbeeld: "00: 30:00 ' (30 minuten).</span><span class="sxs-lookup"><span data-stu-id="34b16-1580">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="34b16-1581">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1581">No</span></span> |
| <span data-ttu-id="34b16-1582">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="34b16-1582">writeBatchSize</span></span> |<span data-ttu-id="34b16-1583">Voegt de gegevens in SQL-tabel Hallo wanneer Hallo buffergrootte writeBatchSize bereikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-1583">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="34b16-1584">Geheel getal (aantal rijen)</span><span class="sxs-lookup"><span data-stu-id="34b16-1584">Integer (number of rows)</span></span> |<span data-ttu-id="34b16-1585">Nee (standaard: 10000)</span><span class="sxs-lookup"><span data-stu-id="34b16-1585">No (default: 10000)</span></span> |
| <span data-ttu-id="34b16-1586">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="34b16-1586">sqlWriterCleanupScript</span></span> |<span data-ttu-id="34b16-1587">Query voor de Kopieeractiviteit tooexecute opgeven zodat de gegevens van een bepaald segment wordt opgeschoond.</span><span class="sxs-lookup"><span data-stu-id="34b16-1587">Specify query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="34b16-1588">Zie voor meer informatie [herhaalbaarheid](#repeatability-during-copy) sectie.</span><span class="sxs-lookup"><span data-stu-id="34b16-1588">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="34b16-1589">Een query-instructie.</span><span class="sxs-lookup"><span data-stu-id="34b16-1589">A query statement.</span></span> |<span data-ttu-id="34b16-1590">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1590">No</span></span> |
| <span data-ttu-id="34b16-1591">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="34b16-1591">sliceIdentifierColumnName</span></span> |<span data-ttu-id="34b16-1592">Geef kolomnaam voor Kopieeractiviteit toofill met segment-ID automatisch gegenereerd en die is gebruikt tooclean van gegevens van een bepaald segment wanneer opnieuw uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="34b16-1592">Specify column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> <span data-ttu-id="34b16-1593">Zie voor meer informatie [herhaalbaarheid](#repeatability-during-copy) sectie.</span><span class="sxs-lookup"><span data-stu-id="34b16-1593">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="34b16-1594">De naam van de kolom van een kolom met gegevenstype binary(32).</span><span class="sxs-lookup"><span data-stu-id="34b16-1594">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="34b16-1595">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1595">No</span></span> |
| <span data-ttu-id="34b16-1596">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="34b16-1596">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="34b16-1597">Naam van Hallo opgeslagen procedure die upserts (updates/INSERT) gegevens in de doeltabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="34b16-1597">Name of hello stored procedure that upserts (updates/inserts) data into hello target table.</span></span> |<span data-ttu-id="34b16-1598">Naam van Hallo opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="34b16-1598">Name of hello stored procedure.</span></span> |<span data-ttu-id="34b16-1599">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1599">No</span></span> |
| <span data-ttu-id="34b16-1600">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="34b16-1600">storedProcedureParameters</span></span> |<span data-ttu-id="34b16-1601">Parameters voor Hallo opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="34b16-1601">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="34b16-1602">Naam/waarde-paren.</span><span class="sxs-lookup"><span data-stu-id="34b16-1602">Name/value pairs.</span></span> <span data-ttu-id="34b16-1603">Namen en hoofdlettergebruik van parameters moeten overeenkomen met Hallo namen en hoofdlettergebruik van Hallo opgeslagen procedureparameters.</span><span class="sxs-lookup"><span data-stu-id="34b16-1603">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="34b16-1604">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1604">No</span></span> |
| <span data-ttu-id="34b16-1605">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="34b16-1605">sqlWriterTableType</span></span> |<span data-ttu-id="34b16-1606">Geef tabel type naam toobe in Hallo opgeslagen procedure gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-1606">Specify table type name toobe used in hello stored procedure.</span></span> <span data-ttu-id="34b16-1607">Kopieeractiviteit beschikbaar Hallo-gegevens worden verplaatst in een tijdelijke tabel met dit tabeltype.</span><span class="sxs-lookup"><span data-stu-id="34b16-1607">Copy activity makes hello data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="34b16-1608">Opgeslagen procedurecode kunt Hallo gegevens wordt gekopieerd met de bestaande gegevens vervolgens samenvoegen.</span><span class="sxs-lookup"><span data-stu-id="34b16-1608">Stored procedure code can then merge hello data being copied with existing data.</span></span> |<span data-ttu-id="34b16-1609">Een typenaam van de tabel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1609">A table type name.</span></span> |<span data-ttu-id="34b16-1610">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1610">No</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-1611">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1611">Example</span></span>
<span data-ttu-id="34b16-1612">Hallo pijplijn bevat een Kopieeractiviteit die is geconfigureerd toouse deze invoer- en uitvoergegevenssets en geplande toorun is om het uur.</span><span class="sxs-lookup"><span data-stu-id="34b16-1612">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="34b16-1613">Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**BlobSource** en **sink** type is ingesteld, te**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="34b16-1613">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlSink**.</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": " SqlServerOutput "
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="34b16-1614">Zie voor meer informatie [SQL Server-connector](data-factory-sqlserver-connector.md#copy-activity-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1614">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span></span> 

## <a name="sybase"></a><span data-ttu-id="34b16-1615">Sybase</span><span class="sxs-lookup"><span data-stu-id="34b16-1615">Sybase</span></span>

### <a name="linked-service"></a><span data-ttu-id="34b16-1616">Gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="34b16-1616">Linked service</span></span>
<span data-ttu-id="34b16-1617">toodefine een Sybase gekoppelde service, set Hallo **type** Hallo gekoppelde service te**OnPremisesSybase**, en opgeven na eigenschappen in Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-1617">toodefine a Sybase linked service, set hello **type** of hello linked service too**OnPremisesSybase**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="34b16-1618">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1618">Property</span></span> | <span data-ttu-id="34b16-1619">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1619">Description</span></span> | <span data-ttu-id="34b16-1620">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1620">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-1621">server</span><span class="sxs-lookup"><span data-stu-id="34b16-1621">server</span></span> |<span data-ttu-id="34b16-1622">Naam van Hallo Sybase-server.</span><span class="sxs-lookup"><span data-stu-id="34b16-1622">Name of hello Sybase server.</span></span> |<span data-ttu-id="34b16-1623">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1623">Yes</span></span> |
| <span data-ttu-id="34b16-1624">database</span><span class="sxs-lookup"><span data-stu-id="34b16-1624">database</span></span> |<span data-ttu-id="34b16-1625">Naam van Hallo Sybase-database.</span><span class="sxs-lookup"><span data-stu-id="34b16-1625">Name of hello Sybase database.</span></span> |<span data-ttu-id="34b16-1626">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1626">Yes</span></span> |
| <span data-ttu-id="34b16-1627">Schema</span><span class="sxs-lookup"><span data-stu-id="34b16-1627">schema</span></span> |<span data-ttu-id="34b16-1628">Naam van Hallo schema in Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="34b16-1628">Name of hello schema in hello database.</span></span> |<span data-ttu-id="34b16-1629">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1629">No</span></span> |
| <span data-ttu-id="34b16-1630">authenticationType</span><span class="sxs-lookup"><span data-stu-id="34b16-1630">authenticationType</span></span> |<span data-ttu-id="34b16-1631">Type verificatie gebruikt tooconnect toohello Sybase-database.</span><span class="sxs-lookup"><span data-stu-id="34b16-1631">Type of authentication used tooconnect toohello Sybase database.</span></span> <span data-ttu-id="34b16-1632">Mogelijke waarden zijn: anoniem, basis en Windows.</span><span class="sxs-lookup"><span data-stu-id="34b16-1632">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="34b16-1633">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1633">Yes</span></span> |
| <span data-ttu-id="34b16-1634">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="34b16-1634">username</span></span> |<span data-ttu-id="34b16-1635">Geef de gebruikersnaam als u basisverificatie of Windows-verificatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-1635">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="34b16-1636">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1636">No</span></span> |
| <span data-ttu-id="34b16-1637">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="34b16-1637">password</span></span> |<span data-ttu-id="34b16-1638">Wachtwoord voor gebruikersaccount Hallo die u hebt opgegeven voor Hallo gebruikersnaam opgeven.</span><span class="sxs-lookup"><span data-stu-id="34b16-1638">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="34b16-1639">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1639">No</span></span> |
| <span data-ttu-id="34b16-1640">gatewayName</span><span class="sxs-lookup"><span data-stu-id="34b16-1640">gatewayName</span></span> |<span data-ttu-id="34b16-1641">Naam van Hallo-gateway die Hallo Data Factory-service moet tooconnect toohello lokale Sybase-database gebruiken.</span><span class="sxs-lookup"><span data-stu-id="34b16-1641">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises Sybase database.</span></span> |<span data-ttu-id="34b16-1642">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1642">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-1643">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1643">Example</span></span>
```json
{
    "name": "OnPremSybaseLinkedService",
    "properties": {
        "type": "OnPremisesSybase",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="34b16-1644">Zie voor meer informatie [Sybase connector](data-factory-onprem-sybase-connector.md#linked-service-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1644">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="34b16-1645">Gegevensset</span><span class="sxs-lookup"><span data-stu-id="34b16-1645">Dataset</span></span>
<span data-ttu-id="34b16-1646">toodefine een gegevensset Sybase set Hallo **type** van Hallo gegevensset te**RelationalTable**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-1646">toodefine a Sybase dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="34b16-1647">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1647">Property</span></span> | <span data-ttu-id="34b16-1648">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1648">Description</span></span> | <span data-ttu-id="34b16-1649">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1649">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-1650">tableName</span><span class="sxs-lookup"><span data-stu-id="34b16-1650">tableName</span></span> |<span data-ttu-id="34b16-1651">De naam van de tabel Hallo in Hallo Sybase-Database-instantie waarnaar de gekoppelde service verwijst.</span><span class="sxs-lookup"><span data-stu-id="34b16-1651">Name of hello table in hello Sybase Database instance that linked service refers to.</span></span> |<span data-ttu-id="34b16-1652">Nee (als **query** van **RelationalSource** is opgegeven)</span><span class="sxs-lookup"><span data-stu-id="34b16-1652">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-1653">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1653">Example</span></span>

```json
{
    "name": "SybaseDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremSybaseLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="34b16-1654">Zie voor meer informatie [Sybase connector](data-factory-onprem-sybase-connector.md#dataset-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1654">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="34b16-1655">Relationele gegevensbron in de kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="34b16-1655">Relational Source in Copy Activity</span></span>
<span data-ttu-id="34b16-1656">Als u gegevens uit een Sybase-database kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**RelationalSource**, en opgeven na eigenschappen in Hallo **bron** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-1656">If you are copying data from a Sybase database, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="34b16-1657">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1657">Property</span></span> | <span data-ttu-id="34b16-1658">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1658">Description</span></span> | <span data-ttu-id="34b16-1659">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="34b16-1659">Allowed values</span></span> | <span data-ttu-id="34b16-1660">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1660">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-1661">query</span><span class="sxs-lookup"><span data-stu-id="34b16-1661">query</span></span> |<span data-ttu-id="34b16-1662">Hallo aangepaste query tooread gegevens worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-1662">Use hello custom query tooread data.</span></span> |<span data-ttu-id="34b16-1663">SQL-query-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="34b16-1663">SQL query string.</span></span> <span data-ttu-id="34b16-1664">Bijvoorbeeld: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="34b16-1664">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="34b16-1665">Nee (als **tableName** van **gegevensset** is opgegeven)</span><span class="sxs-lookup"><span data-stu-id="34b16-1665">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-1666">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1666">Example</span></span>

```json
{
    "name": "CopySybaseToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from DBA.Orders"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "SybaseDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobSybaseDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SybaseToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="34b16-1667">Zie voor meer informatie [Sybase connector](data-factory-onprem-sybase-connector.md#copy-activity-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1667">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#copy-activity-properties) article.</span></span>

## <a name="teradata"></a><span data-ttu-id="34b16-1668">Teradata</span><span class="sxs-lookup"><span data-stu-id="34b16-1668">Teradata</span></span>

### <a name="linked-service"></a><span data-ttu-id="34b16-1669">Gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="34b16-1669">Linked service</span></span>
<span data-ttu-id="34b16-1670">een Teradata toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**OnPremisesTeradata**, en opgeven na eigenschappen in Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-1670">toodefine a Teradata linked service, set hello **type** of hello linked service too**OnPremisesTeradata**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="34b16-1671">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1671">Property</span></span> | <span data-ttu-id="34b16-1672">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1672">Description</span></span> | <span data-ttu-id="34b16-1673">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1673">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-1674">server</span><span class="sxs-lookup"><span data-stu-id="34b16-1674">server</span></span> |<span data-ttu-id="34b16-1675">Naam van Hallo Teradata-server.</span><span class="sxs-lookup"><span data-stu-id="34b16-1675">Name of hello Teradata server.</span></span> |<span data-ttu-id="34b16-1676">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1676">Yes</span></span> |
| <span data-ttu-id="34b16-1677">authenticationType</span><span class="sxs-lookup"><span data-stu-id="34b16-1677">authenticationType</span></span> |<span data-ttu-id="34b16-1678">Type verificatie gebruikt tooconnect toohello Teradata-database.</span><span class="sxs-lookup"><span data-stu-id="34b16-1678">Type of authentication used tooconnect toohello Teradata database.</span></span> <span data-ttu-id="34b16-1679">Mogelijke waarden zijn: anoniem, basis en Windows.</span><span class="sxs-lookup"><span data-stu-id="34b16-1679">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="34b16-1680">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1680">Yes</span></span> |
| <span data-ttu-id="34b16-1681">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="34b16-1681">username</span></span> |<span data-ttu-id="34b16-1682">Geef de gebruikersnaam als u basisverificatie of Windows-verificatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-1682">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="34b16-1683">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1683">No</span></span> |
| <span data-ttu-id="34b16-1684">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="34b16-1684">password</span></span> |<span data-ttu-id="34b16-1685">Wachtwoord voor gebruikersaccount Hallo die u hebt opgegeven voor Hallo gebruikersnaam opgeven.</span><span class="sxs-lookup"><span data-stu-id="34b16-1685">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="34b16-1686">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1686">No</span></span> |
| <span data-ttu-id="34b16-1687">gatewayName</span><span class="sxs-lookup"><span data-stu-id="34b16-1687">gatewayName</span></span> |<span data-ttu-id="34b16-1688">Naam van Hallo-gateway die Hallo Data Factory-service moet tooconnect toohello lokale Teradata-database gebruiken.</span><span class="sxs-lookup"><span data-stu-id="34b16-1688">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises Teradata database.</span></span> |<span data-ttu-id="34b16-1689">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1689">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-1690">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1690">Example</span></span>
```json
{
    "name": "OnPremTeradataLinkedService",
    "properties": {
        "type": "OnPremisesTeradata",
        "typeProperties": {
            "server": "<server>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="34b16-1691">Zie voor meer informatie [Teradata connector](data-factory-onprem-teradata-connector.md#linked-service-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1691">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="34b16-1692">Gegevensset</span><span class="sxs-lookup"><span data-stu-id="34b16-1692">Dataset</span></span>
<span data-ttu-id="34b16-1693">toodefine een Teradata-Blob-gegevensset set Hallo **type** van Hallo gegevensset te**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="34b16-1693">toodefine a Teradata Blob dataset, set hello **type** of hello dataset too**RelationalTable**.</span></span> <span data-ttu-id="34b16-1694">Er zijn momenteel geen type-eigenschappen voor Hallo Teradata gegevensset ondersteund.</span><span class="sxs-lookup"><span data-stu-id="34b16-1694">Currently, there are no type properties supported for hello Teradata dataset.</span></span> 

#### <a name="example"></a><span data-ttu-id="34b16-1695">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1695">Example</span></span>
```json
{
    "name": "TeradataDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremTeradataLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="34b16-1696">Zie voor meer informatie [Teradata connector](data-factory-onprem-teradata-connector.md#dataset-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1696">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="34b16-1697">Relationele gegevensbron in de kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="34b16-1697">Relational Source in Copy Activity</span></span>
<span data-ttu-id="34b16-1698">Als u gegevens uit een Teradata-database kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**RelationalSource**, en opgeven na eigenschappen in Hallo **bron**sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-1698">If you are copying data from a Teradata database, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="34b16-1699">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1699">Property</span></span> | <span data-ttu-id="34b16-1700">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1700">Description</span></span> | <span data-ttu-id="34b16-1701">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="34b16-1701">Allowed values</span></span> | <span data-ttu-id="34b16-1702">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1702">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-1703">query</span><span class="sxs-lookup"><span data-stu-id="34b16-1703">query</span></span> |<span data-ttu-id="34b16-1704">Hallo aangepaste query tooread gegevens worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-1704">Use hello custom query tooread data.</span></span> |<span data-ttu-id="34b16-1705">SQL-query-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="34b16-1705">SQL query string.</span></span> <span data-ttu-id="34b16-1706">Bijvoorbeeld: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="34b16-1706">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="34b16-1707">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1707">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-1708">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1708">Example</span></span>

```json
{
    "name": "CopyTeradataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', SliceStart, SliceEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "TeradataDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobTeradataDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "TeradataToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="34b16-1709">Zie voor meer informatie [Teradata connector](data-factory-onprem-teradata-connector.md#copy-activity-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1709">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#copy-activity-properties) article.</span></span>

## <a name="cassandra"></a><span data-ttu-id="34b16-1710">Cassandra</span><span class="sxs-lookup"><span data-stu-id="34b16-1710">Cassandra</span></span>


### <a name="linked-service"></a><span data-ttu-id="34b16-1711">Gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="34b16-1711">Linked service</span></span>
<span data-ttu-id="34b16-1712">een Cassandra toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**OnPremisesCassandra**, en opgeven na eigenschappen in Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-1712">toodefine a Cassandra linked service, set hello **type** of hello linked service too**OnPremisesCassandra**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="34b16-1713">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1713">Property</span></span> | <span data-ttu-id="34b16-1714">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1714">Description</span></span> | <span data-ttu-id="34b16-1715">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1715">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-1716">host</span><span class="sxs-lookup"><span data-stu-id="34b16-1716">host</span></span> |<span data-ttu-id="34b16-1717">Een of meer IP-adressen of hostnamen van Cassandra servers.</span><span class="sxs-lookup"><span data-stu-id="34b16-1717">One or more IP addresses or host names of Cassandra servers.</span></span><br/><br/><span data-ttu-id="34b16-1718">Geef een door komma's gescheiden lijst met IP-adressen of namen tooconnect tooall hostservers gelijktijdig.</span><span class="sxs-lookup"><span data-stu-id="34b16-1718">Specify a comma-separated list of IP addresses or host names tooconnect tooall servers concurrently.</span></span> |<span data-ttu-id="34b16-1719">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1719">Yes</span></span> |
| <span data-ttu-id="34b16-1720">poort</span><span class="sxs-lookup"><span data-stu-id="34b16-1720">port</span></span> |<span data-ttu-id="34b16-1721">toolisten Hello TCP-poort die Hallo Cassandra server gebruikt voor clientverbindingen.</span><span class="sxs-lookup"><span data-stu-id="34b16-1721">hello TCP port that hello Cassandra server uses toolisten for client connections.</span></span> |<span data-ttu-id="34b16-1722">Nee, de standaardwaarde: 9042</span><span class="sxs-lookup"><span data-stu-id="34b16-1722">No, default value: 9042</span></span> |
| <span data-ttu-id="34b16-1723">authenticationType</span><span class="sxs-lookup"><span data-stu-id="34b16-1723">authenticationType</span></span> |<span data-ttu-id="34b16-1724">Basic- of anonieme</span><span class="sxs-lookup"><span data-stu-id="34b16-1724">Basic, or Anonymous</span></span> |<span data-ttu-id="34b16-1725">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1725">Yes</span></span> |
| <span data-ttu-id="34b16-1726">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="34b16-1726">username</span></span> |<span data-ttu-id="34b16-1727">Geef de gebruikersnaam voor Hallo-gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="34b16-1727">Specify user name for hello user account.</span></span> |<span data-ttu-id="34b16-1728">Ja, als authenticationType tooBasic is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="34b16-1728">Yes, if authenticationType is set tooBasic.</span></span> |
| <span data-ttu-id="34b16-1729">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="34b16-1729">password</span></span> |<span data-ttu-id="34b16-1730">Wachtwoord voor gebruikersaccount Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="34b16-1730">Specify password for hello user account.</span></span> |<span data-ttu-id="34b16-1731">Ja, als authenticationType tooBasic is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="34b16-1731">Yes, if authenticationType is set tooBasic.</span></span> |
| <span data-ttu-id="34b16-1732">gatewayName</span><span class="sxs-lookup"><span data-stu-id="34b16-1732">gatewayName</span></span> |<span data-ttu-id="34b16-1733">Hallo-naam van Hallo-gateway die is gebruikt tooconnect toohello lokale Cassandra-database.</span><span class="sxs-lookup"><span data-stu-id="34b16-1733">hello name of hello gateway that is used tooconnect toohello on-premises Cassandra database.</span></span> |<span data-ttu-id="34b16-1734">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1734">Yes</span></span> |
| <span data-ttu-id="34b16-1735">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="34b16-1735">encryptedCredential</span></span> |<span data-ttu-id="34b16-1736">Referentie versleuteld door Hallo-gateway.</span><span class="sxs-lookup"><span data-stu-id="34b16-1736">Credential encrypted by hello gateway.</span></span> |<span data-ttu-id="34b16-1737">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1737">No</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-1738">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1738">Example</span></span>

```json
{
    "name": "CassandraLinkedService",
    "properties": {
        "type": "OnPremisesCassandra",
        "typeProperties": {
            "authenticationType": "Basic",
            "host": "<cassandra server name or IP address>",
            "port": 9042,
            "username": "user",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="34b16-1739">Zie voor meer informatie [Cassandra connector](data-factory-onprem-cassandra-connector.md#linked-service-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1739">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="34b16-1740">Gegevensset</span><span class="sxs-lookup"><span data-stu-id="34b16-1740">Dataset</span></span>
<span data-ttu-id="34b16-1741">toodefine een gegevensset Cassandra set Hallo **type** van Hallo gegevensset te**CassandraTable**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-1741">toodefine a Cassandra dataset, set hello **type** of hello dataset too**CassandraTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="34b16-1742">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1742">Property</span></span> | <span data-ttu-id="34b16-1743">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1743">Description</span></span> | <span data-ttu-id="34b16-1744">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1744">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-1745">met keyspace</span><span class="sxs-lookup"><span data-stu-id="34b16-1745">keyspace</span></span> |<span data-ttu-id="34b16-1746">Naam van Hallo keyspace of het schema in Cassandra-database.</span><span class="sxs-lookup"><span data-stu-id="34b16-1746">Name of hello keyspace or schema in Cassandra database.</span></span> |<span data-ttu-id="34b16-1747">Ja (als **query** voor **CassandraSource** is niet gedefinieerd).</span><span class="sxs-lookup"><span data-stu-id="34b16-1747">Yes (If **query** for **CassandraSource** is not defined).</span></span> |
| <span data-ttu-id="34b16-1748">tableName</span><span class="sxs-lookup"><span data-stu-id="34b16-1748">tableName</span></span> |<span data-ttu-id="34b16-1749">Naam van de tabel Hallo in Cassandra-database.</span><span class="sxs-lookup"><span data-stu-id="34b16-1749">Name of hello table in Cassandra database.</span></span> |<span data-ttu-id="34b16-1750">Ja (als **query** voor **CassandraSource** is niet gedefinieerd).</span><span class="sxs-lookup"><span data-stu-id="34b16-1750">Yes (If **query** for **CassandraSource** is not defined).</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-1751">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1751">Example</span></span>

```json
{
    "name": "CassandraInput",
    "properties": {
        "linkedServiceName": "CassandraLinkedService",
        "type": "CassandraTable",
        "typeProperties": {
            "tableName": "mytable",
            "keySpace": "<key space>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="34b16-1752">Zie voor meer informatie [Cassandra connector](data-factory-onprem-cassandra-connector.md#dataset-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1752">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#dataset-properties) article.</span></span> 

### <a name="cassandra-source-in-copy-activity"></a><span data-ttu-id="34b16-1753">Cassandra-bron in de kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="34b16-1753">Cassandra Source in Copy Activity</span></span>
<span data-ttu-id="34b16-1754">Als u gegevens uit Cassandra kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**CassandraSource**, en opgeven na eigenschappen in Hallo **bron** sectie :</span><span class="sxs-lookup"><span data-stu-id="34b16-1754">If you are copying data from Cassandra, set hello **source type** of hello copy activity too**CassandraSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="34b16-1755">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1755">Property</span></span> | <span data-ttu-id="34b16-1756">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1756">Description</span></span> | <span data-ttu-id="34b16-1757">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="34b16-1757">Allowed values</span></span> | <span data-ttu-id="34b16-1758">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1758">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-1759">query</span><span class="sxs-lookup"><span data-stu-id="34b16-1759">query</span></span> |<span data-ttu-id="34b16-1760">Hallo aangepaste query tooread gegevens worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-1760">Use hello custom query tooread data.</span></span> |<span data-ttu-id="34b16-1761">SQL-92 query of CQL query.</span><span class="sxs-lookup"><span data-stu-id="34b16-1761">SQL-92 query or CQL query.</span></span> <span data-ttu-id="34b16-1762">Zie [CQL verwijzing](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span><span class="sxs-lookup"><span data-stu-id="34b16-1762">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span></span> <br/><br/><span data-ttu-id="34b16-1763">Wanneer u SQL-query gebruikt, geef **keyspace name.table naam** toorepresent Hallo tabel gewenste tooquery.</span><span class="sxs-lookup"><span data-stu-id="34b16-1763">When using SQL query, specify **keyspace name.table name** toorepresent hello table you want tooquery.</span></span> |<span data-ttu-id="34b16-1764">Nee (als tableName en keyspace op gegevensset zijn gedefinieerd).</span><span class="sxs-lookup"><span data-stu-id="34b16-1764">No (if tableName and keyspace on dataset are defined).</span></span> |
| <span data-ttu-id="34b16-1765">consistencyLevel</span><span class="sxs-lookup"><span data-stu-id="34b16-1765">consistencyLevel</span></span> |<span data-ttu-id="34b16-1766">Hallo consistentieniveau geeft het aantal replica's tooa leesaanvraag moet reageren voordat gegevens toohello clienttoepassing wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="34b16-1766">hello consistency level specifies how many replicas must respond tooa read request before returning data toohello client application.</span></span> <span data-ttu-id="34b16-1767">Cassandra controles Hallo opgegeven aantal replica's voor gegevens toosatisfy Hallo leesaanvraag.</span><span class="sxs-lookup"><span data-stu-id="34b16-1767">Cassandra checks hello specified number of replicas for data toosatisfy hello read request.</span></span> |<span data-ttu-id="34b16-1768">EEN, TWEE, DRIE, QUORUM, ALL, LOCAL_QUORUM EACH_QUORUM, LOCAL_ONE.</span><span class="sxs-lookup"><span data-stu-id="34b16-1768">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span></span> <span data-ttu-id="34b16-1769">Zie [gegevensconsistentie configureren](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="34b16-1769">See [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) for details.</span></span> |<span data-ttu-id="34b16-1770">Nee.</span><span class="sxs-lookup"><span data-stu-id="34b16-1770">No.</span></span> <span data-ttu-id="34b16-1771">Standaardwaarde is een.</span><span class="sxs-lookup"><span data-stu-id="34b16-1771">Default value is ONE.</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-1772">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1772">Example</span></span>
  
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "CassandraInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "CassandraSource",
                    "query": "select id, firstname, lastname from mykeyspace.mytable"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="34b16-1773">Zie voor meer informatie [Cassandra connector](data-factory-onprem-cassandra-connector.md#copy-activity-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1773">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#copy-activity-properties) article.</span></span>

## <a name="mongodb"></a><span data-ttu-id="34b16-1774">MongoDB</span><span class="sxs-lookup"><span data-stu-id="34b16-1774">MongoDB</span></span>

### <a name="linked-service"></a><span data-ttu-id="34b16-1775">Gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="34b16-1775">Linked service</span></span>
<span data-ttu-id="34b16-1776">een MongoDB toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**OnPremisesMongoDB**, en opgeven na eigenschappen in Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-1776">toodefine a MongoDB linked service, set hello **type** of hello linked service too**OnPremisesMongoDB**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="34b16-1777">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1777">Property</span></span> | <span data-ttu-id="34b16-1778">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1778">Description</span></span> | <span data-ttu-id="34b16-1779">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1779">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-1780">server</span><span class="sxs-lookup"><span data-stu-id="34b16-1780">server</span></span> |<span data-ttu-id="34b16-1781">IP-adres of de hostnaam de naam van Hallo MongoDB-server.</span><span class="sxs-lookup"><span data-stu-id="34b16-1781">IP address or host name of hello MongoDB server.</span></span> |<span data-ttu-id="34b16-1782">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1782">Yes</span></span> |
| <span data-ttu-id="34b16-1783">poort</span><span class="sxs-lookup"><span data-stu-id="34b16-1783">port</span></span> |<span data-ttu-id="34b16-1784">Toolisten TCP-poort die Hallo MongoDB-server gebruikt voor clientverbindingen.</span><span class="sxs-lookup"><span data-stu-id="34b16-1784">TCP port that hello MongoDB server uses toolisten for client connections.</span></span> |<span data-ttu-id="34b16-1785">Optionele standaardwaarde: 27017</span><span class="sxs-lookup"><span data-stu-id="34b16-1785">Optional, default value: 27017</span></span> |
| <span data-ttu-id="34b16-1786">authenticationType</span><span class="sxs-lookup"><span data-stu-id="34b16-1786">authenticationType</span></span> |<span data-ttu-id="34b16-1787">Basic of anonieme.</span><span class="sxs-lookup"><span data-stu-id="34b16-1787">Basic, or Anonymous.</span></span> |<span data-ttu-id="34b16-1788">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1788">Yes</span></span> |
| <span data-ttu-id="34b16-1789">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="34b16-1789">username</span></span> |<span data-ttu-id="34b16-1790">Gebruiker account tooaccess MongoDB.</span><span class="sxs-lookup"><span data-stu-id="34b16-1790">User account tooaccess MongoDB.</span></span> |<span data-ttu-id="34b16-1791">Ja (als u basisverificatie wordt gebruikt).</span><span class="sxs-lookup"><span data-stu-id="34b16-1791">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="34b16-1792">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="34b16-1792">password</span></span> |<span data-ttu-id="34b16-1793">Wachtwoord voor gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="34b16-1793">Password for hello user.</span></span> |<span data-ttu-id="34b16-1794">Ja (als u basisverificatie wordt gebruikt).</span><span class="sxs-lookup"><span data-stu-id="34b16-1794">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="34b16-1795">authSource</span><span class="sxs-lookup"><span data-stu-id="34b16-1795">authSource</span></span> |<span data-ttu-id="34b16-1796">Naam van Hallo MongoDB-database dat u wilt dat toouse toocheck uw referenties voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="34b16-1796">Name of hello MongoDB database that you want toouse toocheck your credentials for authentication.</span></span> |<span data-ttu-id="34b16-1797">Optioneel (als basisverificatie wordt gebruikt).</span><span class="sxs-lookup"><span data-stu-id="34b16-1797">Optional (if basic authentication is used).</span></span> <span data-ttu-id="34b16-1798">Standaard: maakt gebruik van Hallo-beheerdersaccount en Hallo database die is opgegeven met de eigenschap databaseName.</span><span class="sxs-lookup"><span data-stu-id="34b16-1798">default: uses hello admin account and hello database specified using databaseName property.</span></span> |
| <span data-ttu-id="34b16-1799">DatabaseName</span><span class="sxs-lookup"><span data-stu-id="34b16-1799">databaseName</span></span> |<span data-ttu-id="34b16-1800">Naam van Hallo MongoDB-database die u tooaccess wilt.</span><span class="sxs-lookup"><span data-stu-id="34b16-1800">Name of hello MongoDB database that you want tooaccess.</span></span> |<span data-ttu-id="34b16-1801">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1801">Yes</span></span> |
| <span data-ttu-id="34b16-1802">gatewayName</span><span class="sxs-lookup"><span data-stu-id="34b16-1802">gatewayName</span></span> |<span data-ttu-id="34b16-1803">Naam van het Hallo-gateway die toegang heeft tot Hallo-gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="34b16-1803">Name of hello gateway that accesses hello data store.</span></span> |<span data-ttu-id="34b16-1804">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1804">Yes</span></span> |
| <span data-ttu-id="34b16-1805">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="34b16-1805">encryptedCredential</span></span> |<span data-ttu-id="34b16-1806">Referentie versleuteld door de gateway.</span><span class="sxs-lookup"><span data-stu-id="34b16-1806">Credential encrypted by gateway.</span></span> |<span data-ttu-id="34b16-1807">Optioneel</span><span class="sxs-lookup"><span data-stu-id="34b16-1807">Optional</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-1808">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1808">Example</span></span>

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties": {
        "type": "OnPremisesMongoDb",
        "typeProperties": {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< hello IP address or host name of hello MongoDB server >",
            "port": "<hello number of hello TCP port that hello MongoDB server uses toolisten for client connections.>",
            "username": "<username>",
            "password": "<password>",
            "authSource": "< hello database that you want toouse toocheck your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="34b16-1809">Zie voor meer informatie [MongoDB-connector artikel](data-factory-on-premises-mongodb-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="34b16-1809">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#linked-service-properties)</span></span>

### <a name="dataset"></a><span data-ttu-id="34b16-1810">Gegevensset</span><span class="sxs-lookup"><span data-stu-id="34b16-1810">Dataset</span></span>
<span data-ttu-id="34b16-1811">toodefine een gegevensset MongoDB set Hallo **type** van Hallo gegevensset te**MongoDbCollection**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-1811">toodefine a MongoDB dataset, set hello **type** of hello dataset too**MongoDbCollection**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="34b16-1812">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1812">Property</span></span> | <span data-ttu-id="34b16-1813">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1813">Description</span></span> | <span data-ttu-id="34b16-1814">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1814">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-1815">CollectionName</span><span class="sxs-lookup"><span data-stu-id="34b16-1815">collectionName</span></span> |<span data-ttu-id="34b16-1816">Naam van de verzameling Hallo in MongoDB-database.</span><span class="sxs-lookup"><span data-stu-id="34b16-1816">Name of hello collection in MongoDB database.</span></span> |<span data-ttu-id="34b16-1817">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1817">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-1818">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1818">Example</span></span>

```json
{
    "name": "MongoDbInputDataset",
    "properties": {
        "type": "MongoDbCollection",
        "linkedServiceName": "OnPremisesMongoDbLinkedService",
        "typeProperties": {
            "collectionName": "<Collection name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

<span data-ttu-id="34b16-1819">Zie voor meer informatie [MongoDB-connector artikel](data-factory-on-premises-mongodb-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="34b16-1819">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#dataset-properties)</span></span>

#### <a name="mongodb-source-in-copy-activity"></a><span data-ttu-id="34b16-1820">MongoDB-bron in de kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="34b16-1820">MongoDB Source in Copy Activity</span></span>
<span data-ttu-id="34b16-1821">Als u gegevens uit MongoDB kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**MongoDbSource**, en opgeven na eigenschappen in Hallo **bron** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-1821">If you are copying data from MongoDB, set hello **source type** of hello copy activity too**MongoDbSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="34b16-1822">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1822">Property</span></span> | <span data-ttu-id="34b16-1823">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1823">Description</span></span> | <span data-ttu-id="34b16-1824">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="34b16-1824">Allowed values</span></span> | <span data-ttu-id="34b16-1825">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1825">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-1826">query</span><span class="sxs-lookup"><span data-stu-id="34b16-1826">query</span></span> |<span data-ttu-id="34b16-1827">Hallo aangepaste query tooread gegevens worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-1827">Use hello custom query tooread data.</span></span> |<span data-ttu-id="34b16-1828">SQL-92 queryreeks.</span><span class="sxs-lookup"><span data-stu-id="34b16-1828">SQL-92 query string.</span></span> <span data-ttu-id="34b16-1829">Bijvoorbeeld: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="34b16-1829">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="34b16-1830">Nee (als **collectionName** van **gegevensset** is opgegeven)</span><span class="sxs-lookup"><span data-stu-id="34b16-1830">No (if **collectionName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-1831">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1831">Example</span></span>

```json
{
    "name": "CopyMongoDBToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "MongoDbSource",
                    "query": "select * from MyTable"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "MongoDbInputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "MongoDBToAzureBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="34b16-1832">Zie voor meer informatie [MongoDB-connector artikel](data-factory-on-premises-mongodb-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="34b16-1832">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#copy-activity-properties)</span></span>

## <a name="amazon-s3"></a><span data-ttu-id="34b16-1833">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="34b16-1833">Amazon S3</span></span>


### <a name="linked-service"></a><span data-ttu-id="34b16-1834">Gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="34b16-1834">Linked service</span></span>
<span data-ttu-id="34b16-1835">een Amazon S3 toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**AwsAccessKey**, en opgeven na eigenschappen in Hallo **typeProperties** sectie :</span><span class="sxs-lookup"><span data-stu-id="34b16-1835">toodefine an Amazon S3 linked service, set hello **type** of hello linked service too**AwsAccessKey**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="34b16-1836">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1836">Property</span></span> | <span data-ttu-id="34b16-1837">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1837">Description</span></span> | <span data-ttu-id="34b16-1838">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="34b16-1838">Allowed values</span></span> | <span data-ttu-id="34b16-1839">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1839">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-1840">accessKeyID</span><span class="sxs-lookup"><span data-stu-id="34b16-1840">accessKeyID</span></span> |<span data-ttu-id="34b16-1841">ID van de geheime toegangssleutel Hallo.</span><span class="sxs-lookup"><span data-stu-id="34b16-1841">ID of hello secret access key.</span></span> |<span data-ttu-id="34b16-1842">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="34b16-1842">string</span></span> |<span data-ttu-id="34b16-1843">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1843">Yes</span></span> |
| <span data-ttu-id="34b16-1844">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="34b16-1844">secretAccessKey</span></span> |<span data-ttu-id="34b16-1845">Hallo geheime toegangssleutel zelf.</span><span class="sxs-lookup"><span data-stu-id="34b16-1845">hello secret access key itself.</span></span> |<span data-ttu-id="34b16-1846">Versleutelde geheime tekenreeks</span><span class="sxs-lookup"><span data-stu-id="34b16-1846">Encrypted secret string</span></span> |<span data-ttu-id="34b16-1847">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1847">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-1848">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1848">Example</span></span>
```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

<span data-ttu-id="34b16-1849">Zie voor meer informatie [Amazon S3 connector artikel](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="34b16-1849">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).</span></span>

### <a name="dataset"></a><span data-ttu-id="34b16-1850">Gegevensset</span><span class="sxs-lookup"><span data-stu-id="34b16-1850">Dataset</span></span>
<span data-ttu-id="34b16-1851">een Amazon S3 toodefine dataset set Hallo **type** van Hallo gegevensset te**AmazonS3**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-1851">toodefine an Amazon S3 dataset, set hello **type** of hello dataset too**AmazonS3**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="34b16-1852">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1852">Property</span></span> | <span data-ttu-id="34b16-1853">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1853">Description</span></span> | <span data-ttu-id="34b16-1854">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="34b16-1854">Allowed values</span></span> | <span data-ttu-id="34b16-1855">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1855">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-1856">bucketName</span><span class="sxs-lookup"><span data-stu-id="34b16-1856">bucketName</span></span> |<span data-ttu-id="34b16-1857">Hallo S3-Bucketnaam.</span><span class="sxs-lookup"><span data-stu-id="34b16-1857">hello S3 bucket name.</span></span> |<span data-ttu-id="34b16-1858">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="34b16-1858">String</span></span> |<span data-ttu-id="34b16-1859">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1859">Yes</span></span> |
| <span data-ttu-id="34b16-1860">sleutel</span><span class="sxs-lookup"><span data-stu-id="34b16-1860">key</span></span> |<span data-ttu-id="34b16-1861">Hallo S3 objectsleutel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1861">hello S3 object key.</span></span> |<span data-ttu-id="34b16-1862">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="34b16-1862">String</span></span> |<span data-ttu-id="34b16-1863">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1863">No</span></span> |
| <span data-ttu-id="34b16-1864">voorvoegsel</span><span class="sxs-lookup"><span data-stu-id="34b16-1864">prefix</span></span> |<span data-ttu-id="34b16-1865">Voorvoegsel voor Hallo S3 objectsleutel.</span><span class="sxs-lookup"><span data-stu-id="34b16-1865">Prefix for hello S3 object key.</span></span> <span data-ttu-id="34b16-1866">Objecten waarvan sleutels met dit voorvoegsel beginnen worden geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="34b16-1866">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="34b16-1867">Geldt alleen als sleutel is leeg.</span><span class="sxs-lookup"><span data-stu-id="34b16-1867">Applies only when key is empty.</span></span> |<span data-ttu-id="34b16-1868">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="34b16-1868">String</span></span> |<span data-ttu-id="34b16-1869">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1869">No</span></span> |
| <span data-ttu-id="34b16-1870">Versie</span><span class="sxs-lookup"><span data-stu-id="34b16-1870">version</span></span> |<span data-ttu-id="34b16-1871">Hallo-versie van S3-object als S3 versiebeheer is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="34b16-1871">hello version of S3 object if S3 versioning is enabled.</span></span> |<span data-ttu-id="34b16-1872">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="34b16-1872">String</span></span> |<span data-ttu-id="34b16-1873">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1873">No</span></span> |
| <span data-ttu-id="34b16-1874">Indeling</span><span class="sxs-lookup"><span data-stu-id="34b16-1874">format</span></span> | <span data-ttu-id="34b16-1875">Hallo na indelingstypen worden ondersteund: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="34b16-1875">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="34b16-1876">Set Hallo **type** eigenschap onder indeling tooone van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="34b16-1876">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="34b16-1877">Zie voor meer informatie [tekstindeling](data-factory-supported-file-and-compression-formats.md#text-format), [Json-indeling](data-factory-supported-file-and-compression-formats.md#json-format), [Avro-indeling](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc indeling](data-factory-supported-file-and-compression-formats.md#orc-format), en [parketvloeren indeling](data-factory-supported-file-and-compression-formats.md#parquet-format) secties.</span><span class="sxs-lookup"><span data-stu-id="34b16-1877">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="34b16-1878">Als u wilt dat te**kopiëren van bestanden als-is** tussen bestandsgebaseerde winkels (binaire kopiëren) Hallo indeling sectie in beide definities invoer en uitvoer gegevensset overslaan.</span><span class="sxs-lookup"><span data-stu-id="34b16-1878">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="34b16-1879">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1879">No</span></span> | |
| <span data-ttu-id="34b16-1880">Compressie</span><span class="sxs-lookup"><span data-stu-id="34b16-1880">compression</span></span> | <span data-ttu-id="34b16-1881">Hallo-type en compressieniveau voor Hallo gegevens opgeven.</span><span class="sxs-lookup"><span data-stu-id="34b16-1881">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="34b16-1882">Ondersteunde typen zijn: **GZip**, **Deflate**, **BZip2**, en **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="34b16-1882">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="34b16-1883">Hallo ondersteund niveaus zijn: **optimale** en **snelst**.</span><span class="sxs-lookup"><span data-stu-id="34b16-1883">hello supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="34b16-1884">Zie voor meer informatie [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="34b16-1884">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="34b16-1885">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1885">No</span></span> | |


> [!NOTE]
> <span data-ttu-id="34b16-1886">bucketName + sleutel geeft Hallo-locatie van Hallo S3 object waarbij bucket Hallo hoofdcontainer voor S3-objecten en sleutel Hallo volledig pad tooS3 object.</span><span class="sxs-lookup"><span data-stu-id="34b16-1886">bucketName + key specifies hello location of hello S3 object where bucket is hello root container for S3 objects and key is hello full path tooS3 object.</span></span>

#### <a name="example-sample-dataset-with-prefix"></a><span data-ttu-id="34b16-1887">Voorbeeld: Voorbeeldgegevensset met voorvoegsel</span><span class="sxs-lookup"><span data-stu-id="34b16-1887">Example: Sample dataset with prefix</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "<S3 bucket name>",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
#### <a name="example-sample-data-set-with-version"></a><span data-ttu-id="34b16-1888">Voorbeeld: Voorbeeldgegevensset (met versie)</span><span class="sxs-lookup"><span data-stu-id="34b16-1888">Example: Sample data set (with version)</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "<S3 bucket name>",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

#### <a name="example-dynamic-paths-for-s3"></a><span data-ttu-id="34b16-1889">Voorbeeld: Dynamische paden voor S3</span><span class="sxs-lookup"><span data-stu-id="34b16-1889">Example: Dynamic paths for S3</span></span>
<span data-ttu-id="34b16-1890">In het Hallo-voorbeeld gebruiken we vaste waarden voor eigenschappen van sleutel en bucketName in Hallo Amazon S3 gegevensset.</span><span class="sxs-lookup"><span data-stu-id="34b16-1890">In hello sample, we use fixed values for key and bucketName properties in hello Amazon S3 dataset.</span></span>

```json
"key": "testFolder/test.orc",
"bucketName": "<S3 bucket name>",
```

<span data-ttu-id="34b16-1891">U kunt Data Factory Hallo-sleutel en bucketName dynamisch tijdens runtime berekenen met behulp van systeemvariabelen zoals SliceStart hebben.</span><span class="sxs-lookup"><span data-stu-id="34b16-1891">You can have Data Factory calculate hello key and bucketName dynamically at runtime by using system variables such as SliceStart.</span></span>

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

<span data-ttu-id="34b16-1892">U kunt doen hello dezelfde voor Hallo voorvoegsel-eigenschap van een gegevensset Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="34b16-1892">You can do hello same for hello prefix property of an Amazon S3 dataset.</span></span> <span data-ttu-id="34b16-1893">Zie [Data Factory-functies en systeemvariabelen](data-factory-functions-variables.md) voor een lijst van ondersteunde functies en variabelen.</span><span class="sxs-lookup"><span data-stu-id="34b16-1893">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of supported functions and variables.</span></span>

<span data-ttu-id="34b16-1894">Zie voor meer informatie [Amazon S3 connector artikel](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="34b16-1894">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="34b16-1895">Systeem bronnen in de kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="34b16-1895">File System Source in Copy Activity</span></span>
<span data-ttu-id="34b16-1896">Als u gegevens vanaf Amazon S3 kopieert, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**FileSystemSource**, en opgeven na eigenschappen in Hallo **bron** sectie :</span><span class="sxs-lookup"><span data-stu-id="34b16-1896">If you are copying data from Amazon S3, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="34b16-1897">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1897">Property</span></span> | <span data-ttu-id="34b16-1898">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1898">Description</span></span> | <span data-ttu-id="34b16-1899">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="34b16-1899">Allowed values</span></span> | <span data-ttu-id="34b16-1900">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1900">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-1901">Recursieve</span><span class="sxs-lookup"><span data-stu-id="34b16-1901">recursive</span></span> |<span data-ttu-id="34b16-1902">Hiermee geeft u op of toorecursively lijst S3 onder Hallo directory-objecten.</span><span class="sxs-lookup"><span data-stu-id="34b16-1902">Specifies whether toorecursively list S3 objects under hello directory.</span></span> |<span data-ttu-id="34b16-1903">waar/onwaar</span><span class="sxs-lookup"><span data-stu-id="34b16-1903">true/false</span></span> |<span data-ttu-id="34b16-1904">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1904">No</span></span> |


#### <a name="example"></a><span data-ttu-id="34b16-1905">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1905">Example</span></span>


```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource",
                    "recursive": true
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "AmazonS3InputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "AmazonS3ToBlob"
        }],
        "start": "2016-08-08T18:00:00",
        "end": "2016-08-08T19:00:00"
    }
}
```

<span data-ttu-id="34b16-1906">Zie voor meer informatie [Amazon S3 connector artikel](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="34b16-1906">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).</span></span>

## <a name="file-system"></a><span data-ttu-id="34b16-1907">Bestandssysteem</span><span class="sxs-lookup"><span data-stu-id="34b16-1907">File System</span></span>


### <a name="linked-service"></a><span data-ttu-id="34b16-1908">Gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="34b16-1908">Linked service</span></span>
<span data-ttu-id="34b16-1909">U kunt een lokaal bestand system tooan Azure data factory Hello koppelen **On-Premises bestandsserver** gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="34b16-1909">You can link an on-premises file system tooan Azure data factory with hello **On-Premises File Server** linked service.</span></span> <span data-ttu-id="34b16-1910">Hallo volgende tabel bevat beschrijvingen van JSON-elementen die specifiek toohello bestandsserver On-Premises gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="34b16-1910">hello following table provides descriptions for JSON elements that are specific toohello On-Premises File Server linked service.</span></span>

| <span data-ttu-id="34b16-1911">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1911">Property</span></span> | <span data-ttu-id="34b16-1912">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1912">Description</span></span> | <span data-ttu-id="34b16-1913">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1913">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-1914">type</span><span class="sxs-lookup"><span data-stu-id="34b16-1914">type</span></span> |<span data-ttu-id="34b16-1915">Zorg ervoor dat de eigenschap type hello te is ingesteld**OnPremisesFileServer**.</span><span class="sxs-lookup"><span data-stu-id="34b16-1915">Ensure that hello type property is set too**OnPremisesFileServer**.</span></span> |<span data-ttu-id="34b16-1916">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1916">Yes</span></span> |
| <span data-ttu-id="34b16-1917">host</span><span class="sxs-lookup"><span data-stu-id="34b16-1917">host</span></span> |<span data-ttu-id="34b16-1918">Hiermee geeft u het hoofdpad Hallo van Hallo map die u toocopy wilt.</span><span class="sxs-lookup"><span data-stu-id="34b16-1918">Specifies hello root path of hello folder that you want toocopy.</span></span> <span data-ttu-id="34b16-1919">Gebruik Hallo escape-teken ' \ ' voor speciale tekens in Hallo-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="34b16-1919">Use hello escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="34b16-1920">Zie [voorbeeld gekoppelde service en gegevensset definities](#sample-linked-service-and-dataset-definitions) voor voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="34b16-1920">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span> |<span data-ttu-id="34b16-1921">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1921">Yes</span></span> |
| <span data-ttu-id="34b16-1922">gebruikers-id</span><span class="sxs-lookup"><span data-stu-id="34b16-1922">userid</span></span> |<span data-ttu-id="34b16-1923">Hallo-ID van het Hallo-gebruiker met toegang toohello server opgeven.</span><span class="sxs-lookup"><span data-stu-id="34b16-1923">Specify hello ID of hello user who has access toohello server.</span></span> |<span data-ttu-id="34b16-1924">Nee (als u ervoor encryptedCredential kiest)</span><span class="sxs-lookup"><span data-stu-id="34b16-1924">No (if you choose encryptedCredential)</span></span> |
| <span data-ttu-id="34b16-1925">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="34b16-1925">password</span></span> |<span data-ttu-id="34b16-1926">Hallo-wachtwoord voor gebruiker hello (gebruikersnaam) opgeven.</span><span class="sxs-lookup"><span data-stu-id="34b16-1926">Specify hello password for hello user (userid).</span></span> |<span data-ttu-id="34b16-1927">Nee (als u encryptedCredential kiezen</span><span class="sxs-lookup"><span data-stu-id="34b16-1927">No (if you choose encryptedCredential</span></span> |
| <span data-ttu-id="34b16-1928">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="34b16-1928">encryptedCredential</span></span> |<span data-ttu-id="34b16-1929">Geef referenties op Hallo versleuteld die u door de cmdlet New-AzureRmDataFactoryEncryptValue Hallo kunt ophalen.</span><span class="sxs-lookup"><span data-stu-id="34b16-1929">Specify hello encrypted credentials that you can get by running hello New-AzureRmDataFactoryEncryptValue cmdlet.</span></span> |<span data-ttu-id="34b16-1930">Nee (als u toospecify gebruikersnaam en wachtwoord als tekst zonder opmaak kiezen)</span><span class="sxs-lookup"><span data-stu-id="34b16-1930">No (if you choose toospecify userid and password in plain text)</span></span> |
| <span data-ttu-id="34b16-1931">gatewayName</span><span class="sxs-lookup"><span data-stu-id="34b16-1931">gatewayName</span></span> |<span data-ttu-id="34b16-1932">Geeft de naam Hallo van Hallo gateway dat Data Factory tooconnect toohello lokale bestandsserver moeten gebruiken.</span><span class="sxs-lookup"><span data-stu-id="34b16-1932">Specifies hello name of hello gateway that Data Factory should use tooconnect toohello on-premises file server.</span></span> |<span data-ttu-id="34b16-1933">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1933">Yes</span></span> |

#### <a name="sample-folder-path-definitions"></a><span data-ttu-id="34b16-1934">Voorbeeld map pad definities</span><span class="sxs-lookup"><span data-stu-id="34b16-1934">Sample folder path definitions</span></span> 
| <span data-ttu-id="34b16-1935">Scenario</span><span class="sxs-lookup"><span data-stu-id="34b16-1935">Scenario</span></span> | <span data-ttu-id="34b16-1936">In de definitie van de gekoppelde service host</span><span class="sxs-lookup"><span data-stu-id="34b16-1936">Host in linked service definition</span></span> | <span data-ttu-id="34b16-1937">folderPath in de definitie van gegevensset</span><span class="sxs-lookup"><span data-stu-id="34b16-1937">folderPath in dataset definition</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-1938">Lokale map op de Data Management Gateway-apparaat:</span><span class="sxs-lookup"><span data-stu-id="34b16-1938">Local folder on Data Management Gateway machine:</span></span> <br/><br/><span data-ttu-id="34b16-1939">Voorbeelden: D:\\ \* of D:\folder\subfolder\\*</span><span class="sxs-lookup"><span data-stu-id="34b16-1939">Examples: D:\\\* or D:\folder\subfolder\\*</span></span> |<span data-ttu-id="34b16-1940">D:\\ \\ (voor Data Management Gateway 2.0 en hoger)</span><span class="sxs-lookup"><span data-stu-id="34b16-1940">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/> <span data-ttu-id="34b16-1941">localhost (voor oudere versies dan Data Management Gateway 2.0)</span><span class="sxs-lookup"><span data-stu-id="34b16-1941">localhost (for earlier versions than Data Management Gateway 2.0)</span></span> |<span data-ttu-id="34b16-1942">. \\ \\ of de map\\\\submap (voor Data Management Gateway 2.0 en hoger)</span><span class="sxs-lookup"><span data-stu-id="34b16-1942">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/><span data-ttu-id="34b16-1943">D:\\ \\ of D:\\\\map\\\\submap (voor gatewayversie lager dan 2.0)</span><span class="sxs-lookup"><span data-stu-id="34b16-1943">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span></span> |
| <span data-ttu-id="34b16-1944">Externe gedeelde map:</span><span class="sxs-lookup"><span data-stu-id="34b16-1944">Remote shared folder:</span></span> <br/><br/><span data-ttu-id="34b16-1945">Voorbeelden: \\ \\MijnServer\\delen\\ \* of \\ \\MijnServer\\delen\\map\\submap\\*</span><span class="sxs-lookup"><span data-stu-id="34b16-1945">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span></span> |<span data-ttu-id="34b16-1946">\\\\\\\\MijnServer\\\\delen</span><span class="sxs-lookup"><span data-stu-id="34b16-1946">\\\\\\\\myserver\\\\share</span></span> |<span data-ttu-id="34b16-1947">. \\ \\ of de map\\\\submap</span><span class="sxs-lookup"><span data-stu-id="34b16-1947">.\\\\ or folder\\\\subfolder</span></span> |


#### <a name="example-using-username-and-password-in-plain-text"></a><span data-ttu-id="34b16-1948">Voorbeeld: Met behulp van gebruikersnaam en wachtwoord in tekst zonder opmaak</span><span class="sxs-lookup"><span data-stu-id="34b16-1948">Example: Using username and password in plain text</span></span>

```json
{
    "Name": "OnPremisesFileServerLinkedService",
    "properties": {
        "type": "OnPremisesFileServer",
        "typeProperties": {
            "host": "\\\\Contosogame-Asia",
            "userid": "Admin",
            "password": "123456",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-encryptedcredential"></a><span data-ttu-id="34b16-1949">Voorbeeld: Encryptedcredential gebruiken</span><span class="sxs-lookup"><span data-stu-id="34b16-1949">Example: Using encryptedcredential</span></span>

```json
{
    "Name": " OnPremisesFileServerLinkedService ",
    "properties": {
        "type": "OnPremisesFileServer",
        "typeProperties": {
            "host": "D:\\",
            "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="34b16-1950">Zie voor meer informatie [bestandssysteem connector artikel](data-factory-onprem-file-system-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="34b16-1950">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#linked-service-properties).</span></span>

### <a name="dataset"></a><span data-ttu-id="34b16-1951">Gegevensset</span><span class="sxs-lookup"><span data-stu-id="34b16-1951">Dataset</span></span>
<span data-ttu-id="34b16-1952">toodefine een gegevensset bestandssysteem set Hallo **type** van Hallo gegevensset te**FileShare**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-1952">toodefine a File System dataset, set hello **type** of hello dataset too**FileShare**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="34b16-1953">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1953">Property</span></span> | <span data-ttu-id="34b16-1954">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1954">Description</span></span> | <span data-ttu-id="34b16-1955">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1955">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-1956">folderPath</span><span class="sxs-lookup"><span data-stu-id="34b16-1956">folderPath</span></span> |<span data-ttu-id="34b16-1957">Hiermee geeft u Hallo subpad toohello map.</span><span class="sxs-lookup"><span data-stu-id="34b16-1957">Specifies hello subpath toohello folder.</span></span> <span data-ttu-id="34b16-1958">Gebruik Hallo escape-teken ' \' voor speciale tekens in Hallo-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="34b16-1958">Use hello escape character ‘\’ for special characters in hello string.</span></span> <span data-ttu-id="34b16-1959">Zie [voorbeeld gekoppelde service en gegevensset definities](#sample-linked-service-and-dataset-definitions) voor voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="34b16-1959">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="34b16-1960">U kunt deze eigenschap combineren met **partitionBy** toohave mappaden op basis van het segment beginnen of eindigen-datums en tijden.</span><span class="sxs-lookup"><span data-stu-id="34b16-1960">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="34b16-1961">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-1961">Yes</span></span> |
| <span data-ttu-id="34b16-1962">fileName</span><span class="sxs-lookup"><span data-stu-id="34b16-1962">fileName</span></span> |<span data-ttu-id="34b16-1963">Hallo-naam van Hallo-bestand opgeven in Hallo **folderPath** als u wilt dat Hallo tabel toorefer tooa specifiek bestand in map Hallo.</span><span class="sxs-lookup"><span data-stu-id="34b16-1963">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="34b16-1964">Als u geen waarde voor deze eigenschap niet opgeeft, wijst Hallo tabel tooall bestanden in de map Hallo.</span><span class="sxs-lookup"><span data-stu-id="34b16-1964">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="34b16-1965">FileName is opgegeven voor een uitvoergegevensset, heeft Hallo naam van Hallo gegenereerd bestand Hallo na indeling:</span><span class="sxs-lookup"><span data-stu-id="34b16-1965">When fileName is not specified for an output dataset, hello name of hello generated file is in hello following format:</span></span> <br/><br/><span data-ttu-id="34b16-1966">`Data.<Guid>.txt`(Voorbeeld: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="34b16-1966">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="34b16-1967">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1967">No</span></span> |
| <span data-ttu-id="34b16-1968">fileFilter</span><span class="sxs-lookup"><span data-stu-id="34b16-1968">fileFilter</span></span> |<span data-ttu-id="34b16-1969">Geef dat een filter toobe tooselect gebruikt een subset van de bestanden in Hallo folderPath in plaats van alle bestanden.</span><span class="sxs-lookup"><span data-stu-id="34b16-1969">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span> <br/><br/><span data-ttu-id="34b16-1970">Toegestane waarden zijn: `*` (meerdere tekens) en `?` (willekeurig teken).</span><span class="sxs-lookup"><span data-stu-id="34b16-1970">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="34b16-1971">Voorbeeld 1: 'fileFilter":" * .log '</span><span class="sxs-lookup"><span data-stu-id="34b16-1971">Example 1: "fileFilter": "*.log"</span></span><br/><span data-ttu-id="34b16-1972">Voorbeeld 2: 'fileFilter': 2016 - 1-?. txt'</span><span class="sxs-lookup"><span data-stu-id="34b16-1972">Example 2: "fileFilter": 2016-1-?.txt"</span></span><br/><br/><span data-ttu-id="34b16-1973">Houd er rekening mee dat fileFilter is van toepassing op een bestandsshare-invoergegevensset.</span><span class="sxs-lookup"><span data-stu-id="34b16-1973">Note that fileFilter is applicable for an input FileShare dataset.</span></span> |<span data-ttu-id="34b16-1974">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1974">No</span></span> |
| <span data-ttu-id="34b16-1975">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="34b16-1975">partitionedBy</span></span> |<span data-ttu-id="34b16-1976">U kunt partitionedBy toospecify een dynamische folderPath/bestandsnaam gebruiken voor timeseries gegevens.</span><span class="sxs-lookup"><span data-stu-id="34b16-1976">You can use partitionedBy toospecify a dynamic folderPath/fileName for time-series data.</span></span> <span data-ttu-id="34b16-1977">Een voorbeeld is folderPath geparametriseerde voor elk uur van gegevens.</span><span class="sxs-lookup"><span data-stu-id="34b16-1977">An example is folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="34b16-1978">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1978">No</span></span> |
| <span data-ttu-id="34b16-1979">Indeling</span><span class="sxs-lookup"><span data-stu-id="34b16-1979">format</span></span> | <span data-ttu-id="34b16-1980">Hallo na indelingstypen worden ondersteund: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="34b16-1980">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="34b16-1981">Set Hallo **type** eigenschap onder indeling tooone van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="34b16-1981">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="34b16-1982">Zie voor meer informatie [tekstindeling](data-factory-supported-file-and-compression-formats.md#text-format), [Json-indeling](data-factory-supported-file-and-compression-formats.md#json-format), [Avro-indeling](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc indeling](data-factory-supported-file-and-compression-formats.md#orc-format), en [parketvloeren indeling](data-factory-supported-file-and-compression-formats.md#parquet-format) secties.</span><span class="sxs-lookup"><span data-stu-id="34b16-1982">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="34b16-1983">Als u wilt dat te**kopiëren van bestanden als-is** tussen bestandsgebaseerde winkels (binaire kopiëren) Hallo indeling sectie in beide definities invoer en uitvoer gegevensset overslaan.</span><span class="sxs-lookup"><span data-stu-id="34b16-1983">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="34b16-1984">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1984">No</span></span> |
| <span data-ttu-id="34b16-1985">Compressie</span><span class="sxs-lookup"><span data-stu-id="34b16-1985">compression</span></span> | <span data-ttu-id="34b16-1986">Hallo-type en compressieniveau voor Hallo gegevens opgeven.</span><span class="sxs-lookup"><span data-stu-id="34b16-1986">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="34b16-1987">Ondersteunde typen zijn: **GZip**, **Deflate**, **BZip2**, en **ZipDeflate**; en ondersteunde niveaus: **optimale** en **snelst**.</span><span class="sxs-lookup"><span data-stu-id="34b16-1987">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="34b16-1988">Zie [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="34b16-1988">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="34b16-1989">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-1989">No</span></span> |

> [!NOTE]
> <span data-ttu-id="34b16-1990">U kunt geen bestandsnaam en fileFilter gelijktijdig gebruiken.</span><span class="sxs-lookup"><span data-stu-id="34b16-1990">You cannot use fileName and fileFilter simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="34b16-1991">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-1991">Example</span></span>

```json
{
    "name": "OnpremisesFileSystemInput",
    "properties": {
        "type": " FileShare",
        "linkedServiceName": " OnPremisesFileServerLinkedService ",
        "typeProperties": {
            "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
            "fileName": "{Hour}.csv",
            "partitionedBy": [{
                "name": "Year",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                        "format": "yyyy"
                }
            }, {
                "name": "Month",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "MM"
                }
            }, {
                "name": "Day",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "dd"
                }
            }, {
                "name": "Hour",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "HH"
                }
            }]
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="34b16-1992">Zie voor meer informatie [bestandssysteem connector artikel](data-factory-onprem-file-system-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="34b16-1992">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#dataset-properties).</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="34b16-1993">Systeem bronnen in de kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="34b16-1993">File System Source in Copy Activity</span></span>
<span data-ttu-id="34b16-1994">Als u gegevens uit bestandssysteem kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**FileSystemSource**, en opgeven na eigenschappen in Hallo **bron** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-1994">If you are copying data from File System, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="34b16-1995">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-1995">Property</span></span> | <span data-ttu-id="34b16-1996">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-1996">Description</span></span> | <span data-ttu-id="34b16-1997">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="34b16-1997">Allowed values</span></span> | <span data-ttu-id="34b16-1998">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-1998">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-1999">Recursieve</span><span class="sxs-lookup"><span data-stu-id="34b16-1999">recursive</span></span> |<span data-ttu-id="34b16-2000">Hiermee wordt aangegeven of Hallo gegevens recursief is gelezen vanuit Hallo submappen of alleen vanuit de opgegeven map Hallo.</span><span class="sxs-lookup"><span data-stu-id="34b16-2000">Indicates whether hello data is read recursively from hello subfolders or only from hello specified folder.</span></span> |<span data-ttu-id="34b16-2001">True, False (standaard)</span><span class="sxs-lookup"><span data-stu-id="34b16-2001">True, False (default)</span></span> |<span data-ttu-id="34b16-2002">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2002">No</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-2003">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-2003">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2015-06-01T18:00:00",
        "end": "2015-06-01T19:00:00",
        "description": "Pipeline for copy activity",
        "activities": [{
            "name": "OnpremisesFileSystemtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "OnpremisesFileSystemInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
            "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="34b16-2004">Zie voor meer informatie [bestandssysteem connector artikel](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="34b16-2004">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span></span>

### <a name="file-system-sink-in-copy-activity"></a><span data-ttu-id="34b16-2005">Bestandssysteem Sink in de kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="34b16-2005">File System Sink in Copy Activity</span></span>
<span data-ttu-id="34b16-2006">Als u gegevens tooFile System kopieert, stelt u Hallo **type sink** Hallo kopieeractiviteit te**FileSystemSink**, en opgeven na eigenschappen in Hallo **sink** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-2006">If you are copying data tooFile System, set hello **sink type** of hello copy activity too**FileSystemSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="34b16-2007">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-2007">Property</span></span> | <span data-ttu-id="34b16-2008">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-2008">Description</span></span> | <span data-ttu-id="34b16-2009">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="34b16-2009">Allowed values</span></span> | <span data-ttu-id="34b16-2010">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-2010">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-2011">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="34b16-2011">copyBehavior</span></span> |<span data-ttu-id="34b16-2012">Hallo kopie gedrag definieert wanneer Hallo bron BlobSource of bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="34b16-2012">Defines hello copy behavior when hello source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="34b16-2013">**PreserveHierarchy:** Hallo bestandshiërarchie in de doelmap Hallo behouden blijft.</span><span class="sxs-lookup"><span data-stu-id="34b16-2013">**PreserveHierarchy:** Preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="34b16-2014">Dat wil zeggen, is relatief pad Hallo van Hallo bestand toohello bron bronmap hetzelfde als het relatieve pad van Hallo bestand toohello doel doelmap Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="34b16-2014">That is, hello relative path of hello source file toohello source folder is hello same as hello relative path of hello target file toohello target folder.</span></span><br/><br/><span data-ttu-id="34b16-2015">**FlattenHierarchy:** alle bestanden uit de bronmap Hallo worden gemaakt in Hallo eerste niveau van de doelmap.</span><span class="sxs-lookup"><span data-stu-id="34b16-2015">**FlattenHierarchy:** All files from hello source folder are created in hello first level of target folder.</span></span> <span data-ttu-id="34b16-2016">Hallo doelbestanden worden gemaakt met een automatisch gegenereerde naam.</span><span class="sxs-lookup"><span data-stu-id="34b16-2016">hello target files are created with an autogenerated name.</span></span><br/><br/><span data-ttu-id="34b16-2017">**MergeFiles:** alle bestanden uit map Hallo-tooone bronbestand worden samengevoegd.</span><span class="sxs-lookup"><span data-stu-id="34b16-2017">**MergeFiles:** Merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="34b16-2018">Als Hallo bestand naam/blob-naam wordt opgegeven, is Hallo Samengevoegde bestandsnaam Hallo opgegeven naam.</span><span class="sxs-lookup"><span data-stu-id="34b16-2018">If hello file name/blob name is specified, hello merged file name is hello specified name.</span></span> <span data-ttu-id="34b16-2019">Anders is het een automatisch gegenereerde naam.</span><span class="sxs-lookup"><span data-stu-id="34b16-2019">Otherwise, it is an auto-generated file name.</span></span> |<span data-ttu-id="34b16-2020">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2020">No</span></span> |
<span data-ttu-id="34b16-2021">Automatische-</span><span class="sxs-lookup"><span data-stu-id="34b16-2021">auto-</span></span>

#### <a name="example"></a><span data-ttu-id="34b16-2022">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-2022">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2015-06-01T18:00:00",
        "end": "2015-06-01T20:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoOnPremisesFile",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "OnpremisesFileSystemOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "FileSystemSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 3,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="34b16-2023">Zie voor meer informatie [bestandssysteem connector artikel](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="34b16-2023">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span></span>

## <a name="ftp"></a><span data-ttu-id="34b16-2024">FTP</span><span class="sxs-lookup"><span data-stu-id="34b16-2024">FTP</span></span>

### <a name="linked-service"></a><span data-ttu-id="34b16-2025">Gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="34b16-2025">Linked service</span></span>
<span data-ttu-id="34b16-2026">toodefine een FTP-service, set Hallo gekoppeld **type** Hallo gekoppelde service te**FtpServer**, en opgeven na eigenschappen in Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-2026">toodefine an FTP linked service, set hello **type** of hello linked service too**FtpServer**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="34b16-2027">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-2027">Property</span></span> | <span data-ttu-id="34b16-2028">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-2028">Description</span></span> | <span data-ttu-id="34b16-2029">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-2029">Required</span></span> | <span data-ttu-id="34b16-2030">Standaard</span><span class="sxs-lookup"><span data-stu-id="34b16-2030">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-2031">host</span><span class="sxs-lookup"><span data-stu-id="34b16-2031">host</span></span> |<span data-ttu-id="34b16-2032">Naam of IP-adres van Hallo FTP-Server</span><span class="sxs-lookup"><span data-stu-id="34b16-2032">Name or IP address of hello FTP Server</span></span> |<span data-ttu-id="34b16-2033">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2033">Yes</span></span> |&nbsp; |
| <span data-ttu-id="34b16-2034">authenticationType</span><span class="sxs-lookup"><span data-stu-id="34b16-2034">authenticationType</span></span> |<span data-ttu-id="34b16-2035">Geef een verificatie</span><span class="sxs-lookup"><span data-stu-id="34b16-2035">Specify authentication type</span></span> |<span data-ttu-id="34b16-2036">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2036">Yes</span></span> |<span data-ttu-id="34b16-2037">Basic, anonieme</span><span class="sxs-lookup"><span data-stu-id="34b16-2037">Basic, Anonymous</span></span> |
| <span data-ttu-id="34b16-2038">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="34b16-2038">username</span></span> |<span data-ttu-id="34b16-2039">Gebruiker met toegang toohello FTP-server</span><span class="sxs-lookup"><span data-stu-id="34b16-2039">User who has access toohello FTP server</span></span> |<span data-ttu-id="34b16-2040">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2040">No</span></span> |&nbsp; |
| <span data-ttu-id="34b16-2041">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="34b16-2041">password</span></span> |<span data-ttu-id="34b16-2042">Wachtwoord voor gebruiker hello (username)</span><span class="sxs-lookup"><span data-stu-id="34b16-2042">Password for hello user (username)</span></span> |<span data-ttu-id="34b16-2043">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2043">No</span></span> |&nbsp; |
| <span data-ttu-id="34b16-2044">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="34b16-2044">encryptedCredential</span></span> |<span data-ttu-id="34b16-2045">Versleutelde referentie tooaccess Hallo FTP-server</span><span class="sxs-lookup"><span data-stu-id="34b16-2045">Encrypted credential tooaccess hello FTP server</span></span> |<span data-ttu-id="34b16-2046">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2046">No</span></span> |&nbsp; |
| <span data-ttu-id="34b16-2047">gatewayName</span><span class="sxs-lookup"><span data-stu-id="34b16-2047">gatewayName</span></span> |<span data-ttu-id="34b16-2048">Naam van Hallo Data Management Gateway gateway tooconnect tooan lokale FTP-server</span><span class="sxs-lookup"><span data-stu-id="34b16-2048">Name of hello Data Management Gateway gateway tooconnect tooan on-premises FTP server</span></span> |<span data-ttu-id="34b16-2049">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2049">No</span></span> |&nbsp; |
| <span data-ttu-id="34b16-2050">poort</span><span class="sxs-lookup"><span data-stu-id="34b16-2050">port</span></span> |<span data-ttu-id="34b16-2051">Poort op welke Hallo FTP-server luistert</span><span class="sxs-lookup"><span data-stu-id="34b16-2051">Port on which hello FTP server is listening</span></span> |<span data-ttu-id="34b16-2052">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2052">No</span></span> |<span data-ttu-id="34b16-2053">21</span><span class="sxs-lookup"><span data-stu-id="34b16-2053">21</span></span> |
| <span data-ttu-id="34b16-2054">enableSsl</span><span class="sxs-lookup"><span data-stu-id="34b16-2054">enableSsl</span></span> |<span data-ttu-id="34b16-2055">Opgeven of toouse FTP via SSL/TLS-kanaal</span><span class="sxs-lookup"><span data-stu-id="34b16-2055">Specify whether toouse FTP over SSL/TLS channel</span></span> |<span data-ttu-id="34b16-2056">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2056">No</span></span> |<span data-ttu-id="34b16-2057">De waarde True</span><span class="sxs-lookup"><span data-stu-id="34b16-2057">true</span></span> |
| <span data-ttu-id="34b16-2058">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="34b16-2058">enableServerCertificateValidation</span></span> |<span data-ttu-id="34b16-2059">Opgeven of tooenable server SSL certificaatcontrole wanneer FTP via SSL/TLS-kanaal</span><span class="sxs-lookup"><span data-stu-id="34b16-2059">Specify whether tooenable server SSL certificate validation when using FTP over SSL/TLS channel</span></span> |<span data-ttu-id="34b16-2060">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2060">No</span></span> |<span data-ttu-id="34b16-2061">De waarde True</span><span class="sxs-lookup"><span data-stu-id="34b16-2061">true</span></span> |

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="34b16-2062">Voorbeeld: Anonieme verificatie gebruikt</span><span class="sxs-lookup"><span data-stu-id="34b16-2062">Example: Using Anonymous authentication</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
            "typeProperties": {
            "authenticationType": "Anonymous",
            "host": "myftpserver.com"
        }
    }
}
```

#### <a name="example-using-username-and-password-in-plain-text-for-basic-authentication"></a><span data-ttu-id="34b16-2063">Voorbeeld: Met behulp van gebruikersnaam en wachtwoord in tekst zonder opmaak voor basisverificatie</span><span class="sxs-lookup"><span data-stu-id="34b16-2063">Example: Using username and password in plain text for basic authentication</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "username": "Admin",
            "password": "123456"
        }
    }
}
```

#### <a name="example-using-port-enablessl-enableservercertificatevalidation"></a><span data-ttu-id="34b16-2064">Voorbeeld: Met behulp van poort, enableSsl, enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="34b16-2064">Example: Using port, enableSsl, enableServerCertificateValidation</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",    
            "username": "Admin",
            "password": "123456",
            "port": "21",
            "enableSsl": true,
            "enableServerCertificateValidation": true
        }
    }
}
```

#### <a name="example-using-encryptedcredential-for-authentication-and-gateway"></a><span data-ttu-id="34b16-2065">Voorbeeld: EncryptedCredential gebruiken voor verificatie en gateway</span><span class="sxs-lookup"><span data-stu-id="34b16-2065">Example: Using encryptedCredential for authentication and gateway</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "<onpremgateway>"
        }
      }
}
```

<span data-ttu-id="34b16-2066">Zie voor meer informatie [FTP-connector](data-factory-ftp-connector.md#linked-service-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-2066">For more information, see [FTP connector](data-factory-ftp-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="34b16-2067">Gegevensset</span><span class="sxs-lookup"><span data-stu-id="34b16-2067">Dataset</span></span>
<span data-ttu-id="34b16-2068">toodefine een FTP-gegevensset, set Hallo **type** van Hallo gegevensset te**FileShare**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-2068">toodefine an FTP dataset, set hello **type** of hello dataset too**FileShare**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="34b16-2069">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-2069">Property</span></span> | <span data-ttu-id="34b16-2070">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-2070">Description</span></span> | <span data-ttu-id="34b16-2071">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-2071">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-2072">folderPath</span><span class="sxs-lookup"><span data-stu-id="34b16-2072">folderPath</span></span> |<span data-ttu-id="34b16-2073">Submap pad toohello.</span><span class="sxs-lookup"><span data-stu-id="34b16-2073">Sub path toohello folder.</span></span> <span data-ttu-id="34b16-2074">Gebruik van escape-teken ' \ ' voor speciale tekens in Hallo-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="34b16-2074">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="34b16-2075">Zie [voorbeeld gekoppelde service en gegevensset definities](#sample-linked-service-and-dataset-definitions) voor voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="34b16-2075">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="34b16-2076">U kunt deze eigenschap combineren met **partitionBy** toohave mappaden op basis van het segment beginnen of eindigen-datums en tijden.</span><span class="sxs-lookup"><span data-stu-id="34b16-2076">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="34b16-2077">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2077">Yes</span></span> 
| <span data-ttu-id="34b16-2078">fileName</span><span class="sxs-lookup"><span data-stu-id="34b16-2078">fileName</span></span> |<span data-ttu-id="34b16-2079">Hallo-naam van Hallo-bestand opgeven in Hallo **folderPath** als u wilt dat Hallo tabel toorefer tooa specifiek bestand in map Hallo.</span><span class="sxs-lookup"><span data-stu-id="34b16-2079">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="34b16-2080">Als u geen waarde voor deze eigenschap niet opgeeft, wijst Hallo tabel tooall bestanden in de map Hallo.</span><span class="sxs-lookup"><span data-stu-id="34b16-2080">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="34b16-2081">Wanneer fileName niet voor een uitvoergegevensset opgegeven is, zou Hallo van Hallo gegenereerd bestand in worden Hallo volgt deze indeling:</span><span class="sxs-lookup"><span data-stu-id="34b16-2081">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="34b16-2082">Gegevens. <Guid>.txt (voorbeeld: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="34b16-2082">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="34b16-2083">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2083">No</span></span> |
| <span data-ttu-id="34b16-2084">fileFilter</span><span class="sxs-lookup"><span data-stu-id="34b16-2084">fileFilter</span></span> |<span data-ttu-id="34b16-2085">Geef dat een filter toobe tooselect gebruikt een subset van de bestanden in Hallo folderPath in plaats van alle bestanden.</span><span class="sxs-lookup"><span data-stu-id="34b16-2085">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="34b16-2086">Toegestane waarden zijn: `*` (meerdere tekens) en `?` (willekeurig teken).</span><span class="sxs-lookup"><span data-stu-id="34b16-2086">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="34b16-2087">Voorbeelden 1:`"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="34b16-2087">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="34b16-2088">Voorbeeld 2:`"fileFilter": 2016-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="34b16-2088">Example 2: `"fileFilter": 2016-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="34b16-2089">fileFilter geldt voor een invoergegevensset bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="34b16-2089">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="34b16-2090">Deze eigenschap wordt niet ondersteund met HDFS.</span><span class="sxs-lookup"><span data-stu-id="34b16-2090">This property is not supported with HDFS.</span></span> |<span data-ttu-id="34b16-2091">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2091">No</span></span> |
| <span data-ttu-id="34b16-2092">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="34b16-2092">partitionedBy</span></span> |<span data-ttu-id="34b16-2093">partitionedBy mag gebruikte toospecify een dynamische folderPath bestandsnaam op van de reeksgegevens.</span><span class="sxs-lookup"><span data-stu-id="34b16-2093">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="34b16-2094">Bijvoorbeeld, folderPath geparametriseerde voor elk uur van gegevens.</span><span class="sxs-lookup"><span data-stu-id="34b16-2094">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="34b16-2095">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2095">No</span></span> |
| <span data-ttu-id="34b16-2096">Indeling</span><span class="sxs-lookup"><span data-stu-id="34b16-2096">format</span></span> | <span data-ttu-id="34b16-2097">Hallo na indelingstypen worden ondersteund: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="34b16-2097">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="34b16-2098">Set Hallo **type** eigenschap onder indeling tooone van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="34b16-2098">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="34b16-2099">Zie voor meer informatie [tekstindeling](data-factory-supported-file-and-compression-formats.md#text-format), [Json-indeling](data-factory-supported-file-and-compression-formats.md#json-format), [Avro-indeling](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc indeling](data-factory-supported-file-and-compression-formats.md#orc-format), en [parketvloeren indeling](data-factory-supported-file-and-compression-formats.md#parquet-format) secties.</span><span class="sxs-lookup"><span data-stu-id="34b16-2099">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="34b16-2100">Als u wilt dat te**kopiëren van bestanden als-is** tussen bestandsgebaseerde winkels (binaire kopiëren) Hallo indeling sectie in beide definities invoer en uitvoer gegevensset overslaan.</span><span class="sxs-lookup"><span data-stu-id="34b16-2100">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="34b16-2101">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2101">No</span></span> |
| <span data-ttu-id="34b16-2102">Compressie</span><span class="sxs-lookup"><span data-stu-id="34b16-2102">compression</span></span> | <span data-ttu-id="34b16-2103">Hallo-type en compressieniveau voor Hallo gegevens opgeven.</span><span class="sxs-lookup"><span data-stu-id="34b16-2103">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="34b16-2104">Ondersteunde typen zijn: **GZip**, **Deflate**, **BZip2**, en **ZipDeflate**; en ondersteunde niveaus: **optimale** en **snelst**.</span><span class="sxs-lookup"><span data-stu-id="34b16-2104">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="34b16-2105">Zie voor meer informatie [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="34b16-2105">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="34b16-2106">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2106">No</span></span> |
| <span data-ttu-id="34b16-2107">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="34b16-2107">useBinaryTransfer</span></span> |<span data-ttu-id="34b16-2108">Geef binaire overdrachtsmodus of gebruiken.</span><span class="sxs-lookup"><span data-stu-id="34b16-2108">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="34b16-2109">De waarde True voor binaire modus en ONWAAR ASCII.</span><span class="sxs-lookup"><span data-stu-id="34b16-2109">True for binary mode and false ASCII.</span></span> <span data-ttu-id="34b16-2110">Standaardwaarde: True.</span><span class="sxs-lookup"><span data-stu-id="34b16-2110">Default value: True.</span></span> <span data-ttu-id="34b16-2111">Deze eigenschap kan alleen worden gebruikt wanneer de bijbehorende gekoppelde-servicetype is van het type: FtpServer.</span><span class="sxs-lookup"><span data-stu-id="34b16-2111">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="34b16-2112">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2112">No</span></span> |

> [!NOTE]
> <span data-ttu-id="34b16-2113">bestandsnaam en fileFilter worden niet gelijktijdig gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-2113">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="34b16-2114">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-2114">Example</span></span>

```json
{
    "name": "FTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "FTPLinkedService",
        "typeProperties": {
            "folderPath": "<path tooshared folder>",
            "fileName": "test.csv",
            "useBinaryTransfer": true
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="34b16-2115">Zie voor meer informatie [FTP-connector](data-factory-ftp-connector.md#dataset-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-2115">For more information, see [FTP connector](data-factory-ftp-connector.md#dataset-properties) article.</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="34b16-2116">Systeem bronnen in de kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="34b16-2116">File System Source in Copy Activity</span></span>
<span data-ttu-id="34b16-2117">Als u gegevens uit een FTP-server kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**FileSystemSource**, en opgeven na eigenschappen in Hallo **bron** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-2117">If you are copying data from an FTP server, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="34b16-2118">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-2118">Property</span></span> | <span data-ttu-id="34b16-2119">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-2119">Description</span></span> | <span data-ttu-id="34b16-2120">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="34b16-2120">Allowed values</span></span> | <span data-ttu-id="34b16-2121">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-2121">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-2122">Recursieve</span><span class="sxs-lookup"><span data-stu-id="34b16-2122">recursive</span></span> |<span data-ttu-id="34b16-2123">Hiermee wordt aangegeven of Hallo gegevens recursief is gelezen vanuit Hallo submappen of alleen vanuit de opgegeven map Hallo.</span><span class="sxs-lookup"><span data-stu-id="34b16-2123">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="34b16-2124">True, False (standaard)</span><span class="sxs-lookup"><span data-stu-id="34b16-2124">True, False (default)</span></span> |<span data-ttu-id="34b16-2125">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2125">No</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-2126">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-2126">Example</span></span>

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "FTPToBlobCopy",
            "inputs": [{
                "name": "FtpFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-08-24T18:00:00",
        "end": "2016-08-24T19:00:00"
    }
}
```

<span data-ttu-id="34b16-2127">Zie voor meer informatie [FTP-connector](data-factory-ftp-connector.md#copy-activity-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-2127">For more information, see [FTP connector](data-factory-ftp-connector.md#copy-activity-properties) article.</span></span>


## <a name="hdfs"></a><span data-ttu-id="34b16-2128">HDFS</span><span class="sxs-lookup"><span data-stu-id="34b16-2128">HDFS</span></span>

### <a name="linked-service"></a><span data-ttu-id="34b16-2129">Gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="34b16-2129">Linked service</span></span>
<span data-ttu-id="34b16-2130">een HDFS toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**Hdfs**, en opgeven na eigenschappen in Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-2130">toodefine a HDFS linked service, set hello **type** of hello linked service too**Hdfs**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="34b16-2131">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-2131">Property</span></span> | <span data-ttu-id="34b16-2132">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-2132">Description</span></span> | <span data-ttu-id="34b16-2133">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-2133">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-2134">type</span><span class="sxs-lookup"><span data-stu-id="34b16-2134">type</span></span> |<span data-ttu-id="34b16-2135">Hallo type eigenschap moet worden ingesteld op: **Hdfs**</span><span class="sxs-lookup"><span data-stu-id="34b16-2135">hello type property must be set to: **Hdfs**</span></span> |<span data-ttu-id="34b16-2136">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2136">Yes</span></span> |
| <span data-ttu-id="34b16-2137">URL</span><span class="sxs-lookup"><span data-stu-id="34b16-2137">Url</span></span> |<span data-ttu-id="34b16-2138">URL toohello HDFS</span><span class="sxs-lookup"><span data-stu-id="34b16-2138">URL toohello HDFS</span></span> |<span data-ttu-id="34b16-2139">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2139">Yes</span></span> |
| <span data-ttu-id="34b16-2140">authenticationType</span><span class="sxs-lookup"><span data-stu-id="34b16-2140">authenticationType</span></span> |<span data-ttu-id="34b16-2141">Anoniem, of Windows.</span><span class="sxs-lookup"><span data-stu-id="34b16-2141">Anonymous, or Windows.</span></span> <br><br> <span data-ttu-id="34b16-2142">toouse **Kerberos-verificatie** voor HDFS-connector te verwijzen[in deze sectie](#use-kerberos-authentication-for-hdfs-connector) tooset van uw on-premises omgeving dienovereenkomstig.</span><span class="sxs-lookup"><span data-stu-id="34b16-2142">toouse **Kerberos authentication** for HDFS connector, refer too[this section](#use-kerberos-authentication-for-hdfs-connector) tooset up your on-premises environment accordingly.</span></span> |<span data-ttu-id="34b16-2143">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2143">Yes</span></span> |
| <span data-ttu-id="34b16-2144">Gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="34b16-2144">userName</span></span> |<span data-ttu-id="34b16-2145">Gebruikersnaam voor Windows-verificatie.</span><span class="sxs-lookup"><span data-stu-id="34b16-2145">Username for Windows authentication.</span></span> |<span data-ttu-id="34b16-2146">Ja (voor Windows-verificatie)</span><span class="sxs-lookup"><span data-stu-id="34b16-2146">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="34b16-2147">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="34b16-2147">password</span></span> |<span data-ttu-id="34b16-2148">Wachtwoord voor Windows-verificatie.</span><span class="sxs-lookup"><span data-stu-id="34b16-2148">Password for Windows authentication.</span></span> |<span data-ttu-id="34b16-2149">Ja (voor Windows-verificatie)</span><span class="sxs-lookup"><span data-stu-id="34b16-2149">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="34b16-2150">gatewayName</span><span class="sxs-lookup"><span data-stu-id="34b16-2150">gatewayName</span></span> |<span data-ttu-id="34b16-2151">Naam van Hallo-gateway die Hallo Data Factory-service moet tooconnect toohello HDFS gebruiken.</span><span class="sxs-lookup"><span data-stu-id="34b16-2151">Name of hello gateway that hello Data Factory service should use tooconnect toohello HDFS.</span></span> |<span data-ttu-id="34b16-2152">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2152">Yes</span></span> |
| <span data-ttu-id="34b16-2153">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="34b16-2153">encryptedCredential</span></span> |<span data-ttu-id="34b16-2154">[Nieuwe AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) uitvoer van de referentie voor Hallo-toegang.</span><span class="sxs-lookup"><span data-stu-id="34b16-2154">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) output of hello access credential.</span></span> |<span data-ttu-id="34b16-2155">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2155">No</span></span> |

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="34b16-2156">Voorbeeld: Anonieme verificatie gebruikt</span><span class="sxs-lookup"><span data-stu-id="34b16-2156">Example: Using Anonymous authentication</span></span>

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "userName": "hadoop",
            "url": "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-windows-authentication"></a><span data-ttu-id="34b16-2157">Voorbeeld: Met behulp van Windows-verificatie</span><span class="sxs-lookup"><span data-stu-id="34b16-2157">Example: Using Windows authentication</span></span>

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url": "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="34b16-2158">Zie voor meer informatie [HDFS connector](#data-factory-hdfs-connector.md#linked-service-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-2158">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="34b16-2159">Gegevensset</span><span class="sxs-lookup"><span data-stu-id="34b16-2159">Dataset</span></span>
<span data-ttu-id="34b16-2160">toodefine een gegevensset HDFS set Hallo **type** van Hallo gegevensset te**FileShare**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-2160">toodefine a HDFS dataset, set hello **type** of hello dataset too**FileShare**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="34b16-2161">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-2161">Property</span></span> | <span data-ttu-id="34b16-2162">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-2162">Description</span></span> | <span data-ttu-id="34b16-2163">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-2163">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-2164">folderPath</span><span class="sxs-lookup"><span data-stu-id="34b16-2164">folderPath</span></span> |<span data-ttu-id="34b16-2165">Pad toohello map.</span><span class="sxs-lookup"><span data-stu-id="34b16-2165">Path toohello folder.</span></span> <span data-ttu-id="34b16-2166">Voorbeeld:`myfolder`</span><span class="sxs-lookup"><span data-stu-id="34b16-2166">Example: `myfolder`</span></span><br/><br/><span data-ttu-id="34b16-2167">Gebruik van escape-teken ' \ ' voor speciale tekens in Hallo-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="34b16-2167">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="34b16-2168">Bijvoorbeeld: map opgeven voor folder\subfolder,\\\\submap en geef voor d:\samplefolder, d:\\\\Voorbeeldmap.</span><span class="sxs-lookup"><span data-stu-id="34b16-2168">For example: for folder\subfolder, specify folder\\\\subfolder and for d:\samplefolder, specify d:\\\\samplefolder.</span></span><br/><br/><span data-ttu-id="34b16-2169">U kunt deze eigenschap combineren met **partitionBy** toohave mappaden op basis van het segment beginnen of eindigen-datums en tijden.</span><span class="sxs-lookup"><span data-stu-id="34b16-2169">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="34b16-2170">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2170">Yes</span></span> |
| <span data-ttu-id="34b16-2171">fileName</span><span class="sxs-lookup"><span data-stu-id="34b16-2171">fileName</span></span> |<span data-ttu-id="34b16-2172">Hallo-naam van Hallo-bestand opgeven in Hallo **folderPath** als u wilt dat Hallo tabel toorefer tooa specifiek bestand in map Hallo.</span><span class="sxs-lookup"><span data-stu-id="34b16-2172">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="34b16-2173">Als u geen waarde voor deze eigenschap niet opgeeft, wijst Hallo tabel tooall bestanden in de map Hallo.</span><span class="sxs-lookup"><span data-stu-id="34b16-2173">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="34b16-2174">Wanneer fileName niet voor een uitvoergegevensset opgegeven is, zou Hallo van Hallo gegenereerd bestand in worden Hallo volgt deze indeling:</span><span class="sxs-lookup"><span data-stu-id="34b16-2174">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="34b16-2175">Gegevens. <Guid>.txt (voorbeeld:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="34b16-2175">Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="34b16-2176">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2176">No</span></span> |
| <span data-ttu-id="34b16-2177">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="34b16-2177">partitionedBy</span></span> |<span data-ttu-id="34b16-2178">partitionedBy mag gebruikte toospecify een dynamische folderPath bestandsnaam op van de reeksgegevens.</span><span class="sxs-lookup"><span data-stu-id="34b16-2178">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="34b16-2179">Voorbeeld: folderPath geparametriseerde voor elk uur van gegevens.</span><span class="sxs-lookup"><span data-stu-id="34b16-2179">Example: folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="34b16-2180">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2180">No</span></span> |
| <span data-ttu-id="34b16-2181">Indeling</span><span class="sxs-lookup"><span data-stu-id="34b16-2181">format</span></span> | <span data-ttu-id="34b16-2182">Hallo na indelingstypen worden ondersteund: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="34b16-2182">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="34b16-2183">Set Hallo **type** eigenschap onder indeling tooone van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="34b16-2183">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="34b16-2184">Zie voor meer informatie [tekstindeling](data-factory-supported-file-and-compression-formats.md#text-format), [Json-indeling](data-factory-supported-file-and-compression-formats.md#json-format), [Avro-indeling](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc indeling](data-factory-supported-file-and-compression-formats.md#orc-format), en [parketvloeren indeling](data-factory-supported-file-and-compression-formats.md#parquet-format) secties.</span><span class="sxs-lookup"><span data-stu-id="34b16-2184">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="34b16-2185">Als u wilt dat te**kopiëren van bestanden als-is** tussen bestandsgebaseerde winkels (binaire kopiëren) Hallo indeling sectie in beide definities invoer en uitvoer gegevensset overslaan.</span><span class="sxs-lookup"><span data-stu-id="34b16-2185">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="34b16-2186">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2186">No</span></span> |
| <span data-ttu-id="34b16-2187">Compressie</span><span class="sxs-lookup"><span data-stu-id="34b16-2187">compression</span></span> | <span data-ttu-id="34b16-2188">Hallo-type en compressieniveau voor Hallo gegevens opgeven.</span><span class="sxs-lookup"><span data-stu-id="34b16-2188">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="34b16-2189">Ondersteunde typen zijn: **GZip**, **Deflate**, **BZip2**, en **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="34b16-2189">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="34b16-2190">Ondersteunde niveaus: **optimale** en **snelst**.</span><span class="sxs-lookup"><span data-stu-id="34b16-2190">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="34b16-2191">Zie voor meer informatie [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="34b16-2191">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="34b16-2192">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2192">No</span></span> |

> [!NOTE]
> <span data-ttu-id="34b16-2193">bestandsnaam en fileFilter worden niet gelijktijdig gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-2193">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="34b16-2194">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-2194">Example</span></span>

```json
{
    "name": "InputDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "HDFSLinkedService",
        "typeProperties": {
            "folderPath": "DataTransfer/UnitTest/"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="34b16-2195">Zie voor meer informatie [HDFS connector](#data-factory-hdfs-connector.md#dataset-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-2195">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#dataset-properties) article.</span></span> 

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="34b16-2196">Systeem bronnen in de kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="34b16-2196">File System Source in Copy Activity</span></span>
<span data-ttu-id="34b16-2197">Als u gegevens uit HDFS kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**FileSystemSource**, en opgeven na eigenschappen in Hallo **bron** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-2197">If you are copying data from HDFS, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>

<span data-ttu-id="34b16-2198">**FileSystemSource** ondersteunt Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="34b16-2198">**FileSystemSource** supports hello following properties:</span></span>

| <span data-ttu-id="34b16-2199">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-2199">Property</span></span> | <span data-ttu-id="34b16-2200">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-2200">Description</span></span> | <span data-ttu-id="34b16-2201">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="34b16-2201">Allowed values</span></span> | <span data-ttu-id="34b16-2202">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-2202">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-2203">Recursieve</span><span class="sxs-lookup"><span data-stu-id="34b16-2203">recursive</span></span> |<span data-ttu-id="34b16-2204">Hiermee wordt aangegeven of Hallo gegevens recursief is gelezen vanuit Hallo submappen of alleen vanuit de opgegeven map Hallo.</span><span class="sxs-lookup"><span data-stu-id="34b16-2204">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="34b16-2205">True, False (standaard)</span><span class="sxs-lookup"><span data-stu-id="34b16-2205">True, False (default)</span></span> |<span data-ttu-id="34b16-2206">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2206">No</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-2207">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-2207">Example</span></span>

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "HdfsToBlobCopy",
            "inputs": [{
                "name": "InputDataset"
            }],
            "outputs": [{
                "name": "OutputDataset"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="34b16-2208">Zie voor meer informatie [HDFS connector](#data-factory-hdfs-connector.md#copy-activity-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-2208">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#copy-activity-properties) article.</span></span>

## <a name="sftp"></a><span data-ttu-id="34b16-2209">SFTP</span><span class="sxs-lookup"><span data-stu-id="34b16-2209">SFTP</span></span>


### <a name="linked-service"></a><span data-ttu-id="34b16-2210">Gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="34b16-2210">Linked service</span></span>
<span data-ttu-id="34b16-2211">toodefine een SFTP gekoppelde service, set Hallo **type** Hallo gekoppelde service te**Sftp**, en opgeven na eigenschappen in Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-2211">toodefine an SFTP linked service, set hello **type** of hello linked service too**Sftp**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="34b16-2212">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-2212">Property</span></span> | <span data-ttu-id="34b16-2213">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-2213">Description</span></span> | <span data-ttu-id="34b16-2214">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-2214">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-2215">host</span><span class="sxs-lookup"><span data-stu-id="34b16-2215">host</span></span> | <span data-ttu-id="34b16-2216">Naam of IP-adres van Hallo SFTP-server.</span><span class="sxs-lookup"><span data-stu-id="34b16-2216">Name or IP address of hello SFTP server.</span></span> |<span data-ttu-id="34b16-2217">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2217">Yes</span></span> |
| <span data-ttu-id="34b16-2218">poort</span><span class="sxs-lookup"><span data-stu-id="34b16-2218">port</span></span> |<span data-ttu-id="34b16-2219">De poort op welke Hallo SFTP-server luistert.</span><span class="sxs-lookup"><span data-stu-id="34b16-2219">Port on which hello SFTP server is listening.</span></span> <span data-ttu-id="34b16-2220">de standaardwaarde Hallo is: 21</span><span class="sxs-lookup"><span data-stu-id="34b16-2220">hello default value is: 21</span></span> |<span data-ttu-id="34b16-2221">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2221">No</span></span> |
| <span data-ttu-id="34b16-2222">authenticationType</span><span class="sxs-lookup"><span data-stu-id="34b16-2222">authenticationType</span></span> |<span data-ttu-id="34b16-2223">Geef het verificatietype.</span><span class="sxs-lookup"><span data-stu-id="34b16-2223">Specify authentication type.</span></span> <span data-ttu-id="34b16-2224">Toegestane waarden: **Basic**, **SshPublicKey**.</span><span class="sxs-lookup"><span data-stu-id="34b16-2224">Allowed values: **Basic**, **SshPublicKey**.</span></span> <br><br> <span data-ttu-id="34b16-2225">Raadpleeg te[Using basisverificatie](#using-basic-authentication) en [met behulp van SSH openbare-sleutelauthenticatie](#using-ssh-public-key-authentication) respectievelijk secties over meer eigenschappen en voorbeelden van JSON.</span><span class="sxs-lookup"><span data-stu-id="34b16-2225">Refer too[Using basic authentication](#using-basic-authentication) and [Using SSH public key authentication](#using-ssh-public-key-authentication) sections on more properties and JSON samples respectively.</span></span> |<span data-ttu-id="34b16-2226">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2226">Yes</span></span> |
| <span data-ttu-id="34b16-2227">skipHostKeyValidation</span><span class="sxs-lookup"><span data-stu-id="34b16-2227">skipHostKeyValidation</span></span> | <span data-ttu-id="34b16-2228">Geef op of tooskip sleutel validatie hosten.</span><span class="sxs-lookup"><span data-stu-id="34b16-2228">Specify whether tooskip host key validation.</span></span> | <span data-ttu-id="34b16-2229">Nee.</span><span class="sxs-lookup"><span data-stu-id="34b16-2229">No.</span></span> <span data-ttu-id="34b16-2230">standaardwaarde Hallo: false</span><span class="sxs-lookup"><span data-stu-id="34b16-2230">hello default value: false</span></span> |
| <span data-ttu-id="34b16-2231">hostKeyFingerprint</span><span class="sxs-lookup"><span data-stu-id="34b16-2231">hostKeyFingerprint</span></span> | <span data-ttu-id="34b16-2232">Hallo-vingerafdruk van Hallo hostsleutel opgeven.</span><span class="sxs-lookup"><span data-stu-id="34b16-2232">Specify hello finger print of hello host key.</span></span> | <span data-ttu-id="34b16-2233">Ja als hello `skipHostKeyValidation` toofalse is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="34b16-2233">Yes if hello `skipHostKeyValidation` is set toofalse.</span></span>  |
| <span data-ttu-id="34b16-2234">gatewayName</span><span class="sxs-lookup"><span data-stu-id="34b16-2234">gatewayName</span></span> |<span data-ttu-id="34b16-2235">Naam van Hallo Data Management Gateway tooconnect tooan een on-premises SFTP-server.</span><span class="sxs-lookup"><span data-stu-id="34b16-2235">Name of hello Data Management Gateway tooconnect tooan on-premises SFTP server.</span></span> | <span data-ttu-id="34b16-2236">Ja als u kopiëren van gegevens uit een on-premises SFTP-server.</span><span class="sxs-lookup"><span data-stu-id="34b16-2236">Yes if copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="34b16-2237">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="34b16-2237">encryptedCredential</span></span> | <span data-ttu-id="34b16-2238">Versleutelde referentie tooaccess Hallo SFTP-server.</span><span class="sxs-lookup"><span data-stu-id="34b16-2238">Encrypted credential tooaccess hello SFTP server.</span></span> <span data-ttu-id="34b16-2239">Automatisch gegenereerd als u basisverificatie (gebruikersnaam en wachtwoord) of SshPublicKey verificatie (gebruikersnaam + pad naar de persoonlijke sleutel of inhoud) in kopiëren wizard of Hallo ClickOnce pop-up dialoogvenster opgeven.</span><span class="sxs-lookup"><span data-stu-id="34b16-2239">Auto-generated when you specify basic authentication (username + password) or SshPublicKey authentication (username + private key path or content) in copy wizard or hello ClickOnce popup dialog.</span></span> | <span data-ttu-id="34b16-2240">Nee.</span><span class="sxs-lookup"><span data-stu-id="34b16-2240">No.</span></span> <span data-ttu-id="34b16-2241">Alleen van toepassing wanneer het kopiëren van gegevens uit een on-premises SFTP-server.</span><span class="sxs-lookup"><span data-stu-id="34b16-2241">Apply only when copying data from an on-premises SFTP server.</span></span> |

#### <a name="example-using-basic-authentication"></a><span data-ttu-id="34b16-2242">Voorbeeld: Met behulp van basisverificatie</span><span class="sxs-lookup"><span data-stu-id="34b16-2242">Example: Using basic authentication</span></span>

<span data-ttu-id="34b16-2243">Basisverificatie toouse ingesteld `authenticationType` als `Basic`, en geef de volgende eigenschappen afgezien van SFTP connector algemene die zijn geïntroduceerd in de laatste sectie Hallo HALLO hallo:</span><span class="sxs-lookup"><span data-stu-id="34b16-2243">toouse basic authentication, set `authenticationType` as `Basic`, and specify hello following properties besides hello SFTP connector generic ones introduced in hello last section:</span></span>

| <span data-ttu-id="34b16-2244">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-2244">Property</span></span> | <span data-ttu-id="34b16-2245">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-2245">Description</span></span> | <span data-ttu-id="34b16-2246">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-2246">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-2247">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="34b16-2247">username</span></span> | <span data-ttu-id="34b16-2248">Gebruiker met toegang toohello SFTP-server.</span><span class="sxs-lookup"><span data-stu-id="34b16-2248">User who has access toohello SFTP server.</span></span> |<span data-ttu-id="34b16-2249">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2249">Yes</span></span> |
| <span data-ttu-id="34b16-2250">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="34b16-2250">password</span></span> | <span data-ttu-id="34b16-2251">Wachtwoord voor gebruiker hello (gebruikersnaam).</span><span class="sxs-lookup"><span data-stu-id="34b16-2251">Password for hello user (username).</span></span> | <span data-ttu-id="34b16-2252">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2252">Yes</span></span> |

```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<SFTP server name or IP address>",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "password": "xxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-basic-authentication-with-encrypted-credential"></a><span data-ttu-id="34b16-2253">Voorbeeld: Basisverificatie met versleutelde referentie **</span><span class="sxs-lookup"><span data-stu-id="34b16-2253">Example: Basic authentication with encrypted credential**</span></span>

```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<FTP server name or IP address>",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="using-ssh-public-key-authentication"></a><span data-ttu-id="34b16-2254">Met behulp van de openbare-sleutelauthenticatie SSH: **</span><span class="sxs-lookup"><span data-stu-id="34b16-2254">Using SSH public key authentication:**</span></span>

<span data-ttu-id="34b16-2255">Basisverificatie toouse ingesteld `authenticationType` als `SshPublicKey`, en geef de volgende eigenschappen afgezien van SFTP connector algemene die zijn geïntroduceerd in de laatste sectie Hallo HALLO hallo:</span><span class="sxs-lookup"><span data-stu-id="34b16-2255">toouse basic authentication, set `authenticationType` as `SshPublicKey`, and specify hello following properties besides hello SFTP connector generic ones introduced in hello last section:</span></span>

| <span data-ttu-id="34b16-2256">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-2256">Property</span></span> | <span data-ttu-id="34b16-2257">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-2257">Description</span></span> | <span data-ttu-id="34b16-2258">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-2258">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-2259">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="34b16-2259">username</span></span> |<span data-ttu-id="34b16-2260">Gebruiker met toegang toohello SFTP-server</span><span class="sxs-lookup"><span data-stu-id="34b16-2260">User who has access toohello SFTP server</span></span> |<span data-ttu-id="34b16-2261">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2261">Yes</span></span> |
| <span data-ttu-id="34b16-2262">privateKeyPath</span><span class="sxs-lookup"><span data-stu-id="34b16-2262">privateKeyPath</span></span> | <span data-ttu-id="34b16-2263">Geef het absolute pad toohello persoonlijke sleutelbestand dat gateway kunt openen.</span><span class="sxs-lookup"><span data-stu-id="34b16-2263">Specify absolute path toohello private key file that gateway can access.</span></span> | <span data-ttu-id="34b16-2264">Geef beide Hallo `privateKeyPath` of `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="34b16-2264">Specify either hello `privateKeyPath` or `privateKeyContent`.</span></span> <br><br> <span data-ttu-id="34b16-2265">Alleen van toepassing wanneer het kopiëren van gegevens uit een on-premises SFTP-server.</span><span class="sxs-lookup"><span data-stu-id="34b16-2265">Apply only when copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="34b16-2266">privateKeyContent</span><span class="sxs-lookup"><span data-stu-id="34b16-2266">privateKeyContent</span></span> | <span data-ttu-id="34b16-2267">Een geserialiseerde tekenreeks Hallo-inhoud met persoonlijke sleutel.</span><span class="sxs-lookup"><span data-stu-id="34b16-2267">A serialized string of hello private key content.</span></span> <span data-ttu-id="34b16-2268">Hallo Wizard kopiëren kunt Hallo persoonlijke sleutelbestand lezen inhoud en extraheren Hallo persoonlijke sleutel automatisch.</span><span class="sxs-lookup"><span data-stu-id="34b16-2268">hello Copy Wizard can read hello private key file and extract hello private key content automatically.</span></span> <span data-ttu-id="34b16-2269">Als u van andere hulpprogramma/SDK gebruikmaakt, gebruikt u de Hallo privateKeyPath eigenschap.</span><span class="sxs-lookup"><span data-stu-id="34b16-2269">If you are using any other tool/SDK, use hello privateKeyPath property instead.</span></span> | <span data-ttu-id="34b16-2270">Geef beide Hallo `privateKeyPath` of `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="34b16-2270">Specify either hello `privateKeyPath` or `privateKeyContent`.</span></span> |
| <span data-ttu-id="34b16-2271">Wachtwoordzin</span><span class="sxs-lookup"><span data-stu-id="34b16-2271">passPhrase</span></span> | <span data-ttu-id="34b16-2272">Hallo pass woordgroep en het wachtwoord toodecrypt Hallo persoonlijke sleutel opgeven als Hallo-sleutelbestand is beveiligd met een wachtwoordzin.</span><span class="sxs-lookup"><span data-stu-id="34b16-2272">Specify hello pass phrase/password toodecrypt hello private key if hello key file is protected by a pass phrase.</span></span> | <span data-ttu-id="34b16-2273">Ja als Hallo-bestand met persoonlijke sleutel wordt beveiligd door een wachtwoordzin.</span><span class="sxs-lookup"><span data-stu-id="34b16-2273">Yes if hello private key file is protected by a pass phrase.</span></span> |

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyPath",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<FTP server name or IP address>",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyPath": "D:\\privatekey_openssh",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true,
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a><span data-ttu-id="34b16-2274">Voorbeeld: SshPublicKey verificatie met persoonlijke sleutel inhoud **</span><span class="sxs-lookup"><span data-stu-id="34b16-2274">Example: SshPublicKey authentication using private key content**</span></span>

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyContent",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver.westus.cloudapp.azure.com",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyContent": "<base64 string of hello private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

<span data-ttu-id="34b16-2275">Zie voor meer informatie [SFTP connector](data-factory-sftp-connector.md#linked-service-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-2275">For more information, see [SFTP connector](data-factory-sftp-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="34b16-2276">Gegevensset</span><span class="sxs-lookup"><span data-stu-id="34b16-2276">Dataset</span></span>
<span data-ttu-id="34b16-2277">toodefine een gegevensset SFTP set Hallo **type** van Hallo gegevensset te**FileShare**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-2277">toodefine an SFTP dataset, set hello **type** of hello dataset too**FileShare**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="34b16-2278">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-2278">Property</span></span> | <span data-ttu-id="34b16-2279">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-2279">Description</span></span> | <span data-ttu-id="34b16-2280">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-2280">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-2281">folderPath</span><span class="sxs-lookup"><span data-stu-id="34b16-2281">folderPath</span></span> |<span data-ttu-id="34b16-2282">Submap pad toohello.</span><span class="sxs-lookup"><span data-stu-id="34b16-2282">Sub path toohello folder.</span></span> <span data-ttu-id="34b16-2283">Gebruik van escape-teken ' \ ' voor speciale tekens in Hallo-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="34b16-2283">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="34b16-2284">Zie [voorbeeld gekoppelde service en gegevensset definities](#sample-linked-service-and-dataset-definitions) voor voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="34b16-2284">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="34b16-2285">U kunt deze eigenschap combineren met **partitionBy** toohave mappaden op basis van het segment beginnen of eindigen-datums en tijden.</span><span class="sxs-lookup"><span data-stu-id="34b16-2285">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="34b16-2286">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2286">Yes</span></span> |
| <span data-ttu-id="34b16-2287">fileName</span><span class="sxs-lookup"><span data-stu-id="34b16-2287">fileName</span></span> |<span data-ttu-id="34b16-2288">Hallo-naam van Hallo-bestand opgeven in Hallo **folderPath** als u wilt dat Hallo tabel toorefer tooa specifiek bestand in map Hallo.</span><span class="sxs-lookup"><span data-stu-id="34b16-2288">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="34b16-2289">Als u geen waarde voor deze eigenschap niet opgeeft, wijst Hallo tabel tooall bestanden in de map Hallo.</span><span class="sxs-lookup"><span data-stu-id="34b16-2289">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="34b16-2290">Wanneer fileName niet voor een uitvoergegevensset opgegeven is, zou Hallo van Hallo gegenereerd bestand in worden Hallo volgt deze indeling:</span><span class="sxs-lookup"><span data-stu-id="34b16-2290">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="34b16-2291">Gegevens. <Guid>.txt (voorbeeld: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="34b16-2291">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="34b16-2292">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2292">No</span></span> |
| <span data-ttu-id="34b16-2293">fileFilter</span><span class="sxs-lookup"><span data-stu-id="34b16-2293">fileFilter</span></span> |<span data-ttu-id="34b16-2294">Geef dat een filter toobe tooselect gebruikt een subset van de bestanden in Hallo folderPath in plaats van alle bestanden.</span><span class="sxs-lookup"><span data-stu-id="34b16-2294">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="34b16-2295">Toegestane waarden zijn: `*` (meerdere tekens) en `?` (willekeurig teken).</span><span class="sxs-lookup"><span data-stu-id="34b16-2295">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="34b16-2296">Voorbeelden 1:`"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="34b16-2296">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="34b16-2297">Voorbeeld 2:`"fileFilter": 2016-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="34b16-2297">Example 2: `"fileFilter": 2016-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="34b16-2298">fileFilter geldt voor een invoergegevensset bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="34b16-2298">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="34b16-2299">Deze eigenschap wordt niet ondersteund met HDFS.</span><span class="sxs-lookup"><span data-stu-id="34b16-2299">This property is not supported with HDFS.</span></span> |<span data-ttu-id="34b16-2300">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2300">No</span></span> |
| <span data-ttu-id="34b16-2301">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="34b16-2301">partitionedBy</span></span> |<span data-ttu-id="34b16-2302">partitionedBy mag gebruikte toospecify een dynamische folderPath bestandsnaam op van de reeksgegevens.</span><span class="sxs-lookup"><span data-stu-id="34b16-2302">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="34b16-2303">Bijvoorbeeld, folderPath geparametriseerde voor elk uur van gegevens.</span><span class="sxs-lookup"><span data-stu-id="34b16-2303">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="34b16-2304">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2304">No</span></span> |
| <span data-ttu-id="34b16-2305">Indeling</span><span class="sxs-lookup"><span data-stu-id="34b16-2305">format</span></span> | <span data-ttu-id="34b16-2306">Hallo na indelingstypen worden ondersteund: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="34b16-2306">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="34b16-2307">Set Hallo **type** eigenschap onder indeling tooone van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="34b16-2307">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="34b16-2308">Zie voor meer informatie [tekstindeling](data-factory-supported-file-and-compression-formats.md#text-format), [Json-indeling](data-factory-supported-file-and-compression-formats.md#json-format), [Avro-indeling](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc indeling](data-factory-supported-file-and-compression-formats.md#orc-format), en [parketvloeren indeling](data-factory-supported-file-and-compression-formats.md#parquet-format) secties.</span><span class="sxs-lookup"><span data-stu-id="34b16-2308">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="34b16-2309">Als u wilt dat te**kopiëren van bestanden als-is** tussen bestandsgebaseerde winkels (binaire kopiëren) Hallo indeling sectie in beide definities invoer en uitvoer gegevensset overslaan.</span><span class="sxs-lookup"><span data-stu-id="34b16-2309">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="34b16-2310">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2310">No</span></span> |
| <span data-ttu-id="34b16-2311">Compressie</span><span class="sxs-lookup"><span data-stu-id="34b16-2311">compression</span></span> | <span data-ttu-id="34b16-2312">Hallo-type en compressieniveau voor Hallo gegevens opgeven.</span><span class="sxs-lookup"><span data-stu-id="34b16-2312">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="34b16-2313">Ondersteunde typen zijn: **GZip**, **Deflate**, **BZip2**, en **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="34b16-2313">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="34b16-2314">Ondersteunde niveaus: **optimale** en **snelst**.</span><span class="sxs-lookup"><span data-stu-id="34b16-2314">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="34b16-2315">Zie voor meer informatie [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="34b16-2315">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="34b16-2316">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2316">No</span></span> |
| <span data-ttu-id="34b16-2317">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="34b16-2317">useBinaryTransfer</span></span> |<span data-ttu-id="34b16-2318">Geef binaire overdrachtsmodus of gebruiken.</span><span class="sxs-lookup"><span data-stu-id="34b16-2318">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="34b16-2319">De waarde True voor binaire modus en ONWAAR ASCII.</span><span class="sxs-lookup"><span data-stu-id="34b16-2319">True for binary mode and false ASCII.</span></span> <span data-ttu-id="34b16-2320">Standaardwaarde: True.</span><span class="sxs-lookup"><span data-stu-id="34b16-2320">Default value: True.</span></span> <span data-ttu-id="34b16-2321">Deze eigenschap kan alleen worden gebruikt wanneer de bijbehorende gekoppelde-servicetype is van het type: FtpServer.</span><span class="sxs-lookup"><span data-stu-id="34b16-2321">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="34b16-2322">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2322">No</span></span> |

> [!NOTE]
> <span data-ttu-id="34b16-2323">bestandsnaam en fileFilter worden niet gelijktijdig gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-2323">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="34b16-2324">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-2324">Example</span></span>

```json
{
    "name": "SFTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "SftpLinkedService",
        "typeProperties": {
            "folderPath": "<path tooshared folder>",
            "fileName": "test.csv"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="34b16-2325">Zie voor meer informatie [SFTP connector](data-factory-sftp-connector.md#dataset-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-2325">For more information, see [SFTP connector](data-factory-sftp-connector.md#dataset-properties) article.</span></span> 

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="34b16-2326">Systeem bronnen in de kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="34b16-2326">File System Source in Copy Activity</span></span>
<span data-ttu-id="34b16-2327">Als u gegevens uit een bron SFTP kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**FileSystemSource**, en opgeven na eigenschappen in Hallo **bron** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-2327">If you are copying data from an SFTP source, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="34b16-2328">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-2328">Property</span></span> | <span data-ttu-id="34b16-2329">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-2329">Description</span></span> | <span data-ttu-id="34b16-2330">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="34b16-2330">Allowed values</span></span> | <span data-ttu-id="34b16-2331">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-2331">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-2332">Recursieve</span><span class="sxs-lookup"><span data-stu-id="34b16-2332">recursive</span></span> |<span data-ttu-id="34b16-2333">Hiermee wordt aangegeven of Hallo gegevens recursief is gelezen vanuit Hallo submappen of alleen vanuit de opgegeven map Hallo.</span><span class="sxs-lookup"><span data-stu-id="34b16-2333">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="34b16-2334">True, False (standaard)</span><span class="sxs-lookup"><span data-stu-id="34b16-2334">True, False (default)</span></span> |<span data-ttu-id="34b16-2335">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2335">No</span></span> |



#### <a name="example"></a><span data-ttu-id="34b16-2336">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-2336">Example</span></span>

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "SFTPToBlobCopy",
            "inputs": [{
                "name": "SFTPFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2017-02-20T18:00:00",
        "end": "2017-02-20T19:00:00"
    }
}
```

<span data-ttu-id="34b16-2337">Zie voor meer informatie [SFTP connector](data-factory-sftp-connector.md#copy-activity-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-2337">For more information, see [SFTP connector](data-factory-sftp-connector.md#copy-activity-properties) article.</span></span>


## <a name="http"></a><span data-ttu-id="34b16-2338">HTTP</span><span class="sxs-lookup"><span data-stu-id="34b16-2338">HTTP</span></span>

### <a name="linked-service"></a><span data-ttu-id="34b16-2339">Gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="34b16-2339">Linked service</span></span>
<span data-ttu-id="34b16-2340">een HTTP toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**Http**, en opgeven na eigenschappen in Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-2340">toodefine a HTTP linked service, set hello **type** of hello linked service too**Http**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="34b16-2341">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-2341">Property</span></span> | <span data-ttu-id="34b16-2342">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-2342">Description</span></span> | <span data-ttu-id="34b16-2343">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-2343">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-2344">URL</span><span class="sxs-lookup"><span data-stu-id="34b16-2344">url</span></span> | <span data-ttu-id="34b16-2345">Basis-URL toohello webserver</span><span class="sxs-lookup"><span data-stu-id="34b16-2345">Base URL toohello Web Server</span></span> | <span data-ttu-id="34b16-2346">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2346">Yes</span></span> |
| <span data-ttu-id="34b16-2347">authenticationType</span><span class="sxs-lookup"><span data-stu-id="34b16-2347">authenticationType</span></span> | <span data-ttu-id="34b16-2348">Hiermee geeft u het verificatietype Hallo.</span><span class="sxs-lookup"><span data-stu-id="34b16-2348">Specifies hello authentication type.</span></span> <span data-ttu-id="34b16-2349">Toegestane waarden zijn: **anoniem**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="34b16-2349">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span></span> <br><br> <span data-ttu-id="34b16-2350">Raadpleeg toosections onder deze tabel over meer eigenschappen en voorbeelden van JSON respectievelijk voor deze verificatietypen.</span><span class="sxs-lookup"><span data-stu-id="34b16-2350">Refer toosections below this table on more properties and JSON samples for those authentication types respectively.</span></span> | <span data-ttu-id="34b16-2351">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2351">Yes</span></span> |
| <span data-ttu-id="34b16-2352">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="34b16-2352">enableServerCertificateValidation</span></span> | <span data-ttu-id="34b16-2353">Opgeven of tooenable server SSL certificaatcontrole als bron is een HTTPS-webserver</span><span class="sxs-lookup"><span data-stu-id="34b16-2353">Specify whether tooenable server SSL certificate validation if source is HTTPS Web Server</span></span> | <span data-ttu-id="34b16-2354">Nee, de standaardwaarde is true</span><span class="sxs-lookup"><span data-stu-id="34b16-2354">No, default is true</span></span> |
| <span data-ttu-id="34b16-2355">gatewayName</span><span class="sxs-lookup"><span data-stu-id="34b16-2355">gatewayName</span></span> | <span data-ttu-id="34b16-2356">Naam van Hallo Data Management Gateway tooconnect tooan lokale HTTP-bron.</span><span class="sxs-lookup"><span data-stu-id="34b16-2356">Name of hello Data Management Gateway tooconnect tooan on-premises HTTP source.</span></span> | <span data-ttu-id="34b16-2357">Ja als u gegevens kopiëren van een lokale HTTP-bron.</span><span class="sxs-lookup"><span data-stu-id="34b16-2357">Yes if copying data from an on-premises HTTP source.</span></span> |
| <span data-ttu-id="34b16-2358">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="34b16-2358">encryptedCredential</span></span> | <span data-ttu-id="34b16-2359">Versleutelde referentie tooaccess Hallo HTTP-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="34b16-2359">Encrypted credential tooaccess hello HTTP endpoint.</span></span> <span data-ttu-id="34b16-2360">Automatisch wordt gegenereerd wanneer u Hallo verificatiegegevens in kopiëren wizard of Hallo ClickOnce pop-up dialoogvenster configureert.</span><span class="sxs-lookup"><span data-stu-id="34b16-2360">Auto-generated when you configure hello authentication information in copy wizard or hello ClickOnce popup dialog.</span></span> | <span data-ttu-id="34b16-2361">Nee.</span><span class="sxs-lookup"><span data-stu-id="34b16-2361">No.</span></span> <span data-ttu-id="34b16-2362">Alleen van toepassing wanneer het kopiëren van gegevens uit een lokale HTTP-server.</span><span class="sxs-lookup"><span data-stu-id="34b16-2362">Apply only when copying data from an on-premises HTTP server.</span></span> |

#### <a name="example-using-basic-digest-or-windows-authentication"></a><span data-ttu-id="34b16-2363">Voorbeeld: Met behulp van basisverificatie, verificatiesamenvatting of Windows-verificatie</span><span class="sxs-lookup"><span data-stu-id="34b16-2363">Example: Using Basic, Digest, or Windows authentication</span></span>
<span data-ttu-id="34b16-2364">Stel `authenticationType` als `Basic`, `Digest`, of `Windows`, en geef de volgende eigenschappen afgezien van HTTP-connector algemene werden geïntroduceerd hierboven Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="34b16-2364">Set `authenticationType` as `Basic`, `Digest`, or `Windows`, and specify hello following properties besides hello HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="34b16-2365">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-2365">Property</span></span> | <span data-ttu-id="34b16-2366">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-2366">Description</span></span> | <span data-ttu-id="34b16-2367">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-2367">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-2368">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="34b16-2368">username</span></span> | <span data-ttu-id="34b16-2369">Gebruikersnaam tooaccess Hallo HTTP-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="34b16-2369">Username tooaccess hello HTTP endpoint.</span></span> | <span data-ttu-id="34b16-2370">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2370">Yes</span></span> |
| <span data-ttu-id="34b16-2371">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="34b16-2371">password</span></span> | <span data-ttu-id="34b16-2372">Wachtwoord voor gebruiker hello (gebruikersnaam).</span><span class="sxs-lookup"><span data-stu-id="34b16-2372">Password for hello user (username).</span></span> | <span data-ttu-id="34b16-2373">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2373">Yes</span></span> |

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "basic",
            "url": "https://en.wikipedia.org/wiki/",
            "userName": "user name",
            "password": "password"
        }
    }
}
```

#### <a name="example-using-clientcertificate-authentication"></a><span data-ttu-id="34b16-2374">Voorbeeld: ClientCertificate verificatie gebruiken</span><span class="sxs-lookup"><span data-stu-id="34b16-2374">Example: Using ClientCertificate authentication</span></span>

<span data-ttu-id="34b16-2375">Basisverificatie toouse ingesteld `authenticationType` als `ClientCertificate`, en geef de volgende eigenschappen afgezien van HTTP-connector algemene werden geïntroduceerd hierboven Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="34b16-2375">toouse basic authentication, set `authenticationType` as `ClientCertificate`, and specify hello following properties besides hello HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="34b16-2376">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-2376">Property</span></span> | <span data-ttu-id="34b16-2377">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-2377">Description</span></span> | <span data-ttu-id="34b16-2378">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-2378">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-2379">embeddedCertData</span><span class="sxs-lookup"><span data-stu-id="34b16-2379">embeddedCertData</span></span> | <span data-ttu-id="34b16-2380">Hallo Base64-gecodeerde inhoud van de binaire gegevens van Hallo Personal Information Exchange (PFX)-bestand.</span><span class="sxs-lookup"><span data-stu-id="34b16-2380">hello Base64-encoded contents of binary data of hello Personal Information Exchange (PFX) file.</span></span> | <span data-ttu-id="34b16-2381">Geef beide Hallo `embeddedCertData` of `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="34b16-2381">Specify either hello `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="34b16-2382">certThumbprint</span><span class="sxs-lookup"><span data-stu-id="34b16-2382">certThumbprint</span></span> | <span data-ttu-id="34b16-2383">Hallo vingerafdruk van certificaat Hallo die is geïnstalleerd op de gatewaycomputer certificaatarchief.</span><span class="sxs-lookup"><span data-stu-id="34b16-2383">hello thumbprint of hello certificate that was installed on your gateway machine’s cert store.</span></span> <span data-ttu-id="34b16-2384">Alleen van toepassing wanneer het kopiëren van gegevens van een lokale HTTP-bron.</span><span class="sxs-lookup"><span data-stu-id="34b16-2384">Apply only when copying data from an on-premises HTTP source.</span></span> | <span data-ttu-id="34b16-2385">Geef beide Hallo `embeddedCertData` of `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="34b16-2385">Specify either hello `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="34b16-2386">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="34b16-2386">password</span></span> | <span data-ttu-id="34b16-2387">Het wachtwoord die zijn gekoppeld aan het Hallo-certificaat.</span><span class="sxs-lookup"><span data-stu-id="34b16-2387">Password associated with hello certificate.</span></span> | <span data-ttu-id="34b16-2388">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2388">No</span></span> |

<span data-ttu-id="34b16-2389">Als u `certThumbprint` voor verificatie en Hallo-certificaat is geïnstalleerd in het persoonlijke archief van de lokale computer Hallo hello, moet u toogrant Hallo leesmachtiging toohello gateway-service:</span><span class="sxs-lookup"><span data-stu-id="34b16-2389">If you use `certThumbprint` for authentication and hello certificate is installed in hello personal store of hello local computer, you need toogrant hello read permission toohello gateway service:</span></span>

1. <span data-ttu-id="34b16-2390">Start Microsoft Management Console (MMC).</span><span class="sxs-lookup"><span data-stu-id="34b16-2390">Launch Microsoft Management Console (MMC).</span></span> <span data-ttu-id="34b16-2391">Hallo toevoegen **certificaten** -module die Hallo doelen **lokale Computer**.</span><span class="sxs-lookup"><span data-stu-id="34b16-2391">Add hello **Certificates** snap-in that targets hello **Local Computer**.</span></span>
2. <span data-ttu-id="34b16-2392">Vouw **certificaten**, **persoonlijke**, en klik op **certificaten**.</span><span class="sxs-lookup"><span data-stu-id="34b16-2392">Expand **Certificates**, **Personal**, and click **Certificates**.</span></span>
3. <span data-ttu-id="34b16-2393">Met de rechtermuisknop op het Hallo-certificaat uit het persoonlijke archief Hallo en selecteer **alle taken**->**persoonlijke sleutels beheren...**</span><span class="sxs-lookup"><span data-stu-id="34b16-2393">Right-click hello certificate from hello personal store, and select **All Tasks**->**Manage Private Keys...**</span></span>
3. <span data-ttu-id="34b16-2394">Op Hallo **beveiliging** tabblad, waaronder Data Management Gateway Host Service wordt uitgevoerd met Hallo leestoegang toohello certificaat Hallo-gebruikersaccount toevoegen.</span><span class="sxs-lookup"><span data-stu-id="34b16-2394">On hello **Security** tab, add hello user account under which Data Management Gateway Host Service is running with hello read access toohello certificate.</span></span>  

<span data-ttu-id="34b16-2395">**Voorbeeld: met behulp van clientcertificaat:** deze gekoppelde service wordt uw data factory tooan lokale HTTP-webserver.</span><span class="sxs-lookup"><span data-stu-id="34b16-2395">**Example: using client certificate:** This linked service links your data factory tooan on-premises HTTP web server.</span></span> <span data-ttu-id="34b16-2396">Dit maakt gebruik van een clientcertificaat dat is geïnstalleerd op machine Hallo met Data Management Gateway is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="34b16-2396">It uses a client certificate that is installed on hello machine with Data Management Gateway installed.</span></span>

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "certThumbprint": "thumbprint of certificate",
            "gatewayName": "gateway name"
        }
    }
}
```

#### <a name="example-using-client-certificate-in-a-file"></a><span data-ttu-id="34b16-2397">Voorbeeld: clientcertificaat gebruiken in een bestand</span><span class="sxs-lookup"><span data-stu-id="34b16-2397">Example: using client certificate in a file</span></span>
<span data-ttu-id="34b16-2398">Deze gekoppelde service wordt uw data factory tooan lokale HTTP-webserver.</span><span class="sxs-lookup"><span data-stu-id="34b16-2398">This linked service links your data factory tooan on-premises HTTP web server.</span></span> <span data-ttu-id="34b16-2399">Een certificaatbestand op Hallo machine wordt met Data Management Gateway is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="34b16-2399">It uses a client certificate file on hello machine with Data Management Gateway installed.</span></span>

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "embeddedCertData": "base64 encoded cert data",
            "password": "password of cert"
        }
    }
}
```

<span data-ttu-id="34b16-2400">Zie voor meer informatie [HTTP connector](data-factory-http-connector.md#linked-service-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-2400">For more information, see [HTTP connector](data-factory-http-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="34b16-2401">Gegevensset</span><span class="sxs-lookup"><span data-stu-id="34b16-2401">Dataset</span></span>
<span data-ttu-id="34b16-2402">toodefine een HTTP-gegevensset, set Hallo **type** van Hallo gegevensset te**Http**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-2402">toodefine a HTTP dataset, set hello **type** of hello dataset too**Http**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="34b16-2403">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-2403">Property</span></span> | <span data-ttu-id="34b16-2404">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-2404">Description</span></span> | <span data-ttu-id="34b16-2405">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-2405">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="34b16-2406">relativeUrl</span><span class="sxs-lookup"><span data-stu-id="34b16-2406">relativeUrl</span></span> | <span data-ttu-id="34b16-2407">Een relatieve URL toohello-bron die Hallo gegevens bevat.</span><span class="sxs-lookup"><span data-stu-id="34b16-2407">A relative URL toohello resource that contains hello data.</span></span> <span data-ttu-id="34b16-2408">Wanneer het pad niet wordt opgegeven, wordt alleen Hallo URL die is opgegeven in de servicedefinitie Hallo gekoppeld gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-2408">When path is not specified, only hello URL specified in hello linked service definition is used.</span></span> <br><br> <span data-ttu-id="34b16-2409">dynamische tooconstruct-URL, kunt u [Data Factory-functies en systeemvariabelen](data-factory-functions-variables.md), bijvoorbeeld: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`.</span><span class="sxs-lookup"><span data-stu-id="34b16-2409">tooconstruct dynamic URL, you can use [Data Factory functions and system variables](data-factory-functions-variables.md), Example: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`.</span></span> | <span data-ttu-id="34b16-2410">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2410">No</span></span> |
| <span data-ttu-id="34b16-2411">requestMethod</span><span class="sxs-lookup"><span data-stu-id="34b16-2411">requestMethod</span></span> | <span data-ttu-id="34b16-2412">HTTP-methode.</span><span class="sxs-lookup"><span data-stu-id="34b16-2412">Http method.</span></span> <span data-ttu-id="34b16-2413">Toegestane waarden zijn **ophalen** of **POST**.</span><span class="sxs-lookup"><span data-stu-id="34b16-2413">Allowed values are **GET** or **POST**.</span></span> | <span data-ttu-id="34b16-2414">Nee.</span><span class="sxs-lookup"><span data-stu-id="34b16-2414">No.</span></span> <span data-ttu-id="34b16-2415">Standaard is `GET`.</span><span class="sxs-lookup"><span data-stu-id="34b16-2415">Default is `GET`.</span></span> |
| <span data-ttu-id="34b16-2416">additionalHeaders</span><span class="sxs-lookup"><span data-stu-id="34b16-2416">additionalHeaders</span></span> | <span data-ttu-id="34b16-2417">Aanvullende HTTP-aanvraagheaders.</span><span class="sxs-lookup"><span data-stu-id="34b16-2417">Additional HTTP request headers.</span></span> | <span data-ttu-id="34b16-2418">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2418">No</span></span> |
| <span data-ttu-id="34b16-2419">requestBody</span><span class="sxs-lookup"><span data-stu-id="34b16-2419">requestBody</span></span> | <span data-ttu-id="34b16-2420">Instantie voor HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="34b16-2420">Body for HTTP request.</span></span> | <span data-ttu-id="34b16-2421">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2421">No</span></span> |
| <span data-ttu-id="34b16-2422">Indeling</span><span class="sxs-lookup"><span data-stu-id="34b16-2422">format</span></span> | <span data-ttu-id="34b16-2423">Als u wilt dat toosimply **Hallo-gegevens ophalen van HTTP-eindpunt als-is** overslaan zonder deze parseren, deze instellingen.</span><span class="sxs-lookup"><span data-stu-id="34b16-2423">If you want toosimply **retrieve hello data from HTTP endpoint as-is** without parsing it, skip this format settings.</span></span> <br><br> <span data-ttu-id="34b16-2424">Als u tooparse Hallo HTTP-antwoord inhoud tijdens het kopiëren wilt, Hallo na indelingstypen worden ondersteund: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="34b16-2424">If you want tooparse hello HTTP response content during copy, hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="34b16-2425">Zie voor meer informatie [tekstindeling](data-factory-supported-file-and-compression-formats.md#text-format), [Json-indeling](data-factory-supported-file-and-compression-formats.md#json-format), [Avro-indeling](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc indeling](data-factory-supported-file-and-compression-formats.md#orc-format), en [parketvloeren indeling](data-factory-supported-file-and-compression-formats.md#parquet-format) secties.</span><span class="sxs-lookup"><span data-stu-id="34b16-2425">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> |<span data-ttu-id="34b16-2426">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2426">No</span></span> |
| <span data-ttu-id="34b16-2427">Compressie</span><span class="sxs-lookup"><span data-stu-id="34b16-2427">compression</span></span> | <span data-ttu-id="34b16-2428">Hallo-type en compressieniveau voor Hallo gegevens opgeven.</span><span class="sxs-lookup"><span data-stu-id="34b16-2428">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="34b16-2429">Ondersteunde typen zijn: **GZip**, **Deflate**, **BZip2**, en **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="34b16-2429">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="34b16-2430">Ondersteunde niveaus: **optimale** en **snelst**.</span><span class="sxs-lookup"><span data-stu-id="34b16-2430">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="34b16-2431">Zie voor meer informatie [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="34b16-2431">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="34b16-2432">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2432">No</span></span> |

#### <a name="example-using-hello-get-default-method"></a><span data-ttu-id="34b16-2433">Voorbeeld: via Hallo GET (standaard)-methode</span><span class="sxs-lookup"><span data-stu-id="34b16-2433">Example: using hello GET (default) method</span></span>

```json
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "XXX/test.xml",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

#### <a name="example-using-hello-post-method"></a><span data-ttu-id="34b16-2434">Voorbeeld: via Hallo POST-methode</span><span class="sxs-lookup"><span data-stu-id="34b16-2434">Example: using hello POST method</span></span>

```json
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "/XXX/test.xml",
            "requestMethod": "Post",
            "requestBody": "body for POST HTTP request"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```
<span data-ttu-id="34b16-2435">Zie voor meer informatie [HTTP connector](data-factory-http-connector.md#dataset-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-2435">For more information, see [HTTP connector](data-factory-http-connector.md#dataset-properties) article.</span></span>

### <a name="http-source-in-copy-activity"></a><span data-ttu-id="34b16-2436">HTTP-bron in de kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="34b16-2436">HTTP Source in Copy Activity</span></span>
<span data-ttu-id="34b16-2437">Als u gegevens van een HTTP-bron kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**HttpSource**, en opgeven na eigenschappen in Hallo **bron** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-2437">If you are copying data from a HTTP source, set hello **source type** of hello copy activity too**HttpSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="34b16-2438">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-2438">Property</span></span> | <span data-ttu-id="34b16-2439">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-2439">Description</span></span> | <span data-ttu-id="34b16-2440">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-2440">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="34b16-2441">httpRequestTimeout</span><span class="sxs-lookup"><span data-stu-id="34b16-2441">httpRequestTimeout</span></span> | <span data-ttu-id="34b16-2442">Hallo-out (TimeSpan) voor Hallo HTTP-aanvraag tooget een antwoord.</span><span class="sxs-lookup"><span data-stu-id="34b16-2442">hello timeout (TimeSpan) for hello HTTP request tooget a response.</span></span> <span data-ttu-id="34b16-2443">Hallo time-out tooget een antwoord niet Hallo time-out tooread antwoordgegevens is.</span><span class="sxs-lookup"><span data-stu-id="34b16-2443">It is hello timeout tooget a response, not hello timeout tooread response data.</span></span> | <span data-ttu-id="34b16-2444">Nee.</span><span class="sxs-lookup"><span data-stu-id="34b16-2444">No.</span></span> <span data-ttu-id="34b16-2445">Standaardwaarde: 00:01:40</span><span class="sxs-lookup"><span data-stu-id="34b16-2445">Default value: 00:01:40</span></span> |


#### <a name="example"></a><span data-ttu-id="34b16-2446">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-2446">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "HttpSourceToAzureBlob",
            "description": "Copy from an HTTP source tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "HttpSourceDataInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "HttpSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="34b16-2447">Zie voor meer informatie [HTTP connector](data-factory-http-connector.md#copy-activity-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-2447">For more information, see [HTTP connector](data-factory-http-connector.md#copy-activity-properties) article.</span></span>

## <a name="odata"></a><span data-ttu-id="34b16-2448">OData</span><span class="sxs-lookup"><span data-stu-id="34b16-2448">OData</span></span>

### <a name="linked-service"></a><span data-ttu-id="34b16-2449">Gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="34b16-2449">Linked service</span></span>
<span data-ttu-id="34b16-2450">een OData-toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**OData**, en opgeven na eigenschappen in Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-2450">toodefine an OData linked service, set hello **type** of hello linked service too**OData**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="34b16-2451">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-2451">Property</span></span> | <span data-ttu-id="34b16-2452">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-2452">Description</span></span> | <span data-ttu-id="34b16-2453">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-2453">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-2454">URL</span><span class="sxs-lookup"><span data-stu-id="34b16-2454">url</span></span> |<span data-ttu-id="34b16-2455">URL van Hallo OData-service.</span><span class="sxs-lookup"><span data-stu-id="34b16-2455">Url of hello OData service.</span></span> |<span data-ttu-id="34b16-2456">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2456">Yes</span></span> |
| <span data-ttu-id="34b16-2457">authenticationType</span><span class="sxs-lookup"><span data-stu-id="34b16-2457">authenticationType</span></span> |<span data-ttu-id="34b16-2458">Type verificatie gebruikt tooconnect toohello OData-bron.</span><span class="sxs-lookup"><span data-stu-id="34b16-2458">Type of authentication used tooconnect toohello OData source.</span></span> <br/><br/> <span data-ttu-id="34b16-2459">Mogelijke waarden zijn voor OData-cloud, anoniem, basis en OAuth (Opmerking momenteel alleen ondersteuning voor Azure Data Factory Azure Active Directory op basis van OAuth).</span><span class="sxs-lookup"><span data-stu-id="34b16-2459">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span></span> <br/><br/> <span data-ttu-id="34b16-2460">Mogelijke waarden zijn voor lokale OData, anoniem, basis en Windows.</span><span class="sxs-lookup"><span data-stu-id="34b16-2460">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="34b16-2461">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2461">Yes</span></span> |
| <span data-ttu-id="34b16-2462">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="34b16-2462">username</span></span> |<span data-ttu-id="34b16-2463">Geef de gebruikersnaam als u basisverificatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-2463">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="34b16-2464">Ja (alleen als u basisverificatie gebruikt)</span><span class="sxs-lookup"><span data-stu-id="34b16-2464">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="34b16-2465">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="34b16-2465">password</span></span> |<span data-ttu-id="34b16-2466">Wachtwoord voor gebruikersaccount Hallo die u hebt opgegeven voor Hallo gebruikersnaam opgeven.</span><span class="sxs-lookup"><span data-stu-id="34b16-2466">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="34b16-2467">Ja (alleen als u basisverificatie gebruikt)</span><span class="sxs-lookup"><span data-stu-id="34b16-2467">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="34b16-2468">authorizedCredential</span><span class="sxs-lookup"><span data-stu-id="34b16-2468">authorizedCredential</span></span> |<span data-ttu-id="34b16-2469">Als u van OAuth gebruikmaakt, klikt u op **autoriseren** knop op Hallo Data Factory-Wizard kopiëren of Editor en voer uw referenties wordt Hallo-waarde van deze eigenschap automatisch wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="34b16-2469">If you are using OAuth, click **Authorize** button in hello Data Factory Copy Wizard or Editor and enter your credential, then hello value of this property will be auto-generated.</span></span> |<span data-ttu-id="34b16-2470">Ja (alleen als u OAuth-verificatie gebruikt)</span><span class="sxs-lookup"><span data-stu-id="34b16-2470">Yes (only if you are using OAuth authentication)</span></span> |
| <span data-ttu-id="34b16-2471">gatewayName</span><span class="sxs-lookup"><span data-stu-id="34b16-2471">gatewayName</span></span> |<span data-ttu-id="34b16-2472">Naam van Hallo-gateway die Hallo Data Factory-service moet tooconnect toohello on-premises OData-service gebruiken.</span><span class="sxs-lookup"><span data-stu-id="34b16-2472">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises OData service.</span></span> <span data-ttu-id="34b16-2473">Geef alleen als u gegevens uit een on-premises OData-bron kopiëren wilt.</span><span class="sxs-lookup"><span data-stu-id="34b16-2473">Specify only if you are copying data from on-prem OData source.</span></span> |<span data-ttu-id="34b16-2474">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2474">No</span></span> |

#### <a name="example---using-basic-authentication"></a><span data-ttu-id="34b16-2475">Voorbeeld: met behulp van basisverificatie</span><span class="sxs-lookup"><span data-stu-id="34b16-2475">Example - Using Basic authentication</span></span>
```json
{
    "name": "inputLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Basic",
            "username": "username",
            "password": "password"
        }
    }
}
```

#### <a name="example---using-anonymous-authentication"></a><span data-ttu-id="34b16-2476">Voorbeeld: anonieme verificatie</span><span class="sxs-lookup"><span data-stu-id="34b16-2476">Example - Using Anonymous authentication</span></span>

```json
{
    "name": "ODataLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
        }
    }
}
```

#### <a name="example---using-windows-authentication-accessing-on-premises-odata-source"></a><span data-ttu-id="34b16-2477">Voorbeeld: met behulp van Windows-verificatie toegang tot lokale OData-bron</span><span class="sxs-lookup"><span data-stu-id="34b16-2477">Example - Using Windows authentication accessing on-premises OData source</span></span>

```json
{
    "name": "inputLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "<endpoint of on-premises OData source, for example, Dynamics CRM>",
            "authenticationType": "Windows",
            "username": "domain\\user",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example---using-oauth-authentication-accessing-cloud-odata-source"></a><span data-ttu-id="34b16-2478">Voorbeeld: met behulp van OAuth-verificatie toegang tot de cloud OData-bron</span><span class="sxs-lookup"><span data-stu-id="34b16-2478">Example - Using OAuth authentication accessing cloud OData source</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of cloud OData source, for example, https://<tenant>.crm.dynamics.com/XRMServices/2011/OrganizationData.svc>",
            "authenticationType": "OAuth",
            "authorizedCredential": "<auto generated by clicking hello Authorize button on UI>"
        }
    }
}
```

<span data-ttu-id="34b16-2479">Zie voor meer informatie [OData-connector](data-factory-odata-connector.md#linked-service-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-2479">For more information, see [OData connector](data-factory-odata-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="34b16-2480">Gegevensset</span><span class="sxs-lookup"><span data-stu-id="34b16-2480">Dataset</span></span>
<span data-ttu-id="34b16-2481">toodefine een gegevensset OData set Hallo **type** van Hallo gegevensset te**ODataResource**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-2481">toodefine an OData dataset, set hello **type** of hello dataset too**ODataResource**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="34b16-2482">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-2482">Property</span></span> | <span data-ttu-id="34b16-2483">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-2483">Description</span></span> | <span data-ttu-id="34b16-2484">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-2484">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-2485">Pad</span><span class="sxs-lookup"><span data-stu-id="34b16-2485">path</span></span> |<span data-ttu-id="34b16-2486">Pad toohello OData-bron</span><span class="sxs-lookup"><span data-stu-id="34b16-2486">Path toohello OData resource</span></span> |<span data-ttu-id="34b16-2487">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2487">No</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-2488">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-2488">Example</span></span>

```json
{
    "name": "ODataDataset",
    "properties": {
        "type": "ODataResource",
        "typeProperties": {
            "path": "Products"
        },
        "linkedServiceName": "ODataLinkedService",
        "structure": [],
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3
        }
    }
}
```

<span data-ttu-id="34b16-2489">Zie voor meer informatie [OData-connector](data-factory-odata-connector.md#dataset-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-2489">For more information, see [OData connector](data-factory-odata-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="34b16-2490">Relationele gegevensbron in de kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="34b16-2490">Relational Source in Copy Activity</span></span>
<span data-ttu-id="34b16-2491">Als u gegevens uit een OData-bron kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**RelationalSource**, en opgeven na eigenschappen in Hallo **bron** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-2491">If you are copying data from an OData source, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="34b16-2492">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-2492">Property</span></span> | <span data-ttu-id="34b16-2493">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-2493">Description</span></span> | <span data-ttu-id="34b16-2494">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-2494">Example</span></span> | <span data-ttu-id="34b16-2495">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-2495">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-2496">query</span><span class="sxs-lookup"><span data-stu-id="34b16-2496">query</span></span> |<span data-ttu-id="34b16-2497">Hallo aangepaste query tooread gegevens worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-2497">Use hello custom query tooread data.</span></span> |<span data-ttu-id="34b16-2498">'? $select = naam, beschrijving & $top = 5 '</span><span class="sxs-lookup"><span data-stu-id="34b16-2498">"?$select=Name, Description&$top=5"</span></span> |<span data-ttu-id="34b16-2499">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2499">No</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-2500">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-2500">Example</span></span>

```json
{
    "name": "CopyODataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "?$select=Name, Description&$top=5"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "ODataDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobODataDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "ODataToBlob"
        }],
        "start": "2017-02-01T18:00:00",
        "end": "2017-02-03T19:00:00"
    }
}
```

<span data-ttu-id="34b16-2501">Zie voor meer informatie [OData-connector](data-factory-odata-connector.md#copy-activity-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-2501">For more information, see [OData connector](data-factory-odata-connector.md#copy-activity-properties) article.</span></span>


## <a name="odbc"></a><span data-ttu-id="34b16-2502">ODBC</span><span class="sxs-lookup"><span data-stu-id="34b16-2502">ODBC</span></span>


### <a name="linked-service"></a><span data-ttu-id="34b16-2503">Gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="34b16-2503">Linked service</span></span>
<span data-ttu-id="34b16-2504">toodefine ODBC gekoppelde service, set Hallo **type** Hallo gekoppelde service te**OnPremisesOdbc**, en opgeven na eigenschappen in Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-2504">toodefine an ODBC linked service, set hello **type** of hello linked service too**OnPremisesOdbc**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="34b16-2505">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-2505">Property</span></span> | <span data-ttu-id="34b16-2506">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-2506">Description</span></span> | <span data-ttu-id="34b16-2507">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-2507">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-2508">connectionString</span><span class="sxs-lookup"><span data-stu-id="34b16-2508">connectionString</span></span> |<span data-ttu-id="34b16-2509">Hallo niet access credential gedeelte van het Hallo-verbindingsreeks en een optionele versleuteld referentie.</span><span class="sxs-lookup"><span data-stu-id="34b16-2509">hello non-access credential portion of hello connection string and an optional encrypted credential.</span></span> <span data-ttu-id="34b16-2510">Zie de voorbeelden in Hallo uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="34b16-2510">See examples in hello following sections.</span></span> |<span data-ttu-id="34b16-2511">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2511">Yes</span></span> |
| <span data-ttu-id="34b16-2512">referentie</span><span class="sxs-lookup"><span data-stu-id="34b16-2512">credential</span></span> |<span data-ttu-id="34b16-2513">Hallo toegang referentie gedeelte van het Hallo-verbindingsreeks die is opgegeven in de indeling van de eigenschapswaarde specifieke stuurprogramma's.</span><span class="sxs-lookup"><span data-stu-id="34b16-2513">hello access credential portion of hello connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="34b16-2514">Voorbeeld: "Uid =<user ID>; Pwd =<password>; RefreshToken =<secret refresh token>; '.</span><span class="sxs-lookup"><span data-stu-id="34b16-2514">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span></span> |<span data-ttu-id="34b16-2515">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2515">No</span></span> |
| <span data-ttu-id="34b16-2516">authenticationType</span><span class="sxs-lookup"><span data-stu-id="34b16-2516">authenticationType</span></span> |<span data-ttu-id="34b16-2517">Type verificatie gebruikt tooconnect toohello ODBC-gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="34b16-2517">Type of authentication used tooconnect toohello ODBC data store.</span></span> <span data-ttu-id="34b16-2518">Mogelijke waarden zijn: anonieme en Basic.</span><span class="sxs-lookup"><span data-stu-id="34b16-2518">Possible values are: Anonymous and Basic.</span></span> |<span data-ttu-id="34b16-2519">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2519">Yes</span></span> |
| <span data-ttu-id="34b16-2520">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="34b16-2520">username</span></span> |<span data-ttu-id="34b16-2521">Geef de gebruikersnaam als u basisverificatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-2521">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="34b16-2522">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2522">No</span></span> |
| <span data-ttu-id="34b16-2523">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="34b16-2523">password</span></span> |<span data-ttu-id="34b16-2524">Wachtwoord voor gebruikersaccount Hallo die u hebt opgegeven voor Hallo gebruikersnaam opgeven.</span><span class="sxs-lookup"><span data-stu-id="34b16-2524">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="34b16-2525">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2525">No</span></span> |
| <span data-ttu-id="34b16-2526">gatewayName</span><span class="sxs-lookup"><span data-stu-id="34b16-2526">gatewayName</span></span> |<span data-ttu-id="34b16-2527">Naam van Hallo-gateway die Hallo Data Factory-service moet tooconnect toohello ODBC-gegevensarchief gebruiken.</span><span class="sxs-lookup"><span data-stu-id="34b16-2527">Name of hello gateway that hello Data Factory service should use tooconnect toohello ODBC data store.</span></span> |<span data-ttu-id="34b16-2528">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2528">Yes</span></span> |

#### <a name="example---using-basic-authentication"></a><span data-ttu-id="34b16-2529">Voorbeeld: met behulp van basisverificatie</span><span class="sxs-lookup"><span data-stu-id="34b16-2529">Example - Using Basic authentication</span></span>

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```
#### <a name="example---using-basic-authentication-with-encrypted-credentials"></a><span data-ttu-id="34b16-2530">Voorbeeld: met behulp van basisverificatie met versleutelde referenties</span><span class="sxs-lookup"><span data-stu-id="34b16-2530">Example - Using Basic authentication with encrypted credentials</span></span>
<span data-ttu-id="34b16-2531">U kunt versleutelen Hallo-referenties met een Hallo [nieuw AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) cmdlet (versie 1.0 van Azure PowerShell) of [nieuw AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0,9 of een eerdere versie van Hallo Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="34b16-2531">You can encrypt hello credentials using hello [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of hello Azure PowerShell).</span></span>  

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="34b16-2532">Voorbeeld: Anonieme verificatie gebruikt</span><span class="sxs-lookup"><span data-stu-id="34b16-2532">Example: Using Anonymous authentication</span></span>

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="34b16-2533">Zie voor meer informatie [ODBC connector](data-factory-odbc-connector.md#linked-service-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-2533">For more information, see [ODBC connector](data-factory-odbc-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="34b16-2534">Gegevensset</span><span class="sxs-lookup"><span data-stu-id="34b16-2534">Dataset</span></span>
<span data-ttu-id="34b16-2535">toodefine een gegevensset ODBC set Hallo **type** van Hallo gegevensset te**RelationalTable**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-2535">toodefine an ODBC dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="34b16-2536">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-2536">Property</span></span> | <span data-ttu-id="34b16-2537">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-2537">Description</span></span> | <span data-ttu-id="34b16-2538">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-2538">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-2539">tableName</span><span class="sxs-lookup"><span data-stu-id="34b16-2539">tableName</span></span> |<span data-ttu-id="34b16-2540">Naam van de tabel Hallo in Hallo ODBC-gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="34b16-2540">Name of hello table in hello ODBC data store.</span></span> |<span data-ttu-id="34b16-2541">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2541">Yes</span></span> |


#### <a name="example"></a><span data-ttu-id="34b16-2542">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-2542">Example</span></span>

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "ODBCLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="34b16-2543">Zie voor meer informatie [ODBC connector](data-factory-odbc-connector.md#dataset-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-2543">For more information, see [ODBC connector](data-factory-odbc-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="34b16-2544">Relationele gegevensbron in de kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="34b16-2544">Relational Source in Copy Activity</span></span>
<span data-ttu-id="34b16-2545">Als u gegevens uit een ODBC data store kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**RelationalSource**, en opgeven na eigenschappen in Hallo **bron** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-2545">If you are copying data from an ODBC data store, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="34b16-2546">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-2546">Property</span></span> | <span data-ttu-id="34b16-2547">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-2547">Description</span></span> | <span data-ttu-id="34b16-2548">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="34b16-2548">Allowed values</span></span> | <span data-ttu-id="34b16-2549">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-2549">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-2550">query</span><span class="sxs-lookup"><span data-stu-id="34b16-2550">query</span></span> |<span data-ttu-id="34b16-2551">Hallo aangepaste query tooread gegevens worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-2551">Use hello custom query tooread data.</span></span> |<span data-ttu-id="34b16-2552">SQL-query-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="34b16-2552">SQL query string.</span></span> <span data-ttu-id="34b16-2553">Bijvoorbeeld: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="34b16-2553">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="34b16-2554">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2554">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-2555">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-2555">Example</span></span>

```json
{
    "name": "CopyODBCToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "OdbcDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobOdbcDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "OdbcToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
``` 

<span data-ttu-id="34b16-2556">Zie voor meer informatie [ODBC connector](data-factory-odbc-connector.md#copy-activity-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-2556">For more information, see [ODBC connector](data-factory-odbc-connector.md#copy-activity-properties) article.</span></span>

## <a name="salesforce"></a><span data-ttu-id="34b16-2557">SalesForce</span><span class="sxs-lookup"><span data-stu-id="34b16-2557">Salesforce</span></span>


### <a name="linked-service"></a><span data-ttu-id="34b16-2558">Gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="34b16-2558">Linked service</span></span>
<span data-ttu-id="34b16-2559">een Salesforce toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**Salesforce**, en opgeven na eigenschappen in Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-2559">toodefine a Salesforce linked service, set hello **type** of hello linked service too**Salesforce**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="34b16-2560">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-2560">Property</span></span> | <span data-ttu-id="34b16-2561">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-2561">Description</span></span> | <span data-ttu-id="34b16-2562">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-2562">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-2563">environmentUrl</span><span class="sxs-lookup"><span data-stu-id="34b16-2563">environmentUrl</span></span> | <span data-ttu-id="34b16-2564">Hallo-URL van de Salesforce-exemplaar opgeven.</span><span class="sxs-lookup"><span data-stu-id="34b16-2564">Specify hello URL of Salesforce instance.</span></span> <br><br> <span data-ttu-id="34b16-2565">-Standaard is 'https://login.salesforce.com'.</span><span class="sxs-lookup"><span data-stu-id="34b16-2565">- Default is "https://login.salesforce.com".</span></span> <br> <span data-ttu-id="34b16-2566">-toocopy gegevens van de sandbox, 'https://test.salesforce.com' opgeven.</span><span class="sxs-lookup"><span data-stu-id="34b16-2566">- toocopy data from sandbox, specify "https://test.salesforce.com".</span></span> <br> <span data-ttu-id="34b16-2567">-toocopy gegevens van aangepast domein opgeven, bijvoorbeeld 'https://[domain].my.salesforce.com'.</span><span class="sxs-lookup"><span data-stu-id="34b16-2567">- toocopy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span></span> |<span data-ttu-id="34b16-2568">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2568">No</span></span> |
| <span data-ttu-id="34b16-2569">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="34b16-2569">username</span></span> |<span data-ttu-id="34b16-2570">Geef een gebruikersnaam voor Hallo-gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="34b16-2570">Specify a user name for hello user account.</span></span> |<span data-ttu-id="34b16-2571">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2571">Yes</span></span> |
| <span data-ttu-id="34b16-2572">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="34b16-2572">password</span></span> |<span data-ttu-id="34b16-2573">Geef een wachtwoord voor gebruikersaccount Hallo.</span><span class="sxs-lookup"><span data-stu-id="34b16-2573">Specify a password for hello user account.</span></span> |<span data-ttu-id="34b16-2574">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2574">Yes</span></span> |
| <span data-ttu-id="34b16-2575">securityToken</span><span class="sxs-lookup"><span data-stu-id="34b16-2575">securityToken</span></span> |<span data-ttu-id="34b16-2576">Geef een beveiligingstoken voor Hallo-gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="34b16-2576">Specify a security token for hello user account.</span></span> <span data-ttu-id="34b16-2577">Zie [security token ophalen](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) voor instructies over het tooreset of ophalen van een beveiligingstoken.</span><span class="sxs-lookup"><span data-stu-id="34b16-2577">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how tooreset/get a security token.</span></span> <span data-ttu-id="34b16-2578">toolearn over beveiligingstokens in het algemeen Zie [beveiligings- en Hallo API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span><span class="sxs-lookup"><span data-stu-id="34b16-2578">toolearn about security tokens in general, see [Security and hello API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span></span> |<span data-ttu-id="34b16-2579">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2579">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-2580">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-2580">Example</span></span>

```json
{
    "name": "SalesforceLinkedService",
    "properties": {
        "type": "Salesforce",
        "typeProperties": {
            "username": "<user name>",
            "password": "<password>",
            "securityToken": "<security token>"
        }
    }
}
```

<span data-ttu-id="34b16-2581">Zie voor meer informatie [Salesforce-connector](data-factory-salesforce-connector.md#linked-service-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-2581">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="34b16-2582">Gegevensset</span><span class="sxs-lookup"><span data-stu-id="34b16-2582">Dataset</span></span>
<span data-ttu-id="34b16-2583">toodefine een Salesforce-gegevensset set Hallo **type** van Hallo gegevensset te**RelationalTable**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-2583">toodefine a Salesforce dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="34b16-2584">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-2584">Property</span></span> | <span data-ttu-id="34b16-2585">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-2585">Description</span></span> | <span data-ttu-id="34b16-2586">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-2586">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-2587">tableName</span><span class="sxs-lookup"><span data-stu-id="34b16-2587">tableName</span></span> |<span data-ttu-id="34b16-2588">Naam van de tabel Hallo in Salesforce.</span><span class="sxs-lookup"><span data-stu-id="34b16-2588">Name of hello table in Salesforce.</span></span> |<span data-ttu-id="34b16-2589">Nee (als een **query** van **RelationalSource** is opgegeven)</span><span class="sxs-lookup"><span data-stu-id="34b16-2589">No (if a **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-2590">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-2590">Example</span></span>

```json
{
    "name": "SalesforceInput",
    "properties": {
        "linkedServiceName": "SalesforceLinkedService",
        "type": "RelationalTable",
        "typeProperties": {
            "tableName": "AllDataType__c"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="34b16-2591">Zie voor meer informatie [Salesforce-connector](data-factory-salesforce-connector.md#dataset-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-2591">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="34b16-2592">Relationele gegevensbron in de kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="34b16-2592">Relational Source in Copy Activity</span></span>
<span data-ttu-id="34b16-2593">Als u gegevens uit Salesforce kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**RelationalSource**, en opgeven na eigenschappen in Hallo **bron** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-2593">If you are copying data from Salesforce, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="34b16-2594">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-2594">Property</span></span> | <span data-ttu-id="34b16-2595">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-2595">Description</span></span> | <span data-ttu-id="34b16-2596">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="34b16-2596">Allowed values</span></span> | <span data-ttu-id="34b16-2597">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-2597">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="34b16-2598">query</span><span class="sxs-lookup"><span data-stu-id="34b16-2598">query</span></span> |<span data-ttu-id="34b16-2599">Hallo aangepaste query tooread gegevens worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-2599">Use hello custom query tooread data.</span></span> |<span data-ttu-id="34b16-2600">Een SQL-92-query of [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span><span class="sxs-lookup"><span data-stu-id="34b16-2600">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span></span> <span data-ttu-id="34b16-2601">Bijvoorbeeld `select * from MyTable__c`.</span><span class="sxs-lookup"><span data-stu-id="34b16-2601">For example:  `select * from MyTable__c`.</span></span> |<span data-ttu-id="34b16-2602">Nee (als hello **tableName** Hallo **gegevensset** is opgegeven)</span><span class="sxs-lookup"><span data-stu-id="34b16-2602">No (if hello **tableName** of hello **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-2603">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-2603">Example</span></span>  



```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "SalesforceInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "SELECT Id, Col_AutoNumber__c, Col_Checkbox__c, Col_Currency__c, Col_Date__c, Col_DateTime__c, Col_Email__c, Col_Number__c, Col_Percent__c, Col_Phone__c, Col_Picklist__c, Col_Picklist_MultiSelect__c, Col_Text__c, Col_Text_Area__c, Col_Text_AreaLong__c, Col_Text_AreaRich__c, Col_URL__c, Col_Text_Encrypt__c, Col_Lookup__c FROM AllDataType__c"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="34b16-2604">Hallo '__c' onderdeel Hallo API-naam is vereist voor elk object dat aangepast.</span><span class="sxs-lookup"><span data-stu-id="34b16-2604">hello "__c" part of hello API Name is needed for any custom object.</span></span>

<span data-ttu-id="34b16-2605">Zie voor meer informatie [Salesforce-connector](data-factory-salesforce-connector.md#copy-activity-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-2605">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#copy-activity-properties) article.</span></span> 

## <a name="web-data"></a><span data-ttu-id="34b16-2606">Web-gegevens</span><span class="sxs-lookup"><span data-stu-id="34b16-2606">Web Data</span></span> 

### <a name="linked-service"></a><span data-ttu-id="34b16-2607">Gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="34b16-2607">Linked service</span></span>
<span data-ttu-id="34b16-2608">een Web toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**Web**, en opgeven na eigenschappen in Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-2608">toodefine a Web linked service, set hello **type** of hello linked service too**Web**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="34b16-2609">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-2609">Property</span></span> | <span data-ttu-id="34b16-2610">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-2610">Description</span></span> | <span data-ttu-id="34b16-2611">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-2611">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-2612">URL</span><span class="sxs-lookup"><span data-stu-id="34b16-2612">Url</span></span> |<span data-ttu-id="34b16-2613">URL toohello webbron</span><span class="sxs-lookup"><span data-stu-id="34b16-2613">URL toohello Web source</span></span> |<span data-ttu-id="34b16-2614">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2614">Yes</span></span> |
| <span data-ttu-id="34b16-2615">authenticationType</span><span class="sxs-lookup"><span data-stu-id="34b16-2615">authenticationType</span></span> |<span data-ttu-id="34b16-2616">Anonieme.</span><span class="sxs-lookup"><span data-stu-id="34b16-2616">Anonymous.</span></span> |<span data-ttu-id="34b16-2617">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2617">Yes</span></span> |
 

#### <a name="example"></a><span data-ttu-id="34b16-2618">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-2618">Example</span></span>


```json
{
    "name": "web",
    "properties": {
        "type": "Web",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "url": "https://en.wikipedia.org/wiki/"
        }
    }
}
```

<span data-ttu-id="34b16-2619">Zie voor meer informatie [Web tabel connector](data-factory-web-table-connector.md#linked-service-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-2619">For more information, see [Web Table connector](data-factory-web-table-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="34b16-2620">Gegevensset</span><span class="sxs-lookup"><span data-stu-id="34b16-2620">Dataset</span></span>
<span data-ttu-id="34b16-2621">toodefine een gegevensset Web set Hallo **type** van Hallo gegevensset te**WebTable**, en geef de volgende eigenschappen in Hallo Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-2621">toodefine a Web dataset, set hello **type** of hello dataset too**WebTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="34b16-2622">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-2622">Property</span></span> | <span data-ttu-id="34b16-2623">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-2623">Description</span></span> | <span data-ttu-id="34b16-2624">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-2624">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="34b16-2625">type</span><span class="sxs-lookup"><span data-stu-id="34b16-2625">type</span></span> |<span data-ttu-id="34b16-2626">Type Hallo gegevensset.</span><span class="sxs-lookup"><span data-stu-id="34b16-2626">type of hello dataset.</span></span> <span data-ttu-id="34b16-2627">te moet worden ingesteld**WebTable**</span><span class="sxs-lookup"><span data-stu-id="34b16-2627">must be set too**WebTable**</span></span> |<span data-ttu-id="34b16-2628">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2628">Yes</span></span> |
| <span data-ttu-id="34b16-2629">Pad</span><span class="sxs-lookup"><span data-stu-id="34b16-2629">path</span></span> |<span data-ttu-id="34b16-2630">Een relatieve URL toohello-bron die Hallo tabel bevat.</span><span class="sxs-lookup"><span data-stu-id="34b16-2630">A relative URL toohello resource that contains hello table.</span></span> |<span data-ttu-id="34b16-2631">Nee.</span><span class="sxs-lookup"><span data-stu-id="34b16-2631">No.</span></span> <span data-ttu-id="34b16-2632">Wanneer het pad niet wordt opgegeven, wordt alleen Hallo URL die is opgegeven in de servicedefinitie Hallo gekoppeld gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-2632">When path is not specified, only hello URL specified in hello linked service definition is used.</span></span> |
| <span data-ttu-id="34b16-2633">Index</span><span class="sxs-lookup"><span data-stu-id="34b16-2633">index</span></span> |<span data-ttu-id="34b16-2634">Hallo index van de tabel Hallo in Hallo resource.</span><span class="sxs-lookup"><span data-stu-id="34b16-2634">hello index of hello table in hello resource.</span></span> <span data-ttu-id="34b16-2635">Zie [Get-index van een tabel in een HTML-pagina](#get-index-of-a-table-in-an-html-page) sectie voor stappen toogetting index van een tabel in een HTML-pagina.</span><span class="sxs-lookup"><span data-stu-id="34b16-2635">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps toogetting index of a table in an HTML page.</span></span> |<span data-ttu-id="34b16-2636">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2636">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="34b16-2637">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-2637">Example</span></span>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="34b16-2638">Zie voor meer informatie [Web tabel connector](data-factory-web-table-connector.md#dataset-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-2638">For more information, see [Web Table connector](data-factory-web-table-connector.md#dataset-properties) article.</span></span> 

### <a name="web-source-in-copy-activity"></a><span data-ttu-id="34b16-2639">Webbron in kopieerbewerking</span><span class="sxs-lookup"><span data-stu-id="34b16-2639">Web Source in Copy Activity</span></span>
<span data-ttu-id="34b16-2640">Als u gegevens uit een tabel web kopiëren wilt, stelt u Hallo **gegevensbrontype** Hallo kopieeractiviteit te**WebSource**.</span><span class="sxs-lookup"><span data-stu-id="34b16-2640">If you are copying data from a web table, set hello **source type** of hello copy activity too**WebSource**.</span></span> <span data-ttu-id="34b16-2641">Op dit moment wanneer Hallo-bron in de kopieerbewerking is van het type **WebSource**, zonder aanvullende eigenschappen worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="34b16-2641">Currently, when hello source in copy activity is of type **WebSource**, no additional properties are supported.</span></span>

#### <a name="example"></a><span data-ttu-id="34b16-2642">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-2642">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "WebTableToAzureBlob",
            "description": "Copy from a Web table tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "WebTableInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "WebSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="34b16-2643">Zie voor meer informatie [Web tabel connector](data-factory-web-table-connector.md#copy-activity-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-2643">For more information, see [Web Table connector](data-factory-web-table-connector.md#copy-activity-properties) article.</span></span> 

## <a name="compute-environments"></a><span data-ttu-id="34b16-2644">COMPUTE-OMGEVINGEN</span><span class="sxs-lookup"><span data-stu-id="34b16-2644">COMPUTE ENVIRONMENTS</span></span>
<span data-ttu-id="34b16-2645">Hallo bevat volgende tabel berekeningsomgevingen hello wordt ondersteund door de Data Factory en Hallo transformatie-activiteiten die kunnen worden uitgevoerd op deze.</span><span class="sxs-lookup"><span data-stu-id="34b16-2645">hello following table lists hello compute environments supported by Data Factory and hello transformation activities that can run on them.</span></span> <span data-ttu-id="34b16-2646">Klik op de koppeling Hallo voor Hallo compute u bent geïnteresseerd in toosee Hallo JSON-schema voor de gekoppelde service toolink het tooa data factory.</span><span class="sxs-lookup"><span data-stu-id="34b16-2646">Click hello link for hello compute you are interested in toosee hello JSON schemas for linked service toolink it tooa data factory.</span></span> 

| <span data-ttu-id="34b16-2647">Compute-omgeving</span><span class="sxs-lookup"><span data-stu-id="34b16-2647">Compute environment</span></span> | <span data-ttu-id="34b16-2648">Activiteiten</span><span class="sxs-lookup"><span data-stu-id="34b16-2648">Activities</span></span> |
| --- | --- |
| <span data-ttu-id="34b16-2649">[HDInsight-cluster op aanvraag](#on-demand-azure-hdinsight-cluster) of [uw eigen HDInsight-cluster](#existing-azure-hdinsight-cluster)</span><span class="sxs-lookup"><span data-stu-id="34b16-2649">[On-demand HDInsight cluster](#on-demand-azure-hdinsight-cluster) or [your own HDInsight cluster](#existing-azure-hdinsight-cluster)</span></span> |<span data-ttu-id="34b16-2650">[Aangepaste activiteit .NET](#net-custom-activity), [Hive-activiteit](#hdinsight-hive-activity), [activiteit varkens] (#hdinsight-pig-activiteit, [MapReduce-activiteit](#hdinsight-mapreduce-activity), [Hadoop-streaming activiteit](#hdinsight-streaming-activityd), [Spark activiteit](#hdinsight-spark-activity)</span><span class="sxs-lookup"><span data-stu-id="34b16-2650">[.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity)</span></span> |
| [<span data-ttu-id="34b16-2651">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="34b16-2651">Azure Batch</span></span>](#azure-batch) |[<span data-ttu-id="34b16-2652">.NET aangepaste activiteit</span><span class="sxs-lookup"><span data-stu-id="34b16-2652">.NET custom activity</span></span>](#net-custom-activity) |
| [<span data-ttu-id="34b16-2653">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="34b16-2653">Azure Machine Learning</span></span>](#azure-machine-learning) | <span data-ttu-id="34b16-2654">[Machine Learning-Batchuitvoeringsactiviteit](#machine-learning-batch-execution-activity), [Machine Learning eigen Update Resourceactiviteit](#machine-learning-update-resource-activity)</span><span class="sxs-lookup"><span data-stu-id="34b16-2654">[Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity)</span></span> |
| [<span data-ttu-id="34b16-2655">Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="34b16-2655">Azure Data Lake Analytics</span></span>](#azure-data-lake-analytics) |[<span data-ttu-id="34b16-2656">Data Lake Analytics U-SQL</span><span class="sxs-lookup"><span data-stu-id="34b16-2656">Data Lake Analytics U-SQL</span></span>](#data-lake-analytics-u-sql-activity) |
| <span data-ttu-id="34b16-2657">[Azure SQL Database](#azure-sql-database-1), [Azure SQL datawarehouse](#azure-sql-data-warehouse-1), [SQL Server](#sql-server-1)</span><span class="sxs-lookup"><span data-stu-id="34b16-2657">[Azure SQL Database](#azure-sql-database-1), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-1), [SQL Server](#sql-server-1)</span></span> |[<span data-ttu-id="34b16-2658">Opgeslagen procedure</span><span class="sxs-lookup"><span data-stu-id="34b16-2658">Stored Procedure</span></span>](#stored-procedure-activity) |

## <a name="on-demand-azure-hdinsight-cluster"></a><span data-ttu-id="34b16-2659">Azure HDInsight-cluster op aanvraag</span><span class="sxs-lookup"><span data-stu-id="34b16-2659">On-demand Azure HDInsight cluster</span></span>
<span data-ttu-id="34b16-2660">Hello Azure Data Factory-service kan een Windows, Linux-gebaseerde bellen op HDInsight-cluster tooprocess gegevens automatisch worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="34b16-2660">hello Azure Data Factory service can automatically create a Windows/Linux-based on-demand HDInsight cluster tooprocess data.</span></span> <span data-ttu-id="34b16-2661">Hallo-cluster wordt gemaakt in dezelfde regio bevinden als Hallo storage-account (de eigenschap linkedServiceName in Hallo JSON) die zijn gekoppeld aan cluster Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="34b16-2661">hello cluster is created in hello same region as hello storage account (linkedServiceName property in hello JSON) associated with hello cluster.</span></span> <span data-ttu-id="34b16-2662">U kunt uitvoeren Hallo activiteiten voor gegevenstransformatie volgen op deze gekoppelde service: [aangepaste activiteit .NET](#net-custom-activity), [Hive-activiteit](#hdinsight-hive-activity), [varkens activiteit] (#hdinsight-pig-activiteit, [MapReduce-activiteit ](#hdinsight-mapreduce-activity), [Hadoop-streaming activiteit](#hdinsight-streaming-activityd), [Spark activiteit](#hdinsight-spark-activity).</span><span class="sxs-lookup"><span data-stu-id="34b16-2662">You can run hello following transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="34b16-2663">Gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="34b16-2663">Linked service</span></span> 
<span data-ttu-id="34b16-2664">Hallo volgende tabel bevat beschrijvingen van Hallo-eigenschappen die in hello Azure JSON-definitie van een gekoppelde HDInsight-service op aanvraag gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-2664">hello following table provides descriptions for hello properties used in hello Azure JSON definition of an on-demand HDInsight linked service.</span></span>

| <span data-ttu-id="34b16-2665">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-2665">Property</span></span> | <span data-ttu-id="34b16-2666">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-2666">Description</span></span> | <span data-ttu-id="34b16-2667">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-2667">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-2668">type</span><span class="sxs-lookup"><span data-stu-id="34b16-2668">type</span></span> |<span data-ttu-id="34b16-2669">de eigenschap type Hello te moet worden ingesteld**HDInsightOnDemand**.</span><span class="sxs-lookup"><span data-stu-id="34b16-2669">hello type property should be set too**HDInsightOnDemand**.</span></span> |<span data-ttu-id="34b16-2670">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2670">Yes</span></span> |
| <span data-ttu-id="34b16-2671">De clustergrootte</span><span class="sxs-lookup"><span data-stu-id="34b16-2671">clusterSize</span></span> |<span data-ttu-id="34b16-2672">Aantal knooppunten in cluster Hallo worker/gegevens.</span><span class="sxs-lookup"><span data-stu-id="34b16-2672">Number of worker/data nodes in hello cluster.</span></span> <span data-ttu-id="34b16-2673">Hallo HDInsight-cluster wordt gemaakt met 2 hoofdknooppunten samen met het aantal worker-knooppunten die u voor deze eigenschap opgeeft Hallo.</span><span class="sxs-lookup"><span data-stu-id="34b16-2673">hello HDInsight cluster is created with 2 head nodes along with hello number of worker nodes you specify for this property.</span></span> <span data-ttu-id="34b16-2674">Hallo-knooppunten zijn met een grootte van Standard_D3 met 4 kernen, zodat een cluster met 4 worker-knooppunten 24 kernen duurt (4\*4 = 16 cores voor worker-knooppunten plus 2\*4 = 8 cores voor hoofdknooppunten).</span><span class="sxs-lookup"><span data-stu-id="34b16-2674">hello nodes are of size Standard_D3 that has 4 cores, so a 4 worker node cluster takes 24 cores (4\*4 = 16 cores for worker nodes, plus 2\*4 = 8 cores for head nodes).</span></span> <span data-ttu-id="34b16-2675">Zie [maken Linux gebaseerde Hadoop-clusters in HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) voor meer informatie over Hallo Standard_D3 laag.</span><span class="sxs-lookup"><span data-stu-id="34b16-2675">See [Create Linux-based Hadoop clusters in HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) for details about hello Standard_D3 tier.</span></span> |<span data-ttu-id="34b16-2676">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2676">Yes</span></span> |
| <span data-ttu-id="34b16-2677">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="34b16-2677">timetolive</span></span> |<span data-ttu-id="34b16-2678">Hallo toegestane niet-actieve tijd voor Hallo bellen op HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="34b16-2678">hello allowed idle time for hello on-demand HDInsight cluster.</span></span> <span data-ttu-id="34b16-2679">Hiermee geeft u op hoe lang Hallo bellen op HDInsight-cluster na voltooiing van een activiteit die wordt uitgevoerd als er geen actieve taken in het cluster Hallo actief blijft.</span><span class="sxs-lookup"><span data-stu-id="34b16-2679">Specifies how long hello on-demand HDInsight cluster stays alive after completion of an activity run if there are no other active jobs in hello cluster.</span></span><br/><br/><span data-ttu-id="34b16-2680">Bijvoorbeeld, als een activiteit die wordt uitgevoerd, 6 minuten en timetolive duurt is ingesteld too5 minuten, Hallo cluster blijft actief gedurende vijf minuten na Hallo 6 minuten van de verwerking van Hallo activiteit die wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="34b16-2680">For example, if an activity run takes 6 minutes and timetolive is set too5 minutes, hello cluster stays alive for 5 minutes after hello 6 minutes of processing hello activity run.</span></span> <span data-ttu-id="34b16-2681">Als een andere activiteit die wordt uitgevoerd met Hallo 6 minuten venster wordt uitgevoerd, wordt verwerkt door Hallo hetzelfde cluster.</span><span class="sxs-lookup"><span data-stu-id="34b16-2681">If another activity run is executed with hello 6 minutes window, it is processed by hello same cluster.</span></span><br/><br/><span data-ttu-id="34b16-2682">Maken van een HDInsight-cluster op aanvraag is een dure bewerking (kan even duren), dus gebruik deze instelling als de prestaties van een gegevensfactory nodig tooimprove door een HDInsight-cluster op aanvraag opnieuw te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="34b16-2682">Creating an on-demand HDInsight cluster is an expensive operation (could take a while), so use this setting as needed tooimprove performance of a data factory by reusing an on-demand HDInsight cluster.</span></span><br/><br/><span data-ttu-id="34b16-2683">Als u timetolive waarde too0 instelt, wordt Hallo cluster verwijderd zodra Hallo activiteit worden uitgevoerd verwerkt.</span><span class="sxs-lookup"><span data-stu-id="34b16-2683">If you set timetolive value too0, hello cluster is deleted as soon as hello activity run in processed.</span></span> <span data-ttu-id="34b16-2684">Op Hallo anderzijds, als u een hoge waarde instelt Hallo cluster mogelijk blijven inactief onnodig wat resulteert in hoge kosten.</span><span class="sxs-lookup"><span data-stu-id="34b16-2684">On hello other hand, if you set a high value, hello cluster may stay idle unnecessarily resulting in high costs.</span></span> <span data-ttu-id="34b16-2685">Het is daarom belangrijk dat u Hallo geschikte waarde op basis van uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="34b16-2685">Therefore, it is important that you set hello appropriate value based on your needs.</span></span><br/><br/><span data-ttu-id="34b16-2686">Meerdere pijplijnen kunnen delen hetzelfde exemplaar van Hallo bellen op HDInsight-cluster Hallo als de waarde van de eigenschap timetolive Hallo op de juiste wijze is ingesteld</span><span class="sxs-lookup"><span data-stu-id="34b16-2686">Multiple pipelines can share hello same instance of hello on-demand HDInsight cluster if hello timetolive property value is appropriately set</span></span> |<span data-ttu-id="34b16-2687">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2687">Yes</span></span> |
| <span data-ttu-id="34b16-2688">Versie</span><span class="sxs-lookup"><span data-stu-id="34b16-2688">version</span></span> |<span data-ttu-id="34b16-2689">De versie van Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="34b16-2689">Version of hello HDInsight cluster.</span></span> <span data-ttu-id="34b16-2690">Zie voor meer informatie [HDInsight-versies ondersteund in Azure Data Factory](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span><span class="sxs-lookup"><span data-stu-id="34b16-2690">For details, see [supported HDInsight versions in Azure Data Factory](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span></span> |<span data-ttu-id="34b16-2691">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2691">No</span></span> |
| <span data-ttu-id="34b16-2692">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="34b16-2692">linkedServiceName</span></span> |<span data-ttu-id="34b16-2693">Een gekoppelde Azure Storage-service toobe door Hallo op aanvraag cluster gebruikt voor het opslaan en verwerken van gegevens.</span><span class="sxs-lookup"><span data-stu-id="34b16-2693">Azure Storage linked service toobe used by hello on-demand cluster for storing and processing data.</span></span> <p><span data-ttu-id="34b16-2694">Op dit moment kunt maken u een HDInsight-cluster op aanvraag die gebruikmaakt van een Azure Data Lake Store als Hallo opslag niet.</span><span class="sxs-lookup"><span data-stu-id="34b16-2694">Currently, you cannot create an on-demand HDInsight cluster that uses an Azure Data Lake Store as hello storage.</span></span> <span data-ttu-id="34b16-2695">Als u toostore Hallo resultaatgegevens uit HDInsight worden verwerkt in een Azure Data Lake Store wilt, gebruikt u een Kopieeractiviteit toocopy Hallo gegevens van hello Azure Blob Storage toohello Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="34b16-2695">If you want toostore hello result data from HDInsight processing in an Azure Data Lake Store, use a Copy Activity toocopy hello data from hello Azure Blob Storage toohello Azure Data Lake Store.</span></span></p>  | <span data-ttu-id="34b16-2696">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2696">Yes</span></span> |
| <span data-ttu-id="34b16-2697">additionalLinkedServiceNames</span><span class="sxs-lookup"><span data-stu-id="34b16-2697">additionalLinkedServiceNames</span></span> |<span data-ttu-id="34b16-2698">Hiermee geeft u extra opslagaccounts voor Hallo HDInsight gekoppelde service zodat Hallo Data Factory-service namens jou registreren kunt.</span><span class="sxs-lookup"><span data-stu-id="34b16-2698">Specifies additional storage accounts for hello HDInsight linked service so that hello Data Factory service can register them on your behalf.</span></span> |<span data-ttu-id="34b16-2699">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2699">No</span></span> |
| <span data-ttu-id="34b16-2700">besturingssysteemtype</span><span class="sxs-lookup"><span data-stu-id="34b16-2700">osType</span></span> |<span data-ttu-id="34b16-2701">Type besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="34b16-2701">Type of operating system.</span></span> <span data-ttu-id="34b16-2702">Toegestane waarden zijn: (standaard) voor Windows en Linux</span><span class="sxs-lookup"><span data-stu-id="34b16-2702">Allowed values are: Windows (default) and Linux</span></span> |<span data-ttu-id="34b16-2703">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2703">No</span></span> |
| <span data-ttu-id="34b16-2704">hcatalogLinkedServiceName</span><span class="sxs-lookup"><span data-stu-id="34b16-2704">hcatalogLinkedServiceName</span></span> |<span data-ttu-id="34b16-2705">Hallo-naam van de Azure SQL gekoppelde service die punt toohello HCatalog-database.</span><span class="sxs-lookup"><span data-stu-id="34b16-2705">hello name of Azure SQL linked service that point toohello HCatalog database.</span></span> <span data-ttu-id="34b16-2706">Hallo bellen op HDInsight-cluster is gemaakt met behulp van hello Azure SQL-database als Hallo metastore.</span><span class="sxs-lookup"><span data-stu-id="34b16-2706">hello on-demand HDInsight cluster is created by using hello Azure SQL database as hello metastore.</span></span> |<span data-ttu-id="34b16-2707">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2707">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="34b16-2708">JSON-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-2708">JSON example</span></span>
<span data-ttu-id="34b16-2709">Hallo volgende JSON definieert een service op aanvraag een gekoppelde HDInsight op basis van Linux.</span><span class="sxs-lookup"><span data-stu-id="34b16-2709">hello following JSON defines a Linux-based on-demand HDInsight linked service.</span></span> <span data-ttu-id="34b16-2710">Hallo Data Factory-service maakt automatisch een **op basis van Linux** HDInsight-cluster bij het verwerken van een gegevenssegment.</span><span class="sxs-lookup"><span data-stu-id="34b16-2710">hello Data Factory service automatically creates a **Linux-based** HDInsight cluster when processing a data slice.</span></span> 

```json
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "StorageLinkedService"
        }
    }
}
```

<span data-ttu-id="34b16-2711">Zie voor meer informatie [gekoppelde services berekenen](data-factory-compute-linked-services.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-2711">For more information, see [Compute linked services](data-factory-compute-linked-services.md) article.</span></span> 

## <a name="existing-azure-hdinsight-cluster"></a><span data-ttu-id="34b16-2712">Bestaande Azure HDInsight-cluster</span><span class="sxs-lookup"><span data-stu-id="34b16-2712">Existing Azure HDInsight cluster</span></span>
<span data-ttu-id="34b16-2713">U kunt een gekoppelde HDInsight-service tooregister uw eigen HDInsight-cluster maken met Data Factory.</span><span class="sxs-lookup"><span data-stu-id="34b16-2713">You can create an Azure HDInsight linked service tooregister your own HDInsight cluster with Data Factory.</span></span> <span data-ttu-id="34b16-2714">U kunt uitvoeren Hallo activiteiten voor gegevenstransformatie volgen op deze gekoppelde service: [aangepaste activiteit .NET](#net-custom-activity), [Hive-activiteit](#hdinsight-hive-activity), [varkens activiteit] (#hdinsight-pig-activiteit, [MapReduce activiteit](#hdinsight-mapreduce-activity), [Hadoop-streaming activiteit](#hdinsight-streaming-activityd), [Spark activiteit](#hdinsight-spark-activity).</span><span class="sxs-lookup"><span data-stu-id="34b16-2714">You can run hello following data transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="34b16-2715">Gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="34b16-2715">Linked service</span></span>
<span data-ttu-id="34b16-2716">Hallo volgende tabel bevat beschrijvingen van Hallo-eigenschappen die in hello Azure JSON-definitie van een gekoppelde HDInsight-service gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-2716">hello following table provides descriptions for hello properties used in hello Azure JSON definition of an Azure HDInsight linked service.</span></span>

| <span data-ttu-id="34b16-2717">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-2717">Property</span></span> | <span data-ttu-id="34b16-2718">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-2718">Description</span></span> | <span data-ttu-id="34b16-2719">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-2719">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-2720">type</span><span class="sxs-lookup"><span data-stu-id="34b16-2720">type</span></span> |<span data-ttu-id="34b16-2721">de eigenschap type Hello te moet worden ingesteld**HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="34b16-2721">hello type property should be set too**HDInsight**.</span></span> |<span data-ttu-id="34b16-2722">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2722">Yes</span></span> |
| <span data-ttu-id="34b16-2723">clusterUri</span><span class="sxs-lookup"><span data-stu-id="34b16-2723">clusterUri</span></span> |<span data-ttu-id="34b16-2724">Hallo-URI van Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="34b16-2724">hello URI of hello HDInsight cluster.</span></span> |<span data-ttu-id="34b16-2725">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2725">Yes</span></span> |
| <span data-ttu-id="34b16-2726">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="34b16-2726">username</span></span> |<span data-ttu-id="34b16-2727">Geef het Hallo-naam van Hallo gebruiker toobe tooconnect tooan bestaand HDInsight-cluster gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-2727">Specify hello name of hello user toobe used tooconnect tooan existing HDInsight cluster.</span></span> |<span data-ttu-id="34b16-2728">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2728">Yes</span></span> |
| <span data-ttu-id="34b16-2729">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="34b16-2729">password</span></span> |<span data-ttu-id="34b16-2730">Wachtwoord voor gebruikersaccount Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="34b16-2730">Specify password for hello user account.</span></span> |<span data-ttu-id="34b16-2731">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2731">Yes</span></span> |
| <span data-ttu-id="34b16-2732">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="34b16-2732">linkedServiceName</span></span> | <span data-ttu-id="34b16-2733">Naam van Hallo gekoppelde Azure Storage-service die toohello Azure blob-opslag verwijst gebruikt door Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="34b16-2733">Name of hello Azure Storage linked service that refers toohello Azure blob storage used by hello HDInsight cluster.</span></span> <p><span data-ttu-id="34b16-2734">Op dit moment kunt opgeven u niet dat een Azure Data Lake Store gekoppelde service voor deze eigenschap.</span><span class="sxs-lookup"><span data-stu-id="34b16-2734">Currently, you cannot specify an Azure Data Lake Store linked service for this property.</span></span> <span data-ttu-id="34b16-2735">U mogelijk toegang tot gegevens in Azure Data Lake Store Hallo van Hive/Pig-scripts als Hallo HDInsight-cluster toegang tot toohello Data Lake Store heeft.</span><span class="sxs-lookup"><span data-stu-id="34b16-2735">You may access data in hello Azure Data Lake Store from Hive/Pig scripts if hello HDInsight cluster has access toohello Data Lake Store.</span></span> </p>  |<span data-ttu-id="34b16-2736">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2736">Yes</span></span> |

<span data-ttu-id="34b16-2737">Zie voor versies van HDInsight-clusters ondersteund [ondersteunde versies van HDInsight](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span><span class="sxs-lookup"><span data-stu-id="34b16-2737">For versions of HDInsight clusters supported, see [supported HDInsight versions](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span></span> 

#### <a name="json-example"></a><span data-ttu-id="34b16-2738">JSON-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-2738">JSON example</span></span>

```json
{
    "name": "HDInsightLinkedService",
    "properties": {
        "type": "HDInsight",
        "typeProperties": {
            "clusterUri": " https://<hdinsightclustername>.azurehdinsight.net/",
            "userName": "admin",
            "password": "<password>",
            "linkedServiceName": "MyHDInsightStoragelinkedService"
        }
    }
}
```

## <a name="azure-batch"></a><span data-ttu-id="34b16-2739">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="34b16-2739">Azure Batch</span></span>
<span data-ttu-id="34b16-2740">U kunt een Azure Batch gekoppelde service tooregister een Batch-pool van virtuele machines (VM's) maken met een data factory.</span><span class="sxs-lookup"><span data-stu-id="34b16-2740">You can create an Azure Batch linked service tooregister a Batch pool of virtual machines (VMs) with a data factory.</span></span> <span data-ttu-id="34b16-2741">U kunt aangepaste .NET-activiteiten met behulp van Azure Batch of Azure HDInsight kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="34b16-2741">You can run .NET custom activities using either Azure Batch or Azure HDInsight.</span></span> <span data-ttu-id="34b16-2742">U kunt uitvoeren een [aangepaste activiteit .NET](#net-custom-activity) op deze gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="34b16-2742">You can run a [.NET custom activity](#net-custom-activity) on this linked service.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="34b16-2743">Gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="34b16-2743">Linked service</span></span>
<span data-ttu-id="34b16-2744">Hallo volgende tabel bevat beschrijvingen van Hallo-eigenschappen die in hello Azure JSON-definitie van een gekoppelde Azure-Batch-service gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-2744">hello following table provides descriptions for hello properties used in hello Azure JSON definition of an Azure Batch linked service.</span></span>

| <span data-ttu-id="34b16-2745">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-2745">Property</span></span> | <span data-ttu-id="34b16-2746">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-2746">Description</span></span> | <span data-ttu-id="34b16-2747">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-2747">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-2748">type</span><span class="sxs-lookup"><span data-stu-id="34b16-2748">type</span></span> |<span data-ttu-id="34b16-2749">de eigenschap type Hello te moet worden ingesteld**AzureBatch**.</span><span class="sxs-lookup"><span data-stu-id="34b16-2749">hello type property should be set too**AzureBatch**.</span></span> |<span data-ttu-id="34b16-2750">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2750">Yes</span></span> |
| <span data-ttu-id="34b16-2751">Accountnaam</span><span class="sxs-lookup"><span data-stu-id="34b16-2751">accountName</span></span> |<span data-ttu-id="34b16-2752">Naam van hello Azure Batch-account.</span><span class="sxs-lookup"><span data-stu-id="34b16-2752">Name of hello Azure Batch account.</span></span> |<span data-ttu-id="34b16-2753">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2753">Yes</span></span> |
| <span data-ttu-id="34b16-2754">accessKey</span><span class="sxs-lookup"><span data-stu-id="34b16-2754">accessKey</span></span> |<span data-ttu-id="34b16-2755">De toegangssleutel voor hello Azure Batch-account.</span><span class="sxs-lookup"><span data-stu-id="34b16-2755">Access key for hello Azure Batch account.</span></span> |<span data-ttu-id="34b16-2756">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2756">Yes</span></span> |
| <span data-ttu-id="34b16-2757">Groepsnaam</span><span class="sxs-lookup"><span data-stu-id="34b16-2757">poolName</span></span> |<span data-ttu-id="34b16-2758">Naam van het Hallo-pool van virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="34b16-2758">Name of hello pool of virtual machines.</span></span> |<span data-ttu-id="34b16-2759">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2759">Yes</span></span> |
| <span data-ttu-id="34b16-2760">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="34b16-2760">linkedServiceName</span></span> |<span data-ttu-id="34b16-2761">Naam van Hallo gekoppelde Azure Storage-service die is gekoppeld aan deze gekoppelde Azure-Batch-service.</span><span class="sxs-lookup"><span data-stu-id="34b16-2761">Name of hello Azure Storage linked service associated with this Azure Batch linked service.</span></span> <span data-ttu-id="34b16-2762">Deze gekoppelde service wordt gebruikt voor tijdelijke bestanden toorun Hallo activiteit en opslaan van logboekbestanden voor het uitvoeren van activiteit Hallo vereist.</span><span class="sxs-lookup"><span data-stu-id="34b16-2762">This linked service is used for staging files required toorun hello activity and storing hello activity execution logs.</span></span> |<span data-ttu-id="34b16-2763">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2763">Yes</span></span> |


#### <a name="json-example"></a><span data-ttu-id="34b16-2764">JSON-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-2764">JSON example</span></span>

```json
{
    "name": "AzureBatchLinkedService",
    "properties": {
        "type": "AzureBatch",
        "typeProperties": {
            "accountName": "<Azure Batch account name>",
            "accessKey": "<Azure Batch account key>",
            "poolName": "<Azure Batch pool name>",
            "linkedServiceName": "<Specify associated storage linked service reference here>"
        }
    }
}
```

## <a name="azure-machine-learning"></a><span data-ttu-id="34b16-2765">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="34b16-2765">Azure Machine Learning</span></span>
<span data-ttu-id="34b16-2766">U een Azure Machine Learning gekoppelde service tooregister op een Machine Learning score-eindpunt met een gegevensfactory maken.</span><span class="sxs-lookup"><span data-stu-id="34b16-2766">You create an Azure Machine Learning linked service tooregister a Machine Learning batch scoring endpoint with a data factory.</span></span> <span data-ttu-id="34b16-2767">Twee activiteiten voor gegevenstransformatie die kunnen worden uitgevoerd op deze gekoppelde service: [Machine Learning-Batchuitvoeringsactiviteit](#machine-learning-batch-execution-activity), [Resourceactiviteit voor Machine Learning Update](#machine-learning-update-resource-activity).</span><span class="sxs-lookup"><span data-stu-id="34b16-2767">Two data transformation activities that can run on this linked service: [Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="34b16-2768">Gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="34b16-2768">Linked service</span></span>
<span data-ttu-id="34b16-2769">Hallo volgende tabel bevat beschrijvingen van Hallo-eigenschappen die in hello Azure JSON-definitie van een Azure Machine Learning gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="34b16-2769">hello following table provides descriptions for hello properties used in hello Azure JSON definition of an Azure Machine Learning linked service.</span></span>

| <span data-ttu-id="34b16-2770">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-2770">Property</span></span> | <span data-ttu-id="34b16-2771">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-2771">Description</span></span> | <span data-ttu-id="34b16-2772">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-2772">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-2773">Type</span><span class="sxs-lookup"><span data-stu-id="34b16-2773">Type</span></span> |<span data-ttu-id="34b16-2774">Hallo type eigenschap moet worden ingesteld op: **AzureML**.</span><span class="sxs-lookup"><span data-stu-id="34b16-2774">hello type property should be set to: **AzureML**.</span></span> |<span data-ttu-id="34b16-2775">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2775">Yes</span></span> |
| <span data-ttu-id="34b16-2776">mlEndpoint</span><span class="sxs-lookup"><span data-stu-id="34b16-2776">mlEndpoint</span></span> |<span data-ttu-id="34b16-2777">Hallo URL voor batchscores.</span><span class="sxs-lookup"><span data-stu-id="34b16-2777">hello batch scoring URL.</span></span> |<span data-ttu-id="34b16-2778">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2778">Yes</span></span> |
| <span data-ttu-id="34b16-2779">apiKey</span><span class="sxs-lookup"><span data-stu-id="34b16-2779">apiKey</span></span> |<span data-ttu-id="34b16-2780">Hallo gepubliceerde werkruimtemodel op de API.</span><span class="sxs-lookup"><span data-stu-id="34b16-2780">hello published workspace model’s API.</span></span> |<span data-ttu-id="34b16-2781">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2781">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="34b16-2782">JSON-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-2782">JSON example</span></span>

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://[batch scoring endpoint]/jobs",
            "apiKey": "<apikey>"
        }
    }
}
```

## <a name="azure-data-lake-analytics"></a><span data-ttu-id="34b16-2783">Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="34b16-2783">Azure Data Lake Analytics</span></span>
<span data-ttu-id="34b16-2784">U maakt een **Azure Data Lake Analytics** service toolink een Azure Data Lake Analytics compute-service tooan Azure data factory gekoppeld voordat u Hallo [Data Lake Analytics U-SQL-activiteit](data-factory-usql-activity.md) in een pijplijn .</span><span class="sxs-lookup"><span data-stu-id="34b16-2784">You create an **Azure Data Lake Analytics** linked service toolink an Azure Data Lake Analytics compute service tooan Azure data factory before using hello [Data Lake Analytics U-SQL activity](data-factory-usql-activity.md) in a pipeline.</span></span>

### <a name="linked-service"></a><span data-ttu-id="34b16-2785">Gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="34b16-2785">Linked service</span></span>

<span data-ttu-id="34b16-2786">Hallo volgende tabel bevat beschrijvingen van Hallo-eigenschappen die in Hallo JSON-definitie van een service van Azure Data Lake Analytics is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="34b16-2786">hello following table provides descriptions for hello properties used in hello JSON definition of an Azure Data Lake Analytics linked service.</span></span> 

| <span data-ttu-id="34b16-2787">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-2787">Property</span></span> | <span data-ttu-id="34b16-2788">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-2788">Description</span></span> | <span data-ttu-id="34b16-2789">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-2789">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-2790">Type</span><span class="sxs-lookup"><span data-stu-id="34b16-2790">Type</span></span> |<span data-ttu-id="34b16-2791">Hallo type eigenschap moet worden ingesteld op: **AzureDataLakeAnalytics**.</span><span class="sxs-lookup"><span data-stu-id="34b16-2791">hello type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="34b16-2792">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2792">Yes</span></span> |
| <span data-ttu-id="34b16-2793">Accountnaam</span><span class="sxs-lookup"><span data-stu-id="34b16-2793">accountName</span></span> |<span data-ttu-id="34b16-2794">Azure Data Lake Analytics-accountnaam.</span><span class="sxs-lookup"><span data-stu-id="34b16-2794">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="34b16-2795">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2795">Yes</span></span> |
| <span data-ttu-id="34b16-2796">dataLakeAnalyticsUri</span><span class="sxs-lookup"><span data-stu-id="34b16-2796">dataLakeAnalyticsUri</span></span> |<span data-ttu-id="34b16-2797">Azure Data Lake Analytics-URI.</span><span class="sxs-lookup"><span data-stu-id="34b16-2797">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="34b16-2798">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2798">No</span></span> |
| <span data-ttu-id="34b16-2799">Autorisatie</span><span class="sxs-lookup"><span data-stu-id="34b16-2799">authorization</span></span> |<span data-ttu-id="34b16-2800">Autorisatiecode wordt automatisch opgehaald nadat te klikken op **autoriseren** knop in Hallo Data Factory-Editor en voltooit Hallo OAuth-aanmelding.</span><span class="sxs-lookup"><span data-stu-id="34b16-2800">Authorization code is automatically retrieved after clicking **Authorize** button in hello Data Factory Editor and completing hello OAuth login.</span></span> |<span data-ttu-id="34b16-2801">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2801">Yes</span></span> |
| <span data-ttu-id="34b16-2802">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="34b16-2802">subscriptionId</span></span> |<span data-ttu-id="34b16-2803">Azure-abonnement-id</span><span class="sxs-lookup"><span data-stu-id="34b16-2803">Azure subscription id</span></span> |<span data-ttu-id="34b16-2804">Nee (als dit niet is opgegeven, abonnement van Hallo data factory wordt gebruikt).</span><span class="sxs-lookup"><span data-stu-id="34b16-2804">No (If not specified, subscription of hello data factory is used).</span></span> |
| <span data-ttu-id="34b16-2805">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="34b16-2805">resourceGroupName</span></span> |<span data-ttu-id="34b16-2806">Naam van een Azure-resourcegroep</span><span class="sxs-lookup"><span data-stu-id="34b16-2806">Azure resource group name</span></span> |<span data-ttu-id="34b16-2807">Nee (als dit niet is opgegeven, brongroep van Hallo data factory wordt gebruikt).</span><span class="sxs-lookup"><span data-stu-id="34b16-2807">No (If not specified, resource group of hello data factory is used).</span></span> |
| <span data-ttu-id="34b16-2808">sessie-id</span><span class="sxs-lookup"><span data-stu-id="34b16-2808">sessionId</span></span> |<span data-ttu-id="34b16-2809">sessie-id van Hallo OAuth-autorisatie-sessie.</span><span class="sxs-lookup"><span data-stu-id="34b16-2809">session id from hello OAuth authorization session.</span></span> <span data-ttu-id="34b16-2810">Elke sessie-id is uniek en kan slechts eenmaal worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-2810">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="34b16-2811">Wanneer u Hallo Data Factory-Editor gebruikt, wordt deze ID is automatisch gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="34b16-2811">When you use hello Data Factory Editor, this ID is auto-generated.</span></span> |<span data-ttu-id="34b16-2812">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2812">Yes</span></span> |


#### <a name="json-example"></a><span data-ttu-id="34b16-2813">JSON-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-2813">JSON example</span></span>
<span data-ttu-id="34b16-2814">Hallo volgende voorbeeld bevat JSON-definitie voor een service van Azure Data Lake Analytics is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="34b16-2814">hello following example provides JSON definition for an Azure Data Lake Analytics linked service.</span></span>

```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "<account name>",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>",
            "subscriptionId": "<subscription id>",
            "resourceGroupName": "<resource group name>"
        }
    }
}
```

## <a name="azure-sql-database"></a><span data-ttu-id="34b16-2815">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="34b16-2815">Azure SQL Database</span></span>
<span data-ttu-id="34b16-2816">U een Azure SQL gekoppelde service maken en deze gebruiken met Hallo [activiteit opgeslagen Procedure](#stored-procedure-activity) tooinvoke een opgeslagen procedure uit een Data Factory-pijplijn.</span><span class="sxs-lookup"><span data-stu-id="34b16-2816">You create an Azure SQL linked service and use it with hello [Stored Procedure Activity](#stored-procedure-activity) tooinvoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="34b16-2817">Gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="34b16-2817">Linked service</span></span>
<span data-ttu-id="34b16-2818">een Azure SQL Database toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**AzureSqlDatabase**, en opgeven na eigenschappen in Hallo **typeProperties**sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-2818">toodefine an Azure SQL Database linked service, set hello **type** of hello linked service too**AzureSqlDatabase**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="34b16-2819">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-2819">Property</span></span> | <span data-ttu-id="34b16-2820">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-2820">Description</span></span> | <span data-ttu-id="34b16-2821">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-2821">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-2822">connectionString</span><span class="sxs-lookup"><span data-stu-id="34b16-2822">connectionString</span></span> |<span data-ttu-id="34b16-2823">Geef informatie tooconnect toohello Azure SQL Database-exemplaar voor de eigenschap connectionString Hallo nodig.</span><span class="sxs-lookup"><span data-stu-id="34b16-2823">Specify information needed tooconnect toohello Azure SQL Database instance for hello connectionString property.</span></span> |<span data-ttu-id="34b16-2824">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2824">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="34b16-2825">JSON-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-2825">JSON example</span></span>

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="34b16-2826">Zie [Azure SQL-Connector](data-factory-azure-sql-connector.md#linked-service-properties) voor meer informatie over deze gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="34b16-2826">See [Azure SQL Connector](data-factory-azure-sql-connector.md#linked-service-properties) article for details about this linked service.</span></span>

## <a name="azure-sql-data-warehouse"></a><span data-ttu-id="34b16-2827">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="34b16-2827">Azure SQL Data Warehouse</span></span>
<span data-ttu-id="34b16-2828">U een Azure SQL Data Warehouse gekoppelde service maken en deze gebruiken met Hallo [activiteit opgeslagen Procedure](data-factory-stored-proc-activity.md) tooinvoke een opgeslagen procedure uit een Data Factory-pijplijn.</span><span class="sxs-lookup"><span data-stu-id="34b16-2828">You create an Azure SQL Data Warehouse linked service and use it with hello [Stored Procedure Activity](data-factory-stored-proc-activity.md) tooinvoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="34b16-2829">Gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="34b16-2829">Linked service</span></span>
<span data-ttu-id="34b16-2830">een Azure SQL Data Warehouse toodefine gekoppelde service, set Hallo **type** Hallo gekoppelde service te**AzureSqlDW**, en opgeven na eigenschappen in Hallo **typeProperties**sectie:</span><span class="sxs-lookup"><span data-stu-id="34b16-2830">toodefine an Azure SQL Data Warehouse linked service, set hello **type** of hello linked service too**AzureSqlDW**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="34b16-2831">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-2831">Property</span></span> | <span data-ttu-id="34b16-2832">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-2832">Description</span></span> | <span data-ttu-id="34b16-2833">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-2833">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-2834">connectionString</span><span class="sxs-lookup"><span data-stu-id="34b16-2834">connectionString</span></span> |<span data-ttu-id="34b16-2835">Geef informatie tooconnect toohello Azure SQL Data Warehouse-exemplaar voor de eigenschap connectionString Hallo nodig.</span><span class="sxs-lookup"><span data-stu-id="34b16-2835">Specify information needed tooconnect toohello Azure SQL Data Warehouse instance for hello connectionString property.</span></span> |<span data-ttu-id="34b16-2836">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2836">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="34b16-2837">JSON-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-2837">JSON example</span></span>

```json
{
    "name": "AzureSqlDWLinkedService",
    "properties": {
        "type": "AzureSqlDW",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="34b16-2838">Zie voor meer informatie [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-2838">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span></span> 

## <a name="sql-server"></a><span data-ttu-id="34b16-2839">SQL Server</span><span class="sxs-lookup"><span data-stu-id="34b16-2839">SQL Server</span></span> 
<span data-ttu-id="34b16-2840">U een SQL Server gekoppelde service maken en deze gebruiken met Hallo [activiteit opgeslagen Procedure](data-factory-stored-proc-activity.md) tooinvoke een opgeslagen procedure uit een Data Factory-pijplijn.</span><span class="sxs-lookup"><span data-stu-id="34b16-2840">You create a SQL Server linked service and use it with hello [Stored Procedure Activity](data-factory-stored-proc-activity.md) tooinvoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="34b16-2841">Gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="34b16-2841">Linked service</span></span>
<span data-ttu-id="34b16-2842">Maken van een gekoppelde service van het type **OnPremisesSqlServer** toolink een lokale SQL Server-database tooa data factory.</span><span class="sxs-lookup"><span data-stu-id="34b16-2842">You create a linked service of type **OnPremisesSqlServer** toolink an on-premises SQL Server database tooa data factory.</span></span> <span data-ttu-id="34b16-2843">Hallo volgende tabel biedt een beschrijving voor de service voor JSON-elementen specifieke tooon-premises SQL Server gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="34b16-2843">hello following table provides description for JSON elements specific tooon-premises SQL Server linked service.</span></span>

<span data-ttu-id="34b16-2844">Hallo volgende tabel bevat een beschrijving voor JSON-elementen specifieke tooSQL gekoppelde Server-service.</span><span class="sxs-lookup"><span data-stu-id="34b16-2844">hello following table provides description for JSON elements specific tooSQL Server linked service.</span></span>

| <span data-ttu-id="34b16-2845">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-2845">Property</span></span> | <span data-ttu-id="34b16-2846">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-2846">Description</span></span> | <span data-ttu-id="34b16-2847">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-2847">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-2848">type</span><span class="sxs-lookup"><span data-stu-id="34b16-2848">type</span></span> |<span data-ttu-id="34b16-2849">Hallo type eigenschap moet worden ingesteld op: **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="34b16-2849">hello type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="34b16-2850">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2850">Yes</span></span> |
| <span data-ttu-id="34b16-2851">connectionString</span><span class="sxs-lookup"><span data-stu-id="34b16-2851">connectionString</span></span> |<span data-ttu-id="34b16-2852">Geef connectionString informatie nodig tooconnect toohello lokale SQL Server-database met behulp van de SQL-verificatie of de Windows-verificatie.</span><span class="sxs-lookup"><span data-stu-id="34b16-2852">Specify connectionString information needed tooconnect toohello on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="34b16-2853">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2853">Yes</span></span> |
| <span data-ttu-id="34b16-2854">gatewayName</span><span class="sxs-lookup"><span data-stu-id="34b16-2854">gatewayName</span></span> |<span data-ttu-id="34b16-2855">Naam van Hallo-gateway die Hallo Data Factory-service moet tooconnect toohello lokale SQL Server-database gebruiken.</span><span class="sxs-lookup"><span data-stu-id="34b16-2855">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SQL Server database.</span></span> |<span data-ttu-id="34b16-2856">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2856">Yes</span></span> |
| <span data-ttu-id="34b16-2857">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="34b16-2857">username</span></span> |<span data-ttu-id="34b16-2858">Geef de gebruikersnaam als u Windows-verificatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-2858">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="34b16-2859">Voorbeeld: **domainname\\gebruikersnaam**.</span><span class="sxs-lookup"><span data-stu-id="34b16-2859">Example: **domainname\\username**.</span></span> |<span data-ttu-id="34b16-2860">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2860">No</span></span> |
| <span data-ttu-id="34b16-2861">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="34b16-2861">password</span></span> |<span data-ttu-id="34b16-2862">Wachtwoord voor gebruikersaccount Hallo die u hebt opgegeven voor Hallo gebruikersnaam opgeven.</span><span class="sxs-lookup"><span data-stu-id="34b16-2862">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="34b16-2863">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2863">No</span></span> |

<span data-ttu-id="34b16-2864">U kunt referenties met een Hallo versleutelen **nieuw AzureRmDataFactoryEncryptValue** cmdlet en in de verbindingsreeks hello gebruiken, zoals wordt weergegeven in het volgende voorbeeld Hallo (**EncryptedCredential** eigenschap):</span><span class="sxs-lookup"><span data-stu-id="34b16-2864">You can encrypt credentials using hello **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in hello connection string as shown in hello following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a><span data-ttu-id="34b16-2865">Voorbeeld: JSON voor het gebruik van SQL-verificatie</span><span class="sxs-lookup"><span data-stu-id="34b16-2865">Example: JSON for using SQL Authentication</span></span>

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
#### <a name="example-json-for-using-windows-authentication"></a><span data-ttu-id="34b16-2866">Voorbeeld: JSON voor het gebruik van Windows-verificatie</span><span class="sxs-lookup"><span data-stu-id="34b16-2866">Example: JSON for using Windows Authentication</span></span>

<span data-ttu-id="34b16-2867">Als de gebruikersnaam en wachtwoord zijn opgegeven, gateway maakt gebruik van deze tooimpersonate Hallo opgegeven gebruiker account tooconnect toohello lokale SQL Server-database.</span><span class="sxs-lookup"><span data-stu-id="34b16-2867">If username and password are specified, gateway uses them tooimpersonate hello specified user account tooconnect toohello on-premises SQL Server database.</span></span> <span data-ttu-id="34b16-2868">Gatewayserver verbindt anders toohello SQL-Server rechtstreeks met de beveiligingscontext Hallo van Gateway (het starten van de account).</span><span class="sxs-lookup"><span data-stu-id="34b16-2868">Otherwise, gateway connects toohello SQL Server directly with hello security context of Gateway (its startup account).</span></span>

```json
{
    "Name": " MyOnPremisesSQLDB",
    "Properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
            "username": "<domain\\username>",
            "password": "<password>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="34b16-2869">Zie voor meer informatie [SQL Server-connector](data-factory-sqlserver-connector.md#linked-service-properties) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-2869">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span></span>

## <a name="data-transformation-activities"></a><span data-ttu-id="34b16-2870">ACTIVITEITEN VOOR GEGEVENSTRANSFORMATIE</span><span class="sxs-lookup"><span data-stu-id="34b16-2870">DATA TRANSFORMATION ACTIVITIES</span></span>

<span data-ttu-id="34b16-2871">Activiteit</span><span class="sxs-lookup"><span data-stu-id="34b16-2871">Activity</span></span> | <span data-ttu-id="34b16-2872">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-2872">Description</span></span>
-------- | -----------
[<span data-ttu-id="34b16-2873">HDInsight Hive-activiteit</span><span class="sxs-lookup"><span data-stu-id="34b16-2873">HDInsight Hive activity</span></span>](#hdinsight-hive-activity) | <span data-ttu-id="34b16-2874">Hallo HDInsight Hive-activiteit in een Data Factory-pijplijn voert Hive-query's op uw eigen of op aanvraag Windows, Linux-gebaseerde HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="34b16-2874">hello HDInsight Hive activity in a Data Factory pipeline executes Hive queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span> 
[<span data-ttu-id="34b16-2875">HDInsight Pig-activiteit</span><span class="sxs-lookup"><span data-stu-id="34b16-2875">HDInsight Pig activity</span></span>](#hdinsight-pig-activity) | <span data-ttu-id="34b16-2876">Hallo HDInsight Pig-activiteit in een Data Factory-pijplijn voert Pig-query's in uw eigen of op aanvraag Windows, Linux-gebaseerde HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="34b16-2876">hello HDInsight Pig activity in a Data Factory pipeline executes Pig queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="34b16-2877">HDInsight MapReduce-activiteit</span><span class="sxs-lookup"><span data-stu-id="34b16-2877">HDInsight MapReduce Activity</span></span>](#hdinsight-mapreduce-activity) | <span data-ttu-id="34b16-2878">Hallo HDInsight MapReduce-activiteit in een Data Factory-pijplijn voert MapReduce-programma's op uw eigen of op aanvraag Windows, Linux-gebaseerde HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="34b16-2878">hello HDInsight MapReduce activity in a Data Factory pipeline executes MapReduce programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="34b16-2879">HDInsight Streaming-activiteit</span><span class="sxs-lookup"><span data-stu-id="34b16-2879">HDInsight Streaming Activity</span></span>](#hdinsight-streaming-activity) | <span data-ttu-id="34b16-2880">Hallo Streaming HDInsight-activiteit in een Data Factory-pijplijn voert Hadoop-Streaming programma's op uw eigen of op aanvraag Windows, Linux-gebaseerde HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="34b16-2880">hello HDInsight Streaming Activity in a Data Factory pipeline executes Hadoop Streaming programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="34b16-2881">HDInsight Spark-activiteit</span><span class="sxs-lookup"><span data-stu-id="34b16-2881">HDInsight Spark Activity</span></span>](#hdinsight-spark-activity) | <span data-ttu-id="34b16-2882">Hallo HDInsight Spark-activiteit in een Data Factory-pijplijn Spark-programma's op uw eigen HDInsight-cluster wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="34b16-2882">hello HDInsight Spark activity in a Data Factory pipeline executes Spark programs on your own HDInsight cluster.</span></span> 
[<span data-ttu-id="34b16-2883">Machine Learning-batchuitvoeringsactiviteit</span><span class="sxs-lookup"><span data-stu-id="34b16-2883">Machine Learning Batch Execution Activity</span></span>](#machine-learning-batch-execution-activity) | <span data-ttu-id="34b16-2884">Azure Data Factory kunt u tooeasily maken pijplijnen die gebruikmaken van een gepubliceerde Azure Machine Learning-webservice voor predictive analytics.</span><span class="sxs-lookup"><span data-stu-id="34b16-2884">Azure Data Factory enables you tooeasily create pipelines that use a published Azure Machine Learning web service for predictive analytics.</span></span> <span data-ttu-id="34b16-2885">Hallo-Batchuitvoeringsactiviteit in een Azure Data Factory-pijplijn kunt u een Machine Learning web service toomake voorspellingen op Hallo-gegevens in een batch aanroepen.</span><span class="sxs-lookup"><span data-stu-id="34b16-2885">Using hello Batch Execution Activity in an Azure Data Factory pipeline, you can invoke a Machine Learning web service toomake predictions on hello data in batch.</span></span> 
[<span data-ttu-id="34b16-2886">Machine Learning-activiteit resources bijwerken</span><span class="sxs-lookup"><span data-stu-id="34b16-2886">Machine Learning Update Resource Activity</span></span>](#machine-learning-update-resource-activity) | <span data-ttu-id="34b16-2887">Na verloop van tijd invoer Hallo voorspellende modellen in Machine Learning-score experimenten moeten toobe retrained met nieuwe Hallo gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="34b16-2887">Over time, hello predictive models in hello Machine Learning scoring experiments need toobe retrained using new input datasets.</span></span> <span data-ttu-id="34b16-2888">Wanneer u klaar bent met de retraining, wilt u tooupdate Hallo score berekenen voor webservice Hello retrained Machine Learning-model.</span><span class="sxs-lookup"><span data-stu-id="34b16-2888">After you are done with retraining, you want tooupdate hello scoring web service with hello retrained Machine Learning model.</span></span> <span data-ttu-id="34b16-2889">Met de Hallo zojuist getraind model kunt u Hallo Update Resourceactiviteit tooupdate Hallo-webservice.</span><span class="sxs-lookup"><span data-stu-id="34b16-2889">You can use hello Update Resource Activity tooupdate hello web service with hello newly trained model.</span></span>
[<span data-ttu-id="34b16-2890">Opgeslagen procedureactiviteit</span><span class="sxs-lookup"><span data-stu-id="34b16-2890">Stored Procedure Activity</span></span>](#stored-procedure-activity) | <span data-ttu-id="34b16-2891">U kunt de activiteit opgeslagen Procedure hello gebruiken in een Data Factory-pijplijn tooinvoke een opgeslagen procedure in een van volgende gegevensarchieven Hallo: Azure SQL Database, Azure SQL Data Warehouse, SQL Server-Database in uw onderneming of een Azure VM.</span><span class="sxs-lookup"><span data-stu-id="34b16-2891">You can use hello Stored Procedure activity in a Data Factory pipeline tooinvoke a stored procedure in one of hello following data stores: Azure SQL Database, Azure SQL Data Warehouse, SQL Server Database in your enterprise or an Azure VM.</span></span> 
[<span data-ttu-id="34b16-2892">Data Lake Analytics U-SQL-activiteit</span><span class="sxs-lookup"><span data-stu-id="34b16-2892">Data Lake Analytics U-SQL activity</span></span>](#data-lake-analytics-u-sql-activity) | <span data-ttu-id="34b16-2893">Data Lake Analytics U-SQL-activiteit wordt een U-SQL-script uitgevoerd op een Azure Data Lake Analytics-cluster.</span><span class="sxs-lookup"><span data-stu-id="34b16-2893">Data Lake Analytics U-SQL Activity runs a U-SQL script on an Azure Data Lake Analytics cluster.</span></span>  
[<span data-ttu-id="34b16-2894">.NET aangepaste activiteit</span><span class="sxs-lookup"><span data-stu-id="34b16-2894">.NET custom activity</span></span>](#net-custom-activity) | <span data-ttu-id="34b16-2895">Als u gegevens op een manier die niet wordt ondersteund door Data Factory tootransform moet, kunt u een aangepaste activiteit maken met uw eigen logica gegevensverwerking en Hallo activiteit in de pijplijn hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="34b16-2895">If you need tootransform data in a way that is not supported by Data Factory, you can create a custom activity with your own data processing logic and use hello activity in hello pipeline.</span></span> <span data-ttu-id="34b16-2896">U kunt Hallo aangepaste .NET activiteit toorun met behulp van een Azure Batch-service of een Azure HDInsight-cluster configureren.</span><span class="sxs-lookup"><span data-stu-id="34b16-2896">You can configure hello custom .NET activity toorun using either an Azure Batch service or an Azure HDInsight cluster.</span></span> 

     
## <a name="hdinsight-hive-activity"></a><span data-ttu-id="34b16-2897">HDInsight Hive-activiteit</span><span class="sxs-lookup"><span data-stu-id="34b16-2897">HDInsight Hive Activity</span></span>
<span data-ttu-id="34b16-2898">Kunt u de volgende eigenschappen in de definitie van een Hive-activiteit JSON Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="34b16-2898">You can specify hello following properties in a Hive Activity JSON definition.</span></span> <span data-ttu-id="34b16-2899">eigenschap voor het type voor activiteit Hallo Hallo moet zijn: **HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="34b16-2899">hello type property for hello activity must be: **HDInsightHive**.</span></span> <span data-ttu-id="34b16-2900">Moet u eerst een gekoppelde HDInsight-service maken en Hallo-naam van dit opgeven als een waarde voor Hallo **linkedServiceName** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="34b16-2900">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="34b16-2901">Hallo volgende eigenschappen worden ondersteund in Hallo **typeProperties** sectie bij het instellen van het soort activiteit tooHDInsightHive Hallo:</span><span class="sxs-lookup"><span data-stu-id="34b16-2901">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightHive:</span></span>

| <span data-ttu-id="34b16-2902">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-2902">Property</span></span> | <span data-ttu-id="34b16-2903">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-2903">Description</span></span> | <span data-ttu-id="34b16-2904">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-2904">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-2905">Script</span><span class="sxs-lookup"><span data-stu-id="34b16-2905">script</span></span> |<span data-ttu-id="34b16-2906">Hallo Hive-script inline opgeven</span><span class="sxs-lookup"><span data-stu-id="34b16-2906">Specify hello Hive script inline</span></span> |<span data-ttu-id="34b16-2907">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2907">No</span></span> |
| <span data-ttu-id="34b16-2908">scriptpad</span><span class="sxs-lookup"><span data-stu-id="34b16-2908">script path</span></span> |<span data-ttu-id="34b16-2909">Hallo archief Hive-script in een Azure blob storage en geef Hallo pad toohello bestand.</span><span class="sxs-lookup"><span data-stu-id="34b16-2909">Store hello Hive script in an Azure blob storage and provide hello path toohello file.</span></span> <span data-ttu-id="34b16-2910">Gebruik de eigenschap 'script' of 'scriptPath'.</span><span class="sxs-lookup"><span data-stu-id="34b16-2910">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="34b16-2911">Beide kunnen niet samen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-2911">Both cannot be used together.</span></span> <span data-ttu-id="34b16-2912">Hallo-bestandsnaam is hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="34b16-2912">hello file name is case-sensitive.</span></span> |<span data-ttu-id="34b16-2913">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2913">No</span></span> |
| <span data-ttu-id="34b16-2914">Hiermee worden gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="34b16-2914">defines</span></span> |<span data-ttu-id="34b16-2915">Geef parameters op als sleutel-waardeparen voor verwijzende binnen Hallo Hive-script met behulp van 'hiveconf'</span><span class="sxs-lookup"><span data-stu-id="34b16-2915">Specify parameters as key/value pairs for referencing within hello Hive script using 'hiveconf'</span></span> |<span data-ttu-id="34b16-2916">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2916">No</span></span> |

<span data-ttu-id="34b16-2917">Deze eigenschappen zijn specifieke toohello Hive-activiteit.</span><span class="sxs-lookup"><span data-stu-id="34b16-2917">These type properties are specific toohello Hive Activity.</span></span> <span data-ttu-id="34b16-2918">Andere eigenschappen (buiten Hallo typeProperties sectie) worden ondersteund voor alle activiteiten.</span><span class="sxs-lookup"><span data-stu-id="34b16-2918">Other properties (outside hello typeProperties section) are supported for all activities.</span></span>   

### <a name="json-example"></a><span data-ttu-id="34b16-2919">JSON-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-2919">JSON example</span></span>
<span data-ttu-id="34b16-2920">Hallo volgende JSON definieert een HDInsight Hive-activiteit in een pijplijn.</span><span class="sxs-lookup"><span data-stu-id="34b16-2920">hello following JSON defines a HDInsight Hive activity in a pipeline.</span></span>  

```json
{
    "name": "Hive Activity",
    "description": "description",
    "type": "HDInsightHive",
    "inputs": [
      {
        "name": "input tables"
      }
    ],
    "outputs": [
      {
        "name": "output tables"
      }
    ],
    "linkedServiceName": "MyHDInsightLinkedService",
    "typeProperties": {
      "script": "Hive script",
      "scriptPath": "<pathtotheHivescriptfileinAzureblobstorage>",
      "defines": {
        "param1": "param1Value"
      }
    },
   "scheduler": {
      "frequency": "Day",
      "interval": 1
    }
}
```

<span data-ttu-id="34b16-2921">Zie voor meer informatie [Hive-activiteit](data-factory-hive-activity.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-2921">For more information, see [Hive Activity](data-factory-hive-activity.md) article.</span></span> 

## <a name="hdinsight-pig-activity"></a><span data-ttu-id="34b16-2922">HDInsight Pig-activiteit</span><span class="sxs-lookup"><span data-stu-id="34b16-2922">HDInsight Pig Activity</span></span>
<span data-ttu-id="34b16-2923">Kunt u de volgende eigenschappen in de definitie van een Pig activiteit JSON Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="34b16-2923">You can specify hello following properties in a Pig Activity JSON definition.</span></span> <span data-ttu-id="34b16-2924">eigenschap voor het type voor activiteit Hallo Hallo moet zijn: **HDInsightPig**.</span><span class="sxs-lookup"><span data-stu-id="34b16-2924">hello type property for hello activity must be: **HDInsightPig**.</span></span> <span data-ttu-id="34b16-2925">Moet u eerst een gekoppelde HDInsight-service maken en Hallo-naam van dit opgeven als een waarde voor Hallo **linkedServiceName** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="34b16-2925">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="34b16-2926">Hallo volgende eigenschappen worden ondersteund in Hallo **typeProperties** sectie bij het instellen van het soort activiteit tooHDInsightPig Hallo:</span><span class="sxs-lookup"><span data-stu-id="34b16-2926">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightPig:</span></span> 

| <span data-ttu-id="34b16-2927">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-2927">Property</span></span> | <span data-ttu-id="34b16-2928">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-2928">Description</span></span> | <span data-ttu-id="34b16-2929">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-2929">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-2930">Script</span><span class="sxs-lookup"><span data-stu-id="34b16-2930">script</span></span> |<span data-ttu-id="34b16-2931">Hallo Pig-script inline opgeven</span><span class="sxs-lookup"><span data-stu-id="34b16-2931">Specify hello Pig script inline</span></span> |<span data-ttu-id="34b16-2932">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2932">No</span></span> |
| <span data-ttu-id="34b16-2933">scriptpad</span><span class="sxs-lookup"><span data-stu-id="34b16-2933">script path</span></span> |<span data-ttu-id="34b16-2934">Hallo Pig-script opslaat in Azure blob storage en geef Hallo pad toohello-bestand.</span><span class="sxs-lookup"><span data-stu-id="34b16-2934">Store hello Pig script in an Azure blob storage and provide hello path toohello file.</span></span> <span data-ttu-id="34b16-2935">Gebruik de eigenschap 'script' of 'scriptPath'.</span><span class="sxs-lookup"><span data-stu-id="34b16-2935">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="34b16-2936">Beide kunnen niet samen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-2936">Both cannot be used together.</span></span> <span data-ttu-id="34b16-2937">Hallo-bestandsnaam is hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="34b16-2937">hello file name is case-sensitive.</span></span> |<span data-ttu-id="34b16-2938">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2938">No</span></span> |
| <span data-ttu-id="34b16-2939">Hiermee worden gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="34b16-2939">defines</span></span> |<span data-ttu-id="34b16-2940">Geef parameters op als sleutel-waardeparen voor verwijzende binnen Hallo Pig-script</span><span class="sxs-lookup"><span data-stu-id="34b16-2940">Specify parameters as key/value pairs for referencing within hello Pig script</span></span> |<span data-ttu-id="34b16-2941">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2941">No</span></span> |

<span data-ttu-id="34b16-2942">Deze eigenschappen zijn specifieke toohello Pig-activiteit.</span><span class="sxs-lookup"><span data-stu-id="34b16-2942">These type properties are specific toohello Pig Activity.</span></span> <span data-ttu-id="34b16-2943">Andere eigenschappen (buiten Hallo typeProperties sectie) worden ondersteund voor alle activiteiten.</span><span class="sxs-lookup"><span data-stu-id="34b16-2943">Other properties (outside hello typeProperties section) are supported for all activities.</span></span>   

### <a name="json-example"></a><span data-ttu-id="34b16-2944">JSON-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-2944">JSON example</span></span>

```json
{
    "name": "HiveActivitySamplePipeline",
      "properties": {
    "activities": [
        {
            "name": "Pig Activity",
            "description": "description",
            "type": "HDInsightPig",
            "inputs": [
                  {
                    "name": "input tables"
                  }
            ],
            "outputs": [
                  {
                    "name": "output tables"
                  }
            ],
            "linkedServiceName": "MyHDInsightLinkedService",
            "typeProperties": {
                  "script": "Pig script",
                  "scriptPath": "<pathtothePigscriptfileinAzureblobstorage>",
                  "defines": {
                    "param1": "param1Value"
                  }
            },
               "scheduler": {
                  "frequency": "Day",
                  "interval": 1
            }
          }
    ]
  }
}
```

<span data-ttu-id="34b16-2945">Zie voor meer informatie [Pig activiteit](#data-factory-pig-activity.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-2945">For more information, see [Pig Activity](#data-factory-pig-activity.md) article.</span></span> 

## <a name="hdinsight-mapreduce-activity"></a><span data-ttu-id="34b16-2946">HDInsight MapReduce-activiteit</span><span class="sxs-lookup"><span data-stu-id="34b16-2946">HDInsight MapReduce Activity</span></span>
<span data-ttu-id="34b16-2947">Kunt u de volgende eigenschappen in de definitie van een MapReduce-activiteit JSON Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="34b16-2947">You can specify hello following properties in a MapReduce Activity JSON definition.</span></span> <span data-ttu-id="34b16-2948">eigenschap voor het type voor activiteit Hallo Hallo moet zijn: **HDInsightMapReduce**.</span><span class="sxs-lookup"><span data-stu-id="34b16-2948">hello type property for hello activity must be: **HDInsightMapReduce**.</span></span> <span data-ttu-id="34b16-2949">Moet u eerst een gekoppelde HDInsight-service maken en Hallo-naam van dit opgeven als een waarde voor Hallo **linkedServiceName** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="34b16-2949">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="34b16-2950">Hallo volgende eigenschappen worden ondersteund in Hallo **typeProperties** sectie bij het instellen van het soort activiteit tooHDInsightMapReduce Hallo:</span><span class="sxs-lookup"><span data-stu-id="34b16-2950">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightMapReduce:</span></span> 

| <span data-ttu-id="34b16-2951">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-2951">Property</span></span> | <span data-ttu-id="34b16-2952">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-2952">Description</span></span> | <span data-ttu-id="34b16-2953">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-2953">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-2954">jarLinkedService</span><span class="sxs-lookup"><span data-stu-id="34b16-2954">jarLinkedService</span></span> | <span data-ttu-id="34b16-2955">Naam van Hallo gekoppelde service voor hello Azure Storage dat Hallo JAR-bestand bevat.</span><span class="sxs-lookup"><span data-stu-id="34b16-2955">Name of hello linked service for hello Azure Storage that contains hello JAR file.</span></span> | <span data-ttu-id="34b16-2956">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2956">Yes</span></span> |
| <span data-ttu-id="34b16-2957">jarFilePath</span><span class="sxs-lookup"><span data-stu-id="34b16-2957">jarFilePath</span></span> | <span data-ttu-id="34b16-2958">Pad toohello JAR-bestand in hello Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="34b16-2958">Path toohello JAR file in hello Azure Storage.</span></span> | <span data-ttu-id="34b16-2959">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2959">Yes</span></span> | 
| <span data-ttu-id="34b16-2960">className</span><span class="sxs-lookup"><span data-stu-id="34b16-2960">className</span></span> | <span data-ttu-id="34b16-2961">Naam van de hoofdklasse Hallo in Hallo JAR-bestand.</span><span class="sxs-lookup"><span data-stu-id="34b16-2961">Name of hello main class in hello JAR file.</span></span> | <span data-ttu-id="34b16-2962">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-2962">Yes</span></span> | 
| <span data-ttu-id="34b16-2963">Argumenten</span><span class="sxs-lookup"><span data-stu-id="34b16-2963">arguments</span></span> | <span data-ttu-id="34b16-2964">Een lijst met door komma's gescheiden argumenten voor Hallo MapReduce-programma.</span><span class="sxs-lookup"><span data-stu-id="34b16-2964">A list of comma-separated arguments for hello MapReduce program.</span></span> <span data-ttu-id="34b16-2965">Tijdens runtime, ziet u enkele extra argumenten (bijvoorbeeld: mapreduce.job.tags) van Hallo MapReduce-framework.</span><span class="sxs-lookup"><span data-stu-id="34b16-2965">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from hello MapReduce framework.</span></span> <span data-ttu-id="34b16-2966">toodifferentiate uw argumenten met Hallo MapReduce argumenten, overweeg het gebruik van zowel de optie als de waarde als argumenten, zoals wordt weergegeven in het volgende voorbeeld Hallo (- s,--invoer,--uitvoer enz., zijn opties onmiddellijk wordt gevolgd door hun waarden)</span><span class="sxs-lookup"><span data-stu-id="34b16-2966">toodifferentiate your arguments with hello MapReduce arguments, consider using both option and value as arguments as shown in hello following example (-s, --input, --output etc., are options immediately followed by their values)</span></span> | <span data-ttu-id="34b16-2967">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-2967">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="34b16-2968">JSON-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-2968">JSON example</span></span>

```json
{
    "name": "MahoutMapReduceSamplePipeline",
    "properties": {
        "description": "Sample Pipeline tooRun a Mahout Custom Map Reduce Jar. This job calculates an Item Similarity Matrix toodetermine hello similarity between two items",
        "activities": [
            {
                "type": "HDInsightMapReduce",
                "typeProperties": {
                    "className": "org.apache.mahout.cf.taste.hadoop.similarity.item.ItemSimilarityJob",
                    "jarFilePath": "adfsamples/Mahout/jars/mahout-examples-0.9.0.2.2.7.1-34.jar",
                    "jarLinkedService": "StorageLinkedService",
                    "arguments": ["-s", "SIMILARITY_LOGLIKELIHOOD", "--input", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/input", "--output", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/output/", "--maxSimilaritiesPerItem", "500", "--tempDir", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/temp/mahout"]
                },
                "inputs": [
                    {
                        "name": "MahoutInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "MahoutOutput"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "MahoutActivity",
                "description": "Custom Map Reduce toogenerate Mahout result",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-01-03T00:00:00",
        "end": "2017-01-04T00:00:00"
    }
}
```

<span data-ttu-id="34b16-2969">Zie voor meer informatie [MapReduce-activiteit](data-factory-map-reduce.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-2969">For more information, see [MapReduce Activity](data-factory-map-reduce.md) article.</span></span> 

## <a name="hdinsight-streaming-activity"></a><span data-ttu-id="34b16-2970">HDInsight-streamingactiviteit</span><span class="sxs-lookup"><span data-stu-id="34b16-2970">HDInsight Streaming Activity</span></span>
<span data-ttu-id="34b16-2971">Kunt u de volgende eigenschappen in de definitie van een Hadoop Streaming activiteit JSON Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="34b16-2971">You can specify hello following properties in a Hadoop Streaming Activity JSON definition.</span></span> <span data-ttu-id="34b16-2972">eigenschap voor het type voor activiteit Hallo Hallo moet zijn: **HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="34b16-2972">hello type property for hello activity must be: **HDInsightStreaming**.</span></span> <span data-ttu-id="34b16-2973">Moet u eerst een gekoppelde HDInsight-service maken en Hallo-naam van dit opgeven als een waarde voor Hallo **linkedServiceName** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="34b16-2973">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="34b16-2974">Hallo volgende eigenschappen worden ondersteund in Hallo **typeProperties** sectie bij het instellen van het soort activiteit tooHDInsightStreaming Hallo:</span><span class="sxs-lookup"><span data-stu-id="34b16-2974">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightStreaming:</span></span> 

| <span data-ttu-id="34b16-2975">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-2975">Property</span></span> | <span data-ttu-id="34b16-2976">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-2976">Description</span></span> | 
| --- | --- |
| <span data-ttu-id="34b16-2977">toewijzen</span><span class="sxs-lookup"><span data-stu-id="34b16-2977">mapper</span></span> | <span data-ttu-id="34b16-2978">Naam van Hallo mapper uitvoerbare.</span><span class="sxs-lookup"><span data-stu-id="34b16-2978">Name of hello mapper executable.</span></span> <span data-ttu-id="34b16-2979">In voorbeeld Hallo is cat.exe Hallo mapper uitvoerbare.</span><span class="sxs-lookup"><span data-stu-id="34b16-2979">In hello example, cat.exe is hello mapper executable.</span></span>| 
| <span data-ttu-id="34b16-2980">reducer</span><span class="sxs-lookup"><span data-stu-id="34b16-2980">reducer</span></span> | <span data-ttu-id="34b16-2981">Naam van Hallo reducer uitvoerbare.</span><span class="sxs-lookup"><span data-stu-id="34b16-2981">Name of hello reducer executable.</span></span> <span data-ttu-id="34b16-2982">In voorbeeld Hallo is wc.exe hello reducer uitvoerbare.</span><span class="sxs-lookup"><span data-stu-id="34b16-2982">In hello example, wc.exe is hello reducer executable.</span></span> | 
| <span data-ttu-id="34b16-2983">Invoer</span><span class="sxs-lookup"><span data-stu-id="34b16-2983">input</span></span> | <span data-ttu-id="34b16-2984">Invoerbestand (inclusief locatie) voor Hallo toewijzen.</span><span class="sxs-lookup"><span data-stu-id="34b16-2984">Input file (including location) for hello mapper.</span></span> <span data-ttu-id="34b16-2985">In Hallo-voorbeeld: ' wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt ': adfsample is Hallo blob-container, gegevens-voorbeeld/Gutenberg Hallo-map en davinci.txt Hallo blob is.</span><span class="sxs-lookup"><span data-stu-id="34b16-2985">In hello example: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample is hello blob container, example/data/Gutenberg is hello folder, and davinci.txt is hello blob.</span></span> |
| <span data-ttu-id="34b16-2986">Uitvoer</span><span class="sxs-lookup"><span data-stu-id="34b16-2986">output</span></span> | <span data-ttu-id="34b16-2987">Uitvoerbestand (inclusief locatie) voor Hallo reducer.</span><span class="sxs-lookup"><span data-stu-id="34b16-2987">Output file (including location) for hello reducer.</span></span> <span data-ttu-id="34b16-2988">Hallo-uitvoer van Hallo Hadoop streamingtaak geschreven toohello locatie die is opgegeven voor deze eigenschap.</span><span class="sxs-lookup"><span data-stu-id="34b16-2988">hello output of hello Hadoop Streaming job is written toohello location specified for this property.</span></span> |
| <span data-ttu-id="34b16-2989">filePaths</span><span class="sxs-lookup"><span data-stu-id="34b16-2989">filePaths</span></span> | <span data-ttu-id="34b16-2990">Paden voor Hallo toewijzen en reducer uitvoerbare bestanden.</span><span class="sxs-lookup"><span data-stu-id="34b16-2990">Paths for hello mapper and reducer executables.</span></span> <span data-ttu-id="34b16-2991">In Hallo-voorbeeld: 'adfsample/example/apps/wc.exe' adfsample is Hallo blob-container, voorbeeld/apps Hallo-map en wc.exe Hallo uitvoerbare is.</span><span class="sxs-lookup"><span data-stu-id="34b16-2991">In hello example: "adfsample/example/apps/wc.exe", adfsample is hello blob container, example/apps is hello folder, and wc.exe is hello executable.</span></span> | 
| <span data-ttu-id="34b16-2992">fileLinkedService</span><span class="sxs-lookup"><span data-stu-id="34b16-2992">fileLinkedService</span></span> | <span data-ttu-id="34b16-2993">Gekoppelde Azure Storage-service die hello Azure-opslag met Hallo-bestanden die zijn opgegeven in Hallo filePaths sectie vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="34b16-2993">Azure Storage linked service that represents hello Azure storage that contains hello files specified in hello filePaths section.</span></span> | 
| <span data-ttu-id="34b16-2994">Argumenten</span><span class="sxs-lookup"><span data-stu-id="34b16-2994">arguments</span></span> | <span data-ttu-id="34b16-2995">Een lijst met door komma's gescheiden argumenten voor Hallo MapReduce-programma.</span><span class="sxs-lookup"><span data-stu-id="34b16-2995">A list of comma-separated arguments for hello MapReduce program.</span></span> <span data-ttu-id="34b16-2996">Tijdens runtime, ziet u enkele extra argumenten (bijvoorbeeld: mapreduce.job.tags) van Hallo MapReduce-framework.</span><span class="sxs-lookup"><span data-stu-id="34b16-2996">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from hello MapReduce framework.</span></span> <span data-ttu-id="34b16-2997">toodifferentiate uw argumenten met Hallo MapReduce argumenten, overweeg het gebruik van zowel de optie als de waarde als argumenten, zoals wordt weergegeven in het volgende voorbeeld Hallo (- s,--invoer,--uitvoer enz., zijn opties onmiddellijk wordt gevolgd door hun waarden)</span><span class="sxs-lookup"><span data-stu-id="34b16-2997">toodifferentiate your arguments with hello MapReduce arguments, consider using both option and value as arguments as shown in hello following example (-s, --input, --output etc., are options immediately followed by their values)</span></span> | 
| <span data-ttu-id="34b16-2998">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="34b16-2998">getDebugInfo</span></span> | <span data-ttu-id="34b16-2999">Een optioneel element.</span><span class="sxs-lookup"><span data-stu-id="34b16-2999">An optional element.</span></span> <span data-ttu-id="34b16-3000">Wanneer deze tooFailure is ingesteld, worden alleen op fout Hallo logboeken gedownload.</span><span class="sxs-lookup"><span data-stu-id="34b16-3000">When it is set tooFailure, hello logs are downloaded only on failure.</span></span> <span data-ttu-id="34b16-3001">Wanneer deze tooAll is ingesteld, worden altijd logboeken ongeacht de uitvoeringsstatus van Hallo gedownload.</span><span class="sxs-lookup"><span data-stu-id="34b16-3001">When it is set tooAll, logs are always downloaded irrespective of hello execution status.</span></span> | 

> [!NOTE]
> <span data-ttu-id="34b16-3002">Geef een uitvoergegevensset voor Hadoop-Streamingactiviteit Hallo voor Hallo **levert** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="34b16-3002">You must specify an output dataset for hello Hadoop Streaming Activity for hello **outputs** property.</span></span> <span data-ttu-id="34b16-3003">Deze gegevensset mag alleen een dummy gegevensset die is vereist toodrive Hallo pijplijn planning (elk uur, dagelijks, enz.).</span><span class="sxs-lookup"><span data-stu-id="34b16-3003">This dataset can be just a dummy dataset that is required toodrive hello pipeline schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="34b16-3004">Als Hallo activiteit geen invoer nemen, kunt u overslaan geven een invoergegevensset voor de activiteit voor Hallo Hallo **invoer** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="34b16-3004">If hello activity doesn't take an input, you can skip specifying an input dataset for hello activity for hello **inputs** property.</span></span>  

## <a name="json-example"></a><span data-ttu-id="34b16-3005">JSON-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-3005">JSON example</span></span>

```json
{
    "name": "HadoopStreamingPipeline",
    "properties": {
        "description": "Hadoop Streaming Demo",
        "activities": [
            {
                "type": "HDInsightStreaming",
                "typeProperties": {
                    "mapper": "cat.exe",
                    "reducer": "wc.exe",
                    "input": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": ["<nameofthecluster>/example/apps/wc.exe","<nameofthecluster>/example/apps/cat.exe"],
                    "fileLinkedService": "StorageLinkedService",
                    "getDebugInfo": "Failure"
                },
                "outputs": [
                    {
                        "name": "StreamingOutputDataset"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "RunHadoopStreamingJob",
                "description": "Run a Hadoop streaming job",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-04T00:00:00",
        "end": "2014-01-05T00:00:00"
    }
}
```

<span data-ttu-id="34b16-3006">Zie voor meer informatie [Hadoop-Streamingactiviteit](data-factory-hadoop-streaming-activity.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-3006">For more information, see [Hadoop Streaming Activity](data-factory-hadoop-streaming-activity.md) article.</span></span> 

## <a name="hdinsight-spark-activity"></a><span data-ttu-id="34b16-3007">HDInsight Spark-activiteit</span><span class="sxs-lookup"><span data-stu-id="34b16-3007">HDInsight Spark Activity</span></span>
<span data-ttu-id="34b16-3008">Kunt u de volgende eigenschappen in de definitie van een Spark activiteit JSON Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="34b16-3008">You can specify hello following properties in a Spark Activity JSON definition.</span></span> <span data-ttu-id="34b16-3009">eigenschap voor het type voor activiteit Hallo Hallo moet zijn: **HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="34b16-3009">hello type property for hello activity must be: **HDInsightSpark**.</span></span> <span data-ttu-id="34b16-3010">Moet u eerst een gekoppelde HDInsight-service maken en Hallo-naam van dit opgeven als een waarde voor Hallo **linkedServiceName** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="34b16-3010">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="34b16-3011">Hallo volgende eigenschappen worden ondersteund in Hallo **typeProperties** sectie bij het instellen van het soort activiteit tooHDInsightSpark Hallo:</span><span class="sxs-lookup"><span data-stu-id="34b16-3011">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightSpark:</span></span> 

| <span data-ttu-id="34b16-3012">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-3012">Property</span></span> | <span data-ttu-id="34b16-3013">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-3013">Description</span></span> | <span data-ttu-id="34b16-3014">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-3014">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="34b16-3015">rootPath</span><span class="sxs-lookup"><span data-stu-id="34b16-3015">rootPath</span></span> | <span data-ttu-id="34b16-3016">Hello Azure Blob-container en map met Hallo Spark-bestand.</span><span class="sxs-lookup"><span data-stu-id="34b16-3016">hello Azure Blob container and folder that contains hello Spark file.</span></span> <span data-ttu-id="34b16-3017">Hallo-bestandsnaam is hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="34b16-3017">hello file name is case-sensitive.</span></span> | <span data-ttu-id="34b16-3018">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-3018">Yes</span></span> |
| <span data-ttu-id="34b16-3019">entryFilePath</span><span class="sxs-lookup"><span data-stu-id="34b16-3019">entryFilePath</span></span> | <span data-ttu-id="34b16-3020">Relatief pad toohello Hallo Spark codepakket hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="34b16-3020">Relative path toohello root folder of hello Spark code/package.</span></span> | <span data-ttu-id="34b16-3021">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-3021">Yes</span></span> |
| <span data-ttu-id="34b16-3022">className</span><span class="sxs-lookup"><span data-stu-id="34b16-3022">className</span></span> | <span data-ttu-id="34b16-3023">Belangrijkste Java/Spark-klasse van de toepassing</span><span class="sxs-lookup"><span data-stu-id="34b16-3023">Application's Java/Spark main class</span></span> | <span data-ttu-id="34b16-3024">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-3024">No</span></span> | 
| <span data-ttu-id="34b16-3025">Argumenten</span><span class="sxs-lookup"><span data-stu-id="34b16-3025">arguments</span></span> | <span data-ttu-id="34b16-3026">Een lijst met opdrachtregelargumenten toohello Spark programma.</span><span class="sxs-lookup"><span data-stu-id="34b16-3026">A list of command-line arguments toohello Spark program.</span></span> | <span data-ttu-id="34b16-3027">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-3027">No</span></span> | 
| <span data-ttu-id="34b16-3028">proxyUser</span><span class="sxs-lookup"><span data-stu-id="34b16-3028">proxyUser</span></span> | <span data-ttu-id="34b16-3029">Hallo account tooimpersonate tooexecute Hallo Spark programma door de gebruiker</span><span class="sxs-lookup"><span data-stu-id="34b16-3029">hello user account tooimpersonate tooexecute hello Spark program</span></span> | <span data-ttu-id="34b16-3030">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-3030">No</span></span> | 
| <span data-ttu-id="34b16-3031">sparkConfig</span><span class="sxs-lookup"><span data-stu-id="34b16-3031">sparkConfig</span></span> | <span data-ttu-id="34b16-3032">Configuratie-eigenschappen van Spark.</span><span class="sxs-lookup"><span data-stu-id="34b16-3032">Spark configuration properties.</span></span> | <span data-ttu-id="34b16-3033">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-3033">No</span></span> | 
| <span data-ttu-id="34b16-3034">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="34b16-3034">getDebugInfo</span></span> | <span data-ttu-id="34b16-3035">Geeft aan wanneer Hallo Spark logboekbestanden gekopieerde toohello Azure-opslag die wordt gebruikt door HDInsight-cluster zijn (of) opgegeven door sparkJobLinkedService.</span><span class="sxs-lookup"><span data-stu-id="34b16-3035">Specifies when hello Spark log files are copied toohello Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span></span> <span data-ttu-id="34b16-3036">Toegestane waarden: None, altijd of fout.</span><span class="sxs-lookup"><span data-stu-id="34b16-3036">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="34b16-3037">Standaardwaarde: geen.</span><span class="sxs-lookup"><span data-stu-id="34b16-3037">Default value: None.</span></span> | <span data-ttu-id="34b16-3038">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-3038">No</span></span> | 
| <span data-ttu-id="34b16-3039">sparkJobLinkedService</span><span class="sxs-lookup"><span data-stu-id="34b16-3039">sparkJobLinkedService</span></span> | <span data-ttu-id="34b16-3040">Hallo gekoppelde Azure Storage-service die Hallo Spark taakbestand, afhankelijkheden en Logboeken bevat.</span><span class="sxs-lookup"><span data-stu-id="34b16-3040">hello Azure Storage linked service that holds hello Spark job file, dependencies, and logs.</span></span>  <span data-ttu-id="34b16-3041">Als u een waarde op voor deze eigenschap niet opgeeft, wordt Hallo opslag die is gekoppeld aan de HDInsight-cluster gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-3041">If you do not specify a value for this property, hello storage associated with HDInsight cluster is used.</span></span> | <span data-ttu-id="34b16-3042">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-3042">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="34b16-3043">JSON-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-3043">JSON example</span></span>

```json
{
    "name": "SparkPipeline",
    "properties": {
        "activities": [
            {
                "type": "HDInsightSpark",
                "typeProperties": {
                    "rootPath": "adfspark\\pyFiles",
                    "entryFilePath": "test.py",
                    "getDebugInfo": "Always"
                },
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ],
                "name": "MySparkActivity",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-05T00:00:00",
        "end": "2017-02-06T00:00:00"
    }
}
```
<span data-ttu-id="34b16-3044">Houd er rekening mee Hallo volgende punten:</span><span class="sxs-lookup"><span data-stu-id="34b16-3044">Note hello following points:</span></span> 

- <span data-ttu-id="34b16-3045">Hallo **type** eigenschap is ingesteld, te**HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="34b16-3045">hello **type** property is set too**HDInsightSpark**.</span></span>
- <span data-ttu-id="34b16-3046">Hallo **rootPath** te is ingesteld,**adfspark\\pyFiles** waarbij adfspark hello Azure Blob-container en pyFiles is map in de container.</span><span class="sxs-lookup"><span data-stu-id="34b16-3046">hello **rootPath** is set too**adfspark\\pyFiles** where adfspark is hello Azure Blob container and pyFiles is fine folder in that container.</span></span> <span data-ttu-id="34b16-3047">In dit voorbeeld is hello Azure Blob Storage Hallo die is gekoppeld aan Hallo Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="34b16-3047">In this example, hello Azure Blob Storage is hello one that is associated with hello Spark cluster.</span></span> <span data-ttu-id="34b16-3048">U kunt uploaden Hallo bestand tooa andere Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="34b16-3048">You can upload hello file tooa different Azure Storage.</span></span> <span data-ttu-id="34b16-3049">Als u doet dit, wordt een gekoppelde Azure Storage-service toolink die storage account toohello een gegevensfactory maken.</span><span class="sxs-lookup"><span data-stu-id="34b16-3049">If you do so, create an Azure Storage linked service toolink that storage account toohello data factory.</span></span> <span data-ttu-id="34b16-3050">Hallo-naam van gekoppelde Hallo-service vervolgens opgeven als een waarde voor Hallo **sparkJobLinkedService** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="34b16-3050">Then, specify hello name of hello linked service as a value for hello **sparkJobLinkedService** property.</span></span> <span data-ttu-id="34b16-3051">Zie [Spark activiteitseigenschappen](#spark-activity-properties) voor meer informatie over deze eigenschap en andere eigenschappen die ondersteund worden door Hallo Spark-activiteit.</span><span class="sxs-lookup"><span data-stu-id="34b16-3051">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by hello Spark Activity.</span></span>
- <span data-ttu-id="34b16-3052">Hallo **entryFilePath** toohello is ingesteld **test.py**, namelijk Hallo python-bestand.</span><span class="sxs-lookup"><span data-stu-id="34b16-3052">hello **entryFilePath** is set toohello **test.py**, which is hello python file.</span></span> 
- <span data-ttu-id="34b16-3053">Hallo **getDebugInfo** eigenschap is ingesteld, te**altijd**, wat betekent dat het Hallo-logboekbestanden zijn altijd gegenereerd (slagen of mislukken).</span><span class="sxs-lookup"><span data-stu-id="34b16-3053">hello **getDebugInfo** property is set too**Always**, which means hello log files are always generated (success or failure).</span></span>  

    > [!IMPORTANT]
    > <span data-ttu-id="34b16-3054">U kunt het beste instellen de tooAlways van deze eigenschap niet in een productieomgeving tenzij u een probleem wilt oplossen.</span><span class="sxs-lookup"><span data-stu-id="34b16-3054">We recommend that you do not set this property tooAlways in a production environment unless you are troubleshooting an issue.</span></span> 
- <span data-ttu-id="34b16-3055">Hallo **levert** sectie heeft één uitvoergegevensset.</span><span class="sxs-lookup"><span data-stu-id="34b16-3055">hello **outputs** section has one output dataset.</span></span> <span data-ttu-id="34b16-3056">U kunt een uitvoergegevensset moet opgeven, zelfs als Hallo spark programma geen uitvoer produceert.</span><span class="sxs-lookup"><span data-stu-id="34b16-3056">You must specify an output dataset even if hello spark program does not produce any output.</span></span> <span data-ttu-id="34b16-3057">Hallo output dataset stations Hallo planning voor Hallo pijplijn (elk uur, dagelijks, enz.).</span><span class="sxs-lookup"><span data-stu-id="34b16-3057">hello output dataset drives hello schedule for hello pipeline (hourly, daily, etc.).</span></span>

<span data-ttu-id="34b16-3058">Zie voor meer informatie over de activiteit Hallo [Spark activiteit](data-factory-spark.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-3058">For more information about hello activity, see [Spark Activity](data-factory-spark.md) article.</span></span>  

## <a name="machine-learning-batch-execution-activity"></a><span data-ttu-id="34b16-3059">Machine Learning-batchuitvoeringsactiviteit</span><span class="sxs-lookup"><span data-stu-id="34b16-3059">Machine Learning Batch Execution Activity</span></span>
<span data-ttu-id="34b16-3060">Kunt u de volgende eigenschappen in de definitie van een Azure ML-Batch uitvoering activiteit JSON Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="34b16-3060">You can specify hello following properties in a Azure ML Batch Execution Activity JSON definition.</span></span> <span data-ttu-id="34b16-3061">eigenschap voor het type voor activiteit Hallo Hallo moet zijn: **AzureMLBatchExecution**.</span><span class="sxs-lookup"><span data-stu-id="34b16-3061">hello type property for hello activity must be: **AzureMLBatchExecution**.</span></span> <span data-ttu-id="34b16-3062">Moet u een Azure Machine Learning gekoppelde service eerst maakt en Hallo-naam van dit opgeven als een waarde voor Hallo **linkedServiceName** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="34b16-3062">You must create a Azure Machine Learning linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="34b16-3063">Hallo volgende eigenschappen worden ondersteund in Hallo **typeProperties** sectie bij het instellen van het soort activiteit tooAzureMLBatchExecution Hallo:</span><span class="sxs-lookup"><span data-stu-id="34b16-3063">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooAzureMLBatchExecution:</span></span>

<span data-ttu-id="34b16-3064">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-3064">Property</span></span> | <span data-ttu-id="34b16-3065">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-3065">Description</span></span> | <span data-ttu-id="34b16-3066">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-3066">Required</span></span> 
-------- | ----------- | --------
<span data-ttu-id="34b16-3067">webServiceInput</span><span class="sxs-lookup"><span data-stu-id="34b16-3067">webServiceInput</span></span> | <span data-ttu-id="34b16-3068">Hallo gegevensset toobe doorgegeven als invoer voor hello Azure ML webservice.</span><span class="sxs-lookup"><span data-stu-id="34b16-3068">hello dataset toobe passed as an input for hello Azure ML web service.</span></span> <span data-ttu-id="34b16-3069">Deze gegevensset moet ook zijn opgenomen in de invoer voor de activiteit Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="34b16-3069">This dataset must also be included in hello inputs for hello activity.</span></span> |<span data-ttu-id="34b16-3070">WebServiceInput of webServiceInputs gebruiken.</span><span class="sxs-lookup"><span data-stu-id="34b16-3070">Use either webServiceInput or webServiceInputs.</span></span> | 
<span data-ttu-id="34b16-3071">webServiceInputs</span><span class="sxs-lookup"><span data-stu-id="34b16-3071">webServiceInputs</span></span> | <span data-ttu-id="34b16-3072">Geef gegevenssets toobe doorgegeven als invoer voor hello Azure ML webservice.</span><span class="sxs-lookup"><span data-stu-id="34b16-3072">Specify datasets toobe passed as inputs for hello Azure ML web service.</span></span> <span data-ttu-id="34b16-3073">Als webservice Hallo meerdere invoer neemt, moet u Hallo webServiceInputs eigenschap gebruiken in plaats van Hallo webServiceInput eigenschap.</span><span class="sxs-lookup"><span data-stu-id="34b16-3073">If hello web service takes multiple inputs, use hello webServiceInputs property instead of using hello webServiceInput property.</span></span> <span data-ttu-id="34b16-3074">Gegevenssets waarnaar wordt verwezen door Hallo **webServiceInputs** moet ook zijn opgenomen in Hallo activiteit **invoer**.</span><span class="sxs-lookup"><span data-stu-id="34b16-3074">Datasets that are referenced by hello **webServiceInputs** must also be included in hello Activity **inputs**.</span></span> | <span data-ttu-id="34b16-3075">WebServiceInput of webServiceInputs gebruiken.</span><span class="sxs-lookup"><span data-stu-id="34b16-3075">Use either webServiceInput or webServiceInputs.</span></span> | 
<span data-ttu-id="34b16-3076">webServiceOutputs</span><span class="sxs-lookup"><span data-stu-id="34b16-3076">webServiceOutputs</span></span> | <span data-ttu-id="34b16-3077">Hallo gegevenssets die zijn toegewezen als uitvoer voor hello Azure ML-webservice.</span><span class="sxs-lookup"><span data-stu-id="34b16-3077">hello datasets that are assigned as outputs for hello Azure ML web service.</span></span> <span data-ttu-id="34b16-3078">Hallo-webservice retourneert uitvoergegevens in deze dataset.</span><span class="sxs-lookup"><span data-stu-id="34b16-3078">hello web service returns output data in this dataset.</span></span> | <span data-ttu-id="34b16-3079">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-3079">Yes</span></span> | 
<span data-ttu-id="34b16-3080">globalParameters</span><span class="sxs-lookup"><span data-stu-id="34b16-3080">globalParameters</span></span> | <span data-ttu-id="34b16-3081">Geef waarden voor Hallo web serviceparameters in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="34b16-3081">Specify values for hello web service parameters in this section.</span></span> | <span data-ttu-id="34b16-3082">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-3082">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="34b16-3083">JSON-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-3083">JSON example</span></span>
<span data-ttu-id="34b16-3084">In dit voorbeeld heeft Hallo activiteit Hallo gegevensset **MLSqlInput** als invoer en **MLSqlOutput** als Hallo uitvoer.</span><span class="sxs-lookup"><span data-stu-id="34b16-3084">In this example, hello activity has hello dataset **MLSqlInput** as input and **MLSqlOutput** as hello output.</span></span> <span data-ttu-id="34b16-3085">Hallo **MLSqlInput** is doorgegeven als een webservice van invoer toohello door Hallo met **webServiceInput** JSON-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="34b16-3085">hello **MLSqlInput** is passed as an input toohello web service by using hello **webServiceInput** JSON property.</span></span> <span data-ttu-id="34b16-3086">Hallo **MLSqlOutput** wordt doorgegeven als uitvoer toohello webservice door met de Hallo **webServiceOutputs** JSON-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="34b16-3086">hello **MLSqlOutput** is passed as an output toohello Web service by using hello **webServiceOutputs** JSON property.</span></span> 

```json
{
   "name": "MLWithSqlReaderSqlWriter",
   "properties": {
      "description": "Azure ML model with sql azure reader/writer",
      "activities": [{
         "name": "MLSqlReaderSqlWriterActivity",
         "type": "AzureMLBatchExecution",
         "description": "test",
         "inputs": [ { "name": "MLSqlInput" }],
         "outputs": [ { "name": "MLSqlOutput" } ],
         "linkedServiceName": "MLSqlReaderSqlWriterDecisionTreeModel",
         "typeProperties":
         {
            "webServiceInput": "MLSqlInput",
            "webServiceOutputs": {
               "output1": "MLSqlOutput"
            },
            "globalParameters": {
               "Database server name": "<myserver>.database.windows.net",
               "Database name": "<database>",
               "Server user account name": "<user name>",
               "Server user account password": "<password>"
            }              
         },
         "policy": {
            "concurrency": 1,
            "executionPriorityOrder": "NewestFirst",
            "retry": 1,
            "timeout": "02:00:00"
         }
      }],
      "start": "2016-02-13T00:00:00",
       "end": "2016-02-14T00:00:00"
   }
}
```

<span data-ttu-id="34b16-3087">In Hallo JSON voorbeeld hello Azure Machine Learning Web service een lezer en een writer module tooread/gegevens schrijven van gebruikt geïmplementeerd / tooan Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="34b16-3087">In hello JSON example, hello deployed Azure Machine Learning Web service uses a reader and a writer module tooread/write data from/tooan Azure SQL Database.</span></span> <span data-ttu-id="34b16-3088">Deze webservice beschrijft Hallo na vier parameters: servernaam, databasenaam, servergebruikersnaam en wachtwoord voor gebruikersaccount Server-Database.</span><span class="sxs-lookup"><span data-stu-id="34b16-3088">This Web service exposes hello following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span></span>

> [!NOTE]
> <span data-ttu-id="34b16-3089">Alleen invoer en uitvoer van Hallo AzureMLBatchExecution activiteit kunnen worden doorgegeven als parameters toohello webservice.</span><span class="sxs-lookup"><span data-stu-id="34b16-3089">Only inputs and outputs of hello AzureMLBatchExecution activity can be passed as parameters toohello Web service.</span></span> <span data-ttu-id="34b16-3090">In Hallo hierboven JSON-codefragment is MLSqlInput bijvoorbeeld een invoer toohello AzureMLBatchExecution activiteit, die is doorgegeven als een invoer toohello webservice via webServiceInput-parameter.</span><span class="sxs-lookup"><span data-stu-id="34b16-3090">For example, in hello above JSON snippet, MLSqlInput is an input toohello AzureMLBatchExecution activity, which is passed as an input toohello Web service via webServiceInput parameter.</span></span>

## <a name="machine-learning-update-resource-activity"></a><span data-ttu-id="34b16-3091">Machine Learning-activiteit resources bijwerken</span><span class="sxs-lookup"><span data-stu-id="34b16-3091">Machine Learning Update Resource Activity</span></span>
<span data-ttu-id="34b16-3092">Kunt u de volgende eigenschappen in de definitie van een Azure ML Update Resource activiteit JSON Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="34b16-3092">You can specify hello following properties in a Azure ML Update Resource Activity JSON definition.</span></span> <span data-ttu-id="34b16-3093">eigenschap voor het type voor activiteit Hallo Hallo moet zijn: **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="34b16-3093">hello type property for hello activity must be: **AzureMLUpdateResource**.</span></span> <span data-ttu-id="34b16-3094">Moet u een Azure Machine Learning gekoppelde service eerst maakt en Hallo-naam van dit opgeven als een waarde voor Hallo **linkedServiceName** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="34b16-3094">You must create a Azure Machine Learning linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="34b16-3095">Hallo volgende eigenschappen worden ondersteund in Hallo **typeProperties** sectie bij het instellen van het soort activiteit tooAzureMLUpdateResource Hallo:</span><span class="sxs-lookup"><span data-stu-id="34b16-3095">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooAzureMLUpdateResource:</span></span>

<span data-ttu-id="34b16-3096">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-3096">Property</span></span> | <span data-ttu-id="34b16-3097">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-3097">Description</span></span> | <span data-ttu-id="34b16-3098">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-3098">Required</span></span> 
-------- | ----------- | --------
<span data-ttu-id="34b16-3099">trainedModelName</span><span class="sxs-lookup"><span data-stu-id="34b16-3099">trainedModelName</span></span> | <span data-ttu-id="34b16-3100">Naam van Hallo retrained model.</span><span class="sxs-lookup"><span data-stu-id="34b16-3100">Name of hello retrained model.</span></span> | <span data-ttu-id="34b16-3101">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-3101">Yes</span></span> |  
<span data-ttu-id="34b16-3102">trainedModelDatasetName</span><span class="sxs-lookup"><span data-stu-id="34b16-3102">trainedModelDatasetName</span></span> | <span data-ttu-id="34b16-3103">DataSet aanwijsapparaat toohello iLearner-bestand wordt geretourneerd door Hallo retraining bewerking.</span><span class="sxs-lookup"><span data-stu-id="34b16-3103">Dataset pointing toohello iLearner file returned by hello retraining operation.</span></span> | <span data-ttu-id="34b16-3104">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-3104">Yes</span></span> | 

### <a name="json-example"></a><span data-ttu-id="34b16-3105">JSON-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-3105">JSON example</span></span>
<span data-ttu-id="34b16-3106">Hallo pipeline heeft twee activiteiten: **AzureMLBatchExecution** en **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="34b16-3106">hello pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span></span> <span data-ttu-id="34b16-3107">Hello Azure ML-Batchuitvoering activiteit duurt Hallo trainingsgegevens als invoer en een iLearner-bestand als uitvoer produceert.</span><span class="sxs-lookup"><span data-stu-id="34b16-3107">hello Azure ML Batch Execution activity takes hello training data as input and produces an iLearner file as an output.</span></span> <span data-ttu-id="34b16-3108">Hallo activiteit roept Hallo training webservice (trainingsexperiment weergegeven als een webservice) met Hallo invoer trainen van gegevens en Hallo ilearner-bestand van de webservice Hallo ontvangt.</span><span class="sxs-lookup"><span data-stu-id="34b16-3108">hello activity invokes hello training web service (training experiment exposed as a web service) with hello input training data and receives hello ilearner file from hello webservice.</span></span> <span data-ttu-id="34b16-3109">Hallo placeholderBlob is een dummy output dataset is vereist door hello Azure Data Factory-service toorun Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="34b16-3109">hello placeholderBlob is just a dummy output dataset that is required by hello Azure Data Factory service toorun hello pipeline.</span></span>


```json
{
    "name": "pipeline",
    "properties": {
        "activities": [
            {
                "name": "retraining",
                "type": "AzureMLBatchExecution",
                "inputs": [
                    {
                        "name": "trainingData"
                    }
                ],
                "outputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "typeProperties": {
                    "webServiceInput": "trainingData",
                    "webServiceOutputs": {
                        "output1": "trainedModelBlob"
                    }              
                 },
                "linkedServiceName": "trainingEndpoint",
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            },
            {
                "type": "AzureMLUpdateResource",
                "typeProperties": {
                    "trainedModelName": "trained model",
                    "trainedModelDatasetName" :  "trainedModelBlob"
                },
                "inputs": [{ "name": "trainedModelBlob" }],
                "outputs": [{ "name": "placeholderBlob" }],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "AzureML Update Resource",
                "linkedServiceName": "updatableScoringEndpoint2"
            }
        ],
        "start": "2016-02-13T00:00:00",
        "end": "2016-02-14T00:00:00"
    }
}
```

## <a name="data-lake-analytics-u-sql-activity"></a><span data-ttu-id="34b16-3110">Data Lake Analytics U-SQL-activiteit</span><span class="sxs-lookup"><span data-stu-id="34b16-3110">Data Lake Analytics U-SQL Activity</span></span>
<span data-ttu-id="34b16-3111">Kunt u de volgende eigenschappen in de definitie van een U-SQL-activiteit JSON Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="34b16-3111">You can specify hello following properties in a U-SQL Activity JSON definition.</span></span> <span data-ttu-id="34b16-3112">eigenschap voor het type voor activiteit Hallo Hallo moet zijn: **DataLakeAnalyticsU SQL**.</span><span class="sxs-lookup"><span data-stu-id="34b16-3112">hello type property for hello activity must be: **DataLakeAnalyticsU-SQL**.</span></span> <span data-ttu-id="34b16-3113">Moet u een Azure Data Lake Analytics gekoppelde service maken en Hallo-naam van dit opgeven als een waarde voor Hallo **linkedServiceName** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="34b16-3113">You must create an Azure Data Lake Analytics linked service and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="34b16-3114">Hallo volgende eigenschappen worden ondersteund in Hallo **typeProperties** sectie bij het instellen van Hallo type activiteit tooDataLakeAnalyticsU-SQL:</span><span class="sxs-lookup"><span data-stu-id="34b16-3114">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooDataLakeAnalyticsU-SQL:</span></span> 

| <span data-ttu-id="34b16-3115">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-3115">Property</span></span> | <span data-ttu-id="34b16-3116">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-3116">Description</span></span> | <span data-ttu-id="34b16-3117">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-3117">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="34b16-3118">scriptPath</span><span class="sxs-lookup"><span data-stu-id="34b16-3118">scriptPath</span></span> |<span data-ttu-id="34b16-3119">Pad toofolder met Hallo U-SQL-script.</span><span class="sxs-lookup"><span data-stu-id="34b16-3119">Path toofolder that contains hello U-SQL script.</span></span> <span data-ttu-id="34b16-3120">Naam van bestand Hallo is hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="34b16-3120">Name of hello file is case-sensitive.</span></span> |<span data-ttu-id="34b16-3121">Nee (als u een script gebruiken)</span><span class="sxs-lookup"><span data-stu-id="34b16-3121">No (if you use script)</span></span> |
| <span data-ttu-id="34b16-3122">scriptLinkedService</span><span class="sxs-lookup"><span data-stu-id="34b16-3122">scriptLinkedService</span></span> |<span data-ttu-id="34b16-3123">Gekoppelde service die is gekoppeld aan Hallo-opslag met Hallo script toohello data factory</span><span class="sxs-lookup"><span data-stu-id="34b16-3123">Linked service that links hello storage that contains hello script toohello data factory</span></span> |<span data-ttu-id="34b16-3124">Nee (als u een script gebruiken)</span><span class="sxs-lookup"><span data-stu-id="34b16-3124">No (if you use script)</span></span> |
| <span data-ttu-id="34b16-3125">Script</span><span class="sxs-lookup"><span data-stu-id="34b16-3125">script</span></span> |<span data-ttu-id="34b16-3126">Geef in plaats van het opgeven van scriptPath en scriptLinkedService inline-script.</span><span class="sxs-lookup"><span data-stu-id="34b16-3126">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span></span> <span data-ttu-id="34b16-3127">Bijvoorbeeld: 'script': 'Test DATABASE maken'.</span><span class="sxs-lookup"><span data-stu-id="34b16-3127">For example: "script": "CREATE DATABASE test".</span></span> |<span data-ttu-id="34b16-3128">Nee (als u scriptPath en scriptLinkedService gebruiken)</span><span class="sxs-lookup"><span data-stu-id="34b16-3128">No (if you use scriptPath and scriptLinkedService)</span></span> |
| <span data-ttu-id="34b16-3129">degreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="34b16-3129">degreeOfParallelism</span></span> |<span data-ttu-id="34b16-3130">maximum aantal knooppunten Hallo toorun Hallo taak tegelijkertijd worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-3130">hello maximum number of nodes simultaneously used toorun hello job.</span></span> |<span data-ttu-id="34b16-3131">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-3131">No</span></span> |
| <span data-ttu-id="34b16-3132">Prioriteit</span><span class="sxs-lookup"><span data-stu-id="34b16-3132">priority</span></span> |<span data-ttu-id="34b16-3133">Hiermee wordt bepaald welke taken uit in de wachtrij moeten geselecteerde toorun eerst.</span><span class="sxs-lookup"><span data-stu-id="34b16-3133">Determines which jobs out of all that are queued should be selected toorun first.</span></span> <span data-ttu-id="34b16-3134">Hallo Hallo minder, Hallo hogere Hallo prioriteit.</span><span class="sxs-lookup"><span data-stu-id="34b16-3134">hello lower hello number, hello higher hello priority.</span></span> |<span data-ttu-id="34b16-3135">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-3135">No</span></span> |
| <span data-ttu-id="34b16-3136">parameters</span><span class="sxs-lookup"><span data-stu-id="34b16-3136">parameters</span></span> |<span data-ttu-id="34b16-3137">Parameters voor Hallo U-SQL-script</span><span class="sxs-lookup"><span data-stu-id="34b16-3137">Parameters for hello U-SQL script</span></span> |<span data-ttu-id="34b16-3138">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-3138">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="34b16-3139">JSON-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-3139">JSON example</span></span>

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This pipeline computes events for en-gb locale and date less than Feb 19, 2012.",
        "activities": 
        [
            {
                "type": "DataLakeAnalyticsU-SQL",
                "typeProperties": {
                    "scriptPath": "scripts\\kona\\SearchLogProcessing.txt",
                    "scriptLinkedService": "StorageLinkedService",
                    "degreeOfParallelism": 3,
                    "priority": 100,
                    "parameters": {
                        "in": "/datalake/input/SearchLog.tsv",
                        "out": "/datalake/output/Result.tsv"
                    }
                },
                "inputs": [
                    {
                        "name": "DataLakeTable"
                    }
                ],
                "outputs": 
                [
                    {
                        "name": "EventsByRegionTable"
                    }
                ],
                "policy": {
                    "timeout": "06:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "EventsByRegion",
                "linkedServiceName": "AzureDataLakeAnalyticsLinkedService"
            }
        ],
        "start": "2015-08-08T00:00:00",
        "end": "2015-08-08T01:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="34b16-3140">Zie voor meer informatie [Data Lake Analytics U-SQL-activiteit](data-factory-usql-activity.md).</span><span class="sxs-lookup"><span data-stu-id="34b16-3140">For more information, see [Data Lake Analytics U-SQL Activity](data-factory-usql-activity.md).</span></span> 

## <a name="stored-procedure-activity"></a><span data-ttu-id="34b16-3141">Opgeslagen procedureactiviteit</span><span class="sxs-lookup"><span data-stu-id="34b16-3141">Stored Procedure Activity</span></span>
<span data-ttu-id="34b16-3142">U kunt Hallo volgende eigenschappen in een opgeslagen Procedure activiteit JSON-definitie opgeven.</span><span class="sxs-lookup"><span data-stu-id="34b16-3142">You can specify hello following properties in a Stored Procedure Activity JSON definition.</span></span> <span data-ttu-id="34b16-3143">eigenschap voor het type voor activiteit Hallo Hallo moet zijn: **SqlServerStoredProcedure**.</span><span class="sxs-lookup"><span data-stu-id="34b16-3143">hello type property for hello activity must be: **SqlServerStoredProcedure**.</span></span> <span data-ttu-id="34b16-3144">U moet een een Hallo na gekoppelde services maken en Hallo naam opgeven van Hallo gekoppelde service als een waarde voor Hallo **linkedServiceName** eigenschap:</span><span class="sxs-lookup"><span data-stu-id="34b16-3144">You must create an one of hello following linked services and specify hello name of hello linked service as a value for hello **linkedServiceName** property:</span></span>

- <span data-ttu-id="34b16-3145">SQL Server</span><span class="sxs-lookup"><span data-stu-id="34b16-3145">SQL Server</span></span> 
- <span data-ttu-id="34b16-3146">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="34b16-3146">Azure SQL Database</span></span>
- <span data-ttu-id="34b16-3147">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="34b16-3147">Azure SQL Data Warehouse</span></span>

<span data-ttu-id="34b16-3148">Hallo volgende eigenschappen worden ondersteund in Hallo **typeProperties** sectie bij het instellen van het soort activiteit tooSqlServerStoredProcedure Hallo:</span><span class="sxs-lookup"><span data-stu-id="34b16-3148">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooSqlServerStoredProcedure:</span></span>

| <span data-ttu-id="34b16-3149">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-3149">Property</span></span> | <span data-ttu-id="34b16-3150">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-3150">Description</span></span> | <span data-ttu-id="34b16-3151">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-3151">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="34b16-3152">storedProcedureName</span><span class="sxs-lookup"><span data-stu-id="34b16-3152">storedProcedureName</span></span> |<span data-ttu-id="34b16-3153">Hallo naam opgeven van Hallo opgeslagen procedure in hello Azure SQL database- of Azure SQL Data Warehouse die wordt vertegenwoordigd door Hallo gekoppelde service die Hallo uitvoer tabel gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34b16-3153">Specify hello name of hello stored procedure in hello Azure SQL database or Azure SQL Data Warehouse that is represented by hello linked service that hello output table uses.</span></span> |<span data-ttu-id="34b16-3154">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-3154">Yes</span></span> |
| <span data-ttu-id="34b16-3155">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="34b16-3155">storedProcedureParameters</span></span> |<span data-ttu-id="34b16-3156">Geef waarden op voor parameters van opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="34b16-3156">Specify values for stored procedure parameters.</span></span> <span data-ttu-id="34b16-3157">Als u toopass null voor een parameter moet, Hallo syntaxis gebruiken: "param1": null (alle kleine letter).</span><span class="sxs-lookup"><span data-stu-id="34b16-3157">If you need toopass null for a parameter, use hello syntax: "param1": null (all lower case).</span></span> <span data-ttu-id="34b16-3158">Zie Hallo toolearn voorbeeld over het gebruik van deze eigenschap te volgen.</span><span class="sxs-lookup"><span data-stu-id="34b16-3158">See hello following sample toolearn about using this property.</span></span> |<span data-ttu-id="34b16-3159">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-3159">No</span></span> |

<span data-ttu-id="34b16-3160">Als u een invoergegevensset opgeeft, moet dit beschikbaar is (in de status 'Gereed') voor Hallo opgeslagen procedure activiteit toorun.</span><span class="sxs-lookup"><span data-stu-id="34b16-3160">If you do specify an input dataset, it must be available (in ‘Ready’ status) for hello stored procedure activity toorun.</span></span> <span data-ttu-id="34b16-3161">Hallo invoergegevensset kan niet worden gebruikt in Hallo opgeslagen procedure als een parameter.</span><span class="sxs-lookup"><span data-stu-id="34b16-3161">hello input dataset cannot be consumed in hello stored procedure as a parameter.</span></span> <span data-ttu-id="34b16-3162">Het is alleen gebruikte toocheck Hallo afhankelijkheid voordat begin Hallo procedure-activiteit opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="34b16-3162">It is only used toocheck hello dependency before starting hello stored procedure activity.</span></span> <span data-ttu-id="34b16-3163">U moet een uitvoergegevensset voor een activiteit opgeslagen procedure opgeven.</span><span class="sxs-lookup"><span data-stu-id="34b16-3163">You must specify an output dataset for a stored procedure activity.</span></span> 

<span data-ttu-id="34b16-3164">Uitvoergegevensset geeft Hallo **planning** voor Hallo opgeslagen procedure activiteit (elk uur, wekelijks, maandelijks, enzovoort).</span><span class="sxs-lookup"><span data-stu-id="34b16-3164">Output dataset specifies hello **schedule** for hello stored procedure activity (hourly, weekly, monthly, etc.).</span></span> <span data-ttu-id="34b16-3165">Hallo uitvoergegevensset moet gebruiken een **gekoppelde service** die tooan Azure SQL Database of een Azure SQL Data Warehouse of een SQL Server-Database die u wilt opgeslagen procedure toorun Hallo verwijst.</span><span class="sxs-lookup"><span data-stu-id="34b16-3165">hello output dataset must use a **linked service** that refers tooan Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want hello stored procedure toorun.</span></span> <span data-ttu-id="34b16-3166">Hallo uitvoergegevensset kan fungeren als een manier toopass Hallo resultaat van Hallo opgeslagen procedure voor verdere verwerking door een andere activiteit ([activiteiten chaining](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) in de pijplijn Hallo.</span><span class="sxs-lookup"><span data-stu-id="34b16-3166">hello output dataset can serve as a way toopass hello result of hello stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) in hello pipeline.</span></span> <span data-ttu-id="34b16-3167">Data Factory biedt Hallo-uitvoer van een gegevensset met de opgeslagen procedure toothis echter automatisch niet schrijven.</span><span class="sxs-lookup"><span data-stu-id="34b16-3167">However, Data Factory does not automatically write hello output of a stored procedure toothis dataset.</span></span> <span data-ttu-id="34b16-3168">Het is Hallo opgeslagen procedure dat SQL-tabel voor schrijfbewerkingen tooa Hallo uitvoer gegevensset verwijst naar.</span><span class="sxs-lookup"><span data-stu-id="34b16-3168">It is hello stored procedure that writes tooa SQL table that hello output dataset points to.</span></span> <span data-ttu-id="34b16-3169">In sommige gevallen Hallo uitvoergegevensset mag een **dummy gegevensset**, waarmee alleen toospecify Hallo schema voor het uitvoeren van Hallo procedure-activiteit opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="34b16-3169">In some cases, hello output dataset can be a **dummy dataset**, which is used only toospecify hello schedule for running hello stored procedure activity.</span></span>  

### <a name="json-example"></a><span data-ttu-id="34b16-3170">JSON-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-3170">JSON example</span></span>

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
                "outputs": [{ "name": "sprocsampleout" }],
                "name": "SprocActivitySample"
            }
        ],
         "start": "2016-08-02T00:00:00",
         "end": "2016-08-02T05:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="34b16-3171">Zie voor meer informatie [activiteit opgeslagen Procedure](data-factory-stored-proc-activity.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-3171">For more information, see [Stored Procedure Activity](data-factory-stored-proc-activity.md) article.</span></span> 

## <a name="net-custom-activity"></a><span data-ttu-id="34b16-3172">Aangepaste .NET-activiteit</span><span class="sxs-lookup"><span data-stu-id="34b16-3172">.NET custom activity</span></span>
<span data-ttu-id="34b16-3173">U kunt Hallo volgende eigenschappen in een aangepaste activiteit .NET JSON-definitie opgeven.</span><span class="sxs-lookup"><span data-stu-id="34b16-3173">You can specify hello following properties in a .NET custom activity JSON definition.</span></span> <span data-ttu-id="34b16-3174">eigenschap voor het type voor activiteit Hallo Hallo moet zijn: **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="34b16-3174">hello type property for hello activity must be: **DotNetActivity**.</span></span> <span data-ttu-id="34b16-3175">Moet u een gekoppelde HDInsight-service maken of een Azure Batch gekoppelde service en Hallo-naam van Hallo gekoppelde service opgeven als een waarde voor Hallo **linkedServiceName** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="34b16-3175">You must create an Azure HDInsight linked service or an Azure Batch linked service, and specify hello name of hello linked service as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="34b16-3176">Hallo volgende eigenschappen worden ondersteund in Hallo **typeProperties** sectie bij het instellen van het soort activiteit tooDotNetActivity Hallo:</span><span class="sxs-lookup"><span data-stu-id="34b16-3176">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooDotNetActivity:</span></span>
 
| <span data-ttu-id="34b16-3177">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="34b16-3177">Property</span></span> | <span data-ttu-id="34b16-3178">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34b16-3178">Description</span></span> | <span data-ttu-id="34b16-3179">Vereist</span><span class="sxs-lookup"><span data-stu-id="34b16-3179">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="34b16-3180">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="34b16-3180">AssemblyName</span></span> | <span data-ttu-id="34b16-3181">Naam van assembly Hallo.</span><span class="sxs-lookup"><span data-stu-id="34b16-3181">Name of hello assembly.</span></span> <span data-ttu-id="34b16-3182">In voorbeeld Hallo is: **MyDotnetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="34b16-3182">In hello example, it is: **MyDotnetActivity.dll**.</span></span> | <span data-ttu-id="34b16-3183">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-3183">Yes</span></span> |
| <span data-ttu-id="34b16-3184">EntryPoint</span><span class="sxs-lookup"><span data-stu-id="34b16-3184">EntryPoint</span></span> |<span data-ttu-id="34b16-3185">Naam van het Hallo-klasse die Hallo IDotNetActivity interface implementeert.</span><span class="sxs-lookup"><span data-stu-id="34b16-3185">Name of hello class that implements hello IDotNetActivity interface.</span></span> <span data-ttu-id="34b16-3186">In voorbeeld Hallo is: **MyDotNetActivityNS.MyDotNetActivity** waarbij MyDotNetActivityNS Hallo-naamruimte en MyDotNetActivity Hallo-klasse.</span><span class="sxs-lookup"><span data-stu-id="34b16-3186">In hello example, it is: **MyDotNetActivityNS.MyDotNetActivity** where MyDotNetActivityNS is hello namespace and MyDotNetActivity is hello class.</span></span>  | <span data-ttu-id="34b16-3187">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-3187">Yes</span></span> | 
| <span data-ttu-id="34b16-3188">PackageLinkedService</span><span class="sxs-lookup"><span data-stu-id="34b16-3188">PackageLinkedService</span></span> | <span data-ttu-id="34b16-3189">Naam van Hallo gekoppelde Azure Storage-service die toohello blob-opslag met Hallo aangepaste activiteit zip-bestand verwijst.</span><span class="sxs-lookup"><span data-stu-id="34b16-3189">Name of hello Azure Storage linked service that points toohello blob storage that contains hello custom activity zip file.</span></span> <span data-ttu-id="34b16-3190">In voorbeeld Hallo is: **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="34b16-3190">In hello example, it is: **AzureStorageLinkedService**.</span></span>| <span data-ttu-id="34b16-3191">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-3191">Yes</span></span> |
| <span data-ttu-id="34b16-3192">PackageFile</span><span class="sxs-lookup"><span data-stu-id="34b16-3192">PackageFile</span></span> | <span data-ttu-id="34b16-3193">Naam van Hallo zip-bestand.</span><span class="sxs-lookup"><span data-stu-id="34b16-3193">Name of hello zip file.</span></span> <span data-ttu-id="34b16-3194">In voorbeeld Hallo is: **customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="34b16-3194">In hello example, it is: **customactivitycontainer/MyDotNetActivity.zip**.</span></span> | <span data-ttu-id="34b16-3195">Ja</span><span class="sxs-lookup"><span data-stu-id="34b16-3195">Yes</span></span> |
| <span data-ttu-id="34b16-3196">extendedProperties</span><span class="sxs-lookup"><span data-stu-id="34b16-3196">extendedProperties</span></span> | <span data-ttu-id="34b16-3197">Uitgebreide eigenschappen die u kunt definiëren en geeft op toohello .NET-code.</span><span class="sxs-lookup"><span data-stu-id="34b16-3197">Extended properties that you can define and pass on toohello .NET code.</span></span> <span data-ttu-id="34b16-3198">In dit voorbeeld Hallo **SliceStart** variabele tooa-waarde op basis van Hallo SliceStart systeemvariabele is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="34b16-3198">In this example, hello **SliceStart** variable is set tooa value based on hello SliceStart system variable.</span></span> | <span data-ttu-id="34b16-3199">Nee</span><span class="sxs-lookup"><span data-stu-id="34b16-3199">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="34b16-3200">JSON-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="34b16-3200">JSON example</span></span>

```json
{
  "name": "ADFTutorialPipelineCustom",
  "properties": {
    "description": "Use custom activity",
    "activities": [
      {
        "Name": "MyDotNetActivity",
        "Type": "DotNetActivity",
        "Inputs": [
          {
            "Name": "InputDataset"
          }
        ],
        "Outputs": [
          {
            "Name": "OutputDataset"
          }
        ],
        "LinkedServiceName": "AzureBatchLinkedService",
        "typeProperties": {
          "AssemblyName": "MyDotNetActivity.dll",
          "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
          "PackageLinkedService": "AzureStorageLinkedService",
          "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
          "extendedProperties": {
            "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
          }
        },
        "Policy": {
          "Concurrency": 2,
          "ExecutionPriorityOrder": "OldestFirst",
          "Retry": 3,
          "Timeout": "00:30:00",
          "Delay": "00:00:00"
        }
      }
    ],
    "start": "2016-11-16T00:00:00",
    "end": "2016-11-16T05:00:00",
    "isPaused": false
  }
}
```

<span data-ttu-id="34b16-3201">Zie voor gedetailleerde informatie [gebruik van aangepaste activiteiten in de Data Factory](data-factory-use-custom-activities.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="34b16-3201">For detailed information, see [Use custom activities in Data Factory](data-factory-use-custom-activities.md) article.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="34b16-3202">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="34b16-3202">Next Steps</span></span>
<span data-ttu-id="34b16-3203">Zie de volgende zelfstudies Hallo:</span><span class="sxs-lookup"><span data-stu-id="34b16-3203">See hello following tutorials:</span></span> 

- [<span data-ttu-id="34b16-3204">Zelfstudie: een pijplijn maken met een kopieeractiviteit</span><span class="sxs-lookup"><span data-stu-id="34b16-3204">Tutorial: create a pipeline with a copy activity</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
- [<span data-ttu-id="34b16-3205">Zelfstudie: een pijplijn maken met een hive-activiteit</span><span class="sxs-lookup"><span data-stu-id="34b16-3205">Tutorial: create a pipeline with a hive activity</span></span>](data-factory-build-your-first-pipeline-using-editor.md)