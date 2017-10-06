---
title: aaaAzure API Management toegangsbeleid beperking | Microsoft Docs
description: Meer informatie over Hallo beperking toegangsbeleid beschikbaar voor gebruik in Azure API Management.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 034febe3-465f-4840-9fc6-c448ef520b0f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 0ef368c2781d9a5cf9eaaa41a47489c904ed3198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-access-restriction-policies"></a>Beperking van API Management toegangsbeleid
Dit onderwerp bevat een verwijzing voor Hallo API Management-beleidsregels te volgen. Zie voor meer informatie over het toevoegen en configureren van beleid [-beleid in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="AccessRestrictionPolicies"></a>Softwarerestrictiebeleid toegang  
  
-   [Controle van HTTP-header](api-management-access-restriction-policies.md#CheckHTTPHeader) -afdwingt bestaan en/of de waarde van een HTTP-Header.  
  
-   [Aanroepfrequentie per abonnement](api-management-access-restriction-policies.md#LimitCallRate) -API wordt voorkomen dat gebruik wordt bereikt door het beperken van de aanroepfrequentie per abonnement op basis van een.  
  
-   [Aanroepfrequentie per sleutel](#LimitCallRateByKey) -API wordt voorkomen dat gebruik wordt bereikt door het beperken van de aanroepfrequentie per sleutel op basis van een.  
  
-   [Aanroeper IP-adressen beperken](api-management-access-restriction-policies.md#RestrictCallerIPs) -Filters (kunt/weigert) aanroepen van bepaalde IP-adressen en/of -adresbereiken.  
  
-   [Gebruiksquotum per abonnement instellen](api-management-access-restriction-policies.md#SetUsageQuota) -kunt u een vernieuwd of levensduur aanroep volume en/of bandbreedte quotum tooenforce op basis van per abonnement.  
  
-   [Gebruiksquotum instellen door sleutel](#SetUsageQuotaByKey) -kunt u een vernieuwd of levensduur aanroep volume en/of bandbreedte quotum tooenforce op basis van de per-sleutel.  
  
-   [Valideren van JWT](api-management-access-restriction-policies.md#ValidateJWT) -afdwingt bestaan en de geldigheid van een JWT opgehaald uit een opgegeven HTTP-koptekst of een opgegeven queryparameter.  
  
##  <a name="CheckHTTPHeader"></a>Controleer de HTTP-header  
 Gebruik Hallo `check-header` beleid tooenforce dat een aanvraag een opgegeven HTTP-header heeft. U kunt eventueel toosee controleren als Hallo-header een specifieke waarde of het selectievakje voor een bereik van toegestane waarden is. Hallo controle mislukt, Hallo beleid aanvraagverwerking wordt beëindigd als HTTP-status code en de fout welkomstbericht opgegeven door het beleid voor Hallo retourneert.  
  
### <a name="policy-statement"></a>Beleidsverklaring  
  
```xml  
<check-header name="header name" failed-check-httpcode="code" failed-check-error-message="message" ignore-case="True">  
    <value>Value1</value>  
    <value>Value2</value>  
</check-header>  
```  
  
### <a name="example"></a>Voorbeeld  
  
```xml  
<check-header name="Authorization" failed-check-httpcode="401" failed-check-error-message="Not authorized" ignore-case="false">  
    <value>f6dc69a089844cf6b2019bae6d36fac8</value>  
</check-header>  
```  
  
### <a name="elements"></a>Elementen  
  
|Naam|Beschrijving|Vereist|  
|----------|-----------------|--------------|  
|controle-header|Hoofdelement.|Ja|  
|waarde|Toegestane waarde voor HTTP-header. Als meerdere elementen van de waarde worden opgegeven, Hallo selectievakje wordt beschouwd als geslaagd als een van de waarden Hallo een overeenkomst.|Nee|  
  
### <a name="attributes"></a>Kenmerken  
  
|Naam|Beschrijving|Vereist|Standaard|  
|----------|-----------------|--------------|-------------|  
|kan de niet-controle-foutbericht|Fout bericht tooreturn in Hallo HTTP-antwoordtekst als Hallo header bestaat niet of een ongeldige waarde heeft. Dit bericht moet de speciale tekens escape hebben.|Ja|N.v.t.|  
|Kan controle httpcode|HTTP-Status code tooreturn als Hallo header bestaat niet of een ongeldige waarde heeft.|Ja|N.v.t.|  
|header-naam|de naam van de Hallo Hallo toocheck HTTP-Header.|Ja|N.v.t.|  
|negeren geval|Kan worden ingesteld tooTrue of ONWAAR. Als de set tooTrue aanvraag wordt genegeerd wanneer het Hallo-kopwaarde vergeleken met de Hallo set van acceptabele waarden.|Ja|N.v.t.|  
  
### <a name="usage"></a>Gebruik  
 Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Beleid secties:** binnenkomende, uitgaande  
  
-   **Beleid scopes:** wereldwijd, product, API, bewerking  
  
##  <a name="LimitCallRate"></a>Aanroepfrequentie per abonnement  
 Hallo `rate-limit` beleid voorkomt dat het gebruik van de API pieken per abonnement op basis van een door het beperken van Hallo aanroepen snelheid tooa opgegeven aantal gedurende een opgegeven periode. Wanneer dit beleid wordt geactiveerd Hallo aanroeper ontvangt een `429 Too Many Requests` statuscode van antwoord.  
  
> [!IMPORTANT]
>  Dit beleid kan slechts één keer per beleidsdocument worden gebruikt.  
>   
>  [Beleidsexpressies](api-management-policy-expressions.md) kan niet worden gebruikt in een van de kenmerken van Hallo-beleid voor dit beleid.  
  
### <a name="policy-statement"></a>Beleidsverklaring  
  
```xml  
<rate-limit calls="number" renewal-period="seconds">  
    <api name="name" calls="number" renewal-period="seconds">  
        <operation name="name" calls="number" renewal-period="seconds" />  
    </api>  
</rate-limit>  
```  
  
### <a name="example"></a>Voorbeeld  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rate-limit calls="20" renewal-period="90" />  
    </inbound>  
    <outbound>  
        <base />          
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Elementen  
  
|Naam|Beschrijving|Vereist|  
|----------|-----------------|--------------|  
|opgegeven limiet|Hoofdelement.|Ja|  
|api|Een of meer van deze elementen tooimpose een frequentielimiet aanroep op API's binnen Hallo product toevoegen. Producten en -API aanroepen snelheid limieten onafhankelijk worden toegepast.|Nee|  
|bewerking|Een of meer van deze elementen tooimpose een frequentielimiet aanroep op bewerkingen binnen een API toevoegen. Product, API en bewerking aanroepen snelheid limieten onafhankelijk worden toegepast.|Nee|  
  
### <a name="attributes"></a>Kenmerken  
  
|Naam|Beschrijving|Vereist|Standaard|  
|----------|-----------------|--------------|-------------|  
|naam|Hallo de naam van Hallo API voor welke tooapply Hallo limiet.|Ja|N.v.t.|  
|aanroepen|maximum aantal aanroepen toegestaan tijdens het Hallo tijdsinterval is opgegeven in Hallo Hallo `renewal-period`.|Ja|N.v.t.|  
|vernieuwingsperiode|Hallo periode in seconden waarna hello quotum wordt opnieuw ingesteld.|Ja|N.v.t.|  
  
### <a name="usage"></a>Gebruik  
 Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Beleid secties:** inkomende  
  
-   **Beleid scopes:** product  
  
##  <a name="LimitCallRateByKey"></a>Aanroepfrequentie per sleutel  
 Hallo `rate-limit-by-key` beleid voorkomt dat het gebruik van de API pieken per sleutel op basis van een door het beperken van Hallo aanroepen snelheid tooa opgegeven aantal gedurende een opgegeven periode. Hallo-sleutel kan een willekeurige tekenreekswaarde en wordt meestal verzorgd door een beleidsexpressie met. Optionele incrementele voorwaarde kan worden toegevoegd als toospecify welke aanvragen naar Hallo limiet moeten worden geteld. Wanneer dit beleid wordt geactiveerd Hallo aanroeper ontvangt een `429 Too Many Requests` statuscode van antwoord.  
  
 Zie voor meer informatie over en voorbeelden van dit beleid, [geavanceerde aanvraagbeperking met Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).  
  
> [!IMPORTANT]
>  Dit beleid kan slechts één keer per beleidsdocument worden gebruikt.  
  
### <a name="policy-statement"></a>Beleidsverklaring  
  
```xml  
<rate-limit-by-key calls="number"  
                   renewal-period="seconds"   
                   increment-condition="condition"   
                   counter-key="key value" />  
  
```  
  
### <a name="example"></a>Voorbeeld  
 In Hallo voorbeeld te volgen, wordt de frequentielimiet Hallo ingevoerd met Hallo aanroeper IP-adres.  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rate-limit-by-key  calls="10"  
              renewal-period="60"  
              increment-condition="@(context.Response.StatusCode == 200)"  
              counter-key="@(context.Request.IpAddress)"/>  
    </inbound>  
    <outbound>  
        <base />          
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Elementen  
  
|Naam|Beschrijving|Vereist|  
|----------|-----------------|--------------|  
|opgegeven limiet|Hoofdelement.|Ja|  
  
### <a name="attributes"></a>Kenmerken  
  
|Naam|Beschrijving|Vereist|Standaard|  
|----------|-----------------|--------------|-------------|  
|aanroepen|maximum aantal aanroepen toegestaan tijdens het Hallo tijdsinterval is opgegeven in Hallo Hallo `renewal-period`.|Ja|N.v.t.|  
|tegenpartij sleutel|Hallo sleutel toouse voor beleid voor frequentielimiet Hallo.|Ja|N.v.t.|  
|verhoging voorwaarde|Hallo Booleaanse expressie opgeven als Hallo-aanvraag moet worden geteld voor Hallo quotum (`true`).|Nee|N.v.t.|  
|vernieuwingsperiode|Hallo periode in seconden waarna hello quotum wordt opnieuw ingesteld.|Ja|N.v.t.|  
  
### <a name="usage"></a>Gebruik  
 Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Beleid secties:** inkomende  
  
-   **Beleid scopes:** wereldwijd, product, API, bewerking  
  
##  <a name="RestrictCallerIPs"></a>Aanroeper IP-adressen beperken  
 Hallo `ip-filter` beleid filtert (kunt/weigert) aanroepen van bepaalde IP-adressen en/of -adresbereiken.  
  
### <a name="policy-statement"></a>Beleidsverklaring  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="example"></a>Voorbeeld  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="elements"></a>Elementen  
  
|Naam|Beschrijving|Vereist|  
|----------|-----------------|--------------|  
|IP-filter|Hoofdelement.|Ja|  
|Adres|Hiermee geeft u één IP-adres op welke toofilter.|Ten minste één `address` of `address-range` element is vereist.|  
|adresbereik van = 'adres' naar 'adres' =|Hiermee geeft u een bereik met IP-adres op welke toofilter.|Ten minste één `address` of `address-range` element is vereist.|  
  
### <a name="attributes"></a>Kenmerken  
  
|Naam|Beschrijving|Vereist|Standaard|  
|----------|-----------------|--------------|-------------|  
|adresbereik van = 'adres' naar 'adres' =|Een bereik met IP-adressen tooallow of weigeren van toegang voor.|Vereist wanneer hello `address-range` element wordt gebruikt.|N.v.t.|  
|IP-filteractie = ' toestaan dat &#124; verbieden"|Geeft aan of aanroepen moeten worden toegestaan of niet voor Hallo IP-adressen en -bereiken opgegeven.|Ja|N.v.t.|  
  
### <a name="usage"></a>Gebruik  
 Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Beleid secties:** inkomende  
  
-   **Beleid scopes:** wereldwijd, product, API, bewerking  
  
##  <a name="SetUsageQuota"></a>Gebruiksquotum per abonnement instellen  
 Hallo `quota` beleid zorgt ervoor dat een vernieuwd of levensduur aanroep volume en/of bandbreedte quotum, op basis van per abonnement.  
  
> [!IMPORTANT]
>  Dit beleid kan slechts één keer per beleidsdocument worden gebruikt.  
>   
>  [Beleidsexpressies](api-management-policy-expressions.md) kan niet worden gebruikt in een van de kenmerken van Hallo-beleid voor dit beleid.  
  
### <a name="policy-statement"></a>Beleidsverklaring  
  
```xml  
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">  
    <api name="name" calls="number" bandwidth="kilobytes">  
        <operation name="name" calls="number" bandwidth="kilobytes" />  
    </api>  
</quota>  
```  
  
### <a name="example"></a>Voorbeeld  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <quota calls="10000" bandwidth="40000" renewal-period="3600" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Elementen  
  
|Naam|Beschrijving|Vereist|  
|----------|-----------------|--------------|  
|quotum|Hoofdelement.|Ja|  
|api|Een of meer van deze elementen tooimpose een quotum op API's binnen Hallo product toevoegen. Product- en API-quota worden onafhankelijk toegepast.|Nee|  
|bewerking|Een of meer van deze elementen tooimpose een quotum op bewerkingen binnen een API toevoegen. Product, API en bewerking quota's worden onafhankelijk van elkaar toegepast.|Nee|  
  
### <a name="attributes"></a>Kenmerken  
  
|Naam|Beschrijving|Vereist|Standaard|  
|----------|-----------------|--------------|-------------|  
|naam|Hallo-naam van het Hallo-API of de bewerking voor welke Hallo quotum van toepassing.|Ja|N.v.t.|  
|Bandbreedte|maximum aantal kilobytes is toegestaan tijdens het Hallo tijdsinterval is opgegeven in Hallo Hallo `renewal-period`.|Beide `calls`, `bandwidth`, of beide moeten samen worden opgegeven.|N.v.t.|  
|aanroepen|maximum aantal aanroepen toegestaan tijdens het Hallo tijdsinterval is opgegeven in Hallo Hallo `renewal-period`.|Beide `calls`, `bandwidth`, of beide moeten samen worden opgegeven.|N.v.t.|  
|vernieuwingsperiode|Hallo periode in seconden waarna hello quotum wordt opnieuw ingesteld.|Ja|N.v.t.|  
  
### <a name="usage"></a>Gebruik  
 Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Beleid secties:** inkomende  
  
-   **Beleid scopes:** product  
  
##  <a name="SetUsageQuotaByKey"></a>Gebruiksquotum instellen door sleutel  
 Hallo `quota-by-key` beleid zorgt ervoor dat een vernieuwd of levensduur aanroep volume en/of bandbreedte quotum, op basis van de per-sleutel. Hallo-sleutel kan een willekeurige tekenreekswaarde en wordt meestal verzorgd door een beleidsexpressie met. Optionele incrementele voorwaarde kan worden toegevoegd als toospecify welke aanvragen naar Hallo quotum moeten worden geteld.  
  
 Zie voor meer informatie over en voorbeelden van dit beleid, [geavanceerde aanvraagbeperking met Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).  
  
> [!IMPORTANT]
>  Dit beleid kan slechts één keer per beleidsdocument worden gebruikt.  
>   
>  [Beleidsexpressies](api-management-policy-expressions.md) kan niet worden gebruikt in een van de kenmerken van Hallo-beleid voor dit beleid.  
  
### <a name="policy-statement"></a>Beleidsverklaring  
  
```xml  
<quota-by-key calls="number"   
              bandwidth="kilobytes"   
              renewal-period="seconds"  
              increment-condition="condition"   
              counter-key="key value" />  
  
```  
  
### <a name="example"></a>Voorbeeld  
 In Hallo voorbeeld te volgen, wordt de Hallo quotum ingevoerd met Hallo aanroeper IP-adres.  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <quota-by-key calls="10000" bandwidth="40000" renewal-period="3600"  
                      increment-condition="@(context.Response.StatusCode >= 200 && context.Response.StatusCode < 400)"  
                      counter-key="@(context.Request.IpAddress)" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Elementen  
  
|Naam|Beschrijving|Vereist|  
|----------|-----------------|--------------|  
|quotum|Hoofdelement.|Ja|  
  
### <a name="attributes"></a>Kenmerken  
  
|Naam|Beschrijving|Vereist|Standaard|  
|----------|-----------------|--------------|-------------|  
|Bandbreedte|maximum aantal kilobytes is toegestaan tijdens het Hallo tijdsinterval is opgegeven in Hallo Hallo `renewal-period`.|Beide `calls`, `bandwidth`, of beide moeten samen worden opgegeven.|N.v.t.|  
|aanroepen|maximum aantal aanroepen toegestaan tijdens het Hallo tijdsinterval is opgegeven in Hallo Hallo `renewal-period`.|Beide `calls`, `bandwidth`, of beide moeten samen worden opgegeven.|N.v.t.|  
|tegenpartij sleutel|Hallo sleutel toouse voor Hallo quotumbeleid.|Ja|N.v.t.|  
|verhoging voorwaarde|Hallo Booleaanse expressie opgeven als Hallo-aanvraag moet worden geteld voor Hallo quotum (`true`)|Nee|N.v.t.|  
|vernieuwingsperiode|Hallo periode in seconden waarna hello quotum wordt opnieuw ingesteld.|Ja|N.v.t.|  
  
### <a name="usage"></a>Gebruik  
 Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Beleid secties:** inkomende  
  
-   **Beleid scopes:** wereldwijd, product, API, bewerking  
  
##  <a name="ValidateJWT"></a>JWT valideren  
 Hallo `validate-jwt` beleid zorgt ervoor dat bestaan en de geldigheid van een JWT opgehaald uit beide een opgegeven HTTP-Header of een opgegeven queryparameter.  
  
> [!IMPORTANT]
>  Hallo `validate-jwt` beleid vereist dat Hallo `exp` geregistreerde claim is inlcuded in Hallo JWT-token, tenzij `require-expiration-time` kenmerk is opgegeven en ingesteld te`false`.  
> Hallo `validate-jwt` beleid ondersteunt HS256 en RS256 ondertekenen algoritmen. HS256 moet Hallo-sleutel worden opgegeven voor inline binnen Hallo beleid Hallo base64-gecodeerde vorm. Hallo-sleutel heeft voor RS256 toobe bieden via een Open ID configuratie-eindpunt.  
  
### <a name="policy-statement"></a>Beleidsverklaring  
  
```xml  
<validate-jwt   
    header-name="name of http header containing hello token (use query-parameter-name attribute if hello token is passed in hello URL)"   
    failed-validation-httpcode="http status code tooreturn on failure"   
    failed-validation-error-message="error message tooreturn on failure"   
    require-expiration-time="true|false"
    require-scheme="scheme"
    require-signed-tokens="true|false"   
    clock-skew="allowed clock skew in seconds">  
  <issuer-signing-keys>  
    <key>base64 encoded signing key</key>  
    <!-- if there are multiple keys, then add additional key elements -->  
  </issuer-signing-keys>  
  <audiences>  
    <audience>audience string</audience>  
    <!-- if there are multiple possible audiences, then add additional audience elements -->  
  </audiences>  
  <issuers>  
    <issuer>issuer string</issuer>  
    <!-- if there are multiple possible issuers, then add additional issuer elements -->  
  </issuers>  
  <required-claims>  
    <claim name="name of hello claim as it appears in hello token" match="all|any">  
      <value>claim value as it is expected tooappear in hello token</value>  
      <!-- if there is more than one allowed values, then add additional value elements -->  
    </claim>  
    <!-- if there are multiple possible allowed values, then add additional value elements -->  
  </required-claims>  
  <openid-config url="full URL of hello configuration endpoint, e.g. https://login.constoso.com/openid-configuration" />  
  <zumo-master-key id="key identifier">key value</zumo-master-key>  
</validate-jwt>  
  
```  
  
### <a name="examples"></a>Voorbeelden  
  
#### <a name="azure-mobile-services-token-validation"></a>Validatie van Azure Mobile Services-tokens  
  
```xml  
<validate-jwt header-name="x-zumo-auth" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Supplied access token is invalid.">  
    <issuers>  
        <issuer>urn:microsoft:windows-azure:zumo</issuer>  
    </issuers>  
    <audiences>  
        <audience>Facebook</audience>  
    </audiences>  
    <issuer-signing-keys>  
        <zumo-master-key id="0">insert key here</zumo-master-key>  
    </issuer-signing-keys>  
</validate-jwt>  
```  
  
#### <a name="azure-active-directory-token-validation"></a>Validatie van Azure Active Directory-tokens  
  
```xml  
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">  
    <openid-config url="https://login.microsoftonline.com/contoso.onmicrosoft.com/.well-known/openid-configuration" />  
    <audiences>
        <audience>25eef6e4-c905-4a07-8eb4-0d08d5df8b3f</audience>
    </audiences>
    <required-claims>  
        <claim name="id" match="all">  
            <value>insert claim here</value>  
        </claim>  
    </required-claims>  
</validate-jwt>  
```  

  
#### <a name="azure-active-directory-b2c-token-validation"></a>Validatie van Azure Active Directory B2C-tokens  
  
```xml  
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">  
    <openid-config url="https://login.microsoftonline.com/tfp/contoso.onmicrosoft.com/b2c_1_signin/v2.0/.well-known/openid-configuration" />
    <audiences>
        <audience>d313c4e4-de5f-4197-9470-e509a2f0b806</audience>
    </audiences>
    <required-claims>  
        <claim name="id" match="all">  
            <value>insert claim here</value>  
        </claim>  
    </required-claims>  
</validate-jwt>  
```  
  
#### <a name="authorize-access-toooperations-based-on-token-claims"></a>Toegang toooperations op basis van claims token autoriseren  
 Dit voorbeeld ziet u hoe toouse hello [JWT valideren](api-management-access-restriction-policies.md#ValidateJWT) beleid toopre-toegang toooperations op basis van claims token autoriseren. Zie voor een demonstratie van configureren en gebruiken van dit beleid [Cloud hebben betrekking op aflevering 177: meer API-beheerfuncties met Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) en too13:50 vooruit. Snel toosee Hallo beleid dat is geconfigureerd in de beleidseditor Hallo doorsturen too15:00 en vervolgens too18:50 voor een demonstratie van een bewerking aanroepen vanuit de ontwikkelaarsportal Hallo zowel met als zonder Hallo verificatietoken vereist.  
  
```xml  
<!-- Copy hello following snippet into hello inbound section at hello api (or higher) level toopre-authorize access toooperations based on token claims -->  
<set-variable name="signingKey" value="insert signing key here" />  
<choose>  
  <when condition="@(context.Request.Method.Equals("patch",StringComparison.OrdinalIgnoreCase))">  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
      <required-claims>  
        <claim name="edit">  
          <value>true</value>  
        </claim>  
      </required-claims>  
    </validate-jwt>  
  </when>  
  <when condition="@(new [] {"post", "put"}.Contains(context.Request.Method,StringComparer.OrdinalIgnoreCase))">  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
      <required-claims>  
        <claim name="create">  
          <value>true</value>  
        </claim>  
      </required-claims>  
    </validate-jwt>  
  </when>  
  <otherwise>  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
    </validate-jwt>  
  </otherwise>  
</choose>  
```  
  
### <a name="elements"></a>Elementen  
  
|Element|Beschrijving|Vereist|  
|-------------|-----------------|--------------|  
|valideren jwt|Hoofdelement.|Ja|  
|doelgroepen|Bevat een lijst met toegestane doelgroep claims die gebruikt op Hallo-token worden kunnen. Als meerdere doelgroep waarden aanwezig zijn, wordt elke waarde wordt geprobeerd totdat alle (in dat geval validatie mislukt) zijn uitgeput of tot er één lukt. Ten minste één doelgroep moet worden opgegeven.|Nee|  
|ondertekening-sleutels van uitgever|Een lijst met Base64-gecodeerd beveiliging sleutels die worden gebruikt toovalidate ondertekend tokens. Als meerdere beveiligingssleutels aanwezig zijn, wordt elke sleutel wordt geprobeerd totdat alle (in dat geval validatie mislukt) zijn uitgeput of tot er één lukt (dit is nuttig voor de overschakeling van token). De belangrijkste elementen hebben een optioneel `id` toomatch kenmerk gebruikt tegen `kid` claim.|Nee|  
|uitgevers van certificaten|Een lijst met toegestane principals die Hallo token uitgegeven. Als meerdere verlener waarden aanwezig zijn, wordt elke waarde wordt geprobeerd totdat alle (in dat geval validatie mislukt) zijn uitgeput of tot er één lukt.|Nee|  
|openid-config|Hallo-element dat wordt gebruikt voor het opgeven van een compatibele configuratie-eindpunt voor Open-ID is waar ondertekenen van sleutels en uitgever kan worden verkregen.|Nee|  
|vereist claims|Bevat een lijst met claims verwacht toobe aanwezig is op Hallo token voor toobe als geldig beschouwd. Wanneer Hallo `match` kenmerk is ingesteld, te`all` elke claimwaarde in Hallo beleid moet aanwezig zijn in Hallo token voor validatie toosucceed. Wanneer Hallo `match` kenmerk is ingesteld, te`any` ten minste één claim moet aanwezig zijn in Hallo token voor validatie toosucceed.|Nee|  
|zumo hoofdsleutel|Hoofdsleutel voor tokens die zijn uitgegeven door Azure Mobile Services|Nee|  
  
### <a name="attributes"></a>Kenmerken  
  
|Naam|Beschrijving|Vereist|Standaard|  
|----------|-----------------|--------------|-------------|  
|tijdverschil|TimeSpan. Biedt een aantal kleine eenheidsprofiel geval Hallo-token verloopt claim aanwezig in het Hallo-token is en na de huidige Hallo valt datum / tijd.|Nee|0 seconden|  
|kan de niet-validatie-foutbericht|Fout bericht tooreturn in Hallo HTTP-antwoordtekst als Hallo JWT niet kan gevalideerd worden. Dit bericht moet de speciale tekens escape hebben.|Nee|Standaardfoutbericht, is afhankelijk van validatieprobleem, bijvoorbeeld 'JWT niet aanwezig."|  
|kan geen validatie httpcode|HTTP-Status code tooreturn als Hallo JWT validatie niet doorstaan.|Nee|401|  
|header-naam|Hallo-naam van Hallo HTTP-header Hallo-token bedrijf.|Ofwel `header-name` of `query-paremeter-name` moet worden opgegeven, maar niet beide.|N.v.t.|  
|id|Hallo `id` -kenmerk op Hallo `key` element kunt u toospecify Hallo tekenreeks die wordt vergeleken met `kid` claim in Hallo token (indien aanwezig) toofind uit Hallo geschikte sleutel toouse voor validatie van handtekening.|Nee|N.v.t.|  
|Overeenkomst|Hallo `match` -kenmerk op Hallo `claim` element geeft aan of de waarde van elke claim in Hallo beleid aanwezig in Hallo token voor validatie toosucceed zijn moet. Mogelijke waarden zijn:<br /><br /> -                          `all`-de waarde van elke claim in Hallo beleid moet aanwezig zijn in Hallo token voor validatie toosucceed.<br /><br /> -                          `any`-ten minste één claimwaarde moet aanwezig zijn in Hallo token voor validatie toosucceed.|Nee|Alle|  
|query-paremeter-naam|Hallo-naam van de queryparameter voor Hallo HALLO hallo-token bedrijf.|Ofwel `header-name` of `query-paremeter-name` moet worden opgegeven, maar niet beide.|N.v.t.|  
|vereisen verlooptijd vallen|Booleaanse waarde. Hiermee geeft u op of een claim vervaldatum in Hallo-token is vereist.|Nee|De waarde True|
|vereisen schema|naam van het token Hallo-schema, bijvoorbeeld Hallo 'Bearer'. Wanneer dit kenmerk is ingesteld, kan Hallo beleid zorgt ervoor dat het schema is aanwezig in Hallo autorisatie-header-waarde opgegeven.|Nee|N.v.t.|
|vereisen ondertekend-tokens|Booleaanse waarde. Geeft aan of een token vereist toobe ondertekend.|Nee|De waarde True|  
|URL|Open ID configuratie eindpunt-URL op waar de metagegevens van de Open-ID-configuratie kan worden verkregen. Voor Azure Active Directory gebruiken Hallo volgende URL: `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` waarbij u de naam van uw directory-tenant, bijvoorbeeld vervangt `contoso.onmicrosoft.com`.|Ja|N.v.t.|  
  
### <a name="usage"></a>Gebruik  
 Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Beleid secties:** inkomende  
  
-   **Beleid scopes:** wereldwijd, product, API, bewerking  
  
## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie werken met beleid [-beleid in API Management](api-management-howto-policies.md).  
