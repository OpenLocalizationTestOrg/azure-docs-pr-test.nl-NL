---
title: aaaUsing Opslagverkenner (Preview) met Azure File storage | Microsoft Docs
description: Meer informatie over hoe meer informatie over hoe toouse Opslagverkenner (Preview) toowork met bestand deelt en bestanden.
services: storage
documentationcenter: na
author: cawaMS
manager: paulyuk
editor: 
ms.assetid: 
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/09/2017
ms.author: cawa
ms.openlocfilehash: 98eb3cde711ae3dbfdb6ffaec23ae24f822370e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-storage-explorer-preview-with-azure-file-storage"></a>Opslagverkenner (preview) gebruiken met Azure File Storage

Azure File storage is een service die bestand aanbiedt deelt in de cloud met behulp van Hallo Hallo standaard Server Message Block (SMB)-Protocol. Zowel SMB 2.1 als SMB 3.0 wordt ondersteund. Met Azure File storage, kunt u oudere toepassingen die afhankelijk van bestandsshares tooAzure snel en zonder kostbare regeneraties zijn te migreren. Kunt u bestandsgegevens opslag tooexpose openbaar toohello world of toostore toepassingsgegevens privé. In dit artikel leert u hoe toouse Opslagverkenner (Preview) toowork met bestand deelt, en bestanden.

## <a name="prerequisites"></a>Vereisten

toocomplete hello stappen in dit artikel, moet u de volgende Hallo:

- [Opslagverkenner (preview) downloaden en installeren](http://www.storageexplorer.com/)

- [Verbinding maken met tooa Azure storage-account of -service](https://docs.microsoft.com//azure/vs-azure-tools-storage-manage-with-storage-explorer#connect-to-a-storage-account-or-service)

## <a name="create-a-file-share"></a>Een bestandsshare maken

Alle bestanden moeten zich bevinden in een bestandsshare, wat in feite niets meer is dan een logische groepering van bestanden. Een account kan een onbeperkt aantal bestandsshares bevatten en elke share kan een onbeperkt aantal bestanden bevatten.

Hallo stappen laten zien hoe toocreate een bestandsshare in Opslagverkenner (Preview).

1. Open Opslagverkenner (Preview).

2. Vouw in het linkerdeelvenster Hallo Hallo waarbinnen u wenst dat toocreate Hallo File Share storage-account

3. Met de rechtermuisknop op **bestandsshares**, en selecteer in het contextmenu Hallo - **bestandsshare maken**.

    ![Bestandsshare maken](media/vs-azure-tools-storage-explorer-files/image1.png)

4. Een tekstvak wordt weergegeven onder Hallo **bestandsshares** map. Voer Hallo-naam voor de bestandsshare. Zie Hallo [delen naamgevingsregels](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container) sectie voor een lijst van regels en beperkingen voor de naamgeving van bestandsshares.

    ![Naamgeving Hallo-share](media/vs-azure-tools-storage-explorer-files/image2.png)

5. Druk op **Enter** wanneer gereed toocreate Hallo bestandsshare, of **Esc** toocancel. Zodra het Hallo-bestandsshare is gemaakt, die wordt weergegeven onder Hallo **bestandsshares** map voor Hallo storage-account geselecteerd.

    ![Hallo nieuwe share](media/vs-azure-tools-storage-explorer-files/image3.png)

## <a name="view-a-file-shares-contents"></a>De inhoud van een bestandsshare weergeven

Bestandsshares bevatten bestanden en mappen (die ook weer bestanden kunnen bevatten).

Hallo volgende stappen laten zien hoe tooview Hallo inhoud van een bestand delen in Opslagverkenner (Preview): +

1. Open Opslagverkenner (Preview).

2. Vouw in het linkerdeelvenster Hallo HALLO hallo-bestandsshare die u wenst dat tooview met storage-account.

3. Vouw Hallo storage account **bestandsshares**.

4. Klik met de rechtermuisknop Hallo bestandsshare u tooview wilt, en - selecteer in het contextmenu Hallo - **Open**. U kunt ook Hallo-bestandsshare die u wenst dat tooview dubbelklikken.

    ![Share openen](media/vs-azure-tools-storage-explorer-files/image4.png)

5. hoofdvenster Hello wordt Hallo van de bestandsshare inhoud weergegeven.
    
    ![Hallo delen van inhoud](media/vs-azure-tools-storage-explorer-files/image5.png)

## <a name="delete-a-file-share"></a>Een bestandsshare verwijderen

U kunt op ieder moment bestandsshares toevoegen en verwijderen. (toosee hoe toodelete afzonderlijke bestanden, Raadpleeg de sectie toohello [beheren van bestanden in een bestandsshare](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)

Hallo stappen laten zien hoe toodelete een bestandsshare in Opslagverkenner (Preview):

1. Open Opslagverkenner (Preview).

2. Vouw in het linkerdeelvenster Hallo HALLO hallo-bestandsshare die u wenst dat tooview met storage-account.

3. Vouw Hallo storage account **bestandsshares**.

4. Klik met de rechtermuisknop Hallo bestandsshare u toodelete wilt, en - selecteer in het contextmenu Hallo - **verwijderen**. U kunt ook op drukken **verwijderen** toodelete Hallo geselecteerde bestandsshare.

    ![Verwijderen](media/vs-azure-tools-storage-explorer-files/image6.png)

5. Selecteer **Ja** toohello bevestigingsvenster.
    
    ![Bevestigingsvenster](media/vs-azure-tools-storage-explorer-files/image7.png)

## <a name="copy-a-file-share"></a>Een bestandsshare kopiëren

Opslagverkenner (Preview) kunt u toocopy file share toohello Klembord en plak vervolgens of de bestandsshare in een ander opslagaccount. (toosee hoe toocopy afzonderlijke bestanden, Raadpleeg de sectie toohello [beheren van bestanden in een bestandsshare](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)

Hallo stappen laten zien hoe toocopy een bestand van een storage account tooanother delen.

1. Open Opslagverkenner (Preview).

2. Vouw in het linkerdeelvenster Hallo HALLO hallo-bestandsshare die u wenst dat toocopy met storage-account.

3. Vouw Hallo storage account **bestandsshares**.

4. Klik met de rechtermuisknop Hallo bestandsshare u toocopy wilt, en - selecteer in het contextmenu Hallo - **kopie-bestandsshare**.

    ![Bestandsshare kopiëren](media/vs-azure-tools-storage-explorer-files/image8.png)

5. Met de rechtermuisknop op de gewenste Hallo 'target' storage-account waarin u wilt toopaste Hallo-bestandsshare en - selecteer in het contextmenu Hallo - **plakken bestandsshare**.

    ![Bestandsshare plakken](media/vs-azure-tools-storage-explorer-files/image9.png)

## <a name="get-hello-sas-for-a-file-share"></a>Hallo SAS ophalen voor een bestandsshare

Een [shared access signature (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) tooresources gedelegeerde toegang in uw opslagaccount biedt. Dit betekent dat u een client beperkte machtigingen tooobjects in uw storage-account gedurende een bepaalde tijd en met een opgegeven set machtigingen, zonder tooshare de toegangssleutels van uw account kunt verlenen.

Hallo volgende stappen laten zien hoe toocreate een SAS voor een bestand delen: +

1. Open Opslagverkenner (Preview).

2. Vouw in het linkerdeelvenster Hallo HALLO hallo bestandsshare waarvoor tooget een SAS met storage-account.

3. Vouw Hallo storage account **bestandsshares**.

4. Met de rechtermuisknop op de gewenste bestandsshare hello, en selecteer in het contextmenu Hallo - **Shared Access Signature ophalen**.

    ![Handtekening voor gedeelde toegang ophalen](media/vs-azure-tools-storage-explorer-files/image10.png)

5. In Hallo **Shared Access Signature** dialoogvenster Hallo-beleid, de begin- en verloopdatum datums, de tijdzone opgeven en toegangsniveaus voor Hallo resource.

    ![SAS-dialoogvenster](media/vs-azure-tools-storage-explorer-files/image11.png)

6. Wanneer u klaar bent Hallo SAS-opties op te geven, selecteert u **maken**.

7. Een tweede **Shared Access Signature** dialoogvenster dat lijsten Hallo bestandsshare samen met de Hallo-URL en kunt u tooaccess QueryStrings Hallo storage resource vervolgens worden weergegeven. Selecteer **kopie** volgende toohello-URL die u wenst dat toocopy toohello Klembord.
    
    ![Tweede SAS-dialoogvenster](media/vs-azure-tools-storage-explorer-files/image12.png)

8. Als u klaar bent, selecteert u **Sluiten**.

## <a name="manage-access-policies-for-a-file-share"></a>Toegangsbeleid voor een bestandsshare beheren

Hallo volgende stappen laten zien hoe toomanage (toevoegen en verwijderen) toegangsbeleid voor een bestandsshare: +. Hallo-beleid wordt gebruikt voor het maken van SAS-URL's via welke mensen tooaccess Hallo opslagbestand resource gedurende een bepaalde tijd kunt gebruiken.

1. Open Opslagverkenner (Preview).

2. Vouw in het linkerdeelvenster Hallo HALLO hallo bestandsshare waarvan u wilt dat toomanage toegangsbeleid met storage-account.

3. Vouw Hallo storage account **bestandsshares**.

4. Selecteer de gewenste bestandsshare Hallo, en selecteer in het contextmenu Hallo - **toegangsbeleid beheren**.

    ![Contextmenu Toegangsbeleid beheren](media/vs-azure-tools-storage-explorer-files/image13.png)

5. Hallo **toegangsbeleid** dialoogvenster vermeldt alle beleidsregels voor toegang al is gemaakt voor de geselecteerde Hallo-bestandsshare.
    
    ![Toegangsbeleid](media/vs-azure-tools-storage-explorer-files/image14.png)

6. Volg deze stappen, afhankelijk van Hallo toegang beleid beheertaak:
    
    - **Een nieuw toegangsbeleid toevoegen**: selecteer **Toevoegen**. Zodra gegenereerd, Hallo **toegangsbeleid** dialoogvenster wordt weergegeven Hallo toegevoegde toegangsbeleid (met de standaardinstellingen).

    - **Een toegangsbeleid bewerken**: breng de gewenste wijzigingen aan en selecteer **Opslaan**.

    - **Verwijderen van een toegangsbeleid** : Selecteer **verwijderen** volgende toohello toegangsbeleid gewenste tooremove.

7. Maak een nieuwe SAS-URL met Hallo toegangsbeleid dat u eerder hebt gemaakt:
    
    ![SAS ophalen](media/vs-azure-tools-storage-explorer-files/image15.png)
    
    ![Naam en eigenschappen va SAS](media/vs-azure-tools-storage-explorer-files/image16.png)

## <a name="managing-files-in-a-file-share"></a>Bestanden in een bestandsshare beheren

Als u een bestandsshare hebt gemaakt, kunt u een bestandsshare toothat-bestand uploaden, downloaden van een bestand tooyour lokale computer, opent u een bestand op uw lokale computer en nog veel meer.

Hallo volgende stappen laten zien hoe toomanage Hallo-bestanden (en mappen) in een bestand delen.

1.  Open Opslagverkenner (Preview).

2.  Vouw in het linkerdeelvenster Hallo HALLO hallo-bestandsshare die u wenst dat toomanage met storage-account.

3.  Vouw Hallo storage account **bestandsshares**.

4.  Dubbelklik op Hallo-bestandsshare die u wenst dat tooview.

5.  hoofdvenster Hello wordt Hallo van de bestandsshare inhoud weergegeven.

    ![Hallo delen van inhoud](media/vs-azure-tools-storage-explorer-files/image17.png)

6.  hoofdvenster Hello wordt Hallo van de bestandsshare inhoud weergegeven.

7.  Volg deze dat stappen, afhankelijk van de taak Hallo gewenste tooperform:

    - **Uploaden van bestanden tooa bestandsshare**

        a.  Selecteer op de werkbalk Hallo hoofdvenster van **uploaden**, en vervolgens **bestanden uploaden** uit de vervolgkeuzelijst Hallo.

        ![Bestanden uploaden](media/vs-azure-tools-storage-explorer-files/image18.png)
        
        b. In Hallo **bestanden uploaden** dialoogvenster, selecteer Hallo weglatingsteken (**...** ) knop aan de rechterkant Hallo Hallo **bestanden** tekstvak tooselect Hallo op die u wenst dat tooupload.

        ![Bestanden toevoegen](media/vs-azure-tools-storage-explorer-files/image19.png)

        c. Selecteer **Uploaden**.

    - **Een bestandsshare van de map tooa uploaden**
        
        a. Selecteer op de werkbalk Hallo hoofdvenster van **uploaden**, en vervolgens **map uploaden** uit de vervolgkeuzelijst Hallo.

        ![Menu voor uploaden van map](media/vs-azure-tools-storage-explorer-files/image20.png)

        b. In Hallo **map Upload** dialoogvenster, selecteer Hallo weglatingsteken (**...** ) knop aan de rechterkant Hallo Hallo **map** tekst vak tooselect Hallo map waarvan de gewenste tooupload inhoud.

        c. Geef desgewenst een doelmap in welke Hallo inhoud van de geselecteerde map wordt geüpload. Als de doelmap Hallo niet bestaat, wordt deze gemaakt.

        d. Selecteer **Uploaden**.

    - **Een bestand tooyour lokale computer downloaden**
        
        a. Selecteer desgewenst toodownload Hallo-bestand.
        
        b. Selecteer op de werkbalk Hallo hoofdvenster van **downloaden**.
        
        c. In Hallo **opgeven waar toosave Hallo bestand hebt gedownload** dialoogvenster Hallo-locatie waar u gedownloade Hallo-bestand wilt opgeven en naam die u wenst dat toogive Hallo deze.

        d. Selecteer **Opslaan**.

    - **Een bestand op de lokale computer openen**
        
        a.  Selecteer desgewenst tooopen Hallo-bestand.
        
        b.  Selecteer op de werkbalk Hallo hoofdvenster van **Open**.
        
        c.  Hallo-bestand wordt gedownload en Hallo-toepassing die is gekoppeld aan de onderliggende bestandstype Hallo-bestand geopend.

    - **Een bestand toohello Klembord kopiëren**

        a. Selecteer desgewenst toocopy Hallo-bestand.

        b. Selecteer op de werkbalk Hallo hoofdvenster van **kopie**.

        c. Klik in het linkerdeelvenster Hallo Ga tooanother bestandsshare en dubbelklik erop tooview in het hoofdvenster Hallo.

        d. Selecteer op de werkbalk Hallo hoofdvenster van **plakken** toocreate een kopie van Hallo-bestand.

    - **Een bestand verwijderen**

        a. Selecteer desgewenst toodelete Hallo-bestand.

        b. Selecteer op de werkbalk Hallo hoofdvenster van **verwijderen**.

        c. Selecteer **Ja** toohello bevestigingsvenster.

## <a name="next-steps"></a>Volgende stappen

- Weergave Hallo [meest recente release-opmerkingen Opslagverkenner (Preview) en video's](http://www.storageexplorer.com/).

- Meer informatie over hoe te[maken van toepassingen met Azure blobs, tabellen, wachtrijen en bestanden](https://azure.microsoft.com/documentation/services/storage/).
