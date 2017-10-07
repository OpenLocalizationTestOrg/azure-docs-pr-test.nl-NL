---
title: aaaMicrosoft Dynamics CRM en Azure Application Insights | Microsoft Docs
description: Telemetrie ophalen uit Microsoft Dynamics CRM Online met behulp van Application Insights. Overzicht van setup ophalen van gegevens, visualisatie en exporteren.
services: application-insights
documentationcenter: 
author: mazharmicrosoft
manager: carmonm
ms.assetid: 04c66338-687e-49e5-9975-be935f98f156
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/16/2017
ms.author: bwren
ms.openlocfilehash: a39398060d6553fb18a26c101f085b7d87443636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-enabling-telemetry-for-microsoft-dynamics-crm-online-using-application-insights"></a>Overzicht: Telemetrie voor Microsoft Dynamics CRM Online met behulp van Application Insights inschakelen
Dit artikel ziet u hoe tooget telemetriegegevens van [Microsoft Dynamics CRM Online](https://www.dynamics.com/) met [Azure Application Insights](https://azure.microsoft.com/services/application-insights/). We doorlopen Hallo complete proces van Application Insights-script tooyour toepassing toe te voegen, het vastleggen van gegevens en gegevensvisualisatie.

> [!NOTE]
> [Hallo Voorbeeldoplossing Bladeren](https://dynamicsandappinsights.codeplex.com/).
> 
> 

## <a name="add-application-insights-toonew-or-existing-crm-online-instance"></a>Application Insights toonew of bestaande CRM Online-instantie toevoegen
toomonitor uw toepassing toevoegen van een Application Insights-SDK tooyour-toepassing. Hallo SDK verzendt telemetrie toohello [Application Insights-portal](https://portal.azure.com), kunt u gebruik van onze krachtige analyse en diagnostische hulpprogramma's, of Hallo gegevens toostorage exporteren.

### <a name="create-an-application-insights-resource-in-azure"></a>Een Application Insights-resource maken in Azure
1. Ophalen van [een account in Microsoft Azure](http://azure.com/pricing). 
2. Meld u aan bij Hallo [Azure-portal](https://portal.azure.com) en een nieuwe Application Insights-resource toevoegen. Dit is waar uw gegevens worden verwerkt en weergegeven.
   
    ![Klik op +, Ontwikkelaarsservices, Application Insights.](./media/app-insights-sample-mscrm/01.png)
   
    Kies ASP.NET als Hallo toepassingstype.
3. Open de pagina aan de slag Hallo en ' bewaken en onderzoeken van client-side '.
   
    ![Codefragment voor het invoegen in uw webpagina](./media/app-insights-sample-mscrm/03.png)

**Hallo-codetabel openhouden** terwijl u de volgende stap in een ander browservenster Hallo. U moet binnenkort Hallo-code. 

### <a name="create-a-javascript-web-resource-in-microsoft-dynamics-crm"></a>Een JavaScript-web-resource maken in Microsoft Dynamics CRM
1. Open uw CRM Online-instantie en aanmelding met administrator-bevoegdheden.
2. Open Microsoft Dynamics CRM-instellingen aanpassingen, aanpassen Hallo systeem
   
    ![Microsoft Dynamics CRM-instellingen](./media/app-insights-sample-mscrm/04.png)
   
    ![Instellingen > aanpassingen](./media/app-insights-sample-mscrm/05.png)

    ![Hallo Systeemoptie aanpassen](./media/app-insights-sample-mscrm/06.png)

1. Maak een JavaScript-resource.
   
    ![Dialoogvenster nieuwe webbron](./media/app-insights-sample-mscrm/07.png)
   
    Geef het een naam, selecteer **Script (JScript)** en open Hallo teksteditor.
   
    ![Open Hallo teksteditor](./media/app-insights-sample-mscrm/08.png)
2. Hallo-code van de Application Insights kopiëren. Zorg ervoor dat tooignore scriptlabels tijdens het kopiëren van. Raadpleeg de onderstaande schermafbeelding:
   
    ![De instrumentatiesleutel instellen](./media/app-insights-sample-mscrm/09.png)
   
    Hallo-code bevat Hallo instrumentatiesleutel die uw Application insights-resource identificeert.
3. Opslaan en publiceren.
   
    ![Opslaan en publiceren](./media/app-insights-sample-mscrm/10.png)

### <a name="instrument-forms"></a>Instrument formulieren
1. Open in Microsoft CRM Online formulier Hallo-Account
   
    ![Accountformulier](./media/app-insights-sample-mscrm/11.png)
2. Hallo formulier eigenschappen openen
   
    ![Eigenschappen van formulier](./media/app-insights-sample-mscrm/12.png)
3. Hallo JavaScript webbron die u hebt gemaakt toevoegen
   
    ![Menu toevoegen](./media/app-insights-sample-mscrm/13.png)
   
    ![Hallo webbron toevoegen](./media/app-insights-sample-mscrm/14.png)
4. Opslaan en publiceren van uw aanpassingen van formulieren.

## <a name="metrics-captured"></a>Metrische gegevens vastgelegd
U hebt nu het vastleggen van telemetriegegevens voor Hallo formulier ingesteld. Wanneer deze wordt gebruikt, worden gegevens verzonden tooyour Application Insights-resource.

Hier vindt u voorbeelden van Hallo-gegevens die u ziet.

#### <a name="application-health"></a>Toepassingsstatus
![Voorbeeld van de paginalaadtijd](./media/app-insights-sample-mscrm/15.png)

![Voorbeeld pagina weergaven grafiek](./media/app-insights-sample-mscrm/16.png)

Browseruitzonderingen:

![Grafiek met serveruitzonderingen klikken](./media/app-insights-sample-mscrm/17.png)

Klik op Hallo grafiek tooget meer detail:

![Lijst met uitzonderingen](./media/app-insights-sample-mscrm/18.png)

#### <a name="usage"></a>Gebruik
![Gebruikers, sessies en paginaweergaven](./media/app-insights-sample-mscrm/19.png)

![Sesion grafieken](./media/app-insights-sample-mscrm/20.png)

![Browserversies](./media/app-insights-sample-mscrm/21.png)

#### <a name="browsers"></a>Browsers
![Overzicht van de laadtijd van pagina](./media/app-insights-sample-mscrm/22.png)

![Het aantal sessies per browserversie](./media/app-insights-sample-mscrm/23.png)

#### <a name="geolocation"></a>Geolocatie
![Het aantal sessies per land](./media/app-insights-sample-mscrm/24.png)

![Sessies en gebruikers per land](./media/app-insights-sample-mscrm/25.png)

#### <a name="inside-page-view-request"></a>Inside pagina-aanvraag voor weergave
![Overzicht van de pagina weergeven](./media/app-insights-sample-mscrm/26.png)

![Zoeken op de pagina-gebeurtenissen weergeven](./media/app-insights-sample-mscrm/27.png)

![Vergelijkbare paginaweergaven](./media/app-insights-sample-mscrm/28.png)

![Eigenschappen van paginaweergaven](./media/app-insights-sample-mscrm/29.png)

![Pagina's per sessie](./media/app-insights-sample-mscrm/30.png)

## <a name="sample-code"></a>Voorbeeldcode
[Hallo voorbeeldcode Bladeren](https://dynamicsandappinsights.codeplex.com/).

## <a name="power-bi"></a>Power BI
U kunt zelfs grondigere analyse doen als u [exporteren Hallo gegevens tooMicrosoft Power BI](app-insights-export-power-bi.md).

## <a name="sample-microsoft-dynamics-crm-solution"></a>Voorbeeld Microsoft Dynamics CRM-oplossing
[Hier volgt Hallo Voorbeeldoplossing geïmplementeerd in Microsoft Dynamics CRM](https://dynamicsandappinsights.codeplex.com/).

## <a name="learn-more"></a>Meer informatie
* [Wat is Application Insights?](app-insights-overview.md)
* [Application Insights voor webpagina 's](app-insights-javascript.md)
* [Meer voorbeelden en scenario 's](app-insights-code-samples.md)
