---
title: aaaHow toouse Azure-tabelopslag Hello WebJobs SDK
description: Meer informatie over hoe toouse Azure table storage Hello WebJobs SDK. Tabellen maken en bestaande tabellen lezen entiteiten tootables toevoegen.
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
ms.openlocfilehash: 8e28c69df4a934646add9e50c6de28e76dca1636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-with-hello-webjobs-sdk"></a><span data-ttu-id="82c06-104">Hoe toouse Azure table storage Hello WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="82c06-104">How toouse Azure table storage with hello WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="82c06-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="82c06-105">Overview</span></span>
<span data-ttu-id="82c06-106">In deze handleiding vindt u voorbeelden van C#-code die tonen hoe tooread en write Azure-opslag met behulp van tabellen [WebJobs SDK](websites-dotnet-webjobs-sdk.md) versie 1.x.</span><span class="sxs-lookup"><span data-stu-id="82c06-106">This guide provides C# code samples that show how tooread and write Azure storage tables by using [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="82c06-107">Hallo handleiding wordt ervan uitgegaan dat u weet [hoe een webtaak-project in Visual Studio met verbinding toocreate dat punt tooyour storage-account tekenreeksen](websites-dotnet-webjobs-sdk-get-started.md) of te[meerdere opslagaccounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="82c06-107">hello guide assumes you know [how toocreate a WebJob project in Visual Studio with connection strings that point tooyour storage account](websites-dotnet-webjobs-sdk-get-started.md) or too[multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

<span data-ttu-id="82c06-108">Een aantal codefragmenten Hallo Hallo weergeven `Table` kenmerk wordt gebruikt in de functies die zijn [handmatig wordt aangeroepen](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), dat wil zeggen, niet met behulp van een Hallo trigger kenmerken.</span><span class="sxs-lookup"><span data-stu-id="82c06-108">Some of hello code snippets show hello `Table` attribute used in functions that are [called manually](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), that is, not by using one of hello trigger attributes.</span></span> 

## <span data-ttu-id="82c06-109"><a id="ingress"></a>Hoe tooadd entiteiten tooa tabel</span><span class="sxs-lookup"><span data-stu-id="82c06-109"><a id="ingress"></a> How tooadd entities tooa table</span></span>
<span data-ttu-id="82c06-110">tooadd entiteiten tooa tabel, gebruik Hallo `Table` kenmerk met een `ICollector<T>` of `IAsyncCollector<T>` parameter waar `T` Hallo schema geeft Hallo entiteiten gewenste tooadd.</span><span class="sxs-lookup"><span data-stu-id="82c06-110">tooadd entities tooa table, use hello `Table` attribute with an `ICollector<T>` or `IAsyncCollector<T>` parameter where `T` specifies hello schema of hello entities you want tooadd.</span></span> <span data-ttu-id="82c06-111">Hallo kenmerkconstructor tekenreeksparameter een waarmee Hallo-naam van het Hallo-tabel.</span><span class="sxs-lookup"><span data-stu-id="82c06-111">hello attribute constructor takes a string parameter that specifies hello name of hello table.</span></span> 

<span data-ttu-id="82c06-112">Hallo codevoorbeeld voegt `Person` entiteiten tooa tabel met de naam *inkomend*.</span><span class="sxs-lookup"><span data-stu-id="82c06-112">hello following code sample adds `Person` entities tooa table named *Ingress*.</span></span>

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

<span data-ttu-id="82c06-113">Doorgaans Hallo type die u met gebruikt `ICollector` is afgeleid van `TableEntity` of implementeert `ITableEntity`, maar heeft geen aan.</span><span class="sxs-lookup"><span data-stu-id="82c06-113">Typically hello type you use with `ICollector` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span></span> <span data-ttu-id="82c06-114">Een van de volgende Hallo `Person` werk klassen met Hallo-code die wordt weergegeven in de voorgaande Hallo `Ingress` methode.</span><span class="sxs-lookup"><span data-stu-id="82c06-114">Either of hello following `Person` classes work with hello code shown in hello preceding `Ingress` method.</span></span>

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

<span data-ttu-id="82c06-115">Als u wilt dat toowork rechtstreeks met hello Azure storage-API, kunt u toevoegen een `CloudStorageAccount` parameter toohello methodehandtekening.</span><span class="sxs-lookup"><span data-stu-id="82c06-115">If you want toowork directly with hello Azure storage API, you can add a `CloudStorageAccount` parameter toohello method signature.</span></span>

## <span data-ttu-id="82c06-116"><a id="monitor"></a>Realtime-controle</span><span class="sxs-lookup"><span data-stu-id="82c06-116"><a id="monitor"></a> Real-time monitoring</span></span>
<span data-ttu-id="82c06-117">Omdat ingress-functies worden vaak grote hoeveelheden gegevens verwerken, biedt Hallo WebJobs SDK dashboard realtime controlegegevens.</span><span class="sxs-lookup"><span data-stu-id="82c06-117">Because data ingress functions often process large volumes of data, hello WebJobs SDK dashboard provides real-time monitoring data.</span></span> <span data-ttu-id="82c06-118">Hallo **aanroep logboek** gedeelte wordt uitgelegd of Hallo-functie nog steeds wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="82c06-118">hello **Invocation Log** section tells you if hello function is still running.</span></span>

![Inkomend functie uitgevoerd](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressrunning.png)

<span data-ttu-id="82c06-120">Hallo **aanroep Details** pagina rapporten Hallo van functie voortgang (aantal entiteiten dat is geschreven) wanneer deze actief is en u een kans tooabort biedt deze.</span><span class="sxs-lookup"><span data-stu-id="82c06-120">hello **Invocation Details** page reports hello function's progress (number of entities written) while it's running and gives you an opportunity tooabort it.</span></span> 

![Inkomend functie uitgevoerd](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressprogress.png)

<span data-ttu-id="82c06-122">Wanneer de functie Hallo is voltooid, hello **aanroep Details** pagina rapporten Hallo aantal geschreven rijen.</span><span class="sxs-lookup"><span data-stu-id="82c06-122">When hello function finishes, hello **Invocation Details** page reports hello number of rows written.</span></span>

![Inkomend functie is voltooid](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingresssuccess.png)

## <span data-ttu-id="82c06-124"><a id="multiple"></a>Hoe tooread meerdere entiteiten uit een tabel</span><span class="sxs-lookup"><span data-stu-id="82c06-124"><a id="multiple"></a> How tooread multiple entities from a table</span></span>
<span data-ttu-id="82c06-125">een tabel tooread gebruiken Hallo `Table` kenmerk met een `IQueryable<T>` parameter waarin typen `T` is afgeleid van `TableEntity` of implementeert `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="82c06-125">tooread a table, use hello `Table` attribute with an `IQueryable<T>` parameter where type `T` derives from `TableEntity` or implements `ITableEntity`.</span></span>

<span data-ttu-id="82c06-126">Hallo codevoorbeeld leest en registreert alle rijen van Hallo `Ingress` tabel:</span><span class="sxs-lookup"><span data-stu-id="82c06-126">hello following code sample reads and logs all rows from hello `Ingress` table:</span></span>

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

### <span data-ttu-id="82c06-127"><a id="readone"></a>Hoe tooread één entiteit uit een tabel</span><span class="sxs-lookup"><span data-stu-id="82c06-127"><a id="readone"></a> How tooread a single entity from a table</span></span>
<span data-ttu-id="82c06-128">Er is een `Table` kenmerkconstructor met twee extra parameters die u Hallo partitiesleutel en rijsleutel opgeven wanneer u toobind tooa één Tabelentiteit wilt laten.</span><span class="sxs-lookup"><span data-stu-id="82c06-128">There is a `Table` attribute constructor with two additional parameters that let you specify hello partition key and row key when you want toobind tooa single table entity.</span></span>

<span data-ttu-id="82c06-129">Hallo codevoorbeeld leest de rij in een tabel voor een `Person` entiteit op basis van partitie sleutel- en sleutelwaarden in een wachtrijbericht ontvangen:</span><span class="sxs-lookup"><span data-stu-id="82c06-129">hello following code sample reads a table row for a `Person` entity based on partition key and row key values received in a queue message:</span></span>  

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


<span data-ttu-id="82c06-130">Hallo `Person` klasse in dit voorbeeld heeft geen tooimplement `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="82c06-130">hello `Person` class in this example does not have tooimplement `ITableEntity`.</span></span>

## <span data-ttu-id="82c06-131"><a id="storageapi"></a>Hoe toouse .NET opslag API Hallo rechtstreeks toowork met een tabel</span><span class="sxs-lookup"><span data-stu-id="82c06-131"><a id="storageapi"></a> How toouse hello .NET Storage API directly toowork with a table</span></span>
<span data-ttu-id="82c06-132">U kunt ook Hallo `Table` kenmerk met een `CloudTable` -object voor meer flexibiliteit bij het werken met een tabel.</span><span class="sxs-lookup"><span data-stu-id="82c06-132">You can also use hello `Table` attribute with a `CloudTable` object for more flexibility in working with a table.</span></span>

<span data-ttu-id="82c06-133">Hallo volgende code voorbeeld wordt een `CloudTable` object tooadd een enkele entiteit toohello *inkomend* tabel.</span><span class="sxs-lookup"><span data-stu-id="82c06-133">hello following code sample uses a `CloudTable` object tooadd a single entity toohello *Ingress* table.</span></span> 

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

<span data-ttu-id="82c06-134">Voor meer informatie over het toouse hello `CloudTable` object, Zie [hoe toouse Table Storage uit het .NET](../cosmos-db/table-storage-how-to-use-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="82c06-134">For more information about how toouse hello `CloudTable` object, see [How toouse Table Storage from .NET](../cosmos-db/table-storage-how-to-use-dotnet.md).</span></span> 

## <span data-ttu-id="82c06-135"><a id="queues"></a>Verwante onderwerpen Hallo wachtrijen hoe-tooarticle vallen</span><span class="sxs-lookup"><span data-stu-id="82c06-135"><a id="queues"></a>Related topics covered by hello queues how-tooarticle</span></span>
<span data-ttu-id="82c06-136">Zie voor informatie over hoe toohandle tabellen verwerken geactiveerd door een wachtrijbericht of voor de WebJobs SDK scenario's geen specifieke tootable verwerking, [hoe toouse Azure queue storage Hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="82c06-136">For information about how toohandle table processing triggered by a queue message, or for WebJobs SDK scenarios not specific tootable processing, see [How toouse Azure queue storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="82c06-137">Onderwerpen in dit artikel zijn Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="82c06-137">Topics covered in that article include hello following:</span></span>

* <span data-ttu-id="82c06-138">Async-functies</span><span class="sxs-lookup"><span data-stu-id="82c06-138">Async functions</span></span>
* <span data-ttu-id="82c06-139">Meerdere exemplaren</span><span class="sxs-lookup"><span data-stu-id="82c06-139">Multiple instances</span></span>
* <span data-ttu-id="82c06-140">Correct afsluiten</span><span class="sxs-lookup"><span data-stu-id="82c06-140">Graceful shutdown</span></span>
* <span data-ttu-id="82c06-141">Kenmerken in de hoofdtekst van een functie Hallo WebJobs SDK gebruiken</span><span class="sxs-lookup"><span data-stu-id="82c06-141">Use WebJobs SDK attributes in hello body of a function</span></span>
* <span data-ttu-id="82c06-142">Hallo SDK verbindingsreeksen instellen in code</span><span class="sxs-lookup"><span data-stu-id="82c06-142">Set hello SDK connection strings in code</span></span>
* <span data-ttu-id="82c06-143">Waarden instellen voor de WebJobs SDK constructorparameters in code</span><span class="sxs-lookup"><span data-stu-id="82c06-143">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="82c06-144">Een functie handmatig activeren</span><span class="sxs-lookup"><span data-stu-id="82c06-144">Trigger a function manually</span></span>
* <span data-ttu-id="82c06-145">Schrijven Logboeken</span><span class="sxs-lookup"><span data-stu-id="82c06-145">Write logs</span></span>

## <span data-ttu-id="82c06-146"><a id="nextsteps"></a> Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="82c06-146"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="82c06-147">Deze handleiding hebt gekregen code voorbeelden die tonen hoe toohandle algemene scenario's voor het werken met Azure-tabellen.</span><span class="sxs-lookup"><span data-stu-id="82c06-147">This guide has provided code samples that show how toohandle common scenarios for working with Azure tables.</span></span> <span data-ttu-id="82c06-148">Voor meer informatie over hoe toouse Azure WebJobs en Hallo WebJobs SDK zien [Azure WebJobs aanbevolen Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="82c06-148">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

