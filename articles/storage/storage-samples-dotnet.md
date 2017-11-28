---
title: Voorbeelden van aaaAzure Storage met .NET | Microsoft Docs
description: Weergeven, downloaden en uitvoeren van toepassingen voor Azure Storage en voorbeeldcode. Ontdek aan de slag voorbeelden voor blobs, wachtrijen, tabellen en bestanden, met behulp van Hallo-opslagclientbibliotheken voor .NET.
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 01/12/2017
ms.author: seguler
ms.openlocfilehash: 9a7055645b0f0658b850f024b8b19ab19840330e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-samples-using-net"></a><span data-ttu-id="345d2-104">Voorbeelden van Azure Storage met .NET</span><span class="sxs-lookup"><span data-stu-id="345d2-104">Azure Storage samples using .NET</span></span>

## <a name="net-sample-index"></a><span data-ttu-id="345d2-105">Index van .NET-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="345d2-105">.NET sample index</span></span>

<span data-ttu-id="345d2-106">Hallo volgende tabel geeft een overzicht van onze voorbeelden opslagplaats en Hallo scenario's die in elk voorbeeld worden behandeld.</span><span class="sxs-lookup"><span data-stu-id="345d2-106">hello following table provides an overview of our samples repository and hello scenarios covered in each sample.</span></span> <span data-ttu-id="345d2-107">Klik op Hallo koppelingen tooview Hallo bijbehorende voorbeeldcode in GitHub.</span><span class="sxs-lookup"><span data-stu-id="345d2-107">Click on hello links tooview hello corresponding sample code in GitHub.</span></span>

<table style="font-size:90%"><thead><tr><th style="font-size:110%"><span data-ttu-id="345d2-108">Eindpunt</span><span class="sxs-lookup"><span data-stu-id="345d2-108">Endpoint</span></span></th><th style="font-size:110%"><span data-ttu-id="345d2-109">Scenario</span><span class="sxs-lookup"><span data-stu-id="345d2-109">Scenario</span></span></th><th style="font-size:110%"><span data-ttu-id="345d2-110">Voorbeeldcode</span><span class="sxs-lookup"><span data-stu-id="345d2-110">Sample Code</span></span></th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><span data-ttu-id="345d2-111"><b>BLOB</b></span><span class="sxs-lookup"><span data-stu-id="345d2-111"><b>Blob</b></span></span></td>
<td><span data-ttu-id="345d2-112">Toevoeg-Blob</span><span class="sxs-lookup"><span data-stu-id="345d2-112">Append Blob</span></span></td> 
<td><span data-ttu-id="345d2-113"><a href="https://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.getappendblobreference.aspx">Voorbeeld van de methode CloudBlobContainer.GetAppendBlobReference</a></span><span class="sxs-lookup"><span data-stu-id="345d2-113"><a href="https://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.getappendblobreference.aspx">CloudBlobContainer.GetAppendBlobReference Method Example</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="345d2-114">Blok-Blob</span><span class="sxs-lookup"><span data-stu-id="345d2-114">Block Blob</span></span></td>
<td><span data-ttu-id="345d2-115"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Fotogalerie-webtoepassing</a></span><span class="sxs-lookup"><span data-stu-id="345d2-115"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="345d2-116">Clientversleuteling</span><span class="sxs-lookup"><span data-stu-id="345d2-116">Client-Side Encryption</span></span></td>
<td><span data-ttu-id="345d2-117"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/BlobGettingStarted/Program.cs">Voorbeelden van BLOB-versleuteling</a></span><span class="sxs-lookup"><span data-stu-id="345d2-117"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/BlobGettingStarted/Program.cs">Blob Encryption Samples</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="345d2-118">Blob kopiëren</span><span class="sxs-lookup"><span data-stu-id="345d2-118">Copy Blob</span></span></td>
<td><span data-ttu-id="345d2-119"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Aan de slag met Blobs</a></span><span class="sxs-lookup"><span data-stu-id="345d2-119"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="345d2-120">Container maken</span><span class="sxs-lookup"><span data-stu-id="345d2-120">Create Container</span></span></td>
<td><span data-ttu-id="345d2-121"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Fotogalerie-webtoepassing</a></span><span class="sxs-lookup"><span data-stu-id="345d2-121"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="345d2-122">Verwijderen van Blob</span><span class="sxs-lookup"><span data-stu-id="345d2-122">Delete Blob</span></span></td>
<td><span data-ttu-id="345d2-123"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Fotogalerie-webtoepassing</a></span><span class="sxs-lookup"><span data-stu-id="345d2-123"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="345d2-124">Verwijderen van Container</span><span class="sxs-lookup"><span data-stu-id="345d2-124">Delete Container</span></span></td>
<td><span data-ttu-id="345d2-125"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Aan de slag met Blobs</a></span><span class="sxs-lookup"><span data-stu-id="345d2-125"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="345d2-126">BLOB eigenschappen-metagegevens/Stats</span><span class="sxs-lookup"><span data-stu-id="345d2-126">Blob Metadata/Properties/Stats</span></span></td>
<td><span data-ttu-id="345d2-127"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Aan de slag met Blobs</a></span><span class="sxs-lookup"><span data-stu-id="345d2-127"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="345d2-128">ACL, metagegevens/eigenschappen van container</span><span class="sxs-lookup"><span data-stu-id="345d2-128">Container ACL/Metadata/Properties</span></span></td>
<td><span data-ttu-id="345d2-129"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Fotogalerie-webtoepassing</a></span><span class="sxs-lookup"><span data-stu-id="345d2-129"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="345d2-130">Get-paginabereiken</span><span class="sxs-lookup"><span data-stu-id="345d2-130">Get Page Ranges</span></span></td>
<td><span data-ttu-id="345d2-131"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Aan de slag met Blobs</a></span><span class="sxs-lookup"><span data-stu-id="345d2-131"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="345d2-132">De lease van Blob-Container</span><span class="sxs-lookup"><span data-stu-id="345d2-132">Lease Blob/Container</span></span></td>
<td><span data-ttu-id="345d2-133"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Aan de slag met Blobs</a></span><span class="sxs-lookup"><span data-stu-id="345d2-133"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="345d2-134">Lijst Blobcontainer</span><span class="sxs-lookup"><span data-stu-id="345d2-134">List Blob/Container</span></span></td>
<td><span data-ttu-id="345d2-135"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Aan de slag met Blobs</a></span><span class="sxs-lookup"><span data-stu-id="345d2-135"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="345d2-136">Pagina-Blob</span><span class="sxs-lookup"><span data-stu-id="345d2-136">Page Blob</span></span></td>
<td><span data-ttu-id="345d2-137"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Aan de slag met Blobs</a></span><span class="sxs-lookup"><span data-stu-id="345d2-137"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a></span></span></td>
</tr>
<tr> 
<td><span data-ttu-id="345d2-138">SAS</span><span class="sxs-lookup"><span data-stu-id="345d2-138">SAS</span></span></td>
<td><span data-ttu-id="345d2-139"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Aan de slag met Blobs</a></span><span class="sxs-lookup"><span data-stu-id="345d2-139"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr>   
<tr> 
<td><span data-ttu-id="345d2-140">Service-eigenschappen</span><span class="sxs-lookup"><span data-stu-id="345d2-140">Service Properties</span></span></td>
<td><span data-ttu-id="345d2-141"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Aan de slag met Blobs</a></span><span class="sxs-lookup"><span data-stu-id="345d2-141"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr>           
<tr> 
<td><span data-ttu-id="345d2-142">Momentopname Blob</span><span class="sxs-lookup"><span data-stu-id="345d2-142">Snapshot Blob</span></span></td>
<td><span data-ttu-id="345d2-143"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-back-up-with-incremental-snapshots/blob/master/Program.cs">Back-virtuele Machine van Azure-schijven met incrementele momentopnamen</a></span><span class="sxs-lookup"><span data-stu-id="345d2-143"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-back-up-with-incremental-snapshots/blob/master/Program.cs">Backup Azure Virtual Machine Disks with Incremental Snapshots</a></span></span></td>
</tr> 
<tr> 
<td rowspan="9"><span data-ttu-id="345d2-144"><b>File</b></span><span class="sxs-lookup"><span data-stu-id="345d2-144"><b>File</b></span></span></td>
<td><span data-ttu-id="345d2-145">Mappen-Shares-bestanden maken</span><span class="sxs-lookup"><span data-stu-id="345d2-145">Create Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="345d2-146"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET-voorbeeldbestand opslag</a></span><span class="sxs-lookup"><span data-stu-id="345d2-146"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="345d2-147">Mappen-Shares-bestanden verwijderen</span><span class="sxs-lookup"><span data-stu-id="345d2-147">Delete Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="345d2-148"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/master/FileStorage/GettingStarted.cs">Aan de slag met Azure File-Service in .NET</a></span><span class="sxs-lookup"><span data-stu-id="345d2-148"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/master/FileStorage/GettingStarted.cs">Getting Started with Azure File Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="345d2-149">Directory eigenschappen/Metadata</span><span class="sxs-lookup"><span data-stu-id="345d2-149">Directory Properties/Metadata</span></span></td> 
<td><span data-ttu-id="345d2-150"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET-voorbeeldbestand opslag</a></span><span class="sxs-lookup"><span data-stu-id="345d2-150"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="345d2-151">Bestanden downloaden</span><span class="sxs-lookup"><span data-stu-id="345d2-151">Download Files</span></span></td> 
<td><span data-ttu-id="345d2-152"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET-voorbeeldbestand opslag</a></span><span class="sxs-lookup"><span data-stu-id="345d2-152"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="345d2-153">Bestand eigenschappen/metagegevens/metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="345d2-153">File Properties/Metadata/Metrics</span></span></td> 
<td><span data-ttu-id="345d2-154"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET-voorbeeldbestand opslag</a></span><span class="sxs-lookup"><span data-stu-id="345d2-154"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="345d2-155">File Service Properties</span><span class="sxs-lookup"><span data-stu-id="345d2-155">File Service Properties</span></span></td> 
<td><span data-ttu-id="345d2-156"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET-voorbeeldbestand opslag</a></span><span class="sxs-lookup"><span data-stu-id="345d2-156"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="345d2-157">Lijst met mappen en bestanden</span><span class="sxs-lookup"><span data-stu-id="345d2-157">List Directories and Files</span></span></td> 
<td><span data-ttu-id="345d2-158"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET-voorbeeldbestand opslag</a></span><span class="sxs-lookup"><span data-stu-id="345d2-158"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="345d2-159">Lijst met Shares</span><span class="sxs-lookup"><span data-stu-id="345d2-159">List Shares</span></span></td> 
<td><span data-ttu-id="345d2-160"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET-voorbeeldbestand opslag</a></span><span class="sxs-lookup"><span data-stu-id="345d2-160"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="345d2-161">Delen van metagegevens-eigenschappen-statistieken</span><span class="sxs-lookup"><span data-stu-id="345d2-161">Share Properties/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="345d2-162"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET-voorbeeldbestand opslag</a></span><span class="sxs-lookup"><span data-stu-id="345d2-162"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td rowspan="8"><span data-ttu-id="345d2-163"><b>Wachtrij</b></span><span class="sxs-lookup"><span data-stu-id="345d2-163"><b>Queue</b></span></span></td>
<td><span data-ttu-id="345d2-164">Bericht toevoegen</span><span class="sxs-lookup"><span data-stu-id="345d2-164">Add Message</span></span></td> 
<td><span data-ttu-id="345d2-165"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Aan de slag met Azure Queue-Service in .NET</a></span><span class="sxs-lookup"><span data-stu-id="345d2-165"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="345d2-166">Clientversleuteling</span><span class="sxs-lookup"><span data-stu-id="345d2-166">Client-Side Encryption</span></span></td> 
<td><span data-ttu-id="345d2-167"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/QueueGettingStarted/Program.cs">Azure Storage .NET wachtrij Client-Side-versleuteling</a></span><span class="sxs-lookup"><span data-stu-id="345d2-167"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/QueueGettingStarted/Program.cs">Azure Storage .NET Queue Client-Side Encryption</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="345d2-168">Wachtrijen maken</span><span class="sxs-lookup"><span data-stu-id="345d2-168">Create Queues</span></span></td> 
<td><span data-ttu-id="345d2-169"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Aan de slag met Azure Queue-Service in .NET</a></span><span class="sxs-lookup"><span data-stu-id="345d2-169"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="345d2-170">Berichtenwachtrij/verwijderen</span><span class="sxs-lookup"><span data-stu-id="345d2-170">Delete Message/Queue</span></span></td> 
<td><span data-ttu-id="345d2-171"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Aan de slag met Azure Queue-Service in .NET</a></span><span class="sxs-lookup"><span data-stu-id="345d2-171"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="345d2-172">Bericht</span><span class="sxs-lookup"><span data-stu-id="345d2-172">Peek Message</span></span></td> 
<td><span data-ttu-id="345d2-173"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Aan de slag met Azure Queue-Service in .NET</a></span><span class="sxs-lookup"><span data-stu-id="345d2-173"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="345d2-174">Wachtrij metagegevens-ACL/Stats</span><span class="sxs-lookup"><span data-stu-id="345d2-174">Queue ACL/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="345d2-175"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Aan de slag met Azure Queue-Service in .NET</a></span><span class="sxs-lookup"><span data-stu-id="345d2-175"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="345d2-176">Eigenschappen van de Queue-Service</span><span class="sxs-lookup"><span data-stu-id="345d2-176">Queue Service Properties</span></span></td> 
<td><span data-ttu-id="345d2-177"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Aan de slag met Azure Queue-Service in .NET</a></span><span class="sxs-lookup"><span data-stu-id="345d2-177"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="345d2-178">Updatebericht</span><span class="sxs-lookup"><span data-stu-id="345d2-178">Update Message</span></span></td> 
<td><span data-ttu-id="345d2-179"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Aan de slag met Azure Queue-Service in .NET</a></span><span class="sxs-lookup"><span data-stu-id="345d2-179"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td rowspan="7"><span data-ttu-id="345d2-180"><b>Tabel</b></span><span class="sxs-lookup"><span data-stu-id="345d2-180"><b>Table</b></span></span></td>
<td><span data-ttu-id="345d2-181">Tabel maken</span><span class="sxs-lookup"><span data-stu-id="345d2-181">Create Table</span></span></td> 
<td><span data-ttu-id="345d2-182"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Gelijktijdigheid van taken met behulp van Azure Storage - voorbeeldtoepassing beheren</a></span><span class="sxs-lookup"><span data-stu-id="345d2-182"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="345d2-183">Entiteit/tabel verwijderen</span><span class="sxs-lookup"><span data-stu-id="345d2-183">Delete Entity/Table</span></span></td> 
<td><span data-ttu-id="345d2-184"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Aan de slag met Azure Table Storage in .NET</a></span><span class="sxs-lookup"><span data-stu-id="345d2-184"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="345d2-185">De entiteit invoegen of Merge/verplaatsen</span><span class="sxs-lookup"><span data-stu-id="345d2-185">Insert/Merge/Replace Entity</span></span></td> 
<td><span data-ttu-id="345d2-186"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Gelijktijdigheid van taken met behulp van Azure Storage - voorbeeldtoepassing beheren</a></span><span class="sxs-lookup"><span data-stu-id="345d2-186"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="345d2-187">Query-entiteiten</span><span class="sxs-lookup"><span data-stu-id="345d2-187">Query Entities</span></span></td> 
<td><span data-ttu-id="345d2-188"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Aan de slag met Azure Table Storage in .NET</a></span><span class="sxs-lookup"><span data-stu-id="345d2-188"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="345d2-189">Querytabellen</span><span class="sxs-lookup"><span data-stu-id="345d2-189">Query Tables</span></span></td> 
<td><span data-ttu-id="345d2-190"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Aan de slag met Azure Table Storage in .NET</a></span><span class="sxs-lookup"><span data-stu-id="345d2-190"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="345d2-191">ACL/eigenschappen van de tabel</span><span class="sxs-lookup"><span data-stu-id="345d2-191">Table ACL/Properties</span></span></td> 
<td><span data-ttu-id="345d2-192"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/AdvancedSamples.cs">Aan de slag met Azure Table Storage in .NET</a></span><span class="sxs-lookup"><span data-stu-id="345d2-192"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/AdvancedSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="345d2-193">Bijwerken van entiteit</span><span class="sxs-lookup"><span data-stu-id="345d2-193">Update Entity</span></span></td> 
<td><span data-ttu-id="345d2-194"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Gelijktijdigheid van taken met behulp van Azure Storage - voorbeeldtoepassing beheren</a></span><span class="sxs-lookup"><span data-stu-id="345d2-194"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a><span data-ttu-id="345d2-195">Azure-codevoorbeelden-bibliotheek</span><span class="sxs-lookup"><span data-stu-id="345d2-195">Azure Code Samples library</span></span>

<span data-ttu-id="345d2-196">tooview hello compleet codevoorbeeld bibliotheek, Ga toohello [Azure codevoorbeelden](https://azure.microsoft.com/resources/samples/?service=storage) bibliotheek, waaronder voorbeelden voor Azure-opslag die u kunt downloaden en lokaal uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="345d2-196">tooview hello complete sample library, go toohello [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=storage) library, which includes samples for Azure Storage that you can download and run locally.</span></span> <span data-ttu-id="345d2-197">Hallo Code voorbeeld van een bibliotheek bevat voorbeeldcode in het ZIP-indeling.</span><span class="sxs-lookup"><span data-stu-id="345d2-197">hello Code Sample Library provides sample code in .zip format.</span></span> <span data-ttu-id="345d2-198">U kunt ook bladeren en Hallo GitHub-opslagplaats voor elk voorbeeld klonen.</span><span class="sxs-lookup"><span data-stu-id="345d2-198">Alternatively, you can browse and clone hello GitHub repository for each sample.</span></span>

[!INCLUDE [storage-dotnet-samples-include](../../includes/storage-dotnet-samples-include.md)]

## <a name="getting-started-guides"></a><span data-ttu-id="345d2-199">Ophalen van slag-handleidingen</span><span class="sxs-lookup"><span data-stu-id="345d2-199">Getting started guides</span></span>

<span data-ttu-id="345d2-200">Hallo handleidingen volgen als u op zoek bent voor instructies over het uitchecken tooinstall en aan de slag met Hallo clientbibliotheken van Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="345d2-200">Check out hello following guides if you are looking for instructions on how tooinstall and get started with hello Azure Storage Client Libraries.</span></span>

* [<span data-ttu-id="345d2-201">Aan de slag met Azure Blob-Service in .NET</span><span class="sxs-lookup"><span data-stu-id="345d2-201">Getting Started with Azure Blob Service in .NET</span></span>](storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="345d2-202">Aan de slag met Azure Queue-Service in .NET</span><span class="sxs-lookup"><span data-stu-id="345d2-202">Getting Started with Azure Queue Service in .NET</span></span>](storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="345d2-203">Aan de slag met Azure Table-Service in .NET</span><span class="sxs-lookup"><span data-stu-id="345d2-203">Getting Started with Azure Table Service in .NET</span></span>](storage-dotnet-how-to-use-tables.md)
* [<span data-ttu-id="345d2-204">Aan de slag met Azure File-Service in .NET</span><span class="sxs-lookup"><span data-stu-id="345d2-204">Getting Started with Azure File Service in .NET</span></span>](storage-dotnet-how-to-use-files.md)

## <a name="next-steps"></a><span data-ttu-id="345d2-205">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="345d2-205">Next steps</span></span>

<span data-ttu-id="345d2-206">Voor informatie over steekproeven voor de andere talen:</span><span class="sxs-lookup"><span data-stu-id="345d2-206">For information on samples for other languages:</span></span>

* <span data-ttu-id="345d2-207">Java: [voorbeelden van Azure Storage met Java](storage-samples-java.md)</span><span class="sxs-lookup"><span data-stu-id="345d2-207">Java: [Azure Storage samples using Java](storage-samples-java.md)</span></span>
* <span data-ttu-id="345d2-208">Alle andere talen: [Azure Storage-voorbeelden](storage-samples.md)</span><span class="sxs-lookup"><span data-stu-id="345d2-208">All other languages: [Azure Storage samples](storage-samples.md)</span></span>
