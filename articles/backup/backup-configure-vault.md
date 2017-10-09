---
title: aaaUse Azure Backup agent tooback van bestanden en mappen | Microsoft Docs
description: "Hallo Microsoft Azure Backup agent tooback van Windows-bestanden en mappen tooAzure gebruiken. Een Recovery Services-kluis maken, Hallo backup-agent installeren en definiëren van de back-upbeleid Hallo Hallo eerste back-up uitvoeren op Hallo bestanden en mappen."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: back-upkluis; back-up van een WindowsServer. back-upvensters;
ms.assetid: 7f5b1943-b3c1-4ddb-8fb7-3560533c68d5
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: be203c24841971872b5c6e7cf260a2fa5c58ac47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-windows-server-or-client-tooazure-using-hello-resource-manager-deployment-model"></a>Back-up van een Windows Server of client tooAzure met Hallo Resource Manager-implementatiemodel
> [!div class="op_single_selector"]
> * [Azure Portal](backup-configure-vault.md)
> * [Klassieke portal](backup-configure-vault-classic.md)
>
>

Dit artikel wordt uitgelegd hoe de bestanden en mappen tooAzure tooback van uw Windows Server (of Windows-client) met het gebruik van Azure Backup Hallo Resource Manager-implementatiemodel.

[!INCLUDE [learn-about-deployment-models](../../includes/backup-deployment-models.md)]

![Back-upproces stappen](./media/backup-configure-vault/initial-backup-process.png)

## <a name="before-you-start"></a>Voordat u begint
tooback u een server of client tooAzure, moet u een Azure-account. Als u niet hebt, kunt u een [gratis account](https://azure.microsoft.com/free/) binnen een paar minuten.

## <a name="create-a-recovery-services-vault"></a>Een Recovery Services-kluis maken
Een Recovery Services-kluis is een entiteit waarmee alle Hallo back-ups en herstelpunten die u gedurende een bepaalde periode maakt zijn opgeslagen. Hallo Recovery Services-kluis bevat ook Hallo back-upbeleid toegepast toohello beveiligde bestanden en mappen. Wanneer u een Recovery Services-kluis maakt, moet u ook de juiste opslagoptie redundantie Hallo selecteren.

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

    * Selecteer **nieuw** als u wilt dat toocreate een nieuwe resourcegroep.
    of
    * Selecteer **gebruik bestaande** en klik op Hallo vervolgkeuzelijst toosee Hallo lijst met beschikbare resourcegroepen.

  Zie voor meer informatie over resourcegroepen Hallo [overzicht van Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).

7. Klik op **locatie** tooselect Hallo geografische regio voor Hallo kluis. Deze keuze bepaalt Hallo geografische regio waar uw back-upgegevens worden verzonden.

8. Aan de onderkant van de Hallo van blade Hallo Recovery Services-kluis, klikt u op **maken**.

  Het kan enkele minuten duren voordat Hallo die Recovery Services-kluis toobe gemaakt. Hallo statusmeldingen rechtsboven Hallo van Hallo portal bewaken. Zodra de kluis is gemaakt, wordt deze weergegeven in de lijst met Recovery Services-kluizen Hallo. Als u uw kluis na enkele minuten niet ziet, klik dan op **Vernieuwen**.

  ![Op de knop Vernieuwen klikken](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

  Nadat u uw kluis in Hallo lijst met Recovery Services-kluizen ziet, bent u klaar tooset Hallo opslag redundantie.


### <a name="set-storage-redundancy"></a>Redundantie van gegevensopslag instellen
Als u voor het eerst een Recovery Services-kluis maakt, bepaalt u hoe uw opslag wordt gerepliceerd.

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

Nu dat u kunt een kluis hebt gemaakt, het voorbereiden van uw infrastructuur tooback van bestanden en mappen door te downloaden en installeren Hallo Microsoft Azure Recovery Services agent, kluisreferenties downloaden en met behulp van deze agent referenties tooregister Hallo met Hallo-kluis.

## <a name="configure-hello-vault"></a>Hallo kluis configureren

1. Op de blade van de Recovery Services-kluis (voor Hallo kluis u zojuist hebt gemaakt), in de sectie aan de slag Hallo Hallo, klikt u op **back-up**, vervolgens op Hallo **aan de slag met back-up** blade Selecteer  **Back-updoel**.

  ![Open de blade back-updoelstelling](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

  Hallo **back-updoel** blade wordt geopend. Als de Recovery Services-kluis Hallo eerder is geconfigureerd, Hallo **back-updoel** blades geopend wanneer u klikt op **back-up** blade op Hallo Recovery Services-kluis.

  ![Open de blade back-updoelstelling](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. Van Hallo **waar wordt uw workload uitgevoerd?** vervolgkeuzelijst, selecteer **On-premises**.

  U kiest **On-premises** omdat uw Windows Server of Windows-computer een fysieke machine is die zich niet in Azure bevindt.

3. Van Hallo **wat wilt u wilt dat toobackup?** selecteert u **bestanden en mappen**, en klik op **OK**.

  ![Bestanden en mappen configureren](./media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

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
> Inschakelen back-ups via hello Azure-portal is nog niet beschikbaar. Gebruik Hallo Microsoft Azure Recovery Services Agent tooback van uw bestanden en mappen.
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

## <a name="network-and-connectivity-requirements"></a>Netwerk- en verbindingsvereisten

Als uw machine/de proxy toegang tot internet beperkt heeft, moet u controleren of firewall-instellingen op Hallo machine/proxy geconfigureerde tooallow Hallo volgende URL's zijn: <br>
    1. www.msftncsi.com
    2. *.Microsoft.com
    3. *.WindowsAzure.com
    4. *.microsoftonline.com
    5. *.windows.ne


## <a name="create-hello-backup-policy"></a>Hallo back-upbeleid maken
back-upbeleid Hallo is Hallo planning wanneer herstelpunten zijn gemaakt en Hallo tijdsduur Hallo herstelpunten worden bewaard. Gebruik Hallo Microsoft Azure Backup agent toocreate Hallo back-upbeleid voor bestanden en mappen.

### <a name="toocreate-a-backup-schedule"></a>een back-upschema toocreate
1. Open Hallo Microsoft Azure backup-agent. U vindt deze door te zoeken naar **Microsoft Azure Backup** op uw machine.

    ![Hello Azure backup-agent starten](./media/backup-configure-vault/snap-in-search.png)
2. In Hallo backup-agent **acties** deelvenster, klikt u op **back-up plannen** toolaunch Hallo de Wizard Back-up plannen.

    ![Een back-up van de Windows Server plannen](./media/backup-configure-vault/schedule-first-backup.png)

3. Op Hallo **aan de slag** pagina Hallo Wizard Back-up plannen, klikt u op **volgende**.
4. Op Hallo **Items selecteren tooBackup** pagina, klikt u op **Items toevoegen**.

  Hallo Items selecteren dialoogvenster wordt geopend.

5. Selecteer Hallo bestanden en mappen wilt tooprotect en klik vervolgens op **OK**.
6. In Hallo **Items selecteren tooBackup** pagina, klikt u op **volgende**.
7. Op Hallo **back-upschema specificeren** pagina, geeft u de back-upschema Hallo en klik op **volgende**.

    U kunt dagelijkse back-ups (maximaal drie keer per dag en wekelijkse back-ups plannen.

    ![Items voor back-up van Windows Server](./media/backup-configure-vault/specify-backup-schedule-close.png)

   > [!NOTE]
   > Zie voor meer informatie over hoe toospecify back-upschema Hallo Hallo artikel [met Azure Backup tooreplace uw tape-infrastructuur](backup-azure-backup-cloud-as-tape.md).
   >
   >

8. Op Hallo **retentiebeleid selecteren** up Hallo specifieke bewaren beleidsregels Hallo voor back-up Hallo kiezen en op **volgende**.

    Hallo bewaarbeleid geeft Hallo duur welke Hallo back-up is opgeslagen. In plaats van alleen 'plat beleid' voor alle back-uppunten geven, kunt u verschillende Bewaarbeleidsregels op basis van wanneer Hallo back-up. Uw behoeften, kunt u Hallo dagelijkse, wekelijkse, maandelijkse en jaarlijkse bewaren beleid toomeet wijzigen.
9. Kies op Hallo eerste back-uptype kiezen pagina Hallo-type voor eerste back-up. Hallo-optie ingesteld laat **automatisch via netwerk Hallo** geselecteerd en klik vervolgens op **volgende**.

    U kunt back-up automatisch via netwerk hello, of u offline back-ups. Hallo rest van dit artikel beschrijft Hallo-proces voor het automatisch een back-up maken. Als u liever toodo een offline back-up, Hallo artikel lezen [Offline back-werkstroom in Azure Backup](backup-azure-backup-import-export.md) voor meer informatie.
10. Op de bevestigingspagina Hallo Hallo informatie bekijken en klik vervolgens op **voltooien**.
11. Nadat het Hallo-wizard is voltooid voor het maken van back-upschema hello, klikt u op **sluiten**.

### <a name="enable-network-throttling"></a>Netwerkbeperking inschakelen
Hallo Microsoft Azure Backup agent biedt netwerkbeperking. Gebeurtenisbeperking bepaalt hoe de netwerkbandbreedte tijdens de gegevensoverdracht wordt gebruikt. Dit besturingselement kan nuttig zijn als u tooback van gegevens tijdens werkuren nodig maar niet dat Hallo back-upproces toointerfere met andere internetverkeer wilt. Beperking van toepassing is tooback up- en herstelbewerkingen.

> [!NOTE]
> Netwerkbeperking is niet beschikbaar op Windows Server 2008 R2 SP1, Windows Server 2008 SP2 of Windows 7 (met servicepacks). Quality of Service (QoS) stelt Hello Azure Backup netwerkbeperking functie op Hallo lokale besturingssysteem. Hoewel Azure back-up kan deze besturingssystemen beveiligen kunt, werkt niet met Azure Backup netwerkbeperking Hallo-versie van QoS beschikbaar op deze platforms. Netwerkbeperking kan worden gebruikt voor alle andere [ondersteunde besturingssystemen](backup-azure-backup-faq.md).
>
>

**netwerkbeperking tooenable**

1. Klik in de Microsoft Azure Backup-agent Hallo **eigenschappen wijzigen**.

    ![Eigenschappen wijzigen](./media/backup-configure-vault/change-properties.png)
2. Op Hallo **bandbreedtebeperking** tabblad, selecteer Hallo **inschakelen voor gebruik van internetbandbreedte voor back-upbewerkingen** selectievakje.

    ![Netwerkbeperking](./media/backup-configure-vault/throttling-dialog.png)
3. Nadat u hebt ingeschakeld beperking, geef Hallo bandbreedte toegestaan voor back-up van de gegevensoverdracht tijdens **werkuren** en **niet-werkuren**.

    Hallo bandbreedte waarden begint in 512 kilobits per seconde (Kbps) en omhoog too1, 023 megabytes per seconde (MBps) kunnen gaan. U kunt ook Hallo start aanwijzen en voltooien voor **werkuren**, en welke dagen van week Hallo worden beschouwd als werkdagen. Uren buiten aangewezen werk uren worden beschouwd als niet-werk uren.
4. Klik op **OK**.

### <a name="tooback-up-files-and-folders-for-hello-first-time"></a>tooback van bestanden en mappen voor de eerste keer Hallo
1. In de back-upagent hello, klikt u op **Back-Up uit** toocomplete Hallo eerste seeding via Hallo-netwerk.

    ![Nu back-up maken van Windows Server](./media/backup-configure-vault/backup-now.png)
2. Op de bevestigingspagina Hallo revisie Hallo-instellingen die de Wizard Back-Up nu Hallo tooback Hallo machine gebruikt. Klik vervolgens op **Back-up maken**.
3. Klik op **sluiten** tooclose Hallo-wizard. Als u dit doet voordat Hallo back-upproces is voltooid, blijft Hallo wizard toorun op Hallo achtergrond.

Nadat de eerste back-up Hallo is voltooid, Hallo **taak voltooid** status wordt weergegeven in Hallo back-up-console.

![IR voltooid](./media/backup-configure-vault/ircomplete.png)

## <a name="questions"></a>Vragen?
Als u vragen hebt of als er een functie die u toosee opgenomen wilt, [Stuur ons feedback](http://aka.ms/azurebackup_feedback).

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over back-ups van virtuele machines of andere werkbelastingen:

* Wanneer u eenmaal een back-up hebt gemaakt van uw bestanden en mappen, kunt u [uw kluizen en servers beheren](backup-azure-manage-windows-server.md).
* Als u een back-up toorestore moet, gebruikt u in dit artikel te[bestanden tooa Windows-machine herstellen](backup-azure-restore-windows-server.md).
