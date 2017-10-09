---
title: aaaGet de slag met Azure-tabelopslag en Visual Studio verbonden Services (ASP.NET) | Microsoft Docs
description: Hoe tooget gestart met behulp van Azure-tabelopslag nadat u hebt aangesloten tooa storage-account met behulp van Visual Studio verbonden Services in een ASP.NET-project in Visual Studio
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: af81a326-18f4-4449-bc0d-e96fba27c1f8
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: kraigb
ms.openlocfilehash: 04f79db7aad60ca51c3c866da1f4b01d9e11ac52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-table-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="238d1-103">Aan de slag met Azure-tabelopslag en Visual Studio verbonden Services (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="238d1-103">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="238d1-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="238d1-104">Overview</span></span>

<span data-ttu-id="238d1-105">Azure Table storage kunt u toostore grote hoeveelheden gestructureerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="238d1-105">Azure Table storage enables you toostore large amounts of structured data.</span></span> <span data-ttu-id="238d1-106">Hallo-service is een NoSQL-gegevensarchief die geverifieerde aanroepen vanuit binnen en buiten hello Azure-cloud accepteert.</span><span class="sxs-lookup"><span data-stu-id="238d1-106">hello service is a NoSQL datastore that accepts authenticated calls from inside and outside hello Azure cloud.</span></span> <span data-ttu-id="238d1-107">Azure-tabellen zijn ideaal voor het opslaan van gestructureerde, niet-relationele gegevens.</span><span class="sxs-lookup"><span data-stu-id="238d1-107">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="238d1-108">Deze zelfstudie laat zien hoe toowrite ASP.NET-code voor enkele algemene scenario's met behulp van Azure table storage entiteiten.</span><span class="sxs-lookup"><span data-stu-id="238d1-108">This tutorial shows how toowrite ASP.NET code for some common scenarios using Azure table storage entities.</span></span> <span data-ttu-id="238d1-109">Deze scenario's omvatten maken van een tabel en toe te voegen, het uitvoeren van query's en het verwijderen van tabelentiteiten.</span><span class="sxs-lookup"><span data-stu-id="238d1-109">These scenarios include creating a table, and adding, querying, and deleting table entities.</span></span> 

##<a name="prerequisites"></a><span data-ttu-id="238d1-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="238d1-110">Prerequisites</span></span>

* [<span data-ttu-id="238d1-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="238d1-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="238d1-112">Azure Storage-account</span><span class="sxs-lookup"><span data-stu-id="238d1-112">Azure storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="238d1-113">Maken van een MVC-controller</span><span class="sxs-lookup"><span data-stu-id="238d1-113">Create an MVC controller</span></span> 

1. <span data-ttu-id="238d1-114">In Hallo **Solution Explorer**, met de rechtermuisknop op **domeincontrollers**, en selecteer in het contextmenu hello, **toevoegen -> Controller**.</span><span class="sxs-lookup"><span data-stu-id="238d1-114">In hello **Solution Explorer**, right-click **Controllers**, and, from hello context menu, select **Add->Controller**.</span></span>

    ![Een controller tooan ASP.NET MVC-app toevoegen](./media/vs-storage-aspnet-getting-started-tables/add-controller-menu.png)

1. <span data-ttu-id="238d1-116">Op Hallo **Add Scaffold** dialoogvenster Selecteer **MVC 5 Controller - leeg**, en selecteer **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="238d1-116">On hello **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![Geef een MVC-controller](./media/vs-storage-aspnet-getting-started-tables/add-controller.png)

1. <span data-ttu-id="238d1-118">Op Hallo **Controller toevoegen** dialoogvenster, naam Hallo controller *TablesController*, en selecteer **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="238d1-118">On hello **Add Controller** dialog, name hello controller *TablesController*, and select **Add**.</span></span>

    ![Naam Hallo MVC-controller](./media/vs-storage-aspnet-getting-started-tables/add-controller-name.png)

1. <span data-ttu-id="238d1-120">Voeg de volgende Hallo *met* richtlijnen toohello `TablesController.cs` bestand:</span><span class="sxs-lookup"><span data-stu-id="238d1-120">Add hello following *using* directives toohello `TablesController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Table;
    ```

### <a name="create-a-model-class"></a><span data-ttu-id="238d1-121">Maak een modelklasse</span><span class="sxs-lookup"><span data-stu-id="238d1-121">Create a model class</span></span>

<span data-ttu-id="238d1-122">Veel van Hallo voorbeelden in dit artikel gebruik een **TableEntity**-afgeleide klasse aangeroepen **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="238d1-122">Many of hello examples in this article use a **TableEntity**-derived class called **CustomerEntity**.</span></span> <span data-ttu-id="238d1-123">Hallo stappen volgen helpt u bij het declareren van deze klasse als een modelklasse:</span><span class="sxs-lookup"><span data-stu-id="238d1-123">hello following steps guide you through declaring this class as a model class:</span></span>

1. <span data-ttu-id="238d1-124">In Hallo **Solution Explorer**, met de rechtermuisknop op **modellen**, en selecteer in het contextmenu hello, **toevoegen -> klasse**.</span><span class="sxs-lookup"><span data-stu-id="238d1-124">In hello **Solution Explorer**, right-click **Models**, and, from hello context menu, select **Add->Class**.</span></span>

1. <span data-ttu-id="238d1-125">Op Hallo **Add New Item** dialoogvenster, naam Hallo klasse, **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="238d1-125">On hello **Add New Item** dialog, name hello class, **CustomerEntity**.</span></span>

1. <span data-ttu-id="238d1-126">Open Hallo `CustomerEntity.cs` bestand en voeg de volgende Hallo **met** richtlijn:</span><span class="sxs-lookup"><span data-stu-id="238d1-126">Open hello `CustomerEntity.cs` file, and add hello following **using** directive:</span></span>

    ```csharp
    using Microsoft.WindowsAzure.Storage.Table;
    ```

1. <span data-ttu-id="238d1-127">Hallo klasse zodanig aanpassen dat, als u klaar bent Hallo klasse zoals in de volgende code Hallo is gedeclareerd.</span><span class="sxs-lookup"><span data-stu-id="238d1-127">Modify hello class so that, when finished, hello class is declared as in hello following code.</span></span> <span data-ttu-id="238d1-128">Hallo klasse declareert een entiteitsklasse aangeroepen **CustomerEntity** dat wordt gebruikt de voornaam van de klant als de rijsleutel Hallo- en achternaam als partitiesleutel Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="238d1-128">hello class declares an entity class called **CustomerEntity** that uses hello customer's first name as hello row key and last name as hello partition key.</span></span>

    ```csharp
    public class CustomerEntity : TableEntity
    {
        public CustomerEntity(string lastName, string firstName)
        {
            this.PartitionKey = lastName;
            this.RowKey = firstName;
        }

        public CustomerEntity() { }

        public string Email { get; set; }
    }
    ```

## <a name="create-a-table"></a><span data-ttu-id="238d1-129">Een tabel maken</span><span class="sxs-lookup"><span data-stu-id="238d1-129">Create a table</span></span>

<span data-ttu-id="238d1-130">Hallo volgende stappen laten zien hoe toocreate een tabel:</span><span class="sxs-lookup"><span data-stu-id="238d1-130">hello following steps illustrate how toocreate a table:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="238d1-131">Deze sectie wordt ervan uitgegaan dat u de stappen in Hallo hebt voltooid [Hallo ontwikkelomgeving instellen](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="238d1-131">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="238d1-132">Open Hallo `TablesController.cs` bestand.</span><span class="sxs-lookup"><span data-stu-id="238d1-132">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="238d1-133">Toevoegen van een methode aangeroepen **CreateTable** die retourneert een **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="238d1-133">Add a method called **CreateTable** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateTable()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="238d1-134">Binnen Hallo **CreateTable** methode, krijgen een **CloudStorageAccount** -object met gegevens over uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="238d1-134">Within hello **CreateTable** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="238d1-135">Gebruik Hallo volgende code tooget Hallo opslag tekenreeks en storage-account verbindingsinformatie van hello Azure serviceconfiguratie: (wijziging  *&lt;storage-account-name >* toohello-naam van hello Azure-opslag account die u toegang hebt.)</span><span class="sxs-lookup"><span data-stu-id="238d1-135">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="238d1-136">Ophalen van een **CloudTableClient** object vertegenwoordigt een tabelserviceclient.</span><span class="sxs-lookup"><span data-stu-id="238d1-136">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="238d1-137">Ophalen van een **CloudTable** -object met een tabelnaam verwijzing toohello gewenste.</span><span class="sxs-lookup"><span data-stu-id="238d1-137">Get a **CloudTable** object that represents a reference toohello desired table name.</span></span> <span data-ttu-id="238d1-138">Hallo **CloudTableClient.GetTableReference** methode maakt u niet een aanvraag in voor de tabelopslag.</span><span class="sxs-lookup"><span data-stu-id="238d1-138">hello **CloudTableClient.GetTableReference** method does not make a request against table storage.</span></span> <span data-ttu-id="238d1-139">Hallo verwijzing wordt geretourneerd of Hallo tabel bestaat of niet.</span><span class="sxs-lookup"><span data-stu-id="238d1-139">hello reference is returned whether or not hello table exists.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="238d1-140">Hallo aanroepen **CloudTable.CreateIfNotExists** methode toocreate Hallo tabel als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="238d1-140">Call hello **CloudTable.CreateIfNotExists** method toocreate hello table if it does not yet exist.</span></span> <span data-ttu-id="238d1-141">Hallo **CloudTable.CreateIfNotExists** methode retourneert **true** als Hallo tabel niet bestaat en is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="238d1-141">hello **CloudTable.CreateIfNotExists** method returns **true** if hello table does not exist, and is successfully created.</span></span> <span data-ttu-id="238d1-142">Anders **false** wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="238d1-142">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = table.CreateIfNotExists();
    ```

1. <span data-ttu-id="238d1-143">Update Hallo **ViewBag** met de naam van de tabel Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="238d1-143">Update hello **ViewBag** with hello name of hello table.</span></span>

    ```csharp
    ViewBag.TableName = table.Name;
    ```

1. <span data-ttu-id="238d1-144">In Hallo **Solution Explorer**, vouw Hallo **weergaven** map met de rechtermuisknop op **tabellen**, en selecteer in het contextmenu hello, **toevoegen -> weergave**.</span><span class="sxs-lookup"><span data-stu-id="238d1-144">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="238d1-145">Op Hallo **weergave toevoegen** dialoogvenster Voer **CreateTable** voor Hallo weergavenaam en selecteer **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="238d1-145">On hello **Add View** dialog, enter **CreateTable** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="238d1-146">Open `CreateTable.cshtml`, en dit zodanig aanpassen dat het lijkt erop dat het volgende codefragment Hallo:</span><span class="sxs-lookup"><span data-stu-id="238d1-146">Open `CreateTable.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Table";
    }
    
    <h2>Create Table results</h2>

    Creation of @ViewBag.TableName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="238d1-147">In Hallo **Solution Explorer**, vouw Hallo **weergaven -> gedeelde** map en open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="238d1-147">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="238d1-148">Na het Hallo laatste **Html.ActionLink**, voeg de volgende Hallo **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="238d1-148">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create table", "CreateTable", "Tables")</li>
    ```

1. <span data-ttu-id="238d1-149">Voer Hallo toepassing uit en selecteer **tabel maken** toosee resulteert vergelijkbare toohello schermopname te volgen:</span><span class="sxs-lookup"><span data-stu-id="238d1-149">Run hello application, and select **Create table** toosee results similar toohello following screen shot:</span></span>
  
    ![Tabel maken](./media/vs-storage-aspnet-getting-started-tables/create-table-results.png)

    <span data-ttu-id="238d1-151">Zoals eerder vermeld, Hallo **CloudTable.CreateIfNotExists** methode retourneert **true** alleen wanneer Hallo tabel bestaat niet en is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="238d1-151">As mentioned previously, hello **CloudTable.CreateIfNotExists** method returns **true** only when hello table doesn't exist and is created.</span></span> <span data-ttu-id="238d1-152">Dus als u Hallo app uitvoeren wanneer Hallo tabel bestaat, Hallo methode retourneert **false**.</span><span class="sxs-lookup"><span data-stu-id="238d1-152">Therefore, if you run hello app when hello table exists, hello method returns **false**.</span></span> <span data-ttu-id="238d1-153">toorun hello app meerdere keren, verwijdert u Hallo tabel voordat Hallo app opnieuw uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="238d1-153">toorun hello app multiple times, you must delete hello table before running hello app again.</span></span> <span data-ttu-id="238d1-154">Verwijderen Hallo tabel kan worden uitgevoerd via Hallo **CloudTable.Delete** methode.</span><span class="sxs-lookup"><span data-stu-id="238d1-154">Deleting hello table can be done via hello **CloudTable.Delete** method.</span></span> <span data-ttu-id="238d1-155">U kunt ook met Hallo Hallo-tabel verwijderen [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) of Hallo [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="238d1-155">You can also delete hello table using hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="238d1-156">Een entiteit tooa tabel toevoegen</span><span class="sxs-lookup"><span data-stu-id="238d1-156">Add an entity tooa table</span></span>

<span data-ttu-id="238d1-157">*Entiteiten* toewijzen tooC\# objecten met behulp van een aangepaste klasse wordt afgeleid van **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="238d1-157">*Entities* map tooC\# objects by using a custom class derived from **TableEntity**.</span></span> <span data-ttu-id="238d1-158">tooadd een entiteit tooa tabel, maak een klasse die eigenschappen Hallo van uw entiteit definieert.</span><span class="sxs-lookup"><span data-stu-id="238d1-158">tooadd an entity tooa table, create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="238d1-159">In deze sectie ziet u hoe toodefine een entiteitsklasse die gebruikmaakt van de voornaam van de klant als de rijsleutel Hallo- en achternaam als partitiesleutel Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="238d1-159">In this section, you'll see how toodefine an entity class that uses hello customer's first name as hello row key and last name as hello partition key.</span></span> <span data-ttu-id="238d1-160">Samen een entiteit partitie en rijsleutel een unieke identificatie Hallo entiteit in Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="238d1-160">Together, an entity's partition and row key uniquely identify hello entity in hello table.</span></span> <span data-ttu-id="238d1-161">Entiteiten met dezelfde partitiesleutel kunnen sneller worden opgevraagd dan entiteiten met verschillende partitiesleutels, maar het gebruik van verschillende partitiesleutels maakt een grotere schaalbaarheid van parallelle bewerkingen mogelijk.</span><span class="sxs-lookup"><span data-stu-id="238d1-161">Entities with the same partition key can be queried faster than entities with different partition keys, but using diverse partition keys allows for greater scalability of parallel operations.</span></span> <span data-ttu-id="238d1-162">Voor alle eigenschappen die moet worden opgeslagen in de tabelservice hello, moet Hallo eigenschap een openbare eigenschap van een ondersteund type dat toegang biedt tot zowel instellen en ophalen van waarden.</span><span class="sxs-lookup"><span data-stu-id="238d1-162">For any property that should be stored in hello table service, hello property must be a public property of a supported type that exposes both setting and retrieving values.</span></span>
<span data-ttu-id="238d1-163">Hallo entiteitsklasse *moet* declareren van een openbare parameterloze constructor.</span><span class="sxs-lookup"><span data-stu-id="238d1-163">hello entity class *must* declare a public parameter-less constructor.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="238d1-164">Deze sectie wordt ervan uitgegaan dat u de stappen in Hallo hebt voltooid [Hallo ontwikkelomgeving instellen](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="238d1-164">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment).</span></span>

1. <span data-ttu-id="238d1-165">Open Hallo `TablesController.cs` bestand.</span><span class="sxs-lookup"><span data-stu-id="238d1-165">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="238d1-166">Toevoegen van de volgende richtlijn zodat die de code in Hallo HALLO hallo `TablesController.cs` bestand heeft toegang tot Hallo **CustomerEntity** klasse:</span><span class="sxs-lookup"><span data-stu-id="238d1-166">Add hello following directive so that hello code in hello `TablesController.cs` file can access hello **CustomerEntity** class:</span></span>

    ```csharp
    using StorageAspnet.Models;
    ```

1. <span data-ttu-id="238d1-167">Toevoegen van een methode aangeroepen **AddEntity** die retourneert een **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="238d1-167">Add a method called **AddEntity** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddEntity()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="238d1-168">Binnen Hallo **AddEntity** methode, krijgen een **CloudStorageAccount** -object met gegevens over uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="238d1-168">Within hello **AddEntity** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="238d1-169">Gebruik Hallo volgende code tooget Hallo opslag tekenreeks en storage-account verbindingsinformatie van hello Azure serviceconfiguratie: (wijziging  *&lt;storage-account-name >* toohello-naam van hello Azure-opslag account die u toegang hebt.)</span><span class="sxs-lookup"><span data-stu-id="238d1-169">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="238d1-170">Ophalen van een **CloudTableClient** object vertegenwoordigt een tabelserviceclient.</span><span class="sxs-lookup"><span data-stu-id="238d1-170">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="238d1-171">Ophalen van een **CloudTable** -object met een verwijzing toohello tabel toowhich u gaat tooadd Hallo nieuwe entiteit.</span><span class="sxs-lookup"><span data-stu-id="238d1-171">Get a **CloudTable** object that represents a reference toohello table toowhich you are going tooadd hello new entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="238d1-172">Exemplaar maken en initialiseren Hallo **CustomerEntity** klasse.</span><span class="sxs-lookup"><span data-stu-id="238d1-172">Instantiate and initialize hello **CustomerEntity** class.</span></span>

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    ```

1. <span data-ttu-id="238d1-173">Maak een **TableOperation** -object dat wordt ingevoegd Hallo klantentiteit.</span><span class="sxs-lookup"><span data-stu-id="238d1-173">Create a **TableOperation** object that inserts hello customer entity.</span></span>

    ```csharp
    TableOperation insertOperation = TableOperation.Insert(customer1);
    ```

1. <span data-ttu-id="238d1-174">Hallo insert-bewerking uitvoeren door de aanroepende Hallo **CloudTable.Execute** methode.</span><span class="sxs-lookup"><span data-stu-id="238d1-174">Execute hello insert operation by calling hello **CloudTable.Execute** method.</span></span> <span data-ttu-id="238d1-175">U kunt Hallo resultaat van Hallo-bewerking controleren door te inspecteren Hallo **TableResult.HttpStatusCode** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="238d1-175">You can verify hello result of hello operation by inspecting hello **TableResult.HttpStatusCode** property.</span></span> <span data-ttu-id="238d1-176">Statuscode 2xx geeft Hallo actie aangevraagd door Hallo-client is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="238d1-176">A status code of 2xx indicates hello action requested by hello client was processed successfully.</span></span> <span data-ttu-id="238d1-177">Geslaagde invoegingen van nieuwe entiteiten resulteert bijvoorbeeld in een HTTP-statuscode van 204, wat betekent dat Hallo bewerking met succes is verwerkt en Hallo-server heeft geen inhoud geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="238d1-177">For example, successful insertions of new entities results in an HTTP status code of 204, meaning that hello operation was successfully processed and hello server did not return any content.</span></span>

    ```csharp
    TableResult result = table.Execute(insertOperation);
    ```

1. <span data-ttu-id="238d1-178">Update Hallo **ViewBag** met Hallo tabelnaam en de resultaten van de Hallo van Hallo insert-bewerking.</span><span class="sxs-lookup"><span data-stu-id="238d1-178">Update hello **ViewBag** with hello table name, and hello results of hello insert operation.</span></span>

    ```csharp
    ViewBag.TableName = table.Name;
    ViewBag.Result = result.HttpStatusCode;
    ```

1. <span data-ttu-id="238d1-179">In Hallo **Solution Explorer**, vouw Hallo **weergaven** map met de rechtermuisknop op **tabellen**, en selecteer in het contextmenu hello, **toevoegen -> weergave**.</span><span class="sxs-lookup"><span data-stu-id="238d1-179">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="238d1-180">Op Hallo **weergave toevoegen** dialoogvenster Voer **AddEntity** voor Hallo weergavenaam en selecteer **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="238d1-180">On hello **Add View** dialog, enter **AddEntity** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="238d1-181">Open `AddEntity.cshtml`, en dit zodanig aanpassen dat het lijkt erop dat het volgende codefragment Hallo:</span><span class="sxs-lookup"><span data-stu-id="238d1-181">Open `AddEntity.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Add entity";
    }
    
    <h2>Add entity results</h2>

    Insert of entity into @ViewBag.TableName @(ViewBag.Result == 204 ? "succeeded" : "failed")
    ```
1. <span data-ttu-id="238d1-182">In Hallo **Solution Explorer**, vouw Hallo **weergaven -> gedeelde** map en open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="238d1-182">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="238d1-183">Na het Hallo laatste **Html.ActionLink**, voeg de volgende Hallo **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="238d1-183">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add entity", "AddEntity", "Tables")</li>
    ```

1. <span data-ttu-id="238d1-184">Voer Hallo toepassing uit en selecteer **entiteit toevoegen** toosee resulteert vergelijkbare toohello schermopname te volgen:</span><span class="sxs-lookup"><span data-stu-id="238d1-184">Run hello application, and select **Add entity** toosee results similar toohello following screen shot:</span></span>
  
    ![Entiteit toevoegen](./media/vs-storage-aspnet-getting-started-tables/add-entity-results.png)

    <span data-ttu-id="238d1-186">U kunt controleren of Hallo entiteit is toegevoegd door Hallo stappen in de sectie Hallo [één entiteit ophalen](#get-a-single-entity).</span><span class="sxs-lookup"><span data-stu-id="238d1-186">You can verify that hello entity was added by following hello steps in hello section, [Get a single entity](#get-a-single-entity).</span></span> <span data-ttu-id="238d1-187">U kunt ook Hallo [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview alle Hallo entiteiten voor de tabellen.</span><span class="sxs-lookup"><span data-stu-id="238d1-187">You can also use hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview all hello entities for your tables.</span></span>

## <a name="add-a-batch-of-entities-tooa-table"></a><span data-ttu-id="238d1-188">Een batch entiteiten tooa tabel toevoegen</span><span class="sxs-lookup"><span data-stu-id="238d1-188">Add a batch of entities tooa table</span></span>

<span data-ttu-id="238d1-189">In aanvulling toobeing kunnen te[toevoegen van een entiteit tooa tabel 1 tegelijk](#add-an-entity-to-a-table), u kunt ook entiteiten in batch toevoegen.</span><span class="sxs-lookup"><span data-stu-id="238d1-189">In addition toobeing able too[add an entity tooa table one at a time](#add-an-entity-to-a-table), you can also add entities in batch.</span></span> <span data-ttu-id="238d1-190">Toevoegen van entiteiten in batch vermindert Hallo aantal retourbewerkingen tussen uw code en hello Azure table-service.</span><span class="sxs-lookup"><span data-stu-id="238d1-190">Adding entities in batch reduces hello number of round-trips between your code and hello Azure table service.</span></span> <span data-ttu-id="238d1-191">Hallo stappen te volgen laten zien hoe tooadd meerdere entiteiten tooa tabel met een enkele insert-bewerking:</span><span class="sxs-lookup"><span data-stu-id="238d1-191">hello following steps illustrate how tooadd multiple entities tooa table with a single insert operation:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="238d1-192">Deze sectie wordt ervan uitgegaan dat u de stappen in Hallo hebt voltooid [Hallo ontwikkelomgeving instellen](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="238d1-192">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment).</span></span>

1. <span data-ttu-id="238d1-193">Open Hallo `TablesController.cs` bestand.</span><span class="sxs-lookup"><span data-stu-id="238d1-193">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="238d1-194">Toevoegen van een methode aangeroepen **AddEntities** die retourneert een **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="238d1-194">Add a method called **AddEntities** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddEntities()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="238d1-195">Binnen Hallo **AddEntities** methode, krijgen een **CloudStorageAccount** -object met gegevens over uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="238d1-195">Within hello **AddEntities** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="238d1-196">Gebruik Hallo volgende code tooget Hallo opslag tekenreeks en storage-account verbindingsinformatie van hello Azure serviceconfiguratie: (wijziging  *&lt;storage-account-name >* toohello-naam van hello Azure-opslag account die u toegang hebt.)</span><span class="sxs-lookup"><span data-stu-id="238d1-196">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="238d1-197">Ophalen van een **CloudTableClient** object vertegenwoordigt een tabelserviceclient.</span><span class="sxs-lookup"><span data-stu-id="238d1-197">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="238d1-198">Ophalen van een **CloudTable** -object met een verwijzing toohello tabel toowhich u gaat tooadd Hallo nieuwe entiteiten zijn.</span><span class="sxs-lookup"><span data-stu-id="238d1-198">Get a **CloudTable** object that represents a reference toohello table toowhich you are going tooadd hello new entities.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="238d1-199">Exemplaar maken van een klantobjecten op basis van Hallo **CustomerEntity** modelklasse weergegeven in de sectie Hallo [toevoegen van een tabel entity tooa](#add-an-entity-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="238d1-199">Instantiate some customer objects based on hello **CustomerEntity** model class presented in hello section, [Add an entity tooa table](#add-an-entity-to-a-table).</span></span>

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
    customer1.Email = "Jeff@contoso.com";

    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.Email = "Ben@contoso.com";
    ```

1. <span data-ttu-id="238d1-200">Ophalen van een **TableBatchOperation** object.</span><span class="sxs-lookup"><span data-stu-id="238d1-200">Get a **TableBatchOperation** object.</span></span>

    ```csharp
    TableBatchOperation batchOperation = new TableBatchOperation();
    ```

1. <span data-ttu-id="238d1-201">Entiteiten toohello batch insert-bewerking object toevoegen.</span><span class="sxs-lookup"><span data-stu-id="238d1-201">Add entities toohello batch insert operation object.</span></span>

    ```csharp
    batchOperation.Insert(customer1);
    batchOperation.Insert(customer2);
    ```

1. <span data-ttu-id="238d1-202">Hallo batch insert-bewerking uitvoeren door de aanroepende Hallo **CloudTable.ExecuteBatch** methode.</span><span class="sxs-lookup"><span data-stu-id="238d1-202">Execute hello batch insert operation by calling hello **CloudTable.ExecuteBatch** method.</span></span>   

    ```csharp
    IList<TableResult> results = table.ExecuteBatch(batchOperation);
    ```

1. <span data-ttu-id="238d1-203">Hallo **CloudTable.ExecuteBatch** methode retourneert een lijst met **TableResult** objecten waar elke **TableResult** -object wordt onderzocht toodetermine Hallo slagen of mislukken van elke afzonderlijke bewerking.</span><span class="sxs-lookup"><span data-stu-id="238d1-203">hello **CloudTable.ExecuteBatch** method returns a list of **TableResult** objects where each **TableResult** object can be examined toodetermine hello success or failure of each individual operation.</span></span> <span data-ttu-id="238d1-204">In dit voorbeeld Hallo tooa lijstweergave doorgeven en laat Hallo weergave Hallo resultaten van elke bewerking weer te geven.</span><span class="sxs-lookup"><span data-stu-id="238d1-204">For this example, pass hello list tooa view and let hello view display hello results of each operation.</span></span> 
 
    ```csharp
    return View(results);
    ```

1. <span data-ttu-id="238d1-205">In Hallo **Solution Explorer**, vouw Hallo **weergaven** map met de rechtermuisknop op **tabellen**, en selecteer in het contextmenu hello, **toevoegen -> weergave**.</span><span class="sxs-lookup"><span data-stu-id="238d1-205">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="238d1-206">Op Hallo **weergave toevoegen** dialoogvenster Voer **AddEntities** voor Hallo weergavenaam en selecteer **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="238d1-206">On hello **Add View** dialog, enter **AddEntities** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="238d1-207">Open `AddEntities.cshtml`, en zodat het lijkt erop dat de volgende hello te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="238d1-207">Open `AddEntities.cshtml`, and modify it so that it looks like hello following.</span></span>

    ```csharp
    @model IEnumerable<Microsoft.WindowsAzure.Storage.Table.TableResult>
    @{
        ViewBag.Title = "AddEntities";
    }
    
    <h2>Add-entities results</h2>
    
    <table border="1">
        <tr>
            <th>First name</th>
            <th>Last name</th>
            <th>HTTP result</th>
        </tr>
        @foreach (var result in Model)
        {
        <tr>
            <td>@((result.Result as StorageAspnet.Models.CustomerEntity).RowKey)</td>
            <td>@((result.Result as StorageAspnet.Models.CustomerEntity).PartitionKey)</td>
            <td>@result.HttpStatusCode</td>
        </tr>
        }
    </table>
    ```

1. <span data-ttu-id="238d1-208">In Hallo **Solution Explorer**, vouw Hallo **weergaven -> gedeelde** map en open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="238d1-208">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="238d1-209">Na het Hallo laatste **Html.ActionLink**, voeg de volgende Hallo **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="238d1-209">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add entities", "AddEntities", "Tables")</li>
    ```

1. <span data-ttu-id="238d1-210">Voer Hallo toepassing uit en selecteer **entiteiten toevoegen** toosee resulteert vergelijkbare toohello schermopname te volgen:</span><span class="sxs-lookup"><span data-stu-id="238d1-210">Run hello application, and select **Add entities** toosee results similar toohello following screen shot:</span></span>
  
    ![Entiteiten toevoegen](./media/vs-storage-aspnet-getting-started-tables/add-entities-results.png)

    <span data-ttu-id="238d1-212">U kunt controleren of Hallo entiteit is toegevoegd door Hallo stappen in de sectie Hallo [één entiteit ophalen](#get-a-single-entity).</span><span class="sxs-lookup"><span data-stu-id="238d1-212">You can verify that hello entity was added by following hello steps in hello section, [Get a single entity](#get-a-single-entity).</span></span> <span data-ttu-id="238d1-213">U kunt ook Hallo [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview alle Hallo entiteiten voor de tabellen.</span><span class="sxs-lookup"><span data-stu-id="238d1-213">You can also use hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview all hello entities for your tables.</span></span>

## <a name="get-a-single-entity"></a><span data-ttu-id="238d1-214">Één entiteit ophalen</span><span class="sxs-lookup"><span data-stu-id="238d1-214">Get a single entity</span></span>

<span data-ttu-id="238d1-215">Deze sectie ziet u hoe tooget vanuit een tabel met één entiteit Hallo rijsleutel en de partitiesleutel van entiteit.</span><span class="sxs-lookup"><span data-stu-id="238d1-215">This section illustrates how tooget a single entity from a table using hello entity's row key and partition key.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="238d1-216">Deze sectie wordt ervan uitgegaan dat u de stappen in Hallo hebt voltooid [Hallo ontwikkelomgeving instellen](#set-up-the-development-environment), en maakt gebruik van gegevens van [toevoegen van een batch entiteiten tooa tabel](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="238d1-216">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="238d1-217">Open Hallo `TablesController.cs` bestand.</span><span class="sxs-lookup"><span data-stu-id="238d1-217">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="238d1-218">Toevoegen van een methode aangeroepen **GetSingle** die retourneert een **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="238d1-218">Add a method called **GetSingle** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetSingle()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="238d1-219">Binnen Hallo **GetSingle** methode, krijgen een **CloudStorageAccount** -object met gegevens over uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="238d1-219">Within hello **GetSingle** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="238d1-220">Gebruik Hallo volgende code tooget Hallo opslag tekenreeks en storage-account verbindingsinformatie van hello Azure serviceconfiguratie: (wijziging  *&lt;storage-account-name >* toohello-naam van hello Azure-opslag account die u toegang hebt.)</span><span class="sxs-lookup"><span data-stu-id="238d1-220">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="238d1-221">Ophalen van een **CloudTableClient** object vertegenwoordigt een tabelserviceclient.</span><span class="sxs-lookup"><span data-stu-id="238d1-221">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="238d1-222">Ophalen van een **CloudTable** -object met een verwijzingstabel toohello van waaruit u Hallo entiteit ophalen.</span><span class="sxs-lookup"><span data-stu-id="238d1-222">Get a **CloudTable** object that represents a reference toohello table from which you are retrieving hello entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="238d1-223">Maakt een ophalen bewerking object waarvoor een entiteitsobject afgeleid van **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="238d1-223">Create a retrieve operation object that takes an entity object derived from **TableEntity**.</span></span> <span data-ttu-id="238d1-224">de eerste parameter Hallo is Hallo *partitionKey*, en de tweede parameter Hallo Hallo *rowKey*.</span><span class="sxs-lookup"><span data-stu-id="238d1-224">hello first parameter is hello *partitionKey*, and hello second parameter is hello *rowKey*.</span></span> <span data-ttu-id="238d1-225">Met behulp van Hallo **CustomerEntity** klasse en gegevens die zijn gepresenteerd in de sectie Hallo [toevoegen van een batch entiteiten tooa tabel](#add-a-batch-of-entities-to-a-table), Hallo na code codefragment query's Hallo tabel voor een **CustomerEntity** entiteit met een *partitionKey* waarde van 'Smith' en een *rowKey* waarde van 'Ben':</span><span class="sxs-lookup"><span data-stu-id="238d1-225">Using hello **CustomerEntity** class and data presented in hello section [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table), hello following code snippet queries hello table for a **CustomerEntity** entity with a *partitionKey* value of "Smith" and a *rowKey* value of "Ben":</span></span>

    ```csharp
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");
    ```

1. <span data-ttu-id="238d1-226">Hallo ophalen bewerking niet uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="238d1-226">Execute hello retrieve operation.</span></span>   

    ```csharp
    TableResult result = table.Execute(retrieveOperation);
    ```

1. <span data-ttu-id="238d1-227">Hallo resultaat toohello weergeven voor weergave doorgeven.</span><span class="sxs-lookup"><span data-stu-id="238d1-227">Pass hello result toohello view for display.</span></span>

    ```csharp
    return View(result);
    ```

1. <span data-ttu-id="238d1-228">In Hallo **Solution Explorer**, vouw Hallo **weergaven** map met de rechtermuisknop op **tabellen**, en selecteer in het contextmenu hello, **toevoegen -> weergave**.</span><span class="sxs-lookup"><span data-stu-id="238d1-228">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="238d1-229">Op Hallo **weergave toevoegen** dialoogvenster Voer **GetSingle** voor Hallo weergavenaam en selecteer **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="238d1-229">On hello **Add View** dialog, enter **GetSingle** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="238d1-230">Open `GetSingle.cshtml`, en dit zodanig aanpassen dat het lijkt erop dat het volgende codefragment Hallo:</span><span class="sxs-lookup"><span data-stu-id="238d1-230">Open `GetSingle.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @model Microsoft.WindowsAzure.Storage.Table.TableResult
    @{
        ViewBag.Title = "GetSingle";
    }
    
    <h2>Get Single results</h2>
    
    <table border="1">
        <tr>
            <th>HTTP result</th>
            <th>First name</th>
            <th>Last name</th>
            <th>Email</th>
        </tr>
        <tr>
            <td>@Model.HttpStatusCode</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).RowKey)</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).PartitionKey)</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).Email)</td>
        </tr>
    </table>
    ```

1. <span data-ttu-id="238d1-231">In Hallo **Solution Explorer**, vouw Hallo **weergaven -> gedeelde** map en open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="238d1-231">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="238d1-232">Na het Hallo laatste **Html.ActionLink**, voeg de volgende Hallo **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="238d1-232">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get single", "GetSingle", "Tables")</li>
    ```

1. <span data-ttu-id="238d1-233">Voer Hallo toepassing uit en selecteer **één ophalen** toosee resulteert vergelijkbare toohello schermopname te volgen:</span><span class="sxs-lookup"><span data-stu-id="238d1-233">Run hello application, and select **Get Single** toosee results similar toohello following screen shot:</span></span>
  
    ![Één ophalen](./media/vs-storage-aspnet-getting-started-tables/get-single-results.png)

## <a name="get-all-entities-in-a-partition"></a><span data-ttu-id="238d1-235">Alle entiteiten in een partitie ophalen</span><span class="sxs-lookup"><span data-stu-id="238d1-235">Get all entities in a partition</span></span>

<span data-ttu-id="238d1-236">Zoals vermeld in de sectie hello, [toevoegen van een tabel entity tooa](#add-an-entity-to-a-table), Hallo combinatie van een partitie en een rijsleutel unieke identificatie van een entiteit in een tabel.</span><span class="sxs-lookup"><span data-stu-id="238d1-236">As mentioned in hello section, [Add an entity tooa table](#add-an-entity-to-a-table), hello combination of a partition and a row key uniquely identify an entity in a table.</span></span> <span data-ttu-id="238d1-237">Entiteiten met dezelfde partitiesleutel kunnen sneller worden opgevraagd dan entiteiten met verschillende partitiesleutels.</span><span class="sxs-lookup"><span data-stu-id="238d1-237">Entities with the same partition key can be queried faster than entities with different partition keys.</span></span> <span data-ttu-id="238d1-238">Deze sectie ziet u hoe tooquery een tabel voor alle Hallo entiteiten van een opgegeven partitie.</span><span class="sxs-lookup"><span data-stu-id="238d1-238">This section illustrates how tooquery a table for all hello entities from a specified partition.</span></span>  

> [!NOTE]
> 
> <span data-ttu-id="238d1-239">Deze sectie wordt ervan uitgegaan dat u de stappen in Hallo hebt voltooid [Hallo ontwikkelomgeving instellen](#set-up-the-development-environment), en maakt gebruik van gegevens van [toevoegen van een batch entiteiten tooa tabel](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="238d1-239">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="238d1-240">Open Hallo `TablesController.cs` bestand.</span><span class="sxs-lookup"><span data-stu-id="238d1-240">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="238d1-241">Toevoegen van een methode aangeroepen **GetPartition** die retourneert een **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="238d1-241">Add a method called **GetPartition** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetPartition()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="238d1-242">Binnen Hallo **GetPartition** methode, krijgen een **CloudStorageAccount** -object met gegevens over uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="238d1-242">Within hello **GetPartition** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="238d1-243">Gebruik Hallo volgende code tooget Hallo opslag tekenreeks en storage-account verbindingsinformatie van hello Azure serviceconfiguratie: (wijziging  *&lt;storage-account-name >* toohello-naam van hello Azure-opslag account die u toegang hebt.)</span><span class="sxs-lookup"><span data-stu-id="238d1-243">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="238d1-244">Ophalen van een **CloudTableClient** object vertegenwoordigt een tabelserviceclient.</span><span class="sxs-lookup"><span data-stu-id="238d1-244">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="238d1-245">Ophalen van een **CloudTable** -object met een verwijzingstabel toohello van waaruit u Hallo entiteiten ophalen.</span><span class="sxs-lookup"><span data-stu-id="238d1-245">Get a **CloudTable** object that represents a reference toohello table from which you are retrieving hello entities.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="238d1-246">Exemplaar maken van een **TableQuery** object Hallo query opgeven in Hallo **waar** component.</span><span class="sxs-lookup"><span data-stu-id="238d1-246">Instantiate a **TableQuery** object specifying hello query in hello **Where** clause.</span></span> <span data-ttu-id="238d1-247">Met behulp van Hallo **CustomerEntity** klasse en gegevens die zijn gepresenteerd in de sectie Hallo [toevoegen van een batch entiteiten tooa tabel](#add-a-batch-of-entities-to-a-table), Hallo volgende codefragment query's Hallo tabel voor een alle entiteiten code waarbij hello  **PartitionKey** (achternaam van de klant) heeft de waarde 'Smith':</span><span class="sxs-lookup"><span data-stu-id="238d1-247">Using hello **CustomerEntity** class and data presented in hello section [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table), hello following code snippet queries hello table for a all entities where hello **PartitionKey** (customer's last name) has a value of "Smith":</span></span>

    ```csharp
    TableQuery<CustomerEntity> query = 
        new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));
    ```

1. <span data-ttu-id="238d1-248">Aanroepen in een lus Hallo **CloudTable.ExecuteQuerySegmented** methode Hallo u geïnstantieerd query-object in de vorige stap hello wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="238d1-248">Within a loop, call hello **CloudTable.ExecuteQuerySegmented** method passing hello query object you instantiated in hello previous step.</span></span>  <span data-ttu-id="238d1-249">Hallo **CloudTable.ExecuteQuerySegmented** methode retourneert een **TableContinuationToken** die - object als **null** -geeft aan dat er geen entiteiten meer tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="238d1-249">hello **CloudTable.ExecuteQuerySegmented** method returns a **TableContinuationToken** object that - when **null** - indicates that there are no more entities tooretrieve.</span></span> <span data-ttu-id="238d1-250">Binnen de lus hello, gebruiken om een andere lus tooiterate via Hallo entiteiten geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="238d1-250">Within hello loop, use another loop tooiterate over hello returned entities.</span></span> <span data-ttu-id="238d1-251">In de Hallo volgende codevoorbeeld, wordt elke geretourneerde entiteit tooa lijst toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="238d1-251">In hello following code example, each returned entity is added tooa list.</span></span> <span data-ttu-id="238d1-252">Eenmaal Hallo lus eindigt, Hallo lijst tooa weergeven voor de weergave wordt doorgegeven:</span><span class="sxs-lookup"><span data-stu-id="238d1-252">Once hello loop ends, hello list is passed tooa view for display:</span></span> 

    ```csharp
    List<CustomerEntity> customers = new List<CustomerEntity>();
    TableContinuationToken token = null;
    do
    {
        TableQuerySegment<CustomerEntity> resultSegment = table.ExecuteQuerySegmented(query, token);
        token = resultSegment.ContinuationToken;

        foreach (CustomerEntity customer in resultSegment.Results)
        {
            customers.Add(customer);
        }
    } while (token != null);

    return View(customers);
    ```

1. <span data-ttu-id="238d1-253">In Hallo **Solution Explorer**, vouw Hallo **weergaven** map met de rechtermuisknop op **tabellen**, en selecteer in het contextmenu hello, **toevoegen -> weergave**.</span><span class="sxs-lookup"><span data-stu-id="238d1-253">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="238d1-254">Op Hallo **weergave toevoegen** dialoogvenster Voer **GetPartition** voor Hallo weergavenaam en selecteer **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="238d1-254">On hello **Add View** dialog, enter **GetPartition** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="238d1-255">Open `GetPartition.cshtml`, en dit zodanig aanpassen dat het lijkt erop dat het volgende codefragment Hallo:</span><span class="sxs-lookup"><span data-stu-id="238d1-255">Open `GetPartition.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @model IEnumerable<StorageAspnet.Models.CustomerEntity>
    @{
        ViewBag.Title = "GetPartition";
    }
    
    <h2>Get Partition results</h2>
    
    <table border="1">
        <tr>
            <th>First name</th>
            <th>Last name</th>
            <th>Email</th>
        </tr>
        @foreach (var customer in Model)
        {
        <tr>
            <td>@(customer.RowKey)</td>
            <td>@(customer.PartitionKey)</td>
            <td>@(customer.Email)</td>
        </tr>
        }
    </table>
    ```

1. <span data-ttu-id="238d1-256">In Hallo **Solution Explorer**, vouw Hallo **weergaven -> gedeelde** map en open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="238d1-256">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="238d1-257">Na het Hallo laatste **Html.ActionLink**, voeg de volgende Hallo **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="238d1-257">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get partition", "GetPartition", "Tables")</li>
    ```

1. <span data-ttu-id="238d1-258">Voer Hallo toepassing uit en selecteer **partitie ophalen** toosee resulteert vergelijkbare toohello schermopname te volgen:</span><span class="sxs-lookup"><span data-stu-id="238d1-258">Run hello application, and select **Get Partition** toosee results similar toohello following screen shot:</span></span>
  
    ![Partitie ophalen](./media/vs-storage-aspnet-getting-started-tables/get-partition-results.png)

## <a name="delete-an-entity"></a><span data-ttu-id="238d1-260">Een entiteit verwijderen</span><span class="sxs-lookup"><span data-stu-id="238d1-260">Delete an entity</span></span>

<span data-ttu-id="238d1-261">Deze sectie ziet u hoe toodelete een entiteit uit een tabel.</span><span class="sxs-lookup"><span data-stu-id="238d1-261">This section illustrates how toodelete an entity from a table.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="238d1-262">Deze sectie wordt ervan uitgegaan dat u de stappen in Hallo hebt voltooid [Hallo ontwikkelomgeving instellen](#set-up-the-development-environment), en maakt gebruik van gegevens van [toevoegen van een batch entiteiten tooa tabel](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="238d1-262">This section assumes you have completed hello steps in [Set up hello development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="238d1-263">Open Hallo `TablesController.cs` bestand.</span><span class="sxs-lookup"><span data-stu-id="238d1-263">Open hello `TablesController.cs` file.</span></span>

1. <span data-ttu-id="238d1-264">Toevoegen van een methode aangeroepen **DeleteEntity** die retourneert een **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="238d1-264">Add a method called **DeleteEntity** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult DeleteEntity()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="238d1-265">Binnen Hallo **DeleteEntity** methode, krijgen een **CloudStorageAccount** -object met gegevens over uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="238d1-265">Within hello **DeleteEntity** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="238d1-266">Gebruik Hallo volgende code tooget Hallo opslag tekenreeks en storage-account verbindingsinformatie van hello Azure serviceconfiguratie: (wijziging  *&lt;storage-account-name >* toohello-naam van hello Azure-opslag account die u toegang hebt.)</span><span class="sxs-lookup"><span data-stu-id="238d1-266">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="238d1-267">Ophalen van een **CloudTableClient** object vertegenwoordigt een tabelserviceclient.</span><span class="sxs-lookup"><span data-stu-id="238d1-267">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="238d1-268">Ophalen van een **CloudTable** -object met een verwijzingstabel toohello Hallo entiteit worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="238d1-268">Get a **CloudTable** object that represents a reference toohello table from which you are deleting hello entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="238d1-269">Maakt een verwijderen bewerking object waarvoor een entiteitsobject afgeleid van **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="238d1-269">Create a delete operation object that takes an entity object derived from **TableEntity**.</span></span> <span data-ttu-id="238d1-270">In dit geval gebruiken we Hallo **CustomerEntity** klasse en gegevens die zijn gepresenteerd in de sectie Hallo [toevoegen van een batch entiteiten tooa tabel](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="238d1-270">In this case, we use hello **CustomerEntity** class and data presented in hello section [Add a batch of entities tooa table](#add-a-batch-of-entities-to-a-table).</span></span> <span data-ttu-id="238d1-271">Hallo van entiteit **ETag** tooa geldige waarde moet worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="238d1-271">hello entity's **ETag** must be set tooa valid value.</span></span>  

    ```csharp
    TableOperation deleteOperation = 
        TableOperation.Delete(new CustomerEntity("Smith", "Ben") { ETag = "*" } );
    ```

1. <span data-ttu-id="238d1-272">Hallo-delete-bewerking uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="238d1-272">Execute hello delete operation.</span></span>   

    ```csharp
    TableResult result = table.Execute(deleteOperation);
    ```

1. <span data-ttu-id="238d1-273">Hallo resultaat toohello weergeven voor weergave doorgeven.</span><span class="sxs-lookup"><span data-stu-id="238d1-273">Pass hello result toohello view for display.</span></span>

    ```csharp
    return View(result);
    ```

1. <span data-ttu-id="238d1-274">In Hallo **Solution Explorer**, vouw Hallo **weergaven** map met de rechtermuisknop op **tabellen**, en selecteer in het contextmenu hello, **toevoegen -> weergave**.</span><span class="sxs-lookup"><span data-stu-id="238d1-274">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Tables**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="238d1-275">Op Hallo **weergave toevoegen** dialoogvenster Voer **DeleteEntity** voor Hallo weergavenaam en selecteer **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="238d1-275">On hello **Add View** dialog, enter **DeleteEntity** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="238d1-276">Open `DeleteEntity.cshtml`, en dit zodanig aanpassen dat het lijkt erop dat het volgende codefragment Hallo:</span><span class="sxs-lookup"><span data-stu-id="238d1-276">Open `DeleteEntity.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @model Microsoft.WindowsAzure.Storage.Table.TableResult
    @{
        ViewBag.Title = "DeleteEntity";
    }
    
    <h2>Delete Entity results</h2>
    
    <table border="1">
        <tr>
            <th>First name</th>
            <th>Last name</th>
            <th>HTTP result</th>
        </tr>
        <tr>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).RowKey)</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).PartitionKey)</td>
            <td>@Model.HttpStatusCode</td>
        </tr>
    </table>

    ```

1. <span data-ttu-id="238d1-277">In Hallo **Solution Explorer**, vouw Hallo **weergaven -> gedeelde** map en open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="238d1-277">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="238d1-278">Na het Hallo laatste **Html.ActionLink**, voeg de volgende Hallo **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="238d1-278">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete entity", "DeleteEntity", "Tables")</li>
    ```

1. <span data-ttu-id="238d1-279">Voer Hallo toepassing uit en selecteer **entiteit verwijderen** toosee resulteert vergelijkbare toohello schermopname te volgen:</span><span class="sxs-lookup"><span data-stu-id="238d1-279">Run hello application, and select **Delete entity** toosee results similar toohello following screen shot:</span></span>
  
    ![Één ophalen](./media/vs-storage-aspnet-getting-started-tables/delete-entity-results.png)

## <a name="next-steps"></a><span data-ttu-id="238d1-281">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="238d1-281">Next steps</span></span>
<span data-ttu-id="238d1-282">Bekijk meer functie handleidingen toolearn over aanvullende mogelijkheden voor het opslaan van gegevens in Azure.</span><span class="sxs-lookup"><span data-stu-id="238d1-282">View more feature guides toolearn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="238d1-283">Aan de slag met Azure blob storage en Visual Studio verbonden Services (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="238d1-283">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>](../storage/vs-storage-aspnet-getting-started-blobs.md)
  * [<span data-ttu-id="238d1-284">Aan de slag met Azure queue storage- en Visual Studio verbonden Services (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="238d1-284">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>](../storage/vs-storage-aspnet-getting-started-queues.md)
