---
title: waarschuwingen voor Azure-services - aaaCreate Azure-portal | Microsoft Docs
description: Trigger e-mailberichten, meldingen, worden URL's van websites (webhooks) of automation aanroepen wanneer Hallo door u opgegeven voorwaarden wordt voldaan.
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: f7457655-ced6-4102-a9dd-7ddf2265c0e2
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/23/2016
ms.author: robb
ms.openlocfilehash: 78d862d25255cda9fdfe347329e908a471c39846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---azure-portal"></a>Metrische waarschuwingen in de Azure-Monitor maken voor Azure-services - Azure-portal
> [!div class="op_single_selector"]
> * [Portal](insights-alerts-portal.md)
> * [PowerShell](insights-alerts-powershell.md)
> * [CLI](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a>Overzicht
Dit artikel laat zien hoe tooset Azure metrische waarschuwingen met behulp van hello Azure-portal.   

U kunt een waarschuwing op basis van bewaking metrische gegevens voor of gebeurtenissen op uw Azure-services kunt ontvangen.

* **Metrische waarden** - hello triggers waarschuwen wanneer Hallo-waarde van een opgegeven metriek overschrijdt de drempelwaarde die u in beide richtingen toewijst. Dat wil zeggen, deze beide wordt geactiveerd wanneer eerst aan Hallo voorwaarde wordt voldaan en vervolgens later wanneer die voorwaarde wordt niet langer wordt voldaan.    
* **Activiteit logboekgebeurtenissen** -een waarschuwing kunt activeren voor *elke* gebeurtenis of alleen wanneer een bepaalde gebeurtenissen optreden. meer informatie over de activiteit logboek waarschuwingen toolearn [Klik hier](monitoring-activity-log-alerts.md)

Een metriek waarschuwing toodo Hallo volgen wanneer deze wordt geactiveerd, kunt u configureren:

* verzenden van e-mailmeldingen toohello servicebeheerder en medebeheerders
* e-mail verzenden tooadditional e-mails die u opgeeft.
* een webhook aanroepen
* starten van de uitvoering van een Azure-runbook (alleen van hello Azure-portal)

U kunt configureren en ophalen van informatie over metrische waarschuwingsregels met

* [Azure Portal](insights-alerts-portal.md)
* [PowerShell](insights-alerts-powershell.md)
* [opdrachtregelinterface (CLI)](insights-alerts-command-line-interface.md)
* [Monitor voor Azure REST-API](https://msdn.microsoft.com/library/azure/dn931945.aspx)

## <a name="create-an-alert-rule-on-a-metric-with-hello-azure-portal"></a>Een waarschuwingsregel maken op een metriek Hello Azure-portal
1. In Hallo [portal](https://portal.azure.com/), zoekt Hallo resource u geïnteresseerd bent in de bewaking en selecteert u deze.

2. Selecteer **waarschuwingen** of **waarschuwing regels** onder Hallo sectie bewaking. tekst Hello en pictogram kunnen enigszins verschillen voor verschillende resources.  

    ![Bewaking](./media/insights-alerts-portal/AlertRulesButton.png)

3. Selecteer Hallo **waarschuwing toevoegen** opdracht en Hallo invullen.

    ![Waarschuwing toevoegen](./media/insights-alerts-portal/AddAlertOnlyParamsPage.png)

4. **Naam** uw Waarschuwing regel en kies een **beschrijving**, die ook weergegeven in e-mailmeldingen.

5. Selecteer Hallo **metriek** u wilt dat toomonitor en kies vervolgens een **voorwaarde** en **drempelwaarde** waarde voor metriek Hallo. Hallo hebt gekozen **periode** hoelang Hallo metriek regel moet worden voldaan voordat de waarschuwing Hallo-triggers. Dus bijvoorbeeld, als u Hallo periode 'PT5M' en de waarschuwing CPU dan 80 zoekt %, Hallo waarschuwing wordt geactiveerd wanneer Hallo CPU is al consistent bovenstaande 80% 5 minuten. Zodra de eerste trigger Hallo plaatsvindt, deze opnieuw wordt geactiveerd wanneer Hallo CPU onder 80% gedurende vijf minuten blijft. Hallo meting van CPU doet zich voor elke 1 minuut.   

6. Controleer **e-eigenaars...**  als u wilt dat beheerders en medebeheerders toobe per e-mail verzonden wanneer Hallo waarschuwing wordt geactiveerd.

7. Als u aanvullende e-mailberichten tooreceive een melding wanneer hello wilt waarschuwing wordt geactiveerd, toe te voegen in Hallo **aanvullende beheerder email(s)** veld. Scheid meerdere e-mailberichten met puntkomma's -  *email@contoso.com;email2@contoso.com*

8. In een geldige URI in Hallo plaatsen **Webhook** veld als u wilt dat deze wordt aangeroepen wanneer Hallo waarschuwing wordt geactiveerd.

9. Als u Azure Automation gebruikt, kunt u een Runbook toobe uitgevoerd wanneer het Hallo-waarschuwing wordt geactiveerd.

10. Selecteer **OK** wanneer gereed toocreate Hallo waarschuwing.   

Binnen een paar minuten Hallo waarschuwing actief is en wordt geactiveerd als eerder beschreven.

## <a name="managing-your-alerts"></a>Uw waarschuwingen beheren
Wanneer u een waarschuwing hebt gemaakt, kunt u deze selecteren en:

* Een grafiek weer met Hallo metrische drempel en de werkelijke waarden van Hallo Hallo vorige dag weergeven.
* Bewerk of verwijder deze.
* **Schakel** of **inschakelen** als u wilt dat tootemporarily stoppen of te hervatten ontvangen van meldingen voor deze waarschuwing.

## <a name="next-steps"></a>Volgende stappen
* [Een overzicht van Azure monitoring](monitoring-overview.md) inclusief Hallo typen gegevens u kunt verzamelen en controleren.
* Meer informatie over [configureren van webhooks in waarschuwingen](insights-webhooks-alerts.md).
* Meer informatie over [waarschuwingen configureren op activiteit logboekgebeurtenissen](monitoring-activity-log-alerts.md).
* Meer informatie over [Azure Automation-Runbooks](../automation/automation-starting-a-runbook.md).
* Ophalen van een [overzicht van diagnostische logboeken](monitoring-overview-of-diagnostic-logs.md) en gedetailleerde hoge frequentie metrische gegevens verzamelen over uw service.
* Ophalen van een [overzicht van metrische gegevens verzameling](insights-how-to-customize-monitoring.md) toomake ervoor dat uw service beschikbaar is en reageert.
