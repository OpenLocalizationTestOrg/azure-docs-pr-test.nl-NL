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
# <a name="back-up-your-app-in-azure"></a>Back-up maken van uw app in Azure
Hallo Back-up en herstellen van de functie in [Azure App Service](../app-service/app-service-value-prop-what-is.md) kunt u eenvoudig back-ups van app handmatig of volgens een planning aan te maken. U kunt Hallo app tooa momentopname van een eerdere status door overschrijven Hallo bestaande app of terugzetten tooanother app herstellen. 

Zie voor informatie over het herstellen van een app van back-up, [herstellen van een app in Azure](web-sites-restore.md).

<a name="whatsbackedup"></a>

## <a name="what-gets-backed-up"></a>Wat wordt een back-up
App Service kunt back-up Hallo volgende informatie tooan Azure-opslagaccount en container dat u uw app toouse hebt geconfigureerd. 

* App-configuratie
* Bestandsinhoud
* Database verbonden tooyour app

Hallo database-oplossingen te volgen worden met de functie back-ups ondersteund: 
   - [SQL Database](https://azure.microsoft.com/en-us/services/sql-database/)
   - [Azure-Database voor MySQL (Preview)](https://azure.microsoft.com/en-us/services/mysql)
   - [Azure-Database voor PostgreSQL (Preview)](https://azure.microsoft.com/en-us/services/postgres)
   - [ClearDB MySQL](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
   - [MySQL in-app](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)
 

> [!NOTE]
>  Elke back-up is een volledige offline kopie van uw app, niet een incrementele update.
>  

<a name="requirements"></a>

## <a name="requirements-and-restrictions"></a>Vereisten en beperkingen
* Hallo Back-up en terugzetten functie vereist Hallo App Service plan toobe in Hallo **standaard** laag of **Premium** laag. Zie voor meer informatie over het schalen van uw App Service plan toouse een hogere laag [een app in Azure opschalen](web-sites-scale.md).  
  **Premium** laag kan een groter aantal dagelijks back-ups dan **standaard** laag.
* U moet een Azure-opslagaccount en container in Hallo hetzelfde abonnement als Hallo-app die u toobackup wilt. Zie voor meer informatie over Azure storage-accounts Hallo [koppelingen](#moreaboutstorage) aan Hallo einde van dit artikel.
* Back-ups kunnen van de app en database inhoud too10 GB zijn. Als het Hallo-back-upgrootte overschrijdt deze limiet, krijgt u een fout opgetreden.

<a name="manualbackup"></a>

## <a name="create-a-manual-backup"></a>Een handmatige back-up maken
1. In Hallo [Azure Portal](https://portal.azure.com), navigeer blade tooyour-app, selecteer **back-ups**. Hallo **back-ups** blade wordt weergegeven.
   
    ![Back-ups pagina][ChooseBackupsPage]
   
   > [!NOTE]
   > Als u het Hallo-bericht hieronder ziet, klikt u erop tooupgrade uw App Service-abonnement voordat u verder kunt gaan met back-ups.
   > Zie [een app in Azure opschalen](web-sites-scale.md) voor meer informatie.  
   > ![Opslagaccount kiezen](./media/web-sites-backup/01UpgradePlan1.png)
   > 
   > 

2. In Hallo **back-up** blade, klikt u op **configureren**
![klikt u op configureren](./media/web-sites-backup/ClickConfigure1.png)
3. In Hallo **back-upconfiguratie** blade, klikt u op **opslag: niet geconfigureerd** tooconfigure een opslagaccount.
   
    ![Opslagaccount kiezen][ChooseStorageAccount]
4. Kies uw back-upbestemming door te selecteren een **Opslagaccount** en **Container**. Hallo storage-account moet behoren toohello hetzelfde abonnement als u wilt dat tooback up Hallo-app. Als u wenst, kunt u een nieuw opslagaccount of een nieuwe container in Hallo respectievelijke blades. Wanneer u bent klaar, klikt u op **Selecteer**.
   
    ![Opslagaccount kiezen](./media/web-sites-backup/02ChooseStorageAccount1-1.png)
5. In Hallo **back-upconfiguratie** blade die nog steeds open blijft, kunt u configureren **Backup Database**, selecteer vervolgens Hallo databases u wilt dat tooinclude in Hallo back-ups (SQL-database of MySQL) en klik vervolgens op **OK**.  
   
    ![Opslagaccount kiezen](./media/web-sites-backup/03ConfigureDatabase1.png)
   
   > [!NOTE]
   > Voor een database tooappear in deze lijst, de verbindingsreeks moet aanwezig zijn in Hallo **verbindingsreeksen** sectie Hallo **toepassingsinstellingen** blade voor uw app.
   > 
   > 
6. In Hallo **back-upconfiguratie** blade, klikt u op **opslaan**.    
7. In Hallo **back-ups** blade, klikt u op **back-up**.
   
    ![Knop BackUpNow][BackUpNow]
   
    U ziet een bericht uitgevoerd tijdens de back-upproces Hallo.

Zodra het Hallo-opslagaccount en container is geconfigureerd kunt u een handmatige back-up op elk gewenst moment kunt starten.  

<a name="automatedbackups"></a>

## <a name="configure-automated-backups"></a>Automatische back-ups configureren
1. In Hallo **back-upconfiguratie** blade ingesteld **geplande back-up** te**op**. 
   
    ![Opslagaccount kiezen](./media/web-sites-backup/05ScheduleBackup1.png)
2. Back-upschema opties wordt weergegeven, stel **geplande back-** te**op**, configureer de gewenste Hallo back-upschema en klikt u op **OK**.
   
    ![Automatische back-ups inschakelen][SetAutomatedBackupOn]

<a name="partialbackups"></a>

## <a name="configure-partial-backups"></a>Gedeeltelijke back-ups configureren
Soms wilt u niet toobackup alles in uw app. Enkele voorbeelden:

* U [wekelijkse back-ups instellen](web-sites-backup.md#configure-automated-backups) van uw app met statische inhoud, die nooit wordt gewijzigd, zoals oude blogberichten of installatiekopieën.
* Uw app heeft meer dan 10 GB aan inhoud (dat wil zeggen Hallo max bedrag die kunt u de back-up op een tijdstip).
* U wilt niet dat toobackup Hallo-logboekbestanden.

Gedeeltelijke back-ups kunt u kiezen exact bestanden die u wilt dat toobackup.

### <a name="exclude-files-from-your-backup"></a>Bestanden uitsluiten van uw back-up
Stel dat u hebt een app met logboekbestanden en statische afbeeldingen die zijn back-up eenmaal en toochange niet gaat. In dergelijke gevallen kunt u de mappen en bestanden uitsluiten van wordt opgeslagen in uw toekomstige back-ups. tooexclude bestanden en mappen van uw back-ups maken van een `_backup.filter` bestand in Hallo `D:\home\site\wwwroot` map van uw app. Hallo-lijst van bestanden en mappen die u wilt dat tooexclude in dit bestand opgeven. 

Een eenvoudige manier tooaccess uw bestanden toouse Kudu is. Klik op **geavanceerde hulpprogramma's -> Ga** instellen voor uw web-app tooaccess Kudu.

![Kudu met portal][kudu-portal]

Hallo-mappen die u tooexclude vanuit uw back-ups wilt identificeren.  U wilt bijvoorbeeld toofilter Hallo gemarkeerde map en bestanden.

![Map installatiekopieën][ImagesFolder]

Maken van een bestand met de naam `_backup.filter` en Hallo bovenstaande lijst plaatsen in Hallo-bestand, maar Verwijder `D:\home`. Lijst van een directory of bestand per regel. Dus moet Hallo inhoud van het Hallo-bestand:
 ```bash
    \site\wwwroot\Images\brand.png
    \site\wwwroot\Images\2014
    \site\wwwroot\Images\2013
```

Uploaden `_backup.filter` bestand toohello `D:\home\site\wwwroot\` map van uw site met [ftp](web-sites-deploy.md#ftp) of een andere methode. Als u wenst, kunt u Hallo-bestand rechtstreeks met Kudu `DebugConsole` en voeg de er Hallo-inhoud.

Voer back-ups Hallo dezelfde manier zou u dat gewend bent, [handmatig](#create-a-manual-backup) of [automatisch](#configure-automated-backups). Nu, worden bestanden en mappen die zijn opgegeven in `_backup.filter` is uitgesloten van Hallo toekomstige back-ups gepland of handmatig is gestart. 

> [!NOTE]
> Herstellen van gedeeltelijke back-ups van uw site Hallo dezelfde manier als [een regelmatige back-up terugzetten](web-sites-restore.md). het herstelproces Hallo wat u Hallo.
> 
> Wanneer een volledige back-up wordt hersteld, wordt alle inhoud op Hallo site vervangen met de Hallo back-up. Als een bestand op Hallo-site, maar niet in de back-up hello wordt deze verwijderd. Maar wanneer een gedeeltelijke back-up wordt hersteld, inhoud die zich in een van de mappen gebeurd hello of een zwarte lijst bestand, is ongewijzigd.
> 


<a name="aboutbackups"></a>

## <a name="how-backups-are-stored"></a>Hoe de back-ups worden opgeslagen
Nadat u een of meer back-ups voor uw app gemaakt hebt, Hallo back-ups zijn zichtbaar op Hallo **Containers** blade van uw opslagaccount en uw app. In Hallo storage-account, wordt elke back-up bestaat uit een`.zip` -bestand met back-upgegevens Hallo en een `.xml` -bestand met een manifest Hallo `.zip` bestand inhoud. U kunt uitpakken en deze bestanden bladeren als u wilt dat tooaccess uw back-ups zonder het daadwerkelijk uitvoeren van een toepassing herstellen.

Hallo databaseback-up voor Hallo app wordt opgeslagen in de hoofdmap Hallo van the.zip-bestand. Voor een SQL-database is een Bacpac-bestand (zonder extensie) en kunnen worden geïmporteerd. toocreate een SQL-database op basis van Hallo Bacpac-uitvoer, Zie [een tooCreate Bacpac-bestand een nieuwe gebruiker-Database importeren](http://technet.microsoft.com/library/hh710052.aspx).

> [!WARNING]
> Wijzigen van Hallo-bestanden in uw **websitebackups** container kan leiden tot de back-toobecome Hallo ongeldig en worden daarom niet-terug te zetten.
> 
> 

<a name="nextsteps"></a>

## <a name="next-steps"></a>Volgende stappen
Zie voor informatie over het herstellen van een app van een back-up, [herstellen van een app in Azure](web-sites-restore.md). U kunt ook back-up en herstellen met behulp van REST-API-App Service-apps (Zie [gebruik REST toobackup en terugzetten van App Service-apps](websites-csm-backup.md)).


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

