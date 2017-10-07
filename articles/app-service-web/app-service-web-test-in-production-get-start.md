---
title: aaaGet gestart met testen in de productieomgeving voor Web-Apps
description: Meer informatie over Hallo testen in productie (TiP)-functie in Azure App Service Web Apps.
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
ms.openlocfilehash: 2ddbd532ffe2a4f3e07fd386d9741a3fde3639ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-test-in-production-for-web-apps"></a>Aan de slag met testen tijdens productie voor Web Apps
In productie testen of live-testen van uw web-app met behulp van de live klantverkeer, is een test-strategie die app-ontwikkelaars steeds integreren in hun [flexibele ontwikkeling](https://en.wikipedia.org/wiki/Agile_software_development) methodologie. Hiermee kunt u tootest Hallo kwaliteit van uw apps met live gebruikersverkeer in uw productieomgeving als tegengestelde toosynthesized gegevens in een testomgeving. Bij het blootstellen van uw nieuwe app tooreal gebruikers kunt u geïnformeerd over Hallo echte problemen die uw app hebben te maken mogelijk nadat deze is geïmplementeerd. U kunt controleren Hallo-functionaliteit, prestaties en waarde van uw app-updates tegen Hallo volume, snelheid en diverse echte gebruikersverkeer, wat u nooit in een testomgeving geschatte kunt.

## <a name="traffic-routing-in-app-service-web-apps"></a>Verkeer routering in App Service-Web-Apps
Functie voor verkeersroutering Hello in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), u kunt instellen dat een deel van de gebruiker live verkeer tooone of meer [implementatiesites](web-sites-staged-publishing.md), en vervolgens uw app met analyseren [Azure-toepassing Insights](/services/application-insights/) of [Azure HDInsight](/services/hdinsight/), of een hulpprogramma van derden, zoals [New Relic](/marketplace/partners/newrelic/newrelic/) toovalidate uw wijziging. U kunt bijvoorbeeld Hallo volgen scenario's met App Service implementeren:

* Functionele bugs detecteren of knelpunten in uw implementatie van updates voorafgaande toosite wide speldenpunt
* "Gecontroleerde test vlucht' van de wijzigingen door te meten bruikbaarheid metrische gegevens op Hallo beta-app uitvoeren
* Geleidelijk mogelijk nieuwe update tooa uitbreiden en probleemloos back-toohello huidige versie als een fout optreedt 
* Optimaliseert u uw app bedrijfsresultaten door [A / B-tests](https://en.wikipedia.org/wiki/A/B_testing) of [multidimensionale tests](https://en.wikipedia.org/wiki/Multivariate_testing_in_marketing) meerdere implementatiesites

### <a name="requirements-for-using-traffic-routing-in-web-apps"></a>Vereisten voor het gebruik van verkeersroutering in Web-Apps
* Uw web-app moet worden uitgevoerd in **standaard** of **Premium** laag, zoals vereist is voor meerdere implementatiesites.
* In de volgorde toowork juist verkeersroutering cookies toobe ingeschakeld in de browser Hallo gebruikers. Traffic Routing maakt gebruik van cookies toopin een implementatiesleuf client browser tooa voor Hallo levensduur Hallo clientsessie.
* Traffic Routing biedt ondersteuning voor geavanceerde TiP-scenario's via Azure PowerShell-cmdlets.

## <a name="route-traffic-segment-tooa-deployment-slot"></a>Route verkeer segment tooa-implementatiesleuf
Op basisniveau in elk scenario TiP hello, moet u een vooraf gedefinieerde percentage van uw live verkeer tooa niet-productieve implementatiesleuf versturen. toodo deze, Hallo stappen hieronder:

> [!NOTE]
> Hallo hier stappen wordt ervan uitgegaan dat er al een [niet-productieve implementatiesleuf](web-sites-staged-publishing.md) en die Hallo gewenst web-app-inhoud is al [geïmplementeerd](web-sites-deploy.md) tooit.
> 
> 

1. Meld u aan bij Hallo [Azure Portal](https://portal.azure.com/).
2. Klik op de blade van uw web-app **instellingen** > **verkeersroutering**.
   ![](./media/app-service-web-test-in-production/01-traffic-routing.png)
3. Selecteer Hallo sleuf gewenste tooroute verkeer tooand Hallo percentage van totale verkeer Hallo u wenst op en klik vervolgens op **opslaan**.
   
    ![](./media/app-service-web-test-in-production/02-select-slot.png)
4. Ga toohello implementatiesleuf blade. U ziet nu live verkeer wordt gerouteerd tooit.
   
    ![](./media/app-service-web-test-in-production/03-traffic-routed.png)

Zodra voor verkeersroutering is geconfigureerd, wordt er Hallo opgegeven percentage van clients worden niet-productiesite willekeurig gerouteerde tooyour. Het is echter belangrijk toonote dat wanneer een client automatisch gerouteerde tooa specifieke sleuf is, 'vastgemaakt' toothat sleuf voor Hallo aanmeldingssessie van die client moeten. Dit gedaan met behulp van een gebruikerssessie cookie toopin Hallo. Als u Hallo HTTP-aanvragen inspecteren, vindt u een `TipMix` cookie in elke volgende aanvraag.

![](./media/app-service-web-test-in-production/04-tip-cookie.png)

## <a name="force-client-requests-tooa-specific-slot"></a>Client-aanvragen tooa specifieke sleuf forceren
App Service is in de toevoeging tooautomatic verkeersroutering kunnen tooroute aanvragen tooa specifieke sleuf. Dit is handig als u wilt dat uw gebruikers toobe kunnen tooopt-in- of opt-out van uw app beta. toodo dit u Hallo `x-ms-routing-name` queryparameter.

tooreroute gebruikers tooa specifieke sleuf gebruiken `x-ms-routing-name`, moet u ervoor zorgen dat sleuf Hallo toohello voor verkeersroutering lijst al is toegevoegd. Aangezien u tooroute tooa sleuf expliciet wilt, Hallo werkelijke routering u percentage ingesteld maakt niet uit. Als u wilt, kunt u een 'beta koppeling' waarop gebruikers kunnen klikken stellen tooaccess Hallo beta-app.

![](./media/app-service-web-test-in-production/06-enable-x-ms-routing-name.png)

### <a name="opt-users-out-of-beta-app"></a>Gebruikers buiten de bèta-app kiezen
toolet gebruikers afmelden van uw app Bèta, bijvoorbeeld, kunt u deze koppeling opnemen in uw webpagina:

    <a href="<webappname>.azurewebsites.net/?x-ms-routing-name=self">Go back tooproduction app</a>

Hallo tekenreeks `x-ms-routing-name=self` Hallo productiesite bevat. Eenmaal hello client browser toegang Hallo koppeling is niet alleen deze toohello productiesite omgeleid, maar elke volgende aanvraag bevat Hallo `x-ms-routing-name=self` cookie die Hallo sessie toohello productiesite pincodes.

![](./media/app-service-web-test-in-production/05-access-production-slot.png)

### <a name="opt-users-in-toobeta-app"></a>Gebruikers in app toobeta kiezen
toolet gebruikers tooyour beta app aanmelden, set Hallo dezelfde query toohello parameternaam van Hallo niet-productieve sleuf, bijvoorbeeld:

        <webappname>.azurewebsites.net/?x-ms-routing-name=staging

## <a name="more-resources"></a>Meer bronnen
* [Faseringsomgevingen voor web-apps in Azure App Service instellen](web-sites-staged-publishing.md)
* [Een complexe toepassing zoals verwacht in Azure implementeren](app-service-deploy-complex-application-predictably.md)
* [Flexibele software ontwikkelen met Azure App Service](app-service-agile-software-development.md)
* [DevOps-omgevingen effectief gebruiken voor uw web-apps](app-service-web-staged-publishing-realworld-scenarios.md)

