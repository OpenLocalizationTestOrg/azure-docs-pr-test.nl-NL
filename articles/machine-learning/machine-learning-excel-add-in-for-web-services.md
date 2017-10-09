---
title: aaaExcel-invoegtoepassing voor Machine Learning-webservices | Microsoft Docs
description: Hoe toouse Azure Machine Learning Web services rechtstreeks in Excel zonder een code te schrijven.
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 9618079d-502f-4974-a3e2-8f924042a23f
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/14/2017
ms.author: tedway;garye
ms.openlocfilehash: c52f40d33c9907f284e4750afe47181dc3365fe5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="excel-add-in-for-azure-machine-learning-web-services"></a>Excel-invoegtoepassing voor Azure Machine Learning-webservices
Excel kunt u eenvoudig toocall webservices rechtstreeks zonder Hallo moet toowrite code.

## <a name="steps-toouse-an-existing-web-service-in-hello-workbook"></a>Stappen tooUse een bestaande webservice in Hallo werkmap

1. Open Hallo [voorbeeld-Excel-bestand](http://aka.ms/amlexcel-sample-2), die bevat Hallo Excel-invoegtoepassing en gegevens over passagiers op Hallo Titanic.
2. Hallo-webservice kiezen door erop te klikken-' Titanic nagelaten manier (Excel-invoegtoepassing voorbeeld) [Score] ' in dit voorbeeld.
   
    ![-Webservice selecteren][01]
3. Hiermee gaat u toohello **Predict** sectie.  Deze werkmap bevat al de voorbeeldgegevens, maar voor een lege werkmap kunt u Selecteer een cel in Excel en klik op **voorbeeldgegevens**.
4. Hallo-gegevens met kopteksten selecteren en klik op Hallo invoergegevens bereik pictogram.  Zorg ervoor dat Hallo 'Mijn gegevens heeft headers' selectievakje is ingeschakeld.
5. Onder **uitvoer**, Voer Hallo cel getal waar u hier uitvoer toobe, bijvoorbeeld 'H1' Hallo.
6. Klik op **voorspellen**.
   
    ![Sectie voorspellen][02]

Implementeer een webservice of een bestaande webservice gebruiken. Zie voor meer informatie over het implementeren van een webservice [scenario stap 5: hello Azure Machine Learning-webservice implementeren](machine-learning-walkthrough-5-publish-web-service.md).

Hallo-API-sleutel voor uw webservice ophalen. Wanneer u uitvoeren met deze actie is afhankelijk van of u een klassieke Machine Learning-webservice van een nieuwe Machine-Learning-webservice gepubliceerd.

**Een klassieke webservice gebruiken** 

1. Klik op Hallo in Machine Learning Studio **WEBSERVICES** sectie in het linkerdeelvenster Hallo en selecteer vervolgens Hallo-webservice.
   
    ![Studio, selecteer een webservice][04]
2. Kopieer Hallo API-sleutel voor Hallo-webservice.
   
    ![Studio-API-sleutel][05]
3. Op Hallo **DASHBOARD** voor Hallo-webservice en klik op Hallo **aanvragen/reacties** koppeling.
4. Zoek naar Hallo **aanvraag-URI** sectie.  Kopieer en sla Hallo-URL.

> [!NOTE]
> Het is nu mogelijk toosign in Hallo [Azure Machine Learning-webservices](https://services.azureml.net) portal tooobtain Hallo API-sleutel voor een klassieke Machine Learning-webservice.
> 
> 

**Een nieuwe webservice gebruiken**

1. In Hallo [Azure Machine Learning-webservices](https://services.azureml.net) en klik op **webservices**, selecteer vervolgens uw webservice. 
2. Klik op **verbruiken**.
3. Zoek naar Hallo **Basic verbruik info** sectie. Kopiëren en opslaan van Hallo **primaire sleutel** en Hallo **aanvragen en antwoorden** URL.

## <a name="steps-tooadd-a-new-web-service"></a>TooAdd stappen een nieuwe webservice

1. Implementeer een webservice of een bestaande webservice gebruiken. Zie voor meer informatie over het implementeren van een webservice [scenario stap 5: hello Azure Machine Learning-webservice implementeren](machine-learning-walkthrough-5-publish-web-service.md).
2. Klik op **verbruiken**.
3. Zoek naar Hallo **Basic verbruik info** sectie. Kopiëren en opslaan van Hallo **primaire sleutel** en Hallo **aanvragen en antwoorden** URL.
4. Ga in Excel, toohello **webservices** sectie (als u in Hallo **Predict** sectie, klikt u op Hallo pijl naar links toogo toohello lijst met web-services).
   
    ![Ga tooWeb service selecteren][03]
5. Klik op **-webservice toevoegen**.
6. Plak Hallo-URL in Excel-invoegtoepassing tekstvak met het label Hallo **URL**.
7. Plakken Hallo API/primaire sleutel in Hallo tekstvak met het label **API-sleutel**.
8. Klik op **Add**.
   
    ![URL en API-sleutel voor een klassieke webservice.][06]
9. toouse hello webservice Hallo voorafgaand aan de instructies volgen, "Stappen voor het tooUse een bestaande web Service."

## <a name="sharing-your-workbook"></a>Delen van uw werkmap
Als u de werkmap opslaan, wordt ook Hallo API/primaire sleutel voor het Hallo-webservices die u hebt toegevoegd opgeslagen. Dit betekent dat u moet Hallo werkmap alleen delen met personen die u vertrouwt.

Vragen te stellen in Hallo volgende sectie Opmerking of op onze [forum](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).

[01]: ./media/machine-learning-excel-add-in-for-web-services/image1.png
[02]: ./media/machine-learning-excel-add-in-for-web-services/image2.png
[03]: ./media/machine-learning-excel-add-in-for-web-services/image3.png
[04]: ./media/machine-learning-excel-add-in-for-web-services/image4.png
[05]: ./media/machine-learning-excel-add-in-for-web-services/image5.png
[06]: ./media/machine-learning-excel-add-in-for-web-services/image6.png
