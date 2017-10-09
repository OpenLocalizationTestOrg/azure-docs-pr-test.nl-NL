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
# <a name="backup-and-restore"></a>Back-ups en herstellen

Back-ups van databases in Azure Analysis Services model in tabelvorm is grotendeels hetzelfde als voor on-premises Analysis-Services Hallo. het belangrijkste verschil Hallo is waar u uw back-upbestanden opslaat. Back-upbestanden moeten worden opgeslagen op de container tooa in een [Azure storage-account](../storage/common/storage-create-storage-account.md). Kunt u een opslagaccount en container die u al hebt, of ze kunnen worden gemaakt bij het configureren van instellingen voor de opslag voor uw server.

> [!NOTE]
> Maken van een opslagaccount kan resulteren in een nieuwe factureerbare service. toolearn meer, Zie [prijzen voor Azure Storage](https://azure.microsoft.com/pricing/details/storage/blobs/).
> 
> 

Back-ups worden opgeslagen met de extensie abf. Voor in het geheugen modellen in tabelvorm, worden zowel modelgegevens en metagegevens opgeslagen. Voor de DirectQuery-modellen in tabelvorm, is alleen de metagegevens van het model opgeslagen. Back-ups worden gecomprimeerd en versleuteld, afhankelijk van het Hallo-opties die u kiest. 



## <a name="configure-storage-settings"></a>Instellingen voor de opslag configureren
Voordat u een back-up, moet u instellingen voor de opslag tooconfigure voor uw server.


### <a name="tooconfigure-storage-settings"></a>instellingen voor de opslag tooconfigure
1.  In Azure portal > **instellingen**, klikt u op **back-up**.

    ![Back-ups in instellingen](./media/analysis-services-backup/aas-backup-backups.png)

2.  Klik op **ingeschakeld**, klikt u vervolgens op **Opslaginstellingen**.

    ![Inschakelen](./media/analysis-services-backup/aas-backup-enable.png)

3. Selecteer uw storage-account of maak een nieuwe.

4. Selecteer een container of maak een nieuwe.

    ![Container selecteren](./media/analysis-services-backup/aas-backup-container.png)

5. De back-instellingen opslaan.

    ![Back-instellingen opslaan](./media/analysis-services-backup/aas-backup-save.png)

## <a name="backup"></a>Back-up

### <a name="toobackup-by-using-ssms"></a>toobackup met behulp van SSMS

1. SSMS, met de rechtermuisknop op een database > **Back-Up**.

2. In **Backup Database** > **back-upbestand**, klikt u op **Bladeren**.

3. In Hallo **bestand opslaan als** dialoogvenster Hallo mappad controleren en typ een naam voor de back-upbestand Hallo. 

4. In Hallo **Backup Database** dialoogvenster, opties selecteren.

    **Toestaan dat bestand overschreven** -Selecteer deze optie toooverwrite back-upbestanden Hallo dezelfde naam. Als deze optie niet is ingeschakeld, kan niet Hallo bestand dat u wilt opslaan Hallo dezelfde naam als een bestand dat al in Hallo dezelfde voorkomt hebben locatie.

    **Compressie toepassen** -Selecteer deze optie toocompress Hallo back-upbestand. Gecomprimeerde back-upbestanden besparen op schijfruimte, maar moeten een enigszins hogere CPU-gebruik. 

    **Versleutelen van back-upbestand** -Selecteer deze optie tooencrypt Hallo back-upbestand. Deze optie vereist een back-upbestand van de gebruiker opgegeven wachtwoord toosecure Hallo. Hallo wachtwoord kan niet worden gelezen van de back-upgegevens Hallo enigerlei andere wijze dan een herstelbewerking. Als u back-ups tooencrypt kiest, moet u Hallo wachtwoord opslaan op een veilige locatie.

5. Klik op **OK** toocreate en Hallo back-upbestand opslaan.


### <a name="powershell"></a>PowerShell
Gebruik [back-up ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet) cmdlet.

## <a name="restore"></a>Herstellen
Bij het herstellen, moet het back-upbestand in Hallo storage-account die u hebt geconfigureerd voor uw server. Als u toomove een back-upbestand van een lokale locatie tooyour storage-account nodig hebt, gebruikt u [Microsoft Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) of Hallo [AzCopy](../storage/common/storage-use-azcopy.md) opdrachtregelprogramma. 



> [!NOTE]
> Als u vanuit een on-premises server terugzetten wilt, moet u alle Hallo domeingebruikers verwijderen uit de rollen van Hallo model en toe te voegen back-toohello rollen als Azure Active Directory-gebruikers.
> 
> 

### <a name="toorestore-by-using-ssms"></a>toorestore met behulp van SSMS

1. SSMS, met de rechtermuisknop op een database > **herstellen**.

2. In Hallo **Backup Database** dialoogvenster in **back-upbestand**, klikt u op **Bladeren**.

3. In Hallo **databasebestanden vinden** dialoogvenster, selecteer Hallo bestand dat u wenst toorestore.

4. In **Restore database**, selecteer Hallo-database.

5. Geef opties op. Beveiligingsopties moeten overeenkomen met de back-upopties Hallo die tijdens een back-up hebt gebruikt.


### <a name="powershell"></a>PowerShell

Gebruik [terugzetten ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet) cmdlet.


## <a name="related-information"></a>Gerelateerde informatie

[Azure storage-accounts](../storage/common/storage-create-storage-account.md)  
[Hoge beschikbaarheid](analysis-services-bcdr.md)     
[Azure analyseservices beheren](analysis-services-manage.md)
