---
title: 'Azure Active Directory B2C: toepassingsregistratie | Microsoft Docs'
description: Hoe tooregister uw toepassing met Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: PatAltimore
ms.assetid: 20e92275-b25d-45dd-9090-181a60c99f69
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/13/2017
ms.author: parakhj
ms.openlocfilehash: bd58e123751db387d6c8f16bd010291ba698b1a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-register-your-application"></a>Azure Active Directory B2C: uw toepassing registreren

Met behulp van deze Quickstart kunt u binnen enkele minuten een toepassing registreren in een B2C-tenant van Microsoft Azure Active Directory (Azure AD). Wanneer u klaar bent, wordt uw toepassing geregistreerd voor gebruik in hello Azure B2C-tenant.

## <a name="prerequisites"></a>Vereisten

toobuild een toepassing waarin zich kunnen registreren en aanmelden consumenten, moet u eerst tooregister Hallo toepassing met een Azure Active Directory B2C-tenant. Haal uw eigen tenant met behulp van Hallo stappen die worden beschreven in [een Azure AD B2C-tenant maken](active-directory-b2c-get-started.md).

Toepassingen die zijn gemaakt op basis van hello Azure AD B2C-blade in hello Azure-portal moeten worden beheerd vanaf Hallo dezelfde locatie. Als u Hallo B2C-toepassingen met PowerShell of een andere portal hebt bewerkt, moet deze worden niet ondersteund en werken niet met Azure AD B2C. Zie de details in Hallo [mislukt apps](#faulted-apps) sectie. 

## <a name="navigate-toob2c-settings"></a>Navigeer tooB2C instellingen

Meld u bij toohello [Azure-portal](https://portal.azure.com/) zoals Hallo globale beheerder van Hallo B2C-tenant. 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../../includes/active-directory-b2c-switch-b2c-tenant.md)]

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](../../includes/active-directory-b2c-portal-navigate-b2c-service.md)]

De volgende stappen op basis van het toepassingstype Hallo die u registreert kiezen:

* [Een web-app registreren](#register-a-web-app)
* [Een web-API registreren](#register-a-web-api)
* [Een mobiele of native toepassing registreren](#register-a-mobile-or-native-app)
 
## <a name="register-a-web-app"></a>Een web-app registreren

[!INCLUDE [active-directory-b2c-register-web-app](../../includes/active-directory-b2c-register-web-app.md)]

Als de web-app een web-API aanroept die is beveiligd door Azure AD B2C, voert u deze stappen uit:
   1. Maken van een toepassingsgeheim door te gaan toohello **sleutels** blade en te klikken op Hallo **sleutel genereren** knop. Noteer Hallo **App-sleutel** waarde. Hallo-waarde worden gebruikt als Hallo toepassingsgeheim in de code van uw toepassing.
   2. Klik op **API-toegang**, klik op **Toevoegen** en selecteer uw web-API en bereiken (machtigingen).

> [!NOTE]
> Een **toepassingsgeheim** is een belangrijke beveiligingsreferentie en moet op de juiste wijze worden beveiligd.
> 

[Te gaan**volgende stappen**](#next-steps)

## <a name="register-a-web-api"></a>Een web-API registreren

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

Klik op **gepubliceerd scopes** tooadd meer scopes zo nodig. Standaard is Hallo 'user_impersonation' bereik gedefinieerd. Hallo user_impersonation bereik biedt andere toepassingen Hallo mogelijkheid tooaccess deze api namens Hallo aangemelde gebruiker. Als u wenst, kunt Hallo user_impersonation bereik worden verwijderd.

[Te gaan**volgende stappen**](#next-steps)

## <a name="register-a-mobile-or-native-app"></a>Een mobiele of native toepassing registreren

[!INCLUDE [active-directory-b2c-register-mobile-native-app](../../includes/active-directory-b2c-register-mobile-native-app.md)]

[Te gaan**volgende stappen**](#next-steps)

## <a name="limitations"></a>Beperkingen

### <a name="choosing-a-web-app-or-api-reply-url"></a>De antwoord-URL van een web-app of -API kiezen

Apps die zijn geregistreerd bij Azure AD B2C zijn momenteel beperkt tooa beperkte set waarden voor antwoord-URL. antwoord-URL voor web-apps en services met het schema Hallo beginnen moet Hallo `https`, en alle beantwoorden URL waarden moeten delen één DNS-domein. U kunt bijvoorbeeld geen webtoepassing met een van deze antwoord-URL's registreren:

`https://login-east.contoso.com`

`https://login-west.contoso.com`

Hallo registratie system Vergelijkt Hallo volledige DNS-naam van Hallo bestaande antwoord-URL toohello DNS-naam van Hallo antwoord-URL die u wilt toevoegen. Hallo aanvraag tooadd Hallo DNS-naam mislukt als een van de Hallo volgende voorwaarden is voldaan:

* Hallo hele DNS-naam van de nieuwe antwoord-URL Hallo komt niet overeen met de Hallo DNS-naam van Hallo bestaande antwoord-URL.
* Hallo volledige DNS-naam van Hallo nieuwe antwoord-URL is niet een subdomein van Hallo bestaande antwoord-URL.

Als hello heeft app deze antwoord-URL:

`https://login.contoso.com`

U kunt tooit als volgt toevoegen:

`https://login.contoso.com/new`

In dit geval overeenkomt Hallo DNS-naam exact. Of u kunt dit doen:

`https://new.login.contoso.com`

In dit geval verwijst u tooa DNS-subdomein van login.contoso.com. Als u een app waarvoor aanmelding east.contoso.com en aanmelding-west.contoso.com als URL's beantwoorden toohave wilt, moet u deze antwoord-URL's in deze volgorde toevoegen:

`https://contoso.com`

`https://login-east.contoso.com`

`https://login-west.contoso.com`

U kunt twee laatstgenoemde Hallo toevoegen omdat ze subdomeinen van Hallo eerste antwoord-URL, contoso.com.

### <a name="choosing-a-native-app-redirect-uri"></a>Een omleidings-URI voor een native app kiezen

Er zijn twee belangrijke overwegingen bij het kiezen van een omleidings-URI voor mobiele/native toepassingen:

* **Unieke**: Hallo-schema van Hallo omleidings-URI moet uniek zijn voor elke toepassing. In ons voorbeeld (com.onmicrosoft.contoso.appname://redirect/path) gebruiken we com.onmicrosoft.contoso.appname als Hallo schema. We raden aan dit patroon te volgen. Als twee toepassingen Hallo delen dezelfde schema, hello gebruiker ziet een dialoogvenster 'Kies app'. Als de gebruiker Hallo een onjuiste keuze, Hallo aanmelden is mislukt.
* **Volledig**: de omleidings-URI moet een schema en een pad hebben. Hallo-pad moet ten minste één een slash bevatten na het Hallo-domein (bijvoorbeeld //contoso/ werkt en //contoso mislukt).

Zorg ervoor dat er geen speciale tekens zoals onderstrepingstekens in Hallo omleidings-uri.

### <a name="faulted-apps"></a>Mislukte toepassingen

B2C-toepassingen moeten niet worden bewerkt:

* Op andere appbeheerportals zoals de [klassieke Azure-portal](https://manage.windowsazure.com/) en de [portal voor appregistratie](https://apps.dev.microsoft.com/).
* Met Graph API of PowerShell

Als u Hallo B2C-toepassing bewerken, zoals hierboven wordt beschreven en tooedit probeert opnieuw in hello Azure AD B2C-functiesblade op Hallo van Azure-portal, wordt een fout-app en uw toepassing is niet langer bruikbaar met Azure AD B2C. U hebt toodelete Hallo toepassing en maak deze opnieuw.

Ga toohello-app Hallo toodelete [toepassing Registratieportal](https://apps.dev.microsoft.com/) en er Hallo toepassing verwijderen. Opdat Hallo toepassing toobe zichtbaar is moet u toobe Hallo eigenaar van de toepassing hello (en niet alleen een beheerder van Hallo tenant).

## <a name="next-steps"></a>Volgende stappen

Nu dat u een toepassing die is geregistreerd bij Azure AD B2C hebt, kunt u een van voltooien [onze zelfstudies snel starten](active-directory-b2c-overview.md#get-started) tooget zetten.

> [!div class="nextstepaction"]
> [Een ASP.NET-web-app maken met registreren, aanmelden en wachtwoord opnieuw instellen](active-directory-b2c-devquickstarts-web-dotnet-susi.md)