---
title: Event Hubs vastleggen aaaAzure inschakelen via de portal | Microsoft Docs
description: Inschakelen Hallo Event Hubs vastleggen via hello Azure-portal.
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/28/2017
ms.author: sethm
ms.openlocfilehash: 27c7528552c497a4d98873a22bd56a991c66247c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-event-hubs-capture-using-hello-azure-portal"></a>Inschakelen van Event Hubs vastleggen met behulp van hello Azure-portal

U kunt vastleggen configureren tijdens het Hallo event hub maken met behulp van Hallo [Azure-portal](https://portal.azure.com). U kunt beide vastleggen Hallo gegevens tooan Azure [Blob storage](https://azure.microsoft.com/services/storage/blobs/) container of tooan [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) account.

## <a name="capture-data-tooan-azure-storage-account"></a>Vastleggen van gegevens tooan Azure Storage-account  

Wanneer u een event hub maakt, kunt u vastleggen inschakelen door te klikken op Hallo **op** knop in Hallo **Event Hub maken** portalblade. Vervolgens geeft u een Opslagaccount en container door te klikken op **Azure Storage** in Hallo **vastleggen Provider** vak. Omdat Event Hubs vastleggen gebruik maakt van verificatie van de service-naar-service met opslag, hoeft u geen toospecify een verbindingsreeks voor opslag. Hallo resource objectkiezer Hallo resource-URI voor uw opslagaccount automatisch geselecteerd. Als u Azure Resource Manager gebruikt, moet u deze URI expliciet als een tekenreeks opgeven.

tijdvenster voor Hallo standaard is 5 minuten. Hallo minimumwaarde is 1, Hallo maximaal 15. Hallo **grootte** venster heeft een bereik van 10 500 MB.

![][1]

## <a name="capture-data-tooan-azure-data-lake-store-account"></a>Gegevens tooan Azure Data Lake Store-account voor het vastleggen

toocapture gegevens tooAzure Data Lake Store die u maakt een Data Lake Store-account en een event hub:

### <a name="create-an-azure-data-lake-store-account-and-folders"></a>Een Azure Data Lake Store-account en -mappen maken

1. Maken van een Data Lake Store-account, Hallo-instructies in [aan de slag met Azure Data Lake Store met hello Azure-portal](../data-lake-store/data-lake-store-get-started-portal.md). 
2. Maak een map onder dit account, instructies te volgen Hallo in Hallo [mappen maken in Azure Data Lake Store-account](../data-lake-store/data-lake-store-get-started-portal.md#createfolder) sectie.
3. Klik op Hallo Data Lake Store-accountblade **Data Explorer**.
4. Klik op **Toegang**.
5. Klik op **Add**.
6. In Hallo **zoeken op naam of e-mailadres** vak type **Microsoft.EventHubs** en selecteer deze optie. 
7. Hallo **machtigingen** tabblad wordt weergegeven. Hallo-machtigingen instellen zoals weergegeven in de volgende afbeelding Hallo:

    ![][6]

8. Klik op **OK**.
9. Maak nu een map in de hoofdmap Hallo door toohello doelmap bladeren en te klikken op Hallo mapnaam.
10. Klik op **Toegang**.
11. Klik op **Add**.
12. In Hallo **zoeken op naam of e-mailadres** vak type **Microsoft.EventHubs** en selecteer deze optie.
13. Hallo **machtigingen** tabblad opnieuw wordt weergegeven. Hallo-machtigingen instellen zoals weergegeven in de volgende afbeelding Hallo:

    ![][5]

### <a name="create-an-event-hub"></a>Een Event Hub maken

1. Houd er rekening mee Hallo event hub moet Hallo dezelfde Azure-abonnement als hello Azure Data Lake Store u zojuist hebt gemaakt. Maak Hallo event hub te klikken op Hallo **op** knop onder **vastleggen** in Hallo **Event Hub maken** portalblade. 
2. In Hallo **Event Hub maken** portalblade, selecteer **Azure Data Lake Store** van Hallo **vastleggen Provider** vak.
3. In **Selecteer Data Lake Store**, geef Hallo Data Lake Store-account voor u eerder en in Hallo gemaakt **pad naar de Data Lake** Voer Hallo pad toohello gegevensmap u hebt gemaakt.

    ![][3]

## <a name="add-or-configure-capture-on-an-existing-event-hub"></a>Capture toevoegen of configureren op een bestaande Event Hub

U kunt Capture configureren op bestaande Event Hubs in Event Hubs-naamruimten. tooenable vastleggen van een bestaande event hub of toochange uw instellingen vastleggen, klikt u op Hallo naamruimte tooload hello **Essentials** blade, klikt u vervolgens op Hallo event hub die u wilt tooenable of Hallo vastleggen instelling wijzigen. Tot slot op Hallo **eigenschappen** sectie Hallo blade geopend en bewerk vervolgens de instellingen voor het vastleggen van hello, zoals wordt weergegeven in de volgende cijfers Hallo:

### <a name="azure-blob-storage"></a>Azure Blob Storage

![][2]

### <a name="azure-data-lake-store"></a>Azure Data Lake Store

![][4]

[1]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture1.png
[2]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture2.png
[3]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture3.png
[4]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture4.png
[5]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture5.png
[6]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture6.png

## <a name="next-steps"></a>Volgende stappen

U kunt ook Event Hubs Capture configureren met behulp van Azure Resource Manager-sjablonen. Zie voor meer informatie [Capture inschakelen met behulp van een Azure Resource Manager-sjabloon](event-hubs-resource-manager-namespace-event-hub-enable-capture.md).
