---
title: aaaGet de slag met Azure Data Lake Analytics met Azure CLI 2.0 | Microsoft Docs
description: 'Informatie over hoe toouse hello Azure Command-line Interface 2.0 toocreate een Data Lake Analytics-account maken van een Data Lake Analytics-taak met U-SQL, en het Hallo-taak verzenden. '
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: jgao
ms.openlocfilehash: c4e91c0d3526e4932c2948c0a326d4cedc985791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-cli-20"></a>Aan de slag met Azure Data Lake Analytics met Azure CLI 2.0
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

In deze zelfstudie ontwikkelt u een taak voor het lezen van een TSV-bestand (door tabs gescheiden waarden) en het converteren ervan naar een CSV-bestand (door komma's gescheiden waarden). toogo via Hallo dezelfde zelfstudie met behulp van andere ondersteunde hulpprogramma's, gebruik Hallo vervolgkeuzelijst bovenaan Hallo van deze sectie.

## <a name="prerequisites"></a>Vereisten
Voordat u deze zelfstudie begint, moet u de volgende items Hallo hebben:

* **Een Azure-abonnement**. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).
* **Azure CLI 2.0**. Zie [Azure CLI installeren en configureren](https://docs.microsoft.com/cli/azure/install-azure-cli).

## <a name="log-in-tooazure"></a>Meld u bij tooAzure

toolog in tooyour Azure-abonnement:

```
azurecli
az login
```

U aangevraagde toobrowse tooa URL zijn en voer een verificatiecode op te geven.  En volg Hallo instructies tooenter uw referenties.

Zodra u zich hebt aangemeld, worden Hallo aanmelding opdracht uw abonnementen.

een specifiek abonnement toouse:

```
az account set --subscription <subscription id>
```

## <a name="create-data-lake-analytics-account"></a>Een Data Lake Analytics-account maken
U hebt een Data Lake Analytics-account nodig voordat u taken kunt uitvoeren. toocreate een Data Lake Analytics-account, moet u Hallo volgende items:

* **Azure-resourcegroep**. Er moet een Data Lake Analytics-account zijn gemaakt binnen een Azure-resourcegroep. [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) kunt u toowork met Hallo resources in uw toepassing als groep. U kunt implementeren, bijwerken of verwijderen alle Hallo resources voor uw toepassing in een enkele, gecoördineerde bewerking.  

toolist hello bestaande resourcegroepen in uw abonnement:

```
az group list
```

een nieuwe resourcegroep toocreate:

```
az group create --name "<Resource Group Name>" --location "<Azure Location>"
```

* **Naam van Data Lake Analytics-account**. Elk Data Lake Analytics-account heeft een naam.
* **Locatie**. Gebruik een van de hello Azure-datacenters die ondersteuning biedt voor Data Lake Analytics.
* **Data Lake Store-standaardaccount**: elk Data Lake Store Analytics-account heeft een Data Lake Store-standaardaccount.

toolist hello bestaande Data Lake Store-account:

```
az dls account list
```

toocreate een nieuw Data Lake Store-account:

```azurecli
az dls account create --account "<Data Lake Store Account Name>" --resource-group "<Resource Group Name>"
```

Hallo na syntaxis toocreate een Data Lake Analytics-account gebruiken:

```
az dla account create --account "<Data Lake Analytics Account Name>" --resource-group "<Resource Group Name>" --location "<Azure location>" --default-data-lake-store "<Default Data Lake Store Account Name>"
```

U kunt na het maken van een account gebruiken Hallo opdrachten toolist Hallo accounts te volgen en accountdetails weergeven:

```
az dla account list
az dla account show --account "<Data Lake Analytics Account Name>"            
```

## <a name="upload-data-toodata-lake-store"></a>Uploaden van gegevens tooData Lake Store
In deze zelfstudie verwerkt u een aantal zoeklogboeken.  Hallo-zoeklogboek kan worden opgeslagen in Data Lake store of Azure Blob-opslag.

Hello Azure-portal biedt een gebruikersinterface voor het kopiëren van sommige sample data bestanden toohello Data Lake Store-standaardaccount, waaronder een zoeklogboekbestand. Zie [brongegevens voorbereiden](data-lake-analytics-get-started-portal.md) tooupload Hallo gegevens toohello Data Lake Store-standaardaccount.

tooupload bestanden met CLI 2.0, gebruik Hallo volgende opdrachten:

```
az dls fs upload --account "<Data Lake Store Account Name>" --source-path "<Source File Path>" --destination-path "<Destination File Path>"
az dls fs list --account "<Data Lake Store Account Name>" --path "<Path>"
```

Data Lake Analytics heeft ook toegang tot Azure Blob-opslag.  Zie voor het uploaden van Blob-opslag voor gegevens tooAzure [Using hello Azure CLI met Azure Storage](../storage/common/storage-azure-cli.md).

## <a name="submit-data-lake-analytics-jobs"></a>Data Lake Analytics-taken verzenden
Hallo Data Lake Analytics-taken worden geschreven in Hallo U-SQL-taal. toolearn meer informatie over U-SQL, Zie [aan de slag met U-SQL-taal](data-lake-analytics-u-sql-get-started.md) en [eence van U-SQL-taal](http://go.microsoft.com/fwlink/?LinkId=691348).

**een Data Lake Analytics-taakscript toocreate**

Maak een tekstbestand met het volgende U-SQL-script en sla van Hallo tekst bestand tooyour werkstation:

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

Dit U-SQL-script leest Hallo brongegevensbestand met **Extractors.Tsv()**, en maakt vervolgens een CSV-bestand met **Outputters.Csv()**.

Het Wijzig Hallo twee paden niet, tenzij u Hallo bronbestand naar een andere locatie kopiëren.  Data Lake Analytics maakt de uitvoermap Hallo als deze niet bestaat.

Het is eenvoudiger toouse relatieve paden voor bestanden die zijn opgeslagen in Data Lake Store-standaardaccounts. Maar u kunt ook absolute paden gebruiken.  Bijvoorbeeld:

```
adl://<Data LakeStorageAccountName>.azuredatalakestore.net:443/Samples/Data/SearchLog.tsv
```

U moet absolute paden tooaccess bestanden in gekoppelde Storage-accounts gebruiken.  Hallo-syntaxis voor bestanden die zijn opgeslagen in het gekoppelde Azure Storage-account is:

```
wasb://<BlobContainerName>@<StorageAccountName>.blob.core.windows.net/Samples/Data/SearchLog.tsv
```

> [!NOTE]
> Azure Blob-containers met openbare blobs worden niet ondersteund.      
> Azure Blob-containers met openbare containers worden niet ondersteund.      
>

**toosubmit taken**

Gebruik Hallo syntaxis toosubmit een taak te volgen.

```
az dla job submit --account "<Data Lake Analytics Account Name>" --job-name "<Job Name>" --script "<Script Path and Name>"
```

Bijvoorbeeld:

```
az dla job submit --account "myadlaaccount" --job-name "myadlajob" --script @"C:\DLA\myscript.txt"
```

**toolist taken en de taakdetails weergeven**

```
azurecli
az dla job list --account "<Data Lake Analytics Account Name>"
az dla job show --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

**toocancel taken**

```
az dla job cancel --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

## <a name="retrieve-job-results"></a>Taakresultaten ophalen

Nadat een taak is voltooid, kunt u gebruiken Hallo opdrachten toolist Hallo uitvoerbestanden te volgen en Hallo bestanden downloaden:

```
az dls fs list --account "<Data Lake Store Account Name>" --source-path "/Output" --destination-path "<Destintion>"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv" --length 128 --offset 0
az dls fs downlod --account "<Data Lake Store Account Name>" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "<Destination Path and File Name>"
```

Bijvoorbeeld:

```
az dls fs downlod --account "myadlsaccount" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "C:\DLA\myfile.csv"
```

## <a name="pipelines-and-recurrences"></a>Pijplijnen en herhalingen

**Meer informatie over pijplijnen en herhalingen**

Gebruik Hallo `az dla job pipeline` opdrachten toosee Hallo pijplijn informatie taken eerder is verzonden.

```
az dla job pipeline list --account "<Data Lake Analytics Account Name>"

az dla job pipeline show --account "<Data Lake Analytics Account Name>" --pipeline-identity "<Pipeline ID>"
```

Gebruik Hallo `az dla job recurrence` opdrachten toosee Hallo terugkeerpatroon informatie voor eerder ingediende taken.

```
az dla job recurrence list --account "<Data Lake Analytics Account Name>"

az dla job recurrence show --account "<Data Lake Analytics Account Name>" --recurrence-identity "<Recurrence ID>"
```

## <a name="next-steps"></a>Volgende stappen

* toosee hello referentiedocument Data Lake Analytics CLI 2.0, Zie [Data Lake Analytics](https://docs.microsoft.com/cli/azure/dla).
* toosee hello referentiedocument Data Lake Store CLI 2.0, Zie [Data Lake Store](https://docs.microsoft.com/cli/azure/dls).
* Zie voor een complexere query toosee [websitelogboeken analyseren met Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).
