---
title: Back-up maken van uw app in Azure
description: Informatie over het maken van back-ups van uw apps in Azure App Service.
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 6223b6bd-84ec-48df-943f-461d84605694
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: 77e983afaaba8e944ab1f337e1c28ced83b63205
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="back-up-your-app-in-azure"></a><span data-ttu-id="39779-103">Back-up maken van uw app in Azure</span><span class="sxs-lookup"><span data-stu-id="39779-103">Back up your app in Azure</span></span>
<span data-ttu-id="39779-104">De Back up en herstel-functie in [Azure App Service](../app-service/app-service-value-prop-what-is.md) kunt u eenvoudig back-ups van app handmatig of volgens een planning aan te maken.</span><span class="sxs-lookup"><span data-stu-id="39779-104">The Back up and Restore feature in [Azure App Service](../app-service/app-service-value-prop-what-is.md) lets you easily create app backups manually or on a schedule.</span></span> <span data-ttu-id="39779-105">U kunt de app naar een momentopname van een eerdere status herstellen door het overschrijven van de bestaande app of het herstellen naar een andere app.</span><span class="sxs-lookup"><span data-stu-id="39779-105">You can restore the app to a snapshot of a previous state by overwriting the existing app or restoring to another app.</span></span> 

<span data-ttu-id="39779-106">Zie voor informatie over het herstellen van een app van back-up, [herstellen van een app in Azure](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="39779-106">For information on restoring an app from backup, see [Restore an app in Azure](web-sites-restore.md).</span></span>

<a name="whatsbackedup"></a>

## <a name="what-gets-backed-up"></a><span data-ttu-id="39779-107">Wat wordt een back-up</span><span class="sxs-lookup"><span data-stu-id="39779-107">What gets backed up</span></span>
<span data-ttu-id="39779-108">App Service kunt back-up van de volgende informatie naar een Azure-opslagaccount en container die u hebt geconfigureerd dat uw app te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="39779-108">App Service can backup the following information to an Azure storage account and container that you have configured your app to use.</span></span> 

* <span data-ttu-id="39779-109">App-configuratie</span><span class="sxs-lookup"><span data-stu-id="39779-109">App configuration</span></span>
* <span data-ttu-id="39779-110">Bestandsinhoud</span><span class="sxs-lookup"><span data-stu-id="39779-110">File content</span></span>
* <span data-ttu-id="39779-111">Database verbonden met uw app</span><span class="sxs-lookup"><span data-stu-id="39779-111">Database connected to your app</span></span>

<span data-ttu-id="39779-112">De volgende databaseoplossingen worden met de functie back-ups ondersteund:</span><span class="sxs-lookup"><span data-stu-id="39779-112">The following database solutions are supported with backup feature:</span></span> 
   - [<span data-ttu-id="39779-113">SQL Database</span><span class="sxs-lookup"><span data-stu-id="39779-113">SQL Database</span></span>](https://azure.microsoft.com/en-us/services/sql-database/)
   - [<span data-ttu-id="39779-114">Azure-Database voor MySQL (Preview)</span><span class="sxs-lookup"><span data-stu-id="39779-114">Azure Database for MySQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/mysql)
   - [<span data-ttu-id="39779-115">Azure-Database voor PostgreSQL (Preview)</span><span class="sxs-lookup"><span data-stu-id="39779-115">Azure Database for PostgreSQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/postgres)
   - [<span data-ttu-id="39779-116">ClearDB MySQL</span><span class="sxs-lookup"><span data-stu-id="39779-116">ClearDB MySQL</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
   - [<span data-ttu-id="39779-117">MySQL in-app</span><span class="sxs-lookup"><span data-stu-id="39779-117">MySQL in-app</span></span>](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)
 

> [!NOTE]
>  <span data-ttu-id="39779-118">Elke back-up is een volledige offline kopie van uw app, niet een incrementele update.</span><span class="sxs-lookup"><span data-stu-id="39779-118">Each backup is a complete offline copy of your app, not an incremental update.</span></span>
>  

<a name="requirements"></a>

## <a name="requirements-and-restrictions"></a><span data-ttu-id="39779-119">Vereisten en beperkingen</span><span class="sxs-lookup"><span data-stu-id="39779-119">Requirements and restrictions</span></span>
* <span data-ttu-id="39779-120">De Back up en herstel onderdeel vereist het App Service-abonnement in de **standaard** laag of **Premium** laag.</span><span class="sxs-lookup"><span data-stu-id="39779-120">The Back up and Restore feature requires the App Service plan to be in the **Standard** tier or **Premium** tier.</span></span> <span data-ttu-id="39779-121">Zie voor meer informatie over het schalen van uw App Service-abonnement te gebruiken van een hogere laag [een app in Azure opschalen](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="39779-121">For more information about scaling your App Service plan to use a higher tier, see [Scale up an app in Azure](web-sites-scale.md).</span></span>  
  <span data-ttu-id="39779-122">**Premium** laag kan een groter aantal dagelijks back-ups dan **standaard** laag.</span><span class="sxs-lookup"><span data-stu-id="39779-122">**Premium** tier allows a greater number of daily back ups than **Standard** tier.</span></span>
* <span data-ttu-id="39779-123">U moet een Azure-opslagaccount en container in hetzelfde abonnement als de app die u wilt back-up.</span><span class="sxs-lookup"><span data-stu-id="39779-123">You need an Azure storage account and container in the same subscription as the app that you want to backup.</span></span> <span data-ttu-id="39779-124">Zie voor meer informatie over Azure storage-accounts, het [koppelingen](#moreaboutstorage) aan het einde van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="39779-124">For more information on Azure storage accounts, see the [links](#moreaboutstorage) at the end of this article.</span></span>
* <span data-ttu-id="39779-125">Back-ups mag maximaal 10 GB-app en database-inhoud.</span><span class="sxs-lookup"><span data-stu-id="39779-125">Backups can be up to 10 GB of app and database content.</span></span> <span data-ttu-id="39779-126">Als de back-upgrootte deze limiet overschrijdt, krijgt u een fout opgetreden.</span><span class="sxs-lookup"><span data-stu-id="39779-126">If the backup size exceeds this limit, you get an error .</span></span>

<a name="manualbackup"></a>

## <a name="create-a-manual-backup"></a><span data-ttu-id="39779-127">Een handmatige back-up maken</span><span class="sxs-lookup"><span data-stu-id="39779-127">Create a manual backup</span></span>
1. <span data-ttu-id="39779-128">In de [Azure Portal](https://portal.azure.com), gaat u naar de blade van uw app, selecteer **back-ups**.</span><span class="sxs-lookup"><span data-stu-id="39779-128">In the [Azure Portal](https://portal.azure.com), navigate to your app's blade, select **Backups**.</span></span> <span data-ttu-id="39779-129">De **back-ups** blade wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="39779-129">The **Backups** blade will be displayed.</span></span>
   
    ![Back-ups pagina][ChooseBackupsPage]
   
   > [!NOTE]
   > <span data-ttu-id="39779-131">Als u de onderstaande bericht ziet, klikt u op om uw App Service-abonnement upgraden voordat u kunt doorgaan met de back-ups.</span><span class="sxs-lookup"><span data-stu-id="39779-131">If you see the message below, click it to upgrade your App Service plan before you can proceed with backups.</span></span>
   > <span data-ttu-id="39779-132">Zie [een app in Azure opschalen](web-sites-scale.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="39779-132">See [Scale up an app in Azure](web-sites-scale.md) for more information.</span></span>  
   > <span data-ttu-id="39779-133">![Opslagaccount kiezen](./media/web-sites-backup/01UpgradePlan1.png)</span><span class="sxs-lookup"><span data-stu-id="39779-133">![Choose storage account](./media/web-sites-backup/01UpgradePlan1.png)</span></span>
   > 
   > 

2. <span data-ttu-id="39779-134">In de **back-up** blade, klikt u op **configureren**
![klikt u op configureren](./media/web-sites-backup/ClickConfigure1.png)</span><span class="sxs-lookup"><span data-stu-id="39779-134">In the **Backup** blade, Click **Configure**
![Click Configure](./media/web-sites-backup/ClickConfigure1.png)</span></span>
3. <span data-ttu-id="39779-135">In de **back-upconfiguratie** blade, klikt u op **opslag: niet geconfigureerd** voor het configureren van een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="39779-135">In the **Backup Configuration** blade, click **Storage: Not configured** to configure a storage account.</span></span>
   
    ![Opslagaccount kiezen][ChooseStorageAccount]
4. <span data-ttu-id="39779-137">Kies uw back-upbestemming door te selecteren een **Opslagaccount** en **Container**.</span><span class="sxs-lookup"><span data-stu-id="39779-137">Choose your backup destination by selecting a **Storage Account** and **Container**.</span></span> <span data-ttu-id="39779-138">Het opslagaccount moet behoren tot hetzelfde abonnement als de app die u back wilt-up.</span><span class="sxs-lookup"><span data-stu-id="39779-138">The storage account must belong to the same subscription as the app you want to back up.</span></span> <span data-ttu-id="39779-139">Als u wenst, kunt u een nieuw opslagaccount of een nieuwe container maken in de respectievelijke blades.</span><span class="sxs-lookup"><span data-stu-id="39779-139">If you wish, you can create a new storage account or a new container in the respective blades.</span></span> <span data-ttu-id="39779-140">Wanneer u bent klaar, klikt u op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="39779-140">When you're done, click **Select**.</span></span>
   
    ![Opslagaccount kiezen](./media/web-sites-backup/02ChooseStorageAccount1-1.png)
5. <span data-ttu-id="39779-142">In de **back-upconfiguratie** blade die nog steeds open blijft, kunt u configureren **Backup Database**, selecteert u de databases die u wilt opnemen in de back-ups (SQL-database of MySQL) en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="39779-142">In the **Backup Configuration** blade that is still left open, you can configure **Backup Database**, then select the databases you want to include in the backups (SQL database or MySQL), then click **OK**.</span></span>  
   
    ![Opslagaccount kiezen](./media/web-sites-backup/03ConfigureDatabase1.png)
   
   > [!NOTE]
   > <span data-ttu-id="39779-144">Voor een database worden weergegeven in deze lijst, de verbindingsreeks moet aanwezig zijn in de **verbindingsreeksen** sectie van de **toepassingsinstellingen** blade voor uw app.</span><span class="sxs-lookup"><span data-stu-id="39779-144">For a database to appear in this list, its connection string must exist in the **Connection strings** section of the **Application settings** blade for your app.</span></span>
   > 
   > 
6. <span data-ttu-id="39779-145">In de **back-upconfiguratie** blade, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="39779-145">In the **Backup Configuration** blade, click **Save**.</span></span>    
7. <span data-ttu-id="39779-146">In de **back-ups** blade, klikt u op **back-up**.</span><span class="sxs-lookup"><span data-stu-id="39779-146">In the  **Backups** blade, click **Backup**.</span></span>
   
    ![Knop BackUpNow][BackUpNow]
   
    <span data-ttu-id="39779-148">U ziet een bericht uitgevoerd tijdens de back-upproces.</span><span class="sxs-lookup"><span data-stu-id="39779-148">You see a progress message during the backup process.</span></span>

<span data-ttu-id="39779-149">Zodra het opslagaccount en container is geconfigureerd kunt u een handmatige back-up op elk gewenst moment kunt starten.</span><span class="sxs-lookup"><span data-stu-id="39779-149">Once the storage account and container is configured you can initiate a manual backup at any time.</span></span>  

<a name="automatedbackups"></a>

## <a name="configure-automated-backups"></a><span data-ttu-id="39779-150">Automatische back-ups configureren</span><span class="sxs-lookup"><span data-stu-id="39779-150">Configure automated backups</span></span>
1. <span data-ttu-id="39779-151">In de **back-upconfiguratie** blade ingesteld **geplande back-up** naar **op**.</span><span class="sxs-lookup"><span data-stu-id="39779-151">In the **Backup Configuration** blade, set **Scheduled backup** to **On**.</span></span> 
   
    ![Opslagaccount kiezen](./media/web-sites-backup/05ScheduleBackup1.png)
2. <span data-ttu-id="39779-153">Back-upschema opties wordt weergegeven, stel **geplande back-** naar **op**, configureer de gewenste back-upschema en klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="39779-153">Backup schedule options will show up, set **Scheduled Backup** to **On**, then configure the backup schedule as desired and click **OK**.</span></span>
   
    ![Automatische back-ups inschakelen][SetAutomatedBackupOn]

<a name="partialbackups"></a>

## <a name="configure-partial-backups"></a><span data-ttu-id="39779-155">Gedeeltelijke back-ups configureren</span><span class="sxs-lookup"><span data-stu-id="39779-155">Configure Partial Backups</span></span>
<span data-ttu-id="39779-156">Soms wilt u geen back-up van alle bestanden op uw app.</span><span class="sxs-lookup"><span data-stu-id="39779-156">Sometimes you don't want to backup everything on your app.</span></span> <span data-ttu-id="39779-157">Enkele voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="39779-157">Here are a few examples:</span></span>

* <span data-ttu-id="39779-158">U [wekelijkse back-ups instellen](web-sites-backup.md#configure-automated-backups) van uw app met statische inhoud, die nooit wordt gewijzigd, zoals oude blogberichten of installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="39779-158">You [set up weekly backups](web-sites-backup.md#configure-automated-backups) of your app that contains static content that never changes, such as old blog posts or images.</span></span>
* <span data-ttu-id="39779-159">Uw app heeft meer dan 10 GB aan inhoud (dat wil zeggen de maximale hoeveelheid die kunt u de back-up op een tijdstip).</span><span class="sxs-lookup"><span data-stu-id="39779-159">Your app has over 10 GB of content (that's the max amount you can backup at a time).</span></span>
* <span data-ttu-id="39779-160">U wilt niet dat back-up van de logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="39779-160">You don't want to backup the log files.</span></span>

<span data-ttu-id="39779-161">Gedeeltelijke back-ups kunt u kiezen exact bestanden die u wilt back-up.</span><span class="sxs-lookup"><span data-stu-id="39779-161">Partial backups allows you choose exactly which files you want to backup.</span></span>

### <a name="exclude-files-from-your-backup"></a><span data-ttu-id="39779-162">Bestanden uitsluiten van uw back-up</span><span class="sxs-lookup"><span data-stu-id="39779-162">Exclude files from your backup</span></span>
<span data-ttu-id="39779-163">Stel dat u hebt een app met logboekbestanden en statische afbeeldingen die zijn back-up eenmaal en gaat niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="39779-163">Suppose you have an app that contains log files and static images that have been backup once and are not going to change.</span></span> <span data-ttu-id="39779-164">In dergelijke gevallen kunt u de mappen en bestanden uitsluiten van wordt opgeslagen in uw toekomstige back-ups.</span><span class="sxs-lookup"><span data-stu-id="39779-164">In such cases you can exclude those folders and files from being stored in your future backups.</span></span> <span data-ttu-id="39779-165">Als u wilt uitsluiten van bestanden en mappen van uw back-ups, maakt een `_backup.filter` bestand de `D:\home\site\wwwroot` map van uw app.</span><span class="sxs-lookup"><span data-stu-id="39779-165">To exclude files and folders from your backups, create a `_backup.filter` file in the `D:\home\site\wwwroot` folder of your app.</span></span> <span data-ttu-id="39779-166">Geef de lijst van bestanden en mappen die u wilt uitsluiten in dit bestand.</span><span class="sxs-lookup"><span data-stu-id="39779-166">Specify the list of files and folders you want to exclude in this file.</span></span> 

<span data-ttu-id="39779-167">Een eenvoudige manier om toegang tot uw bestanden is het gebruik van Kudu.</span><span class="sxs-lookup"><span data-stu-id="39779-167">An easy way to access your files is to use Kudu .</span></span> <span data-ttu-id="39779-168">Klik op **geavanceerde hulpprogramma's -> Ga** instellen voor uw web-app voor toegang tot Kudu.</span><span class="sxs-lookup"><span data-stu-id="39779-168">Click **Advanced Tools -> Go** setting for your web app to access Kudu.</span></span>

![Kudu met portal][kudu-portal]

<span data-ttu-id="39779-170">Identificeer de mappen die u wilt uitsluiten van uw back-ups.</span><span class="sxs-lookup"><span data-stu-id="39779-170">Identify the folders that you want to exclude from your backups.</span></span>  <span data-ttu-id="39779-171">Bijvoorbeeld, wilt u filteren van de geselecteerde map en bestanden.</span><span class="sxs-lookup"><span data-stu-id="39779-171">For example , you want to filter out the highlighted folder and files.</span></span>

![Map installatiekopieën][ImagesFolder]

<span data-ttu-id="39779-173">Maken van een bestand met de naam `_backup.filter` en de bovenstaande lijst plaatsen in het bestand, maar Verwijder `D:\home`.</span><span class="sxs-lookup"><span data-stu-id="39779-173">Create a file called `_backup.filter` and put the list above in the file, but remove `D:\home`.</span></span> <span data-ttu-id="39779-174">Lijst van een directory of bestand per regel.</span><span class="sxs-lookup"><span data-stu-id="39779-174">List one directory or file per line.</span></span> <span data-ttu-id="39779-175">De inhoud van het bestand moet dus:</span><span class="sxs-lookup"><span data-stu-id="39779-175">So the content of the file should be:</span></span>
 ```bash
    \site\wwwroot\Images\brand.png
    \site\wwwroot\Images\2014
    \site\wwwroot\Images\2013
```

<span data-ttu-id="39779-176">Uploaden `_backup.filter` van het bestand in de `D:\home\site\wwwroot\` map van uw site met [ftp](web-sites-deploy.md#ftp) of een andere methode.</span><span class="sxs-lookup"><span data-stu-id="39779-176">Upload `_backup.filter` file to the `D:\home\site\wwwroot\` directory of your site using [ftp](web-sites-deploy.md#ftp) or any other method.</span></span> <span data-ttu-id="39779-177">Als u wenst, kunt u het bestand rechtstreeks met Kudu `DebugConsole` en voeg de inhoud bevat.</span><span class="sxs-lookup"><span data-stu-id="39779-177">If you wish, you can create the file directly using Kudu  `DebugConsole` and insert the content there.</span></span>

<span data-ttu-id="39779-178">Back-ups uitvoeren dezelfde manier als u normaal doet, [handmatig](#create-a-manual-backup) of [automatisch](#configure-automated-backups).</span><span class="sxs-lookup"><span data-stu-id="39779-178">Run backups the same way you would normally do it, [manually](#create-a-manual-backup) or [automatically](#configure-automated-backups).</span></span> <span data-ttu-id="39779-179">Nu, worden bestanden en mappen die zijn opgegeven in `_backup.filter` is uitgesloten van de toekomstige back-ups gepland of handmatig is gestart.</span><span class="sxs-lookup"><span data-stu-id="39779-179">Now, any files and folders that are specified in `_backup.filter` is excluded from the future backups scheduled or manually initiated.</span></span> 

> [!NOTE]
> <span data-ttu-id="39779-180">U herstelt gedeeltelijke back-ups van uw site dezelfde manier als u doet [een regelmatige back-up terugzetten](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="39779-180">You restore partial backups of your site the same way you would [restore a regular backup](web-sites-restore.md).</span></span> <span data-ttu-id="39779-181">Het herstelproces komt goede.</span><span class="sxs-lookup"><span data-stu-id="39779-181">The restore process does the right thing.</span></span>
> 
> <span data-ttu-id="39779-182">Wanneer een volledige back-up wordt hersteld, wordt alle inhoud op de site vervangen door de gewenste bevindt zich in de back-up.</span><span class="sxs-lookup"><span data-stu-id="39779-182">When a full backup is restored, all content on the site is replaced with whatever is in the backup.</span></span> <span data-ttu-id="39779-183">Als een bestand op de site, maar niet in de back-up is, wordt deze verwijderd.</span><span class="sxs-lookup"><span data-stu-id="39779-183">If a file is on the site, but not in the backup it gets deleted.</span></span> <span data-ttu-id="39779-184">Maar wanneer een gedeeltelijke back-up wordt hersteld, inhoud die zich in een van de zwarte lijst mappen of een zwarte lijst bestand is ongewijzigd.</span><span class="sxs-lookup"><span data-stu-id="39779-184">But when a partial backup is restored, any content that is located in one of the blacklisted directories, or any blacklisted file, is left as is.</span></span>
> 


<a name="aboutbackups"></a>

## <a name="how-backups-are-stored"></a><span data-ttu-id="39779-185">Hoe de back-ups worden opgeslagen</span><span class="sxs-lookup"><span data-stu-id="39779-185">How backups are stored</span></span>
<span data-ttu-id="39779-186">Nadat u een of meer back-ups voor uw app gemaakt hebt, de back-ups worden weergegeven op de **Containers** blade van uw opslagaccount en uw app.</span><span class="sxs-lookup"><span data-stu-id="39779-186">After you have made one or more backups for your app, the backups are visible on the **Containers** blade of your storage account, and your app.</span></span> <span data-ttu-id="39779-187">In het opslagaccount wordt elke back-up bestaat uit een`.zip` -bestand met de back-upgegevens en een `.xml` -bestand met een manifest van de `.zip` bestand inhoud.</span><span class="sxs-lookup"><span data-stu-id="39779-187">In the storage account, each backup consists of a`.zip` file that contains the backup data and an `.xml` file that contains a manifest of the `.zip` file contents.</span></span> <span data-ttu-id="39779-188">U kunt uitpakken en deze bestanden bladeren als u toegang krijgen tot uw back-ups wilt zonder het daadwerkelijk uitvoeren van een toepassing herstellen.</span><span class="sxs-lookup"><span data-stu-id="39779-188">You can unzip and browse these files if you want to access your backups without actually performing an app restore.</span></span>

<span data-ttu-id="39779-189">De databaseback-up voor de app wordt opgeslagen in de hoofdmap van the.zip-bestand.</span><span class="sxs-lookup"><span data-stu-id="39779-189">The database backup for the app is stored in the root of the.zip file.</span></span> <span data-ttu-id="39779-190">Voor een SQL-database is een Bacpac-bestand (zonder extensie) en kunnen worden geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="39779-190">For a SQL database, this is a BACPAC file (no file extension) and can be imported.</span></span> <span data-ttu-id="39779-191">Zie het maken van een SQL-database op basis van de export Bacpac- [een Bacpac-bestand voor het maken van een nieuwe gebruiker-Database importeren](http://technet.microsoft.com/library/hh710052.aspx).</span><span class="sxs-lookup"><span data-stu-id="39779-191">To create a SQL database based on the BACPAC export, see [Import a BACPAC File to Create a New User Database](http://technet.microsoft.com/library/hh710052.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="39779-192">Wijzigen van de bestanden in uw **websitebackups** container kan leiden tot de back-up worden ongeldig en worden daarom niet-terug te zetten.</span><span class="sxs-lookup"><span data-stu-id="39779-192">Altering any of the files in your **websitebackups** container can cause the backup to become invalid and therefore non-restorable.</span></span>
> 
> 

<a name="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="39779-193">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="39779-193">Next Steps</span></span>
<span data-ttu-id="39779-194">Zie voor informatie over het herstellen van een app van een back-up, [herstellen van een app in Azure](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="39779-194">For information on restoring an app from a backup, see [Restore an app in Azure](web-sites-restore.md).</span></span> <span data-ttu-id="39779-195">U kunt ook back-up en herstellen met behulp van REST-API-App Service-apps (Zie [gebruik REST back-up en herstellen van App Service-apps](websites-csm-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="39779-195">You can also backup and restore App Service apps using REST API (see [Use REST to backup and restore App Service apps](websites-csm-backup.md)).</span></span>


<!-- IMAGES -->
[ChooseBackupsPage]: ./media/web-sites-backup/01ChooseBackupsPage1.png
[ChooseStorageAccount]: ./media/web-sites-backup/02ChooseStorageAccount-1.png
[IncludedDatabases]: ./media/web-sites-backup/03IncludedDatabases.png
[BackUpNow]: ./media/web-sites-backup/04BackUpNow1.png
[BackupProgress]: ./media/web-sites-backup/05BackupProgress.png
[SetAutomatedBackupOn]: ./media/web-sites-backup/06SetAutomatedBackupOn1.png
[Frequency]: ./media/web-sites-backup/07Frequency.png
[StartDate]: ./media/web-sites-backup/08StartDate.png
[StartTime]: ./media/web-sites-backup/09StartTime.png
[SaveIcon]: ./media/web-sites-backup/10SaveIcon.png
[ImagesFolder]: ./media/web-sites-backup/11Images.png
[LogsFolder]: ./media/web-sites-backup/12Logs.png
[GhostUpgradeWarning]: ./media/web-sites-backup/13GhostUpgradeWarning.png
[kudu-portal]:./media/web-sites-backup/kudu-portal.PNG

