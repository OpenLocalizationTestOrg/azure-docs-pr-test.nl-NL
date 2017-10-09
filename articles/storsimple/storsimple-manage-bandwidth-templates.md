---
title: aaaManage uw StorSimple-bandbreedte-sjablonen | Microsoft Docs
description: Hierin wordt beschreven hoe toomanage StorSimple bandbreedte sjablonen, waarmee u toocontrol bandbreedteverbruik wordt gereduceerd.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 0027b90e-91a5-437d-9bd0-06b05674aa5f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2016
ms.author: alkohli
ms.openlocfilehash: 3f767e985667121e977106e7a1f8e5a3ad25f022
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-storsimple-bandwidth-templates"></a>Hallo StorSimple Manager toomanage StorSimple bandbreedte servicesjablonen gebruiken
## <a name="overview"></a>Overzicht
Bandbreedte-sjablonen kunt u gebruik van netwerkbandbreedte tooconfigure over meerdere schema's van de dag tootier Hallo gegevens van Hallo StorSimple-apparaat toohello cloud.

Met de schema's voor bandbreedteregeling kunt u:

* Aangepaste bandbreedte's afhankelijk van Hallo werkbelasting netwerk gebruik opgeven.
* Management centraliseren en Hallo schema's op meerdere apparaten in een eenvoudig en naadloos manier opnieuw gebruiken.

> [!NOTE]
> Deze functie is alleen beschikbaar voor fysieke StorSimple-apparaten en niet voor virtuele apparaten.
> 
> 

Alle Hallo bandbreedte sjablonen voor uw service worden weergegeven in tabelvorm en Hallo volgende informatie bevatten:

* **Naam** : een unieke naam toegewezen toohello bandbreedtesjabloon wanneer deze is gemaakt.
* **Planning** – Hallo aantal schema's die zijn opgenomen in een bandbreedtesjabloon opgegeven.
* **Gebruikt door** – Hallo aantal volumes met behulp van Hallo bandbreedte sjablonen.

Gebruik van de StorSimple Manager-service Hallo **configureren** pagina in hello Azure classic portal toomanage bandbreedte sjablonen.

U kunt ook aanvullende informatie toohelp bandbreedte sjablonen configureren vinden in:

* Vragen en antwoorden over de bandbreedte-sjablonen
* Aanbevolen procedures voor de bandbreedte-sjablonen

## <a name="add-a-bandwidth-template"></a>Voeg een bandbreedtesjabloon
Voer Hallo toocreate stappen een nieuwe bandbreedtesjabloon te volgen.

#### <a name="tooadd-a-bandwidth-template"></a>tooadd bandbreedtesjabloon
1. Op Hallo StorSimple Manager-service **configureren** pagina, klikt u op **bandbreedtesjabloon toevoegen/bewerken**.
2. In Hallo **Bandbreedtesjabloon toevoegen/bewerken** in het dialoogvenster:
   
   1. Van Hallo **sjabloon** vervolgkeuzelijst, selecteer **nieuw** tooadd een nieuwe bandbreedtesjabloon.
   2. Geef een unieke naam voor de bandbreedtesjabloon.
3. Definieer een **bandbreedte planning**. een planning toocreate:
   
   1. Vervolgkeuzelijst hello, kies Hallo dagen Hallo week Hallo schema is geconfigureerd voor. U kunt meerdere dagen selecteren door de selectievakjes Hallo zich vóór de respectieve dagen in de lijst Hallo Hallo in te schakelen.
   2. Selecteer Hallo **alle dag** optie Hallo planning voor de hele dag hello wordt afgedwongen. Wanneer deze optie is ingeschakeld, kunt u niet langer opgeven een **begintijd** of een **eindtijd**. Hallo planning wordt uitgevoerd vanaf 00:00 uur too11: 59 PM.
   3. Selecteer in de vervolgkeuzelijst hello, een **begintijd**. Dit is wanneer het Hallo-planning wordt gestart.
   4. Selecteer in de vervolgkeuzelijst hello, een **eindtijd**. Dit is wanneer het Hallo-planning wordt gestopt.
      
      > [!NOTE]
      > Overlappende schema's zijn niet toegestaan. Als hello begin- en eindtijden in een overlappende planning resulteren zal, ziet u een fout bericht toothat effect.
      > 
      > 
   5. Geef Hallo **bandbreedte snelheid**. Dit is Hallo bandbreedte in Megabits per seconde (Mbps) die wordt gebruikt door uw StorSimple-apparaat in bewerkingen met betrekking tot Hallo cloud (uploads en downloads). Geef een getal tussen 1 en 1000 voor dit veld.
   6. Klik op het vinkje Hallo ![vinkje](./media/storsimple-manage-bandwidth-templates/HCS_CheckIcon.png). Hallo-sjabloon die u hebt gemaakt wordt toegevoegd toohello lijst met sjablonen van de bandbreedte op Hallo service **configureren** pagina.
      
      ![Nieuwe bandbreedtesjabloon maken](./media/storsimple-manage-bandwidth-templates/HCS_CreateNewBT1.png)
4. Klik op **opslaan** onderin Hallo Hallo pagina en klik vervolgens op **Ja** wanneer u om bevestiging wordt gevraagd. Dit bespaart Hallo configuratiewijzigingen die u hebt aangebracht.

## <a name="edit-a-bandwidth-template"></a>Een bandbreedtesjabloon bewerken
Volgende stappen tooedit bandbreedtesjabloon Hallo uitvoeren.

### <a name="tooedit-a-bandwidth-template"></a>tooedit bandbreedtesjabloon
1. Klik op **bandbreedtesjabloon toevoegen/bewerken**.
2. In Hallo **Bandbreedtesjabloon toevoegen/bewerken** in het dialoogvenster:
   
   1. Van Hallo **sjabloon** vervolgkeuzelijst kiest u een bestaande bandbreedte sjabloon dat u wilt dat toomodify.
   2. Voer de wijzigingen. (U kunt wijzigen van de bestaande instellingen Hallo.)
   3. Klik op het vinkje Hallo ![Vinkje](./media/storsimple-manage-bandwidth-templates/HCS_CheckIcon.png). Hallo gewijzigde sjabloon in de lijst Hallo van bandbreedte sjablonen ziet u op de pagina configureren van Hallo-service.
3. Klik op toosave uw wijzigingen **opslaan** Hallo Hallo pagina onderaan in. Klik op **Ja** wanneer u om bevestiging wordt gevraagd.

> [!NOTE]
> U wordt niet toegestaan toosave uw wijzigingen als Hallo bewerkte planning met een bestaande overlapt in Hallo bandbreedtesjabloon plannen dat u wilt wijzigen.
> 
> 

## <a name="delete-a-bandwidth-template"></a>Een bandbreedtesjabloon verwijderen
Volgende stappen toodelete bandbreedtesjabloon Hallo uitvoeren.

#### <a name="toodelete-a-bandwidth-template"></a>toodelete bandbreedtesjabloon
1. Selecteer Hallo sjabloon dat u wenst dat toodelete in Hallo in tabelvorm lijst van Hallo bandbreedte sjablonen voor uw service. Een verwijderpictogram (**x**) toohello uiterst rechts van de geselecteerde sjabloon hello wordt weergegeven. Klik op Hallo **x** pictogram toodelete Hallo sjabloon.
2. U wordt gevraagd om bevestiging. Klik op **OK** tooproceed.

Als het Hallo-sjabloon is door een of meer volumes gebruikt, u pas weer toegestaan toodelete deze. U ziet een foutmelding dat die sjabloon hello wordt gebruikt. Het dialoogvenster met een foutbericht wordt weergegeven waarin wordt gemeld dat alle Hallo verwijzingen toohello sjabloon moet worden verwijderd.

U kunt alle Hallo verwijzingen toohello sjabloon verwijderen door het openen van Hallo **Volumecontainers** pagina en wijzigen van Hallo volumecontainers die gebruikmaken van deze sjabloon, zodat ze een andere sjabloon gebruiken of een aangepaste of onbeperkte bandbreedte gebruiken instelling. Als alle Hallo verwijzingen zijn verwijderd, kunt u Hallo sjabloon verwijderen.

## <a name="use-a-default-bandwidth-template"></a>Een standaardsjabloon voor bandbreedte
Een standaardsjabloon voor de bandbreedte wordt geleverd en wordt gebruikt door volumecontainers door standaard tooenforce bandbreedte besturingselementen bij het openen van Hallo cloud. Hallo standaardsjabloon fungeert ook als een verwijzing gereed is voor gebruikers die hun eigen sjablonen maken. Hallo-details van deze standaardsjabloon zijn:

* **Naam** : onbeperkte nachten en weekends
* **Planning** – één schema van maandag tooFriday die van toepassing een hoeveelheid bandbreedte van 1 Mbps tussen de 8 uur en 17: 00 uur tijd op het apparaat is. Hallo bandbreedte is tooUnlimited Hallo rest van Hallo week ingesteld.

Hallo standaardsjabloon kan worden bewerkt. Hallo informatie over het gebruik van deze sjabloon (inclusief bewerkte versies) wordt bijgehouden.

## <a name="create-an-all-day-bandwidth-template-that-starts-at-a-specified-time"></a>Een hele bandbreedtesjabloon maken die bij een opgegeven periode begint
Volg deze procedure toocreate een schema dat begint bij een opgegeven periode en alle dag wordt uitgevoerd. In voorbeeld Hallo Hallo planning begint bij 9: 00 uur in de ochtend Hallo en wordt uitgevoerd tot en met 9: 00 uur Hallo volgende ochtend. Het is belangrijk toonote die Hallo start en eindtijden voor een opgegeven schema moeten beide zijn opgenomen op Hallo dezelfde 24-uurs plannen en kan geen gegevens voor meerdere dagen. Als u tooset bandbreedte sjablonen in meerdere dagen moet, moet u toouse meerdere schema's (zoals weergegeven in Hallo voorbeeld).

#### <a name="toocreate-an-all-day-bandwidth-template"></a>een bandbreedtesjabloon voor de hele dag toocreate
1. Maak een planning die begint bij 9: 00 uur in de ochtend Hallo en tot middernacht uitgevoerd.
2. Voeg een ander schema toe. Het tweede planning toorun Hallo van middernacht tot en met 9: 00 uur in de ochtend Hallo configureren.
3. Hallo bandbreedtesjabloon opslaan.

samengesteld schema Hallo vervolgens starten op een tijdstip van uw keuze en hele dag worden uitgevoerd.

## <a name="questions-and-answers-about-bandwidth-templates"></a>Vragen en antwoorden over de bandbreedte-sjablonen
**Q**. Wat gebeurt er toobandwidth besturingselementen wanneer u Between Hallo schema's bent? (Een schema is beëindigd en een andere is nog niet gestart.)

**EEN**. In dergelijke gevallen wordt geen bandbreedte besturingselementen worden gebruikt. Dit betekent dat apparaat Hallo onbeperkte bandbreedte kunt gebruiken wanneer gegevens toohello cloud tiering.

**Q**. Kunt u bandbreedte sjablonen op een apparaat offline wijzigen?

**EEN**. U zich niet kunnen toomodify bandbreedte sjablonen op volumes containers als Hallo bijbehorende apparaat offline is.

**Q**. Kunt u een bandbreedtesjabloon voor die is gekoppeld aan een volumecontainer wanneer Hallo gekoppeld volumes offline zijn bewerken?

**EEN**. U kunt een bandbreedtesjabloon voor die is gekoppeld aan een volumecontainer waarvan volumes offline zijn wijzigen. Houd er rekening mee dat wanneer volumes offline zijn, geen gegevens zal worden geschakeld vanaf Hallo apparaat toohello cloud.

**Q**. Kunt u een standaardsjabloon verwijderen?

**EEN**. Hoewel u een standaardsjabloon verwijderen kunt, is het niet een goed idee toodo dus. Hallo-gebruik van een standaardsjabloon, inclusief bewerkte versies wordt bijgehouden. Hallo traceringsgegevens is geanalyseerd en is in de loop van de Hallo van tijd, gebruikte tooimprove Hallo standaardsjabloon.

**Q**. Hoe bepaal u dat uw bandbreedte sjablonen toobe gewijzigd moeten?

**EEN**. Een van de Hallo tekenen dat u nodig hebt toomodify Hallo bandbreedte sjablonen is wanneer u begint ziet Hallo netwerk vertragen of onderdrukking meerdere keren in een dag. Als dit gebeurt, bewaken Hallo-opslag- en gebruiksgegevens netwerk bekijkt hello i/o-prestaties en netwerkdoorvoer grafieken.

Van gegevens van het Hallo netwerk doorvoer Hallo-tijd van de dag identificeren en Hallo volumecontainers in welke Hallo netwerk knelpunt optreedt. Als dit gebeurt wanneer gegevens gelaagde toohello cloud worden er (deze gegevens ophalen uit i/o-prestaties voor alle volumecontainers voor apparaat toocloud), moet u toomodify Hallo bandbreedte sjablonen die zijn gekoppeld aan uw volumecontainers.

Nadat u Hallo gewijzigd sjablonen worden gebruikt, moet u toomonitor Hallo netwerk opnieuw voor aanzienlijke latenties. Als deze nog steeds bestaan, vervolgens moet u toorevisit uw sjablonen bandbreedte.

**Q**. Wat gebeurt er als meerdere volumecontainers op mijn apparaat plant die elkaar overlappen, maar andere beperkingen gelden tooeach?

**EEN**. Stel dat u een apparaat met 3 volumecontainers hebben. Hallo schema's die zijn gekoppeld aan deze containers volledig elkaar overlappen. Voor elk van deze containers zijn Hallo bandbreedte gebruikt 5, 10 en 15 Mbps respectievelijk. Wanneer de i/o's zich voordoen op al deze containers op Hallo tegelijkertijd Hallo minimum van bandbreedtelimieten Hallo 3 kan worden toegepast: in dit geval 5 Mbps als deze uitgaande i/o-aanvragen delen dezelfde wachtrij Hallo.

## <a name="best-practices-for-bandwidth-templates"></a>Aanbevolen procedures voor de bandbreedte-sjablonen
Volg deze aanbevolen procedures voor uw StorSimple-apparaat:

* Bandbreedte-sjablonen op uw apparaat tooenable variabele beperken van de netwerkdoorvoer Hallo door Hallo apparaat op verschillende tijdstippen Hallo configureren. Deze sjablonen bandbreedte gebruikt in combinatie met de back-upschema's kunnen effectief gebruikmaken van aanvullende netwerkbandbreedte voor cloud-bewerkingen tijdens de daluren.
* Hallo werkelijke bandbreedte die vereist zijn voor een bepaalde implementatie op basis van de grootte Hallo Hallo-implementatie en Hallo vereist beoogde hersteltijd (RTO) berekenen.

## <a name="next-steps"></a>Volgende stappen
Meer informatie over [StorSimple Manager service tooadminister uw StorSimple-apparaat met behulp van Hallo](storsimple-manager-service-administration.md).

