---
title: aaaUse Azure opdrachtregelprogramma 2.0 interface tooget de slag met Azure Data Lake Store | Microsoft Docs
description: Gebruik Azure platformoverschrijdende opdrachtregel 2.0 toocreate een Data Lake Store-account en basisbewerkingen uit te voeren
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 4ffa0f4a-1cca-46ac-803d-1fc8538c685b
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 374dcd6cdbc13ad19f6c65502329986ecae60ef2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-cli-20"></a>Aan de slag met Azure Data Lake Store met Azure CLI 2.0
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

Meer informatie over hoe Azure CLI 2.0 toouse toocreate een Azure Data Lake opslaan account en basisbewerkingen uitvoert, zoals maken van mappen, uploaden en downloaden van gegevensbestanden, verwijderen van uw account, enzovoort. Zie [Overzicht van Data Lake Store](data-lake-store-overview.md) voor meer informatie over Data Lake Store.

Hello Azure CLI 2.0 is een nieuwe Azure opdrachtregelprogramma ervaring voor het beheren van Azure-resources. Deze kan worden gebruikt in Mac OS, Linux en Windows. Zie [Overview of Azure CLI 2.0](https://docs.microsoft.com/cli/azure/overview) (Overzicht van Azure CLI 2.0) voor meer informatie. U kunt ook zoeken op Hallo [naslaginformatie over Azure Data Lake Store CLI 2.0](https://docs.microsoft.com/cli/azure/dls) voor een volledige lijst met opdrachten en syntaxis.


## <a name="prerequisites"></a>Vereisten
Voordat u dit artikel, moet u de volgende Hallo hebben:

* **Een Azure-abonnement**. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).

* **Azure CLI 2.0**: zie [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) (Azure CLI 2.0 installeren) voor instructies.

## <a name="authentication"></a>Verificatie

In dit artikel wordt een eenvoudigere verificatiemethode voor Data Lake Store gebruikt waarbij u zich als een eindgebruiker aanmeldt. Hallo toegang niveau tooData Lake Store-account en een nieuw bestandssysteem vervolgens beheerst door het toegangsniveau Hallo Hallo aangemelde gebruiker. Er zijn echter andere benaderingen als goed tooauthenticate met Data Lake Store, die zijn **eindgebruiker verificatie** of **authentication service-naar-serviceconnector**. Voor instructies en meer informatie over het tooauthenticate, Zie [eindgebruiker verificatie](data-lake-store-end-user-authenticate-using-active-directory.md) of [authentication Service-naar-serviceconnector](data-lake-store-authenticate-using-active-directory.md).


## <a name="log-in-tooyour-azure-subscription"></a>Meld u bij tooyour Azure-abonnement

1. Meld u aan bij uw Azure-abonnement.

    ```azurecli
    az login
    ```

    U kunt een toouse code ophalen in de volgende stap Hallo. Gebruik een web browser tooopen Hallo pagina https://aka.ms/devicelogin en Hallo code tooauthenticate invoeren. U bent na vragen aan gebruiker toolog aan met uw referenties.

2. Zodra u zich aanmeldt, Hallo Hallo venster een lijst met alle Azure-abonnementen die gekoppeld aan uw account zijn. Hallo na de opdracht toouse een specifiek abonnement gebruiken.
   
    ```azurecli
    az account set --subscription <subscription id> 
    ```

## <a name="create-an-azure-data-lake-store-account"></a>Een Azure Data Lake Store-account maken

1. Maak een nieuwe resourcegroep. In Hallo volgende opdracht, bieden Hallo parameterwaarden die u wilt dat toouse. Als het Hallo-locatienaam spaties bevat, kunt u deze aanhalingstekens geplaatst. Bijvoorbeeld “VS-oost 2”. 
   
    ```azurecli
    az group create --location "East US 2" --name myresourcegroup
    ```

2. Hallo Data Lake Store-account maken.
   
    ```azurecli
    az dls account create --account mydatalakestore --resource-group myresourcegroup
    ```

## <a name="create-folders-in-a-data-lake-store-account"></a>Mappen maken in een Data Lake Store-account

U kunt mappen maken onder uw Azure Data Lake Store-account toomanage en opslaan van gegevens. Gebruik Hallo na de opdracht toocreate een map met de naam **mynewfolder** in de hoofdmap Hallo Hallo Data Lake Store.

```azurecli
az dls fs create --account mydatalakestore --path /mynewfolder --folder
```

> [!NOTE]
> Hallo `--folder` parameter zorgt ervoor dat Hallo opdracht maakt u een map. Als deze parameter niet aanwezig is, maakt Hallo opdracht u een leeg bestand met de naam van mynewfolder in de hoofdmap Hallo Hallo Data Lake Store-account.
> 
>

## <a name="upload-data-tooa-data-lake-store-account"></a>Uploaden van gegevens tooa Data Lake Store-account

U kunt gegevens tooData Lake Store rechtstreeks op Hallo niveau of tooa hoofdmap die u hebt gemaakt in Hallo account uploaden. Hallo codefragmenten hieronder laten zien hoe tooupload enkele map toohello met voorbeeldgegevens (**mynewfolder**) u hebt gemaakt in de vorige sectie Hallo.

Als u een aantal gegevens voorbeeld tooupload zoekt, kunt u krijgen Hallo **Ambulance Data** map uit Hallo [Azure Data Lake Git-opslagplaats](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData). Hallo-bestand downloaden en opslaan in een lokale map op uw computer, zoals C:\sampledata\.

```azurecli
az dls fs upload --account mydatalakestore --source-path "C:\SampleData\AmbulanceData\vehicle1_09142014.csv" --destination-path "/mynewfolder/vehicle1_09142014.csv"
```

> [!NOTE]
> U moet Hallo bestemming voor Hallo volledige pad inclusief Hallo-bestandsnaam opgeven.
> 
>


## <a name="list-files-in-a-data-lake-store-account"></a>Bestanden in een Data Lake Store-account weergeven

Hallo volgende opdracht toolist Hallo bestanden in een Data Lake Store-account gebruiken.

```azurecli
az dls fs list --account mydatalakestore --path /mynewfolder
```

Hallo-uitvoer hiervan moet vergelijkbaar toohello volgende:

    [
        {
            "accessTime": 1491323529542,
            "aclBit": false,
            "blockSize": 268435456,
            "group": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
            "length": 1589881,
            "modificationTime": 1491323531638,
            "msExpirationTime": 0,
            "name": "mynewfolder/vehicle1_09142014.csv",
            "owner": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
            "pathSuffix": "vehicle1_09142014.csv",
            "permission": "770",
            "replication": 1,
            "type": "FILE"
        }
    ]

## <a name="rename-download-and-delete-data-from-a-data-lake-store-account"></a>Gegevens in een Data Lake Store-account een nieuwe naam geven, downloaden en verwijderen 

* **een bestand toorename**, Hallo volgende opdracht gebruiken:
  
    ```azurecli
    az dls fs move --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014.csv --destination-path /mynewfolder/vehicle1_09142014_copy.csv
    ```

* **een bestand toodownload**, Hallo volgende opdracht gebruiken. Zorg ervoor dat het doelpad Hallo die u al opgeeft bestaat.
  
    ```azurecli     
    az dls fs download --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014_copy.csv --destination-path "C:\mysampledata\vehicle1_09142014_copy.csv"
    ```

    > [!NOTE]
    > Hallo opdracht maakt u de doelmap Hallo als deze niet bestaat.
    > 
    >

* **een bestand toodelete**, Hallo volgende opdracht gebruiken:
  
    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder/vehicle1_09142014_copy.csv
    ```

    Als u toodelete Hallo map wilt **mynewfolder** en Hallo bestand **vehicle1_09142014_copy.csv** samen in één opdracht gebruik Hallo--recurse parameter

    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder --recurse
    ```

## <a name="work-with-permissions-and-acls-for-a-data-lake-store-account"></a>Machtigingen en ACL's gebruiken voor een Data Lake Store-account

In deze sectie leert u hoe u toomanage ACL's en -machtigingen met Azure CLI 2.0. Zie [Toegangsbeheer in Azure Data Lake Store](data-lake-store-access-control.md) voor gedetailleerde informatie over de implementatie van ACL's in Azure Data Lake Store.

* **tooupdate hello eigenaar van een bestandsmap**, Hallo volgende opdracht gebruiken:

    ```azurecli
    az dls fs access set-owner --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --group 80a3ed5f-959e-4696-ba3c-d3c8b2db6766 --owner 6361e05d-c381-4275-a932-5535806bb323
    ```

* **tooupdate hello machtigingen voor een bestandsmap**, Hallo volgende opdracht gebruiken:

    ```azurecli
    az dls fs access set-permission --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --permission 777
    ```
    
* **tooget hello ACL's voor een opgegeven pad**, Hallo volgende opdracht gebruiken:

    ```azurecli
    az dls fs access show --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv
    ```

    Hallo-uitvoer moet vergelijkbaar toohello volgende:

        {
            "entries": [
            "user::rwx",
            "group::rwx",
            "other::---"
          ],
          "group": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
          "owner": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
          "permission": "770",
          "stickyBit": false
        }

* **een vermelding voor een ACL tooset**, Hallo volgende opdracht gebruiken:

    ```azurecli
    az dls fs access set-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323:-w-
    ```

* **een vermelding voor een ACL tooremove**, Hallo volgende opdracht gebruiken:

    ```azurecli
    az dls fs access remove-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323
    ```

* **de standaardwaarde van een volledige ACL tooremove**, Hallo volgende opdracht gebruiken:

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder --default-acl
    ```

* **een hele niet-standaard ACL tooremove**, Hallo volgende opdracht gebruiken:

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder
    ```
    
## <a name="delete-a-data-lake-store-account"></a>Een Data Lake Store-account verwijderen
Hallo na de opdracht toodelete een Data Lake Store-account gebruiken.

```azurecli
az dls account delete --account mydatalakestore
```

Wanneer u wordt gevraagd, typt u **Y** toodelete Hallo-account.

## <a name="next-steps"></a>Volgende stappen

* [Naslaggegevens van Azure Data Lake Store CLI 2.0](https://docs.microsoft.com/cli/azure/dls)
* [Gegevens in Data Lake Store beveiligen](data-lake-store-secure-data.md)
* [Azure Data Lake Analytics gebruiken met Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Azure HDInsight gebruiken met Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)

[azure-command-line-tools]: ../xplat-cli-install.md
