---
title: aaaStorSimple Snapshot Manager en volumes | Microsoft Docs
description: Hierin wordt beschreven hoe toouse StorSimple Snapshot Manager MMC-module tooview Hallo en beheren van volumes en tooconfigure back-ups.
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 78896323-e57c-431e-bbe2-0cbde1cf43a2
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/18/2016
ms.author: v-sharos
ms.openlocfilehash: b8ce102d082b7c773d667a9d3ec747be9e1d3064
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooview-and-manage-volumes"></a>StorSimple Snapshot Manager tooview gebruiken en beheren van volumes
## <a name="overview"></a>Overzicht
Hallo StorSimple Snapshot Manager kunt u **Volumes** knooppunt (op Hallo **bereik** deelvenster) tooselect volumes en informatie over deze weergeeft. Hallo-volumes worden weergegeven als stations die overeenkomen met toohello volumes die zijn gekoppeld met de Hallo host. Hallo **Volumes** knooppunt wordt de lokale volumes en typen van de volumes die worden ondersteund door StorSimple, met inbegrip van volumes die zijn gedetecteerd via Hallo gebruik van iSCSI- en een apparaat. 

Voor meer informatie over ondersteunde volumes gaat te[ondersteuning voor meerdere volumetypen](storsimple-what-is-snapshot-manager.md#support-for-multiple-volume-types).

![Volumelijst in het deelvenster met resultaten](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Volume_node.png)

Hallo **Volumes** knooppunt ook kunt u het opnieuw scannen of volumes verwijderen nadat ze in StorSimple Snapshot Manager worden gedetecteerd. 

Deze zelfstudie wordt uitgelegd hoe u kunt koppelen, initialiseren, en volumes formatteren en vervolgens StorSimple Snapshot Manager te gebruiken:

* Informatie over volumes weergeven 
* Volumes verwijderen
* Volumes opnieuw scannen 
* Configureer een standaardvolume en back-up maken
* Configureren van een gespiegeld volume en back-up maken

> [!NOTE]
> Alle Hallo **Volume** knooppunt acties zijn ook beschikbaar in Hallo **acties** deelvenster.
> 
> 

## <a name="mount-volumes"></a>Koppelen van volumes
Gebruik Hallo na de procedure toomount, initialiseren en formatteren van StorSimple-volumes. Deze procedure maakt gebruik van een systeemhulpprogramma voor het beheren van harde schijven en de overeenkomstige volumes Hallo of partities Schijfbeheer. Voor meer informatie over Schijfbeheer, gaat u te[Schijfbeheer](https://technet.microsoft.com/library/cc770943.aspx) op Hallo Microsoft TechNet-website.

#### <a name="toomount-volumes"></a>toomount volumes
1. Start Hallo Microsoft iSCSI-initiator op de hostcomputer.
2. Geef een van de Hallo interface IP-adressen als Hallo doelportal of detectie van IP-adres en toohello apparaat aansluit. Nadat het Hallo-apparaat is verbonden, worden Hallo volumes toegankelijk tooyour Windows-systeem. Ga voor meer informatie over het gebruik van Hallo Microsoft iSCSI-initiator toohello sectie 'Verbinding maakt met tooan iSCSI-doelapparaat' [installeren en configureren van Microsoft iSCSI-Initiator][1].
3. Een van de opties toostart Schijfbeheer na hello gebruiken:
   
   * Typ Diskmgmt.msc in Hallo **uitvoeren** vak.
   * Start Serverbeheer uit, vouw Hallo **opslag** knooppunt en selecteer vervolgens **Schijfbeheer**.
   * Start **Systeembeheer**, vouw Hallo **Computerbeheer** knooppunt en selecteer vervolgens **Schijfbeheer**. 
     
     > [!NOTE]
     > U moet administrator-bevoegdheden toorun Schijfbeheer.
     > 
     > 
4. Hallo volumes online nemen:
   
   1. In Schijfbeheer met de rechtermuisknop op een volume dat is gemarkeerd als **Offline**.
   2. Klik op **schijf opnieuw activeren**. Hallo-schijf moet worden gemarkeerd **Online** nadat Hallo schijf opnieuw wordt geactiveerd.
5. Hallo volumes initialiseren:
   
   1. Klik met de rechtermuisknop Hallo gedetecteerd volumes.
   2. Selecteer Hallo menu **schijf initialiseren**.
   3. In Hallo **schijf initialiseren** in het dialoogvenster, selecteer Hallo schijven tooinitialize wilt en klik vervolgens op **OK**.
6. Eenvoudige volumes formatteren:
   
   1. Met de rechtermuisknop op een volume dat u wilt dat tooformat.
   2. Selecteer Hallo menu **Nieuw eenvoudig Volume**.
   3. Hallo Nieuw eenvoudig Volume wizard tooformat Hallo volume gebruiken:
      
      * Hallo volumegrootte opgeven.
      * Geef een stationsletter.
      * Selecteer Hallo NTFS-bestandssysteem.
      * Geef een clustergrootte van 64 kB op.
      * Voer een snelle formattering uit.
7. Meerdere partitie volumes formatteren. Voor instructies gaat u toohello sectie 'Partities en Volumes' [Schijfbeheer implementeren](https://msdn.microsoft.com/library/dd163556.aspx).

## <a name="view-information-about-your-volumes"></a>Informatie over uw volumes weergeven
Gebruik hello te volgen procedure tooview informatie over lokale en Azure StorSimple-volumes.

#### <a name="tooview-volume-information"></a>de volumegegevens tooview
1. Klik op Hallo bureaubladpictogram toostart StorSimple Snapshot Manager. 
2. In Hallo **bereik** deelvenster, klikt u op Hallo **Volumes** knooppunt. Een lijst van lokale en gekoppelde volumes, met inbegrip van alle Azure StorSimple-volumes wordt weergegeven in Hallo **resultaten** deelvenster. kolommen in Hallo Hallo **resultaten** deelvenster worden geconfigureerd. (Klik met de rechtermuisknop Hallo **Volumes** knooppunt **weergave**, en selecteer vervolgens **kolommen toevoegen/verwijderen**.)
   
    ![Hallo kolommen configureren](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_View_volumes.png)
   
   | Kolom | Beschrijving |
   |:--- |:--- |
   |  Naam |Hallo **naam** kolom Hallo station stationsletter toegewezen tooeach gedetecteerd volume bevat. |
   |  Apparaat |Hallo **apparaat** kolom Hallo IP-adres van de hostcomputer van Hallo apparaat verbonden toohello bevat. |
   |  Volumenaam van apparaat |Hallo **Volume apparaatnaam** kolom bevat de naam Hallo Hallo apparaat volume toowhich Hallo geselecteerd volume behoort. Dit is Hallo volumenaam gedefinieerd in hello Azure-portal voor die specifieke volume. |
   |  Toegangspaden |Hallo **Toegangspaden** kolom Hallo toegang pad toohello volume worden weergegeven. Dit is Hallo station stationsletter of koppelpunt op welke Hallo volume toegankelijk op Hallo-hostcomputer is. |

## <a name="delete-a-volume"></a>Een volume verwijderen
Hallo te volgen procedure toodelete een volume van StorSimple Snapshot Manager gebruiken.

> [!NOTE]
> U kunt een volume niet verwijderen als deze deel van een volume-groep uitmaakt. (de optie verwijderen Hallo is niet beschikbaar voor volumes die lid van een volume-groep zijn.) Hallo hele volume groep toodelete Hallo volume, moet u verwijderen.

#### <a name="toodelete-a-volume"></a>een volume toodelete
1. Klik op Hallo bureaubladpictogram toostart StorSimple Snapshot Manager.
2. In Hallo **bereik** deelvenster, klikt u op Hallo **Volumes** knooppunt. 
3. In Hallo **resultaten** deelvenster, klik met de rechtermuisknop Hallo volume dat u wilt dat toodelete.
4. Klik op het menu Hallo **verwijderen**. 
   
    ![Een volume verwijderen](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Delete_volume.png) 
5. Hallo **Volume verwijderen** dialoogvenster wordt weergegeven. Type **bevestigen** in Hallo in het tekstvak en klik vervolgens op **OK**.
6. Standaard StorSimple Snapshot Manager back-ups van een volume voordat u het verwijdert. Deze voorzorgsmaatregel kunt beschermen tegen gegevensverlies als Hallo verwijdering onbedoeld is verwijderd. StorSimple Snapshot Manager geeft een **Automatische momentopname** voortgangsbericht terwijl er een back-up Hallo volume. 
   
    ![Automatische momentopname bericht](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Automatic_snap.png) 

## <a name="rescan-volumes"></a>Volumes opnieuw scannen
Hallo te volgen procedure toorescan Hallo volumes verbonden tooStorSimple Snapshot Manager gebruiken.

#### <a name="toorescan-hello-volumes"></a>toorescan hello volumes
1. Klik op Hallo bureaubladpictogram toostart StorSimple Snapshot Manager.
2. In Hallo **bereik** deelvenster met de rechtermuisknop op **Volumes**, en klik vervolgens op **volumes opnieuw scannen**.
   
    ![Volumes opnieuw scannen](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Rescan_volumes.png)
   
    Deze procedure synchroniseert Hallo volumelijst met StorSimple Snapshot Manager. Wijzigingen, zoals nieuwe volumes of verwijderde volumes worden, weergegeven in het Hallo-resultaten.

## <a name="configure-and-back-up-a-basic-volume"></a>Configureren en back-up van een standaardvolume
Hallo te volgen procedure tooconfigure een back-up van een standaardvolume gebruiken en vervolgens een back-up onmiddellijk te starten of een beleid voor geplande back-ups maken.

### <a name="prerequisites"></a>Vereisten
Voordat u begint:

* Zorg ervoor dat Hallo StorSimple-apparaat en hostcomputer correct zijn geconfigureerd. Voor meer informatie gaat te[uw on-premises StorSimple-apparaat implementeren](storsimple-deployment-walkthrough-u2.md).
* Installeer en configureer StorSimple Snapshot Manager. Voor meer informatie gaat te[implementeren StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md).

#### <a name="tooconfigure-backup-of-a-basic-volume"></a>tooconfigure back-up van een standaardvolume
1. Maak een standaardvolume op Hallo StorSimple-apparaat.
2. Koppelen, initialiseren en formatteren Hallo volume zoals beschreven in [volumes koppelen](#mount-volumes). 
3. Klik op Hallo StorSimple Snapshot Manager-pictogram op het bureaublad. Hallo StorSimple Snapshot Manager-venster wordt weergegeven. 
4. In Hallo **bereik** deelvenster, klik met de rechtermuisknop Hallo **Volumes** knooppunt en selecteer vervolgens **volumes opnieuw scannen**. Wanneer Hallo scan is voltooid, een lijst van volumes moet worden weergegeven in Hallo **resultaten** deelvenster. 
5. In Hallo **resultaten** deelvenster met de rechtermuisknop op het Hallo-volume en selecteer vervolgens **Create Volume Group**. 
   
    ![Volume-groep maken](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Create_volume_group.png) 
6. In Hallo **Create Volume Group** in het dialoogvenster Typ een naam voor Hallo volume groep volumes tooit toewijzen en klik vervolgens op **OK**.
7. In Hallo **bereik** deelvenster Vouw Hallo **Volume groepen** knooppunt. Hallo nieuwe volume groep moet worden weergegeven onder Hallo **Volume groepen** knooppunt. 
8. Met de rechtermuisknop op de naam van de groep volume Hallo.
   
   * toostart een interactieve (op aanvraag) back-uptaak, klikt u op **back-ups nemen**. 
   * tooschedule een automatische back-up, klikt u op **back-upbeleid maken**. Op Hallo **algemene** pagina, selecteert u een volume-groep in Hallo-lijst. Op Hallo **planning** pagina, voert u de details van de planning Hallo. Wanneer u klaar bent, klikt u op **OK**. 
9. tooconfirm die Hallo back-uptaak is gestart, vouw Hallo **taken** knooppunt in Hallo **bereik** deelvenster en klik vervolgens op Hallo **met** knooppunt. Hallo-lijst van de momenteel actieve taken wordt weergegeven in Hallo **resultaten** deelvenster. 

## <a name="configure-and-back-up-a-dynamic-mirrored-volume"></a>Configureren en back-up van een gespiegeld volume
Volgende stappen tooconfigure back-up van een gespiegeld volume Hallo voltooien:

* Stap 1: Gebruik Schijfbeheer toocreate een gespiegeld volume. 
* Stap 2: Gebruik StorSimple Snapshot Manager tooconfigure back-up.

### <a name="prerequisites"></a>Vereisten
Voordat u begint:

* Zorg ervoor dat Hallo StorSimple-apparaat en hostcomputer correct zijn geconfigureerd. Voor meer informatie gaat te[uw on-premises StorSimple-apparaat implementeren](storsimple-8000-deployment-walkthrough-u2.md).
* Installeer en configureer StorSimple Snapshot Manager. Voor meer informatie gaat te[implementeren StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md).
* Configureer twee volumes op Hallo StorSimple-apparaat. (In Hallo voorbeelden, de beschikbare volumes Hallo zijn **schijf 1** en **schijf 2**.) 

### <a name="step-1-use-disk-management-toocreate-a-dynamic-mirrored-volume"></a>Stap 1: Gebruik Schijfbeheer toocreate een gespiegeld volume
Schijfbeheer is een hulpprogramma voor het beheren van harde schijven en volumes Hallo of partities die ze bevatten. Voor meer informatie over Schijfbeheer, gaat u te[Schijfbeheer](https://technet.microsoft.com/library/cc770943.aspx) op Hallo Microsoft TechNet-website.

#### <a name="toocreate-a-dynamic-mirrored-volume"></a>toocreate een gespiegeld volume
1. Een van de opties toostart Schijfbeheer na hello gebruiken: 
   
   * Open Hallo **uitvoeren** in het vak **Diskmgmt.msc**, en druk op Enter.
   * Start Serverbeheer uit, vouw Hallo **opslag** knooppunt en selecteer vervolgens **Schijfbeheer**. 
   * Start **Systeembeheer**, vouw Hallo **Computerbeheer** knooppunt en selecteer vervolgens **Schijfbeheer**. 
2. Zorg ervoor dat er twee volumes beschikbaar op Hallo StorSimple-apparaat. (In Hallo bijvoorbeeld Hallo beschikbare volumes zijn **schijf 1** en **schijf 2**.) 
3. Hallo venster Schijfbeheer in de rechterkolom Hallo van Hallo onderste deelvenster met de rechtermuisknop op **schijf 1** en selecteer **nieuw gespiegeld Volume**. 
   
    ![Nieuw Mirrored Volume](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_New_mirrored_volume.png) 
4. Op Hallo **nieuw gespiegeld Volume** pagina van de wizard, klikt u op **volgende**.
5. Op Hallo **schijven selecteren** pagina **schijf 2** in Hallo **geselecteerde** deelvenster, klikt u op **toevoegen**, en klik vervolgens op **volgende**. 
6. Op Hallo **stationsaanduiding toewijzen of pad** pagina, accepteer Hallo standaardwaarden en klik op **volgende**. 
7. Op Hallo **Opmaakvolume** pagina in Hallo **clustergrootte** de optie **64K**. Selecteer Hallo **Snelformatteren** selectievakje en klik vervolgens op **volgende**. 
8. Op Hallo **voltooien Hallo nieuw gespiegeld Volume** pagina, Controleer uw instellingen en klik vervolgens op **voltooien**. 
9. Er verschijnt een bericht tooindicate die Hallo standaardschijf worden geconverteerde tooa dynamische schijf. Klik op **Ja**.
   
    ![Dynamische schijf converteren bericht](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Disk_management_msg.png) 
10. Controleer of schijf 1 en 2 van de schijf worden als dynamische gespiegelde volumes weergegeven in Schijfbeheer. (**Dynamische** moet worden weergegeven in de kolom status Hallo en de kleur van de balk capaciteit Hallo toored, die wijzen op een gespiegeld volume moet worden gewijzigd.) 
    
    ![Schijf Management gespiegeld dynamische schijven](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Verify_dynamic_disks_2.png) 

### <a name="step-2-use-storsimple-snapshot-manager-tooconfigure-backup"></a>Stap 2: Gebruik StorSimple Snapshot Manager tooconfigure back-up
Hallo te volgen procedure tooconfigure dynamische mirrored volumes, gebruiken en een back-up onmiddellijk te starten of een beleid voor geplande back-ups maken.

#### <a name="tooconfigure-backup-of-a-dynamic-mirrored-volume"></a>tooconfigure back-up van een gespiegeld volume
1. Klik op Hallo StorSimple Snapshot Manager-pictogram op het bureaublad. Hallo StorSimple Snapshot Manager-venster wordt weergegeven. 
2. In Hallo **bereik** deelvenster, klik met de rechtermuisknop Hallo **Volumes** uit en selecteer **volumes opnieuw scannen**. Wanneer Hallo scan is voltooid, een lijst van volumes moet worden weergegeven in Hallo **resultaten** deelvenster. Hallo gespiegeld volume wordt vermeld als een enkel volume. 
3. In Hallo **resultaten** deelvenster met de rechtermuisknop op Hallo gespiegeld volume en klik vervolgens op **Create Volume Group**. 
4. In Hallo **Create Volume Group** in het dialoogvenster Typ een naam voor Hallo volume groep Hallo gespiegeld volume toothis groep worden toegewezen en klik vervolgens op **OK**. 
5. In Hallo **bereik** deelvenster Vouw Hallo **Volume groepen** knooppunt. Hallo nieuwe volume groep moet worden weergegeven onder Hallo **Volume groepen** knooppunt. 
6. Met de rechtermuisknop op de naam van de groep volume Hallo. 
   
   * toostart een interactieve (op aanvraag) back-uptaak, klikt u op **back-ups nemen**. 
   * tooschedule een automatische back-up, klikt u op **back-upbeleid maken**. Op Hallo **algemene** pagina, selecteer Hallo volume groep uit de lijst Hallo. Op Hallo **planning** pagina, voert u de details van de planning Hallo. Wanneer u klaar bent, klikt u op **OK**. 
7. Als dit wordt uitgevoerd, kunt u back-uptaak Hallo bewaken. In Hallo **bereik** deelvenster Vouw Hallo **taken** knooppunt en klik vervolgens op **met**, Hallo taakdetails worden weergegeven in Hallo **resultaten** deelvenster. Wanneer Hallo back-uptaak is voltooid, Hallo details overgebrachte toohello zijn **afgelopen 24** uren taak lijst. 

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe te[StorSimple Snapshot Manager tooadminister uw StorSimple-oplossing gebruiken](storsimple-snapshot-manager-admin.md).
* Meer informatie over hoe te[StorSimple Snapshot Manager toocreate gebruiken en beheren van groepen volume](storsimple-snapshot-manager-manage-volume-groups.md).

<!--Reference links-->
[1]: https://msdn.microsoft.com/library/ee338480(v=ws.10).aspx
