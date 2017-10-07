---
title: aaaCopy gegevens uit Blob Storage tooSQL Database - Azure | Microsoft Docs
description: Deze zelfstudie leert u hoe toouse Kopieeractiviteit in een Azure Data Factory toocopy gegevens uit Blob storage tooSQL database pipeline.
keywords: "BLOB-sql, blob-opslag, gegevens opnieuw te kopiëren"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: e4035060-93bf-4e8d-bf35-35e2d15c51e0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: a2c3fb8a4ddd63b0b6b3e75903b7a7eaf188fda4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-copy-data-from-blob-storage-toosql-database-using-data-factory"></a>Zelfstudie: Gegevens kopiëren van Blob Storage tooSQL-Database met de Data Factory
> [!div class="op_single_selector"]
> * [Overzicht en vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [De wizard Kopiëren](data-factory-copy-data-wizard-tutorial.md)
> * [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Azure Resource Manager-sjabloon](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [REST API](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [.NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md)

In deze zelfstudie maakt u een gegevensfactory met een pipeline toocopy gegevens uit Blob storage tooSQL database.

Hallo Kopieeractiviteit Hallo gegevensverplaatsing in Azure Data Factory uitgevoerd. De activiteit wordt mogelijk gemaakt door een wereldwijd beschikbare service waarmee gegevens veilig, betrouwbaar en schaalbaar kunnen worden gekopieerd tussen verschillende gegevensarchieven. Zie [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) voor meer informatie over Hallo Kopieeractiviteit.  

> [!NOTE]
> Zie voor een gedetailleerd overzicht van Data Factory-service Hallo Hallo [inleiding tooAzure Data Factory](data-factory-introduction.md) artikel.
>
>

## <a name="prerequisites-for-hello-tutorial"></a>Vereisten voor het Hallo-zelfstudie
Voordat u deze zelfstudie begint, hebt u Hallo volgende vereisten:

* **Azure-abonnement**.  Als u geen abonnement hebt, kunt u binnen een paar minuten een gratis proefaccount maken. Zie Hallo [gratis proefversie](http://azure.microsoft.com/pricing/free-trial/) artikel voor meer informatie.
* **Azure Storage-Account**. Gebruik van Hallo blob storage als een **bron** gegevens opslaan in deze zelfstudie. Als u geen Azure storage-account hebt, raadpleegt u Hallo [een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account) artikel voor stappen toocreate een.
* **Azure SQL-database**. Gebruik van een Azure SQL database als een **bestemming** gegevens opslaan in deze zelfstudie. Als u een Azure SQL-database die u in de zelfstudie hello, Zie gebruiken kunt geen [hoe toocreate en configureren van een Azure SQL Database](../sql-database/sql-database-get-started.md) toocreate een.
* **SQL Server 2012-2014 of Visual Studio 2013**. U gebruikt de SQL Server Management Studio of Visual Studio toocreate een voorbeelddatabase en tooview Hallo resultaatgegevens in Hallo-database.  

## <a name="collect-blob-storage-account-name-and-key"></a>Blob storage-accountnaam en sleutel verzamelen
U moet Hallo account naam en sleutel van uw Azure-opslag account toodo in deze zelfstudie. Noteer **accountnaam** en **accountsleutel** voor uw Azure storage-account.

1. Meld u bij toohello [Azure-portal](https://portal.azure.com/).
2. Klik op **meer services** op Hallo menu en selecteer links **Opslagaccounts**.

    ![Bladeren - Storage-accounts](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/browse-storage-accounts.png)
3. In Hallo **Opslagaccounts** blade, selecteer Hallo **Azure storage-account** gewenste toouse in deze zelfstudie.
4. Selecteer **toegangssleutels** koppeling onder **instellingen**.
5. Klik op **kopie** (afbeelding) knop naast te**opslagaccountnaam** tekst vak en opslaan en ergens plakken (bijvoorbeeld: in een tekstbestand).
6. Herhaal de vorige stap toocopy Hallo of noteer Hallo **key1**.

    ![Toegangssleutel voor opslag](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/storage-access-key.png)
7. Alle Hallo blades sluiten door te klikken op **X**.

## <a name="collect-sql-server-database-user-names"></a>SQL server, database, gebruikersnamen verzamelen
U moet deze zelfstudie Hallo namen van Azure SQL-server, database en gebruiker toodo. Noteer de namen van **server**, **database**, en **gebruiker** voor uw Azure SQL database.

1. In Hallo **Azure-portal**, klikt u op **meer services** op Hallo linker- en selecteer **SQL-databases**.
2. In Hallo **SQL databases blade**, selecteer Hallo **database** gewenste toouse in deze zelfstudie. Noteer Hallo **databasenaam**.  
3. In Hallo **SQL-database** blade, klikt u op **eigenschappen** onder **instellingen**.
4. Noteer Hallo waarden voor **servernaam** en **AANMELDGEGEVENS van SERVERBEHEERDER**.
5. Alle Hallo blades sluiten door te klikken op **X**.

## <a name="allow-azure-services-tooaccess-sql-server"></a>Azure-services tooaccess SQL server toestaan
Zorg ervoor dat **tooAzure-services toegang toestaan** instelling ingeschakeld **ON** voor uw Azure SQL-server zodat deze Hallo Data Factory-service toegang heeft tot uw Azure SQL-server. tooverify en schakel deze instelling kan Hallo volgende stappen:

1. Klik op **meer services** hub op Hallo linkerkant en klik op **SQL-servers**.
2. Selecteer uw server en klik op **Firewall** onder **INSTELLINGEN**.
3. In Hallo **Firewall-instellingen** blade, klikt u op **ON** voor **tooAzure-services toegang toestaan**.
4. Alle Hallo blades sluiten door te klikken op **X**.

## <a name="prepare-blob-storage-and-sql-database"></a>Blob-opslag- en SQL-Database voorbereiden
Voorbereiden nu uw Azure blob storage en Azure SQL database voor Hallo zelfstudie door Hallo volgende stappen uit te voeren:  

1. Start Kladblok. Kopiëren van de volgende tekst hello en sla het bestand als **emp.txt** te**C:\ADFGetStarted** map op de harde schijf.

    ```
    John, Doe
    Jane, Doe
    ```
2. Gebruik hulpprogramma's zoals [Azure Opslagverkenner](http://storageexplorer.com/) toocreate hello **adftutorial** container en tooupload hello **emp.txt** toohello bestandscontainer.

    ![Azure Storage Explorer. Gegevens kopiëren van Blob storage tooSQL database](./media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/getstarted-storage-explorer.png)
3. Gebruik Hallo volgende SQL-script toocreate hello **emp** tabel in uw Azure SQL Database.  

    ```SQL
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50),
    )
    GO

    CREATE CLUSTERED INDEX IX_emp_ID ON dbo.emp (ID);
    ```

    **Als u SQL Server 2012-2014 op uw computer geïnstalleerd hebben:** Volg de instructies uit [beherende Azure SQL Database met SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) tooconnect tooyour Azure SQL-server en Voer Hallo SQL-script. Dit artikel wordt Hallo [klassieke Azure portal](http://manage.windowsazure.com), niet Hallo [nieuwe Azure portal](https://portal.azure.com), tooconfigure firewall voor een Azure SQL-server.

    Als de client is niet toegestaan voor tooaccess hello Azure SQL-server, moet u tooconfigure firewall voor uw Azure SQL server tooallow toegang vanaf uw computer (IP-adres). Zie [in dit artikel](../sql-database/sql-database-configure-firewall-settings.md) voor stappen tooconfigure Hallo firewall voor uw Azure SQL-server.

## <a name="create-a-data-factory"></a>Een data factory maken
Hallo vereisten is voltooid. U kunt een gegevensfactory met een van de volgende manieren Hallo maken. Klik op een van de opties Hallo in Hallo vervolgkeuzelijst Hallo koppelingen tooperform Hallo zelfstudie of Hallo bovenaan.     

* [De wizard Kopiëren](data-factory-copy-data-wizard-tutorial.md)
* [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md)
* [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
* [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
* [Azure Resource Manager-sjabloon](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [REST API](data-factory-copy-activity-tutorial-using-rest-api.md)
* [.NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md)

> [!NOTE]
> Hallo data pipeline in deze zelfstudie worden gegevens gekopieerd van een bron data store tooa doelgegevensopslagplaats. Het biedt invoergegevens tooproduce uitvoergegevens niet transformeren. Voor een zelfstudie over het tootransform van gegevens met behulp van Azure Data Factory, Zie [zelfstudie: bouwen van uw eerste pijplijn tootransform gegevens met Hadoop-cluster](data-factory-build-your-first-pipeline.md).
> 
> U kunt twee activiteiten (één activiteit uitgevoerd na de andere) koppelen door de uitvoergegevensset Hallo van een activiteit instellen als de Hallo invoergegevensset Hallo andere activiteit. Zie [Planning en uitvoering in Data Factory](data-factory-scheduling-and-execution.md) voor gedetailleerde informatie. 
