---
title: aaaConfigure prioriteit van verkeer routeringsmethode met Azure Traffic Manager | Microsoft Docs
description: Dit artikel wordt uitgelegd hoe tooconfigure Hallo prioriteit van verkeer routeringsmethode in Traffic Manager
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 6dca6de1-18f7-4962-bd98-6055771fab22
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/20/2017
ms.author: kumud
ms.openlocfilehash: dd3e3bb2a727e5ea087cee35962c8e6f7c357282
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-priority-traffic-routing-method-in-traffic-manager"></a>Prioriteit verkeersrouteringsmethode in Traffic Manager configureren

Ongeacht de websitemodus hello bieden Azure Websites al failover-functionaliteit voor websites binnen een datacenter (ook wel bekend als een regio). Traffic Manager biedt failover voor websites in verschillende datacenters.

Een algemene patroon voor de service failover is toosend verkeer tooa primaire service en een reeks van identieke back-services voor failover. Hallo volgende stappen wordt uitgelegd hoe tooconfigure met dit prioriteit failover met Azure-cloudservices en websites:

## <a name="tooconfigure-hello-priority-traffic-routing-method"></a>tooconfigure hello prioriteit verkeersrouteringsmethode

1. Aanmelden via een browser toohello [Azure-portal](http://portal.azure.com). Als u nog geen account hebt, kunt u zich registreren voor een [gratis proefversie van één maand](https://azure.microsoft.com/free/). 
2. Zoek in de zoekbalk Hallo-portal, op Hallo **Traffic Manager-profielen** en klik vervolgens op Hallo profielnaam die u wilt dat tooconfigure Hallo routeringsmethode voor.
3. In Hallo **Traffic Manager-profiel** blade, Controleer of beide Hallo cloudservices en websites waartoe u tooinclude in uw configuratie aanwezig zijn.
4. In Hallo **instellingen** sectie, klikt u op **configuratie**, en in Hallo **configuratie** blade voltooid zijn als volgt:
    1. Voor **verkeer van de instellingen voor verkeersroutering methode**, Controleer of verkeersrouteringsmethode hello **prioriteit**. Als dit niet het geval is, klikt u op **prioriteit** uit de vervolgkeuzelijst Hallo.
    2. Set Hallo **monitor eindpuntinstellingen** identiek voor alle elk eindpunt binnen dit profiel als volgt:
        1. Selecteer Hallo juiste **Protocol**, en geef Hallo **poort** getal. 
        2. Voor **pad** Typ een slash  */* . toomonitor eindpunten, moet u een pad en bestandsnaam opgeven. Een schuine streep naar voren '/' is een geldige invoer voor Hallo relatief pad en impliceert dat Hallo-bestand is in de hoofdmap hello (standaard).
        3. Bovenaan Hallo Hallo pagina, klikt u op **opslaan**.
5. In Hallo **instellingen** sectie, klikt u op **eindpunten**.
6. In Hallo **eindpunten** blade revisie Hallo prioriteitsvolgorde voor uw eindpunten. Wanneer u selecteert Hallo **prioriteit** verkeersrouteringsmethode, Hallo volgorde van Hallo geselecteerd eindpunten is van belang. Controleer of de volgorde van prioriteit Hallo van eindpunten.  Hallo primaire eindpunt heeft op de voorgrond. Controleer op het Hallo-volgorde die wordt weergegeven. alle aanvragen wordt het eerste eindpunt gerouteerde toohello en als Traffic Manager wordt gedetecteerd, worden niet in orde, het volgende eindpunt toohello Hallo verkeer automatisch failover. 
7. toochange Hallo eindpunt op volgorde van prioriteit, klikt u op Hallo eindpunt, en in Hallo **eindpunt** blade die wordt weergegeven, klikt u op **bewerken** en wijzig Hallo **prioriteit** waarde indien nodig . 
8. Klik op **opslaan** toosave Hallo eindpuntinstellingen wijzigen.
9. Nadat u uw wijzigingen in de configuratie hebt voltooid, klikt u op **opslaan** Hallo Hallo pagina onderaan in.
10. Hallo wijzigingen in uw configuratie als volgt testen:
    1.  In de zoekbalk Hallo-portal, zoeken naar Hallo Traffic Manager-profielnaam en Hallo Traffic Manager-profiel in Hallo resultaten op die Hallo weergegeven.
    2.  In Hallo **Traffic Manager** blade profiel, klikt u op **overzicht**.
    3.  Hallo **Traffic Manager-profiel** blade Hallo DNS-naam van de zojuist gemaakte Traffic Manager-profiel wordt weergegeven. Dit kan worden gebruikt door alle clients (bijvoorbeeld door te gaan met een webbrowser tooit) tooget gerouteerd toohello eindpunt rechts zoals wordt bepaald door de routeringstype Hallo. In dit geval alle aanvragen zijn de eerste eindpunt gerouteerde toohello en als Traffic Manager wordt gedetecteerd, worden niet in orde, het volgende eindpunt toohello Hallo verkeer automatisch failover.
11. Als uw Traffic Manager-profiel werkt, bewerken Hallo DNS-record op de gezaghebbende DNS-server toopoint domain name toohello Traffic Manager-domeinnaam van uw bedrijf.

![Prioriteit verkeersrouteringsmethode met Traffic Manager configureren][1]

## <a name="next-steps"></a>Volgende stappen


- Meer informatie over [verkeersrouteringsmethode gewogen](traffic-manager-configure-weighted-routing-method.md).
- Meer informatie over [routeringsmethode voor prestaties](traffic-manager-configure-performance-routing-method.md).
- Meer informatie over [routeringsmethode voor geografische](traffic-manager-configure-geographic-routing-method.md).
- Meer informatie over hoe te[Traffic Manager-instellingen testen](traffic-manager-testing-settings.md).

<!--Image references-->
[1]: ./media/traffic-manager-priority-routing-method/traffic-manager-priority-routing-method.png