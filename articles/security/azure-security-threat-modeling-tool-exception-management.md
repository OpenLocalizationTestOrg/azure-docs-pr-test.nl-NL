---
title: aaaException Azure Management - Microsoft Threat Modeling Tool - | Microsoft Docs
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
ms.openlocfilehash: 247096c10deeca94ebb9b19df7ba60e442ca1e4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-exception-management--mitigations"></a>Beveiliging Frame: Uitzonderingsbeheer | Oplossingen 
| Product/Service | Artikel |
| --------------- | ------- |
| **WCF** | <ul><li>[WCF - Do serviceDebug knooppunt niet opgenomen in het configuratiebestand](#servicedebug)</li><li>[WCF - Do serviceMetadata knooppunt niet opgenomen in het configuratiebestand](#servicemetadata)</li></ul> |
| **Web-API** | <ul><li>[Zorg ervoor dat de juiste uitzonderingsverwerking in ASP.NET Web API is uitgevoerd](#exception)</li></ul> |
| **Webtoepassing** | <ul><li>[Informatie over de beveiliging in foutberichten niet zichtbaar](#messages)</li><li>[Standaard-fout tijdens het verwerken van pagina implementeren](#default)</li><li>[Implementatiemethode tooRetail instellen in IIS](#deployment)</li><li>[Uitzonderingen zou moeten veilig mislukken](#fail)</li></ul> |

## <a id="servicedebug"></a>WCF - Do serviceDebug knooppunt niet opgenomen in het configuratiebestand

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | WCF | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemeen, NET Framework 3 |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Voeg Koninkrijk](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Stappen** | Framework WCF (Windows Communication) services kunnen de geconfigureerde tooexpose foutopsporingsgegevens zijn. Fouten opsporen informatie mag niet worden gebruikt in een productieomgeving. Hallo `<serviceDebug>` tag definieert of functie Hallo debug-gegevens voor een WCF-service is ingeschakeld. Als Hallo kenmerk includeExceptionDetailInFaults is tootrue ingesteld, wordt uitzonderingsinformatie van de toepassing hello tooclients worden geretourneerd. Aanvallers kunnen gebruikmaken van Hallo aanvullende informatie ze krijgen uit de uitvoer toomount aanvallen gericht op Hallo framework, database of andere resources gebruikt door de toepassing hello foutopsporing. |

### <a name="example"></a>Voorbeeld
Hallo volgende configuratiebestand bevat Hallo `<serviceDebug>` tag: 
```
<configuration> 
<system.serviceModel> 
<behaviors> 
<serviceBehaviors> 
<behavior name=""MyServiceBehavior""> 
<serviceDebug includeExceptionDetailInFaults=""True"" httpHelpPageEnabled=""True""/> 
... 
```
Informatie voor foutopsporing in Hallo service uitschakelen. Kan dit worden bereikt door het verwijderen van Hallo `<serviceDebug>` tag uit het configuratiebestand van uw toepassing. 

## <a id="servicemetadata"></a>WCF - Do serviceMetadata knooppunt niet opgenomen in het configuratiebestand

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | WCF | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | Algemeen, NET Framework 3 |
| **Verwijzingen**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Voeg Koninkrijk](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Stappen** | Informatie over een service openbaar vrijgeeft, kan aanvallers waardevolle inzicht in hoe ze Hallo-service kunnen misbruiken bieden. Hallo `<serviceMetadata>` code kan publicatiefunctie Hallo-metagegevens. Metagegevens van de service kan gevoelige gegevens bevatten die niet moet openbaar toegankelijk zijn. Ten minste staan alleen vertrouwde gebruikers tooaccess Hallo metagegevens en zorg ervoor dat onnodige informatie is niet beschikbaar gemaakt. Volledig uitschakelen nog beter Hallo mogelijkheid toopublish metagegevens. Een veilige WCF-configuratie bevat geen Hallo `<serviceMetadata>` label. |

## <a id="exception"></a>Zorg ervoor dat de juiste uitzonderingsverwerking in ASP.NET Web API is uitgevoerd

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Web-API | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | MVC 5, 6 MVC |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Afhandeling van uitzonderingen in ASP.NET Web API](http://www.asp.net/web-api/overview/error-handling/exception-handling), [Model validatie in ASP.NET-Web-API](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api) |
| **Stappen** | Standaard worden meest niet-onderschepte uitzonderingen in ASP.NET Web API vertaald in een HTTP-antwoord met de statuscode`500, Internal Server Error`|

### <a name="example"></a>Voorbeeld
toocontrol Hallo-statuscode geretourneerd door Hallo API, `HttpResponseException` kan worden gebruikt, zoals hieronder wordt weergegeven: 
```C#
public Product GetProduct(int id)
{
    Product item = repository.Get(id);
    if (item == null)
    {
        throw new HttpResponseException(HttpStatusCode.NotFound);
    }
    return item;
}
```

### <a name="example"></a>Voorbeeld
Voor verdere besturingselement in het antwoord van de uitzondering Hallo Hallo `HttpResponseMessage` klasse kan worden gebruikt, zoals hieronder wordt weergegeven: 
```C#
public Product GetProduct(int id)
{
    Product item = repository.Get(id);
    if (item == null)
    {
        var resp = new HttpResponseMessage(HttpStatusCode.NotFound)
        {
            Content = new StringContent(string.Format("No product with ID = {0}", id)),
            ReasonPhrase = "Product ID Not Found"
        }
        throw new HttpResponseException(resp);
    }
    return item;
}
```
toocatch onverwerkte uitzonderingen die niet van het type Hallo `HttpResponseException`, uitzondering Filters kunnen worden gebruikt. Uitzondering filters implementeren Hallo `System.Web.Http.Filters.IExceptionFilter` interface. Hallo eenvoudigste manier toowrite een uitzonderingsfilter wordt tooderive van Hallo `System.Web.Http.Filters.ExceptionFilterAttribute` klasse en Hallo OnException methode overschrijven. 

### <a name="example"></a>Voorbeeld
Hier volgt een filter dat wordt geconverteerd `NotImplementedException` uitzonderingen in de HTTP-statuscode `501, Not Implemented`: 
```C#
namespace ProductStore.Filters
{
    using System;
    using System.Net;
    using System.Net.Http;
    using System.Web.Http.Filters;

    public class NotImplExceptionFilterAttribute : ExceptionFilterAttribute 
    {
        public override void OnException(HttpActionExecutedContext context)
        {
            if (context.Exception is NotImplementedException)
            {
                context.Response = new HttpResponseMessage(HttpStatusCode.NotImplemented);
            }
        }
    }
}
```

Er zijn verschillende manieren tooregister een uitzonderingsfilter Web-API:
- Door de actie
- Door de netwerkcontroller
- Globaal

### <a name="example"></a>Voorbeeld
tooapply hello tooa specifieke actie filteren, Hallo-filter toevoegen als een kenmerk toohello actie: 
```C#
public class ProductsController : ApiController
{
    [NotImplExceptionFilter]
    public Contact GetContact(int id)
    {
        throw new NotImplementedException("This method is not implemented");
    }
}
```
### <a name="example"></a>Voorbeeld
tooapply hello filter tooall Hallo acties op een `controller`, Hallo-filter toevoegen als een kenmerk toohello `controller` klasse: 

```C#
[NotImplExceptionFilter]
public class ProductsController : ApiController
{
    // ...
}
```

### <a name="example"></a>Voorbeeld
tooapply Hallo filteren globaal tooall Web API-controllers, Voeg een exemplaar van Hallo filter toohello `GlobalConfiguration.Configuration.Filters` verzameling. Uitzondering filters in deze verzameling toepassen tooany Web API-controller actie. 
```C#
GlobalConfiguration.Configuration.Filters.Add(
    new ProductStore.NotImplExceptionFilterAttribute());
```

### <a name="example"></a>Voorbeeld
Voor de validatie, kan de Hallo modelstatus worden doorgegeven aan tooCreateErrorResponse methode, zoals hieronder wordt weergegeven: 
```C#
public HttpResponseMessage PostProduct(Product item)
{
    if (!ModelState.IsValid)
    {
        return Request.CreateErrorResponse(HttpStatusCode.BadRequest, ModelState);
    }
    // Implementation not shown...
}
```

Hallo-koppelingen in Hallo verwijzingen gedeelte voor meer informatie over het afhandelen van uitzonderlijke en modelvalidatie van het in ASP.Net Web API controleren 

## <a id="messages"></a>Informatie over de beveiliging in foutberichten niet zichtbaar

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | <p>Algemene foutberichten worden verstrekt rechtstreeks toohello gebruiker zonder met inbegrip van gegevens voor gevoelige toepassingen. Voorbeelden van gevoelige gegevens omvatten:</p><ul><li>Namen van server</li><li>Verbindingsreeksen</li><li>Gebruikersnamen</li><li>Wachtwoorden</li><li>SQL-procedures</li><li>Details van dynamische SQL-fouten</li><li>Stack-trace en de regels van code</li><li>Variabelen die zijn opgeslagen in het geheugen</li><li>Station en de map locaties</li><li>Toepassing installeren punten</li><li>Host-configuratie-instellingen</li><li>Andere details interne toepassing</li></ul><p>Alle fouten in een toepassing onderscheppen en algemene foutberichten bieden, evenals aangepaste fouten in IIS inschakelen wordt voorkomen dat openbaarmaking van informatie. SQL Server-database en .NET-uitzonderingen afhandelt, onder andere foutafhandeling architecturen, zijn vooral uitgebreide en zeer nuttige tooa kwaadwillende gebruiker profileren van uw toepassing. Voer niet direct weergegeven Hallo inhoud van een klasse is afgeleid van Hallo .NET uitzonderingsklasse en zorg ervoor dat de juiste uitzonderingsverwerking hebben zodat een onverwachte uitzondering per ongeluk wordt niet gegenereerd rechtstreeks toohello gebruiker.</p><ul><li>Geef algemene foutberichten rechtstreeks toohello-gebruiker die abstracte opslag specifieke gegevens rechtstreeks in het Hallo-bericht van uitzondering/fout</li><li>Geen weergave Hallo inhoud van een .NET-uitzondering klasse rechtstreeks toohello gebruiker</li><li>Alle foutberichten afvangen en indien van toepassing hello gebruiker via een algemene fout bericht verzonden toohello toepassingsclient informeren</li><li>Hallo-inhoud van hello uitzonderingsklasse niet blootstellen direct toohello gebruiker, met name Hallo retourwaarde van `.ToString()`, of Hallo-waarden van Hallo-bericht of StackTrace eigenschappen. Veilig Meld deze informatie en een meer onschuldig bericht toohello gebruiker weergeven</li></ul>|

## <a id="default"></a>Standaard-fout tijdens het verwerken van pagina implementeren

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Dialoogvenster voor instellingen van ASP.NET-foutpagina's bewerken](https://technet.microsoft.com/library/dd569096(WS.10).aspx) |
| **Stappen** | <p>Wanneer een ASP.NET-toepassing mislukt en zorgt ervoor dat een HTTP/1.x 500 Interne serverfout opgetreden of de configuratie van een onderdeel (zoals Aanvraagfiltering) voorkomt dat een pagina worden weergegeven, kunt u een foutbericht wordt gegenereerd. Beheerders kunnen kiezen of Hallo toepassing een bericht toohello client, gedetailleerde fout bericht toohello client of gedetailleerde fout bericht toolocalhost alleen moet worden weergegeven. Hallo <customErrors> -label in het bestand web.config Hallo heeft drie beschikbare modi:</p><ul><li>**Op:** geeft aan dat de aangepaste fouten zijn ingeschakeld. Als geen kenmerk defaultRedirect is opgegeven, zien gebruikers een algemene fout. Hallo aangepaste fouten worden weergegeven toohello externe clients en de lokale host toohello</li><li>**Uit:** geeft aan dat de aangepaste fouten zijn uitgeschakeld. Hallo worden gedetailleerde ASP.NET-fouten weergegeven toohello externe clients en de lokale host toohello</li><li>**RemoteOnly:** geeft aan dat aangepaste fouten alleen toohello externe clients worden weergegeven, en dat fouten in ASP.NET toohello lokale host worden weergegeven. Dit is de standaardwaarde Hallo</li></ul><p>Open Hallo `web.config` voor toepassing hello/site en zorg ervoor dat Hallo-label een heeft `<customErrors mode="RemoteOnly" />` of `<customErrors mode="On" />` gedefinieerd.</p>|

## <a id="deployment"></a>Implementatiemethode tooRetail instellen in IIS

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Implementatie |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [implementatie-Element (ASP.NET-instellingenschema)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx) |
| **Stappen** | <p>Hallo `<deployment retail>` switch is bedoeld voor gebruik door IIS productieservers. Dit is de schakeloptie gebruikte toohelp toepassingen worden uitgevoerd met de best mogelijke prestaties Hallo en zo weinig mogelijk beveiligingsgegevens lekken door het uitschakelen van de toepassing mogelijkheid toogenerate traceringsuitvoer op een pagina uitschakelen Hallo mogelijkheid toodisplay Hallo gedetailleerde fout fouten opsporen switch berichten tooend gebruikers en Hallo uit te schakelen.</p><p>Opties die ontwikkelaars zijn gericht, zijn zoals is mislukt, switches en vaak aanvragen tracering en foutopsporing zijn ingeschakeld tijdens het ontwikkelen van active. Het verdient aanbeveling dat Hallo implementatiemethode op een productieserver tooretail wordt ingesteld. Hallo machine.config-bestand te openen en zorg ervoor dat `<deployment retail="true" />` ingesteld tootrue blijft.</p>|

## <a id="fail"></a>Uitzonderingen zou moeten veilig mislukken

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Veilig mislukt](https://www.owasp.org/index.php/Fail_securely) |
| **Stappen** | Toepassing zou moeten veilig mislukken. Elke methode waarbij een Booleaanse waarde retourneert, op basis van welke bepaalde besluit wordt gemaakt, hebt uitzonderingsblok zorgvuldig gemaakt. Er zijn veel logische fouten vanwege toowhich beveiliging problemen kneep in wanneer Hallo uitzonderingsblok ondoordacht is geschreven.|

### <a name="example"></a>Voorbeeld
```C#
        public static bool ValidateDomain(string pathToValidate, Uri currentUrl)
        {
            try
            {
                if (!string.IsNullOrWhiteSpace(pathToValidate))
                {
                    var domain = RetrieveDomain(currentUrl);
                    var replyPath = new Uri(pathToValidate);
                    var replyDomain = RetrieveDomain(replyPath);

                    if (string.Compare(domain, replyDomain, StringComparison.OrdinalIgnoreCase) != 0)
                    {
                        //// Adding additional check tooenable CMS urls if they are not hosted on same domain.
                        if (!string.IsNullOrWhiteSpace(Utilities.CmsBase))
                        {
                            var cmsDomain = RetrieveDomain(new Uri(Utilities.Base.Trim()));
                            if (string.Compare(cmDomain, replyDomain, StringComparison.OrdinalIgnoreCase) != 0)
                            {
                                return false;
                            }
                            else
                            {
                                return true;
                            }
                        }

                        return false;
                    }
                }

                return true;
            }
            catch (UriFormatException ex)
            {
                LogHelper.LogException("Utilities:ValidateDomain", ex);
                return true;
            }
        }
```
Hallo hierboven methode retourneert True, wordt altijd als een uitzondering gebeurt. Als de eindgebruiker Hallo een verkeerd ingedeelde URL biedt, die browser respecteert Hallo, maar Hallo `Uri()` constructor niet, dit wordt Veroorzaak een exception en Hallo slachtoffer toohello geldig, maar een verkeerd ingedeelde URL worden uitgevoerd. 
