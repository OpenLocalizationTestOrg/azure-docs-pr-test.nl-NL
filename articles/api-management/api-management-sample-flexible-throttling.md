---
title: aaaAdvanced aanvraagbeperking met Azure API Management
description: Meer informatie over hoe toocreate en flexibele quota's en -beleid met Azure API Management snelheidsbeperking toe te passen.
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: fc813a65-7793-4c17-8bb9-e387838193ae
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: ac87f83118a37bd587fddf044e5c2d6fc2af9031
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-request-throttling-with-azure-api-management"></a><span data-ttu-id="ceae0-103">Geavanceerde aanvraagbeperking met Azure API Management</span><span class="sxs-lookup"><span data-stu-id="ceae0-103">Advanced request throttling with Azure API Management</span></span>
<span data-ttu-id="ceae0-104">De binnenkomende aanvragen kunnen toothrottle is een belangrijke rol van Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="ceae0-104">Being able toothrottle incoming requests is a key role of Azure API Management.</span></span> <span data-ttu-id="ceae0-105">API Management kunnen door beheren Hallo snelheid van aanvragen of Hallo totale aanvragen/gegevens overgebracht, API-providers tooprotect hun-API's van misbruik en waarde maken voor de verschillende lagen voor API-product.</span><span class="sxs-lookup"><span data-stu-id="ceae0-105">Either by controlling hello rate of requests or hello total requests/data transferred, API Management allows API providers tooprotect their APIs from abuse and create value for different API product tiers.</span></span>

## <a name="product-based-throttling"></a><span data-ttu-id="ceae0-106">Op basis van product-beperking</span><span class="sxs-lookup"><span data-stu-id="ceae0-106">Product based throttling</span></span>
<span data-ttu-id="ceae0-107">toodate, Hallo snelheid beperking mogelijkheden zijn beperkt toobeing binnen het bereik van tooa bepaald Product abonnement (in wezen een sleutel), gedefinieerd in Hallo publicatieportal van API Management.</span><span class="sxs-lookup"><span data-stu-id="ceae0-107">toodate, hello rate throttling capabilities have been limited toobeing scoped tooa particular Product subscription (essentially a key), defined in hello API Management publisher portal.</span></span> <span data-ttu-id="ceae0-108">Dit is handig voor het Hallo-provider tooapply API-limieten op Hallo-ontwikkelaars die zich hebben geregistreerd toouse hun API, echter dat niet helpt, bijvoorbeeld in afzonderlijke eindgebruikers Hallo API beperking.</span><span class="sxs-lookup"><span data-stu-id="ceae0-108">This is useful for hello API provider tooapply limits on hello developers who have signed up toouse their API, however, it does not help, for example, in throttling individual end-users of hello API.</span></span> <span data-ttu-id="ceae0-109">Het is mogelijk dat voor één gebruiker van Hallo ontwikkelaarshandleiding toepassing tooconsume Hallo gehele quota en vervolgens verhinderen andere Hallo developer-klanten kunnen toouse Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="ceae0-109">It is possible that for single user of hello developer's application tooconsume hello entire quota and then prevent other customers of hello developer from being able toouse hello application.</span></span> <span data-ttu-id="ceae0-110">Enkele klanten een groot aantal aanvragen genereren kunnen kunnen ook toegang toooccasional gebruikers te beperken.</span><span class="sxs-lookup"><span data-stu-id="ceae0-110">Also, several customers who might generate a high volume of requests may limit access toooccasional users.</span></span>

## <a name="custom-key-based-throttling"></a><span data-ttu-id="ceae0-111">Aangepaste sleutel op basis van beperking</span><span class="sxs-lookup"><span data-stu-id="ceae0-111">Custom key based throttling</span></span>
<span data-ttu-id="ceae0-112">Hallo nieuwe [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) en [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) -beleid biedt u een aanzienlijk meer flexibele oplossing tootraffic-besturingselement.</span><span class="sxs-lookup"><span data-stu-id="ceae0-112">hello new [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies provide a significantly more flexible solution tootraffic control.</span></span> <span data-ttu-id="ceae0-113">Dit nieuwe beleid kunt u toodefine expressies tooidentify Hallo sleutels die gebruikt tootrack verkeer gebruik worden.</span><span class="sxs-lookup"><span data-stu-id="ceae0-113">These new policies allow you toodefine expressions tooidentify hello keys that will be used tootrack traffic usage.</span></span> <span data-ttu-id="ceae0-114">Hallo die dit werkt wordt geïllustreerd hoe u easiest met een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="ceae0-114">hello way this works is easiest illustrated with an example.</span></span> 

## <a name="ip-address-throttling"></a><span data-ttu-id="ceae0-115">Beperking van IP-adres</span><span class="sxs-lookup"><span data-stu-id="ceae0-115">IP Address throttling</span></span>
<span data-ttu-id="ceae0-116">Hallo volgende beleid beperkt één client IP-adres tooonly 10 aanroepen elke minuut, met een totaal van 1.000.000 aanroepen en 10.000 kilobytes van bandbreedte per maand.</span><span class="sxs-lookup"><span data-stu-id="ceae0-116">hello following policies restrict a single client IP address tooonly 10 calls every minute, with a total of 1,000,000 calls and 10,000 kilobytes of bandwidth per month.</span></span> 

```xml
<rate-limit-by-key  calls="10"
          renewal-period="60"
          counter-key="@(context.Request.IpAddress)" />

<quota-by-key calls="1000000"
          bandwidth="10000"
          renewal-period="2629800"
          counter-key="@(context.Request.IpAddress)" />
```

<span data-ttu-id="ceae0-117">Als alle clients op Internet Hallo een uniek IP-adres gebruikt, dit wordt mogelijk een effectieve manier voor het beperken van gebruiksgegevens door de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="ceae0-117">If all clients on hello Internet used a unique IP address, this might be an effective way of limiting usage by user.</span></span> <span data-ttu-id="ceae0-118">Het is echter wel waarschijnlijk dat meerdere gebruikers delen één openbaar IP-adres vanwege toothem toegang tot Hallo Internet via een NAT-apparaat wordt.</span><span class="sxs-lookup"><span data-stu-id="ceae0-118">However, it is quite likely that multiple users will sharing a single public IP address due toothem accessing hello Internet via a NAT device.</span></span> <span data-ttu-id="ceae0-119">Ondanks dit voor de API's waarmee niet-geverifieerde toegang Hallo `IpAddress` mogelijk de beste optie Hallo.</span><span class="sxs-lookup"><span data-stu-id="ceae0-119">Despite this, for APIs that allow unauthenticated access hello `IpAddress` might be hello best option.</span></span>

## <a name="user-identity-throttling"></a><span data-ttu-id="ceae0-120">Gebruiker identity-beperking</span><span class="sxs-lookup"><span data-stu-id="ceae0-120">User identity throttling</span></span>
<span data-ttu-id="ceae0-121">Als een eindgebruiker is geverifieerd, wordt een bandbreedteregeling sleutel kan worden gegenereerd op basis van informatie die een unieke identificatie van een die gebruiker.</span><span class="sxs-lookup"><span data-stu-id="ceae0-121">If an end user is authenticated then a throttling key can be generated based on information that uniquely identifies an that user.</span></span>

```xml
<rate-limit-by-key calls="10"
    renewal-period="60"
    counter-key="@(context.Request.Headers.GetValueOrDefault("Authorization","").AsJwt()?.Subject)" />
```

<span data-ttu-id="ceae0-122">In dit voorbeeld we extraheren Hallo autorisatie-header, te converteren`JWT` object en onderwerp Hallo van Hallo token tooidentify Hallo gebruiker gebruiken als Hallo snelheidsbeperking-sleutel.</span><span class="sxs-lookup"><span data-stu-id="ceae0-122">In this example we extract hello Authorization header, convert it too`JWT` object and use hello subject of hello token tooidentify hello user and use that as hello rate limiting key.</span></span> <span data-ttu-id="ceae0-123">Als de identiteit van de gebruiker Hallo is opgeslagen in Hallo `JWT` als een van de Hallo andere claims vervolgens dat de waarde kan worden gebruikt in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="ceae0-123">If hello user identity is stored in hello `JWT` as one of hello other claims then that value could be used in its place.</span></span>

## <a name="combined-policies"></a><span data-ttu-id="ceae0-124">Gecombineerde beleid</span><span class="sxs-lookup"><span data-stu-id="ceae0-124">Combined policies</span></span>
<span data-ttu-id="ceae0-125">Hoewel Hallo nieuwe beperking beleidsregels meer controle dan Hallo bestaande beleidsregels voor bandbreedteregeling bieden, is er nog steeds waarde combinatie van beide mogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="ceae0-125">Although hello new throttling policies provide more control than hello existing throttling policies, there is still value combining both capabilities.</span></span> <span data-ttu-id="ceae0-126">Beperkingen door abonnement productcode ([aanroepfrequentie per abonnement](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) en [gebruiksquotum per abonnement instellen](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota)) is een uitstekende manier op tooenable monetizing van een API in rekening gebracht op basis van gebruik niveaus.</span><span class="sxs-lookup"><span data-stu-id="ceae0-126">Throttling by product subscription key ([Limit call rate by subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota by subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota)) is a great way tooenable monetizing of an API by charging based on usage levels.</span></span> <span data-ttu-id="ceae0-127">Hallo betere resultaten gedetailleerde controle over wordt kunnen toothrottle door de gebruiker is een aanvulling en voorkomt dat gedrag van een gebruiker Hallo-ervaring van een andere beïnvloeden.</span><span class="sxs-lookup"><span data-stu-id="ceae0-127">hello finer grained control of being able toothrottle by user is complementary and prevents one user's behavior from degrading hello experience of another.</span></span> 

## <a name="client-driven-throttling"></a><span data-ttu-id="ceae0-128">Client aangestuurd beperking</span><span class="sxs-lookup"><span data-stu-id="ceae0-128">Client driven throttling</span></span>
<span data-ttu-id="ceae0-129">Als Hallo beperking sleutel is gedefinieerd met behulp van een [beleidsexpressie](https://msdn.microsoft.com/library/azure/dn910913.aspx), dan is het Hallo-API-provider die is kiezen hoe Hallo beperking ligt binnen het bereik.</span><span class="sxs-lookup"><span data-stu-id="ceae0-129">When hello throttling key is defined using a [policy expression](https://msdn.microsoft.com/library/azure/dn910913.aspx), then it is hello API provider that is choosing how hello throttling is scoped.</span></span> <span data-ttu-id="ceae0-130">Een ontwikkelaar mogelijk wilt echter toocontrol hoe ze beoordelen beperken hun eigen klanten.</span><span class="sxs-lookup"><span data-stu-id="ceae0-130">However, a developer might want toocontrol how they rate limit their own customers.</span></span> <span data-ttu-id="ceae0-131">Dit kan worden ingeschakeld door Hallo API provider door de introductie van een aangepaste header tooallow Hallo ontwikkelaar client toepassing toocommunicate Hallo sleutel toohello API.</span><span class="sxs-lookup"><span data-stu-id="ceae0-131">This could be enabled by hello API provider by introducing a custom header tooallow hello developer's client application toocommunicate hello key toohello API.</span></span>

```xml
<rate-limit-by-key calls="100"
          renewal-period="60"
          counter-key="@(request.Headers.GetValueOrDefault("Rate-Key",""))"/>
```

<span data-ttu-id="ceae0-132">Hierdoor kunnen Hallo ontwikkelaarshandleiding client toepassing toochoose hoe ze willen toocreate Hallo snelheidsbeperking sleutel.</span><span class="sxs-lookup"><span data-stu-id="ceae0-132">This enables hello developer's client application toochoose how they want toocreate hello rate limiting key.</span></span> <span data-ttu-id="ceae0-133">Met een beetje draaien kan een ontwikkelaar client hun eigen niveaus tarief maken door sets met sleutels toousers toewijzen en roteren Hallo sleutelgebruik.</span><span class="sxs-lookup"><span data-stu-id="ceae0-133">With a little bit of ingenuity a client developer could create their own rate tiers by allocating sets of keys toousers and rotating hello key usage.</span></span>

## <a name="summary"></a><span data-ttu-id="ceae0-134">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="ceae0-134">Summary</span></span>
<span data-ttu-id="ceae0-135">Azure API Management biedt snelheid en beperking tooboth aanhalingsteken beveiligen en waarde tooyour API-service toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ceae0-135">Azure API Management provides rate and quote throttling tooboth protect and add value tooyour API service.</span></span> <span data-ttu-id="ceae0-136">Hallo nieuwe beperking beleidsregels met aangepaste bereik regels kunt dat u meer controle over deze beleidsregels tooenable geslaagde uw klanten toobuild nog beter toepassingen.</span><span class="sxs-lookup"><span data-stu-id="ceae0-136">hello new throttling policies with custom scoping rules allow you finer grained control over those policies tooenable your customers toobuild even better applications.</span></span> <span data-ttu-id="ceae0-137">Hallo-voorbeelden in dit artikel worden Hallo gebruik van dit nieuwe beleid door productie snelheidsbeperking-sleutels met client-IP-adressen, gebruikers-id en waarden van de client gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="ceae0-137">hello examples in this article demonstrate hello use of these new policies by manufacturing rate limiting keys with client IP addresses, user identity, and client generated values.</span></span> <span data-ttu-id="ceae0-138">Er zijn echter veel andere onderdelen van het Hallo-bericht die kunnen worden gebruikt zoals gebruikersagent, fragmenten voor URL-pad, de grootte van het bericht.</span><span class="sxs-lookup"><span data-stu-id="ceae0-138">However, there are many other parts of hello message that could be used such as user agent, URL path fragments, message size.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ceae0-139">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ceae0-139">Next steps</span></span>
<span data-ttu-id="ceae0-140">Geef ons uw feedback in Hallo Disqus-thread voor dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="ceae0-140">Please give us your feedback in hello Disqus thread for this topic.</span></span> <span data-ttu-id="ceae0-141">Het normaal zou zijn goede toohear over andere mogelijke sleutelwaarden die logische keuze in uw scenario's zijn.</span><span class="sxs-lookup"><span data-stu-id="ceae0-141">It would be great toohear about other potential key values that have been a logical choice in your scenarios.</span></span>

## <a name="watch-a-video-overview-of-these-policies"></a><span data-ttu-id="ceae0-142">Bekijk een video-overzicht van deze beleidsregels</span><span class="sxs-lookup"><span data-stu-id="ceae0-142">Watch a video overview of these policies</span></span>
<span data-ttu-id="ceae0-143">Voor meer informatie over Hallo [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) en [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) beleidsregels die in dit artikel, neem Hallo volgende video bekijken.</span><span class="sxs-lookup"><span data-stu-id="ceae0-143">For more information on hello [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies covered in this article, please watch hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Advanced-Request-Throttling-with-Azure-API-Management/player]
> 
> 

