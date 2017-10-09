---
title: een StorSimple-volume van back-up aaaRestore | Microsoft Docs
description: Legt uit hoe toouse Hallo StorSimple Manager service back-upcatalogus pagina toorestore een StorSimple-volume vanuit een back-upset.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 6f289c39-96c7-4d57-b68a-4bc2e99aef9d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 03/22/2017
ms.author: alkohli
ms.openlocfilehash: c2e38765e750749f5764b5cbf2167d3cd5edfe5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set-update-2"></a>Een StorSimple-volume herstelt vanuit een back-upset (Update 2)
[!INCLUDE [storsimple-version-selector-restore-from-backup](../../includes/storsimple-version-selector-restore-from-backup.md)]

## <a name="overview"></a>Overzicht
Hallo **back-upcatalogus** pagina wordt weergegeven voor alle Hallo back-upsets die worden gemaakt wanneer de handmatige of automatische back-ups worden gemaakt. Gebruik deze pagina toolist en back-ups beheren, terugzetten vanaf een back-upset of een volume klonen.

 ![Back-pagina van de catalogus](./media/storsimple-restore-from-backup-set-u2/restore.png)

Deze zelfstudie wordt uitgelegd hoe toouse hello **back-upcatalogus** pagina toorestore uw apparaat bij een back-upset.

U kunt een volume van een lokale of de cloud back-up herstellen. In beide gevallen brengt herstelbewerking Hallo Hallo volume online onmiddellijk tijdens het downloaden van gegevens op de achtergrond Hallo. 

## <a name="before-you-restore"></a>Voordat u herstellen
Voordat u een herstelbewerking start, moet u zich bewust zijn van Hallo volgende voorbehoud:

* **Hallo volume offline halen** : Hallo volume offline nemen op beide Hallo-host en Hallo apparaat voordat u Hallo restore-bewerking starten. Hoewel Hallo volume online Hallo restore-bewerking automatisch op Hallo-apparaat brengt, moet u handmatig Hallo apparaat online brengt op Hallo host. U kunt Hallo volume online zetten op de host Hallo wanneer Hallo volume online op Hallo-apparaat. (U hoeft niet toowait tot Hallo restore-bewerking is voltooid.) Voor procedures gaat te[offline zetten van een volume](storsimple-manage-volumes-u2.md#take-a-volume-offline).
* **Na het terugzetten van het volumetype** – verwijderde volumes zijn hersteld op basis van het type in momentopname Hallo Hallo. Volumes die lokaal zijn vastgemaakt worden teruggezet als lokaal vastgemaakte volumes en volumes die zijn lagen worden teruggezet als gelaagde volumes.
  
    Voor bestaande volumes overschrijft de huidige gebruikstype Hallo van Hallo volume Hallo-type dat is opgeslagen in momentopname Hallo. Bijvoorbeeld, als u een volume vanuit een momentopname die is uitgevoerd herstelt wanneer het Hallo-volumetype is gelaagd en volumetype nu is lokaal vastgemaakt (vervaldatum tooa conversiebewerking), en vervolgens Hallo volume als een lokaal vastgemaakt volume is teruggezet. Op dezelfde manier als een bestaand lokaal vastgemaakt volume wordt uitgebreid en vervolgens wordt teruggezet vanuit een momentopname van een oudere uitgevoerd wanneer het Hallo-volume is kleiner, behoudt hello herstelde volume Hallo huidige uitgevouwen grootte.
  
    U kunt een volume kan niet converteren van een gelaagd volume tooa lokaal vastgemaakt volume of _omgekeerd_ tijdens het Hallo-volume wordt hersteld. Wacht totdat het Hallo restore-bewerking is voltooid en vervolgens kunt u Hallo volume tooanother type converteren. Voor informatie over het converteren van een volume gaat te[Hallo volumetype wijzigen](storsimple-manage-volumes-u2.md#change-the-volume-type). 
* **Hallo volumegrootte komt tot uiting in Hallo hersteld volume** – dit is een belangrijk aandachtspunt als u een lokaal vastgemaakt volume dat is verwijderd (omdat lokaal vastgemaakte volumes zijn volledig is ingericht) wilt herstellen. Zorg ervoor dat u over voldoende ruimte beschikken voordat u de toorestore een lokaal vastgemaakt volume die eerder is verwijderd. 
* **U kunt een volume niet uitbreiden wanneer deze wordt hersteld** : wacht totdat Hallo restore-bewerking is voltooid voordat u de tooexpand Hallo volume. Voor informatie over het uitbreiden van een volume gaat te[wijzigen van een volume](storsimple-manage-volumes-u2.md#modify-a-volume).
* **U kunt een back-up uitvoeren terwijl u een lokaal volume herstelt** – voor procedures te gaat[hello StorSimple Manager-service toomanage back-upbeleid gebruiken](storsimple-manage-backup-policies.md).
* **U kunt een herstelbewerking annuleren** : als u hersteltaak hello, annuleert en vervolgens Hallo volume wordt teruggedraaid toohello staat waarin deze zich bevond voordat u Hallo terugzetten gestart. Voor procedures gaat te[een taak annuleren](storsimple-manage-jobs-u2.md#cancel-a-job).

## <a name="how-does-restore-work"></a>Hoe werk herstellen
Voor apparaten met Update 4 of hoger, is heatmap-herstelfuncties geïmplementeerd. Zoals aanvragen Hallo-tooaccess hostgegevens Hallo-apparaat bereiken, wordt deze aanvragen worden bijgehouden en een heatmap wordt gemaakt. Hoog percentage resulteert in gegevenssegmenten met hogere hitte dat lagere aanvraagsnelheid toochunks met lagere hitte vertaalt. U moet toegang tot Hallo gegevens ten minste tweemaal toobe gemarkeerd als _hot_. Een bestand dat wordt gewijzigd ook is gemarkeerd als _hot_. Zodra u Hallo herstel start, treedt er proactieve hydratie van gegevens op op basis van Hallo heatmap. Voor versies eerder dan Update 4 Hallo gegevens is gedownload tijdens het terugzetten op basis van alleen toegang. 

Op basis van Heatmap bijhouden is ingeschakeld, alleen voor volumes gelaagde en lokaal vastgemaakte volumes worden niet ondersteund. Heatmap-herstelfuncties wordt ook niet ondersteund bij het klonen van een volumeapparaat tooanother. Als er een in-place herstellen en een lokale momentopname voor Hallo volume toobe hersteld op Hallo-apparaat bestaat, komen klikt u vervolgens we niet rehydrate (zoals gegevens al lokaal beschikbaar is). Standaard, wanneer u herstelt, zijn Hallo rehydratering taken gestart die gegevens op basis van Hallo heatmap proactief rehydrate. In Update 4 Windows PowerShell-cmdlets gebruikt tooquery rehydratering taken uitgevoerd worden, een rehydratering taak annuleren en Hallo status Hallo rehydratering taak ophalen.

* `Get-HcsRehydrationJob`-Deze cmdlet Hallo status van Hallo rehydratering taak opgehaald. Een taak één rehydratering wordt geactiveerd voor één volume.
* `Set-HcsRehydrationJob`-Deze cmdlet kunt u toopause, stoppen, hervatten Hallo rehydratering taak als Hallo rehydratering wordt uitgevoerd. 

Voor meer informatie over rehydratering cmdlets gaat te[naslaginformatie over Windows PowerShell-cmdlets voor StorSimple](https://technet.microsoft.com/library/dn688168.aspx).

Met automatische rehdyration wordt doorgaans hogere prestaties voor de tijdelijke lezen verwacht. Hallo werkelijke magniutde van verbeteringen is afhankelijk van verschillende factoren zoals toegangstijden en gegevensverloop gegevenstype. een taak rehydratering toocancel, kunt u Hallo PowerShell-cmdlet. Als u toopermanently uitschakelen rehydratering taken voor alle toekomstige Hallo-herstelt wenst, moet u contact op met Microsoft Support.

## <a name="how-toouse-hello-backup-catalog"></a>Hoe toouse Hallo back-upcatalogus
Hallo **back-upcatalogus** pagina vindt u een query waarmee u toonarrow uw selectie back-upset. U kunt Hallo back-upsets die worden opgehaald op basis van de volgende parameters Hallo filteren:

* **Apparaat** – Hallo-apparaat op welke Hallo back-upset is gemaakt.
* **Back-up maken van beleid** of **volume** – Hallo back-upbeleid of volume dat is gekoppeld aan deze back-upset.
* **Van** en **naar** – Hallo bereik datum en tijd wanneer Hallo back-upset is gemaakt.

Hallo gefilterde back-upsets worden vervolgens in een tabel weergegeven op basis van Hallo volgende kenmerken:

* **Naam** – hello naam van back-upbeleid Hallo of volumes die zijn gekoppeld aan de back-upset Hallo.
* **De grootte van** – werkelijke grootte van de back-upset Hallo Hallo.
* **Gemaakt op** : Hallo datum en tijd waarop Hallo back-ups zijn gemaakt. 
* **Type** – sets van back-up kunnen worden lokale momentopnamen of cloud worden opgeslagen. Een lokale momentopname is een back-up van alle uw worden lokaal opgeslagen volumegegevens op Hallo-apparaat. Een cloudmomentopname verwijst toohello back-up van volumegegevens in de cloud Hallo. Lokale momentopnamen bieden sneller toegang terwijl cloudmomentopnamen voor gegevenstolerantie worden gekozen.
* **Gestart door** – Hallo back-ups worden geïnitieerd automatisch volgens tooa schema of handmatig. (U kunt een back-upbeleid tooschedule back-ups. U kunt ook hello gebruiken **back-up maken** optie tootake een interactieve back-up.)

## <a name="how-toorestore-your-storsimple-volume-from-a-backup"></a>Hoe toorestore uw StorSimple-volume van een back-up
U kunt Hallo **back-upcatalogus** pagina toorestore uw StorSimple-volume van een specifieke back-up. Houd er echter rekening mee, dat het herstellen van een volume wordt teruggezet Hallo volume toohello status toen Hallo back-up is gemaakt. Alle gegevens die zijn toegevoegd na de back-upbewerking Hallo gaat verloren.

> [!WARNING]
> Terugzetten vanuit een back-up vervangt bestaande volumes Hallo van Hallo back-up. Hierdoor kunnen Hallo verlies van gegevens die is geschreven nadat Hallo back-up is gemaakt.
> 
> 

### <a name="toorestore-your-volume"></a>toorestore uw volume
1. Klik op de pagina van de StorSimple Manager service hello, Hallo **back-upcatalogus** tabblad.
   
    ![Back-upcatalogus](./media/storsimple-restore-from-backup-set-u2/restore.png)
2. Selecteer een back-up als volgt instellen:
   
   1. Selecteer het juiste apparaat Hallo.
   2. Kies in de vervolgkeuzelijst hello, Hallo volume of back-up beleid voor back-up Hallo gewenste tooselect.
   3. Hallo tijdsperiode opgeven.
   4. Klik op het vinkje Hallo ![vinkje](./media/storsimple-restore-from-backup-set-u2/HCS_CheckIcon.png) tooexecute deze query.
      
      Hallo back-ups die zijn gekoppeld aan Hallo geselecteerd volume of back-up beleid moeten worden weergegeven in de lijst Hallo van back-upsets.
3. Vouw Hallo back-upset tooview Hallo gekoppeld volumes. Deze volumes moeten op Hallo host en het apparaat offline worden genomen voordat u ze kunt herstellen. Toegang tot Hallo volumes op Hallo **Volumecontainers** pagina en volg de stappen in Hallo [offline zetten van een volume](storsimple-manage-volumes-u2.md#take-a-volume-offline) tootake ze offline.
   
   > [!IMPORTANT]
   > Zorg ervoor dat u hebt ondernomen Hallo volumes offline op Hallo host eerst voordat u Hallo volumes offline op Hallo-apparaat nemen. Als u niet Hallo volumes offline op Hallo host nemen, kan deze toodata beschadiging leiden.
   > 
   > 
4. Navigeer terug toohello **back-upcatalogus** tabblad en selecteert u een back-upset.
5. Klik op **herstellen** Hallo Hallo pagina onderaan in.
6. U wordt gevraagd om bevestiging. Bekijk Hallo gegevens herstellen, en selecteer vervolgens Hallo bevestiging selectievakje.
   
    ![Bevestigingspagina](./media/storsimple-restore-from-backup-set-u2/ConfirmRestore.png)
7. Klik op het vinkje Hallo ![vinkje](./media/storsimple-restore-from-backup-set-u2/HCS_CheckIcon.png). Een hersteltaak begint. U kunt Hallo-taak weergeven door het openen van Hallo **taken** pagina. 
8. Nadat het Hallo herstellen is voltooid, kunt u controleren dat Hallo inhoud van uw volumes worden vervangen door de volumes van Hallo back-up.

![Video beschikbaar](./media/storsimple-restore-from-backup-set-u2/Video_icon.png) **Video beschikbaar**

toowatch een video die u laat zien hoe gebruikt u de Hallo klonen en herstellen van functies in StorSimple toorecover verwijderde bestanden, klikt u op [hier](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).

## <a name="if-hello-restore-fails"></a>Als Hallo herstellen mislukt
U ontvangt een waarschuwing als Hallo herstelbewerking mislukt voor een of andere reden. Als dit gebeurt, is vernieuwen Hallo back-uplijst tooverify Hallo back-up nog geldig. Als back-up Hallo geldig is en u vanuit de cloud hello herstellen wilt, vervolgens verbindingsproblemen mogelijk Hallo probleem veroorzaakt. 

toocomplete hello herstelbewerking, Hallo volume offline nemen op Hallo host en probeer Hallo restore-bewerking. Alle wijzigingen toohello volumegegevens die zijn uitgevoerd tijdens het terugzetten van een Hallo gaan verloren.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe te[beheren StorSimple-volumes](storsimple-manage-volumes-u2.md).
* Meer informatie over hoe te[gebruik Hallo StorSimple Manager service tooadminister uw StorSimple-apparaat](storsimple-manager-service-administration.md).

