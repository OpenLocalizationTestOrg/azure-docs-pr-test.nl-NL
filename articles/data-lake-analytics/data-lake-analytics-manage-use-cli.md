---
title: aaaManage Azure Data Lake Analytics met Azure-opdrachtregelinterface | Microsoft Docs
description: Meer informatie over hoe toomanage Data Lake Analytics-accounts, gegevensbronnen, taken en gebruikers met Azure CLI
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: 4e5a3a0a-6d7f-43ed-aeb5-c3b3979a1e0a
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 0af1f89080739b39f6980989b7694734cc135715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-command-line-interface-cli"></a>Azure Data Lake Analytics beheren met Azure-opdrachtregelinterface (CLI)
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

Meer informatie over hoe Hallo toomanage Azure Data Lake Analytics-accounts, gegevensbronnen, gebruikers en taken met behulp van Azure CLI. toosee management onderwerpen met een ander hulpprogramma, klikt u op Hallo tabblad select bovenaan.


**Vereisten**

Voordat u deze zelfstudie begint, moet u de volgende Hallo hebben:

* **Een Azure-abonnement**. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).
* **Azure CLI**. Zie [Azure CLI installeren en configureren](../cli-install-nodejs.md).
  * Download en installeer Hallo **voorlopige versie** [Azure CLI-hulpprogramma's](https://github.com/MicrosoftBigData/AzureDataLake/releases) in volgorde toocomplete deze demo.
* **Verificatie**met Hallo volgende opdracht:
  
        azure login
    Zie voor meer informatie over verificatie met een werk- of schoolaccount [tooan Azure-abonnement verbinden van hello Azure CLI](../xplat-cli-connect.md).
* **Modus van Azure Resource Manager toohello switch**met Hallo volgende opdracht:
  
        azure config mode arm

**toolist hello Data Lake Store- en Data Lake Analytics-opdrachten:**

    azure datalake store
    azure datalake analytics

<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-accounts"></a>Accounts beheren
Voordat u een Data Lake Analytics-taken uitvoert, moet u een Data Lake Analytics-account hebben. In tegenstelling tot Azure HDInsight betaalt niet u voor een Analytics-account wanneer deze een taak niet wordt uitgevoerd.  U betaalt alleen voor Hallo keer wanneer een taak wordt uitgevoerd.  Zie voor meer informatie [overzicht van Azure Data Lake Analytics](data-lake-analytics-overview.md).  

### <a name="create-accounts"></a>Accounts maken
      azure datalake analytics account create "<Data Lake Analytics Account Name>" "<Azure Location>" "<Resource Group Name>" "<Default Data Lake Account Name>"


### <a name="update-accounts"></a>Bijwerken van accounts
Hallo volgende opdracht werkt Hallo eigenschappen van een bestaande Data Lake Analytics-Account

    azure datalake analytics account set "<Data Lake Analytics Account Name>"


### <a name="list-accounts"></a>Lijst van accounts
Lijst met Data Lake Analytics-accounts 

    azure datalake analytics account list

Lijst met Data Lake Analytics-accounts binnen een specifieke resourcegroep

    azure datalake analytics account list -g "<Azure Resource Group Name>"

Details van een specifieke Data Lake Analytics-account ophalen

    azure datalake analytics account show -g "<Azure Resource Group Name>" -n "<Data Lake Analytics Account Name>"

### <a name="delete-data-lake-analytics-accounts"></a>Data Lake Analytics-accounts te verwijderen
      azure datalake analytics account delete "<Data Lake Analytics Account Name>"


<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-account-data-sources"></a>Account gegevensbronnen beheren
Data Lake Analytics ondersteunt momenteel Hallo gegevensbronnen te volgen:

* [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md)
* [Azure Storage](../storage/common/storage-introduction.md)

Wanneer u een Analytics-account maakt, moet u een Azure Data Lake Storage-account toobe Hallo storage-standaardaccount toewijzen. Hallo storage-standaardaccount ADL wordt gebruikt toostore taak metagegevens en taak controlelogboeken. Nadat u een Analytics-account hebt gemaakt, kunt u extra Data Lake Storage-accounts en/of Azure Storage-account toevoegen. 

### <a name="find-hello-default-adl-storage-account"></a>Hallo ADL standaardopslagaccount vinden
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

Hallo-waarde wordt vermeld onder eigenschappen: datalakeStoreAccount:name.

### <a name="add-additional-azure-blob-storage-accounts"></a>Extra Azure Blob storage-accounts toevoegen
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -b "<Azure Blob Storage Account Short Name>" -k "<Azure Storage Account Key>"

> [!NOTE]
> Alleen Blob storage korte namen worden ondersteund.  Gebruik geen FQDN-naam, bijvoorbeeld 'myblob.blob.core.windows.net'.
> 
> 

### <a name="add-additional-data-lake-store-accounts"></a>Extra Data Lake Store-accounts toevoegen
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -l "<Data Lake Store Account Name>" [-d]

[-d] is een optionele schakeloptie tooindicate of Hallo Data Lake wordt toegevoegd Hallo Data Lake-standaardaccount. 

### <a name="update-existing-data-source"></a>Bestaande gegevensbron bijwerken
een bestaande Data Lake Store-account toobe Hallo standaardwaarde tooset:

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -l "<Azure Data Lake Store Account Name>" -d

een bestaande Blob storage-accountsleutel tooupdate:

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -b "<Blob Storage Account Name>" -k "<New Blob Storage Account Key>"

### <a name="list-data-sources"></a>Lijst van gegevensbronnen:
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

![Gegevensbron voor Data Lake Analytics-lijst](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-data-source.png)

### <a name="delete-data-sources"></a>Gegevensbronnen verwijderen:
toodelete een Data Lake Store-account:

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Azure Data Lake Store Account Name>"

toodelete een Blob storage-account:

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Blob Storage Account Name>"

## <a name="manage-jobs"></a>Taken beheren
U moet een Data Lake Analytics-account hebben voordat u een taak kunt maken.  Zie voor meer informatie [beheren Data Lake Analytics-accounts](#manage-accounts).

### <a name="list-jobs"></a>Taken weergeven
      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"

![Gegevensbron voor Data Lake Analytics-lijst](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-jobs.png)

### <a name="get-job-details"></a>Taakdetails van de ophalen
      azure datalake analytics job show -n "<Data Lake Analytics Account Name>" -j "<Job ID>"

### <a name="submit-jobs"></a>Verzenden van taken
> [!NOTE]
> Hallo standaardprioriteit van een taak is 1000 en Hallo standaard mate van parallelle uitvoering voor een taak is 1.
> 
> 

    azure datalake analytics job create  "<Data Lake Analytics Account Name>" "<Job Name>" "<Script>"

### <a name="cancel-jobs"></a>Taken annuleren
Hallo lijst opdracht toofind Hallo taak-id gebruiken en gebruik vervolgens annuleren toocancel Hallo taak.

      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"
      azure datalake analytics job cancel "<Data Lake Analytics Account Name>" "<Job ID>"

## <a name="manage-catalog"></a>Catalogus beheren
Hallo U-SQL-catalogus is toostructure gebruikte gegevens en code zodat ze kunnen worden gedeeld door de U-SQL-scripts. Hallo catalogus kunt Hallo hoogste prestaties mogelijk met gegevens in Azure Data Lake. Zie [U-SQL-catalogus gebruiken](data-lake-analytics-use-u-sql-catalog.md) voor meer informatie.

### <a name="list-catalog-items"></a>Lijst met catalogusitems
    #List databases
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t database

    #List tables
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t table

Hallo-typen zijn database, schema, assembly, externe gegevensbron, tabel, functie met tabelwaarden of tabelstatistieken.

<!-- ################################ -->
<!-- ################################ -->
## <a name="use-arm-groups"></a>ARM-groepen gebruiken
Toepassingen bestaan in het algemeen uit meerdere onderdelen, bijvoorbeeld een web-app, database, databaseserver, opslag en services van derden. Azure Resource Manager (ARM) kunt u toowork met Hallo resources in uw toepassing als een groep waarnaar wordt verwezen tooas een Azure-resourcegroep. U kunt implementeren, bijwerken, bewaken of verwijder alle Hallo resources voor uw toepassing in een enkele, gecoördineerde bewerking. Voor implementatie gebruikt u een sjabloon. Deze sjabloon kan voor verschillende omgevingen worden gebruikt, zoals testen, faseren en productie. U kunt facturering voor uw organisatie verduidelijken door Hallo Samengevoegde kosten voor de hele groep Hallo weer te geven. Zie [Overzicht van Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) voor meer informatie. 

Een Data Lake Analytics-service kan Hallo volgende onderdelen bevatten:

* Azure Data Lake Analytics-account
* Vereiste standaard Azure Data Lake Storage-account
* Aanvullende Azure Data Lake Storage-accounts
* Extra Azure Storage-accounts

U kunt al deze onderdelen onder één ARM groep toomake maken ze gemakkelijker toomanage.

![Azure Data Lake Analytics-account en opslag](./media/data-lake-analytics-manage-use-portal/data-lake-analytics-arm-structure.png)

Een Data Lake Analytics-account en de afhankelijke opslagaccounts Hallo moeten worden geplaatst in Hallo dezelfde Azure-Datacenter.
Hallo ARM groep kan echter in een ander datacenter worden geplaatst.  

## <a name="see-also"></a>Zie ook
* [Overzicht van Microsoft Azure Data Lake Analytics](data-lake-analytics-overview.md)
* [Aan de slag met Data Lake Analytics met Azure Portal](data-lake-analytics-get-started-portal.md)
* [Azure Data Lake Analytics beheren met Azure Portal](data-lake-analytics-manage-use-portal.md)
* [Azure Data Lake Analytics-taken bewaken en problemen oplossen met Azure Portal](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)

