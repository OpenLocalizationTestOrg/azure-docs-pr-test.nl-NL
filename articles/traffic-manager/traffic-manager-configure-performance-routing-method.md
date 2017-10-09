---
title: aaaConfigure prestaties verkeer routeringsmethode met Azure Traffic Manager | Microsoft Docs
description: Dit artikel wordt uitgelegd hoe tooconfigure Traffic Manager tooroute toohello eindpunt verkeer met de laagste latentie
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
ms.openlocfilehash: d0ccd4c9de411844c6f36068859265244f4aa52b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-performance-traffic-routing-method"></a>Hallo verkeersrouteringsmethode voor prestaties configureren

Hallo verkeersrouteringsmethode prestaties kunt u toodirect verkeer toohello eindpunt met de laagste latentie Hallo van Hallo clientnetwerk. Hallo-datacenter met de laagste latentie Hallo is doorgaans Hallo dichtstbijzijnde in geografische afstand. Deze methode voor het doorsturen van verkeer kan geen account voor realtime-wijzigingen in de netwerkconfiguratie of laden.

##  <a name="tooconfigure-performance-routing-method"></a>routeringsmethode voor prestaties tooconfigure

1. Aanmelden via een browser toohello [Azure-portal](http://portal.azure.com). Als u nog geen account hebt, kunt u zich registreren voor een [gratis proefversie van één maand](https://azure.microsoft.com/free/). 
2. Zoek in de zoekbalk Hallo-portal, op Hallo **Traffic Manager-profielen** en klik vervolgens op Hallo profielnaam die u wilt dat tooconfigure Hallo routeringsmethode voor.
3. In Hallo **Traffic Manager-profiel** blade, Controleer of beide Hallo cloudservices en websites waartoe u tooinclude in uw configuratie aanwezig zijn.
4. In Hallo **instellingen** sectie, klikt u op **configuratie**, en in Hallo **configuratie** blade voltooid zijn als volgt:
    1. Voor **verkeer van de instellingen voor verkeersroutering methode**, voor **routeringsmethode** Selecteer **prestaties**.
    2. Set Hallo **monitor eindpuntinstellingen** identiek voor alle elk eindpunt binnen dit profiel als volgt:
        1. Selecteer Hallo juiste **Protocol**, en geef Hallo **poort** getal. 
        2. Voor **pad** Typ een slash  */* . toomonitor eindpunten, moet u een pad en bestandsnaam opgeven. Een schuine streep naar voren '/' is een geldige invoer voor Hallo relatief pad en impliceert dat Hallo-bestand is in de hoofdmap hello (standaard).
        3. Bovenaan Hallo Hallo pagina, klikt u op **opslaan**.
5.  Hallo wijzigingen in uw configuratie als volgt testen:
    1.  In de zoekbalk Hallo-portal, zoeken naar Hallo Traffic Manager-profielnaam en Hallo Traffic Manager-profiel in Hallo resultaten op die Hallo weergegeven.
    2.  In Hallo **Traffic Manager** blade profiel, klikt u op **overzicht**.
    3.  Hallo **Traffic Manager-profiel** blade Hallo DNS-naam van de zojuist gemaakte Traffic Manager-profiel wordt weergegeven. Dit kan worden gebruikt door alle clients (bijvoorbeeld door te gaan met een webbrowser tooit) tooget gerouteerd toohello eindpunt rechts zoals wordt bepaald door de routeringstype Hallo. In dit geval worden alle aanvragen gerouteerde toohello eindpunt met de laagste latentie Hallo van Hallo clientnetwerk.
6. Als uw Traffic Manager-profiel werkt, bewerken Hallo DNS-record op de gezaghebbende DNS-server toopoint domain name toohello Traffic Manager-domeinnaam van uw bedrijf.

![Prestaties verkeersrouteringsmethode met Traffic Manager configureren][1]

## <a name="next-steps"></a>Volgende stappen

- Meer informatie over [verkeersrouteringsmethode gewogen](traffic-manager-configure-weighted-routing-method.md).
- Meer informatie over [routeringsmethode voor prioriteit](traffic-manager-configure-priority-routing-method.md).
- Meer informatie over [routeringsmethode voor geografische](traffic-manager-configure-geographic-routing-method.md).
- Meer informatie over hoe te[Traffic Manager-instellingen testen](traffic-manager-testing-settings.md).

<!--Image references-->
[1]: ./media/traffic-manager-performance-routing-method/traffic-manager-performance-routing-method.png