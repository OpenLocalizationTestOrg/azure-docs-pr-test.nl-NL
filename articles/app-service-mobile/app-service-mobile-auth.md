---
title: aaaAuthentication en autorisatie in Azure Mobile Apps | Microsoft Docs
description: Voor conceptuele verwijzing en overzicht van Hallo verificatie / autorisatie-functie voor Azure Mobile Apps
services: app-service\mobile
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: a46dbf70-867d-48f6-8885-7f5207ad102e
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 5255734481ada11afb65982aebe45c2a349402fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-in-azure-mobile-apps"></a>Verificatie en autorisatie in Azure Mobile Apps
## <a name="what-is-app-service-authentication--authorization"></a>Wat is er App Service-verificatie / autorisatie?
> [!NOTE]
> In dit onderwerp worden de gemigreerde tooa geconsolideerd [App Service-verificatie / autorisatie](../app-service/app-service-authentication-overview.md) onderwerp bevat informatie over mobiele-, Web- en API-Apps.
> 
> 

App Service-verificatie / autorisatie is een functie waarmee uw toepassing toolog gebruikers zonder code wijzigingen voor back-end Hallo app vereist. Het biedt een eenvoudige manier tooprotect uw toepassing en werk gegevens per gebruiker.

App Service maakt gebruik van federatieve identiteiten waarin 3rd derden **identiteitsprovider** ('IDP') accounts worden opgeslagen en verifieert gebruikers en toepassing hello gebruikt deze identiteit in plaats van een eigen. App Service ondersteunt vijf identiteitsproviders out of box Hallo: *Azure Active Directory*, *Facebook*, *Google*, *Microsoft-Account*, en *Twitter*. U kunt ook deze ondersteuning voor uw apps uitbreiden door te integreren van een andere id-provider of een oplossing voor uw eigen aangepaste identiteit.

Uw app kunt gebruikmaken van een willekeurig aantal deze id-providers, zodat u uw eindgebruikers met opties leveren kan voor hoe ze zich aanmelden.

Als u tooget meteen gestart wenst, vindt u in een van de volgende zelfstudies Hallo:

* [Verificatie tooyour iOS-app toevoegen]
* [Verificatie tooyour Xamarin.iOS-app toevoegen]
* [Verificatie tooyour Xamarin.Android-app toevoegen]
* [Verificatie tooyour Windows-app toevoegen]

## <a name="how-authentication-works"></a>De werking van verificatie
In de volgorde tooauthenticate met een id-providers hello, moet u eerst tooconfigure Hallo identiteit provider tooknow over uw toepassing. Hallo-identiteitsprovider krijgt u vervolgens met de id's en geheimen back toohello toepassing op te geven. Dit Hallo vertrouwensrelatie is voltooid en kunt App Service toovalidate identiteiten opgegeven tooit.

Deze stappen zijn aangegeven in de volgende onderwerpen Hallo:

* [Hoe tooconfigure uw app toouse Azure Active Directory-aanmelding]
* [Hoe tooconfigure uw app toouse Facebook-aanmelding]
* [Hoe tooconfigure uw app toouse Google-aanmelding]
* [Hoe tooconfigure uw aanmelding app toouse Microsoft-Account]
* [Hoe tooconfigure uw app toouse Twitter-aanmelding]

Zodra u alles is geconfigureerd op Hallo back-end, kunt u uw client-toolog in wijzigen. Er zijn twee benaderingen hier:

* Met behulp van één regel code kunt Hallo Mobile Apps client SDK Meld u aan gebruikers.
* Gebruik een SDK gepubliceerd door een bepaalde identiteit provider tooestablish identiteit en vervolgens krijgen toegang tooApp Service.

> [!TIP]
> De meeste toepassingen moeten een provider SDK-tooget gebruiken een systeemeigen gevoel aanmeldingservaring en tooleverage vernieuwen ondersteuning en andere providerspecifieke voordelen.
> 
> 

### <a name="how-authentication-without-a-provider-sdk-works"></a>De werking van de verificatie zonder een SDK-provider
Als u niet dat tooset een SDK-provider wenst, kunt u Mobile Apps tooperform Hallo aanmelding toestaan voor u. Hallo Mobile Apps client SDK opent een web weergave toohello leverancier van uw kiezen en volledig Hallo aanmelding. Van tijd tot tijd op de blogs en forums u ziet dit tooas Hallo 'server stroom' genoemd of 'server gerichte stroom' sinds de server Hallo Hallo aanmelding beheert en Hallo client SDK nooit Hallo provider token ontvangt.

Hallo code nodig toostart die deze stroom wordt besproken in Hallo verificatie zelfstudie voor elk platform. Aan het einde van de Hallo van Hallo stroom, Hallo client SDK heeft een App Service-token en Hallo-token is automatisch gekoppelde tooall aanvragen toohello back-end.

### <a name="how-authentication-with-a-provider-sdk-works"></a>De werking van verificatie met een provider SDK
Werken met een provider SDK kunt Hallo aanmelding toointeract dichter bij Hallo-platform OS Hallo app wordt uitgevoerd. Dit biedt u eveneens-token van een provider en bepaalde gebruikersgegevens op Hallo client, maakt het veel eenvoudiger tooconsume graph API's en gebruikerservaring Hallo aanpassen. Tijd tot tijd op de blogs en forums ziet u deze waarnaar wordt verwezen tooas Hallo 'stroom' of 'client omgeleid stroom' sinds de code op Hallo client verwerkt Hallo aanmelding en Hallo clientcode toegangstoken tooa provider heeft.

Nadat u een provider-token wordt ontvangen, moet deze toobe verzonden tooApp Service voor validatie. Aan het einde van de Hallo van Hallo stroom, Hallo client SDK heeft een App Service-token en Hallo-token is automatisch gekoppelde tooall aanvragen toohello back-end. Hallo ontwikkelaars kan ook een verwijzing toohello provider token behouden desgewenst.

## <a name="how-authorization-works"></a>De werking van autorisatie
App Service-verificatie / autorisatie beschrijft de verschillende mogelijkheden voor **tootake actie wanneer de aanvraag is niet geverifieerd**. Voordat u uw code een bepaalde aanvraag ontvangt, kunt u App Service selectievakje toosee hebben als Hallo-aanvraag is geverifieerd en als dat niet weigeren en toohave Hallo-gebruiker aanmelden voordat u probeert het opnieuw proberen.

Een mogelijkheid is toohave niet-geverifieerde aanvragen omleiden tooone van Hallo id-providers. In een webbrowser, zou dit daadwerkelijk Hallo gebruiker tooa nieuwe pagina duren. Echter uw mobiele clients niet op deze manier worden omgeleid en niet-geverifieerde antwoorden ontvangt een HTTP *401 niet geautoriseerd* antwoord. Daardoor vormen de eerste aanvraag Hallo de client maakt moet altijd toohello aanmelding eindpunt en vervolgens kunt u tooany andere API-aanroepen. Als u een ander API toocall probeert voordat u zich aanmeldt, ontvangt de client een fout opgetreden.

Als u toohave gedetailleerdere bepalen via welke eindpunten verificatie vereisen, kunt u kiezen "Er is geen actie (toestaan aanvraag) ' voor niet-geverifieerde aanvragen. In dit geval alle beslissingen voor de verificatie worden uitgesteld tooyour toepassingscode. Hierdoor kunt u ook tooallow-toospecific gebruikers op basis van regels voor aangepaste autorisatie.

## <a name="documentation"></a>Documentatie
Hallo volgende zelfstudies tonen hoe tooadd verificatie tooyour mobiele clients met behulp van App Service:

* [Verificatie tooyour iOS-app toevoegen]
* [Verificatie tooyour Xamarin.iOS-app toevoegen]
* [Verificatie tooyour Xamarin.Android-app toevoegen]
* [Verificatie tooyour Windows-app toevoegen]

Hallo volgende zelfstudies tonen hoe tooconfigure App Service tooleverage verschillende verificatieproviders:

* [Hoe tooconfigure uw app toouse Azure Active Directory-aanmelding]
* [Hoe tooconfigure uw app toouse Facebook-aanmelding]
* [Hoe tooconfigure uw app toouse Google-aanmelding]
* [Hoe tooconfigure uw aanmelding app toouse Microsoft-Account]
* [Hoe tooconfigure uw app toouse Twitter-aanmelding]

Als u toouse een identiteitssysteem dan wenst Hallo toepassingsgroepen opgegeven hier u van Hallo gebruikmaken kunt [preview-ondersteuning voor aangepaste verificatie Hallo .NET Server SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#custom-auth).

[Verificatie tooyour iOS-app toevoegen]: app-service-mobile-ios-get-started-users.md
[Verificatie tooyour Xamarin.iOS-app toevoegen]: app-service-mobile-xamarin-ios-get-started-users.md
[Verificatie tooyour Xamarin.Android-app toevoegen]: app-service-mobile-xamarin-android-get-started-users.md
[Verificatie tooyour Windows-app toevoegen]: app-service-mobile-windows-store-dotnet-get-started-users.md

[Hoe tooconfigure uw app toouse Azure Active Directory-aanmelding]: app-service-mobile-how-to-configure-active-directory-authentication.md
[Hoe tooconfigure uw app toouse Facebook-aanmelding]: app-service-mobile-how-to-configure-facebook-authentication.md
[Hoe tooconfigure uw app toouse Google-aanmelding]: app-service-mobile-how-to-configure-google-authentication.md
[Hoe tooconfigure uw aanmelding app toouse Microsoft-Account]: app-service-mobile-how-to-configure-microsoft-authentication.md
[Hoe tooconfigure uw app toouse Twitter-aanmelding]: app-service-mobile-how-to-configure-twitter-authentication.md
