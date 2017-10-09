---
title: aaaCreate een Traffic Manager-profiel in Azure | Microsoft Docs
description: Dit artikel wordt beschreven hoe toocreate een Traffic Manager-profiel
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: kumud
ms.openlocfilehash: 5cd3d2903552c9a0427da41a73f6f38f6b0afc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-traffic-manager-profile"></a>Een Traffic Manager-profiel maken

Dit artikel wordt beschreven hoe u een profiel met **prioriteit** routeringstype tooroute gebruikers tootwo Azure Web Apps eindpunten kan worden gemaakt. Met behulp van Hallo **prioriteit** type routering, al het verkeer is het eerste eindpunt gerouteerde toohello terwijl de tweede hello wordt opgeslagen als een back-up. Gebruikers kunnen gerouteerde toohello tweede eindpunt als gevolg hiervan zijn als het eerste eindpunt Hallo slecht.

In dit artikel zijn twee eerder gemaakte Azure-Web-App-eindpunten Traffic Manager-profiel gekoppeld toothis nieuw gemaakt. meer over hoe u toolearn toocreate Azure-Web-App eindpunten, gaat u naar Hallo [documentatiepagina voor Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/). U kunt een willekeurig eindpunt dat een DNS-naam heeft en bereikbaar is via toevoegen Hallo internet en dat we Azure Web Apps eindpunten als voorbeeld gebruiken.

### <a name="create-a-traffic-manager-profile"></a>Een Traffic Manager-profiel maken
1. Aanmelden via een browser toohello [Azure-portal](http://portal.azure.com). Als u nog een account hebt, kunt u aanmelden voor een [gratis proefversie van één maand](https://azure.microsoft.com/free/). 
2. Op Hallo **Hub** menu, klikt u op **nieuw** > **Networking** > **alle**, klikt u op **verkeer Manager** profiel tooopen hello **maken Traffic Manager-profiel** blade, klikt u vervolgens op **maken**.
3. Op Hallo **maken Traffic Manager-profiel** blade voltooid zijn als volgt:
    1. In **Naam** geeft u een naam op voor het profiel. Deze naam moet uniek zijn binnen Hallo trafficmanager.net zone beschikken over toobe en resulteert in het Hallo DNS-naam <name>, trafficmanager.net die gebruikte tooaccess uw Traffic Manager-profiel.
    2. In **routeringsmethode**, selecteer Hallo **prioriteit** routeringsmethode.
    3. In **abonnement**, selecteert u dit profiel onder toocreate wilt Hallo-abonnement
    4. In **resourcegroep**, dit profiel onder een nieuwe resource groep tooplace maakt.
    5. In **locatie voor resourcegroep**, Hallo-locatie van resourcegroep Hallo selecteren. Deze instelling verwijst toohello locatie van resourcegroep Hallo en heeft geen invloed op Hallo Traffic Manager-profiel dat globaal wordt geïmplementeerd.
    6. Klik op **Create**.
    7. Wanneer de globale implementatie Hallo van uw Traffic Manager-profiel voltooid is, wordt het weergegeven in de betreffende resourcegroep als een van de Hallo resources.

    ![Een Traffic Manager-profiel maken](./media/traffic-manager-create-profile/Create-traffic-manager-profile.png)

## <a name="add-traffic-manager-endpoints"></a>Traffic Manager-eindpunten toevoegen

1. Zoek in de zoekbalk Hallo-portal, op Hallo **Traffic Manager-profiel** naam die u hebt gemaakt in de voorgaande sectie en klikt u op Hallo traffic manager-profiel in Hallo Hallo resulteert dat Hallo weergegeven.
2. In Hallo **Traffic Manager-profiel** blade in Hallo **instellingen** sectie, klikt u op **eindpunten**.
3. In Hallo **eindpunten** blade die wordt weergegeven, klikt u op **toevoegen**.
4. In Hallo **eindpunt toevoegen** blade voltooid zijn als volgt:
    1. Klik bij **Type** op **Azure-eindpunt**.
    2. Geef een **naam** waarop u wilt toorecognize dit eindpunt.
    3. Voor **resource doeltype**, klikt u op **App Service**.
    4. Voor **Doelresource**, klikt u op **kiest u een app service** tooshow Hallo aanbieding Hallo Web-Apps onder Hallo hetzelfde abonnement. In Hallo **Resource** blade die wordt weergegeven, kies Hallo gewenste tooadd als eerste eindpunt Hallo-App service.
    5. Selecteer bij **Prioriteit** de optie **1**. Dit resulteert in alle verkeer dat hierheen gaat toothis eindpunt als deze is in orde.
    6. Laat **Toevoegen als uitgeschakeld** uit staan.
    7. Klik op **OK**
5.  Herhaal stap 3 en 4 voor Hallo volgende Azure Web Apps-eindpunt. Zorg ervoor dat tooadd deze met de **prioriteit** waarde ingesteld op **2**.
6.  Wanneer Hallo toevoeging van beide eindpunten voltooid is, worden deze weergegeven in Hallo **Traffic Manager-profiel** blade samen met hun status controleren als **Online**.

    ![Een Traffic Manager-eindpunt toevoegen](./media/traffic-manager-create-profile/add-traffic-manager-endpoint.png)

## <a name="use-hello-traffic-manager-profile"></a>Hallo Traffic Manager-profiel gebruiken
1.  Zoek in de zoekbalk Hallo-portal, op Hallo **Traffic Manager-profiel** naam die u hebt gemaakt in de voorgaande sectie Hallo. In de resultaten Hallo die worden weergegeven, klikt u op Hallo traffic manager-profiel.
2. In Hallo **Traffic Manager-profiel** blade, klikt u op **overzicht**.
3. Hallo **Traffic Manager-profiel** blade Hallo DNS-naam van de zojuist gemaakte Traffic Manager-profiel wordt weergegeven. Dit kan worden gebruikt door alle clients (bijvoorbeeld door te gaan met een webbrowser tooit) tooget gerouteerd toohello eindpunt rechts zoals wordt bepaald door de routeringstype Hallo. In dit geval alle aanvragen zijn de eerste eindpunt gerouteerde toohello en als Traffic Manager wordt gedetecteerd, worden niet in orde, Hallo verkeer automatisch via het volgende eindpunt toohello mislukt.

## <a name="delete-hello-traffic-manager-profile"></a>Hallo Traffic Manager-profiel verwijderen
Wanneer deze niet langer nodig is, verwijderen Hallo-resourcegroep en Hallo Traffic Manager-profiel dat u hebt gemaakt. toodo Selecteer dus Hallo-resourcegroep van Hallo **Traffic Manager-profiel** blade en klik op **verwijderen**.

## <a name="next-steps"></a>Volgende stappen

- Meer informatie over [routering typen](traffic-manager-routing-methods.md).
- Meer informatie over eindpunttypen [eindpunttypen](traffic-manager-endpoint-types.md).
- Meer informatie over [eindpuntcontrole](traffic-manager-monitoring.md).



