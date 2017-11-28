---
title: Azure Analysis Services-database maken en terugzetten | Microsoft Docs
description: Beschrijft hoe u back-up en herstel van een Azure Analysis Services-database.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: bffa481a498b130ef1f2388a5ba856da5d164ee0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="backup-and-restore"></a><span data-ttu-id="e9a26-103">Back-ups en herstellen</span><span class="sxs-lookup"><span data-stu-id="e9a26-103">Backup and restore</span></span>

<span data-ttu-id="e9a26-104">Back-ups van databases in Azure Analysis Services model in tabelvorm is grotendeels hetzelfde als voor on-premises Analysis-Services.</span><span class="sxs-lookup"><span data-stu-id="e9a26-104">Backing up tabular model databases in Azure Analysis Services is much the same as for on-premises Analysis Services.</span></span> <span data-ttu-id="e9a26-105">Het belangrijkste verschil is waar u uw back-upbestanden opslaat.</span><span class="sxs-lookup"><span data-stu-id="e9a26-105">The primary difference is where you store your backup files.</span></span> <span data-ttu-id="e9a26-106">Back-upbestanden moeten worden opgeslagen in een container in een [Azure storage-account](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="e9a26-106">Backup files must be saved to a container in an [Azure storage account](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="e9a26-107">Kunt u een opslagaccount en container die u al hebt, of ze kunnen worden gemaakt bij het configureren van instellingen voor de opslag voor uw server.</span><span class="sxs-lookup"><span data-stu-id="e9a26-107">You can use a storage account and container you already have, or they can be created when configuring storage settings for your server.</span></span>

> [!NOTE]
> <span data-ttu-id="e9a26-108">Maken van een opslagaccount kan resulteren in een nieuwe factureerbare service.</span><span class="sxs-lookup"><span data-stu-id="e9a26-108">Creating a storage account can result in a new billable service.</span></span> <span data-ttu-id="e9a26-109">Zie voor meer informatie, [prijzen voor Azure Storage](https://azure.microsoft.com/pricing/details/storage/blobs/).</span><span class="sxs-lookup"><span data-stu-id="e9a26-109">To learn more, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/blobs/).</span></span>
> 
> 

<span data-ttu-id="e9a26-110">Back-ups worden opgeslagen met de extensie abf.</span><span class="sxs-lookup"><span data-stu-id="e9a26-110">Backups are saved with an abf extension.</span></span> <span data-ttu-id="e9a26-111">Voor in het geheugen modellen in tabelvorm, worden zowel modelgegevens en metagegevens opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="e9a26-111">For in-memory tabular models, both model data and metadata are stored.</span></span> <span data-ttu-id="e9a26-112">Voor de DirectQuery-modellen in tabelvorm, is alleen de metagegevens van het model opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="e9a26-112">For DirectQuery tabular models, only model metadata is stored.</span></span> <span data-ttu-id="e9a26-113">Back-ups worden gecomprimeerd en versleuteld, afhankelijk van de opties die u kiest.</span><span class="sxs-lookup"><span data-stu-id="e9a26-113">Backups can be compressed and encrypted, depending on the options you choose.</span></span> 



## <a name="configure-storage-settings"></a><span data-ttu-id="e9a26-114">Instellingen voor de opslag configureren</span><span class="sxs-lookup"><span data-stu-id="e9a26-114">Configure storage settings</span></span>
<span data-ttu-id="e9a26-115">Voordat u een back-up, moet u instellingen voor de opslag voor uw server configureren.</span><span class="sxs-lookup"><span data-stu-id="e9a26-115">Before backing up, you need to configure storage settings for your server.</span></span>


### <a name="to-configure-storage-settings"></a><span data-ttu-id="e9a26-116">Instellingen voor de opslag configureren</span><span class="sxs-lookup"><span data-stu-id="e9a26-116">To configure storage settings</span></span>
1.  <span data-ttu-id="e9a26-117">In Azure portal > **instellingen**, klikt u op **back-up**.</span><span class="sxs-lookup"><span data-stu-id="e9a26-117">In Azure portal > **Settings**, click **Backup**.</span></span>

    ![Back-ups in instellingen](./media/analysis-services-backup/aas-backup-backups.png)

2.  <span data-ttu-id="e9a26-119">Klik op **ingeschakeld**, klikt u vervolgens op **Opslaginstellingen**.</span><span class="sxs-lookup"><span data-stu-id="e9a26-119">Click **Enabled**, then click **Storage Settings**.</span></span>

    ![Inschakelen](./media/analysis-services-backup/aas-backup-enable.png)

3. <span data-ttu-id="e9a26-121">Selecteer uw storage-account of maak een nieuwe.</span><span class="sxs-lookup"><span data-stu-id="e9a26-121">Select your storage account or create a new one.</span></span>

4. <span data-ttu-id="e9a26-122">Selecteer een container of maak een nieuwe.</span><span class="sxs-lookup"><span data-stu-id="e9a26-122">Select a container or create a new one.</span></span>

    ![Container selecteren](./media/analysis-services-backup/aas-backup-container.png)

5. <span data-ttu-id="e9a26-124">De back-instellingen opslaan.</span><span class="sxs-lookup"><span data-stu-id="e9a26-124">Save your backup settings.</span></span>

    ![Back-instellingen opslaan](./media/analysis-services-backup/aas-backup-save.png)

## <a name="backup"></a><span data-ttu-id="e9a26-126">Back-up</span><span class="sxs-lookup"><span data-stu-id="e9a26-126">Backup</span></span>

### <a name="to-backup-by-using-ssms"></a><span data-ttu-id="e9a26-127">Back-up met behulp van SSMS</span><span class="sxs-lookup"><span data-stu-id="e9a26-127">To backup by using SSMS</span></span>

1. <span data-ttu-id="e9a26-128">SSMS, met de rechtermuisknop op een database > **Back-Up**.</span><span class="sxs-lookup"><span data-stu-id="e9a26-128">In SSMS, right-click a database > **Back Up**.</span></span>

2. <span data-ttu-id="e9a26-129">In **Backup Database** > **back-upbestand**, klikt u op **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="e9a26-129">In **Backup Database** > **Backup file**, click **Browse**.</span></span>

3. <span data-ttu-id="e9a26-130">In de **bestand opslaan als** dialoogvenster, controleert u het mappad en typ een naam voor de back-upbestand.</span><span class="sxs-lookup"><span data-stu-id="e9a26-130">In the **Save file as** dialog, verify the folder path, and then type a name for the backup file.</span></span> 

4. <span data-ttu-id="e9a26-131">In de **Backup Database** dialoogvenster, opties selecteren.</span><span class="sxs-lookup"><span data-stu-id="e9a26-131">In the **Backup Database** dialog, select options.</span></span>

    <span data-ttu-id="e9a26-132">**Toestaan dat bestand overschreven** -Selecteer deze optie om de back-bestanden met dezelfde naam overschrijven.</span><span class="sxs-lookup"><span data-stu-id="e9a26-132">**Allow file overwrite** - Select this option to overwrite backup files of the same name.</span></span> <span data-ttu-id="e9a26-133">Als deze optie niet is ingeschakeld, kan niet het bestand dat u wilt opslaan dezelfde naam als een bestand dat al op dezelfde locatie bestaat hebben.</span><span class="sxs-lookup"><span data-stu-id="e9a26-133">If this option is not selected, the file you are saving cannot have the same name as a file that already exists in the same location.</span></span>

    <span data-ttu-id="e9a26-134">**Compressie toepassen** -Selecteer deze optie voor het comprimeren van het back-upbestand.</span><span class="sxs-lookup"><span data-stu-id="e9a26-134">**Apply compression** - Select this option to compress the backup file.</span></span> <span data-ttu-id="e9a26-135">Gecomprimeerde back-upbestanden besparen op schijfruimte, maar moeten een enigszins hogere CPU-gebruik.</span><span class="sxs-lookup"><span data-stu-id="e9a26-135">Compressed backup files save disk space, but require slightly higher CPU utilization.</span></span> 

    <span data-ttu-id="e9a26-136">**Versleutelen van back-upbestand** -Selecteer deze optie voor het versleutelen van het back-upbestand.</span><span class="sxs-lookup"><span data-stu-id="e9a26-136">**Encrypt backup file** - Select this option to encrypt the backup file.</span></span> <span data-ttu-id="e9a26-137">Deze optie vereist een door de gebruiker opgegeven wachtwoord voor het beveiligen van het back-upbestand.</span><span class="sxs-lookup"><span data-stu-id="e9a26-137">This option requires a user-supplied password to secure the backup file.</span></span> <span data-ttu-id="e9a26-138">Het wachtwoord kan niet worden gelezen van de back-upgegevens enigerlei andere wijze dan een herstelbewerking.</span><span class="sxs-lookup"><span data-stu-id="e9a26-138">The password prevents reading of the backup data any other means than a restore operation.</span></span> <span data-ttu-id="e9a26-139">Als u kiest voor het versleutelen van back-ups, moet u het wachtwoord opslaan op een veilige locatie.</span><span class="sxs-lookup"><span data-stu-id="e9a26-139">If you choose to encrypt backups, store the password in a safe location.</span></span>

5. <span data-ttu-id="e9a26-140">Klik op **OK** maken en de back-upbestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="e9a26-140">Click **OK** to create and save the backup file.</span></span>


### <a name="powershell"></a><span data-ttu-id="e9a26-141">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e9a26-141">PowerShell</span></span>
<span data-ttu-id="e9a26-142">Gebruik [back-up ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e9a26-142">Use [Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet) cmdlet.</span></span>

## <a name="restore"></a><span data-ttu-id="e9a26-143">Herstellen</span><span class="sxs-lookup"><span data-stu-id="e9a26-143">Restore</span></span>
<span data-ttu-id="e9a26-144">Bij het herstellen, moet het back-upbestand in de storage-account dat u hebt geconfigureerd voor uw server.</span><span class="sxs-lookup"><span data-stu-id="e9a26-144">When restoring, your backup file must be in the storage account you've configured for your server.</span></span> <span data-ttu-id="e9a26-145">Als u moet een back-upbestand van een on-premises locatie verplaatsen naar uw opslagaccount, gebruik [Microsoft Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) of de [AzCopy](../storage/common/storage-use-azcopy.md) opdrachtregelprogramma.</span><span class="sxs-lookup"><span data-stu-id="e9a26-145">If you need to move a backup file from an on-premises location to your storage account, use [Microsoft Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) or the [AzCopy](../storage/common/storage-use-azcopy.md) command-line utility.</span></span> 



> [!NOTE]
> <span data-ttu-id="e9a26-146">Als u vanuit een on-premises server terugzetten wilt, moet u alle domeingebruikers uit het model rollen te verwijderen en opnieuw toevoegen aan de rollen als Azure Active Directory-gebruikers.</span><span class="sxs-lookup"><span data-stu-id="e9a26-146">If you're restoring from an on-premises server, you must remove all the domain users from the model's roles and add them back to the roles as Azure Active Directory users.</span></span>
> 
> 

### <a name="to-restore-by-using-ssms"></a><span data-ttu-id="e9a26-147">Te herstellen met behulp van SSMS</span><span class="sxs-lookup"><span data-stu-id="e9a26-147">To restore by using SSMS</span></span>

1. <span data-ttu-id="e9a26-148">SSMS, met de rechtermuisknop op een database > **herstellen**.</span><span class="sxs-lookup"><span data-stu-id="e9a26-148">In SSMS, right-click a database > **Restore**.</span></span>

2. <span data-ttu-id="e9a26-149">In de **Backup Database** dialoogvenster in **back-upbestand**, klikt u op **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="e9a26-149">In the **Backup Database** dialog, in **Backup file**, click **Browse**.</span></span>

3. <span data-ttu-id="e9a26-150">In de **databasebestanden vinden** dialoogvenster, selecteert u het bestand dat u wilt herstellen.</span><span class="sxs-lookup"><span data-stu-id="e9a26-150">In the **Locate Database Files** dialog, select the file you want to restore.</span></span>

4. <span data-ttu-id="e9a26-151">In **Restore database**, selecteert u de database.</span><span class="sxs-lookup"><span data-stu-id="e9a26-151">In **Restore database**, select the database.</span></span>

5. <span data-ttu-id="e9a26-152">Geef opties op.</span><span class="sxs-lookup"><span data-stu-id="e9a26-152">Specify options.</span></span> <span data-ttu-id="e9a26-153">Beveiligingsopties moeten overeenkomen met de back-upopties die u hebt gebruikt om een back-up.</span><span class="sxs-lookup"><span data-stu-id="e9a26-153">Security options must match the backup options you used when backing up.</span></span>


### <a name="powershell"></a><span data-ttu-id="e9a26-154">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e9a26-154">PowerShell</span></span>

<span data-ttu-id="e9a26-155">Gebruik [terugzetten ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e9a26-155">Use [Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet) cmdlet.</span></span>


## <a name="related-information"></a><span data-ttu-id="e9a26-156">Gerelateerde informatie</span><span class="sxs-lookup"><span data-stu-id="e9a26-156">Related information</span></span>

[<span data-ttu-id="e9a26-157">Azure storage-accounts</span><span class="sxs-lookup"><span data-stu-id="e9a26-157">Azure storage accounts</span></span>](../storage/common/storage-create-storage-account.md)  
<span data-ttu-id="e9a26-158">[Hoge beschikbaarheid](analysis-services-bcdr.md)   </span><span class="sxs-lookup"><span data-stu-id="e9a26-158">[High availability](analysis-services-bcdr.md)   </span></span>  
[<span data-ttu-id="e9a26-159">Azure analyseservices beheren</span><span class="sxs-lookup"><span data-stu-id="e9a26-159">Manage Azure Analysis Services</span></span>](analysis-services-manage.md)
