---
title: gebruikersinterface voor Snapshot Manager aaaStorSimple | Microsoft Docs
description: Beschrijving van de gebruikersinterface van Hallo StorSimple Snapshot Manager en wordt uitgelegd hoe toouse deze back-uptaken toomanage en Hallo van back-catalogus.
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: c7d91892-2881-41a2-a7a2-908dc3646493
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.custom: 
ms.openlocfilehash: 865520fdaf1b559714b52b428ad136b084d65c99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-user-interface-toomanage-backup-jobs-and-backup-catalog"></a>Gebruik StorSimple Snapshot Manager gebruikersinterface toomanage back-ups en back-upcatalogus

## <a name="overview"></a>Overzicht
Hallo StorSimple Snapshot Manager heeft een intuïtieve gebruikersinterface tootake gebruiken en beheren van back-ups. Deze zelfstudie biedt een inleiding toohello-gebruikersinterface en vervolgens wordt uitgelegd hoe toouse Hallo-onderdelen. Zie voor een gedetailleerde beschrijving van Hallo StorSimple Snapshot Manager [wat is er StorSimple Snapshot Manager?](storsimple-what-is-snapshot-manager.md)

### <a name="console-description"></a>Beschrijving van de console
tooview hello gebruiker interface, klikt u op Hallo StorSimple Snapshot Manager-pictogram op het bureaublad. Hallo-consolevenster weergegeven, zoals wordt weergegeven in de volgende illustratie Hallo.

![Deelvensters van de StorSimple Snapshot Manager](./media/storsimple-use-snapshot-manager/HCS_SSM_gui_panes.png)

Hallo-consolevenster heeft vijf belangrijke elementen. Klik op de juiste koppeling Hallo voor een volledige beschrijving van elk element.

* [Menubalk](#menu-bar) 
* [Werkbalk](#tool-bar) 
* [Deelvenster bereik](#scope-pane) 
* [Deelvenster met resultaten](#results-pane) 
* [Actiedeelvenster](#actions-pane) 

Bovendien Hallo StorSimple Snapshot Manager ondersteunt [toetsenbord navigatie en een aantal snelkoppelingen](#keyboard-navigation-and-shortcuts).

### <a name="console-accessibility"></a>Toegankelijkheid van de console
Hallo StorSimple Snapshot Manager-gebruikersinterface ondersteunt Hallo toegankelijkheidsfuncties van Windows-besturingssysteem Hallo en Hallo Microsoft Management Console (MMC), evenals enkele StorSimple Snapshot Manager-specifieke sneltoetsen. 

* Voor een beschrijving van de toegankelijkheidsfuncties van Windows hello, gaat u te[sneltoetsen voor Windows](https://support.microsoft.com/kb/126449). 
* Voor een beschrijving van de toegankelijkheidsfuncties van Hallo MMC, gaat u te[toegankelijkheid voor MMC 3.0](https://technet.microsoft.com/library/cc766075.aspx)
* Voor een beschrijving van de toegankelijkheidsfuncties van Hallo StorSimple Snapshot Manager gaat te[toetsenbord navigatie en snelkoppelingen](#keyboard-navigation-and-shortcuts).

## <a name="menu-bar"></a>Menubalk
Hallo menubalk bovenaan Hallo Hallo-consolevenster bevat [bestand](#file-menu), [actie](#action-menu), [weergave](#view-menu), [Favorieten](#favorites-menu), [venster ](#window-menu), en [Help](#help-menu) menu's.

Klik op een item op Hallo menu balk toosee een lijst met beschikbare opdrachten op dat menu. Hallo volgende voorbeeld ziet u Hallo **weergave** menu is geselecteerd op de menubalk Hallo.

![Menu Beeld geselecteerd](./media/storsimple-use-snapshot-manager/HCS_SSM_View_menu.png)

### <a name="file-menu"></a>Menu Bestand
Hallo **bestand** menu bevat de standaardopdrachten van Microsoft Management Console (MMC).

#### <a name="menu-access"></a>Toegang tot menu
Hallo tooview **bestand** menu, klikt u op **bestand** op de menubalk Hallo. Hallo volgende menu wordt weergegeven.

![Menu bestand StorSimple Snapshot Manager](./media/storsimple-use-snapshot-manager/HCS_SSM_FileMenu.png) 

#### <a name="menu-description"></a>Menu-beschrijving
Hallo volgende tabel beschrijft items die worden weergegeven op Hallo **bestand** menu.

| Menu-item | Beschrijving |
|:--- |:--- |
| Nieuw |Klik op **nieuw** toocreate een nieuwe console op basis van Hallo StorSimple Snapshot Manager. |
| Open |Klik op **Open** tooopen een bestaande console. |
| Opslaan |Klik op **opslaan** huidige toosave Hallo-console. |
| Opslaan als |Klik op **OpslaanAls** toocreate een nieuwe, nieuwe naam exemplaar van de huidige console Hallo. Gebruik Hallo **OpslaanAls** optie toocustomize een weergave en opslaan voor later gebruik. Bijvoorbeeld, kan u StorSimple Snapshot Manager-modules die punt toospecific servers maken. |
| Software-module |Klik op **module toevoegen/verwijderen** tooadd of verwijder modules en tooorganize knooppunten in Hallo **bereik** deelvenster. Voor meer informatie gaat te[toevoegen, verwijderen, en organiseren-modules en -extensies in MMC 3.0](https://technet.microsoft.com/library/cc722035.aspx). |
| Opties |Klik op **opties** toochange Hallo console pictogram gebruikersmodi toegang en machtigingen geven of verwijderen van de console bestanden tooincrease beschikbare schijfruimte. |
| Lijst met paden |Klik op een pad in Hallo genummerde lijst tooreopen een bestand dat u onlangs geopend. |
| Afsluiten |Klik op **afsluiten** tooclose hello **bestand** menu. |

### <a name="action-menu"></a>Actiemenu
Gebruik Hallo **actie** menu tooselect uit beschikbare acties. Hallo items beschikbaar tooyou afhankelijk zijn van Hallo selectie die u in Hallo **bereik** deelvenster of **resultaten** deelvenster.

#### <a name="menu-access"></a>Toegang tot menu
Hallo tooview **actie** menu, voert u een van de volgende Hallo:

* Met de rechtermuisknop op een item in Hallo **bereik** deelvenster of **resultaten** deelvenster.
* Selecteer een item in Hallo **bereik** deelvenster of **resultaten** deelvenster en klik vervolgens op **actie** op de menubalk Hallo. 

Bijvoorbeeld, als u het bovenste knooppunt Hallo in Hallo **bereik** deelvenster en klik vervolgens met de rechtermuisknop of **actie** in de menubalk Hallo Hallo volgende menu wordt weergegeven.

![Menu Actie StorSimple Snapshot Manager](./media/storsimple-use-snapshot-manager/HCS_SSM_Action_menu.png)

Hallo **acties** deelvenster (op Hallo van Hallo console) bevat Hallo dezelfde lijst met acties als Hallo **actie** menu. Bovendien Hallo **acties** deelvenster bevat Hallo **weergave** menuopties waarmee u een aangepaste weergave van Hallo toocreate **resultaten** deelvenster.

![Open het actiedeelvenster met menu Beeld](./media/storsimple-use-snapshot-manager/HCS_SSM_ActionsPane_Results.png)

#### <a name="menu-description"></a>Menu-beschrijving
Hallo volgende tabel bevat een alfabetische lijst van acties voor StorSimple Snapshot Manager. 

* Hallo **actie** kolom geeft een lijst van acties die u op de knooppunten en de resultaten uitvoeren kunt. 
* Hallo **navigatie** kolom wordt uitgelegd hoe toodisplay Hallo juiste **actie** menu zodat u Hallo actie kunt selecteren. Sommige acties worden weergegeven in meerdere **actie** menu's. Selecteer voor deze acties een **navigatie** optie uit de lijst met opsommingstekens Hallo. 
* Hallo **beschrijving** kolom wordt beschreven hoe toouse elke actie op Hallo **actie** menu of in het deelvenster Acties, en wordt uitgelegd wat het doet.

> [!NOTE]
> Hallo **acties** deelvenster en **actie** menu's bevatten extra opties, zoals **weergave**, **nieuw venster vanaf hier**,  **Vernieuwen**, **lijst exporteren**, en **Help**. Deze opties zijn beschikbaar als onderdeel van het Hallo MMC en zijn niet specifiek tooStorSimple Snapshot Manager. Hallo tabel bevat beschrijvingen van deze opties.
> 
> 

| Actie | Navigatie | Beschrijving |
|:--- |:--- |:--- |
| Verifiëren |Klik op Hallo **apparaten** -knooppunt en met de rechtermuisknop op een apparaat in Hallo **resultaten** deelvenster. |Klik op **verifiëren** tooenter Hallo wachtwoord die u hebt geconfigureerd voor Hallo-apparaat. |
| Kloon |Vouw **back-upcatalogus**, vouw **Cloudmomentopnamen**, klikt u op een datum back-up en selecteer vervolgens een volume in Hallo **resultaten** deelvenster. |Klik op **kloon** toocreate een kopie van een momentopname en sla deze op een locatie die u opgeeft. |
| Een apparaat configureren |Klik met de rechtermuisknop Hallo **apparaten** knooppunt. |Klik op **configureren van een apparaat** tooconfigure één apparaat of meerdere apparaten tooconnect toohello Windows-host. |
| Back-upbeleid maken |Voer een van de volgende Hallo:<ul><li>Met de rechtermuisknop op **back-upbeleid**.</li><li>Klik op of vouw **Volume groepen**, en klik vervolgens met de rechtermuisknop op een volume-groep.</li><li>Klik of vouw **back-upcatalogus**, en klik vervolgens met de rechtermuisknop op een volume-groep.</li></ul> |Klik op **back-upbeleid maken** tooconfigure een geplande back-up voor een groep volume. |
| Volume-groep maken |Voer een van de volgende Hallo:<ul><li>Klik op Hallo **Volumes** -knooppunt en klik vervolgens met de rechtermuisknop op een volume in Hallo **resultaten** deelvenster.</li><li>Klik met de rechtermuisknop Hallo **Volume groepen** knooppunt.</li></ul> |Klik op **Create Volume Group** tooassign volumes tooa volume groep. |
| Verwijderen |Klik op een knooppunt of het resultaat (dit item wordt weergegeven op veel **actie** menu's en **acties** deelvensters.) |Klik op **verwijderen** toodelete Hallo knooppunt of resultaat die u hebt geselecteerd. Wanneer Hallo bevestigingsdialoogvenster wordt weergegeven, verwijdering bevestigen of annuleren Hallo. |
| Details |Klik op Hallo **apparaten** -knooppunt en klik vervolgens met de rechtermuisknop op een apparaat in Hallo **resultaten** deelvenster. |Klik op **Details** toosee Hallo-configuratiegegevens voor een apparaat. |
| Bewerken |Klik op **back-upbeleid**, en klik vervolgens met de rechtermuisknop op een beleid in Hallo **resultaten** deelvenster. |Klik op **bewerken** toochange Hallo back-upschema voor een groep volume. |
| Lijst exporteren |Klik op een knooppunt of het resultaat (dit item wordt weergegeven op alle **actie** menu's en **acties** deelvensters.) |Klik op **lijst exporteren** toosave een lijst in een bestand met door komma's gescheiden waarden (CSV). U kunt dit bestand vervolgens importeren in een werkbladtoepassing voor analyse. |
| Help |Klik op een knooppunt of het resultaat. (Dit item wordt weergegeven op alle **actie** menu's en **acties** deelvensters.) |Klik op **Help** tooopen online-Help in een apart browservenster. |
| Nieuw venster |Klik op een knooppunt of het resultaat (dit item wordt weergegeven op alle **actie** menu's en **acties** deelvensters.) |Klik op **nieuw venster vanaf hier** tooopen een nieuw venster van de StorSimple Snapshot Manager. |
| Vernieuwen |Klik op een knooppunt of het resultaat (dit item wordt weergegeven op alle **actie** menu's en **acties** deelvensters.) |Klik op **vernieuwen** tooupdate Hallo momenteel weergegeven StorSimple Snapshot Manager-venster. |
| Apparaat vernieuwen |Klik op Hallo **apparaten** -knooppunt en met de rechtermuisknop op een apparaat in Hallo **resultaten** deelvenster. |Klik op **apparaat vernieuwen** toosynchronize specifieke aangesloten apparaat StorSimple Snapshot Manager. |
| Vernieuwen van apparaten |Klik met de rechtermuisknop Hallo **apparaten** knooppunt. |Klik op **apparaten vernieuwen** toosynchronize uw lijst met verbonden apparaten met StorSimple Snapshot Manager. |
| Volumes opnieuw scannen |Klik met de rechtermuisknop Hallo **Volumes** knooppunt. |Klik op **volumes opnieuw scannen** tooupdate Hallo lijst van volumes die wordt weergegeven in Hallo **resultaten** deelvenster. |
| Herstellen |Vouw **back-upcatalogus**, vouw een volume-groep uit, vouw **lokale momentopnamen** of **Cloudmomentopnamen**, en klik vervolgens met de rechtermuisknop op een back-up. |Klik op **herstellen** tooreplace Hallo huidige volumegegevens groeperen met gegevens uit de geselecteerde back-up Hallo Hallo. |
| Back-up maken |Voer een van de volgende Hallo:<ul><li>Vouw **Volume groepen**, en klik vervolgens met de rechtermuisknop op een volume-groep.</li><li>Vouw **back-upcatalogus**, en klik vervolgens met de rechtermuisknop op een volume-groep.</li></ul> |Klik op **duren back-** toostart direct een back-uptaak. |
| Wisselknop invoer weergeven |Klik met de rechtermuisknop Hallo hoofdknooppunt in Hallo **bereik** deelvenster (Hallo **StorSimple Snapshot Manager** knooppunt in het Hallo-voorbeelden). |Klik op **wisselknop invoer weergave** tooshow of verbergen Hallo volume groepen en gekoppelde back-ups die zijn geïmporteerd uit het servicedashboard StorSimple Apparaatbeheer Hallo. |

### <a name="view-menu"></a>Menu Beeld
Gebruik Hallo **weergave** menu toocreate een aangepaste weergave van Hallo **resultaten** deelvenster inhoud. Hallo **weergave** menu bevat **kolommen toevoegen/verwijderen** en **aanpassen** opties.

#### <a name="menu-access"></a>Toegang tot menu
U hebt toegang tot Hallo **weergave** menu op de menubalk Hallo of in Hallo **acties** deelvenster.

![Menu Beeld StorSimple Snapshot Manager](./media/storsimple-use-snapshot-manager/HCS_SSM_View_menu.png) 

#### <a name="menu-description"></a>Menu-beschrijving
Hallo volgende tabel beschrijft items die worden weergegeven op Hallo **weergave** menu.

| Menu-item | Beschrijving |
|:--- |:--- |
| Kolommen toevoegen/verwijderen |Klik op **kolommen toevoegen/verwijderen** tooadd of verwijder kolommen in Hallo **resultaten** deelvenster. |
| Aanpassen |Klik op **aanpassen** tooshow of verbergen items in het venster Hallo StorSimple Snapshot Manager-console. |

### <a name="favorites-menu"></a>Favorieten
Gebruik Hallo **Favorieten** menu tooadd, verwijderen en indelen van paginaweergaven en taken die u vaak gebruikt. 

#### <a name="menu-access"></a>Toegang tot menu
U hebt toegang tot Hallo **Favorieten** menu op de menubalk Hallo.

![Menu StorSimple Snapshot Manager Favorieten](./media/storsimple-use-snapshot-manager/HCS_SSM_FavoritesMenu.png)

#### <a name="menu-description"></a>Menu-beschrijving
Hallo volgende tabel beschrijft items die worden weergegeven op Hallo **Favorieten** menu.

| Menu-item | Beschrijving |
|:--- |:--- |
| TooFavorites toevoegen |Klik op **toevoegen tooFavorites** tooadd Hallo huidige weergave tooyour lijst met Favorieten. |
| Favorieten indelen |Klik op **Favorieten indelen** tooorganize Hallo inhoud van de map van uw Favorieten. |

### <a name="window-menu"></a>Venstermenu
Gebruik Hallo **venster** menu tooadd en ordenen StorSimple Snapshot Manager consolevensters.

#### <a name="menu-access"></a>Toegang tot menu
U hebt toegang tot Hallo **venster** menu op de menubalk Hallo.

![Menu StorSimple Snapshot Manager-venster](./media/storsimple-use-snapshot-manager/HCS_SSM_WindowMenu.png)

Hallo genummerde lijst onderaan Hallo Hallo menu toont windows hello die momenteel zijn geopend. Klik op een venster in dit venster lijst toobring Hallo Hallo voorgrond. 

#### <a name="menu-description"></a>Menu-beschrijving
Hallo volgende tabel beschrijft Hallo-items die worden weergegeven in menu Hallo-venster.

| Menu-item | Beschrijving |
|:--- |:--- |
| Nieuw venster |Klik op **nieuw venster** tooopen een nieuw consolevenster (in aanvulling toohello bestaande venster). |
| CASCADE |Klik op **Cascade** toodisplay Hallo open consolevensters in een CSS-stijl. |
| Schikken |Klik op **tegel horizontaal** toodisplay Hallo open consolevensters in een tegel (of het raster)-indeling. |
| Pictogrammen schikken |Als er meerdere console windows openen en verspreid over uw bureaublad te minimaliseren en klik vervolgens op **schikken Pictogrammen schikken** tooarrange ze in een horizontale rij op Hallo onder aan het scherm. |

### <a name="help-menu"></a>Menu Help
Gebruik Hallo **Help** menu tooview beschikbaar online-help voor StorSimple Snapshot Manager en Hallo MMC. U kunt ook informatie over Hallo MMC en StorSimple Snapshot Manager softwareversies die momenteel zijn geïnstalleerd op uw systeem weergeven. 

U hebt toegang tot Hallo **Help** menu op de menubalk Hallo. U kunt ook StorSimple Snapshot Manager help-onderwerpen openen vanaf Hallo **acties** deelvenster.

![StorSimple Snapshot Manager Help-menu](./media/storsimple-use-snapshot-manager/HCS_SSM_HelpMenu.png)

#### <a name="menu-description"></a>Menu-beschrijving
Hallo volgende tabel worden de items die worden weergegeven op Hallo menu Help beschreven.

| Menu-item | Beschrijving |
|:--- |:--- |
| Help bij StorSimple Snapshot Manager |Klik op **StorSimple Snapshot Manager Help** tooopen StorSimple Snapshot Manager help in een apart venster. |
| Help-onderwerpen |Klik op **Help-onderwerpen** tooopen MMC online-help in een apart venster. |
| TechCenter-website |Klik op **TechCenter-website** tooopen Hallo Microsoft TechNet Tech Center-startpagina in een apart venster. |
| Over Microsoft Management Console |Klik op **over Microsoft Management Console** toosee welke versie van Microsoft Management Console Hallo op uw systeem is geïnstalleerd. |
| StorSimple Snapshot Manager |Klik op **StorSimple Snapshot Manager** toosee welke versie van Hallo-module is geïnstalleerd op uw systeem. |

## <a name="tool-bar"></a>Werkbalk
Hallo-werkbalk zich onder Hallo menubalk bevat navigatie en taakpictogrammen. Elk pictogram is een snelkoppeling tooa specifieke taak.

### <a name="icon-descriptions"></a>Pictogram beschrijvingen
Hallo volgende tabel beschrijft Hallo pictogrammen die worden weergegeven op de werkbalk Hallo. 

| Pictogram | Beschrijving |
|:--- |:--- |
| ![Pijl-links](./media/storsimple-use-snapshot-manager/HCS_SSM_LeftArrow.png) |Klik op Hallo pijl-links pictogram tooreturn toohello vorige pagina. |
| ![Pijl-rechts](./media/storsimple-use-snapshot-manager/HCS_SSM_RightArrow.png) |Klik op volgende pagina van Hallo pijl naar rechts toogo toohello (Hallo pijl grijs wordt weergegeven, Hallo actie is niet beschikbaar als). |
| ![Pictogram omhoog](./media/storsimple-use-snapshot-manager/HCS_SSM_Up.png) |Klik op Hallo van pictogram toogo één niveau in de consolestructuur hello (Hallo **bereik** deelvenster). |
| ![Structuur van de console weergeven/verbergen](./media/storsimple-use-snapshot-manager/HCS_SSM_ShowConsoleTree.png) |Klik op Hallo weergeven/verbergen console structuur pictogram tooshow of verbergen Hallo **bereik** deelvenster. |
| ![Lijst exporteren](./media/storsimple-use-snapshot-manager/HCS_SSM_ExportListIcon.png) |Klik op Hallo export lijst pictogram tooexport tooa CSV-bestand met een lijst die u opgeeft. |
| ![Help-pictogram](./media/storsimple-use-snapshot-manager/HCS_SSM_HelpIcon.png) |Klik op Hallo help pictogram tooopen een MMC help-onderwerp. |
| ![Actiedeelvenster weergeven/verbergen](./media/storsimple-use-snapshot-manager/HCS_SSM_ShowAction.png) |Klik op Hallo weergeven/verbergen **acties** deelvenster pictogram tooshow of verbergen Hallo **acties** deelvenster. |

## <a name="scope-pane"></a>Deelvenster bereik
Hallo **bereik** deelvenster is de meest linkse venster Hallo in Hallo StorSimple Snapshot Manager UI. Het Hallo-console (of een knooppunt)-structuur bevat en Hallo primaire navigatie mechanisme voor StorSimple Snapshot Manager. 

### <a name="scope-pane-structure"></a>Bereik deelvenster Structuur
Hallo **bereik** deelvenster bevat een reeks klikbaar objecten (knooppunten) in een boomstructuur gerangschikt. 

![Deelvenster bereik](./media/storsimple-use-snapshot-manager/HCS_SSM_Scope_pane.png) 

* Klik op Hallo pijl pictogram volgende toohello knooppuntnaam tooexpand of samenvouwen een knooppunt.
* Klik op Hallo knooppuntnaam tooview Hallo status of de inhoud van een knooppunt. Hallo-informatie wordt weergegeven in Hallo **resultaten** deelvenster. 

Hallo **bereik** deelvenster bevat Hallo knooppunten te volgen: 

* [Knooppunt apparaten](#devices-node) 
* [Volumes knooppunt](#volumes-node) 
* [Knooppunt voor volume-groepen](#volume-groups-node) 
* [Back-knooppunt van het beleid](#backup-policies-node) 
* [Back-knooppunt van de catalogus](#backup-catalog-node) 
* [Taken knooppunt](#jobs-node) 

### <a name="scope-pane-tasks"></a>Bereik deelvenster Taken
U kunt Hallo **bereik** deelvenster toocomplete een actie op een specifiek knooppunt. een taak tooselect Doe een van de volgende Hallo:

* Met de rechtermuisknop op het Hallo-knooppunt, en selecteer vervolgens Hallo taak in Hallo menu dat verschijnt.
* Klik op Hallo-knooppunt en klik vervolgens op **actie** op de menubalk Hallo. Selecteer Hallo taak in Hallo menu dat verschijnt.
* Klik op Hallo-knooppunt en selecteert u vervolgens Hallo actie in Hallo **acties** deelvenster.

Wanneer u een knooppunt selecteert en een van deze methoden toosee een lijst met taken gebruiken, worden alleen acties die kunnen worden uitgevoerd op dat knooppunt worden weergegeven.

### <a name="devices-node"></a>Knooppunt apparaten
Hallo **apparaten** knooppunt Hallo StorSimple-apparaten en virtuele StorSimple-apparaten die verbonden tooStorSimple Snapshot Manager zijn vertegenwoordigt. Dit knooppunt tooconnect selecteren en configureren van een apparaat en importeren van de gekoppelde volumes, volumes groepen en bestaande back-ups. Meerdere apparaten kunnen worden verbonden tooa één host.

* tooexpand Hallo-knooppunt, klik op het pijlpictogram Hallo volgende te**apparaten**.
* toosee een menu met acties beschikbaar, met de rechtermuisknop op Hallo **apparaten** knooppunt of met de rechtermuisknop op Hallo knooppunten die worden weergegeven in Hallo uitgebreide weergave.
* een lijst met geconfigureerde apparaten toosee klikt u op **apparaten** in Hallo **bereik** deelvenster. Hallo-lijst van apparaten, evenals informatie over elk apparaat wordt weergegeven in Hallo **resultaten** deelvenster.

### <a name="volumes-node"></a>Volumes knooppunt
Hallo **Volumes** knooppunt vertegenwoordigt Hallo stations die overeenkomen met toohello volumes die zijn gekoppeld met de Hallo host, met inbegrip van die via iSCSI- en die zijn gedetecteerd via een apparaat gedetecteerd. Gebruik deze lijst knooppunt tooview Hallo van de beschikbare volumes en afzonderlijke volumes toovolume groepen toewijzen.

* tooexpand Hallo-knooppunt, klik op het pijlpictogram Hallo volgende te**Volumes**.
* toosee een menu met acties beschikbaar, met de rechtermuisknop op Hallo **Volumes** knooppunt of met de rechtermuisknop op Hallo knooppunten die worden weergegeven in Hallo uitgebreide weergave.
* toosee een lijst van volumes, klikt u op **Volumes** in Hallo **bereik** deelvenster. Hallo-lijst van volumes, samen met informatie over elk volume wordt weergegeven in Hallo **resultaten** deelvenster.

### <a name="volume-groups-node"></a>Knooppunt voor volume-groepen
Volume-groepen zijn ook wel consistentiecontrole groepen. Elke groep volume is een groep met toepassingsgerelateerde volumes waarmee tooensure toepassing consistentie tijdens de back-upbewerkingen. Gebruik Hallo **Volume groepen** knooppunt tooconfigure deze groepen en tootake interactieve back-ups of het maken van back-upschema's. 

* tooexpand Hallo-knooppunt, klik op het pijlpictogram Hallo volgende te**Volume groepen**.
* toosee een menu met acties beschikbaar, met de rechtermuisknop op Hallo **Volume groepen** knooppunt of met de rechtermuisknop op Hallo knooppunten die worden weergegeven in Hallo uitgebreide weergave.
* toosee een lijst met groepen van volume, klikt u op **Volume groepen** in Hallo **bereik** deelvenster. Hallo-lijst van groepen van volume, samen met informatie over elke groep volume wordt weergegeven in Hallo **resultaten** deelvenster.

### <a name="backup-policies-node"></a>Back-knooppunt van het beleid
Back-upbeleid zijn taakschema's voor lokale en cloud worden opgeslagen. Gebruik Hallo **back-upbeleid** knooppunt toospecify hoe vaak een back-up wordt gemaakt en hoe lang een back-up moet worden bewaard. 

* tooexpand Hallo-knooppunt, klik op het pijlpictogram Hallo volgende te**back-upbeleid**.
* toosee een menu met acties beschikbaar, met de rechtermuisknop op Hallo **back-upbeleid** knooppunt of met de rechtermuisknop op Hallo knooppunten die worden weergegeven in Hallo uitgebreide weergave.
* een lijst met back-upbeleid toosee klikt u op **back-upbeleid** in Hallo **bereik** deelvenster. Hallo-lijst van de back-upbeleid, samen met informatie over elk beleid wordt weergegeven in Hallo **resultaten** deelvenster.

> [!NOTE]
> U kunt maximaal 64 back-ups behouden.


### <a name="backup-catalog-node"></a>Back-knooppunt van de catalogus
Hallo **back-upcatalogus** knooppunt bevat lijsten met lokale en externe back-ups van Azure StorSimple-volumes. Dit knooppunt is geordend op het volume-groep, en elke groep volumecontainer bevat afzonderlijke structuren voor lokale momentopnamen (Hallo **lokale momentopname**s knooppunt) en in de cloud momentopnamen (Hallo **Cloudmomentopnamen** knooppunt ). Wanneer u uitgevouwen, wordt elke groep volumecontainer alle Hallo geslaagde back-ups die zijn uitgevoerd, interactief of door een geconfigureerde beleid.

* tooexpand Hallo-knooppunt, klik op het pijlpictogram Hallo volgende te**back-upcatalogus**.
* toosee een menu met acties beschikbaar, met de rechtermuisknop op Hallo **back-upcatalogus** knooppunt of met de rechtermuisknop op Hallo knooppunten die worden weergegeven in Hallo uitgebreide weergave.
* een lijst met back-upmomentopnamen toosee klikt u op **back-upcatalogus** in Hallo **bereik** deelvenster. Hallo-lijst van momentopnamen, samen met informatie over elke momentopname wordt weergegeven in Hallo **resultaten** deelvenster.

### <a name="local-snapshots-node"></a>Lokale momentopnamen knooppunt
Hallo **lokale momentopnamen** knooppunt een lijst met lokale momentopnamen voor een specifieke volume-groep. Hallo-knooppunt bevindt zich onder Hallo **back-upcatalogus** knooppunt in Hallo **bereik** deelvenster. Lokale momentopnamen zijn punt in tijd kopieën van volumegegevens die zijn opgeslagen op Hallo Azure StorSimple-apparaat. Normaal gesproken worden deze type back-up gemaakt en snel worden hersteld. Net als een lokale back-up, kunt u een lokale momentopname gebruiken.

* tooexpand Hallo-knooppunt, klik op het pijlpictogram Hallo volgende te**lokale momentopnamen**.
* toosee een menu met acties beschikbaar, met de rechtermuisknop op Hallo **lokale momentopnamen** knooppunt of met de rechtermuisknop op Hallo knooppunten die worden weergegeven in Hallo uitgebreide weergave.
* een lijst met lokale momentopnamen toosee klikt u op **lokale momentopnamen** in Hallo **bereik** deelvenster. Hallo-lijst van momentopnamen, samen met informatie over elke momentopname wordt weergegeven in Hallo **resultaten** deelvenster.

### <a name="cloud-snapshots-node"></a>Cloud momentopnamen knooppunt
Hallo **Cloudmomentopnamen** knooppunt cloudmomentopnamen voor een groep specifieke volume bevat. Hallo-knooppunt bevindt zich onder Hallo **back-upcatalogus** knooppunt in Hallo **bereik** deelvenster. Cloudmomentopnamen zijn punt in tijd kopieën van volumegegevens die zijn opgeslagen in de cloud Hallo. Een cloudmomentopname is gelijk tooa momentopname op een andere, externe opslagsysteem gerepliceerd. Cloudmomentopnamen zijn bijzonder nuttig voor herstel na noodgevallen.

* tooexpand Hallo-knooppunt, klik op het pijlpictogram Hallo volgende te**Cloudmomentopnamen**.
* toosee een menu met acties beschikbaar, met de rechtermuisknop op Hallo **Cloudmomentopnamen** knooppunt of met de rechtermuisknop op Hallo knooppunten die worden weergegeven in Hallo uitgebreide weergave.
* toosee een lijst met cloudmomentopnamen, klikt u op **Cloudmomentopnamen** in Hallo **bereik** deelvenster. Hallo-lijst van momentopnamen, samen met informatie over elke momentopname wordt weergegeven in Hallo **resultaten** deelvenster.

### <a name="jobs-node"></a>Taken knooppunt
Hallo **taken** knooppunt bevat informatie over de geplande uitgevoerd en recentelijk uitgevoerde back-uptaken. 

* tooexpand Hallo-knooppunt, klik op het pijlpictogram Hallo volgende te**taken**.
* toosee een menu met acties beschikbaar, met de rechtermuisknop op Hallo **taken** knooppunt of met de rechtermuisknop op Hallo knooppunten die worden weergegeven in Hallo uitgebreide weergave.
* een lijst met geplande taken toosee Vouw Hallo **taken** knooppunt en klik vervolgens op **geplande**. Hallo lijst van eerder geconfigureerde taken en informatie over elke taak wordt weergegeven in Hallo **resultaten** deelvenster. 
* een lijst met recentelijk uitgevoerde taken toosee Vouw Hallo **taken** knooppunt en klik vervolgens op **afgelopen 24 uur**. Er wordt een lijst met taken die zijn voltooid in Hallo afgelopen 24 uur weergegeven in Hallo **resultaten** deelvenster. Hallo **resultaten** deelvenster bevat ook informatie over elke voltooide taak.
* toosee een lijst met taken die momenteel worden uitgevoerd, vouw Hallo **taken** knooppunt en klik vervolgens op **met**. Hallo-lijst met actieve taken en informatie over elke taak wordt weergegeven in Hallo **resultaten** deelvenster.

## <a name="results-pane"></a>Deelvenster met resultaten
Hallo **resultaten** deelvenster Hallo middelste deelvenster van Hallo StorSimple Snapshot Manager UI is. Het bevat een lijst met en gedetailleerde statusinformatie voor Hallo-knooppunt die u hebt geselecteerd in Hallo **bereik** deelvenster.

### <a name="example"></a>Voorbeeld
toosee hello volgt, klikt u op Hallo **Volume groepen** knooppunt in Hallo **bereik** deelvenster. Hallo **resultaten** deelvenster geeft een lijst met groepen met informatie over elke groep volume.

![Deelvenster met resultaten](./media/storsimple-use-snapshot-manager/HCS_SSM_Results_pane.png) 

Kunt u Hallo details weergegeven in Hallo **resultaten** deelvenster: met de rechtermuisknop op een knooppunt in Hallo **bereik** deelvenster, klikt u op **weergave**, en klik vervolgens op **toevoegen/verwijderen Kolommen**.

## <a name="actions-pane"></a>Actiedeelvenster
Hallo **acties** deelvenster Hallo rechterdeelvenster in Hallo StorSimple Snapshot Manager UI is. Het bevat een menu van bewerkingen die u kunt uitvoeren op het Hallo-knooppunt, weergave of gegevens die u in Hallo selecteert **bereik** deelvenster of **resultaten** deelvenster. Hallo **acties** deelvenster bevat dezelfde als Hallo opdrachten Hallo **actie** menu's die beschikbaar voor de items in Hallo zijn **bereik** deelvenster en **resultaten**deelvenster. Zie voor een beschrijving van elke actie Hallo-tabel in Hallo **actie** sectie menu.

### <a name="examples"></a>Voorbeelden
toosee hello na bijvoorbeeld Hallo **bereik** deelvenster Vouw Hallo **taken** knooppunt en klik op **geplande**. Hallo **acties** deelvenster ziet u de beschikbare acties Hallo voor Hallo **geplande** knooppunt.

![Voorbeeld van de geplande taken deelvenster Acties](./media/storsimple-use-snapshot-manager/HCS_SSM_ActionsPane.png) 

toosee meer opties in Hallo **bereik** deelvenster Vouw Hallo **taken** knooppunt, klik op **geplande**, en klik vervolgens op een geplande taak in Hallo **resultaten**deelvenster. Hallo **acties** deelvenster ziet u Hallo beschikbare acties voor de geplande taak hello, zoals wordt weergegeven in Hallo voorbeeld te volgen.

![Voorbeeld van de taak acties deelvenster Acties](./media/storsimple-use-snapshot-manager/HCS_SSM_ActionsPane_Results.png)

## <a name="keyboard-navigation-and-shortcuts"></a>Toetsenbordnavigatie en snelkoppelingen
StorSimple Snapshot Manager kunt Hallo toegankelijkheidsfuncties van Windows-besturingssysteem Hallo en Hallo Microsoft Management Console (MMC). Dit omvat ook sommige toetsenbord navigatiefuncties en snelkoppelingen die specifieke toohello StorSimple Snapshot Manager, zoals beschreven in Hallo uit te voeren.

* [Toetsen voor toetsenbordnavigatie](#keyboard-navigation-keys) 
* [Menubalk sneltoetsen](#menu-bar-shortcut-keys) 
* [Sneltoetsen in het bereik](#scope-pane-shortcut-keys) 

### <a name="keyboard-navigation-keys"></a>Toetsen voor toetsenbordnavigatie
Hallo beschrijft volgende tabel Hallo sleutels die u toonavigate hello StorSimple Snapshot Manager-gebruikersinterface kunt gebruiken. 

| Navigatie-sleutel | Actie |
|:--- |:--- |
| Pijltoets-omlaag |Hallo omlaag Pijl sleutel toomove verticaal gebruiken toohello volgende item in een menu of deelvenster. |
| Voer |Druk op Hallo Enter key toocomplete een actie en ga vervolgens verder toohello volgende stap. Bijvoorbeeld, drukt u op Enter tooselect **volgende**, **OK**, of **maken**, en gaat u de volgende stap toohello in een wizard. |
| ESC |Druk op Hallo Esc sleutel tooclose een menu of toocancel en een pagina te sluiten. |
| F1 |Druk op Hallo F1 sleutel tooview een help-onderwerp voor het actieve venster Hallo. |
| F5 |Druk op Hallo F5 sleutel toorefresh een knooppunt. |
| F6 |Druk op Hallo F6 sleutel toomove van Hallo **bereik** deelvenster toohello **resultaten** deelvenster. |
| F10 |Druk op de menubalk van Hallo F10 sleutel toogo toohello. |
| Pijl-links |Hallo pijl sleutel toomove horizontaal links van een balk optie toohello vorige menuoptie gebruiken. Menu voor het vorige item Hallo item op Hallo menu balk, Hallo actie (of context) wordt weergegeven wanneer u de vorige toohello verplaatst. |
| Pijl-rechts |Hallo pijl naar rechts sleutel toomove horizontaal uit één menubalk optie toohello vervolgens gebruiken. Het volgende artikel op Hallo menu balk, Hallo actie (of context) menu toohello voor Hallo nieuwe item wordt weergegeven wanneer u verplaatst. |
| TAB-toets |Gebruik Hallo tabblad sleutel toomove toohello Volgend deelvenster op Hallo-console of toohello volgende selectie of in het tekstvak in een pagina. |
| Pijl-omhoog |Hallo up pijl sleutel toomove verticaal gebruiken toohello vorige item in een menu of deelvenster. |

### <a name="menu-bar-shortcut-keys"></a>Menubalk sneltoetsen
Hallo beschrijft volgende tabel Hallo-sneltoetsen voor Hallo menubalk. Nadat u Hallo snelkoppeling toetsen en Hallo menu wordt geopend, kunt u sneltoetsen voor menuopdrachten (Hallo onderstreepte sleutels op Hallo menu). Voor meer informatie over de menubalk Hallo gaat te[menubalk](#menu-bar).

| Snelkoppeling | Resultaat | Menu sneltoets | Resultaat |
|:--- |:--- |:--- |:--- |
| ALT + F |Hallo wordt geopend **bestand** menu. |N |Hiermee opent u een nieuw exemplaar van de console. |
|  |O |Hallo wordt geopend **Systeembeheer** pagina. | |
|  |S |Hiermee slaat u Hallo StorSimple Snapshot Manager-console. | |
|  |A |Hallo wordt geopend **OpslaanAls** pagina. | |
|  |M |Hallo wordt geopend **module toevoegen/verwijderen** pagina. | |
|  |P |Hallo wordt geopend **opties** pagina. | |
|  |H |Hiermee opent u een online-Help. | |
| ALT + A |Hallo wordt geopend **actie** menu. |I |Hiermee schakelt u optie Hallo importeren in- of uitschakelen. |
|  |W |Hiermee opent u een nieuwe StorSimple Snapshot Manager-console. | |
|  |F |Hallo StorSimple Snapshot Manager-console-updates. | |
|  |L |Hallo wordt geopend **lijst exporteren** pagina. | |
|  |H |Hiermee opent u een online-Help. | |
| ALT + V |Hallo wordt geopend **weergave** menu. |A |Hallo wordt geopend **kolommen toevoegen/verwijderen** pagina. |
|  |U |Hallo wordt geopend **weergave aanpassen** pagina. | |
| ALT + O |Hallo wordt geopend **Favorieten** menu. |A |Hallo wordt geopend **tooFavorites toevoegen** pagina. |
|  |O |Hallo wordt geopend **Favorieten indelen** pagina. | |
| ALT + W |Hallo wordt geopend **venster** menu. |N |Hiermee opent u een ander StorSimple Snapshot Manager-venster. |
|  |C |Geeft alle open consolevensters in een CSS-stijl. | |
|  |T |Geeft alle open consolevensters weer in een rasterpatroon. | |
|  |I |Pictogrammen in een horizontale rij onderaan Hallo van het scherm. | |
| ALT + H |Hallo wordt geopend **Help** menu. |H |Hiermee opent u een online-Help. |
|  |T |Hallo Microsoft TechNet Tech Center webpagina geopend. | |
|  |A |Hallo wordt geopend **over Microsoft Management Console** pagina. | |

### <a name="scope-pane-shortcut-keys"></a>Sneltoetsen in het bereik
Hallo volgende tabellen tonen Hallo snelkoppeling toetsencombinaties voor elk knooppunt in Hallo **bereik** deelvenster. 

* [Sneltoetsen voor knooppunt apparaten](#devices-node-shortcut-keys)
* [Sneltoetsen voor volumes knooppunt](#volumes-node-shortcut-keys)
* [Sneltoetsen voor volume groepen knooppunt](#volume-groups-node-shortcut-keys)
* [Back-up maken van beleid knooppunt sneltoetsen](#backup-policies-node-shortcut-keys)
* [Back-up van catalogus knooppunt sneltoetsen](#backup-catalog-node-shortcut-keys)
* [Sneltoetsen voor taken knooppunt](#jobs-node-shortcut-keys)

#### <a name="devices-node-shortcut-keys"></a>Sneltoetsen voor knooppunt apparaten
| Snelkoppeling menu | Resultaat |
|:--- |:--- |
| C |Hallo wordt geopend **configureren van een apparaat** pagina. |
| D |Hallo-lijst met apparaten en de Apparaatdetails wordt vernieuwd. |
| V |Hallo wordt geopend **weergave** menu. |
| W |Opent een nieuwe StorSimple Snapshot Manager-console die is gericht op het Hallo **Details** knooppunt. |
| F |Hallo StorSimple Snapshot Manager-console-updates. |
| L |Hallo wordt geopend **lijst exporteren** pagina. |
| H |Hiermee opent u een online-Help. |

#### <a name="volumes-node-shortcut-keys"></a>Sneltoetsen voor volumes knooppunt
| Snelkoppeling menu | Resultaat |
|:--- |:--- |
| V |Lijst met updates Hallo van volumes. |
| V (druk tweemaal) |Hallo wordt geopend **weergave** menu. |
| W |Opent een nieuwe StorSimple Snapshot Manager-console die is gericht op het Hallo **Volumes** knooppunt. |
| F |Hallo StorSimple Snapshot Manager-console-updates. |
| L |Hallo wordt geopend **lijst exporteren** pagina. |
| H |Hiermee opent u een online-Help. |

#### <a name="volume-groups-node-shortcut-keys"></a>Sneltoetsen voor volume groepen knooppunt
| Snelkoppeling menu | Resultaat |
|:--- |:--- |
| G |Hallo wordt geopend **maakt u een groep Volume** pagina. |
| V |Hallo wordt geopend **weergave** menu. |
| W |Opent een nieuwe StorSimple Snapshot Manager-console die is gericht op het Hallo **Volume groepen** knooppunt. |
| F |Hallo StorSimple Snapshot Manager-console-updates. |
| L |Hallo wordt geopend **lijst exporteren** pagina. |
| H |Hiermee opent u een online-Help. |

#### <a name="backup-policies-node-shortcut-keys"></a>Back-up maken van beleid knooppunt sneltoetsen
| Snelkoppeling menu | Resultaat |
|:--- |:--- |
| B |Hallo wordt geopend **een beleid maken** pagina. |
| V |Hallo wordt geopend **weergave** menu. |
| W |Opent een nieuwe StorSimple Snapshot Manager-console die is gericht op het Hallo **Volume groepen** knooppunt. |
| F |Hallo StorSimple Snapshot Manager-console-updates. |
| L |Hallo wordt geopend ** lijst exporteren ** pagina. |
| H |Hiermee opent u een online-Help. |

#### <a name="backup-catalog-node-shortcut-keys"></a>Back-up van catalogus knooppunt sneltoetsen
| Snelkoppeling menu | Resultaat |
|:--- |:--- |
| W |Opent een nieuwe StorSimple Snapshot Manager-console die is gericht op het Hallo **Volume groepen** knooppunt. |
| F |Hallo StorSimple Snapshot Manager-console-updates. |
| H |Hiermee opent u een online-Help. |

#### <a name="jobs-node-shortcut-keys"></a>Sneltoetsen voor taken knooppunt
| Snelkoppeling menu | Resultaat |
|:--- |:--- |
| V |Hallo wordt geopend **weergave** menu. |
| W |Opent een nieuwe StorSimple Snapshot Manager-console die is gericht op het Hallo **taken** knooppunt. |
| F |Hallo StorSimple Snapshot Manager-console-updates. |
| L |Hallo wordt geopend **lijst exporteren** pagina. |
| H |Hiermee opent u de online-Help |

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe te[StorSimple Snapshot Manager tooadminister uw StorSimple-oplossing gebruiken](storsimple-snapshot-manager-admin.md).
* Meer informatie over hoe te[StorSimple Snapshot Manager tooconnect gebruiken en beheren van apparaten](storsimple-snapshot-manager-manage-devices.md).

