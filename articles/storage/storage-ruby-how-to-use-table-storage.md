---
title: aaaHow toouse Azure Table Storage met Ruby | Microsoft Docs
description: Gestructureerde gegevens opslaan in Hallo cloud met Azure Table storage, een NoSQL-gegevensarchief.
services: storage
documentationcenter: ruby
author: mmacy
manager: timlt
editor: 
ms.assetid: 047cd9ff-17d3-4c15-9284-1b5cc61a3224
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 9c77ff9f384a776c9bc075b60b351685c61acc36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-from-ruby"></a>Hoe toouse Azure Table Storage met Ruby
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Overzicht
Deze handleiding wordt getoond hoe tooperform algemene scenario's met behulp van hello Azure Table-service. Hallo-voorbeelden zijn geschreven met behulp van Hallo Ruby-API. Hallo scenario's worden behandeld: **maken en verwijderen van een tabel, invoegen en het uitvoeren van query's entiteiten in een tabel**.

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a>Een Ruby-toepassing maken
Zie voor instructies hoe toocreate een Ruby toepassing [Ruby op Rails webtoepassing op een virtuele machine van Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).

## <a name="configure-your-application-tooaccess-storage"></a>Uw toepassing tooaccess opslag configureren
toouse Azure Storage, moet u toodownload en gebruik Hallo Ruby azure-pakket dat bevat een set met gemak bibliotheken die met Hallo Storage REST-services communiceren.

### <a name="use-rubygems-tooobtain-hello-package"></a>RubyGems tooobtain Hallo pakket gebruiken
1. Een opdrachtregelinterface gebruiken zoals **PowerShell** (Windows), **Terminal** (Mac) of **Bash** (Unix).
2. Type **gem installeren azure** in Hallo opdracht venster tooinstall Hallo gem en afhankelijkheden.

### <a name="import-hello-package"></a>Hallo-pakket importeren
Uw favoriete teksteditor gebruiken, voegt Hallo toohello bovenaan Hallo Ruby bestand waarin u van plan toouse opslag bent te volgen:

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a>Een Azure Storage-verbinding instellen
Hello azure-module lezen Hallo omgevingsvariabelen **AZURE\_opslag\_ACCOUNT** en **AZURE\_opslag\_toegang\_sleutel**vereist tooconnect tooyour Azure Storage-account voor meer informatie. Als deze omgevingsvariabelen zijn niet ingesteld, moet u de accountgegevens Hallo voordat u **Azure::TableService** Hello code te volgen:

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

tooobtain deze waarden van een klassiek of Resource Manager-storage-account in hello Azure-portal:

1. Meld u bij toohello [Azure-portal](https://portal.azure.com).
2. Navigeer toohello gewenste toouse storage-account.
3. Klik op Hallo instellingenblade op Hallo rechts **toegangstoetsen**.
4. Hallo toegang sleutels blade die wordt weergegeven, ziet u Hallo toegangssleutel 1 en toegangssleutel 2. U kunt een van beide gebruiken.
5. Klik op Hallo kopiëren pictogram toocopy Hallo sleutel toohello Klembord.

tooobtain deze waarden van een klassieke storage-account in de klassieke Azure portal Hallo:

1. Meld u bij toohello [klassieke Azure-portal](https://manage.windowsazure.com).
2. Navigeer toohello gewenste toouse storage-account.
3. Klik op **TOEGANGSSLEUTELS beheren** Hallo Hallo navigatiedeelvenster onderaan in.
4. In het pop-upvenster hello ziet u opslagaccountnaam hello, de primaire toegangssleutel en de secundaire toegangssleutel. U kunt voor toegangssleutel, Hallo een primaire of secundaire één Hallo gebruiken.
5. Klik op Hallo kopiëren pictogram toocopy Hallo sleutel toohello Klembord.

## <a name="create-a-table"></a>Een tabel maken
Hallo **Azure::TableService** object kunt u samenwerken met tabellen en entiteiten. een tabel toocreate gebruiken Hallo **maken\_table()** methode. Hallo volgende voorbeeld wordt een tabel of afdrukken bestellen Hallo fout indien deze aanwezig is.

```ruby
azure_table_service = Azure::TableService.new
begin
    azure_table_service.create_table("testtable")
rescue
    puts $!
end
```

## <a name="add-an-entity-tooa-table"></a>Een entiteit tooa tabel toevoegen
een entiteit tooadd eerst een hash-object dat de entiteitseigenschappen van uw definieert maken. Houd er rekening mee dat voor elke entiteit moet u een **PartitionKey** en **RowKey**. Dit Hallo unieke id's van de entiteiten en zijn waarden die veel sneller dan de andere eigenschappen kunnen worden opgevraagd. Azure Storage maakt gebruik van **PartitionKey** tooautomatically hello tabelentiteiten distribueren via veel opslagknooppunten. Entiteiten met dezelfde Hallo **PartitionKey** zijn opgeslagen op Hallo hetzelfde knooppunt. Hallo **RowKey** is de unieke ID Hallo van Hallo entiteit binnen deze tot behoort Hallo-partitie.

```ruby
entity = { "content" => "test entity",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.insert_entity("testtable", entity)
```

## <a name="update-an-entity"></a>Bijwerken van een entiteit
Er zijn meerdere methoden beschikbaar tooupdate van een bestaande entiteit:

* **bijwerken\_entity():** bijwerken van een bestaande entiteit door deze te vervangen.
* **samenvoegen\_entity():** Updates van een bestaande entiteit door de nieuwe eigenschapswaarden samenvoegen in een bestaande Hallo-entiteit.
* **invoegen\_of\_samenvoegen\_entity():** Updates van een bestaande entiteit door deze te vervangen. Als er is geen entiteit bestaat, wordt er een nieuwe ingevoegd:
* **invoegen\_of\_vervangen\_entity():** Updates van een bestaande entiteit door de nieuwe eigenschapswaarden samenvoegen in een bestaande Hallo-entiteit. Als er is geen entiteit bestaat, wordt er een nieuwe ingevoegd.

Hallo volgende voorbeeld ziet u het bijwerken van een entiteit met **bijwerken\_entity()**:

```ruby
entity = { "content" => "test entity with updated content",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.update_entity("testtable", entity)
```

Met **bijwerken\_entity()** en **samenvoegen\_entity()**als Hallo-entiteit die u wilt bijwerken, mislukt de updatebewerking Hallo bestaat niet. Dus als u wenst dat toostore een entiteit ongeacht of deze al bestaat, moet u in plaats daarvan gebruiken **invoegen\_of\_vervangen\_entity()** of **invoegen\_of \_samenvoegen\_entity()**.

## <a name="work-with-groups-of-entities"></a>Werken met groepen van entiteiten
Soms is het zin toosubmit meerdere bewerkingen samen in een batch-tooensure atomic verwerken door Hallo-server. tooaccomplish dat, u eerst maakt een **Batch** object en gebruik vervolgens Hallo **uitvoeren\_batch()** methode op **TableService**. Hallo volgende voorbeeld ziet u twee entiteiten met RowKey 2 en 3 in een batch te verzenden. U ziet dat deze alleen werkt voor entiteiten met dezelfde PartitionKey Hallo.

```ruby
azure_table_service = Azure::TableService.new
batch = Azure::Storage::Table::Batch.new("testtable",
    "test-partition-key") do
    insert "2", { "content" => "new content 2" }
    insert "3", { "content" => "new content 3" }
end
results = azure_table_service.execute_batch(batch)
```

## <a name="query-for-an-entity"></a>Query voor een entiteit
een entiteit in een tabel, gebruik Hallo tooquery **ophalen\_entity()** methode door Hallo tabelnaam **PartitionKey** en **RowKey**.

```ruby
result = azure_table_service.get_entity("testtable", "test-partition-key",
    "1")
```

## <a name="query-a-set-of-entities"></a>Query uitvoeren op een verzameling entiteiten
tooquery een set van entiteiten in een tabel, een query-hash-object maken en gebruiken van Hallo **query\_entities()** methode. Hallo volgende voorbeeld ziet u alle Hallo entiteiten Hello aan dezelfde **PartitionKey**:

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'" }
result, token = azure_table_service.query_entities("testtable", query)
```

> [!NOTE]
> Als de resultaatset Hallo is te groot voor een enkele query tooreturn, een vervolgtoken geretourneerd waarin u kunt de volgende pagina's tooretrieve.
>
>

## <a name="query-a-subset-of-entity-properties"></a>Een query uitvoeren op een subset van entiteitseigenschappen
Een query tooa tabel ophalen slechts enkele eigenschappen van een entiteit. Deze techniek, 'projectie' genoemd, verbruikt minder bandbreedte en kan de queryprestaties verbeteren, vooral bij grote entiteiten. Gebruik Hallo select-component en pass Hallo namen van Hallo eigenschappen die u wilt toobring via toohello client.

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'",
    :select => ["content"] }
result, token = azure_table_service.query_entities("testtable", query)
```

## <a name="delete-an-entity"></a>Een entiteit verwijderen
een entiteit toodelete gebruiken Hallo **verwijderen\_entity()** methode. U moet toopass in Hallo-naam van tabel Hallo Hallo entiteit, Hallo PartitionKey en RowKey van Hallo entiteit bevat.

```ruby
azure_table_service.delete_entity("testtable", "test-partition-key", "1")
```

## <a name="delete-a-table"></a>Een tabel verwijderen
een tabel toodelete gebruiken Hallo **verwijderen\_table()** methode en geeft u de naam Hallo van Hallo gewenste toodelete tabel.

```ruby
azure_table_service.delete_table("testtable")
```

## <a name="next-steps"></a>Volgende stappen

* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is een gratis, zelfstandige app van Microsoft waarmee u toowork visueel met Azure Storage-gegevens op Windows-, Mac OS- en Linux.
* [Azure SDK voor Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) opslagplaats op GitHub

