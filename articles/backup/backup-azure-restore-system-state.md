---
title: 'Azure Backup: Systeemstatus terugzetten naar een WindowsServer | Microsoft Docs'
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
ms.openlocfilehash: 320c85f8045d9b72cf7f430d2e2736ba8e5ec269
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="restore-system-state-to-windows-server"></a><span data-ttu-id="f1c57-103">Systeemstatus terugzetten naar WindowsServer</span><span class="sxs-lookup"><span data-stu-id="f1c57-103">Restore System State to Windows Server</span></span>

<span data-ttu-id="f1c57-104">In dit artikel wordt uitgelegd hoe Windows Server System State back-ups herstellen uit een Azure Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="f1c57-104">This article explains how to restore Windows Server System State backups from an Azure Recovery Services vault.</span></span> <span data-ttu-id="f1c57-105">Als u systeemstatus herstellen, moet u een systeemstatusback-up hebben (gemaakt met behulp van de instructies in [Back-up van systeemstatus](backup-azure-system-state.md#back-up-windows-server-system-state-preview)), en zorg ervoor dat u hebt geïnstalleerd het [meest recente versie van de agent van Microsoft Azure Recovery Services (MARS)](http://aka.ms/azurebackup_agent).</span><span class="sxs-lookup"><span data-stu-id="f1c57-105">To restore System State, you must have a System State backup (created using the instructions in [Back up System State](backup-azure-system-state.md#back-up-windows-server-system-state-preview)), and make sure you have installed the [latest version of the Microsoft Azure Recovery Services (MARS) agent](http://aka.ms/azurebackup_agent).</span></span> <span data-ttu-id="f1c57-106">Systeemstatus van Windows Server-gegevens herstellen vanaf een Azure Recovery Services-kluis is een proces in twee stappen:</span><span class="sxs-lookup"><span data-stu-id="f1c57-106">Recovering Windows Server System State data from an Azure Recovery Services vault is a two-step process:</span></span>

1. <span data-ttu-id="f1c57-107">Systeemstatus terugzetten als bestanden vanuit Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="f1c57-107">Restore System State as files from Azure Backup.</span></span> <span data-ttu-id="f1c57-108">Bij het herstellen van systeemstatus als bestanden vanuit Azure Backup, kunt u:</span><span class="sxs-lookup"><span data-stu-id="f1c57-108">When restoring System State as files from Azure Backup, you can either:</span></span>
  * <span data-ttu-id="f1c57-109">Restore systeemstatus naar dezelfde server waarop de back-ups zijn gemaakt, of</span><span class="sxs-lookup"><span data-stu-id="f1c57-109">Restore System State to the same server where the backups were taken, or</span></span>
  * <span data-ttu-id="f1c57-110">Bestand van de systeemstatus herstellen naar een alternatieve server.</span><span class="sxs-lookup"><span data-stu-id="f1c57-110">Restore System State file to an alternate server.</span></span>

2. <span data-ttu-id="f1c57-111">De herstelde bestanden van de systeemstatus van toepassing op een Windows-Server.</span><span class="sxs-lookup"><span data-stu-id="f1c57-111">Apply the restored System State files to a Windows Server.</span></span>


## <a name="recover-system-state-files-to-the-same-server"></a><span data-ttu-id="f1c57-112">Bestanden van de systeemstatus herstellen naar dezelfde server</span><span class="sxs-lookup"><span data-stu-id="f1c57-112">Recover System State files to the same server</span></span>
<span data-ttu-id="f1c57-113">De volgende stappen wordt uitgelegd hoe uw Windows Server-configuratie terugdraaien naar een eerdere status.</span><span class="sxs-lookup"><span data-stu-id="f1c57-113">The following steps explain how to roll back your Windows Server configuration to a previous state.</span></span> <span data-ttu-id="f1c57-114">Configuratie van uw server terugdraaien naar een bekende, stabiele status, kan zeer waardevol zijn.</span><span class="sxs-lookup"><span data-stu-id="f1c57-114">Rolling your server configuration back to a known, stable state, can be extremely valuable.</span></span> <span data-ttu-id="f1c57-115">De systeemstatus van de server terugzetten de volgende stappen vanaf een Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="f1c57-115">The following steps restore the server's System State from a Recovery Services vault.</span></span> 

1. <span data-ttu-id="f1c57-116">Open de **Microsoft Azure Backup** -module.</span><span class="sxs-lookup"><span data-stu-id="f1c57-116">Open the **Microsoft Azure Backup** snap-in.</span></span> <span data-ttu-id="f1c57-117">Als u niet waar dat de module is geïnstalleerd weet, zoekt u de computer of server voor **Microsoft Azure Backup**.</span><span class="sxs-lookup"><span data-stu-id="f1c57-117">If you don't know where the snap-in was installed, search the computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="f1c57-118">De bureaublad-app moet worden weergegeven in de zoekresultaten.</span><span class="sxs-lookup"><span data-stu-id="f1c57-118">The desktop app should appear in the search results.</span></span>

2. <span data-ttu-id="f1c57-119">Klik op **gegevens herstellen** om de wizard te starten.</span><span class="sxs-lookup"><span data-stu-id="f1c57-119">Click **Recover Data** to start the wizard.</span></span>

    ![Gegevens herstellen](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="f1c57-121">Op de **aan de slag** deelvenster voor het terugzetten van de gegevens op dezelfde server of computer, selecteer **deze server (`<server name>`)** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="f1c57-121">On the **Getting Started** pane, to restore the data to the same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![Selecteer deze serveroptie als de gegevens herstelt op de machine](./media/backup-azure-restore-system-state/samemachine.png)

4. <span data-ttu-id="f1c57-123">Op de **herstelmodus Selecteer** deelvenster kiezen **systeemstatus** en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="f1c57-123">On the **Select Recovery Mode** pane, choose **System State** and then click **Next**.</span></span>

    ![Blader door bestanden](./media/backup-azure-restore-system-state/recover-type-selection.png)

5. <span data-ttu-id="f1c57-125">In de kalender in **Volume selecteert en datum** deelvenster, selecteert u een herstel verwijzen.</span><span class="sxs-lookup"><span data-stu-id="f1c57-125">On the calendar in **Select Volume and Date** pane, select a recovery point.</span></span> 

    <span data-ttu-id="f1c57-126">U kunt vanaf elk willekeurig herstelpunt herstellen in de tijd.</span><span class="sxs-lookup"><span data-stu-id="f1c57-126">You can restore from any recovery point in time.</span></span> <span data-ttu-id="f1c57-127">Datums **vet** geven aan de beschikbaarheid van ten minste één herstelpunt.</span><span class="sxs-lookup"><span data-stu-id="f1c57-127">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="f1c57-128">Wanneer u een datum selecteren als er meerdere herstelpunten beschikbaar zijn, kiest u de specifieke herstelpunt in de **tijd** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="f1c57-128">Once you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span>

    ![Volume en datum](./media/backup-azure-restore-system-state/select-date.png)

6. <span data-ttu-id="f1c57-130">Nadat u ervoor het herstelpunt gekozen hebt te herstellen, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="f1c57-130">Once you have chosen the recovery point to restore, click **Next**.</span></span>

    <span data-ttu-id="f1c57-131">Azure Backup koppelt het lokale herstelpunt en gebruikt als een volume herstel.</span><span class="sxs-lookup"><span data-stu-id="f1c57-131">Azure Backup mounts the local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="f1c57-132">Geef het doel voor de herstelde bestanden van de systeemstatus in het volgende deelvenster en klik op **Bladeren** open Windows Verkenner en de bestanden en mappen die u wilt zoeken.</span><span class="sxs-lookup"><span data-stu-id="f1c57-132">On the next pane, specify the destination for the recovered System State files and click **Browse** to open Windows Explorer and find the files and folders you want.</span></span> <span data-ttu-id="f1c57-133">De optie **kopieën te maken, zodat beide versies**, maakt kopieën van afzonderlijke bestanden in een bestaande systeemstatus bestandsarchief in plaats van de kopie van het gehele archief van de systeemstatus te maken.</span><span class="sxs-lookup"><span data-stu-id="f1c57-133">The option, **Create copies so that you have both versions**, creates copies of individual files in an existing System State file archive instead of creating the copy of the entire System State archive.</span></span>

    ![Opties voor herstel](./media/backup-azure-restore-system-state/recover-as-files.png)

8. <span data-ttu-id="f1c57-135">Controleer de details van herstelpunten op de **bevestiging** deelvenster en klik op **herstellen**.</span><span class="sxs-lookup"><span data-stu-id="f1c57-135">Verify the details of recovery on the **Confirmation** pane and click **Recover**.</span></span>

   ![Klik op herstellen om de actie herstellen bevestigen](./media/backup-azure-restore-system-state/confirm-recovery.png)

9. <span data-ttu-id="f1c57-137">Kopieer de *WindowsImageBackup* map in de doel-herstel naar een niet-kritieke volume van de server.</span><span class="sxs-lookup"><span data-stu-id="f1c57-137">Copy the *WindowsImageBackup* directory in the Recovery destination to a non-critical volume of the server.</span></span> <span data-ttu-id="f1c57-138">Het Windows-besturingssysteemvolume is meestal het essentiële volume.</span><span class="sxs-lookup"><span data-stu-id="f1c57-138">Usually, the Windows OS volume is the critical volume.</span></span>

10. <span data-ttu-id="f1c57-139">Wanneer het herstel voltooid is, volg de stappen in de sectie [toepassen systeemstatus bestanden naar de Windows-Server hersteld](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server), om de systeemstatus herstellen proces te voltooien.</span><span class="sxs-lookup"><span data-stu-id="f1c57-139">Once the recovery is successful, follow the steps in the section, [Apply restored System State files to the Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server), to complete the System State recovery process.</span></span>

## <a name="recover-system-state-files-to-an-alternate-server"></a><span data-ttu-id="f1c57-140">Bestanden van de systeemstatus herstellen naar een alternatieve server</span><span class="sxs-lookup"><span data-stu-id="f1c57-140">Recover System State files to an alternate server</span></span>

<span data-ttu-id="f1c57-141">Als uw Windows-Server beschadigd of niet toegankelijk is en u herstellen naar een stabiele status wilt door het herstellen van de systeemstatus van Windows Server, kunt u de systeemstatus van de beschadigde server herstellen vanaf een andere server.</span><span class="sxs-lookup"><span data-stu-id="f1c57-141">If your Windows Server is corrupted or inaccessible, and you want to restore it to a stable state by recovering the Windows Server System State, you can restore the corrupted server's System State from another server.</span></span> <span data-ttu-id="f1c57-142">Gebruik de volgende stappen voor het terugzetten van systeemstatus op een afzonderlijke server.</span><span class="sxs-lookup"><span data-stu-id="f1c57-142">Use the following steps to the restore System State on a separate server.</span></span>  

<span data-ttu-id="f1c57-143">De terminologie die wordt gebruikt in deze stap omvat het volgende:</span><span class="sxs-lookup"><span data-stu-id="f1c57-143">The terminology used in these steps includes:</span></span>

- <span data-ttu-id="f1c57-144">*Bronmachine* : de oorspronkelijke computer waarop de back-up is gemaakt en die momenteel niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="f1c57-144">*Source machine* – The original machine from which the backup was taken and which is currently unavailable.</span></span>
- <span data-ttu-id="f1c57-145">*Doelcomputer* : de computer waarop de gegevens worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="f1c57-145">*Target machine* – The machine to which the data is being recovered.</span></span>
- <span data-ttu-id="f1c57-146">*Voorbeeld kluis* – de Recovery Services-kluis waarnaar de *bronmachine* en *doelmachine* zijn geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="f1c57-146">*Sample vault* – The Recovery Services vault to which the *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="f1c57-147">Back-ups die afkomstig zijn uit één machine kunnen niet worden hersteld naar een machine met een eerdere versie van het besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="f1c57-147">Backups taken from one machine cannot be restored to a machine running an earlier version of the operating system.</span></span> <span data-ttu-id="f1c57-148">Bijvoorbeeld: back-ups die afkomstig zijn uit een Windows Server 2016-machine kunnen niet worden teruggezet naar Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="f1c57-148">For example, backups taken from a Windows Server 2016 machine can't be restored to Windows Server 2012 R2.</span></span> <span data-ttu-id="f1c57-149">De inverse is echter mogelijk.</span><span class="sxs-lookup"><span data-stu-id="f1c57-149">However, the inverse is possible.</span></span> <span data-ttu-id="f1c57-150">U kunt back-ups van Windows Server 2012 R2 gebruiken om te herstellen van Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="f1c57-150">You can use backups from Windows Server 2012 R2 to restore Windows Server 2016.</span></span>
>

1. <span data-ttu-id="f1c57-151">Open de **Microsoft Azure Backup** -module op de *doelmachine*.</span><span class="sxs-lookup"><span data-stu-id="f1c57-151">Open the **Microsoft Azure Backup** snap-in on the *Target machine*.</span></span>
2. <span data-ttu-id="f1c57-152">Zorg ervoor dat de *doelmachine* en de *bronmachine* zijn geregistreerd bij dezelfde Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="f1c57-152">Ensure that the *Target machine* and the *Source machine* are registered to the same Recovery Services vault.</span></span>
3. <span data-ttu-id="f1c57-153">Klik op **gegevens herstellen** starten van de werkstroom.</span><span class="sxs-lookup"><span data-stu-id="f1c57-153">Click **Recover Data** to initiate the workflow.</span></span>

    ![Gegevens herstellen](./media/backup-azure-restore-windows-server-classic/recover.png)

4. <span data-ttu-id="f1c57-155">Selecteer **een andere server**</span><span class="sxs-lookup"><span data-stu-id="f1c57-155">Select **Another server**</span></span>

    ![Een andere Server](./media/backup-azure-restore-system-state/anotherserver.png)

5. <span data-ttu-id="f1c57-157">Geef het kluisreferentiebestand die overeenkomt met de *voorbeeld kluis*.</span><span class="sxs-lookup"><span data-stu-id="f1c57-157">Provide the vault credential file that corresponds to the *Sample vault*.</span></span> <span data-ttu-id="f1c57-158">Als het kluisreferentiebestand is ongeldig (of verlopen), downloadt u een nieuw kluisreferentiebestand van de *voorbeeld kluis* in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f1c57-158">If the vault credential file is invalid (or expired), download a new vault credential file from the *Sample vault* in the Azure portal.</span></span> <span data-ttu-id="f1c57-159">Zodra het kluisreferentiebestand is opgegeven, wordt de Recovery Services-kluis die is gekoppeld aan het kluisreferentiebestand weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f1c57-159">Once the vault credential file is provided, the Recovery Services vault associated with the vault credential file appears.</span></span>

6. <span data-ttu-id="f1c57-160">Selecteer in het deelvenster Selecteer back-upserver van de *bronmachine* uit de lijst met computers weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f1c57-160">On the Select Backup Server pane, select the *Source machine* from the list of displayed machines.</span></span>

    ![Lijst met computers](./media/backup-azure-restore-windows-server-classic/machinelist.png)

7. <span data-ttu-id="f1c57-162">Kies in het deelvenster herstelmodus Selecteer **systeemstatus** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="f1c57-162">On the Select Recovery Mode pane, choose **System State** and click **Next**.</span></span> 

    ![Search](./media/backup-azure-restore-system-state/recover-type-selection.png)

8. <span data-ttu-id="f1c57-164">In de kalender in het **Volume selecteert en datum** deelvenster, selecteert u een herstel verwijzen.</span><span class="sxs-lookup"><span data-stu-id="f1c57-164">On the Calendar in the **Select Volume and Date** pane, select a recovery point.</span></span> <span data-ttu-id="f1c57-165">U kunt vanaf elk willekeurig herstelpunt herstellen in de tijd.</span><span class="sxs-lookup"><span data-stu-id="f1c57-165">You can restore from any recovery point in time.</span></span> <span data-ttu-id="f1c57-166">Datums **vet** geven aan de beschikbaarheid van ten minste één herstelpunt.</span><span class="sxs-lookup"><span data-stu-id="f1c57-166">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="f1c57-167">Wanneer u een datum selecteren als er meerdere herstelpunten beschikbaar zijn, kiest u de specifieke herstelpunt in de **tijd** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="f1c57-167">Once  you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span> 

    ![Zoeken naar objecten](./media/backup-azure-restore-system-state/select-date.png)

9. <span data-ttu-id="f1c57-169">Nadat u ervoor het herstelpunt gekozen hebt te herstellen, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="f1c57-169">Once you have chosen the recovery point to restore, click **Next**.</span></span>

10. <span data-ttu-id="f1c57-170">Op de **System status herstelmodus Selecteer** deelvenster geeft u de doellocatie waar u bestanden van de systeemstatus te herstellen en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="f1c57-170">On the **Select System State Recovery Mode** pane, specify the destination where you want System State files to be recovered, then click **Next**.</span></span>

    ![Versleuteling](./media/backup-azure-restore-system-state/recover-as-files.png)

    <span data-ttu-id="f1c57-172">De optie **kopieën te maken, zodat beide versies**, maakt kopieën van afzonderlijke bestanden in een bestaande systeemstatus bestandsarchief in plaats van de kopie van het gehele archief van de systeemstatus te maken.</span><span class="sxs-lookup"><span data-stu-id="f1c57-172">The option, **Create copies so that you have both versions**, creates copies of individual files in an existing System State file archive instead of creating the copy of the entire System State archive.</span></span>

11. <span data-ttu-id="f1c57-173">Controleer de details van herstel in het deelvenster bevestiging en klik op **herstellen**.</span><span class="sxs-lookup"><span data-stu-id="f1c57-173">Verify the details of recovery on the Confirmation pane, and click **Recover**.</span></span> 

    ![Klik op de knop herstellen om te bevestigen van het herstelproces](./media/backup-azure-restore-system-state/confirm-recovery.png)

12. <span data-ttu-id="f1c57-175">Kopieer de *WindowsImageBackup* map naar een niet-kritieke volume van de server (bijvoorbeeld D:\).</span><span class="sxs-lookup"><span data-stu-id="f1c57-175">Copy the *WindowsImageBackup* directory to a non-critical volume of the server (for example D:\).</span></span> <span data-ttu-id="f1c57-176">Het Windows-besturingssysteemvolume is meestal het essentiële volume.</span><span class="sxs-lookup"><span data-stu-id="f1c57-176">Usually the Windows OS volume is the critical volume.</span></span>

13. <span data-ttu-id="f1c57-177">Gebruik de volgende sectie voor het voltooien van het herstelproces [toepassen van de herstelde bestanden van de systeemstatus op een Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server).</span><span class="sxs-lookup"><span data-stu-id="f1c57-177">To complete the recovery process, use the following section to [apply the restored System State files on a Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server).</span></span>




## <a name="apply-restored-system-state-on-a-windows-server"></a><span data-ttu-id="f1c57-178">Herstelde systeemstatus toepassen op een Windows Server</span><span class="sxs-lookup"><span data-stu-id="f1c57-178">Apply restored System State on a Windows Server</span></span>

<span data-ttu-id="f1c57-179">Eenmaal u systeemstatus als bestanden met behulp van de Azure Recovery Services Agent hebt hersteld, gebruikt u de Windows Server back-up de herstelde systeemstatus toepassen op Windows Server.</span><span class="sxs-lookup"><span data-stu-id="f1c57-179">Once you have recovered System State as files using Azure Recovery Services Agent, use the Windows Server Backup utility to apply the recovered System State to Windows Server.</span></span> <span data-ttu-id="f1c57-180">De Windows Server back-up is al beschikbaar op de server.</span><span class="sxs-lookup"><span data-stu-id="f1c57-180">The Windows Server Backup utility is already available on the server.</span></span> <span data-ttu-id="f1c57-181">De volgende stappen wordt uitgelegd hoe de status van het herstelde toepassen.</span><span class="sxs-lookup"><span data-stu-id="f1c57-181">The following steps explain how to apply the recovered System State.</span></span>

1. <span data-ttu-id="f1c57-182">Gebruik de volgende opdrachten opnieuw opstarten van uw server in *Directory Services Repair Mode*.</span><span class="sxs-lookup"><span data-stu-id="f1c57-182">Use the following commands to reboot your server in *Directory Services Repair Mode*.</span></span> <span data-ttu-id="f1c57-183">In een opdrachtprompt met verhoogde bevoegdheid:</span><span class="sxs-lookup"><span data-stu-id="f1c57-183">In an elevated command prompt:</span></span>

    ```
    PS C:\> Bcdedit /set safeboot dsrepair
    PS C:\> Shutdown /r /t 0
    ```

2. <span data-ttu-id="f1c57-184">Open de module Windows Server Backup na het opstarten.</span><span class="sxs-lookup"><span data-stu-id="f1c57-184">After the reboot, open the Windows Server Backup snap-in.</span></span> <span data-ttu-id="f1c57-185">Als u niet waar dat de module is geïnstalleerd weet, zoekt u de computer of server voor **Windows Server Backup**.</span><span class="sxs-lookup"><span data-stu-id="f1c57-185">If you don't know where the snap-in was installed, search the computer or server for **Windows Server Backup**.</span></span>

    <span data-ttu-id="f1c57-186">De bureaublad-app wordt weergegeven in de zoekresultaten.</span><span class="sxs-lookup"><span data-stu-id="f1c57-186">The desktop app appears in the search results.</span></span>

3. <span data-ttu-id="f1c57-187">Selecteer in de module **lokale back-up**.</span><span class="sxs-lookup"><span data-stu-id="f1c57-187">In the snap-in, select **Local Backup**.</span></span>

    ![Lokale back-up te herstellen vanaf daar selecteren](./media/backup-azure-restore-system-state/win-server-backup-local-backup.png)

4. <span data-ttu-id="f1c57-189">Op de lokale back-up-console in de **actiedeelvenster**, klikt u op **herstellen** om de Wizard herstel te openen.</span><span class="sxs-lookup"><span data-stu-id="f1c57-189">On the Local Backup console, in the **Actions Pane**, click **Recover** to open the Recovery Wizard.</span></span>

5. <span data-ttu-id="f1c57-190">Selecteer de optie **een back-up die is opgeslagen in een andere locatie**, en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="f1c57-190">Select the option, **A backup stored in another location**, and click **Next**.</span></span>

   ![herstellen naar een andere server kiezen](./media/backup-azure-restore-system-state/backup-stored-in-diff-location.png)

6. <span data-ttu-id="f1c57-192">Selecteer bij het opgeven van het type **externe gedeelde map** als uw back-up van systeemstatus is hersteld naar een andere server.</span><span class="sxs-lookup"><span data-stu-id="f1c57-192">When specifying the location type, select **Remote shared folder** if your System State backup was recovered to another server.</span></span> <span data-ttu-id="f1c57-193">Als de status van het systeem lokaal zijn hersteld, selecteert u **lokale stations**.</span><span class="sxs-lookup"><span data-stu-id="f1c57-193">If your System State was recovered locally, then select **Local drives**.</span></span> 

    ![Selecteer of u wilt herstellen van de lokale server of een ander](./media/backup-azure-restore-system-state/ss-recovery-remote-shared-folder.png)

7. <span data-ttu-id="f1c57-195">Geef het pad naar de *WindowsImageBackup* directory, of kies de lokale schijf met deze map (bijvoorbeeld D:\WindowsImageBackup) als onderdeel van de systeemstatus bestanden herstellen met behulp van de Azure Recovery Services Agent hersteld en klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="f1c57-195">Enter the path to the *WindowsImageBackup* directory, or choose the local drive containing this directory (for example, D:\WindowsImageBackup), recovered as part of the System State files recovery using Azure Recovery Services Agent and click **Next**.</span></span>

    ![pad naar het gedeelde bestand](./media/backup-azure-restore-system-state/ss-recovery-remote-folder.png)

8. <span data-ttu-id="f1c57-197">De systeemstatus versie selecteren die u wilt herstellen en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="f1c57-197">Select the System State version that you want to restore, and click **Next**.</span></span>

9. <span data-ttu-id="f1c57-198">Selecteer in het deelvenster Type herstelbewerking selecteren **systeemstatus** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="f1c57-198">In the Select Recovery Type pane, select **System State** and click **Next**.</span></span>

10. <span data-ttu-id="f1c57-199">Voor de locatie van de systeemstatus te herstellen, selecteert u **oorspronkelijke locatie**, en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="f1c57-199">For the location of the System State Recovery, select **Original Location**, and click **Next**.</span></span>

11. <span data-ttu-id="f1c57-200">Bekijk de details van de bevestiging, Controleer de instellingen voor opnieuw opstarten en klikt u op **herstellen** naar applly de status van het herstelde bestanden.</span><span class="sxs-lookup"><span data-stu-id="f1c57-200">Review the confirmation details, verify the reboot settings, and click **Recover** to applly the restored System State files.</span></span>

    ![Start het terugzetten van bestanden van de systeemstatus](./media/backup-azure-restore-system-state/launch-ss-recovery.png)

## <a name="special-considerations-for-system-state-recovery-on-active-directory-server"></a><span data-ttu-id="f1c57-202">Speciale overwegingen voor herstel van de systeemstatus op Active Directory-server</span><span class="sxs-lookup"><span data-stu-id="f1c57-202">Special considerations for System State recovery on Active Directory server</span></span>

<span data-ttu-id="f1c57-203">Systeemstatusback-up bevat Active Directory-gegevens.</span><span class="sxs-lookup"><span data-stu-id="f1c57-203">System State backup includes Active Directory data.</span></span> <span data-ttu-id="f1c57-204">Gebruik de volgende stappen uit om terug te zetten van Active Directory Domain Services (AD DS) van de huidige status naar een eerdere status.</span><span class="sxs-lookup"><span data-stu-id="f1c57-204">Use the following steps to restore Active Directory Domain Service (AD DS) from its current state to a previous state.</span></span>

1. <span data-ttu-id="f1c57-205">Start de domeincontroller opnieuw in de Directory Services Restore Mode (DSRM).</span><span class="sxs-lookup"><span data-stu-id="f1c57-205">Restart the domain controller in Directory Services Restore Mode (DSRM).</span></span>
2. <span data-ttu-id="f1c57-206">Volg de stappen [hier](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx) Windows Server Backup-cmdlets gebruiken om te herstellen van AD DS.</span><span class="sxs-lookup"><span data-stu-id="f1c57-206">Follow the steps [here](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx) to use Windows Server Backup cmdlets to recover AD DS.</span></span>


## <a name="troubleshoot-failed-system-state-restore"></a><span data-ttu-id="f1c57-207">Problemen met mislukte systeemstatus herstellen</span><span class="sxs-lookup"><span data-stu-id="f1c57-207">Troubleshoot failed System State restore</span></span>

<span data-ttu-id="f1c57-208">Als het vorige proces van het toepassen van de systeemstatus niet wordt voltooid, gebruikt u de Windows Herstelomgeving (Win RE) voor het herstellen van uw Windows-Server.</span><span class="sxs-lookup"><span data-stu-id="f1c57-208">If the previous process of applying System State does not complete successfully, use the Windows Recovery Environment (Win RE) to recover your Windows Server.</span></span> <span data-ttu-id="f1c57-209">De volgende stappen wordt uitgelegd hoe herstellen met behulp van Win opnieuw.</span><span class="sxs-lookup"><span data-stu-id="f1c57-209">The following steps explain how to recover using Win RE.</span></span> <span data-ttu-id="f1c57-210">Gebruik deze optie alleen als Windows Server niet normaal wordt opgestart na het terugzetten van de systeemstatus.</span><span class="sxs-lookup"><span data-stu-id="f1c57-210">Use This option only if Windows Server does not boot normally after a System State restore.</span></span> <span data-ttu-id="f1c57-211">Het volgende proces worden niet door het systeem gegevens, Wees voorzichtig gewist.</span><span class="sxs-lookup"><span data-stu-id="f1c57-211">The following process erases non-system data, use caution.</span></span> 

1. <span data-ttu-id="f1c57-212">Start op uw Windows-Server in de Windows Herstelomgeving (Windows RE).</span><span class="sxs-lookup"><span data-stu-id="f1c57-212">Boot your Windows Server into the Windows Recovery Environment (Win RE).</span></span>

2. <span data-ttu-id="f1c57-213">Selecteer oplossen van de drie beschikbare opties.</span><span class="sxs-lookup"><span data-stu-id="f1c57-213">Select Troubleshoot from the three available options.</span></span>

    ![menu openen](./media/backup-azure-restore-system-state/winre-1.png)

3. <span data-ttu-id="f1c57-215">Van de **geavanceerde opties** Schakel in het scherm **opdrachtprompt** en geef de gebruikersnaam voor de beheerder en het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="f1c57-215">From the **Advanced Options** screen, select **Command Prompt** and provide the server administrator username and password.</span></span>

   ![menu openen](./media/backup-azure-restore-system-state/winre-2.png)

4. <span data-ttu-id="f1c57-217">Geef de gebruikersnaam voor de beheerder en het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="f1c57-217">Provide the server administrator username and password.</span></span>

    ![menu openen](./media/backup-azure-restore-system-state/winre-3.png)

5. <span data-ttu-id="f1c57-219">Wanneer u de opdrachtprompt in de beheerdersmodus opent, Voer u de volgende opdracht voor het ophalen van de back-upversies systeemstatus.</span><span class="sxs-lookup"><span data-stu-id="f1c57-219">When you open the command prompt in administrator mode, run following command to get the System State backup versions.</span></span>

    ```
    Wbadmin get versions -backuptarget:<Volume where WindowsImageBackup folder is copied>:
    ```
    ![ophalen van de back-upversies systeemstatus](./media/backup-azure-restore-system-state/winre-4.png)

6. <span data-ttu-id="f1c57-221">Voer de volgende opdracht om op te halen van alle volumes die beschikbaar zijn in de back-up.</span><span class="sxs-lookup"><span data-stu-id="f1c57-221">Run the following command to get all volumes available in the backup.</span></span>

    ```
    Wbadmin get items -version:<copy version from above step> -backuptarget:<Backup volume>
    ```

    ![ophalen van de back-upversies systeemstatus](./media/backup-azure-restore-system-state/winre-5.png)

7. <span data-ttu-id="f1c57-223">De volgende opdracht wordt alle volumes die deel van de systeemstatusback-up uitmaken hersteld.</span><span class="sxs-lookup"><span data-stu-id="f1c57-223">The following command recovers all volumes that are part of the System State Backup.</span></span> <span data-ttu-id="f1c57-224">Houd er rekening mee dat deze stap alleen de essentiële volumes die deel van de systeemstatus uitmaken herstelt.</span><span class="sxs-lookup"><span data-stu-id="f1c57-224">Note that this step recovers only the critical volumes that are part of the System State.</span></span> <span data-ttu-id="f1c57-225">Alle andere gegevens worden gewist.</span><span class="sxs-lookup"><span data-stu-id="f1c57-225">All non-System data is erased.</span></span>

    ```
    Wbadmin start recovery -items:C: -itemtype:Volume -version:<Backupversion> -backuptarget:<backup target volume>
    ```
     ![ophalen van de back-upversies systeemstatus](./media/backup-azure-restore-system-state/winre-6.png)



## <a name="next-steps"></a><span data-ttu-id="f1c57-227">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f1c57-227">Next steps</span></span>
* <span data-ttu-id="f1c57-228">Nu dat u uw bestanden en mappen hebt hersteld, kunt u [beheren van uw back-ups](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="f1c57-228">Now that you've recovered your files and folders, you can [manage your backups](backup-azure-manage-windows-server.md).</span></span>
