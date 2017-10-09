---
title: verklarende woordenlijst voor Active Directory-ontwikkelaar aaaAzure | Microsoft Docs
description: Een lijst met voorwaarden voor vaak gebruikte concepten voor ontwikkelaars van Azure Active Directory en functies.
services: active-directory
documentationcenter: 
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 551512df-46fb-4219-a14b-9c9fc23998ba
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 32a6a6194b8d01409159a2b60263bb66a87a843c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-developer-glossary"></a>Azure Active Directory-ontwikkelaar verklarende woordenlijst
In dit artikel bevat definities voor een aantal Hallo core Azure Active Directory (AD) concepten voor ontwikkelaars, dit handig is bij leren over het ontwikkelen van toepassingen voor Azure AD.

## <a name="access-token"></a>Toegangstoken
Een soort [beveiligingstoken](#security-token) uitgegeven door een [autorisatie server](#authorization-server), en gebruikt door een [clienttoepassing](#client-application) in volgorde tooaccess een [beveiligde resource-server ](#resource-server). Normaal gesproken in Hallo vorm van een [JSON Web Token (JWT)][JWT], Hallo token bevat Hallo autorisatie toohello client verleend door Hallo [resource-eigenaar](#resource-owner), voor een opgegeven niveau van toegang. Hallo token bevat alle toepasselijke [claims](#claim) over Hallo onderwerp, Hallo client toepassing toouse inschakelen als een vorm van referentie bij het openen van een bepaalde bron. Hierdoor wordt ook Hallo Hallo resource eigenaar tooexpose referenties toohello client nodig.

Toegangstokens zijn soms waarnaar wordt verwezen tooas 'Gebruiker + App' of 'App alleen-lezen', afhankelijk van het Hallo-referenties die wordt weergegeven. Wanneer een client-toepassing gebruikt bijvoorbeeld de:

* ['Autorisatiecode' authorization grant](#authorization-grant), Hallo eindgebruiker eerst als eigenaar van de resource Hallo verifieert, delegeren autorisatie toohello client tooaccess Hallo resource. Hallo client verifieert daarna bij het verkrijgen van Hallo-toegangstoken. Hallo-token kan soms waarnaar wordt verwezen toomore specifiek als een token 'Gebruiker + App' zijn omdat deze beide Hallo-gebruiker die gemachtigd Hallo-clienttoepassing en toepassing hello vertegenwoordigt.
* ['Clientreferenties ' authorization grant](#authorization-grant), Hallo client biedt enige Hallo-verificatie, werkt zonder Hallo resource-eigenaar van verificatie/autorisatie, dus Hallo token kan soms worden waarnaar wordt verwezen tooas een token 'App-Only'.

Zie [Azure AD-tokenverwijzing] [ AAD-Tokens-Claims] voor meer informatie.

## <a name="application-manifest"></a>Het toepassingsmanifest
Een functie die is geleverd door Hallo [Azure-portal][AZURE-portal], dat resulteert in een JSON-weergave van configuratie van de toepassing hello van identiteit, gebruikt als een mechanisme voor het bijwerken van de bijbehorende [ Toepassing] [ AAD-Graph-App-Entity] en [ServicePrincipal] [ AAD-Graph-Sp-Entity] entiteiten. Zie [Understanding hello Azure Active Directory-toepassingsmanifest] [ AAD-App-Manifest] voor meer informatie.

## <a name="application-object"></a>Object voor de toepassing
Wanneer u registreren of bij te werken een toepassing in Hallo [Azure-portal][AZURE-portal], Hallo portal bijgewerkte een object voor de toepassing en een bijbehorende [-serviceprincipalobject](#service-principal-object)voor deze tenant. object voor de toepassing Hello *definieert* configuratie van de identiteit van toepassing Hallo globaal (voor alle tenants waar deze toegang heeft), middel van een sjabloon van waaruit de bijbehorende objecten van de service-principal zijn  *afgeleide* voor gebruik tijdens runtime (in een specifieke tenant) lokaal.

Zie [toepassing en Service-Principal objecten] [ AAD-App-SP-Objects] voor meer informatie.

## <a name="application-registration"></a>Toepassing registreren
In volgorde tooallow een toepassing toointegrate met en gemachtigde Identity and Access Management functies tooAzure AD, moet deze worden geregistreerd met een Azure AD [tenant](#tenant). Wanneer u uw toepassing met Azure AD registreren, kunt u biedt een configuratie van de identiteit voor uw toepassing, zodat het toointegrate met Azure AD en functies zoals gebruiken:

* Krachtige beheermogelijkheden van eenmalige aanmelding met behulp van Azure AD Identity Management en [OpenID Connect] [ OpenIDConnect] protocolimplementatie
* Toegang te brokered[beveiligde bronnen](#resource-server) door [clienttoepassingen](#client-application), via Azure AD OAuth 2.0 [autorisatie server](#authorization-server) implementatie
* [Toestemming framework](#consent) voor het beheren van de client toegang tot tooprotected bronnen op basis van de verificatie van de resource-eigenaar.

Zie [toepassingen integreren met Azure Active Directory] [ AAD-Integrating-Apps] voor meer informatie.

## <a name="authentication"></a>Verificatie
Hallo handeling lastig van een partij om geldige referenties Hallo basis voor het maken van een principal toobe gebruikt voor identiteits- en toegangsbeheer van beveiliging bieden. Tijdens een [OAuth2 authorization grant](#authorization-grant) bijvoorbeeld Hallo partij verifiëren Hallo-rol van een van beide is invullen [resource-eigenaar](#resource-owner) of [clienttoepassing](#client-application), afhankelijk van Hallo grant gebruikt.

## <a name="authorization"></a>Autorisatie
Hallo handeling voor het verlenen van een geverifieerde beveiliging hoofdmachtiging toodo iets. Er zijn twee primaire gebruiksvoorbeelden in hello Azure AD-programmeermodel:

* Tijdens een [OAuth2 authorization grant](#authorization-grant) stroom: wanneer Hallo [resource-eigenaar](#resource-owner) verleent autorisatie toohello [clienttoepassing](#client-application), zodat de Hallo clientcomputers tooaccess Hallo bronnen van de resource-eigenaar.
* Tijdens toegang tot bedrijfsbronnen door client Hallo: die is geïmplementeerd in Hallo [bronserver](#resource-server), met behulp van Hallo [claim](#claim) waarden aanwezig zijn op Hallo [toegangstoken](#access-token) toomake toegangsbeheer beslissingen op basis van deze.

## <a name="authorization-code"></a>Autorisatiecode
Een korte gehouden 'token' opgegeven tooa [clienttoepassing](#client-application) door Hallo [autorisatie eindpunt](#authorization-endpoint), als onderdeel van Hallo 'autorisatiecode' stroom, een van de vier OAuth2 Hallo [toestemming verleent ](#authorization-grant). Hallo code toohello clienttoepassing wordt geretourneerd als antwoord tooauthentication van een [resource-eigenaar](#resource-owner), die aangeeft Hallo resource-eigenaar heeft gedelegeerd autorisatie tooaccess Hallo resources aangevraagd. Als onderdeel van de stroom Hallo Hallo code later wordt ingewisseld voor een [toegangstoken](#access-token).

## <a name="authorization-endpoint"></a>Autorisatie-eindpunt
Een van Hallo-eindpunten die zijn geïmplementeerd door Hallo [autorisatie server](#authorization-server), toointeract gebruikt met Hallo [resource-eigenaar](#resource-owner) in volgorde tooprovide een [authorization grant](#authorization-grant) tijdens een OAuth2-machtiging verlenen stroom. Afhankelijk van het Hallo-autorisatie verlenen stroom wordt gebruikt, Hallo werkelijke grant opgegeven kan verschillen, met inbegrip van een [autorisatiecode](#authorization-code) of [beveiligingstoken](#security-token).

Zie Hallo OAuth2-specificatie [autorisatie verlenen typen] [ OAuth2-AuthZ-Grant-Types] en [autorisatie eindpunt] [ OAuth2-AuthZ-Endpoint] secties en Hallo [OpenIDConnect specificatie] [ OpenIDConnect-AuthZ-Endpoint] voor meer informatie.

## <a name="authorization-grant"></a>machtiging verlenen
Een referentie die vertegenwoordigt Hallo [resource-eigenaar](#resource-owner) [autorisatie](#authorization) tooaccess de beveiligde bronnen, verleend tooa [clienttoepassing](#client-application). Een clienttoepassing kunt gebruiken één Hallo [vier typen zijn gedefinieerd door Hallo OAuth2 autorisatie Framework verlenen] [ OAuth2-AuthZ-Grant-Types] tooobtain een toekennen, afhankelijk van clientvereisten type: 'autorisatie code toekennen', ' clientreferenties verlenen', 'impliciete grant' en 'resource eigenaar wachtwoordreferenties verlenen'. Hallo referentie geretourneerd toohello client is een [toegangstoken](#access-token), of een [autorisatiecode](#authorization-code) (uitgewisseld later een toegangstoken), afhankelijk van Hallo type authorization grant gebruikt.

## <a name="authorization-server"></a>Autorisatie-server
Zoals gedefinieerd door Hallo [OAuth2 autorisatie Framework][OAuth2-Role-Def], Hallo server verantwoordelijk is voor het verlenen van toegang tokens toohello [client](#client-application) na verificatie is gelukt Hallo [resource-eigenaar](#resource-owner) en het verkrijgen van de autorisatie. Een [clienttoepassing](#client-application) communiceert met de Hallo autorisatie server tijdens runtime via de [autorisatie](#authorization-endpoint) en [token](#token-endpoint) eindpunten in overeenstemming met Hallo OAuth2 gedefinieerd [toestemming verleent](#authorization-grant).

In geval van de integratie van Azure AD-toepassing hello implementeert Azure AD Hallo autorisatie-serverrol voor Azure AD-toepassingen en Microsoft-service-API's, bijvoorbeeld [Microsoft Graph-API's][Microsoft-Graph].

## <a name="claim"></a>Claim
Een [beveiligingstoken](#security-token) bevat claims, die asserties over één entiteit opgeven (zoals een [clienttoepassing](#client-application) of [resource-eigenaar](#resource-owner)) tooanother entiteit (zoals Hallo [bronserver](#resource-server)). Claims zijn naam/waarde-paren die relay-feiten over Hallo token onderwerp (bijvoorbeeld Hallo beveiligings-principal die is geverifieerd door Hallo [autorisatie server](#authorization-server)). Hallo claims aanwezig zijn in een bepaalde token zijn afhankelijk van verschillende variabelen, zoals Hallo type token, Hallo type referentie gebruikt tooauthenticate Hallo onderwerp, de configuratie van de toepassing hello, enzovoort.

Zie [Azure AD-tokenverwijzing] [ AAD-Tokens-Claims] voor meer informatie.

## <a name="client-application"></a>clienttoepassing
Zoals gedefinieerd door Hallo [OAuth2 autorisatie Framework][OAuth2-Role-Def], een toepassing die wordt beveiligd resource aanvragen namens Hallo [resource-eigenaar](#resource-owner). Hallo term 'client' betekent niet dat voor een bepaalde hardware implementatie-eigenschappen (bijvoorbeeld of Hallo toepassing wordt uitgevoerd op een server, een bureaublad of andere apparaten).  

Een clienttoepassing vraagt [autorisatie](#authorization) van een resource-eigenaar tooparticipate in een [OAuth2 authorization grant](#authorization-grant) vloeien en mogelijk toegang tot API's / gegevens namens Hallo resource eigenaar. Hallo OAuth2 autorisatie Framework [definieert twee soorten clients][OAuth2-Client-Types], 'vertrouwelijk' en 'openbare', afhankelijk van het Hallo-client mogelijkheid toomaintain Hallo vertrouwelijkheid van de referenties. Toepassingen kunnen implementeren een [webclient (vertrouwelijk)](#web-client) die wordt uitgevoerd op een webserver, een [native client (openbaar)](#native-client) geïnstalleerd op een apparaat of een [client op basis van gebruikers-agent (openbaar)](#user-agent-based-client)die wordt uitgevoerd in de browser van een apparaat.

## <a name="consent"></a>Toestemming
Hallo proces van een [resource-eigenaar](#resource-owner) verlenen autorisatie tooa [clienttoepassing](#client-application), tooaccess beveiligde bronnen onder specifieke [machtigingen](#permissions), namens Hallo resource-eigenaar. Afhankelijk van de machtigingen Hallo door Hallo-client wordt aangevraagd, wordt een beheerder of gebruiker gevraagd toestemming tooallow toegang tot tootheir organisatie/afzonderlijke gegevens respectievelijk. Houd er rekening mee in een [multitenant](#multi-tenant-application) scenario, van de toepassing hello [service-principal](#service-principal-object) wordt ook vastgelegd in het Hallo-tenant van Hallo ermee akkoord dat gebruiker.

## <a name="id-token"></a>Token ID
Een [OpenID Connect] [ OpenIDConnect-ID-Token] [beveiligingstoken](#security-token) geleverd door een [autorisatie-server](#authorization-server) [autorisatie eindpunt](#authorization-endpoint), die bevat [claims](#claim) toohello verificatie die deel uitmaakt van een eindgebruiker [resource-eigenaar](#resource-owner). Zoals een toegangstoken ID-tokens ook worden weergegeven als een digitaal ondertekend [JSON Web Token (JWT)][JWT]. In tegenstelling tot een toegangstoken echter worden een ID-token claims niet gebruikt voor toegang tot het gerelateerde tooresource van toepassing en specifiek toegangsbeheer.

Zie [Azure AD-tokenverwijzing] [ AAD-Tokens-Claims] voor meer informatie.

## <a name="multi-tenant-application"></a>multitenant-toepassing
Een klasse die van toepassing waarmee aanmelden en [toestemming](#consent) door gebruikers ingericht in alle Azure AD [tenant](#tenant), met inbegrip van tenants dan Hallo een waar Hallo-client is geregistreerd. [Native client](#native-client) toepassingen zijn multitenant standaard terwijl [webclient](#web-client) en [web-resource/API](#resource-server) toepassingen Hallo mogelijkheid tooselect tussen één of meerdere tenants hebben. Daarentegen is een webtoepassing geregistreerd als één tenant, zouden alleen aanmeldingen van gebruikersaccounts in dezelfde tenant als Hallo een Hallo ingericht toestaan waar de toepassing hello is geregistreerd.

Zie [hoe toosign in elke Azure AD-gebruiker die meerdere tenants toepassing patroon Hallo] [ AAD-Multi-Tenant-Overview] voor meer informatie.

## <a name="native-client"></a>native client
Een soort [clienttoepassing](#client-application) die standaard is geïnstalleerd op een apparaat. Aangezien alle code wordt uitgevoerd op een apparaat, wordt een 'openbare' client vanwege tooits onvermogen toostore referenties privé/vertrouwelijk worden beschouwd. Zie [OAuth2-client van het type en -profielen] [ OAuth2-Client-Types] voor meer informatie.

## <a name="permissions"></a>Machtigingen
Een [clienttoepassing](#client-application) krijgt toegang tot tooa [bronserver](#resource-server) machtigingsaanvragen declareert. Er zijn twee typen beschikbaar:

* 'Gemachtigd', waarbij [op basis van een scope](#scopes) autorisatie van Hallo aangemelde toegang met behulp van gedelegeerde [resource-eigenaar](#resource-owner), toohello resource worden weergegeven tijdens het uitvoeren als ['scp ' claims](#claim) in Hallo-client [toegangstoken](#access-token).
* Machtigingen voor 'Application', die opgeven [op basis van rollen](#roles) openen met behulp van Hallo van de clienttoepassing referenties/identiteit, toohello resource worden weergegeven tijdens het uitvoeren als ['functies' claims](#claim) in Hallo het toegangstoken van de client.

Ze ook surface tijdens Hallo [toestemming](#consent) proces, waardoor Hallo beheerder of de resource-eigenaar Hallo kans toogrant/weigeren Hallo client access tooresources in de tenant.

Machtigingsaanvragen zijn geconfigureerd op Hallo 'Toepassingen' / 'Instellingen' hello tabblad [Azure-portal][AZURE-portal], onder 'Machtigingen vereist', door het selecteren van Hallo gewenst 'Gedelegeerde machtigingen' en ' Toepassingsmachtigingen' (laatste Hallo vereist lidmaatschap van de globale beheerdersrol Hallo). Omdat een [openbare client](#client-application) referenties, kan niet veilig worden onderhouden deze kan alleen aanvragen van gedelegeerde machtigingen, terwijl een [vertrouwelijke client](#client-application) Hallo mogelijkheid toorequest gedelegeerd en een toepassing is machtigingen. Hallo-client [toepassingsobject](#application-object) winkels Hallo gedeclareerd machtigingen in de [requiredResourceAccess eigenschap][AAD-Graph-App-Entity].

## <a name="resource-owner"></a>resource-eigenaar
Zoals gedefinieerd door Hallo [OAuth2 autorisatie Framework][OAuth2-Role-Def], een entiteit die geschikt zijn voor het verlenen van toegang tooa beveiligde resource. Wanneer Hallo resource-eigenaar van een persoon is, is het bedoelde tooas een eindgebruiker. Bijvoorbeeld, wanneer een [clienttoepassing](#client-application) tooaccess wil een gebruikerspostvak via Hallo [Microsoft Graph API][Microsoft-Graph], hiervoor toestemming van de resource-eigenaar Hallo van Hallo-postvak.

## <a name="resource-server"></a>resource-server
Zoals gedefinieerd door Hallo [OAuth2 autorisatie Framework][OAuth2-Role-Def], een server die hosts beveiligde bronnen, kunnen worden geaccepteerd en reageert tooprotected resource aanvragen door [client toepassingen](#client-application) die aanwezig een [toegangstoken](#access-token). Ook wel bekend als een beveiligde resource-server of een resource-toepassing.

Een resource-server beschrijft-API's en dwingt de toegang tot beveiligde tooits bronnen via [scopes](#scopes) en [rollen](#roles), met behulp van OAuth 2.0 autorisatie Framework Hallo. Voorbeelden zijn hello Azure AD Graph API waarmee toegang tot tooAzure AD-tenant gegevens en Hallo Office 365-API's waarmee toegang toodata zoals e-mail en agenda. Beide zijn ook toegankelijk via Hallo [Microsoft Graph API][Microsoft-Graph].  

Net als een clienttoepassing configuratie van de identiteit van de toepassing van de resource is gemaakt [registratie](#application-registration) bieden zowel Hallo-toepassing en service-principal-object in een Azure AD-tenant. Sommige Microsoft geleverde API's, zoals hello Azure AD Graph API hebt vooraf geregistreerd voor service-principals beschikbaar gesteld in alle huurders tijdens het inrichten.

## <a name="roles"></a>rolls
Zoals [scopes](#scopes), functies bieden de mogelijkheid om een [bronserver](#resource-server) toogovern toegang tooits beveiligde bronnen. Er zijn twee typen: een rol 'gebruiker' toegangsbeheer op basis van rollen worden geïmplementeerd voor gebruikers/groepen die toegang toohello resource, vereisen, terwijl een rol 'application' wordt geïmplementeerd voor dezelfde Hallo [clienttoepassingen](#client-application) die toegang nodig.

Rollen zijn tekenreeksen resource gedefinieerd (bijvoorbeeld "onkosten goedkeurder", 'Alleen-lezen', 'Directory.ReadWrite.All'), beheerde in Hallo [Azure-portal] [ AZURE-portal] via van Hallo resource [toepassing manifest](#application-manifest), en opgeslagen in een van de bron van de Hallo [appRoles eigenschap][AAD-Graph-Sp-Entity]. Hello Azure-portal is ook gebruikte tooassign gebruikers te 'gebruiker' rollen, en configureer client [Toepassingsmachtigingen](#permissions) tooaccess een rol 'application'.

Zie voor een gedetailleerde bespreking van de rollen van de toepassing hello die worden weergegeven door Azure AD Graph API [Graph API-Machtigingsbereiken][AAD-Graph-Perm-Scopes]. Zie voor een voorbeeld van stapsgewijze implementatie [op rollen gebaseerde toegangsbeheer in de cloud-toepassingen die gebruikmaken van Azure AD][Duyshant-Role-Blog].

## <a name="scopes"></a>Scopes
Zoals [rollen](#roles), scopes bieden de mogelijkheid om een [bronserver](#resource-server) toogovern toegang tooits beveiligde bronnen. Bereiken zijn gebruikte tooimplement [op basis van een scope] [ OAuth2-Access-Token-Scopes] toegangsbeheer voor een [clienttoepassing](#client-application) die gedelegeerde toegang toohello resource is toegewezen door de eigenaar.

Scopes zijn resource gedefinieerd tekenreeksen (bijvoorbeeld 'Mail.Read', 'Directory.ReadWrite.All'), in Hallo beheerd [Azure-portal] [ AZURE-portal] via van Hallo resource [toepassingsmanifest](#application-manifest), en opgeslagen in een van de bron van de Hallo [oauth2Permissions eigenschap][AAD-Graph-Sp-Entity]. Hello Azure-portal is ook de clienttoepassing gebruikte tooconfigure [overgedragen machtigingen](#permissions) tooaccess een scope.

Een best practice-naamgevingsconventie, is toouse een 'resource.operation.constraint'-indeling. Zie voor een gedetailleerde bespreking van Hallo scopes die worden weergegeven door Azure AD Graph API [Graph API-Machtigingsbereiken][AAD-Graph-Perm-Scopes]. Zie voor de bereiken die worden weergegeven door Office 365-services, [Office 365 API machtigingen verwijzing][O365-Perm-Ref].

## <a name="security-token"></a>beveiligingstoken
Een ondertekend document met claims, zoals een OAuth2-token of SAML 2.0-verklaring. Voor een OAuth2 [authorization grant](#authorization-grant), een [toegangstoken](#access-token) (OAuth2) en een [ID Token](http://openid.net/specs/openid-connect-core-1_0.html#IDToken) zijn typen beveiligingstokens, die beide zijn geïmplementeerd als een [JSON Web-Token (JWT)][JWT].

## <a name="service-principal-object"></a>Service-principal-object
Wanneer u registreren of bij te werken een toepassing in Hallo [Azure-portal][AZURE-portal], Hallo portal bijgewerkte zowel een [toepassingsobject](#application-object) en een bijbehorende service-principal object voor deze tenant. object voor de toepassing Hello *definieert* configuratie van de identiteit van de toepassing hello globaal (voor alle tenants waar Hallo gekoppeld toepassing toegang heeft gekregen), en is Hallo sjabloon op basis waarvan de bijbehorende service Principal-objecten zijn *afgeleid* voor gebruik tijdens runtime (in een specifieke tenant) lokaal.

Zie [toepassing en Service-Principal objecten] [ AAD-App-SP-Objects] voor meer informatie.

## <a name="sign-in"></a>Aanmelden
Hallo proces van een [clienttoepassing](#client-application) eindgebruiker verificatie gestart en vastleggen van gerelateerde status voor Hallo doel van het ophalen van een [beveiligingstoken](#security-token) en scoping Hallo toepassing sessie toothat status. State-artefacten, zoals gebruikersprofielgegevens kunnen bevatten en informatie die is afgeleid van token claims.

Hallo-in functie van een toepassing is gewoonlijk gebruikte tooimplement eenmalige aanmelding (SSO). Het kan ook worden voorafgegaan door een "registratie" functie als toegangspunt Hallo voor een eindgebruiker toogain toegang tooan toepassing (bij het eerste teken-in). Hallo aanmelding functie gebruikte toogather en aanvullende status specifieke toohello gebruiker behouden en mogelijk [toestemming van de gebruiker](#consent).

## <a name="sign-out"></a>afmelden
proces van het niet verifiërende een eindgebruiker loskoppelen Hallo gebruikersstatus die is gekoppeld aan Hallo Hallo [clienttoepassing](#client-application) sessie tijdens [aanmelden](#sign-in)

## <a name="tenant"></a>Tenant
Een exemplaar van een Azure Active directory is waarnaar wordt verwezen tooas een Azure AD-tenant. Biedt tal van functies, waaronder:

* een registerservice voor geïntegreerde toepassingen
* verificatie van gebruikersaccounts en geregistreerde toepassingen
* REST-eindpunten vereist toosupport verschillende protocollen zoals OAuth2 en SAML, met inbegrip van Hallo [autorisatie eindpunt](#authorization-endpoint), [-tokeneindpunt](#token-endpoint) en Hallo 'algemene' eindpunt dat wordt gebruikt door [ multitenant-toepassingen](#multi-tenant-application).

Een tenant is ook gekoppeld aan een Azure AD of Office 365-abonnement tijdens het inrichten van het Hallo-abonnement, Identity & Access Management-functies voorzien in Hallo-abonnement. Zie [hoe tooget een Azure Active Directory-tenant] [ AAD-How-To-Tenant] voor meer informatie over Hallo verschillende manieren krijgt u toegang tooa tenant. Zie [hoe Azure-abonnementen worden gekoppeld aan Azure Active Directory] [ AAD-How-Subscriptions-Assoc] voor meer informatie over het Hallo-relatie tussen abonnementen en Azure AD-tenant.

## <a name="token-endpoint"></a>-Tokeneindpunt
Een van Hallo-eindpunten die zijn geïmplementeerd door Hallo [autorisatie server](#authorization-server) toosupport OAuth2 [toestemming verleent](#authorization-grant). Afhankelijk van Hallo toekennen, het gebruikte tooacquire kan ook een [toegangstoken](#access-token) (en verwante token 'vernieuwen') tooa [client](#client-application), of [token ID](#ID-token) gebruikt in combinatie met Hallo [ OpenID Connect] [ OpenIDConnect] protocol.

## <a name="user-agent-based-client"></a>Client op basis van gebruikers-agent
Een soort [clienttoepassing](#client-application) die code door een webserver gedownload en wordt uitgevoerd binnen een gebruikersagent (bijvoorbeeld een webbrowser), zoals een één pagina toepassing (SPA). Aangezien alle code wordt uitgevoerd op een apparaat, wordt een 'openbare' client vanwege tooits onvermogen toostore referenties privé/vertrouwelijk worden beschouwd. Zie [OAuth2-client van het type en -profielen] [ OAuth2-Client-Types] voor meer informatie.

## <a name="user-principal"></a>UPN
Soortgelijke toohello wijze die een service-principal-object gebruikte toorepresent instantie van een toepassing is, een user principal-object is een ander type beveiligings-principal, waarmee een gebruiker wordt aangeduid. Hello Azure AD Graph [entiteit gebruiker] [ AAD-Graph-User-Entity] definieert Hallo-schema voor een object, met inbegrip van gebruiker-gerelateerde eigenschappen zoals de voornaam en achternaam, UPN-naam, lidmaatschap van de rol directory, enzovoort. Dit biedt Hallo Gebruikersconfiguratie identiteit voor Azure AD-tooestablish een user principal tijdens runtime. Hallo UPN is gebruikte toorepresent een geverifieerde gebruiker voor eenmalige aanmelding, opnemen [toestemming](#consent) overdracht, waardoor de toegang tot het toegangsbeheer, enzovoort.

## <a name="web-client"></a>WebClient
Een soort [clienttoepassing](#client-application) die wordt uitgevoerd alle code op een webserver, en kunnen toofunction als "Vertrouwelijk" client door de referenties veilig opslaan op Hallo-server. Zie [OAuth2-client van het type en -profielen] [ OAuth2-Client-Types] voor meer informatie.

## <a name="next-steps"></a>Volgende stappen
Hallo [Ontwikkelaarshandleiding voor Azure AD] [ AAD-Dev-Guide] is portal toouse hello Azure AD de ontwikkeling van alle verwante onderwerpen, waaronder een overzicht van [toepassingsintegratie] [ AAD-How-To-Integrate] en Hallo basisprincipes van [Azure AD-verificatie en scenario's voor ondersteunde verificatie][AAD-Auth-Scenarios].

Gebruik Hallo opmerkingen sectie tooprovide feedback te volgen en help ons verfijnen en onze inhoud, met inbegrip van aanvragen voor nieuwe definities of voor het bijwerken van bestaande vorm!

<!--Image references-->

<!--Reference style links -->
[AAD-App-Manifest]: ./active-directory-application-manifest.md
[AAD-App-SP-Objects]: ./active-directory-application-objects.md
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Graph-Perm-Scopes]: https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-graph-api-permission-scopes
[AAD-Graph-App-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[AAD-Graph-Sp-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity
[AAD-Graph-User-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity
[AAD-How-Subscriptions-Assoc]: ../active-directory-how-subscriptions-associated-directory.md
[AAD-How-To-Integrate]: ./active-directory-how-to-integrate.md
[AAD-How-To-Tenant]: active-directory-howto-tenant.md
[AAD-Integrating-Apps]: ./active-directory-integrating-applications.md
[AAD-Multi-Tenant-Overview]: active-directory-devhowto-multi-tenant-overview.md
[AAD-Security-Token-Claims]: ./active-directory-authentication-scenarios/#claims-in-azure-ad-security-tokens
[AAD-Tokens-Claims]: ./active-directory-token-and-claims.md
[AZURE-portal]: https://portal.azure.com
[Duyshant-Role-Blog]: http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/
[JWT]: https://tools.ietf.org/html/draft-ietf-oauth-json-web-token-32
[Microsoft-Graph]: https://graph.microsoft.io
[O365-Perm-Ref]: https://msdn.microsoft.com/en-us/office/office365/howto/application-manifest
[OAuth2-Access-Token-Scopes]: https://tools.ietf.org/html/rfc6749#section-3.3
[OAuth2-AuthZ-Endpoint]: https://tools.ietf.org/html/rfc6749#section-3.1
[OAuth2-AuthZ-Grant-Types]: https://tools.ietf.org/html/rfc6749#section-1.3
[OAuth2-Client-Types]: https://tools.ietf.org/html/rfc6749#section-2.1
[OAuth2-Role-Def]: https://tools.ietf.org/html/rfc6749#page-6
[OpenIDConnect]: http://openid.net/specs/openid-connect-core-1_0.html
[OpenIDConnect-AuthZ-Endpoint]: http://openid.net/specs/openid-connect-core-1_0.html#AuthorizationEndpoint
[OpenIDConnect-ID-Token]: http://openid.net/specs/openid-connect-core-1_0.html#IDToken
