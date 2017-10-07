---
title: 'Azure back-up: Systeemstatus terugzetten tooa Windows Server | Microsoft Docs'
description: Stap door stap uitleg voor Windows Server-systeemstatus terugzetten vanaf een back-up in Azure.
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/18/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: a45506507f53e2744350d3b6b2e52f1db415de4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="restore-system-state-toowindows-server"></a>De systeemstatus terugzetten tooWindows Server

Dit artikel wordt uitgelegd hoe toorestore systeemstatus van Windows Server back-ups van een Azure Recovery Services-kluis. toorestore systeemstatus, moet u een systeemstatusback-up hebben (gemaakt met behulp van instructies Hallo in [Back-up van systeemstatus](backup-azure-system-state.md#back-up-windows-server-system-state-preview)), en zorg ervoor dat u hebt geïnstalleerd Hallo [meest recente versie van Microsoft Azure Recovery Hallo Services (MARS)-agent](http://aka.ms/azurebackup_agent). Systeemstatus van Windows Server-gegevens herstellen vanaf een Azure Recovery Services-kluis is een proces in twee stappen:

1. Systeemstatus terugzetten als bestanden vanuit Azure Backup. Bij het herstellen van systeemstatus als bestanden vanuit Azure Backup, kunt u:
  * De systeemstatus terugzetten toohello dezelfde server waar Hallo back-ups zijn gemaakt, of
  * De systeemstatus terugzetten tooan alternatieve bestandsserver.

2. Toepassing hello hersteld systeemstatus bestanden tooa Windows Server.


## <a name="recover-system-state-files-toohello-same-server"></a>Systeemstatus herstellen bestanden toohello dezelfde server
Hallo stappen wordt uitgelegd hoe tooroll uw vorige status van Windows Server-configuratie tooa reservekopieën. Configuratie back tooa bekend, stabiele status van uw server rolling kan zeer waardevol zijn. Hallo volgende systeemstatus stappen terugzetten Hallo van server uit een Recovery Services-kluis. 

1. Open Hallo **Microsoft Azure Backup** -module. Als u niet waar de Hallo-module is geïnstalleerd weet, zoekt u Hallo computer of server voor **Microsoft Azure Backup**.

    Hallo bureaublad-app moet worden weergegeven in zoekresultaten Hallo.

2. Klik op **gegevens herstellen** toostart Hallo-wizard.

    ![Gegevens herstellen](./media/backup-azure-restore-windows-server/recover.png)

3. Op Hallo **aan de slag** deelvenster, toorestore Hallo gegevens toohello dezelfde server of computer, selecteer **deze server (`<server name>`)** en klik op **volgende**.

    ![Kies deze server optie toorestore Hallo gegevens toohello dezelfde machine](./media/backup-azure-restore-system-state/samemachine.png)

4. Op Hallo **herstelmodus Selecteer** deelvenster kiezen **systeemstatus** en klik vervolgens op **volgende**.

    ![Blader door bestanden](./media/backup-azure-restore-system-state/recover-type-selection.png)

5. In de agenda Hallo van **Volume selecteert en datum** deelvenster, selecteert u een herstel verwijzen. 

    U kunt vanaf elk willekeurig herstelpunt herstellen in de tijd. Datums **vet** Hallo beschikbaarheid van ten minste één herstelpunt aangeven. Wanneer u een datum selecteren als er meerdere herstelpunten beschikbaar zijn, kiest u Hallo specifiek herstelpunt van Hallo **tijd** vervolgkeuzelijst.

    ![Volume en datum](./media/backup-azure-restore-system-state/select-date.png)

6. Nadat u Hallo herstel punt toorestore hebt gekozen, klikt u op **volgende**.

    Azure Backup Hallo lokale herstelpunt koppelt en gebruikt als een volume herstel.

7. Geef Hallo bestemming voor Hallo herstelde bestanden van de systeemstatus op Hallo Volgend deelvenster, en klik op **Bladeren** tooopen Windows Verkenner en zoek Hallo bestanden en mappen die u wilt. Hallo-optie **kopieën te maken, zodat beide versies**, maakt kopieën van afzonderlijke bestanden in een bestaande systeemstatus bestandsarchief in plaats van Hallo kopie van het gehele systeemstatus archief Hallo maken.

    ![Opties voor herstel](./media/backup-azure-restore-system-state/recover-as-files.png)

8. Controleer de gegevens van herstel op Hallo van Hallo **bevestiging** deelvenster en klik op **herstellen**.

   ![Klik op herstellen tooacknowledge Hallo herstellen actie](./media/backup-azure-restore-system-state/confirm-recovery.png)

9. Kopiëren Hallo *WindowsImageBackup* map in Hallo herstel tooa niet-kritieke doelvolume van Hallo-server. Meestal is Hallo volume met het besturingssysteem Windows hello essentieel volume.

10. Wanneer Hallo herstel voltooid is, stappen Hallo in sectie Hallo [toepassen hersteld systeemstatus bestanden toohello Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server), toocomplete Hallo systeemstatus herstelproces.

## <a name="recover-system-state-files-tooan-alternate-server"></a>Systeemstatus herstellen bestanden tooan alternatieve server

Als uw Windows-Server beschadigd of niet toegankelijk is en u toorestore wilt het tooa stabiele status door het herstellen van Windows Server System State Hallo, kunt u Hallo beschadigd server systeemstatus terugzetten vanaf een andere server. Hallo stappen toohello terugzetten systeemstatus volgen op een afzonderlijke server gebruiken.  

Hallo-terminologie die wordt gebruikt in deze stap omvat het volgende:

- *Bronmachine* : de oorspronkelijke machine Hallo van welke Hallo back-up is gemaakt en die momenteel niet beschikbaar is.
- *Doelcomputer* – Hallo machine toowhich Hallo gegevens worden hersteld.
- *Voorbeeld kluis* – Hallo Recovery Services-kluis toowhich hello *bronmachine* en *doelmachine* zijn geregistreerd. <br/>

> [!NOTE]
> Back-ups die afkomstig zijn uit één machine kunnen niet herstelde tooa machine met een eerdere versie van besturingssysteem Hallo. Back-ups die afkomstig zijn uit een Windows Server 2016-computer kan niet worden hersteld bijvoorbeeld tooWindows Server 2012 R2. Hallo inverse is echter mogelijk. U kunt back-ups van Windows Server 2012 R2 toorestore Windows Server 2016.
>

1. Open Hallo **Microsoft Azure Backup** -module op Hallo *doelmachine*.
2. Zorg ervoor dat Hallo *doelmachine* en Hallo *bronmachine* zijn geregistreerde toohello dezelfde Recovery Services-kluis.
3. Klik op **gegevens herstellen** tooinitiate Hallo werkstroom.

    ![Gegevens herstellen](./media/backup-azure-restore-windows-server-classic/recover.png)

4. Selecteer **een andere server**

    ![Een andere Server](./media/backup-azure-restore-system-state/anotherserver.png)

5. Hallo-kluisreferentiebestand die overeenkomt met toohello bieden *voorbeeld kluis*. Als het kluisreferentiebestand Hallo is ongeldig (of verlopen), het downloaden van een nieuw kluisreferentiebestand van Hallo *voorbeeld kluis* in hello Azure-portal. Zodra het Hallo-kluisreferentiebestand is opgegeven, wordt Hallo Recovery Services-kluis die is gekoppeld aan het kluisreferentiebestand Hallo weergegeven.

6. Selecteer op Hallo Selecteer back-upserver deelvenster Hallo *bronmachine* uit Hallo lijst met computers weergegeven.

    ![Lijst met computers](./media/backup-azure-restore-windows-server-classic/machinelist.png)

7. Kies op Hallo herstelmodus Selecteer deelvenster **systeemstatus** en klik op **volgende**. 

    ![Search](./media/backup-azure-restore-system-state/recover-type-selection.png)

8. Op Hallo kalender in Hallo **Volume selecteert en datum** deelvenster, selecteert u een herstel verwijzen. U kunt vanaf elk willekeurig herstelpunt herstellen in de tijd. Datums **vet** Hallo beschikbaarheid van ten minste één herstelpunt aangeven. Wanneer u een datum selecteren als er meerdere herstelpunten beschikbaar zijn, kiest u Hallo specifiek herstelpunt van Hallo **tijd** vervolgkeuzelijst. 

    ![Zoeken naar objecten](./media/backup-azure-restore-system-state/select-date.png)

9. Nadat u Hallo herstel punt toorestore hebt gekozen, klikt u op **volgende**.

10. Op Hallo **System status herstelmodus Selecteer** deelvenster Hallo bestemming waar u de systeemstatus bestanden hersteld toobe wilt opgeven en klik vervolgens op **volgende**.

    ![Versleuteling](./media/backup-azure-restore-system-state/recover-as-files.png)

    Hallo-optie **kopieën te maken, zodat beide versies**, maakt kopieën van afzonderlijke bestanden in een bestaande systeemstatus bestandsarchief in plaats van Hallo kopie van het gehele systeemstatus archief Hallo maken.

11. Controleer de details op Hallo van herstel op Hallo bevestiging deelvenster en op **herstellen**. 

    ![Klik op Hallo herstellen knop tooconfirm Hallo herstelproces](./media/backup-azure-restore-system-state/confirm-recovery.png)

12. Kopiëren Hallo *WindowsImageBackup* directory tooa niet-kritieke volume van Hallo-server (bijvoorbeeld D:\). Meestal is Hallo volume met het besturingssysteem Windows hello essentieel volume.

13. Hallo herstelproces toocomplete gebruik Hallo volgende sectie te[toepassing hello hersteld systeemstatus bestanden op een Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server).




## <a name="apply-restored-system-state-on-a-windows-server"></a>Herstelde systeemstatus toepassen op een Windows Server

Wanneer u de systeemstatus als bestanden met behulp van de Azure Recovery Services Agent hebt hersteld, hersteld gebruik Hallo Windows Server Backup hulpprogramma tooapply Hallo systeemstatus tooWindows Server. Hallo Windows Server back-up is al beschikbaar op Hallo-server. Hallo stappen wordt uitgelegd hoe tooapply Hallo systeemstatus hersteld.

1. Uw server in de opdrachten tooreboot gebruik Hallo volgende *Directory Services Repair Mode*. In een opdrachtprompt met verhoogde bevoegdheid:

    ```
    PS C:\> Bcdedit /set safeboot dsrepair
    PS C:\> Shutdown /r /t 0
    ```

2. Na opnieuw opstarten hello, Hallo Windows Server Backup-module openen. Als u niet waar de Hallo-module is geïnstalleerd weet, zoekt u Hallo computer of server voor **Windows Server Backup**.

    Hallo bureaublad-app wordt weergegeven in zoekresultaten Hallo.

3. Selecteer in de module Hallo **lokale back-up**.

    ![Selecteer toorestore lokale back-up van daaruit](./media/backup-azure-restore-system-state/win-server-backup-local-backup.png)

4. Op Hallo lokale back-up-console in Hallo **actiedeelvenster**, klikt u op **herstellen** tooopen Hallo Wizard herstel.

5. Hallo optie selecteert, **een back-up die is opgeslagen in een andere locatie**, en klik op **volgende**.

   ![Kies toorecover tooa andere server](./media/backup-azure-restore-system-state/backup-stored-in-diff-location.png)

6. Wanneer u opgeeft locatietype hello, selecteer **externe gedeelde map** als uw back-up van systeemstatus herstelde tooanother-server. Als de status van het systeem lokaal zijn hersteld, selecteert u **lokale stations**. 

    ![Selecteer of toorecovery van de lokale server of een ander](./media/backup-azure-restore-system-state/ss-recovery-remote-shared-folder.png)

7. Voer Hallo pad toohello *WindowsImageBackup* directory, of kies Hallo lokale schijf met deze map (bijvoorbeeld D:\WindowsImageBackup) als onderdeel van Hallo bestanden systeemstatusherstel met Azure Recovery hersteld Services-Agent en klik op **volgende**.

    ![pad toohello gedeeld bestand](./media/backup-azure-restore-system-state/ss-recovery-remote-folder.png)

8. Selecteer Hallo systeemstatus versie toorestore wilt en klikt u op **volgende**.

9. Selecteer in het deelvenster Hallo Type herstelbewerking selecteren **systeemstatus** en klik op **volgende**.

10. Hallo-locatie van Hallo systeemstatusherstel, selecteert u **oorspronkelijke locatie**, en klik op **volgende**.

11. Bekijk de details van Hallo bevestiging, Controleer de instellingen voor opnieuw opstarten Hallo en op **herstellen** tooapplly Hallo systeemstatus bestanden hersteld.

    ![Start Hallo bestanden van de systeemstatus herstellen](./media/backup-azure-restore-system-state/launch-ss-recovery.png)

## <a name="special-considerations-for-system-state-recovery-on-active-directory-server"></a>Speciale overwegingen voor herstel van de systeemstatus op Active Directory-server

Systeemstatusback-up bevat Active Directory-gegevens. Volgende stappen toorestore Active Directory Domain Services (AD DS) uit de vorige status van huidige status tooa hello gebruiken.

1. Start Hallo-domeincontroller in de Directory Services Restore Mode (DSRM).
2. Volg de stappen Hallo [hier](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx) toouse Windows Server Backup cmdlets toorecover AD DS.


## <a name="troubleshoot-failed-system-state-restore"></a>Problemen met mislukte systeemstatus herstellen

Als Hallo vorige proces van het toepassen van de systeemstatus niet wordt voltooid, gebruikt u Hallo Windows Recovery Environment (Win RE) toorecover uw Windows-Server. Hallo volgende stappen wordt uitgelegd hoe toorecover Win opnieuw gebruiken. Gebruik deze optie alleen als Windows Server niet normaal wordt opgestart na het terugzetten van de systeemstatus. Hallo na systeembestanden gegevens, Wees voorzichtig worden gewist. 

1. Start op uw Windows-Server in Hallo Windows Recovery Environment (Win RE).

2. Selecteer oplossen in Hallo drie opties.

    ![menu openen](./media/backup-azure-restore-system-state/winre-1.png)

3. Van Hallo **geavanceerde opties** Schakel in het scherm **opdrachtprompt** en Hallo beheerder gebruikersnaam en wachtwoord opgeven.

   ![menu openen](./media/backup-azure-restore-system-state/winre-2.png)

4. Hallo server-beheerder gebruikersnaam en wachtwoord opgeven.

    ![menu openen](./media/backup-azure-restore-system-state/winre-3.png)

5. Wanneer u Hallo-opdrachtprompt in de beheerdersmodus openen, voert u de volgende opdracht tooget Hallo systeemstatus back-versies.

    ```
    Wbadmin get versions -backuptarget:<Volume where WindowsImageBackup folder is copied>:
    ```
    ![ophalen van de back-upversies systeemstatus](./media/backup-azure-restore-system-state/winre-4.png)

6. Hallo opdracht tooget na alle volumes die beschikbaar zijn in Hallo back-up uitvoeren.

    ```
    Wbadmin get items -version:<copy version from above step> -backuptarget:<Backup volume>
    ```

    ![ophalen van de back-upversies systeemstatus](./media/backup-azure-restore-system-state/winre-5.png)

7. Hallo herstelt volgende opdracht alle volumes die deel van Hallo systeemstatusback-up uitmaken. Houd er rekening mee dat deze stap alleen Hallo essentiële volumes die deel van de systeemstatus Hallo uitmaken herstelt. Alle andere gegevens worden gewist.

    ```
    Wbadmin start recovery -items:C: -itemtype:Volume -version:<Backupversion> -backuptarget:<backup target volume>
    ```
     ![ophalen van de back-upversies systeemstatus](./media/backup-azure-restore-system-state/winre-6.png)



## <a name="next-steps"></a>Volgende stappen
* Nu dat u uw bestanden en mappen hebt hersteld, kunt u [beheren van uw back-ups](backup-azure-manage-windows-server.md).
