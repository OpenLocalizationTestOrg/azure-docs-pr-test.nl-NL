---
title: aaaManage Azure Blob Storage-resources met Opslagverkenner (Preview) | Microsoft Docs
description: Azure Blob-Containers en Blobs met Opslagverkenner (Preview) beheren
services: storage
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 2f09e545-ec94-4d89-b96c-14783cc9d7a9
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 503dd061b205875da127378ab48e8d465800fc09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-blob-storage-resources-with-storage-explorer-preview"></a>Azure Blob Storage-resources beheren met Opslagverkenner (Preview)
## <a name="overview"></a>Overzicht
[Azure Blob Storage](storage/blobs/storage-dotnet-how-to-use-blobs.md) is een service voor het opslaan van grote hoeveelheden ongestructureerde gegevens, zoals tekst of binaire gegevens, die toegankelijk zijn vanaf een willekeurige plaats in Hallo wereld via HTTP of HTTPS.
U kunt Blob storage-tooexpose gegevens openbaar toohello world of toostore toepassingsgegevens privé. In dit artikel leert u hoe toouse Opslagverkenner (Preview) toowork met blob-containers en blobs.

## <a name="prerequisites"></a>Vereisten
toocomplete hello stappen in dit artikel, moet u de volgende Hallo:

* [Opslagverkenner (preview) downloaden en installeren](http://www.storageexplorer.com)
* [Verbinding maken met tooa Azure storage-account of -service](vs-azure-tools-storage-manage-with-storage-explorer.md#connect-to-a-storage-account-or-service)

## <a name="create-a-blob-container"></a>Een blob-container maken
Alle blobs moeten zich bevinden in een blob-container gewoon een logische groepering van blobs is. Een account kan een onbeperkt aantal containers bevatten en elke container kan een onbeperkt aantal blobs opslaan.

Hallo volgende stappen laten zien hoe toocreate een blobcontainer in Opslagverkenner (Preview).

1. Open Opslagverkenner (Preview).
2. Vouw in het linkerdeelvenster Hallo Hallo storage-account waarin u wenst dat toocreate Hallo blob-container.
3. Met de rechtermuisknop op **Blob-Containers**, en selecteer in het contextmenu Hallo - **Blob-Container maken**.

   ![Contextmenu van blob-containers maken][0]
4. Een tekstvak wordt weergegeven onder Hallo **Blob-Containers** map. Hallo-naam voor uw blob-container opgeven. Zie Hallo [Container naamgevingsregels](storage/blobs/storage-dotnet-how-to-use-blobs.md#create-a-container) sectie voor een lijst van regels en beperkingen voor de naamgeving van blob-containers.

   ![Tekstvak voor Blob-Containers maken][1]
5. Druk op **Enter** wanneer klaar toocreate Hallo blob-container of **Esc** toocancel. Zodra het Hallo blob-container heeft gemaakt, die wordt weergegeven onder Hallo **Blob-Containers** map voor Hallo storage-account geselecteerd.

   ![BLOB-Container gemaakt][2]

## <a name="view-a-blob-containers-contents"></a>Een blob-container inhoud weergeven
BLOB-containers bevatten blobs en -mappen (die ook blobs kunnen bevatten).

Hallo volgende stappen laten zien hoe tooview Hallo inhoud van een blobcontainer in Opslagverkenner (Preview):

1. Open Opslagverkenner (Preview).
2. Vouw in het linkerdeelvenster Hallo HALLO hallo blob-container wilt van tooview met storage-account.
3. Vouw Hallo storage account **Blob-Containers**.
4. Met de rechtermuisknop op Hallo blob-container u tooview wilt en - selecteer in het contextmenu Hallo - **Open Editor voor Blob-Container**.
   U kunt ook Hallo blob-container gewenst tooview dubbelklikken.

   ![Open blob-container editor contextmenu][19]
5. hoofdvenster Hello wordt Hallo blob-container van inhoud weergegeven.

   ![Editor voor BLOB-container][3]

## <a name="delete-a-blob-container"></a>Verwijderen van een blob-container
BLOB-containers kunnen eenvoudig worden gemaakt en verwijderd indien nodig. (toosee hoe toodelete afzonderlijke blobs, Raadpleeg de sectie toohello [beheren blobs in een blobcontainer](#managing-blobs-in-a-blob-container).)

Hallo volgende stappen laten zien hoe toodelete een blobcontainer in Opslagverkenner (Preview):

1. Open Opslagverkenner (Preview).
2. Vouw in het linkerdeelvenster Hallo HALLO hallo blob-container wilt van tooview met storage-account.
3. Vouw Hallo storage account **Blob-Containers**.
4. Met de rechtermuisknop op Hallo blob-container u toodelete wilt en - selecteer in het contextmenu Hallo - **verwijderen**.
   U kunt ook op drukken **verwijderen** toodelete Hallo geselecteerde blob-container.

   ![Contextmenu van blob-container verwijderen][4]
5. Selecteer **Ja** toohello bevestigingsvenster.

   ![Verwijderen van blob-Container bevestigen][5]

## <a name="copy-a-blob-container"></a>Kopiëren van een blob-container
Opslagverkenner (Preview) kunt u toocopy een blob-container toohello Klembord en plak BLOB-container in een ander opslagaccount. (toosee hoe toocopy afzonderlijke blobs, Raadpleeg de sectie toohello [beheren blobs in een blobcontainer](#managing-blobs-in-a-blob-container).)

Hallo stappen laten zien hoe een blob-container uit één opslag toocopy tooanother account.

1. Open Opslagverkenner (Preview).
2. Vouw in het linkerdeelvenster Hallo HALLO hallo blob-container wilt van toocopy met storage-account.
3. Vouw Hallo storage account **Blob-Containers**.
4. Met de rechtermuisknop op Hallo blob-container u toocopy wilt en - selecteer in het contextmenu Hallo - **kopie Blob-Container**.

   ![Kopiëren van blob-container contextmenu][6]
5. Met de rechtermuisknop op de gewenste Hallo 'target' storage-account waarin u wilt toopaste Hallo blob-container en - selecteer in het contextmenu Hallo - **Blob-Container plakken**.

   ![Menu context blob-container plakken][7]

## <a name="get-hello-sas-for-a-blob-container"></a>Hallo SAS ophalen voor een blob-container
Een [shared access signature (SAS)](storage/common/storage-dotnet-shared-access-signature-part-1.md) tooresources gedelegeerde toegang in uw opslagaccount biedt.
Dit betekent dat u een client beperkte machtigingen tooobjects in uw opslagaccount gedurende een bepaalde tijd en met een opgegeven set machtigingen, zonder dat voor het delen van de toegangssleutels van uw account kunt verlenen.

Hallo volgende stappen laten zien hoe toocreate een SAS voor een blob-container:

1. Open Opslagverkenner (Preview).
2. Vouw in het linkerdeelvenster Hallo HALLO hallo blob-container waarvoor tooget een SAS met storage-account.
3. Vouw Hallo storage account **Blob-Containers**.
4. Met de rechtermuisknop op de gewenste blobcontainer hello, en selecteer in het contextmenu Hallo - **Shared Access Signature ophalen**.

   ![Contextmenu SAS ophalen][8]
5. In Hallo **Shared Access Signature** dialoogvenster Hallo-beleid, de begin- en verloopdatum datums, de tijdzone opgeven en toegangsniveaus voor Hallo resource.

   ![Ophalen van SAS-opties][9]
6. Wanneer u klaar bent Hallo SAS-opties op te geven, selecteert u **maken**.
7. Een tweede **Shared Access Signature** dialoogvenster dat een lijst met blob-container samen met de URL Hallo Hallo en kunt u tooaccess QueryStrings Hallo storage resource vervolgens worden weergegeven.
   Selecteer **kopie** volgende toohello-URL die u wenst dat toocopy toohello Klembord.

   ![SAS-URL's kopiëren][10]
8. Als u klaar bent, selecteert u **Sluiten**.

## <a name="manage-access-policies-for-a-blob-container"></a>-Beleid beheren voor een blob-container
Hallo volgende stappen laten zien hoe toomanage (toevoegen en verwijderen) toegangsbeleid voor een blob-container:

1. Open Opslagverkenner (Preview).
2. Vouw in het linkerdeelvenster Hallo HALLO hallo blob-container waarvan u wilt dat toomanage toegangsbeleid met storage-account.
3. Vouw Hallo storage account **Blob-Containers**.
4. Selecteer de gewenste blobcontainer Hallo, en selecteer in het contextmenu Hallo - **toegangsbeleid beheren**.

   ![Contextmenu Toegangsbeleid beheren][11]
5. Hallo **toegangsbeleid** dialoogvenster vermeldt alle beleidsregels voor toegang al is gemaakt voor Hallo geselecteerde blob-container.

   ![Opties voor toegangsbeleid][12]        
6. Volg deze stappen, afhankelijk van Hallo toegang beleid beheertaak:

   * **Een nieuw toegangsbeleid toevoegen**: selecteer **Toevoegen**. Zodra gegenereerd, Hallo **toegangsbeleid** dialoogvenster wordt weergegeven Hallo toegevoegde toegangsbeleid (met de standaardinstellingen).
   * **Een toegangsbeleid bewerken** - eventueel wijzigingen doorvoeren en selecteer **opslaan**.
   * **Verwijderen van een toegangsbeleid** : Selecteer **verwijderen** volgende toohello toegangsbeleid gewenste tooremove.

## <a name="set-hello-public-access-level-for-a-blob-container"></a>Hallo openbare toegangsniveau instellen voor een blob-container
Standaard elke blob-container te ingesteld 'Geen openbare toegang'.

Hallo volgende stappen laten zien hoe toospecify dat door een openbare toegang tot niveau voor een blob-container.

1. Open Opslagverkenner (Preview).
2. Vouw in het linkerdeelvenster Hallo HALLO hallo blob-container waarvan u wilt dat toomanage toegangsbeleid met storage-account.
3. Vouw Hallo storage account **Blob-Containers**.
4. Selecteer de gewenste blobcontainer Hallo, en selecteer in het contextmenu Hallo - **ingesteld openbare toegangsniveau**.

   ![Openbare toegang niveau contextmenu instellen][13]
5. In Hallo **ingesteld Container openbaar toegangsniveau** dialoogvenster u Hallo gewenst toegangsniveau kunt opgeven.

   ![Opties voor openbare toegang niveau instellen][14]
6. Selecteer **Toepassen**.

## <a name="managing-blobs-in-a-blob-container"></a>Blobs in een blobcontainer beheren
Als u een blob-container hebt gemaakt, kunt u een blob-container toothat blob uploaden, downloaden van een blob tooyour lokale computer, opent u een blob op uw lokale computer en nog veel meer.

Hallo stappen laten zien hoe toomanage BLOB's (en mappen) Hallo binnen een blob-container.

1. Open Opslagverkenner (Preview).
2. Vouw in het linkerdeelvenster Hallo HALLO hallo blob-container wilt van toomanage met storage-account.
3. Vouw Hallo storage account **Blob-Containers**.
4. Dubbelklik op Hallo gewenst tooview blob-container.
5. hoofdvenster Hello wordt Hallo blob-container van inhoud weergegeven.

   ![Weergave blob-container][3]
6. hoofdvenster Hello wordt Hallo blob-container van inhoud weergegeven.
7. Volg deze dat stappen, afhankelijk van de taak Hallo gewenste tooperform:

   * **Uploaden van bestanden tooa blob-container**

     1. Selecteer op de werkbalk Hallo hoofdvenster van **uploaden**, en vervolgens **bestanden uploaden** uit de vervolgkeuzelijst Hallo.

        ![Menu bestanden uploaden][15]
     2. In Hallo **bestanden uploaden** dialoogvenster, selecteer Hallo weglatingsteken (**...** ) knop aan de rechterkant Hallo Hallo **bestanden** tekstvak tooselect Hallo op die u wenst dat tooupload.

        ![Opties voor bestanden uploaden][16]
     3. Geef Hallo type **Blob-type**. Hallo artikel [aan de slag met Azure Blob storage met .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) uitgelegd Hallo verschillen tussen Hallo diverse typen van de blob.
     4. Geef desgewenst een pad van de map waarnaar u de geselecteerde bestanden hello wordt geüpload. Als de doelmap Hallo niet bestaat, wordt deze gemaakt.
     5. Selecteer **Uploaden**.
   * **Uploaden van een map tooa blob-container**

     1. Selecteer op de werkbalk Hallo hoofdvenster van **uploaden**, en vervolgens **map uploaden** uit de vervolgkeuzelijst Hallo.

        ![Menu voor uploaden van map][17]
     2. In Hallo **map Upload** dialoogvenster, selecteer Hallo weglatingsteken (**...** ) knop aan de rechterkant Hallo Hallo **map** tekst vak tooselect Hallo map waarvan de gewenste tooupload inhoud.

        ![Mapopties uploaden][18]
     3. Geef Hallo type **Blob-type**. Hallo artikel [aan de slag met Azure Blob storage met .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) uitgelegd Hallo verschillen tussen Hallo diverse typen van de blob.
     4. Geef desgewenst een doelmap in welke Hallo inhoud van de geselecteerde map wordt geüpload. Als de doelmap Hallo niet bestaat, wordt deze gemaakt.
     5. Selecteer **Uploaden**.
   * **Een blob tooyour lokale computer downloaden**

     1. Selecteer desgewenst toodownload Hallo-blob.
     2. Selecteer op de werkbalk Hallo hoofdvenster van **downloaden**.
     3. In Hallo **opgeven waar toosave Hallo blob gedownload** dialoogvenster Geef Hallo-locatie waar u Hallo blob gedownload en naam die u wenst dat toogive Hallo deze.  
     4. Selecteer **Opslaan**.
   * **Open een blob op uw lokale computer**

     1. Selecteer desgewenst tooopen Hallo-blob.
     2. Selecteer op de werkbalk Hallo hoofdvenster van **Open**.
     3. Hallo blob wordt gedownload en geopend met Hallo-toepassing die is gekoppeld aan de onderliggende bestandstype Hallo-blob.
   * **Een blob toohello Klembord kopiëren**

     1. Selecteer desgewenst toocopy Hallo-blob.
     2. Selecteer op de werkbalk Hallo hoofdvenster van **kopie**.
     3. Klik in het linkerdeelvenster Hallo Ga tooanother blob-container en dubbelklik erop tooview in het hoofdvenster Hallo.
     4. Selecteer op de werkbalk Hallo hoofdvenster van **plakken** toocreate een kopie van het Hallo-blob.
   * **Verwijderen van een blob**

     1. Selecteer desgewenst toodelete Hallo-blob.
     2. Selecteer op de werkbalk Hallo hoofdvenster van **verwijderen**.
     3. Selecteer **Ja** toohello bevestigingsvenster.

## <a name="next-steps"></a>Volgende stappen
* Weergave Hallo [meest recente release-opmerkingen Opslagverkenner (Preview) en video's](http://www.storageexplorer.com).
* Meer informatie over hoe te[maken van toepassingen met Azure blobs, tabellen, wachtrijen en bestanden](https://azure.microsoft.com/documentation/services/storage/).

[0]: ./media/vs-azure-tools-storage-explorer-blobs/blob-containers-create-context-menu.png
[1]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-create.png
[2]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-create-done.png
[3]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-editor.png
[4]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-context-menu.png
[5]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-confirmation.png
[6]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-copy-context-menu.png
[7]: ./media/vs-azure-tools-storage-explorer-blobs/blob-containers-paste-context-menu.png
[8]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-context-menu.png
[9]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-options.png
[10]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-urls.png
[11]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-context-menu.png
[12]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-options.png
[13]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-context-menu.png
[14]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-options.png
[15]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-menu.png
[16]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-options.png
[17]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-menu.png
[18]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-options.png
[19]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-open-editor-context-menu.png
