---
title: Maak een back-up van systeemstatus van Windows naar Azure | Microsoft Docs
description: Informatie over het maken van de systeemstatus van Windows Server en/of Windows computers naar Azure.
services: backup
documentationcenter: 
author: saurabhsensharma
manager: carmonm
editor: 
keywords: back-up maken; hoe u een back-up maakt; back-up van bestanden en mappen maken
ms.assetid: 5b15ebf1-2214-4722-b937-96e2be8872bb
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: saurse;markgal
ms.openlocfilehash: 6fbd96935f444d8b0c6d068ebd0d28e612f19816
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="back-up-windows-system-state-in-resource-manager-deployment"></a><span data-ttu-id="19e51-104">Back-up van systeemstatus Windows in de implementatie van Resource Manager</span><span class="sxs-lookup"><span data-stu-id="19e51-104">Back up Windows system state in Resource Manager deployment</span></span>
<span data-ttu-id="19e51-105">Dit artikel wordt uitgelegd hoe u back-up van de systeemstatus van uw Windows Server naar Azure.</span><span class="sxs-lookup"><span data-stu-id="19e51-105">This article explains how to back up your Windows Server system state to Azure.</span></span> <span data-ttu-id="19e51-106">Het artikel is bedoeld als handleiding waarmee u stapsgewijs de basis onder de knie krijgt.</span><span class="sxs-lookup"><span data-stu-id="19e51-106">It's a tutorial intended to walk you through the basics.</span></span>

<span data-ttu-id="19e51-107">Als u meer wilt weten over Azure Backup, lees dan dit [overzicht](backup-introduction-to-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="19e51-107">If you want to know more about Azure Backup, read this [overview](backup-introduction-to-azure-backup.md).</span></span>

<span data-ttu-id="19e51-108">Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/) aan waarmee u toegang hebt tot alle services van Azure.</span><span class="sxs-lookup"><span data-stu-id="19e51-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) that lets you access any Azure service.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="19e51-109">Een Recovery Services-kluis maken</span><span class="sxs-lookup"><span data-stu-id="19e51-109">Create a recovery services vault</span></span>
<span data-ttu-id="19e51-110">Als u een back-up wilt maken van uw bestanden en mappen, moet u een Recovery Services-kluis maken in de regio waar u de gegevens wilt opslaan.</span><span class="sxs-lookup"><span data-stu-id="19e51-110">To back up your files and folders, you need to create a Recovery Services vault in the region where you want to store the data.</span></span> <span data-ttu-id="19e51-111">U moet ook bepalen op welke manier u uw opslag wilt repliceren. </span><span class="sxs-lookup"><span data-stu-id="19e51-111">You also need to determine how you want your storage replicated.</span></span>

### <a name="to-create-a-recovery-services-vault"></a><span data-ttu-id="19e51-112">Een Recovery Services-kluis maken</span><span class="sxs-lookup"><span data-stu-id="19e51-112">To create a Recovery Services vault</span></span>
1. <span data-ttu-id="19e51-113">Meld u met uw Azure-abonnement aan bij de [Azure Portal](https://portal.azure.com/) als u dat nog niet hebt gedaan.</span><span class="sxs-lookup"><span data-stu-id="19e51-113">If you haven't already done so, sign in to the [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="19e51-114">Klik in het menu Hub op **Meer services**, typ in de lijst met resources **Recovery Services** en klik vervolgens op **Recovery Services-kluizen**.</span><span class="sxs-lookup"><span data-stu-id="19e51-114">On the Hub menu, click **More services** and in the list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Een Recovery Services-kluis maken, stap 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="19e51-116">Als er Recovery Services-kluizen in het abonnement aanwezig zijn, worden deze weergegeven.</span><span class="sxs-lookup"><span data-stu-id="19e51-116">If there are recovery services vaults in the subscription, the vaults are listed.</span></span>
3. <span data-ttu-id="19e51-117">Klik in het menu **Recovery Services-kluizen** op **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="19e51-117">On the **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Een Recovery Services-kluis maken, stap 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="19e51-119">De blade Recovery Services-kluis wordt geopend en u wordt gevraagd een **naam**, **abonnement**, **resourcegroep** en **locatie** in te voeren.</span><span class="sxs-lookup"><span data-stu-id="19e51-119">The Recovery Services vault blade opens, prompting you to provide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Een Recovery Services-kluis maken, stap 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="19e51-121">Voer bij **Naam** een beschrijvende naam in om de kluis aan te duiden.</span><span class="sxs-lookup"><span data-stu-id="19e51-121">For **Name**, enter a friendly name to identify the vault.</span></span> <span data-ttu-id="19e51-122">De naam moet uniek zijn voor het Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="19e51-122">The name needs to be unique for the Azure subscription.</span></span> <span data-ttu-id="19e51-123">Typ een naam die tussen 2 en 50 tekens bevat.</span><span class="sxs-lookup"><span data-stu-id="19e51-123">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="19e51-124">De naam moet beginnen met een letter en mag alleen letters, cijfers en afbreekstreepjes bevatten.</span><span class="sxs-lookup"><span data-stu-id="19e51-124">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="19e51-125">Kies het Azure-abonnement in de vervolgkeuzelijst in het gedeelte **Abonnement**.</span><span class="sxs-lookup"><span data-stu-id="19e51-125">In the **Subscription** section, use the drop-down menu to choose the Azure subscription.</span></span> <span data-ttu-id="19e51-126">Als u slechts één abonnement hebt, wordt dit weergegeven en kunt u doorgaan met de volgende stap.</span><span class="sxs-lookup"><span data-stu-id="19e51-126">If you use only one subscription, that subscription appears and you can skip to the next step.</span></span> <span data-ttu-id="19e51-127">Als u niet zeker weet welk abonnement u moet gebruiken, gebruikt u het standaard- (of voorgestelde) abonnement.</span><span class="sxs-lookup"><span data-stu-id="19e51-127">If you are not sure which subscription to use, use the default (or suggested) subscription.</span></span> <span data-ttu-id="19e51-128">Er zijn alleen meerdere mogelijkheden als uw organisatieaccount is gekoppeld aan meerdere Azure-abonnementen.</span><span class="sxs-lookup"><span data-stu-id="19e51-128">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="19e51-129">In het gedeelte **Resourcegroep**:</span><span class="sxs-lookup"><span data-stu-id="19e51-129">In the **Resource group** section:</span></span>

    * <span data-ttu-id="19e51-130">selecteert u **Nieuw** als u een resourcegroep wilt maken,</span><span class="sxs-lookup"><span data-stu-id="19e51-130">select **Create new** if you want to create a Resource group.</span></span>
    <span data-ttu-id="19e51-131">of</span><span class="sxs-lookup"><span data-stu-id="19e51-131">Or</span></span>
    * <span data-ttu-id="19e51-132">selecteert u **Bestaande gebruiken** en klikt u op de vervolgkeuzelijst om de lijst met beschikbare resourcegroepen te zien.</span><span class="sxs-lookup"><span data-stu-id="19e51-132">select **Use existing** and click the drop-down menu to see the available list of Resource groups.</span></span>

  <span data-ttu-id="19e51-133">Zie [Overzicht van Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) voor meer informatie over resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="19e51-133">For complete information on Resource groups, see the [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="19e51-134">Klik op **Locatie** om de geografische regio voor de kluis te selecteren.</span><span class="sxs-lookup"><span data-stu-id="19e51-134">Click **Location** to select the geographic region for the vault.</span></span> <span data-ttu-id="19e51-135">Deze keuze bepaalt de geografische regio waar uw back-upgegevens naartoe worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="19e51-135">This choice determines the geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="19e51-136">Klik onder aan de blade Recovery Services-kluis op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="19e51-136">At the bottom of the Recovery Services vault blade, click **Create**.</span></span>

    <span data-ttu-id="19e51-137">Het kan enkele minuten duren voordat de Recovery Services-kluis is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="19e51-137">It can take several minutes for the Recovery Services vault to be created.</span></span> <span data-ttu-id="19e51-138">Controleer de statusmeldingen rechtsboven in de portal.</span><span class="sxs-lookup"><span data-stu-id="19e51-138">Monitor the status notifications in the upper right-hand area of the portal.</span></span> <span data-ttu-id="19e51-139">Zodra de kluis is gemaakt, wordt deze weergegeven in de lijst met Recovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="19e51-139">Once your vault is created, it appears in the list of Recovery Services vaults.</span></span> <span data-ttu-id="19e51-140">Als u uw kluis na enkele minuten niet ziet, klik dan op **Vernieuwen**.</span><span class="sxs-lookup"><span data-stu-id="19e51-140">If after several minutes you don't see your vault, click **Refresh**.</span></span>

    ![Op de knop Vernieuwen klikken](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    <span data-ttu-id="19e51-142">Wanneer u uw kluis in de lijst met Recovery Services-kluizen ziet, kunt u de opslagredundantie instellen.</span><span class="sxs-lookup"><span data-stu-id="19e51-142">Once you see your vault in the list of Recovery Services vaults, you are ready to set the storage redundancy.</span></span>

### <a name="set-storage-redundancy-for-the-vault"></a><span data-ttu-id="19e51-143">Opslagredundantie instellen voor de kluis</span><span class="sxs-lookup"><span data-stu-id="19e51-143">Set storage redundancy for the vault</span></span>
<span data-ttu-id="19e51-144">Wanneer u een Recovery Services-kluis maakt, zorg er dan voor dat de opslagredundantie op de gewenste manier is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="19e51-144">When you create a Recovery Services vault, make sure storage redundancy is configured the way you want.</span></span>

1. <span data-ttu-id="19e51-145">Klik op de blade **Recovery Services-kluizen** op de nieuwe kluis.</span><span class="sxs-lookup"><span data-stu-id="19e51-145">From the **Recovery Services vaults** blade, click the new vault.</span></span>

    ![De nieuwe kluis in de lijst met Recovery Services-kluizen selecteren](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="19e51-147">Wanneer u de kluis selecteert, wordt de blade **Recovery Services-kluis** smaller en worden de blade Instellingen (*met bovenaan de kluisnaam*) en de blade met kluisdetails geopend.</span><span class="sxs-lookup"><span data-stu-id="19e51-147">When you select the vault, the **Recovery Services vault** blade narrows, and the Settings blade (*which has the name of the vault at the top*) and the vault details blade open.</span></span>

    ![De opslagconfiguratie voor nieuwe kluis bekijken](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)
2. <span data-ttu-id="19e51-149">Schuif op de blade Instellingen van de nieuwe kluis omlaag naar het gedeelte Beheren en klik op **Back-upinfrastructuur**.</span><span class="sxs-lookup"><span data-stu-id="19e51-149">In the new vault's Settings blade, use the vertical slide to scroll down to the Manage section, and click **Backup Infrastructure**.</span></span>
    <span data-ttu-id="19e51-150">De blade Back-up maken van infrastructuur wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="19e51-150">The Backup Infrastructure blade opens.</span></span>
3. <span data-ttu-id="19e51-151">Klik op de blade Back-up maken van infrastructuur op **Back-up maken van configuratie** om de blade **Back-up maken van configuratie** te openen.</span><span class="sxs-lookup"><span data-stu-id="19e51-151">In the Backup Infrastructure blade, click **Backup Configuration** to open the **Backup Configuration** blade.</span></span>

    ![De opslagconfiguratie voor nieuwe kluis instellen](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. <span data-ttu-id="19e51-153">Kies het type opslagreplicatie dat geschikt is voor uw kluis.</span><span class="sxs-lookup"><span data-stu-id="19e51-153">Choose the appropriate storage replication option for your vault.</span></span>

    ![keuzes bij opslagconfiguratie](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    <span data-ttu-id="19e51-155">Uw kluis heeft standaard geografisch redundante opslag.</span><span class="sxs-lookup"><span data-stu-id="19e51-155">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="19e51-156">Als Azure uw primaire eindpunt is voor back-upopslag, blijf dan **Geografisch redundant** gebruiken.</span><span class="sxs-lookup"><span data-stu-id="19e51-156">If you use Azure as a primary backup storage endpoint, continue to use **Geo-redundant**.</span></span> <span data-ttu-id="19e51-157">Als Azure niet uw primaire eindpunt is voor back-upopslag, kiest u **Lokaal redundant**, zodat u de kosten voor Azure-opslag verlaagt.</span><span class="sxs-lookup"><span data-stu-id="19e51-157">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces the Azure storage costs.</span></span> <span data-ttu-id="19e51-158">U vindt meer informatie over de opties voor [geografisch redundante](../storage/common/storage-redundancy.md#geo-redundant-storage) en [lokaal redundante ](../storage/common/storage-redundancy.md#locally-redundant-storage) opslag in dit [overzicht van opslagredundantie](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="19e51-158">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="19e51-159">Nu dat u kunt een kluis hebt gemaakt, kunt u deze voor de back-up van systeemstatus Windows configureren.</span><span class="sxs-lookup"><span data-stu-id="19e51-159">Now that you've created a vault, configure it for backing up Windows System State.</span></span>

## <a name="configure-the-vault"></a><span data-ttu-id="19e51-160">De kluis configureren</span><span class="sxs-lookup"><span data-stu-id="19e51-160">Configure the vault</span></span>
1. <span data-ttu-id="19e51-161">Klik in het gedeelte Aan de slag van de blade van de Recovery Services-kluis (voor de kluis die u zojuist hebt gemaakt) op **Back-up** en dan op de blade **Aan de slag met black-ups**. Selecteer vervolgens **Doel van de back-up**.</span><span class="sxs-lookup"><span data-stu-id="19e51-161">On the Recovery Services vault blade (for the vault you just created), in the Getting Started section, click **Backup**, then on the **Getting Started with Backup** blade, select **Backup goal**.</span></span>

    ![Open de blade back-updoelstelling](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    <span data-ttu-id="19e51-163">De blade **Back-updoelstelling** wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="19e51-163">The **Backup Goal** blade opens.</span></span>

    ![Open de blade back-updoelstelling](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="19e51-165">Selecteer **On-premises** in het menu **Waar wordt uw workload uitgevoerd?**.</span><span class="sxs-lookup"><span data-stu-id="19e51-165">From the **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

    <span data-ttu-id="19e51-166">U kiest **On-premises** omdat uw Windows Server of Windows-computer een fysieke machine is die zich niet in Azure bevindt.</span><span class="sxs-lookup"><span data-stu-id="19e51-166">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="19e51-167">Van de **wat wilt u back-up maken?** selecteert u **systeemstatus**, en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="19e51-167">From the **What do you want to backup?** menu, select **System State**, and click **OK**.</span></span>

    ![Bestanden en mappen configureren](./media/backup-azure-system-state/backup-goal-system-state.png)

    <span data-ttu-id="19e51-169">Nadat u op OK hebt geklikt, wordt er een vinkje weergegeven naast **Back-updoelstelling** en wordt de blade **Infrastructuur voorbereiden** geopend.</span><span class="sxs-lookup"><span data-stu-id="19e51-169">After clicking OK, a checkmark appears next to **Backup goal**, and the **Prepare infrastructure** blade opens.</span></span>

    ![Nu de back-updoelstelling is geconfigureerd, gaat u de infrastructuur voorbereiden](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="19e51-171">Klik op de blade **Infrastructuur voorbereiden** op **Agent voor Windows Server of Windows Client downloaden**.</span><span class="sxs-lookup"><span data-stu-id="19e51-171">On the **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

    ![infrastructuur voorbereiden](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

    <span data-ttu-id="19e51-173">Als u Windows Server Essential gebruikt, kiest u voor het downloaden van de agent voor Windows Server Essential.</span><span class="sxs-lookup"><span data-stu-id="19e51-173">If you are using Windows Server Essential, then choose to download the agent for Windows Server Essential.</span></span> <span data-ttu-id="19e51-174">In een pop-upmenu wordt gevraagd of u MARSAgentInstaller.exe wilt uitvoeren of opslaan.</span><span class="sxs-lookup"><span data-stu-id="19e51-174">A pop-up menu prompts you to run or save MARSAgentInstaller.exe.</span></span>

    ![Dialoogvenster MARSAgentInstaller](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="19e51-176">Klik in het downloadpop-upvenster op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="19e51-176">In the download pop-up menu, click **Save**.</span></span>

    <span data-ttu-id="19e51-177">Standaard wordt het bestand **MARSagentinstaller.exe** opgeslagen in de map Downloads.</span><span class="sxs-lookup"><span data-stu-id="19e51-177">By default, the **MARSagentinstaller.exe** file is saved to your Downloads folder.</span></span> <span data-ttu-id="19e51-178">Wanneer het installatieprogramma is voltooid, ziet u een pop-upvenster waarin wordt gevraagd of u het installatieprogramma wilt uitvoeren of de map wilt openen.</span><span class="sxs-lookup"><span data-stu-id="19e51-178">When the installer completes, you will see a pop-up asking if you want to run the installer, or open the folder.</span></span>

    ![infrastructuur voorbereiden](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

    <span data-ttu-id="19e51-180">U hoeft de agent nog niet te installeren.</span><span class="sxs-lookup"><span data-stu-id="19e51-180">You don't need to install the agent yet.</span></span> <span data-ttu-id="19e51-181">U kunt de agent installeren nadat u de kluisreferenties hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="19e51-181">You can install the agent after you have downloaded the vault credentials.</span></span>

6. <span data-ttu-id="19e51-182">Klik op de blade **Infrastructuur voorbereiden** op **Downloaden**.</span><span class="sxs-lookup"><span data-stu-id="19e51-182">On the **Prepare infrastructure** blade, click **Download**.</span></span>

    ![kluisreferenties downloaden](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

    <span data-ttu-id="19e51-184">De kluisreferenties worden naar de map Downloads gedownload.</span><span class="sxs-lookup"><span data-stu-id="19e51-184">The vault credentials download to your Downloads folder.</span></span> <span data-ttu-id="19e51-185">Nadat de kluisreferenties zijn gedownload, ziet u een pop-upvenster waarin u wordt gevraagd of u de referenties wilt openen of opslaan.</span><span class="sxs-lookup"><span data-stu-id="19e51-185">After the vault credentials finish downloading, you see a pop-up asking if you want to open or save the credentials.</span></span> <span data-ttu-id="19e51-186">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="19e51-186">Click **Save**.</span></span> <span data-ttu-id="19e51-187">Als u per ongeluk klikt op **Openen**, kunt u het dialoogvenster waarmee wordt geprobeerd de kluisreferenties te openen, laten mislukken.</span><span class="sxs-lookup"><span data-stu-id="19e51-187">If you accidentally click **Open**, let the dialog that attempts to open the vault credentials, fail.</span></span> <span data-ttu-id="19e51-188">U kunt de kluisreferenties niet openen.</span><span class="sxs-lookup"><span data-stu-id="19e51-188">You cannot open the vault credentials.</span></span> <span data-ttu-id="19e51-189">Ga door naar de volgende stap.</span><span class="sxs-lookup"><span data-stu-id="19e51-189">Proceed to the next step.</span></span> <span data-ttu-id="19e51-190">De kluisreferenties bevinden zich in de map Downloads.</span><span class="sxs-lookup"><span data-stu-id="19e51-190">The vault credentials are in the Downloads folder.</span></span>   

    ![kluisreferenties downloaden is voltooid](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-the-agent"></a><span data-ttu-id="19e51-192">De agent installeren en registreren</span><span class="sxs-lookup"><span data-stu-id="19e51-192">Install and register the agent</span></span>

> [!NOTE]
> <span data-ttu-id="19e51-193">Het maken van back-ups via Azure Portal is nog niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="19e51-193">Enabling backup through the Azure portal is not available, yet.</span></span> <span data-ttu-id="19e51-194">Gebruik de Microsoft Azure Recovery Services Agent back-up van systeemstatus van Windows Server.</span><span class="sxs-lookup"><span data-stu-id="19e51-194">Use the Microsoft Azure Recovery Services Agent to back up Windows Server System State.</span></span>
>

1. <span data-ttu-id="19e51-195">Zoek en dubbelklik op **MARSagentinstaller.exe** in de map Downloads (of een andere locatie waar het bestand is opgeslagen).</span><span class="sxs-lookup"><span data-stu-id="19e51-195">Locate and double-click the **MARSagentinstaller.exe** from the Downloads folder (or other saved location).</span></span>

    <span data-ttu-id="19e51-196">Het installatieprogramma geeft een reeks berichten tijdens het uitpakken, installeren en registreren van de Recovery Services-agent.</span><span class="sxs-lookup"><span data-stu-id="19e51-196">The installer provides a series of messages as it extracts, installs, and registers the Recovery Services agent.</span></span>

    ![uitvoeren van installatiereferenties van de Recovery Services-agent](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="19e51-198">Doorloop de installatiewizard van de Microsoft Azure Recovery Services Agent.</span><span class="sxs-lookup"><span data-stu-id="19e51-198">Complete the Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="19e51-199">Om de wizard volledig door te kunnen lopen, moet u:</span><span class="sxs-lookup"><span data-stu-id="19e51-199">To complete the wizard, you need to:</span></span>

   * <span data-ttu-id="19e51-200">Een locatie voor de installatie en de cachemap kiezen.</span><span class="sxs-lookup"><span data-stu-id="19e51-200">Choose a location for the installation and cache folder.</span></span>
   * <span data-ttu-id="19e51-201">De informatie van uw proxyserver invoeren als u een proxyserver gebruikt om verbinding te maken met internet.</span><span class="sxs-lookup"><span data-stu-id="19e51-201">Provide your proxy server info if you use a proxy server to connect to the internet.</span></span>
   * <span data-ttu-id="19e51-202">Uw gebruikersnaam en wachtwoord invoeren als u gebruikmaakt van een geverifieerde proxyserver.</span><span class="sxs-lookup"><span data-stu-id="19e51-202">Provide your user name and password details if you use an authenticated proxy.</span></span>
   * <span data-ttu-id="19e51-203">De gedownloade kluisreferenties invoeren</span><span class="sxs-lookup"><span data-stu-id="19e51-203">Provide the downloaded vault credentials</span></span>
   * <span data-ttu-id="19e51-204">De wachtwoordzin voor de versleuteling op een veilige locatie opslaan.</span><span class="sxs-lookup"><span data-stu-id="19e51-204">Save the encryption passphrase in a secure location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="19e51-205">Als u de wachtwoordzin kwijtraakt of vergeet, kan Microsoft u niet helpen om de back-upgegevens te herstellen.</span><span class="sxs-lookup"><span data-stu-id="19e51-205">If you lose or forget the passphrase, Microsoft cannot help recover the backup data.</span></span> <span data-ttu-id="19e51-206">Sla het bestand daarom op een veilige locatie op.</span><span class="sxs-lookup"><span data-stu-id="19e51-206">Save the file in a secure location.</span></span> <span data-ttu-id="19e51-207">Het is verplicht om een back-up te herstellen.</span><span class="sxs-lookup"><span data-stu-id="19e51-207">It is required to restore a backup.</span></span>
     >
     >

<span data-ttu-id="19e51-208">De agent wordt nu geïnstalleerd en uw computer wordt geregistreerd bij de kluis.</span><span class="sxs-lookup"><span data-stu-id="19e51-208">The agent is now installed and your machine is registered to the vault.</span></span> <span data-ttu-id="19e51-209">U kunt nu uw back-up configureren en plannen.</span><span class="sxs-lookup"><span data-stu-id="19e51-209">You're ready to configure and schedule your backup.</span></span>

## <a name="back-up-windows-server-system-state-preview"></a><span data-ttu-id="19e51-210">Back-up van Windows Server System State (Preview)</span><span class="sxs-lookup"><span data-stu-id="19e51-210">Back up Windows Server System State (Preview)</span></span>
<span data-ttu-id="19e51-211">De eerste back-up bevat drie taken:</span><span class="sxs-lookup"><span data-stu-id="19e51-211">The initial backup includes three tasks:</span></span>

* <span data-ttu-id="19e51-212">Systeemstatusback-up met behulp van de Azure Backup agent inschakelen</span><span class="sxs-lookup"><span data-stu-id="19e51-212">Enable System State Backup using the Azure Backup agent</span></span>
* <span data-ttu-id="19e51-213">De back-up plannen</span><span class="sxs-lookup"><span data-stu-id="19e51-213">Schedule the backup</span></span>
* <span data-ttu-id="19e51-214">Voor de eerste keer een back-up maken van bestanden en mappen</span><span class="sxs-lookup"><span data-stu-id="19e51-214">Back up files and folders for the first time</span></span>

<span data-ttu-id="19e51-215">Gebruik de Microsoft Azure Recovery Services-agent om de eerste back-up uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="19e51-215">To complete the initial backup, use the Microsoft Azure Recovery Services agent.</span></span>

### <a name="to-enable-system-state-backup-using-the-azure-backup-agent"></a><span data-ttu-id="19e51-216">Systeemstatusback-up met behulp van de Azure Backup agent inschakelen</span><span class="sxs-lookup"><span data-stu-id="19e51-216">To enable System State backup using the Azure Backup agent</span></span>

1. <span data-ttu-id="19e51-217">Voer de volgende opdracht voor stoppen van de Azure Backup-engine in een PowerShell-sessie.</span><span class="sxs-lookup"><span data-stu-id="19e51-217">In a PowerShell session, run the following command to stop the Azure Backup engine.</span></span>

  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="19e51-218">Open het Windows-register.</span><span class="sxs-lookup"><span data-stu-id="19e51-218">Open the Windows Registry.</span></span>

  ```
  PS C:\> regedit.exe
  ```

3. <span data-ttu-id="19e51-219">Voeg de volgende registersleutel toe met de opgegeven DWord-waarde.</span><span class="sxs-lookup"><span data-stu-id="19e51-219">Add the following registry key with the specified DWord Value.</span></span>

  | <span data-ttu-id="19e51-220">Registerpad</span><span class="sxs-lookup"><span data-stu-id="19e51-220">Registry path</span></span> | <span data-ttu-id="19e51-221">Registersleutel</span><span class="sxs-lookup"><span data-stu-id="19e51-221">Registry key</span></span> | <span data-ttu-id="19e51-222">DWord-waarde</span><span class="sxs-lookup"><span data-stu-id="19e51-222">DWord value</span></span> |
  |---------------|--------------|-------------|
  | <span data-ttu-id="19e51-223">HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span><span class="sxs-lookup"><span data-stu-id="19e51-223">HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span></span> | <span data-ttu-id="19e51-224">TurnOffSSBFeature</span><span class="sxs-lookup"><span data-stu-id="19e51-224">TurnOffSSBFeature</span></span> | <span data-ttu-id="19e51-225">2</span><span class="sxs-lookup"><span data-stu-id="19e51-225">2</span></span> |

4. <span data-ttu-id="19e51-226">Start de Backup-engine opnieuw door het uitvoeren van de volgende opdracht bij een opdrachtprompt met verhoogde bevoegdheid.</span><span class="sxs-lookup"><span data-stu-id="19e51-226">Restart the Backup engine by executing the following command in an elevated command prompt.</span></span>

  ```
  PS C:\> Net start obengine
  ```

### <a name="to-schedule-the-backup-job"></a><span data-ttu-id="19e51-227">De back-up plannen</span><span class="sxs-lookup"><span data-stu-id="19e51-227">To schedule the backup job</span></span>

1. <span data-ttu-id="19e51-228">Open de Microsoft Azure Recovery Services-agent.</span><span class="sxs-lookup"><span data-stu-id="19e51-228">Open the Microsoft Azure Recovery Services agent.</span></span> <span data-ttu-id="19e51-229">U vindt deze door te zoeken naar **Microsoft Azure Backup** op uw machine.</span><span class="sxs-lookup"><span data-stu-id="19e51-229">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![De Azure Recovery Services-agent starten](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)

2. <span data-ttu-id="19e51-231">Klik in de Recovery Services-agent op **Back-up plannen**.</span><span class="sxs-lookup"><span data-stu-id="19e51-231">In the Recovery Services agent, click **Schedule Backup**.</span></span>

    ![Een back-up van de Windows Server plannen](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)

3. <span data-ttu-id="19e51-233">Op de pagina Aan de slag van de wizard Back-up plannen klikt u op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="19e51-233">On the Getting started page of the Schedule Backup Wizard, click **Next**.</span></span>

4. <span data-ttu-id="19e51-234">Op de pagina Items selecteren voor back-up klikt u op **Items toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="19e51-234">On the Select Items to Backup page, click **Add Items**.</span></span>

5. <span data-ttu-id="19e51-235">Selecteer **systeemstatus** en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="19e51-235">Select **System State** and then click **OK**.</span></span>

6. <span data-ttu-id="19e51-236">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="19e51-236">Click **Next**.</span></span>

7. <span data-ttu-id="19e51-237">De planning voor systeemstatusback-up en retentie automatisch ingesteld op de back-up van elke zondag om 21:00 uur lokale tijd en de bewaarperiode is ingesteld op 60 dagen.</span><span class="sxs-lookup"><span data-stu-id="19e51-237">The System State Backup and Retention schedule is automatically set to back up every Sunday at 9:00 PM local time, and the retention period is set to 60 days.</span></span>

   > [!NOTE]
   > <span data-ttu-id="19e51-238">Beleid voor het back-up en retentie van systeemstatus wordt automatisch geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="19e51-238">System State backup and retention policy is automatically configured.</span></span> <span data-ttu-id="19e51-239">Als u back-up van bestanden en mappen naast de status van het Windows Server, geeft u alleen het back-up en retentie-beleid voor back-ups van de wizard.</span><span class="sxs-lookup"><span data-stu-id="19e51-239">If you back up Files and Folders in addition to the Windows Server System State, specify only the Backup and Retention policy for file backups from the wizard.</span></span> 
   >

8. <span data-ttu-id="19e51-240">Lees de informatie op de pagina Bevestiging en klik vervolgens op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="19e51-240">On the Confirmation page, review the information, and then click **Finish**.</span></span>

9. <span data-ttu-id="19e51-241">Nadat u de wizard voor het maken van een back-upschema hebt doorlopen, klikt u op **Sluiten**.</span><span class="sxs-lookup"><span data-stu-id="19e51-241">After the wizard finishes creating the backup schedule, click **Close**.</span></span>

### <a name="to-back-up-windows-server-system-state-for-the-first-time"></a><span data-ttu-id="19e51-242">Back-up systeemstatus van Windows Server voor de eerste keer</span><span class="sxs-lookup"><span data-stu-id="19e51-242">To back up Windows Server System State for the first time</span></span>

1. <span data-ttu-id="19e51-243">Zorg ervoor dat er zijn geen updates in behandeling voor Windows Server waarvoor opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="19e51-243">Make sure there are no pending updates for Windows Server that require a reboot.</span></span>

2. <span data-ttu-id="19e51-244">Klik in de Recovery Services-agent op **Nu een back-up maken** om de eerste seeding via het netwerk te voltooien.</span><span class="sxs-lookup"><span data-stu-id="19e51-244">In the Recovery Services agent, click **Back Up Now** to complete the initial seeding over the network.</span></span>

    ![Nu back-up maken van Windows Server](./media/backup-try-azure-backup-in-10-mins/backup-now.png)

3. <span data-ttu-id="19e51-246">Controleer op de pagina Bevestiging de instellingen die de wizard Nu back-up maken gebruikt om een back-up te maken van de machine.</span><span class="sxs-lookup"><span data-stu-id="19e51-246">On the Confirmation page, review the settings that the Back Up Now Wizard will use to back up the machine.</span></span> <span data-ttu-id="19e51-247">Klik vervolgens op **Back-up maken**.</span><span class="sxs-lookup"><span data-stu-id="19e51-247">Then click **Back Up**.</span></span>

4. <span data-ttu-id="19e51-248">Klik op **Sluiten** om de wizard te sluiten.</span><span class="sxs-lookup"><span data-stu-id="19e51-248">Click **Close** to close the wizard.</span></span> <span data-ttu-id="19e51-249">Als u de wizard sluit voordat het back-upproces is voltooid, blijft de wizard op de achtergrond aanwezig.</span><span class="sxs-lookup"><span data-stu-id="19e51-249">If you close the wizard before the backup process finishes, the wizard continues to run in the background.</span></span>

5. <span data-ttu-id="19e51-250">Als u back-up van bestanden en mappen op uw server, naast de systeemstatus van Windows Server, wordt de wizard Back-up nu alleen reservekopie van bestanden.</span><span class="sxs-lookup"><span data-stu-id="19e51-250">If you back up Files and Folders on your server, in addition to the Windows Server System State, the Backup Now wizard will only back up files.</span></span> <span data-ttu-id="19e51-251">Een ad-hoc systeemstatus back-up, gebruik de volgende PowerShell-opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="19e51-251">To perform an ad hoc System State back up, use the following PowerShell command:</span></span>

    ```
    PS C:\> Start-OBSystemStateBackup
    ```

  <span data-ttu-id="19e51-252">Nadat de eerste back-up is voltooid, wordt de status **Taak voltooid** weergegeven in de back-upconsole.</span><span class="sxs-lookup"><span data-stu-id="19e51-252">After the initial backup is completed, the **Job completed** status appears in the Backup console.</span></span>

  ![IR voltooid](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="frequently-asked-questions"></a><span data-ttu-id="19e51-254">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="19e51-254">Frequently asked questions</span></span>

<span data-ttu-id="19e51-255">De volgende vragen en antwoorden bevatten aanvullende informatie.</span><span class="sxs-lookup"><span data-stu-id="19e51-255">The following questions and answers provide supplementary information.</span></span>

### <a name="what-is-the-staging-volume"></a><span data-ttu-id="19e51-256">Wat is het Volume fasering?</span><span class="sxs-lookup"><span data-stu-id="19e51-256">What is the Staging Volume?</span></span>

<span data-ttu-id="19e51-257">Het Volume fasering vertegenwoordigt de locatie waar de standaard beschikbaar, Windows Server Backup de systeemstatusback-up bereidt.</span><span class="sxs-lookup"><span data-stu-id="19e51-257">The Staging Volume represents the intermediate location where the natively available, Windows Server Backup stages the System State Backup.</span></span> <span data-ttu-id="19e51-258">Azure backup-agent en vervolgens worden gecomprimeerd en versleuteld deze tussenliggende back-up en verzonden via een beveiligde HTTPS-Protocol naar de geconfigureerde Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="19e51-258">Azure Backup agent then compresses and encrypts this intermediate backup and sends it via secure HTTPS Protocol to the configured Recovery Services Vault.</span></span> <span data-ttu-id="19e51-259">**Sterk aanbevolen dat u het Volume Fasering instellen in een niet-Windows-besturingssysteemvolume. Als u problemen met de systeemstatusback-ups ziet, is het controleren van de locatie van het Volume fasering de eerste stap voor het oplossen van problemen.**</span><span class="sxs-lookup"><span data-stu-id="19e51-259">**We strongly recommended you establish the Staging Volume in a non-Windows-OS volume. If you observe problems with System State Backups, checking the location of your Staging Volume is the first troubleshooting step.**</span></span> 

### <a name="how-can-i-change-the-staging-volume-path-specified-in-the-azure-backup-agent"></a><span data-ttu-id="19e51-260">Hoe kan ik het tijdelijke pad naar opgegeven in de Azure Backup agent wijzigen?</span><span class="sxs-lookup"><span data-stu-id="19e51-260">How can I change the Staging Volume Path specified in the Azure Backup agent?</span></span>

<span data-ttu-id="19e51-261">Het Volume fasering bevindt zich in de cachemap van de standaard.</span><span class="sxs-lookup"><span data-stu-id="19e51-261">The Staging Volume is located in the cache folder by default.</span></span> 

1. <span data-ttu-id="19e51-262">U kunt deze locatie wijzigen, moet u de volgende opdracht gebruiken (in een verhoogde opdrachtprompt):</span><span class="sxs-lookup"><span data-stu-id="19e51-262">To change this location, use the following command (in an elevated command prompt):</span></span>
  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="19e51-263">Werk vervolgens de volgende registervermeldingen met het pad naar de nieuwe map voor gefaseerde installatie Volume.</span><span class="sxs-lookup"><span data-stu-id="19e51-263">Then update the following registry entries with the path to the new Staging Volume folder.</span></span>

  |<span data-ttu-id="19e51-264">Registerpad</span><span class="sxs-lookup"><span data-stu-id="19e51-264">Registry path</span></span>|<span data-ttu-id="19e51-265">Registersleutel</span><span class="sxs-lookup"><span data-stu-id="19e51-265">Registry key</span></span>|<span data-ttu-id="19e51-266">Waarde</span><span class="sxs-lookup"><span data-stu-id="19e51-266">Value</span></span>|
  |-------------|------------|-----|
  |<span data-ttu-id="19e51-267">HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span><span class="sxs-lookup"><span data-stu-id="19e51-267">HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span></span> | <span data-ttu-id="19e51-268">SSBStagingPath</span><span class="sxs-lookup"><span data-stu-id="19e51-268">SSBStagingPath</span></span> | <span data-ttu-id="19e51-269">nieuwe volume faseringslocatie</span><span class="sxs-lookup"><span data-stu-id="19e51-269">new staging volume location</span></span> |

<span data-ttu-id="19e51-270">Het pad voor gefaseerde installatie is hoofdlettergevoelig en moet het exacte hetzelfde hoofdlettergebruik als wat op de server bestaat.</span><span class="sxs-lookup"><span data-stu-id="19e51-270">The Staging Path is case sensitive and must be the exact same casing as what exists on the server.</span></span> 

3. <span data-ttu-id="19e51-271">Zodra u het pad naar het tijdelijke wijzigt, start u de Backup-engine opnieuw:</span><span class="sxs-lookup"><span data-stu-id="19e51-271">Once you change the Staging volume path, restart the Backup engine:</span></span>
  ```
  PS C:\> Net start obengine
  ```
4. <span data-ttu-id="19e51-272">Zodat het gewijzigde pad worden opgepikt, opent u de Microsoft Azure Recovery Services-agent en activeren van een ad-hoc back-up van systeemstatus.</span><span class="sxs-lookup"><span data-stu-id="19e51-272">To pick up the changed path, open the Microsoft Azure Recovery Services agent and trigger an ad hoc backup of System State.</span></span>

### <a name="why-is-the-system-state-default-retention-set-to-60-days"></a><span data-ttu-id="19e51-273">Waarom is de bewaarperiode van systeemstatus standaard ingesteld op 60 dagen?</span><span class="sxs-lookup"><span data-stu-id="19e51-273">Why is the System State default retention set to 60 days?</span></span>

<span data-ttu-id="19e51-274">De levensduur van een systeemstatusback-up is hetzelfde als de instelling 'tombstone-levensduur' voor de rol Windows Server Active Directory.</span><span class="sxs-lookup"><span data-stu-id="19e51-274">The useful life of a system state backup is the same as the "tombstone lifetime" setting for the Windows Server Active Directory role.</span></span> <span data-ttu-id="19e51-275">De standaardwaarde voor de vermelding van tombstone-levensduur is 60 dagen.</span><span class="sxs-lookup"><span data-stu-id="19e51-275">The default value for the tombstone lifetime entry is 60 days.</span></span> <span data-ttu-id="19e51-276">Deze waarde kan worden ingesteld op de Directory Service (NTDS) config-object.</span><span class="sxs-lookup"><span data-stu-id="19e51-276">This value can be set on the Directory Service (NTDS) config object.</span></span>

### <a name="how-do-i-change-the-default-backup-and-retention-policy-for-system-state"></a><span data-ttu-id="19e51-277">Hoe wijzig ik de standaard back-up- en bewaarbeleid voor systeemstatus</span><span class="sxs-lookup"><span data-stu-id="19e51-277">How do I change the default Backup and Retention Policy for System State?</span></span>

<span data-ttu-id="19e51-278">Wijzigen van de standaard back-up- en bewaarbeleid voor systeemstatus:</span><span class="sxs-lookup"><span data-stu-id="19e51-278">To change the default Backup and Retention Policy for System State:</span></span>
1. <span data-ttu-id="19e51-279">Stop de Backup-engine.</span><span class="sxs-lookup"><span data-stu-id="19e51-279">Stop the Backup engine.</span></span> <span data-ttu-id="19e51-280">Voer de volgende opdracht vanaf een opdrachtprompt met verhoogde bevoegdheid.</span><span class="sxs-lookup"><span data-stu-id="19e51-280">Run the following command from an elevated command prompt.</span></span>

  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="19e51-281">Toevoegen of bijwerken van de volgende sleutel registervermeldingen in HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider.</span><span class="sxs-lookup"><span data-stu-id="19e51-281">Add or update the following registry key entries in HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider.</span></span>

  |<span data-ttu-id="19e51-282">Naam van routeringsregister</span><span class="sxs-lookup"><span data-stu-id="19e51-282">Registry Name</span></span>|<span data-ttu-id="19e51-283">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="19e51-283">Description</span></span>|<span data-ttu-id="19e51-284">Waarde</span><span class="sxs-lookup"><span data-stu-id="19e51-284">Value</span></span>|
  |-------------|-----------|-----|
  |<span data-ttu-id="19e51-285">SSBScheduleTime</span><span class="sxs-lookup"><span data-stu-id="19e51-285">SSBScheduleTime</span></span>|<span data-ttu-id="19e51-286">Gebruikt voor het configureren van de tijd van de back-up.</span><span class="sxs-lookup"><span data-stu-id="19e51-286">Used to configure the time of the backup.</span></span> <span data-ttu-id="19e51-287">Standaardinstelling is 21: 00 lokale tijd.</span><span class="sxs-lookup"><span data-stu-id="19e51-287">Default is 9PM local time.</span></span>|<span data-ttu-id="19e51-288">DWord: Indeling UUMM (decimaal) zo 2130 voor 9:30:00 lokale tijd</span><span class="sxs-lookup"><span data-stu-id="19e51-288">DWord: Format HHMM (Decimal) for example 2130 for 9:30PM local time</span></span>|
  |<span data-ttu-id="19e51-289">SSBScheduleDays</span><span class="sxs-lookup"><span data-stu-id="19e51-289">SSBScheduleDays</span></span>|<span data-ttu-id="19e51-290">Gebruikt voor het configureren van de dagen waarop systeemstatusback-up moet worden uitgevoerd op de opgegeven tijd.</span><span class="sxs-lookup"><span data-stu-id="19e51-290">Used to configure the days when System State Backup must be performed at the specified time.</span></span> <span data-ttu-id="19e51-291">Afzonderlijke cijfers opgeven dagen van de week.</span><span class="sxs-lookup"><span data-stu-id="19e51-291">Individual digits specify days of the week.</span></span> <span data-ttu-id="19e51-292">zondag 0, 1 is maandag, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="19e51-292">0 represents Sunday, 1 is Monday, and so on.</span></span> <span data-ttu-id="19e51-293">Standaarddag voor back-up is zondag.</span><span class="sxs-lookup"><span data-stu-id="19e51-293">Default day for backup is Sunday.</span></span>|<span data-ttu-id="19e51-294">DWord: dagen van de week voor de back-up (decimaal), bijvoorbeeld 1230 plant u back-ups op maandag, dinsdag, woensdag en zondag uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="19e51-294">DWord: days of the week to run backup (decimal) for example 1230 schedules backups on Monday, Tuesday, Wednesday, and Sunday.</span></span>|
  |<span data-ttu-id="19e51-295">SSBRetentionDays</span><span class="sxs-lookup"><span data-stu-id="19e51-295">SSBRetentionDays</span></span>|<span data-ttu-id="19e51-296">Gebruikt voor het configureren van de dagen als u wilt behouden back-up.</span><span class="sxs-lookup"><span data-stu-id="19e51-296">Used to configure the days to retain backup.</span></span> <span data-ttu-id="19e51-297">Standaardwaarde is 60.</span><span class="sxs-lookup"><span data-stu-id="19e51-297">Default value is 60.</span></span> <span data-ttu-id="19e51-298">Maximaal toegestane waarde is 180.</span><span class="sxs-lookup"><span data-stu-id="19e51-298">Maximum allowed value is 180.</span></span>|<span data-ttu-id="19e51-299">DWord: Dagen voor het bewaren van back-up (decimaal).</span><span class="sxs-lookup"><span data-stu-id="19e51-299">DWord: Days to retain backup (decimal).</span></span>|

3. <span data-ttu-id="19e51-300">Gebruik de volgende opdracht om opnieuw te starten van de back-engine.</span><span class="sxs-lookup"><span data-stu-id="19e51-300">Use the following command to restart the backup engine.</span></span>
    ```
    PS C:\> Net start obengine
    ```

4. <span data-ttu-id="19e51-301">Open de Microsoft Recovery Services-agent.</span><span class="sxs-lookup"><span data-stu-id="19e51-301">Open the Microsoft Recovery Services agent.</span></span>

5. <span data-ttu-id="19e51-302">Klik op **back-up plannen** en klik vervolgens op **volgende** tot u de wijzigingen zijn doorgevoerd.</span><span class="sxs-lookup"><span data-stu-id="19e51-302">Click **Schedule Backup** and then click **Next** until you see the changes reflected.</span></span>

6. <span data-ttu-id="19e51-303">Klik op **voltooien** de wijzigingen toe te passen.</span><span class="sxs-lookup"><span data-stu-id="19e51-303">Click **Finish** to apply the changes.</span></span>


## <a name="questions"></a><span data-ttu-id="19e51-304">Vragen?</span><span class="sxs-lookup"><span data-stu-id="19e51-304">Questions?</span></span>
<span data-ttu-id="19e51-305">Als u vragen hebt of als er een functie is die u graag opgenomen ziet worden, [stuur ons dan uw feedback](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="19e51-305">If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="19e51-306">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="19e51-306">Next steps</span></span>
* <span data-ttu-id="19e51-307">Meer informatie over [back-ups maken van Windows-machines](backup-configure-vault.md).</span><span class="sxs-lookup"><span data-stu-id="19e51-307">Get more details about [backing up Windows machines](backup-configure-vault.md).</span></span>
* <span data-ttu-id="19e51-308">Wanneer u eenmaal een back-up hebt gemaakt van uw bestanden en mappen, kunt u [uw kluizen en servers beheren](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="19e51-308">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="19e51-309">Als u een back-up moet herstellen, [zet de bestanden dan terug naar een Windows-machine](backup-azure-restore-windows-server.md) aan de hand van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="19e51-309">If you need to restore a backup, use this article to [restore files to a Windows machine](backup-azure-restore-windows-server.md).</span></span>
