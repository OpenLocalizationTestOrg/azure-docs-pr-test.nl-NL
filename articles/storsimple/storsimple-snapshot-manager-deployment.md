---
title: aaaDeploy StorSimple Snapshot Manager | Microsoft Docs
description: Meer informatie over hoe Hallo StorSimple Snapshot Manager een MMC-module voor het beheren van StorSimple-beveiliging en back-up gegevensfuncties toodownload downloaden en installeren.
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: f0128f57-519e-49ec-9187-23575809cdbe
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: dd90cca2bbb3410bb8cd459fb1a3ff3fb5f2997b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-snapshot-manager-mmc-snap-in"></a>Hallo StorSimple Snapshot Manager MMC-module implementeren

## <a name="overview"></a>Overzicht
Hallo StorSimple Snapshot Manager is een module Microsoft Management Console (MMC) die vereenvoudigt de bescherming van gegevens en back-beheer in een Microsoft Azure StorSimple-omgeving. Met StorSimple Snapshot Manager kunt u Microsoft Azure StorSimple lokale beheren en dus processen voor back-up en herstel vereenvoudigen en de kosten te verlagen als een volledig geïntegreerde opslagsysteem cloudopslag. 

Deze zelfstudie wordt beschreven configuratievereisten, evenals de procedures voor het installeren, verwijderen en StorSimple Snapshot Manager upgraden.

> [!NOTE]
> * U kunt StorSimple Snapshot Manager toomanage Microsoft Azure StorSimple virtuele matrices (ook wel bekend als StorSimple on-premises virtuele apparaten) niet gebruiken.
> * Als u van plan tooinstall StorSimple Update 2 op uw StorSimple-apparaat bent, toodownload Hallo meest recente versie ervoor van StorSimple Snapshot Manager en het installeren **voordat u het StorSimple Update 2 installeert**. Hallo meest recente versie van StorSimple Snapshot Manager is achterwaarts compatibel en werkt met alle uitgebrachte versies van Microsoft Azure StorSimple. Als u Hallo eerdere versie van StorSimple Snapshot Manager gebruikt, moet u tooupdate it (u hoeft niet toouninstall Hallo vorige versie voordat u de nieuwe versie Hallo installeren).


## <a name="storsimple-snapshot-manager-installation"></a>StorSimple Snapshot Manager-installatie
StorSimple Snapshot Manager kan worden geïnstalleerd op computers met Hallo Windows Server 2008 R2 SP1, Windows Server 2012 of Windows Server 2012 R2-besturingssysteem. Op servers met Windows 2008 R2, moet u ook Windows Server 2008 SP1 en Windows Management Framework 3.0 installeren.

Voordat u installeren of Hallo StorSimple Snapshot Manager-module voor Hallo Microsoft Management Console (MMC upgraden), zorg ervoor dat Microsoft Azure StorSimple-apparaat Hallo en host-server correct zijn geconfigureerd.

## <a name="configure-prerequisites"></a>Vereisten configureren
Hallo volgende stappen bevatten een overzicht van configuratietaken die u uitvoeren moet voordat u Hallo StorSimple Snapshot Manager installeert. Voor volledige Microsoft Azure StorSimple-configuratie en installatie-informatie, met inbegrip van de systeemvereisten en stapsgewijze instructies raadpleegt u [uw on-premises StorSimple-apparaat implementeren](storsimple-8000-deployment-walkthrough-u2.md).

> [!IMPORTANT]
> Voordat u begint, controleert u Hallo [Configuratiecontrolelijst voor implementatie](storsimple-8000-deployment-walkthrough-u2.md#deployment-configuration-checklist) en en [implementatievereisten](storsimple-8000-deployment-walkthrough-u2.md#deployment-prerequisites) in [uw on-premises StorSimple-apparaat implementeren](storsimple-8000-deployment-walkthrough-u2.md).
> <br>
> 
> 

### <a name="before-you-install-storsimple-snapshot-manager"></a>Voordat u StorSimple Snapshot Manager installeren
1. Uitpakken, te koppelen en Hallo Microsoft Azure StorSimple-apparaat verbindt, zoals is beschreven [uw StorSimple 8100-apparaat installeert](storsimple-8100-hardware-installation.md) of [uw StorSimple 8600-apparaat installeert](storsimple-8600-hardware-installation.md).
2. Zorg ervoor dat de hostcomputer een Hallo volgende besturingssystemen wordt uitgevoerd:
   
   * Windows Server 2008 R2 (op servers met Windows 2008 R2, moet u ook installeren Windows Server 2008 SP1 en Windows Management Framework 3.0)
   * Windows Server 2012
   * Windows Server 2012 R2
     
     Voor een virtueel StorSimple-apparaat moet Hallo host een virtuele Machine van de Microsoft Azure.
3. Zorg ervoor dat u voldoet aan alle vereisten voor de Hallo Microsoft Azure StorSimple-configuraties. Voor meer informatie gaat te[implementatievereisten](storsimple-8000-deployment-walkthrough-u2.md#deployment-prerequisites).
4. Hallo apparaat toohello host verbinden en voer een initiële configuratie Hallo. Voor meer informatie gaat te[implementatiestappen](storsimple-8000-deployment-walkthrough-u2.md#deployment-steps).
5. Maken van volumes op Hallo-apparaat, ze toohello host toewijzen en controleren die host hello te koppelen en ze gebruiken. StorSimple Snapshot Manager ondersteunt de volgende typen volumes Hallo:
   
   * Basic-volumes
   * Eenvoudige volumes
   * Dynamische volumes
   * Gespiegelde dynamische volumes (RAID-1)
   * Gedeelde clustervolumes
     
     Voor informatie over het maken van volumes op Hallo StorSimple-apparaat of virtueel StorSimple-apparaat gaat te[stap 6: een volume maken](storsimple-8000-deployment-walkthrough-u2.md#step-6-create-a-volume)in [uw on-premises StorSimple-apparaat implementeren](storsimple-8000-deployment-walkthrough-u2.md).

## <a name="install-a-new-storsimple-snapshot-manager"></a>Een nieuwe StorSimple Snapshot Manager installeren
Voordat u StorSimple Snapshot Manager installeert, zorg ervoor dat Hallo volumes die u hebt gemaakt op Hallo StorSimple-apparaat of virtueel StorSimple-apparaat zijn gekoppeld, geïnitialiseerd en geformatteerd zoals beschreven in [vereisten configureren](#configure-prerequisites).

> [!IMPORTANT]
> * Voor een virtueel StorSimple-apparaat moet Hallo host een virtuele Machine van de Microsoft Azure. 
> * Hallo-host moet worden uitgevoerd, Windows 2008 R2, Windows Server 2012 of Windows Server 2012 R2. Als Windows Server 2008 R2 wordt uitgevoerd op uw server, moet u ook de Windows Server 2008 SP1 en Windows Management Framework 3.0 installeren.
> * Voordat u Hallo apparaat tooStorSimple Snapshot Manager verbinding kan maken, moet u een iSCSI-verbinding van Hallo host toohello StorSimple-apparaat configureren.

Volg deze stappen toocomplete een nieuwe installatie van StorSimple Snapshot Manager. Als u een upgrade installeren wilt, gaat u verder te[bijwerken of opnieuw installeren van StorSimple Snapshot Manager](#upgrade-or-reinstall-storsimple-snapshot-manager).

* Stap 1: StorSimple Snapshot Manager installeren 
* Stap 2: Verbinding maken met de StorSimple Snapshot Manager tooa apparaat 
* Stap 3: Hallo verbinding toohello apparaat controleren 

### <a name="step-1-install-storsimple-snapshot-manager"></a>Stap 1: StorSimple Snapshot Manager installeren
Volgende stappen tooinstall StorSimple Snapshot Manager hello gebruiken.

#### <a name="tooinstall-storsimple-snapshot-manager"></a>tooinstall StorSimple Snapshot Manager
1. Hallo StorSimple Snapshot Manager-software downloaden (Ga te[StorSimple Snapshot Manager](https://www.microsoft.com/download/details.aspx?id=44220) in Hallo Microsoft Download Center) en sla het bestand lokaal op Hallo host.
2. In Verkenner met de rechtermuisknop op Hallo gecomprimeerde map en klik vervolgens op **alle uitpakken**.
3. In Hallo **gecomprimeerde extraheren (Zipped) mappen** in Hallo venster **Selecteer een doel en uitpakken van bestanden** vak typt of bladert u toohello pad waar u toofile toobe hebt uitgepakt wilt.
   
    > [!IMPORTANT]
    > U moet StorSimple Snapshot Manager installeren op station C: Hallo.
    
4. Selecteer Hallo **weergeven wanneer de volledige-bestanden hebt uitgepakt** selectievakje en klik vervolgens op **extraheren**.
   
    ![Dialoogvenster bestanden uitpakken](./media/storsimple-snapshot-manager-deployment/HCS_SSM_extract_files.png) 
5. Wanneer Hallo uitpakken is voltooid, wordt de doelmap Hallo geopend. Dubbelklik op Hallo toepassing setup die wordt weergegeven in de doelmap Hallo.
6. Wanneer Hallo **Setup Successful** bericht wordt weergegeven, klikt u op **sluiten**. U ziet Hallo StorSimple Snapshot Manager-pictogram op het bureaublad.
   
    ![pictogram op het bureaublad](./media/storsimple-snapshot-manager-deployment/HCS_SSM_desktop_icon.png) 

### <a name="step-2-connect-storsimple-snapshot-manager-tooa-device"></a>Stap 2: Verbinding maken met de StorSimple Snapshot Manager tooa apparaat
Hallo te volgen stappen tooconnect StorSimple Snapshot Manager tooa StorSimple-apparaat gebruiken.

#### <a name="tooconnect-storsimple-snapshot-manager-tooa-device"></a>tooconnect StorSimple Snapshot Manager tooa apparaat
1. Klik op Hallo StorSimple Snapshot Manager-pictogram op het bureaublad. Hallo StorSimple Snapshot Manager-venster wordt weergegeven. Hallo-venster bevat een **bereik** deelvenster een **resultaten** deelvenster en een **acties** deelvenster. 
   
    ![StorSimple Snapshot Manager-gebruikersinterface](./media/storsimple-snapshot-manager-deployment/HCS_SSM_gui_panes.png)
   
   * Hallo **bereik** deelvenster (Hallo linker deelvenster) bevat een lijst met knooppunten in een boomstructuur gerangschikt. U kunt sommige knooppunten tooselect een weergave of specifieke gegevens gerelateerde toothat knooppunt uitvouwen. Klik op Hallo pijl pictogram tooexpand of een knooppunt samenvouwen. Met de rechtermuisknop op een item in Hallo **bereik** deelvenster toosee een lijst met beschikbare acties voor dat het item.
   * Hallo **resultaten** deelvenster (Hallo middelste deelvenster) bevat gedetailleerde statusinformatie over Hallo-knooppunt, weergave of gegevens die u hebt geselecteerd in Hallo **bereik** deelvenster.
   * Hallo **acties** deelvenster vindt u Hallo-bewerkingen die u kunt uitvoeren op Hallo-knooppunt, weergeven of gegevens die u hebt geselecteerd in Hallo **bereik** deelvenster.
     
     Zie voor een volledige beschrijving van de gebruikersinterface voor StorSimple Snapshot Manager Hallo [StorSimple Snapshot Manager-gebruikersinterface](storsimple-use-snapshot-manager.md).
2. In Hallo **bereik** deelvenster, klik met de rechtermuisknop Hallo **apparaten** knooppunt en klik vervolgens op **configureren van een apparaat**. Hallo **configureren van een apparaat** dialoogvenster wordt weergegeven.
   
    ![Een apparaat configureren](./media/storsimple-snapshot-manager-deployment/HCS_SSM_config_device.png) 
3. In Hallo **apparaat** lijst vak, selecteer Hallo IP-adres van Hallo Microsoft Azure StorSimple-apparaat of het virtuele apparaat. In Hallo **wachtwoord** tekstvak, type Hallo wachtwoord StorSimple Snapshot Manager die u hebt gemaakt voor Hallo-apparaat in hello Azure-portal. Klik op **OK**.
4. StorSimple Snapshot Manager zoekt naar Hallo-apparaat dat u hebt geïdentificeerd. Als het Hallo-apparaat beschikbaar is, voegt StorSimple Snapshot Manager een verbinding. U kunt [Hallo verbinding toohello apparaat controleren](#to-verify-the-connection) tooconfirm dat connection Hallo is toegevoegd.
   
    Als het Hallo-apparaat voor een of andere reden niet beschikbaar is, retourneert StorSimple Snapshot Manager een foutbericht weergegeven. Klik op **OK** tooclose Hallo foutbericht wordt weergegeven en klik vervolgens op **annuleren** tooclose hello **configureren van een apparaat** in het dialoogvenster.
5. Wanneer deze tooa apparaat verbinding maakt, importeert StorSimple Snapshot Manager elke groep volume is geconfigureerd voor het apparaat, mits hello groep volume is gekoppeld back-ups. Volume-groepen die u geen gekoppelde back-ups hebt zijn niet geïmporteerd. Daarnaast worden back-upbeleid die zijn gemaakt voor een groep volume niet geïmporteerd. toosee Hallo geïmporteerde groepen, met de rechtermuisknop op de bovenste Hallo **Volume groepen** knooppunt in Hallo **bereik** deelvenster en klik op **schakelen geïmporteerde groepen**.

### <a name="step-3-verify-hello-connection-toohello-device"></a>Stap 3: Hallo verbinding toohello apparaat controleren
Gebruik hello te volgen stappen tooverify dat StorSimple Snapshot Manager verbonden toohello StorSimple-apparaat is.

#### <a name="tooverify-hello-connection"></a>tooverify hello verbinding
1. In Hallo **bereik** deelvenster, klikt u op Hallo **apparaten** knooppunt.
   
    ![De apparaatstatus StorSimple Snapshot Manager](./media/storsimple-snapshot-manager-deployment/HCS_SSM_Device_status.png) 
2. Controleer de Hallo **resultaten** deelvenster: 
   
   * Als een groene indicator wordt weergegeven op het pictogram van het apparaat Hallo en **beschikbaar** wordt weergegeven in Hallo **Status** kolom, klikt u vervolgens Hallo-apparaat is verbonden. 
   * Als een rode indicator wordt weergegeven op het pictogram van het apparaat Hallo en niet beschikbaar in Hallo **Status** kolom, klikt u vervolgens Hallo-apparaat niet is verbonden. 
   * Als **Refreshing** wordt weergegeven in Hallo **Status** kolom en vervolgens StorSimple Snapshot Manager haalt volume groepen en gekoppelde back-ups voor een verbonden apparaat.

## <a name="upgrade-or-reinstall-storsimple-snapshot-manager"></a>Bijwerken of opnieuw installeren van StorSimple Snapshot Manager
U moet StorSimple Snapshot Manager volledig verwijderen voordat u bijwerkt of Hallo software opnieuw te installeren. 

Voordat u opnieuw StorSimple Snapshot Manager installeert, back-up Hallo bestaande StorSimple Snapshot Manager-database op de hostcomputer Hallo. Dit bespaart Hallo back-beleid en de configuratie-informatie, zodat u deze gegevens gemakkelijk vanuit back-up herstellen kunt.

Volg deze stappen als u een upgrade of StorSimple Snapshot Manager opnieuw te installeren:

* Stap 1: StorSimple Snapshot Manager verwijderen 
* Stap 2: Back-up Hallo StorSimple Snapshot Manager-database 
* Stap 3: Installeer StorSimple Snapshot Manager en Hallo-database herstellen 

### <a name="step-1-uninstall-storsimple-snapshot-manager"></a>Stap 1: StorSimple Snapshot Manager verwijderen
Volgende stappen toouninstall StorSimple Snapshot Manager hello gebruiken.

#### <a name="toouninstall-storsimple-snapshot-manager"></a>toouninstall StorSimple Snapshot Manager
1. Open op de hostcomputer Hallo Hallo **Configuratiescherm**, klikt u op **programma's**, en klik vervolgens op **programma's en onderdelen**.
2. Klik in het linkerdeelvenster Hallo **een programma verwijderen of wijzigen**.
3. Met de rechtermuisknop op **StorSimple Snapshot Manager**, en klik vervolgens op **verwijderen**.
4. Hiermee start u Hallo StorSimple Snapshot Manager-Setup-programma. Klik op **Setup wijzigen**, en klik vervolgens op **verwijderen**.
   
   > [!NOTE]
   > Als er MMC processen Hallo achtergrond actief zijn, zoals StorSimple Snapshot Manager of Schijfbeheer, Hallo verwijderen mislukt en u een bericht tooclose ontvangt alle exemplaren van MMC voordat u probeert toouninstall Hallo programma. Selecteer **automatisch sluiten van toepassingen en toorestart ze nadat setup is voltooid opnieuw proberen**, en klik vervolgens op **OK**.
   > 
   > 
5. Wanneer de installatie van Hallo proces is voltooid, een **Setup Successful** bericht wordt weergegeven. Klik op **Sluiten**.

### <a name="step-2-back-up-hello-storsimple-snapshot-manager-database"></a>Stap 2: Back-up Hallo StorSimple Snapshot Manager-database
Gebruik van Hallo toocreate stappen te volgen en sla een kopie van Hallo StorSimple Snapshot Manager-database.

#### <a name="tooback-up-hello-database"></a>tooback up Hallo-database
1. Hallo Microsoft StorSimple Management-Service stoppen:
   
   1. Start Serverbeheer.
   2. Op Hallo Dashboard van Serverbeheer op Hallo **extra** selecteert u **Services**.
   3. Op Hallo **Services** pagina **Microsoft StorSimple Management Service**.
   4. In Hallo rechtermuisknop deelvenster onder **Microsoft StorSimple Management Service**, klikt u op **Hallo-service stoppen**.
      
        ![Hallo Apparaatbeheer StorSimple-service niet stoppen](./media/storsimple-snapshot-manager-deployment/HCS_SSM_stop_service.png)
2. Blader tooC:\ProgramData\Microsoft\StorSimple\BACatalog. 
   
   > [!NOTE]
   > ProgramData is een verborgen map.
  
3. Hallo catalogus XML-bestand, Hallo-bestand kopiëren en opslaan Hallo kopiëren zoeken in een veilige locatie of in Hallo cloud.
   
    ![StorSimple-bestand voor back-upcatalogus](./media/storsimple-snapshot-manager-deployment/HCS_SSM_bacatalog.png)
4. Opnieuw opstarten Hallo StorSimple Management-Service van Microsoft: 
   
   1. Op Hallo Dashboard van Serverbeheer op Hallo **extra** selecteert u **Services**.
   2. Op Hallo **Services** pagina, selecteer Hallo **StorSimple Management Servic**e.
   3. In Hallo rechtermuisknop deelvenster onder **Microsoft StorSimple Management Service**, klikt u op **Hallo-service opnieuw starten**. 

### <a name="step-3-reinstall-storsimple-snapshot-manager-and-restore-hello-database"></a>Stap 3: Installeer StorSimple Snapshot Manager en Hallo-database herstellen
tooreinstall StorSimple Snapshot Manager Hallo stappen in [installeren van een nieuwe StorSimple Snapshot Manager](#install-a-new-storsimple-snapshot-manager). Gebruik vervolgens hello te volgen procedure toorestore hello StorSimple Snapshot Manager-database.

#### <a name="toorestore-hello-database"></a>toorestore hello database
1. Hallo Microsoft StorSimple Management-Service stoppen:
   
   1. Start Serverbeheer.
   2. Op Hallo Dashboard van Serverbeheer op Hallo **extra** selecteert u **Services**.
   3. Op Hallo **Services** pagina **Microsoft StorSimple Management Service**.
   4. In Hallo rechtermuisknop deelvenster onder **Microsoft StorSimple Management Service**, klikt u op **Hallo-service stoppen**.
2. Blader tooC:\ProgramData\Microsoft\StorSimple\BACatalog.
   
   > [!NOTE]
   > ProgramData is een verborgen map.
   > 
   > 
3. Hallo catalogus XML-bestand verwijderen en vervang deze door Hallo-versie die u eerder hebt opgeslagen.
4. Opnieuw opstarten Hallo StorSimple Management-Service van Microsoft: 
   
   1. Op Hallo Dashboard van Serverbeheer op Hallo **extra** selecteert u **Services**.
   2. Op Hallo **Services** pagina **Microsoft StorSimple Management Service**.
   3. In Hallo rechtermuisknop deelvenster onder **Microsoft StorSimple Management Service**, klikt u op **Hallo-service opnieuw starten**.

## <a name="next-steps"></a>Volgende stappen
* toolearn meer over StorSimple Snapshot Manager, gaat u te[wat is er StorSimple Snapshot Manager?](storsimple-what-is-snapshot-manager.md).
* toolearn meer informatie over Hallo StorSimple Snapshot Manager-gebruikersinterface, gaat u te[StorSimple Snapshot Manager-gebruikersinterface](storsimple-use-snapshot-manager.md).
* toolearn meer over het gebruik van StorSimple Snapshot Manager te gaan[gebruik StorSimple Snapshot Manager tooadminister uw StorSimple-oplossing](storsimple-snapshot-manager-admin.md).

