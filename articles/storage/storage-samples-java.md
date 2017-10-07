---
title: aaaAzure opslag voorbeelden weergegeven met behulp van Java | Microsoft Docs
description: Weergeven, downloaden en uitvoeren van toepassingen voor Azure Storage en voorbeeldcode. Ontdek voorbeelden voor blobs, wachtrijen, tabellen en bestanden, met behulp van Hallo Java opslagclientbibliotheken aan de slag.
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 01/12/2017
ms.author: seguler
ms.openlocfilehash: e3b8fbe86e82dd58c2a13a3c68760cbf6e9a6e4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-samples-using-java"></a><span data-ttu-id="a66eb-104">Azure Storage-voorbeelden u Java gebruikt</span><span class="sxs-lookup"><span data-stu-id="a66eb-104">Azure Storage samples using Java</span></span>

## <a name="java-sample-index"></a><span data-ttu-id="a66eb-105">Index van Java-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="a66eb-105">Java sample index</span></span>

<span data-ttu-id="a66eb-106">Hallo volgende tabel geeft een overzicht van onze voorbeelden opslagplaats en Hallo scenario's die in elk voorbeeld worden behandeld.</span><span class="sxs-lookup"><span data-stu-id="a66eb-106">hello following table provides an overview of our samples repository and hello scenarios covered in each sample.</span></span> <span data-ttu-id="a66eb-107">Klik op Hallo koppelingen tooview Hallo bijbehorende voorbeeldcode in GitHub.</span><span class="sxs-lookup"><span data-stu-id="a66eb-107">Click on hello links tooview hello corresponding sample code in GitHub.</span></span>

<table style="font-size:90%"><thead><tr><th style="font-size:110%"><span data-ttu-id="a66eb-108">Eindpunt</span><span class="sxs-lookup"><span data-stu-id="a66eb-108">Endpoint</span></span></th><th style="font-size:110%"><span data-ttu-id="a66eb-109">Scenario</span><span class="sxs-lookup"><span data-stu-id="a66eb-109">Scenario</span></span></th><th style="font-size:110%"><span data-ttu-id="a66eb-110">Voorbeeldcode</span><span class="sxs-lookup"><span data-stu-id="a66eb-110">Sample Code</span></span></th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><span data-ttu-id="a66eb-111"><b>BLOB</b></span><span class="sxs-lookup"><span data-stu-id="a66eb-111"><b>Blob</b></span></span></td>
<td><span data-ttu-id="a66eb-112">Toevoeg-Blob</span><span class="sxs-lookup"><span data-stu-id="a66eb-112">Append Blob</span></span></td> 
<td><span data-ttu-id="a66eb-113"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Aan de slag met Azure Blob-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="a66eb-113"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="a66eb-114">Blok-Blob</span><span class="sxs-lookup"><span data-stu-id="a66eb-114">Block Blob</span></span></td>
<td><span data-ttu-id="a66eb-115"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Aan de slag met Azure Blob-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="a66eb-115"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="a66eb-116">Clientversleuteling</span><span class="sxs-lookup"><span data-stu-id="a66eb-116">Client-Side Encryption</span></span></td>
<td><span data-ttu-id="a66eb-117"><a href="https://github.com/Azure-Samples/storage-java-client-side-encryption">Aan de slag met Azure versleuteling voor aan de clientzijde in Java</a></span><span class="sxs-lookup"><span data-stu-id="a66eb-117"><a href="https://github.com/Azure-Samples/storage-java-client-side-encryption">Getting Started with Azure Client Side Encryption in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="a66eb-118">Blob kopiëren</span><span class="sxs-lookup"><span data-stu-id="a66eb-118">Copy Blob</span></span></td>
<td><span data-ttu-id="a66eb-119"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Aan de slag met Azure Blob-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="a66eb-119"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="a66eb-120">Container maken</span><span class="sxs-lookup"><span data-stu-id="a66eb-120">Create Container</span></span></td>
<td><span data-ttu-id="a66eb-121"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Aan de slag met Azure Blob-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="a66eb-121"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="a66eb-122">Verwijderen van Blob</span><span class="sxs-lookup"><span data-stu-id="a66eb-122">Delete Blob</span></span></td>
<td><span data-ttu-id="a66eb-123"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Aan de slag met Azure Blob-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="a66eb-123"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="a66eb-124">Verwijderen van Container</span><span class="sxs-lookup"><span data-stu-id="a66eb-124">Delete Container</span></span></td>
<td><span data-ttu-id="a66eb-125"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Aan de slag met Azure Blob-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="a66eb-125"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="a66eb-126">BLOB eigenschappen-metagegevens/Stats</span><span class="sxs-lookup"><span data-stu-id="a66eb-126">Blob Metadata/Properties/Stats</span></span></td>
<td><span data-ttu-id="a66eb-127"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Aan de slag met Azure Blob-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="a66eb-127"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="a66eb-128">ACL, metagegevens/eigenschappen van container</span><span class="sxs-lookup"><span data-stu-id="a66eb-128">Container ACL/Metadata/Properties</span></span></td>
<td><span data-ttu-id="a66eb-129"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Aan de slag met Azure Blob-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="a66eb-129"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="a66eb-130">Get-paginabereiken</span><span class="sxs-lookup"><span data-stu-id="a66eb-130">Get Page Ranges</span></span></td>
<td><span data-ttu-id="a66eb-131"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/CloudPageBlobTests.java">Pagina-Blob test voorbeeld</a></span><span class="sxs-lookup"><span data-stu-id="a66eb-131"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/CloudPageBlobTests.java">Page Blob Tests Sample</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="a66eb-132">De lease van Blob-Container</span><span class="sxs-lookup"><span data-stu-id="a66eb-132">Lease Blob/Container</span></span></td>
<td><span data-ttu-id="a66eb-133"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Aan de slag met Azure Blob-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="a66eb-133"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="a66eb-134">Lijst Blobcontainer</span><span class="sxs-lookup"><span data-stu-id="a66eb-134">List Blob/Container</span></span></td>
<td><span data-ttu-id="a66eb-135"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Aan de slag met Azure Blob-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="a66eb-135"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="a66eb-136">Pagina-Blob</span><span class="sxs-lookup"><span data-stu-id="a66eb-136">Page Blob</span></span></td>
<td><span data-ttu-id="a66eb-137"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Aan de slag met Azure Blob-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="a66eb-137"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr>
<tr> 
<td><span data-ttu-id="a66eb-138">SAS</span><span class="sxs-lookup"><span data-stu-id="a66eb-138">SAS</span></span></td>
<td><span data-ttu-id="a66eb-139"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/SasTests.java">Voorbeeld van SAS-Tests</a></span><span class="sxs-lookup"><span data-stu-id="a66eb-139"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/SasTests.java">SAS Tests Sample</a></span></span></td>
</tr>   
<tr> 
<td><span data-ttu-id="a66eb-140">Service-eigenschappen</span><span class="sxs-lookup"><span data-stu-id="a66eb-140">Service Properties</span></span></td>
<td><span data-ttu-id="a66eb-141"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Aan de slag met Azure Blob-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="a66eb-141"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr>           
<tr> 
<td><span data-ttu-id="a66eb-142">Momentopname Blob</span><span class="sxs-lookup"><span data-stu-id="a66eb-142">Snapshot Blob</span></span></td>
<td><span data-ttu-id="a66eb-143"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Aan de slag met Azure Blob-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="a66eb-143"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td rowspan="9"><span data-ttu-id="a66eb-144"><b>File</b></span><span class="sxs-lookup"><span data-stu-id="a66eb-144"><b>File</b></span></span></td>
<td><span data-ttu-id="a66eb-145">Mappen-Shares-bestanden maken</span><span class="sxs-lookup"><span data-stu-id="a66eb-145">Create Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="a66eb-146"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Aan de slag met Azure File-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="a66eb-146"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="a66eb-147">Mappen-Shares-bestanden verwijderen</span><span class="sxs-lookup"><span data-stu-id="a66eb-147">Delete Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="a66eb-148"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Aan de slag met Azure File-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="a66eb-148"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="a66eb-149">Directory eigenschappen/Metadata</span><span class="sxs-lookup"><span data-stu-id="a66eb-149">Directory Properties/Metadata</span></span></td> 
<td><span data-ttu-id="a66eb-150"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Aan de slag met Azure File-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="a66eb-150"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="a66eb-151">Bestanden downloaden</span><span class="sxs-lookup"><span data-stu-id="a66eb-151">Download Files</span></span></td> 
<td><span data-ttu-id="a66eb-152"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Aan de slag met Azure File-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="a66eb-152"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="a66eb-153">Bestand eigenschappen/metagegevens/metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="a66eb-153">File Properties/Metadata/Metrics</span></span></td> 
<td><span data-ttu-id="a66eb-154"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Aan de slag met Azure File-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="a66eb-154"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="a66eb-155">File Service Properties</span><span class="sxs-lookup"><span data-stu-id="a66eb-155">File Service Properties</span></span></td> 
<td><span data-ttu-id="a66eb-156"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Aan de slag met Azure File-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="a66eb-156"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="a66eb-157">Lijst met mappen en bestanden</span><span class="sxs-lookup"><span data-stu-id="a66eb-157">List Directories and Files</span></span></td> 
<td><span data-ttu-id="a66eb-158"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Aan de slag met Azure File-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="a66eb-158"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="a66eb-159">Lijst met Shares</span><span class="sxs-lookup"><span data-stu-id="a66eb-159">List Shares</span></span></td> 
<td><span data-ttu-id="a66eb-160"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Aan de slag met Azure File-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="a66eb-160"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="a66eb-161">Delen van metagegevens-eigenschappen-statistieken</span><span class="sxs-lookup"><span data-stu-id="a66eb-161">Share Properties/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="a66eb-162"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Aan de slag met Azure File-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="a66eb-162"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td rowspan="8"><span data-ttu-id="a66eb-163"><b>Wachtrij</b></span><span class="sxs-lookup"><span data-stu-id="a66eb-163"><b>Queue</b></span></span></td>
<td><span data-ttu-id="a66eb-164">Bericht toevoegen</span><span class="sxs-lookup"><span data-stu-id="a66eb-164">Add Message</span></span></td> 
<td><span data-ttu-id="a66eb-165"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/queue/gettingstarted/QueueBasics.java">Opslag Java Client Library-voorbeelden</a></span><span class="sxs-lookup"><span data-stu-id="a66eb-165"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/queue/gettingstarted/QueueBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="a66eb-166">Clientversleuteling</span><span class="sxs-lookup"><span data-stu-id="a66eb-166">Client-Side Encryption</span></span></td> 
<td><span data-ttu-id="a66eb-167"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/encryption/queue/gettingstarted/QueueGettingStarted.java">Opslag Java Client Library-voorbeelden</a></span><span class="sxs-lookup"><span data-stu-id="a66eb-167"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/encryption/queue/gettingstarted/QueueGettingStarted.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="a66eb-168">Wachtrijen maken</span><span class="sxs-lookup"><span data-stu-id="a66eb-168">Create Queues</span></span></td> 
<td><span data-ttu-id="a66eb-169"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Aan de slag met Azure Queue-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="a66eb-169"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="a66eb-170">Berichtenwachtrij/verwijderen</span><span class="sxs-lookup"><span data-stu-id="a66eb-170">Delete Message/Queue</span></span></td> 
<td><span data-ttu-id="a66eb-171"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Aan de slag met Azure Queue-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="a66eb-171"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="a66eb-172">Bericht</span><span class="sxs-lookup"><span data-stu-id="a66eb-172">Peek Message</span></span></td> 
<td><span data-ttu-id="a66eb-173"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Aan de slag met Azure Queue-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="a66eb-173"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="a66eb-174">Wachtrij metagegevens-ACL/Stats</span><span class="sxs-lookup"><span data-stu-id="a66eb-174">Queue ACL/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="a66eb-175"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Aan de slag met Azure Queue-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="a66eb-175"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="a66eb-176">Eigenschappen van de Queue-Service</span><span class="sxs-lookup"><span data-stu-id="a66eb-176">Queue Service Properties</span></span></td> 
<td><span data-ttu-id="a66eb-177"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Aan de slag met Azure Queue-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="a66eb-177"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="a66eb-178">Updatebericht</span><span class="sxs-lookup"><span data-stu-id="a66eb-178">Update Message</span></span></td> 
<td><span data-ttu-id="a66eb-179"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Aan de slag met Azure Queue-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="a66eb-179"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td rowspan="7"><span data-ttu-id="a66eb-180"><b>Tabel</b></span><span class="sxs-lookup"><span data-stu-id="a66eb-180"><b>Table</b></span></span></td>
<td><span data-ttu-id="a66eb-181">Tabel maken</span><span class="sxs-lookup"><span data-stu-id="a66eb-181">Create Table</span></span></td> 
<td><span data-ttu-id="a66eb-182"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Aan de slag met Azure Table-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="a66eb-182"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="a66eb-183">Entiteit/tabel verwijderen</span><span class="sxs-lookup"><span data-stu-id="a66eb-183">Delete Entity/Table</span></span></td> 
<td><span data-ttu-id="a66eb-184"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Aan de slag met Azure Table-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="a66eb-184"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="a66eb-185">De entiteit invoegen of Merge/verplaatsen</span><span class="sxs-lookup"><span data-stu-id="a66eb-185">Insert/Merge/Replace Entity</span></span></td> 
<td><span data-ttu-id="a66eb-186"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Opslag Java Client Library-voorbeelden</a></span><span class="sxs-lookup"><span data-stu-id="a66eb-186"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="a66eb-187">Query-entiteiten</span><span class="sxs-lookup"><span data-stu-id="a66eb-187">Query Entities</span></span></td> 
<td><span data-ttu-id="a66eb-188"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Aan de slag met Azure Table-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="a66eb-188"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="a66eb-189">Querytabellen</span><span class="sxs-lookup"><span data-stu-id="a66eb-189">Query Tables</span></span></td> 
<td><span data-ttu-id="a66eb-190"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Aan de slag met Azure Table-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="a66eb-190"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="a66eb-191">ACL/eigenschappen van de tabel</span><span class="sxs-lookup"><span data-stu-id="a66eb-191">Table ACL/Properties</span></span></td> 
<td><span data-ttu-id="a66eb-192"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableAdvanced.java">Aan de slag met Azure Table-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="a66eb-192"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableAdvanced.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="a66eb-193">Bijwerken van entiteit</span><span class="sxs-lookup"><span data-stu-id="a66eb-193">Update Entity</span></span></td> 
<td><span data-ttu-id="a66eb-194"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Opslag Java Client Library-voorbeelden</a></span><span class="sxs-lookup"><span data-stu-id="a66eb-194"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a><span data-ttu-id="a66eb-195">Azure-codevoorbeelden-bibliotheek</span><span class="sxs-lookup"><span data-stu-id="a66eb-195">Azure Code Samples library</span></span>

<span data-ttu-id="a66eb-196">tooview hello compleet codevoorbeeld bibliotheek, Ga toohello [Azure codevoorbeelden](https://azure.microsoft.com/resources/samples/?service=storage) bibliotheek, waaronder voorbeelden voor Azure-opslag die u kunt downloaden en lokaal uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="a66eb-196">tooview hello complete sample library, go toohello [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=storage) library, which includes samples for Azure Storage that you can download and run locally.</span></span> <span data-ttu-id="a66eb-197">Hallo Code voorbeeld van een bibliotheek bevat voorbeeldcode in het ZIP-indeling.</span><span class="sxs-lookup"><span data-stu-id="a66eb-197">hello Code Sample Library provides sample code in .zip format.</span></span> <span data-ttu-id="a66eb-198">U kunt ook bladeren en Hallo GitHub-opslagplaats voor elk voorbeeld klonen.</span><span class="sxs-lookup"><span data-stu-id="a66eb-198">Alternatively, you can browse and clone hello GitHub repository for each sample.</span></span>

[!INCLUDE [storage-java-samples-include](../../includes/storage-java-samples-include.md)]

## <a name="getting-started-guides"></a><span data-ttu-id="a66eb-199">Ophalen van slag-handleidingen</span><span class="sxs-lookup"><span data-stu-id="a66eb-199">Getting started guides</span></span>

<span data-ttu-id="a66eb-200">Hallo handleidingen volgen als u op zoek bent voor instructies over het uitchecken tooinstall en aan de slag met Hallo clientbibliotheken van Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="a66eb-200">Check out hello following guides if you are looking for instructions on how tooinstall and get started with hello Azure Storage Client Libraries.</span></span>

* [<span data-ttu-id="a66eb-201">Aan de slag met Azure Blob-Service in Java</span><span class="sxs-lookup"><span data-stu-id="a66eb-201">Getting Started with Azure Blob Service in Java</span></span>](storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="a66eb-202">Aan de slag met Azure Queue-Service in Java</span><span class="sxs-lookup"><span data-stu-id="a66eb-202">Getting Started with Azure Queue Service in Java</span></span>](storage-java-how-to-use-queue-storage.md)
* [<span data-ttu-id="a66eb-203">Aan de slag met Azure Table-Service in Java</span><span class="sxs-lookup"><span data-stu-id="a66eb-203">Getting Started with Azure Table Service in Java</span></span>](storage-java-how-to-use-table-storage.md)
* [<span data-ttu-id="a66eb-204">Aan de slag met Azure File-Service in Java</span><span class="sxs-lookup"><span data-stu-id="a66eb-204">Getting Started with Azure File Service in Java</span></span>](storage-java-how-to-use-file-storage.md)

## <a name="next-steps"></a><span data-ttu-id="a66eb-205">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a66eb-205">Next steps</span></span>

<span data-ttu-id="a66eb-206">Voor informatie over steekproeven voor de andere talen:</span><span class="sxs-lookup"><span data-stu-id="a66eb-206">For information on samples for other languages:</span></span>

* <span data-ttu-id="a66eb-207">.NET: [voorbeelden van azure Storage met .NET](storage-samples-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="a66eb-207">.NET: [Azure Storage samples using .NET](storage-samples-dotnet.md)</span></span>
* <span data-ttu-id="a66eb-208">Alle andere talen: [Azure Storage-voorbeelden](storage-samples.md)</span><span class="sxs-lookup"><span data-stu-id="a66eb-208">All other languages: [Azure Storage samples](storage-samples.md)</span></span>
