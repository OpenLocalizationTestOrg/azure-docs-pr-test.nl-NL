---
title: aaaConfigure MPIO voor uw StorSimple-apparaat | Microsoft Docs
description: Hierin wordt beschreven hoe tooconfigure Multipath I/O (MPIO) voor uw StorSimple-apparaat met elkaar verbonden tooa host waarop Windows Server 2012 R2 wordt uitgevoerd.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 879fd0f9-c763-4fa0-a5ba-f589a825b2df
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/03/2017
ms.author: alkohli
ms.openlocfilehash: 08cd53039b3868217c7d28e97d7c3c695c06e399
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multipath-io-for-your-storsimple-device"></a>MPIO configureren voor uw StorSimple-apparaat
Microsoft ondersteuning voor Hallo Multipath I/O (MPIO)-functie in Windows Server toohelp gebouwd bouwen SAN-configuraties, maximaal beschikbare en fouttolerantie. MPIO maakt gebruik van componenten van fysieke paden redundante-adapters, kabels en switches: toocreate logische paden tussen Hallo-server en het Hallo-opslagapparaat. Als er een onderdeelfout, overgestapt waardoor een toofail logische pad gebruik van meerdere paden op een alternatief pad voor i/o zodat toepassingen steeds toegang hun gegevens tot nog. Bovendien afhankelijk van uw configuratie kan MPIO ook prestaties verbeteren door opnieuw Hallo werklast te verdelen over alle deze paden. Zie voor meer informatie [MPIO overzicht](https://technet.microsoft.com/library/cc725907.aspx "MPIO overzicht en kenmerken").  

Voor Hallo hoge beschikbaarheid van uw StorSimple-oplossing, moet de MPIO op uw StorSimple-apparaat worden geconfigureerd. Wanneer de MPIO op de hostservers met Windows Server 2012 R2 is geïnstalleerd, tolereert Hallo servers vervolgens een koppeling-, netwerk- of Interfacefout. 

MPIO is een optionele functie in Windows Server en wordt niet standaard geïnstalleerd. Het moet als een functie via Serverbeheer worden geïnstalleerd. Dit onderwerp beschrijft Hallo stappen u moet volgen tooinstall en Hallo MPIO-functie op een host waarop Windows Server 2012 R2 en verbonden tooa fysieke StorSimple-apparaat gebruiken.

> [!NOTE]
> **Deze procedure is van toepassing op StorSimple 8000-serie alleen. MPIO wordt momenteel niet ondersteund op een virtueel StorSimple-apparaat.**
> 
> 

U moet toofollow deze stappen tooconfigure MPIO op uw StorSimple-apparaat:

* Stap 1: Installeer de MPIO op Hallo Windows Server-host
* Stap 2: MPIO configureren voor StorSimple-volumes
* Stap 3: Koppelpunt StorSimple-volumes op Hallo host
* Stap 4: MPIO configureren voor hoge beschikbaarheid en taakverdeling

Elk Hallo bovenstaande stappen wordt besproken in Hallo uit te voeren.

## <a name="step-1-install-mpio-on-hello-windows-server-host"></a>Stap 1: Installeer de MPIO op Hallo Windows Server-host
tooinstall voltooien van deze functie op de host Windows Server Hallo procedure uitvoert.

#### <a name="tooinstall-mpio-on-hello-host"></a>tooinstall MPIO op Hallo host
1. Open Serverbeheer op uw Windows Server-host. Serverbeheer wordt standaard, wanneer een lid van de groep Administrators Hallo aanmeldt tooa-computer waarop Windows Server 2012 R2 of Windows Server 2012 wordt gestart. Als Serverbeheer Hallo nog niet is geopend, klikt u op **Start > Serverbeheer**.
   ![Serverbeheer](./media/storsimple-configure-mpio-windows-server/IC740997.png)
2. Klik op **Serverbeheer > Dashboard > functies en onderdelen toevoegen**. Hiermee start u Hallo **functies en onderdelen toevoegen** wizard.
   ![Wizard functies en onderdelen 1 toevoegen](./media/storsimple-configure-mpio-windows-server/IC740998.png)
3. In Hallo **functies en onderdelen toevoegen** wizard Hallo te volgen:
   
   * Op Hallo **voordat u begint met** pagina, klikt u op **volgende**.
   * Op Hallo **installatietype selecteren** pagina, accepteer de standaardinstelling Hallo van **op basis van functie of onderdeel gebaseerde** installatie. Klik op **volgende**.![ Wizard functies en onderdelen 2 toevoegen](./media/storsimple-configure-mpio-windows-server/IC740999.png)
   * Op Hallo **Select doelserver** pagina **Selecteer een server uit de servergroep Hallo**. De hostserver moet automatisch worden gedetecteerd. Klik op **Volgende**.
   * Op Hallo **Serverfuncties selecteren** pagina, klikt u op **volgende**.
   * Op Hallo **functies selecteren** pagina **Multipath i/o**, en klik op **volgende**.![ Wizard functies en onderdelen 5 toevoegen](./media/storsimple-configure-mpio-windows-server/IC741000.png)
   * Op Hallo **installatieselecties bevestigen** pagina, bevestig de selectie van Hallo en selecteer vervolgens **Hallo doelserver opnieuw opstarten automatisch indien nodig**, zoals hieronder weergegeven. Klik op **installeren**.![ Wizard functies en onderdelen 8 toevoegen](./media/storsimple-configure-mpio-windows-server/IC741001.png)
   * U wordt gewaarschuwd wanneer Hallo-installatie voltooid is. Klik op **sluiten** tooclose Hallo-wizard.![ Wizard functies en onderdelen 9 toevoegen](./media/storsimple-configure-mpio-windows-server/IC741002.png)

## <a name="step-2-configure-mpio-for-storsimple-volumes"></a>Stap 2: MPIO configureren voor StorSimple-volumes
MPIO moet toobe geconfigureerd tooidentify StorSimple-volumes. tooconfigure MPIO toorecognize StorSimple-volumes, uitvoeren Hallo stappen te volgen.

#### <a name="tooconfigure-mpio-for-storsimple-volumes"></a>tooconfigure MPIO voor StorSimple-volumes
1. Open Hallo **MPIO-configuratie**. Klik op **Serverbeheer > Dashboard > Extra > MPIO**.
2. In Hallo **eigenschappen voor MPIO** dialoogvenster, selecteer Hallo **detecteren met meerdere paden** tabblad.
3. Selecteer **ondersteuning voor iSCSI-apparaten toevoegen**, en klik vervolgens op **toevoegen**.  
   ![Eigenschappen voor MPIO detecteren meerdere paden](./media/storsimple-configure-mpio-windows-server/IC741003.png)
4. Hallo server desgevraagd opnieuw opstarten.
5. In Hallo **eigenschappen voor MPIO** dialoogvenster vak, klikt u op Hallo **MPIO apparaten** tabblad. Klik op **Toevoegen**.
    </br>![MPIO eigenschappen MPIO-apparaten](./media/storsimple-configure-mpio-windows-server/IC741004.png)
6. In Hallo **MPIO-ondersteuning toevoegen** dialoogvenster onder **Hardware-ID apparaat**, voer het serienummer van uw apparaat. U kunt het serienummer apparaat Hallo ophalen door toegang tot uw StorSimple Manager-service en te navigeren**apparaten > Dashboard**. serienummer Hallo-apparaat wordt weergegeven in de juiste Hallo **snel in één oogopslag** deelvenster van Hallo apparaat dashboard.
    </br>![Ondersteuning voor MPIO toevoegen](./media/storsimple-configure-mpio-windows-server/IC741005.png)
7. Hallo server desgevraagd opnieuw opstarten.

## <a name="step-3-mount-storsimple-volumes-on-hello-host"></a>Stap 3: Koppelpunt StorSimple-volumes op Hallo host
Nadat MPIO op Windows Server is geconfigureerd, wordt volumes die zijn gemaakt op Hallo StorSimple-apparaat kan worden gekoppeld en kunnen vervolgens profiteren van MPIO voor redundantie. toomount een volume uitvoeren Hallo stappen te volgen.

#### <a name="toomount-volumes-on-hello-host"></a>toomount volumes op Hallo host
1. Open Hallo **eigenschappen iSCSI-Initiator** -venster op Hallo Windows Server-host. Klik op **Serverbeheer > Dashboard > Extra > iSCSI-Initiator**.
2. In Hallo **eigenschappen iSCSI-Initiator** in het dialoogvenster, klikt u op Hallo detectie tabblad en klik vervolgens op **doelportaal detecteren**.
3. In Hallo **doelportaal detecteren** dialoogvenster vak, Hallo te volgen:
   
   * Geef IP-adres Hallo Hallo poort van de gegevens van uw StorSimple-apparaat (bijvoorbeeld enter DATA 0).
   * Klik op **OK** tooreturn toohello **eigenschappen iSCSI-Initiator** in het dialoogvenster.
     
     > [!IMPORTANT]
     > **Als u van een particulier netwerk voor iSCSI-verbindingen gebruikmaakt, voert u Hallo IP-adres van Hallo gegevenspoort die is verbonden toohello privé-netwerk.**
     > 
     > 
4. Herhaal stappen 2-3 voor een tweede netwerkinterface (bijvoorbeeld, gegevens-1) op uw apparaat. Houd er rekening mee dat deze interfaces moeten worden ingeschakeld voor iSCSI. meer informatie over deze, Zie toolearn [netwerkinterfaces wijzigen](storsimple-modify-device-config.md#modify-network-interfaces).
5. Selecteer Hallo **doelen** tabblad in Hallo **eigenschappen iSCSI-Initiator** in het dialoogvenster. U ziet de StorSimple-apparaat Hallo doel IQN onder **gedetecteerde doelen**.

   ![iSCSI-Initiator eigenschappen doelen tabblad](./media/storsimple-configure-mpio-windows-server/IC741007.png)
   
6. Klik op **Connect** tooestablish een iSCSI-sessie met uw StorSimple-apparaat. Een **tooTarget verbinding** dialoogvenster wordt weergegeven.
7. In Hallo **verbinding tooTarget** dialoogvenster, selecteer Hallo **Multipath inschakelen** selectievakje. Klik op **geavanceerde**.
8. In Hallo **geavanceerde instellingen** dialoogvenster vak, Hallo te volgen:                                        
   
   * Op Hallo **lokale Adapter** vervolgkeuzelijst, selecteer **Microsoft iSCSI-Initiator**.
   * Op Hallo **Initiator IP** vervolgkeuzelijst, selecteer Hallo IP-adres van Hallo host.
   * Op Hallo **doelportal** IP-vervolgkeuzelijst, selecteer Hallo IP-adres van apparaatinterface.
   * Klik op **OK** tooreturn toohello **eigenschappen iSCSI-Initiator** in het dialoogvenster.
9. Klik op **Eigenschappen**. In Hallo **eigenschappen** in het dialoogvenster, klikt u op **sessie toevoegen**.
10. In Hallo **verbinding tooTarget** dialoogvenster, selecteer Hallo **Multipath inschakelen** selectievakje. Klik op **geavanceerde**.
11. In Hallo **geavanceerde instellingen** in het dialoogvenster:                                        
    
    * Op Hallo **lokale adapter** vervolgkeuzelijst, selecteer Microsoft iSCSI-Initiator.
    * Op Hallo **Initiator IP** vervolgkeuzelijst, selecteer Hallo IP-adres bijbehorende toohello host. In dit geval u verbinding maakt twee netwerkinterfaces op Hallo apparaat tooa één netwerkinterface op Hallo host. Deze interface is daarom Hallo hetzelfde als die opgegeven voor Hallo eerste sessie.
    * Op Hallo **IP-adres van doel Portal** vervolgkeuzelijst, selecteer Hallo IP-adres voor Hallo tweede gegevens interface is ingeschakeld op Hallo-apparaat.
    * Klik op **OK** tooreturn toohello iSCSI-Initiator eigenschappenvenster. U kunt een tweede sessie toohello doel hebt toegevoegd.
12. Open **Computerbeheer** door te navigeren**Serverbeheer > Dashboard > Computerbeheer**. Klik in het linkerdeelvenster Hallo **opslag > Schijfbeheer**. Hallo wordt gemaakt op het StorSimple-apparaat Hallo volumes die zijn zichtbaar toothis host weergegeven onder **Schijfbeheer** als nieuwe schijf of schijven.
13. Initialiseer de schijf Hallo en maak een nieuw volume. Tijdens het Hallo-indeling, selecteer een blokgrootte van 64 KB.
    ![Schijfbeheer](./media/storsimple-configure-mpio-windows-server/IC741008.png)
14. Onder **Schijfbeheer**, klik met de rechtermuisknop Hallo **schijf** en selecteer **eigenschappen**.
15. In Hallo StorSimple Model ### **multipath schijf apparaateigenschappen** dialoogvenster vak, klikt u op Hallo **MPIO** tabblad. ![StorSimple 8100 multipath-schijf DeviceProp.](./media/storsimple-configure-mpio-windows-server/IC741009.png)
16. In Hallo **DSM-naam** sectie, klikt u op **Details** en controleer of Hallo parameters toohello standaardparameters zijn ingesteld. Hallo standaardparameters zijn:
    
    * Pad controleren periode = 30
    * Aantal nieuwe pogingen = 3
    * PDO periode verwijdert = 20
    * Interval voor nieuwe pogingen = 1
    * Pad controleren ingeschakeld = niet ingeschakeld.

> [!NOTE]
> **Hallo standaardparameters mag niet worden gewijzigd.**


## <a name="step-4-configure-mpio-for-high-availability-and-load-balancing"></a>Stap 4: MPIO configureren voor hoge beschikbaarheid en taakverdeling
Voor Multipath op basis van hoge beschikbaarheid en taakverdeling, meerdere sessies moeten handmatig worden toegevoegd toodeclare Hallo verschillende paden die beschikbaar zijn. Bijvoorbeeld, als Hallo host twee interfaces zijn verbonden heeft tooSAN en Hallo apparaat heeft twee interfaces verbonden tooSAN, moet u vier sessies met het juiste pad permutaties (slechts twee sessies zijn vereist als elke interface van de gegevens en de hostinterface is geconfigureerd in een ander IP-subnet en kan niet worden omgeleid).

**We raden u aan ten minste 8 parallelle actieve sessies tussen Hallo-apparaat en de toepassingshost van uw.** Dit kan worden bereikt door het inschakelen van 4-netwerkinterfaces op uw Windows Server-systeem. Fysieke netwerkinterfaces of virtuele interfaces via technologieën voor het virtualisatie van netwerk op Hallo hardware of besturingssysteem niveau op de host Windows Server gebruiken. Met de Hallo twee netwerkinterfaces op Hallo-apparaat, worden deze configuratie zou leiden tot 8 actieve sessies. Deze configuratie helpt om het apparaat en cloud doorvoer Hallo optimaliseren.

> [!IMPORTANT]
> **Het is raadzaam dat u niet door elkaar 1 GbE- en 10 GbE-netwerkinterfaces. Als u twee netwerkinterfaces gebruikt, moet beide interfaces Hallo identiek type.**

Hallo volgende procedure wordt beschreven hoe tooadd sessies wanneer een StorSimple-apparaat met twee netwerkinterfaces verbonden tooa is host met twee netwerkinterfaces. U kunt alleen 2 actieve sessies. Gebruik dezelfde procedure met een virtueel StorSimple-apparaat met twee interfaces verbonden tooa netwerkhost met vier netwerkinterfaces. U moet tooconfigure 8 in plaats van Hallo 4 sessies die hier wordt beschreven.

### <a name="tooconfigure-mpio-for-high-availability-and-load-balancing"></a>tooconfigure MPIO voor hoge beschikbaarheid en taakverdeling
1. Hallo-doel te doorzoeken: in Hallo **eigenschappen iSCSI-Initiator** op Hallo van het dialoogvenster **detectie** tabblad **Portal detecteren**.
2. In Hallo **tooTarget verbinding** dialoogvenster Voer Hallo IP-adres van een van de netwerkinterfaces Hallo-apparaat.
3. Klik op **OK** tooreturn toohello **eigenschappen iSCSI-Initiator** in het dialoogvenster.
4. In Hallo **eigenschappen iSCSI-Initiator** dialoogvenster, selecteer Hallo **doelen** tabblad, markeer Hallo gedetecteerd doel en klik vervolgens op **Connect**. Hallo **tooTarget verbinding** dialoogvenster wordt weergegeven.
5. In Hallo **tooTarget verbinding** in het dialoogvenster:
   
   * Laat de eigenschap Hallo standaard geselecteerde doel-instelling voor **toevoegen van deze verbinding** toohello lijst met favoriete doelen. Hierdoor werkt Hallo apparaat proberen automatisch opnieuw toorestart Hallo verbinding elke keer dat deze computer opnieuw wordt opgestart.
   * Selecteer Hallo **Multipath inschakelen** selectievakje.
   * Klik op **geavanceerde**.
6. In Hallo **geavanceerde instellingen** in het dialoogvenster:
   
   * Op Hallo **lokale Adapter** vervolgkeuzelijst, selecteer **Microsoft iSCSI-Initiator**.
   * Op Hallo **Initiator IP** vervolgkeuzelijst, selecteer Hallo IP-adres van Hallo host.
   * Op Hallo **IP-adres van doel Portal** vervolgkeuzelijst, selecteer Hallo IP-adres van Hallo gegevens interface is ingeschakeld op Hallo-apparaat.
   * Klik op **OK** tooreturn toohello iSCSI-Initiator eigenschappenvenster.
7. Klik op **eigenschappen**, en in Hallo **eigenschappen** in het dialoogvenster, klikt u op **sessie toevoegen**.
8. In Hallo **verbinding tooTarget** dialoogvenster, selecteer Hallo **Multipath inschakelen** selectievakje en klik vervolgens op **Geavanceerd**.
9. In Hallo **geavanceerde instellingen** in het dialoogvenster:
   
   1. Op Hallo **lokale adapter** vervolgkeuzelijst, selecteer **Microsoft iSCSI-Initiator**.
   2. Op Hallo **Initiator IP** vervolgkeuzelijst, selecteer Hallo IP-adres bijbehorende toohello tweede interface op Hallo host.
   3. Op Hallo **IP-adres van doel Portal** vervolgkeuzelijst, selecteer Hallo IP-adres voor Hallo tweede gegevens interface is ingeschakeld op Hallo-apparaat.
   4. Klik op **OK** tooreturn toohello **eigenschappen iSCSI-Initiator** in het dialoogvenster. U hebt nu een tweede sessie toohello doel toegevoegd.
10. Herhaal de stappen 8-10 tooadd extra sessies (paden) toohello doel. U kunt een totaal van vier sessies toevoegen met twee interfaces op Hallo host en twee gegevensbronnen op Hallo-apparaat.
11. Na het toevoegen van Hallo gewenst sessies (paden) in Hallo **eigenschappen iSCSI-Initiator** dialoogvenster, selecteer Hallo doel en klik op **eigenschappen**. Op tabblad van sessies Hallo Hallo **eigenschappen** dialoogvenster, opmerking Hallo vier sessie-id's die overeenkomen met het aantal permutaties toohello-pad. toocancel een sessie, Hallo selectievakje volgende tooa sessie-id selecteren en klik vervolgens op **Disconnect**.
12. tooview apparaten die zijn gepresenteerd in sessies, selecteer Hallo **apparaten** tabblad tooconfigure Hallo MPIO-beleid voor een geselecteerd apparaat, klikt u op **MPIO**. Hallo **Apparaatdetails** dialoogvenster wordt weergegeven. Op Hallo **MPIO** tabblad kunt u geschikte Hallo **taakverdelingsbeleid** instellingen. U kunt ook weergeven Hallo **Active** of **stand-by** padtype.

## <a name="next-steps"></a>Volgende stappen
Meer informatie over [toomodify voor StorSimple Manager-service de configuratie van uw StorSimple-apparaat met behulp van Hallo](storsimple-modify-device-config.md).

