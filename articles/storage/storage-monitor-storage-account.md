---
title: aaaHow toomonitor een Azure Storage-account | Microsoft Docs
description: Meer informatie over hoe een opslagaccount in Azure met behulp van toomonitor hello Azure-portal.
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: b83cba7b-4627-4ba7-b5d0-f1039fe30e78
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: marsma
ms.openlocfilehash: 782873648fdbccc0191a074cd4044f97af8b7c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-storage-account-in-hello-azure-portal"></a>Een opslagaccount in hello Azure-portal bewaken

[Azure Storage Analytics](storage-analytics.md) voorziet in maatstaven voor alle storage-services en logboeken voor blobs, wachtrijen en tabellen. U kunt Hallo [Azure-portal](https://portal.azure.com) tooconfigure welke metrische gegevens en de logboeken worden geregistreerd voor uw account en grafieken die visuele weergaven van de metrische gegevens bieden configureren.

> [!NOTE]
> Er worden kosten in verband met het onderzoeken van bewakingsgegevens in hello Azure-portal. Zie voor meer informatie [Storage Analytics en facturering](/rest/api/storageservices/Storage-Analytics-and-Billing).
>
> Azure File storage momenteel ondersteunt Opslaganalyse metrische gegevens, maar logboekregistratie nog niet ondersteunt.
>
> Storage-accounts met een replicatietype van de Zone-redundante opslag (ZRS) op dit moment geen Hallo metrische gegevens of mogelijkheden voor logboekregistratie.
> 
> Voor een gedetailleerde richtlijnen voor het gebruik van Storage Analytics en andere hulpprogramma's voor tooidentify, diagnose, en problemen met Azure Storage, Zie [Monitor, vaststellen en oplossen van Microsoft Azure Storage](storage-monitoring-diagnosing-troubleshooting.md).
>

## <a name="configure-monitoring-for-a-storage-account"></a>Bewaking configureren voor een opslagaccount

1. In Hallo [Azure-portal](https://portal.azure.com), selecteer **opslagaccounts**, en vervolgens Hallo storage account name tooopen Hallo account dashboard.
1. Selecteer **Diagnostics** in Hallo **bewaking** sectie van Hallo menu blade.

    ![MonitoringOptions](./media/storage-monitor-storage-account/stg-enable-metrics-00.png)

1. Selecteer Hallo **type** van metrische gegevens voor elke **service** u wenst dat toomonitor en Hallo **bewaarbeleid** voor Hallo-gegevens. U kunt ook uitschakelen door in te stellen bewaking **Status** te**uit**.

    ![MonitoringOptions](./media/storage-monitor-storage-account/stg-enable-metrics-01.png)

   Er zijn twee soorten metrische gegevens die kunt u inschakelen voor elke service, die beide zijn standaard ingeschakeld voor nieuwe storage-accounts:

   * **Cumulatieve**: metrische gegevens zoals inkomend en uitgaand, beschikbaarheid, latentie en geslaagd percentages verzamelt. Deze metrische gegevens zijn samengevoegd voor Hallo blob, queue, table en Bestandsservices.
   * **Per API**: In toevoeging toohello cumulatieve metrische gegevens, verzamelt dezelfde set van metrische gegevens voor elke opslagbewerking in Azure Storage-service API Hallo Hallo.

   tooset hello bewaarbeleid voor gegevens, verplaatsen Hallo **bewaartermijn (dagen)** schuifregelaar of Hallo aantal dagen aan gegevens tooretain, van 1 too365 invoeren. Hallo standaardwaarde voor nieuwe storage-accounts is zeven dagen. Als u niet dat een bewaarbeleid tooset wilt, voer dan nul. Als er geen bewaarbeleid, is tooyou toodelete Hallo bewakingsgegevens.

   > [!WARNING]
   > U in rekening worden gebracht wanneer u metrische gegevens voor het handmatig verwijderen. Verouderde analytische gegevens (gegevens die ouder zijn dan het bewaarbeleid) is verwijderd door Hallo systeem zonder kosten. Het is raadzaam om een bewaarbeleid op basis van hoe lang u tooretain storage analytics-gegevens voor uw account wilt instellen. Zie [welke kosten komen er gemaakt bij het inschakelen van metrische gegevens storage?](storage-enable-and-view-metrics.md#what-charges-do-you-incur-when-you-enable-storage-metrics) voor meer informatie.
   >

1. Wanneer u klaar bent met de controleconfiguratie hello, selecteert u **opslaan**.

Een standaardset metrische gegevens wordt weergegeven in de grafieken op de blade opslagaccount hello, evenals Hallo afzonderlijke service blades (blob, queue, table en -bestand). Nadat u metrische gegevens voor een service hebt ingeschakeld, kan het tooappear gegevens in de grafieken tooan uur duren. U kunt selecteren **bewerken** op een metriek grafiek te[configureren welke metrische gegevens](#how-to-customize-metrics-charts) in Hallo diagram worden weergegeven.

U kunt metrische gegevens verzamelen en logboekregistratie uitschakelen door in te stellen **Status** te**uit**.

> [!NOTE]
> Azure Storage maakt gebruik van [tabel opslag](storage-introduction.md#table-storage) toostore Hallo metrische gegevens voor uw opslagaccount en winkels Hallo metrische gegevens in de tabellen in uw account. Zie voor meer informatie. [Hoe metrische gegevens worden opgeslagen](storage-analytics.md#how-metrics-are-stored).
>

## <a name="customize-metrics-charts"></a>Metrische gegevens grafieken aanpassen

Gebruik hello te volgen procedure toochoose welke opslag metrische gegevens tooview in een grafiek metrische gegevens. 

1. Start een metrische grafiek opslag in hello Azure-portal weergegeven. U vindt grafieken op Hallo **blade opslagaccount** en in Hallo **metrische gegevens** blade voor een afzonderlijke service (blob, queue, table, bestand).

   In dit voorbeeld werken we met de volgende grafiek die wordt weergegeven op Hallo Hallo **blade opslagaccount**:

   ![Grafiekselectie in Azure-portal](./media/storage-monitor-storage-account/stg-customize-chart-00.png)

1. Klik vervolgens op een willekeurige plaats in Hallo grafiek tooopen hello **metriek** blade. Selecteer **grafiek bewerken** tooopen hello **grafiek bewerken** blade.

   ![Knop grafiek op de blade grafiek bewerken](./media/storage-monitor-storage-account/stg-customize-chart-01.png)

1. Op Hallo **grafiek bewerken** blade, selecteer Hallo **tijdsbereik** van Hallo metrische gegevens toodisplay in Hallo grafiek en Hallo **service** (blob, queue, tabel, bestand) waarvan metrische gegevens die u wilt toodisplay. Hier geselecteerde we toodisplay Hallo voorbij week van metrische gegevens voor Hallo blob-service:

   ![Bereik en de service Tijdselectie Hallo grafiek bewerken blade](./media/storage-monitor-storage-account/stg-customize-chart-02.png)

1. Selecteer Hallo afzonderlijke **metrische gegevens** u was zoals weergegeven in de grafiek Hallo, klikt u op **OK**. Bijvoorbeeld, hier we hebt gekozen toodisplay hello *ContainerCount* en *ObjectCount* metrische gegevens:

   ![Afzonderlijke metrische selectie in de blade grafiek bewerken](./media/storage-monitor-storage-account/stg-customize-chart-03.png)

De grafiekinstellingen niet invloed hebben op Hallo verzameling, aggregatie of opslag van gegevens in het opslagaccount Hallo bewaking, alleen Hallo weergave van metrische gegevens van.

### <a name="metrics-availability-in-charts"></a>Beschikbaarheid van de metrische gegevens in grafieken

Hallo-lijst met wijzigingen van de beschikbare metrische gegevens op basis van welke service die u hebt gekozen in de vervolgkeuzelijst Hallo en eenheidstype Hallo van Hallo grafiek die u wilt bewerken. Bijvoorbeeld, kunt u percentage metrische gegevens zoals *PercentNetworkError* en *PercentThrottlingError* alleen als u een diagram waarin eenheden percentage bewerkt:

![Aanvraag voor fout percentage grafiek in hello Azure-portal](./media/storage-monitor-storage-account/stg-customize-chart-04.png)

### <a name="metrics-resolution"></a>Omzetting van de metrische gegevens

Hallo metrische gegevens die u hebt geselecteerd in de Diagnostics bepaalt Hallo resolutie van Hallo metrische gegevens die beschikbaar voor uw account zijn:

* **Cumulatieve** voorziet in maatstaven zoals inkomend en uitgaand, beschikbaarheid, latentie en geslaagd percentages voor bewaking. Deze metrische gegevens worden samengevoegd uit Hallo blob, table-bestand en wachtrijservices.
* **Per API** fijner oplossing biedt voor de toohello serviceniveau-statistische functies met metrische gegevens beschikbaar voor afzonderlijke opslagbewerkingen, naast.

## <a name="configure-metrics-alerts"></a>Metrische gegevens waarschuwingen configureren

U kunt waarschuwingen toonotify maken wanneer drempels voor metrische gegevens van storage resource is bereikt.

1. Hallo tooopen **waarschuwingsregels blade**, schuif omlaag toohello **bewaking** sectie Hallo **Menu blade** en selecteer **waarschuwing regels**.
1. Selecteer **waarschuwing toevoegen** tooopen hello **een waarschuwingsregel toevoegen** blade
1. Selecteer een **Resource** (blob, bestand, in de wachtrij, tabel) van Hallo vervolgkeuzelijst en voer een **naam** en **beschrijving** voor uw nieuwe waarschuwingsregel.
1. Selecteer Hallo **metriek** waarvoor u tooadd een waarschuwing een waarschuwing wilt **voorwaarde**, en een **drempelwaarde**. Hallo drempelwaarde eenheid wijzigingen van het type, afhankelijk van Hallo metrische gegevens die u hebt gekozen. Bijvoorbeeld, 'aantal' hello eenheidstype voor is *ContainerCount*, tijdens het Hallo-eenheid voor Hallo *PercentNetworkError* meetwaarde is een percentage.
1. Selecteer Hallo **periode**. Metrische gegevens die bereikt of overschrijdt Hallo drempelwaarde binnen Hallo periode trigger een waarschuwing.
1. (Optioneel) Configureer **e** en **Webhook** meldingen. Zie voor meer informatie over webhooks [een webhook configureren op een Azure metrische waarschuwing](../monitoring-and-diagnostics/insights-webhooks-alerts.md). Als u e-mailadres of webhook meldingen niet configureert, wordt alleen in hello Azure-portal waarschuwingen weergegeven.

![Blade 'Een waarschuwingsregel toevoegen' in hello Azure-portal](./media/storage-monitor-storage-account/stg-alert-rules-01.png)

## <a name="add-metrics-charts-toohello-portal-dashboard"></a>Metrische gegevens grafieken toohello portaldashboard toevoegen

U kunt grafieken van Azure Storage metrische gegevens toevoegen voor een van uw storage-accounts tooyour-portaldashboard.

1. Selecteer Klik **bewerken dashboard** tijdens het bekijken van het dashboard in Hallo [Azure-portal](https://portal.azure.com).
1. In Hallo **tegel galerie**, selecteer **zoeken door tegels** > **Type**.
1. Selecteer **Type** > **opslagaccounts**.
1. In **Resources**, selecteert u het opslagaccount Hallo waarvan metrische gegevens die u wenst dat tooadd toohello dashboard.
1. Selecteer **categorieën** > **bewaking**.
1. Diagram van slepen en neerzetten Hallo tegel op uw dashboard voor Hallo metriek gewenst weergegeven. Herhaal van alle metrische gegevens die u wilt weergegeven op het Hallo-dashboard. In Hallo installatiekopie te volgen, Hallo 'BLOB's - totale aanvragen' grafiek is gemarkeerd als voorbeeld, maar alle Hallo grafieken zijn beschikbaar voor plaatsing op uw dashboard.

   ![Tegel galerie in Azure-portal](./media/storage-monitor-storage-account/stg-customize-dashboard-01.png)
1. Selecteer **gedaan aanpassen** aan de bovenkant Hallo van Hallo dashboard wanneer u grafieken toe te voegen bent klaar.

Zodra u grafieken tooyour dashboard hebt toegevoegd, kunt u verder deze aanpassen zoals beschreven in [grafieken van de metrische gegevens aanpassen](#how-to-customize-metrics-charts).

## <a name="configure-logging"></a>Logboekregistratie configureren

U kunt opgeven dat Azure Storage toosave diagnostische logboeken voor lezen, schrijven en verwijderen van aanvragen voor Hallo blob, table en queue-services. Hallo bewaarbeleid voor gegevens u geldt ook toothese Logboeken.

> [!NOTE]
> Azure File storage momenteel ondersteunt Opslaganalyse metrische gegevens, maar logboekregistratie nog niet ondersteunt.
>

1. In Hallo [Azure-portal](https://portal.azure.com), selecteer **opslagaccounts**, en vervolgens de naam Hallo van Hallo storage account tooopen Hallo blade opslagaccount.
1. Selecteer **Diagnostics** in Hallo **bewaking** sectie van Hallo menu blade.

    ![Diagnostische gegevens menu-item onder controle in hello Azure-portal.](./media/storage-monitor-storage-account/stg-enable-metrics-00.png)
    
1. Zorg ervoor dat **Status** te is ingesteld,**op**, en selecteer Hallo **services** waarvoor u tooenable logboekregistratie wilt.

    ![Logboekregistratie in hello Azure-portal configureren.](./media/storage-monitor-storage-account/stg-enable-logging-01.png)
1. Klik op **Opslaan**.

Hallo diagnostische logboeken worden opgeslagen in een blob-container met de naam $logs in uw opslagaccount. U kunt weergeven Hallo logboekgegevens met een Opslagverkenner zoals Hallo [Microsoft Opslagverkenner](http://storageexplorer.com), of programmatisch met behulp van de storage-clientbibliotheek Hallo of PowerShell.

Zie voor meer informatie over het openen van de container Hallo $logs [opslag vastleggen inschakelen en toegang tot logboekgegevens](/rest/api/storageservices/enabling-storage-logging-and-accessing-log-data).

## <a name="next-steps"></a>Volgende stappen

* Meer informatie vinden over [metrische gegevens en de registratie en facturering](storage-analytics.md) voor Storage Analytics.
* [Inschakelen van Azure Storage metrische gegevens en bekijk metrische gegevens](storage-enable-and-view-metrics.md) met behulp van PowerShell en programmatisch met C#.
