---
title: Azure Storage-voorbeelden met Java | Microsoft Docs
description: Weergeven, downloaden en uitvoeren van toepassingen voor Azure Storage en voorbeeldcode. Ontdek aan de slag voorbeelden voor blobs, wachtrijen, tabellen en bestanden, met behulp van de clientbibliotheken van Java-opslag.
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
ms.openlocfilehash: 98e6022062b4ef5b5c71b54a0e94775b925d216b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-storage-samples-using-java"></a><span data-ttu-id="b96a4-104">Azure Storage-voorbeelden u Java gebruikt</span><span class="sxs-lookup"><span data-stu-id="b96a4-104">Azure Storage samples using Java</span></span>

## <a name="java-sample-index"></a><span data-ttu-id="b96a4-105">Index van Java-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="b96a4-105">Java sample index</span></span>

<span data-ttu-id="b96a4-106">De volgende tabel bevat een overzicht van onze voorbeelden-opslagplaats en de scenario's worden behandeld in elk voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="b96a4-106">The following table provides an overview of our samples repository and the scenarios covered in each sample.</span></span> <span data-ttu-id="b96a4-107">Klik op de koppelingen naar de bijbehorende voorbeeldcode weergeven in GitHub.</span><span class="sxs-lookup"><span data-stu-id="b96a4-107">Click on the links to view the corresponding sample code in GitHub.</span></span>

<table style="font-size:90%"><thead><tr><th style="font-size:110%"><span data-ttu-id="b96a4-108">Eindpunt</span><span class="sxs-lookup"><span data-stu-id="b96a4-108">Endpoint</span></span></th><th style="font-size:110%"><span data-ttu-id="b96a4-109">Scenario</span><span class="sxs-lookup"><span data-stu-id="b96a4-109">Scenario</span></span></th><th style="font-size:110%"><span data-ttu-id="b96a4-110">Voorbeeldcode</span><span class="sxs-lookup"><span data-stu-id="b96a4-110">Sample Code</span></span></th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><span data-ttu-id="b96a4-111"><b>BLOB</b></span><span class="sxs-lookup"><span data-stu-id="b96a4-111"><b>Blob</b></span></span></td>
<td><span data-ttu-id="b96a4-112">Toevoeg-Blob</span><span class="sxs-lookup"><span data-stu-id="b96a4-112">Append Blob</span></span></td> 
<td><span data-ttu-id="b96a4-113"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Aan de slag met Azure Blob-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="b96a4-113"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="b96a4-114">Blok-Blob</span><span class="sxs-lookup"><span data-stu-id="b96a4-114">Block Blob</span></span></td>
<td><span data-ttu-id="b96a4-115"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Aan de slag met Azure Blob-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="b96a4-115"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="b96a4-116">Clientversleuteling</span><span class="sxs-lookup"><span data-stu-id="b96a4-116">Client-Side Encryption</span></span></td>
<td><span data-ttu-id="b96a4-117"><a href="https://github.com/Azure-Samples/storage-java-client-side-encryption">Aan de slag met Azure versleuteling voor aan de clientzijde in Java</a></span><span class="sxs-lookup"><span data-stu-id="b96a4-117"><a href="https://github.com/Azure-Samples/storage-java-client-side-encryption">Getting Started with Azure Client Side Encryption in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="b96a4-118">Blob kopiëren</span><span class="sxs-lookup"><span data-stu-id="b96a4-118">Copy Blob</span></span></td>
<td><span data-ttu-id="b96a4-119"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Aan de slag met Azure Blob-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="b96a4-119"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="b96a4-120">Container maken</span><span class="sxs-lookup"><span data-stu-id="b96a4-120">Create Container</span></span></td>
<td><span data-ttu-id="b96a4-121"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Aan de slag met Azure Blob-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="b96a4-121"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="b96a4-122">Verwijderen van Blob</span><span class="sxs-lookup"><span data-stu-id="b96a4-122">Delete Blob</span></span></td>
<td><span data-ttu-id="b96a4-123"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Aan de slag met Azure Blob-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="b96a4-123"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="b96a4-124">Verwijderen van Container</span><span class="sxs-lookup"><span data-stu-id="b96a4-124">Delete Container</span></span></td>
<td><span data-ttu-id="b96a4-125"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Aan de slag met Azure Blob-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="b96a4-125"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="b96a4-126">BLOB eigenschappen-metagegevens/Stats</span><span class="sxs-lookup"><span data-stu-id="b96a4-126">Blob Metadata/Properties/Stats</span></span></td>
<td><span data-ttu-id="b96a4-127"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Aan de slag met Azure Blob-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="b96a4-127"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="b96a4-128">ACL, metagegevens/eigenschappen van container</span><span class="sxs-lookup"><span data-stu-id="b96a4-128">Container ACL/Metadata/Properties</span></span></td>
<td><span data-ttu-id="b96a4-129"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Aan de slag met Azure Blob-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="b96a4-129"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="b96a4-130">Get-paginabereiken</span><span class="sxs-lookup"><span data-stu-id="b96a4-130">Get Page Ranges</span></span></td>
<td><span data-ttu-id="b96a4-131"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/CloudPageBlobTests.java">Pagina-Blob test voorbeeld</a></span><span class="sxs-lookup"><span data-stu-id="b96a4-131"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/CloudPageBlobTests.java">Page Blob Tests Sample</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="b96a4-132">De lease van Blob-Container</span><span class="sxs-lookup"><span data-stu-id="b96a4-132">Lease Blob/Container</span></span></td>
<td><span data-ttu-id="b96a4-133"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Aan de slag met Azure Blob-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="b96a4-133"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="b96a4-134">Lijst Blobcontainer</span><span class="sxs-lookup"><span data-stu-id="b96a4-134">List Blob/Container</span></span></td>
<td><span data-ttu-id="b96a4-135"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Aan de slag met Azure Blob-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="b96a4-135"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="b96a4-136">Pagina-Blob</span><span class="sxs-lookup"><span data-stu-id="b96a4-136">Page Blob</span></span></td>
<td><span data-ttu-id="b96a4-137"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Aan de slag met Azure Blob-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="b96a4-137"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr>
<tr> 
<td><span data-ttu-id="b96a4-138">SAS</span><span class="sxs-lookup"><span data-stu-id="b96a4-138">SAS</span></span></td>
<td><span data-ttu-id="b96a4-139"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/SasTests.java">Voorbeeld van SAS-Tests</a></span><span class="sxs-lookup"><span data-stu-id="b96a4-139"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/SasTests.java">SAS Tests Sample</a></span></span></td>
</tr>   
<tr> 
<td><span data-ttu-id="b96a4-140">Service-eigenschappen</span><span class="sxs-lookup"><span data-stu-id="b96a4-140">Service Properties</span></span></td>
<td><span data-ttu-id="b96a4-141"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Aan de slag met Azure Blob-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="b96a4-141"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr>           
<tr> 
<td><span data-ttu-id="b96a4-142">Momentopname Blob</span><span class="sxs-lookup"><span data-stu-id="b96a4-142">Snapshot Blob</span></span></td>
<td><span data-ttu-id="b96a4-143"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Aan de slag met Azure Blob-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="b96a4-143"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td rowspan="9"><span data-ttu-id="b96a4-144"><b>File</b></span><span class="sxs-lookup"><span data-stu-id="b96a4-144"><b>File</b></span></span></td>
<td><span data-ttu-id="b96a4-145">Mappen-Shares-bestanden maken</span><span class="sxs-lookup"><span data-stu-id="b96a4-145">Create Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="b96a4-146"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Aan de slag met Azure File-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="b96a4-146"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="b96a4-147">Mappen-Shares-bestanden verwijderen</span><span class="sxs-lookup"><span data-stu-id="b96a4-147">Delete Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="b96a4-148"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Aan de slag met Azure File-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="b96a4-148"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="b96a4-149">Directory eigenschappen/Metadata</span><span class="sxs-lookup"><span data-stu-id="b96a4-149">Directory Properties/Metadata</span></span></td> 
<td><span data-ttu-id="b96a4-150"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Aan de slag met Azure File-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="b96a4-150"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="b96a4-151">Bestanden downloaden</span><span class="sxs-lookup"><span data-stu-id="b96a4-151">Download Files</span></span></td> 
<td><span data-ttu-id="b96a4-152"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Aan de slag met Azure File-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="b96a4-152"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="b96a4-153">Bestand eigenschappen/metagegevens/metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="b96a4-153">File Properties/Metadata/Metrics</span></span></td> 
<td><span data-ttu-id="b96a4-154"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Aan de slag met Azure File-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="b96a4-154"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="b96a4-155">File Service Properties</span><span class="sxs-lookup"><span data-stu-id="b96a4-155">File Service Properties</span></span></td> 
<td><span data-ttu-id="b96a4-156"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Aan de slag met Azure File-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="b96a4-156"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="b96a4-157">Lijst met mappen en bestanden</span><span class="sxs-lookup"><span data-stu-id="b96a4-157">List Directories and Files</span></span></td> 
<td><span data-ttu-id="b96a4-158"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Aan de slag met Azure File-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="b96a4-158"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="b96a4-159">Lijst met Shares</span><span class="sxs-lookup"><span data-stu-id="b96a4-159">List Shares</span></span></td> 
<td><span data-ttu-id="b96a4-160"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Aan de slag met Azure File-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="b96a4-160"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="b96a4-161">Delen van metagegevens-eigenschappen-statistieken</span><span class="sxs-lookup"><span data-stu-id="b96a4-161">Share Properties/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="b96a4-162"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Aan de slag met Azure File-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="b96a4-162"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td rowspan="8"><span data-ttu-id="b96a4-163"><b>Wachtrij</b></span><span class="sxs-lookup"><span data-stu-id="b96a4-163"><b>Queue</b></span></span></td>
<td><span data-ttu-id="b96a4-164">Bericht toevoegen</span><span class="sxs-lookup"><span data-stu-id="b96a4-164">Add Message</span></span></td> 
<td><span data-ttu-id="b96a4-165"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/queue/gettingstarted/QueueBasics.java">Opslag Java Client Library-voorbeelden</a></span><span class="sxs-lookup"><span data-stu-id="b96a4-165"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/queue/gettingstarted/QueueBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="b96a4-166">Clientversleuteling</span><span class="sxs-lookup"><span data-stu-id="b96a4-166">Client-Side Encryption</span></span></td> 
<td><span data-ttu-id="b96a4-167"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/encryption/queue/gettingstarted/QueueGettingStarted.java">Opslag Java Client Library-voorbeelden</a></span><span class="sxs-lookup"><span data-stu-id="b96a4-167"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/encryption/queue/gettingstarted/QueueGettingStarted.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="b96a4-168">Wachtrijen maken</span><span class="sxs-lookup"><span data-stu-id="b96a4-168">Create Queues</span></span></td> 
<td><span data-ttu-id="b96a4-169"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Aan de slag met Azure Queue-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="b96a4-169"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="b96a4-170">Berichtenwachtrij/verwijderen</span><span class="sxs-lookup"><span data-stu-id="b96a4-170">Delete Message/Queue</span></span></td> 
<td><span data-ttu-id="b96a4-171"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Aan de slag met Azure Queue-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="b96a4-171"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="b96a4-172">Bericht</span><span class="sxs-lookup"><span data-stu-id="b96a4-172">Peek Message</span></span></td> 
<td><span data-ttu-id="b96a4-173"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Aan de slag met Azure Queue-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="b96a4-173"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="b96a4-174">Wachtrij metagegevens-ACL/Stats</span><span class="sxs-lookup"><span data-stu-id="b96a4-174">Queue ACL/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="b96a4-175"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Aan de slag met Azure Queue-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="b96a4-175"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="b96a4-176">Eigenschappen van de Queue-Service</span><span class="sxs-lookup"><span data-stu-id="b96a4-176">Queue Service Properties</span></span></td> 
<td><span data-ttu-id="b96a4-177"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Aan de slag met Azure Queue-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="b96a4-177"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="b96a4-178">Updatebericht</span><span class="sxs-lookup"><span data-stu-id="b96a4-178">Update Message</span></span></td> 
<td><span data-ttu-id="b96a4-179"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Aan de slag met Azure Queue-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="b96a4-179"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td rowspan="7"><span data-ttu-id="b96a4-180"><b>Tabel</b></span><span class="sxs-lookup"><span data-stu-id="b96a4-180"><b>Table</b></span></span></td>
<td><span data-ttu-id="b96a4-181">Tabel maken</span><span class="sxs-lookup"><span data-stu-id="b96a4-181">Create Table</span></span></td> 
<td><span data-ttu-id="b96a4-182"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Aan de slag met Azure Table-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="b96a4-182"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="b96a4-183">Entiteit/tabel verwijderen</span><span class="sxs-lookup"><span data-stu-id="b96a4-183">Delete Entity/Table</span></span></td> 
<td><span data-ttu-id="b96a4-184"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Aan de slag met Azure Table-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="b96a4-184"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="b96a4-185">De entiteit invoegen of Merge/verplaatsen</span><span class="sxs-lookup"><span data-stu-id="b96a4-185">Insert/Merge/Replace Entity</span></span></td> 
<td><span data-ttu-id="b96a4-186"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Opslag Java Client Library-voorbeelden</a></span><span class="sxs-lookup"><span data-stu-id="b96a4-186"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="b96a4-187">Query-entiteiten</span><span class="sxs-lookup"><span data-stu-id="b96a4-187">Query Entities</span></span></td> 
<td><span data-ttu-id="b96a4-188"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Aan de slag met Azure Table-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="b96a4-188"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="b96a4-189">Querytabellen</span><span class="sxs-lookup"><span data-stu-id="b96a4-189">Query Tables</span></span></td> 
<td><span data-ttu-id="b96a4-190"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Aan de slag met Azure Table-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="b96a4-190"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="b96a4-191">ACL/eigenschappen van de tabel</span><span class="sxs-lookup"><span data-stu-id="b96a4-191">Table ACL/Properties</span></span></td> 
<td><span data-ttu-id="b96a4-192"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableAdvanced.java">Aan de slag met Azure Table-Service in Java</a></span><span class="sxs-lookup"><span data-stu-id="b96a4-192"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableAdvanced.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="b96a4-193">Bijwerken van entiteit</span><span class="sxs-lookup"><span data-stu-id="b96a4-193">Update Entity</span></span></td> 
<td><span data-ttu-id="b96a4-194"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Opslag Java Client Library-voorbeelden</a></span><span class="sxs-lookup"><span data-stu-id="b96a4-194"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a><span data-ttu-id="b96a4-195">Azure-codevoorbeelden-bibliotheek</span><span class="sxs-lookup"><span data-stu-id="b96a4-195">Azure Code Samples library</span></span>

<span data-ttu-id="b96a4-196">Als u wilt de compleet codevoorbeeld bibliotheek bekijken, gaat u naar de [Azure codevoorbeelden](https://azure.microsoft.com/resources/samples/?service=storage) bibliotheek, waaronder voorbeelden voor Azure-opslag die u kunt downloaden en lokaal uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="b96a4-196">To view the complete sample library, go to the [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=storage) library, which includes samples for Azure Storage that you can download and run locally.</span></span> <span data-ttu-id="b96a4-197">De bibliotheek met voorbeeld wordt een voorbeeldcode in het ZIP-indeling.</span><span class="sxs-lookup"><span data-stu-id="b96a4-197">The Code Sample Library provides sample code in .zip format.</span></span> <span data-ttu-id="b96a4-198">U kunt ook bladeren en kloon de GitHub-opslagplaats voor elk voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="b96a4-198">Alternatively, you can browse and clone the GitHub repository for each sample.</span></span>

[!INCLUDE [storage-java-samples-include](../../includes/storage-java-samples-include.md)]

## <a name="getting-started-guides"></a><span data-ttu-id="b96a4-199">Ophalen van slag-handleidingen</span><span class="sxs-lookup"><span data-stu-id="b96a4-199">Getting started guides</span></span>

<span data-ttu-id="b96a4-200">Bekijk de volgende handleidingen in als u op zoek bent voor instructies over het installeren en aan de slag met de clientbibliotheken van Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="b96a4-200">Check out the following guides if you are looking for instructions on how to install and get started with the Azure Storage Client Libraries.</span></span>

* [<span data-ttu-id="b96a4-201">Aan de slag met Azure Blob-Service in Java</span><span class="sxs-lookup"><span data-stu-id="b96a4-201">Getting Started with Azure Blob Service in Java</span></span>](storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="b96a4-202">Aan de slag met Azure Queue-Service in Java</span><span class="sxs-lookup"><span data-stu-id="b96a4-202">Getting Started with Azure Queue Service in Java</span></span>](storage-java-how-to-use-queue-storage.md)
* [<span data-ttu-id="b96a4-203">Aan de slag met Azure Table-Service in Java</span><span class="sxs-lookup"><span data-stu-id="b96a4-203">Getting Started with Azure Table Service in Java</span></span>](storage-java-how-to-use-table-storage.md)
* [<span data-ttu-id="b96a4-204">Aan de slag met Azure File-Service in Java</span><span class="sxs-lookup"><span data-stu-id="b96a4-204">Getting Started with Azure File Service in Java</span></span>](storage-java-how-to-use-file-storage.md)

## <a name="next-steps"></a><span data-ttu-id="b96a4-205">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b96a4-205">Next steps</span></span>

<span data-ttu-id="b96a4-206">Voor informatie over steekproeven voor de andere talen:</span><span class="sxs-lookup"><span data-stu-id="b96a4-206">For information on samples for other languages:</span></span>

* <span data-ttu-id="b96a4-207">.NET: [voorbeelden van azure Storage met .NET](storage-samples-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="b96a4-207">.NET: [Azure Storage samples using .NET](storage-samples-dotnet.md)</span></span>
* <span data-ttu-id="b96a4-208">Alle andere talen: [Azure Storage-voorbeelden](storage-samples.md)</span><span class="sxs-lookup"><span data-stu-id="b96a4-208">All other languages: [Azure Storage samples](storage-samples.md)</span></span>
