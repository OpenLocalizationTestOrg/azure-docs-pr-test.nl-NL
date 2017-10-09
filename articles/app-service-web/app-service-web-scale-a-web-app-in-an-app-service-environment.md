---
title: aaaHow tooScale een App in een App-serviceomgeving
description: Schalen van een app in App Service-omgeving
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: jimbe
ms.assetid: 78eb1e49-4fcd-49e7-b3c7-f1906f0f22e3
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/17/2016
ms.author: ccompy
ms.openlocfilehash: 08916eac056c46bf8cb6edffbf96285317b32062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-apps-in-an-app-service-environment"></a>Apps schalen in een App Service-omgeving
In Azure App Service Hallo zijn er normaal gesproken drie dingen die kunt u de schaal:

* plan prijzen
* de grootte van de werknemer 
* aantal exemplaren.

In een as-omgeving is er geen noodzaak tooselect of wijzig Hallo plan prijzen.  Wat betreft mogelijkheden is het al op een Premium-prijscategorie mogelijkheid niveau.  

Met opzicht tooworker grootten toewijzen Hallo as-omgeving beheerder Hallo grootte van Hallo compute resource toobe gebruikt voor elke worker-groep.  Dit betekent dat u kunt Worker-groep 1 hebben met P4 rekenresources en 2 voor Worker-groep met P1 rekenresources indien gewenst.  Hebben geen toobe in volgorde van de grootte.  Zie voor meer informatie over Hallo grootten en de prijscategorie Hallo document hier [prijzen van Azure App Service][AppServicePricing].  Hierbij blijft Hallo opties voor web-apps en App Service-abonnementen in een App Service-omgeving toobe schalen:

* selectie van Worker-groep
* aantal exemplaren

Het wijzigen van een item wordt gedaan door Hallo gebruikersinterface weergegeven voor de as-omgeving App Service-abonnementen gehoste van toepassing.  

![][1]

U kunt uw ASP dan het aantal beschikbare rekenresources in Hallo worker-groep die de ASP is in Hallo kan niet opschalen.  Als u resources in die groep worker moet berekenen moet u tooget uw as-omgeving beheerder tooadd ze.  Voor informatie over het configureren van uw as-omgeving opnieuw Lees hier Hallo-informatie: [hoe App Service-omgeving tooConfigure][HowtoConfigureASE].  U kunt ook tootake profiteren van Hallo as-omgeving voor automatisch schalen functies tooadd capaciteit op basis van het schema of metrische gegevens.  Zie voor meer informatie over het configureren van automatisch schalen voor Hallo as-omgeving omgeving zelf tooget [hoe tooconfigure automatisch schalen voor een App-serviceomgeving][ASEAutoscale].

Kunt u meerdere app service-abonnementen met behulp van rekenresources vanaf verschillende werknemersgroepen maken of kunt u dezelfde werknemersgroep Hallo.  Voor het voorbeeld hebt u (10) beschikbare rekenresources in het werkproces groep 1, kunt u toocreate één app service-abonnement met behulp van rekenresources (6) en een tweede app service-plan dat maakt gebruik van rekenresources (4).

### <a name="scaling-hello-number-of-instances"></a>Het aantal exemplaren Hallo schalen
Wanneer u eerst uw web-app in App Service-omgeving maken wordt gestart 1 exemplaar.  U kunt vervolgens scale-out tooadditional exemplaren tooprovide extra bronnen berekenen voor uw app.   

Als u uw as-omgeving heeft onvoldoende capaciteit vervolgens is dit heel eenvoudig.  U gaat tooyour App Service-Plan dat Hallo sites u tooscale-up wilt en selecteer schaal bevat.  Hiermee opent u Hallo UI kunt u handmatig Hallo schaal ingesteld voor de ASP of regels voor automatisch schalen configureren voor de ASP.  toomanually schaal uw app in te stellen ***schalen door*** te***aantal instanties dat ik handmatig invoeren***.  Hier Hallo schuifregelaar toohello gewenst aantal slepen of invoeren in Hallo vak volgende toohello schuifregelaar.  

![][2] 

Hallo automatisch schalen regels voor een ASP in een as-omgeving voor werk Hallo dezelfde dan normaal.  U kunt selecteren ***CPU-Percentage*** onder ***schalen door*** en automatisch schalen regels te maken voor de ASP op basis van CPU-Percentage, of u complexere regels die gebruikmaken van kunt maken ***regels voor planning en prestaties ***.  toosee voltooien meer details over het configureren van automatisch schalen gebruik Hallo handleiding hier [schalen van een app in Azure App Service][AppScale]. 

### <a name="worker-pool-selection"></a>Selectie van Worker-groep
Zoals eerder opgemerkt, worden Hallo worker-groep selectie is toegankelijk vanuit Hallo ASP gebruikersinterface.  Hallo-blade voor Hallo ASP dat u tooscale wilt en selecteer werknemersgroep geopend.  U ziet alle Hallo werknemersgroepen die u hebt geconfigureerd in uw App Service-omgeving.  Als er slechts één werknemersgroep vervolgens ziet alleen u een Hallo van toepassingen die worden vermeld.  toochange in welke worker-groep de ASP is, u eenvoudig hello werknemersgroep u wilt dat uw App Service-Plan toomove te selecteren.  

![][3]

Voordat uw ASP verplaatsen van een werknemer groep tooanother is belangrijk dat er voldoende capaciteit voor de ASP toomake.  In Hallo lijst met werknemersgroepen, niet alleen Hallo worker Poolnaam wordt vermeld maar u kunt ook zien hoeveel werknemers beschikbaar zijn in die worker-groep.  Zorg ervoor dat er voldoende beschikbare toocontain exemplaren uw App Service-Plan.  U moet meer rekenresources in Hallo werknemersgroep desgewenst toomove naar Haal vervolgens uw as-omgeving beheerder tooadd ze.  

> [!NOTE]
> Hallo-apps in ASP Start verplaatsen van dat een ASP in een werknemersgroep zullen koude.  Hierdoor kan aanvragen toorun langzaam als uw app koude gestart op de nieuwe rekenresources Hallo is.  Hallo koude start kan worden voorkomen met behulp van Hallo [toepassing warme up mogelijkheid] [ AppWarmup] in Azure App Service.  Hallo initialisatie van de toepassing module beschreven in artikel Hallo werkt ook voor koude startprocedures omdat het initialisatieproces hello ook aangeroepen wordt wanneer apps koude gestart op de nieuwe rekenresources zijn. 
> 
> 

## <a name="getting-started"></a>Aan de slag
tooget de slag met App Service-omgevingen, Zie [hoe tooCreate een App Service-omgeving][HowtoCreateASE]

Zie voor meer informatie over hello Azure App Service-platform, [Azure App Service][AzureAppService].

<!--Image references-->
[1]: ./media/app-service-web-scale-a-web-app-in-an-app-service-environment/aseappscale-aspblade.png
[2]: ./media/app-service-web-scale-a-web-app-in-an-app-service-environment/aseappscale-manualscale.png
[3]: ./media/app-service-web-scale-a-web-app-in-an-app-service-environment/aseappscale-sizescale.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[ScaleWebapp]: http://azure.microsoft.com/documentation/articles/web-sites-scale/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[HowtoConfigureASE]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
[CreateWebappinASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-a-web-app-in-an-ase/
[Appserviceplans]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/ 
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[AppScale]: http://azure.microsoft.com/documentation/articles/web-sites-scale/
[AppWarmup]: http://ruslany.net/2015/09/how-to-warm-up-azure-web-app-during-deployment-slots-swap/
