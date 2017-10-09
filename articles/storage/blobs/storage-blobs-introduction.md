---
title: aaaIntroduction tooAzure Blob storage | Microsoft Docs
description: Inleiding tooAzure Blob-opslag
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: robinsh
ms.openlocfilehash: 3431f826ae51d42dbced084ee60f9ff70a8168d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooblob-storage"></a>Inleiding tooBlob opslag

Azure Blob storage is een service voor het opslaan van grote hoeveelheden ongestructureerde objectgegevens, zoals tekst of binaire gegevens, die toegankelijk zijn vanaf een willekeurige plaats in Hallo wereld via HTTP of HTTPS. U kunt Blob storage-tooexpose gegevens openbaar toohello world of toostore toepassingsgegevens privé.

Veelvoorkomende toepassingen van Blob Storage zijn onder andere:

* Voor afbeeldingen of documenten rechtstreeks tooa browser
* De opslag van bestanden voor gedistribueerde toegang
* Streaming van video en audio
* De opslag van gegevens voor back-up en herstel, herstel na noodgevallen en archivering
* De opslag van gegevens voor analyse door een on-premises in Azure gehoste service

## <a name="blob-service-concepts"></a>Concepten van Blob service

Hallo Blob-service bevat Hallo volgende onderdelen:

![Blobarchitectuur](./media/storage-blobs-introduction/blob1.png)

* **Storage-Account:** alle toegang tot tooAzure opslag wordt gedaan via een opslagaccount. Dit opslagaccount mag een **algemeen opslagaccount** of een **Blob-opslagaccount** die speciaal is bedoeld voor het opslaan van objecten/blobs. Zie [Over Azure Storage-accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) voor meer informatie.

* **Container:** Een container is een groepering van een reeks blobs. Alle blobs moeten zich in een container bevinden. Een account kan een onbeperkt aantal containers bevatten. Een container kan een onbeperkt aantal blobs bevatten. Houd er rekening mee dat Hallo containernaam moet een kleine letter.

* **Blob:** Een bestand van willekeurig type en willekeurige grootte. Azure Storage biedt drie typen blobs: blok-blobs, pagina-blobs en toevoeg-blobs.
  
    *Blok-blobs* zijn ideaal voor de opslag van tekst- of binaire bestanden, zoals documenten en mediabestanden. *Toevoeg-blobs* zijn vergelijkbaar tooblock blobs in dat ze bestaan uit blokken, maar ze zijn geoptimaliseerd voor toevoegbewerkingen; ze zijn daarom nuttig voor logboekscenario's. Een enkel blok-blob kan bevatten up too50, 000 blokken van too100 MB, voor een totale grootte van iets meer dan 4.75 TB (100 MB X 50.000). Een enkele toevoeg-blob kan bevatten up too50, 000 blokken van too4 MB, voor een totale grootte van iets meer dan 195 GB (4 MB X 50.000).
  
    *Pagina-blobs* kan up too1 TB groot zijn en zijn efficiënter voor regelmatige lees-en schrijfbewerkingen. Virtuele Machines in Azure maakt gebruik van pagina-blobs als besturingssysteem en gegevensschijven.
  
    Zie [Containers, blobs en metagegevens een naam geven en hiernaar verwijderen](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata) voor meer informatie over de naamgeving van containers en blobs.

## <a name="next-steps"></a>Volgende stappen

* [Een opslagaccount maken](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [Aan de slag met Blob storage met .NET](storage-dotnet-how-to-use-blobs.md)