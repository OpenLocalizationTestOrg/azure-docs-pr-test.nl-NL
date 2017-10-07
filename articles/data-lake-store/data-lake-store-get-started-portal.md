---
title: Azure portal tooget aaaUse gestart met Data Lake Store | Microsoft Docs
description: Gebruik hello Azure portal toocreate een Data Lake Store-account en uitvoeren van basisbewerkingen in Data Lake Store Hallo
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: fea324d0-ad1a-4150-81f0-8682ddb4591c
ms.service: data-lake-store
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/06/2017
ms.author: nitinme
ms.openlocfilehash: 6bb3413f00bfa4393f08aed18bc1d5f8a2f28fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-hello-azure-portal"></a>Aan de slag met Azure Data Lake Store met hello Azure-portal
> [!div class="op_single_selector"]
> * [Portal](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [.NET-SDK](data-lake-store-get-started-net-sdk.md)
> * [Java-SDK](data-lake-store-get-started-java-sdk.md)
> * [REST API](data-lake-store-get-started-rest-api.md)
> * [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
> 

Meer informatie over hoe toouse Hallo toocreate met Azure portal een Azure Data Lake Store-account en basisbewerkingen uitvoert, zoals maken van mappen, uploaden en downloaden van gegevensbestanden, verwijderen van uw account, enzovoort. Zie [Overzicht van Azure Data Lake Store](data-lake-store-overview.md) voor meer informatie.

Hallo na twee video's bevatten Hallo dezelfde informatie, zoals beschreven in dit artikel:

* [Een Data Lake Store-account maken](https://mix.office.com/watch/1k1cycy4l4gen)
* [Beheren van gegevens in Data Lake Store met Hallo Data Explorer](https://mix.office.com/watch/icletrxrh6pc)

## <a name="prerequisites"></a>Vereisten
Voordat u deze zelfstudie begint, moet u de volgende items Hallo hebben:

* **Een Azure-abonnement**. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).

## <a name="create-an-azure-data-lake-store-account"></a>Een Azure Data Lake Store-account maken

1. Meld u aan bij de nieuwe toohello [Azure-portal](https://portal.azure.com).
2. Klik op **Nieuw**, klik op **Gegevens en opslag** en klik vervolgens op **Azure Data Lake Store**. Lees de informatie Hallo in Hallo **Azure Data Lake Store** blade en klik vervolgens op **maken** in de linkeronderhoek van Hallo blade Hallo.
3. In Hallo **nieuwe Data Lake Store** blade Hallo waarden opgeven, zoals wordt weergegeven in de volgende schermafbeelding Hallo:
   
    ![Een nieuw Azure Data Lake Store-account maken](./media/data-lake-store-get-started-portal/ADL.Create.New.Account.png "Een nieuw Azure Data Lake Store-account maken")
   
   * **Naam**. Voer een unieke naam voor Hallo Data Lake Store-account.
   * **Abonnement**. Hallo-abonnement waarmee u wilt dat toocreate een nieuw Data Lake Store-account selecteren.
   * **Resourcegroep**. Selecteer een bestaande resourcegroep of selecteer Hallo **nieuw** optie toocreate een. Een resourcegroep is een container met verwante resources voor een toepassing. Zie [Resourcegroepen in Azure](../azure-resource-manager/resource-group-overview.md#resource-groups) voor meer informatie.
   * **Locatie**: Selecteer een locatie waar u toocreate Hallo Data Lake Store-account.
   * **Versleutelingsinstellingen**. Er zijn drie opties:
     
     * **Geen versleuteling inschakelen**.
     * **Sleutels gebruiken die worden beheerd door Azure Data Lake**.  Als u wilt dat Azure Data Lake Store toomanage uw versleutelingssleutels.
     * **Sleutels kiezen in Azure Key Vault**. U kunt een bestaande Azure Key Vault selecteren of een nieuwe Key Vault maken. toouse hello sleutels uit een Sleutelkluis, moet u machtigingen voor hello Azure Data Lake Store-account tooaccess hello Azure Key Vault toewijzen. Zie voor instructies Hallo [toewijzen machtigingen tooAzure Sleutelkluis](#assign-permissions-to-azure-key-vault).
       
        ![Versleuteling van Data Lake Store](./media/data-lake-store-get-started-portal/adls-encryption-2.png "Versleuteling van Data Lake Store")
       
        Klik op **OK** in Hallo **versleutelingsinstellingen** blade.

        Zie [Gegevens versleutelen in Azure Data Lake Store](./data-lake-store-encryption.md)voor meer informatie.

4. Klik op **Create**. Als u toopin Hallo account toohello dashboard hebt gekozen, gaat u terug toohello dashboard en ziet u Hallo voortgang van uw Data Lake Store-account ingericht. Eenmaal Hallo Data Lake Store-account ingericht Hallo accountblade weergegeven.

U kunt ook een Data Lake Store-account maken met behulp van Azure Resource Manager-sjablonen. Deze sjablonen zijn toegankelijk vanaf [Azure-snelstartsjablonen](https://azure.microsoft.com/resources/templates/?term=data+lake+store):

- Zonder gegevensversleuteling: [Azure Data Lake Store-account implementeren zonder gegevensversleuteling](https://azure.microsoft.com/en-us/resources/templates/101-data-lake-store-no-encryption/).
- Met gegevensversleuteling met behulp van Data Lake Store: [Data Lake Store-account implementeren met versleuteling (Data Lake)](https://azure.microsoft.com/resources/templates/101-data-lake-store-encryption-adls/).
- Met gegevensversleuteling met behulp van Azure Key Vault: [Data Lake Store-account implementeren met versleuteling (Key Vault)](https://azure.microsoft.com/resources/templates/101-data-lake-store-encryption-key-vault/).

### <a name="assign-permissions-to-azure-key-vault"></a>Wijs machtigingen tooAzure Sleutelkluis
Als u sleutels van een Azure Key Vault tooconfigure versleuteling op Hallo Data Lake Store-account gebruikt, moet u toegang tussen Hallo Data Lake Store-account en hello Azure Key Vault account configureren. Voer Hallo dus toodo stappen te volgen.

1. Als u sleutels van hello Azure Key Vault gebruikt, wordt een waarschuwing weergegeven boven het Hallo van Hallo blade voor Hallo Data Lake Store-account. Klik op Hallo waarschuwing tooopen hello **configureren Key Vault Permissions** blade.
   
    ![Versleuteling van Data Lake Store](./media/data-lake-store-get-started-portal/adls-encryption-3.png "Versleuteling van Data Lake Store")
2. Hallo-blade ziet u twee opties tooconfigure toegang.
   
   * Klik in de eerste optie Hallo op **machtiging verlenen** tooconfigure toegang. Hallo eerste optie is alleen ingeschakeld wanneer Hallo-gebruiker die Hallo Data Lake Store-account gemaakt ook een beheerder voor hello Azure Sleutelkluis is.
   * Hallo is andere optie toorun Hallo PowerShell-cmdlet op Hallo blade weergegeven. U moet toobe Hallo eigenaar van hello Azure Key Vault of Hallo mogelijkheid toogrant machtigingen hebben op Hallo Azure Sleutelkluis. Nadat u de cmdlet Hallo hebt uitgevoerd, keert u terug toohello blade en klik op **inschakelen** tooconfigure toegang.

## <a name="createfolder"></a>Mappen maken in Azure Data Lake Store-account
U kunt mappen maken onder uw Data Lake Store-account toomanage en opslaan van gegevens.

1. Open Hallo Data Lake Store-account dat u hebt gemaakt. Klik in het linkerdeelvenster hello, **Bladeren**, klikt u op **Data Lake Store**, en klik vervolgens op Hallo accountnaam waaronder u wilt dat toocreate mappen Hallo Data Lake Store-blade. Als u Hallo account toohello startboard hebt vastgemaakt, klik op de tegel voor dat account.
2. Klik op de blade van het Data Lake Store-account op **Gegevensverkenner**.
   
    ![Mappen maken in het Data Lake Store-account](./media/data-lake-store-get-started-portal/ADL.Create.Folder.png "Mappen maken in het Data Lake Store-account")
3. Klik in de blade van het Data Lake Store-account op **nieuwe map**, voer een naam voor de nieuwe map Hallo en klik vervolgens op **OK**.
   
    ![Mappen maken in het Data Lake Store-account](./media/data-lake-store-get-started-portal/ADL.Folder.Name.png "Mappen maken in het Data Lake Store-account")
   
    Hallo nieuw gemaakte map wordt vermeld in Hallo **Data Explorer** blade. U kunt geneste mappen maken tot elk gewenst niveau.
   
    ![Mappen maken in het Data Lake-account](./media/data-lake-store-get-started-portal/ADL.New.Directory.png "Mappen maken in het Data Lake-account")

## <a name="uploaddata"></a>Uploaden van gegevens tooAzure Data Lake Store-account
U kunt uw gegevens tooan Azure Data Lake Store-account rechtstreeks op Hallo niveau of tooa hoofdmap die u hebt gemaakt in Hallo account uploaden. In Hallo Hallo stappen tooupload een tooa bestand submap volgende schermafdruk is volgt in Hallo **Data Explorer** blade. In deze schermafbeelding is Hallo bestand geüploade tooa submap wordt weergegeven in Hallo breadcrumbs (gemarkeerd in een rood kader).

Als u een aantal gegevens voorbeeld tooupload zoekt, kunt u krijgen Hallo **Ambulance Data** map uit Hallo [Azure Data Lake Git-opslagplaats](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).

![Gegevens uploaden](./media/data-lake-store-get-started-portal/ADL.New.Upload.File.png "Gegevens uploaden")

## <a name="properties"></a>Eigenschappen en acties die beschikbaar zijn op Hallo van opgeslagen gegevens
Klik op Hallo zojuist toegevoegde bestand tooopen hello **eigenschappen** blade. Hallo-eigenschappen die zijn gekoppeld aan Hallo bestands- en Hallo acties die u op Hallo-bestand uitvoeren kunt zijn beschikbaar in deze blade. U kunt ook Hallo volledig pad toofile in uw Azure Data Lake Store-account gemarkeerd in het vak in de volgende schermafbeelding Hallo Hallo red kopiëren:

![Eigenschappen van Hallo gegevens](./media/data-lake-store-get-started-portal/ADL.File.Properties.png "eigenschappen op Hallo-gegevens")

* Klik op **Preview** toosee een voorbeeld van Hallo-bestand rechtstreeks vanuit de browser Hallo. Hallo-indeling van Hallo preview ook kunt u opgeven. Klik op **Preview**, klikt u op **indeling** in Hallo **bestandsvoorbeeld** blade en in Hallo **bestandsvoorbeeld** blade Geef Hallo opties zoals Als het aantal rijen toodisplay, codering toouse, toouse scheidingsteken, enzovoort.
  
  ![Indeling van het bestandsvoorbeeld](./media/data-lake-store-get-started-portal/ADL.File.Preview.png "Indeling van het bestandsvoorbeeld")
* Klik op **downloaden** toodownload Hallo bestand tooyour computer.
* Klik op **bestandsnaam wijzigen** toorename Hallo-bestand.
* Klik op **Verwijder bestand** toodelete Hallo-bestand.

## <a name="secure-your-data"></a>Uw gegevens beveiligen
U kunt Hallo opgeslagen gegevens in uw Azure Data Lake Store-account met Azure Active Directory en toegangsbeheer (ACL's) kunt beveiligen. Voor instructies over het toodo die Zie [gegevens beveiligen in Azure Data Lake Store](data-lake-store-secure-data.md).

## <a name="delete-azure-data-lake-store-account"></a>Azure Data Lake Store-account verwijderen
Klik op toodelete een Azure Data Lake Store-account van uw Data Lake Store-blade **verwijderen**. tooconfirm hello actie, moet u na vragen aan gebruiker tooenter Hallo naam van gewenst toodelete Hallo-account. Voer Hallo-naam van het Hallo-account en klik vervolgens op **verwijderen**.

![Data Lake-account verwijderen](./media/data-lake-store-get-started-portal/ADL.Delete.Account.png "Data Lake-account verwijderen")

## <a name="next-steps"></a>Volgende stappen
* [Gegevens in Data Lake Store beveiligen](data-lake-store-secure-data.md)
* [Azure Data Lake Analytics gebruiken met Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Azure HDInsight gebruiken met Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Diagnostische logboeken openen voor Data Lake Store](data-lake-store-diagnostic-logs.md)

