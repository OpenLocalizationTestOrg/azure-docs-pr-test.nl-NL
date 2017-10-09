---
title: aaaManage Azure Media Services-Accounts met PowerShell
description: Meer informatie over hoe Azure Media Services toomanage van accounts met PowerShell-cmdlets.
author: Juliako
manager: erikre
editor: 
services: media-services
documentationcenter: 
ms.assetid: 17a10c25-d94f-421c-b6bc-ae0958e2ac96
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/03/2016
ms.author: juliako
ms.openlocfilehash: e8f97bb2393343e45fabf9c437b4fc09f2525dc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-media-services-accounts-with-powershell"></a>Azure Media Services-Accounts met PowerShell beheren
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-create-account.md)
> * [PowerShell](media-services-manage-with-powershell.md)
> * [REST](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> toobe kunnen toocreate een Azure Media Services-account, moet u een Azure-account hebben. Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. Zie <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Gratis proefversie van Azure</a> voor meer informatie.
> 
> 

## <a name="overview"></a>Overzicht
In dit artikel bevat hello Azure PowerShell-cmdlets voor Azure Media Services (AMS) in hello Azure Resource Manager-framework. Hallo-cmdlets bestaan in Hallo **Microsoft.Azure.Commands.Media** naamruimte.

## <a name="versions"></a>Versies
**ApiVersion**: '2015-10-01'

## <a name="new-azurermmediaservice"></a>New-AzureRmMediaService
Hiermee maakt u een mediaservice.

### <a name="syntax"></a>Syntaxis
Parameterset: StorageAccountIdParamSet

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccountId] <string> [-Tags <hashtable>]  [<CommonParameters>]

Parameterset: StorageAccountsParamSet

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccounts] <PSStorageAccount[]> [-Tags <hashtable>]  [<CommonParameters>]

### <a name="parameters"></a>Parameters
**-ResourceGroupName &lt;tekenreeks&gt;**

Geeft de naam Hallo van Hallo resource groep toowhich die deze mediaservice behoort.

| Aliassen | Geen |
| --- | --- |
| Vereist? |De waarde True |
| Positie? |0 |
| Standaardwaarde |Geen |
| Pijpleidinginvoer accepteren? |True(ByPropertyName) |
| Jokertekens accepteren? |ONWAAR |

**-AccountName &lt;tekenreeks&gt;**

Geeft de naam Hallo van Hallo mediaservice.

| Aliassen | Naam |
| --- | --- |
| Vereist? |De waarde True |
| Positie? |1 |
| Standaardwaarde |Geen |
| Pijpleidinginvoer accepteren? |ONWAAR |
| Jokertekens accepteren? |ONWAAR |

**-Locatie &lt;tekenreeks&gt;**

Hiermee geeft u Resourcelocatie Hallo van Hallo mediaservice.

| Aliassen | Geen |
| --- | --- |
| Vereist? |De waarde True |
| Positie? |2 |
| Standaardwaarde |Geen |
| Pijpleidinginvoer accepteren? |True(ByPropertyName) |
| Jokertekens accepteren? |ONWAAR |

**-StorageAccountId &lt;tekenreeks&gt;**

Hiermee geeft u een primaire opslagaccount die zijn gekoppeld aan Hallo mediaservice.

* Nieuwe storage-account (gemaakt met de Hallo Resource Manager-API) alleen wordt ondersteund.
* Hallo storage-account moet aanwezig zijn en heeft dezelfde locatie met mediaservice Hallo Hallo.

| Aliassen | Geen |
| --- | --- |
| Vereist? |De waarde True |
| Positie? |3 |
| Standaardwaarde |Geen |
| Pijpleidinginvoer accepteren? |True(ByPropertyName) |
| Naam van de parameter |StorageAccountIdParamSet |
| Jokertekens accepteren? |ONWAAR |

**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**

Hiermee geeft u opslagaccounts die zijn gekoppeld aan Hallo mediaservice.

* Nieuwe storage-account (gemaakt met de Hallo Resource Manager-API) alleen wordt ondersteund.
* Hallo storage-account moet aanwezig zijn en heeft dezelfde locatie met mediaservice Hallo Hallo.
* Slechts één opslagaccount kan worden opgegeven als primaire.

| Aliassen | Geen |
| --- | --- |
| Vereist? |De waarde True |
| Positie? |3 |
| Standaardwaarde |Geen |
| Pijpleidinginvoer accepteren? |True(ByPropertyName) |
| Naam van de parameter |StorageAccountsParamSet |
| Jokertekens accepteren? |ONWAAR |

**-Tags &lt;hashtabel&gt;**

Hiermee geeft u een hash-tabel van Hallo-labels die gekoppeld aan Hallo mediaservice zijn.

* Voorbeeld: @{"tag1 isgelijkteken (=) value1";" tag2 ' =: value2 "}

| Aliassen | Geen |
| --- | --- |
| Vereist? |ONWAAR |
| Positie? |Met de naam |
| Standaardwaarde |Geen |
| Pijpleidinginvoer accepteren? |ONWAAR |
| Jokertekens accepteren? |ONWAAR |

**&lt;CommandParameters&gt;**

Deze cmdlet ondersteunt Hallo algemene parameters:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, -InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction en -WarningVariable.

### <a name="inputs"></a>Invoer
Hallo-invoertype is Hallo Hallo type objecten dat u toohello cmdlet kunt overbrengen.

### <a name="outputs"></a>uitvoer
Hallo-uitvoertype is Hallo type Hallo-objecten dat Hallo cmdlet verzendt.

## <a name="set-azurermmediaservice"></a>Set-AzureRmMediaService
Een mediaservice-updates.

### <a name="syntax"></a>Syntaxis
    Set-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Tags <hashtable>] [-StorageAccounts <PSStorageAccount[]>]  [<CommonParameters>]

### <a name="parameters"></a>Parameters
**-ResourceGroupName &lt;tekenreeks&gt;**

Geeft de naam Hallo van Hallo resource groep toowhich die deze mediaservice behoort.

| Aliassen | Geen |
| --- | --- |
| Vereist? |De waarde True |
| Positie? |0 |
| Standaardwaarde |Geen |
| Pijpleidinginvoer accepteren? |True(ByPropertyName) |
| Jokertekens accepteren? |ONWAAR |

**-AccountName &lt;tekenreeks&gt;**

Geeft de naam Hallo van Hallo mediaservice.

| Aliassen | Naam |
| --- | --- |
| Vereist? |True |
| Positie? |1 |
| Standaardwaarde |Geen |
| Pijpleidinginvoer accepteren? |True(ByPropertyName) |
| Jokertekens accepteren? |False |

**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**

Hiermee geeft u opslagaccounts die zijn gekoppeld aan Hallo mediaservice.

* Nieuwe storage-account (gemaakt met de Hallo Resource Manager-API) alleen wordt ondersteund.
* Hallo storage-account moet aanwezig zijn en heeft dezelfde locatie met mediaservice Hallo Hallo.
* Slechts één opslagaccount kan worden opgegeven als primaire.

| Aliassen | Geen |
| --- | --- |
| Vereist? |ONWAAR |
| Positie? |Met de naam |
| Standaardwaarde |Geen |
| Pijpleidinginvoer accepteren? |True(ByPropertyName) |
| Naam van de parameter |StorageAccountsParamSet |
| Jokertekens accepteren? |ONWAAR |

**-Tags &lt;hashtabel&gt;**

Hiermee geeft u een hash-tabel van Hallo-labels die gekoppeld aan deze mediaservice zijn.

* Hallo-labels die gekoppeld aan Hallo mediaservice zijn worden vervangen door de waarde die is opgegeven door de klant Hallo.

| Aliassen | Geen |
| --- | --- |
| Vereist? |False |
| Positie? |Met de naam |
| Standaardwaarde |Geen |
| Pijpleidinginvoer accepteren? |True(ByPropertyName) |
| Jokertekens accepteren? |ONWAAR |

**&lt;CommandParameters&gt;**

Deze cmdlet ondersteunt Hallo algemene parameters:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, -InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction en -WarningVariable.

### <a name="inputs"></a>Invoer
Hallo-invoertype is Hallo Hallo type objecten dat u toohello cmdlet kunt overbrengen.

### <a name="outputs"></a>uitvoer
Hallo-uitvoertype is Hallo type Hallo-objecten dat Hallo cmdlet verzendt.

## <a name="remove-azurermmediaservice"></a>Remove-AzureRmMediaService
Hiermee verwijdert u een mediaservice.

### <a name="syntax"></a>Syntaxis
    Remove-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a>Parameters
**-ResourceGroupName &lt;tekenreeks&gt;**

Geeft de naam Hallo van Hallo resource groep toowhich die deze mediaservice behoort.

| Aliassen | Geen |
| --- | --- |
| Vereist? |De waarde True |
| Positie? |0 |
| Standaardwaarde |Geen |
| Pijpleidinginvoer accepteren? |True(ByPropertyName) |
| Jokertekens accepteren? |ONWAAR |

**-AccountName &lt;tekenreeks&gt;**

Geeft de naam Hallo van Hallo mediaservice.

| Aliassen | Geen |
| --- | --- |
| Vereist? |De waarde True |
| Positie? |2 |
| Standaardwaarde |Geen |
| Pijpleidinginvoer accepteren? |True(ByPropertyName) |
| Jokertekens accepteren? |False |

**&lt;CommandParameters&gt;**

Deze cmdlet ondersteunt Hallo algemene parameters:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, -InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction en -WarningVariable.

### <a name="inputs"></a>Invoer
Hallo-invoertype is Hallo Hallo type objecten dat u toohello cmdlet kunt overbrengen.

### <a name="outputs"></a>uitvoer
Hallo-uitvoertype is Hallo type Hallo-objecten dat Hallo cmdlet verzendt.

## <a name="get-azurermmediaservice"></a>Get-AzureRmMediaService
Hiermee haalt u alle mediaservices in een resourcegroep of een mediaservice met een bepaalde naam.

### <a name="syntax"></a>Syntaxis
ParameterSet: ResourceGroupParameterSet

    Get-AzureRmMediaService [-ResourceGroupName] <string>  [<CommonParameters>]    

ParameterSet: AccountNameParameterSet

    Get-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a>Parameters
**-ResourceGroupName &lt;tekenreeks&gt;**

Geeft de naam Hallo van Hallo resource groep toowhich die deze mediaservice behoort.

| Aliassen | Geen |
| --- | --- |
| Vereist? |De waarde True |
| Positie? |0 |
| Standaardwaarde |Geen |
| Pijpleidinginvoer accepteren? |True(ByPropertyName) |
| Naam van de parameter |ResourceGroupParameterSet, AccountNameParameterSet |

Jokertekens accepteren?   ONWAAR

**-AccountName &lt;tekenreeks&gt;**

Geeft de naam Hallo van Hallo mediaservice.

| Aliassen | Geen |
| --- | --- |
| Vereist? |De waarde True |
| Positie? |1 |
| Standaardwaarde |Geen |
| Pijpleidinginvoer accepteren? |True(ByPropertyName) |
| Naam van de parameter |AccountNameParameterSet |
| Jokertekens accepteren? |ONWAAR |

**&lt;CommandParameters&gt;**

Deze cmdlet ondersteunt Hallo algemene parameters:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, -InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction en -WarningVariable.

### <a name="inputs"></a>Invoer
Hallo-invoertype is Hallo Hallo type objecten dat u toohello cmdlet kunt overbrengen.

### <a name="outputs"></a>uitvoer
Hallo-uitvoertype is Hallo type Hallo-objecten dat Hallo cmdlet verzendt.

## <a name="get-azurermmediaservicekeys"></a>Get-AzureRmMediaServiceKeys
Sleutels van een mediaservice opgehaald.

### <a name="syntax"></a>Syntaxis
    Get-AzureRmMediaServiceKeys [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a>Parameters
**-ResourceGroupName &lt;tekenreeks&gt;**

Geeft de naam Hallo van Hallo resource groep toowhich die deze mediaservice behoort.

| Aliassen | Geen |
| --- | --- |
| Vereist? |De waarde True |
| Positie? |0 |
| Standaardwaarde |Geen |
| Pijpleidinginvoer accepteren? |True(ByPropertyName) |
| Jokertekens accepteren? |ONWAAR |

**-AccountName &lt;tekenreeks&gt;**

Geeft de naam Hallo van Hallo mediaservice.

| Aliassen | Geen |
| --- | --- |
| Vereist? |De waarde True |
| Positie? |1 |
| Standaardwaarde |Geen |
| Pijpleidinginvoer accepteren? |True(ByPropertyName) |
| Jokertekens accepteren? |ONWAAR |

**&lt;CommandParameters&gt;**

Deze cmdlet ondersteunt Hallo algemene parameters:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, -InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction en -WarningVariable.

### <a name="inputs"></a>Invoer
Hallo-invoertype is Hallo Hallo type objecten dat u toohello cmdlet kunt overbrengen.

### <a name="outputs"></a>uitvoer
Hallo-uitvoertype is Hallo type Hallo-objecten dat Hallo cmdlet verzendt.

## <a name="set-azurermmediaservicekey"></a>Set-AzureRmMediaServiceKey
Genereert opnieuw een primaire of secundaire sleutel van een mediaservice.

### <a name="syntax"></a>Syntaxis
    Set-AzureRmMediaServiceKey [-ResourceGroupName] <string> [-AccountName] <string> [-KeyType] <KeyType> {Primary | Secondary}  [<CommonParameters>]

### <a name="parameters"></a>Parameters
**-ResourceGroupName &lt;tekenreeks&gt;**

Geeft de naam Hallo van Hallo resource groep toowhich die deze mediaservice behoort.

| Aliassen | Geen |
| --- | --- |
| Vereist? |De waarde True |
| Positie? |0 |
| Standaardwaarde |Geen |
| Pijpleidinginvoer accepteren? |True(ByPropertyName) |
| Jokertekens accepteren? |ONWAAR |

**-AccountName &lt;tekenreeks&gt;**

Geeft de naam Hallo van Hallo mediaservice.

| Aliassen | Geen |
| --- | --- |
| Vereist? |De waarde True |
| Positie? |1 |
| Standaardwaarde |Geen |
| Pijpleidinginvoer accepteren? |True(ByPropertyName) |
| Jokertekens accepteren? |ONWAAR |

**KeyType - &lt;KeyType&gt;**

Hiermee geeft u Hallo sleuteltype van Hallo mediaservice.

* Primaire of secundaire

| Aliassen | Geen |
| --- | --- |
| Vereist? |De waarde True |
| Positie? |2 |
| Standaardwaarde |Geen |
| Pijpleidinginvoer accepteren? |ONWAAR |
| Jokertekens accepteren? |ONWAAR |

**&lt;CommandParameters&gt;**

Deze cmdlet ondersteunt Hallo algemene parameters:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, -InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction en -WarningVariable.

### <a name="inputs"></a>Invoer
Hallo-invoertype is Hallo Hallo type objecten dat u toothe cmdlet kunt overbrengen.

### <a name="outputs"></a>uitvoer
Hallo-uitvoertype is Hallo type Hallo-objecten dat Hallo cmdlet verzendt.

## <a name="sync-azurermmediaservicestoragekeys"></a>Sync-AzureRmMediaServiceStorageKeys
Toegangscodes voor opslag voor een opslagaccount die is gekoppeld aan Hallo mediaservice synchroniseert.

### <a name="syntax"></a>Syntaxis
    Sync-AzureRmMediaServiceStorageKeys [-ResourceGroupName] <string> [-MediaServiceAccountName] <string>    [-StorageAccountId] <string>  [<CommonParameters>]

### <a name="parameters"></a>Parameters
**-ResourceGroupName &lt;tekenreeks&gt;**

Geeft de naam Hallo van Hallo resource groep toowhich die deze mediaservice behoort.

| Aliassen | Geen |
| --- | --- |
| Vereist? |De waarde True |
| Positie? |0 |
| Standaardwaarde |Geen |
| Pijpleidinginvoer accepteren? |True(ByPropertyName) |
| Jokertekens accepteren? |ONWAAR |

**-AccountName &lt;tekenreeks&gt;**

Geeft de naam Hallo van Hallo mediaservice.

| Aliassen | Geen |
| --- | --- |
| Vereist? |De waarde True |
| Positie? |1 |
| Standaardwaarde |Geen |
| Pijpleidinginvoer accepteren? |True(ByPropertyName) |
| Jokertekens accepteren? |ONWAAR |

**-StorageAccountId &lt;tekenreeks&gt;**

Hiermee geeft u Hallo storage-account zijn gekoppeld aan Hallo mediaservice.

| Aliassen | Id |
| --- | --- |
| Vereist? |De waarde True |
| Positie? |2 |
| Standaardwaarde |Geen |
| Pijpleidinginvoer accepteren? |True(ByPropertyName) |
| Jokertekens accepteren? |ONWAAR |

**&lt;CommandParameters&gt;**

Deze cmdlet ondersteunt Hallo algemene parameters:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, -InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction en -WarningVariable.

### <a name="inputs"></a>Invoer
Hallo-invoertype is Hallo Hallo type objecten dat u toohello cmdlet kunt overbrengen.

### <a name="outputs"></a>uitvoer
Hallo-uitvoertype is Hallo type Hallo-objecten dat Hallo cmdlet verzendt.

## <a name="next-step"></a>Volgende stap
Media Services-leertrajecten uitchecken.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

