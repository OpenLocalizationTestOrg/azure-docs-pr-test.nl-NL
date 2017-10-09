---
title: aaaConfigure gewogen round robin-verkeer met behulp van Azure Traffic Manager routeringsmethode | Microsoft Docs
description: Dit artikel wordt uitgelegd hoe tooload balans vinden tussen verkeer dat gebruikmaakt van een round robin-methode in Traffic Manager
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
ms.openlocfilehash: 7e2866ead0b2b653845435dd420a763c5e175f4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-weighted-traffic-routing-method-in-traffic-manager"></a>Hallo gewogen verkeersrouteringsmethode in Traffic Manager configureren

Een algemene traffic routing methode patroon is tooprovide een reeks identieke eindpunten die zijn onder andere cloudservices en websites en verzenden van verkeer tooeach round-robin toewijst. Hallo stappen te volgen overzicht van hoe tooconfigure dit type methode voor het doorsturen van verkeer.

> [!NOTE]
> Azure Websites bieden al round robin-functionaliteit voor websites binnen een datacenter (ook wel bekend als een regio) voor taakverdeling. Traffic Manager kunt u toospecify round robin verkeersrouteringsmethode voor websites in verschillende datacenters.

## <a name="tooconfigure-hello-weighted-traffic-routing-method"></a>verkeersrouteringsmethode hello gewogen tooconfigure

1. Aanmelden via een browser toohello [Azure-portal](http://portal.azure.com). Als u nog geen account hebt, kunt u zich registreren voor een [gratis proefversie van één maand](https://azure.microsoft.com/free/). 
2. Zoek in de zoekbalk Hallo-portal, op Hallo **Traffic Manager-profielen** en klik vervolgens op Hallo profielnaam die u wilt dat tooconfigure Hallo routeringsmethode voor.
3. In Hallo **Traffic Manager-profiel** blade, Controleer of beide Hallo cloudservices en websites waartoe u tooinclude in uw configuratie aanwezig zijn.
4. In Hallo **instellingen** sectie, klikt u op **configuratie**, en in Hallo **configuratie** blade voltooid zijn als volgt:
    1. Voor **verkeer van de instellingen voor verkeersroutering methode**, Controleer of verkeersrouteringsmethode hello **gewogen**. Als dit niet het geval is, klikt u op **gewogen** uit de vervolgkeuzelijst Hallo.
    2. Set Hallo **monitor eindpuntinstellingen** identiek voor alle elk eindpunt binnen dit profiel als volgt:
        1. Selecteer Hallo juiste **Protocol**, en geef Hallo **poort** getal. 
        2. Voor **pad** Typ een slash  */* . toomonitor eindpunten, moet u een pad en bestandsnaam opgeven. Een schuine streep naar voren '/' is een geldige invoer voor Hallo relatief pad en impliceert dat Hallo-bestand is in de hoofdmap hello (standaard).
        3. Bovenaan Hallo Hallo pagina, klikt u op **opslaan**.
5. Hallo wijzigingen in uw configuratie als volgt testen:
    1.  In de zoekbalk Hallo-portal, zoeken naar Hallo Traffic Manager-profielnaam en Hallo Traffic Manager-profiel in Hallo resultaten op die Hallo weergegeven.
    2.  In Hallo **Traffic Manager** blade profiel, klikt u op **overzicht**.
    3.  Hallo **Traffic Manager-profiel** blade Hallo DNS-naam van de zojuist gemaakte Traffic Manager-profiel wordt weergegeven. Dit kan worden gebruikt door alle clients (bijvoorbeeld door te gaan met een webbrowser tooit) tooget gerouteerd toohello eindpunt rechts zoals wordt bepaald door de routeringstype Hallo. In dit geval alle aanvragen worden doorgestuurd elk eindpunt round-robin toewijst.
6. Als uw Traffic Manager-profiel werkt, bewerken Hallo DNS-record op de gezaghebbende DNS-server toopoint domain name toohello Traffic Manager-domeinnaam van uw bedrijf.

![Gewogen verkeersrouteringsmethode met Traffic Manager configureren][1]

## <a name="next-steps"></a>Volgende stappen

- Meer informatie over [prioriteit van verkeer routeringsmethode](traffic-manager-configure-priority-routing-method.md).
- Meer informatie over [prestaties methode voor het doorsturen van verkeer](traffic-manager-configure-performance-routing-method.md).
- Meer informatie over [routeringsmethode voor geografische](traffic-manager-configure-geographic-routing-method.md).
- Meer informatie over hoe te[Traffic Manager-instellingen testen](traffic-manager-testing-settings.md).

<!--Image references-->
[1]: ./media/traffic-manager-weighted-routing-method/traffic-manager-weighted-routing-method.png
