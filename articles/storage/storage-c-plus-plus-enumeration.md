---
title: Azure Storage-resources aaaList Hello Opslagclientbibliotheek voor C++ | Microsoft Docs
description: Meer informatie over hoe toouse Hallo aanbieding API's in Microsoft Azure Storage-clientbibliotheek voor C++ tooenumerate containers, blobs, wachtrijen, tabellen en entiteiten.
documentationcenter: .net
services: storage
author: dineshmurthy
manager: jahogg
editor: tysonn
ms.assetid: 33563639-2945-4567-9254-bc4a7e80698f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: dineshm
ms.openlocfilehash: d20a86688938704c24339aa9a1145786783fea5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="list-azure-storage-resources-in-c"></a>Lijst van Azure Storage-resources in C++
Aanbieding-bewerkingen zijn toomany belangrijke ontwikkelscenario's met Azure Storage. Dit artikel wordt beschreven hoe toomost efficiënt objecten in Azure Storage met API's die zijn opgegeven in Microsoft Azure Storage-clientbibliotheek Hallo voor C++ aanbieding Hallo inventariseren.

> [!NOTE]
> Deze handleiding is bedoeld voor hello Azure Storage-clientbibliotheek voor C++ versie 2.x die beschikbaar is via [NuGet](http://www.nuget.org/packages/wastorage) of [GitHub](https://github.com/Azure/azure-storage-cpp).
> 
> 

Hallo Storage-clientbibliotheek biedt tal van manieren toolist of query-objecten in Azure Storage. In dit artikel komen Hallo volgen scenario's:

* Lijst containers in een account
* Lijst met blobs in een container of blob virtuele map
* Lijst met wachtrijen in een account
* Lijst met tabellen in een account
* Query-entiteiten in een tabel

Elk van deze methoden wordt weergegeven als u verschillende overbelastingen voor verschillende scenario's.

## <a name="asynchronous-versus-synchronous"></a>Asynchrone en synchrone
Omdat Hallo Opslagclientbibliotheek voor C++ is gebouwd boven op Hallo [REST C++-bibliotheek](https://github.com/Microsoft/cpprestsdk), we inherent bieden ondersteuning voor asynchrone bewerkingen met behulp van [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html). Bijvoorbeeld:

```cpp
pplx::task<list_blob_item_segment> list_blobs_segmented_async(continuation_token& token) const;
```

Synchrone bewerkingen teruglopen Hallo corresponderende asynchrone bewerkingen:

```cpp
list_blob_item_segment list_blobs_segmented(const continuation_token& token) const
{
    return list_blobs_segmented_async(token).get();
}
```

Als u met meerdere threads toepassingen of services werkt, raden wij aan dat u Hallo async API's rechtstreeks in plaats van het maken van een thread toocall Hallo synchronisatie API's, die aanzienlijk heeft impact op de prestaties van uw.

## <a name="segmented-listing"></a>Gesegmenteerde aanbieding
Hallo schaal van cloud-opslag vereist gesegmenteerde aanbieding. U kunt bijvoorbeeld via een miljoen blobs in een Azure blob-container of via een miljard entiteiten in een Azure-tabel hebben. Dit zijn geen theoretische cijfers, maar de informatie over het gebruik van echte klantaanvragen.

Daarom is het niet praktisch toolist alle objecten in een enkel antwoord. In plaats daarvan kunt u objecten met behulp van paginering aanbieden. Elk van de API's aanbieding Hallo heeft een *gesegmenteerde* overbelasting.

Hallo-antwoord voor het uitvoeren van een gesegmenteerde aanbieding omvat:

* <i>_Segment</i>, die Hallo set resultaten geretourneerd voor een enkele aanroep toohello aanbieding API bevat.
* *continuation_token*, die de volgende oproep toohello wordt doorgegeven in volgorde tooget Hallo volgende pagina van de resultaten. Wanneer er geen meer resultaten tooreturn, is Hallo vervolgtoken null.

Bijvoorbeeld, een aanroep van typische toolist alle blobs in een container eruit als Hallo codefragment te volgen. Hallo-code is beschikbaar in onze [voorbeelden](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):

```cpp
// List blobs in hello blob container
azure::storage::continuation_token token;
do
{
    azure::storage::list_blob_item_segment segment = container.list_blobs_segmented(token);
    for (auto it = segment.results().cbegin(); it != segment.results().cend(); ++it)
{
    if (it->is_blob())
    {
        process_blob(it->as_blob());
    }
    else
    {
        process_diretory(it->as_directory());
    }
}

    token = segment.continuation_token();
}
while (!token.empty());
```

Houd er rekening mee dat het aantal resultaten in een pagina Hallo kan worden beheerd door Hallo parameter *max_results* in Hallo overbelasting van elke API, bijvoorbeeld:

```cpp
list_blob_item_segment list_blobs_segmented(const utility::string_t& prefix, bool use_flat_blob_listing,
    blob_listing_details::values includes, int max_results, const continuation_token& token,
    const blob_request_options& options, operation_context context)
```

Als u geen Hallo opgeeft *max_results* parameter, Hallo standaard maximale waarde van too5000 resultaten wordt geretourneerd als één pagina.

Let ook op een query op Azure Table storage kan geen records of minder records zijn dan de waarde van Hallo Hallo retourneren *max_results* parameter die u hebt opgegeven, zelfs als Hallo vervolgtoken niet leeg is. Een reden hiervoor is mogelijk dat Hallo-query kan niet worden voltooid in de vijf seconden. Zolang Hallo vervolgtoken niet leeg is, Hallo query moet worden voortgezet en uw code mogen niet Hallo-grootte van het resultaat van een segment aannemen.

Hallo aanbevolen coderen patroon voor de meeste scenario is onderverdeeld op te nemen, waarmee u expliciete voortgang van de aanbieding of uitvoeren van query's en hoe Hallo service tooeach aanvraag reageert. Met name voor C++-toepassingen of services kunt lager niveau besturingselement Hallo aanbieding voortgang besturingselement geheugen en de prestaties.

## <a name="greedy-listing"></a>Greedy aanbieding
Eerdere versies van Hallo Opslagclientbibliotheek voor C++ (Preview-versies 0.5.0 en eerder) niet-gesegmenteerde aanbieding API's voor tabellen en wachtrijen, zoals in het volgende voorbeeld Hallo opgenomen:

```cpp
std::vector<cloud_table> list_tables(const utility::string_t& prefix) const;
std::vector<table_entity> execute_query(const table_query& query) const;
std::vector<cloud_queue> list_queues() const;
```

Deze methoden zijn geïmplementeerd als wrappers gesegmenteerde API's. Voor elke reactie van gesegmenteerde aanbieding Hallo code Hallo resultaten tooa vector toegevoegd en alle resultaten geretourneerd nadat de volledige containers Hallo zijn gescand.

Deze methode werkt mogelijk wanneer Hallo storage-account of de tabel een klein aantal objecten bevat. Echter met een toename in aantal objecten Hallo kan Hallo geheugen vereist verhogen zonder beperking, omdat alle resultaten bleef in het geheugen. Één aanbieding bewerking kan erg lang duren, tijdens welke Hallo aanroeper geen informatie over de voortgang heeft.

Deze greedy aanbieding API's in Hallo SDK niet bestaan in C#, Java, of Hallo JavaScript Node.js-omgeving. tooavoid hello potentiële problemen van het gebruik van deze greedy API's, wordt deze verwijderd in versie 0.6.0 Preview.

Als uw code deze greedy API's aanroept:

```cpp
std::vector<azure::storage::table_entity> entities = table.execute_query(query);
for (auto it = entities.cbegin(); it != entities.cend(); ++it)
{
    process_entity(*it);
}
```

Vervolgens moet u uw code wijzigen toouse Hallo gesegmenteerde aanbieding API's:

```cpp
azure::storage::continuation_token token;
do
{
    azure::storage::table_query_segment segment = table.execute_query_segmented(query, token);
    for (auto it = segment.results().cbegin(); it != segment.results().cend(); ++it)
    {
        process_entity(*it);
    }

    token = segment.continuation_token();
} while (!token.empty());
```

Door op te geven Hallo *max_results* parameter van Hallo segment kan verdeeld tussen Hallo aantallen aanvragen en geheugen gebruik toomeet prestatie-overwegingen voor uw toepassing.

Bovendien, als u gesegmenteerde aanbieding API's gebruiken, maar Hallo gegevens opslaan in een lokale verzameling in een style 'greedy', wordt ook aangeraden dat u uw code toohandle opslaan van gegevens in een lokale verzameling zorgvuldig op grote schaal opsplitsen.

## <a name="lazy-listing"></a>Vertraagde aanbieding
Hoewel greedy aanbieding potentiële problemen gegenereerd, is het handig als er niet te veel objecten in het Hallo-container.

Als u ook C# of Oracle Java SDK's gebruikt, kunt u moet bekend bent met Hallo inventariseerbare programming model een vertraagde--stijl op te nemen biedt, waarbij Hallo gegevens bij een bepaalde offset worden alleen opgehaald als dat nodig is. In C++ kunt biedt Hallo iterator gebaseerde sjabloon ook een soortgelijke benadering.

Een typische vertraagde aanbieding API, met behulp van **list_blobs** bijvoorbeeld zo uitziet:

```cpp
list_blob_item_iterator list_blobs() const;
```

Een typische codefragment dat Hallo vertraagde aanbieding patroon gebruikt uitzien als volgt:

```cpp
// List blobs in hello blob container
azure::storage::list_blob_item_iterator end_of_results;
for (auto it = container.list_blobs(); it != end_of_results; ++it)
{
    if (it->is_blob())
    {
        process_blob(it->as_blob());
    }
    else
    {
        process_directory(it->as_directory());
    }
}
```

Houd er rekening mee vertraagde aanbieding is alleen beschikbaar in synchrone modus.

Vergeleken met greedy aanbieding, haalt vertraagde aanbieding gegevens alleen indien nodig. Onder Hallo dekt ophaalt het gegevens uit Azure Storage alleen wanneer de volgende iterator Hallo is verplaatst naar de volgende segment. Daarom geheugengebruik wordt beheerd met een begrensde grootte en Hallo-bewerking is snel.

Vertraagde aanbieding API's worden opgenomen in Hallo Opslagclientbibliotheek voor C++ in versie 2.2.0.

## <a name="conclusion"></a>Conclusie
In dit artikel wordt besproken verschillende overbelastingen voor het aanbieden van API's voor verschillende objecten in Hallo Opslagclientbibliotheek voor C++. toosummarize:

* Asynchrone APIs ten sterkste aangeraden onder scenario's met meerdere threads.
* Gesegmenteerde aanbieding wordt aanbevolen voor de meeste scenario's.
* Vertraagde aanbieding is opgegeven in de bibliotheek Hallo als een handige wrapper in synchrone scenario's.
* Greedy aanbieding wordt niet aanbevolen en is verwijderd uit het Hallo-bibliotheek.

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over Azure Storage en -clientbibliotheek voor C++ Hallo resources te volgen.

* [Hoe toouse C++ Blob-opslag](storage-c-plus-plus-how-to-use-blobs.md)
* [Hoe toouse Table Storage uit het C++](storage-c-plus-plus-how-to-use-tables.md)
* [Hoe toouse Queue Storage vanuit C++](storage-c-plus-plus-how-to-use-queues.md)
* [Azure Storage-clientbibliotheek voor C++ API-documentatie.](http://azure.github.io/azure-storage-cpp/)
* [Blog van het Azure Storage-team](http://blogs.msdn.com/b/windowsazurestorage/)
* [Documentatie bij Azure Storage](https://azure.microsoft.com/documentation/services/storage/)

