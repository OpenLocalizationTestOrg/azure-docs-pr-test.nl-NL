---
title: aaaGet de slag met Azure Monitor | Microsoft Docs
description: Aan de slag met Azure Monitor toogain inzicht in de bewerking van uw resources Hallo en actie onderneemt op basis van gegevens.
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: ce2930aa-fc41-4b81-b0cb-e7ea922467e1
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: johnkem
ms.openlocfilehash: 49e7105621a9e60c9fa14c4911c4fe45e0d197a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-monitor"></a>Aan de slag met Azure Monitor
Monitor voor Azure is Hallo platformservice en één bron biedt voor het bewaken van de Azure-resources. Met Azure-Monitor kunt u visualiseren, query, routeren, archiveren en Neem maatregelen op Hallo metrische gegevens en de logboeken die afkomstig zijn van bronnen in Azure. U kunt werken met deze gegevens met behulp van Hallo Monitor portalblade, [Monitor PowerShell-Cmdlets](insights-powershell-samples.md), [platformoverschrijdende CLI](insights-cli-samples.md), of [Monitor REST-API's van Azure](https://msdn.microsoft.com/library/dn931943.aspx). In dit artikel doorlopen we een aantal belangrijke onderdelen van de Monitor Azure, met Hallo portal for demonstratie Hallo.

1. Navigeer te in Hallo portal**meer services** en Hallo zoeken **Monitor** optie. Klik op Hallo sterpictogram tooadd de favorietenlijst van deze optie tooyour zodat deze altijd eenvoudig toegankelijk vanaf de linkernavigatiebalk Hallo.
   
    ![In de lijst met services Hallo controleren](./media/monitoring-get-started/monitor-more-services.png)
2. Klik op Hallo **Monitor** optie tooopen up Hallo **Monitor** blade. In deze blade zijn al uw controle-instellingen en -gegevens bijeengebracht in één geconsolideerde weergave. Het eerst wordt geopend toohello **activiteitenlogboek** sectie.
   
    ![Navigatie in de blade Monitor](./media/monitoring-get-started/monitor-blade-nav.png)
   
    Azure Monitor heeft drie categorieën van bewakingsgegevens: Hallo **activiteitenlogboek**, **metrische gegevens**, en **diagnostische logboeken**.
3. Klik op **activiteitenlogboek** tooensure die Hallo uplogboekgedeelte van de activiteit wordt weergegeven.
   
    ![Blade met activiteitenlogboek](./media/monitoring-get-started/monitor-act-log-blade.png)
   
    Hallo [ **activiteitenlogboek** ](monitoring-overview-activity-logs.md) beschrijft alle bewerkingen die worden uitgevoerd op resources in uw abonnement. Hallo activiteitenlogboek gebruikt, u kunt bepalen Hallo ' wat, wie, en wanneer ' voor eventuele maken, bijwerken of verwijderen van bewerkingen op resources in uw abonnement. Bijvoorbeeld, Hallo activiteitenlogboek geeft aan wanneer een web-app is gestopt en die is gestopt. Activiteit logboekgebeurtenissen worden opgeslagen in het Hallo-platform en beschikbare tooquery gedurende 90 dagen.
   
    U kunt maken en query's voor algemene filters vervolgens pincode Hallo belangrijkste query's tooa portaldashboard opslaan zodat u altijd weet als de gebeurtenissen die voldoen aan uw criteria hebben plaatsgevonden.
4. Hallo weergave tooa resourcegroep via Hallo afgelopen week filteren, en klik vervolgens op Hallo **opslaan** knop.
   
    ![Query voor activiteitenlogboek opslaan](./media/monitoring-get-started/monitor-act-log-save.png)
5. Klik nu op Hallo **pincode** knop.
   
    ![Klikken op Vastmaken voor het activiteitenlogboek](./media/monitoring-get-started/monitor-act-log-pin.png)
   
    De meeste Hallo-weergaven in dit scenario kan worden vastgemaakt tooa dashboard. Hierdoor beschikt u over een enkele bron van informatie voor operationele gegevens over uw services. 
6. Dashboard tooyour retourneren. U kunt nu zien dat Hallo-query (en het aantal resultaten) wordt weergegeven in het dashboard. Dit is handig als u wilt dat tooquickly Zie hoogwaardig acties die zijn opgetreden onlangs in uw abonnement, bijv. een nieuwe rol die is toegewezen of een VM die is verwijderd.
   
    ![Activiteit logboek vastgemaakt toodashboard](./media/monitoring-get-started/monitor-act-log-db.png)
7. Retourneren van toohello **Monitor** tegel en klik op Hallo **metrische gegevens** sectie. Een resource tooselect moet u eerst door het filteren en te selecteren met behulp van de vervolgkeuzelijst opties Hallo Hallo boven aan het Hallo-blade.
   
    ![Resource voor metrische gegevens filteren](./media/monitoring-get-started/monitor-met-filter.png)
   
    [**Metrische gegevens**](monitoring-overview-metrics.md) zijn beschikbaar voor alle Azure-resources. In deze weergave ziet u alle metrische gegevens bij elkaar, zodat u gemakkelijk inzicht krijgt in de prestaties van uw resources.
8. Nadat u een resource hebt geselecteerd, worden alle beschikbare metrische gegevens weergegeven op de linkerkant van de blade Hallo Hallo. U kunt meerdere metrische gegevens in één keer grafiek door metrische gegevens te selecteren en Hallo grafiek type en bereik wijzigen. U kunt ook alle metrische waarschuwingen weergeven die zijn ingesteld voor deze resource.
   
    ![Blade met metrische gegevens](./media/monitoring-get-started/monitor-metric-blade.png)
   
   > [!NOTE]
   > Sommige metrische gegevens zijn alleen beschikbaar als u [Application Insights](../application-insights/app-insights-overview.md) en/of Windows Azure Diagnostics of Linux Azure Diagnostics inschakelt voor uw resource.
   > 
   > 
9. Wanneer u tevreden met de grafiek bent, kunt u Hallo **pincode** knop toopin het tooyour dashboard.
10. Retourneren van toohello **Monitor** blade en klik op **diagnostische logboeken**.
    
    ![Blade met diagnostische logboeken](./media/monitoring-get-started/monitor-diaglogs-blade.png)
    
    [**Diagnostische logboeken** ](monitoring-overview-of-diagnostic-logs.md) logboeken verzonden *door* een resource die gegevens over Hallo werking van die resource. Tellers van regels voor netwerkbeveiligingsgroepen en werkstroomlogboeken van logische apps zijn bijvoorbeeld allebei een type diagnostisch logboek. Deze logboeken kunnen worden opgeslagen in een opslagaccount, gestreamde tooan Event Hub en/of verzonden[logboekanalyse](../log-analytics/log-analytics-overview.md). Log Analytics is het operationele intelligence product van Microsoft voor geavanceerde zoekopdrachten en waarschuwingen.
    
    U kunt in Hallo-portal bekijken en een lijst van alle resources in uw abonnement tooidentify filteren als er diagnostische logboeken zijn ingeschakeld.
11. Klik op een resource in Hallo diagnostische logboeken blade. Als diagnostische logboeken worden opgeslagen in een opslagaccount, ziet u een lijst met uurlogboeken die u rechtstreeks kunt downloaden.
    
    ![Diagnostische logboeken voor één resource](./media/monitoring-get-started/monitor-diaglogs-detail.png)
    
    U kunt ook klikken op **diagnostische instellingen**, die kunt u tooset up of wijzig de instellingen voor archivering tooa storage-account, streaming tooEvent Hubs of het verzenden van de werkruimte voor logboekanalyse tooa.
    
    ![Diagnostische logboeken inschakelen](./media/monitoring-get-started/monitor-diaglogs-enable.png)
    
    Als u logboeken met diagnostische gegevens tooLog Analytics hebt ingesteld, kunt u vervolgens zoeken ze in Hallo **logboek zoeken** sectie van het Hallo-portal.
12. Navigeer toohello **waarschuwingen** sectie van Hallo Monitor blade.
    
    ![blade met waarschuwingen voor openbaar gebruik](./media/monitoring-get-started/monitor-alerts-nopp.png)
    
    Hier kunt u alle [**waarschuwingen**](monitoring-overview-alerts.md) voor uw Azure-resources beheren, Dit omvat waarschuwingen op de metrische gegevens, logboekgebeurtenissen activiteit, Application Insights-webtests (locaties) en Application Insights proactieve diagnostische gegevens. Waarschuwingen kunnen resulteren in een e-toobe verzonden of een HTTP POST tooa webhook-URL.
13. Klik op **metrische waarschuwing toevoegen** toocreate een waarschuwing.
    
    ![metrische waarschuwing toevoegen](./media/monitoring-get-started/monitor-alerts-add.png)
    
    U kunt vervolgens een waarschuwing tooyour dashboard tooeasily pincode raadpleegt de status op elk gewenst moment.
14. Hallo Monitor sectie bevat ook koppelingen te[Application Insights](../application-insights/app-insights-overview.md) toepassingen en [logboekanalyse](../log-analytics/log-analytics-overview.md) oplossingen. Deze andere Microsoft-producten zijn vergaand geïntegreerd met Azure Monitor.
15. Als u Application Insights of Log Analytics niet gebruikt, dan werkt Azure Monitor mogelijk samen met de producten van derden die u gebruikt voor controle, logboekregistratie en waarschuwingen. Zie onze [pagina partners](monitoring-partners.md) voor een volledige lijst en instructies voor het toointegrate.

Door deze stappen te volgen en alle relevante tegels tooa dashboard vastmaken, kunt u uitgebreide weergaven van uw toepassing en de infrastructuur zoals deze:

![Azure Monitor-dashboard](./media/monitoring-get-started/monitor-final-dash.png)

## <a name="next-steps"></a>Volgende stappen
* Lees Hallo [overzicht van Azure-Monitor](monitoring-overview.md)

