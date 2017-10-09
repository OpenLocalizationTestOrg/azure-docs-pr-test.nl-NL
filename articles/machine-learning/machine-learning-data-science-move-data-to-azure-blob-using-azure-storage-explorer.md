---
title: aaaMove gegevens tooand van Blob Storage met Azure Storage Explorer | Microsoft Docs
description: Verplaatsen van gegevens tooand uit Azure Blob Storage met behulp van Azure Storage Explorer
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 10bd283f-0875-4c67-af63-6492270b7656
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 38d3bc009950c97d8474b0acceaf74814638dac0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage-using-azure-storage-explorer"></a>Verplaatsen van gegevens tooand uit Azure Blob Storage met behulp van Azure Storage Explorer
Azure Storage Explorer is een gratis hulpprogramma van Microsoft waarmee u toowork met Azure Storage-gegevens op Windows-, Mac OS- en Linux. Dit onderwerp wordt beschreven hoe toouse het tooupload en downloaden van Azure blob storage. Hallo-hulpprogramma kan worden gedownload vanaf [Microsoft Azure Storage Explorer](http://storageexplorer.com/).

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> Als u virtuele machine die is ingesteld met Hallo scripts geleverd door [gegevens wetenschappelijke virtuele machines in Azure](machine-learning-data-science-virtual-machines.md), en vervolgens Azure Opslagverkenner is al geïnstalleerd op Hallo VM.
> 
> [!NOTE]
> Voor een volledige inleiding tooAzure blob-opslag te verwijzen[basisbeginselen van Azure Blob](../storage/blobs/storage-dotnet-how-to-use-blobs.md) en [Azure Blob-Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).   
> 
> 

## <a name="prerequisites"></a>Vereisten
Dit document wordt ervan uitgegaan dat u een Azure-abonnement, een opslagaccount en de bijbehorende opslagsleutel Hallo voor dat account hebt. Voordat u gaat gegevens uploaden/downloaden, moet u weten Azure naam en sleutel van uw opslagaccount. 

* Zie tooset van een Azure-abonnement [gratis proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).
* Zie voor instructies over het maken van een opslagaccount en voor het ophalen van de account en sleutelgegevens [over Azure storage-accounts](../storage/common/storage-create-storage-account.md). Een opmerking Hallo-toegangssleutel voor uw opslagaccount maken als u dit account key tooconnect toohello met hello Azure Opslagverkenner hulpprogramma nodig.
* Hello Azure Opslagverkenner hulpprogramma kan worden gedownload vanaf [Microsoft Azure Storage Explorer](http://storageexplorer.com/). Accepteren Hallo standaardwaarden tijdens de installatie.

<a id="explorer"></a>

## <a name="use-azure-storage-explorer"></a>Azure Opslagverkenner gebruiken
volgende stappen document hoe Hallo tooupload/downloaden van gegevens met behulp van Azure Storage Explorer. 

1. Start Microsoft Azure Storage Explorer.
2. toobring up Hallo **tooyour account aanmelden...**  wizard selecteert u **Azure Accountinstellingen** pictogram, klikt u vervolgens **account toevoegen** en geef de referenties. ![Een Azure storage-account toevoegen](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/add-an-azure-store-account.png)
3. toobring up Hallo **tooAzure opslag verbinding** wizard, selecteer Hallo **tooAzure opslag koppelt** pictogram. ![Koppel tooAzure opslag](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/connect-to-azure-storage-1.png)
4. Voer Hallo toegangssleutel van uw Azure storage-account op Hallo **tooAzure opslag verbinding** wizard en vervolgens **volgende**. ![Koppel tooAzure opslag](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/connect-to-azure-storage-2.png)
5. Voer opslagaccountnaam in Hallo **accountnaam** vak en selecteer vervolgens **volgende**. ![Externe opslag koppelen](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/attach-external-storage.png)
6. Hallo storage-account toegevoegd zou nu moeten worden vermeld. toocreate een blob-container in een opslagaccount met de rechtermuisknop op Hallo **Blob-Containers** knooppunt in het account, selecteer **Blob-Container maken**, en voer een naam.
7. tooupload tooa gegevenscontainer, selecteer Hallo doel container en klikt u op Hallo **uploaden** knop.![ Storage-accounts](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/storage-accounts.png)
8. Klik op Hallo **...**  toohello rechts van Hallo **bestanden** tooupload voor een of meerdere bestanden van het bestandssysteem Hallo optie en klik op **uploaden** toobegin Hallo-bestanden te uploaden.![ Bestanden uploaden](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/upload-files-to-blob.png)
9. toodownload gegevens, Hallo selecteren in de bijbehorende container toodownload Hallo blob en klikt u op **downloaden**. ![Bestanden downloaden](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/download-files-from-blob.png)

