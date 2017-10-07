---
title: aaaHow toouse Queue storage met Ruby | Microsoft Docs
description: Ontdek hoe toocreate toouse hello Azure Queue-service en delete-wachtrijen en invoegen, ophalen en verwijderen van berichten. De voorbeelden in Ruby geschreven.
services: storage
documentationcenter: ruby
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 59c2d81b-db9c-46ee-ade2-2f0caae6b1e6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 726c7d2f08b2d5938ee5f9dcdc2735e447388856
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-ruby"></a>Hoe toouse Queue storage met Ruby
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Overzicht
Deze handleiding wordt getoond hoe tooperform algemene scenario's met behulp van Microsoft Azure Queue Storage-service Hallo. Hallo-voorbeelden zijn geschreven met behulp van Hallo Ruby Azure-API.
Hallo scenario's worden behandeld: **invoegen**, **inspecteren**, **ophalen**, en **verwijderen** wachtrij berichten, evenals  **maken en verwijderen van wachtrijen**.

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a>Een Ruby-toepassing maken
Maak een Ruby toepassing. Zie voor instructies [Ruby op Rails webtoepassing op een virtuele machine van Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).

## <a name="configure-your-application-tooaccess-storage"></a>Uw toepassing tooAccess opslag configureren
toouse Azure-opslag, moet u toodownload en gebruik Hallo Ruby azure, dit pakket bevat een set met gemak bibliotheken die met de Hallo storage REST-services communiceren.

### <a name="use-rubygems-tooobtain-hello-package"></a>RubyGems tooobtain Hallo pakket gebruiken
1. Een opdrachtregelinterface gebruiken zoals **PowerShell** (Windows), **Terminal** (Mac) of **Bash** (Unix).
2. Typ 'gem installeren azure' hello opdracht venster tooinstall Hallo gem en afhankelijkheden.

### <a name="import-hello-package"></a>Hallo-pakket importeren
Uw favoriete teksteditor gebruiken, voegt Hallo toohello bovenaan Hallo Ruby bestand waarin u van plan toouse opslag bent te volgen:

```ruby
require "azure"
```

## <a name="setup-an-azure-storage-connection"></a>Een Azure-opslag-verbinding instellen
Hello azure module lezen Hallo omgevingsvariabelen **AZURE\_opslag\_ACCOUNT** en **AZURE\_opslag\_ACCESS_KEY** voor informatie vereist tooconnect tooyour Azure storage-account. Als deze omgevingsvariabelen zijn niet ingesteld, moet u de accountgegevens Hallo voordat u **Azure::QueueService** Hello code te volgen:

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your Azure storage access key>"
```

tooobtain deze waarden van een klassiek of Resource Manager-storage-account in hello Azure-portal:

1. Meld u bij toohello [Azure-portal](https://portal.azure.com).
2. Navigeer toohello gewenste toouse storage-account.
3. Klik op Hallo instellingenblade op Hallo rechts **toegangstoetsen**.
4. Hallo toegang sleutels blade die wordt weergegeven, ziet u Hallo toegangssleutel 1 en toegangssleutel 2. U kunt een van beide gebruiken. 
5. Klik op Hallo kopiëren pictogram toocopy Hallo sleutel toohello Klembord. 

tooobtain deze waarden van een klassieke storage-account in de klassieke Azure portal Hallo:

1. Meld u bij toohello [klassieke Azure portal](https://manage.windowsazure.com).
2. Navigeer toohello gewenste toouse storage-account.
3. Klik op **TOEGANGSSLEUTELS beheren** Hallo Hallo navigatiedeelvenster onderaan in.
4. In het dialoogvenster pop hello ziet u opslagaccountnaam hello, de primaire toegangssleutel en de secundaire toegangssleutel. U kunt voor toegangssleutel, Hallo een primaire of secundaire één Hallo gebruiken. 
5. Klik op Hallo kopiëren pictogram toocopy Hallo sleutel toohello Klembord.

## <a name="how-to-create-a-queue"></a>Procedure: Een wachtrij maken
Hallo volgende code maakt een **Azure::QueueService** object, waarmee u toowork met wachtrijen.

```ruby
azure_queue_service = Azure::QueueService.new
```

Gebruik Hallo **create_queue()** methode toocreate een wachtrij met Hallo opgegeven naam.

```ruby
begin
  azure_queue_service.create_queue("test-queue")
rescue
  puts $!
end
```

## <a name="how-to-insert-a-message-into-a-queue"></a>Procedure: Een bericht in een wachtrij invoegen
een bericht in een wachtrij, gebruik Hallo tooinsert **create_message()** methode toocreate een nieuw bericht en voeg deze toohello wachtrij.

```ruby
azure_queue_service.create_message("test-queue", "test message")
```

## <a name="how-to-peek-at-hello-next-message"></a>Procedure: Inspecteren Hallo het Volgendebericht
U kunt bekijken van Hallo-bericht in Hallo begin van een wachtrij zonder het te verwijderen uit de wachtrij Hallo door aanroepen Hallo **peek\_messages()** methode. Standaard **peek\_messages()** peeks op één bericht. U kunt ook opgeven hoeveel berichten u wilt dat toopeek.

```ruby
result = azure_queue_service.peek_messages("test-queue",
  {:number_of_messages => 10})
```

## <a name="how-to-dequeue-hello-next-message"></a>Procedure: Hallo het Volgendebericht uit de wachtrij halen
U kunt een bericht verwijderen uit een wachtrij in twee stappen.

1. Als u aanroept **lijst\_messages()**, u het volgende Hallo-bericht in een wachtrij standaard ophalen. U kunt ook opgeven hoeveel berichten u wilt dat tooget. Hallo-berichten dat is geretourneerd door **lijst\_messages()** wordt onzichtbaar tooany andere codes die berichten lezen uit deze wachtrij. U doorgeven Hallo zichtbaarheid time-out in seconden als parameter.
2. toofinish verwijderen Hallo-bericht uit de wachtrij hello, moet u ook aanroepen **delete_message()**.

Dit proces in twee stappen van het verwijderen van een bericht zorgt ervoor dat wanneer uw code mislukt tooprocess een bericht vanwege problemen toohardware of software, een ander exemplaar van uw code krijgt Hallo hetzelfde bericht en probeer het opnieuw. Uw code haalt **verwijderen\_message()** direct nadat het Hallo-bericht is verwerkt.

```ruby
messages = azure_queue_service.list_messages("test-queue", 30)
azure_queue_service.delete_message("test-queue", 
  messages[0].id, messages[0].pop_receipt)
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>Procedure: Hallo inhoud van een bericht in de wachtrij wijzigen
U kunt Hallo inhoud van een bericht in-place in Hallo wachtrij wijzigen. Hallo-code hieronder maakt gebruik van Hallo **update_message()** methode tooupdate een bericht. Hallo-methode retourneert een tuple die Hallo pop ontvangst van de wachtrij het Hallo-bericht bevat en een UTC date tijd-waarde die aangeeft wanneer het Hallo-bericht op Hallo wachtrij zichtbaar zijn.

```ruby
message = azure_queue_service.list_messages("test-queue", 30)
pop_receipt, time_next_visible = azure_queue_service.update_message(
  "test-queue", message.id, message.pop_receipt, "updated test message", 
  30)
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a>Procedure: Aanvullende opties voor waarbij berichten
Er zijn twee manieren waarop u het ophalen van berichten uit een wachtrij kunt aanpassen.

1. U kunt een batch van bericht ophalen.
2. U kunt een time-out langer of korter onzichtbaarheid instellen zodat uw code meer of minder tijd toofully elk bericht niet verwerken.

Hallo volgende codevoorbeeld maakt gebruik van Hallo **lijst\_messages()** methode tooget 15 berichten in één aanroep. Vervolgens wordt afgedrukt en elk bericht wordt verwijderd. Hallo onzichtbaarheid toofive minuten voor de time-out voor elk bericht wordt ook ingesteld.

```ruby
azure_queue_service.list_messages("test-queue", 300
  {:number_of_messages => 15}).each do |m|
  puts m.message_text
  azure_queue_service.delete_message("test-queue", m.id, m.pop_receipt)
end
```

## <a name="how-to-get-hello-queue-length"></a>Procedure: Hallo wachtrijlengte ophalen
U kunt een schatting van het aantal berichten Hallo ophalen in de wachtrij Hallo. Hallo **ophalen\_wachtrij\_metadata()** methode vraagt Hallo wachtrij tooreturn Hallo bericht geschatte aantal en metagegevens over Hallo wachtrij.

```ruby
message_count, metadata = azure_queue_service.get_queue_metadata(
  "test-queue")
```

## <a name="how-to-delete-a-queue"></a>Procedure: Een wachtrij verwijderen
een wachtrij en alle Hallo-berichten toodelete opgenomen in deze aanroep Hallo **verwijderen\_queue()** methode op Hallo wachtrij-object.

```ruby
azure_queue_service.delete_queue("test-queue")
```

## <a name="next-steps"></a>Volgende stappen
Nu u Hallo basisprincipes van queue storage hebt geleerd, volgt u deze koppelingen toolearn over complexere opslagtaken.

* Ga naar Hallo [Blog van Azure Storage-Team](http://blogs.msdn.com/b/windowsazurestorage/)
* Ga naar Hallo [Azure SDK voor Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) opslagplaats op GitHub

Voor een vergelijking tussen hello Azure Queue-Service die wordt besproken in dit artikel en de Azure Service Bus-wachtrijen in Hallo besproken [hoe toouse Service Bus-wachtrijen](/develop/ruby/how-to-guides/service-bus-queues/) artikel, Zie [Azure wachtrijen en Service Bus-wachtrijen - vergeleken en Tegenstelling tot](../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)
