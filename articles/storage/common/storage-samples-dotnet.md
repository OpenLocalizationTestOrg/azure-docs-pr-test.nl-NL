---
title: Voorbeelden van Azure Storage met .NET | Microsoft Docs
description: Weergeven, downloaden en uitvoeren van toepassingen voor Azure Storage en voorbeeldcode. Ontdek aan de slag voorbeelden voor blobs, wachtrijen, tabellen en bestanden, met behulp van de opslagclientbibliotheken voor .NET.
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
ms.openlocfilehash: 74777ed14ebb41ad31657f814e86724ff1e5e62e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-storage-samples-using-net"></a><span data-ttu-id="7274e-104">Voorbeelden van Azure Storage met .NET</span><span class="sxs-lookup"><span data-stu-id="7274e-104">Azure Storage samples using .NET</span></span>

## <a name="net-sample-index"></a><span data-ttu-id="7274e-105">Index van .NET-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="7274e-105">.NET sample index</span></span>

<span data-ttu-id="7274e-106">De volgende tabel bevat een overzicht van onze voorbeelden-opslagplaats en de scenario's worden behandeld in elk voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="7274e-106">The following table provides an overview of our samples repository and the scenarios covered in each sample.</span></span> <span data-ttu-id="7274e-107">Klik op de koppelingen naar de bijbehorende voorbeeldcode weergeven in GitHub.</span><span class="sxs-lookup"><span data-stu-id="7274e-107">Click on the links to view the corresponding sample code in GitHub.</span></span>

<table style="font-size:90%"><thead><tr><th style="font-size:110%"><span data-ttu-id="7274e-108">Eindpunt</span><span class="sxs-lookup"><span data-stu-id="7274e-108">Endpoint</span></span></th><th style="font-size:110%"><span data-ttu-id="7274e-109">Scenario</span><span class="sxs-lookup"><span data-stu-id="7274e-109">Scenario</span></span></th><th style="font-size:110%"><span data-ttu-id="7274e-110">Voorbeeldcode</span><span class="sxs-lookup"><span data-stu-id="7274e-110">Sample Code</span></span></th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><span data-ttu-id="7274e-111"><b>BLOB</b></span><span class="sxs-lookup"><span data-stu-id="7274e-111"><b>Blob</b></span></span></td>
<td><span data-ttu-id="7274e-112">Toevoeg-Blob</span><span class="sxs-lookup"><span data-stu-id="7274e-112">Append Blob</span></span></td> 
<td><span data-ttu-id="7274e-113"><a href="https://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.getappendblobreference.aspx">Voorbeeld van de methode CloudBlobContainer.GetAppendBlobReference</a></span><span class="sxs-lookup"><span data-stu-id="7274e-113"><a href="https://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.getappendblobreference.aspx">CloudBlobContainer.GetAppendBlobReference Method Example</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="7274e-114">Blok-Blob</span><span class="sxs-lookup"><span data-stu-id="7274e-114">Block Blob</span></span></td>
<td><span data-ttu-id="7274e-115"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Fotogalerie-webtoepassing</a></span><span class="sxs-lookup"><span data-stu-id="7274e-115"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="7274e-116">Clientversleuteling</span><span class="sxs-lookup"><span data-stu-id="7274e-116">Client-Side Encryption</span></span></td>
<td><span data-ttu-id="7274e-117"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/BlobGettingStarted/Program.cs">Voorbeelden van BLOB-versleuteling</a></span><span class="sxs-lookup"><span data-stu-id="7274e-117"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/BlobGettingStarted/Program.cs">Blob Encryption Samples</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="7274e-118">Blob kopiëren</span><span class="sxs-lookup"><span data-stu-id="7274e-118">Copy Blob</span></span></td>
<td><span data-ttu-id="7274e-119"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Aan de slag met Blobs</a></span><span class="sxs-lookup"><span data-stu-id="7274e-119"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="7274e-120">Container maken</span><span class="sxs-lookup"><span data-stu-id="7274e-120">Create Container</span></span></td>
<td><span data-ttu-id="7274e-121"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Fotogalerie-webtoepassing</a></span><span class="sxs-lookup"><span data-stu-id="7274e-121"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="7274e-122">Verwijderen van Blob</span><span class="sxs-lookup"><span data-stu-id="7274e-122">Delete Blob</span></span></td>
<td><span data-ttu-id="7274e-123"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Fotogalerie-webtoepassing</a></span><span class="sxs-lookup"><span data-stu-id="7274e-123"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="7274e-124">Verwijderen van Container</span><span class="sxs-lookup"><span data-stu-id="7274e-124">Delete Container</span></span></td>
<td><span data-ttu-id="7274e-125"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Aan de slag met Blobs</a></span><span class="sxs-lookup"><span data-stu-id="7274e-125"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="7274e-126">BLOB eigenschappen-metagegevens/Stats</span><span class="sxs-lookup"><span data-stu-id="7274e-126">Blob Metadata/Properties/Stats</span></span></td>
<td><span data-ttu-id="7274e-127"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Aan de slag met Blobs</a></span><span class="sxs-lookup"><span data-stu-id="7274e-127"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="7274e-128">ACL, metagegevens/eigenschappen van container</span><span class="sxs-lookup"><span data-stu-id="7274e-128">Container ACL/Metadata/Properties</span></span></td>
<td><span data-ttu-id="7274e-129"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Fotogalerie-webtoepassing</a></span><span class="sxs-lookup"><span data-stu-id="7274e-129"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="7274e-130">Get-paginabereiken</span><span class="sxs-lookup"><span data-stu-id="7274e-130">Get Page Ranges</span></span></td>
<td><span data-ttu-id="7274e-131"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Aan de slag met Blobs</a></span><span class="sxs-lookup"><span data-stu-id="7274e-131"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="7274e-132">De lease van Blob-Container</span><span class="sxs-lookup"><span data-stu-id="7274e-132">Lease Blob/Container</span></span></td>
<td><span data-ttu-id="7274e-133"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Aan de slag met Blobs</a></span><span class="sxs-lookup"><span data-stu-id="7274e-133"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="7274e-134">Lijst Blobcontainer</span><span class="sxs-lookup"><span data-stu-id="7274e-134">List Blob/Container</span></span></td>
<td><span data-ttu-id="7274e-135"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Aan de slag met Blobs</a></span><span class="sxs-lookup"><span data-stu-id="7274e-135"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="7274e-136">Pagina-Blob</span><span class="sxs-lookup"><span data-stu-id="7274e-136">Page Blob</span></span></td>
<td><span data-ttu-id="7274e-137"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Aan de slag met Blobs</a></span><span class="sxs-lookup"><span data-stu-id="7274e-137"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a></span></span></td>
</tr>
<tr> 
<td><span data-ttu-id="7274e-138">SAS</span><span class="sxs-lookup"><span data-stu-id="7274e-138">SAS</span></span></td>
<td><span data-ttu-id="7274e-139"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Aan de slag met Blobs</a></span><span class="sxs-lookup"><span data-stu-id="7274e-139"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr>   
<tr> 
<td><span data-ttu-id="7274e-140">Service-eigenschappen</span><span class="sxs-lookup"><span data-stu-id="7274e-140">Service Properties</span></span></td>
<td><span data-ttu-id="7274e-141"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Aan de slag met Blobs</a></span><span class="sxs-lookup"><span data-stu-id="7274e-141"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr>           
<tr> 
<td><span data-ttu-id="7274e-142">Momentopname Blob</span><span class="sxs-lookup"><span data-stu-id="7274e-142">Snapshot Blob</span></span></td>
<td><span data-ttu-id="7274e-143"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-back-up-with-incremental-snapshots/blob/master/Program.cs">Back-virtuele Machine van Azure-schijven met incrementele momentopnamen</a></span><span class="sxs-lookup"><span data-stu-id="7274e-143"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-back-up-with-incremental-snapshots/blob/master/Program.cs">Backup Azure Virtual Machine Disks with Incremental Snapshots</a></span></span></td>
</tr> 
<tr> 
<td rowspan="9"><span data-ttu-id="7274e-144"><b>File</b></span><span class="sxs-lookup"><span data-stu-id="7274e-144"><b>File</b></span></span></td>
<td><span data-ttu-id="7274e-145">Mappen-Shares-bestanden maken</span><span class="sxs-lookup"><span data-stu-id="7274e-145">Create Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="7274e-146"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET-voorbeeldbestand opslag</a></span><span class="sxs-lookup"><span data-stu-id="7274e-146"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="7274e-147">Mappen-Shares-bestanden verwijderen</span><span class="sxs-lookup"><span data-stu-id="7274e-147">Delete Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="7274e-148"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/master/FileStorage/GettingStarted.cs">Aan de slag met Azure File-Service in .NET</a></span><span class="sxs-lookup"><span data-stu-id="7274e-148"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/master/FileStorage/GettingStarted.cs">Getting Started with Azure File Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="7274e-149">Directory eigenschappen/Metadata</span><span class="sxs-lookup"><span data-stu-id="7274e-149">Directory Properties/Metadata</span></span></td> 
<td><span data-ttu-id="7274e-150"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET-voorbeeldbestand opslag</a></span><span class="sxs-lookup"><span data-stu-id="7274e-150"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="7274e-151">Bestanden downloaden</span><span class="sxs-lookup"><span data-stu-id="7274e-151">Download Files</span></span></td> 
<td><span data-ttu-id="7274e-152"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET-voorbeeldbestand opslag</a></span><span class="sxs-lookup"><span data-stu-id="7274e-152"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="7274e-153">Bestand eigenschappen/metagegevens/metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="7274e-153">File Properties/Metadata/Metrics</span></span></td> 
<td><span data-ttu-id="7274e-154"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET-voorbeeldbestand opslag</a></span><span class="sxs-lookup"><span data-stu-id="7274e-154"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="7274e-155">File Service Properties</span><span class="sxs-lookup"><span data-stu-id="7274e-155">File Service Properties</span></span></td> 
<td><span data-ttu-id="7274e-156"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET-voorbeeldbestand opslag</a></span><span class="sxs-lookup"><span data-stu-id="7274e-156"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="7274e-157">Lijst met mappen en bestanden</span><span class="sxs-lookup"><span data-stu-id="7274e-157">List Directories and Files</span></span></td> 
<td><span data-ttu-id="7274e-158"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET-voorbeeldbestand opslag</a></span><span class="sxs-lookup"><span data-stu-id="7274e-158"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="7274e-159">Lijst met Shares</span><span class="sxs-lookup"><span data-stu-id="7274e-159">List Shares</span></span></td> 
<td><span data-ttu-id="7274e-160"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET-voorbeeldbestand opslag</a></span><span class="sxs-lookup"><span data-stu-id="7274e-160"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="7274e-161">Delen van metagegevens-eigenschappen-statistieken</span><span class="sxs-lookup"><span data-stu-id="7274e-161">Share Properties/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="7274e-162"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET-voorbeeldbestand opslag</a></span><span class="sxs-lookup"><span data-stu-id="7274e-162"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td rowspan="8"><span data-ttu-id="7274e-163"><b>Wachtrij</b></span><span class="sxs-lookup"><span data-stu-id="7274e-163"><b>Queue</b></span></span></td>
<td><span data-ttu-id="7274e-164">Bericht toevoegen</span><span class="sxs-lookup"><span data-stu-id="7274e-164">Add Message</span></span></td> 
<td><span data-ttu-id="7274e-165"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Aan de slag met Azure Queue-Service in .NET</a></span><span class="sxs-lookup"><span data-stu-id="7274e-165"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="7274e-166">Clientversleuteling</span><span class="sxs-lookup"><span data-stu-id="7274e-166">Client-Side Encryption</span></span></td> 
<td><span data-ttu-id="7274e-167"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/QueueGettingStarted/Program.cs">Azure Storage .NET wachtrij Client-Side-versleuteling</a></span><span class="sxs-lookup"><span data-stu-id="7274e-167"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/QueueGettingStarted/Program.cs">Azure Storage .NET Queue Client-Side Encryption</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="7274e-168">Wachtrijen maken</span><span class="sxs-lookup"><span data-stu-id="7274e-168">Create Queues</span></span></td> 
<td><span data-ttu-id="7274e-169"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Aan de slag met Azure Queue-Service in .NET</a></span><span class="sxs-lookup"><span data-stu-id="7274e-169"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="7274e-170">Berichtenwachtrij/verwijderen</span><span class="sxs-lookup"><span data-stu-id="7274e-170">Delete Message/Queue</span></span></td> 
<td><span data-ttu-id="7274e-171"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Aan de slag met Azure Queue-Service in .NET</a></span><span class="sxs-lookup"><span data-stu-id="7274e-171"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="7274e-172">Bericht</span><span class="sxs-lookup"><span data-stu-id="7274e-172">Peek Message</span></span></td> 
<td><span data-ttu-id="7274e-173"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Aan de slag met Azure Queue-Service in .NET</a></span><span class="sxs-lookup"><span data-stu-id="7274e-173"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="7274e-174">Wachtrij metagegevens-ACL/Stats</span><span class="sxs-lookup"><span data-stu-id="7274e-174">Queue ACL/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="7274e-175"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Aan de slag met Azure Queue-Service in .NET</a></span><span class="sxs-lookup"><span data-stu-id="7274e-175"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="7274e-176">Eigenschappen van de Queue-Service</span><span class="sxs-lookup"><span data-stu-id="7274e-176">Queue Service Properties</span></span></td> 
<td><span data-ttu-id="7274e-177"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Aan de slag met Azure Queue-Service in .NET</a></span><span class="sxs-lookup"><span data-stu-id="7274e-177"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="7274e-178">Updatebericht</span><span class="sxs-lookup"><span data-stu-id="7274e-178">Update Message</span></span></td> 
<td><span data-ttu-id="7274e-179"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Aan de slag met Azure Queue-Service in .NET</a></span><span class="sxs-lookup"><span data-stu-id="7274e-179"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td rowspan="7"><span data-ttu-id="7274e-180"><b>Tabel</b></span><span class="sxs-lookup"><span data-stu-id="7274e-180"><b>Table</b></span></span></td>
<td><span data-ttu-id="7274e-181">Tabel maken</span><span class="sxs-lookup"><span data-stu-id="7274e-181">Create Table</span></span></td> 
<td><span data-ttu-id="7274e-182"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Gelijktijdigheid van taken met behulp van Azure Storage - voorbeeldtoepassing beheren</a></span><span class="sxs-lookup"><span data-stu-id="7274e-182"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="7274e-183">Entiteit/tabel verwijderen</span><span class="sxs-lookup"><span data-stu-id="7274e-183">Delete Entity/Table</span></span></td> 
<td><span data-ttu-id="7274e-184"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Aan de slag met Azure Table Storage in .NET</a></span><span class="sxs-lookup"><span data-stu-id="7274e-184"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="7274e-185">De entiteit invoegen of Merge/verplaatsen</span><span class="sxs-lookup"><span data-stu-id="7274e-185">Insert/Merge/Replace Entity</span></span></td> 
<td><span data-ttu-id="7274e-186"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Gelijktijdigheid van taken met behulp van Azure Storage - voorbeeldtoepassing beheren</a></span><span class="sxs-lookup"><span data-stu-id="7274e-186"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="7274e-187">Query-entiteiten</span><span class="sxs-lookup"><span data-stu-id="7274e-187">Query Entities</span></span></td> 
<td><span data-ttu-id="7274e-188"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Aan de slag met Azure Table Storage in .NET</a></span><span class="sxs-lookup"><span data-stu-id="7274e-188"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="7274e-189">Querytabellen</span><span class="sxs-lookup"><span data-stu-id="7274e-189">Query Tables</span></span></td> 
<td><span data-ttu-id="7274e-190"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Aan de slag met Azure Table Storage in .NET</a></span><span class="sxs-lookup"><span data-stu-id="7274e-190"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="7274e-191">ACL/eigenschappen van de tabel</span><span class="sxs-lookup"><span data-stu-id="7274e-191">Table ACL/Properties</span></span></td> 
<td><span data-ttu-id="7274e-192"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/AdvancedSamples.cs">Aan de slag met Azure Table Storage in .NET</a></span><span class="sxs-lookup"><span data-stu-id="7274e-192"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/AdvancedSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="7274e-193">Bijwerken van entiteit</span><span class="sxs-lookup"><span data-stu-id="7274e-193">Update Entity</span></span></td> 
<td><span data-ttu-id="7274e-194"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Gelijktijdigheid van taken met behulp van Azure Storage - voorbeeldtoepassing beheren</a></span><span class="sxs-lookup"><span data-stu-id="7274e-194"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a><span data-ttu-id="7274e-195">Azure-codevoorbeelden-bibliotheek</span><span class="sxs-lookup"><span data-stu-id="7274e-195">Azure Code Samples library</span></span>

<span data-ttu-id="7274e-196">Als u wilt de compleet codevoorbeeld bibliotheek bekijken, gaat u naar de [Azure codevoorbeelden](https://azure.microsoft.com/resources/samples/?service=storage) bibliotheek, waaronder voorbeelden voor Azure-opslag die u kunt downloaden en lokaal uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="7274e-196">To view the complete sample library, go to the [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=storage) library, which includes samples for Azure Storage that you can download and run locally.</span></span> <span data-ttu-id="7274e-197">De bibliotheek met voorbeeld wordt een voorbeeldcode in het ZIP-indeling.</span><span class="sxs-lookup"><span data-stu-id="7274e-197">The Code Sample Library provides sample code in .zip format.</span></span> <span data-ttu-id="7274e-198">U kunt ook bladeren en kloon de GitHub-opslagplaats voor elk voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="7274e-198">Alternatively, you can browse and clone the GitHub repository for each sample.</span></span>

[!INCLUDE [storage-dotnet-samples-include](../../../includes/storage-dotnet-samples-include.md)]

## <a name="getting-started-guides"></a><span data-ttu-id="7274e-199">Ophalen van slag-handleidingen</span><span class="sxs-lookup"><span data-stu-id="7274e-199">Getting started guides</span></span>

<span data-ttu-id="7274e-200">Bekijk de volgende handleidingen in als u op zoek bent voor instructies over het installeren en aan de slag met de clientbibliotheken van Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="7274e-200">Check out the following guides if you are looking for instructions on how to install and get started with the Azure Storage Client Libraries.</span></span>

* [<span data-ttu-id="7274e-201">Aan de slag met Azure Blob-Service in .NET</span><span class="sxs-lookup"><span data-stu-id="7274e-201">Getting Started with Azure Blob Service in .NET</span></span>](../blobs/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="7274e-202">Aan de slag met Azure Queue-Service in .NET</span><span class="sxs-lookup"><span data-stu-id="7274e-202">Getting Started with Azure Queue Service in .NET</span></span>](../storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="7274e-203">Aan de slag met Azure Table-Service in .NET</span><span class="sxs-lookup"><span data-stu-id="7274e-203">Getting Started with Azure Table Service in .NET</span></span>](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [<span data-ttu-id="7274e-204">Aan de slag met Azure File-Service in .NET</span><span class="sxs-lookup"><span data-stu-id="7274e-204">Getting Started with Azure File Service in .NET</span></span>](../storage-dotnet-how-to-use-files.md)

## <a name="next-steps"></a><span data-ttu-id="7274e-205">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7274e-205">Next steps</span></span>

<span data-ttu-id="7274e-206">Voor informatie over steekproeven voor de andere talen:</span><span class="sxs-lookup"><span data-stu-id="7274e-206">For information on samples for other languages:</span></span>

* <span data-ttu-id="7274e-207">Java: [voorbeelden van Azure Storage met Java](storage-samples-java.md)</span><span class="sxs-lookup"><span data-stu-id="7274e-207">Java: [Azure Storage samples using Java](storage-samples-java.md)</span></span>
* <span data-ttu-id="7274e-208">Alle andere talen: [Azure Storage-voorbeelden](../storage-samples.md)</span><span class="sxs-lookup"><span data-stu-id="7274e-208">All other languages: [Azure Storage samples](../storage-samples.md)</span></span>
