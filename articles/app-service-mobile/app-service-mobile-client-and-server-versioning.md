---
title: aaaClient en server SDK-versies in Mobile Apps- en Mobile Services | Microsoft Docs
description: Lijst met client-SDK's en compatibiliteit met versies van de server-SDK voor Mobile Services en Azure Mobile Apps
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 35b19672-c9d6-49b5-b405-a6dcd1107cd5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 5874b7455ea407ca8c77fb1bd03d97d0767ebb47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="client-and-server-versioning-in-mobile-apps-and-mobile-services"></a>Client- en versiebeheer in Mobile Apps- en Mobile Services
Hallo meest recente versie van Azure Mobile Services is Hallo **Mobile Apps** functie van Azure App Service.

Hallo mobiele Apps-client en server SDK's oorspronkelijk zijn gebaseerd op die in Mobile Services, maar ze zijn *niet* compatibel met elkaar.
Dat wil zeggen, moet u een *Mobile Apps* SDK voor clients met een *Mobile Apps* server SDK en op dezelfde manier voor *Mobile Services*. Dit contract wordt afgedwongen via een speciale headerwaarde die wordt gebruikt door Hallo-client en server SDK's, `ZUMO-API-VERSION`.

Opmerking: als dit document tooa verwijst *Mobile Services* backend, hoeft deze niet per se toobe gehost in Mobile Services. Het is nu mogelijk toomigrate een mobiele service toorun op App Service zonder codewijzigingen, maar zou Hallo-service nog steeds gebruikmaken van *Mobile Services* SDK-versies.

informatie over toolearn migreren tooApp Service zonder code wijzigen, Zie Hallo artikel [migreren van een tooAzure Mobile Service-App Service].

## <a name="header-specification"></a>Header-specificatie
Hallo sleutel `ZUMO-API-VERSION` in Hallo HTTP-koptekst of queryreeks Hallo mag worden opgegeven. Hallo-waarde is een versietekenreeks in formulier Hallo **x.y.z**.

Bijvoorbeeld:

Https://service.azurewebsites.net/tables/TodoItem ophalen

HEADERS: ZUMO-API-VERSIE: 2.0.0

POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0

## <a name="opting-out-of-version-checking"></a>Buiten-versiecontrole uitschakelen
U kunt ervoor kiezen niet versie controleren door een waarde van **true** voor app-instelling Hallo **MS_SkipVersionCheck**. Geef dit in uw web.config of in Hallo sectie Toepassingsinstellingen hello Azure-portal.

> [!NOTE]
> Er zijn een aantal gedragswijzigingen tussen Mobile Services en mobiele Apps, met name in Hallo gebieden van het offline synchroniseren, verificatie en pushmeldingen. U moet alleen versiecontrole na volledige testen tooensure dat deze wijzigingen het van uw app-functionaliteit niet breken afmelden.
>
>

## <a name="summary-of-compatibility-for-all-versions"></a>Samenvatting van compatibiliteit voor alle versies
Hallo diagram hieronder toont Hallo compatibiliteit tussen alle typen van client en server. Een back-end is geclassificeerd als beide Mobile **Services** of Mobile **Apps** op basis van Hallo server SDK die wordt gebruikt.

|  | **Mobile Services** Node.js- of .NET | **Mobiele Apps** Node.js- of .NET |
| --- | --- | --- |
| [Mobile Services-clients] |OK |Fout\* |
| [Clients voor mobiele Apps] |Fout\* |OK |

\*Dit kan worden beheerd door te geven **MS_SkipVersionCheck**.

<!-- IMPORTANT!  hello anchors for Mobile Services and Mobile Apps MUST be 1.0.0 and 2.0.0 respectively, since there is an exception error message that uses those anchors. -->

<!-- NOTE: hello fwlink toothis document is http://go.microsoft.com/fwlink/?LinkID=690568 -->

## <a name="1.0.0"></a>Mobile Services-client en server
Hallo client-SDK's in onderstaande tabel voor Hallo compatibel zijn met **Mobile Services**.

Opmerking: Hallo Mobile Services-client-SDK's *niet* een headerwaarde verzenden voor `ZUMO-API-VERSION`. Als het Hallo-service ontvangt deze kop- of queryreekswaarde, een fout geretourneerd, tenzij u expliciet uit zoals hierboven beschreven hebt gekozen.

### <a name="MobileServicesClients"></a>Mobiele *Services* client-SDK's
| Clientplatform | Versie | De versieheaderwaarde |
| --- | --- | --- |
| Beheerde client (Windows, Xamarin) |[1.3.2](https://www.nuget.org/packages/WindowsAzure.MobileServices/1.3.2) |N.v.t. |
| iOS |[2.2.2](http://aka.ms/gc6fex) |N.v.t. |
| Android |[2.0.3](https://go.microsoft.com/fwLink/?LinkID=280126) |N.v.t. |
| HTML |[1.2.7](http://ajax.aspnetcdn.com/ajax/mobileservices/MobileServices.Web-1.2.7.min.js) |N.v.t. |

### <a name="mobile-services-server-sdks"></a>Mobiele *Services* server SDK's
| Server-platform | Versie | Geaccepteerde versie-header |
| --- | --- | --- |
| .NET |[WindowsAzure.MobileServices.Backend.* versie 1.0.x](https://www.nuget.org/packages/WindowsAzure.MobileServices.Backend/) |** Geen versiekop ** |
| Node.js |(binnenkort) |**Er is geen versie-header** |

<!-- TODO: add Node npm version -->

### <a name="behavior-of-mobile-services-backends"></a>Gedrag van de back-ends voor Mobile Services
| ZUMO-API-VERSIE | Waarde van MS_SkipVersionCheck | Antwoord |
| --- | --- | --- |
| Niet opgegeven |Alle |200 - OK |
| Een willekeurige waarde |True |200 - OK |
| Een willekeurige waarde |ONWAAR/niet opgegeven |400 - onjuiste aanvraag |

## <a name="2.0.0"></a>Azure Mobile Apps-client en server
### <a name="MobileAppsClients"></a>Mobiele *Apps* client-SDK's
Beginnen met de volgende versies van Hallo client SDK Hallo versiecontrole is geïntroduceerd voor **Azure Mobile Apps**:

| Clientplatform | Versie | De versieheaderwaarde |
| --- | --- | --- |
| Beheerde client (Windows, Xamarin) |[2.0.0](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/2.0.0) |2.0.0 |
| iOS |[3.0.0](http://go.microsoft.com/fwlink/?LinkID=529823) |2.0.0 |
| Android |[3.0.0](http://go.microsoft.com/fwlink/?LinkID=717033&clcid=0x409) |3.0.0 |

<!-- TODO: add HTML version when released -->

### <a name="mobile-apps-server-sdks"></a>Mobiele *Apps* server SDK's
Versiecontrole is opgenomen in de volgende server SDK-versies:

| Server-platform | SDK | Geaccepteerde versie-header |
| --- | --- | --- |
| .NET |[Microsoft.Azure.Mobile.Server](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) |2.0.0 |
| Node.js |[Azure mobile apps)](https://www.npmjs.com/package/azure-mobile-apps) |2.0.0 |

### <a name="behavior-of-mobile-apps-backends"></a>Gedrag van de back-ends voor mobiele Apps
| ZUMO-API-VERSIE | Waarde van MS_SkipVersionCheck | Antwoord |
| --- | --- | --- |
| x.y.z of Null zijn |True |200 - OK |
| Null |ONWAAR/niet opgegeven |400 - onjuiste aanvraag |
| 1.x.y |ONWAAR/niet opgegeven |400 - onjuiste aanvraag |
| 2.0.0-2.x.y |ONWAAR/niet opgegeven |200 - OK |
| 3.0.0-3.x.y |ONWAAR/niet opgegeven |400 - onjuiste aanvraag |

## <a name="next-steps"></a>Volgende stappen
* [migreren van een tooAzure Mobile Service-App Service]

[Mobile Services-clients]: #MobileServicesClients
[Clients voor mobiele Apps]: #MobileAppsClients


[Mobile App Server SDK]: http://www.nuget.org/packages/microsoft.azure.mobile.server
[migreren van een tooAzure Mobile Service-App Service]: app-service-mobile-migrating-from-mobile-services.md
