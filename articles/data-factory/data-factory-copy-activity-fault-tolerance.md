---
title: fouttolerantie in Azure Data Factory-Kopieeractiviteit door niet-compatibele rijen overgeslagen aaaAdd | Microsoft Docs
description: "Meer informatie over hoe tooadd fouttolerantie in Azure Data Factory-Kopieeractiviteit door niet-compatibele rijen overgeslagen tijdens het kopiëren"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: e7cf6117655910844b292d340674d8d631450a81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-fault-tolerance-in-copy-activity-by-skipping-incompatible-rows"></a><span data-ttu-id="8edba-103">Fouttolerantie toevoegen in de kopieerbewerking door niet-compatibele rijen overgeslagen</span><span class="sxs-lookup"><span data-stu-id="8edba-103">Add fault tolerance in Copy Activity by skipping incompatible rows</span></span>

<span data-ttu-id="8edba-104">Azure Data Factory [Kopieeractiviteit](data-factory-data-movement-activities.md) biedt u twee manieren toohandle incompatibel rijen bij het kopiëren van gegevens tussen de bron- en sink gegevensarchieven:</span><span class="sxs-lookup"><span data-stu-id="8edba-104">Azure Data Factory [Copy Activity](data-factory-data-movement-activities.md) offers you two ways toohandle incompatible rows when copying data between source and sink data stores:</span></span>

- <span data-ttu-id="8edba-105">U kunt afbreken en mislukken Hallo kopie activiteit als niet-compatibele gegevens aangetroffen (standaardinstelling).</span><span class="sxs-lookup"><span data-stu-id="8edba-105">You can abort and fail hello copy activity when incompatible data is encountered (default behavior).</span></span>
- <span data-ttu-id="8edba-106">U kunt doorgaan met toocopy alle Hallo gegevens door toe te voegen fouttolerantie en niet-compatibele gegevensrijen wordt overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="8edba-106">You can continue toocopy all of hello data by adding fault tolerance and skipping incompatible data rows.</span></span> <span data-ttu-id="8edba-107">U kunt bovendien Hallo incompatibel rijen registreren in Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="8edba-107">In addition, you can log hello incompatible rows in Azure Blob storage.</span></span> <span data-ttu-id="8edba-108">U kunt vervolgens Hallo logboek toolearn Hallo oorzaak van het Hallo-probleem te onderzoeken, los van Hallo gegevens op het Hallo-gegevensbron en probeer Hallo kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="8edba-108">You can then examine hello log toolearn hello cause for hello failure, fix hello data on hello data source, and retry hello copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="8edba-109">Ondersteunde scenario 's</span><span class="sxs-lookup"><span data-stu-id="8edba-109">Supported scenarios</span></span>
<span data-ttu-id="8edba-110">Kopieeractiviteit ondersteunt drie scenario's voor het detecteren, wordt overgeslagen en logboekregistratie incompatibel gegevens:</span><span class="sxs-lookup"><span data-stu-id="8edba-110">Copy Activity supports three scenarios for detecting, skipping, and logging incompatible data:</span></span>

- <span data-ttu-id="8edba-111">**Incompatibiliteit tussen Hallo gegevensbrontype en systeemeigen Hallo sink-type**</span><span class="sxs-lookup"><span data-stu-id="8edba-111">**Incompatibility between hello source data type and hello sink native type**</span></span>

    <span data-ttu-id="8edba-112">Bijvoorbeeld: gegevens kopiëren van een CSV-bestand in Blob storage tooa SQL database met de schemadefinitie van een dat drie bevat **INT** kolommen van het type.</span><span class="sxs-lookup"><span data-stu-id="8edba-112">For example: Copy data from a CSV file in Blob storage tooa SQL database with a schema definition that contains three **INT** type columns.</span></span> <span data-ttu-id="8edba-113">CSV-bestand rijen die numerieke gegevens, zoals bevatten Hallo `123,456,789` zijn gekopieerd toohello sink store.</span><span class="sxs-lookup"><span data-stu-id="8edba-113">hello CSV file rows that contain numeric data, such as `123,456,789` are copied successfully toohello sink store.</span></span> <span data-ttu-id="8edba-114">Hallo echter rijen met niet-numerieke waarden zoals `123,456,abc` zijn gedetecteerd als incompatibele en worden overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="8edba-114">However, hello rows that contain non-numeric values, such as `123,456,abc` are detected as incompatible and are skipped.</span></span>

- <span data-ttu-id="8edba-115">**Het aantal kolommen tussen Hallo bron en sink Hallo Hallo komt niet overeen**</span><span class="sxs-lookup"><span data-stu-id="8edba-115">**Mismatch in hello number of columns between hello source and hello sink**</span></span>

    <span data-ttu-id="8edba-116">Bijvoorbeeld: gegevens kopiëren van een CSV-bestand in Blob storage tooa SQL database met de schemadefinitie van een dat zes kolommen bevat.</span><span class="sxs-lookup"><span data-stu-id="8edba-116">For example: Copy data from a CSV file in Blob storage tooa SQL database with a schema definition that contains six columns.</span></span> <span data-ttu-id="8edba-117">Hallo CSV-bestand rijen met zes kolommen zijn gekopieerd toohello sink store.</span><span class="sxs-lookup"><span data-stu-id="8edba-117">hello CSV file rows that contain six columns are copied successfully toohello sink store.</span></span> <span data-ttu-id="8edba-118">Hallo CSV-bestand rijen met minder dan zes of meer kolommen zijn gedetecteerd als niet compatibel en worden overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="8edba-118">hello CSV file rows that contain more or fewer than six columns are detected as incompatible and are skipped.</span></span>

- <span data-ttu-id="8edba-119">**Primaire sleutel is geschonden bij het schrijven van tooa relationele database**</span><span class="sxs-lookup"><span data-stu-id="8edba-119">**Primary key violation when writing tooa relational database**</span></span>

    <span data-ttu-id="8edba-120">Bijvoorbeeld: gegevens kopiëren van een SQL server tooa SQL-database.</span><span class="sxs-lookup"><span data-stu-id="8edba-120">For example: Copy data from a SQL server tooa SQL database.</span></span> <span data-ttu-id="8edba-121">Een primaire sleutel is gedefinieerd in Hallo sink SQL-database, maar die geen primaire sleutel is gedefinieerd in Hallo bron SQL server.</span><span class="sxs-lookup"><span data-stu-id="8edba-121">A primary key is defined in hello sink SQL database, but no such primary key is defined in hello source SQL server.</span></span> <span data-ttu-id="8edba-122">Hallo gedupliceerd rijen die in Hallo-bron voorkomen niet gekopieerde toohello sink.</span><span class="sxs-lookup"><span data-stu-id="8edba-122">hello duplicated rows that exist in hello source cannot be copied toohello sink.</span></span> <span data-ttu-id="8edba-123">Eerste rij alleen Hallo Hallo brongegevens kopieert Kopieeractiviteit naar Hallo sink.</span><span class="sxs-lookup"><span data-stu-id="8edba-123">Copy Activity copies only hello first row of hello source data into hello sink.</span></span> <span data-ttu-id="8edba-124">Hallo daaropvolgende bronrijen met primaire sleutelwaarde Hallo gedupliceerd zijn gedetecteerd als niet compatibel en worden overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="8edba-124">hello subsequent source rows that contain hello duplicated primary key value are detected as incompatible and are skipped.</span></span>

## <a name="configuration"></a><span data-ttu-id="8edba-125">Configuratie</span><span class="sxs-lookup"><span data-stu-id="8edba-125">Configuration</span></span>
<span data-ttu-id="8edba-126">Hallo bevat volgende voorbeeld een JSON-definitie tooconfigure Hallo incompatibel rijen in de kopieerbewerking wordt overgeslagen:</span><span class="sxs-lookup"><span data-stu-id="8edba-126">hello following example provides a JSON definition tooconfigure skipping hello incompatible rows in Copy Activity:</span></span>

```json
"typeProperties": {
    "source": {
        "type": "BlobSource"
    },
    "sink": {
        "type": "SqlSink",
    },         
    "enableSkipIncompatibleRow": true,           
    "redirectIncompatibleRowSettings": {
        "linkedServiceName": "BlobStorage",
        "path": "redirectcontainer/erroroutput"
    }
}
```

| <span data-ttu-id="8edba-127">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="8edba-127">Property</span></span> | <span data-ttu-id="8edba-128">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="8edba-128">Description</span></span> | <span data-ttu-id="8edba-129">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="8edba-129">Allowed values</span></span> | <span data-ttu-id="8edba-130">Vereist</span><span class="sxs-lookup"><span data-stu-id="8edba-130">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8edba-131">**enableSkipIncompatibleRow**</span><span class="sxs-lookup"><span data-stu-id="8edba-131">**enableSkipIncompatibleRow**</span></span> | <span data-ttu-id="8edba-132">Schakel overslaan incompatibel rijen tijdens het kopiëren van of niet.</span><span class="sxs-lookup"><span data-stu-id="8edba-132">Enable skipping incompatible rows during copy or not.</span></span> | <span data-ttu-id="8edba-133">True</span><span class="sxs-lookup"><span data-stu-id="8edba-133">True</span></span><br/><span data-ttu-id="8edba-134">False (standaard)</span><span class="sxs-lookup"><span data-stu-id="8edba-134">False (default)</span></span> | <span data-ttu-id="8edba-135">Nee</span><span class="sxs-lookup"><span data-stu-id="8edba-135">No</span></span> |
| <span data-ttu-id="8edba-136">**redirectIncompatibleRowSettings**</span><span class="sxs-lookup"><span data-stu-id="8edba-136">**redirectIncompatibleRowSettings**</span></span> | <span data-ttu-id="8edba-137">Een groep met eigenschappen die kunnen worden opgegeven als u wilt dat toolog Hallo incompatibel rijen.</span><span class="sxs-lookup"><span data-stu-id="8edba-137">A group of properties that can be specified when you want toolog hello incompatible rows.</span></span> | &nbsp; | <span data-ttu-id="8edba-138">Nee</span><span class="sxs-lookup"><span data-stu-id="8edba-138">No</span></span> |
| <span data-ttu-id="8edba-139">**linkedServiceName**</span><span class="sxs-lookup"><span data-stu-id="8edba-139">**linkedServiceName**</span></span> | <span data-ttu-id="8edba-140">Hallo gekoppelde service van Azure Storage toostore Hallo logboek dat Hallo overgeslagen rijen bevat.</span><span class="sxs-lookup"><span data-stu-id="8edba-140">hello linked service of Azure Storage toostore hello log that contains hello skipped rows.</span></span> | <span data-ttu-id="8edba-141">Hallo-naam van een [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) of [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) gekoppelde service die toohello opslag exemplaar toouse toostore Hallo log-bestand dat u wilt verwijst.</span><span class="sxs-lookup"><span data-stu-id="8edba-141">hello name of an [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) linked service, which refers toohello storage instance that you want toouse toostore hello log file.</span></span> | <span data-ttu-id="8edba-142">Nee</span><span class="sxs-lookup"><span data-stu-id="8edba-142">No</span></span> |
| <span data-ttu-id="8edba-143">**pad**</span><span class="sxs-lookup"><span data-stu-id="8edba-143">**path**</span></span> | <span data-ttu-id="8edba-144">Hallo-pad van Hallo-logboekbestand met Hallo overgeslagen rijen.</span><span class="sxs-lookup"><span data-stu-id="8edba-144">hello path of hello log file that contains hello skipped rows.</span></span> | <span data-ttu-id="8edba-145">Hallo Blob storage pad dat u toouse toolog Hallo incompatibele gegevens wilt opgeven.</span><span class="sxs-lookup"><span data-stu-id="8edba-145">Specify hello Blob storage path that you want toouse toolog hello incompatible data.</span></span> <span data-ttu-id="8edba-146">Als u niet een pad opgeeft, wordt in Hallo-service een container voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8edba-146">If you do not provide a path, hello service creates a container for you.</span></span> | <span data-ttu-id="8edba-147">Nee</span><span class="sxs-lookup"><span data-stu-id="8edba-147">No</span></span> |

## <a name="monitoring"></a><span data-ttu-id="8edba-148">Bewaking</span><span class="sxs-lookup"><span data-stu-id="8edba-148">Monitoring</span></span>
<span data-ttu-id="8edba-149">Nadat de kopieeractiviteit Hallo uitgevoerd is voltooid, ziet u Hallo aantal overgeslagen rijen in de sectie bewaking Hallo:</span><span class="sxs-lookup"><span data-stu-id="8edba-149">After hello copy activity run completes, you can see hello number of skipped rows in hello monitoring section:</span></span>

![Monitor incompatibel rijen overgeslagen](./media/data-factory-copy-activity-fault-tolerance/skip-incompatible-rows-monitoring.png)

<span data-ttu-id="8edba-151">Als u toolog Hallo incompatibel rijen configureert, kunt u Hallo logboekbestand aan dit pad vinden: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` In Hallo logboekbestand, kunt u Hallo rijen weergeven die zijn overgeslagen en Hallo hoofdoorzaak Hallo niet compatibel.</span><span class="sxs-lookup"><span data-stu-id="8edba-151">If you configure toolog hello incompatible rows, you can find hello log file at this path: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` In hello log file, you can see hello rows that were skipped and hello root cause of hello incompatibility.</span></span>

<span data-ttu-id="8edba-152">Zowel Hallo oorspronkelijke gegevens en de bijbehorende fout Hallo worden vastgelegd in het Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="8edba-152">Both hello original data and hello corresponding error are logged in hello file.</span></span> <span data-ttu-id="8edba-153">Een voorbeeld van inhoud Hallo log-bestand is als volgt:</span><span class="sxs-lookup"><span data-stu-id="8edba-153">An example of hello log file content is as follows:</span></span>
```
data1, data2, data3, UserErrorInvalidDataValue,Column 'Prop_2' contains an invalid value 'data3'. Cannot convert 'data3' tootype 'DateTime'.,
data4, data5, data6, Violation of PRIMARY KEY constraint 'PK_tblintstrdatetimewithpk'. Cannot insert duplicate key in object 'dbo.tblintstrdatetimewithpk'. hello duplicate key value is (data4).
```

## <a name="next-steps"></a><span data-ttu-id="8edba-154">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8edba-154">Next steps</span></span>
<span data-ttu-id="8edba-155">Zie toolearn meer informatie over Azure Data Factory Kopieeractiviteit [verplaatsen van gegevens met behulp van de Kopieeractiviteit](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="8edba-155">toolearn more about Azure Data Factory Copy Activity, see [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span></span>
