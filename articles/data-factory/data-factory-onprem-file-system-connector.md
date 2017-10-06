---
title: aaaCopy gegevens van/naar een bestandssysteem met behulp van Azure Data Factory | Microsoft Docs
description: Meer informatie over hoe toocopy gegevens tooand uit een on-premises bestandssysteem met behulp van Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ce19f1ae-358e-4ffc-8a80-d802505c9c84
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 201b8bc3ffa639df781443aa0c3f95c975d280be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-an-on-premises-file-system-by-using-azure-data-factory"></a><span data-ttu-id="44aa5-103">Tooand gegevens kopiëren van een on-premises bestandssysteem met behulp van Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="44aa5-103">Copy data tooand from an on-premises file system by using Azure Data Factory</span></span>
<span data-ttu-id="44aa5-104">Dit artikel wordt uitgelegd hoe toouse Kopieeractiviteit Hallo in Azure Data Factory toocopy gegevens uit een on-premises bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="44aa5-104">This article explains how toouse hello Copy Activity in Azure Data Factory toocopy data to/from an on-premises file system.</span></span> <span data-ttu-id="44aa5-105">Dit is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit Hallo geeft.</span><span class="sxs-lookup"><span data-stu-id="44aa5-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="44aa5-106">Ondersteunde scenario 's</span><span class="sxs-lookup"><span data-stu-id="44aa5-106">Supported scenarios</span></span>
<span data-ttu-id="44aa5-107">U kunt gegevens kopiëren **uit een on-premises bestandssysteem** toohello gegevensarchieven te volgen:</span><span class="sxs-lookup"><span data-stu-id="44aa5-107">You can copy data **from an on-premises file system** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="44aa5-108">Gegevens kunnen worden gekopieerd van de volgende gegevensarchieven Hallo **tooan lokaal bestandssysteem**:</span><span class="sxs-lookup"><span data-stu-id="44aa5-108">You can copy data from hello following data stores **tooan on-premises file system**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> <span data-ttu-id="44aa5-109">Kopieeractiviteit worden Hallo-bronbestand niet verwijderd nadat het is gekopieerde toohello bestemming.</span><span class="sxs-lookup"><span data-stu-id="44aa5-109">Copy Activity does not delete hello source file after it is successfully copied toohello destination.</span></span> <span data-ttu-id="44aa5-110">Als u toodelete Hallo-bronbestand na een geslaagde kopie moet, maakt u een aangepaste activiteit toodelete Hallo-bestand en Hallo activiteit in de pijplijn hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="44aa5-110">If you need toodelete hello source file after a successful copy, create a custom activity toodelete hello file and use hello activity in hello pipeline.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="44aa5-111">Connectiviteit inschakelen</span><span class="sxs-lookup"><span data-stu-id="44aa5-111">Enabling connectivity</span></span>
<span data-ttu-id="44aa5-112">Data Factory ondersteunt verbindende tooand uit een on-premises bestandssysteem via **Data Management Gateway**.</span><span class="sxs-lookup"><span data-stu-id="44aa5-112">Data Factory supports connecting tooand from an on-premises file system via **Data Management Gateway**.</span></span> <span data-ttu-id="44aa5-113">U moet Hallo Data Management Gateway installeren in uw on-premises omgeving voor Hallo Data Factory-service tooconnect tooany ondersteunde on-premises gegevensopslag met inbegrip van bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="44aa5-113">You must install hello Data Management Gateway in your on-premises environment for hello Data Factory service tooconnect tooany supported on-premises data store including file system.</span></span> <span data-ttu-id="44aa5-114">toolearn over Data Management Gateway en voor stapsgewijze instructies over het instellen van Hallo-gateway, Zie [gegevens verplaatsen tussen lokale bronnen en Hallo cloud met Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="44aa5-114">toolearn about Data Management Gateway and for step-by-step instructions on setting up hello gateway, see [Move data between on-premises sources and hello cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span></span> <span data-ttu-id="44aa5-115">Naast Data Management Gateway moeten geen binaire bestanden geïnstalleerd toobe toocommunicate tooand uit een on-premises bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="44aa5-115">Apart from Data Management Gateway, no other binary files need toobe installed toocommunicate tooand from an on-premises file system.</span></span> <span data-ttu-id="44aa5-116">U moet installeren en gebruiken van Hallo Data Management Gateway, zelfs als het bestandssysteem Hallo in Azure IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="44aa5-116">You must install and use hello Data Management Gateway even if hello file system is in Azure IaaS VM.</span></span> <span data-ttu-id="44aa5-117">Zie voor gedetailleerde informatie over gateway-Hallo [Data Management Gateway](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="44aa5-117">For detailed information about hello gateway, see [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>

<span data-ttu-id="44aa5-118">installeren van een bestandsshare Linux toouse [Samba](https://www.samba.org/) op uw Linux-server en de Data Management Gateway installeren op een WindowsServer.</span><span class="sxs-lookup"><span data-stu-id="44aa5-118">toouse a Linux file share, install [Samba](https://www.samba.org/) on your Linux server, and install Data Management Gateway on a Windows server.</span></span> <span data-ttu-id="44aa5-119">Data Management Gateway installeren op een Linux-server wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="44aa5-119">Installing Data Management Gateway on a Linux server is not supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="44aa5-120">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="44aa5-120">Getting started</span></span>
<span data-ttu-id="44aa5-121">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens van een bestandssysteem wordt verplaatst met behulp van verschillende hulpprogramma's voor API's.</span><span class="sxs-lookup"><span data-stu-id="44aa5-121">You can create a pipeline with a copy activity that moves data to/from a file system by using different tools/APIs.</span></span>

<span data-ttu-id="44aa5-122">Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="44aa5-122">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="44aa5-123">Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met Hallo wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="44aa5-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="44aa5-124">U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="44aa5-124">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="44aa5-125">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="44aa5-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="44aa5-126">Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="44aa5-126">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="44aa5-127">Maak een **gegevensfactory**.</span><span class="sxs-lookup"><span data-stu-id="44aa5-127">Create a **data factory**.</span></span> <span data-ttu-id="44aa5-128">Een gegevensfactory kan één of meer pijplijnen bevatten.</span><span class="sxs-lookup"><span data-stu-id="44aa5-128">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="44aa5-129">Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="44aa5-129">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="44aa5-130">Bijvoorbeeld, als u gegevens uit een Azure blob storage tooan lokale bestandssysteem kopiëren wilt, u twee gekoppelde services toolink uw on-premises bestandssysteem en de Azure storage-account tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="44aa5-130">For example, if you are copying data from an Azure blob storage tooan on-premises file system, you create two linked services toolink your on-premises file system and Azure storage account tooyour data factory.</span></span> <span data-ttu-id="44aa5-131">Zie voor de gekoppelde service-eigenschappen die specifiek tooan on-premises bestandssysteem, [gekoppelde service-eigenschappen](#linked-service-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="44aa5-131">For linked service properties that are specific tooan on-premises file system, see [linked service properties](#linked-service-properties) section.</span></span>
3. <span data-ttu-id="44aa5-132">Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="44aa5-132">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="44aa5-133">In vermeld in de laatste stap Hallo Hallo voorbeeld maakt u een gegevensset toospecify Hallo blob-container en map met invoergegevens Hallo.</span><span class="sxs-lookup"><span data-stu-id="44aa5-133">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="44aa5-134">En u een andere dataset toospecify Hallo map- en -naam (optioneel) in het bestandssysteem maken.</span><span class="sxs-lookup"><span data-stu-id="44aa5-134">And, you create another dataset toospecify hello folder and file name (optional) in your file system.</span></span> <span data-ttu-id="44aa5-135">Zie voor de eigenschappen van de gegevensset die specifieke tooon lokaal bestandssysteem, [eigenschappen van gegevensset](#dataset-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="44aa5-135">For dataset properties that are specific tooon-premises file system, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="44aa5-136">Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="44aa5-136">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="44aa5-137">In Hallo voorbeeld eerder vermeld, gebruikt u BlobSource als een bron- en FileSystemSink als een sink voor de kopieeractiviteit Hallo.</span><span class="sxs-lookup"><span data-stu-id="44aa5-137">In hello example mentioned earlier, you use BlobSource as a source and FileSystemSink as a sink for hello copy activity.</span></span> <span data-ttu-id="44aa5-138">Op dezelfde manier als u uit het lokale bestand system tooAzure Blob Storage kopiëren wilt, gebruikt u FileSystemSource en BlobSink in Hallo kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="44aa5-138">Similarly, if you are copying from on-premises file system tooAzure Blob Storage, you use FileSystemSource and BlobSink in hello copy activity.</span></span> <span data-ttu-id="44aa5-139">Zie voor de activiteitseigenschappen kopiëren die specifieke tooon lokaal bestandssysteem, [activiteitseigenschappen kopiëren](#copy-activity-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="44aa5-139">For copy activity properties that are specific tooon-premises file system, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="44aa5-140">Voor informatie over hoe toouse een gegevensarchief als een bron of een sink, klikt u op Hallo-koppeling in de vorige sectie Hallo voor de gegevensopslag.</span><span class="sxs-lookup"><span data-stu-id="44aa5-140">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>

<span data-ttu-id="44aa5-141">Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="44aa5-141">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="44aa5-142">Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="44aa5-142">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="44aa5-143">Zie voor voorbeelden met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens van/naar een bestandssysteem zijn, [JSON voorbeelden](#json-examples-for-copying-data-to-and-from-file-system) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="44aa5-143">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from a file system, see [JSON examples](#json-examples-for-copying-data-to-and-from-file-system) section of this article.</span></span>

<span data-ttu-id="44aa5-144">Hallo volgende secties bieden informatie over de JSON-eigenschappen die gebruikt toodefine Data Factory-entiteiten specifieke toofile system zijn:</span><span class="sxs-lookup"><span data-stu-id="44aa5-144">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific toofile system:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="44aa5-145">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="44aa5-145">Linked service properties</span></span>
<span data-ttu-id="44aa5-146">U kunt een lokaal bestand system tooan Azure data factory Hello koppelen **On-Premises bestandsserver** gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="44aa5-146">You can link an on-premises file system tooan Azure data factory with hello **On-Premises File Server** linked service.</span></span> <span data-ttu-id="44aa5-147">Hallo volgende tabel bevat beschrijvingen van JSON-elementen die specifiek toohello bestandsserver On-Premises gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="44aa5-147">hello following table provides descriptions for JSON elements that are specific toohello On-Premises File Server linked service.</span></span>

| <span data-ttu-id="44aa5-148">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="44aa5-148">Property</span></span> | <span data-ttu-id="44aa5-149">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="44aa5-149">Description</span></span> | <span data-ttu-id="44aa5-150">Vereist</span><span class="sxs-lookup"><span data-stu-id="44aa5-150">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="44aa5-151">type</span><span class="sxs-lookup"><span data-stu-id="44aa5-151">type</span></span> |<span data-ttu-id="44aa5-152">Zorg ervoor dat de eigenschap type hello te is ingesteld**OnPremisesFileServer**.</span><span class="sxs-lookup"><span data-stu-id="44aa5-152">Ensure that hello type property is set too**OnPremisesFileServer**.</span></span> |<span data-ttu-id="44aa5-153">Ja</span><span class="sxs-lookup"><span data-stu-id="44aa5-153">Yes</span></span> |
| <span data-ttu-id="44aa5-154">host</span><span class="sxs-lookup"><span data-stu-id="44aa5-154">host</span></span> |<span data-ttu-id="44aa5-155">Hiermee geeft u het hoofdpad Hallo van Hallo map die u toocopy wilt.</span><span class="sxs-lookup"><span data-stu-id="44aa5-155">Specifies hello root path of hello folder that you want toocopy.</span></span> <span data-ttu-id="44aa5-156">Gebruik Hallo escape-teken ' \ ' voor speciale tekens in Hallo-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="44aa5-156">Use hello escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="44aa5-157">Zie [voorbeeld gekoppelde service en gegevensset definities](#sample-linked-service-and-dataset-definitions) voor voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="44aa5-157">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span> |<span data-ttu-id="44aa5-158">Ja</span><span class="sxs-lookup"><span data-stu-id="44aa5-158">Yes</span></span> |
| <span data-ttu-id="44aa5-159">gebruikers-id</span><span class="sxs-lookup"><span data-stu-id="44aa5-159">userid</span></span> |<span data-ttu-id="44aa5-160">Hallo-ID van het Hallo-gebruiker met toegang toohello server opgeven.</span><span class="sxs-lookup"><span data-stu-id="44aa5-160">Specify hello ID of hello user who has access toohello server.</span></span> |<span data-ttu-id="44aa5-161">Nee (als u ervoor encryptedCredential kiest)</span><span class="sxs-lookup"><span data-stu-id="44aa5-161">No (if you choose encryptedCredential)</span></span> |
| <span data-ttu-id="44aa5-162">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="44aa5-162">password</span></span> |<span data-ttu-id="44aa5-163">Hallo-wachtwoord voor gebruiker hello (gebruikersnaam) opgeven.</span><span class="sxs-lookup"><span data-stu-id="44aa5-163">Specify hello password for hello user (userid).</span></span> |<span data-ttu-id="44aa5-164">Nee (als u encryptedCredential kiezen</span><span class="sxs-lookup"><span data-stu-id="44aa5-164">No (if you choose encryptedCredential</span></span> |
| <span data-ttu-id="44aa5-165">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="44aa5-165">encryptedCredential</span></span> |<span data-ttu-id="44aa5-166">Geef referenties op Hallo versleuteld die u door de cmdlet New-AzureRmDataFactoryEncryptValue Hallo kunt ophalen.</span><span class="sxs-lookup"><span data-stu-id="44aa5-166">Specify hello encrypted credentials that you can get by running hello New-AzureRmDataFactoryEncryptValue cmdlet.</span></span> |<span data-ttu-id="44aa5-167">Nee (als u toospecify gebruikersnaam en wachtwoord als tekst zonder opmaak kiezen)</span><span class="sxs-lookup"><span data-stu-id="44aa5-167">No (if you choose toospecify userid and password in plain text)</span></span> |
| <span data-ttu-id="44aa5-168">gatewayName</span><span class="sxs-lookup"><span data-stu-id="44aa5-168">gatewayName</span></span> |<span data-ttu-id="44aa5-169">Geeft de naam Hallo van Hallo gateway dat Data Factory tooconnect toohello lokale bestandsserver moeten gebruiken.</span><span class="sxs-lookup"><span data-stu-id="44aa5-169">Specifies hello name of hello gateway that Data Factory should use tooconnect toohello on-premises file server.</span></span> |<span data-ttu-id="44aa5-170">Ja</span><span class="sxs-lookup"><span data-stu-id="44aa5-170">Yes</span></span> |


### <a name="sample-linked-service-and-dataset-definitions"></a><span data-ttu-id="44aa5-171">Voorbeeld van de gekoppelde service en de definities van de gegevensset</span><span class="sxs-lookup"><span data-stu-id="44aa5-171">Sample linked service and dataset definitions</span></span>
| <span data-ttu-id="44aa5-172">Scenario</span><span class="sxs-lookup"><span data-stu-id="44aa5-172">Scenario</span></span> | <span data-ttu-id="44aa5-173">In de definitie van de gekoppelde service host</span><span class="sxs-lookup"><span data-stu-id="44aa5-173">Host in linked service definition</span></span> | <span data-ttu-id="44aa5-174">folderPath in de definitie van gegevensset</span><span class="sxs-lookup"><span data-stu-id="44aa5-174">folderPath in dataset definition</span></span> |
| --- | --- | --- |
| <span data-ttu-id="44aa5-175">Lokale map op de Data Management Gateway-apparaat:</span><span class="sxs-lookup"><span data-stu-id="44aa5-175">Local folder on Data Management Gateway machine:</span></span> <br/><br/><span data-ttu-id="44aa5-176">Voorbeelden: D:\\ \* of D:\folder\subfolder\\*</span><span class="sxs-lookup"><span data-stu-id="44aa5-176">Examples: D:\\\* or D:\folder\subfolder\\*</span></span> |<span data-ttu-id="44aa5-177">D:\\ \\ (voor Data Management Gateway 2.0 en hoger)</span><span class="sxs-lookup"><span data-stu-id="44aa5-177">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/> <span data-ttu-id="44aa5-178">localhost (voor oudere versies dan Data Management Gateway 2.0)</span><span class="sxs-lookup"><span data-stu-id="44aa5-178">localhost (for earlier versions than Data Management Gateway 2.0)</span></span> |<span data-ttu-id="44aa5-179">. \\ \\ of de map\\\\submap (voor Data Management Gateway 2.0 en hoger)</span><span class="sxs-lookup"><span data-stu-id="44aa5-179">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/><span data-ttu-id="44aa5-180">D:\\ \\ of D:\\\\map\\\\submap (voor gatewayversie lager dan 2.0)</span><span class="sxs-lookup"><span data-stu-id="44aa5-180">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span></span> |
| <span data-ttu-id="44aa5-181">Externe gedeelde map:</span><span class="sxs-lookup"><span data-stu-id="44aa5-181">Remote shared folder:</span></span> <br/><br/><span data-ttu-id="44aa5-182">Voorbeelden: \\ \\MijnServer\\delen\\ \* of \\ \\MijnServer\\delen\\map\\submap\\*</span><span class="sxs-lookup"><span data-stu-id="44aa5-182">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span></span> |<span data-ttu-id="44aa5-183">\\\\\\\\MijnServer\\\\delen</span><span class="sxs-lookup"><span data-stu-id="44aa5-183">\\\\\\\\myserver\\\\share</span></span> |<span data-ttu-id="44aa5-184">. \\ \\ of de map\\\\submap</span><span class="sxs-lookup"><span data-stu-id="44aa5-184">.\\\\ or folder\\\\subfolder</span></span> |


### <a name="example-using-username-and-password-in-plain-text"></a><span data-ttu-id="44aa5-185">Voorbeeld: Met behulp van gebruikersnaam en wachtwoord in tekst zonder opmaak</span><span class="sxs-lookup"><span data-stu-id="44aa5-185">Example: Using username and password in plain text</span></span>

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

### <a name="example-using-encryptedcredential"></a><span data-ttu-id="44aa5-186">Voorbeeld: Encryptedcredential gebruiken</span><span class="sxs-lookup"><span data-stu-id="44aa5-186">Example: Using encryptedcredential</span></span>

```JSON
{
  "Name": " OnPremisesFileServerLinkedService ",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "D:\\",
      "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
      "gatewayName": "mygateway"
    }
  }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="44aa5-187">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="44aa5-187">Dataset properties</span></span>
<span data-ttu-id="44aa5-188">Zie voor een volledige lijst van de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets en secties [gegevenssets maken](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="44aa5-188">For a full list of sections and properties that are available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="44aa5-189">Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle typen van de gegevensset.</span><span class="sxs-lookup"><span data-stu-id="44aa5-189">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="44aa5-190">Hallo typeProperties sectie verschilt voor elk type dataset.</span><span class="sxs-lookup"><span data-stu-id="44aa5-190">hello typeProperties section is different for each type of dataset.</span></span> <span data-ttu-id="44aa5-191">Het levert informatie zoals Hallo locatie en indeling van gegevens in het gegevensarchief Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="44aa5-191">It provides information such as hello location and format of hello data in hello data store.</span></span> <span data-ttu-id="44aa5-192">Hallo typeProperties sectie voor de gegevensset Hallo van het type **FileShare** heeft Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="44aa5-192">hello typeProperties section for hello dataset of type **FileShare** has hello following properties:</span></span>

| <span data-ttu-id="44aa5-193">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="44aa5-193">Property</span></span> | <span data-ttu-id="44aa5-194">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="44aa5-194">Description</span></span> | <span data-ttu-id="44aa5-195">Vereist</span><span class="sxs-lookup"><span data-stu-id="44aa5-195">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="44aa5-196">folderPath</span><span class="sxs-lookup"><span data-stu-id="44aa5-196">folderPath</span></span> |<span data-ttu-id="44aa5-197">Hiermee geeft u Hallo subpad toohello map.</span><span class="sxs-lookup"><span data-stu-id="44aa5-197">Specifies hello subpath toohello folder.</span></span> <span data-ttu-id="44aa5-198">Gebruik Hallo escape-teken ' \' voor speciale tekens in Hallo-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="44aa5-198">Use hello escape character ‘\’ for special characters in hello string.</span></span> <span data-ttu-id="44aa5-199">Zie [voorbeeld gekoppelde service en gegevensset definities](#sample-linked-service-and-dataset-definitions) voor voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="44aa5-199">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="44aa5-200">U kunt deze eigenschap combineren met **partitionBy** toohave mappaden op basis van het segment beginnen of eindigen-datums en tijden.</span><span class="sxs-lookup"><span data-stu-id="44aa5-200">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="44aa5-201">Ja</span><span class="sxs-lookup"><span data-stu-id="44aa5-201">Yes</span></span> |
| <span data-ttu-id="44aa5-202">fileName</span><span class="sxs-lookup"><span data-stu-id="44aa5-202">fileName</span></span> |<span data-ttu-id="44aa5-203">Hallo-naam van Hallo-bestand opgeven in Hallo **folderPath** als u wilt dat Hallo tabel toorefer tooa specifiek bestand in map Hallo.</span><span class="sxs-lookup"><span data-stu-id="44aa5-203">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="44aa5-204">Als u geen waarde voor deze eigenschap niet opgeeft, wijst Hallo tabel tooall bestanden in de map Hallo.</span><span class="sxs-lookup"><span data-stu-id="44aa5-204">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="44aa5-205">Wanneer **fileName** is niet opgegeven voor een uitvoergegevensset en **preserveHierarchy** niet is opgegeven in activiteit sink Hallo-naam van Hallo gegenereerd bestand is in de volgende indeling Hallo:</span><span class="sxs-lookup"><span data-stu-id="44aa5-205">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, hello name of hello generated file is in hello following format:</span></span> <br/><br/><span data-ttu-id="44aa5-206">`Data.<Guid>.txt`(Voorbeeld: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="44aa5-206">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="44aa5-207">Nee</span><span class="sxs-lookup"><span data-stu-id="44aa5-207">No</span></span> |
| <span data-ttu-id="44aa5-208">fileFilter</span><span class="sxs-lookup"><span data-stu-id="44aa5-208">fileFilter</span></span> |<span data-ttu-id="44aa5-209">Geef dat een filter toobe tooselect gebruikt een subset van de bestanden in Hallo folderPath in plaats van alle bestanden.</span><span class="sxs-lookup"><span data-stu-id="44aa5-209">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span> <br/><br/><span data-ttu-id="44aa5-210">Toegestane waarden zijn: `*` (meerdere tekens) en `?` (willekeurig teken).</span><span class="sxs-lookup"><span data-stu-id="44aa5-210">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="44aa5-211">Voorbeeld 1: 'fileFilter":" * .log '</span><span class="sxs-lookup"><span data-stu-id="44aa5-211">Example 1: "fileFilter": "*.log"</span></span><br/><span data-ttu-id="44aa5-212">Voorbeeld 2: 'fileFilter': 2014 - 1-?. txt'</span><span class="sxs-lookup"><span data-stu-id="44aa5-212">Example 2: "fileFilter": 2014-1-?.txt"</span></span><br/><br/><span data-ttu-id="44aa5-213">Houd er rekening mee dat fileFilter is van toepassing op een bestandsshare-invoergegevensset.</span><span class="sxs-lookup"><span data-stu-id="44aa5-213">Note that fileFilter is applicable for an input FileShare dataset.</span></span> |<span data-ttu-id="44aa5-214">Nee</span><span class="sxs-lookup"><span data-stu-id="44aa5-214">No</span></span> |
| <span data-ttu-id="44aa5-215">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="44aa5-215">partitionedBy</span></span> |<span data-ttu-id="44aa5-216">U kunt partitionedBy toospecify een dynamische folderPath/bestandsnaam gebruiken voor timeseries gegevens.</span><span class="sxs-lookup"><span data-stu-id="44aa5-216">You can use partitionedBy toospecify a dynamic folderPath/fileName for time-series data.</span></span> <span data-ttu-id="44aa5-217">Een voorbeeld is folderPath geparametriseerde voor elk uur van gegevens.</span><span class="sxs-lookup"><span data-stu-id="44aa5-217">An example is folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="44aa5-218">Nee</span><span class="sxs-lookup"><span data-stu-id="44aa5-218">No</span></span> |
| <span data-ttu-id="44aa5-219">Indeling</span><span class="sxs-lookup"><span data-stu-id="44aa5-219">format</span></span> | <span data-ttu-id="44aa5-220">Hallo na indelingstypen worden ondersteund: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="44aa5-220">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="44aa5-221">Set Hallo **type** eigenschap onder indeling tooone van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="44aa5-221">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="44aa5-222">Zie voor meer informatie [tekstindeling](data-factory-supported-file-and-compression-formats.md#text-format), [Json-indeling](data-factory-supported-file-and-compression-formats.md#json-format), [Avro-indeling](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc indeling](data-factory-supported-file-and-compression-formats.md#orc-format), en [parketvloeren indeling](data-factory-supported-file-and-compression-formats.md#parquet-format) secties.</span><span class="sxs-lookup"><span data-stu-id="44aa5-222">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="44aa5-223">Als u wilt dat te**kopiëren van bestanden als-is** tussen bestandsgebaseerde winkels (binaire kopiëren) Hallo indeling sectie in beide definities invoer en uitvoer gegevensset overslaan.</span><span class="sxs-lookup"><span data-stu-id="44aa5-223">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="44aa5-224">Nee</span><span class="sxs-lookup"><span data-stu-id="44aa5-224">No</span></span> |
| <span data-ttu-id="44aa5-225">Compressie</span><span class="sxs-lookup"><span data-stu-id="44aa5-225">compression</span></span> | <span data-ttu-id="44aa5-226">Hallo-type en compressieniveau voor Hallo gegevens opgeven.</span><span class="sxs-lookup"><span data-stu-id="44aa5-226">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="44aa5-227">Ondersteunde typen zijn: **GZip**, **Deflate**, **BZip2**, en **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="44aa5-227">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="44aa5-228">Ondersteunde niveaus: **optimale** en **snelst**.</span><span class="sxs-lookup"><span data-stu-id="44aa5-228">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="44aa5-229">Zie [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="44aa5-229">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="44aa5-230">Nee</span><span class="sxs-lookup"><span data-stu-id="44aa5-230">No</span></span> |

> [!NOTE]
> <span data-ttu-id="44aa5-231">U kunt geen bestandsnaam en fileFilter gelijktijdig gebruiken.</span><span class="sxs-lookup"><span data-stu-id="44aa5-231">You cannot use fileName and fileFilter simultaneously.</span></span>

### <a name="using-partitionedby-property"></a><span data-ttu-id="44aa5-232">Gebruik de eigenschap partitionedBy</span><span class="sxs-lookup"><span data-stu-id="44aa5-232">Using partitionedBy property</span></span>
<span data-ttu-id="44aa5-233">Zoals vermeld in de vorige sectie hello, kunt u een dynamische folderPath en de bestandsnaam voor de reeks tijdgegevens Hello **partitionedBy** -eigenschap [Data Factory-functies en Hallo systeemvariabelen](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="44aa5-233">As mentioned in hello previous section, you can specify a dynamic folderPath and filename for time series data with hello **partitionedBy** property, [Data Factory functions, and hello system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="44aa5-234">toounderstand meer informatie over de tijdreeks gegevenssets, planning en segmenten, Zie [gegevenssets maken](data-factory-create-datasets.md), [planning en uitvoering](data-factory-scheduling-and-execution.md), en [pijplijnen maken](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="44aa5-234">toounderstand more details on time-series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span></span>

#### <a name="sample-1"></a><span data-ttu-id="44aa5-235">Voorbeeld 1:</span><span class="sxs-lookup"><span data-stu-id="44aa5-235">Sample 1:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="44aa5-236">In dit voorbeeld {segment} is vervangen door Hallo-waarde van variabele system Data Factory Hallo SliceStart Hallo-indeling (YYYYMMDDHH).</span><span class="sxs-lookup"><span data-stu-id="44aa5-236">In this example, {Slice} is replaced with hello value of hello Data Factory system variable SliceStart in hello format (YYYYMMDDHH).</span></span> <span data-ttu-id="44aa5-237">SliceStart verwijst toostart tijd van Hallo segment.</span><span class="sxs-lookup"><span data-stu-id="44aa5-237">SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="44aa5-238">Hallo folderPath verschilt voor elk segment.</span><span class="sxs-lookup"><span data-stu-id="44aa5-238">hello folderPath is different for each slice.</span></span> <span data-ttu-id="44aa5-239">Bijvoorbeeld: wikidatagateway/wikisampledataout/2014100103 of wikidatagateway/wikisampledataout/2014100104.</span><span class="sxs-lookup"><span data-stu-id="44aa5-239">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="44aa5-240">Voorbeeld 2:</span><span class="sxs-lookup"><span data-stu-id="44aa5-240">Sample 2:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```

<span data-ttu-id="44aa5-241">In dit voorbeeld worden jaar, maand, dag en tijd van de SliceStart uitgepakt in verschillende variabelen die gebruikmaken van Hallo folderPath en de bestandsnaam eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="44aa5-241">In this example, year, month, day, and time of SliceStart are extracted into separate variables that hello folderPath and fileName properties use.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="44aa5-242">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="44aa5-242">Copy activity properties</span></span>
<span data-ttu-id="44aa5-243">Zie voor een volledige lijst met secties & eigenschappen die beschikbaar zijn voor het definiëren van activiteiten, Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="44aa5-243">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="44aa5-244">Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer gegevenssets en beleidsregels zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="44aa5-244">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span> <span data-ttu-id="44aa5-245">Dat eigenschappen beschikbaar zijn in Hallo **typeProperties** sectie van de activiteit Hallo variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="44aa5-245">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span>

<span data-ttu-id="44aa5-246">Voor de kopieeractiviteit variëren ze, afhankelijk van de soorten Hallo van bronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="44aa5-246">For Copy activity, they vary depending on hello types of sources and sinks.</span></span> <span data-ttu-id="44aa5-247">Als u gegevens uit een on-premises bestandssysteem verplaatst, u Hallo brontype instellen in de kopieeractiviteit hello te**FileSystemSource**.</span><span class="sxs-lookup"><span data-stu-id="44aa5-247">If you are moving data from an on-premises file system, you set hello source type in hello copy activity too**FileSystemSource**.</span></span> <span data-ttu-id="44aa5-248">Op dezelfde manier als u overstapt tooan gegevens op het lokale bestandssysteem, u Hallo sink-type instellen in Hallo kopieeractiviteit te**FileSystemSink**.</span><span class="sxs-lookup"><span data-stu-id="44aa5-248">Similarly, if you are moving data tooan on-premises file system, you set hello sink type in hello copy activity too**FileSystemSink**.</span></span> <span data-ttu-id="44aa5-249">Deze sectie bevat een lijst met eigenschappen die worden ondersteund door FileSystemSource en FileSystemSink.</span><span class="sxs-lookup"><span data-stu-id="44aa5-249">This section provides a list of properties supported by FileSystemSource and FileSystemSink.</span></span>

<span data-ttu-id="44aa5-250">**FileSystemSource** ondersteunt Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="44aa5-250">**FileSystemSource** supports hello following properties:</span></span>

| <span data-ttu-id="44aa5-251">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="44aa5-251">Property</span></span> | <span data-ttu-id="44aa5-252">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="44aa5-252">Description</span></span> | <span data-ttu-id="44aa5-253">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="44aa5-253">Allowed values</span></span> | <span data-ttu-id="44aa5-254">Vereist</span><span class="sxs-lookup"><span data-stu-id="44aa5-254">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="44aa5-255">Recursieve</span><span class="sxs-lookup"><span data-stu-id="44aa5-255">recursive</span></span> |<span data-ttu-id="44aa5-256">Hiermee wordt aangegeven of Hallo gegevens recursief is gelezen vanuit Hallo submappen of alleen vanuit de opgegeven map Hallo.</span><span class="sxs-lookup"><span data-stu-id="44aa5-256">Indicates whether hello data is read recursively from hello subfolders or only from hello specified folder.</span></span> |<span data-ttu-id="44aa5-257">True, False (standaard)</span><span class="sxs-lookup"><span data-stu-id="44aa5-257">True, False (default)</span></span> |<span data-ttu-id="44aa5-258">Nee</span><span class="sxs-lookup"><span data-stu-id="44aa5-258">No</span></span> |

<span data-ttu-id="44aa5-259">**FileSystemSink** ondersteunt Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="44aa5-259">**FileSystemSink** supports hello following properties:</span></span>

| <span data-ttu-id="44aa5-260">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="44aa5-260">Property</span></span> | <span data-ttu-id="44aa5-261">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="44aa5-261">Description</span></span> | <span data-ttu-id="44aa5-262">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="44aa5-262">Allowed values</span></span> | <span data-ttu-id="44aa5-263">Vereist</span><span class="sxs-lookup"><span data-stu-id="44aa5-263">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="44aa5-264">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="44aa5-264">copyBehavior</span></span> |<span data-ttu-id="44aa5-265">Hallo kopie gedrag definieert wanneer Hallo bron BlobSource of bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="44aa5-265">Defines hello copy behavior when hello source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="44aa5-266">**PreserveHierarchy:** Hallo bestandshiërarchie in de doelmap Hallo behouden blijft.</span><span class="sxs-lookup"><span data-stu-id="44aa5-266">**PreserveHierarchy:** Preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="44aa5-267">Dat wil zeggen, is relatief pad Hallo van Hallo bestand toohello bron bronmap hetzelfde als het relatieve pad van Hallo bestand toohello doel doelmap Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="44aa5-267">That is, hello relative path of hello source file toohello source folder is hello same as hello relative path of hello target file toohello target folder.</span></span><br/><br/><span data-ttu-id="44aa5-268">**FlattenHierarchy:** alle bestanden uit de bronmap Hallo worden gemaakt in Hallo eerste niveau van de doelmap.</span><span class="sxs-lookup"><span data-stu-id="44aa5-268">**FlattenHierarchy:** All files from hello source folder are created in hello first level of target folder.</span></span> <span data-ttu-id="44aa5-269">Hallo doelbestanden worden gemaakt met een automatisch gegenereerde naam.</span><span class="sxs-lookup"><span data-stu-id="44aa5-269">hello target files are created with an autogenerated name.</span></span><br/><br/><span data-ttu-id="44aa5-270">**MergeFiles:** alle bestanden uit map Hallo-tooone bronbestand worden samengevoegd.</span><span class="sxs-lookup"><span data-stu-id="44aa5-270">**MergeFiles:** Merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="44aa5-271">Als Hallo bestand naam/blob-naam wordt opgegeven, is Hallo Samengevoegde bestandsnaam Hallo opgegeven naam.</span><span class="sxs-lookup"><span data-stu-id="44aa5-271">If hello file name/blob name is specified, hello merged file name is hello specified name.</span></span> <span data-ttu-id="44aa5-272">Anders is het een automatisch gegenereerde naam.</span><span class="sxs-lookup"><span data-stu-id="44aa5-272">Otherwise, it is an auto-generated file name.</span></span> |<span data-ttu-id="44aa5-273">Nee</span><span class="sxs-lookup"><span data-stu-id="44aa5-273">No</span></span> |

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="44aa5-274">Voorbeelden van recursieve en copyBehavior</span><span class="sxs-lookup"><span data-stu-id="44aa5-274">recursive and copyBehavior examples</span></span>
<span data-ttu-id="44aa5-275">Deze sectie beschrijft Hallo resulterende gedrag van de kopieerbewerking Hallo voor verschillende combinaties van waarden voor Hallo recursieve en copyBehavior eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="44aa5-275">This section describes hello resulting behavior of hello Copy operation for different combinations of values for hello recursive and copyBehavior properties.</span></span>

| <span data-ttu-id="44aa5-276">recursieve waarde</span><span class="sxs-lookup"><span data-stu-id="44aa5-276">recursive value</span></span> | <span data-ttu-id="44aa5-277">copyBehavior waarde</span><span class="sxs-lookup"><span data-stu-id="44aa5-277">copyBehavior value</span></span> | <span data-ttu-id="44aa5-278">Resulterende gedrag</span><span class="sxs-lookup"><span data-stu-id="44aa5-278">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="44aa5-279">De waarde True</span><span class="sxs-lookup"><span data-stu-id="44aa5-279">true</span></span> |<span data-ttu-id="44aa5-280">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="44aa5-280">preserveHierarchy</span></span> |<span data-ttu-id="44aa5-281">Voor een bronmap Map1 Hello-structuur te volgen</span><span class="sxs-lookup"><span data-stu-id="44aa5-281">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="44aa5-282">Map1</span><span class="sxs-lookup"><span data-stu-id="44aa5-282">Folder1</span></span><br/><span data-ttu-id="44aa5-283">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="44aa5-283">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="44aa5-284">&nbsp;&nbsp;&nbsp;&nbsp;Bestand2</span><span class="sxs-lookup"><span data-stu-id="44aa5-284">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="44aa5-285">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="44aa5-285">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="44aa5-286">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3</span><span class="sxs-lookup"><span data-stu-id="44aa5-286">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="44aa5-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="44aa5-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="44aa5-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="44aa5-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="44aa5-289">Hallo doelmap Map1 is gemaakt met dezelfde structuur, als de bron Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="44aa5-289">hello target folder Folder1 is created with hello same structure as hello source:</span></span><br/><br/><span data-ttu-id="44aa5-290">Map1</span><span class="sxs-lookup"><span data-stu-id="44aa5-290">Folder1</span></span><br/><span data-ttu-id="44aa5-291">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="44aa5-291">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="44aa5-292">&nbsp;&nbsp;&nbsp;&nbsp;Bestand2</span><span class="sxs-lookup"><span data-stu-id="44aa5-292">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="44aa5-293">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="44aa5-293">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="44aa5-294">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3</span><span class="sxs-lookup"><span data-stu-id="44aa5-294">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="44aa5-295">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="44aa5-295">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="44aa5-296">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="44aa5-296">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span> |
| <span data-ttu-id="44aa5-297">De waarde True</span><span class="sxs-lookup"><span data-stu-id="44aa5-297">true</span></span> |<span data-ttu-id="44aa5-298">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="44aa5-298">flattenHierarchy</span></span> |<span data-ttu-id="44aa5-299">Voor een bronmap Map1 Hello-structuur te volgen</span><span class="sxs-lookup"><span data-stu-id="44aa5-299">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="44aa5-300">Map1</span><span class="sxs-lookup"><span data-stu-id="44aa5-300">Folder1</span></span><br/><span data-ttu-id="44aa5-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="44aa5-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="44aa5-302">&nbsp;&nbsp;&nbsp;&nbsp;Bestand2</span><span class="sxs-lookup"><span data-stu-id="44aa5-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="44aa5-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="44aa5-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="44aa5-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3</span><span class="sxs-lookup"><span data-stu-id="44aa5-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="44aa5-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="44aa5-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="44aa5-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="44aa5-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="44aa5-307">Hallo doel Map1 is gemaakt met de Hallo structuur te volgen:</span><span class="sxs-lookup"><span data-stu-id="44aa5-307">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="44aa5-308">Map1</span><span class="sxs-lookup"><span data-stu-id="44aa5-308">Folder1</span></span><br/><span data-ttu-id="44aa5-309">&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor File1</span><span class="sxs-lookup"><span data-stu-id="44aa5-309">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="44aa5-310">&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor bestand2</span><span class="sxs-lookup"><span data-stu-id="44aa5-310">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="44aa5-311">&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor bestand3</span><span class="sxs-lookup"><span data-stu-id="44aa5-311">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="44aa5-312">&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor File4</span><span class="sxs-lookup"><span data-stu-id="44aa5-312">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="44aa5-313">&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor File5</span><span class="sxs-lookup"><span data-stu-id="44aa5-313">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="44aa5-314">De waarde True</span><span class="sxs-lookup"><span data-stu-id="44aa5-314">true</span></span> |<span data-ttu-id="44aa5-315">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="44aa5-315">mergeFiles</span></span> |<span data-ttu-id="44aa5-316">Voor een bronmap Map1 Hello-structuur te volgen</span><span class="sxs-lookup"><span data-stu-id="44aa5-316">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="44aa5-317">Map1</span><span class="sxs-lookup"><span data-stu-id="44aa5-317">Folder1</span></span><br/><span data-ttu-id="44aa5-318">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="44aa5-318">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="44aa5-319">&nbsp;&nbsp;&nbsp;&nbsp;Bestand2</span><span class="sxs-lookup"><span data-stu-id="44aa5-319">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="44aa5-320">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="44aa5-320">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="44aa5-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3</span><span class="sxs-lookup"><span data-stu-id="44aa5-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="44aa5-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="44aa5-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="44aa5-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="44aa5-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="44aa5-324">Hallo doel Map1 is gemaakt met de Hallo structuur te volgen:</span><span class="sxs-lookup"><span data-stu-id="44aa5-324">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="44aa5-325">Map1</span><span class="sxs-lookup"><span data-stu-id="44aa5-325">Folder1</span></span><br/><span data-ttu-id="44aa5-326">&nbsp;&nbsp;&nbsp;&nbsp;File1 bestand2 + bestand3 + File4 + bestand 5 inhoud worden samengevoegd in één bestand met een automatisch gegenereerde naam.</span><span class="sxs-lookup"><span data-stu-id="44aa5-326">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with an auto-generated file name.</span></span> |
| <span data-ttu-id="44aa5-327">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="44aa5-327">false</span></span> |<span data-ttu-id="44aa5-328">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="44aa5-328">preserveHierarchy</span></span> |<span data-ttu-id="44aa5-329">Voor een bronmap Map1 Hello-structuur te volgen</span><span class="sxs-lookup"><span data-stu-id="44aa5-329">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="44aa5-330">Map1</span><span class="sxs-lookup"><span data-stu-id="44aa5-330">Folder1</span></span><br/><span data-ttu-id="44aa5-331">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="44aa5-331">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="44aa5-332">&nbsp;&nbsp;&nbsp;&nbsp;Bestand2</span><span class="sxs-lookup"><span data-stu-id="44aa5-332">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="44aa5-333">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="44aa5-333">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="44aa5-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3</span><span class="sxs-lookup"><span data-stu-id="44aa5-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="44aa5-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="44aa5-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="44aa5-336">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="44aa5-336">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="44aa5-337">Hallo doelmap Map1 is gemaakt met de Hallo structuur te volgen:</span><span class="sxs-lookup"><span data-stu-id="44aa5-337">hello target folder Folder1 is created with hello following structure:</span></span><br/><br/><span data-ttu-id="44aa5-338">Map1</span><span class="sxs-lookup"><span data-stu-id="44aa5-338">Folder1</span></span><br/><span data-ttu-id="44aa5-339">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="44aa5-339">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="44aa5-340">&nbsp;&nbsp;&nbsp;&nbsp;Bestand2</span><span class="sxs-lookup"><span data-stu-id="44aa5-340">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><span data-ttu-id="44aa5-341">Subfolder1 bestand3 File4 en File5 is niet opgenomen.</span><span class="sxs-lookup"><span data-stu-id="44aa5-341">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="44aa5-342">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="44aa5-342">false</span></span> |<span data-ttu-id="44aa5-343">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="44aa5-343">flattenHierarchy</span></span> |<span data-ttu-id="44aa5-344">Voor een bronmap Map1 Hello-structuur te volgen</span><span class="sxs-lookup"><span data-stu-id="44aa5-344">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="44aa5-345">Map1</span><span class="sxs-lookup"><span data-stu-id="44aa5-345">Folder1</span></span><br/><span data-ttu-id="44aa5-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="44aa5-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="44aa5-347">&nbsp;&nbsp;&nbsp;&nbsp;Bestand2</span><span class="sxs-lookup"><span data-stu-id="44aa5-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="44aa5-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="44aa5-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="44aa5-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3</span><span class="sxs-lookup"><span data-stu-id="44aa5-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="44aa5-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="44aa5-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="44aa5-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="44aa5-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="44aa5-352">Hallo doelmap Map1 is gemaakt met de Hallo structuur te volgen:</span><span class="sxs-lookup"><span data-stu-id="44aa5-352">hello target folder Folder1 is created with hello following structure:</span></span><br/><br/><span data-ttu-id="44aa5-353">Map1</span><span class="sxs-lookup"><span data-stu-id="44aa5-353">Folder1</span></span><br/><span data-ttu-id="44aa5-354">&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor File1</span><span class="sxs-lookup"><span data-stu-id="44aa5-354">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="44aa5-355">&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor bestand2</span><span class="sxs-lookup"><span data-stu-id="44aa5-355">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><span data-ttu-id="44aa5-356">Subfolder1 bestand3 File4 en File5 is niet opgenomen.</span><span class="sxs-lookup"><span data-stu-id="44aa5-356">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="44aa5-357">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="44aa5-357">false</span></span> |<span data-ttu-id="44aa5-358">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="44aa5-358">mergeFiles</span></span> |<span data-ttu-id="44aa5-359">Voor een bronmap Map1 Hello-structuur te volgen</span><span class="sxs-lookup"><span data-stu-id="44aa5-359">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="44aa5-360">Map1</span><span class="sxs-lookup"><span data-stu-id="44aa5-360">Folder1</span></span><br/><span data-ttu-id="44aa5-361">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="44aa5-361">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="44aa5-362">&nbsp;&nbsp;&nbsp;&nbsp;Bestand2</span><span class="sxs-lookup"><span data-stu-id="44aa5-362">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="44aa5-363">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="44aa5-363">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="44aa5-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3</span><span class="sxs-lookup"><span data-stu-id="44aa5-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="44aa5-365">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="44aa5-365">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="44aa5-366">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="44aa5-366">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="44aa5-367">Hallo doelmap Map1 is gemaakt met de Hallo structuur te volgen:</span><span class="sxs-lookup"><span data-stu-id="44aa5-367">hello target folder Folder1 is created with hello following structure:</span></span><br/><br/><span data-ttu-id="44aa5-368">Map1</span><span class="sxs-lookup"><span data-stu-id="44aa5-368">Folder1</span></span><br/><span data-ttu-id="44aa5-369">&nbsp;&nbsp;&nbsp;&nbsp;File1 + bestand2 inhoud worden samengevoegd in één bestand met een automatisch gegenereerde naam.</span><span class="sxs-lookup"><span data-stu-id="44aa5-369">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with an auto-generated file name.</span></span><br/><span data-ttu-id="44aa5-370">&nbsp;&nbsp;&nbsp;&nbsp;Automatisch gegenereerde naam voor File1</span><span class="sxs-lookup"><span data-stu-id="44aa5-370">&nbsp;&nbsp;&nbsp;&nbsp;Auto-generated name for File1</span></span><br/><br/><span data-ttu-id="44aa5-371">Subfolder1 bestand3 File4 en File5 is niet opgenomen.</span><span class="sxs-lookup"><span data-stu-id="44aa5-371">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="44aa5-372">Ondersteunde indelingen voor bestands- en compressie</span><span class="sxs-lookup"><span data-stu-id="44aa5-372">Supported file and compression formats</span></span>
<span data-ttu-id="44aa5-373">Zie [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="44aa5-373">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-examples-for-copying-data-tooand-from-file-system"></a><span data-ttu-id="44aa5-374">JSON-voorbeelden voor het kopiëren van gegevens tooand van bestandssysteem</span><span class="sxs-lookup"><span data-stu-id="44aa5-374">JSON examples for copying data tooand from file system</span></span>
<span data-ttu-id="44aa5-375">Hallo volgende voorbeelden geven voorbeeld JSON definities waarmee u een pijplijn toocreate kunt met behulp van Hallo [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="44aa5-375">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="44aa5-376">Ze geven weer hoe toocopy gegevens tooand uit een on-premises bestandssysteem en de Azure-blobopslag.</span><span class="sxs-lookup"><span data-stu-id="44aa5-376">They show how toocopy data tooand from an on-premises file system and Azure Blob storage.</span></span> <span data-ttu-id="44aa5-377">U kunt gegevens echter kopiëren *rechtstreeks* vanaf elke Hallo bronnen tooany van Hallo put die worden vermeld in [ondersteunde gegevensbronnen en put](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van de Kopieeractiviteit in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="44aa5-377">However, you can copy data *directly* from any of hello sources tooany of hello sinks listed in [Supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-an-on-premises-file-system-tooazure-blob-storage"></a><span data-ttu-id="44aa5-378">Voorbeeld: Gegevens kopiëren van een lokaal bestand system tooAzure Blob-opslag</span><span class="sxs-lookup"><span data-stu-id="44aa5-378">Example: Copy data from an on-premises file system tooAzure Blob storage</span></span>
<span data-ttu-id="44aa5-379">In dit voorbeeld laat zien hoe toocopy gegevens van een lokaal bestand system tooAzure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="44aa5-379">This sample shows how toocopy data from an on-premises file system tooAzure Blob storage.</span></span> <span data-ttu-id="44aa5-380">Hallo voorbeeld heeft Hallo Data Factory-entiteiten te volgen:</span><span class="sxs-lookup"><span data-stu-id="44aa5-380">hello sample has hello following Data Factory entities:</span></span>

* <span data-ttu-id="44aa5-381">Een gekoppelde service van het type [OnPremisesFileServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="44aa5-381">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span></span>
* <span data-ttu-id="44aa5-382">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="44aa5-382">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="44aa5-383">Invoer [gegevensset](data-factory-create-datasets.md) van het type [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="44aa5-383">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="44aa5-384">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="44aa5-384">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="44aa5-385">Een [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [FileSystemSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="44aa5-385">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="44aa5-386">Hallo voorbeeld te volgen gekopieerd timeseries gegevens van een lokaal bestand system tooAzure Blob-opslag om het uur.</span><span class="sxs-lookup"><span data-stu-id="44aa5-386">hello following sample copies time-series data from an on-premises file system tooAzure Blob storage every hour.</span></span> <span data-ttu-id="44aa5-387">Hallo JSON-eigenschappen die worden gebruikt in deze voorbeelden worden beschreven in Hallo secties na Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="44aa5-387">hello JSON properties that are used in these samples are described in hello sections after hello samples.</span></span>

<span data-ttu-id="44aa5-388">Instellen als eerste stap van Data Management Gateway volgens de instructies in Hallo [gegevens verplaatsen tussen lokale bronnen en Hallo cloud met Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="44aa5-388">As a first step, set up Data Management Gateway as per hello instructions in [Move data between on-premises sources and hello cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span></span>

<span data-ttu-id="44aa5-389">**Bestandsserver voor on-Premises gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="44aa5-389">**On-Premises File Server linked service:**</span></span>

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

<span data-ttu-id="44aa5-390">Aangeraden wordt Hallo **encryptedCredential** eigenschap Hallo in plaats daarvan **userid** en **wachtwoord** eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="44aa5-390">We recommend using hello **encryptedCredential** property instead hello **userid** and **password** properties.</span></span> <span data-ttu-id="44aa5-391">Zie [bestandsserver gekoppelde service](#linked-service-properties) voor meer informatie over deze gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="44aa5-391">See [File Server linked service](#linked-service-properties) for details about this linked service.</span></span>

<span data-ttu-id="44aa5-392">**Gekoppelde Azure Storage-service:**</span><span class="sxs-lookup"><span data-stu-id="44aa5-392">**Azure Storage linked service:**</span></span>

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

<span data-ttu-id="44aa5-393">**Lokale bestandsnaam systeem invoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="44aa5-393">**On-premises file system input dataset:**</span></span>

<span data-ttu-id="44aa5-394">Gegevens wordt opgehaald uit een nieuw bestand om het uur.</span><span class="sxs-lookup"><span data-stu-id="44aa5-394">Data is picked up from a new file every hour.</span></span> <span data-ttu-id="44aa5-395">Hallo folderPath en eigenschappen van de bestandsnaam worden bepaald op basis van Hallo begintijd van Hallo segment.</span><span class="sxs-lookup"><span data-stu-id="44aa5-395">hello folderPath and fileName properties are determined based on hello start time of hello slice.</span></span>  

<span data-ttu-id="44aa5-396">Instelling `"external": "true"` Data Factory informeert dat gegevensset Hallo externe toohello data factory is en niet door een activiteit in de gegevensfactory hello wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="44aa5-396">Setting `"external": "true"` informs Data Factory that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "OnpremisesFileSystemInput",
  "properties": {
    "type": " FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ]
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

<span data-ttu-id="44aa5-397">**Azure Blob storage-uitvoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="44aa5-397">**Azure Blob storage output dataset:**</span></span>

<span data-ttu-id="44aa5-398">Gegevens worden geschreven tooa nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="44aa5-398">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="44aa5-399">pad naar map voor blob Hallo Hallo wordt dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="44aa5-399">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="44aa5-400">mappad Hallo Hallo jaar, maand, dag en uur delen van de begintijd Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="44aa5-400">hello folder path uses hello year, month, day, and hour parts of hello start time.</span></span>

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="44aa5-401">**Een kopieeractiviteit in een pijplijn met File System-bron en sink van Blob:**</span><span class="sxs-lookup"><span data-stu-id="44aa5-401">**A copy activity in a pipeline with File System source and Blob sink:**</span></span>

<span data-ttu-id="44aa5-402">Hallo pijplijn bevat een kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur.</span><span class="sxs-lookup"><span data-stu-id="44aa5-402">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="44aa5-403">Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**FileSystemSource**, en **sink** type is ingesteld, te**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="44aa5-403">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource**, and **sink** type is set too**BlobSink**.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T19:00:00",
    "description":"Pipeline for copy activity",
    "activities":[  
      {
        "name": "OnpremisesFileSystemtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "OnpremisesFileSystemInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "FileSystemSource"
          },
          "sink": {
            "type": "BlobSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```

### <a name="example-copy-data-from-azure-sql-database-tooan-on-premises-file-system"></a><span data-ttu-id="44aa5-404">Voorbeeld: Gegevens kopiëren van Azure SQL Database tooan on-premises-bestandssysteem</span><span class="sxs-lookup"><span data-stu-id="44aa5-404">Example: Copy data from Azure SQL Database tooan on-premises file system</span></span>
<span data-ttu-id="44aa5-405">Hallo volgende ziet:</span><span class="sxs-lookup"><span data-stu-id="44aa5-405">hello following sample shows:</span></span>

* <span data-ttu-id="44aa5-406">Een gekoppelde service van het type [AzureSqlDatabase.](data-factory-azure-sql-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="44aa5-406">A linked service of type [AzureSqlDatabase.](data-factory-azure-sql-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="44aa5-407">Een gekoppelde service van het type [OnPremisesFileServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="44aa5-407">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span></span>
* <span data-ttu-id="44aa5-408">Een invoergegevensset van het type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="44aa5-408">An input dataset of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="44aa5-409">Een uitvoergegevensset van het type [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="44aa5-409">An output dataset of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="44aa5-410">Een pijplijn met een kopieeractiviteit die gebruikmaakt van [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) en [FileSystemSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="44aa5-410">A pipeline with a copy activity that uses [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) and [FileSystemSink](#copy-activity-properties).</span></span>

<span data-ttu-id="44aa5-411">Hallo voorbeeld opgehaald-timeseries-gegevens uit een Azure SQL tabel tooan on-premises bestandssysteem om het uur.</span><span class="sxs-lookup"><span data-stu-id="44aa5-411">hello sample copies time-series data from an Azure SQL table tooan on-premises file system every hour.</span></span> <span data-ttu-id="44aa5-412">Hallo JSON-eigenschappen die worden gebruikt in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="44aa5-412">hello JSON properties that are used in these samples are described in sections after hello samples.</span></span>

<span data-ttu-id="44aa5-413">**Azure SQL Database, gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="44aa5-413">**Azure SQL Database linked service:**</span></span>

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```

<span data-ttu-id="44aa5-414">**Bestandsserver voor on-Premises gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="44aa5-414">**On-Premises File Server linked service:**</span></span>

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

<span data-ttu-id="44aa5-415">Aangeraden wordt Hallo **encryptedCredential** eigenschap in plaats van Hallo **userid** en **wachtwoord** eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="44aa5-415">We recommend using hello **encryptedCredential** property instead of using hello **userid** and **password** properties.</span></span> <span data-ttu-id="44aa5-416">Zie [gekoppelde service van bestandssysteem](#linked-service-properties) voor meer informatie over deze gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="44aa5-416">See [File System linked service](#linked-service-properties) for details about this linked service.</span></span>

<span data-ttu-id="44aa5-417">**Azure SQL invoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="44aa5-417">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="44aa5-418">Hallo-voorbeeld wordt ervan uitgegaan dat u een tabel 'MijnTabel' in Azure SQL gemaakt hebt en een kolom met de naam 'timestampcolumn' voor timeseries gegevens bevat.</span><span class="sxs-lookup"><span data-stu-id="44aa5-418">hello sample assumes that you've created a table “MyTable” in Azure SQL, and it contains a column called “timestampcolumn” for time-series data.</span></span>

<span data-ttu-id="44aa5-419">Instelling ``“external”: ”true”`` Data Factory informeert dat gegevensset Hallo externe toohello data factory is en niet door een activiteit in de gegevensfactory hello wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="44aa5-419">Setting ``“external”: ”true”`` informs Data Factory that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

<span data-ttu-id="44aa5-420">**Lokale bestandsnaam uitvoergegevensset systeem:**</span><span class="sxs-lookup"><span data-stu-id="44aa5-420">**On-premises file system output dataset:**</span></span>

<span data-ttu-id="44aa5-421">Gegevens zijn gekopieerde tooa nieuw bestand om het uur.</span><span class="sxs-lookup"><span data-stu-id="44aa5-421">Data is copied tooa new file every hour.</span></span> <span data-ttu-id="44aa5-422">Hallo folderPath en de bestandsnaam voor Hallo blob zijn bepaald op basis van Hallo begintijd van Hallo segment.</span><span class="sxs-lookup"><span data-stu-id="44aa5-422">hello folderPath and fileName for hello blob are determined based on hello start time of hello slice.</span></span>

```JSON
{
  "name": "OnpremisesFileSystemOutput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ]
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

<span data-ttu-id="44aa5-423">**Een kopieeractiviteit in een pijplijn met de SQL-bron en sink van bestandssysteem:**</span><span class="sxs-lookup"><span data-stu-id="44aa5-423">**A copy activity in a pipeline with SQL source and File System sink:**</span></span>

<span data-ttu-id="44aa5-424">Hallo pijplijn bevat een kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur.</span><span class="sxs-lookup"><span data-stu-id="44aa5-424">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="44aa5-425">Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**SqlSource**, en Hallo **sink** type is ingesteld, te**FileSystemSink**.</span><span class="sxs-lookup"><span data-stu-id="44aa5-425">In hello pipeline JSON definition, hello **source** type is set too**SqlSource**, and hello **sink** type is set too**FileSystemSink**.</span></span> <span data-ttu-id="44aa5-426">Hallo SQL-query die is opgegeven voor Hallo **SqlReaderQuery** eigenschap Hallo gegevens selecteert in Hallo voorbij toocopy uur.</span><span class="sxs-lookup"><span data-stu-id="44aa5-426">hello SQL query that is specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T20:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLtoOnPremisesFile",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSQLInput"
          }
        ],
        "outputs": [
          {
            "name": "OnpremisesFileSystemOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "FileSystemSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 3,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```


<span data-ttu-id="44aa5-427">U kunt ook kolommen uit de bron gegevensset toocolumns uit sink gegevensset in de definitie van de activiteit kopiëren Hallo toewijzen.</span><span class="sxs-lookup"><span data-stu-id="44aa5-427">You can also map columns from source dataset toocolumns from sink dataset in hello copy activity definition.</span></span> <span data-ttu-id="44aa5-428">Zie voor meer informatie [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="44aa5-428">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="44aa5-429">Prestaties en afstemmen</span><span class="sxs-lookup"><span data-stu-id="44aa5-429">Performance and tuning</span></span>
 <span data-ttu-id="44aa5-430">toolearn over sleutel factoren die gevolgen Hallo-prestaties van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren toooptimize, Zie Hallo [Kopieeractiviteit prestaties en prestatieafstemming handleiding](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="44aa5-430">toolearn about key factors that impact hello performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it, see hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>
