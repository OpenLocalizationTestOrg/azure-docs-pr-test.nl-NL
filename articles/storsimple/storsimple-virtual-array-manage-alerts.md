---
title: aaaView en Microsoft Azure StorSimple virtuele matrix waarschuwingen beheren | Microsoft Docs
description: Beschrijft virtuele StorSimple-matrix waarschuwingsvoorwaarden en ernst en hoe toouse hello StorSimple Manager service toomanage waarschuwingen.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 97ee25a1-0ec3-4883-9a0a-54b722598462
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b0fb5b1b9064f33df1d8fa7ace45f0d72b0a1622
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-toomanage-alerts-for-hello-storsimple-virtual-array"></a>Gebruik StorSimple Apparaatbeheer toomanage waarschuwingen voor Hallo virtuele StorSimple-matrix

## <a name="overview"></a>Overzicht

de waarschuwingsfunctie Hallo in Hallo StorSimple-apparaat Manager-service biedt een manier voor u tooreview en waarschuwingen gerelateerde tooStorSimple virtuele matrices op basis van realtime wissen. U kunt waarschuwingen Hallo op Hallo **Serviceoverzicht** blade toocentrally hello statusproblemen van uw virtuele StorSimple-matrices bewaken en Hallo algemene Microsoft Azure StorSimple-oplossing.

Deze zelfstudie wordt beschreven hoe u waarschuwingsmeldingen tooconfigure, algemene waarschuwingsvoorwaarden ernst waarschuwingsniveaus en hoe waarschuwingen tooview en bijhouden. Daarnaast bevat deze waarschuwing Naslaggids tabellen, waarmee u tooquickly Zoek een specifieke waarschuwing en reageren op de juiste wijze.

![pagina waarschuwingen](./media/storsimple-virtual-array-manage-alerts/alerts1.png)

## <a name="configure-alert-settings"></a>Instellingen voor waarschuwingen configureren

U kunt kiezen of u wilt dat toobe op de hoogte met e-mailadres van Hallo waarschuwingsvoorwaarden voor elk van uw virtuele StorSimple-matrices. Bovendien kunt u andere ontvangers waarschuwingsmeldingen identificeren met hun e-mailadres invoeren in Hallo **extra e-mailontvangers** vak, gescheiden door puntkomma's.

> [!NOTE]
> U kunt maximaal 20 e-mailadressen per virtuele matrix.


Nadat u een e-mailmelding voor een virtuele-matrix ingeschakeld, ontvangt de leden van de meldingenlijst Hallo een e-mailbericht telkens wanneer een kritieke waarschuwing optreedt. Hallo-berichten worden verzonden vanuit  *storsimple-alerts-noreply@mail.windowsazure.com*  en meldingsvoorwaarde hello wordt beschreven. Ontvangers kunnen klikken op **Unsubscribe** tooremove zichzelf tegen meldingenlijst Hallo-e-mailbericht.

#### <a name="tooenable-email-notification-for-alerts"></a>tooenable e-mailmeldingen voor waarschuwingen

1. Ga tooyour StorSimple Apparaatbeheer service en in Hallo **Management** sectie, selecteert en op **apparaten**. Selecteer in de lijst van de Hallo van apparaten die worden weergegeven, en klikt u op uw apparaat.
   
    ![instellingen voor waarschuwingen](./media/storsimple-virtual-array-manage-alerts/alerts2.png)
2. Hiermee opent u up Hallo **instellingen** blade. In Hallo **apparaatinstellingen** sectie **algemene**. Hiermee opent u up Hallo **algemene instellingen** blade.
   
    ![configuratie voor meldingen van waarschuwingen](./media/storsimple-virtual-array-manage-alerts/alerts4.png)
3. In Hallo **algemene instellingen** blade te gaan**instellingen voor waarschuwingen** sectie en Hallo volgende instellen:
   
   1. In Hallo **Activeer e-mailmelding** optie **Ja**.
   2. In Hallo **e-servicebeheerders** optie **Ja** als toohave Hallo-servicebeheerder gewenst en medebeheerders alle Hallo waarschuwingsmeldingen ontvangt.
   3. In Hallo **extra e-mailontvangers** Voer Hallo e-mailadressen van alle andere ontvangers Hallo waarschuwingsmeldingen. Geef de namen in Hallo indeling  *someone@somewhere.com* . Gebruik een puntkomma tooseparate Hallo e-mailadressen. U kunt maximaal 20 e-mailadressen per virtuele apparaat configureren.
      
       ![configuratie voor meldingen van waarschuwingen](./media/storsimple-virtual-array-manage-alerts/alerts6.png)
   4. toosend een test-e-mailmeldingen, klikt u op **testbericht verzenden**. Hallo StorSimple-apparaat Manager-service wordt weergegeven statusberichten Hallo Testmelding wordt doorgestuurd.
      
       ![Waarschuwingen testen verzonden e-mailmelding](./media/storsimple-virtual-array-manage-alerts/alerts7.png)
      
      > [!NOTE]
      > Als Hallo testen worden Meldingsbericht niet verzonden, een juiste bericht weergegeven met de Hallo Apparaatbeheer StorSimple-service. Klik op **OK**wacht een paar minuten en probeer het vervolgens toosend uw test-melding opnieuw.
      > 
      > 
   5. Klik onder aan de pagina Hallo Hallo op **opslaan** toosave uw configuratie. Klik op **Ja** als u om bevestiging wordt gevraagd.
      
      ![Waarschuwingen testen verzonden e-mailmelding](./media/storsimple-virtual-array-manage-alerts/alerts10.png)

## <a name="common-alert-conditions"></a>Algemene waarschuwingsvoorwaarden

Uw virtuele StorSimple-matrix genereert waarschuwingen in het antwoord tooa diverse omstandigheden. Hallo volgen Hallo meest voorkomende typen waarschuwingen voorwaarden:

* **Problemen met de netwerkverbinding** – deze waarschuwingen zich voordoen als er problemen bij het overbrengen van gegevens. Communicatieproblemen kunnen optreden tijdens de overdracht van gegevens tooand van hello Azure storage-account of vervaldatum toolack van de verbinding tussen virtuele apparaten Hallo en Hallo Apparaatbeheer StorSimple-service. Communicatieproblemen zijn enkele Hallo moeilijkst toofix omdat er zoveel foutpunten. U moet altijd eerst controleren of verbinding met het netwerk en toegang tot Internet beschikbaar zijn voordat u doorgaat op toomore probleemoplossing geavanceerde. Voor informatie over de poorten en firewall-instellingen, gaat u te[virtuele StorSimple-matrix systeemvereisten](storsimple-ova-system-requirements.md). Ga te voor hulp bij het oplossen van[problemen met de cmdlet Test-Connection Hallo](storsimple-troubleshoot-deployment.md).
* **Prestatieproblemen** – deze waarschuwingen worden veroorzaakt wanneer uw systeem is niet optimaal, zoals wanneer het zich onder een zware belasting.

Bovendien ziet u mogelijk de gerelateerde toosecurity waarschuwingen, updates of taakfouten.

## <a name="alert-severity-levels"></a>Ernstniveau van waarschuwingen

Waarschuwingen hebben verschillende niveaus, afhankelijk van Hallo gevolgen die Hallo waarschuwing situatie wordt hebben en Hallo nodig voor een antwoord toohello waarschuwing. Hallo ernstniveaus zijn:

* **Kritieke** – deze waarschuwing is in het antwoord tooa conditie van invloed op Hallo geslaagde prestaties van uw systeem. Actie is vereist tooensure hello StorSimple-service niet wordt onderbroken.
* **Waarschuwing** : dit probleem kritiek kan worden als niet omgezet. U moet onderzoeken Hallo situatie en een probleem actie vereist tooclear Hallo nemen.
* **Informatie** – deze waarschuwing bevat informatie die nuttig zijn kan bij het beheren van uw systeem en bij te houden.

## <a name="view-and-track-alerts"></a>Waarschuwingen weergeven en bijhouden

Hallo StorSimple Apparaatbeheer service samenvatting blade biedt u een kijkje Hallo aantal waarschuwingen op uw virtuele apparaten, gerangschikt op ernst.

![Waarschuwingen-dashboard](./media/storsimple-virtual-array-manage-alerts/alerts14.png)

Klik op Hallo ernst niveau tooopen hello **waarschuwingen** blade. Hallo resultaten bevatten alleen Hallo-waarschuwingen die overeenkomen met die ernst.

![Rapport waarschuwingen binnen het bereik van tooalert type](./media/storsimple-virtual-array-manage-alerts/alerts15.png)

Klik op een waarschuwing in Hallo lijst tooget aanvullende informatie voor Hallo waarschuwing, waaronder Hallo Hallo waarschuwing is gemeld, laatste keer Hallo aantal exemplaren van Hallo waarschuwing op Hallo-apparaat en Hallo aanbevolen actie tooresolve Hallo waarschuwing.

![Lijst met waarschuwingen en details](./media/storsimple-virtual-array-manage-alerts/alerts16.png)

Als u toosend Hallo informatie tooMicrosoft ondersteuning nodig hebt, kunt u Hallo Waarschuwingsdetails tooa tekstbestand kopiëren. Nadat u hebt gevolgd Hallo aanbeveling en Hallo meldingsvoorwaarde lokale opgelost, moet u de waarschuwing in de lijst Hallo Hallo wissen. Hallo waarschuwing in Hallo lijst selecteren en klik vervolgens op **wissen**. tooclear meerdere waarschuwingen selecteert dat elke waarschuwing, klikt u op een van de kolommen behalve Hallo **waarschuwing** kolom en klik vervolgens op **wissen** nadat u hebt geselecteerd Hallo alle waarschuwingen toobe gewist.

Wanneer u klikt op **wissen**, hebt u Hallo kans tooprovide opmerkingen over Hallo waarschuwing en Hallo stappen die u hebt ondernomen tooresolve Hallo probleem. 

![Waarschuwing opmerkingen](./media/storsimple-virtual-array-manage-alerts/alerts17.png)

Sommige gebeurtenissen worden gewist door Hallo systeem als een andere gebeurtenis wordt geactiveerd met nieuwe informatie. 

## <a name="sort-and-review-alerts"></a>Sorteren en bekijk waarschuwingen

Hallo **waarschuwingen** blade kan maximaal too250 waarschuwingen weergeven. Als u dat aantal waarschuwingen hebben overschreden, wordt niet alle waarschuwingen weergegeven in de standaardweergave Hallo. U kunt combineren Hallo na velden toocustomize welke waarschuwingen worden weergegeven:

* **Status** – u kunt ofwel weergeven **Active** of **uitgeschakeld** waarschuwingen. Actieve waarschuwingen zijn nog steeds op het systeem geactiveerd terwijl gewiste waarschuwingen zijn handmatig worden gewist door een beheerder of programmatisch gewist omdat Hallo systeem Hallo meldingsvoorwaarde met nieuwe informatie bijgewerkt.
* **Ernst** – u kunt waarschuwingen van alle niveaus (kritiek, waarschuwing, informatie) of alleen een bepaalde ernst, zoals alleen kritieke waarschuwingen weergeven.
* **Bron** : U kunt waarschuwingen van alle bronnen weergegeven of beperken Hallo waarschuwingen toothose die afkomstig zijn van de service hello of een of alle virtuele apparaten Hallo.
* **Tijdsbereik** – door te geven Hallo **van** en **naar** datums en tijdstempels, kunt u bekijken waarschuwingen tijdens Hallo periode waarin u geïnteresseerd bent in.

## <a name="alerts-quick-reference"></a>Naslaggids voor waarschuwingen

Hallo tabellen na een overzicht van Hallo StorSimple waarschuwingen die u tegenkomen kunt, evenals aanvullende informatie en aanbevelingen indien beschikbaar. Virtuele StorSimple-matrix waarschuwingen kunnen worden onderverdeeld in een van de volgende categorieën Hallo:

* [Connectiviteitswaarschuwingen cloud](#cloud-connectivity-alerts)
* [Configuratiewaarschuwingen](#configuration-alerts)
* [Waarschuwingen met betrekking tot taak](#job-failure-alerts)
* [Waarschuwingen over toepassingsprestaties](#performance-alerts)
* [Beveiligingswaarschuwingen](#security-alerts)
* [Waarschuwingen bijwerken](#update-alerts)

### <a name="cloud-connectivity-alerts"></a>Connectiviteitswaarschuwingen cloud

| Tekst van de waarschuwing | Gebeurtenis | Meer informatie / aanbevolen acties |
|:--- |:--- |:--- |
| Apparaat  *<device name>*  is niet verbonden toohello cloud. |Hallo apparaat met de naam kan geen verbinding toohello cloud. |Kan geen verbinding maken toohello cloud. Dit kan worden veroorzaakt door tooone van Hallo volgende:<ul><li>Het is mogelijk een probleem met het Hallo-netwerkinstellingen op uw apparaat.</li><li>Het is mogelijk een probleem met opslagaccountreferenties Hallo.</li></ul>Ga voor meer informatie over het oplossen van problemen met de netwerkverbinding toohello [lokale webgebruikersinterface](storsimple-ova-web-ui-admin.md) Hallo-apparaat. |

### <a name="configuration-alerts"></a>Configuratiewaarschuwingen

| Tekst van de waarschuwing | Gebeurtenis | Meer informatie / aanbevolen acties |
|:--- |:--- |:--- |
| Een on-premises virtuele apparaatconfiguratie niet ondersteund. |Trage prestaties. |de huidige configuratie Hallo kan leiden tot verminderde prestaties. Zorg ervoor dat uw server voldoet aan de minimale configuratievereisten Hallo. Voor meer informatie gaat te[StorSimple-vereisten voor virtuele matrix](storsimple-ova-system-requirements.md). |
| U worden uitgevoerd buiten de ingerichte schijfruimte beschikbaar op <*apparaatnaam*>. |Waarschuwing voor schijf-ruimte. |U weinig schijfruimte ingericht. toofree ruimte, houd rekening met het verplaatsen van werkbelastingen tooanother volume of share of het verwijderen van gegevens. |

### <a name="job-failure-alerts"></a>Waarschuwingen met betrekking tot taak

| Tekst van de waarschuwing | Gebeurtenis | Meer informatie / aanbevolen acties |
|:--- |:--- |:--- |
| Back-up van <*apparaatnaam*> kan niet worden voltooid. |Back-uptaak is mislukt. |Kan een back-up niet maken. Houd rekening met een van de volgende Hallo:<ul><li>Verbindingsproblemen kunnen verhinderen Hallo back-upbewerking is voltooid. Zorg ervoor dat er geen verbindingsproblemen zijn. Ga voor meer informatie over het oplossen van problemen met de netwerkverbinding toohello [lokale webgebruikersinterface](storsimple-ova-web-ui-admin.md) voor uw virtuele apparaat.</li><li>U hebt Hallo beschikbaar opslaglimiet bereikt. toofree ruimte, houd rekening met het verwijderen van een back-ups die niet langer nodig zijn.</li></ul> Hallo-problemen oplossen, schakelt u de waarschuwing Hallo en probeer Hallo opnieuw. |
| Klonen van <*apparaatnaam*> kan niet worden voltooid. |Kloon de taak is mislukt. |Kan een kloon niet maken. Houd rekening met een van de volgende Hallo:<ul><li>Uw back-lijst is mogelijk niet geldig. Vernieuw Hallo lijst tooverify nog geldig is.</li><li>Verbindingsproblemen kunnen verhinderen Hallo kloonbewerking is voltooid. Zorg ervoor dat er geen verbindingsproblemen zijn.</li><li>U hebt Hallo beschikbaar opslaglimiet bereikt. toofree ruimte, houd rekening met het verwijderen van een back-ups die niet langer nodig zijn.</li></ul>Hallo-problemen oplossen, schakelt u de waarschuwing Hallo en probeer Hallo opnieuw. |

### <a name="performance-alerts"></a>Waarschuwingen over toepassingsprestaties

| Tekst van de waarschuwing | Gebeurtenis | Meer informatie / aanbevolen acties |
|:--- |:--- |:--- |
| Er onverwachte vertragingen bij de overdracht van gegevens. |Trage gegevensoverdracht. |Bandbreedtebeperking fouten optreden wanneer u Hallo schaalbaarheidsdoelen van een opslagservice overschrijdt. Hallo storage-service biedt deze tooensure geen enkele client of de tenant Hallo-service op Hallo kosten van anderen kunt gebruiken. Voor meer informatie over het oplossen van uw Azure storage-account, gaat u te[Monitor, vaststellen en oplossen van Microsoft Azure Storage](../storage/common/storage-monitoring-diagnosing-troubleshooting.md). |
| Er bijna geen schijfruimte lokale reservering op <*apparaatnaam*>. |Langzame reactietijd. |10% van Hallo totale grootte van de ingerichte voor <*apparaatnaam*> is gereserveerd op Hallo lokale apparaat en u bent nu nog maar weinig op Hallo ruimte gereserveerde. Hallo werkbelasting op <*apparaatnaam*> genereert een hogere snelheid van het verloop of u mogelijk hebt onlangs gemigreerd een grote hoeveelheid gegevens. Hierdoor kunnen de prestaties verminderen. Kunt u een van Hallo na acties tooresolve dit:<ul><li>Hallo cloud bandbreedte toothis apparaat verhogen.</li><li>Verminder of verplaatsen van werkbelastingen tooanother volume of share.</li></ul> |

### <a name="security-alerts"></a>Beveiligingswaarschuwingen

| Tekst van de waarschuwing | Gebeurtenis | Meer informatie / aanbevolen acties |
|:--- |:--- |:--- |
| Wachtwoord voor <*apparaatnaam*> verloopt over <*getal*> dagen. |Waarschuwing: wachtwoord. |Uw wachtwoord verloopt < nummer < dagen. U kunt uw wachtwoord te wijzigen. Voor meer informatie gaat te[wijziging Hallo virtuele StorSimple-matrix wachtwoord apparaatbeheerder](storsimple-virtual-array-change-device-admin-password.md). |

### <a name="update-alerts"></a>Waarschuwingen bijwerken

| Tekst van de waarschuwing | Gebeurtenis | Meer informatie / aanbevolen acties |
|:--- |:--- |:--- |
| Er zijn nieuwe updates beschikbaar zijn voor uw apparaat. |Updates toohello virtuele StorSimple-matrix zijn beschikbaar. |U kunt nieuwe updates installeren vanaf Hallo **onderhoud** pagina. |
| Kan niet gescand op nieuwe updates op <*apparaatnaam*>. |Bijwerken is mislukt. |Er is een fout opgetreden tijdens het installeren van nieuwe updates. U kunt handmatig Hallo updates installeren. Als Hallo probleem zich blijft voordoen, neem dan contact op met [Microsoft Support](storsimple-contact-microsoft-support.md). |

## <a name="next-steps"></a>Volgende stappen

* [Meer informatie over virtuele StorSimple-matrix Hallo](storsimple-ova-overview.md).

