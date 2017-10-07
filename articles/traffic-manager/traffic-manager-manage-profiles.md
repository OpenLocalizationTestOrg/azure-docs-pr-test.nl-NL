---
title: aaaManage Azure Traffic Manager-profielen | Microsoft Docs
description: In dit artikel wordt uitgelegd hoe u een Azure Traffic Manager-profiel maakt, uitschakelt, inschakelt en verwijdert.
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: f06e0365-0a20-4d08-b7e1-e56025e64f66
ms.service: traffic-manager
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/10/2017
ms.author: kumud
ms.openlocfilehash: 0c6ab0c451581d039514a9de0b525b3937e45a85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-traffic-manager-profile"></a>Een Azure Traffic Manager-profiel beheren

Traffic Manager-profielen gebruiken voor verkeersroutering methoden toocontrol Hallo distributie van verkeer tooyour cloudservices of website-eindpunten. Dit artikel wordt uitgelegd hoe toocreate en deze profielen beheren.

## <a name="create-a-traffic-manager-profile"></a>Een Traffic Manager-profiel maken

U kunt een Traffic Manager-profiel maken met behulp van hello Azure-portal. Nadat uw profiel is gemaakt, kunt u eindpunten, bewaking en andere instellingen kunt configureren in hello Azure-portal. Traffic Manager biedt ondersteuning voor maximaal too200 eindpunten per profiel. Voor de meeste gebruiksscenario's zijn echter slechts enkele eindpunten vereist.

### <a name="toocreate-a-traffic-manager-profile"></a>toocreate een Traffic Manager-profiel

1. Aanmelden via een browser toohello [Azure-portal](http://portal.azure.com). Als u nog geen account hebt, kunt u zich registreren voor een [gratis proefversie van één maand](https://azure.microsoft.com/free/). 
2. Op Hallo **Hub** menu, klikt u op **nieuw** > **Networking** > **alle**, klikt u op **verkeer Manager** profiel tooopen hello **maken Traffic Manager-profiel** blade, klikt u vervolgens op **maken**.
3. Op Hallo **maken Traffic Manager-profiel** blade voltooid zijn als volgt:
    1. In **Naam** geeft u een naam op voor het profiel. Deze naam moet uniek zijn binnen Hallo trafficmanager.net zone beschikken over toobe en resulteert in het Hallo DNS-naam <name>, trafficmanager.net die gebruikte tooaccess uw Traffic Manager-profiel.
    2. In **routeringsmethode**, selecteer Hallo **prioriteit** routeringsmethode.
    3. In **abonnement**, selecteert u dit profiel onder toocreate wilt Hallo-abonnement
    4. In **resourcegroep**, dit profiel onder een nieuwe resource groep tooplace maakt.
    5. In **locatie voor resourcegroep**, Hallo-locatie van resourcegroep Hallo selecteren. Deze instelling verwijst toohello locatie van resourcegroep Hallo en heeft geen invloed op Hallo Traffic Manager-profiel dat globaal wordt geïmplementeerd.
    6. Klik op **Create**.
    7. Wanneer de globale implementatie Hallo van uw Traffic Manager-profiel voltooid is, wordt het weergegeven in de betreffende resourcegroep als een van de Hallo resources.

## <a name="disable-enable-or-delete-a-profile"></a>Een profiel uitschakelen, inschakelen of verwijderen

U kunt een bestaand profiel uitschakelen zodat die Traffic Manager niet gebruiker aanvragen toohello geconfigureerd eindpunten verwijst. Wanneer u een Traffic Manager-profiel uitschakelt, Hallo profiel Hallo gegevens in Hallo profiel blijven behouden en kan worden bewerkt in Hallo Traffic Manager-interface.  Verwijzingen hervat wanneer u Hallo profiel voor het opnieuw inschakelen. Wanneer u een Traffic Manager-profiel in hello Azure-portal maakt, wordt automatisch ingeschakeld. Als u een profiel niet meer nodig hebt, kunt u het verwijderen.

### <a name="toodisable-a-profile"></a>een profiel toodisable

1. Als u van een aangepaste domeinnaam gebruikmaakt, wijzigt u Hallo CNAME-record op uw Internet-DNS-server zodanig dat deze niet langer tooyour Traffic Manager-profiel wijst.
2. Verkeer wordt niet meer toohello eindpunten via Hallo Traffic Manager-profielinstellingen omgeleid.
3. Aanmelden via een browser toohello [Azure-portal](http://portal.azure.com).
2. Zoek in de zoekbalk Hallo-portal, op Hallo **Traffic Manager-profiel** naam toomodify wilt en klik vervolgens op Hallo Traffic Manager-profiel in Hallo resulteert dat Hallo weergegeven.
3. In Hallo **Traffic Manager-profiel** blade, klikt u op **overzicht**, klik in de blade overzicht Hallo op **uitschakelen**, en Bevestig toodisable Hallo Traffic Manager-profiel.

### <a name="tooenable-a-profile"></a>een profiel tooenable

1. Aanmelden via een browser toohello [Azure-portal](http://portal.azure.com).
2. Zoek in de zoekbalk Hallo-portal, op Hallo **Traffic Manager-profiel** naam toomodify wilt en klik vervolgens op Hallo Traffic Manager-profiel in Hallo resulteert dat Hallo weergegeven.
3. In Hallo **Traffic Manager-profiel** blade, klikt u op **overzicht**, en klik in de blade overzicht Hallo klikt u op **inschakelen**.
5. Als u een aangepaste domeinnaam gebruikt, maakt u een CNAME-resourcerecord op uw Internet DNS-server toopoint toohello-domeinnaam van uw Traffic Manager-profiel.
6. Verkeer is gerichte toohello eindpunten opnieuw.

### <a name="toodelete-a-profile"></a>een profiel toodelete

1. Zorg ervoor dat Hallo DNS-resourcerecord op uw Internet DNS-server niet langer een CNAME-bronrecord die toohello domeinnaam van uw Traffic Manager-profiel wijst gebruikt.
2. Zoek in de zoekbalk Hallo-portal, op Hallo **Traffic Manager-profiel** naam toomodify wilt en klik vervolgens op Hallo Traffic Manager-profiel in Hallo resulteert dat Hallo weergegeven.
3. In Hallo **Traffic Manager-profiel** blade, klikt u op **overzicht**, klik in de blade overzicht Hallo op **verwijderen**, en Bevestig toodelete Hallo Traffic Manager-profiel.

## <a name="next-steps"></a>Volgende stappen

* [Een eindpunt toevoegen](traffic-manager-endpoints.md)
* [Routeringsmethode op basis van prioriteit configureren](traffic-manager-configure-priority-routing-method.md)
* [Routeringsmethode op basis van geografische locatie configureren](traffic-manager-configure-geographic-routing-method.md) 
* [Routeringsmethode op basis van gewogen distributie configureren](traffic-manager-configure-weighted-routing-method.md)
* [Routeringsmethode op basis van prestaties configureren](traffic-manager-configure-performance-routing-method.md)
