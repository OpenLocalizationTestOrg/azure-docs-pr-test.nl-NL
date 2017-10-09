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
# <a name="back-up-a-windows-server-or-client-tooazure-using-hello-resource-manager-deployment-model"></a><span data-ttu-id="8e0fe-105">Back-up van een Windows Server of client tooAzure met Hallo Resource Manager-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="8e0fe-105">Back up a Windows Server or client tooAzure using hello Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8e0fe-106">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="8e0fe-106">Azure portal</span></span>](backup-configure-vault.md)
> * [<span data-ttu-id="8e0fe-107">Klassieke portal</span><span class="sxs-lookup"><span data-stu-id="8e0fe-107">Classic portal</span></span>](backup-configure-vault-classic.md)
>
>

<span data-ttu-id="8e0fe-108">Dit artikel wordt uitgelegd hoe de bestanden en mappen tooAzure tooback van uw Windows Server (of Windows-client) met het gebruik van Azure Backup Hallo Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-108">This article explains how tooback up your Windows Server (or Windows client) files and folders tooAzure with Azure Backup using hello Resource Manager deployment model.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/backup-deployment-models.md)]

![Back-upproces stappen](./media/backup-configure-vault/initial-backup-process.png)

## <a name="before-you-start"></a><span data-ttu-id="8e0fe-110">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="8e0fe-110">Before you start</span></span>
<span data-ttu-id="8e0fe-111">tooback u een server of client tooAzure, moet u een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-111">tooback up a server or client tooAzure, you need an Azure account.</span></span> <span data-ttu-id="8e0fe-112">Als u niet hebt, kunt u een [gratis account](https://azure.microsoft.com/free/) binnen een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-112">If you don't have one, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="8e0fe-113">Een Recovery Services-kluis maken</span><span class="sxs-lookup"><span data-stu-id="8e0fe-113">Create a Recovery Services vault</span></span>
<span data-ttu-id="8e0fe-114">Een Recovery Services-kluis is een entiteit waarmee alle Hallo back-ups en herstelpunten die u gedurende een bepaalde periode maakt zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-114">A Recovery Services vault is an entity that stores all hello backups and recovery points you create over time.</span></span> <span data-ttu-id="8e0fe-115">Hallo Recovery Services-kluis bevat ook Hallo back-upbeleid toegepast toohello beveiligde bestanden en mappen.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-115">hello Recovery Services vault also contains hello backup policy applied toohello protected files and folders.</span></span> <span data-ttu-id="8e0fe-116">Wanneer u een Recovery Services-kluis maakt, moet u ook de juiste opslagoptie redundantie Hallo selecteren.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-116">When you create a Recovery Services vault, you should also select hello appropriate storage redundancy option.</span></span>

### <a name="toocreate-a-recovery-services-vault"></a><span data-ttu-id="8e0fe-117">toocreate een Recovery Services-kluis</span><span class="sxs-lookup"><span data-stu-id="8e0fe-117">toocreate a Recovery Services vault</span></span>
1. <span data-ttu-id="8e0fe-118">Als u dit nog niet hebt gedaan, meld u aan toohello [Azure Portal](https://portal.azure.com/) met behulp van uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-118">If you haven't already done so, sign in toohello [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="8e0fe-119">Klik op het menu Hub Hallo **meer services** en typt u in de lijst met resources Hallo **Recovery Services** en klik op **Recovery Services-kluizen**.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-119">On hello Hub menu, click **More services** and in hello list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Een Recovery Services-kluis maken, stap 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="8e0fe-121">Als er recovery services-kluizen in Hallo abonnement, worden Hallo kluizen weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-121">If there are recovery services vaults in hello subscription, hello vaults are listed.</span></span>

3. <span data-ttu-id="8e0fe-122">Op Hallo **Recovery Services-kluizen** menu, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-122">On hello **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Een Recovery Services-kluis maken, stap 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="8e0fe-124">Hallo Recovery Services vault blade wordt geopend, waarin u wordt gevraagd tooprovide een **naam**, **abonnement**, **resourcegroep**, en **locatie**.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-124">hello Recovery Services vault blade opens, prompting you tooprovide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Een Recovery Services-kluis maken, stap 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="8e0fe-126">Voor **naam**, voer een beschrijvende naam tooidentify Hallo-kluis.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-126">For **Name**, enter a friendly name tooidentify hello vault.</span></span> <span data-ttu-id="8e0fe-127">de naam van de Hallo moet toobe unieke voor hello Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-127">hello name needs toobe unique for hello Azure subscription.</span></span> <span data-ttu-id="8e0fe-128">Typ een naam die tussen 2 en 50 tekens bevat.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-128">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="8e0fe-129">De naam moet beginnen met een letter en mag alleen letters, cijfers en afbreekstreepjes bevatten.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-129">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="8e0fe-130">In Hallo **abonnement** sectie, gebruikt u Hallo vervolgkeuzelijst toochoose hello Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-130">In hello **Subscription** section, use hello drop-down menu toochoose hello Azure subscription.</span></span> <span data-ttu-id="8e0fe-131">Als u slechts één abonnement, dat abonnement wordt weergegeven en kunt u de volgende stap toohello overslaan.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-131">If you use only one subscription, that subscription appears and you can skip toohello next step.</span></span> <span data-ttu-id="8e0fe-132">Als u niet zeker weet welk abonnement toouse Hallo standaard gebruiken (of voorgestelde) abonnement.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-132">If you are not sure which subscription toouse, use hello default (or suggested) subscription.</span></span> <span data-ttu-id="8e0fe-133">Er zijn alleen meerdere mogelijkheden als uw organisatieaccount is gekoppeld aan meerdere Azure-abonnementen.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-133">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="8e0fe-134">In Hallo **resourcegroep** sectie:</span><span class="sxs-lookup"><span data-stu-id="8e0fe-134">In hello **Resource group** section:</span></span>

    * <span data-ttu-id="8e0fe-135">Selecteer **nieuw** als u wilt dat toocreate een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-135">select **Create new** if you want toocreate a new Resource group.</span></span>
    <span data-ttu-id="8e0fe-136">of</span><span class="sxs-lookup"><span data-stu-id="8e0fe-136">Or</span></span>
    * <span data-ttu-id="8e0fe-137">Selecteer **gebruik bestaande** en klik op Hallo vervolgkeuzelijst toosee Hallo lijst met beschikbare resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-137">select **Use existing** and click hello drop-down menu toosee hello available list of Resource groups.</span></span>

  <span data-ttu-id="8e0fe-138">Zie voor meer informatie over resourcegroepen Hallo [overzicht van Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8e0fe-138">For complete information on Resource groups, see hello [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="8e0fe-139">Klik op **locatie** tooselect Hallo geografische regio voor Hallo kluis.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-139">Click **Location** tooselect hello geographic region for hello vault.</span></span> <span data-ttu-id="8e0fe-140">Deze keuze bepaalt Hallo geografische regio waar uw back-upgegevens worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-140">This choice determines hello geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="8e0fe-141">Aan de onderkant van de Hallo van blade Hallo Recovery Services-kluis, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-141">At hello bottom of hello Recovery Services vault blade, click **Create**.</span></span>

  <span data-ttu-id="8e0fe-142">Het kan enkele minuten duren voordat Hallo die Recovery Services-kluis toobe gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-142">It can take several minutes for hello Recovery Services vault toobe created.</span></span> <span data-ttu-id="8e0fe-143">Hallo statusmeldingen rechtsboven Hallo van Hallo portal bewaken.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-143">Monitor hello status notifications in hello upper right-hand area of hello portal.</span></span> <span data-ttu-id="8e0fe-144">Zodra de kluis is gemaakt, wordt deze weergegeven in de lijst met Recovery Services-kluizen Hallo.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-144">Once your vault is created, it appears in hello list of Recovery Services vaults.</span></span> <span data-ttu-id="8e0fe-145">Als u uw kluis na enkele minuten niet ziet, klik dan op **Vernieuwen**.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-145">If after several minutes you don't see your vault, click **Refresh**.</span></span>

  ![Op de knop Vernieuwen klikken](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

  <span data-ttu-id="8e0fe-147">Nadat u uw kluis in Hallo lijst met Recovery Services-kluizen ziet, bent u klaar tooset Hallo opslag redundantie.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-147">Once you see your vault in hello list of Recovery Services vaults, you are ready tooset hello storage redundancy.</span></span>


### <a name="set-storage-redundancy"></a><span data-ttu-id="8e0fe-148">Redundantie van gegevensopslag instellen</span><span class="sxs-lookup"><span data-stu-id="8e0fe-148">Set storage redundancy</span></span>
<span data-ttu-id="8e0fe-149">Als u voor het eerst een Recovery Services-kluis maakt, bepaalt u hoe uw opslag wordt gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-149">When you first create a Recovery Services vault you determine how storage is replicated.</span></span>

1. <span data-ttu-id="8e0fe-150">Van Hallo **Recovery Services-kluizen** blade, klikt u op de nieuwe kluis Hallo.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-150">From hello **Recovery Services vaults** blade, click hello new vault.</span></span>

    ![Selecteer Hallo nieuwe kluis in Hallo-lijst met Recovery Services-kluis](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="8e0fe-152">Wanneer u Hallo kluis selecteert, Hallo **Recovery Services-kluis** blade overzicht en de blade instellingen hello (*die Hallo-naam van de kluis Hallo Hallo boven heeft*) en Hallo details blade kluis openen.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-152">When you select hello vault, hello **Recovery Services vault** blade narrows, and hello Settings blade (*which has hello name of hello vault at hello top*) and hello vault details blade open.</span></span>

    ![Het Hallo-opslagconfiguratie weergeven voor nieuwe kluis](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)

2. <span data-ttu-id="8e0fe-154">Op de blade instellingen Hallo nieuwe kluis, Hallo verticale dia tooscroll omlaag toohello sectie beheren en op **back-upinfrastructuur**.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-154">In hello new vault's Settings blade, use hello vertical slide tooscroll down toohello Manage section, and click **Backup Infrastructure**.</span></span>

  <span data-ttu-id="8e0fe-155">Hallo back-upinfrastructuur blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-155">hello Backup Infrastructure blade opens.</span></span>

3. <span data-ttu-id="8e0fe-156">Klik op Hallo back-upinfrastructuur blade **back-upconfiguratie** tooopen hello **back-upconfiguratie** blade.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-156">In hello Backup Infrastructure blade, click **Backup Configuration** tooopen hello **Backup Configuration** blade.</span></span>

  ![De opslagconfiguratie Hallo voor nieuwe kluis instellen](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)

4. <span data-ttu-id="8e0fe-158">Kies Hallo geschikte optie voor opslagreplicatie voor uw kluis.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-158">Choose hello appropriate storage replication option for your vault.</span></span>

  ![keuzes bij opslagconfiguratie](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

  <span data-ttu-id="8e0fe-160">Uw kluis heeft standaard geografisch redundante opslag.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-160">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="8e0fe-161">Als u Azure als een eindpunt primaire back-upopslag gebruikt, gaat u verder toouse **geografisch redundante**.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-161">If you use Azure as a primary backup storage endpoint, continue toouse **Geo-redundant**.</span></span> <span data-ttu-id="8e0fe-162">Als u geen Azure als een eindpunt primaire back-upopslag gebruikt, kiest u **lokaal redundante**, die zorgt voor lagere kosten voor hello Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-162">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces hello Azure storage costs.</span></span> <span data-ttu-id="8e0fe-163">U vindt meer informatie over de opties voor [geografisch redundante](../storage/common/storage-redundancy.md#geo-redundant-storage) en [lokaal redundante ](../storage/common/storage-redundancy.md#locally-redundant-storage) opslag in dit [overzicht van opslagredundantie](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="8e0fe-163">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="8e0fe-164">Nu dat u kunt een kluis hebt gemaakt, het voorbereiden van uw infrastructuur tooback van bestanden en mappen door te downloaden en installeren Hallo Microsoft Azure Recovery Services agent, kluisreferenties downloaden en met behulp van deze agent referenties tooregister Hallo met Hallo-kluis.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-164">Now that you've created a vault, prepare your infrastructure tooback up files and folders by downloading and installing hello Microsoft Azure Recovery Services agent, downloading vault credentials, and then using those credentials tooregister hello agent with hello vault.</span></span>

## <a name="configure-hello-vault"></a><span data-ttu-id="8e0fe-165">Hallo kluis configureren</span><span class="sxs-lookup"><span data-stu-id="8e0fe-165">Configure hello vault</span></span>

1. <span data-ttu-id="8e0fe-166">Op de blade van de Recovery Services-kluis (voor Hallo kluis u zojuist hebt gemaakt), in de sectie aan de slag Hallo Hallo, klikt u op **back-up**, vervolgens op Hallo **aan de slag met back-up** blade Selecteer  **Back-updoel**.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-166">On hello Recovery Services vault blade (for hello vault you just created), in hello Getting Started section, click **Backup**, then on hello **Getting Started with Backup** blade, select **Backup goal**.</span></span>

  ![Open de blade back-updoelstelling](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

  <span data-ttu-id="8e0fe-168">Hallo **back-updoel** blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-168">hello **Backup Goal** blade opens.</span></span> <span data-ttu-id="8e0fe-169">Als de Recovery Services-kluis Hallo eerder is geconfigureerd, Hallo **back-updoel** blades geopend wanneer u klikt op **back-up** blade op Hallo Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-169">If hello Recovery Services vault has been previously configured, then hello **Backup Goal** blades opens when you click **Backup** on hello Recovery Services vault blade.</span></span>

  ![Open de blade back-updoelstelling](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="8e0fe-171">Van Hallo **waar wordt uw workload uitgevoerd?** vervolgkeuzelijst, selecteer **On-premises**.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-171">From hello **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

  <span data-ttu-id="8e0fe-172">U kiest **On-premises** omdat uw Windows Server of Windows-computer een fysieke machine is die zich niet in Azure bevindt.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-172">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="8e0fe-173">Van Hallo **wat wilt u wilt dat toobackup?** selecteert u **bestanden en mappen**, en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-173">From hello **What do you want toobackup?** menu, select **Files and folders**, and click **OK**.</span></span>

  ![Bestanden en mappen configureren](./media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

  <span data-ttu-id="8e0fe-175">Als u op OK klikt, verschijnt een vinkje volgende te**back-updoel**, en Hallo **infrastructuur voorbereiden** blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-175">After clicking OK, a checkmark appears next too**Backup goal**, and hello **Prepare infrastructure** blade opens.</span></span>

  ![Nu de back-updoelstelling is geconfigureerd, gaat u de infrastructuur voorbereiden](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="8e0fe-177">Op Hallo **infrastructuur voorbereiden** blade, klikt u op **Agent downloaden voor Windows Server of Windows Client**.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-177">On hello **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

  ![infrastructuur voorbereiden](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

  <span data-ttu-id="8e0fe-179">Als u van Windows Server essentiële gebruikmaakt, kiest u toodownload Hallo-agent voor Windows Server essentieel.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-179">If you are using Windows Server Essential, then choose toodownload hello agent for Windows Server Essential.</span></span> <span data-ttu-id="8e0fe-180">Een pop-upmenu vraagt u toorun of MARSAgentInstaller.exe opslaan.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-180">A pop-up menu prompts you toorun or save MARSAgentInstaller.exe.</span></span>

  ![Dialoogvenster MARSAgentInstaller](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="8e0fe-182">In het pop-upmenu Hallo downloaden, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-182">In hello download pop-up menu, click **Save**.</span></span>

  <span data-ttu-id="8e0fe-183">Standaard Hallo **MARSagentinstaller.exe** bestand tooyour downloadmap wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-183">By default, hello **MARSagentinstaller.exe** file is saved tooyour Downloads folder.</span></span> <span data-ttu-id="8e0fe-184">Als het Hallo-installatieprogramma is voltooid, ziet u een pop-upvenster waarin wordt gevraagd als u toorun Hallo installatieprogramma wilt of Hallo-map open.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-184">When hello installer completes, you will see a pop-up asking if you want toorun hello installer, or open hello folder.</span></span>

  ![infrastructuur voorbereiden](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

  <span data-ttu-id="8e0fe-186">U hoeft niet tooinstall Hallo agent nog.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-186">You don't need tooinstall hello agent yet.</span></span> <span data-ttu-id="8e0fe-187">Nadat u de kluisreferenties Hallo hebt gedownload, kunt u Hallo-agent installeren.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-187">You can install hello agent after you have downloaded hello vault credentials.</span></span>

6. <span data-ttu-id="8e0fe-188">Op Hallo **infrastructuur voorbereiden** blade, klikt u op **downloaden**.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-188">On hello **Prepare infrastructure** blade, click **Download**.</span></span>

  ![kluisreferenties downloaden](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

  <span data-ttu-id="8e0fe-190">de map Downloads tooyour downloaden Hello kluisreferenties</span><span class="sxs-lookup"><span data-stu-id="8e0fe-190">hello vault credentials download tooyour Downloads folder.</span></span> <span data-ttu-id="8e0fe-191">Nadat de kluisreferenties Hallo downloaden, ziet u een pop-upvenster waarin wordt gevraagd als u wilt dat tooopen of Hallo referenties op te slaan.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-191">After hello vault credentials finish downloading, you see a pop-up asking if you want tooopen or save hello credentials.</span></span> <span data-ttu-id="8e0fe-192">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-192">Click **Save**.</span></span> <span data-ttu-id="8e0fe-193">Als u per ongeluk op **Open**, laten Hallo dialoogvenster waarmee wordt geprobeerd tooopen hello kluisreferenties, mislukken.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-193">If you accidentally click **Open**, let hello dialog that attempts tooopen hello vault credentials, fail.</span></span> <span data-ttu-id="8e0fe-194">U kunt de kluisreferenties Hallo niet openen.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-194">You cannot open hello vault credentials.</span></span> <span data-ttu-id="8e0fe-195">De volgende stap toohello worden voortgezet.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-195">Proceed toohello next step.</span></span> <span data-ttu-id="8e0fe-196">Hallo kluisreferenties zijn in de map Downloads Hallo.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-196">hello vault credentials are in hello Downloads folder.</span></span>   

  ![kluisreferenties downloaden is voltooid](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-hello-agent"></a><span data-ttu-id="8e0fe-198">Installeren en registreren Hallo-agent</span><span class="sxs-lookup"><span data-stu-id="8e0fe-198">Install and register hello agent</span></span>

> [!NOTE]
> <span data-ttu-id="8e0fe-199">Inschakelen back-ups via hello Azure-portal is nog niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-199">Enabling backup through hello Azure portal is not available, yet.</span></span> <span data-ttu-id="8e0fe-200">Gebruik Hallo Microsoft Azure Recovery Services Agent tooback van uw bestanden en mappen.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-200">Use hello Microsoft Azure Recovery Services Agent tooback up your files and folders.</span></span>
>

1. <span data-ttu-id="8e0fe-201">Zoek en dubbelklik op Hallo **MARSagentinstaller.exe** vanuit Hallo Downloads map (of een andere locatie is opgeslagen).</span><span class="sxs-lookup"><span data-stu-id="8e0fe-201">Locate and double-click hello **MARSagentinstaller.exe** from hello Downloads folder (or other saved location).</span></span>

  <span data-ttu-id="8e0fe-202">Hallo-installatieprogramma biedt een reeks berichten zoals deze pakt wordt geïnstalleerd en geregistreerd Hallo Recovery Services-agent.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-202">hello installer provides a series of messages as it extracts, installs, and registers hello Recovery Services agent.</span></span>

  ![uitvoeren van installatiereferenties van de Recovery Services-agent](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="8e0fe-204">Hallo Microsoft Azure Recovery Services Agent-installatiewizard voltooien.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-204">Complete hello Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="8e0fe-205">wizard toocomplete hello, moet u:</span><span class="sxs-lookup"><span data-stu-id="8e0fe-205">toocomplete hello wizard, you need to:</span></span>

  * <span data-ttu-id="8e0fe-206">Kies een locatie voor de installatie en cache map Hallo.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-206">Choose a location for hello installation and cache folder.</span></span>
  * <span data-ttu-id="8e0fe-207">Geef uw proxyserveradres als u een proxy server tooconnect toohello serverinformatie internet.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-207">Provide your proxy server info if you use a proxy server tooconnect toohello internet.</span></span>
  * <span data-ttu-id="8e0fe-208">Uw gebruikersnaam en wachtwoord invoeren als u gebruikmaakt van een geverifieerde proxyserver.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-208">Provide your user name and password details if you use an authenticated proxy.</span></span>
  * <span data-ttu-id="8e0fe-209">Geef referenties op Hallo gedownload kluis</span><span class="sxs-lookup"><span data-stu-id="8e0fe-209">Provide hello downloaded vault credentials</span></span>
  * <span data-ttu-id="8e0fe-210">Hallo-wachtwoordzin voor versleuteling op een veilige locatie opslaan.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-210">Save hello encryption passphrase in a secure location.</span></span>

  > [!NOTE]
  > <span data-ttu-id="8e0fe-211">Als u kwijtraakt of Hallo wachtwoordzin vergeet, Microsoft u niet helpen Hallo back-upgegevens te herstellen.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-211">If you lose or forget hello passphrase, Microsoft cannot help recover hello backup data.</span></span> <span data-ttu-id="8e0fe-212">Hallo-bestand opslaan in een veilige locatie.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-212">Save hello file in a secure location.</span></span> <span data-ttu-id="8e0fe-213">Het is vereiste toorestore een back-up.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-213">It is required toorestore a backup.</span></span>
  >
  >

<span data-ttu-id="8e0fe-214">Hallo-agent wordt nu geïnstalleerd en uw computer is ingeschreven toohello kluis.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-214">hello agent is now installed and your machine is registered toohello vault.</span></span> <span data-ttu-id="8e0fe-215">U bent klaar tooconfigure en uw back-up plannen.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-215">You're ready tooconfigure and schedule your backup.</span></span>

## <a name="network-and-connectivity-requirements"></a><span data-ttu-id="8e0fe-216">Netwerk- en verbindingsvereisten</span><span class="sxs-lookup"><span data-stu-id="8e0fe-216">Network and Connectivity Requirements</span></span>

<span data-ttu-id="8e0fe-217">Als uw machine/de proxy toegang tot internet beperkt heeft, moet u controleren of firewall-instellingen op Hallo machine/proxy geconfigureerde tooallow Hallo volgende URL's zijn:</span><span class="sxs-lookup"><span data-stu-id="8e0fe-217">If your machine/proxy has limited internet access, ensure that firewall settings on hello machine/proxy are configured tooallow hello following URLs:</span></span> <br>
    1. <span data-ttu-id="8e0fe-218">www.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="8e0fe-218">www.msftncsi.com</span></span>
    2. <span data-ttu-id="8e0fe-219">*.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="8e0fe-219">*.Microsoft.com</span></span>
    3. <span data-ttu-id="8e0fe-220">*.WindowsAzure.com</span><span class="sxs-lookup"><span data-stu-id="8e0fe-220">*.WindowsAzure.com</span></span>
    4. <span data-ttu-id="8e0fe-221">*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="8e0fe-221">*.microsoftonline.com</span></span>
    5. <span data-ttu-id="8e0fe-222">*.windows.ne</span><span class="sxs-lookup"><span data-stu-id="8e0fe-222">*.windows.ne</span></span>


## <a name="create-hello-backup-policy"></a><span data-ttu-id="8e0fe-223">Hallo back-upbeleid maken</span><span class="sxs-lookup"><span data-stu-id="8e0fe-223">Create hello backup policy</span></span>
<span data-ttu-id="8e0fe-224">back-upbeleid Hallo is Hallo planning wanneer herstelpunten zijn gemaakt en Hallo tijdsduur Hallo herstelpunten worden bewaard.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-224">hello backup policy is hello schedule when recovery points are taken, and hello length of time hello recovery points are retained.</span></span> <span data-ttu-id="8e0fe-225">Gebruik Hallo Microsoft Azure Backup agent toocreate Hallo back-upbeleid voor bestanden en mappen.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-225">Use hello Microsoft Azure Backup agent toocreate hello backup policy for files and folders.</span></span>

### <a name="toocreate-a-backup-schedule"></a><span data-ttu-id="8e0fe-226">een back-upschema toocreate</span><span class="sxs-lookup"><span data-stu-id="8e0fe-226">toocreate a backup schedule</span></span>
1. <span data-ttu-id="8e0fe-227">Open Hallo Microsoft Azure backup-agent.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-227">Open hello Microsoft Azure Backup agent.</span></span> <span data-ttu-id="8e0fe-228">U vindt deze door te zoeken naar **Microsoft Azure Backup** op uw machine.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-228">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Hello Azure backup-agent starten](./media/backup-configure-vault/snap-in-search.png)
2. <span data-ttu-id="8e0fe-230">In Hallo backup-agent **acties** deelvenster, klikt u op **back-up plannen** toolaunch Hallo de Wizard Back-up plannen.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-230">In hello Backup agent's **Actions** pane, click **Schedule Backup** toolaunch hello Schedule Backup Wizard.</span></span>

    ![Een back-up van de Windows Server plannen](./media/backup-configure-vault/schedule-first-backup.png)

3. <span data-ttu-id="8e0fe-232">Op Hallo **aan de slag** pagina Hallo Wizard Back-up plannen, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-232">On hello **Getting started** page of hello Schedule Backup Wizard, click **Next**.</span></span>
4. <span data-ttu-id="8e0fe-233">Op Hallo **Items selecteren tooBackup** pagina, klikt u op **Items toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-233">On hello **Select Items tooBackup** page, click **Add Items**.</span></span>

  <span data-ttu-id="8e0fe-234">Hallo Items selecteren dialoogvenster wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-234">hello Select Items dialog opens.</span></span>

5. <span data-ttu-id="8e0fe-235">Selecteer Hallo bestanden en mappen wilt tooprotect en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-235">Select hello files and folders that you want tooprotect, and then click **OK**.</span></span>
6. <span data-ttu-id="8e0fe-236">In Hallo **Items selecteren tooBackup** pagina, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-236">In hello **Select Items tooBackup** page, click **Next**.</span></span>
7. <span data-ttu-id="8e0fe-237">Op Hallo **back-upschema specificeren** pagina, geeft u de back-upschema Hallo en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-237">On hello **Specify Backup Schedule** page, specify hello backup schedule and click **Next**.</span></span>

    <span data-ttu-id="8e0fe-238">U kunt dagelijkse back-ups (maximaal drie keer per dag en wekelijkse back-ups plannen.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-238">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span></span>

    ![Items voor back-up van Windows Server](./media/backup-configure-vault/specify-backup-schedule-close.png)

   > [!NOTE]
   > <span data-ttu-id="8e0fe-240">Zie voor meer informatie over hoe toospecify back-upschema Hallo Hallo artikel [met Azure Backup tooreplace uw tape-infrastructuur](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="8e0fe-240">For more information about how toospecify hello backup schedule, see hello article [Use Azure Backup tooreplace your tape infrastructure](backup-azure-backup-cloud-as-tape.md).</span></span>
   >
   >

8. <span data-ttu-id="8e0fe-241">Op Hallo **retentiebeleid selecteren** up Hallo specifieke bewaren beleidsregels Hallo voor back-up Hallo kiezen en op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-241">On hello **Select Retention Policy** page, choose hello specific retention policies hello for hello backup copy and click **Next**.</span></span>

    <span data-ttu-id="8e0fe-242">Hallo bewaarbeleid geeft Hallo duur welke Hallo back-up is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-242">hello retention policy specifies hello duration which hello backup is stored.</span></span> <span data-ttu-id="8e0fe-243">In plaats van alleen 'plat beleid' voor alle back-uppunten geven, kunt u verschillende Bewaarbeleidsregels op basis van wanneer Hallo back-up.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-243">Rather than just specifying a “flat policy” for all backup points, you can specify different retention policies based on when hello backup occurs.</span></span> <span data-ttu-id="8e0fe-244">Uw behoeften, kunt u Hallo dagelijkse, wekelijkse, maandelijkse en jaarlijkse bewaren beleid toomeet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-244">You can modify hello daily, weekly, monthly, and yearly retention policies toomeet your needs.</span></span>
9. <span data-ttu-id="8e0fe-245">Kies op Hallo eerste back-uptype kiezen pagina Hallo-type voor eerste back-up.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-245">On hello Choose Initial Backup Type page, choose hello initial backup type.</span></span> <span data-ttu-id="8e0fe-246">Hallo-optie ingesteld laat **automatisch via netwerk Hallo** geselecteerd en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-246">Leave hello option **Automatically over hello network** selected, and then click **Next**.</span></span>

    <span data-ttu-id="8e0fe-247">U kunt back-up automatisch via netwerk hello, of u offline back-ups.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-247">You can back up automatically over hello network, or you can back up offline.</span></span> <span data-ttu-id="8e0fe-248">Hallo rest van dit artikel beschrijft Hallo-proces voor het automatisch een back-up maken.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-248">hello remainder of this article describes hello process for backing up automatically.</span></span> <span data-ttu-id="8e0fe-249">Als u liever toodo een offline back-up, Hallo artikel lezen [Offline back-werkstroom in Azure Backup](backup-azure-backup-import-export.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-249">If you prefer toodo an offline backup, review hello article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span></span>
10. <span data-ttu-id="8e0fe-250">Op de bevestigingspagina Hallo Hallo informatie bekijken en klik vervolgens op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-250">On hello Confirmation page, review hello information, and then click **Finish**.</span></span>
11. <span data-ttu-id="8e0fe-251">Nadat het Hallo-wizard is voltooid voor het maken van back-upschema hello, klikt u op **sluiten**.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-251">After hello wizard finishes creating hello backup schedule, click **Close**.</span></span>

### <a name="enable-network-throttling"></a><span data-ttu-id="8e0fe-252">Netwerkbeperking inschakelen</span><span class="sxs-lookup"><span data-stu-id="8e0fe-252">Enable network throttling</span></span>
<span data-ttu-id="8e0fe-253">Hallo Microsoft Azure Backup agent biedt netwerkbeperking.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-253">hello Microsoft Azure Backup agent provides network throttling.</span></span> <span data-ttu-id="8e0fe-254">Gebeurtenisbeperking bepaalt hoe de netwerkbandbreedte tijdens de gegevensoverdracht wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-254">Throttling controls how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="8e0fe-255">Dit besturingselement kan nuttig zijn als u tooback van gegevens tijdens werkuren nodig maar niet dat Hallo back-upproces toointerfere met andere internetverkeer wilt.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-255">This control can be helpful if you need tooback up data during work hours but do not want hello backup process toointerfere with other Internet traffic.</span></span> <span data-ttu-id="8e0fe-256">Beperking van toepassing is tooback up- en herstelbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-256">Throttling applies tooback up and restore activities.</span></span>

> [!NOTE]
> <span data-ttu-id="8e0fe-257">Netwerkbeperking is niet beschikbaar op Windows Server 2008 R2 SP1, Windows Server 2008 SP2 of Windows 7 (met servicepacks).</span><span class="sxs-lookup"><span data-stu-id="8e0fe-257">Network throttling is not available on Windows Server 2008 R2 SP1, Windows Server 2008 SP2, or Windows 7 (with service packs).</span></span> <span data-ttu-id="8e0fe-258">Quality of Service (QoS) stelt Hello Azure Backup netwerkbeperking functie op Hallo lokale besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-258">hello Azure Backup network throttling feature engages Quality of Service (QoS) on hello local operating system.</span></span> <span data-ttu-id="8e0fe-259">Hoewel Azure back-up kan deze besturingssystemen beveiligen kunt, werkt niet met Azure Backup netwerkbeperking Hallo-versie van QoS beschikbaar op deze platforms.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-259">Though Azure Backup can protect these operating systems, hello version of QoS available on these platforms doesn't work with Azure Backup network throttling.</span></span> <span data-ttu-id="8e0fe-260">Netwerkbeperking kan worden gebruikt voor alle andere [ondersteunde besturingssystemen](backup-azure-backup-faq.md).</span><span class="sxs-lookup"><span data-stu-id="8e0fe-260">Network throttling can be used on all other [supported operating systems](backup-azure-backup-faq.md).</span></span>
>
>

<span data-ttu-id="8e0fe-261">**netwerkbeperking tooenable**</span><span class="sxs-lookup"><span data-stu-id="8e0fe-261">**tooenable network throttling**</span></span>

1. <span data-ttu-id="8e0fe-262">Klik in de Microsoft Azure Backup-agent Hallo **eigenschappen wijzigen**.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-262">In hello Microsoft Azure Backup agent, click **Change Properties**.</span></span>

    ![Eigenschappen wijzigen](./media/backup-configure-vault/change-properties.png)
2. <span data-ttu-id="8e0fe-264">Op Hallo **bandbreedtebeperking** tabblad, selecteer Hallo **inschakelen voor gebruik van internetbandbreedte voor back-upbewerkingen** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-264">On hello **Throttling** tab, select hello **Enable internet bandwidth usage throttling for backup operations** check box.</span></span>

    ![Netwerkbeperking](./media/backup-configure-vault/throttling-dialog.png)
3. <span data-ttu-id="8e0fe-266">Nadat u hebt ingeschakeld beperking, geef Hallo bandbreedte toegestaan voor back-up van de gegevensoverdracht tijdens **werkuren** en **niet-werkuren**.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-266">After you have enabled throttling, specify hello allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="8e0fe-267">Hallo bandbreedte waarden begint in 512 kilobits per seconde (Kbps) en omhoog too1, 023 megabytes per seconde (MBps) kunnen gaan.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-267">hello bandwidth values begin at 512 kilobits per second (Kbps) and can go up too1,023 megabytes per second (MBps).</span></span> <span data-ttu-id="8e0fe-268">U kunt ook Hallo start aanwijzen en voltooien voor **werkuren**, en welke dagen van week Hallo worden beschouwd als werkdagen.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-268">You can also designate hello start and finish for **Work hours**, and which days of hello week are considered work days.</span></span> <span data-ttu-id="8e0fe-269">Uren buiten aangewezen werk uren worden beschouwd als niet-werk uren.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-269">Hours outside of designated work hours are considered non-work hours.</span></span>
4. <span data-ttu-id="8e0fe-270">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-270">Click **OK**.</span></span>

### <a name="tooback-up-files-and-folders-for-hello-first-time"></a><span data-ttu-id="8e0fe-271">tooback van bestanden en mappen voor de eerste keer Hallo</span><span class="sxs-lookup"><span data-stu-id="8e0fe-271">tooback up files and folders for hello first time</span></span>
1. <span data-ttu-id="8e0fe-272">In de back-upagent hello, klikt u op **Back-Up uit** toocomplete Hallo eerste seeding via Hallo-netwerk.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-272">In hello backup agent, click **Back Up Now** toocomplete hello initial seeding over hello network.</span></span>

    ![Nu back-up maken van Windows Server](./media/backup-configure-vault/backup-now.png)
2. <span data-ttu-id="8e0fe-274">Op de bevestigingspagina Hallo revisie Hallo-instellingen die de Wizard Back-Up nu Hallo tooback Hallo machine gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-274">On hello Confirmation page, review hello settings that hello Back Up Now Wizard will use tooback up hello machine.</span></span> <span data-ttu-id="8e0fe-275">Klik vervolgens op **Back-up maken**.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-275">Then click **Back Up**.</span></span>
3. <span data-ttu-id="8e0fe-276">Klik op **sluiten** tooclose Hallo-wizard.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-276">Click **Close** tooclose hello wizard.</span></span> <span data-ttu-id="8e0fe-277">Als u dit doet voordat Hallo back-upproces is voltooid, blijft Hallo wizard toorun op Hallo achtergrond.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-277">If you do this before hello backup process finishes, hello wizard continues toorun in hello background.</span></span>

<span data-ttu-id="8e0fe-278">Nadat de eerste back-up Hallo is voltooid, Hallo **taak voltooid** status wordt weergegeven in Hallo back-up-console.</span><span class="sxs-lookup"><span data-stu-id="8e0fe-278">After hello initial backup is completed, hello **Job completed** status appears in hello Backup console.</span></span>

![IR voltooid](./media/backup-configure-vault/ircomplete.png)

## <a name="questions"></a><span data-ttu-id="8e0fe-280">Vragen?</span><span class="sxs-lookup"><span data-stu-id="8e0fe-280">Questions?</span></span>
<span data-ttu-id="8e0fe-281">Als u vragen hebt of als er een functie die u toosee opgenomen wilt, [Stuur ons feedback](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="8e0fe-281">If you have questions, or if there is any feature that you would like toosee included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e0fe-282">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8e0fe-282">Next steps</span></span>
<span data-ttu-id="8e0fe-283">Zie voor meer informatie over back-ups van virtuele machines of andere werkbelastingen:</span><span class="sxs-lookup"><span data-stu-id="8e0fe-283">For additional information about backing up VMs or other workloads, see:</span></span>

* <span data-ttu-id="8e0fe-284">Wanneer u eenmaal een back-up hebt gemaakt van uw bestanden en mappen, kunt u [uw kluizen en servers beheren](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="8e0fe-284">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="8e0fe-285">Als u een back-up toorestore moet, gebruikt u in dit artikel te[bestanden tooa Windows-machine herstellen](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="8e0fe-285">If you need toorestore a backup, use this article too[restore files tooa Windows machine](backup-azure-restore-windows-server.md).</span></span>
