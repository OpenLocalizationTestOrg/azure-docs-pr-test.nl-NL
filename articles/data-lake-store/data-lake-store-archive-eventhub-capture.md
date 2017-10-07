---
title: aaaCapture gegevens uit Event Hubs in Azure Data Lake Store | Microsoft Docs
description: Gebruik Azure Data Lake Store toocapture gegevens uit Event Hubs
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/28/2017
ms.author: nitinme
ms.openlocfilehash: 09b17bd0b47043bd2c83dba72c01a8064f206a0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-lake-store-toocapture-data-from-event-hubs"></a>Gebruik Azure Data Lake Store toocapture gegevens uit Event Hubs

Meer informatie over hoe toouse Azure Data Lake Store toocapture gegevens worden ontvangen door Azure Event Hubs.

## <a name="prerequisites"></a>Vereisten

* **Een Azure-abonnement**. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).

* **Een Azure Data Lake Store-account**. Voor instructies over het toocreate één, Zie [aan de slag met Azure Data Lake Store](data-lake-store-get-started-portal.md).

*  **Een naamruimte Event Hubs**. Zie voor instructies [maken van een naamruimte Event Hubs](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace). Controleer of Hallo Data Lake Store-account en Hallo Event Hubs naamruimte in Hallo hetzelfde Azure-abonnement.


## <a name="assign-permissions-tooevent-hubs"></a>Machtigingen toewijzen aan tooEvent Hubs

In deze sectie maakt maken u een map binnen Hallo account waar u toocapture Hallo gegevens uit Event Hubs. U ook toewijzen machtigingen tooEvent Hubs zodat van gegevens naar een Data Lake Store-account schrijven. 

1. Open Hallo Data Lake Store-account waarin u wilt dat toocapture gegevens uit Event Hubs en klik vervolgens op **Data Explorer**.

    ![Data Lake Store Gegevensverkenner](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Gegevensverkenner Data Lake Store")

2.  Klik op **nieuwe map** en voer een naam voor de map waar u toocapture Hallo gegevens.

    ![Een nieuwe map maken in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "een nieuwe map maken in Data Lake Store")

3. Wijs machtigingen in de hoofdmap van het Hallo Hallo Data Lake Store toe. 

    a. Klik op **Data Explorer**Hallo hoofdmap Hallo Data Lake Store-account selecteren en klik vervolgens op **toegang**.

    ![Machtigingen voor Data Lake Store-basis toe te wijzen](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "toegangsrechten voor de hoofdmap van de Data Lake Store")

    b. Onder **toegang**, klikt u op **toevoegen**, klikt u op **gebruiker of groep selecteren**, en zoek vervolgens naar `Microsoft.EventHubs`. 

    ![Machtigingen voor Data Lake Store-basis toe te wijzen](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "toegangsrechten voor de hoofdmap van de Data Lake Store")
    
    Klik op **Selecteren**.

    c. Onder **machtigingen toewijzen**, klikt u op **Selecteer machtigingen**. Stel **machtigingen** te**Execute**. Stel **toevoegen aan** te**deze map en alle onderliggende**. Stel **toevoegen als** te**een machtigingsvermelding toegang en een standaard machtigingsvermelding**.

    ![Machtigingen voor Data Lake Store-basis toe te wijzen](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "toegangsrechten voor de hoofdmap van de Data Lake Store")

    Klik op **OK**.

4. Machtigingen voor map van de Hallo onder Data Lake Store-account waarin u toocapture gegevens wilt toewijzen.

    a. Klik op **Data Explorer**, selecteert u Hallo-map in Hallo Data Lake Store-account en klik op **toegang**.

    ![Wijs machtigingen voor Data Lake Store-map](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "machtigingen voor Data Lake Store-map toewijzen")

    b. Onder **toegang**, klikt u op **toevoegen**, klikt u op **gebruiker of groep selecteren**, en zoek vervolgens naar `Microsoft.EventHubs`. 

    ![Wijs machtigingen voor Data Lake Store-map](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "machtigingen voor Data Lake Store-map toewijzen")
    
    Klik op **Selecteren**.

    c. Onder **machtigingen toewijzen**, klikt u op **Selecteer machtigingen**. Stel **machtigingen** te**lezen, schrijven,** en **Execute**. Stel **toevoegen aan** te**deze map en alle onderliggende**. Tot slot stelt **toevoegen als** te**een machtigingsvermelding toegang en een standaard machtigingsvermelding**.

    ![Wijs machtigingen voor Data Lake Store-map](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "machtigingen voor Data Lake Store-map toewijzen")
    
    Klik op **OK**. 

## <a name="configure-event-hubs-toocapture-data-toodata-lake-store"></a>Event Hubs toocapture tooData Lake gegevensarchief configureren

In deze sectie maakt u een Event Hub in een Event Hubs-naamruimte. U ook configureren Hallo Event Hub toocapture gegevens tooan Azure Data Lake Store-account. Deze sectie wordt ervan uitgegaan dat u al een naamruimte Event Hubs hebt gemaakt.

2. Van Hallo **overzicht** deelvenster van de naamruimte van de Event Hubs hello, klikt u op **+ Event Hub**.

    ![Event Hub maken](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "Event Hub maken")

3. Geef Hallo volgende waarden tooconfigure Event Hubs toocapture data tooData Lake Store.

    ![Event Hub maken](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "Event Hub maken")

    a. Geef een naam voor Hallo Event Hub.
    
    b. Voor deze zelfstudie stelt **aantal partities** en **bericht bewaren** toohello standaardwaarden.
    
    c. Stel **vastleggen** te**op**. Set Hallo **tijdvenster** (hoe vaak toocapture) en **grootte venster** (gegevens grootte toocapture). 
    
    d. Voor **vastleggen Provider**, selecteer **Azure Data Lake Store** en hello Selecteer Hallo Data Lake Store die u eerder hebt gemaakt. Voor **pad naar de Data Lake**, Hallo-naam van het Hallo-map die u hebt gemaakt in Hallo Data Lake Store-account invoeren. U hoeft alleen tooprovide Hallo relatief pad toohello map.

    e. Hallo laat **voorbeeld vastleggen bestandsindelingen naam** toohello standaardwaarde. Deze optie bepaalt Hallo mapstructuur die wordt gemaakt onder Hallo vastleggen map.

    f. Klik op **Create**.

## <a name="test-hello-setup"></a>Test Hallo setup

U kunt nu Hallo oplossing testen door te sturen gegevens toohello Azure Event Hub. Volg de instructies Hallo voor [gebeurtenissen verzenden tooAzure Event Hubs](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md). Wanneer u begint met het verzenden van gegevens hello, ziet u Hallo-gegevens in Data Lake Store worden weergegeven met behulp van Hallo-mapstructuur die u hebt opgegeven. Bijvoorbeeld, ziet u een mapstructuur, zoals wordt weergegeven in de volgende schermopname in uw Data Lake Store Hallo.

![Voorbeeld van EventHub-gegevens in Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Sample EventHub-gegevens in Data Lake Store")

> [!NOTE]
> Zelfs als er geen inkomende berichten bij Event Hubs, schrijft Event Hubs lege bestanden met NET Hallo kopteksten in Hallo Data Lake Store-account. Hallo-bestanden geschreven op Hallo dezelfde tijdsinterval die u hebt opgegeven tijdens het maken van Hallo Event Hubs.
> 
>

## <a name="analyze-data-in-data-lake-store"></a>Gegevens analyseren in Data Lake Store

Nadat gegevens Hallo Data Lake Store is, kunt u tooprocess en crisis Hallo gegevens analytische taken uitvoeren. Zie [USQL Avro voorbeeld](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) over het toodo deze met Azure Data Lake Analytics.
  

## <a name="see-also"></a>Zie ook
* [Gegevens in Data Lake Store beveiligen](data-lake-store-secure-data.md)
* [Gegevens kopiëren van Azure Storage Blobs tooData Lake Store](data-lake-store-copy-data-azure-storage-blob.md)
