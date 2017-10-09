---
title: dashboard van service Manager aaaStorSimple | Microsoft Docs
description: Beschrijving van dashboard voor Hallo StorSimple Manager-service en wordt uitgelegd hoe toouse het toomonitor Hallo status van uw StorSimple-oplossing.
services: storsimple
documentationcenter: 
author: SharS
manager: carmonm
editor: 
ms.assetid: fb0f131d-d60b-45d7-ace2-56d0502e6627
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/24/2016
ms.author: v-sharos
ms.openlocfilehash: dc1197eb5deac337215b260845631a4f04be1011
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-dashboard"></a>Hallo StorSimple Manager-service-dashboard gebruiken
## <a name="overview"></a>Overzicht
pagina dashboard Hallo StorSimple Manager-service biedt een overzicht van alle Hallo-apparaten die verbonden toohello StorSimple Manager-service zijn, die aandacht vereisen een systeembeheerder is gemarkeerd. In deze zelfstudie Hallo dashboardpagina introduceert, verklaart Hallo Dashboardinhoud en functie en Hallo worden taken beschreven die u op deze pagina uitvoeren kunt.

![Servicedashboard](./media/storsimple-service-dashboard/HCS_ServiceDashboard.png)

Hallo StorSimple Manager servicedashboard toont de Hallo volgende informatie:

* In Hallo **grafiek** gebied, ziet u de relevante meetgegevens Hallo grafiek voor uw apparaten. U kunt bekijken Hallo primaire opslag (lokaal vastgemaakt en lagen) gebruikt via alle apparaten hello, evenals Hallo cloud-opslag verbruikt door apparaten gedurende een periode. Gebruik Hallo besturingselementen in Hallo rechtsboven van Hallo grafiek toospecify een schaal 1 week, 1 maand, 3 maanden of 1 jaar.
* Hallo **overzicht gebruik** toont Hallo primaire opslag die is ingericht en gebruikt door alle apparaten relatieve toohello totale opslagruimte beschikbaar op alle apparaten. **Ingericht** toohello en de hoeveelheid opslagruimte die is voorbereid en toegewezen voor gebruik, terwijl verwijst **gebruikt** toousage van volumes verwijst, zoals weergegeven door het Hallo-initiators die verbonden toohello apparaten zijn.
* Hallo **waarschuwingen** gebied biedt een momentopname van alle actieve waarschuwingen van Hallo op alle apparaten hello, gegroepeerd op de ernst van waarschuwing. Ernst Hallo Hallo wordt geopend **waarschuwingen** pagina, binnen het bereik tooshow waarschuwingen. Op Hallo **waarschuwingen** pagina, klikt u op een afzonderlijke waarschuwing tooview aanvullende details over deze waarschuwing, met inbegrip van alle aanbevolen acties. U kunt ook een waarschuwing Hallo wissen als Hallo probleem is opgelost.
* Hallo **taken** gebied biedt een momentopname van recente taken op alle apparaten die zijn verbonden tooyour service. Er zijn koppelingen waarmee u kunt toolook op taken die momenteel worden uitgevoerd die is mislukt in Hallo afgelopen 24 uur, of die zijn gepland toorun in Hallo binnen 24 uur.
* Hallo **snelle weergave** gebied biedt nuttige informatie zoals de servicestatus, het aantal apparaten verbonden toohello service, de locatie van de service Hallo en details van Hallo-abonnement dat is gekoppeld aan Hallo-service. Er is ook een koppeling toohello operations logboek. Klik op Hallo koppeling toosee een lijst met alle voltooide StorSimple Manager servicebewerkingen.

U kunt Hallo StorSimple Manager service dashboard pagina tooinitiate Hallo taken te volgen:

* Weergeven of Hallo serviceregistratiesleutel genereren.
* De gegevensversleutelingssleutel van Hallo service wijzigen.
* Hallo bewerkingslogboeken weergeven.

## <a name="view-or-regenerate-hello-service-registration-key"></a>Weergeven of Hallo serviceregistratiesleutel genereren
Hallo-serviceregistratiesleutel is gebruikte tooregister een Microsoft Azure StorSimple-apparaat met Hallo StorSimple Manager-service, zodat hello apparaat wordt weergegeven in Hallo klassieke Azure-portal voor verdere acties. Hallo-sleutel is gemaakt op de eerste apparaat Hallo en gedeeld met Hallo rest van uw apparaten.

Te klikken op **registratiesleutel** (aan de onderkant van de Hallo van Hallo pagina) wordt geopend Hallo **Serviceregistratiesleutel** in het dialoogvenster u beide Hallo huidige service registratie sleutel toohello Klembord kopiëren kunt of Hallo-serviceregistratiesleutel genereren.

Opnieuw genereren Hallo-sleutel heeft geen invloed op eerder geregistreerde apparaten: is van invloed op Hallo alleen apparaten die zijn geregistreerd bij service Hallo nadat het Hallo-sleutel wordt opnieuw gegenereerd.

Voor meer informatie over het bekijken en te genereren van sleutels, gaat u Hallo service registratie[serviceregistratiesleutel ophalen-Hallo](storsimple-manage-service.md#get-the-service-registration-key).

## <a name="change-hello-service-data-encryption-key"></a>De gegevensversleutelingssleutel van Hallo service wijzigen
Sleutels voor gegevenscodering service zijn gebruikte tooencrypt vertrouwelijke gegevens van de klant, zoals opslagaccountreferenties, die worden verzonden vanuit uw StorSimple Manager service toohello StorSimple-apparaat. U moet toochange deze sleutels periodiek als uw IT-organisatie een beleid voor belangrijke draaien op Hallo opslagapparaten heeft. Hallo wijzigingsproces kan worden enigszins verschillen afhankelijk van of er is een apparaat met één of meerdere apparaten, beheerd door Hallo StorSimple Manager-service.

Gegevensversleutelingssleutel van veranderende Hallo-service is een proces 3-stappen:

1. Hallo klassieke Azure-portal gebruikt, een apparaat toochange Hallo service gegevensversleutelingssleutel autoriseren.
2. Met Windows PowerShell voor StorSimple, Hallo service encryption key gegevenswijziging initiëren.
3. Als u meer dan een StorSimple-apparaat hebt, bijwerken Hallo gegevensversleutelingssleutel van service op Hallo andere apparaten.

Hallo beschrijven volgende stappen Hallo overschakeling van de procedure voor het Hallo gegevensversleutelingssleutel van service.

[!INCLUDE [storsimple-change-data-encryption-key](../../includes/storsimple-change-data-encryption-key.md)]

## <a name="view-hello-operations-logs"></a>Hallo operations-logboeken bekijken
U kunt bewerkingslogboeken Hallo weergeven door te klikken op Hallo bewerking logboeken beschikbaar in Hallo **snelle weergave** deelvenster van het Hallo-dashboard. Hiermee gaat u toohello management servicepagina kunt u filteren en Zie Hallo registreert specifieke tooyour StorSimple Manager-service.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe te[oplossen van een StorSimple-apparaat](storsimple-troubleshoot-operational-device.md).
* Meer informatie over het te[gebruik Hallo StorSimple Manager service tooadminister uw StorSimple-apparaat](storsimple-manager-service-administration.md).

