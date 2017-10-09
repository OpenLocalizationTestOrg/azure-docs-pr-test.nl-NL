---
title: aaaRestore gegevens tooa Windows Server of Windows-Client van het gebruik van Azure Hallo klassieke implementatiemodel | Microsoft Docs
description: Meer informatie over hoe toorestore van een Windows Server of Windows-Client.
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 85585dfc-c764-4e8c-8f0e-40b969640ac2
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: 4d1458d5233c4f55004ecfa95cbf7b3b18a03dde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="restore-files-tooa-windows-server-or-windows-client-machine-using-hello-classic-deployment-model"></a><span data-ttu-id="2efc2-103">Herstellen van bestanden tooa WindowsServer of Windows client-computer met het klassieke implementatiemodel Hallo</span><span class="sxs-lookup"><span data-stu-id="2efc2-103">Restore files tooa Windows server or Windows client machine using hello classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2efc2-104">Klassieke portal</span><span class="sxs-lookup"><span data-stu-id="2efc2-104">Classic portal</span></span>](backup-azure-restore-windows-server-classic.md)
> * [<span data-ttu-id="2efc2-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="2efc2-105">Azure portal</span></span>](backup-azure-restore-windows-server.md)
>
>

<span data-ttu-id="2efc2-106">Dit artikel wordt uitgelegd hoe toorecover gegevens uit een back-up-kluis en herstel hem tooa server of computer.</span><span class="sxs-lookup"><span data-stu-id="2efc2-106">This article explains how toorecover data from a backup vault and restore it tooa server or computer.</span></span> <span data-ttu-id="2efc2-107">U start in maart 2017, kunt u niet langer maken back-upkluizen in de klassieke portal Hallo.</span><span class="sxs-lookup"><span data-stu-id="2efc2-107">Starting in March 2017, you can no longer create backup vaults in hello classic portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2efc2-108">U kunt nu uw back-up kluizen tooRecovery Services-kluizen upgraden.</span><span class="sxs-lookup"><span data-stu-id="2efc2-108">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="2efc2-109">Zie voor meer informatie artikel Hallo [upgraden van een back-up kluis tooa Recovery Services-kluis](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="2efc2-109">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="2efc2-110">Microsoft raadt u tooupgrade uw back-upkluizen tooRecovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="2efc2-110">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="2efc2-111">**15 oktober 2017**, u niet langer kunnen toouse PowerShell toocreate Backup-kluizen.</span><span class="sxs-lookup"><span data-stu-id="2efc2-111">**October 15, 2017**, you will no longer be able toouse PowerShell toocreate Backup vaults.</span></span> <br/> <span data-ttu-id="2efc2-112">**Vanaf 1 november 2017**:</span><span class="sxs-lookup"><span data-stu-id="2efc2-112">**Starting November 1, 2017**:</span></span>
>- <span data-ttu-id="2efc2-113">Alle resterende Backup-kluizen worden automatisch bijgewerkt tooRecovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="2efc2-113">Any remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="2efc2-114">U niet kunt tooaccess uw back-upgegevens in de klassieke portal Hallo.</span><span class="sxs-lookup"><span data-stu-id="2efc2-114">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="2efc2-115">In plaats daarvan gebruik hello Azure portal tooaccess uw back-upgegevens in Recovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="2efc2-115">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

<span data-ttu-id="2efc2-116">toorestore gegevens, gebruikt u Hallo gegevens herstellen wizard in Hallo Microsoft Azure Recovery Services (MARS)-agent.</span><span class="sxs-lookup"><span data-stu-id="2efc2-116">toorestore data, you use hello Recover Data wizard in hello Microsoft Azure Recovery Services (MARS) agent.</span></span> <span data-ttu-id="2efc2-117">Wanneer u gegevens herstelt, is het mogelijk om te:</span><span class="sxs-lookup"><span data-stu-id="2efc2-117">When you restore data, it is possible to:</span></span>

* <span data-ttu-id="2efc2-118">Terugzetten van gegevens toohello dezelfde machine uit welke Hallo back-ups zijn uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2efc2-118">Restore data toohello same machine from which hello backups were taken.</span></span>
* <span data-ttu-id="2efc2-119">Gegevens tooan alternatieve machine herstellen.</span><span class="sxs-lookup"><span data-stu-id="2efc2-119">Restore data tooan alternate machine.</span></span>

<span data-ttu-id="2efc2-120">Microsoft uitgebracht in januari 2017 een Preview update toohello MARS-agent.</span><span class="sxs-lookup"><span data-stu-id="2efc2-120">In January 2017, Microsoft released a Preview update toohello MARS agent.</span></span> <span data-ttu-id="2efc2-121">Samen met oplossingen voor problemen, deze update kan direct herstellen, zodat u toomount een momentopname van een beschrijfbare herstelpunt als een volume herstel.</span><span class="sxs-lookup"><span data-stu-id="2efc2-121">Along with bug fixes, this update enables Instant Restore, which allows you toomount a writeable recovery point snapshot as a recovery volume.</span></span> <span data-ttu-id="2efc2-122">U kunt vervolgens Hallo herstel volume en kopieert u bestanden tooa lokale computer waardoor selectief terugzetten bestanden verkennen.</span><span class="sxs-lookup"><span data-stu-id="2efc2-122">You can then explore hello recovery volume and copy files tooa local computer thereby selectively restoring files.</span></span>

> [!NOTE]
> <span data-ttu-id="2efc2-123">Hallo [januari 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) is vereist als u gegevens van toouse toorestore direct herstellen.</span><span class="sxs-lookup"><span data-stu-id="2efc2-123">hello [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) is required if you want toouse Instant Restore toorestore data.</span></span> <span data-ttu-id="2efc2-124">Back-upgegevens Hallo moeten ook worden beveiligd in kluizen in de landinstellingen die worden vermeld in artikel Hallo-ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="2efc2-124">Also hello backup data must be protected in vaults in locales listed in hello support article.</span></span> <span data-ttu-id="2efc2-125">Raadpleeg Hallo [januari 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) voor de meest recente lijst Hallo van landinstellingen die ondersteuning bieden voor chatberichten te herstellen.</span><span class="sxs-lookup"><span data-stu-id="2efc2-125">Consult hello [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) for hello latest list of locales that support Instant Restore.</span></span> <span data-ttu-id="2efc2-126">Direct herstellen is **niet** momenteel in alle landen beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="2efc2-126">Instant Restore is **not** currently available in all locales.</span></span>
>

<span data-ttu-id="2efc2-127">Chatberichten terugzetten is beschikbaar voor gebruik in de Recovery Services-kluizen in hello Azure-portal en Backup-kluizen in de klassieke portal Hallo.</span><span class="sxs-lookup"><span data-stu-id="2efc2-127">Instant Restore is available for use in Recovery Services vaults in hello Azure portal and Backup vaults in hello classic portal.</span></span> <span data-ttu-id="2efc2-128">Als u toouse direct herstellen wilt, Hallo MARS update downloaden en Hallo procedures volgen die vermeld direct herstellen.</span><span class="sxs-lookup"><span data-stu-id="2efc2-128">If you want toouse Instant Restore, download hello MARS update, and follow hello procedures that mention Instant Restore.</span></span>


## <a name="use-instant-restore-toorecover-data-toohello-same-machine"></a><span data-ttu-id="2efc2-129">Direct herstellen toorecover gegevens toohello gebruiken dezelfde machine</span><span class="sxs-lookup"><span data-stu-id="2efc2-129">Use Instant Restore toorecover data toohello same machine</span></span>

<span data-ttu-id="2efc2-130">Als u een bestands- en desgewenst toorestore per ongeluk hebt verwijderd deze toohello dezelfde machine (vanaf welke Hallo back-up is gemaakt), Hallo te volgen stappen vindt u een Hallo-gegevens herstellen.</span><span class="sxs-lookup"><span data-stu-id="2efc2-130">If you accidentally deleted a file and wish toorestore it toohello same machine (from which hello backup is taken), hello following steps will help you recover hello data.</span></span>

1. <span data-ttu-id="2efc2-131">Open Hallo **Microsoft Azure Backup** uitlijnen in.</span><span class="sxs-lookup"><span data-stu-id="2efc2-131">Open hello **Microsoft Azure Backup** snap in.</span></span> <span data-ttu-id="2efc2-132">Als u niet waar Hallo-module is geïnstalleerd weet, zoekt u Hallo computer of server voor **Microsoft Azure Backup**.</span><span class="sxs-lookup"><span data-stu-id="2efc2-132">If you don't know where hello snap in was installed, search hello computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="2efc2-133">Hallo bureaublad-app moet worden weergegeven in zoekresultaten Hallo.</span><span class="sxs-lookup"><span data-stu-id="2efc2-133">hello desktop app should appear in hello search results.</span></span>

2. <span data-ttu-id="2efc2-134">Klik op **gegevens herstellen** toostart Hallo-wizard.</span><span class="sxs-lookup"><span data-stu-id="2efc2-134">Click **Recover Data** toostart hello wizard.</span></span>

    ![Gegevens herstellen](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="2efc2-136">Op Hallo **aan de slag** deelvenster, toorestore Hallo gegevens toohello dezelfde server of computer, selecteer **deze server (`<server name>`)** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="2efc2-136">On hello **Getting Started** pane, toorestore hello data toohello same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![Kies deze server optie toorestore Hallo gegevens toohello dezelfde machine](./media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. <span data-ttu-id="2efc2-138">Op Hallo **herstelmodus Selecteer** deelvenster kiezen **afzonderlijke bestanden en mappen** en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="2efc2-138">On hello **Select Recovery Mode** pane, choose **Individual files and folders** and then click **Next**.</span></span>

    ![Blader door bestanden](./media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. <span data-ttu-id="2efc2-140">Op Hallo **Volume selecteert en datum** deelvenster, selecteer Hallo-volume dat Hallo bestanden en/of mappen die u wilt dat toorestore bevat.</span><span class="sxs-lookup"><span data-stu-id="2efc2-140">On hello **Select Volume and Date** pane, select hello volume that contains hello files and/or folders you want toorestore.</span></span>

    <span data-ttu-id="2efc2-141">Selecteer een herstelpunt op Hallo-kalender.</span><span class="sxs-lookup"><span data-stu-id="2efc2-141">On hello calendar, select a recovery point.</span></span> <span data-ttu-id="2efc2-142">U kunt vanaf elk willekeurig herstelpunt herstellen in de tijd.</span><span class="sxs-lookup"><span data-stu-id="2efc2-142">You can restore from any recovery point in time.</span></span> <span data-ttu-id="2efc2-143">Datums **vet** Hallo beschikbaarheid van ten minste één herstelpunt aangeven.</span><span class="sxs-lookup"><span data-stu-id="2efc2-143">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="2efc2-144">Wanneer u een datum selecteren als er meerdere herstelpunten beschikbaar zijn, kiest u Hallo specifiek herstelpunt van Hallo **tijd** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="2efc2-144">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![Volume en datum](./media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. <span data-ttu-id="2efc2-146">Nadat u Hallo herstel punt toorestore hebt gekozen, klikt u op **koppelen**.</span><span class="sxs-lookup"><span data-stu-id="2efc2-146">Once you have chosen hello recovery point toorestore, click **Mount**.</span></span>

    <span data-ttu-id="2efc2-147">Azure Backup Hallo lokale herstelpunt koppelt en gebruikt als een volume herstel.</span><span class="sxs-lookup"><span data-stu-id="2efc2-147">Azure Backup mounts hello local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="2efc2-148">Op Hallo **bladeren en bestanden herstellen** deelvenster, klikt u op **Bladeren** tooopen Windows Verkenner en zoek Hallo bestanden en mappen die u wilt.</span><span class="sxs-lookup"><span data-stu-id="2efc2-148">On hello **Browse and Recover Files** pane, click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span>

    ![Opties voor herstel](./media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. <span data-ttu-id="2efc2-150">In Windows Verkenner, Hallo-bestanden kopiëren en/of mappen wilt toorestore en plak ze tooany locatie toohello lokale server of computer.</span><span class="sxs-lookup"><span data-stu-id="2efc2-150">In Windows Explorer, copy hello files and/or folders you want toorestore and paste them tooany location local toohello server or computer.</span></span> <span data-ttu-id="2efc2-151">U kunt openen of stream Hallo-bestanden rechtstreeks vanuit Hallo herstel volume en controleer of Hallo juist versies zijn hersteld.</span><span class="sxs-lookup"><span data-stu-id="2efc2-151">You can open or stream hello files directly from hello recovery volume and verify hello correct versions are recovered.</span></span>

    ![Kopiëren en plakken van bestanden en mappen van gekoppelde volume toolocal locatie](./media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. <span data-ttu-id="2efc2-153">Als u klaar bent herstellen Hallo bestanden en/of mappen op Hallo **bladeren en herstelbestanden** deelvenster, klikt u op **ontkoppelen**.</span><span class="sxs-lookup"><span data-stu-id="2efc2-153">When you are finished restoring hello files and/or folders, on hello **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="2efc2-154">Klik vervolgens op **Ja** tooconfirm dat u wilt dat toounmount Hallo volume.</span><span class="sxs-lookup"><span data-stu-id="2efc2-154">Then click **Yes** tooconfirm that you want toounmount hello volume.</span></span>

    ![Hallo volume ontkoppelen en bevestigen](./media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="2efc2-156">Als u niet ontkoppelen op, blijft Hallo herstel Volume gekoppelde gedurende zes uur van Hallo tijd wanneer deze is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="2efc2-156">If you do not click Unmount, hello Recovery Volume will remain mounted for six hours from hello time when it was mounted.</span></span> <span data-ttu-id="2efc2-157">Er is geen back-upbewerkingen wordt uitgevoerd tijdens het Hallo-volume is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="2efc2-157">No backup operations will run while hello volume is mounted.</span></span> <span data-ttu-id="2efc2-158">Een back-upbewerking gepland toorun tijdens Hallo wanneer Hallo volume is gekoppeld, wordt uitgevoerd nadat Hallo herstel volume is ontkoppeld.</span><span class="sxs-lookup"><span data-stu-id="2efc2-158">Any backup operation scheduled toorun during hello time when hello volume is mounted, will run after hello recovery volume is unmounted.</span></span>
    >


## <a name="recover-data-toohello-same-machine"></a><span data-ttu-id="2efc2-159">Herstellen van gegevens toohello dezelfde machine</span><span class="sxs-lookup"><span data-stu-id="2efc2-159">Recover data toohello same machine</span></span>
<span data-ttu-id="2efc2-160">Als u een bestands- en desgewenst toorestore per ongeluk hebt verwijderd deze toohello dezelfde machine (vanaf welke Hallo back-up is gemaakt), Hallo te volgen stappen vindt u een Hallo-gegevens herstellen.</span><span class="sxs-lookup"><span data-stu-id="2efc2-160">If you accidentally deleted a file and wish toorestore it toohello same machine (from which hello backup is taken), hello following steps will help you recover hello data.</span></span>

1. <span data-ttu-id="2efc2-161">Open Hallo **Microsoft Azure Backup** uitlijnen in.</span><span class="sxs-lookup"><span data-stu-id="2efc2-161">Open hello **Microsoft Azure Backup** snap in.</span></span>
2. <span data-ttu-id="2efc2-162">Klik op **gegevens herstellen** tooinitiate Hallo werkstroom.</span><span class="sxs-lookup"><span data-stu-id="2efc2-162">Click **Recover Data** tooinitiate hello workflow.</span></span>

    ![Gegevens herstellen](./media/backup-azure-restore-windows-server-classic/recover.png)
3. <span data-ttu-id="2efc2-164">Selecteer Hallo  **deze server (*yourmachinename*) ** optie toorestore Hallo een back-up-bestand op Hallo dezelfde machine.</span><span class="sxs-lookup"><span data-stu-id="2efc2-164">Select hello **This server (*yourmachinename*)** option toorestore hello backed up file on hello same machine.</span></span>

    ![Dezelfde machine](./media/backup-azure-restore-windows-server-classic/samemachine.png)
4. <span data-ttu-id="2efc2-166">Kies te**zoeken naar bestanden** of **zoeken naar bestanden**.</span><span class="sxs-lookup"><span data-stu-id="2efc2-166">Choose too**Browse for files** or **Search for files**.</span></span>

    <span data-ttu-id="2efc2-167">Laat Hallo standaardoptie als u van plan toorestore bent een of meer bestanden waarvan het pad is bekend.</span><span class="sxs-lookup"><span data-stu-id="2efc2-167">Leave hello default option if you plan toorestore one or more files whose path is known.</span></span> <span data-ttu-id="2efc2-168">Als u niet zeker van de mapstructuur Hallo bent maar toosearch voor een bestand, kies Hallo **zoeken naar bestanden** optie.</span><span class="sxs-lookup"><span data-stu-id="2efc2-168">If you are not sure about hello folder structure but would like toosearch for a file, pick hello **Search for files** option.</span></span> <span data-ttu-id="2efc2-169">Voor Hallo doel van deze sectie gaat we nu verder met de standaardoptie Hallo.</span><span class="sxs-lookup"><span data-stu-id="2efc2-169">For hello purpose of this section, we will proceed with hello default option.</span></span>

    ![Blader door bestanden](./media/backup-azure-restore-windows-server-classic/browseandsearch.png)
5. <span data-ttu-id="2efc2-171">Selecteer Hallo volume van waaruit u wilt dat toorestore Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="2efc2-171">Select hello volume from which you wish toorestore hello file.</span></span>

    <span data-ttu-id="2efc2-172">U kunt herstellen vanaf elk punt in tijd.</span><span class="sxs-lookup"><span data-stu-id="2efc2-172">You can restore from any point in time.</span></span> <span data-ttu-id="2efc2-173">Datums die worden weergegeven in **vet** Hallo kalenderbesturingselement duiden op Hallo beschikbaarheid van een herstelpunt.</span><span class="sxs-lookup"><span data-stu-id="2efc2-173">Dates which appear in **bold** in hello calendar control indicate hello availability of a restore point.</span></span> <span data-ttu-id="2efc2-174">Nadat een datum is geselecteerd, op basis van uw back-upschema (en het Hallo slagen van een back-upbewerking), kunt u een punt in tijd van Hallo **tijd** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="2efc2-174">Once a date is selected, based on your backup schedule (and hello success of a backup operation), you can select a point in time from hello **Time** drop down.</span></span>

    ![Volume en datum](./media/backup-azure-restore-windows-server-classic/volanddate.png)
6. <span data-ttu-id="2efc2-176">Selecteer Hallo items toorecover.</span><span class="sxs-lookup"><span data-stu-id="2efc2-176">Select hello items toorecover.</span></span> <span data-ttu-id="2efc2-177">U kunt meerdere mappen/bestanden desgewenst toorestore.</span><span class="sxs-lookup"><span data-stu-id="2efc2-177">You can multi-select folders/files you wish toorestore.</span></span>

    ![Bestanden selecteren](./media/backup-azure-restore-windows-server-classic/selectfiles.png)
7. <span data-ttu-id="2efc2-179">Geef parameters op Hallo herstel.</span><span class="sxs-lookup"><span data-stu-id="2efc2-179">Specify hello recovery parameters.</span></span>

    ![Opties voor herstel](./media/backup-azure-restore-windows-server-classic/recoveroptions.png)

   * <span data-ttu-id="2efc2-181">Hebt u een optie van het terugzetten van de oorspronkelijke locatie toohello (in welke Hallo bestand/map zou worden overschreven) of tooanother locatie in Hallo dezelfde machine.</span><span class="sxs-lookup"><span data-stu-id="2efc2-181">You have an option of restoring toohello original location (in which hello file/folder would be overwritten) or tooanother location in hello same machine.</span></span>
   * <span data-ttu-id="2efc2-182">Als Hallo bestand/map gewenst toorestore bestaat in de doellocatie hello, kunt u kopieën (twee versies van Hallo hetzelfde bestand), Hallo-bestanden in de doellocatie Hallo overschrijven, of het Hallo-herstel van Hallo-bestanden die aanwezig zijn in Hallo doel overslaan.</span><span class="sxs-lookup"><span data-stu-id="2efc2-182">If hello file/folder you wish toorestore exists in hello target location, you can create copies (two versions of hello same file), overwrite hello files in hello target location, or skip hello recovery of hello files which exist in hello target.</span></span>
   * <span data-ttu-id="2efc2-183">Het is raadzaam dat u de standaardoptie Hallo Hallo ACL's op Hallo-bestanden die zijn hersteld terugzetten van laat.</span><span class="sxs-lookup"><span data-stu-id="2efc2-183">It is highly recommended that you leave hello default option of restoring hello ACLs on hello files which are being recovered.</span></span>
8. <span data-ttu-id="2efc2-184">Zodra deze invoer zijn opgegeven, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="2efc2-184">Once these inputs are provided, click **Next**.</span></span> <span data-ttu-id="2efc2-185">Hallo herstelwerkstroom, die Hallo bestanden toothis machine herstelt, wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="2efc2-185">hello recovery workflow, which restores hello files toothis machine, will begin.</span></span>

## <a name="recover-tooan-alternate-machine"></a><span data-ttu-id="2efc2-186">Alternatieve tooan-machine herstellen</span><span class="sxs-lookup"><span data-stu-id="2efc2-186">Recover tooan alternate machine</span></span>
<span data-ttu-id="2efc2-187">Als uw hele server verbroken wordt, kunt u nog steeds gegevens herstellen vanaf de Azure Backup tooa andere machine.</span><span class="sxs-lookup"><span data-stu-id="2efc2-187">If your entire server is lost, you can still recover data from Azure Backup tooa different machine.</span></span> <span data-ttu-id="2efc2-188">Hallo stappen te volgen illustreren Hallo-werkstroom.</span><span class="sxs-lookup"><span data-stu-id="2efc2-188">hello following steps illustrate hello workflow.</span></span>  

<span data-ttu-id="2efc2-189">Hallo-terminologie die wordt gebruikt in deze stap omvat het volgende:</span><span class="sxs-lookup"><span data-stu-id="2efc2-189">hello terminology used in these steps includes:</span></span>

* <span data-ttu-id="2efc2-190">*Bronmachine* : de oorspronkelijke machine Hallo van welke Hallo back-up is gemaakt en die momenteel niet beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="2efc2-190">*Source machine* – hello original machine from which hello backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="2efc2-191">*Doelcomputer* – Hallo machine toowhich Hallo gegevens worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="2efc2-191">*Target machine* – hello machine toowhich hello data is being recovered.</span></span>
* <span data-ttu-id="2efc2-192">*Voorbeeld kluis* – Hallo Backup-kluis toowhich hello *bronmachine* en *doelmachine* zijn geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="2efc2-192">*Sample vault* – hello Backup vault toowhich hello *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="2efc2-193">Back-ups die van een virtuele machine kunnen niet worden teruggezet op een computer waarop een eerdere versie van het Hallo-besturingssysteem wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2efc2-193">Backups taken from a machine cannot be restored on a machine which is running an earlier version of hello operating system.</span></span> <span data-ttu-id="2efc2-194">Bijvoorbeeld, als back-ups worden gemaakt van een machine met Windows 7, kan deze worden hersteld op een Windows 8 of hoger machine.</span><span class="sxs-lookup"><span data-stu-id="2efc2-194">For example, if backups are taken from a Windows 7 machine, it can be restored on a Windows 8 or above machine.</span></span> <span data-ttu-id="2efc2-195">Hallo vice versa biedt echter geen houdt true.</span><span class="sxs-lookup"><span data-stu-id="2efc2-195">However, hello vice-versa does not hold true.</span></span>
>
>

1. <span data-ttu-id="2efc2-196">Open Hallo **Microsoft Azure Backup** uitlijnen in op Hallo *doelmachine*.</span><span class="sxs-lookup"><span data-stu-id="2efc2-196">Open hello **Microsoft Azure Backup** snap in on hello *Target machine*.</span></span>
2. <span data-ttu-id="2efc2-197">Zorg ervoor dat Hallo *doelmachine* en Hallo *bronmachine* geregistreerde toohello zijn dezelfde back-upkluis.</span><span class="sxs-lookup"><span data-stu-id="2efc2-197">Ensure that hello *Target machine* and hello *Source machine* are registered toohello same backup vault.</span></span>
3. <span data-ttu-id="2efc2-198">Klik op **gegevens herstellen** tooinitiate Hallo werkstroom.</span><span class="sxs-lookup"><span data-stu-id="2efc2-198">Click **Recover Data** tooinitiate hello workflow.</span></span>

    ![Gegevens herstellen](./media/backup-azure-restore-windows-server-classic/recover.png)
4. <span data-ttu-id="2efc2-200">Selecteer **een andere server**</span><span class="sxs-lookup"><span data-stu-id="2efc2-200">Select **Another server**</span></span>

    ![Een andere Server](./media/backup-azure-restore-windows-server-classic/anotherserver.png)
5. <span data-ttu-id="2efc2-202">Hallo-kluisreferentiebestand die overeenkomt met toohello bieden *voorbeeld kluis*.</span><span class="sxs-lookup"><span data-stu-id="2efc2-202">Provide hello vault credential file that corresponds toohello *Sample vault*.</span></span> <span data-ttu-id="2efc2-203">Als het kluisreferentiebestand Hallo is ongeldig (of verlopen) het downloaden van een nieuw kluisreferentiebestand van Hallo *voorbeeld kluis* in Hallo klassieke Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="2efc2-203">If hello vault credential file is invalid (or expired) download a new vault credential file from hello *Sample vault* in hello Azure classic portal.</span></span> <span data-ttu-id="2efc2-204">Zodra het Hallo-kluisreferentiebestand is opgegeven, wordt back-upkluis tegen kluisreferentiebestand Hallo Hallo weergegeven.</span><span class="sxs-lookup"><span data-stu-id="2efc2-204">Once hello vault credential file is provided, hello backup vault against hello vault credential file is displayed.</span></span>
6. <span data-ttu-id="2efc2-205">Selecteer Hallo *bronmachine* uit Hallo lijst met computers weergegeven.</span><span class="sxs-lookup"><span data-stu-id="2efc2-205">Select hello *Source machine* from hello list of displayed machines.</span></span>

    ![Lijst met computers](./media/backup-azure-restore-windows-server-classic/machinelist.png)
7. <span data-ttu-id="2efc2-207">Selecteer beide Hallo **zoeken naar bestanden** of **zoeken naar bestanden** optie.</span><span class="sxs-lookup"><span data-stu-id="2efc2-207">Select either hello **Search for files** or **Browse for files** option.</span></span> <span data-ttu-id="2efc2-208">Voor Hallo doel van deze sectie, gebruiken we Hallo **zoeken naar bestanden** optie.</span><span class="sxs-lookup"><span data-stu-id="2efc2-208">For hello purpose of this section, we will use hello **Search for files** option.</span></span>

    ![Search](./media/backup-azure-restore-windows-server-classic/search.png)
8. <span data-ttu-id="2efc2-210">Selecteer Hallo volume en datum in het volgende scherm Hallo.</span><span class="sxs-lookup"><span data-stu-id="2efc2-210">Select hello volume and date in hello next screen.</span></span> <span data-ttu-id="2efc2-211">Zoekactie voor de naam van de map/bestand Hallo gewenste toorestore.</span><span class="sxs-lookup"><span data-stu-id="2efc2-211">Search for hello folder/file name you want toorestore.</span></span>

    ![Zoeken naar objecten](./media/backup-azure-restore-windows-server-classic/searchitems.png)
9. <span data-ttu-id="2efc2-213">Selecteer Hallo-locatie waar Hallo-bestanden toobe hersteld moeten.</span><span class="sxs-lookup"><span data-stu-id="2efc2-213">Select hello location where hello files need toobe restored.</span></span>

    ![Locatie herstellen](./media/backup-azure-restore-windows-server-classic/restorelocation.png)
10. <span data-ttu-id="2efc2-215">Hallo-wachtwoordzin voor versleuteling dat is opgegeven tijdens de bieden *van de bronmachine* registratie te*voorbeeld kluis*.</span><span class="sxs-lookup"><span data-stu-id="2efc2-215">Provide hello encryption passphrase that was provided during *Source machine’s* registration too*Sample vault*.</span></span>

    ![Versleuteling](./media/backup-azure-restore-windows-server-classic/encryption.png)
11. <span data-ttu-id="2efc2-217">Zodra het Hallo-invoer is opgegeven, klikt u op **herstellen**, welke triggers Hallo terugzetten van een back-up bestanden toohello bestemming Hallo.</span><span class="sxs-lookup"><span data-stu-id="2efc2-217">Once hello input is provided, click **Recover**, which triggers hello restore of hello backed up files toohello destination provided.</span></span>

## <a name="use-instant-restore-toorestore-data-tooan-alternate-machine"></a><span data-ttu-id="2efc2-218">Direct herstellen toorestore gegevens tooan alternatieve machine gebruiken</span><span class="sxs-lookup"><span data-stu-id="2efc2-218">Use Instant Restore toorestore data tooan alternate machine</span></span>
<span data-ttu-id="2efc2-219">Als uw hele server verbroken wordt, kunt u nog steeds gegevens herstellen vanaf de Azure Backup tooa andere machine.</span><span class="sxs-lookup"><span data-stu-id="2efc2-219">If your entire server is lost, you can still recover data from Azure Backup tooa different machine.</span></span> <span data-ttu-id="2efc2-220">Hallo stappen te volgen illustreren Hallo-werkstroom.</span><span class="sxs-lookup"><span data-stu-id="2efc2-220">hello following steps illustrate hello workflow.</span></span>

<span data-ttu-id="2efc2-221">Hallo-terminologie die wordt gebruikt in deze stap omvat het volgende:</span><span class="sxs-lookup"><span data-stu-id="2efc2-221">hello terminology used in these steps includes:</span></span>

* <span data-ttu-id="2efc2-222">*Bronmachine* : de oorspronkelijke machine Hallo van welke Hallo back-up is gemaakt en die momenteel niet beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="2efc2-222">*Source machine* – hello original machine from which hello backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="2efc2-223">*Doelcomputer* – Hallo machine toowhich Hallo gegevens worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="2efc2-223">*Target machine* – hello machine toowhich hello data is being recovered.</span></span>
* <span data-ttu-id="2efc2-224">*Voorbeeld kluis* – Hallo Recovery Services-kluis toowhich hello *bronmachine* en *doelmachine* zijn geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="2efc2-224">*Sample vault* – hello Recovery Services vault toowhich hello *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="2efc2-225">Back-ups niet herstelde tooa doelcomputer met een eerdere versie van besturingssysteem Hallo.</span><span class="sxs-lookup"><span data-stu-id="2efc2-225">Backups can't be restored tooa target machine running an earlier version of hello operating system.</span></span> <span data-ttu-id="2efc2-226">Bijvoorbeeld, een back-up van een Windows 7 computer kan worden hersteld op een Windows 8 of hoger, computer.</span><span class="sxs-lookup"><span data-stu-id="2efc2-226">For example, a backup taken from a Windows 7 computer can be restored on a Windows 8, or later, computer.</span></span> <span data-ttu-id="2efc2-227">Een back-up van een Windows 8-computer niet tooa Windows 7 van de herstelde computer.</span><span class="sxs-lookup"><span data-stu-id="2efc2-227">A backup taken from a Windows 8 computer cannot be restored tooa Windows 7 computer.</span></span>
>
>

1. <span data-ttu-id="2efc2-228">Open Hallo **Microsoft Azure Backup** uitlijnen in op Hallo *doelmachine*.</span><span class="sxs-lookup"><span data-stu-id="2efc2-228">Open hello **Microsoft Azure Backup** snap in on hello *Target machine*.</span></span>

2. <span data-ttu-id="2efc2-229">Zorg ervoor dat Hallo *doelmachine* en Hallo *bronmachine* zijn geregistreerde toohello dezelfde Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="2efc2-229">Ensure hello *Target machine* and hello *Source machine* are registered toohello same Recovery Services vault.</span></span>

3. <span data-ttu-id="2efc2-230">Klik op **gegevens herstellen** tooopen hello **wizard gegevens herstellen**.</span><span class="sxs-lookup"><span data-stu-id="2efc2-230">Click **Recover Data** tooopen hello **Recover Data wizard**.</span></span>

    ![Gegevens herstellen](./media/backup-azure-restore-windows-server/recover.png)

4. <span data-ttu-id="2efc2-232">Op Hallo **aan de slag** deelvenster **een andere server**</span><span class="sxs-lookup"><span data-stu-id="2efc2-232">On hello **Getting Started** pane, select **Another server**</span></span>

    ![Een andere Server](./media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. <span data-ttu-id="2efc2-234">Hallo-kluisreferentiebestand die overeenkomt met toohello bieden *voorbeeld kluis*, en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="2efc2-234">Provide hello vault credential file that corresponds toohello *Sample vault*, and click **Next**.</span></span>

    <span data-ttu-id="2efc2-235">Als het kluisreferentiebestand Hallo is ongeldig (of verlopen), het downloaden van een nieuw kluisreferentiebestand van Hallo *voorbeeld kluis* in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="2efc2-235">If hello vault credential file is invalid (or expired), download a new vault credential file from hello *Sample vault* in hello Azure portal.</span></span> <span data-ttu-id="2efc2-236">Zodra u de referenties van een geldige kluis opgeeft, wordt de naam Hallo Hallo Backup-kluis overeenkomt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="2efc2-236">Once you provide a valid vault credential, hello name of hello corresponding Backup Vault appears.</span></span>

6. <span data-ttu-id="2efc2-237">Op Hallo **back-up-Server selecteren** deelvenster, selecteer Hallo *bronmachine* uit Hallo lijst met weergegeven machines en Hallo wachtwoordzin opgeven.</span><span class="sxs-lookup"><span data-stu-id="2efc2-237">On hello **Select Backup Server** pane, select hello *Source machine* from hello list of displayed machines and provide hello passphrase.</span></span> <span data-ttu-id="2efc2-238">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="2efc2-238">Then click **Next**.</span></span>

    ![Lijst met computers](./media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. <span data-ttu-id="2efc2-240">Op Hallo **herstelmodus Selecteer** deelvenster Selecteer **afzonderlijke bestanden en mappen** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="2efc2-240">On hello **Select Recovery Mode** pane, select **Individual files and folders** and click **Next**.</span></span>

    ![Search](./media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. <span data-ttu-id="2efc2-242">Op Hallo **Volume selecteert en datum** deelvenster, selecteer Hallo-volume dat Hallo bestanden en/of mappen die u wilt dat toorestore bevat.</span><span class="sxs-lookup"><span data-stu-id="2efc2-242">On hello **Select Volume and Date** pane, select hello volume that contains hello files and/or folders you want toorestore.</span></span>

    <span data-ttu-id="2efc2-243">Selecteer een herstelpunt op Hallo-kalender.</span><span class="sxs-lookup"><span data-stu-id="2efc2-243">On hello calendar, select a recovery point.</span></span> <span data-ttu-id="2efc2-244">U kunt vanaf elk willekeurig herstelpunt herstellen in de tijd.</span><span class="sxs-lookup"><span data-stu-id="2efc2-244">You can restore from any recovery point in time.</span></span> <span data-ttu-id="2efc2-245">Datums **vet** Hallo beschikbaarheid van ten minste één herstelpunt aangeven.</span><span class="sxs-lookup"><span data-stu-id="2efc2-245">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="2efc2-246">Wanneer u een datum selecteren als er meerdere herstelpunten beschikbaar zijn, kiest u Hallo specifiek herstelpunt van Hallo **tijd** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="2efc2-246">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![Zoeken naar objecten](./media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. <span data-ttu-id="2efc2-248">Klik op **koppelen** toolocally Hallo herstel koppelpunt als een volume herstel op uw *doelmachine*.</span><span class="sxs-lookup"><span data-stu-id="2efc2-248">Click **Mount** toolocally mount hello recovery point as a recovery volume on your *Target machine*.</span></span>

10. <span data-ttu-id="2efc2-249">Op Hallo **bladeren en bestanden herstellen** deelvenster, klikt u op **Bladeren** tooopen Windows Verkenner en zoek Hallo bestanden en mappen die u wilt.</span><span class="sxs-lookup"><span data-stu-id="2efc2-249">On hello **Browse and Recover Files** pane, click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span>

    ![Versleuteling](./media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. <span data-ttu-id="2efc2-251">In Windows Verkenner Hallo bestanden en/of mappen van Hallo herstel volume kopiëren en plakken tooyour *doelmachine* locatie.</span><span class="sxs-lookup"><span data-stu-id="2efc2-251">In Windows Explorer, copy hello files and/or folders from hello recovery volume and paste them tooyour *Target machine* location.</span></span> <span data-ttu-id="2efc2-252">U kunt openen of stream Hallo-bestanden rechtstreeks vanuit Hallo herstel volume en controleer of Hallo juist versies zijn hersteld.</span><span class="sxs-lookup"><span data-stu-id="2efc2-252">You can open or stream hello files directly from hello recovery volume and verify hello correct versions are recovered.</span></span>

    ![Versleuteling](./media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. <span data-ttu-id="2efc2-254">Als u klaar bent herstellen Hallo bestanden en/of mappen op Hallo **bladeren en herstelbestanden** deelvenster, klikt u op **ontkoppelen**.</span><span class="sxs-lookup"><span data-stu-id="2efc2-254">When you are finished restoring hello files and/or folders, on hello **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="2efc2-255">Klik vervolgens op **Ja** tooconfirm dat u wilt dat toounmount Hallo volume.</span><span class="sxs-lookup"><span data-stu-id="2efc2-255">Then click **Yes** tooconfirm that you want toounmount hello volume.</span></span>

    ![Versleuteling](./media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="2efc2-257">Als u niet ontkoppelen op, blijft Hallo herstel Volume gekoppelde gedurende zes uur van Hallo tijd wanneer deze is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="2efc2-257">If you do not click Unmount, hello Recovery Volume will remain mounted for six hours from hello time when it was mounted.</span></span> <span data-ttu-id="2efc2-258">Er is geen back-upbewerkingen wordt uitgevoerd tijdens het Hallo-volume is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="2efc2-258">No backup operations will run while hello volume is mounted.</span></span> <span data-ttu-id="2efc2-259">Een back-upbewerking gepland toorun tijdens Hallo wanneer Hallo volume is gekoppeld, wordt uitgevoerd nadat Hallo herstel volume is ontkoppeld.</span><span class="sxs-lookup"><span data-stu-id="2efc2-259">Any backup operation scheduled toorun during hello time when hello volume is mounted, will run after hello recovery volume is unmounted.</span></span>
    >


## <a name="next-steps"></a><span data-ttu-id="2efc2-260">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2efc2-260">Next steps</span></span>
* [<span data-ttu-id="2efc2-261">Veelgestelde vragen over Azure Backup</span><span class="sxs-lookup"><span data-stu-id="2efc2-261">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)
* <span data-ttu-id="2efc2-262">Ga naar Hallo [Azure back-up-Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933).</span><span class="sxs-lookup"><span data-stu-id="2efc2-262">Visit hello [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933).</span></span>

## <a name="learn-more"></a><span data-ttu-id="2efc2-263">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="2efc2-263">Learn more</span></span>
* [<span data-ttu-id="2efc2-264">Overzicht van Azure Backup</span><span class="sxs-lookup"><span data-stu-id="2efc2-264">Azure Backup Overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=222425)
* [<span data-ttu-id="2efc2-265">Back-virtuele machines in Azure</span><span class="sxs-lookup"><span data-stu-id="2efc2-265">Backup Azure virtual machines</span></span>](backup-azure-vms-introduction.md)
* [<span data-ttu-id="2efc2-266">Back-up van de werkbelasting van Microsoft</span><span class="sxs-lookup"><span data-stu-id="2efc2-266">Backup up Microsoft workloads</span></span>](backup-azure-dpm-introduction.md)
