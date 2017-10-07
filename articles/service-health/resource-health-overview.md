---
title: overzicht van aaaAzure bronnen health | Microsoft Docs
description: Overzicht van Azure-resourcestatus
services: Resource health
documentationcenter: 
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: service-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 07/01/2017
ms.author: BernardoAMunoz
ms.openlocfilehash: f06153864090487829f717dc3e8972c78a4a58af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-health-overview"></a>Overzicht van Azure-resource-status
 
Resource Health helpt u bij het diagnosticeren en krijgen van ondersteuning wanneer een Azure-probleem van invloed is op uw resources. Dit biedt u informatie over de huidige en eerdere status Hallo van uw resources en helpt u problemen verhelpen. Resource Health biedt technische ondersteuning als u hulp nodig heeft bij problemen met Azure-services.

Terwijl [Azure Status](https://status.azure.com) biedt u informatie over problemen met de service die invloed hebben op een uitgebreide reeks Azure-klanten, resourcestatus biedt u een aangepaste dashboard van Hallo status van uw resources. Resourcestatus ziet u alle Hallo tijden uw resources niet beschikbaar in Hallo zijn achterstallige tooAzure problemen met de service. Dit maakt het eenvoudig voor u toounderstand als een SLA is geschonden. 

## <a name="what-is-considered-a-resource-and-how-does-resource-health-decides-if-a-resource-is-healthy-or-not"></a>Wat wordt beschouwd als een resource en hoe gaat resourcestatus besluit als een bron in orde is?
Een bron is een exemplaar van een resourcetype die worden aangeboden door een Azure-service via Azure Resource Manager, bijvoorbeeld: een virtuele machine, een web-app of een SQL-database.

Resourcestatus is afhankelijk van signalen door Hallo verschillende Azure-services tooassess verzonden als een resource in orde of niet is. Als een resource niet in orde is, analyseert resourcestatus aanvullende informatie toodetermine Hallo bron van Hallo probleem. Ook worden acties die Microsoft duurt toofix Hallo probleem of acties die u kunt uitvoeren tooaddress Hallo veroorzaken van Hallo probleem. 

Bekijk Hallo volledige lijst met brontypen en health controleert [Azure resourcestatus](resource-health-checks-resource-types.md) voor meer informatie over hoe status wordt beoordeeld.

## <a name="health-status-provided-by-resource-health"></a>Gezondheidsstatus geleverd door de resourcestatus
Hallo-status van een bron is een van volgende statussen Hallo:

### <a name="available"></a>Beschikbaar
Hallo-service heeft alle gebeurtenissen die invloed hebben op Hallo status van Hallo resource niet gevonden. In gevallen waarbij Hallo resource is hersteld van niet-geplande uitvaltijd tijdens Hallo laatste 24 uur, u ziet Hallo **recent is hersteld** melding.

![Bron health beschikbare virtuele machine](./media/resource-health-overview/Available.png)

### <a name="unavailable"></a>Niet beschikbaar
Hallo-service heeft een lopende platformupdate of niet-platformgebeurtenis die invloed hebben op Hallo status van Hallo resource gedetecteerd.

#### <a name="platform-events"></a>Platform-gebeurtenissen
Deze gebeurtenissen worden geactiveerd door meerdere onderdelen van hello Azure-infrastructuur en omvatten zowel geplande acties zoals gepland onderhoud en onverwachte incidenten, zoals een niet-geplande host opnieuw worden opgestart.

Resourcestatus biedt aanvullende details over Hallo-gebeurtenis met het herstelproces Hallo en kunt u toocontact ondersteuning zelfs als u een actieve Microsoft overeenkomst ondersteunen geen hebt.

![Resource health niet via een virtuele machine vanwege tooplatform gebeurtenis](./media/resource-health-overview/Unavailable.png)

#### <a name="non-platform-events"></a>Niet-Platform-gebeurtenissen
Deze gebeurtenissen worden geactiveerd door acties die worden uitgevoerd door gebruikers, bijvoorbeeld een virtuele machine stoppen of het maximum aantal verbindingen tooa Redis-Cache Hallo bereikt.

![Resource health niet via een virtuele machine vanwege toonon platformgebeurtenis](./media/resource-health-overview/Unavailable_NonPlatform.png)

### <a name="unknown"></a>Onbekend
Deze health-status geeft aan dat resourcestatus informatie over deze bron voor meer dan 10 minuten niet heeft ontvangen. Deze status is niet een definitieve indicatie van Hallo status van Hallo bron, zijn maar er een belangrijk gegevenspunt in Hallo procedure voor probleemoplossing:
* Als Hallo resource wordt uitgevoerd als de status van de verwachte Hallo van Hallo resource wordt tooAvailable bijgewerkt na een paar minuten.
* Als u problemen met Hallo resource ondervindt, hello onbekende gezondheidsstatus kan worden voorgesteld Hallo resource wordt beïnvloed door een gebeurtenis in het Hallo-platform.

![Bron health onbekende virtuele machine](./media/resource-health-overview/Unknown.png)

## <a name="report-an-incorrect-status"></a>Een onjuiste status rapporteren
Als u Hallo huidige health-status is onjuist op elk gewenst moment denkt, kunt u laat ons weten door te klikken op **rapporteren onjuist gezondheidsstatus**. In gevallen waarin u worden beïnvloed door een probleem met de Azure, raden we u toocontact ondersteuning van de resourceblade health Hallo. 

![Resourcestatus rapport onjuiste Status](./media/resource-health-overview/incorrect-status.png)

## <a name="historical-information"></a>Historische gegevens
U toegang hebt tot too14 dagen van historische gegevens door te klikken op **Historie weergeven** Hallo bron health-blade. 

![Resourcestatus rapportgeschiedenis](./media/resource-health-overview/history-blade.png)

## <a name="getting-started"></a>Aan de slag
tooopen resourcestatus voor één resource
1.  Meld u aan bij hello Azure-portal.
2.  Navigeer tooyour resource.
3.  Hallo resource menu zich in de linkerkant hello, klik op **resourcestatus**.

![Open resourcestatus van Resource-blade](./media/resource-health-overview/from-resource-blade.png)

U kunt de resourcestatus ook openen door te klikken op **meer services**, en typ **resourcestatus** in filter tekst vak tooopen hello **Help + ondersteuning** blade. Klik tot slot [ **resourcestatus**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).

![Resourcestatus openen vanuit meer service](./media/resource-health-overview/FromOtherServices.png)

## <a name="next-steps"></a>Volgende stappen

Bekijk deze resources toolearn meer informatie over de resourcestatus:
-  [Status van resourcetypen en controleert in Azure resourcestatus](resource-health-checks-resource-types.md)
-  [Veelgestelde vragen over Azure-resource-status](resource-health-faq.md)




