---
title: Azure Event Hubs Capture inschakelen via de portal | Microsoft Docs
description: Schakel de functie Event Hubs Capture in met behulp van de Azure-portal.
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
ms.openlocfilehash: 0cbf45dce922647f2996f929d2c7cf885a2f4db4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="enable-event-hubs-capture-using-the-azure-portal"></a>Event Hubs Capture inschakelen met behulp van de Azure-portal

Wanneer u de gebeurtenishub maakt, kunt u Capture configureren met behulp van de [Azure-portal](https://portal.azure.com). U kunt de gegevens vastleggen in een [Blob Storage](https://azure.microsoft.com/services/storage/blobs/)-container van Azure of in een [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/)-account.

## <a name="capture-data-to-an-azure-storage-account"></a>Gegevens vastleggen in een Azure Storage-account  

Wanneer u een event hub maakt, kunt u vastleggen inschakelen door te klikken op de **op** knop in de **Event Hub maken** portalblade. Vervolgens geeft u een opslagaccount en een container op door in de lijst **Capture-provider** te klikken op **Azure Storage**. Omdat Event Hubs Capture gebruikmaakt van service-naar-serviceverificatie met opslag, hoeft u geen verbindingsreeks voor opslag op te geven. De objectkiezer selecteert automatisch de resource-URI voor uw opslagaccount. Als u Azure Resource Manager gebruikt, moet u deze URI expliciet als een tekenreeks opgeven.

Het standaardtijdvenster is 5 minuten. De minimale waarde is 1, de maximale 15. Het venster **Grootte** heeft een bereik van 10-500 MB.

![][1]

## <a name="capture-data-to-an-azure-data-lake-store-account"></a>Gegevens vastleggen in een Azure Data Lake Store-account

Als u gegevens wilt vastleggen in Azure Data Lake Store, maakt u een Data Lake Store-account en een Event Hub:

### <a name="create-an-azure-data-lake-store-account-and-folders"></a>Een Azure Data Lake Store-account en -mappen maken

1. Maak een Data Lake Store-account volgens de instructies in [Aan de slag met Azure Data Lake Store met Azure Portal](../data-lake-store/data-lake-store-get-started-portal.md). 
2. Maak een map onder dit account, volgens de instructies in de sectie [Mappen maken in Azure Data Lake Store-account](../data-lake-store/data-lake-store-get-started-portal.md#createfolder).
3. Klik in de blade Data Lake Store-account op **Data Explorer**.
4. Klik op **Toegang**.
5. Klik op **Add**.
6. Typ **Microsoft.EventHubs** in het vak **Zoeken op naam of e-mailadres** en selecteer vervolgens deze optie. 
7. Het tabblad **Machtigingen** wordt weergegeven. Stel de machtigingen in zoals weergegeven in de volgende afbeelding:

    ![][6]

8. Klik op **OK**.
9. Maak nu een map in de hoofdmap door naar de doelmap te bladeren en te klikken op de naam van de map.
10. Klik op **Toegang**.
11. Klik op **Add**.
12. Typ **Microsoft.EventHubs** in het vak **Zoeken op naam of e-mailadres** en selecteer vervolgens deze optie.
13. Het tabblad **Machtigingen** wordt opnieuw weergegeven. Stel de machtigingen in zoals weergegeven in de volgende afbeelding:

    ![][5]

### <a name="create-an-event-hub"></a>Een Event Hub maken

1. De Event Hub moet deel uitmaken van het Azure-abonnement waarin de Azure Data Lake Store-account is opgenomen dat u zojuist hebt gemaakt. Maken van de event hub, te klikken op de **op** knop onder **vastleggen** in de **Event Hub maken** portalblade. 
2. In de **Event Hub maken** portalblade, selecteer **Azure Data Lake Store** van de **vastleggen Provider** vak.
3. Geef bij **Data Lake Store selecteren** het Data Lake Store-account op dat u eerder hebt gemaakt en voer vervolgens in het veld **Data Lake-pad** het pad in naar de gegevensmap die u hebt gemaakt.

    ![][3]

## <a name="add-or-configure-capture-on-an-existing-event-hub"></a>Capture toevoegen of configureren op een bestaande Event Hub

U kunt Capture configureren op bestaande Event Hubs in Event Hubs-naamruimten. Om Capture in te schakelen op een bestaande gebeurtenishub of de Capture-instellingen te wijzigen, klikt u op de naamruimte om de blade **Essentials** te laden en vervolgens klikt u op de gebeurtenishub waarvan u de Capture-instelling wilt inschakelen of wijzigen. Ten slotte op de **eigenschappen** sectie van de blade open en bewerk vervolgens de instellingen voor vastlegging, zoals wordt weergegeven in de volgende afbeeldingen:

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
