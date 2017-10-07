---
title: aaaAPI Apps Inleiding | Microsoft Docs
description: Lees hoe Azure App Service u helpt bij het ontwikkelen, hosten en gebruiken van RESTful-API's.
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 60049a16-8159-47aa-a34b-110be0d8dab6
ms.service: app-service-api
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2016
ms.author: alkarche
ms.openlocfilehash: f066e96db667d4685480001bc43c2b1bff4ea352
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="api-apps-overview"></a>Overzicht van API Apps
API-apps in Azure App Service-aanbieding functies waarmee u gemakkelijker toodevelop hosten en API's in Hallo cloud en on-premises gebruiken. Met API-apps beschikt u over hoogwaardige beveiliging, eenvoudig toegangsbeheer, hybride verbindingen, automatisch genereren van SDK's en naadloze integratie met [Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md).

[De Azure App Service](../app-service/app-service-value-prop-what-is.md) is een volledig beheerd platform voor web- en integratiescenario's en mobiele scenario's. API Apps zijn een van de vier typen apps die worden aangeboden door [Azure App Service](../app-service/app-service-value-prop-what-is.md).

![App-typen in Azure App Service](./media/app-service-api-apps-why-best-platform/appservicesuite.png)

## <a name="why-use-api-apps"></a>Waarom API Apps gebruiken?
Hierna ziet u een aantal belangrijke voordelen van API Apps:

* **Laat uw bestaande API ongewijzigd-is** - u hebt geen toochange van Hallo code in uw bestaande API's tootake voordeel van API Apps--hoeft uw code tooan API-app te implementeren. Voor de API kan elke taal of elk framework worden gebruikt dat wordt ondersteund door App Service, waaronder ASP.NET en C#, Java, PHP, Node.js en Python.
* **Eenvoudig gebruik**: door de geïntegreerde ondersteuning voor [Swagger API-metagegevens](http://swagger.io/) kunnen uw API's eenvoudig worden gebruikt door diverse clients.  Genereer clientcode automatisch voor uw API's in diverse talen, waaronder C#, Java, en Javascript. Configureer [CORS](app-service-api-cors-consume-javascript.md) eenvoudig, zonder uw code te wijzigen. Zie [API Apps-metagegevens van App Service voor het detecteren en genereren van code](app-service-api-metadata.md) en [Een API-app van JavaScript gebruiken met CORS](app-service-api-cors-consume-javascript.md) voor meer informatie. 
* **Eenvoudig toegangsbeheer** -API-app beveiligen tegen niet-geverifieerde toegang niets wijzigingen tooyour code. Met ingebouwde verificatieservices worden API's beveiligd tegen toegang door andere services of door clients waarmee gebruikers worden aangegeven. Ondersteunde identiteitsproviders zijn onder andere Azure Active Directory, Facebook, Twitter, Google en Microsoft-account. Clients kunnen Active Directory Authentication Library (ADAL) of Hallo Mobile Apps SDK gebruiken. Zie [Verificatie en autorisatie voor API Apps in Azure App Service](app-service-api-authentication.md) voor meer informatie.
* **Visual Studio-integratie** -specifieke hulpprogramma's in Visual Studio stroomlijnen Hallo maken, implementeren, verbruikt, foutopsporing en API-apps beheren. Zie voor meer informatie [Announcing hello Azure SDK 2.8.1 voor .NET](https://azure.microsoft.com/blog/announcing-azure-sdk-2-8-1-for-net/).
* **Integratie met Logic Apps**: API Apps die u maakt, kunnen worden gebruikt door [App Service Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md).  Zie [Uw aangepaste API gebruiken die op App Service wordt gehost met logische apps](../logic-apps/logic-apps-custom-hosted-api.md) en [Nieuwe previewschemaversie 2015-08-01](../logic-apps/logic-apps-schema-2015-08-01.md) voor meer informatie.

Daarnaast kunt u met een API-app gebruikmaken van functies die worden aangeboden door [Web Apps](../app-service-web/app-service-web-overview.md) en [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md). Hallo omgekeerde geldt ook: als u een web-app of mobiele app toohost een API gebruikt, deze kunt profiteren van de API-Apps functies zoals Swagger-metagegevens voor genereren van clientcode en CORS voor browsertoegang in meerdere domeinen toegang. Hallo is het enige verschil tussen Hallo drie app-typen (API, web, mobiel) Hallo naam en het pictogram dat wordt gebruikt voor hen in hello Azure-portal.

## <a name="whats-hello-difference-between-api-apps-and-azure-api-management"></a>Wat is Hallo verschil tussen API Apps en Azure API Management?
API Apps en [Azure API Management](../api-management/api-management-key-concepts.md) zijn aanvullende services:

* API Management is bedoeld voor het beheer van API's. U een front-end voor API Management in een API-toomonitor plaatsen en gebruik beperken, invoer en uitvoer te manipuleren, verschillende API's samenvoegen in één eindpunt, enzovoort. Hallo API's die worden beheerd, kan overal worden gehost.
* API Apps is bedoeld om API's te hosten. Hallo-service bevat functies waarmee u eenvoudiger API's ontwikkelen en gebruiken, maar deze bevat niet Hallo soorten bewaking, beperking, bewerken of consolideren dat API Management biedt. Als u geen API Management-functies nodig hebt, kunt u API's hosten in API-apps zonder hiervoor API Management te gebruiken.

Hier ziet u een diagram waarin API Management wordt gebruikt voor API's die in API-apps en op andere locaties worden gehost.

![Azure API Management en API Apps](./media/app-service-api-apps-why-best-platform/apia-apim.png)

Sommige voorzieningen van API Management en API Apps hebben soortgelijke functies.  Met beide kan bijvoorbeeld CORS-ondersteuning worden geautomatiseerd. Wanneer u Hallo twee services samen gebruikt, gebruikt u API Management voor CORS omdat deze fungeert als front-end tooyour API apps Hallo. 

## <a name="getting-started"></a>Aan de slag
tooget gaan met API-Apps implementeren voorbeeld code tooone, Zie Hallo-zelfstudie voor het gewenste framework u liever:

* [ASP.NET](app-service-api-dotnet-get-started.md) 
* [Node.js](app-service-api-nodejs-api-app.md) 
* [Java](app-service-api-java-api-app.md) 

vragen over API-apps tooask begin een thread in Hallo [API Apps-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureAPIApps). 

