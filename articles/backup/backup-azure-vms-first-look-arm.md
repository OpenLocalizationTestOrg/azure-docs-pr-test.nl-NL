---
title: 'Eerste blik: virtuele machines van Azure beveiligen met een Recovery Services-kluis | Microsoft Docs'
description: "Beveilig virtuele machines van Azure met een Recovery Services-kluis. Gebruik back-ups van Resource Manager geïmplementeerde VM's, klassieke geïmplementeerde VM's en Premium-opslag virtuele machines, versleuteld virtuele machines, virtuele machines op schijven beheerd tooprotect uw gegevens. Maak en registreer een Recovery Services-kluis. Registreer VM's, maak beleid en beveilig VM's in Azure."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keyword: backups; vm backup
ms.assetid: 45e773d6-c91f-4501-8876-ae57db517cd1
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 08/15/2017
ms.author: markgal;jimpark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 70e4700abb76e16e32e1ead06ce1dbe277e1f0e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-toorecovery-services-vaults"></a>Back-up van virtuele machines in Azure tooRecovery Services-kluizen
> [!div class="op_single_selector"]
> * [Virtuele machines beveiligen met een Recovery Services-kluis](backup-azure-vms-first-look-arm.md)
> * [Virtuele machines beveiligen met een back-upkluis](backup-azure-vms-first-look.md)
>
>

Deze zelfstudie leert u Hallo stappen voor het maken van een recovery services-kluis en back-ups van Azure een virtuele machine (VM). Recovery Services-kluizen beveiligen:

* VM's die zijn geïmplementeerd met Azure Resource Manager
* Klassieke VM's
* Standaardopslag-VM's
* Premium Storage-VM's
* Virtuele machines die op beheerde schijven worden uitgevoerd
* Virtuele machines die met Azure Disk Encryption zijn versleuteld, met BitLocker-versleutelingssleutels (BEK) en Key Encryption Keys (KEK)
* Toepassingsconsistente back-up van Windows-VM's met behulp van VSS- en Linux-VM's en aangepaste scripts met momentopnamen vooraf en achteraf

Zie voor meer informatie over het beveiligen van virtuele machines van de Premium-opslag Hallo artikel [Back-up en herstellen van VM's voor Premium-opslag](backup-introduction-to-azure-backup.md#using-premium-storage-vms-with-azure-backup). Zie [Back-ups van virtuele machines op beheerde schijven maken en terugzetten](backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup) voor meer informatie over ondersteuning voor virtuele machines op beheerde schijven. Voor meer informatie over pre- en post-script framework voor Linux-VM back-ups raadpleegt u [Application consistent Linux VM backup using pre-script and post-script (Toepassingsconsistente back-up van Linux-VM's met pre-script en post-script)] (https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).

Raadpleeg toofind meer over wat u kunt u back-up en wat u kunt geen, [hier](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm)

> [!NOTE]
> Deze zelfstudie wordt ervan uitgegaan dat er al een virtuele machine in uw Azure-abonnement en dat u maatregelen tooallow Hallo Backup-service tooaccess Hallo VM hebt genomen.
>
>

[!INCLUDE [learn-about-Azure-Backup-deployment-models](../../includes/backup-deployment-models.md)]

Afhankelijk van het aantal virtuele machines Hallo u tooprotect wilt, kunt u beginnen met uit verschillende beginpunten. Als u tooback van meerdere virtuele machines in één bewerking wilt, gaat u toohello Recovery Services-kluis en [initiëren Hallo back-uptaak van Hallo kluisdashboard](backup-azure-vms-first-look-arm.md#configure-the-backup-job-from-the-recovery-services-vault). Als u tooback een virtuele machine wilt, kunt u back-uptaak Hallo VM management Blade starten.

## <a name="configure-hello-backup-job-from-hello-vm-management-blade"></a>Back-uptaak Hallo Hallo VM management Blade configureren

Hallo volgende stappen tooconfigure Hallo back-uptaak uit Hallo virtual machine management-blade in hello Azure-portal gebruiken. Deze stappen toohello virtuele machines in de klassieke portal Hallo niet van toepassing.

1. Meld u aan toohello [Azure-portal](https://portal.azure.com/).
2. Klik op het menu Hub Hallo **meer Services** en typ in het dialoogvenster Filter Hallo **virtuele machines**. Terwijl u typt, filtert Hallo lijst met resources. Wanneer u Virtuele machines ziet, selecteert u deze optie.

  ![Dialoogvenster tekst van meer Services tooopen Klik in de Hub-menu en typt u virtuele machines](./media/backup-azure-vms-first-look-arm/open-vm-from-hub.png)

  Hallo-lijst van virtuele machines (VM) in het Hallo-abonnement wordt weergegeven.

  ![Hallo-lijst van virtuele machines in Hallo abonnement wordt weergegeven.](./media/backup-azure-vms-first-look-arm/list-of-vms.png)

3. Selecteer een VM-tooback uit Hallo-lijst.

  ![Hallo-lijst van virtuele machines in Hallo abonnement wordt weergegeven.](./media/backup-azure-vms-first-look-arm/list-of-vms-selected.png)

  Wanneer u Hallo VM selecteert, lijst met virtuele machines Hallo verschuift toohello links en Hallo virtuele machineblade management en Hallo virtuele machine dashboard, openen. </br>
 ![VM-beheerblade](./media/backup-azure-vms-first-look-arm/vm-management-blade.png)

4. Op Hallo VM management blade in Hallo **instellingen** sectie, klikt u op **back-up**. </br>

  ![Back-upoptie op VM-beheerblade](./media/backup-azure-vms-first-look-arm/backup-option-vm-management-blade.png)

  Hallo inschakelen back-blade wordt geopend.

  ![Back-upoptie op VM-beheerblade](./media/backup-azure-vms-first-look-arm/vm-blade-enable-backup.png)

5. Hallo Recovery Services-kluis, klikt u op **Selecteer een bestaande** en kies Hallo kluis in de vervolgkeuzelijst Hallo.

  ![Wizard Back-up inschakelen](./media/backup-azure-vms-first-look-arm/vm-blade-enable-backup.png)

  Als er geen Recovery Services-kluizen, of u een nieuwe kluis toouse wilt, klikt u op **nieuw** en geef de naam Hallo voor Hallo nieuwe kluis. Een nieuwe kluis is gemaakt in Hallo dezelfde resourcegroep en dezelfde locatie als Hallo virtuele machine. Als u een Recovery Services-kluis met verschillende waarden toocreate wilt, Raadpleeg Hallo sectie over het te[een recovery services-kluis maken](backup-azure-vms-first-look-arm.md#create-a-recovery-services-vault-for-a-vm).

6. tooview Hallo Hallo Backup-beleid, klikt u op **back-up maken van beleid**.

  Hallo **back-up maken van beleid** blade wordt geopend en Hallo details van Hallo geselecteerd beleid bevat. Als andere beleid bestaat, gebruikt u Hallo vervolgkeuzelijst toochoose een andere back-upbeleid. Als u wilt dat een beleid toocreate, selecteert u **nieuw** uit de vervolgkeuzelijst Hallo. Zie [Een back-upbeleid definiëren](backup-azure-vms-first-look-arm.md#defining-a-backup-policy) voor instructies over het definiëren van een back-upbeleid. toosave hello wijzigingen toohello back-upbeleid en back-blade return toohello inschakelen, klikt u op **OK**.

  ![Back-upbeleid selecteren](./media/backup-azure-vms-first-look-arm/setting-rs-backup-policy-new-2.png)

7. Klik op Hallo inschakelen back-blade **back-up inschakelen** toodeploy Hallo beleid. Hallo-beleid implementeren koppelt dit aan Hallo kluis en Hallo virtuele machines.

  ![Knop Backup inschakelen](./media/backup-azure-vms-first-look-arm/vm-management-blade-enable-backup-button.png)

8. Kunt u de voortgang van de configuratie door Hallo-meldingen die worden weergegeven in de portal Hallo Hallo bijhouden. Hallo volgende voorbeeld ziet u dat de implementatie is gestart.

  ![Back-upmeldingen inschakelen](./media/backup-azure-vms-first-look-arm/vm-management-blade-enable-backup-notification.png)

9. Zodra op Hallo VM management blade Hallo voortgang van de configuratie is voltooid, klikt u op **back-up** tooopen Hallo back-up Item blade en bekijkt hello details.

  ![Weergave Back-upitem VM](./media/backup-azure-vms-first-look-arm/backup-item-view.png)

  Totdat Hallo eerste back-up is voltooid, **laatste back-up maken van status** wordt weergegeven als **waarschuwing (eerste back-up in behandeling)**. toosee wanneer het volgende geplande back-uptaak Hallo optreedt, klikt u onder **back-up maken van beleid** klikt u op Hallo-naam van het Hallo-beleid. Hallo back-upbeleid blade wordt geopend en bevat de tijd Hallo Hallo geplande back-up.

10. een back-up toorun taak en Hallo initiële herstelpunt worden gemaakt, op Hallo Backup-kluis Klik op de blade **back-up nu**.

  ![Klik op de back-up nu toorun Hallo eerste back-up](./media/backup-azure-vms-first-look-arm/backup-now.png)

  back-up nu Hallo-blade wordt geopend.

  ![ziet u nu back-up Hallo-blade](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

11. Klik op Hallo nu back-up blade op Hallo kalenderpictogram, gebruikt u Hallo kalender besturingselement tooselect Hallo laatste dag van dit herstelpunt wordt bewaard, en klik op **back-up**.

  ![set Hallo laatste dag Hallo nu back-up een herstelpunt wordt bewaard](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  Meldingen van de implementatie kunnen u weten Hallo back-uptaak is geactiveerd en dat u kunt voortgang Hallo van Hallo-taak op de pagina Hallo back-up-taken.

## <a name="configure-hello-backup-job-from-hello-recovery-services-vault"></a>Back-uptaak van de Recovery Services-kluis Hallo Hallo configureren
back-uptaak tooconfigure hello, voltooit u Hallo stappen te volgen.  

1. Maak een Recovery Services-kluis voor een virtuele machine.
2. Gebruik hello Azure portal tooselect een Scenario met een back-up-beleid instellen en items tooprotect identificeren.
3. Hallo eerste back-up worden uitgevoerd.

## <a name="create-a-recovery-services-vault-for-a-vm"></a>Een Recovery Services-kluis voor een VM maken
Een Recovery Services-kluis is een entiteit waarmee alle Hallo back-ups en herstelpunten die zijn gemaakt na verloop van tijd worden opgeslagen. Hallo Recovery Services-kluis bevat ook de back-upbeleid Hallo toegepast toohello beveiligde virtuele machines.

> [!NOTE]
> Het maken van back-ups van VM's is een lokaal proces. Er kan geen virtuele machines Backup vanaf één locatie tooa Recovery Services-kluis in een andere locatie. Voor elke Azure-locatie met VM's toobe back-up gemaakt, moet ten minste één Recovery Services-kluis dus bestaan op die locatie.
>
>

toocreate een Recovery Services-kluis:

1. Als u dit nog niet hebt gedaan, meld u aan toohello [Azure-portal](https://portal.azure.com/) met behulp van uw Azure-abonnement.
2. Klik op het menu Hub Hallo **meer services** en in het dialoogvenster filtertype Hallo **Recovery Services**. Terwijl u typt, filtert Hallo lijst met resources. Wanneer u een Recovery Services-kluizen in Hallo lijst ziet, klikt u erop.

    ![Een Recovery Services-kluis maken, stap 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    Als er Recovery Services-kluizen in Hallo abonnement, worden Hallo kluizen weergegeven.

    ![Een Recovery Services-kluis maken, stap 2](./media/backup-azure-vms-first-look-arm/list-of-rs-vault.png)
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

  > [!IMPORTANT]
  > Als u niet Hallo-locatie waar uw VM zich bevindt weet, sluit buiten het dialoogvenster voor het Hallo-kluis maken en ga toohello lijst met virtuele Machines in Hallo-portal. Als u virtuele machines in meerdere regio's hebt, moet u in elke regio een Recovery Services-kluis maken. Hallo-kluis maken in de eerste locatie Hallo voordat u de volgende locatie toohello doorgaat. Er is dat geen opslagaccounts nodig toospecify Hallo gebruikt toostore Hallo back-upgegevens--Hallo Recovery Services-kluis en hello Azure Backup-service automatisch afhandelen Hallo-opslag.
  >

8. Aan de onderkant van de Hallo van blade Hallo Recovery Services-kluis, klikt u op **maken**.

    Het kan enkele minuten duren voordat Hallo die Recovery Services-kluis toobe gemaakt. Hallo statusmeldingen rechtsboven Hallo van Hallo portal bewaken. Zodra de kluis is gemaakt, wordt deze weergegeven in de lijst met Recovery Services-kluizen Hallo. Als u uw kluis na enkele minuten niet ziet, klik dan op **Vernieuwen**.

    ![Op de knop Vernieuwen klikken](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    Nadat u uw kluis in Hallo lijst met Recovery Services-kluizen ziet, bent u klaar tooset Hallo opslag redundantie.

Nu u uw kluis hebt gemaakt, kunt u nagaan hoe tooset Hallo storage-replicatie.

### <a name="set-storage-replication"></a>Opslagreplicatie instellen
optie voor opslagreplicatie Hallo kunt u toochoose tussen geografisch redundante opslag en lokaal redundante opslag. Uw kluis heeft standaard geografisch redundante opslag. Als uw primaire back-up is Hallo Recovery Services-kluis, laat u Hallo opslag replicatie optie set toogeo-redundante opslag. Kies lokaal redundante opslag als u een goedkopere optie wilt die minder duurzaam is. Lees meer over [geografisch redundante](../storage/common/storage-redundancy.md#geo-redundant-storage) en [lokaal redundante](../storage/common/storage-redundancy.md#locally-redundant-storage) opslagopties in Hallo [overzicht van Azure Storage-replicatie](../storage/common/storage-redundancy.md).

replicatie-instelling voor tooedit Hallo opslag

1. Van Hallo **Recovery Services-kluizen** blade, selecteer Hallo nieuwe kluis.

  ![Selecteer Hallo nieuwe kluis in Hallo-lijst met Recovery Services-kluis](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

  Wanneer u Hallo kluis selecteert, Hallo blade instellingen (*die Hallo kluisnaam heeft Hallo boven*) en Hallo details blade kluis openen.

  ![Het Hallo-opslagconfiguratie weergeven voor nieuwe kluis](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)

2. Op de blade instellingen Hallo nieuwe kluis, Hallo verticale dia tooscroll omlaag toohello sectie beheren en op **back-upinfrastructuur**.
    Hallo back-upinfrastructuur blade wordt geopend.
3. Klik op Hallo back-upinfrastructuur blade **back-upconfiguratie** tooopen hello **back-upconfiguratie** blade.

    ![De opslagconfiguratie Hallo voor nieuwe kluis instellen](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. Kies Hallo geschikte optie voor opslagreplicatie voor uw kluis.

    ![keuzes bij opslagconfiguratie](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    Uw kluis heeft standaard geografisch redundante opslag. Als u Azure als een eindpunt primaire back-upopslag gebruikt, gaat u verder toouse **geografisch redundante**. Als u geen Azure als een eindpunt primaire back-upopslag gebruikt, kiest u **lokaal redundante**, die zorgt voor lagere kosten voor hello Azure-opslag. U vindt meer informatie over de opties voor [geografisch redundante](../storage/common/storage-redundancy.md#geo-redundant-storage) en [lokaal redundante ](../storage/common/storage-redundancy.md#locally-redundant-storage) opslag in dit [overzicht van opslagredundantie](../storage/common/storage-redundancy.md).


## <a name="select-a-backup-goal-set-policy-and-define-items-tooprotect"></a>Selecteer een back-doel, beleid instellen en definiëren van items tooprotect
Voordat u een virtuele machine met een kluis registreert, Voer Hallo detectie proces tooensure dat nieuwe virtuele machines die zijn toegevoegd aan de toohello abonnement worden geïdentificeerd. Hallo wordt een query uitgevoerd Azure voor Hallo lijst met virtuele machines in het Hallo-abonnement, samen met aanvullende informatie zoals Hallo cloudservicenaam en Hallo regio. In hello Azure-portal verwijst scenario toowhat u tooput gaat in Hallo recovery services-kluis. Beleid is Hallo planning voor hoe vaak en wanneer de herstelpunten worden gemaakt. Het beleid bevat ook Hallo bewaartermijn voor Hallo herstelpunten.

1. Als u al een recovery services kluis openen, gaat u verder toostep 2. Klik anders op Hallo Hub-menu op **meer services** en typt u in de lijst met resources Hallo **Recovery Services** en klik op **Recovery Services-kluizen**.

    ![Een Recovery Services-kluis maken, stap 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    Hallo-lijst met recovery services-kluizen wordt weergegeven.

    ![Weergave van Hallo Recovery Services-kluizen lijst](./media/backup-azure-arm-vms-prepare/rs-list-of-vaults.png)

    Selecteer in Hallo lijst met recovery services-kluizen een kluis tooopen het dashboard.

     ![Blade Kluis openen](./media/backup-azure-arm-vms-prepare/new-vault-settings-blade.png)

2. Klik op het Hallo-kluis dashboard menu **back-up** blade tooopen Hallo-back-up.

    ![Blade Back-up openen](./media/backup-azure-arm-vms-prepare/backup-button.png)

    Hallo back-up- en back-updoel blades geopend.

    ![Blade Scenario openen](./media/backup-azure-arm-vms-prepare/select-backup-goal-1.png)
3. Op de blade back-updoel hello, van Hallo **waar wordt uw workload uitgevoerd** vervolgkeuzelijst, kiest u Azure. Van Hallo **wat wilt u wilt dat toobackup** vervolgkeuzelijst, kies de virtuele machine en klik vervolgens op **OK**.

    Deze acties registreren Hallo VM-extensie met Hallo kluis. Hallo back-updoel blade wordt gesloten en Hallo **back-up maken van beleid** blade wordt geopend.

    ![Blade Scenario openen](./media/backup-azure-arm-vms-prepare/select-backup-goal-2.png)

4. Selecteer op de blade van Hallo back-up Hallo back-upbeleid gewenste tooapply toohello kluis.

    ![Back-upbeleid selecteren](./media/backup-azure-arm-vms-prepare/setting-rs-backup-policy-new.png)

    Hallo-details van het standaardbeleid Hallo worden vermeld in de vervolgkeuzelijst Hallo. Als u wilt dat een beleid toocreate, selecteert u **nieuw** uit de vervolgkeuzelijst Hallo. Zie [Een back-upbeleid definiëren](backup-azure-vms-first-look-arm.md#defining-a-backup-policy) voor instructies over het definiëren van een back-upbeleid.
    Klik op **OK** tooassociate Hallo back-upbeleid met Hallo kluis.

    back-up beleid blade wordt gesloten en Hallo Hallo **virtuele machines selecteren** blade wordt geopend.
5. In Hallo **virtuele machines selecteren** blade kiezen Hallo virtuele machines tooassociate Hello opgegeven beleid en klik op **OK**.

    ![Workload selecteren](./media/backup-azure-arm-vms-prepare/select-vms-to-backup.png)

    Hallo geselecteerde virtuele machine wordt gevalideerd. Als er geen virtuele Hallo Hallo machines die u verwacht toosee, Controleer of deze bestaan in dezelfde Azure-locatie als Hallo Recovery Services-kluis. Hallo-locatie van Hallo die Recovery Services-kluis wordt weergegeven op het kluisdashboard Hallo.

6. Nu dat u alle instellingen voor Hallo-kluis hebt gedefinieerd in de blade back-up hello, klikt u op **back-up inschakelen** toodeploy Hallo beleid toohello kluis en Hallo van virtuele machines. Implementatie van de back-upbeleid Hallo maakt geen Hallo eerste herstelpunt voor Hallo virtuele machine.

    ![Back-up inschakelen](./media/backup-azure-arm-vms-prepare/vm-validated-click-enable.png)

Nadat de Hallo back-up is ingeschakeld, wordt uw back-upbeleid uitgevoerd volgens schema. Echter, gaat u verder tooinitiate Hallo eerste back-uptaak.

## <a name="initial-backup"></a>Eerste back-up
Wanneer een back-upbeleid op Hallo virtuele machine, die betekent niet dat is geïmplementeerd heeft Hallo gegevens zijn back-up. Hallo eerste geplande back-up is (zoals gedefinieerd in de back-upbeleid Hallo) standaard Hallo eerste back-up. Totdat de eerste back-up Hallo optreedt, Hallo Status van de laatste back-up op Hallo **back-uptaken** blade wordt weergegeven als **waarschuwing (eerste back-up in behandeling)**.

![Back-up in behandeling](./media/backup-azure-vms-first-look-arm/initial-backup-not-run.png)

Tenzij u uw eerste back-up toobegin binnenkort is het raadzaam dat u uitvoert **Back-up nu**.

toorun hello eerste back-uptaak:

1. Op het kluisdashboard hello, klikt u op Hallo onder **back-Upitems**, of klik op Hallo **back-Upitems** tegel. <br/>
  ![Pictogram Instellingen](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)

  Hallo **back-Upitems** blade wordt geopend.

  ![Back-upitems](./media/backup-azure-vms-first-look-arm/back-up-items-list.png)

2. Op Hallo **back-Upitems** blade, selecteer Hallo artikel.

  ![Het pictogram Instellingen](./media/backup-azure-vms-first-look-arm/back-up-items-list-selected.png)

  Hallo **back-Upitems** lijst wordt geopend. <br/>

  ![Geactiveerde back-uptaak](./media/backup-azure-vms-first-look-arm/backup-items-not-run.png)

3. Op Hallo **back-Upitems** lijst, klikt u op de weglatingstekens Hallo **...**  tooopen Hallo contextmenu.

  ![Contextmenu](./media/backup-azure-vms-first-look-arm/context-menu.png)

  Hallo contextmenu wordt weergegeven.

  ![Contextmenu](./media/backup-azure-vms-first-look-arm/context-menu-small.png)

4. Klik in het contextmenu hello, **back-up nu**.

  ![Contextmenu](./media/backup-azure-vms-first-look-arm/context-menu-small-backup-now.png)

  back-up nu Hallo-blade wordt geopend.

  ![ziet u nu back-up Hallo-blade](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

5. Klik op Hallo nu back-up blade op Hallo kalenderpictogram, gebruikt u Hallo kalender besturingselement tooselect Hallo laatste dag van dit herstelpunt wordt bewaard, en klik op **back-up**.

  ![set Hallo laatste dag Hallo nu back-up een herstelpunt wordt bewaard](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  Meldingen van de implementatie kunnen u weten Hallo back-uptaak is geactiveerd en dat u kunt voortgang Hallo van Hallo-taak op de pagina Hallo back-up-taken. Afhankelijk van de grootte van de Hallo van uw virtuele machine, kan Hallo eerste back-up maken duren.

6. tooview of bijhouden Hallo-status van Hallo eerste back-up, op Hallo kluisdashboard op Hallo **back-uptaken** Klik op de tegel **Bezig**.

  ![Tegel Back-uptaken](./media/backup-azure-vms-first-look-arm/open-backup-jobs-1.png)

  de blade back-uptaken Hello wordt geopend.

  ![Tegel Back-uptaken](./media/backup-azure-vms-first-look-arm/backup-jobs-in-jobs-view-1.png)

  In Hallo **back-uptaken** blade ziet u Hallo status van alle taken. Controleer als Hallo back-uptaak voor uw virtuele machine wordt nog uitgevoerd of als het is voltooid. Wanneer een back-uptaak is voltooid, is het Hallo-status *voltooid*.

  > [!NOTE]
  > Als onderdeel van de back-upbewerking Hallo verstrekt hello Azure Backup-service een toohello opdracht Backup-extensie in elke VM tooflush alle schrijft en een consistente momentopname.
  >
  >


[!INCLUDE [backup-create-backup-policy-for-vm](../../includes/backup-create-backup-policy-for-vm.md)]

## <a name="install-hello-vm-agent-on-hello-virtual-machine"></a>Hallo VM-Agent installeren op Hallo virtuele machine
Deze informatie wordt verstrekt voor het geval u deze nodig hebt. Hello Azure VM-Agent moet worden geïnstalleerd op Hallo voor Hallo back-up extensie toowork virtuele Azure-machine. Echter, als uw virtuele machine is gemaakt vanuit hello Azure-galerie, vervolgens Hallo VM-Agent is al aanwezig op Hallo virtuele machine. Virtuele machines die worden gemigreerd van lokale datacenters zou niet Hallo VM-Agent zijn geïnstalleerd. In dat geval moet Hallo VM-Agent toobe geïnstalleerd. Als u een back-up hello Azure VM problemen ondervindt, Controleer of de Azure VM-Agent Hallo juist is geïnstalleerd op Hallo virtuele machine (Zie de volgende tabel Hallo). Als u een aangepaste VM maakt [zorg Hallo **installeren Hallo VM-Agent** selectievakje is ingeschakeld](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) voordat Hallo virtuele machine is ingericht.

Meer informatie over Hallo [VM-Agent](https://go.microsoft.com/fwLink/?LinkID=390493&clcid=0x409) en [hoe tooinstall het](../virtual-machines/windows/classic/manage-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Hallo volgende tabel bevat aanvullende informatie over Hallo VM-Agent voor Windows en Linux-machines.

| **Bewerking** | **Windows** | **Linux** |
| --- | --- | --- |
| Hallo VM-Agent installeren |<li>Download en installeer Hallo [agent-MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). U moet Administrator-bevoegdheden toocomplete Hallo installatie. <li>[Werk Hallo VM eigenschap](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate die Hallo agent is geïnstalleerd. |<li> Meest recente Hallo installeren [Linux-agent](https://github.com/Azure/WALinuxAgent) vanuit GitHub. U moet Administrator-bevoegdheden toocomplete Hallo installatie. <li> [Werk Hallo VM eigenschap](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate die Hallo agent is geïnstalleerd. |
| Hallo VM-Agent bijwerken |Bijwerken Hallo VM-Agent is net zo eenvoudig als opnieuw geïnstalleerd Hallo [binaire bestanden voor VM-Agent](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). <br>Zorg ervoor dat er geen back-upbewerking wordt uitgevoerd terwijl Hallo VM-agent wordt bijgewerkt. |Volg de instructies Hallo op [Linux VM-Agent bijwerken Hallo](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). <br>Zorg ervoor dat er geen back-upbewerking wordt uitgevoerd tijdens het Hallo die VM-Agent wordt bijgewerkt. |
| Hallo VM-Agent-installatie valideren |<li>Navigeer toohello *C:\WindowsAzure\Packages* map in hello Azure VM. <li>U moet Hallo WaAppAgent.exe bestand aanwezig is.<li> Met de rechtermuisknop op het Hallo-bestand, gaat u te**eigenschappen**, en selecteer vervolgens Hallo **Details** tabblad Hallo productversie veld moet 2.6.1198.718 of hoger. |N.v.t. |

### <a name="backup-extension"></a>Backup-extensie
Hallo die VM-Agent is geïnstalleerd op Hallo virtuele machine, hello Azure Backup-service wordt eenmaal Hallo Backup-extensie toohello VM-Agent geïnstalleerd. upgrades naadloos Hello Azure Backup-service en -patches Hallo Backup-extensie zonder tussenkomst van de extra kosten voor gebruikers.

Hallo Backup-service installeert Hallo Backup-extensie, zelfs als Hallo VM wordt niet uitgevoerd. Een actieve virtuele machine biedt de grootste kans op Hallo van het ophalen van een toepassingsconsistente herstelpunt. Hello Azure Backup-service blijft echter tooback up Hallo VM, zelfs als deze is uitgeschakeld en Hallo-extensie kan niet worden geïnstalleerd. Dit type back-up wordt ook wel Offline-VM en Hallo herstelpunt is *crashconsistent*.

## <a name="troubleshooting-information"></a>Informatie over probleemoplossing
Als u problemen met het uitvoeren van taken in dit artikel Hallo hebt, raadpleegt u de [richtlijnen voor probleemoplossing](backup-azure-vms-troubleshoot.md).

## <a name="pricing"></a>Prijzen
Hallo kosten van het back-ups van Azure VM's is gebaseerd op Hallo aantal beveiligde exemplaren. Zie voor een definitie van een beveiligd exemplaar [Wat is een beveiligd exemplaar?](backup-introduction-to-azure-backup.md#what-is-a-protected-instance) Zie voor een voorbeeld van de berekening van Hallo kosten van het back-ups van een virtuele machine, [beveiligde instanties berekening](backup-azure-vms-introduction.md#calculating-the-cost-of-protected-instances). Zie Hallo prijzen van Azure-back-up pagina voor meer informatie over [back-up prijzen](https://azure.microsoft.com/pricing/details/backup/).

## <a name="questions"></a>Vragen?
Als u vragen hebt of als er een functie die u toosee opgenomen wilt, [Stuur ons feedback](http://aka.ms/azurebackup_feedback).
