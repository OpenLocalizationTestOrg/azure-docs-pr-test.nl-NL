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
# <a name="custom-caching-in-azure-api-management"></a>Aangepaste opslaan in cache in Azure API Management
Azure API Management-service biedt ingebouwde ondersteuning voor [HTTP-antwoord in cache opslaan](api-management-howto-cache.md) Hallo bron-URL als Hallo sleutel gebruiken. Hallo sleutel kan worden gewijzigd door aanvraagheaders Hallo met `vary-by` eigenschappen. Dit is handig voor het opslaan van de hele HTTP-antwoorden (aka verklaringen), maar soms is het nuttig toojust cache een deel van een weergave. Hallo nieuwe [cache zoekwaarde](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) en [cache-store-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) -beleid biedt de mogelijkheid Hallo willekeurige stukken toostore en ophalen van gegevens vanuit beleidsdefinities. Deze mogelijkheid voegt ook waarde toohello eerder geïntroduceerd [aanvragen verzenden](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) beleid omdat u kunt nu antwoorden van externe services cache.

## <a name="architecture"></a>Architectuur
API Management-service wordt gebruikgemaakt van een gedeelde tenant gegevenscache zodat terwijl u toomultiple eenheden schaalt worden er nog steeds toegang toohello dezelfde gegevens uit de cache. Als u werkt met een implementatie met meerdere regio zijn er echter onafhankelijke caches in elk Hallo regio's. Vervaldatum toothis, is het belangrijk toonot Hallo cache behandelen als een gegevensarchief, waar is de enige bron Hallo van sommige stukje informatie. Als u hebt en later tootake profiteren van de implementatie van Hallo meerdere landen/regio besloten, kunnen toegang toothat in de cache opgeslagen gegevens verliezen door klanten met gebruikers die worden uitgewisseld.

## <a name="fragment-caching"></a>Fragment opslaan in cache
Er zijn bepaalde gevallen waarbij antwoorden wordt geretourneerd een gedeelte van de gegevens die dure toodetermine is en nog blijft vers voor een redelijk tijdsbestek bevatten. Een voorbeeld kunt u een service die is gebouwd door een luchtvaartmaatschappij die voorziet in informatie over Vluchtreserveringen, vlucht status, enzovoort. Als het Hallo-gebruiker is lid van Hallo airlines punten programma, zou moeten ook informatie over de huidige status van tootheir en kilometers verzameld. Deze gebruiker-gerelateerde gegevens worden opgeslagen in een ander systeem, maar deze is mogelijk wenselijk tooinclude in antwoorden over de status van de vlucht en -reserveringen geretourneerd. U kunt dit doen via een proces genaamd fragment opslaan in cache. Hallo kan primaire weergave worden geretourneerd van de bronserver Hallo met een soort token tooindicate waarbij Hallo gebruiker-gerelateerde informatie toobe ingevoegd. 

Overweeg het volgende JSON-antwoord van een back-end API Hallo.

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

En secundaire bron ingesteld op `/userprofile/{userid}` die vergelijkbaar is,

```json
{ "username" : "Bob Smith", "Status" : "Gold" }
```

In de volgorde toodetermine Hallo betreffende informatie tooinclude moeten we tooidentify die de eindgebruiker Hallo is. Dit mechanisme is afhankelijke-implementatie. Als u bijvoorbeeld ik Hallo gebruik `Subject` claimen van een `JWT` token. 

```xml
<set-variable
  name="enduserid"
  value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />
```

Zo bewaren wij dit `enduserid` waarde in een variabele context voor later gebruik. de volgende stap Hallo is toodetermine als een eerdere aanvraag al Hallo gebruikersgegevens opgehaald en opgeslagen in cache Hallo. Voor deze gebruiken we Hallo `cache-lookup-value` beleid.

```xml
<cache-lookup-value
key="@("userprofile-" + context.Variables["enduserid"])"
variable-name="userprofile" />
```

Als er is geen vermelding in de cache Hallo die overeenkomt met de sleutelwaarde toohello en klik op Nee `userprofile` context variabele wordt gemaakt. We controleren of Hallo geslaagd van Hallo zoeken met behulp van Hallo `choose` beleid overdrachten beheren.

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("userprofile"))">
        <!-- If hello userprofile context variable doesn’t exist, make an HTTP request tooretrieve it.  -->
    </when>
</choose>
```

Als hello `userprofile` context variabele bestaat niet en gaat toohave toomake een HTTP-aanvraag tooretrieve worden deze.

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

We gebruiken Hallo `enduserid` tooconstruct Hallo URL toohello gebruiker profiel resource. Zodra er antwoord Hallo hebt, kunnen we pull-hallo platte tekst buiten het antwoord Hallo en sla deze terug in een context-variabele.

```xml
<set-variable
    name="userprofile"
    value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />
```

tooavoid ons met toomake deze HTTP-aanvraag opnieuw wanneer hello dezelfde gebruiker een andere aanvraag indient, we kunt opslaan Hallo gebruikersprofiel in cache Hallo.

```xml
<cache-store-value
    key="@("userprofile-" + context.Variables["enduserid"])"
    value="@((string)context.Variables["userprofile"])" duration="100000" />
```

Hallo waarde opgeslagen in het Hallo-cache met behulp van Hallo exact dezelfde sleutel dat we tooretrieve oorspronkelijk heeft geprobeerd deze met. Hallo moet duur die we toostore Hallo waarde kiezen zijn gebaseerd op hoe vaak hello informatie wijzigingen en over hoe fouttolerante gebruikers tooout van actuele informatie worden. 

Het is belangrijk toorealize dat ophalen uit de cache Hallo nog steeds een out-of-process, een aanvraag voor het netwerk en mogelijk kan nog wel toevoegen tientallen van milliseconden toohello aanvraag. Hallo voordelen wanneer bepalende Hallo gebruikersprofielgegevens aanzienlijk langer dan die vervaldatum tooneeding toodo databasequery's of statistische gegevens uit meerdere back-ends duurt worden geleverd.

Hallo is laatste stap bij het Hallo-proces tooupdate Hallo antwoord met onze gebruikersprofielgegevens geretourneerd.

```xml
<!-- Update response body with user profile-->
<find-and-replace
    from='"$userprofile$"'
    to="@((string)context.Variables["userprofile"])" />
```

Ik heb gekozen tooinclude Hallo tussen aanhalingstekens als onderdeel van Hallo token zodat zelfs wanneer Hallo vervangen niet wordt uitgevoerd, Hallo antwoord nog geldig JSON is. Dit is vooral toomake foutopsporing gemakkelijker.

Als u al deze stappen samen combineren, is het eindresultaat Hallo een beleid dat lijkt op Hallo na een.

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

Deze cache benadering wordt voornamelijk gebruikt in websites waar HTML bestaat aan serverzijde Hallo zodat deze kan worden gerenderd als één pagina. Maar dit kan ook nuttig zijn in API's waar clients client kunnen niet aan de objectkant HTTP opslaan in cache of het wenselijk is niet tooput verantwoordelijkheid op Hallo-client.

Dit dezelfde soort fragment opslaan in cache kan ook worden uitgevoerd op Hallo back-end-webservers met behulp van een in Redis cache van de server, echter met behulp van Hallo API Management-service tooperform dit werk is nuttig wanneer in de cache opgeslagen Hallo fragmenten afkomstig zijn uit verschillende back-ends dan Hallo primaire antwoorden.

## <a name="transparent-versioning"></a>Transparante versiebeheer
Het is gebruikelijk om voor meerdere versies van de andere implementatie van een API-toobe op elk gewenst moment ondersteund. Dit is mogelijk toosupport verschillende omgevingen, zoals ontwikkelen, testen, productie, enzovoort, of wordt mogelijk toosupport oudere versies van Hallo API toogive tijd voor de API consumenten toomigrate toonewer-versies. 

Een aanpak toohandling dit in plaats daarvan van client ontwikkelaars toochange Hallo URL's van vereisen `/v1/customers` te`/v2/customers` is toostore in van de consumer Hallo profielgegevens welke versie van Hallo API ze momenteel wilt toouse en Hallo juiste aanroepen back-end-URL. In de volgorde toodetermine Hallo juiste back-end URL toocall voor een bepaalde client, is het nodig tooquery Sommige configuratiegegevens. Door deze configuratiegegevens caching, kunnen we Hallo op de prestaties van de handeling deze zoekactie minimaliseren.

de eerste stap Hallo is toodetermine Hallo id tooconfigure Hallo gewenste versie gebruikt. In dit voorbeeld gekozen ik tooassociate Hallo versie toohello abonnement-productcode. 

```xml
<set-variable name="clientid" value="@(context.Subscription.Key)" />
```

We doen een cache lookup toosee vervolgens als we de gewenste clientversie Hallo al hebt opgehaald.

```xml
<cache-lookup-value
key="@("clientversion-" + context.Variables["clientid"])"
variable-name="clientversion" />
```

Vervolgens controleren we toosee als we het niet in cache Hallo vinden is.

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("clientversion"))">
```

Als we niet we gaan en dit ophalen.

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

Hallo antwoord platte tekst uit het antwoord Hallo extraheren.

```xml
<set-variable
      name="clientversion"
      value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
```

Opslaan in cache Hallo voor toekomstig gebruik.

```xml
<cache-store-value
      key="@("clientversion-" + context.Variables["clientid"])"
      value="@((string)context.Variables["clientversion"])"
      duration="100000" />
```

En ten slotte Hallo back-end URL tooselect Hallo versie van Hallo service gewenst door Hallo client bijwerken.

```xml
<set-backend-service
      base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
```

Hallo is volledig beleid als volgt.

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

Inschakelen van welke endversie van de back-om wordt geopend door clients zonder tooupdate en de implementatie opnieuw clients van consumenten tootransparently-beheer op API is een elegante oplossing die zijn gericht op veel API versioning problemen.

## <a name="tenant-isolation"></a>Isolatie van tenants
Sommige bedrijven Maak in grotere implementaties met meerdere tenants afzonderlijke groepen van tenants voor verschillende implementaties van back-end-hardware. Dit minimaliseert aantal klanten die worden beïnvloed door een hardwareprobleem op Hallo backend Hallo. Ook kunt nieuwe software versies toobe uitgerold in fasen uitgevoerd. Deze back-end-architectuur moet in het ideale geval transparante tooAPI consumenten. Dit kan worden bereikt in een vergelijkbare manier tootransparent versioning omdat deze is gebaseerd op Hallo dezelfde techniek van het manipuleren van Hallo back-end-URL met behulp van de status van de configuratie per API-sleutel.  

In plaats van een aanbevolen versie van Hallo API voor elke abonnementssleutel wordt geretourneerd, zou u een id die is gekoppeld van een tenant toohello toegewezen Hardwaregroep retourneren. Deze id kan worden gebruikt tooconstruct Hallo juiste back-end-URL.

## <a name="summary"></a>Samenvatting
Hallo vrijheid toouse hello Azure API management-cache voor het opslaan van elk soort gegevens kan efficiënte toegang tooconfiguration gegevens die kunnen invloed hebben op Hallo manier die een binnenkomende aanvraag is verwerkt. Het kan ook worden de gebruikte toostore gegevens fragmenten die reacties, geretourneerd vanuit een back-end API kunnen verbeteren.

## <a name="next-steps"></a>Volgende stappen
Geef ons uw feedback in Hallo Disqus-thread voor dit onderwerp als er andere scenario's dat deze beleidsregels hebt ingeschakeld voor u, of als er scenario's u wilt tooachieve, maar kan niet van mening bent dat momenteel mogelijk zijn.

