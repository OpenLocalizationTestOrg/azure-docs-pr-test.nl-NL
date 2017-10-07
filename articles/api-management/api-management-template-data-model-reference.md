---
title: aaaAzure API Management-sjabloon gegevensmodel verwijzing | Microsoft Docs
description: Meer informatie over de entiteit en type verklaringen Hallo voor algemene items in de gegevensmodellen Hallo gebruikt voor het Hallo developer portal sjablonen in Azure API Management.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: b0ad7e15-9519-4517-bb73-32e593ed6380
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 7d049d8ecc9e597cf48ce0c820c172798bcf86de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-template-data-model-reference"></a>Azure API Management data model verwijzing naar de sjabloon
Dit onderwerp beschrijft de entiteit en type verklaringen Hallo voor algemene items in de gegevensmodellen Hallo gebruikt voor het Hallo developer portal sjablonen in Azure API Management.  
  
 Zie voor meer informatie over het werken met sjablonen [hoe toocustomize API Management-portal voor ontwikkelaars met behulp van sjablonen Hallo](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).  
  
-   [API](#API)  
-   [API-overzicht](#APISummary)  
-   [Toepassing](#Application)  
-   [Bijlage](#Attachment)  
-   [Voorbeeld van code](#Sample)  
-   [Opmerking](#Comment)  
-   [Filteren](#Filtering)  
-   [Koptekst](#Header)  
-   [HTTP-aanvraag](#HTTPRequest)  
-   [HTTP-antwoord](#HTTPResponse)  
-   [Probleem](#Issue)  
-   [Bewerking](#Operation)  
-   [Bewerking menu](#Menu)  
-   [Bewerking menu-item](#MenuItem)  
-   [Paginering](#Paging)  
-   [Parameter](#Parameter)  
-   [Product](#Product)  
-   [Provider](#Provider)  
-   [Weergave](#Representation)  
-   [Abonnement](#Subscription)  
-   [Samenvatting van abonnement](#SubscriptionSummary)  
-   [Gebruikersaccountgegevens](#UserAccountInfo)  
-   [Gebruiker aanmelden](#UseSignIn)  
-   [Meld u aan gebruiker](#UserSignUp)  
  
##  <a name="API"></a>API  
 Hallo `API` entiteit Hallo volgende eigenschappen heeft.  
  
|Eigenschap|Type|Beschrijving|  
|--------------|----------|-----------------|  
|id|Tekenreeks|Bron-id. Een unieke identificatie Hallo API binnen het huidige exemplaar van API Management-service Hallo. Hallo-waarde is een geldig relatieve URL in de indeling van Hallo `apis/{id}` waar `{id}` is een API-id. Deze eigenschap is alleen-lezen.|  
|naam|Tekenreeks|Naam van Hallo API. Mag niet leeg zijn. Maximale lengte is 100 tekens.|  
|description|Tekenreeks|Beschrijving van Hallo API. Mag niet leeg zijn. Kan HTML-opmaak labels bevatten. Maximumlengte is 1000 tekens.|  
|serviceUrl|Tekenreeks|Absolute URL van back-endservice Hallo uitvoering van deze API.|  
|Pad|Tekenreeks|Relatieve URL is een unieke id van deze API en alle bijbehorende paden resource binnen Hallo API Management service-exemplaar. Het wordt toegevoegd toohello API-eindpunt basis-URL opgegeven tijdens het Hallo-service-exemplaar maken van tooform een openbare URL voor deze API.|  
|Protocollen|matrix van getal|Hierin wordt beschreven op welke protocollen Hallo bewerkingen in deze API kunnen worden aangeroepen. Toegestane waarden zijn `1 - http` en `2 - https`, of beide.|  
|authenticationSettings|[Autorisatie-instellingen voor server-verificatie](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#AuthenticationSettings)|Verzameling van verificatie-instellingen die zijn opgenomen in deze API.|  
|subscriptionKeyParameterNames|object|Optionele eigenschap die kan worden gebruikt toospecify aangepaste namen voor query-en/of koptekst parameters die Hallo abonnementssleutel bevat. Als deze eigenschap aanwezig is moet er ten minste één van de twee volgende eigenschappen Hallo bevatten.<br /><br /> `{   "subscriptionKeyParameterNames":   {     "query": “customQueryParameterName",     "header": “customHeaderParameterName"   } }`|  
  
##  <a name="APISummary"></a>API-overzicht  
 Hallo `API summary` entiteit Hallo volgende eigenschappen heeft.  
  
|Eigenschap|Type|Beschrijving|  
|--------------|----------|-----------------|  
|id|Tekenreeks|Bron-id. Een unieke identificatie Hallo API binnen het huidige exemplaar van API Management-service Hallo. Hallo-waarde is een geldig relatieve URL in de indeling van Hallo `apis/{id}` waar `{id}` is een API-id. Deze eigenschap is alleen-lezen.|  
|naam|Tekenreeks|Naam van Hallo API. Mag niet leeg zijn. Maximale lengte is 100 tekens.|  
|description|Tekenreeks|Beschrijving van Hallo API. Mag niet leeg zijn. Kan HTML-opmaak labels bevatten. Maximumlengte is 1000 tekens.|  
  
##  <a name="Application"></a>Toepassing  
 Hallo `application` entiteit Hallo volgende eigenschappen heeft.  
  
|Eigenschap|Type|Beschrijving|  
|--------------|----------|-----------------|  
|Id|Tekenreeks|de unieke id van de toepassing hello Hallo.|  
|Titel|Tekenreeks|Hallo titel van toepassing hello.|  
|Beschrijving|Tekenreeks|Hallo beschrijving van de toepassing hello.|  
|URL|URI|Hallo URI voor de toepassing hello.|  
|Versie|Tekenreeks|Versie-informatie voor de toepassing hello.|  
|Vereisten|Tekenreeks|Een beschrijving van de vereisten voor de toepassing hello.|  
|Status|Aantal|Hallo huidige status van de toepassing hello.<br /><br /> -0 - geregistreerd<br /><br /> -1 - verzonden<br /><br /> -2 - gepubliceerd<br /><br /> -3 - geweigerd<br /><br /> -4 - niet gepubliceerd|  
|RegistrationDate|Datum/tijd|Hallo datum en tijd Hallo toepassing is geregistreerd.|  
|Categorie-id|Aantal|Hallo categorie van het Hallo-toepassing (financiën, entertainment, enz.)|  
|DeveloperId|Tekenreeks|Hallo unieke id van Hallo-ontwikkelaar die toepassing hello verzonden.|  
|Bijlagen|Verzameling van [bijlage](#Attachment) entiteiten.|Eventuele bijlagen voor de toepassing hello zoals schermafbeeldingen of pictogrammen.|  
|Pictogram|[Bijlage](#Attachment)|Hallo pictogram Hallo voor Hallo-toepassing.|  
  
##  <a name="Attachment"></a>Bijlage  
 Hallo `attachment` entiteit Hallo volgende eigenschappen heeft.  
  
|Eigenschap|Type|Beschrijving|  
|--------------|----------|-----------------|  
|Unieke id|Tekenreeks|de unieke id voor de bijlage Hallo Hallo.|  
|URL|Tekenreeks|Hallo-URL van Hallo resource.|  
|Type|Tekenreeks|Hallo-type van de bijlage.|  
|ContentType|Tekenreeks|mediatype Hallo van Hallo bijlage.|  
  
##  <a name="Sample"></a>Voorbeeld van code  
  
|Eigenschap|Type|Beschrijving|  
|--------------|----------|-----------------|  
|titel|Tekenreeks|Hallo-naam van Hallo-bewerking.|  
|codefragment|Tekenreeks|Deze eigenschap is afgeschaft en mag niet worden gebruikt.|  
|kwast|Tekenreeks|Die code syntaxis kleuren sjabloon toobe gebruikt bij het Hallo-codevoorbeeld weergeven. Toegestane waarden zijn `plain`, `php`, `java`, `xml`, `objc`, `python`, `ruby`, en `csharp`.|  
|sjabloon|Tekenreeks|Hallo-naam van deze voorbeeldsjabloon code.|  
|Hoofdtekst|Tekenreeks|Een tijdelijke aanduiding Hallo code voorbeeld deel van het Hallo-codefragment.|  
|Methode|Tekenreeks|Hallo HTTP-methode van Hallo-bewerking.|  
|Schema|Tekenreeks|Hallo protocol toouse voor Hallo bewerkingsaanvraag.|  
|Pad|Tekenreeks|Hallo-pad van Hallo-bewerking.|  
|query|Tekenreeks|Voorbeeld van de query-tekenreeks met gedefinieerde parameters.|  
|host|Tekenreeks|Hallo-URL van Hallo API Management-service gateway voor Hallo API met deze bewerking.|  
|Headers|Verzameling van [Header](#Header) entiteiten.|Headers voor deze bewerking.|  
|parameters|Verzameling van [Parameter](#Parameter) entiteiten.|De parameters die zijn gedefinieerd voor deze bewerking.|  
  
##  <a name="Comment"></a>Opmerking  
 Hallo `API` entiteit Hallo volgende eigenschappen heeft.  
  
|Eigenschap|Type|Beschrijving|  
|--------------|----------|-----------------|  
|Id|Aantal|Hallo-id van Hallo opmerking.|  
|CommentText|Tekenreeks|Hallo-hoofdtekst van Hallo opmerking. Kan HTML bevatten.|  
|DeveloperCompany|Tekenreeks|Bedrijfsnaam Hallo van Hallo-ontwikkelaar.|  
|PostedOn|Datum/tijd|Hallo datum en tijd Hallo opmerking is geplaatst.|  
  
##  <a name="Issue"></a>Probleem  
 Hallo `issue` entiteit Hallo volgende eigenschappen heeft.  
  
|Eigenschap|Type|Beschrijving|  
|--------------|----------|-----------------|  
|Id|Tekenreeks|Hallo unieke id voor Hallo probleem.|  
|ApiID|Tekenreeks|Hallo-id voor Hallo API waarvoor dit probleem is gerapporteerd.|  
|Titel|Tekenreeks|Titel van het Hallo-probleem.|  
|Beschrijving|Tekenreeks|Beschrijving van Hallo probleem.|  
|SubscriptionDeveloperName|Tekenreeks|De voornaam van Hallo-ontwikkelaar die Hallo probleem gerapporteerd.|  
|IssueState|Tekenreeks|Hallo huidige status van probleem Hallo. Mogelijke waarden zijn voorgesteld, Opened, gesloten.|  
|ReportedOn|Datum/tijd|Hallo datum en tijd Hallo probleem is opgetreden.|  
|Opmerkingen|Verzameling van [Opmerking](#Comment) entiteiten.|Opmerkingen over dit probleem.|  
|Bijlagen|Verzameling van [bijlage](api-management-template-data-model-reference.md#Attachment) entiteiten.|Eventuele bijlagen toohello problemen.|  
|Services|Verzameling van [API](#API) entiteiten.|Hallo API's geabonneerd tooby Hallo gebruiker dat Hallo probleem gearchiveerd.|  
  
##  <a name="Filtering"></a>Filteren  
 Hallo `filtering` entiteit Hallo volgende eigenschappen heeft.  
  
|Eigenschap|Type|Beschrijving|  
|--------------|----------|-----------------|  
|patroon|Tekenreeks|het huidige zoekterm Hallo; of `null` als er geen zoekterm.|  
|Tijdelijke aanduiding voor|Tekenreeks|Hallo toodisplay tekst in het zoekvak Hallo wanneer er geen zoekterm opgegeven.|  
  
##  <a name="Header"></a>Koptekst  
 Deze sectie beschrijft Hallo `parameter` weergave.  
  
|Eigenschap|Beschrijving|Type|  
|--------------|-----------------|----------|  
|naam|Tekenreeks|Parameternaam.|  
|description|Tekenreeks|Beschrijving van de parameter.|  
|waarde|Tekenreeks|Headerwaarde.|  
|TypeName|Tekenreeks|Het gegevenstype van headerwaarde.|  
|Opties|Tekenreeks|Opties.|  
|Vereist|Booleaanse waarde|Hiermee wordt aangegeven of Hallo-header is vereist.|  
|Alleen-lezen|Booleaanse waarde|Hallo-header is of alleen-lezen.|  
  
##  <a name="HTTPRequest"></a>HTTP-aanvraag  
 Deze sectie beschrijft Hallo `request` weergave.  
  
|Eigenschap|Type|Beschrijving|  
|--------------|----------|-----------------|  
|description|Tekenreeks|Beschrijving van de aanvraag opnieuw.|  
|Headers|matrix van [Header](#Header) entiteiten.|Aanvraagheaders.|  
|parameters|matrix van [Parameter](#Parameter)|Verzameling parameters van de aanvraag opnieuw.|  
|verklaringen|matrix van [weergave](#Representation)|Verzameling van bewerking aanvraag verklaringen.|  
  
##  <a name="HTTPResponse"></a>HTTP-antwoord  
 Deze sectie beschrijft Hallo `response` weergave.  
  
|Eigenschap|Type|Beschrijving|  
|--------------|----------|-----------------|  
|statusCode|Positief geheel getal|Code voor antwoordstatus bewerking.|  
|description|Tekenreeks|Beschrijving van de reactie bewerking.|  
|verklaringen|matrix van [weergave](#Representation)|Verzameling van bewerking antwoord verklaringen.|  
  
##  <a name="Operation"></a>Bewerking  
 Hallo `operation` entiteit Hallo volgende eigenschappen heeft.  
  
|Eigenschap|Type|Beschrijving|  
|--------------|----------|-----------------|  
|id|Tekenreeks|Bron-id. Een unieke identificatie Hallo bewerking binnen het huidige exemplaar van API Management-service Hallo. Hallo-waarde is een geldig relatieve URL in de indeling van Hallo `apis/{aid}/operations/{id}` waar `{aid}` is een API-id en `{id}` is een bewerking-id. Deze eigenschap is alleen-lezen.|  
|naam|Tekenreeks|Naam van Hallo-bewerking. Mag niet leeg zijn. Maximale lengte is 100 tekens.|  
|description|Tekenreeks|Beschrijving van het Hallo-bewerking. Mag niet leeg zijn. Kan HTML-opmaak labels bevatten. Maximumlengte is 1000 tekens.|  
|Schema|Tekenreeks|Hierin wordt beschreven op welke protocollen Hallo bewerkingen in deze API kunnen worden aangeroepen. Toegestane waarden zijn `http`, `https`, of beide `http` en `https`.|  
|uriTemplate|Tekenreeks|Relatieve URL sjabloon Hallo doelbron voor deze bewerking te identificeren. Kan parameters bevatten. Voorbeeld:`customers/{cid}/orders/{oid}/?date={date}`|  
|host|Tekenreeks|Hallo API Management gateway-URL die als host fungeert voor Hallo-API.|  
|HttpMethod|Tekenreeks|HTTP-bewerkingsmethode.|  
|Aanvraag|[HTTP-aanvraag](#HTTPRequest)|Een entiteit die gegevens voor de aanvraag bevat.|  
|antwoorden|matrix van [HTTP-antwoord](#HTTPResponse)|Matrix van bewerking [HTTP-antwoord](#HTTPResponse) entiteiten.|  
  
##  <a name="Menu"></a>Bewerking menu  
 Hallo `operation menu` entiteit Hallo volgende eigenschappen heeft.  
  
|Eigenschap|Type|Beschrijving|  
|--------------|----------|-----------------|  
|apiId|Tekenreeks|Hallo-id van de huidige API Hallo.|  
|CurrentOperationId|Tekenreeks|Hallo-id van de huidige bewerking Hallo.|  
|Actie|Tekenreeks|Hallo Menutype.|  
|MenuItems|Verzameling van [bewerking menuopdracht](#MenuItem) entiteiten.|Hallo-bewerkingen voor de huidige API Hallo.|  
  
##  <a name="MenuItem"></a>Bewerking menu-item  
 Hallo `operation menu item` entiteit Hallo volgende eigenschappen heeft.  
  
|Eigenschap|Type|Beschrijving|  
|--------------|----------|-----------------|  
|Id|Tekenreeks|Hallo-id van Hallo-bewerking.|  
|Titel|Tekenreeks|Hallo-omschrijving van Hallo-bewerking.|  
|HttpMethod|Tekenreeks|Hallo HTTP-methode van Hallo-bewerking.|  
  
##  <a name="Paging"></a>Paginering  
 Hallo `paging` entiteit Hallo volgende eigenschappen heeft.  
  
|Eigenschap|Type|Beschrijving|  
|--------------|----------|-----------------|  
|Pagina|Aantal|het huidige paginanummer Hallo.|  
|PageSize|Aantal|Hallo maximum aantal resultaten toobe op één pagina weergegeven.|  
|TotalItemCount|Aantal|Hallo aantal items om weer te geven.|  
|ShowAll|Booleaanse waarde|Hiermee wordt aangegeven of toosho alle resultaten worden op één pagina.|  
|PageCount|Aantal|Hallo aantal pagina's van de resultaten.|  
  
##  <a name="Parameter"></a>Parameter  
 Deze sectie beschrijft Hallo `parameter` weergave.  
  
|Eigenschap|Beschrijving|Type|  
|--------------|-----------------|----------|  
|naam|Tekenreeks|Parameternaam.|  
|description|Tekenreeks|Beschrijving van de parameter.|  
|waarde|Tekenreeks|Waarde voor parameter.|  
|Opties|Matrix van tekenreeks|Waarden die zijn gedefinieerd voor parameterwaarden.|  
|Vereist|Booleaanse waarde|Hiermee geeft u op of de parameter vereist is.|  
|type|Aantal|Hiermee wordt aangegeven of deze parameter is een padparameter (1) of een parameter querystring (2).|  
|TypeName|Tekenreeks|Het parametertype.|  
  
##  <a name="Product"></a>Product  
 Hallo `product` entiteit Hallo volgende eigenschappen heeft.  
  
|Eigenschap|Type|Beschrijving|  
|--------------|----------|-----------------|  
|Id|Tekenreeks|Bron-id. Een unieke identificatie Hallo product binnen het huidige exemplaar van API Management-service Hallo. Hallo-waarde is een geldig relatieve URL in de indeling van Hallo `products/{pid}` waar `{pid}` is een product-id. Deze eigenschap is alleen-lezen.|  
|Titel|Tekenreeks|Naam van Hallo product. Mag niet leeg zijn. Maximale lengte is 100 tekens.|  
|Beschrijving|Tekenreeks|Beschrijving van Hallo product. Mag niet leeg zijn. Kan HTML-opmaak labels bevatten. Maximumlengte is 1000 tekens.|  
|Voorwaarden|Tekenreeks|Product gebruiksvoorwaarden. Ontwikkelaars probeert toosubscribe toohello product krijgt en tooaccept nodig deze voorwaarden voordat ze Hallo abonnement proces kunnen voltooien.|  
|ProductState|Aantal|Hiermee geeft u op of Hallo product is gepubliceerd of niet. Gepubliceerde producten kunnen worden gevonden door ontwikkelaars op Hallo-portal voor ontwikkelaars. Niet-gepubliceerde producten zijn zichtbaar alleen tooadministrators.<br /><br /> toegestane waarden voor Productstatus Hallo zijn:<br /><br /> - `0 - Not Published`<br /><br /> - `1 - Published`<br /><br /> - `2 - Deleted`|  
|AllowMultipleSubscriptions|Booleaanse waarde|Hiermee geeft u op of een gebruiker meerdere abonnementen toothis product op Hallo hebben kan hetzelfde moment.|  
|MultipleSubscriptionsCount|Aantal|Hallo aantal abonnementen toothis product door de huidige gebruiker Hallo.|  
  
##  <a name="Provider"></a>Provider  
 Hallo `provider` entiteit Hallo volgende eigenschappen heeft.  
  
|Eigenschap|Type|Beschrijving|  
|--------------|----------|-----------------|  
|Eigenschappen|tekenreeks woordenlijst|Eigenschappen voor deze verificatieprovider.|  
|authenticationType|Tekenreeks|Hallo-providertype. (Azure Active Directory, Facebook-aanmelding, Google-Account, Microsoft-Account, Twitter).|  
|Bijschrift|Tekenreeks|Weergavenaam van het Hallo-provider.|  
  
##  <a name="Representation"></a>Weergave  
 Deze sectie beschrijft een `representation`.  
  
|Eigenschap|Type|Beschrijving|  
|--------------|----------|-----------------|  
|ContentType|Tekenreeks|Hiermee geeft u een geregistreerde of aangepaste inhoudstype voor deze weergave bijvoorbeeld `application/xml`.|  
|voorbeeld|Tekenreeks|Een voorbeeld van Hallo weergave.|  
  
##  <a name="Subscription"></a>Abonnement  
 Hallo `subscription` entiteit Hallo volgende eigenschappen heeft.  
  
|Eigenschap|Type|Beschrijving|  
|--------------|----------|-----------------|  
|Id|Tekenreeks|Bron-id. Een unieke identificatie Hallo abonnement binnen het huidige exemplaar van API Management-service Hallo. Hallo-waarde is een geldig relatieve URL in de indeling van Hallo `subscriptions/{sid}` waar `{sid}` is de abonnement-id. Deze eigenschap is alleen-lezen.|  
|product-id|Tekenreeks|Hallo product resource-id van Hallo product geabonneerd. Hallo-waarde is een geldig relatieve URL in de indeling van Hallo `products/{pid}` waar `{pid}` is een product-id.|  
|ProductTitle|Tekenreeks|Naam van Hallo product. Mag niet leeg zijn. Maximale lengte is 100 tekens.|  
|ProductDescription|Tekenreeks|Beschrijving van Hallo product. Mag niet leeg zijn. Kan HTML-opmaak labels bevatten. Maximumlengte is 1000 tekens.|  
|ProductDetailsUrl|Tekenreeks|Relatieve URL toohello-productgegevens.|  
|state|Tekenreeks|Hallo-status van het Hallo-abonnement. Mogelijke statussen zijn:<br /><br /> - `0 - suspended`– Hallo-abonnement is geblokkeerd en Hallo abonnee kan API's van Hallo product niet aanroepen.<br /><br /> - `1 - active`– Hallo abonnement actief is.<br /><br /> - `2 - expired`– Hallo-abonnement is bereikt de verloopdatum en is gedeactiveerd.<br /><br /> - `3 - submitted`– Hallo Abonnementaanvraag is gemaakt door de ontwikkelaar Hallo, maar is nog niet goedgekeurd of afgewezen.<br /><br /> - `4 - rejected`– Hallo Abonnementaanvraag is geweigerd door een beheerder.<br /><br /> - `5 - cancelled`– Hallo-abonnement is geannuleerd door Hallo ontwikkelaar of beheerder.|  
|Weergavenaam|Tekenreeks|Weergavenaam van het Hallo-abonnement.|  
|CreatedDate|Datum/tijd|Hallo datum Hallo-abonnement is gemaakt, in de ISO 8601-notatie: `2014-06-24T16:25:00Z`.|  
|CanBeCancelled|Booleaanse waarde|Hiermee wordt aangegeven of Hallo-abonnement kan worden geannuleerd door de huidige gebruiker Hallo.|  
|IsAwaitingApproval|Booleaanse waarde|Hiermee wordt aangegeven of Hallo abonnement wacht op goedkeuring.|  
|Begindatum|Datum/tijd|Hallo begindatum voor het Hallo-abonnement in de ISO 8601-notatie: `2014-06-24T16:25:00Z`.|  
|ExpirationDate|Datum/tijd|de vervaldatum Hallo voor Hallo-abonnement in de ISO 8601-notatie: `2014-06-24T16:25:00Z`.|  
|NotificationDate|Datum/tijd|datum van Hallo-bericht voor het Hallo-abonnement in de ISO 8601-notatie: `2014-06-24T16:25:00Z`.|  
|primaryKey|Tekenreeks|Hallo abonnement primaire sleutel. Maximale lengte is 256 tekens.|  
|secundaire sleutel|Tekenreeks|Hallo abonnement secundaire sleutel. Maximale lengte is 256 tekens.|  
|CanBeRenewed|Booleaanse waarde|Hiermee wordt aangegeven of Hallo abonnement kan worden vernieuwd door de huidige gebruiker Hallo.|  
|HasExpired|Booleaanse waarde|Hiermee wordt aangegeven of Hallo-abonnement is verlopen.|  
|IsRejected|Booleaanse waarde|Hiermee wordt aangegeven of Hallo Abonnementaanvraag is geweigerd.|  
|cancelUrl|Tekenreeks|Hallo relatieve Url toocancel Hallo-abonnement.|  
|RenewUrl|Tekenreeks|Hallo relatieve Url toorenew Hallo-abonnement.|  
  
##  <a name="SubscriptionSummary"></a>Samenvatting van abonnement  
 Hallo `subscription summary` entiteit Hallo volgende eigenschappen heeft.  
  
|Eigenschap|Type|Beschrijving|  
|--------------|----------|-----------------|  
|Id|Tekenreeks|Bron-id. Een unieke identificatie Hallo abonnement binnen het huidige exemplaar van API Management-service Hallo. Hallo-waarde is een geldig relatieve URL in de indeling van Hallo `subscriptions/{sid}` waar `{sid}` is de abonnement-id. Deze eigenschap is alleen-lezen.|  
|Weergavenaam|Tekenreeks|Hallo weergavenaam van het Hallo-abonnement|  
  
##  <a name="UserAccountInfo"></a>Gebruikersaccountgegevens  
 Hallo `user account info` entiteit Hallo volgende eigenschappen heeft.  
  
|Eigenschap|Type|Beschrijving|  
|--------------|----------|-----------------|  
|Voornaam|Tekenreeks|De voornaam. Mag niet leeg zijn. Maximale lengte is 100 tekens.|  
|Achternaam|Tekenreeks|De achternaam. Mag niet leeg zijn. Maximale lengte is 100 tekens.|  
|E-mail|Tekenreeks|E-mailadres. Mag niet leeg zijn en moet uniek zijn binnen Hallo service-exemplaar. Maximale lengte is 254 tekens.|  
|Wachtwoord|Tekenreeks|Het wachtwoord voor gebruikersaccount.|  
|NameIdentifier|Tekenreeks|Account-id, hello hetzelfde als e-mailadres Hallo gebruiker.|  
|ProviderName|Tekenreeks|Providernaam van verificatie.|  
|IsBasicAccount|Booleaanse waarde|De waarde True als dit account is geregistreerd met e-mailadres en wachtwoord; ONWAAR als het Hallo-account is geregistreerd met een provider.|  
  
##  <a name="UseSignIn"></a>Gebruiker aanmelden  
 Hallo `user sign in` entiteit Hallo volgende eigenschappen heeft.  
  
|Eigenschap|Type|Beschrijving|  
|--------------|----------|-----------------|  
|E-mail|Tekenreeks|E-mailadres. Mag niet leeg zijn en moet uniek zijn binnen Hallo service-exemplaar. Maximale lengte is 254 tekens.|  
|Wachtwoord|Tekenreeks|Het wachtwoord voor gebruikersaccount.|  
|ReturnUrl|Tekenreeks|Hallo-URL van Hallo-pagina waar Hallo gebruiker aanmelden klikt.|  
|RememberMe|Booleaanse waarde|Hiermee wordt aangegeven of Hallo toosave informatie van huidige gebruiker.|  
|RegistrationEnabled|Booleaanse waarde|Hiermee wordt aangegeven of de registratie is ingeschakeld.|  
|DelegationEnabled|Booleaanse waarde|Hiermee wordt aangegeven of gedelegeerde aanmelding is ingeschakeld.|  
|DelegationUrl|Tekenreeks|Hallo gedelegeerd-url, meld u aan als ingeschakeld.|  
|SsoSignUpUrl|Tekenreeks|Hallo één aanmelding URL voor Hallo gebruiker, indien aanwezig.|  
|AuxServiceUrl|Tekenreeks|Als de huidige gebruiker Hallo beheerder is, is dit een koppeling toohello service-exemplaar in Hallo klassieke Azure-Portal.|  
|Providers|Verzameling van [Provider](#Provider) entiteiten|Hallo-verificatieproviders voor deze gebruiker.|  
|UserRegistrationTerms|Tekenreeks|Termen die een gebruiker moet akkoord gaan toobefore aanmelden.|  
|UserRegistrationTermsEnabled|Booleaanse waarde|Hiermee wordt aangegeven of de voorwaarden zijn ingeschakeld.|  
  
##  <a name="UserSignUp"></a>Meld u aan gebruiker  
 Hallo `user sign up` entiteit Hallo volgende eigenschappen heeft.  
  
|Eigenschap|Type|Beschrijving|  
|--------------|----------|-----------------|  
|PasswordConfirm|Booleaanse waarde|Waarde die wordt gebruikt door Hallo [aanmelding](api-management-page-controls.md#sign-up)aanmelding besturingselement.|  
|Wachtwoord|Tekenreeks|Het wachtwoord voor gebruikersaccount.|  
|PasswordVerdictLevel|Aantal|Waarde die wordt gebruikt door Hallo [aanmelding](api-management-page-controls.md#sign-up)aanmelding besturingselement.|  
|UserRegistrationTerms|Tekenreeks|Termen die een gebruiker moet akkoord gaan toobefore aanmelden.|  
|UserRegistrationTermsOptions|Aantal|Waarde die wordt gebruikt door Hallo [aanmelding](api-management-page-controls.md#sign-up)aanmelding besturingselement.|  
|ConsentAccepted|Booleaanse waarde|Waarde die wordt gebruikt door Hallo [aanmelding](api-management-page-controls.md#sign-up)aanmelding besturingselement.|  
|E-mail|Tekenreeks|E-mailadres. Mag niet leeg zijn en moet uniek zijn binnen Hallo service-exemplaar. Maximale lengte is 254 tekens.|  
|Voornaam|Tekenreeks|De voornaam. Mag niet leeg zijn. Maximale lengte is 100 tekens.|  
|Achternaam|Tekenreeks|De achternaam. Mag niet leeg zijn. Maximale lengte is 100 tekens.|  
|UserData|Tekenreeks|Waarde die wordt gebruikt door Hallo [aanmelding](api-management-page-controls.md#sign-up) besturingselement.|  
|NameIdentifier|Tekenreeks|Waarde die wordt gebruikt door Hallo [aanmelding](api-management-page-controls.md#sign-up)aanmelding besturingselement.|  
|ProviderName|Tekenreeks|Providernaam van verificatie.|

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over het werken met sjablonen [hoe toocustomize API Management-portal voor ontwikkelaars met behulp van sjablonen Hallo](api-management-developer-portal-templates.md).
