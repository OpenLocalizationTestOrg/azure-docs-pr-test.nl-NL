---
title: aaaHow toouse Queue storage met Python | Microsoft Docs
description: Informatie over hoe toouse hello Azure Queue-service van Python toocreate en verwijderen van wachtrijen, en invoegen, ophalen en verwijderen van berichten.
services: storage
documentationcenter: python
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: cc0d2da2-379a-4b58-a234-8852b4e3d99d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: ce8d999d9fafaef0dab48442560d004c034c0804
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-python"></a>Hoe toouse Queue storage met Python
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Overzicht
Deze handleiding wordt getoond hoe tooperform algemene scenario's met behulp van hello Azure Queue storage-service. Hallo-voorbeelden zijn geschreven in Python en gebruiken van Hallo [Microsoft Azure-opslag-SDK voor Python]. Hallo scenario's worden behandeld: **invoegen**, **inspecteren**, **ophalen**, en **verwijderen** wachtrij berichten, evenals  **maken en verwijderen van wachtrijen**. Raadpleeg voor meer informatie over wachtrijen toohello [Vervolgstappen]-sectie.

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="how-to-create-a-queue"></a>Procedure: Een wachtrij maken
Hallo **QueueService** object kunt u samenwerken met wachtrijen. Hallo volgende code maakt een **QueueService** object. Voeg de volgende Hallo bij Hallo bovenkant van een Python-bestand waarin u wenst dat tooprogrammatically toegang tot Azure Storage:

```python
from azure.storage.queue import QueueService
```

Hallo volgende code maakt een **QueueService** -object op met de Hallo naam en opslagaccountsleutel. 'Myaccount' en 'mykey' vervangen door uw accountnaam en de sleutel.

```python
queue_service = QueueService(account_name='myaccount', account_key='mykey')

queue_service.create_queue('taskqueue')
```

## <a name="how-to-insert-a-message-into-a-queue"></a>Procedure: Een bericht in een wachtrij invoegen
een bericht in een wachtrij, gebruik Hallo tooinsert **plaatsen\_bericht** methode voor het maken van een nieuw bericht en deze wachtrij toohello toevoegen.

```python
queue_service.put_message('taskqueue', u'Hello World')
```

## <a name="how-to-peek-at-hello-next-message"></a>Procedure: Inspecteren Hallo het Volgendebericht
U kunt bekijken van Hallo-bericht in Hallo begin van een wachtrij zonder het te verwijderen uit de wachtrij Hallo door aanroepen Hallo **peek\_berichten** methode. Standaard **peek\_berichten** peeks op één bericht.

```python
messages = queue_service.peek_messages('taskqueue')
for message in messages:
    print(message.content)
```

## <a name="how-to-dequeue-messages"></a>Procedure: Berichten in wachtrij
Uw code wordt een bericht uit een wachtrij in twee stappen. Als u aanroept **ophalen\_berichten**, u het volgende Hallo-bericht in een wachtrij standaard ophalen. Een bericht dat wordt geretourneerd door **ophalen\_berichten** wordt onzichtbaar tooany andere codes die berichten lezen uit deze wachtrij. Standaard blijft het bericht onzichtbaar gedurende 30 seconden. toofinish verwijderen Hallo-bericht uit de wachtrij hello, moet u ook aanroepen **verwijderen\_bericht**. Dit proces in twee stappen van het verwijderen van een bericht zorgt ervoor dat wanneer uw code tooprocess een bericht als gevolg van hardware-of softwarefout mislukt, een ander exemplaar van uw code kunt het bericht verschijnt en probeer het opnieuw. Uw code haalt **verwijderen\_bericht** direct nadat het Hallo-bericht is verwerkt.

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)
```

Er zijn twee manieren waarop u het ophalen van berichten uit een wachtrij kunt aanpassen.
U krijgt eerst een batch met berichten (omhoog too32). Ten tweede kunt u instellen een time-out voor onzichtbaarheid langer of korter, zodat uw code meer of minder tijd toofully elk bericht niet verwerken. Hallo volgende codevoorbeeld wordt de **ophalen\_berichten** methode tooget 16 berichten in één aanroep. Vervolgens wordt verwerkt elke bericht met een for-lus. Time-out voor onzichtbaarheid van Hallo wordt ingesteld op vijf minuten voor elk bericht.

```python
messages = queue_service.get_messages('taskqueue', num_messages=16, visibility_timeout=5*60)
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)        
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>Procedure: Hallo inhoud van een bericht in de wachtrij wijzigen
U kunt Hallo inhoud van een bericht in-place in Hallo wachtrij wijzigen. Als het bericht een werktaak vertegenwoordigt, kunt u deze functie tooupdate de status van de werktaak hello gebruiken. Hallo-code hieronder maakt gebruik van Hallo **bijwerken\_bericht** methode tooupdate een bericht. Hallo zichtbaarheid time-out ingesteld too0, wat betekent dat het bericht verschijnt onmiddellijk en Hallo inhoud wordt bijgewerkt.

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    queue_service.update_message('taskqueue', message.id, message.pop_receipt, 0, u'Hello World Again')
```

## <a name="how-to-get-hello-queue-length"></a>Procedure: Hallo wachtrijlengte ophalen
U kunt een schatting maken van het aantal berichten Hallo krijgen in een wachtrij. De **ophalen\_wachtrij\_metagegevens** methode vraagt Hallo wachtrij tooreturn metagegevens over Hallo wachtrij en Hallo **approximate_message_count**. Hallo-resultaat is alleen een benadering omdat berichten kunnen worden toegevoegd of verwijderd nadat de queue-service tooyour aanvraag reageert.

```python
metadata = queue_service.get_queue_metadata('taskqueue')
count = metadata.approximate_message_count
```

## <a name="how-to-delete-a-queue"></a>Procedure: Een wachtrij verwijderen
toodelete een wachtrij en alle Hallo-berichten die dit, neemt u contact de **verwijderen\_wachtrij** methode.

```python
queue_service.delete_queue('taskqueue')
```

## <a name="next-steps"></a>Volgende stappen
Nu u Hallo basisprincipes van Queue storage hebt geleerd, volgt u deze koppelingen toolearn meer.

* [Python Developer Center](/develop/python/)
* [REST-API voor Azure Storage-services](http://msdn.microsoft.com/library/azure/dd179355)
* [Blog van het Azure Storage-team]
* [Microsoft Azure-opslag-SDK voor Python]

[Blog van het Azure Storage-team]: http://blogs.msdn.com/b/windowsazurestorage/
[Microsoft Azure-opslag-SDK voor Python]: https://github.com/Azure/azure-storage-python