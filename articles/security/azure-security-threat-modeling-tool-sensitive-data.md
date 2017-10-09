---
title: Azure Data - Microsoft Threat Modeling Tool - aaaSensitive | Microsoft Docs
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
ms.openlocfilehash: 8a18f43af439241ba193ccf668971ddc4655355f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-sensitive-data--mitigations"></a>Beveiliging Frame: Gevoelige gegevens | Oplossingen 
| Product/Service | Artikel |
| --------------- | ------- |
| **Een grens machine vertrouwensrelatie** | <ul><li>[Zorg ervoor dat de binaire bestanden worden verborgen als ze gevoelige informatie bevatten](#binaries-info)</li><li>[Houd rekening met het gebruikte tooprotect vertrouwelijke gebruikersspecifieke gegevens voor het gebruik van Encrypted File System (EFS) is](#efs-user)</li><li>[Zorg ervoor dat gevoelige gegevens die zijn opgeslagen door de toepassing hello op Hallo-bestandssysteem is versleuteld](#filesystem)</li></ul> | 
| **Webtoepassing** | <ul><li>[Zorg ervoor dat gevoelige inhoud is niet in de cache op Hallo-browser](#cache-browser)</li><li>[Secties van Web-App-configuratiebestanden met gevoelige gegevens versleutelen](#encrypt-data)</li><li>[Hallo automatisch aanvullen HTML-kenmerk in gevoelige formulieren en invoer expliciet uitschakelen](#autocomplete-input)</li><li>[Zorg ervoor dat gevoelige gegevens die worden weergegeven op het welkomstscherm van de gebruiker wordt gemaskeerd](#data-mask)</li></ul> | 
| **Database** | <ul><li>[Dynamische gegevens maskeren toolimit gevoelige gegevens blootstelling niet bevoegde gebruikers implementeren](#dynamic-users)</li><li>[Zorg ervoor dat de wachtwoorden worden opgeslagen in gezouten hash-indeling](#salted-hash)</li><li>[Zorg ervoor dat gevoelige gegevens in de databasekolommen worden versleuteld](#db-encrypted)</li><li>[Zorg ervoor dat versleuteling databaseniveau (TDE) is ingeschakeld](#tde-enabled)</li><li>[Ervoor zorgen dat databaseback-ups worden gecodeerd](#backup)</li></ul> | 
| **Web-API** | <ul><li>[Zorg ervoor dat gevoelige gegevens relevante tooWeb die API niet in de opslag van de browser opgeslagen wordt](#api-browser)</li></ul> | 
| Azure Documentdb | <ul><li>[Versleutelen van gevoelige gegevens die zijn opgeslagen in DocumentDB](#encrypt-docdb)</li></ul> | 
| **Vertrouwensgrenzen van Azure IaaS VM** | <ul><li>[Gebruik Azure Disk Encryption tooencrypt schijven gebruikt door virtuele Machines](#disk-vm)</li></ul> | 
| **Service Fabric-Vertrouwensgrenzen** | <ul><li>[Versleutelen van geheimen in Service Fabric-toepassingen](#fabric-apps)</li></ul> | 
| **Dynamics CRM** | <ul><li>[Beveiliging modellering uitvoeren en zakelijke eenheden/Teams gebruiken indien vereist](#modeling-teams)</li><li>[Beperken van toegang tooshare onderdeel op Kritiek entiteiten](#entities)</li><li>[Gebruikers van de trein op Hallo risico's van Hallo Dynamics CRM-Share-functie en goede beveiligingsprocedures](#good-practices)</li><li>[Een ontwikkeling standaarden regel met config details in Uitzonderingsbeheer proscribing opnemen](#exception-mgmt)</li></ul> | 
| **Azure Storage** | <ul><li>[Versleuteling van Azure Storage-Service (SSE) gebruiken voor Data-at-Rest (Preview)](#sse-preview)</li><li>[Versleuteling van de Client-Side toostore gevoelige gegevens in Azure Storage gebruiken](#client-storage)</li></ul> | 
| **Mobiele clients** | <ul><li>[Versleutelen van gevoelige of persoonlijke gegevens die zijn geschreven toophones lokale opslag](#pii-phones)</li><li>[Verbergen, gegenereerde binaire bestanden voordat u distribueert tooend gebruikers weergeven](#binaries-end)</li></ul> | 
| **WCF** | <ul><li>[Set clientCredentialType tooCertificate of Windows](#cert)</li><li>[WCF-beveiligingsmodus is niet ingeschakeld](#security)</li></ul> | 

## <a id="binaries-info"></a>Zorg ervoor dat de binaire bestanden worden verborgen als ze gevoelige informatie bevatten

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Een grens machine vertrouwensrelatie | 
| **SDL-fase**               | Implementatie |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | Zorg ervoor dat de binaire bestanden worden verborgen als ze gevoelige informatie zoals handelsgeheimen, vertrouwelijke zakelijke logica die moet worden niet omgekeerd bevatten. Dit is toostop reverse-engineering van assembly's. Hulpprogramma's zoals `CryptoObfuscator` kan worden gebruikt voor dit doel. |

## <a id="efs-user"></a>Houd rekening met het gebruikte tooprotect vertrouwelijke gebruikersspecifieke gegevens voor het gebruik van Encrypted File System (EFS) is

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Een grens machine vertrouwensrelatie | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | U kunt met behulp van Encrypted File System (EFS) zijn gebruikte tooprotect vertrouwelijke gebruikersspecifieke gegevens van tegenstanders met fysieke toegang toohello computer. |

## <a id="filesystem"></a>Zorg ervoor dat gevoelige gegevens die zijn opgeslagen door de toepassing hello op Hallo-bestandssysteem is versleuteld

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Een grens machine vertrouwensrelatie | 
| **SDL-fase**               | Implementatie |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | Ervoor zorgen dat gevoelige gegevens die zijn opgeslagen door de toepassing hello op Hallo-bestandssysteem is gecodeerd (bijvoorbeeld met behulp van DPAPI), als EFS kunnen niet worden afgedwongen. |

## <a id="cache-browser"></a>Zorg ervoor dat gevoelige inhoud is niet in de cache op Hallo-browser

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemeen, Web Forms, MVC5, MVC6 |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | Browsers kunnen gegevens voor de doeleinden van opslaan in cache en geschiedenis opslaan. Deze bestanden in de cache worden opgeslagen in een map, zoals de map van de tijdelijke internetbestanden Hallo in geval van Hallo van Internet Explorer. Wanneer deze pagina's opnieuw worden aangeduid, worden deze door Hallo browser uit de cache weergegeven. Als gevoelige informatie weergegeven toohello gebruiker (zoals hun adres, creditcardgegevens, sociaal-fiscaal nummer of gebruikersnaam), wordt deze informatie worden kan opgeslagen in de browser-cache en daarom worden opgehaald via Hallo browsercache onderzoeken of door op knop 'Terug' Hallo van de browser te drukken. Cache-control van antwoord headerwaarde te 'Nee-store' voor alle pagina's ingesteld. |

### <a name="example"></a>Voorbeeld
```XML
<configuration>
  <system.webServer>
   <httpProtocol>
    <customHeaders>
        <add name="Cache-Control" value="no-cache" />
        <add name="Pragma" value="no-cache" />
        <add name="Expires" value="-1" />
    </customHeaders>
  </httpProtocol>
 </system.webServer>
</configuration>
```

### <a name="example"></a>Voorbeeld
Dit kan worden geïmplementeerd door een filter. Voorbeeld van de volgende kan worden gebruikt: 
```C#
public override void OnActionExecuting(ActionExecutingContext filterContext)
        {
            if (filterContext == null || (filterContext.HttpContext != null && filterContext.HttpContext.Response != null && filterContext.HttpContext.Response.IsRequestBeingRedirected))
            {
                //// Since this is MVC pipeline, this should never be null.
                return;
            }

            var attributes = filterContext.ActionDescriptor.GetCustomAttributes(typeof(System.Web.Mvc.OutputCacheAttribute), false);
            if (attributes == null || **Attributes**.Count() == 0)
            {
                filterContext.HttpContext.Response.Cache.SetNoStore();
                filterContext.HttpContext.Response.Cache.SetCacheability(HttpCacheability.NoCache);
                filterContext.HttpContext.Response.Cache.SetExpires(DateTime.UtcNow.AddHours(-1));
                if (!filterContext.IsChildAction)
                {
                    filterContext.HttpContext.Response.AppendHeader("Pragma", "no-cache");
                }
            }

            base.OnActionExecuting(filterContext);
        }
``` 

## <a id="encrypt-data"></a>Secties van Web-App-configuratiebestanden met gevoelige gegevens versleutelen

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Procedure: Coderen configuratiesecties in ASP.NET 2.0 met behulp van DPAPI](https://msdn.microsoft.com/library/ff647398.aspx), [geven een Configuratieprovider beveiligd](https://msdn.microsoft.com/library/68ze1hb2.aspx), [met behulp van Azure Sleutelkluis tooprotect toepassing geheimen](https://azure.microsoft.com/documentation/articles/guidance-multitenant-identity-keyvault/) |
| **Stappen** | Configuratiebestanden zoals Hallo Web.config, appsettings.json zijn vaak toohold gevoelige gegevens, zoals gebruikersnamen, wachtwoorden, databaseverbindingsreeksen en versleutelingssleutels gebruikt. Als u deze informatie niet beveiligt, wordt de toepassing is kwetsbaar tooattackers of kwaadwillende gebruikers het verkrijgen van gevoelige informatie zoals gebruikersnamen en wachtwoorden, databasenamen en servernamen. Op basis van het implementatietype hello (azure/on-premises), versleutelen Hallo gevoelige secties van configuratiebestanden met DPAPI of services zoals Azure Sleutelkluis. |

## <a id="autocomplete-input"></a>Hallo automatisch aanvullen HTML-kenmerk in gevoelige formulieren en invoer expliciet uitschakelen

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [MSDN: automatisch aanvullen kenmerk](http://msdn.microsoft.com/library/ms533486(VS.85).aspx), [automatisch aanvullen gebruiken in HTML](http://msdn.microsoft.com/library/ms533032.aspx), [beveiligingslek in HTML opschoning](http://technet.microsoft.com/security/bulletin/MS10-071), [automatisch aanvullen., opnieuw?](http://blog.mindedsecurity.com/2011/10/autocompleteagain.html) |
| **Stappen** | Hallo automatisch aanvullen kenmerk geeft aan of een formulier automatisch aanvullen in- of uitschakelen hebben moet. Wanneer automatisch aanvullen ingeschakeld is, Hallo browser automatisch volledige waarden op basis van waarden die Hallo gebruiker heeft ingevoerd voordat. Bijvoorbeeld wanneer een nieuwe naam en het wachtwoord is ingevoerd in een formulier en Hallo formulier wordt ingediend, Hallo browser gevraagd als Hallo wachtwoord moet worden opgeslagen. Daarna wanneer Hallo formulier wordt weergegeven, Hallo naam en het wachtwoord worden automatisch ingevuld of zijn voltooid, zoals de naam van de Hallo is ingevoerd. Een aanvaller met lokale toegang kan krijgen van wachtwoord met ongecodeerde tekst hello uit de browsercache Hallo. Automatisch aanvullen is standaard ingeschakeld en moet expliciet worden uitgeschakeld. |

### <a name="example"></a>Voorbeeld
```C#
<form action="Login.aspx" method="post " autocomplete="off" >
      Social Security Number: <input type="text" name="ssn" />
      <input type="submit" value="Submit" />    
</form>
```

## <a id="data-mask"></a>Zorg ervoor dat gevoelige gegevens die worden weergegeven op het welkomstscherm van de gebruiker wordt gemaskeerd

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | Gevoelige gegevens, zoals wachtwoorden, creditcardnummers, enz. sofi-nummer moet worden gemaskeerd wanneer weergegeven op het welkomstscherm. Dit is niet-geautoriseerde tooprevent personeel toegang krijgen tot Hallo-gegevens (bijvoorbeeld schouder surfen wachtwoorden, ondersteuningspersoneel SSN aantallen gebruikers weergeven). Zorg ervoor dat de elementen van deze gegevens niet zichtbaar in tekst zonder opmaak zijn en op de juiste wijze worden gemaskeerd. Dit heeft toobe gezorgd terwijl ze worden geaccepteerd als invoer (zoals. input type = 'password') en het weergeven van terug op het welkomstscherm (bijvoorbeeld weergave alleen Hallo laatste 4 cijfers van het creditcardnummer hello). |

## <a id="dynamic-users"></a>Dynamische gegevens maskeren toolimit gevoelige gegevens blootstelling niet bevoegde gebruikers implementeren

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Database | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | SQL Azure, OnPrem |
| **Kenmerken**              | SQL-versie - V12, SQL-versie - MsSQL2016 |
| **Verwijzingen**              | [Maskering van dynamische gegevens](https://msdn.microsoft.com/library/mt130841) |
| **Stappen** | Hallo-doel van de dynamische-gegevensmaskering is toolimit blootstelling van gevoelige gegevens, voorkomen dat gebruikers die geen toegang tot toohello gegevens kunnen bekijken. Dynamische gegevensmaskering richt u niet tooprevent databasegebruikers toohello database rechtstreeks verbinding maken en u uitgebreide query's uitvoert die gevoelige gegevens Hallo blootstellen. Dynamische gegevensmaskering is aanvullende tooother beveiligingsfuncties in SQL Server (controle, versleuteling en beveiliging op rijniveau...) en het is raadzaam toouse deze functie in combinatie met deze bovendien in volgorde toobetter Hallo gevoelige gegevens beveiligen in Hallo de database. Houd er rekening mee dat deze functie wordt alleen ondersteund door SQL Server 2016 vanaf en Azure SQL Database. |

## <a id="salted-hash"></a>Zorg ervoor dat de wachtwoorden worden opgeslagen in gezouten hash-indeling

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Database | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Hashing van wachtwoord met .NET Crypto-API 's](http://docs.asp.net/en/latest/security/data-protection/consumer-apis/password-hashing.html) |
| **Stappen** | Wachtwoorden moeten niet worden opgeslagen in databases met aangepaste store. Wachtwoord-hashes moeten in plaats daarvan met salt waarden worden opgeslagen. Zorg ervoor dat Hallo salt voor Hallo gebruiker altijd uniek is en u b-crypt, s-crypt of PBKDF2 voordat tooeliminate Hallo mogelijkheid brute force opslaan Hallo-wachtwoord met een minimale werk factor herhaling telling van 150.000 lus.| 

## <a id="db-encrypted"></a>Zorg ervoor dat gevoelige gegevens in de databasekolommen worden versleuteld

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Database | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | SQL-versie - alle |
| **Verwijzingen**              | [Versleutelen van gevoelige gegevens in SQL server](https://technet.microsoft.com/library/ff848751(v=sql.105).aspx), [hoe: een kolom van de gegevens in SQL Server versleutelen](https://msdn.microsoft.com/library/ms179331), [coderen van certificaat](https://msdn.microsoft.com/library/ms188061) |
| **Stappen** | Gevoelige gegevens, zoals creditcardnummers heeft toobe versleuteld in Hallo-database. Gegevens kunnen worden versleuteld met behulp van versleuteling op kolomniveau of door de functie van een toepassing met behulp van Hallo versleuteling functies. |

## <a id="tde-enabled"></a>Zorg ervoor dat versleuteling databaseniveau (TDE) is ingeschakeld

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Database | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Transparent Data Encryption (TDE) voor informatie over SQL Server](https://technet.microsoft.com/library/bb934049(v=sql.105).aspx) |
| **Stappen** | Transparent Data Encryption (TDE) functie in SQL server helpt u bij het versleutelen van gevoelige gegevens in een database en Beveilig Hallo sleutels die gebruikte tooencrypt Hallo gegevens met een certificaat. Dit voorkomt dat iedereen zonder Hallo sleutels met behulp van Hallo-gegevens. TDE beschermt gegevens 'in rust', wat betekent dat de gegevens en logboekbestanden bestanden Hallo. Het biedt Hallo mogelijkheid toocomply veel wettelijke, en tot stand gebracht in verschillende branches richtlijnen. |

## <a id="backup"></a>Ervoor zorgen dat databaseback-ups worden gecodeerd

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Database | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | SQL Azure, OnPrem |
| **Kenmerken**              | SQL-versie - V12, SQL-versie - MsSQL2014 |
| **Verwijzingen**              | [SQL database-back-versleuteling](https://msdn.microsoft.com/library/dn449489) |
| **Stappen** | SQL Server heeft Hallo mogelijkheid tooencrypt Hallo gegevens tijdens het maken van een back-up. Door het versleutelingsalgoritme Hallo en Hallo encryptor (certificaten of asymmetrische sleutel) te geven wanneer u een back-up maakt, een gecodeerde back-upbestand kan worden gemaakt. |

## <a id="api-browser"></a>Zorg ervoor dat gevoelige gegevens relevante tooWeb die API niet in de opslag van de browser opgeslagen wordt

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Web-API | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | MVC 5, 6 MVC |
| **Kenmerken**              | ID-Provider - ADFS, identiteitsprovider - Azure AD |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | <p>In bepaalde implementaties verificatie voor gevoelige artefacten relevante tooWeb-API's worden opgeslagen in de lokale opslag van de browser. Bijvoorbeeld, zoals Azure AD authentication artefacten adal.idtoken, adal.nonce.idtoken, adal.access.token.key, adal.token.keys, adal.state.login, adal.session.state, adal.expiration.key enzovoort.</p><p>Alle deze artefacten beschikbaar, zelfs na het zijn afmelden of de browser wordt gesloten. Als een adversary toegang toothese artefacten krijgt, kan hij ze tooaccess Hallo beveiligde bronnen (API's) hergebruiken. Zorg ervoor dat alle gevoelige artefacten gerelateerde tooWeb API niet zijn opgeslagen in de opslag van de browser. In gevallen waarin de client-side '-opslag onvermijdelijk is (bijv, moet één pagina toepassingen (SPA) die gebruikmaken van de impliciete OpenIdConnect/OAuth stromen toostore toegangstokens lokaal), gebruik opslagopties met hebben geen persistentie. bijvoorbeeld, liefst SessionStorage tooLocalStorage.</p>| 

### <a name="example"></a>Voorbeeld
Hallo hieronder JavaScript-codefragment is afkomstig van een aangepaste verificatie-bibliotheek die verificatie artefacten in de lokale opslag opslaat. Deze implementaties moeten worden vermeden. 
```javascript
ns.AuthHelper.Authenticate = function () {
window.config = {
instance: 'https://login.microsoftonline.com/',
tenant: ns.Configurations.Tenant,
clientId: ns.Configurations.AADApplicationClientID,
postLogoutRedirectUri: window.location.origin,
cacheLocation: 'localStorage', // enable this for IE, as sessionStorage does not work for localhost.
};
```

## <a id="encrypt-docdb"></a>Versleutelen van gevoelige gegevens die zijn opgeslagen in Cosmos-DB

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Azure Documentdb | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | Versleutelen van gevoelige gegevens op toepassingsniveau voordat u ze opslaan in een document DB of dat geen gevoelige gegevens worden opgeslagen in andere opslagoplossingen zoals Azure Storage of Azure SQL| 

## <a id="disk-vm"></a>Gebruik Azure Disk Encryption tooencrypt schijven gebruikt door virtuele Machines

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Vertrouwensgrenzen van Azure IaaS VM | 
| **SDL-fase**               | Implementatie |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Met behulp van Azure Disk Encryption tooencrypt schijven gebruikt door uw virtuele machines](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_using-azure-disk-encryption-to-encrypt-disks-used-by-your-virtual-machines) |
| **Stappen** | <p>Azure Disk Encryption is een nieuwe functie die zich momenteel in preview. Deze functie kunt u tooencrypt Hallo OS schijven en gegevensschijven die wordt gebruikt door een virtuele Machine voor IaaS. Hallo stations zijn versleuteld met behulp van standaard-BitLocker-versleuteling technologie voor Windows. Hallo-schijven zijn versleuteld met behulp van technologie Hallo DM-Crypt voor Linux. Dit is geïntegreerd met Azure Key Vault tooallow u toocontrol en beheren van versleutelingssleutels Hallo-schijf. Hello Azure Disk Encryption-oplossing ondersteunt Hallo drie scenario's de versleuteling van klanten te volgen:</p><ul><li>Schakel versleuteling in op de nieuwe IaaS VM's die worden gemaakt op basis van de klant versleuteld VHD-bestanden en klant geleverde versleutelingssleutels die zijn opgeslagen in Azure Sleutelkluis.</li><li>Schakel versleuteling in op de nieuwe IaaS VM's die worden gemaakt op basis van hello Azure Marketplace.</li><li>Schakel versleuteling in op bestaande IaaS VM's al wordt uitgevoerd in Azure.</li></ul>| 

## <a id="fabric-apps"></a>Versleutelen van geheimen in Service Fabric-toepassingen

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Service Fabric-Vertrouwensgrenzen | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | Omgeving - Azure |
| **Verwijzingen**              | [Het beheren van geheimen in Service Fabric-toepassingen](https://azure.microsoft.com/documentation/articles/service-fabric-application-secret-management/) |
| **Stappen** | Geheimen mag gevoelige informatie, zoals de storage-verbindingsreeksen, wachtwoorden of andere waarden die niet moeten worden behandeld als tekst zonder opmaak. Gebruik Azure Key Vault toomanage sleutels en geheimen in service fabric-toepassingen. |

## <a id="modeling-teams"></a>Beveiliging modellering uitvoeren en zakelijke eenheden/Teams gebruiken indien vereist

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Dynamics CRM | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | Beveiliging modellering uitvoeren en zakelijke eenheden/Teams gebruiken indien vereist |

## <a id="entities"></a>Beperken van toegang tooshare onderdeel op Kritiek entiteiten

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Dynamics CRM | 
| **SDL-fase**               | Implementatie |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | Beperken van toegang tooshare onderdeel op Kritiek entiteiten |

## <a id="good-practices"></a>Gebruikers van de trein op Hallo risico's van Hallo Dynamics CRM-Share-functie en goede beveiligingsprocedures

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Dynamics CRM | 
| **SDL-fase**               | Implementatie |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | Gebruikers van de trein op Hallo risico's van Hallo Dynamics CRM-Share-functie en goede beveiligingsprocedures |

## <a id="exception-mgmt"></a>Een ontwikkeling standaarden regel met config details in Uitzonderingsbeheer proscribing opnemen

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Dynamics CRM | 
| **SDL-fase**               | Implementatie |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | Een regel voor het standaarden van ontwikkeling met config details in Uitzonderingsbeheer buiten ontwikkeling proscribing opnemen. Test voor deze als onderdeel van de beoordelingen code of periodieke controle.|

## <a id="sse-preview"></a>Versleuteling van Azure Storage-Service (SSE) gebruiken voor Data-at-Rest (Preview)

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Azure Storage | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | StorageType - Blob |
| **Verwijzingen**              | [Azure Storage-Service: versleuteling voor Data-at-Rest (Preview)](https://azure.microsoft.com/documentation/articles/storage-service-encryption/) |
| **Stappen** | <p>Azure Storage Service versleuteling (SSE) voor gegevens in rust helpt u bij het beveiligen en uw toomeet gegevens beveiligt uw organisatie beveiliging en naleving verplichtingen. Met deze functie van Azure Storage automatisch versleutelt uw gegevens voorafgaande toopersisting toostorage en ontsleutelt voorafgaande tooretrieval. Hallo versleuteling, ontsleuteling en sleutel is volledig transparant toousers. SSE geldt alleen tooblock blobs, pagina-blobs en toevoeg-blobs. Hallo wordt andere typen gegevens, waaronder tabellen, wachtrijen en -bestanden niet versleuteld.</p><p>Versleuteling en ontsleuteling werkstroom:</p><ul><li>Hallo klant schakelt u versleuteling op Hallo storage-account</li><li>Wanneer de klant Hallo schrijft nieuwe opslag van gegevens (Blob plaatsen, blok plaatsen, pagina plaatsen, enz.) tooBlob; elke schrijfbewerking is versleuteld met behulp van 256-bits AES-versleuteling, een Hallo sterkste blokcodering beschikbaar</li><li>Wanneer het Hallo-klant moet tooaccess gegevens (Blob ophalen, enzovoort), gegevens worden automatisch ontsleuteld voordat er wordt teruggekeerd toohello gebruiker</li><li>Als versleuteling is uitgeschakeld, nieuwe schrijfbewerkingen zijn niet langer gecodeerd en bestaande versleutelde gegevens blijven versleuteld totdat herschreven door Hallo-gebruiker. Terwijl versleuteling is ingeschakeld, worden schrijfbewerkingen tooBlob opslag wordt versleuteld. Hallo-status van de gegevens wijzigen niet met Hallo gebruiker schakelen tussen in-/ uitschakelen versleuteling voor Hallo storage-account</li><li>Alle versleutelingssleutels zijn opgeslagen, gecodeerd en beheerd door Microsoft</li></ul><p>Houd er rekening mee dat de sleutels voor versleuteling Hallo Hallo op dit moment worden beheerd door Microsoft. Microsoft oorspronkelijk Hallo sleutels genereert en veilige opslag Hallo Hallo-sleutels, evenals Hallo reguliere rotatie van beheren zoals gedefinieerd door intern beleid van Microsoft. In toekomstige hello, klanten krijgen Hallo mogelijkheid toomanage hun eigen > versleutelingssleutels, en geef het migratiepad van door Microsoft beheerde sleutels toocustomer beheerde sleutels.</p>| 

## <a id="client-storage"></a>Versleuteling van de Client-Side toostore gevoelige gegevens in Azure Storage gebruiken

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Azure Storage | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Client-Side-versleuteling en Azure Key Vault voor Microsoft Azure Storage](https://azure.microsoft.com/documentation/articles/storage-client-side-encryption/), [zelfstudie: blobs in Microsoft Azure Storage met Azure Key Vault versleutelen en ontsleutelen](https://azure.microsoft.com/documentation/articles/storage-encrypt-decrypt-blobs-key-vault/), [gegevens veilig opslaan in Azure Blob Opslag met versleuteling van Azure-extensies](https://blogs.msdn.microsoft.com/partnercatalystteam/2015/06/17/storing-data-securely-in-azure-blob-storage-with-azure-encryption-extensions/) |
| **Stappen** | <p>Hello Azure Storage-clientbibliotheek voor .NET-Nuget-pakket ondersteunt de versleuteling van gegevens binnen clienttoepassingen voordat tooAzure opslag uploaden en ontsleutelen van gegevens tijdens het downloaden van toohello client. Hallo-bibliotheek ondersteunt ook integratie met Azure Key Vault voor sleutelbeheer storage-account. Hier volgt een korte beschrijving van de werking van versleuteling aan de clientzijde:</p><ul><li>Hello Azure Storage client SDK genereert een inhoud versleutelingssleutel (CEK), die een symmetrische sleutel met een eenmalig gebruik</li><li>Gegevens van de klant is versleuteld met behulp van deze CEK</li><li>Hallo wordt CEK vervolgens verpakt (versleuteld) met de belangrijkste versleutelingssleutel hello (KEK-sleutel). Hallo KEK wordt aangeduid met een sleutel-id en een asymmetrisch sleutelpaar of een symmetrische sleutel en kan worden beheerd lokaal of opgeslagen in Azure Sleutelkluis. Hallo opslag client zichzelf heeft nooit toegang toohello KEK-sleutel. Het aanroept zojuist Hallo sleutel wrapping algoritme die wordt geleverd door Sleutelkluis. Klanten kunnen ervoor kiezen toouse aangepaste providers voor de sleutel als ze willen wrapping/uitpakken</li><li>Hallo versleutelde gegevens is vervolgens toohello Azure Storage-service geüpload. Hallo-koppelingen in Hallo verwijzingen sectie voor meer informatie op laag niveau implementatie controleren.</li></ul>|

## <a id="pii-phones"></a>Versleutelen van gevoelige of persoonlijke gegevens die zijn geschreven toophones lokale opslag

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Mobiele clients | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemeen, Xamarin  |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Instellingen en functies op uw apparaten met Microsoft Intune-beleid beheren](https://docs.microsoft.com/intune/deploy-use/manage-settings-and-features-on-your-devices-with-microsoft-intune-policies#create-a-configuration-policy), [sleutelhanger Valet](https://components.xamarin.com/view/square.valet) |
| **Stappen** | <p>Als de toepassing hello schrijft gevoelige informatie, zoals PII van gebruiker (e-mailadres, telefoonnummer, voornaam, achternaam, voorkeuren enz.) -in het bestandssysteem van mobile, waarna deze moet worden versleuteld voordat u het lokale bestandssysteem toohello schrijft. Als Hallo toepassing een bedrijfstoepassing, vervolgens publiceren met Windows Intune-toepassing hello mogelijkheid om te verkennen.</p>|

### <a name="example"></a>Voorbeeld
Intune kan worden geconfigureerd met de volgende security-beleid toosafeguard gevoelige gegevens: 
```C#
Require encryption on mobile device    
Require encryption on storage cards
Allow screen capture
```

### <a name="example"></a>Voorbeeld
Als het Hallo-toepassing is niet een zakelijke toepassing en klik vervolgens op gebruik platform opgegeven sleutelopslag, kunnen sleutelhangers toostore versleutelingssleutels met behulp van welke cryptografische bewerking worden uitgevoerd op Hallo-bestandssysteem. Na de code toont fragment hoe tooaccess sleutel uit sleutelhanger met xamarin: 
```C#
        protected static string EncryptionKey
        {
            get
            {
                if (String.IsNullOrEmpty(_Key))
                {
                    var query = new SecRecord(SecKind.GenericPassword);
                    query.Service = NSBundle.MainBundle.BundleIdentifier;
                    query.Account = "UniqueID";

                    NSData uniqueId = SecKeyChain.QueryAsData(query);
                    if (uniqueId == null)
                    {
                        query.ValueData = NSData.FromString(System.Guid.NewGuid().ToString());
                        var err = SecKeyChain.Add(query);
                        _Key = query.ValueData.ToString();
                    }
                    else
                    {
                        _Key = uniqueId.ToString();
                    }
                }

                return _Key;
            }
        }
```

## <a id="binaries-end"></a>Verbergen, gegenereerde binaire bestanden voordat u distribueert tooend gebruikers weergeven

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Mobiele clients | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Crypto codeversleuteling voor .net](http://www.ssware.com/cryptoobfuscator/obfuscator-net.htm) |
| **Stappen** | Gegenereerde binaire bestanden (assembly's in apk) moeten worden verborgen toostop reverse-engineering van assembly's. Hulpprogramma's zoals `CryptoObfuscator` kan worden gebruikt voor dit doel. |

## <a id="cert"></a>Set clientCredentialType tooCertificate of Windows

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | WCF | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | .NET framework 3 |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Voeg](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Stappen** | Met behulp van een UsernameToken via een niet-versleutelde kanaal met een wachtwoord als leesbare tekst beschrijft hello wachtwoord tooattackers die hello SOAP-berichten kunt netwerkhulpprogramma. Serviceproviders die gebruikmaken van Hallo UsernameToken mogelijk accepteren wachtwoorden als leesbare tekst verzonden. Hallo referentie tooattackers die Hallo SOAP-bericht kunt netwerkhulpprogramma kan worden blootgesteld ongecodeerde wachtwoorden via een niet-versleutelde kanaal te verzenden. | 

### <a name="example"></a>Voorbeeld
Hallo volgende providerconfiguratie van WCF-service gebruikt Hallo UsernameToken: 
```
<security mode="Message"> 
<message clientCredentialType="UserName" />
``` 
ClientCredentialType tooCertificate of Windows instellen. 

## <a id="security"></a>WCF-beveiligingsmodus is niet ingeschakeld

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | WCF | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemeen, .NET Framework 3 |
| **Kenmerken**              | Beveiliging modus - Transport, beveiligingsmodus - bericht |
| **Verwijzingen**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Koninkrijk Voeg](https://vulncat.fortify.com/en/vulncat/index.html), [basisprincipes van beveiliging WCF CoDe Magazine](http://www.codemag.com/article/0611051) |
| **Stappen** | Er is geen beveiliging transport of het bericht is gedefinieerd. Toepassingen die berichten zonder transport of bericht beveiliging kan niet worden gegarandeerd Hallo integriteit of vertrouwelijkheid van Hallo-berichten worden verzonden. Wanneer een binding van de beveiliging WCF is tooNone ingesteld, worden zowel transport en bericht-beveiliging uitgeschakeld. |

### <a name="example"></a>Voorbeeld
Hallo configuratiesets volgende Hallo beveiliging modus tooNone. 
```
<system.serviceModel> 
  <bindings> 
    <wsHttpBinding> 
      <binding name=""MyBinding""> 
        <security mode=""None""/> 
      </binding> 
  </bindings> 
</system.serviceModel> 
```

### <a name="example"></a>Voorbeeld
Beveiligingsmodus over alle servicebindingen er zijn vijf mogelijke beveiligingsmodi: 
* Geen. Beveiliging wordt uitgeschakeld. 
* Transport. Maakt gebruik van transport beveiliging voor wederzijdse verificatie en bericht-beveiliging. 
* Bericht. Maakt gebruik van berichtbeveiliging voor wederzijdse verificatie- en beveiliging. 
* Beide. Hiermee kunt u instellingen voor toosupply voor transport en bericht-beveiliging (alleen MSMQ ondersteunt dit). 
* TransportWithMessageCredential. Referenties worden doorgegeven met het Hallo-bericht en bericht-beveiliging en server-verificatie worden geleverd door de transportlaag Hallo. 
* TransportCredentialOnly. Clientreferenties met transportlaag Hallo worden doorgegeven en er geen bericht beveiliging wordt toegepast. Gebruik transport en het bericht beveiliging tooprotect Hallo integriteit en vertrouwelijkheid van berichten. Hallo configuratie hieronder weten Hallo service toouse transportbeveiliging met bericht referenties.
```
<system.serviceModel>
  <bindings>
    <wsHttpBinding>
    <binding name=""MyBinding""> 
    <security mode=""TransportWithMessageCredential""/> 
    <message clientCredentialType=""Windows""/> 
    </binding> 
  </bindings> 
</system.serviceModel> 
```
