---
title: aaaHow toouse Azure Service Bus-onderwerpen met behulp van Python | Microsoft Docs
description: Meer informatie over hoe toouse Azure Service Bus-onderwerpen en abonnementen van Python.
services: service-bus-messaging
documentationcenter: python
author: sethmanheim
manager: timlt
editor: 
ms.assetid: c4f1d76c-7567-4b33-9193-3788f82934e4
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 1171cbe8061bb3d73e2ce92ecc0cf45afae37054
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-python"></a>Hoe toouse Service Bus-onderwerpen en abonnementen, met Python

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

Dit artikel wordt beschreven hoe toouse Service Bus-onderwerpen en abonnementen. Hallo-voorbeelden zijn geschreven in Python en gebruiken van Hallo [Azure Python SDK-pakket][Azure Python package]. Hallo scenario's worden behandeld: **maken van onderwerpen en abonnementen**, **maken van abonnementsfilters**, **verzenden van berichten tooa onderwerp**, **ontvangen berichten van een abonnement**, en **verwijderen van onderwerpen en abonnementen**. Zie voor meer informatie over onderwerpen en abonnementen Hallo [Vervolgstappen](#next-steps) sectie.

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

> [!NOTE] 
> Als u tooinstall Python of Hallo nodig [Azure Python-pakket][Azure Python package], Zie Hallo [Python installatiehandleiding](../python-how-to-install.md).

## <a name="create-a-topic"></a>Een onderwerp maken
Hallo **ServiceBusService** object kunt u toowork met onderwerpen. Voeg de volgende Hallo bij Hallo bovenkant van een Python-bestand waarin u wenst dat tooprogrammatically access Service Bus:

```python
from azure.servicebus import ServiceBusService, Message, Topic, Rule, DEFAULT_RULE_NAME
```

Hallo volgende code maakt een **ServiceBusService** object. Vervang `mynamespace`, `sharedaccesskeyname`, en `sharedaccesskey` met uw werkelijke naamruimte Shared Access Signature (SAS) sleutelwaarde naam en een sleutel.

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

U kunt ophalen Hallo waarden voor Hallo SAS-sleutelnaam en de waarde Hallo [Azure-portal][Azure portal].

```python
bus_service.create_topic('mytopic')
```

Hallo `create_topic` methode biedt ook ondersteuning voor extra opties waarmee u toooverride standaardinstellingen onderwerp zoals bericht tijd onderwerp toolive of de maximale grootte. Hallo volgende voorbeeld wordt Hallo onderwerp maximale grootte too5 GB en een tijd toolive (TTL)-waarde van 1 minuut:

```python
topic_options = Topic()
topic_options.max_size_in_megabytes = '5120'
topic_options.default_message_time_to_live = 'PT1M'

bus_service.create_topic('mytopic', topic_options)
```

## <a name="create-subscriptions"></a>Abonnementen maken
Abonnementen tootopics tevens zijn gemaakt met de Hallo **ServiceBusService** object. Abonnementen kunnen worden genoemd en een optioneel filter waarmee Hallo verzameling berichten dat de virtuele wachtrij van het abonnement toohello wordt beperkt.

> [!NOTE]
> Abonnementen worden permanent en tooexist zal worden voortgezet totdat beide ze of hello onderwerp toowhich ze bent geabonneerd, worden verwijderd.
> 
> 

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Een abonnement maken met de Hallo standaardfilter (MatchAll)
Hallo **MatchAll** filter is Hallo standaardfilter dat wordt gebruikt als geen filter is opgegeven als een nieuw abonnement wordt gemaakt. Wanneer Hallo **MatchAll** filter wordt gebruikt, worden alle berichten gepubliceerde toohello onderwerp in virtuele wachtrij van Hallo abonnement geplaatst. Hallo volgende voorbeeld maakt u een abonnement met de naam `AllMessages` en gebruikt standaard Hallo **MatchAll** filter.

```python
bus_service.create_subscription('mytopic', 'AllMessages')
```

### <a name="create-subscriptions-with-filters"></a>Abonnementen met filters maken
U kunt ook filters waarmee u welke berichten verzonden tooa onderwerp weergegeven binnen een bepaald onderwerpabonnement toospecify definiëren.

Hallo meest flexibele type filter dat wordt ondersteund door abonnementen is een **SqlFilter**, waarmee een subset van SQL92 wordt geïmplementeerd implementeert. SQL-filters worden uitgevoerd op Hallo eigenschappen van Hallo-berichten die gepubliceerd toohello onderwerp zijn. Zie voor meer informatie over Hallo expressies die kunnen worden gebruikt met een SQL-filter Hallo [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] syntaxis.

U kunt filters tooa abonnement kunt toevoegen met behulp van Hallo **maken\_regel** methode Hallo **ServiceBusService** object. Deze methode kunt u tooadd nieuwe filters tooan bestaande abonnement.

> [!NOTE]
> Omdat het standaardfilter hello wordt automatisch toegepast tooall nieuwe abonnementen, moet u eerst het standaardfilter Hallo of Hallo verwijderen **MatchAll** overschrijft alle andere filters die u kunt opgeven. U kunt de standaardregel Hallo verwijderen via Hallo `delete_rule` methode Hallo **ServiceBusService** object.
> 
> 

Hallo volgende voorbeeld maakt u een abonnement met de naam `HighMessages` met een **SqlFilter** die alleen berichten selecteert die een aangepaste `messagenumber` eigenschap groter is dan 3:

```python
bus_service.create_subscription('mytopic', 'HighMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber > 3'

bus_service.create_rule('mytopic', 'HighMessages', 'HighMessageFilter', rule)
bus_service.delete_rule('mytopic', 'HighMessages', DEFAULT_RULE_NAME)
```

Op deze manier hello volgende voorbeeld maakt u een abonnement met de naam `LowMessages` met een **SqlFilter** die alleen berichten selecteert die een `messagenumber` eigenschap kleiner dan of gelijk too3:

```python
bus_service.create_subscription('mytopic', 'LowMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber <= 3'

bus_service.create_rule('mytopic', 'LowMessages', 'LowMessageFilter', rule)
bus_service.delete_rule('mytopic', 'LowMessages', DEFAULT_RULE_NAME)
```

Nu wanneer een bericht verzonden te`mytopic` wordt het tooreceivers geabonneerd toohello altijd bezorgd **AllMessages** onderwerpabonnement en selectief bezorgd tooreceivers geabonneerd toohello **HighMessages**  en **LowMessages** onderwerpabonnementen (afhankelijk van de inhoud van Hallo-bericht).

## <a name="send-messages-tooa-topic"></a>Verzenden van berichten tooa onderwerp
een bericht tooa Service Bus-onderwerp toosend, uw toepassing moet gebruiken Hallo `send_topic_message` methode Hallo **ServiceBusService** object.

Hallo volgende voorbeeld toont hoe vijf toosend test berichten te`mytopic`. Houd er rekening mee dat Hallo `messagenumber` eigenschapswaarde van elk bericht varieert op Hallo herhaling van Hallo lus (deze bepaalt welke abonnementen ontvangen):

```python
for i in range(5):
    msg = Message('Msg {0}'.format(i).encode('utf-8'), custom_properties={'messagenumber':i})
    bus_service.send_topic_message('mytopic', msg)
```

Service Bus-onderwerpen ondersteunen een maximale berichtgrootte van 256 KB in Hallo [standaardcategorie](service-bus-premium-messaging.md) en 1 MB in Hallo [Premium-laag](service-bus-premium-messaging.md). Hallo-kop, die standaard Hallo- en aangepaste toepassingseigenschappen bevat, kan een maximale grootte van 64 KB hebben. Er is geen limiet voor het aantal berichten in een onderwerp hello, maar er is een limiet voor de totale grootte van berichten in een onderwerp Hallo Hallo. De grootte van het onderwerp wordt gedefinieerd tijdens het maken, met een bovengrens van 5 GB. Zie voor meer informatie over quota [Service Bus-quota][Service Bus quotas].

## <a name="receive-messages-from-a-subscription"></a>Berichten ontvangen van een abonnement
Berichten worden ontvangen van een abonnement met Hallo `receive_subscription_message` methode op Hallo **ServiceBusService** object:

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=False)
print(msg.body)
```

Berichten worden verwijderd uit het Hallo-abonnement als ze worden gelezen wanneer de parameter Hallo `peek_lock` te is ingesteld**False**. U kunt lezen (peek) en het Hallo-bericht zonder het te verwijderen uit de wachtrij Hallo door instelling Hallo parameter vergrendelen `peek_lock` te**True**.

Hallo gedrag van lezen en Hallo-bericht is verwijderd als onderdeel van Hallo ontvangstbewerking is Hallo eenvoudigste model en werkt het beste voor scenario's waarin een toepassing kan tolereren niet verwerken van een bericht in de gebeurtenis Hallo van een fout. toounderstand dit, Neem bijvoorbeeld een scenario in welke problemen van de consument Hallo Hallo aanvraag ontvangen en vervolgens vastloopt voordat het wordt verwerkt. Omdat Service Bus heeft gemarkeerd als verbruikt, vervolgens wanneer Hallo toepassing opnieuw wordt opgestart en verbruik van berichten opnieuw begint het Hallo-bericht, ontbreekt het Hallo-bericht dat was voorafgaande toohello crash verbruikt.

Als hello `peek_lock` parameter is ingesteld, te**True**, Hallo ontvangen, wordt een bewerking met twee fasen, waardoor het mogelijk toosupport toepassingen die geen ontbrekende berichten kunnen tolereren. Wanneer Service Bus een aanvraag ontvangt, zoeken naar het volgende bericht toobe Hallo verbruikt, wordt vergrendeld tooprevent andere consumenten het ontvangen en retourneert vervolgens toohello toepassing. Nadat de toepassing hello klaar is met verwerking van het Hallo-bericht (of veilig heeft opgeslagen voor toekomstige verwerking), is de tweede fase Hallo Hallo voltooid proces ontvangen door het aanroepen van `delete` methode op Hallo **bericht** object. Hallo `delete` methode markeert het Hallo-bericht als verbruikt en wordt deze verwijderd uit het Hallo-abonnement.

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Hoe toohandle toepassing is vastgelopen en onleesbare berichten
Service Bus biedt functionaliteit toohelp die u netjes te herstellen bij fouten in uw toepassing of problemen bij het verwerken van een bericht. Als een ontvangende toepassing niet kan tooprocess hello bericht voor een bepaalde reden en vervolgens kan worden aangeroepen Hallo `unlock` methode op Hallo **bericht** object. Hierdoor wordt ervoor zorgen dat Service Bus toounlock Hallo-bericht binnen Hallo-abonnement en beschikbaar toobe opnieuw ontvangen, ofwel Hallo door dezelfde toepassing of door een andere consumerende toepassing verbruikt.

Daarnaast is er een time-out gekoppeld aan een bericht in het Hallo-abonnement is vergrendeld en als de toepassing hello tooprocess Hallo-bericht voordat mislukt Hallo vergrendelingstime-out verloopt (bijvoorbeeld als Hallo toepassing vastloopt), en vervolgens de Service Bus Hiermee ontgrendelt u het Hallo-bericht automatisch en wordt het beschikbaar toobe opnieuw ontvangen.

In Hallo gebeurtenis die toepassing hello vastgelopen na het verwerken van het Hallo-bericht, maar voordat u Hallo `delete` methode wordt aangeroepen, is het Hallo-bericht altijd opnieuw bezorgd toohello toepassing opnieuw wordt gestart. Dit wordt vaak genoemd *tenminste eenmaal verwerken*, dat wil zeggen elk bericht ten minste één keer wordt verwerkt maar in bepaalde situaties Hallo hetzelfde bericht opnieuw kan worden bezorgd. Als Hallo scenario kan geen dubbele verwerking tolereren, moeten toepassingsontwikkelaars levering van aanvullende logica tootheir toepassing toohandle dubbele berichten toevoegen. Dit wordt vaak bereikt met behulp van Hallo **MessageId** eigenschap van Hallo-bericht dat gelijk bij meerdere bezorgingspogingen blijft.

## <a name="delete-topics-and-subscriptions"></a>Onderwerpen en abonnementen verwijderen
Onderwerpen en abonnementen worden permanent en expliciet moet worden verwijderd via Hallo [Azure-portal] [ Azure portal] of via een programma. Hallo volgende voorbeeld laat zien hoe toodelete Hallo onderwerp met de naam `mytopic`:

```python
bus_service.delete_topic('mytopic')
```

Als u een onderwerp verwijdert, verwijdert tevens abonnementen die zijn geregistreerd bij Hallo onderwerp. Abonnementen kunnen ook afzonderlijk worden verwijderd. Hallo volgende code toont hoe toodelete een abonnement met de naam `HighMessages` van Hallo `mytopic` onderwerp:

```python
bus_service.delete_subscription('mytopic', 'HighMessages')
```

## <a name="next-steps"></a>Volgende stappen
Nu u de basisprincipes van Service Bus-onderwerpen Hallo hebt geleerd, volgt u deze koppelingen toolearn meer.

* Zie [wachtrijen, onderwerpen en abonnementen][Queues, topics, and subscriptions].
* Referentiemateriaal [SqlFilter.SqlExpression][SqlFilter.SqlExpression].

[Azure portal]: https://portal.azure.com
[Azure Python package]: https://pypi.python.org/pypi/azure  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Service Bus quotas]: service-bus-quotas.md 
