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
# <a name="how-toouse-azure-table-storage-with-hello-webjobs-sdk"></a>Hoe toouse Azure table storage Hello WebJobs SDK
## <a name="overview"></a>Overzicht
In deze handleiding vindt u voorbeelden van C#-code die tonen hoe tooread en write Azure-opslag met behulp van tabellen [WebJobs SDK](websites-dotnet-webjobs-sdk.md) versie 1.x.

Hallo handleiding wordt ervan uitgegaan dat u weet [hoe een webtaak-project in Visual Studio met verbinding toocreate dat punt tooyour storage-account tekenreeksen](websites-dotnet-webjobs-sdk-get-started.md) of te[meerdere opslagaccounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).

Een aantal codefragmenten Hallo Hallo weergeven `Table` kenmerk wordt gebruikt in de functies die zijn [handmatig wordt aangeroepen](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), dat wil zeggen, niet met behulp van een Hallo trigger kenmerken. 

## <a id="ingress"></a>Hoe tooadd entiteiten tooa tabel
tooadd entiteiten tooa tabel, gebruik Hallo `Table` kenmerk met een `ICollector<T>` of `IAsyncCollector<T>` parameter waar `T` Hallo schema geeft Hallo entiteiten gewenste tooadd. Hallo kenmerkconstructor tekenreeksparameter een waarmee Hallo-naam van het Hallo-tabel. 

Hallo codevoorbeeld voegt `Person` entiteiten tooa tabel met de naam *inkomend*.

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

Doorgaans Hallo type die u met gebruikt `ICollector` is afgeleid van `TableEntity` of implementeert `ITableEntity`, maar heeft geen aan. Een van de volgende Hallo `Person` werk klassen met Hallo-code die wordt weergegeven in de voorgaande Hallo `Ingress` methode.

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

Als u wilt dat toowork rechtstreeks met hello Azure storage-API, kunt u toevoegen een `CloudStorageAccount` parameter toohello methodehandtekening.

## <a id="monitor"></a>Realtime-controle
Omdat ingress-functies worden vaak grote hoeveelheden gegevens verwerken, biedt Hallo WebJobs SDK dashboard realtime controlegegevens. Hallo **aanroep logboek** gedeelte wordt uitgelegd of Hallo-functie nog steeds wordt uitgevoerd.

![Inkomend functie uitgevoerd](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressrunning.png)

Hallo **aanroep Details** pagina rapporten Hallo van functie voortgang (aantal entiteiten dat is geschreven) wanneer deze actief is en u een kans tooabort biedt deze. 

![Inkomend functie uitgevoerd](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressprogress.png)

Wanneer de functie Hallo is voltooid, hello **aanroep Details** pagina rapporten Hallo aantal geschreven rijen.

![Inkomend functie is voltooid](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingresssuccess.png)

## <a id="multiple"></a>Hoe tooread meerdere entiteiten uit een tabel
een tabel tooread gebruiken Hallo `Table` kenmerk met een `IQueryable<T>` parameter waarin typen `T` is afgeleid van `TableEntity` of implementeert `ITableEntity`.

Hallo codevoorbeeld leest en registreert alle rijen van Hallo `Ingress` tabel:

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

### <a id="readone"></a>Hoe tooread één entiteit uit een tabel
Er is een `Table` kenmerkconstructor met twee extra parameters die u Hallo partitiesleutel en rijsleutel opgeven wanneer u toobind tooa één Tabelentiteit wilt laten.

Hallo codevoorbeeld leest de rij in een tabel voor een `Person` entiteit op basis van partitie sleutel- en sleutelwaarden in een wachtrijbericht ontvangen:  

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


Hallo `Person` klasse in dit voorbeeld heeft geen tooimplement `ITableEntity`.

## <a id="storageapi"></a>Hoe toouse .NET opslag API Hallo rechtstreeks toowork met een tabel
U kunt ook Hallo `Table` kenmerk met een `CloudTable` -object voor meer flexibiliteit bij het werken met een tabel.

Hallo volgende code voorbeeld wordt een `CloudTable` object tooadd een enkele entiteit toohello *inkomend* tabel. 

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

Voor meer informatie over het toouse hello `CloudTable` object, Zie [hoe toouse Table Storage uit het .NET](../cosmos-db/table-storage-how-to-use-dotnet.md). 

## <a id="queues"></a>Verwante onderwerpen Hallo wachtrijen hoe-tooarticle vallen
Zie voor informatie over hoe toohandle tabellen verwerken geactiveerd door een wachtrijbericht of voor de WebJobs SDK scenario's geen specifieke tootable verwerking, [hoe toouse Azure queue storage Hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md). 

Onderwerpen in dit artikel zijn Hallo volgende:

* Async-functies
* Meerdere exemplaren
* Correct afsluiten
* Kenmerken in de hoofdtekst van een functie Hallo WebJobs SDK gebruiken
* Hallo SDK verbindingsreeksen instellen in code
* Waarden instellen voor de WebJobs SDK constructorparameters in code
* Een functie handmatig activeren
* Schrijven Logboeken

## <a id="nextsteps"></a> Volgende stappen
Deze handleiding hebt gekregen code voorbeelden die tonen hoe toohandle algemene scenario's voor het werken met Azure-tabellen. Voor meer informatie over hoe toouse Azure WebJobs en Hallo WebJobs SDK zien [Azure WebJobs aanbevolen Resources](http://go.microsoft.com/fwlink/?linkid=390226).

