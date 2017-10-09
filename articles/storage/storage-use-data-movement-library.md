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
# <a name="transfer-data-with-hello-microsoft-azure-storage-data-movement-library"></a>Gegevens overdragen met Hallo Microsoft Azure Storage-bibliotheek voor gegevensverplaatsing

## <a name="overview"></a>Overzicht
Hallo Microsoft Azure Storage-bibliotheek voor gegevensverplaatsing is een open-source platformoverschrijdende-bibliotheek die is ontworpen voor hoge prestaties uploaden, downloaden en uit Azure Storage-Blobs en bestanden te kopiëren. Deze bibliotheek is Hallo data movement basisschema die ook door [AzCopy](storage-use-azcopy.md). Hallo-bibliotheek voor gegevensverplaatsing biedt handige methoden die niet beschikbaar zijn in onze traditionele [.NET Azure Storage-clientbibliotheek](storage-dotnet-how-to-use-blobs.md). Dit omvat Hallo mogelijkheid tooset Hallo aantal parallelle bewerkingen, bijhouden overdracht voortgang, hervatten eenvoudig een geannuleerde overdracht en nog veel meer.  

Deze bibliotheek gebruikt ook .NET Core, wat betekent dat u deze kunt gebruiken dat bij het bouwen van .NET-toepassingen voor Windows, Linux en Mac OS. toolearn meer informatie over .NET Core verwijzen toohello [.NET Core documentatie](https://dotnet.github.io/). Deze bibliotheek werkt ook voor traditionele .NET Framework-apps voor Windows. 

Dit document wordt gedemonstreerd hoe toocreate een .NET Core consoletoepassing die wordt uitgevoerd op Windows, Linux en Mac OS en voert Hallo volgen scenario's:

- Het uploaden van bestanden en mappen tooBlob opslag.
- Definieer Hallo aantal parallelle bewerkingen bij de overdracht van gegevens.
- Voortgang van het overbrengen bijhouden.
- Overdracht van gegevens hervatten geannuleerd. 
- Bestand kopiëren van de URL tooBlob opslag. 
- Kopiëren van Blob Storage tooBlob opslag.

**Wat u nodig hebt:**

* [Visual Studio Code](https://code.visualstudio.com/)
* Een [Azure Storage-account](storage-create-storage-account.md#create-a-storage-account)

> [!NOTE]
> Deze handleiding wordt ervan uitgegaan dat u al bekend met bent [Azure Storage](https://azure.microsoft.com/services/storage/). Als u niet lezen Hallo [inleiding tooAzure opslag](storage-introduction.md) documentatie is het handig. Het belangrijkste is dat u nodig hebt te[een opslagaccount maken](storage-create-storage-account.md#create-a-storage-account) met behulp van toostart Hallo-bibliotheek voor gegevensverplaatsing.
> 
> 

## <a name="setup"></a>Instellen  

1. Ga naar Hallo [installatiehandleiding voor .NET Core](https://www.microsoft.com/net/core) tooinstall .NET Core. Als u uw omgeving, kies Hallo-opdrachtregeloptie. 
2. Vanaf de opdrachtregel hello, maak een map voor uw project. Navigeer naar deze map staan, typ `dotnet new` toocreate een C#-consoleproject.
3. Deze map openen in Visual Studio Code. Deze stap kan worden snel uitgevoerd via de opdrachtregel Hallo door te typen `code .`.  
4. Hallo installeren [C#-extensie](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) van Hallo Visual Studio Code Marketplace. Start Visual Studio Code opnieuw. 
5. U ziet nu twee keer worden gevraagd. Een is voor het toevoegen van 'vereist activa toobuild en foutopsporing'. Klik op 'Ja'. Een andere vraag is voor het herstellen van niet-omgezette afhankelijkheden. Klik op 'herstellen'.
6. Uw toepassing moet nu bevatten een `launch.json` bestand onder Hallo `.vscode` directory. In dit bestand, wijzig Hallo `externalConsole` waarde te`true`.
7. Visual Studio Code kunt u toodebug .NET Core toepassingen. Klik op `F5` toorun uw toepassing en controleer of de installatie werkt. U ziet "Hello World!" afgedrukte toohello-console. 

## <a name="add-data-movement-library-tooyour-project"></a>Bibliotheek voor gegevensverplaatsing tooyour project toevoegen

1. Toevoegen van de meest recente versie van het Hallo-bibliotheek voor gegevensverplaatsing toohello Hallo `dependencies` gedeelte van uw `project.json` bestand. Bij Hallo schrijven is deze versie`"Microsoft.Azure.Storage.DataMovement": "0.5.0"` 
2. Voeg `"portable-net45+win8"` toohello `imports` sectie. 
3. Een prompt moet worden weergegeven toorestore uw project. Klik op de knop 'herstellen' Hallo. U kunt ook uw project terugzetten vanaf de opdrachtregel Hallo door Hallo-opdracht te typen `dotnet restore` in Hallo hoofdmap van uw projectmap.

Wijzig `project.json`:

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

## <a name="set-up-hello-skeleton-of-your-application"></a>Instellen van een geraamte van uw toepassing hello
Hallo is eerste wat die we doen ingesteld Hallo 'basisproject' code van de toepassing. Deze code ons gevraagd een naam en het account opslagaccountsleutel en gebruikt deze referenties toocreate een `CloudStorageAccount` object. Dit object is gebruikte toointeract met onze opslagaccount in alle scenario's voor overdracht. Hallo-code gevraagd ons ook toochoose Hallo type overdrachtsbewerking willen we graag tooexecute. 

Wijzig `Program.cs`:

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

## <a name="transfer-local-file-tooazure-blob"></a>Overdracht lokaal bestand tooAzure Blob
Voeg Hallo methoden `GetSourcePath` en `GetBlob` te`Program.cs`:

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

Hallo wijzigen `TransferLocalFileToAzureBlob` methode:

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

Deze code gevraagd ons Hallo pad tooa lokaal bestand, Hallo-naam van een nieuwe of bestaande container en Hallo-naam van een nieuwe blob. Hallo `TransferManager.UploadAsync` methode Hallo uploaden met behulp van deze informatie wordt uitgevoerd. 

Klik op `F5` toorun uw toepassing. U kunt controleren dat uploaden Hallo is opgetreden door het bekijken van uw opslagaccount Hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).

## <a name="set-number-of-parallel-operations"></a>Aantal parallelle bewerkingen
Een goede functie aangeboden door Hallo-bibliotheek voor gegevensverplaatsing is Hallo mogelijkheid tooset Hallo aantal parallelle bewerkingen tooincrease Hallo-gegevensdoorvoer overdracht. Hallo-bibliotheek voor gegevensverplaatsing wordt standaard ingesteld van het aantal parallelle bewerkingen too8 Hallo * Hallo aantal kernen op uw computer. 

Houd er rekening mee dat veel parallelle bewerkingen in een omgeving met lage bandbreedte mogelijk Hallo netwerkverbinding overbelast en daadwerkelijk te voorkomen dat de bewerkingen van het volledig is voltooid. U moet tooexperiment met deze instelling toodetermine wat werkt er beste op basis van de beschikbare netwerkbandbreedte. 

Laten we code waarmee we tooset Hallo aantal parallelle bewerkingen toevoegen. We gaan ook programmacode toevoegen die hoe lang het duurt Hallo overdracht toocomplete time-out.

Voeg een `SetNumberOfParallelOperations` methode te`Program.cs`:

```csharp
public static void SetNumberOfParallelOperations()
{
    Console.WriteLine("\nHow many parallel operations would you like toouse?");
    string parallelOperations = Console.ReadLine();
    TransferManager.Configurations.ParallelOperations = int.Parse(parallelOperations);
}
```

Hallo wijzigen `ExecuteChoice` methode toouse `SetNumberOfParallelOperations`:

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

Hallo wijzigen `TransferLocalFileToAzureBlob` methode toouse een timer:

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

## <a name="track-transfer-progress"></a>Voortgang van de overdracht bijhouden
Weten hoe lang geduurd voor onze gegevens tootransfer is uitstekend. Wordt echter kunnen toosee Hallo voortgang van onze overdracht *tijdens* Hallo overdrachtsbewerking nog beter zou zijn. tooachieve dit scenario moeten we toocreate een `TransferContext` object. Hallo `TransferContext` object kent twee vormen: `SingleTransferContext` en `DirectoryTransferContext`. Hallo voormalige is voor de overdracht van één bestand (dit is wat we geven nu) en Hallo laatstgenoemde is voor de overdracht van een map met bestanden (die we later toevoegen).

Voeg Hallo methoden `GetSingleTransferContext` en `GetDirectoryTransferContext` te`Program.cs`: 

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

Hallo wijzigen `TransferLocalFileToAzureBlob` methode toouse `GetSingleTransferContext`:

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

## <a name="resume-a-canceled-transfer"></a>Een geannuleerde overdracht hervat
Een andere handige functie aangeboden door Hallo-bibliotheek voor gegevensverplaatsing is Hallo mogelijkheid tooresume een geannuleerde overdracht. Laten we code waarmee we tootemporarily annuleren Hallo overdracht door te typen toevoegen `c`, en vervolgens 3 seconden later hervatten Hallo overdracht.

Wijzig `TransferLocalFileToAzureBlob`:

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

Tot nu toe onze `checkpoint` waarde is altijd ingesteld te`null`. Nu als we Hallo overbrengen annuleren, we Hallo laatste controlepunt van onze overdracht ophalen en deze nieuw controlepunt in de context van onze overdracht gebruiken. 

## <a name="transfer-local-directory-tooazure-blob-directory"></a>Lokale directory tooAzure Blob directory overdragen
Het normaal zou zijn geplaatst als het Hallo-bibliotheek voor gegevensverplaatsing kan slechts één bestandsoverdracht tegelijk. Dit is gelukkig niet Hallo geval. Hallo-bibliotheek voor gegevensverplaatsing biedt Hallo mogelijkheid tootransfer een lijst van bestanden en alle submappen. Laten we code toevoegen waarmee we toodo geregeld.

Voeg eerst de methode Hallo `GetBlobDirectory` te`Program.cs`:

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

Wijzig `TransferLocalDirectoryToAzureBlobDirectory`:

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

Er zijn een aantal verschillen tussen deze methode en het Hallo-methode voor het uploaden van één bestand. We maken nu gebruik `TransferManager.UploadDirectoryAsync` en Hallo `getDirectoryTransferContext` methode we eerder hebben gemaakt. Bovendien we bieden nu een `options` tooour uploadbewerking, waardoor we tooindicate dat we tooinclude submappen in de upload willen-waarde. 

## <a name="copy-file-from-url-tooazure-blob"></a>Bestand kopiëren vanuit URL tooAzure Blob
Nu gaan we code waarmee we een bestand van een URL tooan Azure Blob toocopy toevoegen. 

Wijzig `TransferUrlToAzureBlob`:

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

Een belangrijk gebruiksvoorbeeld voor deze functie is wanneer u gegevens uit een andere cloud-service (bijvoorbeeld AWS) tooAzure toomove nodig. Als u een URL waarmee hebt u toegang tot toohello bron, kunt u eenvoudig die resource in Azure Blobs verplaatsen met behulp van Hallo `TransferManager.CopyAsync` methode. Deze methode wordt ook introduceert een nieuwe Boole-parameter. Als deze parameter te`true` geeft aan dat er een asynchrone serverzijde toodo kopiëren. Als deze parameter te`false` geeft een synchrone kopie - betekenis Hallo-bron is de lokale computer gedownloade tooour eerst tooAzure Blob vervolgens geüpload. Synchrone kopie is echter momenteel alleen beschikbaar voor het kopiëren van een Azure Storage resource tooanother. 

## <a name="transfer-azure-blob-tooazure-blob"></a>Azure Blob-tooAzure Blob overdragen
Een andere functie die een unieke wordt geleverd door het Hallo-bibliotheek voor gegevensverplaatsing is Hallo mogelijkheid toocopy van een Azure Storage resource tooanother. 

Wijzig `TransferAzureBlobToAzureBlob`:

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

In dit voorbeeld ingesteld we Hallo Boole-parameter in `TransferManager.CopyAsync` te`false` tooindicate willen we toodo een synchrone kopie. Dit betekent dat Hallo resource eerst de lokale computer gedownloade tooour is en tooAzure Blob geüpload. Hallo synchrone kopie-optie is een uitstekende manier tooensure dat uw kopieerbewerking een consistente snelheid heeft. Daarentegen is Hallo snelheid van de kopie van een asynchrone serverzijde afhankelijk van de beschikbare netwerkbandbreedte Hallo op Hallo-server kan variëren. Synchrone kopie mogelijk echter extra uitgaande kosten vergeleken tooasynchronous kopie genereren. Hallo aanbevolen aanpak is toouse synchrone kopie in een virtuele machine van Azure in Hallo dezelfde regio bevinden als uw gegevensbron account tooavoid uitgaande opslagkosten.

## <a name="conclusion"></a>Conclusie
Onze toepassing van de verplaatsing van gegevens is voltooid. [Voorbeeld van de volledige code Hallo is beschikbaar op GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app). 

## <a name="next-steps"></a>Volgende stappen
In deze aan de slag, is er een toepassing die communiceert met Azure Storage en wordt uitgevoerd op Windows, Linux en Mac OS gemaakt. Deze aan de slag gericht op het Blob-opslag. Deze dezelfde kennis kan echter toegepaste tooFile opslag zijn. toolearn meer, Bekijk [Azure Storage-bibliotheek voor gegevensverplaatsing naslagdocumentatie](https://azure.github.io/azure-storage-net-data-movement).

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]




