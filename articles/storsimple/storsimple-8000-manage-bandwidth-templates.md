---
title: aaaManage bandbreedte sjablonen voor StorSimple 8000-serie | Microsoft Docs
description: Hierin wordt beschreven hoe toomanage StorSimple bandbreedte sjablonen, waarmee u toocontrol bandbreedteverbruik wordt gereduceerd.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: ebcd1824d7bb9e4c235194c04edbfe8001a3e794
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-storsimple-bandwidth-templates"></a>Hallo Apparaatbeheer StorSimple toomanage StorSimple bandbreedte servicesjablonen gebruiken

## <a name="overview"></a>Overzicht

Bandbreedte-sjablonen kunt u gebruik van netwerkbandbreedte tooconfigure over meerdere schema's van de dag tootier Hallo gegevens van Hallo StorSimple-apparaat toohello cloud.

Met de schema's voor bandbreedteregeling kunt u:

* Aangepaste bandbreedte's afhankelijk van Hallo werkbelasting netwerk gebruik opgeven.
* Management centraliseren en Hallo schema's op meerdere apparaten in een eenvoudig en naadloos manier opnieuw gebruiken.

> [!NOTE]
> Deze functie is alleen beschikbaar voor fysieke StorSimple-apparaten (modellen 8100 en 8600) en niet voor StorSimple Cloud toestellen (modellen 8010 als de 8020).


## <a name="hello-bandwidth-templates-blade"></a>Hallo bandbreedte sjablonen blade

Hallo **bandbreedte sjablonen** blade alle Hallo bandbreedte sjablonen voor uw service in tabelvorm en bevat Hallo volgende informatie:

* **Naam** : een unieke naam toegewezen toohello bandbreedtesjabloon wanneer deze is gemaakt.
* **Planning** – Hallo aantal schema's die zijn opgenomen in een bandbreedtesjabloon opgegeven.
* **Gebruikt door** – Hallo aantal volumes met behulp van Hallo bandbreedte sjablonen.

U kunt ook aanvullende informatie toohelp bandbreedte sjablonen configureren vinden in:

* [Vragen en antwoorden over de bandbreedte-sjablonen](#questions-and-answers-about-bandwidth-templates)
* [Aanbevolen procedures voor de bandbreedte-sjablonen](#best-practices-for-bandwidth-templates)

## <a name="add-a-bandwidth-template"></a>Voeg een bandbreedtesjabloon

Voer Hallo toocreate stappen een nieuwe bandbreedtesjabloon te volgen.

#### <a name="tooadd-a-bandwidth-template"></a>tooadd bandbreedtesjabloon

1. Ga tooyour Apparaatbeheer StorSimple-service, klikt u op **bandbreedte sjablonen** en klik vervolgens op **+ bandbreedtesjabloon toevoegen**.

    ![Klik op + bandbreedtesjabloon toevoegen](./media/storsimple-8000-manage-bandwidth-templates/addbwtemp1.png)

2. In Hallo **bandbreedtesjabloon toevoegen** blade Hallo volgende stappen:
   
    1. Geef een unieke naam voor de bandbreedtesjabloon.
    2. Een schema bandbreedte definiëren. een planning toocreate:
   
        1. Kies in de vervolgkeuzelijst hello, Hallo **dagen** Hallo week Hallo planning is geconfigureerd voor. U kunt meerdere dagen selecteren.        
        
        2. Voer een **begintijd** in _uu: mm_ indeling. Dit is wanneer het Hallo-planning wordt gestart.

        3. Voer een **eindtijd** in _uu: mm_ indeling. Dit is wanneer het Hallo-planning wordt gestopt.
      
           > [!NOTE]
           > Overlappende schema's zijn niet toegestaan. Als hello begin- en eindtijden in een overlappende planning resulteren zal, ziet u een fout bericht toothat effect.

        4. Geef Hallo **bandbreedte snelheid**. Dit is Hallo bandbreedte in Megabits per seconde (Mbps) die wordt gebruikt door uw StorSimple-apparaat in bewerkingen met betrekking tot Hallo cloud (uploads en downloads). Geef een getal tussen 1 en 1000 voor dit veld.

            ![Bandbreedte-schema definiëren](./media/storsimple-8000-manage-bandwidth-templates/addbwtemp2.png)
         
            Herhaal de Hallo bovenstaande stappen toodefine meerdere planningen voor de sjabloon totdat u klaar bent.

        5. Klik op **toevoegen** toostart maken van een bandbreedtesjabloon. Hallo sjabloon hebt gemaakt, toohello lijst met sjablonen van de bandbreedte wordt toegevoegd.
      

## <a name="edit-a-bandwidth-template"></a>Een bandbreedtesjabloon bewerken

Volgende stappen tooedit bandbreedtesjabloon Hallo uitvoeren.

### <a name="tooedit-a-bandwidth-template"></a>tooedit bandbreedtesjabloon

1. Ga tooyour Apparaatbeheer StorSimple-service en klik op **bandbreedte sjablonen**.
2. Selecteer Hallo-sjabloon die u wenst dat toodelete in Hallo lijst met sjablonen van de bandbreedte. Met de rechtermuisknop en selecteer in het contextmenu hello, **verwijderen**.
3. Wanneer u om bevestiging gevraagd, klikt u op **OK**. Dit moet Hallo bandbreedtesjabloon verwijderen. 
4. Hallo-lijst van bandbreedte sjablonen updates tooreflect Hallo verwijdering.

> [!NOTE]
> U kunt uw wijzigingen niet opslaan als Hallo bewerkt planning overlapt met een bestaand schema in Hallo bandbreedtesjabloon die u wilt wijzigen.

## <a name="delete-a-bandwidth-template"></a>Een bandbreedtesjabloon verwijderen

Volgende stappen toodelete bandbreedtesjabloon Hallo uitvoeren.

#### <a name="toodelete-a-bandwidth-template"></a>toodelete bandbreedtesjabloon

1. Ga tooyour Apparaatbeheer StorSimple-service en klik op **bandbreedte sjablonen**.
2. Selecteer Hallo-sjabloon die u wenst dat toodelete in Hallo lijst met sjablonen van de bandbreedte. Klik met de rechtermuisknop en selecteer in het contextmenu hello, verwijderen.
3. Wanneer u om bevestiging gevraagd, klikt u op **OK**. Dit moet Hallo bandbreedtesjabloon verwijderen.
4. Hallo-lijst van bandbreedte sjablonen updates tooreflect Hallo verwijdering.

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

**EEN**. Stel dat u een apparaat met 3 volumecontainers hebben. Hallo schema's die zijn gekoppeld aan deze containers volledig elkaar overlappen. Voor elk van deze containers zijn Hallo bandbreedte gebruikt 5, 10 en 15 Mbps respectievelijk. Wanneer de i/o zich voordoen op al deze containers op Hallo tegelijkertijd Hallo minimum van bandbreedtelimieten Hallo 3 kan worden toegepast: in dit geval 5 Mbps als deze uitgaande i/o-aanvragen delen dezelfde wachtrij Hallo.

## <a name="best-practices-for-bandwidth-templates"></a>Aanbevolen procedures voor de bandbreedte-sjablonen

Volg deze aanbevolen procedures voor uw StorSimple-apparaat:

* Bandbreedte-sjablonen op uw apparaat tooenable variabele beperken van de netwerkdoorvoer Hallo door Hallo apparaat op verschillende tijdstippen Hallo configureren. Deze sjablonen bandbreedte gebruikt in combinatie met de back-upschema's kunnen effectief gebruikmaken van aanvullende netwerkbandbreedte voor cloud-bewerkingen tijdens de daluren.
* Hallo werkelijke bandbreedte die vereist zijn voor een bepaalde implementatie op basis van de grootte Hallo Hallo-implementatie en Hallo vereist beoogde hersteltijd (RTO) berekenen.

## <a name="next-steps"></a>Volgende stappen

Meer informatie over [StorSimple Apparaatbeheer service tooadminister uw StorSimple-apparaat met behulp van Hallo](storsimple-8000-manager-service-administration.md).

