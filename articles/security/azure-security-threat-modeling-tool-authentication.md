---
title: -Microsoft Threat Modeling Tool - aaaAuthentication Azure | Microsoft Docs
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
ms.openlocfilehash: 06c1b1aebab25e6fb5b666d24ecd9d86085d656c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-authentication--mitigations"></a>Beveiliging Frame: Verificatie | Oplossingen 
| Product/Service | Artikel |
| --------------- | ------- |
| **Webtoepassing**    | <ul><li>[Overweeg het gebruik van een standaard verificatie mechanisme tooauthenticate tooWeb toepassing](#standard-authn-web-app)</li><li>[Toepassingen moeten veilig mislukte verificatiepogingen scenario's verwerken](#handle-failed-authn)</li><li>[Stap up inschakelen of adaptieve verificatie](#step-up-adaptive-authn)</li><li>[Zorg ervoor dat administratieve interfaces op de juiste wijze zijn vergrendeld](#admin-interface-lockdown)</li><li>[Implementeer vergeten wachtwoord functionaliteiten veilig](#forgot-pword-fxn)</li><li>[Zorg ervoor dat de wachtwoord- en -beleid worden toegepast](#pword-account-policy)</li><li>[Implementeer besturingselementen tooprevent gebruikersnaam opsomming](#controls-username-enum)</li></ul> |
| **Database** | <ul><li>[Gebruik zo mogelijk Windows-verificatie voor het verbinden van tooSQL Server](#win-authn-sql)</li><li>[Gebruik zo mogelijk Azure Active Directory-verificatie voor tooSQL verbinding maakt met Database](#aad-authn-sql)</li><li>[SQL-verificatiemodus wordt gebruikt, zorg er bij dat account en wachtwoord beleid worden afgedwongen op SQL server](#authn-account-pword)</li><li>[Gebruik geen SQL-verificatie in ingesloten databases](#autn-contained-db)</li></ul> |
| **Azure Event Hub** | <ul><li>[Per apparaat referenties voor verificatie met behulp van SaS-tokens worden gebruikt](#authn-sas-tokens)</li></ul> |
| **Vertrouwensgrenzen van Azure** | <ul><li>[Azure multi-factor Authentication voor beheerders voor Azure inschakelen](#multi-factor-azure-admin)</li></ul> |
| **Service Fabric-Vertrouwensgrenzen** | <ul><li>[Anonieme toegang tooService Fabric-Cluster beperken](#anon-access-cluster)</li><li>[Zorg ervoor dat Service Fabric-clientknooppunt certificaat verschilt van het knooppunt naar certificaat](#fabric-cn-nn)</li><li>[Gebruik AAD tooauthenticate clients tooservice fabric-clusters](#aad-client-fabric)</li><li>[Zorg ervoor dat service fabric-certificaten van een erkende certificeringsinstantie (CA) worden verkregen](#fabric-cert-ca)</li></ul> |
| **Identiteitsserver** | <ul><li>[Gebruik standaard verificatie scenario's ondersteund door Identiteitsserver](#standard-authn-id)</li><li>[Hallo standaard Identiteitsserver tokencache met een schaalbare alternatief overschrijven](#override-token)</li></ul> |
| **Een grens machine vertrouwensrelatie** | <ul><li>[Zorg ervoor dat de binaire bestanden van geïmplementeerde toepassingen digitaal zijn ondertekend](#binaries-signed)</li></ul> |
| **WCF** | <ul><li>[-Verificatie inschakelen wanneer u verbinding maakt tooMSMQ wachtrijen in WCF](#msmq-queues)</li><li>[WCF-Do bericht clientCredentialType toonone niet ingesteld](#message-none)</li><li>[WCF-Do Transport clientCredentialType toonone niet ingesteld](#transport-none)</li></ul> |
| **Web-API** | <ul><li>[Zorg ervoor dat standaard authenticatietechnieken gebruikte toosecure Web-API 's](#authn-secure-api)</li></ul> |
| **Azure AD** | <ul><li>[Gebruik standaard verificatie scenario's ondersteund door Azure Active Directory](#authn-aad)</li><li>[Hallo standaard ADAL tokencache met een schaalbare alternatief overschrijven](#adal-scalable)</li><li>[Zorg ervoor dat TokenReplayCache gebruikte tooprevent Hallo replay van tokens voor ADAL-verificatie](#tokenreplaycache-adal)</li><li>[Gebruik ADAL-bibliotheken toomanage token-aanvragen van OAuth2 clients tooAAD (of on-premises AD)](#adal-oauth2)</li></ul> |
| **Veld IoT Gateway** | <ul><li>[Apparaten die verbinding maken toohello Veldgateway verifiëren](#authn-devices-field)</li></ul> |
| **IoT-Cloudgateway** | <ul><li>[Zorg ervoor dat de apparaten die verbinding maken tooCloud gateway worden geverifieerd](#authn-devices-cloud)</li><li>[Referenties voor verificatie per apparaat gebruiken](#authn-cred)</li></ul> |
| **Azure Storage** | <ul><li>[Zorg dat alleen Hallo vereist containers en blobs anonieme leestoegang zijn opgegeven](#req-containers-anon)</li><li>[Beperkte toegang tooobjects in Azure-opslag met SAS of SAP verlenen](#limited-access-sas)</li></ul> |

## <a id="standard-authn-web-app"></a>Overweeg het gebruik van een standaard verificatie mechanisme tooauthenticate tooWeb toepassing

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| Details | <p>Verificatie is Hallo proces waarbij een entiteit aantoont de identiteit, doorgaans via referenties, zoals een gebruikersnaam en wachtwoord dat. Er zijn verschillende verificatieprotocollen beschikbaar die kunnen worden beschouwd. Enkele ervan worden hieronder weergegeven:</p><ul><li>Clientcertificaten</li><li>Op basis van Windows</li><li>Op basis van formulieren</li><li>Federation - ADFS</li><li>Federation - Azure AD</li><li>Federation - Identiteitsserver</li></ul><p>Overweeg het gebruik van een standaard mechanisme tooidentify Hallo bron verificatieproces</p>|

## <a id="handle-failed-authn"></a>Toepassingen moeten veilig mislukte verificatiepogingen scenario's verwerken

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| Details | <p>Toepassingen die expliciet verificatie van gebruikers moeten mislukte verificatiepogingen scenario's securely.hello verificatiemechanisme moet verwerken:</p><ul><li>Toegang weigeren tooprivileged resources als verificatie is mislukt</li><li>Een algemeen foutbericht weergegeven na een mislukte verificatie en toegang is geweigerd vindt plaats</li></ul><p>Test voor:</p><ul><li>Beveiliging van bevoegde resources na mislukte aanmeldingen</li><li>Een algemene foutmelding wordt weergegeven op mislukte verificatie en toegang geweigerd gebeurtenis(sen)</li><li>Accounts zijn uitgeschakeld na een uitzonderlijk groot aantal mislukte pogingen</li><ul>|

## <a id="step-up-adaptive-authn"></a>Stap up inschakelen of adaptieve verificatie

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| Details | <p>Controleer of toepassing hello heeft extra autorisatie (zoals stap omhoog of adaptieve verificatie via meervoudige verificatie, zoals het zenden van OTP in SMS, e-mail, enz., of vragen om nieuwe verificatie) zodat Hallo gebruiker wordt gevraagd voordat hun toegang wordt verleend toosensitive informatie. Deze regel geldt ook voor het maken van belangrijke wijzigingen tooan account of actie</p><p>Ook dit betekent dat Hallo aanpassing van de verificatie is geïmplementeerd in deze toobe een manier die toepassing hello correct worden afgedwongen contextgevoelige autorisatie als toonot waardoor het niet-geautoriseerde manipulatie door middel van in voorbeeld parameter knoeien</p>|

## <a id="admin-interface-lockdown"></a>Zorg ervoor dat administratieve interfaces op de juiste wijze zijn vergrendeld

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| Details | de eerste oplossing Hallo is toogrant alleen toegankelijk is vanaf een bepaalde bron IP-bereik toohello beheerinterface. Als deze oplossing is niet mogelijk dan altijd aanbevolen tooenforce een geslaagde of adaptieve verificatie voor logboekregistratie in in de beheerinterface Hallo |

## <a id="forgot-pword-fxn"></a>Implementeer vergeten wachtwoord functionaliteiten veilig

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| Details | <p>Hallo is eerst te beginnen tooverify die vergeten wachtwoord en andere herstel naar een koppeling met inbegrip van een tijdelijke activering token in plaats van Hallo wachtwoord zelf verzenden. Aanvullende verificatie op basis van de soft-tokens (bijvoorbeeld SMS token mobiele toepassingen, etc.) kan worden vereist ook voordat Hallo koppeling wordt verzonden via. Ten tweede moet u niet vergrendelen Hallo gebruikers account terwijl Hallo proces van het ophalen van een nieuw wachtwoord uitgevoerd wordt.</p><p>Wanneer een aanvaller toointentionally vergrendelen Hallo gebruikers met een geautomatiseerde aanval besluit, kan dit tooa Denial of service-aanval leiden. Derde, wanneer het nieuwe wachtwoord aanvraag Hallo bezig was ingesteld, kan u weer te geven het Hallo-bericht moet worden gegeneraliseerd in volgorde tooprevent gebruikersnaam opsomming. Vierde altijd Hallo gebruik van oude wachtwoorden weigeren en een sterk wachtwoordbeleid implementeert.</p> |

## <a id="pword-account-policy"></a>Zorg ervoor dat de wachtwoord- en -beleid worden toegepast

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| Details | <p>Beleid voor wachtwoorden en voldoen aan het organisatiebeleid en best practices moet worden geïmplementeerd.</p><p>toodefend tegen brute kracht en woordenlijst gebaseerd raden: beleid voor sterke wachtwoorden moet geïmplementeerde tooensure dat gebruikers complex wachtwoord (bijv, de minimumlengte 12 tekens, alfanumerieke en speciale tekens) maken.</p><p>Het beleid voor accountvergrendeling mogen worden uitgevoerd in Hallo manier te volgen:</p><ul><li>**Voorlopig lock-out:** dit is een goede optie voor het beveiligen van uw gebruikers tegen gewelddadige aanvallen. Bijvoorbeeld, wanneer Hallo gebruiker een onjuist wachtwoord driemaal Hallo toepassing kan worden vergrendeld Hallo-account voor een minuut in volgorde tooslow omlaag Hallo proces van het forceren van zijn/haar wachtwoord zodat u minder winstgevend voor Hallo aanvaller tooproceed brute. Als u vaste uitsluiting countermeasures voor dit voorbeeld zou worden behaald tooimplement zou een Dos' ' door permanent accounts worden vergrendeld. U kunt ook toepassing kan een OTP (één keer wachtwoord) genereren en verzenden out-of-band (via e-mail, sms, enz.) toohello gebruiker. Een andere benadering mogelijk tooimplement CAPTCHA nadat een drempelwaarde voor aantal mislukte pogingen is bereikt.</li><li>**Vaste lock-out:** dit type vergrendeling moet worden toegepast wanneer u een gebruiker een aanval op uw toepassing te detecteren en hem door middel van hun account permanent accountvergrendeling totdat een team antwoord gehad tijd toodo hun forensische teller. Na dit proces kunt u besluiten toogive Hallo gebruiker terug hun account of maatregelen verdere juridische tegen hem. Dit type benadering wordt voorkomen dat Hallo aanvaller verdere vocht uw toepassingen en infrastructuur.</li></ul><p>toodefend tegen aanvallen op de standaard- en voorspelbare accounts, Controleer of alle sleutels en wachtwoorden worden vervangen, en zijn gegenereerd of na het tijdstip van de vervangen.</p><p>Als de toepassing hello tooauto-wachtwoorden genereren, Controleer of Hallo gegenereerd wachtwoorden willekeurige worden en hoge entropie hebben.</p>|

## <a id="controls-username-enum"></a>Implementeer besturingselementen tooprevent gebruikersnaam opsomming

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | Alle foutberichten moeten worden gegeneraliseerd in volgorde tooprevent gebruikersnaam opsomming. Ook soms kan niet worden vermeden informatie in functies zoals een registratiepagina lekken. U moet hier toouse frequentiebeperkende methoden zoals CAPTCHA tooprevent een geautomatiseerde aanval door een aanvaller. |

## <a id="win-authn-sql"></a>Gebruik zo mogelijk Windows-verificatie voor het verbinden van tooSQL Server

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Database | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | OnPrem |
| **Kenmerken**              | SQL-versie - alle |
| **Verwijzingen**              | [SQL Server - een verificatiemodus kiezen](https://msdn.microsoft.com/library/ms144284.aspx) |
| **Stappen** | Windows-verificatie gebruikt Kerberos veiligheidsprotocol, voorziet wachtwoord-beleidsafdwinging met inachtneming van toocomplexity validatie voor sterke wachtwoorden, biedt ondersteuning voor accountvergrendeling en ondersteunt verlopen van wachtwoorden.|

## <a id="aad-authn-sql"></a>Gebruik zo mogelijk Azure Active Directory-verificatie voor tooSQL verbinding maakt met Database

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Database | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | SQL Azure |
| **Kenmerken**              | SQL-versie - V12 |
| **Verwijzingen**              | [TooSQL Database met behulp van Azure Active Directory-verificatie verbinding te maken](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/) |
| **Stappen** | **Minimale versie:** Azure SQL Database V12 tooallow Azure SQL Database toouse AAD-verificaties tegen Hallo Microsoft Directory vereist |

## <a id="authn-account-pword"></a>SQL-verificatiemodus wordt gebruikt, zorg er bij dat account en wachtwoord beleid worden afgedwongen op SQL server

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Database | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [SQL Server-wachtwoordbeleid](https://technet.microsoft.com/library/ms161959(v=sql.110).aspx) |
| **Stappen** | Wanneer u SQL Server-verificatie gebruikt, worden de aanmeldingen gemaakt in SQL Server die niet zijn gebaseerd op Windows-gebruikersaccounts. Zowel Hallo-gebruikersnaam en wachtwoord Hallo zijn gemaakt met behulp van SQL Server en opgeslagen in SQL Server. SQL Server kan mechanismen voor beleid voor Windows-wachtwoord gebruiken. Hallo dezelfde complexiteit en de vervaldatum beleid in Windows toopasswords in SQL Server gebruikt gebruikt kan worden toegepast. |

## <a id="autn-contained-db"></a>Gebruik geen SQL-verificatie in ingesloten databases

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Database | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | OnPrem, Azure SQL |
| **Kenmerken**              | SQL - MSSQL2012, SQL-versie --versie V12 |
| **Verwijzingen**              | [Best Practices voor beveiliging met ingesloten Databases](http://msdn.microsoft.com/library/ff929055.aspx) |
| **Stappen** | Hallo afwezigheid van een afgedwongen wachtwoordbeleid kan verhogen Hallo kans op een zwakke referentie in een ingesloten database tot stand wordt gebracht. Maak gebruik van Windows-verificatie. |

## <a id="authn-sas-tokens"></a>Per apparaat referenties voor verificatie met behulp van SaS-tokens worden gebruikt

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Azure Event Hub | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Verificatie en beveiliging model overzicht van Event Hubs](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **Stappen** | <p>Hallo Event Hubs beveiligingsmodel is gebaseerd op een combinatie van Shared Access Signature (SAS)-tokens en gebeurtenisuitgevers. naam van de uitgever Hallo vertegenwoordigt Hallo DeviceID die Hallo token ontvangt. Hierdoor zou Hallo-tokens gegenereerd met de betreffende apparaten Hallo koppelen.</p><p>Alle berichten zijn gelabeld met de oorspronkelijke aanvrager op servicezijde zodat de detectie van in de nettolading oorsprong adresvervalsing (spoofing) pogingen. Bij het verifiëren van apparaten genereren een per apparaat SaS-token bereik tooa unieke uitgever.</p>|

## <a id="multi-factor-azure-admin"></a>Azure multi-factor Authentication voor beheerders voor Azure inschakelen

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Vertrouwensgrenzen van Azure | 
| **SDL-fase**               | Implementatie |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Wat is Azure Multi-Factor Authentication?](https://azure.microsoft.com/documentation/articles/multi-factor-authentication/) |
| **Stappen** | <p>Multi-factor authentication (MFA) is een authenticatiemethode die meer dan één verificatiemethode is vereist en voegt een cruciale tweede beveiligingslaag van beveiliging toouser aanmeldingen en transacties. Het werkt door te vereisen van twee of meer van Hallo verificatiemethoden te volgen:</p><ul><li>Iets u weet (doorgaans een wachtwoord)</li><li>Iets er (een vertrouwd apparaat die niet eenvoudig wordt gedupliceerd, zoals een telefoon)</li><li>Iets dat u (biometrie)</li><ul>|

## <a id="anon-access-cluster"></a>Anonieme toegang tooService Fabric-Cluster beperken

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Service Fabric-Vertrouwensgrenzen | 
| **SDL-fase**               | Implementatie |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | Omgeving - Azure  |
| **Verwijzingen**              | [Scenario's voor beveiliging van service Fabric-cluster](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security) |
| **Stappen** | <p>Clusters moet altijd beveiligde tooprevent niet-geautoriseerde gebruikers verbinding maken met cluster tooyour, vooral wanneer er productieworkloads uitgevoerd.</p><p>Zorg ervoor dat beveiligingsmodus hello te "veilig" is ingesteld tijdens het maken van een service fabric-cluster en configureren van Hallo vereist X.509-servercertificaat. Maken van een cluster 'onveilig', krijgt een anonieme gebruiker tooconnect tooit als deze management eindpunten toohello beschrijft openbare Internet.</p>|

## <a id="fabric-cn-nn"></a>Zorg ervoor dat Service Fabric-clientknooppunt certificaat verschilt van het knooppunt naar certificaat

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Service Fabric-Vertrouwensgrenzen | 
| **SDL-fase**               | Implementatie |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | Zelfstandige omgeving - Azure, omgeving- |
| **Verwijzingen**              | [Beveiliging van service Fabric-clientknooppunt certificate](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/#_client-to-node-certificate-security), [Connect tooa beveiligde cluster clientcertificaat](https://azure.microsoft.com/documentation/articles/service-fabric-connect-to-secure-cluster/) |
| **Stappen** | <p>De beveiliging van client-naar-node certificate is tijdens het maken van Hallo-cluster via hello Azure-portal, Resource Manager-sjablonen of een zelfstandige JSON-sjabloon door op te geven van een clientcertificaat voor de beheerder en/of een clientcertificaat voor de gebruiker geconfigureerd.</p><p>Hallo beheerder client- en clientcertificaten die u opgeeft moet anders dan Hallo primaire en secundaire certificaten die u voor knooppunt naar beveiliging opgeeft.</p>|

## <a id="aad-client-fabric"></a>Gebruik AAD tooauthenticate clients tooservice fabric-clusters

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Service Fabric-Vertrouwensgrenzen | 
| **SDL-fase**               | Implementatie |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | Omgeving - Azure |
| **Verwijzingen**              | [Scenario's voor beveiliging - aanbevelingen voor beveiliging](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/#security-recommendations) |
| **Stappen** | Clusters die worden uitgevoerd op Azure kunnen ook veilige toegang toohello eindpunten voor beheer met behulp van Azure Active Directory (AAD), afgezien van clientcertificaten. Voor Azure clusters, wordt het aanbevolen AAD beveiliging tooauthenticate clients en -certificaten te voor een knooppunt naar beveiliging gebruiken.|

## <a id="fabric-cert-ca"></a>Zorg ervoor dat service fabric-certificaten van een erkende certificeringsinstantie (CA) worden verkregen

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Service Fabric-Vertrouwensgrenzen | 
| **SDL-fase**               | Implementatie |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | Omgeving - Azure |
| **Verwijzingen**              | [X.509-certificaten en Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/#x509-certificates-and-service-fabric) |
| **Stappen** | <p>Service Fabric maakt gebruik van x.509-certificaten voor het verifiëren van de knooppunten en clients.</p><p>Een aantal belangrijke zaken tooconsider tijdens het gebruik van certificaten in service-fabrics:</p><ul><li>Certificaten worden gebruikt in clusters met productieworkloads moeten worden gemaakt met een juist geconfigureerde service voor Windows Server-certificaat of verkregen van een erkende certificeringsinstantie (CA). Hallo CA mag een goedgekeurde externe Certificeringsinstantie of een goed beheerde interne Public Key Infrastructure (PKI)</li><li>Gebruik nooit een tijdelijke en certificaten in productie die zijn gemaakt met de hulpprogramma's zoals MakeCert.exe testen</li><li>U kunt een zelfondertekend certificaat gebruiken, maar moet alleen doen voor testclusters en niet in productie</li></ul>|

## <a id="standard-authn-id"></a>Gebruik standaard verificatie scenario's ondersteund door Identiteitsserver

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Identiteitsserver | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [IdentityServer3 - Hallo grote afbeelding](https://identityserver.github.io/Documentation/docsv2/overview/bigPicture.html) |
| **Stappen** | <p>Hieronder vindt Hallo typische interacties ondersteund door de identiteit van Server:</p><ul><li>Browsers communiceren met webtoepassingen</li><li>Webtoepassingen communiceren met de web-API's (soms op hun eigen soms namens een gebruiker)</li><li>Browser gebaseerde toepassingen communiceren met de web-API 's</li><li>Systeemeigen toepassingen communiceren met de web-API 's</li><li>Servertoepassingen communiceren met de web-API 's</li><li>Web-API's communiceren met de web-API's (soms op hun eigen soms namens een gebruiker)</li></ul>|

## <a id="override-token"></a>Hallo standaard Identiteitsserver tokencache met een schaalbare alternatief overschrijven

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Identiteitsserver | 
| **SDL-fase**               | Implementatie |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Implementatie van de Server Identity - Caching](https://identityserver.github.io/Documentation/docsv2/advanced/deployment.html) |
| **Stappen** | <p>IdentityServer heeft een eenvoudige ingebouwde geheugencache. Dit is geschikt voor kleine schaal systeemeigen apps, deze niet kan worden uitgebreid voor mid-laag en back-end-toepassingen voor Hallo volgende redenen:</p><ul><li>Deze toepassingen zijn toegankelijk door veel gebruikers tegelijk. Opslaan van alle toegangstokens in Hallo dezelfde opslag wordt gemaakt van isolatie problemen en geeft de uitdagingen bij het besturingssysteem op grote schaal: veel gebruikers, elk met zoveel tokens zoals Hallo resources Hallo app toegang geeft tot namens hen kan betekenen grote aantallen en bijzonder veeleisende lookup bewerkingen</li><li>Deze toepassingen worden doorgaans geïmplementeerd op gedistribueerde topologieën, waarbij meerdere knooppunten toohello toegang moeten hebben dezelfde cache</li><li>In de cache tokens moeten overleven wordt gerecycled en deactivations</li><li>Voor alle Hallo bovenstaande redenen tijdens de implementatie van web-apps, wordt aanbevolen de tokencache toooverride Hallo standaard identiteit van Server met een schaalbare alternatief zoals Azure Redis-cache</li></ul>|

## <a id="binaries-signed"></a>Zorg ervoor dat de binaire bestanden van geïmplementeerde toepassingen digitaal zijn ondertekend

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Een grens machine vertrouwensrelatie | 
| **SDL-fase**               | Implementatie |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | Zorg ervoor dat binaire bestanden van geïmplementeerde toepassingen digitaal zijn ondertekend, zodat de integriteit van de binaire bestanden Hallo Hallo kan worden gecontroleerd.|

## <a id="msmq-queues"></a>-Verificatie inschakelen wanneer u verbinding maakt tooMSMQ wachtrijen in WCF

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | WCF | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemeen, NET Framework 3 |
| **Kenmerken**              | N.v.t. |
| **Verwijzingen**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx) |
| **Stappen** | Programma tooenable verificatie is mislukt bij het verbinden van tooMSMQ wachtrijen, een aanvaller kan anoniem indienen berichten toohello wachtrij voor verwerking. Als verificatie niet gebruikte tooconnect tooan MSMQ wachtrij gebruikt toodeliver een bericht tooanother programma, kan een aanvaller een anonieme bericht dat schadelijk is verzonden.|

### <a name="example"></a>Voorbeeld
Hallo `<netMsmqBinding/>` element van Hallo WCF-configuratiebestand onderstaande Hiermee geeft u WCF toodisable verificatie bij het verbinden van tooan MSMQ-wachtrij voor de levering van berichten.
```
<bindings>
    <netMsmqBinding>
        <binding>
            <security>
                <transport msmqAuthenticationMode=""None"" />
            </security>
        </binding>
    </netMsmqBinding>
</bindings>
```
MSMQ toorequire verificatie van Windows-domein of certificaat altijd voor binnenkomende of uitgaande berichten configureren.

### <a name="example"></a>Voorbeeld
Hallo `<netMsmqBinding/>` element van Hallo WCF-configuratiebestand onderstaande Hiermee geeft u WCF tooenable certificaatverificatie bij het verbinden van tooan MSMQ-wachtrij. Hallo-client is geverifieerd met behulp van x.509-certificaten. Hallo-clientcertificaat moet aanwezig zijn in het certificaatarchief Hallo van Hallo-server.
```
<bindings>
    <netMsmqBinding>
        <binding>
            <security>
                <transport msmqAuthenticationMode=""Certificate"" />
            </security>
        </binding>
    </netMsmqBinding>
</bindings>
```

## <a id="message-none"></a>WCF-Do bericht clientCredentialType toonone niet ingesteld

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | WCF | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | .NET framework 3 |
| **Kenmerken**              | Het referentietype client - geen |
| **Verwijzingen**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Voeg](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Stappen** | Hallo gebrek aan authenticatie betekent iedereen kunnen tooaccess is deze service. Een service die de clients niet geverifieerd kan toegang tooall gebruikers. Hallo toepassing tooauthenticate tegen clientreferenties configureren. Dit kan worden gedaan door in te stellen Hallo-bericht clientCredentialType tooWindows of het certificaat. |

### <a name="example"></a>Voorbeeld
```
<message clientCredentialType=""Certificate""/>
```

## <a id="transport-none"></a>WCF-Do Transport clientCredentialType toonone niet ingesteld

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | WCF | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemeen, .NET Framework 3 |
| **Kenmerken**              | Het referentietype client - geen |
| **Verwijzingen**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Voeg](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Stappen** | Hallo gebrek aan authenticatie betekent iedereen kunnen tooaccess is deze service. Een service die de clients niet geverifieerd kan alle gebruikers tooaccess functionaliteit ervan. Hallo toepassing tooauthenticate tegen clientreferenties configureren. Dit kan worden gedaan door in te stellen Hallo transport clientCredentialType tooWindows of het certificaat. |

### <a name="example"></a>Voorbeeld
```
<transport clientCredentialType=""Certificate""/>
```

## <a id="authn-secure-api"></a>Zorg ervoor dat standaard authenticatietechnieken gebruikte toosecure Web-API 's

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Web-API | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Verificatie en autorisatie in ASP.NET Web-API](http://www.asp.net/web-api/overview/security/authentication-and-authorization-in-aspnet-web-api), [externe verificatieservices met ASP.NET-Web-API (C#)](http://www.asp.net/web-api/overview/security/external-authentication-services) |
| **Stappen** | <p>Verificatie is Hallo proces waarbij een entiteit aantoont de identiteit, doorgaans via referenties, zoals een gebruikersnaam en wachtwoord dat. Er zijn verschillende verificatieprotocollen beschikbaar die kunnen worden beschouwd. Enkele ervan worden hieronder weergegeven:</p><ul><li>Clientcertificaten</li><li>Op basis van Windows</li><li>Op basis van formulieren</li><li>Federation - ADFS</li><li>Federation - Azure AD</li><li>Federation - Identiteitsserver</li></ul><p>Koppelingen in de sectie Verwijzingen Hallo vindt op laag niveau meer informatie over hoe elk van de Hallo verificatieschema's kan worden geïmplementeerd toosecure een Web-API.</p>|

## <a id="authn-aad"></a>Gebruik standaard verificatie scenario's ondersteund door Azure Active Directory

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Azure AD | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Verificatie-scenario's voor Azure AD](https://azure.microsoft.com/documentation/articles/active-directory-authentication-scenarios/), [Azure Active Directory-codevoorbeelden](https://azure.microsoft.com/documentation/articles/active-directory-code-samples/), [ontwikkelaarshandleiding Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-developers-guide/) |
| **Stappen** | <p>Azure Active Directory (Azure AD) vereenvoudigt de verificatie voor ontwikkelaars dankzij de identiteit als een service met ondersteuning voor de industriestandaard-protocollen zoals OAuth 2.0 en OpenID Connect. Hieronder volgen Hallo vijf primaire toepassing scenario's die worden ondersteund door Azure AD:</p><ul><li>Web Browser tooWeb toepassing: een gebruiker moet toosign in tooa-webtoepassing die wordt beveiligd door Azure AD</li><li>Één pagina toepassing (SPA): Een gebruiker moet toosign in tooa één pagina toepassing die wordt beveiligd door Azure AD</li><li>Systeemeigen toepassing tooWeb API: een systeemeigen toepassing die wordt uitgevoerd op een telefoon, tablet of PC behoeften tooauthenticate een gebruiker tooget bronnen van een web-API die wordt beveiligd door Azure AD</li><li>Web-API van Application tooWeb: een webtoepassing moet tooget bronnen van een web-API die zijn beveiligd door Azure AD</li><li>Daemon of servertoepassing tooWeb API: een daemontoepassing of een servertoepassing zonder gebruikersinterface web moet tooget bronnen van een web-API die zijn beveiligd door Azure AD</li></ul><p>Raadpleeg toohello koppelingen in de sectie Verwijzingen Hallo voor op laag niveau implementatiegegevens</p>|

## <a id="adal-scalable"></a>Hallo standaard ADAL tokencache met een schaalbare alternatief overschrijven

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Azure AD | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Moderne verificatie met Azure Active Directory voor webtoepassingen](https://blogs.msdn.microsoft.com/microsoft_press/2016/01/04/new-book-modern-authentication-with-azure-active-directory-for-web-applications/), [als ADAL-token cache met behulp van Redis](https://blogs.msdn.microsoft.com/mrochon/2016/09/19/using-redis-as-adal-token-cache/)  |
| **Stappen** | <p>Hallo standaardcache ADAL (Active Directory Authentication Library) gebruikt een cache in het geheugen die afhankelijk is van een statische opslag proces hele beschikbaar is. Hoewel dit voor toepassingen werkt, deze niet kan worden uitgebreid voor mid-laag en back-end-toepassingen voor Hallo volgende redenen:</p><ul><li>Deze toepassingen zijn toegankelijk door veel gebruikers tegelijk. Opslaan van alle toegangstokens in Hallo dezelfde opslag wordt gemaakt van isolatie problemen en geeft de uitdagingen bij het besturingssysteem op grote schaal: veel gebruikers, elk met zoveel tokens zoals Hallo resources Hallo app toegang geeft tot namens hen kan betekenen grote aantallen en bijzonder veeleisende lookup bewerkingen</li><li>Deze toepassingen worden doorgaans geïmplementeerd op gedistribueerde topologieën, waarbij meerdere knooppunten toohello toegang moeten hebben dezelfde cache</li><li>In de cache tokens moeten overleven wordt gerecycled en deactivations</li></ul><p>Voor alle Hallo bovenstaande redenen tijdens de implementatie van web-apps, wordt aanbevolen toooverride Hallo standaard ADAL tokencache met een schaalbare alternatief zoals Azure Redis-cache.</p>|

## <a id="tokenreplaycache-adal"></a>Zorg ervoor dat TokenReplayCache gebruikte tooprevent Hallo replay van tokens voor ADAL-verificatie

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Azure AD | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Moderne verificatie met Azure Active Directory voor webtoepassingen](https://blogs.msdn.microsoft.com/microsoft_press/2016/01/04/new-book-modern-authentication-with-azure-active-directory-for-web-applications/) |
| **Stappen** | <p>Hallo TokenReplayCache eigenschap kunnen ontwikkelaars toodefine tokenreplay-cache, een store, die kan worden gebruikt voor het opslaan van tokens voor Hallo doel om te controleren die geen token kan meer dan eenmaal worden gebruikt.</p><p>Dit is een meting op basis van een algemene aanval hello toepasselijke aangeroepen tokenreplay aanval: een aanvaller onderscheppen Hallo token verzonden bij het aanmelden toosend proberen deze toohello app opnieuw ('opnieuw afspelen') voor het tot stand brengen van een nieuwe sessie. Bijvoorbeeld In OIDC code-grant flow, na een geslaagde verificatie, een aanvraag te ' / aanmelding oidc ' eindpunt van de relying party hello wordt gemaakt met 'id_token', 'code' en 'status'-parameters.</p><p>Hallo relying party deze aanvraag valideert en er wordt een nieuwe sessie. Als een adversary deze aanvraag wordt vastgelegd en opnieuw wordt weergegeven, kan hij een geslaagde sessie en vervalste Hallo gebruiker maken. Hallo aanwezigheid van de nonce Hallo in OpenID Connect kunt beperken, maar niet volledig elimineren Hallo omstandigheden waarin Hallo aanval met succes kan worden ingesteld. tooprotect hun toepassingen, ontwikkelaars kunnen een implementatie leveren van ITokenReplayCache en een exemplaar tooTokenReplayCache toewijzen.</p>|

### <a name="example"></a>Voorbeeld
```C#
// ITokenReplayCache defined in ADAL
public interface ITokenReplayCache
{
bool TryAdd(string securityToken, DateTime expiresOn);
bool TryFind(string securityToken);
}
```

### <a name="example"></a>Voorbeeld
Hier volgt een Voorbeeldimplementatie van Hallo ITokenReplayCache interface. (Geef aanpassen en implementeren van uw project-specifieke cache-framework)
```C#
public class TokenReplayCache : ITokenReplayCache
{
    private readonly ICacheProvider cache; // Your project-specific cache provider
    public TokenReplayCache(ICacheProvider cache)
    {
        this.cache = cache;
    }
    public bool TryAdd(string securityToken, DateTime expiresOn)
    {
        if (this.cache.Get<string>(securityToken) == null)
        {
            this.cache.Set(securityToken, securityToken);
            return true;
        }
        return false;
    }
    public bool TryFind(string securityToken)
    {
        return this.cache.Get<string>(securityToken) != null;
    }
}
```
Hallo geïmplementeerd cache heeft toobe waarnaar wordt verwezen in de opties OIDC via de eigenschap 'TokenValidationParameters' Hallo als volgt.
```C#
OpenIdConnectOptions openIdConnectOptions = new OpenIdConnectOptions
{
    AutomaticAuthenticate = true,
    ... // other configuration properties follow..
    TokenValidationParameters = new TokenValidationParameters
    {
        TokenReplayCache = new TokenReplayCache(/*Inject your cache provider*/);
    }
}
```

Controleer Houd er rekening mee dat tootest Hallo effectiviteit van deze configuratie, aanmelding in uw lokale OIDC beveiligde toepassing en Hallo aanvraag te leggen`"/signin-oidc"` eindpunt in fiddler. Deze aanvraag in fiddler herstelbewerking wordt wanneer Hallo beveiliging niet aanwezig is, een nieuwe sessiecookie ingesteld. Wanneer het Hallo-aanvraag wordt opnieuw afgespeeld nadat Hallo TokenReplayCache beveiliging wordt toegevoegd, wordt toepassing hello Veroorzaak een exception als volgt:`SecurityTokenReplayDetectedException: IDX10228: hello securityToken has previously been validated, securityToken: 'eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ1......`

## <a id="adal-oauth2"></a>Gebruik ADAL-bibliotheken toomanage token-aanvragen van OAuth2 clients tooAAD (of on-premises AD)

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Azure AD | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [ADAL](https://azure.microsoft.com/documentation/articles/active-directory-authentication-libraries/) |
| **Stappen** | <p>Hello Azure AD authentication Library (ADAL) kan client toepassing ontwikkelaars tooeasily toocloud gebruikers verifiëren of on-premises Active Directory (AD), en vervolgens verkrijgen toegangstokens voor het beveiligen van API-aanroepen.</p><p>ADAL bevat veel functies die verificatie maken eenvoudiger voor ontwikkelaars, zoals ondersteuning voor asynchrone, een configureerbare tokencache waarmee toegangstokens en vernieuwen van tokens, automatisch token vernieuwen wanneer een toegangstoken is verlopen en een vernieuwingstoken beschikbaar is, worden opgeslagen en meer.</p><p>Door het verwerken van de meeste Hallo complexiteit ADAL doelgericht op bedrijfslogica in de toepassing in developer en eenvoudig resources beveiligen zonder een expert over de beveiliging. Afzonderlijke bibliotheken zijn beschikbaar voor .NET, JavaScript (client en Node.js), iOS, Android en Java.</p>|

## <a id="authn-devices-field"></a>Apparaten die verbinding maken toohello Veldgateway verifiëren

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Veld IoT Gateway | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | Zorg ervoor dat elk apparaat wordt geverifieerd door Hallo Veldgateway voordat u gegevens uit deze accepteert en vóór de upstream-communicatie met de Hallo Cloudgateway. Zorg er ook voor dat apparaten verbinding met maken een per apparaat credential zodat afzonderlijke apparaten uniek kunnen worden geïdentificeerd.|

## <a id="authn-devices-cloud"></a>Zorg ervoor dat de apparaten die verbinding maken tooCloud gateway worden geverifieerd

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | IoT-Cloudgateway | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemeen, C#, Node.JS,  |
| **Kenmerken**              | N.V.T., Gateway keuze - Azure IoT Hub |
| **Verwijzingen**              | N.V.T., [Azure IoT hub met .NET](https://azure.microsoft.com/documentation/articles/iot-hub-csharp-csharp-getstarted/), [wih IoT-hub aan de slag en knooppunt JS](https://azure.microsoft.com/documentation/articles/iot-hub-node-node-getstarted), [IoT met SAS en certificaten beveiligen](https://azure.microsoft.com/documentation/articles/iot-hub-sas-tokens/), [Git-opslagplaats](https://github.com/Azure/azure-iot-sdks/tree/master/node) |
| **Stappen** | <ul><li>**Algemene:** verifiëren Hallo apparaat met Transport Layer Security (TLS) of IPSec. Infrastructuur moet ondersteuning met behulp van vooraf gedeelde sleutel (PSK) op apparaten die volledige asymmetrische cryptografie kunnen niet worden verwerkt. Maak gebruik van Azure AD, Oauth.</li><li>**C#:** bij het maken van een exemplaar DeviceClient standaard, Hallo methode Create maakt een DeviceClient-exemplaar die gebruikmaakt van Hallo AMQP-protocol toocommunicate met IoT Hub. toouse hello HTTPS-protocol gebruiken Hallo-onderdrukken van Hallo maken methode waarmee u toospecify Hallo-protocol. Als u Hallo HTTPS-protocol gebruikt, moet u ook Hallo toevoegen `Microsoft.AspNet.WebApi.Client` NuGet-pakket tooyour project tooinclude hello `System.Net.Http.Formatting` naamruimte.</li></ul>|

### <a name="example"></a>Voorbeeld
```C#
static DeviceClient deviceClient;

static string deviceKey = "{device key}";
static string iotHubUri = "{iot hub hostname}";

var messageString = "{message in string format}";
var message = new Message(Encoding.ASCII.GetBytes(messageString));

deviceClient = DeviceClient.Create(iotHubUri, new DeviceAuthenticationWithRegistrySymmetricKey("myFirstDevice", deviceKey));

await deviceClient.SendEventAsync(message);
```

### <a name="example"></a>Voorbeeld
**Node.JS: verificatie**
#### <a name="symmetric-key"></a>Symmetrische sleutel
* Een iothub maken in azure
* Een vermelding maken in het register Hallo apparaat-id 's
    ```javascript
    var device = new iothub.Device(null);
    device.deviceId = <DeviceId >
    registry.create(device, function(err, deviceInfo, res) {})
    ```
* Een gesimuleerd apparaat maken
    ```javascript
    var clientFromConnectionString = require('azure-iot-device-amqp').clientFromConnectionString;
    var Message = require('azure-iot-device').Message;
    var connectionString = 'HostName=<HostName>DeviceId=<DeviceId>SharedAccessKey=<SharedAccessKey>';
    var client = clientFromConnectionString(connectionString);
    ```
#### <a name="sas-token"></a>SAS-Token
* Opgehaald intern zijn gegenereerd wanneer u symmetrische sleutel, maar we kunnen genereren en deze ook expliciet gebruiken
* Een protocol definiëren:`var Http = require('azure-iot-device-http').Http;`
* Een sas-token maken:
    ```javascript
    resourceUri = encodeURIComponent(resourceUri.toLowerCase()).toLowerCase();
    var deviceName = "<deviceName >";
    var expires = (Date.now() / 1000) + expiresInMins * 60;
    var toSign = resourceUri + '\n' + expires;
    // using crypto
    var decodedPassword = new Buffer(signingKey, 'base64').toString('binary');
    const hmac = crypto.createHmac('sha256', decodedPassword);
    hmac.update(toSign);
    var base64signature = hmac.digest('base64');
    var base64UriEncoded = encodeURIComponent(base64signature);
    // construct authorization string
    var token = "SharedAccessSignature sr=" + resourceUri + "%2fdevices%2f"+deviceName+"&sig="
    + base64UriEncoded + "&se=" + expires;
    if (policyName) token += "&skn="+policyName;
    return token;
    ```
* Verbinding maken via sas-token: 
    ```javascript
    Client.fromSharedAccessSignature(sas, Http); 
    ```
#### <a name="certificates"></a>Certificaten
* Genereren van een zelf-ondertekend X509 certificaat met behulp van een hulpprogramma zoals OpenSSL toogenerate een .cert en .key bestanden toostore Hallo certificaat en Hallo sleutel respectievelijk
* Inrichten van een apparaat dat accepteert beveiligde verbinding met behulp van certificaten.
    ```javascript
    var connectionString = '<connectionString>';
    var registry = iothub.Registry.fromConnectionString(connectionString);
    var deviceJSON = {deviceId:"<deviceId>",
    authentication: {
        x509Thumbprint: {
        primaryThumbprint: "<PrimaryThumbprint>",
        secondaryThumbprint: "<SecondaryThumbprint>"
        }
    }}
    var device = deviceJSON;
    registry.create(device, function (err) {});
    ```
* Verbinding maken met een apparaat met een certificaat
    ```javascript
    var Protocol = require('azure-iot-device-http').Http;
    var Client = require('azure-iot-device').Client;
    var connectionString = 'HostName=<HostName>DeviceId=<DeviceId>x509=true';
    var client = Client.fromConnectionString(connectionString, Protocol);
    var options = {
        key: fs.readFileSync('./key.pem', 'utf8'),
        cert: fs.readFileSync('./server.crt', 'utf8')
    }; 
    // Calling setOptions with hello x509 certificate and key (and optionally, passphrase) will configure hello client //transport toouse x509 when connecting tooIoT Hub
    client.setOptions(options);
    //call fn tooexecute after hello connection is set up
    client.open(fn);
    ```

## <a id="authn-cred"></a>Referenties voor verificatie per apparaat gebruiken

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | IoT-Cloudgateway  | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | Keuze van de gateway - Azure IoT Hub |
| **Verwijzingen**              | [Azure IoT Hub beveiligingstokens](https://azure.microsoft.com/documentation/articles/iot-hub-sas-tokens/) |
| **Stappen** | Gebruik per apparaat referenties voor verificatie met behulp van SaS-tokens op basis van de sleutel voor apparaat of een clientcertificaat, in plaats van IoT Hub-niveau gedeelde toegangsbeleid. Hiermee voorkomt u dat Hallo hergebruik van verificatietokens van een apparaat of het veld gateway door een andere |

## <a id="req-containers-anon"></a>Zorg dat alleen Hallo vereist containers en blobs anonieme leestoegang zijn opgegeven

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Azure Storage | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | StorageType - Blob |
| **Verwijzingen**              | [Anonieme leestoegang toocontainers en blobs beheren](https://azure.microsoft.com/documentation/articles/storage-manage-access-to-resources/), [handtekeningen voor gedeelde toegang, deel 1: Understanding Hallo SAS-model](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/) |
| **Stappen** | <p>Standaard kunnen een container en alle bestaande blobs erin alleen worden geopend door Hallo eigenaar van Hallo storage-account. toogive anonieme gebruikers leesmachtigingen tooa container en de blobs, kan een Hallo container machtigingen tooallow openbare toegang ingesteld. Anonieme gebruikers kunnen BLOB's binnen een container openbaar toegankelijk lezen zonder verificatie Hallo-aanvraag.</p><p>Containers bieden Hallo opties voor het beheren van toegang tot de container te volgen:</p><ul><li>Volledige openbare leestoegang: Container en de blob-gegevens kunnen worden gelezen via anonieme aanvraag. Clients kunnen opsommen blobs in de container Hallo via anonieme aanvraag, maar kunnen de containers in Hallo storage-account niet inventariseren.</li><li>Openbare leestoegang voor blobs alleen: Blob-gegevens in deze container via anonieme aanvragen kunnen worden gelezen, maar de containergegevens is niet beschikbaar. Clients kunnen blobs in de container Hallo via anonieme aanvragen niet inventariseren</li><li>Geen enkele openbare leestoegang: Container en de blob-gegevens kunnen worden gelezen door de accounteigenaar alleen Hallo</li></ul><p>Anonieme toegang wordt aanbevolen voor scenario's waarin bepaalde blobs altijd beschikbaar voor anonieme toegang voor lezen zijn moeten. Voor nauwkeurigere beheer, een shared access signature waarmee toodelegate beperkte toegang met behulp van andere machtigingen kan worden gemaakt en via een opgegeven tijdsinterval. Zorg ervoor dat containers en blobs, dat mogelijk gevoelige gegevens bevatten kunnen, niet anonieme toegang per ongeluk opgegeven zijn</p>|

## <a id="limited-access-sas"></a>Beperkte toegang tooobjects in Azure-opslag met SAS of SAP verlenen

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Azure Storage | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t. |
| **Verwijzingen**              | [Shared Access Signatures, deel 1: Understanding Hallo SAS-model](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/), [handtekeningen voor gedeelde toegang, deel 2: maken en gebruiken van een SAS met Blob storage](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-2/), [hoe toodelegate tooobjects aan uw account met toegang Handtekeningen voor gedeelde toegang en opgeslagen toegangsbeleid](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_how-to-delegate-access-to-objects-in-your-account-using-shared-access-signatures-and-stored-access-policies) |
| **Stappen** | <p>Met behulp van een shared access signature (SAS) is een krachtige manier toogrant beperkte toegang tooobjects in een storage account tooother clients zonder tooexpose toegangssleutel. Hallo SAS is een URI die in de queryparameters omvat alle Hallo informatie nodig voor geverifieerde toegang tot tooa storage resource. opslagbronnen tooaccess Hello SAS, Hallo-client moet alleen toopass in Hallo SAS toohello geschikte constructor of methode.</p><p>U kunt een SAS gebruiken als u wilt tooprovide toegang tooresources in uw storage-account tooa client niet kan vertrouwd door de sleutel van Hallo worden. De opslagaccountsleutels bevatten zowel een primaire en secundaire sleutel, die beide beheerderstoegang tooyour account en alle resources in het Hallo verlenen. De mogelijkheid om uw account toohello van schadelijke of Achteloos gebruik blootstellen van een van de sleutels van uw account worden geopend. Handtekeningen voor gedeelde toegang bieden een veilige alternatief waarmee andere clients tooread-, schrijf- en verwijderen van gegevens in uw opslagaccount volgens toohello machtigingen die u hebt verleend, en zonder dat nodig is voor de sleutel Hallo-account.</p><p>Als u een logische set parameters die vergelijkbaar telkens zijn hebt, is gebruik van opgeslagen Access Policy (SAP) een beter idee. Omdat met behulp van een SAS afgeleid van een toegangsbeleid opgeslagen, kunt u gebruiken Hallo mogelijkheid toorevoke SAS onmiddellijk, is het Hallo aanbevolen best practice tooalways toegangsbeleid opgeslagen indien mogelijk.</p>|
