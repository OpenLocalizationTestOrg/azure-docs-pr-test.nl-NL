---
title: Fiddler gebruiken om Azure Search REST API's te evalueren en te testen | Microsoft Docs
description: "Gebruik Fiddler om zonder code de beschikbaarheid van Azure Search te verifiëren en de REST API's uit te proberen."
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
ms.openlocfilehash: c38b73fa69bee34ce2434c6274cb017c99ef3c35
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-fiddler-to-evaluate-and-test-azure-search-rest-apis"></a><span data-ttu-id="c98df-103">Gebruik Fiddler om Azure Search REST API's te evalueren en te testen</span><span class="sxs-lookup"><span data-stu-id="c98df-103">Use Fiddler to evaluate and test Azure Search REST APIs</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="c98df-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="c98df-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="c98df-105">Search Explorer</span><span class="sxs-lookup"><span data-stu-id="c98df-105">Search Explorer</span></span>](search-explorer.md)
> * [<span data-ttu-id="c98df-106">Fiddler</span><span class="sxs-lookup"><span data-stu-id="c98df-106">Fiddler</span></span>](search-fiddler.md)
> * [<span data-ttu-id="c98df-107">.NET</span><span class="sxs-lookup"><span data-stu-id="c98df-107">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="c98df-108">REST</span><span class="sxs-lookup"><span data-stu-id="c98df-108">REST</span></span>](search-query-rest-api.md)
>
>

<span data-ttu-id="c98df-109">In dit artikel wordt uitgelegd hoe u Fiddler, beschikbaar als [gratis download via Telerik](http://www.telerik.com/fiddler), gebruikt om HTTP-aanvragen te verzenden en antwoorden weer te geven met de Azure Search REST API, zonder dat u code hoeft te schrijven.</span><span class="sxs-lookup"><span data-stu-id="c98df-109">This article explains how to use Fiddler, available as a [free download from Telerik](http://www.telerik.com/fiddler), to issue HTTP requests to and view responses using the Azure Search REST API, without having to write any code.</span></span> <span data-ttu-id="c98df-110">Azure Search is een volledig beheerde, gehoste Microsoft Azure-service voor zoeken in de cloud. De service is eenvoudig programmeerbaar via .NET en REST API's.</span><span class="sxs-lookup"><span data-stu-id="c98df-110">Azure Search is fully-managed, hosted cloud search service on Microsoft Azure, easily programmable through .NET and REST APIs.</span></span> <span data-ttu-id="c98df-111">Documentatie over de REST API's voor de Azure Search-service vindt u op [MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx).</span><span class="sxs-lookup"><span data-stu-id="c98df-111">The Azure Search service REST APIs are documented on [MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx).</span></span>

<span data-ttu-id="c98df-112">In de volgende stappen maakt u een index, uploadt u documenten, voert u een query uit op de index en voert u vervolgens een query uit op het systeem om servicegegevens te zoeken.</span><span class="sxs-lookup"><span data-stu-id="c98df-112">In the following steps, you'll create an index, upload documents, query the index, and then query the system for service information.</span></span>

<span data-ttu-id="c98df-113">U hebt een Azure Search-service en `api-key` nodig om deze stappen te kunnen voltooien.</span><span class="sxs-lookup"><span data-stu-id="c98df-113">To complete these steps, you will need an Azure Search service and `api-key`.</span></span> <span data-ttu-id="c98df-114">Zie [Een Azure Search-service in de portal maken](search-create-service-portal.md) voor instructies om aan de slag gaan.</span><span class="sxs-lookup"><span data-stu-id="c98df-114">See [Create an Azure Search service in the portal](search-create-service-portal.md) for instructions on how to get started.</span></span>

## <a name="create-an-index"></a><span data-ttu-id="c98df-115">Een index maken</span><span class="sxs-lookup"><span data-stu-id="c98df-115">Create an index</span></span>
1. <span data-ttu-id="c98df-116">Start Fiddler.</span><span class="sxs-lookup"><span data-stu-id="c98df-116">Start Fiddler.</span></span> <span data-ttu-id="c98df-117">Schakel in het menu **File** (Bestand) de optie **Capture Traffic** (Verkeer vastleggen) uit om de HTTP-activiteit te verbergen die niet van belang is voor de huidige taak.</span><span class="sxs-lookup"><span data-stu-id="c98df-117">On the **File** menu, turn off **Capture Traffic** to hide extraneous HTTP activity that is unrelated to the current task.</span></span>
2. <span data-ttu-id="c98df-118">Op het tabblad **Composer** (Opstellen) formuleert u een aanvraag die vergelijkbaar is met de volgende schermopname.</span><span class="sxs-lookup"><span data-stu-id="c98df-118">On the **Composer** tab, you'll formulate a request that looks like the following screen shot.</span></span>

      ![][1]
3. <span data-ttu-id="c98df-119">Selecteer **PUT**.</span><span class="sxs-lookup"><span data-stu-id="c98df-119">Select **PUT**.</span></span>
4. <span data-ttu-id="c98df-120">Geef een URL op waarin de service-URL, aanvraagkenmerken en de API-versie worden gespecificeerd.</span><span class="sxs-lookup"><span data-stu-id="c98df-120">Enter a URL that specifies the service URL, request attributes, and the api-version.</span></span> <span data-ttu-id="c98df-121">Enkele punten om rekening mee te houden:</span><span class="sxs-lookup"><span data-stu-id="c98df-121">A few pointers to keep in mind:</span></span>

   * <span data-ttu-id="c98df-122">Gebruik HTTPS als voorvoegsel.</span><span class="sxs-lookup"><span data-stu-id="c98df-122">Use HTTPS as the prefix.</span></span>
   * <span data-ttu-id="c98df-123">Het aanvraagkenmerk is '/indexes/hotels'.</span><span class="sxs-lookup"><span data-stu-id="c98df-123">Request attribute is "/indexes/hotels".</span></span> <span data-ttu-id="c98df-124">Zodoende weet Search dat de index met de naam 'hotels' moet worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c98df-124">This tells Search to create an index named 'hotels'.</span></span>
   * <span data-ttu-id="c98df-125">De API-versie moet worden opgegeven in kleine letters, als '?api-version=2016-09-01'.</span><span class="sxs-lookup"><span data-stu-id="c98df-125">Api-version is lowercase, specified as "?api-version=2016-09-01".</span></span> <span data-ttu-id="c98df-126">API-versies zijn belangrijk omdat Azure Search regelmatig updates implementeert.</span><span class="sxs-lookup"><span data-stu-id="c98df-126">API versions are important because Azure Search deploys updates regularly.</span></span> <span data-ttu-id="c98df-127">In uitzonderlijk gevallen introduceert een service-update een belangrijke wijziging in de API.</span><span class="sxs-lookup"><span data-stu-id="c98df-127">On rare occasions, a service update may introduce a breaking change to the API.</span></span> <span data-ttu-id="c98df-128">Daarom vereist Azure Search bij elke aanvraag een API-versie, zodat u de volledige controle hebt over de API-versie die wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c98df-128">For this reason, Azure Search requires an api-version on each request so that you are in full control over which one is used.</span></span>

     <span data-ttu-id="c98df-129">De volledige URL moet er ongeveer uitzien als de URL in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="c98df-129">The full URL should look similar to the following example.</span></span>

             https://my-app.search.windows.net/indexes/hotels?api-version=2016-09-01
5. <span data-ttu-id="c98df-130">Geef de aanvraagheader de host en de API-sleutel hebt vervangen door de geldige waarden voor uw service.</span><span class="sxs-lookup"><span data-stu-id="c98df-130">Specify the request header, replacing the host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
6. <span data-ttu-id="c98df-131">Plak de velden waaruit de indexdefinitie bestaat in de aanvraagtekst.</span><span class="sxs-lookup"><span data-stu-id="c98df-131">In Request Body, paste in the fields that make up the index definition.</span></span>

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
7. <span data-ttu-id="c98df-132">Klik op **Execute** (Uitvoeren).</span><span class="sxs-lookup"><span data-stu-id="c98df-132">Click **Execute**.</span></span>

<span data-ttu-id="c98df-133">Over een paar seconden wordt er een 201 HTTP-respons in de sessielijst weergegeven dat de index is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c98df-133">In a few seconds, you should see an HTTP 201 response in the session list, indicating the index was created successfully.</span></span>

<span data-ttu-id="c98df-134">Als u een HTTP 504-respons ontvangt, controleert u of de URL HTTPS bevat.</span><span class="sxs-lookup"><span data-stu-id="c98df-134">If you get HTTP 504, verify the URL specifies HTTPS.</span></span> <span data-ttu-id="c98df-135">Als de HTTP-fout 400 of 404 wordt weergegeven ziet, controleert u of de aanvraagtekst op fouten die mogelijk zijn opgetreden tijden kopiëren en plakken.</span><span class="sxs-lookup"><span data-stu-id="c98df-135">If you see HTTP 400 or 404, check the request body to verify there were no copy-paste errors.</span></span> <span data-ttu-id="c98df-136">Een HTTP 403 duidt doorgaans op een probleem met de API-sleutel (een ongeldige sleutel of een syntaxisfout in de opgegeven API-sleutel).</span><span class="sxs-lookup"><span data-stu-id="c98df-136">An HTTP 403 typically indicates a problem with the api-key (either an invalid key or a syntax problem with how the api-key is specified).</span></span>

## <a name="load-documents"></a><span data-ttu-id="c98df-137">Documenten laden</span><span class="sxs-lookup"><span data-stu-id="c98df-137">Load documents</span></span>
<span data-ttu-id="c98df-138">Uw aanvraag op het tabblad **Composer** (Opstellen) om documenten te plaatsen, ziet er als volgt uit.</span><span class="sxs-lookup"><span data-stu-id="c98df-138">On the **Composer** tab, your request to post documents will look like the following.</span></span> <span data-ttu-id="c98df-139">De hoofdtekst van de aanvraag bevat de zoekgegevens voor vier hotels.</span><span class="sxs-lookup"><span data-stu-id="c98df-139">The body of the request contains the search data for 4 hotels.</span></span>

   ![][2]

1. <span data-ttu-id="c98df-140">Selecteer **POST**.</span><span class="sxs-lookup"><span data-stu-id="c98df-140">Select **POST**.</span></span>
2. <span data-ttu-id="c98df-141">Geef een URL op die begint met HTTPS, gevolgd door uw service-URL, gevolgd door '/indexes/<indexnaam>/docs/index?api-version=2016-09-01'.</span><span class="sxs-lookup"><span data-stu-id="c98df-141">Enter a URL that starts with HTTPS, followed by your service URL, followed by "/indexes/<'indexname'>/docs/index?api-version=2016-09-01".</span></span> <span data-ttu-id="c98df-142">De volledige URL moet er ongeveer uitzien als de URL in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="c98df-142">The full URL should look similar to the following example.</span></span>

         https://my-app.search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
3. <span data-ttu-id="c98df-143">De aanvraagheader blijft ongewijzigd.</span><span class="sxs-lookup"><span data-stu-id="c98df-143">Request Header should be the same as before.</span></span> <span data-ttu-id="c98df-144">Vergeet niet dat u de host en de API-sleutel hebt vervangen door waarden die geldig voor uw service zijn.</span><span class="sxs-lookup"><span data-stu-id="c98df-144">Remember that you replaced the host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. <span data-ttu-id="c98df-145">De aanvraagtekst bevat vier documenten die moeten worden toegevoegd aan de index hotels.</span><span class="sxs-lookup"><span data-stu-id="c98df-145">The Request Body contains four documents to be added to the hotels index.</span></span>

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
             "description": "This could be the one",
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
5. <span data-ttu-id="c98df-146">Klik op **Execute** (Uitvoeren).</span><span class="sxs-lookup"><span data-stu-id="c98df-146">Click **Execute**.</span></span>

<span data-ttu-id="c98df-147">Over enkele seconden verschijnt er een HTTP 200-respons in de sessielijst.</span><span class="sxs-lookup"><span data-stu-id="c98df-147">In a few seconds, you should see an HTTP 200 response in the session list.</span></span> <span data-ttu-id="c98df-148">Dit geeft aan dat de documenten zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c98df-148">This indicates the documents were created successfully.</span></span> <span data-ttu-id="c98df-149">Als u een 207-respons ontvang, is minimaal één document niet geüpload.</span><span class="sxs-lookup"><span data-stu-id="c98df-149">If you get a 207, at least one document failed to upload.</span></span> <span data-ttu-id="c98df-150">Als u een 404-respons ontvangt, bevat de header of de hoofdtekst van de aanvraag een syntaxisfout.</span><span class="sxs-lookup"><span data-stu-id="c98df-150">If you get a 404, you have a syntax error in either the header or body of the request.</span></span>

## <a name="query-the-index"></a><span data-ttu-id="c98df-151">Een query op de index uitvoeren</span><span class="sxs-lookup"><span data-stu-id="c98df-151">Query the index</span></span>
<span data-ttu-id="c98df-152">Nu er een index en documenten zijn geladen, kunt u hier query's op uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="c98df-152">Now that an index and documents are loaded, you can issue queries against them.</span></span>  <span data-ttu-id="c98df-153">Een **GET**-opdracht op het tabblad**Composer** (Opstellen), waarmee een query op uw service wordt uitgevoerd, is vergelijkbaar met de volgende schermopname.</span><span class="sxs-lookup"><span data-stu-id="c98df-153">On the **Composer** tab, a **GET** command that queries your service will look similar to the following screen shot.</span></span>

   ![][3]

1. <span data-ttu-id="c98df-154">Selecteer **GET**.</span><span class="sxs-lookup"><span data-stu-id="c98df-154">Select **GET**.</span></span>
2. <span data-ttu-id="c98df-155">Geef een URL op die begint met HTTPS, gevolgd door uw service-URL, gevolgd door '/indexes/<indexnaam>/docs/index?', gevolgd door queryparameters.</span><span class="sxs-lookup"><span data-stu-id="c98df-155">Enter a URL that starts with HTTPS, followed by your service URL, followed by "/indexes/<'indexname'>/docs?", followed by query parameters.</span></span> <span data-ttu-id="c98df-156">Gebruik als bijvoorbeeld de volgende URL en vervang de naam van de voorbeeldhost door een geldige naam voor uw service.</span><span class="sxs-lookup"><span data-stu-id="c98df-156">By way of example, use the following URL, replacing the sample host name with one that is valid for your service.</span></span>

         https://my-app.search.windows.net/indexes/hotels/docs?search=motel&facet=category&facet=rating,values:1|2|3|4|5&api-version=2016-09-01

   <span data-ttu-id="c98df-157">Met deze query wordt naar de term 'motel' en worden er facetcategorieën voor beoordelingen opgehaald.</span><span class="sxs-lookup"><span data-stu-id="c98df-157">This query searches on the term “motel” and retrieves facet categories for ratings.</span></span>
3. <span data-ttu-id="c98df-158">De aanvraagheader blijft ongewijzigd.</span><span class="sxs-lookup"><span data-stu-id="c98df-158">Request Header should be the same as before.</span></span> <span data-ttu-id="c98df-159">Vergeet niet dat u de host en de API-sleutel hebt vervangen door waarden die geldig voor uw service zijn.</span><span class="sxs-lookup"><span data-stu-id="c98df-159">Remember that you replaced the host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444

<span data-ttu-id="c98df-160">De responscode moet 200 zijn en de responsuitvoer moet er ongeveer hetzelfde uitzien als in de volgende schermopname.</span><span class="sxs-lookup"><span data-stu-id="c98df-160">The response code should be 200, and the response output should look similar to the following screen shot.</span></span>

   ![][4]

<span data-ttu-id="c98df-161">De volgende voorbeeldquery is afkomstig uit de [Search Index-bewerking (Azure Search API)](http://msdn.microsoft.com/library/dn798927.aspx) op MSDN.</span><span class="sxs-lookup"><span data-stu-id="c98df-161">The following example query is from the [Search Index operation (Azure Search API)](http://msdn.microsoft.com/library/dn798927.aspx) on MSDN.</span></span> <span data-ttu-id="c98df-162">Veel van de voorbeeldquery's in dit onderwerp bevatten spaties. Deze zijn niet toegestaan in Fiddler.</span><span class="sxs-lookup"><span data-stu-id="c98df-162">Many of the example queries in this topic include spaces, which are not allowed in Fiddler.</span></span> <span data-ttu-id="c98df-163">Vervang elke spatie door een plusteken (+) voordat u de queryreeks in Fiddler plakt en uitvoert.</span><span class="sxs-lookup"><span data-stu-id="c98df-163">Replace each space with a + character before pasting in the query string before attempting the query in Fiddler.</span></span>

<span data-ttu-id="c98df-164">**Voordat de spaties zijn vervangen:**</span><span class="sxs-lookup"><span data-stu-id="c98df-164">**Before spaces are replaced:**</span></span>

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2016-09-01

<span data-ttu-id="c98df-165">**Nadat de spaties zijn vervangen door +:**</span><span class="sxs-lookup"><span data-stu-id="c98df-165">**After spaces are replaced with +:**</span></span>

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate+desc&api-version=2016-09-01

## <a name="query-the-system"></a><span data-ttu-id="c98df-166">Een query uitvoeren op het systeem</span><span class="sxs-lookup"><span data-stu-id="c98df-166">Query the system</span></span>
<span data-ttu-id="c98df-167">U kunt ook een query op het systeem uitvoeren om het aantal documenten en opslagverbruik op te vragen.</span><span class="sxs-lookup"><span data-stu-id="c98df-167">You can also query the system to get document counts and storage consumption.</span></span> <span data-ttu-id="c98df-168">Uw aanvraag op het tabblad **Composer** (Opstellen) ziet er ongeveer als volgt uit en de respons retourneert een getal voor het aantal documenten en de gebruikte ruimte.</span><span class="sxs-lookup"><span data-stu-id="c98df-168">On the **Composer** tab, your request will look similar to the following, and the response will return a count for the number of documents and space used.</span></span>

 ![][5]

1. <span data-ttu-id="c98df-169">Selecteer **GET**.</span><span class="sxs-lookup"><span data-stu-id="c98df-169">Select **GET**.</span></span>
2. <span data-ttu-id="c98df-170">Geef een URL op die uw service-URL bevat, gevolgd door '/indexes/hotels/stats?api-version=2016-09-01':</span><span class="sxs-lookup"><span data-stu-id="c98df-170">Enter a URL that includes your service URL, followed by "/indexes/hotels/stats?api-version=2016-09-01":</span></span>

         https://my-app.search.windows.net/indexes/hotels/stats?api-version=2016-09-01
3. <span data-ttu-id="c98df-171">Geef de aanvraagheader de host en de API-sleutel hebt vervangen door de geldige waarden voor uw service.</span><span class="sxs-lookup"><span data-stu-id="c98df-171">Specify the request header, replacing the host and api-key with values that are valid for your service.</span></span>

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. <span data-ttu-id="c98df-172">Laat de aanvraagtekst leeg.</span><span class="sxs-lookup"><span data-stu-id="c98df-172">Leave the request body empty.</span></span>
5. <span data-ttu-id="c98df-173">Klik op **Execute** (Uitvoeren).</span><span class="sxs-lookup"><span data-stu-id="c98df-173">Click **Execute**.</span></span> <span data-ttu-id="c98df-174">Er wordt een HTTP 200-statuscode weergegeven in de sessielijst.</span><span class="sxs-lookup"><span data-stu-id="c98df-174">You should see an HTTP 200 status code in the session list.</span></span> <span data-ttu-id="c98df-175">Selecteer de vermelding van uw opdracht.</span><span class="sxs-lookup"><span data-stu-id="c98df-175">Select the entry posted for your command.</span></span>
6. <span data-ttu-id="c98df-176">Klik op het tabblad **Inspectors** (Inspecteurs), klik op het tabblad **Headers** en selecteer vervolgens de JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="c98df-176">Click the **Inspectors** tab, click the **Headers** tab, and then select the JSON format.</span></span> <span data-ttu-id="c98df-177">Als het goed is wordt het aantal documenten en de opslaggrootte (in kB) weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c98df-177">You should see the document count and storage size (in KB).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c98df-178">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c98df-178">Next steps</span></span>
<span data-ttu-id="c98df-179">Zie [Uw Search-service op Azure beheren](search-manage.md) om te zien hoe u Azure Search zonder code kunt beheren en gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c98df-179">See [Manage your Search service on Azure](search-manage.md) for a no-code approach to managing and using Azure Search.</span></span>

<!--Image References-->
[1]: ./media/search-fiddler/AzureSearch_Fiddler1_PutIndex.png
[2]: ./media/search-fiddler/AzureSearch_Fiddler2_PostDocs.png
[3]: ./media/search-fiddler/AzureSearch_Fiddler3_Query.png
[4]: ./media/search-fiddler/AzureSearch_Fiddler4_QueryResults.png
[5]: ./media/search-fiddler/AzureSearch_Fiddler5_QueryStats.png
