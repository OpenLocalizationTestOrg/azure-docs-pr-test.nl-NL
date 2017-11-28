---
title: aaaMove gegevens van de lokale HDFS | Microsoft Docs
description: Meer informatie over hoe toomove gegevens van de lokale HDFS met behulp van Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 3215b82d-291a-46db-8478-eac1a3219614
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 96387e5dd089099fc2e983ab26d67c2044b973b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-on-premises-hdfs-using-azure-data-factory"></a><span data-ttu-id="a1174-103">Gegevens verplaatsen van de lokale HDFS met behulp van Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a1174-103">Move data from on-premises HDFS using Azure Data Factory</span></span>
<span data-ttu-id="a1174-104">Dit artikel wordt uitgelegd hoe toouse Kopieeractiviteit Hallo in Azure Data Factory toomove gegevens uit een lokale HDFS.</span><span class="sxs-lookup"><span data-stu-id="a1174-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises HDFS.</span></span> <span data-ttu-id="a1174-105">Dit is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit Hallo geeft.</span><span class="sxs-lookup"><span data-stu-id="a1174-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="a1174-106">U kunt gegevens uit HDFS tooany ondersteund sink gegevensarchief kopiëren.</span><span class="sxs-lookup"><span data-stu-id="a1174-106">You can copy data from HDFS tooany supported sink data store.</span></span> <span data-ttu-id="a1174-107">Zie voor een lijst van gegevens winkels ondersteund zoals sinks door kopieeractiviteit hello, Hallo [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabel.</span><span class="sxs-lookup"><span data-stu-id="a1174-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="a1174-108">Data factory ondersteunt momenteel alleen zwevend gegevens uit een gegevensarchieven lokale HDFS tooother, maar niet voor het verplaatsen van gegevens van andere gegevens winkels tooan lokale HDFS.</span><span class="sxs-lookup"><span data-stu-id="a1174-108">Data factory currently supports only moving data from an on-premises HDFS tooother data stores, but not for moving data from other data stores tooan on-premises HDFS.</span></span>

> [!NOTE]
> <span data-ttu-id="a1174-109">Kopieeractiviteit worden Hallo-bronbestand niet verwijderd nadat het is gekopieerde toohello bestemming.</span><span class="sxs-lookup"><span data-stu-id="a1174-109">Copy Activity does not delete hello source file after it is successfully copied toohello destination.</span></span> <span data-ttu-id="a1174-110">Als u toodelete Hallo-bronbestand na een geslaagde kopie moet, maakt u een aangepaste activiteit toodelete Hallo-bestand en Hallo activiteit in de pijplijn hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a1174-110">If you need toodelete hello source file after a successful copy, create a custom activity toodelete hello file and use hello activity in hello pipeline.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="a1174-111">Connectiviteit inschakelen</span><span class="sxs-lookup"><span data-stu-id="a1174-111">Enabling connectivity</span></span>
<span data-ttu-id="a1174-112">Data Factory-service ondersteunt verbindende tooon lokale HDFS met Hallo Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="a1174-112">Data Factory service supports connecting tooon-premises HDFS using hello Data Management Gateway.</span></span> <span data-ttu-id="a1174-113">Zie [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) toolearn artikel over Data Management Gateway en stapsgewijze instructies over het instellen van Hallo-gateway.</span><span class="sxs-lookup"><span data-stu-id="a1174-113">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span> <span data-ttu-id="a1174-114">Gebruik Hallo gateway tooconnect tooHDFS zelfs als deze is opgenomen in een Azure IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="a1174-114">Use hello gateway tooconnect tooHDFS even if it is hosted in an Azure IaaS VM.</span></span>

> [!NOTE]
> <span data-ttu-id="a1174-115">Zorg ervoor dat Hallo Data Management Gateway toegankelijk te**alle** Hallo [naam van knooppunt server]: [name knooppunt poort] en [knooppunt gegevensservers]: [knooppunt gegevenspoort] van Hallo Hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="a1174-115">Make sure hello Data Management Gateway can access too**ALL** hello [name node server]:[name node port] and [data node servers]:[data node port] of hello Hadoop cluster.</span></span> <span data-ttu-id="a1174-116">Standaard [naam van knooppunt poort] is 50070 en standaard [knooppunt gegevenspoort] 50075 is.</span><span class="sxs-lookup"><span data-stu-id="a1174-116">Default [name node port] is 50070, and default [data node port] is 50075.</span></span>

<span data-ttu-id="a1174-117">Terwijl u kunt de gateway installeren op Hallo dezelfde lokale machine of hello Azure VM als HDFS hello, is het raadzaam dat u Hallo-gateway installeert op een afzonderlijke computer/Azure IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="a1174-117">While you can install gateway on hello same on-premises machine or hello Azure VM as hello HDFS, we recommend that you install hello gateway on a separate machine/Azure IaaS VM.</span></span> <span data-ttu-id="a1174-118">Met gateway op een afzonderlijke computer bronconflicten vermindert en verbetert de prestaties.</span><span class="sxs-lookup"><span data-stu-id="a1174-118">Having gateway on a separate machine reduces resource contention and improves performance.</span></span> <span data-ttu-id="a1174-119">Wanneer u Hallo-gateway op een afzonderlijke computer installeert, is het Hallo-machine moeten kunnen tooaccess Hallo machine Hello HDFS.</span><span class="sxs-lookup"><span data-stu-id="a1174-119">When you install hello gateway on a separate machine, hello machine should be able tooaccess hello machine with hello HDFS.</span></span>

## <a name="getting-started"></a><span data-ttu-id="a1174-120">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="a1174-120">Getting started</span></span>
<span data-ttu-id="a1174-121">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens van een HDFS-bron verplaatst met behulp van verschillende hulpprogramma's voor API's.</span><span class="sxs-lookup"><span data-stu-id="a1174-121">You can create a pipeline with a copy activity that moves data from a HDFS source by using different tools/APIs.</span></span>

<span data-ttu-id="a1174-122">Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="a1174-122">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="a1174-123">Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met Hallo wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="a1174-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="a1174-124">U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="a1174-124">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="a1174-125">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="a1174-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="a1174-126">Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="a1174-126">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="a1174-127">Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="a1174-127">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="a1174-128">Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="a1174-128">Create **datasets** toorepresent input and output data for hello copy operation.</span></span>
3. <span data-ttu-id="a1174-129">Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="a1174-129">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="a1174-130">Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a1174-130">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="a1174-131">Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="a1174-131">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="a1174-132">Zie voor een voorbeeld met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens van een gegevensarchief HDFS zijn [JSON-voorbeeld: gegevens kopiëren van lokale HDFS tooAzure Blob](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="a1174-132">For a sample with JSON definitions for Data Factory entities that are used toocopy data from a HDFS data store, see [JSON example: Copy data from on-premises HDFS tooAzure Blob](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob) section of this article.</span></span>

<span data-ttu-id="a1174-133">Hallo volgende secties bieden informatie over de JSON-eigenschappen die gebruikt toodefine Data Factory-entiteiten specifieke tooHDFS zijn:</span><span class="sxs-lookup"><span data-stu-id="a1174-133">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooHDFS:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="a1174-134">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="a1174-134">Linked service properties</span></span>
<span data-ttu-id="a1174-135">Een gekoppelde service een gegevensfactory store tooa gegevens gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="a1174-135">A linked service links a data store tooa data factory.</span></span> <span data-ttu-id="a1174-136">Maken van een gekoppelde service van het type **Hdfs** toolink een lokale HDFS tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="a1174-136">You create a linked service of type **Hdfs** toolink an on-premises HDFS tooyour data factory.</span></span> <span data-ttu-id="a1174-137">Hallo volgende tabel biedt een beschrijving voor de JSON-elementen specifieke tooHDFS gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="a1174-137">hello following table provides description for JSON elements specific tooHDFS linked service.</span></span>

| <span data-ttu-id="a1174-138">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="a1174-138">Property</span></span> | <span data-ttu-id="a1174-139">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a1174-139">Description</span></span> | <span data-ttu-id="a1174-140">Vereist</span><span class="sxs-lookup"><span data-stu-id="a1174-140">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a1174-141">type</span><span class="sxs-lookup"><span data-stu-id="a1174-141">type</span></span> |<span data-ttu-id="a1174-142">Hallo type eigenschap moet worden ingesteld op: **Hdfs**</span><span class="sxs-lookup"><span data-stu-id="a1174-142">hello type property must be set to: **Hdfs**</span></span> |<span data-ttu-id="a1174-143">Ja</span><span class="sxs-lookup"><span data-stu-id="a1174-143">Yes</span></span> |
| <span data-ttu-id="a1174-144">URL</span><span class="sxs-lookup"><span data-stu-id="a1174-144">Url</span></span> |<span data-ttu-id="a1174-145">URL toohello HDFS</span><span class="sxs-lookup"><span data-stu-id="a1174-145">URL toohello HDFS</span></span> |<span data-ttu-id="a1174-146">Ja</span><span class="sxs-lookup"><span data-stu-id="a1174-146">Yes</span></span> |
| <span data-ttu-id="a1174-147">authenticationType</span><span class="sxs-lookup"><span data-stu-id="a1174-147">authenticationType</span></span> |<span data-ttu-id="a1174-148">Anoniem, of Windows.</span><span class="sxs-lookup"><span data-stu-id="a1174-148">Anonymous, or Windows.</span></span> <br><br> <span data-ttu-id="a1174-149">toouse **Kerberos-verificatie** voor HDFS-connector te verwijzen[in deze sectie](#use-kerberos-authentication-for-hdfs-connector) tooset van uw on-premises omgeving dienovereenkomstig.</span><span class="sxs-lookup"><span data-stu-id="a1174-149">toouse **Kerberos authentication** for HDFS connector, refer too[this section](#use-kerberos-authentication-for-hdfs-connector) tooset up your on-premises environment accordingly.</span></span> |<span data-ttu-id="a1174-150">Ja</span><span class="sxs-lookup"><span data-stu-id="a1174-150">Yes</span></span> |
| <span data-ttu-id="a1174-151">Gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="a1174-151">userName</span></span> |<span data-ttu-id="a1174-152">Gebruikersnaam voor Windows-verificatie.</span><span class="sxs-lookup"><span data-stu-id="a1174-152">Username for Windows authentication.</span></span> |<span data-ttu-id="a1174-153">Ja (voor Windows-verificatie)</span><span class="sxs-lookup"><span data-stu-id="a1174-153">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="a1174-154">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="a1174-154">password</span></span> |<span data-ttu-id="a1174-155">Wachtwoord voor Windows-verificatie.</span><span class="sxs-lookup"><span data-stu-id="a1174-155">Password for Windows authentication.</span></span> |<span data-ttu-id="a1174-156">Ja (voor Windows-verificatie)</span><span class="sxs-lookup"><span data-stu-id="a1174-156">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="a1174-157">gatewayName</span><span class="sxs-lookup"><span data-stu-id="a1174-157">gatewayName</span></span> |<span data-ttu-id="a1174-158">Naam van Hallo-gateway die Hallo Data Factory-service moet tooconnect toohello HDFS gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a1174-158">Name of hello gateway that hello Data Factory service should use tooconnect toohello HDFS.</span></span> |<span data-ttu-id="a1174-159">Ja</span><span class="sxs-lookup"><span data-stu-id="a1174-159">Yes</span></span> |
| <span data-ttu-id="a1174-160">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="a1174-160">encryptedCredential</span></span> |<span data-ttu-id="a1174-161">[Nieuwe AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) uitvoer van de referentie voor Hallo-toegang.</span><span class="sxs-lookup"><span data-stu-id="a1174-161">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) output of hello access credential.</span></span> |<span data-ttu-id="a1174-162">Nee</span><span class="sxs-lookup"><span data-stu-id="a1174-162">No</span></span> |

### <a name="using-anonymous-authentication"></a><span data-ttu-id="a1174-163">Anonieme verificatie</span><span class="sxs-lookup"><span data-stu-id="a1174-163">Using Anonymous authentication</span></span>

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "userName": "hadoop",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-windows-authentication"></a><span data-ttu-id="a1174-164">Met behulp van Windows-verificatie</span><span class="sxs-lookup"><span data-stu-id="a1174-164">Using Windows authentication</span></span>

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```
## <a name="dataset-properties"></a><span data-ttu-id="a1174-165">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="a1174-165">Dataset properties</span></span>
<span data-ttu-id="a1174-166">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="a1174-166">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="a1174-167">Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure blob-, Azure-tabel, enz.).</span><span class="sxs-lookup"><span data-stu-id="a1174-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="a1174-168">Hallo **typeProperties** sectie verschilt voor elk type gegevensset en bevat informatie over Hallo-locatie van gegevens in het gegevensarchief Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="a1174-168">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="a1174-169">Hallo typeProperties sectie voor de gegevensset van het type **FileShare** (inclusief HDFS gegevensset) heeft Hallo volgende eigenschappen</span><span class="sxs-lookup"><span data-stu-id="a1174-169">hello typeProperties section for dataset of type **FileShare** (which includes HDFS dataset) has hello following properties</span></span>

| <span data-ttu-id="a1174-170">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="a1174-170">Property</span></span> | <span data-ttu-id="a1174-171">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a1174-171">Description</span></span> | <span data-ttu-id="a1174-172">Vereist</span><span class="sxs-lookup"><span data-stu-id="a1174-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a1174-173">folderPath</span><span class="sxs-lookup"><span data-stu-id="a1174-173">folderPath</span></span> |<span data-ttu-id="a1174-174">Pad toohello map.</span><span class="sxs-lookup"><span data-stu-id="a1174-174">Path toohello folder.</span></span> <span data-ttu-id="a1174-175">Voorbeeld:`myfolder`</span><span class="sxs-lookup"><span data-stu-id="a1174-175">Example: `myfolder`</span></span><br/><br/><span data-ttu-id="a1174-176">Gebruik van escape-teken ' \ ' voor speciale tekens in Hallo-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="a1174-176">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="a1174-177">Bijvoorbeeld: map opgeven voor folder\subfolder,\\\\submap en geef voor d:\samplefolder, d:\\\\Voorbeeldmap.</span><span class="sxs-lookup"><span data-stu-id="a1174-177">For example: for folder\subfolder, specify folder\\\\subfolder and for d:\samplefolder, specify d:\\\\samplefolder.</span></span><br/><br/><span data-ttu-id="a1174-178">U kunt deze eigenschap combineren met **partitionBy** toohave mappaden op basis van het segment beginnen of eindigen-datums en tijden.</span><span class="sxs-lookup"><span data-stu-id="a1174-178">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="a1174-179">Ja</span><span class="sxs-lookup"><span data-stu-id="a1174-179">Yes</span></span> |
| <span data-ttu-id="a1174-180">fileName</span><span class="sxs-lookup"><span data-stu-id="a1174-180">fileName</span></span> |<span data-ttu-id="a1174-181">Hallo-naam van Hallo-bestand opgeven in Hallo **folderPath** als u wilt dat Hallo tabel toorefer tooa specifiek bestand in map Hallo.</span><span class="sxs-lookup"><span data-stu-id="a1174-181">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="a1174-182">Als u geen waarde voor deze eigenschap niet opgeeft, wijst Hallo tabel tooall bestanden in de map Hallo.</span><span class="sxs-lookup"><span data-stu-id="a1174-182">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="a1174-183">Wanneer fileName niet voor een uitvoergegevensset opgegeven is, zou Hallo van Hallo gegenereerd bestand in worden Hallo volgt deze indeling:</span><span class="sxs-lookup"><span data-stu-id="a1174-183">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="a1174-184">Gegevens. <Guid>.txt (voorbeeld:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="a1174-184">Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="a1174-185">Nee</span><span class="sxs-lookup"><span data-stu-id="a1174-185">No</span></span> |
| <span data-ttu-id="a1174-186">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="a1174-186">partitionedBy</span></span> |<span data-ttu-id="a1174-187">partitionedBy mag gebruikte toospecify een dynamische folderPath bestandsnaam op van de reeksgegevens.</span><span class="sxs-lookup"><span data-stu-id="a1174-187">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="a1174-188">Voorbeeld: folderPath geparametriseerde voor elk uur van gegevens.</span><span class="sxs-lookup"><span data-stu-id="a1174-188">Example: folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="a1174-189">Nee</span><span class="sxs-lookup"><span data-stu-id="a1174-189">No</span></span> |
| <span data-ttu-id="a1174-190">Indeling</span><span class="sxs-lookup"><span data-stu-id="a1174-190">format</span></span> | <span data-ttu-id="a1174-191">Hallo na indelingstypen worden ondersteund: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="a1174-191">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="a1174-192">Set Hallo **type** eigenschap onder indeling tooone van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="a1174-192">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="a1174-193">Zie voor meer informatie [tekstindeling](data-factory-supported-file-and-compression-formats.md#text-format), [Json-indeling](data-factory-supported-file-and-compression-formats.md#json-format), [Avro-indeling](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc indeling](data-factory-supported-file-and-compression-formats.md#orc-format), en [parketvloeren indeling](data-factory-supported-file-and-compression-formats.md#parquet-format) secties.</span><span class="sxs-lookup"><span data-stu-id="a1174-193">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="a1174-194">Als u wilt dat te**kopiëren van bestanden als-is** tussen bestandsgebaseerde winkels (binaire kopiëren) Hallo indeling sectie in beide definities invoer en uitvoer gegevensset overslaan.</span><span class="sxs-lookup"><span data-stu-id="a1174-194">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="a1174-195">Nee</span><span class="sxs-lookup"><span data-stu-id="a1174-195">No</span></span> |
| <span data-ttu-id="a1174-196">Compressie</span><span class="sxs-lookup"><span data-stu-id="a1174-196">compression</span></span> | <span data-ttu-id="a1174-197">Hallo-type en compressieniveau voor Hallo gegevens opgeven.</span><span class="sxs-lookup"><span data-stu-id="a1174-197">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="a1174-198">Ondersteunde typen zijn: **GZip**, **Deflate**, **BZip2**, en **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="a1174-198">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="a1174-199">Ondersteunde niveaus: **optimale** en **snelst**.</span><span class="sxs-lookup"><span data-stu-id="a1174-199">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="a1174-200">Zie voor meer informatie [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="a1174-200">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="a1174-201">Nee</span><span class="sxs-lookup"><span data-stu-id="a1174-201">No</span></span> |

> [!NOTE]
> <span data-ttu-id="a1174-202">bestandsnaam en fileFilter worden niet gelijktijdig gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a1174-202">filename and fileFilter cannot be used simultaneously.</span></span>

### <a name="using-partionedby-property"></a><span data-ttu-id="a1174-203">Gebruik de eigenschap partionedBy</span><span class="sxs-lookup"><span data-stu-id="a1174-203">Using partionedBy property</span></span>
<span data-ttu-id="a1174-204">Zoals vermeld in de vorige sectie hello, kunt u een dynamische folderPath en de bestandsnaam voor de reeks tijdgegevens Hello **partitionedBy** -eigenschap [Data Factory-functies en Hallo systeemvariabelen](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="a1174-204">As mentioned in hello previous section, you can specify a dynamic folderPath and filename for time series data with hello **partitionedBy** property, [Data Factory functions, and hello system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="a1174-205">toolearn meer informatie over het time series gegevenssets, planning en segmenten, Zie [gegevenssets maken](data-factory-create-datasets.md), [planning en uitvoering](data-factory-scheduling-and-execution.md), en [pijplijnen maken](data-factory-create-pipelines.md) artikelen.</span><span class="sxs-lookup"><span data-stu-id="a1174-205">toolearn more about time series datasets, scheduling, and slices, see [Creating Datasets](data-factory-create-datasets.md), [Scheduling & Execution](data-factory-scheduling-and-execution.md), and [Creating Pipelines](data-factory-create-pipelines.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="a1174-206">Voorbeeld 1:</span><span class="sxs-lookup"><span data-stu-id="a1174-206">Sample 1:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="a1174-207">In dit voorbeeld {segment} is vervangen door de waarde van de Hallo van Data Factory systeemvariabele SliceStart Hallo-indeling (YYYYMMDDHH) opgegeven.</span><span class="sxs-lookup"><span data-stu-id="a1174-207">In this example {Slice} is replaced with hello value of Data Factory system variable SliceStart in hello format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="a1174-208">Hallo SliceStart verwijst toostart tijd van Hallo segment.</span><span class="sxs-lookup"><span data-stu-id="a1174-208">hello SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="a1174-209">Hallo folderPath verschilt voor elk segment.</span><span class="sxs-lookup"><span data-stu-id="a1174-209">hello folderPath is different for each slice.</span></span> <span data-ttu-id="a1174-210">Bijvoorbeeld: wikidatagateway/wikisampledataout/2014100103 of wikidatagateway/wikisampledataout/2014100104.</span><span class="sxs-lookup"><span data-stu-id="a1174-210">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="a1174-211">Voorbeeld 2:</span><span class="sxs-lookup"><span data-stu-id="a1174-211">Sample 2:</span></span>

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
<span data-ttu-id="a1174-212">In dit voorbeeld worden jaar, maand, dag en tijd van de SliceStart uitgepakt in verschillende variabelen die worden gebruikt door de eigenschappen voor folderPath en de bestandsnaam.</span><span class="sxs-lookup"><span data-stu-id="a1174-212">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="a1174-213">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="a1174-213">Copy activity properties</span></span>
<span data-ttu-id="a1174-214">Zie voor een volledige lijst met secties & eigenschappen die beschikbaar zijn voor het definiëren van activiteiten, Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="a1174-214">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="a1174-215">Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en beleidsregels zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="a1174-215">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="a1174-216">Terwijl de eigenschappen die beschikbaar zijn in Hallo typeProperties gedeelte van de activiteit Hallo variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="a1174-216">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="a1174-217">Voor de kopieeractiviteit variëren ze, afhankelijk van de soorten Hallo van bronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="a1174-217">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="a1174-218">Voor de Kopieeractiviteit, wanneer de bron van het type **FileSystemSource** Hallo volgende eigenschappen beschikbaar zijn in de sectie typeProperties:</span><span class="sxs-lookup"><span data-stu-id="a1174-218">For Copy Activity, when source is of type **FileSystemSource** hello following properties are available in typeProperties section:</span></span>

<span data-ttu-id="a1174-219">**FileSystemSource** ondersteunt Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="a1174-219">**FileSystemSource** supports hello following properties:</span></span>

| <span data-ttu-id="a1174-220">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="a1174-220">Property</span></span> | <span data-ttu-id="a1174-221">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a1174-221">Description</span></span> | <span data-ttu-id="a1174-222">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="a1174-222">Allowed values</span></span> | <span data-ttu-id="a1174-223">Vereist</span><span class="sxs-lookup"><span data-stu-id="a1174-223">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a1174-224">Recursieve</span><span class="sxs-lookup"><span data-stu-id="a1174-224">recursive</span></span> |<span data-ttu-id="a1174-225">Hiermee wordt aangegeven of Hallo gegevens recursief is gelezen vanuit Hallo submappen of alleen vanuit de opgegeven map Hallo.</span><span class="sxs-lookup"><span data-stu-id="a1174-225">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="a1174-226">True, False (standaard)</span><span class="sxs-lookup"><span data-stu-id="a1174-226">True, False (default)</span></span> |<span data-ttu-id="a1174-227">Nee</span><span class="sxs-lookup"><span data-stu-id="a1174-227">No</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="a1174-228">Ondersteunde indelingen voor bestands- en compressie</span><span class="sxs-lookup"><span data-stu-id="a1174-228">Supported file and compression formats</span></span>
<span data-ttu-id="a1174-229">Zie [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a1174-229">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-example-copy-data-from-on-premises-hdfs-tooazure-blob"></a><span data-ttu-id="a1174-230">JSON-voorbeeld: gegevens kopiëren van lokale HDFS tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="a1174-230">JSON example: Copy data from on-premises HDFS tooAzure Blob</span></span>
<span data-ttu-id="a1174-231">In dit voorbeeld laat zien hoe toocopy gegevens uit een lokale HDFS tooAzure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="a1174-231">This sample shows how toocopy data from an on-premises HDFS tooAzure Blob Storage.</span></span> <span data-ttu-id="a1174-232">Echter, de gegevens kunnen worden gekopieerd **rechtstreeks** tooany van Hallo put vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van Hallo Kopieeractiviteit in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="a1174-232">However, data can be copied **directly** tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="a1174-233">Hallo-voorbeeld bevat JSON-definities voor Hallo Data Factory-entiteiten te volgen.</span><span class="sxs-lookup"><span data-stu-id="a1174-233">hello sample provides JSON definitions for hello following Data Factory entities.</span></span> <span data-ttu-id="a1174-234">U kunt deze definities toocreate een pijplijn toocopy gegevens uit HDFS tooAzure Blob Storage gebruiken met behulp van [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="a1174-234">You can use these definitions toocreate a pipeline toocopy data from HDFS tooAzure Blob Storage by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span>

1. <span data-ttu-id="a1174-235">Een gekoppelde service van het type [OnPremisesHdfs](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a1174-235">A linked service of type [OnPremisesHdfs](#linked-service-properties).</span></span>
2. <span data-ttu-id="a1174-236">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a1174-236">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="a1174-237">Invoer [gegevensset](data-factory-create-datasets.md) van het type [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a1174-237">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
4. <span data-ttu-id="a1174-238">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a1174-238">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="a1174-239">Een [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [FileSystemSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="a1174-239">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="a1174-240">Hallo-voorbeeld worden gegevens gekopieerd van een lokale HDFS tooan Azure blob elk uur.</span><span class="sxs-lookup"><span data-stu-id="a1174-240">hello sample copies data from an on-premises HDFS tooan Azure blob every hour.</span></span> <span data-ttu-id="a1174-241">Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="a1174-241">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="a1174-242">Instellen als eerste stap Hallo data management gateway.</span><span class="sxs-lookup"><span data-stu-id="a1174-242">As a first step, set up hello data management gateway.</span></span> <span data-ttu-id="a1174-243">instructies in Hallo Hallo [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="a1174-243">hello instructions in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="a1174-244">**HDFS gekoppelde service:** in dit voorbeeld gebruikt Hallo Windows-verificatie.</span><span class="sxs-lookup"><span data-stu-id="a1174-244">**HDFS linked service:** This example uses hello Windows authentication.</span></span> <span data-ttu-id="a1174-245">Zie [HDFS gekoppelde service](#linked-service-properties) sectie voor verschillende soorten verificatie die u kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a1174-245">See [HDFS linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON
{
    "name": "HDFSLinkedService",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

<span data-ttu-id="a1174-246">**Gekoppelde Azure Storage-service:**</span><span class="sxs-lookup"><span data-stu-id="a1174-246">**Azure Storage linked service:**</span></span>

```JSON
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

<span data-ttu-id="a1174-247">**HDFS invoergegevensset:** deze gegevensset verwijst toohello HDFS map DataTransfer/UnitTest /.</span><span class="sxs-lookup"><span data-stu-id="a1174-247">**HDFS input dataset:** This dataset refers toohello HDFS folder DataTransfer/UnitTest/.</span></span> <span data-ttu-id="a1174-248">Hallo pijplijn kopieert alle Hallo-bestanden in deze map toohello bestemming.</span><span class="sxs-lookup"><span data-stu-id="a1174-248">hello pipeline copies all hello files in this folder toohello destination.</span></span>

<span data-ttu-id="a1174-249">Instelling 'extern': 'true' informeert Hallo Data Factory-service die gegevensset Hallo externe toohello data factory is en niet door een activiteit in de gegevensfactory hello wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="a1174-249">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
    "name": "InputDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "HDFSLinkedService",
        "typeProperties": {
            "folderPath": "DataTransfer/UnitTest/"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

<span data-ttu-id="a1174-250">**Azure Blob-uitvoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="a1174-250">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="a1174-251">Gegevens worden geschreven tooa nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="a1174-251">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="a1174-252">pad naar map voor blob Hallo Hallo wordt dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="a1174-252">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="a1174-253">Hallo mappad jaar, maand, dag en uur delen van de begintijd Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a1174-253">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```JSON
{
    "name": "OutputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/hdfs/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
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
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="a1174-254">**Een kopieeractiviteit in een pijplijn met File System-bron en sink van Blob:**</span><span class="sxs-lookup"><span data-stu-id="a1174-254">**A copy activity in a pipeline with File System source and Blob sink:**</span></span>

<span data-ttu-id="a1174-255">Hallo pijplijn bevat een Kopieeractiviteit die is geconfigureerd toouse deze invoer- en uitvoergegevenssets en geplande toorun is om het uur.</span><span class="sxs-lookup"><span data-stu-id="a1174-255">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="a1174-256">Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**FileSystemSource** en **sink** type is ingesteld, te**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="a1174-256">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="a1174-257">Hallo SQL-query is opgegeven voor Hallo **query** eigenschap Hallo gegevens selecteert in Hallo voorbij toocopy uur.</span><span class="sxs-lookup"><span data-stu-id="a1174-257">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```JSON
{
    "name": "pipeline",
    "properties":
    {
        "activities":
        [
            {
                "name": "HdfsToBlobCopy",
                "inputs": [ {"name": "InputDataset"} ],
                "outputs": [ {"name": "OutputDataset"} ],
                "type": "Copy",
                "typeProperties":
                {
                    "source":
                    {
                        "type": "FileSystemSource"
                    },
                    "sink":
                    {
                        "type": "BlobSink"
                    }
                },
                "policy":
                {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "00:05:00"
                }
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="use-kerberos-authentication-for-hdfs-connector"></a><span data-ttu-id="a1174-258">Kerberos-verificatie gebruiken voor HDFS-connector</span><span class="sxs-lookup"><span data-stu-id="a1174-258">Use Kerberos authentication for HDFS connector</span></span>
<span data-ttu-id="a1174-259">Er zijn twee opties tooset up Hallo on-premises omgeving dus als toouse Kerberos-verificatie in HDFS-connector.</span><span class="sxs-lookup"><span data-stu-id="a1174-259">There are two options tooset up hello on-premises environment so as toouse Kerberos Authentication in HDFS connector.</span></span> <span data-ttu-id="a1174-260">U kunt kiezen Hallo een beter past bij uw aanvraag.</span><span class="sxs-lookup"><span data-stu-id="a1174-260">You can choose hello one better fits your case.</span></span>
* <span data-ttu-id="a1174-261">Optie 1: [Join gatewaycomputer in Kerberos-realm](#kerberos-join-realm)</span><span class="sxs-lookup"><span data-stu-id="a1174-261">Option 1: [Join gateway machine in Kerberos realm](#kerberos-join-realm)</span></span>
* <span data-ttu-id="a1174-262">Optie 2: [wederzijdse vertrouwensrelatie tussen Windows-domein en Kerberos-realm inschakelen](#kerberos-mutual-trust)</span><span class="sxs-lookup"><span data-stu-id="a1174-262">Option 2: [Enable mutual trust between Windows domain and Kerberos realm](#kerberos-mutual-trust)</span></span>

### <span data-ttu-id="a1174-263"><a name="kerberos-join-realm"></a>Optie 1: Join gatewaycomputer in Kerberos-realm</span><span class="sxs-lookup"><span data-stu-id="a1174-263"><a name="kerberos-join-realm"></a>Option 1: Join gateway machine in Kerberos realm</span></span>

#### <a name="requirement"></a><span data-ttu-id="a1174-264">Vereiste:</span><span class="sxs-lookup"><span data-stu-id="a1174-264">Requirement:</span></span>

* <span data-ttu-id="a1174-265">Hallo gatewaycomputer moet toojoin Hallo Kerberos-realm en kan niet deelnemen aan een Windows-domein.</span><span class="sxs-lookup"><span data-stu-id="a1174-265">hello gateway machine needs toojoin hello Kerberos realm and can’t join any Windows domain.</span></span>

#### <a name="how-tooconfigure"></a><span data-ttu-id="a1174-266">Hoe tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="a1174-266">How tooconfigure:</span></span>

<span data-ttu-id="a1174-267">**Op de gatewaycomputer:**</span><span class="sxs-lookup"><span data-stu-id="a1174-267">**On gateway machine:**</span></span>

1.  <span data-ttu-id="a1174-268">Voer Hallo **Ksetup** hulpprogramma tooconfigure Hallo Kerberos KDC-server en de standaardrealm.</span><span class="sxs-lookup"><span data-stu-id="a1174-268">Run hello **Ksetup** utility tooconfigure hello Kerberos KDC server and realm.</span></span>

    <span data-ttu-id="a1174-269">Hallo-machine moet worden geconfigureerd als lid van een werkgroep, omdat een Kerberos-realm af van een Windows-domein wijkt.</span><span class="sxs-lookup"><span data-stu-id="a1174-269">hello machine must be configured as a member of a workgroup since a Kerberos realm is different from a Windows domain.</span></span> <span data-ttu-id="a1174-270">Dit kan worden bereikt door Kerberos-realm Hallo instellen en als volgt een KDC-server toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="a1174-270">This can be achieved by setting hello Kerberos realm and adding a KDC server as follows.</span></span> <span data-ttu-id="a1174-271">Vervang *REALM.COM* met uw eigen respectieve realm indien nodig.</span><span class="sxs-lookup"><span data-stu-id="a1174-271">Replace *REALM.COM* with your own respective realm as needed.</span></span>

            C:> Ksetup /setdomain REALM.COM
            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>

    <span data-ttu-id="a1174-272">**Opnieuw opstarten** Hallo machine na het uitvoeren van deze opdrachten 2.</span><span class="sxs-lookup"><span data-stu-id="a1174-272">**Restart** hello machine after executing these 2 commands.</span></span>

2.  <span data-ttu-id="a1174-273">Controleer de configuratie Hallo met **Ksetup** opdracht.</span><span class="sxs-lookup"><span data-stu-id="a1174-273">Verify hello configuration with **Ksetup** command.</span></span> <span data-ttu-id="a1174-274">Hallo-uitvoer moet als volgt:</span><span class="sxs-lookup"><span data-stu-id="a1174-274">hello output should be like:</span></span>

            C:> Ksetup
            default realm = REALM.COM (external)
            REALM.com:
                kdc = <your_kdc_server_address>

<span data-ttu-id="a1174-275">**In Azure Data Factory:**</span><span class="sxs-lookup"><span data-stu-id="a1174-275">**In Azure Data Factory:**</span></span>

* <span data-ttu-id="a1174-276">Configureren met behulp Hallo HDFS connector **Windows-verificatie** samen met de Kerberos-principal name en wachtwoord tooconnect toohello HDFS gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="a1174-276">Configure hello HDFS connector using **Windows authentication** together with your Kerberos principal name and password tooconnect toohello HDFS data source.</span></span> <span data-ttu-id="a1174-277">Controleer [eigenschappen van de gekoppelde Service HDFS](#linked-service-properties) sectie over configuratie-informatie.</span><span class="sxs-lookup"><span data-stu-id="a1174-277">Check [HDFS Linked Service properties](#linked-service-properties) section on configuration details.</span></span>

### <span data-ttu-id="a1174-278"><a name="kerberos-mutual-trust"></a>Optie 2: Wederzijdse vertrouwensrelatie tussen Windows-domein en Kerberos-realm inschakelen</span><span class="sxs-lookup"><span data-stu-id="a1174-278"><a name="kerberos-mutual-trust"></a>Option 2: Enable mutual trust between Windows domain and Kerberos realm</span></span>

#### <a name="requirement"></a><span data-ttu-id="a1174-279">Vereiste:</span><span class="sxs-lookup"><span data-stu-id="a1174-279">Requirement:</span></span>
*   <span data-ttu-id="a1174-280">Hallo gatewaycomputer moet lid worden van een Windows-domein.</span><span class="sxs-lookup"><span data-stu-id="a1174-280">hello gateway machine must join a Windows domain.</span></span>
*   <span data-ttu-id="a1174-281">U moet de machtiging tooupdate Hallo van de domeincontroller-instellingen.</span><span class="sxs-lookup"><span data-stu-id="a1174-281">You need permission tooupdate hello domain controller's settings.</span></span>

#### <a name="how-tooconfigure"></a><span data-ttu-id="a1174-282">Hoe tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="a1174-282">How tooconfigure:</span></span>

> [!NOTE]
> <span data-ttu-id="a1174-283">Vervang REALM.COM en AD.COM in Hallo zelfstudie met uw eigen respectieve realm en de domeincontroller na indien nodig.</span><span class="sxs-lookup"><span data-stu-id="a1174-283">Replace REALM.COM and AD.COM in hello following tutorial with your own respective realm and domain controller as needed.</span></span>

<span data-ttu-id="a1174-284">**Op de KDC-server:**</span><span class="sxs-lookup"><span data-stu-id="a1174-284">**On KDC server:**</span></span>

1.  <span data-ttu-id="a1174-285">Hallo KDC configuratie in bewerken **krb5.conf** bestand toolet KDC vertrouwt Windows-domein toohello na configuratiesjabloon verwijst.</span><span class="sxs-lookup"><span data-stu-id="a1174-285">Edit hello KDC configuration in **krb5.conf** file toolet KDC trust Windows Domain referring toohello following configuration template.</span></span> <span data-ttu-id="a1174-286">Standaard Hallo configuratie bevindt zich op **/etc/krb5.conf**.</span><span class="sxs-lookup"><span data-stu-id="a1174-286">By default, hello configuration is located at **/etc/krb5.conf**.</span></span>

            [logging]
             default = FILE:/var/log/krb5libs.log
             kdc = FILE:/var/log/krb5kdc.log
             admin_server = FILE:/var/log/kadmind.log

            [libdefaults]
             default_realm = REALM.COM
             dns_lookup_realm = false
             dns_lookup_kdc = false
             ticket_lifetime = 24h
             renew_lifetime = 7d
             forwardable = true

            [realms]
             REALM.COM = {
              kdc = node.REALM.COM
              admin_server = node.REALM.COM
             }
            AD.COM = {
             kdc = windc.ad.com
             admin_server = windc.ad.com
            }

            [domain_realm]
             .REALM.COM = REALM.COM
             REALM.COM = REALM.COM
             .ad.com = AD.COM
             ad.com = AD.COM

            [capaths]
             AD.COM = {
              REALM.COM = .
             }

  <span data-ttu-id="a1174-287">**Opnieuw opstarten** Hallo KDC-service na de configuratie.</span><span class="sxs-lookup"><span data-stu-id="a1174-287">**Restart** hello KDC service after configuration.</span></span>

2.  <span data-ttu-id="a1174-288">Voorbereiden van een principal met de naam  **krbtgt/REALM.COM@AD.COM**  in de KDC-server met volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="a1174-288">Prepare a principal named **krbtgt/REALM.COM@AD.COM** in KDC server with hello following command:</span></span>

            Kadmin> addprinc krbtgt/REALM.COM@AD.COM

3.  <span data-ttu-id="a1174-289">In **hadoop.security.auth_to_local** HDFS-serviceconfiguratie bestand, het toevoegen van `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.</span><span class="sxs-lookup"><span data-stu-id="a1174-289">In **hadoop.security.auth_to_local** HDFS service configuration file, add `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.</span></span>

<span data-ttu-id="a1174-290">**Op de domeincontroller:**</span><span class="sxs-lookup"><span data-stu-id="a1174-290">**On domain controller:**</span></span>

1.  <span data-ttu-id="a1174-291">Voer de volgende Hallo **Ksetup** tooadd een vermelding realm-opdrachten:</span><span class="sxs-lookup"><span data-stu-id="a1174-291">Run hello following **Ksetup** commands tooadd a realm entry:</span></span>

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

2.  <span data-ttu-id="a1174-292">Een vertrouwensrelatie van Windows-domein tooKerberos Realm.</span><span class="sxs-lookup"><span data-stu-id="a1174-292">Establish trust from Windows Domain tooKerberos Realm.</span></span> <span data-ttu-id="a1174-293">[wachtwoord] is Hallo wachtwoord voor Hallo principal  **krbtgt/REALM.COM@AD.COM** .</span><span class="sxs-lookup"><span data-stu-id="a1174-293">[password] is hello password for hello principal **krbtgt/REALM.COM@AD.COM**.</span></span>

            C:> netdom trust REALM.COM /Domain: AD.COM /add /realm /passwordt:[password]

3.  <span data-ttu-id="a1174-294">Selecteer de versleutelingsalgoritme die worden gebruikt in Kerberos.</span><span class="sxs-lookup"><span data-stu-id="a1174-294">Select encryption algorithm used in Kerberos.</span></span>

    1. <span data-ttu-id="a1174-295">Ga tooServer Manager > Group Policy Management > Domain > groepsbeleidsobjecten > standaard of actieve domeinbeleid en bewerken.</span><span class="sxs-lookup"><span data-stu-id="a1174-295">Go tooServer Manager > Group Policy Management > Domain > Group Policy Objects > Default or Active Domain Policy, and Edit.</span></span>

    2. <span data-ttu-id="a1174-296">In Hallo **Editor voor Groepsbeleidsbeheer** pop-upvenster, Ga tooComputer Configuration > beleidsregels > Windows-instellingen > Beveiligingsinstellingen > lokaal beleid > beveiligingsopties, en configureer **netwerk beveiliging: Configureer versleutelingstypen voor Kerberos toegestaan**.</span><span class="sxs-lookup"><span data-stu-id="a1174-296">In hello **Group Policy Management Editor** popup window, go tooComputer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Security Options, and configure **Network security: Configure Encryption types allowed for Kerberos**.</span></span>

    3. <span data-ttu-id="a1174-297">Selecteer Hallo versleutelingsalgoritme gewenste toouse wanneer een verbinding tussen tooKDC.</span><span class="sxs-lookup"><span data-stu-id="a1174-297">Select hello encryption algorithm you want toouse when connect tooKDC.</span></span> <span data-ttu-id="a1174-298">Doorgaans kunt u gewoon alle Hallo opties selecteren.</span><span class="sxs-lookup"><span data-stu-id="a1174-298">Commonly, you can simply select all hello options.</span></span>

        ![Configuratie-versleutelingstypen voor Kerberos](media/data-factory-hdfs-connector/config-encryption-types-for-kerberos.png)

    4. <span data-ttu-id="a1174-300">Gebruik **Ksetup** opdracht toospecify Hallo versleuteling algoritme toobe gebruikt op Hallo specifieke REALM.</span><span class="sxs-lookup"><span data-stu-id="a1174-300">Use **Ksetup** command toospecify hello encryption algorithm toobe used on hello specific REALM.</span></span>

                C:> ksetup /SetEncTypeAttr REALM.COM DES-CBC-CRC DES-CBC-MD5 RC4-HMAC-MD5 AES128-CTS-HMAC-SHA1-96 AES256-CTS-HMAC-SHA1-96

4.  <span data-ttu-id="a1174-301">Hallo-toewijzing tussen Hallo domeinaccount en Kerberos-principal in volgorde toouse Kerberos-principal in Windows-domein te maken.</span><span class="sxs-lookup"><span data-stu-id="a1174-301">Create hello mapping between hello domain account and Kerberos principal, in order toouse Kerberos principal in Windows Domain.</span></span>

    1. <span data-ttu-id="a1174-302">Hallo Systeembeheer Start > **Active Directory: gebruikers en Computers**.</span><span class="sxs-lookup"><span data-stu-id="a1174-302">Start hello Administrative tools > **Active Directory Users and Computers**.</span></span>

    2. <span data-ttu-id="a1174-303">Geavanceerde functies configureren door te klikken op **weergave** > **geavanceerde functies**.</span><span class="sxs-lookup"><span data-stu-id="a1174-303">Configure advanced features by clicking **View** > **Advanced Features**.</span></span>

    3. <span data-ttu-id="a1174-304">Zoek Hallo account toowhich gewenste toocreate toewijzingen, en met de rechtermuisknop op tooview **naamstoewijzingen** > klikt u op **Kerberos-namen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="a1174-304">Locate hello account toowhich you want toocreate mappings, and right-click tooview **Name Mappings** > click **Kerberos Names** tab.</span></span>

    4. <span data-ttu-id="a1174-305">Een principal van Hallo realm toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a1174-305">Add a principal from hello realm.</span></span>

        ![Beveiligings-id toewijzen](media/data-factory-hdfs-connector/map-security-identity.png)

<span data-ttu-id="a1174-307">**Op de gatewaycomputer:**</span><span class="sxs-lookup"><span data-stu-id="a1174-307">**On gateway machine:**</span></span>

* <span data-ttu-id="a1174-308">Voer de volgende Hallo **Ksetup** tooadd een vermelding realm-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="a1174-308">Run hello following **Ksetup** commands tooadd a realm entry.</span></span>

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

<span data-ttu-id="a1174-309">**In Azure Data Factory:**</span><span class="sxs-lookup"><span data-stu-id="a1174-309">**In Azure Data Factory:**</span></span>

* <span data-ttu-id="a1174-310">Configureren met behulp Hallo HDFS connector **Windows-verificatie** samen met uw domeinaccount of een Kerberos-Principal tooconnect toohello HDFS-gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="a1174-310">Configure hello HDFS connector using **Windows authentication** together with either your Domain Account or Kerberos Principal tooconnect toohello HDFS data source.</span></span> <span data-ttu-id="a1174-311">Controleer [eigenschappen van de gekoppelde Service HDFS](#linked-service-properties) sectie over configuratie-informatie.</span><span class="sxs-lookup"><span data-stu-id="a1174-311">Check [HDFS Linked Service properties](#linked-service-properties) section on configuration details.</span></span>

> [!NOTE]
> <span data-ttu-id="a1174-312">toomap kolommen uit de bron gegevensset toocolumns uit sink gegevensset, Zie [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="a1174-312">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="performance-and-tuning"></a><span data-ttu-id="a1174-313">Prestaties en het afstemmen</span><span class="sxs-lookup"><span data-stu-id="a1174-313">Performance and Tuning</span></span>
<span data-ttu-id="a1174-314">Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren toooptimize deze.</span><span class="sxs-lookup"><span data-stu-id="a1174-314">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
