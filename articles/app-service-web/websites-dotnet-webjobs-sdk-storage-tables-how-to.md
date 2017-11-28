---
title: Azure Table Storage gebruiken met de WebJobs SDK
description: Informatie over het Azure table storage gebruiken met de WebJobs SDK. Tabellen maken en bestaande tabellen lezen entiteiten toevoegen aan tabellen.
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 451432cc-c780-4310-85d3-84f44fe48afe
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: 13cfc788c14d714df7022ce003d34691cf73d121
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-azure-table-storage-with-the-webjobs-sdk"></a><span data-ttu-id="471cb-104">Azure Table Storage gebruiken met de WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="471cb-104">How to use Azure table storage with the WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="471cb-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="471cb-105">Overview</span></span>
<span data-ttu-id="471cb-106">De C#-codevoorbeelden die laten hoe zien te lezen en schrijven van Azure storage-tabellen met behulp van deze handleiding [WebJobs SDK](websites-dotnet-webjobs-sdk.md) versie 1.x.</span><span class="sxs-lookup"><span data-stu-id="471cb-106">This guide provides C# code samples that show how to read and write Azure storage tables by using [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="471cb-107">De handleiding wordt ervan uitgegaan dat u weet [tekenreeksen dat punt naar uw opslagaccount, het maken van een webtaak-project in Visual Studio met verbinding](websites-dotnet-webjobs-sdk-get-started.md) of [meerdere opslagaccounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="471cb-107">The guide assumes you know [how to create a WebJob project in Visual Studio with connection strings that point to your storage account](websites-dotnet-webjobs-sdk-get-started.md) or to [multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

<span data-ttu-id="471cb-108">Sommige van de code codefragmenten weergeven de `Table` kenmerk wordt gebruikt in de functies die zijn [handmatig wordt aangeroepen](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), dat wil zeggen, niet met behulp van een van de trigger-kenmerken.</span><span class="sxs-lookup"><span data-stu-id="471cb-108">Some of the code snippets show the `Table` attribute used in functions that are [called manually](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), that is, not by using one of the trigger attributes.</span></span> 

## <span data-ttu-id="471cb-109"><a id="ingress"></a>Entiteiten toevoegen aan een tabel</span><span class="sxs-lookup"><span data-stu-id="471cb-109"><a id="ingress"></a> How to add entities to a table</span></span>
<span data-ttu-id="471cb-110">U kunt entiteiten toevoegen aan een tabel met de `Table` kenmerk met een `ICollector<T>` of `IAsyncCollector<T>` parameter waar `T` Hiermee geeft u het schema van de entiteiten die u wilt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="471cb-110">To add entities to a table, use the `Table` attribute with an `ICollector<T>` or `IAsyncCollector<T>` parameter where `T` specifies the schema of the entities you want to add.</span></span> <span data-ttu-id="471cb-111">De kenmerkconstructor heeft een tekenreeksparameter gebruikt met de naam van de tabel.</span><span class="sxs-lookup"><span data-stu-id="471cb-111">The attribute constructor takes a string parameter that specifies the name of the table.</span></span> 

<span data-ttu-id="471cb-112">Het volgende codevoorbeeld wordt toegevoegd `Person` entiteiten aan een tabel met de naam *inkomend*.</span><span class="sxs-lookup"><span data-stu-id="471cb-112">The following code sample adds `Person` entities to a table named *Ingress*.</span></span>

        [NoAutomaticTrigger]
        public static void IngressDemo(
            [Table("Ingress")] ICollector<Person> tableBinding)
        {
            for (int i = 0; i < 100000; i++)
            {
                tableBinding.Add(
                    new Person() { 
                        PartitionKey = "Test", 
                        RowKey = i.ToString(), 
                        Name = "Name" }
                    );
            }
        }

<span data-ttu-id="471cb-113">Meestal het type u gebruiken met `ICollector` is afgeleid van `TableEntity` of implementeert `ITableEntity`, maar heeft geen aan.</span><span class="sxs-lookup"><span data-stu-id="471cb-113">Typically the type you use with `ICollector` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span></span> <span data-ttu-id="471cb-114">Een van de volgende `Person` werk klassen met de code die wordt weergegeven in de voorgaande `Ingress` methode.</span><span class="sxs-lookup"><span data-stu-id="471cb-114">Either of the following `Person` classes work with the code shown in the preceding `Ingress` method.</span></span>

        public class Person : TableEntity
        {
            public string Name { get; set; }
        }

        public class Person
        {
            public string PartitionKey { get; set; }
            public string RowKey { get; set; }
            public string Name { get; set; }
        }

<span data-ttu-id="471cb-115">Als u samenwerken met de Azure storage-API wilt, kunt u toevoegen een `CloudStorageAccount` -parameter voor de methodehandtekening.</span><span class="sxs-lookup"><span data-stu-id="471cb-115">If you want to work directly with the Azure storage API, you can add a `CloudStorageAccount` parameter to the method signature.</span></span>

## <span data-ttu-id="471cb-116"><a id="monitor"></a>Realtime-controle</span><span class="sxs-lookup"><span data-stu-id="471cb-116"><a id="monitor"></a> Real-time monitoring</span></span>
<span data-ttu-id="471cb-117">Omdat ingress-functies te vaak grote hoeveelheden gegevens verwerken, kunt het dashboard WebJobs SDK u realtime controlegegevens.</span><span class="sxs-lookup"><span data-stu-id="471cb-117">Because data ingress functions often process large volumes of data, the WebJobs SDK dashboard provides real-time monitoring data.</span></span> <span data-ttu-id="471cb-118">De **aanroep logboek** gedeelte wordt uitgelegd of de functie nog steeds wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="471cb-118">The **Invocation Log** section tells you if the function is still running.</span></span>

![Inkomend functie uitgevoerd](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressrunning.png)

<span data-ttu-id="471cb-120">De **aanroep Details** pagina rapporten van de functie voortgang (aantal entiteiten dat is geschreven) wanneer deze actief is en hebt u de mogelijkheid om af te breken deze.</span><span class="sxs-lookup"><span data-stu-id="471cb-120">The **Invocation Details** page reports the function's progress (number of entities written) while it's running and gives you an opportunity to abort it.</span></span> 

![Inkomend functie uitgevoerd](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressprogress.png)

<span data-ttu-id="471cb-122">Wanneer de functie is voltooid, de **aanroep Details** pagina rapporteert het aantal rijen dat is geschreven.</span><span class="sxs-lookup"><span data-stu-id="471cb-122">When the function finishes, the **Invocation Details** page reports the number of rows written.</span></span>

![Inkomend functie is voltooid](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingresssuccess.png)

## <span data-ttu-id="471cb-124"><a id="multiple"></a>Het lezen van meerdere entiteiten uit een tabel</span><span class="sxs-lookup"><span data-stu-id="471cb-124"><a id="multiple"></a> How to read multiple entities from a table</span></span>
<span data-ttu-id="471cb-125">Als u wilt lezen van een tabel, gebruikt u de `Table` kenmerk met een `IQueryable<T>` parameter waarin typen `T` is afgeleid van `TableEntity` of implementeert `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="471cb-125">To read a table, use the `Table` attribute with an `IQueryable<T>` parameter where type `T` derives from `TableEntity` or implements `ITableEntity`.</span></span>

<span data-ttu-id="471cb-126">Het volgende codevoorbeeld leest en registreert alle rijen uit de `Ingress` tabel:</span><span class="sxs-lookup"><span data-stu-id="471cb-126">The following code sample reads and logs all rows from the `Ingress` table:</span></span>

        public static void ReadTable(
            [Table("Ingress")] IQueryable<Person> tableBinding,
            TextWriter logger)
        {
            var query = from p in tableBinding select p;
            foreach (Person person in query)
            {
                logger.WriteLine("PK:{0}, RK:{1}, Name:{2}", 
                    person.PartitionKey, person.RowKey, person.Name);
            }
        }

### <span data-ttu-id="471cb-127"><a id="readone"></a>Het lezen van één entiteit uit een tabel</span><span class="sxs-lookup"><span data-stu-id="471cb-127"><a id="readone"></a> How to read a single entity from a table</span></span>
<span data-ttu-id="471cb-128">Er is een `Table` kenmerkconstructor met twee aanvullende parameters u de partitiesleutel en de rijsleutel opgeven kunt wanneer u wilt binden aan een met één Tabelentiteit.</span><span class="sxs-lookup"><span data-stu-id="471cb-128">There is a `Table` attribute constructor with two additional parameters that let you specify the partition key and row key when you want to bind to a single table entity.</span></span>

<span data-ttu-id="471cb-129">Het volgende codevoorbeeld leest de rij in een tabel voor een `Person` entiteit op basis van partitie sleutel- en sleutelwaarden in een wachtrijbericht ontvangen:</span><span class="sxs-lookup"><span data-stu-id="471cb-129">The following code sample reads a table row for a `Person` entity based on partition key and row key values received in a queue message:</span></span>  

        public static void ReadTableEntity(
            [QueueTrigger("inputqueue")] Person personInQueue,
            [Table("persontable","{PartitionKey}", "{RowKey}")] Person personInTable,
            TextWriter logger)
        {
            if (personInTable == null)
            {
                logger.WriteLine("Person not found: PK:{0}, RK:{1}",
                        personInQueue.PartitionKey, personInQueue.RowKey);
            }
            else
            {
                logger.WriteLine("Person found: PK:{0}, RK:{1}, Name:{2}",
                        personInTable.PartitionKey, personInTable.RowKey, personInTable.Name);
            }
        }


<span data-ttu-id="471cb-130">De `Person` klasse in dit voorbeeld heeft geen voor het implementeren van `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="471cb-130">The `Person` class in this example does not have to implement `ITableEntity`.</span></span>

## <span data-ttu-id="471cb-131"><a id="storageapi"></a>Het gebruik van de API van de .NET-opslag rechtstreeks aan het werken met een tabel</span><span class="sxs-lookup"><span data-stu-id="471cb-131"><a id="storageapi"></a> How to use the .NET Storage API directly to work with a table</span></span>
<span data-ttu-id="471cb-132">U kunt ook de `Table` kenmerk met een `CloudTable` -object voor meer flexibiliteit bij het werken met een tabel.</span><span class="sxs-lookup"><span data-stu-id="471cb-132">You can also use the `Table` attribute with a `CloudTable` object for more flexibility in working with a table.</span></span>

<span data-ttu-id="471cb-133">De volgende code voorbeeld wordt een `CloudTable` object toevoegen aan één entiteit de *inkomend* tabel.</span><span class="sxs-lookup"><span data-stu-id="471cb-133">The following code sample uses a `CloudTable` object to add a single entity to the *Ingress* table.</span></span> 

        public static void UseStorageAPI(
            [Table("Ingress")] CloudTable tableBinding,
            TextWriter logger)
        {
            var person = new Person()
                {
                    PartitionKey = "Test",
                    RowKey = "100",
                    Name = "Name"
                };
            TableOperation insertOperation = TableOperation.Insert(person);
            tableBinding.Execute(insertOperation);
        }

<span data-ttu-id="471cb-134">Voor meer informatie over het gebruik van de `CloudTable` object, Zie [hoe Table Storage gebruiken met .NET](../cosmos-db/table-storage-how-to-use-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="471cb-134">For more information about how to use the `CloudTable` object, see [How to use Table Storage from .NET](../cosmos-db/table-storage-how-to-use-dotnet.md).</span></span> 

## <span data-ttu-id="471cb-135"><a id="queues"></a>Verwante onderwerpen gedekt door het wachtrijen how-to artikel</span><span class="sxs-lookup"><span data-stu-id="471cb-135"><a id="queues"></a>Related topics covered by the queues how-to article</span></span>
<span data-ttu-id="471cb-136">Zie voor meer informatie over het afhandelen van de tabel verwerking geactiveerd door een wachtrijbericht of voor WebJobs SDK scenario's die niet specifiek zijn voor de verwerking van de tabel [Azure queue storage gebruiken met de WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="471cb-136">For information about how to handle table processing triggered by a queue message, or for WebJobs SDK scenarios not specific to table processing, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="471cb-137">Onderwerpen in dit artikel omvatten het volgende:</span><span class="sxs-lookup"><span data-stu-id="471cb-137">Topics covered in that article include the following:</span></span>

* <span data-ttu-id="471cb-138">Async-functies</span><span class="sxs-lookup"><span data-stu-id="471cb-138">Async functions</span></span>
* <span data-ttu-id="471cb-139">Meerdere exemplaren</span><span class="sxs-lookup"><span data-stu-id="471cb-139">Multiple instances</span></span>
* <span data-ttu-id="471cb-140">Correct afsluiten</span><span class="sxs-lookup"><span data-stu-id="471cb-140">Graceful shutdown</span></span>
* <span data-ttu-id="471cb-141">Kenmerken in de hoofdtekst van een functie WebJobs SDK gebruiken</span><span class="sxs-lookup"><span data-stu-id="471cb-141">Use WebJobs SDK attributes in the body of a function</span></span>
* <span data-ttu-id="471cb-142">De SDK-verbindingsreeksen instellen in code</span><span class="sxs-lookup"><span data-stu-id="471cb-142">Set the SDK connection strings in code</span></span>
* <span data-ttu-id="471cb-143">Waarden instellen voor de WebJobs SDK constructorparameters in code</span><span class="sxs-lookup"><span data-stu-id="471cb-143">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="471cb-144">Een functie handmatig activeren</span><span class="sxs-lookup"><span data-stu-id="471cb-144">Trigger a function manually</span></span>
* <span data-ttu-id="471cb-145">Schrijven Logboeken</span><span class="sxs-lookup"><span data-stu-id="471cb-145">Write logs</span></span>

## <span data-ttu-id="471cb-146"><a id="nextsteps"></a> Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="471cb-146"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="471cb-147">Deze handleiding is opgegeven codevoorbeelden die laten hoe u algemene scenario's zien voor het werken met Azure-tabellen te verwerken.</span><span class="sxs-lookup"><span data-stu-id="471cb-147">This guide has provided code samples that show how to handle common scenarios for working with Azure tables.</span></span> <span data-ttu-id="471cb-148">Zie voor meer informatie over het gebruik van Azure WebJobs en de WebJobs SDK [Azure WebJobs aanbevolen Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="471cb-148">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

