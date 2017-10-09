---
title: aaaGet slag met Azure Data Lake Analytics met Azure portal | Microsoft Docs
description: 'Informatie over hoe toouse hello Azure portal toocreate een Data Lake Analytics-account maken van een Data Lake Analytics-taak met U-SQL, en het Hallo-taak verzenden. '
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: b1584d16-e0d2-4019-ad1f-f04be8c5b430
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/21/2017
ms.author: edmaca
ms.openlocfilehash: 6bb54404fa42cfed25b18bc2bfb7c72e6c361149
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-portal"></a>Aan de slag met Azure Data Lake Analytics met Azure Portal
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

Meer informatie over hoe toouse hello Azure portal toocreate Azure Data Lake Analytics-accounts, het definiëren van taken in [U-SQL](data-lake-analytics-u-sql-get-started.md), en het verzenden van taken toohello Data Lake Analytics-service. Zie [Overzicht van Azure Data Lake Analytics](data-lake-analytics-overview.md) voor meer informatie over Data Lake Analytics.

## <a name="prerequisites"></a>Vereisten

Voordat u met deze zelfstudie begint, moet u een **Azure-abonnement** hebben. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).

## <a name="create-a-data-lake-analytics-account"></a>Een Data Lake Analytics-account maken

Nu u een Data Lake Analytics maakt en een Data Lake Store-account op Hallo dezelfde tijd.  Deze stap is eenvoudig en alleen toofinish 60 seconden duurt.

1. Meld u aan bij toohello [Azure-portal](https://portal.azure.com).
2. Klik op **Nieuw** >  **Gegevens + analyse** > **Data Lake Analytics**.
3. Waarden selecteren voor Hallo volgende items:
   * **Naam**: geef uw Data Lake Analytics-account een naam (alleen kleine letters en cijfers zijn toegestaan).
   * **Abonnement**: Kies hello Azure-abonnement gebruikt voor Hallo Analytics-account.
   * **Resourcegroep**. Selecteer een bestaande Azure-resourcegroep of maak een nieuwe.
   * **Locatie**. Selecteer een Azure-Datacenter voor Hallo Data Lake Analytics-account.
   * **Data Lake Store**: Volg Hallo instructie toocreate een nieuw Data Lake Store-account of een bestaande set selecteren. 
4. U kunt ervoor kiezen om een prijscategorie te selecteren voor uw Data Lake Analytics-account.
5. Klik op **Create**. 


## <a name="your-first-u-sql-script"></a>Uw eerste U-SQL-script

na de tekst Hello is een zeer eenvoudige U-SQL-script. Deze methode wordt een kleine gegevensset binnen Hallo script definiëren en vervolgens deze gegevensset uit toohello default Data Lake Store niet schrijven als een bestand met de naam `/data.csv`.

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
```

## <a name="submit-a-u-sql-job"></a>Een U-SQL-taak verzenden

1. Hallo Data Lake Analytics-account, klik op **nieuwe taak**.
2. U-SQL-script hierboven weergegeven in de tekst hello Hallo plakken. 
3. Klik op **Taak verzenden**.   
4. Wachten tot Hallo taakstatuswijzigingen te**geslaagd**.
5. Als het Hallo-taak is mislukt, raadpleegt u [Monitor en Data Lake Analytics-taken oplossen](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).
6. Klik op Hallo **uitvoer** tabblad en klik vervolgens op `data.csv`. 

## <a name="see-also"></a>Zie ook

* tooget gestart met het ontwikkelen van U-SQL-toepassingen, Zie [U-SQL-scripts ontwikkelen met Data Lake Tools voor Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).
* toolearn U-SQL, Zie [aan de slag met Azure Data Lake Analytics U-SQL-taal](data-lake-analytics-u-sql-get-started.md).
* Zie [Azure Data Lake Analytics beheren met Azure Portal](data-lake-analytics-manage-use-portal.md) voor informatie over beheertaken.
