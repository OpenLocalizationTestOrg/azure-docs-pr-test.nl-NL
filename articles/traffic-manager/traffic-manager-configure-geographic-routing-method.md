---
title: geografische aaaConfigure verkeer routeringsmethode met Azure Traffic Manager | Microsoft Docs
description: Dit artikel wordt uitgelegd hoe tooconfigure Hallo geografische verkeersrouteringsmethode met behulp van Azure Traffic Manager
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
ms.date: 03/22/2017
ms.author: kumud
ms.openlocfilehash: 4142389211ae54e7feea6564641e01e4477491e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-geographic-traffic-routing-method-using-traffic-manager"></a>Hallo geografische verkeersrouteringsmethode met Traffic Manager configureren

Hallo geografische verkeersrouteringsmethode kunt u verkeer toodirect toospecific eindpunten op basis van de geografische locatie Hallo waar Hallo aanvragen afkomstig zijn. Deze zelfstudie laat zien u hoe toocreate een Traffic Manager-profiel met deze methode voor het doorsturen en configureer Hallo eindpunten tooreceive verkeer van specifieke locaties.

## <a name="create-a-traffic-manager-profile"></a>Een Traffic Manager-profiel maken

1. Aanmelden via een browser toohello [Azure-portal](http://portal.azure.com). Als u nog geen account hebt, kunt u zich registreren voor een [gratis proefversie van één maand](https://azure.microsoft.com/free/).
2. Klik op het menu Hub Hallo **nieuw** > **Networking** > **alle**, en klik vervolgens op **Traffic Manager-profiel**tooopen hello **maken Traffic Manager-profiel** blade.
3. Op Hallo **maken Traffic Manager-profiel** blade:
    1. Geef een naam voor uw profiel. Deze naam moet toobe uniek zijn binnen Hallo trafficmanager.net zone en resulteert in het Hallo DNS-naam <profilename>, trafficmanager.net die zal worden gebruikt tooaccess uw Traffic Manager-profiel.
    2. Selecteer Hallo **geografisch** routeringsmethode.
    3. Hallo-abonnement die u dit profiel onder toocreate wilt selecteren.
    4. Gebruik een bestaande resourcegroep of maak een nieuwe resource groep tooplace dit profiel onder. Als u een nieuwe resourcegroep toocreate kiest, gebruikt u Hallo **locatie van resourcegroep** dropdown toospecify Hallo locatie van resourcegroep Hallo. Deze instelling verwijst toohello locatie van resourcegroep Hallo en heeft geen invloed op Hallo Traffic Manager-profiel dat globaal wordt geïmplementeerd.
    5. Nadat u op **maken**, uw Traffic Manager-profiel is gemaakt en geïmplementeerd globaal.

![Een Traffic Manager-profiel maken](./media/traffic-manager-geographic-routing-method/create-traffic-manager-profile.png)

## <a name="add-endpoints"></a>Het toevoegen van eindpunten

1. Zoeken naar Hallo Traffic Manager-profielnaam die u zojuist hebt gemaakt in de zoekbalk Hallo-portal en klik op Hallo resultaat wanneer deze wordt weergegeven.
2. Navigeer te**instellingen** -> **eindpunten** Hallo Traffic Manager-blade.
3. Klik op **toevoegen** tooshow hello **eindpunt toevoegen** blade.
3. In Hallo **eindpunten** blade, klikt u op **toevoegen** en in Hallo **eindpunt toevoegen** blade die wordt weergegeven, voltooi als volgt:
4. Selecteer **Type** afhankelijk van Hallo-type van het eindpunt dat u wilt toevoegen. Voor geografische routering profielen die worden gebruikt in productie, wordt aangeraden met behulp van geneste eindpunttypen met een onderliggende profiel met meer dan één eindpunt. Zie voor meer informatie [Veelgestelde vragen over geografische verkeersrouteringsmethoden](traffic-manager-FAQs.md).
5. Geef een **naam** waarop u wilt toorecognize dit eindpunt.
6. Bepaalde velden in deze blade is afhankelijk van Hallo-type van het eindpunt dat u wilt toevoegen:
    1. Als u een Azure-eindpunt toevoegt, selecteert u Hallo **resource doeltype** en Hallo **doel** op basis van Hallo resource gewenste toodirect verkeer naar
    2. Als u wilt toevoegen een **externe** eindpunt, bieden Hallo **FQDN-naam (Fully qualified domain name)** voor uw eindpunt.
    3. Als u wilt toevoegen een **geneste eindpunt**, selecteer Hallo **Doelresource** die overeenkomt met toohello onderliggende gewenste profiel toouse en geef Hallo **Minimum onderliggende eindpunten tellen**.
7. Gebruik Hallo vervolgkeuzelijst tooadd Hallo regio's waar u wilt dat verkeer toobe verzonden toothis eindpunt in Hallo sectie Geo-toewijzing. U moet ten minste één regio toevoegen en u kunt meerdere regio's die zijn toegewezen.
8. Herhaal deze stap voor alle eindpunten gewenste tooadd onder dit profiel

![Een Traffic Manager-eindpunt toevoegen](./media/traffic-manager-geographic-routing-method/add-traffic-manager-endpoint.png)

## <a name="use-hello-traffic-manager-profile"></a>Hallo Traffic Manager-profiel gebruiken
1.  Zoek in de zoekbalk Hallo-portal, op Hallo **Traffic Manager-profiel** naam dat u hebt gemaakt in de voorgaande sectie Hallo en klik op Hallo traffic manager-profiel in Hallo dat Hallo weergegeven resulteert.
2. In Hallo **Traffic Manager-profiel** blade, klikt u op **overzicht**.
3. Hallo **Traffic Manager-profiel** blade Hallo DNS-naam van de zojuist gemaakte Traffic Manager-profiel wordt weergegeven. Dit kan worden gebruikt door alle clients (bijvoorbeeld door te gaan met een webbrowser tooit) tooget gerouteerd toohello eindpunt rechts zoals wordt bepaald door de routeringstype Hallo.  In geval van geografische routering Hallo Traffic Manager bekijkt hello bron-IP voor inkomende hello-aanvraag en bepaalt Hallo regio van waaruit deze afkomstig is. Als deze regio toegewezen tooan eindpunt is, is het verkeer gerouteerde toothere. Als u deze regio is niet toegewezen tooan eindpunt, retourneert Traffic Manager een GEENGEGEVENS query-antwoord.

## <a name="next-steps"></a>Volgende stappen

- Meer informatie over [geografisch methode voor het doorsturen van verkeer](traffic-manager-routing-methods.md#geographic).
- Meer informatie over hoe te[Traffic Manager-instellingen testen](traffic-manager-testing-settings.md).
