---
title: aaaAuthentication en autorisatie in Azure App Service | Microsoft Docs
description: Voor conceptuele verwijzing en overzicht van Hallo verificatie / autorisatie-functie voor Azure App Service
services: app-service
documentationcenter: 
author: mattchenderson
manager: erikre
editor: 
ms.assetid: b7151b57-09e5-4c77-a10c-375a262f17e5
ms.service: app-service
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 08/29/2016
ms.author: mahender
ms.openlocfilehash: dc2074b16cce47b72b78ea7afeda89dbc4832166
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-in-azure-app-service"></a>Verificatie en autorisatie in Azure App Service
## <a name="what-is-app-service-authentication--authorization"></a>Wat is er App Service-verificatie / autorisatie?
App Service-verificatie / autorisatie is een functie die een manier voor uw toepassing toosign in gebruikers, biedt zodat u geen toochange code op Hallo app back-end hebt. Het biedt een eenvoudige manier tooprotect uw toepassing en werk gegevens per gebruiker.

App Service maakt gebruik van federatieve identiteiten, waarbij een derde partij identiteitsprovider accounts worden opgeslagen en verificatie van gebruikers. Hallo-toepassing is afhankelijk van de gegevens van de identiteit van de provider Hallo zodat hello app heeft geen toostore die informatie zelf. App Service ondersteunt vijf identiteitsproviders out of box Hallo: Azure Active Directory, Facebook, Google, Microsoft-Account en Twitter. Uw app kunt gebruiken een willekeurig aantal deze identiteit providers tooprovide uw gebruikers met opties voor hoe ze zich aanmelden. ingebouwde ondersteuning tooexpand hello, kunt u een andere identiteitsprovider integreren of [uw eigen aangepaste identiteitsoplossing][custom-auth].

Als u tooget meteen gestart wilt, ziet u een van de volgende zelfstudies Hallo:

* [Verificatie tooyour iOS-app toevoegen] [ iOS] (of [Android], [Windows], [Xamarin.iOS], [ Xamarin.Android], [Xamarin.Forms], of [Cordova])
* [Gebruikersverificatie voor API-Apps in Azure App Service][apia-user]
* [Aan de slag met Azure App Service - deel 2][web-getstarted]

## <a name="how-authentication-works-in-app-service"></a>De werking van verificatie in App Service
In de volgorde tooauthenticate met behulp van een id-providers hello, moet u eerst tooconfigure Hallo identiteit provider tooknow over uw toepassing. Hallo-identiteitsprovider Geef vervolgens-id's en geheimen tooApp Service op te geven. Dit is voltooid Hallo vertrouwensrelatie zodat App Service kunt controleren of de gebruiker asserties, zoals verificatietokens van Hallo id-provider.

toosign in een gebruiker met behulp van een van deze providers moet Hallo gebruiker omgeleide tooan-eindpunt dat gebruikers zich voor die provider. Als klanten een webbrowser gebruikt, kunt u automatisch alle niet-geverifieerde gebruikers toohello-eindpunt dat gebruikers worden aangemeld directe-App Service kunt hebben. Anders moet u toodirect uw klanten te`{your App Service base URL}/.auth/login/<provider>`, waarbij `<provider>` is een van de volgende waarden Hallo: aad, facebook, google en microsoft- of twitter. Mobiele en API-scenario's worden in de secties verderop in dit artikel beschreven.

Een cookie instellen, zodat ze geverifieerde blijven kunnen als ze door uw toepassing bladeren hebben gebruikers die met uw toepassing via een webbrowser werken. Voor andere clienttypen, zoals mobile, een JSON web token (JWT), die moet worden gepresenteerd in Hallo `X-ZUMO-AUTH` header toohello client worden uitgegeven. Hallo Mobile Apps client-SDK's verwerken dit voor u. U kunt ook een token van Azure Active Directory-identiteit of het toegangstoken mogelijk rechtstreeks opgenomen in Hallo `Authorization` header als een [bearer-token](https://tools.ietf.org/html/rfc6750).

App Service valideert een cookie of dat uw toepassing tooauthenticate gebruikers problemen token. toorestrict wie toegang tot uw toepassing hello Zie [autorisatie](#authorization) verderop in dit artikel.

### <a name="mobile-authentication-with-a-provider-sdk"></a>Mobiele verificatie met een provider SDK
Nadat u alles is geconfigureerd op Hallo back-end, kunt u mobiele clients toosign met App Service wijzigen. Er zijn twee benaderingen hier:

* Gebruik een SDK dat een opgegeven identiteitsprovider tooestablish identiteit publiceert en vervolgens toegang tooApp Service krijgen.
* Gebruik één regel code zodat Hallo Mobile Apps client SDK gebruikers kunt aanmelden.

> [!TIP]
> De meeste toepassingen moeten gebruiken voor een provider SDK tooget een consistente gebruikerservaring wanneer gebruikers zich aanmelden, ondersteuning voor het vernieuwen van toouse en tooget andere voordelen die Hallo-provider bevat.
> 
> 

Wanneer u een provider SDK, kunnen gebruikers zich aanmelden wordt tooan ervaring die dichter met Hallo-besturingssysteem die Hallo-app integreert op uitgevoerd. Dit biedt u eveneens-token van een provider en bepaalde gebruikersgegevens op Hallo client, maakt het veel eenvoudiger tooconsume graph API's en gebruikerservaring Hallo aanpassen. Van tijd tot tijd van blogs en forums, ziet u deze waarnaar wordt verwezen tooas Hallo 'stroom' of 'client omgeleid stroom' omdat de code op Hallo-client ondertekent in gebruikers en het Hallo-clientcode is toegangstoken tooa provider.

Wanneer een provider-token wordt ontvangen, moet deze toobe verzonden tooApp Service voor validatie. Nadat de App Service valideert Hallo token, maakt de App Service een nieuw App Service-token dat toohello client wordt geretourneerd. Hallo Mobile Apps client SDK heeft helper methoden toomanage deze exchange- en automatisch koppelen Hallo token tooall aanvragen toohello toepassing back-end. Ontwikkelaars kunnen ook een verwijzing toohello provider token behouden desgewenst.

### <a name="mobile-authentication-without-a-provider-sdk"></a>Mobiele verificatie zonder een SDK-provider
Als u niet dat tooset een SDK-provider wilt, kunt u Hallo Mobile Apps-functie van toosign in Azure App Service kunt u toestaan. Hallo Mobile Apps client SDK wordt opent u een web-toohello-provider voor weergave van uw keuze en Hallo gebruiker aanmelden. Tijd tot tijd op de blogs en forums ziet u deze waarnaar wordt verwezen tooas Hallo 'server stroom' of 'server gerichte stroom' omdat Hallo-server wordt beheerd Hallo-proces dat gebruikers worden aangemeld en Hallo client SDK nooit Hallo provider token ontvangt.

Code toostart die deze stroom is opgenomen in Hallo verificatie zelfstudie voor elk platform. Aan het einde van de Hallo van Hallo stroom, Hallo client SDK heeft een App Service-token en Hallo-token is automatisch gekoppelde tooall aanvragen toohello toepassing back-end.

### <a name="service-to-service-authentication"></a>Verificatie van service-tot-service
Hoewel u gebruikers toegang tooyour toepassing op te geven kunt, kunt u ook vertrouwen een andere toepassing toocall uw eigen API. Bijvoorbeeld, kunnen u een web-app een API-aanroep in een andere web-app hebben. In dit scenario moet u referenties gebruikt voor een serviceaccount in plaats van de gebruiker referenties tooget een token. Een service-account wordt ook wel een *service-principal* in Azure Active Directory-jargon en authenticatie die gebruikmaakt van zo'n account wordt ook wel bekend als een service-naar-service-scenario.

> [!IMPORTANT]
> Omdat mobiele apps worden uitgevoerd op apparaten van de klant, mobiele toepassingen doen *niet* tellen als vertrouwde toepassingen en moet een service-principal stroom niet gebruiken. In plaats daarvan moeten ze gebruiken in de gebruikersstroom van een die eerder is beschreven.
> 
> 

App Service kunt uw toepassing beveiligen met behulp van Azure Active Directory voor scenario's met service-naar-service. de aanroepende toepassing Hello moet net tooprovide een Azure Active Directory service principal verificatietoken die wordt verkregen door Hallo client-ID en geheime van Azure Active Directory-client. Een voorbeeld van dit scenario die gebruikmaakt van ASP.NET-API-apps wordt uitgelegd in Hallo-zelfstudie [principal verificatie van de Service voor API-Apps][apia-service].

Als u toouse toohandle van App Service-verificatie een scenario voor service-naar-service wilt, kunt u clientcertificaten of basisverificatie. Zie voor informatie over clientcertificaten in Azure, [hoe tooConfigure TLS wederzijdse verificatie voor Web-Apps](../app-service-web/app-service-web-configure-tls-mutual-auth.md). Zie voor meer informatie over basisverificatie in ASP.NET [verificatie-Filters in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/authentication-filters).

Verificatie van de service-account van een App Service logic app tooan API-app is een speciaal geval die wordt beschreven in [uw aangepaste API gebruiken die worden gehost op App Service met Logic apps](../logic-apps/logic-apps-custom-hosted-api.md).

## <a name="authorization"></a>De werking van autorisatie in App Service
Hebt u volledige controle over Hallo-aanvragen die toegang uw toepassing tot. App Service-verificatie / autorisatie kan worden geconfigureerd met een van de volgende gedragingen Hallo:

* Toestaan dat alleen geverifieerde aanvragen tooreach uw toepassing.
  
    Als een browser een anonieme aanvraag ontvangt, worden de App Service tooa pagina voor Hallo-identiteitsprovider die u kiest, zodat gebruikers zich kunnen aanmelden omgeleid. Als Hallo aanvraag afkomstig zijn van een mobiel apparaat, Hallo geretourneerd antwoord is een HTTP *401 niet geautoriseerd* antwoord.
  
    Met deze optie hoeft u geen toowrite een verificatiecode op te geven op alle in uw app. Als u moet de mate autorisatie, wordt informatie over Hallo gebruiker beschikbaar tooyour code.
* Toestaan van alle aanvragen tooreach uw toepassing, maar geverifieerde aanvragen valideren en doorgegeven verificatiegegevens in Hallo HTTP-headers.
  
    Deze optie past omleiding autorisatie beslissingen tooyour toepassingscode. Biedt dit meer flexibiliteit bij het anonieme aanvragen voor de verwerking, maar er toowrite code.
* Alle aanvragen tooreach kan uw toepassing en geen actie onderneemt op verificatiegegevens in Hallo aanvragen.
  
    In dit geval Hallo verificatie / autorisatie-functie is uitgeschakeld. Hallo-taken voor verificatie en autorisatie zijn volledig tooyour toepassingscode.

Hallo vorige gedrag worden beheerd door Hallo **tootake actie wanneer de aanvraag is niet geverifieerd** optie in hello Azure-portal. Als u ervoor kiest ** Meld u aan met *providernaam* **, alle aanvragen hebben toobe geverifieerd. **Laat de aanvraag (geen actie)** past omleiding Hallo besluit tooyour autorisatiecode, maar nog steeds biedt verificatie-informatie. Als u wilt dat toohave uw code alles verwerken, kunt u uitschakelen Hallo verificatie / autorisatie-functie.

## <a name="working-with-user-identities-in-your-application"></a>Werken met gebruikers-id's in uw toepassing
App Service een gebruiker informatie tooyour toepassing met behulp van speciale kopteksten is geslaagd. Externe aanvragen verbieden deze koppen en wordt alleen aanwezig als ingesteld door App Service-verificatie / autorisatie. Er zijn enkele koppen voorbeeld:

* X-MS-CLIENT-PRINCIPAL-NAAM
* X-MS-CLIENT-PRINCIPAL-ID
* X-MS-TOKEN-FACEBOOK-ACCESS-TOKEN
* X-MS-TOKEN-FACEBOOK-EXPIRES-ON

Code die is geschreven in elke taal of elk framework krijgen van deze koppen Hallo-informatie die nodig is. Voor ASP.NET 4.6-apps Hallo **claimsprincipal is** automatisch ingesteld met de juiste waarden Hallo.

Uw toepassing krijgt ook aanvullende gegevens via een HTTP GET op Hallo `/.auth/me` eindpunt van uw toepassing. Een geldig token dat is opgenomen in het Hallo-aanvraag wordt retourneren een JSON-nettolading met informatie over het Hallo-provider die wordt gebruikt, Hallo van de onderliggende provider-token en sommige andere gegevens van de gebruiker. Hallo server Mobile Apps SDK's bieden Help-methoden toowork met deze gegevens. Zie voor meer informatie [hoe toouse hello Azure Mobile Apps Node.js SDK](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#howto-tables-getidentity), en [werken met back-endserver voor Hallo .NET SDK voor Azure Mobile Apps](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#user-info).

## <a name="documentation-and-additional-resources"></a>Documentatie en aanvullende bronnen
### <a name="identity-providers"></a>Id-providers
Hallo volgende zelfstudies tonen hoe tooconfigure App Service toouse verschillende verificatieproviders:

* [Hoe tooconfigure uw app toouse Azure Active Directory-aanmelding][AAD]
* [Hoe tooconfigure uw app toouse Facebook-aanmelding][Facebook]
* [Hoe tooconfigure uw app toouse Google-aanmelding][Google]
* [Hoe tooconfigure uw aanmelding app toouse Microsoft-Account][MSA]
* [Hoe tooconfigure uw app toouse Twitter-aanmelding][Twitter]

Als u wilt dat een identiteitssysteem toouse dan Hallo zijn opgegeven, kunt u ook hello gebruiken [preview-ondersteuning voor aangepaste verificatie in server Hallo-Mobile Apps .NET SDK][custom-auth], die kan worden gebruikt in web-apps mobiele apps of API-apps.

### <a name="web-applications"></a>Web-apps
Hallo volgende zelfstudies wordt uitgelegd hoe tooadd verificatie tooa webtoepassing:

* [Aan de slag met Azure App Service - deel 2][web-getstarted]

### <a name="mobile-applications"></a>Mobiele toepassingen
Hallo volgende zelfstudies tonen hoe tooadd verificatie tooyour mobiele clients met behulp van server gerichte stroom Hallo:

* [Verificatie tooyour iOS-app toevoegen][iOS]
* [Verificatie tooyour Android-app toevoegen][Android]
* [Toevoegen van Windows-app voor verificatie tooyour][Windows]
* [Verificatie tooyour Xamarin.iOS-app toevoegen][Xamarin.iOS]
* [Verificatie tooyour Xamarin.Android-app toevoegen][ Xamarin.Android]
* [Verificatie tooyour Xamarin.Forms-app toevoegen][Xamarin.Forms]
* [Verificatie tooyour Cordova-app toevoegen][Cordova]

Hallo resources te volgen als u toouse Hallo client omgeleid stroom voor Azure Active Directory wilt gebruiken:

* [Gebruik Hallo Active Directory Authentication Library voor iOS][ADAL-iOS]
* [Hallo Active Directory Authentication Library voor Android gebruiken][ADAL-Android]
* [Hallo Active Directory Authentication Library voor Windows en Xamarin gebruiken][ADAL-dotnet]

Resources te volgen als u wilt dat toouse Hallo client omgeleid stroom voor Facebook hello gebruiken:

* [Gebruik Hallo Facebook SDK voor iOS](../app-service-mobile/app-service-mobile-ios-how-to-use-client-library.md#facebook-sdk)

Resources te volgen als u wilt dat toouse Hallo client omgeleid stroom voor Twitter hello gebruiken:

* [Gebruik Twitter Fabric voor iOS](../app-service-mobile/app-service-mobile-ios-how-to-use-client-library.md#twitter-fabric)

Resources te volgen als u wilt dat toouse Hallo client omgeleid stroom voor Google hello gebruiken:

* [Gebruik Hallo Google-In SDK voor iOS](../app-service-mobile/app-service-mobile-ios-how-to-use-client-library.md#google-sdk)

### <a name="api-applications"></a>API-toepassingen
Hallo volgende zelfstudies tonen hoe tooprotect uw API-apps:

* [Gebruikersverificatie voor API-Apps in Azure App Service][apia-user]
* [Verificatie van service-principal voor API Apps in Azure App Service][apia-service]

[apia-user]: ../app-service-api/app-service-api-dotnet-user-principal-auth.md
[apia-service]: ../app-service-api/app-service-api-dotnet-service-principal-auth.md

[web-getstarted]: ../app-service-web/app-service-web-get-started-2.md#authenticate-your-users

[iOS]: ../app-service-mobile/app-service-mobile-ios-get-started-users.md
[Android]: ../app-service-mobile/app-service-mobile-android-get-started-users.md
[Xamarin.iOS]: ../app-service-mobile/app-service-mobile-xamarin-ios-get-started-users.md
[ Xamarin.Android]: ../app-service-mobile/app-service-mobile-xamarin-android-get-started-users.md
[Xamarin.Forms]: ../app-service-mobile/app-service-mobile-xamarin-forms-get-started-users.md
[Windows]: ../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-users.md
[Cordova]: ../app-service-mobile/app-service-mobile-cordova-get-started-users.md

[AAD]: ../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md
[Facebook]: ../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md
[Google]: ../app-service-mobile/app-service-mobile-how-to-configure-google-authentication.md
[MSA]: ../app-service-mobile/app-service-mobile-how-to-configure-microsoft-authentication.md
[Twitter]: ../app-service-mobile/app-service-mobile-how-to-configure-twitter-authentication.md

[custom-auth]: ../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#custom-auth

[ADAL-Android]: ../app-service-mobile/app-service-mobile-android-how-to-use-client-library.md#adal
[ADAL-iOS]: ../app-service-mobile/app-service-mobile-ios-how-to-use-client-library.md#adal
[ADAL-dotnet]: ../app-service-mobile/app-service-mobile-dotnet-how-to-use-client-library.md#adal
