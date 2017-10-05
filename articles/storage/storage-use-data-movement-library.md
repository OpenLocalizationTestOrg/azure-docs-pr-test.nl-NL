---
title: Gegevensoverdracht met het Microsoft Azure Storage-bibliotheek voor gegevensverplaatsing | Microsoft Docs
description: "Gebruik de bibliotheek voor gegevensverplaatsing verplaatsen of kopiëren van gegevens of naar blob- en -inhoud. Gegevens van lokale bestanden kopiëren naar Azure Storage of kopiëren van gegevens binnen of tussen opslagaccounts. Uw gegevens eenvoudig migreren naar Azure Storage."
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
ms.openlocfilehash: 2ba94e4dd931b6d385101c7dadccfa3583b5296e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="transfer-data-with-the-microsoft-azure-storage-data-movement-library"></a><span data-ttu-id="f31eb-105">Gegevensoverdracht met het Microsoft Azure Storage-bibliotheek voor gegevensverplaatsing</span><span class="sxs-lookup"><span data-stu-id="f31eb-105">Transfer Data with the Microsoft Azure Storage Data Movement Library</span></span>

## <a name="overview"></a><span data-ttu-id="f31eb-106">Overzicht</span><span class="sxs-lookup"><span data-stu-id="f31eb-106">Overview</span></span>
<span data-ttu-id="f31eb-107">De Microsoft Azure Storage-bibliotheek voor gegevensverplaatsing is een open-source platformoverschrijdende-bibliotheek die is ontworpen voor hoge prestaties uploaden, downloaden en uit Azure Storage-Blobs en bestanden te kopiëren.</span><span class="sxs-lookup"><span data-stu-id="f31eb-107">The Microsoft Azure Storage Data Movement Library is a cross-platform open source library that is designed for high performance uploading, downloading, and copying of Azure Storage Blobs and Files.</span></span> <span data-ttu-id="f31eb-108">Deze bibliotheek is core data movement framework die ook door [AzCopy](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="f31eb-108">This library is the core data movement framework that powers [AzCopy](storage-use-azcopy.md).</span></span> <span data-ttu-id="f31eb-109">De bibliotheek voor gegevensverplaatsing biedt handige methoden die niet beschikbaar zijn in onze traditionele [.NET Azure Storage-clientbibliotheek](storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="f31eb-109">The Data Movement Library provides convenient methods that aren't available in our traditional [.NET Azure Storage Client Library](storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="f31eb-110">Dit biedt de mogelijkheid om het aantal parallelle bewerkingen instellen, overdracht voortgang volgen, hervat eenvoudig een geannuleerde overdracht en nog veel meer.</span><span class="sxs-lookup"><span data-stu-id="f31eb-110">This includes the ability to set the number of parallel operations, track transfer progress, easily resume a canceled transfer, and much more.</span></span>  

<span data-ttu-id="f31eb-111">Deze bibliotheek gebruikt ook .NET Core, wat betekent dat u deze kunt gebruiken dat bij het bouwen van .NET-toepassingen voor Windows, Linux en Mac OS.</span><span class="sxs-lookup"><span data-stu-id="f31eb-111">This library also uses .NET Core, which means you can use it when building .NET apps for Windows, Linux and macOS.</span></span> <span data-ttu-id="f31eb-112">Raadpleeg voor meer informatie over .NET Core, de [.NET Core documentatie](https://dotnet.github.io/).</span><span class="sxs-lookup"><span data-stu-id="f31eb-112">To learn more about .NET Core, refer to the [.NET Core documentation](https://dotnet.github.io/).</span></span> <span data-ttu-id="f31eb-113">Deze bibliotheek werkt ook voor traditionele .NET Framework-apps voor Windows.</span><span class="sxs-lookup"><span data-stu-id="f31eb-113">This library also works for traditional .NET Framework apps for Windows.</span></span> 

<span data-ttu-id="f31eb-114">Dit document laat zien hoe u een .NET Core-consoletoepassing maken die die wordt uitgevoerd op Windows, Linux en Mac OS en voert de volgende scenario's:</span><span class="sxs-lookup"><span data-stu-id="f31eb-114">This document demonstrates how to create a .NET Core console application that that runs on Windows, Linux, and macOS and performs the following scenarios:</span></span>

- <span data-ttu-id="f31eb-115">Het van uploadbestanden en mappen naar Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="f31eb-115">Upload files and directories to Blob Storage.</span></span>
- <span data-ttu-id="f31eb-116">Definieer het aantal parallelle bewerkingen bij de overdracht van gegevens.</span><span class="sxs-lookup"><span data-stu-id="f31eb-116">Define the number of parallel operations when transferring data.</span></span>
- <span data-ttu-id="f31eb-117">Voortgang van het overbrengen bijhouden.</span><span class="sxs-lookup"><span data-stu-id="f31eb-117">Track data transfer progress.</span></span>
- <span data-ttu-id="f31eb-118">Overdracht van gegevens hervatten geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="f31eb-118">Resume canceled data transfer.</span></span> 
- <span data-ttu-id="f31eb-119">Bestand kopiëren van de URL naar Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="f31eb-119">Copy file from URL to Blob Storage.</span></span> 
- <span data-ttu-id="f31eb-120">Kopiëren van Blob-opslag naar Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="f31eb-120">Copy from Blob Storage to Blob Storage.</span></span>

<span data-ttu-id="f31eb-121">**Wat u nodig hebt:**</span><span class="sxs-lookup"><span data-stu-id="f31eb-121">**What you need:**</span></span>

* [<span data-ttu-id="f31eb-122">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="f31eb-122">Visual Studio Code</span></span>](https://code.visualstudio.com/)
* <span data-ttu-id="f31eb-123">Een [Azure Storage-account](storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="f31eb-123">An [Azure storage account](storage-create-storage-account.md#create-a-storage-account)</span></span>

> [!NOTE]
> <span data-ttu-id="f31eb-124">Deze handleiding wordt ervan uitgegaan dat u al bekend met bent [Azure Storage](https://azure.microsoft.com/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="f31eb-124">This guide assumes that you are already familiar with [Azure Storage](https://azure.microsoft.com/services/storage/).</span></span> <span data-ttu-id="f31eb-125">Als u niet lezen van de [Inleiding tot Azure Storage](storage-introduction.md) documentatie is het handig.</span><span class="sxs-lookup"><span data-stu-id="f31eb-125">If not, reading the [Introduction to Azure Storage](storage-introduction.md) documentation is helpful.</span></span> <span data-ttu-id="f31eb-126">Het belangrijkste is, moet u [een opslagaccount maken](storage-create-storage-account.md#create-a-storage-account) aan de slag met de bibliotheek voor gegevensverplaatsing.</span><span class="sxs-lookup"><span data-stu-id="f31eb-126">Most importantly, you need to [create a Storage account](storage-create-storage-account.md#create-a-storage-account) to start using the Data Movement Library.</span></span>
> 
> 

## <a name="setup"></a><span data-ttu-id="f31eb-127">Instellen</span><span class="sxs-lookup"><span data-stu-id="f31eb-127">Setup</span></span>  

1. <span data-ttu-id="f31eb-128">Ga naar de [installatiehandleiding voor .NET Core](https://www.microsoft.com/net/core) .NET Core installeren.</span><span class="sxs-lookup"><span data-stu-id="f31eb-128">Visit the [.NET Core Installation Guide](https://www.microsoft.com/net/core) to install .NET Core.</span></span> <span data-ttu-id="f31eb-129">Als u uw omgeving, kiest u de opdrachtregeloptie.</span><span class="sxs-lookup"><span data-stu-id="f31eb-129">When selecting your environment, choose the command-line option.</span></span> 
2. <span data-ttu-id="f31eb-130">Maak een map voor uw project vanaf de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="f31eb-130">From the command line, create a directory for your project.</span></span> <span data-ttu-id="f31eb-131">Navigeer naar deze map staan, typ `dotnet new` een C#-console-project maken.</span><span class="sxs-lookup"><span data-stu-id="f31eb-131">Navigate into this directory, then type `dotnet new` to create a C# console project.</span></span>
3. <span data-ttu-id="f31eb-132">Deze map openen in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="f31eb-132">Open this directory in Visual Studio Code.</span></span> <span data-ttu-id="f31eb-133">Deze stap kan worden snel gedaan via de opdrachtregel te typen `code .`.</span><span class="sxs-lookup"><span data-stu-id="f31eb-133">This step can be quickly done via the command line by typing `code .`.</span></span>  
4. <span data-ttu-id="f31eb-134">Installeer de [C#-extensie](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) vanuit Visual Studio Code Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f31eb-134">Install the [C# extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) from the Visual Studio Code Marketplace.</span></span> <span data-ttu-id="f31eb-135">Start Visual Studio Code opnieuw.</span><span class="sxs-lookup"><span data-stu-id="f31eb-135">Restart Visual Studio Code.</span></span> 
5. <span data-ttu-id="f31eb-136">U ziet nu twee keer worden gevraagd.</span><span class="sxs-lookup"><span data-stu-id="f31eb-136">At this point, you should see two prompts.</span></span> <span data-ttu-id="f31eb-137">Een is voor het toevoegen van 'vereist activa voor het bouwen en debug'.</span><span class="sxs-lookup"><span data-stu-id="f31eb-137">One is for adding "required assets to build and debug."</span></span> <span data-ttu-id="f31eb-138">Klik op 'Ja'.</span><span class="sxs-lookup"><span data-stu-id="f31eb-138">Click "yes."</span></span> <span data-ttu-id="f31eb-139">Een andere vraag is voor het herstellen van niet-omgezette afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="f31eb-139">Another prompt is for restoring unresolved dependencies.</span></span> <span data-ttu-id="f31eb-140">Klik op 'herstellen'.</span><span class="sxs-lookup"><span data-stu-id="f31eb-140">Click "restore."</span></span>
6. <span data-ttu-id="f31eb-141">Uw toepassing moet nu bevatten een `launch.json` bestand onder de `.vscode` directory.</span><span class="sxs-lookup"><span data-stu-id="f31eb-141">Your application should now contain a `launch.json` file under the `.vscode` directory.</span></span> <span data-ttu-id="f31eb-142">In dit bestand, wijzig de `externalConsole` van waarde naar `true`.</span><span class="sxs-lookup"><span data-stu-id="f31eb-142">In this file, change the `externalConsole` value to `true`.</span></span>
7. <span data-ttu-id="f31eb-143">Visual Studio Code kunt u foutopsporing .NET Core-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="f31eb-143">Visual Studio Code allows you to debug .NET Core applications.</span></span> <span data-ttu-id="f31eb-144">Klik op `F5` voor het uitvoeren van uw toepassing en controleren of uw instellingen werkt.</span><span class="sxs-lookup"><span data-stu-id="f31eb-144">Hit `F5` to run your application and verify that your setup is working.</span></span> <span data-ttu-id="f31eb-145">U ziet "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="f31eb-145">You should see "Hello World!"</span></span> <span data-ttu-id="f31eb-146">aan de console afgedrukt.</span><span class="sxs-lookup"><span data-stu-id="f31eb-146">printed to the console.</span></span> 

## <a name="add-data-movement-library-to-your-project"></a><span data-ttu-id="f31eb-147">Bibliotheek voor gegevensverplaatsing toevoegen aan uw project</span><span class="sxs-lookup"><span data-stu-id="f31eb-147">Add Data Movement Library to your project</span></span>

1. <span data-ttu-id="f31eb-148">Toevoegen van de nieuwste versie van de bibliotheek voor gegevensverplaatsing voor de `dependencies` gedeelte van uw `project.json` bestand.</span><span class="sxs-lookup"><span data-stu-id="f31eb-148">Add the latest version of the Data Movement Library to the `dependencies` section of your `project.json` file.</span></span> <span data-ttu-id="f31eb-149">Op het moment van schrijven is deze versie`"Microsoft.Azure.Storage.DataMovement": "0.5.0"`</span><span class="sxs-lookup"><span data-stu-id="f31eb-149">At the time of writing, this version would be `"Microsoft.Azure.Storage.DataMovement": "0.5.0"`</span></span> 
2. <span data-ttu-id="f31eb-150">Voeg `"portable-net45+win8"` naar de `imports` sectie.</span><span class="sxs-lookup"><span data-stu-id="f31eb-150">Add `"portable-net45+win8"` to the `imports` section.</span></span> 
3. <span data-ttu-id="f31eb-151">Een prompt moet worden weergegeven voor het herstellen van uw project.</span><span class="sxs-lookup"><span data-stu-id="f31eb-151">A prompt should display to restore your project.</span></span> <span data-ttu-id="f31eb-152">Klik op de knop 'restore'.</span><span class="sxs-lookup"><span data-stu-id="f31eb-152">Click the "restore" button.</span></span> <span data-ttu-id="f31eb-153">U kunt ook uw project terugzetten vanaf de opdrachtregel typt u de opdracht `dotnet restore` in de hoofdmap van uw projectmap.</span><span class="sxs-lookup"><span data-stu-id="f31eb-153">You can also restore your project from the command line by typing the command `dotnet restore` in the root of your project directory.</span></span>

<span data-ttu-id="f31eb-154">Wijzig `project.json`:</span><span class="sxs-lookup"><span data-stu-id="f31eb-154">Modify `project.json`:</span></span>

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

## <a name="set-up-the-skeleton-of-your-application"></a><span data-ttu-id="f31eb-155">De basis van uw toepassing instellen</span><span class="sxs-lookup"><span data-stu-id="f31eb-155">Set up the skeleton of your application</span></span>
<span data-ttu-id="f31eb-156">Het eerste wat dat we doen is de code 'basisproject' van de toepassing ingesteld.</span><span class="sxs-lookup"><span data-stu-id="f31eb-156">The first thing we do is set up the "skeleton" code of our application.</span></span> <span data-ttu-id="f31eb-157">Deze code ons gevraagd een naam en het account opslagaccountsleutel en deze referenties gebruikt voor het maken een `CloudStorageAccount` object.</span><span class="sxs-lookup"><span data-stu-id="f31eb-157">This code prompts us for a Storage account name and account key and uses those credentials to create a `CloudStorageAccount` object.</span></span> <span data-ttu-id="f31eb-158">Dit object wordt gebruikt om te communiceren met de Storage-account in alle scenario's voor overdracht.</span><span class="sxs-lookup"><span data-stu-id="f31eb-158">This object is used to interact with our Storage account in all transfer scenarios.</span></span> <span data-ttu-id="f31eb-159">De code wordt ook gevraagd ons Kies het type overdrachtsbewerking willen we uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f31eb-159">The code also prompts us to choose the type of transfer operation we would like to execute.</span></span> 

<span data-ttu-id="f31eb-160">Wijzig `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="f31eb-160">Modify `Program.cs`:</span></span>

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
            Console.WriteLine("\nWhat type of transfer would you like to execute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
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

## <a name="transfer-local-file-to-azure-blob"></a><span data-ttu-id="f31eb-161">Lokale bestand overdragen naar Azure-Blob</span><span class="sxs-lookup"><span data-stu-id="f31eb-161">Transfer local file to Azure Blob</span></span>
<span data-ttu-id="f31eb-162">Voeg de methoden `GetSourcePath` en `GetBlob` naar `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="f31eb-162">Add the methods `GetSourcePath` and `GetBlob` to `Program.cs`:</span></span>

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

<span data-ttu-id="f31eb-163">Wijzig de `TransferLocalFileToAzureBlob` methode:</span><span class="sxs-lookup"><span data-stu-id="f31eb-163">Modify the `TransferLocalFileToAzureBlob` method:</span></span>

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

<span data-ttu-id="f31eb-164">Deze code wordt ons gevraagd om het pad naar een lokaal bestand, de naam van een nieuwe of bestaande container en de naam van een nieuwe blob.</span><span class="sxs-lookup"><span data-stu-id="f31eb-164">This code prompts us for the path to a local file, the name of a new or existing container, and the name of a new blob.</span></span> <span data-ttu-id="f31eb-165">De `TransferManager.UploadAsync` methode voert u het gebruik van deze informatie uploaden.</span><span class="sxs-lookup"><span data-stu-id="f31eb-165">The `TransferManager.UploadAsync` method performs the upload using this information.</span></span> 

<span data-ttu-id="f31eb-166">Raak `F5` uw toepassing uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="f31eb-166">Hit `F5` to run your application.</span></span> <span data-ttu-id="f31eb-167">U kunt controleren dat de upload is opgetreden door het bekijken van uw opslagaccount met de [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="f31eb-167">You can verify that the upload occurred by viewing your Storage account with the [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <a name="set-number-of-parallel-operations"></a><span data-ttu-id="f31eb-168">Aantal parallelle bewerkingen</span><span class="sxs-lookup"><span data-stu-id="f31eb-168">Set number of parallel operations</span></span>
<span data-ttu-id="f31eb-169">Een goede functie aangeboden door de bibliotheek voor gegevensverplaatsing is de mogelijkheid het aantal parallelle bewerkingen te verhogen van de overdracht gegevensdoorvoer instellen.</span><span class="sxs-lookup"><span data-stu-id="f31eb-169">A great feature offered by the Data Movement Library is the ability to set the number of parallel operations to increase the data transfer throughput.</span></span> <span data-ttu-id="f31eb-170">De bibliotheek voor gegevensverplaatsing wordt standaard het aantal parallelle bewerkingen zijn ingesteld op 8 * het aantal kernen op uw computer.</span><span class="sxs-lookup"><span data-stu-id="f31eb-170">By default, the Data Movement Library sets the number of parallel operations to 8 * the number of cores on your machine.</span></span> 

<span data-ttu-id="f31eb-171">Houd er rekening mee dat veel parallelle bewerkingen in een omgeving met lage bandbreedte mogelijk de netwerkverbinding overbelast en daadwerkelijk te voorkomen dat de bewerkingen van het volledig is voltooid.</span><span class="sxs-lookup"><span data-stu-id="f31eb-171">Keep in mind that many parallel operations in a low-bandwidth environment may overwhelm the network connection and actually prevent operations from fully completing.</span></span> <span data-ttu-id="f31eb-172">U wilt experimenteren met deze instelling om te bepalen wat het beste op basis werkt op de beschikbare netwerkbandbreedte.</span><span class="sxs-lookup"><span data-stu-id="f31eb-172">You'll need to experiment with this setting to determine what works best based on your available network bandwidth.</span></span> 

<span data-ttu-id="f31eb-173">Laten we code waarmee we het aantal parallelle bewerkingen instellen toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f31eb-173">Let's add some code that allows us to set the number of parallel operations.</span></span> <span data-ttu-id="f31eb-174">We gaan ook programmacode toevoegen die hoe lang het duurt voor de overdracht time-out te voltooien.</span><span class="sxs-lookup"><span data-stu-id="f31eb-174">Let's also add code that times how long it takes for the transfer to complete.</span></span>

<span data-ttu-id="f31eb-175">Voeg een `SetNumberOfParallelOperations` methode `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="f31eb-175">Add a `SetNumberOfParallelOperations` method to `Program.cs`:</span></span>

```csharp
public static void SetNumberOfParallelOperations()
{
    Console.WriteLine("\nHow many parallel operations would you like to use?");
    string parallelOperations = Console.ReadLine();
    TransferManager.Configurations.ParallelOperations = int.Parse(parallelOperations);
}
```

<span data-ttu-id="f31eb-176">Wijzig de `ExecuteChoice` te gebruiken methode `SetNumberOfParallelOperations`:</span><span class="sxs-lookup"><span data-stu-id="f31eb-176">Modify the `ExecuteChoice` method to use `SetNumberOfParallelOperations`:</span></span>

```csharp
public static void ExecuteChoice(CloudStorageAccount account)
{
    Console.WriteLine("\nWhat type of transfer would you like to execute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
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

<span data-ttu-id="f31eb-177">Wijzig de `TransferLocalFileToAzureBlob` methode een timer gebruiken:</span><span class="sxs-lookup"><span data-stu-id="f31eb-177">Modify the `TransferLocalFileToAzureBlob` method to use a timer:</span></span>

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

## <a name="track-transfer-progress"></a><span data-ttu-id="f31eb-178">Voortgang van de overdracht bijhouden</span><span class="sxs-lookup"><span data-stu-id="f31eb-178">Track transfer progress</span></span>
<span data-ttu-id="f31eb-179">Weten hoe lang geduurd voor onze gegevens om over te dragen is uitstekend.</span><span class="sxs-lookup"><span data-stu-id="f31eb-179">Knowing how long it took for our data to transfer is great.</span></span> <span data-ttu-id="f31eb-180">Echter, wordt de voortgang van onze overdracht zien *tijdens* de overdrachtsbewerking nog beter zou zijn.</span><span class="sxs-lookup"><span data-stu-id="f31eb-180">However, being able to see the progress of our transfer *during* the transfer operation would be even better.</span></span> <span data-ttu-id="f31eb-181">Voor dit scenario, moeten we maken een `TransferContext` object.</span><span class="sxs-lookup"><span data-stu-id="f31eb-181">To achieve this scenario, we need to create a `TransferContext` object.</span></span> <span data-ttu-id="f31eb-182">De `TransferContext` object kent twee vormen: `SingleTransferContext` en `DirectoryTransferContext`.</span><span class="sxs-lookup"><span data-stu-id="f31eb-182">The `TransferContext` object comes in two forms: `SingleTransferContext` and `DirectoryTransferContext`.</span></span> <span data-ttu-id="f31eb-183">De voormalige is voor de overdracht van één bestand (dit is wat we geven nu) en de laatste is voor de overdracht van een map met bestanden (die we later toevoegen).</span><span class="sxs-lookup"><span data-stu-id="f31eb-183">The former is for transferring a single file (which is what we're doing now) and the latter is for transferring a directory of files (which we are adding later).</span></span>

<span data-ttu-id="f31eb-184">Voeg de methoden `GetSingleTransferContext` en `GetDirectoryTransferContext` naar `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="f31eb-184">Add the methods `GetSingleTransferContext` and `GetDirectoryTransferContext` to `Program.cs`:</span></span> 

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

<span data-ttu-id="f31eb-185">Wijzig de `TransferLocalFileToAzureBlob` te gebruiken methode `GetSingleTransferContext`:</span><span class="sxs-lookup"><span data-stu-id="f31eb-185">Modify the `TransferLocalFileToAzureBlob` method to use `GetSingleTransferContext`:</span></span>

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

## <a name="resume-a-canceled-transfer"></a><span data-ttu-id="f31eb-186">Een geannuleerde overdracht hervat</span><span class="sxs-lookup"><span data-stu-id="f31eb-186">Resume a canceled transfer</span></span>
<span data-ttu-id="f31eb-187">Een andere handige functie aangeboden door de bibliotheek voor gegevensverplaatsing is de mogelijkheid een geannuleerde overdracht hervatten.</span><span class="sxs-lookup"><span data-stu-id="f31eb-187">Another convenient feature offered by the Data Movement Library is the ability to resume a canceled transfer.</span></span> <span data-ttu-id="f31eb-188">Laten we de code die kan worden uitgevoerd op de overdracht tijdelijk annuleren door op te geven toevoegen `c`, en vervolgens de overdracht 3 seconden later hervatten.</span><span class="sxs-lookup"><span data-stu-id="f31eb-188">Let's add some code that allows us to temporarily cancel the transfer by typing `c`, and then resume the transfer 3 seconds later.</span></span>

<span data-ttu-id="f31eb-189">Wijzig `TransferLocalFileToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="f31eb-189">Modify `TransferLocalFileToAzureBlob`:</span></span>

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

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

<span data-ttu-id="f31eb-190">Tot nu toe onze `checkpoint` waarde is altijd ingesteld op `null`.</span><span class="sxs-lookup"><span data-stu-id="f31eb-190">Up until now, our `checkpoint` value has always been set to `null`.</span></span> <span data-ttu-id="f31eb-191">Nu als we de overdracht annuleert, we het laatste controlepunt van onze overdracht ophalen en dit nieuwe controlepunt in de context van onze overdracht gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f31eb-191">Now, if we cancel the transfer, we retrieve the last checkpoint of our transfer, then use this new checkpoint in our transfer context.</span></span> 

## <a name="transfer-local-directory-to-azure-blob-directory"></a><span data-ttu-id="f31eb-192">Lokale directory overdragen naar Azure Blob-directory</span><span class="sxs-lookup"><span data-stu-id="f31eb-192">Transfer local directory to Azure Blob directory</span></span>
<span data-ttu-id="f31eb-193">Het normaal zou zijn geplaatst als de bibliotheek voor gegevensverplaatsing slechts één tegelijk bestandsoverdracht kan.</span><span class="sxs-lookup"><span data-stu-id="f31eb-193">It would be disappointing if the Data Movement Library could only transfer one file at a time.</span></span> <span data-ttu-id="f31eb-194">Gelukkig is dit niet het geval.</span><span class="sxs-lookup"><span data-stu-id="f31eb-194">Luckily, this is not the case.</span></span> <span data-ttu-id="f31eb-195">De bibliotheek voor gegevensverplaatsing biedt de mogelijkheid om over te dragen van een map met bestanden en alle submappen.</span><span class="sxs-lookup"><span data-stu-id="f31eb-195">The Data Movement Library provides the ability to transfer a directory of files and all of its subdirectories.</span></span> <span data-ttu-id="f31eb-196">Laten we code waarmee we dit wordt geregeld toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f31eb-196">Let's add some code that allows us to do just that.</span></span>

<span data-ttu-id="f31eb-197">Voeg eerst de methode `GetBlobDirectory` naar `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="f31eb-197">First, add the method `GetBlobDirectory` to `Program.cs`:</span></span>

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

<span data-ttu-id="f31eb-198">Wijzig `TransferLocalDirectoryToAzureBlobDirectory`:</span><span class="sxs-lookup"><span data-stu-id="f31eb-198">Then, modify `TransferLocalDirectoryToAzureBlobDirectory`:</span></span>

```csharp
public static async Task TransferLocalDirectoryToAzureBlobDirectory(CloudStorageAccount account)
{ 
    string localDirectoryPath = GetSourcePath();
    CloudBlobDirectory blobDirectory = GetBlobDirectory(account); 
    TransferCheckpoint checkpoint = null;
    DirectoryTransferContext context = GetDirectoryTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

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

<span data-ttu-id="f31eb-199">Er zijn een aantal verschillen tussen deze methode en de methode voor het uploaden van één bestand.</span><span class="sxs-lookup"><span data-stu-id="f31eb-199">There are a few differences between this method and the method for uploading a single file.</span></span> <span data-ttu-id="f31eb-200">We maken nu gebruik `TransferManager.UploadDirectoryAsync` en de `getDirectoryTransferContext` methode we eerder hebben gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f31eb-200">We're now using `TransferManager.UploadDirectoryAsync` and the `getDirectoryTransferContext` method we created earlier.</span></span> <span data-ttu-id="f31eb-201">Bovendien we bieden nu een `options` waarde aan onze uploadbewerking, waardoor we om aan te geven dat we willen submappen opnemen in de upload.</span><span class="sxs-lookup"><span data-stu-id="f31eb-201">In addition, we now provide an `options` value to our upload operation, which allows us to indicate that we want to include subdirectories in our upload.</span></span> 

## <a name="copy-file-from-url-to-azure-blob"></a><span data-ttu-id="f31eb-202">Bestand kopiëren vanuit de URL naar Azure-Blob</span><span class="sxs-lookup"><span data-stu-id="f31eb-202">Copy file from URL to Azure Blob</span></span>
<span data-ttu-id="f31eb-203">Nu gaan we code toevoegen die kan worden uitgevoerd op een bestand kopiëren vanuit een URL naar een Azure-Blob.</span><span class="sxs-lookup"><span data-stu-id="f31eb-203">Now, let's add code that allows us to copy a file from a URL to an Azure Blob.</span></span> 

<span data-ttu-id="f31eb-204">Wijzig `TransferUrlToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="f31eb-204">Modify `TransferUrlToAzureBlob`:</span></span>

```csharp
public static async Task TransferUrlToAzureBlob(CloudStorageAccount account)
{
    Uri uri = new Uri(GetSourcePath());
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

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

<span data-ttu-id="f31eb-205">Een belangrijk gebruiksvoorbeeld voor deze functie is als u nodig hebt om gegevens te verplaatsen van een andere cloudservice (bijvoorbeeld AWS) naar Azure.</span><span class="sxs-lookup"><span data-stu-id="f31eb-205">One important use case for this feature is when you need to move data from another cloud service (e.g. AWS) to Azure.</span></span> <span data-ttu-id="f31eb-206">Als u een URL die u toegang tot de resource biedt hebt, kunt u eenvoudig verplaatsen die resource in Azure Blobs met behulp van de `TransferManager.CopyAsync` methode.</span><span class="sxs-lookup"><span data-stu-id="f31eb-206">As long as you have a URL that gives you access to the resource, you can easily move that resource into Azure Blobs by using the `TransferManager.CopyAsync` method.</span></span> <span data-ttu-id="f31eb-207">Deze methode wordt ook introduceert een nieuwe Boole-parameter.</span><span class="sxs-lookup"><span data-stu-id="f31eb-207">This method also introduces a new boolean parameter.</span></span> <span data-ttu-id="f31eb-208">Als deze parameter `true` geeft aan dat er een asynchrone serverzijde kopiëren wilt maken.</span><span class="sxs-lookup"><span data-stu-id="f31eb-208">Setting this parameter to `true` indicates that we want to do an asynchronous server-side copy.</span></span> <span data-ttu-id="f31eb-209">Als deze parameter `false` synchrone kopiëren - wat betekent dat de resource eerst gedownload naar de lokale computer, wordt geüpload naar Azure-Blob.</span><span class="sxs-lookup"><span data-stu-id="f31eb-209">Setting this parameter to `false` indicates a synchronous copy - meaning the resource is downloaded to our local machine first, then uploaded to Azure Blob.</span></span> <span data-ttu-id="f31eb-210">Synchrone kopie is echter momenteel alleen beschikbaar voor het kopiëren van een Azure Storage-resource naar een andere.</span><span class="sxs-lookup"><span data-stu-id="f31eb-210">However, synchronous copy is currently only available for copying from one Azure Storage resource to another.</span></span> 

## <a name="transfer-azure-blob-to-azure-blob"></a><span data-ttu-id="f31eb-211">Azure Blob overdragen naar Azure Blob</span><span class="sxs-lookup"><span data-stu-id="f31eb-211">Transfer Azure Blob to Azure Blob</span></span>
<span data-ttu-id="f31eb-212">Een andere functie die uniek opgegeven door de bibliotheek voor gegevensverplaatsing is de mogelijkheid om te kopiëren van de ene Azure Storage resource naar een andere.</span><span class="sxs-lookup"><span data-stu-id="f31eb-212">Another feature that's uniquely provided by the Data Movement Library is the ability to copy from one Azure Storage resource to another.</span></span> 

<span data-ttu-id="f31eb-213">Wijzig `TransferAzureBlobToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="f31eb-213">Modify `TransferAzureBlobToAzureBlob`:</span></span>

```csharp
public static async Task TransferAzureBlobToAzureBlob(CloudStorageAccount account)
{
    CloudBlockBlob sourceBlob = GetBlob(account);
    CloudBlockBlob destinationBlob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

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

<span data-ttu-id="f31eb-214">In dit voorbeeld wordt de Booleaanse parameter ingesteld in `TransferManager.CopyAsync` naar `false` om aan te geven dat we willen een synchrone kopiëren.</span><span class="sxs-lookup"><span data-stu-id="f31eb-214">In this example, we set the boolean parameter in `TransferManager.CopyAsync` to `false` to indicate that we want to do a synchronous copy.</span></span> <span data-ttu-id="f31eb-215">Dit betekent dat de resource is eerst gedownload naar de lokale computer vervolgens geüpload naar Azure-Blob.</span><span class="sxs-lookup"><span data-stu-id="f31eb-215">This means that the resource is downloaded to our local machine first, then uploaded to Azure Blob.</span></span> <span data-ttu-id="f31eb-216">De optie synchrone kopie is een uitstekende manier om ervoor te zorgen dat uw kopieerbewerking een consistente snelheid.</span><span class="sxs-lookup"><span data-stu-id="f31eb-216">The synchronous copy option is a great way to ensure that your copy operation has a consistent speed.</span></span> <span data-ttu-id="f31eb-217">Daarentegen is is de snelheid van een asynchrone serverzijde kopie afhankelijk van de beschikbare netwerkbandbreedte op de server, kan variëren.</span><span class="sxs-lookup"><span data-stu-id="f31eb-217">In contrast, the speed of an asynchronous server-side copy is dependent on the available network bandwidth on the server, which can fluctuate.</span></span> <span data-ttu-id="f31eb-218">Synchrone kopie mogelijk echter extra uitgaande kosten vergeleken met de asynchrone kopie genereren.</span><span class="sxs-lookup"><span data-stu-id="f31eb-218">However, synchronous copy may generate additional egress cost compared to asynchronous copy.</span></span> <span data-ttu-id="f31eb-219">De aanbevolen aanpak is het synchrone exemplaar gebruiken op een virtuele machine van Azure die zich in dezelfde regio bevinden als uw storage-account van de bron om te voorkomen dat de kosten voor uitgaande gegevens.</span><span class="sxs-lookup"><span data-stu-id="f31eb-219">The recommended approach is to use synchronous copy in an Azure VM that is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="conclusion"></a><span data-ttu-id="f31eb-220">Conclusie</span><span class="sxs-lookup"><span data-stu-id="f31eb-220">Conclusion</span></span>
<span data-ttu-id="f31eb-221">Onze toepassing van de verplaatsing van gegevens is voltooid.</span><span class="sxs-lookup"><span data-stu-id="f31eb-221">Our data movement application is now complete.</span></span> <span data-ttu-id="f31eb-222">[Het volledige voorbeeld is beschikbaar op GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app).</span><span class="sxs-lookup"><span data-stu-id="f31eb-222">[The full code sample is available on GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f31eb-223">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f31eb-223">Next steps</span></span>
<span data-ttu-id="f31eb-224">In deze aan de slag, is er een toepassing die communiceert met Azure Storage en wordt uitgevoerd op Windows, Linux en Mac OS gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f31eb-224">In this getting started, we created an application that interacts with Azure Storage and runs on Windows, Linux, and macOS.</span></span> <span data-ttu-id="f31eb-225">Deze aan de slag gericht op het Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="f31eb-225">This getting started focused on Blob Storage.</span></span> <span data-ttu-id="f31eb-226">Deze dezelfde kennis kan echter worden toegepast op File Storage.</span><span class="sxs-lookup"><span data-stu-id="f31eb-226">However, this same knowledge can be applied to File Storage.</span></span> <span data-ttu-id="f31eb-227">Bekijk voor meer informatie, [Azure Storage-bibliotheek voor gegevensverplaatsing naslagdocumentatie](https://azure.github.io/azure-storage-net-data-movement).</span><span class="sxs-lookup"><span data-stu-id="f31eb-227">To learn more, check out [Azure Storage Data Movement Library reference documentation](https://azure.github.io/azure-storage-net-data-movement).</span></span>

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]




