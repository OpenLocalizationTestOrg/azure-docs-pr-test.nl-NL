---
title: Herstellen van gegevens in Azure met een Windows Server of Windows-computer | Microsoft Docs
description: Informatie over het herstellen van gegevens die zijn opgeslagen in Azure met een Windows Server of Windows-computer.
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
ms.openlocfilehash: 231dd61f95267b3a504ed70e9b3a5abc470b69b2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="restore-files-to-a-windows-server-or-windows-client-machine-using-resource-manager-deployment-model"></a><span data-ttu-id="8291b-103">Met het Resource Manager implementatiemodel bestanden herstellen op een Windows-server of Windows-clientcomputer</span><span class="sxs-lookup"><span data-stu-id="8291b-103">Restore files to a Windows server or Windows client machine using Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8291b-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="8291b-104">Azure portal</span></span>](backup-azure-restore-windows-server.md)
> * [<span data-ttu-id="8291b-105">Klassieke portal</span><span class="sxs-lookup"><span data-stu-id="8291b-105">Classic portal</span></span>](backup-azure-restore-windows-server-classic.md)
>
>

<span data-ttu-id="8291b-106">In dit artikel wordt uitgelegd hoe u gegevens terugzetten vanuit een back-upkluis.</span><span class="sxs-lookup"><span data-stu-id="8291b-106">This article explains how to restore data from a backup vault.</span></span> <span data-ttu-id="8291b-107">Voor het herstellen van gegevens, kunt u de wizard herstellen in de Microsoft Azure Recovery Services (MARS)-agent gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8291b-107">To restore data, you use the Recover Data wizard in the Microsoft Azure Recovery Services (MARS) agent.</span></span> <span data-ttu-id="8291b-108">Wanneer u gegevens herstelt, is het mogelijk om te:</span><span class="sxs-lookup"><span data-stu-id="8291b-108">When you restore data, it is possible to:</span></span>

* <span data-ttu-id="8291b-109">Gegevens terugzetten op dezelfde machine waaruit de back-ups zijn uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8291b-109">Restore data to the same machine from which the backups were taken.</span></span>
* <span data-ttu-id="8291b-110">Gegevens herstellen naar een andere virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8291b-110">Restore data to an alternate machine.</span></span>

<span data-ttu-id="8291b-111">Microsoft uitgebracht in januari 2017 een Preview-update voor de MARS-agent.</span><span class="sxs-lookup"><span data-stu-id="8291b-111">In January 2017, Microsoft released a Preview update to the MARS agent.</span></span> <span data-ttu-id="8291b-112">Samen met oplossingen voor problemen kan deze update direct herstellen, zodat u kunt het koppelen van een momentopname van een beschrijfbare herstelpunt als een volume herstel.</span><span class="sxs-lookup"><span data-stu-id="8291b-112">Along with bug fixes, this update enables Instant Restore, which allows you to mount a writeable recovery point snapshot as a recovery volume.</span></span> <span data-ttu-id="8291b-113">U kunt vervolgens de herstelde volume en kopieer de bestanden naar een lokale computer, waardoor selectief terugzetten bestanden verkennen.</span><span class="sxs-lookup"><span data-stu-id="8291b-113">You can then explore the recovery volume and copy files to a local computer thereby selectively restoring files.</span></span>

> [!NOTE]
> <span data-ttu-id="8291b-114">De [januari 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) is vereist als u wilt gebruiken direct herstellen om gegevens te herstellen.</span><span class="sxs-lookup"><span data-stu-id="8291b-114">The [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) is required if you want to use Instant Restore to restore data.</span></span> <span data-ttu-id="8291b-115">De back-upgegevens moeten ook worden beveiligd in kluizen in de landinstellingen die worden vermeld in het support-artikel.</span><span class="sxs-lookup"><span data-stu-id="8291b-115">Also the backup data must be protected in vaults in locales listed in the support article.</span></span> <span data-ttu-id="8291b-116">Raadpleeg de [januari 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) voor de meest recente lijst van landinstellingen die ondersteuning bieden voor chatberichten te herstellen.</span><span class="sxs-lookup"><span data-stu-id="8291b-116">Consult the [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) for the latest list of locales that support Instant Restore.</span></span> <span data-ttu-id="8291b-117">Direct herstellen is **niet** momenteel in alle landen beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="8291b-117">Instant Restore is **not** currently available in all locales.</span></span>
>

<span data-ttu-id="8291b-118">Chatberichten terugzetten is beschikbaar voor gebruik in de Recovery Services-kluizen in de Azure-portal en de Backup-kluizen in de klassieke portal.</span><span class="sxs-lookup"><span data-stu-id="8291b-118">Instant Restore is available for use in Recovery Services vaults in the Azure portal and Backup vaults in the classic portal.</span></span> <span data-ttu-id="8291b-119">Als u wilt gebruiken direct herstellen, de MARS-update downloaden en de procedures volgen die vermeld direct herstellen.</span><span class="sxs-lookup"><span data-stu-id="8291b-119">If you want to use Instant Restore, download the MARS update, and follow the procedures that mention Instant Restore.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="use-instant-restore-to-recover-data-to-the-same-machine"></a><span data-ttu-id="8291b-120">Direct herstellen gebruiken om gegevens op de machine te herstellen</span><span class="sxs-lookup"><span data-stu-id="8291b-120">Use Instant Restore to recover data to the same machine</span></span>

<span data-ttu-id="8291b-121">Als u per ongeluk een bestand verwijderd en u herstellen op de machine wilt (van waaruit de back-up is gemaakt), kunt de volgende stappen de gegevens te herstellen.</span><span class="sxs-lookup"><span data-stu-id="8291b-121">If you accidentally deleted a file and wish to restore it to the same machine (from which the backup is taken), the following steps will help you recover the data.</span></span>

1. <span data-ttu-id="8291b-122">Open de **Microsoft Azure Backup** uitlijnen in.</span><span class="sxs-lookup"><span data-stu-id="8291b-122">Open the **Microsoft Azure Backup** snap in.</span></span> <span data-ttu-id="8291b-123">Als u niet waar de module is geïnstalleerd weet, zoekt u de computer of server voor **Microsoft Azure Backup**.</span><span class="sxs-lookup"><span data-stu-id="8291b-123">If you don't know where the snap in was installed, search the computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="8291b-124">De bureaublad-app moet worden weergegeven in de zoekresultaten.</span><span class="sxs-lookup"><span data-stu-id="8291b-124">The desktop app should appear in the search results.</span></span>

2. <span data-ttu-id="8291b-125">Klik op **gegevens herstellen** om de wizard te starten.</span><span class="sxs-lookup"><span data-stu-id="8291b-125">Click **Recover Data** to start the wizard.</span></span>

    ![Gegevens herstellen](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="8291b-127">Op de **aan de slag** deelvenster voor het terugzetten van de gegevens op dezelfde server of computer, selecteer **deze server (`<server name>`)** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="8291b-127">On the **Getting Started** pane, to restore the data to the same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![Selecteer deze serveroptie als de gegevens herstelt op de machine](./media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. <span data-ttu-id="8291b-129">Op de **herstelmodus Selecteer** deelvenster kiezen **afzonderlijke bestanden en mappen** en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="8291b-129">On the **Select Recovery Mode** pane, choose **Individual files and folders** and then click **Next**.</span></span>

    ![Blader door bestanden](./media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. <span data-ttu-id="8291b-131">Op de **Volume selecteert en datum** deelvenster, selecteert u het volume met de bestanden en/of de mappen die u wilt herstellen.</span><span class="sxs-lookup"><span data-stu-id="8291b-131">On the **Select Volume and Date** pane, select the volume that contains the files and/or folders you want to restore.</span></span>

    <span data-ttu-id="8291b-132">Selecteer een herstelpunt op de kalender.</span><span class="sxs-lookup"><span data-stu-id="8291b-132">On the calendar, select a recovery point.</span></span> <span data-ttu-id="8291b-133">U kunt vanaf elk willekeurig herstelpunt herstellen in de tijd.</span><span class="sxs-lookup"><span data-stu-id="8291b-133">You can restore from any recovery point in time.</span></span> <span data-ttu-id="8291b-134">Datums **vet** geven aan de beschikbaarheid van ten minste één herstelpunt.</span><span class="sxs-lookup"><span data-stu-id="8291b-134">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="8291b-135">Wanneer u een datum selecteren als er meerdere herstelpunten beschikbaar zijn, kiest u de specifieke herstelpunt in de **tijd** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="8291b-135">Once you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span>

    ![Volume en datum](./media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. <span data-ttu-id="8291b-137">Nadat u ervoor het herstelpunt gekozen hebt te herstellen, klikt u op **koppelen**.</span><span class="sxs-lookup"><span data-stu-id="8291b-137">Once you have chosen the recovery point to restore, click **Mount**.</span></span>

    <span data-ttu-id="8291b-138">Azure Backup koppelt het lokale herstelpunt en gebruikt als een volume herstel.</span><span class="sxs-lookup"><span data-stu-id="8291b-138">Azure Backup mounts the local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="8291b-139">Op de **bladeren en bestanden herstellen** deelvenster, klikt u op **Bladeren** open Windows Verkenner en de bestanden en mappen die u wilt zoeken.</span><span class="sxs-lookup"><span data-stu-id="8291b-139">On the **Browse and Recover Files** pane, click **Browse** to open Windows Explorer and find the files and folders you want.</span></span>

    ![Opties voor herstel](./media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. <span data-ttu-id="8291b-141">Kopieer de bestanden en/of de mappen die u wilt herstellen en plak ze naar een locatie die lokaal op de server of de computer in Windows Verkenner.</span><span class="sxs-lookup"><span data-stu-id="8291b-141">In Windows Explorer, copy the files and/or folders you want to restore and paste them to any location local to the server or computer.</span></span> <span data-ttu-id="8291b-142">U kunt openen of de bestanden rechtstreeks van het volume herstel stream en controleer of dat de juiste versies zijn hersteld.</span><span class="sxs-lookup"><span data-stu-id="8291b-142">You can open or stream the files directly from the recovery volume and verify the correct versions are recovered.</span></span>

    ![Kopiëren en plakken van bestanden en mappen van het gekoppelde volume naar lokale locatie](./media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. <span data-ttu-id="8291b-144">Wanneer u klaar voor het herstellen van de bestanden en/of mappen bent, op de **bladeren en herstelbestanden** deelvenster, klikt u op **ontkoppelen**.</span><span class="sxs-lookup"><span data-stu-id="8291b-144">When you are finished restoring the files and/or folders, on the **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="8291b-145">Klik vervolgens op **Ja** om te bevestigen dat u wilt ontkoppelen van het volume.</span><span class="sxs-lookup"><span data-stu-id="8291b-145">Then click **Yes** to confirm that you want to unmount the volume.</span></span>

    ![Ontkoppelen van het volume en bevestigen](./media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="8291b-147">Als u niet ontkoppelen op, blijft het Volume Recovery gekoppelde gedurende 6 uur vanaf het moment waarop het is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="8291b-147">If you do not click Unmount, the Recovery Volume will remain mounted for 6 hours from the time when it was mounted.</span></span> <span data-ttu-id="8291b-148">De koppeltijd is echter uitgebreide tot aan maximaal 24 uur in het geval van een doorlopende kopiëren van bestanden.</span><span class="sxs-lookup"><span data-stu-id="8291b-148">However, the mount time is extended upto a maximum of 24 hours in case of an ongoing file-copy.</span></span> <span data-ttu-id="8291b-149">Er is geen back-upbewerkingen worden uitgevoerd terwijl het volume is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="8291b-149">No backup operations will run while the volume is mounted.</span></span> <span data-ttu-id="8291b-150">Een back-upbewerking die is gepland tijdens de tijd wanneer het volume is gekoppeld, wordt uitgevoerd nadat het herstel volume is ontkoppeld.</span><span class="sxs-lookup"><span data-stu-id="8291b-150">Any backup operation scheduled to run during the time when the volume is mounted, will run after the recovery volume is unmounted.</span></span>
    >


## <a name="use-instant-restore-to-restore-data-to-an-alternate-machine"></a><span data-ttu-id="8291b-151">Direct herstellen gebruiken om gegevens te herstellen naar een andere computer</span><span class="sxs-lookup"><span data-stu-id="8291b-151">Use Instant Restore to restore data to an alternate machine</span></span>
<span data-ttu-id="8291b-152">Als uw hele server verloren gegaan is, kunt u nog steeds gegevens herstellen vanaf Azure back-up naar een andere computer.</span><span class="sxs-lookup"><span data-stu-id="8291b-152">If your entire server is lost, you can still recover data from Azure Backup to a different machine.</span></span> <span data-ttu-id="8291b-153">De volgende stappen laten zien dat de werkstroom.</span><span class="sxs-lookup"><span data-stu-id="8291b-153">The following steps illustrate the workflow.</span></span>


<span data-ttu-id="8291b-154">De terminologie die wordt gebruikt in deze stap omvat het volgende:</span><span class="sxs-lookup"><span data-stu-id="8291b-154">The terminology used in these steps includes:</span></span>

* <span data-ttu-id="8291b-155">*Bronmachine* : de oorspronkelijke computer waarop de back-up is gemaakt en die momenteel niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="8291b-155">*Source machine* – The original machine from which the backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="8291b-156">*Doelcomputer* : de computer waarop de gegevens worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="8291b-156">*Target machine* – The machine to which the data is being recovered.</span></span>
* <span data-ttu-id="8291b-157">*Voorbeeld kluis* – de Recovery Services-kluis waarnaar de *bronmachine* en *doelmachine* zijn geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="8291b-157">*Sample vault* – The Recovery Services vault to which the *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="8291b-158">Back-ups kunnen niet worden hersteld naar een doelcomputer met een eerdere versie van het besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="8291b-158">Backups can't be restored to a target machine running an earlier version of the operating system.</span></span> <span data-ttu-id="8291b-159">Bijvoorbeeld, een back-up van een Windows 7 computer kan worden hersteld op een Windows 8 of hoger, computer.</span><span class="sxs-lookup"><span data-stu-id="8291b-159">For example, a backup taken from a Windows 7 computer can be restored on a Windows 8, or later, computer.</span></span> <span data-ttu-id="8291b-160">Een back-up van een computer met Windows 8 kan niet worden hersteld naar een computer met Windows 7.</span><span class="sxs-lookup"><span data-stu-id="8291b-160">A backup taken from a Windows 8 computer cannot be restored to a Windows 7 computer.</span></span>
>
>

1. <span data-ttu-id="8291b-161">Open de **Microsoft Azure Backup** uitlijnen in op de *doelmachine*.</span><span class="sxs-lookup"><span data-stu-id="8291b-161">Open the **Microsoft Azure Backup** snap in on the *Target machine*.</span></span>

2. <span data-ttu-id="8291b-162">Zorg ervoor dat de *doelmachine* en de *bronmachine* zijn geregistreerd bij dezelfde Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="8291b-162">Ensure the *Target machine* and the *Source machine* are registered to the same Recovery Services vault.</span></span>

3. <span data-ttu-id="8291b-163">Klik op **gegevens herstellen** openen de **wizard gegevens herstellen**.</span><span class="sxs-lookup"><span data-stu-id="8291b-163">Click **Recover Data** to open the **Recover Data wizard**.</span></span>

    ![Gegevens herstellen](./media/backup-azure-restore-windows-server/recover.png)

4. <span data-ttu-id="8291b-165">Op de **aan de slag** deelvenster **een andere server**</span><span class="sxs-lookup"><span data-stu-id="8291b-165">On the **Getting Started** pane, select **Another server**</span></span>

    ![Een andere Server](./media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. <span data-ttu-id="8291b-167">Geef het kluisreferentiebestand die overeenkomt met de *voorbeeld kluis*, en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="8291b-167">Provide the vault credential file that corresponds to the *Sample vault*, and click **Next**.</span></span>

    <span data-ttu-id="8291b-168">Als het kluisreferentiebestand is ongeldig (of verlopen), downloadt u een nieuw kluisreferentiebestand van de *voorbeeld kluis* in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8291b-168">If the vault credential file is invalid (or expired), download a new vault credential file from the *Sample vault* in the Azure portal.</span></span> <span data-ttu-id="8291b-169">Zodra u de referenties van een geldige kluis opgeeft, wordt de naam van de bijbehorende Backup-kluis weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8291b-169">Once you provide a valid vault credential, the name of the corresponding Backup Vault appears.</span></span>


6. <span data-ttu-id="8291b-170">Op de **back-up-Server selecteren** deelvenster, selecteer de *bronmachine* uit de lijst met weergegeven machines en geef de wachtwoordzin.</span><span class="sxs-lookup"><span data-stu-id="8291b-170">On the **Select Backup Server** pane, select the *Source machine* from the list of displayed machines and provide the passphrase.</span></span> <span data-ttu-id="8291b-171">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="8291b-171">Then click **Next**.</span></span>

    ![Lijst met computers](./media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. <span data-ttu-id="8291b-173">Op de **herstelmodus Selecteer** deelvenster Selecteer **afzonderlijke bestanden en mappen** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="8291b-173">On the **Select Recovery Mode** pane, select **Individual files and folders** and click **Next**.</span></span>

    ![Search](./media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. <span data-ttu-id="8291b-175">Op de **Volume selecteert en datum** deelvenster, selecteert u het volume met de bestanden en/of de mappen die u wilt herstellen.</span><span class="sxs-lookup"><span data-stu-id="8291b-175">On the **Select Volume and Date** pane, select the volume that contains the files and/or folders you want to restore.</span></span>

    <span data-ttu-id="8291b-176">Selecteer een herstelpunt op de kalender.</span><span class="sxs-lookup"><span data-stu-id="8291b-176">On the calendar, select a recovery point.</span></span> <span data-ttu-id="8291b-177">U kunt vanaf elk willekeurig herstelpunt herstellen in de tijd.</span><span class="sxs-lookup"><span data-stu-id="8291b-177">You can restore from any recovery point in time.</span></span> <span data-ttu-id="8291b-178">Datums **vet** geven aan de beschikbaarheid van ten minste één herstelpunt.</span><span class="sxs-lookup"><span data-stu-id="8291b-178">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="8291b-179">Wanneer u een datum selecteren als er meerdere herstelpunten beschikbaar zijn, kiest u de specifieke herstelpunt in de **tijd** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="8291b-179">Once you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span>

    ![Zoeken naar objecten](./media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. <span data-ttu-id="8291b-181">Klik op **koppelen** lokaal koppelen van het herstelpunt dat als een volume herstel aan uw *doelmachine*.</span><span class="sxs-lookup"><span data-stu-id="8291b-181">Click **Mount** to locally mount the recovery point as a recovery volume on your *Target machine*.</span></span>

10. <span data-ttu-id="8291b-182">Op de **bladeren en bestanden herstellen** deelvenster, klikt u op **Bladeren** open Windows Verkenner en de bestanden en mappen die u wilt zoeken.</span><span class="sxs-lookup"><span data-stu-id="8291b-182">On the **Browse and Recover Files** pane, click **Browse** to open Windows Explorer and find the files and folders you want.</span></span>

    ![Versleuteling](./media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. <span data-ttu-id="8291b-184">In Windows Verkenner, kopieert u de bestanden en/of mappen van het volume herstel en plak ze aan uw *doelmachine* locatie.</span><span class="sxs-lookup"><span data-stu-id="8291b-184">In Windows Explorer, copy the files and/or folders from the recovery volume and paste them to your *Target machine* location.</span></span> <span data-ttu-id="8291b-185">U kunt openen of de bestanden rechtstreeks van het volume herstel stream en controleer of dat de juiste versies zijn hersteld.</span><span class="sxs-lookup"><span data-stu-id="8291b-185">You can open or stream the files directly from the recovery volume and verify the correct versions are recovered.</span></span>

    ![Versleuteling](./media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. <span data-ttu-id="8291b-187">Wanneer u klaar voor het herstellen van de bestanden en/of mappen bent, op de **bladeren en herstelbestanden** deelvenster, klikt u op **ontkoppelen**.</span><span class="sxs-lookup"><span data-stu-id="8291b-187">When you are finished restoring the files and/or folders, on the **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="8291b-188">Klik vervolgens op **Ja** om te bevestigen dat u wilt ontkoppelen van het volume.</span><span class="sxs-lookup"><span data-stu-id="8291b-188">Then click **Yes** to confirm that you want to unmount the volume.</span></span>

    ![Versleuteling](./media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="8291b-190">Als u niet ontkoppelen op, blijft het Volume Recovery gekoppelde gedurende 6 uur vanaf het moment waarop het is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="8291b-190">If you do not click Unmount, the Recovery Volume will remain mounted for 6 hours from the time when it was mounted.</span></span> <span data-ttu-id="8291b-191">De koppeltijd is echter uitgebreide tot aan maximaal 24 uur in het geval van een doorlopende kopiëren van bestanden.</span><span class="sxs-lookup"><span data-stu-id="8291b-191">However, the mount time is extended upto a maximum of 24 hours in case of an ongoing file-copy.</span></span> <span data-ttu-id="8291b-192">Er is geen back-upbewerkingen worden uitgevoerd terwijl het volume is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="8291b-192">No backup operations will run while the volume is mounted.</span></span> <span data-ttu-id="8291b-193">Een back-upbewerking die is gepland tijdens de tijd wanneer het volume is gekoppeld, wordt uitgevoerd nadat het herstel volume is ontkoppeld.</span><span class="sxs-lookup"><span data-stu-id="8291b-193">Any backup operation scheduled to run during the time when the volume is mounted, will run after the recovery volume is unmounted.</span></span>
    >

## <a name="troubleshooting"></a><span data-ttu-id="8291b-194">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="8291b-194">Troubleshooting</span></span>
<span data-ttu-id="8291b-195">Als Azure Backup het herstel volume niet met succes koppelt zelfs na enkele minuten van het klikken op **koppelen** of koppelen van het volume herstel met een of meer fouten niet de volgende stappen om te beginnen met het herstellen van normaal.</span><span class="sxs-lookup"><span data-stu-id="8291b-195">If Azure Backup does not successfully mount the recovery volume even after several minutes of clicking **Mount** or fails to mount the recovery volume with one or more errors, follow the steps below to begin recovering normally.</span></span>

1.  <span data-ttu-id="8291b-196">Het actieve koppelpunt annuleren als deze actief is geweest gedurende enkele minuten.</span><span class="sxs-lookup"><span data-stu-id="8291b-196">Cancel the ongoing mount process in case it has been running for several minutes.</span></span>

2.  <span data-ttu-id="8291b-197">Zorg ervoor dat u over de nieuwste versie van de Azure Backup agent.</span><span class="sxs-lookup"><span data-stu-id="8291b-197">Ensure that you are on the latest version of the Azure Backup agent.</span></span> <span data-ttu-id="8291b-198">Voor de versie-informatie van Azure backup-agent, klikt u op **over Microsoft Azure Recovery Services Agent** op de **acties** deelvenster van de Microsoft Azure Backup console en zorg ervoor dat de **versie** getal gelijk is aan of hoger is dan de versie vermeld in [in dit artikel](https://go.microsoft.com/fwlink/?linkid=229525).</span><span class="sxs-lookup"><span data-stu-id="8291b-198">To find out the version information of Azure Backup agent, click on **About Microsoft Azure Recovery Services Agent** on the **Actions** pane of Microsoft Azure Backup console and ensure that the **Version** number is equal to or higher than the version mentioned in [this article](https://go.microsoft.com/fwlink/?linkid=229525).</span></span> <span data-ttu-id="8291b-199">U kunt de nieuwste versie van downloaden [hier](https://go.microsoft.com/fwLink/?LinkID=288905)</span><span class="sxs-lookup"><span data-stu-id="8291b-199">You can download the latest version from [here](https://go.microsoft.com/fwLink/?LinkID=288905)</span></span>

3.  <span data-ttu-id="8291b-200">Ga naar **Apparaatbeheer** -> **opslagcontrollers** en zorg ervoor dat u kunt vinden **Microsoft iSCSI-Initiator**.</span><span class="sxs-lookup"><span data-stu-id="8291b-200">Go to **Device Manager** -> **Storage Controllers** and ensure that you can locate **Microsoft iSCSI Initiator**.</span></span> <span data-ttu-id="8291b-201">Als u deze vinden kunt, rechtstreeks gaat u naar stap 7 hieronder.</span><span class="sxs-lookup"><span data-stu-id="8291b-201">If you can locate it, directly go to step 7 below.</span></span> 

4.  <span data-ttu-id="8291b-202">Als u kunt Microsoft iSCSI Initiator-service kan niet vinden, zoals vermeld in stap 3, controleert u als vindt u een item onder **Apparaatbeheer** -> **opslagcontrollers** aangeroepen **onbekend apparaat** met Hardware-ID **ROOT\ISCSIPRT**.</span><span class="sxs-lookup"><span data-stu-id="8291b-202">If you cannot locate Microsoft iSCSI Initiator service as mentioned in step 3, check to see if you can find an entry under **Device Manager** -> **Storage Controllers** called **Unknown Device** with Hardware ID **ROOT\ISCSIPRT**.</span></span>

5.  <span data-ttu-id="8291b-203">Klik met de rechtermuisknop op **onbekend apparaat** en selecteer **Update stuurprogramma's**.</span><span class="sxs-lookup"><span data-stu-id="8291b-203">Right click on **Unknown Device** and select **Update Driver Software**.</span></span>

6.  <span data-ttu-id="8291b-204">Het stuurprogramma bijwerken door de optie voor **zoeken voor bijgewerkte stuurprogramma's automatisch**.</span><span class="sxs-lookup"><span data-stu-id="8291b-204">Update the driver by selecting the option to  **Search automatically for updated driver software**.</span></span> <span data-ttu-id="8291b-205">Voltooiing van de update moet worden gewijzigd **onbekend apparaat** naar **Microsoft iSCSI-Initiator** zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8291b-205">Completion of the update should change **Unknown Device** to **Microsoft iSCSI Initiator** as shown below.</span></span> 

    ![Versleuteling](./media/backup-azure-restore-windows-server/UnknowniSCSIDevice.png)

7.  <span data-ttu-id="8291b-207">Ga naar **Taakbeheer** -> **Services (lokaal)** -> **Microsoft iSCSI Initiator-Service**.</span><span class="sxs-lookup"><span data-stu-id="8291b-207">Go to **Task Manager** -> **Services (Local)** -> **Microsoft iSCSI Initiator Service**.</span></span> 

    ![Versleuteling](./media/backup-azure-restore-windows-server/MicrosoftInitiatorServiceRunning.png)
    
8.  <span data-ttu-id="8291b-209">Microsoft iSCSI Initiator-service opnieuw starten met de rechtermuisknop op de service, te klikken op **stoppen** en verdere rechtermuisknop opnieuw te klikken en te klikken op **Start**.</span><span class="sxs-lookup"><span data-stu-id="8291b-209">Restart the Microsoft iSCSI Initiator service by right-clicking on the service, clicking on **Stop** and further right clicking again and clicking on **Start**.</span></span>

9.  <span data-ttu-id="8291b-210">Probeer herstellen met behulp van directe herstellen.</span><span class="sxs-lookup"><span data-stu-id="8291b-210">Retry recovering using Instant Restore.</span></span> 

<span data-ttu-id="8291b-211">Als het herstel nog steeds mislukt, start opnieuw op uw server /-client.</span><span class="sxs-lookup"><span data-stu-id="8291b-211">If the recovery still fails, reboot your server/client.</span></span> <span data-ttu-id="8291b-212">Als opnieuw opstarten niet wenselijk is of het herstel nog steeds mislukt nadat de server opnieuw opstarten vanaf een andere virtuele Machine en neem contact op met ondersteuning van Azure door te gaan naar [Azure Portal](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) en een ondersteuningsaanvraag indienen.</span><span class="sxs-lookup"><span data-stu-id="8291b-212">If a reboot is not desirable or the recovery still fails even after rebooting the server, try recovering from an Alternate Machine, and contact Azure Support by going to [Azure Portal](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) and submitting a support request.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8291b-213">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8291b-213">Next steps</span></span>
* <span data-ttu-id="8291b-214">Nu dat u uw bestanden en mappen hebt hersteld, kunt u [beheren van uw back-ups](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="8291b-214">Now that you've recovered your files and folders, you can [manage your backups](backup-azure-manage-windows-server.md).</span></span>
