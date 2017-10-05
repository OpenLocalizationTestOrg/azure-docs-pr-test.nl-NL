---
title: Gegevens verplaatsen van een lokale SQL Server naar SQL Azure met Azure Data Factory | Microsoft Docs
description: Stel een ADF-pijplijn die stelt het bericht op twee activiteiten van de gegevens migreren die gegevens samen dagelijks tussen databases on-premises en in de cloud verplaatsen.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 36837c83-2015-48be-b850-c4346aa5ae8a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 39fe26d3388be8b558f05063a8965889c013a41e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-from-an-on-premises-sql-server-to-sql-azure-with-azure-data-factory"></a><span data-ttu-id="e43c4-103">Gegevens verplaatsen van een lokale SQL server naar SQL Azure met Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="e43c4-103">Move data from an on-premises SQL server to SQL Azure with Azure Data Factory</span></span>
<span data-ttu-id="e43c4-104">Dit onderwerp wordt beschreven hoe gegevens uit een lokale SQL Server-Database verplaatsen naar een Azure SQL Database via Azure Blob Storage met Azure Data Factory (ADF).</span><span class="sxs-lookup"><span data-stu-id="e43c4-104">This topic shows how to move data from an on-premises SQL Server Database to a SQL Azure Database via Azure Blob Storage using the Azure Data Factory (ADF).</span></span>

<span data-ttu-id="e43c4-105">Zie voor een tabel die een overzicht van de verschillende opties voor het verplaatsen van gegevens naar een Azure SQL Database, [gegevens verplaatsen naar een Azure SQL Database voor Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span><span class="sxs-lookup"><span data-stu-id="e43c4-105">For a table that summarizes various options for moving data to an Azure SQL Database, see [Move data to an Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span></span>

## <span data-ttu-id="e43c4-106"><a name="intro"></a>Inleiding: Wat is er ADF en wanneer moet deze worden gebruikt om gegevens te migreren?</span><span class="sxs-lookup"><span data-stu-id="e43c4-106"><a name="intro"></a>Introduction: What is ADF and when should it be used to migrate data?</span></span>
<span data-ttu-id="e43c4-107">Azure Data Factory is een volledig beheerde gegevens cloud-gebaseerde integration-service die is ingedeeld en automatiseert de verplaatsing en transformatie van gegevens.</span><span class="sxs-lookup"><span data-stu-id="e43c4-107">Azure Data Factory is a fully managed cloud-based data integration service that orchestrates and automates the movement and transformation of data.</span></span> <span data-ttu-id="e43c4-108">Het belangrijkste concept in het model ADF is pijplijn.</span><span class="sxs-lookup"><span data-stu-id="e43c4-108">The key concept in the ADF model is pipeline.</span></span> <span data-ttu-id="e43c4-109">Een pijplijn is een logische groepering van activiteiten, die elk de acties die worden uitgevoerd op de gegevens in de gegevenssets definieert.</span><span class="sxs-lookup"><span data-stu-id="e43c4-109">A pipeline is a logical grouping of Activities, each of which defines the actions to perform on the data contained in Datasets.</span></span> <span data-ttu-id="e43c4-110">Gekoppelde services worden gebruikt voor het definiëren van de informatie die nodig zijn voor Data Factory verbinding maken met de gegevensbronnen.</span><span class="sxs-lookup"><span data-stu-id="e43c4-110">Linked services are used to define the information needed for Data Factory to connect to the data resources.</span></span>

<span data-ttu-id="e43c4-111">Met ADF, bestaande services voor gegevensverwerking samengesteld kunnen zijn, in gegevenspijplijnen die maximaal beschikbaar en wordt beheerd in de cloud.</span><span class="sxs-lookup"><span data-stu-id="e43c4-111">With ADF, existing data processing services can be composed into data pipelines that are highly available and managed in the cloud.</span></span> <span data-ttu-id="e43c4-112">Deze gegevenspijplijnen voor opnemen, voorbereiden, transformeren, analyseren en publiceren van gegevens kunnen worden gepland en ADF beheert en stuurt de complexe gegevens en de verwerking van afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="e43c4-112">These data pipelines can be scheduled to ingest, prepare, transform, analyze, and publish data, and ADF manages and orchestrates the complex data and processing dependencies.</span></span> <span data-ttu-id="e43c4-113">Oplossingen kunnen snel worden gemaakt en geïmplementeerd in de cloud, verbinding maken met een toenemend aantal lokale en cloud-gegevensbronnen.</span><span class="sxs-lookup"><span data-stu-id="e43c4-113">Solutions can be quickly built and deployed in the cloud, connecting a growing number of on-premises and cloud data sources.</span></span>

<span data-ttu-id="e43c4-114">Overweeg het gebruik van ADF:</span><span class="sxs-lookup"><span data-stu-id="e43c4-114">Consider using ADF:</span></span>

* <span data-ttu-id="e43c4-115">Wanneer de gegevens moeten voortdurend worden gemigreerd in een hybride scenario die toegang heeft tot zowel on-premises en cloudresources</span><span class="sxs-lookup"><span data-stu-id="e43c4-115">when data needs to be continually migrated in a hybrid scenario that accesses both on-premises and cloud resources</span></span>
* <span data-ttu-id="e43c4-116">Wanneer de gegevens is transactionele of moet worden gewijzigd of dat er zakelijke logica toegevoegd wanneer wordt gemigreerd.</span><span class="sxs-lookup"><span data-stu-id="e43c4-116">when the data is transacted or needs to be modified or have business logic added to it when being migrated.</span></span>

<span data-ttu-id="e43c4-117">ADF kunt u de planning en bewaking van taken met behulp van eenvoudige JSON-scripts die de verplaatsing van gegevens op periodieke basis beheren.</span><span class="sxs-lookup"><span data-stu-id="e43c4-117">ADF allows for the scheduling and monitoring of jobs using simple JSON scripts that manage the movement of data on a periodic basis.</span></span> <span data-ttu-id="e43c4-118">ADF heeft ook andere mogelijkheden, zoals ondersteuning voor complexe bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="e43c4-118">ADF also has other capabilities such as support for complex operations.</span></span> <span data-ttu-id="e43c4-119">Zie de documentatie op voor meer informatie over ADF [Azure Data Factory (ADF)](https://azure.microsoft.com/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="e43c4-119">For more information on ADF, see the documentation at [Azure Data Factory (ADF)](https://azure.microsoft.com/services/data-factory/).</span></span>

## <span data-ttu-id="e43c4-120"><a name="scenario"></a>Het Scenario</span><span class="sxs-lookup"><span data-stu-id="e43c4-120"><a name="scenario"></a>The Scenario</span></span>
<span data-ttu-id="e43c4-121">We instellen een ADF-pijplijn die de activiteiten van de migratie twee gegevens stelt het bericht.</span><span class="sxs-lookup"><span data-stu-id="e43c4-121">We set up an ADF pipeline that composes two data migration activities.</span></span> <span data-ttu-id="e43c4-122">Samen wordt gegevens dagelijks verplaatsen tussen een lokale SQL-database en een Azure SQL Database in de cloud.</span><span class="sxs-lookup"><span data-stu-id="e43c4-122">Together they move data on a daily basis between an on-premises SQL database and an Azure SQL Database in the cloud.</span></span> <span data-ttu-id="e43c4-123">Er zijn twee activiteiten:</span><span class="sxs-lookup"><span data-stu-id="e43c4-123">The two activities are:</span></span>

* <span data-ttu-id="e43c4-124">gegevens kopiëren van een on-premises SQL Server database naar een Azure Blob Storage-account</span><span class="sxs-lookup"><span data-stu-id="e43c4-124">copy data from an on-premises SQL Server database to an Azure Blob Storage account</span></span>
* <span data-ttu-id="e43c4-125">gegevens kopiëren van de Azure Blob Storage-account naar een Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="e43c4-125">copy data from the Azure Blob Storage account to an Azure SQL Database.</span></span>

> [!NOTE]
> <span data-ttu-id="e43c4-126">De stappen die hier zijn aangepast uit de meer gedetailleerde zelfstudie geleverd door de ADF-team weergegeven: [gegevens verplaatsen tussen lokale bronnen en cloud met Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md) verwijzingen naar de relevante secties in dat onderwerp zijn opgegeven indien van toepassing.</span><span class="sxs-lookup"><span data-stu-id="e43c4-126">The steps shown here have been adapted from the more detailed tutorial provided by the ADF team: [Move data between on-premises sources and cloud with Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md) References to the relevant sections of that topic are provided when appropriate.</span></span>
>
>

## <span data-ttu-id="e43c4-127"><a name="prereqs"></a>Vereisten</span><span class="sxs-lookup"><span data-stu-id="e43c4-127"><a name="prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="e43c4-128">Deze zelfstudie wordt ervan uitgegaan dat u hebt:</span><span class="sxs-lookup"><span data-stu-id="e43c4-128">This tutorial assumes you have:</span></span>

* <span data-ttu-id="e43c4-129">Een **Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="e43c4-129">An **Azure subscription**.</span></span> <span data-ttu-id="e43c4-130">Als u geen abonnement hebt, kunt u zich aanmelden voor een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e43c4-130">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="e43c4-131">Een **Azure storage-account**.</span><span class="sxs-lookup"><span data-stu-id="e43c4-131">An **Azure storage account**.</span></span> <span data-ttu-id="e43c4-132">U kunt een Azure storage-account gebruiken voor het opslaan van de gegevens in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="e43c4-132">You use an Azure storage account for storing the data in this tutorial.</span></span> <span data-ttu-id="e43c4-133">Zie het artikel [Een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account) als u geen account Azure-opslagaccount hebt.</span><span class="sxs-lookup"><span data-stu-id="e43c4-133">If you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article.</span></span> <span data-ttu-id="e43c4-134">Nadat u het opslagaccount hebt gemaakt, moet u de accountsleutel ophalen die wordt gebruikt voor toegang tot de opslag.</span><span class="sxs-lookup"><span data-stu-id="e43c4-134">After you have created the storage account, you need to obtain the account key used to access the storage.</span></span> <span data-ttu-id="e43c4-135">Zie [beheren van uw toegangssleutels voor opslag](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="e43c4-135">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>
* <span data-ttu-id="e43c4-136">Toegang tot een **Azure SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="e43c4-136">Access to an **Azure SQL Database**.</span></span> <span data-ttu-id="e43c4-137">Als u een Azure SQL Database, de tpoic moet instellen [aan de slag met Microsoft Azure SQL Database ](../sql-database/sql-database-get-started.md) bevat informatie over het inrichten van een nieuw exemplaar van een Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="e43c4-137">If you must set up an Azure SQL Database, the tpoic [Getting Started with Microsoft Azure SQL Database ](../sql-database/sql-database-get-started.md) provides information on how to provision a new instance of an Azure SQL Database.</span></span>
* <span data-ttu-id="e43c4-138">Geïnstalleerd en geconfigureerd **Azure PowerShell** lokaal.</span><span class="sxs-lookup"><span data-stu-id="e43c4-138">Installed and configured **Azure PowerShell** locally.</span></span> <span data-ttu-id="e43c4-139">Zie voor instructies [installeren en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e43c4-139">For instructions, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

> [!NOTE]
> <span data-ttu-id="e43c4-140">Deze procedure gebruikt u de [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e43c4-140">This procedure uses the [Azure portal](https://portal.azure.com/).</span></span>
>
>

## <span data-ttu-id="e43c4-141"><a name="upload-data"></a>De gegevens uploaden naar uw lokale SQL Server</span><span class="sxs-lookup"><span data-stu-id="e43c4-141"><a name="upload-data"></a> Upload the data to your on-premises SQL Server</span></span>
<span data-ttu-id="e43c4-142">We gebruiken de [NYC Taxi gegevensset](http://chriswhong.com/open-data/foil_nyc_taxi/) ter illustratie van het migratieproces.</span><span class="sxs-lookup"><span data-stu-id="e43c4-142">We use the [NYC Taxi dataset](http://chriswhong.com/open-data/foil_nyc_taxi/) to demonstrate the migration process.</span></span> <span data-ttu-id="e43c4-143">De gegevensset NYC Taxi beschikbaar is, zoals beschreven in deze post, op Azure-blobopslag [NYC Taxi gegevens](http://www.andresmh.com/nyctaxitrips/).</span><span class="sxs-lookup"><span data-stu-id="e43c4-143">The NYC Taxi dataset is available, as noted in that post, on Azure blob storage [NYC Taxi Data](http://www.andresmh.com/nyctaxitrips/).</span></span> <span data-ttu-id="e43c4-144">De gegevens heeft twee bestanden: het bestand trip_data.csv reis details bevat, en het bestand trip_far.csv details van het tarief dat voor elke reis betaald bevat.</span><span class="sxs-lookup"><span data-stu-id="e43c4-144">The data has two files, the trip_data.csv file, which contains trip details, and the  trip_far.csv file, which contains details of the fare paid for each trip.</span></span> <span data-ttu-id="e43c4-145">Een beschrijving van deze bestanden en voorbeelden vindt u in [NYC Taxi reizen gegevensset beschrijving](machine-learning-data-science-process-sql-walkthrough.md#dataset).</span><span class="sxs-lookup"><span data-stu-id="e43c4-145">A sample and description of these files are provided in [NYC Taxi Trips Dataset Description](machine-learning-data-science-process-sql-walkthrough.md#dataset).</span></span>

<span data-ttu-id="e43c4-146">U kunt aanpassen van de procedure die hier worden opgegeven voor een set van uw eigen gegevens of de stappen zoals beschreven met behulp van de NYC Taxi gegevensset.</span><span class="sxs-lookup"><span data-stu-id="e43c4-146">You can either adapt the procedure provided here to a set of your own data or follow the steps as described by using the NYC Taxi dataset.</span></span> <span data-ttu-id="e43c4-147">Als u wilt de gegevensset NYC Taxi uploaden naar uw lokale SQL Server-database, volgt u de procedure beschreven in [gegevens voor bulksgewijs importeren in SQL Server-Database](machine-learning-data-science-process-sql-walkthrough.md#dbload).</span><span class="sxs-lookup"><span data-stu-id="e43c4-147">To upload the NYC Taxi dataset into your on-premises SQL Server database, follow the procedure outlined in [Bulk Import Data into SQL Server Database](machine-learning-data-science-process-sql-walkthrough.md#dbload).</span></span> <span data-ttu-id="e43c4-148">Deze instructies zijn voor een SQL-Server op een virtuele Machine van Azure, maar de procedure voor het uploaden naar de lokale SQL Server is hetzelfde.</span><span class="sxs-lookup"><span data-stu-id="e43c4-148">These instructions are for a SQL Server on an Azure Virtual Machine, but the procedure for uploading to the on-premises SQL Server is the same.</span></span>

## <span data-ttu-id="e43c4-149"><a name="create-adf"></a>Een Azure-Gegevensfactory maken</span><span class="sxs-lookup"><span data-stu-id="e43c4-149"><a name="create-adf"></a> Create an Azure Data Factory</span></span>
<span data-ttu-id="e43c4-150">De instructies voor het maken van een nieuwe Azure Data Factory en een resourcegroep in de [Azure-portal](https://portal.azure.com/) vindt u [maken van een Azure Data Factory](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory).</span><span class="sxs-lookup"><span data-stu-id="e43c4-150">The instructions for creating a new Azure Data Factory and a resource group in the [Azure portal](https://portal.azure.com/) are provided [Create an Azure Data Factory](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory).</span></span> <span data-ttu-id="e43c4-151">Naam van het nieuwe exemplaar van de ADF *adfdsp* en de naam van de resourcegroep gemaakt *adfdsprg*.</span><span class="sxs-lookup"><span data-stu-id="e43c4-151">Name the new ADF instance *adfdsp* and name the resource group created *adfdsprg*.</span></span>

## <a name="install-and-configure-up-the-data-management-gateway"></a><span data-ttu-id="e43c4-152">Installeren en configureren van de Data Management Gateway</span><span class="sxs-lookup"><span data-stu-id="e43c4-152">Install and configure up the Data Management Gateway</span></span>
<span data-ttu-id="e43c4-153">Zodat uw pijplijnen in een Azure data factory werkt met een lokale SQL Server die u wilt toevoegen als een gekoppelde Service aan de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="e43c4-153">To enable your pipelines in an Azure data factory to work with an on-premises SQL Server, you need to add it as a Linked Service to the data factory.</span></span> <span data-ttu-id="e43c4-154">Voor het maken van een gekoppelde Service voor een lokale SQL Server, moet u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="e43c4-154">To create a Linked Service for an on-premises SQL Server, you must:</span></span>

* <span data-ttu-id="e43c4-155">Download en installeer Microsoft Data Management Gateway op de lokale computer.</span><span class="sxs-lookup"><span data-stu-id="e43c4-155">download and install Microsoft Data Management Gateway onto the on-premises computer.</span></span>
* <span data-ttu-id="e43c4-156">Configureer de gekoppelde service voor de lokale gegevensbron om de gateway te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e43c4-156">configure the linked service for the on-premises data source to use the gateway.</span></span>

<span data-ttu-id="e43c4-157">Data Management Gateway serialiseert en deserializes van de bron- en sink-gegevens op de computer waarop deze wordt gehost.</span><span class="sxs-lookup"><span data-stu-id="e43c4-157">The Data Management Gateway serializes and deserializes the source and sink data on the computer where it is hosted.</span></span>

<span data-ttu-id="e43c4-158">Zie voor installatie-instructies en informatie over Data Management Gateway [gegevens verplaatsen tussen lokale bronnen en cloud met Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)</span><span class="sxs-lookup"><span data-stu-id="e43c4-158">For set-up instructions and details on Data Management Gateway, see [Move data between on-premises sources and cloud with Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)</span></span>

## <span data-ttu-id="e43c4-159"><a name="adflinkedservices"></a>Gekoppelde services verbinding maken met de gegevensbronnen maken</span><span class="sxs-lookup"><span data-stu-id="e43c4-159"><a name="adflinkedservices"></a>Create linked services to connect to the data resources</span></span>
<span data-ttu-id="e43c4-160">Een gekoppelde service definieert de informatie die nodig zijn voor Azure Data Factory verbinding maken met een bron van gegevens.</span><span class="sxs-lookup"><span data-stu-id="e43c4-160">A linked service defines the information needed for Azure Data Factory to connect to a data resource.</span></span> <span data-ttu-id="e43c4-161">Stapsgewijze procedures voor het maken van de gekoppelde services is beschikbaar in [gekoppelde services maken](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services).</span><span class="sxs-lookup"><span data-stu-id="e43c4-161">The step-by-step procedure for creating linked services is provided in [Create linked services](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services).</span></span>

<span data-ttu-id="e43c4-162">Er zijn drie bronnen in dit scenario waarvoor de gekoppelde services vereist zijn.</span><span class="sxs-lookup"><span data-stu-id="e43c4-162">We have three resources in this scenario for which linked services are needed.</span></span>

1. [<span data-ttu-id="e43c4-163">Gekoppelde service voor on-premises SQL-Server</span><span class="sxs-lookup"><span data-stu-id="e43c4-163">Linked service for on-premises SQL Server</span></span>](#adf-linked-service-onprem-sql)
2. [<span data-ttu-id="e43c4-164">Gekoppelde service voor Azure Blob-opslag</span><span class="sxs-lookup"><span data-stu-id="e43c4-164">Linked service for Azure Blob Storage</span></span>](#adf-linked-service-blob-store)
3. [<span data-ttu-id="e43c4-165">Gekoppelde service voor Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="e43c4-165">Linked service for Azure SQL database</span></span>](#adf-linked-service-azure-sql)

### <span data-ttu-id="e43c4-166"><a name="adf-linked-service-onprem-sql"></a>Gekoppelde service voor on-premises SQL Server-database</span><span class="sxs-lookup"><span data-stu-id="e43c4-166"><a name="adf-linked-service-onprem-sql"></a>Linked service for on-premises SQL Server database</span></span>
<span data-ttu-id="e43c4-167">De gekoppelde service voor de lokale SQL Server maken:</span><span class="sxs-lookup"><span data-stu-id="e43c4-167">To create the linked service for the on-premises SQL Server:</span></span>

* <span data-ttu-id="e43c4-168">Klik op de **gegevensarchief** in de ADF-startpagina op de klassieke Azure-Portal</span><span class="sxs-lookup"><span data-stu-id="e43c4-168">click the **Data Store** in the ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="e43c4-169">Selecteer **SQL** en voer de *gebruikersnaam* en *wachtwoord* referenties voor de lokale SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e43c4-169">select **SQL** and enter the *username* and *password* credentials for the on-premises SQL Server.</span></span> <span data-ttu-id="e43c4-170">U moet de servernaam als invoeren een **volledig gekwalificeerde servernaam backslash exemplaarnaam (servernaam\exemplaarnaam)**.</span><span class="sxs-lookup"><span data-stu-id="e43c4-170">You need to enter the servername as a **fully qualified servername backslash instance name (servername\instancename)**.</span></span> <span data-ttu-id="e43c4-171">Naam van de gekoppelde service *adfonpremsql*.</span><span class="sxs-lookup"><span data-stu-id="e43c4-171">Name the linked service *adfonpremsql*.</span></span>

### <span data-ttu-id="e43c4-172"><a name="adf-linked-service-blob-store"></a>Gekoppelde service voor Blob</span><span class="sxs-lookup"><span data-stu-id="e43c4-172"><a name="adf-linked-service-blob-store"></a>Linked service for Blob</span></span>
<span data-ttu-id="e43c4-173">De gekoppelde service voor het Azure Blob Storage-account maken:</span><span class="sxs-lookup"><span data-stu-id="e43c4-173">To create the linked service for the Azure Blob Storage account:</span></span>

* <span data-ttu-id="e43c4-174">Klik op de **gegevensarchief** in de ADF-startpagina op de klassieke Azure-Portal</span><span class="sxs-lookup"><span data-stu-id="e43c4-174">click the **Data Store** in the ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="e43c4-175">Selecteer **Azure Storage-Account**</span><span class="sxs-lookup"><span data-stu-id="e43c4-175">select **Azure Storage Account**</span></span>
* <span data-ttu-id="e43c4-176">Voer de naam Azure Blob Storage-account sleutel en de container.</span><span class="sxs-lookup"><span data-stu-id="e43c4-176">enter the Azure Blob Storage account key and container name.</span></span> <span data-ttu-id="e43c4-177">Naam van de gekoppelde Service *adfds*.</span><span class="sxs-lookup"><span data-stu-id="e43c4-177">Name the Linked Service *adfds*.</span></span>

### <span data-ttu-id="e43c4-178"><a name="adf-linked-service-azure-sql"></a>Gekoppelde service voor Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="e43c4-178"><a name="adf-linked-service-azure-sql"></a>Linked service for Azure SQL database</span></span>
<span data-ttu-id="e43c4-179">De gekoppelde service voor de Azure SQL Database maken:</span><span class="sxs-lookup"><span data-stu-id="e43c4-179">To create the linked service for the Azure SQL Database:</span></span>

* <span data-ttu-id="e43c4-180">Klik op de **gegevensarchief** in de ADF-startpagina op de klassieke Azure-Portal</span><span class="sxs-lookup"><span data-stu-id="e43c4-180">click the **Data Store** in the ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="e43c4-181">Selecteer **Azure SQL** en voer de *gebruikersnaam* en *wachtwoord* referenties voor de Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="e43c4-181">select **Azure SQL** and enter the *username* and *password* credentials for the Azure SQL Database.</span></span> <span data-ttu-id="e43c4-182">De *gebruikersnaam* moet worden opgegeven als  *user@servername* .</span><span class="sxs-lookup"><span data-stu-id="e43c4-182">The *username* must be specified as *user@servername*.</span></span>   

## <span data-ttu-id="e43c4-183"><a name="adf-tables"></a>Definieer en tabellen om op te geven over toegang tot de gegevenssets maken</span><span class="sxs-lookup"><span data-stu-id="e43c4-183"><a name="adf-tables"></a>Define and create tables to specify how to access the datasets</span></span>
<span data-ttu-id="e43c4-184">Maak tabellen die de structuur, de locatie en de beschikbaarheid van de gegevenssets met de volgende procedures op basis van scripts opgeven.</span><span class="sxs-lookup"><span data-stu-id="e43c4-184">Create tables that specify the structure, location, and availability of the datasets with the following script-based procedures.</span></span> <span data-ttu-id="e43c4-185">JSON-bestanden worden gebruikt voor het definiëren van de tabellen.</span><span class="sxs-lookup"><span data-stu-id="e43c4-185">JSON files are used to define the tables.</span></span> <span data-ttu-id="e43c4-186">Zie voor meer informatie over de structuur van deze bestanden [gegevenssets](../data-factory/data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="e43c4-186">For more information on the structure of these files, see [Datasets](../data-factory/data-factory-create-datasets.md).</span></span>

> [!NOTE]
> <span data-ttu-id="e43c4-187">U dient te worden uitgevoerd de `Add-AzureAccount` cmdlet voordat u de [nieuw AzureDataFactoryTable](https://msdn.microsoft.com/library/azure/dn835096.aspx) cmdlet om te bevestigen dat het juiste Azure-abonnement is ingeschakeld voor uitvoering van de opdracht.</span><span class="sxs-lookup"><span data-stu-id="e43c4-187">You should execute the `Add-AzureAccount` cmdlet before executing the [New-AzureDataFactoryTable](https://msdn.microsoft.com/library/azure/dn835096.aspx) cmdlet to confirm that the right Azure subscription is selected for the command execution.</span></span> <span data-ttu-id="e43c4-188">Zie voor documentatie van deze cmdlet [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="e43c4-188">For documentation of this cmdlet, see [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0).</span></span>
>
>

<span data-ttu-id="e43c4-189">De definities JSON-indeling in de tabellen gebruiken de volgende namen:</span><span class="sxs-lookup"><span data-stu-id="e43c4-189">The JSON-based definitions in the tables use the following names:</span></span>

* <span data-ttu-id="e43c4-190">de **tabelnaam** in de lokale SQL server is *nyctaxi_data*</span><span class="sxs-lookup"><span data-stu-id="e43c4-190">the **table name** in the on-premises SQL server is *nyctaxi_data*</span></span>
* <span data-ttu-id="e43c4-191">de **containernaam** in Azure Blob Storage-account is *containername*</span><span class="sxs-lookup"><span data-stu-id="e43c4-191">the **container name** in the Azure Blob Storage account is *containername*</span></span>  

<span data-ttu-id="e43c4-192">Drie tabeldefinities nodig zijn voor deze ADF-pijplijn:</span><span class="sxs-lookup"><span data-stu-id="e43c4-192">Three table definitions are needed for this ADF pipeline:</span></span>

1. [<span data-ttu-id="e43c4-193">On-premises SQL-tabel</span><span class="sxs-lookup"><span data-stu-id="e43c4-193">SQL on-premises Table</span></span>](#adf-table-onprem-sql)
2. [<span data-ttu-id="e43c4-194">Blobtabel</span><span class="sxs-lookup"><span data-stu-id="e43c4-194">Blob Table </span></span>](#adf-table-blob-store)
3. [<span data-ttu-id="e43c4-195">SQL Azure-tabel</span><span class="sxs-lookup"><span data-stu-id="e43c4-195">SQL Azure Table</span></span>](#adf-table-azure-sql)

> [!NOTE]
> <span data-ttu-id="e43c4-196">Deze procedures Azure PowerShell gebruiken om te definiëren en te maken van de ADF-activiteiten.</span><span class="sxs-lookup"><span data-stu-id="e43c4-196">These procedures use Azure PowerShell to define and create the ADF activities.</span></span> <span data-ttu-id="e43c4-197">Maar deze taken kunnen ook worden bereikt met de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e43c4-197">But these tasks can also be accomplished using the Azure portal.</span></span> <span data-ttu-id="e43c4-198">Zie voor meer informatie [gegevenssets maken](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets).</span><span class="sxs-lookup"><span data-stu-id="e43c4-198">For details, see [Create datasets](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets).</span></span>
>
>

### <span data-ttu-id="e43c4-199"><a name="adf-table-onprem-sql"></a>On-premises SQL-tabel</span><span class="sxs-lookup"><span data-stu-id="e43c4-199"><a name="adf-table-onprem-sql"></a>SQL on-premises Table</span></span>
<span data-ttu-id="e43c4-200">De definitie van de tabel voor de lokale SQL Server is opgegeven in het volgende JSON-bestand:</span><span class="sxs-lookup"><span data-stu-id="e43c4-200">The table definition for the on-premises SQL Server is specified in the following JSON file:</span></span>

        {
            "name": "OnPremSQLTable",
            "properties":
            {
                "location":
                {
                "type": "OnPremisesSqlServerTableLocation",
                "tableName": "nyctaxi_data",
                "linkedServiceName": "adfonpremsql"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1,   
                "waitOnExternal":
                {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
                }

                }
            }
        }

<span data-ttu-id="e43c4-201">De kolomnamen zijn hier niet opgenomen.</span><span class="sxs-lookup"><span data-stu-id="e43c4-201">The column names were not included here.</span></span> <span data-ttu-id="e43c4-202">U kunt subplan selecteren op de kolomnamen door ze hier (Raadpleeg voor meer informatie de [ADF documentatie](../data-factory/data-factory-data-movement-activities.md) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="e43c4-202">You can sub-select on the column names by including them here (for details check the [ADF documentation](../data-factory/data-factory-data-movement-activities.md) topic.</span></span>

<span data-ttu-id="e43c4-203">Naam van de JSON-definitie van de tabel in een bestand kopiëren *onpremtabledef.json* -bestand en sla deze op een bekende locatie (hier ervan uitgegaan dat de *C:\temp\onpremtabledef.json*).</span><span class="sxs-lookup"><span data-stu-id="e43c4-203">Copy the JSON definition of the table into a file called *onpremtabledef.json* file and save it to a known location (here assumed to be *C:\temp\onpremtabledef.json*).</span></span> <span data-ttu-id="e43c4-204">De tabel in ADF maken met de volgende Azure PowerShell-cmdlet:</span><span class="sxs-lookup"><span data-stu-id="e43c4-204">Create the table in ADF with the following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp –File C:\temp\onpremtabledef.json


### <span data-ttu-id="e43c4-205"><a name="adf-table-blob-store"></a>Blobtabel</span><span class="sxs-lookup"><span data-stu-id="e43c4-205"><a name="adf-table-blob-store"></a>Blob Table</span></span>
<span data-ttu-id="e43c4-206">De definitie voor de tabel voor de locatie van de uitvoer-blob is in de volgende (Hiermee worden de opgenomen gegevens van on-premises naar Azure blob):</span><span class="sxs-lookup"><span data-stu-id="e43c4-206">Definition for the table for the output blob location is in the following (this maps the ingested data from on-premises to Azure blob):</span></span>

        {
            "name": "OutputBlobTable",
            "properties":
            {
                "location":
                {
                "type": "AzureBlobLocation",
                "folderPath": "containername",
                "format":
                {
                "type": "TextFormat",
                "columnDelimiter": "\t"
                },
                "linkedServiceName": "adfds"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1
                }
            }
        }

<span data-ttu-id="e43c4-207">Naam van de JSON-definitie van de tabel in een bestand kopiëren *bloboutputtabledef.json* -bestand en sla deze op een bekende locatie (hier ervan uitgegaan dat de *C:\temp\bloboutputtabledef.json*).</span><span class="sxs-lookup"><span data-stu-id="e43c4-207">Copy the JSON definition of the table into a file called *bloboutputtabledef.json* file and save it to a known location (here assumed to be *C:\temp\bloboutputtabledef.json*).</span></span> <span data-ttu-id="e43c4-208">De tabel in ADF maken met de volgende Azure PowerShell-cmdlet:</span><span class="sxs-lookup"><span data-stu-id="e43c4-208">Create the table in ADF with the following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\bloboutputtabledef.json  

### <span data-ttu-id="e43c4-209"><a name="adf-table-azure-sq"></a>SQL Azure-tabel</span><span class="sxs-lookup"><span data-stu-id="e43c4-209"><a name="adf-table-azure-sq"></a>SQL Azure Table</span></span>
<span data-ttu-id="e43c4-210">Definitie voor de tabel voor de SQL Azure-uitvoer is in de volgende (de gegevens die afkomstig zijn van de blob dit schema toegewezen):</span><span class="sxs-lookup"><span data-stu-id="e43c4-210">Definition for the table for the SQL Azure output is in the following (this schema maps the data coming from the blob):</span></span>

    {
        "name": "OutputSQLAzureTable",
        "properties":
        {
            "structure":
            [
                { "name": "column1", type": "String"},
                { "name": "column2", type": "String"}                
            ],
            "location":
            {
                "type": "AzureSqlTableLocation",
                "tableName": "your_db_name",
                "linkedServiceName": "adfdssqlazure_linked_servicename"
            },
            "availability":
            {
                "frequency": "Day",
                "interval": 1            
            }
        }
    }

<span data-ttu-id="e43c4-211">Naam van de JSON-definitie van de tabel in een bestand kopiëren *AzureSqlTable.json* -bestand en sla deze op een bekende locatie (hier ervan uitgegaan dat de *C:\temp\AzureSqlTable.json*).</span><span class="sxs-lookup"><span data-stu-id="e43c4-211">Copy the JSON definition of the table into a file called *AzureSqlTable.json* file and save it to a known location (here assumed to be *C:\temp\AzureSqlTable.json*).</span></span> <span data-ttu-id="e43c4-212">De tabel in ADF maken met de volgende Azure PowerShell-cmdlet:</span><span class="sxs-lookup"><span data-stu-id="e43c4-212">Create the table in ADF with the following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\AzureSqlTable.json  


## <span data-ttu-id="e43c4-213"><a name="adf-pipeline"></a>Definiëren en de pijplijn maken</span><span class="sxs-lookup"><span data-stu-id="e43c4-213"><a name="adf-pipeline"></a>Define and create the pipeline</span></span>
<span data-ttu-id="e43c4-214">Geef de activiteiten die behoren tot de pijplijn en de pijplijn maken met de volgende procedures op basis van scripts.</span><span class="sxs-lookup"><span data-stu-id="e43c4-214">Specify the activities that belong to the pipeline and create the pipeline with the following script-based procedures.</span></span> <span data-ttu-id="e43c4-215">Een JSON-bestand wordt gebruikt voor het definiëren van de pipeline-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="e43c4-215">A JSON file is used to define the pipeline properties.</span></span>

* <span data-ttu-id="e43c4-216">Het script wordt ervan uitgegaan dat de **pijplijn naam** is *AMLDSProcessPipeline*.</span><span class="sxs-lookup"><span data-stu-id="e43c4-216">The script assumes that the **pipeline name** is *AMLDSProcessPipeline*.</span></span>
* <span data-ttu-id="e43c4-217">Houd er ook rekening mee dat we de periodiciteit van de pijplijn worden dagelijks uitgevoerd en de uitvoeringstijd van de standaard gebruiken voor de taak (12: 00 a.m. UTC) ingesteld.</span><span class="sxs-lookup"><span data-stu-id="e43c4-217">Also note that we set the periodicity of the pipeline to be executed on daily basis and use the default execution time for the job (12 am UTC).</span></span>

> [!NOTE]
> <span data-ttu-id="e43c4-218">Azure PowerShell de volgende procedures gebruiken om te definiëren en te maken van de ADF-pijplijn.</span><span class="sxs-lookup"><span data-stu-id="e43c4-218">The following procedures use Azure PowerShell to define and create the ADF pipeline.</span></span> <span data-ttu-id="e43c4-219">Maar deze taak kan ook worden bereikt met de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e43c4-219">But this task can also be accomplished using the Azure portal.</span></span> <span data-ttu-id="e43c4-220">Zie voor meer informatie [maken pijplijn](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline).</span><span class="sxs-lookup"><span data-stu-id="e43c4-220">For details, see [Create pipeline](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline).</span></span>
>
>

<span data-ttu-id="e43c4-221">Met behulp van de tabeldefinities eerder hebt opgegeven, wordt de definitie van de pijplijn voor de ADF als volgt opgegeven:</span><span class="sxs-lookup"><span data-stu-id="e43c4-221">Using the table definitions provided previously, the pipeline definition for the ADF is specified as follows:</span></span>

        {
            "name": "AMLDSProcessPipeline",
            "properties":
            {
                "description" : "This pipeline has one Copy activity that copies data from an on-premises SQL to Azure blob",
                 "activities":
                [
                    {
                        "name": "CopyFromSQLtoBlob",
                        "description": "Copy data from on-premises SQL server to blob",     
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OnPremSQLTable"} ],
                        "outputs": [ {"name": "OutputBlobTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "SqlSource",
                                "sqlReaderQuery": "select * from nyctaxi_data"
                            },
                            "sink":
                            {
                                "type": "BlobSink"
                            }   
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 0,
                            "timeout": "01:00:00"
                        }       

                     },

                    {
                        "name": "CopyFromBlobtoSQLAzure",
                        "description": "Push data to Sql Azure",        
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OutputBlobTable"} ],
                        "outputs": [ {"name": "OutputSQLAzureTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "BlobSource"
                            },
                            "sink":
                            {
                                "type": "SqlSink",
                                "WriteBatchTimeout": "00:5:00",                
                            }            
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 2,
                            "timeout": "02:00:00"
                        }
                     }
                ]
            }
        }

<span data-ttu-id="e43c4-222">Kopieer deze JSON-definitie van de pijplijn in een bestand genaamd *pipelinedef.json* -bestand en sla deze op een bekende locatie (hier ervan uitgegaan dat de *C:\temp\pipelinedef.json*).</span><span class="sxs-lookup"><span data-stu-id="e43c4-222">Copy this JSON definition of the pipeline into a file called *pipelinedef.json* file and save it to a known location (here assumed to be *C:\temp\pipelinedef.json*).</span></span> <span data-ttu-id="e43c4-223">De pijplijn in ADF maken met de volgende Azure PowerShell-cmdlet:</span><span class="sxs-lookup"><span data-stu-id="e43c4-223">Create the pipeline in ADF with the following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryPipeline  -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\pipelinedef.json

<span data-ttu-id="e43c4-224">Controleer of u kunt de pijplijn in de ADF in de klassieke Azure-Portal weergegeven als de volgende (wanneer u klikt op het diagram)</span><span class="sxs-lookup"><span data-stu-id="e43c4-224">Confirm that you can see the pipeline on the ADF in the Azure Classic Portal show up as following (when you click the diagram)</span></span>

![ADF-pipeline](media/machine-learning-data-science-move-sql-azure-adf/DJP1kji.png)

## <span data-ttu-id="e43c4-226"><a name="adf-pipeline-start"></a>Start de pijplijn</span><span class="sxs-lookup"><span data-stu-id="e43c4-226"><a name="adf-pipeline-start"></a>Start the Pipeline</span></span>
<span data-ttu-id="e43c4-227">De pijplijn kan nu worden uitgevoerd met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="e43c4-227">The pipeline can now be run using the following command:</span></span>

    Set-AzureDataFactoryPipelineActivePeriod -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp -StartDateTime startdateZ –EndDateTime enddateZ –Name AMLDSProcessPipeline

<span data-ttu-id="e43c4-228">De *startdate* en *enddate* parameterwaarden moeten worden vervangen door de werkelijke datums tussen wie u wilt dat de pijplijn om uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="e43c4-228">The *startdate* and *enddate* parameter values need to be replaced with the actual dates between which you want the pipeline to run.</span></span>

<span data-ttu-id="e43c4-229">Zodra de pijplijn wordt uitgevoerd, moet u mogelijk zijn om de gegevens weergegeven in de container die is geselecteerd voor de blob, één bestand per dag te bekijken.</span><span class="sxs-lookup"><span data-stu-id="e43c4-229">Once the pipeline executes, you should be able to see the data show up in the container selected for the blob, one file per day.</span></span>

<span data-ttu-id="e43c4-230">Houd er rekening mee dat we hebben de functionaliteit van ADF pipe gegevens stapsgewijs niet gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e43c4-230">Note that we have not leveraged the functionality provided by ADF to pipe data incrementally.</span></span> <span data-ttu-id="e43c4-231">Zie voor meer informatie over hoe u deze en andere mogelijkheden van ADF de [ADF documentatie](https://azure.microsoft.com/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="e43c4-231">For more information on how to do this and other capabilities provided by ADF, see the [ADF documentation](https://azure.microsoft.com/services/data-factory/).</span></span>
