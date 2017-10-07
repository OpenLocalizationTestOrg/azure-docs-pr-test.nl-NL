---
title: aaaUpload bestanden naar een Azure Media Services-account met behulp van Aspera | Microsoft Docs
description: Deze zelfstudie wordt u begeleid Hallo stappen voor het uploaden van bestanden in een opslagaccount dat is gekoppeld aan een Media Services-account met behulp van Hallo ** Aspera Server op aanvraag **-service op Azure.
services: media-services
documentationcenter: 
author: johndeu
manager: cfowler
editor: 
ms.assetid: 8812623a-b425-4a0f-9e05-0ee6c839b6f9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/17/2017
ms.author: juliako
ms.openlocfilehash: 7213f016cc1b7f262b14db7b39b478a03970d1c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-hello-aspera-server-on-demand-service-on-azure"></a>Bestanden uploaden naar een Media Services-account met Hallo Aspera Server On Demand-service op Azure

## <a name="overview"></a>Overzicht

**Aspera** is software die een snelle bestandsoverdracht mogelijk maakt. **Aspera Server On Demand** voor Azure maakt snel uploaden en downloaden van grote bestanden rechtstreeks in Azure Blob-objectopslag mogelijk. Voor informatie over **Aspera On Demand**, Zie Hallo [Aspera Cloud](http://cloud.asperasoft.com/) site. 
  
**Aspera Server On Demand** voor Azure gekocht bij Hallo is [Azure marketplace](https://azure.microsoft.com/en-us/marketplace/). In volgorde toocomplete een aankoop van **Aspera Server On Demand** voor Azure, meld u in Azure Marketplace met uw Windows Live ID.

Deze zelfstudie wordt u begeleid Hallo stappen voor het uploaden van bestanden in een opslagaccount dat is gekoppeld aan een Media Services-account met behulp van Hallo **Aspera Server On Demand** service op Azure. 

U vindt een voorbeeld ziet u hoe toouse Azure werkt met Aspera en Media Services [hier](https://github.com/Azure-Samples/media-services-dotnet-functions-integration/tree/master/103-aspera-ingest).

>[!NOTE]
>Er is een limiet toohello maximale bestandsgrootte ondersteund voor de verwerking met Azure Media Services-mediaprocessoren (Management Packs). Zie [dit](media-services-quotas-and-limitations.md) onderwerp voor meer informatie over Hallo beperking voor de bestandsgrootte.
>

## <a name="prerequisites"></a>Vereisten 

toocomplete deze zelfstudie hebt u nodig:

* Een Windows Live ID
* Een [Azure-account](https://azure.microsoft.com). Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie. 
* Een [Azure Media Services-account](media-services-portal-create-account.md).

## <a name="purchase-aspera-on-demand-for-azure"></a>Aspera On Demand kopen voor Azure

Zodra u hebt geregistreerd in Azure Marketplace, volgt u deze basisstappen toocomplete uw aanschaf van Aspera On Demand voor Azure.

1. Zoek naar Aspera en selecteer 'Server On Demand'.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera001.png)

2. Hallo-abonnementen en klik op Sign Up

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera002.png)

3. Vul in het Hallo-specifieke informatie voor uw Server op verzoek-abonnement.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera003.png)

4. Klik op Hallo **prijscategorie** in en selecteer de gewenste maandelijkse volume Hallo sub Configuratiescherm. In Hallo **plannen details** Configuratiescherm, selecteer **OK**. Klik op Hallo **Kies uw prijscategorie** -scherm, klikt u op **Selecteer**.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera004.png)

5. Klik op **juridische voorwaarden** tooview en accepteer de juridische bepalingen Hallo Hallo sub Configuratiescherm. Nadat u de juridische voorwaarden Hallo hebt bekeken, klikt u op **aankoop**.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera005.png)

6. Hallo aankoop voltooien door te klikken op **maken**.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera006.png)

7. Hello Azure-dashboard wordt aangekondigd dat het Hallo-service is ingericht.  Zodra deze is voltooid met het leveren, kunt u Hallo nieuw abonnement vinden door te zoeken in uw resources voor Hallo-naam van het Hallo-service. Als u Hallo-service, dubbele klik erop toolaunch Hallo service management-portal gevonden hebt.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera007.png)

8. Start Hallo Aspera-beheerportal. Als u uw nieuwe Aspera-service hebt gevonden, krijgt u toegang toohello-beheerportal door te klikken op Hallo-service.  Er wordt een nieuw deelvenster geopend. Uit binnen die nieuw deelvenster, moet u tooclick op Hallo **resourcenaam** van uw nieuwe service.  In Hallo schermafbeelding te volgen, is het Hallo-resourcenaam 'AsperaTransferDemo'. Zodra u op Hallo Resourcenaam klikt, wordt een ander deelvenster wordt gestart. In het nieuwe deelvenster ziet u een koppeling 'Beheren'. Klik op Hallo 'Beheren' koppeling toolaunch hello Aspera-beheerportal.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera008.png)

9. Door te klikken op Hallo beheren koppeling, krijgt u de registratiepagina toohello, die vereist is tooaccess Hallo service.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera009.png)

10. U hebt nu toegang toohello Aspera service management-portal, kunt u toegangstoetsen maken, downloaden clients Aspera en licenties, adresgebruik weergeven en meer informatie over Hallo API's.

    Hallo toont volgende schermafbeelding Hallo toegang maken. 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera010.png)

    Hallo toont volgende schermafbeelding Hallo gebruiksrapportage-interfaces in Hallo-portal. 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera011.png)

## <a name="upload-files-with-aspera"></a>Bestanden uploaden met Aspera

1. Download en installeer Hallo Aspera clientsoftware:
    
    * [Invoegtoepassing browser](http://downloads.asperasoft.com/connect2/)
    * [Rich client](http://downloads.asperasoft.com/en/downloads/2)

2. Voer uw eerste overdracht uit. In de volgorde toouse hello Aspera client tootransfer Hello Aspera transfer-service moet u toocomplete Hallo volgende: 

    1. Maak een toegangssleutel met Hallo Aspera portal.  
    2. Downloaden, installeren en licentie Hallo Aspera client (software kunt u vinden in Hallo Aspera portal).  

    >[!NOTE]
    >Lees Hallo Aspera client-handleiding voor configuratie-informatie.
    
    3. Sommige gegevens van uw opslagaccount die is gekoppeld aan uw Azure-Media-Account met Hallo ophalen [Azure-portal](https://portal.azure.com/). In het bijzonder naam en sleutel en naam Hallo opslag blob-container in toowhich gewenste tooplace uw inhoud. 

        * tooget hello opslag info van Hallo-portal: vinden uw storage-account, klikt u op Hallo toegangstoetsen en kopiëren Hallo naam en het Hallo-sleutel van uw account.
        * tooget hello containernaam: vinden van uw opslagaccount, selecteer **Blobs**, selecteer Hallo-naam van Hallo-container die u wilt dat tooupload Hallo inhoud in. 

    Hieronder vindt u Hallo schermopname van Hallo Aspera client **Verbindingsbeheer** waarin u de 'Azure' opslagtype Hallo en referenties, evenals Hallo blob-container moet opgeven.

    ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera012.png)

## <a name="resources"></a>Resources

Hallo volgende resources zijn vermeld in dit artikel. 

* [Connect Browser Plugin](http://downloads.asperasoft.com/connect2/)
* [Connect-handleiding](http://downloads.asperasoft.com/en/documentation/8)
* [Aspera-client](http://downloads.asperasoft.com/en/downloads/2)
* [Clienthandleiding](http://downloads.asperasoft.com/en/documentation/2)

## <a name="next-steps"></a>Volgende stappen

U kunt nu [blobs vanuit een opslagaccount kopiëren naar een AMS-account](media-services-copying-existing-blob.md#copy-blobs-from-a-storage-account-into-an-ams-account).

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

