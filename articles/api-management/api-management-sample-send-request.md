---
title: aaaUsing API Management-service toogenerate HTTP-aanvragen
description: Meer informatie over de aanvraag en -antwoord beleid toouse van API Management toocall externe services van uw API
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: 4539c0fa-21ef-4b1c-a1d4-d89a38c242fa
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 8002ee453057513340328d99f298703c3b3a9531
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-external-services-from-hello-azure-api-management-service"></a><span data-ttu-id="78947-103">Met behulp van externe services van hello Azure API Management-service</span><span class="sxs-lookup"><span data-stu-id="78947-103">Using external services from hello Azure API Management service</span></span>
<span data-ttu-id="78947-104">Hallo-beleid beschikbaar is in Azure API Management-service kan een breed scala aan goed functioneren op basis van uitsluitend op Hallo inkomende aanvraag, het uitgaande antwoord Hallo en basisinformatie over de configuratie kunnen doen.</span><span class="sxs-lookup"><span data-stu-id="78947-104">hello policies available in Azure API Management service can do a wide range of useful work based purely on hello incoming request, hello outgoing response and basic configuration information.</span></span> <span data-ttu-id="78947-105">Echter, kunnen toointeract met externe services van API Management wordt beleid wordt geopend veel meer mogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="78947-105">However, being able toointeract with external services from API Management policies opens up many more opportunities.</span></span>

<span data-ttu-id="78947-106">We eerder hebben gezien hoe we kunnen werken met Hallo [Azure Event Hub-service voor logboekregistratie, bewaken en analytics](api-management-log-to-eventhub-sample.md).</span><span class="sxs-lookup"><span data-stu-id="78947-106">We have previously seen how we can interact with hello [Azure Event Hub service for logging, monitoring and analytics](api-management-log-to-eventhub-sample.md).</span></span> <span data-ttu-id="78947-107">In dit artikel wordt gedemonstreerd service op basis van beleid waarmee u toointeract met een externe HTTP.</span><span class="sxs-lookup"><span data-stu-id="78947-107">In this article we will demonstrate policies that allow you toointeract with any external HTTP based service.</span></span> <span data-ttu-id="78947-108">Dit beleid kunnen worden gebruikt voor activering van externe gebeurtenissen of voor het ophalen van informatie die wordt gebruikt toomanipulate Hallo oorspronkelijke aanvraag en -antwoord op een bepaalde manier zijn.</span><span class="sxs-lookup"><span data-stu-id="78947-108">These policies can be used for triggering remote events or for retrieving information that will be used toomanipulate hello original request and response in some way.</span></span>

## <a name="send-one-way-request"></a><span data-ttu-id="78947-109">Een-manier-verzoek om te verzenden</span><span class="sxs-lookup"><span data-stu-id="78947-109">Send-One-Way-Request</span></span>
<span data-ttu-id="78947-110">Mogelijk hello eenvoudigste externe interactie is Hallo fire en vergeet stijl van de aanvraag waarmee een externe service toobe de hoogte gesteld van een soort belangrijke gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="78947-110">Possibly hello simplest external interaction is hello fire-and-forget style of request that allows an external service toobe notified of some kind of important event.</span></span> <span data-ttu-id="78947-111">We kunnen beleid voor toegangsbeheer stroom hello gebruiken `choose` toodetect elk soort voorwaarde bent geïnteresseerd en klikt u vervolgens aan als hello voorwaarde wordt voldaan, maken we een externe HTTP-aanvraag met Hallo [-één-manier-verzoek om te verzenden](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) beleid.</span><span class="sxs-lookup"><span data-stu-id="78947-111">We can use hello control flow policy `choose` toodetect any kind of condition that we are interested in and then, if hello condition is satisfied, we can make an external HTTP request using hello [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) policy.</span></span> <span data-ttu-id="78947-112">Dit kan een aanvraag tooa berichtensysteem zoals Hipchat of vertraging of een e-mailbericht API zoals SendGrid of MailChimp, of voor kritieke ondersteuningsaanvragen als PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="78947-112">This could be a request tooa messaging system like Hipchat or Slack, or a mail API like SendGrid or MailChimp, or for critical support incidents something like PagerDuty.</span></span> <span data-ttu-id="78947-113">Alle deze berichtsystemen hebben eenvoudige HTTP-APIs die we kunnen eenvoudig worden aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="78947-113">All of these messaging systems have simple HTTP APIs that we can easily invoke.</span></span>

### <a name="alerting-with-slack"></a><span data-ttu-id="78947-114">Waarschuwingen met Slack</span><span class="sxs-lookup"><span data-stu-id="78947-114">Alerting with Slack</span></span>
<span data-ttu-id="78947-115">Hallo volgende voorbeeld laat zien hoe een bericht tooa toosend vertraging chat ruimte als Hallo HTTP-code voor antwoordstatus is groter dan of gelijk zijn aan too500.</span><span class="sxs-lookup"><span data-stu-id="78947-115">hello following example demonstrates how toosend a message tooa Slack chat room if hello HTTP response status code is greater than or equal too500.</span></span> <span data-ttu-id="78947-116">Een 500-bereikfout geeft aan zichzelf kan niet worden omgezet door een probleem met onze end-API die Hallo-client van de API.</span><span class="sxs-lookup"><span data-stu-id="78947-116">A 500 range error indicates a problem with our backend API that hello client of our API cannot resolve themselves.</span></span> <span data-ttu-id="78947-117">Normaal gesproken een soort interventie van onze kant.</span><span class="sxs-lookup"><span data-stu-id="78947-117">It usually requires some kind of intervention on our part.</span></span>  

```xml
<choose>
    <when condition="@(context.Response.StatusCode >= 500)">
      <send-one-way-request mode="new">
        <set-url>https://hooks.slack.com/services/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</set-url>
        <set-method>POST</set-method>
        <set-body>@{
                return new JObject(
                        new JProperty("username","APIM Alert"),
                        new JProperty("icon_emoji", ":ghost:"),
                        new JProperty("text", String.Format("{0} {1}\nHost: {2}\n{3} {4}\n User: {5}",
                                                context.Request.Method,
                                                context.Request.Url.Path + context.Request.Url.QueryString,
                                                context.Request.Url.Host,
                                                context.Response.StatusCode,
                                                context.Response.StatusReason,
                                                context.User.Email
                                                ))
                        ).ToString();
            }</set-body>
      </send-one-way-request>
    </when>
</choose>
```

<span data-ttu-id="78947-118">Vertraging heeft Hallo begrip van inkomende web hooks.</span><span class="sxs-lookup"><span data-stu-id="78947-118">Slack has hello notion of inbound web hooks.</span></span> <span data-ttu-id="78947-119">Bij het configureren van een binnenkomende web haakje genereert Slack een speciale URL waarmee u een eenvoudige POST-aanvraag toodo en toopass een bericht in Hallo ongebruikt kanaal.</span><span class="sxs-lookup"><span data-stu-id="78947-119">When configuring an inbound web hook, Slack generates a special URL which allows you toodo a simple POST request and toopass a message into hello Slack channel.</span></span> <span data-ttu-id="78947-120">Hallo JSON-hoofdtekst die we maken is gebaseerd op een indeling die is gedefinieerd door vertraging.</span><span class="sxs-lookup"><span data-stu-id="78947-120">hello JSON body that we create is based on a format defined by Slack.</span></span>

![Toegestane Web haakje](./media/api-management-sample-send-request/api-management-slack-webhook.png)

### <a name="is-fire-and-forget-good-enough"></a><span data-ttu-id="78947-122">Fire is en goed vergeten?</span><span class="sxs-lookup"><span data-stu-id="78947-122">Is fire and forget good enough?</span></span>
<span data-ttu-id="78947-123">Er zijn bepaalde voor-en nadelen wanneer u een stijl fire en vergeet van aanvraag.</span><span class="sxs-lookup"><span data-stu-id="78947-123">There are certain tradeoffs when using a fire-and-forget style of request.</span></span> <span data-ttu-id="78947-124">Als voor een bepaalde reden Hallo aanvraag mislukt en Hallo fout niet worden gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="78947-124">If for some reason, hello request fails, then hello failure will not be reported.</span></span> <span data-ttu-id="78947-125">In dit geval is Hallo complexiteit van het met een secundaire fout rapportagesysteem en Hallo extra kosten van wachten op antwoord Hallo niet gerechtvaardigd.</span><span class="sxs-lookup"><span data-stu-id="78947-125">In this particular situation, hello complexity of having a secondary failure reporting system and hello additional performance cost of waiting for hello response is not warranted.</span></span> <span data-ttu-id="78947-126">Voor scenario's waarin het antwoord van essentiële toocheck Hallo, vervolgens Hallo [aanvragen verzenden](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) beleid is een betere optie.</span><span class="sxs-lookup"><span data-stu-id="78947-126">For scenarios where it is essential toocheck hello response, then hello [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) policy is a better option.</span></span>

## <a name="send-request"></a><span data-ttu-id="78947-127">Aanvragen verzenden</span><span class="sxs-lookup"><span data-stu-id="78947-127">Send-Request</span></span>
<span data-ttu-id="78947-128">Hallo `send-request` beleid schakelt u met behulp van een externe service tooperform complexe verwerking van functies en beleidsretourgegevens toohello API management-service die kan worden gebruikt voor verdere beleidsverwerking.</span><span class="sxs-lookup"><span data-stu-id="78947-128">hello `send-request` policy enables using an external service tooperform complex processing functions and return data toohello API management service that can be used for further policy processing.</span></span>

### <a name="authorizing-reference-tokens"></a><span data-ttu-id="78947-129">Verwijzingstokens autoriseren</span><span class="sxs-lookup"><span data-stu-id="78947-129">Authorizing reference tokens</span></span>
<span data-ttu-id="78947-130">Een belangrijke functie van API Management met het beveiligen van de back-end-bronnen.</span><span class="sxs-lookup"><span data-stu-id="78947-130">A major function of API Management is protecting backend resources.</span></span> <span data-ttu-id="78947-131">Als Hallo autorisatie-server die wordt gebruikt door uw API maakt [JWT-tokens](http://jwt.io/) als onderdeel van de stroom OAuth2 als [Azure Active Directory](../active-directory/active-directory-aadconnect.md) komt, kunt u Hallo `validate-jwt` beleid tooverify Hallo geldigheid van Hallo-token.</span><span class="sxs-lookup"><span data-stu-id="78947-131">If hello authorization server used by your API creates [JWT tokens](http://jwt.io/) as part of its OAuth2 flow, as [Azure Active Directory](../active-directory/active-directory-aadconnect.md) does, then you can use hello `validate-jwt` policy tooverify hello validity of hello token.</span></span> <span data-ttu-id="78947-132">Echter enkele autorisatieservers maken zogenaamde [verwijzen naar tokens](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) die zonder dat een aanroep back toohello autorisatie-server kan niet worden geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="78947-132">However, some authorization servers create what are called [reference tokens](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) that cannot be verified without making a call back toohello authorization server.</span></span>

### <a name="standardized-introspection"></a><span data-ttu-id="78947-133">Gestandaardiseerde introspection</span><span class="sxs-lookup"><span data-stu-id="78947-133">Standardized introspection</span></span>
<span data-ttu-id="78947-134">In de afgelopen Hallo is er geen gestandaardiseerde manier om een verwijzingstoken met een server van de autorisatie te controleren.</span><span class="sxs-lookup"><span data-stu-id="78947-134">In hello past there has been no standardized way of verifying a reference token with an authorization server.</span></span> <span data-ttu-id="78947-135">Echter een onlangs voorgestelde standaard [RFC 7662](https://tools.ietf.org/html/rfc7662) is gepubliceerd door Hallo IETF die definieert hoe een bronserver Hallo geldigheid van een token kunt controleren.</span><span class="sxs-lookup"><span data-stu-id="78947-135">However a recently proposed standard [RFC 7662](https://tools.ietf.org/html/rfc7662) was published by hello IETF that defines how a resource server can verify hello validity of a token.</span></span>

### <a name="extracting-hello-token"></a><span data-ttu-id="78947-136">Hallo-token ophalen</span><span class="sxs-lookup"><span data-stu-id="78947-136">Extracting hello token</span></span>
<span data-ttu-id="78947-137">de eerste stap Hallo is tooextract Hallo-token van Hallo autorisatie-header.</span><span class="sxs-lookup"><span data-stu-id="78947-137">hello first step is tooextract hello token from hello Authorization header.</span></span> <span data-ttu-id="78947-138">Hallo-header-waarde moet zijn geformatteerd met Hallo `Bearer` autorisatieschema, een spatie en vervolgens Hallo autorisatie token conform [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1).</span><span class="sxs-lookup"><span data-stu-id="78947-138">hello header value should be formatted with hello `Bearer` authorization scheme, a single space and then hello authorization token as per [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1).</span></span> <span data-ttu-id="78947-139">Er zijn helaas gevallen waarbij Hallo autorisatieschema wordt weggelaten.</span><span class="sxs-lookup"><span data-stu-id="78947-139">Unfortunately there are cases where hello authorization scheme is omitted.</span></span> <span data-ttu-id="78947-140">tooaccount voor deze tijdens het parseren van, we splitsen Hallo headerwaarde op een spatie en selecteer Hallo laatste tekenreeks uit Hallo matrix met tekenreeksen die zijn geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="78947-140">tooaccount for this when parsing, we split hello header value on a space and select hello last string from hello returned array of strings.</span></span> <span data-ttu-id="78947-141">Dit biedt een oplossing voor onjuist ingedeeld autorisatie-header.</span><span class="sxs-lookup"><span data-stu-id="78947-141">This provides a workaround for badly formatted authorization headers.</span></span>

```xml
<set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />
```

### <a name="making-hello-validation-request"></a><span data-ttu-id="78947-142">Hallo-validatieaanvraag maken</span><span class="sxs-lookup"><span data-stu-id="78947-142">Making hello validation request</span></span>
<span data-ttu-id="78947-143">Wanneer we Hallo verificatietoken hebt, maken we Hallo aanvraag toovalidate Hallo-token.</span><span class="sxs-lookup"><span data-stu-id="78947-143">Once we have hello authorization token, we can make hello request toovalidate hello token.</span></span> <span data-ttu-id="78947-144">RFC 7662 roept deze introspection proces en vereist dat u `POST` een HTML-formulier toohello introspection resource.</span><span class="sxs-lookup"><span data-stu-id="78947-144">RFC 7662 calls this process introspection and requires that you `POST` a HTML form toohello introspection resource.</span></span> <span data-ttu-id="78947-145">Hallo HTML-formulier moet ten minste een sleutel-waardepaar bevatten met Hallo sleutel `token`.</span><span class="sxs-lookup"><span data-stu-id="78947-145">hello HTML form must at least contain a key/value pair with hello key `token`.</span></span> <span data-ttu-id="78947-146">Deze aanvraag toohello autorisatie-server moet ook geverifieerde tooensure die schadelijke clients kunnen niet voor geldige-tokens sleepnetten gaat.</span><span class="sxs-lookup"><span data-stu-id="78947-146">This request toohello authorization server must also be authenticated tooensure that malicious clients cannot go trawling for valid tokens.</span></span>

```xml
<send-request mode="new" response-variable-name="tokenstate" timeout="20" ignore-error="true">
  <set-url>https://microsoft-apiappec990ad4c76641c6aea22f566efc5a4e.azurewebsites.net/introspection</set-url>
  <set-method>POST</set-method>
  <set-header name="Authorization" exists-action="override">
    <value>basic dXNlcm5hbWU6cGFzc3dvcmQ=</value>
  </set-header>
  <set-header name="Content-Type" exists-action="override">
    <value>application/x-www-form-urlencoded</value>
  </set-header>
  <set-body>@($"token={(string)context.Variables["token"]}")</set-body>
</send-request>
```

### <a name="checking-hello-response"></a><span data-ttu-id="78947-147">Antwoord Hallo controleren</span><span class="sxs-lookup"><span data-stu-id="78947-147">Checking hello response</span></span>
<span data-ttu-id="78947-148">Hallo `response-variable-name` kenmerk is gebruikte toogive toegang Hallo antwoord geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="78947-148">hello `response-variable-name` attribute is used toogive access hello returned response.</span></span> <span data-ttu-id="78947-149">Hallo naam zijn gedefinieerd in deze eigenschap kan worden gebruikt als een sleutel in Hallo `context.Variables` woordenlijst tooaccess hello `IResponse` object.</span><span class="sxs-lookup"><span data-stu-id="78947-149">hello name defined in this property can be used as a key into hello `context.Variables` dictionary tooaccess hello `IResponse` object.</span></span>

<span data-ttu-id="78947-150">Uit het Hallo-antwoordobject Hallo hoofdtekst kan worden opgehaald en RFC 7622 vertellen Hallo antwoord moet een JSON-object zijn, en moet ten minste een eigenschap met de naam bevatten `active` dat een Booleaanse waarde.</span><span class="sxs-lookup"><span data-stu-id="78947-150">From hello response object we can retrieve hello body and RFC 7622 tells us that hello response must be a JSON object and must contain at least a property called `active` that is a boolean value.</span></span> <span data-ttu-id="78947-151">Wanneer `active` is ingesteld op true en vervolgens het Hallo-token als geldig wordt aangemerkt.</span><span class="sxs-lookup"><span data-stu-id="78947-151">When `active` is true then hello token is considered valid.</span></span>

### <a name="reporting-failure"></a><span data-ttu-id="78947-152">Reporting is mislukt</span><span class="sxs-lookup"><span data-stu-id="78947-152">Reporting failure</span></span>
<span data-ttu-id="78947-153">We gebruiken een `<choose>` beleid toodetect als Hallo-token is ongeldig en als dat het geval is, retourneert een 401-respons.</span><span class="sxs-lookup"><span data-stu-id="78947-153">We use a `<choose>` policy toodetect if hello token is invalid and if so, return a 401 response.</span></span>

```xml
<choose>
  <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">
    <return-response response-variable-name="existing response variable">
      <set-status code="401" reason="Unauthorized" />
      <set-header name="WWW-Authenticate" exists-action="override">
        <value>Bearer error="invalid_token"</value>
      </set-header>
    </return-response>
  </when>
</choose>
```

<span data-ttu-id="78947-154">Als per [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3) waarin wordt beschreven hoe `bearer` tokens moeten worden gebruikt, wordt ook geretourneerd een `WWW-Authenticate` header met Hallo 401-respons.</span><span class="sxs-lookup"><span data-stu-id="78947-154">As per [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3) which describes how `bearer` tokens should be used, we also return a `WWW-Authenticate` header with hello 401 response.</span></span> <span data-ttu-id="78947-155">Hallo WWW-verificatie is bedoeld tooinstruct een client op het tooconstruct een goed ongeautoriseerde aanvraag.</span><span class="sxs-lookup"><span data-stu-id="78947-155">hello WWW-Authenticate is intended tooinstruct a client on how tooconstruct a properly authorized request.</span></span> <span data-ttu-id="78947-156">Vervaldatum toohello breed scala aan benaderingen mogelijk met Hallo OAuth2-framework, is het moeilijk toocommunicate alle Hallo informatie nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="78947-156">Due toohello wide variety of approaches possible with hello OAuth2 framework, it is difficult toocommunicate all hello needed information.</span></span> <span data-ttu-id="78947-157">Gelukkig zijn inspanningen Bezig toohelp [clients ontdekken hoe tooproperly aanvragen tooa bronserver autoriseren](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).</span><span class="sxs-lookup"><span data-stu-id="78947-157">Fortunately there are efforts underway toohelp [clients discover how tooproperly authorize requests tooa resource server](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).</span></span>

### <a name="final-solution"></a><span data-ttu-id="78947-158">Definitieve oplossing</span><span class="sxs-lookup"><span data-stu-id="78947-158">Final solution</span></span>
<span data-ttu-id="78947-159">Het samenstellen van alle Hallo stukken, krijgen we Hallo volgende beleid:</span><span class="sxs-lookup"><span data-stu-id="78947-159">Putting all hello pieces together, we get hello following policy:</span></span>

```xml
<inbound>
  <!-- Extract Token from Authorization header parameter -->
  <set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />

  <!-- Send request tooToken Server toovalidate token (see RFC 7662) -->
  <send-request mode="new" response-variable-name="tokenstate" timeout="20" ignore-error="true">
    <set-url>https://microsoft-apiappec990ad4c76641c6aea22f566efc5a4e.azurewebsites.net/introspection</set-url>
    <set-method>POST</set-method>
    <set-header name="Authorization" exists-action="override">
      <value>basic dXNlcm5hbWU6cGFzc3dvcmQ=</value>
    </set-header>
    <set-header name="Content-Type" exists-action="override">
      <value>application/x-www-form-urlencoded</value>
    </set-header>
    <set-body>@($"token={(string)context.Variables["token"]}")</set-body>
  </send-request>

  <choose>
          <!-- Check active property in response -->
          <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">
              <!-- Return 401 Unauthorized with http-problem payload -->
              <return-response response-variable-name="existing response variable">
                  <set-status code="401" reason="Unauthorized" />
                  <set-header name="WWW-Authenticate" exists-action="override">
                      <value>Bearer error="invalid_token"</value>
                  </set-header>
              </return-response>
          </when>
      </choose>
  <base />
</inbound>
```

<span data-ttu-id="78947-160">Dit is slechts een aantal voorbeelden van hoe Hallo `send-request` beleid gebruikte toointegrate nuttig externe services samen Hallo-proces voor aanvragen en antwoorden tot Hallo API Management-service kan worden.</span><span class="sxs-lookup"><span data-stu-id="78947-160">This is only one of many examples of how hello `send-request` policy can be used toointegrate useful external services into hello process of requests and responses flowing through hello API Management service.</span></span>

## <a name="response-composition"></a><span data-ttu-id="78947-161">Antwoord samenstelling</span><span class="sxs-lookup"><span data-stu-id="78947-161">Response Composition</span></span>
<span data-ttu-id="78947-162">Hallo `send-request` beleid kan worden gebruikt voor het verbeteren van een primaire aanvraag tooa back-end-systeem als hebt gezien in het vorige voorbeeld Hallo of het kan worden gebruikt als een volledige vervangen voor van Hallo back-end-aanroep.</span><span class="sxs-lookup"><span data-stu-id="78947-162">hello `send-request` policy can be used for enhancing a primary request tooa backend system, as we saw in hello previous example, or it can be used as a complete replace for of hello backend call.</span></span> <span data-ttu-id="78947-163">Met deze techniek kunnen we gemakkelijk maken samengestelde bronnen die worden samengevoegd uit meerdere verschillende systemen.</span><span class="sxs-lookup"><span data-stu-id="78947-163">Using this technique we can easily create composite resources that are aggregated from multiple different systems.</span></span>

### <a name="building-a-dashboard"></a><span data-ttu-id="78947-164">Een dashboard maken</span><span class="sxs-lookup"><span data-stu-id="78947-164">Building a dashboard</span></span>
<span data-ttu-id="78947-165">Soms wilt u toobe kunnen tooexpose informatie die in meerdere back endsystemen voorkomt bijvoorbeeld toodrive een dashboard.</span><span class="sxs-lookup"><span data-stu-id="78947-165">Sometimes you want toobe able tooexpose information that exists in multiple backend systems, for example, toodrive a dashboard.</span></span> <span data-ttu-id="78947-166">Hallo KPI's afkomstig zijn van alle verschillende back-ends, maar u liever niet tooprovide directe toegang toothem en het normaal zou zijn nice als alle Hallo-gegevens in één aanvraag kunnen worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="78947-166">hello KPIs come from all different back-ends, but you would prefer not tooprovide direct access toothem and it would be nice if all hello information could be retrieved in a single request.</span></span> <span data-ttu-id="78947-167">Sommige Hallo back-end gegevens moet mogelijk bepaalde segmenteren en opdelen en eerst een beetje opschonen!</span><span class="sxs-lookup"><span data-stu-id="78947-167">Perhaps some of hello backend information needs some slicing and dicing and a little sanitizing first!</span></span> <span data-ttu-id="78947-168">Kan toocache samengestelde bron is een nuttig tooreduce wordt Hallo back-end laden als u weet dat gebruikers hebben een gewoonte van Hallo F5-toets in volgorde toosee hammering als hun underperforming metrische gegevens kan worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="78947-168">Being able toocache that composite resource would be a useful tooreduce hello backend load as you know users have a habit of hammering hello F5 key in order toosee if their underperforming metrics might change.</span></span>    

### <a name="faking-hello-resource"></a><span data-ttu-id="78947-169">Hallo resource faking</span><span class="sxs-lookup"><span data-stu-id="78947-169">Faking hello resource</span></span>
<span data-ttu-id="78947-170">eerste stap toobuilding Hallo onze dashboard-bron is een nieuwe bewerking in de publicatieportal van API Management Hallo tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="78947-170">hello first step toobuilding our dashboard resource is tooconfigure a new operation in hello API Management publisher portal.</span></span> <span data-ttu-id="78947-171">Dit is een tijdelijke aanduiding voor bewerking gebruikt tooconfigure onze samenstelling beleid toobuild onze dynamische bron.</span><span class="sxs-lookup"><span data-stu-id="78947-171">This will be a placeholder operation used tooconfigure our composition policy toobuild our dynamic resource.</span></span>

![Dashboard-bewerking](./media/api-management-sample-send-request/api-management-dashboard-operation.png)

### <a name="making-hello-requests"></a><span data-ttu-id="78947-173">Hallo-aanvragen</span><span class="sxs-lookup"><span data-stu-id="78947-173">Making hello requests</span></span>
<span data-ttu-id="78947-174">Eenmaal Hallo `dashboard` bewerking is gemaakt kunnen we een beleid specifiek voor die bewerking configureren.</span><span class="sxs-lookup"><span data-stu-id="78947-174">Once hello `dashboard` operation has been created we can configure a policy specifically for that operation.</span></span> 

![Dashboard-bewerking](./media/api-management-sample-send-request/api-management-dashboard-policy.png)

<span data-ttu-id="78947-176">de eerste stap Hallo tooextract is queryparameters van Hallo inkomende aanvraag, zodat we ze tooour back-end kan doorsturen.</span><span class="sxs-lookup"><span data-stu-id="78947-176">hello first step  is tooextract any query parameters from hello incoming request, so that we can forward them tooour backend.</span></span> <span data-ttu-id="78947-177">In dit voorbeeld onze dashboard op basis van een bepaalde periode informatie wordt weergegeven een daarom heeft een `fromDate` en `toDate` parameter.</span><span class="sxs-lookup"><span data-stu-id="78947-177">In this example our dashboard is showing information based on a period of time an therefore has a `fromDate` and `toDate` parameter.</span></span> <span data-ttu-id="78947-178">We kunnen hello gebruiken `set-variable` tooextract Hallo beleidsgegevens van Hallo aanvraag-URL.</span><span class="sxs-lookup"><span data-stu-id="78947-178">We can use hello `set-variable` policy tooextract hello information from hello request URL.</span></span>

```xml
<set-variable name="fromDate" value="@(context.Request.Url.Query["fromDate"].Last())">
<set-variable name="toDate" value="@(context.Request.Url.Query["toDate"].Last())">
```

<span data-ttu-id="78947-179">Zodra deze informatie kunnen we aanvragen tooall Hallo back-end-systemen.</span><span class="sxs-lookup"><span data-stu-id="78947-179">Once we have this information we can make requests tooall hello backend systems.</span></span> <span data-ttu-id="78947-180">Elke aanvraag vormt een nieuwe URL met informatie voor de parameter Hallo en roept de desbetreffende server en antwoord Hallo opslaat in een context-variabele.</span><span class="sxs-lookup"><span data-stu-id="78947-180">Each request constructs a new URL with hello parameter information and calls its respective server and stores hello response in a context variable.</span></span>

```xml
<send-request mode="new" response-variable-name="revenuedata" timeout="20" ignore-error="true">
  <set-url>@($"https://accounting.acme.com/salesdata?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>

<send-request mode="new" response-variable-name="materialdata" timeout="20" ignore-error="true">
  <set-url>@($"https://inventory.acme.com/materiallevels?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>

<send-request mode="new" response-variable-name="throughputdata" timeout="20" ignore-error="true">
<set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>

<send-request mode="new" response-variable-name="accidentdata" timeout="20" ignore-error="true">
<set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>
```

<span data-ttu-id="78947-181">Deze aanvragen worden uitgevoerd in de juiste volgorde niet ideaal is.</span><span class="sxs-lookup"><span data-stu-id="78947-181">These requests will execute in sequence, which is not ideal.</span></span> <span data-ttu-id="78947-182">In een toekomstige release we een nieuw beleid aangeroepen introducing `wait` waarmee al deze aanvragen tooexecute parallel.</span><span class="sxs-lookup"><span data-stu-id="78947-182">In an upcoming release we will be introducing a new policy called `wait` that will enable all of these requests tooexecute in parallel.</span></span>

### <a name="responding"></a><span data-ttu-id="78947-183">Reageert</span><span class="sxs-lookup"><span data-stu-id="78947-183">Responding</span></span>
<span data-ttu-id="78947-184">tooconstruct samengestelde antwoord Hallo gebruiken we Hallo [return antwoord](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) beleid.</span><span class="sxs-lookup"><span data-stu-id="78947-184">tooconstruct hello composite response we can use hello [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) policy.</span></span> <span data-ttu-id="78947-185">Hallo `set-body` element kunt een expressie tooconstruct een nieuwe `JObject` met alle Hallo onderdeel verklaringen ingesloten als eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="78947-185">hello `set-body` element can use an expression tooconstruct a new `JObject` with all hello component representations embedded as properties.</span></span>

```xml
<return-response response-variable-name="existing response variable">
  <set-status code="200" reason="OK" />
  <set-header name="Content-Type" exists-action="override">
    <value>application/json</value>
  </set-header>
  <set-body>
    @(new JObject(new JProperty("revenuedata",((IResponse)context.Variables["revenuedata"]).Body.As<JObject>()),
                  new JProperty("materialdata",((IResponse)context.Variables["materialdata"]).Body.As<JObject>()),
                  new JProperty("throughputdata",((IResponse)context.Variables["throughputdata"]).Body.As<JObject>()),
                  new JProperty("accidentdata",((IResponse)context.Variables["accidentdata"]).Body.As<JObject>())
                  ).ToString())
  </set-body>
</return-response>
```

<span data-ttu-id="78947-186">Hallo voltooid beleid ziet er als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="78947-186">hello complete policy looks as follows:</span></span>

```xml
<policies>
    <inbound>

  <set-variable name="fromDate" value="@(context.Request.Url.Query["fromDate"].Last())">
  <set-variable name="toDate" value="@(context.Request.Url.Query["toDate"].Last())">

    <send-request mode="new" response-variable-name="revenuedata" timeout="20" ignore-error="true">
      <set-url>@($"https://accounting.acme.com/salesdata?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <send-request mode="new" response-variable-name="materialdata" timeout="20" ignore-error="true">
      <set-url>@($"https://inventory.acme.com/materiallevels?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <send-request mode="new" response-variable-name="throughputdata" timeout="20" ignore-error="true">
    <set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <send-request mode="new" response-variable-name="accidentdata" timeout="20" ignore-error="true">
    <set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <return-response response-variable-name="existing response variable">
      <set-status code="200" reason="OK" />
      <set-header name="Content-Type" exists-action="override">
        <value>application/json</value>
      </set-header>
      <set-body>
        @(new JObject(new JProperty("revenuedata",((IResponse)context.Variables["revenuedata"]).Body.As<JObject>()),
                      new JProperty("materialdata",((IResponse)context.Variables["materialdata"]).Body.As<JObject>()),
                      new JProperty("throughputdata",((IResponse)context.Variables["throughputdata"]).Body.As<JObject>()),
                      new JProperty("accidentdata",((IResponse)context.Variables["accidentdata"]).Body.As<JObject>())
                      ).ToString())
      </set-body>
    </return-response>
    </inbound>
    <backend>
        <base />
    </backend>
    <outbound>
        <base />
    </outbound>
</policies>
```

<span data-ttu-id="78947-187">In de configuratie van Hallo tijdelijke aanduiding voor bewerking die kunnen we configureren Hallo Hallo dashboard resource toobe in cache opgeslagen voor ten minste een uur omdat we Hallo aard van Hallo gegevens houdt in dat zelfs als deze een verouderd begrijpen, dat nog steeds moeten voldoende effectieve uur tooconvey waardevolle informatie toohello gebruikers.</span><span class="sxs-lookup"><span data-stu-id="78947-187">In hello configuration of hello placeholder operation we can configure hello dashboard resource toobe cached for at least an hour because we understand hello nature of hello data means that even if it is an hour out of date, it will still be sufficiently effective tooconvey valuable information toohello users.</span></span>

## <a name="summary"></a><span data-ttu-id="78947-188">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="78947-188">Summary</span></span>
<span data-ttu-id="78947-189">Azure API Management-service biedt flexibele beleidsregels die selectief kunnen worden toegepast tooHTTP verkeer en Hiermee samenstelling van back-end-services.</span><span class="sxs-lookup"><span data-stu-id="78947-189">Azure API Management service provides flexible policies that can be selectively applied tooHTTP traffic and enables composition of backend services.</span></span> <span data-ttu-id="78947-190">Of u wilt dat tooenhance uw API-gateway met waarschuwingen, functies, verificatie, validatie mogelijkheden of maken van nieuwe samengestelde resources op basis van meerdere back-end-services, Hallo `send-request` en bijbehorende beleid opent u een wereld van mogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="78947-190">Whether you want tooenhance your API gateway with alerting functions, verification, validation capabilities or create new composite resources based on multiple backend services, hello `send-request` and related policies open a world of possibilities.</span></span>

## <a name="watch-a-video-overview-of-these-policies"></a><span data-ttu-id="78947-191">Bekijk een video-overzicht van deze beleidsregels</span><span class="sxs-lookup"><span data-stu-id="78947-191">Watch a video overview of these policies</span></span>
<span data-ttu-id="78947-192">Voor meer informatie over Hallo [-één-manier-Verzendaanvraag](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [aanvragen verzenden](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest), en [return antwoord](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) beleidsregels die in dit artikel, neem Hallo volgende video bekijken.</span><span class="sxs-lookup"><span data-stu-id="78947-192">For more information on hello [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest), and [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) policies covered in this article, please watch hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Send-Request-and-Return-Response-Policies/player]
> 
> 

