---
title: Azure SQL Analytics-oplossing in Log Analytics | Microsoft Docs
description: De Azure SQL Analytics-oplossing kunt u uw Azure SQL-databases beheren.
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: b2712749-1ded-40c4-b211-abc51cc65171
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: banders
ms.openlocfilehash: cab45cc6dd621eb4a95ef5f1842ec38c25e980b6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="monitor-azure-sql-database-using-azure-sql-analytics-preview-in-log-analytics"></a>Azure SQL Database met behulp van Azure SQL Analytics (Preview) in logboekanalyse bewaken

![Azure SQL Analytics symbool](./media/log-analytics-azure-sql/azure-sql-symbol.png)

De Azure SQL Analytics-oplossing in Azure-logboekanalyse verzamelt en visualiseren van belangrijke maatstaven voor prestaties van SQL Azure. Met behulp van de metrische gegevens die u verzamelt van de oplossing, kunt u aangepaste regels voor bewaking en waarschuwingen. U kunt Azure SQL Database bewaken en elastische pool metrische gegevens op meerdere Azure-abonnementen en elastische pools en ze visualiseren. De oplossing helpt u problemen bij elke laag van uw toepassing stack kunt identificeren.  Hierbij [diagnostische Azure metrische gegevens](log-analytics-azure-storage.md) samen met logboekanalyse weergaven om gegevens over uw Azure SQL-databases en elastische pools in een enkel Log Analytics-werkruimte te presenteren.

Deze preview-oplossing ondersteunt momenteel maximaal 150.000 Azure SQL-Databases en 5000 SQL elastische Pools per werkruimte.

De Azure SQL Analytics-oplossing, net zoals andere beschikbaar voor logboekanalyse, kunt u controleren en meldingen ontvangen over de status van uw Azure-resources: in dit geval, Azure SQL Database. Microsoft Azure SQL Database is een schaalbare relationele database-service die bekende SQL-Server-achtige mogelijkheden voor toepassingen die worden uitgevoerd in de Azure-cloud biedt. Log Analytics, helpt u bij het verzamelen, correleren en gestructureerde en ongestructureerde gegevens visualiseren.

## <a name="connected-sources"></a>Verbonden bronnen

De Azure SQL Analytics-oplossing gebruikt niet agents verbinding maken met de Log Analytics-service.

De volgende tabel beschrijft de verbonden bronnen die worden ondersteund door deze oplossing.

| Verbonden bron | Ondersteuning | Beschrijving |
| --- | --- | --- |
| [Windows-agents](log-analytics-windows-agents.md) | Nee | Directe Windows-agents worden niet gebruikt door de oplossing. |
| [Linux-agents](log-analytics-linux-agents.md) | Nee | Directe Linux-agents worden niet gebruikt door de oplossing. |
| [SCOM-beheergroep](log-analytics-om-agents.md) | Nee | Een rechtstreekse verbinding tussen de SCOM-agents met logboekanalyse wordt niet gebruikt door de oplossing. |
| [Azure Storage-account](log-analytics-azure-storage.md) | Nee | Log Analytics biedt de gegevens niet lezen uit een opslagaccount. |
| [Azure diagnostics](log-analytics-azure-storage.md) | Ja | Azure metrische gegevens worden verzonden met logboekanalyse rechtstreeks door Azure. |

## <a name="prerequisites"></a>Vereisten

- Een Azure-abonnement. Als u niet hebt, kunt u één voor [gratis](https://azure.microsoft.com/free/).
- Een werkruimte voor logboekanalyse. U kunt een bestaande of kunt u [Maak een nieuwe](log-analytics-get-started.md) voordat u begint met behulp van deze oplossing.
- Azure Diagnostics inschakelen voor uw Azure SQL-databases en elastische pools en [configureren zodat ze hun gegevens verzenden naar logboekanalyse](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).

## <a name="configuration"></a>Configuratie

Voer de volgende stappen uit om toe te voegen van de Azure SQL Analytics-oplossing naar de werkruimte.

1. De Azure SQL Analytics-oplossing toevoegen aan uw werkruimte van [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview) of met behulp van de procedure beschreven in [toevoegen Log Analytics-oplossingen van de galerie met oplossingen](log-analytics-add-solutions.md).
2. Klik in de Azure-portal op **nieuw** (het symbool +), selecteer vervolgens in de lijst met resources **bewaking + Management**.  
    ![Controle en beheer](./media/log-analytics-azure-sql/monitoring-management.png)
3. In de **bewaking + Management** Klik **alle**.
4. In de **aanbevolen** lijst, klikt u op **meer** , en klik vervolgens in de nieuwe lijst vinden **Azure SQL Analytics (Preview)** en selecteert u vervolgens.  
    ![Azure SQL Analytics-oplossing](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)
5. In de **Azure SQL Analytics (Preview)** blade, klikt u op **maken**.  
    ![Maken](./media/log-analytics-azure-sql/portal-create.png)
6. In de **nieuwe oplossing maken** blade, selecteer de werkruimte die u wilt toevoegen, de oplossing en klik vervolgens op **maken**.  
    ![toevoegen aan werkruimte](./media/log-analytics-azure-sql/add-to-workspace.png)


### <a name="to-configure-multiple-azure-subscriptions"></a>Voor het configureren van meerdere Azure-abonnementen

Gebruik de PowerShell-script uit ter ondersteuning van meerdere abonnementen [inschakelen Azure resource metrische gegevens logboekregistratie met behulp van PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/). Geef de werkruimte-ID als parameter bij het uitvoeren van het script voor het verzenden van diagnostische gegevens van resources in een Azure-abonnement met een werkruimte in een andere Azure-abonnement.

**Voorbeeld**

```
PS C:\> $WSID = "/subscriptions/<subID>/resourcegroups/oms/providers/microsoft.operationalinsights/workspaces/omsws"
```

```
PS C:\> .\Enable-AzureRMDiagnostics.ps1 -WSID $WSID
```

## <a name="using-the-solution"></a>De oplossing gebruiken

Wanneer u de oplossing voor uw werkruimte toevoegt, is de tegel Azure SQL Analytics toegevoegd aan uw werkruimte en wordt deze weergegeven in het overzicht. De tegel toont het aantal Azure SQL-databases en elastische pools SQL Azure die de oplossing is verbonden met.

![Azure SQL-Analytics tegel](./media/log-analytics-azure-sql/azure-sql-sol-tile.png)

### <a name="viewing-azure-sql-analytics-data"></a>Azure SQL analytische gegevens weergeven

Klik op de **Azure SQL Analytics** tegel om de Azure SQL Analytics dashboard te openen. Het dashboard bevat de blades zoals hieronder gedefinieerd. Elke blade bevat maximaal 15 bronnen (abonnement, server elastische pool en database). Klik op de bronnen om het dashboard voor die specifieke bron te openen. Elastische Pool of Database bevat de grafieken met metrische gegevens voor een geselecteerde bron. Klik op een grafiek om te openen van het dialoogvenster logboek zoeken.

| Blade | Beschrijving |
|---|---|
| Abonnementen | Lijst met abonnementen met het aantal gekoppelde servers, -adresgroepen en -databases. |
| Servers | Lijst met servers met een aantal van de verbonden groepen en databases. |
| Elastische pools | Lijst met verbonden elastische pools met maximale GB en eDTU in de gecontroleerde periode. |
|Databases | Lijst met verbonden databases met een maximale GB en DTU in de gecontroleerde periode.|


### <a name="analyze-data-and-create-alerts"></a>Gegevens analyseren en waarschuwingen maken

U kunt eenvoudig waarschuwingen maken met de gegevens die afkomstig zijn van Azure SQL Database-resources. Hier volgen enkele nuttige [logboek zoeken](log-analytics-log-searches.md) query's die u voor waarschuwingen gebruiken kunt:

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]


*Hoge DTU voor Azure SQL Database*

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/DATABASES/"* MetricName=dtu_consumption_percent | measure Avg(Average) by Resource interval 5minutes
```

*Hoge DTU op elastische Pool in Azure SQL Database*

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource interval 5minutes
```

U kunt deze waarschuwing-query's gebruiken om te attenderen op specifieke drempelwaarden voor Azure SQL Database en elastische pools. Voor het configureren van een waarschuwing voor de OMS-werkruimte:

#### <a name="to-configure-an-alert-for-your-workspace"></a>Een waarschuwing voor uw werkruimte configureren

1. Ga naar de [OMS-portal](http://mms.microsoft.com/) en meld u aan.
2. Open de werkruimte die u hebt geconfigureerd voor de oplossing.
3. Klik op de pagina overzicht de **Azure SQL Analytics (Preview)** tegel.
4. Voer een van de voorbeelden van query's.
5. In logboek zoekopdracht, klikt u op **waarschuwing**.  
![waarschuwing in de zoekopdracht maken](./media/log-analytics-azure-sql/create-alert01.png)
6. Op de **waarschuwingsregel toevoegen** pagina, configureert de toepasselijke eigenschappen en de specifieke drempelwaarden die u wilt en klik vervolgens op **opslaan**.  
![toevoegen van waarschuwingsregel](./media/log-analytics-azure-sql/create-alert02.png)

### <a name="act-on-azure-sql-analytics-data"></a>Reageren op Azure SQL analytische gegevens

Een van de handigste query's die u kunt uitvoeren is bijvoorbeeld het DTU-gebruik voor alle Azure SQL elastische Pools van alle Azure-abonnement met elkaar vergelijken. Doorvoer DTU (database Unit) biedt een manier om te beschrijven de relatieve capaciteit van een prestatieniveau van Basic, Standard en Premium-databases en pools. Dtu's zijn gebaseerd op een gecombineerde meting van CPU, geheugen, leest en schrijft. Als het aantal dtu's verhoogt, verhoogt de macht die worden aangeboden door het prestatieniveau. Bijvoorbeeld, heeft een prestatieniveau met 5 dtu's vijf keer krachtiger dan een prestatieniveau met 1 DTU. Maximale DTU-quotum geldt voor elke server en de elastische groep.

Door de volgende logboek-zoekopdracht wordt uitgevoerd, kunt u eenvoudig zien als u bepaalde zijn of over het gebruik van uw SQL Azure elastische pools.

```
Type=AzureMetrics ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource | display LineChart
```

>[!NOTE]
> Als uw werkruimte is bijgewerkt naar de [nieuwe logboekanalyse querytaal](log-analytics-log-search-upgrade.md), en vervolgens de bovenstaande query zou Wijzig in het volgende.
>
>`search in (AzureMetrics) isnotempty(ResourceId) and "/ELASTICPOOLS/" and MetricName == "dtu_consumption_percent" | summarize AggregatedValue = avg(Average) by bin(TimeGenerated, 1h), Resource | render timechart`

In het volgende voorbeeld ziet u dat een elastische groep een hoog gebruik in de buurt van 100 heeft % DTU weinig gebruik zijn. U kunt verder onderzoeken om op te lossen potentiële recente wijzigingen in uw omgeving met Logboeken van de Azure-activiteit.

![Zoekresultaten voor logboek - hoog gebruik](./media/log-analytics-azure-sql/log-search-high-util.png)

## <a name="see-also"></a>Zie ook

- Gebruik [logboek zoekopdrachten](log-analytics-log-searches.md) in Log Analytics om gedetailleerde Azure SQL-gegevens te bekijken.
- [Maak uw eigen dashboards](log-analytics-dashboards.md) Azure SQL-gegevens worden weergegeven.
- [Waarschuwingen maken](log-analytics-alerts.md) wanneer specifieke Azure SQL-gebeurtenissen plaatsvinden.
