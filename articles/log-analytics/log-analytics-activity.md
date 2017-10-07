---
title: aaaView Azure activiteit logboeken met Log Analytics | Microsoft Docs
description: U kunt hello Azure activiteitenlogboeken oplossing tooanalyze en zoeken hello Azure activiteitenlogboek voor uw Azure abonnementen gebruiken.
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: dbac4c73-0058-4191-a906-e59aca8e2ee0
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: banders
ms.openlocfilehash: 171d0d604d03a5714a9599cc0b448fc5f6471f69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="view-azure-activity-logs"></a>Azure activiteit-logboeken bekijken

![Azure activiteitenlogboeken symbool](./media/log-analytics-activity/activity-log-analytics.png)

Hallo activiteit Log Analytics-oplossing helpt u bij het analyseren en zoek Hallo [Azure activiteitenlogboek](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) voor uw Azure abonnementen. Hello Azure Activity Log is een logboek biedt inzicht in Hallo bewerkingen die worden uitgevoerd op resources in uw abonnementen. Hallo activiteitenlogboek heette vroeger *controlelogboeken* of *operationele logboeken* omdat gebeurtenissen voor uw abonnementen rapporteert.

Met de Hallo activiteitenlogboek, kunt u Hallo bepalen *wat*, *die*, en *wanneer* voor een (PUT, POST, verwijderen schrijfbewerkingen) gemaakt voor Hallo resources in uw abonnement. U kunt ook Hallo status van het Hallo-bewerkingen en andere relevante eigenschappen begrijpen. Hallo activiteitenlogboek bevat geen lezen (GET)-bewerkingen en bewerkingen voor resources die Hallo klassieke implementatiemodel gebruikt.

Wanneer u verbinding maakt met uw Azure-activiteit logboeken tooLog Analytics, kunt u het volgende doen:

- Hallo activiteitenlogboeken met vooraf gedefinieerde weergaven analyseren
- Analyseren en zoek- en logboeken van meerdere Azure-abonnementen
- Activiteitenlogboeken voor meer dan 90 dagen bewaren<sup>1</sup>
- Activiteitenlogboeken correleren met andere Azure-platform-en toepassingsgegevens
- Zie operationele activiteiten samenvoegen met status
- Weergave van trends van activiteiten plaatsvinden op elk van uw Azure-services
- Rapport over autorisatie wijzigingen op alle Azure-resources
- Onderbreking of service problemen die invloed hebben op uw resources bepalen
- Logboek zoeken toocorrelate gebruikersactiviteiten, automatisch schalen operations, wijzigingen van de autorisatie, en servicelogboeken health tooother of metrische gegevens uit uw omgeving gebruiken

<sup>1</sup>standaard logboekanalyse houdt uw Azure activiteitenlogboeken negentig dagen weergegeven, zelfs als u op Hallo gratis laag. Of, als u een instelling voor het bewaren van werkruimte van minder dan 90 dagen hebben. Als uw werkruimte bewaren die langer is dan 90 dagen heeft, Hallo activiteitenlogboeken bewaard voor de bewaarperiode Hallo van uw werkruimte.

Log Analytics verzamelt activiteitenlogboeken kosteloos en slaat Hallo logboeken gedurende 90 dagen gratis. Als u Logboeken voor meer dan 90 dagen opslaat, wordt u kosten gegevens bewaren voor Hallo gegevens langer is dan 90 dagen opgeslagen.

Wanneer u op de gratis prijscategorie hello bent, activiteitenlogboeken niet tooyour dagelijkse gegevens consumptie van toepassing.

## <a name="connected-sources"></a>Verbonden bronnen

In tegenstelling tot de meeste andere Log Analytics-oplossingen, is niet gegevens voor activiteitenlogboeken verzameld door agents. Alle gegevens die worden gebruikt door Hallo oplossing komt rechtstreeks uit Azure.

| Verbonden bron | Ondersteund | Beschrijving |
| --- | --- | --- |
| [Windows-agents](log-analytics-windows-agents.md) | Nee | Hallo oplossing verzamelt geen informatie van Windows-agents. |
| [Linux-agents](log-analytics-linux-agents.md) | Nee | Hallo-oplossing worden geen gegevens verzameld van Linux-agents. |
| [SCOM-beheergroep](log-analytics-om-agents.md) | Nee | Hallo-oplossing worden geen gegevens verzameld van agents in een verbonden SCOM-beheergroep. |
| [Azure Storage-account](log-analytics-azure-storage.md) | Nee | Hallo oplossing verzamelt geen gegevens naar Azure storage. |

## <a name="prerequisites"></a>Vereisten

- tooaccess Azure activiteit logboekgegevens, moet u een Azure-abonnement hebben.

## <a name="configuration"></a>Configuratie

Volgende stappen tooconfigure Hallo activiteit Log Analytics-oplossing voor uw werkruimten Hallo uitvoeren.

1. Hallo activiteit Log Analytics-oplossing van Hallo inschakelen [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureActivityOMS?tab=Overview) of met behulp van Hallo procedure beschreven in [toevoegen Log Analytics-oplossingen van Hallo galerie met oplossingen](log-analytics-add-solutions.md).
2. Werkruimte voor logboekanalyse van activiteit logboeken toogo tooyour configureren.
    1. In hello Azure-portal, selecteer uw werkruimte en klik op **Azure Activity log**.
    2. Klik op de naam van een abonnement Hallo voor elk abonnement.  
        ![Abonnement toevoegen](./media/log-analytics-activity/add-subscription.png)
    3. In Hallo *SubscriptionName* blade, klikt u op **Connect**.  
        ![verbinding maken met abonnement](./media/log-analytics-activity/subscription-connect.png)

Als u Hallo-oplossing met behulp van de OMS-portal Hallo toevoegt, ziet u Hallo volgende tegel. Azure portal tooconnect toohello aanmelden met een Azure-abonnement tooyour-werkruimte.  
![beoordeling uitvoeren](./media/log-analytics-activity/tile-performing-assessment.png)

## <a name="using-hello-solution"></a>Met behulp van Hallo-oplossing

Wanneer u Hallo activiteit Log Analytics-oplossing tooyour werkruimte toevoegt, Hallo **Azure activiteitenlogboeken** tegel tooyour Overzichtsdashboard is toegevoegd. Deze tegel geeft een telling van het aantal Azure activiteitsrecords bekijkt hello weer voor hello Azure-abonnementen die Hallo-oplossing heeft voor toegang tot.

![Azure activiteitenlogboeken tegel](./media/log-analytics-activity/azure-activity-logs-tile.png)

### <a name="view-azure-activity-logs"></a>Registreert de activiteit Azure weergeven

Klik op Hallo **Azure activiteitenlogboeken** tegel tooopen hello **Azure activiteitenlogboeken** dashboard. Hallo dashboard bevat Hallo blades Hallo volgende tabel. Elke blade geeft een lijst van too10 items die overeenkomen met die van de blade criteria voor Hallo bereik en tijdbereik opgegeven. U kunt een logboek-zoekquery waarmee alle records door te klikken op uitvoeren **alle** onderin Hallo van Hallo-blade of door te klikken op Hallo blade-header.

Logboekgegevens van de activiteit wordt alleen weergegeven *nadat* u uw oplossing activiteit logboeken toogo toohello hebt geconfigureerd, zodat u gegevens voor die tijd niet weergeven.

| Blade | Beschrijving |
| --- | --- |
| Logboekvermeldingen Azure activiteit | Toont een staafdiagram van bovenste hello Azure activiteit logboekvermelding record totalen voor Hallo datumbereik dat u hebt geselecteerd en bevat een overzicht van Hallo bovenste 10 activiteit aanroepfuncties. Klik op Hallo staafdiagram toorun logboek zoekt <code>Type=AzureActivity</code>. Klik op een item aanroeper toorun een logboek zoekopdracht logboekvermeldingen voor alle activiteit voor dat item geretourneerd. |
| Activiteitenlogboeken met Status | Toont een ringdiagram voor Azure log de activiteitsstatus voor Hallo datumbereik dat u hebt geselecteerd. Ook wordt een lijst van een lijst met Hallo top tien status records. Klik op Hallo grafiek toorun logboek zoekt <code>Type=AzureActivity &#124; measure count() by ActivityStatus</code>. Klik op een item status toorun een logboek zoekopdracht retourneren van alle activiteit logboekvermeldingen voor die status-record. |
| Activiteitenlogboeken door Resource | Totale aantal resources met activiteitenlogboeken Hallo en lijsten Hallo top tien resources met record telt voor elke resource. Klik op Hallo totale gebied toorun logboek zoekt <code>Type=AzureActivity &#124; measure count() by Resource</code>, waarin alle Azure-resources beschikbaar toohello oplossing. Klik op een resource toorun een logboek zoekopdracht retourneren van alle activiteitenrecords voor die bron. |
| Activiteitenlogboeken door Resourceprovider | Toont Hallo totaal aantal resourceproviders die activiteit produceren logboeken en geeft een lijst van Hallo tien. Klik op Hallo totale gebied toorun logboek zoekt <code>Type=AzureActivity &#124; measure count() by ResourceProvider</code>, waarin alle Azure-resourceproviders. Klik op een resource provider toorun een logboek zoekopdracht alle activiteitenrecords voor Hallo-provider opvragen. |

![Azure activiteitenlogboeken-dashboard](./media/log-analytics-activity/activity-log-dash.png)

## <a name="next-steps"></a>Volgende stappen

- Maak een [waarschuwing](log-analytics-alerts-creating.md) wanneer een bepaalde activiteit gebeurt.
- Gebruik [logboek zoeken](log-analytics-log-searches.md) tooview gedetailleerde informatie uit de activiteitenlogboeken.
