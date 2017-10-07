---
title: aaaStorSimple virtuele matrix disaster recovery en apparaat failover | Microsoft Docs
description: Meer informatie over het toofailover uw virtuele StorSimple-matrix.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 3c1f9c62-af57-4634-a0d8-435522d969aa
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5f125efd1ffb94489cdfa7cfaafae7d57cc10131
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-and-device-failover-for-your-storsimple-virtual-array-via-azure-portal"></a>Disaster recovery en apparaat failover voor uw virtuele StorSimple-matrix via Azure portal

## <a name="overview"></a>Overzicht
In dit artikel beschrijft Hallo noodherstel voor uw Microsoft Azure StorSimple virtuele matrix met inbegrip van Hallo gedetailleerde toofail via tooanother virtuele matrix stappen. Een failover kunt u toomove uw gegevens uit een *bron* apparaat in Hallo datacenter tooa *doel* apparaat. Hallo doelapparaat mogelijk zich in Hallo dezelfde of een andere geografische locatie. Hallo apparaat failover is voor het hele apparaat Hallo. Tijdens de failover, Hallo cloud voor het bronvolume Hallo gegevenswijzigingen toothat eigendom van het doelapparaat Hallo.

Dit artikel is van toepassing tooStorSimple alleen virtuele matrices. toofail via een apparaat 8000-serie gaat te[apparaat failover en herstel na noodgevallen van uw StorSimple-apparaat](storsimple-device-failover-disaster-recovery.md).

## <a name="what-is-disaster-recovery-and-device-failover"></a>Wat is disaster recovery en apparaat failover?

In een (DR) noodherstelscenario Hallo primair apparaat niet meer werkt. In dit scenario kunt u cloudgegevens Hallo Hallo mislukte apparaat tooanother apparaat gekoppeld. U kunt het primaire apparaat Hallo gebruiken als Hallo *bron* en een ander apparaat opgeeft als Hallo *doel*. Dit proces is waarnaar wordt verwezen tooas hello *failover*. Tijdens de failover, alle volumes Hallo of shares van het bronvolume Hallo Hallo eigendom wijzigen en zijn overgedragen toohello doelapparaat. Er is geen filteren van gegevens Hallo is toegestaan.

Noodherstel is gemodelleerd als een volledige apparaat te herstellen met behulp van Hallo heat map gebaseerde in lagen en bij te houden. Een heatmap wordt gedefinieerd door het toewijzen van een hitte waarde toohello gegevens op basis van lezen en schrijven van patronen. Deze hitte toewijzen en vervolgens de laagste hitte gegevens segmenten toohello cloud lagen eerst Hallo terwijl Hallo hoge hitte (meest gebruikt) gegevenssegmenten in Hallo lokale laag. Tijdens een DR StorSimple Hallo heat map toorestore gebruikt en rehydrate Hallo gegevens uit Hallo cloud. Hallo apparaat haalt alle Hallo volumes/shares in Hallo laatste recente back-up (zoals intern bepaald) en voert een herstel van back-up. Hallo virtuele matrix ingedeeld Hallo hele DR-proces.

> [!IMPORTANT]
> Hallo bronapparaat aan Hallo einde van de failover-apparaat wordt verwijderd en daarom een failback wordt niet ondersteund.
> 
> 

Herstel na noodgevallen wordt beheerd via failoverfunctie Hallo-apparaat en wordt gestart vanuit Hallo **apparaten** blade. Deze blade registreert alle Hallo StorSimple-apparaten verbonden tooyour Apparaatbeheer StorSimple-service. Voor elk apparaat ziet u de beschrijvende naam hello, status, ingericht en de maximale capaciteit, type en model.

## <a name="prerequisites-for-device-failover"></a>Vereisten voor failover-apparaat

### <a name="prerequisites"></a>Vereisten

Zorg ervoor dat Hallo volgende vereisten wordt voldaan voor een failover apparaat:

* Hallo Bronapparaat moet toobe in een **gedeactiveerd** status.
* Hallo doelapparaat moet tooshow up als **tooset gereed** in hello Azure-portal. Inrichten van een virtuele doelmatrix Hallo dezelfde of een hogere capaciteit. Hallo lokale web UI tooconfigure gebruik en virtuele doelmatrix hello wordt geregistreerd.
  
  > [!IMPORTANT]
  > Probeer niet tooconfigure Hallo geregistreerde virtuele apparaat via Hallo-service. Er is geen apparaatconfiguratie moet worden uitgevoerd via Hallo-service.
  > 
  > 
* Hallo doelapparaat kan niet dezelfde naam als het bronvolume Hallo Hallo hebben.
* Hallo bron en doel-apparaat hebt toobe Hallo van hetzelfde type. U kunt alleen een virtuele matrix die is geconfigureerd als een bestandsserver van het server-tooanother failover. Hallo geldt voor een iSCSI-server.
* Voor een bestandsserver DR, raden we aan dat u Hallo doel apparaat toohello deelnemen aan hetzelfde domein als Hallo bron. Deze configuratie zorgt ervoor dat de sharemachtigingen Hallo automatisch opgelost. Alleen Hallo failover tooa doelapparaat in Hallo hetzelfde domein.
* Hallo beschikbaar doelapparaten voor herstel na Noodgevallen zijn apparaten waarop dezelfde Hallo of grotere capaciteit ten opzichte van het bronvolume toohello. Hallo apparaten die verbonden tooyour zijn service, maar niet Hallo voldoen aan de criteria van voldoende ruimte zijn niet beschikbaar als doelapparaten.

### <a name="other-considerations"></a>Andere overwegingen

* Voor een geplande failover 
  
  * Het is raadzaam dat u alle Hallo volumes of shares op Hallo Bronapparaat offline neemt.
  * U wordt aangeraden dat u een back-up van Hallo-apparaat en ga vervolgens verder met de Hallo failover toominimize gegevens verloren gaan. 
* Hallo-apparaat gebruikt voor een niet-geplande failover Hallo meest recente back-toorestore Hallo gegevens.

### <a name="device-failover-prechecks"></a>Apparaat failover prechecks

Voordat Hallo die Dr begint, voert Hallo apparaat prechecks. Deze controles zorgen ervoor dat er geen fouten optreden wanneer DR begint. Hallo prechecks zijn onder andere:

* Valideren van het Hallo-opslagaccount.
* Hallo cloud connectiviteit tooAzure controleren.
* Beschikbare ruimte op het doelapparaat Hallo controleren.
* Controleren of een iSCSI-server bronvolume apparaat heeft
  
  * geldige ACR-namen.
  * geldige IQN (van ten hoogste 220 tekens).
  * geldige CHAP wachtwoorden (12-16 tekens).

Als een voorgaande prechecks Hallo mislukt, kunt u kunt niet doorgaan met de Hallo DR. Deze problemen oplossen en probeer vervolgens Noodherstel.

Nadat Hallo DR is voltooid, is eigendom van Hallo cloudgegevens op het bronvolume Hallo Hallo overgebrachte toohello doelapparaat. Hallo het bronvolume is vervolgens niet meer beschikbaar zijn in Hallo-portal. Toegang tooall Hallo volumes/shares op Hallo Bronapparaat is geblokkeerd en Hallo doelapparaat wordt geactiveerd.

> [!IMPORTANT]
> Hoewel het Hallo-apparaat is niet meer beschikbaar, verbruikt Hallo virtuele machine die u hebt ingericht op het hostsysteem Hallo nog steeds bronnen. Zodra de Hallo DR is met succes voltooid, kunt u deze virtuele machine verwijderen uit uw hostsysteem.
> 
> 

## <a name="fail-over-tooa-virtual-array"></a>Failover van virtuele matrix tooa

U wordt aangeraden inrichten, configureren en registreren van een andere virtuele StorSimple-matrix met uw StorSimple-apparaat Manager-service voordat u deze procedure uitvoert.

> [!IMPORTANT]
> 
> * U kan niet worden overgenomen van een StorSimple 8000 series apparaat tooa 1200 virtueel apparaat.
> * U kunt een failover uitvoeren van een Federal Information Processing Standard (FIPS) ingeschakeld virtueel apparaat tooanother FIPS ingeschakeld apparaat of tooa niet FIPS apparaat is geïmplementeerd in Hallo overheid-portal.


Volgende stappen toorestore Hallo apparaat tooa doel virtueel StorSimple-apparaat Hallo uitvoeren.

1. Inrichten en configureren van een apparaat dat voldoet aan Hallo [vereisten voor failover apparaat](#prerequisites). Hallo apparaatconfiguratie via Hallo lokale webgebruikersinterface voltooien en registreer tooyour Apparaatbeheer StorSimple-service. Als het maken van een bestandsserver gaat toostep 1 van [instellen als bestandsserver](storsimple-virtual-array-deploy3-fs-setup.md#step-1-complete-the-local-web-ui-setup-and-register-your-device). Als u een iSCSI-server maakt, gaat u toostep 1 van [ingesteld als iSCSI-server](storsimple-virtual-array-deploy3-iscsi-setup.md#step-1-complete-the-local-web-ui-setup-and-register-your-device).

2. Volumes/shares offline nemen op Hallo host. tootake hello volumes/shares offline, Raadpleeg toohello besturingssysteem-specifieke instructies voor Hallo host. Als niet al offline is, moet u op tootake alle Hallo volumes/shares offline op Hallo apparaat door Hallo volgende te doen.
   
    1. Ga te**apparaten** blade en selecteer het apparaat.
   
    2. Ga te**instellingen > beheren > Shares** (of **instellingen > beheren > Volumes**). 
   
    3. Selecteer een share of het geselecteerde volume, klik met de rechtermuisknop en selecteer **offline zetten**. 
   
    4. Wanneer u wordt gevraagd om bevestiging, controleert u **ik begrijp Hallo gevolgen van deze share offline moet worden gezet.** 
   
    5. Klik op **offline zetten**.

3. In uw StorSimple-apparaat Manager-service, gaan te**Management > apparaten**. In Hallo **apparaten** blade selecteren en klik op het bronapparaat.

4. In uw **apparaat dashboard** blade, klikt u op **deactiveren**.

5. In Hallo **deactiveren** blade u om bevestiging wordt gevraagd. Deactivering van het apparaat is een *permanente* proces dat kan niet ongedaan worden gemaakt. U zijn ook tootake herinnerd dat de shares/volumes offline op Hallo host. Typ Hallo apparaat naam tooconfirm en klik op **deactiveren**.
   
    ![](./media/storsimple-virtual-array-failover-dr/failover1.png)
6. Hallo deactivering wordt gestart. U ontvangt een melding nadat Hallo deactivering is voltooid.
   
    ![](./media/storsimple-virtual-array-failover-dr/failover2.png)
7. Op de pagina apparaten hello, Hallo Apparaatstatus nu verandert te**gedeactiveerd**.
    ![](./media/storsimple-virtual-array-failover-dr/failover3.png)
8. In Hallo **apparaten** blade en op Hallo gedeactiveerde Bronapparaat voor failover. 
9. In Hallo **apparaat dashboard** blade, klikt u op **failover**. 
10. In Hallo **apparaat failover** blade Hallo te volgen:
    
    1. Hallo bron apparaat veld wordt automatisch gevuld. Houd er rekening mee Hallo totale gegevensgrootte voor Hallo het bronvolume. Hallo gegevensgrootte moet kleiner zijn dan de beschikbare capaciteit op het doelapparaat Hallo Hallo. Bekijk de details van de Hallo die zijn gekoppeld aan het bronvolume Hallo zoals apparaatnaam totale capaciteit en Hallo namen van Hallo shares die worden overgenomen.

    2. Kies in de vervolgkeuzelijst met beschikbare apparaten hello, een **doelapparaat**. Hallo alleen apparaten die voldoende capaciteit hebben worden in de vervolgkeuzelijst Hallo weergegeven.

    3. Controleer of **ik begrijp dat deze bewerking failover gegevens toohello doelapparaat**. 

    4. Klik op **failover**.
    
        ![](./media/storsimple-virtual-array-failover-dr/failover4.png)
11. Een failover-taak wordt gestart en u ontvangt een melding. Ga te**apparaten > taken** toomonitor Hallo failover.
    
     ![](./media/storsimple-virtual-array-failover-dr/failover5.png)
12. In Hallo **taken** blade ziet u een failover-taak gemaakt voor het bronvolume Hallo. Deze taak voert Hallo DR prechecks.
    
    ![](./media/storsimple-virtual-array-failover-dr/failover6.png)
    
     Nadat Hallo DR prechecks geslaagd zijn, wordt het herstellen van taken voor elk share/volume dat zich op uw Bronapparaat kan gemaakt Hallo failover-taak.
    
    ![](./media/storsimple-virtual-array-failover-dr/failover7.png)
13. Nadat de Hallo failover is voltooid, gaat u toohello **apparaten** blade.
    
    1. Selecteren en op Hallo StorSimple-apparaat dat is gebruikt als het doelapparaat Hallo voor Hallo failover-proces.
    2. Ga te**instellingen > Beheer > Shares** (of **Volumes** als iSCSI-server). In Hallo **Shares** blade kunt u alle Hallo shares (volumes) van het oude apparaat Hallo weergeven.
        ![](./media/storsimple-virtual-array-failover-dr/failover9.png)
14. U moet te[maken van een DNS-alias](https://support.microsoft.com/kb/168322) zodat alle toepassingen die probeert Hallo tooconnect omgeleide toohello nieuw apparaat kunt krijgen.

## <a name="errors-during-dr"></a>Fouten tijdens DR

**Cloud-connectiviteit onderbreking tijdens DR**

Als Hallo cloud connectiviteit wordt onderbroken na DR is gestart en voordat Hallo apparaat terugzetten voltooid is, Hallo DR zal mislukken. U ontvangt een melding failore. Hallo doelapparaat voor herstel na Noodgevallen is gemarkeerd als *onbruikbaar.* U kunt geen hello gebruiken hetzelfde doelapparaat voor toekomstige DRs.

**Er is geen compatibele doelapparaten**

Als Hallo beschikbaar doelapparaten niet voldoende ruimte hebt, ziet u een fout toohello effect dat er geen doelapparaten compatibel zijn.

**Controle vooraf fouten**

Als een van de Hallo prechecks niet is voldaan, ziet u mislukte controle vooraf.

## <a name="business-continuity-disaster-recovery-bcdr"></a>Herstel van zakelijke continuïteit na noodgevallen (BCDR)

Een zakelijke continuïteit (BCDR) noodherstelscenario treedt op wanneer Hallo volledige Azure-datacenter niet meer werkt. Dit kan invloed hebben op uw StorSimple-apparaat Manager-service en Hallo bijbehorende StorSimple-apparaten.

Als er StorSimple-apparaten die zijn geregistreerd, net voordat een noodgeval is opgetreden, mogelijk verwijderd toobe moet op deze StorSimple-apparaten. U kunt na noodgevallen Hallo opnieuw maken en configureren van deze apparaten.

## <a name="next-steps"></a>Volgende stappen

Meer informatie over het te[beheren van uw virtuele StorSimple-matrix met Hallo lokale webgebruikersinterface](storsimple-ova-web-ui-admin.md).

