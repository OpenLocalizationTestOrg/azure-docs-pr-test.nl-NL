---
title: aaaAzure App Service voor web-, mobiele en API-apps | Microsoft Docs
description: Lees hoe u met Azure App Service web-apps en mobiele apps kunt ontwikkelen, implementeren en beheren.
keywords: app service, azure app service, kosten app service, schaal, schaalbaar, implementatie app, implementatie azure app, paas, platform as a service, website, web site, web, azure mobiel
services: app-service
documentationcenter: 
author: omarkmsft
manager: erikre
editor: cephalin
ms.assetid: 979cafa8-eeb6-4d3b-87cf-764a821c3e4f
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/02/2016
ms.author: byvinyal
ms.openlocfilehash: 22f414c7d79092d87406a8d3538b946881fb4580
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-app-service"></a>Wat is Azure App Service?
*App Service* is een [Platform as a Service](https://en.wikipedia.org/wiki/Platform_as_a_service)-product (PaaS) van Microsoft Azure. Maak web-apps en mobiele apps voor alle platforms en apparaten. Integreer uw apps met SaaS-oplossingen, maak verbinding met on-premises toepassingen en automatiseer uw bedrijfsprocessen. Met Azure worden uw apps uitgevoerd op volledig beheerde virtuele machines (VM's), waarbij u kunt kiezen uit gedeelde VM-resources of toegewezen VM's.

App Service bevat Hallo web en mobiel mogelijkheden die we eerder afzonderlijk verkrijgbaar Azure Websites en Azure Mobile Services. Deze service bevat ook nieuwe mogelijkheden voor het automatiseren van bedrijfsprocessen en het hosten van cloud-API's. Omdat App Service één geïntegreerde service is, kunt u diverse onderdelen, waaronder websites, back-ends van mobiele apps, RESTful API's en bedrijfsprocessen, samenvoegen in één oplossing.

Hallo volgende video van 4 minuten bevat een korte uitleg van de relatie van App Service op Azure tooearlier aanbiedingen en wat is er nieuw in deze.

> [!VIDEO https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/app-service-history-lesson/player]
> 
> 

## <a name="why-use-app-service"></a>Waarom App Service gebruiken?
Hierna ziet u een paar belangrijke functies en mogelijkheden van App Service:

* **Meerdere talen en frameworks**: App Service biedt uitstekende ondersteuning voor ASP.NET, Node.js, Java, PHP en Python. U kunt ook [Windows PowerShell en andere scripts of uitvoerbare bestanden](../app-service-web/web-sites-create-web-jobs.md) uitvoeren op virtuele machines van App Service.
* **DevOps-optimalisatie**: stel [continue integratie en implementatie](../app-service-web/app-service-continuous-deployment.md) in met Visual Studio Team Services, GitHub of BitBucket. Verhoog updateniveaus via [test- en faseringsomgevingen](../app-service-web/web-sites-staged-publishing.md). Voer [A/B-tests](../app-service-web/app-service-web-test-in-production-get-start.md) uit. Uw apps in App Service beheren met behulp van [Azure PowerShell](/powershell/azureps-cmdlets-docs) of Hallo [platformoverschrijdende opdrachtregelinterface (CLI)](../cli-install-nodejs.md).
* **Globale schaling met hoge beschikbaarheid**: u kunt handmatig of automatisch [omhoog](../app-service-web/web-sites-scale.md) schalen of [uit](../monitoring-and-diagnostics/insights-how-to-scale.md)schalen. Host uw apps overal in de globale datacenterinfrastructuur van Microsoft en App Service Hallo [SLA](https://azure.microsoft.com/support/legal/sla/app-service/) belooft hoge beschikbaarheid.
* **Verbindingen tooSaaS platforms en on-premises gegevens** -kiezen uit meer dan 50 [connectors](../connectors/apis-list.md) voor bedrijfssystemen (zoals SAP, Siebel en Oracle), SaaS-services (zoals Salesforce en Office 365) en internet Services (zoals Facebook en Twitter). Toegang tot on-premises gegevens met [hybride verbindingen](../biztalk-services/integration-hybrid-connection-overview.md) en [Azure Virtual Networks](../app-service-web/web-sites-integrate-with-vnet.md).
* **Beveiliging en naleving**: App Service voldoet aan de vereisten van [ISO, SOC en PCI](https://www.microsoft.com/TrustCenter/).
* **Toepassingssjablonen** -kiezen uit een uitgebreide lijst met sjablonen in Hallo [Azure Marketplace](https://azure.microsoft.com/marketplace/) waarmee u een wizard tooinstall populaire open-source software zoals WordPress, Joomla en Drupal gebruiken.
* **Visual Studio-integratie** -specifieke hulpprogramma's in Visual Studio stroomlijnen Hallo maken, implementeren en foutopsporing.

## <a name="app-types-in-app-service"></a>App-typen in App Service
App Service biedt diverse *app-typen*, elk waarvan is beoogde toohost een specifieke werkbelasting:

* [**Web Apps**](../app-service-web/app-service-web-overview.md): voor het hosten van websites en webtoepassingen.
* [**Mobile Apps**](../app-service-mobile/app-service-mobile-value-prop.md): voor het hosten van de back-end van mobiele apps.
* [**API-apps**](../app-service-api/app-service-api-apps-why-best-platform.md): voor het hosten van RESTful-API's.
* [**Logische apps**](../logic-apps/logic-apps-what-are-logic-apps.md): voor het automatiseren van bedrijfsprocessen en het integreren van systemen en gegevens tussen clouds zonder code te schrijven.

Hallo word *app* verwijst hier toohello hosting-resources toegewezen toorunning een werkbelasting. Duurt 'web-app' als voorbeeld, u bevindt zich waarschijnlijk vertrouwd toothinking van een web-app als zowel de Hallo rekenresources en de toepassing die samen afleveren functionaliteit tooa browser code. Maar in App Service een *web-app* is Hallo rekenresources die Azure biedt voor het hosten van uw toepassingscode. 

Uw toepassing kan bestaan uit meerdere App Service-apps van verschillende typen. Als uw toepassing bijvoorbeeld bestaat uit een webfront-end en een RESTful-API-back-end, kunt u:

- Zowel (front-end- en api) implementeren tooa één web-app  
- Implementeer uw front-code tooa web-app en uw back-end-code tooan API-app. 



## <a name="app-service-plans"></a>App Service-abonnementen
[App Service-plannen](azure-web-sites-web-hosting-plans-in-depth-overview.md) omvatten Hallo verzameling fysieke resources gebruikt toohost uw apps.

In App Service-plannen wordt het volgende gedefinieerd:

- **Regio** (VS - west, VS - oost, etc.)
- **Schaal** (een, twee, drie exemplaren, etc.)
- **Exemplaargrootte** (klein, normaal, groot)
- **SKU** (Free, Shared, Basic, Standard, Premium)

Alle toepassingen toegewezen tooan **App Service-abonnement** Hallo-resources die zijn gedefinieerd door het zodat u toosave kosten bij het hosten van meerdere apps delen.

Uw **App Service-abonnement** kunt opschalen van **vrije** en **gedeelde** SKU's te**Basic**, **standaard**, en **Premium** SKU's zodat u toegang tot resources toomore en functies langs Hallo manier. Zodra uw App Service-Plan te is ingesteld**Basic** of hoger kunt u ook Hallo bepalen **grootte** en aantal Hallo virtuele machines worden geschaald.

Hallo **SKU** en **Scale** Hallo App Service plan bepaalt Hallo kosten en niet Hallo aantal apps die erin worden gehost. 

Als u meer schaalbaarheid en netwerkisolatie nodig hebt, kunt u uw apps uitvoeren in een [App Service-omgeving](../app-service-web/app-service-app-service-environment-intro.md).

## <a name="pricing"></a>Prijzen
Zie [Prijzen van App Service](https://azure.microsoft.com/pricing/details/app-service/) voor meer informatie over de prijzen van App Service.

## <a name="test-drive-app-service"></a>App Service uitproberen
[Maak een voorbeeld-web-app, mobiele app of logische app](https://azure.microsoft.com/try/app-service/) en speel hier een uur mee, zonder dat u een creditcard nodig hebt, zonder verbintenissen en zonder gedoe.

Of open een [gratis Azure-account](https://azure.microsoft.com/pricing/free-trial/) en probeer een van onze zelfstudies Aan de slag:

* [Zelfstudie: een web-app maken](../app-service-web/app-service-web-get-started.md)
* [Zelfstudie: een mobiele app maken](../app-service-mobile/app-service-mobile-android-get-started.md)
* [Zelfstudie: een API-app maken](../app-service-api/app-service-api-dotnet-get-started.md)
* [Zelfstudie: een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md)

