---
title: aaaUse Azure portal toocreate SQL-Database waarschuwingen | Microsoft Docs
description: Gebruik hello Azure portal toocreate SQL-Database waarschuwingen, die meldingen of automation activeren kunnen wanneer Hallo door u opgegeven voorwaarden wordt voldaan.
author: aamalvea
manager: jhubbard
editor: 
services: sql-database
documentationcenter: 
ms.assetid: f7457655-ced6-4102-a9dd-7ddf2265c0e2
ms.service: sql-database
ms.custom: monitor and tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: aamalvea
ms.openlocfilehash: 4e494b130a26c4cdf42445cb49648fce9bf4d300
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-portal-toocreate-alerts-for-azure-sql-database-and-data-warehouse"></a>Azure portal toocreate waarschuwingen gebruiken voor Azure SQL Database en datawarehouse

## <a name="overview"></a>Overzicht
Dit artikel laat zien hoe tooset van Azure SQL Database en datawarehouse waarschuwingen met hello Azure-portal. Dit artikel bevat ook aanbevolen procedures voor het instellen van waarschuwing perioden.    

U kunt een waarschuwing op basis van bewaking metrische gegevens voor of gebeurtenissen op uw Azure-services kunt ontvangen.

* **Metrische waarden** - hello triggers waarschuwen wanneer Hallo-waarde van een opgegeven metriek overschrijdt de drempelwaarde die u in beide richtingen toewijst. Dat wil zeggen, deze beide wordt geactiveerd wanneer eerst aan Hallo voorwaarde wordt voldaan en vervolgens later wanneer die voorwaarde wordt niet langer wordt voldaan.    
* **Activiteit logboekgebeurtenissen** -een waarschuwing kunt activeren voor *elke* gebeurtenis of alleen wanneer een bepaald aantal gebeurtenissen optreden.

U kunt configureren om een waarschuwing toodo Hallo volgen wanneer deze wordt geactiveerd:

* verzenden van e-mailmeldingen toohello servicebeheerder en medebeheerders
* e-mail verzenden tooadditional e-mails die u opgeeft.
* een webhook aanroepen

U kunt configureren en informatie ophalen over met behulp van regels voor waarschuwingen

* [Azure Portal](../monitoring-and-diagnostics/insights-alerts-portal.md)
* [PowerShell](../monitoring-and-diagnostics/insights-alerts-powershell.md)
* [opdrachtregelinterface (CLI)](../monitoring-and-diagnostics/insights-alerts-command-line-interface.md)
* [Monitor voor Azure REST-API](https://msdn.microsoft.com/library/azure/dn931945.aspx)

## <a name="create-an-alert-rule-on-a-metric-with-hello-azure-portal"></a>Een waarschuwingsregel maken op een metriek Hello Azure-portal
1. In Hallo [portal](https://portal.azure.com/), zoekt Hallo resource u geïnteresseerd bent in de bewaking en selecteert u deze.
2. Deze stap is verschillend voor SQL-database en elastische pools versus SQL DW: 

   - **SQL-database & alleen elastische Pools**: Selecteer **waarschuwingen** of **waarschuwing regels** onder de sectie bewaking Hallo. tekst Hello en pictogram kunnen enigszins verschillen voor verschillende resources.  
   
     ![Bewaking](../monitoring-and-diagnostics/media/insights-alerts-portal/AlertRulesButton.png)
  
   - **SQL DW alleen**: Selecteer **bewaking** onder Hallo sectie Algemene taken. Klik op Hallo **DWU gebruik** grafiek.

     ![ALGEMENE TAKEN](../monitoring-and-diagnostics/media/insights-alerts-portal/AlertRulesButtonDW.png)

3. Selecteer Hallo **waarschuwing toevoegen** opdracht en Hallo invullen.
   
    ![Waarschuwing toevoegen](../monitoring-and-diagnostics/media/insights-alerts-portal/AddDBAlertPage.png)
4. **Naam** uw Waarschuwing regel en kies een **beschrijving**, die ook weergegeven in e-mailmeldingen.
5. Selecteer Hallo **metriek** u wilt dat toomonitor en kies vervolgens een **voorwaarde** en **drempelwaarde** waarde voor metriek Hallo. Hallo hebt gekozen **periode** hoelang Hallo metriek regel moet worden voldaan voordat de waarschuwing Hallo-triggers. Dus bijvoorbeeld, als u Hallo periode 'PT5M' en de waarschuwing CPU dan 80 zoekt %, Hallo waarschuwing wordt geactiveerd wanneer Hallo CPU is al consistent bovenstaande 80% 5 minuten. Zodra de eerste trigger Hallo plaatsvindt, deze opnieuw wordt geactiveerd wanneer Hallo CPU onder 80% gedurende vijf minuten blijft. Hallo meting van CPU doet zich voor elke 1 minuut.   
6. Controleer **e-eigenaars...**  als u wilt dat beheerders en medebeheerders toobe per e-mail verzonden wanneer Hallo waarschuwing wordt geactiveerd.
7. Als u aanvullende e-mailberichten tooreceive een melding wanneer hello wilt waarschuwing wordt geactiveerd, toe te voegen in Hallo **aanvullende beheerder email(s)** veld. Scheid meerdere e-mailberichten met puntkomma's -  *email@contoso.com;email2@contoso.com*
8. In een geldige URI in Hallo plaatsen **Webhook** veld als u wilt dat deze wordt aangeroepen wanneer Hallo waarschuwing wordt geactiveerd.
9. Selecteer **OK** wanneer gereed toocreate Hallo waarschuwing.   

Binnen een paar minuten Hallo waarschuwing actief is en wordt geactiveerd als eerder beschreven.

## <a name="managing-your-alerts"></a>Uw waarschuwingen beheren
Wanneer u een waarschuwing hebt gemaakt, kunt u deze selecteren en:

* Een grafiek weer met Hallo metrische drempel en de werkelijke waarden van Hallo Hallo vorige dag weergeven.
* Bewerk of verwijder deze.
* **Schakel** of **inschakelen** als u wilt dat tootemporarily stoppen of te hervatten ontvangen van meldingen voor deze waarschuwing.


## <a name="sql-database-alert-values"></a>Waarschuwing waarden SQL-Database

| Resourcetype | Metrische naam | Beschrijvende naam | Samenvoegingstype | Minimale waarschuwing tijdvenster|
| --- | --- | --- | --- | --- |
| SQL-database | cpu_percent | CPU-percentage | Gemiddelde | 5 minuten |
| SQL-database | physical_data_read_percent | Gegevens-I/O-percentage | Gemiddelde | 5 minuten |
| SQL-database | log_write_percent | Percentage van logboek-i/o | Gemiddelde | 5 minuten |
| SQL-database | dtu_consumption_percent | DTU-percentage | Gemiddelde | 5 minuten |
| SQL-database | Opslag | Totale grootte | Maximum | 30 minuten |
| SQL-database | connection_successful | Geslaagde verbindingen | Totaal | 10 minuten |
| SQL-database | connection_failed | Mislukte verbindingen | Totaal | 10 minuten |
| SQL-database | blocked_by_firewall | Geblokkeerd door een Firewall | Totaal | 10 minuten |
| SQL-database | impasse | Impassen | Totaal | 10 minuten |
| SQL-database | storage_percent | Databaseomvangpercentage | Maximum | 30 minuten |
| SQL-database | xtp_storage_percent | In het geheugen OLTP opslag percent(Preview) | Gemiddelde | 5 minuten |
| SQL-database | workers_percent | Percentage van de werknemers | Gemiddelde | 5 minuten |
| SQL-database | sessions_percent | Percentage van sessies | Gemiddelde | 5 minuten |
| SQL-database | dtu_limit | DTU limiet | Gemiddelde | 5 minuten |
| SQL-database | dtu_used | DTU gebruikt | Gemiddelde | 5 minuten |
||||||
| Elastische pool | cpu_percent | CPU-percentage | Gemiddelde | 10 minuten |
| Elastische pool | physical_data_read_percent | Gegevens-I/O-percentage | Gemiddelde | 10 minuten |
| Elastische pool | log_write_percent | Percentage van logboek-i/o | Gemiddelde | 10 minuten |
| Elastische pool | dtu_consumption_percent | DTU-percentage | Gemiddelde | 10 minuten |
| Elastische pool | storage_percent | Opslagpercentage | Gemiddelde | 10 minuten |
| Elastische pool | workers_percent | Percentage van de werknemers | Gemiddelde | 10 minuten |
| Elastische pool | eDTU_limit | limiet voor eDTU | Gemiddelde | 10 minuten |
| Elastische pool | storage_limit | Opslaglimiet bereikt | Gemiddelde | 10 minuten |
| Elastische pool | eDTU_used | eDTU gebruikt | Gemiddelde | 10 minuten |
| Elastische pool | storage_used | Gebruikte opslag | Gemiddelde | 10 minuten |
||||||               
| SQL-datawarehouse | cpu_percent | CPU-percentage | Gemiddelde | 10 minuten |
| SQL-datawarehouse | physical_data_read_percent | Gegevens-I/O-percentage | Gemiddelde | 10 minuten |
| SQL-datawarehouse | Opslag | Totale grootte | Maximum | 10 minuten |
| SQL-datawarehouse | connection_successful | Geslaagde verbindingen | Totaal | 10 minuten |
| SQL-datawarehouse | connection_failed | Mislukte verbindingen | Totaal | 10 minuten |
| SQL-datawarehouse | blocked_by_firewall | Geblokkeerd door een Firewall | Totaal | 10 minuten |
| SQL-datawarehouse | service_level_objective | Serviceniveaudoelstelling van Hallo-database | Totaal | 10 minuten |
| SQL-datawarehouse | dwu_limit | dwu-limiet | Maximum | 10 minuten |
| SQL-datawarehouse | dwu_consumption_percent | DWU-percentage | Gemiddelde | 10 minuten |
| SQL-datawarehouse | dwu_used | DWU gebruikt | Gemiddelde | 10 minuten |
||||||


## <a name="next-steps"></a>Volgende stappen
* [Een overzicht van Azure monitoring](../monitoring-and-diagnostics/monitoring-overview.md) inclusief Hallo typen gegevens u kunt verzamelen en controleren.
* Meer informatie over [configureren van webhooks in waarschuwingen](../monitoring-and-diagnostics/insights-webhooks-alerts.md).
* Ophalen van een [overzicht van diagnostische logboeken](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) en gedetailleerde hoge frequentie metrische gegevens verzamelen over uw service.
* Ophalen van een [overzicht van metrische gegevens verzameling](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) toomake ervoor dat uw service beschikbaar is en reageert.
