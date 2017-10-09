---
title: aaaMonitor bewerkingen, gebeurtenissen en prestatiemeteritems voor de Load Balancer | Microsoft Docs
description: Meer informatie over hoe tooenable waarschuwing gebeurtenissen en registratie van de health-status voor Azure Load Balancer-test
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 56656d74-0241-4096-88c8-aa88515d676d
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: ac53c2254e06cad780ad6144c5c30f0085d12576
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-for-azure-load-balancer"></a>Logboekanalyse voor Azure Load Balancer

U kunt verschillende typen Logboeken gebruiken in Azure toomanage en netwerktaakverdelers oplossen. Sommige van deze logboeken zijn toegankelijk via Hallo-portal. Alle logboeken kunnen worden opgehaald uit Azure blob-opslag en worden bekeken in verschillende hulpprogramma's zoals Excel en Power BI. U kunt meer informatie over Hallo verschillende typen logboeken in Hallo onderstaande lijst.

* **Controlelogboeken:** kunt u [Azure controlelogboeken](../monitoring-and-diagnostics/insights-debugging-with-events.md) (voorheen bekend als operationele Logboeken) tooview alle bewerkingen worden verzonden tooyour Azure-abonnementen en hun status. Controlelogboeken zijn standaard ingeschakeld en kunnen worden bekeken in hello Azure-portal.
* **Waarschuwing van gebeurtenislogboeken:** kunt u dit logboek tooview waarschuwingen rasied door Hallo load balancer. Hallo-status voor Hallo load balancer worden verzameld om de vijf minuten. Dit logboek wordt alleen geschreven als een load balancer waarschuwing gebeurtenis treedt op.
* **Health test Logboeken:** kunt u dit logboek tooview problemen die door uw health test, zoals het aantal exemplaren in uw back-end-pool die aanvragen vanwege health test problemen niet van Hallo load balancer ontvangen Hallo gedetecteerd. Dit logboek wordt geschreven toowhen Hallo health test status is gewijzigd.

> [!IMPORTANT]
> Meld u analytics momenteel werkt alleen voor Internet gerichte load balancers. Logboeken zijn alleen beschikbaar voor resources geïmplementeerd in Hallo Resource Manager-implementatiemodel. U kunt Logboeken niet gebruiken voor bronnen in het klassieke implementatiemodel Hallo. Zie voor meer informatie over de implementatiemodellen Hallo [Understanding Resource Manager-implementatie en klassieke implementatie](../azure-resource-manager/resource-manager-deployment-model.md).

## <a name="enable-logging"></a>Logboekregistratie inschakelen

Logboekregistratie is automatisch ingeschakeld voor elke Resource Manager-resource. U moet tooenable gebeurtenis en health test logboekregistratie toostart Hallo gegevens beschikbaar zijn via deze logboeken worden verzameld. Volgende stappen tooenable logboekregistratie hello gebruiken.

Aanmelden toohello [Azure-portal](http://portal.azure.com). Als u een load balancer, nog niet hebt [maken van een load balancer](load-balancer-get-started-internet-arm-ps.md) voordat u doorgaat.

1. Klik in de portal Hallo op **Bladeren**.
2. Selecteer **Taakverdelers**.

    ![Portal - load balancer](./media/load-balancer-monitor-log/load-balancer-browse.png)

3. Selecteer een bestaande load balancer >> **alle instellingen**.
4. Aan de rechterkant Hallo van Hallo dialoogvenster onder de naam van de Hallo Hallo load balancer, schuif te**bewaking**, klikt u op **Diagnostics**.

    ![Portal - instellingen van een load balancer](./media/load-balancer-monitor-log/load-balancer-settings.png)

5. In Hallo **Diagnostics** deelvenster onder **Status**, selecteer **op**.
6. Klik op **Opslagaccount**.
7. Onder **LOGBOEKEN**, selecteer een bestaand opslagaccount of maak een nieuwe. Hallo schuifregelaar toodetermine hoeveel dagen aan gebeurtenisgegevens wordt opgeslagen in de gebeurtenislogboeken Hallo gebruiken. 
8. Klik op **Opslaan**.

    ![Portal - logboeken met diagnostische gegevens](./media/load-balancer-monitor-log/load-balancer-diagnostics.png)

> [!NOTE]
> Controlelogboeken vereisen een afzonderlijke opslagaccount niet. Hallo gebruik van opslag voor de gebeurtenis en health test logboekregistratie wordt service worden kosten in rekening.

## <a name="audit-log"></a>Controlelogboek

Hallo-controlelogboek wordt standaard gegenereerd. Hallo-logboeken worden bewaard gedurende 90 dagen in Azure gebeurtenislogboeken store. Meer informatie over deze logboeken door te lezen Hallo [gebeurtenissen bekijken en controlelogboeken](../monitoring-and-diagnostics/insights-debugging-with-events.md) artikel.

## <a name="alert-event-log"></a>Waarschuwing gebeurtenislogboek

Dit logboek wordt alleen gegenereerd als u het hebt ingeschakeld op een per load balancer basis. Hallo-gebeurtenissen worden vastgelegd in JSON-indeling en opgeslagen in Hallo storage-account opgegeven wanneer u Hallo-logboekregistratie is ingeschakeld. Hallo Hieronder volgt een voorbeeld van een gebeurtenis.

```json
{
    "time": "2016-01-26T10:37:46.6024215Z",
    "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
    "category": "LoadBalancerAlertEvent",
    "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
    "operationName": "LoadBalancerProbeHealthStatus",
    "properties": {
        "eventName": "Resource Limits Hit",
        "eventDescription": "Ports exhausted",
        "eventProperties": {
            "public ip address": "40.117.227.32"
        }
    }
}
```

Hallo JSON-uitvoer toont Hallo *eventname* eigenschap die wordt beschreven Hallo reden voor Hallo load balancer een waarschuwing gemaakt. In dit geval is Hallo waarschuwing gegenereerd vervallen tooTCP poort uitputting veroorzaakt door de bron-IP NAT beperkt (snat omzetten).

## <a name="health-probe-log"></a>Health test-logboek

Dit logboek wordt alleen gegenereerd als u het hebt ingeschakeld op een per per load balancer als gedetailleerde hierboven. Hallo-gegevens worden opgeslagen in Hallo storage-account opgegeven wanneer u Hallo-logboekregistratie is ingeschakeld. Een container met de naam 'insights-logboeken-loadbalancerprobehealthstatus' wordt gemaakt en Hallo volgt gegevens vastgelegd:

```json
{
    "records":[
    {
        "time": "2016-01-26T10:37:46.6024215Z",
        "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
        "category": "LoadBalancerProbeHealthStatus",
        "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
        "operationName": "LoadBalancerProbeHealthStatus",
        "properties": {
            "publicIpAddress": "40.83.190.158",
            "port": "81",
            "totalDipCount": 2,
            "dipDownCount": 1,
            "healthPercentage": 50.000000
        }
    },
    {
        "time": "2016-01-26T10:37:46.6024215Z",
        "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
        "category": "LoadBalancerProbeHealthStatus",
        "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
        "operationName": "LoadBalancerProbeHealthStatus",
        "properties": {
            "publicIpAddress": "40.83.190.158",
            "port": "81",
            "totalDipCount": 2,
            "dipDownCount": 0,
            "healthPercentage": 100.000000
        }
    }]
}
```

Hallo JSON-uitvoer geeft in Hallo eigenschappen veld Hallo basisinformatie voor Hallo test gezondheidsstatus. Hallo *dipDownCount* eigenschap toont Hallo kunt u het totale aantal exemplaren op Hallo back-end die netwerkverkeer vanwege toofailed test antwoorden niet ontvangen.

## <a name="view-and-analyze-hello-audit-log"></a>Weergeven en analyseren van het controlelogboek Hallo

U kunt weergeven en analyseren van audit logboekgegevens met behulp van een Hallo volgende methoden:

* **Azure-hulpprogramma's:** gegevens ophalen uit controlelogboeken Hallo via Azure PowerShell, hello Azure opdrachtregelinterface (CLI), hello Azure REST-API of hello Azure preview-portal. Stapsgewijze instructies voor elke methode zijn aangegeven in Hallo [bewerkingen met Resource Manager controleren](../azure-resource-manager/resource-group-audit.md) artikel.
* **Power BI:** als u nog geen een [Power BI](https://powerbi.microsoft.com/pricing) account, kunt u proberen deze gratis. Met behulp van Hallo [Azure controlelogboeken inhoud pack voor Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), kunt u uw gegevens met vooraf geconfigureerde dashboards analyseren, of u weergaven toosuit uw vereisten kunt aanpassen.

## <a name="view-and-analyze-hello-health-probe-and-event-log"></a>Weergeven en analyseren Hallo health test en gebeurtenislogboek

U moet tooconnect tooyour storage-account en Hallo JSON logboekvermeldingen voor gebeurtenis en health test-logboeken ophalen. Zodra u Hallo JSON-bestanden hebt gedownload, kunt u deze converteren tooCSV en weergeven in Excel, Power BI of een ander gegevensvisualisatie-hulpprogramma.

> [!TIP]
> Als u bekend met Visual Studio en de basisconcepten bent van het wijzigen van waarden voor de constanten en variabelen in C#, kunt u Hallo [Meld converter extra](https://github.com/Azure-Samples/networking-dotnet-log-converter) beschikbaar is via GitHub.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Uw Azure controlelogboeken met Power BI visualiseren](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blogbericht.
* [Weergeven en analyseren van Azure controlelogboeken in Power BI en meer](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blogbericht.

## <a name="next-steps"></a>Volgende stappen

[Load Balancer-testen](load-balancer-custom-probe-overview.md)
