---
title: AAA(deprecated) publiceren machine learning web service tooAzure Marketplace | Microsoft Docs
description: (afgeschaft) Hoe toopublish uw Azure Machine Learning-webservice toohello Azure Marketplace
services: machine-learning
documentationcenter: 
author: BharathS
manager: jhubbard
editor: cgronlun
ms.assetid: 68e908be-3a99-4cd7-9517-e2b5f2f341b8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: bharaths
ROBOTS: NOINDEX
redirect_url: machine-learning-gallery-experiments
redirect_document_id: True
ms.openlocfilehash: 149abc3df9b79c1b37d233d5e85e803592ff1020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-publish-azure-machine-learning-web-service-toohello-azure-marketplace"></a>(afgeschaft) Azure Machine Learning-webservice toohello Azure Marketplace publiceren

> [!NOTE]
> DataMarket en Data Services worden gesteld en bestaande abonnementen wordt buiten gebruik worden gesteld en geannuleerd vanaf 3/31/2017. Als gevolg hiervan wordt in dit artikel afgeschaft. 
> 
> Als alternatief kunt u uw Machine Learning-experimenten toohello kunt publiceren [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) voor Hallo voordeel van het Hallo gegevens wetenschappelijke community. Zie voor meer informatie [Share en het detecteren van bronnen in Hallo Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).

Hello Azure Marketplace biedt de mogelijkheid Hallo betaald toopublish Azure Machine Learning-webservices of gratis services voor verbruik door externe klanten. Dit artikel bevat een overzicht van het proces met koppelingen tooguidelines tooget die u gestart. Met behulp van dit proces kunt u uw webservices beschikbaar voor andere ontwikkelaars tooconsume in hun toepassingen.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview-of-hello-publishing-process"></a>Overzicht van Hallo publicatieproces
Hallo volgen Hallo stappen voor het publiceren van een Azure Machine Learning web service tooAzure Marketplace:

1. Maken en publiceren van een Machine Learning-reactie op aanvragen-service (RR's)
2. Hallo service tooproduction implementeren en Hallo API-sleutel en OData-eindpuntinformatie verkrijgen.
3. Gebruik Hallo URL Hallo gepubliceerde web service toopublish te[Azure Marketplace (markt gegevens)](https://publish.windowsazure.com/workspace/) 
4. Zodra ingediend, uw aanbieding wordt gecontroleerd en toobe goedgekeurd voordat uw klanten kunt met het aanschaffen beginnen moet. Hallo-publicatieproces kan enkele dagen duren. 

## <a name="walk-through"></a>Overzicht
### <a name="step-1-create-and-publish-a-machine-learning-request-response-service-rrs"></a>Stap 1: Maken en publiceren van een Machine Learning-reactie op aanvragen-service (RR's)
 Als u nog niet hebt gedaan dit, bekijk dan deze [doorlopen](machine-learning-walkthrough-5-publish-web-service.md).

### <a name="step-2-deploy-hello-service-tooproduction-and-obtain-hello-api-key-and-odata-endpoint-information"></a>Stap 2: Hallo service tooproduction implementeren en Hallo API-sleutel en OData-eindpuntinformatie verkrijgen
1. Van Hallo [klassieke Azure-Portal](http://manage.windowsazure.com), selecteer Hallo **MACHINE LEARNING** optie van de linkernavigatiebalk Hallo en selecteer uw werkruimte. 
2. Klik op Hallo **WEBSERVICES** tabblad en selecteer Hallo webservice gewenst toopublish toohello marketplace.
   
    ![Azure Marketplace][workspace]
3. Selecteer Hallo eindpunt die u zou zoals toohave Hallo marketplace verbruiken. Als u geen extra eindpunten niet hebt gemaakt, kunt u Hallo **standaard** eindpunt.
4. Zodra u hebt geklikt op Hallo eindpunt, kunt u zich kunt toosee hello **API-sleutel**. U moet dit stuk informatie later in stap 3, dus maak een kopie van deze.
   
    ![Azure Marketplace][apikey]
5. Klik op Hallo **aanvragen/reacties** methode op dit punt wordt niet ondersteund publishing Batchuitvoering services toohello marketplace. Die u gaat toohello API help-pagina voor Hallo aanvraag/antwoord-methode.
6. Kopiëren Hallo **adres van de OData-eindpunt**, moet u deze informatie later in stap 3.
   
    ![Azure Marketplace][odata]

Hallo service implementeren in productie.

### <a name="step-3-use-hello-url-of-hello-published-web-service-toopublish-tooazure-marketplace-datamarket"></a>Stap 3: Gebruik Hallo URL Hallo gepubliceerde web service toopublish tooAzure Marketplace (DataMarket)
1. Navigeer te[Azure Marketplace (markt gegevens)](http://datamarket.azure.com/home) 
2. Klik op Hallo **publiceren** koppeling bovenaan Hallo Hallo pagina. Hiermee gaat u toohello [Microsoft Azure Publishing Portal](https://publish.windowsazure.com)
3. Klik op Hallo **uitgevers** sectie tooregister als een publisher.
4. Wanneer u een nieuwe aanbieding maakt, selecteert u **Data Services**, klikt u vervolgens op **maken van een nieuwe gegevensservice**. 
   
   ![Azure Marketplace][image1]
   
   <br />
5. Onder **plannen** bieden informatie over uw oplossing, inclusief een prijsstelling. Bepaal als u een gratis of betaalde service biedt. tooget betaald, bieden betalingsinformatie zoals uw bank en de btw-gegevens.
6. Onder **Marketing** bevatten informatie over uw aanbieding, zoals Hallo titel en beschrijving voor uw aanbieding.
7. Onder **prijzen** Hallo prijs ingesteld voor uw plannen voor specifieke landen of laat Hallo systeem 'autoprice' uw aanbieding.
8. Op Hallo **gegevensservice** tabblad **webservice** als Hallo **gegevensbron**.
   
    ![Azure Marketplace][image2]
9. Hallo web service-URL en API-sleutel ophalen van Hallo klassieke Azure-Portal, zoals beschreven in stap 2 hierboven.
10. Hallo Marketplace Data Service-instelling in het dialoogvenster Plakken Hallo OData-eindpuntadres Hallo **Service-URL** in het tekstvak.
11. Voor **verificatie**, kies **Header** als Hallo **verificatieschema**.
    
    * Voer 'Verificatie' voor Hallo **headernaam**.
    * Voor Hallo **headerwaarde**, Voer u 'Bearer' (zonder aanhalingstekens Hallo), klik op Hallo **ruimte** balk en plak Hallo API-sleutel.
    * Selecteer Hallo **deze Service is OData** selectievakje.
    * Klik op **testverbinding** tootest Hallo verbinding.
12. Onder **categorieën**, zorg ervoor dat **Machine Learning** is geselecteerd.
13. Wanneer u klaar bent, voeren alle Hallo metagegevens over uw aanbieding, klikt u op **publiceren**, en vervolgens **tooStaging Push**. Op dit moment wordt u gewaarschuwd voor overige problemen moet u toofix.
14. Nadat u ervoor gezorgd alle Hallo openstaande problemen is voltooid dat hebt, klikt u op **aanvragen van goedkeuring toopush tooProduction**. Hallo-publicatieproces kan enkele dagen duren. 

[image1]:./media/machine-learning-publish-web-service-to-azure-marketplace/image1.png
[image2]:./media/machine-learning-publish-web-service-to-azure-marketplace/image2.png
[workspace]:./media/machine-learning-publish-web-service-to-azure-marketplace/selectworkspace.png
[apikey]:./media/machine-learning-publish-web-service-to-azure-marketplace/apikey.png
[odata]:./media/machine-learning-publish-web-service-to-azure-marketplace/odata.png

