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
# <a name="event-hubs-capture-walkthrough-python"></a><span data-ttu-id="10155-103">Overzicht van Event Hubs vastleggen: Python</span><span class="sxs-lookup"><span data-stu-id="10155-103">Event Hubs Capture walkthrough: Python</span></span>

<span data-ttu-id="10155-104">Vastleggen van Event Hubs is een functie van Event Hubs waarmee u tooautomatically leveren Hallo gegevensstromen in uw event hub tooan Azure Blob storage-account van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="10155-104">Event Hubs Capture is a feature of Event Hubs that enables you tooautomatically deliver hello streaming data in your event hub tooan Azure Blob storage account of your choice.</span></span> <span data-ttu-id="10155-105">Hierdoor kunt u eenvoudig tooperform batchverwerking voor realtime streaming-gegevens.</span><span class="sxs-lookup"><span data-stu-id="10155-105">This capability makes it easy tooperform batch processing on real-time streaming data.</span></span> <span data-ttu-id="10155-106">Dit artikel wordt beschreven hoe toouse Event Hubs vastleggen met behulp van Python.</span><span class="sxs-lookup"><span data-stu-id="10155-106">This article describes how toouse Event Hubs Capture with Python.</span></span> <span data-ttu-id="10155-107">Zie voor meer informatie over het vastleggen van Event Hubs Hallo [overzichtsartikel](event-hubs-archive-overview.md).</span><span class="sxs-lookup"><span data-stu-id="10155-107">For more information about Event Hubs Capture, see hello [overview article](event-hubs-archive-overview.md).</span></span>

<span data-ttu-id="10155-108">In dit voorbeeld gebruikt Hallo [Azure Python SDK](https://azure.microsoft.com/develop/python/) toodemonstrate Hallo vastleggen functie.</span><span class="sxs-lookup"><span data-stu-id="10155-108">This sample uses hello [Azure Python SDK](https://azure.microsoft.com/develop/python/) toodemonstrate hello Capture feature.</span></span> <span data-ttu-id="10155-109">Hallo sender.py programma gesimuleerde omgeving telemetrie verzendt tooEvent Hubs in JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="10155-109">hello sender.py program sends simulated environmental telemetry tooEvent Hubs in JSON format.</span></span> <span data-ttu-id="10155-110">Hallo event hub is geconfigureerd toouse Hallo vastleggen functie toowrite deze tooblob opslag van gegevens in batches.</span><span class="sxs-lookup"><span data-stu-id="10155-110">hello event hub is configured toouse hello Capture feature toowrite this data tooblob storage in batches.</span></span> <span data-ttu-id="10155-111">Hallo capturereader.py app vervolgens deze blobs leest en maakt een toevoeg-bestand per apparaat en schrijft Hallo gegevens naar CSV-bestanden.</span><span class="sxs-lookup"><span data-stu-id="10155-111">hello capturereader.py app then reads these blobs and creates an append file per device, then writes hello data into .csv files.</span></span>

## <a name="what-will-be-accomplished"></a><span data-ttu-id="10155-112">Wat wordt bereikt</span><span class="sxs-lookup"><span data-stu-id="10155-112">What will be accomplished</span></span>

1. <span data-ttu-id="10155-113">Maak een Azure Blob Storage-account en een blob-container binnen, met behulp van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="10155-113">Create an Azure Blob Storage account and a blob container within it, using hello Azure portal.</span></span>
2. <span data-ttu-id="10155-114">Maak een Event Hub-naamruimte met behulp van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="10155-114">Create an Event Hub namespace, using hello Azure portal.</span></span>
3. <span data-ttu-id="10155-115">Een event hub met Hallo vastleggen functie is ingeschakeld, met hello Azure-portal maakt.</span><span class="sxs-lookup"><span data-stu-id="10155-115">Create an event hub with hello Capture feature enabled, using hello Azure portal.</span></span>
4. <span data-ttu-id="10155-116">Verzenden van gegevens toohello event hub, met een pythonscript.</span><span class="sxs-lookup"><span data-stu-id="10155-116">Send data toohello event hub with a Python script.</span></span>
5. <span data-ttu-id="10155-117">Hallo bestanden lezen uit Hallo vastleggen en deze met een ander pythonscript te verwerken.</span><span class="sxs-lookup"><span data-stu-id="10155-117">Read hello files from hello capture and process them with another Python script.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="10155-118">Vereisten</span><span class="sxs-lookup"><span data-stu-id="10155-118">Prerequisites</span></span>

- <span data-ttu-id="10155-119">Python 2.7.x</span><span class="sxs-lookup"><span data-stu-id="10155-119">Python 2.7.x</span></span>
- <span data-ttu-id="10155-120">Een Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="10155-120">An Azure subscription</span></span>
- <span data-ttu-id="10155-121">Een actieve [Event Hubs-naamruimte en event hub.](event-hubs-create.md)</span><span class="sxs-lookup"><span data-stu-id="10155-121">An active [Event Hubs namespace and event hub.](event-hubs-create.md)</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="10155-122">Een Azure Storage-account maken</span><span class="sxs-lookup"><span data-stu-id="10155-122">Create an Azure Storage account</span></span>
1. <span data-ttu-id="10155-123">Meld u aan toohello [Azure-portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="10155-123">Log on toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="10155-124">In Hallo navigatiedeelvenster links van de portal hello, klikt u op **nieuw**, klikt u vervolgens op **opslag**, en klik vervolgens op **Opslagaccount**.</span><span class="sxs-lookup"><span data-stu-id="10155-124">In hello left navigation pane of hello portal, click **New**, then click **Storage**, and then click **Storage Account**.</span></span>
3. <span data-ttu-id="10155-125">Hallo-velden in de blade opslagaccount hello en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="10155-125">Complete hello fields in hello storage account blade and then click **Create**.</span></span>
   
   ![][1]
4. <span data-ttu-id="10155-126">Nadat er Hallo **implementaties is geslaagd** bericht wordt weergegeven, klikt u op Hallo-naam van nieuw opslagaccount hello en in Hallo **Essentials** blade, klikt u op **Blobs**.</span><span class="sxs-lookup"><span data-stu-id="10155-126">After you see hello **Deployments Succeeded** message, click hello name of hello new storage account and in hello **Essentials** blade, click **Blobs**.</span></span> <span data-ttu-id="10155-127">Wanneer Hallo **Blob-service** blade wordt geopend, klikt u op **+ Container** Hallo bovenaan.</span><span class="sxs-lookup"><span data-stu-id="10155-127">When hello **Blob service** blade opens, click **+ Container** at hello top.</span></span> <span data-ttu-id="10155-128">Naam Hallo container **vastleggen**, sluit Hallo **Blob-service** blade.</span><span class="sxs-lookup"><span data-stu-id="10155-128">Name hello container **capture**, then close hello **Blob service** blade.</span></span>
5. <span data-ttu-id="10155-129">Klik op **toegangssleutels** in het Hallo links blade en kopiëren Hallo Hallo storage-account en Hallo-waarde van **key1**.</span><span class="sxs-lookup"><span data-stu-id="10155-129">Click **Access keys** in hello left blade and copy hello name of hello storage account and hello value of **key1**.</span></span> <span data-ttu-id="10155-130">Deze waarden tooNotepad of andere tijdelijke locatie opslaan.</span><span class="sxs-lookup"><span data-stu-id="10155-130">Save these values tooNotepad or some other temporary location.</span></span>

## <a name="create-a-python-script-toosend-events-tooyour-event-hub"></a><span data-ttu-id="10155-131">Maken van een Python script toosend gebeurtenissen tooyour event hub</span><span class="sxs-lookup"><span data-stu-id="10155-131">Create a Python script toosend events tooyour event hub</span></span>
1. <span data-ttu-id="10155-132">Open uw favoriete Python-editor, zoals [Visual Studio Code][Visual Studio Code].</span><span class="sxs-lookup"><span data-stu-id="10155-132">Open your favorite Python editor, such as [Visual Studio Code][Visual Studio Code].</span></span>
2. <span data-ttu-id="10155-133">Maken van een script met de naam **sender.py**.</span><span class="sxs-lookup"><span data-stu-id="10155-133">Create a script called **sender.py**.</span></span> <span data-ttu-id="10155-134">Dit script verzendt 200 gebeurtenissen tooyour event hub.</span><span class="sxs-lookup"><span data-stu-id="10155-134">This script sends 200 events tooyour event hub.</span></span> <span data-ttu-id="10155-135">Ze zijn eenvoudige milieu metingen in JSON verzonden.</span><span class="sxs-lookup"><span data-stu-id="10155-135">They are simple environmental readings sent in JSON.</span></span>
3. <span data-ttu-id="10155-136">Plak de volgende code in sender.py Hallo:</span><span class="sxs-lookup"><span data-stu-id="10155-136">Paste hello following code into sender.py:</span></span>
   
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
4. <span data-ttu-id="10155-137">Hallo code toouse voorafgaand aan uw naamruimtenaam, de sleutelwaarde en de naam van de event hub die u hebt verkregen tijdens het maken van Event Hubs-naamruimte Hallo bijwerken.</span><span class="sxs-lookup"><span data-stu-id="10155-137">Update hello preceding code toouse your namespace name, key value, and event hub name that you obtained when you created hello Event Hubs namespace.</span></span>

## <a name="create-a-python-script-tooread-your-capture-files"></a><span data-ttu-id="10155-138">Maken van een Python script tooread uw bestanden vastleggen</span><span class="sxs-lookup"><span data-stu-id="10155-138">Create a Python script tooread your Capture files</span></span>

1. <span data-ttu-id="10155-139">Hallo-blade invullen en klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="10155-139">Fill out hello blade and click **Create**.</span></span>
2. <span data-ttu-id="10155-140">Maken van een script met de naam **capturereader.py**.</span><span class="sxs-lookup"><span data-stu-id="10155-140">Create a script called **capturereader.py**.</span></span> <span data-ttu-id="10155-141">Dit script leest Hallo bestanden vastgelegd en maakt een bestand per apparaat toowrite Hallo gegevens alleen voor dat apparaat.</span><span class="sxs-lookup"><span data-stu-id="10155-141">This script reads hello captured files and creates a file per device toowrite hello data only for that device.</span></span>
3. <span data-ttu-id="10155-142">Plak de volgende code in capturereader.py Hallo:</span><span class="sxs-lookup"><span data-stu-id="10155-142">Paste hello following code into capturereader.py:</span></span>
   
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
4. <span data-ttu-id="10155-143">Ervoor toopaste worden Hallo juiste waarden voor de naam van het opslagaccount en de sleutel in Hallo aanroep te`startProcessing`.</span><span class="sxs-lookup"><span data-stu-id="10155-143">Be sure toopaste hello appropriate values for your storage account name and key in hello call too`startProcessing`.</span></span>

## <a name="run-hello-scripts"></a><span data-ttu-id="10155-144">Hallo-scripts uitvoeren</span><span class="sxs-lookup"><span data-stu-id="10155-144">Run hello scripts</span></span>
1. <span data-ttu-id="10155-145">Open een opdrachtprompt met Python in het pad en voer deze opdrachten vereiste tooinstall Python-pakketten:</span><span class="sxs-lookup"><span data-stu-id="10155-145">Open a command prompt that has Python in its path, and then run these commands tooinstall Python prerequisite packages:</span></span>
   
  ```
  pip install azure-storage
  pip install azure-servicebus
  pip install avro
  ```
   
  <span data-ttu-id="10155-146">Als u een eerdere versie van azure storage of azure hebt, moet u mogelijk toouse hello **--upgrade** optie</span><span class="sxs-lookup"><span data-stu-id="10155-146">If you have an earlier version of either azure-storage or azure, you may need toouse hello **--upgrade** option</span></span>
   
  <span data-ttu-id="10155-147">Mogelijk moet u ook toorun Hallo volgen (niet nodig op de meeste systemen):</span><span class="sxs-lookup"><span data-stu-id="10155-147">You might also need toorun hello following (not necessary on most systems):</span></span>
   
  ```
  pip install cryptography
  ```
2. <span data-ttu-id="10155-148">Wijzigen van uw directory toowherever u sender.py en capturereader.py opgeslagen en voer deze opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="10155-148">Change your directory toowherever you saved sender.py and capturereader.py, and run this command:</span></span>
   
  ```
  start python sender.py
  ```
   
  <span data-ttu-id="10155-149">Deze opdracht start een nieuwe Python proces toorun Hallo-afzender.</span><span class="sxs-lookup"><span data-stu-id="10155-149">This command starts a new Python process toorun hello sender.</span></span>
3. <span data-ttu-id="10155-150">Nu wacht enkele minuten tot Hallo vastleggen toorun.</span><span class="sxs-lookup"><span data-stu-id="10155-150">Now wait a few minutes for hello capture toorun.</span></span> <span data-ttu-id="10155-151">Typ vervolgens de volgende opdracht in uw oorspronkelijke opdrachtvenster Hallo:</span><span class="sxs-lookup"><span data-stu-id="10155-151">Then type hello following command into your original command window:</span></span>
   
   ```
   python capturereader.py
   ```

   <span data-ttu-id="10155-152">Deze processor vastleggen gebruikt Hallo lokale directory toodownload alle Hallo blobs uit Hallo storage-account/container.</span><span class="sxs-lookup"><span data-stu-id="10155-152">This capture processor uses hello local directory toodownload all hello blobs from hello storage account/container.</span></span> <span data-ttu-id="10155-153">Deze processen die niet leeg zijn, en Hallo resultaten als CSV-bestanden naar de lokale directory Hallo schrijft.</span><span class="sxs-lookup"><span data-stu-id="10155-153">It processes any that are not empty, and writes hello results as .csv files into hello local directory.</span></span>

## <a name="next-steps"></a><span data-ttu-id="10155-154">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="10155-154">Next steps</span></span>

<span data-ttu-id="10155-155">U meer informatie over Event Hubs via Hallo koppelingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="10155-155">You can learn more about Event Hubs by visiting hello following links:</span></span>

* <span data-ttu-id="10155-156">[Overzicht van Event Hubs vastleggen][Overview of Event Hubs Capture]</span><span class="sxs-lookup"><span data-stu-id="10155-156">[Overview of Event Hubs Capture][Overview of Event Hubs Capture]</span></span>
* <span data-ttu-id="10155-157">Een complete [voorbeeldtoepassing die gebruikmaakt van Event Hubs][sample application that uses Event Hubs].</span><span class="sxs-lookup"><span data-stu-id="10155-157">A complete [sample application that uses Event Hubs][sample application that uses Event Hubs].</span></span>
* <span data-ttu-id="10155-158">Hallo [uitschalen met Event Hubs verwerking] [ Scale out Event Processing with Event Hubs] voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="10155-158">hello [Scale out Event Processing with Event Hubs][Scale out Event Processing with Event Hubs] sample.</span></span>
* <span data-ttu-id="10155-159">[Event Hubs-overzicht][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="10155-159">[Event Hubs overview][Event Hubs overview]</span></span>

[Azure portal]: https://portal.azure.com/
[Overview of Event Hubs Capture]: event-hubs-archive-overview.md
[1]: ./media/event-hubs-archive-python/event-hubs-python1.png
[About Azure storage accounts]:../storage/common/storage-create-storage-account.md
[Visual Studio Code]: https://code.visualstudio.com/
[Event Hubs overview]: event-hubs-overview.md
[sample application that uses Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
