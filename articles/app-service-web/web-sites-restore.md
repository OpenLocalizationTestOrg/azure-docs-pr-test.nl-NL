---
title: Een app in Azure herstellen
description: Informatie over het herstellen van uw app vanaf een back-up.
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
ms.openlocfilehash: 5fe74d992edb7028fa4a2500e427013d98ebc250
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="restore-an-app-in-azure"></a><span data-ttu-id="239b8-103">Een app in Azure herstellen</span><span class="sxs-lookup"><span data-stu-id="239b8-103">Restore an app in Azure</span></span>
<span data-ttu-id="239b8-104">Dit artikel laat zien hoe u een app in [Azure App Service](../app-service/app-service-value-prop-what-is.md) die u hebt eerder back-up gemaakt (Zie [Back-up van uw app in Azure](web-sites-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="239b8-104">This article shows you how to restore an app in [Azure App Service](../app-service/app-service-value-prop-what-is.md) that you have previously backed up (see [Back up your app in Azure](web-sites-backup.md)).</span></span> <span data-ttu-id="239b8-105">U kunt uw app met de gekoppelde databases op aanvraag naar een eerdere status herstellen of een nieuwe app op basis van een back-up van uw oorspronkelijke app maken.</span><span class="sxs-lookup"><span data-stu-id="239b8-105">You can restore your app with its linked databases on-demand to a previous state, or create a new app based on one of your original app's backup.</span></span> <span data-ttu-id="239b8-106">Azure App Service ondersteunt de volgende databases voor back-up en herstel:</span><span class="sxs-lookup"><span data-stu-id="239b8-106">Azure App Service supports the following databases for backup and restore:</span></span>
- [<span data-ttu-id="239b8-107">SQL Database</span><span class="sxs-lookup"><span data-stu-id="239b8-107">SQL Database</span></span>](https://azure.microsoft.com/en-us/services/sql-database/)
- [<span data-ttu-id="239b8-108">Azure-Database voor MySQL (Preview)</span><span class="sxs-lookup"><span data-stu-id="239b8-108">Azure Database for MySQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/mysql)
- [<span data-ttu-id="239b8-109">Azure-Database voor PostgreSQL (Preview)</span><span class="sxs-lookup"><span data-stu-id="239b8-109">Azure Database for PostgreSQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/postgres)
- [<span data-ttu-id="239b8-110">ClearDB MySQL</span><span class="sxs-lookup"><span data-stu-id="239b8-110">ClearDB MySQL</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
- [<span data-ttu-id="239b8-111">MySQL in-app</span><span class="sxs-lookup"><span data-stu-id="239b8-111">MySQL in-app</span></span>](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)

<span data-ttu-id="239b8-112">Herstellen vanuit back-ups is beschikbaar voor apps die worden uitgevoerd **standaard** en **Premium** laag.</span><span class="sxs-lookup"><span data-stu-id="239b8-112">Restoring from backups is available to apps running in **Standard** and **Premium** tier.</span></span> <span data-ttu-id="239b8-113">Zie voor meer informatie over het schalen van uw app [een app in Azure opschalen](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="239b8-113">For information about scaling up your app, see [Scale up an app in Azure](web-sites-scale.md).</span></span> <span data-ttu-id="239b8-114">**Premium** laag kan een groter aantal dagelijkse back-ups worden uitgevoerd dan **standaard** laag.</span><span class="sxs-lookup"><span data-stu-id="239b8-114">**Premium** tier allows a greater number of daily backups to be performed than **Standard** tier.</span></span>

<a name="PreviousBackup"></a>

## <a name="restore-an-app-from-an-existing-backup"></a><span data-ttu-id="239b8-115">Een app uit een bestaande back-up herstellen</span><span class="sxs-lookup"><span data-stu-id="239b8-115">Restore an app from an existing backup</span></span>
1. <span data-ttu-id="239b8-116">Op de **instellingen** blade van uw app in de Azure-Portal klikt u op **back-ups** om weer te geven de **back-ups** blade.</span><span class="sxs-lookup"><span data-stu-id="239b8-116">On the **Settings** blade of your app in the Azure Portal, click **Backups** to display the **Backups** blade.</span></span> <span data-ttu-id="239b8-117">Klik vervolgens op **herstellen**.</span><span class="sxs-lookup"><span data-stu-id="239b8-117">Then click **Restore**.</span></span>
   
    ![Kies nu terugzetten][ChooseRestoreNow]
2. <span data-ttu-id="239b8-119">In de **herstellen** blade, selecteert u eerst de back-bron.</span><span class="sxs-lookup"><span data-stu-id="239b8-119">In the **Restore** blade, first select the backup source.</span></span>
   
    ![](./media/web-sites-restore/021ChooseSource1.png)
   
    <span data-ttu-id="239b8-120">De **App back-up** optie ziet u alle de bestaande back-ups van de huidige app en u deze eenvoudig kunt selecteren.</span><span class="sxs-lookup"><span data-stu-id="239b8-120">The **App backup** option shows you all the existing backups of the current app, and you can easily select one.</span></span>
    <span data-ttu-id="239b8-121">De **opslag** optie kunt u een back-ZIP-bestand van een bestaande Azure-opslagaccount en container in uw abonnement te selecteren.</span><span class="sxs-lookup"><span data-stu-id="239b8-121">The **Storage** option lets you select any backup ZIP file from any existing Azure Storage account and container in your subscription.</span></span>
    <span data-ttu-id="239b8-122">Als u probeert te herstellen van een back-up van een andere app, gebruikt u de **opslag** optie.</span><span class="sxs-lookup"><span data-stu-id="239b8-122">If you're trying to restore a backup of another app, use the **Storage** option.</span></span>
3. <span data-ttu-id="239b8-123">Geef het doel voor het herstellen van de app in **terugzetdoel**.</span><span class="sxs-lookup"><span data-stu-id="239b8-123">Then, specify the destination for the app restore in **Restore destination**.</span></span>
   
    ![](./media/web-sites-restore/022ChooseDestination1.png)
   
   > [!WARNING]
   > <span data-ttu-id="239b8-124">Als u ervoor kiest **overschrijven**, worden alle bestaande gegevens in uw huidige app is gewist en overschreven.</span><span class="sxs-lookup"><span data-stu-id="239b8-124">If you choose **Overwrite**, all existing data in your current app is erased and overwritten.</span></span> <span data-ttu-id="239b8-125">Voordat u op **OK**, zorg ervoor dat deze precies wat u wilt doen.</span><span class="sxs-lookup"><span data-stu-id="239b8-125">Before you click **OK**, make sure that it is exactly what you want to do.</span></span>
   > 
   > 
   
    <span data-ttu-id="239b8-126">U kunt selecteren **bestaande App** om te zetten back-up van de app op een andere app in dezelfde groep resoure.</span><span class="sxs-lookup"><span data-stu-id="239b8-126">You can select **Existing App** to restore the app backup to another app in the same resoure group.</span></span> <span data-ttu-id="239b8-127">Voordat u deze optie gebruikt, moet hebt u al een andere app gemaakt in de resourcegroep met de databaseconfiguratie naar een gedefinieerd in de app back-up voor het spiegelen.</span><span class="sxs-lookup"><span data-stu-id="239b8-127">Before you use this option, you should have already created another app in your resource group with mirroring database configuration to the one defined in the app backup.</span></span> <span data-ttu-id="239b8-128">U kunt ook maken een **nieuw** app uw inhoud te herstellen.</span><span class="sxs-lookup"><span data-stu-id="239b8-128">You can also Create a **New** app to restore your content to.</span></span>

4. <span data-ttu-id="239b8-129">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="239b8-129">Click **OK**.</span></span>

<a name="StorageAccount"></a>

## <a name="download-or-delete-a-backup-from-a-storage-account"></a><span data-ttu-id="239b8-130">Downloaden of een back-up van een opslagaccount verwijderen</span><span class="sxs-lookup"><span data-stu-id="239b8-130">Download or delete a backup from a storage account</span></span>
1. <span data-ttu-id="239b8-131">Vanuit het hoofdvenster **Bladeren** blade van de Azure portal, selecteer **opslagaccounts**.</span><span class="sxs-lookup"><span data-stu-id="239b8-131">From the main **Browse** blade of the Azure portal, select **Storage accounts**.</span></span> <span data-ttu-id="239b8-132">Er wordt een lijst met uw bestaande opslagaccounts weergegeven.</span><span class="sxs-lookup"><span data-stu-id="239b8-132">A list of your existing storage accounts is displayed.</span></span>
2. <span data-ttu-id="239b8-133">Selecteer het opslagaccount waarin de back-up die u wilt downloaden of verwijderen. De blade voor het opslagaccount wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="239b8-133">Select the storage account that contains the backup that you want to download or delete.The blade for the storage account is displayed.</span></span>
3. <span data-ttu-id="239b8-134">Selecteer de container die u wilt dat in de blade opslagaccount</span><span class="sxs-lookup"><span data-stu-id="239b8-134">In the storage account blade, select the container you want</span></span>
   
    ![Weergavecontainers][ViewContainers]
4. <span data-ttu-id="239b8-136">Selecteer de back-upbestand dat u wilt downloaden of verwijderen.</span><span class="sxs-lookup"><span data-stu-id="239b8-136">Select backup file you want to download or delete.</span></span>
   
    ![ViewContainers](./media/web-sites-restore/03ViewFiles.png)
5. <span data-ttu-id="239b8-138">Klik op **downloaden** of **verwijderen** afhankelijk van wat u wilt doen.</span><span class="sxs-lookup"><span data-stu-id="239b8-138">Click **Download** or **Delete** depending on what you want to do.</span></span>  

<a name="OperationLogs"></a>

## <a name="monitor-a-restore-operation"></a><span data-ttu-id="239b8-139">Een herstelbewerking bewaken</span><span class="sxs-lookup"><span data-stu-id="239b8-139">Monitor a restore operation</span></span>
<span data-ttu-id="239b8-140">Voor informatie over het slagen of mislukken van de app-herstelbewerking, gaat u naar de **activiteitenlogboek** blade in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="239b8-140">To see details about the success or failure of the app restore operation, navigate to the **Activity Log** blade in the Azure portal.</span></span>  
 

<span data-ttu-id="239b8-141">Schuif naar beneden om te zoeken naar de gewenste herstelbewerking en klikt u op om deze te selecteren.</span><span class="sxs-lookup"><span data-stu-id="239b8-141">Scroll down to find the desired restore operation and click to select it.</span></span>

<span data-ttu-id="239b8-142">De blade toewijzingdetails geeft de beschikbare informatie met betrekking tot de herstelbewerking opnieuw.</span><span class="sxs-lookup"><span data-stu-id="239b8-142">The details blade displays the available information related to the restore operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="239b8-143">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="239b8-143">Next Steps</span></span>
<span data-ttu-id="239b8-144">U kunt back-up en herstellen met behulp van REST-API-App Service-apps (Zie [gebruik REST back-up en herstellen van App Service-apps](websites-csm-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="239b8-144">You can backup and restore App Service apps using REST API (see [Use REST to back up and restore App Service apps](websites-csm-backup.md)).</span></span>


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
