---
title: aaaRestore gegevens in Azure tooa Windows Server of Windows-computer | Microsoft Docs
description: Meer informatie over hoe toorestore gegevens opgeslagen in Azure tooa Windows Server of Windows-computer.
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 742f4b9e-c0ab-4eeb-8e22-ee29b83c22c4
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/16/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: 11335495e448986a74f1733406f87e04331641d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="restore-files-tooa-windows-server-or-windows-client-machine-using-resource-manager-deployment-model"></a><span data-ttu-id="08617-103">Herstellen van bestanden tooa WindowsServer of Windows client-computer met Resource Manager-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="08617-103">Restore files tooa Windows server or Windows client machine using Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="08617-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="08617-104">Azure portal</span></span>](backup-azure-restore-windows-server.md)
> * [<span data-ttu-id="08617-105">Klassieke portal</span><span class="sxs-lookup"><span data-stu-id="08617-105">Classic portal</span></span>](backup-azure-restore-windows-server-classic.md)
>
>

<span data-ttu-id="08617-106">Dit artikel wordt uitgelegd hoe toorestore gegevens uit een back-upkluis.</span><span class="sxs-lookup"><span data-stu-id="08617-106">This article explains how toorestore data from a backup vault.</span></span> <span data-ttu-id="08617-107">toorestore gegevens, gebruikt u Hallo gegevens herstellen wizard in Hallo Microsoft Azure Recovery Services (MARS)-agent.</span><span class="sxs-lookup"><span data-stu-id="08617-107">toorestore data, you use hello Recover Data wizard in hello Microsoft Azure Recovery Services (MARS) agent.</span></span> <span data-ttu-id="08617-108">Wanneer u gegevens herstelt, is het mogelijk om te:</span><span class="sxs-lookup"><span data-stu-id="08617-108">When you restore data, it is possible to:</span></span>

* <span data-ttu-id="08617-109">Terugzetten van gegevens toohello dezelfde machine uit welke Hallo back-ups zijn uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="08617-109">Restore data toohello same machine from which hello backups were taken.</span></span>
* <span data-ttu-id="08617-110">Gegevens tooan alternatieve machine herstellen.</span><span class="sxs-lookup"><span data-stu-id="08617-110">Restore data tooan alternate machine.</span></span>

<span data-ttu-id="08617-111">Microsoft uitgebracht in januari 2017 een Preview update toohello MARS-agent.</span><span class="sxs-lookup"><span data-stu-id="08617-111">In January 2017, Microsoft released a Preview update toohello MARS agent.</span></span> <span data-ttu-id="08617-112">Samen met oplossingen voor problemen, deze update kan direct herstellen, zodat u toomount een momentopname van een beschrijfbare herstelpunt als een volume herstel.</span><span class="sxs-lookup"><span data-stu-id="08617-112">Along with bug fixes, this update enables Instant Restore, which allows you toomount a writeable recovery point snapshot as a recovery volume.</span></span> <span data-ttu-id="08617-113">U kunt vervolgens Hallo herstel volume en kopieert u bestanden tooa lokale computer waardoor selectief terugzetten bestanden verkennen.</span><span class="sxs-lookup"><span data-stu-id="08617-113">You can then explore hello recovery volume and copy files tooa local computer thereby selectively restoring files.</span></span>

> [!NOTE]
> <span data-ttu-id="08617-114">Hallo [januari 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) is vereist als u gegevens van toouse toorestore direct herstellen.</span><span class="sxs-lookup"><span data-stu-id="08617-114">hello [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) is required if you want toouse Instant Restore toorestore data.</span></span> <span data-ttu-id="08617-115">Back-upgegevens Hallo moeten ook worden beveiligd in kluizen in de landinstellingen die worden vermeld in artikel Hallo-ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="08617-115">Also hello backup data must be protected in vaults in locales listed in hello support article.</span></span> <span data-ttu-id="08617-116">Raadpleeg Hallo [januari 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) voor de meest recente lijst Hallo van landinstellingen die ondersteuning bieden voor chatberichten te herstellen.</span><span class="sxs-lookup"><span data-stu-id="08617-116">Consult hello [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) for hello latest list of locales that support Instant Restore.</span></span> <span data-ttu-id="08617-117">Direct herstellen is **niet** momenteel in alle landen beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="08617-117">Instant Restore is **not** currently available in all locales.</span></span>
>

<span data-ttu-id="08617-118">Chatberichten terugzetten is beschikbaar voor gebruik in de Recovery Services-kluizen in hello Azure-portal en Backup-kluizen in de klassieke portal Hallo.</span><span class="sxs-lookup"><span data-stu-id="08617-118">Instant Restore is available for use in Recovery Services vaults in hello Azure portal and Backup vaults in hello classic portal.</span></span> <span data-ttu-id="08617-119">Als u toouse direct herstellen wilt, Hallo MARS update downloaden en Hallo procedures volgen die vermeld direct herstellen.</span><span class="sxs-lookup"><span data-stu-id="08617-119">If you want toouse Instant Restore, download hello MARS update, and follow hello procedures that mention Instant Restore.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="use-instant-restore-toorecover-data-toohello-same-machine"></a><span data-ttu-id="08617-120">Direct herstellen toorecover gegevens toohello gebruiken dezelfde machine</span><span class="sxs-lookup"><span data-stu-id="08617-120">Use Instant Restore toorecover data toohello same machine</span></span>

<span data-ttu-id="08617-121">Als u een bestands- en desgewenst toorestore per ongeluk hebt verwijderd deze toohello dezelfde machine (vanaf welke Hallo back-up is gemaakt), Hallo te volgen stappen vindt u een Hallo-gegevens herstellen.</span><span class="sxs-lookup"><span data-stu-id="08617-121">If you accidentally deleted a file and wish toorestore it toohello same machine (from which hello backup is taken), hello following steps will help you recover hello data.</span></span>

1. <span data-ttu-id="08617-122">Open Hallo **Microsoft Azure Backup** uitlijnen in.</span><span class="sxs-lookup"><span data-stu-id="08617-122">Open hello **Microsoft Azure Backup** snap in.</span></span> <span data-ttu-id="08617-123">Als u niet waar Hallo-module is geïnstalleerd weet, zoekt u Hallo computer of server voor **Microsoft Azure Backup**.</span><span class="sxs-lookup"><span data-stu-id="08617-123">If you don't know where hello snap in was installed, search hello computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="08617-124">Hallo bureaublad-app moet worden weergegeven in zoekresultaten Hallo.</span><span class="sxs-lookup"><span data-stu-id="08617-124">hello desktop app should appear in hello search results.</span></span>

2. <span data-ttu-id="08617-125">Klik op **gegevens herstellen** toostart Hallo-wizard.</span><span class="sxs-lookup"><span data-stu-id="08617-125">Click **Recover Data** toostart hello wizard.</span></span>

    ![Gegevens herstellen](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="08617-127">Op Hallo **aan de slag** deelvenster, toorestore Hallo gegevens toohello dezelfde server of computer, selecteer **deze server (`<server name>`)** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="08617-127">On hello **Getting Started** pane, toorestore hello data toohello same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![Kies deze server optie toorestore Hallo gegevens toohello dezelfde machine](./media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. <span data-ttu-id="08617-129">Op Hallo **herstelmodus Selecteer** deelvenster kiezen **afzonderlijke bestanden en mappen** en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="08617-129">On hello **Select Recovery Mode** pane, choose **Individual files and folders** and then click **Next**.</span></span>

    ![Blader door bestanden](./media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. <span data-ttu-id="08617-131">Op Hallo **Volume selecteert en datum** deelvenster, selecteer Hallo-volume dat Hallo bestanden en/of mappen die u wilt dat toorestore bevat.</span><span class="sxs-lookup"><span data-stu-id="08617-131">On hello **Select Volume and Date** pane, select hello volume that contains hello files and/or folders you want toorestore.</span></span>

    <span data-ttu-id="08617-132">Selecteer een herstelpunt op Hallo-kalender.</span><span class="sxs-lookup"><span data-stu-id="08617-132">On hello calendar, select a recovery point.</span></span> <span data-ttu-id="08617-133">U kunt vanaf elk willekeurig herstelpunt herstellen in de tijd.</span><span class="sxs-lookup"><span data-stu-id="08617-133">You can restore from any recovery point in time.</span></span> <span data-ttu-id="08617-134">Datums **vet** Hallo beschikbaarheid van ten minste één herstelpunt aangeven.</span><span class="sxs-lookup"><span data-stu-id="08617-134">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="08617-135">Wanneer u een datum selecteren als er meerdere herstelpunten beschikbaar zijn, kiest u Hallo specifiek herstelpunt van Hallo **tijd** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="08617-135">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![Volume en datum](./media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. <span data-ttu-id="08617-137">Nadat u Hallo herstel punt toorestore hebt gekozen, klikt u op **koppelen**.</span><span class="sxs-lookup"><span data-stu-id="08617-137">Once you have chosen hello recovery point toorestore, click **Mount**.</span></span>

    <span data-ttu-id="08617-138">Azure Backup Hallo lokale herstelpunt koppelt en gebruikt als een volume herstel.</span><span class="sxs-lookup"><span data-stu-id="08617-138">Azure Backup mounts hello local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="08617-139">Op Hallo **bladeren en bestanden herstellen** deelvenster, klikt u op **Bladeren** tooopen Windows Verkenner en zoek Hallo bestanden en mappen die u wilt.</span><span class="sxs-lookup"><span data-stu-id="08617-139">On hello **Browse and Recover Files** pane, click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span>

    ![Opties voor herstel](./media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. <span data-ttu-id="08617-141">In Windows Verkenner, Hallo-bestanden kopiëren en/of mappen wilt toorestore en plak ze tooany locatie toohello lokale server of computer.</span><span class="sxs-lookup"><span data-stu-id="08617-141">In Windows Explorer, copy hello files and/or folders you want toorestore and paste them tooany location local toohello server or computer.</span></span> <span data-ttu-id="08617-142">U kunt openen of stream Hallo-bestanden rechtstreeks vanuit Hallo herstel volume en controleer of Hallo juist versies zijn hersteld.</span><span class="sxs-lookup"><span data-stu-id="08617-142">You can open or stream hello files directly from hello recovery volume and verify hello correct versions are recovered.</span></span>

    ![Kopiëren en plakken van bestanden en mappen van gekoppelde volume toolocal locatie](./media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. <span data-ttu-id="08617-144">Als u klaar bent herstellen Hallo bestanden en/of mappen op Hallo **bladeren en herstelbestanden** deelvenster, klikt u op **ontkoppelen**.</span><span class="sxs-lookup"><span data-stu-id="08617-144">When you are finished restoring hello files and/or folders, on hello **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="08617-145">Klik vervolgens op **Ja** tooconfirm dat u wilt dat toounmount Hallo volume.</span><span class="sxs-lookup"><span data-stu-id="08617-145">Then click **Yes** tooconfirm that you want toounmount hello volume.</span></span>

    ![Hallo volume ontkoppelen en bevestigen](./media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="08617-147">Als u niet ontkoppelen op, blijft Hallo herstel Volume gekoppelde gedurende zes uur van Hallo tijd wanneer deze is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="08617-147">If you do not click Unmount, hello Recovery Volume will remain mounted for 6 hours from hello time when it was mounted.</span></span> <span data-ttu-id="08617-148">Hallo mount-tijd is echter uitgebreide tot aan maximaal 24 uur in het geval van een doorlopende kopiëren van bestanden.</span><span class="sxs-lookup"><span data-stu-id="08617-148">However, hello mount time is extended upto a maximum of 24 hours in case of an ongoing file-copy.</span></span> <span data-ttu-id="08617-149">Er is geen back-upbewerkingen wordt uitgevoerd tijdens het Hallo-volume is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="08617-149">No backup operations will run while hello volume is mounted.</span></span> <span data-ttu-id="08617-150">Een back-upbewerking gepland toorun tijdens Hallo wanneer Hallo volume is gekoppeld, wordt uitgevoerd nadat Hallo herstel volume is ontkoppeld.</span><span class="sxs-lookup"><span data-stu-id="08617-150">Any backup operation scheduled toorun during hello time when hello volume is mounted, will run after hello recovery volume is unmounted.</span></span>
    >


## <a name="use-instant-restore-toorestore-data-tooan-alternate-machine"></a><span data-ttu-id="08617-151">Direct herstellen toorestore gegevens tooan alternatieve machine gebruiken</span><span class="sxs-lookup"><span data-stu-id="08617-151">Use Instant Restore toorestore data tooan alternate machine</span></span>
<span data-ttu-id="08617-152">Als uw hele server verbroken wordt, kunt u nog steeds gegevens herstellen vanaf de Azure Backup tooa andere machine.</span><span class="sxs-lookup"><span data-stu-id="08617-152">If your entire server is lost, you can still recover data from Azure Backup tooa different machine.</span></span> <span data-ttu-id="08617-153">Hallo stappen te volgen illustreren Hallo-werkstroom.</span><span class="sxs-lookup"><span data-stu-id="08617-153">hello following steps illustrate hello workflow.</span></span>


<span data-ttu-id="08617-154">Hallo-terminologie die wordt gebruikt in deze stap omvat het volgende:</span><span class="sxs-lookup"><span data-stu-id="08617-154">hello terminology used in these steps includes:</span></span>

* <span data-ttu-id="08617-155">*Bronmachine* : de oorspronkelijke machine Hallo van welke Hallo back-up is gemaakt en die momenteel niet beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="08617-155">*Source machine* – hello original machine from which hello backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="08617-156">*Doelcomputer* – Hallo machine toowhich Hallo gegevens worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="08617-156">*Target machine* – hello machine toowhich hello data is being recovered.</span></span>
* <span data-ttu-id="08617-157">*Voorbeeld kluis* – Hallo Recovery Services-kluis toowhich hello *bronmachine* en *doelmachine* zijn geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="08617-157">*Sample vault* – hello Recovery Services vault toowhich hello *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="08617-158">Back-ups niet herstelde tooa doelcomputer met een eerdere versie van besturingssysteem Hallo.</span><span class="sxs-lookup"><span data-stu-id="08617-158">Backups can't be restored tooa target machine running an earlier version of hello operating system.</span></span> <span data-ttu-id="08617-159">Bijvoorbeeld, een back-up van een Windows 7 computer kan worden hersteld op een Windows 8 of hoger, computer.</span><span class="sxs-lookup"><span data-stu-id="08617-159">For example, a backup taken from a Windows 7 computer can be restored on a Windows 8, or later, computer.</span></span> <span data-ttu-id="08617-160">Een back-up van een Windows 8-computer niet tooa Windows 7 van de herstelde computer.</span><span class="sxs-lookup"><span data-stu-id="08617-160">A backup taken from a Windows 8 computer cannot be restored tooa Windows 7 computer.</span></span>
>
>

1. <span data-ttu-id="08617-161">Open Hallo **Microsoft Azure Backup** uitlijnen in op Hallo *doelmachine*.</span><span class="sxs-lookup"><span data-stu-id="08617-161">Open hello **Microsoft Azure Backup** snap in on hello *Target machine*.</span></span>

2. <span data-ttu-id="08617-162">Zorg ervoor dat Hallo *doelmachine* en Hallo *bronmachine* zijn geregistreerde toohello dezelfde Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="08617-162">Ensure hello *Target machine* and hello *Source machine* are registered toohello same Recovery Services vault.</span></span>

3. <span data-ttu-id="08617-163">Klik op **gegevens herstellen** tooopen hello **wizard gegevens herstellen**.</span><span class="sxs-lookup"><span data-stu-id="08617-163">Click **Recover Data** tooopen hello **Recover Data wizard**.</span></span>

    ![Gegevens herstellen](./media/backup-azure-restore-windows-server/recover.png)

4. <span data-ttu-id="08617-165">Op Hallo **aan de slag** deelvenster **een andere server**</span><span class="sxs-lookup"><span data-stu-id="08617-165">On hello **Getting Started** pane, select **Another server**</span></span>

    ![Een andere Server](./media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. <span data-ttu-id="08617-167">Hallo-kluisreferentiebestand die overeenkomt met toohello bieden *voorbeeld kluis*, en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="08617-167">Provide hello vault credential file that corresponds toohello *Sample vault*, and click **Next**.</span></span>

    <span data-ttu-id="08617-168">Als het kluisreferentiebestand Hallo is ongeldig (of verlopen), het downloaden van een nieuw kluisreferentiebestand van Hallo *voorbeeld kluis* in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="08617-168">If hello vault credential file is invalid (or expired), download a new vault credential file from hello *Sample vault* in hello Azure portal.</span></span> <span data-ttu-id="08617-169">Zodra u de referenties van een geldige kluis opgeeft, wordt de naam Hallo Hallo Backup-kluis overeenkomt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="08617-169">Once you provide a valid vault credential, hello name of hello corresponding Backup Vault appears.</span></span>


6. <span data-ttu-id="08617-170">Op Hallo **back-up-Server selecteren** deelvenster, selecteer Hallo *bronmachine* uit Hallo lijst met weergegeven machines en Hallo wachtwoordzin opgeven.</span><span class="sxs-lookup"><span data-stu-id="08617-170">On hello **Select Backup Server** pane, select hello *Source machine* from hello list of displayed machines and provide hello passphrase.</span></span> <span data-ttu-id="08617-171">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="08617-171">Then click **Next**.</span></span>

    ![Lijst met computers](./media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. <span data-ttu-id="08617-173">Op Hallo **herstelmodus Selecteer** deelvenster Selecteer **afzonderlijke bestanden en mappen** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="08617-173">On hello **Select Recovery Mode** pane, select **Individual files and folders** and click **Next**.</span></span>

    ![Search](./media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. <span data-ttu-id="08617-175">Op Hallo **Volume selecteert en datum** deelvenster, selecteer Hallo-volume dat Hallo bestanden en/of mappen die u wilt dat toorestore bevat.</span><span class="sxs-lookup"><span data-stu-id="08617-175">On hello **Select Volume and Date** pane, select hello volume that contains hello files and/or folders you want toorestore.</span></span>

    <span data-ttu-id="08617-176">Selecteer een herstelpunt op Hallo-kalender.</span><span class="sxs-lookup"><span data-stu-id="08617-176">On hello calendar, select a recovery point.</span></span> <span data-ttu-id="08617-177">U kunt vanaf elk willekeurig herstelpunt herstellen in de tijd.</span><span class="sxs-lookup"><span data-stu-id="08617-177">You can restore from any recovery point in time.</span></span> <span data-ttu-id="08617-178">Datums **vet** Hallo beschikbaarheid van ten minste één herstelpunt aangeven.</span><span class="sxs-lookup"><span data-stu-id="08617-178">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="08617-179">Wanneer u een datum selecteren als er meerdere herstelpunten beschikbaar zijn, kiest u Hallo specifiek herstelpunt van Hallo **tijd** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="08617-179">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![Zoeken naar objecten](./media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. <span data-ttu-id="08617-181">Klik op **koppelen** toolocally Hallo herstel koppelpunt als een volume herstel op uw *doelmachine*.</span><span class="sxs-lookup"><span data-stu-id="08617-181">Click **Mount** toolocally mount hello recovery point as a recovery volume on your *Target machine*.</span></span>

10. <span data-ttu-id="08617-182">Op Hallo **bladeren en bestanden herstellen** deelvenster, klikt u op **Bladeren** tooopen Windows Verkenner en zoek Hallo bestanden en mappen die u wilt.</span><span class="sxs-lookup"><span data-stu-id="08617-182">On hello **Browse and Recover Files** pane, click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span>

    ![Versleuteling](./media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. <span data-ttu-id="08617-184">In Windows Verkenner Hallo bestanden en/of mappen van Hallo herstel volume kopiëren en plakken tooyour *doelmachine* locatie.</span><span class="sxs-lookup"><span data-stu-id="08617-184">In Windows Explorer, copy hello files and/or folders from hello recovery volume and paste them tooyour *Target machine* location.</span></span> <span data-ttu-id="08617-185">U kunt openen of stream Hallo-bestanden rechtstreeks vanuit Hallo herstel volume en controleer of Hallo juist versies zijn hersteld.</span><span class="sxs-lookup"><span data-stu-id="08617-185">You can open or stream hello files directly from hello recovery volume and verify hello correct versions are recovered.</span></span>

    ![Versleuteling](./media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. <span data-ttu-id="08617-187">Als u klaar bent herstellen Hallo bestanden en/of mappen op Hallo **bladeren en herstelbestanden** deelvenster, klikt u op **ontkoppelen**.</span><span class="sxs-lookup"><span data-stu-id="08617-187">When you are finished restoring hello files and/or folders, on hello **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="08617-188">Klik vervolgens op **Ja** tooconfirm dat u wilt dat toounmount Hallo volume.</span><span class="sxs-lookup"><span data-stu-id="08617-188">Then click **Yes** tooconfirm that you want toounmount hello volume.</span></span>

    ![Versleuteling](./media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="08617-190">Als u niet ontkoppelen op, blijft Hallo herstel Volume gekoppelde gedurende zes uur van Hallo tijd wanneer deze is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="08617-190">If you do not click Unmount, hello Recovery Volume will remain mounted for 6 hours from hello time when it was mounted.</span></span> <span data-ttu-id="08617-191">Hallo mount-tijd is echter uitgebreide tot aan maximaal 24 uur in het geval van een doorlopende kopiëren van bestanden.</span><span class="sxs-lookup"><span data-stu-id="08617-191">However, hello mount time is extended upto a maximum of 24 hours in case of an ongoing file-copy.</span></span> <span data-ttu-id="08617-192">Er is geen back-upbewerkingen wordt uitgevoerd tijdens het Hallo-volume is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="08617-192">No backup operations will run while hello volume is mounted.</span></span> <span data-ttu-id="08617-193">Een back-upbewerking gepland toorun tijdens Hallo wanneer Hallo volume is gekoppeld, wordt uitgevoerd nadat Hallo herstel volume is ontkoppeld.</span><span class="sxs-lookup"><span data-stu-id="08617-193">Any backup operation scheduled toorun during hello time when hello volume is mounted, will run after hello recovery volume is unmounted.</span></span>
    >

## <a name="troubleshooting"></a><span data-ttu-id="08617-194">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="08617-194">Troubleshooting</span></span>
<span data-ttu-id="08617-195">Als Azure Backup Hallo herstel volume niet met succes koppelt zelfs na enkele minuten van het klikken op **koppelen** of mislukt toomount Hallo herstel volume met een of meer fouten Hallo stappen hieronder toobegin normaal herstellen.</span><span class="sxs-lookup"><span data-stu-id="08617-195">If Azure Backup does not successfully mount hello recovery volume even after several minutes of clicking **Mount** or fails toomount hello recovery volume with one or more errors, follow hello steps below toobegin recovering normally.</span></span>

1.  <span data-ttu-id="08617-196">Hallo lopende koppelpunt proces annuleren als deze actief is geweest gedurende enkele minuten.</span><span class="sxs-lookup"><span data-stu-id="08617-196">Cancel hello ongoing mount process in case it has been running for several minutes.</span></span>

2.  <span data-ttu-id="08617-197">Zorg ervoor dat u zich op de meest recente versie Hallo van hello Azure backup-agent.</span><span class="sxs-lookup"><span data-stu-id="08617-197">Ensure that you are on hello latest version of hello Azure Backup agent.</span></span> <span data-ttu-id="08617-198">toofind hello versie-informatie van de Azure Backup-agent, klikt u op **over Microsoft Azure Recovery Services Agent** op Hallo **acties** deelvenster van de Microsoft Azure Backup console en zorg ervoor dat Hallo  **Versie** aantal is gelijk tooor hoger is dan de versie van Hallo vermeld in [in dit artikel](https://go.microsoft.com/fwlink/?linkid=229525).</span><span class="sxs-lookup"><span data-stu-id="08617-198">toofind out hello version information of Azure Backup agent, click on **About Microsoft Azure Recovery Services Agent** on hello **Actions** pane of Microsoft Azure Backup console and ensure that hello **Version** number is equal tooor higher than hello version mentioned in [this article](https://go.microsoft.com/fwlink/?linkid=229525).</span></span> <span data-ttu-id="08617-199">U kunt Hallo nieuwste versie downloaden van [hier](https://go.microsoft.com/fwLink/?LinkID=288905)</span><span class="sxs-lookup"><span data-stu-id="08617-199">You can download hello latest version from [here](https://go.microsoft.com/fwLink/?LinkID=288905)</span></span>

3.  <span data-ttu-id="08617-200">Ga te**Apparaatbeheer** -> **opslagcontrollers** en zorg ervoor dat u kunt vinden **Microsoft iSCSI-Initiator**.</span><span class="sxs-lookup"><span data-stu-id="08617-200">Go too**Device Manager** -> **Storage Controllers** and ensure that you can locate **Microsoft iSCSI Initiator**.</span></span> <span data-ttu-id="08617-201">Als u deze vinden kunt, gaat u rechtstreeks toostep 7 hieronder.</span><span class="sxs-lookup"><span data-stu-id="08617-201">If you can locate it, directly go toostep 7 below.</span></span> 

4.  <span data-ttu-id="08617-202">Als u kunt Microsoft iSCSI Initiator-service niet kunt vinden, zoals vermeld in stap 3, toosee controleren als u een item onder vindt **Apparaatbeheer** -> **opslagcontrollers** aangeroepen  **Onbekend apparaat** met Hardware-ID **ROOT\ISCSIPRT**.</span><span class="sxs-lookup"><span data-stu-id="08617-202">If you cannot locate Microsoft iSCSI Initiator service as mentioned in step 3, check toosee if you can find an entry under **Device Manager** -> **Storage Controllers** called **Unknown Device** with Hardware ID **ROOT\ISCSIPRT**.</span></span>

5.  <span data-ttu-id="08617-203">Klik met de rechtermuisknop op **onbekend apparaat** en selecteer **Update stuurprogramma's**.</span><span class="sxs-lookup"><span data-stu-id="08617-203">Right click on **Unknown Device** and select **Update Driver Software**.</span></span>

6.  <span data-ttu-id="08617-204">Hallo-stuurprogramma bijwerken door het Hallo-optie te selecteren **zoeken voor bijgewerkte stuurprogramma's automatisch**.</span><span class="sxs-lookup"><span data-stu-id="08617-204">Update hello driver by selecting hello option too **Search automatically for updated driver software**.</span></span> <span data-ttu-id="08617-205">Voltooiing van Hallo update moet worden gewijzigd **onbekend apparaat** te**Microsoft iSCSI-Initiator** zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="08617-205">Completion of hello update should change **Unknown Device** too**Microsoft iSCSI Initiator** as shown below.</span></span> 

    ![Versleuteling](./media/backup-azure-restore-windows-server/UnknowniSCSIDevice.png)

7.  <span data-ttu-id="08617-207">Ga te**Taakbeheer** -> **Services (lokaal)** -> **Microsoft iSCSI Initiator-Service**.</span><span class="sxs-lookup"><span data-stu-id="08617-207">Go too**Task Manager** -> **Services (Local)** -> **Microsoft iSCSI Initiator Service**.</span></span> 

    ![Versleuteling](./media/backup-azure-restore-windows-server/MicrosoftInitiatorServiceRunning.png)
    
8.  <span data-ttu-id="08617-209">Hallo Microsoft iSCSI Initiator-service opnieuw starten met de rechtermuisknop op het Hallo-service, te klikken op **stoppen** en verdere rechtermuisknop opnieuw te klikken en te klikken op **Start**.</span><span class="sxs-lookup"><span data-stu-id="08617-209">Restart hello Microsoft iSCSI Initiator service by right-clicking on hello service, clicking on **Stop** and further right clicking again and clicking on **Start**.</span></span>

9.  <span data-ttu-id="08617-210">Probeer herstellen met behulp van directe herstellen.</span><span class="sxs-lookup"><span data-stu-id="08617-210">Retry recovering using Instant Restore.</span></span> 

<span data-ttu-id="08617-211">Als het Hallo-herstel nog steeds mislukt, start opnieuw op uw server /-client.</span><span class="sxs-lookup"><span data-stu-id="08617-211">If hello recovery still fails, reboot your server/client.</span></span> <span data-ttu-id="08617-212">Als een opnieuw opstarten niet wenselijk is of Hallo herstel nog steeds niet zelfs na het Hallo-server opnieuw opstarten, vanaf een andere virtuele Machine en neem contact op met ondersteuning van Azure door te gaan[Azure Portal](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) en een ondersteuningsaanvraag indienen.</span><span class="sxs-lookup"><span data-stu-id="08617-212">If a reboot is not desirable or hello recovery still fails even after rebooting hello server, try recovering from an Alternate Machine, and contact Azure Support by going too[Azure Portal](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) and submitting a support request.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08617-213">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="08617-213">Next steps</span></span>
* <span data-ttu-id="08617-214">Nu dat u uw bestanden en mappen hebt hersteld, kunt u [beheren van uw back-ups](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="08617-214">Now that you've recovered your files and folders, you can [manage your backups](backup-azure-manage-windows-server.md).</span></span>
