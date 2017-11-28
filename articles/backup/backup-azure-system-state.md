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
# <a name="back-up-windows-system-state-in-resource-manager-deployment"></a><span data-ttu-id="97549-104">Back-up van systeemstatus Windows in de implementatie van Resource Manager</span><span class="sxs-lookup"><span data-stu-id="97549-104">Back up Windows system state in Resource Manager deployment</span></span>
<span data-ttu-id="97549-105">Dit artikel wordt uitgelegd hoe tooback uw Windows Server-systeem tooAzure status.</span><span class="sxs-lookup"><span data-stu-id="97549-105">This article explains how tooback up your Windows Server system state tooAzure.</span></span> <span data-ttu-id="97549-106">Het is een zelfstudie beoogde toowalk u bij het Hallo-basisbeginselen.</span><span class="sxs-lookup"><span data-stu-id="97549-106">It's a tutorial intended toowalk you through hello basics.</span></span>

<span data-ttu-id="97549-107">Als u tooknow meer informatie over Azure Backup wilt, Lees dit [overzicht](backup-introduction-to-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="97549-107">If you want tooknow more about Azure Backup, read this [overview](backup-introduction-to-azure-backup.md).</span></span>

<span data-ttu-id="97549-108">Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/) aan waarmee u toegang hebt tot alle services van Azure.</span><span class="sxs-lookup"><span data-stu-id="97549-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) that lets you access any Azure service.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="97549-109">Een Recovery Services-kluis maken</span><span class="sxs-lookup"><span data-stu-id="97549-109">Create a recovery services vault</span></span>
<span data-ttu-id="97549-110">tooback van uw bestanden en mappen, moet u een Recovery Services-kluis in Hallo regio waar u toostore Hallo gegevens toocreate.</span><span class="sxs-lookup"><span data-stu-id="97549-110">tooback up your files and folders, you need toocreate a Recovery Services vault in hello region where you want toostore hello data.</span></span> <span data-ttu-id="97549-111">U moet ook toodetermine hoe u uw opslag repliceren wilt.</span><span class="sxs-lookup"><span data-stu-id="97549-111">You also need toodetermine how you want your storage replicated.</span></span>

### <a name="toocreate-a-recovery-services-vault"></a><span data-ttu-id="97549-112">toocreate een Recovery Services-kluis</span><span class="sxs-lookup"><span data-stu-id="97549-112">toocreate a Recovery Services vault</span></span>
1. <span data-ttu-id="97549-113">Als u dit nog niet hebt gedaan, meld u aan toohello [Azure Portal](https://portal.azure.com/) met behulp van uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="97549-113">If you haven't already done so, sign in toohello [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="97549-114">Klik op het menu Hub Hallo **meer services** en typt u in de lijst met resources Hallo **Recovery Services** en klik op **Recovery Services-kluizen**.</span><span class="sxs-lookup"><span data-stu-id="97549-114">On hello Hub menu, click **More services** and in hello list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Een Recovery Services-kluis maken, stap 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="97549-116">Als er recovery services-kluizen in Hallo abonnement, worden Hallo kluizen weergegeven.</span><span class="sxs-lookup"><span data-stu-id="97549-116">If there are recovery services vaults in hello subscription, hello vaults are listed.</span></span>
3. <span data-ttu-id="97549-117">Op Hallo **Recovery Services-kluizen** menu, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="97549-117">On hello **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Een Recovery Services-kluis maken, stap 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="97549-119">Hallo Recovery Services vault blade wordt geopend, waarin u wordt gevraagd tooprovide een **naam**, **abonnement**, **resourcegroep**, en **locatie**.</span><span class="sxs-lookup"><span data-stu-id="97549-119">hello Recovery Services vault blade opens, prompting you tooprovide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Een Recovery Services-kluis maken, stap 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="97549-121">Voor **naam**, voer een beschrijvende naam tooidentify Hallo-kluis.</span><span class="sxs-lookup"><span data-stu-id="97549-121">For **Name**, enter a friendly name tooidentify hello vault.</span></span> <span data-ttu-id="97549-122">de naam van de Hallo moet toobe unieke voor hello Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="97549-122">hello name needs toobe unique for hello Azure subscription.</span></span> <span data-ttu-id="97549-123">Typ een naam die tussen 2 en 50 tekens bevat.</span><span class="sxs-lookup"><span data-stu-id="97549-123">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="97549-124">De naam moet beginnen met een letter en mag alleen letters, cijfers en afbreekstreepjes bevatten.</span><span class="sxs-lookup"><span data-stu-id="97549-124">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="97549-125">In Hallo **abonnement** sectie, gebruikt u Hallo vervolgkeuzelijst toochoose hello Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="97549-125">In hello **Subscription** section, use hello drop-down menu toochoose hello Azure subscription.</span></span> <span data-ttu-id="97549-126">Als u slechts één abonnement, dat abonnement wordt weergegeven en kunt u de volgende stap toohello overslaan.</span><span class="sxs-lookup"><span data-stu-id="97549-126">If you use only one subscription, that subscription appears and you can skip toohello next step.</span></span> <span data-ttu-id="97549-127">Als u niet zeker weet welk abonnement toouse Hallo standaard gebruiken (of voorgestelde) abonnement.</span><span class="sxs-lookup"><span data-stu-id="97549-127">If you are not sure which subscription toouse, use hello default (or suggested) subscription.</span></span> <span data-ttu-id="97549-128">Er zijn alleen meerdere mogelijkheden als uw organisatieaccount is gekoppeld aan meerdere Azure-abonnementen.</span><span class="sxs-lookup"><span data-stu-id="97549-128">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="97549-129">In Hallo **resourcegroep** sectie:</span><span class="sxs-lookup"><span data-stu-id="97549-129">In hello **Resource group** section:</span></span>

    * <span data-ttu-id="97549-130">Selecteer **nieuw** als u wilt dat toocreate een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="97549-130">select **Create new** if you want toocreate a Resource group.</span></span>
    <span data-ttu-id="97549-131">of</span><span class="sxs-lookup"><span data-stu-id="97549-131">Or</span></span>
    * <span data-ttu-id="97549-132">Selecteer **gebruik bestaande** en klik op Hallo vervolgkeuzelijst toosee Hallo lijst met beschikbare resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="97549-132">select **Use existing** and click hello drop-down menu toosee hello available list of Resource groups.</span></span>

  <span data-ttu-id="97549-133">Zie voor meer informatie over resourcegroepen Hallo [overzicht van Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="97549-133">For complete information on Resource groups, see hello [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="97549-134">Klik op **locatie** tooselect Hallo geografische regio voor Hallo kluis.</span><span class="sxs-lookup"><span data-stu-id="97549-134">Click **Location** tooselect hello geographic region for hello vault.</span></span> <span data-ttu-id="97549-135">Deze keuze bepaalt Hallo geografische regio waar uw back-upgegevens worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="97549-135">This choice determines hello geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="97549-136">Aan de onderkant van de Hallo van blade Hallo Recovery Services-kluis, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="97549-136">At hello bottom of hello Recovery Services vault blade, click **Create**.</span></span>

    <span data-ttu-id="97549-137">Het kan enkele minuten duren voordat Hallo die Recovery Services-kluis toobe gemaakt.</span><span class="sxs-lookup"><span data-stu-id="97549-137">It can take several minutes for hello Recovery Services vault toobe created.</span></span> <span data-ttu-id="97549-138">Hallo statusmeldingen rechtsboven Hallo van Hallo portal bewaken.</span><span class="sxs-lookup"><span data-stu-id="97549-138">Monitor hello status notifications in hello upper right-hand area of hello portal.</span></span> <span data-ttu-id="97549-139">Zodra de kluis is gemaakt, wordt deze weergegeven in de lijst met Recovery Services-kluizen Hallo.</span><span class="sxs-lookup"><span data-stu-id="97549-139">Once your vault is created, it appears in hello list of Recovery Services vaults.</span></span> <span data-ttu-id="97549-140">Als u uw kluis na enkele minuten niet ziet, klik dan op **Vernieuwen**.</span><span class="sxs-lookup"><span data-stu-id="97549-140">If after several minutes you don't see your vault, click **Refresh**.</span></span>

    ![Op de knop Vernieuwen klikken](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    <span data-ttu-id="97549-142">Nadat u uw kluis in Hallo lijst met Recovery Services-kluizen ziet, bent u klaar tooset Hallo opslag redundantie.</span><span class="sxs-lookup"><span data-stu-id="97549-142">Once you see your vault in hello list of Recovery Services vaults, you are ready tooset hello storage redundancy.</span></span>

### <a name="set-storage-redundancy-for-hello-vault"></a><span data-ttu-id="97549-143">Redundantie van gegevensopslag voor Hallo kluis instellen</span><span class="sxs-lookup"><span data-stu-id="97549-143">Set storage redundancy for hello vault</span></span>
<span data-ttu-id="97549-144">Wanneer u een Recovery Services-kluis maakt, zorg ervoor dat redundantie van gegevensopslag geconfigureerde Hallo zoals u dat wilt.</span><span class="sxs-lookup"><span data-stu-id="97549-144">When you create a Recovery Services vault, make sure storage redundancy is configured hello way you want.</span></span>

1. <span data-ttu-id="97549-145">Van Hallo **Recovery Services-kluizen** blade, klikt u op de nieuwe kluis Hallo.</span><span class="sxs-lookup"><span data-stu-id="97549-145">From hello **Recovery Services vaults** blade, click hello new vault.</span></span>

    ![Selecteer Hallo nieuwe kluis in Hallo-lijst met Recovery Services-kluis](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="97549-147">Wanneer u Hallo kluis selecteert, Hallo **Recovery Services-kluis** blade overzicht en de blade instellingen hello (*die Hallo-naam van de kluis Hallo Hallo boven heeft*) en Hallo details blade kluis openen.</span><span class="sxs-lookup"><span data-stu-id="97549-147">When you select hello vault, hello **Recovery Services vault** blade narrows, and hello Settings blade (*which has hello name of hello vault at hello top*) and hello vault details blade open.</span></span>

    ![Het Hallo-opslagconfiguratie weergeven voor nieuwe kluis](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)
2. <span data-ttu-id="97549-149">Op de blade instellingen Hallo nieuwe kluis, Hallo verticale dia tooscroll omlaag toohello sectie beheren en op **back-upinfrastructuur**.</span><span class="sxs-lookup"><span data-stu-id="97549-149">In hello new vault's Settings blade, use hello vertical slide tooscroll down toohello Manage section, and click **Backup Infrastructure**.</span></span>
    <span data-ttu-id="97549-150">Hallo back-upinfrastructuur blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="97549-150">hello Backup Infrastructure blade opens.</span></span>
3. <span data-ttu-id="97549-151">Klik op Hallo back-upinfrastructuur blade **back-upconfiguratie** tooopen hello **back-upconfiguratie** blade.</span><span class="sxs-lookup"><span data-stu-id="97549-151">In hello Backup Infrastructure blade, click **Backup Configuration** tooopen hello **Backup Configuration** blade.</span></span>

    ![De opslagconfiguratie Hallo voor nieuwe kluis instellen](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. <span data-ttu-id="97549-153">Kies Hallo geschikte optie voor opslagreplicatie voor uw kluis.</span><span class="sxs-lookup"><span data-stu-id="97549-153">Choose hello appropriate storage replication option for your vault.</span></span>

    ![keuzes bij opslagconfiguratie](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    <span data-ttu-id="97549-155">Uw kluis heeft standaard geografisch redundante opslag.</span><span class="sxs-lookup"><span data-stu-id="97549-155">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="97549-156">Als u Azure als een eindpunt primaire back-upopslag gebruikt, gaat u verder toouse **geografisch redundante**.</span><span class="sxs-lookup"><span data-stu-id="97549-156">If you use Azure as a primary backup storage endpoint, continue toouse **Geo-redundant**.</span></span> <span data-ttu-id="97549-157">Als u geen Azure als een eindpunt primaire back-upopslag gebruikt, kiest u **lokaal redundante**, die zorgt voor lagere kosten voor hello Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="97549-157">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces hello Azure storage costs.</span></span> <span data-ttu-id="97549-158">U vindt meer informatie over de opties voor [geografisch redundante](../storage/common/storage-redundancy.md#geo-redundant-storage) en [lokaal redundante ](../storage/common/storage-redundancy.md#locally-redundant-storage) opslag in dit [overzicht van opslagredundantie](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="97549-158">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="97549-159">Nu dat u kunt een kluis hebt gemaakt, kunt u deze voor de back-up van systeemstatus Windows configureren.</span><span class="sxs-lookup"><span data-stu-id="97549-159">Now that you've created a vault, configure it for backing up Windows System State.</span></span>

## <a name="configure-hello-vault"></a><span data-ttu-id="97549-160">Hallo kluis configureren</span><span class="sxs-lookup"><span data-stu-id="97549-160">Configure hello vault</span></span>
1. <span data-ttu-id="97549-161">Op de blade van de Recovery Services-kluis (voor Hallo kluis u zojuist hebt gemaakt), in de sectie aan de slag Hallo Hallo, klikt u op **back-up**, vervolgens op Hallo **aan de slag met back-up** blade Selecteer  **Back-updoel**.</span><span class="sxs-lookup"><span data-stu-id="97549-161">On hello Recovery Services vault blade (for hello vault you just created), in hello Getting Started section, click **Backup**, then on hello **Getting Started with Backup** blade, select **Backup goal**.</span></span>

    ![Open de blade back-updoelstelling](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    <span data-ttu-id="97549-163">Hallo **back-updoel** blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="97549-163">hello **Backup Goal** blade opens.</span></span>

    ![Open de blade back-updoelstelling](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="97549-165">Van Hallo **waar wordt uw workload uitgevoerd?** vervolgkeuzelijst, selecteer **On-premises**.</span><span class="sxs-lookup"><span data-stu-id="97549-165">From hello **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

    <span data-ttu-id="97549-166">U kiest **On-premises** omdat uw Windows Server of Windows-computer een fysieke machine is die zich niet in Azure bevindt.</span><span class="sxs-lookup"><span data-stu-id="97549-166">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="97549-167">Van Hallo **wat wilt u wilt dat toobackup?** selecteert u **systeemstatus**, en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="97549-167">From hello **What do you want toobackup?** menu, select **System State**, and click **OK**.</span></span>

    ![Bestanden en mappen configureren](./media/backup-azure-system-state/backup-goal-system-state.png)

    <span data-ttu-id="97549-169">Als u op OK klikt, verschijnt een vinkje volgende te**back-updoel**, en Hallo **infrastructuur voorbereiden** blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="97549-169">After clicking OK, a checkmark appears next too**Backup goal**, and hello **Prepare infrastructure** blade opens.</span></span>

    ![Nu de back-updoelstelling is geconfigureerd, gaat u de infrastructuur voorbereiden](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="97549-171">Op Hallo **infrastructuur voorbereiden** blade, klikt u op **Agent downloaden voor Windows Server of Windows Client**.</span><span class="sxs-lookup"><span data-stu-id="97549-171">On hello **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

    ![infrastructuur voorbereiden](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

    <span data-ttu-id="97549-173">Als u van Windows Server essentiële gebruikmaakt, kiest u toodownload Hallo-agent voor Windows Server essentieel.</span><span class="sxs-lookup"><span data-stu-id="97549-173">If you are using Windows Server Essential, then choose toodownload hello agent for Windows Server Essential.</span></span> <span data-ttu-id="97549-174">Een pop-upmenu vraagt u toorun of MARSAgentInstaller.exe opslaan.</span><span class="sxs-lookup"><span data-stu-id="97549-174">A pop-up menu prompts you toorun or save MARSAgentInstaller.exe.</span></span>

    ![Dialoogvenster MARSAgentInstaller](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="97549-176">In het pop-upmenu Hallo downloaden, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="97549-176">In hello download pop-up menu, click **Save**.</span></span>

    <span data-ttu-id="97549-177">Standaard Hallo **MARSagentinstaller.exe** bestand tooyour downloadmap wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="97549-177">By default, hello **MARSagentinstaller.exe** file is saved tooyour Downloads folder.</span></span> <span data-ttu-id="97549-178">Als het Hallo-installatieprogramma is voltooid, ziet u een pop-upvenster waarin wordt gevraagd als u toorun Hallo installatieprogramma wilt of Hallo-map open.</span><span class="sxs-lookup"><span data-stu-id="97549-178">When hello installer completes, you will see a pop-up asking if you want toorun hello installer, or open hello folder.</span></span>

    ![infrastructuur voorbereiden](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

    <span data-ttu-id="97549-180">U hoeft niet tooinstall Hallo agent nog.</span><span class="sxs-lookup"><span data-stu-id="97549-180">You don't need tooinstall hello agent yet.</span></span> <span data-ttu-id="97549-181">Nadat u de kluisreferenties Hallo hebt gedownload, kunt u Hallo-agent installeren.</span><span class="sxs-lookup"><span data-stu-id="97549-181">You can install hello agent after you have downloaded hello vault credentials.</span></span>

6. <span data-ttu-id="97549-182">Op Hallo **infrastructuur voorbereiden** blade, klikt u op **downloaden**.</span><span class="sxs-lookup"><span data-stu-id="97549-182">On hello **Prepare infrastructure** blade, click **Download**.</span></span>

    ![kluisreferenties downloaden](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

    <span data-ttu-id="97549-184">de map Downloads tooyour downloaden Hello kluisreferenties</span><span class="sxs-lookup"><span data-stu-id="97549-184">hello vault credentials download tooyour Downloads folder.</span></span> <span data-ttu-id="97549-185">Nadat de kluisreferenties Hallo downloaden, ziet u een pop-upvenster waarin wordt gevraagd als u wilt dat tooopen of Hallo referenties op te slaan.</span><span class="sxs-lookup"><span data-stu-id="97549-185">After hello vault credentials finish downloading, you see a pop-up asking if you want tooopen or save hello credentials.</span></span> <span data-ttu-id="97549-186">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="97549-186">Click **Save**.</span></span> <span data-ttu-id="97549-187">Als u per ongeluk op **Open**, laten Hallo dialoogvenster waarmee wordt geprobeerd tooopen hello kluisreferenties, mislukken.</span><span class="sxs-lookup"><span data-stu-id="97549-187">If you accidentally click **Open**, let hello dialog that attempts tooopen hello vault credentials, fail.</span></span> <span data-ttu-id="97549-188">U kunt de kluisreferenties Hallo niet openen.</span><span class="sxs-lookup"><span data-stu-id="97549-188">You cannot open hello vault credentials.</span></span> <span data-ttu-id="97549-189">De volgende stap toohello worden voortgezet.</span><span class="sxs-lookup"><span data-stu-id="97549-189">Proceed toohello next step.</span></span> <span data-ttu-id="97549-190">Hallo kluisreferenties zijn in de map Downloads Hallo.</span><span class="sxs-lookup"><span data-stu-id="97549-190">hello vault credentials are in hello Downloads folder.</span></span>   

    ![kluisreferenties downloaden is voltooid](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-hello-agent"></a><span data-ttu-id="97549-192">Installeren en registreren Hallo-agent</span><span class="sxs-lookup"><span data-stu-id="97549-192">Install and register hello agent</span></span>

> [!NOTE]
> <span data-ttu-id="97549-193">Inschakelen back-ups via hello Azure-portal is nog niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="97549-193">Enabling backup through hello Azure portal is not available, yet.</span></span> <span data-ttu-id="97549-194">Windows Server System State Hallo Microsoft Azure Recovery Services Agent tooback gebruikt.</span><span class="sxs-lookup"><span data-stu-id="97549-194">Use hello Microsoft Azure Recovery Services Agent tooback up Windows Server System State.</span></span>
>

1. <span data-ttu-id="97549-195">Zoek en dubbelklik op Hallo **MARSagentinstaller.exe** vanuit Hallo Downloads map (of een andere locatie is opgeslagen).</span><span class="sxs-lookup"><span data-stu-id="97549-195">Locate and double-click hello **MARSagentinstaller.exe** from hello Downloads folder (or other saved location).</span></span>

    <span data-ttu-id="97549-196">Hallo-installatieprogramma biedt een reeks berichten zoals deze pakt wordt geïnstalleerd en geregistreerd Hallo Recovery Services-agent.</span><span class="sxs-lookup"><span data-stu-id="97549-196">hello installer provides a series of messages as it extracts, installs, and registers hello Recovery Services agent.</span></span>

    ![uitvoeren van installatiereferenties van de Recovery Services-agent](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="97549-198">Hallo Microsoft Azure Recovery Services Agent-installatiewizard voltooien.</span><span class="sxs-lookup"><span data-stu-id="97549-198">Complete hello Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="97549-199">wizard toocomplete hello, moet u:</span><span class="sxs-lookup"><span data-stu-id="97549-199">toocomplete hello wizard, you need to:</span></span>

   * <span data-ttu-id="97549-200">Kies een locatie voor de installatie en cache map Hallo.</span><span class="sxs-lookup"><span data-stu-id="97549-200">Choose a location for hello installation and cache folder.</span></span>
   * <span data-ttu-id="97549-201">Geef uw proxyserveradres als u een proxy server tooconnect toohello serverinformatie internet.</span><span class="sxs-lookup"><span data-stu-id="97549-201">Provide your proxy server info if you use a proxy server tooconnect toohello internet.</span></span>
   * <span data-ttu-id="97549-202">Uw gebruikersnaam en wachtwoord invoeren als u gebruikmaakt van een geverifieerde proxyserver.</span><span class="sxs-lookup"><span data-stu-id="97549-202">Provide your user name and password details if you use an authenticated proxy.</span></span>
   * <span data-ttu-id="97549-203">Geef referenties op Hallo gedownload kluis</span><span class="sxs-lookup"><span data-stu-id="97549-203">Provide hello downloaded vault credentials</span></span>
   * <span data-ttu-id="97549-204">Hallo-wachtwoordzin voor versleuteling op een veilige locatie opslaan.</span><span class="sxs-lookup"><span data-stu-id="97549-204">Save hello encryption passphrase in a secure location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="97549-205">Als u kwijtraakt of Hallo wachtwoordzin vergeet, Microsoft u niet helpen Hallo back-upgegevens te herstellen.</span><span class="sxs-lookup"><span data-stu-id="97549-205">If you lose or forget hello passphrase, Microsoft cannot help recover hello backup data.</span></span> <span data-ttu-id="97549-206">Hallo-bestand opslaan in een veilige locatie.</span><span class="sxs-lookup"><span data-stu-id="97549-206">Save hello file in a secure location.</span></span> <span data-ttu-id="97549-207">Het is vereiste toorestore een back-up.</span><span class="sxs-lookup"><span data-stu-id="97549-207">It is required toorestore a backup.</span></span>
     >
     >

<span data-ttu-id="97549-208">Hallo-agent wordt nu geïnstalleerd en uw computer is ingeschreven toohello kluis.</span><span class="sxs-lookup"><span data-stu-id="97549-208">hello agent is now installed and your machine is registered toohello vault.</span></span> <span data-ttu-id="97549-209">U bent klaar tooconfigure en uw back-up plannen.</span><span class="sxs-lookup"><span data-stu-id="97549-209">You're ready tooconfigure and schedule your backup.</span></span>

## <a name="back-up-windows-server-system-state-preview"></a><span data-ttu-id="97549-210">Back-up van Windows Server System State (Preview)</span><span class="sxs-lookup"><span data-stu-id="97549-210">Back up Windows Server System State (Preview)</span></span>
<span data-ttu-id="97549-211">de eerste back-up Hallo omvat drie taken:</span><span class="sxs-lookup"><span data-stu-id="97549-211">hello initial backup includes three tasks:</span></span>

* <span data-ttu-id="97549-212">Systeemstatusback-up met hello Azure backup-agent inschakelen</span><span class="sxs-lookup"><span data-stu-id="97549-212">Enable System State Backup using hello Azure Backup agent</span></span>
* <span data-ttu-id="97549-213">Hallo back-up plannen</span><span class="sxs-lookup"><span data-stu-id="97549-213">Schedule hello backup</span></span>
* <span data-ttu-id="97549-214">Back-up van bestanden en mappen voor Hallo eerst</span><span class="sxs-lookup"><span data-stu-id="97549-214">Back up files and folders for hello first time</span></span>

<span data-ttu-id="97549-215">toocomplete hello eerste back-up, gebruik Hallo Microsoft Azure Recovery Services agent.</span><span class="sxs-lookup"><span data-stu-id="97549-215">toocomplete hello initial backup, use hello Microsoft Azure Recovery Services agent.</span></span>

### <a name="tooenable-system-state-backup-using-hello-azure-backup-agent"></a><span data-ttu-id="97549-216">tooenable systeemstatusback-up met behulp van Azure Backup agent Hallo</span><span class="sxs-lookup"><span data-stu-id="97549-216">tooenable System State backup using hello Azure Backup agent</span></span>

1. <span data-ttu-id="97549-217">Voer in een PowerShell-sessie Hallo opdracht toostop hello Azure Backup-engine te volgen.</span><span class="sxs-lookup"><span data-stu-id="97549-217">In a PowerShell session, run hello following command toostop hello Azure Backup engine.</span></span>

  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="97549-218">Open Hallo Windows-register.</span><span class="sxs-lookup"><span data-stu-id="97549-218">Open hello Windows Registry.</span></span>

  ```
  PS C:\> regedit.exe
  ```

3. <span data-ttu-id="97549-219">Voeg Hallo registersleutel Hello volgende DWord-waarde opgegeven.</span><span class="sxs-lookup"><span data-stu-id="97549-219">Add hello following registry key with hello specified DWord Value.</span></span>

  | <span data-ttu-id="97549-220">Registerpad</span><span class="sxs-lookup"><span data-stu-id="97549-220">Registry path</span></span> | <span data-ttu-id="97549-221">Registersleutel</span><span class="sxs-lookup"><span data-stu-id="97549-221">Registry key</span></span> | <span data-ttu-id="97549-222">DWord-waarde</span><span class="sxs-lookup"><span data-stu-id="97549-222">DWord value</span></span> |
  |---------------|--------------|-------------|
  | <span data-ttu-id="97549-223">HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span><span class="sxs-lookup"><span data-stu-id="97549-223">HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span></span> | <span data-ttu-id="97549-224">TurnOffSSBFeature</span><span class="sxs-lookup"><span data-stu-id="97549-224">TurnOffSSBFeature</span></span> | <span data-ttu-id="97549-225">2</span><span class="sxs-lookup"><span data-stu-id="97549-225">2</span></span> |

4. <span data-ttu-id="97549-226">Hallo Backup-engine opnieuw door het uitvoeren van de volgende opdracht in een verhoogde opdrachtprompt Hallo.</span><span class="sxs-lookup"><span data-stu-id="97549-226">Restart hello Backup engine by executing hello following command in an elevated command prompt.</span></span>

  ```
  PS C:\> Net start obengine
  ```

### <a name="tooschedule-hello-backup-job"></a><span data-ttu-id="97549-227">back-uptaak van tooschedule Hallo</span><span class="sxs-lookup"><span data-stu-id="97549-227">tooschedule hello backup job</span></span>

1. <span data-ttu-id="97549-228">Open Hallo Microsoft Azure Recovery Services agent.</span><span class="sxs-lookup"><span data-stu-id="97549-228">Open hello Microsoft Azure Recovery Services agent.</span></span> <span data-ttu-id="97549-229">U vindt deze door te zoeken naar **Microsoft Azure Backup** op uw machine.</span><span class="sxs-lookup"><span data-stu-id="97549-229">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Hello Azure Recovery Services-agent starten](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)

2. <span data-ttu-id="97549-231">Klik in de Recovery Services-agent Hallo op **back-up plannen**.</span><span class="sxs-lookup"><span data-stu-id="97549-231">In hello Recovery Services agent, click **Schedule Backup**.</span></span>

    ![Een back-up van de Windows Server plannen](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)

3. <span data-ttu-id="97549-233">Op Hallo aan de slag pagina van de Wizard Back-up plannen hello, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="97549-233">On hello Getting started page of hello Schedule Backup Wizard, click **Next**.</span></span>

4. <span data-ttu-id="97549-234">Klik op Hallo Items selecteren tooBackup pagina op **Items toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="97549-234">On hello Select Items tooBackup page, click **Add Items**.</span></span>

5. <span data-ttu-id="97549-235">Selecteer **systeemstatus** en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="97549-235">Select **System State** and then click **OK**.</span></span>

6. <span data-ttu-id="97549-236">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="97549-236">Click **Next**.</span></span>

7. <span data-ttu-id="97549-237">Hello systeemstatusback-up en retentie plannen is automatisch ingesteld tooback van elke zondag om 21:00 uur lokale tijd, en de bewaarperiode Hallo too60 dagen.</span><span class="sxs-lookup"><span data-stu-id="97549-237">hello System State Backup and Retention schedule is automatically set tooback up every Sunday at 9:00 PM local time, and hello retention period is set too60 days.</span></span>

   > [!NOTE]
   > <span data-ttu-id="97549-238">Beleid voor het back-up en retentie van systeemstatus wordt automatisch geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="97549-238">System State backup and retention policy is automatically configured.</span></span> <span data-ttu-id="97549-239">Als u back-ups van bestanden en mappen bovendien toohello Windows Server System State, kunt u alleen Hallo-back-up en retentie beleid voor back-ups van de wizard Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="97549-239">If you back up Files and Folders in addition toohello Windows Server System State, specify only hello Backup and Retention policy for file backups from hello wizard.</span></span> 
   >

8. <span data-ttu-id="97549-240">Op de bevestigingspagina Hallo Hallo informatie bekijken en klik vervolgens op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="97549-240">On hello Confirmation page, review hello information, and then click **Finish**.</span></span>

9. <span data-ttu-id="97549-241">Nadat het Hallo-wizard is voltooid voor het maken van back-upschema hello, klikt u op **sluiten**.</span><span class="sxs-lookup"><span data-stu-id="97549-241">After hello wizard finishes creating hello backup schedule, click **Close**.</span></span>

### <a name="tooback-up-windows-server-system-state-for-hello-first-time"></a><span data-ttu-id="97549-242">tooback van Windows Server-systeemstatus voor Hallo eerst</span><span class="sxs-lookup"><span data-stu-id="97549-242">tooback up Windows Server System State for hello first time</span></span>

1. <span data-ttu-id="97549-243">Zorg ervoor dat er zijn geen updates in behandeling voor Windows Server waarvoor opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="97549-243">Make sure there are no pending updates for Windows Server that require a reboot.</span></span>

2. <span data-ttu-id="97549-244">Klik in het Hallo Recovery Services-agent op **Back-Up uit** toocomplete Hallo eerste seeding via Hallo netwerk.</span><span class="sxs-lookup"><span data-stu-id="97549-244">In hello Recovery Services agent, click **Back Up Now** toocomplete hello initial seeding over hello network.</span></span>

    ![Nu back-up maken van Windows Server](./media/backup-try-azure-backup-in-10-mins/backup-now.png)

3. <span data-ttu-id="97549-246">Op de bevestigingspagina Hallo revisie Hallo-instellingen die de Wizard Back-Up nu Hallo tooback Hallo machine gebruikt.</span><span class="sxs-lookup"><span data-stu-id="97549-246">On hello Confirmation page, review hello settings that hello Back Up Now Wizard will use tooback up hello machine.</span></span> <span data-ttu-id="97549-247">Klik vervolgens op **Back-up maken**.</span><span class="sxs-lookup"><span data-stu-id="97549-247">Then click **Back Up**.</span></span>

4. <span data-ttu-id="97549-248">Klik op **sluiten** tooclose Hallo-wizard.</span><span class="sxs-lookup"><span data-stu-id="97549-248">Click **Close** tooclose hello wizard.</span></span> <span data-ttu-id="97549-249">Als u Hallo wizard sluit voordat de back-upproces Hallo is voltooid, blijft Hallo wizard toorun op Hallo achtergrond.</span><span class="sxs-lookup"><span data-stu-id="97549-249">If you close hello wizard before hello backup process finishes, hello wizard continues toorun in hello background.</span></span>

5. <span data-ttu-id="97549-250">Als u back-up bestanden en mappen op uw server bovendien toohello Windows Server System State, wordt de wizard nu back-up in Hallo alleen reservekopie van bestanden.</span><span class="sxs-lookup"><span data-stu-id="97549-250">If you back up Files and Folders on your server, in addition toohello Windows Server System State, hello Backup Now wizard will only back up files.</span></span> <span data-ttu-id="97549-251">tooperform de systeemstatus van een ad-hoc back-up, Hallo volgende PowerShell-opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="97549-251">tooperform an ad hoc System State back up, use hello following PowerShell command:</span></span>

    ```
    PS C:\> Start-OBSystemStateBackup
    ```

  <span data-ttu-id="97549-252">Nadat de eerste back-up Hallo is voltooid, Hallo **taak voltooid** status wordt weergegeven in Hallo back-up-console.</span><span class="sxs-lookup"><span data-stu-id="97549-252">After hello initial backup is completed, hello **Job completed** status appears in hello Backup console.</span></span>

  ![IR voltooid](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="frequently-asked-questions"></a><span data-ttu-id="97549-254">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="97549-254">Frequently asked questions</span></span>

<span data-ttu-id="97549-255">Hallo bevatten onderstaande vragen en antwoorden aanvullende informatie.</span><span class="sxs-lookup"><span data-stu-id="97549-255">hello following questions and answers provide supplementary information.</span></span>

### <a name="what-is-hello-staging-volume"></a><span data-ttu-id="97549-256">Wat is Hallo fasering Volume?</span><span class="sxs-lookup"><span data-stu-id="97549-256">What is hello Staging Volume?</span></span>

<span data-ttu-id="97549-257">Hallo fasering Volume vertegenwoordigt Hallo tussenliggende locatie waar Hallo standaard beschikbaar zijn, Windows Server Backup Hallo systeemstatusback-up voorbereid.</span><span class="sxs-lookup"><span data-stu-id="97549-257">hello Staging Volume represents hello intermediate location where hello natively available, Windows Server Backup stages hello System State Backup.</span></span> <span data-ttu-id="97549-258">Azure backup-agent en vervolgens worden gecomprimeerd en versleuteld deze tussenliggende back-up en verzendt dat deze via een beveiligde HTTPS-Protocol toohello Recovery Services-kluis hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="97549-258">Azure Backup agent then compresses and encrypts this intermediate backup and sends it via secure HTTPS Protocol toohello configured Recovery Services Vault.</span></span> <span data-ttu-id="97549-259">**Sterk aanbevolen dat u Hallo fasering Volume instellen in een niet-Windows-besturingssysteemvolume. Als u problemen met de systeemstatusback-ups ziet, is het Hallo-locatie van het Volume fasering controleren Hallo eerste probleemoplossing.**</span><span class="sxs-lookup"><span data-stu-id="97549-259">**We strongly recommended you establish hello Staging Volume in a non-Windows-OS volume. If you observe problems with System State Backups, checking hello location of your Staging Volume is hello first troubleshooting step.**</span></span> 

### <a name="how-can-i-change-hello-staging-volume-path-specified-in-hello-azure-backup-agent"></a><span data-ttu-id="97549-260">Hoe kan ik Hallo fasering Volumepad is opgegeven in hello Azure backup-agent wijzigen?</span><span class="sxs-lookup"><span data-stu-id="97549-260">How can I change hello Staging Volume Path specified in hello Azure Backup agent?</span></span>

<span data-ttu-id="97549-261">Hallo fasering Volume bevindt zich in de cachemap Hallo standaard.</span><span class="sxs-lookup"><span data-stu-id="97549-261">hello Staging Volume is located in hello cache folder by default.</span></span> 

1. <span data-ttu-id="97549-262">toochange deze locatie, gebruik Hallo na de opdracht (in een verhoogde opdrachtprompt):</span><span class="sxs-lookup"><span data-stu-id="97549-262">toochange this location, use hello following command (in an elevated command prompt):</span></span>
  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="97549-263">Werk vervolgens Hallo registervermeldingen met Hallo pad toohello nieuwe tijdelijke map Volume te volgen.</span><span class="sxs-lookup"><span data-stu-id="97549-263">Then update hello following registry entries with hello path toohello new Staging Volume folder.</span></span>

  |<span data-ttu-id="97549-264">Registerpad</span><span class="sxs-lookup"><span data-stu-id="97549-264">Registry path</span></span>|<span data-ttu-id="97549-265">Registersleutel</span><span class="sxs-lookup"><span data-stu-id="97549-265">Registry key</span></span>|<span data-ttu-id="97549-266">Waarde</span><span class="sxs-lookup"><span data-stu-id="97549-266">Value</span></span>|
  |-------------|------------|-----|
  |<span data-ttu-id="97549-267">HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span><span class="sxs-lookup"><span data-stu-id="97549-267">HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span></span> | <span data-ttu-id="97549-268">SSBStagingPath</span><span class="sxs-lookup"><span data-stu-id="97549-268">SSBStagingPath</span></span> | <span data-ttu-id="97549-269">nieuwe volume faseringslocatie</span><span class="sxs-lookup"><span data-stu-id="97549-269">new staging volume location</span></span> |

<span data-ttu-id="97549-270">Hallo pad voor gefaseerde installatie is hoofdlettergevoelig en moet Hallo exact hetzelfde hoofdlettergebruik als wat op Hallo server bestaat.</span><span class="sxs-lookup"><span data-stu-id="97549-270">hello Staging Path is case sensitive and must be hello exact same casing as what exists on hello server.</span></span> 

3. <span data-ttu-id="97549-271">Zodra u Hallo fasering Volumepad wijzigt, start opnieuw op Hallo Backup-engine:</span><span class="sxs-lookup"><span data-stu-id="97549-271">Once you change hello Staging volume path, restart hello Backup engine:</span></span>
  ```
  PS C:\> Net start obengine
  ```
4. <span data-ttu-id="97549-272">toopick up Hallo gewijzigd pad, open Hallo Microsoft Azure Recovery Services agent en een ad-hoc back-up van systeemstatus trigger.</span><span class="sxs-lookup"><span data-stu-id="97549-272">toopick up hello changed path, open hello Microsoft Azure Recovery Services agent and trigger an ad hoc backup of System State.</span></span>

### <a name="why-is-hello-system-state-default-retention-set-too60-days"></a><span data-ttu-id="97549-273">Waarom is de systeemstatus Hallo standaard bewaren too60 dagen instellen?</span><span class="sxs-lookup"><span data-stu-id="97549-273">Why is hello System State default retention set too60 days?</span></span>

<span data-ttu-id="97549-274">Hallo-levensduur van een systeemstatusback-up is hetzelfde als de instelling voor Windows Server Active Directory-rol Hallo Hallo 'tombstone-levensduur' Hallo.</span><span class="sxs-lookup"><span data-stu-id="97549-274">hello useful life of a system state backup is hello same as hello "tombstone lifetime" setting for hello Windows Server Active Directory role.</span></span> <span data-ttu-id="97549-275">de standaardwaarde Hallo voor Hallo tombstone-levensduur vermelding is 60 dagen.</span><span class="sxs-lookup"><span data-stu-id="97549-275">hello default value for hello tombstone lifetime entry is 60 days.</span></span> <span data-ttu-id="97549-276">Deze waarde kan worden ingesteld op Hallo Directory Service (NTDS) config-object.</span><span class="sxs-lookup"><span data-stu-id="97549-276">This value can be set on hello Directory Service (NTDS) config object.</span></span>

### <a name="how-do-i-change-hello-default-backup-and-retention-policy-for-system-state"></a><span data-ttu-id="97549-277">Hoe wijzig ik Hallo standaard back-up- en bewaarbeleid voor systeemstatus</span><span class="sxs-lookup"><span data-stu-id="97549-277">How do I change hello default Backup and Retention Policy for System State?</span></span>

<span data-ttu-id="97549-278">toochange hello standaard back-up en het bewaarbeleid voor systeemstatus:</span><span class="sxs-lookup"><span data-stu-id="97549-278">toochange hello default Backup and Retention Policy for System State:</span></span>
1. <span data-ttu-id="97549-279">Stop Hallo Backup-engine.</span><span class="sxs-lookup"><span data-stu-id="97549-279">Stop hello Backup engine.</span></span> <span data-ttu-id="97549-280">Hallo volgende opdracht uit een verhoogde opdrachtprompt worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="97549-280">Run hello following command from an elevated command prompt.</span></span>

  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="97549-281">Toevoegen of bijwerken van de volgende registervermeldingen in HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider Hallo.</span><span class="sxs-lookup"><span data-stu-id="97549-281">Add or update hello following registry key entries in HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider.</span></span>

  |<span data-ttu-id="97549-282">Naam van routeringsregister</span><span class="sxs-lookup"><span data-stu-id="97549-282">Registry Name</span></span>|<span data-ttu-id="97549-283">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="97549-283">Description</span></span>|<span data-ttu-id="97549-284">Waarde</span><span class="sxs-lookup"><span data-stu-id="97549-284">Value</span></span>|
  |-------------|-----------|-----|
  |<span data-ttu-id="97549-285">SSBScheduleTime</span><span class="sxs-lookup"><span data-stu-id="97549-285">SSBScheduleTime</span></span>|<span data-ttu-id="97549-286">Tijd van de gebruikte tooconfigure Hallo Hallo back-up.</span><span class="sxs-lookup"><span data-stu-id="97549-286">Used tooconfigure hello time of hello backup.</span></span> <span data-ttu-id="97549-287">Standaardinstelling is 21: 00 lokale tijd.</span><span class="sxs-lookup"><span data-stu-id="97549-287">Default is 9PM local time.</span></span>|<span data-ttu-id="97549-288">DWord: Indeling UUMM (decimaal) zo 2130 voor 9:30:00 lokale tijd</span><span class="sxs-lookup"><span data-stu-id="97549-288">DWord: Format HHMM (Decimal) for example 2130 for 9:30PM local time</span></span>|
  |<span data-ttu-id="97549-289">SSBScheduleDays</span><span class="sxs-lookup"><span data-stu-id="97549-289">SSBScheduleDays</span></span>|<span data-ttu-id="97549-290">Gebruikte tooconfigure Hallo dagen wanneer systeemstatusback-up moet worden uitgevoerd op Hallo opgegeven tijd.</span><span class="sxs-lookup"><span data-stu-id="97549-290">Used tooconfigure hello days when System State Backup must be performed at hello specified time.</span></span> <span data-ttu-id="97549-291">Afzonderlijke cijfers opgeven dagen van week Hallo.</span><span class="sxs-lookup"><span data-stu-id="97549-291">Individual digits specify days of hello week.</span></span> <span data-ttu-id="97549-292">zondag 0, 1 is maandag, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="97549-292">0 represents Sunday, 1 is Monday, and so on.</span></span> <span data-ttu-id="97549-293">Standaarddag voor back-up is zondag.</span><span class="sxs-lookup"><span data-stu-id="97549-293">Default day for backup is Sunday.</span></span>|<span data-ttu-id="97549-294">DWord: dagen van Hallo week toorun back-up (decimaal), bijvoorbeeld 1230 plant u back-ups op maandag, dinsdag, woensdag en zondag.</span><span class="sxs-lookup"><span data-stu-id="97549-294">DWord: days of hello week toorun backup (decimal) for example 1230 schedules backups on Monday, Tuesday, Wednesday, and Sunday.</span></span>|
  |<span data-ttu-id="97549-295">SSBRetentionDays</span><span class="sxs-lookup"><span data-stu-id="97549-295">SSBRetentionDays</span></span>|<span data-ttu-id="97549-296">Gebruikte tooconfigure Hallo dagen tooretain back-up.</span><span class="sxs-lookup"><span data-stu-id="97549-296">Used tooconfigure hello days tooretain backup.</span></span> <span data-ttu-id="97549-297">Standaardwaarde is 60.</span><span class="sxs-lookup"><span data-stu-id="97549-297">Default value is 60.</span></span> <span data-ttu-id="97549-298">Maximaal toegestane waarde is 180.</span><span class="sxs-lookup"><span data-stu-id="97549-298">Maximum allowed value is 180.</span></span>|<span data-ttu-id="97549-299">DWord: Dagen tooretain back-up (decimaal).</span><span class="sxs-lookup"><span data-stu-id="97549-299">DWord: Days tooretain backup (decimal).</span></span>|

3. <span data-ttu-id="97549-300">Gebruik Hallo volgende opdracht toorestart Hallo back-engine.</span><span class="sxs-lookup"><span data-stu-id="97549-300">Use hello following command toorestart hello backup engine.</span></span>
    ```
    PS C:\> Net start obengine
    ```

4. <span data-ttu-id="97549-301">Open Hallo Microsoft Recovery Services agent.</span><span class="sxs-lookup"><span data-stu-id="97549-301">Open hello Microsoft Recovery Services agent.</span></span>

5. <span data-ttu-id="97549-302">Klik op **back-up plannen** en klik vervolgens op **volgende** totdat u Hallo wijzigingen weer.</span><span class="sxs-lookup"><span data-stu-id="97549-302">Click **Schedule Backup** and then click **Next** until you see hello changes reflected.</span></span>

6. <span data-ttu-id="97549-303">Klik op **voltooien** tooapply Hallo wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="97549-303">Click **Finish** tooapply hello changes.</span></span>


## <a name="questions"></a><span data-ttu-id="97549-304">Vragen?</span><span class="sxs-lookup"><span data-stu-id="97549-304">Questions?</span></span>
<span data-ttu-id="97549-305">Als u vragen hebt of als er een functie die u toosee opgenomen wilt, [Stuur ons feedback](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="97549-305">If you have questions, or if there is any feature that you would like toosee included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="97549-306">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="97549-306">Next steps</span></span>
* <span data-ttu-id="97549-307">Meer informatie over [back-ups maken van Windows-machines](backup-configure-vault.md).</span><span class="sxs-lookup"><span data-stu-id="97549-307">Get more details about [backing up Windows machines](backup-configure-vault.md).</span></span>
* <span data-ttu-id="97549-308">Wanneer u eenmaal een back-up hebt gemaakt van uw bestanden en mappen, kunt u [uw kluizen en servers beheren](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="97549-308">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="97549-309">Als u een back-up toorestore moet, gebruikt u in dit artikel te[bestanden tooa Windows-machine herstellen](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="97549-309">If you need toorestore a backup, use this article too[restore files tooa Windows machine](backup-azure-restore-windows-server.md).</span></span>
