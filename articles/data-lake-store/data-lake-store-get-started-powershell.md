---
title: aaaUse PowerShell tooget de slag met Azure Data Lake Store | Microsoft Docs
description: Gebruik Azure PowerShell toocreate een Data Lake Store-account en basisbewerkingen uit te voeren
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: bf85f369-f9aa-4ca1-9ae7-e03a78eb7290
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 9c958bfd63e412ec0b0a4113a149f61aee026bc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-powershell"></a>Aan de slag met Azure Data Lake Store met Azure PowerShell
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

Meer informatie over hoe toouse Azure PowerShell toocreate een Azure Data Lake opslaan account en basisbewerkingen uitvoert, zoals maken van mappen, uploaden en downloaden van gegevensbestanden, verwijderen van uw account, enzovoort. Zie [Overzicht van Data Lake Store](data-lake-store-overview.md) voor meer informatie over Data Lake Store.

## <a name="prerequisites"></a>Vereisten
Voordat u deze zelfstudie begint, moet u de volgende Hallo hebben:

* **Een Azure-abonnement**. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).
* **Azure PowerShell 1.0 of hoger**. Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).

## <a name="authentication"></a>Authentication
Dit artikel wordt het eenvoudiger voor verificatie met Data Lake Store waar u zich na vragen aan gebruiker tooenter de referenties van uw Azure-account. Hallo toegang niveau tooData Lake Store-account en een nieuw bestandssysteem vervolgens beheerst door het toegangsniveau Hallo Hallo aangemelde gebruiker. Er zijn echter andere benaderingen als goed tooauthenticate met Data Lake Store, die zijn **eindgebruiker verificatie** of **authentication service-naar-serviceconnector**. Voor instructies en meer informatie over het tooauthenticate, Zie [eindgebruiker verificatie](data-lake-store-end-user-authenticate-using-active-directory.md) of [authentication Service-naar-serviceconnector](data-lake-store-authenticate-using-active-directory.md).

## <a name="create-an-azure-data-lake-store-account"></a>Een Azure Data Lake Store-account maken
1. Op het bureaublad een nieuw Windows PowerShell-venster openen Hallo volgende codefragment toolog in tooyour Azure-account invoeren, ingesteld Hallo-abonnement en Hallo Data Lake Store-provider geregistreerd. Wanneer de vraag toolog, zorg ervoor dat u zich aanmelden als een Hallo abonnement beheerders/eigenaars:

        # Log in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Azure Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"
2. Een Azure Data Lake Store-account is gekoppeld aan een Azure-resourcegroep. Maak daarom eerst een Azure-resourcegroep.

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    ![Een Azure-resourcegroep maken](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Een Azure-resourcegroep maken")
3. Maak een Azure Data Lake Store-account. Hallo-naam die u opgeeft mag alleen kleine letters en cijfers bevatten.

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    ![Een Azure Data Lake Store-account maken](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Een Azure Data Lake Store-account maken")
4. Controleer of Hallo-account is gemaakt.

        Test-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

    Hallo uitvoer voor dit mag **True**.

## <a name="create-directory-structures-in-your-azure-data-lake-store"></a>Mapstructuren maken in uw Azure Data Lake Store
U kunt mappen maken onder uw Azure Data Lake Store-account toomanage en opslaan van gegevens.

1. Geef een hoofdmap op.

        $myrootdir = "/"
2. Maak een nieuwe map aangeroepen **mynewdirectory** onder Hallo opgegeven toegangspunt.

        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/mynewdirectory
3. Controleer of dat nieuwe map Hallo is gemaakt.

        Get-AzureRmDataLakeStoreChildItem -AccountName $dataLakeStoreName -Path $myrootdir

    Hallo volgende uitvoer moet worden weergegeven:

    ![Map controleren](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "Map controleren")

## <a name="upload-data-tooyour-azure-data-lake-store"></a>Uploaden van gegevens tooyour Azure Data Lake Store
U kunt uw data Lake Store van de tooData rechtstreeks op Hallo niveau of tooa hoofdmap die u hebt gemaakt in Hallo account uploaden. Hallo codefragmenten hieronder laten zien hoe tooupload enkele voorbeeld-gegevensmap toohello (**mynewdirectory**) u hebt gemaakt in de vorige sectie Hallo.

Als u een aantal gegevens voorbeeld tooupload zoekt, kunt u krijgen Hallo **Ambulance Data** map uit Hallo [Azure Data Lake Git-opslagplaats](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData). Hallo-bestand downloaden en opslaan in een lokale map op uw computer, zoals C:\sampledata\.

    Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\sampledata\vehicle1_09142014.csv" -Destination $myrootdir\mynewdirectory\vehicle1_09142014.csv


## <a name="rename-download-and-delete-data-from-your-data-lake-store"></a>Gegevens in uw Data Lake Store een nieuwe naam geven, downloaden en verwijderen
toorename een bestand Hallo volgende opdracht gebruiken:

    Move-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014.csv -Destination $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

toodownload een bestand Hallo volgende opdracht gebruiken:

    Export-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv -Destination "C:\sampledata\vehicle1_09142014_Copy.csv"

toodelete een bestand Hallo volgende opdracht gebruiken:

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

Wanneer u wordt gevraagd, typt u **Y** toodelete Hallo item. Als u meer dan één bestand toodelete hebt, kunt u opgeven dat alle Hallo paden, gescheiden door een komma.

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014.csv, $myrootdir\mynewdirectoryvehicle1_09142014_Copy.csv

## <a name="delete-your-azure-data-lake-store-account"></a>Uw Azure Data Lake Store-account verwijderen
Hallo opdracht toodelete na uw Data Lake Store-account gebruiken.

    Remove-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

Wanneer u wordt gevraagd, typt u **Y** toodelete Hallo-account.

## <a name="performance-guidance-while-using-powershell"></a>Prestatierichtlijnen bij het gebruik van PowerShell

Hieronder vindt Hallo meest belangrijke instellingen die afgestemd tooget Hallo optimale prestaties worden kunnen tijdens het gebruik van PowerShell toowork met Data Lake Store:

| Eigenschap            | Standaard | Beschrijving |
|---------------------|---------|-------------|
| PerFileThreadCount  | 10      | Deze parameter kunt u toochoose Hallo aantal parallelle threads voor uploaden of elk bestand downloaden. Dit nummer geeft Hallo max threads dat kunnen worden verdeeld per bestand, maar krijgt u mogelijk minder threads, afhankelijk van uw scenario (bijvoorbeeld als u een 1 KB-bestand uploadt, krijgt u één thread zelfs als u voor 20 threads vragen).  |
| ConcurrentFileCount | 10      | Deze parameter is specifiek bedoeld voor het uploaden en downloaden van mappen. Deze parameter bepaalt het aantal gelijktijdige bestanden die kunnen worden geüpload of gedownload Hallo. Dit aantal geeft Hallo kunt u het maximum aantal gelijktijdige bestanden die kunnen worden geüpload of in één keer worden gedownload, maar krijgt u mogelijk minder gelijktijdigheid, afhankelijk van uw scenario (bijvoorbeeld als u twee bestanden uploaden wilt, krijgt u twee gelijktijdige bestandsuploads zelfs als u vragen 15). |

**Voorbeeld**

Met deze opdracht downloadt bestanden van de lokale schijf van Azure Data Lake Store toohello gebruiker met 20 threads per bestand en 100 gelijktijdige bestanden.

    Export-AzureRmDataLakeStoreItem -AccountName <Data Lake Store account name> -PerFileThreadCount 20-ConcurrentFileCount 100 -Path /Powershell/100GB/ -Destination C:\Performance\ -Force -Recurse

### <a name="how-do-i-determine-hello-value-tooset-for-these-parameters"></a>Hoe bepaal ik Hallo waarde tooset voor deze parameters

Hier volgen een aantal richtlijnen.

* **Stap 1: Bepalen Hallo totale aantal threads** -door berekenen Hallo thread totale aantal toouse moet worden gestart. Een algemene richtlijn is 6 threads voor elke fysieke kern.

        Total thread count = total physical cores * 6

    **Voorbeeld**

    Ervan uitgaande dat u uitvoert Hallo PowerShell-opdrachten van een VM D14 die 16 kernen heeft

        Total thread count = 16 cores * 6 = 96 threads


* **Stap 2: Berekenen PerFileThreadCount** -We onze PerFileThreadCount op basis van Hallo grootte van bestanden Hallo berekenen. Voor bestanden die kleiner zijn dan 2,5 GB is er geen toochange moet deze parameter omdat Hallo standaardwaarde van 10 voldoende is. Voor bestanden groter zijn dan 2,5 GB, moet u 10 threads terwijl Hallo basis voor de eerste 2,5 GB Hallo en 1-thread voor elke extra 256 MB toename bestandsgrootte toegevoegd. Als u een map kopieert met bestanden van zeer verschillende groottes, kunt u overwegen ze op vergelijkbare grootte te sorteren. Grote verschillen in bestandsgroottes kunnen tot slechtere prestaties leiden. Als dat niet mogelijk toogroup vergelijkbare bestandsgrootten, moet u PerFileThreadCount op basis van de maximale bestandsgrootte Hallo instellen.

        PerFileThreadCount = 10 threads for hello first 2.5GB + 1 thread for each additional 256MB increase in file size

    **Voorbeeld**

    Als er 100 bestanden variëren van 1GB too10GB, gebruiken we Hallo 10GB als Hallo grootste bestandsgrootte voor vergelijking, welke Hallo volgende zou lezen.

        PerFileThreadCount = 10 + ((10GB - 2.5GB) / 256MB) = 40 threads

* **Stap 3: Berekenen ConcurrentFilecount** -gebruik Hallo totale aantal threads en PerFileThreadCount toocalculate ConcurrentFileCount op basis van Hallo volgende vergelijking.

        Total thread count = PerFileThreadCount * ConcurrentFileCount

    **Voorbeeld**

    Op basis van voorbeeldwaarden Hallo die we hebt gebruikt

        96 = 40 * ConcurrentFileCount

    Dus **ConcurrentFileCount** is **2.4**, die we te kunnen afronden**2**.

### <a name="further-tuning"></a>Verder afstemmen

U wordt mogelijk verder afstemmen omdat er een bereik van het bestand grootten toowork met. Hallo hierboven berekening werkt goed als alle of de meeste van Hallo bestanden groter en dichter toohello 10GB bereik zijn. Als het echter bestanden van zeer uiteenlopende groottes betreft, waarbij veel bestanden kleiner zijn, kunt u de PerFileThreadCount verlagen. Hallo PerFileThreadCount verlaagt, kunnen we ConcurrentFileCount verhogen. Dus als gaan we ervan uit dat de meeste van de bestanden zijn kleiner Hallo 5GB bereik, kunnen we doen opnieuw onze berekening:

    PerFileThreadCount = 10 + ((5GB - 2.5GB) / 256MB) = 20

Dus **ConcurrentFileCount** wordt nu 96/20, namelijk 4.8 afgerond te**4**.

U kunt tootune deze instellingen gaan door het wijzigen van Hallo **PerFileThreadCount** omhoog en omlaag afhankelijk van Hallo distributie van de bestandsgrootte.

### <a name="limitation"></a>Beperking

* **Aantal bestanden is kleiner dan ConcurrentFileCount**: als het aantal bestanden die u uploadt Hallo kleiner dan Hallo is **ConcurrentFileCount** die u hebt berekend vervolgens minder  **ConcurrentFileCount** toobe gelijk toohello aantal bestanden. Kunt u eventuele resterende threads tooincrease **PerFileThreadCount**.

* **Te veel threads**: als u thread verhogen tellen te veel zonder te verhogen van de clustergrootte van uw, loopt u verminderde prestaties Hallo risico. Kunnen er conflicten problemen bij het context overschakelen op Hallo CPU.

* **Onvoldoende gelijktijdigheid**: als Hallo gelijktijdigheid niet voldoende is, wordt het cluster is mogelijk te klein. U kunt Hallo aantal knooppunten in uw cluster zodat u meer gelijktijdige uitvoering verhogen.

* **Beperkingsfouten**: er treden mogelijk beperkingsfouten op als uw gelijktijdigheid te hoog is. Als u beperking fouten ziet, moet u beperkt Hallo of contact met ons opnemen.

## <a name="next-steps"></a>Volgende stappen
* [Gegevens in Data Lake Store beveiligen](data-lake-store-secure-data.md)
* [Azure Data Lake Analytics gebruiken met Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Azure HDInsight gebruiken met Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)

