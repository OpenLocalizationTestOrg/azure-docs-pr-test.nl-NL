---
title: aaaConfigure MPIO op de host verbonden tooStorSimple virtuele matrix | Microsoft Docs
description: Hierin wordt beschreven hoe tooconfigure Multipath I/O (MPIO) voor uw virtuele StorSimple-matrix met elkaar verbonden tooa host waarop Windows Server 2012 R2 wordt uitgevoerd.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 5b7a7f99-ee5b-4b7d-ab32-483a5a1fa504
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/01/2017
ms.author: alkohli
ms.openlocfilehash: 0e6df23bba29395329685cbf2c968675abb04cfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multipath-io-on-windows-server-host-for-hello-storsimple-virtual-array"></a>Multipath i/o op Windows Server-host voor virtuele StorSimple-matrix Hallo configureren
## <a name="overview"></a>Overzicht
Dit artikel wordt beschreven hoe tooinstall MPIO-functie (MPIO) op de host Windows Server specifieke configuratie-instellingen voor alleen-StorSimple-volumes van toepassing en controleer vervolgens MPIO voor StorSimple-volumes. Hallo procedure wordt ervan uitgegaan dat uw virtuele StorSimple-1200-matrix met twee netwerkinterfaces verbonden tooa Windows Server-host met twee netwerkinterfaces. Hallo-informatie in dit artikel is van toepassing alleen toohello virtuele matrix. Voor informatie over apparaten van de serie StorSimple 8000, ga te[MPIO configureren voor StorSimple host](storsimple-configure-mpio-windows-server.md). 

Hallo MPIO-functie in Windows Server helpt build maximaal beschikbare en fouttolerantie opslagconfiguraties. MPIO maakt gebruik van componenten van fysieke paden redundante-adapters, kabels en switches: toocreate logische paden tussen Hallo-server en het Hallo-opslagapparaat. Als er een onderdeelfout, overgestapt waardoor een toofail logische pad gebruik van meerdere paden op een alternatief pad voor i/o zodat toepassingen steeds toegang hun gegevens tot nog. Bovendien afhankelijk van uw configuratie kan MPIO ook prestaties verbeteren door opnieuw Hallo werklast te verdelen over alle deze paden. Zie voor meer informatie [MPIO overzicht](https://technet.microsoft.com/library/cc725907.aspx "MPIO overzicht en kenmerken").

Voor Hallo hoge beschikbaarheid van uw StorSimple-oplossing, moet u MPIO configureren op Hallo van Windows Server-hosts verbonden tooyour virtuele StorSimple-matrix (model 1200). Hallo-hostservers tolereert vervolgens een koppeling-, netwerk- of Interfacefout. 

U moet deze stappen tooconfigure MPIO toofollow: 

* Configuratievereisten
* Stap 1: Installeer de MPIO op Hallo Windows Server-host
* Stap 2: MPIO configureren voor StorSimple-volumes
* Stap 3: Koppelpunt StorSimple-volumes op Hallo host

Elk Hallo bovenstaande stappen wordt besproken in Hallo uit te voeren.

## <a name="prerequisites"></a>Vereisten
In deze sectie beschrijft Hallo-configuratievereisten voor Windows Server-host Hallo en uw virtuele matrix.

### <a name="on-windows-server-host"></a>Op Windows Server-host
* Zorg ervoor dat uw Windows Server-host 2 netwerkinterfaces ingeschakeld heeft.

### <a name="on-storsimple-virtual-array"></a>Op de virtuele StorSimple-matrix
* Hallo virtuele matrix moet worden geconfigureerd als een iSCSI-server. toolearn meer, Zie [virtuele matrix als iSCSI-server instellen](storsimple-virtual-array-deploy3-iscsi-setup.md). Een of meer netwerkinterfaces moeten zijn ingeschakeld op Hallo matrix.   
* Hallo-netwerkinterfaces op uw virtuele matrix moeten bereikbaar zijn vanaf Hallo Windows Server-host.
* Een of meer volumes moeten worden gemaakt op uw virtuele StorSimple-matrix. toolearn meer, Zie [toevoegen van een volume](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume) op uw virtuele StorSimple-matrix. In deze procedure we 3 volumes (1 lokaal vastgemaakte en 2 gelaagde volumes zoals hieronder) gemaakt op de virtuele Hallo-matrix.
  
    ![mpio0](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio0.png)

### <a name="hardware-configuration-for-storsimple-virtual-array"></a>Hardwareconfiguratie voor virtuele StorSimple-matrix
Hallo afbeelding hieronder toont Hallo hardwareconfiguratie voor hoge beschikbaarheid en taakverdeling gebruik van meerdere paden voor uw Windows Server-host en virtuele StorSimple-matrix in deze procedure gebruikt.

![hardware-configuratie van MPIO](./media/storsimple-virtual-array-configure-mpio-windows-server/1200hardwareconfig.png)

Zoals u in de voorgaande afbeelding Hallo:

* Uw virtuele StorSimple-matrix is ingericht op Hyper-V is een enkel knooppunt active apparaat geconfigureerd als een iSCSI-server.
* Twee virtuele netwerkinterfaces zijn ingeschakeld op uw matrix. Hallo lokale webgebruikersinterface van uw virtuele matrix, controleert u of dat er twee netwerkinterfaces zijn ingeschakeld door te navigeren**netwerkinstellingen** zoals hieronder wordt weergegeven:
  
    ![Netwerkinterfaces die zijn ingeschakeld op 1200](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio9.png)
  
    Opmerking Hallo IPv4-adressen Hallo ingeschakeld netwerkinterfaces (Ethernet, Ethernet 2 standaard) en opslaan voor toekomstig gebruik op Hallo host.
* Twee netwerkinterfaces zijn ingeschakeld op uw Windows Server-host. Als hello verbonden interfaces voor de matrix en de host zich op hetzelfde subnet, Hallo wordt er 4 paden beschikbaar. Dit was Hallo geval in deze procedure. Echter, als elke netwerkinterface op Hallo matrix en host-interface op een ander IP-subnet (en niet-routeerbaar), vervolgens alleen 2 paden zijn beschikbaar.

## <a name="step-1-install-mpio-on-hello-windows-server-host"></a>Stap 1: Installeer de MPIO op Hallo Windows Server-host
MPIO is een optionele functie in Windows Server en wordt niet standaard geïnstalleerd. Het moet als een functie via Serverbeheer worden geïnstalleerd. tooinstall voltooien van deze functie op de host Windows Server Hallo procedure uitvoert.

[!INCLUDE [storsimple-install-mpio-windows-server-host](../../includes/storsimple-install-mpio-windows-server-host.md)]

## <a name="step-2-configure-mpio-for-storsimple-volumes"></a>Stap 2: MPIO configureren voor StorSimple-volumes
MPIO moet toobe geconfigureerd tooidentify StorSimple-volumes. tooconfigure MPIO toorecognize StorSimple-volumes, uitvoeren Hallo stappen te volgen.

[!INCLUDE [storsimple-configure-mpio-volumes](../../includes/storsimple-configure-mpio-volumes.md)]

## <a name="step-3-mount-storsimple-volumes-on-hello-host"></a>Stap 3: Koppelpunt StorSimple-volumes op Hallo host
Nadat MPIO op Windows Server is geconfigureerd, of meer volumes op Hallo StorSimple matrix gemaakt kan worden gekoppeld en kan vervolgens profiteren van MPIO voor redundantie. toomount een volume uitvoeren Hallo stappen te volgen.

#### <a name="toomount-volumes-on-hello-host"></a>toomount volumes op Hallo host
1. Open Hallo **eigenschappen iSCSI-Initiator** -venster op Hallo Windows Server-host. Ga te**Serverbeheer > Dashboard > Extra > iSCSI-Initiator**.
2. In Hallo **eigenschappen iSCSI-Initiator** in het dialoogvenster, klikt u op **detectie**, en klik vervolgens op **doelportaal detecteren**.
3. In Hallo **doelportaal detecteren** dialoogvenster vak, Hallo te volgen:
   
    1. Voer Hallo IP-adres van de eerste ingeschakelde-netwerkinterface Hallo op uw virtuele StorSimple-matrix. Standaard is dit **Ethernet**. 
    2. Klik op **OK** tooreturn toohello **eigenschappen iSCSI-Initiator** in het dialoogvenster.
     
    > [!IMPORTANT]
    > Als u van een particulier netwerk voor iSCSI-verbindingen gebruikmaakt, voert u Hallo IP-adres van Hallo gegevenspoort die is verbonden toohello privé-netwerk.
     
4. Herhaal stap 2-3 voor een tweede netwerkinterface (bijvoorbeeld Ethernet 2) in uw matrix. 
5. Selecteer Hallo **doelen** tabblad in Hallo **eigenschappen iSCSI-Initiator** in het dialoogvenster. Voor uw virtuele matrix ziet u elk volume oppervlak als doel onder **gedetecteerde doelen**. In dit geval zou drie doelen (overeenkomstige toothree volumes) worden gedetecteerd.
   
    ![mpio1](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio1.png)
6. Klik op **Connect** tooestablish een iSCSI-sessie met uw virtuele StorSimple-matrix. Een **tooTarget verbinding** dialoogvenster wordt weergegeven. Selecteer Hallo **Multipath inschakelen** selectievakje. Klik op **geavanceerde**.
   
    ![mpio2](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio2.png)
7. In Hallo **geavanceerde instellingen** dialoogvenster vak, Hallo te volgen:                                        
   
    1. Op Hallo **lokale Adapter** vervolgkeuzelijst, selecteer **Microsoft iSCSI-Initiator**.
    2. Op Hallo **Initiator IP** vervolgkeuzelijst, selecteer Hallo IP-adres van Hallo host.
    3. Op Hallo **doelportal** IP-vervolgkeuzelijst, selecteer Hallo IP-adres van de interface matrix.
    4. Klik op **OK** tooreturn toohello **eigenschappen iSCSI-Initiator** in het dialoogvenster.
     
        ![mpio3](./media/storsimple-ova-configure-mpio-windows-server/mpio3.png)

8. Klik op **Eigenschappen**. 
   
    ![mpio4](./media/storsimple-ova-configure-mpio-windows-server/mpio4.png)

9. In Hallo **eigenschappen** in het dialoogvenster, klikt u op **sessie toevoegen**.
   
   ![mpio5](./media/storsimple-ova-configure-mpio-windows-server/mpio5.png)
10. In Hallo **verbinding tooTarget** dialoogvenster, selecteer Hallo **Multipath inschakelen** selectievakje. Klik op **geavanceerde**.
11. In Hallo **geavanceerde instellingen** in het dialoogvenster:                                        
    
    1. Op Hallo **lokale adapter** vervolgkeuzelijst, selecteer Microsoft iSCSI-Initiator.

    2. Op Hallo **Initiator IP** vervolgkeuzelijst, selecteer Hallo IP-adres bijbehorende toohello host. In dit geval u verbinding maakt twee netwerkinterfaces op Hallo matrix tooa één netwerkinterface op Hallo host. Deze interface is daarom Hallo hetzelfde als die opgegeven voor Hallo eerste sessie.

    3. Op Hallo **IP-adres van doel Portal** vervolgkeuzelijst, selecteer Hallo IP-adres voor Hallo tweede gegevens interface is ingeschakeld op Hallo matrix.

    4. Klik op **OK** tooreturn toohello iSCSI-Initiator eigenschappenvenster. U kunt een tweede sessie toohello doel hebt toegevoegd.
      
       ![mpio11](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio11.png)
    
    5. Na het toevoegen van Hallo gewenst sessies (paden) in Hallo **eigenschappen iSCSI-Initiator** dialoogvenster, selecteer Hallo doel en klik op **eigenschappen**. Op tabblad van sessies Hallo Hallo **eigenschappen** dialoogvenster, opmerking Hallo vier sessie-id's die overeenkomen met het aantal permutaties toohello-pad. toocancel een sessie, Hallo selectievakje volgende tooa sessie-id selecteren en klik vervolgens op **Disconnect**.

    6. tooview apparaten die zijn gepresenteerd in sessies, selecteer Hallo **apparaten** tabblad tooconfigure Hallo MPIO-beleid voor een geselecteerd apparaat, klikt u op **MPIO**.

    7. Hallo **Details** dialoogvenster wordt weergegeven. Op Hallo **MPIO** tabblad kunt u geschikte Hallo **taakverdelingsbeleid** instellingen. U kunt ook weergeven Hallo **Active** of **stand-by** padtype.
12. Herhaal stap 8 11 tooadd extra sessies (paden) toohello doel. U kunt een totaal van vier sessies voor elk doel toevoegen met twee interfaces op Hallo host en twee gegevensbronnen op de virtuele Hallo-matrix. 
    
    ![mpio14](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio14.png)
13. U moet toorepeat deze stappen voor elk volume (verwerkingsinformatie als doel).
    
    ![mpio15](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio15.png)
14. Open **Computerbeheer** door te navigeren**Serverbeheer > Dashboard > Computerbeheer**. Klik in het linkerdeelvenster Hallo **opslag > Schijfbeheer**. Hallo of meer volumes op Hallo virtuele StorSimple-matrix gemaakt die zichtbaar toothis host zal worden weergegeven onder **Schijfbeheer** als nieuwe schijf of schijven.
15. Initialiseer de schijf Hallo en maak een nieuw volume. Tijdens het Hallo-indeling, selecteer een clustergrootte (AUS) van 64 KB. Hallo proces herhalen voor alle Hallo beschikbare volumes.
    
    ![Schijfbeheer](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio20.png)
16. Onder **Schijfbeheer**, klik met de rechtermuisknop Hallo **schijf** en selecteer **eigenschappen**.
17. In Hallo **multipath schijf apparaateigenschappen** dialoogvenster vak, klikt u op Hallo **MPIO** tabblad.
    
    ![Schijfeigenschappen](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio21.png)
18. In Hallo **DSM-naam** sectie, klikt u op **Details** en controleer of Hallo parameters toohello standaardparameters zijn ingesteld. Hallo standaardparameters zijn:
    
    * Pad controleren periode = 30
    * Aantal nieuwe pogingen = 3
    * PDO periode verwijdert = 20
    * Interval voor nieuwe pogingen = 1
    * Pad controleren ingeschakeld = niet ingeschakeld.
    
    > [!NOTE]
    > **Hallo standaardparameters mag niet worden gewijzigd.**
   
## <a name="next-steps"></a>Volgende stappen
Meer informatie over [StorSimple Apparaatbeheer service tooadminister uw virtuele StorSimple-matrix met behulp van Hallo](storsimple-virtual-array-manager-service-administration.md).

