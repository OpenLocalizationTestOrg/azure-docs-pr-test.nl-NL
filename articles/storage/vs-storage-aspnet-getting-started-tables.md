---
title: aaaGet de slag met Azure-tabelopslag en Visual Studio verbonden Services (ASP.NET) | Microsoft Docs
description: Hoe tooget gestart met behulp van Azure-tabelopslag nadat u hebt aangesloten tooa storage-account met behulp van Visual Studio verbonden Services in een ASP.NET-project in Visual Studio
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: af81a326-18f4-4449-bc0d-e96fba27c1f8
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: tarcher
ms.openlocfilehash: e7ed17098c8742954972dc9e1b50eca77221e327
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-table-storage-and-visual-studio-connected-services-aspnet"></a>Aan de slag met Azure-tabelopslag en Visual Studio verbonden Services (ASP.NET)
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a>Overzicht

Azure Table storage kunt u toostore grote hoeveelheden gestructureerde gegevens. Hallo-service is een NoSQL-gegevensarchief die geverifieerde aanroepen vanuit binnen en buiten hello Azure-cloud accepteert. Azure-tabellen zijn ideaal voor het opslaan van gestructureerde, niet-relationele gegevens.

Deze zelfstudie laat zien hoe toowrite ASP.NET-code voor enkele algemene scenario's met behulp van Azure table storage entiteiten. Deze scenario's omvatten maken van een tabel en toe te voegen, het uitvoeren van query's en het verwijderen van tabelentiteiten. 

##<a name="prerequisites"></a>Vereisten

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Azure Storage-account](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a>Maken van een MVC-controller 

1. In Hallo **Solution Explorer**, met de rechtermuisknop op **domeincontrollers**, en selecteer in het contextmenu hello, **toevoegen -> Controller**.

    ![Een controller tooan ASP.NET MVC-app toevoegen](./media/vs-storage-aspnet-getting-started-tables/add-controller-menu.png)

1. Op Hallo **Add Scaffold** dialoogvenster Selecteer **MVC 5 Controller - leeg**, en selecteer **toevoegen**.

    ![Geef een MVC-controller](./media/vs-storage-aspnet-getting-started-tables/add-controller.png)

1. Op Hallo **Controller toevoegen** dialoogvenster, naam Hallo controller *TablesController*, en selecteer **toevoegen**.

    ![Naam Hallo MVC-controller](./media/vs-storage-aspnet-getting-started-tables/add-controller-name.png)

1. Voeg de volgende Hallo *met* richtlijnen toohello `TablesController.cs` bestand:

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Table;
    ```

### <a name="create-a-model-class"></a>Maak een modelklasse

Veel van Hallo voorbeelden in dit artikel gebruik een **TableEntity**-afgeleide klasse aangeroepen **CustomerEntity**. Hallo stappen volgen helpt u bij het declareren van deze klasse als een modelklasse:

1. In Hallo **Solution Explorer**, met de rechtermuisknop op **modellen**, en selecteer in het contextmenu hello, **toevoegen -> klasse**.

1. Op Hallo **Add New Item** dialoogvenster, naam Hallo klasse, **CustomerEntity**.

1. Open Hallo `CustomerEntity.cs` bestand en voeg de volgende Hallo **met** richtlijn:

    ```csharp
    using Microsoft.WindowsAzure.Storage.Table;
    ```

1. Hallo klasse zodanig aanpassen dat, als u klaar bent Hallo klasse zoals in de volgende code Hallo is gedeclareerd. Hallo klasse declareert een entiteitsklasse aangeroepen **CustomerEntity** dat wordt gebruikt de voornaam van de klant als de rijsleutel Hallo- en achternaam als partitiesleutel Hallo Hallo.

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

## <a name="create-a-table"></a>Een tabel maken

Hallo volgende stappen laten zien hoe toocreate een tabel:

> [!NOTE]
> 
> Deze sectie wordt ervan uitgegaan dat u de stappen in Hallo hebt voltooid [Hallo ontwikkelomgeving instellen](#set-up-the-development-environment). 

1. Open Hallo `TablesController.cs` bestand.

1. Toevoegen van een methode aangeroepen **CreateTable** die retourneert een **ActionResult**.

    ```csharp
    public ActionResult CreateTable()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Binnen Hallo **CreateTable** methode, krijgen een **CloudStorageAccount** -object met gegevens over uw storage-account. Gebruik Hallo volgende code tooget Hallo opslag tekenreeks en storage-account verbindingsinformatie van hello Azure serviceconfiguratie: (wijziging  *&lt;storage-account-name >* toohello-naam van hello Azure-opslag account die u toegang hebt.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Ophalen van een **CloudTableClient** object vertegenwoordigt een tabelserviceclient.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Ophalen van een **CloudTable** -object met een tabelnaam verwijzing toohello gewenste. Hallo **CloudTableClient.GetTableReference** methode maakt u niet een aanvraag in voor de tabelopslag. Hallo verwijzing wordt geretourneerd of Hallo tabel bestaat of niet. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Hallo aanroepen **CloudTable.CreateIfNotExists** methode toocreate Hallo tabel als deze nog niet bestaat. Hallo **CloudTable.CreateIfNotExists** methode retourneert **true** als Hallo tabel niet bestaat en is gemaakt. Anders **false** wordt geretourneerd.    

    ```csharp
    ViewBag.Success = table.CreateIfNotExists();
    ```

1. Update Hallo **ViewBag** met de naam van de tabel Hallo Hallo.

    ```csharp
    ViewBag.TableName = table.Name;
    ```

1. In Hallo **Solution Explorer**, vouw Hallo **weergaven** map met de rechtermuisknop op **tabellen**, en selecteer in het contextmenu hello, **toevoegen -> weergave**.

1. Op Hallo **weergave toevoegen** dialoogvenster Voer **CreateTable** voor Hallo weergavenaam en selecteer **toevoegen**.

1. Open `CreateTable.cshtml`, en dit zodanig aanpassen dat het lijkt erop dat het volgende codefragment Hallo:

    ```csharp
    @{
        ViewBag.Title = "Create Table";
    }
    
    <h2>Create Table results</h2>

    Creation of @ViewBag.TableName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. In Hallo **Solution Explorer**, vouw Hallo **weergaven -> gedeelde** map en open `_Layout.cshtml`.

1. Na het Hallo laatste **Html.ActionLink**, voeg de volgende Hallo **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Create table", "CreateTable", "Tables")</li>
    ```

1. Voer Hallo toepassing uit en selecteer **tabel maken** toosee resulteert vergelijkbare toohello schermopname te volgen:
  
    ![Tabel maken](./media/vs-storage-aspnet-getting-started-tables/create-table-results.png)

    Zoals eerder vermeld, Hallo **CloudTable.CreateIfNotExists** methode retourneert **true** alleen wanneer Hallo tabel bestaat niet en is gemaakt. Dus als u Hallo app uitvoeren wanneer Hallo tabel bestaat, Hallo methode retourneert **false**. toorun hello app meerdere keren, verwijdert u Hallo tabel voordat Hallo app opnieuw uit te voeren. Verwijderen Hallo tabel kan worden uitgevoerd via Hallo **CloudTable.Delete** methode. U kunt ook met Hallo Hallo-tabel verwijderen [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) of Hallo [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).  

## <a name="add-an-entity-tooa-table"></a>Een entiteit tooa tabel toevoegen

*Entiteiten* toewijzen tooC\# objecten met behulp van een aangepaste klasse wordt afgeleid van **TableEntity**. tooadd een entiteit tooa tabel, maak een klasse die eigenschappen Hallo van uw entiteit definieert. In deze sectie ziet u hoe toodefine een entiteitsklasse die gebruikmaakt van de voornaam van de klant als de rijsleutel Hallo- en achternaam als partitiesleutel Hallo Hallo. Samen een entiteit partitie en rijsleutel een unieke identificatie Hallo entiteit in Hallo tabel. Entiteiten met dezelfde partitiesleutel kunnen sneller worden opgevraagd dan entiteiten met verschillende partitiesleutels, maar het gebruik van verschillende partitiesleutels maakt een grotere schaalbaarheid van parallelle bewerkingen mogelijk. Voor alle eigenschappen die moet worden opgeslagen in de tabelservice hello, moet Hallo eigenschap een openbare eigenschap van een ondersteund type dat toegang biedt tot zowel instellen en ophalen van waarden.
Hallo entiteitsklasse *moet* declareren van een openbare parameterloze constructor.

> [!NOTE]
> 
> Deze sectie wordt ervan uitgegaan dat u de stappen in Hallo hebt voltooid [Hallo ontwikkelomgeving instellen](#set-up-the-development-environment).

1. Open Hallo `TablesController.cs` bestand.

1. Toevoegen van de volgende richtlijn zodat die de code in Hallo HALLO hallo `TablesController.cs` bestand heeft toegang tot Hallo **CustomerEntity** klasse:

    ```csharp
    using StorageAspnet.Models;
    ```

1. Toevoegen van een methode aangeroepen **AddEntity** die retourneert een **ActionResult**.

    ```csharp
    public ActionResult AddEntity()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Binnen Hallo **AddEntity** methode, krijgen een **CloudStorageAccount** -object met gegevens over uw storage-account. Gebruik Hallo volgende code tooget Hallo opslag tekenreeks en storage-account verbindingsinformatie van hello Azure serviceconfiguratie: (wijziging  *&lt;storage-account-name >* toohello-naam van hello Azure-opslag account die u toegang hebt.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Ophalen van een **CloudTableClient** object vertegenwoordigt een tabelserviceclient.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Ophalen van een **CloudTable** -object met een verwijzing toohello tabel toowhich u gaat tooadd Hallo nieuwe entiteit. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Exemplaar maken en initialiseren Hallo **CustomerEntity** klasse.

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    ```

1. Maak een **TableOperation** -object dat wordt ingevoegd Hallo klantentiteit.

    ```csharp
    TableOperation insertOperation = TableOperation.Insert(customer1);
    ```

1. Hallo insert-bewerking uitvoeren door de aanroepende Hallo **CloudTable.Execute** methode. U kunt Hallo resultaat van Hallo-bewerking controleren door te inspecteren Hallo **TableResult.HttpStatusCode** eigenschap. Statuscode 2xx geeft Hallo actie aangevraagd door Hallo-client is verwerkt. Geslaagde invoegingen van nieuwe entiteiten resulteert bijvoorbeeld in een HTTP-statuscode van 204, wat betekent dat Hallo bewerking met succes is verwerkt en Hallo-server heeft geen inhoud geretourneerd.

    ```csharp
    TableResult result = table.Execute(insertOperation);
    ```

1. Update Hallo **ViewBag** met Hallo tabelnaam en de resultaten van de Hallo van Hallo insert-bewerking.

    ```csharp
    ViewBag.TableName = table.Name;
    ViewBag.Result = result.HttpStatusCode;
    ```

1. In Hallo **Solution Explorer**, vouw Hallo **weergaven** map met de rechtermuisknop op **tabellen**, en selecteer in het contextmenu hello, **toevoegen -> weergave**.

1. Op Hallo **weergave toevoegen** dialoogvenster Voer **AddEntity** voor Hallo weergavenaam en selecteer **toevoegen**.

1. Open `AddEntity.cshtml`, en dit zodanig aanpassen dat het lijkt erop dat het volgende codefragment Hallo:

    ```csharp
    @{
        ViewBag.Title = "Add entity";
    }
    
    <h2>Add entity results</h2>

    Insert of entity into @ViewBag.TableName @(ViewBag.Result == 204 ? "succeeded" : "failed")
    ```
1. In Hallo **Solution Explorer**, vouw Hallo **weergaven -> gedeelde** map en open `_Layout.cshtml`.

1. Na het Hallo laatste **Html.ActionLink**, voeg de volgende Hallo **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Add entity", "AddEntity", "Tables")</li>
    ```

1. Voer Hallo toepassing uit en selecteer **entiteit toevoegen** toosee resulteert vergelijkbare toohello schermopname te volgen:
  
    ![Entiteit toevoegen](./media/vs-storage-aspnet-getting-started-tables/add-entity-results.png)

    U kunt controleren of Hallo entiteit is toegevoegd door Hallo stappen in de sectie Hallo [één entiteit ophalen](#get-a-single-entity). U kunt ook Hallo [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview alle Hallo entiteiten voor de tabellen.

## <a name="add-a-batch-of-entities-tooa-table"></a>Een batch entiteiten tooa tabel toevoegen

In aanvulling toobeing kunnen te[toevoegen van een entiteit tooa tabel 1 tegelijk](#add-an-entity-to-a-table), u kunt ook entiteiten in batch toevoegen. Toevoegen van entiteiten in batch vermindert Hallo aantal retourbewerkingen tussen uw code en hello Azure table-service. Hallo stappen te volgen laten zien hoe tooadd meerdere entiteiten tooa tabel met een enkele insert-bewerking:

> [!NOTE]
> 
> Deze sectie wordt ervan uitgegaan dat u de stappen in Hallo hebt voltooid [Hallo ontwikkelomgeving instellen](#set-up-the-development-environment).

1. Open Hallo `TablesController.cs` bestand.

1. Toevoegen van een methode aangeroepen **AddEntities** die retourneert een **ActionResult**.

    ```csharp
    public ActionResult AddEntities()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Binnen Hallo **AddEntities** methode, krijgen een **CloudStorageAccount** -object met gegevens over uw storage-account. Gebruik Hallo volgende code tooget Hallo opslag tekenreeks en storage-account verbindingsinformatie van hello Azure serviceconfiguratie: (wijziging  *&lt;storage-account-name >* toohello-naam van hello Azure-opslag account die u toegang hebt.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Ophalen van een **CloudTableClient** object vertegenwoordigt een tabelserviceclient.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Ophalen van een **CloudTable** -object met een verwijzing toohello tabel toowhich u gaat tooadd Hallo nieuwe entiteiten zijn. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Exemplaar maken van een klantobjecten op basis van Hallo **CustomerEntity** modelklasse weergegeven in de sectie Hallo [toevoegen van een tabel entity tooa](#add-an-entity-to-a-table).

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
    customer1.Email = "Jeff@contoso.com";

    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.Email = "Ben@contoso.com";
    ```

1. Ophalen van een **TableBatchOperation** object.

    ```csharp
    TableBatchOperation batchOperation = new TableBatchOperation();
    ```

1. Entiteiten toohello batch insert-bewerking object toevoegen.

    ```csharp
    batchOperation.Insert(customer1);
    batchOperation.Insert(customer2);
    ```

1. Hallo batch insert-bewerking uitvoeren door de aanroepende Hallo **CloudTable.ExecuteBatch** methode.   

    ```csharp
    IList<TableResult> results = table.ExecuteBatch(batchOperation);
    ```

1. Hallo **CloudTable.ExecuteBatch** methode retourneert een lijst met **TableResult** objecten waar elke **TableResult** -object wordt onderzocht toodetermine Hallo slagen of mislukken van elke afzonderlijke bewerking. In dit voorbeeld Hallo tooa lijstweergave doorgeven en laat Hallo weergave Hallo resultaten van elke bewerking weer te geven. 
 
    ```csharp
    return View(results);
    ```

1. In Hallo **Solution Explorer**, vouw Hallo **weergaven** map met de rechtermuisknop op **tabellen**, en selecteer in het contextmenu hello, **toevoegen -> weergave**.

1. Op Hallo **weergave toevoegen** dialoogvenster Voer **AddEntities** voor Hallo weergavenaam en selecteer **toevoegen**.

1. Open `AddEntities.cshtml`, en zodat het lijkt erop dat de volgende hello te wijzigen.

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

1. In Hallo **Solution Explorer**, vouw Hallo **weergaven -> gedeelde** map en open `_Layout.cshtml`.

1. Na het Hallo laatste **Html.ActionLink**, voeg de volgende Hallo **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Add entities", "AddEntities", "Tables")</li>
    ```

1. Voer Hallo toepassing uit en selecteer **entiteiten toevoegen** toosee resulteert vergelijkbare toohello schermopname te volgen:
  
    ![Entiteiten toevoegen](./media/vs-storage-aspnet-getting-started-tables/add-entities-results.png)

    U kunt controleren of Hallo entiteit is toegevoegd door Hallo stappen in de sectie Hallo [één entiteit ophalen](#get-a-single-entity). U kunt ook Hallo [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview alle Hallo entiteiten voor de tabellen.

## <a name="get-a-single-entity"></a>Één entiteit ophalen

Deze sectie ziet u hoe tooget vanuit een tabel met één entiteit Hallo rijsleutel en de partitiesleutel van entiteit. 

> [!NOTE]
> 
> Deze sectie wordt ervan uitgegaan dat u de stappen in Hallo hebt voltooid [Hallo ontwikkelomgeving instellen](#set-up-the-development-environment), en maakt gebruik van gegevens van [toevoegen van een batch entiteiten tooa tabel](#add-a-batch-of-entities-to-a-table). 

1. Open Hallo `TablesController.cs` bestand.

1. Toevoegen van een methode aangeroepen **GetSingle** die retourneert een **ActionResult**.

    ```csharp
    public ActionResult GetSingle()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Binnen Hallo **GetSingle** methode, krijgen een **CloudStorageAccount** -object met gegevens over uw storage-account. Gebruik Hallo volgende code tooget Hallo opslag tekenreeks en storage-account verbindingsinformatie van hello Azure serviceconfiguratie: (wijziging  *&lt;storage-account-name >* toohello-naam van hello Azure-opslag account die u toegang hebt.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Ophalen van een **CloudTableClient** object vertegenwoordigt een tabelserviceclient.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Ophalen van een **CloudTable** -object met een verwijzingstabel toohello van waaruit u Hallo entiteit ophalen. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Maakt een ophalen bewerking object waarvoor een entiteitsobject afgeleid van **TableEntity**. de eerste parameter Hallo is Hallo *partitionKey*, en de tweede parameter Hallo Hallo *rowKey*. Met behulp van Hallo **CustomerEntity** klasse en gegevens die zijn gepresenteerd in de sectie Hallo [toevoegen van een batch entiteiten tooa tabel](#add-a-batch-of-entities-to-a-table), Hallo na code codefragment query's Hallo tabel voor een **CustomerEntity** entiteit met een *partitionKey* waarde van 'Smith' en een *rowKey* waarde van 'Ben':

    ```csharp
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");
    ```

1. Hallo ophalen bewerking niet uitvoeren.   

    ```csharp
    TableResult result = table.Execute(retrieveOperation);
    ```

1. Hallo resultaat toohello weergeven voor weergave doorgeven.

    ```csharp
    return View(result);
    ```

1. In Hallo **Solution Explorer**, vouw Hallo **weergaven** map met de rechtermuisknop op **tabellen**, en selecteer in het contextmenu hello, **toevoegen -> weergave**.

1. Op Hallo **weergave toevoegen** dialoogvenster Voer **GetSingle** voor Hallo weergavenaam en selecteer **toevoegen**.

1. Open `GetSingle.cshtml`, en dit zodanig aanpassen dat het lijkt erop dat het volgende codefragment Hallo:

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

1. In Hallo **Solution Explorer**, vouw Hallo **weergaven -> gedeelde** map en open `_Layout.cshtml`.

1. Na het Hallo laatste **Html.ActionLink**, voeg de volgende Hallo **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Get single", "GetSingle", "Tables")</li>
    ```

1. Voer Hallo toepassing uit en selecteer **één ophalen** toosee resulteert vergelijkbare toohello schermopname te volgen:
  
    ![Één ophalen](./media/vs-storage-aspnet-getting-started-tables/get-single-results.png)

## <a name="get-all-entities-in-a-partition"></a>Alle entiteiten in een partitie ophalen

Zoals vermeld in de sectie hello, [toevoegen van een tabel entity tooa](#add-an-entity-to-a-table), Hallo combinatie van een partitie en een rijsleutel unieke identificatie van een entiteit in een tabel. Entiteiten met dezelfde partitiesleutel kunnen sneller worden opgevraagd dan entiteiten met verschillende partitiesleutels. Deze sectie ziet u hoe tooquery een tabel voor alle Hallo entiteiten van een opgegeven partitie.  

> [!NOTE]
> 
> Deze sectie wordt ervan uitgegaan dat u de stappen in Hallo hebt voltooid [Hallo ontwikkelomgeving instellen](#set-up-the-development-environment), en maakt gebruik van gegevens van [toevoegen van een batch entiteiten tooa tabel](#add-a-batch-of-entities-to-a-table). 

1. Open Hallo `TablesController.cs` bestand.

1. Toevoegen van een methode aangeroepen **GetPartition** die retourneert een **ActionResult**.

    ```csharp
    public ActionResult GetPartition()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Binnen Hallo **GetPartition** methode, krijgen een **CloudStorageAccount** -object met gegevens over uw storage-account. Gebruik Hallo volgende code tooget Hallo opslag tekenreeks en storage-account verbindingsinformatie van hello Azure serviceconfiguratie: (wijziging  *&lt;storage-account-name >* toohello-naam van hello Azure-opslag account die u toegang hebt.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Ophalen van een **CloudTableClient** object vertegenwoordigt een tabelserviceclient.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Ophalen van een **CloudTable** -object met een verwijzingstabel toohello van waaruit u Hallo entiteiten ophalen. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Exemplaar maken van een **TableQuery** object Hallo query opgeven in Hallo **waar** component. Met behulp van Hallo **CustomerEntity** klasse en gegevens die zijn gepresenteerd in de sectie Hallo [toevoegen van een batch entiteiten tooa tabel](#add-a-batch-of-entities-to-a-table), Hallo volgende codefragment query's Hallo tabel voor een alle entiteiten code waarbij hello  **PartitionKey** (achternaam van de klant) heeft de waarde 'Smith':

    ```csharp
    TableQuery<CustomerEntity> query = 
        new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));
    ```

1. Aanroepen in een lus Hallo **CloudTable.ExecuteQuerySegmented** methode Hallo u geïnstantieerd query-object in de vorige stap hello wordt doorgegeven.  Hallo **CloudTable.ExecuteQuerySegmented** methode retourneert een **TableContinuationToken** die - object als **null** -geeft aan dat er geen entiteiten meer tooretrieve. Binnen de lus hello, gebruiken om een andere lus tooiterate via Hallo entiteiten geretourneerd. In de Hallo volgende codevoorbeeld, wordt elke geretourneerde entiteit tooa lijst toegevoegd. Eenmaal Hallo lus eindigt, Hallo lijst tooa weergeven voor de weergave wordt doorgegeven: 

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

1. In Hallo **Solution Explorer**, vouw Hallo **weergaven** map met de rechtermuisknop op **tabellen**, en selecteer in het contextmenu hello, **toevoegen -> weergave**.

1. Op Hallo **weergave toevoegen** dialoogvenster Voer **GetPartition** voor Hallo weergavenaam en selecteer **toevoegen**.

1. Open `GetPartition.cshtml`, en dit zodanig aanpassen dat het lijkt erop dat het volgende codefragment Hallo:

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

1. In Hallo **Solution Explorer**, vouw Hallo **weergaven -> gedeelde** map en open `_Layout.cshtml`.

1. Na het Hallo laatste **Html.ActionLink**, voeg de volgende Hallo **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Get partition", "GetPartition", "Tables")</li>
    ```

1. Voer Hallo toepassing uit en selecteer **partitie ophalen** toosee resulteert vergelijkbare toohello schermopname te volgen:
  
    ![Partitie ophalen](./media/vs-storage-aspnet-getting-started-tables/get-partition-results.png)

## <a name="delete-an-entity"></a>Een entiteit verwijderen

Deze sectie ziet u hoe toodelete een entiteit uit een tabel.

> [!NOTE]
> 
> Deze sectie wordt ervan uitgegaan dat u de stappen in Hallo hebt voltooid [Hallo ontwikkelomgeving instellen](#set-up-the-development-environment), en maakt gebruik van gegevens van [toevoegen van een batch entiteiten tooa tabel](#add-a-batch-of-entities-to-a-table). 

1. Open Hallo `TablesController.cs` bestand.

1. Toevoegen van een methode aangeroepen **DeleteEntity** die retourneert een **ActionResult**.

    ```csharp
    public ActionResult DeleteEntity()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Binnen Hallo **DeleteEntity** methode, krijgen een **CloudStorageAccount** -object met gegevens over uw storage-account. Gebruik Hallo volgende code tooget Hallo opslag tekenreeks en storage-account verbindingsinformatie van hello Azure serviceconfiguratie: (wijziging  *&lt;storage-account-name >* toohello-naam van hello Azure-opslag account die u toegang hebt.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Ophalen van een **CloudTableClient** object vertegenwoordigt een tabelserviceclient.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. Ophalen van een **CloudTable** -object met een verwijzingstabel toohello Hallo entiteit worden verwijderd. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Maakt een verwijderen bewerking object waarvoor een entiteitsobject afgeleid van **TableEntity**. In dit geval gebruiken we Hallo **CustomerEntity** klasse en gegevens die zijn gepresenteerd in de sectie Hallo [toevoegen van een batch entiteiten tooa tabel](#add-a-batch-of-entities-to-a-table). Hallo van entiteit **ETag** tooa geldige waarde moet worden ingesteld.  

    ```csharp
    TableOperation deleteOperation = 
        TableOperation.Delete(new CustomerEntity("Smith", "Ben") { ETag = "*" } );
    ```

1. Hallo-delete-bewerking uitvoeren.   

    ```csharp
    TableResult result = table.Execute(deleteOperation);
    ```

1. Hallo resultaat toohello weergeven voor weergave doorgeven.

    ```csharp
    return View(result);
    ```

1. In Hallo **Solution Explorer**, vouw Hallo **weergaven** map met de rechtermuisknop op **tabellen**, en selecteer in het contextmenu hello, **toevoegen -> weergave**.

1. Op Hallo **weergave toevoegen** dialoogvenster Voer **DeleteEntity** voor Hallo weergavenaam en selecteer **toevoegen**.

1. Open `DeleteEntity.cshtml`, en dit zodanig aanpassen dat het lijkt erop dat het volgende codefragment Hallo:

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

1. In Hallo **Solution Explorer**, vouw Hallo **weergaven -> gedeelde** map en open `_Layout.cshtml`.

1. Na het Hallo laatste **Html.ActionLink**, voeg de volgende Hallo **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Delete entity", "DeleteEntity", "Tables")</li>
    ```

1. Voer Hallo toepassing uit en selecteer **entiteit verwijderen** toosee resulteert vergelijkbare toohello schermopname te volgen:
  
    ![Één ophalen](./media/vs-storage-aspnet-getting-started-tables/delete-entity-results.png)

## <a name="next-steps"></a>Volgende stappen
Bekijk meer functie handleidingen toolearn over aanvullende mogelijkheden voor het opslaan van gegevens in Azure.

  * [Aan de slag met Azure blob storage en Visual Studio verbonden Services (ASP.NET)](./vs-storage-aspnet-getting-started-blobs.md)
  * [Aan de slag met Azure queue storage- en Visual Studio verbonden Services (ASP.NET)](./vs-storage-aspnet-getting-started-queues.md)
