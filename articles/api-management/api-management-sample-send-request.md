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
# <a name="using-external-services-from-hello-azure-api-management-service"></a>Met behulp van externe services van hello Azure API Management-service
Hallo-beleid beschikbaar is in Azure API Management-service kan een breed scala aan goed functioneren op basis van uitsluitend op Hallo inkomende aanvraag, het uitgaande antwoord Hallo en basisinformatie over de configuratie kunnen doen. Echter, kunnen toointeract met externe services van API Management wordt beleid wordt geopend veel meer mogelijkheden.

We eerder hebben gezien hoe we kunnen werken met Hallo [Azure Event Hub-service voor logboekregistratie, bewaken en analytics](api-management-log-to-eventhub-sample.md). In dit artikel wordt gedemonstreerd service op basis van beleid waarmee u toointeract met een externe HTTP. Dit beleid kunnen worden gebruikt voor activering van externe gebeurtenissen of voor het ophalen van informatie die wordt gebruikt toomanipulate Hallo oorspronkelijke aanvraag en -antwoord op een bepaalde manier zijn.

## <a name="send-one-way-request"></a>Een-manier-verzoek om te verzenden
Mogelijk hello eenvoudigste externe interactie is Hallo fire en vergeet stijl van de aanvraag waarmee een externe service toobe de hoogte gesteld van een soort belangrijke gebeurtenis. We kunnen beleid voor toegangsbeheer stroom hello gebruiken `choose` toodetect elk soort voorwaarde bent geïnteresseerd en klikt u vervolgens aan als hello voorwaarde wordt voldaan, maken we een externe HTTP-aanvraag met Hallo [-één-manier-verzoek om te verzenden](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) beleid. Dit kan een aanvraag tooa berichtensysteem zoals Hipchat of vertraging of een e-mailbericht API zoals SendGrid of MailChimp, of voor kritieke ondersteuningsaanvragen als PagerDuty. Alle deze berichtsystemen hebben eenvoudige HTTP-APIs die we kunnen eenvoudig worden aangeroepen.

### <a name="alerting-with-slack"></a>Waarschuwingen met Slack
Hallo volgende voorbeeld laat zien hoe een bericht tooa toosend vertraging chat ruimte als Hallo HTTP-code voor antwoordstatus is groter dan of gelijk zijn aan too500. Een 500-bereikfout geeft aan zichzelf kan niet worden omgezet door een probleem met onze end-API die Hallo-client van de API. Normaal gesproken een soort interventie van onze kant.  

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

Vertraging heeft Hallo begrip van inkomende web hooks. Bij het configureren van een binnenkomende web haakje genereert Slack een speciale URL waarmee u een eenvoudige POST-aanvraag toodo en toopass een bericht in Hallo ongebruikt kanaal. Hallo JSON-hoofdtekst die we maken is gebaseerd op een indeling die is gedefinieerd door vertraging.

![Toegestane Web haakje](./media/api-management-sample-send-request/api-management-slack-webhook.png)

### <a name="is-fire-and-forget-good-enough"></a>Fire is en goed vergeten?
Er zijn bepaalde voor-en nadelen wanneer u een stijl fire en vergeet van aanvraag. Als voor een bepaalde reden Hallo aanvraag mislukt en Hallo fout niet worden gerapporteerd. In dit geval is Hallo complexiteit van het met een secundaire fout rapportagesysteem en Hallo extra kosten van wachten op antwoord Hallo niet gerechtvaardigd. Voor scenario's waarin het antwoord van essentiële toocheck Hallo, vervolgens Hallo [aanvragen verzenden](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) beleid is een betere optie.

## <a name="send-request"></a>Aanvragen verzenden
Hallo `send-request` beleid schakelt u met behulp van een externe service tooperform complexe verwerking van functies en beleidsretourgegevens toohello API management-service die kan worden gebruikt voor verdere beleidsverwerking.

### <a name="authorizing-reference-tokens"></a>Verwijzingstokens autoriseren
Een belangrijke functie van API Management met het beveiligen van de back-end-bronnen. Als Hallo autorisatie-server die wordt gebruikt door uw API maakt [JWT-tokens](http://jwt.io/) als onderdeel van de stroom OAuth2 als [Azure Active Directory](../active-directory/active-directory-aadconnect.md) komt, kunt u Hallo `validate-jwt` beleid tooverify Hallo geldigheid van Hallo-token. Echter enkele autorisatieservers maken zogenaamde [verwijzen naar tokens](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) die zonder dat een aanroep back toohello autorisatie-server kan niet worden geverifieerd.

### <a name="standardized-introspection"></a>Gestandaardiseerde introspection
In de afgelopen Hallo is er geen gestandaardiseerde manier om een verwijzingstoken met een server van de autorisatie te controleren. Echter een onlangs voorgestelde standaard [RFC 7662](https://tools.ietf.org/html/rfc7662) is gepubliceerd door Hallo IETF die definieert hoe een bronserver Hallo geldigheid van een token kunt controleren.

### <a name="extracting-hello-token"></a>Hallo-token ophalen
de eerste stap Hallo is tooextract Hallo-token van Hallo autorisatie-header. Hallo-header-waarde moet zijn geformatteerd met Hallo `Bearer` autorisatieschema, een spatie en vervolgens Hallo autorisatie token conform [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1). Er zijn helaas gevallen waarbij Hallo autorisatieschema wordt weggelaten. tooaccount voor deze tijdens het parseren van, we splitsen Hallo headerwaarde op een spatie en selecteer Hallo laatste tekenreeks uit Hallo matrix met tekenreeksen die zijn geretourneerd. Dit biedt een oplossing voor onjuist ingedeeld autorisatie-header.

```xml
<set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />
```

### <a name="making-hello-validation-request"></a>Hallo-validatieaanvraag maken
Wanneer we Hallo verificatietoken hebt, maken we Hallo aanvraag toovalidate Hallo-token. RFC 7662 roept deze introspection proces en vereist dat u `POST` een HTML-formulier toohello introspection resource. Hallo HTML-formulier moet ten minste een sleutel-waardepaar bevatten met Hallo sleutel `token`. Deze aanvraag toohello autorisatie-server moet ook geverifieerde tooensure die schadelijke clients kunnen niet voor geldige-tokens sleepnetten gaat.

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

### <a name="checking-hello-response"></a>Antwoord Hallo controleren
Hallo `response-variable-name` kenmerk is gebruikte toogive toegang Hallo antwoord geretourneerd. Hallo naam zijn gedefinieerd in deze eigenschap kan worden gebruikt als een sleutel in Hallo `context.Variables` woordenlijst tooaccess hello `IResponse` object.

Uit het Hallo-antwoordobject Hallo hoofdtekst kan worden opgehaald en RFC 7622 vertellen Hallo antwoord moet een JSON-object zijn, en moet ten minste een eigenschap met de naam bevatten `active` dat een Booleaanse waarde. Wanneer `active` is ingesteld op true en vervolgens het Hallo-token als geldig wordt aangemerkt.

### <a name="reporting-failure"></a>Reporting is mislukt
We gebruiken een `<choose>` beleid toodetect als Hallo-token is ongeldig en als dat het geval is, retourneert een 401-respons.

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

Als per [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3) waarin wordt beschreven hoe `bearer` tokens moeten worden gebruikt, wordt ook geretourneerd een `WWW-Authenticate` header met Hallo 401-respons. Hallo WWW-verificatie is bedoeld tooinstruct een client op het tooconstruct een goed ongeautoriseerde aanvraag. Vervaldatum toohello breed scala aan benaderingen mogelijk met Hallo OAuth2-framework, is het moeilijk toocommunicate alle Hallo informatie nodig hebt. Gelukkig zijn inspanningen Bezig toohelp [clients ontdekken hoe tooproperly aanvragen tooa bronserver autoriseren](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).

### <a name="final-solution"></a>Definitieve oplossing
Het samenstellen van alle Hallo stukken, krijgen we Hallo volgende beleid:

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

Dit is slechts een aantal voorbeelden van hoe Hallo `send-request` beleid gebruikte toointegrate nuttig externe services samen Hallo-proces voor aanvragen en antwoorden tot Hallo API Management-service kan worden.

## <a name="response-composition"></a>Antwoord samenstelling
Hallo `send-request` beleid kan worden gebruikt voor het verbeteren van een primaire aanvraag tooa back-end-systeem als hebt gezien in het vorige voorbeeld Hallo of het kan worden gebruikt als een volledige vervangen voor van Hallo back-end-aanroep. Met deze techniek kunnen we gemakkelijk maken samengestelde bronnen die worden samengevoegd uit meerdere verschillende systemen.

### <a name="building-a-dashboard"></a>Een dashboard maken
Soms wilt u toobe kunnen tooexpose informatie die in meerdere back endsystemen voorkomt bijvoorbeeld toodrive een dashboard. Hallo KPI's afkomstig zijn van alle verschillende back-ends, maar u liever niet tooprovide directe toegang toothem en het normaal zou zijn nice als alle Hallo-gegevens in één aanvraag kunnen worden opgehaald. Sommige Hallo back-end gegevens moet mogelijk bepaalde segmenteren en opdelen en eerst een beetje opschonen! Kan toocache samengestelde bron is een nuttig tooreduce wordt Hallo back-end laden als u weet dat gebruikers hebben een gewoonte van Hallo F5-toets in volgorde toosee hammering als hun underperforming metrische gegevens kan worden gewijzigd.    

### <a name="faking-hello-resource"></a>Hallo resource faking
eerste stap toobuilding Hallo onze dashboard-bron is een nieuwe bewerking in de publicatieportal van API Management Hallo tooconfigure. Dit is een tijdelijke aanduiding voor bewerking gebruikt tooconfigure onze samenstelling beleid toobuild onze dynamische bron.

![Dashboard-bewerking](./media/api-management-sample-send-request/api-management-dashboard-operation.png)

### <a name="making-hello-requests"></a>Hallo-aanvragen
Eenmaal Hallo `dashboard` bewerking is gemaakt kunnen we een beleid specifiek voor die bewerking configureren. 

![Dashboard-bewerking](./media/api-management-sample-send-request/api-management-dashboard-policy.png)

de eerste stap Hallo tooextract is queryparameters van Hallo inkomende aanvraag, zodat we ze tooour back-end kan doorsturen. In dit voorbeeld onze dashboard op basis van een bepaalde periode informatie wordt weergegeven een daarom heeft een `fromDate` en `toDate` parameter. We kunnen hello gebruiken `set-variable` tooextract Hallo beleidsgegevens van Hallo aanvraag-URL.

```xml
<set-variable name="fromDate" value="@(context.Request.Url.Query["fromDate"].Last())">
<set-variable name="toDate" value="@(context.Request.Url.Query["toDate"].Last())">
```

Zodra deze informatie kunnen we aanvragen tooall Hallo back-end-systemen. Elke aanvraag vormt een nieuwe URL met informatie voor de parameter Hallo en roept de desbetreffende server en antwoord Hallo opslaat in een context-variabele.

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

Deze aanvragen worden uitgevoerd in de juiste volgorde niet ideaal is. In een toekomstige release we een nieuw beleid aangeroepen introducing `wait` waarmee al deze aanvragen tooexecute parallel.

### <a name="responding"></a>Reageert
tooconstruct samengestelde antwoord Hallo gebruiken we Hallo [return antwoord](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) beleid. Hallo `set-body` element kunt een expressie tooconstruct een nieuwe `JObject` met alle Hallo onderdeel verklaringen ingesloten als eigenschappen.

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

Hallo voltooid beleid ziet er als volgt uit:

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

In de configuratie van Hallo tijdelijke aanduiding voor bewerking die kunnen we configureren Hallo Hallo dashboard resource toobe in cache opgeslagen voor ten minste een uur omdat we Hallo aard van Hallo gegevens houdt in dat zelfs als deze een verouderd begrijpen, dat nog steeds moeten voldoende effectieve uur tooconvey waardevolle informatie toohello gebruikers.

## <a name="summary"></a>Samenvatting
Azure API Management-service biedt flexibele beleidsregels die selectief kunnen worden toegepast tooHTTP verkeer en Hiermee samenstelling van back-end-services. Of u wilt dat tooenhance uw API-gateway met waarschuwingen, functies, verificatie, validatie mogelijkheden of maken van nieuwe samengestelde resources op basis van meerdere back-end-services, Hallo `send-request` en bijbehorende beleid opent u een wereld van mogelijkheden.

## <a name="watch-a-video-overview-of-these-policies"></a>Bekijk een video-overzicht van deze beleidsregels
Voor meer informatie over Hallo [-één-manier-Verzendaanvraag](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [aanvragen verzenden](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest), en [return antwoord](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) beleidsregels die in dit artikel, neem Hallo volgende video bekijken.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Send-Request-and-Return-Response-Policies/player]
> 
> 

