---
title: aaaHow toouse Fiddler tooevaluate en Azure Search REST-API's testen | Microsoft Docs
description: Gebruik Fiddler om de beschikbaarheid van een benadering code gratis tooverifying Azure Search en uitprobeert Hallo REST-API's.
services: search
documentationcenter: 
author: HeidiSteen
manager: mblythe
editor: 
ms.assetid: 790e5779-c6a3-4a07-9d1e-d6739e6b87d2
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: heidist
ms.openlocfilehash: 2912e1180717d7b40a1e4f7f7f00daf2cc254f0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-fiddler-tooevaluate-and-test-azure-search-rest-apis"></a><span data-ttu-id="b9660-103">Gebruik Fiddler tooevaluate en testen van Azure Search REST-API 's</span><span class="sxs-lookup"><span data-stu-id="b9660-103">Use Fiddler tooevaluate and test Azure Search REST APIs</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="b9660-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="b9660-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="b9660-105">Search Explorer</span><span class="sxs-lookup"><span data-stu-id="b9660-105">Search Explorer</span></span>](search-explorer.md)
> * [<span data-ttu-id="b9660-106">Fiddler</span><span class="sxs-lookup"><span data-stu-id="b9660-106">Fiddler</span></span>](search-fiddler.md)
> * [<span data-ttu-id="b9660-107">.NET</span><span class="sxs-lookup"><span data-stu-id="b9660-107">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="b9660-108">REST</span><span class="sxs-lookup"><span data-stu-id="b9660-108">REST</span></span>](search-query-rest-api.md)
>
>

<span data-ttu-id="b9660-109">Dit artikel wordt uitgelegd hoe toouse Fiddler, beschikbaar als een [gratis download via Telerik](http://www.telerik.com/fiddler), tooissue HTTP-aanvragen tooand antwoorden weergeven met behulp van hello Azure Search REST API, zonder toowrite code.</span><span class="sxs-lookup"><span data-stu-id="b9660-109">This article explains how toouse Fiddler, available as a [free download from Telerik](http://www.telerik.com/fiddler), tooissue HTTP requests tooand view responses using hello Azure Search REST API, without having toowrite any code.</span></span> <span data-ttu-id="b9660-110">Azure Search is een volledig beheerde, gehoste Microsoft Azure-service voor zoeken in de cloud. De service is eenvoudig programmeerbaar via .NET en REST API's.</span><span class="sxs-lookup"><span data-stu-id="b9660-110">Azure Search is fully-managed, hosted cloud search service on Microsoft Azure, easily programmable through .NET and REST APIs.</span></span> <span data-ttu-id="b9660-111">Hello Azure Search service REST-API's zijn beschreven op [MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx).</span><span class="sxs-lookup"><span data-stu-id="b9660-111">hello Azure Search service REST APIs are documented on [MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx).</span></span>

<span data-ttu-id="b9660-112">In de Hallo stappen te volgen, hebt u een index maken, uploaden van documenten, query Hallo index en query Hallo systeem om servicegegevens te zoeken.</span><span class="sxs-lookup"><span data-stu-id="b9660-112">In hello following steps, you'll create an index, upload documents, query hello index, and then query hello system for service information.</span></span>

<span data-ttu-id="b9660-113">toocomplete deze stappen, moet u een Azure Search-service en `api-key`.</span><span class="sxs-lookup"><span data-stu-id="b9660-113">toocomplete these steps, you will need an Azure Search service and `api-key`.</span></span> <span data-ttu-id="b9660-114">Zie [maken van een Azure Search-service in Hallo portal](search-create-service-portal.md) voor instructies over hoe tooget gestart.</span><span class="sxs-lookup"><span data-stu-id="b9660-114">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for instructions on how tooget started.</span></span>

## <a name="create-an-index"></a><span data-ttu-id="b9660-115">Een index maken</span><span class="sxs-lookup"><span data-stu-id="b9660-115">Create an index</span></span>
1. <span data-ttu-id="b9660-116">Start Fiddler.</span><span class="sxs-lookup"><span data-stu-id="b9660-116">Start Fiddler.</span></span> <span data-ttu-id="b9660-117">Op Hallo **bestand** menu uitschakelen **verkeer vastleggen** toohide HTTP-activiteit die geen verband toohello huidige taak.</span><span class="sxs-lookup"><span data-stu-id="b9660-117">On hello **File** menu, turn off **Capture Traffic** toohide extraneous HTTP activity that is unrelated toohello current task.</span></span>
2. <span data-ttu-id="b9660-118">Op Hallo **Composer** tabblad formuleert u een aanvraag dat lijkt op Hallo volgende schermopname.</span><span class="sxs-lookup"><span data-stu-id="b9660-118">On hello **Composer** tab, you'll formulate a request that looks like hello following screen shot.</span></span>

      ![][1]
3. <span data-ttu-id="b9660-119">Selecteer **PUT**.</span><span class="sxs-lookup"><span data-stu-id="b9660-119">Select **PUT**.</span></span>
4. <span data-ttu-id="b9660-120">Voer een URL waarmee Hallo service-URL, Aanvraagkenmerken en Hallo api-versie.</span><span class="sxs-lookup"><span data-stu-id="b9660-120">Enter a URL that specifies hello service URL, request attributes, and hello api-version.</span></span> <span data-ttu-id="b9660-121">Enkele aanwijzers tookeep rekening:</span><span class="sxs-lookup"><span data-stu-id="b9660-121">A few pointers tookeep in mind:</span></span>

   * <span data-ttu-id="b9660-122">Gebruik HTTPS als voorvoegsel Hallo.</span><span class="sxs-lookup"><span data-stu-id="b9660-122">Use HTTPS as hello prefix.</span></span>
   * <span data-ttu-id="b9660-123">Het aanvraagkenmerk is '/indexes/hotels'.</span><span class="sxs-lookup"><span data-stu-id="b9660-123">Request attribute is "/indexes/hotels".</span></span> <span data-ttu-id="b9660-124">Zo weet Search toocreate index met de naam 'hotels'.</span><span class="sxs-lookup"><span data-stu-id="b9660-124">This tells Search toocreate an index named 'hotels'.</span></span>
   * <span data-ttu-id="b9660-125">De API-versie moet worden opgegeven in kleine letters, als '?api-version=2016-09-01'.</span><span class="sxs-lookup"><span data-stu-id="b9660-125">Api-version is lowercase, specified as "?api-version=2016-09-01".</span></span> <span data-ttu-id="b9660-126">API-versies zijn belangrijk omdat Azure Search regelmatig updates implementeert.</span><span class="sxs-lookup"><span data-stu-id="b9660-126">API versions are important because Azure Search deploys updates regularly.</span></span> <span data-ttu-id="b9660-127">In zeldzame gevallen kan een service-update kan leiden tot een recente wijziging toohello API.</span><span class="sxs-lookup"><span data-stu-id="b9660-127">On rare occasions, a service update may introduce a breaking change toohello API.</span></span> <span data-ttu-id="b9660-128">Daarom vereist Azure Search bij elke aanvraag een API-versie, zodat u de volledige controle hebt over de API-versie die wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b9660-128">For this reason, Azure Search requires an api-version on each request so that you are in full control over which one is used.</span></span>

     <span data-ttu-id="b9660-129">Hallo volledige URL moet eruitzien vergelijkbare toohello voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="b9660-129">hello full URL should look similar toohello following example.</span></span>

             https://my-app.search.windows.net/indexes/hotels?api-version=2016-09-01
5. <span data-ttu-id="b9660-130">Geef de aanvraagheader hello, Hallo host en api-sleutel vervangen door waarden die geldig voor uw service zijn.</span><span class="sxs-lookup"><span data-stu-id="b9660-130">Specify hello request header, replacing hello host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
6. <span data-ttu-id="b9660-131">Plak in Hallo velden waaruit de indexdefinitie Hallo aanvraagtekst.</span><span class="sxs-lookup"><span data-stu-id="b9660-131">In Request Body, paste in hello fields that make up hello index definition.</span></span>

          {
         "name": "hotels",  
         "fields": [
           {"name": "hotelId", "type": "Edm.String", "key":true, "searchable": false},
           {"name": "baseRate", "type": "Edm.Double"},
           {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
           {"name": "hotelName", "type": "Edm.String"},
           {"name": "category", "type": "Edm.String"},
           {"name": "tags", "type": "Collection(Edm.String)"},
           {"name": "parkingIncluded", "type": "Edm.Boolean"},
           {"name": "smokingAllowed", "type": "Edm.Boolean"},
           {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
           {"name": "rating", "type": "Edm.Int32"},
           {"name": "location", "type": "Edm.GeographyPoint"}
          ]
         }
7. <span data-ttu-id="b9660-132">Klik op **Uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="b9660-132">Click **Execute**.</span></span>

<span data-ttu-id="b9660-133">In enkele seconden, ziet u een 201 HTTP-antwoord in de sessielijst hello, hetgeen betekent dat Hallo index is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b9660-133">In a few seconds, you should see an HTTP 201 response in hello session list, indicating hello index was created successfully.</span></span>

<span data-ttu-id="b9660-134">Als u HTTP 504-respons ontvangt, controleert u of dat Hallo URL HTTPS bevat.</span><span class="sxs-lookup"><span data-stu-id="b9660-134">If you get HTTP 504, verify hello URL specifies HTTPS.</span></span> <span data-ttu-id="b9660-135">Als u HTTP-fout 400 of 404 wordt weergegeven, controleert u Hallo aanvraag hoofdtekst tooverify er geen fouten zijn opgetreden kopiëren en plakken.</span><span class="sxs-lookup"><span data-stu-id="b9660-135">If you see HTTP 400 or 404, check hello request body tooverify there were no copy-paste errors.</span></span> <span data-ttu-id="b9660-136">Een HTTP 403 duidt doorgaans op een probleem met Hallo api-sleutel (een ongeldige sleutel of een probleem syntaxis met hoe Hallo api-sleutel is opgegeven).</span><span class="sxs-lookup"><span data-stu-id="b9660-136">An HTTP 403 typically indicates a problem with hello api-key (either an invalid key or a syntax problem with how hello api-key is specified).</span></span>

## <a name="load-documents"></a><span data-ttu-id="b9660-137">Documenten laden</span><span class="sxs-lookup"><span data-stu-id="b9660-137">Load documents</span></span>
<span data-ttu-id="b9660-138">Op Hallo **Composer** tabblad uw aanvraag toopost documenten eruit Hallo volgende.</span><span class="sxs-lookup"><span data-stu-id="b9660-138">On hello **Composer** tab, your request toopost documents will look like hello following.</span></span> <span data-ttu-id="b9660-139">Hallo-hoofdtekst van Hallo-aanvraag bevat Hallo zoekgegevens voor 4 hotels.</span><span class="sxs-lookup"><span data-stu-id="b9660-139">hello body of hello request contains hello search data for 4 hotels.</span></span>

   ![][2]

1. <span data-ttu-id="b9660-140">Selecteer **POST**.</span><span class="sxs-lookup"><span data-stu-id="b9660-140">Select **POST**.</span></span>
2. <span data-ttu-id="b9660-141">Geef een URL op die begint met HTTPS, gevolgd door uw service-URL, gevolgd door '/indexes/<indexnaam>/docs/index?api-version=2016-09-01'.</span><span class="sxs-lookup"><span data-stu-id="b9660-141">Enter a URL that starts with HTTPS, followed by your service URL, followed by "/indexes/<'indexname'>/docs/index?api-version=2016-09-01".</span></span> <span data-ttu-id="b9660-142">Hallo volledige URL moet eruitzien vergelijkbare toohello voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="b9660-142">hello full URL should look similar toohello following example.</span></span>

         https://my-app.search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
3. <span data-ttu-id="b9660-143">Aanvraag-Header moet worden Hallo hetzelfde als voorheen.</span><span class="sxs-lookup"><span data-stu-id="b9660-143">Request Header should be hello same as before.</span></span> <span data-ttu-id="b9660-144">Houd er rekening mee dat u Hallo host en api-sleutel vervangen door waarden die geldig voor uw service zijn.</span><span class="sxs-lookup"><span data-stu-id="b9660-144">Remember that you replaced hello host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. <span data-ttu-id="b9660-145">Hallo aanvraagtekst bevat vier documenten toobe toegevoegde toohello hotels index.</span><span class="sxs-lookup"><span data-stu-id="b9660-145">hello Request Body contains four documents toobe added toohello hotels index.</span></span>

         {
         "value": [
         {
             "@search.action": "upload",
             "hotelId": "1",
             "baseRate": 199.0,
             "description": "Best hotel in town",
             "hotelName": "Fancy Stay",
             "category": "Luxury",
             "tags": ["pool", "view", "wifi", "concierge"],
             "parkingIncluded": false,
             "smokingAllowed": false,
             "lastRenovationDate": "2010-06-27T00:00:00Z",
             "rating": 5,
             "location": { "type": "Point", "coordinates": [-122.131577, 47.678581] }
           },
           {
             "@search.action": "upload",
             "hotelId": "2",
             "baseRate": 79.99,
             "description": "Cheapest hotel in town",
             "hotelName": "Roach Motel",
             "category": "Budget",
             "tags": ["motel", "budget"],
             "parkingIncluded": true,
             "smokingAllowed": true,
             "lastRenovationDate": "1982-04-28T00:00:00Z",
             "rating": 1,
             "location": { "type": "Point", "coordinates": [-122.131577, 49.678581] }
           },
           {
             "@search.action": "upload",
             "hotelId": "3",
             "baseRate": 279.99,
             "description": "Surprisingly expensive",
             "hotelName": "Dew Drop Inn",
             "category": "Bed and Breakfast",
             "tags": ["charming", "quaint"],
             "parkingIncluded": true,
             "smokingAllowed": false,
             "lastRenovationDate": null,
             "rating": 4,
             "location": { "type": "Point", "coordinates": [-122.33207, 47.60621] }
           },
           {
             "@search.action": "upload",
             "hotelId": "4",
             "baseRate": 220.00,
             "description": "This could be hello one",
             "hotelName": "A Hotel for Everyone",
             "category": "Basic hotel",
             "tags": ["pool", "wifi"],
             "parkingIncluded": true,
             "smokingAllowed": false,
             "lastRenovationDate": null,
             "rating": 4,
             "location": { "type": "Point", "coordinates": [-122.12151, 47.67399] }
           }
          ]
         }
5. <span data-ttu-id="b9660-146">Klik op **Uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="b9660-146">Click **Execute**.</span></span>

<span data-ttu-id="b9660-147">In enkele seconden ziet u een HTTP 200-respons in de sessielijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="b9660-147">In a few seconds, you should see an HTTP 200 response in hello session list.</span></span> <span data-ttu-id="b9660-148">Hiermee wordt aangegeven Hallo documenten zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b9660-148">This indicates hello documents were created successfully.</span></span> <span data-ttu-id="b9660-149">Als u een 207 krijgt, wordt er door ten minste één document tooupload niet.</span><span class="sxs-lookup"><span data-stu-id="b9660-149">If you get a 207, at least one document failed tooupload.</span></span> <span data-ttu-id="b9660-150">Als u een 404 krijgt, hebt u Hallo koptekst of hoofdtekst van Hallo aanvraag een syntaxisfout.</span><span class="sxs-lookup"><span data-stu-id="b9660-150">If you get a 404, you have a syntax error in either hello header or body of hello request.</span></span>

## <a name="query-hello-index"></a><span data-ttu-id="b9660-151">Query Hallo index</span><span class="sxs-lookup"><span data-stu-id="b9660-151">Query hello index</span></span>
<span data-ttu-id="b9660-152">Nu er een index en documenten zijn geladen, kunt u hier query's op uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="b9660-152">Now that an index and documents are loaded, you can issue queries against them.</span></span>  <span data-ttu-id="b9660-153">Op Hallo **Composer** tabblad een **ophalen** opdracht waarmee een query op uw service ziet er vergelijkbare toohello volgende schermopname.</span><span class="sxs-lookup"><span data-stu-id="b9660-153">On hello **Composer** tab, a **GET** command that queries your service will look similar toohello following screen shot.</span></span>

   ![][3]

1. <span data-ttu-id="b9660-154">Selecteer **GET**.</span><span class="sxs-lookup"><span data-stu-id="b9660-154">Select **GET**.</span></span>
2. <span data-ttu-id="b9660-155">Geef een URL op die begint met HTTPS, gevolgd door uw service-URL, gevolgd door '/indexes/<indexnaam>/docs/index?', gevolgd door queryparameters.</span><span class="sxs-lookup"><span data-stu-id="b9660-155">Enter a URL that starts with HTTPS, followed by your service URL, followed by "/indexes/<'indexname'>/docs?", followed by query parameters.</span></span> <span data-ttu-id="b9660-156">Gebruik als bijvoorbeeld Hallo URL te volgen en vervangt Hallo Voorbeeldnaam van een host met een geldige voor uw service.</span><span class="sxs-lookup"><span data-stu-id="b9660-156">By way of example, use hello following URL, replacing hello sample host name with one that is valid for your service.</span></span>

         https://my-app.search.windows.net/indexes/hotels/docs?search=motel&facet=category&facet=rating,values:1|2|3|4|5&api-version=2016-09-01

   <span data-ttu-id="b9660-157">Deze query zoekt op Hallo term 'motel' en facetcategorieën voor beoordelingen opgehaald.</span><span class="sxs-lookup"><span data-stu-id="b9660-157">This query searches on hello term “motel” and retrieves facet categories for ratings.</span></span>
3. <span data-ttu-id="b9660-158">Aanvraag-Header moet worden Hallo hetzelfde als voorheen.</span><span class="sxs-lookup"><span data-stu-id="b9660-158">Request Header should be hello same as before.</span></span> <span data-ttu-id="b9660-159">Houd er rekening mee dat u Hallo host en api-sleutel vervangen door waarden die geldig voor uw service zijn.</span><span class="sxs-lookup"><span data-stu-id="b9660-159">Remember that you replaced hello host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444

<span data-ttu-id="b9660-160">Hallo responscode moet 200 en Hallo antwoorduitvoer moet eruitzien vergelijkbare toohello volgende schermopname.</span><span class="sxs-lookup"><span data-stu-id="b9660-160">hello response code should be 200, and hello response output should look similar toohello following screen shot.</span></span>

   ![][4]

<span data-ttu-id="b9660-161">Hallo volgende voorbeeldquery is afkomstig uit Hallo [Search Index-bewerking (Azure Search API)](http://msdn.microsoft.com/library/dn798927.aspx) op MSDN.</span><span class="sxs-lookup"><span data-stu-id="b9660-161">hello following example query is from hello [Search Index operation (Azure Search API)](http://msdn.microsoft.com/library/dn798927.aspx) on MSDN.</span></span> <span data-ttu-id="b9660-162">Veel van Hallo voorbeelden van query's in dit onderwerp bevatten spaties, deze zijn niet toegestaan in Fiddler.</span><span class="sxs-lookup"><span data-stu-id="b9660-162">Many of hello example queries in this topic include spaces, which are not allowed in Fiddler.</span></span> <span data-ttu-id="b9660-163">Vervang elke spatie door een + teken voordat plakken Hallo querytekenreeks voordat u probeert Hallo-query in Fiddler.</span><span class="sxs-lookup"><span data-stu-id="b9660-163">Replace each space with a + character before pasting in hello query string before attempting hello query in Fiddler.</span></span>

<span data-ttu-id="b9660-164">**Voordat de spaties zijn vervangen:**</span><span class="sxs-lookup"><span data-stu-id="b9660-164">**Before spaces are replaced:**</span></span>

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2016-09-01

<span data-ttu-id="b9660-165">**Nadat de spaties zijn vervangen door +:**</span><span class="sxs-lookup"><span data-stu-id="b9660-165">**After spaces are replaced with +:**</span></span>

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate+desc&api-version=2016-09-01

## <a name="query-hello-system"></a><span data-ttu-id="b9660-166">query Hallo systeem</span><span class="sxs-lookup"><span data-stu-id="b9660-166">Query hello system</span></span>
<span data-ttu-id="b9660-167">U kunt ook Hallo system tooget tellingen en opslag documentverbruik opvragen.</span><span class="sxs-lookup"><span data-stu-id="b9660-167">You can also query hello system tooget document counts and storage consumption.</span></span> <span data-ttu-id="b9660-168">Op Hallo **Composer** tabblad vergelijkbare toohello volgende eruit ziet uw aanvraag en Hallo respons retourneert een getal voor Hallo aantal documenten en de gebruikte ruimte.</span><span class="sxs-lookup"><span data-stu-id="b9660-168">On hello **Composer** tab, your request will look similar toohello following, and hello response will return a count for hello number of documents and space used.</span></span>

 ![][5]

1. <span data-ttu-id="b9660-169">Selecteer **GET**.</span><span class="sxs-lookup"><span data-stu-id="b9660-169">Select **GET**.</span></span>
2. <span data-ttu-id="b9660-170">Geef een URL op die uw service-URL bevat, gevolgd door '/indexes/hotels/stats?api-version=2016-09-01':</span><span class="sxs-lookup"><span data-stu-id="b9660-170">Enter a URL that includes your service URL, followed by "/indexes/hotels/stats?api-version=2016-09-01":</span></span>

         https://my-app.search.windows.net/indexes/hotels/stats?api-version=2016-09-01
3. <span data-ttu-id="b9660-171">Geef de aanvraagheader hello, Hallo host en api-sleutel vervangen door waarden die geldig voor uw service zijn.</span><span class="sxs-lookup"><span data-stu-id="b9660-171">Specify hello request header, replacing hello host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. <span data-ttu-id="b9660-172">Hallo aanvraagtekst leeg laten.</span><span class="sxs-lookup"><span data-stu-id="b9660-172">Leave hello request body empty.</span></span>
5. <span data-ttu-id="b9660-173">Klik op **Uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="b9660-173">Click **Execute**.</span></span> <span data-ttu-id="b9660-174">Hier ziet u een HTTP 200-statuscode in de sessielijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="b9660-174">You should see an HTTP 200 status code in hello session list.</span></span> <span data-ttu-id="b9660-175">Selecteer Hallo-vermelding voor de opdracht.</span><span class="sxs-lookup"><span data-stu-id="b9660-175">Select hello entry posted for your command.</span></span>
6. <span data-ttu-id="b9660-176">Klik op Hallo **Inspectors** en klik op Hallo **Headers** tabblad en selecteer vervolgens Hallo JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="b9660-176">Click hello **Inspectors** tab, click hello **Headers** tab, and then select hello JSON format.</span></span> <span data-ttu-id="b9660-177">U ziet Hallo document count en opslaggrootte (in KB).</span><span class="sxs-lookup"><span data-stu-id="b9660-177">You should see hello document count and storage size (in KB).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b9660-178">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b9660-178">Next steps</span></span>
<span data-ttu-id="b9660-179">Zie [uw Search-service op Azure beheren](search-manage.md) voor een toomanaging zonder code benadering en het gebruik van Azure Search.</span><span class="sxs-lookup"><span data-stu-id="b9660-179">See [Manage your Search service on Azure](search-manage.md) for a no-code approach toomanaging and using Azure Search.</span></span>

<!--Image References-->
[1]: ./media/search-fiddler/AzureSearch_Fiddler1_PutIndex.png
[2]: ./media/search-fiddler/AzureSearch_Fiddler2_PostDocs.png
[3]: ./media/search-fiddler/AzureSearch_Fiddler3_Query.png
[4]: ./media/search-fiddler/AzureSearch_Fiddler4_QueryResults.png
[5]: ./media/search-fiddler/AzureSearch_Fiddler5_QueryStats.png
