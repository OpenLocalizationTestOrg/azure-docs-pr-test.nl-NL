---
title: Azure CDN gebruiken met CORS | Microsoft Docs
description: Informatie over het gebruik van het Azure Content Delivery Network (CDN) aan met Cross-Origin-Resource delen (CORS).
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 86740a96-4269-4060-aba3-a69f00e6f14e
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 7070397f6e69b21add75bad8220f0b8ebe36d266
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-cdn-with-cors"></a><span data-ttu-id="64148-103">Azure CDN gebruiken met CORS</span><span class="sxs-lookup"><span data-stu-id="64148-103">Using Azure CDN with CORS</span></span>
## <a name="what-is-cors"></a><span data-ttu-id="64148-104">Wat is CORS?</span><span class="sxs-lookup"><span data-stu-id="64148-104">What is CORS?</span></span>
<span data-ttu-id="64148-105">CORS (Cross Origin Resource Sharing) is een HTTP-functie waarmee een webtoepassing in een domein met toegang tot bronnen in een ander domein.</span><span class="sxs-lookup"><span data-stu-id="64148-105">CORS (Cross Origin Resource Sharing) is an HTTP feature that enables a web application running under one domain to access resources in another domain.</span></span> <span data-ttu-id="64148-106">Om het risico te verkleinen van aanvallen via cross-site scripting, alle moderne webbrowsers implementeren een beveiligingsbeperkingen bekend als [dezelfde oorsprong beleid](http://www.w3.org/Security/wiki/Same_Origin_Policy).</span><span class="sxs-lookup"><span data-stu-id="64148-106">In order to reduce the possibility of cross-site scripting attacks, all modern web browsers implement a security restriction known as [same-origin policy](http://www.w3.org/Security/wiki/Same_Origin_Policy).</span></span>  <span data-ttu-id="64148-107">Dit voorkomt dat een webpagina van aanroepen API's in een ander domein.</span><span class="sxs-lookup"><span data-stu-id="64148-107">This prevents a web page from calling APIs in a different domain.</span></span>  <span data-ttu-id="64148-108">CORS biedt een veilige manier om toe te staan van één bron (het domein van de oorsprong) API's in een andere bron aanroepen.</span><span class="sxs-lookup"><span data-stu-id="64148-108">CORS provides a secure way to allow one origin (the origin domain) to call APIs in another origin.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="64148-109">Hoe werkt het?</span><span class="sxs-lookup"><span data-stu-id="64148-109">How it works</span></span>
<span data-ttu-id="64148-110">Er zijn twee soorten CORS aanvragen, *eenvoudige aanvragen* en *complexe aanvragen.*</span><span class="sxs-lookup"><span data-stu-id="64148-110">There are two types of CORS requests, *simple requests* and *complex requests.*</span></span>

### <a name="for-simple-requests"></a><span data-ttu-id="64148-111">Voor eenvoudige aanvragen:</span><span class="sxs-lookup"><span data-stu-id="64148-111">For simple requests:</span></span>

1. <span data-ttu-id="64148-112">De browser verzendt de CORS-aanvraag met een extra **oorsprong** header HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="64148-112">The browser sends the CORS request with an additional **Origin** HTTP request header.</span></span> <span data-ttu-id="64148-113">De waarde van deze header is de oorsprong die de bovenliggende pagina, die is gedefinieerd als de combinatie van behandeld *protocol* *domein,* en *poort.*</span><span class="sxs-lookup"><span data-stu-id="64148-113">The value of this header is the origin that served the parent page, which is defined as the combination of *protocol,* *domain,* and *port.*</span></span>  <span data-ttu-id="64148-114">Wanneer een pagina uit https://www.contoso.com probeert te krijgen tot de gegevens van een gebruiker in de oorsprong fabrikam.com, zou u de volgende aanvraagheader verzonden naar fabrikam.com:</span><span class="sxs-lookup"><span data-stu-id="64148-114">When a page from https://www.contoso.com attempts to access a user's data in the fabrikam.com origin, the following request header would be sent to fabrikam.com:</span></span>

   `Origin: https://www.contoso.com`

2. <span data-ttu-id="64148-115">De server reageert met het volgende:</span><span class="sxs-lookup"><span data-stu-id="64148-115">The server may respond with any of the following:</span></span>

   * <span data-ttu-id="64148-116">Een **Access Control-toestaan-oorsprong** header in zijn reactie waarmee wordt aangegeven welke bronsite is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="64148-116">An **Access-Control-Allow-Origin** header in its response indicating which origin site is allowed.</span></span> <span data-ttu-id="64148-117">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="64148-117">For example:</span></span>

     `Access-Control-Allow-Origin: https://www.contoso.com`

   * <span data-ttu-id="64148-118">Een HTTP-foutcode zoals 403 als de server niet toe de cross-origin-aanvraag dat staat na het controleren van de header van oorsprong</span><span class="sxs-lookup"><span data-stu-id="64148-118">An HTTP error code such as 403 if the server does not allow the cross-origin request after checking the Origin header</span></span>

   * <span data-ttu-id="64148-119">Een **Access Control-toestaan-oorsprong** koptekst met een jokerteken waarmee alle oorsprongen:</span><span class="sxs-lookup"><span data-stu-id="64148-119">An **Access-Control-Allow-Origin** header with a wildcard that allows all origins:</span></span>

     `Access-Control-Allow-Origin: *`

### <a name="for-complex-requests"></a><span data-ttu-id="64148-120">Voor complexe aanvragen:</span><span class="sxs-lookup"><span data-stu-id="64148-120">For complex requests:</span></span>

<span data-ttu-id="64148-121">Een complexe aanvraag is een aanvraag CORS waarvoor de browser is vereist voor het verzenden van een *voorbereidende aanvraag* (dat wil zeggen een voorlopige test) voordat u de werkelijke CORS-aanvraag verzendt.</span><span class="sxs-lookup"><span data-stu-id="64148-121">A complex request is a CORS request where the browser is required to send a *preflight request* (i.e. a preliminary probe) before sending the actual CORS request.</span></span> <span data-ttu-id="64148-122">De voorbereidende aanvraag toestemming wordt gevraagd de server als de oorspronkelijke CORS aanvragen kan worden voortgezet en wordt een `OPTIONS` aanvraag naar dezelfde URL.</span><span class="sxs-lookup"><span data-stu-id="64148-122">The preflight request asks the server permission if the original CORS request can proceed and is an `OPTIONS` request to the same URL.</span></span>

> [!TIP]
> <span data-ttu-id="64148-123">Voor meer informatie over de CORS-stromen en verrassingen, bekijkt u de [handleiding voor het CORS voor REST-API's](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).</span><span class="sxs-lookup"><span data-stu-id="64148-123">For more details on CORS flows and common pitfalls, view the [Guide to CORS for REST APIs](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).</span></span>
>
>

## <a name="wildcard-or-single-origin-scenarios"></a><span data-ttu-id="64148-124">Jokertekens of één oorsprong scenario 's</span><span class="sxs-lookup"><span data-stu-id="64148-124">Wildcard or single origin scenarios</span></span>
<span data-ttu-id="64148-125">CORS op Azure CDN werkt automatisch zonder aanvullende configuratie als de **Access Control-toestaan-oorsprong** header is ingesteld op het jokerteken (*) of een enkel oorsprong.</span><span class="sxs-lookup"><span data-stu-id="64148-125">CORS on Azure CDN will work automatically with no additional configuration when the **Access-Control-Allow-Origin** header is set to wildcard (*) or a single origin.</span></span>  <span data-ttu-id="64148-126">De CDN cache worden opgeslagen door de eerste reactie en volgende aanvragen gebruik van dezelfde kop.</span><span class="sxs-lookup"><span data-stu-id="64148-126">The CDN will cache the first response and subsequent requests will use the same header.</span></span>

<span data-ttu-id="64148-127">Als aanvragen al naar de CDN voordat CORS wordt ingesteld aangebracht zijn op de uw oorsprong, moet u opschonen van de inhoud van de inhoud van uw eindpunt opnieuw laden van de inhoud met de **Access Control-toestaan-oorsprong** header.</span><span class="sxs-lookup"><span data-stu-id="64148-127">If requests have already been made to the CDN prior to CORS being set on the your origin, you will need to purge content on your endpoint content to reload the content with the **Access-Control-Allow-Origin** header.</span></span>

## <a name="multiple-origin-scenarios"></a><span data-ttu-id="64148-128">Scenario's met meerdere oorsprong</span><span class="sxs-lookup"><span data-stu-id="64148-128">Multiple origin scenarios</span></span>
<span data-ttu-id="64148-129">Als u toestaan dat een specifieke lijst met oorsprongen wilt moet worden toegestaan voor CORS, krijgen die dingen iets gecompliceerder.</span><span class="sxs-lookup"><span data-stu-id="64148-129">If you need to allow a specific list of origins to be allowed for CORS, things get a little more complicated.</span></span> <span data-ttu-id="64148-130">Het probleem treedt op wanneer de CDN plaatst de **Access Control-toestaan-oorsprong** -header voor de eerste CORS-oorsprong.</span><span class="sxs-lookup"><span data-stu-id="64148-130">The problem occurs when the CDN caches the **Access-Control-Allow-Origin** header for the first CORS origin.</span></span>  <span data-ttu-id="64148-131">Wanneer een andere CORS-oorsprong een volgende aanvraag indient, de CDN fungeert de in de cache **Access Control-toestaan-oorsprong** koptekst, die niet overeen met.</span><span class="sxs-lookup"><span data-stu-id="64148-131">When a different CORS origin makes a subsequent request, the CDN will serve the cached **Access-Control-Allow-Origin** header, which won't match.</span></span>  <span data-ttu-id="64148-132">Er zijn verschillende manieren om dit te corrigeren.</span><span class="sxs-lookup"><span data-stu-id="64148-132">There are several ways to correct this.</span></span>

### <a name="azure-cdn-premium-from-verizon"></a><span data-ttu-id="64148-133">Azure CDN Premium van Verizon</span><span class="sxs-lookup"><span data-stu-id="64148-133">Azure CDN Premium from Verizon</span></span>
<span data-ttu-id="64148-134">De beste manier om dit te gebruiken is **Azure CDN Premium van Verizon**, die beschrijft sommige geavanceerde functies.</span><span class="sxs-lookup"><span data-stu-id="64148-134">The best way to enable this is to use **Azure CDN Premium from Verizon**, which exposes some advanced functionality.</span></span> 

<span data-ttu-id="64148-135">U moet [maakt u een regel](cdn-rules-engine.md) om te controleren de **oorsprong** header voor de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="64148-135">You'll need to [create a rule](cdn-rules-engine.md) to check the **Origin** header on the request.</span></span>  <span data-ttu-id="64148-136">Als het een geldige oorsprong, de regel stelt de **Access Control-toestaan-oorsprong** header met de opgegeven in de aanvraag van de oorsprong.</span><span class="sxs-lookup"><span data-stu-id="64148-136">If it's a valid origin, your rule will set the **Access-Control-Allow-Origin** header with the origin provided in the request.</span></span>  <span data-ttu-id="64148-137">Als de oorsprong is opgegeven in de **oorsprong** header is niet toegestaan, de regel moet weglaten de **Access Control-toestaan-oorsprong** header waardoor de browser om de aanvraag af te wijzen.</span><span class="sxs-lookup"><span data-stu-id="64148-137">If the origin specified in the **Origin** header is not allowed, your rule should omit the **Access-Control-Allow-Origin** header which will cause the browser to reject the request.</span></span> 

<span data-ttu-id="64148-138">Er zijn twee manieren om dit te doen met de regelengine.</span><span class="sxs-lookup"><span data-stu-id="64148-138">There are two ways to do this with the rules engine.</span></span>  <span data-ttu-id="64148-139">In beide gevallen moet de **Access Control-toestaan-oorsprong** koptekst van de oorsprong van de bestandsserver volledig wordt genegeerd, de toegestane oorsprongen van CORS volledig worden beheerd door het CDN regelengine.</span><span class="sxs-lookup"><span data-stu-id="64148-139">In both cases, the **Access-Control-Allow-Origin** header from the file's origin server is completely ignored, the CDN's rules engine completely manages the allowed CORS origins.</span></span>

#### <a name="one-regular-expression-with-all-valid-origins"></a><span data-ttu-id="64148-140">Een reguliere expressie met alle geldige oorsprongen</span><span class="sxs-lookup"><span data-stu-id="64148-140">One regular expression with all valid origins</span></span>
<span data-ttu-id="64148-141">In dit geval maakt u een reguliere expressie waarin alle van de oorsprongen die u wilt toestaan:</span><span class="sxs-lookup"><span data-stu-id="64148-141">In this case, you'll create a regular expression that includes all of the origins you want to allow:</span></span> 

    https?:\/\/(www\.contoso\.com|contoso\.com|www\.microsoft\.com|microsoft.com\.com)$

> [!TIP]
> <span data-ttu-id="64148-142">**Azure CDN van Verizon** gebruikt [Perl compatibel reguliere expressies](http://pcre.org/) als de engine voor reguliere expressies.</span><span class="sxs-lookup"><span data-stu-id="64148-142">**Azure CDN from Verizon** uses [Perl Compatible Regular Expressions](http://pcre.org/) as its engine for regular expressions.</span></span>  <span data-ttu-id="64148-143">U kunt een hulpprogramma zoals [reguliere expressies 101](https://regex101.com/) valideren van de reguliere expressie.</span><span class="sxs-lookup"><span data-stu-id="64148-143">You can use a tool like [Regular Expressions 101](https://regex101.com/) to validate your regular expression.</span></span>  <span data-ttu-id="64148-144">Houd er rekening mee dat het teken '/' is ongeldig in reguliere expressies en niet moet worden voorafgegaan, echter escape-teken wordt beschouwd als een best practice en wordt verwacht door sommige validatiefuncties regex.</span><span class="sxs-lookup"><span data-stu-id="64148-144">Note that the "/" character is valid in regular expressions and doesn't need to be escaped, however, escaping that character is considered a best practice and is expected by some regex validators.</span></span>
> 
> 

<span data-ttu-id="64148-145">Als de reguliere expressie overeenkomt, de regel wordt vervangen door de **Access Control-toestaan-oorsprong** header (indien aanwezig) vanuit de oorsprong met de oorsprong die de aanvraag heeft verzonden.</span><span class="sxs-lookup"><span data-stu-id="64148-145">If the regular expression matches, your rule will replace the **Access-Control-Allow-Origin** header (if any) from the origin with the origin that sent the request.</span></span>  <span data-ttu-id="64148-146">U kunt ook aanvullende CORS-kopteksten, zoals toevoegen **-besturingselement-toestaan-toegangsmethoden**.</span><span class="sxs-lookup"><span data-stu-id="64148-146">You can also add additional CORS headers, such as **Access-Control-Allow-Methods**.</span></span>

![Voorbeeld van de regels met de reguliere expressie](./media/cdn-cors/cdn-cors-regex.png)

#### <a name="request-header-rule-for-each-origin"></a><span data-ttu-id="64148-148">Aanvraag-header-regel voor elke oorsprong.</span><span class="sxs-lookup"><span data-stu-id="64148-148">Request header rule for each origin.</span></span>
<span data-ttu-id="64148-149">In plaats van reguliere expressies, kunt u een afzonderlijke regel voor elke bron die u wilt toestaan met behulp van in plaats daarvan maakt de **aanvraag-Header jokertekens** [overeenkomen met de voorwaarde](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1).</span><span class="sxs-lookup"><span data-stu-id="64148-149">Rather than regular expressions, you can instead create a separate rule for each origin you wish to allow using the **Request Header Wildcard** [match condition](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1).</span></span> <span data-ttu-id="64148-150">Net als bij de methode reguliere expressie, stelt de motor regels de CORS-headers.</span><span class="sxs-lookup"><span data-stu-id="64148-150">As with the regular expression method, the rules engine alone sets the CORS headers.</span></span> 

![Voorbeeld van de regels zonder reguliere expressie](./media/cdn-cors/cdn-cors-no-regex.png)

> [!TIP]
> <span data-ttu-id="64148-152">In het bovenstaande voorbeeld wordt het gebruik van het jokerteken * vertelt regelengine voor de overeenkomen met zowel HTTP als HTTPS.</span><span class="sxs-lookup"><span data-stu-id="64148-152">In the example above, the use of the wildcard character * tells the rules engine to match both HTTP and HTTPS.</span></span>
> 
> 

### <a name="azure-cdn-standard"></a><span data-ttu-id="64148-153">Azure CDN Standard</span><span class="sxs-lookup"><span data-stu-id="64148-153">Azure CDN Standard</span></span>
<span data-ttu-id="64148-154">Op Azure CDN Standard profielen, is het enige mechanisme om toe te staan voor meerdere oorsprongen zonder het gebruik van de oorsprong jokerteken is het gebruik van [query opslaan in cache](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="64148-154">On Azure CDN Standard profiles, the only mechanism to allow for multiple origins without the use of the wildcard origin is to use [query string caching](cdn-query-string.md).</span></span>  <span data-ttu-id="64148-155">U moet query tekenreeks instelling inschakelen voor het CDN-eindpunt en een unieke queryreeks vervolgens gebruiken voor aanvragen van elk domein.</span><span class="sxs-lookup"><span data-stu-id="64148-155">You need to enable query string setting for the CDN endpoint and then use a unique query string for requests from each allowed domain.</span></span> <span data-ttu-id="64148-156">Dit resulteert in de cache van een afzonderlijk object voor elke unieke queryreeks CDN.</span><span class="sxs-lookup"><span data-stu-id="64148-156">Doing this will result in the CDN caching a separate object for each unique query string.</span></span> <span data-ttu-id="64148-157">Deze aanpak is echter niet ideaal, zoals het tot meerdere exemplaren van hetzelfde bestand in cache op de CDN leiden zal.</span><span class="sxs-lookup"><span data-stu-id="64148-157">This approach is not ideal, however, as it will result in multiple copies of the same file cached on the CDN.</span></span>  

