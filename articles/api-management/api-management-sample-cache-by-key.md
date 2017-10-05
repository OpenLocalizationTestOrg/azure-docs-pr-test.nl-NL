---
title: Aangepaste opslaan in cache in Azure API Management
description: Meer informatie over het items in de cache per sleutel in Azure API Management
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: 772bc8dd-5cda-41c4-95bf-b9f6f052bc85
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: f5d5f44e34fbcd122a10be0ca5b3001760c4c64d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="custom-caching-in-azure-api-management"></a><span data-ttu-id="c8e45-103">Aangepaste opslaan in cache in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="c8e45-103">Custom caching in Azure API Management</span></span>
<span data-ttu-id="c8e45-104">Azure API Management-service biedt ingebouwde ondersteuning voor [HTTP-antwoord in cache opslaan](api-management-howto-cache.md) met behulp van de bron-URL als de sleutel.</span><span class="sxs-lookup"><span data-stu-id="c8e45-104">Azure API Management service has built-in support for [HTTP response caching](api-management-howto-cache.md) using the resource URL as the key.</span></span> <span data-ttu-id="c8e45-105">De sleutel kan worden gewijzigd door aanvraagheaders met behulp van de `vary-by` eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="c8e45-105">The key can be modified by request headers using the `vary-by` properties.</span></span> <span data-ttu-id="c8e45-106">Dit is handig voor het opslaan van de hele HTTP-antwoorden (aka verklaringen), maar soms is het nuttig om alleen cache een deel van een weergave.</span><span class="sxs-lookup"><span data-stu-id="c8e45-106">This is useful for caching entire HTTP responses (aka representations), but sometimes it is useful to just cache a portion of a representation.</span></span> <span data-ttu-id="c8e45-107">De nieuwe [cache zoekwaarde](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) en [cache-store-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) -beleid biedt de mogelijkheid op te slaan en willekeurige soorten gegevens vanuit beleidsdefinities ophalen.</span><span class="sxs-lookup"><span data-stu-id="c8e45-107">The new [cache-lookup-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) and [cache-store-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) policies provide the ability to store and retrieve arbitrary pieces of data from within policy definitions.</span></span> <span data-ttu-id="c8e45-108">Deze mogelijkheid wordt ook waarde toegevoegd aan de eerder geïntroduceerd [aanvragen verzenden](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) beleid omdat u kunt nu antwoorden van externe services cache.</span><span class="sxs-lookup"><span data-stu-id="c8e45-108">This ability also adds value to the previously introduced [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) policy because you can now cache responses from external services.</span></span>

## <a name="architecture"></a><span data-ttu-id="c8e45-109">Architectuur</span><span class="sxs-lookup"><span data-stu-id="c8e45-109">Architecture</span></span>
<span data-ttu-id="c8e45-110">API Management-service gebruikt een gedeelde tenant gegevenscache zodat terwijl u tot schaalt meerdere eenheden die u ontvangt nog steeds toegang tot dezelfde gegevens in de cache opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="c8e45-110">API Management service uses a shared per-tenant data cache so that, as you scale up to multiple units you will still get access to the same cached data.</span></span> <span data-ttu-id="c8e45-111">Als u werkt met een implementatie met meerdere regio zijn er echter onafhankelijke caches in elke regio.</span><span class="sxs-lookup"><span data-stu-id="c8e45-111">However, when working with a multi-region deployment there are independent caches within each of the regions.</span></span> <span data-ttu-id="c8e45-112">Als gevolg hiervan is het belangrijk dat de cache niet behandelen als een gegevensarchief, waar de enige bron van een stukje informatie is.</span><span class="sxs-lookup"><span data-stu-id="c8e45-112">Due to this, it is important to not treat the cache as a data store, where it is the only source of some piece of information.</span></span> <span data-ttu-id="c8e45-113">Als u hebt en later besluit om te profiteren van de implementatie van meerdere landen/regio, klikt u vervolgens klanten met gebruikers die geen toegang meer tot die gegevens in de cache.</span><span class="sxs-lookup"><span data-stu-id="c8e45-113">If you did, and later decided to take advantage of the multi-region deployment, then customers with users that travel may lose access to that cached data.</span></span>

## <a name="fragment-caching"></a><span data-ttu-id="c8e45-114">Fragment opslaan in cache</span><span class="sxs-lookup"><span data-stu-id="c8e45-114">Fragment caching</span></span>
<span data-ttu-id="c8e45-115">Er zijn bepaalde gevallen waarbij antwoorden worden geretourneerd bevatten een gedeelte van de gegevens die kostbaar om te bepalen en voor een redelijk tijdsbestek nog actueel blijft.</span><span class="sxs-lookup"><span data-stu-id="c8e45-115">There are certain cases where responses being returned contain some portion of data that is expensive to determine and yet remains fresh for a reasonable amount of time.</span></span> <span data-ttu-id="c8e45-116">Een voorbeeld kunt u een service die is gebouwd door een luchtvaartmaatschappij die voorziet in informatie over Vluchtreserveringen, vlucht status, enzovoort. Als de gebruiker lid is van het programma van de punten airlines, zouden ze ook informatie met betrekking tot hun huidige status en kilometers verzameld hebben.</span><span class="sxs-lookup"><span data-stu-id="c8e45-116">As an example, consider a service built by an airline that provides information relating flight reservations, flight status, etc. If the user is a member of the airlines points program, they would also have information relating to their current status and mileage accumulated.</span></span> <span data-ttu-id="c8e45-117">Deze gebruiker-gerelateerde gegevens worden opgeslagen in een ander systeem, maar het wenselijk is opgenomen in antwoorden over de status van de vlucht en -reserveringen geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="c8e45-117">This user-related information might be stored in a different system, but it may be desirable to include it in responses returned about flight status and reservations.</span></span> <span data-ttu-id="c8e45-118">U kunt dit doen via een proces genaamd fragment opslaan in cache.</span><span class="sxs-lookup"><span data-stu-id="c8e45-118">This can be done using a process called fragment caching.</span></span> <span data-ttu-id="c8e45-119">De primaire weergave kan worden opgehaald vanaf de oorspronkelijke server met behulp van een soort token om aan te geven waar de gebruiker-gerelateerde informatie moet worden ingevoegd.</span><span class="sxs-lookup"><span data-stu-id="c8e45-119">The primary representation can be returned from the origin server using some kind of token to indicate where the user-related information is to be inserted.</span></span> 

<span data-ttu-id="c8e45-120">Houd rekening met het volgende JSON-antwoord van een back-end API.</span><span class="sxs-lookup"><span data-stu-id="c8e45-120">Consider the following JSON response from a backend API.</span></span>

```json
{
  "airline" : "Air Canada",
  "flightno" : "871",
  "status" : "ontime",
  "gate" : "B40",
  "terminal" : "2A",
  "userprofile" : "$userprofile$"
}  
```

<span data-ttu-id="c8e45-121">En secundaire bron ingesteld op `/userprofile/{userid}` die vergelijkbaar is,</span><span class="sxs-lookup"><span data-stu-id="c8e45-121">And secondary resource at `/userprofile/{userid}` that looks like,</span></span>

```json
{ "username" : "Bob Smith", "Status" : "Gold" }
```

<span data-ttu-id="c8e45-122">Om te bepalen van de juiste gebruikersinformatie wilt opnemen, moeten we identificeren die de eindgebruiker.</span><span class="sxs-lookup"><span data-stu-id="c8e45-122">In order to determine the appropriate user information to include, we need to identify who the end user is.</span></span> <span data-ttu-id="c8e45-123">Dit mechanisme is afhankelijke-implementatie.</span><span class="sxs-lookup"><span data-stu-id="c8e45-123">This mechanism is implementation dependent.</span></span> <span data-ttu-id="c8e45-124">Als u bijvoorbeeld gebruik ik de `Subject` claimen van een `JWT` token.</span><span class="sxs-lookup"><span data-stu-id="c8e45-124">As an example, I am using the `Subject` claim of a `JWT` token.</span></span> 

```xml
<set-variable
  name="enduserid"
  value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />
```

<span data-ttu-id="c8e45-125">Zo bewaren wij dit `enduserid` waarde in een variabele context voor later gebruik.</span><span class="sxs-lookup"><span data-stu-id="c8e45-125">We store this `enduserid` value in a context variable for later use.</span></span> <span data-ttu-id="c8e45-126">De volgende stap is om te bepalen of een eerdere aanvraag al is opgehaald van de gebruikersgegevens en in de cache opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="c8e45-126">The next step is to determine if a previous request has already retrieved the user information and stored it in the cache.</span></span> <span data-ttu-id="c8e45-127">We gebruiken hiervoor de `cache-lookup-value` beleid.</span><span class="sxs-lookup"><span data-stu-id="c8e45-127">For this we use the `cache-lookup-value` policy.</span></span>

```xml
<cache-lookup-value
key="@("userprofile-" + context.Variables["enduserid"])"
variable-name="userprofile" />
```

<span data-ttu-id="c8e45-128">Als er is geen vermelding in de cache die overeenkomt met de waarde van de sleutel en klik op Nee `userprofile` context variabele wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c8e45-128">If there is no entry in the cache that corresponds to the key value, then no `userprofile` context variable will be created.</span></span> <span data-ttu-id="c8e45-129">We controleren of het succes van de zoekactie met behulp van de `choose` beleid overdrachten beheren.</span><span class="sxs-lookup"><span data-stu-id="c8e45-129">We check the success of the lookup using the `choose` control flow policy.</span></span>

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("userprofile"))">
        <!-- If the userprofile context variable doesn’t exist, make an HTTP request to retrieve it.  -->
    </when>
</choose>
```

<span data-ttu-id="c8e45-130">Als de `userprofile` context variabele bestaat niet en gaan we hebt om een HTTP-aanvraag te halen.</span><span class="sxs-lookup"><span data-stu-id="c8e45-130">If the `userprofile` context variable doesn’t exist, then we are going to have to make an HTTP request to retrieve it.</span></span>

```xml
<send-request
  mode="new"
  response-variable-name="userprofileresponse"
  timeout="10"
  ignore-error="true">

  <!-- Build a URL that points to the profile for the current end-user -->
  <set-url>@(new Uri(new Uri("https://apimairlineapi.azurewebsites.net/UserProfile/"),
      (string)context.Variables["enduserid"]).AbsoluteUri)
  </set-url>
  <set-method>GET</set-method>
</send-request>
```

<span data-ttu-id="c8e45-131">We gebruiken de `enduserid` de URL van de gebruiker de resource-profiel maken.</span><span class="sxs-lookup"><span data-stu-id="c8e45-131">We use the `enduserid` to construct the URL to the user profile resource.</span></span> <span data-ttu-id="c8e45-132">Nadat we het antwoord hebben, kunnen we de platte tekst uit het antwoord pull en sla deze terug in een context-variabele.</span><span class="sxs-lookup"><span data-stu-id="c8e45-132">Once we have the response, we can pull the body text out of the response and store it back into a context variable.</span></span>

```xml
<set-variable
    name="userprofile"
    value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />
```

<span data-ttu-id="c8e45-133">Om te voorkomen ons hoeven deze HTTP-aanvraag opnieuw maken wanneer dezelfde gebruiker een andere aanvraag indient, kunnen we het gebruikersprofiel in de cache opslaan.</span><span class="sxs-lookup"><span data-stu-id="c8e45-133">To avoid us having to make this HTTP request again, when the same user makes another request, we can store the user profile in the cache.</span></span>

```xml
<cache-store-value
    key="@("userprofile-" + context.Variables["enduserid"])"
    value="@((string)context.Variables["userprofile"])" duration="100000" />
```

<span data-ttu-id="c8e45-134">Zo bewaren wij de waarde in de cache met exact dezelfde sleutel die we oorspronkelijk heeft geprobeerd om op te halen met.</span><span class="sxs-lookup"><span data-stu-id="c8e45-134">We store the value in the cache using the exact same key that we originally attempted to retrieve it with.</span></span> <span data-ttu-id="c8e45-135">De duur die u kiest voor het opslaan van de waarde moet worden gebaseerd op hoe vaak worden de wijzigingen en hoe fouttolerante gebruikers tot actuele informatie.</span><span class="sxs-lookup"><span data-stu-id="c8e45-135">The duration that we choose to store the value should be based on how often the information changes and how tolerant users are to out of date information.</span></span> 

<span data-ttu-id="c8e45-136">Houd er rekening mee dat bij het ophalen van de cache nog steeds een out-of-process netwerkaanvraag is en mogelijk kan nog steeds tientallen tijd in milliseconden aan de aanvraag toevoegen is.</span><span class="sxs-lookup"><span data-stu-id="c8e45-136">It is important to realize that retrieving from the cache is still an out-of-process, network request and potentially can still add tens of milliseconds to the request.</span></span> <span data-ttu-id="c8e45-137">De voordelen worden geleverd bij het bepalen van de gebruikersprofielgegevens aanzienlijk langer duurt dan die als gevolg van hoeven om query's of statistische gegevens uit meerdere back-ends van databases.</span><span class="sxs-lookup"><span data-stu-id="c8e45-137">The benefits come when determining the user profile information takes significantly longer than that due to needing to do database queries or aggregate information from multiple back-ends.</span></span>

<span data-ttu-id="c8e45-138">De laatste stap in het proces is het bijwerken van het geretourneerde antwoord met onze gebruikersprofielgegevens.</span><span class="sxs-lookup"><span data-stu-id="c8e45-138">The final step in the process is to update the returned response with our user profile information.</span></span>

```xml
<!-- Update response body with user profile-->
<find-and-replace
    from='"$userprofile$"'
    to="@((string)context.Variables["userprofile"])" />
```

<span data-ttu-id="c8e45-139">Ik heb gekozen voor de aanhalingstekens als onderdeel van het token bevatten, zodat zelfs wanneer het vervangen niet wordt uitgevoerd, het antwoord nog geldig JSON is.</span><span class="sxs-lookup"><span data-stu-id="c8e45-139">I chose to include the quotation marks as part of the token so that even when the replace doesn’t occur, the response was still valid JSON.</span></span> <span data-ttu-id="c8e45-140">Dit is vooral om foutopsporing gemakkelijker.</span><span class="sxs-lookup"><span data-stu-id="c8e45-140">This was primarily to make debugging easier.</span></span>

<span data-ttu-id="c8e45-141">Als u al deze stappen samen combineren, is het eindresultaat een beleid dat op een lijkt.</span><span class="sxs-lookup"><span data-stu-id="c8e45-141">Once you combine all these steps together, the end result is a policy that looks like the following one.</span></span>

```xml
<policies>
    <inbound>
        <!-- How you determine user identity is application dependent -->
        <set-variable
          name="enduserid"
          value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />

        <!--Look for userprofile for this user in the cache -->
        <cache-lookup-value
          key="@("userprofile-" + context.Variables["enduserid"])"
          variable-name="userprofile" />

        <!-- If we don’t find it in the cache, make a request for it and store it -->
        <choose>
            <when condition="@(!context.Variables.ContainsKey("userprofile"))">
                <!-- Make HTTP request to get user profile -->
                <send-request
                  mode="new"
                  response-variable-name="userprofileresponse"
                  timeout="10"
                  ignore-error="true">

                   <!-- Build a URL that points to the profile for the current end-user -->
                    <set-url>@(new Uri(new Uri("https://apimairlineapi.azurewebsites.net/UserProfile/"),(string)context.Variables["enduserid"]).AbsoluteUri)</set-url>
                    <set-method>GET</set-method>
                </send-request>

                <!-- Store response body in context variable -->
                <set-variable
                  name="userprofile"
                  value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />

                <!-- Store result in cache -->
                <cache-store-value
                  key="@("userprofile-" + context.Variables["enduserid"])"
                  value="@((string)context.Variables["userprofile"])"
                  duration="100000" />
            </when>
        </choose>
        <base />
    </inbound>
    <outbound>
        <!-- Update response body with user profile-->
        <find-and-replace
              from='"$userprofile$"'
              to="@((string)context.Variables["userprofile"])" />
        <base />
    </outbound>
</policies>
```

<span data-ttu-id="c8e45-142">Deze cache benadering wordt voornamelijk gebruikt in websites waar HTML bestaat op de server zodat deze kan worden gerenderd als één pagina.</span><span class="sxs-lookup"><span data-stu-id="c8e45-142">This caching approach is primarily used in web sites where HTML is composed on the server side so that it can be rendered as a single page.</span></span> <span data-ttu-id="c8e45-143">Maar dit kan ook nuttig zijn in API's waar clients client kunnen niet aan de objectkant HTTP-caching of is het wenselijk zijn geen te plaatsen dat de verantwoordelijkheid van de client.</span><span class="sxs-lookup"><span data-stu-id="c8e45-143">However, it can also be useful in APIs where clients cannot do client side HTTP caching or it is desirable not to put that responsibility on the client.</span></span>

<span data-ttu-id="c8e45-144">Dit dezelfde soort fragment opslaan in cache kan ook worden uitgevoerd op de back-end-webservers met behulp van een in Redis cache van de server, echter met de API Management-service voor het uitvoeren van deze taak is nuttig wanneer de in de cache fragmenten afkomstig zijn uit verschillende back-ends dan de antwoorden in de primaire.</span><span class="sxs-lookup"><span data-stu-id="c8e45-144">This same kind of fragment caching can also be done on the backend web servers using a Redis caching server, however, using the API Management service to perform this work is useful when the cached fragments are coming from different back-ends than the primary responses.</span></span>

## <a name="transparent-versioning"></a><span data-ttu-id="c8e45-145">Transparante versiebeheer</span><span class="sxs-lookup"><span data-stu-id="c8e45-145">Transparent versioning</span></span>
<span data-ttu-id="c8e45-146">Het is gebruikelijk om voor meerdere versies van de andere implementatie van een API op elk gewenst moment worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="c8e45-146">It is common practice for multiple different implementation versions of an API to be supported at any one time.</span></span> <span data-ttu-id="c8e45-147">Dit is mogelijk voor de ondersteuning van verschillende omgevingen, zoals ontwikkelen, testen, productie, enzovoort, of kan zijn voor de ondersteuning van oudere versies van de API om tijd voor de API-consumenten te migreren naar nieuwere versies te geven.</span><span class="sxs-lookup"><span data-stu-id="c8e45-147">This is perhaps to support different environments, like dev, test, production, etc, or it may be to support older versions of the API to give time for API consumers to migrate to newer versions.</span></span> 

<span data-ttu-id="c8e45-148">Een aanpak voor het verwerken van dit hoeft client ontwikkelaars wijzigen van de URL's van `/v1/customers` naar `/v2/customers` opslaan in de consument profielgegevens welke versie van de API ze momenteel wilt gebruiken en roept u de juiste back-end-URL.</span><span class="sxs-lookup"><span data-stu-id="c8e45-148">One approach to handling this instead of requiring client developers to change the URLs from `/v1/customers` to `/v2/customers` is to store in the consumer’s profile data which version of the API they currently wish to use and call the appropriate backend URL.</span></span> <span data-ttu-id="c8e45-149">De juiste back-end-URL voor het aanroepen van een bepaalde client bepalen, is het nodig zijn sommige configuratiegegevens opvragen.</span><span class="sxs-lookup"><span data-stu-id="c8e45-149">In order to determine the correct backend URL to call for a particular client, it is necessary to query some configuration data.</span></span> <span data-ttu-id="c8e45-150">Door deze configuratiegegevens caching, kunnen we de prestaties van de handeling deze zoekactie minimaliseren.</span><span class="sxs-lookup"><span data-stu-id="c8e45-150">By caching this configuration data, we can minimize the performance penalty of doing this lookup.</span></span>

<span data-ttu-id="c8e45-151">De eerste stap is om te bepalen van de id die wordt gebruikt voor het configureren van de gewenste versie.</span><span class="sxs-lookup"><span data-stu-id="c8e45-151">The first step is to determine the identifier used to configure the desired version.</span></span> <span data-ttu-id="c8e45-152">In dit voorbeeld hebt ik ervoor gekozen om te koppelen van de versie op de productcode van het abonnement.</span><span class="sxs-lookup"><span data-stu-id="c8e45-152">In this example, I chose to associate the version to the product subscription key.</span></span> 

```xml
<set-variable name="clientid" value="@(context.Subscription.Key)" />
```

<span data-ttu-id="c8e45-153">We doen vervolgens een zoeken in het cachegeheugen om te zien als er al de gewenste clientversie is.</span><span class="sxs-lookup"><span data-stu-id="c8e45-153">We then do a cache lookup to see if we already have retrieved the desired client version.</span></span>

```xml
<cache-lookup-value
key="@("clientversion-" + context.Variables["clientid"])"
variable-name="clientversion" />
```

<span data-ttu-id="c8e45-154">Vervolgens controleren we om te zien als we niet in de cache vinden kon.</span><span class="sxs-lookup"><span data-stu-id="c8e45-154">Then we check to see if we did not find it in the cache.</span></span>

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("clientversion"))">
```

<span data-ttu-id="c8e45-155">Als we niet we gaan en dit ophalen.</span><span class="sxs-lookup"><span data-stu-id="c8e45-155">If we didn’t then we go and retrieve it.</span></span>

```xml
<send-request
    mode="new"
    response-variable-name="clientconfiguresponse"
    timeout="10"
    ignore-error="true">
            <set-url>@(new Uri(new Uri(context.Api.ServiceUrl.ToString() + "api/ClientConfig/"),(string)context.Variables["clientid"]).AbsoluteUri)</set-url>
            <set-method>GET</set-method>
</send-request>
```

<span data-ttu-id="c8e45-156">De hoofdtekst van antwoord extraheren uit het antwoord.</span><span class="sxs-lookup"><span data-stu-id="c8e45-156">Extract the response body text from the response.</span></span>

```xml
<set-variable
      name="clientversion"
      value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
```

<span data-ttu-id="c8e45-157">Sla het terug in het cachegeheugen voor toekomstig gebruik.</span><span class="sxs-lookup"><span data-stu-id="c8e45-157">Store it back in the cache for future use.</span></span>

```xml
<cache-store-value
      key="@("clientversion-" + context.Variables["clientid"])"
      value="@((string)context.Variables["clientversion"])"
      duration="100000" />
```

<span data-ttu-id="c8e45-158">En tot slot werkt u de URL van de back-end om te selecteren van de versie van de gewenste door de client-service.</span><span class="sxs-lookup"><span data-stu-id="c8e45-158">And finally update the back-end URL to select the version of the service desired by the client.</span></span>

```xml
<set-backend-service
      base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
```

<span data-ttu-id="c8e45-159">Het beleid volledig is als volgt.</span><span class="sxs-lookup"><span data-stu-id="c8e45-159">The completely policy is as follows.</span></span>

```xml
<inbound>
    <base />
    <set-variable name="clientid" value="@(context.Subscription.Key)" />
    <cache-lookup-value key="@("clientversion-" + context.Variables["clientid"])" variable-name="clientversion" />

    <!-- If we don’t find it in the cache, make a request for it and store it -->
    <choose>
        <when condition="@(!context.Variables.ContainsKey("clientversion"))">
            <send-request mode="new" response-variable-name="clientconfiguresponse" timeout="10" ignore-error="true">
                <set-url>@(new Uri(new Uri(context.Api.ServiceUrl.ToString() + "api/ClientConfig/"),(string)context.Variables["clientid"]).AbsoluteUri)</set-url>
                <set-method>GET</set-method>
            </send-request>
            <!-- Store response body in context variable -->
            <set-variable name="clientversion" value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
            <!-- Store result in cache -->
            <cache-store-value key="@("clientversion-" + context.Variables["clientid"])" value="@((string)context.Variables["clientversion"])" duration="100000" />
        </when>
    </choose>
    <set-backend-service base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
</inbound>
```

<span data-ttu-id="c8e45-160">Om de API-consumenten transparant bepalen welke endversie van de back-om wordt geopend door clients zonder bijwerken en implementeren van clients is een elegante oplossing die zijn gericht op veel API versioning problemen.</span><span class="sxs-lookup"><span data-stu-id="c8e45-160">Enabling API consumers to transparently control which backend version is being accessed by clients without having to update and redeploy clients is a elegant solution that addresses many API versioning concerns.</span></span>

## <a name="tenant-isolation"></a><span data-ttu-id="c8e45-161">Isolatie van tenants</span><span class="sxs-lookup"><span data-stu-id="c8e45-161">Tenant Isolation</span></span>
<span data-ttu-id="c8e45-162">Sommige bedrijven Maak in grotere implementaties met meerdere tenants afzonderlijke groepen van tenants voor verschillende implementaties van back-end-hardware.</span><span class="sxs-lookup"><span data-stu-id="c8e45-162">In larger, multi-tenant deployments some companies create separate groups of tenants on distinct deployments of backend hardware.</span></span> <span data-ttu-id="c8e45-163">Hiermee wordt het aantal klanten die worden beïnvloed door de hardware op de back-end geminimaliseerd.</span><span class="sxs-lookup"><span data-stu-id="c8e45-163">This minimizes the number of customers who are impacted by a hardware issue on the backend.</span></span> <span data-ttu-id="c8e45-164">Ook kunt nieuwe softwareversies voor een in fasen uit worden vernieuwd.</span><span class="sxs-lookup"><span data-stu-id="c8e45-164">It also enables new software versions to be rolled out in stages.</span></span> <span data-ttu-id="c8e45-165">Deze back-end-architectuur moet in het ideale geval transparant voor gebruikers van de API.</span><span class="sxs-lookup"><span data-stu-id="c8e45-165">Ideally this backend architecture should be transparent to API consumers.</span></span> <span data-ttu-id="c8e45-166">Dit kan worden bereikt op een vergelijkbare manier als in transparante versiebeheer omdat deze is gebaseerd op dezelfde techniek van het manipuleren van de back-end-URL met behulp van de status van de configuratie per API-sleutel.</span><span class="sxs-lookup"><span data-stu-id="c8e45-166">This can be achieved in a similar way to transparent versioning because it is based on the same technique of manipulating the backend URL using configuration state per API key.</span></span>  

<span data-ttu-id="c8e45-167">In plaats van een aanbevolen versie van de API voor elke abonnementssleutel wordt geretourneerd, zou u een id die is gekoppeld van een tenant aan de Hardwaregroep toegewezen retourneren.</span><span class="sxs-lookup"><span data-stu-id="c8e45-167">Instead of returning a preferred version of the API for each subscription key, you would return an identifier that relates a tenant to the assigned hardware group.</span></span> <span data-ttu-id="c8e45-168">Deze id kan worden gebruikt om de juiste back-end-URL samen te stellen.</span><span class="sxs-lookup"><span data-stu-id="c8e45-168">That identifier can be used to construct the appropriate backend URL.</span></span>

## <a name="summary"></a><span data-ttu-id="c8e45-169">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="c8e45-169">Summary</span></span>
<span data-ttu-id="c8e45-170">De vrijheid biedt de Azure API management-cache gebruiken voor het opslaan van elk soort gegevens kan efficiënte toegang tot de configuratiegegevens die kunnen invloed hebben op de manier die een binnenkomende aanvraag is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="c8e45-170">The freedom to use the Azure API management cache for storing any kind of data enables efficient access to configuration data that can affect the way an inbound request is processed.</span></span> <span data-ttu-id="c8e45-171">Het kan ook worden gebruikt voor het opslaan van gegevens fragmenten die reacties, geretourneerd vanuit een back-end API kunnen verbeteren.</span><span class="sxs-lookup"><span data-stu-id="c8e45-171">It can also be used to store data fragments that can augment responses, returned from a backend API.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c8e45-172">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c8e45-172">Next steps</span></span>
<span data-ttu-id="c8e45-173">Geef ons uw feedback in de Disqus-thread voor dit onderwerp als er andere scenario's die voor u deze beleidsregels hebt ingeschakeld, of als er scenario's u wilt bereiken, maar niet van mening bent dat momenteel mogelijk zijn.</span><span class="sxs-lookup"><span data-stu-id="c8e45-173">Please give us your feedback in the Disqus thread for this topic if there are other scenarios that these policies have enabled for you, or if there are scenarios you would like to achieve but do not feel are currently possible.</span></span>

