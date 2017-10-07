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
# <a name="restore-an-app-in-azure"></a>Een app in Azure herstellen
Dit artikel ziet u hoe toorestore een app in [Azure App Service](../app-service/app-service-value-prop-what-is.md) die u hebt eerder back-up gemaakt (Zie [Back-up van uw app in Azure](web-sites-backup.md)). U kunt uw app met de gekoppelde databases op aanvraag tooa oorspronkelijke staat herstellen of een nieuwe app op basis van een back-up van uw oorspronkelijke app maken. Azure App Service ondersteunt Hallo databases voor back-up en herstel na:
- [SQL Database](https://azure.microsoft.com/en-us/services/sql-database/)
- [Azure-Database voor MySQL (Preview)](https://azure.microsoft.com/en-us/services/mysql)
- [Azure-Database voor PostgreSQL (Preview)](https://azure.microsoft.com/en-us/services/postgres)
- [ClearDB MySQL](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
- [MySQL in-app](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)

Herstellen vanuit back-ups is beschikbaar tooapps uitgevoerd in de **standaard** en **Premium** laag. Zie voor meer informatie over het schalen van uw app [een app in Azure opschalen](web-sites-scale.md). **Premium** laag kan een groter aantal dagelijkse back-ups toobe uitgevoerd dan **standaard** laag.

<a name="PreviousBackup"></a>

## <a name="restore-an-app-from-an-existing-backup"></a>Een app uit een bestaande back-up herstellen
1. Op Hallo **instellingen** blade van uw app in hello Azure-Portal klikt u op **back-ups** toodisplay hello **back-ups** blade. Klik vervolgens op **herstellen**.
   
    ![Kies nu terugzetten][ChooseRestoreNow]
2. In Hallo **herstellen** blade, eerste Selecteer Hallo back-gegevensbron.
   
    ![](./media/web-sites-restore/021ChooseSource1.png)
   
    Hallo **App back-up** optie ziet u alle bestaande back-ups van de huidige app Hallo Hallo en u deze eenvoudig kunt selecteren.
    Hallo **opslag** optie kunt u een back-ZIP-bestand van een bestaande Azure-opslagaccount en container in uw abonnement te selecteren.
    Als u een back-up van een andere app toorestore probeert, gebruikt u Hallo **opslag** optie.
3. Geef vervolgens Hallo bestemming voor Hallo app terugzetten **terugzetdoel**.
   
    ![](./media/web-sites-restore/022ChooseDestination1.png)
   
   > [!WARNING]
   > Als u ervoor kiest **overschrijven**, worden alle bestaande gegevens in uw huidige app is gewist en overschreven. Voordat u op **OK**, zorg ervoor dat deze precies naar wens toodo.
   > 
   > 
   
    U kunt selecteren **bestaande App** toorestore Hallo app back-tooanother-app in Hallo dezelfde resoure-groep. Voordat u deze optie gebruikt, moet u al hebt gemaakt een andere app in de resourcegroep met het spiegelen van de database configuration toohello gedefinieerd in de back-up Hallo-app. U kunt ook maken een **nieuw** app toorestore de inhoud op.

4. Klik op **OK**.

<a name="StorageAccount"></a>

## <a name="download-or-delete-a-backup-from-a-storage-account"></a>Downloaden of een back-up van een opslagaccount verwijderen
1. Van de belangrijkste Hallo **Bladeren** blade van Azure portal, selecteer Hallo **opslagaccounts**. Er wordt een lijst met uw bestaande opslagaccounts weergegeven.
2. Selecteer Hallo storage-account met Hallo back-up die u wilt toodownload of delete.hello blade voor Hallo storage-account wordt weergegeven.
3. Selecteer in de blade opslagaccount Hallo Hallo-container die u wilt
   
    ![Weergavecontainers][ViewContainers]
4. Selecteer de back-upbestand of wilt u toodownload verwijderen.
   
    ![ViewContainers](./media/web-sites-restore/03ViewFiles.png)
5. Klik op **downloaden** of **verwijderen** afhankelijk van wat u wilt dat toodo.  

<a name="OperationLogs"></a>

## <a name="monitor-a-restore-operation"></a>Een herstelbewerking bewaken
toosee details over Hallo slagen of mislukken van Hallo app restore-bewerking, navigeer toohello **activiteitenlogboek** blade in hello Azure-portal.  
 

Schuif naar beneden toofind Hallo gewenst restore opnieuw en klik op tooselect deze.

Hallo details blade geeft Hallo beschikbare informatie gerelateerd toohello restore-bewerking.

## <a name="next-steps"></a>Volgende stappen
U kunt back-up en herstellen met behulp van REST-API-App Service-apps (Zie [gebruik REST tooback ups en het terugzetten van App Service-apps](websites-csm-backup.md)).


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
