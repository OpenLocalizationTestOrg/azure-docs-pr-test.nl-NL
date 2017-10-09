---
title: aaaService Fabric-project maken de volgende stappen | Microsoft Docs
description: Dit artikel bevat koppelingen tooa verzameling ontwikkeling kerntaken voor Service Fabric
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 299d1f97-1ca9-440d-9f81-d1d0dd2bf4df
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: rwike77
ms.openlocfilehash: 45598bfabedf280fba8af449ef920f40b409a609
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="your-service-fabric-application-and-next-steps"></a>Uw Service Fabric-toepassing en de volgende stappen
Uw Azure Service Fabric-toepassing is gemaakt. Hallo samenstelling van uw project en een aantal mogelijke volgende stappen wordt beschreven.

## <a name="your-application"></a>Uw toepassing
Elke nieuwe toepassing bevat een toepassingsproject. Er zijn een of twee extra projecten, afhankelijk van het Hallo-type van de service gekozen.

### <a name="hello-application-project"></a>Hallo-toepassingsproject
Hallo-toepassingsproject bestaat uit:

* Een aantal verwijzingen toohello services die gezamenlijk uw toepassing.
* Drie publiceren profielen (1-knooppunt lokale, 5-knooppunt lokale en Cloud) waarmee u toomaintain voorkeuren kunt voor het werken met verschillende omgevingen--zoals voorkeuren gerelateerde tooa clustereindpunt en Hiermee wordt aangegeven of tooperform implementaties upgrade standaard.
* Drie parameter voor toepassingsbestanden (zelfde als hierboven) waarmee u toomaintain toepassing omgeving-specifieke configuraties, zoals Hallo aantal partities toocreate voor een service kunt.
* Het script voor een implementatie waarmee u toodeploy uw toepassing vanaf de opdrachtregel Hallo of als onderdeel van een geautomatiseerde continue integratie en implementatie-pijplijn kunt.
* Hallo toepassingsmanifest, waarin wordt beschreven Hallo-toepassing. U vindt Hallo manifest onder Hallo ApplicationPackageRoot map.

### <a name="stateless-service"></a>Staatloze service
Wanneer u een nieuwe staatloze service toevoegt, Visual Studio wordt toegevoegd een oplossing voor service-project tooyour met een type dat is afgeleid van `StatelessService`. Hallo-service wordt een lokale variabele in een teller verhoogd.

### <a name="stateful-service"></a>Stateful service
Wanneer u een nieuwe stateful service toevoegt, Visual Studio wordt toegevoegd een oplossing voor service-project tooyour met een type dat is afgeleid van `StatefulService`. Hallo service verhoogt een item in de `RunAsync` methode en winkels Hallo resulteren in een `ReliableDictionary`.

### <a name="actor-service"></a>Actor-service
Wanneer u een nieuwe betrouwbare actor toevoegt, Visual Studio twee projecten tooyour oplossing voegt: een actor-project en een interface-project.

Hallo actor project biedt methoden voor het instellen en betrouwbaar binnen Hallo actorstatus ophalen van Hallo-waarde van een prestatiemeteritem dat wordt bewaard. Hallo project interface biedt een interface die andere services tooinvoke Hallo actor kunt gebruiken.

### <a name="stateless-web-api"></a>Staatloze Web-API
Hallo staatloze Web API-project biedt een eenvoudige webservice waarmee u tooopen uw toepassing tooexternal-clients kunt. Zie voor meer informatie over de structuur van Hallo project [Service Fabric-Web-API-services met OWIN zelf hosting](service-fabric-reliable-services-communication-webapi.md).


### <a name="aspnet-core"></a>ASP.NET core
Hallo Service Fabric SDK bevat Hallo dezelfde set van ASP.NET Core sjablonen die beschikbaar zijn voor zelfstandige ASP.NET Core projecten: leeg is, [Web API][aspnet-webapi], en [webtoepassing][aspnet-webapp].

### <a name="guest-executables-and-guest-containers"></a>Gast uitvoerbare bestanden en de Gast-containers

Een Service Fabric 'gast' is een service die niet is gebouwd met programmeermodellen Hallo-platform. Kunt u een pakket Hallo binaire bestanden voor een gast ofwel [rechtstreeks in het toepassingspakket Hallo](service-fabric-deploy-existing-app.md) of [via een installatiekopie van een container](service-fabric-deploy-container.md). In beide gevallen Visual Studio maakt Hallo nodig artefacten in Hallo **ApplicationPackageRoot** map van het toepassingsproject Hallo. Visual Studio wordt een nieuw serviceproject niet maken omdat Hallo code al elders bestaat. Als u uw gast naast Hallo Service Fabric-toepassingsproject projecten toomanage wilt, kunt u deze toevoegen toohello dezelfde Visual Studio-oplossing.

## <a name="next-steps"></a>Volgende stappen
### <a name="create-an-azure-cluster"></a>Een Azure-cluster maken
Hallo Service Fabric SDK bevat een lokaal cluster voor ontwikkeling en testen. Zie voor een cluster in Azure, toocreate [instellen van een Service Fabric-cluster van hello Azure-portal][create-cluster-in-portal].

### <a name="publish-your-application-tooazure"></a>Uw toepassing tooAzure publiceren
U kunt uw toepassing rechtstreeks vanuit Visual Studio tooan Azure cluster publiceren. toolearn Zie [publiceren van uw toepassing tooAzure][publish-app-to-azure].

### <a name="use-service-fabric-explorer-toovisualize-your-cluster"></a>Uw cluster Service Fabric Explorer toovisualize gebruiken
Service Fabric Explorer biedt een eenvoudige manier toovisualize uw cluster, inclusief geïmplementeerde toepassingen en de fysieke indeling. toolearn meer, Zie [uw cluster visualiseren met behulp van Service Fabric Explorer][visualize-with-sfx].

### <a name="version-and-upgrade-your-services"></a>Versie en werk uw services
Service Fabric kunnen onafhankelijke versioning en upgraden van onafhankelijke services in een toepassing. toolearn meer, Zie [versiebeheer en upgraden van uw services][app-upgrade-tutorial].

### <a name="configure-continuous-integration-with-visual-studio-team-services"></a>Continue integratie met Visual Studio Team Services configureren
toolearn hoe u een continue integratie-proces kan instellen voor uw Service Fabric-toepassing raadpleegt [continue integratie met Visual Studio Team Services configureren][ci-with-vso].

<!-- Links -->
[add-web-frontend]: service-fabric-add-a-web-frontend.md
[create-cluster-in-portal]: service-fabric-cluster-creation-via-portal.md
[publish-app-to-azure]: service-fabric-publish-app-remote-cluster.md
[visualize-with-sfx]: service-fabric-visualizing-your-cluster.md
[ci-with-vso]: service-fabric-set-up-continuous-integration.md
[reliable-services-webapi]: service-fabric-reliable-services-communication-webapi.md
[app-upgrade-tutorial]: service-fabric-application-upgrade-tutorial.md
[aspnet-webapi]: https://docs.asp.net/en/latest/tutorials/first-web-api.html
[aspnet-webapp]: https://docs.asp.net/en/latest/tutorials/first-mvc-app/index.html
