---
title: Fouttolerantie in Azure Data Factory-Kopieeractiviteit toevoegen incompatibel rijen overgeslagen | Microsoft Docs
description: "Informatie over het toevoegen van fouttolerantie in Azure Data Factory-Kopieeractiviteit door niet-compatibele rijen overgeslagen tijdens het kopiëren"
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
ms.openlocfilehash: e2a108752259d5da3b401666c6bdbaad13b7ea90
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="add-fault-tolerance-in-copy-activity-by-skipping-incompatible-rows"></a><span data-ttu-id="399cf-103">Fouttolerantie toevoegen in de kopieerbewerking door niet-compatibele rijen overgeslagen</span><span class="sxs-lookup"><span data-stu-id="399cf-103">Add fault tolerance in Copy Activity by skipping incompatible rows</span></span>

<span data-ttu-id="399cf-104">Azure Data Factory [Kopieeractiviteit](data-factory-data-movement-activities.md) biedt twee manieren om af te handelen incompatibel rijen bij het kopiëren van gegevens tussen de bron- en sink gegevensarchieven:</span><span class="sxs-lookup"><span data-stu-id="399cf-104">Azure Data Factory [Copy Activity](data-factory-data-movement-activities.md) offers you two ways to handle incompatible rows when copying data between source and sink data stores:</span></span>

- <span data-ttu-id="399cf-105">U kunt afbreken en mislukt de kopie activiteit als niet-compatibele gegevens aangetroffen (standaardinstelling).</span><span class="sxs-lookup"><span data-stu-id="399cf-105">You can abort and fail the copy activity when incompatible data is encountered (default behavior).</span></span>
- <span data-ttu-id="399cf-106">U kunt doorgaan met het kopiëren alle gegevens door toe te voegen fouttolerantie en niet-compatibele gegevensrijen wordt overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="399cf-106">You can continue to copy all of the data by adding fault tolerance and skipping incompatible data rows.</span></span> <span data-ttu-id="399cf-107">Bovendien kunt u de niet-compatibele rijen registreren in Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="399cf-107">In addition, you can log the incompatible rows in Azure Blob storage.</span></span> <span data-ttu-id="399cf-108">Bekijk vervolgens het logboek voor meer informatie over de oorzaak van de fout, los van de gegevens op de gegevensbron en probeer het opnieuw met de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="399cf-108">You can then examine the log to learn the cause for the failure, fix the data on the data source, and retry the copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="399cf-109">Ondersteunde scenario 's</span><span class="sxs-lookup"><span data-stu-id="399cf-109">Supported scenarios</span></span>
<span data-ttu-id="399cf-110">Kopieeractiviteit ondersteunt drie scenario's voor het detecteren, wordt overgeslagen en logboekregistratie incompatibel gegevens:</span><span class="sxs-lookup"><span data-stu-id="399cf-110">Copy Activity supports three scenarios for detecting, skipping, and logging incompatible data:</span></span>

- <span data-ttu-id="399cf-111">**Incompatibiliteit tussen het gegevensbrontype en het systeemeigen sink-type**</span><span class="sxs-lookup"><span data-stu-id="399cf-111">**Incompatibility between the source data type and the sink native type**</span></span>

    <span data-ttu-id="399cf-112">Bijvoorbeeld: gegevens kopiëren van een CSV-bestand in Blob storage naar een SQL-database met de schemadefinitie van een dat drie bevat **INT** kolommen van het type.</span><span class="sxs-lookup"><span data-stu-id="399cf-112">For example: Copy data from a CSV file in Blob storage to a SQL database with a schema definition that contains three **INT** type columns.</span></span> <span data-ttu-id="399cf-113">De CSV-bestand rijen die numerieke gegevens, zoals bevatten `123,456,789` is gekopieerd naar de store sink.</span><span class="sxs-lookup"><span data-stu-id="399cf-113">The CSV file rows that contain numeric data, such as `123,456,789` are copied successfully to the sink store.</span></span> <span data-ttu-id="399cf-114">Echter, de rijen die niet-numerieke waarden bevatten, zoals `123,456,abc` zijn gedetecteerd als incompatibele en worden overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="399cf-114">However, the rows that contain non-numeric values, such as `123,456,abc` are detected as incompatible and are skipped.</span></span>

- <span data-ttu-id="399cf-115">**Het aantal kolommen tussen de bron en de sink komt niet overeen**</span><span class="sxs-lookup"><span data-stu-id="399cf-115">**Mismatch in the number of columns between the source and the sink**</span></span>

    <span data-ttu-id="399cf-116">Bijvoorbeeld: gegevens kopiëren van een CSV-bestand in Blob storage naar een SQL-database met de schemadefinitie van een dat zes kolommen bevat.</span><span class="sxs-lookup"><span data-stu-id="399cf-116">For example: Copy data from a CSV file in Blob storage to a SQL database with a schema definition that contains six columns.</span></span> <span data-ttu-id="399cf-117">De CSV-bestand-rijen met zes kolommen worden gekopieerd naar de store sink.</span><span class="sxs-lookup"><span data-stu-id="399cf-117">The CSV file rows that contain six columns are copied successfully to the sink store.</span></span> <span data-ttu-id="399cf-118">De CSV-bestand rijen die minder dan zes of meer kolommen bevatten als niet compatibel zijn gedetecteerd en worden overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="399cf-118">The CSV file rows that contain more or fewer than six columns are detected as incompatible and are skipped.</span></span>

- <span data-ttu-id="399cf-119">**Primaire sleutel is geschonden bij het schrijven naar een relationele database**</span><span class="sxs-lookup"><span data-stu-id="399cf-119">**Primary key violation when writing to a relational database**</span></span>

    <span data-ttu-id="399cf-120">Bijvoorbeeld: gegevens kopiëren van een SQL-server naar een SQL-database.</span><span class="sxs-lookup"><span data-stu-id="399cf-120">For example: Copy data from a SQL server to a SQL database.</span></span> <span data-ttu-id="399cf-121">Een primaire sleutel is gedefinieerd in de sink SQL-database, maar die geen primaire sleutel is gedefinieerd in de bron-SQL-server.</span><span class="sxs-lookup"><span data-stu-id="399cf-121">A primary key is defined in the sink SQL database, but no such primary key is defined in the source SQL server.</span></span> <span data-ttu-id="399cf-122">De dubbele rijen die in de bron voorkomen kunnen niet worden gekopieerd naar de sink.</span><span class="sxs-lookup"><span data-stu-id="399cf-122">The duplicated rows that exist in the source cannot be copied to the sink.</span></span> <span data-ttu-id="399cf-123">Alleen de eerste rij van de brongegevens Kopieeractiviteit gekopieerd naar de sink.</span><span class="sxs-lookup"><span data-stu-id="399cf-123">Copy Activity copies only the first row of the source data into the sink.</span></span> <span data-ttu-id="399cf-124">De volgende bronrijen met dubbele primaire sleutelwaarde zijn gedetecteerd als niet compatibel en worden overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="399cf-124">The subsequent source rows that contain the duplicated primary key value are detected as incompatible and are skipped.</span></span>

## <a name="configuration"></a><span data-ttu-id="399cf-125">Configuratie</span><span class="sxs-lookup"><span data-stu-id="399cf-125">Configuration</span></span>
<span data-ttu-id="399cf-126">Het volgende voorbeeld bevat een JSON-definitie voor het configureren van de niet-compatibele rijen in de kopieerbewerking wordt overgeslagen:</span><span class="sxs-lookup"><span data-stu-id="399cf-126">The following example provides a JSON definition to configure skipping the incompatible rows in Copy Activity:</span></span>

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

| <span data-ttu-id="399cf-127">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="399cf-127">Property</span></span> | <span data-ttu-id="399cf-128">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="399cf-128">Description</span></span> | <span data-ttu-id="399cf-129">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="399cf-129">Allowed values</span></span> | <span data-ttu-id="399cf-130">Vereist</span><span class="sxs-lookup"><span data-stu-id="399cf-130">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="399cf-131">**enableSkipIncompatibleRow**</span><span class="sxs-lookup"><span data-stu-id="399cf-131">**enableSkipIncompatibleRow**</span></span> | <span data-ttu-id="399cf-132">Schakel overslaan incompatibel rijen tijdens het kopiëren van of niet.</span><span class="sxs-lookup"><span data-stu-id="399cf-132">Enable skipping incompatible rows during copy or not.</span></span> | <span data-ttu-id="399cf-133">True</span><span class="sxs-lookup"><span data-stu-id="399cf-133">True</span></span><br/><span data-ttu-id="399cf-134">False (standaard)</span><span class="sxs-lookup"><span data-stu-id="399cf-134">False (default)</span></span> | <span data-ttu-id="399cf-135">Nee</span><span class="sxs-lookup"><span data-stu-id="399cf-135">No</span></span> |
| <span data-ttu-id="399cf-136">**redirectIncompatibleRowSettings**</span><span class="sxs-lookup"><span data-stu-id="399cf-136">**redirectIncompatibleRowSettings**</span></span> | <span data-ttu-id="399cf-137">Een groep met eigenschappen die kunnen worden opgegeven wanneer u wilt vastleggen van de niet-compatibele rijen.</span><span class="sxs-lookup"><span data-stu-id="399cf-137">A group of properties that can be specified when you want to log the incompatible rows.</span></span> | &nbsp; | <span data-ttu-id="399cf-138">Nee</span><span class="sxs-lookup"><span data-stu-id="399cf-138">No</span></span> |
| <span data-ttu-id="399cf-139">**linkedServiceName**</span><span class="sxs-lookup"><span data-stu-id="399cf-139">**linkedServiceName**</span></span> | <span data-ttu-id="399cf-140">De gekoppelde service van Azure Storage voor het opslaan van het logboek dat overgeslagen rijen bevat.</span><span class="sxs-lookup"><span data-stu-id="399cf-140">The linked service of Azure Storage to store the log that contains the skipped rows.</span></span> | <span data-ttu-id="399cf-141">De naam van een [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) of [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) gekoppelde service die naar de opslag-instantie die u gebruiken verwijst wilt voor het opslaan van het logboekbestand.</span><span class="sxs-lookup"><span data-stu-id="399cf-141">The name of an [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) linked service, which refers to the storage instance that you want to use to store the log file.</span></span> | <span data-ttu-id="399cf-142">Nee</span><span class="sxs-lookup"><span data-stu-id="399cf-142">No</span></span> |
| <span data-ttu-id="399cf-143">**pad**</span><span class="sxs-lookup"><span data-stu-id="399cf-143">**path**</span></span> | <span data-ttu-id="399cf-144">Het pad van het logboekbestand dat overgeslagen rijen bevat.</span><span class="sxs-lookup"><span data-stu-id="399cf-144">The path of the log file that contains the skipped rows.</span></span> | <span data-ttu-id="399cf-145">Geef het pad voor Blob-opslag die u wilt gebruiken om de niet-compatibele gegevens te registreren.</span><span class="sxs-lookup"><span data-stu-id="399cf-145">Specify the Blob storage path that you want to use to log the incompatible data.</span></span> <span data-ttu-id="399cf-146">Als u niet een pad opgeeft, wordt in de service een container voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="399cf-146">If you do not provide a path, the service creates a container for you.</span></span> | <span data-ttu-id="399cf-147">Nee</span><span class="sxs-lookup"><span data-stu-id="399cf-147">No</span></span> |

## <a name="monitoring"></a><span data-ttu-id="399cf-148">Bewaking</span><span class="sxs-lookup"><span data-stu-id="399cf-148">Monitoring</span></span>
<span data-ttu-id="399cf-149">Nadat de kopieeractiviteit uitgevoerd is voltooid, ziet u het aantal overgeslagen rijen in de sectie bewaking:</span><span class="sxs-lookup"><span data-stu-id="399cf-149">After the copy activity run completes, you can see the number of skipped rows in the monitoring section:</span></span>

![Monitor incompatibel rijen overgeslagen](./media/data-factory-copy-activity-fault-tolerance/skip-incompatible-rows-monitoring.png)

<span data-ttu-id="399cf-151">Als u voor de niet-compatibele rijen logboekregistratie hebt geconfigureerd, kunt u het logboekbestand op dit pad vinden: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` In het logboekbestand kunt u de rijen die zijn overgeslagen en de hoofdoorzaak van deze incompatibiliteit bekijken.</span><span class="sxs-lookup"><span data-stu-id="399cf-151">If you configure to log the incompatible rows, you can find the log file at this path: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` In the log file, you can see the rows that were skipped and the root cause of the incompatibility.</span></span>

<span data-ttu-id="399cf-152">Zowel de oorspronkelijke gegevens en de bijbehorende fout worden geregistreerd in het bestand.</span><span class="sxs-lookup"><span data-stu-id="399cf-152">Both the original data and the corresponding error are logged in the file.</span></span> <span data-ttu-id="399cf-153">Een voorbeeld van de inhoud van het logboek-bestand is als volgt:</span><span class="sxs-lookup"><span data-stu-id="399cf-153">An example of the log file content is as follows:</span></span>
```
data1, data2, data3, UserErrorInvalidDataValue,Column 'Prop_2' contains an invalid value 'data3'. Cannot convert 'data3' to type 'DateTime'.,
data4, data5, data6, Violation of PRIMARY KEY constraint 'PK_tblintstrdatetimewithpk'. Cannot insert duplicate key in object 'dbo.tblintstrdatetimewithpk'. The duplicate key value is (data4).
```

## <a name="next-steps"></a><span data-ttu-id="399cf-154">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="399cf-154">Next steps</span></span>
<span data-ttu-id="399cf-155">Zie voor meer informatie over Azure Data Factory-Kopieeractiviteit, [verplaatsen van gegevens met behulp van de Kopieeractiviteit](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="399cf-155">To learn more about Azure Data Factory Copy Activity, see [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span></span>