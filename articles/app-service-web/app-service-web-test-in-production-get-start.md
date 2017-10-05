---
title: Aan de slag met testen tijdens productie voor Web Apps
description: Meer informatie over de Test in productie (TiP)-functie in Azure App Service Web Apps.
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 4623468d-886e-4203-8012-8f86deb2790b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: cephalin
ms.openlocfilehash: 9f38b635140cacf0513c75385bce3c110a930969
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-test-in-production-for-web-apps"></a>Aan de slag met testen tijdens productie voor Web Apps
In productie testen of live-testen van uw web-app met behulp van de live klantverkeer, is een test-strategie die app-ontwikkelaars steeds integreren in hun [flexibele ontwikkeling](https://en.wikipedia.org/wiki/Agile_software_development) methodologie. Hiermee kunt u de kwaliteit van uw apps met live gebruikersverkeer in uw productieomgeving, in plaats van de kunstmatige gegevens in een testomgeving te testen. Bij het blootstellen van uw nieuwe app voor echte gebruikers kunt u geïnformeerd over de echte problemen die uw app hebben te maken mogelijk nadat deze is geïmplementeerd. U kunt controleren of de functionaliteit, de prestaties en de waarde van uw app-updates op basis van het volume, snelheid en diverse echte gebruikersverkeer, wat u nooit in een testomgeving geschatte kunt.

## <a name="traffic-routing-in-app-service-web-apps"></a>Verkeer routering in App Service-Web-Apps
Met de functie voor verkeersroutering in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), u kunt instellen dat een deel van live gebruikersverkeer op een of meer [implementatiesites](web-sites-staged-publishing.md), en vervolgens uw app met analyseren [Azure-toepassing Insights](/services/application-insights/) of [Azure HDInsight](/services/hdinsight/), of een hulpprogramma van derden, zoals [New Relic](/marketplace/partners/newrelic/newrelic/) voor het valideren van de wijziging. U kunt bijvoorbeeld de volgende scenario's implementeren met App Service:

* Functionele bugs detecteren of knelpunten in uw updates voorafgaand aan de implementatie van de gehele site speldenpunt
* "Gecontroleerde test vlucht' van de wijzigingen door te meten bruikbaarheid metrische gegevens over de bèta-app uitvoeren
* Geleidelijk mogelijk uitbreiden tot een nieuwe update en probleemloos weer omlaag naar de huidige versie als een fout optreedt 
* Optimaliseert u uw app bedrijfsresultaten door [A / B-tests](https://en.wikipedia.org/wiki/A/B_testing) of [multidimensionale tests](https://en.wikipedia.org/wiki/Multivariate_testing_in_marketing) meerdere implementatiesites

### <a name="requirements-for-using-traffic-routing-in-web-apps"></a>Vereisten voor het gebruik van verkeersroutering in Web-Apps
* Uw web-app moet worden uitgevoerd in **standaard** of **Premium** laag, zoals vereist is voor meerdere implementatiesites.
* Een goede werking verkeersroutering cookies zijn ingeschakeld in de browser van gebruikers. Traffic Routing worden cookies gebruikt vastmaken een clientbrowser in de implementatiesleuf van een voor de levensduur van de clientsessie.
* Traffic Routing biedt ondersteuning voor geavanceerde TiP-scenario's via Azure PowerShell-cmdlets.

## <a name="route-traffic-segment-to-a-deployment-slot"></a>Route verkeer segment moet een implementatiesleuf
Op het niveau basis van elk scenario TiP kunt u een vooraf gedefinieerde percentage van uw live verkeer naar een niet-productieve implementatiesleuf routeren. U doet dit door de volgende stappen uit te voeren:

> [!NOTE]
> Hier de stappen wordt ervan uitgegaan dat er al een [niet-productieve implementatiesleuf](web-sites-staged-publishing.md) en dat de gewenste web-app-inhoud is al [geïmplementeerd](web-sites-deploy.md) aan.
> 
> 

1. Meld u aan bij de [Azure-Portal](https://portal.azure.com/).
2. Klik op de blade van uw web-app **instellingen** > **verkeersroutering**.
   ![](./media/app-service-web-test-in-production/01-traffic-routing.png)
3. Selecteer de site die u wilt routeren van verkeer en het percentage van het totale verkeer u wenst op en klik vervolgens op **opslaan**.
   
    ![](./media/app-service-web-test-in-production/02-select-slot.png)
4. Ga naar de implementatiesleuf blade. U ziet nu live verkeer wordt doorgestuurd naar het.
   
    ![](./media/app-service-web-test-in-production/03-traffic-routed.png)

Zodra voor verkeersroutering is geconfigureerd, wordt het opgegeven percentage van clients willekeurig worden gerouteerd naar uw-productiesite. Het is echter belangrijk te weten dat wanneer een client wordt automatisch doorgestuurd naar een specifieke site, deze worden '' aan die sleuf voor de levensduur van die clientsessie vastgemaakt wordt. Dit gedaan met behulp van een cookie om de gebruikerssessie vast te maken. Als u de HTTP-aanvragen inspecteren, vindt u een `TipMix` cookie in elke volgende aanvraag.

![](./media/app-service-web-test-in-production/04-tip-cookie.png)

## <a name="force-client-requests-to-a-specific-slot"></a>Clientaanvragen omzetten in een specifieke site
Naast de automatische verkeersroutering kan App Service route-aanvragen voor een specifieke site. Dit is handig als u wilt dat gebruikers kunnen kiezen in of opt-out van uw app beta. Hiervoor gebruikt u de `x-ms-routing-name` queryparameter.

Gebruikers in een specifieke sleuf met omgeleid `x-ms-routing-name`, moet u ervoor zorgen dat de sleuf is al toegevoegd aan de lijst voor verkeersroutering. Omdat u routeren expliciet naar een site wilt, worden de werkelijke routering u percentage ingesteld maakt niet uit. Als u wilt, kunt u een 'beta koppeling' waarop gebruikers klikken kunnen om toegang tot de app beta opgesteld.

![](./media/app-service-web-test-in-production/06-enable-x-ms-routing-name.png)

### <a name="opt-users-out-of-beta-app"></a>Gebruikers buiten de bèta-app kiezen
Zodat gebruikers afmelden uw bèta-app kunt u bijvoorbeeld deze koppeling in uw webpagina plaatsen:

    <a href="<webappname>.azurewebsites.net/?x-ms-routing-name=self">Go back to production app</a>

De tekenreeks `x-ms-routing-name=self` Hiermee geeft u de productiesite. Zodra de clientbrowser toegang krijgen tot de koppeling, niet alleen het omgeleid naar de productiesite, maar elke volgende aanvraag bevat de `x-ms-routing-name=self` cookie die pincodes van de sessie naar de productiesite.

![](./media/app-service-web-test-in-production/05-access-production-slot.png)

### <a name="opt-users-in-to-beta-app"></a>Gebruikers in beta app kiezen
Om gebruikers te laten deelnemen aan uw app beta, stelt u de dezelfde queryparameter bijvoorbeeld op de naam van de niet-productiesite:

        <webappname>.azurewebsites.net/?x-ms-routing-name=staging

## <a name="more-resources"></a>Meer bronnen
* [Faseringsomgevingen voor web-apps in Azure App Service instellen](web-sites-staged-publishing.md)
* [Een complexe toepassing zoals verwacht in Azure implementeren](app-service-deploy-complex-application-predictably.md)
* [Flexibele software ontwikkelen met Azure App Service](app-service-agile-software-development.md)
* [DevOps-omgevingen effectief gebruiken voor uw web-apps](app-service-web-staged-publishing-realworld-scenarios.md)

