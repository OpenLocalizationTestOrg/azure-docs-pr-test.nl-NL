---
title: aaaAdd hello Azure blob-opslag-Connector in uw logische Apps | Microsoft Docs
description: Aan de slag en hello Azure blob storage-connector in een logische app configureren
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b5dc3f75-6bea-420b-b250-183668d2848d
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/02/2017
ms.author: mandia; ladocs
ms.openlocfilehash: add61287ef1b2228ef9d3f54ce082807bad6858b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-blob-storage-connector-in-a-logic-app"></a>Hello Azure blob storage-connector in een logische app gebruiken
Gebruik hello Azure Blob storage-connector tooupload, bijwerken, ophalen en verwijderen van blobs in uw opslagaccount, alle binnen een logische app.  

Met Azure blob storage, u:

* De werkstroom maken door nieuwe projecten uploaden of ophalen van bestanden die onlangs zijn bijgewerkt.
* Acties tooget bestandsmetagegevens gebruiken en verwijderen van een bestand en bestanden kopiëren. Bijvoorbeeld wanneer een hulpprogramma is bijgewerkt in een Azure-website (een trigger), vervolgens bijwerken een bestand in blob storage (een actie). 

Dit onderwerp leest u hoe toouse Hallo blob-opslag-connector in een logische app.

toolearn meer informatie over Logic Apps, Zie [wat zijn logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) en [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).

toolearn meer informatie over Logic Apps, Zie [wat zijn logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) en [een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-tooazure-blob-storage"></a>Verbinding maken met tooAzure blob-opslag
Om uw logische app toegang alle services tot, maakt u eerst een *verbinding* toohello service. Een verbinding biedt connectiviteit tussen een logische app en een andere service. Bijvoorbeeld: tooconnect tooa storage-account, u eerst maken een blob-opslag *verbinding*. toocreate een verbinding, geef referenties op Hallo u normaal gesproken tooaccess Hallo service u verbinding maakt. Voer dus Hallo referenties tooyour storage account toocreate Hallo verbinding met Azure storage. 

#### <a name="create-hello-connection"></a>Hallo verbinding maken
> [!INCLUDE [Create a connection tooAzure blob storage](../../includes/connectors-create-api-azureblobstorage.md)]

## <a name="use-a-trigger"></a>Een trigger te gebruiken
Deze connector heeft geen triggers bestaan niet. Gebruik andere triggers toostart Hallo logische app, zoals een trigger terugkeerpatroon, een HTTP-Webhook-trigger, triggers beschikbaar met andere connectors en meer. [Een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md) bevat een voorbeeld.

## <a name="use-an-action"></a>Gebruik een actie
Een actie is een bewerking uitgevoerd door Hallo werkstroom gedefinieerd in een logische app.

1. Selecteer Hallo plus -teken. Ziet u verschillende mogelijkheden: **een actie toevoegen**, **een voorwaarde toevoegen**, of een van de Hallo **meer** opties.
   
    ![](./media/connectors-create-api-azureblobstorage/add-action.png)
2. Kies **een actie toevoegen**.
3. Typ 'blob' tooget een lijst met alle beschikbare Hallo-acties in Hallo tekstvak.
   
    ![](./media/connectors-create-api-azureblobstorage/actions.png) 
4. Kies in ons voorbeeld **AzureBlob - metagegevens van bestand ophalen met behulp van pad**. Als er al een verbinding bestaat, selecteert u Hallo **...** (Objectkiezer tonen) knop tooselect een bestand.
   
    ![](./media/connectors-create-api-azureblobstorage/sample-file.png)
   
    Als u wordt gevraagd om de verbindingsgegevens hello, voert u Hallo details toocreate Hallo verbinding. [Hallo verbinding maken](connectors-create-api-azureblobstorage.md#create-the-connection) in dit onderwerp beschrijft deze eigenschappen. 
   
   > [!NOTE]
   > In dit voorbeeld ophalen we Hallo metagegevens van een bestand. toosee Hallo metagegevens, een andere actie die u maakt een nieuw bestand met een andere connector toevoegen. Bijvoorbeeld, een OneDrive-actie die u een nieuw bestand maakt 'test' op basis van metagegevens Hallo toevoegen. 


5. **Sla** uw wijzigingen (linksboven Hallo werkbalk). Uw logische app wordt opgeslagen en automatisch kan worden ingeschakeld.

> [!TIP]
> [Opslagverkenner](http://storageexplorer.com/) is een uitstekend hulpprogramma meerdere opslagaccounts te beheren.

## <a name="connector-specific-details"></a>Connector-specifieke details

Alle triggers en acties die zijn gedefinieerd in swagger Hallo bekijken en ook bekijken in Hallo beperkingen [connector details](/connectors/azureblobconnector/). 

## <a name="next-steps"></a>Volgende stappen
[Een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md). Verken Hallo van andere beschikbare connectors in Logic Apps op onze [API's lijst](apis-list.md).

