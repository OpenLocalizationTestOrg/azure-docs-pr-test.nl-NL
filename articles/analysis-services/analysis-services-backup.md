---
title: Analysis Services-database aaaAzure back-up en herstellen | Microsoft Docs
description: Hierin wordt beschreven hoe toobackup en terugzetten van een Azure Analysis Services-database.
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
ms.openlocfilehash: cf0a782d237a95fdfa5ef628f998bd053aac0d9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="backup-and-restore"></a><span data-ttu-id="6971b-103">Back-ups en herstellen</span><span class="sxs-lookup"><span data-stu-id="6971b-103">Backup and restore</span></span>

<span data-ttu-id="6971b-104">Back-ups van databases in Azure Analysis Services model in tabelvorm is grotendeels hetzelfde als voor on-premises Analysis-Services Hallo.</span><span class="sxs-lookup"><span data-stu-id="6971b-104">Backing up tabular model databases in Azure Analysis Services is much hello same as for on-premises Analysis Services.</span></span> <span data-ttu-id="6971b-105">het belangrijkste verschil Hallo is waar u uw back-upbestanden opslaat.</span><span class="sxs-lookup"><span data-stu-id="6971b-105">hello primary difference is where you store your backup files.</span></span> <span data-ttu-id="6971b-106">Back-upbestanden moeten worden opgeslagen op de container tooa in een [Azure storage-account](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="6971b-106">Backup files must be saved tooa container in an [Azure storage account](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="6971b-107">Kunt u een opslagaccount en container die u al hebt, of ze kunnen worden gemaakt bij het configureren van instellingen voor de opslag voor uw server.</span><span class="sxs-lookup"><span data-stu-id="6971b-107">You can use a storage account and container you already have, or they can be created when configuring storage settings for your server.</span></span>

> [!NOTE]
> <span data-ttu-id="6971b-108">Maken van een opslagaccount kan resulteren in een nieuwe factureerbare service.</span><span class="sxs-lookup"><span data-stu-id="6971b-108">Creating a storage account can result in a new billable service.</span></span> <span data-ttu-id="6971b-109">toolearn meer, Zie [prijzen voor Azure Storage](https://azure.microsoft.com/pricing/details/storage/blobs/).</span><span class="sxs-lookup"><span data-stu-id="6971b-109">toolearn more, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/blobs/).</span></span>
> 
> 

<span data-ttu-id="6971b-110">Back-ups worden opgeslagen met de extensie abf.</span><span class="sxs-lookup"><span data-stu-id="6971b-110">Backups are saved with an abf extension.</span></span> <span data-ttu-id="6971b-111">Voor in het geheugen modellen in tabelvorm, worden zowel modelgegevens en metagegevens opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="6971b-111">For in-memory tabular models, both model data and metadata are stored.</span></span> <span data-ttu-id="6971b-112">Voor de DirectQuery-modellen in tabelvorm, is alleen de metagegevens van het model opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="6971b-112">For DirectQuery tabular models, only model metadata is stored.</span></span> <span data-ttu-id="6971b-113">Back-ups worden gecomprimeerd en versleuteld, afhankelijk van het Hallo-opties die u kiest.</span><span class="sxs-lookup"><span data-stu-id="6971b-113">Backups can be compressed and encrypted, depending on hello options you choose.</span></span> 



## <a name="configure-storage-settings"></a><span data-ttu-id="6971b-114">Instellingen voor de opslag configureren</span><span class="sxs-lookup"><span data-stu-id="6971b-114">Configure storage settings</span></span>
<span data-ttu-id="6971b-115">Voordat u een back-up, moet u instellingen voor de opslag tooconfigure voor uw server.</span><span class="sxs-lookup"><span data-stu-id="6971b-115">Before backing up, you need tooconfigure storage settings for your server.</span></span>


### <a name="tooconfigure-storage-settings"></a><span data-ttu-id="6971b-116">instellingen voor de opslag tooconfigure</span><span class="sxs-lookup"><span data-stu-id="6971b-116">tooconfigure storage settings</span></span>
1.  <span data-ttu-id="6971b-117">In Azure portal > **instellingen**, klikt u op **back-up**.</span><span class="sxs-lookup"><span data-stu-id="6971b-117">In Azure portal > **Settings**, click **Backup**.</span></span>

    ![Back-ups in instellingen](./media/analysis-services-backup/aas-backup-backups.png)

2.  <span data-ttu-id="6971b-119">Klik op **ingeschakeld**, klikt u vervolgens op **Opslaginstellingen**.</span><span class="sxs-lookup"><span data-stu-id="6971b-119">Click **Enabled**, then click **Storage Settings**.</span></span>

    ![Inschakelen](./media/analysis-services-backup/aas-backup-enable.png)

3. <span data-ttu-id="6971b-121">Selecteer uw storage-account of maak een nieuwe.</span><span class="sxs-lookup"><span data-stu-id="6971b-121">Select your storage account or create a new one.</span></span>

4. <span data-ttu-id="6971b-122">Selecteer een container of maak een nieuwe.</span><span class="sxs-lookup"><span data-stu-id="6971b-122">Select a container or create a new one.</span></span>

    ![Container selecteren](./media/analysis-services-backup/aas-backup-container.png)

5. <span data-ttu-id="6971b-124">De back-instellingen opslaan.</span><span class="sxs-lookup"><span data-stu-id="6971b-124">Save your backup settings.</span></span>

    ![Back-instellingen opslaan](./media/analysis-services-backup/aas-backup-save.png)

## <a name="backup"></a><span data-ttu-id="6971b-126">Back-up</span><span class="sxs-lookup"><span data-stu-id="6971b-126">Backup</span></span>

### <a name="toobackup-by-using-ssms"></a><span data-ttu-id="6971b-127">toobackup met behulp van SSMS</span><span class="sxs-lookup"><span data-stu-id="6971b-127">toobackup by using SSMS</span></span>

1. <span data-ttu-id="6971b-128">SSMS, met de rechtermuisknop op een database > **Back-Up**.</span><span class="sxs-lookup"><span data-stu-id="6971b-128">In SSMS, right-click a database > **Back Up**.</span></span>

2. <span data-ttu-id="6971b-129">In **Backup Database** > **back-upbestand**, klikt u op **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="6971b-129">In **Backup Database** > **Backup file**, click **Browse**.</span></span>

3. <span data-ttu-id="6971b-130">In Hallo **bestand opslaan als** dialoogvenster Hallo mappad controleren en typ een naam voor de back-upbestand Hallo.</span><span class="sxs-lookup"><span data-stu-id="6971b-130">In hello **Save file as** dialog, verify hello folder path, and then type a name for hello backup file.</span></span> 

4. <span data-ttu-id="6971b-131">In Hallo **Backup Database** dialoogvenster, opties selecteren.</span><span class="sxs-lookup"><span data-stu-id="6971b-131">In hello **Backup Database** dialog, select options.</span></span>

    <span data-ttu-id="6971b-132">**Toestaan dat bestand overschreven** -Selecteer deze optie toooverwrite back-upbestanden Hallo dezelfde naam.</span><span class="sxs-lookup"><span data-stu-id="6971b-132">**Allow file overwrite** - Select this option toooverwrite backup files of hello same name.</span></span> <span data-ttu-id="6971b-133">Als deze optie niet is ingeschakeld, kan niet Hallo bestand dat u wilt opslaan Hallo dezelfde naam als een bestand dat al in Hallo dezelfde voorkomt hebben locatie.</span><span class="sxs-lookup"><span data-stu-id="6971b-133">If this option is not selected, hello file you are saving cannot have hello same name as a file that already exists in hello same location.</span></span>

    <span data-ttu-id="6971b-134">**Compressie toepassen** -Selecteer deze optie toocompress Hallo back-upbestand.</span><span class="sxs-lookup"><span data-stu-id="6971b-134">**Apply compression** - Select this option toocompress hello backup file.</span></span> <span data-ttu-id="6971b-135">Gecomprimeerde back-upbestanden besparen op schijfruimte, maar moeten een enigszins hogere CPU-gebruik.</span><span class="sxs-lookup"><span data-stu-id="6971b-135">Compressed backup files save disk space, but require slightly higher CPU utilization.</span></span> 

    <span data-ttu-id="6971b-136">**Versleutelen van back-upbestand** -Selecteer deze optie tooencrypt Hallo back-upbestand.</span><span class="sxs-lookup"><span data-stu-id="6971b-136">**Encrypt backup file** - Select this option tooencrypt hello backup file.</span></span> <span data-ttu-id="6971b-137">Deze optie vereist een back-upbestand van de gebruiker opgegeven wachtwoord toosecure Hallo.</span><span class="sxs-lookup"><span data-stu-id="6971b-137">This option requires a user-supplied password toosecure hello backup file.</span></span> <span data-ttu-id="6971b-138">Hallo wachtwoord kan niet worden gelezen van de back-upgegevens Hallo enigerlei andere wijze dan een herstelbewerking.</span><span class="sxs-lookup"><span data-stu-id="6971b-138">hello password prevents reading of hello backup data any other means than a restore operation.</span></span> <span data-ttu-id="6971b-139">Als u back-ups tooencrypt kiest, moet u Hallo wachtwoord opslaan op een veilige locatie.</span><span class="sxs-lookup"><span data-stu-id="6971b-139">If you choose tooencrypt backups, store hello password in a safe location.</span></span>

5. <span data-ttu-id="6971b-140">Klik op **OK** toocreate en Hallo back-upbestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="6971b-140">Click **OK** toocreate and save hello backup file.</span></span>


### <a name="powershell"></a><span data-ttu-id="6971b-141">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6971b-141">PowerShell</span></span>
<span data-ttu-id="6971b-142">Gebruik [back-up ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6971b-142">Use [Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet) cmdlet.</span></span>

## <a name="restore"></a><span data-ttu-id="6971b-143">Herstellen</span><span class="sxs-lookup"><span data-stu-id="6971b-143">Restore</span></span>
<span data-ttu-id="6971b-144">Bij het herstellen, moet het back-upbestand in Hallo storage-account die u hebt geconfigureerd voor uw server.</span><span class="sxs-lookup"><span data-stu-id="6971b-144">When restoring, your backup file must be in hello storage account you've configured for your server.</span></span> <span data-ttu-id="6971b-145">Als u toomove een back-upbestand van een lokale locatie tooyour storage-account nodig hebt, gebruikt u [Microsoft Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) of Hallo [AzCopy](../storage/common/storage-use-azcopy.md) opdrachtregelprogramma.</span><span class="sxs-lookup"><span data-stu-id="6971b-145">If you need toomove a backup file from an on-premises location tooyour storage account, use [Microsoft Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) or hello [AzCopy](../storage/common/storage-use-azcopy.md) command-line utility.</span></span> 



> [!NOTE]
> <span data-ttu-id="6971b-146">Als u vanuit een on-premises server terugzetten wilt, moet u alle Hallo domeingebruikers verwijderen uit de rollen van Hallo model en toe te voegen back-toohello rollen als Azure Active Directory-gebruikers.</span><span class="sxs-lookup"><span data-stu-id="6971b-146">If you're restoring from an on-premises server, you must remove all hello domain users from hello model's roles and add them back toohello roles as Azure Active Directory users.</span></span>
> 
> 

### <a name="toorestore-by-using-ssms"></a><span data-ttu-id="6971b-147">toorestore met behulp van SSMS</span><span class="sxs-lookup"><span data-stu-id="6971b-147">toorestore by using SSMS</span></span>

1. <span data-ttu-id="6971b-148">SSMS, met de rechtermuisknop op een database > **herstellen**.</span><span class="sxs-lookup"><span data-stu-id="6971b-148">In SSMS, right-click a database > **Restore**.</span></span>

2. <span data-ttu-id="6971b-149">In Hallo **Backup Database** dialoogvenster in **back-upbestand**, klikt u op **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="6971b-149">In hello **Backup Database** dialog, in **Backup file**, click **Browse**.</span></span>

3. <span data-ttu-id="6971b-150">In Hallo **databasebestanden vinden** dialoogvenster, selecteer Hallo bestand dat u wenst toorestore.</span><span class="sxs-lookup"><span data-stu-id="6971b-150">In hello **Locate Database Files** dialog, select hello file you want toorestore.</span></span>

4. <span data-ttu-id="6971b-151">In **Restore database**, selecteer Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="6971b-151">In **Restore database**, select hello database.</span></span>

5. <span data-ttu-id="6971b-152">Geef opties op.</span><span class="sxs-lookup"><span data-stu-id="6971b-152">Specify options.</span></span> <span data-ttu-id="6971b-153">Beveiligingsopties moeten overeenkomen met de back-upopties Hallo die tijdens een back-up hebt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="6971b-153">Security options must match hello backup options you used when backing up.</span></span>


### <a name="powershell"></a><span data-ttu-id="6971b-154">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6971b-154">PowerShell</span></span>

<span data-ttu-id="6971b-155">Gebruik [terugzetten ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6971b-155">Use [Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet) cmdlet.</span></span>


## <a name="related-information"></a><span data-ttu-id="6971b-156">Gerelateerde informatie</span><span class="sxs-lookup"><span data-stu-id="6971b-156">Related information</span></span>

[<span data-ttu-id="6971b-157">Azure storage-accounts</span><span class="sxs-lookup"><span data-stu-id="6971b-157">Azure storage accounts</span></span>](../storage/common/storage-create-storage-account.md)  
<span data-ttu-id="6971b-158">[Hoge beschikbaarheid](analysis-services-bcdr.md)   </span><span class="sxs-lookup"><span data-stu-id="6971b-158">[High availability](analysis-services-bcdr.md)   </span></span>  
[<span data-ttu-id="6971b-159">Azure analyseservices beheren</span><span class="sxs-lookup"><span data-stu-id="6971b-159">Manage Azure Analysis Services</span></span>](analysis-services-manage.md)
