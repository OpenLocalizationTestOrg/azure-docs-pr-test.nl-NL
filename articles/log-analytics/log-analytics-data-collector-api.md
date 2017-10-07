---
title: aaaLog Analytics HTTP Data Collector API | Microsoft Docs
description: Kunt u Hallo Log Analytics HTTP Data Collector API tooadd POST JSON data toohello Log Analytics-opslagplaats vanaf elke client die kunt Hallo REST-API aanroepen. Dit artikel wordt beschreven hoe u toouse Hallo API en voorbeelden van hoe heeft toopublish gegevens met behulp van verschillende programmeertalen.
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: a831fd90-3f55-423b-8b20-ccbaaac2ca75
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: bwren
ms.openlocfilehash: c2921082831c49da764d946ac9c4fab975a38185
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="send-data-toolog-analytics-with-hello-http-data-collector-api"></a><span data-ttu-id="50ac4-104">Verzenden van gegevens tooLog Analytics Hello HTTP Data Collector API</span><span class="sxs-lookup"><span data-stu-id="50ac4-104">Send data tooLog Analytics with hello HTTP Data Collector API</span></span>
<span data-ttu-id="50ac4-105">Dit artikel laat zien hoe toouse Hallo HTTP Data Collector API toosend gegevens tooLog Analytics van een REST-API-client.</span><span class="sxs-lookup"><span data-stu-id="50ac4-105">This article shows you how toouse hello HTTP Data Collector API toosend data tooLog Analytics from a REST API client.</span></span>  <span data-ttu-id="50ac4-106">Het beschrijft hoe tooformat gegevens verzameld door het script of een toepassing, opneemt in een aanvraag en die aanvraag geautoriseerd door logboekanalyse hebben.</span><span class="sxs-lookup"><span data-stu-id="50ac4-106">It describes how tooformat data collected by your script or application, include it in a request, and have that request authorized by Log Analytics.</span></span>  <span data-ttu-id="50ac4-107">Voorbeelden zijn bedoeld voor PowerShell, C# en Python.</span><span class="sxs-lookup"><span data-stu-id="50ac4-107">Examples are provided for PowerShell, C#, and Python.</span></span>

## <a name="concepts"></a><span data-ttu-id="50ac4-108">Concepten</span><span class="sxs-lookup"><span data-stu-id="50ac4-108">Concepts</span></span>
<span data-ttu-id="50ac4-109">U kunt Hallo HTTP Data Collector API toosend gegevens tooLog Analytics vanaf elke client die een REST-API kan aanroepen.</span><span class="sxs-lookup"><span data-stu-id="50ac4-109">You can use hello HTTP Data Collector API toosend data tooLog Analytics from any client that can call a REST API.</span></span>  <span data-ttu-id="50ac4-110">Dit wordt mogelijk een runbook in Azure Automation die management verzamelt gegevens uit Azure of een andere cloud, of het mogelijk een alternatieve beheersysteem die gebruikmaakt van logboekanalyse tooconsolidate en analyseren van gegevens.</span><span class="sxs-lookup"><span data-stu-id="50ac4-110">This might be a runbook in Azure Automation that collects management data from Azure or another cloud, or it might be an alternate management system that uses Log Analytics tooconsolidate and analyze data.</span></span>

<span data-ttu-id="50ac4-111">Alle gegevens in Hallo Log Analytics-bibliotheek is opgeslagen als een record met een bepaald recordtype.</span><span class="sxs-lookup"><span data-stu-id="50ac4-111">All data in hello Log Analytics repository is stored as a record with a particular record type.</span></span>  <span data-ttu-id="50ac4-112">U kunt uw gegevens toosend toohello HTTP Data Collector API opmaken als meerdere records in JSON.</span><span class="sxs-lookup"><span data-stu-id="50ac4-112">You format your data toosend toohello HTTP Data Collector API as multiple records in JSON.</span></span>  <span data-ttu-id="50ac4-113">Wanneer u hello gegevens verzenden, wordt een afzonderlijke record gemaakt in Hallo-opslagplaats voor elke record in de aanvraaglading van de Hallo.</span><span class="sxs-lookup"><span data-stu-id="50ac4-113">When you submit hello data, an individual record is created in hello repository for each record in hello request payload.</span></span>


![Overzicht van de HTTP-gegevensverzamelaar](media/log-analytics-data-collector-api/overview.png)



## <a name="create-a-request"></a><span data-ttu-id="50ac4-115">Een aanvraag maken</span><span class="sxs-lookup"><span data-stu-id="50ac4-115">Create a request</span></span>
<span data-ttu-id="50ac4-116">toouse hello HTTP gegevensverzamelaar API u maakt een POST-aanvraag met Hallo gegevens toosend in JSON JavaScript Object Notation ().</span><span class="sxs-lookup"><span data-stu-id="50ac4-116">toouse hello HTTP Data Collector API, you create a POST request that includes hello data toosend in JavaScript Object Notation (JSON).</span></span>  <span data-ttu-id="50ac4-117">Hallo volgende drie tabellen lijst Hallo kenmerken die vereist voor elke aanvraag zijn.</span><span class="sxs-lookup"><span data-stu-id="50ac4-117">hello next three tables list hello attributes that are required for each request.</span></span> <span data-ttu-id="50ac4-118">Elk kenmerk later in Hallo artikel nader worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="50ac4-118">We describe each attribute in more detail later in hello article.</span></span>

### <a name="request-uri"></a><span data-ttu-id="50ac4-119">Aanvraag-URI</span><span class="sxs-lookup"><span data-stu-id="50ac4-119">Request URI</span></span>
| <span data-ttu-id="50ac4-120">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="50ac4-120">Attribute</span></span> | <span data-ttu-id="50ac4-121">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="50ac4-121">Property</span></span> |
|:--- |:--- |
| <span data-ttu-id="50ac4-122">Methode</span><span class="sxs-lookup"><span data-stu-id="50ac4-122">Method</span></span> |<span data-ttu-id="50ac4-123">VERZENDEN</span><span class="sxs-lookup"><span data-stu-id="50ac4-123">POST</span></span> |
| <span data-ttu-id="50ac4-124">URI</span><span class="sxs-lookup"><span data-stu-id="50ac4-124">URI</span></span> |<span data-ttu-id="50ac4-125">https://\<CustomerId\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01</span><span class="sxs-lookup"><span data-stu-id="50ac4-125">https://\<CustomerId\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01</span></span> |
| <span data-ttu-id="50ac4-126">Type inhoud</span><span class="sxs-lookup"><span data-stu-id="50ac4-126">Content type</span></span> |<span data-ttu-id="50ac4-127">application/json</span><span class="sxs-lookup"><span data-stu-id="50ac4-127">application/json</span></span> |

### <a name="request-uri-parameters"></a><span data-ttu-id="50ac4-128">De parameters van de aanvraag-URI</span><span class="sxs-lookup"><span data-stu-id="50ac4-128">Request URI parameters</span></span>
| <span data-ttu-id="50ac4-129">Parameter</span><span class="sxs-lookup"><span data-stu-id="50ac4-129">Parameter</span></span> | <span data-ttu-id="50ac4-130">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="50ac4-130">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="50ac4-131">Klant-id</span><span class="sxs-lookup"><span data-stu-id="50ac4-131">CustomerID</span></span> |<span data-ttu-id="50ac4-132">de unieke id voor de Microsoft Operations Management Suite-werkruimte Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="50ac4-132">hello unique identifier for hello Microsoft Operations Management Suite workspace.</span></span> |
| <span data-ttu-id="50ac4-133">Resource</span><span class="sxs-lookup"><span data-stu-id="50ac4-133">Resource</span></span> |<span data-ttu-id="50ac4-134">de resourcenaam Hallo API: / api/Logboeken.</span><span class="sxs-lookup"><span data-stu-id="50ac4-134">hello API resource name: /api/logs.</span></span> |
| <span data-ttu-id="50ac4-135">API-versie</span><span class="sxs-lookup"><span data-stu-id="50ac4-135">API Version</span></span> |<span data-ttu-id="50ac4-136">Hallo-versie van Hallo API toouse aan deze aanvraag.</span><span class="sxs-lookup"><span data-stu-id="50ac4-136">hello version of hello API toouse with this request.</span></span> <span data-ttu-id="50ac4-137">Het is momenteel 2016-04-01.</span><span class="sxs-lookup"><span data-stu-id="50ac4-137">Currently, it's 2016-04-01.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="50ac4-138">Aanvraagheaders</span><span class="sxs-lookup"><span data-stu-id="50ac4-138">Request headers</span></span>
| <span data-ttu-id="50ac4-139">Koptekst</span><span class="sxs-lookup"><span data-stu-id="50ac4-139">Header</span></span> | <span data-ttu-id="50ac4-140">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="50ac4-140">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="50ac4-141">Autorisatie</span><span class="sxs-lookup"><span data-stu-id="50ac4-141">Authorization</span></span> |<span data-ttu-id="50ac4-142">Hallo autorisatie handtekening.</span><span class="sxs-lookup"><span data-stu-id="50ac4-142">hello authorization signature.</span></span> <span data-ttu-id="50ac4-143">Verderop in Hallo artikel, kunt u meer informatie over het toocreate een HMAC-SHA256-header.</span><span class="sxs-lookup"><span data-stu-id="50ac4-143">Later in hello article, you can read about how toocreate an HMAC-SHA256 header.</span></span> |
| <span data-ttu-id="50ac4-144">Logboek-Type</span><span class="sxs-lookup"><span data-stu-id="50ac4-144">Log-Type</span></span> |<span data-ttu-id="50ac4-145">Geef Hallo recordtype Hallo-gegevens die wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="50ac4-145">Specify hello record type of hello data that is being submitted.</span></span> <span data-ttu-id="50ac4-146">Hallo Logboektype ondersteunt momenteel alleen alfanumerieke tekens.</span><span class="sxs-lookup"><span data-stu-id="50ac4-146">Currently, hello log type supports only alpha characters.</span></span> <span data-ttu-id="50ac4-147">Het ondersteunt geen numerieke waarden of speciale tekens.</span><span class="sxs-lookup"><span data-stu-id="50ac4-147">It does not support numerics or special characters.</span></span> |
| <span data-ttu-id="50ac4-148">x-ms-datum</span><span class="sxs-lookup"><span data-stu-id="50ac4-148">x-ms-date</span></span> |<span data-ttu-id="50ac4-149">Hallo datum die Hallo-aanvraag is verwerkt, in RFC 1123-indeling.</span><span class="sxs-lookup"><span data-stu-id="50ac4-149">hello date that hello request was processed, in RFC 1123 format.</span></span> |
| <span data-ttu-id="50ac4-150">Time-gegenereerd-veld</span><span class="sxs-lookup"><span data-stu-id="50ac4-150">time-generated-field</span></span> |<span data-ttu-id="50ac4-151">Hallo-naam van een veld in Hallo-gegevens die Hallo tijdstempel van gegevensitem Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="50ac4-151">hello name of a field in hello data that contains hello timestamp of hello data item.</span></span> <span data-ttu-id="50ac4-152">Als u een veld opgeven en vervolgens de inhoud ervan worden gebruikt voor **TimeGenerated**.</span><span class="sxs-lookup"><span data-stu-id="50ac4-152">If you specify a field then its contents are used for **TimeGenerated**.</span></span> <span data-ttu-id="50ac4-153">Als dit veld niet wordt opgegeven, de standaardwaarde voor Hallo **TimeGenerated** Hallo tijd is die Hallo bericht wordt ingenomen.</span><span class="sxs-lookup"><span data-stu-id="50ac4-153">If this field isn’t specified, hello default for **TimeGenerated** is hello time that hello message is ingested.</span></span> <span data-ttu-id="50ac4-154">Hallo-inhoud van het veld Hallo-bericht moeten volgen Hallo ISO 8601-notatie jjjj-MM-ssZ.</span><span class="sxs-lookup"><span data-stu-id="50ac4-154">hello contents of hello message field should follow hello ISO 8601 format YYYY-MM-DDThh:mm:ssZ.</span></span> |

## <a name="authorization"></a><span data-ttu-id="50ac4-155">Autorisatie</span><span class="sxs-lookup"><span data-stu-id="50ac4-155">Authorization</span></span>
<span data-ttu-id="50ac4-156">Een aanvraag toohello Log Analytics HTTP Data Collector API moet een autorisatie-header bevatten.</span><span class="sxs-lookup"><span data-stu-id="50ac4-156">Any request toohello Log Analytics HTTP Data Collector API must include an authorization header.</span></span> <span data-ttu-id="50ac4-157">tooauthenticate een aanvraag, moet u zich aanmelden Hallo-aanvraag met Hallo primaire of secundaire sleutel Hallo voor Hallo-werkruimte die Hallo heeft aangevraagd.</span><span class="sxs-lookup"><span data-stu-id="50ac4-157">tooauthenticate a request, you must sign hello request with either hello primary or hello secondary key for hello workspace that is making hello request.</span></span> <span data-ttu-id="50ac4-158">Vervolgens moet die handtekening doorgegeven als onderdeel van Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="50ac4-158">Then, pass that signature as part of hello request.</span></span>   

<span data-ttu-id="50ac4-159">Hier volgt Hallo-indeling voor Hallo autorisatie-header:</span><span class="sxs-lookup"><span data-stu-id="50ac4-159">Here's hello format for hello authorization header:</span></span>

```
Authorization: SharedKey <WorkspaceID>:<Signature>
```

<span data-ttu-id="50ac4-160">*WorkspaceID* is de unieke id Hallo voor Hallo Operations Management Suite-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="50ac4-160">*WorkspaceID* is hello unique identifier for hello Operations Management Suite workspace.</span></span> <span data-ttu-id="50ac4-161">*Handtekening* is een [HMAC Hash-based Message Authentication Code ()](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) die is gemaakt op basis van aanvraag Hallo en vervolgens wordt berekend met behulp van Hallo [algoritme SHA256](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx).</span><span class="sxs-lookup"><span data-stu-id="50ac4-161">*Signature* is a [Hash-based Message Authentication Code (HMAC)](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) that is constructed from hello request and then computed by using hello [SHA256 algorithm](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx).</span></span> <span data-ttu-id="50ac4-162">Vervolgens coderen u deze met behulp van Base64-codering.</span><span class="sxs-lookup"><span data-stu-id="50ac4-162">Then, you encode it by using Base64 encoding.</span></span>

<span data-ttu-id="50ac4-163">Gebruik deze indeling tooencode hello **SharedKey** handtekening tekenreeks:</span><span class="sxs-lookup"><span data-stu-id="50ac4-163">Use this format tooencode hello **SharedKey** signature string:</span></span>

```
StringToSign = VERB + "\n" +
                  Content-Length + "\n" +
               Content-Type + "\n" +
                  x-ms-date + "\n" +
                  "/api/logs";
```

<span data-ttu-id="50ac4-164">Hier volgt een voorbeeld van een tekenreeks in handtekening:</span><span class="sxs-lookup"><span data-stu-id="50ac4-164">Here's an example of a signature string:</span></span>

```
POST\n1024\napplication/json\nx-ms-date:Mon, 04 Apr 2016 08:00:00 GMT\n/api/logs
```

<span data-ttu-id="50ac4-165">Wanneer u Hallo handtekening tekenreeks, deze coderen met behulp van Hallo HMAC SHA256-algoritme op Hallo UTF-8-gecodeerde tekenreeks en vervolgens coderen Hallo resultaat als Base64.</span><span class="sxs-lookup"><span data-stu-id="50ac4-165">When you have hello signature string, encode it by using hello HMAC-SHA256 algorithm on hello UTF-8-encoded string, and then encode hello result as Base64.</span></span> <span data-ttu-id="50ac4-166">Gebruik deze indeling:</span><span class="sxs-lookup"><span data-stu-id="50ac4-166">Use this format:</span></span>

```
Signature=Base64(HMAC-SHA256(UTF8(StringToSign)))
```

<span data-ttu-id="50ac4-167">Hallo-voorbeelden in de volgende secties Hallo hebben voorbeeld code toohelp maken van een autorisatie-header.</span><span class="sxs-lookup"><span data-stu-id="50ac4-167">hello samples in hello next sections have sample code toohelp you create an authorization header.</span></span>

## <a name="request-body"></a><span data-ttu-id="50ac4-168">Aanvraagtekst</span><span class="sxs-lookup"><span data-stu-id="50ac4-168">Request body</span></span>
<span data-ttu-id="50ac4-169">Hallo-hoofdtekst van het Hallo-bericht moet zich in JSON.</span><span class="sxs-lookup"><span data-stu-id="50ac4-169">hello body of hello message must be in JSON.</span></span> <span data-ttu-id="50ac4-170">Er moet een of meer records met de eigenschap naam- en waardeparen Hallo opnemen in deze indeling:</span><span class="sxs-lookup"><span data-stu-id="50ac4-170">It must include one or more records with hello property name and value pairs in this format:</span></span>

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

<span data-ttu-id="50ac4-171">U kunt meerdere records in één aanvraag samen met behulp van de volgende indeling Hallo batch.</span><span class="sxs-lookup"><span data-stu-id="50ac4-171">You can batch multiple records together in a single request by using hello following format.</span></span> <span data-ttu-id="50ac4-172">Alle Hallo records moet Hallo dezelfde recordtype.</span><span class="sxs-lookup"><span data-stu-id="50ac4-172">All hello records must be hello same record type.</span></span>

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
},
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

## <a name="record-type-and-properties"></a><span data-ttu-id="50ac4-173">Recordtype en de eigenschappen</span><span class="sxs-lookup"><span data-stu-id="50ac4-173">Record type and properties</span></span>
<span data-ttu-id="50ac4-174">U kunt een aangepaste recordtype definiëren bij het indienen van gegevens via Hallo Log Analytics HTTP Data Collector API.</span><span class="sxs-lookup"><span data-stu-id="50ac4-174">You define a custom record type when you submit data through hello Log Analytics HTTP Data Collector API.</span></span> <span data-ttu-id="50ac4-175">Op dit moment kunt u kan niet schrijven gegevens tooexisting recordtypen die zijn gemaakt door andere gegevenstypen en oplossingen.</span><span class="sxs-lookup"><span data-stu-id="50ac4-175">Currently, you can't write data tooexisting record types that were created by other data types and solutions.</span></span> <span data-ttu-id="50ac4-176">Log Analytics Hallo binnenkomende gegevens leest en maakt vervolgens eigenschappen die overeenkomen met de gegevenstypen Hallo van Hallo-waarden die u invoert.</span><span class="sxs-lookup"><span data-stu-id="50ac4-176">Log Analytics reads hello incoming data and then creates properties that match hello data types of hello values that you enter.</span></span>

<span data-ttu-id="50ac4-177">Elke aanvraag toohello Log Analytics-API moet bevatten een **Logboektype** header met de naam Hallo voor Hallo recordtype.</span><span class="sxs-lookup"><span data-stu-id="50ac4-177">Each request toohello Log Analytics API must include a **Log-Type** header with hello name for hello record type.</span></span> <span data-ttu-id="50ac4-178">Hallo achtervoegsel **_CL** automatisch toegevoegde toohello naam invoeren van toodistinguish uit andere logboek als een aangepast logboek typen.</span><span class="sxs-lookup"><span data-stu-id="50ac4-178">hello suffix **_CL** is automatically appended toohello name you enter toodistinguish it from other log types as a custom log.</span></span> <span data-ttu-id="50ac4-179">Bijvoorbeeld, als u Hallo naam invoeren **MyNewRecordType**, Log Analytics maakt een record met Hallo type **MyNewRecordType_CL**.</span><span class="sxs-lookup"><span data-stu-id="50ac4-179">For example, if you enter hello name **MyNewRecordType**, Log Analytics creates a record with hello type **MyNewRecordType_CL**.</span></span> <span data-ttu-id="50ac4-180">Dit zorgt ervoor dat er geen conflicten tussen typenamen die door de gebruiker is gemaakt en die in de huidig of toekomstig Microsoft-oplossingen hebt verzonden zijn.</span><span class="sxs-lookup"><span data-stu-id="50ac4-180">This helps ensure that there are no conflicts between user-created type names and those shipped in current or future Microsoft solutions.</span></span>

<span data-ttu-id="50ac4-181">gegevenstype tooidentify een eigenschap, logboekanalyse eigenschapsnaam toohello achtervoegsel wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="50ac4-181">tooidentify a property's data type, Log Analytics adds a suffix toohello property name.</span></span> <span data-ttu-id="50ac4-182">Als een eigenschap een null-waarde bevat, wordt Hallo-eigenschap is niet opgenomen in deze record.</span><span class="sxs-lookup"><span data-stu-id="50ac4-182">If a property contains a null value, hello property is not included in that record.</span></span> <span data-ttu-id="50ac4-183">Deze tabel ziet u het gegevenstype van de eigenschap Hallo en bijbehorende achtervoegsel:</span><span class="sxs-lookup"><span data-stu-id="50ac4-183">This table lists hello property data type and corresponding suffix:</span></span>

| <span data-ttu-id="50ac4-184">Het gegevenstype eigenschap</span><span class="sxs-lookup"><span data-stu-id="50ac4-184">Property data type</span></span> | <span data-ttu-id="50ac4-185">Achtervoegsel</span><span class="sxs-lookup"><span data-stu-id="50ac4-185">Suffix</span></span> |
|:--- |:--- |
| <span data-ttu-id="50ac4-186">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="50ac4-186">String</span></span> |<span data-ttu-id="50ac4-187">_K</span><span class="sxs-lookup"><span data-stu-id="50ac4-187">_s</span></span> |
| <span data-ttu-id="50ac4-188">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="50ac4-188">Boolean</span></span> |<span data-ttu-id="50ac4-189">_b</span><span class="sxs-lookup"><span data-stu-id="50ac4-189">_b</span></span> |
| <span data-ttu-id="50ac4-190">dubbele</span><span class="sxs-lookup"><span data-stu-id="50ac4-190">Double</span></span> |<span data-ttu-id="50ac4-191">_D</span><span class="sxs-lookup"><span data-stu-id="50ac4-191">_d</span></span> |
| <span data-ttu-id="50ac4-192">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="50ac4-192">Date/time</span></span> |<span data-ttu-id="50ac4-193">_Nauw</span><span class="sxs-lookup"><span data-stu-id="50ac4-193">_t</span></span> |
| <span data-ttu-id="50ac4-194">GUID</span><span class="sxs-lookup"><span data-stu-id="50ac4-194">GUID</span></span> |<span data-ttu-id="50ac4-195">_g</span><span class="sxs-lookup"><span data-stu-id="50ac4-195">_g</span></span> |

<span data-ttu-id="50ac4-196">Hallo-gegevenstype dat Log Analytics voor elke eigenschap gebruikt, is afhankelijk van of Hallo recordtype voor de nieuwe record Hallo al bestaat.</span><span class="sxs-lookup"><span data-stu-id="50ac4-196">hello data type that Log Analytics uses for each property depends on whether hello record type for hello new record already exists.</span></span>

* <span data-ttu-id="50ac4-197">Als er recordtype Hallo niet bestaat, maakt Log Analytics een nieuwe.</span><span class="sxs-lookup"><span data-stu-id="50ac4-197">If hello record type does not exist, Log Analytics creates a new one.</span></span> <span data-ttu-id="50ac4-198">Log Analytics Hallo JSON type Deductie toodetermine Hallo met gegevenstype gebruikt voor elke eigenschap voor de nieuwe record Hallo.</span><span class="sxs-lookup"><span data-stu-id="50ac4-198">Log Analytics uses hello JSON type inference toodetermine hello data type for each property for hello new record.</span></span>
* <span data-ttu-id="50ac4-199">Als er recordtype Hallo bestaat, probeert logboekanalyse toocreate een nieuwe record op basis van bestaande eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="50ac4-199">If hello record type does exist, Log Analytics attempts toocreate a new record based on existing properties.</span></span> <span data-ttu-id="50ac4-200">Als hello gegevenstype voor een eigenschap in de nieuwe record Hallo komt niet overeen met en kan niet worden geconverteerd toohello bestaande type of als hello record bevat een eigenschap die niet bestaat, maakt u een nieuwe eigenschap Log Analytics heeft dat Hallo relevante achtervoegsel.</span><span class="sxs-lookup"><span data-stu-id="50ac4-200">If hello data type for a property in hello new record doesn’t match and can’t be converted toohello existing type, or if hello record includes a property that doesn’t exist, Log Analytics creates a new property that has hello relevant suffix.</span></span>

<span data-ttu-id="50ac4-201">Deze vermelding verzending zou bijvoorbeeld een record maken met drie eigenschappen **number_d**, **boolean_b**, en **string_s**:</span><span class="sxs-lookup"><span data-stu-id="50ac4-201">For example, this submission entry would create a record with three properties, **number_d**, **boolean_b**, and **string_s**:</span></span>

![Voorbeeldrecord 1](media/log-analytics-data-collector-api/record-01.png)

<span data-ttu-id="50ac4-203">Als u vervolgens de volgende post ingediend met alle waarden die zijn opgemaakt als tekenreeksen, zou niet Hallo eigenschappen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="50ac4-203">If you then submitted this next entry, with all values formatted as strings, hello properties would not change.</span></span> <span data-ttu-id="50ac4-204">Deze waarden kunnen geconverteerde tooexisting gegevenstypen zijn:</span><span class="sxs-lookup"><span data-stu-id="50ac4-204">These values can be converted tooexisting data types:</span></span>

![Voorbeeldrecord 2](media/log-analytics-data-collector-api/record-02.png)

<span data-ttu-id="50ac4-206">Maar als u vervolgens het volgende indienen hebt aangebracht, logboekanalyse Hallo nieuwe eigenschappen maakt **boolean_d** en **string_d**.</span><span class="sxs-lookup"><span data-stu-id="50ac4-206">But, if you then made this next submission, Log Analytics would create hello new properties **boolean_d** and **string_d**.</span></span> <span data-ttu-id="50ac4-207">Deze waarden kunnen niet worden geconverteerd:</span><span class="sxs-lookup"><span data-stu-id="50ac4-207">These values can't be converted:</span></span>

![Voorbeeldrecord 3](media/log-analytics-data-collector-api/record-03.png)

<span data-ttu-id="50ac4-209">Als u de volgende vermelding, voordat het Hallo-recordtype werd gemaakt Hallo vervolgens ingediend, Log Analytics maakt een record met drie eigenschappen **gunstig**, **boolean_s**, en **string_s**.</span><span class="sxs-lookup"><span data-stu-id="50ac4-209">If you then submitted hello following entry, before hello record type was created, Log Analytics would create a record with three properties, **number_s**, **boolean_s**, and **string_s**.</span></span> <span data-ttu-id="50ac4-210">In dit item is elk van de oorspronkelijke waarden Hallo opgemaakt als een tekenreeks:</span><span class="sxs-lookup"><span data-stu-id="50ac4-210">In this entry, each of hello initial values is formatted as a string:</span></span>

![Voorbeeldrecord 4](media/log-analytics-data-collector-api/record-04.png)

## <a name="data-limits"></a><span data-ttu-id="50ac4-212">Gegevenslimieten</span><span class="sxs-lookup"><span data-stu-id="50ac4-212">Data limits</span></span>
<span data-ttu-id="50ac4-213">Er zijn enkele beperkingen rond Hallo gegevens toohello Log Analytics gegevensverzameling API geplaatst.</span><span class="sxs-lookup"><span data-stu-id="50ac4-213">There are some constraints around hello data posted toohello Log Analytics Data collection API.</span></span>

* <span data-ttu-id="50ac4-214">Maximaal 30 MB per post tooLog Analytics Data Collector API.</span><span class="sxs-lookup"><span data-stu-id="50ac4-214">Maximum of 30 MB per post tooLog Analytics Data Collector API.</span></span> <span data-ttu-id="50ac4-215">Dit is een maximale grootte voor een enkele post.</span><span class="sxs-lookup"><span data-stu-id="50ac4-215">This is a size limit for a single post.</span></span> <span data-ttu-id="50ac4-216">Als Hallo gegevens uit een enkele post die langer is dan 30 MB, u moet splitsen Hallo gegevens up toosmaller grootte segmenten gedownload en deze gelijktijdig te verzenden.</span><span class="sxs-lookup"><span data-stu-id="50ac4-216">If hello data from a single post that exceeds 30 MB, you should split hello data up toosmaller sized chunks and send them concurrently.</span></span>
* <span data-ttu-id="50ac4-217">Maximum van 32 KB limiet voor veldwaarden.</span><span class="sxs-lookup"><span data-stu-id="50ac4-217">Maximum of 32 KB limit for field values.</span></span> <span data-ttu-id="50ac4-218">Als de veldwaarde Hallo groter dan 32 KB is, worden Hallo gegevens afgekapt.</span><span class="sxs-lookup"><span data-stu-id="50ac4-218">If hello field value is greater than 32 KB, hello data will be truncated.</span></span>
* <span data-ttu-id="50ac4-219">Aanbevolen maximumaantal velden voor een bepaald type is 50.</span><span class="sxs-lookup"><span data-stu-id="50ac4-219">Recommended maximum number of fields for a given type is 50.</span></span> <span data-ttu-id="50ac4-220">Dit is een limiet van bruikbaarheid en zoeken ervaring perspectief.</span><span class="sxs-lookup"><span data-stu-id="50ac4-220">This is a practical limit from a usability and search experience perspective.</span></span>  

## <a name="return-codes"></a><span data-ttu-id="50ac4-221">Retourcodes</span><span class="sxs-lookup"><span data-stu-id="50ac4-221">Return codes</span></span>
<span data-ttu-id="50ac4-222">Hallo HTTP-statuscode 200 betekent dat Hallo-aanvraag is ontvangen voor verwerking.</span><span class="sxs-lookup"><span data-stu-id="50ac4-222">hello HTTP status code 200 means that hello request has been received for processing.</span></span> <span data-ttu-id="50ac4-223">Hiermee wordt aangegeven die Hallo-bewerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="50ac4-223">This indicates that hello operation completed successfully.</span></span>

<span data-ttu-id="50ac4-224">Deze tabel bevat de volledige reeks statuscodes die Hallo-service retourneert mogelijk Hallo:</span><span class="sxs-lookup"><span data-stu-id="50ac4-224">This table lists hello complete set of status codes that hello service might return:</span></span>

| <span data-ttu-id="50ac4-225">Code</span><span class="sxs-lookup"><span data-stu-id="50ac4-225">Code</span></span> | <span data-ttu-id="50ac4-226">Status</span><span class="sxs-lookup"><span data-stu-id="50ac4-226">Status</span></span> | <span data-ttu-id="50ac4-227">Foutcode</span><span class="sxs-lookup"><span data-stu-id="50ac4-227">Error code</span></span> | <span data-ttu-id="50ac4-228">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="50ac4-228">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="50ac4-229">200</span><span class="sxs-lookup"><span data-stu-id="50ac4-229">200</span></span> |<span data-ttu-id="50ac4-230">OK</span><span class="sxs-lookup"><span data-stu-id="50ac4-230">OK</span></span> | |<span data-ttu-id="50ac4-231">Hallo-aanvraag is geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="50ac4-231">hello request was successfully accepted.</span></span> |
| <span data-ttu-id="50ac4-232">400</span><span class="sxs-lookup"><span data-stu-id="50ac4-232">400</span></span> |<span data-ttu-id="50ac4-233">Onjuiste aanvraag</span><span class="sxs-lookup"><span data-stu-id="50ac4-233">Bad request</span></span> |<span data-ttu-id="50ac4-234">InactiveCustomer</span><span class="sxs-lookup"><span data-stu-id="50ac4-234">InactiveCustomer</span></span> |<span data-ttu-id="50ac4-235">Hallo-werkruimte is gesloten.</span><span class="sxs-lookup"><span data-stu-id="50ac4-235">hello workspace has been closed.</span></span> |
| <span data-ttu-id="50ac4-236">400</span><span class="sxs-lookup"><span data-stu-id="50ac4-236">400</span></span> |<span data-ttu-id="50ac4-237">Onjuiste aanvraag</span><span class="sxs-lookup"><span data-stu-id="50ac4-237">Bad request</span></span> |<span data-ttu-id="50ac4-238">InvalidApiVersion</span><span class="sxs-lookup"><span data-stu-id="50ac4-238">InvalidApiVersion</span></span> |<span data-ttu-id="50ac4-239">Hallo API-versie die u hebt opgegeven, is niet herkend door Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="50ac4-239">hello API version that you specified was not recognized by hello service.</span></span> |
| <span data-ttu-id="50ac4-240">400</span><span class="sxs-lookup"><span data-stu-id="50ac4-240">400</span></span> |<span data-ttu-id="50ac4-241">Onjuiste aanvraag</span><span class="sxs-lookup"><span data-stu-id="50ac4-241">Bad request</span></span> |<span data-ttu-id="50ac4-242">InvalidCustomerId</span><span class="sxs-lookup"><span data-stu-id="50ac4-242">InvalidCustomerId</span></span> |<span data-ttu-id="50ac4-243">Hallo opgegeven werkruimte-ID is ongeldig.</span><span class="sxs-lookup"><span data-stu-id="50ac4-243">hello workspace ID specified is invalid.</span></span> |
| <span data-ttu-id="50ac4-244">400</span><span class="sxs-lookup"><span data-stu-id="50ac4-244">400</span></span> |<span data-ttu-id="50ac4-245">Onjuiste aanvraag</span><span class="sxs-lookup"><span data-stu-id="50ac4-245">Bad request</span></span> |<span data-ttu-id="50ac4-246">InvalidDataFormat</span><span class="sxs-lookup"><span data-stu-id="50ac4-246">InvalidDataFormat</span></span> |<span data-ttu-id="50ac4-247">Ongeldige JSON is ingediend.</span><span class="sxs-lookup"><span data-stu-id="50ac4-247">Invalid JSON was submitted.</span></span> <span data-ttu-id="50ac4-248">Hallo-antwoordtekst mogelijk meer informatie over hoe tooresolve fout Hallo bevatten.</span><span class="sxs-lookup"><span data-stu-id="50ac4-248">hello response body might contain more information about how tooresolve hello error.</span></span> |
| <span data-ttu-id="50ac4-249">400</span><span class="sxs-lookup"><span data-stu-id="50ac4-249">400</span></span> |<span data-ttu-id="50ac4-250">Onjuiste aanvraag</span><span class="sxs-lookup"><span data-stu-id="50ac4-250">Bad request</span></span> |<span data-ttu-id="50ac4-251">InvalidLogType</span><span class="sxs-lookup"><span data-stu-id="50ac4-251">InvalidLogType</span></span> |<span data-ttu-id="50ac4-252">Hallo Logboektype opgegeven opgenomen speciale tekens of cijfers.</span><span class="sxs-lookup"><span data-stu-id="50ac4-252">hello log type specified contained special characters or numerics.</span></span> |
| <span data-ttu-id="50ac4-253">400</span><span class="sxs-lookup"><span data-stu-id="50ac4-253">400</span></span> |<span data-ttu-id="50ac4-254">Onjuiste aanvraag</span><span class="sxs-lookup"><span data-stu-id="50ac4-254">Bad request</span></span> |<span data-ttu-id="50ac4-255">MissingApiVersion</span><span class="sxs-lookup"><span data-stu-id="50ac4-255">MissingApiVersion</span></span> |<span data-ttu-id="50ac4-256">Hallo-API-versie is niet opgegeven.</span><span class="sxs-lookup"><span data-stu-id="50ac4-256">hello API version wasn’t specified.</span></span> |
| <span data-ttu-id="50ac4-257">400</span><span class="sxs-lookup"><span data-stu-id="50ac4-257">400</span></span> |<span data-ttu-id="50ac4-258">Onjuiste aanvraag</span><span class="sxs-lookup"><span data-stu-id="50ac4-258">Bad request</span></span> |<span data-ttu-id="50ac4-259">MissingContentType</span><span class="sxs-lookup"><span data-stu-id="50ac4-259">MissingContentType</span></span> |<span data-ttu-id="50ac4-260">Hallo-inhoudstype is niet opgegeven.</span><span class="sxs-lookup"><span data-stu-id="50ac4-260">hello content type wasn’t specified.</span></span> |
| <span data-ttu-id="50ac4-261">400</span><span class="sxs-lookup"><span data-stu-id="50ac4-261">400</span></span> |<span data-ttu-id="50ac4-262">Onjuiste aanvraag</span><span class="sxs-lookup"><span data-stu-id="50ac4-262">Bad request</span></span> |<span data-ttu-id="50ac4-263">MissingLogType</span><span class="sxs-lookup"><span data-stu-id="50ac4-263">MissingLogType</span></span> |<span data-ttu-id="50ac4-264">Hallo vereist logboek waardetype is niet opgegeven.</span><span class="sxs-lookup"><span data-stu-id="50ac4-264">hello required value log type wasn’t specified.</span></span> |
| <span data-ttu-id="50ac4-265">400</span><span class="sxs-lookup"><span data-stu-id="50ac4-265">400</span></span> |<span data-ttu-id="50ac4-266">Onjuiste aanvraag</span><span class="sxs-lookup"><span data-stu-id="50ac4-266">Bad request</span></span> |<span data-ttu-id="50ac4-267">UnsupportedContentType</span><span class="sxs-lookup"><span data-stu-id="50ac4-267">UnsupportedContentType</span></span> |<span data-ttu-id="50ac4-268">Hallo-inhoudstype is niet ingesteld te**application/json**.</span><span class="sxs-lookup"><span data-stu-id="50ac4-268">hello content type was not set too**application/json**.</span></span> |
| <span data-ttu-id="50ac4-269">403</span><span class="sxs-lookup"><span data-stu-id="50ac4-269">403</span></span> |<span data-ttu-id="50ac4-270">Is niet toegestaan</span><span class="sxs-lookup"><span data-stu-id="50ac4-270">Forbidden</span></span> |<span data-ttu-id="50ac4-271">InvalidAuthorization</span><span class="sxs-lookup"><span data-stu-id="50ac4-271">InvalidAuthorization</span></span> |<span data-ttu-id="50ac4-272">Hallo-service niet tooauthenticate Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="50ac4-272">hello service failed tooauthenticate hello request.</span></span> <span data-ttu-id="50ac4-273">Controleer of deze sleutel Hallo werkruimte-ID en de verbinding zijn geldig.</span><span class="sxs-lookup"><span data-stu-id="50ac4-273">Verify that hello workspace ID and connection key are valid.</span></span> |
| <span data-ttu-id="50ac4-274">404</span><span class="sxs-lookup"><span data-stu-id="50ac4-274">404</span></span> |<span data-ttu-id="50ac4-275">Niet gevonden</span><span class="sxs-lookup"><span data-stu-id="50ac4-275">Not Found</span></span> | | <span data-ttu-id="50ac4-276">De opgegeven Hallo-URL is onjuist of Hallo-aanvraag is te groot.</span><span class="sxs-lookup"><span data-stu-id="50ac4-276">Either hello URL provided is incorrect, or hello request is too large.</span></span> |
| <span data-ttu-id="50ac4-277">429</span><span class="sxs-lookup"><span data-stu-id="50ac4-277">429</span></span> |<span data-ttu-id="50ac4-278">Te veel aanvragen</span><span class="sxs-lookup"><span data-stu-id="50ac4-278">Too Many Requests</span></span> | | <span data-ttu-id="50ac4-279">Hallo-service is in korte tijd een groot aantal gegevens uit uw account.</span><span class="sxs-lookup"><span data-stu-id="50ac4-279">hello service is experiencing a high volume of data from your account.</span></span> <span data-ttu-id="50ac4-280">Probeer het Hallo-aanvraag later opnieuw.</span><span class="sxs-lookup"><span data-stu-id="50ac4-280">Please retry hello request later.</span></span> |
| <span data-ttu-id="50ac4-281">500</span><span class="sxs-lookup"><span data-stu-id="50ac4-281">500</span></span> |<span data-ttu-id="50ac4-282">Interne serverfout</span><span class="sxs-lookup"><span data-stu-id="50ac4-282">Internal Server Error</span></span> |<span data-ttu-id="50ac4-283">UnspecifiedError</span><span class="sxs-lookup"><span data-stu-id="50ac4-283">UnspecifiedError</span></span> |<span data-ttu-id="50ac4-284">Hallo-service heeft een interne fout.</span><span class="sxs-lookup"><span data-stu-id="50ac4-284">hello service encountered an internal error.</span></span> <span data-ttu-id="50ac4-285">Probeer het Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="50ac4-285">Please retry hello request.</span></span> |
| <span data-ttu-id="50ac4-286">503</span><span class="sxs-lookup"><span data-stu-id="50ac4-286">503</span></span> |<span data-ttu-id="50ac4-287">Service is niet beschikbaar</span><span class="sxs-lookup"><span data-stu-id="50ac4-287">Service Unavailable</span></span> |<span data-ttu-id="50ac4-288">ServiceUnavailable</span><span class="sxs-lookup"><span data-stu-id="50ac4-288">ServiceUnavailable</span></span> |<span data-ttu-id="50ac4-289">Hallo-service is momenteel niet beschikbaar tooreceive aanvragen.</span><span class="sxs-lookup"><span data-stu-id="50ac4-289">hello service currently is unavailable tooreceive requests.</span></span> <span data-ttu-id="50ac4-290">Probeer uw aanvraag.</span><span class="sxs-lookup"><span data-stu-id="50ac4-290">Please retry your request.</span></span> |

## <a name="query-data"></a><span data-ttu-id="50ac4-291">Querygegevens</span><span class="sxs-lookup"><span data-stu-id="50ac4-291">Query data</span></span>
<span data-ttu-id="50ac4-292">tooquery gegevens die zijn ingediend door Hallo Log Analytics HTTP Data Collector API, zoekt u records met **Type** is gelijk toohello **LogType** waarde die u hebt opgegeven, worden toegevoegd aan de **_CL**.</span><span class="sxs-lookup"><span data-stu-id="50ac4-292">tooquery data submitted by hello Log Analytics HTTP Data Collector API, search for records with **Type** that is equal toohello **LogType** value that you specified, appended with **_CL**.</span></span> <span data-ttu-id="50ac4-293">Als u gebruikt bijvoorbeeld **MyCustomLog**, zou u alle records met geretourneerd **Type = MyCustomLog_CL**.</span><span class="sxs-lookup"><span data-stu-id="50ac4-293">For example, if you used **MyCustomLog**, then you'd return all records with **Type=MyCustomLog_CL**.</span></span>

>[!NOTE]
> <span data-ttu-id="50ac4-294">Als uw werkruimte bijgewerkte toohello is [nieuwe logboekanalyse querytaal](log-analytics-log-search-upgrade.md), Hallo hierboven query zou Wijzig toohello volgende.</span><span class="sxs-lookup"><span data-stu-id="50ac4-294">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then hello above query would change toohello following.</span></span>

> `MyCustomLog_CL`

## <a name="sample-requests"></a><span data-ttu-id="50ac4-295">Voorbeeld aanvragen</span><span class="sxs-lookup"><span data-stu-id="50ac4-295">Sample requests</span></span>
<span data-ttu-id="50ac4-296">In de volgende secties hello, vindt u voorbeelden van hoe toosubmit gegevens toohello Log Analytics HTTP Data Collector API met behulp van verschillende programmeertalen.</span><span class="sxs-lookup"><span data-stu-id="50ac4-296">In hello next sections, you'll find samples of how toosubmit data toohello Log Analytics HTTP Data Collector API by using different programming languages.</span></span>

<span data-ttu-id="50ac4-297">Voor elk voorbeeld als volgt te werk tooset Hallo variabelen voor Hallo autorisatie-header:</span><span class="sxs-lookup"><span data-stu-id="50ac4-297">For each sample, do these steps tooset hello variables for hello authorization header:</span></span>

1. <span data-ttu-id="50ac4-298">Selecteer in de Operations Management Suite-portal Hallo Hallo **instellingen** tegel en selecteer vervolgens Hallo **verbonden bronnen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="50ac4-298">In hello Operations Management Suite portal, select hello **Settings** tile, and then select hello **Connected Sources** tab.</span></span>
2. <span data-ttu-id="50ac4-299">toohello rechts van **werkruimte-ID**Hallo kopie-pictogram en selecteer plak Hallo-ID als de waarde Hallo Hallo **klant-ID** variabele.</span><span class="sxs-lookup"><span data-stu-id="50ac4-299">toohello right of **Workspace ID**, select hello copy icon, and then paste hello ID as hello value of hello **Customer ID** variable.</span></span>
3. <span data-ttu-id="50ac4-300">toohello rechts van **primaire sleutel**Hallo kopie-pictogram en selecteer plak Hallo-ID als de waarde Hallo Hallo **gedeelde sleutel** variabele.</span><span class="sxs-lookup"><span data-stu-id="50ac4-300">toohello right of **Primary Key**, select hello copy icon, and then paste hello ID as hello value of hello **Shared Key** variable.</span></span>

<span data-ttu-id="50ac4-301">U kunt ook Hallo variabelen voor Hallo Logboektype en JSON-gegevens wijzigen.</span><span class="sxs-lookup"><span data-stu-id="50ac4-301">Alternatively, you can change hello variables for hello log type and JSON data.</span></span>

### <a name="powershell-sample"></a><span data-ttu-id="50ac4-302">PowerShell-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="50ac4-302">PowerShell sample</span></span>
```
# Replace with your Workspace ID
$CustomerId = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"  

# Replace with your Primary Key
$SharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# Specify hello name of hello record type that you'll be creating
$LogType = "MyRecordType"

# Specify a field with hello created time for hello records
$TimeStampField = "DateValue"


# Create two records with hello same set of properties toocreate
$json = @"
[{  "StringValue": "MyString1",
    "NumberValue": 42,
    "BooleanValue": true,
    "DateValue": "2016-05-12T20:00:00.625Z",
    "GUIDValue": "9909ED01-A74C-4874-8ABF-D2678E3AE23D"
},
{   "StringValue": "MyString2",
    "NumberValue": 43,
    "BooleanValue": false,
    "DateValue": "2016-05-12T20:00:00.625Z",
    "GUIDValue": "8809ED01-A74C-4874-8ABF-D2678E3AE23D"
}]
"@

# Create hello function toocreate hello authorization signature
Function Build-Signature ($customerId, $sharedKey, $date, $contentLength, $method, $contentType, $resource)
{
    $xHeaders = "x-ms-date:" + $date
    $stringToHash = $method + "`n" + $contentLength + "`n" + $contentType + "`n" + $xHeaders + "`n" + $resource

    $bytesToHash = [Text.Encoding]::UTF8.GetBytes($stringToHash)
    $keyBytes = [Convert]::FromBase64String($sharedKey)

    $sha256 = New-Object System.Security.Cryptography.HMACSHA256
    $sha256.Key = $keyBytes
    $calculatedHash = $sha256.ComputeHash($bytesToHash)
    $encodedHash = [Convert]::ToBase64String($calculatedHash)
    $authorization = 'SharedKey {0}:{1}' -f $customerId,$encodedHash
    return $authorization
}


# Create hello function toocreate and post hello request
Function Post-OMSData($customerId, $sharedKey, $body, $logType)
{
    $method = "POST"
    $contentType = "application/json"
    $resource = "/api/logs"
    $rfc1123date = [DateTime]::UtcNow.ToString("r")
    $contentLength = $body.Length
    $signature = Build-Signature `
        -customerId $customerId `
        -sharedKey $sharedKey `
        -date $rfc1123date `
        -contentLength $contentLength `
        -fileName $fileName `
        -method $method `
        -contentType $contentType `
        -resource $resource
    $uri = "https://" + $customerId + ".ods.opinsights.azure.com" + $resource + "?api-version=2016-04-01"

    $headers = @{
        "Authorization" = $signature;
        "Log-Type" = $logType;
        "x-ms-date" = $rfc1123date;
        "time-generated-field" = $TimeStampField;
    }

    $response = Invoke-WebRequest -Uri $uri -Method $method -ContentType $contentType -Headers $headers -Body $body -UseBasicParsing
    return $response.StatusCode

}

# Submit hello data toohello API endpoint
Post-OMSData -customerId $customerId -sharedKey $sharedKey -body ([System.Text.Encoding]::UTF8.GetBytes($json)) -logType $logType  
```

### <a name="c-sample"></a><span data-ttu-id="50ac4-303">C#-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="50ac4-303">C# sample</span></span>
```
using System;
using System.Net;
using System.Net.Http;
using System.Net.Http.Headers;
using System.Security.Cryptography;
using System.Text;
using System.Threading.Tasks;

namespace OIAPIExample
{
    class ApiExample
    {
        // An example JSON object, with key/value pairs
        static string json = @"[{""DemoField1"":""DemoValue1"",""DemoField2"":""DemoValue2""},{""DemoField3"":""DemoValue3"",""DemoField4"":""DemoValue4""}]";

        // Update customerId tooyour Operations Management Suite workspace ID
        static string customerId = "xxxxxxxx-xxx-xxx-xxx-xxxxxxxxxxxx";

        // For sharedKey, use either hello primary or hello secondary Connected Sources client authentication key   
        static string sharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";

        // LogName is name of hello event type that is being submitted tooLog Analytics
        static string LogName = "DemoExample";

        // You can use an optional field toospecify hello timestamp from hello data. If hello time field is not specified, Log Analytics assumes hello time is hello message ingestion time
        static string TimeStampField = "";

        static void Main()
        {
            // Create a hash for hello API signature
            var datestring = DateTime.UtcNow.ToString("r");
            string stringToHash = "POST\n" + json.Length + "\napplication/json\n" + "x-ms-date:" + datestring + "\n/api/logs";
            string hashedString = BuildSignature(stringToHash, sharedKey);
            string signature = "SharedKey " + customerId + ":" + hashedString;

            PostData(signature, datestring, json);
        }

        // Build hello API signature
        public static string BuildSignature(string message, string secret)
        {
            var encoding = new System.Text.ASCIIEncoding();
            byte[] keyByte = Convert.FromBase64String(secret);
            byte[] messageBytes = encoding.GetBytes(message);
            using (var hmacsha256 = new HMACSHA256(keyByte))
            {
                byte[] hash = hmacsha256.ComputeHash(messageBytes);
                return Convert.ToBase64String(hash);
            }
        }

        // Send a request toohello POST API endpoint
        public static void PostData(string signature, string date, string json)
        {
            try
            {
                string url = "https://" + customerId + ".ods.opinsights.azure.com/api/logs?api-version=2016-04-01";

                System.Net.Http.HttpClient client = new System.Net.Http.HttpClient();
                client.DefaultRequestHeaders.Add("Accept", "application/json");
                client.DefaultRequestHeaders.Add("Log-Type", LogName);
                client.DefaultRequestHeaders.Add("Authorization", signature);
                client.DefaultRequestHeaders.Add("x-ms-date", date);
                client.DefaultRequestHeaders.Add("time-generated-field", TimeStampField);

                System.Net.Http.HttpContent httpContent = new StringContent(json, Encoding.UTF8);
                httpContent.Headers.ContentType = new MediaTypeHeaderValue("application/json");
                Task<System.Net.Http.HttpResponseMessage> response = client.PostAsync(new Uri(url), httpContent);

                System.Net.Http.HttpContent responseContent = response.Result.Content;
                string result = responseContent.ReadAsStringAsync().Result;
                Console.WriteLine("Return Result: " + result);
            }
            catch (Exception excep)
            {
                Console.WriteLine("API Post Exception: " + excep.Message);
            }
        }
    }
}

```

### <a name="python-sample"></a><span data-ttu-id="50ac4-304">Python-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="50ac4-304">Python sample</span></span>
```
import json
import requests
import datetime
import hashlib
import hmac
import base64

# Update hello customer ID tooyour Operations Management Suite workspace ID
customer_id = 'xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'

# For hello shared key, use either hello primary or hello secondary Connected Sources client authentication key   
shared_key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# hello log type is hello name of hello event that is being submitted
log_type = 'WebMonitorTest'

# An example JSON web monitor object
json_data = [{
   "slot_ID": 12345,
    "ID": "5cdad72f-c848-4df0-8aaa-ffe033e75d57",
    "availability_Value": 100,
    "performance_Value": 6.954,
    "measurement_Name": "last_one_hour",
    "duration": 3600,
    "warning_Threshold": 0,
    "critical_Threshold": 0,
    "IsActive": "true"
},
{   
    "slot_ID": 67890,
    "ID": "b6bee458-fb65-492e-996d-61c4d7fbb942",
    "availability_Value": 100,
    "performance_Value": 3.379,
    "measurement_Name": "last_one_hour",
    "duration": 3600,
    "warning_Threshold": 0,
    "critical_Threshold": 0,
    "IsActive": "false"
}]
body = json.dumps(json_data)

#####################
######Functions######  
#####################

# Build hello API signature
def build_signature(customer_id, shared_key, date, content_length, method, content_type, resource):
    x_headers = 'x-ms-date:' + date
    string_to_hash = method + "\n" + str(content_length) + "\n" + content_type + "\n" + x_headers + "\n" + resource
    bytes_to_hash = bytes(string_to_hash).encode('utf-8')  
    decoded_key = base64.b64decode(shared_key)
    encoded_hash = base64.b64encode(hmac.new(decoded_key, bytes_to_hash, digestmod=hashlib.sha256).digest())
    authorization = "SharedKey {}:{}".format(customer_id,encoded_hash)
    return authorization

# Build and send a request toohello POST API
def post_data(customer_id, shared_key, body, log_type):
    method = 'POST'
    content_type = 'application/json'
    resource = '/api/logs'
    rfc1123date = datetime.datetime.utcnow().strftime('%a, %d %b %Y %H:%M:%S GMT')
    content_length = len(body)
    signature = build_signature(customer_id, shared_key, rfc1123date, content_length, method, content_type, resource)
    uri = 'https://' + customer_id + '.ods.opinsights.azure.com' + resource + '?api-version=2016-04-01'

    headers = {
        'content-type': content_type,
        'Authorization': signature,
        'Log-Type': log_type,
        'x-ms-date': rfc1123date
    }

    response = requests.post(uri,data=body, headers=headers)
    if (response.status_code >= 200 and response.status_code <= 299):
        print 'Accepted'
    else:
        print "Response code: {}".format(response.status_code)

post_data(customer_id, shared_key, body, log_type)
```

## <a name="next-steps"></a><span data-ttu-id="50ac4-305">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="50ac4-305">Next steps</span></span>
- <span data-ttu-id="50ac4-306">Gebruik Hallo [Log-API van zoekservice](log-analytics-log-search-api.md) tooretrieve gegevens van Hallo Log Analytics-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="50ac4-306">Use hello [Log Search API](log-analytics-log-search-api.md) tooretrieve data from hello Log Analytics repository.</span></span>
