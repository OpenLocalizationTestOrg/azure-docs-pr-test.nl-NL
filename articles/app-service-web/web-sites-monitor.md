---
title: aaaMonitor Apps in Azure App Service | Microsoft Docs
description: Meer informatie over hoe toomonitor Apps in Azure App Service met behulp van Azure Portal Hallo.
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: d273da4e-07de-48e0-b99d-4020d84a425e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/07/2016
ms.author: byvinyal
ms.openlocfilehash: 80d5a466102a894a49d04ae35aa54cc1d05a58df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-monitor-apps-in-azure-app-service"></a>How to: in Azure App Service-Apps bewaken
[App Service](http://go.microsoft.com/fwlink/?LinkId=529714) biedt ingebouwde bewaking functionaliteit in Hallo [Azure Portal](https://portal.azure.com).
Dit omvat Hallo mogelijkheid tooreview **quota** en **metrische gegevens** voor een app evenals Hallo App Service-abonnement in te stellen **waarschuwingen** en zelfs **schalen** automatisch op basis van deze metrische gegevens.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="understanding-quotas-and-metrics"></a>Understanding quota's en metrische gegevens
### <a name="quotas"></a>Quota
Toepassingen die worden gehost in App Service zijn onderwerp toocertain *limieten* op de bronnen die ze kunnen gebruiken. Hallo limieten, worden gedefinieerd door Hallo **App Service-abonnement** Hallo app gekoppeld.

Als de toepassing hello wordt gehost een **vrije** of **gedeelde** plant, en vervolgens Hallo limieten op Hallo bronnen Hallo app kunt gebruiken, zijn gedefinieerd door **quota**.

Als de toepassing hello wordt gehost een **Basic**, **standaard** of **Premium** plant, en vervolgens Hallo limieten op Hallo bronnen kan worden gebruikt zijn ingesteld door Hallo **grootte** (Klein, normaal, groot) en **aantal exemplaar** (1, 2, 3,...) Hallo **App Service-abonnement**.

**Quota's** voor **vrije** of **gedeelde** apps zijn:

* **CPU(Short)**
  * De hoeveelheid CPU toegestaan voor deze toepassing in een interval van 5 minuten. Dit quotum wordt opnieuw ingesteld om de 5 minuten.
* **CPU(Day)**
  * Totale hoeveelheid CPU toegestaan voor deze toepassing in een dag. Dit quotum wordt opnieuw ingesteld voor elke 24 uur om middernacht UTC.
* **Geheugen**
  * Totale hoeveelheid geheugen die is toegestaan voor deze toepassing.
* **Bandbreedte**
  * Totale hoeveelheid bandbreedte voor uitgaande toegestaan voor deze toepassing in een dag.
    Dit quotum wordt opnieuw ingesteld voor elke 24 uur om middernacht UTC.
* **Bestandssysteem**
  * Totale hoeveelheid opslag dat is toegestaan.

alleen quotum toepasselijke tooapps gehost op Hallo **Basic**, **standaard** en **Premium** plannen is **bestandssysteem**.

Meer informatie over specifieke quota hello, limieten en functies beschikbaar zijn voor verschillende App Service-SKU's Hallo vindt u hier: [Servicelimieten voor Azure-abonnement](../azure-subscription-service-limits.md#app-service-limits)

#### <a name="quota-enforcement"></a>Het afdwingen van quota
Als een toepassing in het gebruik ervan Hallo overschrijdt **CPU (korte)**, **CPU (dag)**, of **bandbreedte** quotum vervolgens Hallo toepassing wordt gestopt tot Hallo quotum opnieuw ingesteld. Tijdens deze periode kunnen alle inkomende aanvragen resulteert in een **HTTP 403**.
![][http403]

Als toepassing hello **geheugen** quotum wordt overschreden, wordt de toepassing hello instelling opnieuw is gestart.

Als hello **bestandssysteem** quotum wordt overschreden, en vervolgens een bewerking mislukt, dit omvat toologs schrijven schrijven.

Quota's kunnen worden verhoogd of verwijderd uit uw app door het upgraden van uw App Service-abonnement.

### <a name="metrics"></a>Metrische gegevens
**Metrische gegevens** bevatten informatie over het Hallo-app, of het gedrag van de App Service-abonnement.

Voor een **toepassing**, Hallo beschikbare metrische gegevens zijn:

* **Gemiddelde reactietijd**
  * Hallo gemiddelde tijd voor Hallo app tooserve aanvragen in ms.
* **Gemiddelde geheugen werkset**
  * Hallo gemiddelde hoeveelheid geheugen in MIB's die worden gebruikt door het Hallo-app.
* **CPU-tijd**
  * Hallo hoeveelheid CPU in seconden verbruikt door Hallo-app. Voor meer informatie over deze metrische Zie: [tegenover CPU-percentage van CPU-tijd](#cpu-time-vs-cpu-percentage)
* **Gegevens In**
  * Hallo hoeveelheid binnenkomende bandbreedte Hallo-app in MIB's.
* **Gegevens uit**
  * Hallo hoeveelheid bandbreedte voor uitgaande verbruikt door Hallo-app in MIB's.
* **HTTP-2xx**
  * Aantal aanvragen, wat resulteert in een http-statuscode > = 200 maar < 300.
* **HTTP-3xx**
  * Aantal aanvragen, wat resulteert in een http-statuscode > 300 maar 400 < =.
* **401 HTTP**
  * Het aantal aanvragen, wat resulteert in een 401 HTTP-statuscode.
* **HTTP-fout 403**
  * Het aantal aanvragen, wat resulteert in 403 HTTP-statuscode.
* **HTTP 404**
  * Het aantal aanvragen, wat resulteert in een HTTP 404-statuscode.
* **HTTP 406**
  * Het aantal aanvragen, wat resulteert in 406 HTTP-statuscode.
* **HTTP-4xx**
  * Aantal aanvragen, wat resulteert in een http-statuscode > = 400 maar < 500.
* **HTTP-Server-fouten**
  * Aantal aanvragen, wat resulteert in een http-statuscode > = 500 maar < 600.
* **Geheugen-werkset**
  * Huidige hoeveelheid geheugen die wordt gebruikt door de app Hallo in MIB's.
* **Aanvragen**
  * Totaal aantal aanvragen ongeacht hun resulterende HTTP-statuscode.

Voor een **App Service-abonnement**, Hallo beschikbare metrische gegevens zijn:

> [!NOTE]
> App Service plan metrische gegevens zijn alleen beschikbaar voor abonnementen in **Basic**, **standaard** en **Premium** SKU.
> 
> 

* **CPU-Percentage**
  * Hallo gemiddelde CPU-gebruik over alle exemplaren van Hallo plan.
* **Geheugenpercentage**
  * Hallo gemiddelde geheugen gebruikt in alle exemplaren van Hallo plan.
* **Gegevens In**
  * Hallo gemiddelde binnenkomende bandbreedte die wordt gebruikt in alle exemplaren van Hallo plan.
* **Gegevens uit**
  * Hallo gemiddelde bandbreedte die wordt gebruikt in alle exemplaren van Hallo plan uitgaande.
* **Wachtrijlengte voor schijf**
  * Hallo gemiddeld aantal lees door en schrijfaanvragen die in de wachtrij zijn geplaatst in de opslag. Een hoge wachtrijlengte is een indicatie van een toepassing die mogelijk vanwege tooexcessive schijf-i/o vertragen.
* **HTTP-wachtrijlengte**
  * Hallo gemiddelde aantal HTTP-aanvragen dat toosit op Hallo wachtrij had voordat het wordt voldaan. Een hoog of toenemende HTTP-wachtrijlengte is een symptoom van een plan zwaar wordt belast.

### <a name="cpu-time-vs-cpu-percentage"></a>Vs CPU-percentage van CPU-tijd
<!-- toodo: Fix Anchor (#CPU-time-vs.-CPU-percentage) -->

Er zijn 2 metrische gegevens die overeenkomen met het CPU-gebruik. **CPU-tijd** en **CPU-percentage**

**CPU-tijd** is nuttig voor apps die worden gehost **vrije** of **gedeelde** plannen omdat een van hun quota is gedefinieerd in CPU minuten door Hallo app gebruikt.

**CPU-percentage** op Hallo daarentegen is nuttig voor apps die worden gehost **basic**, **standaard** en **premium** plannen omdat ze kunnen worden uitgebreid en deze metrische gegevens is een goede indicatie van Hallo algemene gebruik in alle exemplaren.

## <a name="metrics-granularity-and-retention-policy"></a>Samenvattingen van de metrische gegevens en bewaarbeleid
Metrische gegevens voor een toepassing en de app service-abonnement zijn geregistreerd en geaggregeerd door Hallo service Hello granulaties en bewaarbeleid te volgen:

* **Minuut** granulatie metrische gegevens worden bewaard voor **48 uur**
* **Uur** granulatie metrische gegevens worden bewaard voor **30 dagen**
* **Dag** granulatie metrische gegevens worden bewaard voor **90 dagen**

## <a name="monitoring-quotas-and-metrics-in-hello-azure-portal"></a>Quota's en metrische gegevens controleren in hello Azure-Portal.
U kunt de status Hallo Hallo verschillende bekijken **quota** en **metrische gegevens** die invloed hebben op een toepassing in Hallo [Azure Portal](https://portal.azure.com).

![][quotas]
**Quota's** vindt u onder Instellingen >**quota**. Hallo UX kunt u bekijken: de naam van de quota's (1) hello, (2) het interval opnieuw instellen, (3) de huidige limiet en (4) de huidige waarde.

![][metrics]
**Metrische gegevens** toegang rechtstreeks vanaf de resourceblade Hallo kan zijn. U kunt ook aanpassen Hallo grafiek door: (1) **klikt u op** op en selecteert u (2) **grafiek bewerken**.
Hier kunt u hello (3) **tijdsbereik**, (4) **grafiektype**, en 5, **metrische gegevens** toodisplay.  

U kunt meer informatie over metrische gegevens hier: [service metrische gegevens controleren](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).

## <a name="alerts-and-autoscale"></a>Waarschuwingen en voor automatisch schalen
Metrische gegevens voor een App of een App Service-plan kan worden aangesloten tooalerts, toolearn meer over deze, Zie [ontvangen van meldingen van waarschuwingen](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

App Service-apps die zijn gehost in basic, standard of premium App Service-abonnementen ondersteunen **automatisch schalen**. Hiermee kunt u tooconfigure regels die de App Service plan metrische gegevens controleren en kunnen vergroten of verkleinen Hallo exemplaren verstrekken aanvullende bronnen die nodig is of opslaan money wanneer de toepassing hello te veel inrichten. U kunt meer informatie over automatisch schalen hier: [hoe tooScale](../monitoring-and-diagnostics/insights-how-to-scale.md) en hier [Best practices voor het bewaken van de Azure-automatisch schalen](../monitoring-and-diagnostics/insights-autoscale-best-practices.md)

> [!NOTE]
> Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
> 
> 

## <a name="whats-changed"></a>Wat is er gewijzigd
* Zie voor een handleiding toohello wijzigingen van de Websites tooApp Service: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)

[fzilla]:http://go.microsoft.com/fwlink/?LinkId=247914
[vmsizes]:http://go.microsoft.com/fwlink/?LinkID=309169



<!-- Images. -->
[http403]: ./media/web-sites-monitor/http403.png
[quotas]: ./media/web-sites-monitor/quotas.png
[metrics]: ./media/web-sites-monitor/metrics.png
