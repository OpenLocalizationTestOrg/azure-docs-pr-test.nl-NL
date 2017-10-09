---
title: 'Azure Cosmos DB: aan de slag met de DocumentDB-API | Microsoft Docs'
description: Een zelfstudie waarmee u maakt een online database en C#-consoletoepassing Hallo DocumentDB API gebruiken.
keywords: nosql zelfstudie, onlinedatabase, c#-consoletoepassing
services: cosmos-db
documentationcenter: .net
author: AndrewHoh
manager: jhubbard
editor: monicar
ms.assetid: bf08e031-718a-4a2a-89d6-91e12ff8797d
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/16/2017
ms.author: anhoh
ms.openlocfilehash: 65a181f715a670987492ad7815ef2ec94498e84d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-documentdb-api-getting-started-tutorial"></a><span data-ttu-id="a4a09-104">Azure Cosmos DB: aan de slag met de DocumentDB-API</span><span class="sxs-lookup"><span data-stu-id="a4a09-104">Azure Cosmos DB: DocumentDB API getting started tutorial</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a4a09-105">.NET</span><span class="sxs-lookup"><span data-stu-id="a4a09-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="a4a09-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="a4a09-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="a4a09-107">Node.js voor MongoDB</span><span class="sxs-lookup"><span data-stu-id="a4a09-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="a4a09-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="a4a09-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="a4a09-109">Java</span><span class="sxs-lookup"><span data-stu-id="a4a09-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="a4a09-110">C++</span><span class="sxs-lookup"><span data-stu-id="a4a09-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="a4a09-111">Zelfstudie Welkom toohello API van Azure Cosmos DB DocumentDB aan de slag!</span><span class="sxs-lookup"><span data-stu-id="a4a09-111">Welcome toohello Azure Cosmos DB DocumentDB API getting started tutorial!</span></span> <span data-ttu-id="a4a09-112">Wanneer u deze zelfstudie hebt voltooid, beschikt u over een consoletoepassing waarmee u Azure Cosmos DB-resources kunt maken en er query's op kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="a4a09-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="a4a09-113">De volgende onderwerpen komen aan bod:</span><span class="sxs-lookup"><span data-stu-id="a4a09-113">We'll cover:</span></span>

* <span data-ttu-id="a4a09-114">Maken en te verbinden tooan Azure DB die Cosmos-account</span><span class="sxs-lookup"><span data-stu-id="a4a09-114">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="a4a09-115">Uw Visual Studio-oplossing configureren</span><span class="sxs-lookup"><span data-stu-id="a4a09-115">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="a4a09-116">Een online-database maken</span><span class="sxs-lookup"><span data-stu-id="a4a09-116">Creating an online database</span></span>
* <span data-ttu-id="a4a09-117">Een verzameling maken</span><span class="sxs-lookup"><span data-stu-id="a4a09-117">Creating a collection</span></span>
* <span data-ttu-id="a4a09-118">JSON-documenten maken</span><span class="sxs-lookup"><span data-stu-id="a4a09-118">Creating JSON documents</span></span>
* <span data-ttu-id="a4a09-119">Hallo verzameling opvragen</span><span class="sxs-lookup"><span data-stu-id="a4a09-119">Querying hello collection</span></span>
* <span data-ttu-id="a4a09-120">Een document vervangen</span><span class="sxs-lookup"><span data-stu-id="a4a09-120">Replacing a document</span></span>
* <span data-ttu-id="a4a09-121">Een document verwijderen</span><span class="sxs-lookup"><span data-stu-id="a4a09-121">Deleting a document</span></span>
* <span data-ttu-id="a4a09-122">Hallo-database verwijderen</span><span class="sxs-lookup"><span data-stu-id="a4a09-122">Deleting hello database</span></span>

<span data-ttu-id="a4a09-123">Hebt u geen tijd?</span><span class="sxs-lookup"><span data-stu-id="a4a09-123">Don't have time?</span></span> <span data-ttu-id="a4a09-124">Geen probleem.</span><span class="sxs-lookup"><span data-stu-id="a4a09-124">Don't worry!</span></span> <span data-ttu-id="a4a09-125">Hallo volledige oplossing is beschikbaar op [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="a4a09-125">hello complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span></span> <span data-ttu-id="a4a09-126">Springen toohello [Hallo volledige NoSQL-zelfstudieoplossing sectie ophalen](#GetSolution) voor beknopte instructies.</span><span class="sxs-lookup"><span data-stu-id="a4a09-126">Jump toohello [Get hello complete NoSQL tutorial solution section](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="a4a09-127">Daarna stemknoppen Neem gebruik Hallo Hallo boven of onder aan deze pagina toogive ons feedback.</span><span class="sxs-lookup"><span data-stu-id="a4a09-127">Afterwards, please use hello voting buttons at hello top or bottom of this page toogive us feedback.</span></span> <span data-ttu-id="a4a09-128">Als u graag toocontact u rechtstreeks kunt u gratis tooinclude je e-mailadres in uw opmerkingen.</span><span class="sxs-lookup"><span data-stu-id="a4a09-128">If you'd like us toocontact you directly, feel free tooinclude your email address in your comments.</span></span>

<span data-ttu-id="a4a09-129">Tijd om aan de slag te gaan.</span><span class="sxs-lookup"><span data-stu-id="a4a09-129">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4a09-130">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a4a09-130">Prerequisites</span></span>
<span data-ttu-id="a4a09-131">Controleer of dat u de volgende Hallo hebt:</span><span class="sxs-lookup"><span data-stu-id="a4a09-131">Please make sure you have hello following:</span></span>

* <span data-ttu-id="a4a09-132">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="a4a09-132">An active Azure account.</span></span> <span data-ttu-id="a4a09-133">Als u nog geen account hebt, kunt u zich aanmelden voor een [gratis account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="a4a09-133">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="a4a09-134">U kunt ook hello gebruiken [Azure Cosmos DB Emulator](local-emulator.md) voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="a4a09-134">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="a4a09-135">[Visual Studio Community 2017](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="a4a09-135">[Visual Studio Community 2017](http://www.visualstudio.com/).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="a4a09-136">Stap 1: een Azure Cosmos DB-account maken</span><span class="sxs-lookup"><span data-stu-id="a4a09-136">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="a4a09-137">Begin met het maken van een Azure Cosmos DB-account.</span><span class="sxs-lookup"><span data-stu-id="a4a09-137">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="a4a09-138">Als u al een account dat u wilt dat toouse hebt, kunt u verder gaan te[uw Visual Studio-oplossing instellen](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="a4a09-138">If you already have an account you want toouse, you can skip ahead too[Setup your Visual Studio Solution](#SetupVS).</span></span> <span data-ttu-id="a4a09-139">Als u hello Azure Cosmos DB Emulator, volgt u stappen op Hallo [Azure Cosmos DB Emulator](local-emulator.md) toosetup Hallo emulator en gaat u verder te[uw Visual Studio-oplossing instellen](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="a4a09-139">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Setup your Visual Studio Solution](#SetupVS).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="a4a09-140"><a id="SetupVS"></a>Stap 2: uw Visual Studio-oplossing instellen</span><span class="sxs-lookup"><span data-stu-id="a4a09-140"><a id="SetupVS"></a>Step 2: Setup your Visual Studio solution</span></span>
1. <span data-ttu-id="a4a09-141">Open **Visual Studio 2017** op uw computer.</span><span class="sxs-lookup"><span data-stu-id="a4a09-141">Open **Visual Studio 2017** on your computer.</span></span>
2. <span data-ttu-id="a4a09-142">Op Hallo **bestand** selecteert u **nieuw**, en kies vervolgens **Project**.</span><span class="sxs-lookup"><span data-stu-id="a4a09-142">On hello **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="a4a09-143">In Hallo **nieuw Project** dialoogvenster Selecteer **sjablonen** / **Visual C#** / **consoletoepassing**en de naam uw project en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="a4a09-143">In hello **New Project** dialog, select **Templates** / **Visual C#** / **Console Application**, name your project, and then click **OK**.</span></span>
   <span data-ttu-id="a4a09-144">![Schermopname van het venster Hallo-nieuw Project](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)</span><span class="sxs-lookup"><span data-stu-id="a4a09-144">![Screen shot of hello New Project window](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)</span></span>
4. <span data-ttu-id="a4a09-145">In Hallo **Solution Explorer**, klik met de rechtermuisknop op uw nieuwe consoletoepassing die zich onder uw Visual Studio-oplossing, en klik vervolgens op **NuGet-pakketten beheren...**</span><span class="sxs-lookup"><span data-stu-id="a4a09-145">In hello **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
    
    ![Schermopname van Hallo rechts op wordt geklikt Menu voor Hallo Project](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges.png)
5. <span data-ttu-id="a4a09-147">In Hallo **Nuget** tabblad **Bladeren**, en het type **azure documentdb** in het zoekvak Hallo.</span><span class="sxs-lookup"><span data-stu-id="a4a09-147">In hello **Nuget** tab, click **Browse**, and type **azure documentdb** in hello search box.</span></span>
6. <span data-ttu-id="a4a09-148">Binnen Hallo resultaten vinden **Microsoft.Azure.DocumentDB** en klik op **installeren**.</span><span class="sxs-lookup"><span data-stu-id="a4a09-148">Within hello results, find **Microsoft.Azure.DocumentDB** and click **Install**.</span></span>
   <span data-ttu-id="a4a09-149">Hallo pakket-id voor hello Azure Cosmos DB DocumentDB-API-clientbibliotheek [Microsoft Azure DocumentDB-clientbibliotheek](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/).</span><span class="sxs-lookup"><span data-stu-id="a4a09-149">hello package ID for hello Azure Cosmos DB DocumentDB API Client Library is [Microsoft Azure DocumentDB Client Library](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/).</span></span>
   <span data-ttu-id="a4a09-150">![Schermopname van het Hallo Nuget-Menu voor het vinden van Client-SDK van Azure Cosmos DB](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)</span><span class="sxs-lookup"><span data-stu-id="a4a09-150">![Screen shot of hello Nuget Menu for finding Azure Cosmos DB Client SDK](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)</span></span>

    <span data-ttu-id="a4a09-151">Als u een berichten krijgt over het controleren van wijzigingen toohello oplossing, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="a4a09-151">If you get a messages about reviewing changes toohello solution, click **OK**.</span></span> <span data-ttu-id="a4a09-152">Als u een bericht ontvangt over het accepteren van de licentie, klikt u op **Accepteren**.</span><span class="sxs-lookup"><span data-stu-id="a4a09-152">If you get a message about license acceptance, click **I accept**.</span></span>

<span data-ttu-id="a4a09-153">Goed gedaan.</span><span class="sxs-lookup"><span data-stu-id="a4a09-153">Great!</span></span> <span data-ttu-id="a4a09-154">Nu dat Hallo setup is voltooid, begint schrijven van code.</span><span class="sxs-lookup"><span data-stu-id="a4a09-154">Now that we finished hello setup, let's start writing some code.</span></span> <span data-ttu-id="a4a09-155">Op [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs) vindt u een voltooid codeproject voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="a4a09-155">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs).</span></span>

## <span data-ttu-id="a4a09-156"><a id="Connect"></a>Stap 3: Verbinding maken met tooan Azure DB die Cosmos-account</span><span class="sxs-lookup"><span data-stu-id="a4a09-156"><a id="Connect"></a>Step 3: Connect tooan Azure Cosmos DB account</span></span>
<span data-ttu-id="a4a09-157">Voeg eerst deze verwijzingen toohello begin van de C#-toepassing, in het bestand Program.cs Hallo:</span><span class="sxs-lookup"><span data-stu-id="a4a09-157">First, add these references toohello beginning of your C# application, in hello Program.cs file:</span></span>

    using System;
    using System.Linq;
    using System.Threading.Tasks;

    // ADD THIS PART tooYOUR CODE
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;

> [!IMPORTANT]
> <span data-ttu-id="a4a09-158">Controleer of dat u Hallo bovenstaande afhankelijkheden toevoegen in de volgorde toocomplete Hallo zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="a4a09-158">In order toocomplete hello tutorial, make sure you add hello dependencies above.</span></span>
> 
> 

<span data-ttu-id="a4a09-159">Voeg nu deze twee constanten en de variabele *client* toe onder de openbare klasse *Program*.</span><span class="sxs-lookup"><span data-stu-id="a4a09-159">Now, add these two constants and your *client* variable underneath your public class *Program*.</span></span>

    public class Program
    {
        // ADD THIS PART tooYOUR CODE
        private const string EndpointUrl = "<your endpoint URL>";
        private const string PrimaryKey = "<your primary key>";
        private DocumentClient client;

<span data-ttu-id="a4a09-160">Vervolgens head back-toohello [Azure Portal](https://portal.azure.com) tooretrieve uw eindpunt-URL en de primaire sleutel.</span><span class="sxs-lookup"><span data-stu-id="a4a09-160">Next, head back toohello [Azure Portal](https://portal.azure.com) tooretrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="a4a09-161">Hallo eindpunt-URL en de primaire sleutel nodig zijn om uw toepassing toounderstand waar tooconnect en voor Azure Cosmos DB tootrust van uw toepassing verbinding.</span><span class="sxs-lookup"><span data-stu-id="a4a09-161">hello endpoint URL and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span>

<span data-ttu-id="a4a09-162">In Azure Portal Hallo, navigeer tooyour Azure DB die Cosmos-account en klik op **sleutels**.</span><span class="sxs-lookup"><span data-stu-id="a4a09-162">In hello Azure Portal, navigate tooyour Azure Cosmos DB account, and then click **Keys**.</span></span>

<span data-ttu-id="a4a09-163">Hallo URI van de portal Hallo Kopieer en plak deze in `<your endpoint URL>` in het bestand program.cs Hallo.</span><span class="sxs-lookup"><span data-stu-id="a4a09-163">Copy hello URI from hello portal and paste it into `<your endpoint URL>` in hello program.cs file.</span></span> <span data-ttu-id="a4a09-164">Vervolgens kopiëren primaire sleutel van de portal Hallo Hallo en plak deze in `<your primary key>`.</span><span class="sxs-lookup"><span data-stu-id="a4a09-164">Then copy hello PRIMARY KEY from hello portal and paste it into `<your primary key>`.</span></span>

![Schermopname van hello Azure Portal gebruikt door Hallo NoSQL-zelfstudie toocreate een C#-consoletoepassing.][keys]

<span data-ttu-id="a4a09-167">Vervolgens we toepassing hello beginnen met het maken van een nieuw exemplaar van Hallo **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="a4a09-167">Next, we'll start hello application by creating a new instance of hello **DocumentClient**.</span></span>

<span data-ttu-id="a4a09-168">Hieronder Hallo **Main** methode toevoegen van nieuwe asynchrone taak aangeroepen **GetStartedDemo**, die wordt een exemplaar van onze nieuwe **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="a4a09-168">Below hello **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span></span>

    static void Main(string[] args)
    {
    }

    // ADD THIS PART tooYOUR CODE
    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);
    }

<span data-ttu-id="a4a09-169">Voeg Hallo volgende code toorun uw asynchrone taak van uw **Main** methode.</span><span class="sxs-lookup"><span data-stu-id="a4a09-169">Add hello following code toorun your asynchronous task from your **Main** method.</span></span> <span data-ttu-id="a4a09-170">Hallo **Main** methode wordt onderschept uitzonderingen en toohello console geschreven.</span><span class="sxs-lookup"><span data-stu-id="a4a09-170">hello **Main** method will catch exceptions and write them toohello console.</span></span>

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

<span data-ttu-id="a4a09-171">Druk op **F5** toorun uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="a4a09-171">Press **F5** toorun your application.</span></span> <span data-ttu-id="a4a09-172">Hallo-console-venster uitvoer geeft het Hallo-bericht `End of demo, press any key tooexit.` bevestigen dat Hallo verbinding is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a4a09-172">hello console window output displays hello message `End of demo, press any key tooexit.` confirming that hello connection was made.</span></span>  <span data-ttu-id="a4a09-173">U kunt vervolgens Hallo-consolevenster sluiten.</span><span class="sxs-lookup"><span data-stu-id="a4a09-173">You can then close hello console window.</span></span> 

<span data-ttu-id="a4a09-174">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="a4a09-174">Congratulations!</span></span> <span data-ttu-id="a4a09-175">U hebt verbinding gemaakt tooan Azure DB die Cosmos-account, laten we nu eens kijken werken met Azure DB die Cosmos-resources.</span><span class="sxs-lookup"><span data-stu-id="a4a09-175">You have successfully connected tooan Azure Cosmos DB account, let's now take a look at working with Azure Cosmos DB resources.</span></span>  

## <a name="step-4-create-a-database"></a><span data-ttu-id="a4a09-176">Stap 4: een database maken</span><span class="sxs-lookup"><span data-stu-id="a4a09-176">Step 4: Create a database</span></span>
<span data-ttu-id="a4a09-177">Voordat u Hallo-code voor het maken van een database toevoegt, Voeg een Help-methode voor het schrijven van toohello-console.</span><span class="sxs-lookup"><span data-stu-id="a4a09-177">Before you add hello code for creating a database, add a helper method for writing toohello console.</span></span>

<span data-ttu-id="a4a09-178">Kopieer en plak Hallo **WriteToConsoleAndPromptToContinue** methode na Hallo **GetStartedDemo** methode.</span><span class="sxs-lookup"><span data-stu-id="a4a09-178">Copy and paste hello **WriteToConsoleAndPromptToContinue** method after hello **GetStartedDemo** method.</span></span>

    // ADD THIS PART tooYOUR CODE
    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
            Console.WriteLine(format, args);
            Console.WriteLine("Press any key toocontinue ...");
            Console.ReadKey();
    }

<span data-ttu-id="a4a09-179">Uw Azure-Cosmos-DB [database](documentdb-resources.md#databases) kunnen worden gemaakt met behulp van Hallo [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) methode Hallo **DocumentClient** klasse.</span><span class="sxs-lookup"><span data-stu-id="a4a09-179">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using hello [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="a4a09-180">Een database is een logische container voor documentopslag, gepartitioneerd in verzamelingen JSON Hallo.</span><span class="sxs-lookup"><span data-stu-id="a4a09-180">A database is hello logical container of JSON document storage partitioned across collections.</span></span>

<span data-ttu-id="a4a09-181">Kopiëren en plakken Hallo volgende code tooyour **GetStartedDemo** methode na het Hallo-client maken.</span><span class="sxs-lookup"><span data-stu-id="a4a09-181">Copy and paste hello following code tooyour **GetStartedDemo** method after hello client creation.</span></span> <span data-ttu-id="a4a09-182">Hiermee maakt u een database met de naam *FamilyDB*.</span><span class="sxs-lookup"><span data-stu-id="a4a09-182">This will create a database named *FamilyDB*.</span></span>

    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        // ADD THIS PART tooYOUR CODE
        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

<span data-ttu-id="a4a09-183">Druk op **F5** toorun uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="a4a09-183">Press **F5** toorun your application.</span></span>

<span data-ttu-id="a4a09-184">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="a4a09-184">Congratulations!</span></span> <span data-ttu-id="a4a09-185">U hebt een Azure Cosmos DB-database gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a4a09-185">You have successfully created an Azure Cosmos DB database.</span></span>  

## <span data-ttu-id="a4a09-186"><a id="CreateColl"></a>Stap 5: een verzameling maken</span><span class="sxs-lookup"><span data-stu-id="a4a09-186"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="a4a09-187">Met **CreateDocumentCollectionIfNotExistsAsync** maakt u een nieuwe verzameling met gereserveerde doorvoer, wat gevolgen heeft voor de kosten.</span><span class="sxs-lookup"><span data-stu-id="a4a09-187">**CreateDocumentCollectionIfNotExistsAsync** will create a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="a4a09-188">Zie onze [pagina met prijzen](https://azure.microsoft.com/pricing/details/cosmos-db/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a4a09-188">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="a4a09-189">Een [verzameling](documentdb-resources.md#collections) kunnen worden gemaakt met behulp van Hallo [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) methode Hallo **DocumentClient** klasse.</span><span class="sxs-lookup"><span data-stu-id="a4a09-189">A [collection](documentdb-resources.md#collections) can be created by using hello [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="a4a09-190">Een verzameling is een container van JSON-documenten en de bijbehorende JavaScript-toepassingslogica.</span><span class="sxs-lookup"><span data-stu-id="a4a09-190">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="a4a09-191">Kopiëren en plakken Hallo volgende code tooyour **GetStartedDemo** methode na het Hallo-database maken.</span><span class="sxs-lookup"><span data-stu-id="a4a09-191">Copy and paste hello following code tooyour **GetStartedDemo** method after hello database creation.</span></span> <span data-ttu-id="a4a09-192">Hiermee maakt u een documentverzameling met de naam *FamilyCollection*.</span><span class="sxs-lookup"><span data-stu-id="a4a09-192">This will create a document collection named *FamilyCollection*.</span></span>

        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

        // ADD THIS PART tooYOUR CODE
         await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });

<span data-ttu-id="a4a09-193">Druk op **F5** toorun uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="a4a09-193">Press **F5** toorun your application.</span></span>

<span data-ttu-id="a4a09-194">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="a4a09-194">Congratulations!</span></span> <span data-ttu-id="a4a09-195">U hebt een Azure Cosmos DB-documentverzameling gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a4a09-195">You have successfully created an Azure Cosmos DB document collection.</span></span>  

## <span data-ttu-id="a4a09-196"><a id="CreateDoc"></a>Stap 6: JSON-documenten maken</span><span class="sxs-lookup"><span data-stu-id="a4a09-196"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="a4a09-197">Een [document](documentdb-resources.md#documents) kunnen worden gemaakt met behulp van Hallo [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) methode Hallo **DocumentClient** klasse.</span><span class="sxs-lookup"><span data-stu-id="a4a09-197">A [document](documentdb-resources.md#documents) can be created by using hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="a4a09-198">Documenten bestaan uit door gebruikers gedefinieerde (willekeurige) JSON-inhoud.</span><span class="sxs-lookup"><span data-stu-id="a4a09-198">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="a4a09-199">U kunt nu een of meer documenten invoegen.</span><span class="sxs-lookup"><span data-stu-id="a4a09-199">We can now insert one or more documents.</span></span> <span data-ttu-id="a4a09-200">Als u gegevens die u wilt toostore in de database al hebt, kunt u hello Azure Cosmos DB [hulpprogramma voor gegevensmigratie](import-data.md) tooimport Hallo gegevens in een database.</span><span class="sxs-lookup"><span data-stu-id="a4a09-200">If you already have data you'd like toostore in your database, you can use hello Azure Cosmos DB [Data Migration tool](import-data.md) tooimport hello data into a database.</span></span>

<span data-ttu-id="a4a09-201">We moeten eerst toocreate een **familie** klasse die objecten die zijn opgeslagen in Azure Cosmos DB in dit voorbeeld wordt aangegeven.</span><span class="sxs-lookup"><span data-stu-id="a4a09-201">First, we need toocreate a **Family** class that will represent objects stored within Azure Cosmos DB in this sample.</span></span> <span data-ttu-id="a4a09-202">Daarnaast moeten de subklassen **Parent**, **Child**, **Pet** en **Address** worden gemaakt die in de klasse **Family** worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a4a09-202">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span></span> <span data-ttu-id="a4a09-203">Houd er rekening mee dat de documenten een **id**-eigenschap moeten bevatten die in JSON is geserialiseerd als **id**.</span><span class="sxs-lookup"><span data-stu-id="a4a09-203">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> <span data-ttu-id="a4a09-204">Maak deze klassen door toe te voegen na interne onderliggende klassen na Hallo Hallo **GetStartedDemo** methode.</span><span class="sxs-lookup"><span data-stu-id="a4a09-204">Create these classes by adding hello following internal sub-classes after hello **GetStartedDemo** method.</span></span>

<span data-ttu-id="a4a09-205">Kopieer en plak Hallo **familie**, **bovenliggende**, **onderliggende**, **huisdier**, en **adres** klassen na Hallo **WriteToConsoleAndPromptToContinue** methode.</span><span class="sxs-lookup"><span data-stu-id="a4a09-205">Copy and paste hello **Family**, **Parent**, **Child**, **Pet**, and **Address** classes after hello **WriteToConsoleAndPromptToContinue** method.</span></span>

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

<span data-ttu-id="a4a09-206">Kopieer en plak Hallo **CreateFamilyDocumentIfNotExists** methode onder uw **adres** klasse.</span><span class="sxs-lookup"><span data-stu-id="a4a09-206">Copy and paste hello **CreateFamilyDocumentIfNotExists** method underneath your **Address** class.</span></span>

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

<span data-ttu-id="a4a09-207">En Voeg twee documenten, één voor Hallo Andersen Family en Hallo Wakefield Family.</span><span class="sxs-lookup"><span data-stu-id="a4a09-207">And insert two documents, one each for hello Andersen Family and hello Wakefield Family.</span></span>

<span data-ttu-id="a4a09-208">Kopiëren en plakken Hallo volgende code tooyour **GetStartedDemo** methode na het maken van een verzameling Hallo document.</span><span class="sxs-lookup"><span data-stu-id="a4a09-208">Copy and paste hello following code tooyour **GetStartedDemo** method after hello document collection creation.</span></span>

    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });
    
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });


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

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", andersenFamily);

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

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

<span data-ttu-id="a4a09-209">Druk op **F5** toorun uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="a4a09-209">Press **F5** toorun your application.</span></span>

<span data-ttu-id="a4a09-210">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="a4a09-210">Congratulations!</span></span> <span data-ttu-id="a4a09-211">U hebt twee Azure Cosmos DB-documenten gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a4a09-211">You have successfully created two Azure Cosmos DB documents.</span></span>  

![Diagram ter illustratie Hallo hiërarchische relatie tussen Hallo-account, onlinedatabase Hallo Hallo verzameling en Hallo documenten die worden gebruikt door Hallo NoSQL-zelfstudie toocreate een C#-consoletoepassing](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="a4a09-213"><a id="Query"></a>Stap 7: query's uitvoeren op Azure Cosmos DB-resources</span><span class="sxs-lookup"><span data-stu-id="a4a09-213"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="a4a09-214">Azure Cosmos DB biedt ondersteuning voor uitgebreide [query's](documentdb-sql-query.md) op de JSON-documenten die zijn opgeslagen in elke verzameling.</span><span class="sxs-lookup"><span data-stu-id="a4a09-214">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="a4a09-215">Hallo volgende voorbeeldcode bevat verschillende query's: met behulp van zowel SQL Azure Cosmos DB syntaxis als LINQ, die kunnen worden uitgevoerd op basis van documenten die wordt ingevoegd in de vorige stap Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="a4a09-215">hello following sample code shows various queries - using both Azure Cosmos DB SQL syntax as well as LINQ - that we can run against hello documents we inserted in hello previous step.</span></span>

<span data-ttu-id="a4a09-216">Kopieer en plak Hallo **ExecuteSimpleQuery** methode na uw **CreateFamilyDocumentIfNotExists** methode.</span><span class="sxs-lookup"><span data-stu-id="a4a09-216">Copy and paste hello **ExecuteSimpleQuery** method after your **CreateFamilyDocumentIfNotExists** method.</span></span>

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

<span data-ttu-id="a4a09-217">Kopiëren en plakken Hallo volgende code tooyour **GetStartedDemo** methode na het Hallo tweede document maken.</span><span class="sxs-lookup"><span data-stu-id="a4a09-217">Copy and paste hello following code tooyour **GetStartedDemo** method after hello second document creation.</span></span>

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    // ADD THIS PART tooYOUR CODE
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

<span data-ttu-id="a4a09-218">Druk op **F5** toorun uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="a4a09-218">Press **F5** toorun your application.</span></span>

<span data-ttu-id="a4a09-219">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="a4a09-219">Congratulations!</span></span> <span data-ttu-id="a4a09-220">U hebt een query uitgevoerd op een Azure Cosmos DB-verzameling.</span><span class="sxs-lookup"><span data-stu-id="a4a09-220">You have successfully queried against an Azure Cosmos DB collection.</span></span>

<span data-ttu-id="a4a09-221">Hallo volgende diagram illustreert hoe hello Azure Cosmos DB SQL-query syntaxis wordt aangeroepen voor Hallo verzameling die u hebt gemaakt en hello dezelfde logica toegepast toohello LINQ-query.</span><span class="sxs-lookup"><span data-stu-id="a4a09-221">hello following diagram illustrates how hello Azure Cosmos DB SQL query syntax is called against hello collection you created, and hello same logic applies toohello LINQ query as well.</span></span>

![Diagram ter illustratie van Hallo bereik en de betekenis van Hallo query die wordt gebruikt door Hallo NoSQL-zelfstudie toocreate een C#-consoletoepassing](./media/documentdb-get-started/nosql-tutorial-collection-documents.png)

<span data-ttu-id="a4a09-223">Hallo [FROM](documentdb-sql-query.md#FromClause) sleutelwoord is optioneel in Hallo query omdat Azure Cosmos DB-query's al één verzameling tooa binnen het bereik zijn.</span><span class="sxs-lookup"><span data-stu-id="a4a09-223">hello [FROM](documentdb-sql-query.md#FromClause) keyword is optional in hello query because Azure Cosmos DB queries are already scoped tooa single collection.</span></span> <span data-ttu-id="a4a09-224">Daarom kan FROM Families f worden ingewisseld door FROM root r, of een andere gewenste variabelenaam.</span><span class="sxs-lookup"><span data-stu-id="a4a09-224">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="a4a09-225">Azure Cosmos DB wordt afgeleid dat Families, root of Hallo variabelenaam u hebt gekozen, verwijzing Hallo huidige verzameling standaard.</span><span class="sxs-lookup"><span data-stu-id="a4a09-225">Azure Cosmos DB will infer that Families, root, or hello variable name you chose, reference hello current collection by default.</span></span>

## <span data-ttu-id="a4a09-226"><a id="ReplaceDocument"></a>Stap 8: JSON-document vervangen</span><span class="sxs-lookup"><span data-stu-id="a4a09-226"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="a4a09-227">Azure Cosmos DB biedt ondersteuning voor het vervangen van JSON-documenten.</span><span class="sxs-lookup"><span data-stu-id="a4a09-227">Azure Cosmos DB supports replacing JSON documents.</span></span>  

<span data-ttu-id="a4a09-228">Kopieer en plak Hallo **ReplaceFamilyDocument** methode na uw **ExecuteSimpleQuery** methode.</span><span class="sxs-lookup"><span data-stu-id="a4a09-228">Copy and paste hello **ReplaceFamilyDocument** method after your **ExecuteSimpleQuery** method.</span></span>

    // ADD THIS PART tooYOUR CODE
    private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
    {
         await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
         this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }

<span data-ttu-id="a4a09-229">Kopiëren en plakken Hallo volgende code tooyour **GetStartedDemo** methode na de queryuitvoering Hallo achter Hallo Hallo-methode.</span><span class="sxs-lookup"><span data-stu-id="a4a09-229">Copy and paste hello following code tooyour **GetStartedDemo** method after hello query execution, at hello end of hello method.</span></span> <span data-ttu-id="a4a09-230">Na het Hallo-document vervangen, Hallo wordt uitgevoerd dezelfde query opnieuw tooview Hallo gewijzigd document.</span><span class="sxs-lookup"><span data-stu-id="a4a09-230">After replacing hello document, this will run hello same query again tooview hello changed document.</span></span>

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    // ADD THIS PART tooYOUR CODE
    // Update hello Grade of hello Andersen Family child
    andersenFamily.Children[0].Grade = 6;

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

<span data-ttu-id="a4a09-231">Druk op **F5** toorun uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="a4a09-231">Press **F5** toorun your application.</span></span>

<span data-ttu-id="a4a09-232">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="a4a09-232">Congratulations!</span></span> <span data-ttu-id="a4a09-233">U hebt een Azure Cosmos DB-document vervangen.</span><span class="sxs-lookup"><span data-stu-id="a4a09-233">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="a4a09-234"><a id="DeleteDocument"></a>Stap 9: JSON-document verwijderen</span><span class="sxs-lookup"><span data-stu-id="a4a09-234"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="a4a09-235">Azure Cosmos DB biedt ondersteuning voor het verwijderen van JSON-documenten.</span><span class="sxs-lookup"><span data-stu-id="a4a09-235">Azure Cosmos DB supports deleting JSON documents.</span></span>  

<span data-ttu-id="a4a09-236">Kopieer en plak Hallo **DeleteFamilyDocument** methode na uw **ReplaceFamilyDocument** methode.</span><span class="sxs-lookup"><span data-stu-id="a4a09-236">Copy and paste hello **DeleteFamilyDocument** method after your **ReplaceFamilyDocument** method.</span></span>

    // ADD THIS PART tooYOUR CODE
    private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
    {
         await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
         Console.WriteLine("Deleted Family {0}", documentName);
    }

<span data-ttu-id="a4a09-237">Kopiëren en plakken Hallo volgende code tooyour **GetStartedDemo** methode na Hallo tweede queryuitvoering, achter Hallo Hallo-methode.</span><span class="sxs-lookup"><span data-stu-id="a4a09-237">Copy and paste hello following code tooyour **GetStartedDemo** method after hello second query execution, at hello end of hello method.</span></span>

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);
    
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");
    
    // ADD THIS PART tooCODE
    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

<span data-ttu-id="a4a09-238">Druk op **F5** toorun uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="a4a09-238">Press **F5** toorun your application.</span></span>

<span data-ttu-id="a4a09-239">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="a4a09-239">Congratulations!</span></span> <span data-ttu-id="a4a09-240">U hebt een Azure Cosmos DB-document verwijderd.</span><span class="sxs-lookup"><span data-stu-id="a4a09-240">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="a4a09-241"><a id="DeleteDatabase"></a>Stap 10: Hallo-database verwijderen</span><span class="sxs-lookup"><span data-stu-id="a4a09-241"><a id="DeleteDatabase"></a>Step 10: Delete hello database</span></span>
<span data-ttu-id="a4a09-242">Verwijderen Hallo gemaakt van de database wordt verwijderd Hallo-database en alle onderliggende resources (verzamelingen, documenten, enz.).</span><span class="sxs-lookup"><span data-stu-id="a4a09-242">Deleting hello created database will remove hello database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="a4a09-243">Kopiëren en plakken Hallo volgende code tooyour **GetStartedDemo** methode na Hallo document toodelete Hallo gehele database en alle onderliggende resources verwijderen.</span><span class="sxs-lookup"><span data-stu-id="a4a09-243">Copy and paste hello following code tooyour **GetStartedDemo** method after hello document delete toodelete hello entire database and all children resources.</span></span>

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

    // ADD THIS PART tooCODE
    // Clean up/delete hello database
    await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB"));

<span data-ttu-id="a4a09-244">Druk op **F5** toorun uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="a4a09-244">Press **F5** toorun your application.</span></span>

<span data-ttu-id="a4a09-245">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="a4a09-245">Congratulations!</span></span> <span data-ttu-id="a4a09-246">U hebt een Azure Cosmos DB-database verwijderd.</span><span class="sxs-lookup"><span data-stu-id="a4a09-246">You have successfully deleted an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="a4a09-247"><a id="Run"></a>Stap 11: uw C#-consoletoepassing volledig uitvoeren</span><span class="sxs-lookup"><span data-stu-id="a4a09-247"><a id="Run"></a>Step 11: Run your C# console application all together!</span></span>
<span data-ttu-id="a4a09-248">Druk op F5 in Visual Studio toobuild Hallo toepassing in de foutopsporingsmodus.</span><span class="sxs-lookup"><span data-stu-id="a4a09-248">Hit F5 in Visual Studio toobuild hello application in debug mode.</span></span>

<span data-ttu-id="a4a09-249">U ziet Hallo-uitvoer van uw getstarted-app in een consolevenster.</span><span class="sxs-lookup"><span data-stu-id="a4a09-249">You should see hello output of your get started app in a console window.</span></span> <span data-ttu-id="a4a09-250">Hallo-uitvoer ziet Hallo resultaten van Hallo query's die zijn toegevoegd en moet overeenkomen met de onderstaande Hallo voorbeeldtekst.</span><span class="sxs-lookup"><span data-stu-id="a4a09-250">hello output will show hello results of hello queries we added and should match hello example text below.</span></span>

    Created FamilyDB
    Press any key toocontinue ...
    Created FamilyCollection
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

<span data-ttu-id="a4a09-251">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="a4a09-251">Congratulations!</span></span> <span data-ttu-id="a4a09-252">U hebt Hallo-zelfstudie voltooid en beschikt nu over een werkende C#-consoletoepassing!</span><span class="sxs-lookup"><span data-stu-id="a4a09-252">You've completed hello tutorial and have a working C# console application!</span></span>

## <span data-ttu-id="a4a09-253"><a id="GetSolution"></a>Volledige Hallo-zelfstudieoplossing ophalen</span><span class="sxs-lookup"><span data-stu-id="a4a09-253"><a id="GetSolution"></a> Get hello complete tutorial solution</span></span>
<span data-ttu-id="a4a09-254">Als u geen tijd toocomplete Hallo in deze zelfstudie of alleen wilt toodownload Hallo codevoorbeelden stappen, kunt u het krijgen van [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="a4a09-254">If you didn't have time toocomplete hello steps in this tutorial, or just want toodownload hello code samples, you can get it from [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span></span> 

<span data-ttu-id="a4a09-255">toobuild hello GetStarted-oplossing, moet u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="a4a09-255">toobuild hello GetStarted solution, you will need hello following:</span></span>

* <span data-ttu-id="a4a09-256">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="a4a09-256">An active Azure account.</span></span> <span data-ttu-id="a4a09-257">Als u nog geen account hebt, kunt u zich aanmelden voor een [gratis account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="a4a09-257">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="a4a09-258">Een [Azure Cosmos DB account][cosmos-db-create-account].</span><span class="sxs-lookup"><span data-stu-id="a4a09-258">An [Azure Cosmos DB account][cosmos-db-create-account].</span></span>
* <span data-ttu-id="a4a09-259">Hallo [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) oplossing is beschikbaar op GitHub.</span><span class="sxs-lookup"><span data-stu-id="a4a09-259">hello [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="a4a09-260">toorestore hello verwijzingen toohello Azure Cosmos DB .NET SDK in Visual Studio met de rechtermuisknop op Hallo **GetStarted** oplossing in Solution Explorer en klik vervolgens op **NuGet-pakket herstellen inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="a4a09-260">toorestore hello references toohello Azure Cosmos DB .NET SDK in Visual Studio, right-click hello **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span></span> <span data-ttu-id="a4a09-261">In het bestand App.config Hallo werk vervolgens de waarden bij voor EndpointUrl en AuthorizationKey Hallo zoals beschreven in [tooan Azure DB die Cosmos-account koppelen](#Connect).</span><span class="sxs-lookup"><span data-stu-id="a4a09-261">Next, in hello App.config file, update hello EndpointUrl and AuthorizationKey values as described in [Connect tooan Azure Cosmos DB account](#Connect).</span></span>

<span data-ttu-id="a4a09-262">Dat is alles, bouw nu de oplossing. Succes!</span><span class="sxs-lookup"><span data-stu-id="a4a09-262">That's it, build it and you're on your way!</span></span>


## <a name="next-steps"></a><span data-ttu-id="a4a09-263">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a4a09-263">Next steps</span></span>
* <span data-ttu-id="a4a09-264">Wilt u een complexere ASP.NET MVC-zelfstudie?</span><span class="sxs-lookup"><span data-stu-id="a4a09-264">Want a more complex ASP.NET MVC tutorial?</span></span> <span data-ttu-id="a4a09-265">Zie [ASP.NET MVC-zelfstudie: Web ontwikkelen van toepassingen met Azure Cosmos DB](documentdb-dotnet-application.md).</span><span class="sxs-lookup"><span data-stu-id="a4a09-265">See [ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB](documentdb-dotnet-application.md).</span></span>
* <span data-ttu-id="a4a09-266">Wilt u tooperform schaal en prestaties testen met Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="a4a09-266">Want tooperform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="a4a09-267">Zie [prestaties en schaal testen met Azure Cosmos-DB](performance-testing.md)</span><span class="sxs-lookup"><span data-stu-id="a4a09-267">See [Performance and scale testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="a4a09-268">Meer informatie over hoe te[bewaken aanvragen, gebruik en opslag van Azure DB die Cosmos](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="a4a09-268">Learn how too[monitor Azure Cosmos DB requests, usage, and storage](monitor-accounts.md).</span></span>
* <span data-ttu-id="a4a09-269">Query's uitvoeren op onze voorbeeldgegevensset in Hallo [Queryspeelplaats](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="a4a09-269">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="a4a09-270">Zie toolearn meer informatie over Azure Cosmos DB [tooAzure Cosmos DB Welkom](https://docs.microsoft.com/azure/cosmos-db/introduction).</span><span class="sxs-lookup"><span data-stu-id="a4a09-270">toolearn more about Azure Cosmos DB, see [Welcome tooAzure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span></span>

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
[cosmos-db-create-account]: create-documentdb-dotnet.md#create-account
