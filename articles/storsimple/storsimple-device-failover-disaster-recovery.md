---
title: aaaStorSimple failover en herstel na noodgevallen | Microsoft Docs
description: Meer informatie over hoe toofail via uw tooitself StorSimple-apparaat, een ander fysiek apparaat of een virtueel apparaat.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 5751598e-49c8-42b3-8121-fea5857a7d83
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/16/2016
ms.author: alkohli
ms.openlocfilehash: 00ce365f8a9095d1f0292e665d7f9eaa844b44ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="failover-and-disaster-recovery-for-your-storsimple-device"></a>Failover en herstel na noodgevallen voor uw StorSimple-apparaat
## <a name="overview"></a>Overzicht
Deze zelfstudie wordt beschreven Hallo stappen vereist toofail via een virtueel StorSimple-apparaat in de gebeurtenis Hallo van een noodgeval. Een failover kunt u toomigrate uw gegevens uit een Bronapparaat in Hallo datacenter tooanother fysieke of zelfs een virtueel apparaat zich in Hallo dezelfde of een andere geografische locatie. 

Noodherstel (DR) wordt beheerd via failoverfunctie Hallo-apparaat en wordt gestart vanuit Hallo **apparaten** pagina. Deze pagina registreert alle Hallo StorSimple-apparaten verbonden tooyour StorSimple Manager-service. Voor elk apparaat, Hallo beschrijvende naam, status, ingericht en de maximale capaciteit, worden type en model weergegeven.

![Pagina apparaten](./media/storsimple-device-failover-disaster-recovery/IC740972.png)

Hallo richtlijnen in deze zelfstudie geldt tooStorSimple fysieke en virtuele apparaten in alle softwareversies.

## <a name="disaster-recovery-dr-and-device-failover"></a>Noodherstel (DR) en failover-apparaat
In een (DR) noodherstelscenario Hallo primair apparaat niet meer werkt. In dit geval kunt u cloudgegevens Hallo Hallo mislukte apparaat tooanother apparaat gekoppeld met behulp van het primaire apparaat Hallo als Hallo *bron* en een ander apparaat op te geven als Hallo *doel*. U kunt een of meer volume containers toomigrate toohello doelapparaat selecteren. Dit proces is waarnaar wordt verwezen tooas hello *failover*. 

Tijdens de failover van Hallo Hallo volumecontainers van het bronvolume Hallo eigendom wijzigen en worden overgedragen toohello doelapparaat. Zodra de volumecontainers Hallo eigendom wijzigen, wordt deze verwijderd van het bronvolume Hallo. Nadat Hallo verwijdering voltooid is, Hallo doelapparaat vervolgens terug failover.

Doorgaans na een DR, de meest recente back-up van Hallo is gebruikte toorestore hello toohello doelapparaat. Echter als er meerdere back-upbeleid voor Hallo hetzelfde volume, vervolgens back-upbeleid met het grootste aantal volumes Hallo Hallo opgehaald verzameld en Hallo meest recente back-up van dat beleid gebruikte toorestore Hallo gegevens op het doelapparaat Hallo.

Een voorbeeld: als er twee back-upbeleid (één standaard- en een aangepaste) *defaultPol*, *customPol* Hello volgende details:

* *defaultPol* : één volume *vol1*, dagelijkse begint bij 10:30 uur uitgevoerd.
* *customPol* : vier volumes *vol1*, *vol2*, *vol3*, *vol4*, dagelijkse begint bij 10:00 uur uitgevoerd.

In dit geval *customPol* wordt gebruikt als er meerdere volumes en we voor crashconsistentie prioriteren. Hallo meest recente back-up van dit beleid is gebruikte toorestore gegevens.

## <a name="considerations-for-device-failover"></a>Overwegingen voor het apparaat failover
U kunt in geval van een noodgeval Hallo toofail kiezen via uw StorSimple-apparaat:

* het fysieke apparaat tooa 
* tooitself
* tooa virtueel apparaat

Houd er rekening mee Hallo volgende voor de failover van een apparaat:

* Hallo vereisten voor herstel na Noodgevallen zijn dat alle Hallo volumes binnen Hallo volumecontainers offline zijn en Hallo volumecontainers een gekoppeld hebben cloudmomentopname. 
* Hallo beschikbaar doelapparaten voor herstel na Noodgevallen zijn apparaten waarop voldoende ruimte tooaccommodate Hallo containers geselecteerde volume. 
* Hallo apparaten die verbonden tooyour zijn service, maar niet voldoen aan de criteria Hallo van voldoende ruimte is alleen beschikbaar als doelapparaten.
* Na een DR, voor een bepaalde duur Hallo data access-prestaties aanzienlijk kan worden beïnvloed, als Hallo-apparaat wordt moet tooaccess Hallo van gegevens van Hallo cloud en lokaal opslaan.

#### <a name="device-failover-across-software-versions"></a>Apparaat failover tussen softwareversies
Een StorSimple Manager-service in een implementatie mogelijk op meerdere apparaten, fysieke en virtuele, alle actieve verschillende software-versies. Afhankelijk van de softwareversie hello, Hallo volumetypen op Hallo apparaten mogelijk ook andere. Bijvoorbeeld, een apparaat actieve Update 2 of hoger zou gelden lokaal vastgemaakt en gelaagde volumes (met archivering wordt een subset van gelaagd). Een apparaat vóór Update 2 op Hallo daarentegen kan hebben lagen en archivering volumes. 

Hallo tabel toodetermine volgen als u failover uitvoeren van een ander software-versie en Hallo gedrag van volumetypen tijdens DR tooanother-apparaat gebruiken.

| Failover van | Toegestaan voor het fysieke apparaat | Toegestaan voor het virtuele apparaat |
| --- | --- | --- |
| Update 2 toopre-Update 1 (Release, 0,1, 0,2, 0,3) |Nee |Nee |
| Update 2 tooUpdate 1 (1, 1.1, 1.2) |Ja <br></br>Als u met behulp van lokaal vastgemaakt of gelaagde volumes of een combinatie van twee, Hallo volumes wordt altijd een failover uitgevoerd als lagen. |Ja<br></br>Als u lokaal vastgemaakte volumes, zijn deze dan gelaagde mislukt. |
| Update 2 tooUpdate 2 (latere versie) |Ja<br></br>Als u lokaal vastgemaakte of gelaagde volumes of een combinatie van twee, Hallo volumes wordt altijd een failover uitgevoerd als Hallo volumetype; starten gelaagde als gelaagde en lokaal vastgemaakt als lokaal vastgemaakt. |Ja<br></br>Als u lokaal vastgemaakte volumes, zijn deze dan gelaagde mislukt. |

#### <a name="partial-failover-across-software-versions"></a>Gedeeltelijke failover tussen softwareversies
Volg deze richtlijnen als u van plan bent tooperform een gedeeltelijke failover met behulp van een StorSimple-bron-apparaat met vooraf Update 1 tooa doel met Update 1 of hoger. 

| Gedeeltelijke failover van | Toegestaan voor het fysieke apparaat | Toegestaan voor het virtuele apparaat |
| --- | --- | --- |
| Vooraf Update 1 (Release, 0,1, 0,2, 0,3) tooUpdate 1 of hoger |Ja, Zie hieronder voor Hallo best practice tip. |Ja, Zie hieronder voor Hallo best practice tip. |

> [!TIP]
> Er is een cloud metagegevens en gegevens indeling gewijzigd in Update 1 en latere versies. Daarom raden we niet een gedeeltelijke failover van vooraf Update 1 tooUpdate 1 of hoger in. Als u een gedeeltelijke failover tooperform nodig hebt, raden wij u eerst toepassen Update 1 of later op beide Hallo apparaten (bron en doel) en ga vervolgens verder met de Hallo failover. 
> 
> 

## <a name="fail-over-tooanother-physical-device"></a>Het fysieke apparaat tooanother failover
Volgende stappen toorestore Hallo uw apparaat tooa fysieke doelapparaat uitvoeren.

1. Controleer of deze Hallo volumecontainer toofail via gewenste cloudmomentopnamen is gekoppeld.
2. Op Hallo **apparaten** pagina, klikt u op Hallo **Volumecontainers** tabblad.
3. Selecteer een volumecontainer dat u toofail via tooanother apparaat dat wilt. Klik op Hallo volume container toodisplay Hallo lijst van volumes in deze container. Selecteer een volume en klik op **Offline nemen** tootake Hallo volume offline. Herhaal dit proces voor alle Hallo volumes in de volumecontainer Hallo.
4. De vorige stap herhalen Hallo voor alle volumecontainers Hallo gewenst toofail via tooanother apparaat.
5. Op Hallo **apparaten** pagina, klikt u op **Failover**.
6. In de wizard Hallo die wordt geopend, klikt u onder **volume container toofail kiezen via**:
   
   1. Selecteer in de lijst van de Hallo met volumecontainers, Hallo volumecontainers toofail via gewenst.
      **Alleen Hallo volumecontainers met momentopnamen van de gekoppelde cloud en offline volumes worden weergegeven.**
   2. Onder **kiezen een doelapparaat** voor Hallo volumes in containers Hallo geselecteerd, selecteert u een doelapparaat van Hallo vervolgkeuzelijst met beschikbare apparaten. Alleen Hallo-apparaten waarvoor de beschikbare capaciteit Hallo worden weergegeven in de vervolgkeuzelijst Hallo.
   3. Controleer ten slotte alle Hallo failover-instellingen onder **bevestigen failover**. Klik op het vinkje Hallo ![vinkje](./media/storsimple-device-failover-disaster-recovery/IC740895.png).
7. Een failover-taak gemaakt die kunnen worden bewaakt via Hallo **taken** pagina. Als het Hallo-volumecontainer waarvoor u failover lokale volumes heeft, ziet u het herstellen van de afzonderlijke taken voor alle lokale volumes (en niet voor gelaagde volumes) in Hallo-container. Deze taken herstelpunten geruime toocomplete tijd kan duren. Is het waarschijnlijk dat Hallo failover-taak mogelijk eerder voltooid. Houd er rekening mee dat deze volumes beschikken over lokale garanties alleen nadat Hallo hersteltaken voltooid zijn. Nadat het Hallo-failover is voltooid, gaat u toohello **apparaten** pagina.                                            
   
   1. Selecteer Hallo-apparaat dat is gebruikt voor het doelapparaat Hallo voor Hallo failover-proces.
   2. Ga toohello **Volumecontainers** pagina. Alle Hallo-volumecontainers, samen met de Hallo volumes van de oude apparaat hello, moeten worden vermeld.

## <a name="failover-using-a-single-device"></a>Failover via één apparaat
Hallo volgende stappen uit als u slechts een enkele tooperform apparaat en moet een failover uitvoeren.

1. Momentopnamen cloud van alle Hallo volumes in uw apparaat.
2. De standaardinstellingen van uw apparaat toofactory opnieuw. Ga als volgt Hallo gedetailleerde instructies in [hoe de standaardinstellingen voor een StorSimple-apparaat toofactory tooreset](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).
3. Uw apparaat configureren en het opnieuw registreren met StorSimple Manager-service.
4. Op Hallo **apparaten** pagina Hallo oude apparaat moet worden weergegeven als **Offline**. Hallo nieuw ingeschreven apparaat moet worden weergegeven als **Online**.
5. Voor het nieuwe apparaat hello, Hallo minimale configuratie van Hallo apparaat eerst te voltooien. 
   
   > [!IMPORTANT]
   > **Als de minimale configuratie Hallo niet eerst is voltooid, mislukt uw DR als gevolg van een fout in de huidige implementatie Hallo. Dit probleem wordt opgelost in een latere release.**
   > 
   > 
6. Selecteer Hallo oude apparaat (offline status) en klik op **Failover**. In de wizard Hallo die wordt weergegeven, dit apparaat failover en Hallo doelapparaat opgeeft als Hallo nieuw ingeschreven apparaat. Voor gedetailleerde instructies te verwijzen[tooanother fysiek apparaat failover](#fail-over-to-another-physical-device).
7. Een hersteltaak van het apparaat wordt gemaakt dat u vanaf Hallo bewaken kunt **taken** pagina.
8. Nadat het Hallo-taak is voltooid, toegang tot Hallo nieuwe apparaat en navigeer toohello **Volumecontainers** pagina. Alle Hallo volumecontainers van het oude apparaat Hallo worden nu gemigreerde toohello nieuw apparaat.

## <a name="fail-over-tooa-storsimple-virtual-device"></a>Failover tooa virtuele StorSimple-apparaat
U moet een StorSimple virtueel apparaat maken en configureren van eerdere toorunning hebben deze procedure. Als u Update 2 wordt uitgevoerd, kunt u overwegen een virtueel apparaat 8020 voor Hallo DR die is 64 TB en Premium-opslag gebruikt. 

Volgende stappen toorestore Hallo apparaat tooa doel virtueel StorSimple-apparaat Hallo uitvoeren.

1. Controleer of deze Hallo volumecontainer toofail via gewenste cloudmomentopnamen is gekoppeld.
2. Op Hallo **apparaten** pagina, klikt u op Hallo **Volumecontainers** tabblad.
3. Selecteer een volumecontainer dat u toofail via tooanother apparaat dat wilt. Klik op Hallo volume container toodisplay Hallo lijst van volumes in deze container. Selecteer een volume en klik op **Offline nemen** tootake Hallo volume offline. Herhaal dit proces voor alle Hallo volumes in de volumecontainer Hallo.
4. De vorige stap herhalen Hallo voor alle volumecontainers Hallo gewenst toofail via tooanother apparaat.
5. Op Hallo **apparaten** pagina, klikt u op **Failover**.
6. In de wizard Hallo die wordt geopend, klikt u onder **kiezen volume container toofailover**, Hallo volgende voltooien:
   
    a. Selecteer in de lijst van de Hallo met volumecontainers, Hallo volumecontainers toofail via gewenst.
   
    **Alleen Hallo volumecontainers met momentopnamen van de gekoppelde cloud en offline volumes worden weergegeven.**
   
    b. Onder **kiest u een doelapparaat voor Hallo volumes in containers Hallo geselecteerd**, selecteer Hallo virtueel StorSimple-apparaat uit Hallo vervolgkeuzelijst met beschikbare apparaten. **Hallo alleen apparaten die voldoende capaciteit hebben worden weergegeven in de vervolgkeuzelijst Hallo.**  
7. Controleer ten slotte alle Hallo failover-instellingen onder **bevestigen failover**. Klik op het vinkje Hallo ![vinkje](./media/storsimple-device-failover-disaster-recovery/IC740895.png).
8. Nadat het Hallo-failover is voltooid, gaat u toohello **apparaten** pagina.
   
    a. Selecteer Hallo virtueel StorSimple-apparaat dat is gebruikt als het doelapparaat Hallo voor Hallo failover-proces.
   
    b. Ga toohello **Volumecontainers** pagina. Alle Hallo-volumecontainers, samen met de volumes van de oude apparaat Hallo Hallo zou nu moeten worden vermeld.

![Video beschikbaar](./media/storsimple-device-failover-disaster-recovery/Video_icon.png) **Video beschikbaar**

toowatch een video die u laat zien hoe u kunt een mislukte via fysieke apparaat tooa virtueel apparaat in de cloud hello, klikt u op [hier](https://azure.microsoft.com/documentation/videos/storsimple-and-disaster-recovery/).

## <a name="failback"></a>Failback
Update 3 en hoger ondersteuning StorSimple ook voor failback. Nadat het Hallo-failover is voltooid, hello volgende acties uitgevoerd:

* Hallo volumecontainers die worden overgenomen worden van het bronvolume Hallo opgeschoond.
* Een achtergrondtaak per volumecontainer (failover) wordt gestart op het bronvolume Hallo. Als u toofailback probeert tijdens het Hallo-taak wordt uitgevoerd, ontvangt u een melding toothat effect. U moet toowait totdat het Hallo-taak is voltooid toostart Hallo failback. 
  
    Hallo tijd toocomplete Hallo verwijdering van volumecontainers is afhankelijk van verschillende factoren zoals de hoeveelheid gegevens, de leeftijd van Hallo gegevens, het aantal back-ups en beschikbare Hallo netwerkbandbreedte voor Hallo-bewerking. Als u van plan bent test failovers/failbacks, raden wij volumecontainers met minder gegevens (GB) te testen. In de meeste gevallen kunt u Hallo failback starten 24 uur na het Hallo-failover is voltooid. 

## <a name="frequently-asked-questions"></a>Veelgestelde vragen
Q. **Wat gebeurt er als Hallo DR mislukt of gedeeltelijk geslaagd is?**

A. Als Hallo DR mislukt, wordt u aangeraden dat u het opnieuw proberen. Hallo tweede keer, DR weet wat alle werd uitgevoerd en wanneer Hallo proces tot stilstand gekomen Hallo eerst. Hallo DR-proces wordt gestart vanaf dat moment en hoger. 

Q. **Kan ik een apparaat verwijderen terwijl Hallo apparaat failover uitgevoerd wordt?**

A. U kunt een apparaat niet verwijderen, terwijl een DR uitgevoerd wordt. U kunt uw apparaat alleen verwijderen als Hallo DR voltooid is.

Q.    **Wanneer Hallo garbagecollection begint op het bronvolume Hallo zodat Hallo lokale gegevens op het bronvolume is verwijderd?**

A. Garbagecollection wordt ingeschakeld op het bronvolume Hallo pas nadat Hallo apparaat volledig wordt opgeschoond. Hallo opschonen bevat objecten die failover van Hallo Bronapparaat zoals volumes, back-objecten (geen gegevens), volumecontainers en beleidsregels voor het opruimen.

Q. **Wat gebeurt er als Hallo taak die is gekoppeld aan Hallo volumecontainers in het bronvolume Hallo verwijderen mislukt?**

A.  Als Hallo verwijderen van taak mislukt, moet u toomanually trigger Hallo verwijdering van volumecontainers Hallo. In Hallo **apparaten** pagina, selecteer het bronapparaat en klik op **volumecontainers**. Selecteer Hallo volumecontainers die u niet via en in de onderste Hallo Hallo pagina, klikt u op **verwijderen**. Zodra u alle Hallo hebt verwijderd volumecontainers op het bronvolume Hallo failover, kunt u beginnen met Hallo failback.

## <a name="business-continuity-disaster-recovery-bcdr"></a>Herstel van zakelijke continuïteit na noodgevallen (BCDR)
Een zakelijke continuïteit (BCDR) noodherstelscenario treedt op wanneer Hallo volledige Azure-datacenter niet meer werkt. Dit kan invloed hebben op uw StorSimple Manager-service en Hallo bijbehorende StorSimple-apparaten.

Als er StorSimple-apparaten die zijn geregistreerd, net voordat een noodgeval is opgetreden, mogelijk een van de fabrieksinstellingen tooundergo moet op deze StorSimple-apparaten. Na noodgevallen Hallo wordt Hallo StorSimple-apparaat weergegeven als offline. Hallo StorSimple-apparaat moet worden verwijderd uit Hallo-portal en fabrieksinstellingen moet worden gedaan, gevolgd door een nieuwe registratie.

## <a name="next-steps"></a>Volgende stappen
* Nadat u hebt een failover uitgevoerd, moet u wellicht te[deactiveren of verwijderen van uw StorSimple-apparaat](storsimple-deactivate-and-delete-device.md).
* Voor informatie over hoe toouse Hallo StorSimple Manager-service, gaat u te[gebruik Hallo StorSimple Manager service tooadminister uw StorSimple-apparaat](storsimple-manager-service-administration.md).

