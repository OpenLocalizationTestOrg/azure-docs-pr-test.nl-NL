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
# <a name="how-to-use-azure-table-storage-with-the-webjobs-sdk"></a>Azure Table Storage gebruiken met de WebJobs SDK
## <a name="overview"></a>Overzicht
De C#-codevoorbeelden die laten hoe zien te lezen en schrijven van Azure storage-tabellen met behulp van deze handleiding [WebJobs SDK](websites-dotnet-webjobs-sdk.md) versie 1.x.

De handleiding wordt ervan uitgegaan dat u weet [tekenreeksen dat punt naar uw opslagaccount, het maken van een webtaak-project in Visual Studio met verbinding](websites-dotnet-webjobs-sdk-get-started.md) of [meerdere opslagaccounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).

Sommige van de code codefragmenten weergeven de `Table` kenmerk wordt gebruikt in de functies die zijn [handmatig wordt aangeroepen](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual), dat wil zeggen, niet met behulp van een van de trigger-kenmerken. 

## <a id="ingress"></a>Entiteiten toevoegen aan een tabel
U kunt entiteiten toevoegen aan een tabel met de `Table` kenmerk met een `ICollector<T>` of `IAsyncCollector<T>` parameter waar `T` Hiermee geeft u het schema van de entiteiten die u wilt toevoegen. De kenmerkconstructor heeft een tekenreeksparameter gebruikt met de naam van de tabel. 

Het volgende codevoorbeeld wordt toegevoegd `Person` entiteiten aan een tabel met de naam *inkomend*.

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

Meestal het type u gebruiken met `ICollector` is afgeleid van `TableEntity` of implementeert `ITableEntity`, maar heeft geen aan. Een van de volgende `Person` werk klassen met de code die wordt weergegeven in de voorgaande `Ingress` methode.

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

Als u samenwerken met de Azure storage-API wilt, kunt u toevoegen een `CloudStorageAccount` -parameter voor de methodehandtekening.

## <a id="monitor"></a>Realtime-controle
Omdat ingress-functies te vaak grote hoeveelheden gegevens verwerken, kunt het dashboard WebJobs SDK u realtime controlegegevens. De **aanroep logboek** gedeelte wordt uitgelegd of de functie nog steeds wordt uitgevoerd.

![Inkomend functie uitgevoerd](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressrunning.png)

De **aanroep Details** pagina rapporten van de functie voortgang (aantal entiteiten dat is geschreven) wanneer deze actief is en hebt u de mogelijkheid om af te breken deze. 

![Inkomend functie uitgevoerd](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingressprogress.png)

Wanneer de functie is voltooid, de **aanroep Details** pagina rapporteert het aantal rijen dat is geschreven.

![Inkomend functie is voltooid](./media/websites-dotnet-webjobs-sdk-storage-tables-how-to/ingresssuccess.png)

## <a id="multiple"></a>Het lezen van meerdere entiteiten uit een tabel
Als u wilt lezen van een tabel, gebruikt u de `Table` kenmerk met een `IQueryable<T>` parameter waarin typen `T` is afgeleid van `TableEntity` of implementeert `ITableEntity`.

Het volgende codevoorbeeld leest en registreert alle rijen uit de `Ingress` tabel:

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

### <a id="readone"></a>Het lezen van één entiteit uit een tabel
Er is een `Table` kenmerkconstructor met twee aanvullende parameters u de partitiesleutel en de rijsleutel opgeven kunt wanneer u wilt binden aan een met één Tabelentiteit.

Het volgende codevoorbeeld leest de rij in een tabel voor een `Person` entiteit op basis van partitie sleutel- en sleutelwaarden in een wachtrijbericht ontvangen:  

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


De `Person` klasse in dit voorbeeld heeft geen voor het implementeren van `ITableEntity`.

## <a id="storageapi"></a>Het gebruik van de API van de .NET-opslag rechtstreeks aan het werken met een tabel
U kunt ook de `Table` kenmerk met een `CloudTable` -object voor meer flexibiliteit bij het werken met een tabel.

De volgende code voorbeeld wordt een `CloudTable` object toevoegen aan één entiteit de *inkomend* tabel. 

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

Voor meer informatie over het gebruik van de `CloudTable` object, Zie [hoe Table Storage gebruiken met .NET](../cosmos-db/table-storage-how-to-use-dotnet.md). 

## <a id="queues"></a>Verwante onderwerpen gedekt door het wachtrijen how-to artikel
Zie voor meer informatie over het afhandelen van de tabel verwerking geactiveerd door een wachtrijbericht of voor WebJobs SDK scenario's die niet specifiek zijn voor de verwerking van de tabel [Azure queue storage gebruiken met de WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md). 

Onderwerpen in dit artikel omvatten het volgende:

* Async-functies
* Meerdere exemplaren
* Correct afsluiten
* Kenmerken in de hoofdtekst van een functie WebJobs SDK gebruiken
* De SDK-verbindingsreeksen instellen in code
* Waarden instellen voor de WebJobs SDK constructorparameters in code
* Een functie handmatig activeren
* Schrijven Logboeken

## <a id="nextsteps"></a> Volgende stappen
Deze handleiding is opgegeven codevoorbeelden die laten hoe u algemene scenario's zien voor het werken met Azure-tabellen te verwerken. Zie voor meer informatie over het gebruik van Azure WebJobs en de WebJobs SDK [Azure WebJobs aanbevolen Resources](http://go.microsoft.com/fwlink/?linkid=390226).

