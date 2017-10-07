---
title: aaaMove gegevens uit een lokale SQL Server tooSQL Azure met Azure Data Factory | Microsoft Docs
description: Een ADF-pijplijn die twee activiteiten van de gegevens migreren die gegevens samen dagelijks tussen databases on-premises en in de cloud Hallo verplaatsen stelt het bericht instellen.
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
ms.openlocfilehash: 7f7e78c7a84a259539221d3235b76bb5a3cf9866
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-on-premises-sql-server-toosql-azure-with-azure-data-factory"></a><span data-ttu-id="a4a80-103">Gegevens verplaatsen van een lokale SQL server tooSQL Azure met Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a4a80-103">Move data from an on-premises SQL server tooSQL Azure with Azure Data Factory</span></span>
<span data-ttu-id="a4a80-104">Dit onderwerp leest hoe toomove gegevens uit een lokale SQL Server-Database tooa SQL Azure Database via Azure Blob Storage met behulp van Azure Data Factory (ADF) Hallo.</span><span class="sxs-lookup"><span data-stu-id="a4a80-104">This topic shows how toomove data from an on-premises SQL Server Database tooa SQL Azure Database via Azure Blob Storage using hello Azure Data Factory (ADF).</span></span>

<span data-ttu-id="a4a80-105">Zie voor een tabel die een overzicht van de verschillende opties voor verplaatsen gegevens tooan Azure SQL Database, [verplaatsen van gegevens tooan Azure SQL Database voor Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span><span class="sxs-lookup"><span data-stu-id="a4a80-105">For a table that summarizes various options for moving data tooan Azure SQL Database, see [Move data tooan Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span></span>

## <span data-ttu-id="a4a80-106"><a name="intro"></a>Inleiding: Wat is er ADF en wanneer moet het gebruikte toomigrate gegevens?</span><span class="sxs-lookup"><span data-stu-id="a4a80-106"><a name="intro"></a>Introduction: What is ADF and when should it be used toomigrate data?</span></span>
<span data-ttu-id="a4a80-107">Azure Data Factory is een volledig beheerde gegevens cloud-gebaseerde integration-service die is ingedeeld en automatiseert Hallo verplaatsing en transformatie van gegevens.</span><span class="sxs-lookup"><span data-stu-id="a4a80-107">Azure Data Factory is a fully managed cloud-based data integration service that orchestrates and automates hello movement and transformation of data.</span></span> <span data-ttu-id="a4a80-108">Hallo sleutel concept in Hallo ADF model is pijplijn.</span><span class="sxs-lookup"><span data-stu-id="a4a80-108">hello key concept in hello ADF model is pipeline.</span></span> <span data-ttu-id="a4a80-109">Een pijplijn is een logische groepering van activiteiten, die elk Hallo acties tooperform op Hallo gegevens in de gegevenssets definieert.</span><span class="sxs-lookup"><span data-stu-id="a4a80-109">A pipeline is a logical grouping of Activities, each of which defines hello actions tooperform on hello data contained in Datasets.</span></span> <span data-ttu-id="a4a80-110">Gekoppelde services zijn gebruikte toodefine Hallo informatie die nodig is voor de gegevensbronnen voor Data Factory tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="a4a80-110">Linked services are used toodefine hello information needed for Data Factory tooconnect toohello data resources.</span></span>

<span data-ttu-id="a4a80-111">Met ADF, bestaande services voor gegevensverwerking in gegevenspijplijnen die maximaal beschikbaar en wordt beheerd in de cloud Hallo samengesteld.</span><span class="sxs-lookup"><span data-stu-id="a4a80-111">With ADF, existing data processing services can be composed into data pipelines that are highly available and managed in hello cloud.</span></span> <span data-ttu-id="a4a80-112">Deze gegevenspijplijnen kunnen worden geplande tooingest, voorbereiden, transformeren, analyseren en gegevens publiceren en ADF beheert en stuurt Hallo complexe gegevens en afhankelijkheden voor verwerking.</span><span class="sxs-lookup"><span data-stu-id="a4a80-112">These data pipelines can be scheduled tooingest, prepare, transform, analyze, and publish data, and ADF manages and orchestrates hello complex data and processing dependencies.</span></span> <span data-ttu-id="a4a80-113">Oplossingen worden snel gebouwd en geïmplementeerde in Hallo cloud, verbinding maken met een toenemend aantal lokale en cloud-gegevensbronnen.</span><span class="sxs-lookup"><span data-stu-id="a4a80-113">Solutions can be quickly built and deployed in hello cloud, connecting a growing number of on-premises and cloud data sources.</span></span>

<span data-ttu-id="a4a80-114">Overweeg het gebruik van ADF:</span><span class="sxs-lookup"><span data-stu-id="a4a80-114">Consider using ADF:</span></span>

* <span data-ttu-id="a4a80-115">Wanneer gegevens die behoeften toobe voortdurend gemigreerd in een hybride scenario die toegang heeft tot zowel on-premises en cloudresources</span><span class="sxs-lookup"><span data-stu-id="a4a80-115">when data needs toobe continually migrated in a hybrid scenario that accesses both on-premises and cloud resources</span></span>
* <span data-ttu-id="a4a80-116">Wanneer gegevens Hallo is transactionele of behoeften toobe gewijzigd of bedrijfslogica toegevoegd tooit wanneer wordt gemigreerd.</span><span class="sxs-lookup"><span data-stu-id="a4a80-116">when hello data is transacted or needs toobe modified or have business logic added tooit when being migrated.</span></span>

<span data-ttu-id="a4a80-117">ADF kunt Hallo planning en bewaking van taken met behulp van eenvoudige JSON-scripts die Hallo verplaatsing van gegevens op periodieke basis beheren.</span><span class="sxs-lookup"><span data-stu-id="a4a80-117">ADF allows for hello scheduling and monitoring of jobs using simple JSON scripts that manage hello movement of data on a periodic basis.</span></span> <span data-ttu-id="a4a80-118">ADF heeft ook andere mogelijkheden, zoals ondersteuning voor complexe bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="a4a80-118">ADF also has other capabilities such as support for complex operations.</span></span> <span data-ttu-id="a4a80-119">Zie voor meer informatie over ADF Hallo-documentatie op [Azure Data Factory (ADF)](https://azure.microsoft.com/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="a4a80-119">For more information on ADF, see hello documentation at [Azure Data Factory (ADF)](https://azure.microsoft.com/services/data-factory/).</span></span>

## <span data-ttu-id="a4a80-120"><a name="scenario"></a>Hallo Scenario</span><span class="sxs-lookup"><span data-stu-id="a4a80-120"><a name="scenario"></a>hello Scenario</span></span>
<span data-ttu-id="a4a80-121">We instellen een ADF-pijplijn die de activiteiten van de migratie twee gegevens stelt het bericht.</span><span class="sxs-lookup"><span data-stu-id="a4a80-121">We set up an ADF pipeline that composes two data migration activities.</span></span> <span data-ttu-id="a4a80-122">Samen wordt gegevens dagelijks verplaatsen tussen een lokale SQL-database en een Azure SQL Database in de cloud Hallo.</span><span class="sxs-lookup"><span data-stu-id="a4a80-122">Together they move data on a daily basis between an on-premises SQL database and an Azure SQL Database in hello cloud.</span></span> <span data-ttu-id="a4a80-123">Hallo twee activiteiten zijn:</span><span class="sxs-lookup"><span data-stu-id="a4a80-123">hello two activities are:</span></span>

* <span data-ttu-id="a4a80-124">gegevens kopiëren van een lokale SQL Server-database tooan Azure Blob Storage-account</span><span class="sxs-lookup"><span data-stu-id="a4a80-124">copy data from an on-premises SQL Server database tooan Azure Blob Storage account</span></span>
* <span data-ttu-id="a4a80-125">gegevens kopiëren van hello Azure Blob Storage-account tooan Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="a4a80-125">copy data from hello Azure Blob Storage account tooan Azure SQL Database.</span></span>

> [!NOTE]
> <span data-ttu-id="a4a80-126">stappen die hier zijn aangepast van Hallo meer zelfstudie geleverd door Hallo ADF-team gedetailleerde weergegeven Hallo: [gegevens verplaatsen tussen lokale bronnen en cloud met Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md) toohello relevante secties van dit onderwerp verwijst naar Als het nodig zijn worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="a4a80-126">hello steps shown here have been adapted from hello more detailed tutorial provided by hello ADF team: [Move data between on-premises sources and cloud with Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md) References toohello relevant sections of that topic are provided when appropriate.</span></span>
>
>

## <span data-ttu-id="a4a80-127"><a name="prereqs"></a>Vereisten</span><span class="sxs-lookup"><span data-stu-id="a4a80-127"><a name="prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="a4a80-128">Deze zelfstudie wordt ervan uitgegaan dat u hebt:</span><span class="sxs-lookup"><span data-stu-id="a4a80-128">This tutorial assumes you have:</span></span>

* <span data-ttu-id="a4a80-129">Een **Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="a4a80-129">An **Azure subscription**.</span></span> <span data-ttu-id="a4a80-130">Als u geen abonnement hebt, kunt u zich aanmelden voor een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a4a80-130">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="a4a80-131">Een **Azure storage-account**.</span><span class="sxs-lookup"><span data-stu-id="a4a80-131">An **Azure storage account**.</span></span> <span data-ttu-id="a4a80-132">U kunt een Azure storage-account gebruiken voor het opslaan van Hallo gegevens in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="a4a80-132">You use an Azure storage account for storing hello data in this tutorial.</span></span> <span data-ttu-id="a4a80-133">Als u geen Azure storage-account hebt, raadpleegt u Hallo [een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account) artikel.</span><span class="sxs-lookup"><span data-stu-id="a4a80-133">If you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article.</span></span> <span data-ttu-id="a4a80-134">Nadat u Hallo storage-account hebt gemaakt, moet u tooobtain Hallo account sleutel tooaccess Hallo opslagruimte hebt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a4a80-134">After you have created hello storage account, you need tooobtain hello account key used tooaccess hello storage.</span></span> <span data-ttu-id="a4a80-135">Zie [beheren van uw toegangssleutels voor opslag](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="a4a80-135">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>
* <span data-ttu-id="a4a80-136">Toegang tooan **Azure SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="a4a80-136">Access tooan **Azure SQL Database**.</span></span> <span data-ttu-id="a4a80-137">Als u een Azure SQL Database, moet Hallo tpoic [aan de slag met Microsoft Azure SQL Database ](../sql-database/sql-database-get-started.md) bevat informatie over het tooprovision een nieuw exemplaar van een Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="a4a80-137">If you must set up an Azure SQL Database, hello tpoic [Getting Started with Microsoft Azure SQL Database ](../sql-database/sql-database-get-started.md) provides information on how tooprovision a new instance of an Azure SQL Database.</span></span>
* <span data-ttu-id="a4a80-138">Geïnstalleerd en geconfigureerd **Azure PowerShell** lokaal.</span><span class="sxs-lookup"><span data-stu-id="a4a80-138">Installed and configured **Azure PowerShell** locally.</span></span> <span data-ttu-id="a4a80-139">Zie voor instructies [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a4a80-139">For instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

> [!NOTE]
> <span data-ttu-id="a4a80-140">Met deze procedure gebruikt Hallo [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a4a80-140">This procedure uses hello [Azure portal](https://portal.azure.com/).</span></span>
>
>

## <span data-ttu-id="a4a80-141"><a name="upload-data"></a>Het uploaden van Hallo gegevens tooyour lokale SQL Server</span><span class="sxs-lookup"><span data-stu-id="a4a80-141"><a name="upload-data"></a> Upload hello data tooyour on-premises SQL Server</span></span>
<span data-ttu-id="a4a80-142">We gebruiken Hallo [NYC Taxi gegevensset](http://chriswhong.com/open-data/foil_nyc_taxi/) toodemonstrate Hallo-migratieproces.</span><span class="sxs-lookup"><span data-stu-id="a4a80-142">We use hello [NYC Taxi dataset](http://chriswhong.com/open-data/foil_nyc_taxi/) toodemonstrate hello migration process.</span></span> <span data-ttu-id="a4a80-143">Hallo NYC Taxi gegevensset beschikbaar is, zoals beschreven in deze post, op Azure-blobopslag [NYC Taxi gegevens](http://www.andresmh.com/nyctaxitrips/).</span><span class="sxs-lookup"><span data-stu-id="a4a80-143">hello NYC Taxi dataset is available, as noted in that post, on Azure blob storage [NYC Taxi Data](http://www.andresmh.com/nyctaxitrips/).</span></span> <span data-ttu-id="a4a80-144">Hallo gegevens heeft twee bestanden, Hallo trip_data.csv bestand, dat reis details bevat, en Hallo trip_far.csv bestand, met details over Hallo tarief voor elke reis betaald.</span><span class="sxs-lookup"><span data-stu-id="a4a80-144">hello data has two files, hello trip_data.csv file, which contains trip details, and hello  trip_far.csv file, which contains details of hello fare paid for each trip.</span></span> <span data-ttu-id="a4a80-145">Een beschrijving van deze bestanden en voorbeelden vindt u in [NYC Taxi reizen gegevensset beschrijving](machine-learning-data-science-process-sql-walkthrough.md#dataset).</span><span class="sxs-lookup"><span data-stu-id="a4a80-145">A sample and description of these files are provided in [NYC Taxi Trips Dataset Description](machine-learning-data-science-process-sql-walkthrough.md#dataset).</span></span>

<span data-ttu-id="a4a80-146">Hallo-procedure die hier tooa set van uw eigen gegevens aanpassen of Hallo stappen zoals beschreven met behulp van Hallo NYC Taxi gegevensset.</span><span class="sxs-lookup"><span data-stu-id="a4a80-146">You can either adapt hello procedure provided here tooa set of your own data or follow hello steps as described by using hello NYC Taxi dataset.</span></span> <span data-ttu-id="a4a80-147">tooupload hello NYC Taxi gegevensset in uw lokale SQL Server-database, volgt u Hallo procedure beschreven in [gegevens voor bulksgewijs importeren in SQL Server-Database](machine-learning-data-science-process-sql-walkthrough.md#dbload).</span><span class="sxs-lookup"><span data-stu-id="a4a80-147">tooupload hello NYC Taxi dataset into your on-premises SQL Server database, follow hello procedure outlined in [Bulk Import Data into SQL Server Database](machine-learning-data-science-process-sql-walkthrough.md#dbload).</span></span> <span data-ttu-id="a4a80-148">Deze instructies zijn voor een SQL-Server op een virtuele Machine van Azure, maar de procedure voor het uploaden van de lokale SQL Server is toohello Hallo Hallo dezelfde.</span><span class="sxs-lookup"><span data-stu-id="a4a80-148">These instructions are for a SQL Server on an Azure Virtual Machine, but hello procedure for uploading toohello on-premises SQL Server is hello same.</span></span>

## <span data-ttu-id="a4a80-149"><a name="create-adf"></a>Een Azure-Gegevensfactory maken</span><span class="sxs-lookup"><span data-stu-id="a4a80-149"><a name="create-adf"></a> Create an Azure Data Factory</span></span>
<span data-ttu-id="a4a80-150">instructies voor het maken van een nieuwe Azure Data Factory en een resourcegroep in Hallo Hallo [Azure-portal](https://portal.azure.com/) vindt u [maken van een Azure Data Factory](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory).</span><span class="sxs-lookup"><span data-stu-id="a4a80-150">hello instructions for creating a new Azure Data Factory and a resource group in hello [Azure portal](https://portal.azure.com/) are provided [Create an Azure Data Factory](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory).</span></span> <span data-ttu-id="a4a80-151">Naam Hallo nieuw ADF exemplaar *adfdsp* en naam Hallo-resourcegroep gemaakt *adfdsprg*.</span><span class="sxs-lookup"><span data-stu-id="a4a80-151">Name hello new ADF instance *adfdsp* and name hello resource group created *adfdsprg*.</span></span>

## <a name="install-and-configure-up-hello-data-management-gateway"></a><span data-ttu-id="a4a80-152">Installeren en configureren van Hallo Data Management Gateway</span><span class="sxs-lookup"><span data-stu-id="a4a80-152">Install and configure up hello Data Management Gateway</span></span>
<span data-ttu-id="a4a80-153">tooenable uw pijplijnen in een Azure data factory-toowork met een lokale SQL Server, moet u tooadd als een gekoppelde Service toohello data factory.</span><span class="sxs-lookup"><span data-stu-id="a4a80-153">tooenable your pipelines in an Azure data factory toowork with an on-premises SQL Server, you need tooadd it as a Linked Service toohello data factory.</span></span> <span data-ttu-id="a4a80-154">toocreate een gekoppelde Service voor een lokale SQL Server, moet u:</span><span class="sxs-lookup"><span data-stu-id="a4a80-154">toocreate a Linked Service for an on-premises SQL Server, you must:</span></span>

* <span data-ttu-id="a4a80-155">Download en installeer Microsoft Data Management Gateway op Hallo lokale computer.</span><span class="sxs-lookup"><span data-stu-id="a4a80-155">download and install Microsoft Data Management Gateway onto hello on-premises computer.</span></span>
* <span data-ttu-id="a4a80-156">Hallo gekoppelde service voor Hallo lokale bron toouse Hallo gegevensgateway configureren.</span><span class="sxs-lookup"><span data-stu-id="a4a80-156">configure hello linked service for hello on-premises data source toouse hello gateway.</span></span>

<span data-ttu-id="a4a80-157">Hallo Data Management Gateway serialiseert en deserializes Hallo bron- en sink-gegevens op Hallo-computer waarop deze wordt gehost.</span><span class="sxs-lookup"><span data-stu-id="a4a80-157">hello Data Management Gateway serializes and deserializes hello source and sink data on hello computer where it is hosted.</span></span>

<span data-ttu-id="a4a80-158">Zie voor installatie-instructies en informatie over Data Management Gateway [gegevens verplaatsen tussen lokale bronnen en cloud met Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)</span><span class="sxs-lookup"><span data-stu-id="a4a80-158">For set-up instructions and details on Data Management Gateway, see [Move data between on-premises sources and cloud with Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)</span></span>

## <span data-ttu-id="a4a80-159"><a name="adflinkedservices"></a>Gekoppelde services tooconnect toohello gegevens resources maken</span><span class="sxs-lookup"><span data-stu-id="a4a80-159"><a name="adflinkedservices"></a>Create linked services tooconnect toohello data resources</span></span>
<span data-ttu-id="a4a80-160">Een gekoppelde service definieert Hallo-informatie die nodig is voor Azure Data Factory tooconnect tooa Gegevensresource.</span><span class="sxs-lookup"><span data-stu-id="a4a80-160">A linked service defines hello information needed for Azure Data Factory tooconnect tooa data resource.</span></span> <span data-ttu-id="a4a80-161">Hallo Stapsgewijze instructies voor het maken van de gekoppelde services is beschikbaar in [gekoppelde services maken](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services).</span><span class="sxs-lookup"><span data-stu-id="a4a80-161">hello step-by-step procedure for creating linked services is provided in [Create linked services](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services).</span></span>

<span data-ttu-id="a4a80-162">Er zijn drie bronnen in dit scenario waarvoor de gekoppelde services vereist zijn.</span><span class="sxs-lookup"><span data-stu-id="a4a80-162">We have three resources in this scenario for which linked services are needed.</span></span>

1. [<span data-ttu-id="a4a80-163">Gekoppelde service voor on-premises SQL-Server</span><span class="sxs-lookup"><span data-stu-id="a4a80-163">Linked service for on-premises SQL Server</span></span>](#adf-linked-service-onprem-sql)
2. [<span data-ttu-id="a4a80-164">Gekoppelde service voor Azure Blob-opslag</span><span class="sxs-lookup"><span data-stu-id="a4a80-164">Linked service for Azure Blob Storage</span></span>](#adf-linked-service-blob-store)
3. [<span data-ttu-id="a4a80-165">Gekoppelde service voor Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="a4a80-165">Linked service for Azure SQL database</span></span>](#adf-linked-service-azure-sql)

### <span data-ttu-id="a4a80-166"><a name="adf-linked-service-onprem-sql"></a>Gekoppelde service voor on-premises SQL Server-database</span><span class="sxs-lookup"><span data-stu-id="a4a80-166"><a name="adf-linked-service-onprem-sql"></a>Linked service for on-premises SQL Server database</span></span>
<span data-ttu-id="a4a80-167">toocreate hello gekoppelde service voor Hallo lokale SQL Server:</span><span class="sxs-lookup"><span data-stu-id="a4a80-167">toocreate hello linked service for hello on-premises SQL Server:</span></span>

* <span data-ttu-id="a4a80-168">Klik op Hallo **gegevensarchief** in Hallo ADF-startpagina op de klassieke Azure-Portal</span><span class="sxs-lookup"><span data-stu-id="a4a80-168">click hello **Data Store** in hello ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="a4a80-169">Selecteer **SQL** en Voer Hallo *gebruikersnaam* en *wachtwoord* voor Hallo on-premises SQL Server-referenties.</span><span class="sxs-lookup"><span data-stu-id="a4a80-169">select **SQL** and enter hello *username* and *password* credentials for hello on-premises SQL Server.</span></span> <span data-ttu-id="a4a80-170">U moet tooenter Hallo servername als een **volledig gekwalificeerde servernaam backslash exemplaarnaam (servernaam\exemplaarnaam)**.</span><span class="sxs-lookup"><span data-stu-id="a4a80-170">You need tooenter hello servername as a **fully qualified servername backslash instance name (servername\instancename)**.</span></span> <span data-ttu-id="a4a80-171">Naam Hallo gekoppelde service *adfonpremsql*.</span><span class="sxs-lookup"><span data-stu-id="a4a80-171">Name hello linked service *adfonpremsql*.</span></span>

### <span data-ttu-id="a4a80-172"><a name="adf-linked-service-blob-store"></a>Gekoppelde service voor Blob</span><span class="sxs-lookup"><span data-stu-id="a4a80-172"><a name="adf-linked-service-blob-store"></a>Linked service for Blob</span></span>
<span data-ttu-id="a4a80-173">toocreate Hallo gekoppelde service voor hello Azure Blob Storage-account:</span><span class="sxs-lookup"><span data-stu-id="a4a80-173">toocreate hello linked service for hello Azure Blob Storage account:</span></span>

* <span data-ttu-id="a4a80-174">Klik op Hallo **gegevensarchief** in Hallo ADF-startpagina op de klassieke Azure-Portal</span><span class="sxs-lookup"><span data-stu-id="a4a80-174">click hello **Data Store** in hello ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="a4a80-175">Selecteer **Azure Storage-Account**</span><span class="sxs-lookup"><span data-stu-id="a4a80-175">select **Azure Storage Account**</span></span>
* <span data-ttu-id="a4a80-176">Geef hello Azure Blob Storage-account sleutel en container.</span><span class="sxs-lookup"><span data-stu-id="a4a80-176">enter hello Azure Blob Storage account key and container name.</span></span> <span data-ttu-id="a4a80-177">Naam Hallo gekoppelde Service *adfds*.</span><span class="sxs-lookup"><span data-stu-id="a4a80-177">Name hello Linked Service *adfds*.</span></span>

### <span data-ttu-id="a4a80-178"><a name="adf-linked-service-azure-sql"></a>Gekoppelde service voor Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="a4a80-178"><a name="adf-linked-service-azure-sql"></a>Linked service for Azure SQL database</span></span>
<span data-ttu-id="a4a80-179">toocreate Hallo gekoppelde service voor hello Azure SQL Database:</span><span class="sxs-lookup"><span data-stu-id="a4a80-179">toocreate hello linked service for hello Azure SQL Database:</span></span>

* <span data-ttu-id="a4a80-180">Klik op Hallo **gegevensarchief** in Hallo ADF-startpagina op de klassieke Azure-Portal</span><span class="sxs-lookup"><span data-stu-id="a4a80-180">click hello **Data Store** in hello ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="a4a80-181">Selecteer **Azure SQL** en Voer Hallo *gebruikersnaam* en *wachtwoord* referenties voor hello Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="a4a80-181">select **Azure SQL** and enter hello *username* and *password* credentials for hello Azure SQL Database.</span></span> <span data-ttu-id="a4a80-182">Hallo *gebruikersnaam* moet worden opgegeven als  *user@servername* .</span><span class="sxs-lookup"><span data-stu-id="a4a80-182">hello *username* must be specified as *user@servername*.</span></span>   

## <span data-ttu-id="a4a80-183"><a name="adf-tables"></a>Definieer en maken van tabellen toospecify hoe tooaccess Hallo gegevenssets</span><span class="sxs-lookup"><span data-stu-id="a4a80-183"><a name="adf-tables"></a>Define and create tables toospecify how tooaccess hello datasets</span></span>
<span data-ttu-id="a4a80-184">Maak tabellen die Hallo structuur, de locatie en de beschikbaarheid van Hallo gegevenssets Hello volgen van procedures op basis van een script opgeeft.</span><span class="sxs-lookup"><span data-stu-id="a4a80-184">Create tables that specify hello structure, location, and availability of hello datasets with hello following script-based procedures.</span></span> <span data-ttu-id="a4a80-185">JSON-bestanden zijn gebruikte toodefine Hallo tabellen.</span><span class="sxs-lookup"><span data-stu-id="a4a80-185">JSON files are used toodefine hello tables.</span></span> <span data-ttu-id="a4a80-186">Zie voor meer informatie over de structuur Hallo van deze bestanden [gegevenssets](../data-factory/data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="a4a80-186">For more information on hello structure of these files, see [Datasets](../data-factory/data-factory-create-datasets.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a4a80-187">Hallo moet worden uitgevoerd `Add-AzureAccount` cmdlet alvorens uit te voeren Hallo [nieuw AzureDataFactoryTable](https://msdn.microsoft.com/library/azure/dn835096.aspx) cmdlet tooconfirm die Hallo rechts Azure-abonnement is geselecteerd voor Hallo opdrachten uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="a4a80-187">You should execute hello `Add-AzureAccount` cmdlet before executing hello [New-AzureDataFactoryTable](https://msdn.microsoft.com/library/azure/dn835096.aspx) cmdlet tooconfirm that hello right Azure subscription is selected for hello command execution.</span></span> <span data-ttu-id="a4a80-188">Zie voor documentatie van deze cmdlet [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="a4a80-188">For documentation of this cmdlet, see [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0).</span></span>
>
>

<span data-ttu-id="a4a80-189">Hallo JSON gebaseerde definities in Hallo tabellen gebruiken Hallo namen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a4a80-189">hello JSON-based definitions in hello tables use hello following names:</span></span>

* <span data-ttu-id="a4a80-190">Hallo **tabelnaam** in Hallo is het lokale SQL server *nyctaxi_data*</span><span class="sxs-lookup"><span data-stu-id="a4a80-190">hello **table name** in hello on-premises SQL server is *nyctaxi_data*</span></span>
* <span data-ttu-id="a4a80-191">Hallo **containernaam** in hello Azure Blob Storage-account is *containername*</span><span class="sxs-lookup"><span data-stu-id="a4a80-191">hello **container name** in hello Azure Blob Storage account is *containername*</span></span>  

<span data-ttu-id="a4a80-192">Drie tabeldefinities nodig zijn voor deze ADF-pijplijn:</span><span class="sxs-lookup"><span data-stu-id="a4a80-192">Three table definitions are needed for this ADF pipeline:</span></span>

1. [<span data-ttu-id="a4a80-193">On-premises SQL-tabel</span><span class="sxs-lookup"><span data-stu-id="a4a80-193">SQL on-premises Table</span></span>](#adf-table-onprem-sql)
2. [<span data-ttu-id="a4a80-194">Blobtabel</span><span class="sxs-lookup"><span data-stu-id="a4a80-194">Blob Table </span></span>](#adf-table-blob-store)
3. [<span data-ttu-id="a4a80-195">SQL Azure-tabel</span><span class="sxs-lookup"><span data-stu-id="a4a80-195">SQL Azure Table</span></span>](#adf-table-azure-sql)

> [!NOTE]
> <span data-ttu-id="a4a80-196">Deze procedures gebruikt u Azure PowerShell toodefine en Hallo ADF activiteiten maken.</span><span class="sxs-lookup"><span data-stu-id="a4a80-196">These procedures use Azure PowerShell toodefine and create hello ADF activities.</span></span> <span data-ttu-id="a4a80-197">Maar deze taken kunnen ook worden gerealiseerd met hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a4a80-197">But these tasks can also be accomplished using hello Azure portal.</span></span> <span data-ttu-id="a4a80-198">Zie voor meer informatie [gegevenssets maken](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets).</span><span class="sxs-lookup"><span data-stu-id="a4a80-198">For details, see [Create datasets](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets).</span></span>
>
>

### <span data-ttu-id="a4a80-199"><a name="adf-table-onprem-sql"></a>On-premises SQL-tabel</span><span class="sxs-lookup"><span data-stu-id="a4a80-199"><a name="adf-table-onprem-sql"></a>SQL on-premises Table</span></span>
<span data-ttu-id="a4a80-200">de tabeldefinitie Hallo voor Hallo lokale SQL Server is opgegeven in de volgende JSON-bestand Hallo:</span><span class="sxs-lookup"><span data-stu-id="a4a80-200">hello table definition for hello on-premises SQL Server is specified in hello following JSON file:</span></span>

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

<span data-ttu-id="a4a80-201">Hallo kolomnamen zijn niet opgenomen in hier.</span><span class="sxs-lookup"><span data-stu-id="a4a80-201">hello column names were not included here.</span></span> <span data-ttu-id="a4a80-202">U kunt subplan selecteren op Hallo kolomnamen door ze hier (voor meer informatie Hallo verplicht [ADF documentatie](../data-factory/data-factory-data-movement-activities.md) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="a4a80-202">You can sub-select on hello column names by including them here (for details check hello [ADF documentation](../data-factory/data-factory-data-movement-activities.md) topic.</span></span>

<span data-ttu-id="a4a80-203">Hallo JSON-definitie van Hallo tabel kopiëren naar een bestand met de naam *onpremtabledef.json* bestand en sla het tooa bekende locatie (hier uitgegaan toobe *C:\temp\onpremtabledef.json*).</span><span class="sxs-lookup"><span data-stu-id="a4a80-203">Copy hello JSON definition of hello table into a file called *onpremtabledef.json* file and save it tooa known location (here assumed toobe *C:\temp\onpremtabledef.json*).</span></span> <span data-ttu-id="a4a80-204">Hallo-tabel maken in ADF Hello Azure PowerShell-cmdlet te volgen:</span><span class="sxs-lookup"><span data-stu-id="a4a80-204">Create hello table in ADF with hello following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp –File C:\temp\onpremtabledef.json


### <span data-ttu-id="a4a80-205"><a name="adf-table-blob-store"></a>Blobtabel</span><span class="sxs-lookup"><span data-stu-id="a4a80-205"><a name="adf-table-blob-store"></a>Blob Table</span></span>
<span data-ttu-id="a4a80-206">Definitie voor de tabel voor Hallo Hallo uitvoer blob bevindt zich in Hallo volgende (toegewezen Hallo ingenomen gegevens van de lokale tooAzure blob):</span><span class="sxs-lookup"><span data-stu-id="a4a80-206">Definition for hello table for hello output blob location is in hello following (this maps hello ingested data from on-premises tooAzure blob):</span></span>

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

<span data-ttu-id="a4a80-207">Hallo JSON-definitie van Hallo tabel kopiëren naar een bestand met de naam *bloboutputtabledef.json* bestand en sla het tooa bekende locatie (hier uitgegaan toobe *C:\temp\bloboutputtabledef.json*).</span><span class="sxs-lookup"><span data-stu-id="a4a80-207">Copy hello JSON definition of hello table into a file called *bloboutputtabledef.json* file and save it tooa known location (here assumed toobe *C:\temp\bloboutputtabledef.json*).</span></span> <span data-ttu-id="a4a80-208">Hallo-tabel maken in ADF Hello Azure PowerShell-cmdlet te volgen:</span><span class="sxs-lookup"><span data-stu-id="a4a80-208">Create hello table in ADF with hello following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\bloboutputtabledef.json  

### <span data-ttu-id="a4a80-209"><a name="adf-table-azure-sq"></a>SQL Azure-tabel</span><span class="sxs-lookup"><span data-stu-id="a4a80-209"><a name="adf-table-azure-sq"></a>SQL Azure Table</span></span>
<span data-ttu-id="a4a80-210">Definitie voor de tabel Hallo voor Hallo die SQL Azure-uitvoer heeft Hallo volgende (dit schema toegewezen Hallo-gegevens die afkomstig zijn van een blob Hallo):</span><span class="sxs-lookup"><span data-stu-id="a4a80-210">Definition for hello table for hello SQL Azure output is in hello following (this schema maps hello data coming from hello blob):</span></span>

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

<span data-ttu-id="a4a80-211">Hallo JSON-definitie van Hallo tabel kopiëren naar een bestand met de naam *AzureSqlTable.json* bestand en sla het tooa bekende locatie (hier uitgegaan toobe *C:\temp\AzureSqlTable.json*).</span><span class="sxs-lookup"><span data-stu-id="a4a80-211">Copy hello JSON definition of hello table into a file called *AzureSqlTable.json* file and save it tooa known location (here assumed toobe *C:\temp\AzureSqlTable.json*).</span></span> <span data-ttu-id="a4a80-212">Hallo-tabel maken in ADF Hello Azure PowerShell-cmdlet te volgen:</span><span class="sxs-lookup"><span data-stu-id="a4a80-212">Create hello table in ADF with hello following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\AzureSqlTable.json  


## <span data-ttu-id="a4a80-213"><a name="adf-pipeline"></a>Definieer en Hallo pijplijn maken</span><span class="sxs-lookup"><span data-stu-id="a4a80-213"><a name="adf-pipeline"></a>Define and create hello pipeline</span></span>
<span data-ttu-id="a4a80-214">Hallo-activiteiten die toohello behoren pipeline en Hallo pijplijn maken met de Hallo volgen van procedures op basis van scripts opgeven.</span><span class="sxs-lookup"><span data-stu-id="a4a80-214">Specify hello activities that belong toohello pipeline and create hello pipeline with hello following script-based procedures.</span></span> <span data-ttu-id="a4a80-215">Een JSON-bestand is gebruikte toodefine Hallo pipeline-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="a4a80-215">A JSON file is used toodefine hello pipeline properties.</span></span>

* <span data-ttu-id="a4a80-216">Hallo script wordt ervan uitgegaan dat Hallo **pijplijn naam** is *AMLDSProcessPipeline*.</span><span class="sxs-lookup"><span data-stu-id="a4a80-216">hello script assumes that hello **pipeline name** is *AMLDSProcessPipeline*.</span></span>
* <span data-ttu-id="a4a80-217">Vergeet niet dat we Hallo periodiciteit van Hallo pijplijn toobe uitgevoerd op dagelijks basis en gebruik Hallo standaard uitvoeringstijd voor Hallo taak (12: 00 a.m. UTC) ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a4a80-217">Also note that we set hello periodicity of hello pipeline toobe executed on daily basis and use hello default execution time for hello job (12 am UTC).</span></span>

> [!NOTE]
> <span data-ttu-id="a4a80-218">Hallo volgende procedures gebruikt u Azure PowerShell toodefine en Hallo ADF pijplijn maken.</span><span class="sxs-lookup"><span data-stu-id="a4a80-218">hello following procedures use Azure PowerShell toodefine and create hello ADF pipeline.</span></span> <span data-ttu-id="a4a80-219">Maar deze taak kan ook worden bereikt met de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a4a80-219">But this task can also be accomplished using the Azure portal.</span></span> <span data-ttu-id="a4a80-220">Zie voor meer informatie [maken pijplijn](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline).</span><span class="sxs-lookup"><span data-stu-id="a4a80-220">For details, see [Create pipeline](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline).</span></span>
>
>

<span data-ttu-id="a4a80-221">Hallo tabeldefinities opgegeven voorheen Hallo pijplijn definitie voor Hallo die ADF is opgegeven, als volgt:</span><span class="sxs-lookup"><span data-stu-id="a4a80-221">Using hello table definitions provided previously, hello pipeline definition for hello ADF is specified as follows:</span></span>

        {
            "name": "AMLDSProcessPipeline",
            "properties":
            {
                "description" : "This pipeline has one Copy activity that copies data from an on-premises SQL tooAzure blob",
                 "activities":
                [
                    {
                        "name": "CopyFromSQLtoBlob",
                        "description": "Copy data from on-premises SQL server tooblob",     
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
                        "description": "Push data tooSql Azure",        
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

<span data-ttu-id="a4a80-222">Kopieer deze JSON-definitie van de pijplijn Hallo naar een bestand met de naam *pipelinedef.json* bestand en sla het tooa bekende locatie (hier uitgegaan toobe *C:\temp\pipelinedef.json*).</span><span class="sxs-lookup"><span data-stu-id="a4a80-222">Copy this JSON definition of hello pipeline into a file called *pipelinedef.json* file and save it tooa known location (here assumed toobe *C:\temp\pipelinedef.json*).</span></span> <span data-ttu-id="a4a80-223">Hallo pijplijn in ADF maken met de Hallo Azure PowerShell-cmdlet te volgen:</span><span class="sxs-lookup"><span data-stu-id="a4a80-223">Create hello pipeline in ADF with hello following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryPipeline  -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\pipelinedef.json

<span data-ttu-id="a4a80-224">Controleer of u kunt Hallo pijplijn op Hallo ADF in Hallo klassieke Azure-Portal weergegeven als volgt (wanneer u klikt op Hallo diagram)</span><span class="sxs-lookup"><span data-stu-id="a4a80-224">Confirm that you can see hello pipeline on hello ADF in hello Azure Classic Portal show up as following (when you click hello diagram)</span></span>

![ADF-pipeline](media/machine-learning-data-science-move-sql-azure-adf/DJP1kji.png)

## <span data-ttu-id="a4a80-226"><a name="adf-pipeline-start"></a>Hallo pijplijn starten</span><span class="sxs-lookup"><span data-stu-id="a4a80-226"><a name="adf-pipeline-start"></a>Start hello Pipeline</span></span>
<span data-ttu-id="a4a80-227">Hallo-pijplijn kan nu worden uitgevoerd met behulp van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="a4a80-227">hello pipeline can now be run using hello following command:</span></span>

    Set-AzureDataFactoryPipelineActivePeriod -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp -StartDateTime startdateZ –EndDateTime enddateZ –Name AMLDSProcessPipeline

<span data-ttu-id="a4a80-228">Hallo *startdate* en *enddate* parameterwaarden toobe vervangen door de werkelijke Hallo-datums tussen wie u wilt dat Hallo pijplijn toorun nodig.</span><span class="sxs-lookup"><span data-stu-id="a4a80-228">hello *startdate* and *enddate* parameter values need toobe replaced with hello actual dates between which you want hello pipeline toorun.</span></span>

<span data-ttu-id="a4a80-229">Zodra het Hallo-pijplijn wordt uitgevoerd, moet u kunnen toosee Hallo gegevens weergegeven in het Hallo-container die zijn geselecteerd voor Hallo blob, één bestand per dag.</span><span class="sxs-lookup"><span data-stu-id="a4a80-229">Once hello pipeline executes, you should be able toosee hello data show up in hello container selected for hello blob, one file per day.</span></span>

<span data-ttu-id="a4a80-230">Houd er rekening mee dat we geen Hallo functionaliteit van ADF toopipe gegevens stapsgewijs hebt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a4a80-230">Note that we have not leveraged hello functionality provided by ADF toopipe data incrementally.</span></span> <span data-ttu-id="a4a80-231">Voor meer informatie over hoe toodo deze en andere mogelijkheden van ADF, zien Hallo [ADF documentatie](https://azure.microsoft.com/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="a4a80-231">For more information on how toodo this and other capabilities provided by ADF, see hello [ADF documentation](https://azure.microsoft.com/services/data-factory/).</span></span>
