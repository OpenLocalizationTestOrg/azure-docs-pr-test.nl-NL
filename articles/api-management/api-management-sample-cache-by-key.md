---
title: aaaCustom opslaan in cache in Azure API Management
description: Meer informatie over hoe toocache items door de sleutel in Azure API Management
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
ms.openlocfilehash: 681380743c8c96af5d0a8e25948a8c0663e9fd35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="custom-caching-in-azure-api-management"></a><span data-ttu-id="b989e-103">Aangepaste opslaan in cache in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="b989e-103">Custom caching in Azure API Management</span></span>
<span data-ttu-id="b989e-104">Azure API Management-service biedt ingebouwde ondersteuning voor [HTTP-antwoord in cache opslaan](api-management-howto-cache.md) Hallo bron-URL als Hallo sleutel gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b989e-104">Azure API Management service has built-in support for [HTTP response caching](api-management-howto-cache.md) using hello resource URL as hello key.</span></span> <span data-ttu-id="b989e-105">Hallo sleutel kan worden gewijzigd door aanvraagheaders Hallo met `vary-by` eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="b989e-105">hello key can be modified by request headers using hello `vary-by` properties.</span></span> <span data-ttu-id="b989e-106">Dit is handig voor het opslaan van de hele HTTP-antwoorden (aka verklaringen), maar soms is het nuttig toojust cache een deel van een weergave.</span><span class="sxs-lookup"><span data-stu-id="b989e-106">This is useful for caching entire HTTP responses (aka representations), but sometimes it is useful toojust cache a portion of a representation.</span></span> <span data-ttu-id="b989e-107">Hallo nieuwe [cache zoekwaarde](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) en [cache-store-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) -beleid biedt de mogelijkheid Hallo willekeurige stukken toostore en ophalen van gegevens vanuit beleidsdefinities.</span><span class="sxs-lookup"><span data-stu-id="b989e-107">hello new [cache-lookup-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) and [cache-store-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) policies provide hello ability toostore and retrieve arbitrary pieces of data from within policy definitions.</span></span> <span data-ttu-id="b989e-108">Deze mogelijkheid voegt ook waarde toohello eerder geïntroduceerd [aanvragen verzenden](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) beleid omdat u kunt nu antwoorden van externe services cache.</span><span class="sxs-lookup"><span data-stu-id="b989e-108">This ability also adds value toohello previously introduced [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) policy because you can now cache responses from external services.</span></span>

## <a name="architecture"></a><span data-ttu-id="b989e-109">Architectuur</span><span class="sxs-lookup"><span data-stu-id="b989e-109">Architecture</span></span>
<span data-ttu-id="b989e-110">API Management-service wordt gebruikgemaakt van een gedeelde tenant gegevenscache zodat terwijl u toomultiple eenheden schaalt worden er nog steeds toegang toohello dezelfde gegevens uit de cache.</span><span class="sxs-lookup"><span data-stu-id="b989e-110">API Management service uses a shared per-tenant data cache so that, as you scale up toomultiple units you will still get access toohello same cached data.</span></span> <span data-ttu-id="b989e-111">Als u werkt met een implementatie met meerdere regio zijn er echter onafhankelijke caches in elk Hallo regio's.</span><span class="sxs-lookup"><span data-stu-id="b989e-111">However, when working with a multi-region deployment there are independent caches within each of hello regions.</span></span> <span data-ttu-id="b989e-112">Vervaldatum toothis, is het belangrijk toonot Hallo cache behandelen als een gegevensarchief, waar is de enige bron Hallo van sommige stukje informatie.</span><span class="sxs-lookup"><span data-stu-id="b989e-112">Due toothis, it is important toonot treat hello cache as a data store, where it is hello only source of some piece of information.</span></span> <span data-ttu-id="b989e-113">Als u hebt en later tootake profiteren van de implementatie van Hallo meerdere landen/regio besloten, kunnen toegang toothat in de cache opgeslagen gegevens verliezen door klanten met gebruikers die worden uitgewisseld.</span><span class="sxs-lookup"><span data-stu-id="b989e-113">If you did, and later decided tootake advantage of hello multi-region deployment, then customers with users that travel may lose access toothat cached data.</span></span>

## <a name="fragment-caching"></a><span data-ttu-id="b989e-114">Fragment opslaan in cache</span><span class="sxs-lookup"><span data-stu-id="b989e-114">Fragment caching</span></span>
<span data-ttu-id="b989e-115">Er zijn bepaalde gevallen waarbij antwoorden wordt geretourneerd een gedeelte van de gegevens die dure toodetermine is en nog blijft vers voor een redelijk tijdsbestek bevatten.</span><span class="sxs-lookup"><span data-stu-id="b989e-115">There are certain cases where responses being returned contain some portion of data that is expensive toodetermine and yet remains fresh for a reasonable amount of time.</span></span> <span data-ttu-id="b989e-116">Een voorbeeld kunt u een service die is gebouwd door een luchtvaartmaatschappij die voorziet in informatie over Vluchtreserveringen, vlucht status, enzovoort. Als het Hallo-gebruiker is lid van Hallo airlines punten programma, zou moeten ook informatie over de huidige status van tootheir en kilometers verzameld.</span><span class="sxs-lookup"><span data-stu-id="b989e-116">As an example, consider a service built by an airline that provides information relating flight reservations, flight status, etc. If hello user is a member of hello airlines points program, they would also have information relating tootheir current status and mileage accumulated.</span></span> <span data-ttu-id="b989e-117">Deze gebruiker-gerelateerde gegevens worden opgeslagen in een ander systeem, maar deze is mogelijk wenselijk tooinclude in antwoorden over de status van de vlucht en -reserveringen geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b989e-117">This user-related information might be stored in a different system, but it may be desirable tooinclude it in responses returned about flight status and reservations.</span></span> <span data-ttu-id="b989e-118">U kunt dit doen via een proces genaamd fragment opslaan in cache.</span><span class="sxs-lookup"><span data-stu-id="b989e-118">This can be done using a process called fragment caching.</span></span> <span data-ttu-id="b989e-119">Hallo kan primaire weergave worden geretourneerd van de bronserver Hallo met een soort token tooindicate waarbij Hallo gebruiker-gerelateerde informatie toobe ingevoegd.</span><span class="sxs-lookup"><span data-stu-id="b989e-119">hello primary representation can be returned from hello origin server using some kind of token tooindicate where hello user-related information is toobe inserted.</span></span> 

<span data-ttu-id="b989e-120">Overweeg het volgende JSON-antwoord van een back-end API Hallo.</span><span class="sxs-lookup"><span data-stu-id="b989e-120">Consider hello following JSON response from a backend API.</span></span>

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

<span data-ttu-id="b989e-121">En secundaire bron ingesteld op `/userprofile/{userid}` die vergelijkbaar is,</span><span class="sxs-lookup"><span data-stu-id="b989e-121">And secondary resource at `/userprofile/{userid}` that looks like,</span></span>

```json
{ "username" : "Bob Smith", "Status" : "Gold" }
```

<span data-ttu-id="b989e-122">In de volgorde toodetermine Hallo betreffende informatie tooinclude moeten we tooidentify die de eindgebruiker Hallo is.</span><span class="sxs-lookup"><span data-stu-id="b989e-122">In order toodetermine hello appropriate user information tooinclude, we need tooidentify who hello end user is.</span></span> <span data-ttu-id="b989e-123">Dit mechanisme is afhankelijke-implementatie.</span><span class="sxs-lookup"><span data-stu-id="b989e-123">This mechanism is implementation dependent.</span></span> <span data-ttu-id="b989e-124">Als u bijvoorbeeld ik Hallo gebruik `Subject` claimen van een `JWT` token.</span><span class="sxs-lookup"><span data-stu-id="b989e-124">As an example, I am using hello `Subject` claim of a `JWT` token.</span></span> 

```xml
<set-variable
  name="enduserid"
  value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />
```

<span data-ttu-id="b989e-125">Zo bewaren wij dit `enduserid` waarde in een variabele context voor later gebruik.</span><span class="sxs-lookup"><span data-stu-id="b989e-125">We store this `enduserid` value in a context variable for later use.</span></span> <span data-ttu-id="b989e-126">de volgende stap Hallo is toodetermine als een eerdere aanvraag al Hallo gebruikersgegevens opgehaald en opgeslagen in cache Hallo.</span><span class="sxs-lookup"><span data-stu-id="b989e-126">hello next step is toodetermine if a previous request has already retrieved hello user information and stored it in hello cache.</span></span> <span data-ttu-id="b989e-127">Voor deze gebruiken we Hallo `cache-lookup-value` beleid.</span><span class="sxs-lookup"><span data-stu-id="b989e-127">For this we use hello `cache-lookup-value` policy.</span></span>

```xml
<cache-lookup-value
key="@("userprofile-" + context.Variables["enduserid"])"
variable-name="userprofile" />
```

<span data-ttu-id="b989e-128">Als er is geen vermelding in de cache Hallo die overeenkomt met de sleutelwaarde toohello en klik op Nee `userprofile` context variabele wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b989e-128">If there is no entry in hello cache that corresponds toohello key value, then no `userprofile` context variable will be created.</span></span> <span data-ttu-id="b989e-129">We controleren of Hallo geslaagd van Hallo zoeken met behulp van Hallo `choose` beleid overdrachten beheren.</span><span class="sxs-lookup"><span data-stu-id="b989e-129">We check hello success of hello lookup using hello `choose` control flow policy.</span></span>

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("userprofile"))">
        <!-- If hello userprofile context variable doesn’t exist, make an HTTP request tooretrieve it.  -->
    </when>
</choose>
```

<span data-ttu-id="b989e-130">Als hello `userprofile` context variabele bestaat niet en gaat toohave toomake een HTTP-aanvraag tooretrieve worden deze.</span><span class="sxs-lookup"><span data-stu-id="b989e-130">If hello `userprofile` context variable doesn’t exist, then we are going toohave toomake an HTTP request tooretrieve it.</span></span>

```xml
<send-request
  mode="new"
  response-variable-name="userprofileresponse"
  timeout="10"
  ignore-error="true">

  <!-- Build a URL that points toohello profile for hello current end-user -->
  <set-url>@(new Uri(new Uri("https://apimairlineapi.azurewebsites.net/UserProfile/"),
      (string)context.Variables["enduserid"]).AbsoluteUri)
  </set-url>
  <set-method>GET</set-method>
</send-request>
```

<span data-ttu-id="b989e-131">We gebruiken Hallo `enduserid` tooconstruct Hallo URL toohello gebruiker profiel resource.</span><span class="sxs-lookup"><span data-stu-id="b989e-131">We use hello `enduserid` tooconstruct hello URL toohello user profile resource.</span></span> <span data-ttu-id="b989e-132">Zodra er antwoord Hallo hebt, kunnen we pull-hallo platte tekst buiten het antwoord Hallo en sla deze terug in een context-variabele.</span><span class="sxs-lookup"><span data-stu-id="b989e-132">Once we have hello response, we can pull hello body text out of hello response and store it back into a context variable.</span></span>

```xml
<set-variable
    name="userprofile"
    value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />
```

<span data-ttu-id="b989e-133">tooavoid ons met toomake deze HTTP-aanvraag opnieuw wanneer hello dezelfde gebruiker een andere aanvraag indient, we kunt opslaan Hallo gebruikersprofiel in cache Hallo.</span><span class="sxs-lookup"><span data-stu-id="b989e-133">tooavoid us having toomake this HTTP request again, when hello same user makes another request, we can store hello user profile in hello cache.</span></span>

```xml
<cache-store-value
    key="@("userprofile-" + context.Variables["enduserid"])"
    value="@((string)context.Variables["userprofile"])" duration="100000" />
```

<span data-ttu-id="b989e-134">Hallo waarde opgeslagen in het Hallo-cache met behulp van Hallo exact dezelfde sleutel dat we tooretrieve oorspronkelijk heeft geprobeerd deze met.</span><span class="sxs-lookup"><span data-stu-id="b989e-134">We store hello value in hello cache using hello exact same key that we originally attempted tooretrieve it with.</span></span> <span data-ttu-id="b989e-135">Hallo moet duur die we toostore Hallo waarde kiezen zijn gebaseerd op hoe vaak hello informatie wijzigingen en over hoe fouttolerante gebruikers tooout van actuele informatie worden.</span><span class="sxs-lookup"><span data-stu-id="b989e-135">hello duration that we choose toostore hello value should be based on how often hello information changes and how tolerant users are tooout of date information.</span></span> 

<span data-ttu-id="b989e-136">Het is belangrijk toorealize dat ophalen uit de cache Hallo nog steeds een out-of-process, een aanvraag voor het netwerk en mogelijk kan nog wel toevoegen tientallen van milliseconden toohello aanvraag.</span><span class="sxs-lookup"><span data-stu-id="b989e-136">It is important toorealize that retrieving from hello cache is still an out-of-process, network request and potentially can still add tens of milliseconds toohello request.</span></span> <span data-ttu-id="b989e-137">Hallo voordelen wanneer bepalende Hallo gebruikersprofielgegevens aanzienlijk langer dan die vervaldatum tooneeding toodo databasequery's of statistische gegevens uit meerdere back-ends duurt worden geleverd.</span><span class="sxs-lookup"><span data-stu-id="b989e-137">hello benefits come when determining hello user profile information takes significantly longer than that due tooneeding toodo database queries or aggregate information from multiple back-ends.</span></span>

<span data-ttu-id="b989e-138">Hallo is laatste stap bij het Hallo-proces tooupdate Hallo antwoord met onze gebruikersprofielgegevens geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b989e-138">hello final step in hello process is tooupdate hello returned response with our user profile information.</span></span>

```xml
<!-- Update response body with user profile-->
<find-and-replace
    from='"$userprofile$"'
    to="@((string)context.Variables["userprofile"])" />
```

<span data-ttu-id="b989e-139">Ik heb gekozen tooinclude Hallo tussen aanhalingstekens als onderdeel van Hallo token zodat zelfs wanneer Hallo vervangen niet wordt uitgevoerd, Hallo antwoord nog geldig JSON is.</span><span class="sxs-lookup"><span data-stu-id="b989e-139">I chose tooinclude hello quotation marks as part of hello token so that even when hello replace doesn’t occur, hello response was still valid JSON.</span></span> <span data-ttu-id="b989e-140">Dit is vooral toomake foutopsporing gemakkelijker.</span><span class="sxs-lookup"><span data-stu-id="b989e-140">This was primarily toomake debugging easier.</span></span>

<span data-ttu-id="b989e-141">Als u al deze stappen samen combineren, is het eindresultaat Hallo een beleid dat lijkt op Hallo na een.</span><span class="sxs-lookup"><span data-stu-id="b989e-141">Once you combine all these steps together, hello end result is a policy that looks like hello following one.</span></span>

```xml
<policies>
    <inbound>
        <!-- How you determine user identity is application dependent -->
        <set-variable
          name="enduserid"
          value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />

        <!--Look for userprofile for this user in hello cache -->
        <cache-lookup-value
          key="@("userprofile-" + context.Variables["enduserid"])"
          variable-name="userprofile" />

        <!-- If we don’t find it in hello cache, make a request for it and store it -->
        <choose>
            <when condition="@(!context.Variables.ContainsKey("userprofile"))">
                <!-- Make HTTP request tooget user profile -->
                <send-request
                  mode="new"
                  response-variable-name="userprofileresponse"
                  timeout="10"
                  ignore-error="true">

                   <!-- Build a URL that points toohello profile for hello current end-user -->
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

<span data-ttu-id="b989e-142">Deze cache benadering wordt voornamelijk gebruikt in websites waar HTML bestaat aan serverzijde Hallo zodat deze kan worden gerenderd als één pagina.</span><span class="sxs-lookup"><span data-stu-id="b989e-142">This caching approach is primarily used in web sites where HTML is composed on hello server side so that it can be rendered as a single page.</span></span> <span data-ttu-id="b989e-143">Maar dit kan ook nuttig zijn in API's waar clients client kunnen niet aan de objectkant HTTP opslaan in cache of het wenselijk is niet tooput verantwoordelijkheid op Hallo-client.</span><span class="sxs-lookup"><span data-stu-id="b989e-143">However, it can also be useful in APIs where clients cannot do client side HTTP caching or it is desirable not tooput that responsibility on hello client.</span></span>

<span data-ttu-id="b989e-144">Dit dezelfde soort fragment opslaan in cache kan ook worden uitgevoerd op Hallo back-end-webservers met behulp van een in Redis cache van de server, echter met behulp van Hallo API Management-service tooperform dit werk is nuttig wanneer in de cache opgeslagen Hallo fragmenten afkomstig zijn uit verschillende back-ends dan Hallo primaire antwoorden.</span><span class="sxs-lookup"><span data-stu-id="b989e-144">This same kind of fragment caching can also be done on hello backend web servers using a Redis caching server, however, using hello API Management service tooperform this work is useful when hello cached fragments are coming from different back-ends than hello primary responses.</span></span>

## <a name="transparent-versioning"></a><span data-ttu-id="b989e-145">Transparante versiebeheer</span><span class="sxs-lookup"><span data-stu-id="b989e-145">Transparent versioning</span></span>
<span data-ttu-id="b989e-146">Het is gebruikelijk om voor meerdere versies van de andere implementatie van een API-toobe op elk gewenst moment ondersteund.</span><span class="sxs-lookup"><span data-stu-id="b989e-146">It is common practice for multiple different implementation versions of an API toobe supported at any one time.</span></span> <span data-ttu-id="b989e-147">Dit is mogelijk toosupport verschillende omgevingen, zoals ontwikkelen, testen, productie, enzovoort, of wordt mogelijk toosupport oudere versies van Hallo API toogive tijd voor de API consumenten toomigrate toonewer-versies.</span><span class="sxs-lookup"><span data-stu-id="b989e-147">This is perhaps toosupport different environments, like dev, test, production, etc, or it may be toosupport older versions of hello API toogive time for API consumers toomigrate toonewer versions.</span></span> 

<span data-ttu-id="b989e-148">Een aanpak toohandling dit in plaats daarvan van client ontwikkelaars toochange Hallo URL's van vereisen `/v1/customers` te`/v2/customers` is toostore in van de consumer Hallo profielgegevens welke versie van Hallo API ze momenteel wilt toouse en Hallo juiste aanroepen back-end-URL.</span><span class="sxs-lookup"><span data-stu-id="b989e-148">One approach toohandling this instead of requiring client developers toochange hello URLs from `/v1/customers` too`/v2/customers` is toostore in hello consumer’s profile data which version of hello API they currently wish toouse and call hello appropriate backend URL.</span></span> <span data-ttu-id="b989e-149">In de volgorde toodetermine Hallo juiste back-end URL toocall voor een bepaalde client, is het nodig tooquery Sommige configuratiegegevens.</span><span class="sxs-lookup"><span data-stu-id="b989e-149">In order toodetermine hello correct backend URL toocall for a particular client, it is necessary tooquery some configuration data.</span></span> <span data-ttu-id="b989e-150">Door deze configuratiegegevens caching, kunnen we Hallo op de prestaties van de handeling deze zoekactie minimaliseren.</span><span class="sxs-lookup"><span data-stu-id="b989e-150">By caching this configuration data, we can minimize hello performance penalty of doing this lookup.</span></span>

<span data-ttu-id="b989e-151">de eerste stap Hallo is toodetermine Hallo id tooconfigure Hallo gewenste versie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b989e-151">hello first step is toodetermine hello identifier used tooconfigure hello desired version.</span></span> <span data-ttu-id="b989e-152">In dit voorbeeld gekozen ik tooassociate Hallo versie toohello abonnement-productcode.</span><span class="sxs-lookup"><span data-stu-id="b989e-152">In this example, I chose tooassociate hello version toohello product subscription key.</span></span> 

```xml
<set-variable name="clientid" value="@(context.Subscription.Key)" />
```

<span data-ttu-id="b989e-153">We doen een cache lookup toosee vervolgens als we de gewenste clientversie Hallo al hebt opgehaald.</span><span class="sxs-lookup"><span data-stu-id="b989e-153">We then do a cache lookup toosee if we already have retrieved hello desired client version.</span></span>

```xml
<cache-lookup-value
key="@("clientversion-" + context.Variables["clientid"])"
variable-name="clientversion" />
```

<span data-ttu-id="b989e-154">Vervolgens controleren we toosee als we het niet in cache Hallo vinden is.</span><span class="sxs-lookup"><span data-stu-id="b989e-154">Then we check toosee if we did not find it in hello cache.</span></span>

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("clientversion"))">
```

<span data-ttu-id="b989e-155">Als we niet we gaan en dit ophalen.</span><span class="sxs-lookup"><span data-stu-id="b989e-155">If we didn’t then we go and retrieve it.</span></span>

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

<span data-ttu-id="b989e-156">Hallo antwoord platte tekst uit het antwoord Hallo extraheren.</span><span class="sxs-lookup"><span data-stu-id="b989e-156">Extract hello response body text from hello response.</span></span>

```xml
<set-variable
      name="clientversion"
      value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
```

<span data-ttu-id="b989e-157">Opslaan in cache Hallo voor toekomstig gebruik.</span><span class="sxs-lookup"><span data-stu-id="b989e-157">Store it back in hello cache for future use.</span></span>

```xml
<cache-store-value
      key="@("clientversion-" + context.Variables["clientid"])"
      value="@((string)context.Variables["clientversion"])"
      duration="100000" />
```

<span data-ttu-id="b989e-158">En ten slotte Hallo back-end URL tooselect Hallo versie van Hallo service gewenst door Hallo client bijwerken.</span><span class="sxs-lookup"><span data-stu-id="b989e-158">And finally update hello back-end URL tooselect hello version of hello service desired by hello client.</span></span>

```xml
<set-backend-service
      base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
```

<span data-ttu-id="b989e-159">Hallo is volledig beleid als volgt.</span><span class="sxs-lookup"><span data-stu-id="b989e-159">hello completely policy is as follows.</span></span>

```xml
<inbound>
    <base />
    <set-variable name="clientid" value="@(context.Subscription.Key)" />
    <cache-lookup-value key="@("clientversion-" + context.Variables["clientid"])" variable-name="clientversion" />

    <!-- If we don’t find it in hello cache, make a request for it and store it -->
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

<span data-ttu-id="b989e-160">Inschakelen van welke endversie van de back-om wordt geopend door clients zonder tooupdate en de implementatie opnieuw clients van consumenten tootransparently-beheer op API is een elegante oplossing die zijn gericht op veel API versioning problemen.</span><span class="sxs-lookup"><span data-stu-id="b989e-160">Enabling API consumers tootransparently control which backend version is being accessed by clients without having tooupdate and redeploy clients is a elegant solution that addresses many API versioning concerns.</span></span>

## <a name="tenant-isolation"></a><span data-ttu-id="b989e-161">Isolatie van tenants</span><span class="sxs-lookup"><span data-stu-id="b989e-161">Tenant Isolation</span></span>
<span data-ttu-id="b989e-162">Sommige bedrijven Maak in grotere implementaties met meerdere tenants afzonderlijke groepen van tenants voor verschillende implementaties van back-end-hardware.</span><span class="sxs-lookup"><span data-stu-id="b989e-162">In larger, multi-tenant deployments some companies create separate groups of tenants on distinct deployments of backend hardware.</span></span> <span data-ttu-id="b989e-163">Dit minimaliseert aantal klanten die worden beïnvloed door een hardwareprobleem op Hallo backend Hallo.</span><span class="sxs-lookup"><span data-stu-id="b989e-163">This minimizes hello number of customers who are impacted by a hardware issue on hello backend.</span></span> <span data-ttu-id="b989e-164">Ook kunt nieuwe software versies toobe uitgerold in fasen uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b989e-164">It also enables new software versions toobe rolled out in stages.</span></span> <span data-ttu-id="b989e-165">Deze back-end-architectuur moet in het ideale geval transparante tooAPI consumenten.</span><span class="sxs-lookup"><span data-stu-id="b989e-165">Ideally this backend architecture should be transparent tooAPI consumers.</span></span> <span data-ttu-id="b989e-166">Dit kan worden bereikt in een vergelijkbare manier tootransparent versioning omdat deze is gebaseerd op Hallo dezelfde techniek van het manipuleren van Hallo back-end-URL met behulp van de status van de configuratie per API-sleutel.</span><span class="sxs-lookup"><span data-stu-id="b989e-166">This can be achieved in a similar way tootransparent versioning because it is based on hello same technique of manipulating hello backend URL using configuration state per API key.</span></span>  

<span data-ttu-id="b989e-167">In plaats van een aanbevolen versie van Hallo API voor elke abonnementssleutel wordt geretourneerd, zou u een id die is gekoppeld van een tenant toohello toegewezen Hardwaregroep retourneren.</span><span class="sxs-lookup"><span data-stu-id="b989e-167">Instead of returning a preferred version of hello API for each subscription key, you would return an identifier that relates a tenant toohello assigned hardware group.</span></span> <span data-ttu-id="b989e-168">Deze id kan worden gebruikt tooconstruct Hallo juiste back-end-URL.</span><span class="sxs-lookup"><span data-stu-id="b989e-168">That identifier can be used tooconstruct hello appropriate backend URL.</span></span>

## <a name="summary"></a><span data-ttu-id="b989e-169">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="b989e-169">Summary</span></span>
<span data-ttu-id="b989e-170">Hallo vrijheid toouse hello Azure API management-cache voor het opslaan van elk soort gegevens kan efficiënte toegang tooconfiguration gegevens die kunnen invloed hebben op Hallo manier die een binnenkomende aanvraag is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="b989e-170">hello freedom toouse hello Azure API management cache for storing any kind of data enables efficient access tooconfiguration data that can affect hello way an inbound request is processed.</span></span> <span data-ttu-id="b989e-171">Het kan ook worden de gebruikte toostore gegevens fragmenten die reacties, geretourneerd vanuit een back-end API kunnen verbeteren.</span><span class="sxs-lookup"><span data-stu-id="b989e-171">It can also be used toostore data fragments that can augment responses, returned from a backend API.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b989e-172">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b989e-172">Next steps</span></span>
<span data-ttu-id="b989e-173">Geef ons uw feedback in Hallo Disqus-thread voor dit onderwerp als er andere scenario's dat deze beleidsregels hebt ingeschakeld voor u, of als er scenario's u wilt tooachieve, maar kan niet van mening bent dat momenteel mogelijk zijn.</span><span class="sxs-lookup"><span data-stu-id="b989e-173">Please give us your feedback in hello Disqus thread for this topic if there are other scenarios that these policies have enabled for you, or if there are scenarios you would like tooachieve but do not feel are currently possible.</span></span>

