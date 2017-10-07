---
title: aaaBack van uw app in Azure
description: Meer informatie over hoe toocreate back-ups van uw apps in Azure App Service.
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
ms.openlocfilehash: e41d93d322bbc48b45b28eeaa817928d83c2b9d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-your-app-in-azure"></a><span data-ttu-id="98c94-103">Back-up maken van uw app in Azure</span><span class="sxs-lookup"><span data-stu-id="98c94-103">Back up your app in Azure</span></span>
<span data-ttu-id="98c94-104">Hallo Back-up en herstellen van de functie in [Azure App Service](../app-service/app-service-value-prop-what-is.md) kunt u eenvoudig back-ups van app handmatig of volgens een planning aan te maken.</span><span class="sxs-lookup"><span data-stu-id="98c94-104">hello Back up and Restore feature in [Azure App Service](../app-service/app-service-value-prop-what-is.md) lets you easily create app backups manually or on a schedule.</span></span> <span data-ttu-id="98c94-105">U kunt Hallo app tooa momentopname van een eerdere status door overschrijven Hallo bestaande app of terugzetten tooanother app herstellen.</span><span class="sxs-lookup"><span data-stu-id="98c94-105">You can restore hello app tooa snapshot of a previous state by overwriting hello existing app or restoring tooanother app.</span></span> 

<span data-ttu-id="98c94-106">Zie voor informatie over het herstellen van een app van back-up, [herstellen van een app in Azure](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="98c94-106">For information on restoring an app from backup, see [Restore an app in Azure](web-sites-restore.md).</span></span>

<a name="whatsbackedup"></a>

## <a name="what-gets-backed-up"></a><span data-ttu-id="98c94-107">Wat wordt een back-up</span><span class="sxs-lookup"><span data-stu-id="98c94-107">What gets backed up</span></span>
<span data-ttu-id="98c94-108">App Service kunt back-up Hallo volgende informatie tooan Azure-opslagaccount en container dat u uw app toouse hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="98c94-108">App Service can backup hello following information tooan Azure storage account and container that you have configured your app toouse.</span></span> 

* <span data-ttu-id="98c94-109">App-configuratie</span><span class="sxs-lookup"><span data-stu-id="98c94-109">App configuration</span></span>
* <span data-ttu-id="98c94-110">Bestandsinhoud</span><span class="sxs-lookup"><span data-stu-id="98c94-110">File content</span></span>
* <span data-ttu-id="98c94-111">Database verbonden tooyour app</span><span class="sxs-lookup"><span data-stu-id="98c94-111">Database connected tooyour app</span></span>

<span data-ttu-id="98c94-112">Hallo database-oplossingen te volgen worden met de functie back-ups ondersteund:</span><span class="sxs-lookup"><span data-stu-id="98c94-112">hello following database solutions are supported with backup feature:</span></span> 
   - [<span data-ttu-id="98c94-113">SQL Database</span><span class="sxs-lookup"><span data-stu-id="98c94-113">SQL Database</span></span>](https://azure.microsoft.com/en-us/services/sql-database/)
   - [<span data-ttu-id="98c94-114">Azure-Database voor MySQL (Preview)</span><span class="sxs-lookup"><span data-stu-id="98c94-114">Azure Database for MySQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/mysql)
   - [<span data-ttu-id="98c94-115">Azure-Database voor PostgreSQL (Preview)</span><span class="sxs-lookup"><span data-stu-id="98c94-115">Azure Database for PostgreSQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/postgres)
   - [<span data-ttu-id="98c94-116">ClearDB MySQL</span><span class="sxs-lookup"><span data-stu-id="98c94-116">ClearDB MySQL</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
   - [<span data-ttu-id="98c94-117">MySQL in-app</span><span class="sxs-lookup"><span data-stu-id="98c94-117">MySQL in-app</span></span>](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)
 

> [!NOTE]
>  <span data-ttu-id="98c94-118">Elke back-up is een volledige offline kopie van uw app, niet een incrementele update.</span><span class="sxs-lookup"><span data-stu-id="98c94-118">Each backup is a complete offline copy of your app, not an incremental update.</span></span>
>  

<a name="requirements"></a>

## <a name="requirements-and-restrictions"></a><span data-ttu-id="98c94-119">Vereisten en beperkingen</span><span class="sxs-lookup"><span data-stu-id="98c94-119">Requirements and restrictions</span></span>
* <span data-ttu-id="98c94-120">Hallo Back-up en terugzetten functie vereist Hallo App Service plan toobe in Hallo **standaard** laag of **Premium** laag.</span><span class="sxs-lookup"><span data-stu-id="98c94-120">hello Back up and Restore feature requires hello App Service plan toobe in hello **Standard** tier or **Premium** tier.</span></span> <span data-ttu-id="98c94-121">Zie voor meer informatie over het schalen van uw App Service plan toouse een hogere laag [een app in Azure opschalen](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="98c94-121">For more information about scaling your App Service plan toouse a higher tier, see [Scale up an app in Azure](web-sites-scale.md).</span></span>  
  <span data-ttu-id="98c94-122">**Premium** laag kan een groter aantal dagelijks back-ups dan **standaard** laag.</span><span class="sxs-lookup"><span data-stu-id="98c94-122">**Premium** tier allows a greater number of daily back ups than **Standard** tier.</span></span>
* <span data-ttu-id="98c94-123">U moet een Azure-opslagaccount en container in Hallo hetzelfde abonnement als Hallo-app die u toobackup wilt.</span><span class="sxs-lookup"><span data-stu-id="98c94-123">You need an Azure storage account and container in hello same subscription as hello app that you want toobackup.</span></span> <span data-ttu-id="98c94-124">Zie voor meer informatie over Azure storage-accounts Hallo [koppelingen](#moreaboutstorage) aan Hallo einde van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="98c94-124">For more information on Azure storage accounts, see hello [links](#moreaboutstorage) at hello end of this article.</span></span>
* <span data-ttu-id="98c94-125">Back-ups kunnen van de app en database inhoud too10 GB zijn.</span><span class="sxs-lookup"><span data-stu-id="98c94-125">Backups can be up too10 GB of app and database content.</span></span> <span data-ttu-id="98c94-126">Als het Hallo-back-upgrootte overschrijdt deze limiet, krijgt u een fout opgetreden.</span><span class="sxs-lookup"><span data-stu-id="98c94-126">If hello backup size exceeds this limit, you get an error .</span></span>

<a name="manualbackup"></a>

## <a name="create-a-manual-backup"></a><span data-ttu-id="98c94-127">Een handmatige back-up maken</span><span class="sxs-lookup"><span data-stu-id="98c94-127">Create a manual backup</span></span>
1. <span data-ttu-id="98c94-128">In Hallo [Azure Portal](https://portal.azure.com), navigeer blade tooyour-app, selecteer **back-ups**.</span><span class="sxs-lookup"><span data-stu-id="98c94-128">In hello [Azure Portal](https://portal.azure.com), navigate tooyour app's blade, select **Backups**.</span></span> <span data-ttu-id="98c94-129">Hallo **back-ups** blade wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="98c94-129">hello **Backups** blade will be displayed.</span></span>
   
    ![Back-ups pagina][ChooseBackupsPage]
   
   > [!NOTE]
   > <span data-ttu-id="98c94-131">Als u het Hallo-bericht hieronder ziet, klikt u erop tooupgrade uw App Service-abonnement voordat u verder kunt gaan met back-ups.</span><span class="sxs-lookup"><span data-stu-id="98c94-131">If you see hello message below, click it tooupgrade your App Service plan before you can proceed with backups.</span></span>
   > <span data-ttu-id="98c94-132">Zie [een app in Azure opschalen](web-sites-scale.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="98c94-132">See [Scale up an app in Azure](web-sites-scale.md) for more information.</span></span>  
   > <span data-ttu-id="98c94-133">![Opslagaccount kiezen](./media/web-sites-backup/01UpgradePlan1.png)</span><span class="sxs-lookup"><span data-stu-id="98c94-133">![Choose storage account](./media/web-sites-backup/01UpgradePlan1.png)</span></span>
   > 
   > 

2. <span data-ttu-id="98c94-134">In Hallo **back-up** blade, klikt u op **configureren**
![klikt u op configureren](./media/web-sites-backup/ClickConfigure1.png)</span><span class="sxs-lookup"><span data-stu-id="98c94-134">In hello **Backup** blade, Click **Configure**
![Click Configure](./media/web-sites-backup/ClickConfigure1.png)</span></span>
3. <span data-ttu-id="98c94-135">In Hallo **back-upconfiguratie** blade, klikt u op **opslag: niet geconfigureerd** tooconfigure een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="98c94-135">In hello **Backup Configuration** blade, click **Storage: Not configured** tooconfigure a storage account.</span></span>
   
    ![Opslagaccount kiezen][ChooseStorageAccount]
4. <span data-ttu-id="98c94-137">Kies uw back-upbestemming door te selecteren een **Opslagaccount** en **Container**.</span><span class="sxs-lookup"><span data-stu-id="98c94-137">Choose your backup destination by selecting a **Storage Account** and **Container**.</span></span> <span data-ttu-id="98c94-138">Hallo storage-account moet behoren toohello hetzelfde abonnement als u wilt dat tooback up Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="98c94-138">hello storage account must belong toohello same subscription as hello app you want tooback up.</span></span> <span data-ttu-id="98c94-139">Als u wenst, kunt u een nieuw opslagaccount of een nieuwe container in Hallo respectievelijke blades.</span><span class="sxs-lookup"><span data-stu-id="98c94-139">If you wish, you can create a new storage account or a new container in hello respective blades.</span></span> <span data-ttu-id="98c94-140">Wanneer u bent klaar, klikt u op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="98c94-140">When you're done, click **Select**.</span></span>
   
    ![Opslagaccount kiezen](./media/web-sites-backup/02ChooseStorageAccount1-1.png)
5. <span data-ttu-id="98c94-142">In Hallo **back-upconfiguratie** blade die nog steeds open blijft, kunt u configureren **Backup Database**, selecteer vervolgens Hallo databases u wilt dat tooinclude in Hallo back-ups (SQL-database of MySQL) en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="98c94-142">In hello **Backup Configuration** blade that is still left open, you can configure **Backup Database**, then select hello databases you want tooinclude in hello backups (SQL database or MySQL), then click **OK**.</span></span>  
   
    ![Opslagaccount kiezen](./media/web-sites-backup/03ConfigureDatabase1.png)
   
   > [!NOTE]
   > <span data-ttu-id="98c94-144">Voor een database tooappear in deze lijst, de verbindingsreeks moet aanwezig zijn in Hallo **verbindingsreeksen** sectie Hallo **toepassingsinstellingen** blade voor uw app.</span><span class="sxs-lookup"><span data-stu-id="98c94-144">For a database tooappear in this list, its connection string must exist in hello **Connection strings** section of hello **Application settings** blade for your app.</span></span>
   > 
   > 
6. <span data-ttu-id="98c94-145">In Hallo **back-upconfiguratie** blade, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="98c94-145">In hello **Backup Configuration** blade, click **Save**.</span></span>    
7. <span data-ttu-id="98c94-146">In Hallo **back-ups** blade, klikt u op **back-up**.</span><span class="sxs-lookup"><span data-stu-id="98c94-146">In hello  **Backups** blade, click **Backup**.</span></span>
   
    ![Knop BackUpNow][BackUpNow]
   
    <span data-ttu-id="98c94-148">U ziet een bericht uitgevoerd tijdens de back-upproces Hallo.</span><span class="sxs-lookup"><span data-stu-id="98c94-148">You see a progress message during hello backup process.</span></span>

<span data-ttu-id="98c94-149">Zodra het Hallo-opslagaccount en container is geconfigureerd kunt u een handmatige back-up op elk gewenst moment kunt starten.</span><span class="sxs-lookup"><span data-stu-id="98c94-149">Once hello storage account and container is configured you can initiate a manual backup at any time.</span></span>  

<a name="automatedbackups"></a>

## <a name="configure-automated-backups"></a><span data-ttu-id="98c94-150">Automatische back-ups configureren</span><span class="sxs-lookup"><span data-stu-id="98c94-150">Configure automated backups</span></span>
1. <span data-ttu-id="98c94-151">In Hallo **back-upconfiguratie** blade ingesteld **geplande back-up** te**op**.</span><span class="sxs-lookup"><span data-stu-id="98c94-151">In hello **Backup Configuration** blade, set **Scheduled backup** too**On**.</span></span> 
   
    ![Opslagaccount kiezen](./media/web-sites-backup/05ScheduleBackup1.png)
2. <span data-ttu-id="98c94-153">Back-upschema opties wordt weergegeven, stel **geplande back-** te**op**, configureer de gewenste Hallo back-upschema en klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="98c94-153">Backup schedule options will show up, set **Scheduled Backup** too**On**, then configure hello backup schedule as desired and click **OK**.</span></span>
   
    ![Automatische back-ups inschakelen][SetAutomatedBackupOn]

<a name="partialbackups"></a>

## <a name="configure-partial-backups"></a><span data-ttu-id="98c94-155">Gedeeltelijke back-ups configureren</span><span class="sxs-lookup"><span data-stu-id="98c94-155">Configure Partial Backups</span></span>
<span data-ttu-id="98c94-156">Soms wilt u niet toobackup alles in uw app.</span><span class="sxs-lookup"><span data-stu-id="98c94-156">Sometimes you don't want toobackup everything on your app.</span></span> <span data-ttu-id="98c94-157">Enkele voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="98c94-157">Here are a few examples:</span></span>

* <span data-ttu-id="98c94-158">U [wekelijkse back-ups instellen](web-sites-backup.md#configure-automated-backups) van uw app met statische inhoud, die nooit wordt gewijzigd, zoals oude blogberichten of installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="98c94-158">You [set up weekly backups](web-sites-backup.md#configure-automated-backups) of your app that contains static content that never changes, such as old blog posts or images.</span></span>
* <span data-ttu-id="98c94-159">Uw app heeft meer dan 10 GB aan inhoud (dat wil zeggen Hallo max bedrag die kunt u de back-up op een tijdstip).</span><span class="sxs-lookup"><span data-stu-id="98c94-159">Your app has over 10 GB of content (that's hello max amount you can backup at a time).</span></span>
* <span data-ttu-id="98c94-160">U wilt niet dat toobackup Hallo-logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="98c94-160">You don't want toobackup hello log files.</span></span>

<span data-ttu-id="98c94-161">Gedeeltelijke back-ups kunt u kiezen exact bestanden die u wilt dat toobackup.</span><span class="sxs-lookup"><span data-stu-id="98c94-161">Partial backups allows you choose exactly which files you want toobackup.</span></span>

### <a name="exclude-files-from-your-backup"></a><span data-ttu-id="98c94-162">Bestanden uitsluiten van uw back-up</span><span class="sxs-lookup"><span data-stu-id="98c94-162">Exclude files from your backup</span></span>
<span data-ttu-id="98c94-163">Stel dat u hebt een app met logboekbestanden en statische afbeeldingen die zijn back-up eenmaal en toochange niet gaat.</span><span class="sxs-lookup"><span data-stu-id="98c94-163">Suppose you have an app that contains log files and static images that have been backup once and are not going toochange.</span></span> <span data-ttu-id="98c94-164">In dergelijke gevallen kunt u de mappen en bestanden uitsluiten van wordt opgeslagen in uw toekomstige back-ups.</span><span class="sxs-lookup"><span data-stu-id="98c94-164">In such cases you can exclude those folders and files from being stored in your future backups.</span></span> <span data-ttu-id="98c94-165">tooexclude bestanden en mappen van uw back-ups maken van een `_backup.filter` bestand in Hallo `D:\home\site\wwwroot` map van uw app.</span><span class="sxs-lookup"><span data-stu-id="98c94-165">tooexclude files and folders from your backups, create a `_backup.filter` file in hello `D:\home\site\wwwroot` folder of your app.</span></span> <span data-ttu-id="98c94-166">Hallo-lijst van bestanden en mappen die u wilt dat tooexclude in dit bestand opgeven.</span><span class="sxs-lookup"><span data-stu-id="98c94-166">Specify hello list of files and folders you want tooexclude in this file.</span></span> 

<span data-ttu-id="98c94-167">Een eenvoudige manier tooaccess uw bestanden toouse Kudu is.</span><span class="sxs-lookup"><span data-stu-id="98c94-167">An easy way tooaccess your files is toouse Kudu .</span></span> <span data-ttu-id="98c94-168">Klik op **geavanceerde hulpprogramma's -> Ga** instellen voor uw web-app tooaccess Kudu.</span><span class="sxs-lookup"><span data-stu-id="98c94-168">Click **Advanced Tools -> Go** setting for your web app tooaccess Kudu.</span></span>

![Kudu met portal][kudu-portal]

<span data-ttu-id="98c94-170">Hallo-mappen die u tooexclude vanuit uw back-ups wilt identificeren.</span><span class="sxs-lookup"><span data-stu-id="98c94-170">Identify hello folders that you want tooexclude from your backups.</span></span>  <span data-ttu-id="98c94-171">U wilt bijvoorbeeld toofilter Hallo gemarkeerde map en bestanden.</span><span class="sxs-lookup"><span data-stu-id="98c94-171">For example , you want toofilter out hello highlighted folder and files.</span></span>

![Map installatiekopieën][ImagesFolder]

<span data-ttu-id="98c94-173">Maken van een bestand met de naam `_backup.filter` en Hallo bovenstaande lijst plaatsen in Hallo-bestand, maar Verwijder `D:\home`.</span><span class="sxs-lookup"><span data-stu-id="98c94-173">Create a file called `_backup.filter` and put hello list above in hello file, but remove `D:\home`.</span></span> <span data-ttu-id="98c94-174">Lijst van een directory of bestand per regel.</span><span class="sxs-lookup"><span data-stu-id="98c94-174">List one directory or file per line.</span></span> <span data-ttu-id="98c94-175">Dus moet Hallo inhoud van het Hallo-bestand:</span><span class="sxs-lookup"><span data-stu-id="98c94-175">So hello content of hello file should be:</span></span>
 ```bash
    \site\wwwroot\Images\brand.png
    \site\wwwroot\Images\2014
    \site\wwwroot\Images\2013
```

<span data-ttu-id="98c94-176">Uploaden `_backup.filter` bestand toohello `D:\home\site\wwwroot\` map van uw site met [ftp](web-sites-deploy.md#ftp) of een andere methode.</span><span class="sxs-lookup"><span data-stu-id="98c94-176">Upload `_backup.filter` file toohello `D:\home\site\wwwroot\` directory of your site using [ftp](web-sites-deploy.md#ftp) or any other method.</span></span> <span data-ttu-id="98c94-177">Als u wenst, kunt u Hallo-bestand rechtstreeks met Kudu `DebugConsole` en voeg de er Hallo-inhoud.</span><span class="sxs-lookup"><span data-stu-id="98c94-177">If you wish, you can create hello file directly using Kudu  `DebugConsole` and insert hello content there.</span></span>

<span data-ttu-id="98c94-178">Voer back-ups Hallo dezelfde manier zou u dat gewend bent, [handmatig](#create-a-manual-backup) of [automatisch](#configure-automated-backups).</span><span class="sxs-lookup"><span data-stu-id="98c94-178">Run backups hello same way you would normally do it, [manually](#create-a-manual-backup) or [automatically](#configure-automated-backups).</span></span> <span data-ttu-id="98c94-179">Nu, worden bestanden en mappen die zijn opgegeven in `_backup.filter` is uitgesloten van Hallo toekomstige back-ups gepland of handmatig is gestart.</span><span class="sxs-lookup"><span data-stu-id="98c94-179">Now, any files and folders that are specified in `_backup.filter` is excluded from hello future backups scheduled or manually initiated.</span></span> 

> [!NOTE]
> <span data-ttu-id="98c94-180">Herstellen van gedeeltelijke back-ups van uw site Hallo dezelfde manier als [een regelmatige back-up terugzetten](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="98c94-180">You restore partial backups of your site hello same way you would [restore a regular backup](web-sites-restore.md).</span></span> <span data-ttu-id="98c94-181">het herstelproces Hallo wat u Hallo.</span><span class="sxs-lookup"><span data-stu-id="98c94-181">hello restore process does hello right thing.</span></span>
> 
> <span data-ttu-id="98c94-182">Wanneer een volledige back-up wordt hersteld, wordt alle inhoud op Hallo site vervangen met de Hallo back-up.</span><span class="sxs-lookup"><span data-stu-id="98c94-182">When a full backup is restored, all content on hello site is replaced with whatever is in hello backup.</span></span> <span data-ttu-id="98c94-183">Als een bestand op Hallo-site, maar niet in de back-up hello wordt deze verwijderd.</span><span class="sxs-lookup"><span data-stu-id="98c94-183">If a file is on hello site, but not in hello backup it gets deleted.</span></span> <span data-ttu-id="98c94-184">Maar wanneer een gedeeltelijke back-up wordt hersteld, inhoud die zich in een van de mappen gebeurd hello of een zwarte lijst bestand, is ongewijzigd.</span><span class="sxs-lookup"><span data-stu-id="98c94-184">But when a partial backup is restored, any content that is located in one of hello blacklisted directories, or any blacklisted file, is left as is.</span></span>
> 


<a name="aboutbackups"></a>

## <a name="how-backups-are-stored"></a><span data-ttu-id="98c94-185">Hoe de back-ups worden opgeslagen</span><span class="sxs-lookup"><span data-stu-id="98c94-185">How backups are stored</span></span>
<span data-ttu-id="98c94-186">Nadat u een of meer back-ups voor uw app gemaakt hebt, Hallo back-ups zijn zichtbaar op Hallo **Containers** blade van uw opslagaccount en uw app.</span><span class="sxs-lookup"><span data-stu-id="98c94-186">After you have made one or more backups for your app, hello backups are visible on hello **Containers** blade of your storage account, and your app.</span></span> <span data-ttu-id="98c94-187">In Hallo storage-account, wordt elke back-up bestaat uit een`.zip` -bestand met back-upgegevens Hallo en een `.xml` -bestand met een manifest Hallo `.zip` bestand inhoud.</span><span class="sxs-lookup"><span data-stu-id="98c94-187">In hello storage account, each backup consists of a`.zip` file that contains hello backup data and an `.xml` file that contains a manifest of hello `.zip` file contents.</span></span> <span data-ttu-id="98c94-188">U kunt uitpakken en deze bestanden bladeren als u wilt dat tooaccess uw back-ups zonder het daadwerkelijk uitvoeren van een toepassing herstellen.</span><span class="sxs-lookup"><span data-stu-id="98c94-188">You can unzip and browse these files if you want tooaccess your backups without actually performing an app restore.</span></span>

<span data-ttu-id="98c94-189">Hallo databaseback-up voor Hallo app wordt opgeslagen in de hoofdmap Hallo van the.zip-bestand.</span><span class="sxs-lookup"><span data-stu-id="98c94-189">hello database backup for hello app is stored in hello root of the.zip file.</span></span> <span data-ttu-id="98c94-190">Voor een SQL-database is een Bacpac-bestand (zonder extensie) en kunnen worden geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="98c94-190">For a SQL database, this is a BACPAC file (no file extension) and can be imported.</span></span> <span data-ttu-id="98c94-191">toocreate een SQL-database op basis van Hallo Bacpac-uitvoer, Zie [een tooCreate Bacpac-bestand een nieuwe gebruiker-Database importeren](http://technet.microsoft.com/library/hh710052.aspx).</span><span class="sxs-lookup"><span data-stu-id="98c94-191">toocreate a SQL database based on hello BACPAC export, see [Import a BACPAC File tooCreate a New User Database](http://technet.microsoft.com/library/hh710052.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="98c94-192">Wijzigen van Hallo-bestanden in uw **websitebackups** container kan leiden tot de back-toobecome Hallo ongeldig en worden daarom niet-terug te zetten.</span><span class="sxs-lookup"><span data-stu-id="98c94-192">Altering any of hello files in your **websitebackups** container can cause hello backup toobecome invalid and therefore non-restorable.</span></span>
> 
> 

<a name="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="98c94-193">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="98c94-193">Next Steps</span></span>
<span data-ttu-id="98c94-194">Zie voor informatie over het herstellen van een app van een back-up, [herstellen van een app in Azure](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="98c94-194">For information on restoring an app from a backup, see [Restore an app in Azure](web-sites-restore.md).</span></span> <span data-ttu-id="98c94-195">U kunt ook back-up en herstellen met behulp van REST-API-App Service-apps (Zie [gebruik REST toobackup en terugzetten van App Service-apps](websites-csm-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="98c94-195">You can also backup and restore App Service apps using REST API (see [Use REST toobackup and restore App Service apps](websites-csm-backup.md)).</span></span>


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

