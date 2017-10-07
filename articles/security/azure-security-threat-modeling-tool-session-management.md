---
title: aaaSession Azure Management - Microsoft Threat Modeling Tool - | Microsoft Docs
description: oplossingen voor bedreigingen die worden weergegeven in Hallo Threat Modeling hulpprogramma
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 915ffae3f775ca6902fcfb93e7e1952ce85612f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-session-management--articles"></a>Beveiliging Frame: Sessiebeheer | Artikelen 
| Product/Service | Artikel |
| --------------- | ------- |
| **Azure AD**    | <ul><li>[De juiste afmelding implementeren met behulp van ADAL methoden bij gebruik van Azure AD](#logout-adal)</li></ul> |
| IoT-apparaat | <ul><li>[Het gebruiken van beperkte levensduur voor gegenereerde SaS-tokens](#finite-tokens)</li></ul> |
| **Azure Documentdb** | <ul><li>[Minimale token levensduur voor tokens voor gegenereerde Resource gebruiken](#resource-tokens)</li></ul> |
| **ADFS** | <ul><li>[Juiste afmelding WsFederation methoden gebruiken wanneer u AD FS implementeren](#wsfederation-logout)</li></ul> |
| **Identiteitsserver** | <ul><li>[Implementeren in de juiste afmelden bij gebruik van Identiteitsserver](#proper-logout)</li></ul> |
| **Webtoepassing** | <ul><li>[Toepassingen die beschikbaar zijn via HTTPS moeten beveiligde cookies gebruiken](#https-secure-cookies)</li><li>[Alle HTTP-gebaseerde toepassing moet http alleen voor de definitie van de cookie opgeven](#cookie-definition)</li><li>[Beperken dat Cross-Site aanvragen kunnen worden vervalst (CSRF) aanvallen op ASP.NET-webpagina 's](#csrf-asp)</li><li>[Sessie voor inactiviteit levensduur instellen](#inactivity-lifetime)</li><li>[Juiste afmelden van de toepassing hello implementeren](#proper-app-logout)</li></ul> |
| **Web-API** | <ul><li>[Beperken dat Cross-Site aanvragen kunnen worden vervalst (CSRF) aanvallen op ASP.NET Web-API 's](#csrf-api)</li></ul> |

## <a id="logout-adal"></a>De juiste afmelding implementeren met behulp van ADAL methoden bij gebruik van Azure AD

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Azure AD | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | Als de toepassing hello vertrouwt op access token dat is uitgegeven door Azure AD, moet Hallo afmelding gebeurtenis-handler aanroepen |

### <a name="example"></a>Voorbeeld
```C#
HttpContext.GetOwinContext().Authentication.SignOut(OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType)
```

### <a name="example"></a>Voorbeeld
Het moet ook de gebruikerssessie door het aanroepen van methode Session.Abandon() vernietigen. Methode, ziet u beveiligde implementatie van de gebruiker afmelden in:
```C#
    [HttpPost]
        [ValidateAntiForgeryToken]
        public void LogOff()
        {
            string userObjectID = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
            AuthenticationContext authContext = new AuthenticationContext(Authority + TenantId, new NaiveSessionCache(userObjectID));
            authContext.TokenCache.Clear();
            Session.Clear();
            Session.Abandon();
            Response.SetCookie(new HttpCookie("ASP.NET_SessionId", string.Empty));
            HttpContext.GetOwinContext().Authentication.SignOut(
                OpenIdConnectAuthenticationDefaults.AuthenticationType,
                CookieAuthenticationDefaults.AuthenticationType);
        } 
```

## <a id="finite-tokens"></a>Het gebruiken van beperkte levensduur voor gegenereerde SaS-tokens

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | IoT-apparaat | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | SaS-tokens gegenereerd voor het verifiëren van tooAzure IoT Hub moeten een eindige verloopperiode hebben. Houd Hallo SaS token levensduur tooa minimale toolimit Hallo hoeveelheid tijd die kan worden cookies geval Hallo tokens worden getroffen.|

## <a id="resource-tokens"></a>Minimale token levensduur voor tokens voor gegenereerde Resource gebruiken

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Azure Documentdb | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | Reduceren timespan Hallo van resource token tooa voorgeschreven minimumwaarde. Resource-tokens hebben een geldige timespan standaardwaarde van 1 uur.|

## <a id="wsfederation-logout"></a>Juiste afmelding WsFederation methoden gebruiken wanneer u AD FS implementeren

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | ADFS | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | Als de toepassing hello STS token dat is uitgegeven door AD FS, moet Hallo afmelding gebeurtenis-handler WSFederationAuthenticationModule.FederatedSignOut() methode toolog uit Hallo gebruiker aanroepen. Ook Hallo huidige sessie moet worden vernietigd en Hallo token-outwaarde voor sessies te herstellen en geneutraliseerd.|

### <a name="example"></a>Voorbeeld
```C#
        [HttpPost, ValidateAntiForgeryToken]
        [Authorization]
        public ActionResult SignOut(string redirectUrl)
        {
            if (!this.User.Identity.IsAuthenticated)
            {
                return this.View("LogOff", null);
            }

            // Removes hello user profile.
            this.Session.Clear();
            this.Session.Abandon();
            HttpContext.Current.Response.Cookies.Add(new System.Web.HttpCookie("ASP.NET_SessionId", string.Empty)
                {
                    Expires = DateTime.Now.AddDays(-1D),
                    Secure = true,
                    HttpOnly = true
                });

            // Signs out at hello specified security token service (STS) by using hello WS-Federation protocol.
            Uri signOutUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Issuer);
            Uri replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm);
            if (!string.IsNullOrEmpty(redirectUrl))
            {
                replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm + redirectUrl);
            }
           //     Signs out of hello current session and raises hello appropriate events.
            var authModule = FederatedAuthentication.WSFederationAuthenticationModule;
            authModule.SignOut(false);
        //     Signs out at hello specified security token service (STS) by using hello WS-Federation
        //     protocol.            
            WSFederationAuthenticationModule.FederatedSignOut(signOutUrl, replyUrl);
            return new RedirectResult(redirectUrl);
        }
```

## <a id="proper-logout"></a>Implementeren in de juiste afmelden bij gebruik van Identiteitsserver

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Identiteitsserver | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [IdentityServer3 federatieve afmelden](https://identityserver.github.io/Documentation/docsv2/advanced/federated-signout.html) |
| **Stappen** | IdentityServer ondersteunt Hallo mogelijkheid toofederate met externe id-providers. Wanneer een gebruiker zich afmeldt een upstream-id-provider, kan afhankelijk van het Hallo-protocol gebruikt, dit worden mogelijk tooreceive een melding wanneer Hallo gebruiker zich afmeldt. Kunt u IdentityServer toonotify clients zodat ze kunnen ook zich Hallo gebruiker uit. Raadpleeg de documentatie Hallo in Hallo verwijzingen gedeelte voor het Hallo-implementatiegegevens.|

## <a id="https-secure-cookies"></a>Toepassingen die beschikbaar zijn via HTTPS moeten beveiligde cookies gebruiken

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | EnvironmentType - OnPrem |
| **Verwijzingen**              | [httpCookies Element (ASP.NET-instellingenschema)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx), [HttpCookie.Secure-eigenschap](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx) |
| **Stappen** | Cookies zijn normaal gesproken alleen toegankelijk toohello domein waarvoor ze zijn binnen het bereik. Helaas bevat Hallo definitie van 'domein' geen Hallo protocol zodat cookies die zijn gemaakt via HTTPS toegankelijk via HTTP zijn. Hallo "veilig" kenmerk geeft aan toohello browser die cookie Hallo alleen beschikbaar moet worden gesteld via HTTPS. Zorg dat alle cookies instellen via HTTPS Hallo gebruikt **beveiligde** kenmerk. Hallo-vereiste kan worden afgedwongen in Hallo web.config-bestand door Hallo requireSSL kenmerk tootrue instellen. Hallo benadering de voorkeur omdat deze Hallo zal geforceerd is **beveiligde** kenmerk voor alle huidige en toekomstige cookies zonder Hallo nodig toomake extra codewijzigingen.|

### <a name="example"></a>Voorbeeld
```C#
<configuration>
  <system.web>
    <httpCookies requireSSL="true"/>
  </system.web>
</configuration>
```
Hallo-instelling wordt afgedwongen, zelfs als HTTP gebruikte tooaccess Hallo-toepassing is. Als u HTTP gebruikt tooaccess Hallo toepassing, hello instelling einden Hallo toepassing omdat Hallo cookies worden ingesteld met Hallo beveiligde kenmerk en het Hallo-browser niet deze verstuurt back-toohello toepassing.

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Webformulieren, MVC5 |
| **Kenmerken**              | EnvironmentType - OnPrem |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | Wanneer Hallo-webtoepassing is Hallo Relying Party en Hallo IdP ADFS-server is, Hallo FedAuth-token van beveiligde kenmerk kan worden geconfigureerd met requireSSL tooTrue instellen in `system.identityModel.services` sectie van web.config:|

### <a name="example"></a>Voorbeeld
```C#
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:20:0" />
    ....  
    </federationConfiguration>
  </system.identityModel.services>
```

## <a id="cookie-definition"></a>Alle HTTP-gebaseerde toepassing moet http alleen voor de definitie van de cookie opgeven

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Beveiligde Cookie-kenmerk](https://en.wikipedia.org/wiki/HTTP_cookie#Secure_cookie) |
| **Stappen** | toomitigate hello gevaar voor openbaarmaking met een aanval cross-site scripting (XSS), een nieuw kenmerk - httpOnly - geïntroduceerd toocookies is en wordt ondersteund door alle belangrijke browsers. Hallo-kenmerk bevat een cookie is niet toegankelijk via script. Met behulp van cookies HttpOnly verkleint een webtoepassing Hallo kans dat gevoelige informatie in Hallo cookie kan worden gestolen via scripts en website tooan kwaadwillende persoon verzonden. |

### <a name="example"></a>Voorbeeld
Alle HTTP-gebaseerde toepassingen die gebruikmaken van cookies moeten HttpOnly opgeven in de definitie van de cookie hello, door het implementeren van na de configuratie in web.config:
```XML
<system.web>
.
.
   <httpCookies requireSSL="false" httpOnlyCookies="true"/>
.
.
</system.web>
```

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Web Forms |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [De eigenschap FormsAuthentication.RequireSSL](https://msdn.microsoft.com/library/system.web.security.formsauthentication.requiressl.aspx) |
| **Stappen** | Hallo RequireSSL eigenschapswaarde wordt ingesteld op Hallo-configuratiebestand voor een ASP.NET-toepassing met behulp van Hallo requireSSL kenmerk van het Hallo-configuratie-element. U kunt opgeven in Hallo Web.config-bestand voor uw ASP.NET-toepassing of SSL (Secure Sockets Layer) vereist tooreturn Hallo formulierverificatie cookie toohello server door instelling Hallo requireSSL kenmerk is.|

### <a name="example"></a>Voorbeeld 
Hallo stelt volgende codevoorbeeld Hallo requireSSL-kenmerk in Hallo Web.config-bestand.
```XML
<authentication mode="Forms">
  <forms loginUrl="member_login.aspx" cookieless="UseCookies" requireSSL="true"/>
</authentication>
```

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | MVC5 |
| **Kenmerken**              | EnvironmentType - OnPrem |
| **Verwijzingen**              | [Configuratie van Windows Identity Foundation (WIF) – deel II](https://blogs.msdn.microsoft.com/alikl/2011/02/01/windows-identity-foundation-wif-configuration-part-ii-cookiehandler-chunkedcookiehandler-customcookiehandler/) |
| **Stappen** | tooset httpOnly kenmerk voor FedAuth cookies, hideFromCsript kenmerkwaarde moet worden ingesteld tooTrue hebben. |

### <a name="example"></a>Voorbeeld
Volgende configuratie ziet u de juiste configuratie Hallo:
```XML
<federatedAuthentication>
<cookieHandler mode="Custom"
                       hideFromScript="true"
                       name="FedAuth"
                       path="/"
                       requireSsl="true"
                       persistentSessionLifetime="25">
</cookieHandler>
</federatedAuthentication>
```

## <a id="csrf-asp"></a>Beperken dat Cross-Site aanvragen kunnen worden vervalst (CSRF) aanvallen op ASP.NET-webpagina 's

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | Aanvraagvervalsing op meerdere sites (CSRF of XSRF) is een type van een aanval waarbij een aanvaller acties in de beveiligingscontext Hallo van vastgestelde sessie een andere gebruiker op een website kunt uitvoeren. Hallo-doel is toomodify of inhoud verwijderen als gerichte website Hallo afhankelijk is uitsluitend van cookies tooauthenticate ontvangen verzoek om sessie. Een aanvaller kan deze kwetsbaarheid misbruiken door een andere gebruiker browser tooload een URL met een opdracht van een kwetsbaar site waarop Hallo gebruiker is al aangemeld. Er zijn veel manieren voor een aanvaller toodo dat, zoals door het hosten van een andere website die wordt geladen een resource van kwetsbare Hallo-server of ophalen Hallo gebruiker tooclick een koppeling. Hallo-aanval kan worden voorkomen als Hallo-server stuurt de client van een extra token toohello, vereist Hallo client tooinclude dat token in alle toekomstige aanvragen en verifieert dat alle toekomstige aanvragen een token dat betrekking heeft toohello huidige sessie bevatten, zoals door met behulp van ASP.NET AntiForgeryToken Hallo of ViewState. |

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | MVC5, MVC6 |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [XSRF/CSRF voorkomen in ASP.NET MVC en webpagina 's](http://www.asp.net/mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages) |
| **Stappen** | Formulieren anti-CSRF en ASP.NET MVC - gebruik Hallo `AntiForgeryToken` Help-methode op weergaven; put een `Html.AntiForgeryToken()` in Hallo formulier, bijvoorbeeld:|

### <a name="example"></a>Voorbeeld
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
```

### <a name="example"></a>Voorbeeld
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a>Voorbeeld
Op Hallo dezelfde tijdstip, Html.AntiForgeryToken() biedt Hallo bezoeker een cookie aangeroepen __RequestVerificationToken Hello dezelfde als Hallo willekeurige verborgen waarde waarde hierboven weergegeven. Vervolgens voegt u toovalidate een binnenkomende Formulierbericht Hallo [ValidateAntiForgeryToken] filter toohello doel-actiemethode. Bijvoorbeeld:
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
Autorisatiefilter die of controleert:
* Hallo binnenkomende aanvraag heeft een cookie met de naam __RequestVerificationToken
* Hallo binnenkomende aanvraag heeft een `Request.Form` vermelding __RequestVerificationToken aangeroepen
* Deze cookie en `Request.Form` waarden overeenkomen, ervan uitgaande dat alle goed is, doorloopt NTDS Hallo-aanvraag die normaal werken. Maar als dit niet het geval is, klikt u vervolgens een Autorisatiefout met het bericht 'een vereiste anti-vervalsingstoken is niet opgegeven of is ongeldig'. 

### <a name="example"></a>Voorbeeld
Anti-CSRF en AJAX: Hallo formulier token kan een probleem voor AJAX-aanvragen worden, omdat een AJAX-aanvraag JSON-gegevens, geen HTML-formuliergegevens kan verzenden. Eén oplossing is toosend Hallo tokens in een aangepaste HTTP-header. Hallo volgende code gebruikt Razor syntaxis toogenerate Hallo tokens en vervolgens voegt Hallo tokens tooan AJAX-aanvraag. 
```C#
<script>
    @functions{
        public string TokenHeaderValue()
        {
            string cookieToken, formToken;
            AntiForgery.GetTokens(null, out cookieToken, out formToken);
            return cookieToken + ":" + formToken;                
        }
    }

    $.ajax("api/values", {
        type: "post",
        contentType: "application/json",
        data: {  }, // JSON data goes here
        dataType: "json",
        headers: {
            'RequestVerificationToken': '@TokenHeaderValue()'
        }
    });
</script>
```

### <a name="example"></a>Voorbeeld
Wanneer u Hallo aanvraag verwerkt, moet u Hallo tokens extraheren uit de aanvraagheader Hallo. Vervolgens roept Hallo AntiForgery.Validate methode toovalidate Hallo tokens. Hallo methode Validate genereert een uitzondering als Hallo tokens niet geldig zijn.
```C#
void ValidateRequestHeader(HttpRequestMessage request)
{
    string cookieToken = "";
    string formToken = "";

    IEnumerable<string> tokenHeaders;
    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
    {
        string[] tokens = tokenHeaders.First().Split(':');
        if (tokens.Length == 2)
        {
            cookieToken = tokens[0].Trim();
            formToken = tokens[1].Trim();
        }
    }
    AntiForgery.Validate(cookieToken, formToken);
}
```

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Web Forms |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Los het voordeel van ASP.NET ingebouwde functies tooFend uit Web-aanvallen](https://msdn.microsoft.com/library/ms972969.aspx#securitybarriers_topic2) |
| **Stappen** | CSRF aanvallen in het webformulier op basis van toepassingen kunnen worden verminderd door het instellen van ViewStateUserKey tooa willekeurige tekenreeks varieert voor elke gebruiker - gebruikers-ID of beter nog sessie-id. Sessie-ID is veel beter geschikt zijn voor een aantal technische en sociale oorzaken hebben, omdat een sessie-ID onvoorspelbare, is een time-out optreedt en varieert op basis van een gebruiker.|

### <a name="example"></a>Voorbeeld
Dit is Hallo-code die u nodig hebt toohave in alle pagina's:
```C#
void Page_Init (object sender, EventArgs e) {
   ViewStateUserKey = Session.SessionID;
   :
}
```

## <a id="inactivity-lifetime"></a>Sessie voor inactiviteit levensduur instellen

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [De eigenschap HttpSessionState.Timeout](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx) |
| **Stappen** | Sessietime-out vertegenwoordigt Hallo gebeurtenis voordoet wanneer een gebruiker niet voert geen actie op een website tijdens een interval van (gedefinieerd door de webserver). Hallo gebeurtenis aan serverzijde, Hallo Wijzigingsstatus van Hallo gebruiker sessie too'invalid' (bijvoorbeeld ' niet meer gebruikt') en Hallo web server toodestroy krijgt deze de instructie (verwijderen van alle gegevens die zijn opgenomen in de App). Hallo stelt volgende codevoorbeeld Hallo time-out sessie kenmerk too15 minuten in Hallo Web.config-bestand.|

### <a name="example"></a>Voorbeeld
'''XML-code <configuration> < system.web > <sessionState mode="InProc" cookieless="true" timeout="15" /> < /system.web ></configuration>
```

## <a id="threat-detection"></a>Enable Threat detection on Azure SQL
```

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Web Forms |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Element vormt voor verificatie (ASP.NET-instellingenschema)](https://msdn.microsoft.com/library/1d3t3c61(v=vs.100).aspx) |
| **Stappen** | Hallo Formulierverificatieticket cookie time-out too15 minuten instellen|

### <a name="example"></a>Voorbeeld
'''XML-code<forms  name=".ASPXAUTH" loginUrl="login.aspx"  defaultUrl="default.aspx" protection="All" timeout="15" path="/" requireSSL="true" slidingExpiration="true"/>
</forms>
```

| Title                   | Details      |
| ----------------------- | ------------ |
| **Component**               | Web Application | 
| **SDL Phase**               | Build |  
| **Applicable Technologies** | Web Forms, MVC5 |
| **Attributes**              | EnvironmentType - OnPrem |
| **References**              | [asdeqa](https://skf.azurewebsites.net/Mitigations/Details/wefr) |
| **Steps** | When hello web application is Relying Party and ADFS is hello STS, hello lifetime of hello authentication cookies - FedAuth tokens - can be set by hello following configuration in web.config:|

### Example
```XML
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:15:0" />
      <!-- Set requireHttps=true; -->
      <wsFederation passiveRedirectEnabled="true" issuer="http://localhost:39529/" realm="https://localhost:44302/" reply="https://localhost:44302/" requireHttps="true"/>
      <!--
      Use hello code below tooenable encryption-decryption of claims received from ADFS. Thumbprint value varies based on hello certificate being used.
      <serviceCertificate>
        <certificateReference findValue="4FBBBA33A1D11A9022A5BF3492FF83320007686A" storeLocation="LocalMachine" storeName="My" x509FindType="FindByThumbprint" />
      </serviceCertificate>
      -->
    </federationConfiguration>
  </system.identityModel.services>
```

### <a name="example"></a>Voorbeeld
Ook Hallo levensduur van token SAML-claim uitgegeven AD FS moet worden ingesteld op too15 minuten, door het uitvoeren van de volgende powershell-opdracht op de ADFS-server Hallo Hallo:
```C#
Set-ADFSRelyingPartyTrust -TargetName “<RelyingPartyWebApp>” -ClaimsProviderName @(“Active Directory”) -TokenLifetime 15 -AlwaysRequireAuthentication $true
```

## <a id="proper-app-logout"></a>Juiste afmelden van de toepassing hello implementeren

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | Uitvoeren juiste afmelden van de toepassing hello, als de gebruiker op drukt knop Afmelden. Bij het afmelden, moet toepassing vernietigen gebruikerssessie, en ook opnieuw instellen en cookie-outwaarde voor sessies, samen met opnieuw instellen en de waarde van de cookie verificatie nullifying ongeldig verklaard. Ook wanneer meerdere sessies gebonden tooa één gebruikersidentiteit zijn, moeten ze worden gezamenlijk afgesloten aan de serverzijde Hallo op time-out of meld u af. Ten slotte zorgen ervoor dat afmelding functionaliteit beschikbaar op elke pagina. |

## <a id="csrf-api"></a>Beperken dat Cross-Site aanvragen kunnen worden vervalst (CSRF) aanvallen op ASP.NET Web-API 's

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Web-API | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | Aanvraagvervalsing op meerdere sites (CSRF of XSRF) is een type van een aanval waarbij een aanvaller acties in de beveiligingscontext Hallo van vastgestelde sessie een andere gebruiker op een website kunt uitvoeren. Hallo-doel is toomodify of inhoud verwijderen als gerichte website Hallo afhankelijk is uitsluitend van cookies tooauthenticate ontvangen verzoek om sessie. Een aanvaller kan deze kwetsbaarheid misbruiken door een andere gebruiker browser tooload een URL met een opdracht van een kwetsbaar site waarop Hallo gebruiker is al aangemeld. Er zijn veel manieren voor een aanvaller toodo dat, zoals door het hosten van een andere website die wordt geladen een resource van kwetsbare Hallo-server of ophalen Hallo gebruiker tooclick een koppeling. Hallo-aanval kan worden voorkomen als Hallo-server stuurt de client van een extra token toohello, vereist Hallo client tooinclude dat token in alle toekomstige aanvragen en verifieert dat alle toekomstige aanvragen een token dat betrekking heeft toohello huidige sessie bevatten, zoals door met behulp van ASP.NET AntiForgeryToken Hallo of ViewState. |

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Web-API | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | MVC5, MVC6 |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Het voorkomen van Aanvraagvervalsing op meerdere sites (CSRF) aanvallen in ASP.NET Web-API](http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks) |
| **Stappen** | Anti-CSRF en AJAX: Hallo formulier token kan een probleem voor AJAX-aanvragen worden, omdat een AJAX-aanvraag JSON-gegevens, geen HTML-formuliergegevens kan verzenden. Eén oplossing is toosend Hallo tokens in een aangepaste HTTP-header. Hallo volgende code gebruikt Razor syntaxis toogenerate Hallo tokens en vervolgens voegt Hallo tokens tooan AJAX-aanvraag. |

### <a name="example"></a>Voorbeeld
```Javascript
<script>
    @functions{
        public string TokenHeaderValue()
        {
            string cookieToken, formToken;
            AntiForgery.GetTokens(null, out cookieToken, out formToken);
            return cookieToken + ":" + formToken;                
        }
    }
    $.ajax("api/values", {
        type: "post",
        contentType: "application/json",
        data: {  }, // JSON data goes here
        dataType: "json",
        headers: {
            'RequestVerificationToken': '@TokenHeaderValue()'
        }
    });
</script>
```

### <a name="example"></a>Voorbeeld
Wanneer u Hallo aanvraag verwerkt, moet u Hallo tokens extraheren uit de aanvraagheader Hallo. Vervolgens roept Hallo AntiForgery.Validate methode toovalidate Hallo tokens. Hallo methode Validate genereert een uitzondering als Hallo tokens niet geldig zijn.
```C#
void ValidateRequestHeader(HttpRequestMessage request)
{
    string cookieToken = "";
    string formToken = "";

    IEnumerable<string> tokenHeaders;
    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
    {
        string[] tokens = tokenHeaders.First().Split(':');
        if (tokens.Length == 2)
        {
            cookieToken = tokens[0].Trim();
            formToken = tokens[1].Trim();
        }
    }
    AntiForgery.Validate(cookieToken, formToken);
}
```

### <a name="example"></a>Voorbeeld
Anti-CSRF en formulieren in ASP.NET MVC - gebruik Hallo AntiForgeryToken Help-methode op weergaven; bijvoorbeeld, een Html.AntiForgeryToken() in Hallo formulier plaatsen
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
}
```

### <a name="example"></a>Voorbeeld
Hallo in bovenstaand voorbeeld wordt ongeveer de volgende Hallo uitvoer:
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a>Voorbeeld
Op Hallo dezelfde tijdstip, Html.AntiForgeryToken() biedt Hallo bezoeker een cookie aangeroepen __RequestVerificationToken Hello dezelfde als Hallo willekeurige verborgen waarde waarde hierboven weergegeven. Vervolgens voegt u toovalidate een binnenkomende Formulierbericht Hallo [ValidateAntiForgeryToken] filter toohello doel-actiemethode. Bijvoorbeeld:
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
Autorisatiefilter die of controleert:
* Hallo binnenkomende aanvraag heeft een cookie met de naam __RequestVerificationToken
* Hallo binnenkomende aanvraag heeft een `Request.Form` vermelding __RequestVerificationToken aangeroepen
* Deze cookie en `Request.Form` waarden overeenkomen, ervan uitgaande dat alle goed is, doorloopt NTDS Hallo-aanvraag die normaal werken. Maar als dit niet het geval is, klikt u vervolgens een Autorisatiefout met het bericht 'een vereiste anti-vervalsingstoken is niet opgegeven of is ongeldig'.

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Web-API | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | MVC5, MVC6 |
| **Kenmerken**              | ID-Provider - ADFS, identiteitsprovider - Azure AD |
| **Verwijzingen**              | [Een Web-API met afzonderlijke Accounts en lokale aanmelding in ASP.NET Web-API 2.2 beveiligen](http://www.asp.net/web-api/overview/security/individual-accounts-in-web-api) |
| **Stappen** | Als het Hallo-Web-API is beveiligd met OAuth 2.0, wordt verwacht bearer-token in autorisatie-aanvraag-header en verleent toegangsaanvraag toohello alleen als het Hallo-token is geldig. In tegenstelling tot op basis van Cookieverificatie, worden Hallo bearer-tokens toorequests in browsers niet koppelen. Hallo vraagt de client moet tooexplicitly hello bearer-token in de aanvraagheader Hallo koppelen. Daarom voor ASP.NET Web API's beveiligd met OAuth 2.0-bearer-tokens worden beschouwd als bij de bescherming tegen aanvallen CSRF. Houd er rekening mee dat als Hallo MVC-gedeelte van de toepassing hello formulierverificatie (dat wil zeggen, maakt gebruik van cookies) gebruikt, ter voorkoming tokens toobe die wordt gebruikt door Hallo MVC-web-app hebt. |

### <a name="example"></a>Voorbeeld
Hallo-Web-API heeft toobe op de hoogte toorely alleen op bearer-tokens en niet op cookies. Het kan worden gedaan door de configuratie in de volgende Hallo `WebApiConfig.Register` methode: '''C-Sharp code config. SuppressDefaultHostAuthentication(); configuratie. Filters.Add (nieuwe HostAuthenticationFilter(OAuthDefaults.AuthenticationType));
```
hello SuppressDefaultHostAuthentication method tells Web API tooignore any authentication that happens before hello request reaches hello Web API pipeline, either by IIS or by OWIN middleware. That way, we can restrict Web API tooauthenticate only using bearer tokens.
