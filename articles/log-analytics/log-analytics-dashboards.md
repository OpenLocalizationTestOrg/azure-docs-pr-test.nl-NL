---
title: een aangepast dashboard in Azure-logboekanalyse aaaCreate | Microsoft Docs
description: "Deze handleiding helpt u begrijpen hoe logboekanalyse dashboards Visualiseer al uw zoekopdrachten opgeslagen logboek, zodat u één lens tooview uw omgeving."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: abb07f6c-b356-4f15-85f5-60e4415d0ba2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 73fcf131a91c743d473f37d5a40d52eaf78a7ba3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-dashboard-for-use-in-log-analytics"></a>Maken van een aangepast dashboard voor gebruik in Log Analytics

>[!NOTE]
> Als uw werkruimte bijgewerkte toohello is [nieuwe logboekanalyse querytaal](log-analytics-log-search-upgrade.md), en u geen nieuwe dashboards maken of bewerken van bestaande dashboards. 

Deze handleiding helpt u begrijpen hoe logboekanalyse dashboards Visualiseer al uw zoekopdrachten opgeslagen logboek, zodat u één lens tooview uw omgeving.

![Voorbeeld van Dashboard](./media/log-analytics-dashboards/oms-dashboards-example-dash.png)

Alle Hallo aangepaste dashboards die u in Hallo OMS-portal maakt zijn ook beschikbaar in Hallo OMS mobiele App. Zie de volgende pagina's voor meer informatie over apps Hallo Hallo.

* [Mobiele app van Microsoft Store Hallo OMS](http://www.windowsphone.com/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865)
* [Mobiele app van Apple iTunes OMS](https://itunes.apple.com/app/microsoft-operations-management/id1042424859?mt=8)

![mobiele dashboard](./media/log-analytics-dashboards/oms-search-mobile.png)

## <a name="how-do-i-create-my-dashboard"></a>Hoe maak ik mijn dashboard
toobegin, Ga toohello OMS-overzichtspagina. Ziet u Hallo **mijn Dashboard** tegel op Hallo links. Klik op het toodrill omlaag in uw dashboard.

![Overzicht](./media/log-analytics-dashboards/oms-dashboards-overview.png)

## <a name="adding-a-tile"></a>Toevoegen van een tegel
Dashboards, worden de tegels aangedreven door uw zoekopdrachten opgeslagen logboek. OMS wordt geleverd met veel en-klare opgeslagen logboek zoekopdrachten, zodat u meteen kunt beginnen. Gebruik Hallo volgende stappen overzicht hoe toobegin.

In deze dashboardweergave Hallo, klikt u op **aanpassen** tooenter modus aanpassen.

![Afbeeldingen](./media/log-analytics-dashboards/oms-dashboards-pictorial01.png)

 Hallo-Configuratiescherm dat wordt geopend aan de rechterkant Hallo van Hallo pagina geeft alle uw werkruimte opgeslagen logboek zoekopdrachten. een opgeslagen logboek zoeken als een tegel toovisualize Beweeg de muisaanwijzer over een opgeslagen zoekopdracht en klik vervolgens op Hallo **plus** symbool.

![1 tegels toevoegen](./media/log-analytics-dashboards/oms-dashboards-pictorial02.png)

Wanneer u klikt op Hallo **plus** een symbool, een nieuwe tegel wordt weergegeven in Hallo mijn dashboardweergave.

![2 tegels toevoegen](./media/log-analytics-dashboards/oms-dashboards-pictorial03.png)

## <a name="edit-a-tile"></a>Een tegel bewerken
In deze dashboardweergave Hallo, klikt u op **aanpassen** tooenter modus aanpassen. Klik op de gewenste tooedit tegel Hallo. Hallo rechterpaneel tooedit wijzigingen, en biedt een aantal opties:

![Tegel bewerken](./media/log-analytics-dashboards/oms-dashboards-pictorial04.png)

![Tegel bewerken](./media/log-analytics-dashboards/oms-dashboards-pictorial05.png)

### <a name="tile-visualizations"></a>Tegel visualisaties
Er zijn drie soorten tegel visualisaties toochoose uit:

| grafiektype | wat het programma doet |
| --- | --- |
| ![Staafdiagram](./media/log-analytics-dashboards/oms-dashboards-bar-chart.png) |Geeft een tijdlijn met uw opgeslagen logboek zoekresultaten weer als een staafdiagram of een lijst met resultaten in een veld afhankelijk van als uw zoekopdracht logboek resultaten door een veld of niet aggregeert. |
| ![Metrische gegevens](./media/log-analytics-dashboards/oms-dashboards-metric.png) |Worden uw totale logboek zoeken resultaat treffers weergegeven als een getal in een tegel. Metrische tegels kunnen u tooset een drempel die Hallo-tegel wordt gemarkeerd als Hallo drempelwaarde is bereikt. |
| ![regel](./media/log-analytics-dashboards/oms-dashboards-line.png) |Hiermee geeft u een tijdlijn van uw opgeslagen logboek resultaat gevonden in de zoekopdracht met waarden weer als een lijndiagram. |

### <a name="threshold"></a>Drempelwaarde
U kunt een drempelwaarde maken op een tegel Hallo metrische visualisatie gebruiken. Selecteer op de toocreate een drempelwaarde op Hallo tegel. Kies of toohighlight Hallo tegel wanneer Hallo waarde boven of onder de drempelwaarde voor Hallo gekozen, stel Hallo drempelwaarde hieronder.

## <a name="organizing-hello-dashboard"></a>Hallo dashboard ordenen
tooorganize uw dashboard toohello mijn dashboardweergave te navigeren en klik op **aanpassen** tooenter modus aanpassen. Klik en sleep Hallo tegel u toomove wilt en u wilt dat uw tegel toobe toowhere verplaatsen.

![Uw Dashboard ordenen](./media/log-analytics-dashboards/oms-dashboards-organize.png)

## <a name="remove-a-tile"></a>Een tegel verwijderen
een tegel tooremove toohello mijn dashboardweergave te navigeren en klik op **aanpassen** tooenter modus aanpassen. Selecteer Hallo tegel u wilt tooremove en selecteer in het rechterdeelvenster Hallo **verwijderen tegel**.

![Een tegel verwijderen](./media/log-analytics-dashboards/oms-dashboards-remove-tile.png)

## <a name="next-steps"></a>Volgende stappen
* Maak [waarschuwingen](log-analytics-alerts.md) in tooremediate problemen en Log Analytics toogenerate meldingen.
