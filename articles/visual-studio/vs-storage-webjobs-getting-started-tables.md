---
title: aaaGetting gestart met Azure storage en Visual Studio verbonden services (webtaak projecten)
description: Hoe tooget gestart met Azure Table storage in een Azure WebJobs-project in Visual Studio nadat tooa storage-account met Visual Studio verbinding services verbonden
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 061a6c46-0592-4e5d-aced-ab7498481cde
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 80d9f8d8b493ce612623dfed7e89325fb154a1c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-storage-azure-webjob-projects"></a>Aan de slag met Azure Storage (Azure webtaak projecten)
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a>Overzicht
Dit artikel vindt u C#-codevoorbeelden die laten zien hoe toouse hello Azure WebJobs SDK versie 1.x Hello Azure table storage-service. Hallo-codevoorbeelden gebruiken Hallo [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) versie 1.x.

Hello Azure Table storage-service kunt u toostore grote hoeveelheden gestructureerde gegevens. Hallo-service is een NoSQL-gegevensarchief die geverifieerde aanroepen vanuit binnen en buiten hello Azure-cloud accepteert. Azure-tabellen zijn ideaal voor het opslaan van gestructureerde, niet-relationele gegevens.  Zie [aan de slag met Azure Table storage met .NET](../cosmos-db/table-storage-how-to-use-dotnet.md#create-a-table) voor meer informatie.

Een aantal codefragmenten Hallo Hallo weergeven **tabel** kenmerk wordt gebruikt in de functies die worden genoemd handmatig, dat wil zeggen, niet met behulp van een Hallo trigger kenmerken.

## <a name="how-tooadd-entities-tooa-table"></a>Hoe tooadd entiteiten tooa tabel
tooadd entiteiten tooa tabel, gebruik Hallo **tabel** kenmerk met een **ICollector<T>**  of **IAsyncCollector<T>**  parameter waar **T** Hallo schema geeft Hallo entiteiten gewenste tooadd. Hallo kenmerkconstructor tekenreeksparameter een waarmee Hallo-naam van het Hallo-tabel.

Hallo codevoorbeeld voegt **persoon** entiteiten tooa tabel met de naam *inkomend*.

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

Doorgaans Hallo type die u met gebruikt **ICollector** is afgeleid van **TableEntity** of implementeert **ITableEntity**, maar heeft geen aan. Een van de volgende Hallo **persoon** werk klassen met Hallo-code die wordt weergegeven in de voorgaande Hallo **inkomend** methode.

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

Als u wilt dat toowork rechtstreeks met hello Azure storage-API, kunt u toevoegen een **CloudStorageAccount** parameter toohello methodehandtekening.

## <a name="real-time-monitoring"></a>Realtime-controle
Omdat ingress-functies worden vaak grote hoeveelheden gegevens verwerken, biedt Hallo WebJobs SDK dashboard realtime controlegegevens. Hallo **aanroep logboek** gedeelte wordt uitgelegd of Hallo-functie nog steeds wordt uitgevoerd.

![Inkomend functie uitgevoerd](./media/vs-storage-webjobs-getting-started-tables/ingressrunning.png)

Hallo **aanroep Details** pagina rapporten Hallo van functie voortgang (aantal entiteiten dat is geschreven) wanneer deze actief is en u een kans tooabort biedt deze.

![Inkomend functie uitgevoerd](./media/vs-storage-webjobs-getting-started-tables/ingressprogress.png)

Wanneer de functie Hallo is voltooid, hello **aanroep Details** pagina rapporten Hallo aantal geschreven rijen.

![Inkomend functie is voltooid](./media/vs-storage-webjobs-getting-started-tables/ingresssuccess.png)

## <a name="how-tooread-multiple-entities-from-a-table"></a>Hoe tooread meerdere entiteiten uit een tabel
een tabel tooread gebruiken Hallo **tabel** kenmerk met een **IQueryable<T>**  parameter waarin typen **T** is afgeleid van **TableEntity**of implementeert **ITableEntity**.

Hallo codevoorbeeld leest en registreert alle rijen van Hallo **inkomend** tabel:

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

### <a name="how-tooread-a-single-entity-from-a-table"></a>Hoe tooread één entiteit uit een tabel
Er is een **tabel** kenmerkconstructor met twee extra parameters die u Hallo partitiesleutel en rijsleutel opgeven wanneer u toobind tooa één Tabelentiteit wilt laten.

Hallo codevoorbeeld leest de rij in een tabel voor een **persoon** entiteit op basis van partitie sleutel- en sleutelwaarden in een wachtrijbericht ontvangen:  

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


Hallo **persoon** klasse in dit voorbeeld heeft geen tooimplement **ITableEntity**.

## <a name="how-toouse-hello-net-storage-api-directly-toowork-with-a-table"></a>Hoe toouse .NET opslag API Hallo rechtstreeks toowork met een tabel
U kunt ook Hallo **tabel** kenmerk met een **CloudTable** -object voor meer flexibiliteit bij het werken met een tabel.

Hallo volgende code voorbeeld wordt een **CloudTable** object tooadd een enkele entiteit toohello *inkomend* tabel.

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

Voor meer informatie over het toouse hello **CloudTable** object, Zie [aan de slag met Azure Table storage met .NET](../storage/storage-dotnet-how-to-use-tables.md).

## <a name="related-topics-covered-by-hello-queues-how-tooarticle"></a>Verwante onderwerpen Hallo wachtrijen hoe-tooarticle vallen
Zie voor informatie over hoe toohandle tabellen verwerken geactiveerd door een wachtrijbericht of voor de WebJobs SDK scenario's geen specifieke tootable verwerking, [aan de slag met Azure Queue storage en Visual Studio verbonden services (webtaak projecten) ](../storage/vs-storage-webjobs-getting-started-queues.md).

## <a name="next-steps"></a>Volgende stappen
In dit artikel hebt gekregen code voorbeelden die tonen hoe toohandle algemene scenario's voor het werken met Azure-tabellen. Voor meer informatie over hoe toouse Azure WebJobs en Hallo WebJobs SDK zien [documentatiebronnen Azure WebJobs](http://go.microsoft.com/fwlink/?linkid=390226).

