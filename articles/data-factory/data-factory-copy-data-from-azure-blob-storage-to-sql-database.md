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
# <a name="tutorial-copy-data-from-blob-storage-toosql-database-using-data-factory"></a><span data-ttu-id="18fde-104">Zelfstudie: Gegevens kopiëren van Blob Storage tooSQL-Database met de Data Factory</span><span class="sxs-lookup"><span data-stu-id="18fde-104">Tutorial: Copy data from Blob Storage tooSQL Database using Data Factory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="18fde-105">Overzicht en vereisten</span><span class="sxs-lookup"><span data-stu-id="18fde-105">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="18fde-106">De wizard Kopiëren</span><span class="sxs-lookup"><span data-stu-id="18fde-106">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="18fde-107">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="18fde-107">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="18fde-108">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="18fde-108">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="18fde-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="18fde-109">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="18fde-110">Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="18fde-110">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="18fde-111">REST API</span><span class="sxs-lookup"><span data-stu-id="18fde-111">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="18fde-112">.NET API</span><span class="sxs-lookup"><span data-stu-id="18fde-112">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="18fde-113">In deze zelfstudie maakt u een gegevensfactory met een pipeline toocopy gegevens uit Blob storage tooSQL database.</span><span class="sxs-lookup"><span data-stu-id="18fde-113">In this tutorial, you create a data factory with a pipeline toocopy data from Blob storage tooSQL database.</span></span>

<span data-ttu-id="18fde-114">Hallo Kopieeractiviteit Hallo gegevensverplaatsing in Azure Data Factory uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="18fde-114">hello Copy Activity performs hello data movement in Azure Data Factory.</span></span> <span data-ttu-id="18fde-115">De activiteit wordt mogelijk gemaakt door een wereldwijd beschikbare service waarmee gegevens veilig, betrouwbaar en schaalbaar kunnen worden gekopieerd tussen verschillende gegevensarchieven.</span><span class="sxs-lookup"><span data-stu-id="18fde-115">It is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="18fde-116">Zie [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) voor meer informatie over Hallo Kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="18fde-116">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about hello Copy Activity.</span></span>  

> [!NOTE]
> <span data-ttu-id="18fde-117">Zie voor een gedetailleerd overzicht van Data Factory-service Hallo Hallo [inleiding tooAzure Data Factory](data-factory-introduction.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="18fde-117">For a detailed overview of hello Data Factory service, see hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article.</span></span>
>
>

## <a name="prerequisites-for-hello-tutorial"></a><span data-ttu-id="18fde-118">Vereisten voor het Hallo-zelfstudie</span><span class="sxs-lookup"><span data-stu-id="18fde-118">Prerequisites for hello tutorial</span></span>
<span data-ttu-id="18fde-119">Voordat u deze zelfstudie begint, hebt u Hallo volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="18fde-119">Before you begin this tutorial, you must have hello following prerequisites:</span></span>

* <span data-ttu-id="18fde-120">**Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="18fde-120">**Azure subscription**.</span></span>  <span data-ttu-id="18fde-121">Als u geen abonnement hebt, kunt u binnen een paar minuten een gratis proefaccount maken.</span><span class="sxs-lookup"><span data-stu-id="18fde-121">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="18fde-122">Zie Hallo [gratis proefversie](http://azure.microsoft.com/pricing/free-trial/) artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="18fde-122">See hello [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.</span></span>
* <span data-ttu-id="18fde-123">**Azure Storage-Account**.</span><span class="sxs-lookup"><span data-stu-id="18fde-123">**Azure Storage Account**.</span></span> <span data-ttu-id="18fde-124">Gebruik van Hallo blob storage als een **bron** gegevens opslaan in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="18fde-124">You use hello blob storage as a **source** data store in this tutorial.</span></span> <span data-ttu-id="18fde-125">Als u geen Azure storage-account hebt, raadpleegt u Hallo [een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account) artikel voor stappen toocreate een.</span><span class="sxs-lookup"><span data-stu-id="18fde-125">if you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps toocreate one.</span></span>
* <span data-ttu-id="18fde-126">**Azure SQL-database**.</span><span class="sxs-lookup"><span data-stu-id="18fde-126">**Azure SQL Database**.</span></span> <span data-ttu-id="18fde-127">Gebruik van een Azure SQL database als een **bestemming** gegevens opslaan in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="18fde-127">You use an Azure SQL database as a **destination** data store in this tutorial.</span></span> <span data-ttu-id="18fde-128">Als u een Azure SQL-database die u in de zelfstudie hello, Zie gebruiken kunt geen [hoe toocreate en configureren van een Azure SQL Database](../sql-database/sql-database-get-started.md) toocreate een.</span><span class="sxs-lookup"><span data-stu-id="18fde-128">If you don't have an Azure SQL database that you can use in hello tutorial, See [How toocreate and configure an Azure SQL Database](../sql-database/sql-database-get-started.md) toocreate one.</span></span>
* <span data-ttu-id="18fde-129">**SQL Server 2012-2014 of Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="18fde-129">**SQL Server 2012/2014 or Visual Studio 2013**.</span></span> <span data-ttu-id="18fde-130">U gebruikt de SQL Server Management Studio of Visual Studio toocreate een voorbeelddatabase en tooview Hallo resultaatgegevens in Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="18fde-130">You use SQL Server Management Studio or Visual Studio toocreate a sample database and tooview hello result data in hello database.</span></span>  

## <a name="collect-blob-storage-account-name-and-key"></a><span data-ttu-id="18fde-131">Blob storage-accountnaam en sleutel verzamelen</span><span class="sxs-lookup"><span data-stu-id="18fde-131">Collect blob storage account name and key</span></span>
<span data-ttu-id="18fde-132">U moet Hallo account naam en sleutel van uw Azure-opslag account toodo in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="18fde-132">You need hello account name and account key of your Azure storage account toodo this tutorial.</span></span> <span data-ttu-id="18fde-133">Noteer **accountnaam** en **accountsleutel** voor uw Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="18fde-133">Note down **account name** and **account key** for your Azure storage account.</span></span>

1. <span data-ttu-id="18fde-134">Meld u bij toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="18fde-134">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="18fde-135">Klik op **meer services** op Hallo menu en selecteer links **Opslagaccounts**.</span><span class="sxs-lookup"><span data-stu-id="18fde-135">Click **More services** on hello left menu and select **Storage Accounts**.</span></span>

    ![Bladeren - Storage-accounts](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/browse-storage-accounts.png)
3. <span data-ttu-id="18fde-137">In Hallo **Opslagaccounts** blade, selecteer Hallo **Azure storage-account** gewenste toouse in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="18fde-137">In hello **Storage Accounts** blade, select hello **Azure storage account** that you want toouse in this tutorial.</span></span>
4. <span data-ttu-id="18fde-138">Selecteer **toegangssleutels** koppeling onder **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="18fde-138">Select **Access keys** link under **SETTINGS**.</span></span>
5. <span data-ttu-id="18fde-139">Klik op **kopie** (afbeelding) knop naast te**opslagaccountnaam** tekst vak en opslaan en ergens plakken (bijvoorbeeld: in een tekstbestand).</span><span class="sxs-lookup"><span data-stu-id="18fde-139">Click **copy** (image) button next too**Storage account name** text box and save/paste it somewhere (for example: in a text file).</span></span>
6. <span data-ttu-id="18fde-140">Herhaal de vorige stap toocopy Hallo of noteer Hallo **key1**.</span><span class="sxs-lookup"><span data-stu-id="18fde-140">Repeat hello previous step toocopy or note down hello **key1**.</span></span>

    ![Toegangssleutel voor opslag](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/storage-access-key.png)
7. <span data-ttu-id="18fde-142">Alle Hallo blades sluiten door te klikken op **X**.</span><span class="sxs-lookup"><span data-stu-id="18fde-142">Close all hello blades by clicking **X**.</span></span>

## <a name="collect-sql-server-database-user-names"></a><span data-ttu-id="18fde-143">SQL server, database, gebruikersnamen verzamelen</span><span class="sxs-lookup"><span data-stu-id="18fde-143">Collect SQL server, database, user names</span></span>
<span data-ttu-id="18fde-144">U moet deze zelfstudie Hallo namen van Azure SQL-server, database en gebruiker toodo.</span><span class="sxs-lookup"><span data-stu-id="18fde-144">You need hello names of Azure SQL server, database, and user toodo this tutorial.</span></span> <span data-ttu-id="18fde-145">Noteer de namen van **server**, **database**, en **gebruiker** voor uw Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="18fde-145">Note down names of **server**, **database**, and **user** for your Azure SQL database.</span></span>

1. <span data-ttu-id="18fde-146">In Hallo **Azure-portal**, klikt u op **meer services** op Hallo linker- en selecteer **SQL-databases**.</span><span class="sxs-lookup"><span data-stu-id="18fde-146">In hello **Azure portal**, click **More services** on hello left and select **SQL databases**.</span></span>
2. <span data-ttu-id="18fde-147">In Hallo **SQL databases blade**, selecteer Hallo **database** gewenste toouse in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="18fde-147">In hello **SQL databases blade**, select hello **database** that you want toouse in this tutorial.</span></span> <span data-ttu-id="18fde-148">Noteer Hallo **databasenaam**.</span><span class="sxs-lookup"><span data-stu-id="18fde-148">Note down hello **database name**.</span></span>  
3. <span data-ttu-id="18fde-149">In Hallo **SQL-database** blade, klikt u op **eigenschappen** onder **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="18fde-149">In hello **SQL database** blade, click **Properties** under **SETTINGS**.</span></span>
4. <span data-ttu-id="18fde-150">Noteer Hallo waarden voor **servernaam** en **AANMELDGEGEVENS van SERVERBEHEERDER**.</span><span class="sxs-lookup"><span data-stu-id="18fde-150">Note down hello values for **SERVER NAME** and **SERVER ADMIN LOGIN**.</span></span>
5. <span data-ttu-id="18fde-151">Alle Hallo blades sluiten door te klikken op **X**.</span><span class="sxs-lookup"><span data-stu-id="18fde-151">Close all hello blades by clicking **X**.</span></span>

## <a name="allow-azure-services-tooaccess-sql-server"></a><span data-ttu-id="18fde-152">Azure-services tooaccess SQL server toestaan</span><span class="sxs-lookup"><span data-stu-id="18fde-152">Allow Azure services tooaccess SQL server</span></span>
<span data-ttu-id="18fde-153">Zorg ervoor dat **tooAzure-services toegang toestaan** instelling ingeschakeld **ON** voor uw Azure SQL-server zodat deze Hallo Data Factory-service toegang heeft tot uw Azure SQL-server.</span><span class="sxs-lookup"><span data-stu-id="18fde-153">Ensure that **Allow access tooAzure services** setting turned **ON** for your Azure SQL server so that hello Data Factory service can access your Azure SQL server.</span></span> <span data-ttu-id="18fde-154">tooverify en schakel deze instelling kan Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="18fde-154">tooverify and turn on this setting, do hello following steps:</span></span>

1. <span data-ttu-id="18fde-155">Klik op **meer services** hub op Hallo linkerkant en klik op **SQL-servers**.</span><span class="sxs-lookup"><span data-stu-id="18fde-155">Click **More services** hub on hello left and click **SQL servers**.</span></span>
2. <span data-ttu-id="18fde-156">Selecteer uw server en klik op **Firewall** onder **INSTELLINGEN**.</span><span class="sxs-lookup"><span data-stu-id="18fde-156">Select your server, and click **Firewall** under **SETTINGS**.</span></span>
3. <span data-ttu-id="18fde-157">In Hallo **Firewall-instellingen** blade, klikt u op **ON** voor **tooAzure-services toegang toestaan**.</span><span class="sxs-lookup"><span data-stu-id="18fde-157">In hello **Firewall settings** blade, click **ON** for **Allow access tooAzure services**.</span></span>
4. <span data-ttu-id="18fde-158">Alle Hallo blades sluiten door te klikken op **X**.</span><span class="sxs-lookup"><span data-stu-id="18fde-158">Close all hello blades by clicking **X**.</span></span>

## <a name="prepare-blob-storage-and-sql-database"></a><span data-ttu-id="18fde-159">Blob-opslag- en SQL-Database voorbereiden</span><span class="sxs-lookup"><span data-stu-id="18fde-159">Prepare Blob Storage and SQL Database</span></span>
<span data-ttu-id="18fde-160">Voorbereiden nu uw Azure blob storage en Azure SQL database voor Hallo zelfstudie door Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="18fde-160">Now, prepare your Azure blob storage and Azure SQL database for hello tutorial by performing hello following steps:</span></span>  

1. <span data-ttu-id="18fde-161">Start Kladblok.</span><span class="sxs-lookup"><span data-stu-id="18fde-161">Launch Notepad.</span></span> <span data-ttu-id="18fde-162">Kopiëren van de volgende tekst hello en sla het bestand als **emp.txt** te**C:\ADFGetStarted** map op de harde schijf.</span><span class="sxs-lookup"><span data-stu-id="18fde-162">Copy hello following text and save it as **emp.txt** too**C:\ADFGetStarted** folder on your hard drive.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
2. <span data-ttu-id="18fde-163">Gebruik hulpprogramma's zoals [Azure Opslagverkenner](http://storageexplorer.com/) toocreate hello **adftutorial** container en tooupload hello **emp.txt** toohello bestandscontainer.</span><span class="sxs-lookup"><span data-stu-id="18fde-163">Use tools such as [Azure Storage Explorer](http://storageexplorer.com/) toocreate hello **adftutorial** container and tooupload hello **emp.txt** file toohello container.</span></span>

    ![Azure Storage Explorer.](./media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/getstarted-storage-explorer.png)
3. <span data-ttu-id="18fde-166">Gebruik Hallo volgende SQL-script toocreate hello **emp** tabel in uw Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="18fde-166">Use hello following SQL script toocreate hello **emp** table in your Azure SQL Database.</span></span>  

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

    <span data-ttu-id="18fde-167">**Als u SQL Server 2012-2014 op uw computer geïnstalleerd hebben:** Volg de instructies uit [beherende Azure SQL Database met SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) tooconnect tooyour Azure SQL-server en Voer Hallo SQL-script.</span><span class="sxs-lookup"><span data-stu-id="18fde-167">**If you have SQL Server 2012/2014 installed on your computer:** follow instructions from [Managing Azure SQL Database using SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) tooconnect tooyour Azure SQL server and run hello SQL script.</span></span> <span data-ttu-id="18fde-168">Dit artikel wordt Hallo [klassieke Azure portal](http://manage.windowsazure.com), niet Hallo [nieuwe Azure portal](https://portal.azure.com), tooconfigure firewall voor een Azure SQL-server.</span><span class="sxs-lookup"><span data-stu-id="18fde-168">This article uses hello [classic Azure portal](http://manage.windowsazure.com), not hello [new Azure portal](https://portal.azure.com), tooconfigure firewall for an Azure SQL server.</span></span>

    <span data-ttu-id="18fde-169">Als de client is niet toegestaan voor tooaccess hello Azure SQL-server, moet u tooconfigure firewall voor uw Azure SQL server tooallow toegang vanaf uw computer (IP-adres).</span><span class="sxs-lookup"><span data-stu-id="18fde-169">If your client is not allowed tooaccess hello Azure SQL server, you need tooconfigure firewall for your Azure SQL server tooallow access from your machine (IP Address).</span></span> <span data-ttu-id="18fde-170">Zie [in dit artikel](../sql-database/sql-database-configure-firewall-settings.md) voor stappen tooconfigure Hallo firewall voor uw Azure SQL-server.</span><span class="sxs-lookup"><span data-stu-id="18fde-170">See [this article](../sql-database/sql-database-configure-firewall-settings.md) for steps tooconfigure hello firewall for your Azure SQL server.</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="18fde-171">Een data factory maken</span><span class="sxs-lookup"><span data-stu-id="18fde-171">Create a data factory</span></span>
<span data-ttu-id="18fde-172">Hallo vereisten is voltooid.</span><span class="sxs-lookup"><span data-stu-id="18fde-172">You have completed hello prerequisites.</span></span> <span data-ttu-id="18fde-173">U kunt een gegevensfactory met een van de volgende manieren Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="18fde-173">You can create a data factory using one of hello following ways.</span></span> <span data-ttu-id="18fde-174">Klik op een van de opties Hallo in Hallo vervolgkeuzelijst Hallo koppelingen tooperform Hallo zelfstudie of Hallo bovenaan.</span><span class="sxs-lookup"><span data-stu-id="18fde-174">Click one of hello options in hello drop-down list at hello top or hello following links tooperform hello tutorial.</span></span>     

* [<span data-ttu-id="18fde-175">De wizard Kopiëren</span><span class="sxs-lookup"><span data-stu-id="18fde-175">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
* [<span data-ttu-id="18fde-176">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="18fde-176">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
* [<span data-ttu-id="18fde-177">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="18fde-177">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
* [<span data-ttu-id="18fde-178">PowerShell</span><span class="sxs-lookup"><span data-stu-id="18fde-178">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
* [<span data-ttu-id="18fde-179">Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="18fde-179">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [<span data-ttu-id="18fde-180">REST API</span><span class="sxs-lookup"><span data-stu-id="18fde-180">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
* [<span data-ttu-id="18fde-181">.NET API</span><span class="sxs-lookup"><span data-stu-id="18fde-181">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

> [!NOTE]
> <span data-ttu-id="18fde-182">Hallo data pipeline in deze zelfstudie worden gegevens gekopieerd van een bron data store tooa doelgegevensopslagplaats.</span><span class="sxs-lookup"><span data-stu-id="18fde-182">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="18fde-183">Het biedt invoergegevens tooproduce uitvoergegevens niet transformeren.</span><span class="sxs-lookup"><span data-stu-id="18fde-183">It does not transform input data tooproduce output data.</span></span> <span data-ttu-id="18fde-184">Voor een zelfstudie over het tootransform van gegevens met behulp van Azure Data Factory, Zie [zelfstudie: bouwen van uw eerste pijplijn tootransform gegevens met Hadoop-cluster](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="18fde-184">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build your first pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>
> 
> <span data-ttu-id="18fde-185">U kunt twee activiteiten (één activiteit uitgevoerd na de andere) koppelen door de uitvoergegevensset Hallo van een activiteit instellen als de Hallo invoergegevensset Hallo andere activiteit.</span><span class="sxs-lookup"><span data-stu-id="18fde-185">You can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="18fde-186">Zie [Planning en uitvoering in Data Factory](data-factory-scheduling-and-execution.md) voor gedetailleerde informatie.</span><span class="sxs-lookup"><span data-stu-id="18fde-186">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 
