---
title: aaaGetting gestart met Azure storage en Visual Studio verbonden services (webtaak projecten)
description: Hoe tooget gestart met Azure Table storage in een Azure WebJobs-project in Visual Studio nadat tooa storage-account met Visual Studio verbinding services verbonden
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 061a6c46-0592-4e5d-aced-ab7498481cde
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 448dee3369207062ee85c6636c84bcb4e26a2085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-storage-azure-webjob-projects"></a><span data-ttu-id="f6a9f-103">Aan de slag met Azure Storage (Azure webtaak projecten)</span><span class="sxs-lookup"><span data-stu-id="f6a9f-103">Getting Started with Azure Storage (Azure WebJob Projects)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="f6a9f-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="f6a9f-104">Overview</span></span>
<span data-ttu-id="f6a9f-105">Dit artikel vindt u C#-codevoorbeelden die laten zien hoe toouse hello Azure WebJobs SDK versie 1.x Hello Azure table storage-service.</span><span class="sxs-lookup"><span data-stu-id="f6a9f-105">This article provides C# code samples that show show how toouse hello Azure WebJobs SDK version 1.x with hello Azure table storage service.</span></span> <span data-ttu-id="f6a9f-106">Hallo-codevoorbeelden gebruiken Hallo [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) versie 1.x.</span><span class="sxs-lookup"><span data-stu-id="f6a9f-106">hello code samples use hello [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="f6a9f-107">Hello Azure Table storage-service kunt u toostore grote hoeveelheden gestructureerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="f6a9f-107">hello Azure Table storage service enables you toostore large amounts of structured data.</span></span> <span data-ttu-id="f6a9f-108">Hallo-service is een NoSQL-gegevensarchief die geverifieerde aanroepen vanuit binnen en buiten hello Azure-cloud accepteert.</span><span class="sxs-lookup"><span data-stu-id="f6a9f-108">hello service is a NoSQL datastore that accepts authenticated calls from inside and outside hello Azure cloud.</span></span> <span data-ttu-id="f6a9f-109">Azure-tabellen zijn ideaal voor het opslaan van gestructureerde, niet-relationele gegevens.</span><span class="sxs-lookup"><span data-stu-id="f6a9f-109">Azure tables are ideal for storing structured, non-relational data.</span></span>  <span data-ttu-id="f6a9f-110">Zie [aan de slag met Azure Table storage met .NET](storage-dotnet-how-to-use-tables.md#create-a-table) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f6a9f-110">See [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md#create-a-table) for more information.</span></span>

<span data-ttu-id="f6a9f-111">Een aantal codefragmenten Hallo Hallo weergeven **tabel** kenmerk wordt gebruikt in de functies die worden genoemd handmatig, dat wil zeggen, niet met behulp van een Hallo trigger kenmerken.</span><span class="sxs-lookup"><span data-stu-id="f6a9f-111">Some of hello code snippets show hello **Table** attribute used in functions that are called manually, that is, not by using one of hello trigger attributes.</span></span>

## <a name="how-tooadd-entities-tooa-table"></a><span data-ttu-id="f6a9f-112">Hoe tooadd entiteiten tooa tabel</span><span class="sxs-lookup"><span data-stu-id="f6a9f-112">How tooadd entities tooa table</span></span>
<span data-ttu-id="f6a9f-113">tooadd entiteiten tooa tabel, gebruik Hallo **tabel** kenmerk met een **ICollector<T>**  of **IAsyncCollector<T>**  parameter waar **T** Hallo schema geeft Hallo entiteiten gewenste tooadd.</span><span class="sxs-lookup"><span data-stu-id="f6a9f-113">tooadd entities tooa table, use hello **Table** attribute with an **ICollector<T>** or **IAsyncCollector<T>** parameter where **T** specifies hello schema of hello entities you want tooadd.</span></span> <span data-ttu-id="f6a9f-114">Hallo kenmerkconstructor tekenreeksparameter een waarmee Hallo-naam van het Hallo-tabel.</span><span class="sxs-lookup"><span data-stu-id="f6a9f-114">hello attribute constructor takes a string parameter that specifies hello name of hello table.</span></span>

<span data-ttu-id="f6a9f-115">Hallo codevoorbeeld voegt **persoon** entiteiten tooa tabel met de naam *inkomend*.</span><span class="sxs-lookup"><span data-stu-id="f6a9f-115">hello following code sample adds **Person** entities tooa table named *Ingress*.</span></span>

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

<span data-ttu-id="f6a9f-116">Doorgaans Hallo type die u met gebruikt **ICollector** is afgeleid van **TableEntity** of implementeert **ITableEntity**, maar heeft geen aan.</span><span class="sxs-lookup"><span data-stu-id="f6a9f-116">Typically hello type you use with **ICollector** derives from **TableEntity** or implements **ITableEntity**, but it doesn't have to.</span></span> <span data-ttu-id="f6a9f-117">Een van de volgende Hallo **persoon** werk klassen met Hallo-code die wordt weergegeven in de voorgaande Hallo **inkomend** methode.</span><span class="sxs-lookup"><span data-stu-id="f6a9f-117">Either of hello following **Person** classes work with hello code shown in hello preceding **Ingress** method.</span></span>

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

<span data-ttu-id="f6a9f-118">Als u wilt dat toowork rechtstreeks met hello Azure storage-API, kunt u toevoegen een **CloudStorageAccount** parameter toohello methodehandtekening.</span><span class="sxs-lookup"><span data-stu-id="f6a9f-118">If you want toowork directly with hello Azure storage API, you can add a **CloudStorageAccount** parameter toohello method signature.</span></span>

## <a name="real-time-monitoring"></a><span data-ttu-id="f6a9f-119">Realtime-controle</span><span class="sxs-lookup"><span data-stu-id="f6a9f-119">Real-time monitoring</span></span>
<span data-ttu-id="f6a9f-120">Omdat ingress-functies worden vaak grote hoeveelheden gegevens verwerken, biedt Hallo WebJobs SDK dashboard realtime controlegegevens.</span><span class="sxs-lookup"><span data-stu-id="f6a9f-120">Because data ingress functions often process large volumes of data, hello WebJobs SDK dashboard provides real-time monitoring data.</span></span> <span data-ttu-id="f6a9f-121">Hallo **aanroep logboek** gedeelte wordt uitgelegd of Hallo-functie nog steeds wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f6a9f-121">hello **Invocation Log** section tells you if hello function is still running.</span></span>

![Inkomend functie uitgevoerd](./media/vs-storage-webjobs-getting-started-tables/ingressrunning.png)

<span data-ttu-id="f6a9f-123">Hallo **aanroep Details** pagina rapporten Hallo van functie voortgang (aantal entiteiten dat is geschreven) wanneer deze actief is en u een kans tooabort biedt deze.</span><span class="sxs-lookup"><span data-stu-id="f6a9f-123">hello **Invocation Details** page reports hello function's progress (number of entities written) while it's running and gives you an opportunity tooabort it.</span></span>

![Inkomend functie uitgevoerd](./media/vs-storage-webjobs-getting-started-tables/ingressprogress.png)

<span data-ttu-id="f6a9f-125">Wanneer de functie Hallo is voltooid, hello **aanroep Details** pagina rapporten Hallo aantal geschreven rijen.</span><span class="sxs-lookup"><span data-stu-id="f6a9f-125">When hello function finishes, hello **Invocation Details** page reports hello number of rows written.</span></span>

![Inkomend functie is voltooid](./media/vs-storage-webjobs-getting-started-tables/ingresssuccess.png)

## <a name="how-tooread-multiple-entities-from-a-table"></a><span data-ttu-id="f6a9f-127">Hoe tooread meerdere entiteiten uit een tabel</span><span class="sxs-lookup"><span data-stu-id="f6a9f-127">How tooread multiple entities from a table</span></span>
<span data-ttu-id="f6a9f-128">een tabel tooread gebruiken Hallo **tabel** kenmerk met een **IQueryable<T>**  parameter waarin typen **T** is afgeleid van **TableEntity**of implementeert **ITableEntity**.</span><span class="sxs-lookup"><span data-stu-id="f6a9f-128">tooread a table, use hello **Table** attribute with an **IQueryable<T>** parameter where type **T** derives from **TableEntity** or implements **ITableEntity**.</span></span>

<span data-ttu-id="f6a9f-129">Hallo codevoorbeeld leest en registreert alle rijen van Hallo **inkomend** tabel:</span><span class="sxs-lookup"><span data-stu-id="f6a9f-129">hello following code sample reads and logs all rows from hello **Ingress** table:</span></span>

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

### <a name="how-tooread-a-single-entity-from-a-table"></a><span data-ttu-id="f6a9f-130">Hoe tooread één entiteit uit een tabel</span><span class="sxs-lookup"><span data-stu-id="f6a9f-130">How tooread a single entity from a table</span></span>
<span data-ttu-id="f6a9f-131">Er is een **tabel** kenmerkconstructor met twee extra parameters die u Hallo partitiesleutel en rijsleutel opgeven wanneer u toobind tooa één Tabelentiteit wilt laten.</span><span class="sxs-lookup"><span data-stu-id="f6a9f-131">There is a **Table** attribute constructor with two additional parameters that let you specify hello partition key and row key when you want toobind tooa single table entity.</span></span>

<span data-ttu-id="f6a9f-132">Hallo codevoorbeeld leest de rij in een tabel voor een **persoon** entiteit op basis van partitie sleutel- en sleutelwaarden in een wachtrijbericht ontvangen:</span><span class="sxs-lookup"><span data-stu-id="f6a9f-132">hello following code sample reads a table row for a **Person** entity based on partition key and row key values received in a queue message:</span></span>  

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


<span data-ttu-id="f6a9f-133">Hallo **persoon** klasse in dit voorbeeld heeft geen tooimplement **ITableEntity**.</span><span class="sxs-lookup"><span data-stu-id="f6a9f-133">hello **Person** class in this example does not have tooimplement **ITableEntity**.</span></span>

## <a name="how-toouse-hello-net-storage-api-directly-toowork-with-a-table"></a><span data-ttu-id="f6a9f-134">Hoe toouse .NET opslag API Hallo rechtstreeks toowork met een tabel</span><span class="sxs-lookup"><span data-stu-id="f6a9f-134">How toouse hello .NET Storage API directly toowork with a table</span></span>
<span data-ttu-id="f6a9f-135">U kunt ook Hallo **tabel** kenmerk met een **CloudTable** -object voor meer flexibiliteit bij het werken met een tabel.</span><span class="sxs-lookup"><span data-stu-id="f6a9f-135">You can also use hello **Table** attribute with a **CloudTable** object for more flexibility in working with a table.</span></span>

<span data-ttu-id="f6a9f-136">Hallo volgende code voorbeeld wordt een **CloudTable** object tooadd een enkele entiteit toohello *inkomend* tabel.</span><span class="sxs-lookup"><span data-stu-id="f6a9f-136">hello following code sample uses a **CloudTable** object tooadd a single entity toohello *Ingress* table.</span></span>

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

<span data-ttu-id="f6a9f-137">Voor meer informatie over het toouse hello **CloudTable** object, Zie [aan de slag met Azure Table storage met .NET](storage-dotnet-how-to-use-tables.md).</span><span class="sxs-lookup"><span data-stu-id="f6a9f-137">For more information about how toouse hello **CloudTable** object, see [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md).</span></span>

## <a name="related-topics-covered-by-hello-queues-how-tooarticle"></a><span data-ttu-id="f6a9f-138">Verwante onderwerpen Hallo wachtrijen hoe-tooarticle vallen</span><span class="sxs-lookup"><span data-stu-id="f6a9f-138">Related topics covered by hello queues how-tooarticle</span></span>
<span data-ttu-id="f6a9f-139">Zie voor informatie over hoe toohandle tabellen verwerken geactiveerd door een wachtrijbericht of voor de WebJobs SDK scenario's geen specifieke tootable verwerking, [aan de slag met Azure Queue storage en Visual Studio verbonden services (webtaak projecten) ](vs-storage-webjobs-getting-started-queues.md).</span><span class="sxs-lookup"><span data-stu-id="f6a9f-139">For information about how toohandle table processing triggered by a queue message, or for WebJobs SDK scenarios not specific tootable processing, see [Getting started with Azure Queue storage and Visual Studio connected services (WebJob Projects)](vs-storage-webjobs-getting-started-queues.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6a9f-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f6a9f-140">Next steps</span></span>
<span data-ttu-id="f6a9f-141">In dit artikel hebt gekregen code voorbeelden die tonen hoe toohandle algemene scenario's voor het werken met Azure-tabellen.</span><span class="sxs-lookup"><span data-stu-id="f6a9f-141">This article has provided code samples that show how toohandle common scenarios for working with Azure tables.</span></span> <span data-ttu-id="f6a9f-142">Voor meer informatie over hoe toouse Azure WebJobs en Hallo WebJobs SDK zien [documentatiebronnen Azure WebJobs](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="f6a9f-142">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

