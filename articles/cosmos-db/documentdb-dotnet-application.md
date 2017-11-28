---
title: 'ASP.NET MVC-zelfstudie voor Azure Cosmos DB: webtoepassingsontwikkeling | Microsoft Docs'
description: ASP.NET MVC zelfstudie toocreate een MVC-webtoepassing met Azure Cosmos DB. JSON opslaan en gegevens benaderen via een takenlijst-app die wordt gehost op Azure Websites - Stapsgewijze zelfstudie voor ASP NET MVC.
keywords: asp.net mvc-zelfstudie, ontwikkelen van webtoepassingen, mvc-webtoepassing, asp net mvc zelfstudie stapsgewijs
services: cosmos-db
documentationcenter: .net
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 52532d89-a40e-4fdf-9b38-aadb3a4cccbc
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/03/2017
ms.author: mimig
ms.openlocfilehash: dac2a9599b395524533e6fe14983789ff095331f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="89e5b-105"><a name="_Toc395809351"></a>ASP.NET MVC-zelfstudie: webtoepassingsontwikkeling met Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="89e5b-105"><a name="_Toc395809351"></a>ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="89e5b-106">.NET</span><span class="sxs-lookup"><span data-stu-id="89e5b-106">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="89e5b-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="89e5b-107">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="89e5b-108">Java</span><span class="sxs-lookup"><span data-stu-id="89e5b-108">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="89e5b-109">Python</span><span class="sxs-lookup"><span data-stu-id="89e5b-109">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="89e5b-110">toohighlight hoe efficiënt kunt u gebruikmaken van Azure DB die Cosmos toostore en JSON-documenten opvragen, in dit artikel biedt een end-to-end-procedure die laat zien u hoe een app met behulp van Azure DB die Cosmos toobuild.</span><span class="sxs-lookup"><span data-stu-id="89e5b-110">toohighlight how you can efficiently leverage Azure Cosmos DB toostore and query JSON documents, this article provides an end-to-end walk-through showing you how toobuild a todo app using Azure Cosmos DB.</span></span> <span data-ttu-id="89e5b-111">Hallo-taken worden opgeslagen als JSON-documenten in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="89e5b-111">hello tasks will be stored as JSON documents in Azure Cosmos DB.</span></span>

![Schermopname van het Hallo-takenlijst MVC-webtoepassing die is gemaakt met deze zelfstudie - stapsgewijze voor ASP NET MVC-zelfstudie](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-image01.png)

<span data-ttu-id="89e5b-113">Deze procedure ziet u hoe toouse hello Azure Cosmos DB service toostore en toegang tot gegevens uit een ASP.NET MVC-webtoepassing gehost op Azure.</span><span class="sxs-lookup"><span data-stu-id="89e5b-113">This walk-through shows you how toouse hello Azure Cosmos DB service toostore and access data from an ASP.NET MVC web application hosted on Azure.</span></span> <span data-ttu-id="89e5b-114">Als u zoekt naar een zelfstudie is alleen op Azure Cosmos DB gericht en niet hello ASP.NET MVC-onderdelen, Zie [een Azure Cosmos DB C#-consoletoepassing bouwen](documentdb-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="89e5b-114">If you're looking for a tutorial that focuses only on Azure Cosmos DB, and not hello ASP.NET MVC components, see [Build an Azure Cosmos DB C# console application](documentdb-get-started.md).</span></span>

> [!TIP]
> <span data-ttu-id="89e5b-115">Voor deze zelfstudie wordt ervan uitgegaan dat u ervaring hebt met ASP.NET MVC en Azure Websites.</span><span class="sxs-lookup"><span data-stu-id="89e5b-115">This tutorial assumes that you have prior experience using ASP.NET MVC and Azure Websites.</span></span> <span data-ttu-id="89e5b-116">Als u nieuwe tooASP.NET of Hallo [vereiste hulpprogramma's](#_Toc395637760), het is raadzaam Hallo volledige voorbeeldproject via downloaden [GitHub] [ GitHub] en het Hallo-instructies in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="89e5b-116">If you are new tooASP.NET or hello [prerequisite tools](#_Toc395637760), we recommend downloading hello complete sample project from [GitHub][GitHub] and following hello instructions in this sample.</span></span> <span data-ttu-id="89e5b-117">Zodra u klaar hebt, kunt u dit artikel toogain inzicht op Hallo code in de context van project Hallo Hallo bekijken.</span><span class="sxs-lookup"><span data-stu-id="89e5b-117">Once you have it built, you can review this article toogain insight on hello code in hello context of hello project.</span></span>
> 
> 

## <span data-ttu-id="89e5b-118"><a name="_Toc395637760"></a>Vereisten voor deze databasezelfstudie</span><span class="sxs-lookup"><span data-stu-id="89e5b-118"><a name="_Toc395637760"></a>Prerequisites for this database tutorial</span></span>
<span data-ttu-id="89e5b-119">Voordat u Hallo-instructies in dit artikel uitvoert, moet u ervoor zorgen dat u de volgende Hallo hebt:</span><span class="sxs-lookup"><span data-stu-id="89e5b-119">Before following hello instructions in this article, you should ensure that you have hello following:</span></span>

* <span data-ttu-id="89e5b-120">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="89e5b-120">An active Azure account.</span></span> <span data-ttu-id="89e5b-121">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="89e5b-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="89e5b-122">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="89e5b-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

    <span data-ttu-id="89e5b-123">OF</span><span class="sxs-lookup"><span data-stu-id="89e5b-123">OR</span></span>

    <span data-ttu-id="89e5b-124">Een lokale installatie van Hallo [Azure Cosmos DB Emulator](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="89e5b-124">A local installation of hello [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="89e5b-125">[Visual Studio 2017](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="89e5b-125">[Visual Studio 2017](http://www.visualstudio.com/).</span></span>  
* <span data-ttu-id="89e5b-126">Microsoft Azure SDK voor .NET voor Visual Studio 2017 beschikbaar via Hallo Visual Studio Installer.</span><span class="sxs-lookup"><span data-stu-id="89e5b-126">Microsoft Azure SDK for .NET for Visual Studio 2017, available through hello Visual Studio Installer.</span></span>

<span data-ttu-id="89e5b-127">Alle Hallo schermopnamen in dit artikel zijn gemaakt met behulp van Microsoft Visual Studio Community 2017.</span><span class="sxs-lookup"><span data-stu-id="89e5b-127">All hello screen shots in this article have been taken using Microsoft Visual Studio Community 2017.</span></span> <span data-ttu-id="89e5b-128">Als uw systeem is geconfigureerd met een andere versie is het mogelijk dat de schermen en opties niet volledig overeenkomen, maar als u voldoet aan Hallo bovenstaande vereisten moet deze oplossing werken.</span><span class="sxs-lookup"><span data-stu-id="89e5b-128">If your system is configured with a different version it is possible that your screens and options won't match entirely, but if you meet hello above prerequisites this solution should work.</span></span>

## <span data-ttu-id="89e5b-129"><a name="_Toc395637761"></a>Stap 1: een Azure Cosmos DB-databaseaccount maken</span><span class="sxs-lookup"><span data-stu-id="89e5b-129"><a name="_Toc395637761"></a>Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="89e5b-130">Begin met het maken van een Azure Cosmos DB-account.</span><span class="sxs-lookup"><span data-stu-id="89e5b-130">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="89e5b-131">Als u al een account voor SQL (DocumentDB) voor Azure Cosmos DB hebben of als u Azure Cosmos DB Emulator Hallo voor deze zelfstudie, kunt u overslaan te[Maak een nieuwe ASP.NET MVC-toepassing](#_Toc395637762).</span><span class="sxs-lookup"><span data-stu-id="89e5b-131">If you already have a SQL (DocumentDB) account for Azure Cosmos DB or if you are using hello Azure Cosmos DB Emulator for this tutorial, you can skip too[Create a new ASP.NET MVC application](#_Toc395637762).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

<br/>
<span data-ttu-id="89e5b-132">Nu u kunt zien via hoe toocreate een nieuwe ASP.NET MVC-toepassing van Hallo a t/m.</span><span class="sxs-lookup"><span data-stu-id="89e5b-132">We will now walk through how toocreate a new ASP.NET MVC application from hello ground-up.</span></span> 

## <span data-ttu-id="89e5b-133"><a name="_Toc395637762"></a>Stap 2: Een nieuwe ASP.NET MVC-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="89e5b-133"><a name="_Toc395637762"></a>Step 2: Create a new ASP.NET MVC application</span></span>

1. <span data-ttu-id="89e5b-134">In Visual Studio op Hallo **bestand** menu te verwijzen**nieuw**, en klik vervolgens op **Project**.</span><span class="sxs-lookup"><span data-stu-id="89e5b-134">In Visual Studio, on hello **File** menu, point too**New**, and then click **Project**.</span></span> <span data-ttu-id="89e5b-135">Hallo **nieuw Project** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="89e5b-135">hello **New Project** dialog box appears.</span></span>

2. <span data-ttu-id="89e5b-136">In Hallo **projecttypen** deelvenster Vouw **sjablonen**, **Visual C#**, **Web**, en selecteer vervolgens **ASP.NET-webtoepassing** .</span><span class="sxs-lookup"><span data-stu-id="89e5b-136">In hello **Project types** pane, expand **Templates**, **Visual C#**, **Web**, and then select **ASP.NET Web Application**.</span></span>

      ![Schermopname van het dialoogvenster Nieuw Project Hallo met Hallo projecttype voor ASP.NET-webtoepassing gemarkeerd](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-project-dialog.png)

3. <span data-ttu-id="89e5b-138">In Hallo **naam** vak, Hallo-typenaam van Hallo-project.</span><span class="sxs-lookup"><span data-stu-id="89e5b-138">In hello **Name** box, type hello name of hello project.</span></span> <span data-ttu-id="89e5b-139">Hallo-naam 'todo' maakt gebruik van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="89e5b-139">This tutorial uses hello name "todo".</span></span> <span data-ttu-id="89e5b-140">Als u toouse iets anders dan dit kiest, waar deze zelfstudie wordt gesproken over Hallo todo-naamruimte, moet u tooadjust Hallo opgegeven code voorbeelden toouse met de naam die uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="89e5b-140">If you choose toouse something other than this, then wherever this tutorial talks about hello todo namespace, you need tooadjust hello provided code samples toouse whatever you named your application.</span></span> 
4. <span data-ttu-id="89e5b-141">Klik op **Bladeren** toonavigate toohello map waar u wilt toocreate Hallo-project en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="89e5b-141">Click **Browse** toonavigate toohello folder where you would like toocreate hello project, and then click **OK**.</span></span>
   
      <span data-ttu-id="89e5b-142">Hallo **nieuwe ASP.NET-webtoepassing** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="89e5b-142">hello **New ASP.NET Web Application** dialog box appears.</span></span>
   
    ![Schermopname van dialoogvenster Hallo-nieuwe ASP.NET-webtoepassing met Hallo MVC-toepassingssjabloon gemarkeerd](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-MVC.png)
5. <span data-ttu-id="89e5b-144">Selecteer in het deelvenster met sjablonen Hallo **MVC**.</span><span class="sxs-lookup"><span data-stu-id="89e5b-144">In hello templates pane, select **MVC**.</span></span>

6. <span data-ttu-id="89e5b-145">Klik op **OK** en bijbehorende dingen rond steigers Hallo lege ASP.NET MVC-sjabloon doen in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="89e5b-145">Click **OK** and let Visual Studio do its thing around scaffolding hello empty ASP.NET MVC template.</span></span> 

          
7. <span data-ttu-id="89e5b-146">Nadat Visual Studio Hallo standaardtekst MVC-toepassing heeft gemaakt hebt u een lege ASP.NET-toepassing die u lokaal kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="89e5b-146">Once Visual Studio has finished creating hello boilerplate MVC application you have an empty ASP.NET application that you can run locally.</span></span>
   
    <span data-ttu-id="89e5b-147">We zullen uitgevoerd Hallo-project lokaal omdat ik ervoor dat we alle waargenomen Hallo ASP.NET 'Hallo wereld' hebt toepassing.</span><span class="sxs-lookup"><span data-stu-id="89e5b-147">We'll skip running hello project locally because I'm sure we've all seen hello ASP.NET "Hello World" application.</span></span> <span data-ttu-id="89e5b-148">We gaan rechte tooadding Azure Cosmos DB toothis project en onze toepassing bouwen.</span><span class="sxs-lookup"><span data-stu-id="89e5b-148">Let's go straight tooadding Azure Cosmos DB toothis project and building our application.</span></span>

## <span data-ttu-id="89e5b-149"><a name="_Toc395637767"></a>Stap 3: Azure Cosmos DB tooyour MVC-webproject toepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="89e5b-149"><a name="_Toc395637767"></a>Step 3: Add Azure Cosmos DB tooyour MVC web application project</span></span>
<span data-ttu-id="89e5b-150">Nu dat we de meeste Hallo ASP.NET MVC Loodgieterswerk die we nodig hebben voor deze oplossing hebben, krijgen we toohello Werkelijke doel van deze zelfstudie, Azure Cosmos DB tooour MVC-webtoepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="89e5b-150">Now that we have most of hello ASP.NET MVC plumbing that we need for this solution, let's get toohello real purpose of this tutorial, adding Azure Cosmos DB tooour MVC web application.</span></span>

1. <span data-ttu-id="89e5b-151">Hello Azure Cosmos DB .NET SDK wordt verpakt en gedistribueerd als een NuGet-pakket.</span><span class="sxs-lookup"><span data-stu-id="89e5b-151">hello Azure Cosmos DB .NET SDK is packaged and distributed as a NuGet package.</span></span> <span data-ttu-id="89e5b-152">tooget Hallo NuGet-pakket in Visual Studio, Hallo NuGet-Pakketbeheer in Visual Studio gebruiken door met de rechtermuisknop op het Hallo-project in **Solution Explorer** en vervolgens te klikken op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="89e5b-152">tooget hello NuGet package in Visual Studio, use hello NuGet package manager in Visual Studio by right-clicking on hello project in **Solution Explorer** and then clicking **Manage NuGet Packages**.</span></span>
   
    ![Schermopname van het Hallo met de rechtermuisknop op de opties voor het Hallo-webtoepassingsproject in Solution Explorer, met NuGet-pakketten beheren gemarkeerd.](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-manage-nuget.png)
   
    <span data-ttu-id="89e5b-154">Hallo **NuGet-pakketten beheren** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="89e5b-154">hello **Manage NuGet Packages** dialog box appears.</span></span>
2. <span data-ttu-id="89e5b-155">In Hallo NuGet **Bladeren** in het vak ***Azure DocumentDB***.</span><span class="sxs-lookup"><span data-stu-id="89e5b-155">In hello NuGet **Browse** box, type ***Azure DocumentDB***.</span></span> <span data-ttu-id="89e5b-156">(Hallo pakketnaam is geen bijgewerkte tooAzure Cosmos DB.)</span><span class="sxs-lookup"><span data-stu-id="89e5b-156">(hello package name has not been updated tooAzure Cosmos DB.)</span></span>
   
    <span data-ttu-id="89e5b-157">Installeren in Hallo resultaten Hallo **Microsoft.Azure.DocumentDB door Microsoft** pakket.</span><span class="sxs-lookup"><span data-stu-id="89e5b-157">From hello results, install hello **Microsoft.Azure.DocumentDB by Microsoft** package.</span></span> <span data-ttu-id="89e5b-158">Dit zal downloaden en installeren hello Azure Cosmos DB pakket, evenals alle afhankelijkheden, zoals Newtonsoft.Json.</span><span class="sxs-lookup"><span data-stu-id="89e5b-158">This will download and install hello Azure Cosmos DB package as well as all dependencies, such as Newtonsoft.Json.</span></span> <span data-ttu-id="89e5b-159">Klik op **OK** in Hallo **Preview** venster en **ik ga akkoord** in Hallo **licentie acceptatie** venster toocomplete Hallo installeren.</span><span class="sxs-lookup"><span data-stu-id="89e5b-159">Click **OK** in hello **Preview** window, and **I Accept** in hello **License Acceptance** window toocomplete hello install.</span></span>
   
    ![Schermopname van het venster NuGet-pakketten beheren hello, hello Microsoft Azure DocumentDB-clientbibliotheek gemarkeerd](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-install-nuget.png)
   
      <span data-ttu-id="89e5b-161">U kunt ook Hallo Package Manager Console tooinstall Hallo pakket gebruiken.</span><span class="sxs-lookup"><span data-stu-id="89e5b-161">Alternatively you can use hello Package Manager Console tooinstall hello package.</span></span> <span data-ttu-id="89e5b-162">toodo in dat geval op Hallo **extra** menu, klikt u op **NuGet Package Manager**, en klik vervolgens op **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="89e5b-162">toodo so, on hello **Tools** menu, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span> <span data-ttu-id="89e5b-163">Hallo opdrachtprompt, typt u Hallo volgende.</span><span class="sxs-lookup"><span data-stu-id="89e5b-163">At hello prompt, type hello following.</span></span>
   
        Install-Package Microsoft.Azure.DocumentDB
        
3. <span data-ttu-id="89e5b-164">Nadat Hallo-pakket is geïnstalleerd, ziet uw Visual Studio-oplossing Hallo volgende met twee nieuwe verwijzingen Microsoft.Azure.Documents.Client en Newtonsoft.Json.</span><span class="sxs-lookup"><span data-stu-id="89e5b-164">Once hello package is installed, your Visual Studio solution should resemble hello following with two new references added, Microsoft.Azure.Documents.Client and Newtonsoft.Json.</span></span>
   
    ![Schermopname van de twee verwijzingen Hallo toegevoegd toohello JSON-gegevensproject in Solution Explorer](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-added-references.png)

## <span data-ttu-id="89e5b-166"><a name="_Toc395637763"></a>Stap 4: Hallo ASP.NET MVC-toepassing instellen</span><span class="sxs-lookup"><span data-stu-id="89e5b-166"><a name="_Toc395637763"></a>Step 4: Set up hello ASP.NET MVC application</span></span>
<span data-ttu-id="89e5b-167">Nu gaan we Hallo modellen, weergaven en controllers toothis MVC-toepassing toevoegen:</span><span class="sxs-lookup"><span data-stu-id="89e5b-167">Now let's add hello models, views, and controllers toothis MVC application:</span></span>

* <span data-ttu-id="89e5b-168">[Een model toevoegen](#_Toc395637764).</span><span class="sxs-lookup"><span data-stu-id="89e5b-168">[Add a model](#_Toc395637764).</span></span>
* <span data-ttu-id="89e5b-169">[Een controller toevoegen](#_Toc395637765).</span><span class="sxs-lookup"><span data-stu-id="89e5b-169">[Add a controller](#_Toc395637765).</span></span>
* <span data-ttu-id="89e5b-170">[Weergaven toevoegen](#_Toc395637766).</span><span class="sxs-lookup"><span data-stu-id="89e5b-170">[Add views](#_Toc395637766).</span></span>

### <span data-ttu-id="89e5b-171"><a name="_Toc395637764"></a>Een JSON-gegevensmodel toevoegen</span><span class="sxs-lookup"><span data-stu-id="89e5b-171"><a name="_Toc395637764"></a>Add a JSON data model</span></span>
<span data-ttu-id="89e5b-172">Laten we beginnen met het maken van Hallo **M** in MVC, Hallo model.</span><span class="sxs-lookup"><span data-stu-id="89e5b-172">Let's begin by creating hello **M** in MVC, hello model.</span></span> 

1. <span data-ttu-id="89e5b-173">In **Solution Explorer**, klik met de rechtermuisknop Hallo **modellen** map, klikt u op **toevoegen**, en klik vervolgens op **klasse**.</span><span class="sxs-lookup"><span data-stu-id="89e5b-173">In **Solution Explorer**, right-click hello **Models** folder, click **Add**, and then click **Class**.</span></span>
   
      <span data-ttu-id="89e5b-174">Hallo **Add New Item** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="89e5b-174">hello **Add New Item** dialog box appears.</span></span>
2. <span data-ttu-id="89e5b-175">Geef een naam op voor uw nieuwe klasse **Item.cs** en klik op **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="89e5b-175">Name your new class **Item.cs** and click **Add**.</span></span> 
3. <span data-ttu-id="89e5b-176">In het nieuwe **Item.cs** bestand, Hallo volgende na Hallo laatste toevoegen *met de instructie*.</span><span class="sxs-lookup"><span data-stu-id="89e5b-176">In this new **Item.cs** file, add hello following after hello last *using statement*.</span></span>
   
        using Newtonsoft.Json;
4. <span data-ttu-id="89e5b-177">Vervang deze code nu</span><span class="sxs-lookup"><span data-stu-id="89e5b-177">Now replace this code</span></span> 
   
        public class Item
        {
        }
   
    <span data-ttu-id="89e5b-178">Hello code te volgen.</span><span class="sxs-lookup"><span data-stu-id="89e5b-178">with hello following code.</span></span>
   
        public class Item
        {
            [JsonProperty(PropertyName = "id")]
            public string Id { get; set; }
   
            [JsonProperty(PropertyName = "name")]
            public string Name { get; set; }
   
            [JsonProperty(PropertyName = "description")]
            public string Description { get; set; }
   
            [JsonProperty(PropertyName = "isComplete")]
            public bool Completed { get; set; }
        }
   
    <span data-ttu-id="89e5b-179">Alle gegevens in Azure DB die Cosmos is doorgegeven via de kabel Hallo en opgeslagen als JSON.</span><span class="sxs-lookup"><span data-stu-id="89e5b-179">All data in Azure Cosmos DB is passed over hello wire and stored as JSON.</span></span> <span data-ttu-id="89e5b-180">toocontrol hello manier uw objecten worden geserialiseerd/gedeserialiseerd door JSON.NET kunt u Hallo **JsonProperty** kenmerk, zoals wordt beschreven in Hallo **Item** klasse die we zojuist hebben gemaakt.</span><span class="sxs-lookup"><span data-stu-id="89e5b-180">toocontrol hello way your objects are serialized/deserialized by JSON.NET you can use hello **JsonProperty** attribute as demonstrated in hello **Item** class we just created.</span></span> <span data-ttu-id="89e5b-181">U geen **hebben** toodo dit maar wilt tooensure dat mijn eigenschappen naamgevingsregels van Hallo JSON camelCase volgen.</span><span class="sxs-lookup"><span data-stu-id="89e5b-181">You don't **have** toodo this but I want tooensure that my properties follow hello JSON camelCase naming conventions.</span></span> 
   
    <span data-ttu-id="89e5b-182">Niet alleen kunt u bepalen Hallo-indeling van de naam van de eigenschap Hallo wanneer deze worden opgeslagen in de JSON, maar u uw .NET-eigenschappen volledig wijzigen kunt zoals ik deed met Hallo **beschrijving** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="89e5b-182">Not only can you control hello format of hello property name when it goes into JSON, but you can entirely rename your .NET properties like I did with hello **Description** property.</span></span> 

### <span data-ttu-id="89e5b-183"><a name="_Toc395637765"></a>Een controller toevoegen</span><span class="sxs-lookup"><span data-stu-id="89e5b-183"><a name="_Toc395637765"></a>Add a controller</span></span>
<span data-ttu-id="89e5b-184">Dat zorgt voor Hallo **M**, nu gaan we maken Hallo **C** in MVC, een controllerklasse.</span><span class="sxs-lookup"><span data-stu-id="89e5b-184">That takes care of hello **M**, now let's create hello **C** in MVC, a controller class.</span></span>

1. <span data-ttu-id="89e5b-185">In **Solution Explorer**, klik met de rechtermuisknop Hallo **domeincontrollers** map, klikt u op **toevoegen**, en klik vervolgens op **Controller**.</span><span class="sxs-lookup"><span data-stu-id="89e5b-185">In **Solution Explorer**, right-click hello **Controllers** folder, click **Add**, and then click **Controller**.</span></span>
   
    <span data-ttu-id="89e5b-186">Hallo **Add Scaffold** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="89e5b-186">hello **Add Scaffold** dialog box appears.</span></span>
2. <span data-ttu-id="89e5b-187">Selecteer **MVC 5 Controller - Empty** (MVC 5-controller - Leeg) en klik vervolgens op **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="89e5b-187">Select **MVC 5 Controller - Empty** and then click **Add**.</span></span>
   
    ![Schermopname van dialoogvenster Hallo Add Scaffold met Hallo MVC 5 Controller - leeg optie gemarkeerd](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-controller-add-scaffold.png)
3. <span data-ttu-id="89e5b-189">Noem uw nieuwe controller **ItemController**.</span><span class="sxs-lookup"><span data-stu-id="89e5b-189">Name your new Controller, **ItemController.**</span></span>
   
    ![Schermopname van dialoogvenster Hallo-Controller toevoegen](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-controller.png)
   
    <span data-ttu-id="89e5b-191">Zodra het Hallo-bestand is gemaakt, uw Visual Studio-oplossing moet eruitzien als Hallo volgende met Hallo nieuwe bestand ItemController.cs in **Solution Explorer**.</span><span class="sxs-lookup"><span data-stu-id="89e5b-191">Once hello file is created, your Visual Studio solution should resemble hello following with hello new ItemController.cs file in **Solution Explorer**.</span></span> <span data-ttu-id="89e5b-192">Hallo nieuwe bestand Item.cs file eerder hebt gemaakt, wordt ook weergegeven.</span><span class="sxs-lookup"><span data-stu-id="89e5b-192">hello new Item.cs file created earlier is also shown.</span></span>
   
    ![Schermopname van Hallo Visual Studio-oplossing - Solution Explorer met het nieuwe bestand ItemController.cs hello en gemarkeerd](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-item-solution-explorer.png)
   
    <span data-ttu-id="89e5b-194">U kunt ItemController.cs sluiten, we je tooit later terugkomen.</span><span class="sxs-lookup"><span data-stu-id="89e5b-194">You can close ItemController.cs, we'll come back tooit later.</span></span> 

### <span data-ttu-id="89e5b-195"><a name="_Toc395637766"></a>Weergaven toevoegen</span><span class="sxs-lookup"><span data-stu-id="89e5b-195"><a name="_Toc395637766"></a>Add views</span></span>
<span data-ttu-id="89e5b-196">Nu gaan we maken Hallo **V** in MVC, Hallo weergaven:</span><span class="sxs-lookup"><span data-stu-id="89e5b-196">Now, let's create hello **V** in MVC, hello views:</span></span>

* <span data-ttu-id="89e5b-197">[Een weergave toevoegen voor een itemindex ](#AddItemIndexView).</span><span class="sxs-lookup"><span data-stu-id="89e5b-197">[Add an Item Index view](#AddItemIndexView).</span></span>
* <span data-ttu-id="89e5b-198">[Een weergave toevoegen voor nieuwe items](#AddNewIndexView).</span><span class="sxs-lookup"><span data-stu-id="89e5b-198">[Add a New Item view](#AddNewIndexView).</span></span>
* <span data-ttu-id="89e5b-199">[Een weergave toevoegen voor het bewerken van items](#_Toc395888515).</span><span class="sxs-lookup"><span data-stu-id="89e5b-199">[Add an Edit Item view](#_Toc395888515).</span></span>

#### <span data-ttu-id="89e5b-200"><a name="AddItemIndexView"></a>Een weergave toevoegen voor een itemindex</span><span class="sxs-lookup"><span data-stu-id="89e5b-200"><a name="AddItemIndexView"></a>Add an Item Index view</span></span>
1. <span data-ttu-id="89e5b-201">In **Solution Explorer**, vouw Hallo **weergaven** map, klik met de rechtermuisknop Hallo leeg **Item** map die Visual Studio voor u gemaakt bij het toevoegen van Hallo  **ItemController** Klik **toevoegen**, en klik vervolgens op **weergave**.</span><span class="sxs-lookup"><span data-stu-id="89e5b-201">In **Solution Explorer**, expand hello **Views**  folder, right-click hello empty **Item** folder that Visual Studio created for you when you added hello **ItemController** earlier, click **Add**, and then click **View**.</span></span>
   
    ![Schermopname van Solution Explorer toont Hallo Item map die Visual Studio hebt gemaakt met Hallo weergave toevoegen opdrachten gemarkeerd](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view.png)
2. <span data-ttu-id="89e5b-203">In Hallo **weergave toevoegen** dialoogvenster vak, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="89e5b-203">In hello **Add View** dialog box, do hello following:</span></span>
   
   * <span data-ttu-id="89e5b-204">In Hallo **weergavenaam** in het vak ***Index***.</span><span class="sxs-lookup"><span data-stu-id="89e5b-204">In hello **View name** box, type ***Index***.</span></span>
   * <span data-ttu-id="89e5b-205">In Hallo **sjabloon** de optie ***lijst***.</span><span class="sxs-lookup"><span data-stu-id="89e5b-205">In hello **Template** box, select ***List***.</span></span>
   * <span data-ttu-id="89e5b-206">In Hallo **Modelklasse** de optie ***Item (todo. Modellen)***.</span><span class="sxs-lookup"><span data-stu-id="89e5b-206">In hello **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="89e5b-207">Hallo indeling pagina Typ in ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="89e5b-207">In hello layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
     
   ![Schermopname van Hallo weergave toevoegen voor dialoogvenster scherm](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view-dialog.png)
3. <span data-ttu-id="89e5b-209">Zodra al deze waarden zijn ingesteld, klikt u op **Toevoegen** en wordt er een nieuwe sjabloonweergave in Visual Studio gemaakt.</span><span class="sxs-lookup"><span data-stu-id="89e5b-209">Once all these values are set, click **Add** and let Visual Studio create a new template view.</span></span> <span data-ttu-id="89e5b-210">Als deze is voltooid, wordt deze geopend Hallo cshtml-bestand dat is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="89e5b-210">Once it is done, it will open hello cshtml file  that was created.</span></span> <span data-ttu-id="89e5b-211">We kunnen dat bestand in Visual Studio kunt sluiten als we zullen tooit later terugkomen.</span><span class="sxs-lookup"><span data-stu-id="89e5b-211">We can close that file in Visual Studio as we will come back tooit later.</span></span>

#### <span data-ttu-id="89e5b-212"><a name="AddNewIndexView"></a>Een weergave toevoegen voor nieuwe items</span><span class="sxs-lookup"><span data-stu-id="89e5b-212"><a name="AddNewIndexView"></a>Add a New Item view</span></span>
<span data-ttu-id="89e5b-213">Vergelijkbare toohow gemaakt een **itemindex** weergave we gaan nu een nieuwe weergave voor het maken van nieuwe maken **Items**.</span><span class="sxs-lookup"><span data-stu-id="89e5b-213">Similar toohow we created an **Item Index** view, we will now create a new view for creating new **Items**.</span></span>

1. <span data-ttu-id="89e5b-214">In **Solution Explorer**, klik met de rechtermuisknop Hallo **Item** map opnieuw in en klikt u op **toevoegen**, en klik vervolgens op **weergave**.</span><span class="sxs-lookup"><span data-stu-id="89e5b-214">In **Solution Explorer**, right-click hello **Item** folder again, click **Add**, and then click **View**.</span></span>
2. <span data-ttu-id="89e5b-215">In Hallo **weergave toevoegen** dialoogvenster vak, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="89e5b-215">In hello **Add View** dialog box, do hello following:</span></span>
   
   * <span data-ttu-id="89e5b-216">In Hallo **weergavenaam** in het vak ***maken***.</span><span class="sxs-lookup"><span data-stu-id="89e5b-216">In hello **View name** box, type ***Create***.</span></span>
   * <span data-ttu-id="89e5b-217">In Hallo **sjabloon** de optie ***maken***.</span><span class="sxs-lookup"><span data-stu-id="89e5b-217">In hello **Template** box, select ***Create***.</span></span>
   * <span data-ttu-id="89e5b-218">In Hallo **Modelklasse** de optie ***Item (todo. Modellen)***.</span><span class="sxs-lookup"><span data-stu-id="89e5b-218">In hello **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="89e5b-219">Hallo indeling pagina Typ in ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="89e5b-219">In hello layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
   * <span data-ttu-id="89e5b-220">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="89e5b-220">Click **Add**.</span></span>
   
#### <span data-ttu-id="89e5b-221"><a name="_Toc395888515"></a>Een weergave toevoegen voor het bewerken van items</span><span class="sxs-lookup"><span data-stu-id="89e5b-221"><a name="_Toc395888515"></a>Add an Edit Item view</span></span>
<span data-ttu-id="89e5b-222">En voeg een weergave voor het bewerken van een **Item** in Hallo dezelfde manier als voorheen.</span><span class="sxs-lookup"><span data-stu-id="89e5b-222">And finally, add one last view for editing an **Item** in hello same way as before.</span></span>

1. <span data-ttu-id="89e5b-223">In **Solution Explorer**, klik met de rechtermuisknop Hallo **Item** map opnieuw in en klikt u op **toevoegen**, en klik vervolgens op **weergave**.</span><span class="sxs-lookup"><span data-stu-id="89e5b-223">In **Solution Explorer**, right-click hello **Item** folder again, click **Add**, and then click **View**.</span></span>
2. <span data-ttu-id="89e5b-224">In Hallo **weergave toevoegen** dialoogvenster vak, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="89e5b-224">In hello **Add View** dialog box, do hello following:</span></span>
   
   * <span data-ttu-id="89e5b-225">In Hallo **weergavenaam** in het vak ***bewerken***.</span><span class="sxs-lookup"><span data-stu-id="89e5b-225">In hello **View name** box, type ***Edit***.</span></span>
   * <span data-ttu-id="89e5b-226">In Hallo **sjabloon** de optie ***bewerken***.</span><span class="sxs-lookup"><span data-stu-id="89e5b-226">In hello **Template** box, select ***Edit***.</span></span>
   * <span data-ttu-id="89e5b-227">In Hallo **Modelklasse** de optie ***Item (todo. Modellen)***.</span><span class="sxs-lookup"><span data-stu-id="89e5b-227">In hello **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="89e5b-228">Hallo indeling pagina Typ in ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="89e5b-228">In hello layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
   * <span data-ttu-id="89e5b-229">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="89e5b-229">Click **Add**.</span></span>

<span data-ttu-id="89e5b-230">Zodra dit is gebeurd, sluit u alle Hallo cshtml-documenten in Visual Studio als we toothese weergaven later terug.</span><span class="sxs-lookup"><span data-stu-id="89e5b-230">Once this is done, close all hello cshtml documents in Visual Studio as we will return toothese views later.</span></span>

## <span data-ttu-id="89e5b-231"><a name="_Toc395637769"></a>Stap 5: Azure Cosmos DB fysiek aansluiten</span><span class="sxs-lookup"><span data-stu-id="89e5b-231"><a name="_Toc395637769"></a>Step 5: Wiring up Azure Cosmos DB</span></span>
<span data-ttu-id="89e5b-232">Nu dat Hallo MVC hebben voltooid is afgehandeld, nu gaan we tooadding Hallo code voor Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="89e5b-232">Now that hello standard MVC stuff is taken care of, let's turn tooadding hello code for Azure Cosmos DB.</span></span> 

<span data-ttu-id="89e5b-233">In deze sectie gaan we de code toohandle Hallo volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="89e5b-233">In this section, we'll add code toohandle hello following:</span></span>

* <span data-ttu-id="89e5b-234">[Vermelden van onvolledige items](#_Toc395637770).</span><span class="sxs-lookup"><span data-stu-id="89e5b-234">[Listing incomplete Items](#_Toc395637770).</span></span>
* <span data-ttu-id="89e5b-235">[Items toevoegen](#_Toc395637771).</span><span class="sxs-lookup"><span data-stu-id="89e5b-235">[Adding Items](#_Toc395637771).</span></span>
* <span data-ttu-id="89e5b-236">[Items bewerken](#_Toc395637772).</span><span class="sxs-lookup"><span data-stu-id="89e5b-236">[Editing Items](#_Toc395637772).</span></span>

### <span data-ttu-id="89e5b-237"><a name="_Toc395637770"></a>Onvolledige objecten in uw MVC-webtoepassing vermelden</span><span class="sxs-lookup"><span data-stu-id="89e5b-237"><a name="_Toc395637770"></a>Listing incomplete Items in your MVC web application</span></span>
<span data-ttu-id="89e5b-238">Hallo eerste ding toodo hier is een klasse toevoegen die alle Hallo logica tooconnect tooand gebruik Azure Cosmos DB bevat.</span><span class="sxs-lookup"><span data-stu-id="89e5b-238">hello first thing toodo here is add a class that contains all hello logic tooconnect tooand use Azure Cosmos DB.</span></span> <span data-ttu-id="89e5b-239">Voor deze zelfstudie voegen we alle logica tooa opslagplaatsklasse naam DocumentDBRepository.</span><span class="sxs-lookup"><span data-stu-id="89e5b-239">For this tutorial we'll encapsulate all this logic in tooa repository class called DocumentDBRepository.</span></span> 

1. <span data-ttu-id="89e5b-240">In **Solution Explorer**, met de rechtermuisknop op het Hallo-project, klik op **toevoegen**, en klik vervolgens op **klasse**.</span><span class="sxs-lookup"><span data-stu-id="89e5b-240">In **Solution Explorer**, right-click on hello project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="89e5b-241">Naam nieuwe klasse Hallo **DocumentDBRepository** en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="89e5b-241">Name hello new class **DocumentDBRepository** and click **Add**.</span></span>
2. <span data-ttu-id="89e5b-242">In nieuw gemaakte Hallo **DocumentDBRepository** klasse en voeg de volgende Hallo *using-instructies* hierboven Hallo *naamruimte* declaratie</span><span class="sxs-lookup"><span data-stu-id="89e5b-242">In hello newly created **DocumentDBRepository** class and add hello following *using statements* above hello *namespace* declaration</span></span>
   
        using Microsoft.Azure.Documents; 
        using Microsoft.Azure.Documents.Client; 
        using Microsoft.Azure.Documents.Linq; 
        using System.Configuration;
        using System.Linq.Expressions;
        using System.Threading.Tasks;
        using System.Net
        
    <span data-ttu-id="89e5b-243">Vervang deze code nu</span><span class="sxs-lookup"><span data-stu-id="89e5b-243">Now replace this code</span></span> 
   
        public class DocumentDBRepository
        {
        }
   
    <span data-ttu-id="89e5b-244">Hello code te volgen.</span><span class="sxs-lookup"><span data-stu-id="89e5b-244">with hello following code.</span></span>
   
        public static class DocumentDBRepository<T> where T : class
        {
            private static readonly string DatabaseId = ConfigurationManager.AppSettings["database"];
            private static readonly string CollectionId = ConfigurationManager.AppSettings["collection"];
            private static DocumentClient client;
   
            public static void Initialize()
            {
                client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);
                CreateDatabaseIfNotExistsAsync().Wait();
                CreateCollectionIfNotExistsAsync().Wait();
            }
   
            private static async Task CreateDatabaseIfNotExistsAsync()
            {
                try
                {
                    await client.ReadDatabaseAsync(UriFactory.CreateDatabaseUri(DatabaseId));
                }
                catch (DocumentClientException e)
                {
                    if (e.StatusCode == System.Net.HttpStatusCode.NotFound)
                    {
                        await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
                    }
                    else
                    {
                        throw;
                    }
                }
            }
   
            private static async Task CreateCollectionIfNotExistsAsync()
            {
                try
                {
                    await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId));
                }
                catch (DocumentClientException e)
                {
                    if (e.StatusCode == System.Net.HttpStatusCode.NotFound)
                    {
                        await client.CreateDocumentCollectionAsync(
                            UriFactory.CreateDatabaseUri(DatabaseId),
                            new DocumentCollection { Id = CollectionId },
                            new RequestOptions { OfferThroughput = 1000 });
                    }
                    else
                    {
                        throw;
                    }
                }
            }
        }
   
    
3. <span data-ttu-id="89e5b-245">We sommige waarden uit de configuratie van leest, zodat openen Hallo **Web.config** bestand van uw toepassing en voeg de volgende regels onder Hallo Hallo `<AppSettings>` sectie.</span><span class="sxs-lookup"><span data-stu-id="89e5b-245">We're reading some values from configuration, so open hello **Web.config** file of your application and add hello following lines under hello `<AppSettings>` section.</span></span>
   
        <add key="endpoint" value="enter hello URI from hello Keys blade of hello Azure Portal"/>
        <add key="authKey" value="enter hello PRIMARY KEY, or hello SECONDARY KEY, from hello Keys blade of hello Azure  Portal"/>
        <add key="database" value="ToDoList"/>
        <add key="collection" value="Items"/>
4. <span data-ttu-id="89e5b-246">Werk nu Hallo waarden voor *eindpunt* en *authKey* met behulp van de blade van de sleutels Hallo van hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="89e5b-246">Now, update hello values for *endpoint* and *authKey* using hello Keys blade of hello Azure Portal.</span></span> <span data-ttu-id="89e5b-247">Hallo gebruiken **URI** Hallo sleutels blade als Hallo-waarde van Hallo endpoint-instelling en gebruik Hallo **primaire sleutel**, of **secundaire sleutel** van de blade van Hallo sleutels als waarde Hallo Hallo authKey-instelling.</span><span class="sxs-lookup"><span data-stu-id="89e5b-247">Use hello **URI** from hello Keys blade as hello value of hello endpoint setting, and use hello **PRIMARY KEY**, or **SECONDARY KEY** from hello Keys blade as hello value of hello authKey setting.</span></span>

    <span data-ttu-id="89e5b-248">Dat zorgt voor de bekabeling van de opslagplaats hello Azure Cosmos DB, nu gaan we toepassingslogica toevoegen.</span><span class="sxs-lookup"><span data-stu-id="89e5b-248">That takes care of wiring up hello Azure Cosmos DB repository, now let's add our application logic.</span></span>

1. <span data-ttu-id="89e5b-249">Hallo willen eerst te beginnen we toobe kunnen toodo met een takenlijsttoepassing toodisplay Hallo onvolledige items is.</span><span class="sxs-lookup"><span data-stu-id="89e5b-249">hello first thing we want toobe able toodo with a todo list application is toodisplay hello incomplete items.</span></span>  <span data-ttu-id="89e5b-250">Kopieer en plak de volgende codefragment overal in Hallo Hallo **DocumentDBRepository** klasse.</span><span class="sxs-lookup"><span data-stu-id="89e5b-250">Copy and paste hello following code snippet anywhere within hello **DocumentDBRepository** class.</span></span>
   
        public static async Task<IEnumerable<T>> GetItemsAsync(Expression<Func<T, bool>> predicate)
        {
            IDocumentQuery<T> query = client.CreateDocumentQuery<T>(
                UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId))
                .Where(predicate)
                .AsDocumentQuery();
   
            List<T> results = new List<T>();
            while (query.HasMoreResults)
            {
                results.AddRange(await query.ExecuteNextAsync<T>());
            }
   
            return results;
        }
2. <span data-ttu-id="89e5b-251">Open Hallo **ItemController** we eerder hebt toegevoegd en voeg de volgende Hallo *using-instructies* boven de naamruimtedeclaratie Hallo.</span><span class="sxs-lookup"><span data-stu-id="89e5b-251">Open hello **ItemController** we added earlier and add hello following *using statements* above hello namespace declaration.</span></span>
   
        using System.Net;
        using System.Threading.Tasks;
        using todo.Models;
   
    <span data-ttu-id="89e5b-252">Als uw project niet de naam 'todo', moet u tooupdate met behulp van 'todo. Modellen'; tooreflect Hallo-naam van uw project.</span><span class="sxs-lookup"><span data-stu-id="89e5b-252">If your project is not named "todo", then you need tooupdate using "todo.Models"; tooreflect hello name of your project.</span></span>
   
    <span data-ttu-id="89e5b-253">Vervang deze code nu</span><span class="sxs-lookup"><span data-stu-id="89e5b-253">Now replace this code</span></span>
   
        //GET: Item
        public ActionResult Index()
        {
            return View();
        }
   
    <span data-ttu-id="89e5b-254">Hello code te volgen.</span><span class="sxs-lookup"><span data-stu-id="89e5b-254">with hello following code.</span></span>
   
        [ActionName("Index")]
        public async Task<ActionResult> IndexAsync()
        {
            var items = await DocumentDBRepository<Item>.GetItemsAsync(d => !d.Completed);
            return View(items);
        }
3. <span data-ttu-id="89e5b-255">Open **Global.asax.cs** en voeg Hallo volgende regel toohello **Application_Start** methode</span><span class="sxs-lookup"><span data-stu-id="89e5b-255">Open **Global.asax.cs** and add hello following line toohello **Application_Start** method</span></span> 
   
        DocumentDBRepository<todo.Models.Item>.Initialize();

<span data-ttu-id="89e5b-256">Op dit moment moet uw oplossing kunnen toobuild zonder fouten.</span><span class="sxs-lookup"><span data-stu-id="89e5b-256">At this point your solution should be able toobuild without any errors.</span></span>

<span data-ttu-id="89e5b-257">Als u Hallo toepassing nu hebt uitgevoerd, gaat u toohello **HomeController** en Hallo **Index** van die controller.</span><span class="sxs-lookup"><span data-stu-id="89e5b-257">If you ran hello application now, you would go toohello **HomeController** and hello **Index** view of that controller.</span></span> <span data-ttu-id="89e5b-258">Dit is het standaardgedrag Hallo voor MVC-sjabloonproject Hallo die we aan begin Hallo hebt gekozen, maar we willen dat niet!</span><span class="sxs-lookup"><span data-stu-id="89e5b-258">This is hello default behavior for hello MVC template project we chose at hello start but we don't want that!</span></span> <span data-ttu-id="89e5b-259">Laten we Hallo routering op deze MVC-toepassing tooalter dit gedrag wijzigen.</span><span class="sxs-lookup"><span data-stu-id="89e5b-259">Let's change hello routing on this MVC application tooalter this behavior.</span></span>

<span data-ttu-id="89e5b-260">Open ***App\_Start\RouteConfig.cs*** en zoek Hallo regel die begint met "standaardwaarden: ' en wijzigt u tooresemble hello te volgen.</span><span class="sxs-lookup"><span data-stu-id="89e5b-260">Open ***App\_Start\RouteConfig.cs*** and locate hello line starting with "defaults:" and change it tooresemble hello following.</span></span>

        defaults: new { controller = "Item", action = "Index", id = UrlParameter.Optional }

<span data-ttu-id="89e5b-261">Hiermee stelt ASP.NET MVC die u hebt een waarde niet opgegeven in Hallo URL toocontrol Hallo routeringsgedrag routeringsgedrag **Start**, gebruik **Item** als Hallo-controller en de gebruiker **Index** als Hallo weergave.</span><span class="sxs-lookup"><span data-stu-id="89e5b-261">This now tells ASP.NET MVC that if you have not specified a value in hello URL toocontrol hello routing behavior that instead of **Home**, use **Item** as hello controller and user **Index** as hello view.</span></span>

<span data-ttu-id="89e5b-262">Nu als u de toepassing hello uitvoert, wordt gebeld naar uw **ItemController** die wordt in de opslagplaatsklasse toohello aanroepen en Hallo GetItems methode tooreturn alle Hallo onvolledige items toohello **weergaven** \\ **Item**\\**Index** weergeven.</span><span class="sxs-lookup"><span data-stu-id="89e5b-262">Now if you run hello application, it will call into your **ItemController** which will call in toohello repository class and use hello GetItems method tooreturn all hello incomplete items toohello **Views**\\**Item**\\**Index** view.</span></span> 

<span data-ttu-id="89e5b-263">Als u dit project nu maakt en uitvoert, ziet u iets dat vergelijkbaar is met het volgende.</span><span class="sxs-lookup"><span data-stu-id="89e5b-263">If you build and run this project now, you should now see something that looks this.</span></span>    

![Schermopname van het Hallo takenlijstwebtoepassing gemaakt met deze databasezelfstudie](./media/documentdb-dotnet-application/build-and-run-the-project-now.png)

### <span data-ttu-id="89e5b-265"><a name="_Toc395637771"></a>Items toevoegen</span><span class="sxs-lookup"><span data-stu-id="89e5b-265"><a name="_Toc395637771"></a>Adding Items</span></span>
<span data-ttu-id="89e5b-266">Laten we enkele items aan de database zodat we hebben iets meer dan een leeg raster toolook op.</span><span class="sxs-lookup"><span data-stu-id="89e5b-266">Let's put some items into our database so we have something more than an empty grid toolook at.</span></span>

<span data-ttu-id="89e5b-267">Laten we de code te toevoegen Azure Cosmos DBRepository ItemController toopersist Hallo record in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="89e5b-267">Let's add some code too Azure Cosmos DBRepository and ItemController toopersist hello record in Azure Cosmos DB.</span></span>

1. <span data-ttu-id="89e5b-268">Hallo na methode tooyour toevoegen **DocumentDBRepository** klasse.</span><span class="sxs-lookup"><span data-stu-id="89e5b-268">Add hello following method tooyour **DocumentDBRepository** class.</span></span>
   
       public static async Task<Document> CreateItemAsync(T item)
       {
           return await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId), item);
       }
   
   <span data-ttu-id="89e5b-269">Deze methode wordt een tooit doorgegeven object gewoon en deze in Azure Cosmos DB zich blijft voordoen.</span><span class="sxs-lookup"><span data-stu-id="89e5b-269">This method simply takes an object passed tooit and persists it in Azure Cosmos DB.</span></span>
2. <span data-ttu-id="89e5b-270">Hallo ItemController.cs bestand openen en voeg Hallo volgende codefragment in Hallo-klasse.</span><span class="sxs-lookup"><span data-stu-id="89e5b-270">Open hello ItemController.cs file and add hello following code snippet within hello class.</span></span> <span data-ttu-id="89e5b-271">Dit is hoe weet ASP.NET MVC wat toodo voor Hallo **maken** in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="89e5b-271">This is how ASP.NET MVC knows what toodo for hello **Create** action.</span></span> <span data-ttu-id="89e5b-272">In dit geval gekoppelde alleen render Hallo Create.cshtml weergave eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="89e5b-272">In this case just render hello associated Create.cshtml view created earlier.</span></span>
   
        [ActionName("Create")]
        public async Task<ActionResult> CreateAsync()
        {
            return View();
        }
   
    <span data-ttu-id="89e5b-273">Nu moet u meer code in deze controller die Hallo inzending vanuit Hallo accepteert **maken** weergeven.</span><span class="sxs-lookup"><span data-stu-id="89e5b-273">We now need some more code in this controller that will accept hello submission from hello **Create** view.</span></span>
3. <span data-ttu-id="89e5b-274">Hallo volgende blok van code toohello klasse ItemController.cs waarmee ASP.NET MVC wat toodo met een form POST voor deze controller toevoegen.</span><span class="sxs-lookup"><span data-stu-id="89e5b-274">Add hello next block of code toohello ItemController.cs class that tells ASP.NET MVC what toodo with a form POST for this controller.</span></span>
   
        [HttpPost]
        [ActionName("Create")]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> CreateAsync([Bind(Include = "Id,Name,Description,Completed")] Item item)
        {
            if (ModelState.IsValid)
            {
                await DocumentDBRepository<Item>.CreateItemAsync(item);
                return RedirectToAction("Index");
            }
   
            return View(item);
        }
   
    <span data-ttu-id="89e5b-275">Deze code roept toohello DocumentDBRepository en Hallo CreateItemAsync methode toopersist Hallo nieuwe todo item toohello database gebruikt.</span><span class="sxs-lookup"><span data-stu-id="89e5b-275">This code calls in toohello DocumentDBRepository and uses hello CreateItemAsync method toopersist hello new todo item toohello database.</span></span> 
   
    <span data-ttu-id="89e5b-276">**Opmerking over beveiliging**: Hallo **ValidateAntiForgeryToken** kenmerk wordt gebruikt hier toohelp beveiligen voor deze toepassing tegen aanvallen van aanvraagvervalsing op meerdere sites.</span><span class="sxs-lookup"><span data-stu-id="89e5b-276">**Security Note**: hello **ValidateAntiForgeryToken** attribute is used here toohelp protect this application against cross-site request forgery attacks.</span></span> <span data-ttu-id="89e5b-277">Er is meer tooit alleen toe te voegen dit kenmerk, uw weergaven moeten toowork met dit anti-vervalsingstoken ook.</span><span class="sxs-lookup"><span data-stu-id="89e5b-277">There is more tooit than just adding this attribute, your views need toowork with this anti-forgery token as well.</span></span> <span data-ttu-id="89e5b-278">Voor meer informatie over het Hallo-onderwerp en voorbeelden van hoe tooimplement dit correct Zie [Cross-Site zo wordt voorkomen dat aanvragen vervalsing][Preventing Cross-Site Request Forgery].</span><span class="sxs-lookup"><span data-stu-id="89e5b-278">For more on hello subject, and examples of how tooimplement this correctly, please see [Preventing Cross-Site Request Forgery][Preventing Cross-Site Request Forgery].</span></span> <span data-ttu-id="89e5b-279">broncode op Hallo [GitHub] [ GitHub] beschikt over de volledige implementatie Hallo.</span><span class="sxs-lookup"><span data-stu-id="89e5b-279">hello source code provided on [GitHub][GitHub] has hello full implementation in place.</span></span>
   
    <span data-ttu-id="89e5b-280">**Opmerking over beveiliging**: We gebruiken ook Hallo **binden** -kenmerk op Hallo methode parameter toohelp beschermen tegen over-postingaanvallen.</span><span class="sxs-lookup"><span data-stu-id="89e5b-280">**Security Note**: We also use hello **Bind** attribute on hello method parameter toohelp protect against over-posting attacks.</span></span> <span data-ttu-id="89e5b-281">Zie [Eenvoudige CRUD-bewerkingen in ASP.NET MVC][Basic CRUD Operations in ASP.NET MVC] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="89e5b-281">For more details please see [Basic CRUD Operations in ASP.NET MVC][Basic CRUD Operations in ASP.NET MVC].</span></span>

<span data-ttu-id="89e5b-282">Hiermee is Hallo code vereist tooadd nieuwe Items tooour database.</span><span class="sxs-lookup"><span data-stu-id="89e5b-282">This concludes hello code required tooadd new Items tooour database.</span></span>

### <span data-ttu-id="89e5b-283"><a name="_Toc395637772"></a>Items bewerken</span><span class="sxs-lookup"><span data-stu-id="89e5b-283"><a name="_Toc395637772"></a>Editing Items</span></span>
<span data-ttu-id="89e5b-284">Er is een ding voor ons toodo en dat tooadd Hallo mogelijkheid tooedit **Items** in Hallo-database en toomark als voltooid.</span><span class="sxs-lookup"><span data-stu-id="89e5b-284">There is one last thing for us toodo, and that is tooadd hello ability tooedit **Items** in hello database and toomark them as complete.</span></span> <span data-ttu-id="89e5b-285">Hallo weergave voor bewerken is al toegevoegd toohello project, hoeft daarom alleen tooadd sommige code tooour controller en toohello **DocumentDBRepository** klasse opnieuw.</span><span class="sxs-lookup"><span data-stu-id="89e5b-285">hello view for editing was already added toohello project, so we just need tooadd some code tooour controller and toohello **DocumentDBRepository** class again.</span></span>

1. <span data-ttu-id="89e5b-286">Hallo na toohello toevoegen **DocumentDBRepository** klasse.</span><span class="sxs-lookup"><span data-stu-id="89e5b-286">Add hello following toohello **DocumentDBRepository** class.</span></span>
   
        public static async Task<Document> UpdateItemAsync(string id, T item)
        {
            return await client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(DatabaseId, CollectionId, id), item);
        }
   
        public static async Task<T> GetItemAsync(string id)
        {
            try
            {
                Document document = await client.ReadDocumentAsync(UriFactory.CreateDocumentUri(DatabaseId, CollectionId, id));
                return (T)(dynamic)document;
            }
            catch (DocumentClientException e)
            {
                if (e.StatusCode == HttpStatusCode.NotFound)
                {
                    return null;
                }
                else
                {
                    throw;
                }
            }
        }
   
    <span data-ttu-id="89e5b-287">eerste dag van deze methoden Hallo **GetItem** haalt u een Item uit Azure Cosmos-database die wordt doorgegeven back toohello **ItemController** en klik vervolgens op toohello **bewerken** weergeven.</span><span class="sxs-lookup"><span data-stu-id="89e5b-287">hello first of these methods, **GetItem** fetches an Item from Azure Cosmos DB which is passed back toohello **ItemController** and then on toohello **Edit** view.</span></span>
   
    <span data-ttu-id="89e5b-288">Hallo seconde van Hallo methoden die zojuist is toegevoegd vervangt Hallo **Document** in Azure Cosmos DB met Hallo-versie van Hallo **Document** doorgegeven vanuit Hallo **ItemController**.</span><span class="sxs-lookup"><span data-stu-id="89e5b-288">hello second of hello methods we just added replaces hello **Document** in Azure Cosmos DB with hello version of hello **Document** passed in from hello **ItemController**.</span></span>
2. <span data-ttu-id="89e5b-289">Hallo na toohello toevoegen **ItemController** klasse.</span><span class="sxs-lookup"><span data-stu-id="89e5b-289">Add hello following toohello **ItemController** class.</span></span>
   
        [HttpPost]
        [ActionName("Edit")]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> EditAsync([Bind(Include = "Id,Name,Description,Completed")] Item item)
        {
            if (ModelState.IsValid)
            {
                await DocumentDBRepository<Item>.UpdateItemAsync(item.Id, item);
                return RedirectToAction("Index");
            }
   
            return View(item);
        }
   
        [ActionName("Edit")]
        public async Task<ActionResult> EditAsync(string id)
        {
            if (id == null)
            {
                return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
            }
   
            Item item = await DocumentDBRepository<Item>.GetItemAsync(id);
            if (item == null)
            {
                return HttpNotFound();
            }
   
            return View(item);
        }
   
    <span data-ttu-id="89e5b-290">Hallo eerste methode verwerkt Hallo Http GET die plaatsvindt wanneer de gebruiker Hallo op Hallo **bewerken** koppeling van Hallo **Index** weergeven.</span><span class="sxs-lookup"><span data-stu-id="89e5b-290">hello first method handles hello Http GET that happens when hello user clicks on hello **Edit** link from hello **Index** view.</span></span> <span data-ttu-id="89e5b-291">Deze methode haalt een [ **Document** ](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) van Azure DB die Cosmos en geeft deze door toohello **bewerken** weergeven.</span><span class="sxs-lookup"><span data-stu-id="89e5b-291">This method fetches a [**Document**](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) from Azure Cosmos DB and passes it toohello **Edit** view.</span></span>
   
    <span data-ttu-id="89e5b-292">Hallo **bewerken** weergave voert een Http POST-toohello **IndexController**.</span><span class="sxs-lookup"><span data-stu-id="89e5b-292">hello **Edit** view will then do an Http POST toohello **IndexController**.</span></span> 
   
    <span data-ttu-id="89e5b-293">Hallo tweede methode we Hallo bijgewerkt object tooAzure Cosmos DB toobe doorgeven ingangen toegevoegd permanent in Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="89e5b-293">hello second method we added handles passing hello updated object tooAzure Cosmos DB toobe persisted in hello database.</span></span>

<span data-ttu-id="89e5b-294">Dit is alles dat is alles wat we onze toepassing toorun nodig, onvolledige lijst **Items**, nieuwe toevoegen **Items**, en bewerken **Items**.</span><span class="sxs-lookup"><span data-stu-id="89e5b-294">That's it, that is everything we need toorun our application, list incomplete **Items**, add new **Items**, and edit **Items**.</span></span>

## <span data-ttu-id="89e5b-295"><a name="_Toc395637773"></a>Stap 6: Hallo toepassing lokaal uitvoeren</span><span class="sxs-lookup"><span data-stu-id="89e5b-295"><a name="_Toc395637773"></a>Step 6: Run hello application locally</span></span>
<span data-ttu-id="89e5b-296">tootest hello toepassing op uw lokale machine Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="89e5b-296">tootest hello application on your local machine, do hello following:</span></span>

1. <span data-ttu-id="89e5b-297">Druk op F5 in Visual Studio toobuild Hallo toepassing in de foutopsporingsmodus.</span><span class="sxs-lookup"><span data-stu-id="89e5b-297">Hit F5 in Visual Studio toobuild hello application in debug mode.</span></span> <span data-ttu-id="89e5b-298">Het moet Hallo toepassing bouwen en een browser gestart met de Hallo lege rasterpagina dat we eerder hebben gezien:</span><span class="sxs-lookup"><span data-stu-id="89e5b-298">It should build hello application and launch a browser with hello empty grid page we saw before:</span></span>
   
    ![Schermopname van het Hallo takenlijstwebtoepassing gemaakt met deze databasezelfstudie](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item-a.png)
   
     
2. <span data-ttu-id="89e5b-300">Klik op Hallo **nieuw** koppelen en voeg waarden toohello **naam** en **beschrijving** velden.</span><span class="sxs-lookup"><span data-stu-id="89e5b-300">Click hello **Create New** link and add values toohello **Name** and **Description** fields.</span></span> <span data-ttu-id="89e5b-301">Hallo laat **voltooid** selectievakje uitgeschakeld anders Hallo nieuwe **Item** worden toegevoegd met een onvoltooide status en wordt niet weergegeven in de initiële lijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="89e5b-301">Leave hello **Completed** check box unselected otherwise hello new **Item** will be added in a completed state and will not appear on hello initial list.</span></span>
   
    ![Schermopname van het Hallo weergave maken](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-new-item.png)
3. <span data-ttu-id="89e5b-303">Klik op **maken** en u omgeleide back toohello **Index** weergeven en uw **Item** wordt weergegeven in de lijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="89e5b-303">Click **Create** and you are redirected back toohello **Index** view and your **Item** appears in hello list.</span></span>
   
    ![Schermopname van het Hallo weergave Index](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item.png)
   
    <span data-ttu-id="89e5b-305">Kunt u gratis tooadd enkele **Items** tooyour takenlijsten.</span><span class="sxs-lookup"><span data-stu-id="89e5b-305">Feel free tooadd a few more **Items** tooyour todo list.</span></span>
    
4. <span data-ttu-id="89e5b-306">Klik op **bewerken** volgende tooan **Item** op Hallo lijst en u zijn genomen toohello **bewerken** weergave waarin u een eigenschap van het object, met inbegrip van Hallo kunt bijwerken  **Voltooid** vlag.</span><span class="sxs-lookup"><span data-stu-id="89e5b-306">Click **Edit** next tooan **Item** on hello list and you are taken toohello **Edit** view where you can update any property of your object, including hello **Completed** flag.</span></span> <span data-ttu-id="89e5b-307">Als u Hallo markeert **Complete** markeert en op **opslaan**, Hallo **Item** wordt verwijderd uit de lijst Hallo met onvolledige taken.</span><span class="sxs-lookup"><span data-stu-id="89e5b-307">If you mark hello **Complete** flag and click **Save**, hello **Item** is removed from hello list of incomplete tasks.</span></span>
   
    ![Schermopname van het Hallo weergave Index met de selectievakje voltooid Hallo ingeschakeld](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-completed-item.png)
5. <span data-ttu-id="89e5b-309">Zodra u Hallo app hebt getest, drukt u op Ctrl + F5 toostop foutopsporing Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="89e5b-309">Once you've tested hello app, press Ctrl+F5 toostop debugging hello app.</span></span> <span data-ttu-id="89e5b-310">U bent klaar toodeploy!</span><span class="sxs-lookup"><span data-stu-id="89e5b-310">You're ready toodeploy!</span></span>

## <span data-ttu-id="89e5b-311"><a name="_Toc395637774"></a>Stap 7: Hallo toepassing tooAzure App Service implementeren</span><span class="sxs-lookup"><span data-stu-id="89e5b-311"><a name="_Toc395637774"></a>Step 7: Deploy hello application tooAzure App Service</span></span> 
<span data-ttu-id="89e5b-312">Nu dat u de volledige toepassing hello hebt gaan correct werkt met Azure Cosmos DB we toodeploy deze web-app tooAzure App Service.</span><span class="sxs-lookup"><span data-stu-id="89e5b-312">Now that you have hello complete application working correctly with Azure Cosmos DB we're going toodeploy this web app tooAzure App Service.</span></span>  

1. <span data-ttu-id="89e5b-313">toopublish alle van deze toepassing moet u toodo is met de rechtermuisknop op het Hallo-project in **Solution Explorer** en klik op **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="89e5b-313">toopublish this application all you need toodo is right-click on hello project in **Solution Explorer** and click **Publish**.</span></span>
   
    ![Schermopname van het Hallo optie publiceren in Solution Explorer](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish.png)

2. <span data-ttu-id="89e5b-315">In Hallo **publiceren** in het dialoogvenster klikt u op **Microsoft Azure App Service**, selecteer daarna **nieuw** toocreate een App Service-profiel, of klik op **selecteren Bestaande** toouse een bestaand profiel.</span><span class="sxs-lookup"><span data-stu-id="89e5b-315">In hello **Publish** dialog box, click **Microsoft Azure App Service**, then select **Create New** toocreate an App Service profile, or click **Select Existing** toouse an existing profile.</span></span>

    ![Het dialoogvenster Publish in Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish-to-existing.png)

3. <span data-ttu-id="89e5b-317">Als u een bestaand Azure App Service-profiel, voert u de abonnementsnaam van uw.</span><span class="sxs-lookup"><span data-stu-id="89e5b-317">If you have an existing Azure App Service profile, enter your subscription name.</span></span> <span data-ttu-id="89e5b-318">Gebruik Hallo **weergave** toosort door resourcegroep of resourcetype filteren en selecteer vervolgens uw Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="89e5b-318">Use hello **View** filter toosort by resource group or resource type, then select your Azure App Service.</span></span> 
   
    ![In het dialoogvenster App Service in Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-app-service.png)

4. <span data-ttu-id="89e5b-320">toocreate een nieuw Azure App Service-profiel, klikt u op **nieuw** in Hallo **publiceren** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="89e5b-320">toocreate a new Azure App Service profile, click **Create New** in hello **Publish** dialog box.</span></span> <span data-ttu-id="89e5b-321">In Hallo **Create App Service** dialoogvenster, Voer uw Web-App-naam en de juiste abonnement, de resourcegroep en de App Service-abonnement en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="89e5b-321">In hello **Create App Service** dialog, enter your Web App name and appropriate subscription, resource group, and App Service plan, then click **Create**.</span></span>

    ![Het dialoogvenster App Service maken in Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-app-service.png)

<span data-ttu-id="89e5b-323">Binnen een paar seconden zal Visual Studio publicatie van uw webtoepassing voltooien en een browser starten waarin u kunt zien uw werk in Azure wordt uitgevoerd!</span><span class="sxs-lookup"><span data-stu-id="89e5b-323">In a few seconds, Visual Studio will finish publishing your web application and launch a browser where you can see your handiwork running in Azure!</span></span>



## <span data-ttu-id="89e5b-324"><a name="_Toc395637775"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="89e5b-324"><a name="_Toc395637775"></a>Next steps</span></span>
<span data-ttu-id="89e5b-325">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="89e5b-325">Congratulations!</span></span> <span data-ttu-id="89e5b-326">U zojuist hebt gemaakt van uw eerste ASP.NET MVC-webtoepassing met Azure Cosmos DB en tooAzure gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="89e5b-326">You just built your first ASP.NET MVC web application using Azure Cosmos DB and published it tooAzure.</span></span> <span data-ttu-id="89e5b-327">Hallo broncode voor de volledige toepassing hello, met inbegrip van Hallo detail functionaliteit en verwijderen die niet zijn opgenomen in deze zelfstudie kan worden gedownload of gekloond van [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="89e5b-327">hello source code for hello complete application, including hello detail and delete functionality that were not included in this tutorial can be downloaded or cloned from [GitHub][GitHub].</span></span> <span data-ttu-id="89e5b-328">Dus als u geïnteresseerd bent in die app tooyour toe te voegen, halen Hallo code en voeg deze toothis app.</span><span class="sxs-lookup"><span data-stu-id="89e5b-328">So if you're interested in adding that tooyour app, grab hello code and add it toothis app.</span></span>

<span data-ttu-id="89e5b-329">Bekijk Hallo beschikbare API's in Hallo-tooadd aanvullende functionaliteit tooyour toepassing [Azure Cosmos DB .NET-bibliotheek](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) harte gratis toocontribute toohello Azure Cosmos DB .NET-bibliotheek op [GitHub] [GitHub].</span><span class="sxs-lookup"><span data-stu-id="89e5b-329">tooadd additional functionality tooyour application, review hello APIs available in hello [Azure Cosmos DB .NET Library](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) and feel free toocontribute toohello Azure Cosmos DB .NET Library on [GitHub][GitHub].</span></span> 

[\*]: https://microsoft.sharepoint.com/teams/DocDB/Shared%20Documents/Documentation/Docs.LatestVersions/PicExportError
[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Preventing Cross-Site Request Forgery]: http://go.microsoft.com/fwlink/?LinkID=517254
[Basic CRUD Operations in ASP.NET MVC]: http://go.microsoft.com/fwlink/?LinkId=317598
[GitHub]: https://github.com/Azure-Samples/documentdb-net-todo-app
