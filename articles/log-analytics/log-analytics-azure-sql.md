---
title: aaaAzure SQL Analytics-oplossing in Log Analytics | Microsoft Docs
description: Hello Azure SQL Analytics-oplossing kunt u uw Azure SQL-databases beheren.
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
ms.openlocfilehash: fe228bb3cb3f9d578a84707c3917f02fbeb8a627
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-sql-database-using-azure-sql-analytics-preview-in-log-analytics"></a>Azure SQL Database met behulp van Azure SQL Analytics (Preview) in logboekanalyse bewaken

![Azure SQL Analytics symbool](./media/log-analytics-azure-sql/azure-sql-symbol.png)

Hello Azure SQL Analytics-oplossing in Azure-logboekanalyse verzamelt en visualiseren van belangrijke maatstaven voor prestaties van SQL Azure. Hallo metrische gegevens die u verzamelt met Hallo oplossing gebruikt, kunt u aangepaste regels voor bewaking en waarschuwingen. U kunt Azure SQL Database bewaken en elastische pool metrische gegevens op meerdere Azure-abonnementen en elastische pools en ze visualiseren. Hallo-oplossing kunt u ook tooidentify problemen bij elke laag van de stack van uw toepassing.  Hierbij [diagnostische Azure metrische gegevens](log-analytics-azure-storage.md) samen met logboekanalyse toopresent gegevens over uw Azure SQL-databases en elastische pools-weergaven in een enkel werkruimte voor logboekanalyse.

Deze preview-oplossing ondersteunt momenteel tot too150, 000 Azure SQL-Databases en 5000 SQL elastische Pools per werkruimte.

Hello Azure SQL Analytics-oplossing, net zoals andere beschikbaar voor logboekanalyse, kunt u controleren en meldingen ontvangen over Hallo status van uw Azure-resources: in dit geval, Azure SQL Database. Microsoft Azure SQL Database is een schaalbare relationele database-service waarmee bekende SQL-Server-achtige mogelijkheden tooapplications uitgevoerd in hello Azure-cloud. Log Analytics kunt u toocollect, correleren en gestructureerde en ongestructureerde gegevens visualiseren.

## <a name="connected-sources"></a>Verbonden bronnen

Hello Azure SQL Analytics-oplossing gebruik geen maakt van agents tooconnect toohello Log Analytics-service.

Hallo volgende tabel beschrijft Hallo verbonden gegevensbronnen die worden ondersteund door deze oplossing.

| Verbonden bron | Ondersteuning | Beschrijving |
| --- | --- | --- |
| [Windows-agents](log-analytics-windows-agents.md) | Nee | Directe Windows-agents worden niet gebruikt door Hallo-oplossing. |
| [Linux-agents](log-analytics-linux-agents.md) | Nee | Directe Linux-agents worden niet gebruikt door Hallo-oplossing. |
| [SCOM-beheergroep](log-analytics-om-agents.md) | Nee | Een rechtstreekse verbinding tussen Hallo SCOM agent tooLog Analytics wordt niet gebruikt door Hallo-oplossing. |
| [Azure Storage-account](log-analytics-azure-storage.md) | Nee | Log Analytics biedt Hallo gegevens niet lezen uit een opslagaccount. |
| [Azure diagnostics](log-analytics-azure-storage.md) | Ja | Azure metrische gegevens verzonden tooLog Analytics rechtstreeks door Azure. |

## <a name="prerequisites"></a>Vereisten

- Een Azure-abonnement. Als u niet hebt, kunt u één voor [gratis](https://azure.microsoft.com/free/).
- Een werkruimte voor logboekanalyse. U kunt een bestaande of kunt u [Maak een nieuwe](log-analytics-get-started.md) voordat u begint met behulp van deze oplossing.
- Azure Diagnostics inschakelen voor uw Azure SQL-databases en elastische pools en [configureren zodat deze toosend hun gegevens tooLog Analytics](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).

## <a name="configuration"></a>Configuratie

Volgende stappen tooadd hello Azure SQL Analytics-oplossing tooyour werkruimte Hallo uitvoeren.

1. Hello Azure SQL Analytics-oplossing tooyour werkruimte van toevoegen [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview) of met behulp van Hallo procedure beschreven in [toevoegen Log Analytics-oplossingen van Hallo galerie met oplossingen](log-analytics-add-solutions.md).
2. In hello Azure-portal, klikt u op **nieuw** (Hallo + symbool), selecteer vervolgens in lijst met resources Hallo **bewaking + Management**.  
    ![Controle en beheer](./media/log-analytics-azure-sql/monitoring-management.png)
3. In Hallo **bewaking + Management** Klik **alle**.
4. In Hallo **aanbevolen** lijst, klikt u op **meer** , en zoekt u in de nieuwe lijst Hallo **Azure SQL Analytics (Preview)** en selecteert u vervolgens.  
    ![Azure SQL Analytics-oplossing](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)
5. In Hallo **Azure SQL Analytics (Preview)** blade, klikt u op **maken**.  
    ![Maken](./media/log-analytics-azure-sql/portal-create.png)
6. In Hallo **nieuwe oplossing maken** blade, selecteer Hallo werkruimte dat u wilt dat tooadd Hallo oplossing tooand en klik vervolgens op **maken**.  
    ![tooworkspace toevoegen](./media/log-analytics-azure-sql/add-to-workspace.png)


### <a name="tooconfigure-multiple-azure-subscriptions"></a>tooconfigure meerdere Azure-abonnementen

toosupport meerdere abonnementen gebruiken Hallo PowerShell-script uit [inschakelen Azure resource metrische gegevens logboekregistratie met behulp van PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/). Hallo werkruimte resource-ID opgeven als parameter bij het uitvoeren van Hallo script toosend diagnostische gegevens van resources in één Azure-abonnement tooa werkruimte in een andere Azure-abonnement.

**Voorbeeld**

```
PS C:\> $WSID = "/subscriptions/<subID>/resourcegroups/oms/providers/microsoft.operationalinsights/workspaces/omsws"
```

```
PS C:\> .\Enable-AzureRMDiagnostics.ps1 -WSID $WSID
```

## <a name="using-hello-solution"></a>Met behulp van Hallo-oplossing

Wanneer u Hallo oplossing tooyour werkruimte toevoegt, hello Azure SQL Analytics tegel tooyour werkruimte is toegevoegd en wordt deze weergegeven in het overzicht. Hallo-tegel toont Hallo aantal Azure SQL-databases en elastische pools Azure SQL die Hallo-oplossing is verbonden met.

![Azure SQL-Analytics tegel](./media/log-analytics-azure-sql/azure-sql-sol-tile.png)

### <a name="viewing-azure-sql-analytics-data"></a>Azure SQL analytische gegevens weergeven

Klik op Hallo **Azure SQL Analytics** tegel tooopen hello Azure SQL Analytics dashboard. Hallo dashboard bevat Hallo blades zoals hieronder gedefinieerd. Elke blade bevat too15 resources (abonnement, server elastische pool en database). Klik op een Hallo resources tooopen Hallo dashboard voor die specifieke bron. Elastische Pool of Database bevat Hallo grafieken met metrische gegevens voor een geselecteerde bron. Klik op een grafiek tooopen Hallo logboek zoeken dialoogvenster.

| Blade | Beschrijving |
|---|---|
| Abonnementen | Lijst met abonnementen met het aantal gekoppelde servers, -adresgroepen en -databases. |
| Servers | Lijst met servers met een aantal van de verbonden groepen en databases. |
| Elastische pools | Lijst met verbonden elastische pools met maximale GB en eDTU in Hallo waargenomen periode. |
|Databases | Lijst van de gekoppelde databases met maximale GB en DTU op Hallo waargenomen periode.|


### <a name="analyze-data-and-create-alerts"></a>Gegevens analyseren en waarschuwingen maken

U kunt eenvoudig waarschuwingen maken met de Hallo-gegevens die afkomstig zijn uit Azure SQL Database-resources. Hier volgen enkele nuttige [logboek zoeken](log-analytics-log-searches.md) query's die u voor waarschuwingen gebruiken kunt:

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]


*Hoge DTU voor Azure SQL Database*

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/DATABASES/"* MetricName=dtu_consumption_percent | measure Avg(Average) by Resource interval 5minutes
```

*Hoge DTU op elastische Pool in Azure SQL Database*

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource interval 5minutes
```

U kunt deze tooalert waarschuwing-query's op specifieke drempelwaarden voor Azure SQL Database en elastische pools. tooconfigure een waarschuwing voor de OMS-werkruimte:

#### <a name="tooconfigure-an-alert-for-your-workspace"></a>een waarschuwing voor uw werkruimte tooconfigure

1. Ga toohello [OMS-portal](http://mms.microsoft.com/) en meld u aan.
2. Hallo-werkruimte die u hebt geconfigureerd voor Hallo oplossing worden geopend.
3. Klik op de overzichtspagina Hallo Hallo **Azure SQL Analytics (Preview)** tegel.
4. Voer een van de Hallo voorbeelden van query's.
5. In logboek zoekopdracht, klikt u op **waarschuwing**.  
![waarschuwing in de zoekopdracht maken](./media/log-analytics-azure-sql/create-alert01.png)
6. Op Hallo **waarschuwingsregel toevoegen** pagina, Hallo toepasselijke eigenschappen configureren en specifieke drempelwaarden die u wilt en klik vervolgens op Hallo **opslaan**.  
![toevoegen van waarschuwingsregel](./media/log-analytics-azure-sql/create-alert02.png)

### <a name="act-on-azure-sql-analytics-data"></a>Reageren op Azure SQL analytische gegevens

Als u bijvoorbeeld is een van Hallo nuttigst-query's die u kunt uitvoeren toocompare hello DTU-gebruik voor alle Azure SQL elastische Pools voor uw Azure abonnementen. Doorvoer DTU (database Unit) biedt een manier toodescribe Hallo relatieve capaciteit van een prestatieniveau van Basic, Standard en Premium-databases en pools. Dtu's zijn gebaseerd op een gecombineerde meting van CPU, geheugen, leest en schrijft. Als het aantal dtu's verhogen Hallo power die worden aangeboden door Hallo prestaties wordt verhoogd. Bijvoorbeeld, heeft een prestatieniveau met 5 dtu's vijf keer krachtiger dan een prestatieniveau met 1 DTU. Maximale DTU-quotum geldt tooeach server en de elastische pool.

Hallo na logboek zoekopdracht uitvoert, kunt u eenvoudig zien als u bepaalde of meer dan het gebruik van uw SQL Azure elastische pools.

```
Type=AzureMetrics ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource | display LineChart
```

>[!NOTE]
> Als uw werkruimte bijgewerkte toohello is [nieuwe logboekanalyse querytaal](log-analytics-log-search-upgrade.md), Hallo hierboven query zou Wijzig toohello volgende.
>
>`search in (AzureMetrics) isnotempty(ResourceId) and "/ELASTICPOOLS/" and MetricName == "dtu_consumption_percent" | summarize AggregatedValue = avg(Average) by bin(TimeGenerated, 1h), Resource | render timechart`

In de Hallo voorbeeld te volgen, kunt u zien dat een elastische groep een hoog gebruik in de buurt van 100 heeft % DTU weinig gebruik zijn. Verdere tootroubleshoot potentiële recente wijzigingen kunt u onderzoeken in uw omgeving met Logboeken van de Azure-activiteit.

![Zoekresultaten voor logboek - hoog gebruik](./media/log-analytics-azure-sql/log-search-high-util.png)

## <a name="see-also"></a>Zie ook

- Gebruik [logboek zoekopdrachten](log-analytics-log-searches.md) in logboekanalyse tooview gedetailleerde Azure SQL-gegevens.
- [Maak uw eigen dashboards](log-analytics-dashboards.md) Azure SQL-gegevens worden weergegeven.
- [Waarschuwingen maken](log-analytics-alerts.md) wanneer specifieke Azure SQL-gebeurtenissen plaatsvinden.
