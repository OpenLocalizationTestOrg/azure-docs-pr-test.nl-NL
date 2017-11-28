---
title: aaaRestore een app in Azure
description: Meer informatie over hoe toorestore uw app uit een back-up.
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 4444dbf7-363c-47e2-b24a-dbd45cb08491
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: 4b54029a9197064f990f29a3c4558c8322668714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-app-in-azure"></a><span data-ttu-id="31d7b-103">Een app in Azure herstellen</span><span class="sxs-lookup"><span data-stu-id="31d7b-103">Restore an app in Azure</span></span>
<span data-ttu-id="31d7b-104">Dit artikel ziet u hoe toorestore een app in [Azure App Service](../app-service/app-service-value-prop-what-is.md) die u hebt eerder back-up gemaakt (Zie [Back-up van uw app in Azure](web-sites-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="31d7b-104">This article shows you how toorestore an app in [Azure App Service](../app-service/app-service-value-prop-what-is.md) that you have previously backed up (see [Back up your app in Azure](web-sites-backup.md)).</span></span> <span data-ttu-id="31d7b-105">U kunt uw app met de gekoppelde databases op aanvraag tooa oorspronkelijke staat herstellen of een nieuwe app op basis van een back-up van uw oorspronkelijke app maken.</span><span class="sxs-lookup"><span data-stu-id="31d7b-105">You can restore your app with its linked databases on-demand tooa previous state, or create a new app based on one of your original app's backup.</span></span> <span data-ttu-id="31d7b-106">Azure App Service ondersteunt Hallo databases voor back-up en herstel na:</span><span class="sxs-lookup"><span data-stu-id="31d7b-106">Azure App Service supports hello following databases for backup and restore:</span></span>
- [<span data-ttu-id="31d7b-107">SQL Database</span><span class="sxs-lookup"><span data-stu-id="31d7b-107">SQL Database</span></span>](https://azure.microsoft.com/en-us/services/sql-database/)
- [<span data-ttu-id="31d7b-108">Azure-Database voor MySQL (Preview)</span><span class="sxs-lookup"><span data-stu-id="31d7b-108">Azure Database for MySQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/mysql)
- [<span data-ttu-id="31d7b-109">Azure-Database voor PostgreSQL (Preview)</span><span class="sxs-lookup"><span data-stu-id="31d7b-109">Azure Database for PostgreSQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/postgres)
- [<span data-ttu-id="31d7b-110">ClearDB MySQL</span><span class="sxs-lookup"><span data-stu-id="31d7b-110">ClearDB MySQL</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
- [<span data-ttu-id="31d7b-111">MySQL in-app</span><span class="sxs-lookup"><span data-stu-id="31d7b-111">MySQL in-app</span></span>](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)

<span data-ttu-id="31d7b-112">Herstellen vanuit back-ups is beschikbaar tooapps uitgevoerd in de **standaard** en **Premium** laag.</span><span class="sxs-lookup"><span data-stu-id="31d7b-112">Restoring from backups is available tooapps running in **Standard** and **Premium** tier.</span></span> <span data-ttu-id="31d7b-113">Zie voor meer informatie over het schalen van uw app [een app in Azure opschalen](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="31d7b-113">For information about scaling up your app, see [Scale up an app in Azure](web-sites-scale.md).</span></span> <span data-ttu-id="31d7b-114">**Premium** laag kan een groter aantal dagelijkse back-ups toobe uitgevoerd dan **standaard** laag.</span><span class="sxs-lookup"><span data-stu-id="31d7b-114">**Premium** tier allows a greater number of daily backups toobe performed than **Standard** tier.</span></span>

<a name="PreviousBackup"></a>

## <a name="restore-an-app-from-an-existing-backup"></a><span data-ttu-id="31d7b-115">Een app uit een bestaande back-up herstellen</span><span class="sxs-lookup"><span data-stu-id="31d7b-115">Restore an app from an existing backup</span></span>
1. <span data-ttu-id="31d7b-116">Op Hallo **instellingen** blade van uw app in hello Azure-Portal klikt u op **back-ups** toodisplay hello **back-ups** blade.</span><span class="sxs-lookup"><span data-stu-id="31d7b-116">On hello **Settings** blade of your app in hello Azure Portal, click **Backups** toodisplay hello **Backups** blade.</span></span> <span data-ttu-id="31d7b-117">Klik vervolgens op **herstellen**.</span><span class="sxs-lookup"><span data-stu-id="31d7b-117">Then click **Restore**.</span></span>
   
    ![Kies nu terugzetten][ChooseRestoreNow]
2. <span data-ttu-id="31d7b-119">In Hallo **herstellen** blade, eerste Selecteer Hallo back-gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="31d7b-119">In hello **Restore** blade, first select hello backup source.</span></span>
   
    ![](./media/web-sites-restore/021ChooseSource1.png)
   
    <span data-ttu-id="31d7b-120">Hallo **App back-up** optie ziet u alle bestaande back-ups van de huidige app Hallo Hallo en u deze eenvoudig kunt selecteren.</span><span class="sxs-lookup"><span data-stu-id="31d7b-120">hello **App backup** option shows you all hello existing backups of hello current app, and you can easily select one.</span></span>
    <span data-ttu-id="31d7b-121">Hallo **opslag** optie kunt u een back-ZIP-bestand van een bestaande Azure-opslagaccount en container in uw abonnement te selecteren.</span><span class="sxs-lookup"><span data-stu-id="31d7b-121">hello **Storage** option lets you select any backup ZIP file from any existing Azure Storage account and container in your subscription.</span></span>
    <span data-ttu-id="31d7b-122">Als u een back-up van een andere app toorestore probeert, gebruikt u Hallo **opslag** optie.</span><span class="sxs-lookup"><span data-stu-id="31d7b-122">If you're trying toorestore a backup of another app, use hello **Storage** option.</span></span>
3. <span data-ttu-id="31d7b-123">Geef vervolgens Hallo bestemming voor Hallo app terugzetten **terugzetdoel**.</span><span class="sxs-lookup"><span data-stu-id="31d7b-123">Then, specify hello destination for hello app restore in **Restore destination**.</span></span>
   
    ![](./media/web-sites-restore/022ChooseDestination1.png)
   
   > [!WARNING]
   > <span data-ttu-id="31d7b-124">Als u ervoor kiest **overschrijven**, worden alle bestaande gegevens in uw huidige app is gewist en overschreven.</span><span class="sxs-lookup"><span data-stu-id="31d7b-124">If you choose **Overwrite**, all existing data in your current app is erased and overwritten.</span></span> <span data-ttu-id="31d7b-125">Voordat u op **OK**, zorg ervoor dat deze precies naar wens toodo.</span><span class="sxs-lookup"><span data-stu-id="31d7b-125">Before you click **OK**, make sure that it is exactly what you want toodo.</span></span>
   > 
   > 
   
    <span data-ttu-id="31d7b-126">U kunt selecteren **bestaande App** toorestore Hallo app back-tooanother-app in Hallo dezelfde resoure-groep.</span><span class="sxs-lookup"><span data-stu-id="31d7b-126">You can select **Existing App** toorestore hello app backup tooanother app in hello same resoure group.</span></span> <span data-ttu-id="31d7b-127">Voordat u deze optie gebruikt, moet u al hebt gemaakt een andere app in de resourcegroep met het spiegelen van de database configuration toohello gedefinieerd in de back-up Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="31d7b-127">Before you use this option, you should have already created another app in your resource group with mirroring database configuration toohello one defined in hello app backup.</span></span> <span data-ttu-id="31d7b-128">U kunt ook maken een **nieuw** app toorestore de inhoud op.</span><span class="sxs-lookup"><span data-stu-id="31d7b-128">You can also Create a **New** app toorestore your content to.</span></span>

4. <span data-ttu-id="31d7b-129">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="31d7b-129">Click **OK**.</span></span>

<a name="StorageAccount"></a>

## <a name="download-or-delete-a-backup-from-a-storage-account"></a><span data-ttu-id="31d7b-130">Downloaden of een back-up van een opslagaccount verwijderen</span><span class="sxs-lookup"><span data-stu-id="31d7b-130">Download or delete a backup from a storage account</span></span>
1. <span data-ttu-id="31d7b-131">Van de belangrijkste Hallo **Bladeren** blade van Azure portal, selecteer Hallo **opslagaccounts**.</span><span class="sxs-lookup"><span data-stu-id="31d7b-131">From hello main **Browse** blade of hello Azure portal, select **Storage accounts**.</span></span> <span data-ttu-id="31d7b-132">Er wordt een lijst met uw bestaande opslagaccounts weergegeven.</span><span class="sxs-lookup"><span data-stu-id="31d7b-132">A list of your existing storage accounts is displayed.</span></span>
2. <span data-ttu-id="31d7b-133">Selecteer Hallo storage-account met Hallo back-up die u wilt toodownload of delete.hello blade voor Hallo storage-account wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="31d7b-133">Select hello storage account that contains hello backup that you want toodownload or delete.hello blade for hello storage account is displayed.</span></span>
3. <span data-ttu-id="31d7b-134">Selecteer in de blade opslagaccount Hallo Hallo-container die u wilt</span><span class="sxs-lookup"><span data-stu-id="31d7b-134">In hello storage account blade, select hello container you want</span></span>
   
    ![Weergavecontainers][ViewContainers]
4. <span data-ttu-id="31d7b-136">Selecteer de back-upbestand of wilt u toodownload verwijderen.</span><span class="sxs-lookup"><span data-stu-id="31d7b-136">Select backup file you want toodownload or delete.</span></span>
   
    ![ViewContainers](./media/web-sites-restore/03ViewFiles.png)
5. <span data-ttu-id="31d7b-138">Klik op **downloaden** of **verwijderen** afhankelijk van wat u wilt dat toodo.</span><span class="sxs-lookup"><span data-stu-id="31d7b-138">Click **Download** or **Delete** depending on what you want toodo.</span></span>  

<a name="OperationLogs"></a>

## <a name="monitor-a-restore-operation"></a><span data-ttu-id="31d7b-139">Een herstelbewerking bewaken</span><span class="sxs-lookup"><span data-stu-id="31d7b-139">Monitor a restore operation</span></span>
<span data-ttu-id="31d7b-140">toosee details over Hallo slagen of mislukken van Hallo app restore-bewerking, navigeer toohello **activiteitenlogboek** blade in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="31d7b-140">toosee details about hello success or failure of hello app restore operation, navigate toohello **Activity Log** blade in hello Azure portal.</span></span>  
 

<span data-ttu-id="31d7b-141">Schuif naar beneden toofind Hallo gewenst restore opnieuw en klik op tooselect deze.</span><span class="sxs-lookup"><span data-stu-id="31d7b-141">Scroll down toofind hello desired restore operation and click tooselect it.</span></span>

<span data-ttu-id="31d7b-142">Hallo details blade geeft Hallo beschikbare informatie gerelateerd toohello restore-bewerking.</span><span class="sxs-lookup"><span data-stu-id="31d7b-142">hello details blade displays hello available information related toohello restore operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="31d7b-143">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="31d7b-143">Next Steps</span></span>
<span data-ttu-id="31d7b-144">U kunt back-up en herstellen met behulp van REST-API-App Service-apps (Zie [gebruik REST tooback ups en het terugzetten van App Service-apps](websites-csm-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="31d7b-144">You can backup and restore App Service apps using REST API (see [Use REST tooback up and restore App Service apps](websites-csm-backup.md)).</span></span>


<!-- IMAGES -->
[ChooseRestoreNow]: ./media/web-sites-restore/02ChooseRestoreNow1.png
[ViewContainers]: ./media/web-sites-restore/03ViewContainers.png
[StorageAccountFile]: ./media/web-sites-restore/02StorageAccountFile.png
[BrowseCloudStorage]: ./media/web-sites-restore/03BrowseCloudStorage.png
[StorageAccountFileSelected]: ./media/web-sites-restore/04StorageAccountFileSelected.png
[ChooseRestoreSettings]: ./media/web-sites-restore/05ChooseRestoreSettings.png
[ChooseDBServer]: ./media/web-sites-restore/06ChooseDBServer.png
[RestoreToNewSQLDB]: ./media/web-sites-restore/07RestoreToNewSQLDB.png
[NewSQLDBConfig]: ./media/web-sites-restore/08NewSQLDBConfig.png
[RestoredContosoWebSite]: ./media/web-sites-restore/09RestoredContosoWebSite.png
[DashboardOperationLogsLink]: ./media/web-sites-restore/10DashboardOperationLogsLink.png
[ManagementServicesOperationLogsList]: ./media/web-sites-restore/11ManagementServicesOperationLogsList.png
[DetailsButton]: ./media/web-sites-restore/12DetailsButton.png
[OperationDetails]: ./media/web-sites-restore/13OperationDetails.png
