---
title: overzicht van de Apps aaaWeb | Microsoft Docs
description: Lees hoe Azure App Service u helpt bij het ontwikkelen en hosten van web-apps
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 94af2caf-a2ec-4415-a097-f60694b860b3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: overview
ms.date: 01/04/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: ce27519bddd62a7fca6ba1fb23c763d0fc378c2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="web-apps-overview"></a>Overzicht van Web Apps
*App Service Web Apps* is een volledig beheerd rekenplatform dat is geoptimaliseerd voor het hosten van websites en web-apps. Dit [platform as a service](https://en.wikipedia.org/wiki/Platform_as_a_service) (PaaS)-aanbod van Microsoft Azure kunt u zich richten op uw bedrijfslogica terwijl Azure voor Hallo infrastructuur toorun zorgt en schalen van uw apps.

Hallo na 5 minuten durende video maakt u kennis met Azure App Service Web Apps.

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-App-Service-Web-Apps-with-Yochay-Kiriaty/player]
>
>

> [!INCLUDE [app-service-linux](../../includes/app-service-linux.md)]
> 
> 

## <a name="what-is-a-web-app-in-app-service"></a>Wat is een web-app in App Service?
In App Service een *web-app* hello rekenresources die Azure biedt voor het hosten van een website of web-toepassing is.  

Hallo rekenresources mogelijk op gedeelde of toegewezen virtuele machines (VM's), afhankelijk van Hallo prijscategorie die u kiest. De toepassingscode wordt uitgevoerd op een beheerde virtuele machine die is geïsoleerd van andere klanten.

De code kan zijn geschreven in elke taal die of elk framework dat wordt ondersteund door [Azure App Service](../app-service/app-service-value-prop-what-is.md), zoals ASP.NET, Node.js, Java, PHP of Python. U kunt in een web-app ook scripts uitvoeren die gebruikmaken van [PowerShell en andere scripttalen](web-sites-create-web-jobs.md#acceptablefiles).

Voor voorbeelden van typische toepassingsscenario's die u Web-Apps voor Zie gebruiken kunt [Web-app-scenario's](https://azure.microsoft.com/documentation/scenarios/web-app/) en Hallo **scenario's en aanbevelingen** sectie van [Azure App Service, virtuele Vergelijking van machines, Service Fabric en Cloud Services](choose-web-site-cloud-service-vm.md#scenarios).

## <a name="why-use-web-apps"></a>Waarom Web Apps gebruiken?
Hier volgen enkele belangrijke functies van App Service die van toepassing zijn tooWeb Apps:

* **Meerdere talen en frameworks**: App Service biedt uitstekende ondersteuning voor ASP.NET, Node.js, Java, PHP en Python. U kunt ook [PowerShell en andere scripts of uitvoerbare bestanden](web-sites-create-web-jobs.md) uitvoeren op virtuele machines van App Service.
* **DevOps-optimalisatie**: stel [continue integratie en implementatie](app-service-continuous-deployment.md) in met Visual Studio Team Services, GitHub of BitBucket. Verhoog updateniveaus via [test- en faseringsomgevingen](web-sites-staged-publishing.md). Voer [A/B-tests](app-service-web-test-in-production-get-start.md) uit. Uw apps in App Service beheren met behulp van [Azure PowerShell](/powershell/azureps-cmdlets-docs) of Hallo [platformoverschrijdende opdrachtregelinterface (CLI)](../cli-install-nodejs.md).
* **Globale schaling met hoge beschikbaarheid**: u kunt handmatig of automatisch [omhoog](web-sites-scale.md) schalen of [uit](../monitoring-and-diagnostics/insights-how-to-scale.md)schalen. Host uw apps overal in de globale datacenterinfrastructuur van Microsoft en App Service Hallo [SLA](https://azure.microsoft.com/support/legal/sla/app-service/) belooft hoge beschikbaarheid.
* **Verbindingen tooSaaS platforms en on-premises gegevens** -kiezen uit meer dan 50 [connectors](../connectors/apis-list.md) voor bedrijfssystemen (zoals SAP, Siebel en Oracle), SaaS-services (zoals Salesforce en Office 365) en internet Services (zoals Facebook en Twitter). Toegang tot on-premises gegevens met [hybride verbindingen](../biztalk-services/integration-hybrid-connection-overview.md) en [Azure Virtual Networks](web-sites-integrate-with-vnet.md).
* **Beveiliging en naleving**: App Service voldoet aan de vereisten van [ISO, SOC en PCI](https://www.microsoft.com/TrustCenter/).
* **Toepassingssjablonen** -kiezen uit een uitgebreide lijst met Toepassingssjablonen in Hallo [Azure Marketplace](https://azure.microsoft.com/marketplace/) waarmee u een wizard tooinstall populaire open-source software zoals WordPress, Joomla en Drupal gebruiken.
* **Visual Studio-integratie** -specifieke hulpprogramma's in Visual Studio stroomlijnen Hallo maken, implementeren en foutopsporing.

Bovendien kan een web-app gebruikmaken van functies die worden aangeboden door [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md) (zoals CORS-ondersteuning) en [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) (zoals pushmeldingen). Zie [Overzicht van Azure App Service](../app-service/app-service-value-prop-what-is.md) voor meer informatie over soorten apps in App Service.

Naast Web Apps in App Service biedt Azure nog andere services die kunnen worden gebruikt voor het hosten van websites en web-apps. Voor de meeste scenario's is Web-Apps de beste keuze Hallo.  Voor microservice-architectuur, kunt u overwegen [Service Fabric](https://azure.microsoft.com/documentation/services/service-fabric), en als u meer controle over virtuele machines die uw code wordt uitgevoerd op Hallo nodig hebt, overweeg dan [Azure Virtual Machines](https://azure.microsoft.com/documentation/services/virtual-machines/). Voor meer informatie over het toochoose tussen deze Azure-services, Zie [vergelijking van Azure App Service, virtuele Machines, Service Fabric en Cloud Services](choose-web-site-cloud-service-vm.md).

## <a name="getting-started"></a>Aan de slag
tooget gaan voorbeeld code tooa nieuwe web-app in App Service implementeren Volg een van de Hallo zelfstudies in Hallo vervolgkeuzelijst te volgen. U hebt een gratis Azure-account nodig.

> [!div class="op_single_selector"]
> * [Uw eerste ASP.NET web app tooAzure in vijf minuten implementeren](app-service-web-get-started-dotnet.md)
> * [Uw eerste PHP-web-app tooAzure in vijf minuten implementeren](app-service-web-get-started-php.md)
> * [Uw eerste Node.js-web-app tooAzure in vijf minuten implementeren](app-service-web-get-started-nodejs.md)
> * [Uw eerste Java-web-app tooAzure in vijf minuten implementeren](app-service-web-get-started-java.md)
> * [Uw eerste Python-web-app tooAzure in vijf minuten implementeren](app-service-web-get-started-python.md)
> * [Uw eerste HTML site tooAzure in vijf minuten implementeren](app-service-web-get-started-html.md)
> 
> 

> [!NOTE]
> U kunt [App Service proberen](https://azure.microsoft.com/try/app-service/) zonder een Azure-account. Een eenvoudige app maken en te spelen met voor up tooan uur--geen creditcard nodig en zonder verdere verplichtingen.
> 
> 
