---
title: Geavanceerde aanvraagbeperking met Azure API Management
description: Informatie over het maken en toepassen van flexibele quota's en snelheidsbeperking beleid met Azure API Management.
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
ms.openlocfilehash: 35375e599891a9443a91c4c3a8657e8c9c48c7b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="advanced-request-throttling-with-azure-api-management"></a><span data-ttu-id="02ada-103">Geavanceerde aanvraagbeperking met Azure API Management</span><span class="sxs-lookup"><span data-stu-id="02ada-103">Advanced request throttling with Azure API Management</span></span>
<span data-ttu-id="02ada-104">Om te beperken van binnenkomende aanvragen kunnen is een belangrijke functie van Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="02ada-104">Being able to throttle incoming requests is a key role of Azure API Management.</span></span> <span data-ttu-id="02ada-105">Een door de snelheid van aanvragen of de totale aanvragen/gegevensoverdracht te beheren, kunt API Management API-providers voor hun-API's beveiligen tegen misbruik en waarde maken voor de verschillende lagen voor API-product.</span><span class="sxs-lookup"><span data-stu-id="02ada-105">Either by controlling the rate of requests or the total requests/data transferred, API Management allows API providers to protect their APIs from abuse and create value for different API product tiers.</span></span>

## <a name="product-based-throttling"></a><span data-ttu-id="02ada-106">Op basis van product-beperking</span><span class="sxs-lookup"><span data-stu-id="02ada-106">Product based throttling</span></span>
<span data-ttu-id="02ada-107">Op dit moment, de frequentie waarmee beperking zijn mogelijkheden beperkt tot wordt binnen het bereik van een bepaald Product-abonnement (in wezen een sleutel), gedefinieerd in de publicatieportal van API Management.</span><span class="sxs-lookup"><span data-stu-id="02ada-107">To date, the rate throttling capabilities have been limited to being scoped to a particular Product subscription (essentially a key), defined in the API Management publisher portal.</span></span> <span data-ttu-id="02ada-108">Dit is handig voor de API-provider beperkingen toepassen op de ontwikkelaars die zich hebben geregistreerd hun API gebruiken, echter dat niet helpt, bijvoorbeeld in een beperking van afzonderlijke eindgebruikers van de API.</span><span class="sxs-lookup"><span data-stu-id="02ada-108">This is useful for the API provider to apply limits on the developers who have signed up to use their API, however, it does not help, for example, in throttling individual end-users of the API.</span></span> <span data-ttu-id="02ada-109">Het is mogelijk dat voor één gebruiker van de toepassing van de ontwikkelaar het hele quotum gebruiken en vervolgens te voorkomen dat andere klanten van de ontwikkelaar kan de toepassing gebruiken.</span><span class="sxs-lookup"><span data-stu-id="02ada-109">It is possible that for single user of the developer's application to consume the entire quota and then prevent other customers of the developer from being able to use the application.</span></span> <span data-ttu-id="02ada-110">Enkele klanten een groot aantal aanvragen genereren kunnen kunnen ook toegang tot incidentele gebruikers te beperken.</span><span class="sxs-lookup"><span data-stu-id="02ada-110">Also, several customers who might generate a high volume of requests may limit access to occasional users.</span></span>

## <a name="custom-key-based-throttling"></a><span data-ttu-id="02ada-111">Aangepaste sleutel op basis van beperking</span><span class="sxs-lookup"><span data-stu-id="02ada-111">Custom key based throttling</span></span>
<span data-ttu-id="02ada-112">De nieuwe [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) en [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) -beleid biedt u een aanzienlijk meer flexibele oplossing voor beheer van netwerkverkeer.</span><span class="sxs-lookup"><span data-stu-id="02ada-112">The new [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies provide a significantly more flexible solution to traffic control.</span></span> <span data-ttu-id="02ada-113">Dit nieuwe beleid kunt u voor het definiëren van expressies voor het aanduiden van de sleutels die worden gebruikt voor het bijhouden van gebruik van verkeer.</span><span class="sxs-lookup"><span data-stu-id="02ada-113">These new policies allow you to define expressions to identify the keys that will be used to track traffic usage.</span></span> <span data-ttu-id="02ada-114">De manier waarop die dit werkt wordt easiest weergegeven met een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="02ada-114">The way this works is easiest illustrated with an example.</span></span> 

## <a name="ip-address-throttling"></a><span data-ttu-id="02ada-115">Beperking van IP-adres</span><span class="sxs-lookup"><span data-stu-id="02ada-115">IP Address throttling</span></span>
<span data-ttu-id="02ada-116">De volgende beleidsregels voor beperken een IP-adres van één client tot alleen 10 aanroepen elke minuut, met een totaal van 1.000.000 aanroepen en 10.000 kilobytes van bandbreedte per maand.</span><span class="sxs-lookup"><span data-stu-id="02ada-116">The following policies restrict a single client IP address to only 10 calls every minute, with a total of 1,000,000 calls and 10,000 kilobytes of bandwidth per month.</span></span> 

```xml
<rate-limit-by-key  calls="10"
          renewal-period="60"
          counter-key="@(context.Request.IpAddress)" />

<quota-by-key calls="1000000"
          bandwidth="10000"
          renewal-period="2629800"
          counter-key="@(context.Request.IpAddress)" />
```

<span data-ttu-id="02ada-117">Als alle clients op het Internet een uniek IP-adres gebruikt, dit wordt mogelijk een effectieve manier voor het beperken van gebruiksgegevens door de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="02ada-117">If all clients on the Internet used a unique IP address, this might be an effective way of limiting usage by user.</span></span> <span data-ttu-id="02ada-118">Het is echter wel waarschijnlijk dat meerdere gebruikers delen één openbaar IP-adres omdat ze toegang tot Internet via een NAT-apparaat wordt.</span><span class="sxs-lookup"><span data-stu-id="02ada-118">However, it is quite likely that multiple users will sharing a single public IP address due to them accessing the Internet via a NAT device.</span></span> <span data-ttu-id="02ada-119">Ondanks dit voor de API's waarmee niet-geverifieerde toegang tot de `IpAddress` mogelijk de beste optie.</span><span class="sxs-lookup"><span data-stu-id="02ada-119">Despite this, for APIs that allow unauthenticated access the `IpAddress` might be the best option.</span></span>

## <a name="user-identity-throttling"></a><span data-ttu-id="02ada-120">Gebruiker identity-beperking</span><span class="sxs-lookup"><span data-stu-id="02ada-120">User identity throttling</span></span>
<span data-ttu-id="02ada-121">Als een eindgebruiker is geverifieerd, wordt een bandbreedteregeling sleutel kan worden gegenereerd op basis van informatie die een unieke identificatie van een die gebruiker.</span><span class="sxs-lookup"><span data-stu-id="02ada-121">If an end user is authenticated then a throttling key can be generated based on information that uniquely identifies an that user.</span></span>

```xml
<rate-limit-by-key calls="10"
    renewal-period="60"
    counter-key="@(context.Request.Headers.GetValueOrDefault("Authorization","").AsJwt()?.Subject)" />
```

<span data-ttu-id="02ada-122">In dit voorbeeld we uitpakken van de autorisatie-header, converteert u deze naar `JWT` object en het onderwerp van het token gebruiken om te bepalen van de gebruiker en gebruiken als de frequentie waarmee de sleutel te beperken.</span><span class="sxs-lookup"><span data-stu-id="02ada-122">In this example we extract the Authorization header, convert it to `JWT` object and use the subject of the token to identify the user and use that as the rate limiting key.</span></span> <span data-ttu-id="02ada-123">Als de identiteit van de gebruiker is opgeslagen in de `JWT` als een van de andere claims vervolgens dat de waarde kan worden gebruikt in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="02ada-123">If the user identity is stored in the `JWT` as one of the other claims then that value could be used in its place.</span></span>

## <a name="combined-policies"></a><span data-ttu-id="02ada-124">Gecombineerde beleid</span><span class="sxs-lookup"><span data-stu-id="02ada-124">Combined policies</span></span>
<span data-ttu-id="02ada-125">Hoewel de nieuwe bandbreedteregeling beleidsregels meer controle dan de bestaande beleidsregels voor bandbreedteregeling bieden, is er nog steeds waarde combinatie van beide mogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="02ada-125">Although the new throttling policies provide more control than the existing throttling policies, there is still value combining both capabilities.</span></span> <span data-ttu-id="02ada-126">Beperkingen door abonnement productcode ([aanroepfrequentie per abonnement](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) en [gebruiksquotum per abonnement instellen](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota)) is een uitstekende manier om in te schakelen van een API monetizing in rekening gebracht op basis van gebruik niveaus op.</span><span class="sxs-lookup"><span data-stu-id="02ada-126">Throttling by product subscription key ([Limit call rate by subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota by subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota)) is a great way to enable monetizing of an API by charging based on usage levels.</span></span> <span data-ttu-id="02ada-127">De betere resultaten gedetailleerde besturingselement niet in staat om te beperken door de gebruiker is een aanvulling en gedrag van een gebruiker wordt voorkomen dat de ervaring van een andere beïnvloeden.</span><span class="sxs-lookup"><span data-stu-id="02ada-127">The finer grained control of being able to throttle by user is complementary and prevents one user's behavior from degrading the experience of another.</span></span> 

## <a name="client-driven-throttling"></a><span data-ttu-id="02ada-128">Client aangestuurd beperking</span><span class="sxs-lookup"><span data-stu-id="02ada-128">Client driven throttling</span></span>
<span data-ttu-id="02ada-129">Als de bandbreedteregeling sleutel is gedefinieerd met behulp van een [beleidsexpressie](https://msdn.microsoft.com/library/azure/dn910913.aspx), dan is de API-provider die is kiezen hoe de beperking ligt binnen het bereik.</span><span class="sxs-lookup"><span data-stu-id="02ada-129">When the throttling key is defined using a [policy expression](https://msdn.microsoft.com/library/azure/dn910913.aspx), then it is the API provider that is choosing how the throttling is scoped.</span></span> <span data-ttu-id="02ada-130">Echter, een ontwikkelaar mogelijk wilt bepalen hoe ze frequentielimiet hun eigen klanten.</span><span class="sxs-lookup"><span data-stu-id="02ada-130">However, a developer might want to control how they rate limit their own customers.</span></span> <span data-ttu-id="02ada-131">Dit kan worden ingeschakeld door de API-provider door de introductie van een aangepaste header om toe te staan van de ontwikkelaar de clienttoepassing communiceren de sleutel voor de API.</span><span class="sxs-lookup"><span data-stu-id="02ada-131">This could be enabled by the API provider by introducing a custom header to allow the developer's client application to communicate the key to the API.</span></span>

```xml
<rate-limit-by-key calls="100"
          renewal-period="60"
          counter-key="@(request.Headers.GetValueOrDefault("Rate-Key",""))"/>
```

<span data-ttu-id="02ada-132">Hierdoor kunnen de clienttoepassing van de ontwikkelaar te kiezen hoe ze willen maken van de sleutel van de snelheidsbeperking.</span><span class="sxs-lookup"><span data-stu-id="02ada-132">This enables the developer's client application to choose how they want to create the rate limiting key.</span></span> <span data-ttu-id="02ada-133">Met een beetje draaien kan een ontwikkelaar client hun eigen niveaus tarief maken door sets van sleutels toewijzen aan gebruikers en het sleutelgebruik draaien.</span><span class="sxs-lookup"><span data-stu-id="02ada-133">With a little bit of ingenuity a client developer could create their own rate tiers by allocating sets of keys to users and rotating the key usage.</span></span>

## <a name="summary"></a><span data-ttu-id="02ada-134">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="02ada-134">Summary</span></span>
<span data-ttu-id="02ada-135">Azure API Management biedt snelheid en aanhalingsteken beperking zowel wilt beveiligen en waarde toevoegen aan uw API-service.</span><span class="sxs-lookup"><span data-stu-id="02ada-135">Azure API Management provides rate and quote throttling to both protect and add value to your API service.</span></span> <span data-ttu-id="02ada-136">De nieuwe bandbreedteregeling beleidsregels met aangepaste bereik regels kunnen u betere resultaten gedetailleerde controle over deze beleidsregels waarmee uw klanten om nog betere toepassingen te bouwen.</span><span class="sxs-lookup"><span data-stu-id="02ada-136">The new throttling policies with custom scoping rules allow you finer grained control over those policies to enable your customers to build even better applications.</span></span> <span data-ttu-id="02ada-137">De voorbeelden in dit artikel worden het gebruik van dit nieuwe beleid door productie snelheidsbeperking-sleutels met client-IP-adressen, gebruikers-id en waarden van de client gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="02ada-137">The examples in this article demonstrate the use of these new policies by manufacturing rate limiting keys with client IP addresses, user identity, and client generated values.</span></span> <span data-ttu-id="02ada-138">Er zijn echter veel andere onderdelen van het bericht dat kan worden gebruikt zoals gebruikersagent, fragmenten voor URL-pad, de grootte van het bericht.</span><span class="sxs-lookup"><span data-stu-id="02ada-138">However, there are many other parts of the message that could be used such as user agent, URL path fragments, message size.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02ada-139">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="02ada-139">Next steps</span></span>
<span data-ttu-id="02ada-140">Geef ons uw feedback in de Disqus-thread voor dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="02ada-140">Please give us your feedback in the Disqus thread for this topic.</span></span> <span data-ttu-id="02ada-141">Het normaal zou zijn ideaal voor informatie over andere mogelijke sleutelwaarden die een logische keuze in uw scenario's zijn gekomen.</span><span class="sxs-lookup"><span data-stu-id="02ada-141">It would be great to hear about other potential key values that have been a logical choice in your scenarios.</span></span>

## <a name="watch-a-video-overview-of-these-policies"></a><span data-ttu-id="02ada-142">Bekijk een video-overzicht van deze beleidsregels</span><span class="sxs-lookup"><span data-stu-id="02ada-142">Watch a video overview of these policies</span></span>
<span data-ttu-id="02ada-143">Voor meer informatie over de [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) en [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) beleidsregels die in dit artikel, bekijk Neem de volgende video.</span><span class="sxs-lookup"><span data-stu-id="02ada-143">For more information on the [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies covered in this article, please watch the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Advanced-Request-Throttling-with-Azure-API-Management/player]
> 
> 

