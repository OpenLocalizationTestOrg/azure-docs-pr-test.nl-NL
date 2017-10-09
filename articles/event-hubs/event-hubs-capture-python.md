---
title: aaaAzure vastleggen van Event Hubs-overzicht | Microsoft Docs
description: Voorbeeld dat gebruikmaakt van hello Azure Python SDK toodemonstrate met Event Hubs vastleggen Hallo-functie.
services: event-hubs
documentationcenter: 
author: djrosanova
manager: timlt
editor: 
ms.assetid: bdff820c-5b38-4054-a06a-d1de207f01f6
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: darosa;sethm
ms.openlocfilehash: 1737dcca283711d863aa970db0e80ae71814e666
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-capture-walkthrough-python"></a>Overzicht van Event Hubs vastleggen: Python

Vastleggen van Event Hubs is een functie van Event Hubs waarmee u tooautomatically leveren Hallo gegevensstromen in uw event hub tooan Azure Blob storage-account van uw keuze. Hierdoor kunt u eenvoudig tooperform batchverwerking voor realtime streaming-gegevens. Dit artikel wordt beschreven hoe toouse Event Hubs vastleggen met behulp van Python. Zie voor meer informatie over het vastleggen van Event Hubs Hallo [overzichtsartikel](event-hubs-archive-overview.md).

In dit voorbeeld gebruikt Hallo [Azure Python SDK](https://azure.microsoft.com/develop/python/) toodemonstrate Hallo vastleggen functie. Hallo sender.py programma gesimuleerde omgeving telemetrie verzendt tooEvent Hubs in JSON-indeling. Hallo event hub is geconfigureerd toouse Hallo vastleggen functie toowrite deze tooblob opslag van gegevens in batches. Hallo capturereader.py app vervolgens deze blobs leest en maakt een toevoeg-bestand per apparaat en schrijft Hallo gegevens naar CSV-bestanden.

## <a name="what-will-be-accomplished"></a>Wat wordt bereikt

1. Maak een Azure Blob Storage-account en een blob-container binnen, met behulp van hello Azure-portal.
2. Maak een Event Hub-naamruimte met behulp van hello Azure-portal.
3. Een event hub met Hallo vastleggen functie is ingeschakeld, met hello Azure-portal maakt.
4. Verzenden van gegevens toohello event hub, met een pythonscript.
5. Hallo bestanden lezen uit Hallo vastleggen en deze met een ander pythonscript te verwerken.

## <a name="prerequisites"></a>Vereisten

- Python 2.7.x
- Een Azure-abonnement
- Een actieve [Event Hubs-naamruimte en event hub.](event-hubs-create.md)

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="create-an-azure-storage-account"></a>Een Azure Storage-account maken
1. Meld u aan toohello [Azure-portal][Azure portal].
2. In Hallo navigatiedeelvenster links van de portal hello, klikt u op **nieuw**, klikt u vervolgens op **opslag**, en klik vervolgens op **Opslagaccount**.
3. Hallo-velden in de blade opslagaccount hello en klik vervolgens op **maken**.
   
   ![][1]
4. Nadat er Hallo **implementaties is geslaagd** bericht wordt weergegeven, klikt u op Hallo-naam van nieuw opslagaccount hello en in Hallo **Essentials** blade, klikt u op **Blobs**. Wanneer Hallo **Blob-service** blade wordt geopend, klikt u op **+ Container** Hallo bovenaan. Naam Hallo container **vastleggen**, sluit Hallo **Blob-service** blade.
5. Klik op **toegangssleutels** in het Hallo links blade en kopiëren Hallo Hallo storage-account en Hallo-waarde van **key1**. Deze waarden tooNotepad of andere tijdelijke locatie opslaan.

## <a name="create-a-python-script-toosend-events-tooyour-event-hub"></a>Maken van een Python script toosend gebeurtenissen tooyour event hub
1. Open uw favoriete Python-editor, zoals [Visual Studio Code][Visual Studio Code].
2. Maken van een script met de naam **sender.py**. Dit script verzendt 200 gebeurtenissen tooyour event hub. Ze zijn eenvoudige milieu metingen in JSON verzonden.
3. Plak de volgende code in sender.py Hallo:
   
  ```python
  import uuid
  import datetime
  import random
  import json
  from azure.servicebus import ServiceBusService
   
  sbs = ServiceBusService(service_namespace='INSERT YOUR NAMESPACE NAME', shared_access_key_name='RootManageSharedAccessKey', shared_access_key_value='INSERT YOUR KEY')
  devices = []
  for x in range(0, 10):
      devices.append(str(uuid.uuid4()))
   
  for y in range(0,20):
      for dev in devices:
          reading = {'id': dev, 'timestamp': str(datetime.datetime.utcnow()), 'uv': random.random(), 'temperature': random.randint(70, 100), 'humidity': random.randint(70, 100)}
          s = json.dumps(reading)
          sbs.send_event('INSERT YOUR EVENT HUB NAME', s)
      print y
  ```
4. Hallo code toouse voorafgaand aan uw naamruimtenaam, de sleutelwaarde en de naam van de event hub die u hebt verkregen tijdens het maken van Event Hubs-naamruimte Hallo bijwerken.

## <a name="create-a-python-script-tooread-your-capture-files"></a>Maken van een Python script tooread uw bestanden vastleggen

1. Hallo-blade invullen en klikt u op **maken**.
2. Maken van een script met de naam **capturereader.py**. Dit script leest Hallo bestanden vastgelegd en maakt een bestand per apparaat toowrite Hallo gegevens alleen voor dat apparaat.
3. Plak de volgende code in capturereader.py Hallo:
   
  ```python
  import os
  import string
  import json
  import avro.schema
  from avro.datafile import DataFileReader, DataFileWriter
  from avro.io import DatumReader, DatumWriter
  from azure.storage.blob import BlockBlobService
   
  def processBlob(filename):
      reader = DataFileReader(open(filename, 'rb'), DatumReader())
      dict = {}
      for reading in reader:
          parsed_json = json.loads(reading["Body"])
          if not 'id' in parsed_json:
              return
          if not dict.has_key(parsed_json['id']):
              list = []
              dict[parsed_json['id']] = list
          else:
              list = dict[parsed_json['id']]
              list.append(parsed_json)
      reader.close()
      for device in dict.keys():
          deviceFile = open(device + '.csv', "a")
          for r in dict[device]:
              deviceFile.write(", ".join([str(r[x]) for x in r.keys()])+'\n')
   
  def startProcessing(accountName, key, container):
      print 'Processor started using path: ' + os.getcwd()
      block_blob_service = BlockBlobService(account_name=accountName, account_key=key)
      generator = block_blob_service.list_blobs(container)
      for blob in generator:
          if blob.properties.content_length != 0:
              print('Downloaded a non empty blob: ' + blob.name)
              cleanName = string.replace(blob.name, '/', '_')
              block_blob_service.get_blob_to_path(container, blob.name, cleanName)
              processBlob(cleanName)
              os.remove(cleanName)
          block_blob_service.delete_blob(container, blob.name)
  startProcessing('YOUR STORAGE ACCOUNT NAME', 'YOUR KEY', 'capture')
  ```
4. Ervoor toopaste worden Hallo juiste waarden voor de naam van het opslagaccount en de sleutel in Hallo aanroep te`startProcessing`.

## <a name="run-hello-scripts"></a>Hallo-scripts uitvoeren
1. Open een opdrachtprompt met Python in het pad en voer deze opdrachten vereiste tooinstall Python-pakketten:
   
  ```
  pip install azure-storage
  pip install azure-servicebus
  pip install avro
  ```
   
  Als u een eerdere versie van azure storage of azure hebt, moet u mogelijk toouse hello **--upgrade** optie
   
  Mogelijk moet u ook toorun Hallo volgen (niet nodig op de meeste systemen):
   
  ```
  pip install cryptography
  ```
2. Wijzigen van uw directory toowherever u sender.py en capturereader.py opgeslagen en voer deze opdracht uit:
   
  ```
  start python sender.py
  ```
   
  Deze opdracht start een nieuwe Python proces toorun Hallo-afzender.
3. Nu wacht enkele minuten tot Hallo vastleggen toorun. Typ vervolgens de volgende opdracht in uw oorspronkelijke opdrachtvenster Hallo:
   
   ```
   python capturereader.py
   ```

   Deze processor vastleggen gebruikt Hallo lokale directory toodownload alle Hallo blobs uit Hallo storage-account/container. Deze processen die niet leeg zijn, en Hallo resultaten als CSV-bestanden naar de lokale directory Hallo schrijft.

## <a name="next-steps"></a>Volgende stappen

U meer informatie over Event Hubs via Hallo koppelingen te volgen:

* [Overzicht van Event Hubs vastleggen][Overview of Event Hubs Capture]
* Een complete [voorbeeldtoepassing die gebruikmaakt van Event Hubs][sample application that uses Event Hubs].
* Hallo [uitschalen met Event Hubs verwerking] [ Scale out Event Processing with Event Hubs] voorbeeld.
* [Event Hubs-overzicht][Event Hubs overview]

[Azure portal]: https://portal.azure.com/
[Overview of Event Hubs Capture]: event-hubs-archive-overview.md
[1]: ./media/event-hubs-archive-python/event-hubs-python1.png
[About Azure storage accounts]:../storage/common/storage-create-storage-account.md
[Visual Studio Code]: https://code.visualstudio.com/
[Event Hubs overview]: event-hubs-overview.md
[sample application that uses Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
