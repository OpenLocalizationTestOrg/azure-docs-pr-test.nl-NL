---
title: "Gegevens kopiëren van Blob-opslag naar SQL Database - Azure | Microsoft Docs"
description: "Deze zelfstudie ziet u het gebruik van de Kopieeractiviteit in een Azure Data Factory-pijplijn om gegevens te kopiëren van Blob-opslag met SQL-database."
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
ms.openlocfilehash: 730140d15f4dec7ddc1280c2e4da1d247902fe4a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-copy-data-from-blob-storage-to-sql-database-using-data-factory"></a><span data-ttu-id="dd902-104">Zelfstudie: Gegevens kopiëren van Blob Storage met SQL Database met behulp van de Data Factory</span><span class="sxs-lookup"><span data-stu-id="dd902-104">Tutorial: Copy data from Blob Storage to SQL Database using Data Factory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dd902-105">Overzicht en vereisten</span><span class="sxs-lookup"><span data-stu-id="dd902-105">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="dd902-106">De wizard Kopiëren</span><span class="sxs-lookup"><span data-stu-id="dd902-106">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="dd902-107">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="dd902-107">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="dd902-108">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dd902-108">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="dd902-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd902-109">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="dd902-110">Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="dd902-110">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="dd902-111">REST API</span><span class="sxs-lookup"><span data-stu-id="dd902-111">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="dd902-112">.NET API</span><span class="sxs-lookup"><span data-stu-id="dd902-112">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="dd902-113">In deze zelfstudie maakt u een gegevensfactory met een pijplijn om gegevens te kopiëren van Blob-opslag met SQL-database.</span><span class="sxs-lookup"><span data-stu-id="dd902-113">In this tutorial, you create a data factory with a pipeline to copy data from Blob storage to SQL database.</span></span>

<span data-ttu-id="dd902-114">Met de kopieeractiviteit wordt de gegevensverplaatsing in Azure Data Factory uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="dd902-114">The Copy Activity performs the data movement in Azure Data Factory.</span></span> <span data-ttu-id="dd902-115">De activiteit wordt mogelijk gemaakt door een wereldwijd beschikbare service waarmee gegevens veilig, betrouwbaar en schaalbaar kunnen worden gekopieerd tussen verschillende gegevensarchieven.</span><span class="sxs-lookup"><span data-stu-id="dd902-115">It is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="dd902-116">Zie [Activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) voor meer informatie over de kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="dd902-116">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about the Copy Activity.</span></span>  

> [!NOTE]
> <span data-ttu-id="dd902-117">Zie voor een gedetailleerd overzicht van de Data Factory-service de [Inleiding tot Azure Data Factory](data-factory-introduction.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="dd902-117">For a detailed overview of the Data Factory service, see the [Introduction to Azure Data Factory](data-factory-introduction.md) article.</span></span>
>
>

## <a name="prerequisites-for-the-tutorial"></a><span data-ttu-id="dd902-118">Vereisten voor de zelfstudie</span><span class="sxs-lookup"><span data-stu-id="dd902-118">Prerequisites for the tutorial</span></span>
<span data-ttu-id="dd902-119">Voordat u met deze zelfstudie begint, moet u aan de volgende vereisten voldoen:</span><span class="sxs-lookup"><span data-stu-id="dd902-119">Before you begin this tutorial, you must have the following prerequisites:</span></span>

* <span data-ttu-id="dd902-120">**Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="dd902-120">**Azure subscription**.</span></span>  <span data-ttu-id="dd902-121">Als u geen abonnement hebt, kunt u binnen een paar minuten een gratis proefaccount maken.</span><span class="sxs-lookup"><span data-stu-id="dd902-121">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="dd902-122">Zie de [gratis proefversie](http://azure.microsoft.com/pricing/free-trial/) artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="dd902-122">See the [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.</span></span>
* <span data-ttu-id="dd902-123">**Azure Storage-Account**.</span><span class="sxs-lookup"><span data-stu-id="dd902-123">**Azure Storage Account**.</span></span> <span data-ttu-id="dd902-124">Gebruik van de blob storage als een **bron** gegevens opslaan in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="dd902-124">You use the blob storage as a **source** data store in this tutorial.</span></span> <span data-ttu-id="dd902-125">Als u geen Azure storage-account hebt, raadpleegt u de [een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account) voor stappen voor het maken van een artikel.</span><span class="sxs-lookup"><span data-stu-id="dd902-125">if you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps to create one.</span></span>
* <span data-ttu-id="dd902-126">**Azure SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="dd902-126">**Azure SQL Database**.</span></span> <span data-ttu-id="dd902-127">Gebruik van een Azure SQL database als een **bestemming** gegevens opslaan in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="dd902-127">You use an Azure SQL database as a **destination** data store in this tutorial.</span></span> <span data-ttu-id="dd902-128">Als u een Azure SQL-database die u in de zelfstudie, Zie gebruiken kunt geen [maken en configureren van een Azure SQL Database](../sql-database/sql-database-get-started.md) een maken.</span><span class="sxs-lookup"><span data-stu-id="dd902-128">If you don't have an Azure SQL database that you can use in the tutorial, See [How to create and configure an Azure SQL Database](../sql-database/sql-database-get-started.md) to create one.</span></span>
* <span data-ttu-id="dd902-129">**SQL Server 2012-2014 of Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="dd902-129">**SQL Server 2012/2014 or Visual Studio 2013**.</span></span> <span data-ttu-id="dd902-130">U gebruikt de SQL Server Management Studio of Visual Studio een voorbeelddatabase te maken en de result-gegevens weergeven in de database.</span><span class="sxs-lookup"><span data-stu-id="dd902-130">You use SQL Server Management Studio or Visual Studio to create a sample database and to view the result data in the database.</span></span>  

## <a name="collect-blob-storage-account-name-and-key"></a><span data-ttu-id="dd902-131">Blob storage-accountnaam en sleutel verzamelen</span><span class="sxs-lookup"><span data-stu-id="dd902-131">Collect blob storage account name and key</span></span>
<span data-ttu-id="dd902-132">U moet de accountnaam en accountsleutel van uw Azure storage-account te doen in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="dd902-132">You need the account name and account key of your Azure storage account to do this tutorial.</span></span> <span data-ttu-id="dd902-133">Noteer **accountnaam** en **accountsleutel** voor uw Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="dd902-133">Note down **account name** and **account key** for your Azure storage account.</span></span>

1. <span data-ttu-id="dd902-134">Meld u aan bij [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="dd902-134">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="dd902-135">Klik op **meer services** op het menu aan de linkerkant en selecteer **Opslagaccounts**.</span><span class="sxs-lookup"><span data-stu-id="dd902-135">Click **More services** on the left menu and select **Storage Accounts**.</span></span>

    ![Bladeren - Storage-accounts](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/browse-storage-accounts.png)
3. <span data-ttu-id="dd902-137">In de **Opslagaccounts** blade, selecteer de **Azure storage-account** die u wilt gebruiken in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="dd902-137">In the **Storage Accounts** blade, select the **Azure storage account** that you want to use in this tutorial.</span></span>
4. <span data-ttu-id="dd902-138">Selecteer **toegangssleutels** koppeling onder **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="dd902-138">Select **Access keys** link under **SETTINGS**.</span></span>
5. <span data-ttu-id="dd902-139">Klik op **kopie** (afbeelding)-knop naast **opslagaccountnaam** tekst vak en opslaan en ergens plakken (bijvoorbeeld: in een tekstbestand).</span><span class="sxs-lookup"><span data-stu-id="dd902-139">Click **copy** (image) button next to **Storage account name** text box and save/paste it somewhere (for example: in a text file).</span></span>
6. <span data-ttu-id="dd902-140">Herhaal de vorige stap om te kopiëren of noteer de **key1**.</span><span class="sxs-lookup"><span data-stu-id="dd902-140">Repeat the previous step to copy or note down the **key1**.</span></span>

    ![Toegangssleutel voor opslag](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/storage-access-key.png)
7. <span data-ttu-id="dd902-142">Alle blades te sluiten door te klikken op **X**.</span><span class="sxs-lookup"><span data-stu-id="dd902-142">Close all the blades by clicking **X**.</span></span>

## <a name="collect-sql-server-database-user-names"></a><span data-ttu-id="dd902-143">SQL server, database, gebruikersnamen verzamelen</span><span class="sxs-lookup"><span data-stu-id="dd902-143">Collect SQL server, database, user names</span></span>
<span data-ttu-id="dd902-144">U moet de namen van Azure SQL-server, database en gebruiker in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="dd902-144">You need the names of Azure SQL server, database, and user to do this tutorial.</span></span> <span data-ttu-id="dd902-145">Noteer de namen van **server**, **database**, en **gebruiker** voor uw Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="dd902-145">Note down names of **server**, **database**, and **user** for your Azure SQL database.</span></span>

1. <span data-ttu-id="dd902-146">In de **Azure-portal**, klikt u op **meer services** op de linkerkant en selecteer **SQL-databases**.</span><span class="sxs-lookup"><span data-stu-id="dd902-146">In the **Azure portal**, click **More services** on the left and select **SQL databases**.</span></span>
2. <span data-ttu-id="dd902-147">In de **SQL databases blade**, selecteer de **database** die u wilt gebruiken in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="dd902-147">In the **SQL databases blade**, select the **database** that you want to use in this tutorial.</span></span> <span data-ttu-id="dd902-148">Noteer de **databasenaam**.</span><span class="sxs-lookup"><span data-stu-id="dd902-148">Note down the **database name**.</span></span>  
3. <span data-ttu-id="dd902-149">In de **SQL-database** blade, klikt u op **eigenschappen** onder **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="dd902-149">In the **SQL database** blade, click **Properties** under **SETTINGS**.</span></span>
4. <span data-ttu-id="dd902-150">Noteer de waarden voor **servernaam** en **AANMELDGEGEVENS van SERVERBEHEERDER**.</span><span class="sxs-lookup"><span data-stu-id="dd902-150">Note down the values for **SERVER NAME** and **SERVER ADMIN LOGIN**.</span></span>
5. <span data-ttu-id="dd902-151">Alle blades te sluiten door te klikken op **X**.</span><span class="sxs-lookup"><span data-stu-id="dd902-151">Close all the blades by clicking **X**.</span></span>

## <a name="allow-azure-services-to-access-sql-server"></a><span data-ttu-id="dd902-152">Azure-services voor toegang tot SQL server toestaan</span><span class="sxs-lookup"><span data-stu-id="dd902-152">Allow Azure services to access SQL server</span></span>
<span data-ttu-id="dd902-153">Zorg ervoor dat **toegang tot Azure-services toestaan** instelling ingeschakeld **ON** voor uw Azure SQL-server zodat de Data Factory-service toegang heeft tot uw Azure SQL-server.</span><span class="sxs-lookup"><span data-stu-id="dd902-153">Ensure that **Allow access to Azure services** setting turned **ON** for your Azure SQL server so that the Data Factory service can access your Azure SQL server.</span></span> <span data-ttu-id="dd902-154">Controleren en deze instelling inschakelt, kunt u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="dd902-154">To verify and turn on this setting, do the following steps:</span></span>

1. <span data-ttu-id="dd902-155">Klik op **meer services** hub aan de linkerzijde en klik op **SQL-servers**.</span><span class="sxs-lookup"><span data-stu-id="dd902-155">Click **More services** hub on the left and click **SQL servers**.</span></span>
2. <span data-ttu-id="dd902-156">Selecteer uw server en klik op **Firewall** onder **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="dd902-156">Select your server, and click **Firewall** under **SETTINGS**.</span></span>
3. <span data-ttu-id="dd902-157">In de blade **Firewallinstellingen**schakelt u **Toegang tot Azure-services toestaan** **in**.</span><span class="sxs-lookup"><span data-stu-id="dd902-157">In the **Firewall settings** blade, click **ON** for **Allow access to Azure services**.</span></span>
4. <span data-ttu-id="dd902-158">Alle blades te sluiten door te klikken op **X**.</span><span class="sxs-lookup"><span data-stu-id="dd902-158">Close all the blades by clicking **X**.</span></span>

## <a name="prepare-blob-storage-and-sql-database"></a><span data-ttu-id="dd902-159">Blob-opslag- en SQL-Database voorbereiden</span><span class="sxs-lookup"><span data-stu-id="dd902-159">Prepare Blob Storage and SQL Database</span></span>
<span data-ttu-id="dd902-160">Nu uw Azure blob storage en Azure SQL database voor de zelfstudie door bereid de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="dd902-160">Now, prepare your Azure blob storage and Azure SQL database for the tutorial by performing the following steps:</span></span>  

1. <span data-ttu-id="dd902-161">Start Kladblok.</span><span class="sxs-lookup"><span data-stu-id="dd902-161">Launch Notepad.</span></span> <span data-ttu-id="dd902-162">Kopieer de volgende tekst en sla het bestand als **emp.txt** naar **C:\ADFGetStarted** map op de harde schijf.</span><span class="sxs-lookup"><span data-stu-id="dd902-162">Copy the following text and save it as **emp.txt** to **C:\ADFGetStarted** folder on your hard drive.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
2. <span data-ttu-id="dd902-163">Gebruik hulpprogramma's zoals [Azure Opslagverkenner](http://storageexplorer.com/) om de container **adftutorial** te maken en om het bestand **emp.txt** te uploaden naar de container.</span><span class="sxs-lookup"><span data-stu-id="dd902-163">Use tools such as [Azure Storage Explorer](http://storageexplorer.com/) to create the **adftutorial** container and to upload the **emp.txt** file to the container.</span></span>

    ![Azure Storage Explorer.](./media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/getstarted-storage-explorer.png)
3. <span data-ttu-id="dd902-166">Gebruik het volgende SQL-script om de tabel **emp** te maken in uw Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="dd902-166">Use the following SQL script to create the **emp** table in your Azure SQL Database.</span></span>  

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

    <span data-ttu-id="dd902-167">**Als u SQL Server 2012-2014 op uw computer geïnstalleerd hebben:** Volg de instructies uit [beherende Azure SQL Database met SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) verbinding maken met uw Azure SQL-server en voer de SQL-script.</span><span class="sxs-lookup"><span data-stu-id="dd902-167">**If you have SQL Server 2012/2014 installed on your computer:** follow instructions from [Managing Azure SQL Database using SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) to connect to your Azure SQL server and run the SQL script.</span></span> <span data-ttu-id="dd902-168">Dit artikel wordt de [klassieke Azure portal](http://manage.windowsazure.com), niet de [nieuwe Azure portal](https://portal.azure.com), firewall voor een Azure SQL-server te configureren.</span><span class="sxs-lookup"><span data-stu-id="dd902-168">This article uses the [classic Azure portal](http://manage.windowsazure.com), not the [new Azure portal](https://portal.azure.com), to configure firewall for an Azure SQL server.</span></span>

    <span data-ttu-id="dd902-169">Als de client geen toegang heeft tot de Azure SQL-server, moet u de firewall configureren voor uw Azure SQL-server zodat toegang vanaf uw apparaat (IP-adres) wordt toegestaan.</span><span class="sxs-lookup"><span data-stu-id="dd902-169">If your client is not allowed to access the Azure SQL server, you need to configure firewall for your Azure SQL server to allow access from your machine (IP Address).</span></span> <span data-ttu-id="dd902-170">Raadpleeg [dit artikel](../sql-database/sql-database-configure-firewall-settings.md) voor stappen waarmee u uw firewall kunt configureren voor uw Azure SQL-server.</span><span class="sxs-lookup"><span data-stu-id="dd902-170">See [this article](../sql-database/sql-database-configure-firewall-settings.md) for steps to configure the firewall for your Azure SQL server.</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="dd902-171">Een data factory maken</span><span class="sxs-lookup"><span data-stu-id="dd902-171">Create a data factory</span></span>
<span data-ttu-id="dd902-172">U kunt de vereisten hebt voltooid.</span><span class="sxs-lookup"><span data-stu-id="dd902-172">You have completed the prerequisites.</span></span> <span data-ttu-id="dd902-173">U kunt een gegevensfactory met een van de volgende manieren maken.</span><span class="sxs-lookup"><span data-stu-id="dd902-173">You can create a data factory using one of the following ways.</span></span> <span data-ttu-id="dd902-174">Klik op een van de opties in de vervolgkeuzelijst boven of de volgende koppelingen voor het uitvoeren van de zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="dd902-174">Click one of the options in the drop-down list at the top or the following links to perform the tutorial.</span></span>     

* [<span data-ttu-id="dd902-175">De wizard Kopiëren</span><span class="sxs-lookup"><span data-stu-id="dd902-175">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
* [<span data-ttu-id="dd902-176">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="dd902-176">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
* [<span data-ttu-id="dd902-177">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dd902-177">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
* [<span data-ttu-id="dd902-178">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd902-178">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
* [<span data-ttu-id="dd902-179">Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="dd902-179">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [<span data-ttu-id="dd902-180">REST API</span><span class="sxs-lookup"><span data-stu-id="dd902-180">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
* [<span data-ttu-id="dd902-181">.NET API</span><span class="sxs-lookup"><span data-stu-id="dd902-181">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

> [!NOTE]
> <span data-ttu-id="dd902-182">In de gegevenspijplijn in deze zelfstudie worden gegevens van een brongegevensarchief gekopieerd naar een doelgegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="dd902-182">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="dd902-183">Er worden geen invoergegevens mee getransformeerd in uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="dd902-183">It does not transform input data to produce output data.</span></span> <span data-ttu-id="dd902-184">Zie [Zelfstudie: uw eerste pijplijn maken om gegevens te transformeren met een Hadoop-cluster](data-factory-build-your-first-pipeline.md) voor meer informatie over het transformeren van gegevens met Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="dd902-184">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build your first pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>
> 
> <span data-ttu-id="dd902-185">U kunt twee activiteiten koppelen (de ene activiteit na de andere laten uitvoeren) door de uitvoergegevensset van één activiteit in te stellen als invoergegevensset voor een andere activiteit.</span><span class="sxs-lookup"><span data-stu-id="dd902-185">You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="dd902-186">Zie [Planning en uitvoering in Data Factory](data-factory-scheduling-and-execution.md) voor gedetailleerde informatie.</span><span class="sxs-lookup"><span data-stu-id="dd902-186">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 
