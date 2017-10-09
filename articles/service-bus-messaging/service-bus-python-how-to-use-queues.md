---
title: aaaHow toouse Azure Service Bus-wachtrijen met behulp van Python | Microsoft Docs
description: Meer informatie over hoe Azure Service Bus toouse wachtrijen met Python.
services: service-bus-messaging
documentationcenter: python
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b95ee5cd-3b31-459c-a7f3-cf8bcf77858b
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm;lmazuel
ms.openlocfilehash: bceb84d04ff3445c3087a9c246c583d6630f07af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-python"></a>Hoe toouse Service Bus wachtrijen met behulp van Python

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

Dit artikel wordt beschreven hoe toouse Service Bus-wachtrijen. Hallo-voorbeelden zijn geschreven in Python en gebruiken van Hallo [Python Azure Service Bus-pakket][Python Azure Service Bus package]. Hallo scenario's worden behandeld: **maken van wachtrijen, verzenden en ontvangen berichten**, en **verwijderen van wachtrijen**.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

> [!NOTE]
> tooinstall Python of Hallo [Python Azure Service Bus-pakket][Python Azure Service Bus package], Zie Hallo [Python installatiehandleiding](../python-how-to-install.md).
> 
> 

## <a name="create-a-queue"></a>Een wachtrij maken
Hallo **ServiceBusService** object kunt u toowork met wachtrijen. Hallo volgende code bij Hallo bovenkant van een Python-bestand waarin u tooprogrammatically access Service Bus wilt toevoegen:

```python
from azure.servicebus import ServiceBusService, Message, Queue
```

Hallo volgende code maakt een **ServiceBusService** object. Vervang `mynamespace`, `sharedaccesskeyname`, en `sharedaccesskey` met uw naamruimte, naam van shared access signature (SAS)-sleutel en waarde.

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

Hallo waarden voor Hallo SAS-sleutelnaam en -waarde kunnen worden gevonden in Hallo [Azure-portal] [ Azure portal] verbindingsinformatie, of in Visual Studio Hallo **eigenschappen** deelvenster bij het selecteren van Hallo Service Bus-naamruimte in Server Explorer (zoals weergegeven in de vorige sectie Hallo).

```python
bus_service.create_queue('taskqueue')
```

Hallo `create_queue` methode biedt ook ondersteuning voor extra opties waarmee u toooverride standaard wachtrij-instellingen zoals bericht toolive TTL (time) of de maximale wachtrijgrootte. Hallo volgende voorbeeld wordt Hallo wachtrij maximale grootte too5 GB en Hallo TTL-waarde too1 minuut:

```python
queue_options = Queue()
queue_options.max_size_in_megabytes = '5120'
queue_options.default_message_time_to_live = 'PT1M'

bus_service.create_queue('taskqueue', queue_options)
```

## <a name="send-messages-tooa-queue"></a>Berichten tooa wachtrij verzenden
een bericht tooa Service Bus-wachtrij toosend, roept uw toepassing hello `send_queue_message` methode op Hallo **ServiceBusService** object.

Hallo volgende voorbeeld laat zien hoe toosend een test toohello berichtenwachtrij genoemd `taskqueue` met `send_queue_message`:

```python
msg = Message(b'Test Message')
bus_service.send_queue_message('taskqueue', msg)
```

Service Bus-wachtrijen ondersteunen een maximale berichtgrootte van 256 KB in Hallo [standaardcategorie](service-bus-premium-messaging.md) en 1 MB in Hallo [Premium-laag](service-bus-premium-messaging.md). Hallo-kop, die standaard Hallo- en aangepaste toepassingseigenschappen bevat, kan een maximale grootte van 64 KB hebben. Er is geen limiet voor het aantal berichten in een wachtrij hello, maar er is een limiet voor de totale grootte van berichten in een wachtrij Hallo Hallo. De grootte van de wachtrij wordt gedefinieerd tijdens het aanmaken, met een bovengrens van 5 GB. Zie voor meer informatie over quota [Service Bus-quota][Service Bus quotas].

## <a name="receive-messages-from-a-queue"></a>Berichten ontvangen uit een wachtrij
Berichten worden ontvangen van een wachtrij met Hallo `receive_queue_message` methode op Hallo **ServiceBusService** object:

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=False)
print(msg.body)
```

Berichten worden verwijderd uit de wachtrij Hallo als ze worden gelezen wanneer de parameter Hallo `peek_lock` te is ingesteld**False**. U kunt lezen (peek) en het Hallo-bericht zonder het te verwijderen uit de wachtrij Hallo door instelling Hallo parameter vergrendelen `peek_lock` te**True**.

Hallo gedrag van lezen en Hallo-bericht is verwijderd als onderdeel van Hallo ontvangstbewerking is Hallo eenvoudigste model en werkt het beste voor scenario's waarin een toepassing kan tolereren niet verwerken van een bericht in de gebeurtenis Hallo van een fout. toounderstand dit, Neem bijvoorbeeld een scenario in welke problemen van de consument Hallo Hallo aanvraag ontvangen en vervolgens vastloopt voordat het wordt verwerkt. Omdat Service Bus heeft gemarkeerd als verbruikt, vervolgens wanneer Hallo toepassing opnieuw wordt opgestart en verbruik van berichten opnieuw begint het Hallo-bericht, ontbreekt het Hallo-bericht dat was voorafgaande toohello crash verbruikt.

Als hello `peek_lock` parameter is ingesteld, te**True**, Hallo ontvangen, wordt een bewerking met twee fasen, waardoor het mogelijk toosupport toepassingen die geen ontbrekende berichten kunnen tolereren. Wanneer Service Bus een aanvraag ontvangt, zoeken naar het volgende bericht toobe Hallo verbruikt, wordt vergrendeld tooprevent andere consumenten het ontvangen en retourneert vervolgens toohello toepassing. Nadat de toepassing hello klaar is met verwerking van het Hallo-bericht (of veilig heeft opgeslagen voor toekomstige verwerking), is de tweede fase Hallo Hallo voltooid proces ontvangen door de aanroepende Hallo **verwijderen** methode op Hallo **bericht** object. Hallo **verwijderen** methode wordt het Hallo-bericht als verbruikt markeren en verwijderen uit de wachtrij Hallo.

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Hoe toohandle toepassing is vastgelopen en onleesbare berichten
Service Bus biedt functionaliteit toohelp die u netjes te herstellen bij fouten in uw toepassing of problemen bij het verwerken van een bericht. Als een ontvangende toepassing niet kan tooprocess hello bericht voor een bepaalde reden en vervolgens kan worden aangeroepen Hallo **ontgrendelen** methode op Hallo **bericht** object. Hierdoor wordt ervoor zorgen dat Service Bus toounlock Hallo-bericht in de wachtrij Hallo en beschikbare toobe opnieuw ontvangen, ofwel Hallo door dezelfde toepassing of door een andere consumerende toepassing verbruikt.

Daarnaast is er een time-out gekoppeld aan een bericht in de wachtrij Hallo is vergrendeld en als Hallo toepassing mislukt tooprocess Hallo-bericht voordat Hallo time-out van de vergrendeling verloopt (bijvoorbeeld als Hallo toepassing vastloopt), en vervolgens de Service Bus wordt het Hallo-bericht automatisch ontgrendelen en het beschikbaar toobe ontvangen opnieuw maken.

In Hallo gebeurtenis die toepassing hello vastgelopen na het verwerken van het Hallo-bericht, maar voordat u Hallo **verwijderen** methode wordt aangeroepen, is het Hallo-bericht altijd opnieuw bezorgd toohello toepassing opnieuw wordt gestart. Dit wordt vaak genoemd **tenminste eenmaal verwerken**, dat wil zeggen elk bericht ten minste één keer wordt verwerkt maar in bepaalde situaties Hallo hetzelfde bericht opnieuw kan worden bezorgd. Als Hallo scenario kan geen dubbele verwerking tolereren, moeten toepassingsontwikkelaars levering van aanvullende logica tootheir toepassing toohandle dubbele berichten toevoegen. Dit wordt vaak bereikt met behulp van Hallo **MessageId** eigenschap van Hallo-bericht dat gelijk bij meerdere bezorgingspogingen blijft.

## <a name="next-steps"></a>Volgende stappen
Nu u Hallo basisprincipes van Service Bus-wachtrijen hebt geleerd, gaat u naar deze artikelen toolearn meer.

* [Wachtrijen, onderwerpen en abonnementen][Queues, topics, and subscriptions]

[Azure portal]: https://portal.azure.com
[Python Azure Service Bus package]: https://pypi.python.org/pypi/azure-servicebus  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Service Bus quotas]: service-bus-quotas.md

