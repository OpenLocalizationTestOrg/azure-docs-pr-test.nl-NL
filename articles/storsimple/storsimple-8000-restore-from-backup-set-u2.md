---
title: een volume van de back-up op een StorSimple 8000 serie aaaRestore | Microsoft Docs
description: Legt uit hoe toouse Hallo StorSimple Apparaatbeheer service back-upcatalogus toorestore een StorSimple-volume vanuit een back-upset.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/23/2017
ms.author: alkohli
ms.openlocfilehash: 0fe2e4c23a23c75ce4058a8531356c94c973c6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set"></a>Een StorSimple-volume herstelt vanuit een back-upset

## <a name="overview"></a>Overzicht

Deze zelfstudie wordt beschreven Hallo restore-bewerking uitgevoerd op een StorSimple 8000 series apparaat met een bestaande back-upset. Gebruik Hallo **back-upcatalogus** blade toorestore een volume van een lokale of cloud back-up. Hallo **back-upcatalogus** blade geeft alle Hallo back-upsets die worden gemaakt wanneer de handmatige of automatische back-ups worden gemaakt. Hallo-herstelbewerking vanuit een back-upset brengt Hallo volume online onmiddellijk tijdens het downloaden van gegevens op de achtergrond Hallo.

Is een alternatieve methode toostart terugzetbewerking toogo te**apparaten > [uw apparaat] > Volumes**. In Hallo **Volumes** blade, selecteer een volume, klik met de rechtermuisknop tooinvoke Hallo contextmenu en selecteer vervolgens **herstellen**.

## <a name="before-you-restore"></a>Voordat u herstellen

Voordat u een terugzetbewerking begint, controleert u Hallo volgende voorbehoud:

* **U moet Hallo volume offline halen** : Hallo volume offline nemen op beide Hallo-host en Hallo apparaat voordat u Hallo restore-bewerking starten. Hoewel Hallo volume online Hallo restore-bewerking automatisch op Hallo-apparaat brengt, moet u handmatig Hallo apparaat online brengt op Hallo host. U kunt Hallo volume online zetten op Hallo host als Hallo volume op Hallo apparaat online is. (U hoeft niet toowait tot Hallo restore-bewerking is voltooid.) Voor procedures gaat te[offline zetten van een volume](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline).

* **Na het terugzetten van het volumetype** : verwijderde volumes zijn hersteld op basis van het type in momentopname Hallo Hallo; dat wil zeggen, volumes die lokaal zijn vastgemaakt worden teruggezet als lokaal vastgemaakte volumes en volumes die zijn lagen worden teruggezet als gelaagde volumes.

    Voor bestaande volumes overschrijft de huidige gebruikstype Hallo van Hallo volume Hallo-type dat is opgeslagen in momentopname Hallo. Bijvoorbeeld, als u een volume herstelt vanuit een momentopname die is uitgevoerd wanneer het Hallo-volumetype is gelaagd volumetype dat nu lokaal is vastgemaakt (vervaldatum conversiebewerking tooa die is uitgevoerd), wordt vervolgens Hallo volume hersteld als een lokaal vastgemaakt volume. Op dezelfde manier als een bestaand lokaal vastgemaakt volume is uitgebreid en vervolgens wordt teruggezet vanuit een momentopname van een oudere uitgevoerd wanneer het Hallo-volume is kleiner, behoudt hello herstelde volume Hallo huidige uitgevouwen grootte.

    U een volume kan niet converteren van een gelaagd volume tooa lokaal vastgemaakt volume of vanaf een lokaal vastgemaakt volume tooa gelaagd volume terwijl Hallo volume wordt hersteld. Wacht totdat het Hallo restore-bewerking is voltooid en vervolgens kunt u Hallo volume tooanother type converteren. Voor informatie over het converteren van een volume gaat te[Hallo volumetype wijzigen](storsimple-8000-manage-volumes-u2.md#change-the-volume-type). 

* **Hallo volumegrootte komt tot uiting in Hallo hersteld volume** – dit is een belangrijk aandachtspunt als u een lokaal vastgemaakt volume dat is verwijderd (omdat lokaal vastgemaakte volumes zijn volledig is ingericht) wilt herstellen. Zorg ervoor dat u over voldoende ruimte beschikken voordat u de toorestore een lokaal vastgemaakt volume die eerder is verwijderd.

* **U kunt een volume niet uitbreiden wanneer deze wordt hersteld** : wacht totdat Hallo restore-bewerking is voltooid voordat u de tooexpand Hallo volume. Voor informatie over het uitbreiden van een volume gaat te[wijzigen van een volume](storsimple-8000-manage-volumes-u2.md#modify-a-volume).

* **U kunt een back-up uitvoeren terwijl u een lokale volume herstelt** – voor procedures te gaat[hello StorSimple Apparaatbeheer service toomanage back-upbeleid gebruiken](storsimple-8000-manage-backup-policies-u2.md).

* **U kunt een herstelbewerking annuleren** : als u hersteltaak hello, annuleert en vervolgens Hallo volume wordt teruggedraaid toohello staat waarin deze zich bevond voordat u de herstelbewerking Hallo geïnitieerd. Voor procedures gaat te[een taak annuleren](storsimple-8000-manage-jobs-u2.md#cancel-a-job).

## <a name="how-does-restore-work"></a>Hoe werk herstellen

Voor apparaten met Update 4 of hoger, is heatmap-herstelfuncties geïmplementeerd. Zoals aanvragen Hallo-tooaccess hostgegevens Hallo-apparaat bereiken, wordt deze aanvragen worden bijgehouden en een heatmap wordt gemaakt. Hoog percentage resulteert in gegevenssegmenten met hogere hitte dat lagere aanvraagsnelheid toochunks met lagere hitte vertaalt. U moet toegang tot Hallo gegevens ten minste tweemaal toobe gemarkeerd als _hot_. Een bestand dat wordt gewijzigd ook is gemarkeerd als _hot_. Zodra u Hallo herstel start, treedt er proactieve hydratie van gegevens op op basis van Hallo heatmap. Voor versies wordt eerder dan Update 4 Hallo gegevens gedownload tijdens het terugzetten op basis van alleen toegang.

Hallo volgende voorbehoud van toepassing op basis van tooheatmap herstelacties:

* Heatmap bijhouden is alleen ingeschakeld voor gelaagde volumes en lokaal vastgemaakte volumes worden niet ondersteund.

* Heatmap-herstelfuncties wordt niet ondersteund bij het klonen van een volumeapparaat tooanother. 

* Als er een in-place herstellen en een lokale momentopname voor Hallo volume toobe hersteld op Hallo-apparaat bestaat, komen klikt u vervolgens we niet rehydrate (zoals gegevens al lokaal beschikbaar is). 

* Standaard, wanneer u herstelt, zijn Hallo rehydratering taken gestart die gegevens op basis van Hallo heatmap proactief rehydrate. 

In Update 4 Windows PowerShell-cmdlets gebruikt tooquery rehydratering taken uitgevoerd worden, een rehydratering taak annuleren en Hallo status Hallo rehydratering taak ophalen.

* `Get-HcsRehydrationJob`-Deze cmdlet Hallo status van Hallo rehydratering taak opgehaald. Een taak één rehydratering wordt geactiveerd voor één volume.

* `Set-HcsRehydrationJob`-Deze cmdlet kunt u toopause, stoppen, hervatten Hallo rehydratering taak als Hallo rehydratering wordt uitgevoerd.

Voor meer informatie over rehydratering cmdlets gaat te[naslaginformatie over Windows PowerShell-cmdlets voor StorSimple](https://technet.microsoft.com/library/dn688168.aspx).

Met automatische rehdyration wordt doorgaans hogere prestaties voor de tijdelijke lezen verwacht. Hallo werkelijke magniutde van verbeteringen is afhankelijk van verschillende factoren zoals toegangstijden en gegevensverloop gegevenstype. 

een taak rehydratering toocancel, kunt u Hallo PowerShell-cmdlet. U kunt eventueel toopermanently uitschakelen rehydratering taken voor alle toekomstige herstelbewerkingen Hallo [contact op met Microsoft Support](storsimple-8000-contact-microsoft-support.md).

## <a name="how-toouse-hello-backup-catalog"></a>Hoe toouse Hallo back-upcatalogus

Hallo **back-upcatalogus** blade biedt een query waarmee u toonarrow uw selectie back-upset. U kunt Hallo back-upsets die worden opgehaald op basis van de volgende parameters Hallo filteren:

* **Tijdsbereik** – Hallo bereik datum en tijd wanneer Hallo back-upset is gemaakt.
* **Apparaat** – Hallo-apparaat op welke Hallo back-upset is gemaakt.
* **Back-up maken van beleid** of **Volume** – Hallo back-upbeleid of volume dat is gekoppeld aan deze back-upset.

Hallo gefilterde back-upsets worden vervolgens in een tabel weergegeven op basis van Hallo volgende kenmerken:

* **Naam** – hello naam van back-upbeleid Hallo of volumes die zijn gekoppeld aan de back-upset Hallo.
* **Type** – sets van back-up kunnen worden lokale momentopnamen of cloud worden opgeslagen. Een lokale momentopname is een back-up van alle uw worden lokaal opgeslagen volumegegevens op Hallo-apparaat dat een cloudmomentopname toohello back-up van volumegegevens in de cloud Hallo verwijst. Lokale momentopnamen bieden sneller toegang terwijl cloudmomentopnamen voor gegevenstolerantie worden gekozen.
* **De grootte van** – werkelijke grootte van de back-upset Hallo Hallo.
* **Gemaakt op** : Hallo datum en tijd waarop Hallo back-ups zijn gemaakt. 
* **Volumes** -aantal volumes die zijn gekoppeld aan de back-upset Hallo Hallo.
* **Geïnitieerd** – Hallo back-ups worden geïnitieerd automatisch volgens tooa schema of handmatig door een gebruiker. (U kunt een back-upbeleid tooschedule back-ups. U kunt ook hello gebruiken **back-up maken** optie tootake een back-up interactieve of op aanvraag.)

## <a name="how-toorestore-your-storsimple-volume-from-a-backup"></a>Hoe toorestore uw StorSimple-volume van een back-up

U kunt Hallo **back-upcatalogus** blade toorestore uw StorSimple-volume van een specifieke back-up. Houd er rekening mee echter dat herstellen van die een volume wordt teruggezet Hallo volume toohello status toen Hallo back-up is gemaakt. Alle gegevens die zijn toegevoegd na de back-upbewerking Hallo niet verloren.

> [!WARNING]
> Terugzetten vanuit een back-up wordt vervangen door bestaande volumes Hallo van Hallo back-up. Hierdoor kunnen Hallo verlies van gegevens die is geschreven nadat Hallo back-up is gemaakt.


### <a name="toorestore-your-volume"></a>toorestore uw volume
1. Ga tooyour Apparaatbeheer StorSimple-service en klik vervolgens op **back-upcatalogus**.

2. Selecteer een back-up als volgt instellen:
   
   1. Hallo tijdsperiode opgeven.
   2. Selecteer het juiste apparaat Hallo.
   3. Kies in de vervolgkeuzelijst hello, Hallo volume of back-up beleid voor back-up Hallo gewenste tooselect.
   4. Klik op **toepassen** tooexecute deze query.

    Hallo back-ups die zijn gekoppeld aan Hallo geselecteerd volume of back-up beleid moeten worden weergegeven in de lijst Hallo van back-upsets.
   
    ![Back-upset lijst](./media/storsimple-8000-restore-from-backup-set-u2/bucatalog.png)     
     
3. Vouw Hallo back-upset tooview Hallo gekoppeld volumes. Deze volumes moeten op Hallo host en het apparaat offline worden genomen voordat u ze kunt herstellen. Toegang tot Hallo volumes op Hallo **Volumes** blade van uw apparaat en Hallo Volg de stappen in [offline zetten van een volume](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline) tootake ze offline.
   
   > [!IMPORTANT]
   > Zorg ervoor dat u hebt ondernomen Hallo volumes offline op Hallo host eerst voordat u Hallo volumes offline op Hallo-apparaat nemen. Als u niet Hallo volumes offline op Hallo host nemen, kan deze toodata beschadiging leiden.
   
4. Navigeer terug toohello **back-upcatalogus** tabblad en selecteert u een back-upset. Met de rechtermuisknop en selecteer vervolgens in het contextmenu hello, **herstellen**.

    ![Back-upset lijst](./media/storsimple-8000-restore-from-backup-set-u2/restorebu1.png)

5. U wordt gevraagd om bevestiging. Bekijk Hallo gegevens herstellen, en selecteer vervolgens Hallo bevestiging selectievakje.
   
    ![Bevestigingspagina](./media/storsimple-8000-restore-from-backup-set-u2/restorebu2.png)

7.  Klik op **herstellen**. Hiermee initieert u een hersteltaak die u bekijken kunt door het openen van Hallo **taken** pagina.

    ![Bevestigingspagina](./media/storsimple-8000-restore-from-backup-set-u2/restorebu5.png)

8. Nadat het Hallo herstellen is voltooid, moet u controleren dat Hallo inhoud van uw volumes worden vervangen door de volumes van Hallo back-up.


## <a name="if-hello-restore-fails"></a>Als Hallo herstellen mislukt

U ontvangt een waarschuwing als Hallo herstelbewerking mislukt voor een of andere reden. Als dit gebeurt, is vernieuwen Hallo back-uplijst tooverify Hallo back-up nog geldig. Als back-up Hallo geldig is en u vanuit de cloud hello herstellen wilt, vervolgens verbindingsproblemen mogelijk Hallo probleem veroorzaakt.

toocomplete hello herstelbewerking, Hallo volume offline nemen op Hallo host en probeer Hallo restore-bewerking. Opmerking wijzigingen toohello volumegegevens die zijn uitgevoerd tijdens het Hallo herstelproces niet verloren.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe te[beheren StorSimple-volumes](storsimple-8000-manage-volumes-u2.md).
* Meer informatie over hoe te[gebruik Hallo StorSimple Apparaatbeheer service tooadminister uw StorSimple-apparaat](storsimple-8000-manager-service-administration.md).

