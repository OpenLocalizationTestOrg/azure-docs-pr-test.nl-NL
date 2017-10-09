---
title: aaaBack up Windows bestanden en mappen tooAzure (Resource Manager) | Microsoft Docs
description: Meer informatie over tooback van Windows-bestanden en mappen tooAzure in een implementatie van Resource Manager.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: hoe toobackup; hoe tooback; back-bestanden en mappen
ms.assetid: 5b15ebf1-2214-4722-b937-96e2be8872bb
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 8/15/2017
ms.author: markgal;
ms.openlocfilehash: 07d6580a84d5092ed2c61bf86ff5fcb148423ef2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="first-look-back-up-files-and-folders-in-resource-manager-deployment"></a><span data-ttu-id="f197b-104">Eerste blik: een back-up maken van bestanden en mappen met Resource Manager-implementatie</span><span class="sxs-lookup"><span data-stu-id="f197b-104">First look: back up files and folders in Resource Manager deployment</span></span>
<span data-ttu-id="f197b-105">Dit artikel wordt uitgelegd hoe tooback van uw Windows Server (of Windows-computer)-bestanden en mappen tooAzure met behulp van de implementatie van een Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f197b-105">This article explains how tooback up your Windows Server (or Windows computer) files and folders tooAzure using a Resource Manager deployment.</span></span> <span data-ttu-id="f197b-106">Het is een zelfstudie beoogde toowalk u bij het Hallo-basisbeginselen.</span><span class="sxs-lookup"><span data-stu-id="f197b-106">It's a tutorial intended toowalk you through hello basics.</span></span> <span data-ttu-id="f197b-107">Als u wilt dat tooget gestart met behulp van Azure Backup, bent u op de juiste plaats Hallo.</span><span class="sxs-lookup"><span data-stu-id="f197b-107">If you want tooget started using Azure Backup, you're in hello right place.</span></span>

<span data-ttu-id="f197b-108">Als u tooknow meer informatie over Azure Backup wilt, Lees dit [overzicht](backup-introduction-to-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="f197b-108">If you want tooknow more about Azure Backup, read this [overview](backup-introduction-to-azure-backup.md).</span></span>

<span data-ttu-id="f197b-109">Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/) aan waarmee u toegang hebt tot alle services van Azure.</span><span class="sxs-lookup"><span data-stu-id="f197b-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) that lets you access any Azure service.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="f197b-110">Een Recovery Services-kluis maken</span><span class="sxs-lookup"><span data-stu-id="f197b-110">Create a recovery services vault</span></span>
<span data-ttu-id="f197b-111">tooback van uw bestanden en mappen, moet u een Recovery Services-kluis in Hallo regio waar u toostore Hallo gegevens toocreate.</span><span class="sxs-lookup"><span data-stu-id="f197b-111">tooback up your files and folders, you need toocreate a Recovery Services vault in hello region where you want toostore hello data.</span></span> <span data-ttu-id="f197b-112">U moet ook toodetermine hoe u uw opslag repliceren wilt.</span><span class="sxs-lookup"><span data-stu-id="f197b-112">You also need toodetermine how you want your storage replicated.</span></span>

### <a name="toocreate-a-recovery-services-vault"></a><span data-ttu-id="f197b-113">toocreate een Recovery Services-kluis</span><span class="sxs-lookup"><span data-stu-id="f197b-113">toocreate a Recovery Services vault</span></span>
1. <span data-ttu-id="f197b-114">Als u dit nog niet hebt gedaan, meld u aan toohello [Azure Portal](https://portal.azure.com/) met behulp van uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="f197b-114">If you haven't already done so, sign in toohello [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="f197b-115">Klik op het menu Hub Hallo **meer services** en typt u in de lijst met resources Hallo **Recovery Services** en klik op **Recovery Services-kluizen**.</span><span class="sxs-lookup"><span data-stu-id="f197b-115">On hello Hub menu, click **More services** and in hello list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Een Recovery Services-kluis maken, stap 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="f197b-117">Als er recovery services-kluizen in Hallo abonnement, worden Hallo kluizen weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f197b-117">If there are recovery services vaults in hello subscription, hello vaults are listed.</span></span>
3. <span data-ttu-id="f197b-118">Op Hallo **Recovery Services-kluizen** menu, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="f197b-118">On hello **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Een Recovery Services-kluis maken, stap 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="f197b-120">Hallo Recovery Services vault blade wordt geopend, waarin u wordt gevraagd tooprovide een **naam**, **abonnement**, **resourcegroep**, en **locatie**.</span><span class="sxs-lookup"><span data-stu-id="f197b-120">hello Recovery Services vault blade opens, prompting you tooprovide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Een Recovery Services-kluis maken, stap 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="f197b-122">Voor **naam**, voer een beschrijvende naam tooidentify Hallo-kluis.</span><span class="sxs-lookup"><span data-stu-id="f197b-122">For **Name**, enter a friendly name tooidentify hello vault.</span></span> <span data-ttu-id="f197b-123">de naam van de Hallo moet toobe unieke voor hello Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="f197b-123">hello name needs toobe unique for hello Azure subscription.</span></span> <span data-ttu-id="f197b-124">Typ een naam die tussen 2 en 50 tekens bevat.</span><span class="sxs-lookup"><span data-stu-id="f197b-124">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="f197b-125">De naam moet beginnen met een letter en mag alleen letters, cijfers en afbreekstreepjes bevatten.</span><span class="sxs-lookup"><span data-stu-id="f197b-125">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="f197b-126">In Hallo **abonnement** sectie, gebruikt u Hallo vervolgkeuzelijst toochoose hello Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="f197b-126">In hello **Subscription** section, use hello drop-down menu toochoose hello Azure subscription.</span></span> <span data-ttu-id="f197b-127">Als u slechts één abonnement, dat abonnement wordt weergegeven en kunt u de volgende stap toohello overslaan.</span><span class="sxs-lookup"><span data-stu-id="f197b-127">If you use only one subscription, that subscription appears and you can skip toohello next step.</span></span> <span data-ttu-id="f197b-128">Als u niet zeker weet welk abonnement toouse Hallo standaard gebruiken (of voorgestelde) abonnement.</span><span class="sxs-lookup"><span data-stu-id="f197b-128">If you are not sure which subscription toouse, use hello default (or suggested) subscription.</span></span> <span data-ttu-id="f197b-129">Er zijn alleen meerdere mogelijkheden als uw organisatieaccount is gekoppeld aan meerdere Azure-abonnementen.</span><span class="sxs-lookup"><span data-stu-id="f197b-129">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="f197b-130">In Hallo **resourcegroep** sectie:</span><span class="sxs-lookup"><span data-stu-id="f197b-130">In hello **Resource group** section:</span></span>

    * <span data-ttu-id="f197b-131">Selecteer **nieuw** als u wilt dat toocreate een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="f197b-131">select **Create new** if you want toocreate a new Resource group.</span></span>
    <span data-ttu-id="f197b-132">of</span><span class="sxs-lookup"><span data-stu-id="f197b-132">Or</span></span>
    * <span data-ttu-id="f197b-133">Selecteer **gebruik bestaande** en klik op Hallo vervolgkeuzelijst toosee Hallo lijst met beschikbare resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="f197b-133">select **Use existing** and click hello drop-down menu toosee hello available list of Resource groups.</span></span>

  <span data-ttu-id="f197b-134">Zie voor meer informatie over resourcegroepen Hallo [overzicht van Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f197b-134">For complete information on Resource groups, see hello [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="f197b-135">Klik op **locatie** tooselect Hallo geografische regio voor Hallo kluis.</span><span class="sxs-lookup"><span data-stu-id="f197b-135">Click **Location** tooselect hello geographic region for hello vault.</span></span> <span data-ttu-id="f197b-136">Deze keuze bepaalt Hallo geografische regio waar uw back-upgegevens worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="f197b-136">This choice determines hello geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="f197b-137">Aan de onderkant van de Hallo van blade Hallo Recovery Services-kluis, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="f197b-137">At hello bottom of hello Recovery Services vault blade, click **Create**.</span></span>

    <span data-ttu-id="f197b-138">Het kan enkele minuten duren voordat Hallo die Recovery Services-kluis toobe gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f197b-138">It can take several minutes for hello Recovery Services vault toobe created.</span></span> <span data-ttu-id="f197b-139">Hallo statusmeldingen rechtsboven Hallo van Hallo portal bewaken.</span><span class="sxs-lookup"><span data-stu-id="f197b-139">Monitor hello status notifications in hello upper right-hand area of hello portal.</span></span> <span data-ttu-id="f197b-140">Zodra de kluis is gemaakt, wordt deze weergegeven in de lijst met Recovery Services-kluizen Hallo.</span><span class="sxs-lookup"><span data-stu-id="f197b-140">Once your vault is created, it appears in hello list of Recovery Services vaults.</span></span> <span data-ttu-id="f197b-141">Als u uw kluis na enkele minuten niet ziet, klik dan op **Vernieuwen**.</span><span class="sxs-lookup"><span data-stu-id="f197b-141">If after several minutes you don't see your vault, click **Refresh**.</span></span>

    ![Op de knop Vernieuwen klikken](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    <span data-ttu-id="f197b-143">Nadat u uw kluis in Hallo lijst met Recovery Services-kluizen ziet, bent u klaar tooset Hallo opslag redundantie.</span><span class="sxs-lookup"><span data-stu-id="f197b-143">Once you see your vault in hello list of Recovery Services vaults, you are ready tooset hello storage redundancy.</span></span>

### <a name="set-storage-redundancy-for-hello-vault"></a><span data-ttu-id="f197b-144">Redundantie van gegevensopslag voor Hallo kluis instellen</span><span class="sxs-lookup"><span data-stu-id="f197b-144">Set storage redundancy for hello vault</span></span>
<span data-ttu-id="f197b-145">Wanneer u een Recovery Services-kluis maakt, zorg ervoor dat redundantie van gegevensopslag geconfigureerde Hallo zoals u dat wilt.</span><span class="sxs-lookup"><span data-stu-id="f197b-145">When you create a Recovery Services vault, make sure storage redundancy is configured hello way you want.</span></span>

1. <span data-ttu-id="f197b-146">Van Hallo **Recovery Services-kluizen** blade, klikt u op de nieuwe kluis Hallo.</span><span class="sxs-lookup"><span data-stu-id="f197b-146">From hello **Recovery Services vaults** blade, click hello new vault.</span></span>

    ![Selecteer Hallo nieuwe kluis in Hallo-lijst met Recovery Services-kluis](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="f197b-148">Wanneer u Hallo kluis selecteert, Hallo **Recovery Services-kluis** blade overzicht en de blade instellingen hello (*die Hallo-naam van de kluis Hallo Hallo boven heeft*) en Hallo details blade kluis openen.</span><span class="sxs-lookup"><span data-stu-id="f197b-148">When you select hello vault, hello **Recovery Services vault** blade narrows, and hello Settings blade (*which has hello name of hello vault at hello top*) and hello vault details blade open.</span></span>

    ![Het Hallo-opslagconfiguratie weergeven voor nieuwe kluis](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)
2. <span data-ttu-id="f197b-150">Op de blade instellingen Hallo nieuwe kluis, Hallo verticale dia tooscroll omlaag toohello sectie beheren en op **back-upinfrastructuur**.</span><span class="sxs-lookup"><span data-stu-id="f197b-150">In hello new vault's Settings blade, use hello vertical slide tooscroll down toohello Manage section, and click **Backup Infrastructure**.</span></span>
    <span data-ttu-id="f197b-151">Hallo back-upinfrastructuur blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="f197b-151">hello Backup Infrastructure blade opens.</span></span>
3. <span data-ttu-id="f197b-152">Klik op Hallo back-upinfrastructuur blade **back-upconfiguratie** tooopen hello **back-upconfiguratie** blade.</span><span class="sxs-lookup"><span data-stu-id="f197b-152">In hello Backup Infrastructure blade, click **Backup Configuration** tooopen hello **Backup Configuration** blade.</span></span>

    ![De opslagconfiguratie Hallo voor nieuwe kluis instellen](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. <span data-ttu-id="f197b-154">Kies Hallo geschikte optie voor opslagreplicatie voor uw kluis.</span><span class="sxs-lookup"><span data-stu-id="f197b-154">Choose hello appropriate storage replication option for your vault.</span></span>

    ![keuzes bij opslagconfiguratie](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    <span data-ttu-id="f197b-156">Uw kluis heeft standaard geografisch redundante opslag.</span><span class="sxs-lookup"><span data-stu-id="f197b-156">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="f197b-157">Als u Azure als een eindpunt primaire back-upopslag gebruikt, gaat u verder toouse **geografisch redundante**.</span><span class="sxs-lookup"><span data-stu-id="f197b-157">If you use Azure as a primary backup storage endpoint, continue toouse **Geo-redundant**.</span></span> <span data-ttu-id="f197b-158">Als u geen Azure als een eindpunt primaire back-upopslag gebruikt, kiest u **lokaal redundante**, die zorgt voor lagere kosten voor hello Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="f197b-158">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces hello Azure storage costs.</span></span> <span data-ttu-id="f197b-159">U vindt meer informatie over de opties voor [geografisch redundante](../storage/common/storage-redundancy.md#geo-redundant-storage) en [lokaal redundante ](../storage/common/storage-redundancy.md#locally-redundant-storage) opslag in dit [overzicht van opslagredundantie](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="f197b-159">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="f197b-160">Nu u een kluis hebt gemaakt, kunt u deze voor de back-ups van bestanden en mappen configureren.</span><span class="sxs-lookup"><span data-stu-id="f197b-160">Now that you've created a vault, configure it for backing up files and folders.</span></span>

## <a name="configure-hello-vault"></a><span data-ttu-id="f197b-161">Hallo kluis configureren</span><span class="sxs-lookup"><span data-stu-id="f197b-161">Configure hello vault</span></span>
1. <span data-ttu-id="f197b-162">Op de blade van de Recovery Services-kluis (voor Hallo kluis u zojuist hebt gemaakt), in de sectie aan de slag Hallo Hallo, klikt u op **back-up**, vervolgens op Hallo **aan de slag met back-up** blade Selecteer  **Back-updoel**.</span><span class="sxs-lookup"><span data-stu-id="f197b-162">On hello Recovery Services vault blade (for hello vault you just created), in hello Getting Started section, click **Backup**, then on hello **Getting Started with Backup** blade, select **Backup goal**.</span></span>

    ![Open de blade back-updoelstelling](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    <span data-ttu-id="f197b-164">Hallo **back-updoel** blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="f197b-164">hello **Backup Goal** blade opens.</span></span>

    ![Open de blade back-updoelstelling](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="f197b-166">Van Hallo **waar wordt uw workload uitgevoerd?** vervolgkeuzelijst, selecteer **On-premises**.</span><span class="sxs-lookup"><span data-stu-id="f197b-166">From hello **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

    <span data-ttu-id="f197b-167">U kiest **On-premises** omdat uw Windows Server of Windows-computer een fysieke machine is die zich niet in Azure bevindt.</span><span class="sxs-lookup"><span data-stu-id="f197b-167">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="f197b-168">Van Hallo **wat wilt u wilt dat toobackup?** selecteert u **bestanden en mappen**, en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="f197b-168">From hello **What do you want toobackup?** menu, select **Files and folders**, and click **OK**.</span></span>

    ![Bestanden en mappen configureren](./media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

    <span data-ttu-id="f197b-170">Als u op OK klikt, verschijnt een vinkje volgende te**back-updoel**, en Hallo **infrastructuur voorbereiden** blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="f197b-170">After clicking OK, a checkmark appears next too**Backup goal**, and hello **Prepare infrastructure** blade opens.</span></span>

    ![Nu de back-updoelstelling is geconfigureerd, gaat u de infrastructuur voorbereiden](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="f197b-172">Op Hallo **infrastructuur voorbereiden** blade, klikt u op **Agent downloaden voor Windows Server of Windows Client**.</span><span class="sxs-lookup"><span data-stu-id="f197b-172">On hello **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

    ![infrastructuur voorbereiden](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

    <span data-ttu-id="f197b-174">Als u van Windows Server essentiële gebruikmaakt, kiest u toodownload Hallo-agent voor Windows Server essentieel.</span><span class="sxs-lookup"><span data-stu-id="f197b-174">If you are using Windows Server Essential, then choose toodownload hello agent for Windows Server Essential.</span></span> <span data-ttu-id="f197b-175">Een pop-upmenu vraagt u toorun of MARSAgentInstaller.exe opslaan.</span><span class="sxs-lookup"><span data-stu-id="f197b-175">A pop-up menu prompts you toorun or save MARSAgentInstaller.exe.</span></span>

    ![Dialoogvenster MARSAgentInstaller](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="f197b-177">In het pop-upmenu Hallo downloaden, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f197b-177">In hello download pop-up menu, click **Save**.</span></span>

    <span data-ttu-id="f197b-178">Standaard Hallo **MARSagentinstaller.exe** bestand tooyour downloadmap wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="f197b-178">By default, hello **MARSagentinstaller.exe** file is saved tooyour Downloads folder.</span></span> <span data-ttu-id="f197b-179">Als het Hallo-installatieprogramma is voltooid, ziet u een pop-upvenster waarin wordt gevraagd als u toorun Hallo installatieprogramma wilt of Hallo-map open.</span><span class="sxs-lookup"><span data-stu-id="f197b-179">When hello installer completes, you will see a pop-up asking if you want toorun hello installer, or open hello folder.</span></span>

    ![infrastructuur voorbereiden](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

    <span data-ttu-id="f197b-181">U hoeft niet tooinstall Hallo agent nog.</span><span class="sxs-lookup"><span data-stu-id="f197b-181">You don't need tooinstall hello agent yet.</span></span> <span data-ttu-id="f197b-182">Nadat u de kluisreferenties Hallo hebt gedownload, kunt u Hallo-agent installeren.</span><span class="sxs-lookup"><span data-stu-id="f197b-182">You can install hello agent after you have downloaded hello vault credentials.</span></span>

6. <span data-ttu-id="f197b-183">Op Hallo **infrastructuur voorbereiden** blade, klikt u op **downloaden**.</span><span class="sxs-lookup"><span data-stu-id="f197b-183">On hello **Prepare infrastructure** blade, click **Download**.</span></span>

    ![kluisreferenties downloaden](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

    <span data-ttu-id="f197b-185">de map Downloads tooyour downloaden Hello kluisreferenties</span><span class="sxs-lookup"><span data-stu-id="f197b-185">hello vault credentials download tooyour Downloads folder.</span></span> <span data-ttu-id="f197b-186">Nadat de kluisreferenties Hallo downloaden, ziet u een pop-upvenster waarin wordt gevraagd als u wilt dat tooopen of Hallo referenties op te slaan.</span><span class="sxs-lookup"><span data-stu-id="f197b-186">After hello vault credentials finish downloading, you see a pop-up asking if you want tooopen or save hello credentials.</span></span> <span data-ttu-id="f197b-187">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f197b-187">Click **Save**.</span></span> <span data-ttu-id="f197b-188">Als u per ongeluk op **Open**, laten Hallo dialoogvenster waarmee wordt geprobeerd tooopen hello kluisreferenties, mislukken.</span><span class="sxs-lookup"><span data-stu-id="f197b-188">If you accidentally click **Open**, let hello dialog that attempts tooopen hello vault credentials, fail.</span></span> <span data-ttu-id="f197b-189">U kunt de kluisreferenties Hallo niet openen.</span><span class="sxs-lookup"><span data-stu-id="f197b-189">You cannot open hello vault credentials.</span></span> <span data-ttu-id="f197b-190">De volgende stap toohello worden voortgezet.</span><span class="sxs-lookup"><span data-stu-id="f197b-190">Proceed toohello next step.</span></span> <span data-ttu-id="f197b-191">Hallo kluisreferenties zijn in de map Downloads Hallo.</span><span class="sxs-lookup"><span data-stu-id="f197b-191">hello vault credentials are in hello Downloads folder.</span></span>   

    ![kluisreferenties downloaden is voltooid](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-hello-agent"></a><span data-ttu-id="f197b-193">Installeren en registreren Hallo-agent</span><span class="sxs-lookup"><span data-stu-id="f197b-193">Install and register hello agent</span></span>

> [!NOTE]
> <span data-ttu-id="f197b-194">Inschakelen back-ups via hello Azure-portal is nog niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="f197b-194">Enabling backup through hello Azure portal is not available, yet.</span></span> <span data-ttu-id="f197b-195">Gebruik Hallo Microsoft Azure Recovery Services Agent tooback van uw bestanden en mappen.</span><span class="sxs-lookup"><span data-stu-id="f197b-195">Use hello Microsoft Azure Recovery Services Agent tooback up your files and folders.</span></span>
>

1. <span data-ttu-id="f197b-196">Zoek en dubbelklik op Hallo **MARSagentinstaller.exe** vanuit Hallo Downloads map (of een andere locatie is opgeslagen).</span><span class="sxs-lookup"><span data-stu-id="f197b-196">Locate and double-click hello **MARSagentinstaller.exe** from hello Downloads folder (or other saved location).</span></span>

    <span data-ttu-id="f197b-197">Hallo-installatieprogramma biedt een reeks berichten zoals deze pakt wordt geïnstalleerd en geregistreerd Hallo Recovery Services-agent.</span><span class="sxs-lookup"><span data-stu-id="f197b-197">hello installer provides a series of messages as it extracts, installs, and registers hello Recovery Services agent.</span></span>

    ![uitvoeren van installatiereferenties van de Recovery Services-agent](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="f197b-199">Hallo Microsoft Azure Recovery Services Agent-installatiewizard voltooien.</span><span class="sxs-lookup"><span data-stu-id="f197b-199">Complete hello Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="f197b-200">wizard toocomplete hello, moet u:</span><span class="sxs-lookup"><span data-stu-id="f197b-200">toocomplete hello wizard, you need to:</span></span>

   * <span data-ttu-id="f197b-201">Kies een locatie voor de installatie en cache map Hallo.</span><span class="sxs-lookup"><span data-stu-id="f197b-201">Choose a location for hello installation and cache folder.</span></span>
   * <span data-ttu-id="f197b-202">Geef uw proxyserveradres als u een proxy server tooconnect toohello serverinformatie internet.</span><span class="sxs-lookup"><span data-stu-id="f197b-202">Provide your proxy server info if you use a proxy server tooconnect toohello internet.</span></span>
   * <span data-ttu-id="f197b-203">Uw gebruikersnaam en wachtwoord invoeren als u gebruikmaakt van een geverifieerde proxyserver.</span><span class="sxs-lookup"><span data-stu-id="f197b-203">Provide your user name and password details if you use an authenticated proxy.</span></span>
   * <span data-ttu-id="f197b-204">Geef referenties op Hallo gedownload kluis</span><span class="sxs-lookup"><span data-stu-id="f197b-204">Provide hello downloaded vault credentials</span></span>
   * <span data-ttu-id="f197b-205">Hallo-wachtwoordzin voor versleuteling op een veilige locatie opslaan.</span><span class="sxs-lookup"><span data-stu-id="f197b-205">Save hello encryption passphrase in a secure location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="f197b-206">Als u kwijtraakt of Hallo wachtwoordzin vergeet, Microsoft u niet helpen Hallo back-upgegevens te herstellen.</span><span class="sxs-lookup"><span data-stu-id="f197b-206">If you lose or forget hello passphrase, Microsoft cannot help recover hello backup data.</span></span> <span data-ttu-id="f197b-207">Hallo-bestand opslaan in een veilige locatie.</span><span class="sxs-lookup"><span data-stu-id="f197b-207">Save hello file in a secure location.</span></span> <span data-ttu-id="f197b-208">Het is vereiste toorestore een back-up.</span><span class="sxs-lookup"><span data-stu-id="f197b-208">It is required toorestore a backup.</span></span>
     >
     >

<span data-ttu-id="f197b-209">Hallo-agent wordt nu geïnstalleerd en uw computer is ingeschreven toohello kluis.</span><span class="sxs-lookup"><span data-stu-id="f197b-209">hello agent is now installed and your machine is registered toohello vault.</span></span> <span data-ttu-id="f197b-210">U bent klaar tooconfigure en uw back-up plannen.</span><span class="sxs-lookup"><span data-stu-id="f197b-210">You're ready tooconfigure and schedule your backup.</span></span>

## <a name="network-and-connectivity-requirements"></a><span data-ttu-id="f197b-211">Netwerk- en verbindingsvereisten</span><span class="sxs-lookup"><span data-stu-id="f197b-211">Network and Connectivity Requirements</span></span>

<span data-ttu-id="f197b-212">Als uw machine/de proxy toegang tot internet beperkt heeft, moet u controleren of firewall-instellingen op Hallo mcahine/proxy geconfigureerde tooallow Hallo volgende URL's zijn:</span><span class="sxs-lookup"><span data-stu-id="f197b-212">If your machine/proxy has limited internet access, ensure that firewall settings on hello mcahine/proxy are configured tooallow hello following URLs:</span></span> <br>
    1. <span data-ttu-id="f197b-213">www.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="f197b-213">www.msftncsi.com</span></span>
    2. <span data-ttu-id="f197b-214">*.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="f197b-214">*.Microsoft.com</span></span>
    3. <span data-ttu-id="f197b-215">*.WindowsAzure.com</span><span class="sxs-lookup"><span data-stu-id="f197b-215">*.WindowsAzure.com</span></span>
    4. <span data-ttu-id="f197b-216">*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="f197b-216">*.microsoftonline.com</span></span>
    5. <span data-ttu-id="f197b-217">*.windows.ne</span><span class="sxs-lookup"><span data-stu-id="f197b-217">*.windows.ne</span></span>

## <a name="back-up-your-files-and-folders"></a><span data-ttu-id="f197b-218">Een back-up maken van uw bestanden en mappen</span><span class="sxs-lookup"><span data-stu-id="f197b-218">Back up your files and folders</span></span>
<span data-ttu-id="f197b-219">Hallo eerste back-up bevat twee belangrijke taken uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f197b-219">hello initial backup includes two key tasks:</span></span>

* <span data-ttu-id="f197b-220">Hallo back-up plannen</span><span class="sxs-lookup"><span data-stu-id="f197b-220">Schedule hello backup</span></span>
* <span data-ttu-id="f197b-221">Back-up van bestanden en mappen voor Hallo eerst</span><span class="sxs-lookup"><span data-stu-id="f197b-221">Back up files and folders for hello first time</span></span>

<span data-ttu-id="f197b-222">toocomplete hello eerste back-up, gebruik Hallo Microsoft Azure Recovery Services agent.</span><span class="sxs-lookup"><span data-stu-id="f197b-222">toocomplete hello initial backup, use hello Microsoft Azure Recovery Services agent.</span></span>

### <a name="tooschedule-hello-backup-job"></a><span data-ttu-id="f197b-223">back-uptaak van tooschedule Hallo</span><span class="sxs-lookup"><span data-stu-id="f197b-223">tooschedule hello backup job</span></span>
1. <span data-ttu-id="f197b-224">Open Hallo Microsoft Azure Recovery Services agent.</span><span class="sxs-lookup"><span data-stu-id="f197b-224">Open hello Microsoft Azure Recovery Services agent.</span></span> <span data-ttu-id="f197b-225">U vindt deze door te zoeken naar **Microsoft Azure Backup** op uw machine.</span><span class="sxs-lookup"><span data-stu-id="f197b-225">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Hello Azure Recovery Services-agent starten](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)
2. <span data-ttu-id="f197b-227">Klik in de Recovery Services-agent Hallo op **back-up plannen**.</span><span class="sxs-lookup"><span data-stu-id="f197b-227">In hello Recovery Services agent, click **Schedule Backup**.</span></span>

    ![Een back-up van de Windows Server plannen](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)
3. <span data-ttu-id="f197b-229">Op Hallo aan de slag pagina van de Wizard Back-up plannen hello, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="f197b-229">On hello Getting started page of hello Schedule Backup Wizard, click **Next**.</span></span>
4. <span data-ttu-id="f197b-230">Klik op Hallo Items selecteren tooBackup pagina op **Items toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="f197b-230">On hello Select Items tooBackup page, click **Add Items**.</span></span>
5. <span data-ttu-id="f197b-231">Selecteer Hallo bestanden en mappen die u wilt tooback en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="f197b-231">Select hello files and folders that you want tooback up, and then click **Okay**.</span></span>
6. <span data-ttu-id="f197b-232">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="f197b-232">Click **Next**.</span></span>
7. <span data-ttu-id="f197b-233">Op Hallo **back-upschema specificeren** pagina, geeft u Hallo **back-upschema** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="f197b-233">On hello **Specify Backup Schedule** page, specify hello **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="f197b-234">U kunt dagelijkse back-ups (maximaal drie keer per dag en wekelijkse back-ups plannen.</span><span class="sxs-lookup"><span data-stu-id="f197b-234">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span></span>

    ![Items voor back-up van Windows Server](./media/backup-try-azure-backup-in-10-mins/specify-backup-schedule-close.png)

   > [!NOTE]
   > <span data-ttu-id="f197b-236">Zie voor meer informatie over hoe toospecify back-upschema Hallo Hallo artikel [met Azure Backup tooreplace uw tape-infrastructuur](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="f197b-236">For more information about how toospecify hello backup schedule, see hello article [Use Azure Backup tooreplace your tape infrastructure](backup-azure-backup-cloud-as-tape.md).</span></span>
   >

8. <span data-ttu-id="f197b-237">Op Hallo **retentiebeleid selecteren** pagina, selecteer Hallo **bewaarbeleid** voor Hallo back-up.</span><span class="sxs-lookup"><span data-stu-id="f197b-237">On hello **Select Retention Policy** page, select hello **Retention Policy** for hello backup copy.</span></span>

    <span data-ttu-id="f197b-238">Hallo het bewaarbeleid geeft aan hoe lang de back-upgegevens hello wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="f197b-238">hello retention policy specifies how long hello backup data is stored.</span></span> <span data-ttu-id="f197b-239">U kunt verschillende Bewaarbeleidsregels op basis van wanneer Hallo back-up opgeven in plaats van het opgeven van een 'plat beleid' voor alle back-punten.</span><span class="sxs-lookup"><span data-stu-id="f197b-239">Rather than specifying a “flat policy” for all backup points, you can specify different retention policies based on when hello backup occurs.</span></span> <span data-ttu-id="f197b-240">Uw behoeften, kunt u Hallo dagelijkse, wekelijkse, maandelijkse en jaarlijkse bewaren beleid toomeet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="f197b-240">You can modify hello daily, weekly, monthly, and yearly retention policies toomeet your needs.</span></span>
9. <span data-ttu-id="f197b-241">Kies op Hallo eerste back-uptype kiezen pagina Hallo-type voor eerste back-up.</span><span class="sxs-lookup"><span data-stu-id="f197b-241">On hello Choose Initial Backup Type page, choose hello initial backup type.</span></span> <span data-ttu-id="f197b-242">Hallo-optie ingesteld laat **automatisch via netwerk Hallo** geselecteerd en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="f197b-242">Leave hello option **Automatically over hello network** selected, and then click **Next**.</span></span>

    <span data-ttu-id="f197b-243">U kunt back-up automatisch via netwerk hello, of u offline back-ups.</span><span class="sxs-lookup"><span data-stu-id="f197b-243">You can back up automatically over hello network, or you can back up offline.</span></span> <span data-ttu-id="f197b-244">Hallo rest van dit artikel beschrijft Hallo-proces voor het automatisch een back-up maken.</span><span class="sxs-lookup"><span data-stu-id="f197b-244">hello remainder of this article describes hello process for backing up automatically.</span></span> <span data-ttu-id="f197b-245">Als u liever toodo een offline back-up, Hallo artikel lezen [Offline back-werkstroom in Azure Backup](backup-azure-backup-import-export.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f197b-245">If you prefer toodo an offline backup, review hello article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span></span>
10. <span data-ttu-id="f197b-246">Op de bevestigingspagina Hallo Hallo informatie bekijken en klik vervolgens op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="f197b-246">On hello Confirmation page, review hello information, and then click **Finish**.</span></span>
11. <span data-ttu-id="f197b-247">Nadat het Hallo-wizard is voltooid voor het maken van back-upschema hello, klikt u op **sluiten**.</span><span class="sxs-lookup"><span data-stu-id="f197b-247">After hello wizard finishes creating hello backup schedule, click **Close**.</span></span>

### <a name="tooback-up-files-and-folders-for-hello-first-time"></a><span data-ttu-id="f197b-248">tooback van bestanden en mappen voor de eerste keer Hallo</span><span class="sxs-lookup"><span data-stu-id="f197b-248">tooback up files and folders for hello first time</span></span>
1. <span data-ttu-id="f197b-249">Klik in het Hallo Recovery Services-agent op **Back-Up uit** toocomplete Hallo eerste seeding via Hallo netwerk.</span><span class="sxs-lookup"><span data-stu-id="f197b-249">In hello Recovery Services agent, click **Back Up Now** toocomplete hello initial seeding over hello network.</span></span>

    ![Nu back-up maken van Windows Server](./media/backup-try-azure-backup-in-10-mins/backup-now.png)
2. <span data-ttu-id="f197b-251">Op de bevestigingspagina Hallo revisie Hallo-instellingen die de Wizard Back-Up nu Hallo tooback Hallo machine gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f197b-251">On hello Confirmation page, review hello settings that hello Back Up Now Wizard will use tooback up hello machine.</span></span> <span data-ttu-id="f197b-252">Klik vervolgens op **Back-up maken**.</span><span class="sxs-lookup"><span data-stu-id="f197b-252">Then click **Back Up**.</span></span>
3. <span data-ttu-id="f197b-253">Klik op **sluiten** tooclose Hallo-wizard.</span><span class="sxs-lookup"><span data-stu-id="f197b-253">Click **Close** tooclose hello wizard.</span></span> <span data-ttu-id="f197b-254">Als u Hallo wizard sluit voordat de back-upproces Hallo is voltooid, blijft Hallo wizard toorun op Hallo achtergrond.</span><span class="sxs-lookup"><span data-stu-id="f197b-254">If you close hello wizard before hello backup process finishes, hello wizard continues toorun in hello background.</span></span>

<span data-ttu-id="f197b-255">Nadat de eerste back-up Hallo is voltooid, Hallo **taak voltooid** status wordt weergegeven in Hallo back-up-console.</span><span class="sxs-lookup"><span data-stu-id="f197b-255">After hello initial backup is completed, hello **Job completed** status appears in hello Backup console.</span></span>

![IR voltooid](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="questions"></a><span data-ttu-id="f197b-257">Vragen?</span><span class="sxs-lookup"><span data-stu-id="f197b-257">Questions?</span></span>
<span data-ttu-id="f197b-258">Als u vragen hebt of als er een functie die u toosee opgenomen wilt, [Stuur ons feedback](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="f197b-258">If you have questions, or if there is any feature that you would like toosee included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f197b-259">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f197b-259">Next steps</span></span>
* <span data-ttu-id="f197b-260">Meer informatie over [back-ups maken van Windows-machines](backup-configure-vault.md).</span><span class="sxs-lookup"><span data-stu-id="f197b-260">Get more details about [backing up Windows machines](backup-configure-vault.md).</span></span>
* <span data-ttu-id="f197b-261">Wanneer u eenmaal een back-up hebt gemaakt van uw bestanden en mappen, kunt u [uw kluizen en servers beheren](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="f197b-261">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="f197b-262">Als u een back-up toorestore moet, gebruikt u in dit artikel te[bestanden tooa Windows-machine herstellen](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="f197b-262">If you need toorestore a backup, use this article too[restore files tooa Windows machine](backup-azure-restore-windows-server.md).</span></span>
