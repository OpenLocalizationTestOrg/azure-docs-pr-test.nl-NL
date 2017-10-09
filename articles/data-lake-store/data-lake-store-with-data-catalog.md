---
title: aaaRegister gegevens van Data Lake Store in Azure Data Catalog | Microsoft Docs
description: Registreert gegevens van Data Lake Store in Azure Data Catalog
services: data-lake-store,data-catalog
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 3294d91e-a723-41b5-9eca-ace0ee408a4b
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 3e895b42cab4ba39d288950763312a243883cbdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="register-data-from-data-lake-store-in-azure-data-catalog"></a>Registreert gegevens van Data Lake Store in Azure Data Catalog
In dit artikel leert u hoe toointegrate Azure Data Lake met Azure Data Catalog toomake uw gegevens opslaat in een organisatie kan worden gedetecteerd door integratie met Data Catalog. Zie voor meer informatie over de gegevens worden gecatalogiseerd, [Azure Data Catalog](../data-catalog/data-catalog-what-is-data-catalog.md). toounderstand scenario's waarin kunt u Data Catalog, Zie [algemene scenario's voor een Azure Data Catalog](../data-catalog/data-catalog-common-scenarios.md).

## <a name="prerequisites"></a>Vereisten
Voordat u deze zelfstudie begint, moet u de volgende Hallo hebben:

* **Een Azure-abonnement**. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).
* **Uw Azure-abonnement inschakelen** voor openbare Preview van Data Lake Store. Zie [Instructies](data-lake-store-get-started-portal.md).
* **Azure Data Lake Store-account**. Volg de instructies Hallo voor [aan de slag met Azure Data Lake Store met Azure Portal Hallo](data-lake-store-get-started-portal.md). Voor deze zelfstudie maken we een Data Lake Store-account genoemd **datacatalogstore**.

    Nadat u Hallo-account hebt gemaakt, uploadt u een voorbeeld gegevensset tooit. Voor deze zelfstudie laat het ons uploaden alle Hallo .csv-bestanden onder Hallo **AmbulanceData** map in Hallo [Azure Data Lake Git-opslagplaats](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/). U kunt verschillende clients, zoals [Azure Opslagverkenner](http://storageexplorer.com/), tooupload gegevens tooa blob-container.
* **Azure Data Catalog**. Uw organisatie moet een Azure Data Catalog gemaakt voor uw organisatie al hebben. Slechts één catalogus is toegestaan voor elke organisatie.

## <a name="register-data-lake-store-as-a-source-for-data-catalog"></a>Registratie Data Lake Store als bron voor Data Catalog

> [!VIDEO https://channel9.msdn.com/Series/AzureDataLake/ADCwithADL/player]

1. Ga te`https://azure.microsoft.com/services/data-catalog`, en klik op **aan de slag**.
2. Meld u aan bij hello Azure Data Catalog-portal en klikt u op **gegevens publiceren**.

    ![Een gegevensbron registreert](./media/data-lake-store-with-data-catalog/register-data-source.png "een gegevensbron registreren")
3. Klik op volgende pagina Hallo **toepassing starten**. Dit wordt Hallo application manifest-bestand op uw computer gedownload. Dubbelklik op Hallo manifestbestand toostart Hallo toepassing.
4. Klik op de welkomstpagina Hallo **aanmelden**, en voer uw referenties.

    ![Welkomstscherm](./media/data-lake-store-with-data-catalog/welcome.screen.png "welkomstscherm")
5. Selecteer op Hallo Selecteer een pagina van de gegevensbron, **Azure Data Lake**, en klik vervolgens op **volgende**.

    ![Selecteer gegevensbron](./media/data-lake-store-with-data-catalog/select-source.png "gegevensbron selecteren")
6. Geef op de volgende pagina Hallo, Hallo naam Data Lake Store-account dat u wilt dat tooregister in Data Catalog. Laat Hallo andere opties als standaard en klik vervolgens op **Connect**.

    ![Verbinding maken met toodata bron](./media/data-lake-store-with-data-catalog/connect-to-source.png "Connect toodata bron")
7. de volgende pagina Hallo kan worden onderverdeeld in Hallo segmenten te volgen.

    a. Hallo **serverhiërarchie** vak geeft Hallo Data Lake Store-account-mapstructuur. **$Root** vertegenwoordigt Hallo root van Data Lake Store-account, en **AmbulanceData** vertegenwoordigt Hallo map in de hoofdmap Hallo Hallo Data Lake Store-account hebt gemaakt.

    b. Hallo **beschikbare objecten** vak geeft een lijst van Hallo bestanden en mappen onder Hallo **AmbulanceData** map.

    c. **Objecten toobe geregistreerd vak** lijsten Hallo bestanden en mappen die u wilt dat tooregister in Azure Data Catalog.

    ![Bekijk gegevensstructuur](./media/data-lake-store-with-data-catalog/view-data-structure.png "gegevensstructuur weergeven")
8. U moet alle Hallo-bestanden in de map Hallo registreren voor deze zelfstudie. Die, klikt u op Hallo (![objecten verplaatsen](./media/data-lake-store-with-data-catalog/move-objects.png "objecten verplaatsen")) knop toomove alle Hallo bestanden te**objecten toobe geregistreerd** vak.

    Omdat het Hallo-gegevens worden geregistreerd in een catalogus met gegevens van de hele organisatie, is een aanbevolen benadering tooadd bepaalde metagegevens die u kunt later tooquickly Hallo gegevens plaatsen. U kunt bijvoorbeeld een e-mailadres voor Hallo gegevenseigenaar (bijvoorbeeld één die wordt uploaden van gegevens van de Hallo) toevoegen of een tag tooidentify Hallo gegevens toe te voegen. Hallo-schermafbeelding hieronder ziet u een label dat we toohello gegevens toevoegen.

    ![Bekijk gegevensstructuur](./media/data-lake-store-with-data-catalog/view-selected-data-structure.png "gegevensstructuur weergeven")

    Klik op **registreren**.
9. Hallo volgende schermopname geeft aan dat gegevens Hallo met succes is geregistreerd in Hallo Data Catalog.

    ![Inschrijving voltooid](./media/data-lake-store-with-data-catalog/registration-complete.png "gegevensstructuur weergeven")
10. Klik op **Portal weergeven** toogo back-toohello Data Catalog-portal en controleer of u kunt nu toegang Hallo gegevens vanuit de portal Hallo geregistreerd. toosearch hello gegevens, kunt u Hallo tag die u hebt gebruikt bij het registreren van Hallo-gegevens.

     ![Gegevens zoeken in de catalogus](./media/data-lake-store-with-data-catalog/search-data-in-catalog.png "gegevens zoeken in catalogus")
11. U kunt nu bewerkingen zoals het toevoegen van aantekeningen en documentatie toohello gegevens uitvoeren. Zie Hallo koppelingen volgen voor meer informatie.

    * [Aantekeningen toevoegen aan gegevensbronnen in de catalogus met gegevens](../data-catalog/data-catalog-how-to-annotate.md)
    * [Gegevensbronnen van document in Data Catalog](../data-catalog/data-catalog-how-to-documentation.md)

## <a name="see-also"></a>Zie ook
* [Aantekeningen toevoegen aan gegevensbronnen in de catalogus met gegevens](../data-catalog/data-catalog-how-to-annotate.md)
* [Gegevensbronnen van document in Data Catalog](../data-catalog/data-catalog-how-to-documentation.md)
* [Data Lake Store integreren met andere Azure-services](data-lake-store-integrate-with-other-services.md)
