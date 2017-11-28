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
# <a name="restore-system-state-toowindows-server"></a><span data-ttu-id="50c14-103">De systeemstatus terugzetten tooWindows Server</span><span class="sxs-lookup"><span data-stu-id="50c14-103">Restore System State tooWindows Server</span></span>

<span data-ttu-id="50c14-104">Dit artikel wordt uitgelegd hoe toorestore systeemstatus van Windows Server back-ups van een Azure Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="50c14-104">This article explains how toorestore Windows Server System State backups from an Azure Recovery Services vault.</span></span> <span data-ttu-id="50c14-105">toorestore systeemstatus, moet u een systeemstatusback-up hebben (gemaakt met behulp van instructies Hallo in [Back-up van systeemstatus](backup-azure-system-state.md#back-up-windows-server-system-state-preview)), en zorg ervoor dat u hebt geïnstalleerd Hallo [meest recente versie van Microsoft Azure Recovery Hallo Services (MARS)-agent](http://aka.ms/azurebackup_agent).</span><span class="sxs-lookup"><span data-stu-id="50c14-105">toorestore System State, you must have a System State backup (created using hello instructions in [Back up System State](backup-azure-system-state.md#back-up-windows-server-system-state-preview)), and make sure you have installed hello [latest version of hello Microsoft Azure Recovery Services (MARS) agent](http://aka.ms/azurebackup_agent).</span></span> <span data-ttu-id="50c14-106">Systeemstatus van Windows Server-gegevens herstellen vanaf een Azure Recovery Services-kluis is een proces in twee stappen:</span><span class="sxs-lookup"><span data-stu-id="50c14-106">Recovering Windows Server System State data from an Azure Recovery Services vault is a two-step process:</span></span>

1. <span data-ttu-id="50c14-107">Systeemstatus terugzetten als bestanden vanuit Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="50c14-107">Restore System State as files from Azure Backup.</span></span> <span data-ttu-id="50c14-108">Bij het herstellen van systeemstatus als bestanden vanuit Azure Backup, kunt u:</span><span class="sxs-lookup"><span data-stu-id="50c14-108">When restoring System State as files from Azure Backup, you can either:</span></span>
  * <span data-ttu-id="50c14-109">De systeemstatus terugzetten toohello dezelfde server waar Hallo back-ups zijn gemaakt, of</span><span class="sxs-lookup"><span data-stu-id="50c14-109">Restore System State toohello same server where hello backups were taken, or</span></span>
  * <span data-ttu-id="50c14-110">De systeemstatus terugzetten tooan alternatieve bestandsserver.</span><span class="sxs-lookup"><span data-stu-id="50c14-110">Restore System State file tooan alternate server.</span></span>

2. <span data-ttu-id="50c14-111">Toepassing hello hersteld systeemstatus bestanden tooa Windows Server.</span><span class="sxs-lookup"><span data-stu-id="50c14-111">Apply hello restored System State files tooa Windows Server.</span></span>


## <a name="recover-system-state-files-toohello-same-server"></a><span data-ttu-id="50c14-112">Systeemstatus herstellen bestanden toohello dezelfde server</span><span class="sxs-lookup"><span data-stu-id="50c14-112">Recover System State files toohello same server</span></span>
<span data-ttu-id="50c14-113">Hallo stappen wordt uitgelegd hoe tooroll uw vorige status van Windows Server-configuratie tooa reservekopieën.</span><span class="sxs-lookup"><span data-stu-id="50c14-113">hello following steps explain how tooroll back your Windows Server configuration tooa previous state.</span></span> <span data-ttu-id="50c14-114">Configuratie back tooa bekend, stabiele status van uw server rolling kan zeer waardevol zijn.</span><span class="sxs-lookup"><span data-stu-id="50c14-114">Rolling your server configuration back tooa known, stable state, can be extremely valuable.</span></span> <span data-ttu-id="50c14-115">Hallo volgende systeemstatus stappen terugzetten Hallo van server uit een Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="50c14-115">hello following steps restore hello server's System State from a Recovery Services vault.</span></span> 

1. <span data-ttu-id="50c14-116">Open Hallo **Microsoft Azure Backup** -module.</span><span class="sxs-lookup"><span data-stu-id="50c14-116">Open hello **Microsoft Azure Backup** snap-in.</span></span> <span data-ttu-id="50c14-117">Als u niet waar de Hallo-module is geïnstalleerd weet, zoekt u Hallo computer of server voor **Microsoft Azure Backup**.</span><span class="sxs-lookup"><span data-stu-id="50c14-117">If you don't know where hello snap-in was installed, search hello computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="50c14-118">Hallo bureaublad-app moet worden weergegeven in zoekresultaten Hallo.</span><span class="sxs-lookup"><span data-stu-id="50c14-118">hello desktop app should appear in hello search results.</span></span>

2. <span data-ttu-id="50c14-119">Klik op **gegevens herstellen** toostart Hallo-wizard.</span><span class="sxs-lookup"><span data-stu-id="50c14-119">Click **Recover Data** toostart hello wizard.</span></span>

    ![Gegevens herstellen](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="50c14-121">Op Hallo **aan de slag** deelvenster, toorestore Hallo gegevens toohello dezelfde server of computer, selecteer **deze server (`<server name>`)** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="50c14-121">On hello **Getting Started** pane, toorestore hello data toohello same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![Kies deze server optie toorestore Hallo gegevens toohello dezelfde machine](./media/backup-azure-restore-system-state/samemachine.png)

4. <span data-ttu-id="50c14-123">Op Hallo **herstelmodus Selecteer** deelvenster kiezen **systeemstatus** en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="50c14-123">On hello **Select Recovery Mode** pane, choose **System State** and then click **Next**.</span></span>

    ![Blader door bestanden](./media/backup-azure-restore-system-state/recover-type-selection.png)

5. <span data-ttu-id="50c14-125">In de agenda Hallo van **Volume selecteert en datum** deelvenster, selecteert u een herstel verwijzen.</span><span class="sxs-lookup"><span data-stu-id="50c14-125">On hello calendar in **Select Volume and Date** pane, select a recovery point.</span></span> 

    <span data-ttu-id="50c14-126">U kunt vanaf elk willekeurig herstelpunt herstellen in de tijd.</span><span class="sxs-lookup"><span data-stu-id="50c14-126">You can restore from any recovery point in time.</span></span> <span data-ttu-id="50c14-127">Datums **vet** Hallo beschikbaarheid van ten minste één herstelpunt aangeven.</span><span class="sxs-lookup"><span data-stu-id="50c14-127">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="50c14-128">Wanneer u een datum selecteren als er meerdere herstelpunten beschikbaar zijn, kiest u Hallo specifiek herstelpunt van Hallo **tijd** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="50c14-128">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![Volume en datum](./media/backup-azure-restore-system-state/select-date.png)

6. <span data-ttu-id="50c14-130">Nadat u Hallo herstel punt toorestore hebt gekozen, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="50c14-130">Once you have chosen hello recovery point toorestore, click **Next**.</span></span>

    <span data-ttu-id="50c14-131">Azure Backup Hallo lokale herstelpunt koppelt en gebruikt als een volume herstel.</span><span class="sxs-lookup"><span data-stu-id="50c14-131">Azure Backup mounts hello local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="50c14-132">Geef Hallo bestemming voor Hallo herstelde bestanden van de systeemstatus op Hallo Volgend deelvenster, en klik op **Bladeren** tooopen Windows Verkenner en zoek Hallo bestanden en mappen die u wilt.</span><span class="sxs-lookup"><span data-stu-id="50c14-132">On hello next pane, specify hello destination for hello recovered System State files and click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span> <span data-ttu-id="50c14-133">Hallo-optie **kopieën te maken, zodat beide versies**, maakt kopieën van afzonderlijke bestanden in een bestaande systeemstatus bestandsarchief in plaats van Hallo kopie van het gehele systeemstatus archief Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="50c14-133">hello option, **Create copies so that you have both versions**, creates copies of individual files in an existing System State file archive instead of creating hello copy of hello entire System State archive.</span></span>

    ![Opties voor herstel](./media/backup-azure-restore-system-state/recover-as-files.png)

8. <span data-ttu-id="50c14-135">Controleer de gegevens van herstel op Hallo van Hallo **bevestiging** deelvenster en klik op **herstellen**.</span><span class="sxs-lookup"><span data-stu-id="50c14-135">Verify hello details of recovery on hello **Confirmation** pane and click **Recover**.</span></span>

   ![Klik op herstellen tooacknowledge Hallo herstellen actie](./media/backup-azure-restore-system-state/confirm-recovery.png)

9. <span data-ttu-id="50c14-137">Kopiëren Hallo *WindowsImageBackup* map in Hallo herstel tooa niet-kritieke doelvolume van Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="50c14-137">Copy hello *WindowsImageBackup* directory in hello Recovery destination tooa non-critical volume of hello server.</span></span> <span data-ttu-id="50c14-138">Meestal is Hallo volume met het besturingssysteem Windows hello essentieel volume.</span><span class="sxs-lookup"><span data-stu-id="50c14-138">Usually, hello Windows OS volume is hello critical volume.</span></span>

10. <span data-ttu-id="50c14-139">Wanneer Hallo herstel voltooid is, stappen Hallo in sectie Hallo [toepassen hersteld systeemstatus bestanden toohello Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server), toocomplete Hallo systeemstatus herstelproces.</span><span class="sxs-lookup"><span data-stu-id="50c14-139">Once hello recovery is successful, follow hello steps in hello section, [Apply restored System State files toohello Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server), toocomplete hello System State recovery process.</span></span>

## <a name="recover-system-state-files-tooan-alternate-server"></a><span data-ttu-id="50c14-140">Systeemstatus herstellen bestanden tooan alternatieve server</span><span class="sxs-lookup"><span data-stu-id="50c14-140">Recover System State files tooan alternate server</span></span>

<span data-ttu-id="50c14-141">Als uw Windows-Server beschadigd of niet toegankelijk is en u toorestore wilt het tooa stabiele status door het herstellen van Windows Server System State Hallo, kunt u Hallo beschadigd server systeemstatus terugzetten vanaf een andere server.</span><span class="sxs-lookup"><span data-stu-id="50c14-141">If your Windows Server is corrupted or inaccessible, and you want toorestore it tooa stable state by recovering hello Windows Server System State, you can restore hello corrupted server's System State from another server.</span></span> <span data-ttu-id="50c14-142">Hallo stappen toohello terugzetten systeemstatus volgen op een afzonderlijke server gebruiken.</span><span class="sxs-lookup"><span data-stu-id="50c14-142">Use hello following steps toohello restore System State on a separate server.</span></span>  

<span data-ttu-id="50c14-143">Hallo-terminologie die wordt gebruikt in deze stap omvat het volgende:</span><span class="sxs-lookup"><span data-stu-id="50c14-143">hello terminology used in these steps includes:</span></span>

- <span data-ttu-id="50c14-144">*Bronmachine* : de oorspronkelijke machine Hallo van welke Hallo back-up is gemaakt en die momenteel niet beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="50c14-144">*Source machine* – hello original machine from which hello backup was taken and which is currently unavailable.</span></span>
- <span data-ttu-id="50c14-145">*Doelcomputer* – Hallo machine toowhich Hallo gegevens worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="50c14-145">*Target machine* – hello machine toowhich hello data is being recovered.</span></span>
- <span data-ttu-id="50c14-146">*Voorbeeld kluis* – Hallo Recovery Services-kluis toowhich hello *bronmachine* en *doelmachine* zijn geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="50c14-146">*Sample vault* – hello Recovery Services vault toowhich hello *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="50c14-147">Back-ups die afkomstig zijn uit één machine kunnen niet herstelde tooa machine met een eerdere versie van besturingssysteem Hallo.</span><span class="sxs-lookup"><span data-stu-id="50c14-147">Backups taken from one machine cannot be restored tooa machine running an earlier version of hello operating system.</span></span> <span data-ttu-id="50c14-148">Back-ups die afkomstig zijn uit een Windows Server 2016-computer kan niet worden hersteld bijvoorbeeld tooWindows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="50c14-148">For example, backups taken from a Windows Server 2016 machine can't be restored tooWindows Server 2012 R2.</span></span> <span data-ttu-id="50c14-149">Hallo inverse is echter mogelijk.</span><span class="sxs-lookup"><span data-stu-id="50c14-149">However, hello inverse is possible.</span></span> <span data-ttu-id="50c14-150">U kunt back-ups van Windows Server 2012 R2 toorestore Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="50c14-150">You can use backups from Windows Server 2012 R2 toorestore Windows Server 2016.</span></span>
>

1. <span data-ttu-id="50c14-151">Open Hallo **Microsoft Azure Backup** -module op Hallo *doelmachine*.</span><span class="sxs-lookup"><span data-stu-id="50c14-151">Open hello **Microsoft Azure Backup** snap-in on hello *Target machine*.</span></span>
2. <span data-ttu-id="50c14-152">Zorg ervoor dat Hallo *doelmachine* en Hallo *bronmachine* zijn geregistreerde toohello dezelfde Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="50c14-152">Ensure that hello *Target machine* and hello *Source machine* are registered toohello same Recovery Services vault.</span></span>
3. <span data-ttu-id="50c14-153">Klik op **gegevens herstellen** tooinitiate Hallo werkstroom.</span><span class="sxs-lookup"><span data-stu-id="50c14-153">Click **Recover Data** tooinitiate hello workflow.</span></span>

    ![Gegevens herstellen](./media/backup-azure-restore-windows-server-classic/recover.png)

4. <span data-ttu-id="50c14-155">Selecteer **een andere server**</span><span class="sxs-lookup"><span data-stu-id="50c14-155">Select **Another server**</span></span>

    ![Een andere Server](./media/backup-azure-restore-system-state/anotherserver.png)

5. <span data-ttu-id="50c14-157">Hallo-kluisreferentiebestand die overeenkomt met toohello bieden *voorbeeld kluis*.</span><span class="sxs-lookup"><span data-stu-id="50c14-157">Provide hello vault credential file that corresponds toohello *Sample vault*.</span></span> <span data-ttu-id="50c14-158">Als het kluisreferentiebestand Hallo is ongeldig (of verlopen), het downloaden van een nieuw kluisreferentiebestand van Hallo *voorbeeld kluis* in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="50c14-158">If hello vault credential file is invalid (or expired), download a new vault credential file from hello *Sample vault* in hello Azure portal.</span></span> <span data-ttu-id="50c14-159">Zodra het Hallo-kluisreferentiebestand is opgegeven, wordt Hallo Recovery Services-kluis die is gekoppeld aan het kluisreferentiebestand Hallo weergegeven.</span><span class="sxs-lookup"><span data-stu-id="50c14-159">Once hello vault credential file is provided, hello Recovery Services vault associated with hello vault credential file appears.</span></span>

6. <span data-ttu-id="50c14-160">Selecteer op Hallo Selecteer back-upserver deelvenster Hallo *bronmachine* uit Hallo lijst met computers weergegeven.</span><span class="sxs-lookup"><span data-stu-id="50c14-160">On hello Select Backup Server pane, select hello *Source machine* from hello list of displayed machines.</span></span>

    ![Lijst met computers](./media/backup-azure-restore-windows-server-classic/machinelist.png)

7. <span data-ttu-id="50c14-162">Kies op Hallo herstelmodus Selecteer deelvenster **systeemstatus** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="50c14-162">On hello Select Recovery Mode pane, choose **System State** and click **Next**.</span></span> 

    ![Search](./media/backup-azure-restore-system-state/recover-type-selection.png)

8. <span data-ttu-id="50c14-164">Op Hallo kalender in Hallo **Volume selecteert en datum** deelvenster, selecteert u een herstel verwijzen.</span><span class="sxs-lookup"><span data-stu-id="50c14-164">On hello Calendar in hello **Select Volume and Date** pane, select a recovery point.</span></span> <span data-ttu-id="50c14-165">U kunt vanaf elk willekeurig herstelpunt herstellen in de tijd.</span><span class="sxs-lookup"><span data-stu-id="50c14-165">You can restore from any recovery point in time.</span></span> <span data-ttu-id="50c14-166">Datums **vet** Hallo beschikbaarheid van ten minste één herstelpunt aangeven.</span><span class="sxs-lookup"><span data-stu-id="50c14-166">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="50c14-167">Wanneer u een datum selecteren als er meerdere herstelpunten beschikbaar zijn, kiest u Hallo specifiek herstelpunt van Hallo **tijd** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="50c14-167">Once  you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span> 

    ![Zoeken naar objecten](./media/backup-azure-restore-system-state/select-date.png)

9. <span data-ttu-id="50c14-169">Nadat u Hallo herstel punt toorestore hebt gekozen, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="50c14-169">Once you have chosen hello recovery point toorestore, click **Next**.</span></span>

10. <span data-ttu-id="50c14-170">Op Hallo **System status herstelmodus Selecteer** deelvenster Hallo bestemming waar u de systeemstatus bestanden hersteld toobe wilt opgeven en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="50c14-170">On hello **Select System State Recovery Mode** pane, specify hello destination where you want System State files toobe recovered, then click **Next**.</span></span>

    ![Versleuteling](./media/backup-azure-restore-system-state/recover-as-files.png)

    <span data-ttu-id="50c14-172">Hallo-optie **kopieën te maken, zodat beide versies**, maakt kopieën van afzonderlijke bestanden in een bestaande systeemstatus bestandsarchief in plaats van Hallo kopie van het gehele systeemstatus archief Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="50c14-172">hello option, **Create copies so that you have both versions**, creates copies of individual files in an existing System State file archive instead of creating hello copy of hello entire System State archive.</span></span>

11. <span data-ttu-id="50c14-173">Controleer de details op Hallo van herstel op Hallo bevestiging deelvenster en op **herstellen**.</span><span class="sxs-lookup"><span data-stu-id="50c14-173">Verify hello details of recovery on hello Confirmation pane, and click **Recover**.</span></span> 

    ![Klik op Hallo herstellen knop tooconfirm Hallo herstelproces](./media/backup-azure-restore-system-state/confirm-recovery.png)

12. <span data-ttu-id="50c14-175">Kopiëren Hallo *WindowsImageBackup* directory tooa niet-kritieke volume van Hallo-server (bijvoorbeeld D:\).</span><span class="sxs-lookup"><span data-stu-id="50c14-175">Copy hello *WindowsImageBackup* directory tooa non-critical volume of hello server (for example D:\).</span></span> <span data-ttu-id="50c14-176">Meestal is Hallo volume met het besturingssysteem Windows hello essentieel volume.</span><span class="sxs-lookup"><span data-stu-id="50c14-176">Usually hello Windows OS volume is hello critical volume.</span></span>

13. <span data-ttu-id="50c14-177">Hallo herstelproces toocomplete gebruik Hallo volgende sectie te[toepassing hello hersteld systeemstatus bestanden op een Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server).</span><span class="sxs-lookup"><span data-stu-id="50c14-177">toocomplete hello recovery process, use hello following section too[apply hello restored System State files on a Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server).</span></span>




## <a name="apply-restored-system-state-on-a-windows-server"></a><span data-ttu-id="50c14-178">Herstelde systeemstatus toepassen op een Windows Server</span><span class="sxs-lookup"><span data-stu-id="50c14-178">Apply restored System State on a Windows Server</span></span>

<span data-ttu-id="50c14-179">Wanneer u de systeemstatus als bestanden met behulp van de Azure Recovery Services Agent hebt hersteld, hersteld gebruik Hallo Windows Server Backup hulpprogramma tooapply Hallo systeemstatus tooWindows Server.</span><span class="sxs-lookup"><span data-stu-id="50c14-179">Once you have recovered System State as files using Azure Recovery Services Agent, use hello Windows Server Backup utility tooapply hello recovered System State tooWindows Server.</span></span> <span data-ttu-id="50c14-180">Hallo Windows Server back-up is al beschikbaar op Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="50c14-180">hello Windows Server Backup utility is already available on hello server.</span></span> <span data-ttu-id="50c14-181">Hallo stappen wordt uitgelegd hoe tooapply Hallo systeemstatus hersteld.</span><span class="sxs-lookup"><span data-stu-id="50c14-181">hello following steps explain how tooapply hello recovered System State.</span></span>

1. <span data-ttu-id="50c14-182">Uw server in de opdrachten tooreboot gebruik Hallo volgende *Directory Services Repair Mode*.</span><span class="sxs-lookup"><span data-stu-id="50c14-182">Use hello following commands tooreboot your server in *Directory Services Repair Mode*.</span></span> <span data-ttu-id="50c14-183">In een opdrachtprompt met verhoogde bevoegdheid:</span><span class="sxs-lookup"><span data-stu-id="50c14-183">In an elevated command prompt:</span></span>

    ```
    PS C:\> Bcdedit /set safeboot dsrepair
    PS C:\> Shutdown /r /t 0
    ```

2. <span data-ttu-id="50c14-184">Na opnieuw opstarten hello, Hallo Windows Server Backup-module openen.</span><span class="sxs-lookup"><span data-stu-id="50c14-184">After hello reboot, open hello Windows Server Backup snap-in.</span></span> <span data-ttu-id="50c14-185">Als u niet waar de Hallo-module is geïnstalleerd weet, zoekt u Hallo computer of server voor **Windows Server Backup**.</span><span class="sxs-lookup"><span data-stu-id="50c14-185">If you don't know where hello snap-in was installed, search hello computer or server for **Windows Server Backup**.</span></span>

    <span data-ttu-id="50c14-186">Hallo bureaublad-app wordt weergegeven in zoekresultaten Hallo.</span><span class="sxs-lookup"><span data-stu-id="50c14-186">hello desktop app appears in hello search results.</span></span>

3. <span data-ttu-id="50c14-187">Selecteer in de module Hallo **lokale back-up**.</span><span class="sxs-lookup"><span data-stu-id="50c14-187">In hello snap-in, select **Local Backup**.</span></span>

    ![Selecteer toorestore lokale back-up van daaruit](./media/backup-azure-restore-system-state/win-server-backup-local-backup.png)

4. <span data-ttu-id="50c14-189">Op Hallo lokale back-up-console in Hallo **actiedeelvenster**, klikt u op **herstellen** tooopen Hallo Wizard herstel.</span><span class="sxs-lookup"><span data-stu-id="50c14-189">On hello Local Backup console, in hello **Actions Pane**, click **Recover** tooopen hello Recovery Wizard.</span></span>

5. <span data-ttu-id="50c14-190">Hallo optie selecteert, **een back-up die is opgeslagen in een andere locatie**, en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="50c14-190">Select hello option, **A backup stored in another location**, and click **Next**.</span></span>

   ![Kies toorecover tooa andere server](./media/backup-azure-restore-system-state/backup-stored-in-diff-location.png)

6. <span data-ttu-id="50c14-192">Wanneer u opgeeft locatietype hello, selecteer **externe gedeelde map** als uw back-up van systeemstatus herstelde tooanother-server.</span><span class="sxs-lookup"><span data-stu-id="50c14-192">When specifying hello location type, select **Remote shared folder** if your System State backup was recovered tooanother server.</span></span> <span data-ttu-id="50c14-193">Als de status van het systeem lokaal zijn hersteld, selecteert u **lokale stations**.</span><span class="sxs-lookup"><span data-stu-id="50c14-193">If your System State was recovered locally, then select **Local drives**.</span></span> 

    ![Selecteer of toorecovery van de lokale server of een ander](./media/backup-azure-restore-system-state/ss-recovery-remote-shared-folder.png)

7. <span data-ttu-id="50c14-195">Voer Hallo pad toohello *WindowsImageBackup* directory, of kies Hallo lokale schijf met deze map (bijvoorbeeld D:\WindowsImageBackup) als onderdeel van Hallo bestanden systeemstatusherstel met Azure Recovery hersteld Services-Agent en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="50c14-195">Enter hello path toohello *WindowsImageBackup* directory, or choose hello local drive containing this directory (for example, D:\WindowsImageBackup), recovered as part of hello System State files recovery using Azure Recovery Services Agent and click **Next**.</span></span>

    ![pad toohello gedeeld bestand](./media/backup-azure-restore-system-state/ss-recovery-remote-folder.png)

8. <span data-ttu-id="50c14-197">Selecteer Hallo systeemstatus versie toorestore wilt en klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="50c14-197">Select hello System State version that you want toorestore, and click **Next**.</span></span>

9. <span data-ttu-id="50c14-198">Selecteer in het deelvenster Hallo Type herstelbewerking selecteren **systeemstatus** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="50c14-198">In hello Select Recovery Type pane, select **System State** and click **Next**.</span></span>

10. <span data-ttu-id="50c14-199">Hallo-locatie van Hallo systeemstatusherstel, selecteert u **oorspronkelijke locatie**, en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="50c14-199">For hello location of hello System State Recovery, select **Original Location**, and click **Next**.</span></span>

11. <span data-ttu-id="50c14-200">Bekijk de details van Hallo bevestiging, Controleer de instellingen voor opnieuw opstarten Hallo en op **herstellen** tooapplly Hallo systeemstatus bestanden hersteld.</span><span class="sxs-lookup"><span data-stu-id="50c14-200">Review hello confirmation details, verify hello reboot settings, and click **Recover** tooapplly hello restored System State files.</span></span>

    ![Start Hallo bestanden van de systeemstatus herstellen](./media/backup-azure-restore-system-state/launch-ss-recovery.png)

## <a name="special-considerations-for-system-state-recovery-on-active-directory-server"></a><span data-ttu-id="50c14-202">Speciale overwegingen voor herstel van de systeemstatus op Active Directory-server</span><span class="sxs-lookup"><span data-stu-id="50c14-202">Special considerations for System State recovery on Active Directory server</span></span>

<span data-ttu-id="50c14-203">Systeemstatusback-up bevat Active Directory-gegevens.</span><span class="sxs-lookup"><span data-stu-id="50c14-203">System State backup includes Active Directory data.</span></span> <span data-ttu-id="50c14-204">Volgende stappen toorestore Active Directory Domain Services (AD DS) uit de vorige status van huidige status tooa hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="50c14-204">Use hello following steps toorestore Active Directory Domain Service (AD DS) from its current state tooa previous state.</span></span>

1. <span data-ttu-id="50c14-205">Start Hallo-domeincontroller in de Directory Services Restore Mode (DSRM).</span><span class="sxs-lookup"><span data-stu-id="50c14-205">Restart hello domain controller in Directory Services Restore Mode (DSRM).</span></span>
2. <span data-ttu-id="50c14-206">Volg de stappen Hallo [hier](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx) toouse Windows Server Backup cmdlets toorecover AD DS.</span><span class="sxs-lookup"><span data-stu-id="50c14-206">Follow hello steps [here](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx) toouse Windows Server Backup cmdlets toorecover AD DS.</span></span>


## <a name="troubleshoot-failed-system-state-restore"></a><span data-ttu-id="50c14-207">Problemen met mislukte systeemstatus herstellen</span><span class="sxs-lookup"><span data-stu-id="50c14-207">Troubleshoot failed System State restore</span></span>

<span data-ttu-id="50c14-208">Als Hallo vorige proces van het toepassen van de systeemstatus niet wordt voltooid, gebruikt u Hallo Windows Recovery Environment (Win RE) toorecover uw Windows-Server.</span><span class="sxs-lookup"><span data-stu-id="50c14-208">If hello previous process of applying System State does not complete successfully, use hello Windows Recovery Environment (Win RE) toorecover your Windows Server.</span></span> <span data-ttu-id="50c14-209">Hallo volgende stappen wordt uitgelegd hoe toorecover Win opnieuw gebruiken.</span><span class="sxs-lookup"><span data-stu-id="50c14-209">hello following steps explain how toorecover using Win RE.</span></span> <span data-ttu-id="50c14-210">Gebruik deze optie alleen als Windows Server niet normaal wordt opgestart na het terugzetten van de systeemstatus.</span><span class="sxs-lookup"><span data-stu-id="50c14-210">Use This option only if Windows Server does not boot normally after a System State restore.</span></span> <span data-ttu-id="50c14-211">Hallo na systeembestanden gegevens, Wees voorzichtig worden gewist.</span><span class="sxs-lookup"><span data-stu-id="50c14-211">hello following process erases non-system data, use caution.</span></span> 

1. <span data-ttu-id="50c14-212">Start op uw Windows-Server in Hallo Windows Recovery Environment (Win RE).</span><span class="sxs-lookup"><span data-stu-id="50c14-212">Boot your Windows Server into hello Windows Recovery Environment (Win RE).</span></span>

2. <span data-ttu-id="50c14-213">Selecteer oplossen in Hallo drie opties.</span><span class="sxs-lookup"><span data-stu-id="50c14-213">Select Troubleshoot from hello three available options.</span></span>

    ![menu openen](./media/backup-azure-restore-system-state/winre-1.png)

3. <span data-ttu-id="50c14-215">Van Hallo **geavanceerde opties** Schakel in het scherm **opdrachtprompt** en Hallo beheerder gebruikersnaam en wachtwoord opgeven.</span><span class="sxs-lookup"><span data-stu-id="50c14-215">From hello **Advanced Options** screen, select **Command Prompt** and provide hello server administrator username and password.</span></span>

   ![menu openen](./media/backup-azure-restore-system-state/winre-2.png)

4. <span data-ttu-id="50c14-217">Hallo server-beheerder gebruikersnaam en wachtwoord opgeven.</span><span class="sxs-lookup"><span data-stu-id="50c14-217">Provide hello server administrator username and password.</span></span>

    ![menu openen](./media/backup-azure-restore-system-state/winre-3.png)

5. <span data-ttu-id="50c14-219">Wanneer u Hallo-opdrachtprompt in de beheerdersmodus openen, voert u de volgende opdracht tooget Hallo systeemstatus back-versies.</span><span class="sxs-lookup"><span data-stu-id="50c14-219">When you open hello command prompt in administrator mode, run following command tooget hello System State backup versions.</span></span>

    ```
    Wbadmin get versions -backuptarget:<Volume where WindowsImageBackup folder is copied>:
    ```
    ![ophalen van de back-upversies systeemstatus](./media/backup-azure-restore-system-state/winre-4.png)

6. <span data-ttu-id="50c14-221">Hallo opdracht tooget na alle volumes die beschikbaar zijn in Hallo back-up uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="50c14-221">Run hello following command tooget all volumes available in hello backup.</span></span>

    ```
    Wbadmin get items -version:<copy version from above step> -backuptarget:<Backup volume>
    ```

    ![ophalen van de back-upversies systeemstatus](./media/backup-azure-restore-system-state/winre-5.png)

7. <span data-ttu-id="50c14-223">Hallo herstelt volgende opdracht alle volumes die deel van Hallo systeemstatusback-up uitmaken.</span><span class="sxs-lookup"><span data-stu-id="50c14-223">hello following command recovers all volumes that are part of hello System State Backup.</span></span> <span data-ttu-id="50c14-224">Houd er rekening mee dat deze stap alleen Hallo essentiële volumes die deel van de systeemstatus Hallo uitmaken herstelt.</span><span class="sxs-lookup"><span data-stu-id="50c14-224">Note that this step recovers only hello critical volumes that are part of hello System State.</span></span> <span data-ttu-id="50c14-225">Alle andere gegevens worden gewist.</span><span class="sxs-lookup"><span data-stu-id="50c14-225">All non-System data is erased.</span></span>

    ```
    Wbadmin start recovery -items:C: -itemtype:Volume -version:<Backupversion> -backuptarget:<backup target volume>
    ```
     ![ophalen van de back-upversies systeemstatus](./media/backup-azure-restore-system-state/winre-6.png)



## <a name="next-steps"></a><span data-ttu-id="50c14-227">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="50c14-227">Next steps</span></span>
* <span data-ttu-id="50c14-228">Nu dat u uw bestanden en mappen hebt hersteld, kunt u [beheren van uw back-ups](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="50c14-228">Now that you've recovered your files and folders, you can [manage your backups](backup-azure-manage-windows-server.md).</span></span>
