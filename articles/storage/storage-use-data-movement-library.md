---
title: aaaTransfer gegevens met Microsoft Azure Storage-bibliotheek voor gegevensverplaatsing Hallo | Microsoft Docs
description: "Hallo-bibliotheek voor gegevensverplaatsing toomove of een kopie van gegevens tooor van blob- en inhoud gebruiken. Kopiëren van gegevens tooAzure opslag van lokale bestanden of kopiëren van gegevens binnen of tussen opslagaccounts. Eenvoudig uw gegevens tooAzure opslag migreren."
services: storage
documentationcenter: 
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/22/2017
ms.author: seguler
ms.openlocfilehash: 5de902d132565a8eafdc672f7a1a18e1a2db3a06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-hello-microsoft-azure-storage-data-movement-library"></a><span data-ttu-id="e73a4-105">Gegevens overdragen met Hallo Microsoft Azure Storage-bibliotheek voor gegevensverplaatsing</span><span class="sxs-lookup"><span data-stu-id="e73a4-105">Transfer Data with hello Microsoft Azure Storage Data Movement Library</span></span>

## <a name="overview"></a><span data-ttu-id="e73a4-106">Overzicht</span><span class="sxs-lookup"><span data-stu-id="e73a4-106">Overview</span></span>
<span data-ttu-id="e73a4-107">Hallo Microsoft Azure Storage-bibliotheek voor gegevensverplaatsing is een open-source platformoverschrijdende-bibliotheek die is ontworpen voor hoge prestaties uploaden, downloaden en uit Azure Storage-Blobs en bestanden te kopiëren.</span><span class="sxs-lookup"><span data-stu-id="e73a4-107">hello Microsoft Azure Storage Data Movement Library is a cross-platform open source library that is designed for high performance uploading, downloading, and copying of Azure Storage Blobs and Files.</span></span> <span data-ttu-id="e73a4-108">Deze bibliotheek is Hallo data movement basisschema die ook door [AzCopy](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="e73a4-108">This library is hello core data movement framework that powers [AzCopy](storage-use-azcopy.md).</span></span> <span data-ttu-id="e73a4-109">Hallo-bibliotheek voor gegevensverplaatsing biedt handige methoden die niet beschikbaar zijn in onze traditionele [.NET Azure Storage-clientbibliotheek](storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="e73a4-109">hello Data Movement Library provides convenient methods that aren't available in our traditional [.NET Azure Storage Client Library](storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="e73a4-110">Dit omvat Hallo mogelijkheid tooset Hallo aantal parallelle bewerkingen, bijhouden overdracht voortgang, hervatten eenvoudig een geannuleerde overdracht en nog veel meer.</span><span class="sxs-lookup"><span data-stu-id="e73a4-110">This includes hello ability tooset hello number of parallel operations, track transfer progress, easily resume a canceled transfer, and much more.</span></span>  

<span data-ttu-id="e73a4-111">Deze bibliotheek gebruikt ook .NET Core, wat betekent dat u deze kunt gebruiken dat bij het bouwen van .NET-toepassingen voor Windows, Linux en Mac OS.</span><span class="sxs-lookup"><span data-stu-id="e73a4-111">This library also uses .NET Core, which means you can use it when building .NET apps for Windows, Linux and macOS.</span></span> <span data-ttu-id="e73a4-112">toolearn meer informatie over .NET Core verwijzen toohello [.NET Core documentatie](https://dotnet.github.io/).</span><span class="sxs-lookup"><span data-stu-id="e73a4-112">toolearn more about .NET Core, refer toohello [.NET Core documentation](https://dotnet.github.io/).</span></span> <span data-ttu-id="e73a4-113">Deze bibliotheek werkt ook voor traditionele .NET Framework-apps voor Windows.</span><span class="sxs-lookup"><span data-stu-id="e73a4-113">This library also works for traditional .NET Framework apps for Windows.</span></span> 

<span data-ttu-id="e73a4-114">Dit document wordt gedemonstreerd hoe toocreate een .NET Core consoletoepassing die wordt uitgevoerd op Windows, Linux en Mac OS en voert Hallo volgen scenario's:</span><span class="sxs-lookup"><span data-stu-id="e73a4-114">This document demonstrates how toocreate a .NET Core console application that that runs on Windows, Linux, and macOS and performs hello following scenarios:</span></span>

- <span data-ttu-id="e73a4-115">Het uploaden van bestanden en mappen tooBlob opslag.</span><span class="sxs-lookup"><span data-stu-id="e73a4-115">Upload files and directories tooBlob Storage.</span></span>
- <span data-ttu-id="e73a4-116">Definieer Hallo aantal parallelle bewerkingen bij de overdracht van gegevens.</span><span class="sxs-lookup"><span data-stu-id="e73a4-116">Define hello number of parallel operations when transferring data.</span></span>
- <span data-ttu-id="e73a4-117">Voortgang van het overbrengen bijhouden.</span><span class="sxs-lookup"><span data-stu-id="e73a4-117">Track data transfer progress.</span></span>
- <span data-ttu-id="e73a4-118">Overdracht van gegevens hervatten geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="e73a4-118">Resume canceled data transfer.</span></span> 
- <span data-ttu-id="e73a4-119">Bestand kopiëren van de URL tooBlob opslag.</span><span class="sxs-lookup"><span data-stu-id="e73a4-119">Copy file from URL tooBlob Storage.</span></span> 
- <span data-ttu-id="e73a4-120">Kopiëren van Blob Storage tooBlob opslag.</span><span class="sxs-lookup"><span data-stu-id="e73a4-120">Copy from Blob Storage tooBlob Storage.</span></span>

<span data-ttu-id="e73a4-121">**Wat u nodig hebt:**</span><span class="sxs-lookup"><span data-stu-id="e73a4-121">**What you need:**</span></span>

* [<span data-ttu-id="e73a4-122">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="e73a4-122">Visual Studio Code</span></span>](https://code.visualstudio.com/)
* <span data-ttu-id="e73a4-123">Een [Azure Storage-account](storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="e73a4-123">An [Azure storage account](storage-create-storage-account.md#create-a-storage-account)</span></span>

> [!NOTE]
> <span data-ttu-id="e73a4-124">Deze handleiding wordt ervan uitgegaan dat u al bekend met bent [Azure Storage](https://azure.microsoft.com/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="e73a4-124">This guide assumes that you are already familiar with [Azure Storage](https://azure.microsoft.com/services/storage/).</span></span> <span data-ttu-id="e73a4-125">Als u niet lezen Hallo [inleiding tooAzure opslag](storage-introduction.md) documentatie is het handig.</span><span class="sxs-lookup"><span data-stu-id="e73a4-125">If not, reading hello [Introduction tooAzure Storage](storage-introduction.md) documentation is helpful.</span></span> <span data-ttu-id="e73a4-126">Het belangrijkste is dat u nodig hebt te[een opslagaccount maken](storage-create-storage-account.md#create-a-storage-account) met behulp van toostart Hallo-bibliotheek voor gegevensverplaatsing.</span><span class="sxs-lookup"><span data-stu-id="e73a4-126">Most importantly, you need too[create a Storage account](storage-create-storage-account.md#create-a-storage-account) toostart using hello Data Movement Library.</span></span>
> 
> 

## <a name="setup"></a><span data-ttu-id="e73a4-127">Instellen</span><span class="sxs-lookup"><span data-stu-id="e73a4-127">Setup</span></span>  

1. <span data-ttu-id="e73a4-128">Ga naar Hallo [installatiehandleiding voor .NET Core](https://www.microsoft.com/net/core) tooinstall .NET Core.</span><span class="sxs-lookup"><span data-stu-id="e73a4-128">Visit hello [.NET Core Installation Guide](https://www.microsoft.com/net/core) tooinstall .NET Core.</span></span> <span data-ttu-id="e73a4-129">Als u uw omgeving, kies Hallo-opdrachtregeloptie.</span><span class="sxs-lookup"><span data-stu-id="e73a4-129">When selecting your environment, choose hello command-line option.</span></span> 
2. <span data-ttu-id="e73a4-130">Vanaf de opdrachtregel hello, maak een map voor uw project.</span><span class="sxs-lookup"><span data-stu-id="e73a4-130">From hello command line, create a directory for your project.</span></span> <span data-ttu-id="e73a4-131">Navigeer naar deze map staan, typ `dotnet new` toocreate een C#-consoleproject.</span><span class="sxs-lookup"><span data-stu-id="e73a4-131">Navigate into this directory, then type `dotnet new` toocreate a C# console project.</span></span>
3. <span data-ttu-id="e73a4-132">Deze map openen in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="e73a4-132">Open this directory in Visual Studio Code.</span></span> <span data-ttu-id="e73a4-133">Deze stap kan worden snel uitgevoerd via de opdrachtregel Hallo door te typen `code .`.</span><span class="sxs-lookup"><span data-stu-id="e73a4-133">This step can be quickly done via hello command line by typing `code .`.</span></span>  
4. <span data-ttu-id="e73a4-134">Hallo installeren [C#-extensie](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) van Hallo Visual Studio Code Marketplace.</span><span class="sxs-lookup"><span data-stu-id="e73a4-134">Install hello [C# extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) from hello Visual Studio Code Marketplace.</span></span> <span data-ttu-id="e73a4-135">Start Visual Studio Code opnieuw.</span><span class="sxs-lookup"><span data-stu-id="e73a4-135">Restart Visual Studio Code.</span></span> 
5. <span data-ttu-id="e73a4-136">U ziet nu twee keer worden gevraagd.</span><span class="sxs-lookup"><span data-stu-id="e73a4-136">At this point, you should see two prompts.</span></span> <span data-ttu-id="e73a4-137">Een is voor het toevoegen van 'vereist activa toobuild en foutopsporing'.</span><span class="sxs-lookup"><span data-stu-id="e73a4-137">One is for adding "required assets toobuild and debug."</span></span> <span data-ttu-id="e73a4-138">Klik op 'Ja'.</span><span class="sxs-lookup"><span data-stu-id="e73a4-138">Click "yes."</span></span> <span data-ttu-id="e73a4-139">Een andere vraag is voor het herstellen van niet-omgezette afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="e73a4-139">Another prompt is for restoring unresolved dependencies.</span></span> <span data-ttu-id="e73a4-140">Klik op 'herstellen'.</span><span class="sxs-lookup"><span data-stu-id="e73a4-140">Click "restore."</span></span>
6. <span data-ttu-id="e73a4-141">Uw toepassing moet nu bevatten een `launch.json` bestand onder Hallo `.vscode` directory.</span><span class="sxs-lookup"><span data-stu-id="e73a4-141">Your application should now contain a `launch.json` file under hello `.vscode` directory.</span></span> <span data-ttu-id="e73a4-142">In dit bestand, wijzig Hallo `externalConsole` waarde te`true`.</span><span class="sxs-lookup"><span data-stu-id="e73a4-142">In this file, change hello `externalConsole` value too`true`.</span></span>
7. <span data-ttu-id="e73a4-143">Visual Studio Code kunt u toodebug .NET Core toepassingen.</span><span class="sxs-lookup"><span data-stu-id="e73a4-143">Visual Studio Code allows you toodebug .NET Core applications.</span></span> <span data-ttu-id="e73a4-144">Klik op `F5` toorun uw toepassing en controleer of de installatie werkt.</span><span class="sxs-lookup"><span data-stu-id="e73a4-144">Hit `F5` toorun your application and verify that your setup is working.</span></span> <span data-ttu-id="e73a4-145">U ziet "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="e73a4-145">You should see "Hello World!"</span></span> <span data-ttu-id="e73a4-146">afgedrukte toohello-console.</span><span class="sxs-lookup"><span data-stu-id="e73a4-146">printed toohello console.</span></span> 

## <a name="add-data-movement-library-tooyour-project"></a><span data-ttu-id="e73a4-147">Bibliotheek voor gegevensverplaatsing tooyour project toevoegen</span><span class="sxs-lookup"><span data-stu-id="e73a4-147">Add Data Movement Library tooyour project</span></span>

1. <span data-ttu-id="e73a4-148">Toevoegen van de meest recente versie van het Hallo-bibliotheek voor gegevensverplaatsing toohello Hallo `dependencies` gedeelte van uw `project.json` bestand.</span><span class="sxs-lookup"><span data-stu-id="e73a4-148">Add hello latest version of hello Data Movement Library toohello `dependencies` section of your `project.json` file.</span></span> <span data-ttu-id="e73a4-149">Bij Hallo schrijven is deze versie`"Microsoft.Azure.Storage.DataMovement": "0.5.0"`</span><span class="sxs-lookup"><span data-stu-id="e73a4-149">At hello time of writing, this version would be `"Microsoft.Azure.Storage.DataMovement": "0.5.0"`</span></span> 
2. <span data-ttu-id="e73a4-150">Voeg `"portable-net45+win8"` toohello `imports` sectie.</span><span class="sxs-lookup"><span data-stu-id="e73a4-150">Add `"portable-net45+win8"` toohello `imports` section.</span></span> 
3. <span data-ttu-id="e73a4-151">Een prompt moet worden weergegeven toorestore uw project.</span><span class="sxs-lookup"><span data-stu-id="e73a4-151">A prompt should display toorestore your project.</span></span> <span data-ttu-id="e73a4-152">Klik op de knop 'herstellen' Hallo.</span><span class="sxs-lookup"><span data-stu-id="e73a4-152">Click hello "restore" button.</span></span> <span data-ttu-id="e73a4-153">U kunt ook uw project terugzetten vanaf de opdrachtregel Hallo door Hallo-opdracht te typen `dotnet restore` in Hallo hoofdmap van uw projectmap.</span><span class="sxs-lookup"><span data-stu-id="e73a4-153">You can also restore your project from hello command line by typing hello command `dotnet restore` in hello root of your project directory.</span></span>

<span data-ttu-id="e73a4-154">Wijzig `project.json`:</span><span class="sxs-lookup"><span data-stu-id="e73a4-154">Modify `project.json`:</span></span>

    {
      "version": "1.0.0-*",
      "buildOptions": {
        "debugType": "portable",
        "emitEntryPoint": true
      },
      "dependencies": {
        "Microsoft.Azure.Storage.DataMovement": "0.5.0"
      },
      "frameworks": {
        "netcoreapp1.1": {
          "dependencies": {
            "Microsoft.NETCore.App": {
              "type": "platform",
              "version": "1.1.0"
            }
          },
          "imports": [
            "dnxcore50",
            "portable-net45+win8"
          ]
        }
      }
    }

## <a name="set-up-hello-skeleton-of-your-application"></a><span data-ttu-id="e73a4-155">Instellen van een geraamte van uw toepassing hello</span><span class="sxs-lookup"><span data-stu-id="e73a4-155">Set up hello skeleton of your application</span></span>
<span data-ttu-id="e73a4-156">Hallo is eerste wat die we doen ingesteld Hallo 'basisproject' code van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="e73a4-156">hello first thing we do is set up hello "skeleton" code of our application.</span></span> <span data-ttu-id="e73a4-157">Deze code ons gevraagd een naam en het account opslagaccountsleutel en gebruikt deze referenties toocreate een `CloudStorageAccount` object.</span><span class="sxs-lookup"><span data-stu-id="e73a4-157">This code prompts us for a Storage account name and account key and uses those credentials toocreate a `CloudStorageAccount` object.</span></span> <span data-ttu-id="e73a4-158">Dit object is gebruikte toointeract met onze opslagaccount in alle scenario's voor overdracht.</span><span class="sxs-lookup"><span data-stu-id="e73a4-158">This object is used toointeract with our Storage account in all transfer scenarios.</span></span> <span data-ttu-id="e73a4-159">Hallo-code gevraagd ons ook toochoose Hallo type overdrachtsbewerking willen we graag tooexecute.</span><span class="sxs-lookup"><span data-stu-id="e73a4-159">hello code also prompts us toochoose hello type of transfer operation we would like tooexecute.</span></span> 

<span data-ttu-id="e73a4-160">Wijzig `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="e73a4-160">Modify `Program.cs`:</span></span>

```csharp
using System;
using System.Threading;
using System.Diagnostics;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.WindowsAzure.Storage.DataMovement;

namespace DMLibSample
{
    public class Program
    {
        public static void Main()
        {
            Console.WriteLine("Enter Storage account name:");           
            string accountName = Console.ReadLine();

            Console.WriteLine("\nEnter Storage account key:");           
            string accountKey = Console.ReadLine();

            string storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=" + accountName + ";AccountKey=" + accountKey;
            CloudStorageAccount account = CloudStorageAccount.Parse(storageConnectionString);

            ExecuteChoice(account);
        }

        public static void ExecuteChoice(CloudStorageAccount account)
        {
            Console.WriteLine("\nWhat type of transfer would you like tooexecute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
            int choice = int.Parse(Console.ReadLine());

            if(choice == 1)
            {
                TransferLocalFileToAzureBlob(account).Wait();
            }
            else if(choice == 2)
            {
                TransferLocalDirectoryToAzureBlobDirectory(account).Wait();
            }
            else if(choice == 3)
            {
                TransferUrlToAzureBlob(account).Wait();
            }
            else if(choice == 4)
            {
                TransferAzureBlobToAzureBlob(account).Wait();
            }
        }

        public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
        { 
            
        }

        public static async Task TransferLocalDirectoryToAzureBlobDirectory(CloudStorageAccount account)
        { 
            
        }

        public static async Task TransferUrlToAzureBlob(CloudStorageAccount account)
        {

        }

        public static async Task TransferAzureBlobToAzureBlob(CloudStorageAccount account)
        {

        }
    }
}
```

## <a name="transfer-local-file-tooazure-blob"></a><span data-ttu-id="e73a4-161">Overdracht lokaal bestand tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="e73a4-161">Transfer local file tooAzure Blob</span></span>
<span data-ttu-id="e73a4-162">Voeg Hallo methoden `GetSourcePath` en `GetBlob` te`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="e73a4-162">Add hello methods `GetSourcePath` and `GetBlob` too`Program.cs`:</span></span>

```csharp
public static string GetSourcePath()
{
    Console.WriteLine("\nProvide path for source:");
    string sourcePath = Console.ReadLine();

    return sourcePath;
}

public static CloudBlockBlob GetBlob(CloudStorageAccount account)
{
    CloudBlobClient blobClient = account.CreateCloudBlobClient();

    Console.WriteLine("\nProvide name of Blob container:");
    string containerName = Console.ReadLine();
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);
    container.CreateIfNotExistsAsync().Wait();

    Console.WriteLine("\nProvide name of new Blob:");
    string blobName = Console.ReadLine();
    CloudBlockBlob blob = container.GetBlockBlobReference(blobName);

    return blob;
}
```

<span data-ttu-id="e73a4-163">Hallo wijzigen `TransferLocalFileToAzureBlob` methode:</span><span class="sxs-lookup"><span data-stu-id="e73a4-163">Modify hello `TransferLocalFileToAzureBlob` method:</span></span>

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account);
    Console.WriteLine("\nTransfer started...");
    await TransferManager.UploadAsync(localFilePath, blob);
    Console.WriteLine("\nTransfer operation complete.");
    ExecuteChoice(account);
}
```

<span data-ttu-id="e73a4-164">Deze code gevraagd ons Hallo pad tooa lokaal bestand, Hallo-naam van een nieuwe of bestaande container en Hallo-naam van een nieuwe blob.</span><span class="sxs-lookup"><span data-stu-id="e73a4-164">This code prompts us for hello path tooa local file, hello name of a new or existing container, and hello name of a new blob.</span></span> <span data-ttu-id="e73a4-165">Hallo `TransferManager.UploadAsync` methode Hallo uploaden met behulp van deze informatie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e73a4-165">hello `TransferManager.UploadAsync` method performs hello upload using this information.</span></span> 

<span data-ttu-id="e73a4-166">Klik op `F5` toorun uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="e73a4-166">Hit `F5` toorun your application.</span></span> <span data-ttu-id="e73a4-167">U kunt controleren dat uploaden Hallo is opgetreden door het bekijken van uw opslagaccount Hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="e73a4-167">You can verify that hello upload occurred by viewing your Storage account with hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <a name="set-number-of-parallel-operations"></a><span data-ttu-id="e73a4-168">Aantal parallelle bewerkingen</span><span class="sxs-lookup"><span data-stu-id="e73a4-168">Set number of parallel operations</span></span>
<span data-ttu-id="e73a4-169">Een goede functie aangeboden door Hallo-bibliotheek voor gegevensverplaatsing is Hallo mogelijkheid tooset Hallo aantal parallelle bewerkingen tooincrease Hallo-gegevensdoorvoer overdracht.</span><span class="sxs-lookup"><span data-stu-id="e73a4-169">A great feature offered by hello Data Movement Library is hello ability tooset hello number of parallel operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="e73a4-170">Hallo-bibliotheek voor gegevensverplaatsing wordt standaard ingesteld van het aantal parallelle bewerkingen too8 Hallo * Hallo aantal kernen op uw computer.</span><span class="sxs-lookup"><span data-stu-id="e73a4-170">By default, hello Data Movement Library sets hello number of parallel operations too8 * hello number of cores on your machine.</span></span> 

<span data-ttu-id="e73a4-171">Houd er rekening mee dat veel parallelle bewerkingen in een omgeving met lage bandbreedte mogelijk Hallo netwerkverbinding overbelast en daadwerkelijk te voorkomen dat de bewerkingen van het volledig is voltooid.</span><span class="sxs-lookup"><span data-stu-id="e73a4-171">Keep in mind that many parallel operations in a low-bandwidth environment may overwhelm hello network connection and actually prevent operations from fully completing.</span></span> <span data-ttu-id="e73a4-172">U moet tooexperiment met deze instelling toodetermine wat werkt er beste op basis van de beschikbare netwerkbandbreedte.</span><span class="sxs-lookup"><span data-stu-id="e73a4-172">You'll need tooexperiment with this setting toodetermine what works best based on your available network bandwidth.</span></span> 

<span data-ttu-id="e73a4-173">Laten we code waarmee we tooset Hallo aantal parallelle bewerkingen toevoegen.</span><span class="sxs-lookup"><span data-stu-id="e73a4-173">Let's add some code that allows us tooset hello number of parallel operations.</span></span> <span data-ttu-id="e73a4-174">We gaan ook programmacode toevoegen die hoe lang het duurt Hallo overdracht toocomplete time-out.</span><span class="sxs-lookup"><span data-stu-id="e73a4-174">Let's also add code that times how long it takes for hello transfer toocomplete.</span></span>

<span data-ttu-id="e73a4-175">Voeg een `SetNumberOfParallelOperations` methode te`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="e73a4-175">Add a `SetNumberOfParallelOperations` method too`Program.cs`:</span></span>

```csharp
public static void SetNumberOfParallelOperations()
{
    Console.WriteLine("\nHow many parallel operations would you like toouse?");
    string parallelOperations = Console.ReadLine();
    TransferManager.Configurations.ParallelOperations = int.Parse(parallelOperations);
}
```

<span data-ttu-id="e73a4-176">Hallo wijzigen `ExecuteChoice` methode toouse `SetNumberOfParallelOperations`:</span><span class="sxs-lookup"><span data-stu-id="e73a4-176">Modify hello `ExecuteChoice` method toouse `SetNumberOfParallelOperations`:</span></span>

```csharp
public static void ExecuteChoice(CloudStorageAccount account)
{
    Console.WriteLine("\nWhat type of transfer would you like tooexecute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
    int choice = int.Parse(Console.ReadLine());

    SetNumberOfParallelOperations();

    if(choice == 1)
    {
        TransferLocalFileToAzureBlob(account).Wait();
    }
    else if(choice == 2)
    {
        TransferLocalDirectoryToAzureBlobDirectory(account).Wait();
    }
    else if(choice == 3)
    {
        TransferUrlToAzureBlob(account).Wait();
    }
    else if(choice == 4)
    {
        TransferAzureBlobToAzureBlob(account).Wait();
    }
}
```

<span data-ttu-id="e73a4-177">Hallo wijzigen `TransferLocalFileToAzureBlob` methode toouse een timer:</span><span class="sxs-lookup"><span data-stu-id="e73a4-177">Modify hello `TransferLocalFileToAzureBlob` method toouse a timer:</span></span>

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account);
    Console.WriteLine("\nTransfer started...");
    Stopwatch stopWatch = Stopwatch.StartNew();
    await TransferManager.UploadAsync(localFilePath, blob);
    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

## <a name="track-transfer-progress"></a><span data-ttu-id="e73a4-178">Voortgang van de overdracht bijhouden</span><span class="sxs-lookup"><span data-stu-id="e73a4-178">Track transfer progress</span></span>
<span data-ttu-id="e73a4-179">Weten hoe lang geduurd voor onze gegevens tootransfer is uitstekend.</span><span class="sxs-lookup"><span data-stu-id="e73a4-179">Knowing how long it took for our data tootransfer is great.</span></span> <span data-ttu-id="e73a4-180">Wordt echter kunnen toosee Hallo voortgang van onze overdracht *tijdens* Hallo overdrachtsbewerking nog beter zou zijn.</span><span class="sxs-lookup"><span data-stu-id="e73a4-180">However, being able toosee hello progress of our transfer *during* hello transfer operation would be even better.</span></span> <span data-ttu-id="e73a4-181">tooachieve dit scenario moeten we toocreate een `TransferContext` object.</span><span class="sxs-lookup"><span data-stu-id="e73a4-181">tooachieve this scenario, we need toocreate a `TransferContext` object.</span></span> <span data-ttu-id="e73a4-182">Hallo `TransferContext` object kent twee vormen: `SingleTransferContext` en `DirectoryTransferContext`.</span><span class="sxs-lookup"><span data-stu-id="e73a4-182">hello `TransferContext` object comes in two forms: `SingleTransferContext` and `DirectoryTransferContext`.</span></span> <span data-ttu-id="e73a4-183">Hallo voormalige is voor de overdracht van één bestand (dit is wat we geven nu) en Hallo laatstgenoemde is voor de overdracht van een map met bestanden (die we later toevoegen).</span><span class="sxs-lookup"><span data-stu-id="e73a4-183">hello former is for transferring a single file (which is what we're doing now) and hello latter is for transferring a directory of files (which we are adding later).</span></span>

<span data-ttu-id="e73a4-184">Voeg Hallo methoden `GetSingleTransferContext` en `GetDirectoryTransferContext` te`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="e73a4-184">Add hello methods `GetSingleTransferContext` and `GetDirectoryTransferContext` too`Program.cs`:</span></span> 

```csharp
public static SingleTransferContext GetSingleTransferContext(TransferCheckpoint checkpoint)
{
    SingleTransferContext context = new SingleTransferContext(checkpoint);

    context.ProgressHandler = new Progress<TransferStatus>((progress) =>
    {
        Console.Write("\rBytes transferred: {0}", progress.BytesTransferred );
    });
    
    return context;
}

public static DirectoryTransferContext GetDirectoryTransferContext(TransferCheckpoint checkpoint)
{
    DirectoryTransferContext context = new DirectoryTransferContext(checkpoint);

    context.ProgressHandler = new Progress<TransferStatus>((progress) =>
    {
        Console.Write("\rBytes transferred: {0}", progress.BytesTransferred );
    });
    
    return context;
}
```

<span data-ttu-id="e73a4-185">Hallo wijzigen `TransferLocalFileToAzureBlob` methode toouse `GetSingleTransferContext`:</span><span class="sxs-lookup"><span data-stu-id="e73a4-185">Modify hello `TransferLocalFileToAzureBlob` method toouse `GetSingleTransferContext`:</span></span>

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account);
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint);
    Console.WriteLine("\nTransfer started...\n");
    Stopwatch stopWatch = Stopwatch.StartNew();
    await TransferManager.UploadAsync(localFilePath, blob, null, context);
    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

## <a name="resume-a-canceled-transfer"></a><span data-ttu-id="e73a4-186">Een geannuleerde overdracht hervat</span><span class="sxs-lookup"><span data-stu-id="e73a4-186">Resume a canceled transfer</span></span>
<span data-ttu-id="e73a4-187">Een andere handige functie aangeboden door Hallo-bibliotheek voor gegevensverplaatsing is Hallo mogelijkheid tooresume een geannuleerde overdracht.</span><span class="sxs-lookup"><span data-stu-id="e73a4-187">Another convenient feature offered by hello Data Movement Library is hello ability tooresume a canceled transfer.</span></span> <span data-ttu-id="e73a4-188">Laten we code waarmee we tootemporarily annuleren Hallo overdracht door te typen toevoegen `c`, en vervolgens 3 seconden later hervatten Hallo overdracht.</span><span class="sxs-lookup"><span data-stu-id="e73a4-188">Let's add some code that allows us tootemporarily cancel hello transfer by typing `c`, and then resume hello transfer 3 seconds later.</span></span>

<span data-ttu-id="e73a4-189">Wijzig `TransferLocalFileToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="e73a4-189">Modify `TransferLocalFileToAzureBlob`:</span></span>

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    try
    {
        task = TransferManager.UploadAsync(localFilePath, blob, null, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetSingleTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.UploadAsync(localFilePath, blob, null, context);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

<span data-ttu-id="e73a4-190">Tot nu toe onze `checkpoint` waarde is altijd ingesteld te`null`.</span><span class="sxs-lookup"><span data-stu-id="e73a4-190">Up until now, our `checkpoint` value has always been set too`null`.</span></span> <span data-ttu-id="e73a4-191">Nu als we Hallo overbrengen annuleren, we Hallo laatste controlepunt van onze overdracht ophalen en deze nieuw controlepunt in de context van onze overdracht gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e73a4-191">Now, if we cancel hello transfer, we retrieve hello last checkpoint of our transfer, then use this new checkpoint in our transfer context.</span></span> 

## <a name="transfer-local-directory-tooazure-blob-directory"></a><span data-ttu-id="e73a4-192">Lokale directory tooAzure Blob directory overdragen</span><span class="sxs-lookup"><span data-stu-id="e73a4-192">Transfer local directory tooAzure Blob directory</span></span>
<span data-ttu-id="e73a4-193">Het normaal zou zijn geplaatst als het Hallo-bibliotheek voor gegevensverplaatsing kan slechts één bestandsoverdracht tegelijk.</span><span class="sxs-lookup"><span data-stu-id="e73a4-193">It would be disappointing if hello Data Movement Library could only transfer one file at a time.</span></span> <span data-ttu-id="e73a4-194">Dit is gelukkig niet Hallo geval.</span><span class="sxs-lookup"><span data-stu-id="e73a4-194">Luckily, this is not hello case.</span></span> <span data-ttu-id="e73a4-195">Hallo-bibliotheek voor gegevensverplaatsing biedt Hallo mogelijkheid tootransfer een lijst van bestanden en alle submappen.</span><span class="sxs-lookup"><span data-stu-id="e73a4-195">hello Data Movement Library provides hello ability tootransfer a directory of files and all of its subdirectories.</span></span> <span data-ttu-id="e73a4-196">Laten we code toevoegen waarmee we toodo geregeld.</span><span class="sxs-lookup"><span data-stu-id="e73a4-196">Let's add some code that allows us toodo just that.</span></span>

<span data-ttu-id="e73a4-197">Voeg eerst de methode Hallo `GetBlobDirectory` te`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="e73a4-197">First, add hello method `GetBlobDirectory` too`Program.cs`:</span></span>

```csharp
public static CloudBlobDirectory GetBlobDirectory(CloudStorageAccount account)
{
    CloudBlobClient blobClient = account.CreateCloudBlobClient();

    Console.WriteLine("\nProvide name of Blob container. This can be a new or existing Blob container:");
    string containerName = Console.ReadLine();
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);
    container.CreateIfNotExistsAsync().Wait();

    CloudBlobDirectory blobDirectory = container.GetDirectoryReference("");

    return blobDirectory;
}
```

<span data-ttu-id="e73a4-198">Wijzig `TransferLocalDirectoryToAzureBlobDirectory`:</span><span class="sxs-lookup"><span data-stu-id="e73a4-198">Then, modify `TransferLocalDirectoryToAzureBlobDirectory`:</span></span>

```csharp
public static async Task TransferLocalDirectoryToAzureBlobDirectory(CloudStorageAccount account)
{ 
    string localDirectoryPath = GetSourcePath();
    CloudBlobDirectory blobDirectory = GetBlobDirectory(account); 
    TransferCheckpoint checkpoint = null;
    DirectoryTransferContext context = GetDirectoryTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    UploadDirectoryOptions options = new UploadDirectoryOptions()
    {
        Recursive = true
    };

    try
    {
        task = TransferManager.UploadDirectoryAsync(localDirectoryPath, blobDirectory, options, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetDirectoryTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.UploadDirectoryAsync(localDirectoryPath, blobDirectory, options, context);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

<span data-ttu-id="e73a4-199">Er zijn een aantal verschillen tussen deze methode en het Hallo-methode voor het uploaden van één bestand.</span><span class="sxs-lookup"><span data-stu-id="e73a4-199">There are a few differences between this method and hello method for uploading a single file.</span></span> <span data-ttu-id="e73a4-200">We maken nu gebruik `TransferManager.UploadDirectoryAsync` en Hallo `getDirectoryTransferContext` methode we eerder hebben gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e73a4-200">We're now using `TransferManager.UploadDirectoryAsync` and hello `getDirectoryTransferContext` method we created earlier.</span></span> <span data-ttu-id="e73a4-201">Bovendien we bieden nu een `options` tooour uploadbewerking, waardoor we tooindicate dat we tooinclude submappen in de upload willen-waarde.</span><span class="sxs-lookup"><span data-stu-id="e73a4-201">In addition, we now provide an `options` value tooour upload operation, which allows us tooindicate that we want tooinclude subdirectories in our upload.</span></span> 

## <a name="copy-file-from-url-tooazure-blob"></a><span data-ttu-id="e73a4-202">Bestand kopiëren vanuit URL tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="e73a4-202">Copy file from URL tooAzure Blob</span></span>
<span data-ttu-id="e73a4-203">Nu gaan we code waarmee we een bestand van een URL tooan Azure Blob toocopy toevoegen.</span><span class="sxs-lookup"><span data-stu-id="e73a4-203">Now, let's add code that allows us toocopy a file from a URL tooan Azure Blob.</span></span> 

<span data-ttu-id="e73a4-204">Wijzig `TransferUrlToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="e73a4-204">Modify `TransferUrlToAzureBlob`:</span></span>

```csharp
public static async Task TransferUrlToAzureBlob(CloudStorageAccount account)
{
    Uri uri = new Uri(GetSourcePath());
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    try
    {
        task = TransferManager.CopyAsync(uri, blob, true, null, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetSingleTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.CopyAsync(uri, blob, true, null, context, cancellationSource.Token);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

<span data-ttu-id="e73a4-205">Een belangrijk gebruiksvoorbeeld voor deze functie is wanneer u gegevens uit een andere cloud-service (bijvoorbeeld AWS) tooAzure toomove nodig.</span><span class="sxs-lookup"><span data-stu-id="e73a4-205">One important use case for this feature is when you need toomove data from another cloud service (e.g. AWS) tooAzure.</span></span> <span data-ttu-id="e73a4-206">Als u een URL waarmee hebt u toegang tot toohello bron, kunt u eenvoudig die resource in Azure Blobs verplaatsen met behulp van Hallo `TransferManager.CopyAsync` methode.</span><span class="sxs-lookup"><span data-stu-id="e73a4-206">As long as you have a URL that gives you access toohello resource, you can easily move that resource into Azure Blobs by using hello `TransferManager.CopyAsync` method.</span></span> <span data-ttu-id="e73a4-207">Deze methode wordt ook introduceert een nieuwe Boole-parameter.</span><span class="sxs-lookup"><span data-stu-id="e73a4-207">This method also introduces a new boolean parameter.</span></span> <span data-ttu-id="e73a4-208">Als deze parameter te`true` geeft aan dat er een asynchrone serverzijde toodo kopiëren.</span><span class="sxs-lookup"><span data-stu-id="e73a4-208">Setting this parameter too`true` indicates that we want toodo an asynchronous server-side copy.</span></span> <span data-ttu-id="e73a4-209">Als deze parameter te`false` geeft een synchrone kopie - betekenis Hallo-bron is de lokale computer gedownloade tooour eerst tooAzure Blob vervolgens geüpload.</span><span class="sxs-lookup"><span data-stu-id="e73a4-209">Setting this parameter too`false` indicates a synchronous copy - meaning hello resource is downloaded tooour local machine first, then uploaded tooAzure Blob.</span></span> <span data-ttu-id="e73a4-210">Synchrone kopie is echter momenteel alleen beschikbaar voor het kopiëren van een Azure Storage resource tooanother.</span><span class="sxs-lookup"><span data-stu-id="e73a4-210">However, synchronous copy is currently only available for copying from one Azure Storage resource tooanother.</span></span> 

## <a name="transfer-azure-blob-tooazure-blob"></a><span data-ttu-id="e73a4-211">Azure Blob-tooAzure Blob overdragen</span><span class="sxs-lookup"><span data-stu-id="e73a4-211">Transfer Azure Blob tooAzure Blob</span></span>
<span data-ttu-id="e73a4-212">Een andere functie die een unieke wordt geleverd door het Hallo-bibliotheek voor gegevensverplaatsing is Hallo mogelijkheid toocopy van een Azure Storage resource tooanother.</span><span class="sxs-lookup"><span data-stu-id="e73a4-212">Another feature that's uniquely provided by hello Data Movement Library is hello ability toocopy from one Azure Storage resource tooanother.</span></span> 

<span data-ttu-id="e73a4-213">Wijzig `TransferAzureBlobToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="e73a4-213">Modify `TransferAzureBlobToAzureBlob`:</span></span>

```csharp
public static async Task TransferAzureBlobToAzureBlob(CloudStorageAccount account)
{
    CloudBlockBlob sourceBlob = GetBlob(account);
    CloudBlockBlob destinationBlob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    try
    {
        task = TransferManager.CopyAsync(sourceBlob, destinationBlob, true, null, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetSingleTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.CopyAsync(sourceBlob, destinationBlob, false, null, context, cancellationSource.Token);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

<span data-ttu-id="e73a4-214">In dit voorbeeld ingesteld we Hallo Boole-parameter in `TransferManager.CopyAsync` te`false` tooindicate willen we toodo een synchrone kopie.</span><span class="sxs-lookup"><span data-stu-id="e73a4-214">In this example, we set hello boolean parameter in `TransferManager.CopyAsync` too`false` tooindicate that we want toodo a synchronous copy.</span></span> <span data-ttu-id="e73a4-215">Dit betekent dat Hallo resource eerst de lokale computer gedownloade tooour is en tooAzure Blob geüpload.</span><span class="sxs-lookup"><span data-stu-id="e73a4-215">This means that hello resource is downloaded tooour local machine first, then uploaded tooAzure Blob.</span></span> <span data-ttu-id="e73a4-216">Hallo synchrone kopie-optie is een uitstekende manier tooensure dat uw kopieerbewerking een consistente snelheid heeft.</span><span class="sxs-lookup"><span data-stu-id="e73a4-216">hello synchronous copy option is a great way tooensure that your copy operation has a consistent speed.</span></span> <span data-ttu-id="e73a4-217">Daarentegen is Hallo snelheid van de kopie van een asynchrone serverzijde afhankelijk van de beschikbare netwerkbandbreedte Hallo op Hallo-server kan variëren.</span><span class="sxs-lookup"><span data-stu-id="e73a4-217">In contrast, hello speed of an asynchronous server-side copy is dependent on hello available network bandwidth on hello server, which can fluctuate.</span></span> <span data-ttu-id="e73a4-218">Synchrone kopie mogelijk echter extra uitgaande kosten vergeleken tooasynchronous kopie genereren.</span><span class="sxs-lookup"><span data-stu-id="e73a4-218">However, synchronous copy may generate additional egress cost compared tooasynchronous copy.</span></span> <span data-ttu-id="e73a4-219">Hallo aanbevolen aanpak is toouse synchrone kopie in een virtuele machine van Azure in Hallo dezelfde regio bevinden als uw gegevensbron account tooavoid uitgaande opslagkosten.</span><span class="sxs-lookup"><span data-stu-id="e73a4-219">hello recommended approach is toouse synchronous copy in an Azure VM that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="conclusion"></a><span data-ttu-id="e73a4-220">Conclusie</span><span class="sxs-lookup"><span data-stu-id="e73a4-220">Conclusion</span></span>
<span data-ttu-id="e73a4-221">Onze toepassing van de verplaatsing van gegevens is voltooid.</span><span class="sxs-lookup"><span data-stu-id="e73a4-221">Our data movement application is now complete.</span></span> <span data-ttu-id="e73a4-222">[Voorbeeld van de volledige code Hallo is beschikbaar op GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app).</span><span class="sxs-lookup"><span data-stu-id="e73a4-222">[hello full code sample is available on GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e73a4-223">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e73a4-223">Next steps</span></span>
<span data-ttu-id="e73a4-224">In deze aan de slag, is er een toepassing die communiceert met Azure Storage en wordt uitgevoerd op Windows, Linux en Mac OS gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e73a4-224">In this getting started, we created an application that interacts with Azure Storage and runs on Windows, Linux, and macOS.</span></span> <span data-ttu-id="e73a4-225">Deze aan de slag gericht op het Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="e73a4-225">This getting started focused on Blob Storage.</span></span> <span data-ttu-id="e73a4-226">Deze dezelfde kennis kan echter toegepaste tooFile opslag zijn.</span><span class="sxs-lookup"><span data-stu-id="e73a4-226">However, this same knowledge can be applied tooFile Storage.</span></span> <span data-ttu-id="e73a4-227">toolearn meer, Bekijk [Azure Storage-bibliotheek voor gegevensverplaatsing naslagdocumentatie](https://azure.github.io/azure-storage-net-data-movement).</span><span class="sxs-lookup"><span data-stu-id="e73a4-227">toolearn more, check out [Azure Storage Data Movement Library reference documentation](https://azure.github.io/azure-storage-net-data-movement).</span></span>

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]




