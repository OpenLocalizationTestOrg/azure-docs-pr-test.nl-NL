---
title: aaaGet de slag met Azure Data Lake Analytics met Azure PowerShell | Microsoft Docs
description: 'Azure PowerShell toocreate een Data Lake Analytics-account gebruiken, maken van een Data Lake Analytics-taak met U-SQL en verzenden van Hallo-taak. '
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 8a4e901e-9656-4a60-90d0-d78ff2f00656
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/04/2017
ms.author: edmaca
ms.openlocfilehash: cb9b35352d1cc9a78337448b1d6835875a212e08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-powershell"></a>Aan de slag met Azure Data Lake Analytics met Azure PowerShell
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

Informatie over hoe toouse Azure PowerShell toocreate Azure Data Lake Analytics-accounts en vervolgens verzenden en U-SQL-taken uitvoeren. Zie [Overzicht van Azure Data Lake Analytics](data-lake-analytics-overview.md) voor meer informatie over Data Lake Analytics.

## <a name="prerequisites"></a>Vereisten

Voordat u deze zelfstudie begint, hebt u de volgende informatie Hallo:

* **Een Azure Data Lake Analytics-account**. Zie [Aan de slag met Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal).
* **Een werkstation met Azure PowerShell**. Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).

## <a name="log-in-tooazure"></a>Meld u bij tooAzure

In deze zelfstudie wordt ervan uitgegaan dat u al bekend bent met het gebruik van Azure PowerShell. In het bijzonder, moet u tooknow hoe toolog in tooAzure. Zie Hallo [aan de slag met Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps) als u hulp nodig hebt.

toolog met de abonnementsnaam van een:

```
Login-AzureRmAccount -SubscriptionName "ContosoSubscription"
```

U kunt ook een abonnement-id toolog in gebruiken in plaats van de naam van Hallo abonnement:

```
Login-AzureRmAccount -SubscriptionId "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
```

Als dit lukt, ziet er Hallo-uitvoer van deze opdracht Hallo volgende tekst:

```
Environment           : AzureCloud
Account               : joe@contoso.com
TenantId              : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionId        : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionName      : ContosoSubscription
CurrentStorageAccount :
```

## <a name="preparing-for-hello-tutorial"></a>Hallo-zelfstudie voorbereiden

Hallo PowerShell codefragmenten in deze zelfstudie gebruikt u deze variabelen toostore deze informatie:

```
$rg = "<ResourceGroupName>"
$adls = "<DataLakeStoreAccountName>"
$adla = "<DataLakeAnalyticsAccountName>"
$location = "East US 2"
```

## <a name="get-information-about-a-data-lake-analytics-account"></a>Informatie krijgen over een Data Lake Analytics-account

```
Get-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla  
```

## <a name="submit-a-u-sql-job"></a>Een U-SQL-taak verzenden

Maak een PowerShell-script variabele toohold Hallo U-SQL.

```
$script = @"
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

"@
```

Hallo script verzenden.

```
$job = Submit-AdlJob -AccountName $adla –Script $script
```

U kunt ook Hallo script als een bestand opslaan en verzenden met de volgende opdracht Hallo:

```
$filename = "d:\test.usql"
$script | out-File $filename
$job = Submit-AdlJob -AccountName $adla –ScriptPath $filename
```


Hallo-status van een bepaalde taak ophalen. Deze cmdlet blijven worden gebruiken totdat er Hallo-taak wordt uitgevoerd.

```
$job = Get-AdlJob -AccountName $adla -JobId $job.JobId
```

In plaats van het aanroepen van Get-AdlAnalyticsJob steeds totdat een taak is voltooid, kunt u Hallo wacht AdlJob cmdlet gebruiken.

```
Wait-AdlJob -Account $adla -JobId $job.JobId
```

Hallo-uitvoerbestand downloaden.

```
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "C:\data.csv"
```

## <a name="see-also"></a>Zie ook
* toosee Hallo dezelfde zelfstudie met een ander hulpprogramma, klikt u op Hallo-tabselectors op Hallo Hallo pagina bovenaan.
* toolearn U-SQL, Zie [aan de slag met Azure Data Lake Analytics U-SQL-taal](data-lake-analytics-u-sql-get-started.md).
* Zie [Azure Data Lake Analytics beheren met Azure Portal](data-lake-analytics-manage-use-portal.md) voor informatie over beheertaken.
