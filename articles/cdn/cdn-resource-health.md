---
title: aaaMonitor hello status van Azure CDN resources | Microsoft Docs
description: Meer informatie over hoe toomonitor Hallo status van uw Azure CDN-resources met behulp van de status van de Azure-resources.
services: cdn
documentationcenter: .net
author: zhangmanling
manager: zhangmanling
editor: 
ms.assetid: bf23bd89-35b2-4aca-ac7f-68ee02953f31
ms.service: cdn
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 0a77e56d2fecae4bde6c83730c05375853a6638a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-hello-health-of-azure-cdn-resources"></a>Hallo-status van Azure CDN-resources bewaken
  
Azure CDN resourcestatus is een subset van [Azure resourcestatus](../resource-health/resource-health-overview.md).  U kunt Azure-resource health toomonitor Hallo status van CDN-resources gebruiken en bruikbare richtlijnen tootroubleshoot problemen ontvangen.

>[!IMPORTANT] 
>Azure CDN-resourcestatus accounts momenteel alleen Hallo status van globale levering van CDN en API-mogelijkheden.  Azure CDN-resourcestatus controleert niet of afzonderlijke CDN-eindpunten.
>
>Hallo geeft aan dat de resourcestatus Azure CDN feed mogelijk up too15 minuten vertraagd.

## <a name="how-toofind-azure-cdn-resource-health"></a>Hoe toofind Azure CDN-resourcestatus

1. In Hallo [Azure-portal](https://portal.azure.com), bladeren tooyour CDN-profiel.

2. Klik op Hallo **instellingen** knop.

    ![Knop Instellingen](./media/cdn-resource-health/cdn-profile-settings.png)

3. Onder *ondersteuning + probleemoplossing*, klikt u op **resourcestatus**.

    ![CDN-resourcestatus](./media/cdn-resource-health/cdn-resource-health3.png)

>[!TIP] 
>U vindt ook CDN bronnen in Hallo *resourcestatus* -tegel in Hallo *Help + ondersteuning* blade.  U kunt snel te krijgen*Help + ondersteuning* door te klikken op Hallo omcirkeld **?** in Hallo rechtsboven Hallo-portal.
>
> ![Help en ondersteuning](./media/cdn-resource-health/cdn-help-support.png)

## <a name="azure-cdn-specific-messages"></a>Azure CDN-specifieke berichten

Hieronder vindt u statussen gerelateerde tooAzure CDN resourcestatus.

|Bericht | Aanbevolen actie |
|---|---|
|U kunt hebt gestopt, verwijderd of onjuist geconfigureerd een of meer van uw CDN-eindpunten | U kunt hebt gestopt, verwijderd of onjuist geconfigureerd een of meer van uw CDN-eindpunten.|
|Helaas, Hallo CDN management-service is momenteel niet beschikbaar | Controleer hier terug voor statusupdates; Als het probleem zich blijft voordoen nadat Hallo oplossingstijd verwacht, neem dan contact op met ondersteuning.|
|Helaas is dat uw CDN-eindpunten wordt mogelijk beïnvloed door een voortdurende problemen met enkele van onze CDN-providers | Controleer hier terug voor statusupdates; Gebruik Hallo oplossen hulpprogramma toolearn hoe tootest uw oorsprong en CDN-eindpunt; Als het probleem zich blijft voordoen nadat Hallo oplossingstijd verwacht, neem dan contact op met ondersteuning. |
|Helaas CDN-eindpunt configuratiewijzigingen ondervinden vertragingen bij het doorgeven | Controleer hier terug voor statusupdates; Als u uw wijzigingen in de configuratie niet volledig in Hallo verwacht tijd worden overgebracht, moet u contact op met ondersteuning.|
|We vinden het jammer, dat er zijn momenteel problemen bij het laden van de aanvullende portal Hallo | Controleer hier terug voor statusupdates; Als het probleem zich blijft voordoen nadat Hallo oplossingstijd verwacht, neem dan contact op met ondersteuning.|
Helaas, dat we hebben momenteel problemen met enkele van onze CDN-providers | Controleer hier terug voor statusupdates; Als het probleem zich blijft voordoen nadat Hallo oplossingstijd verwacht, neem dan contact op met ondersteuning. |

## <a name="next-steps"></a>Volgende stappen

- [Een overzicht van Azure resourcestatus lezen](../resource-health/resource-health-overview.md)
- [Problemen oplossen met CDN compressie](./cdn-troubleshoot-compression.md)
- [Problemen oplossen met 404-fouten](./cdn-troubleshoot-endpoint.md)