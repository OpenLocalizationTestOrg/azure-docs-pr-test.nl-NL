---
title: aaaOverview van waarschuwingen in Microsoft Azure en Azure Monitor | Microsoft Docs
description: Waarschuwingen kunnen u toomonitor Azure-resource metrische gegevens en gebeurtenissen en logboeken en worden gewaarschuwd wanneer een opgegeven voorwaarde wordt voldaan.
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: a6dea224-57bf-43d8-a292-06523037d70b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: robb
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d080080666fedc9eefda6b35cdea3714785d2223
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-alerts-in-microsoft-azure"></a>Wat zijn de waarschuwingen in Microsoft Azure?
Dit artikel wordt beschreven Hallo verschillende bronnen van waarschuwingen in Microsoft Azure, wat zijn Hallo doeleinden voor waarschuwingen, hun voordelen en hoe tooget gestart met het gebruik ervan. Specifiek geldt tooAzure Monitor maar aanwijzers tooother services biedt ook waarschuwingen. Waarschuwingen bieden een methode voor het bewaken in Azure die kunt u voorwaarden tooconfigure over gegevens en worden gewaarschuwd als Hallo voorwaarden overeenkomen met de meest recente bewakingsgegevens Hallo.

## <a name="taxonomy-of-azure-alerts"></a>Taxonomie van waarschuwingen van Azure
Maakt gebruik van Azure Hallo volgende termen toodescribe waarschuwingen en hun functies:
* **Waarschuwing** -definitie van een van de criteria (een of meer regels of -voorwaarden) die wordt geactiveerd wanneer voldaan.
* **Actieve** - hello status wanneer hello criteria die zijn gedefinieerd door een waarschuwing wordt voldaan.
* **Opgelost** - hello status wanneer hello criteria die zijn gedefinieerd door een waarschuwing niet meer na een eerder zijn voldaan wordt voldaan.
* **Melding** -actie op die op basis van een waarschuwing actief Hallo.
* **Actie** -specifieke aanroep verzonden tooa ontvanger van een melding (bijvoorbeeld e-mailen een adres of boeken tooa webhook-URL). Meldingen kunnen meestal meerdere acties activeren.

## <a name="alerts-in-different-azure-services"></a>Waarschuwingen in verschillende Azure-services
Waarschuwingen zijn beschikbaar in verschillende Azure-services controleren. Voor informatie over hoe en wanneer toouse deze-services, [Raadpleeg dit artikel](./monitoring-overview.md). Hier volgt een overzicht van Waarschuwingstypen Hallo beschikbaar in Azure:

| Service | Waarschuwingstype | Ondersteunde services | Beschrijving |
|---|---|---|---|
| Azure Monitor | [Metrische waarschuwingen](./insights-alerts-portal.md) | [Ondersteunde metrische gegevens van de Azure-Monitor](./monitoring-supported-metrics.md) | Een melding ontvangen wanneer een metriek platform niveau voldoet aan een bepaalde voorwaarde (bijvoorbeeld, CPU-percentage op een virtuele machine is groter dan 90 voor Hallo afgelopen vijf minuten). |
| Azure Monitor | [Activiteit logboek waarschuwingen](./monitoring-activity-log-alerts.md) | Alle brontypen die beschikbaar zijn in Azure Resource Manager | Ontvangt een melding wanneer een nieuwe gebeurtenis in Hallo [Azure Activity Log](./monitoring-overview-activity-logs.md) overeenkomt met bepaalde voorwaarden (bijvoorbeeld, als er een bewerking 'VM verwijderen' optreedt in myProductionResourceGroup of de wanneer een nieuwe gebeurtenis servicestatus met 'Active' als Hallo-status wordt weergegeven). |
| Application Insights | [Metrische waarschuwingen](../application-insights/app-insights-alerts.md) | Elke toepassing geïnstrumenteerd toosend gegevens tooApplication Insights | Een melding ontvangen wanneer een metriek op toepassingsniveau voldoet aan een bepaalde voorwaarde (bijvoorbeeld serverreactietijd is groter dan 2 seconden). |
| Application Insights | [Waarschuwingen voor web-test](../application-insights/app-insights-monitor-web-app-availability.md) | Een website geïnstrumenteerd toosend gegevens tooApplication Insights | U ontvangt een melding wanneer de beschikbaarheid of reactiesnelheid van een website lager dan de verwachtingen is. |
| Log Analytics | [Log Analytics waarschuwingen](../log-analytics/log-analytics-alerts.md) | Elke service geconfigureerd toosend gegevens in Log Analytics | Een melding ontvangen wanneer een zoekquery logboekanalyse over metrische gegevens en/of gebeurtenis gegevens aan bepaalde criteria voldoet. |

## <a name="alerts-on-azure-monitor-data"></a>Waarschuwingen op gegevens van de Azure-Monitor
Er zijn twee typen waarschuwingen van de gegevens beschikbaar zijn vanuit Azure Monitor--metrische waarschuwingen en het activiteitenlogboek waarschuwingen.

* **Metrische waarschuwingen** -deze waarschuwing wordt geactiveerd wanneer het Hallo-waarde van een opgegeven metriek overschrijdt de drempelwaarde die u toewijst. Hallo waarschuwing genereert een melding wanneer de waarschuwing Hallo is 'geactiveerd' (als Hallo drempelwaarde is overschreden en Hallo waarschuwing voorwaarde wordt voldaan), evenals wanneer deze 'opgelost is' (wanneer Hallo drempelwaarde opnieuw wordt gepasseerd en niet langer aan Hallo voorwaarde wordt voldaan). Zie voor een groeiende lijst met beschikbare metrische gegevens die worden ondersteund door Azure monitor, [lijst met metrische gegevens die worden ondersteund op Azure Monitor](monitoring-supported-metrics.md).
* **Activiteit logboek waarschuwingen** -een streaming logboek waarschuwing die wordt geactiveerd wanneer een gebeurtenis activiteitenlogboek wordt gegenereerd dat overeenkomt met filtercriteria die u hebt toegewezen. Deze waarschuwingen hebben slechts één status 'Geactiveerd', omdat Hallo waarschuwings-engine gewoon Hallo filter criteria tooany nieuwe gebeurtenis geldt. Deze waarschuwingen kunnen worden gebruikt toobecome een melding wanneer er een nieuw incident in de servicestatus optreedt of als een gebruiker of toepassing een bewerking uitvoert in uw abonnement, bijvoorbeeld 'Virtuele machine verwijderen'.

We raden routering Hallo-gegevens in Log Analytics en het gebruik van een waarschuwing voor logboekanalyse voor diagnostische logboekgegevens die beschikbaar is via Azure Monitor. Hallo volgende diagram geeft een overzicht van bronnen van de gegevens in Azure Monitor en, conceptueel gezien hoe u waarschuwt af die gegevens.

![Waarschuwingen uitgelegd](./media/monitoring-overview-alerts/Alerts_Overview_Resource_v4.png)

## <a name="how-do-i-receive-a-notification-on-an-azure-monitor-alert"></a>Hoe ontvang ik een melding op een waarschuwing voor Azure?
Waarschuwingen van andere services van Azure gebruikt in het verleden hebben hun eigen ingebouwde notification-methoden. Voortaan kunt biedt Azure een herbruikbare melding groepering actiegroepen genoemd. Actiegroepen Geef een set van ontvangers voor een melding--een willekeurig aantal e-mailadressen, telefoonnummers (SMS) of webhook-URL's-- en elk gewenst moment een waarschuwing is geactiveerd dat verwijst naar een groep acties Hallo alle ontvangers die meldingen ontvangen. Hiermee kunt u een groepering van ontvangers (bijvoorbeeld uw op aanroep engineer lijst) tooreuse over veel waarschuwingen objecten. Op dit moment alleen activiteitenlogboek waarschuwingen maken gebruik van groepen in te grijpen, maar verschillende Waarschuwingstypen van andere Azure werkt ook met behulp van groepen in te grijpen.

Actie beheergroepen ondersteunen melding door boeken tooa webhook-URL in de toevoeging tooemail adressen en SMS-nummers. Hiermee kunt automation en het doorvoeren, bijvoorbeeld met behulp van:
    - Azure Automation Runbook
    - Azure-functie
    - Azure Logic App
    - een service van derden

Metrische waarschuwingen gebruik nog geen groepen in te grijpen. U kunt meldingen configureren op een afzonderlijke waarschuwing metrische:
* E-mailmeldingen toohello service administrator, tooco-beheerders of tooadditional e-mailadressen die u opgeeft verzenden.
* Aanroepen van een webhook waarmee u toolaunch extra automation acties.

## <a name="next-steps"></a>Volgende stappen
Informatie ophalen over de regels voor waarschuwingen en ze te configureren met behulp van:

* Meer informatie over [metrische gegevens](monitoring-overview-metrics.md)
* Configureer [metriek waarschuwingen per Azure-portal](insights-alerts-portal.md)
* Configureer [metriek waarschuwingen PowerShell](insights-alerts-powershell.md)
* Configureer [metriek waarschuwingen opdrachtregelinterface (CLI)](insights-alerts-command-line-interface.md)
* Configureer [metriek waarschuwingen Azure Monitor REST-API](https://msdn.microsoft.com/library/azure/dn931945.aspx)
* Meer informatie over [Activity Log](monitoring-overview-activity-logs.md)
* Configureer [activiteit logboek waarschuwingen per Azure-portal](monitoring-activity-log-alerts.md)
* Configureer [activiteit logboek waarschuwingen via Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md)
* Bekijk Hallo [activiteit logboek waarschuwing webhook schema](monitoring-activity-log-alerts-webhook.md)
* Meer informatie over [servicemeldingen](monitoring-service-notifications.md)
* Meer informatie over [actiegroepen](monitoring-action-groups.md)
