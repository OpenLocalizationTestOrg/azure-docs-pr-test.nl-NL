---
title: Service Bus-onderwerpen voor aaaHow toouse (Ruby) | Microsoft Docs
description: Meer informatie over hoe toouse Service Bus-onderwerpen en abonnementen in Azure. Codevoorbeelden zijn geschreven voor Ruby-toepassingen.
services: service-bus-messaging
documentationcenter: ruby
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3ef2295e-7c5f-4c54-a13b-a69c8045d4b6
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 236d6495825e68e336c23e1b500d0764ee512e49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-ruby"></a>Hoe toouse Service Bus-onderwerpen en abonnementen, met Ruby
 
[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

Dit artikel wordt beschreven hoe toouse Service Bus-onderwerpen en abonnementen van Ruby toepassingen. Hallo scenario's worden behandeld: **maken van onderwerpen en abonnementen, het maken van abonnementsfilters, het verzenden van berichten** tooa onderwerp **ontvangen van berichten van een abonnement**, en  **verwijderen van onderwerpen en abonnementen**. Zie voor meer informatie over onderwerpen en abonnementen Hallo [Vervolgstappen](#next-steps) sectie.

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="create-a-topic"></a>Een onderwerp maken
Hallo **Azure::ServiceBusService** object kunt u toowork met onderwerpen. Hallo volgende code maakt een **Azure::ServiceBusService** object. een onderwerp toocreate gebruiken Hallo `create_topic()` methode. Hallo volgende voorbeeld maakt een onderwerp of wordt afgedrukt Hallo fouten als er een.

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  topic = azure_service_bus_service.create_queue("test-topic")
rescue
  puts $!
end
```

U kunt ook doorgeven een **Azure::ServiceBus::Topic** object met extra opties waarmee u toooverride standaardinstellingen onderwerp zoals bericht tijd toolive of Maximale wachtrijgrootte. Hallo volgende voorbeeld wordt getoond als de maximale wachtrij Hallo instelt omvang too5 GB en toolive too1 minuut tijd:

```ruby
topic = Azure::ServiceBus::Topic.new("test-topic")
topic.max_size_in_megabytes = 5120
topic.default_message_time_to_live = "PT1M"

topic = azure_service_bus_service.create_topic(topic)
```

## <a name="create-subscriptions"></a>Abonnementen maken
Onderwerpabonnementen worden ook gemaakt met de Hallo **Azure::ServiceBusService** object. Abonnementen kunnen worden genoemd en een optioneel filter waarmee Hallo verzameling berichten dat de virtuele wachtrij van het abonnement toohello wordt beperkt.

Abonnementen worden permanent en tooexist zal worden voortgezet totdat beide ze of hello onderwerp ze zijn gekoppeld, worden verwijderd. Als uw toepassing bevat de logica toocreate een abonnement, moet eerst controleren als Hallo abonnement bestaat al met Hallo getSubscription methode.

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Een abonnement maken met de Hallo standaardfilter (MatchAll)
Hallo **MatchAll** filter is Hallo standaardfilter dat wordt gebruikt als geen filter is opgegeven als een nieuw abonnement wordt gemaakt. Wanneer Hallo **MatchAll** filter wordt gebruikt, worden alle berichten gepubliceerde toohello onderwerp in virtuele wachtrij van Hallo abonnement geplaatst. Hallo volgende voorbeeld wordt een abonnement genaamd 'all '-berichten en gebruikt standaard Hallo **MatchAll** filter.

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "all-messages")
```

### <a name="create-subscriptions-with-filters"></a>Abonnementen met filters maken
U kunt ook filters waarmee u welke berichten verzonden tooa onderwerp weergegeven binnen een bepaald abonnement toospecify definiëren.

Hallo meest flexibele type filter dat wordt ondersteund door abonnementen is Hallo **Azure::ServiceBus::SqlFilter**, waarmee een subset van SQL92 wordt geïmplementeerd implementeert. SQL-filters worden uitgevoerd op Hallo eigenschappen van Hallo-berichten die gepubliceerd toohello onderwerp zijn. Bekijk voor meer informatie over Hallo expressies die kunnen worden gebruikt met een SQL-filter Hallo [SqlFilter](service-bus-messaging-sql-filter.md) syntaxis.

U kunt filters tooa abonnement kunt toevoegen met behulp van Hallo `create_rule()` methode Hallo **Azure::ServiceBusService** object. Deze methode kunt u tooadd nieuwe filters tooan bestaande abonnement.

Aangezien het standaardfilter hello wordt automatisch toegepast tooall nieuwe abonnementen, moet u eerst het standaardfilter Hallo verwijderen, of Hallo **MatchAll** overschrijft alle andere filters die u kunt opgeven. U kunt de standaardregel Hallo verwijderen via Hallo `delete_rule()` methode op Hallo **Azure::ServiceBusService** object.

Hallo volgende voorbeeld maakt u een abonnement met de naam 'hoog '-berichten met een **Azure::ServiceBus::SqlFilter** die alleen berichten selecteert die een aangepaste `message_number` eigenschap groter is dan 3:

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "high-messages")
azure_service_bus_service.delete_rule("test-topic", "high-messages", "$Default")

rule = Azure::ServiceBus::Rule.new("high-messages-rule")
rule.topic = "test-topic"
rule.subscription = "high-messages"
rule.filter = Azure::ServiceBus::SqlFilter.new({
  :sql_expression => "message_number > 3" })
rule = azure_service_bus_service.create_rule(rule)
```

Op deze manier hello volgende voorbeeld maakt u een abonnement met de naam `low-messages` met een **Azure::ServiceBus::SqlFilter** die alleen berichten selecteert die een `message_number` eigenschap kleiner dan of gelijk too3:

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "low-messages")
azure_service_bus_service.delete_rule("test-topic", "low-messages", "$Default")

rule = Azure::ServiceBus::Rule.new("low-messages-rule")
rule.topic = "test-topic"
rule.subscription = "low-messages"
rule.filter = Azure::ServiceBus::SqlFilter.new({
  :sql_expression => "message_number <= 3" })
rule = azure_service_bus_service.create_rule(rule)
```

Wanneer een bericht nu te verzonden`test-topic`, kan altijd worden geleverd tooreceivers geabonneerd toohello `all-messages` onderwerpabonnement en selectief bezorgd tooreceivers geabonneerd toohello `high-messages` en `low-messages` onderwerp abonnementen ( afhankelijk van de inhoud van de Hallo-bericht).

## <a name="send-messages-tooa-topic"></a>Verzenden van berichten tooa onderwerp
een bericht tooa Service Bus-onderwerp toosend, uw toepassing moet gebruiken Hallo `send_topic_message()` methode op Hallo **Azure::ServiceBusService** object. Berichten verzonden tooService Bus-onderwerpen, zijn exemplaren van Hallo **Azure::ServiceBus::BrokeredMessage** objecten. **Azure::ServiceBus::BrokeredMessage** objecten hebben een aantal standaardeigenschappen (zoals `label` en `time_to_live`), een woordenlijst die wordt gebruikt toohold aangepaste toepassingsspecifieke eigenschappen en een hoofdtekst met tekenreeksen. Een toepassing hello hoofdtekst van het Hallo-bericht worden ingesteld door een string-waarde toohello `send_topic_message()` methode en alle vereiste standaardeigenschappen standaardwaarden worden ingevuld.

Hallo volgende voorbeeld toont hoe vijf toosend test berichten te`test-topic`. Houd er rekening mee dat Hallo `message_number` waarde van de aangepaste eigenschap van elk bericht varieert op Hallo herhaling van Hallo lus (deze bepaalt welke abonnement ontvangt):

```ruby
5.times do |i|
  message = Azure::ServiceBus::BrokeredMessage.new("test message " + i,
    { :message_number => i })
  azure_service_bus_service.send_topic_message("test-topic", message)
end
```

Service Bus-onderwerpen ondersteunen een maximale berichtgrootte van 256 KB in Hallo [standaardcategorie](service-bus-premium-messaging.md) en 1 MB in Hallo [Premium-laag](service-bus-premium-messaging.md). Hallo-kop, die standaard Hallo- en aangepaste toepassingseigenschappen bevat, kan een maximale grootte van 64 KB hebben. Er is geen limiet voor het aantal berichten in een onderwerp hello, maar er is een limiet voor de totale grootte van berichten in een onderwerp Hallo Hallo. De grootte van het onderwerp wordt gedefinieerd tijdens het maken, met een bovengrens van 5 GB.

## <a name="receive-messages-from-a-subscription"></a>Berichten ontvangen van een abonnement
Berichten worden ontvangen van een abonnement met Hallo `receive_subscription_message()` methode op Hallo **Azure::ServiceBusService** object. Standaard berichten zijn read(peak) en zonder het te verwijderen uit het Hallo-abonnement is vergrendeld. U kunt lezen en het Hallo-bericht verwijderen uit abonnement Hallo door Hallo instelling `peek_lock` te optie**false**.

Hallo standaardgedrag maakt Hallo lezen en verwijderen van een bewerking met twee fasen, waardoor dit ook mogelijk toosupport toepassingen die geen ontbrekende berichten kunnen tolereren. Wanneer Service Bus een aanvraag ontvangt, zoeken naar het volgende bericht toobe Hallo verbruikt, wordt vergrendeld tooprevent andere consumenten het ontvangen en retourneert vervolgens toohello toepassing. Nadat de toepassing hello klaar is met verwerking van het Hallo-bericht (of veilig heeft opgeslagen voor toekomstige verwerking), is de tweede fase Hallo Hallo voltooid proces ontvangen door het aanroepen van `delete_subscription_message()` methode en het Hallo-bericht toobe verwijderd als een parameter geven. Hallo `delete_subscription_message()` methode wordt het Hallo-bericht als verbruikt markeren en verwijderen uit het Hallo-abonnement.

Als hello `:peek_lock` parameter is ingesteld, te**false**, lezen en verwijderen van het Hallo-bericht, wordt het Hallo eenvoudigste model en werkt het beste voor scenario's waarin een toepassing kan tolereren niet verwerken van een bericht in de gebeurtenis Hallo van een is mislukt. toounderstand dit, Neem bijvoorbeeld een scenario in welke problemen van de consument Hallo Hallo aanvraag ontvangen en vervolgens vastloopt voordat het wordt verwerkt. Omdat Service Bus heeft gemarkeerd als verbruikt, vervolgens wanneer Hallo toepassing opnieuw wordt opgestart en verbruik van berichten opnieuw begint het Hallo-bericht, ontbreekt het Hallo-bericht dat was voorafgaande toohello crash verbruikt.

Hallo volgende voorbeeld laat zien hoe berichten kunnen worden ontvangen en verwerkt met behulp `receive_subscription_message()`. Hallo voorbeeld eerst ontvangt en verwijdert van een bericht van Hallo `low-messages` abonnement via `:peek_lock` instellen te**false**, en vervolgens wordt een ander bericht van Hallo ontvangen `high-messages` en vervolgens verwijdert het bericht met Hallo `delete_subscription_message()`:

```ruby
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "low-messages", { :peek_lock => false })
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "high-messages")
azure_service_bus_service.delete_subscription_message(message)
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Hoe toohandle toepassing is vastgelopen en onleesbare berichten
Service Bus biedt functionaliteit toohelp die u netjes te herstellen bij fouten in uw toepassing of problemen bij het verwerken van een bericht. Als een ontvangende toepassing niet kan tooprocess hello bericht voor een bepaalde reden en vervolgens kan worden aangeroepen Hallo `unlock_subscription_message()` methode op Hallo **Azure::ServiceBusService** object. Deze tot gevolg dat het Service Bus toounlock Hallo binnen abonnement Hallo-bericht, waardoor het beschikbaar toobe ontvangen, Hallo ofwel door dezelfde toepassing of door een andere consumerende toepassing verbruikt.

Daarnaast is er een time-out gekoppeld aan een bericht in het Hallo-abonnement is vergrendeld en als Hallo toepassing tooprocess Hallo-bericht voordat mislukt Hallo vergrendelingstime-out verloopt (bijvoorbeeld als Hallo toepassing vastloopt), en vervolgens de Service Bus wordt ontgrendeld Hallo-bericht automatisch en wordt het beschikbaar toobe opnieuw ontvangen.

In Hallo gebeurtenis die toepassing hello vastgelopen na het verwerken van het Hallo-bericht, maar voordat u Hallo `delete_subscription_message()` methode wordt aangeroepen en vervolgens het Hallo-bericht is opnieuw bezorgd toohello toepassing opnieuw wordt gestart. Dit wordt vaak genoemd *tenminste eenmaal verwerken*; dat wil zeggen, elk bericht ten minste één keer wordt verwerkt maar in bepaalde situaties Hallo hetzelfde bericht opnieuw kan worden bezorgd. Als Hallo scenario kan geen dubbele verwerking tolereren, moeten toepassingsontwikkelaars levering van aanvullende logica tootheir toepassing toohandle dubbele berichten toevoegen. Deze logica wordt vaak bereikt met behulp van Hallo `message_id` eigenschap van Hallo-bericht dat gelijk bij meerdere bezorgingspogingen blijft.

## <a name="delete-topics-and-subscriptions"></a>Onderwerpen en abonnementen verwijderen
Onderwerpen en abonnementen worden permanent en expliciet moet worden verwijderd via Hallo [Azure-portal] [ Azure portal] of via een programma. Hallo in het volgende voorbeeld laat zien hoe toodelete Hallo onderwerp met de naam `test-topic`.

```ruby
azure_service_bus_service.delete_topic("test-topic")
```

Als u een onderwerp verwijdert, verwijdert tevens abonnementen die zijn geregistreerd bij Hallo onderwerp. Abonnementen kunnen ook afzonderlijk worden verwijderd. Hallo volgende code laat zien hoe toodelete Hallo abonnement met de naam `high-messages` van Hallo `test-topic` onderwerp:

```ruby
azure_service_bus_service.delete_subscription("test-topic", "high-messages")
```

## <a name="next-steps"></a>Volgende stappen
Nu u de basisprincipes van Service Bus-onderwerpen Hallo hebt geleerd, volgt u deze koppelingen toolearn meer.

* Zie [wachtrijen, onderwerpen en abonnementen](service-bus-queues-topics-subscriptions.md).
* API-naslaginformatie voor [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter).
* Ga naar Hallo [Azure SDK voor Ruby](https://github.com/Azure/azure-sdk-for-ruby) opslagplaats op GitHub.

[Azure portal]: https://portal.azure.com
