---
title: Azure CDN met CORS aaaUsing | Microsoft Docs
description: Meer informatie over hoe toouse hello Azure Content Delivery Network (CDN) toowith Cross-Origin-Resource delen (CORS).
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
ms.openlocfilehash: 6c743b56c32a2d3aacc9a77094cb87d61b95d2f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-cdn-with-cors"></a><span data-ttu-id="21ee8-103">Azure CDN gebruiken met CORS</span><span class="sxs-lookup"><span data-stu-id="21ee8-103">Using Azure CDN with CORS</span></span>
## <a name="what-is-cors"></a><span data-ttu-id="21ee8-104">Wat is CORS?</span><span class="sxs-lookup"><span data-stu-id="21ee8-104">What is CORS?</span></span>
<span data-ttu-id="21ee8-105">CORS (Cross Origin Resource Sharing) is een HTTP-functie waarmee een webtoepassing die wordt uitgevoerd in een domein tooaccess resources in een ander domein.</span><span class="sxs-lookup"><span data-stu-id="21ee8-105">CORS (Cross Origin Resource Sharing) is an HTTP feature that enables a web application running under one domain tooaccess resources in another domain.</span></span> <span data-ttu-id="21ee8-106">Alle moderne webbrowsers implementeren volgorde tooreduce Hallo mogelijkheid van cross-site scripting aanvallen, een beveiligingsbeperkingen bekend als [dezelfde oorsprong beleid](http://www.w3.org/Security/wiki/Same_Origin_Policy).</span><span class="sxs-lookup"><span data-stu-id="21ee8-106">In order tooreduce hello possibility of cross-site scripting attacks, all modern web browsers implement a security restriction known as [same-origin policy](http://www.w3.org/Security/wiki/Same_Origin_Policy).</span></span>  <span data-ttu-id="21ee8-107">Dit voorkomt dat een webpagina van aanroepen API's in een ander domein.</span><span class="sxs-lookup"><span data-stu-id="21ee8-107">This prevents a web page from calling APIs in a different domain.</span></span>  <span data-ttu-id="21ee8-108">CORS biedt een veilige manier tooallow één oorsprong (Hallo brondomein) toocall API's in een andere bron.</span><span class="sxs-lookup"><span data-stu-id="21ee8-108">CORS provides a secure way tooallow one origin (hello origin domain) toocall APIs in another origin.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="21ee8-109">Hoe werkt het?</span><span class="sxs-lookup"><span data-stu-id="21ee8-109">How it works</span></span>
<span data-ttu-id="21ee8-110">Er zijn twee soorten CORS aanvragen, *eenvoudige aanvragen* en *complexe aanvragen.*</span><span class="sxs-lookup"><span data-stu-id="21ee8-110">There are two types of CORS requests, *simple requests* and *complex requests.*</span></span>

### <a name="for-simple-requests"></a><span data-ttu-id="21ee8-111">Voor eenvoudige aanvragen:</span><span class="sxs-lookup"><span data-stu-id="21ee8-111">For simple requests:</span></span>

1. <span data-ttu-id="21ee8-112">Hallo browser verzendt Hallo CORS-aanvraag met een extra **oorsprong** header HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="21ee8-112">hello browser sends hello CORS request with an additional **Origin** HTTP request header.</span></span> <span data-ttu-id="21ee8-113">Hallo-waarde van deze header is Hallo oorsprong die behandeld Hallo bovenliggende pagina die wordt gedefinieerd als Hallo combinatie van *protocol* *domein,* en *poort.*</span><span class="sxs-lookup"><span data-stu-id="21ee8-113">hello value of this header is hello origin that served hello parent page, which is defined as hello combination of *protocol,* *domain,* and *port.*</span></span>  <span data-ttu-id="21ee8-114">Wanneer een pagina uit https://www.contoso.com tooaccess gebruikersgegevens in Hallo fabrikam.com oorsprong probeert, zou Hallo aanvraagheader na toofabrikam.com worden verzonden:</span><span class="sxs-lookup"><span data-stu-id="21ee8-114">When a page from https://www.contoso.com attempts tooaccess a user's data in hello fabrikam.com origin, hello following request header would be sent toofabrikam.com:</span></span>

   `Origin: https://www.contoso.com`

2. <span data-ttu-id="21ee8-115">Hallo-server reageert met een van de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="21ee8-115">hello server may respond with any of hello following:</span></span>

   * <span data-ttu-id="21ee8-116">Een **Access Control-toestaan-oorsprong** header in zijn reactie waarmee wordt aangegeven welke bronsite is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="21ee8-116">An **Access-Control-Allow-Origin** header in its response indicating which origin site is allowed.</span></span> <span data-ttu-id="21ee8-117">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="21ee8-117">For example:</span></span>

     `Access-Control-Allow-Origin: https://www.contoso.com`

   * <span data-ttu-id="21ee8-118">Een HTTP-fout 403 code als Hallo server staat niet toe dat Hallo cross-origin-aanvraag na Hallo oorsprong header controleren</span><span class="sxs-lookup"><span data-stu-id="21ee8-118">An HTTP error code such as 403 if hello server does not allow hello cross-origin request after checking hello Origin header</span></span>

   * <span data-ttu-id="21ee8-119">Een **Access Control-toestaan-oorsprong** koptekst met een jokerteken waarmee alle oorsprongen:</span><span class="sxs-lookup"><span data-stu-id="21ee8-119">An **Access-Control-Allow-Origin** header with a wildcard that allows all origins:</span></span>

     `Access-Control-Allow-Origin: *`

### <a name="for-complex-requests"></a><span data-ttu-id="21ee8-120">Voor complexe aanvragen:</span><span class="sxs-lookup"><span data-stu-id="21ee8-120">For complex requests:</span></span>

<span data-ttu-id="21ee8-121">Een complexe aanvraag is een aanvraag CORS waarbij Hallo browser vereist toosend een *voorbereidende aanvraag* (dat wil zeggen een voorlopige test) voordat Hallo werkelijke CORS-aanvraag wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="21ee8-121">A complex request is a CORS request where hello browser is required toosend a *preflight request* (i.e. a preliminary probe) before sending hello actual CORS request.</span></span> <span data-ttu-id="21ee8-122">Hallo voorbereidende aanvraag Hallo-server om toestemming wordt gevraagd als Hallo oorspronkelijke CORS-aanvraag kan worden voortgezet en wordt een `OPTIONS` toohello aanvragen dezelfde URL.</span><span class="sxs-lookup"><span data-stu-id="21ee8-122">hello preflight request asks hello server permission if hello original CORS request can proceed and is an `OPTIONS` request toohello same URL.</span></span>

> [!TIP]
> <span data-ttu-id="21ee8-123">Voor meer informatie over de CORS-stromen en verrassingen, bekijkt hello [tooCORS handleiding voor de REST-API's](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).</span><span class="sxs-lookup"><span data-stu-id="21ee8-123">For more details on CORS flows and common pitfalls, view hello [Guide tooCORS for REST APIs](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).</span></span>
>
>

## <a name="wildcard-or-single-origin-scenarios"></a><span data-ttu-id="21ee8-124">Jokertekens of één oorsprong scenario 's</span><span class="sxs-lookup"><span data-stu-id="21ee8-124">Wildcard or single origin scenarios</span></span>
<span data-ttu-id="21ee8-125">CORS op Azure CDN werkt automatisch zonder aanvullende configuratie wanneer hello **Access Control-toestaan-oorsprong** header toowildcard (*) of een enkel oorsprong is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="21ee8-125">CORS on Azure CDN will work automatically with no additional configuration when hello **Access-Control-Allow-Origin** header is set toowildcard (*) or a single origin.</span></span>  <span data-ttu-id="21ee8-126">Hallo CDN cache worden opgeslagen door de eerste antwoord Hallo en het gebruik van de volgende aanvragen Hallo dezelfde kop.</span><span class="sxs-lookup"><span data-stu-id="21ee8-126">hello CDN will cache hello first response and subsequent requests will use hello same header.</span></span>

<span data-ttu-id="21ee8-127">Als aanvragen al toohello CDN eerdere tooCORS wordt ingesteld op Hallo van uw oorsprong aangebracht zijn, moet u toopurge inhoud op uw eindpunt inhoud tooreload Hallo inhoud Hello **Access Control-toestaan-oorsprong** header.</span><span class="sxs-lookup"><span data-stu-id="21ee8-127">If requests have already been made toohello CDN prior tooCORS being set on hello your origin, you will need toopurge content on your endpoint content tooreload hello content with hello **Access-Control-Allow-Origin** header.</span></span>

## <a name="multiple-origin-scenarios"></a><span data-ttu-id="21ee8-128">Scenario's met meerdere oorsprong</span><span class="sxs-lookup"><span data-stu-id="21ee8-128">Multiple origin scenarios</span></span>
<span data-ttu-id="21ee8-129">Als u een specifieke lijst met oorsprongen toobe toegestaan voor CORS tooallow moet, ophalen dingen iets gecompliceerder.</span><span class="sxs-lookup"><span data-stu-id="21ee8-129">If you need tooallow a specific list of origins toobe allowed for CORS, things get a little more complicated.</span></span> <span data-ttu-id="21ee8-130">Hallo probleem treedt op wanneer Hallo CDN in de cache Hallo opgeslagen **Access Control-toestaan-oorsprong** -header voor de eerste CORS-oorsprong Hallo.</span><span class="sxs-lookup"><span data-stu-id="21ee8-130">hello problem occurs when hello CDN caches hello **Access-Control-Allow-Origin** header for hello first CORS origin.</span></span>  <span data-ttu-id="21ee8-131">Wanneer een andere CORS-oorsprong een volgende aanvraag indient, Hallo CDN Hallo in de cache opgeslagen fungeert **Access Control-toestaan-oorsprong** koptekst, die niet overeen met.</span><span class="sxs-lookup"><span data-stu-id="21ee8-131">When a different CORS origin makes a subsequent request, hello CDN will serve hello cached **Access-Control-Allow-Origin** header, which won't match.</span></span>  <span data-ttu-id="21ee8-132">Er zijn verschillende manieren toocorrect dit.</span><span class="sxs-lookup"><span data-stu-id="21ee8-132">There are several ways toocorrect this.</span></span>

### <a name="azure-cdn-premium-from-verizon"></a><span data-ttu-id="21ee8-133">Azure CDN Premium van Verizon</span><span class="sxs-lookup"><span data-stu-id="21ee8-133">Azure CDN Premium from Verizon</span></span>
<span data-ttu-id="21ee8-134">Hallo van de beste manier tooenable dit toouse is **Azure CDN Premium van Verizon**, die beschrijft sommige geavanceerde functies.</span><span class="sxs-lookup"><span data-stu-id="21ee8-134">hello best way tooenable this is toouse **Azure CDN Premium from Verizon**, which exposes some advanced functionality.</span></span> 

<span data-ttu-id="21ee8-135">Je hebt te[maakt u een regel](cdn-rules-engine.md) toocheck hello **oorsprong** header op Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="21ee8-135">You'll need too[create a rule](cdn-rules-engine.md) toocheck hello **Origin** header on hello request.</span></span>  <span data-ttu-id="21ee8-136">Als het een geldige oorsprong, Hallo wordt ingesteld door de regel **Access Control-toestaan-oorsprong** header met Hallo oorsprong in het Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="21ee8-136">If it's a valid origin, your rule will set hello **Access-Control-Allow-Origin** header with hello origin provided in hello request.</span></span>  <span data-ttu-id="21ee8-137">Als Hallo oorsprong in Hallo opgegeven **oorsprong** header is niet toegestaan, de regel moet Hallo weglaten **Access Control-toestaan-oorsprong** header waardoor Hallo browser tooreject Hallo aanvraag.</span><span class="sxs-lookup"><span data-stu-id="21ee8-137">If hello origin specified in hello **Origin** header is not allowed, your rule should omit hello **Access-Control-Allow-Origin** header which will cause hello browser tooreject hello request.</span></span> 

<span data-ttu-id="21ee8-138">Er zijn twee manieren toodo dit met de Hallo regelengine.</span><span class="sxs-lookup"><span data-stu-id="21ee8-138">There are two ways toodo this with hello rules engine.</span></span>  <span data-ttu-id="21ee8-139">In beide gevallen Hallo **Access Control-toestaan-oorsprong** koptekst van de bronserver Hallo-bestand volledig wordt genegeerd, Hallo CDN van regelengine beheert volledig Hallo CORS oorsprongen toegestaan.</span><span class="sxs-lookup"><span data-stu-id="21ee8-139">In both cases, hello **Access-Control-Allow-Origin** header from hello file's origin server is completely ignored, hello CDN's rules engine completely manages hello allowed CORS origins.</span></span>

#### <a name="one-regular-expression-with-all-valid-origins"></a><span data-ttu-id="21ee8-140">Een reguliere expressie met alle geldige oorsprongen</span><span class="sxs-lookup"><span data-stu-id="21ee8-140">One regular expression with all valid origins</span></span>
<span data-ttu-id="21ee8-141">In dit geval maakt u een reguliere expressie waarin alle oorsprongen Hallo gewenste tooallow:</span><span class="sxs-lookup"><span data-stu-id="21ee8-141">In this case, you'll create a regular expression that includes all of hello origins you want tooallow:</span></span> 

    https?:\/\/(www\.contoso\.com|contoso\.com|www\.microsoft\.com|microsoft.com\.com)$

> [!TIP]
> <span data-ttu-id="21ee8-142">**Azure CDN van Verizon** gebruikt [Perl compatibel reguliere expressies](http://pcre.org/) als de engine voor reguliere expressies.</span><span class="sxs-lookup"><span data-stu-id="21ee8-142">**Azure CDN from Verizon** uses [Perl Compatible Regular Expressions](http://pcre.org/) as its engine for regular expressions.</span></span>  <span data-ttu-id="21ee8-143">U kunt een hulpprogramma zoals [reguliere expressies 101](https://regex101.com/) toovalidate uw reguliere expressie.</span><span class="sxs-lookup"><span data-stu-id="21ee8-143">You can use a tool like [Regular Expressions 101](https://regex101.com/) toovalidate your regular expression.</span></span>  <span data-ttu-id="21ee8-144">Let op: Hallo ' / ' teken is geldig in reguliere expressies en hoeft niet toobe escape-teken, echter escape-teken wordt beschouwd als een best practice en wordt verwacht door sommige validatiefuncties regex.</span><span class="sxs-lookup"><span data-stu-id="21ee8-144">Note that hello "/" character is valid in regular expressions and doesn't need toobe escaped, however, escaping that character is considered a best practice and is expected by some regex validators.</span></span>
> 
> 

<span data-ttu-id="21ee8-145">Indien de reguliere expressie Hallo overeenkomt, de regel Hallo vervangt **Access Control-toestaan-oorsprong** header (indien aanwezig) van de oorsprong van Hallo met Hallo oorsprong die Hallo-aanvraag heeft verzonden.</span><span class="sxs-lookup"><span data-stu-id="21ee8-145">If hello regular expression matches, your rule will replace hello **Access-Control-Allow-Origin** header (if any) from hello origin with hello origin that sent hello request.</span></span>  <span data-ttu-id="21ee8-146">U kunt ook aanvullende CORS-kopteksten, zoals toevoegen **-besturingselement-toestaan-toegangsmethoden**.</span><span class="sxs-lookup"><span data-stu-id="21ee8-146">You can also add additional CORS headers, such as **Access-Control-Allow-Methods**.</span></span>

![Voorbeeld van de regels met de reguliere expressie](./media/cdn-cors/cdn-cors-regex.png)

#### <a name="request-header-rule-for-each-origin"></a><span data-ttu-id="21ee8-148">Aanvraag-header-regel voor elke oorsprong.</span><span class="sxs-lookup"><span data-stu-id="21ee8-148">Request header rule for each origin.</span></span>
<span data-ttu-id="21ee8-149">In plaats van reguliere expressies, kunt u in plaats daarvan een afzonderlijke maken regel voor oorsprong van elke gewenste tooallow met Hallo **aanvraag-Header jokertekens** [overeenkomen met de voorwaarde](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1).</span><span class="sxs-lookup"><span data-stu-id="21ee8-149">Rather than regular expressions, you can instead create a separate rule for each origin you wish tooallow using hello **Request Header Wildcard** [match condition](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1).</span></span> <span data-ttu-id="21ee8-150">Als engine Hallo regels met Hallo reguliere expressie methode alleen sets Hallo CORS headers.</span><span class="sxs-lookup"><span data-stu-id="21ee8-150">As with hello regular expression method, hello rules engine alone sets hello CORS headers.</span></span> 

![Voorbeeld van de regels zonder reguliere expressie](./media/cdn-cors/cdn-cors-no-regex.png)

> [!TIP]
> <span data-ttu-id="21ee8-152">Hallo Hallo bovenstaande voorbeeld gebruik van Hallo jokerteken * vertelt Hallo regels engine toomatch HTTP en HTTPS.</span><span class="sxs-lookup"><span data-stu-id="21ee8-152">In hello example above, hello use of hello wildcard character * tells hello rules engine toomatch both HTTP and HTTPS.</span></span>
> 
> 

### <a name="azure-cdn-standard"></a><span data-ttu-id="21ee8-153">Azure CDN Standard</span><span class="sxs-lookup"><span data-stu-id="21ee8-153">Azure CDN Standard</span></span>
<span data-ttu-id="21ee8-154">Hallo op Azure CDN Standard profielen alleen tooallow mechanisme voor meerdere oorsprongen zonder het gebruik van Hallo jokertekens oorsprong Hallo toouse is [query opslaan in cache](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="21ee8-154">On Azure CDN Standard profiles, hello only mechanism tooallow for multiple origins without hello use of hello wildcard origin is toouse [query string caching](cdn-query-string.md).</span></span>  <span data-ttu-id="21ee8-155">U moet tooenable query-tekenreeks instelling voor Hallo CDN-eindpunt en een unieke queryreeks vervolgens gebruiken voor aanvragen van elk domein.</span><span class="sxs-lookup"><span data-stu-id="21ee8-155">You need tooenable query string setting for hello CDN endpoint and then use a unique query string for requests from each allowed domain.</span></span> <span data-ttu-id="21ee8-156">Dit leidt tot Hallo CDN in cache plaatsen van een afzonderlijk object voor elke unieke queryreeks.</span><span class="sxs-lookup"><span data-stu-id="21ee8-156">Doing this will result in hello CDN caching a separate object for each unique query string.</span></span> <span data-ttu-id="21ee8-157">Deze aanpak is niet ideaal, echter als het zal leiden tot meerdere exemplaren van Hallo hetzelfde bestand in cache op Hallo CDN.</span><span class="sxs-lookup"><span data-stu-id="21ee8-157">This approach is not ideal, however, as it will result in multiple copies of hello same file cached on hello CDN.</span></span>  

