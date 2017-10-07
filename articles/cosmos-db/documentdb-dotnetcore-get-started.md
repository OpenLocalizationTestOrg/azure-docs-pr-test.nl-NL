---
title: 'Azure Cosmos DB: aan de slag met de DocumentDB-API met .NET Core | Microsoft Docs'
description: Een zelfstudie waarmee u maakt een online database en C#-consoletoepassing hello Azure Cosmos DB DocumentDB API .NET Core SDK gebruiken.
services: cosmos-db
documentationcenter: .net
author: arramac
manager: jhubbard
editor: 
ms.assetid: 9f93e276-9936-4efb-a534-a9889fa7c7d2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: 5e7efb327252e9e73e9b2a340820eeecc6937fa5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-getting-started-with-hello-documentdb-api-and-net-core"></a><span data-ttu-id="7864d-103">Azure Cosmos DB: Aan de slag met Hallo DocumentDB API en .NET Core</span><span class="sxs-lookup"><span data-stu-id="7864d-103">Azure Cosmos DB: Getting started with hello DocumentDB API and .NET Core</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7864d-104">.NET</span><span class="sxs-lookup"><span data-stu-id="7864d-104">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="7864d-105">.NET Core</span><span class="sxs-lookup"><span data-stu-id="7864d-105">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="7864d-106">Node.js voor MongoDB</span><span class="sxs-lookup"><span data-stu-id="7864d-106">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="7864d-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="7864d-107">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="7864d-108">Java</span><span class="sxs-lookup"><span data-stu-id="7864d-108">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="7864d-109">C++</span><span class="sxs-lookup"><span data-stu-id="7864d-109">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="7864d-110">Welkom toohello DocumentDB-API voor Azure Cosmos DB aan de slag met .NET Core zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="7864d-110">Welcome toohello DocumentDB API for Azure Cosmos DB getting started with .NET Core tutorial!</span></span> <span data-ttu-id="7864d-111">Wanneer u deze zelfstudie hebt voltooid, beschikt u over een consoletoepassing waarmee u Azure Cosmos DB-resources kunt maken en er query's op kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="7864d-111">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="7864d-112">De volgende onderwerpen komen aan bod:</span><span class="sxs-lookup"><span data-stu-id="7864d-112">We'll cover:</span></span>

* <span data-ttu-id="7864d-113">Maken en te verbinden tooan Azure DB die Cosmos-account</span><span class="sxs-lookup"><span data-stu-id="7864d-113">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="7864d-114">Uw Visual Studio-oplossing configureren</span><span class="sxs-lookup"><span data-stu-id="7864d-114">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="7864d-115">Een online-database maken</span><span class="sxs-lookup"><span data-stu-id="7864d-115">Creating an online database</span></span>
* <span data-ttu-id="7864d-116">Een verzameling maken</span><span class="sxs-lookup"><span data-stu-id="7864d-116">Creating a collection</span></span>
* <span data-ttu-id="7864d-117">JSON-documenten maken</span><span class="sxs-lookup"><span data-stu-id="7864d-117">Creating JSON documents</span></span>
* <span data-ttu-id="7864d-118">Hallo verzameling opvragen</span><span class="sxs-lookup"><span data-stu-id="7864d-118">Querying hello collection</span></span>
* <span data-ttu-id="7864d-119">Een document vervangen</span><span class="sxs-lookup"><span data-stu-id="7864d-119">Replacing a document</span></span>
* <span data-ttu-id="7864d-120">Een document verwijderen</span><span class="sxs-lookup"><span data-stu-id="7864d-120">Deleting a document</span></span>
* <span data-ttu-id="7864d-121">Hallo-database verwijderen</span><span class="sxs-lookup"><span data-stu-id="7864d-121">Deleting hello database</span></span>

<span data-ttu-id="7864d-122">Hebt u geen tijd?</span><span class="sxs-lookup"><span data-stu-id="7864d-122">Don't have time?</span></span> <span data-ttu-id="7864d-123">Geen probleem.</span><span class="sxs-lookup"><span data-stu-id="7864d-123">Don't worry!</span></span> <span data-ttu-id="7864d-124">Hallo volledige oplossing is beschikbaar op [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span><span class="sxs-lookup"><span data-stu-id="7864d-124">hello complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span></span> <span data-ttu-id="7864d-125">Springen toohello [Hallo volledige oplossing sectie ophalen](#GetSolution) voor beknopte instructies.</span><span class="sxs-lookup"><span data-stu-id="7864d-125">Jump toohello [Get hello complete solution section](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="7864d-126">Wilt u toobuild een Xamarin iOS, Android of formulieren met behulp van toepassing hello DocumentDB API en .NET Core SDK?</span><span class="sxs-lookup"><span data-stu-id="7864d-126">Want toobuild a Xamarin iOS, Android, or Forms application using hello DocumentDB API and .NET Core SDK?</span></span> <span data-ttu-id="7864d-127">Zie [ontwikkelen van mobiele toepassingen met Xamarin en Azure Cosmos DB](mobile-apps-with-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="7864d-127">See [Build mobile applications with Xamarin and Azure Cosmos DB](mobile-apps-with-xamarin.md).</span></span>

> [!NOTE]
> <span data-ttu-id="7864d-128">Hello Azure Cosmos DB .NET Core SDK gebruikt in deze zelfstudie is nog niet compatibel met Universal Windows Platform (UWP)-apps.</span><span class="sxs-lookup"><span data-stu-id="7864d-128">hello Azure Cosmos DB .NET Core SDK used in this tutorial is not yet compatible with Universal Windows Platform (UWP) apps.</span></span> <span data-ttu-id="7864d-129">Voor een preview-versie van Hallo .NET Core SDK die ondersteuning biedt voor UWP-apps te e-mailbericht verzenden[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="7864d-129">For a preview version of hello .NET Core SDK that does support UWP apps, send email too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

<span data-ttu-id="7864d-130">Tijd om aan de slag te gaan.</span><span class="sxs-lookup"><span data-stu-id="7864d-130">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7864d-131">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7864d-131">Prerequisites</span></span>
<span data-ttu-id="7864d-132">Controleer of dat u de volgende Hallo hebt:</span><span class="sxs-lookup"><span data-stu-id="7864d-132">Please make sure you have hello following:</span></span>

* <span data-ttu-id="7864d-133">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="7864d-133">An active Azure account.</span></span> <span data-ttu-id="7864d-134">Als u nog geen account hebt, kunt u zich aanmelden voor een [gratis account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="7864d-134">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="7864d-135">U kunt ook hello gebruiken [Azure Cosmos DB Emulator](local-emulator.md) voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="7864d-135">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* [<span data-ttu-id="7864d-136">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="7864d-136">Visual Studio 2017</span></span>](https://www.visualstudio.com/vs/) 
    * <span data-ttu-id="7864d-137">Als u op Mac OS- of Linux werkt, kunt u Hallo opdrachtregelprogramma .NET Core-apps ontwikkelen Hallo installeren [.NET Core SDK](https://www.microsoft.com/net/core#macos) voor Hallo platform van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="7864d-137">If you're working on MacOS or Linux, you can develop .NET Core apps from hello command-line by installing hello [.NET Core SDK](https://www.microsoft.com/net/core#macos) for hello platform of your choice.</span></span> 
    * <span data-ttu-id="7864d-138">Als u in Windows werkt, kunt u .NET Core apps Hallo opdrachtregelprogramma ontwikkelen door het installeren van Hallo [.NET Core SDK](https://www.microsoft.com/net/core#windows).</span><span class="sxs-lookup"><span data-stu-id="7864d-138">If you're working on Windows, you can develop .NET Core apps from hello command-line by installing hello [.NET Core SDK](https://www.microsoft.com/net/core#windows).</span></span> 
    * <span data-ttu-id="7864d-139">U kunt uw eigen editor gebruiken of [Visual Studio-code](https://code.visualstudio.com/) downloaden. Deze code is gratis en werkt onder Windows, Linux en Mac OS.</span><span class="sxs-lookup"><span data-stu-id="7864d-139">You can use your own editor, or download [Visual Studio Code](https://code.visualstudio.com/) which is free and works on Windows, Linux, and MacOS.</span></span> 

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="7864d-140">Stap 1: een Azure Cosmos DB-account maken</span><span class="sxs-lookup"><span data-stu-id="7864d-140">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="7864d-141">Begin met het maken van een Azure Cosmos DB-account.</span><span class="sxs-lookup"><span data-stu-id="7864d-141">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="7864d-142">Als u al een account dat u wilt dat toouse hebt, kunt u verder gaan te[uw Visual Studio-oplossing instellen](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="7864d-142">If you already have an account you want toouse, you can skip ahead too[Setup your Visual Studio Solution](#SetupVS).</span></span> <span data-ttu-id="7864d-143">Als u hello Azure Cosmos DB Emulator, volgt u stappen op Hallo [Azure Cosmos DB Emulator](local-emulator.md) toosetup Hallo emulator en gaat u verder te[uw Visual Studio-oplossing instellen](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="7864d-143">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Setup your Visual Studio Solution](#SetupVS).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="7864d-144"><a id="SetupVS"></a>Stap 2: uw Visual Studio-oplossing instellen</span><span class="sxs-lookup"><span data-stu-id="7864d-144"><a id="SetupVS"></a>Step 2: Setup your Visual Studio solution</span></span>
1. <span data-ttu-id="7864d-145">Open **Visual Studio 2017** op uw computer.</span><span class="sxs-lookup"><span data-stu-id="7864d-145">Open **Visual Studio 2017** on your computer.</span></span>
2. <span data-ttu-id="7864d-146">Op Hallo **bestand** selecteert u **nieuw**, en kies vervolgens **Project**.</span><span class="sxs-lookup"><span data-stu-id="7864d-146">On hello **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="7864d-147">In Hallo **nieuw Project** dialoogvenster Selecteer **sjablonen** / **Visual C#** / **.NET Core** / **Consoletoepassing (.NET Core)**, uw project een naam **DocumentDBGettingStarted**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="7864d-147">In hello **New Project** dialog, select **Templates** / **Visual C#** / **.NET Core**/**Console Application (.NET Core)**, name your project **DocumentDBGettingStarted**, and then click **OK**.</span></span>

   ![Schermopname van het venster Hallo-nieuw Project](./media/documentdb-dotnetcore-get-started/nosql-tutorial-new-project-2.png)
4. <span data-ttu-id="7864d-149">In Hallo **Solution Explorer**, klik met de rechtermuisknop op **DocumentDBGettingStarted**.</span><span class="sxs-lookup"><span data-stu-id="7864d-149">In hello **Solution Explorer**, right click on **DocumentDBGettingStarted**.</span></span>
5. <span data-ttu-id="7864d-150">Klikt u op zonder Hallo menu **NuGet-pakketten beheren...** .</span><span class="sxs-lookup"><span data-stu-id="7864d-150">Then without leaving hello menu, click on **Manage NuGet Packages...**.</span></span>

   ![Schermopname van Hallo rechts op wordt geklikt Menu voor Hallo Project](./media/documentdb-dotnetcore-get-started/nosql-tutorial-manage-nuget-pacakges.png)
6. <span data-ttu-id="7864d-152">In Hallo **NuGet** tabblad **Bladeren** Hallo boven aan het Hallo-venster en typ **azure documentdb** in het zoekvak Hallo.</span><span class="sxs-lookup"><span data-stu-id="7864d-152">In hello **NuGet** tab, click **Browse** at hello top of hello window, and type **azure documentdb** in hello search box.</span></span>
7. <span data-ttu-id="7864d-153">Binnen Hallo resultaten vinden **Microsoft.Azure.DocumentDB.Core** en klik op **installeren**.</span><span class="sxs-lookup"><span data-stu-id="7864d-153">Within hello results, find **Microsoft.Azure.DocumentDB.Core** and click **Install**.</span></span>
   <span data-ttu-id="7864d-154">Hallo pakket-id voor DocumentDB-clientbibliotheek voor .NET Core Hallo [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core).</span><span class="sxs-lookup"><span data-stu-id="7864d-154">hello package ID for hello DocumentDB Client Library for .NET Core is [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core).</span></span> <span data-ttu-id="7864d-155">Als u zich richt op een .NET Framework-versie (zoals net461) die niet wordt ondersteund door dit .NET Core NuGet-pakket, gebruikt u [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB) die alle versies van .NET Framework vanaf .NET Framework 4.5 ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="7864d-155">If you are targeting a .NET Framework version (like net461) that is not supported by this .NET Core NuGet package, then use [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB) that supports all .NET Framework versions starting .NET Framework 4.5.</span></span>
8. <span data-ttu-id="7864d-156">Op Hallo prompts Hallo NuGet-pakket installaties en Hallo licentieovereenkomst te accepteren.</span><span class="sxs-lookup"><span data-stu-id="7864d-156">At hello prompts, accept hello NuGet package installations and hello license agreement.</span></span>

<span data-ttu-id="7864d-157">Goed gedaan.</span><span class="sxs-lookup"><span data-stu-id="7864d-157">Great!</span></span> <span data-ttu-id="7864d-158">Nu dat Hallo setup is voltooid, begint schrijven van code.</span><span class="sxs-lookup"><span data-stu-id="7864d-158">Now that we finished hello setup, let's start writing some code.</span></span> <span data-ttu-id="7864d-159">Op [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) vindt u een voltooid codeproject voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="7864d-159">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span></span>

## <span data-ttu-id="7864d-160"><a id="Connect"></a>Stap 3: Verbinding maken met tooan Azure DB die Cosmos-account</span><span class="sxs-lookup"><span data-stu-id="7864d-160"><a id="Connect"></a>Step 3: Connect tooan Azure Cosmos DB account</span></span>
<span data-ttu-id="7864d-161">Voeg eerst deze verwijzingen toohello begin van de C#-toepassing, in het bestand Program.cs Hallo:</span><span class="sxs-lookup"><span data-stu-id="7864d-161">First, add these references toohello beginning of your C# application, in hello Program.cs file:</span></span>

```csharp
using System;

// ADD THIS PART tooYOUR CODE
using System.Linq;
using System.Threading.Tasks;
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

> [!IMPORTANT]
> <span data-ttu-id="7864d-162">In deze zelfstudie voor toocomplete order, zorg ervoor dat u Hallo bovenstaande afhankelijkheden toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7864d-162">In order toocomplete this tutorial, make sure you add hello dependencies above.</span></span>

<span data-ttu-id="7864d-163">Voeg nu deze twee constanten en de variabele *client* toe onder de openbare klasse *Program*.</span><span class="sxs-lookup"><span data-stu-id="7864d-163">Now, add these two constants and your *client* variable underneath your public class *Program*.</span></span>

```csharp
class Program
{
    // ADD THIS PART tooYOUR CODE
    private const string EndpointUri = "<your endpoint URI>";
    private const string PrimaryKey = "<your key>";
    private DocumentClient client;
```

<span data-ttu-id="7864d-164">Vervolgens head toohello [Azure Portal](https://portal.azure.com) tooretrieve uw URI en primaire sleutel.</span><span class="sxs-lookup"><span data-stu-id="7864d-164">Next, head toohello [Azure Portal](https://portal.azure.com) tooretrieve your URI and primary key.</span></span> <span data-ttu-id="7864d-165">Hello Azure Cosmos DB URI en primaire sleutel nodig zijn voor uw toepassing toounderstand waar tooconnect en voor Azure Cosmos DB tootrust van uw toepassing verbinding.</span><span class="sxs-lookup"><span data-stu-id="7864d-165">hello Azure Cosmos DB URI and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span>

<span data-ttu-id="7864d-166">In Azure Portal Hallo, navigeer tooyour Azure DB die Cosmos-account en klik op **sleutels**.</span><span class="sxs-lookup"><span data-stu-id="7864d-166">In hello Azure Portal, navigate tooyour Azure Cosmos DB account, and then click **Keys**.</span></span>

<span data-ttu-id="7864d-167">Hallo URI van de portal Hallo Kopieer en plak deze in `<your endpoint URI>` in het bestand program.cs Hallo.</span><span class="sxs-lookup"><span data-stu-id="7864d-167">Copy hello URI from hello portal and paste it into `<your endpoint URI>` in hello program.cs file.</span></span> <span data-ttu-id="7864d-168">Vervolgens kopiëren primaire sleutel van de portal Hallo Hallo en plak deze in `<your key>`.</span><span class="sxs-lookup"><span data-stu-id="7864d-168">Then copy hello PRIMARY KEY from hello portal and paste it into `<your key>`.</span></span> <span data-ttu-id="7864d-169">Als u hello Azure Cosmos DB Emulator, gebruikt u `https://localhost:8081` als Hallo eindpunt en Hallo goed gedefinieerde autorisatiesleutel van [hoe met behulp van toodevelop hello Azure Cosmos DB Emulator](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="7864d-169">If you are using hello Azure Cosmos DB Emulator, use `https://localhost:8081` as hello endpoint, and hello well-defined authorization key from [How toodevelop using hello Azure Cosmos DB Emulator](local-emulator.md).</span></span> <span data-ttu-id="7864d-170">Zorg ervoor dat tooremove Hallo < en >, maar laat Hallo dubbele aanhalingstekens rond uw eindpunt en -sleutel.</span><span class="sxs-lookup"><span data-stu-id="7864d-170">Make sure tooremove hello < and > but leave hello double quotes around your endpoint and key.</span></span>

![Schermopname van hello Azure Portal gebruikt door Hallo NoSQL-zelfstudie toocreate een C#-consoletoepassing.][keys]

<span data-ttu-id="7864d-173">We ophalen gestarte toepassing hello beginnen met het maken van een nieuw exemplaar van Hallo **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="7864d-173">We'll start hello getting started application by creating a new instance of hello **DocumentClient**.</span></span>

<span data-ttu-id="7864d-174">Hieronder Hallo **Main** methode toevoegen van nieuwe asynchrone taak aangeroepen **GetStartedDemo**, die wordt een exemplaar van onze nieuwe **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="7864d-174">Below hello **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span></span>

```csharp
static void Main(string[] args)
{
}

// ADD THIS PART tooYOUR CODE
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);
}
```

<span data-ttu-id="7864d-175">Voeg Hallo volgende code toorun uw asynchrone taak van uw **Main** methode.</span><span class="sxs-lookup"><span data-stu-id="7864d-175">Add hello following code toorun your asynchronous task from your **Main** method.</span></span> <span data-ttu-id="7864d-176">Hallo **Main** methode wordt onderschept uitzonderingen en toohello console geschreven.</span><span class="sxs-lookup"><span data-stu-id="7864d-176">hello **Main** method will catch exceptions and write them toohello console.</span></span>

```csharp
static void Main(string[] args)
{
        // ADD THIS PART tooYOUR CODE
        try
        {
                Program p = new Program();
                p.GetStartedDemo().Wait();
        }
        catch (DocumentClientException de)
        {
                Exception baseException = de.GetBaseException();
                Console.WriteLine("{0} error occurred: {1}, Message: {2}", de.StatusCode, de.Message, baseException.Message);
        }
        catch (Exception e)
        {
                Exception baseException = e.GetBaseException();
                Console.WriteLine("Error: {0}, Message: {1}", e.Message, baseException.Message);
        }
        finally
        {
                Console.WriteLine("End of demo, press any key tooexit.");
                Console.ReadKey();
        }
```

<span data-ttu-id="7864d-177">Druk op Hallo **DocumentDBGettingStarted** toobuild knop en het Hallo-toepassing worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7864d-177">Press hello **DocumentDBGettingStarted** button toobuild and run hello application.</span></span>

<span data-ttu-id="7864d-178">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="7864d-178">Congratulations!</span></span> <span data-ttu-id="7864d-179">U hebt verbinding gemaakt tooan Azure DB die Cosmos-account, laten we nu eens kijken werken met Azure DB die Cosmos-resources.</span><span class="sxs-lookup"><span data-stu-id="7864d-179">You have successfully connected tooan Azure Cosmos DB account, let's now take a look at working with Azure Cosmos DB resources.</span></span>  

## <a name="step-4-create-a-database"></a><span data-ttu-id="7864d-180">Stap 4: een database maken</span><span class="sxs-lookup"><span data-stu-id="7864d-180">Step 4: Create a database</span></span>
<span data-ttu-id="7864d-181">Voordat u Hallo-code voor het maken van een database toevoegt, Voeg een Help-methode voor het schrijven van toohello-console.</span><span class="sxs-lookup"><span data-stu-id="7864d-181">Before you add hello code for creating a database, add a helper method for writing toohello console.</span></span>

<span data-ttu-id="7864d-182">Kopieer en plak Hallo **WriteToConsoleAndPromptToContinue** methode onder Hallo **GetStartedDemo** methode.</span><span class="sxs-lookup"><span data-stu-id="7864d-182">Copy and paste hello **WriteToConsoleAndPromptToContinue** method underneath hello **GetStartedDemo** method.</span></span>

```csharp
// ADD THIS PART tooYOUR CODE
private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
{
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key toocontinue ...");
        Console.ReadKey();
}
```

<span data-ttu-id="7864d-183">Uw Azure-Cosmos-DB [database](documentdb-resources.md#databases) kunnen worden gemaakt met behulp van Hallo [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) methode Hallo **DocumentClient** klasse.</span><span class="sxs-lookup"><span data-stu-id="7864d-183">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="7864d-184">Een database is een logische container voor documentopslag, gepartitioneerd in verzamelingen JSON Hallo.</span><span class="sxs-lookup"><span data-stu-id="7864d-184">A database is hello logical container of JSON document storage partitioned across collections.</span></span>

<span data-ttu-id="7864d-185">Kopiëren en plakken Hallo volgende code tooyour **GetStartedDemo** methode onder Hallo client maken.</span><span class="sxs-lookup"><span data-stu-id="7864d-185">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello client creation.</span></span> <span data-ttu-id="7864d-186">Hiermee maakt u een database met de naam *FamilyDB*.</span><span class="sxs-lookup"><span data-stu-id="7864d-186">This will create a database named *FamilyDB*.</span></span>

```csharp
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    // ADD THIS PART tooYOUR CODE
    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB_oa" });
```

<span data-ttu-id="7864d-187">Druk op Hallo **DocumentDBGettingStarted** knop toorun uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="7864d-187">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="7864d-188">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="7864d-188">Congratulations!</span></span> <span data-ttu-id="7864d-189">U hebt een Azure Cosmos DB-database gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7864d-189">You have successfully created an Azure Cosmos DB database.</span></span>  

## <span data-ttu-id="7864d-190"><a id="CreateColl"></a>Stap 5: een verzameling maken</span><span class="sxs-lookup"><span data-stu-id="7864d-190"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="7864d-191">Met **CreateDocumentCollectionAsync** maakt u een nieuwe verzameling met gereserveerde doorvoer, wat gevolgen heeft voor de kosten.</span><span class="sxs-lookup"><span data-stu-id="7864d-191">**CreateDocumentCollectionAsync** will create a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="7864d-192">Zie onze [pagina met prijzen](https://azure.microsoft.com/pricing/details/cosmos-db/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="7864d-192">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>

<span data-ttu-id="7864d-193">Een [verzameling](documentdb-resources.md#collections) kunnen worden gemaakt met behulp van Hallo [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) methode Hallo **DocumentClient** klasse.</span><span class="sxs-lookup"><span data-stu-id="7864d-193">A [collection](documentdb-resources.md#collections) can be created by using hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="7864d-194">Een verzameling is een container van JSON-documenten en de bijbehorende JavaScript-toepassingslogica.</span><span class="sxs-lookup"><span data-stu-id="7864d-194">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="7864d-195">Kopiëren en plakken Hallo volgende code tooyour **GetStartedDemo** methode onder Hallo database wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7864d-195">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello database creation.</span></span> <span data-ttu-id="7864d-196">Hiermee maakt u een documentverzameling met de naam *FamilyCollection_oa*.</span><span class="sxs-lookup"><span data-stu-id="7864d-196">This will create a document collection named *FamilyCollection_oa*.</span></span>

```csharp
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    await this.client.CreateDatabaseIfNotExists("FamilyDB_oa");

    // ADD THIS PART tooYOUR CODE
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"), new DocumentCollection { Id = "FamilyCollection_oa" });
```

<span data-ttu-id="7864d-197">Druk op Hallo **DocumentDBGettingStarted** knop toorun uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="7864d-197">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="7864d-198">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="7864d-198">Congratulations!</span></span> <span data-ttu-id="7864d-199">U hebt een Azure Cosmos DB-documentverzameling gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7864d-199">You have successfully created an Azure Cosmos DB document collection.</span></span>  

## <span data-ttu-id="7864d-200"><a id="CreateDoc"></a>Stap 6: JSON-documenten maken</span><span class="sxs-lookup"><span data-stu-id="7864d-200"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="7864d-201">Een [document](documentdb-resources.md#documents) kunnen worden gemaakt met behulp van Hallo [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) methode Hallo **DocumentClient** klasse.</span><span class="sxs-lookup"><span data-stu-id="7864d-201">A [document](documentdb-resources.md#documents) can be created by using hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="7864d-202">Documenten bestaan uit door gebruikers gedefinieerde (willekeurige) JSON-inhoud.</span><span class="sxs-lookup"><span data-stu-id="7864d-202">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="7864d-203">U kunt nu een of meer documenten invoegen.</span><span class="sxs-lookup"><span data-stu-id="7864d-203">We can now insert one or more documents.</span></span> <span data-ttu-id="7864d-204">Als u gegevens die u wilt toostore in de database al hebt, kunt u Azure Cosmos DB [hulpprogramma voor gegevensmigratie](import-data.md).</span><span class="sxs-lookup"><span data-stu-id="7864d-204">If you already have data you'd like toostore in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md).</span></span>

<span data-ttu-id="7864d-205">We moeten eerst toocreate een **familie** klasse die objecten die zijn opgeslagen in Azure Cosmos DB in dit voorbeeld wordt aangegeven.</span><span class="sxs-lookup"><span data-stu-id="7864d-205">First, we need toocreate a **Family** class that will represent objects stored within Azure Cosmos DB in this sample.</span></span> <span data-ttu-id="7864d-206">Daarnaast moeten de subklassen **Parent**, **Child**, **Pet** en **Address** worden gemaakt die in de klasse **Family** worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7864d-206">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span></span> <span data-ttu-id="7864d-207">Houd er rekening mee dat de documenten een **id**-eigenschap moeten bevatten die in JSON is geserialiseerd als **id**.</span><span class="sxs-lookup"><span data-stu-id="7864d-207">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> <span data-ttu-id="7864d-208">Maak deze klassen door toe te voegen na interne onderliggende klassen na Hallo Hallo **GetStartedDemo** methode.</span><span class="sxs-lookup"><span data-stu-id="7864d-208">Create these classes by adding hello following internal sub-classes after hello **GetStartedDemo** method.</span></span>

<span data-ttu-id="7864d-209">Kopieer en plak Hallo **familie**, **bovenliggende**, **onderliggende**, **huisdier**, en **adres** klassen onder Hallo **WriteToConsoleAndPromptToContinue** methode.</span><span class="sxs-lookup"><span data-stu-id="7864d-209">Copy and paste hello **Family**, **Parent**, **Child**, **Pet**, and **Address** classes underneath hello **WriteToConsoleAndPromptToContinue** method.</span></span>

```csharp
private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
{
    Console.WriteLine(format, args);
    Console.WriteLine("Press any key toocontinue ...");
    Console.ReadKey();
}

// ADD THIS PART tooYOUR CODE
public class Family
{
    [JsonProperty(PropertyName = "id")]
    public string Id { get; set; }
    public string LastName { get; set; }
    public Parent[] Parents { get; set; }
    public Child[] Children { get; set; }
    public Address Address { get; set; }
    public bool IsRegistered { get; set; }
    public override string ToString()
    {
            return JsonConvert.SerializeObject(this);
    }
}

public class Parent
{
    public string FamilyName { get; set; }
    public string FirstName { get; set; }
}

public class Child
{
    public string FamilyName { get; set; }
    public string FirstName { get; set; }
    public string Gender { get; set; }
    public int Grade { get; set; }
    public Pet[] Pets { get; set; }
}

public class Pet
{
    public string GivenName { get; set; }
}

public class Address
{
    public string State { get; set; }
    public string County { get; set; }
    public string City { get; set; }
}
```

<span data-ttu-id="7864d-210">Kopieer en plak Hallo **CreateFamilyDocumentIfNotExists** methode onder uw **CreateDocumentCollectionIfNotExists** methode.</span><span class="sxs-lookup"><span data-stu-id="7864d-210">Copy and paste hello **CreateFamilyDocumentIfNotExists** method underneath your **CreateDocumentCollectionIfNotExists** method.</span></span>

```csharp
// ADD THIS PART tooYOUR CODE
private async Task CreateFamilyDocumentIfNotExists(string databaseName, string collectionName, Family family)
{
    try
    {
        await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, family.Id));
        this.WriteToConsoleAndPromptToContinue("Found {0}", family.Id);
    }
    catch (DocumentClientException de)
    {
        if (de.StatusCode == HttpStatusCode.NotFound)
        {
            await this.client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), family);
            this.WriteToConsoleAndPromptToContinue("Created Family {0}", family.Id);
        }
        else
        {
            throw;
        }
    }
}
```

<span data-ttu-id="7864d-211">En Voeg twee documenten, één voor Hallo Andersen Family en Hallo Wakefield Family.</span><span class="sxs-lookup"><span data-stu-id="7864d-211">And insert two documents, one each for hello Andersen Family and hello Wakefield Family.</span></span>

<span data-ttu-id="7864d-212">Kopieer en plak Hallo-code die volgt `// ADD THIS PART tooYOUR CODE` tooyour **GetStartedDemo** methode onder Hallo verzamelen van documenten.</span><span class="sxs-lookup"><span data-stu-id="7864d-212">Copy and paste hello code that follows `// ADD THIS PART tooYOUR CODE` tooyour **GetStartedDemo** method underneath hello document collection creation.</span></span>

```csharp
await this.CreateDatabaseIfNotExists("FamilyDB_oa");

await this.CreateDocumentCollectionIfNotExists("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART tooYOUR CODE
Family andersenFamily = new Family
{
        Id = "Andersen.1",
        LastName = "Andersen",
        Parents = new Parent[]
        {
                new Parent { FirstName = "Thomas" },
                new Parent { FirstName = "Mary Kay" }
        },
        Children = new Child[]
        {
                new Child
                {
                        FirstName = "Henriette Thaulow",
                        Gender = "female",
                        Grade = 5,
                        Pets = new Pet[]
                        {
                                new Pet { GivenName = "Fluffy" }
                        }
                }
        },
        Address = new Address { State = "WA", County = "King", City = "Seattle" },
        IsRegistered = true
};

await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", andersenFamily);

Family wakefieldFamily = new Family
{
        Id = "Wakefield.7",
        LastName = "Wakefield",
        Parents = new Parent[]
        {
                new Parent { FamilyName = "Wakefield", FirstName = "Robin" },
                new Parent { FamilyName = "Miller", FirstName = "Ben" }
        },
        Children = new Child[]
        {
                new Child
                {
                        FamilyName = "Merriam",
                        FirstName = "Jesse",
                        Gender = "female",
                        Grade = 8,
                        Pets = new Pet[]
                        {
                                new Pet { GivenName = "Goofy" },
                                new Pet { GivenName = "Shadow" }
                        }
                },
                new Child
                {
                        FamilyName = "Miller",
                        FirstName = "Lisa",
                        Gender = "female",
                        Grade = 1
                }
        },
        Address = new Address { State = "NY", County = "Manhattan", City = "NY" },
        IsRegistered = false
};

await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);
```

<span data-ttu-id="7864d-213">Druk op Hallo **DocumentDBGettingStarted** knop toorun uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="7864d-213">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="7864d-214">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="7864d-214">Congratulations!</span></span> <span data-ttu-id="7864d-215">U hebt twee Azure Cosmos DB-documenten gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7864d-215">You have successfully created two Azure Cosmos DB documents.</span></span>  

![Diagram ter illustratie Hallo hiërarchische relatie tussen Hallo-account, onlinedatabase Hallo Hallo verzameling en Hallo documenten die worden gebruikt door Hallo NoSQL-zelfstudie toocreate een C#-consoletoepassing](./media/documentdb-dotnetcore-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="7864d-217"><a id="Query"></a>Stap 7: query's uitvoeren op Azure Cosmos DB-resources</span><span class="sxs-lookup"><span data-stu-id="7864d-217"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="7864d-218">Azure Cosmos DB biedt ondersteuning voor uitgebreide [query's](documentdb-sql-query.md) op de JSON-documenten die zijn opgeslagen in elke verzameling.</span><span class="sxs-lookup"><span data-stu-id="7864d-218">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="7864d-219">Hallo volgende voorbeeldcode bevat verschillende query's: met behulp van zowel SQL Azure Cosmos DB syntaxis als LINQ, die kunnen worden uitgevoerd op basis van documenten die wordt ingevoegd in de vorige stap Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="7864d-219">hello following sample code shows various queries - using both Azure Cosmos DB SQL syntax as well as LINQ - that we can run against hello documents we inserted in hello previous step.</span></span>

<span data-ttu-id="7864d-220">Kopieer en plak Hallo **ExecuteSimpleQuery** methode onder uw **CreateFamilyDocumentIfNotExists** methode.</span><span class="sxs-lookup"><span data-stu-id="7864d-220">Copy and paste hello **ExecuteSimpleQuery** method underneath your **CreateFamilyDocumentIfNotExists** method.</span></span>

```csharp
// ADD THIS PART tooYOUR CODE
private void ExecuteSimpleQuery(string databaseName, string collectionName)
{
    // Set some common query options
    FeedOptions queryOptions = new FeedOptions { MaxItemCount = -1 };

        // Here we find hello Andersen family via its LastName
        IQueryable<Family> familyQuery = this.client.CreateDocumentQuery<Family>(
                UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), queryOptions)
                .Where(f => f.LastName == "Andersen");

        // hello query is executed synchronously here, but can also be executed asynchronously via hello IDocumentQuery<T> interface
        Console.WriteLine("Running LINQ query...");
        foreach (Family family in familyQuery)
        {
            Console.WriteLine("\tRead {0}", family);
        }

        // Now execute hello same query via direct SQL
        IQueryable<Family> familyQueryInSql = this.client.CreateDocumentQuery<Family>(
                UriFactory.CreateDocumentCollectionUri(databaseName, collectionName),
                "SELECT * FROM Family WHERE Family.LastName = 'Andersen'",
                queryOptions);

        Console.WriteLine("Running direct SQL query...");
        foreach (Family family in familyQueryInSql)
        {
                Console.WriteLine("\tRead {0}", family);
        }

        Console.WriteLine("Press any key toocontinue ...");
        Console.ReadKey();
}
```

<span data-ttu-id="7864d-221">Kopiëren en plakken Hallo volgende code tooyour **GetStartedDemo** methode onder Hallo tweede document maken.</span><span class="sxs-lookup"><span data-stu-id="7864d-221">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello second document creation.</span></span>

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

// ADD THIS PART tooYOUR CODE
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

<span data-ttu-id="7864d-222">Druk op Hallo **DocumentDBGettingStarted** knop toorun uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="7864d-222">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="7864d-223">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="7864d-223">Congratulations!</span></span> <span data-ttu-id="7864d-224">U hebt een query uitgevoerd op een Azure Cosmos DB-verzameling.</span><span class="sxs-lookup"><span data-stu-id="7864d-224">You have successfully queried against an Azure Cosmos DB collection.</span></span>

<span data-ttu-id="7864d-225">Hallo volgende diagram illustreert hoe hello Azure Cosmos DB SQL-query syntaxis wordt aangeroepen voor Hallo verzameling die u hebt gemaakt en hello dezelfde logica toegepast toohello LINQ-query.</span><span class="sxs-lookup"><span data-stu-id="7864d-225">hello following diagram illustrates how hello Azure Cosmos DB SQL query syntax is called against hello collection you created, and hello same logic applies toohello LINQ query as well.</span></span>

![Diagram ter illustratie van Hallo bereik en de betekenis van Hallo query die wordt gebruikt door Hallo NoSQL-zelfstudie toocreate een C#-consoletoepassing](./media/documentdb-dotnetcore-get-started/nosql-tutorial-collection-documents.png)

<span data-ttu-id="7864d-227">Hallo [FROM](documentdb-sql-query.md#FromClause) sleutelwoord is optioneel in Hallo query omdat Azure Cosmos DB-query's al één verzameling tooa binnen het bereik zijn.</span><span class="sxs-lookup"><span data-stu-id="7864d-227">hello [FROM](documentdb-sql-query.md#FromClause) keyword is optional in hello query because Azure Cosmos DB queries are already scoped tooa single collection.</span></span> <span data-ttu-id="7864d-228">Daarom kan FROM Families f worden ingewisseld door FROM root r, of een andere gewenste variabelenaam.</span><span class="sxs-lookup"><span data-stu-id="7864d-228">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="7864d-229">DocumentDB wordt afgeleid dat Families, root of Hallo variabelenaam u hebt gekozen, verwijzing Hallo huidige verzameling standaard.</span><span class="sxs-lookup"><span data-stu-id="7864d-229">DocumentDB will infer that Families, root, or hello variable name you chose, reference hello current collection by default.</span></span>

## <span data-ttu-id="7864d-230"><a id="ReplaceDocument"></a>Stap 8: JSON-document vervangen</span><span class="sxs-lookup"><span data-stu-id="7864d-230"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="7864d-231">Azure Cosmos DB biedt ondersteuning voor het vervangen van JSON-documenten.</span><span class="sxs-lookup"><span data-stu-id="7864d-231">Azure Cosmos DB supports replacing JSON documents.</span></span>  

<span data-ttu-id="7864d-232">Kopieer en plak Hallo **ReplaceFamilyDocument** methode onder uw **ExecuteSimpleQuery** methode.</span><span class="sxs-lookup"><span data-stu-id="7864d-232">Copy and paste hello **ReplaceFamilyDocument** method underneath your **ExecuteSimpleQuery** method.</span></span>

```csharp
// ADD THIS PART tooYOUR CODE
private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
{
    try
    {
        await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
        this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }
    catch (DocumentClientException de)
    {
        throw;
    }
}
```

<span data-ttu-id="7864d-233">Kopiëren en plakken Hallo volgende code tooyour **GetStartedDemo** methode onder Hallo queryuitvoering.</span><span class="sxs-lookup"><span data-stu-id="7864d-233">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello query execution.</span></span> <span data-ttu-id="7864d-234">Na het Hallo-document vervangen, Hallo wordt uitgevoerd dezelfde query opnieuw tooview Hallo gewijzigd document.</span><span class="sxs-lookup"><span data-stu-id="7864d-234">After replacing hello document, this will run hello same query again tooview hello changed document.</span></span>

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART tooYOUR CODE
// Update hello Grade of hello Andersen Family child
andersenFamily.Children[0].Grade = 6;

await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

<span data-ttu-id="7864d-235">Druk op Hallo **DocumentDBGettingStarted** knop toorun uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="7864d-235">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="7864d-236">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="7864d-236">Congratulations!</span></span> <span data-ttu-id="7864d-237">U hebt een Azure Cosmos DB-document vervangen.</span><span class="sxs-lookup"><span data-stu-id="7864d-237">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="7864d-238"><a id="DeleteDocument"></a>Stap 9: JSON-document verwijderen</span><span class="sxs-lookup"><span data-stu-id="7864d-238"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="7864d-239">Azure Cosmos DB biedt ondersteuning voor het verwijderen van JSON-documenten.</span><span class="sxs-lookup"><span data-stu-id="7864d-239">Azure Cosmos DB supports deleting JSON documents.</span></span>  

<span data-ttu-id="7864d-240">Kopieer en plak Hallo **DeleteFamilyDocument** methode onder uw **ReplaceFamilyDocument** methode.</span><span class="sxs-lookup"><span data-stu-id="7864d-240">Copy and paste hello **DeleteFamilyDocument** method underneath your **ReplaceFamilyDocument** method.</span></span>

```csharp
// ADD THIS PART tooYOUR CODE
private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
{
    try
    {
        await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
        Console.WriteLine("Deleted Family {0}", documentName);
    }
    catch (DocumentClientException de)
    {
        throw;
    }
}
```

<span data-ttu-id="7864d-241">Kopiëren en plakken Hallo volgende code tooyour **GetStartedDemo** methode onder Hallo tweede queryuitvoering.</span><span class="sxs-lookup"><span data-stu-id="7864d-241">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello second query execution.</span></span>

```csharp
await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART tooCODE
await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");
```

<span data-ttu-id="7864d-242">Druk op Hallo **DocumentDBGettingStarted** knop toorun uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="7864d-242">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="7864d-243">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="7864d-243">Congratulations!</span></span> <span data-ttu-id="7864d-244">U hebt een Azure Cosmos DB-document verwijderd.</span><span class="sxs-lookup"><span data-stu-id="7864d-244">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="7864d-245"><a id="DeleteDatabase"></a>Stap 10: Hallo-database verwijderen</span><span class="sxs-lookup"><span data-stu-id="7864d-245"><a id="DeleteDatabase"></a>Step 10: Delete hello database</span></span>
<span data-ttu-id="7864d-246">Verwijderen Hallo gemaakt van de database wordt verwijderd Hallo-database en alle onderliggende resources (verzamelingen, documenten, enz.).</span><span class="sxs-lookup"><span data-stu-id="7864d-246">Deleting hello created database will remove hello database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="7864d-247">Kopiëren en plakken Hallo volgende code tooyour **GetStartedDemo** methode onder Hallo document toodelete Hallo gehele database en alle onderliggende resources verwijderen.</span><span class="sxs-lookup"><span data-stu-id="7864d-247">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello document delete toodelete hello entire database and all children resources.</span></span>

```csharp
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");

// ADD THIS PART tooCODE
// Clean up/delete hello database
await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"));
```

<span data-ttu-id="7864d-248">Druk op Hallo **DocumentDBGettingStarted** knop toorun uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="7864d-248">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="7864d-249">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="7864d-249">Congratulations!</span></span> <span data-ttu-id="7864d-250">U hebt een Azure Cosmos DB-database verwijderd.</span><span class="sxs-lookup"><span data-stu-id="7864d-250">You have successfully deleted an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="7864d-251"><a id="Run"></a>Stap 11: uw C#-consoletoepassing volledig uitvoeren</span><span class="sxs-lookup"><span data-stu-id="7864d-251"><a id="Run"></a>Step 11: Run your C# console application all together!</span></span>
<span data-ttu-id="7864d-252">Druk op Hallo **DocumentDBGettingStarted** knop in Visual Studio toobuild Hallo toepassing in de foutopsporingsmodus.</span><span class="sxs-lookup"><span data-stu-id="7864d-252">Press hello **DocumentDBGettingStarted** button in Visual Studio toobuild hello application in debug mode.</span></span>

<span data-ttu-id="7864d-253">U ziet de uitvoer van uw getstarted-app in het consolevenster Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="7864d-253">You should see hello output of your get started app in hello console window.</span></span> <span data-ttu-id="7864d-254">Hallo-uitvoer ziet Hallo resultaten van Hallo query's die zijn toegevoegd en moet overeenkomen met de onderstaande Hallo voorbeeldtekst.</span><span class="sxs-lookup"><span data-stu-id="7864d-254">hello output will show hello results of hello queries we added and should match hello example text below.</span></span>

```
Created FamilyDB_oa
Press any key toocontinue ...
Created FamilyCollection_oa
Press any key toocontinue ...
Created Family Andersen.1
Press any key toocontinue ...
Created Family Wakefield.7
Press any key toocontinue ...
Running LINQ query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Running direct SQL query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Replaced Family Andersen.1
Press any key toocontinue ...
Running LINQ query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Running direct SQL query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Deleted Family Andersen.1
End of demo, press any key tooexit.
```

<span data-ttu-id="7864d-255">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="7864d-255">Congratulations!</span></span> <span data-ttu-id="7864d-256">U hebt Hallo-zelfstudie voltooid en beschikt nu over een werkende C#-consoletoepassing!</span><span class="sxs-lookup"><span data-stu-id="7864d-256">You've completed hello tutorial and have a working C# console application!</span></span>

## <span data-ttu-id="7864d-257"><a id="GetSolution"></a>Volledige Hallo-zelfstudieoplossing ophalen</span><span class="sxs-lookup"><span data-stu-id="7864d-257"><a id="GetSolution"></a> Get hello complete tutorial solution</span></span>
<span data-ttu-id="7864d-258">toobuild hello GetStarted-oplossing die alle Hallo voorbeelden in dit artikel bevat, moet u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="7864d-258">toobuild hello GetStarted solution that contains all hello samples in this article, you will need hello following:</span></span>

* <span data-ttu-id="7864d-259">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="7864d-259">An active Azure account.</span></span> <span data-ttu-id="7864d-260">Als u nog geen account hebt, kunt u zich aanmelden voor een [gratis account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="7864d-260">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="7864d-261">Een [Azure Cosmos DB account][create-documentdb-dotnet.md#create-account].</span><span class="sxs-lookup"><span data-stu-id="7864d-261">An [Azure Cosmos DB account][create-documentdb-dotnet.md#create-account].</span></span>
* <span data-ttu-id="7864d-262">Hallo [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) oplossing is beschikbaar op GitHub.</span><span class="sxs-lookup"><span data-stu-id="7864d-262">hello [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="7864d-263">toorestore hello verwijzingen toohello DocumentDB-API voor Azure Cosmos DB .NET Core SDK in Visual Studio met de rechtermuisknop op Hallo **GetStarted** oplossing in Solution Explorer en klik vervolgens op **inschakelen NuGet-pakket herstellen**.</span><span class="sxs-lookup"><span data-stu-id="7864d-263">toorestore hello references toohello DocumentDB API for Azure Cosmos DB .NET Core SDK in Visual Studio, right-click hello **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span></span> <span data-ttu-id="7864d-264">In het bestand Program.cs Hallo werk vervolgens de waarden bij voor EndpointUrl en AuthorizationKey Hallo zoals beschreven in [tooan Azure DB die Cosmos-account koppelen](#Connect).</span><span class="sxs-lookup"><span data-stu-id="7864d-264">Next, in hello Program.cs file, update hello EndpointUrl and AuthorizationKey values as described in [Connect tooan Azure Cosmos DB account](#Connect).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7864d-265">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7864d-265">Next steps</span></span>
* <span data-ttu-id="7864d-266">Wilt u een complexere ASP.NET MVC-zelfstudie?</span><span class="sxs-lookup"><span data-stu-id="7864d-266">Want a more complex ASP.NET MVC tutorial?</span></span> <span data-ttu-id="7864d-267">Zie [ASP.NET MVC-zelfstudie: Web ontwikkelen van toepassingen met Azure Cosmos DB](documentdb-dotnet-application.md).</span><span class="sxs-lookup"><span data-stu-id="7864d-267">See [ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB](documentdb-dotnet-application.md).</span></span>
* <span data-ttu-id="7864d-268">Wilt u toodevelop een Xamarin iOS, Android of formulieren DocumentDB-API voor Azure Cosmos DB .NET Core SDK gebruikt toepassing hello?</span><span class="sxs-lookup"><span data-stu-id="7864d-268">Want toodevelop a Xamarin iOS, Android, or Forms application using hello DocumentDB API for Azure Cosmos DB .NET Core SDK?</span></span> <span data-ttu-id="7864d-269">Zie [ontwikkelen van mobiele toepassingen met Xamarin en Azure Cosmos DB](mobile-apps-with-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="7864d-269">See [Build mobile applications with Xamarin and Azure Cosmos DB](mobile-apps-with-xamarin.md).</span></span>
* <span data-ttu-id="7864d-270">Wilt u tooperform schaal en prestaties testen met Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="7864d-270">Want tooperform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="7864d-271">Zie [prestaties en schaal testen met Azure Cosmos-DB](performance-testing.md)</span><span class="sxs-lookup"><span data-stu-id="7864d-271">See [Performance and scale testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="7864d-272">Meer informatie over hoe te[Monitor Azure Cosmos DB aanvragen, het gebruik en de opslag](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="7864d-272">Learn how too[Monitor Azure Cosmos DB requests, usage, and storage](monitor-accounts.md).</span></span>
* <span data-ttu-id="7864d-273">Query's uitvoeren op onze voorbeeldgegevensset in Hallo [Queryspeelplaats](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="7864d-273">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="7864d-274">toolearn meer informatie over het programmeermodel hello, Zie [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="7864d-274">toolearn more about hello programming model, see [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span>

[create-documentdb-dotnet.md#create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-dotnetcore-get-started/nosql-tutorial-keys.png
