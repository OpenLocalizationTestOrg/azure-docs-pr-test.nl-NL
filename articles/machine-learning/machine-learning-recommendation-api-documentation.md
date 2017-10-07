---
title: aaaMachine Learning aanbevelingen API-documentatie | Microsoft Docs
description: Azure Machine Learning aanbevelingen API-documentatie voor een beschikbaar is in Microsoft Azure Marketplace Hallo aanbevelingen-engine.
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 32c3ab2f-fdd7-48cc-b501-ad55c79b87dc
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: LuisCa
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: d1cec228bf23870c05c8ab8df2779b0c3c65b06d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-recommendations-api-documentation"></a><span data-ttu-id="d044f-103">Documentatie voor Recommendations-API voor Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d044f-103">Azure Machine Learning Recommendations API Documentation</span></span>
> [!NOTE]
> <span data-ttu-id="d044f-104">U moet beginnen met Hallo cognitieve aanbevelingen API-Service in plaats van deze versie.</span><span class="sxs-lookup"><span data-stu-id="d044f-104">You should start using hello Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="d044f-105">Hallo aanbevelingen cognitieve Service vervangt deze service en alle nieuwe functies in Hallo er zal worden ontwikkeld.</span><span class="sxs-lookup"><span data-stu-id="d044f-105">hello Recommendations Cognitive Service will be replacing this service, and all hello new features will be developed there.</span></span> <span data-ttu-id="d044f-106">Heeft nieuwe mogelijkheden, zoals batchverwerking ondersteuning, beter API Explorer, een schonere API surface, consistente aanmelding/facturering ervaring, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="d044f-106">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="d044f-107">Meer informatie over [migreren toohello nieuwe cognitieve Service](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="d044f-107">Learn more about [Migrating toohello new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="d044f-108">Dit document beschrijft de Microsoft Azure Machine Learning-aanbevelingen API's.</span><span class="sxs-lookup"><span data-stu-id="d044f-108">This document depicts Microsoft Azure Machine Learning Recommendations APIs.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a><span data-ttu-id="d044f-109">1. Algemeen overzicht</span><span class="sxs-lookup"><span data-stu-id="d044f-109">1. General overview</span></span>
<span data-ttu-id="d044f-110">Dit document is een API-verwijzing.</span><span class="sxs-lookup"><span data-stu-id="d044f-110">This document is an API reference.</span></span> <span data-ttu-id="d044f-111">U moet beginnen met 'Azure Machine Learning aanbeveling--Quick Start' Hallo-document.</span><span class="sxs-lookup"><span data-stu-id="d044f-111">You should start with hello “Azure Machine Learning Recommendation - Quick Start” document.</span></span>

<span data-ttu-id="d044f-112">Hello Azure Machine Learning aanbevelingen API kan worden onderverdeeld in Hallo logische groepen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d044f-112">hello Azure Machine Learning Recommendations API can be divided into hello following logical groups:</span></span>

* <span data-ttu-id="d044f-113"><ins>Beperkingen</ins> -aanbevelingen API-beperkingen.</span><span class="sxs-lookup"><span data-stu-id="d044f-113"><ins>Limitations</ins> - Recommendations API limitations.</span></span>
* <span data-ttu-id="d044f-114"><ins>Algemene informatie</ins> -informatie over verificatie, service-URI en versiebeheer.</span><span class="sxs-lookup"><span data-stu-id="d044f-114"><ins>General Information</ins> - Information on authentication, service URI and versioning.</span></span>
* <span data-ttu-id="d044f-115"><ins>Basic model</ins> -API's waarmee u toodo Hallo basisbewerkingen-model (bijvoorbeeld maken, bijwerken en verwijderen van een model).</span><span class="sxs-lookup"><span data-stu-id="d044f-115"><ins>Model Basic</ins> - APIs that enable you toodo hello basic operations on model (e.g. create, update and delete a model).</span></span>
* <span data-ttu-id="d044f-116"><ins>Geavanceerd model</ins> -API's waarmee u geavanceerde tooget gegevens insights Hallo-model.</span><span class="sxs-lookup"><span data-stu-id="d044f-116"><ins>Model Advanced</ins> - APIs that enable you tooget advanced data insights on hello model.</span></span>
* <span data-ttu-id="d044f-117"><ins>Bedrijfsregels model</ins> -API's waarmee u bedrijfsregels toomanage op Hallo model aanbeveling Resultaten.</span><span class="sxs-lookup"><span data-stu-id="d044f-117"><ins>Model Business Rules</ins> - APIs that enable you toomanage business rules on hello model recommendation results.</span></span>
* <span data-ttu-id="d044f-118"><ins>Catalogus</ins> -API's waarmee u toodo basisbewerkingen op een model-catalogus.</span><span class="sxs-lookup"><span data-stu-id="d044f-118"><ins>Catalog</ins> - APIs that enable you toodo basic operations on a model catalog.</span></span> <span data-ttu-id="d044f-119">Een catalogus bevat informatie over de metagegevens op Hallo items van Hallo gebruiksgegevens.</span><span class="sxs-lookup"><span data-stu-id="d044f-119">A catalog contains metadata information on hello items of hello usage data.</span></span>
* <span data-ttu-id="d044f-120"><ins>Functie</ins> -API's waarmee tooget insights op item in de catalogus Hallo en hoe toouse deze informatie toobuild betere aanbevelingen.</span><span class="sxs-lookup"><span data-stu-id="d044f-120"><ins>Feature</ins> - APIs that enable tooget insights on item into hello catalog and how toouse this information toobuild better recommendations.</span></span>
* <span data-ttu-id="d044f-121"><ins>Gebruiksgegevens</ins> -API's waarmee u toodo basisbewerkingen op Hallo model gebruiksgegevens.</span><span class="sxs-lookup"><span data-stu-id="d044f-121"><ins>Usage Data</ins> - APIs that enable you toodo basic operations on hello model usage data.</span></span> <span data-ttu-id="d044f-122">Gebruiksgegevens in elementaire vorm Hallo bestaat uit rijen met paren &#60; userId &#62; &#60; itemId &#62;.</span><span class="sxs-lookup"><span data-stu-id="d044f-122">Usage data in hello basic form consists of rows that include pairs of &#60;userId&#62;,&#60;itemId&#62;.</span></span>
* <span data-ttu-id="d044f-123"><ins>Bouwen</ins> - API's waarmee u een model tootrigger bouwen en bouw basisbewerkingen uit die gerelateerd toothis zijn.</span><span class="sxs-lookup"><span data-stu-id="d044f-123"><ins>Build</ins> - APIs that enable you tootrigger a model build and do basic operations that are related toothis build.</span></span> <span data-ttu-id="d044f-124">Zodra u waardevolle gebruiksgegevens hebt, kunt u een build van het model activeren.</span><span class="sxs-lookup"><span data-stu-id="d044f-124">You can trigger a model build once you have valuable usage data.</span></span>
* <span data-ttu-id="d044f-125"><ins>Aanbeveling</ins> -API's waarmee u tooconsume aanbevelingen als Hallo build van een model is beëindigd.</span><span class="sxs-lookup"><span data-stu-id="d044f-125"><ins>Recommendation</ins> - APIs that enable you tooconsume recommendations once hello build of a model ends.</span></span>
* <span data-ttu-id="d044f-126"><ins>Gebruikersgegevens</ins> -API's waarmee u informatie toofetch van gebruiksgegevens Hallo-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="d044f-126"><ins>User Data</ins> - APIs that enable you toofetch information on hello user usage data.</span></span>
* <span data-ttu-id="d044f-127"><ins>Meldingen</ins> -API's waarmee u tooreceive meldingen op problemen gerelateerde tooyour API-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="d044f-127"><ins>Notifications</ins> - APIs that enable you tooreceive notifications on problems related tooyour API operations.</span></span> <span data-ttu-id="d044f-128">(Bijvoorbeeld, u gebruiksgegevens via overname van gegevens en de meeste Hallo gebeurtenissen verwerken mislukken rapportage.</span><span class="sxs-lookup"><span data-stu-id="d044f-128">(For example, you are reporting usage data via Data Acquisition and most of hello events processing are failing.</span></span> <span data-ttu-id="d044f-129">Een foutmelding weergegeven.)</span><span class="sxs-lookup"><span data-stu-id="d044f-129">An error notification will be raised.)</span></span>

## <a name="2-limitations"></a><span data-ttu-id="d044f-130">2. Beperkingen</span><span class="sxs-lookup"><span data-stu-id="d044f-130">2. Limitations</span></span>
* <span data-ttu-id="d044f-131">Hallo maximumaantal modellen per abonnement is 10.</span><span class="sxs-lookup"><span data-stu-id="d044f-131">hello maximum number of models per subscription is 10.</span></span>
* <span data-ttu-id="d044f-132">maximum aantal builds per model Hallo is 20.</span><span class="sxs-lookup"><span data-stu-id="d044f-132">hello maximum number of builds per model is 20.</span></span>
* <span data-ttu-id="d044f-133">maximum aantal items dat een catalogus kan bevatten Hallo is 100.000.</span><span class="sxs-lookup"><span data-stu-id="d044f-133">hello maximum number of items that a catalog can hold is 100,000.</span></span>
* <span data-ttu-id="d044f-134">maximum aantal gebruik punten die blijven Hallo is ~ 5,000,000.</span><span class="sxs-lookup"><span data-stu-id="d044f-134">hello maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="d044f-135">Hallo oudste worden verwijderd als nieuwe wordt geüpload of gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="d044f-135">hello oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="d044f-136">Hallo maximale grootte van gegevens die kunnen worden verzonden in POST (bijvoorbeeld importeren catalogusgegevens, gebruiksgegevens importeren) is 200MB.</span><span class="sxs-lookup"><span data-stu-id="d044f-136">hello maximum size of data that can be sent in POST (e.g. import catalog data, import usage data) is 200MB.</span></span>
* <span data-ttu-id="d044f-137">maximum aantal items dat kan worden gevraagd om bij het ophalen van aanbevelingen Hallo is 150.</span><span class="sxs-lookup"><span data-stu-id="d044f-137">hello maximum number of items that can be asked for when getting recommendations is 150.</span></span>

## <a name="3-apis---general-information"></a><span data-ttu-id="d044f-138">3. API's - algemene informatie</span><span class="sxs-lookup"><span data-stu-id="d044f-138">3. APIs - general information</span></span>
### <a name="31-authentication"></a><span data-ttu-id="d044f-139">3.1.</span><span class="sxs-lookup"><span data-stu-id="d044f-139">3.1.</span></span> <span data-ttu-id="d044f-140">Authentication</span><span class="sxs-lookup"><span data-stu-id="d044f-140">Authentication</span></span>
<span data-ttu-id="d044f-141">Volg de richtlijnen van Microsoft Azure Marketplace Hallo met betrekking tot verificatie.</span><span class="sxs-lookup"><span data-stu-id="d044f-141">Please follow hello Microsoft Azure Marketplace guidelines regarding authentication.</span></span> <span data-ttu-id="d044f-142">Hallo marketplace biedt ondersteuning voor beide Hallo Basic of OAuth-verificatiemethode.</span><span class="sxs-lookup"><span data-stu-id="d044f-142">hello marketplace supports either hello Basic or OAuth authentication method.</span></span>

### <a name="32-service-uri"></a><span data-ttu-id="d044f-143">3.2.</span><span class="sxs-lookup"><span data-stu-id="d044f-143">3.2.</span></span> <span data-ttu-id="d044f-144">Service-URI</span><span class="sxs-lookup"><span data-stu-id="d044f-144">Service URI</span></span>
<span data-ttu-id="d044f-145">Hallo-hoofdmap URI voor hello Azure Machine Learning aanbevelingen API's is [hier.](https://api.datamarket.azure.com/amla/recommendations/v3/)</span><span class="sxs-lookup"><span data-stu-id="d044f-145">hello service root URI for hello Azure Machine Learning Recommendations APIs is [here.](https://api.datamarket.azure.com/amla/recommendations/v3/)</span></span>

<span data-ttu-id="d044f-146">Hallo volledige service-URI wordt uitgedrukt met behulp van elementen van Hallo OData-specificatie.</span><span class="sxs-lookup"><span data-stu-id="d044f-146">hello full service URI is expressed using elements of hello OData specification.</span></span>  

### <a name="33-api-version"></a><span data-ttu-id="d044f-147">3.3.</span><span class="sxs-lookup"><span data-stu-id="d044f-147">3.3.</span></span> <span data-ttu-id="d044f-148">API-versie</span><span class="sxs-lookup"><span data-stu-id="d044f-148">API version</span></span>
<span data-ttu-id="d044f-149">Elke API-aanroep heeft aan het einde van Hallo een queryparameter apiVersion die moet worden ingesteld als too1.0 aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="d044f-149">Each API call will have, at hello end, a query parameter called apiVersion that should be set too1.0.</span></span>

### <a name="34-ids-are-case-sensitive"></a><span data-ttu-id="d044f-150">3.4.</span><span class="sxs-lookup"><span data-stu-id="d044f-150">3.4.</span></span> <span data-ttu-id="d044f-151">Id's zijn hoofdlettergevoelig</span><span class="sxs-lookup"><span data-stu-id="d044f-151">IDs are case sensitive</span></span>
<span data-ttu-id="d044f-152">Id's die wordt geretourneerd door een van de Hallo-API's, zijn hoofdlettergevoelig en moeten als zodanig worden gebruikt als als parameters doorgegeven in de volgende API-aanroepen.</span><span class="sxs-lookup"><span data-stu-id="d044f-152">IDs, returned by any of hello APIs, are case sensitive and should be used as such when passed as parameters in subsequent API calls.</span></span> <span data-ttu-id="d044f-153">Bijvoorbeeld, zijn model-id's en de catalogus-id's hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="d044f-153">For instance, model IDs and catalog IDs are case sensitive.</span></span>

## <a name="4-recommendations-quality-and-cold-items"></a><span data-ttu-id="d044f-154">4. Aanbevelingen voor kwaliteit en koude Items</span><span class="sxs-lookup"><span data-stu-id="d044f-154">4. Recommendations Quality and Cold Items</span></span>
### <a name="41-recommendation-quality"></a><span data-ttu-id="d044f-155">4.1.</span><span class="sxs-lookup"><span data-stu-id="d044f-155">4.1.</span></span> <span data-ttu-id="d044f-156">Aanbeveling kwaliteit</span><span class="sxs-lookup"><span data-stu-id="d044f-156">Recommendation quality</span></span>
<span data-ttu-id="d044f-157">Maken van een model aanbeveling is meestal voldoende tooallow Hallo system tooprovide aanbevelingen.</span><span class="sxs-lookup"><span data-stu-id="d044f-157">Creating a recommendation model is usually enough tooallow hello system tooprovide recommendations.</span></span> <span data-ttu-id="d044f-158">Evenwel aanbeveling kwaliteit varieert op basis van Hallo gebruik verwerkt en Hallo dekking van Hallo-catalogus.</span><span class="sxs-lookup"><span data-stu-id="d044f-158">Nevertheless, recommendation quality varies based on hello usage processed and hello coverage of hello catalog.</span></span> <span data-ttu-id="d044f-159">Bijvoorbeeld als er een groot aantal koude artikelen (artikelen zonder aanzienlijke gebruik), Hallo systeem problemen bij het leveren van een aanbeveling voor een dergelijke item of een item gebruiken als een aanbevolen zal hebben.</span><span class="sxs-lookup"><span data-stu-id="d044f-159">For example if you have a lot of cold items (items without significant usage), hello system will have difficulties providing a recommendation for such an item or using such an item as a recommended one.</span></span> <span data-ttu-id="d044f-160">In de volgorde tooovercome Hallo koude item probleem staat Hallo systeem Hallo gebruik van metagegevens van Hallo items tooenhance Hallo aanbevelingen.</span><span class="sxs-lookup"><span data-stu-id="d044f-160">In order tooovercome hello cold item problem, hello system allows hello use of metadata of hello items tooenhance hello recommendations.</span></span> <span data-ttu-id="d044f-161">Deze metagegevens is waarnaar wordt verwezen tooas functies.</span><span class="sxs-lookup"><span data-stu-id="d044f-161">This metadata is referred tooas features.</span></span> <span data-ttu-id="d044f-162">Typische functies zijn van een boek auteur of een film actor.</span><span class="sxs-lookup"><span data-stu-id="d044f-162">Typical features are a book's author or a movie's actor.</span></span> <span data-ttu-id="d044f-163">Functies zijn beschikbaar via Hallo catalogus in de vorm Hallo van sleutel/waarde-tekenreeksen.</span><span class="sxs-lookup"><span data-stu-id="d044f-163">Features are provided via hello catalog in hello form of key/value strings.</span></span> <span data-ttu-id="d044f-164">Voor volledige formattering Hallo van catalogusbestand hello, raadpleegt u toohello [sectie catalogus importeren](#81-import-catalog-data).</span><span class="sxs-lookup"><span data-stu-id="d044f-164">For hello full format of hello catalog file, please refer toohello [import catalog section](#81-import-catalog-data).</span></span> 

### <a name="42-rank-build"></a><span data-ttu-id="d044f-165">4.2.</span><span class="sxs-lookup"><span data-stu-id="d044f-165">4.2.</span></span> <span data-ttu-id="d044f-166">Waarden van positie build</span><span class="sxs-lookup"><span data-stu-id="d044f-166">Rank build</span></span>
<span data-ttu-id="d044f-167">Hallo aanbeveling model kunnen verbeteren van functies, maar toodo dus Hallo gebruik van zinvolle functies vereist.</span><span class="sxs-lookup"><span data-stu-id="d044f-167">Features can enhance hello recommendation model, but toodo so requires hello use of meaningful features.</span></span> <span data-ttu-id="d044f-168">Voor dit doel is een nieuwe build geïntroduceerd - positie maken.</span><span class="sxs-lookup"><span data-stu-id="d044f-168">For this purpose a new build was introduced - a rank build.</span></span> <span data-ttu-id="d044f-169">Deze versie wordt Hallo nut van functies rangschikken.</span><span class="sxs-lookup"><span data-stu-id="d044f-169">This build will rank hello usefulness of features.</span></span> <span data-ttu-id="d044f-170">Een functie stukje zinvolle is een functie met een positie score van 2 en omhoog in.</span><span class="sxs-lookup"><span data-stu-id="d044f-170">A meaningful feature is a feature with a rank score of 2 and up.</span></span>
<span data-ttu-id="d044f-171">Na de kennis van die functies Hallo nuttig zijn, een aanbeveling build met lijst hello (of sublijst) van zinvolle functies te activeren.</span><span class="sxs-lookup"><span data-stu-id="d044f-171">After understanding which of hello features are meaningful, trigger a recommendation build with hello list (or sublist) of meaningful features.</span></span> <span data-ttu-id="d044f-172">Het is mogelijk toouse die deze functie voor Hallo uitbreiding van zowel warme en koude artikelen.</span><span class="sxs-lookup"><span data-stu-id="d044f-172">It is possible toouse these feature for hello enhancement of both warm items and cold items.</span></span> <span data-ttu-id="d044f-173">In de volgorde toouse ze voor warme items Hallo `UseFeatureInModel` build-parameter moet worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="d044f-173">In order toouse them for warm items, hello `UseFeatureInModel` build parameter should be set up.</span></span> <span data-ttu-id="d044f-174">In de volgorde toouse functies voor koude items, Hallo `AllowColdItemPlacement` build-parameter moet worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="d044f-174">In order toouse features for cold items, hello `AllowColdItemPlacement` build parameter should be enabled.</span></span>
<span data-ttu-id="d044f-175">Opmerking: Het is niet mogelijk tooenable `AllowColdItemPlacement` zonder in te schakelen `UseFeatureInModel`.</span><span class="sxs-lookup"><span data-stu-id="d044f-175">Note: It is not possible tooenable `AllowColdItemPlacement` without enabling `UseFeatureInModel`.</span></span>

### <a name="43-recommendation-reasoning"></a><span data-ttu-id="d044f-176">4.3.</span><span class="sxs-lookup"><span data-stu-id="d044f-176">4.3.</span></span> <span data-ttu-id="d044f-177">Aanbeveling redenering</span><span class="sxs-lookup"><span data-stu-id="d044f-177">Recommendation reasoning</span></span>
<span data-ttu-id="d044f-178">Aanbeveling redenering is een ander aspect van het gebruik van functies.</span><span class="sxs-lookup"><span data-stu-id="d044f-178">Recommendation reasoning is another aspect of feature usage.</span></span> <span data-ttu-id="d044f-179">Hello Azure Machine Learning aanbevelingen engine kunt functies tooprovide aanbeveling uitleg immers (ook gebruiken</span><span class="sxs-lookup"><span data-stu-id="d044f-179">Indeed, hello Azure Machine Learning Recommendations engine can use features tooprovide recommendation explanations (a.k.a.</span></span> <span data-ttu-id="d044f-180">redeneren), aanbevolen voorloop toomore vertrouwen in Hallo item van Hallo aanbeveling consumer.</span><span class="sxs-lookup"><span data-stu-id="d044f-180">reasoning), leading toomore confidence in hello recommended item from hello recommendation consumer.</span></span>
<span data-ttu-id="d044f-181">tooenable redeneren, hello `AllowFeatureCorrelation` en `ReasoningFeatureList` moeten parameters setup voorafgaande toorequesting een aanbeveling build zijn.</span><span class="sxs-lookup"><span data-stu-id="d044f-181">tooenable reasoning, hello `AllowFeatureCorrelation` and `ReasoningFeatureList` parameters should be setup prior toorequesting a recommendation build.</span></span>

## <a name="5-model-basic"></a><span data-ttu-id="d044f-182">5. Model Basic</span><span class="sxs-lookup"><span data-stu-id="d044f-182">5. Model Basic</span></span>
### <a name="51-create-model"></a><span data-ttu-id="d044f-183">5.1.</span><span class="sxs-lookup"><span data-stu-id="d044f-183">5.1.</span></span> <span data-ttu-id="d044f-184">Model maken</span><span class="sxs-lookup"><span data-stu-id="d044f-184">Create Model</span></span>
<span data-ttu-id="d044f-185">Maakt een aanvraag 'model maken'.</span><span class="sxs-lookup"><span data-stu-id="d044f-185">Creates a “create model” request.</span></span>

| <span data-ttu-id="d044f-186">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-186">HTTP Method</span></span> | <span data-ttu-id="d044f-187">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-187">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-188">VERZENDEN</span><span class="sxs-lookup"><span data-stu-id="d044f-188">POST</span></span> |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="d044f-189">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d044f-189">Example:</span></span><br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| <span data-ttu-id="d044f-190">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-190">Parameter Name</span></span> | <span data-ttu-id="d044f-191">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-191">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-192">modelName</span><span class="sxs-lookup"><span data-stu-id="d044f-192">modelName</span></span> |<span data-ttu-id="d044f-193">Alleen letters (A-Z, a-z), cijfers (0-9), afbreekstreepjes (-) en onderstrepingsteken (_) zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="d044f-193">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="d044f-194">Maximale lengte: 20</span><span class="sxs-lookup"><span data-stu-id="d044f-194">Max length: 20</span></span> |
| <span data-ttu-id="d044f-195">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-195">apiVersion</span></span> |<span data-ttu-id="d044f-196">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-196">1.0</span></span> |
|  | |
| <span data-ttu-id="d044f-197">Aanvraagtekst</span><span class="sxs-lookup"><span data-stu-id="d044f-197">Request Body</span></span> |<span data-ttu-id="d044f-198">GEEN</span><span class="sxs-lookup"><span data-stu-id="d044f-198">NONE</span></span> |

<span data-ttu-id="d044f-199">**Antwoord**:</span><span class="sxs-lookup"><span data-stu-id="d044f-199">**Response**:</span></span>

<span data-ttu-id="d044f-200">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-200">HTTP Status code: 200</span></span>

* <span data-ttu-id="d044f-201">`feed/entry/content/properties/id`-Bevat Hallo model-ID.</span><span class="sxs-lookup"><span data-stu-id="d044f-201">`feed/entry/content/properties/id` - Contains hello model ID.</span></span>
  <span data-ttu-id="d044f-202">**Opmerking**: model-ID is hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="d044f-202">**Note**: model ID is case sensitive.</span></span>

<span data-ttu-id="d044f-203">OData-XML</span><span class="sxs-lookup"><span data-stu-id="d044f-203">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Create A New Model</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:35:21Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">CreateANewModelEntity2</title>
    <updated>2014-10-05T06:35:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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

### <a name="52-get-model"></a><span data-ttu-id="d044f-204">5.2.</span><span class="sxs-lookup"><span data-stu-id="d044f-204">5.2.</span></span> <span data-ttu-id="d044f-205">Model ophalen</span><span class="sxs-lookup"><span data-stu-id="d044f-205">Get Model</span></span>
<span data-ttu-id="d044f-206">Maakt een 'get-model'-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="d044f-206">Creates a “get model” request.</span></span>

| <span data-ttu-id="d044f-207">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-207">HTTP Method</span></span> | <span data-ttu-id="d044f-208">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-208">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-209">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="d044f-209">GET</span></span> |`<rootURI>/GetModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="d044f-210">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d044f-210">Example:</span></span><br>`<rootURI>/GetModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="d044f-211">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-211">Parameter Name</span></span> | <span data-ttu-id="d044f-212">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-212">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-213">id</span><span class="sxs-lookup"><span data-stu-id="d044f-213">id</span></span> |<span data-ttu-id="d044f-214">De unieke id van het Hallo-model (hoofdlettergevoelig)</span><span class="sxs-lookup"><span data-stu-id="d044f-214">Unique identifier of hello model (case sensitive)</span></span> |
| <span data-ttu-id="d044f-215">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-215">apiVersion</span></span> |<span data-ttu-id="d044f-216">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-216">1.0</span></span> |
|  | |
| <span data-ttu-id="d044f-217">Aanvraagtekst</span><span class="sxs-lookup"><span data-stu-id="d044f-217">Request Body</span></span> |<span data-ttu-id="d044f-218">GEEN</span><span class="sxs-lookup"><span data-stu-id="d044f-218">NONE</span></span> |

<span data-ttu-id="d044f-219">**Antwoord**:</span><span class="sxs-lookup"><span data-stu-id="d044f-219">**Response**:</span></span>

<span data-ttu-id="d044f-220">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-220">HTTP Status code: 200</span></span>

<span data-ttu-id="d044f-221">Hallo modelgegevens vindt u onder Hallo volgende elementen:</span><span class="sxs-lookup"><span data-stu-id="d044f-221">hello model data can be found under hello following elements:</span></span>

* <span data-ttu-id="d044f-222">`feed/entry/content/properties/Id`-De unieke id model.</span><span class="sxs-lookup"><span data-stu-id="d044f-222">`feed/entry/content/properties/Id` - Model unique ID.</span></span>
* <span data-ttu-id="d044f-223">`feed/entry/content/properties/Name`-Naam model.</span><span class="sxs-lookup"><span data-stu-id="d044f-223">`feed/entry/content/properties/Name` - Model name.</span></span>
* <span data-ttu-id="d044f-224">`feed/entry/content/properties/Date`-Aanmaakdatum model.</span><span class="sxs-lookup"><span data-stu-id="d044f-224">`feed/entry/content/properties/Date` - Model creation date.</span></span>
* <span data-ttu-id="d044f-225">`feed/entry/content/properties/Status`-Status van het model.</span><span class="sxs-lookup"><span data-stu-id="d044f-225">`feed/entry/content/properties/Status` - Model status.</span></span> <span data-ttu-id="d044f-226">Een van de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="d044f-226">One of hello following:</span></span>
  * <span data-ttu-id="d044f-227">Gemaakt - Model wordt gemaakt en bevat geen catalogus en informatie over het gebruik.</span><span class="sxs-lookup"><span data-stu-id="d044f-227">Created - Model is created and does not contain Catalog and Usage.</span></span>
  * <span data-ttu-id="d044f-228">ReadyForBuild - Model wordt gemaakt en bevat Catalog en het gebruik.</span><span class="sxs-lookup"><span data-stu-id="d044f-228">ReadyForBuild - Model is created and contains Catalog and Usage.</span></span>
* <span data-ttu-id="d044f-229">`feed/entry/content/properties/HasActiveBuild`-Geeft aan of Hallo model is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d044f-229">`feed/entry/content/properties/HasActiveBuild` - Indicates if hello model was built successfully.</span></span>
* <span data-ttu-id="d044f-230">`feed/entry/content/properties/BuildId`-Model active build-ID.</span><span class="sxs-lookup"><span data-stu-id="d044f-230">`feed/entry/content/properties/BuildId` - Model active build ID.</span></span>
* <span data-ttu-id="d044f-231">`feed/entry/content/properties/Mpr`-Gemiddelde percentiel ranking model (MPR - ModelInsight Zie voor meer informatie).</span><span class="sxs-lookup"><span data-stu-id="d044f-231">`feed/entry/content/properties/Mpr` - Model mean percentile ranking (MPR - see ModelInsight for more information).</span></span>
* <span data-ttu-id="d044f-232">`feed/entry/content/properties/UserName`-Naam van de interne gebruiker model.</span><span class="sxs-lookup"><span data-stu-id="d044f-232">`feed/entry/content/properties/UserName` - Model internal user name.</span></span>

<span data-ttu-id="d044f-233">OData-XML</span><span class="sxs-lookup"><span data-stu-id="d044f-233">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get A List Of All Models</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-28T14:35:51Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetAListOfAllModelsEntity</title>
    <updated>2014-10-28T14:35:51Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">68b232f2-1037-45f7-8f49-af822695ee63</d:Id>
        <d:Name m:type="Edm.String">vah-11111</d:Name>
        <d:Date m:type="Edm.String">10/28/2014 2:16:07 PM</d:Date>
        <d:Status m:type="Edm.String">ReadyForBuild</d:Status>
        <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
        <d:BuildId m:type="Edm.String">-1</d:BuildId>
        <d:Mpr m:type="Edm.String">0</d:Mpr>
        <d:UsageFileNames m:type="Edm.String">ImplicitMatrix10_Guid_small.txt, ImplicitMatrix11_Guid_small.txt</d:UsageFileNames>
        <d:CatalogId m:type="Edm.String">626babdb-cab6-43a6-82ef-4fb86345700c</d:CatalogId>
        <d:UserName m:type="Edm.String">89dc4722-03ba-4f90-8821-b1db388408b5@dm.com</d:UserName>
        <d:Description m:type="Edm.String">short description</d:Description>
        <d:CatalogFileName m:type="Edm.String">catalog10_small.txt</d:CatalogFileName>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="53----get-all-models"></a><span data-ttu-id="d044f-234">5.3.</span><span class="sxs-lookup"><span data-stu-id="d044f-234">5.3.</span></span>    <span data-ttu-id="d044f-235">Ophalen van alle modellen</span><span class="sxs-lookup"><span data-stu-id="d044f-235">Get All Models</span></span>
<span data-ttu-id="d044f-236">Hiermee haalt u alle modellen van de huidige gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="d044f-236">Retrieves all models of hello current user.</span></span>

| <span data-ttu-id="d044f-237">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-237">HTTP Method</span></span> | <span data-ttu-id="d044f-238">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-238">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-239">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="d044f-239">GET</span></span> |`<rootURI>/GetAllModels?apiVersion=%271.0%27`<br><span data-ttu-id="d044f-240">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d044f-240">Example:</span></span><br>`<rootURI>/GetAllModels?apiVersion=%271.0%27` |

| <span data-ttu-id="d044f-241">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-241">Parameter Name</span></span> | <span data-ttu-id="d044f-242">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-242">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-243">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-243">apiVersion</span></span> |<span data-ttu-id="d044f-244">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-244">1.0</span></span> |
|  | |
| <span data-ttu-id="d044f-245">Aanvraagtekst</span><span class="sxs-lookup"><span data-stu-id="d044f-245">Request Body</span></span> |<span data-ttu-id="d044f-246">GEEN</span><span class="sxs-lookup"><span data-stu-id="d044f-246">NONE</span></span> |

<span data-ttu-id="d044f-247">**Antwoord**:</span><span class="sxs-lookup"><span data-stu-id="d044f-247">**Response**:</span></span>

<span data-ttu-id="d044f-248">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-248">HTTP Status code: 200</span></span>

* <span data-ttu-id="d044f-249">`feed/entry/content/properties/Id`-De unieke id model.</span><span class="sxs-lookup"><span data-stu-id="d044f-249">`feed/entry/content/properties/Id` - Model unique ID.</span></span>
* <span data-ttu-id="d044f-250">`feed/entry/content/properties/Name`-Naam model.</span><span class="sxs-lookup"><span data-stu-id="d044f-250">`feed/entry/content/properties/Name` - Model name.</span></span>
* <span data-ttu-id="d044f-251">`feed/entry/content/properties/Date`-Aanmaakdatum model.</span><span class="sxs-lookup"><span data-stu-id="d044f-251">`feed/entry/content/properties/Date` - Model creation date.</span></span>
* <span data-ttu-id="d044f-252">`feed/entry/content/properties/Status`-Status van het model.</span><span class="sxs-lookup"><span data-stu-id="d044f-252">`feed/entry/content/properties/Status` - Model status.</span></span> <span data-ttu-id="d044f-253">Een van de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="d044f-253">One of hello following:</span></span>
  * <span data-ttu-id="d044f-254">Gemaakt - Model wordt gemaakt en bevat geen catalogus en informatie over het gebruik.</span><span class="sxs-lookup"><span data-stu-id="d044f-254">Created - Model is created and does not contain Catalog and Usage.</span></span>
  * <span data-ttu-id="d044f-255">ReadyForBuild - Model wordt gemaakt en bevat Catalog en het gebruik.</span><span class="sxs-lookup"><span data-stu-id="d044f-255">ReadyForBuild - Model is created and contains Catalog and Usage.</span></span>
* <span data-ttu-id="d044f-256">`feed/entry/content/properties/HasActiveBuild`-Geeft aan of Hallo model is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d044f-256">`feed/entry/content/properties/HasActiveBuild` - Indicates if hello model was built successfully.</span></span>
* <span data-ttu-id="d044f-257">`feed/entry/content/properties/BuildId`-Model active build-ID.</span><span class="sxs-lookup"><span data-stu-id="d044f-257">`feed/entry/content/properties/BuildId` - Model active build ID.</span></span>
* <span data-ttu-id="d044f-258">`feed/entry/content/properties/Mpr`-Model MPR (Zie ModelInsight voor meer informatie).</span><span class="sxs-lookup"><span data-stu-id="d044f-258">`feed/entry/content/properties/Mpr` - Model MPR (see ModelInsight for more information).</span></span>
* <span data-ttu-id="d044f-259">`feed/entry/content/properties/UserName`-Naam van de interne gebruiker model.</span><span class="sxs-lookup"><span data-stu-id="d044f-259">`feed/entry/content/properties/UserName` - Model internal user name.</span></span>
* <span data-ttu-id="d044f-260">`feed/entry/content/properties/UsageFileNames`-Lijst met informatie over het gebruik van modelbestanden gescheiden door komma.</span><span class="sxs-lookup"><span data-stu-id="d044f-260">`feed/entry/content/properties/UsageFileNames` - List of model usage files separated by comma.</span></span>
* <span data-ttu-id="d044f-261">`feed/entry/content/properties/CatalogId`-Model catalogus-ID.</span><span class="sxs-lookup"><span data-stu-id="d044f-261">`feed/entry/content/properties/CatalogId` - Model catalog ID.</span></span>
* <span data-ttu-id="d044f-262">`feed/entry/content/properties/Description`-Beschrijving model.</span><span class="sxs-lookup"><span data-stu-id="d044f-262">`feed/entry/content/properties/Description` - Model description.</span></span>
* <span data-ttu-id="d044f-263">`feed/entry/content/properties/CatalogFileName`-Bestandsnaam van de model catalogus.</span><span class="sxs-lookup"><span data-stu-id="d044f-263">`feed/entry/content/properties/CatalogFileName` - Model catalog file name.</span></span>

<span data-ttu-id="d044f-264">OData-XML</span><span class="sxs-lookup"><span data-stu-id="d044f-264">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get A List Of All Models</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-28T14:35:51Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfAllModelsEntity</title>
    <updated>2014-10-28T14:35:51Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Id m:type="Edm.String">68b232f2-1037-45f7-8f49-af822695ee63</d:Id>
                    <d:Name m:type="Edm.String">vah-11111</d:Name>
                    <d:Date m:type="Edm.String">10/28/2014 2:16:07 PM</d:Date>
                    <d:Status m:type="Edm.String">ReadyForBuild</d:Status>
                    <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
                    <d:BuildId m:type="Edm.String">-1</d:BuildId>
                    <d:Mpr m:type="Edm.String">0</d:Mpr>
                    <d:UsageFileNames m:type="Edm.String">ImplicitMatrix10_Guid_small.txt, ImplicitMatrix11_Guid_small.txt</d:UsageFileNames>
                    <d:CatalogId m:type="Edm.String">626babdb-cab6-43a6-82ef-4fb86345700c</d:CatalogId>
                    <d:UserName m:type="Edm.String">89dc4722-03ba-4f90-8821-b1db388408b5@dm.com</d:UserName>
                    <d:Description m:type="Edm.String">short description</d:Description>
                    <d:CatalogFileName m:type="Edm.String">catalog10_small.txt</d:CatalogFileName>
                </m:properties>
            </content>
        </entry>
    </feed>

### <a name="54----update-model"></a><span data-ttu-id="d044f-265">5.4.</span><span class="sxs-lookup"><span data-stu-id="d044f-265">5.4.</span></span>    <span data-ttu-id="d044f-266">Model bijwerken</span><span class="sxs-lookup"><span data-stu-id="d044f-266">Update Model</span></span>
<span data-ttu-id="d044f-267">U kunt Hallo Modelbeschrijving van update of Hallo active build-ID.</span><span class="sxs-lookup"><span data-stu-id="d044f-267">You can update hello model description or hello active build ID.</span></span><br><span data-ttu-id="d044f-268">
<ins>ID van de actieve build</ins> -elke build voor elk model heeft een build-ID.</span><span class="sxs-lookup"><span data-stu-id="d044f-268">
<ins>Active build ID</ins> - Every build for every model has a build ID.</span></span> <span data-ttu-id="d044f-269">Hallo active build-ID is Hallo eerste geslaagde build van elke nieuwe model.</span><span class="sxs-lookup"><span data-stu-id="d044f-269">hello active build ID is hello first successful build of every new model.</span></span> <span data-ttu-id="d044f-270">Wanneer u een actieve build-ID hebt en u extra builds voor Hallo doen hetzelfde model, moet u tooexplicitly ingesteld dat deze zoals hello standaard bouwen ID als u wilt.</span><span class="sxs-lookup"><span data-stu-id="d044f-270">Once you have an active build ID and you do additional builds for hello same model, you need tooexplicitly set it as hello default build ID if you want to.</span></span> <span data-ttu-id="d044f-271">Wanneer u aanbevelingen gebruiken als u geen opgeeft Hallo build-ID die u wilt dat toouse, Hallo standaard één automatisch zal worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d044f-271">When you consume recommendations, if you do not specify hello build ID that you want toouse, hello default one will be used automatically.</span></span><br>
<span data-ttu-id="d044f-272">Dit mechanisme kunt u - zodra u een aanbeveling-model in productie - toobuild nieuwe modellen hebt en te testen voordat u ze promoveert tooproduction.</span><span class="sxs-lookup"><span data-stu-id="d044f-272">This mechanism enables you - once you have a recommendation model in production - toobuild new models and test them before you promote them tooproduction.</span></span>

| <span data-ttu-id="d044f-273">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-273">HTTP Method</span></span> | <span data-ttu-id="d044f-274">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-274">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-275">PLAATSEN</span><span class="sxs-lookup"><span data-stu-id="d044f-275">PUT</span></span> |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br><span data-ttu-id="d044f-276">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d044f-276">Example:</span></span><br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| <span data-ttu-id="d044f-277">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-277">Parameter Name</span></span> | <span data-ttu-id="d044f-278">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-278">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-279">id</span><span class="sxs-lookup"><span data-stu-id="d044f-279">id</span></span> |<span data-ttu-id="d044f-280">De unieke id van het Hallo-model (hoofdlettergevoelig)</span><span class="sxs-lookup"><span data-stu-id="d044f-280">Unique identifier of hello model (case sensitive)</span></span> |
| <span data-ttu-id="d044f-281">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-281">apiVersion</span></span> |<span data-ttu-id="d044f-282">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-282">1.0</span></span> |
|  | |
| <span data-ttu-id="d044f-283">Aanvraagtekst</span><span class="sxs-lookup"><span data-stu-id="d044f-283">Request Body</span></span> |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`<Description>New Description</Description>`<br>`<ActiveBuildId>-1</ActiveBuildId>`<br>` </ModelUpdateParams>`<br><br><span data-ttu-id="d044f-284">Houd er rekening mee dat Hallo XML-beschrijving tags en ActiveBuildId zijn optioneel.</span><span class="sxs-lookup"><span data-stu-id="d044f-284">Note that hello XML tags Description and ActiveBuildId are optional.</span></span> <span data-ttu-id="d044f-285">Als u niet dat tooset beschrijving of ActiveBuildId wilt, moet u de volledige code Hallo verwijderen.</span><span class="sxs-lookup"><span data-stu-id="d044f-285">If you do not want tooset Description or ActiveBuildId, remove hello entire tag.</span></span> |

<span data-ttu-id="d044f-286">**Antwoord**:</span><span class="sxs-lookup"><span data-stu-id="d044f-286">**Response**:</span></span>

<span data-ttu-id="d044f-287">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-287">HTTP Status code: 200</span></span>

### <a name="55----delete-model"></a><span data-ttu-id="d044f-288">5.5.</span><span class="sxs-lookup"><span data-stu-id="d044f-288">5.5.</span></span>    <span data-ttu-id="d044f-289">Model verwijderen</span><span class="sxs-lookup"><span data-stu-id="d044f-289">Delete Model</span></span>
<span data-ttu-id="d044f-290">Hiermee verwijdert u een bestaand model op-ID.</span><span class="sxs-lookup"><span data-stu-id="d044f-290">Deletes an existing model by ID.</span></span>

| <span data-ttu-id="d044f-291">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-291">HTTP Method</span></span> | <span data-ttu-id="d044f-292">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-292">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-293">VERWIJDEREN</span><span class="sxs-lookup"><span data-stu-id="d044f-293">DELETE</span></span> |`<rootURI>/DeleteModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="d044f-294">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d044f-294">Example:</span></span><br>`<rootURI>/DeleteModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="d044f-295">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-295">Parameter Name</span></span> | <span data-ttu-id="d044f-296">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-296">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-297">id</span><span class="sxs-lookup"><span data-stu-id="d044f-297">id</span></span> |<span data-ttu-id="d044f-298">De unieke id van het Hallo-model (hoofdlettergevoelig)</span><span class="sxs-lookup"><span data-stu-id="d044f-298">Unique identifier of hello model (case sensitive)</span></span> |
| <span data-ttu-id="d044f-299">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-299">apiVersion</span></span> |<span data-ttu-id="d044f-300">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-300">1.0</span></span> |
|  | |
| <span data-ttu-id="d044f-301">Aanvraagtekst</span><span class="sxs-lookup"><span data-stu-id="d044f-301">Request Body</span></span> |<span data-ttu-id="d044f-302">GEEN</span><span class="sxs-lookup"><span data-stu-id="d044f-302">NONE</span></span> |

<span data-ttu-id="d044f-303">**Antwoord**:</span><span class="sxs-lookup"><span data-stu-id="d044f-303">**Response**:</span></span>

<span data-ttu-id="d044f-304">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-304">HTTP Status code: 200</span></span>

<span data-ttu-id="d044f-305">OData-XML</span><span class="sxs-lookup"><span data-stu-id="d044f-305">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Delete Model by Id</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-28T10:39:33Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">DeleteModelByIdEntity</title>
    <updated>2014-10-28T10:39:33Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:string m:type="Edm.String"></d:string>
      </m:properties>
    </content>
      </entry>
    </feed>

## <a name="6-model-advanced"></a><span data-ttu-id="d044f-306">6. Geavanceerde model</span><span class="sxs-lookup"><span data-stu-id="d044f-306">6. Model Advanced</span></span>
### <a name="61----model-data-insight"></a><span data-ttu-id="d044f-307">6.1.</span><span class="sxs-lookup"><span data-stu-id="d044f-307">6.1.</span></span>    <span data-ttu-id="d044f-308">Model Data-inzicht</span><span class="sxs-lookup"><span data-stu-id="d044f-308">Model Data Insight</span></span>
<span data-ttu-id="d044f-309">Retourneert de statistische gegevens op Hallo gebruiksgegevens die met dit model is gebouwd.</span><span class="sxs-lookup"><span data-stu-id="d044f-309">Returns statistical data on hello usage data that this model was built with.</span></span>

<span data-ttu-id="d044f-310">Alleen beschikbaar voor aanbeveling build.</span><span class="sxs-lookup"><span data-stu-id="d044f-310">Available only for Recommendation build.</span></span>

| <span data-ttu-id="d044f-311">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-311">HTTP Method</span></span> | <span data-ttu-id="d044f-312">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-312">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-313">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="d044f-313">GET</span></span> |`<rootURI>/GetDataInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="d044f-314">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d044f-314">Example:</span></span><br>`<rootURI>/GetDataInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="d044f-315">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-315">Parameter Name</span></span> | <span data-ttu-id="d044f-316">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-316">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-317">Model</span><span class="sxs-lookup"><span data-stu-id="d044f-317">modelId</span></span> |<span data-ttu-id="d044f-318">De unieke id van het Hallo-model</span><span class="sxs-lookup"><span data-stu-id="d044f-318">Unique identifier of hello model</span></span> |
| <span data-ttu-id="d044f-319">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-319">apiVersion</span></span> |<span data-ttu-id="d044f-320">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-320">1.0</span></span> |
|  | |
| <span data-ttu-id="d044f-321">Aanvraagtekst</span><span class="sxs-lookup"><span data-stu-id="d044f-321">Request Body</span></span> |<span data-ttu-id="d044f-322">GEEN</span><span class="sxs-lookup"><span data-stu-id="d044f-322">NONE</span></span> |

<span data-ttu-id="d044f-323">**Antwoord**:</span><span class="sxs-lookup"><span data-stu-id="d044f-323">**Response**:</span></span>

<span data-ttu-id="d044f-324">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-324">HTTP Status code: 200</span></span>

<span data-ttu-id="d044f-325">Hallo-gegevens worden geretourneerd als een verzameling eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="d044f-325">hello data is returned as a collection of properties.</span></span>

* <span data-ttu-id="d044f-326">`feed/entry/id/content/properties/key`-De naam van de eigenschap Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="d044f-326">`feed/entry/id/content/properties/key` - Holds hello property name.</span></span>
* <span data-ttu-id="d044f-327">`feed/entry/id/content/properties/value`-Eigenschapswaarde Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="d044f-327">`feed/entry/id/content/properties/value` - Holds hello property value.</span></span>

<span data-ttu-id="d044f-328">Hallo in de volgende tabel beschrijft Hallo-waarde die aangeeft voor elke sleutel.</span><span class="sxs-lookup"><span data-stu-id="d044f-328">hello table below depicts hello value that each key represents.</span></span>

| <span data-ttu-id="d044f-329">Sleutel</span><span class="sxs-lookup"><span data-stu-id="d044f-329">Key</span></span> | <span data-ttu-id="d044f-330">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d044f-330">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-331">AvgItemLength</span><span class="sxs-lookup"><span data-stu-id="d044f-331">AvgItemLength</span></span> |<span data-ttu-id="d044f-332">Gemiddeld aantal unieke gebruikers per artikel.</span><span class="sxs-lookup"><span data-stu-id="d044f-332">Average number of distinct users per item.</span></span> |
| <span data-ttu-id="d044f-333">AvgUserLength</span><span class="sxs-lookup"><span data-stu-id="d044f-333">AvgUserLength</span></span> |<span data-ttu-id="d044f-334">Gemiddelde aantal afzonderlijke items per gebruiker.</span><span class="sxs-lookup"><span data-stu-id="d044f-334">Average number of distinct items per user.</span></span> |
| <span data-ttu-id="d044f-335">DensificationNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="d044f-335">DensificationNumberOfItems</span></span> |<span data-ttu-id="d044f-336">Aantal items na weghalen items die niet kunnen worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="d044f-336">Number of items after pruning items that cannot be modelled.</span></span> |
| <span data-ttu-id="d044f-337">DensificationNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="d044f-337">DensificationNumberOfUsers</span></span> |<span data-ttu-id="d044f-338">Aantal punten gebruik na weghalen gebruikers en de items die niet kunnen worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="d044f-338">Number of usage points after pruning users and items that can't be modelled.</span></span> |
| <span data-ttu-id="d044f-339">DensificationNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="d044f-339">DensificationNumberOfRecords</span></span> |<span data-ttu-id="d044f-340">Aantal punten gebruik na weghalen gebruikers en de items die niet kunnen worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="d044f-340">Number of usage points after pruning users and items that can't be modelled.</span></span> |
| <span data-ttu-id="d044f-341">MaxItemLength</span><span class="sxs-lookup"><span data-stu-id="d044f-341">MaxItemLength</span></span> |<span data-ttu-id="d044f-342">Het aantal afzonderlijke gebruikers voor de meest populaire item Hallo.</span><span class="sxs-lookup"><span data-stu-id="d044f-342">Number of distinct users for hello most popular item.</span></span> |
| <span data-ttu-id="d044f-343">MaxUserLength</span><span class="sxs-lookup"><span data-stu-id="d044f-343">MaxUserLength</span></span> |<span data-ttu-id="d044f-344">Maximale aantal afzonderlijke items voor een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="d044f-344">Maximal number of distinct items for a user.</span></span> |
| <span data-ttu-id="d044f-345">MinItemLength</span><span class="sxs-lookup"><span data-stu-id="d044f-345">MinItemLength</span></span> |<span data-ttu-id="d044f-346">Maximale aantal van afzonderlijke gebruikers voor een item.</span><span class="sxs-lookup"><span data-stu-id="d044f-346">Maximal number of distinct users for an item.</span></span> |
| <span data-ttu-id="d044f-347">MinUserLength</span><span class="sxs-lookup"><span data-stu-id="d044f-347">MinUserLength</span></span> |<span data-ttu-id="d044f-348">Minimum aantal afzonderlijke items voor een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="d044f-348">Minimal number of distinct items for a user.</span></span> |
| <span data-ttu-id="d044f-349">RawNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="d044f-349">RawNumberOfItems</span></span> |<span data-ttu-id="d044f-350">Het aantal items in Hallo gebruiksbestanden.</span><span class="sxs-lookup"><span data-stu-id="d044f-350">Number of items in hello usage files.</span></span> |
| <span data-ttu-id="d044f-351">RawNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="d044f-351">RawNumberOfUsers</span></span> |<span data-ttu-id="d044f-352">Aantal punten voordat alle weghalen gebruik.</span><span class="sxs-lookup"><span data-stu-id="d044f-352">Number of usage points before any pruning.</span></span> |
| <span data-ttu-id="d044f-353">RawNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="d044f-353">RawNumberOfRecords</span></span> |<span data-ttu-id="d044f-354">Aantal punten voordat alle weghalen gebruik.</span><span class="sxs-lookup"><span data-stu-id="d044f-354">Number of usage points before any pruning.</span></span> |
| <span data-ttu-id="d044f-355">SamplingNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="d044f-355">SamplingNumberOfItems</span></span> |<span data-ttu-id="d044f-356">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="d044f-356">N/A</span></span> |
| <span data-ttu-id="d044f-357">SamplingNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="d044f-357">SamplingNumberOfRecords</span></span> |<span data-ttu-id="d044f-358">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="d044f-358">N/A</span></span> |
| <span data-ttu-id="d044f-359">SamplingNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="d044f-359">SamplingNumberOfUsers</span></span> |<span data-ttu-id="d044f-360">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="d044f-360">N/A</span></span> |

<span data-ttu-id="d044f-361">OData-XML</span><span class="sxs-lookup"><span data-stu-id="d044f-361">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get data insight statistics</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'" />
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">AvgItemLength</d:Key>
        <d:Value m:type="Edm.String">18.936</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">AvgUserLength</d:Key>
        <d:Value m:type="Edm.String">51.879</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">DensificationNumberOfItems</d:Key>
        <d:Value m:type="Edm.String">2,000</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">DensificationNumberOfRecords</d:Key>
        <d:Value m:type="Edm.String">37,872</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
    <content type="application/xml">
        <m:properties>
            <d:Key m:type="Edm.String">DensificationNumberOfUsers</d:Key>
            <d:Value m:type="Edm.String">730</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MaxItemLength</d:Key>
                <d:Value m:type="Edm.String">4,704</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MaxUserLength</d:Key>
                <d:Value m:type="Edm.String">190</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MinItemLength</d:Key>
                <d:Value m:type="Edm.String">8</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MinUserLength</d:Key>
                <d:Value m:type="Edm.String">20</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfItems</d:Key>
                <d:Value m:type="Edm.String">2,000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfRecords</d:Key>
                <d:Value m:type="Edm.String">72,022</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfUsers</d:Key>
                <d:Value m:type="Edm.String">9,044</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfItems</d:Key>
                <d:Value m:type="Edm.String">2,000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=13&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=13&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfRecords</d:Key>
                <d:Value m:type="Edm.String">72,022</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=14&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=14&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfUsers</d:Key>
                <d:Value m:type="Edm.String">9,044</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="62----model-insight"></a><span data-ttu-id="d044f-362">6.2.</span><span class="sxs-lookup"><span data-stu-id="d044f-362">6.2.</span></span>    <span data-ttu-id="d044f-363">Model inzicht</span><span class="sxs-lookup"><span data-stu-id="d044f-363">Model Insight</span></span>
<span data-ttu-id="d044f-364">Retourneert model inzicht op Hallo active build of (indien opgegeven) een specifieke versie.</span><span class="sxs-lookup"><span data-stu-id="d044f-364">Returns model insight on hello active build or (if given) on a specific build.</span></span>

<span data-ttu-id="d044f-365">Alleen beschikbaar voor aanbeveling build.</span><span class="sxs-lookup"><span data-stu-id="d044f-365">Available only for Recommendation build.</span></span>

| <span data-ttu-id="d044f-366">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-366">HTTP Method</span></span> | <span data-ttu-id="d044f-367">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-367">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-368">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="d044f-368">GET</span></span> |<span data-ttu-id="d044f-369">Met de ID van de actieve build:</span><span class="sxs-lookup"><span data-stu-id="d044f-369">With active build ID:</span></span><br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="d044f-370">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d044f-370">Example:</span></span><br>`<rootURI>/GetModelInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="d044f-371">Met specifieke build-ID:</span><span class="sxs-lookup"><span data-stu-id="d044f-371">With specific build ID:</span></span><br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27` |

| <span data-ttu-id="d044f-372">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-372">Parameter Name</span></span> | <span data-ttu-id="d044f-373">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-373">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-374">Model</span><span class="sxs-lookup"><span data-stu-id="d044f-374">modelId</span></span> |<span data-ttu-id="d044f-375">De unieke id van het Hallo-model</span><span class="sxs-lookup"><span data-stu-id="d044f-375">Unique identifier of hello model</span></span> |
| <span data-ttu-id="d044f-376">buildId</span><span class="sxs-lookup"><span data-stu-id="d044f-376">buildId</span></span> |<span data-ttu-id="d044f-377">Optioneel - nummer waarmee een geslaagde build.</span><span class="sxs-lookup"><span data-stu-id="d044f-377">Optional - number that identifies a successful build.</span></span> |
| <span data-ttu-id="d044f-378">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-378">apiVersion</span></span> |<span data-ttu-id="d044f-379">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-379">1.0</span></span> |
|  | |
| <span data-ttu-id="d044f-380">Aanvraagtekst</span><span class="sxs-lookup"><span data-stu-id="d044f-380">Request Body</span></span> |<span data-ttu-id="d044f-381">GEEN</span><span class="sxs-lookup"><span data-stu-id="d044f-381">NONE</span></span> |

<span data-ttu-id="d044f-382">**Antwoord**:</span><span class="sxs-lookup"><span data-stu-id="d044f-382">**Response**:</span></span>

<span data-ttu-id="d044f-383">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-383">HTTP Status code: 200</span></span>

<span data-ttu-id="d044f-384">Hallo-gegevens worden geretourneerd als een verzameling eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="d044f-384">hello data is returned as a collection of properties.</span></span>

* `feed/entry/id/content/properties/key`
* `feed/entry/id/content/properties/value`

<span data-ttu-id="d044f-385">Hallo in de volgende tabel beschrijft Hallo-waarde die aangeeft voor elke sleutel.</span><span class="sxs-lookup"><span data-stu-id="d044f-385">hello table below depicts hello value that each key represents.</span></span>

| <span data-ttu-id="d044f-386">Sleutel</span><span class="sxs-lookup"><span data-stu-id="d044f-386">Key</span></span> | <span data-ttu-id="d044f-387">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d044f-387">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-388">CatalogCoverage</span><span class="sxs-lookup"><span data-stu-id="d044f-388">CatalogCoverage</span></span> |<span data-ttu-id="d044f-389">Welk gedeelte van de catalogus Hallo kan worden gebracht met gebruikspatronen.</span><span class="sxs-lookup"><span data-stu-id="d044f-389">What part of hello catalog can be modelled with usage patterns.</span></span> <span data-ttu-id="d044f-390">Hallo rest Hallo items moet functies op basis van inhoud.</span><span class="sxs-lookup"><span data-stu-id="d044f-390">hello rest of hello items will need content-based features.</span></span> |
| <span data-ttu-id="d044f-391">MPR</span><span class="sxs-lookup"><span data-stu-id="d044f-391">Mpr</span></span> |<span data-ttu-id="d044f-392">Gemiddelde percentiel rangschikking van Hallo-model.</span><span class="sxs-lookup"><span data-stu-id="d044f-392">Mean percentile ranking of hello model.</span></span> <span data-ttu-id="d044f-393">Kleine is beter.</span><span class="sxs-lookup"><span data-stu-id="d044f-393">Lower is better.</span></span> |
| <span data-ttu-id="d044f-394">NumberOfDimensions</span><span class="sxs-lookup"><span data-stu-id="d044f-394">NumberOfDimensions</span></span> |<span data-ttu-id="d044f-395">Het aantal dimensies die worden gebruikt door Hallo matrix factoriseren algoritme.</span><span class="sxs-lookup"><span data-stu-id="d044f-395">Number of dimensions used by hello matrix factorization algorithm.</span></span> |

<span data-ttu-id="d044f-396">OData-XML</span><span class="sxs-lookup"><span data-stu-id="d044f-396">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get model insight statistics</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-27T14:27:11Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">CatalogCoverage</d:Key>
                <d:Value m:type="Edm.String">1.000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">Mpr</d:Key>
                <d:Value m:type="Edm.String">0.367</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">NumberOfDimensions</d:Key>
                <d:Value m:type="Edm.String">20</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="63----get-model-sample"></a><span data-ttu-id="d044f-397">6.3.</span><span class="sxs-lookup"><span data-stu-id="d044f-397">6.3.</span></span>    <span data-ttu-id="d044f-398">Model Sample ophalen</span><span class="sxs-lookup"><span data-stu-id="d044f-398">Get Model Sample</span></span>
<span data-ttu-id="d044f-399">Hiermee haalt u een voorbeeld van Hallo aanbeveling model.</span><span class="sxs-lookup"><span data-stu-id="d044f-399">Gets a sample of hello recommendation model.</span></span>

| <span data-ttu-id="d044f-400">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-400">HTTP Method</span></span> | <span data-ttu-id="d044f-401">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-401">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-402">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="d044f-402">GET</span></span> |`<rootURI>/GetModelSample?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="d044f-403">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d044f-403">Example:</span></span><br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="d044f-404">Met specifieke build-ID:</span><span class="sxs-lookup"><span data-stu-id="d044f-404">With specific build ID:</span></span><br>`<rootURI>/GetModelSample?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="d044f-405">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d044f-405">Example:</span></span><br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&buildId=%271500068%27&apiVersion=%271.0%27` |

| <span data-ttu-id="d044f-406">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-406">Parameter Name</span></span> | <span data-ttu-id="d044f-407">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-407">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-408">Model</span><span class="sxs-lookup"><span data-stu-id="d044f-408">modelId</span></span> |<span data-ttu-id="d044f-409">De unieke id van het Hallo-model</span><span class="sxs-lookup"><span data-stu-id="d044f-409">Unique identifier of hello model</span></span> |
| <span data-ttu-id="d044f-410">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-410">apiVersion</span></span> |<span data-ttu-id="d044f-411">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-411">1.0</span></span> |
|  | |
| <span data-ttu-id="d044f-412">Aanvraagtekst</span><span class="sxs-lookup"><span data-stu-id="d044f-412">Request Body</span></span> |<span data-ttu-id="d044f-413">GEEN</span><span class="sxs-lookup"><span data-stu-id="d044f-413">NONE</span></span> |

<span data-ttu-id="d044f-414">**Antwoord**:</span><span class="sxs-lookup"><span data-stu-id="d044f-414">**Response**:</span></span>

<span data-ttu-id="d044f-415">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-415">HTTP Status code: 200</span></span>

<span data-ttu-id="d044f-416">OData-XML</span><span class="sxs-lookup"><span data-stu-id="d044f-416">OData XML</span></span>

<span data-ttu-id="d044f-417">Onbewerkte tekst wordt geretourneerd als antwoord:</span><span class="sxs-lookup"><span data-stu-id="d044f-417">Response is returned in raw text format:</span></span>

<pre>
Level 1
---------------
655fc955-a5a3-4a26-9723-3090859cb27b, Prey: A Novel
    655fc955-a5a3-4a26-9723-3090859cb27b, Prey: A Novel Rating: 0.5215
    3f471802-f84f-44a0-99c8-6d2e7418eec1, Black Hawk Down: A Story of Modern War Rating: 0.5151
    07b10e28-9e7c-4032-90b7-10acab7f2460, Cryptonomicon Rating: 0.5148
    6afc18e4-8c2a-43d1-9021-57543d6b11d8, Imajica Rating: 0.5146
    e4cc5e69-3567-43ab-b00f-f0d8d0506870, Hit List Rating: 0.514
56b61441-0eed-46cc-a8f6-112775b81892, Life and Death in Shanghai
    56b61441-0eed-46cc-a8f6-112775b81892, Life and Death in Shanghai Rating: 0.5218
    53156702-cc0c-443d-b718-6fb74b2491d3, Son of \ Rating: 0.5212
    fb8cf7a6-8719-46ee-97d4-92f931d77a3a, Smoke and Mirrors: Short Fictions and Illusions Rating: 0.5188
    8f5fe006-79e4-4679-816b-950989d1db4b, A Place I've Never Been (Contemporary American Fiction) Rating: 0.5156
    d8db4583-cc0f-49ce-bc95-b7fa3491623f, Happiness: A Novel Rating: 0.5156
50471eec-9aeb-4900-84d7-21567ab18546, If hello Buddha Dated: A Handbook for Finding Love on a Spiritual Path
    cfe922a1-7ca0-4f8d-ad9d-b7cc87bfe0ef, Divine Secrets of hello Ya-Ya Sisterhood: A Novel Rating: 0.5266
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5252
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5244
    e2cbf7ad-0636-4117-8b30-298da6df7077, Animal Dreams Rating: 0.5227
    6c818fd3-5a09-417d-9ab4-7ffe090f0fef, Confessions of an Ugly Stepsister: A Novel Rating: 0.5222
5e97148f-defb-4d74-af2d-80f4763bf531, hello Deep End of hello Ocean (Oprah's Book Club)
    5e97148f-defb-4d74-af2d-80f4763bf531, hello Deep End of hello Ocean (Oprah's Book Club) Rating: 0.537
    5dcbac37-2946-4f2a-a0b3-bbe710f9409a, Up Island: A Novel Rating: 0.5277
    bc5b69db-733b-4346-adde-3927544258f7, Downtown Rating: 0.5275
    31fe5c63-3e5a-48d0-802b-d3b0f989a634, Have a Nice Day: A Tale of Blood and Sweatsocks Rating: 0.5252
    0adf981a-b65b-4c11-b36b-78aca2f948a2, hello Perfect Storm: A True Story of Men Against hello Sea Rating: 0.5238
68f97068-ae1a-4163-9e94-396b800b743d, Modoc: hello True Story of hello Greatest Elephant That Ever Lived
    68f97068-ae1a-4163-9e94-396b800b743d, Modoc: hello True Story of hello Greatest Elephant That Ever Lived Rating: 0.5379
    6724862e-e4e7-4022-9614-1468d8b902ff, Little House on hello Prairie Rating: 0.5345
    cdedb837-1620-496d-94c4-6ccfed888320, Little House in hello Big Woods Rating: 0.5325
    382164ba-406b-4187-b726-d7a54b9d790d, hello Tao of Pooh Rating: 0.5309
    6a068d6a-bb74-4ba3-b3f2-a956c4f9d1b5, On hello Banks of Plum Creek Rating: 0.5285
37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships
    37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars, Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships Rating: 0.5397
    f2be16d4-5faf-4d32-ab83-7ba74d29261e, Politically Correct Bedtime Stories: Modern Tales for Our Life and Times Rating: 0.5207
    ef732c5c-334b-4d6b-ab82-7255eb7286d0, Honor Among Thieves Rating: 0.5195
    0b209b8c-7cdd-47fd-b940-05c7ff7c60fc, hello Giving Tree Rating: 0.5194
    883b360f-8b42-407f-b977-2f44ad840877, Scary Stories tooTell in hello Dark: Collected from American Folklore (Scary Stories) Rating: 0.5184
ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: hello Craft of Baseball
    d008dae9-c73a-40a1-9a9b-96d5cf546f36, hello Gulag Archipelago 1918-1956: An Experiment in Literary Investigation I-II Rating: 0.5416
    ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: hello Craft of Baseball Rating: 0.5403
    49dec30e-0adb-411a-b186-48eaabf6f8bc, Fatherland Rating: 0.5394
    cc7964fd-d30f-478e-a425-93ddbdf094ed, Magic hello Gathering: Arena Vol. 1 Rating: 0.5379
    8a1e9f36-97af-4614-bed9-24e3940a05f3, More Sniglets: Any Word That Doesn't Appear in hello Dictionary but Should Rating: 0.5377
12a6d988-be21-4a09-8143-9d5f4261ba16, A Dream of Eagles
    07b10e28-9e7c-4032-90b7-10acab7f2460, Cryptonomicon Rating: 0.5417
    e4cc5e69-3567-43ab-b00f-f0d8d0506870, Hit List Rating: 0.5416
    1f1a34c4-9781-49f5-a3cc-acec3ae3c71d, hello Family Rating: 0.5371
    56daeffe-7d48-43cd-8ef8-7dffd0c103d3, Kilo Class Rating: 0.5366
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5366
df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish
    56d33036-dfda-46b9-8e2a-76cb03921bb0, hello X-Files: Ground Zero Rating: 0.5417
    0780cde8-6529-4e1d-b6c6-082c1b80e596, Twelve Red Herrings Rating: 0.5416
    df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish Rating: 0.5408
    400fe331-2c35-490c-adbc-b28b4b73d56c, Shall We Tell hello President? Rating: 0.5383
    f86ad7d0-5c03-42b3-aebf-13d44aec8b30, Shades of Grace Rating: 0.5358
de1f62a4-89e6-44d2-aaee-992a4bf093f1, hello Map That Changed hello World: William Smith and hello Birth of Modern Geology
    de1f62a4-89e6-44d2-aaee-992a4bf093f1, hello Map That Changed hello World: William Smith and hello Birth of Modern Geology Rating: 0.5422
    b303538f-e2c6-4a2c-b425-8d21e684fc3e, My Uncle Oswald Rating: 0.5385
    34b84627-48af-4a4c-96c4-b26fb3863f56, Midnight In hello Garden of Good and Evil Rating: 0.5379
    306cbaa7-b1a8-4142-9d55-e11b5018a7a8, hello Street Lawyer Rating: 0.5376
    e53b4baa-8c09-45c4-95c0-b6a26b98770b, Miss Smillas Feeling for Snow Rating: 0.5367

Level 2
---------------
352aaea1-6b12-454d-a3d5-46379d9e4eb2, hello Sinister Pig (Hillerman Tony)
    352aaea1-6b12-454d-a3d5-46379d9e4eb2, hello Sinister Pig (Hillerman Tony) Rating: 0.5425
    74c49398-bc10-4af5-a658-a996a1201254, Children of hello Storm (Peters Elizabeth) Rating: 0.5387
    9ba80080-196e-43fd-8025-391d963f77e7, hello Floating Girl Rating: 0.5372
    e68f81d5-7745-4cc7-b943-fedb8fcc2ced, Killer Smile (Scottoline Lisa) Rating: 0.5353
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5332
c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days
    0adf981a-b65b-4c11-b36b-78aca2f948a2, hello Perfect Storm: A True Story of Men Against hello Sea Rating: 0.5433
    c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days Rating: 0.543
    a00ae6ad-4a7f-4211-9836-75ce8834eb11, Sniglets (Snig'lit: Any Word That Doesn't Appear in hello Dictionary But Should) Rating: 0.5327
    6f6e192e-0d64-49ca-9b63-f09413ea1ee6, Politically Correct Holiday Stories: For an Enlightened Yuletide Season Rating: 0.5307
    798051a8-147d-4d46-b0dc-e836325029e6, AGE OF INNOCENCE (MOVIE TIE-IN) Rating: 0.5301
73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics)
    cba8163f-6536-436b-8130-47b4a43c827f, Trust No One (hello Official Guide toohello X-Files Vol. 2) Rating: 0.5434
    5708e4cb-2492-49c0-94a8-cc413eec5d89, Small Gods (Discworld Novels (Paperback)) Rating: 0.5406
    73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics) Rating: 0.5403
    d885b0bd-ae4b-452d-bdf2-faa90197dbc9, hello Color of Magic Rating: 0.539
    b133a9c4-4784-4db3-b100-d0d6dffb94d2, hello Truth Is Out There (hello Official Guide toohello X-Files Vol. 1) Rating: 0.5367
271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why hello Winged Whale Sings
    271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why hello Winged Whale Sings Rating: 0.5445
    2de1c354-90ff-47c5-a0db-1bad7d88ef94, hello Salaryman's Wife (Children of Violence Series) Rating: 0.5329
    d279416e-19c0-43f8-9ec9-a585947879ca, Zen Attitude Rating: 0.5316
    c8f854d7-3de3-4b23-8217-f4f851670fd4, Revenge of hello Cootie Girls: A Robin Hudson Mystery (Robin Hudson Mysteries (Paperback)) Rating: 0.5305
    8ef4751c-7074-409e-a3ac-d49b222fc864, Where hello Wild Things Are Rating: 0.5289
9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God
    9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God Rating: 0.5446
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, hello Bean Trees Rating: 0.5389
    65ecbdd1-131c-40c3-a3d6-d86ca281377a, hello God of Small Things Rating: 0.5387
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, hello Stone Diaries Rating: 0.5355
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5344
5f17d90a-2604-4fe8-8977-1a280b9098b1, One for hello Money (Stephanie Plum Novels (Paperback))
    5f17d90a-2604-4fe8-8977-1a280b9098b1, One for hello Money (Stephanie Plum Novels (Paperback)) Rating: 0.5446
    57169b2b-9a8a-486b-9aac-1ed98ce57168, Final Appeal Rating: 0.5332
    efcb1bc4-7278-4a8f-b491-befde02070d6, Moment of Truth Rating: 0.5329
    1efa91a2-993b-4c43-9f5c-3454fc12612d, Burn Factor Rating: 0.5309
    24c59962-458a-4ec8-b95d-d694e861919c, At Home in Mitford (hello Mitford Years) Rating: 0.5303
4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: hello Boy Who Was Raised As a Girl
    4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: hello Boy Who Was Raised As a Girl Rating: 0.5449
    cd5f2c03-20cb-43be-a1fb-3b4233e63222, Pigs in Heaven Rating: 0.5329
    19985fdb-d07a-4a25-ae4a-97b9cb61e5d1, Love in hello Time of Cholera (Penguin Great Books of hello 20th Century) Rating: 0.5267
    15689d09-c711-4844-84d8-130a90237b26, Bel Canto Rating: 0.5245
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5235
98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories
    f874b5a3-5d40-4436-94ff-0fa1c090ddf5, hello Sun Also Rises (A Scribner classic) Rating: 0.5451
    98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories Rating: 0.5442
    0ce0014a-9a48-4013-a08a-7f2c11877930, H.M.S. Unseen Rating: 0.5421
    15316ca6-1e38-425f-893d-691944a47000, More Scary Stories tooTell In hello Dark Rating: 0.5409
    329d5682-3dc3-4206-8aa2-eef4b1032258, Letters from hello Earth Rating: 0.54
5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover))
    5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover)) Rating: 0.5462
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5372
    604eb3bd-6026-4f51-bffd-9fb54f180400, Family Pictures: A Novel Rating: 0.5341
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5334
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, hello Bean Trees Rating: 0.5319
d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven
    d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven Rating: 0.5491
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5401
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, hello Stone Diaries Rating: 0.5393
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5382
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5367

</pre>


## <a name="7-model-business-rules"></a><span data-ttu-id="d044f-418">7. Bedrijfsregels model</span><span class="sxs-lookup"><span data-stu-id="d044f-418">7. Model Business Rules</span></span>
<span data-ttu-id="d044f-419">Dit zijn Hallo typen regels die ondersteund:</span><span class="sxs-lookup"><span data-stu-id="d044f-419">These are hello types of rules supported:</span></span>

* <span data-ttu-id="d044f-420"><strong>BlockList</strong> -BlockList kunt u een lijst met items die u niet dat tooreturn in Hallo aanbeveling resultaten wilt tooprovide.</span><span class="sxs-lookup"><span data-stu-id="d044f-420"><strong>BlockList</strong> - BlockList enables you tooprovide a list of items that you do not want tooreturn in hello recommendation results.</span></span> 
* <span data-ttu-id="d044f-421"><strong>FeatureBlockList</strong> -functie BlockList kunt u tooblock items op basis van Hallo waarden van de functies.</span><span class="sxs-lookup"><span data-stu-id="d044f-421"><strong>FeatureBlockList</strong> - Feature BlockList enables you tooblock items based on hello values of its features.</span></span>

<span data-ttu-id="d044f-422">*Meer dan 1000 items in een regel één blocklist niet verzenden of de aanroep kan time-out. Als u tooblock meer dan 1000 items moet, kunt u verschillende blocklist aanroepen.*</span><span class="sxs-lookup"><span data-stu-id="d044f-422">*Do not send more than 1000 items in a single blocklist rule or your call may timeout. If you need tooblock more than 1000 items, you can make several blocklist calls.*</span></span>

* <span data-ttu-id="d044f-423"><strong>Upsale</strong> -Upsale kunt u tooenforce items tooreturn in Hallo aanbeveling Resultaten.</span><span class="sxs-lookup"><span data-stu-id="d044f-423"><strong>Upsale</strong> - Upsale enables you tooenforce items tooreturn in hello recommendation results.</span></span>
* <span data-ttu-id="d044f-424"><strong>Geaccepteerde</strong> -witte lijst kunt u tooonly voorstellen aanbevelingen uit een lijst met items.</span><span class="sxs-lookup"><span data-stu-id="d044f-424"><strong>WhiteList</strong> - White List enables you tooonly suggest recommendations from a list of items.</span></span>
* <span data-ttu-id="d044f-425"><strong>FeatureWhiteList</strong> -functie witte lijst kunt u tooonly aanbevolen items die specifiek functie waarden hebben.</span><span class="sxs-lookup"><span data-stu-id="d044f-425"><strong>FeatureWhiteList</strong> - Feature White List enables you tooonly recommend items that have specific feature values.</span></span>
* <span data-ttu-id="d044f-426"><strong>PerSeedBlockList</strong> - Per Seed blokkeringslijst schakelt tooprovide per item voor een lijst met items die als aanbeveling resultaten kan niet worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="d044f-426"><strong>PerSeedBlockList</strong> - Per Seed Block List enables you tooprovide per item a list of items that cannot be returned as recommendation results.</span></span>

### <a name="71----get-model-rules"></a><span data-ttu-id="d044f-427">7.1.</span><span class="sxs-lookup"><span data-stu-id="d044f-427">7.1.</span></span>    <span data-ttu-id="d044f-428">Model-regels ophalen</span><span class="sxs-lookup"><span data-stu-id="d044f-428">Get Model Rules</span></span>
| <span data-ttu-id="d044f-429">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-429">HTTP Method</span></span> | <span data-ttu-id="d044f-430">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-430">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-431">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="d044f-431">GET</span></span> |`<rootURI>/GetModelRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="d044f-432">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d044f-432">Example:</span></span><br>`<rootURI>/GetModelRules?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="d044f-433">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-433">Parameter Name</span></span> | <span data-ttu-id="d044f-434">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-434">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-435">Model</span><span class="sxs-lookup"><span data-stu-id="d044f-435">modelId</span></span> |<span data-ttu-id="d044f-436">De unieke id van het Hallo-model</span><span class="sxs-lookup"><span data-stu-id="d044f-436">Unique identifier of hello model</span></span> |
| <span data-ttu-id="d044f-437">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-437">apiVersion</span></span> |<span data-ttu-id="d044f-438">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-438">1.0</span></span> |
|  | |
| <span data-ttu-id="d044f-439">Aanvraagtekst</span><span class="sxs-lookup"><span data-stu-id="d044f-439">Request Body</span></span> |<span data-ttu-id="d044f-440">GEEN</span><span class="sxs-lookup"><span data-stu-id="d044f-440">NONE</span></span> |

<span data-ttu-id="d044f-441">**Antwoord**:</span><span class="sxs-lookup"><span data-stu-id="d044f-441">**Response**:</span></span>

<span data-ttu-id="d044f-442">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-442">HTTP Status code: 200</span></span>

* <span data-ttu-id="d044f-443">`feed/entry/content/properties/Id`-De unieke id van deze regel.</span><span class="sxs-lookup"><span data-stu-id="d044f-443">`feed/entry/content/properties/Id` - Unique identifier of this rule.</span></span>
* <span data-ttu-id="d044f-444">`feed/entry/content/properties/Type`-Type Hallo regel.</span><span class="sxs-lookup"><span data-stu-id="d044f-444">`feed/entry/content/properties/Type` - Type of hello rule.</span></span>
* <span data-ttu-id="d044f-445">`feed/entry/content/properties/Parameter`-De parameter regel.</span><span class="sxs-lookup"><span data-stu-id="d044f-445">`feed/entry/content/properties/Parameter` - Rule parameter.</span></span>

<span data-ttu-id="d044f-446">OData-XML</span><span class="sxs-lookup"><span data-stu-id="d044f-446">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get a list of rules for a model</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T12:58:57Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetAListOfRulesForAModelEntity</title>
        <updated>2014-11-05T12:58:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000043</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1000"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetAListOfRulesForAModelEntity</title>
        <updated>2014-11-05T12:58:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000044</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1001"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="72----add-rule"></a><span data-ttu-id="d044f-447">7.2.</span><span class="sxs-lookup"><span data-stu-id="d044f-447">7.2.</span></span>    <span data-ttu-id="d044f-448">Regel toevoegen</span><span class="sxs-lookup"><span data-stu-id="d044f-448">Add Rule</span></span>
| <span data-ttu-id="d044f-449">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-449">HTTP Method</span></span> | <span data-ttu-id="d044f-450">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-450">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-451">VERZENDEN</span><span class="sxs-lookup"><span data-stu-id="d044f-451">POST</span></span> |`<rootURI>/AddRule?apiVersion=%271.0%27` |
| <span data-ttu-id="d044f-452">KOPTEKST</span><span class="sxs-lookup"><span data-stu-id="d044f-452">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="d044f-453">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-453">Parameter Name</span></span> | <span data-ttu-id="d044f-454">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-454">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-455">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-455">apiVersion</span></span> |<span data-ttu-id="d044f-456">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-456">1.0</span></span> |
|  | |
| <span data-ttu-id="d044f-457">Aanvraagtekst</span><span class="sxs-lookup"><span data-stu-id="d044f-457">Request Body</span></span> | |

<span data-ttu-id="d044f-458"><ins>Wanneer het bieden van Item-id's voor bedrijfsregels, zorg ervoor dat toouse Hallo externe Hallo item-Id (dezelfde Id die u hebt gebruikt in catalogusbestand Hallo Hallo)</ins></span><span class="sxs-lookup"><span data-stu-id="d044f-458"><ins>Whenever providing Item Ids for business rules, make sure toouse hello External Id of hello item (hello same Id that you used in hello catalog file)</ins></span></span><br><span data-ttu-id="d044f-459">
<ins>een regel BlockList tooadd:</ins></span><span class="sxs-lookup"><span data-stu-id="d044f-459">
<ins>tooadd a BlockList rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>BlockList</Type><Value>{"ItemsToExclude":["2406E770-769C-4189-89DE-1C9283F93A96","3906E110-769C-4189-89DE-1C9283F98888"]}</Value></ApiFilter>`<br><br><span data-ttu-id="d044f-460"><ins>
<ins>een regel FeatureBlockList tooadd:</ins></span><span class="sxs-lookup"><span data-stu-id="d044f-460"><ins>
<ins>tooadd a FeatureBlockList rule:</ins></span></span><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureBlockList</Type><Value>{"Name":"Movie_category","Values":["Adult","Drama"]}</Value></ApiFilter>`<br><br><span data-ttu-id="d044f-461"><ins>een regel Upsale tooadd:</ins></span><span class="sxs-lookup"><span data-stu-id="d044f-461"><ins> tooadd an Upsale rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>Upsale</Type><Value>{"ItemsToUpsale":["2406E770-769C-4189-89DE-1C9283F93A96"],"NumberOfItemsToUpsale":5}</Value></ApiFilter>`<br><br><span data-ttu-id="d044f-462">
<ins>een regel geaccepteerde tooadd:</ins></span><span class="sxs-lookup"><span data-stu-id="d044f-462">
<ins>tooadd a WhiteList rule:</ins></span></span><br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>WhiteList</Type><Value>{"ItemsToInclude":["2406E770-769C-4189-89DE-1C9283F93A96","1116E770-769C-4189-89DE-1C9283F88888"]}</Value></ApiFilter>`<br><br><span data-ttu-id="d044f-463"><ins>
<ins>een regel FeatureWhiteList tooadd:</ins></span><span class="sxs-lookup"><span data-stu-id="d044f-463"><ins>
<ins>tooadd a FeatureWhiteList rule:</ins></span></span><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureWhiteList</Type><Value>{"Name":"Movie_rating","Values":["PG13"]}</Value></ApiFilter>`<br><br><span data-ttu-id="d044f-464"><ins>een regel PerSeedBlockList tooadd:</ins></span><span class="sxs-lookup"><span data-stu-id="d044f-464"><ins> tooadd a PerSeedBlockList rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>PerSeedBlockList</Type><Value>{"SeedItems":["9949"],"ItemsToExclude":["9862","8158","8244"]}</Value></ApiFilter>`|

<span data-ttu-id="d044f-465">**Antwoord**:</span><span class="sxs-lookup"><span data-stu-id="d044f-465">**Response**:</span></span>

<span data-ttu-id="d044f-466">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-466">HTTP Status code: 200</span></span>

<span data-ttu-id="d044f-467">Hallo API retourneert Hallo regel zojuist hebt gemaakt met de details ervan.</span><span class="sxs-lookup"><span data-stu-id="d044f-467">hello API returns hello newly created rule with its details.</span></span> <span data-ttu-id="d044f-468">Hallo regels eigenschap kan worden opgehaald uit de volgende paden Hallo:</span><span class="sxs-lookup"><span data-stu-id="d044f-468">hello rules property can be retrieved from hello following paths:</span></span>

* <span data-ttu-id="d044f-469">`feed/entry/content/properties/Id`-De unieke id van deze regel.</span><span class="sxs-lookup"><span data-stu-id="d044f-469">`feed/entry/content/properties/Id` - Unique identifier of this rule.</span></span>
* <span data-ttu-id="d044f-470">`feed/entry/content/properties/Type`-Type van de regel Hallo: BlockList of Upsale.</span><span class="sxs-lookup"><span data-stu-id="d044f-470">`feed/entry/content/properties/Type` - Type of hello rule: BlockList or Upsale.</span></span>
* <span data-ttu-id="d044f-471">`feed/entry/content/properties/Parameter`-De parameter regel.</span><span class="sxs-lookup"><span data-stu-id="d044f-471">`feed/entry/content/properties/Parameter` - Rule parameter.</span></span>

<span data-ttu-id="d044f-472">OData-XML</span><span class="sxs-lookup"><span data-stu-id="d044f-472">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Add A Rule</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T11:13:28Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">AddARuleEntity</title>
        <updated>2014-11-05T11:13:28Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000041</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1002"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="73----delete-rule"></a><span data-ttu-id="d044f-473">7.3.</span><span class="sxs-lookup"><span data-stu-id="d044f-473">7.3.</span></span>    <span data-ttu-id="d044f-474">Regel verwijderen</span><span class="sxs-lookup"><span data-stu-id="d044f-474">Delete Rule</span></span>
| <span data-ttu-id="d044f-475">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-475">HTTP Method</span></span> | <span data-ttu-id="d044f-476">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-476">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-477">VERWIJDEREN</span><span class="sxs-lookup"><span data-stu-id="d044f-477">DELETE</span></span> |`<rootURI>/DeleteRule?modelId=%27<model_id>%27&filterId=%27<filter_Id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="d044f-478">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d044f-478">Example:</span></span><br>`DeleteRule?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&filterId=%271000011%27&apiVersion=%271.0%27` |

| <span data-ttu-id="d044f-479">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-479">Parameter Name</span></span> | <span data-ttu-id="d044f-480">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-480">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-481">Model</span><span class="sxs-lookup"><span data-stu-id="d044f-481">modelId</span></span> |<span data-ttu-id="d044f-482">De unieke id van het Hallo-model</span><span class="sxs-lookup"><span data-stu-id="d044f-482">Unique identifier of hello model</span></span> |
| <span data-ttu-id="d044f-483">filterId</span><span class="sxs-lookup"><span data-stu-id="d044f-483">filterId</span></span> |<span data-ttu-id="d044f-484">De unieke id van het Hallo-filter</span><span class="sxs-lookup"><span data-stu-id="d044f-484">Unique identifier of hello filter</span></span> |
| <span data-ttu-id="d044f-485">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-485">apiVersion</span></span> |<span data-ttu-id="d044f-486">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-486">1.0</span></span> |
|  | |
| <span data-ttu-id="d044f-487">Aanvraagtekst</span><span class="sxs-lookup"><span data-stu-id="d044f-487">Request Body</span></span> |<span data-ttu-id="d044f-488">GEEN</span><span class="sxs-lookup"><span data-stu-id="d044f-488">NONE</span></span> |

<span data-ttu-id="d044f-489">**Antwoord**:</span><span class="sxs-lookup"><span data-stu-id="d044f-489">**Response**:</span></span>

<span data-ttu-id="d044f-490">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-490">HTTP Status code: 200</span></span>

### <a name="74----delete-all-rules"></a><span data-ttu-id="d044f-491">7.4.</span><span class="sxs-lookup"><span data-stu-id="d044f-491">7.4.</span></span>    <span data-ttu-id="d044f-492">Alle regels verwijderen</span><span class="sxs-lookup"><span data-stu-id="d044f-492">Delete All Rules</span></span>
| <span data-ttu-id="d044f-493">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-493">HTTP Method</span></span> | <span data-ttu-id="d044f-494">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-494">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-495">VERWIJDEREN</span><span class="sxs-lookup"><span data-stu-id="d044f-495">DELETE</span></span> |`<rootURI>/DeleteAllRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="d044f-496">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d044f-496">Example:</span></span><br>`DeleteAllRules?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| <span data-ttu-id="d044f-497">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-497">Parameter Name</span></span> | <span data-ttu-id="d044f-498">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-498">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-499">Model</span><span class="sxs-lookup"><span data-stu-id="d044f-499">modelId</span></span> |<span data-ttu-id="d044f-500">De unieke id van het Hallo-model</span><span class="sxs-lookup"><span data-stu-id="d044f-500">Unique identifier of hello model</span></span> |
| <span data-ttu-id="d044f-501">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-501">apiVersion</span></span> |<span data-ttu-id="d044f-502">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-502">1.0</span></span> |
|  | |
| <span data-ttu-id="d044f-503">Aanvraagtekst</span><span class="sxs-lookup"><span data-stu-id="d044f-503">Request Body</span></span> |<span data-ttu-id="d044f-504">GEEN</span><span class="sxs-lookup"><span data-stu-id="d044f-504">NONE</span></span> |

<span data-ttu-id="d044f-505">**Antwoord**:</span><span class="sxs-lookup"><span data-stu-id="d044f-505">**Response**:</span></span>

<span data-ttu-id="d044f-506">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-506">HTTP Status code: 200</span></span>

## <a name="8-catalog"></a><span data-ttu-id="d044f-507">8. Catalogus</span><span class="sxs-lookup"><span data-stu-id="d044f-507">8. Catalog</span></span>
### <a name="81----import-catalog-data"></a><span data-ttu-id="d044f-508">8.1.</span><span class="sxs-lookup"><span data-stu-id="d044f-508">8.1.</span></span>    <span data-ttu-id="d044f-509">Gegevens van de catalogus importeren</span><span class="sxs-lookup"><span data-stu-id="d044f-509">Import Catalog Data</span></span>
<span data-ttu-id="d044f-510">Als u verschillende catalogus bestanden toohello dezelfde model met verschillende aanroepen uploadt, wordt er alleen Hallo nieuwe catalogusitems ingevoegd.</span><span class="sxs-lookup"><span data-stu-id="d044f-510">If you upload several catalog files toohello same model with several calls, we will insert only hello new catalog items.</span></span> <span data-ttu-id="d044f-511">Bestaande items blijft met de oorspronkelijke waarden Hallo.</span><span class="sxs-lookup"><span data-stu-id="d044f-511">Existing items will remain with hello original values.</span></span> <span data-ttu-id="d044f-512">U kunt gegevens in de catalogus niet bijwerken met deze methode.</span><span class="sxs-lookup"><span data-stu-id="d044f-512">You cannot update catalog data by using this method.</span></span>

<span data-ttu-id="d044f-513">Hallo catalogusgegevens Voer Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="d044f-513">hello catalog data should follow hello following format:</span></span>

* <span data-ttu-id="d044f-514">Zonder functies:`<Item Id>,<Item Name>,<Item Category>[,<Description>]`</span><span class="sxs-lookup"><span data-stu-id="d044f-514">Without features - `<Item Id>,<Item Name>,<Item Category>[,<Description>]`</span></span>
* <span data-ttu-id="d044f-515">Met functies:`<Item Id>,<Item Name>,<Item Category>,[<Description>],<Features list>`</span><span class="sxs-lookup"><span data-stu-id="d044f-515">With features - `<Item Id>,<Item Name>,<Item Category>,[<Description>],<Features list>`</span></span>

<span data-ttu-id="d044f-516">Opmerking: de maximale bestandsgrootte Hallo is 200MB.</span><span class="sxs-lookup"><span data-stu-id="d044f-516">Note: hello maximum file size is 200MB.</span></span>

<span data-ttu-id="d044f-517">** Details opmaken **</span><span class="sxs-lookup"><span data-stu-id="d044f-517">** Format details **</span></span>

| <span data-ttu-id="d044f-518">Naam</span><span class="sxs-lookup"><span data-stu-id="d044f-518">Name</span></span> | <span data-ttu-id="d044f-519">Verplicht</span><span class="sxs-lookup"><span data-stu-id="d044f-519">Mandatory</span></span> | <span data-ttu-id="d044f-520">Type</span><span class="sxs-lookup"><span data-stu-id="d044f-520">Type</span></span> | <span data-ttu-id="d044f-521">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d044f-521">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d044f-522">Artikel-Id</span><span class="sxs-lookup"><span data-stu-id="d044f-522">Item Id</span></span> |<span data-ttu-id="d044f-523">Ja</span><span class="sxs-lookup"><span data-stu-id="d044f-523">Yes</span></span> |<span data-ttu-id="d044f-524">[A-z], [a-z], [0-9] [_] &#40; Onderstrepingsteken &#41; [-] &#40; Dash &#41;</span><span class="sxs-lookup"><span data-stu-id="d044f-524">[A-z], [a-z], [0-9], [_] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="d044f-525">Maximale lengte: 50</span><span class="sxs-lookup"><span data-stu-id="d044f-525">Max length: 50</span></span> |<span data-ttu-id="d044f-526">De unieke id van een item.</span><span class="sxs-lookup"><span data-stu-id="d044f-526">Unique identifier of an item.</span></span> |
| <span data-ttu-id="d044f-527">De itemnaam van het</span><span class="sxs-lookup"><span data-stu-id="d044f-527">Item Name</span></span> |<span data-ttu-id="d044f-528">Ja</span><span class="sxs-lookup"><span data-stu-id="d044f-528">Yes</span></span> |<span data-ttu-id="d044f-529">Alle alfanumerieke tekens</span><span class="sxs-lookup"><span data-stu-id="d044f-529">Any alphanumeric characters</span></span><br> <span data-ttu-id="d044f-530">Maximale lengte: 255</span><span class="sxs-lookup"><span data-stu-id="d044f-530">Max length: 255</span></span> |<span data-ttu-id="d044f-531">Naam van het item.</span><span class="sxs-lookup"><span data-stu-id="d044f-531">Item name.</span></span> |
| <span data-ttu-id="d044f-532">Item categorie</span><span class="sxs-lookup"><span data-stu-id="d044f-532">Item Category</span></span> |<span data-ttu-id="d044f-533">Ja</span><span class="sxs-lookup"><span data-stu-id="d044f-533">Yes</span></span> |<span data-ttu-id="d044f-534">Alle alfanumerieke tekens</span><span class="sxs-lookup"><span data-stu-id="d044f-534">Any alphanumeric characters</span></span> <br> <span data-ttu-id="d044f-535">Maximale lengte: 255</span><span class="sxs-lookup"><span data-stu-id="d044f-535">Max length: 255</span></span> |<span data-ttu-id="d044f-536">Categorie toowhich dit item behoort (bijvoorbeeld koken Books, Drama...); kan niet leeg zijn.</span><span class="sxs-lookup"><span data-stu-id="d044f-536">Category toowhich this item belongs (e.g. Cooking Books, Drama…); can be empty.</span></span> |
| <span data-ttu-id="d044f-537">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d044f-537">Description</span></span> |<span data-ttu-id="d044f-538">Nee, tenzij er functies zijn aanwezig (maar mag leeg zijn)</span><span class="sxs-lookup"><span data-stu-id="d044f-538">No, unless features are present (but can be empty)</span></span> |<span data-ttu-id="d044f-539">Alle alfanumerieke tekens</span><span class="sxs-lookup"><span data-stu-id="d044f-539">Any alphanumeric characters</span></span> <br> <span data-ttu-id="d044f-540">Maximale lengte: 4000</span><span class="sxs-lookup"><span data-stu-id="d044f-540">Max length: 4000</span></span> |<span data-ttu-id="d044f-541">Beschrijving van dit item.</span><span class="sxs-lookup"><span data-stu-id="d044f-541">Description of this item.</span></span> |
| <span data-ttu-id="d044f-542">Lijst met functies</span><span class="sxs-lookup"><span data-stu-id="d044f-542">Features list</span></span> |<span data-ttu-id="d044f-543">Nee</span><span class="sxs-lookup"><span data-stu-id="d044f-543">No</span></span> |<span data-ttu-id="d044f-544">Alle alfanumerieke tekens</span><span class="sxs-lookup"><span data-stu-id="d044f-544">Any alphanumeric characters</span></span> <br> <span data-ttu-id="d044f-545">Maximale lengte: 4000; Maximumaantal functies: 20</span><span class="sxs-lookup"><span data-stu-id="d044f-545">Max length: 4000; Max number of features:20</span></span> |<span data-ttu-id="d044f-546">Door komma's gescheiden lijst met de functienaam van de = functie-waarde die gebruikt tooenhance model aanbeveling worden kan; Zie [geavanceerde onderwerpen](#2-advanced-topics) sectie.</span><span class="sxs-lookup"><span data-stu-id="d044f-546">Comma-separated list of feature name=feature value that can be used tooenhance model recommendation; see [Advanced topics](#2-advanced-topics) section.</span></span> |

| <span data-ttu-id="d044f-547">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-547">HTTP Method</span></span> | <span data-ttu-id="d044f-548">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-548">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-549">VERZENDEN</span><span class="sxs-lookup"><span data-stu-id="d044f-549">POST</span></span> |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="d044f-550">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d044f-550">Example:</span></span><br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |
| <span data-ttu-id="d044f-551">KOPTEKST</span><span class="sxs-lookup"><span data-stu-id="d044f-551">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="d044f-552">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-552">Parameter Name</span></span> | <span data-ttu-id="d044f-553">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-553">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-554">Model</span><span class="sxs-lookup"><span data-stu-id="d044f-554">modelId</span></span> |<span data-ttu-id="d044f-555">De unieke id van het Hallo-model</span><span class="sxs-lookup"><span data-stu-id="d044f-555">Unique identifier of hello model</span></span> |
| <span data-ttu-id="d044f-556">bestandsnaam</span><span class="sxs-lookup"><span data-stu-id="d044f-556">filename</span></span> |<span data-ttu-id="d044f-557">Tekstuele Hallo catalogus-ID.</span><span class="sxs-lookup"><span data-stu-id="d044f-557">Textual identifier of hello catalog.</span></span><br><span data-ttu-id="d044f-558">Alleen letters (A-Z, a-z), cijfers (0-9), afbreekstreepjes (-) en onderstrepingsteken (_) zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="d044f-558">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="d044f-559">Maximale lengte: 50</span><span class="sxs-lookup"><span data-stu-id="d044f-559">Max length: 50</span></span> |
| <span data-ttu-id="d044f-560">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-560">apiVersion</span></span> |<span data-ttu-id="d044f-561">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-561">1.0</span></span> |
|  | |
| <span data-ttu-id="d044f-562">Aanvraagtekst</span><span class="sxs-lookup"><span data-stu-id="d044f-562">Request Body</span></span> |<span data-ttu-id="d044f-563">Als u bijvoorbeeld (met functies):</span><span class="sxs-lookup"><span data-stu-id="d044f-563">Example (with features):</span></span><br/><span data-ttu-id="d044f-564">2406e770-769c-4189-89de-1c9283f93a96, Clara Callan, boek, Hallo adresboek beschrijving, auteur = Richard Wright, publisher Harper Flamingo Canada = jaar 2001 =</span><span class="sxs-lookup"><span data-stu-id="d044f-564">2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book,hello book  description,author=Richard Wright,publisher=Harper Flamingo Canada,year=2001</span></span><br><span data-ttu-id="d044f-565">21bf8088-b6c0-4509-870c-e1c7ac78304a, Hallo Forgetting ruimte: A fictie (Byzantium Book), adresboek,, auteur = Nick Bantock, publisher = Harpercollins, jaar 1997 =</span><span class="sxs-lookup"><span data-stu-id="d044f-565">21bf8088-b6c0-4509-870c-e1c7ac78304a,hello Forgetting Room: A Fiction (Byzantium Book),Book,,author=Nick Bantock,publisher=Harpercollins,year=1997</span></span><br><span data-ttu-id="d044f-566">3bb5cb44-d143-4bdd-a55c-443964bf4b23, Spadework, adresboek,, auteur = Timothy Findley, publisher = HarperFlamingo Canada, jaar 2001 =</span><span class="sxs-lookup"><span data-stu-id="d044f-566">3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book,,author=Timothy Findley, publisher=HarperFlamingo Canada, year=2001</span></span><br><span data-ttu-id="d044f-567">552a1940-21e4-4399-82bb-594b46d7ed54, beperking van beesten, boek, Hallo adresboek beschrijving, auteur = Magnus Mills, publisher = Arcade Publishing, jaar 1998 =</span><span class="sxs-lookup"><span data-stu-id="d044f-567">552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book,hello book description,author=Magnus Mills, publisher=Arcade Publishing, year=1998</span></span></pre> |

<span data-ttu-id="d044f-568">**Antwoord**:</span><span class="sxs-lookup"><span data-stu-id="d044f-568">**Response**:</span></span>

<span data-ttu-id="d044f-569">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-569">HTTP Status code: 200</span></span>

<span data-ttu-id="d044f-570">Hallo API retourneert een rapport van Hallo importeren.</span><span class="sxs-lookup"><span data-stu-id="d044f-570">hello API returns a report of hello import.</span></span>

* <span data-ttu-id="d044f-571">`feed\entry\content\properties\LineCount`-Het aantal regels is geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="d044f-571">`feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="d044f-572">`feed\entry\content\properties\ErrorCount`-Het aantal regels dat niet is ingevoegd vanwege fout tooan.</span><span class="sxs-lookup"><span data-stu-id="d044f-572">`feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due tooan error.</span></span>

<span data-ttu-id="d044f-573">OData-XML</span><span class="sxs-lookup"><span data-stu-id="d044f-573">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Import catalog file</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-05T06:58:04Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'" />
    <entry>
       <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">ImportCatalogFileEntity2</title>
        <updated>2014-10-05T06:58:04Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:LineCount m:type="Edm.String">4</d:LineCount>
                <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="82----get-catalog"></a><span data-ttu-id="d044f-574">8.2.</span><span class="sxs-lookup"><span data-stu-id="d044f-574">8.2.</span></span>    <span data-ttu-id="d044f-575">Catalogus ophalen</span><span class="sxs-lookup"><span data-stu-id="d044f-575">Get Catalog</span></span>
<span data-ttu-id="d044f-576">Hiermee haalt u alle catalogusitems.</span><span class="sxs-lookup"><span data-stu-id="d044f-576">Retrieves all catalog items.</span></span>
<span data-ttu-id="d044f-577">Hallo-catalogus worden opgehaald van één pagina tegelijk.</span><span class="sxs-lookup"><span data-stu-id="d044f-577">hello catalog will be retrieved one page at a time.</span></span> <span data-ttu-id="d044f-578">Als u tooget items op een specifieke index wilt, kunt u Hallo $skip odata-parameter.</span><span class="sxs-lookup"><span data-stu-id="d044f-578">If you want tooget items at a particular index, you can use hello $skip odata parameter.</span></span> <span data-ttu-id="d044f-579">Bijvoorbeeld als u beginnen bij positie 100 tooget-items wilt, voegt u Hallo parameter $skip = 100 toohello-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="d044f-579">For instance if you want tooget items starting at position 100, add hello parameter $skip=100 toohello request.</span></span>

| <span data-ttu-id="d044f-580">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-580">HTTP Method</span></span> | <span data-ttu-id="d044f-581">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-581">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-582">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="d044f-582">GET</span></span> |`<rootURI>/GetCatalog?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="d044f-583">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d044f-583">Example:</span></span><br>`GetCatalog?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| <span data-ttu-id="d044f-584">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-584">Parameter Name</span></span> | <span data-ttu-id="d044f-585">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-585">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-586">Model</span><span class="sxs-lookup"><span data-stu-id="d044f-586">modelId</span></span> |<span data-ttu-id="d044f-587">De unieke id van het Hallo-model</span><span class="sxs-lookup"><span data-stu-id="d044f-587">Unique identifier of hello model</span></span> |
| <span data-ttu-id="d044f-588">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-588">apiVersion</span></span> |<span data-ttu-id="d044f-589">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-589">1.0</span></span> |
|  | |
| <span data-ttu-id="d044f-590">Aanvraagtekst</span><span class="sxs-lookup"><span data-stu-id="d044f-590">Request Body</span></span> |<span data-ttu-id="d044f-591">GEEN</span><span class="sxs-lookup"><span data-stu-id="d044f-591">NONE</span></span> |

<span data-ttu-id="d044f-592">**Antwoord**:</span><span class="sxs-lookup"><span data-stu-id="d044f-592">**Response**:</span></span>

<span data-ttu-id="d044f-593">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-593">HTTP Status code: 200</span></span>

<span data-ttu-id="d044f-594">Hallo-antwoord bevat één vermelding per catalogusitem.</span><span class="sxs-lookup"><span data-stu-id="d044f-594">hello response includes one entry per catalog item.</span></span> <span data-ttu-id="d044f-595">Elk item heeft Hallo gegevens te volgen:</span><span class="sxs-lookup"><span data-stu-id="d044f-595">Each entry has hello following data:</span></span>

* <span data-ttu-id="d044f-596">`feed/entry/content/properties/ExternalId`-Catalogus externe item-ID, geleverd door de klant Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="d044f-596">`feed/entry/content/properties/ExternalId` - Catalog item external ID, hello one provided by hello customer.</span></span>
* <span data-ttu-id="d044f-597">`feed/entry/content/properties/InternalId`-Catalogus item interne ID Hallo die Azure Machine Learning aanbevelingen heeft gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="d044f-597">`feed/entry/content/properties/InternalId` - Catalog item internal ID, hello one that Azure Machine Learning Recommendations has generated.</span></span>
* <span data-ttu-id="d044f-598">`feed/entry/content/properties/Name`-De itemnaam catalogus.</span><span class="sxs-lookup"><span data-stu-id="d044f-598">`feed/entry/content/properties/Name` - Catalog item name.</span></span>
* <span data-ttu-id="d044f-599">`feed/entry/content/properties/Category`-De rubriek voor object catalogus.</span><span class="sxs-lookup"><span data-stu-id="d044f-599">`feed/entry/content/properties/Category` - Catalog item category.</span></span>
* <span data-ttu-id="d044f-600">`feed/entry/content/properties/Description`-Catalogus beschrijving item.</span><span class="sxs-lookup"><span data-stu-id="d044f-600">`feed/entry/content/properties/Description` - Catalog item description.</span></span>
* <span data-ttu-id="d044f-601">`feed/entry/content/properties/Metadata`-Catalogus itemmetagegevens.</span><span class="sxs-lookup"><span data-stu-id="d044f-601">`feed/entry/content/properties/Metadata` - Catalog item metadata.</span></span>

<span data-ttu-id="d044f-602">OData-XML</span><span class="sxs-lookup"><span data-stu-id="d044f-602">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get All Catalog Items</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">552A1940-21E4-4399-82BB-594B46D7ED54</d:ExternalId>
                <d:InternalId m:type="Edm.String">060db26a-e6a6-464e-bb52-436d2da82a50</d:InternalId>
                <d:Name m:type="Edm.String">Restraint of Beasts</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:ExternalId>
                <d:InternalId m:type="Edm.String">209d7bfe-2eb9-4455-92a3-7c867a41a74a</d:InternalId>
                <d:Name m:type="Edm.String">Clara Callan</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">3BB5CB44-D143-4BDD-A55C-443964BF4B23</d:ExternalId>
                <d:InternalId m:type="Edm.String">913ff79b-059b-4d4d-8042-6fa4cc1391dd</d:InternalId>
                <d:Name m:type="Edm.String">Spadework</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">21BF8088-B6C0-4509-870C-E1C7AC78304A</d:ExternalId>
                <d:InternalId m:type="Edm.String">ea65e4fa-768c-40b4-92c3-69d3e8178691</d:InternalId>
                <d:Name m:type="Edm.String">hello Forgetting Room: A Fiction (Byzantium Book)</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="83----get-catalog-items-by-token"></a><span data-ttu-id="d044f-603">8.3.</span><span class="sxs-lookup"><span data-stu-id="d044f-603">8.3.</span></span>    <span data-ttu-id="d044f-604">Catalogusitems door Token ophalen</span><span class="sxs-lookup"><span data-stu-id="d044f-604">Get Catalog Items by Token</span></span>
| <span data-ttu-id="d044f-605">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-605">HTTP Method</span></span> | <span data-ttu-id="d044f-606">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-606">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-607">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="d044f-607">GET</span></span> |`<rootURI>/GetCatalogItemsByToken?modelId=%27<modelId>%27&token=%27<token>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="d044f-608">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d044f-608">Example:</span></span><br>`GetCatalogItemsByToken?modelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&token=%27Cla%27&apiVersion=%271.0%27` |

| <span data-ttu-id="d044f-609">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-609">Parameter Name</span></span> | <span data-ttu-id="d044f-610">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-610">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-611">Model</span><span class="sxs-lookup"><span data-stu-id="d044f-611">modelId</span></span> |<span data-ttu-id="d044f-612">De unieke id van het Hallo-model</span><span class="sxs-lookup"><span data-stu-id="d044f-612">Unique identifier of hello model</span></span> |
| <span data-ttu-id="d044f-613">Token</span><span class="sxs-lookup"><span data-stu-id="d044f-613">token</span></span> |<span data-ttu-id="d044f-614">Token van de naam van item Hallo-catalogus.</span><span class="sxs-lookup"><span data-stu-id="d044f-614">Token of hello catalog item’s name.</span></span> <span data-ttu-id="d044f-615">Moet ten minste 3 tekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="d044f-615">Should contain at least 3 characters.</span></span> |
| <span data-ttu-id="d044f-616">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-616">apiVersion</span></span> |<span data-ttu-id="d044f-617">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-617">1.0</span></span> |
|  | |
| <span data-ttu-id="d044f-618">Aanvraagtekst</span><span class="sxs-lookup"><span data-stu-id="d044f-618">Request Body</span></span> |<span data-ttu-id="d044f-619">GEEN</span><span class="sxs-lookup"><span data-stu-id="d044f-619">NONE</span></span> |

<span data-ttu-id="d044f-620">**Antwoord**:</span><span class="sxs-lookup"><span data-stu-id="d044f-620">**Response**:</span></span>

<span data-ttu-id="d044f-621">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-621">HTTP Status code: 200</span></span>

<span data-ttu-id="d044f-622">Hallo-antwoord bevat één vermelding per catalogusitem.</span><span class="sxs-lookup"><span data-stu-id="d044f-622">hello response includes one entry per catalog item.</span></span> <span data-ttu-id="d044f-623">Elk item heeft Hallo gegevens te volgen:</span><span class="sxs-lookup"><span data-stu-id="d044f-623">Each entry has hello following data:</span></span>

* <span data-ttu-id="d044f-624">`feed/entry/content/properties/InternalId`-Catalogus item interne ID Hallo die Azure Machine Learning aanbevelingen heeft gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="d044f-624">`feed/entry/content/properties/InternalId` - Catalog item internal ID, hello one that Azure Machine Learning Recommendations has generated.</span></span>
* <span data-ttu-id="d044f-625">`feed/entry/content/properties/Name`-De itemnaam catalogus.</span><span class="sxs-lookup"><span data-stu-id="d044f-625">`feed/entry/content/properties/Name` - Catalog item name.</span></span>
* <span data-ttu-id="d044f-626">`feed/entry/content/properties/Rating`-(voor toekomstig gebruik)</span><span class="sxs-lookup"><span data-stu-id="d044f-626">`feed/entry/content/properties/Rating` -  (for future use)</span></span>
* <span data-ttu-id="d044f-627">`feed/entry/content/properties/Reasoning`-(voor toekomstig gebruik)</span><span class="sxs-lookup"><span data-stu-id="d044f-627">`feed/entry/content/properties/Reasoning` -  (for future use)</span></span>
* <span data-ttu-id="d044f-628">`feed/entry/content/properties/Metadata`-(voor toekomstig gebruik)</span><span class="sxs-lookup"><span data-stu-id="d044f-628">`feed/entry/content/properties/Metadata` -  (for future use)</span></span>
* <span data-ttu-id="d044f-629">`feed/entry/content/properties/FormattedRating`-(voor toekomstig gebruik)</span><span class="sxs-lookup"><span data-stu-id="d044f-629">`feed/entry/content/properties/FormattedRating` - (for future use)</span></span>

<span data-ttu-id="d044f-630">OData-XML</span><span class="sxs-lookup"><span data-stu-id="d044f-630">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get Catalog items that contain a token</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-29T11:48:19Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">CatalogItemsThatContainATokenEntity</title>
            <updated>2014-10-29T11:48:19Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                  <m:properties>
                    <d:Id m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:Id>
                    <d:Name m:type="Edm.String">Clara Callan</d:Name>
                    <d:Rating m:type="Edm.Double">0</d:Rating>
                    <d:Reasoning m:type="Edm.String"></d:Reasoning>
                    <d:Metadata m:type="Edm.String"></d:Metadata>
                    <d:FormattedRating m:type="Edm.Double" m:null="true"></d:FormattedRating>
                  </m:properties>
            </content>
        </entry>
    </feed>

## <a name="9-usage-data"></a><span data-ttu-id="d044f-631">9. Gebruiksgegevens</span><span class="sxs-lookup"><span data-stu-id="d044f-631">9. Usage data</span></span>
### <a name="91----import-usage-data"></a><span data-ttu-id="d044f-632">9.1.</span><span class="sxs-lookup"><span data-stu-id="d044f-632">9.1.</span></span>    <span data-ttu-id="d044f-633">De gebruiksgegevens importeren</span><span class="sxs-lookup"><span data-stu-id="d044f-633">Import Usage Data</span></span>
#### <a name="911-uploading-file"></a><span data-ttu-id="d044f-634">9.1.1.</span><span class="sxs-lookup"><span data-stu-id="d044f-634">9.1.1.</span></span> <span data-ttu-id="d044f-635">Bestand uploaden</span><span class="sxs-lookup"><span data-stu-id="d044f-635">Uploading File</span></span>
<span data-ttu-id="d044f-636">Deze sectie wordt beschreven hoe de gebruiksgegevens tooupload met behulp van een bestand.</span><span class="sxs-lookup"><span data-stu-id="d044f-636">This section shows how tooupload usage data by using a file.</span></span> <span data-ttu-id="d044f-637">U kunt deze API is meerdere keren met gebruiksgegevens aanroepen.</span><span class="sxs-lookup"><span data-stu-id="d044f-637">You can call this API several times with usage data.</span></span> <span data-ttu-id="d044f-638">Alle gebruiksgegevens worden opgeslagen voor alle aanroepen.</span><span class="sxs-lookup"><span data-stu-id="d044f-638">All usage data will be saved for all calls.</span></span>

| <span data-ttu-id="d044f-639">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-639">HTTP Method</span></span> | <span data-ttu-id="d044f-640">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-640">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-641">VERZENDEN</span><span class="sxs-lookup"><span data-stu-id="d044f-641">POST</span></span> |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="d044f-642">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d044f-642">Example:</span></span><br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="d044f-643">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-643">Parameter Name</span></span> | <span data-ttu-id="d044f-644">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-644">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-645">Model</span><span class="sxs-lookup"><span data-stu-id="d044f-645">modelId</span></span> |<span data-ttu-id="d044f-646">De unieke id van het Hallo-model</span><span class="sxs-lookup"><span data-stu-id="d044f-646">Unique identifier of hello model</span></span> |
| <span data-ttu-id="d044f-647">bestandsnaam</span><span class="sxs-lookup"><span data-stu-id="d044f-647">filename</span></span> |<span data-ttu-id="d044f-648">Tekstuele Hallo catalogus-ID.</span><span class="sxs-lookup"><span data-stu-id="d044f-648">Textual identifier of hello catalog.</span></span><br><span data-ttu-id="d044f-649">Alleen letters (A-Z, a-z), cijfers (0-9), afbreekstreepjes (-) en onderstrepingsteken (_) zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="d044f-649">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="d044f-650">Maximale lengte: 50</span><span class="sxs-lookup"><span data-stu-id="d044f-650">Max length: 50</span></span> |
| <span data-ttu-id="d044f-651">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-651">apiVersion</span></span> |<span data-ttu-id="d044f-652">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-652">1.0</span></span> |
|  | |
| <span data-ttu-id="d044f-653">Aanvraagtekst</span><span class="sxs-lookup"><span data-stu-id="d044f-653">Request Body</span></span> |<span data-ttu-id="d044f-654">Gebruiksgegevens.</span><span class="sxs-lookup"><span data-stu-id="d044f-654">Usage data.</span></span> <span data-ttu-id="d044f-655">Indeling:</span><span class="sxs-lookup"><span data-stu-id="d044f-655">Format:</span></span><br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th><span data-ttu-id="d044f-656">Naam</span><span class="sxs-lookup"><span data-stu-id="d044f-656">Name</span></span></th><th><span data-ttu-id="d044f-657">Verplicht</span><span class="sxs-lookup"><span data-stu-id="d044f-657">Mandatory</span></span></th><th><span data-ttu-id="d044f-658">Type</span><span class="sxs-lookup"><span data-stu-id="d044f-658">Type</span></span></th><th><span data-ttu-id="d044f-659">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d044f-659">Description</span></span></th></tr><tr><td><span data-ttu-id="d044f-660">Gebruikers-Id</span><span class="sxs-lookup"><span data-stu-id="d044f-660">User Id</span></span></td><td><span data-ttu-id="d044f-661">Ja</span><span class="sxs-lookup"><span data-stu-id="d044f-661">Yes</span></span></td><td><span data-ttu-id="d044f-662">[A-z], [a-z], [0-9] [_] &#40; Onderstrepingsteken &#41; [-] &#40; Dash &#41;</span><span class="sxs-lookup"><span data-stu-id="d044f-662">[A-z], [a-z], [0-9], [_] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="d044f-663">Maximale lengte: 255</span><span class="sxs-lookup"><span data-stu-id="d044f-663">Max length: 255</span></span> </td><td><span data-ttu-id="d044f-664">De unieke id van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="d044f-664">Unique identifier of a user.</span></span></td></tr><tr><td><span data-ttu-id="d044f-665">Artikel-Id</span><span class="sxs-lookup"><span data-stu-id="d044f-665">Item Id</span></span></td><td><span data-ttu-id="d044f-666">Ja</span><span class="sxs-lookup"><span data-stu-id="d044f-666">Yes</span></span></td><td><span data-ttu-id="d044f-667">[A-z], [a-z], [0-9] [&#95;] &#40; Onderstrepingsteken &#41; [-] &#40; Dash &#41;</span><span class="sxs-lookup"><span data-stu-id="d044f-667">[A-z], [a-z], [0-9], [&#95;] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="d044f-668">Maximale lengte: 50</span><span class="sxs-lookup"><span data-stu-id="d044f-668">Max length: 50</span></span></td><td><span data-ttu-id="d044f-669">De unieke id van een item.</span><span class="sxs-lookup"><span data-stu-id="d044f-669">Unique identifier of an item.</span></span></td></tr><tr><td><span data-ttu-id="d044f-670">Time</span><span class="sxs-lookup"><span data-stu-id="d044f-670">Time</span></span></td><td><span data-ttu-id="d044f-671">Nee</span><span class="sxs-lookup"><span data-stu-id="d044f-671">No</span></span></td><td><span data-ttu-id="d044f-672">Datum in de notatie: jjjj/MM/ddTUU (bijvoorbeeld 2013/06/20T10:00:00)</span><span class="sxs-lookup"><span data-stu-id="d044f-672">Date in format: YYYY/MM/DDTHH:MM:SS (e.g. 2013/06/20T10:00:00)</span></span></td><td><span data-ttu-id="d044f-673">Tijd van de gegevens.</span><span class="sxs-lookup"><span data-stu-id="d044f-673">Time of data.</span></span></td></tr><tr><td><span data-ttu-id="d044f-674">Gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="d044f-674">Event</span></span></td><td><span data-ttu-id="d044f-675">Er is geen; Indien opgegeven en klik vervolgens datum moet ook worden geplaatst</span><span class="sxs-lookup"><span data-stu-id="d044f-675">No; if supplied then must also put date</span></span></td><td><span data-ttu-id="d044f-676">Een van de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="d044f-676">One of hello following:</span></span><br><span data-ttu-id="d044f-677">• Klik</span><span class="sxs-lookup"><span data-stu-id="d044f-677">• Click</span></span><br><span data-ttu-id="d044f-678">• RecommendationClick</span><span class="sxs-lookup"><span data-stu-id="d044f-678">• RecommendationClick</span></span><br><span data-ttu-id="d044f-679">• AddShopCart</span><span class="sxs-lookup"><span data-stu-id="d044f-679">•    AddShopCart</span></span><br><span data-ttu-id="d044f-680">• RemoveShopCart</span><span class="sxs-lookup"><span data-stu-id="d044f-680">• RemoveShopCart</span></span><br><span data-ttu-id="d044f-681">• Aankoop</span><span class="sxs-lookup"><span data-stu-id="d044f-681">• Purchase</span></span></td><td></td></tr></table><br><span data-ttu-id="d044f-682">Maximale bestandsgrootte: 200MB</span><span class="sxs-lookup"><span data-stu-id="d044f-682">Maximum file size: 200MB</span></span><br><br><span data-ttu-id="d044f-683">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d044f-683">Example:</span></span><br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

<span data-ttu-id="d044f-684">**Antwoord**:</span><span class="sxs-lookup"><span data-stu-id="d044f-684">**Response**:</span></span>

<span data-ttu-id="d044f-685">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-685">HTTP Status code: 200</span></span>

* <span data-ttu-id="d044f-686">`Feed\entry\content\properties\LineCount`-Het aantal regels is geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="d044f-686">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="d044f-687">`Feed\entry\content\properties\ErrorCount`-Het aantal regels dat niet is ingevoegd vanwege fout tooan.</span><span class="sxs-lookup"><span data-stu-id="d044f-687">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due tooan error.</span></span>
* <span data-ttu-id="d044f-688">`Feed\entry\content\properties\FileId`-Id van het bestand.</span><span class="sxs-lookup"><span data-stu-id="d044f-688">`Feed\entry\content\properties\FileId` - File identifier.</span></span>

<span data-ttu-id="d044f-689">OData-XML</span><span class="sxs-lookup"><span data-stu-id="d044f-689">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Add bulk usage data (usage file)</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T07:21:44Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">AddBulkUsageDataUsageFileEntity2</title>
    <updated>2014-10-05T07:21:44Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">33</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
        <d:FileId m:type="Edm.String">fead7c1c-db01-46c0-872f-65bcda36025d</d:FileId>
      </m:properties>
    </content>
      </entry>
    </feed>


#### <a name="912-using-data-acquisition"></a><span data-ttu-id="d044f-690">9.1.2.</span><span class="sxs-lookup"><span data-stu-id="d044f-690">9.1.2.</span></span> <span data-ttu-id="d044f-691">Met behulp van de gegevens verkrijgen</span><span class="sxs-lookup"><span data-stu-id="d044f-691">Using Data Acquisition</span></span>
<span data-ttu-id="d044f-692">Deze sectie wordt beschreven hoe toosend gebeurtenissen in real time tooAzure Machine Learning aanbevelingen meestal van uw website.</span><span class="sxs-lookup"><span data-stu-id="d044f-692">This section shows how toosend events in real time tooAzure Machine Learning Recommendations, usually from your website.</span></span>

| <span data-ttu-id="d044f-693">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-693">HTTP Method</span></span> | <span data-ttu-id="d044f-694">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-694">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-695">VERZENDEN</span><span class="sxs-lookup"><span data-stu-id="d044f-695">POST</span></span> |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27` |
| <span data-ttu-id="d044f-696">KOPTEKST</span><span class="sxs-lookup"><span data-stu-id="d044f-696">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="d044f-697">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-697">Parameter Name</span></span> | <span data-ttu-id="d044f-698">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-698">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-699">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-699">apiVersion</span></span> |<span data-ttu-id="d044f-700">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-700">1.0</span></span> |
| <span data-ttu-id="d044f-701">Aanvraagtekst</span><span class="sxs-lookup"><span data-stu-id="d044f-701">Request body</span></span> |<span data-ttu-id="d044f-702">Gebeurtenis gegevensinvoer voor elke gebeurtenis die u wilt toosend.</span><span class="sxs-lookup"><span data-stu-id="d044f-702">Event data entry for each event you want toosend.</span></span> <span data-ttu-id="d044f-703">Voor hello dezelfde gebruiker of browser sessie Hallo dezelfde ID in het Hallo-sessie-id-veld moet worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="d044f-703">You should send for hello same user or browser session hello same ID in hello SessionId field.</span></span> <span data-ttu-id="d044f-704">(Zie het voorbeeld van de hoofdtekst van de gebeurtenis is hieronder).</span><span class="sxs-lookup"><span data-stu-id="d044f-704">(See sample of event body below.)</span></span> |

* <span data-ttu-id="d044f-705">Voorbeeld voor gebeurtenis 'Klik':</span><span class="sxs-lookup"><span data-stu-id="d044f-705">Example for event 'Click':</span></span>
  
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
* <span data-ttu-id="d044f-706">Voorbeeld voor gebeurtenis 'RecommendationClick':</span><span class="sxs-lookup"><span data-stu-id="d044f-706">Example for event 'RecommendationClick':</span></span>
  
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
* <span data-ttu-id="d044f-707">Voorbeeld voor gebeurtenis 'AddShopCart':</span><span class="sxs-lookup"><span data-stu-id="d044f-707">Example for event 'AddShopCart':</span></span>
  
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
* <span data-ttu-id="d044f-708">Voorbeeld voor gebeurtenis 'RemoveShopCart':</span><span class="sxs-lookup"><span data-stu-id="d044f-708">Example for event 'RemoveShopCart':</span></span>
  
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
* <span data-ttu-id="d044f-709">Voorbeeld voor gebeurtenis 'Aankoop':</span><span class="sxs-lookup"><span data-stu-id="d044f-709">Example for event 'Purchase':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
            <EventData>
                <Name>Purchase</Name>
                <PurchaseItems>
                    <PurchaseItem>
                        <ItemId>ABBF8081-C5C0-4F09-9701-E1C7AC78304A</ItemId>
                        <Count>1</Count>
                    </PurchaseItem>
                    <PurchaseItem>
                        <ItemId>21BF8088-B6C0-4509-870C-11C0AC7F304B</ItemId>
                        <Count>3</Count>
                    </PurchaseItem>
                </PurchaseItems>
            </EventData>
        </EventData>
        </Event>
* <span data-ttu-id="d044f-710">Voorbeeld '2 gebeurtenissen op' en 'AddShopCart' verzenden:</span><span class="sxs-lookup"><span data-stu-id="d044f-710">Example sending 2 events, 'Click' and 'AddShopCart':</span></span>
  
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

<span data-ttu-id="d044f-711">**Antwoord**: HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-711">**Response**: HTTP Status code: 200</span></span>

### <a name="92----list-model-usage-files"></a><span data-ttu-id="d044f-712">9.2.</span><span class="sxs-lookup"><span data-stu-id="d044f-712">9.2.</span></span>    <span data-ttu-id="d044f-713">Informatie over het gebruik van lijst modelbestanden</span><span class="sxs-lookup"><span data-stu-id="d044f-713">List Model Usage Files</span></span>
<span data-ttu-id="d044f-714">Haalt de metagegevens van informatie over het gebruik van alle modelbestanden.</span><span class="sxs-lookup"><span data-stu-id="d044f-714">Retrieves metadata of all model usage files.</span></span>
<span data-ttu-id="d044f-715">Hallo gebruik van bestanden die zijn opgehaald één pagina tegelijk.</span><span class="sxs-lookup"><span data-stu-id="d044f-715">hello usage files will be retrieved one page at a time.</span></span> <span data-ttu-id="d044f-716">Elke pagina containes 100 items.</span><span class="sxs-lookup"><span data-stu-id="d044f-716">Each page containes 100 items.</span></span> <span data-ttu-id="d044f-717">Als u tooget items op een specifieke index wilt, kunt u Hallo $skip odata-parameter.</span><span class="sxs-lookup"><span data-stu-id="d044f-717">If you want tooget items at a particular index, you can use hello $skip odata parameter.</span></span> <span data-ttu-id="d044f-718">Bijvoorbeeld als u beginnen bij positie 100 tooget-items wilt, voegt u Hallo parameter $skip = 100 toohello-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="d044f-718">For instance if you want tooget items starting at position 100, add hello parameter $skip=100 toohello request.</span></span>

| <span data-ttu-id="d044f-719">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-719">HTTP Method</span></span> | <span data-ttu-id="d044f-720">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-720">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-721">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="d044f-721">GET</span></span> |`<rootURI>/ListModelUsageFiles?forModelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="d044f-722">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d044f-722">Example:</span></span><br>`<rootURI>/ListModelUsageFiles?forModelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&apiVersion=%271.0%27` |

| <span data-ttu-id="d044f-723">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-723">Parameter Name</span></span> | <span data-ttu-id="d044f-724">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-724">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-725">forModelId</span><span class="sxs-lookup"><span data-stu-id="d044f-725">forModelId</span></span> |<span data-ttu-id="d044f-726">De unieke id van het Hallo-model</span><span class="sxs-lookup"><span data-stu-id="d044f-726">Unique identifier of hello model</span></span> |
| <span data-ttu-id="d044f-727">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-727">apiVersion</span></span> |<span data-ttu-id="d044f-728">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-728">1.0</span></span> |
|  | |
| <span data-ttu-id="d044f-729">Aanvraagtekst</span><span class="sxs-lookup"><span data-stu-id="d044f-729">Request Body</span></span> |<span data-ttu-id="d044f-730">GEEN</span><span class="sxs-lookup"><span data-stu-id="d044f-730">NONE</span></span> |

<span data-ttu-id="d044f-731">**Antwoord**:</span><span class="sxs-lookup"><span data-stu-id="d044f-731">**Response**:</span></span>

<span data-ttu-id="d044f-732">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-732">HTTP Status code: 200</span></span>

<span data-ttu-id="d044f-733">Hallo-antwoord bevat één vermelding per bestand in gebruik.</span><span class="sxs-lookup"><span data-stu-id="d044f-733">hello response includes one entry per usage file.</span></span> <span data-ttu-id="d044f-734">Elk item heeft Hallo gegevens te volgen:</span><span class="sxs-lookup"><span data-stu-id="d044f-734">Each entry has hello following data:</span></span>

* <span data-ttu-id="d044f-735">`feed\entry\content\properties\Id`-Gebruik bestands-id</span><span class="sxs-lookup"><span data-stu-id="d044f-735">`feed\entry\content\properties\Id` - Usage file ID.</span></span>
* <span data-ttu-id="d044f-736">`feed\entry\content\properties\Length`-Lengte van de usage bestand in MB.</span><span class="sxs-lookup"><span data-stu-id="d044f-736">`feed\entry\content\properties\Length` - Usage file length in MB.</span></span>
* <span data-ttu-id="d044f-737">`feed\entry\content\properties\DateModified`-Datum wanneer Hallo gebruik bestand is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d044f-737">`feed\entry\content\properties\DateModified` - Date when hello usage file was created.</span></span>
* <span data-ttu-id="d044f-738">`feed\entry\content\properties\UseInModel`-Of Hallo-bestand voor gebruik in Hallo model wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d044f-738">`feed\entry\content\properties\UseInModel` - Whether hello usage file is used in hello model.</span></span>

<span data-ttu-id="d044f-739">OData-XML</span><span class="sxs-lookup"><span data-stu-id="d044f-739">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get a list of model's usage files info</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-30T09:40:25Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfModelsUsageFilesInfoEntity</title>
            <updated>2014-10-30T09:40:25Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Id m:type="Edm.String">4c067b42-e975-4cb2-8c98-a6ab80ed6d63</d:Id>
                    <d:Length m:type="Edm.Double">0</d:Length>
                    <d:DateModified m:type="Edm.String">10/30/2014 9:19:57 AM</d:DateModified>
                    <d:UseInModel m:type="Edm.String">true</d:UseInModel>
                </m:properties>
            </content>
        </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetAListOfModelsUsageFilesInfoEntity</title>
        <updated>2014-10-30T09:40:25Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">3126d816-4e80-4248-8339-1ebbdb9d544d</d:Id>
                <d:Length m:type="Edm.Double">0.001</d:Length>
                <d:DateModified m:type="Edm.String">10/30/2014 9:21:44 AM</d:DateModified>
                <d:UseInModel m:type="Edm.String">true</d:UseInModel>
              </m:properties>
        </content>
    </entry>
</feed>

### <a name="93----get-usage-statistics"></a><span data-ttu-id="d044f-740">9.3.</span><span class="sxs-lookup"><span data-stu-id="d044f-740">9.3.</span></span>    <span data-ttu-id="d044f-741">Gebruiksstatistieken ophalen</span><span class="sxs-lookup"><span data-stu-id="d044f-741">Get Usage Statistics</span></span>
<span data-ttu-id="d044f-742">Gebruiksstatistieken opgehaald.</span><span class="sxs-lookup"><span data-stu-id="d044f-742">Gets usage statistics.</span></span>

| <span data-ttu-id="d044f-743">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-743">HTTP Method</span></span> | <span data-ttu-id="d044f-744">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-744">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-745">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="d044f-745">GET</span></span> |`<rootURI>/GetUsageStatistics?modelId=%27<modelId>%27& startDate=%27<date>%27&endDate=%27<date>%27&eventTypes=%27<types>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="d044f-746">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d044f-746">Example:</span></span><br>`<rootURI>/GetUsageStatistics?modelId=%271d20c34f-dca1-4eac-8e5d-f299e4e4ad66%27&startDate=%272014%2F10%2F17T00%3A00%3A00%27&endDate=%272014%2F11%2F16T00%3A00%3A00%27&eventTypes=%271%2C2%2C3%2C4%2C5%27&apiVersion=%271.0%27` |

| <span data-ttu-id="d044f-747">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-747">Parameter Name</span></span> | <span data-ttu-id="d044f-748">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-748">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-749">Model</span><span class="sxs-lookup"><span data-stu-id="d044f-749">modelId</span></span> |<span data-ttu-id="d044f-750">De unieke id van het Hallo-model</span><span class="sxs-lookup"><span data-stu-id="d044f-750">Unique identifier of hello model</span></span> |
| <span data-ttu-id="d044f-751">Begindatum</span><span class="sxs-lookup"><span data-stu-id="d044f-751">startDate</span></span> |<span data-ttu-id="d044f-752">De begindatum.</span><span class="sxs-lookup"><span data-stu-id="d044f-752">Start date.</span></span> <span data-ttu-id="d044f-753">Indeling: jjjj/MM/ddTUU</span><span class="sxs-lookup"><span data-stu-id="d044f-753">Format: yyyy/MM/ddTHH:mm:ss</span></span> |
| <span data-ttu-id="d044f-754">EndDate bevat</span><span class="sxs-lookup"><span data-stu-id="d044f-754">endDate</span></span> |<span data-ttu-id="d044f-755">Einddatum.</span><span class="sxs-lookup"><span data-stu-id="d044f-755">End date.</span></span> <span data-ttu-id="d044f-756">Indeling: jjjj/MM/ddTUU</span><span class="sxs-lookup"><span data-stu-id="d044f-756">Format: yyyy/MM/ddTHH:mm:ss</span></span> |
| <span data-ttu-id="d044f-757">eigenschap eventTypes</span><span class="sxs-lookup"><span data-stu-id="d044f-757">eventTypes</span></span> |<span data-ttu-id="d044f-758">Door komma's gescheiden tekenreeks van gebeurtenis typen of null tooget alle gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="d044f-758">Comma-separated string of event types or null tooget all events</span></span> |
| <span data-ttu-id="d044f-759">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-759">apiVersion</span></span> |<span data-ttu-id="d044f-760">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-760">1.0</span></span> |
|  | |
| <span data-ttu-id="d044f-761">Aanvraagtekst</span><span class="sxs-lookup"><span data-stu-id="d044f-761">Request Body</span></span> |<span data-ttu-id="d044f-762">GEEN</span><span class="sxs-lookup"><span data-stu-id="d044f-762">NONE</span></span> |

<span data-ttu-id="d044f-763">**Antwoord**:</span><span class="sxs-lookup"><span data-stu-id="d044f-763">**Response**:</span></span>

<span data-ttu-id="d044f-764">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-764">HTTP Status code: 200</span></span>

<span data-ttu-id="d044f-765">Een verzameling van sleutel/waarde-elementen.</span><span class="sxs-lookup"><span data-stu-id="d044f-765">A collection of key/value elements.</span></span> <span data-ttu-id="d044f-766">Elke bevat Hallo som van gebeurtenissen voor een specifiek gebeurtenistype gegroepeerd per uur.</span><span class="sxs-lookup"><span data-stu-id="d044f-766">Each one contains hello sum of events for a specific event type grouped by hour.</span></span>

* <span data-ttu-id="d044f-767">`feed\entry[i]\content\properties\Key`-Bevat Hallo-tijd (gegroepeerd per uur) en Hallo gebeurtenistype.</span><span class="sxs-lookup"><span data-stu-id="d044f-767">`feed\entry[i]\content\properties\Key` - Contains hello time (grouped by hour) and hello event type.</span></span>
* <span data-ttu-id="d044f-768">`feed\entry[i]\content\properties\Value`-Het aantal totaal aantal gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="d044f-768">`feed\entry[i]\content\properties\Value` - Total event count.</span></span>

<span data-ttu-id="d044f-769">OData-XML</span><span class="sxs-lookup"><span data-stu-id="d044f-769">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get usage statistics</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-18T11:39:16Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/9/2014 8:00:00 AM;Click</d:Event>
                <d:Value m:type="Edm.String">5</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/9/2014 8:00:00 AM;RecommendationClick</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
              </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/1/2014 8:00:00 AM;RemoveShopCart</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/5/2014 8:00:00 AM;RemoveShopCart</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="94----get-usage-file-sample"></a><span data-ttu-id="d044f-770">9.4.</span><span class="sxs-lookup"><span data-stu-id="d044f-770">9.4.</span></span>    <span data-ttu-id="d044f-771">Gebruik-voorbeeldbestand ophalen</span><span class="sxs-lookup"><span data-stu-id="d044f-771">Get Usage File Sample</span></span>
<span data-ttu-id="d044f-772">Haalt Hallo eerste 2KB van het gebruik van de inhoud van bestand.</span><span class="sxs-lookup"><span data-stu-id="d044f-772">Retrieves hello first 2KB of usage file content.</span></span>

| <span data-ttu-id="d044f-773">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-773">HTTP Method</span></span> | <span data-ttu-id="d044f-774">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-774">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-775">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="d044f-775">GET</span></span> |`<rootURI>/GetUsageFileSample?modelId=%27<modelId>%27& fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="d044f-776">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d044f-776">Example:</span></span><br>`<rootURI>/GetUsageFileSample?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fileId=%274c067b42-e975-4cb2-8c98-a6ab80ed6d63%27&apiVersion=%271.0%27` |

| <span data-ttu-id="d044f-777">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-777">Parameter Name</span></span> | <span data-ttu-id="d044f-778">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-778">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-779">Model</span><span class="sxs-lookup"><span data-stu-id="d044f-779">modelId</span></span> |<span data-ttu-id="d044f-780">De unieke id van het Hallo-model</span><span class="sxs-lookup"><span data-stu-id="d044f-780">Unique identifier of hello model</span></span> |
| <span data-ttu-id="d044f-781">fileId</span><span class="sxs-lookup"><span data-stu-id="d044f-781">fileId</span></span> |<span data-ttu-id="d044f-782">De unieke id van de informatie over het gebruik van Hallo modelbestand</span><span class="sxs-lookup"><span data-stu-id="d044f-782">Unique identifier of hello model usage file</span></span> |
| <span data-ttu-id="d044f-783">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-783">apiVersion</span></span> |<span data-ttu-id="d044f-784">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-784">1.0</span></span> |
|  | |
| <span data-ttu-id="d044f-785">Aanvraagtekst</span><span class="sxs-lookup"><span data-stu-id="d044f-785">Request Body</span></span> |<span data-ttu-id="d044f-786">GEEN</span><span class="sxs-lookup"><span data-stu-id="d044f-786">NONE</span></span> |

<span data-ttu-id="d044f-787">**Antwoord**:</span><span class="sxs-lookup"><span data-stu-id="d044f-787">**Response**:</span></span>

<span data-ttu-id="d044f-788">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-788">HTTP Status code: 200</span></span>

<span data-ttu-id="d044f-789">Onbewerkte tekst wordt geretourneerd als antwoord:</span><span class="sxs-lookup"><span data-stu-id="d044f-789">Response is returned in raw text format:</span></span>

<pre>
85526,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
210926,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
116866,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
177458,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
274004,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
123883,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
37712,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
152249,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
250948,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
235588,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
158254,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
271195,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
141157,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
171118,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
225087,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
</pre>


### <a name="95----get-model-usage-file"></a><span data-ttu-id="d044f-790">9.5.</span><span class="sxs-lookup"><span data-stu-id="d044f-790">9.5.</span></span>    <span data-ttu-id="d044f-791">Informatie over het gebruik van modelbestand ophalen</span><span class="sxs-lookup"><span data-stu-id="d044f-791">Get Model Usage File</span></span>
<span data-ttu-id="d044f-792">Haalt de volledige inhoud Hallo van Hallo gebruik bestand.</span><span class="sxs-lookup"><span data-stu-id="d044f-792">Retrieves hello full content of hello usage file.</span></span>

| <span data-ttu-id="d044f-793">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-793">HTTP Method</span></span> | <span data-ttu-id="d044f-794">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-794">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-795">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="d044f-795">GET</span></span> |`<rootURI>/GetModelUsageFile?mid=%27<modelId>%27& fid=%27<fileId>%27&download=%27<download_value>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="d044f-796">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d044f-796">Example:</span></span><br>`<rootURI>/GetModelUsageFile?mid=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fid=%273126d816-4e80-4248-8339-1ebbdb9d544d%27&download=%271%27&apiVersion=%271.0%27` |

| <span data-ttu-id="d044f-797">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-797">Parameter Name</span></span> | <span data-ttu-id="d044f-798">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-798">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-799">Mid</span><span class="sxs-lookup"><span data-stu-id="d044f-799">mid</span></span> |<span data-ttu-id="d044f-800">De unieke id van het Hallo-model</span><span class="sxs-lookup"><span data-stu-id="d044f-800">Unique identifier of hello model</span></span> |
| <span data-ttu-id="d044f-801">bestands-id</span><span class="sxs-lookup"><span data-stu-id="d044f-801">fid</span></span> |<span data-ttu-id="d044f-802">De unieke id van de informatie over het gebruik van Hallo modelbestand</span><span class="sxs-lookup"><span data-stu-id="d044f-802">Unique identifier of hello model usage file</span></span> |
| <span data-ttu-id="d044f-803">Downloaden</span><span class="sxs-lookup"><span data-stu-id="d044f-803">download</span></span> |<span data-ttu-id="d044f-804">1</span><span class="sxs-lookup"><span data-stu-id="d044f-804">1</span></span> |
| <span data-ttu-id="d044f-805">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-805">apiVersion</span></span> |<span data-ttu-id="d044f-806">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-806">1.0</span></span> |
|  | |
| <span data-ttu-id="d044f-807">Aanvraagtekst</span><span class="sxs-lookup"><span data-stu-id="d044f-807">Request Body</span></span> |<span data-ttu-id="d044f-808">GEEN</span><span class="sxs-lookup"><span data-stu-id="d044f-808">NONE</span></span> |

<span data-ttu-id="d044f-809">**Antwoord**:</span><span class="sxs-lookup"><span data-stu-id="d044f-809">**Response**:</span></span>

<span data-ttu-id="d044f-810">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-810">HTTP Status code: 200</span></span>

<span data-ttu-id="d044f-811">Onbewerkte tekst wordt geretourneerd als antwoord:</span><span class="sxs-lookup"><span data-stu-id="d044f-811">Response is returned in raw text format:</span></span>

<pre>
85526,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
210926,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
116866,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
177458,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
274004,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
123883,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
37712,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
152249,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
250948,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
235588,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
158254,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
271195,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
141157,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
171118,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
225087,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
244881,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
50547,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
213090,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
260655,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
72214,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189334,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
36326,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189336,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189334,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
260655,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
162100,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
54946,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
260965,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
102758,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
112602,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
163925,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
262998,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
144717,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
</pre>

### <a name="96----delete-usage-file"></a><span data-ttu-id="d044f-812">9.6.</span><span class="sxs-lookup"><span data-stu-id="d044f-812">9.6.</span></span>    <span data-ttu-id="d044f-813">Gebruik bestand verwijderen</span><span class="sxs-lookup"><span data-stu-id="d044f-813">Delete Usage File</span></span>
<span data-ttu-id="d044f-814">Hallo opgegeven model gebruik bestand verwijderd.</span><span class="sxs-lookup"><span data-stu-id="d044f-814">Deletes hello specified model usage file.</span></span>

| <span data-ttu-id="d044f-815">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-815">HTTP Method</span></span> | <span data-ttu-id="d044f-816">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-816">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-817">VERWIJDEREN</span><span class="sxs-lookup"><span data-stu-id="d044f-817">DELETE</span></span> |`<rootURI>/DeleteUsageFile?modelId=%27<modelId>%27&fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="d044f-818">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d044f-818">Example:</span></span><br>`<rootURI>/DeleteUsageFile?modelId=%270f86d698-d0f4-4406-a684-d13d22c47a73%27&fileId=%27f2e0b09d-be5c-46b2-9ac2-c7f622e5e1a5%27&apiVersion=%271.0%27` |

| <span data-ttu-id="d044f-819">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-819">Parameter Name</span></span> | <span data-ttu-id="d044f-820">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-820">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-821">Model</span><span class="sxs-lookup"><span data-stu-id="d044f-821">modelId</span></span> |<span data-ttu-id="d044f-822">De unieke id van het Hallo-model</span><span class="sxs-lookup"><span data-stu-id="d044f-822">Unique identifier of hello model</span></span> |
| <span data-ttu-id="d044f-823">fileId</span><span class="sxs-lookup"><span data-stu-id="d044f-823">fileId</span></span> |<span data-ttu-id="d044f-824">De unieke id van Hallo bestand toobe verwijderd</span><span class="sxs-lookup"><span data-stu-id="d044f-824">Unique identifier of hello file toobe deleted</span></span> |
| <span data-ttu-id="d044f-825">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-825">apiVersion</span></span> |<span data-ttu-id="d044f-826">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-826">1.0</span></span> |
|  | |
| <span data-ttu-id="d044f-827">Aanvraagtekst</span><span class="sxs-lookup"><span data-stu-id="d044f-827">Request Body</span></span> |<span data-ttu-id="d044f-828">GEEN</span><span class="sxs-lookup"><span data-stu-id="d044f-828">NONE</span></span> |

<span data-ttu-id="d044f-829">**Antwoord**:</span><span class="sxs-lookup"><span data-stu-id="d044f-829">**Response**:</span></span>

<span data-ttu-id="d044f-830">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-830">HTTP Status code: 200</span></span>

### <a name="97----delete-all-usage-files"></a><span data-ttu-id="d044f-831">9.7.</span><span class="sxs-lookup"><span data-stu-id="d044f-831">9.7.</span></span>    <span data-ttu-id="d044f-832">Verwijder alle bestanden met gebruiksgegevens</span><span class="sxs-lookup"><span data-stu-id="d044f-832">Delete All Usage Files</span></span>
<span data-ttu-id="d044f-833">Hiermee verwijdert u alle modelbestanden voor informatie over het gebruik.</span><span class="sxs-lookup"><span data-stu-id="d044f-833">Deletes all model usage files.</span></span>

| <span data-ttu-id="d044f-834">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-834">HTTP Method</span></span> | <span data-ttu-id="d044f-835">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-835">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-836">VERWIJDEREN</span><span class="sxs-lookup"><span data-stu-id="d044f-836">DELETE</span></span> |`<rootURI>/DeleteAllUsageFiles?modelId=%27<modelId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="d044f-837">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d044f-837">Example:</span></span><br>`<rootURI>/DeleteAllUsageFiles?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&apiVersion=%271.0%27` |

| <span data-ttu-id="d044f-838">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-838">Parameter Name</span></span> | <span data-ttu-id="d044f-839">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-839">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-840">Model</span><span class="sxs-lookup"><span data-stu-id="d044f-840">modelId</span></span> |<span data-ttu-id="d044f-841">De unieke id van het Hallo-model</span><span class="sxs-lookup"><span data-stu-id="d044f-841">Unique identifier of hello model</span></span> |
| <span data-ttu-id="d044f-842">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-842">apiVersion</span></span> |<span data-ttu-id="d044f-843">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-843">1.0</span></span> |
|  | |
| <span data-ttu-id="d044f-844">Aanvraagtekst</span><span class="sxs-lookup"><span data-stu-id="d044f-844">Request Body</span></span> |<span data-ttu-id="d044f-845">GEEN</span><span class="sxs-lookup"><span data-stu-id="d044f-845">NONE</span></span> |

<span data-ttu-id="d044f-846">**Antwoord**:</span><span class="sxs-lookup"><span data-stu-id="d044f-846">**Response**:</span></span>

<span data-ttu-id="d044f-847">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-847">HTTP Status code: 200</span></span>

## <a name="10-features"></a><span data-ttu-id="d044f-848">10. Functies</span><span class="sxs-lookup"><span data-stu-id="d044f-848">10. Features</span></span>
<span data-ttu-id="d044f-849">Deze sectie wordt beschreven hoe tooretrieve voorzien van informatie, zoals Hallo geïmporteerd functies en hun waarden, hun positie, en wanneer deze positie is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="d044f-849">This section shows how tooretrieve feature information, such as hello imported features and their values, their rank, and when this rank was allocated.</span></span> <span data-ttu-id="d044f-850">Functies worden geïmporteerd als onderdeel van de catalogusgegevens Hallo en vervolgens hun positie is gekoppeld als het een absolute build is voltooid.</span><span class="sxs-lookup"><span data-stu-id="d044f-850">Features are imported as part of hello catalog data, and then their rank is associated when a rank build is done.</span></span>
<span data-ttu-id="d044f-851">Positie van de functie kunt volgens toohello patroon van gebruiksgegevens en type items wijzigen.</span><span class="sxs-lookup"><span data-stu-id="d044f-851">Feature rank can change according toohello pattern of usage data and type of items.</span></span> <span data-ttu-id="d044f-852">Maar voor consistent gebruik/items, Hallo positie hebben slechts kleine schommelingen.</span><span class="sxs-lookup"><span data-stu-id="d044f-852">But for consistent usage/items, hello rank should have only small fluctuations.</span></span>
<span data-ttu-id="d044f-853">Hallo-positie van functies is een niet-negatief getal.</span><span class="sxs-lookup"><span data-stu-id="d044f-853">hello rank of features is a non-negative number.</span></span> <span data-ttu-id="d044f-854">Hallo nummer 0 betekent dat Hallo-functie niet is gerangschikt (gebeurt als u bij het aanroepen van deze API voorafgaande toohello voltooiing van de eerste positie build Hallo).</span><span class="sxs-lookup"><span data-stu-id="d044f-854">hello  number 0 means that hello feature was not ranked (happens if you invoke this API prior toohello completion of hello first rank build).</span></span> <span data-ttu-id="d044f-855">Hallo datum waarop Hallo positie is toegekend, Hallo score nieuwheid wordt genoemd.</span><span class="sxs-lookup"><span data-stu-id="d044f-855">hello date at which hello rank was attributed is called hello score freshness.</span></span>

### <a name="101-get-features-info-for-last-rank-build"></a><span data-ttu-id="d044f-856">10.1.</span><span class="sxs-lookup"><span data-stu-id="d044f-856">10.1.</span></span> <span data-ttu-id="d044f-857">Functies Info ophalen (voor laatste positie Build)</span><span class="sxs-lookup"><span data-stu-id="d044f-857">Get Features Info (For Last Rank Build)</span></span>
<span data-ttu-id="d044f-858">Hallo functie informatie, met inbegrip van ranking voor Hallo laatste geslaagde positie build opgehaald.</span><span class="sxs-lookup"><span data-stu-id="d044f-858">Retrieves hello feature information, including ranking, for hello last successful rank build.</span></span>

| <span data-ttu-id="d044f-859">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-859">HTTP Method</span></span> | <span data-ttu-id="d044f-860">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-860">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-861">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="d044f-861">GET</span></span> |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="d044f-862">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d044f-862">Example:</span></span><br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&apiVersion=%271.0%27` |

| <span data-ttu-id="d044f-863">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-863">Parameter Name</span></span> | <span data-ttu-id="d044f-864">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-864">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-865">Model</span><span class="sxs-lookup"><span data-stu-id="d044f-865">modelId</span></span> |<span data-ttu-id="d044f-866">De unieke id van het Hallo-model</span><span class="sxs-lookup"><span data-stu-id="d044f-866">Unique identifier of hello model</span></span> |
| <span data-ttu-id="d044f-867">samplingSize</span><span class="sxs-lookup"><span data-stu-id="d044f-867">samplingSize</span></span> |<span data-ttu-id="d044f-868">Het aantal waarden tooinclude voor elk onderdeel volgens toohello gegevens aanwezig zijn in de catalogus Hallo.</span><span class="sxs-lookup"><span data-stu-id="d044f-868">Number of values tooinclude for each feature according toohello data present in hello catalog.</span></span> <br/><span data-ttu-id="d044f-869">Mogelijke waarden zijn:</span><span class="sxs-lookup"><span data-stu-id="d044f-869">Possible values are:</span></span><br> <span data-ttu-id="d044f-870">-1 - alle voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="d044f-870">-1 - All samples.</span></span> <br><span data-ttu-id="d044f-871">0 - geen steekproeven.</span><span class="sxs-lookup"><span data-stu-id="d044f-871">0 - No sampling.</span></span> <br><span data-ttu-id="d044f-872">N - N steekproeven voor de functienaam van elke retourneren.</span><span class="sxs-lookup"><span data-stu-id="d044f-872">N - Return N samples for each feature name.</span></span> |
| <span data-ttu-id="d044f-873">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-873">apiVersion</span></span> |<span data-ttu-id="d044f-874">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-874">1.0</span></span> |
|  | |
| <span data-ttu-id="d044f-875">Aanvraagtekst</span><span class="sxs-lookup"><span data-stu-id="d044f-875">Request Body</span></span> |<span data-ttu-id="d044f-876">GEEN</span><span class="sxs-lookup"><span data-stu-id="d044f-876">NONE</span></span> |

<span data-ttu-id="d044f-877">**Antwoord**:</span><span class="sxs-lookup"><span data-stu-id="d044f-877">**Response**:</span></span>

<span data-ttu-id="d044f-878">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-878">HTTP Status code: 200</span></span>

<span data-ttu-id="d044f-879">Hallo-antwoord bevat een lijst met functie info vermeldingen.</span><span class="sxs-lookup"><span data-stu-id="d044f-879">hello response contains a list of feature info entries.</span></span> <span data-ttu-id="d044f-880">Elk item bevat:</span><span class="sxs-lookup"><span data-stu-id="d044f-880">Each entry contains:</span></span>

* <span data-ttu-id="d044f-881">`feed/entry/content/m:properties/d:Name`-Naam functie.</span><span class="sxs-lookup"><span data-stu-id="d044f-881">`feed/entry/content/m:properties/d:Name` - Feature name.</span></span>
* <span data-ttu-id="d044f-882">`feed/entry/content/m:properties/d:RankUpdateDate`-De datum op welke Hallo positie toegewezen toothis functie, ook is</span><span class="sxs-lookup"><span data-stu-id="d044f-882">`feed/entry/content/m:properties/d:RankUpdateDate` - Date at which hello rank was allocated toothis feature, a.k.a.</span></span> <span data-ttu-id="d044f-883">score nieuwheid functie.</span><span class="sxs-lookup"><span data-stu-id="d044f-883">score freshness feature.</span></span> <span data-ttu-id="d044f-884">Een historische datum ('0001-01-01T00:00:00') betekent dat er geen waarden van positie build is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d044f-884">A historical date ('0001-01-01T00:00:00') means that no rank build was performed.</span></span>
* <span data-ttu-id="d044f-885">`feed/entry/content/m:properties/d:Rank`-Functie positie (float).</span><span class="sxs-lookup"><span data-stu-id="d044f-885">`feed/entry/content/m:properties/d:Rank` - Feature rank (float).</span></span> <span data-ttu-id="d044f-886">Positie van 2.0 en omhoog wordt beschouwd als een goede functie.</span><span class="sxs-lookup"><span data-stu-id="d044f-886">A rank of 2.0 and up is considered a good feature.</span></span>
* <span data-ttu-id="d044f-887">`feed/entry/content/m:properties/d:SampleValues`-Door komma's gescheiden lijst met waarden toohello steekproeven grootte aangevraagd.</span><span class="sxs-lookup"><span data-stu-id="d044f-887">`feed/entry/content/m:properties/d:SampleValues` - Comma-separated list of values up toohello sampling size requested.</span></span>

<span data-ttu-id="d044f-888">OData-XML</span><span class="sxs-lookup"><span data-stu-id="d044f-888">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get hello features of a model</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2015-01-08T13:15:02Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Name m:type="Edm.String">Author</d:Name>
                <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
                <d:Rank m:type="Edm.String">0</d:Rank>
                <d:SampleValues m:type="Edm.String">A. A. Attanasio, A. A. Milne, A. Bates, A. C. Bhaktivedanta Swami Prabhupada et al., A. C. Crispin, A. C. Doyle, A. C. H. Smith, A. E. Parker, A. J. Holt, A. J. Matthews</d:SampleValues>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Name m:type="Edm.String">Publisher</d:Name>
                <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
                <d:Rank m:type="Edm.String">0</d:Rank>
                <d:SampleValues m:type="Edm.String">A. Mondadori, Abacus, Abacus Press, Abacus Uk, Abstract Studio, Acacia Press, Academy Chicago Publishers, Ace Books, ACE Charter, Actar</d:SampleValues>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1"/>
        <contenttype="application/xml">
        <m:properties>
            <d:Name m:type="Edm.String">Year</d:Name>
            <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
            <d:Rank m:type="Edm.String">0</d:Rank>
            <d:SampleValues m:type="Edm.String">0, 1920, 1926, 1927, 1929, 1930, 1932, 1942, 1943, 1946</d:SampleValues>
        </m:properties>
        </content>
    </entry>
</feed>

### <a name="102-get-features-info-for-specific-rank-build"></a><span data-ttu-id="d044f-889">10.2.</span><span class="sxs-lookup"><span data-stu-id="d044f-889">10.2.</span></span> <span data-ttu-id="d044f-890">Functies Info ophalen (voor een specifieke positie Build)</span><span class="sxs-lookup"><span data-stu-id="d044f-890">Get Features Info (For Specific Rank Build)</span></span>
<span data-ttu-id="d044f-891">Hallo functie informatie, met inbegrip van Hallo rangschikking voor een specifieke positie build opgehaald.</span><span class="sxs-lookup"><span data-stu-id="d044f-891">Retrieves hello feature information, including hello ranking for a specific rank build.</span></span>

| <span data-ttu-id="d044f-892">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-892">HTTP Method</span></span> | <span data-ttu-id="d044f-893">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-893">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-894">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="d044f-894">GET</span></span> |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&rankBuildId=<rankBuildId>&apiVersion=%271.0%27`<br><br><span data-ttu-id="d044f-895">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d044f-895">Example:</span></span><br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&rankBuildId=1000551&apiVersion=%271.0%27` |

| <span data-ttu-id="d044f-896">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-896">Parameter Name</span></span> | <span data-ttu-id="d044f-897">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-897">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-898">Model</span><span class="sxs-lookup"><span data-stu-id="d044f-898">modelId</span></span> |<span data-ttu-id="d044f-899">De unieke id van het Hallo-model</span><span class="sxs-lookup"><span data-stu-id="d044f-899">Unique identifier of hello model</span></span> |
| <span data-ttu-id="d044f-900">samplingSize</span><span class="sxs-lookup"><span data-stu-id="d044f-900">samplingSize</span></span> |<span data-ttu-id="d044f-901">Het aantal waarden tooinclude voor elk onderdeel volgens toohello gegevens aanwezig zijn in de catalogus Hallo.</span><span class="sxs-lookup"><span data-stu-id="d044f-901">Number of values tooinclude for each feature according toohello data present in hello catalog.</span></span><br/> <span data-ttu-id="d044f-902">Mogelijke waarden zijn:</span><span class="sxs-lookup"><span data-stu-id="d044f-902">Possible values are:</span></span><br> <span data-ttu-id="d044f-903">-1 - alle voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="d044f-903">-1 - All samples.</span></span> <br><span data-ttu-id="d044f-904">0 - geen steekproeven.</span><span class="sxs-lookup"><span data-stu-id="d044f-904">0 - No sampling.</span></span> <br><span data-ttu-id="d044f-905">N - N steekproeven voor de functienaam van elke retourneren.</span><span class="sxs-lookup"><span data-stu-id="d044f-905">N - Return N samples for each feature name.</span></span> |
| <span data-ttu-id="d044f-906">rankBuildId</span><span class="sxs-lookup"><span data-stu-id="d044f-906">rankBuildId</span></span> |<span data-ttu-id="d044f-907">De unieke id van de waarden van positie build Hallo of -1 voor de laatste positie build Hallo</span><span class="sxs-lookup"><span data-stu-id="d044f-907">Unique identifier of hello rank build or -1 for hello last rank build</span></span> |
| <span data-ttu-id="d044f-908">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-908">apiVersion</span></span> |<span data-ttu-id="d044f-909">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-909">1.0</span></span> |
|  | |
| <span data-ttu-id="d044f-910">Aanvraagtekst</span><span class="sxs-lookup"><span data-stu-id="d044f-910">Request Body</span></span> |<span data-ttu-id="d044f-911">GEEN</span><span class="sxs-lookup"><span data-stu-id="d044f-911">NONE</span></span> |

<span data-ttu-id="d044f-912">**Antwoord**:</span><span class="sxs-lookup"><span data-stu-id="d044f-912">**Response**:</span></span>

<span data-ttu-id="d044f-913">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-913">HTTP Status code: 200</span></span>

<span data-ttu-id="d044f-914">Hallo-antwoord bevat een lijst met functie info vermeldingen.</span><span class="sxs-lookup"><span data-stu-id="d044f-914">hello response contains a list of feature info entries.</span></span> <span data-ttu-id="d044f-915">Elk item bevat:</span><span class="sxs-lookup"><span data-stu-id="d044f-915">Each entry contains:</span></span>

* <span data-ttu-id="d044f-916">`feed/entry/content/m:properties/d:Name`-Naam functie.</span><span class="sxs-lookup"><span data-stu-id="d044f-916">`feed/entry/content/m:properties/d:Name` - Feature name.</span></span>
* <span data-ttu-id="d044f-917">`feed/entry/content/m:properties/d:RankUpdateDate`-De datum op welke Hallo positie toegewezen toothis functie, ook is</span><span class="sxs-lookup"><span data-stu-id="d044f-917">`feed/entry/content/m:properties/d:RankUpdateDate` - Date at which hello rank was allocated toothis feature, a.k.a.</span></span> <span data-ttu-id="d044f-918">score nieuwheid functie.</span><span class="sxs-lookup"><span data-stu-id="d044f-918">score freshness feature.</span></span> <span data-ttu-id="d044f-919">Een historische datum ('0001-01-01T00:00:00') betekent dat er geen waarden van positie build is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d044f-919">A historical date ('0001-01-01T00:00:00') means that no rank build was performed.</span></span>
* <span data-ttu-id="d044f-920">`feed/entry/content/m:properties/d:Rank`-Functie positie (float).</span><span class="sxs-lookup"><span data-stu-id="d044f-920">`feed/entry/content/m:properties/d:Rank` - Feature rank (float).</span></span> <span data-ttu-id="d044f-921">Positie van 2.0 en omhoog wordt beschouwd als een goede functie.</span><span class="sxs-lookup"><span data-stu-id="d044f-921">A rank of 2.0 and up is considered a good feature.</span></span>
* <span data-ttu-id="d044f-922">`feed/entry/content/m:properties/d:SampleValues`-Door komma's gescheiden lijst met waarden toohello steekproeven grootte aangevraagd.</span><span class="sxs-lookup"><span data-stu-id="d044f-922">`feed/entry/content/m:properties/d:SampleValues` - Comma-separated list of values up toohello sampling size requested.</span></span>

<span data-ttu-id="d044f-923">OData</span><span class="sxs-lookup"><span data-stu-id="d044f-923">OData</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get hello features of a model</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2015-01-08T13:54:22Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Author</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">3.38867426</d:Rank>
                    <d:SampleValues m:type="Edm.String">A. A. Attanasio, A. A. Milne, A. Bates, A. C. Bhaktivedanta Swami Prabhupada et al., A. C. Crispin, A. C. Doyle, A. C. H. Smith, A. E. Parker, A. J. Holt, A. J. Matthews</d:SampleValues>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Publisher</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">1.67839336</d:Rank>
                    <d:SampleValues m:type="Edm.String">A. Mondadori, Abacus, Abacus Press, Abacus Uk, Abstract Studio, Acacia Press, Academy Chicago Publishers, Ace Books, ACE Charter, Actar</d:SampleValues>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Year</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">1.12352145</d:Rank>
                    <d:SampleValues m:type="Edm.String">0, 1920, 1926, 1927, 1929, 1930, 1932, 1942, 1943, 1946</d:SampleValues>
                </m:properties>
            </content>
        </entry>
    </feed>


## <a name="11-build"></a><span data-ttu-id="d044f-924">11. Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="d044f-924">11. Build</span></span>
  <span data-ttu-id="d044f-925">Deze sectie wordt uitgelegd Hallo verschillende API's toobuilds gerelateerd.</span><span class="sxs-lookup"><span data-stu-id="d044f-925">This section explains hello different APIs related toobuilds.</span></span> <span data-ttu-id="d044f-926">Er zijn 3 soorten builds: een aanbeveling build, een positie build en een build FBT (vaak gekocht samen).</span><span class="sxs-lookup"><span data-stu-id="d044f-926">There are 3 types of builds: a recommendation build, a rank build and an FBT (frequently bought together) build.</span></span>

<span data-ttu-id="d044f-927">Hallo aanbeveling build-doel is een model aanbeveling voor voorspellingen gebruikt toogenerate.</span><span class="sxs-lookup"><span data-stu-id="d044f-927">hello recommendation build's purpose is toogenerate a recommendation model used for predictions.</span></span> <span data-ttu-id="d044f-928">Voorspellingen (voor dit type build) er zijn twee versies:</span><span class="sxs-lookup"><span data-stu-id="d044f-928">Predictions (for this type of build) come in two flavors:</span></span>

* <span data-ttu-id="d044f-929">I2I - ook</span><span class="sxs-lookup"><span data-stu-id="d044f-929">I2I - a.k.a.</span></span> <span data-ttu-id="d044f-930">Item tooItem aanbevelingen - gegeven een item of een lijst van artikelen met deze optie een lijst met items die waarschijnlijk toobe van groot belang zijn wordt voorspellen.</span><span class="sxs-lookup"><span data-stu-id="d044f-930">Item tooItem recommendations - given an item or a list of items this option will predict a list of items that are likely toobe of high interest.</span></span>
* <span data-ttu-id="d044f-931">U2I - ook</span><span class="sxs-lookup"><span data-stu-id="d044f-931">U2I - a.k.a.</span></span> <span data-ttu-id="d044f-932">Gebruiker tooItem aanbevelingen - basis van een gebruikers-id (en optioneel een lijst met items) deze optie wordt een lijst met items die waarschijnlijk toobe van groot belang voor de opgegeven gebruiker (en de aanvullende keuze van items) Hallo zijn voorspellen.</span><span class="sxs-lookup"><span data-stu-id="d044f-932">User tooItem recommendations - given a user id (and optionally a list of items) this option will predict a list of items that are likely toobe of high interest for hello given user (and its additional choice of items).</span></span> <span data-ttu-id="d044f-933">Hallo U2I aanbevelingen zijn gebaseerd op Hallo overzicht van items die zijn van belang zijn voor de gebruiker Hallo toohello tijd Hallo model is opgebouwd.</span><span class="sxs-lookup"><span data-stu-id="d044f-933">hello U2I recommendations are based on hello history of items that were of interest for hello user up toohello time hello model was built.</span></span>

<span data-ttu-id="d044f-934">Een positie build is een technische build waarmee u toolearn over Hallo nut van uw functies.</span><span class="sxs-lookup"><span data-stu-id="d044f-934">A rank build is a technical build that allows you toolearn about hello usefulness of your features.</span></span> <span data-ttu-id="d044f-935">Meestal in volgorde tooget Hallo beste resultaat voor een model in aanbeveling met betrekking tot de functies, moet u Hallo stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="d044f-935">Usually, in order tooget hello best result for a recommendation model involving features, you should take hello following steps:</span></span>

* <span data-ttu-id="d044f-936">Activeren van een absolute build (tenzij een stabiele Hallo score van uw functies) en wacht tot u Hallo functie score ophalen.</span><span class="sxs-lookup"><span data-stu-id="d044f-936">Trigger a rank build (unless hello score of your features is stable) and wait till you get hello feature score.</span></span>
* <span data-ttu-id="d044f-937">Hallo-positie van uw functies ophalen door de aanroepende Hallo [functies Info ophalen](#101-get-features-info-for-last-rank-build) API.</span><span class="sxs-lookup"><span data-stu-id="d044f-937">Retrieve hello rank of your features by calling hello [Get Features Info](#101-get-features-info-for-last-rank-build) API.</span></span>
* <span data-ttu-id="d044f-938">Configureer een aanbeveling build met Hallo volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="d044f-938">Configure a recommendation build with hello following parameters:</span></span>
  * <span data-ttu-id="d044f-939">`useFeatureInModel`-TooTrue set.</span><span class="sxs-lookup"><span data-stu-id="d044f-939">`useFeatureInModel` - Set tooTrue.</span></span>
  * <span data-ttu-id="d044f-940">`ModelingFeatureList`-Set tooa door komma's gescheiden lijst met functies met een score van 2.0 of meer (op basis van twee of meer toohello die u hebt opgehaald in de vorige stap Hallo).</span><span class="sxs-lookup"><span data-stu-id="d044f-940">`ModelingFeatureList` - Set tooa comma-separated list of features with a score of 2.0 or more (according toohello ranks you retrieved in hello previous step).</span></span>
  * <span data-ttu-id="d044f-941">`AllowColdItemPlacement`-TooTrue set.</span><span class="sxs-lookup"><span data-stu-id="d044f-941">`AllowColdItemPlacement` - Set tooTrue.</span></span>
  * <span data-ttu-id="d044f-942">U kunt desgewenst instellen `EnableFeatureCorrelation` tooTrue en `ReasoningFeatureList` toohello eigenschappenlijst gewenste toouse uitleg (meestal hello dezelfde lijst met functies in modellering of een sublijst gebruikt).</span><span class="sxs-lookup"><span data-stu-id="d044f-942">Optionally you can set `EnableFeatureCorrelation` tooTrue and `ReasoningFeatureList` toohello list of features you want toouse for explanations (usually hello same list of features used in modelling or a sublist).</span></span>
* <span data-ttu-id="d044f-943">Trigger Hallo aanbeveling build Hello geconfigureerd parameters.</span><span class="sxs-lookup"><span data-stu-id="d044f-943">Trigger hello recommendation build with hello configured parameters.</span></span>

<span data-ttu-id="d044f-944">Opmerking: Als u niet alle parameters configureert (bijvoorbeeld aanroepen Hallo aanbeveling build zonder parameters) of u niet expliciet uitschakelt Hallo informatie over het gebruik van functies (bijvoorbeeld `UseFeatureInModel` tooFalse ingesteld), system Hallo Hallo functie-gerelateerde parameters wordt instellen Als een positie build bestaat, worden in toohello waarden die hierboven beschreven.</span><span class="sxs-lookup"><span data-stu-id="d044f-944">Note: If you do not configure any parameters (e.g. invoke hello recommendation build without parameters) or you do not explicitly disable hello usage of features (e.g. `UseFeatureInModel` set tooFalse), hello system will set up hello feature-related parameters toohello explained values above in case a rank build exists.</span></span>

<span data-ttu-id="d044f-945">Er is geen beperking voor het uitvoeren van een absolute build en een aanbeveling build gelijktijdig voor Hallo dezelfde model.</span><span class="sxs-lookup"><span data-stu-id="d044f-945">There is no restriction on running a rank build and a recommendation build concurrently for hello same model.</span></span> <span data-ttu-id="d044f-946">U kunt twee versies van dezelfde typt u op dezelfde model parallel Hallo Hallo evenwel niet uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="d044f-946">Nevertheless, you cannot run two builds of hello same type on hello same model in parallel.</span></span>

<span data-ttu-id="d044f-947">Een build FBT (vaak gekocht samen) is nog een andere aanbevelingen algoritme soms 'conservatief' recommender die geschikt is voor catalogi die niet in aard homogene aangeroepen (homogene: books, films, sommige voeding wijze; niet-homogeen: computer en apparaten, tussen domeinen, zeer diverse).</span><span class="sxs-lookup"><span data-stu-id="d044f-947">An FBT (Frequently bought together) build is yet another recommendations algorithm called sometimes "conservative" recommender, which is good for catalogs that are not homogeneous in nature (homogeneous: books, movies, some food, fashion; non-homogeneous: computer and devices, cross-domain, highly diverse).</span></span>

<span data-ttu-id="d044f-948">Opmerking: als hello informatie over het van gebruiksbestanden die u hebt geüpload Hallo optioneel veld 'gebeurtenistype bevatten' vervolgens voor FBT modellering alleen 'Aankoop' gebeurtenissen wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d044f-948">Note: if hello usage files that you uploaded contain hello optional field "event type" then for FBT modelling only "Purchase" events will be used.</span></span> <span data-ttu-id="d044f-949">Als geen gebeurtenistype is opgegeven, dat worden alle gebeurtenissen worden beschouwd als aankoop.</span><span class="sxs-lookup"><span data-stu-id="d044f-949">If no event type is provided all events will be considered as purchase.</span></span>

#### <a name="111-build-parameters"></a><span data-ttu-id="d044f-950">11.1 bouwen parameters</span><span class="sxs-lookup"><span data-stu-id="d044f-950">11.1 Build parameters</span></span>
<span data-ttu-id="d044f-951">Elk BuildType kan worden geconfigureerd via een set parameters (afgebeeld hieronder).</span><span class="sxs-lookup"><span data-stu-id="d044f-951">Each build type can be configured via a set of parameters (depicted below).</span></span> <span data-ttu-id="d044f-952">Als u Hallo-parameters niet configureert, worden in Hallo system waarden toohello parameters volgens toohello aanwezige informatie Hallo gelijktijdig activeren van een build automatisch kenmerk.</span><span class="sxs-lookup"><span data-stu-id="d044f-952">If you don't configure hello parameters, hello system will automatically attribute values toohello parameters according toohello information present at hello time you trigger a build.</span></span>

##### <a name="1111-usage-condenser"></a><span data-ttu-id="d044f-953">11.1.1.</span><span class="sxs-lookup"><span data-stu-id="d044f-953">11.1.1.</span></span> <span data-ttu-id="d044f-954">Gebruik koeler</span><span class="sxs-lookup"><span data-stu-id="d044f-954">Usage condenser</span></span>
<span data-ttu-id="d044f-955">Gebruikers- of artikelen met enkele gebruik punten bevatten mogelijk meer ruis dan informatie.</span><span class="sxs-lookup"><span data-stu-id="d044f-955">Users or items with few usage points might contain more noise than information.</span></span> <span data-ttu-id="d044f-956">Hallo-systeem probeert toopredict Hallo minimum aantal gebruik punten per gebruiker/item toobe gebruikt in een model.</span><span class="sxs-lookup"><span data-stu-id="d044f-956">hello system attempts toopredict hello minimal number of usage points per user/item toobe used in a model.</span></span> <span data-ttu-id="d044f-957">Dit nummer is binnen het bereik van Hallo gedefinieerd door Hallo ItemCutoffLowerBound en ItemCutoffUpperBound parameters voor artikelen en Hallo bereik dat is gedefinieerd door Hallo UserCutOffLowerBound en UserCutoffUpperBound parameters voor gebruikers.</span><span class="sxs-lookup"><span data-stu-id="d044f-957">This number will be within hello range defined by hello ItemCutoffLowerBound and ItemCutoffUpperBound parameters for items, and hello range defined by hello UserCutOffLowerBound and UserCutoffUpperBound parameters for users.</span></span> <span data-ttu-id="d044f-958">Hallo koeler effect op items of gebruikers kan worden geminimaliseerd door ten minste één van de bijbehorende grenzen toozero Hallo-instelling.</span><span class="sxs-lookup"><span data-stu-id="d044f-958">hello condenser effect on items or users can be minimized by setting at least one of hello corresponding bounds toozero.</span></span>

##### <a name="1112-rank-build-parameters"></a><span data-ttu-id="d044f-959">11.1.2.</span><span class="sxs-lookup"><span data-stu-id="d044f-959">11.1.2.</span></span> <span data-ttu-id="d044f-960">Positie bouwen parameters</span><span class="sxs-lookup"><span data-stu-id="d044f-960">Rank build parameters</span></span>
<span data-ttu-id="d044f-961">Hallo in de volgende tabel beschrijft Hallo build parameters voor een positie build.</span><span class="sxs-lookup"><span data-stu-id="d044f-961">hello table below depicts hello build parameters for a rank build.</span></span>

| <span data-ttu-id="d044f-962">Sleutel</span><span class="sxs-lookup"><span data-stu-id="d044f-962">Key</span></span> | <span data-ttu-id="d044f-963">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d044f-963">Description</span></span> | <span data-ttu-id="d044f-964">Type</span><span class="sxs-lookup"><span data-stu-id="d044f-964">Type</span></span> | <span data-ttu-id="d044f-965">Geldige waarde</span><span class="sxs-lookup"><span data-stu-id="d044f-965">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d044f-966">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="d044f-966">NumberOfModelIterations</span></span> |<span data-ttu-id="d044f-967">het aantal iteraties Hallo model functioneert Hallo komt tot uiting in Hallo algemene compute tijd en Hallo nauwkeurigheid van het model.</span><span class="sxs-lookup"><span data-stu-id="d044f-967">hello number of iterations hello model performs is reflected by hello overall compute time and hello model accuracy.</span></span> <span data-ttu-id="d044f-968">Hallo hoger Hallo nummer, Hallo betere nauwkeurigheid u krijgt, maar Hallo compute tijd zal langer duren.</span><span class="sxs-lookup"><span data-stu-id="d044f-968">hello higher hello number, hello better accuracy you will get, but hello compute time will take longer.</span></span> |<span data-ttu-id="d044f-969">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="d044f-969">Integer</span></span> |<span data-ttu-id="d044f-970">10-50</span><span class="sxs-lookup"><span data-stu-id="d044f-970">10-50</span></span> |
| <span data-ttu-id="d044f-971">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="d044f-971">NumberOfModelDimensions</span></span> |<span data-ttu-id="d044f-972">het aantal dimensies Hallo is gekoppeld toohello aantal 'functies' hello model wordt geprobeerd toofind binnen uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="d044f-972">hello number of dimensions relates toohello number of 'features' hello model will try toofind within your data.</span></span> <span data-ttu-id="d044f-973">Vergroot het aantal dimensies Hallo kunt beter aan te passen van Hallo resultaten in kleinere clusters.</span><span class="sxs-lookup"><span data-stu-id="d044f-973">Increasing hello number of dimensions will allow better fine-tuning of hello results into smaller clusters.</span></span> <span data-ttu-id="d044f-974">Te veel dimensies kunnen echter Hallo model niet vinden van correlatie tussen items.</span><span class="sxs-lookup"><span data-stu-id="d044f-974">However, too many dimensions will prevent hello model from finding correlations between items.</span></span> |<span data-ttu-id="d044f-975">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="d044f-975">Integer</span></span> |<span data-ttu-id="d044f-976">10-40</span><span class="sxs-lookup"><span data-stu-id="d044f-976">10-40</span></span> |
| <span data-ttu-id="d044f-977">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="d044f-977">ItemCutOffLowerBound</span></span> |<span data-ttu-id="d044f-978">Hallo item ondergrens voor Hallo koeler definieert.</span><span class="sxs-lookup"><span data-stu-id="d044f-978">Defines hello item lower bound for hello condenser.</span></span> <span data-ttu-id="d044f-979">Zie gebruik koeler hierboven.</span><span class="sxs-lookup"><span data-stu-id="d044f-979">See usage condenser above.</span></span> |<span data-ttu-id="d044f-980">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="d044f-980">Integer</span></span> |<span data-ttu-id="d044f-981">2 of hoger (koeler 0 uitschakelen)</span><span class="sxs-lookup"><span data-stu-id="d044f-981">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="d044f-982">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="d044f-982">ItemCutOffUpperBound</span></span> |<span data-ttu-id="d044f-983">Hallo item bovengrens voor Hallo koeler definieert.</span><span class="sxs-lookup"><span data-stu-id="d044f-983">Defines hello item upper bound for hello condenser.</span></span> <span data-ttu-id="d044f-984">Zie gebruik koeler hierboven.</span><span class="sxs-lookup"><span data-stu-id="d044f-984">See usage condenser above.</span></span> |<span data-ttu-id="d044f-985">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="d044f-985">Integer</span></span> |<span data-ttu-id="d044f-986">2 of hoger (koeler 0 uitschakelen)</span><span class="sxs-lookup"><span data-stu-id="d044f-986">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="d044f-987">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="d044f-987">UserCutOffLowerBound</span></span> |<span data-ttu-id="d044f-988">Hallo gebruiker ondergrens voor Hallo koeler definieert.</span><span class="sxs-lookup"><span data-stu-id="d044f-988">Defines hello user lower bound for hello condenser.</span></span> <span data-ttu-id="d044f-989">Zie gebruik koeler hierboven.</span><span class="sxs-lookup"><span data-stu-id="d044f-989">See usage condenser above.</span></span> |<span data-ttu-id="d044f-990">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="d044f-990">Integer</span></span> |<span data-ttu-id="d044f-991">2 of hoger (koeler 0 uitschakelen)</span><span class="sxs-lookup"><span data-stu-id="d044f-991">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="d044f-992">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="d044f-992">UserCutOffUpperBound</span></span> |<span data-ttu-id="d044f-993">Hallo gebruiker bovengrens voor Hallo koeler definieert.</span><span class="sxs-lookup"><span data-stu-id="d044f-993">Defines hello user upper bound for hello condenser.</span></span> <span data-ttu-id="d044f-994">Zie gebruik koeler hierboven.</span><span class="sxs-lookup"><span data-stu-id="d044f-994">See usage condenser above.</span></span> |<span data-ttu-id="d044f-995">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="d044f-995">Integer</span></span> |<span data-ttu-id="d044f-996">2 of hoger (koeler 0 uitschakelen)</span><span class="sxs-lookup"><span data-stu-id="d044f-996">2 or more (0 disable condenser)</span></span> |

##### <a name="1113-recommendation-build-parameters"></a><span data-ttu-id="d044f-997">11.1.3.</span><span class="sxs-lookup"><span data-stu-id="d044f-997">11.1.3.</span></span> <span data-ttu-id="d044f-998">Aanbeveling build parameters</span><span class="sxs-lookup"><span data-stu-id="d044f-998">Recommendation build parameters</span></span>
<span data-ttu-id="d044f-999">Hallo in de volgende tabel beschrijft Hallo build parameters voor de aanbeveling build.</span><span class="sxs-lookup"><span data-stu-id="d044f-999">hello table below depicts hello build parameters for recommendation build.</span></span>

| <span data-ttu-id="d044f-1000">Sleutel</span><span class="sxs-lookup"><span data-stu-id="d044f-1000">Key</span></span> | <span data-ttu-id="d044f-1001">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d044f-1001">Description</span></span> | <span data-ttu-id="d044f-1002">Type</span><span class="sxs-lookup"><span data-stu-id="d044f-1002">Type</span></span> | <span data-ttu-id="d044f-1003">Geldige waarde</span><span class="sxs-lookup"><span data-stu-id="d044f-1003">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d044f-1004">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="d044f-1004">NumberOfModelIterations</span></span> |<span data-ttu-id="d044f-1005">het aantal iteraties Hallo model functioneert Hallo komt tot uiting in Hallo algemene compute tijd en Hallo nauwkeurigheid van het model.</span><span class="sxs-lookup"><span data-stu-id="d044f-1005">hello number of iterations hello model performs is reflected by hello overall compute time and hello model accuracy.</span></span> <span data-ttu-id="d044f-1006">Hallo hoger Hallo nummer, Hallo betere nauwkeurigheid u krijgt, maar Hallo compute tijd zal langer duren.</span><span class="sxs-lookup"><span data-stu-id="d044f-1006">hello higher hello number, hello better accuracy you will get, but hello compute time will take longer.</span></span> |<span data-ttu-id="d044f-1007">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="d044f-1007">Integer</span></span> |<span data-ttu-id="d044f-1008">10-50</span><span class="sxs-lookup"><span data-stu-id="d044f-1008">10-50</span></span> |
| <span data-ttu-id="d044f-1009">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="d044f-1009">NumberOfModelDimensions</span></span> |<span data-ttu-id="d044f-1010">het aantal dimensies Hallo is gekoppeld toohello aantal 'functies' hello model wordt geprobeerd toofind binnen uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="d044f-1010">hello number of dimensions relates toohello number of 'features' hello model will try toofind within your data.</span></span> <span data-ttu-id="d044f-1011">Vergroot het aantal dimensies Hallo kunt beter aan te passen van Hallo resultaten in kleinere clusters.</span><span class="sxs-lookup"><span data-stu-id="d044f-1011">Increasing hello number of dimensions will allow better fine-tuning of hello results into smaller clusters.</span></span> <span data-ttu-id="d044f-1012">Te veel dimensies kunnen echter Hallo model niet vinden van correlatie tussen items.</span><span class="sxs-lookup"><span data-stu-id="d044f-1012">However, too many dimensions will prevent hello model from finding correlations between items.</span></span> |<span data-ttu-id="d044f-1013">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="d044f-1013">Integer</span></span> |<span data-ttu-id="d044f-1014">10-40</span><span class="sxs-lookup"><span data-stu-id="d044f-1014">10-40</span></span> |
| <span data-ttu-id="d044f-1015">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="d044f-1015">ItemCutOffLowerBound</span></span> |<span data-ttu-id="d044f-1016">Hallo item ondergrens voor Hallo koeler definieert.</span><span class="sxs-lookup"><span data-stu-id="d044f-1016">Defines hello item lower bound for hello condenser.</span></span> <span data-ttu-id="d044f-1017">Zie gebruik koeler hierboven.</span><span class="sxs-lookup"><span data-stu-id="d044f-1017">See usage condenser above.</span></span> |<span data-ttu-id="d044f-1018">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="d044f-1018">Integer</span></span> |<span data-ttu-id="d044f-1019">2 of hoger (koeler 0 uitschakelen)</span><span class="sxs-lookup"><span data-stu-id="d044f-1019">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="d044f-1020">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="d044f-1020">ItemCutOffUpperBound</span></span> |<span data-ttu-id="d044f-1021">Hallo item bovengrens voor Hallo koeler definieert.</span><span class="sxs-lookup"><span data-stu-id="d044f-1021">Defines hello item upper bound for hello condenser.</span></span> <span data-ttu-id="d044f-1022">Zie gebruik koeler hierboven.</span><span class="sxs-lookup"><span data-stu-id="d044f-1022">See usage condenser above.</span></span> |<span data-ttu-id="d044f-1023">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="d044f-1023">Integer</span></span> |<span data-ttu-id="d044f-1024">2 of hoger (koeler 0 uitschakelen)</span><span class="sxs-lookup"><span data-stu-id="d044f-1024">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="d044f-1025">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="d044f-1025">UserCutOffLowerBound</span></span> |<span data-ttu-id="d044f-1026">Hallo gebruiker ondergrens voor Hallo koeler definieert.</span><span class="sxs-lookup"><span data-stu-id="d044f-1026">Defines hello user lower bound for hello condenser.</span></span> <span data-ttu-id="d044f-1027">Zie gebruik koeler hierboven.</span><span class="sxs-lookup"><span data-stu-id="d044f-1027">See usage condenser above.</span></span> |<span data-ttu-id="d044f-1028">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="d044f-1028">Integer</span></span> |<span data-ttu-id="d044f-1029">2 of hoger (koeler 0 uitschakelen)</span><span class="sxs-lookup"><span data-stu-id="d044f-1029">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="d044f-1030">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="d044f-1030">UserCutOffUpperBound</span></span> |<span data-ttu-id="d044f-1031">Hallo gebruiker bovengrens voor Hallo koeler definieert.</span><span class="sxs-lookup"><span data-stu-id="d044f-1031">Defines hello user upper bound for hello condenser.</span></span> <span data-ttu-id="d044f-1032">Zie gebruik koeler hierboven.</span><span class="sxs-lookup"><span data-stu-id="d044f-1032">See usage condenser above.</span></span> |<span data-ttu-id="d044f-1033">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="d044f-1033">Integer</span></span> |<span data-ttu-id="d044f-1034">2 of hoger (koeler 0 uitschakelen)</span><span class="sxs-lookup"><span data-stu-id="d044f-1034">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="d044f-1035">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d044f-1035">Description</span></span> |<span data-ttu-id="d044f-1036">Beschrijving bouwen.</span><span class="sxs-lookup"><span data-stu-id="d044f-1036">Build description.</span></span> |<span data-ttu-id="d044f-1037">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d044f-1037">String</span></span> |<span data-ttu-id="d044f-1038">Alle tekst maximaal 512 tekens</span><span class="sxs-lookup"><span data-stu-id="d044f-1038">Any text, maximum 512 chars</span></span> |
| <span data-ttu-id="d044f-1039">EnableModelingInsights</span><span class="sxs-lookup"><span data-stu-id="d044f-1039">EnableModelingInsights</span></span> |<span data-ttu-id="d044f-1040">Hiermee kunt u toocompute metrische gegevens op Hallo aanbeveling model.</span><span class="sxs-lookup"><span data-stu-id="d044f-1040">Allows you toocompute metrics on hello recommendation model.</span></span> |<span data-ttu-id="d044f-1041">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="d044f-1041">Boolean</span></span> |<span data-ttu-id="d044f-1042">Waar/onwaar</span><span class="sxs-lookup"><span data-stu-id="d044f-1042">True/False</span></span> |
| <span data-ttu-id="d044f-1043">UseFeaturesInModel</span><span class="sxs-lookup"><span data-stu-id="d044f-1043">UseFeaturesInModel</span></span> |<span data-ttu-id="d044f-1044">Hiermee wordt aangegeven als functies in volgorde tooenhance Hallo aanbeveling model kunnen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d044f-1044">Indicates if features can be used in order tooenhance hello recommendation model.</span></span> |<span data-ttu-id="d044f-1045">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="d044f-1045">Boolean</span></span> |<span data-ttu-id="d044f-1046">Waar/onwaar</span><span class="sxs-lookup"><span data-stu-id="d044f-1046">True/False</span></span> |
| <span data-ttu-id="d044f-1047">ModelingFeatureList</span><span class="sxs-lookup"><span data-stu-id="d044f-1047">ModelingFeatureList</span></span> |<span data-ttu-id="d044f-1048">Door komma's gescheiden lijst van de functie namen toobe Hallo aanbeveling gebouwd in volgorde tooenhance Hallo aanbeveling gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d044f-1048">Comma-separated list of feature names toobe used in hello recommendation build, in order tooenhance hello recommendation.</span></span> |<span data-ttu-id="d044f-1049">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d044f-1049">String</span></span> |<span data-ttu-id="d044f-1050">Onderdeelnamen up too512 tekens</span><span class="sxs-lookup"><span data-stu-id="d044f-1050">Feature names, up too512 chars</span></span> |
| <span data-ttu-id="d044f-1051">AllowColdItemPlacement</span><span class="sxs-lookup"><span data-stu-id="d044f-1051">AllowColdItemPlacement</span></span> |<span data-ttu-id="d044f-1052">Hiermee wordt aangegeven als Hallo aanbeveling ook koude items via de functie overeenkomsten pushen moet.</span><span class="sxs-lookup"><span data-stu-id="d044f-1052">Indicates if hello recommendation should also push cold items via feature similarity.</span></span> |<span data-ttu-id="d044f-1053">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="d044f-1053">Boolean</span></span> |<span data-ttu-id="d044f-1054">Waar/onwaar</span><span class="sxs-lookup"><span data-stu-id="d044f-1054">True/False</span></span> |
| <span data-ttu-id="d044f-1055">EnableFeatureCorrelation</span><span class="sxs-lookup"><span data-stu-id="d044f-1055">EnableFeatureCorrelation</span></span> |<span data-ttu-id="d044f-1056">Hiermee wordt aangegeven als functies kunnen worden gebruikt in de redenering.</span><span class="sxs-lookup"><span data-stu-id="d044f-1056">Indicates if features can be used in reasoning.</span></span> |<span data-ttu-id="d044f-1057">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="d044f-1057">Boolean</span></span> |<span data-ttu-id="d044f-1058">Waar/onwaar</span><span class="sxs-lookup"><span data-stu-id="d044f-1058">True/False</span></span> |
| <span data-ttu-id="d044f-1059">ReasoningFeatureList</span><span class="sxs-lookup"><span data-stu-id="d044f-1059">ReasoningFeatureList</span></span> |<span data-ttu-id="d044f-1060">Door komma's gescheiden lijst van de functie namen toobe gebruikt voor redeneren zinnen (bijvoorbeeld aanbeveling uitleg).</span><span class="sxs-lookup"><span data-stu-id="d044f-1060">Comma-separated list of feature names toobe used for reasoning sentences (e.g. recommendation explanations).</span></span> |<span data-ttu-id="d044f-1061">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d044f-1061">String</span></span> |<span data-ttu-id="d044f-1062">Onderdeelnamen up too512 tekens</span><span class="sxs-lookup"><span data-stu-id="d044f-1062">Feature names, up too512 chars</span></span> |
| <span data-ttu-id="d044f-1063">EnableU2I</span><span class="sxs-lookup"><span data-stu-id="d044f-1063">EnableU2I</span></span> |<span data-ttu-id="d044f-1064">Hallo persoonlijke aanbeveling ook toestaan</span><span class="sxs-lookup"><span data-stu-id="d044f-1064">Allow hello personalized recommendation a.k.a.</span></span> <span data-ttu-id="d044f-1065">U2I (gebruiker tooitem recommendations).</span><span class="sxs-lookup"><span data-stu-id="d044f-1065">U2I (user tooitem recommendations).</span></span> |<span data-ttu-id="d044f-1066">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="d044f-1066">Boolean</span></span> |<span data-ttu-id="d044f-1067">True/False (standaard waar)</span><span class="sxs-lookup"><span data-stu-id="d044f-1067">True/False (default true)</span></span> |

##### <a name="1114-fbt-build-parameters"></a><span data-ttu-id="d044f-1068">11.1.4.</span><span class="sxs-lookup"><span data-stu-id="d044f-1068">11.1.4.</span></span> <span data-ttu-id="d044f-1069">FBT build parameters</span><span class="sxs-lookup"><span data-stu-id="d044f-1069">FBT build parameters</span></span>
<span data-ttu-id="d044f-1070">Hallo in de volgende tabel beschrijft Hallo build parameters voor de aanbeveling build.</span><span class="sxs-lookup"><span data-stu-id="d044f-1070">hello table below depicts hello build parameters for recommendation build.</span></span>

| <span data-ttu-id="d044f-1071">Sleutel</span><span class="sxs-lookup"><span data-stu-id="d044f-1071">Key</span></span> | <span data-ttu-id="d044f-1072">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d044f-1072">Description</span></span> | <span data-ttu-id="d044f-1073">Type</span><span class="sxs-lookup"><span data-stu-id="d044f-1073">Type</span></span> | <span data-ttu-id="d044f-1074">Geldige waarde (standaard)</span><span class="sxs-lookup"><span data-stu-id="d044f-1074">Valid Value (Default)</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d044f-1075">FbtSupportThreshold</span><span class="sxs-lookup"><span data-stu-id="d044f-1075">FbtSupportThreshold</span></span> |<span data-ttu-id="d044f-1076">Hoe conservatief Hallo model is.</span><span class="sxs-lookup"><span data-stu-id="d044f-1076">How conservative hello model is.</span></span> <span data-ttu-id="d044f-1077">Het aantal mede exemplaren van items toobe in aanmerking voor het model.</span><span class="sxs-lookup"><span data-stu-id="d044f-1077">Number of co-occurrences of items toobe considered for modeling.</span></span> |<span data-ttu-id="d044f-1078">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="d044f-1078">Integer</span></span> |<span data-ttu-id="d044f-1079">3-50 (6)</span><span class="sxs-lookup"><span data-stu-id="d044f-1079">3-50 (6)</span></span> |
| <span data-ttu-id="d044f-1080">FbtMaxItemSetSize</span><span class="sxs-lookup"><span data-stu-id="d044f-1080">FbtMaxItemSetSize</span></span> |<span data-ttu-id="d044f-1081">Grenzen Hallo aantal items in een set veelvuldig.</span><span class="sxs-lookup"><span data-stu-id="d044f-1081">Bounds hello number of items in a frequent set.</span></span> |<span data-ttu-id="d044f-1082">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="d044f-1082">Integer</span></span> |<span data-ttu-id="d044f-1083">2-3 (2)</span><span class="sxs-lookup"><span data-stu-id="d044f-1083">2-3 (2)</span></span> |
| <span data-ttu-id="d044f-1084">FbtMinimalScore</span><span class="sxs-lookup"><span data-stu-id="d044f-1084">FbtMinimalScore</span></span> |<span data-ttu-id="d044f-1085">Minimale score die een set veelvuldig moet in de volgorde toobe opgenomen in Hallo geretourneerd resulteert.</span><span class="sxs-lookup"><span data-stu-id="d044f-1085">Minimal score that a frequent set should have in order toobe included in hello returned results.</span></span> <span data-ttu-id="d044f-1086">Hallo hoger Hallo beter.</span><span class="sxs-lookup"><span data-stu-id="d044f-1086">hello higher hello better.</span></span> |<span data-ttu-id="d044f-1087">dubbele</span><span class="sxs-lookup"><span data-stu-id="d044f-1087">Double</span></span> |<span data-ttu-id="d044f-1088">0 en hoger (0)</span><span class="sxs-lookup"><span data-stu-id="d044f-1088">0 and above (0)</span></span> |
| <span data-ttu-id="d044f-1089">FbtSimilarityFunction</span><span class="sxs-lookup"><span data-stu-id="d044f-1089">FbtSimilarityFunction</span></span> |<span data-ttu-id="d044f-1090">Hallo gelijkenis functie toobe gebruikt door Hallo build definieert.</span><span class="sxs-lookup"><span data-stu-id="d044f-1090">Defines hello similarity function toobe used by hello build.</span></span> <span data-ttu-id="d044f-1091">Lift Hiermee worden verbeterd serendipity, mede exemplaar Hiermee worden verbeterd voorspelbaarheid en Jaccard is een nice compromis tussen twee Hallo.</span><span class="sxs-lookup"><span data-stu-id="d044f-1091">Lift favors serendipity, Co-occurrence favors predictability, and Jaccard is a nice compromise between hello two.</span></span> |<span data-ttu-id="d044f-1092">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d044f-1092">String</span></span> |<span data-ttu-id="d044f-1093">cooccurrence lift jaccard (lift)</span><span class="sxs-lookup"><span data-stu-id="d044f-1093">cooccurrence, lift, jaccard (lift)</span></span> |

### <a name="112-trigger-a-recommendation-build"></a><span data-ttu-id="d044f-1094">11.2.</span><span class="sxs-lookup"><span data-stu-id="d044f-1094">11.2.</span></span> <span data-ttu-id="d044f-1095">Een aanbeveling Build activeren</span><span class="sxs-lookup"><span data-stu-id="d044f-1095">Trigger a Recommendation Build</span></span>
  <span data-ttu-id="d044f-1096">Standaard wordt deze API een aanbeveling build van het model activeren.</span><span class="sxs-lookup"><span data-stu-id="d044f-1096">By default this API will trigger a recommendation model build.</span></span> <span data-ttu-id="d044f-1097">tootrigger positie bouwen (in volgorde tooscore functies), Hallo build API variant met build typeparameter moet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d044f-1097">tootrigger a rank build (in order tooscore  features), hello build API variant with build type parameter should be used.</span></span>

| <span data-ttu-id="d044f-1098">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-1098">HTTP Method</span></span> | <span data-ttu-id="d044f-1099">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-1099">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-1100">VERZENDEN</span><span class="sxs-lookup"><span data-stu-id="d044f-1100">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="d044f-1101">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d044f-1101">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |
| <span data-ttu-id="d044f-1102">KOPTEKST</span><span class="sxs-lookup"><span data-stu-id="d044f-1102">HEADER</span></span> |<span data-ttu-id="d044f-1103">`"Content-Type", "text/xml"`(Als aanvraagtekst verzenden)</span><span class="sxs-lookup"><span data-stu-id="d044f-1103">`"Content-Type", "text/xml"` (If sending Request Body)</span></span> |

| <span data-ttu-id="d044f-1104">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-1104">Parameter Name</span></span> | <span data-ttu-id="d044f-1105">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-1105">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-1106">Model</span><span class="sxs-lookup"><span data-stu-id="d044f-1106">modelId</span></span> |<span data-ttu-id="d044f-1107">De unieke id van het Hallo-model</span><span class="sxs-lookup"><span data-stu-id="d044f-1107">Unique identifier of hello model</span></span> |
| <span data-ttu-id="d044f-1108">userDescription</span><span class="sxs-lookup"><span data-stu-id="d044f-1108">userDescription</span></span> |<span data-ttu-id="d044f-1109">Tekstuele Hallo catalogus-ID.</span><span class="sxs-lookup"><span data-stu-id="d044f-1109">Textual identifier of hello catalog.</span></span> <span data-ttu-id="d044f-1110">Houd er rekening mee dat als u opslagruimten gebruikt u deze met % 20 in plaats daarvan coderen moet.</span><span class="sxs-lookup"><span data-stu-id="d044f-1110">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="d044f-1111">Zie het bovenstaande voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="d044f-1111">See example above.</span></span><br><span data-ttu-id="d044f-1112">Maximale lengte: 50</span><span class="sxs-lookup"><span data-stu-id="d044f-1112">Max length: 50</span></span> |
| <span data-ttu-id="d044f-1113">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-1113">apiVersion</span></span> |<span data-ttu-id="d044f-1114">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-1114">1.0</span></span> |
|  | |
| <span data-ttu-id="d044f-1115">Aanvraagtekst</span><span class="sxs-lookup"><span data-stu-id="d044f-1115">Request Body</span></span> |<span data-ttu-id="d044f-1116">Als dit veld leeg wordt met de standaardparameters voor build Hallo Hallo build uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d044f-1116">If left empty then hello build will be executed with hello default build parameters.</span></span><br><br><span data-ttu-id="d044f-1117">Als u tooset Hallo build-parameters wilt, Hallo parameters verzenden als XML in de hoofdtekst Hallo zoals in Hallo voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="d044f-1117">If you want tooset hello build parameters, send hello parameters as XML into hello body as in hello following sample.</span></span> <span data-ttu-id="d044f-1118">(Zie de sectie Hallo Build 'parameters' voor een uitleg van Hallo-parameters.)`<NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance><EnableModelingInsights>true</EnableModelingInsights><UseFeaturesInModel>false</UseFeaturesInModel><ModelingFeatureList>feature_name_1,feature_name_2,...</ModelingFeatureList><AllowColdItemPlacement>false</AllowColdItemPlacement><EnableFeatureCorrelation>false</EnableFeatureCorrelation><ReasoningFeatureList>feature_name_a,feature_name_b,...</ReasoningFeatureList></BuildParametersList>`</span><span class="sxs-lookup"><span data-stu-id="d044f-1118">(See hello "Build parameters" section for an explanation of hello parameters.)`<NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance><EnableModelingInsights>true</EnableModelingInsights><UseFeaturesInModel>false</UseFeaturesInModel><ModelingFeatureList>feature_name_1,feature_name_2,...</ModelingFeatureList><AllowColdItemPlacement>false</AllowColdItemPlacement><EnableFeatureCorrelation>false</EnableFeatureCorrelation><ReasoningFeatureList>feature_name_a,feature_name_b,...</ReasoningFeatureList></BuildParametersList>`</span></span> |

<span data-ttu-id="d044f-1119">**Antwoord**:</span><span class="sxs-lookup"><span data-stu-id="d044f-1119">**Response**:</span></span>

<span data-ttu-id="d044f-1120">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-1120">HTTP Status code: 200</span></span>

<span data-ttu-id="d044f-1121">Dit is een asynchrone API.</span><span class="sxs-lookup"><span data-stu-id="d044f-1121">This is an asynchronous API.</span></span> <span data-ttu-id="d044f-1122">U krijgt een build-ID als antwoord.</span><span class="sxs-lookup"><span data-stu-id="d044f-1122">You will get a build ID as a response.</span></span> <span data-ttu-id="d044f-1123">tooknow wanneer Hallo build is beëindigd, die u moet Hallo 'Ophalen Builds Status van een Model' API aanroepen en zoek deze ID in het antwoord Hallo bouwen.</span><span class="sxs-lookup"><span data-stu-id="d044f-1123">tooknow when hello build has ended, you should call hello “Get Builds Status of a Model” API and locate this build ID in hello response.</span></span> <span data-ttu-id="d044f-1124">Houd er rekening mee dat een build van toohours minuten, afhankelijk van de grootte Hallo Hallo gegevens kan opnemen.</span><span class="sxs-lookup"><span data-stu-id="d044f-1124">Note that a build can take from minutes toohours depending on hello size of hello data.</span></span>

<span data-ttu-id="d044f-1125">U kan geen aanbevelingen verbruiken tot Hallo bouwen eindigt.</span><span class="sxs-lookup"><span data-stu-id="d044f-1125">You cannot consume recommendations till hello build ends.</span></span>

<span data-ttu-id="d044f-1126">Geldige build-status:</span><span class="sxs-lookup"><span data-stu-id="d044f-1126">Valid build status:</span></span>

* <span data-ttu-id="d044f-1127">Maak - Build-aanvraag is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d044f-1127">Create - Build request was created.</span></span>
* <span data-ttu-id="d044f-1128">In de wachtrij - Build-aanvraag is verzonden en deze in de wachtrij staat.</span><span class="sxs-lookup"><span data-stu-id="d044f-1128">Queued - Build request was sent and it is queued.</span></span>
* <span data-ttu-id="d044f-1129">Gebouw - Build wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d044f-1129">Building - Build is in progress.</span></span>
* <span data-ttu-id="d044f-1130">Geslaagd - Build is beëindigd.</span><span class="sxs-lookup"><span data-stu-id="d044f-1130">Success - Build ended successfully.</span></span>
* <span data-ttu-id="d044f-1131">Fout - Build beëindigd met een fout.</span><span class="sxs-lookup"><span data-stu-id="d044f-1131">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="d044f-1132">Geannuleerd - is Build geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="d044f-1132">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="d044f-1133">Annuleren - een verzoek tot annuleren voor Hallo build is verzonden.</span><span class="sxs-lookup"><span data-stu-id="d044f-1133">Cancelling - A cancel request for hello build was sent.</span></span>

<span data-ttu-id="d044f-1134">Houd er rekening mee dat Hallo-build-ID vindt onder in het pad naar Hallo:`Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="d044f-1134">Note that hello build ID can be found under hello following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="d044f-1135">OData-XML</span><span class="sxs-lookup"><span data-stu-id="d044f-1135">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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

### <a name="113-trigger-build-recommendation-rank-or-fbt"></a><span data-ttu-id="d044f-1136">11.3.</span><span class="sxs-lookup"><span data-stu-id="d044f-1136">11.3.</span></span> <span data-ttu-id="d044f-1137">Trigger Build (aanbeveling, positie of FBT)</span><span class="sxs-lookup"><span data-stu-id="d044f-1137">Trigger Build (Recommendation, Rank or FBT)</span></span>
| <span data-ttu-id="d044f-1138">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-1138">HTTP Method</span></span> | <span data-ttu-id="d044f-1139">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-1139">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-1140">VERZENDEN</span><span class="sxs-lookup"><span data-stu-id="d044f-1140">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&buildType=%27<buildType>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="d044f-1141">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d044f-1141">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&buildType=%27Ranking%27&apiVersion=%271.0%27` |
| <span data-ttu-id="d044f-1142">KOPTEKST</span><span class="sxs-lookup"><span data-stu-id="d044f-1142">HEADER</span></span> |<span data-ttu-id="d044f-1143">`"Content-Type", "text/xml"`(Als aanvraagtekst verzenden)</span><span class="sxs-lookup"><span data-stu-id="d044f-1143">`"Content-Type", "text/xml"` (If sending Request Body)</span></span> |

| <span data-ttu-id="d044f-1144">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-1144">Parameter Name</span></span> | <span data-ttu-id="d044f-1145">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-1145">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-1146">Model</span><span class="sxs-lookup"><span data-stu-id="d044f-1146">modelId</span></span> |<span data-ttu-id="d044f-1147">De unieke id van het Hallo-model</span><span class="sxs-lookup"><span data-stu-id="d044f-1147">Unique identifier of hello model</span></span> |
| <span data-ttu-id="d044f-1148">userDescription</span><span class="sxs-lookup"><span data-stu-id="d044f-1148">userDescription</span></span> |<span data-ttu-id="d044f-1149">Tekstuele Hallo catalogus-ID.</span><span class="sxs-lookup"><span data-stu-id="d044f-1149">Textual identifier of hello catalog.</span></span> <span data-ttu-id="d044f-1150">Houd er rekening mee dat als u opslagruimten gebruikt u deze met % 20 in plaats daarvan coderen moet.</span><span class="sxs-lookup"><span data-stu-id="d044f-1150">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="d044f-1151">Zie het bovenstaande voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="d044f-1151">See example above.</span></span><br><span data-ttu-id="d044f-1152">Maximale lengte: 50</span><span class="sxs-lookup"><span data-stu-id="d044f-1152">Max length: 50</span></span> |
| <span data-ttu-id="d044f-1153">buildType</span><span class="sxs-lookup"><span data-stu-id="d044f-1153">buildType</span></span> |<span data-ttu-id="d044f-1154">Type Hallo build tooinvoke:</span><span class="sxs-lookup"><span data-stu-id="d044f-1154">Type of hello build tooinvoke:</span></span> <br/> <span data-ttu-id="d044f-1155">-Aanbeveling als u uw voor aanbeveling build</span><span class="sxs-lookup"><span data-stu-id="d044f-1155">- 'Recommendation' for recommendation build</span></span> <br> <span data-ttu-id="d044f-1156">-Volgorde voor waarden van positie build</span><span class="sxs-lookup"><span data-stu-id="d044f-1156">- 'Ranking' for rank build</span></span> <br/> <span data-ttu-id="d044f-1157">-'Fbt' voor FBT build</span><span class="sxs-lookup"><span data-stu-id="d044f-1157">- 'Fbt' for FBT build</span></span> |
| <span data-ttu-id="d044f-1158">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-1158">apiVersion</span></span> |<span data-ttu-id="d044f-1159">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-1159">1.0</span></span> |
|  | |
| <span data-ttu-id="d044f-1160">Aanvraagtekst</span><span class="sxs-lookup"><span data-stu-id="d044f-1160">Request Body</span></span> |<span data-ttu-id="d044f-1161">Als dit veld leeg wordt met de standaardparameters voor build Hallo Hallo build uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d044f-1161">If left empty then hello build will be executed with hello default build parameters.</span></span><br><br><span data-ttu-id="d044f-1162">Als u tooset build-parameters wilt, stuurt u ze als XML in de hoofdtekst Hallo zoals in Hallo voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="d044f-1162">If you want tooset build parameters, send them as XML into hello body like in hello following sample.</span></span> <span data-ttu-id="d044f-1163">(Zie de sectie Hallo Build 'parameters' voor een uitleg en een volledige lijst met parameters Hallo.)`<BuildParametersList><NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance></BuildParametersList>`</span><span class="sxs-lookup"><span data-stu-id="d044f-1163">(See hello "Build parameters" section for an explanation and full list of hello parameters.)`<BuildParametersList><NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance></BuildParametersList>`</span></span> |

<span data-ttu-id="d044f-1164">**Antwoord**:</span><span class="sxs-lookup"><span data-stu-id="d044f-1164">**Response**:</span></span>

<span data-ttu-id="d044f-1165">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-1165">HTTP Status code: 200</span></span>

<span data-ttu-id="d044f-1166">Dit is een asynchrone API.</span><span class="sxs-lookup"><span data-stu-id="d044f-1166">This is an asynchronous API.</span></span> <span data-ttu-id="d044f-1167">U krijgt een build-ID als antwoord.</span><span class="sxs-lookup"><span data-stu-id="d044f-1167">You will get a build ID as a response.</span></span> <span data-ttu-id="d044f-1168">tooknow wanneer Hallo build is beëindigd, die u moet Hallo 'Ophalen Builds Status van een Model' API aanroepen en zoek deze ID in het antwoord Hallo bouwen.</span><span class="sxs-lookup"><span data-stu-id="d044f-1168">tooknow when hello build has ended, you should call hello “Get Builds Status of a Model” API and locate this build ID in hello response.</span></span> <span data-ttu-id="d044f-1169">Houd er rekening mee dat een build van toohours minuten, afhankelijk van de grootte Hallo Hallo gegevens kan opnemen.</span><span class="sxs-lookup"><span data-stu-id="d044f-1169">Note that a build can take from minutes toohours depending on hello size of hello data.</span></span>

<span data-ttu-id="d044f-1170">U kan geen aanbevelingen verbruiken tot Hallo bouwen eindigt.</span><span class="sxs-lookup"><span data-stu-id="d044f-1170">You cannot consume recommendations till hello build ends.</span></span>

<span data-ttu-id="d044f-1171">Geldige build-status:</span><span class="sxs-lookup"><span data-stu-id="d044f-1171">Valid build status:</span></span>

* <span data-ttu-id="d044f-1172">Maak - Model is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d044f-1172">Create - Model was created.</span></span>
* <span data-ttu-id="d044f-1173">In de wachtrij - Model build is geactiveerd en deze in de wachtrij staat.</span><span class="sxs-lookup"><span data-stu-id="d044f-1173">Queued - Model build was triggered and it is queued.</span></span>
* <span data-ttu-id="d044f-1174">Gebouw - Model wordt samengesteld.</span><span class="sxs-lookup"><span data-stu-id="d044f-1174">Building - Model is being built.</span></span>
* <span data-ttu-id="d044f-1175">Geslaagd - Build is beëindigd.</span><span class="sxs-lookup"><span data-stu-id="d044f-1175">Success - Build ended successfully.</span></span>
* <span data-ttu-id="d044f-1176">Fout - Build beëindigd met een fout.</span><span class="sxs-lookup"><span data-stu-id="d044f-1176">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="d044f-1177">Geannuleerd - is Build geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="d044f-1177">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="d044f-1178">Annuleert - Build wordt geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="d044f-1178">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="d044f-1179">Houd er rekening mee dat Hallo-build-ID vindt onder in het pad naar Hallo:`Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="d044f-1179">Note that hello build ID can be found under hello following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="d044f-1180">OData-XML</span><span class="sxs-lookup"><span data-stu-id="d044f-1180">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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




### <a name="114-get-builds-status-of-a-model"></a><span data-ttu-id="d044f-1181">11.4.</span><span class="sxs-lookup"><span data-stu-id="d044f-1181">11.4.</span></span> <span data-ttu-id="d044f-1182">Builds van Status van een Model ophalen</span><span class="sxs-lookup"><span data-stu-id="d044f-1182">Get Builds Status of a Model</span></span>
<span data-ttu-id="d044f-1183">Haalt builds en hun status voor een opgegeven model.</span><span class="sxs-lookup"><span data-stu-id="d044f-1183">Retrieves builds and their status for a specified model.</span></span>

| <span data-ttu-id="d044f-1184">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-1184">HTTP Method</span></span> | <span data-ttu-id="d044f-1185">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-1185">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-1186">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="d044f-1186">GET</span></span> |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="d044f-1187">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d044f-1187">Example:</span></span><br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| <span data-ttu-id="d044f-1188">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-1188">Parameter Name</span></span> | <span data-ttu-id="d044f-1189">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-1189">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-1190">Model</span><span class="sxs-lookup"><span data-stu-id="d044f-1190">modelId</span></span> |<span data-ttu-id="d044f-1191">De unieke id van het Hallo-model</span><span class="sxs-lookup"><span data-stu-id="d044f-1191">Unique identifier of hello model</span></span> |
| <span data-ttu-id="d044f-1192">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="d044f-1192">onlyLastBuild</span></span> |<span data-ttu-id="d044f-1193">Hiermee wordt aangegeven of tooreturn alle Hallo geschiedenis van Hallo model of de status alleen Hallo van de meest recente build Hallo bouwen</span><span class="sxs-lookup"><span data-stu-id="d044f-1193">Indicates whether tooreturn all hello build history of hello model or only hello status of hello most recent build</span></span> |
| <span data-ttu-id="d044f-1194">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-1194">apiVersion</span></span> |<span data-ttu-id="d044f-1195">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-1195">1.0</span></span> |

<span data-ttu-id="d044f-1196">**Antwoord**:</span><span class="sxs-lookup"><span data-stu-id="d044f-1196">**Response**:</span></span>

<span data-ttu-id="d044f-1197">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-1197">HTTP Status code: 200</span></span>

<span data-ttu-id="d044f-1198">Hallo-antwoord bevat één vermelding per build.</span><span class="sxs-lookup"><span data-stu-id="d044f-1198">hello response includes one entry per build.</span></span> <span data-ttu-id="d044f-1199">Elk item heeft Hallo gegevens te volgen:</span><span class="sxs-lookup"><span data-stu-id="d044f-1199">Each entry has hello following data:</span></span>

* <span data-ttu-id="d044f-1200">`feed/entry/content/properties/UserName`-Naam van de gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="d044f-1200">`feed/entry/content/properties/UserName` - Name of hello user.</span></span>
* <span data-ttu-id="d044f-1201">`feed/entry/content/properties/ModelName`-De naam van het Hallo-model.</span><span class="sxs-lookup"><span data-stu-id="d044f-1201">`feed/entry/content/properties/ModelName` - Name of hello model.</span></span>
* <span data-ttu-id="d044f-1202">`feed/entry/content/properties/ModelId`-De unieke id model.</span><span class="sxs-lookup"><span data-stu-id="d044f-1202">`feed/entry/content/properties/ModelId` - Model unique identifier.</span></span>
* <span data-ttu-id="d044f-1203">`feed/entry/content/properties/IsDeployed`-Of Hallo build (ook wordt geïmplementeerd</span><span class="sxs-lookup"><span data-stu-id="d044f-1203">`feed/entry/content/properties/IsDeployed` - Whether hello build is deployed (a.k.a.</span></span> <span data-ttu-id="d044f-1204">actieve build).</span><span class="sxs-lookup"><span data-stu-id="d044f-1204">active build).</span></span>
* <span data-ttu-id="d044f-1205">`feed/entry/content/properties/BuildId`-De unieke id maken.</span><span class="sxs-lookup"><span data-stu-id="d044f-1205">`feed/entry/content/properties/BuildId` - Build unique identifier.</span></span>
* <span data-ttu-id="d044f-1206">`feed/entry/content/properties/BuildType`-Type van Hallo build.</span><span class="sxs-lookup"><span data-stu-id="d044f-1206">`feed/entry/content/properties/BuildType` - Type of hello build.</span></span>
* <span data-ttu-id="d044f-1207">`feed/entry/content/properties/Status`-Status maken.</span><span class="sxs-lookup"><span data-stu-id="d044f-1207">`feed/entry/content/properties/Status` - Build status.</span></span> <span data-ttu-id="d044f-1208">Een van de volgende Hallo: fout, gebouwen, in de wachtrij geplaatst, Cancelling, geannuleerd, geslaagd.</span><span class="sxs-lookup"><span data-stu-id="d044f-1208">Can be one of hello following: Error, Building, Queued, Cancelling, Cancelled, Success.</span></span>
* <span data-ttu-id="d044f-1209">`feed/entry/content/properties/StatusMessage`-Het gedetailleerde statusbericht (geldt alleen toospecific statussen).</span><span class="sxs-lookup"><span data-stu-id="d044f-1209">`feed/entry/content/properties/StatusMessage` - Detailed status message (applies only toospecific states).</span></span>
* <span data-ttu-id="d044f-1210">`feed/entry/content/properties/Progress`-Bouwen voortgang (%).</span><span class="sxs-lookup"><span data-stu-id="d044f-1210">`feed/entry/content/properties/Progress` - Build progress (%).</span></span>
* <span data-ttu-id="d044f-1211">`feed/entry/content/properties/StartTime`-Begintijd build.</span><span class="sxs-lookup"><span data-stu-id="d044f-1211">`feed/entry/content/properties/StartTime` - Build start time.</span></span>
* <span data-ttu-id="d044f-1212">`feed/entry/content/properties/EndTime`-Eindtijd bouwen.</span><span class="sxs-lookup"><span data-stu-id="d044f-1212">`feed/entry/content/properties/EndTime` - Build end time.</span></span>
* <span data-ttu-id="d044f-1213">`feed/entry/content/properties/ExecutionTime`-Duur maken.</span><span class="sxs-lookup"><span data-stu-id="d044f-1213">`feed/entry/content/properties/ExecutionTime` - Build duration.</span></span>
* <span data-ttu-id="d044f-1214">`feed/entry/content/properties/ProgressStep`-Gegevens over Hallo huidige fase van een build uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d044f-1214">`feed/entry/content/properties/ProgressStep` - Details about hello current stage of a build in progress.</span></span>

<span data-ttu-id="d044f-1215">Geldige build-status:</span><span class="sxs-lookup"><span data-stu-id="d044f-1215">Valid build status:</span></span>

* <span data-ttu-id="d044f-1216">Gemaakt - is vermelding van Build-aanvraag gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d044f-1216">Created - Build request entry was created.</span></span>
* <span data-ttu-id="d044f-1217">In de wachtrij - aanvraag voor het samenstellen is geactiveerd en deze in de wachtrij staat.</span><span class="sxs-lookup"><span data-stu-id="d044f-1217">Queued - Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="d044f-1218">Gebouw - Build is bezig.</span><span class="sxs-lookup"><span data-stu-id="d044f-1218">Building - Build is in process.</span></span>
* <span data-ttu-id="d044f-1219">Geslaagd - Build is beëindigd.</span><span class="sxs-lookup"><span data-stu-id="d044f-1219">Success - Build ended successfully.</span></span>
* <span data-ttu-id="d044f-1220">Fout - Build beëindigd met een fout.</span><span class="sxs-lookup"><span data-stu-id="d044f-1220">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="d044f-1221">Geannuleerd - is Build geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="d044f-1221">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="d044f-1222">Annuleert - Build wordt geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="d044f-1222">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="d044f-1223">Geldige waarden voor de BuildType:</span><span class="sxs-lookup"><span data-stu-id="d044f-1223">Valid values for build type:</span></span>

* <span data-ttu-id="d044f-1224">Positie - positie bouwen.</span><span class="sxs-lookup"><span data-stu-id="d044f-1224">Rank - Rank build.</span></span>
* <span data-ttu-id="d044f-1225">Aanbeveling - aanbeveling build.</span><span class="sxs-lookup"><span data-stu-id="d044f-1225">Recommendation - Recommendation build.</span></span>

<span data-ttu-id="d044f-1226">OData-XML</span><span class="sxs-lookup"><span data-stu-id="d044f-1226">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get builds status of a model</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-05T17:51:10Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildsStatusEntity</title>
            <updated>2014-11-05T17:51:10Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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


### <a name="115-get-builds-status"></a><span data-ttu-id="d044f-1227">11.5.</span><span class="sxs-lookup"><span data-stu-id="d044f-1227">11.5.</span></span> <span data-ttu-id="d044f-1228">Builds Status ophalen</span><span class="sxs-lookup"><span data-stu-id="d044f-1228">Get Builds Status</span></span>
<span data-ttu-id="d044f-1229">Haalt maken status van alle modellen van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="d044f-1229">Retrieves build statuses of all models of a user.</span></span>

| <span data-ttu-id="d044f-1230">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-1230">HTTP Method</span></span> | <span data-ttu-id="d044f-1231">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-1231">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-1232">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="d044f-1232">GET</span></span> |`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="d044f-1233">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d044f-1233">Example:</span></span><br>`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=true&apiVersion=%271.0%27` |

| <span data-ttu-id="d044f-1234">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-1234">Parameter Name</span></span> | <span data-ttu-id="d044f-1235">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-1235">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-1236">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="d044f-1236">onlyLastBuild</span></span> |<span data-ttu-id="d044f-1237">Hiermee wordt aangegeven of tooreturn alle Hallo geschiedenis van Hallo model of de status alleen Hallo van de meest recente build Hallo bouwen.</span><span class="sxs-lookup"><span data-stu-id="d044f-1237">Indicates whether tooreturn all hello build history of hello model or only hello status of hello most recent build.</span></span> |
| <span data-ttu-id="d044f-1238">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-1238">apiVersion</span></span> |<span data-ttu-id="d044f-1239">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-1239">1.0</span></span> |

<span data-ttu-id="d044f-1240">**Antwoord**:</span><span class="sxs-lookup"><span data-stu-id="d044f-1240">**Response**:</span></span>

<span data-ttu-id="d044f-1241">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-1241">HTTP Status code: 200</span></span>

<span data-ttu-id="d044f-1242">Hallo-antwoord bevat één vermelding per build.</span><span class="sxs-lookup"><span data-stu-id="d044f-1242">hello response includes one entry per build.</span></span> <span data-ttu-id="d044f-1243">Elk item heeft Hallo gegevens te volgen:</span><span class="sxs-lookup"><span data-stu-id="d044f-1243">Each entry has hello following data:</span></span>

* <span data-ttu-id="d044f-1244">`feed/entry/content/properties/UserName`-Naam van de gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="d044f-1244">`feed/entry/content/properties/UserName` - Name of hello user.</span></span>
* <span data-ttu-id="d044f-1245">`feed/entry/content/properties/ModelName`-De naam van het Hallo-model.</span><span class="sxs-lookup"><span data-stu-id="d044f-1245">`feed/entry/content/properties/ModelName` - Name of hello model.</span></span>
* <span data-ttu-id="d044f-1246">`feed/entry/content/properties/ModelId`-De unieke id model.</span><span class="sxs-lookup"><span data-stu-id="d044f-1246">`feed/entry/content/properties/ModelId` - Model unique identifier.</span></span>
* <span data-ttu-id="d044f-1247">`feed/entry/content/properties/IsDeployed`-Of Hallo build wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="d044f-1247">`feed/entry/content/properties/IsDeployed` - Whether hello build is deployed.</span></span>
* <span data-ttu-id="d044f-1248">`feed/entry/content/properties/BuildId`-De unieke id maken.</span><span class="sxs-lookup"><span data-stu-id="d044f-1248">`feed/entry/content/properties/BuildId` - Build unique identifier.</span></span>
* <span data-ttu-id="d044f-1249">`feed/entry/content/properties/BuildType`-Type van Hallo build.</span><span class="sxs-lookup"><span data-stu-id="d044f-1249">`feed/entry/content/properties/BuildType` - Type of hello build.</span></span>
* <span data-ttu-id="d044f-1250">`feed/entry/content/properties/Status`-Status maken.</span><span class="sxs-lookup"><span data-stu-id="d044f-1250">`feed/entry/content/properties/Status` - Build status.</span></span> <span data-ttu-id="d044f-1251">Een van de volgende Hallo: fout, gebouwen, in de wachtrij geplaatst, geannuleerd, Cancelling, geslaagd.</span><span class="sxs-lookup"><span data-stu-id="d044f-1251">Can be one of hello following: Error, Building, Queued, Cancelled, Cancelling, Success.</span></span>
* <span data-ttu-id="d044f-1252">`feed/entry/content/properties/StatusMessage`-Het gedetailleerde statusbericht (geldt alleen toospecific statussen).</span><span class="sxs-lookup"><span data-stu-id="d044f-1252">`feed/entry/content/properties/StatusMessage` - Detailed status message (applies only toospecific states).</span></span>
* <span data-ttu-id="d044f-1253">`feed/entry/content/properties/Progress`-Bouwen voortgang (%).</span><span class="sxs-lookup"><span data-stu-id="d044f-1253">`feed/entry/content/properties/Progress` - Build progress (%).</span></span>
* <span data-ttu-id="d044f-1254">`feed/entry/content/properties/StartTime`-Begintijd build.</span><span class="sxs-lookup"><span data-stu-id="d044f-1254">`feed/entry/content/properties/StartTime` - Build start time.</span></span>
* <span data-ttu-id="d044f-1255">`feed/entry/content/properties/EndTime`-Eindtijd bouwen.</span><span class="sxs-lookup"><span data-stu-id="d044f-1255">`feed/entry/content/properties/EndTime` - Build end time.</span></span>
* <span data-ttu-id="d044f-1256">`feed/entry/content/properties/ExecutionTime`-Duur maken.</span><span class="sxs-lookup"><span data-stu-id="d044f-1256">`feed/entry/content/properties/ExecutionTime` - Build duration.</span></span>
* <span data-ttu-id="d044f-1257">`feed/entry/content/properties/ProgressStep`-Gegevens over Hallo huidige fase van een build uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d044f-1257">`feed/entry/content/properties/ProgressStep` - Details about hello current stage of a build in progress.</span></span>

<span data-ttu-id="d044f-1258">Geldige build-status:</span><span class="sxs-lookup"><span data-stu-id="d044f-1258">Valid build status:</span></span>

* <span data-ttu-id="d044f-1259">Gemaakt - is vermelding van Build-aanvraag gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d044f-1259">Created - Build request entry was created.</span></span>
* <span data-ttu-id="d044f-1260">In de wachtrij - aanvraag voor het samenstellen is geactiveerd en deze in de wachtrij staat.</span><span class="sxs-lookup"><span data-stu-id="d044f-1260">Queued - Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="d044f-1261">Gebouw - Build is bezig.</span><span class="sxs-lookup"><span data-stu-id="d044f-1261">Building - Build is in process.</span></span>
* <span data-ttu-id="d044f-1262">Geslaagd - Build is beëindigd.</span><span class="sxs-lookup"><span data-stu-id="d044f-1262">Success - Build ended successfully.</span></span>
* <span data-ttu-id="d044f-1263">Fout - Build beëindigd met een fout.</span><span class="sxs-lookup"><span data-stu-id="d044f-1263">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="d044f-1264">Geannuleerd - is Build geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="d044f-1264">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="d044f-1265">Annuleert - Build wordt geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="d044f-1265">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="d044f-1266">Geldige waarden voor de BuildType:</span><span class="sxs-lookup"><span data-stu-id="d044f-1266">Valid values for build type:</span></span>

* <span data-ttu-id="d044f-1267">Positie - positie bouwen.</span><span class="sxs-lookup"><span data-stu-id="d044f-1267">Rank - Rank build.</span></span>
* <span data-ttu-id="d044f-1268">Aanbeveling - aanbeveling build.</span><span class="sxs-lookup"><span data-stu-id="d044f-1268">Recommendation - Recommendation build.</span></span>

<span data-ttu-id="d044f-1269">OData-XML</span><span class="sxs-lookup"><span data-stu-id="d044f-1269">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get builds status of a user</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-05T18:41:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildsStatusEntity</title>
            <updated>2014-11-05T18:41:21Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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


### <a name="116-delete-build"></a><span data-ttu-id="d044f-1270">11.6.</span><span class="sxs-lookup"><span data-stu-id="d044f-1270">11.6.</span></span> <span data-ttu-id="d044f-1271">Versie verwijderen</span><span class="sxs-lookup"><span data-stu-id="d044f-1271">Delete Build</span></span>
<span data-ttu-id="d044f-1272">Hiermee verwijdert u een build.</span><span class="sxs-lookup"><span data-stu-id="d044f-1272">Deletes a build.</span></span>

<span data-ttu-id="d044f-1273">OPMERKING:</span><span class="sxs-lookup"><span data-stu-id="d044f-1273">NOTE:</span></span> <br><span data-ttu-id="d044f-1274">U kunt een actieve build niet verwijderen.</span><span class="sxs-lookup"><span data-stu-id="d044f-1274">You cannot delete an active build.</span></span> <span data-ttu-id="d044f-1275">Hallo model moet worden bijgewerkt tooa andere actieve build voordat u deze verwijdert.</span><span class="sxs-lookup"><span data-stu-id="d044f-1275">hello model should be updated tooa different active build before you delete it.</span></span><br><span data-ttu-id="d044f-1276">U kunt een build wordt uitgevoerd niet verwijderen.</span><span class="sxs-lookup"><span data-stu-id="d044f-1276">You cannot delete an in-progress build.</span></span> <span data-ttu-id="d044f-1277">Moet u eerst Hallo build annuleren door het aanroepen van <strong>annuleren bouwen</strong>.</span><span class="sxs-lookup"><span data-stu-id="d044f-1277">You should cancel hello build first by calling <strong>Cancel Build</strong>.</span></span>

| <span data-ttu-id="d044f-1278">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-1278">HTTP Method</span></span> | <span data-ttu-id="d044f-1279">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-1279">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-1280">VERWIJDEREN</span><span class="sxs-lookup"><span data-stu-id="d044f-1280">DELETE</span></span> |`<rootURI>/DeleteBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="d044f-1281">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d044f-1281">Example:</span></span><br>`<rootURI>/DeleteBuild?buildId=%271500068%27&apiVersion=%271.0%27` |

| <span data-ttu-id="d044f-1282">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-1282">Parameter Name</span></span> | <span data-ttu-id="d044f-1283">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-1283">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-1284">buildId</span><span class="sxs-lookup"><span data-stu-id="d044f-1284">buildId</span></span> |<span data-ttu-id="d044f-1285">De unieke id van Hallo build.</span><span class="sxs-lookup"><span data-stu-id="d044f-1285">Unique identifier of hello build.</span></span> |
| <span data-ttu-id="d044f-1286">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-1286">apiVersion</span></span> |<span data-ttu-id="d044f-1287">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-1287">1.0</span></span> |

<span data-ttu-id="d044f-1288">**Antwoord:**</span><span class="sxs-lookup"><span data-stu-id="d044f-1288">**Response:**</span></span>

<span data-ttu-id="d044f-1289">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-1289">HTTP Status code: 200</span></span>

### <a name="117-cancel-build"></a><span data-ttu-id="d044f-1290">11.7.</span><span class="sxs-lookup"><span data-stu-id="d044f-1290">11.7.</span></span> <span data-ttu-id="d044f-1291">Build annuleren</span><span class="sxs-lookup"><span data-stu-id="d044f-1291">Cancel Build</span></span>
<span data-ttu-id="d044f-1292">Een build waarvan bij het bouwen van de status is geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="d044f-1292">Cancels a build that is in building status.</span></span>

| <span data-ttu-id="d044f-1293">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-1293">HTTP Method</span></span> | <span data-ttu-id="d044f-1294">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-1294">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-1295">PLAATSEN</span><span class="sxs-lookup"><span data-stu-id="d044f-1295">PUT</span></span> |`<rootURI>/CancelBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="d044f-1296">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d044f-1296">Example:</span></span><br>`<rootURI>/CancelBuild?buildId=%271500076%27&apiVersion=%271.0%27` |

| <span data-ttu-id="d044f-1297">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-1297">Parameter Name</span></span> | <span data-ttu-id="d044f-1298">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-1298">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-1299">buildId</span><span class="sxs-lookup"><span data-stu-id="d044f-1299">buildId</span></span> |<span data-ttu-id="d044f-1300">De unieke id van Hallo build.</span><span class="sxs-lookup"><span data-stu-id="d044f-1300">Unique identifier of hello build.</span></span> |
| <span data-ttu-id="d044f-1301">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-1301">apiVersion</span></span> |<span data-ttu-id="d044f-1302">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-1302">1.0</span></span> |

<span data-ttu-id="d044f-1303">**Antwoord:**</span><span class="sxs-lookup"><span data-stu-id="d044f-1303">**Response:**</span></span>

<span data-ttu-id="d044f-1304">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-1304">HTTP Status code: 200</span></span>

### <a name="118-get-build-parameters"></a><span data-ttu-id="d044f-1305">11.8.</span><span class="sxs-lookup"><span data-stu-id="d044f-1305">11.8.</span></span> <span data-ttu-id="d044f-1306">Het ophalen van Build-Parameters</span><span class="sxs-lookup"><span data-stu-id="d044f-1306">Get Build Parameters</span></span>
<span data-ttu-id="d044f-1307">Haalt bouwen parameters.</span><span class="sxs-lookup"><span data-stu-id="d044f-1307">Retrieves build parameters.</span></span>

| <span data-ttu-id="d044f-1308">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-1308">HTTP Method</span></span> | <span data-ttu-id="d044f-1309">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-1309">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-1310">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="d044f-1310">GET</span></span> |`<rootURI>/GetBuildParameters?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="d044f-1311">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d044f-1311">Example:</span></span><br>`<rootURI>/GetBuildParameters?buildId=%271000653%27&apiVersion=%271.0%27` |

| <span data-ttu-id="d044f-1312">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-1312">Parameter Name</span></span> | <span data-ttu-id="d044f-1313">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-1313">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-1314">buildId</span><span class="sxs-lookup"><span data-stu-id="d044f-1314">buildId</span></span> |<span data-ttu-id="d044f-1315">De unieke id van Hallo build.</span><span class="sxs-lookup"><span data-stu-id="d044f-1315">Unique identifier of hello build.</span></span> |
| <span data-ttu-id="d044f-1316">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-1316">apiVersion</span></span> |<span data-ttu-id="d044f-1317">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-1317">1.0</span></span> |

<span data-ttu-id="d044f-1318">**Antwoord:**</span><span class="sxs-lookup"><span data-stu-id="d044f-1318">**Response:**</span></span>

<span data-ttu-id="d044f-1319">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-1319">HTTP Status code: 200</span></span>

<span data-ttu-id="d044f-1320">Deze API retourneert een verzameling van sleutel/waarde-elementen.</span><span class="sxs-lookup"><span data-stu-id="d044f-1320">This API returns a collection of key/value elements.</span></span> <span data-ttu-id="d044f-1321">Elk element staat voor een parameter en de waarde ervan:</span><span class="sxs-lookup"><span data-stu-id="d044f-1321">Each element represents a parameter and its value:</span></span>

* <span data-ttu-id="d044f-1322">`feed/entry/content/properties/Key`-Parameternaam bouwen.</span><span class="sxs-lookup"><span data-stu-id="d044f-1322">`feed/entry/content/properties/Key` - Build parameter name.</span></span>
* <span data-ttu-id="d044f-1323">`feed/entry/content/properties/Value`-Parameterwaarde bouwen.</span><span class="sxs-lookup"><span data-stu-id="d044f-1323">`feed/entry/content/properties/Value` - Build parameter value.</span></span>

<span data-ttu-id="d044f-1324">Hallo in de volgende tabel beschrijft Hallo-waarde die aangeeft voor elke sleutel.</span><span class="sxs-lookup"><span data-stu-id="d044f-1324">hello table below depicts hello value that each key represents.</span></span>

| <span data-ttu-id="d044f-1325">Sleutel</span><span class="sxs-lookup"><span data-stu-id="d044f-1325">Key</span></span> | <span data-ttu-id="d044f-1326">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d044f-1326">Description</span></span> | <span data-ttu-id="d044f-1327">Type</span><span class="sxs-lookup"><span data-stu-id="d044f-1327">Type</span></span> | <span data-ttu-id="d044f-1328">Geldige waarde</span><span class="sxs-lookup"><span data-stu-id="d044f-1328">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d044f-1329">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="d044f-1329">NumberOfModelIterations</span></span> |<span data-ttu-id="d044f-1330">het aantal iteraties Hallo model functioneert Hallo komt tot uiting in Hallo algemene compute tijd en Hallo nauwkeurigheid van het model.</span><span class="sxs-lookup"><span data-stu-id="d044f-1330">hello number of iterations hello model performs is reflected by hello overall compute time and hello model accuracy.</span></span> <span data-ttu-id="d044f-1331">Hallo hoger Hallo nummer, Hallo betere nauwkeurigheid u krijgt, maar Hallo compute tijd zal langer duren.</span><span class="sxs-lookup"><span data-stu-id="d044f-1331">hello higher hello number, hello better accuracy you will get, but hello compute time will take longer.</span></span> |<span data-ttu-id="d044f-1332">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="d044f-1332">Integer</span></span> |<span data-ttu-id="d044f-1333">10-50</span><span class="sxs-lookup"><span data-stu-id="d044f-1333">10-50</span></span> |
| <span data-ttu-id="d044f-1334">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="d044f-1334">NumberOfModelDimensions</span></span> |<span data-ttu-id="d044f-1335">het aantal dimensies Hallo is gekoppeld toohello aantal 'functies' hello model wordt geprobeerd toofind binnen uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="d044f-1335">hello number of dimensions relates toohello number of 'features' hello model will try toofind within your data.</span></span> <span data-ttu-id="d044f-1336">Vergroot het aantal dimensies Hallo kunt beter aan te passen van Hallo resultaten in kleinere clusters.</span><span class="sxs-lookup"><span data-stu-id="d044f-1336">Increasing hello number of dimensions will allow better fine-tuning of hello results into smaller clusters.</span></span> <span data-ttu-id="d044f-1337">Te veel dimensies kunnen echter Hallo model niet vinden van correlatie tussen items.</span><span class="sxs-lookup"><span data-stu-id="d044f-1337">However, too many dimensions will prevent hello model from finding correlations between items.</span></span> |<span data-ttu-id="d044f-1338">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="d044f-1338">Integer</span></span> |<span data-ttu-id="d044f-1339">10-40</span><span class="sxs-lookup"><span data-stu-id="d044f-1339">10-40</span></span> |
| <span data-ttu-id="d044f-1340">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="d044f-1340">ItemCutOffLowerBound</span></span> |<span data-ttu-id="d044f-1341">Hallo item ondergrens voor Hallo koeler definieert.</span><span class="sxs-lookup"><span data-stu-id="d044f-1341">Defines hello item lower bound for hello condenser.</span></span> <span data-ttu-id="d044f-1342">Zie gebruik koeler hierboven.</span><span class="sxs-lookup"><span data-stu-id="d044f-1342">See usage condenser above.</span></span> |<span data-ttu-id="d044f-1343">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="d044f-1343">Integer</span></span> |<span data-ttu-id="d044f-1344">2 of hoger (koeler 0 uitschakelen)</span><span class="sxs-lookup"><span data-stu-id="d044f-1344">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="d044f-1345">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="d044f-1345">ItemCutOffUpperBound</span></span> |<span data-ttu-id="d044f-1346">Hallo item bovengrens voor Hallo koeler definieert.</span><span class="sxs-lookup"><span data-stu-id="d044f-1346">Defines hello item upper bound for hello condenser.</span></span> <span data-ttu-id="d044f-1347">Zie gebruik koeler hierboven.</span><span class="sxs-lookup"><span data-stu-id="d044f-1347">See usage condenser above.</span></span> |<span data-ttu-id="d044f-1348">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="d044f-1348">Integer</span></span> |<span data-ttu-id="d044f-1349">2 of hoger (koeler 0 uitschakelen)</span><span class="sxs-lookup"><span data-stu-id="d044f-1349">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="d044f-1350">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="d044f-1350">UserCutOffLowerBound</span></span> |<span data-ttu-id="d044f-1351">Hallo gebruiker ondergrens voor Hallo koeler definieert.</span><span class="sxs-lookup"><span data-stu-id="d044f-1351">Defines hello user lower bound for hello condenser.</span></span> <span data-ttu-id="d044f-1352">Zie gebruik koeler hierboven.</span><span class="sxs-lookup"><span data-stu-id="d044f-1352">See usage condenser above.</span></span> |<span data-ttu-id="d044f-1353">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="d044f-1353">Integer</span></span> |<span data-ttu-id="d044f-1354">2 of hoger (koeler 0 uitschakelen)</span><span class="sxs-lookup"><span data-stu-id="d044f-1354">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="d044f-1355">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="d044f-1355">UserCutOffUpperBound</span></span> |<span data-ttu-id="d044f-1356">Hallo gebruiker bovengrens voor Hallo koeler definieert.</span><span class="sxs-lookup"><span data-stu-id="d044f-1356">Defines hello user upper bound for hello condenser.</span></span> <span data-ttu-id="d044f-1357">Zie gebruik koeler hierboven.</span><span class="sxs-lookup"><span data-stu-id="d044f-1357">See usage condenser above.</span></span> |<span data-ttu-id="d044f-1358">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="d044f-1358">Integer</span></span> |<span data-ttu-id="d044f-1359">2 of hoger (koeler 0 uitschakelen)</span><span class="sxs-lookup"><span data-stu-id="d044f-1359">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="d044f-1360">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d044f-1360">Description</span></span> |<span data-ttu-id="d044f-1361">Beschrijving bouwen.</span><span class="sxs-lookup"><span data-stu-id="d044f-1361">Build description.</span></span> |<span data-ttu-id="d044f-1362">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d044f-1362">String</span></span> |<span data-ttu-id="d044f-1363">Alle tekst maximaal 512 tekens</span><span class="sxs-lookup"><span data-stu-id="d044f-1363">Any text, maximum 512 chars</span></span> |
| <span data-ttu-id="d044f-1364">EnableModelingInsights</span><span class="sxs-lookup"><span data-stu-id="d044f-1364">EnableModelingInsights</span></span> |<span data-ttu-id="d044f-1365">Hiermee kunt u toocompute metrische gegevens op Hallo aanbeveling model.</span><span class="sxs-lookup"><span data-stu-id="d044f-1365">Allows you toocompute metrics on hello recommendation model.</span></span> |<span data-ttu-id="d044f-1366">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="d044f-1366">Boolean</span></span> |<span data-ttu-id="d044f-1367">Waar/onwaar</span><span class="sxs-lookup"><span data-stu-id="d044f-1367">True/False</span></span> |
| <span data-ttu-id="d044f-1368">UseFeaturesInModel</span><span class="sxs-lookup"><span data-stu-id="d044f-1368">UseFeaturesInModel</span></span> |<span data-ttu-id="d044f-1369">Hiermee wordt aangegeven als functies in volgorde tooenhance Hallo aanbeveling model kunnen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d044f-1369">Indicates if features can be used in order tooenhance hello recommendation model.</span></span> |<span data-ttu-id="d044f-1370">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="d044f-1370">Boolean</span></span> |<span data-ttu-id="d044f-1371">Waar/onwaar</span><span class="sxs-lookup"><span data-stu-id="d044f-1371">True/False</span></span> |
| <span data-ttu-id="d044f-1372">ModelingFeatureList</span><span class="sxs-lookup"><span data-stu-id="d044f-1372">ModelingFeatureList</span></span> |<span data-ttu-id="d044f-1373">Door komma's gescheiden lijst van de functie namen toobe Hallo aanbeveling gebouwd in volgorde tooenhance Hallo aanbeveling gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d044f-1373">Comma-separated list of feature names toobe used in hello recommendation build, in order tooenhance hello recommendation.</span></span> |<span data-ttu-id="d044f-1374">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d044f-1374">String</span></span> |<span data-ttu-id="d044f-1375">Onderdeelnamen up too512 tekens</span><span class="sxs-lookup"><span data-stu-id="d044f-1375">Feature names, up too512 chars</span></span> |
| <span data-ttu-id="d044f-1376">AllowColdItemPlacement</span><span class="sxs-lookup"><span data-stu-id="d044f-1376">AllowColdItemPlacement</span></span> |<span data-ttu-id="d044f-1377">Hiermee wordt aangegeven als Hallo aanbeveling ook koude items via de functie overeenkomsten pushen moet.</span><span class="sxs-lookup"><span data-stu-id="d044f-1377">Indicates if hello recommendation should also push cold items via feature similarity.</span></span> |<span data-ttu-id="d044f-1378">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="d044f-1378">Boolean</span></span> |<span data-ttu-id="d044f-1379">Waar/onwaar</span><span class="sxs-lookup"><span data-stu-id="d044f-1379">True/False</span></span> |
| <span data-ttu-id="d044f-1380">EnableFeatureCorrelation</span><span class="sxs-lookup"><span data-stu-id="d044f-1380">EnableFeatureCorrelation</span></span> |<span data-ttu-id="d044f-1381">Hiermee wordt aangegeven als functies kunnen worden gebruikt in de redenering.</span><span class="sxs-lookup"><span data-stu-id="d044f-1381">Indicates if features can be used in reasoning.</span></span> |<span data-ttu-id="d044f-1382">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="d044f-1382">Boolean</span></span> |<span data-ttu-id="d044f-1383">Waar/onwaar</span><span class="sxs-lookup"><span data-stu-id="d044f-1383">True/False</span></span> |
| <span data-ttu-id="d044f-1384">ReasoningFeatureList</span><span class="sxs-lookup"><span data-stu-id="d044f-1384">ReasoningFeatureList</span></span> |<span data-ttu-id="d044f-1385">Door komma's gescheiden lijst van de functie namen toobe gebruikt voor redeneren zinnen (bijvoorbeeld aanbeveling uitleg).</span><span class="sxs-lookup"><span data-stu-id="d044f-1385">Comma-separated list of feature names toobe used for reasoning sentences (e.g. recommendation explanations).</span></span> |<span data-ttu-id="d044f-1386">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d044f-1386">String</span></span> |<span data-ttu-id="d044f-1387">Onderdeelnamen up too512 tekens</span><span class="sxs-lookup"><span data-stu-id="d044f-1387">Feature names, up too512 chars</span></span> |

<span data-ttu-id="d044f-1388">OData-XML</span><span class="sxs-lookup"><span data-stu-id="d044f-1388">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get build parameters</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2015-01-08T13:50:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UseFeaturesInModel</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">AllowColdItemPlacement</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">EnableFeatureCorrelation</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">EnableModelingInsights</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">NumberOfModelIterations</d:Key>
                    <d:Value m:type="Edm.String">10</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
            <titletype="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">NumberOfModelDimensions</d:Key>
                    <d:Value m:type="Edm.String">10</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <linkrel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ItemCutOffLowerBound</d:Key>
                    <d:Value m:type="Edm.String">2</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ItemCutOffUpperBound</d:Key>
                    <d:Value m:type="Edm.String">2147483647</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UserCutOffLowerBound</d:Key>
                    <d:Value m:type="Edm.String">2</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UserCutOffUpperBound</d:Key>
                    <d:Value m:type="Edm.String">2147483647</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ModelingFeatureList</d:Key>
                    <d:Value m:type="Edm.String"/>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ReasoningFeatureList</d:Key>
                    <d:Value m:type="Edm.String"/>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">Description</d:Key>
                    <d:Value m:type="Edm.String">rankBuild</d:Value>
                </m:properties>
            </content>
        </entry>
    </feed>

## <a name="12-recommendation"></a><span data-ttu-id="d044f-1389">12. Aanbeveling</span><span class="sxs-lookup"><span data-stu-id="d044f-1389">12. Recommendation</span></span>
### <a name="121-get-item-recommendations-for-active-build"></a><span data-ttu-id="d044f-1390">12.1.</span><span class="sxs-lookup"><span data-stu-id="d044f-1390">12.1.</span></span> <span data-ttu-id="d044f-1391">Item aanbevelingen krijgen (voor actieve build)</span><span class="sxs-lookup"><span data-stu-id="d044f-1391">Get Item Recommendations (for active build)</span></span>
<span data-ttu-id="d044f-1392">Ophalen van aanbevelingen van Hallo active build van het type 'Aanbeveling' of 'Fbt' op basis van een lijst met items zaden (invoer).</span><span class="sxs-lookup"><span data-stu-id="d044f-1392">Get recommendations of hello active build of type "Recommendation" or "Fbt" based on a list of seeds (input) items.</span></span>

| <span data-ttu-id="d044f-1393">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-1393">HTTP Method</span></span> | <span data-ttu-id="d044f-1394">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-1394">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-1395">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="d044f-1395">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="d044f-1396">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d044f-1396">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="d044f-1397">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-1397">Parameter Name</span></span> | <span data-ttu-id="d044f-1398">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-1398">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-1399">Model</span><span class="sxs-lookup"><span data-stu-id="d044f-1399">modelId</span></span> |<span data-ttu-id="d044f-1400">De unieke id van het Hallo-model</span><span class="sxs-lookup"><span data-stu-id="d044f-1400">Unique identifier of hello model</span></span> |
| <span data-ttu-id="d044f-1401">ItemID 's</span><span class="sxs-lookup"><span data-stu-id="d044f-1401">itemIds</span></span> |<span data-ttu-id="d044f-1402">Door komma's gescheiden lijst met Hallo items toorecommend voor.</span><span class="sxs-lookup"><span data-stu-id="d044f-1402">Comma-separated list of hello items toorecommend for.</span></span> <br><span data-ttu-id="d044f-1403">Als Hallo active build van typt FBT en vervolgens kunt u slechts één item verzenden.</span><span class="sxs-lookup"><span data-stu-id="d044f-1403">If hello active build is of type FBT then you can send only one item.</span></span> <br><span data-ttu-id="d044f-1404">Maximale lengte: 1024</span><span class="sxs-lookup"><span data-stu-id="d044f-1404">Max length: 1024</span></span> |
| <span data-ttu-id="d044f-1405">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="d044f-1405">numberOfResults</span></span> |<span data-ttu-id="d044f-1406">Aantal vereiste resultaten</span><span class="sxs-lookup"><span data-stu-id="d044f-1406">Number of required results</span></span> <br> <span data-ttu-id="d044f-1407">Max: 150</span><span class="sxs-lookup"><span data-stu-id="d044f-1407">Max: 150</span></span> |
| <span data-ttu-id="d044f-1408">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="d044f-1408">includeMetatadata</span></span> |<span data-ttu-id="d044f-1409">Toekomstig gebruik, altijd Onwaar</span><span class="sxs-lookup"><span data-stu-id="d044f-1409">Future use, always false</span></span> |
| <span data-ttu-id="d044f-1410">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-1410">apiVersion</span></span> |<span data-ttu-id="d044f-1411">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-1411">1.0</span></span> |

<span data-ttu-id="d044f-1412">**Antwoord:**</span><span class="sxs-lookup"><span data-stu-id="d044f-1412">**Response:**</span></span>

<span data-ttu-id="d044f-1413">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-1413">HTTP Status code: 200</span></span>

<span data-ttu-id="d044f-1414">Hallo-antwoord bevat één vermelding per aanbevolen-item.</span><span class="sxs-lookup"><span data-stu-id="d044f-1414">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="d044f-1415">Elk item heeft Hallo gegevens te volgen:</span><span class="sxs-lookup"><span data-stu-id="d044f-1415">Each entry has hello following data:</span></span>

* <span data-ttu-id="d044f-1416">`Feed\entry\content\properties\Id`-Aanbevolen artikel-ID.</span><span class="sxs-lookup"><span data-stu-id="d044f-1416">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="d044f-1417">`Feed\entry\content\properties\Name`-De naam van het Hallo-item.</span><span class="sxs-lookup"><span data-stu-id="d044f-1417">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="d044f-1418">`Feed\entry\content\properties\Rating`-Classificatie van Hallo aanbeveling; hogere waarde betekent hogere betrouwbaarheid.</span><span class="sxs-lookup"><span data-stu-id="d044f-1418">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="d044f-1419">`Feed\entry\content\properties\Reasoning`-Aanbeveling redeneren (bijvoorbeeld aanbeveling uitleg).</span><span class="sxs-lookup"><span data-stu-id="d044f-1419">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="d044f-1420">Hallo voorbeeld hieronder reactie bevat 10 aanbevolen items.</span><span class="sxs-lookup"><span data-stu-id="d044f-1420">hello example response below includes 10 recommended items.</span></span>

<span data-ttu-id="d044f-1421">OData-XML</span><span class="sxs-lookup"><span data-stu-id="d044f-1421">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
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

### <a name="122-get-item-recommendations-of-a-specific-build"></a><span data-ttu-id="d044f-1422">12.2.</span><span class="sxs-lookup"><span data-stu-id="d044f-1422">12.2.</span></span> <span data-ttu-id="d044f-1423">Item aanbevelingen (van een specifieke build) ophalen</span><span class="sxs-lookup"><span data-stu-id="d044f-1423">Get Item Recommendations (of a specific build)</span></span>
<span data-ttu-id="d044f-1424">De aanbevelingen van een specifieke build van het type 'Aanbeveling' of 'Fbt' krijgen.</span><span class="sxs-lookup"><span data-stu-id="d044f-1424">Get recommendations of a specific build of type "Recommendation" or "Fbt".</span></span>

| <span data-ttu-id="d044f-1425">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-1425">HTTP Method</span></span> | <span data-ttu-id="d044f-1426">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-1426">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-1427">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="d044f-1427">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="d044f-1428">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d044f-1428">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| <span data-ttu-id="d044f-1429">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-1429">Parameter Name</span></span> | <span data-ttu-id="d044f-1430">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-1430">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-1431">Model</span><span class="sxs-lookup"><span data-stu-id="d044f-1431">modelId</span></span> |<span data-ttu-id="d044f-1432">De unieke id van het Hallo-model</span><span class="sxs-lookup"><span data-stu-id="d044f-1432">Unique identifier of hello model</span></span> |
| <span data-ttu-id="d044f-1433">ItemID 's</span><span class="sxs-lookup"><span data-stu-id="d044f-1433">itemIds</span></span> |<span data-ttu-id="d044f-1434">Door komma's gescheiden lijst met Hallo items toorecommend voor.</span><span class="sxs-lookup"><span data-stu-id="d044f-1434">Comma-separated list of hello items toorecommend for.</span></span> <br><span data-ttu-id="d044f-1435">Als Hallo active build van typt FBT en vervolgens kunt u slechts één item verzenden.</span><span class="sxs-lookup"><span data-stu-id="d044f-1435">If hello active build is of type FBT then you can send only one item.</span></span> <br><span data-ttu-id="d044f-1436">Maximale lengte: 1024</span><span class="sxs-lookup"><span data-stu-id="d044f-1436">Max length: 1024</span></span> |
| <span data-ttu-id="d044f-1437">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="d044f-1437">numberOfResults</span></span> |<span data-ttu-id="d044f-1438">Aantal vereiste resultaten</span><span class="sxs-lookup"><span data-stu-id="d044f-1438">Number of required results</span></span> <br> <span data-ttu-id="d044f-1439">Max: 150</span><span class="sxs-lookup"><span data-stu-id="d044f-1439">Max: 150</span></span> |
| <span data-ttu-id="d044f-1440">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="d044f-1440">includeMetatadata</span></span> |<span data-ttu-id="d044f-1441">Toekomstig gebruik, altijd Onwaar</span><span class="sxs-lookup"><span data-stu-id="d044f-1441">Future use, always false</span></span> |
| <span data-ttu-id="d044f-1442">buildId</span><span class="sxs-lookup"><span data-stu-id="d044f-1442">buildId</span></span> |<span data-ttu-id="d044f-1443">Hallo toouse id voor deze aanvraag aanbeveling bouwen</span><span class="sxs-lookup"><span data-stu-id="d044f-1443">hello build id toouse for this recommendation request</span></span> |
| <span data-ttu-id="d044f-1444">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-1444">apiVersion</span></span> |<span data-ttu-id="d044f-1445">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-1445">1.0</span></span> |

<span data-ttu-id="d044f-1446">**Antwoord:**</span><span class="sxs-lookup"><span data-stu-id="d044f-1446">**Response:**</span></span>

<span data-ttu-id="d044f-1447">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-1447">HTTP Status code: 200</span></span>

<span data-ttu-id="d044f-1448">Hallo-antwoord bevat één vermelding per aanbevolen-item.</span><span class="sxs-lookup"><span data-stu-id="d044f-1448">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="d044f-1449">Elk item heeft Hallo gegevens te volgen:</span><span class="sxs-lookup"><span data-stu-id="d044f-1449">Each entry has hello following data:</span></span>

* <span data-ttu-id="d044f-1450">`Feed\entry\content\properties\Id`-Aanbevolen artikel-ID.</span><span class="sxs-lookup"><span data-stu-id="d044f-1450">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="d044f-1451">`Feed\entry\content\properties\Name`-De naam van het Hallo-item.</span><span class="sxs-lookup"><span data-stu-id="d044f-1451">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="d044f-1452">`Feed\entry\content\properties\Rating`-Classificatie van Hallo aanbeveling; hogere waarde betekent hogere betrouwbaarheid.</span><span class="sxs-lookup"><span data-stu-id="d044f-1452">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="d044f-1453">`Feed\entry\content\properties\Reasoning`-Aanbeveling redeneren (bijvoorbeeld aanbeveling uitleg).</span><span class="sxs-lookup"><span data-stu-id="d044f-1453">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="d044f-1454">Zie het voorbeeld van een reactie in 12.1</span><span class="sxs-lookup"><span data-stu-id="d044f-1454">See a response example in 12.1</span></span>

### <a name="123-get-fbt-recommendations-for-active-build"></a><span data-ttu-id="d044f-1455">12.3.</span><span class="sxs-lookup"><span data-stu-id="d044f-1455">12.3.</span></span> <span data-ttu-id="d044f-1456">FBT aanbevelingen krijgen (voor actieve build)</span><span class="sxs-lookup"><span data-stu-id="d044f-1456">Get FBT Recommendations (for active build)</span></span>
<span data-ttu-id="d044f-1457">Haal de aanbevelingen van Hallo active build van het type 'Fbt' die is gebaseerd op een item seed (invoer).</span><span class="sxs-lookup"><span data-stu-id="d044f-1457">Get recommendations of hello active build of type "Fbt" based on a seed (input) item.</span></span>

| <span data-ttu-id="d044f-1458">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-1458">HTTP Method</span></span> | <span data-ttu-id="d044f-1459">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-1459">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-1460">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="d044f-1460">GET</span></span> |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="d044f-1461">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d044f-1461">Example:</span></span><br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=<double>&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="d044f-1462">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-1462">Parameter Name</span></span> | <span data-ttu-id="d044f-1463">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-1463">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-1464">Model</span><span class="sxs-lookup"><span data-stu-id="d044f-1464">modelId</span></span> |<span data-ttu-id="d044f-1465">De unieke id van het Hallo-model</span><span class="sxs-lookup"><span data-stu-id="d044f-1465">Unique identifier of hello model</span></span> |
| <span data-ttu-id="d044f-1466">itemId</span><span class="sxs-lookup"><span data-stu-id="d044f-1466">itemId</span></span> |<span data-ttu-id="d044f-1467">Item toorecommend voor.</span><span class="sxs-lookup"><span data-stu-id="d044f-1467">Item toorecommend for.</span></span> <br><span data-ttu-id="d044f-1468">Maximale lengte: 1024</span><span class="sxs-lookup"><span data-stu-id="d044f-1468">Max length: 1024</span></span> |
| <span data-ttu-id="d044f-1469">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="d044f-1469">numberOfResults</span></span> |<span data-ttu-id="d044f-1470">Aantal vereiste resultaten</span><span class="sxs-lookup"><span data-stu-id="d044f-1470">Number of required results</span></span> <br><span data-ttu-id="d044f-1471">Max: 150</span><span class="sxs-lookup"><span data-stu-id="d044f-1471">Max: 150</span></span> |
| <span data-ttu-id="d044f-1472">minimalScore</span><span class="sxs-lookup"><span data-stu-id="d044f-1472">minimalScore</span></span> |<span data-ttu-id="d044f-1473">Minimale score die een set veelvuldig moet in de volgorde toobe opgenomen in Hallo geretourneerd resulteert</span><span class="sxs-lookup"><span data-stu-id="d044f-1473">Minimal score that a frequent set should have in order toobe included in hello returned results</span></span> |
| <span data-ttu-id="d044f-1474">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="d044f-1474">includeMetatadata</span></span> |<span data-ttu-id="d044f-1475">Toekomstig gebruik, altijd Onwaar</span><span class="sxs-lookup"><span data-stu-id="d044f-1475">Future use, always false</span></span> |
| <span data-ttu-id="d044f-1476">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-1476">apiVersion</span></span> |<span data-ttu-id="d044f-1477">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-1477">1.0</span></span> |

<span data-ttu-id="d044f-1478">**Antwoord:**</span><span class="sxs-lookup"><span data-stu-id="d044f-1478">**Response:**</span></span>

<span data-ttu-id="d044f-1479">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-1479">HTTP Status code: 200</span></span>

<span data-ttu-id="d044f-1480">Hallo-antwoord bevat één vermelding per set aanbevolen item (een set van items die meestal worden gekocht met Hallo seed/invoer item).</span><span class="sxs-lookup"><span data-stu-id="d044f-1480">hello response includes one entry per recommended item set (a set of items which are usually bought together with hello seed/input item).</span></span> <span data-ttu-id="d044f-1481">Elk item heeft Hallo gegevens te volgen:</span><span class="sxs-lookup"><span data-stu-id="d044f-1481">Each entry has hello following data:</span></span>

* <span data-ttu-id="d044f-1482">`Feed\entry\content\properties\Id1`-Aanbevolen artikel-ID.</span><span class="sxs-lookup"><span data-stu-id="d044f-1482">`Feed\entry\content\properties\Id1` - Recommended item ID.</span></span>
* <span data-ttu-id="d044f-1483">`Feed\entry\content\properties\Name1`-De naam van het Hallo-item.</span><span class="sxs-lookup"><span data-stu-id="d044f-1483">`Feed\entry\content\properties\Name1` - Name of hello item.</span></span>
* <span data-ttu-id="d044f-1484">`Feed\entry\content\properties\Id2`-2e aanbevolen artikel-ID (optioneel).</span><span class="sxs-lookup"><span data-stu-id="d044f-1484">`Feed\entry\content\properties\Id2` - 2nd recommended item ID (optional).</span></span>
* <span data-ttu-id="d044f-1485">`Feed\entry\content\properties\Name2`-De naam van de 2e item hello (optioneel).</span><span class="sxs-lookup"><span data-stu-id="d044f-1485">`Feed\entry\content\properties\Name2` - Name of hello 2nd item (optional).</span></span>
* <span data-ttu-id="d044f-1486">`Feed\entry\content\properties\Rating`-Classificatie van Hallo aanbeveling; hogere waarde betekent hogere betrouwbaarheid.</span><span class="sxs-lookup"><span data-stu-id="d044f-1486">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="d044f-1487">`Feed\entry\content\properties\Reasoning`-Aanbeveling redeneren (bijvoorbeeld aanbeveling uitleg).</span><span class="sxs-lookup"><span data-stu-id="d044f-1487">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="d044f-1488">Hallo voorbeeld hieronder reactie bevat 3 aanbevolen item sets.</span><span class="sxs-lookup"><span data-stu-id="d044f-1488">hello example response below includes 3 recommended item sets.</span></span>

<span data-ttu-id="d044f-1489">OData-XML</span><span class="sxs-lookup"><span data-stu-id="d044f-1489">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemId='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">159</d:Id1>
        <d:Name1 m:type="Edm.String">159</d:Name1>
        <d:Id2 m:type="Edm.String"></d:Id2>
        <d:Name2 m:type="Edm.String"></d:Name2>
        <d:Rating m:type="Edm.Double">0.543343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '159'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">52</d:Id1>
        <d:Name1 m:type="Edm.String">52</d:Name1>
        <d:Id2 m:type="Edm.String"></d:Id2>
        <d:Name2 m:type="Edm.String"></d:Name2>
        <d:Rating m:type="Edm.Double">0.533343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '52'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">35</d:Id1>
        <d:Name1 m:type="Edm.String">35</d:Name1>
        <d:Id2 m:type="Edm.String">102</d:Id2>
        <d:Name2 m:type="Edm.String">102</d:Name2>
        <d:Rating m:type="Edm.Double">0.523343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '35' and '102'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="124-get-fbt-recommendations-of-a-specific-build"></a><span data-ttu-id="d044f-1490">12.4.</span><span class="sxs-lookup"><span data-stu-id="d044f-1490">12.4.</span></span> <span data-ttu-id="d044f-1491">Ophalen van de aanbevelingen FBT (van een specifieke build)</span><span class="sxs-lookup"><span data-stu-id="d044f-1491">Get FBT Recommendations (of a specific build)</span></span>
<span data-ttu-id="d044f-1492">De aanbevelingen van een specifieke build van het type 'Fbt' krijgen.</span><span class="sxs-lookup"><span data-stu-id="d044f-1492">Get recommendations of a specific build of type "Fbt".</span></span>

| <span data-ttu-id="d044f-1493">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-1493">HTTP Method</span></span> | <span data-ttu-id="d044f-1494">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-1494">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-1495">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="d044f-1495">GET</span></span> |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="d044f-1496">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d044f-1496">Example:</span></span><br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=0.1&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| <span data-ttu-id="d044f-1497">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-1497">Parameter Name</span></span> | <span data-ttu-id="d044f-1498">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-1498">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-1499">Model</span><span class="sxs-lookup"><span data-stu-id="d044f-1499">modelId</span></span> |<span data-ttu-id="d044f-1500">De unieke id van het Hallo-model</span><span class="sxs-lookup"><span data-stu-id="d044f-1500">Unique identifier of hello model</span></span> |
| <span data-ttu-id="d044f-1501">itemId</span><span class="sxs-lookup"><span data-stu-id="d044f-1501">itemId</span></span> |<span data-ttu-id="d044f-1502">Item toorecommend voor.</span><span class="sxs-lookup"><span data-stu-id="d044f-1502">Item toorecommend for.</span></span> <br><span data-ttu-id="d044f-1503">Maximale lengte: 1024</span><span class="sxs-lookup"><span data-stu-id="d044f-1503">Max length: 1024</span></span> |
| <span data-ttu-id="d044f-1504">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="d044f-1504">numberOfResults</span></span> |<span data-ttu-id="d044f-1505">Aantal vereiste resultaten</span><span class="sxs-lookup"><span data-stu-id="d044f-1505">Number of required results</span></span> <br><span data-ttu-id="d044f-1506">Max: 150</span><span class="sxs-lookup"><span data-stu-id="d044f-1506">Max: 150</span></span> |
| <span data-ttu-id="d044f-1507">minimalScore</span><span class="sxs-lookup"><span data-stu-id="d044f-1507">minimalScore</span></span> |<span data-ttu-id="d044f-1508">Minimale score die een set veelvuldig moet in de volgorde toobe opgenomen in Hallo geretourneerd resulteert</span><span class="sxs-lookup"><span data-stu-id="d044f-1508">Minimal score that a frequent set should have in order toobe included in hello returned results</span></span> |
| <span data-ttu-id="d044f-1509">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="d044f-1509">includeMetatadata</span></span> |<span data-ttu-id="d044f-1510">Toekomstig gebruik, altijd Onwaar</span><span class="sxs-lookup"><span data-stu-id="d044f-1510">Future use, always false</span></span> |
| <span data-ttu-id="d044f-1511">buildId</span><span class="sxs-lookup"><span data-stu-id="d044f-1511">buildId</span></span> |<span data-ttu-id="d044f-1512">Hallo toouse id voor deze aanvraag aanbeveling bouwen</span><span class="sxs-lookup"><span data-stu-id="d044f-1512">hello build id toouse for this recommendation request</span></span> |
| <span data-ttu-id="d044f-1513">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-1513">apiVersion</span></span> |<span data-ttu-id="d044f-1514">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-1514">1.0</span></span> |

<span data-ttu-id="d044f-1515">**Antwoord:**</span><span class="sxs-lookup"><span data-stu-id="d044f-1515">**Response:**</span></span>

<span data-ttu-id="d044f-1516">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-1516">HTTP Status code: 200</span></span>

<span data-ttu-id="d044f-1517">Hallo-antwoord bevat één vermelding per set aanbevolen item (een set van items die meestal worden gekocht met Hallo seed/invoer item).</span><span class="sxs-lookup"><span data-stu-id="d044f-1517">hello response includes one entry per recommended item set (a set of items which are usually bought together with hello seed/input item).</span></span> <span data-ttu-id="d044f-1518">Elk item heeft Hallo gegevens te volgen:</span><span class="sxs-lookup"><span data-stu-id="d044f-1518">Each entry has hello following data:</span></span>

* <span data-ttu-id="d044f-1519">`Feed\entry\content\properties\Id1`-Aanbevolen artikel-ID.</span><span class="sxs-lookup"><span data-stu-id="d044f-1519">`Feed\entry\content\properties\Id1` - Recommended item ID.</span></span>
* <span data-ttu-id="d044f-1520">`Feed\entry\content\properties\Name1`-De naam van het Hallo-item.</span><span class="sxs-lookup"><span data-stu-id="d044f-1520">`Feed\entry\content\properties\Name1` - Name of hello item.</span></span>
* <span data-ttu-id="d044f-1521">`Feed\entry\content\properties\Id2`-2e aanbevolen artikel-ID (optioneel).</span><span class="sxs-lookup"><span data-stu-id="d044f-1521">`Feed\entry\content\properties\Id2` - 2nd recommended item ID (optional).</span></span>
* <span data-ttu-id="d044f-1522">`Feed\entry\content\properties\Name2`-De naam van de 2e item hello (optioneel).</span><span class="sxs-lookup"><span data-stu-id="d044f-1522">`Feed\entry\content\properties\Name2` - Name of hello 2nd item (optional).</span></span>
* <span data-ttu-id="d044f-1523">`Feed\entry\content\properties\Rating`-Classificatie van Hallo aanbeveling; hogere waarde betekent hogere betrouwbaarheid.</span><span class="sxs-lookup"><span data-stu-id="d044f-1523">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="d044f-1524">`Feed\entry\content\properties\Reasoning`-Aanbeveling redeneren (bijvoorbeeld aanbeveling uitleg).</span><span class="sxs-lookup"><span data-stu-id="d044f-1524">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="d044f-1525">Zie het voorbeeld van een reactie in 12.3</span><span class="sxs-lookup"><span data-stu-id="d044f-1525">See a response example in 12.3</span></span>

### <a name="125-get-user-recommendations-for-active-build"></a><span data-ttu-id="d044f-1526">12.5.</span><span class="sxs-lookup"><span data-stu-id="d044f-1526">12.5.</span></span> <span data-ttu-id="d044f-1527">Gebruiker aanbevelingen krijgen (voor actieve build)</span><span class="sxs-lookup"><span data-stu-id="d044f-1527">Get User Recommendations (for active build)</span></span>
<span data-ttu-id="d044f-1528">Aanbevelingen van de gebruiker van een build van het type 'Aanbeveling' is gemarkeerd als actief build krijgen.</span><span class="sxs-lookup"><span data-stu-id="d044f-1528">Get user recommendations of a build of type "Recommendation" marked as active build.</span></span>

<span data-ttu-id="d044f-1529">Hallo API retourneert een lijst met voorspelde item op basis van de gebruiksgeschiedenis toohello van Hallo-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="d044f-1529">hello API will return a list of predicted item according toohello usage history of hello user.</span></span>

<span data-ttu-id="d044f-1530">Opmerkingen:</span><span class="sxs-lookup"><span data-stu-id="d044f-1530">Notes:</span></span> 

1. <span data-ttu-id="d044f-1531">Er is geen gebruiker aanbeveling voor FBT build.</span><span class="sxs-lookup"><span data-stu-id="d044f-1531">There is no user recommendation for FBT build.</span></span>
2. <span data-ttu-id="d044f-1532">Als het build-Hallo active is FBT deze methode wordt een foutmelding.</span><span class="sxs-lookup"><span data-stu-id="d044f-1532">If hello active build is FBT this method will returns an error.</span></span>

| <span data-ttu-id="d044f-1533">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-1533">HTTP Method</span></span> | <span data-ttu-id="d044f-1534">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-1534">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-1535">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="d044f-1535">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="d044f-1536">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d044f-1536">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="d044f-1537">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-1537">Parameter Name</span></span> | <span data-ttu-id="d044f-1538">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-1538">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-1539">Model</span><span class="sxs-lookup"><span data-stu-id="d044f-1539">modelId</span></span> |<span data-ttu-id="d044f-1540">De unieke id van het Hallo-model</span><span class="sxs-lookup"><span data-stu-id="d044f-1540">Unique identifier of hello model</span></span> |
| <span data-ttu-id="d044f-1541">Gebruikers-id</span><span class="sxs-lookup"><span data-stu-id="d044f-1541">userId</span></span> |<span data-ttu-id="d044f-1542">Unieke id van gebruiker Hallo</span><span class="sxs-lookup"><span data-stu-id="d044f-1542">Unique identifier of hello user</span></span> |
| <span data-ttu-id="d044f-1543">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="d044f-1543">numberOfResults</span></span> |<span data-ttu-id="d044f-1544">Aantal vereiste resultaten</span><span class="sxs-lookup"><span data-stu-id="d044f-1544">Number of required results</span></span> |
| <span data-ttu-id="d044f-1545">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="d044f-1545">includeMetatadata</span></span> |<span data-ttu-id="d044f-1546">Toekomstig gebruik, altijd Onwaar</span><span class="sxs-lookup"><span data-stu-id="d044f-1546">Future use, always false</span></span> |
| <span data-ttu-id="d044f-1547">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-1547">apiVersion</span></span> |<span data-ttu-id="d044f-1548">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-1548">1.0</span></span> |

<span data-ttu-id="d044f-1549">**Antwoord:**</span><span class="sxs-lookup"><span data-stu-id="d044f-1549">**Response:**</span></span>

<span data-ttu-id="d044f-1550">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-1550">HTTP Status code: 200</span></span>

<span data-ttu-id="d044f-1551">Hallo-antwoord bevat één vermelding per aanbevolen-item.</span><span class="sxs-lookup"><span data-stu-id="d044f-1551">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="d044f-1552">Elk item heeft Hallo gegevens te volgen:</span><span class="sxs-lookup"><span data-stu-id="d044f-1552">Each entry has hello following data:</span></span>

* <span data-ttu-id="d044f-1553">`Feed\entry\content\properties\Id`-Aanbevolen artikel-ID.</span><span class="sxs-lookup"><span data-stu-id="d044f-1553">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="d044f-1554">`Feed\entry\content\properties\Name`-De naam van het Hallo-item.</span><span class="sxs-lookup"><span data-stu-id="d044f-1554">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="d044f-1555">`Feed\entry\content\properties\Rating`-Classificatie van Hallo aanbeveling; hogere waarde betekent hogere betrouwbaarheid.</span><span class="sxs-lookup"><span data-stu-id="d044f-1555">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="d044f-1556">`Feed\entry\content\properties\Reasoning`-Aanbeveling redeneren (bijvoorbeeld aanbeveling uitleg).</span><span class="sxs-lookup"><span data-stu-id="d044f-1556">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="d044f-1557">Zie het voorbeeld van een reactie in 12.1</span><span class="sxs-lookup"><span data-stu-id="d044f-1557">See a response example in 12.1</span></span>

### <a name="126-get-user-recommendations-with-item-list-for-active-build"></a><span data-ttu-id="d044f-1558">12.6.</span><span class="sxs-lookup"><span data-stu-id="d044f-1558">12.6.</span></span> <span data-ttu-id="d044f-1559">Gebruiker aanbevelingen krijgen met de lijst met items (voor actieve build)</span><span class="sxs-lookup"><span data-stu-id="d044f-1559">Get User Recommendations with item list (for active build)</span></span>
<span data-ttu-id="d044f-1560">Ophalen van de aanbevelingen van de gebruiker van een build van het type 'Aanbeveling' is gemarkeerd als actief wordt gemaakt met een aanvullende lijst met items</span><span class="sxs-lookup"><span data-stu-id="d044f-1560">Get user recommendations of a build of type "Recommendation" marked as active build with an additional list of items</span></span>

<span data-ttu-id="d044f-1561">Hallo API retourneert een lijst met voorspelde item op basis van de gebruiksgeschiedenis toohello van Hallo gebruiker en Hallo extra items zijn opgegeven.</span><span class="sxs-lookup"><span data-stu-id="d044f-1561">hello API will return a list of predicted item according toohello usage history of hello user and hello additional provided items.</span></span>

<span data-ttu-id="d044f-1562">Opmerkingen:</span><span class="sxs-lookup"><span data-stu-id="d044f-1562">Notes:</span></span> 

1. <span data-ttu-id="d044f-1563">Er is geen gebruiker aanbeveling voor FBT build.</span><span class="sxs-lookup"><span data-stu-id="d044f-1563">There is no user recommendation for FBT build.</span></span>
2. <span data-ttu-id="d044f-1564">Als het build-Hallo active is FBT deze methode wordt een foutmelding.</span><span class="sxs-lookup"><span data-stu-id="d044f-1564">If hello active build is FBT this method will returns an error.</span></span>

| <span data-ttu-id="d044f-1565">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-1565">HTTP Method</span></span> | <span data-ttu-id="d044f-1566">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-1566">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-1567">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="d044f-1567">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="d044f-1568">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d044f-1568">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%2C1000%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="d044f-1569">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-1569">Parameter Name</span></span> | <span data-ttu-id="d044f-1570">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-1570">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-1571">Model</span><span class="sxs-lookup"><span data-stu-id="d044f-1571">modelId</span></span> |<span data-ttu-id="d044f-1572">De unieke id van het Hallo-model</span><span class="sxs-lookup"><span data-stu-id="d044f-1572">Unique identifier of hello model</span></span> |
| <span data-ttu-id="d044f-1573">Gebruikers-id</span><span class="sxs-lookup"><span data-stu-id="d044f-1573">userId</span></span> |<span data-ttu-id="d044f-1574">Unieke id van gebruiker Hallo</span><span class="sxs-lookup"><span data-stu-id="d044f-1574">Unique identifier of hello user</span></span> |
| <span data-ttu-id="d044f-1575">itemsIds</span><span class="sxs-lookup"><span data-stu-id="d044f-1575">itemsIds</span></span> |<span data-ttu-id="d044f-1576">Door komma's gescheiden lijst met Hallo items toorecommend voor.</span><span class="sxs-lookup"><span data-stu-id="d044f-1576">Comma-separated list of hello items toorecommend for.</span></span> <span data-ttu-id="d044f-1577">Maximale lengte: 1024</span><span class="sxs-lookup"><span data-stu-id="d044f-1577">Max length: 1024</span></span> |
| <span data-ttu-id="d044f-1578">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="d044f-1578">numberOfResults</span></span> |<span data-ttu-id="d044f-1579">Aantal vereiste resultaten</span><span class="sxs-lookup"><span data-stu-id="d044f-1579">Number of required results</span></span> |
| <span data-ttu-id="d044f-1580">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="d044f-1580">includeMetatadata</span></span> |<span data-ttu-id="d044f-1581">Toekomstig gebruik, altijd Onwaar</span><span class="sxs-lookup"><span data-stu-id="d044f-1581">Future use, always false</span></span> |
| <span data-ttu-id="d044f-1582">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-1582">apiVersion</span></span> |<span data-ttu-id="d044f-1583">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-1583">1.0</span></span> |

<span data-ttu-id="d044f-1584">**Antwoord:**</span><span class="sxs-lookup"><span data-stu-id="d044f-1584">**Response:**</span></span>

<span data-ttu-id="d044f-1585">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-1585">HTTP Status code: 200</span></span>

<span data-ttu-id="d044f-1586">Hallo-antwoord bevat één vermelding per aanbevolen-item.</span><span class="sxs-lookup"><span data-stu-id="d044f-1586">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="d044f-1587">Elk item heeft Hallo gegevens te volgen:</span><span class="sxs-lookup"><span data-stu-id="d044f-1587">Each entry has hello following data:</span></span>

* <span data-ttu-id="d044f-1588">`Feed\entry\content\properties\Id`-Aanbevolen artikel-ID.</span><span class="sxs-lookup"><span data-stu-id="d044f-1588">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="d044f-1589">`Feed\entry\content\properties\Name`-De naam van het Hallo-item.</span><span class="sxs-lookup"><span data-stu-id="d044f-1589">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="d044f-1590">`Feed\entry\content\properties\Rating`-Classificatie van Hallo aanbeveling; hogere waarde betekent hogere betrouwbaarheid.</span><span class="sxs-lookup"><span data-stu-id="d044f-1590">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="d044f-1591">`Feed\entry\content\properties\Reasoning`-Aanbeveling redeneren (bijvoorbeeld aanbeveling uitleg).</span><span class="sxs-lookup"><span data-stu-id="d044f-1591">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="d044f-1592">Zie het voorbeeld van een reactie in 12.1</span><span class="sxs-lookup"><span data-stu-id="d044f-1592">See a response example in 12.1</span></span>

### <a name="127-get-user-recommendations--of-a-specific-build"></a><span data-ttu-id="d044f-1593">12.7.</span><span class="sxs-lookup"><span data-stu-id="d044f-1593">12.7.</span></span> <span data-ttu-id="d044f-1594">Ophalen van de aanbevelingen van de gebruiker (van een specifieke build)</span><span class="sxs-lookup"><span data-stu-id="d044f-1594">Get User Recommendations  (of a specific build)</span></span>
<span data-ttu-id="d044f-1595">Aanbevelingen van de gebruiker van een specifieke build van het type 'Aanbeveling' krijgen.</span><span class="sxs-lookup"><span data-stu-id="d044f-1595">Get user recommendations of a specific build of type "Recommendation".</span></span>

<span data-ttu-id="d044f-1596">Hallo API retourneert een lijst met voorspelde item op basis van de gebruiksgeschiedenis toohello van Hallo gebruiker (gebruikt in een specifieke Hallo-build).</span><span class="sxs-lookup"><span data-stu-id="d044f-1596">hello API will return a list of predicted item according toohello usage history of hello user (used in hello specific build).</span></span>

<span data-ttu-id="d044f-1597">Opmerking: Er is geen gebruiker aanbeveling voor FBT build.</span><span class="sxs-lookup"><span data-stu-id="d044f-1597">Note: There is no user recommendation for FBT build.</span></span>

| <span data-ttu-id="d044f-1598">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-1598">HTTP Method</span></span> | <span data-ttu-id="d044f-1599">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-1599">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-1600">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="d044f-1600">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="d044f-1601">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d044f-1601">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| <span data-ttu-id="d044f-1602">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-1602">Parameter Name</span></span> | <span data-ttu-id="d044f-1603">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-1603">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-1604">Model</span><span class="sxs-lookup"><span data-stu-id="d044f-1604">modelId</span></span> |<span data-ttu-id="d044f-1605">De unieke id van het Hallo-model</span><span class="sxs-lookup"><span data-stu-id="d044f-1605">Unique identifier of hello model</span></span> |
| <span data-ttu-id="d044f-1606">Gebruikers-id</span><span class="sxs-lookup"><span data-stu-id="d044f-1606">userId</span></span> |<span data-ttu-id="d044f-1607">Unieke id van gebruiker Hallo</span><span class="sxs-lookup"><span data-stu-id="d044f-1607">Unique identifier of hello user</span></span> |
| <span data-ttu-id="d044f-1608">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="d044f-1608">numberOfResults</span></span> |<span data-ttu-id="d044f-1609">Aantal vereiste resultaten</span><span class="sxs-lookup"><span data-stu-id="d044f-1609">Number of required results</span></span> |
| <span data-ttu-id="d044f-1610">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="d044f-1610">includeMetatadata</span></span> |<span data-ttu-id="d044f-1611">Toekomstig gebruik, altijd Onwaar</span><span class="sxs-lookup"><span data-stu-id="d044f-1611">Future use, always false</span></span> |
| <span data-ttu-id="d044f-1612">buildId</span><span class="sxs-lookup"><span data-stu-id="d044f-1612">buildId</span></span> |<span data-ttu-id="d044f-1613">Hallo toouse id voor deze aanvraag aanbeveling bouwen</span><span class="sxs-lookup"><span data-stu-id="d044f-1613">hello build id toouse for this recommendation request</span></span> |
| <span data-ttu-id="d044f-1614">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-1614">apiVersion</span></span> |<span data-ttu-id="d044f-1615">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-1615">1.0</span></span> |

<span data-ttu-id="d044f-1616">**Antwoord:**</span><span class="sxs-lookup"><span data-stu-id="d044f-1616">**Response:**</span></span>

<span data-ttu-id="d044f-1617">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-1617">HTTP Status code: 200</span></span>

<span data-ttu-id="d044f-1618">Hallo-antwoord bevat één vermelding per aanbevolen-item.</span><span class="sxs-lookup"><span data-stu-id="d044f-1618">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="d044f-1619">Elk item heeft Hallo gegevens te volgen:</span><span class="sxs-lookup"><span data-stu-id="d044f-1619">Each entry has hello following data:</span></span>

* <span data-ttu-id="d044f-1620">`Feed\entry\content\properties\Id`-Aanbevolen artikel-ID.</span><span class="sxs-lookup"><span data-stu-id="d044f-1620">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="d044f-1621">`Feed\entry\content\properties\Name`-De naam van het Hallo-item.</span><span class="sxs-lookup"><span data-stu-id="d044f-1621">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="d044f-1622">`Feed\entry\content\properties\Rating`-Classificatie van Hallo aanbeveling; hogere waarde betekent hogere betrouwbaarheid.</span><span class="sxs-lookup"><span data-stu-id="d044f-1622">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="d044f-1623">`Feed\entry\content\properties\Reasoning`-Aanbeveling redeneren (bijvoorbeeld aanbeveling uitleg).</span><span class="sxs-lookup"><span data-stu-id="d044f-1623">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="d044f-1624">Zie het voorbeeld van een reactie in 12.1</span><span class="sxs-lookup"><span data-stu-id="d044f-1624">See a response example in 12.1</span></span>

### <a name="128-get-user-recommendations-with-item-list-of-a-specific-build"></a><span data-ttu-id="d044f-1625">12.8.</span><span class="sxs-lookup"><span data-stu-id="d044f-1625">12.8.</span></span> <span data-ttu-id="d044f-1626">Gebruiker aanbevelingen krijgen met itemlijst (van een specifieke build)</span><span class="sxs-lookup"><span data-stu-id="d044f-1626">Get User Recommendations with item list (of a specific build)</span></span>
<span data-ttu-id="d044f-1627">Aanbevelingen van de gebruiker van een specifieke versie van het type 'Aanbeveling' en Hallo-lijst van extra items ophalen.</span><span class="sxs-lookup"><span data-stu-id="d044f-1627">Get user recommendations of a specific build of type "Recommendation" and hello list of additional items.</span></span>

<span data-ttu-id="d044f-1628">Hallo API retourneert een lijst met voorspelde punt volgens de gebruiksgeschiedenis toohello van Hallo gebruiker en Hallo aanvullende lijst met items.</span><span class="sxs-lookup"><span data-stu-id="d044f-1628">hello API will return a list of predicted item according toohello usage history of hello user and hello additional list of items.</span></span>

<span data-ttu-id="d044f-1629">Opmerking: Ter is geen gebruiker aanbeveling voor FBT build.</span><span class="sxs-lookup"><span data-stu-id="d044f-1629">Note: Tthere is no user recommendation for FBT build.</span></span>

| <span data-ttu-id="d044f-1630">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-1630">HTTP Method</span></span> | <span data-ttu-id="d044f-1631">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-1631">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-1632">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="d044f-1632">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="d044f-1633">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d044f-1633">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| <span data-ttu-id="d044f-1634">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-1634">Parameter Name</span></span> | <span data-ttu-id="d044f-1635">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-1635">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-1636">Model</span><span class="sxs-lookup"><span data-stu-id="d044f-1636">modelId</span></span> |<span data-ttu-id="d044f-1637">De unieke id van het Hallo-model</span><span class="sxs-lookup"><span data-stu-id="d044f-1637">Unique identifier of hello model</span></span> |
| <span data-ttu-id="d044f-1638">Gebruikers-id</span><span class="sxs-lookup"><span data-stu-id="d044f-1638">userId</span></span> |<span data-ttu-id="d044f-1639">Unieke id van gebruiker Hallo</span><span class="sxs-lookup"><span data-stu-id="d044f-1639">Unique identifier of hello user</span></span> |
| <span data-ttu-id="d044f-1640">ItemID 's</span><span class="sxs-lookup"><span data-stu-id="d044f-1640">itemIds</span></span> |<span data-ttu-id="d044f-1641">Door komma's gescheiden lijst met Hallo items toorecommend voor.</span><span class="sxs-lookup"><span data-stu-id="d044f-1641">Comma-separated list of hello items toorecommend for.</span></span> <span data-ttu-id="d044f-1642">Maximale lengte: 1024</span><span class="sxs-lookup"><span data-stu-id="d044f-1642">Max length: 1024</span></span> |
| <span data-ttu-id="d044f-1643">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="d044f-1643">numberOfResults</span></span> |<span data-ttu-id="d044f-1644">Aantal vereiste resultaten</span><span class="sxs-lookup"><span data-stu-id="d044f-1644">Number of required results</span></span> |
| <span data-ttu-id="d044f-1645">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="d044f-1645">includeMetatadata</span></span> |<span data-ttu-id="d044f-1646">Toekomstig gebruik, altijd Onwaar</span><span class="sxs-lookup"><span data-stu-id="d044f-1646">Future use, always false</span></span> |
| <span data-ttu-id="d044f-1647">buildId</span><span class="sxs-lookup"><span data-stu-id="d044f-1647">buildId</span></span> |<span data-ttu-id="d044f-1648">Hallo toouse id voor deze aanvraag aanbeveling bouwen</span><span class="sxs-lookup"><span data-stu-id="d044f-1648">hello build id toouse for this recommendation request</span></span> |
| <span data-ttu-id="d044f-1649">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-1649">apiVersion</span></span> |<span data-ttu-id="d044f-1650">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-1650">1.0</span></span> |

<span data-ttu-id="d044f-1651">**Antwoord:**</span><span class="sxs-lookup"><span data-stu-id="d044f-1651">**Response:**</span></span>

<span data-ttu-id="d044f-1652">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-1652">HTTP Status code: 200</span></span>

<span data-ttu-id="d044f-1653">Hallo-antwoord bevat één vermelding per aanbevolen-item.</span><span class="sxs-lookup"><span data-stu-id="d044f-1653">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="d044f-1654">Elk item heeft Hallo gegevens te volgen:</span><span class="sxs-lookup"><span data-stu-id="d044f-1654">Each entry has hello following data:</span></span>

* <span data-ttu-id="d044f-1655">`Feed\entry\content\properties\Id`-Aanbevolen artikel-ID.</span><span class="sxs-lookup"><span data-stu-id="d044f-1655">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="d044f-1656">`Feed\entry\content\properties\Name`-De naam van het Hallo-item.</span><span class="sxs-lookup"><span data-stu-id="d044f-1656">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="d044f-1657">`Feed\entry\content\properties\Rating`-Classificatie van Hallo aanbeveling; hogere waarde betekent hogere betrouwbaarheid.</span><span class="sxs-lookup"><span data-stu-id="d044f-1657">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="d044f-1658">`Feed\entry\content\properties\Reasoning`-Aanbeveling redeneren (bijvoorbeeld aanbeveling uitleg).</span><span class="sxs-lookup"><span data-stu-id="d044f-1658">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="d044f-1659">Zie het voorbeeld van een reactie in 12.1</span><span class="sxs-lookup"><span data-stu-id="d044f-1659">See a response example in 12.1</span></span>

## <a name="13-user-usage-history"></a><span data-ttu-id="d044f-1660">13. Geschiedenis van de gebruiker</span><span class="sxs-lookup"><span data-stu-id="d044f-1660">13. User Usage History</span></span>
<span data-ttu-id="d044f-1661">Als een model aanbeveling is gebouwd kunnen Hallo tooretrieve Hallo geschiedenis van gebruikers (items gekoppeld tooa specifieke gebruiker) gebruikt voor Hallo build.</span><span class="sxs-lookup"><span data-stu-id="d044f-1661">Once a recommendation model was built hello system will allow tooretrieve hello user history (items associated tooa specific user) used for hello build.</span></span>
<span data-ttu-id="d044f-1662">Deze API geschiedenis van tooretrieve Hallo gebruikers toestaan</span><span class="sxs-lookup"><span data-stu-id="d044f-1662">This API allow tooretrieve hello user history</span></span>

<span data-ttu-id="d044f-1663">Opmerking: Hallo gebruikersgeschiedenis is momenteel alleen beschikbaar voor aanbeveling builds.</span><span class="sxs-lookup"><span data-stu-id="d044f-1663">Note: hello user history is currently available only for recommendation builds.</span></span>

### <a name="131-retrieve-user-history"></a><span data-ttu-id="d044f-1664">13,1 geschiedenis van gebruikers ophalen</span><span class="sxs-lookup"><span data-stu-id="d044f-1664">13.1 Retrieve user history</span></span>
<span data-ttu-id="d044f-1665">Ophalen Hallo lijst van item gebruikt in Hallo active bouwen of bouwen in Hallo opgegeven voor Hallo opgegeven gebruikers-id.</span><span class="sxs-lookup"><span data-stu-id="d044f-1665">Retrieve hello list of item used in hello active build or in hello specified build for hello given user id.</span></span>

| <span data-ttu-id="d044f-1666">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-1666">HTTP Method</span></span> | <span data-ttu-id="d044f-1667">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-1667">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-1668">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="d044f-1668">GET</span></span> |<span data-ttu-id="d044f-1669">Hallo gebruikersgeschiedenis voor actieve build Hallo niet ophalen.</span><span class="sxs-lookup"><span data-stu-id="d044f-1669">Get hello user history for hello active build.</span></span><br/>`<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&apiVersion=%271.0%27`<br/><br/><span data-ttu-id="d044f-1670">Hallo gebruikersgeschiedenis voor Hallo gegeven build ophalen`<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&buildId=<int>&apiVersion=%271.0%27`</span><span class="sxs-lookup"><span data-stu-id="d044f-1670">Get hello user history for hello given build `<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&buildId=<int>&apiVersion=%271.0%27`</span></span><br/><br/><span data-ttu-id="d044f-1671">Voorbeeld:`<rootURI>/GetUserHistory?modelId=%2727967136e8-f868-4258-9331-10d567f87fae%27&&userId=%27u_1013%27&apiVersion=%271.0%277`</span><span class="sxs-lookup"><span data-stu-id="d044f-1671">Example:`<rootURI>/GetUserHistory?modelId=%2727967136e8-f868-4258-9331-10d567f87fae%27&&userId=%27u_1013%27&apiVersion=%271.0%277`</span></span> |

| <span data-ttu-id="d044f-1672">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-1672">Parameter Name</span></span> | <span data-ttu-id="d044f-1673">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-1673">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-1674">Model</span><span class="sxs-lookup"><span data-stu-id="d044f-1674">modelId</span></span> |<span data-ttu-id="d044f-1675">Hallo unieke id van Hallo-model.</span><span class="sxs-lookup"><span data-stu-id="d044f-1675">hello unique identifier of hello model.</span></span> |
| <span data-ttu-id="d044f-1676">Gebruikers-id</span><span class="sxs-lookup"><span data-stu-id="d044f-1676">userId</span></span> |<span data-ttu-id="d044f-1677">unieke id van gebruiker Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="d044f-1677">hello unique identifier of hello user.</span></span> |
| <span data-ttu-id="d044f-1678">buildId</span><span class="sxs-lookup"><span data-stu-id="d044f-1678">buildId</span></span> |<span data-ttu-id="d044f-1679">optionele parameter, van welke versie Hallo gebruikersgeschiedenis ophalen moet tooindicate toestaan</span><span class="sxs-lookup"><span data-stu-id="d044f-1679">optional parameter, allow tooindicate from which build hello user history should be fetch</span></span> |
| <span data-ttu-id="d044f-1680">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-1680">apiVersion</span></span> |<span data-ttu-id="d044f-1681">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-1681">1.0</span></span> |

<span data-ttu-id="d044f-1682">**Antwoord:**</span><span class="sxs-lookup"><span data-stu-id="d044f-1682">**Response:**</span></span>

<span data-ttu-id="d044f-1683">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-1683">HTTP Status code: 200</span></span>

<span data-ttu-id="d044f-1684">Hallo-antwoord bevat één vermelding per aanbevolen-item.</span><span class="sxs-lookup"><span data-stu-id="d044f-1684">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="d044f-1685">Elk item heeft Hallo gegevens te volgen:</span><span class="sxs-lookup"><span data-stu-id="d044f-1685">Each entry has hello following data:</span></span>

* <span data-ttu-id="d044f-1686">`Feed\entry\content\properties\Id`-Aanbevolen artikel-ID.</span><span class="sxs-lookup"><span data-stu-id="d044f-1686">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="d044f-1687">`Feed\entry\content\properties\Name`-De naam van het Hallo-item.</span><span class="sxs-lookup"><span data-stu-id="d044f-1687">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="d044f-1688">`Feed\entry\content\properties\Rating`-N.V.T..</span><span class="sxs-lookup"><span data-stu-id="d044f-1688">`Feed\entry\content\properties\Rating` - N/A.</span></span>
* <span data-ttu-id="d044f-1689">`Feed\entry\content\properties\Reasoning`-N.V.T..</span><span class="sxs-lookup"><span data-stu-id="d044f-1689">`Feed\entry\content\properties\Reasoning` - N/A.</span></span>

<span data-ttu-id="d044f-1690">OData-XML</span><span class="sxs-lookup"><span data-stu-id="d044f-1690">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get User History</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2015-05-26T15:32:47Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">CatalogItemsThatContainATokenEntity</title>
        <updated>2015-05-26T15:32:47Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:Id>
                <d:Name m:type="Edm.String">Clara Callan</d:Name>
                <d:Rating m:type="Edm.Double">0</d:Rating>
                <d:Reasoning m:type="Edm.String"/>
                <d:Metadata m:type="Edm.String"/>
                <d:FormattedRating m:type="Edm.Double" m:null="true"/>
            </m:properties>
        </content>
    </entry>
</feed>

## <a name="14-notifications"></a><span data-ttu-id="d044f-1691">14. Meldingen</span><span class="sxs-lookup"><span data-stu-id="d044f-1691">14. Notifications</span></span>
<span data-ttu-id="d044f-1692">Azure Machine Learning aanbevelingen meldingen worden gegenereerd als permanente fouten in Hallo-systeem optreden.</span><span class="sxs-lookup"><span data-stu-id="d044f-1692">Azure Machine Learning Recommendations creates notifications when persistent errors happen in hello system.</span></span> <span data-ttu-id="d044f-1693">Er zijn 3 soorten meldingen:</span><span class="sxs-lookup"><span data-stu-id="d044f-1693">There are 3 types of notifications:</span></span>

1. <span data-ttu-id="d044f-1694">Fout bij build - deze melding wordt geactiveerd voor elke build-fout.</span><span class="sxs-lookup"><span data-stu-id="d044f-1694">Build failure - This notification is triggered for every build failure.</span></span>
2. <span data-ttu-id="d044f-1695">Gegevens overname verwerkingsfout - deze melding wordt geactiveerd wanneer we meer dan 100 fouten in de Hallo laatste vijf minuten in Hallo verwerking van gebruiksgebeurtenissen per model hebben.</span><span class="sxs-lookup"><span data-stu-id="d044f-1695">Data acquisition processing failure - This notification is triggered when we have more than 100 errors in hello last 5 minutes in hello processing of usage events per model.</span></span>
3. <span data-ttu-id="d044f-1696">Aanbeveling verbruik mislukt - deze melding wordt geactiveerd wanneer we meer dan 100 fouten in de Hallo laatste vijf minuten in Hallo verwerking van aanvragen van de aanbeveling per model hebben.</span><span class="sxs-lookup"><span data-stu-id="d044f-1696">Recommendation consumption failure - This notification is triggered when we have more than 100 errors in hello last 5 minutes in hello processing of recommendation requests per model.</span></span>

### <a name="141-get-notifications"></a><span data-ttu-id="d044f-1697">14.1.</span><span class="sxs-lookup"><span data-stu-id="d044f-1697">14.1.</span></span> <span data-ttu-id="d044f-1698">Meldingen ophalen</span><span class="sxs-lookup"><span data-stu-id="d044f-1698">Get Notifications</span></span>
<span data-ttu-id="d044f-1699">Hiermee haalt u alle Hallo meldingen voor alle modellen of voor een enkelvoudig model.</span><span class="sxs-lookup"><span data-stu-id="d044f-1699">Retrieves all hello notifications for all models or for a single model.</span></span>

| <span data-ttu-id="d044f-1700">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-1700">HTTP Method</span></span> | <span data-ttu-id="d044f-1701">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-1701">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-1702">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="d044f-1702">GET</span></span> |`<rootURI>/GetNotifications?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="d044f-1703">Alle meldingen voor alle modellen ophalen:</span><span class="sxs-lookup"><span data-stu-id="d044f-1703">Getting all notifications for all models:</span></span><br>`<rootURI>/GetNotifications?apiVersion=%271.0%27`<br><br><span data-ttu-id="d044f-1704">Voorbeeld voor het ophalen van meldingen voor een bepaald model:</span><span class="sxs-lookup"><span data-stu-id="d044f-1704">Example for getting notifications for a specific model:</span></span><br>`<rootURI>/GetNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%277` |

| <span data-ttu-id="d044f-1705">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-1705">Parameter Name</span></span> | <span data-ttu-id="d044f-1706">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-1706">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-1707">Model</span><span class="sxs-lookup"><span data-stu-id="d044f-1707">modelId</span></span> |<span data-ttu-id="d044f-1708">Een optionele parameter.</span><span class="sxs-lookup"><span data-stu-id="d044f-1708">Optional parameter.</span></span> <span data-ttu-id="d044f-1709">Wanneer u dit weglaat, krijgt u alle meldingen voor alle modellen.</span><span class="sxs-lookup"><span data-stu-id="d044f-1709">When omitted, you will get all notifications for all models.</span></span> <br><span data-ttu-id="d044f-1710">Geldige waarde: de unieke id van het Hallo-model.</span><span class="sxs-lookup"><span data-stu-id="d044f-1710">Valid value: unique identifier of hello model.</span></span> |
| <span data-ttu-id="d044f-1711">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-1711">apiVersion</span></span> |<span data-ttu-id="d044f-1712">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-1712">1.0</span></span> |
|  | |
| <span data-ttu-id="d044f-1713">Aanvraagtekst</span><span class="sxs-lookup"><span data-stu-id="d044f-1713">Request Body</span></span> |<span data-ttu-id="d044f-1714">GEEN</span><span class="sxs-lookup"><span data-stu-id="d044f-1714">NONE</span></span> |

<span data-ttu-id="d044f-1715">**Antwoord:**</span><span class="sxs-lookup"><span data-stu-id="d044f-1715">**Response:**</span></span>

<span data-ttu-id="d044f-1716">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-1716">HTTP Status code: 200</span></span>

<span data-ttu-id="d044f-1717">OData-XML</span><span class="sxs-lookup"><span data-stu-id="d044f-1717">OData XML</span></span>

    hello response includes one entry per notification. Each entry has hello following data:
        * feed\entry\content\properties\UserName - Internal user name identification.
        * feed\entry\content\properties\ModelId - Model ID.
        * feed\entry\content\properties\Message - Notification message.
        * feed\entry\content\properties\DateCreated - Date that this notification was created in UTC format.
        * feed\entry\content\properties\NotificationType - Notification types. Values are BuildFailure, RecommendationFailure, and DataAquisitionFailure.

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get a list of Notifications for a user</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-04T13:24:23Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'" />
        <entry>
                <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfNotificationsForAUserEntity</title>
            <updated>2014-11-04T13:24:23Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:UserName m:type="Edm.String">515506bc-3693-4dce-a5e2-81cb3e8efb56@dm.com</d:UserName>
                    <d:ModelId m:type="Edm.String">967136e8-f868-4258-9331-10d567f87fae</d:ModelId>
                    <d:Message m:type="Edm.String">Build failed for user</d:Message>
                    <d:DateCreated m:type="Edm.String">2014-11-04T13:23:14.383</d:DateCreated>
                    <d:NotificationType m:type="Edm.String">BuildFailure</d:NotificationType>
                </m:properties>
            </content>
        </entry>
    </feed>

### <a name="142-delete-model-notifications"></a><span data-ttu-id="d044f-1718">14.2.</span><span class="sxs-lookup"><span data-stu-id="d044f-1718">14.2.</span></span> <span data-ttu-id="d044f-1719">Model meldingen verwijderen</span><span class="sxs-lookup"><span data-stu-id="d044f-1719">Delete Model Notifications</span></span>
<span data-ttu-id="d044f-1720">Hiermee verwijdert u alle lezen meldingen voor een model.</span><span class="sxs-lookup"><span data-stu-id="d044f-1720">Deletes all read notifications for a model.</span></span>

| <span data-ttu-id="d044f-1721">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-1721">HTTP Method</span></span> | <span data-ttu-id="d044f-1722">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-1722">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-1723">VERWIJDEREN</span><span class="sxs-lookup"><span data-stu-id="d044f-1723">DELETE</span></span> |`<rootURI>/DeleteModelNotifications?modelId=%<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="d044f-1724">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d044f-1724">Example:</span></span><br>`<rootURI>/DeleteModelNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%27` |

| <span data-ttu-id="d044f-1725">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-1725">Parameter Name</span></span> | <span data-ttu-id="d044f-1726">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-1726">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-1727">Model</span><span class="sxs-lookup"><span data-stu-id="d044f-1727">modelId</span></span> |<span data-ttu-id="d044f-1728">De unieke id van het Hallo-model</span><span class="sxs-lookup"><span data-stu-id="d044f-1728">Unique identifier of hello model</span></span> |
| <span data-ttu-id="d044f-1729">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-1729">apiVersion</span></span> |<span data-ttu-id="d044f-1730">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-1730">1.0</span></span> |
|  | |
| <span data-ttu-id="d044f-1731">Aanvraagtekst</span><span class="sxs-lookup"><span data-stu-id="d044f-1731">Request Body</span></span> |<span data-ttu-id="d044f-1732">GEEN</span><span class="sxs-lookup"><span data-stu-id="d044f-1732">NONE</span></span> |

<span data-ttu-id="d044f-1733">**Antwoord**:</span><span class="sxs-lookup"><span data-stu-id="d044f-1733">**Response**:</span></span>

<span data-ttu-id="d044f-1734">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-1734">HTTP Status code: 200</span></span>

### <a name="143-delete-user-notifications"></a><span data-ttu-id="d044f-1735">14.3.</span><span class="sxs-lookup"><span data-stu-id="d044f-1735">14.3.</span></span> <span data-ttu-id="d044f-1736">Meldingen voor gebruikers verwijderen</span><span class="sxs-lookup"><span data-stu-id="d044f-1736">Delete User Notifications</span></span>
<span data-ttu-id="d044f-1737">Hiermee verwijdert u alle meldingen voor alle modellen.</span><span class="sxs-lookup"><span data-stu-id="d044f-1737">Deletes all notifications for all models.</span></span>

| <span data-ttu-id="d044f-1738">HTTP-methode</span><span class="sxs-lookup"><span data-stu-id="d044f-1738">HTTP Method</span></span> | <span data-ttu-id="d044f-1739">URI</span><span class="sxs-lookup"><span data-stu-id="d044f-1739">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-1740">VERWIJDEREN</span><span class="sxs-lookup"><span data-stu-id="d044f-1740">DELETE</span></span> |`<rootURI>/DeleteUserNotifications?apiVersion=%271.0%27` |

| <span data-ttu-id="d044f-1741">Parameternaam</span><span class="sxs-lookup"><span data-stu-id="d044f-1741">Parameter Name</span></span> | <span data-ttu-id="d044f-1742">Geldige waarden</span><span class="sxs-lookup"><span data-stu-id="d044f-1742">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="d044f-1743">apiVersion</span><span class="sxs-lookup"><span data-stu-id="d044f-1743">apiVersion</span></span> |<span data-ttu-id="d044f-1744">1.0</span><span class="sxs-lookup"><span data-stu-id="d044f-1744">1.0</span></span> |
|  | |
| <span data-ttu-id="d044f-1745">Aanvraagtekst</span><span class="sxs-lookup"><span data-stu-id="d044f-1745">Request Body</span></span> |<span data-ttu-id="d044f-1746">GEEN</span><span class="sxs-lookup"><span data-stu-id="d044f-1746">NONE</span></span> |

<span data-ttu-id="d044f-1747">**Antwoord**:</span><span class="sxs-lookup"><span data-stu-id="d044f-1747">**Response**:</span></span>

<span data-ttu-id="d044f-1748">HTTP-statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="d044f-1748">HTTP Status code: 200</span></span>

## <a name="15-legal"></a><span data-ttu-id="d044f-1749">15. Juridische informatie</span><span class="sxs-lookup"><span data-stu-id="d044f-1749">15. Legal</span></span>
<span data-ttu-id="d044f-1750">Dit document wordt geleverd ' as-is '.</span><span class="sxs-lookup"><span data-stu-id="d044f-1750">This document is provided “as-is”.</span></span> <span data-ttu-id="d044f-1751">Informatie en inzichten die in dit document, inclusief URL's en andere websiteverwijzingen, kunnen zonder kennisgeving worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="d044f-1751">Information and views expressed in this document, including URL and other Internet Web site references, may change without notice.</span></span><br><br>
<span data-ttu-id="d044f-1752">Enkele voorbeelden die hierin staan zijn uitsluitend ter illustratie en zijn fictief.</span><span class="sxs-lookup"><span data-stu-id="d044f-1752">Some examples depicted herein are provided for illustration only and are fictitious.</span></span> <span data-ttu-id="d044f-1753">Er is geen echte verwantschap of relatie is bedoeld of moet worden afgeleid.</span><span class="sxs-lookup"><span data-stu-id="d044f-1753">No real association or connection is intended or should be inferred.</span></span><br><br>
<span data-ttu-id="d044f-1754">Dit document biedt geen u enkel wettelijk recht tooany intellectueel eigendom in een Microsoft-product.</span><span class="sxs-lookup"><span data-stu-id="d044f-1754">This document does not provide you with any legal rights tooany intellectual property in any Microsoft product.</span></span> <span data-ttu-id="d044f-1755">U kunt kopiëren en het gebruik van dit document voor eigen referentiedoeleinden.</span><span class="sxs-lookup"><span data-stu-id="d044f-1755">You may copy and use this document for your internal, reference purposes.</span></span><br><br>
<span data-ttu-id="d044f-1756">© 2015 Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d044f-1756">© 2015 Microsoft.</span></span> <span data-ttu-id="d044f-1757">Alle rechten voorbehouden.</span><span class="sxs-lookup"><span data-stu-id="d044f-1757">All rights reserved.</span></span>

