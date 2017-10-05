---
title: 'ASP.NET MVC-zelfstudie voor Azure Cosmos DB: webtoepassingsontwikkeling | Microsoft Docs'
description: Dit is een zelfstudie voor ASP.NET MVC om een MVC-webtoepassing met Azure Cosmos DB te maken. JSON opslaan en gegevens benaderen via een takenlijst-app die wordt gehost op Azure Websites - Stapsgewijze zelfstudie voor ASP NET MVC.
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
ms.openlocfilehash: 3f2950fe25feb8f3ee81cc0a79bf624f0ee33bd5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <span data-ttu-id="3adbc-105"><a name="_Toc395809351"></a>ASP.NET MVC-zelfstudie: webtoepassingsontwikkeling met Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="3adbc-105"><a name="_Toc395809351"></a>ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3adbc-106">.NET</span><span class="sxs-lookup"><span data-stu-id="3adbc-106">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="3adbc-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="3adbc-107">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="3adbc-108">Java</span><span class="sxs-lookup"><span data-stu-id="3adbc-108">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="3adbc-109">Python</span><span class="sxs-lookup"><span data-stu-id="3adbc-109">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="3adbc-110">Dit artikel biedt een end-to-end-overzicht waarin wordt getoond hoe u met Azure Cosmos DB een to-do-app kunt maken. Zo ziet u hoe u effectief kunt gebruikmaken van Azure Cosmos DB voor het opslaan van en uitvoeren van query's voor JSON-documenten.</span><span class="sxs-lookup"><span data-stu-id="3adbc-110">To highlight how you can efficiently leverage Azure Cosmos DB to store and query JSON documents, this article provides an end-to-end walk-through showing you how to build a todo app using Azure Cosmos DB.</span></span> <span data-ttu-id="3adbc-111">De taken worden opgeslagen als JSON-documenten in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3adbc-111">The tasks will be stored as JSON documents in Azure Cosmos DB.</span></span>

![Schermopname van de takenlijst MVC-webtoepassing die is gemaakt met deze zelfstudie - Stapsgewijze zelfstudie voor ASP NET MVC.](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-image01.png)

<span data-ttu-id="3adbc-113">Deze procedure ziet u hoe de Azure DB die Cosmos-service gebruiken voor het opslaan van en toegang tot gegevens uit een ASP.NET MVC-webtoepassing gehost op Azure.</span><span class="sxs-lookup"><span data-stu-id="3adbc-113">This walk-through shows you how to use the Azure Cosmos DB service to store and access data from an ASP.NET MVC web application hosted on Azure.</span></span> <span data-ttu-id="3adbc-114">Zie [Een Azure Cosmos DB C#-consoletoepassing bouwen](documentdb-get-started.md) als u een zelfstudie zoekt die volledig is gericht op Azure Cosmos DB en niet op de ASP.NET MVC-onderdelen.</span><span class="sxs-lookup"><span data-stu-id="3adbc-114">If you're looking for a tutorial that focuses only on Azure Cosmos DB, and not the ASP.NET MVC components, see [Build an Azure Cosmos DB C# console application](documentdb-get-started.md).</span></span>

> [!TIP]
> <span data-ttu-id="3adbc-115">Voor deze zelfstudie wordt ervan uitgegaan dat u ervaring hebt met ASP.NET MVC en Azure Websites.</span><span class="sxs-lookup"><span data-stu-id="3adbc-115">This tutorial assumes that you have prior experience using ASP.NET MVC and Azure Websites.</span></span> <span data-ttu-id="3adbc-116">Als u niet bekend met ASP.NET of de [vereiste hulpprogramma's](#_Toc395637760) bent, is het raadzaam het volledige voorbeeldproject via [GitHub][GitHub] te downloaden en de instructies in dit voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="3adbc-116">If you are new to ASP.NET or the [prerequisite tools](#_Toc395637760), we recommend downloading the complete sample project from [GitHub][GitHub] and following the instructions in this sample.</span></span> <span data-ttu-id="3adbc-117">Zodra u klaar bent, kunt u dit artikel lezen voor meer informatie over de code in de context van het project.</span><span class="sxs-lookup"><span data-stu-id="3adbc-117">Once you have it built, you can review this article to gain insight on the code in the context of the project.</span></span>
> 
> 

## <span data-ttu-id="3adbc-118"><a name="_Toc395637760"></a>Vereisten voor deze databasezelfstudie</span><span class="sxs-lookup"><span data-stu-id="3adbc-118"><a name="_Toc395637760"></a>Prerequisites for this database tutorial</span></span>
<span data-ttu-id="3adbc-119">Voordat u de instructies in dit artikel uitvoert, moet u beschikken over het volgende:</span><span class="sxs-lookup"><span data-stu-id="3adbc-119">Before following the instructions in this article, you should ensure that you have the following:</span></span>

* <span data-ttu-id="3adbc-120">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="3adbc-120">An active Azure account.</span></span> <span data-ttu-id="3adbc-121">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="3adbc-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="3adbc-122">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3adbc-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

    <span data-ttu-id="3adbc-123">OF</span><span class="sxs-lookup"><span data-stu-id="3adbc-123">OR</span></span>

    <span data-ttu-id="3adbc-124">Een lokale installatie van de [Azure Cosmos DB-emulator](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="3adbc-124">A local installation of the [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="3adbc-125">[Visual Studio 2017](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="3adbc-125">[Visual Studio 2017](http://www.visualstudio.com/).</span></span>  
* <span data-ttu-id="3adbc-126">Microsoft Azure SDK voor .NET voor Visual Studio 2017 beschikbaar via de Visual Studio Installer.</span><span class="sxs-lookup"><span data-stu-id="3adbc-126">Microsoft Azure SDK for .NET for Visual Studio 2017, available through the Visual Studio Installer.</span></span>

<span data-ttu-id="3adbc-127">Alle schermopnamen in dit artikel zijn gemaakt met behulp van Microsoft Visual Studio Community 2017.</span><span class="sxs-lookup"><span data-stu-id="3adbc-127">All the screen shots in this article have been taken using Microsoft Visual Studio Community 2017.</span></span> <span data-ttu-id="3adbc-128">Als uw systeem is geconfigureerd met een andere versie is het mogelijk dat de schermen en opties niet volledig overeenkomen, maar als u voldoet aan de bovenstaande vereisten moet deze oplossing werken.</span><span class="sxs-lookup"><span data-stu-id="3adbc-128">If your system is configured with a different version it is possible that your screens and options won't match entirely, but if you meet the above prerequisites this solution should work.</span></span>

## <span data-ttu-id="3adbc-129"><a name="_Toc395637761"></a>Stap 1: een Azure Cosmos DB-databaseaccount maken</span><span class="sxs-lookup"><span data-stu-id="3adbc-129"><a name="_Toc395637761"></a>Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="3adbc-130">Begin met het maken van een Azure Cosmos DB-account.</span><span class="sxs-lookup"><span data-stu-id="3adbc-130">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="3adbc-131">Als u al een account voor SQL (DocumentDB) voor Azure Cosmos DB of als u de Azure-Emulator Cosmos-database voor deze zelfstudie gebruikt, kunt u doorgaan met [Maak een nieuwe ASP.NET MVC-toepassing](#_Toc395637762).</span><span class="sxs-lookup"><span data-stu-id="3adbc-131">If you already have a SQL (DocumentDB) account for Azure Cosmos DB or if you are using the Azure Cosmos DB Emulator for this tutorial, you can skip to [Create a new ASP.NET MVC application](#_Toc395637762).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

<br/>
<span data-ttu-id="3adbc-132">U kunt nu zien hoe u een compleet nieuwe ASP.NET MVC-toepassing maakt.</span><span class="sxs-lookup"><span data-stu-id="3adbc-132">We will now walk through how to create a new ASP.NET MVC application from the ground-up.</span></span> 

## <span data-ttu-id="3adbc-133"><a name="_Toc395637762"></a>Stap 2: Een nieuwe ASP.NET MVC-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="3adbc-133"><a name="_Toc395637762"></a>Step 2: Create a new ASP.NET MVC application</span></span>

1. <span data-ttu-id="3adbc-134">Wijs in het menu **Bestand** van Visual Studio de optie **Nieuw** aan en klik vervolgens op **Project**.</span><span class="sxs-lookup"><span data-stu-id="3adbc-134">In Visual Studio, on the **File** menu, point to **New**, and then click **Project**.</span></span> <span data-ttu-id="3adbc-135">Het dialoogvenster **Nieuw project** wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3adbc-135">The **New Project** dialog box appears.</span></span>

2. <span data-ttu-id="3adbc-136">Vouw in het deelvenster **Projecttypen** achtereenvolgens **Sjablonen**, **Visual C#** en **Web** uit en selecteer vervolgens**ASP.NET-webtoepassing**.</span><span class="sxs-lookup"><span data-stu-id="3adbc-136">In the **Project types** pane, expand **Templates**, **Visual C#**, **Web**, and then select **ASP.NET Web Application**.</span></span>

      ![Schermopname van het dialoogvenster met daarin het projecttype ASP.NET-webtoepassing gemarkeerd](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-project-dialog.png)

3. <span data-ttu-id="3adbc-138">Typ in het vak **Naam** de naam van het project.</span><span class="sxs-lookup"><span data-stu-id="3adbc-138">In the **Name** box, type the name of the project.</span></span> <span data-ttu-id="3adbc-139">In deze zelfstudie wordt de naam 'todo' gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3adbc-139">This tutorial uses the name "todo".</span></span> <span data-ttu-id="3adbc-140">Als u een andere naam gebruikt, moet u waar in deze zelfstudie over de naamruimte todo wordt gesproken, de codevoorbeelden aanpassen met de naam die u voor uw toepassing gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3adbc-140">If you choose to use something other than this, then wherever this tutorial talks about the todo namespace, you need to adjust the provided code samples to use whatever you named your application.</span></span> 
4. <span data-ttu-id="3adbc-141">Klik op **Bladeren** om naar de map te navigeren waarin u het project wilt maken en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="3adbc-141">Click **Browse** to navigate to the folder where you would like to create the project, and then click **OK**.</span></span>
   
      <span data-ttu-id="3adbc-142">De **nieuwe ASP.NET-webtoepassing** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3adbc-142">The **New ASP.NET Web Application** dialog box appears.</span></span>
   
    ![Schermopname van het dialoogvenster Nieuw ASP.NET-webtoepassing met de MVC-toepassingssjabloon gemarkeerd](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-MVC.png)
5. <span data-ttu-id="3adbc-144">Selecteer in het deelvenster met sjablonen **MVC**.</span><span class="sxs-lookup"><span data-stu-id="3adbc-144">In the templates pane, select **MVC**.</span></span>

6. <span data-ttu-id="3adbc-145">Klik op **OK** om de scaffolding van de lege ASP.NET MVC-sjabloon aan Visual Studio over te laten.</span><span class="sxs-lookup"><span data-stu-id="3adbc-145">Click **OK** and let Visual Studio do its thing around scaffolding the empty ASP.NET MVC template.</span></span> 

          
7. <span data-ttu-id="3adbc-146">Zodra de Visual Studio de standaard MVC-toepassing heeft gemaakt, beschikt u over een lege ASP.NET-toepassing die u lokaal kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="3adbc-146">Once Visual Studio has finished creating the boilerplate MVC application you have an empty ASP.NET application that you can run locally.</span></span>
   
    <span data-ttu-id="3adbc-147">We zullen het project niet lokaal uitvoeren, aangezien iedereen waarschijnlijk wel bekend is met de ASP.NET-toepassing Hello World.</span><span class="sxs-lookup"><span data-stu-id="3adbc-147">We'll skip running the project locally because I'm sure we've all seen the ASP.NET "Hello World" application.</span></span> <span data-ttu-id="3adbc-148">U gaat meteen Azure Cosmos DB aan dit project toevoegen en uw toepassing bouwen.</span><span class="sxs-lookup"><span data-stu-id="3adbc-148">Let's go straight to adding Azure Cosmos DB to this project and building our application.</span></span>

## <span data-ttu-id="3adbc-149"><a name="_Toc395637767"></a>Stap 3: Azure Cosmos DB aan uw project met de MVC-webtoepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="3adbc-149"><a name="_Toc395637767"></a>Step 3: Add Azure Cosmos DB to your MVC web application project</span></span>
<span data-ttu-id="3adbc-150">Nu de meeste ASP.NET MVC-werkzaamheden voor deze oplossing zijn voltooid, kunt u zich richten op het werkelijke doel van deze zelfstudie, namelijk het toevoegen van Azure Cosmos DB aan de MVC-webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="3adbc-150">Now that we have most of the ASP.NET MVC plumbing that we need for this solution, let's get to the real purpose of this tutorial, adding Azure Cosmos DB to our MVC web application.</span></span>

1. <span data-ttu-id="3adbc-151">De Azure Cosmos DB .NET SDK wordt verpakt en gedistribueerd als een NuGet-pakket.</span><span class="sxs-lookup"><span data-stu-id="3adbc-151">The Azure Cosmos DB .NET SDK is packaged and distributed as a NuGet package.</span></span> <span data-ttu-id="3adbc-152">Als u het NuGet-pakket aan Visual Studio wilt toevoegen, gebruikt u NuGet-pakketbeheer in Visual Studio door in **Solution Explorer** met de rechtermuisknop op het project te klikken en vervolgens op **NuGet-pakketten beheren** te klikken.</span><span class="sxs-lookup"><span data-stu-id="3adbc-152">To get the NuGet package in Visual Studio, use the NuGet package manager in Visual Studio by right-clicking on the project in **Solution Explorer** and then clicking **Manage NuGet Packages**.</span></span>
   
    ![Schermopname van de opties voor klikken met de rechtermuisknop voor het webtoepassingsproject in Solution Explorer, met NuGet-pakketten beheren gemarkeerd.](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-manage-nuget.png)
   
    <span data-ttu-id="3adbc-154">Het dialoogvenster **NuGet-pakketten beheren** wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3adbc-154">The **Manage NuGet Packages** dialog box appears.</span></span>
2. <span data-ttu-id="3adbc-155">Typ in het NuGet-vak **Bladeren** ***Azure DocumentDB***.</span><span class="sxs-lookup"><span data-stu-id="3adbc-155">In the NuGet **Browse** box, type ***Azure DocumentDB***.</span></span> <span data-ttu-id="3adbc-156">(Naam van het pakket niet is bijgewerkt naar Azure Cosmos DB.)</span><span class="sxs-lookup"><span data-stu-id="3adbc-156">(The package name has not been updated to Azure Cosmos DB.)</span></span>
   
    <span data-ttu-id="3adbc-157">Installeren van de resultaten de **Microsoft.Azure.DocumentDB door Microsoft** pakket.</span><span class="sxs-lookup"><span data-stu-id="3adbc-157">From the results, install the **Microsoft.Azure.DocumentDB by Microsoft** package.</span></span> <span data-ttu-id="3adbc-158">Dit wordt download en installeer het pakket Azure Cosmos DB, evenals alle afhankelijkheden, zoals Newtonsoft.Json.</span><span class="sxs-lookup"><span data-stu-id="3adbc-158">This will download and install the Azure Cosmos DB package as well as all dependencies, such as Newtonsoft.Json.</span></span> <span data-ttu-id="3adbc-159">Klik op **OK** in het venster **Voorbeeld** en op **I Accept** (Ik ga akkoord) in het venster **License Acceptance** (Licentie accepteren) om de installatie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="3adbc-159">Click **OK** in the **Preview** window, and **I Accept** in the **License Acceptance** window to complete the install.</span></span>
   
    ![Schermopname van het venster NuGet-pakketten beheren met de Microsoft Azure DocumentDB-clientbibliotheek gemarkeerd](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-install-nuget.png)
   
      <span data-ttu-id="3adbc-161">U kunt eventueel ook de console voor Pakketbeheer gebruiken om het pakket te installeren.</span><span class="sxs-lookup"><span data-stu-id="3adbc-161">Alternatively you can use the Package Manager Console to install the package.</span></span> <span data-ttu-id="3adbc-162">Hiervoor klikt u in het menu **Extra** op **NuGet Package Manager** (NuGet-pakketbeheer) en vervolgens op **Package Manager Console** (Pakketbeheer-console).</span><span class="sxs-lookup"><span data-stu-id="3adbc-162">To do so, on the **Tools** menu, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span> <span data-ttu-id="3adbc-163">Typ achter de prompt het volgende.</span><span class="sxs-lookup"><span data-stu-id="3adbc-163">At the prompt, type the following.</span></span>
   
        Install-Package Microsoft.Azure.DocumentDB
        
3. <span data-ttu-id="3adbc-164">Nadat het pakket is geïnstalleerd, moet uw Visual Studio-oplossing er ongeveer als volgt uitzien, met de twee nieuwe verwijzingen Microsoft.Azure.Documents.Client en Newtonsoft.Json.</span><span class="sxs-lookup"><span data-stu-id="3adbc-164">Once the package is installed, your Visual Studio solution should resemble the following with two new references added, Microsoft.Azure.Documents.Client and Newtonsoft.Json.</span></span>
   
    ![Schermopname van de twee verwijzingen die zijn toegevoegd aan het JSON-gegevensproject in Solution Explorer](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-added-references.png)

## <span data-ttu-id="3adbc-166"><a name="_Toc395637763"></a>Stap 4: De ASP.NET MVC-toepassing instellen</span><span class="sxs-lookup"><span data-stu-id="3adbc-166"><a name="_Toc395637763"></a>Step 4: Set up the ASP.NET MVC application</span></span>
<span data-ttu-id="3adbc-167">U kunt nu de modellen, weergaven en controllers toevoegen aan deze MVC-toepassing:</span><span class="sxs-lookup"><span data-stu-id="3adbc-167">Now let's add the models, views, and controllers to this MVC application:</span></span>

* <span data-ttu-id="3adbc-168">[Een model toevoegen](#_Toc395637764).</span><span class="sxs-lookup"><span data-stu-id="3adbc-168">[Add a model](#_Toc395637764).</span></span>
* <span data-ttu-id="3adbc-169">[Een controller toevoegen](#_Toc395637765).</span><span class="sxs-lookup"><span data-stu-id="3adbc-169">[Add a controller](#_Toc395637765).</span></span>
* <span data-ttu-id="3adbc-170">[Weergaven toevoegen](#_Toc395637766).</span><span class="sxs-lookup"><span data-stu-id="3adbc-170">[Add views](#_Toc395637766).</span></span>

### <span data-ttu-id="3adbc-171"><a name="_Toc395637764"></a>Een JSON-gegevensmodel toevoegen</span><span class="sxs-lookup"><span data-stu-id="3adbc-171"><a name="_Toc395637764"></a>Add a JSON data model</span></span>
<span data-ttu-id="3adbc-172">Als eerste wordt de **M** in MVC gemaakt, het model.</span><span class="sxs-lookup"><span data-stu-id="3adbc-172">Let's begin by creating the **M** in MVC, the model.</span></span> 

1. <span data-ttu-id="3adbc-173">Klik in **Solution Explorer** met de rechtermuisknop op de map **Modellen** en klik achtereenvolgens op **Toevoegen** en **Klasse**.</span><span class="sxs-lookup"><span data-stu-id="3adbc-173">In **Solution Explorer**, right-click the **Models** folder, click **Add**, and then click **Class**.</span></span>
   
      <span data-ttu-id="3adbc-174">Het dialoogvenster **Nieuw item toevoegen** wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3adbc-174">The **Add New Item** dialog box appears.</span></span>
2. <span data-ttu-id="3adbc-175">Geef een naam op voor uw nieuwe klasse **Item.cs** en klik op **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="3adbc-175">Name your new class **Item.cs** and click **Add**.</span></span> 
3. <span data-ttu-id="3adbc-176">Voeg in het nieuwe bestand **Item.cs** achter de laatste *gebruiksinstructie* het volgende toe.</span><span class="sxs-lookup"><span data-stu-id="3adbc-176">In this new **Item.cs** file, add the following after the last *using statement*.</span></span>
   
        using Newtonsoft.Json;
4. <span data-ttu-id="3adbc-177">Vervang deze code nu</span><span class="sxs-lookup"><span data-stu-id="3adbc-177">Now replace this code</span></span> 
   
        public class Item
        {
        }
   
    <span data-ttu-id="3adbc-178">door de volgende code.</span><span class="sxs-lookup"><span data-stu-id="3adbc-178">with the following code.</span></span>
   
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
   
    <span data-ttu-id="3adbc-179">Alle gegevens in Azure Cosmos DB worden doorgegeven via de kabel en opgeslagen als JSON.</span><span class="sxs-lookup"><span data-stu-id="3adbc-179">All data in Azure Cosmos DB is passed over the wire and stored as JSON.</span></span> <span data-ttu-id="3adbc-180">U kunt het kenmerk **JsonProperty** gebruiken, zoals wordt beschreven in de klasse **Item** die we zojuist hebben gemaakt, om te bepalen hoe uw objecten door JSON.NET worden geserialiseerd/gedeserialiseerd.</span><span class="sxs-lookup"><span data-stu-id="3adbc-180">To control the way your objects are serialized/deserialized by JSON.NET you can use the **JsonProperty** attribute as demonstrated in the **Item** class we just created.</span></span> <span data-ttu-id="3adbc-181">U **hoeft** dit niet te doen, maar ik wil ervoor zorgen dat mijn eigenschappen de naamgevingsconventie van JSON camelCase volgen.</span><span class="sxs-lookup"><span data-stu-id="3adbc-181">You don't **have** to do this but I want to ensure that my properties follow the JSON camelCase naming conventions.</span></span> 
   
    <span data-ttu-id="3adbc-182">U kunt niet alleen de indeling van de eigenschapsnaam voor JSON bepalen, maar ook de naam van uw .NET-eigenschappen volledig wijzigen, zoals ik deed met de **Description**.</span><span class="sxs-lookup"><span data-stu-id="3adbc-182">Not only can you control the format of the property name when it goes into JSON, but you can entirely rename your .NET properties like I did with the **Description** property.</span></span> 

### <span data-ttu-id="3adbc-183"><a name="_Toc395637765"></a>Een controller toevoegen</span><span class="sxs-lookup"><span data-stu-id="3adbc-183"><a name="_Toc395637765"></a>Add a controller</span></span>
<span data-ttu-id="3adbc-184">Nu we de **M** hebben gehad, kunnen we de **C** in MVC, een controllerklasse, maken.</span><span class="sxs-lookup"><span data-stu-id="3adbc-184">That takes care of the **M**, now let's create the **C** in MVC, a controller class.</span></span>

1. <span data-ttu-id="3adbc-185">Klik in **Solution Explorer** met de rechtermuisknop op de map **Controllers** en klik achtereenvolgens op **Toevoegen** en **Controller**.</span><span class="sxs-lookup"><span data-stu-id="3adbc-185">In **Solution Explorer**, right-click the **Controllers** folder, click **Add**, and then click **Controller**.</span></span>
   
    <span data-ttu-id="3adbc-186">Het dialoogvenster **Add Scaffold** (Scaffold toevoegen) wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3adbc-186">The **Add Scaffold** dialog box appears.</span></span>
2. <span data-ttu-id="3adbc-187">Selecteer **MVC 5 Controller - Empty** (MVC 5-controller - Leeg) en klik vervolgens op **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="3adbc-187">Select **MVC 5 Controller - Empty** and then click **Add**.</span></span>
   
    ![Schermopname van het dialoogvenster Add Scaffold met de optie MVC 5 Controller - Empty gemarkeerd](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-controller-add-scaffold.png)
3. <span data-ttu-id="3adbc-189">Noem uw nieuwe controller **ItemController**.</span><span class="sxs-lookup"><span data-stu-id="3adbc-189">Name your new Controller, **ItemController.**</span></span>
   
    ![Schermopname van het dialoogvenster Add Controller (Controller toevoegen)](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-controller.png)
   
    <span data-ttu-id="3adbc-191">Zodra het bestand is gemaakt, wordt het nieuwe bestand ItemController.cs in **Solution Explorer** weergegeven en ziet uw Visual Studio-oplossing er ongeveer als volgt uit.</span><span class="sxs-lookup"><span data-stu-id="3adbc-191">Once the file is created, your Visual Studio solution should resemble the following with the new ItemController.cs file in **Solution Explorer**.</span></span> <span data-ttu-id="3adbc-192">Het nieuwe bestand Item.cs file, dat eerder is gemaakt, wordt ook weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3adbc-192">The new Item.cs file created earlier is also shown.</span></span>
   
    ![Schermopname van de Visual Studio-oplossing - Solution Explorer met het nieuwe bestand ItemController.cs gemarkeerd](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-item-solution-explorer.png)
   
    <span data-ttu-id="3adbc-194">U kunt ItemController.cs sluiten. Hier komen we later op terug.</span><span class="sxs-lookup"><span data-stu-id="3adbc-194">You can close ItemController.cs, we'll come back to it later.</span></span> 

### <span data-ttu-id="3adbc-195"><a name="_Toc395637766"></a>Weergaven toevoegen</span><span class="sxs-lookup"><span data-stu-id="3adbc-195"><a name="_Toc395637766"></a>Add views</span></span>
<span data-ttu-id="3adbc-196">Laten we nu de **V**, de weergaven, in MVC maken:</span><span class="sxs-lookup"><span data-stu-id="3adbc-196">Now, let's create the **V** in MVC, the views:</span></span>

* <span data-ttu-id="3adbc-197">[Een weergave toevoegen voor een itemindex ](#AddItemIndexView).</span><span class="sxs-lookup"><span data-stu-id="3adbc-197">[Add an Item Index view](#AddItemIndexView).</span></span>
* <span data-ttu-id="3adbc-198">[Een weergave toevoegen voor nieuwe items](#AddNewIndexView).</span><span class="sxs-lookup"><span data-stu-id="3adbc-198">[Add a New Item view](#AddNewIndexView).</span></span>
* <span data-ttu-id="3adbc-199">[Een weergave toevoegen voor het bewerken van items](#_Toc395888515).</span><span class="sxs-lookup"><span data-stu-id="3adbc-199">[Add an Edit Item view](#_Toc395888515).</span></span>

#### <span data-ttu-id="3adbc-200"><a name="AddItemIndexView"></a>Een weergave toevoegen voor een itemindex</span><span class="sxs-lookup"><span data-stu-id="3adbc-200"><a name="AddItemIndexView"></a>Add an Item Index view</span></span>
1. <span data-ttu-id="3adbc-201">Vouw in **Solution Explorer** de map **Weergaven** uit en klik met de rechtermuisknop op de lege map **Item** die Visual Studio voor u heeft gemaakt toen u **ItemController** hebt toegevoegd. Klik vervolgens op **Toevoegen** en **Weergave**.</span><span class="sxs-lookup"><span data-stu-id="3adbc-201">In **Solution Explorer**, expand the **Views**  folder, right-click the empty **Item** folder that Visual Studio created for you when you added the **ItemController** earlier, click **Add**, and then click **View**.</span></span>
   
    ![Schermopname van Solution Explorer waarin de map Item wordt weergegeven die Visual Studio heeft gemaakt en waarin de opdrachten voor het toevoegen van een weergave zijn gemarkeerd](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view.png)
2. <span data-ttu-id="3adbc-203">Voer in het dialoogvenster **Weergave toevoegen** de volgende handelingen uit:</span><span class="sxs-lookup"><span data-stu-id="3adbc-203">In the **Add View** dialog box, do the following:</span></span>
   
   * <span data-ttu-id="3adbc-204">In het vak **Weergavenaam** typt u ***Index***.</span><span class="sxs-lookup"><span data-stu-id="3adbc-204">In the **View name** box, type ***Index***.</span></span>
   * <span data-ttu-id="3adbc-205">Selecteer in het vak **Sjabloon** de optie ***Lijst***.</span><span class="sxs-lookup"><span data-stu-id="3adbc-205">In the **Template** box, select ***List***.</span></span>
   * <span data-ttu-id="3adbc-206">Selecteer in het vak **Modelklasse** de optie ***Item (todo.Models)***.</span><span class="sxs-lookup"><span data-stu-id="3adbc-206">In the **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="3adbc-207">Typ in het veld voor de indelingspagina ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="3adbc-207">In the layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
     
   ![Schermopname van het dialoogvenster Weergave toevoegen](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view-dialog.png)
3. <span data-ttu-id="3adbc-209">Zodra al deze waarden zijn ingesteld, klikt u op **Toevoegen** en wordt er een nieuwe sjabloonweergave in Visual Studio gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3adbc-209">Once all these values are set, click **Add** and let Visual Studio create a new template view.</span></span> <span data-ttu-id="3adbc-210">Vervolgens wordt het cshtml-bestand geopend dat is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3adbc-210">Once it is done, it will open the cshtml file  that was created.</span></span> <span data-ttu-id="3adbc-211">Dit bestand in Visual Studio kan voorlopig worden gesloten, aangezien dit pas later aan bod komt.</span><span class="sxs-lookup"><span data-stu-id="3adbc-211">We can close that file in Visual Studio as we will come back to it later.</span></span>

#### <span data-ttu-id="3adbc-212"><a name="AddNewIndexView"></a>Een weergave toevoegen voor nieuwe items</span><span class="sxs-lookup"><span data-stu-id="3adbc-212"><a name="AddNewIndexView"></a>Add a New Item view</span></span>
<span data-ttu-id="3adbc-213">We kunnen op ongeveer dezelfde manier als voor de weergave **Itemindex** nu een nieuwe weergave voor het maken van nieuwe **Items** maken.</span><span class="sxs-lookup"><span data-stu-id="3adbc-213">Similar to how we created an **Item Index** view, we will now create a new view for creating new **Items**.</span></span>

1. <span data-ttu-id="3adbc-214">Klik in **Solution Explorer** met de rechtermuisknop nogmaals op de map **Item** en klik achtereenvolgens op **Toevoegen** en **Weergave**.</span><span class="sxs-lookup"><span data-stu-id="3adbc-214">In **Solution Explorer**, right-click the **Item** folder again, click **Add**, and then click **View**.</span></span>
2. <span data-ttu-id="3adbc-215">Voer in het dialoogvenster **Weergave toevoegen** de volgende handelingen uit:</span><span class="sxs-lookup"><span data-stu-id="3adbc-215">In the **Add View** dialog box, do the following:</span></span>
   
   * <span data-ttu-id="3adbc-216">Typ in het vak **Weergavenaam** ***Maken***.</span><span class="sxs-lookup"><span data-stu-id="3adbc-216">In the **View name** box, type ***Create***.</span></span>
   * <span data-ttu-id="3adbc-217">Selecteer in het vak **Sjabloon** de optie ***Maken***.</span><span class="sxs-lookup"><span data-stu-id="3adbc-217">In the **Template** box, select ***Create***.</span></span>
   * <span data-ttu-id="3adbc-218">Selecteer in het vak **Modelklasse** de optie ***Item (todo.Models)***.</span><span class="sxs-lookup"><span data-stu-id="3adbc-218">In the **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="3adbc-219">Typ in het veld voor de indelingspagina ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="3adbc-219">In the layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
   * <span data-ttu-id="3adbc-220">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="3adbc-220">Click **Add**.</span></span>
   
#### <span data-ttu-id="3adbc-221"><a name="_Toc395888515"></a>Een weergave toevoegen voor het bewerken van items</span><span class="sxs-lookup"><span data-stu-id="3adbc-221"><a name="_Toc395888515"></a>Add an Edit Item view</span></span>
<span data-ttu-id="3adbc-222">Tot slot voegt u op dezelfde manier als hiervoor een weergave toe waarin u **items** kunt bewerken.</span><span class="sxs-lookup"><span data-stu-id="3adbc-222">And finally, add one last view for editing an **Item** in the same way as before.</span></span>

1. <span data-ttu-id="3adbc-223">Klik in **Solution Explorer** met de rechtermuisknop nogmaals op de map **Item** en klik achtereenvolgens op **Toevoegen** en **Weergave**.</span><span class="sxs-lookup"><span data-stu-id="3adbc-223">In **Solution Explorer**, right-click the **Item** folder again, click **Add**, and then click **View**.</span></span>
2. <span data-ttu-id="3adbc-224">Voer in het dialoogvenster **Weergave toevoegen** de volgende handelingen uit:</span><span class="sxs-lookup"><span data-stu-id="3adbc-224">In the **Add View** dialog box, do the following:</span></span>
   
   * <span data-ttu-id="3adbc-225">Typ in het vak **Weergavenaam** ***Bewerken***.</span><span class="sxs-lookup"><span data-stu-id="3adbc-225">In the **View name** box, type ***Edit***.</span></span>
   * <span data-ttu-id="3adbc-226">Selecteer in het vak **Sjabloon** de optie ***Bewerken***.</span><span class="sxs-lookup"><span data-stu-id="3adbc-226">In the **Template** box, select ***Edit***.</span></span>
   * <span data-ttu-id="3adbc-227">Selecteer in het vak **Modelklasse** de optie ***Item (todo.Models)***.</span><span class="sxs-lookup"><span data-stu-id="3adbc-227">In the **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="3adbc-228">Typ in het veld voor de indelingspagina ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="3adbc-228">In the layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
   * <span data-ttu-id="3adbc-229">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="3adbc-229">Click **Add**.</span></span>

<span data-ttu-id="3adbc-230">Zodra dit is gebeurd, sluit u alle cshtml-documenten in Visual Studio. We komen later op deze weergaven terug.</span><span class="sxs-lookup"><span data-stu-id="3adbc-230">Once this is done, close all the cshtml documents in Visual Studio as we will return to these views later.</span></span>

## <span data-ttu-id="3adbc-231"><a name="_Toc395637769"></a>Stap 5: Azure Cosmos DB fysiek aansluiten</span><span class="sxs-lookup"><span data-stu-id="3adbc-231"><a name="_Toc395637769"></a>Step 5: Wiring up Azure Cosmos DB</span></span>
<span data-ttu-id="3adbc-232">Nu de standaardwerkzaamheden voor MVC zijn voltooid, kunt u de code voor Azure Cosmos DB toevoegen.</span><span class="sxs-lookup"><span data-stu-id="3adbc-232">Now that the standard MVC stuff is taken care of, let's turn to adding the code for Azure Cosmos DB.</span></span> 

<span data-ttu-id="3adbc-233">In deze sectie voegen we code toe voor de verwerking van het volgende:</span><span class="sxs-lookup"><span data-stu-id="3adbc-233">In this section, we'll add code to handle the following:</span></span>

* <span data-ttu-id="3adbc-234">[Vermelden van onvolledige items](#_Toc395637770).</span><span class="sxs-lookup"><span data-stu-id="3adbc-234">[Listing incomplete Items](#_Toc395637770).</span></span>
* <span data-ttu-id="3adbc-235">[Items toevoegen](#_Toc395637771).</span><span class="sxs-lookup"><span data-stu-id="3adbc-235">[Adding Items](#_Toc395637771).</span></span>
* <span data-ttu-id="3adbc-236">[Items bewerken](#_Toc395637772).</span><span class="sxs-lookup"><span data-stu-id="3adbc-236">[Editing Items](#_Toc395637772).</span></span>

### <span data-ttu-id="3adbc-237"><a name="_Toc395637770"></a>Onvolledige objecten in uw MVC-webtoepassing vermelden</span><span class="sxs-lookup"><span data-stu-id="3adbc-237"><a name="_Toc395637770"></a>Listing incomplete Items in your MVC web application</span></span>
<span data-ttu-id="3adbc-238">Allereerst moet u een klasse toevoegen die de logica bevat voor de verbinding met en het gebruik van Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3adbc-238">The first thing to do here is add a class that contains all the logic to connect to and use Azure Cosmos DB.</span></span> <span data-ttu-id="3adbc-239">Voor deze zelfstudie voegen we alle logica toe aan een opslagplaatsklasse met de naam DocumentDBRepository.</span><span class="sxs-lookup"><span data-stu-id="3adbc-239">For this tutorial we'll encapsulate all this logic in to a repository class called DocumentDBRepository.</span></span> 

1. <span data-ttu-id="3adbc-240">Klik in **Solution Explorer** met de rechtermuisknop op het project, klik op **Toevoegen** en klik vervolgens op **Klasse**.</span><span class="sxs-lookup"><span data-stu-id="3adbc-240">In **Solution Explorer**, right-click on the project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="3adbc-241">Geef een naam voor de nieuwe klasse **DocumentDBRepository** op en klik op **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="3adbc-241">Name the new class **DocumentDBRepository** and click **Add**.</span></span>
2. <span data-ttu-id="3adbc-242">Voeg de volgende *gebruiksinstructies* boven de *naamruimtedeclaratie* toe in de klasse **DocumentDBRepository** die we zojuist hebben gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3adbc-242">In the newly created **DocumentDBRepository** class and add the following *using statements* above the *namespace* declaration</span></span>
   
        using Microsoft.Azure.Documents; 
        using Microsoft.Azure.Documents.Client; 
        using Microsoft.Azure.Documents.Linq; 
        using System.Configuration;
        using System.Linq.Expressions;
        using System.Threading.Tasks;
        using System.Net
        
    <span data-ttu-id="3adbc-243">Vervang deze code nu</span><span class="sxs-lookup"><span data-stu-id="3adbc-243">Now replace this code</span></span> 
   
        public class DocumentDBRepository
        {
        }
   
    <span data-ttu-id="3adbc-244">door de volgende code.</span><span class="sxs-lookup"><span data-stu-id="3adbc-244">with the following code.</span></span>
   
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
   
    
3. <span data-ttu-id="3adbc-245">Aangezien er enkele waarden uit de configuratie worden gelezen, opent u het bestand **Web.config** van de toepassing en voegt u de volgende regels onder de sectie `<AppSettings>` toe.</span><span class="sxs-lookup"><span data-stu-id="3adbc-245">We're reading some values from configuration, so open the **Web.config** file of your application and add the following lines under the `<AppSettings>` section.</span></span>
   
        <add key="endpoint" value="enter the URI from the Keys blade of the Azure Portal"/>
        <add key="authKey" value="enter the PRIMARY KEY, or the SECONDARY KEY, from the Keys blade of the Azure  Portal"/>
        <add key="database" value="ToDoList"/>
        <add key="collection" value="Items"/>
4. <span data-ttu-id="3adbc-246">Werk nu de waarden voor *endpoint* en *authKey* bij door gebruik te maken van de blade Sleutels van Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="3adbc-246">Now, update the values for *endpoint* and *authKey* using the Keys blade of the Azure Portal.</span></span> <span data-ttu-id="3adbc-247">Gebruik de **URI** op de blade Sleutels als waarde voor de endpoint-instelling en gebruik de **PRIMAIRE SLEUTEL** of **SECUNDAIRE SLEUTEL** op de blade Sleutels als waarde voor authKey-instelling.</span><span class="sxs-lookup"><span data-stu-id="3adbc-247">Use the **URI** from the Keys blade as the value of the endpoint setting, and use the **PRIMARY KEY**, or **SECONDARY KEY** from the Keys blade as the value of the authKey setting.</span></span>

    <span data-ttu-id="3adbc-248">Dat zorgt voor de bekabeling van de opslagplaats Azure Cosmos DB nu gaan we toepassingslogica toevoegen.</span><span class="sxs-lookup"><span data-stu-id="3adbc-248">That takes care of wiring up the Azure Cosmos DB repository, now let's add our application logic.</span></span>

1. <span data-ttu-id="3adbc-249">Op de eerste plaats willen we natuurlijk de onvolledige items kunnen weergeven met een takenlijsttoepassing.</span><span class="sxs-lookup"><span data-stu-id="3adbc-249">The first thing we want to be able to do with a todo list application is to display the incomplete items.</span></span>  <span data-ttu-id="3adbc-250">Kopieer het volgende codefragment en plak dit ergens in de klasse **DocumentDBRepository**.</span><span class="sxs-lookup"><span data-stu-id="3adbc-250">Copy and paste the following code snippet anywhere within the **DocumentDBRepository** class.</span></span>
   
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
2. <span data-ttu-id="3adbc-251">Open de **ItemController** die eerder is toegevoegd en voeg de volgende *Using-instructies* toe boven de naamruimtedeclaratie.</span><span class="sxs-lookup"><span data-stu-id="3adbc-251">Open the **ItemController** we added earlier and add the following *using statements* above the namespace declaration.</span></span>
   
        using System.Net;
        using System.Threading.Tasks;
        using todo.Models;
   
    <span data-ttu-id="3adbc-252">Als u het project een andere naam dan 'todo' hebt gegeven, moet u 'todo.Models' bijwerken om hier de naam van uw project weer te geven.</span><span class="sxs-lookup"><span data-stu-id="3adbc-252">If your project is not named "todo", then you need to update using "todo.Models"; to reflect the name of your project.</span></span>
   
    <span data-ttu-id="3adbc-253">Vervang deze code nu</span><span class="sxs-lookup"><span data-stu-id="3adbc-253">Now replace this code</span></span>
   
        //GET: Item
        public ActionResult Index()
        {
            return View();
        }
   
    <span data-ttu-id="3adbc-254">door de volgende code.</span><span class="sxs-lookup"><span data-stu-id="3adbc-254">with the following code.</span></span>
   
        [ActionName("Index")]
        public async Task<ActionResult> IndexAsync()
        {
            var items = await DocumentDBRepository<Item>.GetItemsAsync(d => !d.Completed);
            return View(items);
        }
3. <span data-ttu-id="3adbc-255">Open **Global.asax.cs** en voeg de volgende regel aan de methode **Application_Start** toe.</span><span class="sxs-lookup"><span data-stu-id="3adbc-255">Open **Global.asax.cs** and add the following line to the **Application_Start** method</span></span> 
   
        DocumentDBRepository<todo.Models.Item>.Initialize();

<span data-ttu-id="3adbc-256">Op dit moment moet uw oplossing opbouwbewerking kunnen uitvoeren zonder dat er fouten optreden.</span><span class="sxs-lookup"><span data-stu-id="3adbc-256">At this point your solution should be able to build without any errors.</span></span>

<span data-ttu-id="3adbc-257">Als u de toepassing nu hebt uitgevoerd, gaat u naar de weergaven **HomeController** en **Index** van die controller.</span><span class="sxs-lookup"><span data-stu-id="3adbc-257">If you ran the application now, you would go to the **HomeController** and the **Index** view of that controller.</span></span> <span data-ttu-id="3adbc-258">Dit is het standaardgedrag voor het MVC-sjabloonproject dat we aan het begin hebben gekozen, maar dit is niet het gewenste gedrag.</span><span class="sxs-lookup"><span data-stu-id="3adbc-258">This is the default behavior for the MVC template project we chose at the start but we don't want that!</span></span> <span data-ttu-id="3adbc-259">U kunt de routering op deze MVC-toepassing wijzigen om dit gedrag te veranderen.</span><span class="sxs-lookup"><span data-stu-id="3adbc-259">Let's change the routing on this MVC application to alter this behavior.</span></span>

<span data-ttu-id="3adbc-260">Open ***App\_Start\RouteConfig.cs*** en zoek de regel die begint met "defaults:" en pas deze als volgt aan.</span><span class="sxs-lookup"><span data-stu-id="3adbc-260">Open ***App\_Start\RouteConfig.cs*** and locate the line starting with "defaults:" and change it to resemble the following.</span></span>

        defaults: new { controller = "Item", action = "Index", id = UrlParameter.Optional }

<span data-ttu-id="3adbc-261">Hiermee stelt u in dat ASP.NET MVC niet **Home** maar **Item** als controller gebruikt en **Index** als weergave gebruikt als u in de URL geen waarde hebt opgegeven voor het routeringsgedrag.</span><span class="sxs-lookup"><span data-stu-id="3adbc-261">This now tells ASP.NET MVC that if you have not specified a value in the URL to control the routing behavior that instead of **Home**, use **Item** as the controller and user **Index** as the view.</span></span>

<span data-ttu-id="3adbc-262">Als u de toepassing nu uitvoert, wordt uw **ItemController** aangeroepen, die vervolgens de opslagplaatsklasse aanroept en de methode GetItems gebruikt om alle onvolledige items naar de weergave **Weergaven**\\**Item**\\**Index** te retourneren.</span><span class="sxs-lookup"><span data-stu-id="3adbc-262">Now if you run the application, it will call into your **ItemController** which will call in to the repository class and use the GetItems method to return all the incomplete items to the **Views**\\**Item**\\**Index** view.</span></span> 

<span data-ttu-id="3adbc-263">Als u dit project nu maakt en uitvoert, ziet u iets dat vergelijkbaar is met het volgende.</span><span class="sxs-lookup"><span data-stu-id="3adbc-263">If you build and run this project now, you should now see something that looks this.</span></span>    

![Schermopname van de takenlijstwebtoepassing die is gemaakt met deze databasezelfstudie](./media/documentdb-dotnet-application/build-and-run-the-project-now.png)

### <span data-ttu-id="3adbc-265"><a name="_Toc395637771"></a>Items toevoegen</span><span class="sxs-lookup"><span data-stu-id="3adbc-265"><a name="_Toc395637771"></a>Adding Items</span></span>
<span data-ttu-id="3adbc-266">Laten we enkele items toevoegen aan de database zodat we niet tegen een leeg raster aankijken.</span><span class="sxs-lookup"><span data-stu-id="3adbc-266">Let's put some items into our database so we have something more than an empty grid to look at.</span></span>

<span data-ttu-id="3adbc-267">U kunt nu code toevoegen aan Azure Cosmos DBRepository en ItemController om de record in Azure Cosmos DB te houden.</span><span class="sxs-lookup"><span data-stu-id="3adbc-267">Let's add some code to  Azure Cosmos DBRepository and ItemController to persist the record in Azure Cosmos DB.</span></span>

1. <span data-ttu-id="3adbc-268">Voeg de volgende methode toe aan uw klasse **DocumentDBRepository**.</span><span class="sxs-lookup"><span data-stu-id="3adbc-268">Add the following method to your **DocumentDBRepository** class.</span></span>
   
       public static async Task<Document> CreateItemAsync(T item)
       {
           return await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId), item);
       }
   
   <span data-ttu-id="3adbc-269">Deze methode wordt een object dat is doorgegeven aan deze gewoon en deze in Azure Cosmos DB zich blijft voordoen.</span><span class="sxs-lookup"><span data-stu-id="3adbc-269">This method simply takes an object passed to it and persists it in Azure Cosmos DB.</span></span>
2. <span data-ttu-id="3adbc-270">Open het bestand ItemController.cs en voeg het volgende codefragment toe binnen de klasse.</span><span class="sxs-lookup"><span data-stu-id="3adbc-270">Open the ItemController.cs file and add the following code snippet within the class.</span></span> <span data-ttu-id="3adbc-271">Zodoende weet ASP.NET MVC wat er voor de actie **Create** moet worden gedaan.</span><span class="sxs-lookup"><span data-stu-id="3adbc-271">This is how ASP.NET MVC knows what to do for the **Create** action.</span></span> <span data-ttu-id="3adbc-272">In dit geval geeft u de bijbehorende weergave Create.cshtml weer die eerder is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3adbc-272">In this case just render the associated Create.cshtml view created earlier.</span></span>
   
        [ActionName("Create")]
        public async Task<ActionResult> CreateAsync()
        {
            return View();
        }
   
    <span data-ttu-id="3adbc-273">Er is nu meer code in deze controller nodig die de inzending vanuit de weergave **Create** accepteert.</span><span class="sxs-lookup"><span data-stu-id="3adbc-273">We now need some more code in this controller that will accept the submission from the **Create** view.</span></span>
3. <span data-ttu-id="3adbc-274">Voeg het volgende codeblok toe aan de klasse ItemController.cs waarmee ASP.NET MVC wordt geïnstrueerd wat er moet gebeuren met een form POST voor deze controller.</span><span class="sxs-lookup"><span data-stu-id="3adbc-274">Add the next block of code to the ItemController.cs class that tells ASP.NET MVC what to do with a form POST for this controller.</span></span>
   
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
   
    <span data-ttu-id="3adbc-275">Deze code roept de DocumentDBRepository aan en gebruikt de methode CreateItemAsync om het nieuwe takenlijstitem door te geven aan de database.</span><span class="sxs-lookup"><span data-stu-id="3adbc-275">This code calls in to the DocumentDBRepository and uses the CreateItemAsync method to persist the new todo item to the database.</span></span> 
   
    <span data-ttu-id="3adbc-276">**Opmerking over de beveiliging**: het kenmerk **ValidateAntiForgeryToken** wordt hier gebruikt om deze toepassing te beschermen tegen aanvallen via aanvraagvervalsing op meerdere sites.</span><span class="sxs-lookup"><span data-stu-id="3adbc-276">**Security Note**: The **ValidateAntiForgeryToken** attribute is used here to help protect this application against cross-site request forgery attacks.</span></span> <span data-ttu-id="3adbc-277">Het volstaat echter niet om dit kenmerk alleen toe te voegen. Uw weergaven moeten samenwerken met dit anti-vervalsingstoken.</span><span class="sxs-lookup"><span data-stu-id="3adbc-277">There is more to it than just adding this attribute, your views need to work with this anti-forgery token as well.</span></span> <span data-ttu-id="3adbc-278">Zie [Voorkomen van aanvraagvervalsing op meerdere sites][Preventing Cross-Site Request Forgery] voor meer informatie over dit onderwerp en voorbeelden van een juiste implementatie.</span><span class="sxs-lookup"><span data-stu-id="3adbc-278">For more on the subject, and examples of how to implement this correctly, please see [Preventing Cross-Site Request Forgery][Preventing Cross-Site Request Forgery].</span></span> <span data-ttu-id="3adbc-279">De broncode op [GitHub][GitHub] beschikt over de volledige implementatie.</span><span class="sxs-lookup"><span data-stu-id="3adbc-279">The source code provided on [GitHub][GitHub] has the full implementation in place.</span></span>
   
    <span data-ttu-id="3adbc-280">**Opmerking over de beveiliging**: we gebruiken ook het kenmerk **Bind** voor de methodeparameter om u te beschermen tegen over-postingaanvallen.</span><span class="sxs-lookup"><span data-stu-id="3adbc-280">**Security Note**: We also use the **Bind** attribute on the method parameter to help protect against over-posting attacks.</span></span> <span data-ttu-id="3adbc-281">Zie [Eenvoudige CRUD-bewerkingen in ASP.NET MVC][Basic CRUD Operations in ASP.NET MVC] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3adbc-281">For more details please see [Basic CRUD Operations in ASP.NET MVC][Basic CRUD Operations in ASP.NET MVC].</span></span>

<span data-ttu-id="3adbc-282">Hiermee is de benodigde code toegevoegd om nieuwe items aan de database toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="3adbc-282">This concludes the code required to add new Items to our database.</span></span>

### <span data-ttu-id="3adbc-283"><a name="_Toc395637772"></a>Items bewerken</span><span class="sxs-lookup"><span data-stu-id="3adbc-283"><a name="_Toc395637772"></a>Editing Items</span></span>
<span data-ttu-id="3adbc-284">Tot slot moeten we ervoor zorgen dat we **Items** in de database kunnen bewerken en dat we ze kunnen markeren als voltooid.</span><span class="sxs-lookup"><span data-stu-id="3adbc-284">There is one last thing for us to do, and that is to add the ability to edit **Items** in the database and to mark them as complete.</span></span> <span data-ttu-id="3adbc-285">De weergave voor het bewerken van items was al toegevoegd aan het project. U hoeft daarom alleen code toe te voegen aan de controller en de klasse **DocumentDBRepository**.</span><span class="sxs-lookup"><span data-stu-id="3adbc-285">The view for editing was already added to the project, so we just need to add some code to our controller and to the **DocumentDBRepository** class again.</span></span>

1. <span data-ttu-id="3adbc-286">Voeg het volgende toe aan de klasse **DocumentDBRepository**.</span><span class="sxs-lookup"><span data-stu-id="3adbc-286">Add the following to the **DocumentDBRepository** class.</span></span>
   
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
   
    <span data-ttu-id="3adbc-287">Met de eerste methode, **GetItem**, wordt een item uit Azure Cosmos DB opgehaald dat wordt doorgegeven aan de **ItemController** en vervolgens aan de weergave **Bewerken**.</span><span class="sxs-lookup"><span data-stu-id="3adbc-287">The first of these methods, **GetItem** fetches an Item from Azure Cosmos DB which is passed back to the **ItemController** and then on to the **Edit** view.</span></span>
   
    <span data-ttu-id="3adbc-288">Met de tweede methode die zojuist is toegevoegd, wordt het **document** in Azure Cosmos DB vervangen door de versie van het **document** dat is doorgegeven via de **ItemController**.</span><span class="sxs-lookup"><span data-stu-id="3adbc-288">The second of the methods we just added replaces the **Document** in Azure Cosmos DB with the version of the **Document** passed in from the **ItemController**.</span></span>
2. <span data-ttu-id="3adbc-289">Voeg het volgende toe aan de klasse **ItemController**.</span><span class="sxs-lookup"><span data-stu-id="3adbc-289">Add the following to the **ItemController** class.</span></span>
   
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
   
    <span data-ttu-id="3adbc-290">De eerste methode verwerkt de Http GET die plaatsvindt wanneer de gebruiker klikt op de koppeling **Bewerken** in de weergave **Index**.</span><span class="sxs-lookup"><span data-stu-id="3adbc-290">The first method handles the Http GET that happens when the user clicks on the **Edit** link from the **Index** view.</span></span> <span data-ttu-id="3adbc-291">Met deze methode wordt er een [**document**](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) uit Azure Cosmos DB opgehaald en doorgegeven aan de weergave **Bewerken**.</span><span class="sxs-lookup"><span data-stu-id="3adbc-291">This method fetches a [**Document**](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) from Azure Cosmos DB and passes it to the **Edit** view.</span></span>
   
    <span data-ttu-id="3adbc-292">In de weergave **Bewerken** wordt vervolgens een Http POST naar de **IndexController** uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3adbc-292">The **Edit** view will then do an Http POST to the **IndexController**.</span></span> 
   
    <span data-ttu-id="3adbc-293">Voor de tweede methode zijn er ingangen toegevoegd om het bijgewerkte object door te geven aan Azure Cosmos DB, zodat het object wordt bewaard in de database.</span><span class="sxs-lookup"><span data-stu-id="3adbc-293">The second method we added handles passing the updated object to Azure Cosmos DB to be persisted in the database.</span></span>

<span data-ttu-id="3adbc-294">Meer hoeft u niet te doen om uw toepassing uit te voeren, onvolledige **Items** weer te geven, nieuwe **Items** toe te voegen en **Items** te bewerken.</span><span class="sxs-lookup"><span data-stu-id="3adbc-294">That's it, that is everything we need to run our application, list incomplete **Items**, add new **Items**, and edit **Items**.</span></span>

## <span data-ttu-id="3adbc-295"><a name="_Toc395637773"></a>Stap 6: De toepassing lokaal uitvoeren</span><span class="sxs-lookup"><span data-stu-id="3adbc-295"><a name="_Toc395637773"></a>Step 6: Run the application locally</span></span>
<span data-ttu-id="3adbc-296">Ga als volgt te werk als u de toepassing wilt testen op een lokale machine:</span><span class="sxs-lookup"><span data-stu-id="3adbc-296">To test the application on your local machine, do the following:</span></span>

1. <span data-ttu-id="3adbc-297">Druk in Visual Studio op F5 om de toepassing in de foutopsporingsmodus op te bouwen.</span><span class="sxs-lookup"><span data-stu-id="3adbc-297">Hit F5 in Visual Studio to build the application in debug mode.</span></span> <span data-ttu-id="3adbc-298">De toepassing wordt opgebouwd en wordt er een browser gestart met het lege rasterpagina dat we eerder hebben gezien:</span><span class="sxs-lookup"><span data-stu-id="3adbc-298">It should build the application and launch a browser with the empty grid page we saw before:</span></span>
   
    ![Schermopname van de takenlijstwebtoepassing die is gemaakt met deze databasezelfstudie](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item-a.png)
   
     
2. <span data-ttu-id="3adbc-300">Klik op de koppeling **Nieuw maken** en voeg waarden toe aan de velden **Naam** en **Beschrijving**.</span><span class="sxs-lookup"><span data-stu-id="3adbc-300">Click the **Create New** link and add values to the **Name** and **Description** fields.</span></span> <span data-ttu-id="3adbc-301">Schakel het selectievakje **Voltooid** niet in, anders wordt het nieuwe **Item** toegevoegd met een onvoltooide status en wordt het niet weergegeven in de aanvankelijke lijst.</span><span class="sxs-lookup"><span data-stu-id="3adbc-301">Leave the **Completed** check box unselected otherwise the new **Item** will be added in a completed state and will not appear on the initial list.</span></span>
   
    ![Schermopname van de weergave Maken](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-new-item.png)
3. <span data-ttu-id="3adbc-303">Als u op **Maken** klikt, keert u terug naar de weergaven **Index** en wordt uw **Item** weergegeven in de lijst.</span><span class="sxs-lookup"><span data-stu-id="3adbc-303">Click **Create** and you are redirected back to the **Index** view and your **Item** appears in the list.</span></span>
   
    ![Schermopname van de weergave Index](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item.png)
   
    <span data-ttu-id="3adbc-305">U kunt gerust nog enkele **Items** aan uw takenlijst toevoegen.</span><span class="sxs-lookup"><span data-stu-id="3adbc-305">Feel free to add a few more **Items** to your todo list.</span></span>
    
4. <span data-ttu-id="3adbc-306">Klik op **Bewerken** naast een **Item** in de lijst, zodat u wordt omgeleid naar de weergave **Bewerken**. Hier kunt u de eigenschappen van uw object bijwerken, inclusief de vlag **Voltooid**.</span><span class="sxs-lookup"><span data-stu-id="3adbc-306">Click **Edit** next to an **Item** on the list and you are taken to the **Edit** view where you can update any property of your object, including the **Completed** flag.</span></span> <span data-ttu-id="3adbc-307">Als u de vlag **Voltooid** markeert en op **Opslaan** klikt, wordt het **Item** verwijderd uit de lijst met onvolledige taken.</span><span class="sxs-lookup"><span data-stu-id="3adbc-307">If you mark the **Complete** flag and click **Save**, the **Item** is removed from the list of incomplete tasks.</span></span>
   
    ![Schermopname van de weergave Index met het selectievakje Voltooid ingeschakeld](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-completed-item.png)
5. <span data-ttu-id="3adbc-309">Zodra u de app hebt getest, drukt u op Ctrl + F5 om de foutopsporing voor de app te stoppen.</span><span class="sxs-lookup"><span data-stu-id="3adbc-309">Once you've tested the app, press Ctrl+F5 to stop debugging the app.</span></span> <span data-ttu-id="3adbc-310">U kunt de app nu implementeren.</span><span class="sxs-lookup"><span data-stu-id="3adbc-310">You're ready to deploy!</span></span>

## <span data-ttu-id="3adbc-311"><a name="_Toc395637774"></a>Stap 7: De toepassing in Azure App Service implementeren</span><span class="sxs-lookup"><span data-stu-id="3adbc-311"><a name="_Toc395637774"></a>Step 7: Deploy the application to Azure App Service</span></span> 
<span data-ttu-id="3adbc-312">Nu dat u hebt de volledige toepassing correct werkt met Azure Cosmos DB gaan we deze web-app implementeren in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="3adbc-312">Now that you have the complete application working correctly with Azure Cosmos DB we're going to deploy this web app to Azure App Service.</span></span>  

1. <span data-ttu-id="3adbc-313">Als u deze toepassing wilt publiceren, hoeft u alleen maar met de rechtermuisknop op het project in **Solution Explorer** te klikken en vervolgens op **Publiceren** te klikken.</span><span class="sxs-lookup"><span data-stu-id="3adbc-313">To publish this application all you need to do is right-click on the project in **Solution Explorer** and click **Publish**.</span></span>
   
    ![Schermopname van de optie Publiceren in Solution Explorer](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish.png)

2. <span data-ttu-id="3adbc-315">In de **publiceren** in het dialoogvenster klikt u op **Microsoft Azure App Service**, selecteer daarna **nieuw** een App Service-profiel maken of klik op **bestaande selecteren**  een bestaand profiel gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3adbc-315">In the **Publish** dialog box, click **Microsoft Azure App Service**, then select **Create New** to create an App Service profile, or click **Select Existing** to use an existing profile.</span></span>

    ![Het dialoogvenster Publish in Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish-to-existing.png)

3. <span data-ttu-id="3adbc-317">Als u een bestaand Azure App Service-profiel, voert u de abonnementsnaam van uw.</span><span class="sxs-lookup"><span data-stu-id="3adbc-317">If you have an existing Azure App Service profile, enter your subscription name.</span></span> <span data-ttu-id="3adbc-318">Gebruik de **weergave** filteren om te sorteren op resourcegroep of brontype en selecteer vervolgens uw Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="3adbc-318">Use the **View** filter to sort by resource group or resource type, then select your Azure App Service.</span></span> 
   
    ![In het dialoogvenster App Service in Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-app-service.png)

4. <span data-ttu-id="3adbc-320">Klik op om een nieuw Azure App Service-profiel **nieuw** in de **publiceren** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3adbc-320">To create a new Azure App Service profile, click **Create New** in the **Publish** dialog box.</span></span> <span data-ttu-id="3adbc-321">In de **Create App Service** dialoogvenster, Voer uw Web-App-naam en de juiste abonnement, de resourcegroep en de App Service-abonnement en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="3adbc-321">In the **Create App Service** dialog, enter your Web App name and appropriate subscription, resource group, and App Service plan, then click **Create**.</span></span>

    ![Het dialoogvenster App Service maken in Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-app-service.png)

<span data-ttu-id="3adbc-323">Binnen een paar seconden zal Visual Studio publicatie van uw webtoepassing voltooien en een browser starten waarin u kunt zien uw werk in Azure wordt uitgevoerd!</span><span class="sxs-lookup"><span data-stu-id="3adbc-323">In a few seconds, Visual Studio will finish publishing your web application and launch a browser where you can see your handiwork running in Azure!</span></span>



## <span data-ttu-id="3adbc-324"><a name="_Toc395637775"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3adbc-324"><a name="_Toc395637775"></a>Next steps</span></span>
<span data-ttu-id="3adbc-325">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="3adbc-325">Congratulations!</span></span> <span data-ttu-id="3adbc-326">U zojuist hebt gemaakt van uw eerste ASP.NET MVC-webtoepassing met Azure Cosmos DB en gepubliceerd naar Azure.</span><span class="sxs-lookup"><span data-stu-id="3adbc-326">You just built your first ASP.NET MVC web application using Azure Cosmos DB and published it to Azure.</span></span> <span data-ttu-id="3adbc-327">De broncode voor de volledige toepassing, met inbegrip van de functionaliteit voor details en verwijderen die niet is opgenomen in deze zelfstudie, kan worden gedownload of gekloond via [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="3adbc-327">The source code for the complete application, including the detail and delete functionality that were not included in this tutorial can be downloaded or cloned from [GitHub][GitHub].</span></span> <span data-ttu-id="3adbc-328">Als dit wilt toevoegen aan uw app, kunt u de code ophalen en toevoegen aan deze app.</span><span class="sxs-lookup"><span data-stu-id="3adbc-328">So if you're interested in adding that to your app, grab the code and add it to this app.</span></span>

<span data-ttu-id="3adbc-329">Om extra functionaliteit toe te voegen aan uw toepassing, bekijkt u de API's beschikbaar zijn in de [Azure Cosmos DB .NET-bibliotheek](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) harte welkom om bij te dragen naar de Azure Cosmos DB .NET-bibliotheek op [GitHub] [GitHub].</span><span class="sxs-lookup"><span data-stu-id="3adbc-329">To add additional functionality to your application, review the APIs available in the [Azure Cosmos DB .NET Library](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) and feel free to contribute to the Azure Cosmos DB .NET Library on [GitHub][GitHub].</span></span> 

[\*]: https://microsoft.sharepoint.com/teams/DocDB/Shared%20Documents/Documentation/Docs.LatestVersions/PicExportError
[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Preventing Cross-Site Request Forgery]: http://go.microsoft.com/fwlink/?LinkID=517254
[Basic CRUD Operations in ASP.NET MVC]: http://go.microsoft.com/fwlink/?LinkId=317598
[GitHub]: https://github.com/Azure-Samples/documentdb-net-todo-app
