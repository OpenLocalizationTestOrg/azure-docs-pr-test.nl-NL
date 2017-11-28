---
title: 'Snel aan de slag: Azure Machine Learning aanbevelingen API (versie 1) | Microsoft Docs'
description: Azure Machine Learning-aanbevelingen - snelstartgids
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 5bce1a4a-1ad6-473f-812b-84f800fdc09a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: d8f98e85f723a1104cb169b26d797934140979f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="quick-start-guide-for-hello-machine-learning-recommendations-api-version-1"></a><span data-ttu-id="2628f-104">Quick start guide voor Hallo Machine Learning aanbevelingen API (versie 1)</span><span class="sxs-lookup"><span data-stu-id="2628f-104">Quick start guide for hello Machine Learning Recommendations API (version 1)</span></span>

> [!NOTE]
> <span data-ttu-id="2628f-105">U moet beginnen met behulp van Hallo [cognitieve aanbevelingen API-Service](https://www.microsoft.com/cognitive-services/recommendations-api) in plaats van deze versie.</span><span class="sxs-lookup"><span data-stu-id="2628f-105">You should start using hello [Recommendations API Cognitive Service](https://www.microsoft.com/cognitive-services/recommendations-api) instead of this version.</span></span> <span data-ttu-id="2628f-106">Hallo aanbevelingen cognitieve Service vervangt deze service en alle nieuwe functies in Hallo er zal worden ontwikkeld.</span><span class="sxs-lookup"><span data-stu-id="2628f-106">hello Recommendations Cognitive Service will be replacing this service, and all hello new features will be developed there.</span></span> <span data-ttu-id="2628f-107">Heeft nieuwe mogelijkheden, zoals batchverwerking ondersteuning, beter API Explorer, een schonere API surface, consistente aanmelding/facturering ervaring, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="2628f-107">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
>
> <span data-ttu-id="2628f-108">Meer informatie over [migreren toohello nieuwe cognitieve Service](http://aka.ms/recomigrate).</span><span class="sxs-lookup"><span data-stu-id="2628f-108">Learn more about [Migrating toohello new Cognitive Service](http://aka.ms/recomigrate).</span></span>
> 
> 

<span data-ttu-id="2628f-109">Dit document wordt beschreven hoe tooonboard uw service of toepassing toouse aanbevelingen van Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="2628f-109">This document describes how tooonboard your service or application toouse Microsoft Azure Machine Learning Recommendations.</span></span> <span data-ttu-id="2628f-110">U vindt meer informatie op Hallo aanbevelingen API in Hallo [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2).</span><span class="sxs-lookup"><span data-stu-id="2628f-110">You can find more details on hello Recommendations API in hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="general-overview"></a><span data-ttu-id="2628f-111">Algemeen overzicht</span><span class="sxs-lookup"><span data-stu-id="2628f-111">General overview</span></span>
<span data-ttu-id="2628f-112">Azure Machine Learning aanbevelingen toouse, moet u tootake Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2628f-112">toouse Azure Machine Learning Recommendations, you need tootake hello following steps:</span></span>

* <span data-ttu-id="2628f-113">Een model maken: een model is een container van uw gegevens over het gebruik, catalogusgegevens en Hallo aanbeveling model.</span><span class="sxs-lookup"><span data-stu-id="2628f-113">Create a model - A model is a container of your usage data, catalog data, and hello recommendation model.</span></span>
* <span data-ttu-id="2628f-114">Gegevens importeren catalogus - een catalogus bevat informatie over de metagegevens op Hallo items.</span><span class="sxs-lookup"><span data-stu-id="2628f-114">Import catalog data - A catalog contains metadata information on hello items.</span></span> 
* <span data-ttu-id="2628f-115">Gebruiksgegevens importeren - gebruiksgegevens kunnen worden geüpload in twee manieren (of beide):</span><span class="sxs-lookup"><span data-stu-id="2628f-115">Import usage data - Usage data can be uploaded in one of two ways (or both):</span></span>
  * <span data-ttu-id="2628f-116">Door het uploaden van een bestand met gebruiksgegevens Hallo.</span><span class="sxs-lookup"><span data-stu-id="2628f-116">By uploading a file that contains hello usage data.</span></span>
  * <span data-ttu-id="2628f-117">Door het verzenden van gegevens overname gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="2628f-117">By sending data acquisition events.</span></span>
    <span data-ttu-id="2628f-118">Meestal u een bestand voor gebruik in volgorde toobe kunnen toocreate een eerste aanbeveling model (bootstrap) uploaden en deze gebruiken totdat Hallo systeem voldoende gegevens worden verzameld met behulp van Hallo overname gegevensindeling.</span><span class="sxs-lookup"><span data-stu-id="2628f-118">Usually you upload a usage file in order toobe able toocreate an initial recommendation model (bootstrap) and use it until hello system gathers enough data by using hello data acquisition format.</span></span>
* <span data-ttu-id="2628f-119">Een aanbeveling model bouwen: dit is een asynchrone bewerking in welke Hallo aanbeveling system neemt alle Hallo gebruiksgegevens en maakt een aanbeveling-model.</span><span class="sxs-lookup"><span data-stu-id="2628f-119">Build a recommendation model - This is an asynchronous operation in which hello recommendation system takes all hello usage data and creates a recommendation model.</span></span> <span data-ttu-id="2628f-120">Deze bewerking kan enkele minuten duren of enkele uren, afhankelijk van het Hallo-grootte van het Hallo-gegevens en Hallo configuratieparameters bouwen.</span><span class="sxs-lookup"><span data-stu-id="2628f-120">This operation can take several minutes or several hours depending on hello size of hello data and hello build configuration parameters.</span></span> <span data-ttu-id="2628f-121">Wanneer activering Hallo build, krijgt u een build-ID.</span><span class="sxs-lookup"><span data-stu-id="2628f-121">When triggering hello build, you will get a build ID.</span></span> <span data-ttu-id="2628f-122">Gebruik deze methode toocheck als Hallo build-proces is beëindigd voordat u begint tooconsume aanbevelingen.</span><span class="sxs-lookup"><span data-stu-id="2628f-122">Use it toocheck when hello build process has ended before starting tooconsume recommendations.</span></span>
* <span data-ttu-id="2628f-123">Aanbevelingen - Get-aanbevelingen voor een specifiek item of de lijst met items in beslag nemen.</span><span class="sxs-lookup"><span data-stu-id="2628f-123">Consume recommendations - Get recommendations for a specific item or list of items.</span></span>

<span data-ttu-id="2628f-124">Alle Hallo stappen hierboven worden gedaan door hello Azure Machine Learning aanbevelingen API.</span><span class="sxs-lookup"><span data-stu-id="2628f-124">All hello steps above are done through hello Azure Machine Learning Recommendations API.</span></span>  <span data-ttu-id="2628f-125">U kunt een voorbeeldtoepassing die u implementeert op elk van deze stappen uit Hallo downloaden [ook galerie.](http://1drv.ms/1xeO2F3)</span><span class="sxs-lookup"><span data-stu-id="2628f-125">You can download a sample application that implements each of these steps from hello [gallery as well.](http://1drv.ms/1xeO2F3)</span></span>

## <a name="limitations"></a><span data-ttu-id="2628f-126">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="2628f-126">Limitations</span></span>
* <span data-ttu-id="2628f-127">Hallo maximumaantal modellen per abonnement is 10.</span><span class="sxs-lookup"><span data-stu-id="2628f-127">hello maximum number of models per subscription is 10.</span></span>
* <span data-ttu-id="2628f-128">maximum aantal items dat een catalogus kan bevatten Hallo is 100.000.</span><span class="sxs-lookup"><span data-stu-id="2628f-128">hello maximum number of items that a catalog can hold is 100,000.</span></span>
* <span data-ttu-id="2628f-129">maximum aantal gebruik punten die blijven Hallo is ~ 5,000,000.</span><span class="sxs-lookup"><span data-stu-id="2628f-129">hello maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="2628f-130">Hallo oudste worden verwijderd als nieuwe wordt geüpload of gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="2628f-130">hello oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="2628f-131">Hallo maximale grootte van gegevens die kunnen worden verzonden in POST (bijvoorbeeld importeren catalogusgegevens, gebruiksgegevens importeren) is 200MB.</span><span class="sxs-lookup"><span data-stu-id="2628f-131">hello maximum size of data that can be sent in POST (for example, import catalog data, import usage data) is 200MB.</span></span>
* <span data-ttu-id="2628f-132">Hallo aantal transacties per seconde voor een aanbeveling model-build die niet actief is ~ 2TPS.</span><span class="sxs-lookup"><span data-stu-id="2628f-132">hello number of transactions per second for a recommendation model build that is not active is ~2TPS.</span></span> <span data-ttu-id="2628f-133">Een aanbeveling model build actieve kan up too20TPS bevatten.</span><span class="sxs-lookup"><span data-stu-id="2628f-133">A recommendation model build that is active can hold up too20TPS.</span></span>

## <a name="integration"></a><span data-ttu-id="2628f-134">Integratie</span><span class="sxs-lookup"><span data-stu-id="2628f-134">Integration</span></span>
### <a name="authentication"></a><span data-ttu-id="2628f-135">Authentication</span><span class="sxs-lookup"><span data-stu-id="2628f-135">Authentication</span></span>
<span data-ttu-id="2628f-136">Microsoft Azure Marketplace biedt ondersteuning voor beide Hallo Basic of OAuth-verificatiemethode.</span><span class="sxs-lookup"><span data-stu-id="2628f-136">Microsoft Azure Marketplace supports either hello Basic or OAuth authentication method.</span></span> <span data-ttu-id="2628f-137">Kunt u gemakkelijk vinden Hallo toegangscodes door te navigeren toohello sleutels in Hallo marketplace onder [uw accountinstellingen](https://datamarket.azure.com/account/keys).</span><span class="sxs-lookup"><span data-stu-id="2628f-137">You can easily find hello account keys by navigating toohello keys in hello marketplace under [your account settings](https://datamarket.azure.com/account/keys).</span></span> 

#### <a name="basic-authentication"></a><span data-ttu-id="2628f-138">Basisverificatie</span><span class="sxs-lookup"><span data-stu-id="2628f-138">Basic Authentication</span></span>
<span data-ttu-id="2628f-139">Hallo-autorisatie-header toevoegen:</span><span class="sxs-lookup"><span data-stu-id="2628f-139">Add hello Authorization header:</span></span>

    Authorization: Basic <creds>

    Where <creds> = ConvertToBase64("AccountKey:" + yourAccountKey);  

<span data-ttu-id="2628f-140">TooBase64 converteren (C#)</span><span class="sxs-lookup"><span data-stu-id="2628f-140">Convert tooBase64 (C#)</span></span>

    var bytes = Encoding.UTF8.GetBytes("AccountKey:" + yourAccountKey);
    var creds = Convert.ToBase64String(bytes);

<span data-ttu-id="2628f-141">TooBase64 converteren (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="2628f-141">Convert tooBase64 (JavaScript)</span></span>

    var creds = window.btoa("AccountKey" + ":" + yourAccountKey);




### <a name="service-uri"></a><span data-ttu-id="2628f-142">Service-URI</span><span class="sxs-lookup"><span data-stu-id="2628f-142">Service URI</span></span>
<span data-ttu-id="2628f-143">Hallo-hoofdmap URI voor hello Azure Machine Learning aanbevelingen API's is [hier.](https://api.datamarket.azure.com/amla/recommendations/v2/)</span><span class="sxs-lookup"><span data-stu-id="2628f-143">hello service root URI for hello Azure Machine Learning Recommendations APIs is [here.](https://api.datamarket.azure.com/amla/recommendations/v2/)</span></span>

<span data-ttu-id="2628f-144">Hallo volledige service-URI wordt uitgedrukt met behulp van elementen van Hallo OData-specificatie.</span><span class="sxs-lookup"><span data-stu-id="2628f-144">hello full service URI is expressed using elements of hello OData specification.</span></span>

### <a name="api-version"></a><span data-ttu-id="2628f-145">API-versie</span><span class="sxs-lookup"><span data-stu-id="2628f-145">API version</span></span>
<span data-ttu-id="2628f-146">Elke API-aanroep heeft, aan het einde van Hallo een queryparameter aangeroepen apiVersion die moet worden ingesteld te "1.0".</span><span class="sxs-lookup"><span data-stu-id="2628f-146">Each API call will have, at hello end, a query parameter called apiVersion that should be set too"1.0".</span></span>

### <a name="ids-are-case-sensitive"></a><span data-ttu-id="2628f-147">Id's zijn hoofdlettergevoelig</span><span class="sxs-lookup"><span data-stu-id="2628f-147">IDs are case-sensitive</span></span>
<span data-ttu-id="2628f-148">Id's die wordt geretourneerd door een van de Hallo-API's, zijn hoofdlettergevoelig en moeten als zodanig worden gebruikt als als parameters doorgegeven in de volgende API-aanroepen.</span><span class="sxs-lookup"><span data-stu-id="2628f-148">IDs, returned by any of hello APIs, are case-sensitive and should be used as such when passed as parameters in subsequent API calls.</span></span> <span data-ttu-id="2628f-149">Bijvoorbeeld, zijn model-id's en de catalogus-id's hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="2628f-149">For instance, model IDs and catalog IDs are case-sensitive.</span></span>

### <a name="create-a-model"></a><span data-ttu-id="2628f-150">Een model maken</span><span class="sxs-lookup"><span data-stu-id="2628f-150">Create a model</span></span>
<span data-ttu-id="2628f-151">Het maken van een aanvraag 'model maken':</span><span class="sxs-lookup"><span data-stu-id="2628f-151">Creating a "create model" request:</span></span>

| <span data-ttu-id="2628f-152">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="2628f-152">HTTP Method</span></span> | <span data-ttu-id="2628f-153">URI</span><span class="sxs-lookup"><span data-stu-id="2628f-153">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2628f-154">VERZENDEN</span><span class="sxs-lookup"><span data-stu-id="2628f-154">POST</span></span> |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="2628f-155">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2628f-155">Example:</span></span><br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| <span data-ttu-id="2628f-156">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="2628f-156">Parameter Name</span></span> | <span data-ttu-id="2628f-157">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="2628f-157">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2628f-158">modelName</span><span class="sxs-lookup"><span data-stu-id="2628f-158">modelName</span></span> |<span data-ttu-id="2628f-159">Alleen letters (A-Z, a-z), cijfers (0-9), afbreekstreepjes (-) en onderstrepingsteken (_) zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="2628f-159">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="2628f-160">Maximale lengte: 20</span><span class="sxs-lookup"><span data-stu-id="2628f-160">Max length: 20</span></span> |
| <span data-ttu-id="2628f-161">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2628f-161">apiVersion</span></span> |<span data-ttu-id="2628f-162">1.0</span><span class="sxs-lookup"><span data-stu-id="2628f-162">1.0</span></span> |
|  | |
| <span data-ttu-id="2628f-163">Aanvraagtekst</span><span class="sxs-lookup"><span data-stu-id="2628f-163">Request Body</span></span> |<span data-ttu-id="2628f-164">GEEN</span><span class="sxs-lookup"><span data-stu-id="2628f-164">NONE</span></span> |

<span data-ttu-id="2628f-165">**Antwoord**:</span><span class="sxs-lookup"><span data-stu-id="2628f-165">**Response**:</span></span>

<span data-ttu-id="2628f-166">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="2628f-166">HTTP Status code: 200</span></span>

* <span data-ttu-id="2628f-167">`feed/entry/content/properties/id`-Bevat Hallo model-ID.</span><span class="sxs-lookup"><span data-stu-id="2628f-167">`feed/entry/content/properties/id` - Contains hello model ID.</span></span>
  <span data-ttu-id="2628f-168">Houd er rekening mee dat Hallo model-ID hoofdlettergevoelig is.</span><span class="sxs-lookup"><span data-stu-id="2628f-168">Note that hello model ID is case-sensitive.</span></span>

<span data-ttu-id="2628f-169">OData-XML</span><span class="sxs-lookup"><span data-stu-id="2628f-169">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Create A New Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:35:21Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">CreateANewModelEntity2</title>
    <updated>2014-10-05T06:35:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">a658c626-2baa-43a7-ac98-f6ee26120a12</d:Id>
        <d:Name m:type="Edm.String">MyFirstModel</d:Name>
        <d:Date m:type="Edm.String">10/5/2014 6:35:19 AM</d:Date>
        <d:Status m:type="Edm.String">Created</d:Status>
        <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
        <d:BuildId m:type="Edm.String">-1</d:BuildId>
        <d:Mpr m:type="Edm.String">0</d:Mpr>
        <d:UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:UserName>
        <d:Description m:type="Edm.String"></d:Description>
      </m:properties>
    </content>
      </entry>
    </feed>


### <a name="import-catalog-data"></a><span data-ttu-id="2628f-170">Gegevens van de catalogus importeren</span><span class="sxs-lookup"><span data-stu-id="2628f-170">Import catalog data</span></span>
<span data-ttu-id="2628f-171">Als u verschillende catalogus bestanden toohello dezelfde model met verschillende aanroepen uploadt, wordt er alleen Hallo nieuwe catalogusitems ingevoegd.</span><span class="sxs-lookup"><span data-stu-id="2628f-171">If you upload several catalog files toohello same model with several calls, we will insert only hello new catalog items.</span></span> <span data-ttu-id="2628f-172">Bestaande items blijft met de oorspronkelijke waarden Hallo.</span><span class="sxs-lookup"><span data-stu-id="2628f-172">Existing items will remain with hello original values.</span></span>

| <span data-ttu-id="2628f-173">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="2628f-173">HTTP Method</span></span> | <span data-ttu-id="2628f-174">URI</span><span class="sxs-lookup"><span data-stu-id="2628f-174">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2628f-175">VERZENDEN</span><span class="sxs-lookup"><span data-stu-id="2628f-175">POST</span></span> |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="2628f-176">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2628f-176">Example:</span></span><br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="2628f-177">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="2628f-177">Parameter Name</span></span> | <span data-ttu-id="2628f-178">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="2628f-178">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2628f-179">Model</span><span class="sxs-lookup"><span data-stu-id="2628f-179">modelId</span></span> |<span data-ttu-id="2628f-180">De unieke id van het Hallo-model (hoofdlettergevoelig)</span><span class="sxs-lookup"><span data-stu-id="2628f-180">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="2628f-181">bestandsnaam</span><span class="sxs-lookup"><span data-stu-id="2628f-181">filename</span></span> |<span data-ttu-id="2628f-182">Tekstuele Hallo catalogus-ID.</span><span class="sxs-lookup"><span data-stu-id="2628f-182">Textual identifier of hello catalog.</span></span><br><span data-ttu-id="2628f-183">Alleen letters (A-Z, a-z), cijfers (0-9), afbreekstreepjes (-) en onderstrepingsteken (_) zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="2628f-183">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="2628f-184">Maximale lengte: 50</span><span class="sxs-lookup"><span data-stu-id="2628f-184">Max length: 50</span></span> |
| <span data-ttu-id="2628f-185">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2628f-185">apiVersion</span></span> |<span data-ttu-id="2628f-186">1.0</span><span class="sxs-lookup"><span data-stu-id="2628f-186">1.0</span></span> |
|  | |
| <span data-ttu-id="2628f-187">Aanvraagtekst</span><span class="sxs-lookup"><span data-stu-id="2628f-187">Request Body</span></span> |<span data-ttu-id="2628f-188">Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="2628f-188">Catalog data.</span></span> <span data-ttu-id="2628f-189">Indeling:</span><span class="sxs-lookup"><span data-stu-id="2628f-189">Format:</span></span><br>`<Item Id>,<Item Name>,<Item Category>[,<description>]`<br><br><table><tr><th><span data-ttu-id="2628f-190">Naam</span><span class="sxs-lookup"><span data-stu-id="2628f-190">Name</span></span></th><th><span data-ttu-id="2628f-191">Verplicht</span><span class="sxs-lookup"><span data-stu-id="2628f-191">Mandatory</span></span></th><th><span data-ttu-id="2628f-192">Type</span><span class="sxs-lookup"><span data-stu-id="2628f-192">Type</span></span></th><th><span data-ttu-id="2628f-193">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="2628f-193">Description</span></span></th></tr><tr><td><span data-ttu-id="2628f-194">Artikel-Id</span><span class="sxs-lookup"><span data-stu-id="2628f-194">Item Id</span></span></td><td><span data-ttu-id="2628f-195">Ja</span><span class="sxs-lookup"><span data-stu-id="2628f-195">Yes</span></span></td><td><span data-ttu-id="2628f-196">Alfanumeriek, max lengte 50</span><span class="sxs-lookup"><span data-stu-id="2628f-196">Alphanumeric, max length 50</span></span></td><td><span data-ttu-id="2628f-197">De unieke id van een item</span><span class="sxs-lookup"><span data-stu-id="2628f-197">Unique identifier of an item</span></span></td></tr><tr><td><span data-ttu-id="2628f-198">De itemnaam van het</span><span class="sxs-lookup"><span data-stu-id="2628f-198">Item Name</span></span></td><td><span data-ttu-id="2628f-199">Ja</span><span class="sxs-lookup"><span data-stu-id="2628f-199">Yes</span></span></td><td><span data-ttu-id="2628f-200">Alfanumeriek, max lengte 255</span><span class="sxs-lookup"><span data-stu-id="2628f-200">Alphanumeric, max length 255</span></span></td><td><span data-ttu-id="2628f-201">De itemnaam van het</span><span class="sxs-lookup"><span data-stu-id="2628f-201">Item name</span></span></td></tr><tr><td><span data-ttu-id="2628f-202">Item categorie</span><span class="sxs-lookup"><span data-stu-id="2628f-202">Item Category</span></span></td><td><span data-ttu-id="2628f-203">Ja</span><span class="sxs-lookup"><span data-stu-id="2628f-203">Yes</span></span></td><td><span data-ttu-id="2628f-204">Alfanumeriek, max lengte 255</span><span class="sxs-lookup"><span data-stu-id="2628f-204">Alphanumeric, max length 255</span></span></td><td><span data-ttu-id="2628f-205">Categorie toowhich die dit item behoort (bijvoorbeeld koken Books Drama...)</span><span class="sxs-lookup"><span data-stu-id="2628f-205">Category toowhich this item belongs (for example, Cooking Books, Drama…)</span></span></td></tr><tr><td><span data-ttu-id="2628f-206">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="2628f-206">Description</span></span></td><td><span data-ttu-id="2628f-207">Nee</span><span class="sxs-lookup"><span data-stu-id="2628f-207">No</span></span></td><td><span data-ttu-id="2628f-208">Alfanumeriek, maximale lengte van 4000</span><span class="sxs-lookup"><span data-stu-id="2628f-208">Alphanumeric, max length 4000</span></span></td><td><span data-ttu-id="2628f-209">Beschrijving van dit item</span><span class="sxs-lookup"><span data-stu-id="2628f-209">Description of this item</span></span></td></tr></table><br><span data-ttu-id="2628f-210">Maximale bestandsgrootte is 200MB.</span><span class="sxs-lookup"><span data-stu-id="2628f-210">Maximum file size is 200MB.</span></span><br><br><span data-ttu-id="2628f-211">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2628f-211">Example:</span></span><br><code>2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book<br>21bf8088-b6c0-4509-870c-e1c7ac78304a,hello Forgetting Room: A Fiction (Byzantium Book),Book<br>3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book<br>552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book</code> |

<span data-ttu-id="2628f-212">**Antwoord**:</span><span class="sxs-lookup"><span data-stu-id="2628f-212">**Response**:</span></span>

<span data-ttu-id="2628f-213">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="2628f-213">HTTP Status code: 200</span></span>

* <span data-ttu-id="2628f-214">`Feed\entry\content\properties\LineCount`-Het aantal regels is geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="2628f-214">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="2628f-215">`Feed\entry\content\properties\ErrorCount`-Het aantal regels dat niet is ingevoegd vanwege fout tooan.</span><span class="sxs-lookup"><span data-stu-id="2628f-215">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due tooan error.</span></span>

<span data-ttu-id="2628f-216">OData-XML</span><span class="sxs-lookup"><span data-stu-id="2628f-216">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
          <subtitle type="text">Import catalog file</subtitle>
          <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:58:04Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">ImportCatalogFileEntity2</title>
    <updated>2014-10-05T06:58:04Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">4</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
      </m:properties>
    </content>
      </entry>
    </feed>


### <a name="import-usage-data"></a><span data-ttu-id="2628f-217">De gebruiksgegevens importeren</span><span class="sxs-lookup"><span data-stu-id="2628f-217">Import usage data</span></span>
#### <a name="uploading-a-file"></a><span data-ttu-id="2628f-218">Uploaden van een bestand</span><span class="sxs-lookup"><span data-stu-id="2628f-218">Uploading a file</span></span>
<span data-ttu-id="2628f-219">Deze sectie wordt beschreven hoe de gebruiksgegevens tooupload met behulp van een bestand.</span><span class="sxs-lookup"><span data-stu-id="2628f-219">This section shows how tooupload usage data by using a file.</span></span> <span data-ttu-id="2628f-220">U kunt deze API is meerdere keren met gebruiksgegevens aanroepen.</span><span class="sxs-lookup"><span data-stu-id="2628f-220">You can call this API several times with usage data.</span></span> <span data-ttu-id="2628f-221">Alle gebruiksgegevens worden opgeslagen voor alle aanroepen.</span><span class="sxs-lookup"><span data-stu-id="2628f-221">All usage data will be saved for all calls.</span></span>

| <span data-ttu-id="2628f-222">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="2628f-222">HTTP Method</span></span> | <span data-ttu-id="2628f-223">URI</span><span class="sxs-lookup"><span data-stu-id="2628f-223">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2628f-224">VERZENDEN</span><span class="sxs-lookup"><span data-stu-id="2628f-224">POST</span></span> |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="2628f-225">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2628f-225">Example:</span></span><br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="2628f-226">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="2628f-226">Parameter Name</span></span> | <span data-ttu-id="2628f-227">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="2628f-227">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2628f-228">Model</span><span class="sxs-lookup"><span data-stu-id="2628f-228">modelId</span></span> |<span data-ttu-id="2628f-229">De unieke id van het Hallo-model (hoofdlettergevoelig)</span><span class="sxs-lookup"><span data-stu-id="2628f-229">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="2628f-230">bestandsnaam</span><span class="sxs-lookup"><span data-stu-id="2628f-230">filename</span></span> |<span data-ttu-id="2628f-231">Tekstuele Hallo catalogus-ID.</span><span class="sxs-lookup"><span data-stu-id="2628f-231">Textual identifier of hello catalog.</span></span><br><span data-ttu-id="2628f-232">Alleen letters (A-Z, a-z), cijfers (0-9), afbreekstreepjes (-) en onderstrepingsteken (_) zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="2628f-232">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="2628f-233">Maximale lengte: 50</span><span class="sxs-lookup"><span data-stu-id="2628f-233">Max length: 50</span></span> |
| <span data-ttu-id="2628f-234">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2628f-234">apiVersion</span></span> |<span data-ttu-id="2628f-235">1.0</span><span class="sxs-lookup"><span data-stu-id="2628f-235">1.0</span></span> |
|  | |
| <span data-ttu-id="2628f-236">Aanvraagtekst</span><span class="sxs-lookup"><span data-stu-id="2628f-236">Request Body</span></span> |<span data-ttu-id="2628f-237">Gebruiksgegevens.</span><span class="sxs-lookup"><span data-stu-id="2628f-237">Usage data.</span></span> <span data-ttu-id="2628f-238">Indeling:</span><span class="sxs-lookup"><span data-stu-id="2628f-238">Format:</span></span><br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th><span data-ttu-id="2628f-239">Naam</span><span class="sxs-lookup"><span data-stu-id="2628f-239">Name</span></span></th><th><span data-ttu-id="2628f-240">Verplicht</span><span class="sxs-lookup"><span data-stu-id="2628f-240">Mandatory</span></span></th><th><span data-ttu-id="2628f-241">Type</span><span class="sxs-lookup"><span data-stu-id="2628f-241">Type</span></span></th><th><span data-ttu-id="2628f-242">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="2628f-242">Description</span></span></th></tr><tr><td><span data-ttu-id="2628f-243">Gebruikers-Id</span><span class="sxs-lookup"><span data-stu-id="2628f-243">User Id</span></span></td><td><span data-ttu-id="2628f-244">Ja</span><span class="sxs-lookup"><span data-stu-id="2628f-244">Yes</span></span></td><td><span data-ttu-id="2628f-245">Alfanumeriek</span><span class="sxs-lookup"><span data-stu-id="2628f-245">Alphanumeric</span></span></td><td><span data-ttu-id="2628f-246">De unieke id van een gebruiker</span><span class="sxs-lookup"><span data-stu-id="2628f-246">Unique identifier of a user</span></span></td></tr><tr><td><span data-ttu-id="2628f-247">Artikel-Id</span><span class="sxs-lookup"><span data-stu-id="2628f-247">Item Id</span></span></td><td><span data-ttu-id="2628f-248">Ja</span><span class="sxs-lookup"><span data-stu-id="2628f-248">Yes</span></span></td><td><span data-ttu-id="2628f-249">Alfanumeriek, max lengte 50</span><span class="sxs-lookup"><span data-stu-id="2628f-249">Alphanumeric, max length 50</span></span></td><td><span data-ttu-id="2628f-250">De unieke id van een item</span><span class="sxs-lookup"><span data-stu-id="2628f-250">Unique identifier of an item</span></span></td></tr><tr><td><span data-ttu-id="2628f-251">Time</span><span class="sxs-lookup"><span data-stu-id="2628f-251">Time</span></span></td><td><span data-ttu-id="2628f-252">Nee</span><span class="sxs-lookup"><span data-stu-id="2628f-252">No</span></span></td><td><span data-ttu-id="2628f-253">Datum in de notatie: jjjj/MM/ddTUU (bijvoorbeeld 2013/06/20T10:00:00)</span><span class="sxs-lookup"><span data-stu-id="2628f-253">Date in format: YYYY/MM/DDTHH:MM:SS (for example, 2013/06/20T10:00:00)</span></span></td><td><span data-ttu-id="2628f-254">Tijd van gegevens</span><span class="sxs-lookup"><span data-stu-id="2628f-254">Time of data</span></span></td></tr><tr><td><span data-ttu-id="2628f-255">Gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="2628f-255">Event</span></span></td><td><span data-ttu-id="2628f-256">Nee, indien opgegeven, en vervolgens datum moet ook worden geplaatst</span><span class="sxs-lookup"><span data-stu-id="2628f-256">No, if supplied then must also put date</span></span></td><td><span data-ttu-id="2628f-257">Een van de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="2628f-257">One of hello following:</span></span><br><span data-ttu-id="2628f-258">• Klik</span><span class="sxs-lookup"><span data-stu-id="2628f-258">• Click</span></span><br><span data-ttu-id="2628f-259">• RecommendationClick</span><span class="sxs-lookup"><span data-stu-id="2628f-259">• RecommendationClick</span></span><br><span data-ttu-id="2628f-260">• AddShopCart</span><span class="sxs-lookup"><span data-stu-id="2628f-260">•    AddShopCart</span></span><br><span data-ttu-id="2628f-261">• RemoveShopCart</span><span class="sxs-lookup"><span data-stu-id="2628f-261">• RemoveShopCart</span></span><br><span data-ttu-id="2628f-262">• Aankoop</span><span class="sxs-lookup"><span data-stu-id="2628f-262">• Purchase</span></span></td><td></td></tr></table><br><span data-ttu-id="2628f-263">Maximale bestandsgrootte is 200MB.</span><span class="sxs-lookup"><span data-stu-id="2628f-263">Maximum file size is 200MB.</span></span><br><br><span data-ttu-id="2628f-264">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2628f-264">Example:</span></span><br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

<span data-ttu-id="2628f-265">**Antwoord**:</span><span class="sxs-lookup"><span data-stu-id="2628f-265">**Response**:</span></span>

<span data-ttu-id="2628f-266">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="2628f-266">HTTP Status code: 200</span></span>

* <span data-ttu-id="2628f-267">`Feed\entry\content\properties\LineCount`-Het aantal regels is geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="2628f-267">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="2628f-268">`Feed\entry\content\properties\ErrorCount`-Het aantal regels dat niet is ingevoegd vanwege fout tooan.</span><span class="sxs-lookup"><span data-stu-id="2628f-268">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due tooan error.</span></span>
* <span data-ttu-id="2628f-269">`Feed\entry\content\properties\FileId`-Id van het bestand.</span><span class="sxs-lookup"><span data-stu-id="2628f-269">`Feed\entry\content\properties\FileId` - File identifier.</span></span>

<span data-ttu-id="2628f-270">OData-XML</span><span class="sxs-lookup"><span data-stu-id="2628f-270">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Add bulk usage data (usage file)</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T07:21:44Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">AddBulkUsageDataUsageFileEntity2</title>
    <updated>2014-10-05T07:21:44Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">33</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
        <d:FileId m:type="Edm.String">fead7c1c-db01-46c0-872f-65bcda36025d</d:FileId>
      </m:properties>
    </content>
      </entry>
    </feed>


#### <a name="using-data-acquisition"></a><span data-ttu-id="2628f-271">Met behulp van de gegevens verkrijgen</span><span class="sxs-lookup"><span data-stu-id="2628f-271">Using data acquisition</span></span>
<span data-ttu-id="2628f-272">Deze sectie wordt beschreven hoe toosend gebeurtenissen in real time tooAzure Machine Learning aanbevelingen meestal van uw website.</span><span class="sxs-lookup"><span data-stu-id="2628f-272">This section shows how toosend events in real time tooAzure Machine Learning Recommendations, usually from your website.</span></span>

| <span data-ttu-id="2628f-273">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="2628f-273">HTTP Method</span></span> | <span data-ttu-id="2628f-274">URI</span><span class="sxs-lookup"><span data-stu-id="2628f-274">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2628f-275">VERZENDEN</span><span class="sxs-lookup"><span data-stu-id="2628f-275">POST</span></span> |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="2628f-276">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="2628f-276">Parameter Name</span></span> | <span data-ttu-id="2628f-277">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="2628f-277">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2628f-278">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2628f-278">apiVersion</span></span> |<span data-ttu-id="2628f-279">1.0</span><span class="sxs-lookup"><span data-stu-id="2628f-279">1.0</span></span> |
|  | |
| <span data-ttu-id="2628f-280">Aanvraagtekst</span><span class="sxs-lookup"><span data-stu-id="2628f-280">Request body</span></span> |<span data-ttu-id="2628f-281">Gebeurtenis gegevensinvoer voor elke gebeurtenis die u wilt toosend.</span><span class="sxs-lookup"><span data-stu-id="2628f-281">Event data entry for each event you want toosend.</span></span> <span data-ttu-id="2628f-282">Voor hello dezelfde gebruiker of browser sessie Hallo dezelfde ID in het Hallo-sessie-id-veld moet worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="2628f-282">You should send for hello same user or browser session hello same ID in hello SessionId field.</span></span> <span data-ttu-id="2628f-283">(Zie het voorbeeld van de hoofdtekst van de gebeurtenis is hieronder).</span><span class="sxs-lookup"><span data-stu-id="2628f-283">(See sample of event body below.)</span></span> |

* <span data-ttu-id="2628f-284">Voorbeeld voor gebeurtenis 'Klik':</span><span class="sxs-lookup"><span data-stu-id="2628f-284">Example for event 'Click':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
        <EventData>
        <Name>Click</Name>
        <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
        </EventData>
        </Event>
* <span data-ttu-id="2628f-285">Voorbeeld voor gebeurtenis 'RecommendationClick':</span><span class="sxs-lookup"><span data-stu-id="2628f-285">Example for event 'RecommendationClick':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>RecommendationClick</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* <span data-ttu-id="2628f-286">Voorbeeld voor gebeurtenis 'AddShopCart':</span><span class="sxs-lookup"><span data-stu-id="2628f-286">Example for event 'AddShopCart':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>AddShopCart</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* <span data-ttu-id="2628f-287">Voorbeeld voor gebeurtenis 'RemoveShopCart':</span><span class="sxs-lookup"><span data-stu-id="2628f-287">Example for event 'RemoveShopCart':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>RemoveShopCart</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* <span data-ttu-id="2628f-288">Voorbeeld voor gebeurtenis 'Aankoop':</span><span class="sxs-lookup"><span data-stu-id="2628f-288">Example for event 'Purchase':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
        <EventData>
            <Name>Purchase</Name> 
            <PurchaseItems>
            <PurchaseItems>
                <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
                <Count>3</Count>
            </PurchaseItems>
        </PurchaseItems>
        </EventData>
        </EventData>
        </Event>
* <span data-ttu-id="2628f-289">Voorbeeld '2 gebeurtenissen op' en 'AddShopCart' verzenden:</span><span class="sxs-lookup"><span data-stu-id="2628f-289">Example sending 2 events, 'Click' and 'AddShopCart':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>Click</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
          <ItemName>itemName</ItemName>
          <ItemDescription>item description</ItemDescription>
          <ItemCategory>category</ItemCategory>
        </EventData>
        <EventData>
          <Name>AddShopCart</Name>
          <ItemId>552A1940-21E4-4399-82BB-594B46D7ED54</ItemId>
        </EventData>
          </EventData>
        </Event>

<span data-ttu-id="2628f-290">**Antwoord**: HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="2628f-290">**Response**: HTTP Status code: 200</span></span>

### <a name="build-a-recommendation-model"></a><span data-ttu-id="2628f-291">Een aanbeveling model bouwen</span><span class="sxs-lookup"><span data-stu-id="2628f-291">Build a recommendation model</span></span>
| <span data-ttu-id="2628f-292">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="2628f-292">HTTP Method</span></span> | <span data-ttu-id="2628f-293">URI</span><span class="sxs-lookup"><span data-stu-id="2628f-293">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2628f-294">VERZENDEN</span><span class="sxs-lookup"><span data-stu-id="2628f-294">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="2628f-295">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2628f-295">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |

| <span data-ttu-id="2628f-296">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="2628f-296">Parameter Name</span></span> | <span data-ttu-id="2628f-297">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="2628f-297">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2628f-298">Model</span><span class="sxs-lookup"><span data-stu-id="2628f-298">modelId</span></span> |<span data-ttu-id="2628f-299">De unieke id van het Hallo-model (hoofdlettergevoelig)</span><span class="sxs-lookup"><span data-stu-id="2628f-299">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="2628f-300">userDescription</span><span class="sxs-lookup"><span data-stu-id="2628f-300">userDescription</span></span> |<span data-ttu-id="2628f-301">Tekstuele Hallo catalogus-ID.</span><span class="sxs-lookup"><span data-stu-id="2628f-301">Textual identifier of hello catalog.</span></span> <span data-ttu-id="2628f-302">Houd er rekening mee dat als u opslagruimten gebruikt u deze met % 20 in plaats daarvan coderen moet.</span><span class="sxs-lookup"><span data-stu-id="2628f-302">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="2628f-303">Zie het bovenstaande voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="2628f-303">See example above.</span></span><br><span data-ttu-id="2628f-304">Maximale lengte: 50</span><span class="sxs-lookup"><span data-stu-id="2628f-304">Max length: 50</span></span> |
| <span data-ttu-id="2628f-305">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2628f-305">apiVersion</span></span> |<span data-ttu-id="2628f-306">1.0</span><span class="sxs-lookup"><span data-stu-id="2628f-306">1.0</span></span> |
|  | |
| <span data-ttu-id="2628f-307">Aanvraagtekst</span><span class="sxs-lookup"><span data-stu-id="2628f-307">Request Body</span></span> |<span data-ttu-id="2628f-308">GEEN</span><span class="sxs-lookup"><span data-stu-id="2628f-308">NONE</span></span> |

<span data-ttu-id="2628f-309">**Antwoord**:</span><span class="sxs-lookup"><span data-stu-id="2628f-309">**Response**:</span></span>

<span data-ttu-id="2628f-310">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="2628f-310">HTTP Status code: 200</span></span>

<span data-ttu-id="2628f-311">Dit is een asynchrone API.</span><span class="sxs-lookup"><span data-stu-id="2628f-311">This is an asynchronous API.</span></span> <span data-ttu-id="2628f-312">U krijgt een build-ID als antwoord.</span><span class="sxs-lookup"><span data-stu-id="2628f-312">You will get a build ID as a response.</span></span> <span data-ttu-id="2628f-313">tooknow wanneer Hallo build is beëindigd, die u moet Hallo 'Ophalen Builds Status van een Model' API aanroepen en zoek deze ID in het antwoord Hallo bouwen.</span><span class="sxs-lookup"><span data-stu-id="2628f-313">tooknow when hello build has ended, you should call hello "Get Builds Status of a Model" API and locate this build ID in hello response.</span></span> <span data-ttu-id="2628f-314">Houd er rekening mee dat een build van toohours minuten, afhankelijk van de grootte Hallo Hallo gegevens kan opnemen.</span><span class="sxs-lookup"><span data-stu-id="2628f-314">Note that a build can take from minutes toohours depending on hello size of hello data.</span></span>

<span data-ttu-id="2628f-315">U kan geen aanbevelingen verbruiken tot Hallo bouwen eindigt.</span><span class="sxs-lookup"><span data-stu-id="2628f-315">You cannot consume recommendations till hello build ends.</span></span>

<span data-ttu-id="2628f-316">Geldige build-status:</span><span class="sxs-lookup"><span data-stu-id="2628f-316">Valid build status:</span></span>

* <span data-ttu-id="2628f-317">Maken – Model is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2628f-317">Create – Model was created.</span></span>
* <span data-ttu-id="2628f-318">In de wachtrij: Model build is geactiveerd en deze in de wachtrij staat.</span><span class="sxs-lookup"><span data-stu-id="2628f-318">Queued – Model build was triggered and it is queued.</span></span>
* <span data-ttu-id="2628f-319">Gebouw – Model wordt samengesteld.</span><span class="sxs-lookup"><span data-stu-id="2628f-319">Building – Model is being built.</span></span>
* <span data-ttu-id="2628f-320">Geslaagde – Build is beëindigd.</span><span class="sxs-lookup"><span data-stu-id="2628f-320">Success – Build ended successfully.</span></span>
* <span data-ttu-id="2628f-321">Fout: Build beëindigd met een fout.</span><span class="sxs-lookup"><span data-stu-id="2628f-321">Error – Build ended with a failure.</span></span>
* <span data-ttu-id="2628f-322">Geannuleerd – is Build geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="2628f-322">Canceled – Build was canceled.</span></span>
* <span data-ttu-id="2628f-323">Annuleren – Build wordt geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="2628f-323">Canceling – Build is being canceled.</span></span>

<span data-ttu-id="2628f-324">Houd er rekening mee dat Hallo-build-ID vindt onder in het pad naar Hallo:`Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="2628f-324">Note that hello build ID can be found under hello following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="2628f-325">OData-XML</span><span class="sxs-lookup"><span data-stu-id="2628f-325">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">1000272</d:Id>
        <d:UserName m:type="Edm.String"></d:UserName>
        <d:ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:ModelId>
        <d:ModelName m:type="Edm.String">docTest</d:ModelName>
        <d:Type m:type="Edm.String">Recommendation</d:Type>
        <d:CreationTime m:type="Edm.String">2014-10-05T08:56:31.893</d:CreationTime>
        <d:Progress_BuildId m:type="Edm.String">1000272</d:Progress_BuildId>
        <d:Progress_ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:Progress_ModelId>
        <d:Progress_UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:Progress_UserName>
        <d:Progress_IsExecutionStarted m:type="Edm.String">false</d:Progress_IsExecutionStarted>
        <d:Progress_IsExecutionEnded m:type="Edm.String">false</d:Progress_IsExecutionEnded>
        <d:Progress_Percent m:type="Edm.String">0</d:Progress_Percent>
        <d:Progress_StartTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_StartTime>
        <d:Progress_EndTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_EndTime>
        <d:Progress_UpdateDateUTC m:type="Edm.String"></d:Progress_UpdateDateUTC>
        <d:Status m:type="Edm.String">Queued</d:Status>
        <d:Key1 m:type="Edm.String">UseFeaturesInModel</d:Key1>
        <d:Value1 m:type="Edm.String">False</d:Value1>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="get-build-status-of-a-model"></a><span data-ttu-id="2628f-326">Status van een model bouwen ophalen</span><span class="sxs-lookup"><span data-stu-id="2628f-326">Get build status of a model</span></span>
| <span data-ttu-id="2628f-327">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="2628f-327">HTTP Method</span></span> | <span data-ttu-id="2628f-328">URI</span><span class="sxs-lookup"><span data-stu-id="2628f-328">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2628f-329">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="2628f-329">GET</span></span> |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="2628f-330">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2628f-330">Example:</span></span><br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| <span data-ttu-id="2628f-331">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="2628f-331">Parameter Name</span></span> | <span data-ttu-id="2628f-332">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="2628f-332">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2628f-333">Model</span><span class="sxs-lookup"><span data-stu-id="2628f-333">modelId</span></span> |<span data-ttu-id="2628f-334">De unieke id van het Hallo-model (hoofdlettergevoelig)</span><span class="sxs-lookup"><span data-stu-id="2628f-334">Unique identifier of hello model  (case-sensitive)</span></span> |
| <span data-ttu-id="2628f-335">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="2628f-335">onlyLastBuild</span></span> |<span data-ttu-id="2628f-336">Hiermee wordt aangegeven of tooreturn alle Hallo geschiedenis van Hallo model of de status alleen Hallo van de meest recente build Hallo bouwen.</span><span class="sxs-lookup"><span data-stu-id="2628f-336">Indicates whether tooreturn all hello build history of hello model or only hello status of hello most recent build.</span></span> |
| <span data-ttu-id="2628f-337">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2628f-337">apiVersion</span></span> |<span data-ttu-id="2628f-338">1.0</span><span class="sxs-lookup"><span data-stu-id="2628f-338">1.0</span></span> |

<span data-ttu-id="2628f-339">**Antwoord**:</span><span class="sxs-lookup"><span data-stu-id="2628f-339">**Response**:</span></span>

<span data-ttu-id="2628f-340">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="2628f-340">HTTP Status code: 200</span></span>

<span data-ttu-id="2628f-341">Hallo-antwoord bevat één vermelding per build.</span><span class="sxs-lookup"><span data-stu-id="2628f-341">hello response includes one entry per build.</span></span> <span data-ttu-id="2628f-342">Elk item heeft Hallo gegevens te volgen:</span><span class="sxs-lookup"><span data-stu-id="2628f-342">Each entry has hello following data:</span></span>

* <span data-ttu-id="2628f-343">`feed/entry/content/properties/UserName`– Naam van de gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="2628f-343">`feed/entry/content/properties/UserName` – Name of hello user.</span></span>
* <span data-ttu-id="2628f-344">`feed/entry/content/properties/ModelName`– Naam van Hallo-model.</span><span class="sxs-lookup"><span data-stu-id="2628f-344">`feed/entry/content/properties/ModelName` – Name of hello model.</span></span>
* <span data-ttu-id="2628f-345">`feed/entry/content/properties/ModelId`– De unieke id van het model.</span><span class="sxs-lookup"><span data-stu-id="2628f-345">`feed/entry/content/properties/ModelId` – Model unique identifier.</span></span>
* <span data-ttu-id="2628f-346">`feed/entry/content/properties/IsDeployed`– Of Hallo build (ook wordt geïmplementeerd</span><span class="sxs-lookup"><span data-stu-id="2628f-346">`feed/entry/content/properties/IsDeployed` – Whether hello build is deployed (a.k.a.</span></span> <span data-ttu-id="2628f-347">actieve build).</span><span class="sxs-lookup"><span data-stu-id="2628f-347">active build).</span></span>
* <span data-ttu-id="2628f-348">`feed/entry/content/properties/BuildId`– De unieke id maken.</span><span class="sxs-lookup"><span data-stu-id="2628f-348">`feed/entry/content/properties/BuildId` – Build unique identifier.</span></span>
* <span data-ttu-id="2628f-349">`feed/entry/content/properties/BuildType`-Type van Hallo build.</span><span class="sxs-lookup"><span data-stu-id="2628f-349">`feed/entry/content/properties/BuildType` - Type of hello build.</span></span>
* <span data-ttu-id="2628f-350">`feed/entry/content/properties/Status`– Status maken.</span><span class="sxs-lookup"><span data-stu-id="2628f-350">`feed/entry/content/properties/Status` – Build status.</span></span> <span data-ttu-id="2628f-351">Een van de volgende Hallo: fout, gebouwen, in de wachtrij geplaatst, Canceling, geannuleerd, geslaagd</span><span class="sxs-lookup"><span data-stu-id="2628f-351">Can be one of hello following: Error, Building, Queued, Canceling, Canceled, Success</span></span>
* <span data-ttu-id="2628f-352">`feed/entry/content/properties/StatusMessage`– Gedetailleerde statusbericht (geldt alleen toospecific statussen).</span><span class="sxs-lookup"><span data-stu-id="2628f-352">`feed/entry/content/properties/StatusMessage` – Detailed status message (applies only toospecific states).</span></span>
* <span data-ttu-id="2628f-353">`feed/entry/content/properties/Progress`– Bouwen voortgang (%).</span><span class="sxs-lookup"><span data-stu-id="2628f-353">`feed/entry/content/properties/Progress` – Build progress (%).</span></span>
* <span data-ttu-id="2628f-354">`feed/entry/content/properties/StartTime`– Begintijd build.</span><span class="sxs-lookup"><span data-stu-id="2628f-354">`feed/entry/content/properties/StartTime` – Build start time.</span></span>
* <span data-ttu-id="2628f-355">`feed/entry/content/properties/EndTime`– Eindtijd bouwen.</span><span class="sxs-lookup"><span data-stu-id="2628f-355">`feed/entry/content/properties/EndTime` – Build end time.</span></span>
* <span data-ttu-id="2628f-356">`feed/entry/content/properties/ExecutionTime`– Duur maken.</span><span class="sxs-lookup"><span data-stu-id="2628f-356">`feed/entry/content/properties/ExecutionTime` – Build duration.</span></span>
* <span data-ttu-id="2628f-357">`feed/entry/content/properties/ProgressStep`– Details over de huidige fase Hallo die een build uitgevoerd in.</span><span class="sxs-lookup"><span data-stu-id="2628f-357">`feed/entry/content/properties/ProgressStep` – Details about hello current stage that a build in progress is in.</span></span>

<span data-ttu-id="2628f-358">Geldige build-status:</span><span class="sxs-lookup"><span data-stu-id="2628f-358">Valid build status:</span></span>

* <span data-ttu-id="2628f-359">Gemaakt – is de vermelding van de Build-verzoek gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2628f-359">Created – Build request entry was created.</span></span>
* <span data-ttu-id="2628f-360">In de wachtrij: aanvraag voor het samenstellen is geactiveerd en deze in de wachtrij staat.</span><span class="sxs-lookup"><span data-stu-id="2628f-360">Queued – Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="2628f-361">Gebouw – Build is bezig.</span><span class="sxs-lookup"><span data-stu-id="2628f-361">Building – Build is in process.</span></span>
* <span data-ttu-id="2628f-362">Geslaagde – Build is beëindigd.</span><span class="sxs-lookup"><span data-stu-id="2628f-362">Success – Build ended successfully.</span></span>
* <span data-ttu-id="2628f-363">Fout: Build beëindigd met een fout.</span><span class="sxs-lookup"><span data-stu-id="2628f-363">Error – Build ended with a failure.</span></span>
* <span data-ttu-id="2628f-364">Geannuleerd – is Build geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="2628f-364">Canceled – Build was canceled.</span></span>
* <span data-ttu-id="2628f-365">Annuleren – Build wordt geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="2628f-365">Canceling – Build is being canceled.</span></span>

<span data-ttu-id="2628f-366">Geldige waarden voor de BuildType:</span><span class="sxs-lookup"><span data-stu-id="2628f-366">Valid values for build type:</span></span>

* <span data-ttu-id="2628f-367">Positie - positie bouwen.</span><span class="sxs-lookup"><span data-stu-id="2628f-367">Rank - Rank build.</span></span> <span data-ttu-id="2628f-368">(Voor positie bouwen details, raadpleegt u toohello 'Aanbeveling van Machine Learning API-documentatie' document).</span><span class="sxs-lookup"><span data-stu-id="2628f-368">(For rank build details, please refer toohello "Machine Learning Recommendation API documentation" document.)</span></span>
* <span data-ttu-id="2628f-369">Aanbeveling - aanbeveling build.</span><span class="sxs-lookup"><span data-stu-id="2628f-369">Recommendation - Recommendation build.</span></span>
* <span data-ttu-id="2628f-370">FBT - vaak samen build hebt gekocht.</span><span class="sxs-lookup"><span data-stu-id="2628f-370">Fbt - Frequently bought together build.</span></span>

<span data-ttu-id="2628f-371">OData-XML</span><span class="sxs-lookup"><span data-stu-id="2628f-371">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get builds status of a model</subtitle>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T17:51:10Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'" />
    <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetBuildsStatusEntity</title>
    <updated>2014-11-05T17:51:10Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:UserName m:type="Edm.String">b-434e-b2c9-84935664ff20@dm.com</d:UserName>
        <d:ModelName m:type="Edm.String">ModelName</d:ModelName>
        <d:ModelId m:type="Edm.String">1d20c34f-dca1-4eac-8e5d-f299e4e4ad66</d:ModelId>
        <d:IsDeployed m:type="Edm.String">true</d:IsDeployed>
        <d:BuildId m:type="Edm.String">1000272</d:BuildId>
        <d:BuildType m:type="Edm.String">Recommendation</d:BuildType>
        <d:Status m:type="Edm.String">Success</d:Status>
        <d:StatusMessage m:type="Edm.String"></d:StatusMessage>
        <d:Progress m:type="Edm.String">0</d:Progress>
        <d:StartTime m:type="Edm.String">2014-11-02T13:43:51</d:StartTime>
        <d:EndTime m:type="Edm.String">2014-11-02T13:45:10</d:EndTime>
        <d:ExecutionTime m:type="Edm.String">00:01:19</d:ExecutionTime>
        <d:IsExecutionStarted m:type="Edm.String">false</d:IsExecutionStarted>
        <d:ProgressStep m:type="Edm.String"></d:ProgressStep>
      </m:properties>
     </content>
    </entry>
    </feed>


### <a name="get-recommendations"></a><span data-ttu-id="2628f-372">Aanbevelingen ophalen</span><span class="sxs-lookup"><span data-stu-id="2628f-372">Get recommendations</span></span>
| <span data-ttu-id="2628f-373">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="2628f-373">HTTP Method</span></span> | <span data-ttu-id="2628f-374">URI</span><span class="sxs-lookup"><span data-stu-id="2628f-374">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2628f-375">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="2628f-375">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="2628f-376">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2628f-376">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="2628f-377">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="2628f-377">Parameter Name</span></span> | <span data-ttu-id="2628f-378">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="2628f-378">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2628f-379">Model</span><span class="sxs-lookup"><span data-stu-id="2628f-379">modelId</span></span> |<span data-ttu-id="2628f-380">De unieke id van het Hallo-model (hoofdlettergevoelig)</span><span class="sxs-lookup"><span data-stu-id="2628f-380">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="2628f-381">ItemID 's</span><span class="sxs-lookup"><span data-stu-id="2628f-381">itemIds</span></span> |<span data-ttu-id="2628f-382">Door komma's gescheiden lijst met Hallo items toorecommend voor.</span><span class="sxs-lookup"><span data-stu-id="2628f-382">Comma-separated list of hello items toorecommend for.</span></span><br><span data-ttu-id="2628f-383">Maximale lengte: 1024</span><span class="sxs-lookup"><span data-stu-id="2628f-383">Max length: 1024</span></span> |
| <span data-ttu-id="2628f-384">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="2628f-384">numberOfResults</span></span> |<span data-ttu-id="2628f-385">Aantal vereiste resultaten</span><span class="sxs-lookup"><span data-stu-id="2628f-385">Number of required results</span></span> |
| <span data-ttu-id="2628f-386">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="2628f-386">includeMetatadata</span></span> |<span data-ttu-id="2628f-387">Toekomstig gebruik, altijd Onwaar</span><span class="sxs-lookup"><span data-stu-id="2628f-387">Future use, always false</span></span> |
| <span data-ttu-id="2628f-388">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2628f-388">apiVersion</span></span> |<span data-ttu-id="2628f-389">1.0</span><span class="sxs-lookup"><span data-stu-id="2628f-389">1.0</span></span> |

<span data-ttu-id="2628f-390">**Antwoord:**</span><span class="sxs-lookup"><span data-stu-id="2628f-390">**Response:**</span></span>

<span data-ttu-id="2628f-391">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="2628f-391">HTTP Status code: 200</span></span>

<span data-ttu-id="2628f-392">Hallo-antwoord bevat één vermelding per aanbevolen-item.</span><span class="sxs-lookup"><span data-stu-id="2628f-392">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="2628f-393">Elk item heeft Hallo gegevens te volgen:</span><span class="sxs-lookup"><span data-stu-id="2628f-393">Each entry has hello following data:</span></span>

* <span data-ttu-id="2628f-394">`Feed\entry\content\properties\Id`-Aanbevolen artikel-ID.</span><span class="sxs-lookup"><span data-stu-id="2628f-394">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="2628f-395">`Feed\entry\content\properties\Name`-De naam van het Hallo-item.</span><span class="sxs-lookup"><span data-stu-id="2628f-395">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="2628f-396">`Feed\entry\content\properties\Rating`-Classificatie van Hallo aanbeveling; hogere waarde betekent hogere betrouwbaarheid.</span><span class="sxs-lookup"><span data-stu-id="2628f-396">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="2628f-397">`Feed\entry\content\properties\Reasoning`-Aanbeveling redenering (bijvoorbeeld aanbeveling uitleg).</span><span class="sxs-lookup"><span data-stu-id="2628f-397">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (for example, recommendation explanations).</span></span>

<span data-ttu-id="2628f-398">OData-XML</span><span class="sxs-lookup"><span data-stu-id="2628f-398">OData XML</span></span>

<span data-ttu-id="2628f-399">Hallo voorbeeld hieronder reactie omvat 10 aanbevolen artikelen:</span><span class="sxs-lookup"><span data-stu-id="2628f-399">hello example response below includes 10 recommended items:</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">159</d:Id>
        <d:Name m:type="Edm.String">159</d:Name>
        <d:Rating m:type="Edm.Double">0.543343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '159'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">52</d:Id>
        <d:Name m:type="Edm.String">52</d:Name>
        <d:Rating m:type="Edm.Double">0.539588900748721</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '52'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">35</d:Id>
        <d:Name m:type="Edm.String">35</d:Name>
        <d:Rating m:type="Edm.Double">0.53842946443853</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '35'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">124</d:Id>
        <d:Name m:type="Edm.String">124</d:Name>
        <d:Rating m:type="Edm.Double">0.536712832792886</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '124'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">120</d:Id>
        <d:Name m:type="Edm.String">120</d:Name>
        <d:Rating m:type="Edm.Double">0.533673023762878</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '120'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">96</d:Id>
        <d:Name m:type="Edm.String">96</d:Name>
        <d:Rating m:type="Edm.Double">0.532544826370521</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '96'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">69</d:Id>
        <d:Name m:type="Edm.String">69</d:Name>
        <d:Rating m:type="Edm.Double">0.531678607847759</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '69'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">172</d:Id>
        <d:Name m:type="Edm.String">172</d:Name>
        <d:Rating m:type="Edm.Double">0.530957821375951</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '172'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">155</d:Id>
        <d:Name m:type="Edm.String">155</d:Name>
        <d:Rating m:type="Edm.Double">0.529093541481333</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '155'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">32</d:Id>
        <d:Name m:type="Edm.String">32</d:Name>
        <d:Rating m:type="Edm.Double">0.528917978168322</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '32'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="update-model"></a><span data-ttu-id="2628f-400">Model bijwerken</span><span class="sxs-lookup"><span data-stu-id="2628f-400">Update model</span></span>
<span data-ttu-id="2628f-401">U kunt Hallo Modelbeschrijving van update of Hallo active build-ID.</span><span class="sxs-lookup"><span data-stu-id="2628f-401">You can update hello model description or hello active build ID.</span></span>
<span data-ttu-id="2628f-402">*ID van de actieve build* -elke build voor elk model heeft een build-ID.</span><span class="sxs-lookup"><span data-stu-id="2628f-402">*Active build ID* - Every build for every model has a build ID.</span></span> <span data-ttu-id="2628f-403">Hallo active build-ID is Hallo eerste geslaagde build van elke nieuwe model.</span><span class="sxs-lookup"><span data-stu-id="2628f-403">hello active build ID is hello first successful build of every new model.</span></span> <span data-ttu-id="2628f-404">Wanneer u een actieve build-ID hebt en u extra builds voor Hallo doen hetzelfde model, moet u tooexplicitly ingesteld dat deze zoals hello standaard bouwen ID als u wilt.</span><span class="sxs-lookup"><span data-stu-id="2628f-404">Once you have an active build ID and you do additional builds for hello same model, you need tooexplicitly set it as hello default build ID if you want to.</span></span> <span data-ttu-id="2628f-405">Wanneer u aanbevelingen gebruiken als u geen opgeeft Hallo build-ID die u wilt dat toouse, Hallo standaard één automatisch zal worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="2628f-405">When you consume recommendations, if you do not specify hello build ID that you want toouse, hello default one will be used automatically.</span></span>

<span data-ttu-id="2628f-406">Dit mechanisme kunt u - zodra u een aanbeveling-model in productie - toobuild nieuwe modellen hebt en te testen voordat u ze promoveert tooproduction.</span><span class="sxs-lookup"><span data-stu-id="2628f-406">This mechanism enables you - once you have a recommendation model in production - toobuild new models and test them before you promote them tooproduction.</span></span>

| <span data-ttu-id="2628f-407">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="2628f-407">HTTP Method</span></span> | <span data-ttu-id="2628f-408">URI</span><span class="sxs-lookup"><span data-stu-id="2628f-408">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="2628f-409">PLAATSEN</span><span class="sxs-lookup"><span data-stu-id="2628f-409">PUT</span></span> |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="2628f-410">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2628f-410">Example:</span></span><br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| <span data-ttu-id="2628f-411">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="2628f-411">Parameter Name</span></span> | <span data-ttu-id="2628f-412">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="2628f-412">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="2628f-413">id</span><span class="sxs-lookup"><span data-stu-id="2628f-413">id</span></span> |<span data-ttu-id="2628f-414">De unieke id van het Hallo-model (hoofdlettergevoelig)</span><span class="sxs-lookup"><span data-stu-id="2628f-414">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="2628f-415">apiVersion</span><span class="sxs-lookup"><span data-stu-id="2628f-415">apiVersion</span></span> |<span data-ttu-id="2628f-416">1.0</span><span class="sxs-lookup"><span data-stu-id="2628f-416">1.0</span></span> |
|  | |
| <span data-ttu-id="2628f-417">Aanvraagtekst</span><span class="sxs-lookup"><span data-stu-id="2628f-417">Request Body</span></span> |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`   <Description>New Description</Description>`<br>`          <ActiveBuildId>-1</ActiveBuildId>`<br>`</ModelUpdateParams>`<br><br><span data-ttu-id="2628f-418">Houd er rekening mee dat Hallo XML-beschrijving tags en ActiveBuildId zijn optioneel.</span><span class="sxs-lookup"><span data-stu-id="2628f-418">Note that hello XML tags Description and ActiveBuildId are optional.</span></span> <span data-ttu-id="2628f-419">Als u niet dat tooset beschrijving of ActiveBuildId wilt, moet u de volledige code Hallo verwijderen.</span><span class="sxs-lookup"><span data-stu-id="2628f-419">If you do not want tooset Description or ActiveBuildId, remove hello entire tag.</span></span> |

<span data-ttu-id="2628f-420">**Antwoord**:</span><span class="sxs-lookup"><span data-stu-id="2628f-420">**Response**:</span></span>

<span data-ttu-id="2628f-421">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="2628f-421">HTTP Status code: 200</span></span>

<span data-ttu-id="2628f-422">OData-XML</span><span class="sxs-lookup"><span data-stu-id="2628f-422">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Update an Existing Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T10:27:17Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'" />
    </feed>

## <a name="legal"></a><span data-ttu-id="2628f-423">Juridische informatie</span><span class="sxs-lookup"><span data-stu-id="2628f-423">Legal</span></span>
<span data-ttu-id="2628f-424">Dit document wordt geleverd ' as-is '.</span><span class="sxs-lookup"><span data-stu-id="2628f-424">This document is provided "as-is".</span></span> <span data-ttu-id="2628f-425">Informatie en inzichten die in dit document, inclusief URL's en andere websiteverwijzingen, kunnen zonder kennisgeving worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="2628f-425">Information and views expressed in this document, including URL and other Internet website references, may change without notice.</span></span> <span data-ttu-id="2628f-426">Enkele voorbeelden die hierin staan zijn uitsluitend ter illustratie en zijn fictief.</span><span class="sxs-lookup"><span data-stu-id="2628f-426">Some examples depicted herein are provided for illustration only and are fictitious.</span></span> <span data-ttu-id="2628f-427">Er is geen echte verwantschap of relatie is bedoeld of moet worden afgeleid.</span><span class="sxs-lookup"><span data-stu-id="2628f-427">No real association or connection is intended or should be inferred.</span></span> <span data-ttu-id="2628f-428">Dit document biedt geen u enkel wettelijk recht tooany intellectueel eigendom in een Microsoft-product.</span><span class="sxs-lookup"><span data-stu-id="2628f-428">This document does not provide you with any legal rights tooany intellectual property in any Microsoft product.</span></span> <span data-ttu-id="2628f-429">U kunt kopiëren en het gebruik van dit document voor eigen referentiedoeleinden.</span><span class="sxs-lookup"><span data-stu-id="2628f-429">You may copy and use this document for your internal, reference purposes.</span></span> <span data-ttu-id="2628f-430">© 2014 Microsoft Corporation.</span><span class="sxs-lookup"><span data-stu-id="2628f-430">© 2014 Microsoft.</span></span> <span data-ttu-id="2628f-431">Alle rechten voorbehouden.</span><span class="sxs-lookup"><span data-stu-id="2628f-431">All rights reserved.</span></span> 

