---
title: aaaHow toouse Azure Service Bus-wachtrijen met Ruby | Microsoft Docs
description: Meer informatie over hoe toouse Service Bus wachtrijen in Azure. Codevoorbeelden geschreven in Ruby.
services: service-bus-messaging
documentationcenter: ruby
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 0a11eab2-823f-4cc7-842b-fbbe0f953751
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 7270154583f98e3372e82efbb967ea7a5acd1686
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-ruby"></a>Hoe toouse Service Bus wachtrijen met Ruby

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

Deze handleiding wordt beschreven hoe toouse Service Bus-wachtrijen. Hallo-voorbeelden zijn geschreven in Ruby en hello Azure gem gebruiken. Hallo scenario's worden behandeld: **maken van wachtrijen, verzenden en ontvangen berichten**, en **verwijderen van wachtrijen**. Zie voor meer informatie over Service Bus-wachtrijen Hallo [Vervolgstappen](#next-steps) sectie.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]
   
[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="how-toocreate-a-queue"></a>Hoe een wachtrij toocreate
Hallo **Azure::ServiceBusService** object kunt u toowork met wachtrijen. toocreate een wachtrij gebruiken Hallo `create_queue()` methode. Hallo volgende voorbeeld maakt u een wachtrij of eventuele fouten wordt afgedrukt.

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  queue = azure_service_bus_service.create_queue("test-queue")
rescue
  puts $!
end
```

U kunt ook doorgeven een **Azure::ServiceBus::Queue** object met extra opties waarmee u toooverride Hallo standaard wachtrij-instellingen, zoals bericht tijd toolive of Maximale wachtrijgrootte. Hallo volgende voorbeeld ziet u hoe tooset Hallo wachtrij maximale grootte too5 GB en toolive too1 minuut tijd:

```ruby
queue = Azure::ServiceBus::Queue.new("test-queue")
queue.max_size_in_megabytes = 5120
queue.default_message_time_to_live = "PT1M"

queue = azure_service_bus_service.create_queue(queue)
```

## <a name="how-toosend-messages-tooa-queue"></a>Hoe toosend tooa wachtrij berichten
een bericht tooa Service Bus-wachtrij toosend, roept uw toepassing hello `send_queue_message()` methode op Hallo **Azure::ServiceBusService** object. Berichten verzonden te (en ontvangen van) Service Bus-wachtrijen zijn **Azure::ServiceBus::BrokeredMessage** objecten en hebben een aantal standaardeigenschappen (zoals `label` en `time_to_live`), een woordenlijst die wordt gebruikt toohold aangepaste toepassingsspecifieke eigenschappen en een hoofdtekst met willekeurige toepassingsgegevens. Een toepassing hello hoofdtekst van het Hallo-bericht met het doorgeven van een string-waarde als het Hallo-bericht kan worden ingesteld en eventueel vereiste eigenschappen standaard worden ingevuld met standaardwaarden.

Hallo volgende voorbeeld laat zien hoe toosend een test toohello berichtenwachtrij genoemd `test-queue` met `send_queue_message()`:

```ruby
message = Azure::ServiceBus::BrokeredMessage.new("test queue message")
message.correlation_id = "test-correlation-id"
azure_service_bus_service.send_queue_message("test-queue", message)
```

Service Bus-wachtrijen ondersteunen een maximale berichtgrootte van 256 KB in Hallo [standaardcategorie](service-bus-premium-messaging.md) en 1 MB in Hallo [Premium-laag](service-bus-premium-messaging.md). Hallo-kop, die standaard Hallo- en aangepaste toepassingseigenschappen bevat, kan een maximale grootte van 64 KB hebben. Er is geen limiet voor het aantal berichten in een wachtrij hello, maar er is een limiet voor de totale grootte van berichten in een wachtrij Hallo Hallo. De grootte van de wachtrij wordt gedefinieerd tijdens het aanmaken, met een bovengrens van 5 GB.

## <a name="how-tooreceive-messages-from-a-queue"></a>Hoe tooreceive berichten uit een wachtrij
Berichten worden ontvangen van een wachtrij met Hallo `receive_queue_message()` methode op Hallo **Azure::ServiceBusService** object. Standaard worden berichten lezen en zonder wordt verwijderd uit de wachtrij Hallo vergrendeld. Echter u kunt berichten verwijderen uit de wachtrij Hallo als ze worden gelezen door de instelling Hallo `:peek_lock` te optie**false**.

Hallo standaardgedrag maakt Hallo lezen en verwijderen van een bewerking met twee fasen, waardoor dit ook mogelijk toosupport toepassingen die geen ontbrekende berichten kunnen tolereren. Wanneer Service Bus een aanvraag ontvangt, zoeken naar het volgende bericht toobe Hallo verbruikt, wordt vergrendeld tooprevent andere consumenten het ontvangen en retourneert vervolgens toohello toepassing. Nadat de toepassing hello klaar is met verwerking van het Hallo-bericht (of veilig heeft opgeslagen voor toekomstige verwerking), is de tweede fase Hallo Hallo voltooid proces ontvangen door het aanroepen van `delete_queue_message()` methode en het Hallo-bericht toobe verwijderd als een parameter geven. Hallo `delete_queue_message()` methode wordt het Hallo-bericht als verbruikt markeren en verwijderen uit de wachtrij Hallo.

Als hello `:peek_lock` parameter is ingesteld, te**false**, lezen en verwijderen van het Hallo-bericht, wordt het Hallo eenvoudigste model en werkt het beste voor scenario's waarin een toepassing kan tolereren niet verwerken van een bericht in de gebeurtenis Hallo van een is mislukt. toounderstand dit, Neem bijvoorbeeld een scenario in welke problemen van de consument Hallo Hallo aanvraag ontvangen en vervolgens vastloopt voordat het wordt verwerkt. Omdat Service Bus is gemarkeerd als verbruikt, wanneer Hallo toepassing opnieuw wordt opgestart en verbruik van berichten opnieuw begint het Hallo-bericht, ontbreekt het Hallo-bericht dat was voorafgaande toohello crash verbruikt.

Hallo volgende voorbeeld laat zien hoe tooreceive en proces berichten met behulp van `receive_queue_message()`. Hallo voorbeeld eerst ontvangt en verwijdert van een bericht met behulp van `:peek_lock` instellen te**false**, een ander bericht wordt ontvangen en vervolgens verwijdert het bericht met Hallo `delete_queue_message()`:

```ruby
message = azure_service_bus_service.receive_queue_message("test-queue",
  { :peek_lock => false })
message = azure_service_bus_service.receive_queue_message("test-queue")
azure_service_bus_service.delete_queue_message(message)
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Hoe toohandle toepassing is vastgelopen en onleesbare berichten
Service Bus biedt functionaliteit toohelp die u netjes te herstellen bij fouten in uw toepassing of problemen bij het verwerken van een bericht. Als een ontvangende toepassing niet kan tooprocess hello bericht voor een bepaalde reden en vervolgens kan worden aangeroepen Hallo `unlock_queue_message()` methode op Hallo **Azure::ServiceBusService** object. Deze aanroep tot gevolg dat Service Bus toounlock Hallo in wachtrij Hallo-bericht, waardoor het beschikbaar toobe ontvangen, Hallo ofwel door dezelfde toepassing of door een andere consumerende toepassing verbruikt.

Daarnaast is er een time-out gekoppeld aan een bericht in de wachtrij Hallo is vergrendeld en als de toepassing hello tooprocess Hallo-bericht voordat mislukt Hallo vergrendelingstime-out verloopt (bijvoorbeeld als Hallo toepassing vastloopt), en vervolgens de Service Bus Hiermee ontgrendelt u het Hallo-bericht automatisch en wordt het beschikbaar toobe opnieuw ontvangen.

In Hallo gebeurtenis die toepassing hello vastgelopen na het verwerken van het Hallo-bericht, maar voordat u Hallo `delete_queue_message()` methode wordt aangeroepen en vervolgens het Hallo-bericht is opnieuw bezorgd toohello toepassing opnieuw wordt gestart. Dit proces wordt vaak genoemd *tenminste eenmaal verwerken*; dat wil zeggen dat elk bericht ten minste één keer wordt verwerkt maar in bepaalde situaties Hallo hetzelfde bericht opnieuw kan worden bezorgd. Als Hallo scenario kan geen dubbele verwerking tolereren, moeten toepassingsontwikkelaars levering van aanvullende logica tootheir toepassing toohandle dubbele berichten toevoegen. Dit wordt vaak bereikt met behulp van Hallo `message_id` eigenschap van het Hallo-bericht dat gelijk blijft bij meerdere bezorgingspogingen.

## <a name="next-steps"></a>Volgende stappen
Nu u Hallo basisprincipes van Service Bus-wachtrijen hebt geleerd, volgt u deze koppelingen toolearn meer.

* Overzicht van [wachtrijen, onderwerpen en abonnementen](service-bus-queues-topics-subscriptions.md).
* Ga naar Hallo [Azure SDK voor Ruby](https://github.com/Azure/azure-sdk-for-ruby) opslagplaats op GitHub.

Voor een vergelijking tussen hello Azure Service Bus-wachtrijen in dit artikel besproken en wachtrijen van Azure die wordt besproken in Hallo [hoe toouse Queue storage met Ruby](../storage/queues/storage-ruby-how-to-use-queue-storage.md) artikel, Zie [Azure wachtrijen en Azure Service Bus-wachtrijen - vergeleken en in tegenstelling tot](service-bus-azure-and-service-bus-queues-compared-contrasted.md)

