---
title: aaaAnalyze gegevens in Data Lake Store met behulp van Power BI | Microsoft Docs
description: Gebruik Power BI tooanalyze opgeslagen gegevens in Azure Data Lake Store
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 57d19d27-e135-49d9-a7ea-46c48ef4e3bd
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 6a1bfa80fd1b0dda59b7eaaae9ca1585ba42783e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-data-in-data-lake-store-by-using-power-bi"></a>Gegevens in Data Lake Store te analyseren met Power BI
In dit artikel leert u hoe toouse Power BI Desktop tooanalyze en visualiseren van gegevens die zijn opgeslagen in Azure Data Lake Store.

## <a name="prerequisites"></a>Vereisten
Voordat u deze zelfstudie begint, moet u de volgende Hallo hebben:

* **Een Azure-abonnement**. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).
* **Azure Data Lake Store-account**. Volg de instructies Hallo voor [aan de slag met Azure Data Lake Store met Azure Portal Hallo](data-lake-store-get-started-portal.md). In dit artikel wordt ervan uitgegaan dat u hebt al een Data Lake Store-account genoemd gemaakt **mybidatalakestore**, en een voorbeeldbestand gegevens geüpload (**Drivers.txt**) tooit. Dit voorbeeldbestand is beschikbaar voor downloaden van [Azure Data Lake Git-opslagplaats](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).
* **Power BI Desktop**. U kunt dit downloaden van [Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=45331). 

## <a name="create-a-report-in-power-bi-desktop"></a>Een rapport maken in Power BI Desktop
1. Power BI Desktop op uw computer starten.
2. Van Hallo **Start** lint, klikt u op **gegevens ophalen**, en klik vervolgens op meer. In Hallo **gegevens ophalen** in het dialoogvenster, klikt u op **Azure**, klikt u op **Azure Data Lake Store**, en klik vervolgens op **Connect**.
   
    ![Verbinding maken met tooData Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account.png "Connect tooData Lake Store")
3. Als er een dialoogvenster over Hallo-connector wordt in een ontwikkelingsfase bevindt, ervoor kiezen de toocontinue.
4. In Hallo **Microsoft Azure Data Lake Store** in het dialoogvenster biedt Hallo URL tooyour Data Lake Store-account en klik vervolgens op **OK**.
   
    ![URL voor Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-url.png "URL voor Data Lake Store")
5. Klik in het volgende dialoogvenster hello, **aanmelden** toosign in Data Lake Store-account. U zult de aanmeldingspagina van de organisatie van de tooyour omgeleid. Ga als volgt Hallo prompts toosign Hallo rekening.
   
    ![Meld u aan bij de Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-signin.png "Meld u aan bij de Data Lake Store")
6. Nadat u bent aangemeld, klikt u op **Connect**.
   
    ![Verbinding maken met tooData Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-connect.png "Connect tooData Lake Store")
7. het volgende dialoogvenster Hallo toont Hallo-bestand dat u hebt geüpload tooyour Data Lake Store-account. Hallo info controleren en klik vervolgens op **Load**.
   
    ![Gegevens laden in Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-load.png "laden van gegevens uit Data Lake Store")
8. Nadat het Hallo gegevens zijn geladen in Power BI, ziet u de volgende velden in Hallo Hallo **velden** tabblad.
   
    ![Velden geïmporteerd](./media/data-lake-store-power-bi/imported-fields.png "velden geïmporteerd")
   
    Echter, toovisualize en Hallo gegevens analyseren, we liever Hallo gegevens toobe per Hallo na velden beschikbaar
   
    ![Velden gewenst](./media/data-lake-store-power-bi/desired-fields.png "gewenst velden")
   
    In de volgende stappen Hallo wordt Hallo query tooconvert Hallo geïmporteerd gegevens in de gewenste indeling hello bijgewerkt.
9. Van Hallo **Start** lint, klikt u op **query's bewerken**.
   
    ![Query's bewerken](./media/data-lake-store-power-bi/edit-queries.png "query's bewerken")
10. In Hallo Query-Editor, onder Hallo **inhoud** kolom, klikt u op **binaire**.
    
    ![Query's bewerken](./media/data-lake-store-power-bi/convert-query1.png "query's bewerken")
11. Ziet u een bestandspictogram, waarmee Hallo **Drivers.txt** -bestand dat u hebt geüpload. Met de rechtermuisknop op het Hallo-bestand en klik op **CSV**.    
    
    ![Query's bewerken](./media/data-lake-store-power-bi/convert-query2.png "query's bewerken")
12. U ziet een uitvoer zoals hieronder wordt weergegeven. Uw gegevens is nu beschikbaar in een indeling die u toocreate visualisaties kunt gebruiken.
    
    ![Query's bewerken](./media/data-lake-store-power-bi/convert-query3.png "query's bewerken")
13. Van Hallo **Start** lint, klikt u op **sluiten en toepassen**, en klik vervolgens op **sluiten en toepassen**.
    
    ![Query's bewerken](./media/data-lake-store-power-bi/load-edited-query.png "query's bewerken")
14. Zodra het Hallo-query wordt bijgewerkt, Hallo **velden** tabblad ziet Hallo nieuwe velden beschikbaar voor visualisatie.
    
    ![Bijgewerkte velden](./media/data-lake-store-power-bi/updated-query-fields.png "velden bijgewerkt")
15. Laat het ons maken een cirkeldiagram toorepresent Hallo stuurprogramma's in verschillende steden voor een bepaald land. toodo Zorg dus Hallo selecties te volgen.
    
    1. Klik in het Hallo visualisaties tabblad Hallo symbool voor een cirkeldiagram.
       
        ![Maken van het cirkeldiagram](./media/data-lake-store-power-bi/create-pie-chart.png "cirkeldiagram maken")
    2. Hallo-kolommen die we gaan toouse zijn **kolom 4** (naam van Hallo stad) en **kolom 7** (naam van Hallo land). Sleep deze kolommen uit **velden** tabblad te**visualisaties** tabblad zoals hieronder wordt weergegeven.
       
        ![Maak visualisaties](./media/data-lake-store-power-bi/create-visualizations.png "visualisaties maken")
    3. Hallo-cirkeldiagram ziet er nu zoals Hallo voorbeeld hieronder.
       
        ![Cirkeldiagram](./media/data-lake-store-power-bi/pie-chart.png "visualisaties maken")
16. Als u een bepaald land van niveau paginafilters Hallo selecteert, nu ziet u Hallo aantal stuurprogramma's in elke stad van Hallo geselecteerd land. Bijvoorbeeld onder Hallo **visualisaties** tabblad onder **niveau filters pagina**, selecteer **Brazilië**.
    
    ![Selecteer een land](./media/data-lake-store-power-bi/select-country.png "land selecteren")
17. Hallo-cirkeldiagram wordt automatisch bijgewerkt toodisplay Hallo stuurprogramma's in de steden van Brazilië Hallo.
    
    ![Stuurprogramma's in een land](./media/data-lake-store-power-bi/driver-per-country.png "stuurprogramma's per land")
18. Van Hallo **bestand** menu, klikt u op **opslaan** toosave Hallo visualisatie als Power BI Desktop-bestand.

## <a name="publish-report-toopower-bi-service"></a>Rapport tooPower BI-service publiceren
Zodra u Hallo visualisaties in Power BI Desktop hebt gemaakt, kunt u het delen met anderen door deze te publiceren toohello Power BI-service. Voor instructies over het toodo die Zie [publiceren vanuit Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-upload-desktop-files/).

## <a name="see-also"></a>Zie ook
* [Gegevens analyseren in Data Lake Store met Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md)

