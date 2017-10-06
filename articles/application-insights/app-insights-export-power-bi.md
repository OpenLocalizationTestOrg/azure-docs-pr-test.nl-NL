---
title: aaaExport tooPower BI van Application Insights | Microsoft Docs
description: Analytics-query's kunnen worden weergegeven in Power BI.
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 7f13ea66-09dc-450f-b8f9-f40fdad239f2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: 6668cd7f4e0fbf41695972617f5f8ec207356659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="feed-power-bi-from-application-insights"></a>Power BI feed vanuit Application Insights
[Power BI](http://www.powerbi.com/) is een suite met business analytics hulpmiddelen waarmee u gegevens analyseren en inzichten te delen. Uitgebreide dashboards zijn beschikbaar op elk apparaat. U kunt gegevens uit diverse bronnen, met inbegrip van analysequery's van combineren [Azure Application Insights](app-insights-overview.md).

Er zijn drie aanbevolen methoden voor het exporteren van Application Insights gegevens tooPower BI. U kunt deze afzonderlijk of samen gebruiken.

* [**Power BI adapter** ](#power-pi-adapter) -instellen van een volledig dashboard telemetrie van uw app. Hallo set grafieken vooraf wordt gedefinieerd, maar u kunt uw eigen query's uit andere bronnen toevoegen.
* [**Exporteren van analysequery's** ](#export-analytics-queries) -schrijven van een query die u wilt met Analytics en tooPower BI exporteren. U kunt deze query op een dashboard samen met andere gegevens plaatsen.
* [**Continue export en Stream Analytics** ](app-insights-export-stream-analytics.md) -hierbij meer werk tooset up. Dit is handig als u wilt dat tookeep gegevens gedurende langere perioden. Anders worden hello andere methoden aanbevolen.

## <a name="power-bi-adapter"></a>Power BI-adapter
Deze methode maakt u een volledig dashboard telemetrie voor u. Hallo initiële gegevensset is vooraf gedefinieerd, maar u kunt meer gegevens tooit toevoegen.

### <a name="get-hello-adapter"></a>Hallo adapter ophalen
1. Aanmelden te[Power BI](https://app.powerbi.com/).
2. Open **gegevens ophalen**, **Services**, **Application Insights**
   
    ![Ophalen van Application Insights-gegevensbron](./media/app-insights-export-power-bi/power-bi-adapter.png)
3. Geef details op Hallo van uw Application Insights-resource.
   
    ![Ophalen van Application Insights-gegevensbron](./media/app-insights-export-power-bi/azure-subscription-resource-group-name.png)
4. Wacht een minuut of twee Hallo gegevens toobe geïmporteerd.
   
    ![Power BI-adapter](./media/app-insights-export-power-bi/010.png)

U kunt dashboard Hallo Hallo Application Insights grafieken combineren met die van andere bronnen en met analysequery's bewerken. Er is een visualisatie galerie krijgt u meer grafieken, waarbij elke grafiek heeft een parameters die u kunt instellen.

Na Hallo blijven importeren in eerste instantie, Hallo dashboard en rapporten Hallo tooupdate dagelijks. U kunt het schema voor gegevensvernieuwing Hallo op Hallo gegevensset beheren.

## <a name="export-analytics-queries"></a>Analysequery's exporteren
Deze route kunt u toowrite eventuele Analytics query u zoals en exporteert u dat tooa Power BI-dashboard. (U kunt toohello dashboard dat is gemaakt door Hallo-adapter toevoegen).

### <a name="one-time-install-power-bi-desktop"></a>Eén keer: Installeer Power BI Desktop
tooimport uw query Application Insights u Hallo bureaubladversie van Power BI gebruiken. Maar vervolgens kunt u deze publiceren toohello web- of tooyour Power BI cloud werkruimte. 

Installeer [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).

### <a name="export-an-analytics-query"></a>Exporteren van een query Analytics
1. [Open Analytics en uw query schrijven](app-insights-analytics-tour.md).
2. Testen en Hallo-query te verfijnen totdat u tevreden met Hallo resultaten bent.

   **Zorg ervoor dat deze Hallo-query wordt uitgevoerd correct in Analytics voordat u dit exporteren.**
3. Op Hallo **exporteren** menu kiezen **Power BI (M)**. Hallo-tekstbestand opslaan.
   
    ![Power BI query exporteren](./media/app-insights-export-power-bi/analytics-export-power-bi.png)
4. In Power BI Desktop selecteer **gegevens ophalen, lege Query** en klik vervolgens in Hallo-query-editor, onder **weergave** Selecteer **geavanceerde Query-Editor**.

    Plakken Hallo geëxporteerd M taal script in Hallo geavanceerde Query-Editor.

    ![Geavanceerde query-editor](./media/app-insights-export-power-bi/power-bi-import-analytics-query.png)

1. Mogelijk hebt u tooprovide referenties tooallow Power BI tooaccess Azure. Gebruik 'organisatieaccount' toosign met uw Microsoft-account.
   
    ![Azure-referenties tooenable Power BI toorun uw Application Insights-query opgeven](./media/app-insights-export-power-bi/power-bi-import-sign-in.png)

    (Als u tooverify Hallo referenties nodig hebt, gebruik Hallo Gegevensbroninstellingen menuopdracht in Hallo Query-Editor. Maatregelen treffen toospecify Hallo referenties voor Azure, dit van uw referenties voor Power BI afwijken kan.)
2. Kies een visualisatie in voor uw query en selecteer de velden Hallo voor x-as, y-as en dimensie segmenteren.
   
    ![Visualisatie selecteren](./media/app-insights-export-power-bi/power-bi-analytics-visualize.png)
3. Publiceren van uw rapport tooyour Power BI cloud-werkruimte. Daar kunt u een gesynchroniseerde versie insluiten in andere webpagina's.
   
    ![Visualisatie selecteren](./media/app-insights-export-power-bi/publish-power-bi.png)
4. Hallo rapport handmatig vernieuwen met tussenpozen of een geplande vernieuwing op de optiepagina voor Hallo instelt.

## <a name="troubleshooting"></a>Problemen oplossen

### <a name="401-or-403-unauthorized"></a>401- of 403 niet geautoriseerd 
Dit kan gebeuren als uw refesh-token is niet bijgewerkt. Probeer deze stappen tooensure u nog steeds toegang hebben. Als u toegang hebt en refershing Hallo referenties niet werkt, opent u een ondersteuningsticket.

1. Meld u aan bij hello Azure-Portal en controleer of dat u toegang hebt tot Hallo resource
2. Probeer toorefresh Hallo referenties voor Hallo Dashboard

### <a name="502-bad-gateway"></a>502 Slechte Gateway
Dit wordt meestal veroorzaakt door een Analytics-query die te veel gegevens retourneert. Moet u proberen met behulp van een kleinere tijdsbereik of met behulp van Hallo [geleden](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago) of [startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek) werkt alleen [project](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator) Hallo velden die u nodig hebt.

Als verminderen Hallo gegevensset afkomstig is van Hallo Analytics query niet voldoet aan uw vereisten moet u overwegen Hallo [API](https://dev.applicationinsights.io/documentation/overview) toopull een grotere gegevensset. Hier vindt u instructies over hoe de toouse Hallo API voor het exporteren van tooconvert Hallo M-Query.

1. Maak een [API-sleutel](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID)
2. Update Hallo Power BI-M-script dat u hebt geëxporteerd van analytische gegevens door te vervangen Hallo ARM-URL met AI-API (Zie onderstaand voorbeeld)
   * Vervang **https://management.azure.com/subscriptions/...**
   * met **https://api.applicationinsights.io/beta/apps/...**
3. Ten slotte toobasic referenties bijwerken en gebruik van uw API-sleutel
  

**Bestaand Script**
 ```
 Source = Json.Document(Web.Contents("https://management.azure.com/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups//providers/microsoft.insights/components//api/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```
**Bijgewerkte Script**
 ```
 Source = Json.Document(Web.Contents("https://api.applicationinsights.io/beta/apps/<APPLICATION_ID>/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```

## <a name="about-sampling"></a>Over steekproeven
Als uw toepassing grote hoeveelheden gegevens verzendt, mag de functie voor adaptieve steekproeven Hallo werkt en slechts een percentage van uw telemetrie verzenden. Hallo geldt ook als u hebt de steekproef nemen handmatig ingesteld in Hallo SDK of op de opname. [Meer informatie over steekproeven.](app-insights-sampling.md)


## <a name="next-steps"></a>Volgende stappen
* [Power BI - informatie](http://www.powerbi.com/learning/)
* [Analytics-zelfstudie](app-insights-analytics-tour.md)

