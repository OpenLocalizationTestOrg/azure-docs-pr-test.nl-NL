---
title: aaaCreating webservice-eindpunten in Machine Learning | Microsoft Docs
description: Webservice-eindpunten maken in Azure Machine Learning
services: machine-learning
documentationcenter: 
author: hiteshmadan
manager: padou
editor: cgronlun
ms.assetid: 4657fc1b-5228-4950-a29e-bc709259f728
ms.service: machine-learning
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 10/04/2016
ms.author: himad
ms.openlocfilehash: 10a2bc586c6fe35e28d8bf0293854c578827c453
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-endpoints"></a>Eindpunten maken
> [!NOTE]
>  Dit onderwerp wordt beschreven technieken toepasselijke tooa **klassieke** Machine Learning-webservice.
> 
> 

Wanneer u webservices die u doorsturen tooyour klanten verkoopt maakt, moet u tooprovide getraind modellen tooeach klant die nog steeds gekoppelde toohello experiment uit welke Hallo Web service is gemaakt. Bovendien geen updates toohello experiment moet worden toegepast selectief tooan eindpunt zonder Hallo aanpassingen wordt overschreven.

tooaccomplish, kunt u in Azure Machine Learning toocreate meerdere eindpunten voor een geïmplementeerde webservice. Elk eindpunt in Hallo-webservice is onafhankelijk geadresseerd, beperkt en beheerd. Elk eindpunt is een unieke URL's en autorisatie sleutel tooyour klanten kunt distribueren.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="adding-endpoints-tooa-web-service"></a>Toevoegen van eindpunten tooa-webservice
Er zijn drie manieren tooadd een eindpunt tooa webservice.

* Programmatisch
* Via hello Azure Machine Learning-webservices-portal
* Hoewel Hallo klassieke Azure-portal

Zodra het Hallo-eindpunt is gemaakt, kunt u deze via synchrone API's, batch-API's, gebruiken en excel-werkbladen. Bovendien tooadding eindpunten via deze gebruikersinterface, u kunt ook Hallo eindpunt Management-API's tooprogrammatically toevoegen van eindpunten.

> [!NOTE]
> Als u extra eindpunten toohello webservice hebt toegevoegd, kunt u het standaardeindpunt Hallo niet verwijderen.
> 
> 

## <a name="adding-an-endpoint-programmatically"></a>Een eindpunt toevoegen programmatisch
U kunt een eindpunt tooyour webservice programmatisch met behulp van Hallo toevoegen [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) voorbeeldcode.

## <a name="adding-an-endpoint-using-hello-azure-machine-learning-web-services-portal"></a>Toevoegen van een eindpunt met hello Azure Machine Learning-webservices-portal
1. Klik op Web-Services op Hallo linkernavigatievenster kolom in Machine Learning Studio.
2. Aan de onderkant van de Hallo van Hallo Web servicedashboard, klikt u op **eindpunten beheren**. Hello Azure Machine Learning-webservices portal opent toohello eindpunten pagina voor het Hallo-webservice.
3. Klik op **Nieuw**.
4. Typ een naam en beschrijving voor het nieuwe eindpunt Hallo. Namen van eindpunten moeten 24 tekens of minder lang zijn en moeten bestaan uit kleine letters of cijfers. Selecteer het logboekregistratieniveau Hallo en of voorbeeldgegevens is ingeschakeld. Zie voor meer informatie over logboekregistratie [inschakelen van logboekregistratie voor Machine Learning-webservices](machine-learning-web-services-logging.md).

## <a name="adding-an-endpoint-using-hello-azure-classic-portal"></a>Toevoegen van een eindpunt met behulp van Hallo klassieke Azure-portal
1. Meld u aan toohello [klassieke Azure-portal](http://manage.windowsazure.com), klikt u op **Machine Learning** in de linkerkolom Hallo. Klik op Hallo werkruimte waarin Hallo webservice waarin u geïnteresseerd bent.
   
    ![Navigeer tooworkspace](./media/machine-learning-create-endpoint/figure-1.png)
2. Klik op **webservices**.
   
    ![Navigeer tooWeb services](./media/machine-learning-create-endpoint/figure-2.png)
3. Klik op Hallo webservice u geïnteresseerd bent in toosee Hallo lijst met beschikbare eindpunten.
   
    ![Navigeer tooendpoint](./media/machine-learning-create-endpoint/figure-3.png)
4. Klik onder aan de pagina Hallo Hallo op **eindpunt toevoegen**. Typ een naam en beschrijving, zorg ervoor dat er zijn geen andere eindpunten met dezelfde naam in deze webservice Hallo. Tenzij u speciale vereisten hebt, laat u Hallo versnelling niveau met de standaardwaarde. toolearn meer informatie over beperking, Zie [API-eindpunten schalen](machine-learning-scaling-webservice.md).
   
    ![Eindpunt maken](./media/machine-learning-create-endpoint/figure-4.png)

## <a name="next-steps"></a>Volgende stappen
[Hoe een Azure Machine Learning-webservice tooconsume](machine-learning-consume-web-services.md).

