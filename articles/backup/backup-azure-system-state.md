---
title: aaaBack van Windows system status tooAzure | Microsoft Docs
description: Meer informatie over tooback van de systeemstatus Hallo van Windows Server en/of tooAzure voor Windows-computers.
services: backup
documentationcenter: 
author: saurabhsensharma
manager: carmonm
editor: 
keywords: hoe toobackup; hoe tooback; back-bestanden en mappen
ms.assetid: 5b15ebf1-2214-4722-b937-96e2be8872bb
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: saurse;markgal
ms.openlocfilehash: be5d4be81af981c10de82add9fe962a730753cf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-windows-system-state-in-resource-manager-deployment"></a>Back-up van systeemstatus Windows in de implementatie van Resource Manager
Dit artikel wordt uitgelegd hoe tooback uw Windows Server-systeem tooAzure status. Het is een zelfstudie beoogde toowalk u bij het Hallo-basisbeginselen.

Als u tooknow meer informatie over Azure Backup wilt, Lees dit [overzicht](backup-introduction-to-azure-backup.md).

Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/) aan waarmee u toegang hebt tot alle services van Azure.

## <a name="create-a-recovery-services-vault"></a>Een Recovery Services-kluis maken
tooback van uw bestanden en mappen, moet u een Recovery Services-kluis in Hallo regio waar u toostore Hallo gegevens toocreate. U moet ook toodetermine hoe u uw opslag repliceren wilt.

### <a name="toocreate-a-recovery-services-vault"></a>toocreate een Recovery Services-kluis
1. Als u dit nog niet hebt gedaan, meld u aan toohello [Azure Portal](https://portal.azure.com/) met behulp van uw Azure-abonnement.
2. Klik op het menu Hub Hallo **meer services** en typt u in de lijst met resources Hallo **Recovery Services** en klik op **Recovery Services-kluizen**.

    ![Een Recovery Services-kluis maken, stap 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    Als er recovery services-kluizen in Hallo abonnement, worden Hallo kluizen weergegeven.
3. Op Hallo **Recovery Services-kluizen** menu, klikt u op **toevoegen**.

    ![Een Recovery Services-kluis maken, stap 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    Hallo Recovery Services vault blade wordt geopend, waarin u wordt gevraagd tooprovide een **naam**, **abonnement**, **resourcegroep**, en **locatie**.

    ![Een Recovery Services-kluis maken, stap 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. Voor **naam**, voer een beschrijvende naam tooidentify Hallo-kluis. de naam van de Hallo moet toobe unieke voor hello Azure-abonnement. Typ een naam die tussen 2 en 50 tekens bevat. De naam moet beginnen met een letter en mag alleen letters, cijfers en afbreekstreepjes bevatten.

5. In Hallo **abonnement** sectie, gebruikt u Hallo vervolgkeuzelijst toochoose hello Azure-abonnement. Als u slechts één abonnement, dat abonnement wordt weergegeven en kunt u de volgende stap toohello overslaan. Als u niet zeker weet welk abonnement toouse Hallo standaard gebruiken (of voorgestelde) abonnement. Er zijn alleen meerdere mogelijkheden als uw organisatieaccount is gekoppeld aan meerdere Azure-abonnementen.

6. In Hallo **resourcegroep** sectie:

    * Selecteer **nieuw** als u wilt dat toocreate een resourcegroep.
    of
    * Selecteer **gebruik bestaande** en klik op Hallo vervolgkeuzelijst toosee Hallo lijst met beschikbare resourcegroepen.

  Zie voor meer informatie over resourcegroepen Hallo [overzicht van Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).

7. Klik op **locatie** tooselect Hallo geografische regio voor Hallo kluis. Deze keuze bepaalt Hallo geografische regio waar uw back-upgegevens worden verzonden.

8. Aan de onderkant van de Hallo van blade Hallo Recovery Services-kluis, klikt u op **maken**.

    Het kan enkele minuten duren voordat Hallo die Recovery Services-kluis toobe gemaakt. Hallo statusmeldingen rechtsboven Hallo van Hallo portal bewaken. Zodra de kluis is gemaakt, wordt deze weergegeven in de lijst met Recovery Services-kluizen Hallo. Als u uw kluis na enkele minuten niet ziet, klik dan op **Vernieuwen**.

    ![Op de knop Vernieuwen klikken](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    Nadat u uw kluis in Hallo lijst met Recovery Services-kluizen ziet, bent u klaar tooset Hallo opslag redundantie.

### <a name="set-storage-redundancy-for-hello-vault"></a>Redundantie van gegevensopslag voor Hallo kluis instellen
Wanneer u een Recovery Services-kluis maakt, zorg ervoor dat redundantie van gegevensopslag geconfigureerde Hallo zoals u dat wilt.

1. Van Hallo **Recovery Services-kluizen** blade, klikt u op de nieuwe kluis Hallo.

    ![Selecteer Hallo nieuwe kluis in Hallo-lijst met Recovery Services-kluis](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    Wanneer u Hallo kluis selecteert, Hallo **Recovery Services-kluis** blade overzicht en de blade instellingen hello (*die Hallo-naam van de kluis Hallo Hallo boven heeft*) en Hallo details blade kluis openen.

    ![Het Hallo-opslagconfiguratie weergeven voor nieuwe kluis](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)
2. Op de blade instellingen Hallo nieuwe kluis, Hallo verticale dia tooscroll omlaag toohello sectie beheren en op **back-upinfrastructuur**.
    Hallo back-upinfrastructuur blade wordt geopend.
3. Klik op Hallo back-upinfrastructuur blade **back-upconfiguratie** tooopen hello **back-upconfiguratie** blade.

    ![De opslagconfiguratie Hallo voor nieuwe kluis instellen](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. Kies Hallo geschikte optie voor opslagreplicatie voor uw kluis.

    ![keuzes bij opslagconfiguratie](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    Uw kluis heeft standaard geografisch redundante opslag. Als u Azure als een eindpunt primaire back-upopslag gebruikt, gaat u verder toouse **geografisch redundante**. Als u geen Azure als een eindpunt primaire back-upopslag gebruikt, kiest u **lokaal redundante**, die zorgt voor lagere kosten voor hello Azure-opslag. U vindt meer informatie over de opties voor [geografisch redundante](../storage/common/storage-redundancy.md#geo-redundant-storage) en [lokaal redundante ](../storage/common/storage-redundancy.md#locally-redundant-storage) opslag in dit [overzicht van opslagredundantie](../storage/common/storage-redundancy.md).

Nu dat u kunt een kluis hebt gemaakt, kunt u deze voor de back-up van systeemstatus Windows configureren.

## <a name="configure-hello-vault"></a>Hallo kluis configureren
1. Op de blade van de Recovery Services-kluis (voor Hallo kluis u zojuist hebt gemaakt), in de sectie aan de slag Hallo Hallo, klikt u op **back-up**, vervolgens op Hallo **aan de slag met back-up** blade Selecteer  **Back-updoel**.

    ![Open de blade back-updoelstelling](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    Hallo **back-updoel** blade wordt geopend.

    ![Open de blade back-updoelstelling](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. Van Hallo **waar wordt uw workload uitgevoerd?** vervolgkeuzelijst, selecteer **On-premises**.

    U kiest **On-premises** omdat uw Windows Server of Windows-computer een fysieke machine is die zich niet in Azure bevindt.

3. Van Hallo **wat wilt u wilt dat toobackup?** selecteert u **systeemstatus**, en klik op **OK**.

    ![Bestanden en mappen configureren](./media/backup-azure-system-state/backup-goal-system-state.png)

    Als u op OK klikt, verschijnt een vinkje volgende te**back-updoel**, en Hallo **infrastructuur voorbereiden** blade wordt geopend.

    ![Nu de back-updoelstelling is geconfigureerd, gaat u de infrastructuur voorbereiden](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. Op Hallo **infrastructuur voorbereiden** blade, klikt u op **Agent downloaden voor Windows Server of Windows Client**.

    ![infrastructuur voorbereiden](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

    Als u van Windows Server essentiële gebruikmaakt, kiest u toodownload Hallo-agent voor Windows Server essentieel. Een pop-upmenu vraagt u toorun of MARSAgentInstaller.exe opslaan.

    ![Dialoogvenster MARSAgentInstaller](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. In het pop-upmenu Hallo downloaden, klikt u op **opslaan**.

    Standaard Hallo **MARSagentinstaller.exe** bestand tooyour downloadmap wordt opgeslagen. Als het Hallo-installatieprogramma is voltooid, ziet u een pop-upvenster waarin wordt gevraagd als u toorun Hallo installatieprogramma wilt of Hallo-map open.

    ![infrastructuur voorbereiden](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

    U hoeft niet tooinstall Hallo agent nog. Nadat u de kluisreferenties Hallo hebt gedownload, kunt u Hallo-agent installeren.

6. Op Hallo **infrastructuur voorbereiden** blade, klikt u op **downloaden**.

    ![kluisreferenties downloaden](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

    de map Downloads tooyour downloaden Hello kluisreferenties Nadat de kluisreferenties Hallo downloaden, ziet u een pop-upvenster waarin wordt gevraagd als u wilt dat tooopen of Hallo referenties op te slaan. Klik op **Opslaan**. Als u per ongeluk op **Open**, laten Hallo dialoogvenster waarmee wordt geprobeerd tooopen hello kluisreferenties, mislukken. U kunt de kluisreferenties Hallo niet openen. De volgende stap toohello worden voortgezet. Hallo kluisreferenties zijn in de map Downloads Hallo.   

    ![kluisreferenties downloaden is voltooid](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-hello-agent"></a>Installeren en registreren Hallo-agent

> [!NOTE]
> Inschakelen back-ups via hello Azure-portal is nog niet beschikbaar. Windows Server System State Hallo Microsoft Azure Recovery Services Agent tooback gebruikt.
>

1. Zoek en dubbelklik op Hallo **MARSagentinstaller.exe** vanuit Hallo Downloads map (of een andere locatie is opgeslagen).

    Hallo-installatieprogramma biedt een reeks berichten zoals deze pakt wordt geïnstalleerd en geregistreerd Hallo Recovery Services-agent.

    ![uitvoeren van installatiereferenties van de Recovery Services-agent](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. Hallo Microsoft Azure Recovery Services Agent-installatiewizard voltooien. wizard toocomplete hello, moet u:

   * Kies een locatie voor de installatie en cache map Hallo.
   * Geef uw proxyserveradres als u een proxy server tooconnect toohello serverinformatie internet.
   * Uw gebruikersnaam en wachtwoord invoeren als u gebruikmaakt van een geverifieerde proxyserver.
   * Geef referenties op Hallo gedownload kluis
   * Hallo-wachtwoordzin voor versleuteling op een veilige locatie opslaan.

     > [!NOTE]
     > Als u kwijtraakt of Hallo wachtwoordzin vergeet, Microsoft u niet helpen Hallo back-upgegevens te herstellen. Hallo-bestand opslaan in een veilige locatie. Het is vereiste toorestore een back-up.
     >
     >

Hallo-agent wordt nu geïnstalleerd en uw computer is ingeschreven toohello kluis. U bent klaar tooconfigure en uw back-up plannen.

## <a name="back-up-windows-server-system-state-preview"></a>Back-up van Windows Server System State (Preview)
de eerste back-up Hallo omvat drie taken:

* Systeemstatusback-up met hello Azure backup-agent inschakelen
* Hallo back-up plannen
* Back-up van bestanden en mappen voor Hallo eerst

toocomplete hello eerste back-up, gebruik Hallo Microsoft Azure Recovery Services agent.

### <a name="tooenable-system-state-backup-using-hello-azure-backup-agent"></a>tooenable systeemstatusback-up met behulp van Azure Backup agent Hallo

1. Voer in een PowerShell-sessie Hallo opdracht toostop hello Azure Backup-engine te volgen.

  ```
  PS C:\> Net stop obengine
  ```

2. Open Hallo Windows-register.

  ```
  PS C:\> regedit.exe
  ```

3. Voeg Hallo registersleutel Hello volgende DWord-waarde opgegeven.

  | Registerpad | Registersleutel | DWord-waarde |
  |---------------|--------------|-------------|
  | HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider | TurnOffSSBFeature | 2 |

4. Hallo Backup-engine opnieuw door het uitvoeren van de volgende opdracht in een verhoogde opdrachtprompt Hallo.

  ```
  PS C:\> Net start obengine
  ```

### <a name="tooschedule-hello-backup-job"></a>back-uptaak van tooschedule Hallo

1. Open Hallo Microsoft Azure Recovery Services agent. U vindt deze door te zoeken naar **Microsoft Azure Backup** op uw machine.

    ![Hello Azure Recovery Services-agent starten](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)

2. Klik in de Recovery Services-agent Hallo op **back-up plannen**.

    ![Een back-up van de Windows Server plannen](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)

3. Op Hallo aan de slag pagina van de Wizard Back-up plannen hello, klikt u op **volgende**.

4. Klik op Hallo Items selecteren tooBackup pagina op **Items toevoegen**.

5. Selecteer **systeemstatus** en klik vervolgens op **OK**.

6. Klik op **Volgende**.

7. Hello systeemstatusback-up en retentie plannen is automatisch ingesteld tooback van elke zondag om 21:00 uur lokale tijd, en de bewaarperiode Hallo too60 dagen.

   > [!NOTE]
   > Beleid voor het back-up en retentie van systeemstatus wordt automatisch geconfigureerd. Als u back-ups van bestanden en mappen bovendien toohello Windows Server System State, kunt u alleen Hallo-back-up en retentie beleid voor back-ups van de wizard Hallo opgeven. 
   >

8. Op de bevestigingspagina Hallo Hallo informatie bekijken en klik vervolgens op **voltooien**.

9. Nadat het Hallo-wizard is voltooid voor het maken van back-upschema hello, klikt u op **sluiten**.

### <a name="tooback-up-windows-server-system-state-for-hello-first-time"></a>tooback van Windows Server-systeemstatus voor Hallo eerst

1. Zorg ervoor dat er zijn geen updates in behandeling voor Windows Server waarvoor opnieuw opstarten.

2. Klik in het Hallo Recovery Services-agent op **Back-Up uit** toocomplete Hallo eerste seeding via Hallo netwerk.

    ![Nu back-up maken van Windows Server](./media/backup-try-azure-backup-in-10-mins/backup-now.png)

3. Op de bevestigingspagina Hallo revisie Hallo-instellingen die de Wizard Back-Up nu Hallo tooback Hallo machine gebruikt. Klik vervolgens op **Back-up maken**.

4. Klik op **sluiten** tooclose Hallo-wizard. Als u Hallo wizard sluit voordat de back-upproces Hallo is voltooid, blijft Hallo wizard toorun op Hallo achtergrond.

5. Als u back-up bestanden en mappen op uw server bovendien toohello Windows Server System State, wordt de wizard nu back-up in Hallo alleen reservekopie van bestanden. tooperform de systeemstatus van een ad-hoc back-up, Hallo volgende PowerShell-opdracht gebruiken:

    ```
    PS C:\> Start-OBSystemStateBackup
    ```

  Nadat de eerste back-up Hallo is voltooid, Hallo **taak voltooid** status wordt weergegeven in Hallo back-up-console.

  ![IR voltooid](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="frequently-asked-questions"></a>Veelgestelde vragen

Hallo bevatten onderstaande vragen en antwoorden aanvullende informatie.

### <a name="what-is-hello-staging-volume"></a>Wat is Hallo fasering Volume?

Hallo fasering Volume vertegenwoordigt Hallo tussenliggende locatie waar Hallo standaard beschikbaar zijn, Windows Server Backup Hallo systeemstatusback-up voorbereid. Azure backup-agent en vervolgens worden gecomprimeerd en versleuteld deze tussenliggende back-up en verzendt dat deze via een beveiligde HTTPS-Protocol toohello Recovery Services-kluis hebt geconfigureerd. **Sterk aanbevolen dat u Hallo fasering Volume instellen in een niet-Windows-besturingssysteemvolume. Als u problemen met de systeemstatusback-ups ziet, is het Hallo-locatie van het Volume fasering controleren Hallo eerste probleemoplossing.** 

### <a name="how-can-i-change-hello-staging-volume-path-specified-in-hello-azure-backup-agent"></a>Hoe kan ik Hallo fasering Volumepad is opgegeven in hello Azure backup-agent wijzigen?

Hallo fasering Volume bevindt zich in de cachemap Hallo standaard. 

1. toochange deze locatie, gebruik Hallo na de opdracht (in een verhoogde opdrachtprompt):
  ```
  PS C:\> Net stop obengine
  ```

2. Werk vervolgens Hallo registervermeldingen met Hallo pad toohello nieuwe tijdelijke map Volume te volgen.

  |Registerpad|Registersleutel|Waarde|
  |-------------|------------|-----|
  |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider | SSBStagingPath | nieuwe volume faseringslocatie |

Hallo pad voor gefaseerde installatie is hoofdlettergevoelig en moet Hallo exact hetzelfde hoofdlettergebruik als wat op Hallo server bestaat. 

3. Zodra u Hallo fasering Volumepad wijzigt, start opnieuw op Hallo Backup-engine:
  ```
  PS C:\> Net start obengine
  ```
4. toopick up Hallo gewijzigd pad, open Hallo Microsoft Azure Recovery Services agent en een ad-hoc back-up van systeemstatus trigger.

### <a name="why-is-hello-system-state-default-retention-set-too60-days"></a>Waarom is de systeemstatus Hallo standaard bewaren too60 dagen instellen?

Hallo-levensduur van een systeemstatusback-up is hetzelfde als de instelling voor Windows Server Active Directory-rol Hallo Hallo 'tombstone-levensduur' Hallo. de standaardwaarde Hallo voor Hallo tombstone-levensduur vermelding is 60 dagen. Deze waarde kan worden ingesteld op Hallo Directory Service (NTDS) config-object.

### <a name="how-do-i-change-hello-default-backup-and-retention-policy-for-system-state"></a>Hoe wijzig ik Hallo standaard back-up- en bewaarbeleid voor systeemstatus

toochange hello standaard back-up en het bewaarbeleid voor systeemstatus:
1. Stop Hallo Backup-engine. Hallo volgende opdracht uit een verhoogde opdrachtprompt worden uitgevoerd.

  ```
  PS C:\> Net stop obengine
  ```

2. Toevoegen of bijwerken van de volgende registervermeldingen in HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider Hallo.

  |Naam van routeringsregister|Beschrijving|Waarde|
  |-------------|-----------|-----|
  |SSBScheduleTime|Tijd van de gebruikte tooconfigure Hallo Hallo back-up. Standaardinstelling is 21: 00 lokale tijd.|DWord: Indeling UUMM (decimaal) zo 2130 voor 9:30:00 lokale tijd|
  |SSBScheduleDays|Gebruikte tooconfigure Hallo dagen wanneer systeemstatusback-up moet worden uitgevoerd op Hallo opgegeven tijd. Afzonderlijke cijfers opgeven dagen van week Hallo. zondag 0, 1 is maandag, enzovoort. Standaarddag voor back-up is zondag.|DWord: dagen van Hallo week toorun back-up (decimaal), bijvoorbeeld 1230 plant u back-ups op maandag, dinsdag, woensdag en zondag.|
  |SSBRetentionDays|Gebruikte tooconfigure Hallo dagen tooretain back-up. Standaardwaarde is 60. Maximaal toegestane waarde is 180.|DWord: Dagen tooretain back-up (decimaal).|

3. Gebruik Hallo volgende opdracht toorestart Hallo back-engine.
    ```
    PS C:\> Net start obengine
    ```

4. Open Hallo Microsoft Recovery Services agent.

5. Klik op **back-up plannen** en klik vervolgens op **volgende** totdat u Hallo wijzigingen weer.

6. Klik op **voltooien** tooapply Hallo wijzigingen.


## <a name="questions"></a>Vragen?
Als u vragen hebt of als er een functie die u toosee opgenomen wilt, [Stuur ons feedback](http://aka.ms/azurebackup_feedback).

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over [back-ups maken van Windows-machines](backup-configure-vault.md).
* Wanneer u eenmaal een back-up hebt gemaakt van uw bestanden en mappen, kunt u [uw kluizen en servers beheren](backup-azure-manage-windows-server.md).
* Als u een back-up toorestore moet, gebruikt u in dit artikel te[bestanden tooa Windows-machine herstellen](backup-azure-restore-windows-server.md).
