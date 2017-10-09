---
title: aaaManage apparaten met StorSimple Snapshot Manager | Microsoft Docs
description: Hierin wordt beschreven hoe toouse Hallo StorSimple Snapshot Manager MMC-module tooconnect en StorSimple-apparaten beheren.
services: storsimple
documentationcenter: 
author: SharS
manager: timlt
editor: 
ms.assetid: 966ecbe3-a7fa-4752-825f-6694dd949946
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 7a2a2ca830e4ea6eb4b01f2542958df3871c1700
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooconnect-and-manage-storsimple-devices"></a>StorSimple Snapshot Manager tooconnect gebruiken en beheren van StorSimple-apparaten
## <a name="overview"></a>Overzicht
Kunt u knooppunten in Hallo StorSimple Snapshot Manager **bereik** deelvenster tooverify geïmporteerde gegevens van StorSimple-apparaat en verbonden opslagapparaten te vernieuwen. Bovendien, als u klikt op Hallo **apparaten** knooppunt, ziet u een lijst van verbonden apparaten en de bijbehorende statusgegevens in Hallo **resultaten** deelvenster.

![Verbonden apparaten](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_connect_devices.png)

**Afbeelding 1: StorSimple Snapshot Manager aangesloten apparaat** 

Afhankelijk van uw **weergave** selecties, Hallo **resultaten** deelvenster bevat informatie over elk apparaat na Hallo. (Voor meer informatie over het configureren van een weergave te gaan[menu Beeld](storsimple-use-snapshot-manager.md#view-menu).

| Kolom | Beschrijving |
|:--- |:--- |
| Naam |Hallo-naam van Hallo apparaat zoals geconfigureerd in de klassieke Azure-portal Hallo |
| Model |Hallo modelnummer van Hallo-apparaat |
| Versie |Hallo-versie van het Hallo-software op Hallo apparaat geïnstalleerd |
| Status |Hiermee wordt aangegeven of Hallo-apparaat beschikbaar is |
| Laatste synchronisatie |Datum en tijd waarop Hallo apparaat voor het laatst is gesynchroniseerd |
| Serienummer |Hallo-serienummer voor Hallo-apparaat |

Als u met de rechtermuisknop op Hallo **apparaten** knooppunt in Hallo **bereik** deelvenster die u kunt kiezen uit Hallo van de volgende activiteiten:

* Toevoegen of vervangen van een apparaat
* Een apparaat aansluit en controleer of invoer
* Verbonden apparaten vernieuwen

Als u klikt op Hallo **apparaten** knooppunt en klik vervolgens met de rechtermuisknop op een apparaat een naam in Hallo **resultaten** deelvenster die u kunt kiezen uit Hallo van de volgende activiteiten:

* Een apparaat verifiëren
* Details van de apparaten weergeven
* Een apparaat vernieuwen
* De apparaatconfiguratie van een verwijderen
* Wachtwoord van een apparaat wijzigen

> [!NOTE]
> Al deze acties zijn ook beschikbaar in Hallo **acties** deelvenster.


Deze zelfstudie wordt uitgelegd hoe toouse StorSimple Snapshot Manager tooconnect en apparaten beheren en uitvoeren van Hallo taken te volgen:

* Toevoegen of vervangen van een apparaat
* Een apparaat aansluit en controleer of invoer
* Verbonden apparaten vernieuwen
* Een apparaat verifiëren
* Details van de apparaten weergeven
* Een afzonderlijk apparaat vernieuwen
* De apparaatconfiguratie van een verwijderen
* Een apparaatwachtwoord verlopen wijzigen
* Vervangen van een mislukte apparaat

> [!NOTE]
> Voor algemene informatie over het gebruik van Hallo StorSimple Snapshot Manager interface gaat te[StorSimple Snapshot Manager-gebruikersinterface](storsimple-use-snapshot-manager.md).


## <a name="add-or-replace-a-device"></a>Toevoegen of vervangen van een apparaat
Hallo te volgen procedure tooadd gebruiken of vervangen van een StorSimple-apparaat.

#### <a name="tooadd-or-replace-a-device"></a>tooadd of vervangen, een apparaat
1. Klik op Hallo bureaubladpictogram toostart StorSimple Snapshot Manager.
2. In Hallo **bereik** deelvenster, klik met de rechtermuisknop Hallo **apparaten** knooppunt en klik vervolgens op **configureren van een apparaat**. Hallo **configureren van een apparaat** dialoogvenster wordt weergegeven.
   
    ![Een StorSimple-apparaat configureren](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_config_device.png) 
3. In Hallo **apparaat** vervolgkeuzelijst, selecteer Hallo IP-adres van het Hallo-apparaat of virtueel apparaat. 
4. In Hallo **wachtwoord** tekstvak, type Hallo wachtwoord StorSimple Snapshot Manager die u hebt gemaakt voor Hallo-apparaat in Hallo klassieke Azure-portal. Klik op **OK**. StorSimple Snapshot Manager zoekt naar Hallo-apparaat dat u hebt geïdentificeerd. 
   
   * Als het Hallo-apparaat beschikbaar is, voegt StorSimple Snapshot Manager een verbinding.
   * Als het Hallo-apparaat voor een of andere reden niet beschikbaar is, retourneert StorSimple Snapshot Manager een foutbericht weergegeven. Klik op **OK** tooclose Hallo foutbericht wordt weergegeven en klik vervolgens op **annuleren** tooclose hello **configureren van een apparaat** in het dialoogvenster.

## <a name="connect-a-device-and-verify-imports"></a>Een apparaat aansluit en controleer of invoer
Hallo te volgen procedure tooconnect een StorSimple-apparaat gebruiken en controleren of een bestaande volume groepen die zijn gekoppeld aan back-ups zijn geïmporteerd.

#### <a name="tooconnect-a-device-and-verify-imports"></a>een apparaat tooconnect en controleer of de invoer
1. tooconnect een apparaat tooStorSimple Snapshot Manager, volg de aanwijzingen Hallo in toevoegen of vervangen van een apparaat. Wanneer deze tooa apparaat verbinding maakt, reageert StorSimple Snapshot Manager als volgt:
   
   * Als het Hallo-apparaat voor een of andere reden niet beschikbaar is, retourneert StorSimple Snapshot Manager een foutbericht weergegeven. 
   
   * Als het Hallo-apparaat beschikbaar is, voegt StorSimple Snapshot Manager een verbinding. Wanneer u Hallo apparaat selecteert, wordt deze weergegeven in Hallo **resultaten** deelvenster en Hallo statusveld geeft aan dat het Hallo-apparaat is **beschikbaar**. StorSimple Snapshot Manager importeert volume groepen geconfigureerd voor het Hallo-apparaat, mits Hallo volume groepen hebt gekoppeld aan back-ups. Back-upbeleid zijn niet geïmporteerd. Volume-groepen die u geen gekoppelde back-ups hebt zijn niet geïmporteerd.
2. Klik op Hallo bureaubladpictogram toostart StorSimple Snapshot Manager.
3. Klik met de rechtermuisknop Hallo hoofdknooppunt in Hallo **bereik** deelvenster en klik vervolgens op **wisselknop invoer weergave**.
   
    ![Selecteer wisselknop invoer weergeven](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Toggle_Imports_Display.png) 
4. Hallo **wisselknop invoer weergave** dialoogvenster wordt weergegeven, met de status Hallo Hallo geïmporteerd volume groepen en back-ups. Klik op **OK**.

Nadat de back-ups en Hallo volume groepen geïmporteerd zijn, kunt u StorSimple Snapshot Manager toomanage ze, net zoals u zou volume groepen en back-ups die u hebt gemaakt en geconfigureerd met StorSimple Snapshot Manager beheren. 

## <a name="refresh-connected-devices"></a>Verbonden apparaten vernieuwen
Hallo te volgen procedure toosynchronize Hallo verbonden StorSimple-apparaten met StorSimple Snapshot Manager gebruiken.

#### <a name="toorefresh-connected-devices"></a>toorefresh verbonden apparaten
1. Klik op Hallo bureaubladpictogram toostart StorSimple Snapshot Manager.
2. In Hallo **bereik** deelvenster met de rechtermuisknop op **apparaten**, en klik vervolgens op **apparaten vernieuwen**. Dit synchroniseert Hallo verbonden apparaten met StorSimple Snapshot Manager zodat u Hallo volume groepen en back-ups, met inbegrip van alle recente toevoegingen kunt weergeven. 
   
    ![Hallo StorSimple-apparaten vernieuwen](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Refresh_devices.png)

Hallo **apparaten vernieuwen** actie haalt nieuwe groepen volume en eventuele bijbehorende back-ups van verbonden apparaten. In tegenstelling tot Hallo **volumes opnieuw scannen** actie beschikbaar voor Hallo **Volumes** knooppunt **apparaten vernieuwen** Hallo reservekopie van het register niet hersteld.

## <a name="authenticate-a-device"></a>Een apparaat verifiëren
Hallo te volgen procedure tooauthenticate een StorSimple-apparaat met StorSimple Snapshot Manager gebruiken.

#### <a name="tooauthenticate-a-device"></a>een apparaat tooauthenticate
1. Klik op Hallo bureaubladpictogram toostart StorSimple Snapshot Manager.
2. In Hallo **bereik** deelvenster, klikt u op **apparaten**.
3. In Hallo **resultaten** deelvenster met de rechtermuisknop op Hallo van Hallo-apparaat en klik vervolgens op **verifiëren**.
4. Hallo **verifiëren** dialoogvenster wordt weergegeven. Typ het wachtwoord voor Hallo apparaat en klik vervolgens op **OK**.
   
    ![In het dialoogvenster verifiëren](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Authenticate.png) 

## <a name="view-device-details"></a>Details van de apparaten weergeven
Hallo onderstaande procedure tooview Hallo gegevens van een StorSimple-apparaat gebruikt en, indien nodig, opnieuw synchroniseren Hallo-apparaat met StorSimple Snapshot Manager.

#### <a name="tooview-and-resynchronize-device-details"></a>details van het apparaat tooview en opnieuw synchroniseren
1. Klik op Hallo bureaubladpictogram toostart StorSimple Snapshot Manager.
2. In Hallo **bereik** deelvenster, klikt u op **apparaten**.
3. In Hallo **resultaten** deelvenster met de rechtermuisknop op Hallo van Hallo-apparaat en klik vervolgens op **Details**.

4. Klik Hallo **Apparaatdetails** dialoogvenster wordt weergegeven. In dit vak weergegeven naam hello, model, versie, serienummer, status, iSCSI-doel Qualified Name (IQN) en laatste synchronisatiedatum en tijd.

* Klik op **Resync** toosynchronize Hallo apparaat.
* Klik op **OK** of **annuleren** tooclose Hallo dialoogvenster.
  
  ![Apparaatdetails](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Device_details.png) 

## <a name="refresh-an-individual-device"></a>Een afzonderlijk apparaat vernieuwen
Hallo te volgen procedure tooresynchronize een afzonderlijk StorSimple-apparaat met StorSimple Snapshot Manager gebruiken.

#### <a name="toorefresh-a-device"></a>een apparaat toorefresh
1. Klik op Hallo bureaubladpictogram toostart StorSimple Snapshot Manager. 
2. In Hallo **bereik** deelvenster, klikt u op **apparaten**. 
3. In Hallo **resultaten** deelvenster met de rechtermuisknop op Hallo van Hallo-apparaat en klik vervolgens op **apparaat vernieuwen**. Dit synchroniseert apparaat Hallo met StorSimple Snapshot Manager.

## <a name="delete-a-device-configuration"></a>De apparaatconfiguratie van een verwijderen
Hallo van StorSimple Snapshot Manager te volgen procedure toodelete een afzonderlijke configuratie van de StorSimple-apparaat gebruiken.

#### <a name="toodelete-a-device-configuration"></a>configuratie van een toodelete
1. Klik op Hallo bureaubladpictogram toostart StorSimple Snapshot Manager.
2. In Hallo **bereik** deelvenster, klikt u op **apparaten**. 
3. In Hallo **resultaten** deelvenster met de rechtermuisknop op Hallo van Hallo-apparaat en klik vervolgens op **verwijderen**. 
4. Hallo volgende bericht wordt weergegeven. Klik op **Ja** toodelete Hallo configuratie of klik op **Nee** toocancel Hallo verwijderen.
   
    ![Configureren van een apparaat verwijderen](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_DeleteDevice.png)

## <a name="change-an-expired-device-password"></a>Een apparaatwachtwoord verlopen wijzigen
U moet een wachtwoord tooauthenticate een StorSimple-apparaat met StorSimple Snapshot Manager invoeren. U kunt dit wachtwoord configureren wanneer u Hallo Windows PowerShell-interface tooset Hallo-apparaat gebruikt. Hallo wachtwoord kan echter verloopt. Als dit gebeurt, kunt u hello Azure classic portal toochange Hallo wachtwoord. Omdat Hallo-apparaat is in StorSimple Snapshot Manager geconfigureerd voordat Hallo wachtwoord verlopen, moet u vervolgens opnieuw Hallo-apparaat in StorSimple Snapshot Manager verifiëren.

#### <a name="toochange-hello-expired-password"></a>toochange hello verlopen wachtwoord
1. In de klassieke Azure-portal hello, Hallo StorSimple Manager-service te starten.
2. Klik op **apparaten** > **configureren** voor Hallo-apparaat.
3. Schuif naar beneden toohello StorSimple Snapshot Manager-sectie. Voer een wachtwoord 14-15 tekens. Zorg ervoor dat wachtwoord Hallo een combinatie van hoofdletters, kleine letters, numerieke en speciale tekens bevat.
4. Opnieuw invoeren Hallo wachtwoord tooconfirm deze.
5. Klik op **opslaan** Hallo Hallo pagina onderaan in.

#### <a name="toore-authenticate-hello-device"></a>toore-Hallo apparaat verifiëren
1. StorSimple Snapshot Manager start.
2. In Hallo **bereik** deelvenster, klikt u op **apparaten**. Een lijst met geconfigureerde apparaten wordt weergegeven in Hallo **resultaten** deelvenster.
3. Selecteer het Hallo-apparaat, klik met de rechtermuisknop en klik vervolgens op **verifiëren**.
4. In Hallo **verifiëren** venster Hallo nieuw wachtwoord invoeren.
5. Selecteer het Hallo-apparaat, klik met de rechtermuisknop en selecteer **vernieuwen apparaat**. Dit synchroniseert apparaat Hallo met StorSimple Snapshot Manager.

## <a name="replace-a-failed-device"></a>Vervangen van een mislukte apparaat
Als een StorSimple-apparaat mislukt en wordt hello vervangen door een apparaat stand-by (failover), gebruik Hallo tooconnect stappen te volgen toohello nieuw apparaat en bekijkt gekoppelde back-ups.

#### <a name="tooconnect-tooa-new-device-after-failover"></a>tooconnect tooa nieuw apparaat na een failover
1. Hallo iSCSI-verbinding toohello nieuwe apparaat opnieuw te configureren. Voor instructies gaat te ' stap 7: koppelen, initialiseren en een volume-indeling ' in [uw on-premises StorSimple-apparaat implementeren](storsimple-8000-deployment-walkthrough-u2.md).

> [!NOTE]
> Als Hallo nieuwe StorSimple-apparaat heeft hetzelfde IP-adres als Hallo oude hello, bent u mogelijk kunnen tooconnect Hallo oude configuratie.


1. Hallo Microsoft StorSimple Management-Service stoppen:
   
   1. Start Serverbeheer.
   2. Op Hallo Dashboard van Serverbeheer op Hallo **extra** selecteert u **Services**.
   3. Op Hallo **Services** venster, selecteer Hallo **Microsoft StorSimple Management Service**.
   4. In Hallo rechtermuisknop deelvenster onder **Microsoft StorSimple Management Service**, klikt u op **Hallo-service stoppen**.
2. Hallo configuratie informatie gerelateerde toohello oude apparaat verwijderen:
   
   1. Blader in Windows Verkenner tooC:\ProgramData\Microsoft\StorSimple\BACatalog.
   2. Hallo-bestanden in Hallo BACatalog map verwijderen.
3. Opnieuw opstarten Hallo StorSimple Management-Service van Microsoft:
   
   1. Op Hallo Dashboard van Serverbeheer op Hallo **extra** selecteert u **Services**.
   2. Op Hallo **Services** venster, selecteer Hallo **Microsoft StorSimple Management Service**.
   3. In Hallo rechtermuisknop deelvenster onder **Microsoft StorSimple Management Service**, klikt u op **Hallo-service opnieuw starten**.
4. StorSimple Snapshot Manager start.
5. StorSimple-apparaat voor tooconfigure Hallo nieuwe, volledige Hallo stappen in stap 2: verbinding maken met een virtueel StorSimple-apparaat in [implementeren StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md).
6. Klik met de rechtermuisknop Hallo op het hoogste niveau knooppunt in Hallo **bereik** deelvenster (StorSimple Snapshot Manager in Hallo voorbeeld) en klik vervolgens op **wisselknop invoer weergave**. 
7. Er verschijnt een bericht wanneer Hallo volume groepen geïmporteerd en back-ups zichtbaar in StorSimple Snapshot Manager zijn. Klik op **OK**.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe te[StorSimple Snapshot Manager tooadminister uw StorSimple-oplossing gebruiken](storsimple-snapshot-manager-admin.md).
* Meer informatie over hoe te[StorSimple Snapshot Manager tooview gebruiken en beheren van volumes](storsimple-snapshot-manager-manage-volumes.md).

