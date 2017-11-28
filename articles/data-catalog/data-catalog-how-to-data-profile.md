---
title: aaaHow tooData profiel gegevensbronnen
description: Hoe-tooarticle hoe tooinclude tabel - en op kolomniveau gegevens bij het registreren van gegevensbronnen in Azure Data Catalog profielen en hoe gegevens toouse toounderstand gegevensbronnen profielen is gemarkeerd.
services: data-catalog
documentationcenter: 
author: spelluru
manager: NA
editor: 
tags: 
ms.assetid: 94a8274b-5c9c-4962-a4b1-2fed38a3d919
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: 12c9f38501cdaee903d0dcbbdd0b82395f35a187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="data-profile-data-sources"></a><span data-ttu-id="b5397-103">Gegevensbronnen met gegevensprofielen</span><span class="sxs-lookup"><span data-stu-id="b5397-103">Data profile data sources</span></span>
## <a name="introduction"></a><span data-ttu-id="b5397-104">Inleiding</span><span class="sxs-lookup"><span data-stu-id="b5397-104">Introduction</span></span>
<span data-ttu-id="b5397-105">**Microsoft Azure Data Catalog** is een volledig beheerde cloudservice die als een systeem van registratie en systeem van detectie voor zakelijke gegevensbronnen fungeert.</span><span class="sxs-lookup"><span data-stu-id="b5397-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="b5397-106">Met andere woorden, **Azure Data Catalog** wordt alle informatie over mensen helpen detecteren, begrijpen en gebruiken van gegevensbronnen en helpt organisaties tooget meer waarde van hun bestaande gegevens.</span><span class="sxs-lookup"><span data-stu-id="b5397-106">In other words, **Azure Data Catalog** is all about helping people discover, understand, and use data sources, and helping organizations tooget more value from their existing data.</span></span> <span data-ttu-id="b5397-107">Wanneer een gegevensbron is geregistreerd met **Azure Data Catalog**, de metagegevens wordt gekopieerd en geïndexeerd door Hallo-service, maar Hallo verhaal er eindigt niet.</span><span class="sxs-lookup"><span data-stu-id="b5397-107">When a data source is registered with **Azure Data Catalog**, its metadata is copied and indexed by hello service, but hello story doesn’t end there.</span></span>

<span data-ttu-id="b5397-108">Hallo **gegevens profilering** functie van **Azure Data Catalog** Hallo gegevens van ondersteunde gegevensbronnen in de catalogus worden gecontroleerd en verzamelt statistische gegevens en informatie over die gegevens.</span><span class="sxs-lookup"><span data-stu-id="b5397-108">hello **Data Profiling** feature of **Azure Data Catalog** examines hello data from supported data sources in your catalog and collects statistics and information about that data.</span></span> <span data-ttu-id="b5397-109">Het is gemakkelijk tooinclude een profiel van de activa van uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="b5397-109">It's easy tooinclude a profile of your data assets.</span></span> <span data-ttu-id="b5397-110">Wanneer u een gegevensasset registreert, kies **gegevens profiel opnemen** in hulpprogramma voor registratie van gegevensbronnen Hallo.</span><span class="sxs-lookup"><span data-stu-id="b5397-110">When you register a data asset, choose **Include Data Profile** in hello data source registration tool.</span></span>

## <a name="what-is-data-profiling"></a><span data-ttu-id="b5397-111">Wat is profileren van gegevens</span><span class="sxs-lookup"><span data-stu-id="b5397-111">What is Data Profiling</span></span>
<span data-ttu-id="b5397-112">Profileren van gegevens onderzoekt Hallo-gegevens in het Hallo-gegevensbron wordt geregistreerd en verzamelt statistische gegevens en informatie over die gegevens.</span><span class="sxs-lookup"><span data-stu-id="b5397-112">Data profiling examines hello data in hello data source being registered, and collects statistics and information about that data.</span></span> <span data-ttu-id="b5397-113">Tijdens de detectie van gegevensbron kunt deze statistische gegevens u bepalen Hallo geschiktheid van Hallo gegevens toosolve het zakelijke probleem.</span><span class="sxs-lookup"><span data-stu-id="b5397-113">During data source discovery, these statistics can help you determine hello suitability of hello data toosolve their business problem.</span></span>

<!-- In [How toodiscover data sources](data-catalog-how-to-discover.md), you learn about **Azure Data Catalog's** extensive search capabilities including searching for data assets that have a profile. See [How tooinclude a data profile when registering a data source](#howto). -->

<span data-ttu-id="b5397-114">Hallo ondersteunen volgende gegevensbronnen gegevens samenstellen van profiel:</span><span class="sxs-lookup"><span data-stu-id="b5397-114">hello following data sources support data profiling:</span></span>

* <span data-ttu-id="b5397-115">SQL Server (inclusief Azure SQL DB en Azure SQL Data Warehouse)-tabellen en weergaven</span><span class="sxs-lookup"><span data-stu-id="b5397-115">SQL Server (including Azure SQL DB and Azure SQL Data Warehouse) tables and views</span></span>
* <span data-ttu-id="b5397-116">Oracle-tabellen en weergaven</span><span class="sxs-lookup"><span data-stu-id="b5397-116">Oracle tables and views</span></span>
* <span data-ttu-id="b5397-117">Teradata-tabellen en weergaven</span><span class="sxs-lookup"><span data-stu-id="b5397-117">Teradata tables and views</span></span>
* <span data-ttu-id="b5397-118">Hive-tabellen</span><span class="sxs-lookup"><span data-stu-id="b5397-118">Hive tables</span></span>

<span data-ttu-id="b5397-119">Inclusief gegevens profielen wanneer gebruikers voor het registreren van gegevensassets helpt beantwoorden vragen over gegevensbronnen, waaronder:</span><span class="sxs-lookup"><span data-stu-id="b5397-119">Including data profiles when registering data assets helps users answer questions about data sources, including:</span></span>

* <span data-ttu-id="b5397-120">Deze kunnen worden gebruikt toosolve mijn zakelijke probleem?</span><span class="sxs-lookup"><span data-stu-id="b5397-120">Can it be used toosolve my business problem?</span></span>
* <span data-ttu-id="b5397-121">Voldoet Hallo gegevens tooparticular standaarden of patronen?</span><span class="sxs-lookup"><span data-stu-id="b5397-121">Does hello data conform tooparticular standards or patterns?</span></span>
* <span data-ttu-id="b5397-122">Wat zijn enkele Hallo afwijkingen van de gegevensbron Hallo?</span><span class="sxs-lookup"><span data-stu-id="b5397-122">What are some of hello anomalies of hello data source?</span></span>
* <span data-ttu-id="b5397-123">Wat zijn mogelijk uitdagingen bij het integreren van deze gegevens in mijn toepassing?</span><span class="sxs-lookup"><span data-stu-id="b5397-123">What are possible challenges of integrating this data into my application?</span></span>

> [!NOTE]
> <span data-ttu-id="b5397-124">U kunt ook de documentatie bij tooan asset toodescribe hoe gegevens kan worden geïntegreerd in een toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b5397-124">You can also add documentation tooan asset toodescribe how data could be integrated into an application.</span></span> <span data-ttu-id="b5397-125">Zie [hoe gegevensbronnen toodocument](data-catalog-how-to-documentation.md).</span><span class="sxs-lookup"><span data-stu-id="b5397-125">See [How toodocument data sources](data-catalog-how-to-documentation.md).</span></span>
>
>

<a name="howto"/>

## <a name="how-tooinclude-a-data-profile-when-registering-a-data-source"></a><span data-ttu-id="b5397-126">Hoe tooinclude data profiel bij het registreren van een gegevensbron</span><span class="sxs-lookup"><span data-stu-id="b5397-126">How tooinclude a data profile when registering a data source</span></span>
<span data-ttu-id="b5397-127">Het is gemakkelijk tooinclude een profiel van de gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="b5397-127">It's easy tooinclude a profile of your data source.</span></span> <span data-ttu-id="b5397-128">Wanneer u een gegevensbron registreren in Hallo **objecten toobe geregistreerd** Configuratiescherm van de registratie van gegevensbron Hallo hulpprogramma, kiest u **gegevens profiel opnemen**.</span><span class="sxs-lookup"><span data-stu-id="b5397-128">When you register a data source, in hello **Objects toobe registered** panel of hello data source registration tool, choose **Include Data Profile**.</span></span>

![](media/data-catalog-data-profile/data-catalog-register-profile.png)

<span data-ttu-id="b5397-129">toolearn informatie over hoe tooregister gegevensbronnen, Zie [hoe gegevensbronnen tooregister](data-catalog-how-to-register.md) en [aan de slag met Azure Data Catalog](data-catalog-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b5397-129">toolearn more about how tooregister data sources, see [How tooregister data sources](data-catalog-how-to-register.md) and [Get started with Azure Data Catalog](data-catalog-get-started.md).</span></span>

## <a name="filtering-on-data-assets-that-include-data-profiles"></a><span data-ttu-id="b5397-130">Filteren op gegevensassets die gegevens profielen bevatten</span><span class="sxs-lookup"><span data-stu-id="b5397-130">Filtering on data assets that include data profiles</span></span>
<span data-ttu-id="b5397-131">gegevensassets toodiscover die een profiel van de gegevens bevatten, die u kunt opnemen `has:tableDataProfiles` of `has:columnsDataProfiles` als een van de zoektermen.</span><span class="sxs-lookup"><span data-stu-id="b5397-131">toodiscover data assets that include a data profile, you can include `has:tableDataProfiles` or `has:columnsDataProfiles` as one of your search terms.</span></span>

> [!NOTE]
> <span data-ttu-id="b5397-132">Selecteren **gegevens profiel opnemen** in Hallo gegevens bevat hulpprogramma voor registratie tabel en profielgegevens op kolomniveau.</span><span class="sxs-lookup"><span data-stu-id="b5397-132">Selecting **Include Data Profile** in hello data source registration tool includes both table and column-level profile information.</span></span> <span data-ttu-id="b5397-133">Hallo kunnen API van Data Catalog echter gegevens activa toobe geregistreerd met slechts één set met profielgegevens opgenomen.</span><span class="sxs-lookup"><span data-stu-id="b5397-133">However, hello Data Catalog API allows data assets toobe registered with only one set of profile information included.</span></span>
>
>

## <a name="viewing-data-profile-information"></a><span data-ttu-id="b5397-134">Data-profielgegevens weergeven</span><span class="sxs-lookup"><span data-stu-id="b5397-134">Viewing data profile information</span></span>
<span data-ttu-id="b5397-135">Als u een geschikte gegevensbron aan een profiel hebt gevonden, kunt u gegevens uit het profiel Hallo gegevens kunt weergeven.</span><span class="sxs-lookup"><span data-stu-id="b5397-135">Once you find a suitable data source with a profile, you can view hello data profile details.</span></span> <span data-ttu-id="b5397-136">tooview hello gegevens profiel, selecteert u een gegevensasset en kiest u **gegevens profiel** Hallo Data Catalog-portal-venster.</span><span class="sxs-lookup"><span data-stu-id="b5397-136">tooview hello data profile, select a data asset and choose **Data Profile** in hello Data Catalog portal window.</span></span>

![](media/data-catalog-data-profile/data-catalog-view.png)

<span data-ttu-id="b5397-137">Een profiel van de gegevens in **Azure Data Catalog** toont tabel en de kolom profiel informatie zoals:</span><span class="sxs-lookup"><span data-stu-id="b5397-137">A data profile in **Azure Data Catalog** shows table and column profile information including:</span></span>

### <a name="object-data-profile"></a><span data-ttu-id="b5397-138">Object gegevens profiel</span><span class="sxs-lookup"><span data-stu-id="b5397-138">Object data profile</span></span>
* <span data-ttu-id="b5397-139">Aantal rijen</span><span class="sxs-lookup"><span data-stu-id="b5397-139">Number of rows</span></span>
* <span data-ttu-id="b5397-140">De tabelgrootte van de</span><span class="sxs-lookup"><span data-stu-id="b5397-140">Table size</span></span>
* <span data-ttu-id="b5397-141">Wanneer Hallo-object voor het laatst is bijgewerkt</span><span class="sxs-lookup"><span data-stu-id="b5397-141">When hello object was last updated</span></span>

### <a name="column-data-profile"></a><span data-ttu-id="b5397-142">Kolom gegevens profiel</span><span class="sxs-lookup"><span data-stu-id="b5397-142">Column data profile</span></span>
* <span data-ttu-id="b5397-143">Gegevenstype van kolom</span><span class="sxs-lookup"><span data-stu-id="b5397-143">Column data type</span></span>
* <span data-ttu-id="b5397-144">Aantal afzonderlijke waarden</span><span class="sxs-lookup"><span data-stu-id="b5397-144">Number of distinct values</span></span>
* <span data-ttu-id="b5397-145">Aantal rijen met NULL-waarden</span><span class="sxs-lookup"><span data-stu-id="b5397-145">Number of rows with NULL values</span></span>
* <span data-ttu-id="b5397-146">Minimum, maximum, gemiddelde en standaarddeviatie voor kolomwaarden</span><span class="sxs-lookup"><span data-stu-id="b5397-146">Minimum, maximum, average, and standard deviation for column values</span></span>

## <a name="summary"></a><span data-ttu-id="b5397-147">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="b5397-147">Summary</span></span>
<span data-ttu-id="b5397-148">Profileren van gegevens voorziet in statistieken en informatie over gegevens activa toohelp u Hallo geschiktheid van Hallo gegevens toosolve zakelijke problemen vaststellen geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="b5397-148">Data profiling provides statistics and information about registered data assets toohelp you determine hello suitability of hello data toosolve business problems.</span></span> <span data-ttu-id="b5397-149">Samen met aantekeningen maken en gegevensbronnen documenteren, kunnen profielen van de gegevens gebruikers geven een beter begrip van uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="b5397-149">Along with annotating, and documenting data sources, data profiles can give users a deeper understanding of your data.</span></span>

## <a name="see-also"></a><span data-ttu-id="b5397-150">Zie ook</span><span class="sxs-lookup"><span data-stu-id="b5397-150">See Also</span></span>
* [<span data-ttu-id="b5397-151">Hoe tooregister gegevensbronnen</span><span class="sxs-lookup"><span data-stu-id="b5397-151">How tooregister data sources</span></span>](data-catalog-how-to-register.md)
* [<span data-ttu-id="b5397-152">Aan de slag met Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="b5397-152">Get started with Azure Data Catalog</span></span>](data-catalog-get-started.md)
