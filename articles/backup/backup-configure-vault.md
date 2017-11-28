---
title: Gebruik Azure backup-agent naar de back-up van bestanden en mappen | Microsoft Docs
description: "Gebruik de Microsoft Azure Backup agent naar de back-up van Windows-bestanden en mappen in Azure. Een Recovery Services-kluis maken, de backup-agent installeren en de back-upbeleid definiëren de eerste back-up uitvoeren op de bestanden en mappen."
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
ms.openlocfilehash: b95dc0a83d8e5618effb573353f419e1837d30c5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="back-up-a-windows-server-or-client-to-azure-using-the-resource-manager-deployment-model"></a><span data-ttu-id="ca501-105">Een back-up van een Windows-server of -client maken op Azure met behulp van het Resource Manager-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="ca501-105">Back up a Windows Server or client to Azure using the Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ca501-106">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ca501-106">Azure portal</span></span>](backup-configure-vault.md)
> * [<span data-ttu-id="ca501-107">Klassieke portal</span><span class="sxs-lookup"><span data-stu-id="ca501-107">Classic portal</span></span>](backup-configure-vault-classic.md)
>
>

<span data-ttu-id="ca501-108">Dit artikel wordt uitgelegd hoe u back-up van uw Windows Server (of Windows-client) bestanden en mappen in Azure met Azure Backup met het implementatiemodel van Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ca501-108">This article explains how to back up your Windows Server (or Windows client) files and folders to Azure with Azure Backup using the Resource Manager deployment model.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/backup-deployment-models.md)]

![Back-upproces stappen](./media/backup-configure-vault/initial-backup-process.png)

## <a name="before-you-start"></a><span data-ttu-id="ca501-110">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="ca501-110">Before you start</span></span>
<span data-ttu-id="ca501-111">Als u wilt back-up van een server of client naar Azure, moet u een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="ca501-111">To back up a server or client to Azure, you need an Azure account.</span></span> <span data-ttu-id="ca501-112">Als u niet hebt, kunt u een [gratis account](https://azure.microsoft.com/free/) binnen een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="ca501-112">If you don't have one, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="ca501-113">Een Recovery Services-kluis maken</span><span class="sxs-lookup"><span data-stu-id="ca501-113">Create a Recovery Services vault</span></span>
<span data-ttu-id="ca501-114">Een Recovery Services-kluis is een entiteit waarmee alle back-ups en herstelpunten die u gedurende een bepaalde periode maakt zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="ca501-114">A Recovery Services vault is an entity that stores all the backups and recovery points you create over time.</span></span> <span data-ttu-id="ca501-115">De Recovery Services-kluis bevat ook het back-upbeleid toegepast op de beveiligde bestanden en mappen.</span><span class="sxs-lookup"><span data-stu-id="ca501-115">The Recovery Services vault also contains the backup policy applied to the protected files and folders.</span></span> <span data-ttu-id="ca501-116">Wanneer u een Recovery Services-kluis maakt, moet u ook de juiste optie voor redundantie.</span><span class="sxs-lookup"><span data-stu-id="ca501-116">When you create a Recovery Services vault, you should also select the appropriate storage redundancy option.</span></span>

### <a name="to-create-a-recovery-services-vault"></a><span data-ttu-id="ca501-117">Een Recovery Services-kluis maken</span><span class="sxs-lookup"><span data-stu-id="ca501-117">To create a Recovery Services vault</span></span>
1. <span data-ttu-id="ca501-118">Meld u met uw Azure-abonnement aan bij de [Azure Portal](https://portal.azure.com/) als u dat nog niet hebt gedaan.</span><span class="sxs-lookup"><span data-stu-id="ca501-118">If you haven't already done so, sign in to the [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="ca501-119">Klik in het menu Hub op **Meer services**, typ in de lijst met resources **Recovery Services** en klik vervolgens op **Recovery Services-kluizen**.</span><span class="sxs-lookup"><span data-stu-id="ca501-119">On the Hub menu, click **More services** and in the list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Een Recovery Services-kluis maken, stap 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="ca501-121">Als er Recovery Services-kluizen in het abonnement aanwezig zijn, worden deze weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ca501-121">If there are recovery services vaults in the subscription, the vaults are listed.</span></span>

3. <span data-ttu-id="ca501-122">Klik in het menu **Recovery Services-kluizen** op **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="ca501-122">On the **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Een Recovery Services-kluis maken, stap 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="ca501-124">De blade Recovery Services-kluis wordt geopend en u wordt gevraagd een **naam**, **abonnement**, **resourcegroep** en **locatie** in te voeren.</span><span class="sxs-lookup"><span data-stu-id="ca501-124">The Recovery Services vault blade opens, prompting you to provide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Een Recovery Services-kluis maken, stap 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="ca501-126">Voer bij **Naam** een beschrijvende naam in om de kluis aan te duiden.</span><span class="sxs-lookup"><span data-stu-id="ca501-126">For **Name**, enter a friendly name to identify the vault.</span></span> <span data-ttu-id="ca501-127">De naam moet uniek zijn voor het Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="ca501-127">The name needs to be unique for the Azure subscription.</span></span> <span data-ttu-id="ca501-128">Typ een naam die tussen 2 en 50 tekens bevat.</span><span class="sxs-lookup"><span data-stu-id="ca501-128">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="ca501-129">De naam moet beginnen met een letter en mag alleen letters, cijfers en afbreekstreepjes bevatten.</span><span class="sxs-lookup"><span data-stu-id="ca501-129">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="ca501-130">Kies het Azure-abonnement in de vervolgkeuzelijst in het gedeelte **Abonnement**.</span><span class="sxs-lookup"><span data-stu-id="ca501-130">In the **Subscription** section, use the drop-down menu to choose the Azure subscription.</span></span> <span data-ttu-id="ca501-131">Als u slechts één abonnement hebt, wordt dit weergegeven en kunt u doorgaan met de volgende stap.</span><span class="sxs-lookup"><span data-stu-id="ca501-131">If you use only one subscription, that subscription appears and you can skip to the next step.</span></span> <span data-ttu-id="ca501-132">Als u niet zeker weet welk abonnement u moet gebruiken, gebruikt u het standaard- (of voorgestelde) abonnement.</span><span class="sxs-lookup"><span data-stu-id="ca501-132">If you are not sure which subscription to use, use the default (or suggested) subscription.</span></span> <span data-ttu-id="ca501-133">Er zijn alleen meerdere mogelijkheden als uw organisatieaccount is gekoppeld aan meerdere Azure-abonnementen.</span><span class="sxs-lookup"><span data-stu-id="ca501-133">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="ca501-134">In het gedeelte **Resourcegroep**:</span><span class="sxs-lookup"><span data-stu-id="ca501-134">In the **Resource group** section:</span></span>

    * <span data-ttu-id="ca501-135">selecteert u **Nieuw** als u een nieuwe resourcegroep wilt maken,</span><span class="sxs-lookup"><span data-stu-id="ca501-135">select **Create new** if you want to create a new Resource group.</span></span>
    <span data-ttu-id="ca501-136">of</span><span class="sxs-lookup"><span data-stu-id="ca501-136">Or</span></span>
    * <span data-ttu-id="ca501-137">selecteert u **Bestaande gebruiken** en klikt u op de vervolgkeuzelijst om de lijst met beschikbare resourcegroepen te zien.</span><span class="sxs-lookup"><span data-stu-id="ca501-137">select **Use existing** and click the drop-down menu to see the available list of Resource groups.</span></span>

  <span data-ttu-id="ca501-138">Zie [Overzicht van Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) voor meer informatie over resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="ca501-138">For complete information on Resource groups, see the [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="ca501-139">Klik op **Locatie** om de geografische regio voor de kluis te selecteren.</span><span class="sxs-lookup"><span data-stu-id="ca501-139">Click **Location** to select the geographic region for the vault.</span></span> <span data-ttu-id="ca501-140">Deze keuze bepaalt de geografische regio waar uw back-upgegevens naartoe worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="ca501-140">This choice determines the geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="ca501-141">Klik onder aan de blade Recovery Services-kluis op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="ca501-141">At the bottom of the Recovery Services vault blade, click **Create**.</span></span>

  <span data-ttu-id="ca501-142">Het kan enkele minuten duren voordat de Recovery Services-kluis is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ca501-142">It can take several minutes for the Recovery Services vault to be created.</span></span> <span data-ttu-id="ca501-143">Controleer de statusmeldingen rechtsboven in de portal.</span><span class="sxs-lookup"><span data-stu-id="ca501-143">Monitor the status notifications in the upper right-hand area of the portal.</span></span> <span data-ttu-id="ca501-144">Zodra de kluis is gemaakt, wordt deze weergegeven in de lijst met Recovery Services-kluizen.</span><span class="sxs-lookup"><span data-stu-id="ca501-144">Once your vault is created, it appears in the list of Recovery Services vaults.</span></span> <span data-ttu-id="ca501-145">Als u uw kluis na enkele minuten niet ziet, klik dan op **Vernieuwen**.</span><span class="sxs-lookup"><span data-stu-id="ca501-145">If after several minutes you don't see your vault, click **Refresh**.</span></span>

  ![Op de knop Vernieuwen klikken](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

  <span data-ttu-id="ca501-147">Wanneer u uw kluis in de lijst met Recovery Services-kluizen ziet, kunt u de opslagredundantie instellen.</span><span class="sxs-lookup"><span data-stu-id="ca501-147">Once you see your vault in the list of Recovery Services vaults, you are ready to set the storage redundancy.</span></span>


### <a name="set-storage-redundancy"></a><span data-ttu-id="ca501-148">Redundantie van gegevensopslag instellen</span><span class="sxs-lookup"><span data-stu-id="ca501-148">Set storage redundancy</span></span>
<span data-ttu-id="ca501-149">Als u voor het eerst een Recovery Services-kluis maakt, bepaalt u hoe uw opslag wordt gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="ca501-149">When you first create a Recovery Services vault you determine how storage is replicated.</span></span>

1. <span data-ttu-id="ca501-150">Klik op de blade **Recovery Services-kluizen** op de nieuwe kluis.</span><span class="sxs-lookup"><span data-stu-id="ca501-150">From the **Recovery Services vaults** blade, click the new vault.</span></span>

    ![De nieuwe kluis in de lijst met Recovery Services-kluizen selecteren](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="ca501-152">Wanneer u de kluis selecteert, wordt de blade **Recovery Services-kluis** smaller en worden de blade Instellingen (*met bovenaan de kluisnaam*) en de blade met kluisdetails geopend.</span><span class="sxs-lookup"><span data-stu-id="ca501-152">When you select the vault, the **Recovery Services vault** blade narrows, and the Settings blade (*which has the name of the vault at the top*) and the vault details blade open.</span></span>

    ![De opslagconfiguratie voor nieuwe kluis bekijken](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)

2. <span data-ttu-id="ca501-154">Schuif op de blade Instellingen van de nieuwe kluis omlaag naar het gedeelte Beheren en klik op **Back-upinfrastructuur**.</span><span class="sxs-lookup"><span data-stu-id="ca501-154">In the new vault's Settings blade, use the vertical slide to scroll down to the Manage section, and click **Backup Infrastructure**.</span></span>

  <span data-ttu-id="ca501-155">De blade Back-up maken van infrastructuur wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="ca501-155">The Backup Infrastructure blade opens.</span></span>

3. <span data-ttu-id="ca501-156">Klik op de blade Back-up maken van infrastructuur op **Back-up maken van configuratie** om de blade **Back-up maken van configuratie** te openen.</span><span class="sxs-lookup"><span data-stu-id="ca501-156">In the Backup Infrastructure blade, click **Backup Configuration** to open the **Backup Configuration** blade.</span></span>

  ![De opslagconfiguratie voor nieuwe kluis instellen](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)

4. <span data-ttu-id="ca501-158">Kies het type opslagreplicatie dat geschikt is voor uw kluis.</span><span class="sxs-lookup"><span data-stu-id="ca501-158">Choose the appropriate storage replication option for your vault.</span></span>

  ![keuzes bij opslagconfiguratie](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

  <span data-ttu-id="ca501-160">Uw kluis heeft standaard geografisch redundante opslag.</span><span class="sxs-lookup"><span data-stu-id="ca501-160">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="ca501-161">Als Azure uw primaire eindpunt is voor back-upopslag, blijf dan **Geografisch redundant** gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ca501-161">If you use Azure as a primary backup storage endpoint, continue to use **Geo-redundant**.</span></span> <span data-ttu-id="ca501-162">Als Azure niet uw primaire eindpunt is voor back-upopslag, kiest u **Lokaal redundant**, zodat u de kosten voor Azure-opslag verlaagt.</span><span class="sxs-lookup"><span data-stu-id="ca501-162">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces the Azure storage costs.</span></span> <span data-ttu-id="ca501-163">U vindt meer informatie over de opties voor [geografisch redundante](../storage/common/storage-redundancy.md#geo-redundant-storage) en [lokaal redundante ](../storage/common/storage-redundancy.md#locally-redundant-storage) opslag in dit [overzicht van opslagredundantie](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="ca501-163">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="ca501-164">Nu dat u kunt een kluis hebt gemaakt, bereid uw infrastructuur voor back-up van bestanden en mappen door te downloaden en installeren van de Microsoft Azure Recovery Services-agent, kluisreferenties downloaden en vervolgens via deze referenties te registreren van de agent met de kluis.</span><span class="sxs-lookup"><span data-stu-id="ca501-164">Now that you've created a vault, prepare your infrastructure to back up files and folders by downloading and installing the Microsoft Azure Recovery Services agent, downloading vault credentials, and then using those credentials to register the agent with the vault.</span></span>

## <a name="configure-the-vault"></a><span data-ttu-id="ca501-165">De kluis configureren</span><span class="sxs-lookup"><span data-stu-id="ca501-165">Configure the vault</span></span>

1. <span data-ttu-id="ca501-166">Klik in het gedeelte Aan de slag van de blade van de Recovery Services-kluis (voor de kluis die u zojuist hebt gemaakt) op **Back-up** en dan op de blade **Aan de slag met black-ups**. Selecteer vervolgens **Doel van de back-up**.</span><span class="sxs-lookup"><span data-stu-id="ca501-166">On the Recovery Services vault blade (for the vault you just created), in the Getting Started section, click **Backup**, then on the **Getting Started with Backup** blade, select **Backup goal**.</span></span>

  ![Open de blade back-updoelstelling](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

  <span data-ttu-id="ca501-168">De blade **Back-updoelstelling** wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="ca501-168">The **Backup Goal** blade opens.</span></span> <span data-ttu-id="ca501-169">Als de Recovery Services-kluis eerder is geconfigureerd, wordt de **back-updoel** blades geopend wanneer u klikt op **back-up** op de Recovery Services-blade kluis.</span><span class="sxs-lookup"><span data-stu-id="ca501-169">If the Recovery Services vault has been previously configured, then the **Backup Goal** blades opens when you click **Backup** on the Recovery Services vault blade.</span></span>

  ![Open de blade back-updoelstelling](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="ca501-171">Selecteer **On-premises** in het menu **Waar wordt uw workload uitgevoerd?**.</span><span class="sxs-lookup"><span data-stu-id="ca501-171">From the **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

  <span data-ttu-id="ca501-172">U kiest **On-premises** omdat uw Windows Server of Windows-computer een fysieke machine is die zich niet in Azure bevindt.</span><span class="sxs-lookup"><span data-stu-id="ca501-172">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="ca501-173">Selecteer **Bestanden en mappen** in het menu **Waarvan wilt u een back-up maken?** en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="ca501-173">From the **What do you want to backup?** menu, select **Files and folders**, and click **OK**.</span></span>

  ![Bestanden en mappen configureren](./media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

  <span data-ttu-id="ca501-175">Nadat u op OK hebt geklikt, wordt er een vinkje weergegeven naast **Back-updoelstelling** en wordt de blade **Infrastructuur voorbereiden** geopend.</span><span class="sxs-lookup"><span data-stu-id="ca501-175">After clicking OK, a checkmark appears next to **Backup goal**, and the **Prepare infrastructure** blade opens.</span></span>

  ![Nu de back-updoelstelling is geconfigureerd, gaat u de infrastructuur voorbereiden](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="ca501-177">Klik op de blade **Infrastructuur voorbereiden** op **Agent voor Windows Server of Windows Client downloaden**.</span><span class="sxs-lookup"><span data-stu-id="ca501-177">On the **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

  ![infrastructuur voorbereiden](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

  <span data-ttu-id="ca501-179">Als u Windows Server Essential gebruikt, kiest u voor het downloaden van de agent voor Windows Server Essential.</span><span class="sxs-lookup"><span data-stu-id="ca501-179">If you are using Windows Server Essential, then choose to download the agent for Windows Server Essential.</span></span> <span data-ttu-id="ca501-180">In een pop-upmenu wordt gevraagd of u MARSAgentInstaller.exe wilt uitvoeren of opslaan.</span><span class="sxs-lookup"><span data-stu-id="ca501-180">A pop-up menu prompts you to run or save MARSAgentInstaller.exe.</span></span>

  ![Dialoogvenster MARSAgentInstaller](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="ca501-182">Klik in het downloadpop-upvenster op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="ca501-182">In the download pop-up menu, click **Save**.</span></span>

  <span data-ttu-id="ca501-183">Standaard wordt het bestand **MARSagentinstaller.exe** opgeslagen in de map Downloads.</span><span class="sxs-lookup"><span data-stu-id="ca501-183">By default, the **MARSagentinstaller.exe** file is saved to your Downloads folder.</span></span> <span data-ttu-id="ca501-184">Wanneer het installatieprogramma is voltooid, ziet u een pop-upvenster waarin wordt gevraagd of u het installatieprogramma wilt uitvoeren of de map wilt openen.</span><span class="sxs-lookup"><span data-stu-id="ca501-184">When the installer completes, you will see a pop-up asking if you want to run the installer, or open the folder.</span></span>

  ![infrastructuur voorbereiden](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

  <span data-ttu-id="ca501-186">U hoeft de agent nog niet te installeren.</span><span class="sxs-lookup"><span data-stu-id="ca501-186">You don't need to install the agent yet.</span></span> <span data-ttu-id="ca501-187">U kunt de agent installeren nadat u de kluisreferenties hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="ca501-187">You can install the agent after you have downloaded the vault credentials.</span></span>

6. <span data-ttu-id="ca501-188">Klik op de blade **Infrastructuur voorbereiden** op **Downloaden**.</span><span class="sxs-lookup"><span data-stu-id="ca501-188">On the **Prepare infrastructure** blade, click **Download**.</span></span>

  ![kluisreferenties downloaden](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

  <span data-ttu-id="ca501-190">De kluisreferenties worden naar de map Downloads gedownload.</span><span class="sxs-lookup"><span data-stu-id="ca501-190">The vault credentials download to your Downloads folder.</span></span> <span data-ttu-id="ca501-191">Nadat de kluisreferenties zijn gedownload, ziet u een pop-upvenster waarin u wordt gevraagd of u de referenties wilt openen of opslaan.</span><span class="sxs-lookup"><span data-stu-id="ca501-191">After the vault credentials finish downloading, you see a pop-up asking if you want to open or save the credentials.</span></span> <span data-ttu-id="ca501-192">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="ca501-192">Click **Save**.</span></span> <span data-ttu-id="ca501-193">Als u per ongeluk klikt op **Openen**, kunt u het dialoogvenster waarmee wordt geprobeerd de kluisreferenties te openen, laten mislukken.</span><span class="sxs-lookup"><span data-stu-id="ca501-193">If you accidentally click **Open**, let the dialog that attempts to open the vault credentials, fail.</span></span> <span data-ttu-id="ca501-194">U kunt de kluisreferenties niet openen.</span><span class="sxs-lookup"><span data-stu-id="ca501-194">You cannot open the vault credentials.</span></span> <span data-ttu-id="ca501-195">Ga door naar de volgende stap.</span><span class="sxs-lookup"><span data-stu-id="ca501-195">Proceed to the next step.</span></span> <span data-ttu-id="ca501-196">De kluisreferenties bevinden zich in de map Downloads.</span><span class="sxs-lookup"><span data-stu-id="ca501-196">The vault credentials are in the Downloads folder.</span></span>   

  ![kluisreferenties downloaden is voltooid](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-the-agent"></a><span data-ttu-id="ca501-198">De agent installeren en registreren</span><span class="sxs-lookup"><span data-stu-id="ca501-198">Install and register the agent</span></span>

> [!NOTE]
> <span data-ttu-id="ca501-199">Het maken van back-ups via Azure Portal is nog niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="ca501-199">Enabling backup through the Azure portal is not available, yet.</span></span> <span data-ttu-id="ca501-200">U kunt met de Microsoft Azure Recovery Services-agent back-ups maken van uw bestanden en mappen.</span><span class="sxs-lookup"><span data-stu-id="ca501-200">Use the Microsoft Azure Recovery Services Agent to back up your files and folders.</span></span>
>

1. <span data-ttu-id="ca501-201">Zoek en dubbelklik op **MARSagentinstaller.exe** in de map Downloads (of een andere locatie waar het bestand is opgeslagen).</span><span class="sxs-lookup"><span data-stu-id="ca501-201">Locate and double-click the **MARSagentinstaller.exe** from the Downloads folder (or other saved location).</span></span>

  <span data-ttu-id="ca501-202">Het installatieprogramma geeft een reeks berichten tijdens het uitpakken, installeren en registreren van de Recovery Services-agent.</span><span class="sxs-lookup"><span data-stu-id="ca501-202">The installer provides a series of messages as it extracts, installs, and registers the Recovery Services agent.</span></span>

  ![uitvoeren van installatiereferenties van de Recovery Services-agent](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="ca501-204">Doorloop de installatiewizard van de Microsoft Azure Recovery Services Agent.</span><span class="sxs-lookup"><span data-stu-id="ca501-204">Complete the Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="ca501-205">Om de wizard volledig door te kunnen lopen, moet u:</span><span class="sxs-lookup"><span data-stu-id="ca501-205">To complete the wizard, you need to:</span></span>

  * <span data-ttu-id="ca501-206">Een locatie voor de installatie en de cachemap kiezen.</span><span class="sxs-lookup"><span data-stu-id="ca501-206">Choose a location for the installation and cache folder.</span></span>
  * <span data-ttu-id="ca501-207">De informatie van uw proxyserver invoeren als u een proxyserver gebruikt om verbinding te maken met internet.</span><span class="sxs-lookup"><span data-stu-id="ca501-207">Provide your proxy server info if you use a proxy server to connect to the internet.</span></span>
  * <span data-ttu-id="ca501-208">Uw gebruikersnaam en wachtwoord invoeren als u gebruikmaakt van een geverifieerde proxyserver.</span><span class="sxs-lookup"><span data-stu-id="ca501-208">Provide your user name and password details if you use an authenticated proxy.</span></span>
  * <span data-ttu-id="ca501-209">De gedownloade kluisreferenties invoeren</span><span class="sxs-lookup"><span data-stu-id="ca501-209">Provide the downloaded vault credentials</span></span>
  * <span data-ttu-id="ca501-210">De wachtwoordzin voor de versleuteling op een veilige locatie opslaan.</span><span class="sxs-lookup"><span data-stu-id="ca501-210">Save the encryption passphrase in a secure location.</span></span>

  > [!NOTE]
  > <span data-ttu-id="ca501-211">Als u de wachtwoordzin kwijtraakt of vergeet, kan Microsoft u niet helpen om de back-upgegevens te herstellen.</span><span class="sxs-lookup"><span data-stu-id="ca501-211">If you lose or forget the passphrase, Microsoft cannot help recover the backup data.</span></span> <span data-ttu-id="ca501-212">Sla het bestand daarom op een veilige locatie op.</span><span class="sxs-lookup"><span data-stu-id="ca501-212">Save the file in a secure location.</span></span> <span data-ttu-id="ca501-213">Het is verplicht om een back-up te herstellen.</span><span class="sxs-lookup"><span data-stu-id="ca501-213">It is required to restore a backup.</span></span>
  >
  >

<span data-ttu-id="ca501-214">De agent wordt nu geïnstalleerd en uw computer wordt geregistreerd bij de kluis.</span><span class="sxs-lookup"><span data-stu-id="ca501-214">The agent is now installed and your machine is registered to the vault.</span></span> <span data-ttu-id="ca501-215">U kunt nu uw back-up configureren en plannen.</span><span class="sxs-lookup"><span data-stu-id="ca501-215">You're ready to configure and schedule your backup.</span></span>

## <a name="network-and-connectivity-requirements"></a><span data-ttu-id="ca501-216">Netwerk- en verbindingsvereisten</span><span class="sxs-lookup"><span data-stu-id="ca501-216">Network and Connectivity Requirements</span></span>

<span data-ttu-id="ca501-217">Als uw machine/de proxy toegang tot internet beperkt heeft, moet u zorgen dat de firewall op de machine/proxy-instellingen zijn geconfigureerd om toe te staan van de volgende URL's:</span><span class="sxs-lookup"><span data-stu-id="ca501-217">If your machine/proxy has limited internet access, ensure that firewall settings on the machine/proxy are configured to allow the following URLs:</span></span> <br>
    1. <span data-ttu-id="ca501-218">www.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="ca501-218">www.msftncsi.com</span></span>
    2. <span data-ttu-id="ca501-219">*.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="ca501-219">*.Microsoft.com</span></span>
    3. <span data-ttu-id="ca501-220">*.WindowsAzure.com</span><span class="sxs-lookup"><span data-stu-id="ca501-220">*.WindowsAzure.com</span></span>
    4. <span data-ttu-id="ca501-221">*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="ca501-221">*.microsoftonline.com</span></span>
    5. <span data-ttu-id="ca501-222">*.windows.ne</span><span class="sxs-lookup"><span data-stu-id="ca501-222">*.windows.ne</span></span>


## <a name="create-the-backup-policy"></a><span data-ttu-id="ca501-223">Het back-upbeleid maken</span><span class="sxs-lookup"><span data-stu-id="ca501-223">Create the backup policy</span></span>
<span data-ttu-id="ca501-224">Het back-upbeleid is het plannen wanneer de herstelpunten worden gemaakt en hoe lang die de herstelpunten worden bewaard.</span><span class="sxs-lookup"><span data-stu-id="ca501-224">The backup policy is the schedule when recovery points are taken, and the length of time the recovery points are retained.</span></span> <span data-ttu-id="ca501-225">Gebruik de Microsoft Azure Backup-agent te maken van de back-upbeleid voor bestanden en mappen.</span><span class="sxs-lookup"><span data-stu-id="ca501-225">Use the Microsoft Azure Backup agent to create the backup policy for files and folders.</span></span>

### <a name="to-create-a-backup-schedule"></a><span data-ttu-id="ca501-226">Een back-upschema maken</span><span class="sxs-lookup"><span data-stu-id="ca501-226">To create a backup schedule</span></span>
1. <span data-ttu-id="ca501-227">Open de Microsoft Azure Backup agent.</span><span class="sxs-lookup"><span data-stu-id="ca501-227">Open the Microsoft Azure Backup agent.</span></span> <span data-ttu-id="ca501-228">U vindt deze door te zoeken naar **Microsoft Azure Backup** op uw machine.</span><span class="sxs-lookup"><span data-stu-id="ca501-228">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![De Azure Backup agent starten](./media/backup-configure-vault/snap-in-search.png)
2. <span data-ttu-id="ca501-230">In de Backup-agent **acties** deelvenster, klikt u op **back-up plannen** om de Wizard planning-back-up te starten.</span><span class="sxs-lookup"><span data-stu-id="ca501-230">In the Backup agent's **Actions** pane, click **Schedule Backup** to launch the Schedule Backup Wizard.</span></span>

    ![Een back-up van de Windows Server plannen](./media/backup-configure-vault/schedule-first-backup.png)

3. <span data-ttu-id="ca501-232">Op de **aan de slag** pagina van de Wizard Back-up plannen klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="ca501-232">On the **Getting started** page of the Schedule Backup Wizard, click **Next**.</span></span>
4. <span data-ttu-id="ca501-233">Op de **Items selecteren voor back-up** pagina, klikt u op **Items toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="ca501-233">On the **Select Items to Backup** page, click **Add Items**.</span></span>

  <span data-ttu-id="ca501-234">Hiermee opent u het dialoogvenster Items selecteren.</span><span class="sxs-lookup"><span data-stu-id="ca501-234">The Select Items dialog opens.</span></span>

5. <span data-ttu-id="ca501-235">Selecteer de bestanden en mappen die u wilt beveiligen en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="ca501-235">Select the files and folders that you want to protect, and then click **OK**.</span></span>
6. <span data-ttu-id="ca501-236">In de **Items selecteren voor back-up** pagina, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="ca501-236">In the **Select Items to Backup** page, click **Next**.</span></span>
7. <span data-ttu-id="ca501-237">Op de **back-upschema specificeren** pagina geeft u het back-upschema en op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="ca501-237">On the **Specify Backup Schedule** page, specify the backup schedule and click **Next**.</span></span>

    <span data-ttu-id="ca501-238">U kunt dagelijkse back-ups (maximaal drie keer per dag en wekelijkse back-ups plannen.</span><span class="sxs-lookup"><span data-stu-id="ca501-238">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span></span>

    ![Items voor back-up van Windows Server](./media/backup-configure-vault/specify-backup-schedule-close.png)

   > [!NOTE]
   > <span data-ttu-id="ca501-240">Zie het artikel [Uw tape-infrastructuur vervangen met Azure Backup](backup-azure-backup-cloud-as-tape.md) voor meer informatie over hoe u een back-upschema moet invoeren.</span><span class="sxs-lookup"><span data-stu-id="ca501-240">For more information about how to specify the backup schedule, see the article [Use Azure Backup to replace your tape infrastructure](backup-azure-backup-cloud-as-tape.md).</span></span>
   >
   >

8. <span data-ttu-id="ca501-241">Op de **retentiebeleid selecteren** pagina, kiest u de specifieke bewaarbeleidsregels de voor de back-up en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="ca501-241">On the **Select Retention Policy** page, choose the specific retention policies the for the backup copy and click **Next**.</span></span>

    <span data-ttu-id="ca501-242">Het bewaarbeleid geeft de duur dat de back-up is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="ca501-242">The retention policy specifies the duration which the backup is stored.</span></span> <span data-ttu-id="ca501-243">In plaats van alleen 'plat beleid' voor alle back-uppunten op te geven kunt u een ander retentiebeleid opgeven op basis van wanneer de back-up plaatsvindt.</span><span class="sxs-lookup"><span data-stu-id="ca501-243">Rather than just specifying a “flat policy” for all backup points, you can specify different retention policies based on when the backup occurs.</span></span> <span data-ttu-id="ca501-244">U kunt het dagelijkse, wekelijkse, maandelijkse en jaarlijkse retentiebeleid aanpassen, zodat het beleid altijd is afgestemd op uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="ca501-244">You can modify the daily, weekly, monthly, and yearly retention policies to meet your needs.</span></span>
9. <span data-ttu-id="ca501-245">Op de pagina Type voor eerste back-up kiezen kiest u het type voor de eerste back-up.</span><span class="sxs-lookup"><span data-stu-id="ca501-245">On the Choose Initial Backup Type page, choose the initial backup type.</span></span> <span data-ttu-id="ca501-246">Laat de optie **Automatisch via het netwerk** aangevinkt staan en klik vervolgens op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="ca501-246">Leave the option **Automatically over the network** selected, and then click **Next**.</span></span>

    <span data-ttu-id="ca501-247">U kunt automatisch via het netwerk of offline back-ups maken.</span><span class="sxs-lookup"><span data-stu-id="ca501-247">You can back up automatically over the network, or you can back up offline.</span></span> <span data-ttu-id="ca501-248">In het laatste deel van dit artikel wordt het proces voor automatische back-ups beschreven.</span><span class="sxs-lookup"><span data-stu-id="ca501-248">The remainder of this article describes the process for backing up automatically.</span></span> <span data-ttu-id="ca501-249">Als u liever offline back-ups maakt, lees dan het artikel [Werkstroom voor offline back-up in Azure Backup](backup-azure-backup-import-export.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ca501-249">If you prefer to do an offline backup, review the article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span></span>
10. <span data-ttu-id="ca501-250">Lees de informatie op de pagina Bevestiging en klik vervolgens op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="ca501-250">On the Confirmation page, review the information, and then click **Finish**.</span></span>
11. <span data-ttu-id="ca501-251">Nadat u de wizard voor het maken van een back-upschema hebt doorlopen, klikt u op **Sluiten**.</span><span class="sxs-lookup"><span data-stu-id="ca501-251">After the wizard finishes creating the backup schedule, click **Close**.</span></span>

### <a name="enable-network-throttling"></a><span data-ttu-id="ca501-252">Netwerkbeperking inschakelen</span><span class="sxs-lookup"><span data-stu-id="ca501-252">Enable network throttling</span></span>
<span data-ttu-id="ca501-253">De Microsoft Azure Backup agent biedt netwerkbeperking.</span><span class="sxs-lookup"><span data-stu-id="ca501-253">The Microsoft Azure Backup agent provides network throttling.</span></span> <span data-ttu-id="ca501-254">Gebeurtenisbeperking bepaalt hoe de netwerkbandbreedte tijdens de gegevensoverdracht wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ca501-254">Throttling controls how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="ca501-255">Dit besturingselement is handig als u back wilt-up van gegevens tijdens werkuren, maar niet wilt dat de back-upproces andere internetverkeer verstoort zijn.</span><span class="sxs-lookup"><span data-stu-id="ca501-255">This control can be helpful if you need to back up data during work hours but do not want the backup process to interfere with other Internet traffic.</span></span> <span data-ttu-id="ca501-256">Beperking van toepassing op back-up en herstelbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="ca501-256">Throttling applies to back up and restore activities.</span></span>

> [!NOTE]
> <span data-ttu-id="ca501-257">Netwerkbeperking is niet beschikbaar op Windows Server 2008 R2 SP1, Windows Server 2008 SP2 of Windows 7 (met servicepacks).</span><span class="sxs-lookup"><span data-stu-id="ca501-257">Network throttling is not available on Windows Server 2008 R2 SP1, Windows Server 2008 SP2, or Windows 7 (with service packs).</span></span> <span data-ttu-id="ca501-258">De Azure Backup-functie voor netwerkbeperking stelt Quality of Service (QoS) op het lokale besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="ca501-258">The Azure Backup network throttling feature engages Quality of Service (QoS) on the local operating system.</span></span> <span data-ttu-id="ca501-259">Hoewel Azure back-up kan deze besturingssystemen beveiligen kunt, wordt de versie van QoS beschikbaar op deze platforms werkt met Azure Backup netwerkbeperking.</span><span class="sxs-lookup"><span data-stu-id="ca501-259">Though Azure Backup can protect these operating systems, the version of QoS available on these platforms doesn't work with Azure Backup network throttling.</span></span> <span data-ttu-id="ca501-260">Netwerkbeperking kan worden gebruikt voor alle andere [ondersteunde besturingssystemen](backup-azure-backup-faq.md).</span><span class="sxs-lookup"><span data-stu-id="ca501-260">Network throttling can be used on all other [supported operating systems](backup-azure-backup-faq.md).</span></span>
>
>

<span data-ttu-id="ca501-261">**Netwerkbeperking inschakelen**</span><span class="sxs-lookup"><span data-stu-id="ca501-261">**To enable network throttling**</span></span>

1. <span data-ttu-id="ca501-262">Klik in de Microsoft Azure Backup-agent op **eigenschappen wijzigen**.</span><span class="sxs-lookup"><span data-stu-id="ca501-262">In the Microsoft Azure Backup agent, click **Change Properties**.</span></span>

    ![Eigenschappen wijzigen](./media/backup-configure-vault/change-properties.png)
2. <span data-ttu-id="ca501-264">Op de **bandbreedtebeperking** tabblad de **inschakelen voor gebruik van internetbandbreedte voor back-upbewerkingen** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="ca501-264">On the **Throttling** tab, select the **Enable internet bandwidth usage throttling for backup operations** check box.</span></span>

    ![Netwerkbeperking](./media/backup-configure-vault/throttling-dialog.png)
3. <span data-ttu-id="ca501-266">Nadat u hebt ingeschakeld beperking, geef de toegestane bandbreedte voor back-up van de gegevensoverdracht tijdens **werkuren** en **niet-werkuren**.</span><span class="sxs-lookup"><span data-stu-id="ca501-266">After you have enabled throttling, specify the allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="ca501-267">De waarden van de bandbreedte begint in 512 kilobits per seconde (Kbps) en maximaal 1023 megabytes per seconde (MBps) kunnen gaan.</span><span class="sxs-lookup"><span data-stu-id="ca501-267">The bandwidth values begin at 512 kilobits per second (Kbps) and can go up to 1,023 megabytes per second (MBps).</span></span> <span data-ttu-id="ca501-268">U kunt ook aanwijzen is gestart en voltooien voor **werkuren**, en welke dagen van de week worden beschouwd als werkdagen.</span><span class="sxs-lookup"><span data-stu-id="ca501-268">You can also designate the start and finish for **Work hours**, and which days of the week are considered work days.</span></span> <span data-ttu-id="ca501-269">Uren buiten aangewezen werk uren worden beschouwd als niet-werk uren.</span><span class="sxs-lookup"><span data-stu-id="ca501-269">Hours outside of designated work hours are considered non-work hours.</span></span>
4. <span data-ttu-id="ca501-270">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="ca501-270">Click **OK**.</span></span>

### <a name="to-back-up-files-and-folders-for-the-first-time"></a><span data-ttu-id="ca501-271">Voor de eerste keer een back-up maken van bestanden en mappen</span><span class="sxs-lookup"><span data-stu-id="ca501-271">To back up files and folders for the first time</span></span>
1. <span data-ttu-id="ca501-272">Klik in de back-upagent op **Back-Up uit** voltooien van de eerste seeding via het netwerk.</span><span class="sxs-lookup"><span data-stu-id="ca501-272">In the backup agent, click **Back Up Now** to complete the initial seeding over the network.</span></span>

    ![Nu back-up maken van Windows Server](./media/backup-configure-vault/backup-now.png)
2. <span data-ttu-id="ca501-274">Controleer op de pagina Bevestiging de instellingen die de wizard Nu back-up maken gebruikt om een back-up te maken van de machine.</span><span class="sxs-lookup"><span data-stu-id="ca501-274">On the Confirmation page, review the settings that the Back Up Now Wizard will use to back up the machine.</span></span> <span data-ttu-id="ca501-275">Klik vervolgens op **Back-up maken**.</span><span class="sxs-lookup"><span data-stu-id="ca501-275">Then click **Back Up**.</span></span>
3. <span data-ttu-id="ca501-276">Klik op **Sluiten** om de wizard te sluiten.</span><span class="sxs-lookup"><span data-stu-id="ca501-276">Click **Close** to close the wizard.</span></span> <span data-ttu-id="ca501-277">Als u dit doet voordat het back-upproces is voltooid, blijft de wizard op de achtergrond aanwezig.</span><span class="sxs-lookup"><span data-stu-id="ca501-277">If you do this before the backup process finishes, the wizard continues to run in the background.</span></span>

<span data-ttu-id="ca501-278">Nadat de eerste back-up is voltooid, wordt de status **Taak voltooid** weergegeven in de back-upconsole.</span><span class="sxs-lookup"><span data-stu-id="ca501-278">After the initial backup is completed, the **Job completed** status appears in the Backup console.</span></span>

![IR voltooid](./media/backup-configure-vault/ircomplete.png)

## <a name="questions"></a><span data-ttu-id="ca501-280">Vragen?</span><span class="sxs-lookup"><span data-stu-id="ca501-280">Questions?</span></span>
<span data-ttu-id="ca501-281">Als u vragen hebt of als er een functie is die u graag opgenomen ziet worden, [stuur ons dan uw feedback](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="ca501-281">If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca501-282">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ca501-282">Next steps</span></span>
<span data-ttu-id="ca501-283">Zie voor meer informatie over back-ups van virtuele machines of andere werkbelastingen:</span><span class="sxs-lookup"><span data-stu-id="ca501-283">For additional information about backing up VMs or other workloads, see:</span></span>

* <span data-ttu-id="ca501-284">Wanneer u eenmaal een back-up hebt gemaakt van uw bestanden en mappen, kunt u [uw kluizen en servers beheren](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="ca501-284">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="ca501-285">Als u een back-up moet herstellen, [zet de bestanden dan terug naar een Windows-machine](backup-azure-restore-windows-server.md) aan de hand van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="ca501-285">If you need to restore a backup, use this article to [restore files to a Windows machine](backup-azure-restore-windows-server.md).</span></span>
