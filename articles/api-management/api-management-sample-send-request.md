---
title: Met behulp van API Management-service voor het genereren van HTTP-aanvragen
description: Informatie over het gebruik van beleidsregels voor aanvraag en antwoord in API Management externe services van uw API niet aanroepen
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
ms.openlocfilehash: e778943715d6ca5256ad612d82bdc1f82197df0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="using-external-services-from-the-azure-api-management-service"></a><span data-ttu-id="0ccd0-103">Met behulp van externe services van de Azure API Management-service</span><span class="sxs-lookup"><span data-stu-id="0ccd0-103">Using external services from the Azure API Management service</span></span>
<span data-ttu-id="0ccd0-104">De beleidsregels die beschikbaar zijn in Azure API Management-service kan een breed scala aan goed functioneren op basis van uitsluitend op de inkomende aanvraag, het uitgaande antwoord en basisinformatie over de configuratie kunnen doen.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-104">The policies available in Azure API Management service can do a wide range of useful work based purely on the incoming request, the outgoing response and basic configuration information.</span></span> <span data-ttu-id="0ccd0-105">Echter, kunnen communiceren met externe services van API Management beleid wordt geopend veel meer mogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-105">However, being able to interact with external services from API Management policies opens up many more opportunities.</span></span>

<span data-ttu-id="0ccd0-106">We eerder hebben gezien hoe we kunnen werken met de [Azure Event Hub-service voor logboekregistratie, bewaken en analytics](api-management-log-to-eventhub-sample.md).</span><span class="sxs-lookup"><span data-stu-id="0ccd0-106">We have previously seen how we can interact with the [Azure Event Hub service for logging, monitoring and analytics](api-management-log-to-eventhub-sample.md).</span></span> <span data-ttu-id="0ccd0-107">In dit artikel wordt gedemonstreerd service op basis van beleid waarmee u communiceren met een externe HTTP.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-107">In this article we will demonstrate policies that allow you to interact with any external HTTP based service.</span></span> <span data-ttu-id="0ccd0-108">Dit beleid kunnen worden gebruikt voor activering van externe gebeurtenissen of voor het ophalen van informatie die wordt gebruikt om de oorspronkelijke aanvraag en antwoord op een bepaalde manier te bewerken.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-108">These policies can be used for triggering remote events or for retrieving information that will be used to manipulate the original request and response in some way.</span></span>

## <a name="send-one-way-request"></a><span data-ttu-id="0ccd0-109">Een-manier-verzoek om te verzenden</span><span class="sxs-lookup"><span data-stu-id="0ccd0-109">Send-One-Way-Request</span></span>
<span data-ttu-id="0ccd0-110">Mogelijk de meest eenvoudige externe interactie wordt de stijl die wordt gestart en vergeet van aanvraag waarmee een externe service op de hoogte gesteld van een soort belangrijke gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-110">Possibly the simplest external interaction is the fire-and-forget style of request that allows an external service to be notified of some kind of important event.</span></span> <span data-ttu-id="0ccd0-111">Gebruiken we het beleid voor toegangsbeheer stroom `choose` voor het detecteren van elk soort voorwaarde dat we geïnteresseerd bent in en klik, als de voorwaarde is voldaan, kunnen we een externe HTTP-aanvraag met de [-één-manier-Verzendaanvraag](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) beleid.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-111">We can use the control flow policy `choose` to detect any kind of condition that we are interested in and then, if the condition is satisfied, we can make an external HTTP request using the [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) policy.</span></span> <span data-ttu-id="0ccd0-112">Dit kan een aanvraag naar een berichtensysteem zoals Hipchat of vertraging of een e-mailbericht API zoals SendGrid of MailChimp, of voor kritieke ondersteuningsaanvragen als PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-112">This could be a request to a messaging system like Hipchat or Slack, or a mail API like SendGrid or MailChimp, or for critical support incidents something like PagerDuty.</span></span> <span data-ttu-id="0ccd0-113">Alle deze berichtsystemen hebben eenvoudige HTTP-APIs die we kunnen eenvoudig worden aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-113">All of these messaging systems have simple HTTP APIs that we can easily invoke.</span></span>

### <a name="alerting-with-slack"></a><span data-ttu-id="0ccd0-114">Waarschuwingen met Slack</span><span class="sxs-lookup"><span data-stu-id="0ccd0-114">Alerting with Slack</span></span>
<span data-ttu-id="0ccd0-115">Het volgende voorbeeld laat zien hoe u een bericht te verzenden naar toegestane chatruimten als de HTTP-statuscode van antwoord groter dan of gelijk zijn aan 500 is.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-115">The following example demonstrates how to send a message to a Slack chat room if the HTTP response status code is greater than or equal to 500.</span></span> <span data-ttu-id="0ccd0-116">Een 500-bereikfout duidt op een probleem met onze end-API die de client van onze API kan zichzelf niet omzetten.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-116">A 500 range error indicates a problem with our backend API that the client of our API cannot resolve themselves.</span></span> <span data-ttu-id="0ccd0-117">Normaal gesproken een soort interventie van onze kant.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-117">It usually requires some kind of intervention on our part.</span></span>  

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

<span data-ttu-id="0ccd0-118">Vertraging heeft het begrip van inkomende web haken.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-118">Slack has the notion of inbound web hooks.</span></span> <span data-ttu-id="0ccd0-119">Bij het configureren van een binnenkomende web haakje genereert Slack een speciale URL waarmee u een eenvoudige POST-aanvraag en het doorgeven van een bericht in de ongebruikt kanaal.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-119">When configuring an inbound web hook, Slack generates a special URL which allows you to do a simple POST request and to pass a message into the Slack channel.</span></span> <span data-ttu-id="0ccd0-120">De JSON-hoofdtekst die we maken is gebaseerd op een indeling die is gedefinieerd door vertraging.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-120">The JSON body that we create is based on a format defined by Slack.</span></span>

![Toegestane Web haakje](./media/api-management-sample-send-request/api-management-slack-webhook.png)

### <a name="is-fire-and-forget-good-enough"></a><span data-ttu-id="0ccd0-122">Fire is en goed vergeten?</span><span class="sxs-lookup"><span data-stu-id="0ccd0-122">Is fire and forget good enough?</span></span>
<span data-ttu-id="0ccd0-123">Er zijn bepaalde voor-en nadelen wanneer u een stijl fire en vergeet van aanvraag.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-123">There are certain tradeoffs when using a fire-and-forget style of request.</span></span> <span data-ttu-id="0ccd0-124">Als voor een bepaalde reden mislukt de aanvraag en de fout wordt niet gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-124">If for some reason, the request fails, then the failure will not be reported.</span></span> <span data-ttu-id="0ccd0-125">In dit geval wordt de complexiteit van een secundaire fout reporting systeem en de extra kosten van het wachten op het antwoord dat niet gerechtvaardigd.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-125">In this particular situation, the complexity of having a secondary failure reporting system and the additional performance cost of waiting for the response is not warranted.</span></span> <span data-ttu-id="0ccd0-126">Voor scenario's waar het is essentieel om te controleren van het antwoord, wordt de [aanvragen verzenden](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) beleid is een betere optie.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-126">For scenarios where it is essential to check the response, then the [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) policy is a better option.</span></span>

## <a name="send-request"></a><span data-ttu-id="0ccd0-127">Aanvragen verzenden</span><span class="sxs-lookup"><span data-stu-id="0ccd0-127">Send-Request</span></span>
<span data-ttu-id="0ccd0-128">De `send-request` beleid maakt gebruik van een externe service voor complexe verwerkingsfuncties uitvoeren en retourneren van gegevens naar de API management-service kunnen worden gebruikt voor verdere beleidsverwerking.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-128">The `send-request` policy enables using an external service to perform complex processing functions and return data to the API management service that can be used for further policy processing.</span></span>

### <a name="authorizing-reference-tokens"></a><span data-ttu-id="0ccd0-129">Verwijzingstokens autoriseren</span><span class="sxs-lookup"><span data-stu-id="0ccd0-129">Authorizing reference tokens</span></span>
<span data-ttu-id="0ccd0-130">Een belangrijke functie van API Management met het beveiligen van de back-end-bronnen.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-130">A major function of API Management is protecting backend resources.</span></span> <span data-ttu-id="0ccd0-131">Als de autorisatie-server die wordt gebruikt door uw API maakt [JWT-tokens](http://jwt.io/) als onderdeel van de stroom OAuth2 als [Azure Active Directory](../active-directory/active-directory-aadconnect.md) komt, kunt u de `validate-jwt` beleid om de geldigheid van het token.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-131">If the authorization server used by your API creates [JWT tokens](http://jwt.io/) as part of its OAuth2 flow, as [Azure Active Directory](../active-directory/active-directory-aadconnect.md) does, then you can use the `validate-jwt` policy to verify the validity of the token.</span></span> <span data-ttu-id="0ccd0-132">Echter enkele autorisatieservers maken zogenaamde [verwijzen naar tokens](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) die zonder dat een aanroep naar de autorisatie-server kan niet worden geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-132">However, some authorization servers create what are called [reference tokens](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) that cannot be verified without making a call back to the authorization server.</span></span>

### <a name="standardized-introspection"></a><span data-ttu-id="0ccd0-133">Gestandaardiseerde introspection</span><span class="sxs-lookup"><span data-stu-id="0ccd0-133">Standardized introspection</span></span>
<span data-ttu-id="0ccd0-134">In het verleden is er geen gestandaardiseerde manier om een verwijzingstoken met een server van de autorisatie te controleren.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-134">In the past there has been no standardized way of verifying a reference token with an authorization server.</span></span> <span data-ttu-id="0ccd0-135">Echter een onlangs voorgestelde standaard [RFC 7662](https://tools.ietf.org/html/rfc7662) is gepubliceerd door de IETF die definieert hoe een resource-server kan de geldigheid van een token.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-135">However a recently proposed standard [RFC 7662](https://tools.ietf.org/html/rfc7662) was published by the IETF that defines how a resource server can verify the validity of a token.</span></span>

### <a name="extracting-the-token"></a><span data-ttu-id="0ccd0-136">Het uitpakken van het token</span><span class="sxs-lookup"><span data-stu-id="0ccd0-136">Extracting the token</span></span>
<span data-ttu-id="0ccd0-137">De eerste stap is het token ophalen uit de autorisatie-header.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-137">The first step is to extract the token from the Authorization header.</span></span> <span data-ttu-id="0ccd0-138">Waarde van de header moet zijn geformatteerd met het `Bearer` autorisatieschema, een spatie en vervolgens de autorisatie token conform [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1).</span><span class="sxs-lookup"><span data-stu-id="0ccd0-138">The header value should be formatted with the `Bearer` authorization scheme, a single space and then the authorization token as per [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1).</span></span> <span data-ttu-id="0ccd0-139">Er zijn helaas gevallen waarbij het autorisatieschema wordt weggelaten.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-139">Unfortunately there are cases where the authorization scheme is omitted.</span></span> <span data-ttu-id="0ccd0-140">Voor het account voor deze tijdens het parseren van we de waarde van de header op een spatie splitsen en selecteert u de laatste tekenreeks in de geretourneerde matrix van tekenreeksen.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-140">To account for this when parsing, we split the header value on a space and select the last string from the returned array of strings.</span></span> <span data-ttu-id="0ccd0-141">Dit biedt een oplossing voor onjuist ingedeeld autorisatie-header.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-141">This provides a workaround for badly formatted authorization headers.</span></span>

```xml
<set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />
```

### <a name="making-the-validation-request"></a><span data-ttu-id="0ccd0-142">Maken van de validatieaanvraag</span><span class="sxs-lookup"><span data-stu-id="0ccd0-142">Making the validation request</span></span>
<span data-ttu-id="0ccd0-143">Wanneer wij het verificatietoken hebt, maken we de aanvraag voor het valideren van het token.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-143">Once we have the authorization token, we can make the request to validate the token.</span></span> <span data-ttu-id="0ccd0-144">RFC 7662 roept deze introspection proces en vereist dat u `POST` een HTML-formulier op de resource introspection.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-144">RFC 7662 calls this process introspection and requires that you `POST` a HTML form to the introspection resource.</span></span> <span data-ttu-id="0ccd0-145">Het HTML-formulier moet ten minste een sleutel-waardepaar bevatten met de sleutel `token`.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-145">The HTML form must at least contain a key/value pair with the key `token`.</span></span> <span data-ttu-id="0ccd0-146">Deze aanvraag naar de autorisatie-server moet ook worden geverifieerd om ervoor te zorgen dat kwaadwillende clients kunnen niet voor geldige tokens sleepnetten gaat.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-146">This request to the authorization server must also be authenticated to ensure that malicious clients cannot go trawling for valid tokens.</span></span>

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

### <a name="checking-the-response"></a><span data-ttu-id="0ccd0-147">Het antwoord controleren</span><span class="sxs-lookup"><span data-stu-id="0ccd0-147">Checking the response</span></span>
<span data-ttu-id="0ccd0-148">De `response-variable-name` kenmerk wordt gebruikt om toegang te geven het geretourneerde antwoord.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-148">The `response-variable-name` attribute is used to give access the returned response.</span></span> <span data-ttu-id="0ccd0-149">De naam zijn gedefinieerd in deze eigenschap kan worden gebruikt als een sleutel in de `context.Variables` woordenlijst voor toegang tot de `IResponse` object.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-149">The name defined in this property can be used as a key into the `context.Variables` dictionary to access the `IResponse` object.</span></span>

<span data-ttu-id="0ccd0-150">Uit het antwoordobject kan de instantie worden opgehaald en RFC 7622 leest ons dat het antwoord een JSON-object moet, en moet ten minste een eigenschap genaamd bevatten `active` dat een Booleaanse waarde.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-150">From the response object we can retrieve the body and RFC 7622 tells us that the response must be a JSON object and must contain at least a property called `active` that is a boolean value.</span></span> <span data-ttu-id="0ccd0-151">Wanneer `active` is ingesteld op true en vervolgens het token als geldig wordt aangemerkt.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-151">When `active` is true then the token is considered valid.</span></span>

### <a name="reporting-failure"></a><span data-ttu-id="0ccd0-152">Reporting is mislukt</span><span class="sxs-lookup"><span data-stu-id="0ccd0-152">Reporting failure</span></span>
<span data-ttu-id="0ccd0-153">We gebruiken een `<choose>` beleid om te detecteren of het token ongeldig is en als dat het geval is, retourneert een 401-respons.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-153">We use a `<choose>` policy to detect if the token is invalid and if so, return a 401 response.</span></span>

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

<span data-ttu-id="0ccd0-154">Als per [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3) waarin wordt beschreven hoe `bearer` tokens moeten worden gebruikt, wordt ook geretourneerd een `WWW-Authenticate` header met de 401-respons.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-154">As per [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3) which describes how `bearer` tokens should be used, we also return a `WWW-Authenticate` header with the 401 response.</span></span> <span data-ttu-id="0ccd0-155">De WWW-verificatie is bedoeld om een client op het maken van een aanvraag goed geautoriseerde instrueren.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-155">The WWW-Authenticate is intended to instruct a client on how to construct a properly authorized request.</span></span> <span data-ttu-id="0ccd0-156">Vanwege de grote verscheidenheid aan benaderingen mogelijk met de OAuth2-framework is het lastig om alle benodigde informatie te communiceren.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-156">Due to the wide variety of approaches possible with the OAuth2 framework, it is difficult to communicate all the needed information.</span></span> <span data-ttu-id="0ccd0-157">Er zijn gelukkig pogingen uitgevoerd om te helpen [clients ontdekken hoe goed aanvragen naar een resource-server te autoriseren](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).</span><span class="sxs-lookup"><span data-stu-id="0ccd0-157">Fortunately there are efforts underway to help [clients discover how to properly authorize requests to a resource server](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).</span></span>

### <a name="final-solution"></a><span data-ttu-id="0ccd0-158">Definitieve oplossing</span><span class="sxs-lookup"><span data-stu-id="0ccd0-158">Final solution</span></span>
<span data-ttu-id="0ccd0-159">Het samenstellen van alle onderdelen, krijgen we het volgende beleid:</span><span class="sxs-lookup"><span data-stu-id="0ccd0-159">Putting all the pieces together, we get the following policy:</span></span>

```xml
<inbound>
  <!-- Extract Token from Authorization header parameter -->
  <set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />

  <!-- Send request to Token Server to validate token (see RFC 7662) -->
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

<span data-ttu-id="0ccd0-160">Dit is slechts een aantal voorbeelden van hoe de `send-request` beleid kan worden gebruikt om nuttige externe services integreren met het proces voor aanvragen en -antwoorden die door de API Management-service.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-160">This is only one of many examples of how the `send-request` policy can be used to integrate useful external services into the process of requests and responses flowing through the API Management service.</span></span>

## <a name="response-composition"></a><span data-ttu-id="0ccd0-161">Antwoord samenstelling</span><span class="sxs-lookup"><span data-stu-id="0ccd0-161">Response Composition</span></span>
<span data-ttu-id="0ccd0-162">De `send-request` beleid kan worden gebruikt voor het verbeteren van een primaire aanvraag voor een back endsysteem, zoals in het vorige voorbeeld hebt gezien, of het kan worden gebruikt als een volledige vervangen voor van de back-end-aanroep.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-162">The `send-request` policy can be used for enhancing a primary request to a backend system, as we saw in the previous example, or it can be used as a complete replace for of the backend call.</span></span> <span data-ttu-id="0ccd0-163">Met deze techniek kunnen we gemakkelijk maken samengestelde bronnen die worden samengevoegd uit meerdere verschillende systemen.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-163">Using this technique we can easily create composite resources that are aggregated from multiple different systems.</span></span>

### <a name="building-a-dashboard"></a><span data-ttu-id="0ccd0-164">Een dashboard maken</span><span class="sxs-lookup"><span data-stu-id="0ccd0-164">Building a dashboard</span></span>
<span data-ttu-id="0ccd0-165">Soms wilt u mogelijk gegevens die in meerdere back endsystemen, bijvoorbeeld voorkomt openbaar, om een dashboard.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-165">Sometimes you want to be able to expose information that exists in multiple backend systems, for example, to drive a dashboard.</span></span> <span data-ttu-id="0ccd0-166">De KPI's afkomstig zijn van alle verschillende back-ends, maar u liever niet voorzien in directe toegang tot en het normaal zou zijn handig als u alle gegevens in één aanvraag kan worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-166">The KPIs come from all different back-ends, but you would prefer not to provide direct access to them and it would be nice if all the information could be retrieved in a single request.</span></span> <span data-ttu-id="0ccd0-167">Enkele van de back-end-gegevens moet wellicht enkele segmenteren en opdelen en eerst een beetje opschonen!</span><span class="sxs-lookup"><span data-stu-id="0ccd0-167">Perhaps some of the backend information needs some slicing and dicing and a little sanitizing first!</span></span> <span data-ttu-id="0ccd0-168">Kunnen in de cache die samengestelde bron zou een nuttig zijn voor de back-end-belasting te verminderen, zoals u weet dat gebruikers hebben een gewoonte van hammering de toets F5 om te zien als hun underperforming metrische gegevens kan worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-168">Being able to cache that composite resource would be a useful to reduce the backend load as you know users have a habit of hammering the F5 key in order to see if their underperforming metrics might change.</span></span>    

### <a name="faking-the-resource"></a><span data-ttu-id="0ccd0-169">De resource faking</span><span class="sxs-lookup"><span data-stu-id="0ccd0-169">Faking the resource</span></span>
<span data-ttu-id="0ccd0-170">De eerste stap voor het ontwikkelen van onze dashboard-resource is voor het configureren van een nieuwe bewerking in de publicatieportal van API Management.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-170">The first step to building our dashboard resource is to configure a new operation in the API Management publisher portal.</span></span> <span data-ttu-id="0ccd0-171">Dit is een tijdelijke aanduiding voor bewerking gebruikt voor het configureren van ons beleid samenstelling om samen te stellen van onze dynamische bron.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-171">This will be a placeholder operation used to configure our composition policy to build our dynamic resource.</span></span>

![Dashboard-bewerking](./media/api-management-sample-send-request/api-management-dashboard-operation.png)

### <a name="making-the-requests"></a><span data-ttu-id="0ccd0-173">De aanvragen</span><span class="sxs-lookup"><span data-stu-id="0ccd0-173">Making the requests</span></span>
<span data-ttu-id="0ccd0-174">Eenmaal de `dashboard` bewerking is gemaakt kunnen we een beleid specifiek voor die bewerking configureren.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-174">Once the `dashboard` operation has been created we can configure a policy specifically for that operation.</span></span> 

![Dashboard-bewerking](./media/api-management-sample-send-request/api-management-dashboard-policy.png)

<span data-ttu-id="0ccd0-176">De eerste stap is queryparameters ophalen uit de binnenkomende aanvraag zodat we ze naar onze back-end doorsturen kan.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-176">The first step  is to extract any query parameters from the incoming request, so that we can forward them to our backend.</span></span> <span data-ttu-id="0ccd0-177">In dit voorbeeld onze dashboard op basis van een bepaalde periode informatie wordt weergegeven een daarom heeft een `fromDate` en `toDate` parameter.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-177">In this example our dashboard is showing information based on a period of time an therefore has a `fromDate` and `toDate` parameter.</span></span> <span data-ttu-id="0ccd0-178">Kunnen we gebruiken de `set-variable` beleid voor het ophalen van de informatie uit de aanvraag-URL.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-178">We can use the `set-variable` policy to extract the information from the request URL.</span></span>

```xml
<set-variable name="fromDate" value="@(context.Request.Url.Query["fromDate"].Last())">
<set-variable name="toDate" value="@(context.Request.Url.Query["toDate"].Last())">
```

<span data-ttu-id="0ccd0-179">Zodra deze informatie kunnen we aanvragen op alle back endsystemen.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-179">Once we have this information we can make requests to all the backend systems.</span></span> <span data-ttu-id="0ccd0-180">Elke aanvraag vormt een nieuwe URL met de parameterinformatie en roept de desbetreffende server en het antwoord worden opgeslagen in een context-variabele.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-180">Each request constructs a new URL with the parameter information and calls its respective server and stores the response in a context variable.</span></span>

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

<span data-ttu-id="0ccd0-181">Deze aanvragen worden uitgevoerd in de juiste volgorde niet ideaal is.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-181">These requests will execute in sequence, which is not ideal.</span></span> <span data-ttu-id="0ccd0-182">In een toekomstige release we een nieuw beleid aangeroepen introducing `wait` waarmee al deze aanvragen worden parallel uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-182">In an upcoming release we will be introducing a new policy called `wait` that will enable all of these requests to execute in parallel.</span></span>

### <a name="responding"></a><span data-ttu-id="0ccd0-183">Reageert</span><span class="sxs-lookup"><span data-stu-id="0ccd0-183">Responding</span></span>
<span data-ttu-id="0ccd0-184">Maken van de samengestelde reactie we gebruiken de [return antwoord](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) beleid.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-184">To construct the composite response we can use the [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) policy.</span></span> <span data-ttu-id="0ccd0-185">De `set-body` element een expressie kunt gebruiken om een nieuwe samen te stellen `JObject` met alle onderdeel verklaringen ingesloten als eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-185">The `set-body` element can use an expression to construct a new `JObject` with all the component representations embedded as properties.</span></span>

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

<span data-ttu-id="0ccd0-186">Het volledige beleid ziet er als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="0ccd0-186">The complete policy looks as follows:</span></span>

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

<span data-ttu-id="0ccd0-187">In de configuratie van de tijdelijke aanduiding voor betekent bewerking die kunnen we de resource dashboard voor ten minste een uur worden opgeslagen omdat we begrijpen de aard van de gegevens wat configureren dat zelfs als het een uur verouderd, dat nog steeds moeten voldoende effectieve om waardevolle informatie aan de gebruikers over te brengen.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-187">In the configuration of the placeholder operation we can configure the dashboard resource to be cached for at least an hour because we understand the nature of the data means that even if it is an hour out of date, it will still be sufficiently effective to convey valuable information to the users.</span></span>

## <a name="summary"></a><span data-ttu-id="0ccd0-188">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="0ccd0-188">Summary</span></span>
<span data-ttu-id="0ccd0-189">Azure API Management-service biedt flexibele beleidsregels die u kunnen selectief worden toegepast op HTTP-verkeer en Hiermee samenstelling van back-end-services.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-189">Azure API Management service provides flexible policies that can be selectively applied to HTTP traffic and enables composition of backend services.</span></span> <span data-ttu-id="0ccd0-190">Of u wilt uw API-gateway met waarschuwingen, functies, verificatie, validatie-mogelijkheden verbeteren of maken van nieuwe samengestelde resources op basis van meerdere back-end-services de `send-request` en bijbehorende beleid opent u een wereld van mogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-190">Whether you want to enhance your API gateway with alerting functions, verification, validation capabilities or create new composite resources based on multiple backend services, the `send-request` and related policies open a world of possibilities.</span></span>

## <a name="watch-a-video-overview-of-these-policies"></a><span data-ttu-id="0ccd0-191">Bekijk een video-overzicht van deze beleidsregels</span><span class="sxs-lookup"><span data-stu-id="0ccd0-191">Watch a video overview of these policies</span></span>
<span data-ttu-id="0ccd0-192">Voor meer informatie over de [-één-manier-Verzendaanvraag](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [aanvragen verzenden](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest), en [return antwoord](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) beleidsregels die in dit artikel, bekijk Neem de volgende video.</span><span class="sxs-lookup"><span data-stu-id="0ccd0-192">For more information on the [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest), and [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) policies covered in this article, please watch the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Send-Request-and-Return-Response-Policies/player]
> 
> 

