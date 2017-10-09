---
title: aaaError verwerken in Azure API Management-beleid | Microsoft Docs
description: Meer informatie over hoe toorespond tooerror voorwaarden die tijdens optreden kunnen de verwerking van aanvragen in Azure API Management Hallo.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 3c777964-02b2-4f55-8731-8c3bd3c0ae27
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 002c65f21e763fd644da61b6a11685ffd97488c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="error-handling-in-api-management-policies"></a>Fout tijdens verwerken van in API Management-beleidsregels
Azure API Management kunnen uitgevers toorespond tooerror voorwaarden die tijdens de verwerking van aanvragen toohello proxy Hallo doordat optreden kunnen een `ProxyError` object. Hallo `ProxyError` object kan worden geopend via Hallo [context. LastError](api-management-policy-expressions.md#ContextVariables) eigenschap en kan worden gebruikt door het beleid in Hallo `on-error` beleidssectie. Dit onderwerp bevat een verwijzing voor Hallo fout verwerking mogelijkheden in Azure API Management.  
  
## <a name="error-handling-in-api-management"></a>Fout tijdens verwerken van in API Management  
 Beleid in Azure API Management zijn onderverdeeld in `inbound`, `backend`, `outbound`, en `on-error` zoals weergegeven in het volgende voorbeeld Hallo secties.  
  
```xml  
<policies>  
  <inbound>  
    <!-- statements toobe applied toohello request go here -->  
  </inbound>  
  <backend>  
    <!-- statements toobe applied before hello request is   
         forwarded toohello backend service go here -->  
    </backend>  
    <outbound>  
      <!-- statements toobe applied toohello response go here -->  
    </outbound>  
    <on-error>  
        <!-- statements toobe applied if there is an error   
             condition go here -->  
  </on-error>  
</policies>  
```  
  
 Tijdens de verwerking van een aanvraag Hallo ingebouwde stappen uitgevoerd samen met het beleid dat in het bereik voor Hallo-aanvraag. Als er een fout optreedt, verwerking van onmiddellijk aan de slag gaat toohello `on-error` beleidssectie. Hallo `on-error` beleidssectie kan worden gebruikt op een bereik en API-uitgevers aangepaste gedrag zoals logboekregistratie Hallo fout tooevent hubs of maken van een nieuw antwoord tooreturn toohello aanroeper kunnen configureren.  
  
> [!NOTE]
>  Hallo `on-error` sectie is niet aanwezig in het beleid standaard. tooadd hello `on-error` sectie tooa beleid, toohello gewenst beleid in de beleidseditor Hallo bladeren en toe te voegen. Zie voor meer informatie over het configureren van beleid [-beleid in API Management](https://azure.microsoft.com/documentation/articles/api-management-howto-policies/).  
>   
>  Als er geen `on-error` sectie aanroepfuncties 400 of 500 HTTP-antwoordberichten ontvangt als er een fout optreedt.  
  
### <a name="policies-allowed-in-on-error"></a>Beleid dat is toegestaan in op fout  
 Hallo volgende beleidsregels kunnen worden gebruikt in Hallo `on-error` beleidssectie.  
  
-   [Kies](api-management-advanced-policies.md#choose)  
  
-   [variabele instellen](api-management-advanced-policies.md#set-variable)  
  
-   [zoeken en vervangen](api-management-transformation-policies.md#Findandreplacestringinbody)  
  
-   [Return-antwoord](api-management-advanced-policies.md#ReturnResponse)  
  
-   [set-header](api-management-transformation-policies.md#SetHTTPheader)  
  
-   [set-methode](api-management-advanced-policies.md#SetRequestMethod)  
  
-   [status instellen](api-management-advanced-policies.md#SetStatus)  
  
-   [aanvragen verzenden](api-management-advanced-policies.md#SendRequest)  
  
-   [een-manier-verzoek om te verzenden](api-management-advanced-policies.md#SendOneWayRequest)  
  
-   [logboek voor eventhub](api-management-advanced-policies.md#log-to-eventhub)  
  
-   [JSON-to-xml](api-management-transformation-policies.md#ConvertJSONtoXML)  
  
-   [XML-json-](api-management-transformation-policies.md#ConvertXMLtoJSON)  
  
## <a name="lasterror"></a>LastError  
 Wanneer er een fout optreedt en het besturingselement aan de slag gaat toohello `on-error` beleidssectie Hallo fout wordt opgeslagen in [context. LastError](api-management-policy-expressions.md#ContextVariables) -eigenschap hebben die toegankelijk zijn voor het beleid in Hallo `on-error` sectie en Hallo volgende eigenschappen heeft.  
  
|Naam|Type|Beschrijving|Vereist|  
|----------|----------|-----------------|--------------|  
|Bron|Tekenreeks|Namen Hallo element waarin Hallo-fout is opgetreden. Kan worden beleid of de naam van een ingebouwde pijplijn stap.|Ja|  
|Reden|Tekenreeks|Machine-vriendelijk foutcode die kan worden gebruikt in de foutafhandeling.|Nee|  
|Bericht|Tekenreeks|Er zijn foutomschrijving leesbare.|Ja|  
|Bereik|Tekenreeks|Naam van de scope Hallo waar Hallo-fout opgetreden en mogelijk een van de 'global', 'product', 'api' of 'bewerking'|Nee|  
|Sectie|Tekenreeks|Naam van de sectie waar de fout is opgetreden en kan een van de 'inkomende', back-end', 'uitgaande' of 'on error'.|Nee|  
|Pad|Tekenreeks|Hiermee geeft u geneste beleid, bijvoorbeeld ' kiezen [3] / wanneer [2] '.|Nee|  
|PolicyId|Tekenreeks|Waarde van Hallo `id` kenmerk toe, indien opgegeven door de klant Hallo op Hallo beleid waar de fout is opgetreden|Nee|  
  
> [!NOTE]
>  Alle beleidsregels hebben een optioneel `id` kenmerk die toohello hoofdelement van het Hallo-beleid kan worden toegevoegd. Als dit kenmerk aanwezig in een beleid is als een fout optreedt, Hallo-waarde van het Hallo-kenmerk kan worden opgehaald met Hallo `context.LastError.PolicyId` eigenschap.  
  
## <a name="predefined-errors-for-built-in-steps"></a>Vooraf gedefinieerde fouten voor de ingebouwde stappen  
 Hallo volgende fouten zijn vooraf gedefinieerd voor foutvoorwaarden die tijdens de evaluatie van de van de ingebouwde verwerkingsstappen Hallo optreden kunnen.  
  
|Bron|Voorwaarde|Reden|Bericht|  
|------------|---------------|------------|-------------|  
|configuratie|URI komt niet overeen met bewerking of tooany Api|OperationNotFound|Kan geen toomatch binnenkomende aanvraag tooan bewerking.|  
|Autorisatie|Abonnementssleutel niet opgegeven|SubscriptionKeyNotFound|Toegang is geweigerd vanwege toomissing abonnementssleutel. Zorg ervoor dat tooinclude abonnementssleutel bij het maken van aanvragen toothis API.|  
|Autorisatie|De sleutelwaarde abonnement is ongeldig|SubscriptionKeyInvalid|Toegang is geweigerd vanwege tooinvalid abonnementssleutel. Zorg ervoor dat tooprovide een geldige sleutel voor een actief abonnement.|  
  
## <a name="predefined-errors-for-policies"></a>Vooraf gedefinieerde fouten voor beleid  
 Hallo volgende fouten zijn vooraf gedefinieerd voor fouten die tijdens de evaluatie van het beleid optreden kunnen.  
  
|Bron|Voorwaarde|Reden|Bericht|  
|------------|---------------|------------|-------------|  
|Frequentielimiet|Frequentielimiet is overschreden|RateLimitExceeded|Frequentielimiet is overschreden|  
|quotum|Quota overschreden|QuotaExceeded|Volumequotum buiten bereik. Quotum wordt aangevuld in xx:xx:xx. - of - Out van de quota voor bandbreedte. Quotum wordt aangevuld in xx:xx:xx.|  
|jsonp|De parameterwaarde retouraanroep is ongeldig (bevat verkeerde tekens)|CallbackParameterInvalid|Waarde van parameter callback {retouraanroep-parameter-name} is geen geldige JavaScript-id.|  
|IP-filter|Mislukte tooparse aanroeper IP-adres uit de aanvraag|FailedToParseCallerIP|Kan geen tooestablish IP-adres voor Hallo aanroeper. Toegang geweigerd.|  
|IP-filter|Aanroeper IP staat niet in lijst met toegestane|CallerIpNotAllowed|Aanroeper {IP-adres-} is niet toegestaan. Toegang geweigerd.|  
|IP-filter|Aanroeper IP staat in de lijst met geblokkeerde|CallerIpBlocked|Aanroeper IP-adres wordt geblokkeerd. Toegang geweigerd.|  
|controle-header|Vereiste header is niet opgenomen of waarde ontbreekt|HeaderNotFound|Header {header-name} is niet gevonden in Hallo-aanvraag. Toegang geweigerd.|  
|controle-header|Vereiste header is niet opgenomen of waarde ontbreekt|HeaderValueNotAllowed|De waarde van de header {headernaam} van {headerwaarde} is niet toegestaan. Toegang geweigerd.|  
|valideren jwt|Jwt-token ontbreekt in de aanvraag|TokenNotFound|De JWT is niet gevonden in het Hallo-aanvraag. Toegang geweigerd.|  
|valideren jwt|Handtekeningvalidatie is mislukt|TokenSignatureInvalid|< bericht van jwt-bibliotheek\>. Toegang geweigerd.|  
|valideren jwt|Ongeldige doelgroep|TokenAudienceNotAllowed|< bericht van jwt-bibliotheek\>. Toegang geweigerd.|  
|valideren jwt|Ongeldige verlener|TokenIssuerNotAllowed|< bericht van jwt-bibliotheek\>. Toegang geweigerd.|  
|valideren jwt|Token is verlopen|TokenExpired|< bericht van jwt-bibliotheek\>. Toegang geweigerd.|  
|valideren jwt|Handtekeningsleutel is niet opgelost door de id|TokenSignatureKeyNotFound|< bericht van jwt-bibliotheek\>. Toegang geweigerd.|  
|valideren jwt|Er ontbreken vereiste claims in token|TokenClaimNotFound|JWT-token ontbreekt Hallo claims te volgen: < c1\>, < c2\>,... Toegang geweigerd.|  
|valideren jwt|Claim waarden verschil|TokenClaimValueNotAllowed|Claimwaarde {claimnaam} van {claimwaarde} is niet toegestaan. Toegang geweigerd.|  
|valideren jwt|Andere validatiefouten|JwtInvalid|< bericht van jwt-bibliotheek\>|

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie werken met beleid [-beleid in API Management](api-management-howto-policies.md).  